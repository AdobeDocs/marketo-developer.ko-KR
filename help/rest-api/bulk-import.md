---
title: 일괄 가져오기
feature: REST API
description: 개인 데이터를 일괄 가져오는 중.
exl-id: f7922fd2-8408-4d04-8955-0f8f58914d24
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# 일괄 가져오기

Marketo은 일괄 가져오기라고 하는 대규모 개인 및 개인 관련 데이터 세트를 삽입하기 위한 인터페이스를 제공합니다. 현재 인터페이스는 다음 세 가지 객체 유형에 대해 제공됩니다.

- 잠재 고객 (개인)
- 사용자 지정 개체
- 프로그램 구성원

대량 가져오기는 작업을 만든 다음 작업이 파일 읽기가 완료될 때까지 기다려서 수행됩니다. 이러한 작업은 비동기적으로 실행되며 폴링하여 가져오기 상태를 검색할 수 있습니다. 파일은 RFC 2399에 따라 HTTP multipart/form-data를 사용하여 업로드됩니다.

벌크 API 끝점에는 다른 끝점처럼 &#39;/rest&#39; 접두사가 붙지 않습니다.

## 인증

대량 가져오기 API는 다른 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용합니다.  HTTP 헤더 `Authorization: Bearer {_AccessToken_}`(으)로 보낸 올바른 액세스 토큰이 필요합니다.

>[!IMPORTANT]
>
>**access_token** 쿼리 매개 변수를 사용하는 인증 지원이 2025년 6월 30일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 **인증** 헤더를 사용하도록 업데이트해야 합니다. 새 개발에서는 **Authorization** 헤더만 사용해야 합니다.

## 제한

- 최대 동시 가져오기 작업: 2
- 대기 중인 최대 가져오기 작업(현재 가져오는 작업 포함): 10
- 가져오기 파일의 최대 크기: 10MB

## 권한

일괄 가져오기는 Marketo REST API와 동일한 권한 모델을 사용하며, 각 끝점 세트에 특정 권한이 필요하지만 사용하기 위해 별도의 특수 권한이 필요하지 않습니다.

## 레코드 작업

일괄 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업입니다. 데이터베이스에서 일치하는 레코드가 발견되면 업데이트됩니다. 그렇지 않으면 새 레코드가 만들어집니다. 대량 가져오기 응답은 지정된 레코드가 업데이트되었는지 또는 삽입되었는지 여부를 나타내지 않습니다.

## 작업 생성

Marketo의 벌크 가져오기 API는 데이터 가져오기를 실행하는 작업 개념을 사용합니다. [리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) 끝점을 사용하여 간단한 리드 가져오기 작업을 만드는 방법을 살펴보겠습니다.  이 끝점은 [multipart/form-data를 content-type](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html)&#x200B;(으)로 사용합니다. 이 방법은 올바른 이해에 까다로울 수 있으므로 가장 좋은 방법은 선택한 언어에 HTTP 지원 라이브러리를 사용하는 것입니다.  발을 막 젖게 하는 경우에는 [curl](https://curl.se/)을(를) 사용하는 것이 좋습니다.

```
POST /bulk/v1/leads.json?format=csv
```

```
Content-Type: multipart/form-data; boundary=--------------------------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

firstName,lastName,email
Able,Baker,ablebaker@marketo.com
Charlie,Dog,charliedog@marketo.com
Easy,Fox,easyfox@marketo.com
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

이 요청은 &quot;FirstName&quot;, &quot;LastName&quot;, &quot;Email&quot;, &quot;Company&quot; 열 헤더로 &quot;leads.csv&quot;라는 CSV 파일에 포함된 값을 가져오는 작업을 구성합니다.

```json
{
    "requestId": "d01f#15d672f8560",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Queued"
        }
    ],
    "success": true
}
```

작업을 제출하면 batchId가 반환되고 이후 해당 상태를 확인하는 데 사용할 수 있습니다.

### 일반 매개 변수

각 작업 생성 끝점은 대량 추출 작업의 파일 형식, 필드 이름 및 필터를 구성하기 위한 몇 가지 일반적인 매개 변수를 공유합니다.  추출 작업의 각 하위 유형에는 추가 매개 변수가 있을 수 있습니다.

| 매개변수 | 데이터 유형 | 참고 |
|---|---|---|
| 형식 | 문자열 | 쉼표로 구분된 값, 탭으로 구분된 값 및 세미콜론으로 구분된 값에 대한 옵션을 사용하여 가져온 데이터의 파일 형식을 결정합니다. CSV, SSV, TSV 중 하나를 허용합니다. 형식은 기본적으로 CSV로 설정됩니다. |
| 파일 | 문자열 | 데이터는 파일의 여러 부분 양식 데이터를 통해 지정됩니다. |

## 폴링 작업 상태

[가져오기 리드 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET) 끝점을 사용하여 작업 상태를 간단하게 확인할 수 있습니다.

```
GET /bulk/v1/leads/batch/{batchId}.json
```

```json
{
    "requestId": "1f63#15d6738fd15",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Complete",
            "numOfLeadsProcessed": 3,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "message": "Import succeeded, 3 records imported (3 members)"
        }
    ],
    "success": true
}
```

내부 `status` 구성원은 작업의 진행 상황을 나타내며 [큐에 있음], [가져오기], [완료], [실패] 값 중 하나일 수 있습니다. 이 경우 우리의 작업이 완료되었으므로 우리는 투표를 중지할 수 있습니다.

## 실패

가져오기 리드 상태 가져오기 응답에서 `numOfRowsFailed` 특성으로 오류가 표시됩니다. `numOfRowsFailed`이(가) 0보다 크면 이 값은 발생한 실패 횟수를 나타냅니다.

실패한 행의 레코드와 원인을 검색하려면 [가져오기 리드 실패 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET) 끝점을 사용하여 실패 파일을 검색해야 합니다.

```
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

이 파일은 레코드가 실패한 이유를 나타내는 메시지와 함께 실패한 행을 나타냅니다.
