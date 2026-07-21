---
title: 일괄 가져오기
feature: REST API
description: 다중 부분 업로드를 통해 리드, 사용자 지정 개체 및 프로그램 구성원을 로드하고 비동기 작업을 생성하며, 폴링 상태가 설정되고, 오류가 처리되는 Marketo 일괄 가져오기.
exl-id: f7922fd2-8408-4d04-8955-0f8f58914d24
TQID: https://experienceleague.adobe.com/lr9dyX-fY-oJ2LM5P0zE1m24HtFYKQYYbxMkVe--PkE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 538
ht-degree: 2%

---

# 일괄 가져오기

일괄 가져오기는 대규모 사용자 및 사용자 관련 데이터 세트를 삽입하기 위한 인터페이스를 제공합니다. 세 가지 객체 유형을 가져올 수 있습니다.

- 잠재 고객 (개인)
- 사용자 정의 오브젝트
- 프로그램 구성원

일괄 가져오기를 수행하려면 업로드된 파일을 읽는 작업을 만듭니다. 작업이 비동기적으로 실행되므로 폴링하여 가져오기 상태를 검색합니다.

RFC 2399에 따라 HTTP `multipart/form-data`을(를) 사용하여 파일을 업로드합니다.

다른 끝점과 달리 Bulk API 끝점에는 `/rest` 접두사가 붙지 않습니다.

## 인증

대량 가져오기 API는 다른 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용합니다. `Authorization: Bearer {_AccessToken_}` HTTP 헤더에서 올바른 액세스 토큰을 보냅니다.

>[!IMPORTANT]
>
>**access_token** 쿼리 매개 변수를 사용하는 인증 지원이 2025년 6월 30일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 **인증** 헤더를 사용하도록 업데이트해야 합니다. 새 개발에서는 **Authorization** 헤더만 사용해야 합니다.

## 제한

- 최대 동시 가져오기 작업: 2개
- 현재 가져오는 작업을 포함하여 큐에 추가된 최대 가져오기 작업: 10개
- 최대 가져오기 파일 크기: 10MB

## 권한

대량 가져오기는 Marketo REST API와 동일한 권한 모델을 사용합니다. 추가 권한은 필요하지 않지만 각 엔드포인트 세트에는 특정 권한이 필요합니다.

## 레코드 작업

일괄 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업입니다. 데이터베이스에 일치하는 레코드가 있으면 해당 레코드가 업데이트됩니다. 그렇지 않으면 레코드가 만들어집니다.

일괄 가져오기 응답은 개별 레코드가 업데이트되었는지 또는 삽입되었는지 여부를 나타내지 않습니다.

## 작업 생성

[리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/importLeadUsingPOST) 끝점을 호출하여 리드 가져오기 작업을 만듭니다. 이 끝점은 [multipart/form-data를 content-type](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html)&#x200B;(으)로 사용합니다.

원하는 언어에 대해 HTTP 지원 라이브러리를 사용하여 다중 부분 요청을 구성합니다. [curl](https://curl.se/)을(를) 사용하여 시작할 수도 있습니다.

```http
POST /bulk/v1/leads.json?format=csv
```

```text
Content-Type: multipart/form-data; boundary=--------------------------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```text
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

firstName,lastName,email
Able,Baker,ablebaker@marketo.com
Charlie,Dog,charliedog@marketo.com
Easy,Fox,easyfox@marketo.com
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

이 요청은 CSV 파일 `leads.csv`에서 값을 가져오는 작업을 만듭니다.

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

응답이 `batchId`을(를) 반환합니다. 이 값을 사용하여 작업 상태를 확인합니다.

### 일반 매개 변수

각 작업 생성 끝점은 가져오기 파일 구성을 위한 매개 변수를 공유합니다. 가져오기 하위 유형은 추가 매개 변수도 지원할 수 있습니다.

| 매개변수 | 데이터 유형 | 참고 |
| --- | --- | --- |
| 형식 | 문자열 | 쉼표로 구분된 값, 탭으로 구분된 값 및 세미콜론으로 구분된 값에 대한 옵션을 사용하여 가져온 데이터의 파일 형식을 결정합니다. CSV, SSV, TSV 중 하나를 허용합니다. 형식은 기본적으로 CSV로 설정됩니다. |
| 파일 | 문자열 | 데이터는 파일의 여러 부분 양식 데이터를 통해 지정됩니다. |

## 폴링 작업 상태

`batchId`을(를) [가져오기 리드 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/getImportLeadStatusUsingGET) 끝점에 전달하여 작업 상태를 검색합니다.

```http
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

`status` 구성원은 작업의 진행 상황을 나타냅니다. 해당 값은 `Queued`, `Importing`, `Complete` 또는 `Failed`일 수 있습니다.

이 예에서는 작업이 완료되므로 폴링을 중지할 수 있습니다.

## 실패

가져오기 리드 상태 가져오기 응답의 `numOfRowsFailed` 특성은 실패한 행 수를 나타냅니다. 값이 0보다 크면 오류가 발생했음을 의미합니다.

실패한 레코드와 그 원인을 검색하려면 [가져오기 리드 실패 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/getImportLeadFailuresUsingGET) 끝점을 사용하십시오.

```http
GET /bulk/v1/leads/batch/{batchId}/failures.json
```

실패 파일은 실패한 각 행을 식별하고 레코드가 실패한 이유를 설명합니다.
