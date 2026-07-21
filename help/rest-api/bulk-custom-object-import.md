---
title: 대량 사용자 지정 개체 가져오기
feature: Custom Objects
description: CSV, TSV 또는 SSV 파일을 사용하여 REST를 통해 Marketo 사용자 지정 개체를 대량 가져오는 방법에 대해 알아봅니다.
exl-id: e795476c-14bc-4e8c-b611-1f0941a65825
TQID: https://experienceleague.adobe.com/C1LKLZDEvv95XXH3AEoxIXsLK55tgKTrvyxvs4LnYWw
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 736
ht-degree: 0%

---

# 대량 사용자 지정 개체 가져오기

[대량 사용자 지정 개체 가져오기 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Custom-Objects)

대량 API를 사용하여 많은 사용자 지정 개체 레코드를 비동기적으로 가져올 수 있습니다. 쉼표, 탭 또는 세미콜론으로 구분된 10MB 미만의 플랫 파일로 레코드를 제공합니다. 파일이 더 큰 경우 API는 HTTP 413 상태 코드를 반환합니다.

파일 내용은 사용자 지정 개체 정의에 따라 다릅니다. 첫 번째 행은 헤더여야 하며, 모든 헤더 필드는 API 이름과 일치해야 합니다. 나머지 행에는 각각 1개의 레코드가 포함됩니다.

대량 사용자 지정 개체 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업만 지원합니다.

## 처리 제한

각 벌크 가져오기 요청은 선입선출(FIFO) 큐에 작업으로 추가됩니다. 다음과 같은 제한이 적용됩니다.

- 최대 두 개의 작업을 동시에 처리할 수 있습니다.
- 처리 중인 두 작업을 포함하여 최대 10개의 작업이 대기열에 있을 수 있습니다.

최대 작업 10개를 초과하면 API에서 `1016, Too many imports` 오류를 반환합니다.

## 사용자 지정 개체 예

벌크 API를 사용하기 전에 Marketo 관리 UI를 사용하여 [사용자 지정 개체를 만듭니다](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects).

이 예제에서는 `Color`, `Make`, `Model` 및 `VIN` 필드가 있는 `Car` 사용자 지정 개체를 사용합니다. 중복 제거에는 VIN 필드가 사용됩니다. 관리 UI 화면에서는 벌크 API 끝점에 필요한 API 이름을 강조 표시합니다.

![사용자 지정 개체 삽입](assets/bulk-insert-co-car-1.png)

다음은 관리 UI에 표시되는 사용자 지정 개체 필드입니다.

![사용자 지정 개체 필드 삽입](assets/bulk-insert-co-car-fields.png)

### API 이름

