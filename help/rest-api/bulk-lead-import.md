---
title: 벌크 리드 가져오기
feature: REST API
description: CSV TSV 또는 SSV를 사용하여 Marketo에서 비동기 대량 리드 가져오기를 만들고 모니터링합니다.
exl-id: 615f158b-35f9-425a-b568-0a7041262504
TQID: https://experienceleague.adobe.com/UamXYWis5J1ERqnp5lAnfUf3pFcgfSOLfKRXRB-Yg4I
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: e2290edd-b061-4880-9d79-dee306cf5aa9
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 623
ht-degree: 0%

---

# 벌크 리드 가져오기

[대량 리드 가져오기 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads)

[일괄 API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Leads/operation/importLeadUsingPOST)를 사용하여 많은 리드 레코드를 비동기적으로 가져옵니다. 쉼표, 탭 또는 세미콜론으로 구분된 10MB 미만의 플랫 파일로 레코드를 제공합니다.

대량 리드 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업만 지원합니다.

## 처리 제한

각 벌크 가져오기 요청은 선입선출(FIFO) 큐에 작업으로 추가됩니다. 다음과 같은 제한이 적용됩니다.

- 최대 두 개의 작업을 동시에 처리할 수 있습니다.
- 처리 중인 두 작업을 포함하여 최대 10개의 작업이 대기열에 있을 수 있습니다.

최대 작업 10개를 초과하면 API에서 `1016, Too many imports` 오류를 반환합니다.

## 파일 가져오기

파일의 첫 행은 각 행의 값이 매핑되는 REST API 필드를 나열하는 헤더여야 합니다. 일반적인 파일은 다음 패턴을 따릅니다.

```csv
email,firstName,lastName
test@example.com,John,Doe
```

`externalCompanyId`을(를) 사용하여 잠재 고객 레코드를 회사 레코드에 연결합니다. `externalSalesPersonId`을(를) 사용하여 잠재 고객 레코드를 영업 사원 레코드에 연결합니다.

`multipart/form-data` 콘텐츠 형식을 사용하여 요청을 보냅니다. 기존 라이브러리 구현을 사용하여 다중 파트 요청을 구성합니다.

## 작업 생성

일괄 가져오기 작업을 만들려면 콘텐츠 형식을 `multipart/form-data`(으)로 설정하고 다음 매개 변수를 포함하십시오.

- `file`: 파일 내용을 가져오는 중입니다.
- `format`: 파일 형식입니다. 유효한 값은 `csv`, `tsv` 및 `ssv`입니다.

```http
POST /bulk/v1/leads.json?format=csv
```

```text
Content-Type: multipart/form-data; boundary=------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```text
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

firstName,lastName,email,company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

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

이 끝점은 [multipart/form-data를 content-type](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html)&#x200B;(으)로 사용합니다. 원하는 언어에 대해 HTTP 지원 라이브러리를 사용하여 요청을 올바르게 구성하십시오. 다음 예제에서는 명령줄의 cURL을 사용합니다.

```bash
curl -i -F format=csv -F file=@lead_data.csv -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/leads.json
```

이 예제에서 `lead_data.csv` 가져오기 파일에는 다음 데이터가 포함되어 있습니다.

```text
firstName,lastName,email,company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
```

다음과 같은 선택적 매개 변수를 포함할 수도 있습니다.

- `lookupField`: 중복 제거에 사용되는 필드를 선택하고 기본값은 `email`입니다. `id`을(를) 지정하여 &quot;업데이트 전용&quot; 작업을 수행하십시오.
- `listId`: 정적 목록을 선택합니다. 가져온 리드는 가져오기로 생성되거나 업데이트된 레코드 외에 이 목록의 멤버가 됩니다.
- `partitionName`: 가져올 파티션을 선택하십시오. 자세한 내용은 작업 공간 및 파티션 섹션을 참조하십시오.

API는 비동기적이므로 응답에는 개별 성공 및 실패 대신 `batchId` 및 `status` 필드가 포함되어 있습니다. 상태는 `Queued`, `Importing` 또는 `Failed`일 수 있습니다.

작업 상태를 확인하고 완료 후 오류 또는 경고를 검색하려면 `batchId`을(를) 유지합니다. `batchId`은(는) 7일 동안 유효합니다.

## 폴링 작업 상태

가져오기 리드 상태 가져오기 API를 사용하여 지연 요구 사항 및 API 호출 제한에 따라 5~30초마다 작업을 폴링합니다.

```http
GET /bulk/v1/leads/batch/{id}.json
```

```json
{
   "requestId":"8136#146daebc2ed",
   "success":true,
   "result":[
      {
         "batchId":1022,
         "status":"Complete",
         "numOfLeadsProcessed":2,
         "numOfRowsFailed":1,
         "numOfRowsWithWarning":0,
         "message":"Import completed with errors, 2 records imported (2 members), 1 failed"
      }
   ]
}
```

이 응답은 완료된 가져오기를 표시합니다. 상태는 다음 값 중 하나일 수 있습니다.

- 완료
- 대기열에 추가됨
- 가져오는 중
- 실패

작업이 완료되면 응답에는 처리, 실패 및 처리된 행 수가 경고와 함께 나열됩니다. 상태가 `Failed`인 경우 `message` 매개 변수가 오류 메시지를 제공할 수도 있습니다.

## 실패

가져오기 리드 상태 가져오기 응답의 `numOfRowsFailed` 특성은 실패한 행 수를 나타냅니다. 값이 0보다 크면 오류가 발생했음을 의미합니다.

실패한 레코드와 그 원인을 검색하려면 실패 파일을 요청합니다.

```http
GET /bulk/v1/leads/batch/{id}/failures.json
```

API는 실패한 각 행을 식별하고 레코드가 실패한 이유를 설명하는 파일을 반환합니다. 파일이 작업을 만드는 동안 `format` 매개 변수로 지정된 형식을 사용합니다. 각 레코드의 추가 필드는 오류를 설명합니다.

## 경고

가져오기 리드 상태 가져오기 응답의 `numOfRowsWithWarning` 특성은 경고가 있는 행 수를 나타냅니다. 값이 0보다 크면 경고가 발생한 것입니다.

영향을 받는 레코드와 그 원인을 검색하려면 경고 파일을 요청하십시오.

```http
GET /bulk/v1/leads/batch/{id}/warnings.json
```

API는 경고가 있는 각 행을 식별하고 경고가 발생한 이유를 설명하는 파일을 반환합니다. 파일이 작업을 만드는 동안 `format` 매개 변수로 지정된 형식을 사용합니다. 각 레코드의 추가 필드는 경고를 설명합니다.
