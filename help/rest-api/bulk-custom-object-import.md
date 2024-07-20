---
title: 대량 사용자 지정 개체 가져오기
feature: Custom Objects
description: 사용자 지정 개체의 일괄 가져오기.
exl-id: e795476c-14bc-4e8c-b611-1f0941a65825
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# 대량 사용자 지정 개체 가져오기

[대량 사용자 지정 개체 가져오기 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects)

에 대한 사용자 지정 개체 레코드가 많을 때  가져오기, 가장 좋은 방법은 벌크 API를 사용하여 비동기적으로 가져오는 것입니다. 이 작업은 구분된 레코드(쉼표, 탭 또는 세미콜론)가 포함된 플랫 파일을 가져와서 수행합니다. 파일의 크기가 10MB 미만이면 파일에 원하는 수의 레코드를 포함할 수 있습니다(그렇지 않으면 HTTP)  413 상태 코드가 반환됨). 파일의 내용은 사용자 지정 개체 정의에 따라 다릅니다. 첫 번째 행에는 항상 각 행의 값을 로 매핑할 필드를 나열하는 헤더가 포함됩니다. 헤더의 모든 필드 이름은 API 이름과 일치해야 합니다(아래 설명). 나머지 행에는 가져올 데이터가 포함되며, 행당 하나의 레코드입니다. 레코드 작업은 &quot;삽입 또는 업데이트&quot;만 가능합니다.

## 처리 제한

한도 내에서 두 개 이상의 일괄 가져오기 요청을 제출할 수 있습니다. 각 요청은 처리할 FIFO 대기열에 작업으로 추가됩니다. 최대 두 개의 작업이 동시에 처리됩니다. 지정된 시간에 큐에 최대 10개의 작업이 허용됩니다(현재 처리 중인 2개 포함). 최대 10개의 작업 수를 초과하면 &quot;1016, 너무 많은 가져오기&quot; 오류가 반환됩니다.

## 사용자 지정 개체 예

벌크 API를 사용하기 전에 먼저 Marketo 관리 UI를 사용하여 [사용자 지정 개체를 만들기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)해야 합니다. 예를 들어 &quot;Color&quot;, &quot;Make&quot;, &quot;Model&quot; 및 &quot;VIN&quot; 필드가 있는 &quot;Car&quot; 사용자 지정 개체를 만들었다고 가정합니다. 다음은 사용자 지정 개체를 보여주는 관리자 UI 화면입니다. 중복 제거를 위해 VIN 필드를 사용했음을 알 수 있습니다. API 이름은 일괄 API 관련 끝점을 호출할 때 사용해야 하므로 강조 표시됩니다.

![사용자 지정 개체 삽입](assets/bulk-insert-co-car-1.png)

다음은 관리 UI에 표시되는 사용자 지정 개체 필드입니다.

![사용자 지정 개체 필드 삽입](assets/bulk-insert-co-car-fields.png)

### API 이름