프로그래밍 방식으로 API 이름을 검색하려면 사용자 지정 개체 API 이름을 [사용자 지정 개체 설명](#describe) 끝점에 전달하십시오.

```text
/rest/v1/customobjects/{apiName}/describe.json
```

```json
{
    "requestId": "46ff#15a686e66de",
    "result": [
        {
            "name": "car_c",
            "displayName": "Car",
            "description": "It is a car.",
            "createdAt": "2017-02-22T19:55:51Z",
            "updatedAt": "2017-02-22T19:55:51Z",
            "idField": "marketoGUID",
            "dedupeFields": [
                "vin"
            ],
            "searchableFields": [
                [
                    "vin"
                ],
                [
                    "marketoGUID"
                ]
            ],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false
                },
                {
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true
                }
            ]
        }
    ],
    "success": true
}
```

### 파일 가져오기

다음 CSV 파일에는 세 개의 `Car` 사용자 지정 개체 레코드가 포함되어 있습니다.

```text
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

첫 번째 줄은 헤더입니다. 2-4행에는 사용자 지정 개체 데이터 레코드가 포함되어 있습니다.

## 작업 생성

대량 가져오기 작업을 만들려면 [사용자 지정 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Identity/operation/identityUsingPOST) 끝점의 경로에 사용자 지정 개체 API 이름을 포함하십시오. 다음 매개 변수를 포함합니다.

- `file`: 가져오기 파일의 이름입니다.
- `format`: 파일 구분 기호 형식(`csv`, `tsv` 또는 `ssv`)입니다.

```http
POST /bulk/v1/customobjects/{apiName}/import.json?format=csv
```

```text
Transfer-Encoding: chunked
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXjWP6BP8Ciq6bPeo
Content-Length: 290
Host: <munchkinId>.mktorest.com
```

```text
------WebKitFormBoundaryXjWP6BP8Ciq6bPeo
Content-Disposition: form-data; name="file"; filename="custom_object_import.csv"
Content-Type: text/csv

color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
------WebKitFormBoundaryXjWP6BP8Ciq6bPeo--
```

```json
{
    "requestId": "c015#15a68a23418",
    "result": [
        {
            "batchId": 1013,
            "status": "Queued",
            "objectApiName": "car_c"
        }
    ],
    "success": true
}
```

이 예제에서는 `csv` 형식을 지정하고 가져오기 파일 `custom_object_import.csv`의 이름을 지정합니다.

호출이 비동기적이므로 응답에는 사용자 지정 개체 동기화 끝점에서 반환된 개별 성공 및 실패 대신 `batchId`이(가) 포함됩니다. `status`은(는) `Queued`, `Importing` 또는 `Failed`일 수 있습니다.

가져오기 상태를 확인하고 완료 후 오류 또는 경고를 검색하려면 `batchId`을(를) 유지합니다. `batchId`은(는) 7일 동안 유효합니다.

다음 명령줄 cURL 요청은 예제 작업을 제출합니다.

```bash
curl -X POST -i -F format='csv' -F file='@custom_object_import.csv' -F access_token='<Access Token>' <REST API Endpoint URL>/bulk/v1/customobjects/car_c/import.json
```

이 예제에서 `custom_object_import.csv` 파일에는 다음 데이터가 포함되어 있습니다.

```text
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

## 폴링 작업 상태

가져오기 작업을 만든 후 5~30초마다 폴링합니다. [사용자 지정 개체 가져오기 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET) 끝점에 대한 경로에 사용자 지정 개체 API 이름과 `batchId`을(를) 전달합니다.

```http
GET /bulk/v1/customobjects/{apiName}/import/{batchId}/status.json
```

```json
{
    "requestId": "2a5#15a68dd9be1",
    "result": [
        {
            "batchId": 1013,
            "operation": "import",
            "status": "Complete",
            "objectApiName": "car_c",
            "numOfObjectsProcessed": 3,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "importTime": "2 second(s)",
            "message": "Import succeeded, 3 records imported (3 members)"
        }
    ],
    "success": true
}
```

이 응답은 완료된 가져오기를 표시합니다. `status`은(는) `Complete`, `Queued`, `Importing` 또는 `Failed`일 수 있습니다.

작업이 완료되면 응답에는 처리, 실패 및 처리된 행 수가 경고와 함께 나열됩니다. `message` 특성은 추가 작업 정보를 제공할 수 있습니다.

## 실패

[사용자 지정 개체 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET) 응답의 `numOfRowsFailed` 특성은 실패한 행 수를 나타냅니다. 값이 0보다 크면 오류가 발생했음을 의미합니다.

[사용자 지정 개체 가져오기 실패](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectFailuresUsingGET) 끝점에 대한 경로에 사용자 지정 개체 API 이름과 `batchId`을(를) 전달합니다. 끝점이 실패 세부 정보가 포함된 파일을 반환합니다. 오류 파일이 없으면 HTTP 404 상태 코드를 반환합니다.

오류를 확인하려면 `vin`을(를) ` vin`(으)로 변경하고 쉼표와 `vin` 사이에 공백을 추가하여 헤더를 수정하십시오.

```text
color,make,model, vin
```

파일을 다시 가져온 후 상태 응답에 `numRowsFailed`: 3이 표시되어 세 가지 오류가 표시됩니다.

```http
GET /bulk/v1/customobjects/car_c/import/{batchId}/status.json
```

```json
{
    "requestId": "12260#15a68f491ed",
    "result": [
        {
            "batchId": 1016,
            "operation": "import",
            "status": "Complete",
            "objectApiName": "car_c",
            "numOfObjectsProcessed": 0,
            "numOfRowsFailed": 3,
            "numOfRowsWithWarning": 0,
            "importTime": "1 second(s)",
            "message": "Import completed with errors, 0 records imported (0 members), 3 failed"
        }
    ],
    "success": true
}
```

자세한 내용은 사용자 지정 개체 가져오기 실패 끝점을 호출하십시오.

```http
GET /bulk/v1/customobjects/car_c/import/{batchId}/failures.json
```

```text
color,make,model, vin,Import Failure Reason
red,bmw,2002,WBA4R7C55HK895912,missing.dedupe.fields
yellow,bmw,320i,WBA4R7C30HK896061,missing.dedupe.fields
blue,bmw,325i,WBS3U9C52HP970604,missing.dedupe.fields
```

응답이 중복 제거 필드 `vin`이(가) 누락되었음을 보여 줍니다.

## 경고

사용자 지정 개체 상태 가져오기 응답의 `numOfRowsWithWarning` 특성은 경고가 있는 행 수를 나타냅니다. 값이 0보다 크면 경고가 발생한 것입니다.

[사용자 지정 개체 가져오기 경고](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectWarningsUsingGET) 끝점에 대한 경로에 사용자 지정 개체 API 이름과 `batchId`을(를) 전달합니다. 끝점이 경고 세부 정보가 있는 파일을 반환합니다. 경고 파일이 없으면 HTTP 404 상태 코드를 반환합니다.

```http
GET /bulk/v1/customobjects/car_c/import/{batchId}/warnings.json
```
