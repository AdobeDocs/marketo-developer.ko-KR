---
title: "일괄 가져오기"
feature: REST API
description: "개인 데이터를 일괄 가져오는 중"
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '554'
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

대량 가져오기 API는 다른 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용합니다.  이를 위해서는 쿼리-문자열 매개 변수로 포함할 유효한 액세스 토큰이 필요합니다 `access_token={_AccessToken_}`또는 HTTP 헤더로서 `Authorization: Bearer {_AccessToken_}`.

## 제한

- 최대 동시 가져오기 작업: 2
- 대기 중인 최대 가져오기 작업(현재 가져오는 작업 포함): 10
- 가져오기 파일의 최대 크기: 10MB

## 권한

일괄 가져오기는 Marketo REST API와 동일한 권한 모델을 사용하며, 각 끝점 세트에 특정 권한이 필요하지만 사용하기 위해 별도의 특수 권한이 필요하지 않습니다.

## 레코드 작업

일괄 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업입니다. 데이터베이스에서 일치하는 레코드가 발견되면 업데이트됩니다. 그렇지 않으면 새 레코드가 만들어집니다. 대량 가져오기 응답은 지정된 레코드가 업데이트되었는지 또는 삽입되었는지 여부를 나타내지 않습니다.

## 작업 생성

Marketo의 벌크 가져오기 API는 데이터 가져오기를 실행하는 작업 개념을 사용합니다. 다음을 사용하여 간단한 리드 가져오기 작업을 만드는 방법을 살펴보겠습니다. [리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) 엔드포인트.  이 엔드포인트는 다음을 사용합니다. [content-type으로서의 multipart/form-data](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html). 이 방법은 올바른 이해에 까다로울 수 있으므로 가장 좋은 방법은 선택한 언어에 HTTP 지원 라이브러리를 사용하는 것입니다.  만약 여러분이 단지 발을 적시는 것이라면, 우리는 여러분이 [컬](https://curl.se/).

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

| 매개 변수 | 데이터 유형 | 참고 사항 |
|---|---|---|
| 형식 | 문자열 | 쉼표로 구분된 값, 탭으로 구분된 값 및 세미콜론으로 구분된 값에 대한 옵션을 사용하여 가져온 데이터의 파일 형식을 결정합니다. CSV, SSV, TSV 중 하나를 허용합니다. 형식은 기본적으로 CSV로 설정됩니다. |
| 파일 | 문자열 | 데이터는 파일의 여러 부분 양식 데이터를 통해 지정됩니다. |


## 폴링 작업 상태

작업 상태 확인은 다음을 사용하여 간단합니다 [가져오기 리드 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET) 엔드포인트.

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

더 이너 `status` 구성원은 작업의 진행 상황을 나타내며 큐에 있음, 가져오기, 완료, 실패 값 중 하나일 수 있습니다. 이 경우 우리의 작업이 완료되었으므로 우리는 투표를 중지할 수 있습니다.

## 실패

실패는 `numOfRowsFailed` 가져오기 리드 상태 가져오기 응답의 특성. If `numOfRowsFailed` 이 0보다 큰 경우 해당 값은 발생한 실패 수를 나타냅니다.

실패한 행의 레코드와 원인을 검색하려면 다음을 사용하여 실패 파일을 검색해야 합니다 [가져오기 리드 가져오기 실패](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET) 엔드포인트.

```
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

이 파일은 레코드가 실패한 이유를 나타내는 메시지와 함께 실패한 행을 나타냅니다.