사용자 지정 개체 API 이름을 [사용자 지정 개체 설명](#describe) 끝점에 전달하여 프로그래밍 방식으로 API 이름을 검색할 수 있습니다.

```
/rest/v1/customobjects/{apiName}/describe.json
```

```json
{
    "requestId": "46ff#15a686e66de",
    "result": [
        {
            "name": "car_c",
            "displayName": "Car",
            "description": "It's a car.",
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

이제 세 개의 &quot;Car&quot; 사용자 지정 개체 레코드를 가져오려고 한다고 가정합니다. 쉼표로 구분된 형식(CSV)을 사용하면 파일은 다음과 같이 표시될 수 있습니다.

```
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

1행은 헤더이고 2-4행은 사용자 지정 개체 데이터 레코드입니다.

## 작업 생성

대량 가져오기 요청을 수행하려면 [사용자 지정 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Identity/operation/identityUsingPOST) 끝점에 대한 경로에 사용자 지정 개체의 API 이름을 포함해야 합니다. 가져오기 파일의 이름을 참조하는 &quot;file&quot; 매개 변수와 가져오기 파일이 구분된 방법을 지정하는 &quot;format&quot; 매개 변수(&quot;csv&quot;, &quot;tsv&quot; 또는 &quot;ssv&quot;)도 포함해야 합니다.

```
POST /bulk/v1/customobjects/{apiName}/import.json?format=csv
```

```
Transfer-Encoding: chunked
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXjWP6BP8Ciq6bPeo
Content-Length: 290
Host: <munchkinId>.mktorest.com
```

```
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

이 예에서는 &quot;csv&quot; 형식을 지정하고 가져오기 파일의 이름을 &quot;custom_object_import.csv&quot;로 지정했습니다.

호출에 대한 응답으로 사용자 지정 개체 동기화 엔드포인트에서 가져오는 것과 같은 성공 또는 실패 목록은 여기에 없습니다. 대신 `batchId`을(를) 받습니다. 이 호출은 비동기적으로 수행되며 &quot;대기 중&quot;, &quot;가져오기&quot; 또는 &quot;실패&quot;의 `status`을(를) 반환할 수 있기 때문입니다. 가져오기 작업의 상태를 가져오거나 완료 시 실패 및/또는 경고를 검색할 수 있도록 batchId를 유지해야 합니다. batchId는 7일 동안 유효합니다.

대량 가져오기 요청을 복제하는 간단한 방법은 명령줄에서 curl을 사용하는 것입니다.

```
curl -X POST -i -F format='csv' -F file='@custom_object_import.csv' -F access_token='<Access Token>' <REST API Endpoint URL>/bulk/v1/customobjects/car_c/import.json
```

가져오기 파일 &quot;custom_object_import.csv&quot;에 다음이 포함되어 있는 경우:

```
color,make,model,vin
red,bmw,2002,WBA4R7C55HK895912
yellow,bmw,320i,WBA4R7C30HK896061
blue,bmw,325i,WBS3U9C52HP970604
```

## 폴링 작업 상태

가져오기 작업이 생성되면 해당 상태를 쿼리해야 합니다. 가져오기 작업을 5-30초마다 폴링하는 것이 가장 좋습니다. 이렇게 하려면 [사용자 지정 개체 가져오기 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET) 끝점에 대한 경로에 사용자 지정 개체의 API 이름과 `batchId`을(를) 전달합니다.

```
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

이 응답은 완료된 가져오기를 표시하지만 `status`은(는) 완료, 대기 중, 가져오기, 실패 중 하나일 수 있습니다. 작업이 완료된 경우 처리된 행 수, 실패 및 경고 목록이 표시됩니다. 또한 메시지 속성은 추가 작업 정보를 찾는 데 좋은 위치입니다.

## 실패

[사용자 지정 개체 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectStatusUsingGET) 응답에서 `numOfRowsFailed` 특성으로 오류가 표시됩니다. numOfRowsFailed가 0보다 크면 해당 값은 발생한 실패 횟수를 나타냅니다. [사용자 지정 개체 가져오기 실패](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectFailuresUsingGET) 끝점을 호출하여 실패 세부 정보가 포함된 파일을 가져옵니다. 다시 경로에 사용자 지정 개체 API 이름과 `batchId`을(를) 전달해야 합니다. 오류 파일이 없으면 HTTP 404 상태 코드가 반환됩니다.

예제를 계속 진행하여 헤더를 수정하고 &quot;vin&quot;을 &quot;vin&quot;으로 변경합니다(쉼표와 &quot;vin&quot; 사이에 공백을 추가).

```
color,make,model, vin
```

다시 가져오고 상태를 확인하면 `numRowsFailed`: 3에 대한 이 응답이 표시됩니다. 이는 세 가지 실패를 나타냅니다.

```
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

이제 Get Custom Object Failures 엔드포인트 호출을 수행하여 추가 실패 세부 정보를 가져옵니다.

```
GET /bulk/v1/customobjects/car_c/import/{batchId}/failures.json
```

```
color,make,model, vin,Import Failure Reason
red,bmw,2002,WBA4R7C55HK895912,missing.dedupe.fields
yellow,bmw,320i,WBA4R7C30HK896061,missing.dedupe.fields
blue,bmw,325i,WBS3U9C52HP970604,missing.dedupe.fields
```

중복 제거 필드 `vin`이(가) 누락되었습니다.

## 경고

사용자 지정 개체 상태 가져오기 응답에서 `numOfRowsWithWarning` 특성에 경고가 표시됩니다. numOfRowsWithWarning이 0보다 크면 해당 값은 발생한 경고 수를 나타냅니다. [사용자 지정 개체 가져오기 경고](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Custom-Objects/operation/getImportCustomObjectWarningsUsingGET) 끝점을 호출하여 경고 세부 정보가 있는 파일을 가져옵니다. 다시 경로에 사용자 지정 개체 API 이름과 `batchId`을(를) 전달해야 합니다. 경고 파일이 없으면 HTTP 404 상태 코드가 반환됩니다.

```
GET /bulk/v1/customobjects/car_c/import/{batchId}/warnings.json
```
