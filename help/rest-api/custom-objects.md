---
title: 사용자 지정 개체
feature: REST API, Custom Objects
description: 사용자 지정 Marketo 개체를 만들고 조작합니다.
source-git-commit: f1c9c5ba07013c2fdccb9f799b5c0077eb789a4b
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 0%

---


# 사용자 지정 개체

[**사용자 지정 개체 끝점 참조**](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects) Marketo을 통해 사용자는 Marketo 표준 개체(Leads, Company) 또는 기타 Marketo 사용자 지정 개체와 관련된 Marketo 사용자 지정 개체를 정의할 수 있습니다.  Marketo 사용자 지정 개체는 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)에 설명된 대로 Marketo UI를 사용하거나 아래 설명된 대로 사용자 지정 개체 메타데이터 API를 사용하여 만들 수 있습니다.

사용자 지정 개체 메타데이터 API에 액세스하려면 적절한 Marketo 구독 유형이 필요합니다.  자세한 내용은 CSM에 문의하십시오.

## 목록

리드 데이터베이스 개체에 사용할 수 있는 표준 설명, 쿼리, 업데이트 및 삭제 호출 외에 사용자 지정 개체에 사용할 수 있는 [목록 호출](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)이 있습니다.  이 끝점을 호출하면 개체에 대한 추가 메타데이터와 함께 대상 인스턴스에서 사용할 수 있는 사용자 지정 개체 목록이 포함된 응답이 반환됩니다.

```
GET /rest/v1/customobjects.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[  
      {  
         "name":"Car",
         "displayName":"Car",
         "description":"Car owner",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":["vin"],
         "searchableFields":[ 
            ["vin"],
            ["marketoGUID"],
            ["siebelId"]
         ],
         "relationships":[  
            {  
               "field":"siebelId",
               "type":"parent",
               "relatedTo":{  
                  "name":"Lead",
                  "field":"siebelId"
               }
            }
         ]
      }
   ]
}
```

응답은 각 개체에 있는 관계의 목록을 제공합니다.  관계에는 링크 값이 있는 개체의 필드를 나타내는 `field` 멤버, 관계가 부모 또는 자식 형식 개체에 있는지 나타내는 `type` 멤버 및 관련 개체의 이름을 나타내는 `relatedTo` 개체와 해당 개체의 링크 필드가 있습니다.

## 설명

사용자 지정 개체에 대한 [describe 호출](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1)은(는) Opportunities 및 Companies의 패턴과 동일한 패턴을 따릅니다. 여기에는 응답에 `relationships` 배열이 추가되고, 설명할 사용자 지정 개체 형식의 API 이름을 사용하는 URI에 `apiName` 경로 매개 변수가 추가됩니다.  목록 호출과 마찬가지로 이 사용자 지정 개체 유형에 사용할 수 있는 모든 관계가 나열됩니다.

```
GET /rest/v1/customobjects/{apiName}/describe.json
```

```json
{  
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[  
      {  
         "name":"Car",
         "displayName":"Car",
         "description":"Car owner",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":["vin"],
         "searchableFields":[  
            ["vin"],
            ["marketoGUID"],
            ["siebelId"]
         ],
         "relationships":[  
            {  
               "field":"siebelId",
               "type":"parent",
               "object":{  
                  "name":"Lead",
                  "field":"siebelId"
               }
            }
         ],
         "fields":[  
            {  
               "name":"marketoGUID",
               "displayName":"Marketo GUID",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {  
               "name":"createdAt",
               "displayName":"Created At",
               "dataType":"datetime",
               "updateable":false
            },
            {  
               "name":"updatedAt",
               "displayName":"Updated At",
               "dataType":"datetime",
               "updateable":false
            },
            {  
               "name":"vin",
               "displayName":"VIN",
               "description":"Vehicle Identification Number",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {  
               "name":"siebelId",
               "displayName":"External Id",
               "description":"External Id",
               "dataType":"string",
               "length":36,
               "updateable":true
            },
            {  
               "name":"make",
               "displayName":"Make",
               "dataType":"string",
               "length":36,
               "updateable":true
            },
            {  
               "name":"model",
               "displayName":"Model",
               "description":"Vehicle Model",
               "dataType":"string",
               "length":255,
               "updateable":true
            },
            {  
               "name":"year",
               "displayName":"Year",
               "dataType":"integer",
               "updateable":true
            },
            {  
               "name":"color",
               "displayName":"Color",
               "description":"Vehicle color",
               "dataType":"String",
               "length": 255,
               "updateable":true
            }
         ]
      }
   ]
}
```

## 쿼리

[사용자 지정 개체 쿼리](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)는 다른 리드 데이터베이스 API와 약간 다르며 설명 같은 `apiName` 경로 매개 변수를 사용합니다.  일반 filterType 매개 변수의 경우 쿼리는 다른 레코드 형식의 쿼리와 같은 간단한 GET으로, `filterType` 및 `filterValues`이(가) 필요합니다.  선택적으로 `**fields**`, `batchSize` 및 `nextPageToken` 매개 변수를 허용합니다.  필드 목록을 요청할 때 특정 필드가 요청되었지만 반환되지 않은 경우 값이 null로 간주됩니다.

```
GET /rest/v1/customobjects/{apiName}.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa,dff23271-f996-47d7-984f-f2676861b5fb
```

```
{  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa",
         "vin":"19UYA31581L000000",
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {  
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "vin":"29UYA31581L000000",
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
   ]
}
```

또는 복합 키로 쿼리할 때 API는 JSON 본문이 있는 POST을 수락하여 Opportunity Roles API처럼 작동합니다.  `filterValues`을(를) 제외하고 JSON 본문에 GET 쿼리와 동일한 멤버가 있을 수 있습니다.  필터 값 대신 각 개체 형식의 `dedupeFields`에 대해 이름이 지정된 멤버를 포함하는 개체를 가져오는 `input` 배열이 있습니다.

```
POST /rest/v1/customobjects/{apiName}.json?_method=GET
```

```json
{  
   "filterType":"dedupeFields",
   "fields":[  
      "marketoGuid",
      "Bedrooms",
      "yearBuilt"
   ],
   "input":[  
      {  
         "mlsNum":"1962352",
         "houseOwnerId":"42645756"
      },
      {  
         "mlsNum":"2962352",
         "houseOwnerId":"52645756"
      },
      {  
         "mlsNum":"3962352",
         "houseOwnerId":"62645756"
      }
   ]
}
```


```json
{  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa",
         "Bedrooms":3,
         "yearBuilt":1948,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {  
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "Bedrooms":4,
         "yearBuilt":1956,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      },
      {  
         "seq":2,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc",
         "Bedrooms":3,
         "yearBuilt":2001,
         "createdAt":"2015-02-23T18:21:53Z",
         "updatedAt":"2015-02-23T18:23:41Z"
      }
   ]
}
```

## 만들기 및 업데이트

[사용자 지정 개체 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) 끝점을 사용하여 사용자 지정 개체를 만들거나 업데이트하십시오. `action` 매개 변수를 사용하여 작업을 지정할 수 있습니다.  한 번의 호출로 최대 300개의 레코드를 만들거나 업데이트할 수 있습니다.  `input` 배열에 사용된 값은 대개 [사용자 지정 개체 설명](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/endpoint-reference#!/Custom_Objects/describeUsingGET_1) 끝점에서 반환된 정보를 기반으로 합니다. 예제 car 개체에는 중복 제거 필드 `vin`이(가) 하나만 있습니다.  dedupeFields 모드를 사용할 때 레코드를 업데이트하거나 만들려면 입력 배열의 각 레코드에 `vin`개 이상의 필드가 포함되어야 합니다.

```
POST /rest/v1/customobjects/{apiName}.json
```

```json
{
   "action":"updateOnly",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "vin":"19UYA31581L000000",
         "siebelId":"f2676861b5fb",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
      },
      {
         "vin":"29UYA31581L000000",
         "siebelId":"f2676861b5fc",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
      },
      {
         "vin":"39UYA31581L000000",
         "siebelId":"f2676861b5fd",
         "make":"BMW",
         "model":"3-Series 330i",
         "year":2003
      }
   ]
}
```


```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "status": "updated",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":1,
         "status": "created",
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":2,
         "status": "skipped"
         "reasons":[
            {
               "code":"1004",
               "message":"Lead not found"
            }
         ]
      }
   ]
}
```

`idField` 모드를 통해 업데이트를 수행할 때 `idField`은(는) 항상 `marketoGUID`이므로 각 레코드에는 항상 `marketoGUID` 필드가 필요합니다.  이 필드는 항상 시스템 관리이므로 `idField`은(는) updateOnly 작업 유형에만 사용할 수 있습니다.  응답에는 결과 배열에 있는 각 개별 레코드의 **상태**&#x200B;가 포함되며 개별 레코드에 대한 작업의 성공 여부에 따라 `marketoGUID` 또는 `reasons` 배열이 포함됩니다.

## 삭제

[레코드 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)은(는) 매우 간단합니다.  `deleteBy` 모드(`idField` 또는 `dedupeFields`)를 선택하고 `input` 배열의 각 레코드에 해당 필드를 포함하기만 하면 됩니다. 호출당 최대 300개의 레코드가 허용됩니다.

```
POST /rest/v1/customobjects/{apiName}/delete.json
```

```json
{  
   "deleteBy":"dedupeFields",
   "input":[  
      {  
         "vin":"19UYA31581L000000"
      },
      {  
         "vin":"29UYA31581L000000"
      },
      {  
         "vin":"39UYA31581L000000"
      }
   ]
}

{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status": "deleted"
      },
      {
         "seq":1,
         "marketoGUID":"da42707c-4dc4-4fc1-9fef-f30a3017240a",
         "status": "deleted"
      },
      {
         "seq":2,
         "status": "skipped"
         "reasons":[
            {
               "code":"1013",
               "message":"Object not found"
            }
         ]
      }
   ]
}
```

업데이트와 마찬가지로 결과에는 각 개별 레코드의 상태가 포함되며, 삭제 성공 여부에 따라 `marketoGUID` 또는 `reasons` 배열이 포함됩니다.

## 사용자 지정 개체 유형

사용자 지정 개체 메타데이터 API를 사용하면 사용자 지정 개체 스키마를 원격으로 관리할 수 있습니다.  API를 사용하면 새 사용자 지정 개체 유형을 만들거나 기존 사용자 지정 개체 유형을 수정할 수 있습니다.  사용자 지정 개체 유형을 만들거나 수정한 후에는 사용을 승인해야 합니다.  사용자 지정 개체에 대한 자세한 내용은 제품 설명서 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하세요.

* API로 생성된 사용자 지정 오브젝트 유형은 Marketo UI를 사용하여 수정할 수 없습니다
* 허용되는 최대 사용자 지정 개체 유형 수는 10개입니다.
* 허용되는 최대 사용자 정의 오브젝트 필드 수는 유형당 50개입니다.
* 사용자 정의 객체 유형 API 이름 및 표시 이름에는 영숫자와 밑줄 &quot;_&quot;가 포함될 수 있습니다.

### 쿼리 유형

사용자 지정 개체 유형 메타데이터를 검색하는 방법에는 다음 두 가지가 있습니다. 사용자 지정 개체 유형을 설명하고 를 반환합니다.  단일 사용자 지정 개체 유형에 대한 레코드로, 승인 상태별로 필터링할 수 있고 구독의 모든 사용자 지정 개체 유형 목록을 반환하며 이름 및 승인 상태별로 필터링할 수 있는 목록 사용자 지정 개체 유형별로 필터링할 수 있습니다.

### 설명 유형

[사용자 지정 개체 유형 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) 끝점이 단일 사용자 지정 개체 유형에 대한 메타데이터를 반환합니다. 필요한 `apiName` 경로 매개 변수는 설명된 사용자 지정 개체 형식의 API 이름입니다.  승인된 버전이 있으면 반환됩니다.  그렇지 않으면 초안 버전이 반환됩니다.  선택적 `state` 매개 변수는 `draft`, `approved` 또는 `approvedWithDraft`을(를) 반환할 버전을 지정하는 데 사용됩니다.

```
GET /rest/v1/customobjects/schema/{apiName}/describe.json?state=approved
```

```json
{
    "requestId": "d9bf#16876fa84b9",
    "result": [
        {
            "state": "approved",
            "version": "approved",
            "displayName": "Car",
            "description": "Automobile owned",
            "apiName": "car",
            "idField": "marketoGUID",
            "createdAt": "2019-01-22T19:12:18Z",
            "updatedAt": "2019-01-22T19:12:18Z",
            "dedupeFields": [
                "vin"
            ],
            "searchableFields": [
                [
                    "vin"
                ],
                [
                    "marketoGUID"
                ],
                [
                    "leadID"
                ]
            ],
            "relationships": [
                {
                    "field": "leadID",
                    "type": "child",
                    "relatedTo": {
                        "name": "Lead",
                        "field": "id"
                    }
                }
            ],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "leadID",
                    "displayName": "Lead ID",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "year",
                    "displayName": "Year",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

여기에서 다음 속성을 볼 수 있습니다.

* 메타데이터: state, displayName, description, apiName, idField, createdAt, updatedAt, dedupeFields, searchableFields, relationship
* 표준 필드: marketoGUID, createdAt, updatedAt
* 사용자 정의 필드 leadId, vin, make,  모델, 연도

### 목록 유형

[List Custom Object Types](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/listCustomObjectTypesUsingGET) 끝점이 대상 인스턴스에서 사용할 수 있는 모든 사용자 지정 개체 유형에 대한 메타데이터를 반환합니다.  이 끝점은 [사용자 지정 개체 나열](https://experienceleague.adobe.com/docs/marketo-developer/marketo/soap/custom-objects/custom-objects.html?lang=en)과(와) 유사하지만 보다 포괄적이고 상태, 관계 및 필드와 같은 추가 메타데이터를 포함합니다. 승인된 버전이 있으면 반환됩니다.  그렇지 않으면 초안 버전이 반환됩니다.  선택적 **state** 매개 변수는 반환할 사용자 지정 개체 형식의 버전을 지정하는 데 사용됩니다. **draft**, **approved** 또는 **approvedWithDraft**  선택적 **names** 매개 변수는 반환할 사용자 지정 개체 유형의 특정 이름을 지정하는 데 사용됩니다. 이 매개 변수는 쉼표로 구분된 API 이름 목록으로 구성됩니다.

```
GET /rest/v1/customobjects/schema.json?names=purchaseHistory
```

```json
{
    "requestId": "a181#167ebe94703",
    "result": [
        {
            "state": "approved",
            "displayName": "Purchases",
            "description": "Purchase data",
            "apiName": "purchaseHistory",
            "idField": "marketoGUID",
            "createdAt": "2014-09-12T16:13:37Z",
            "updatedAt": "2014-09-12T16:13:42Z",
            "dedupeFields": [
                "lead_id",
                "product_name"
            ],
            "searchableFields": [
                [
                    "lead_id",
                    "product_name"
                ],
                [
                    "marketoGUID"
                ],
                [
                    "lead_id"
                ]
            ],
            "relationships": [
                {
                    "field": "lead_id",
                    "type": "child",
                    "relatedTo": {
                        "name": "Lead",
                        "field": "lead_id"
                    }
                }
            ],
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "marketoGUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "amount",
                    "displayName": "Amount",
                    "dataType": "float",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "lead_id",
                    "displayName": "lead_id",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "product_name",
                    "displayName": "Product Name",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "purchase_date",
                    "displayName": "Transaction Date",
                    "dataType": "datetime",
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        },
        {
            "state": "approved",
            "version": "approved",
            "displayName": "Car",
            "description": "No really, it's a car!",
            "apiName": "car_c",
            "idField": "marketoGUID",
            "createdAt": "2017-02-22T19:55:51Z",
            "updatedAt": "2018-12-11T23:52:56Z",
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
            "relationships": [],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "year",
                    "displayName": "Year",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

### 유형 만들기 및 업데이트

#### 유형 만들기

[사용자 지정 개체 형식 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) 끝점을 사용하여 사용자 지정 개체 형식을 만들거나 업데이트합니다.  수행할 레코드 작업은 **createOnly**, **createOrUpdate** 또는 **updateOnly**&#x200B;일 수 있는 선택적 **action** 특성에 의해 제어됩니다.  기본 설정은 createOrUpdate입니다. **displayName** 및 **apiName** 특성이 필요합니다. 단, updateOnly를 작업으로 사용하는 경우는 예외입니다.   고객이 프로비저닝한 유형과의 충돌을 방지하기 위해 둘 다 고유해야 합니다.  LaunchPoint 파트너인 경우 이러한 이름에 대표 네임스페이스를 앞에 추가해야 합니다.  apiName의 경우, 이 규칙은 다른 텍스트 문자열을 구분하는 데 도움이 되도록 소문자나 카멜 대/소문자를 사용하는 것입니다. 선택적 **pluralName** 특성은 displayName의 plural 형식을 지정합니다.  선택적 **description** 특성은 사용자 지정 개체 형식을 설명하는 데 사용됩니다.  선택적 **showInLeadDetail** 부울 특성을 사용하여 Marketo UI의 [리드 데이터베이스] 페이지에서 사용자 지정 개체 데이터를 볼 수 있습니다.  기본 설정은 false입니다.

사용자 지정 개체의 이름을 지정할 때 주의하십시오. 새 사용자 지정 개체를 만들 때 회사 이름(영숫자 또는 밑줄 허용)을 나타내는 문자열로 이름 앞에 를 붙이는 것이 좋습니다. 이렇게 하면 사용자 지정 오브젝트를 MLM UI에서 쉽게 검색할 수 있으며 이름이 고유한지 확인하는 데도 도움이 됩니다.

다음은 API를 사용하여 새 사용자 지정 개체 유형을 만드는 예제입니다  이름 &quot;transaction&quot;.

```
POST /rest/v1/customobjects/schema.json
```

```json
{
  "action":"createOnly",
  "displayName": "Transaction",
  "apiName": "transaction",
  "description": "Commerce happens"
}
```

```json
{
    "requestId": "fb9d#167f2879557",
    "result": [],
    "success": true
}
```

다음은 새로 만든 유형을 설명하는 후속 호출입니다.

```
GET /rest/v1/customobjects/schema/transaction/describe.json
```

```json
{
    "requestId": "cf9b#167f28db0a9",
    "result": [
        {
            "state": "draft",
            "displayName": "Transaction",
            "description": "Commerce happens",
            "apiName": "transaction",
            "idField": null,
            "createdAt": null,
            "updatedAt": null,
            "dedupeFields": [],
            "searchableFields": [
                []
            ],
            "relationships": [],
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

여기에서 다음 사용자 지정 개체 관련 데이터를 볼 수 있습니다.

* 메타데이터: state, displayName, description, apiName, idField, createdAt, updatedAt, dedupeFields, searchableFields, relationship
* 표준 필드: marketoGUID, createdAt, updatedAt

#### 업데이트 유형

다음은 API 이름이 &quot;transaction&quot;인 기존 유형의 설명을 업데이트하는 예제입니다.  **apiName** 특성이 필요합니다.  여기에서는 형식이 이미 있으며 선택적 **action** 특성에 updateOnly를 사용한다고 가정합니다.  **apiName** 외에 만들 수 있는 특성을 업데이트할 수 있습니다.

```
POST /rest/v1/customobjects/schema.json
```

```json
{
  "action":"updateOnly",
  "apiName": "transaction",
  "description":"No really, commerce happens!"
}
```

```json
{
    "requestId": "103c3#167f2223fd7",
    "result": [],
    "success": true
}
```

## 유형 승인

사용자 지정 개체 유형을 사용하려면 먼저 승인해야 합니다. [사용자 지정 개체 형식 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectTypeUsingPOST) 끝점을 사용하여 새 사용자 지정 개체 형식을 만들면 초안 버전으로 만들어집니다. 사용자 정의 필드를 추가한 후에는 초안 버전을 승인해야 합니다. 이렇게 하면 승인된 버전이 만들어지고 초안 버전이 삭제됩니다. 사용자 지정 개체 유형 동기화 엔드포인트를 사용하거나 사용자 지정 개체 유형 필드 엔드포인트 추가/업데이트/삭제 중 하나를 사용하여 기존 사용자 지정 개체 유형을 수정하면 초안 버전이 만들어집니다. 유형 또는 해당 필드에 대한 모든 수정 사항은 초안 버전에만 영향을 줍니다. 수정을 마치면 초안 버전을 승인해야 합니다. 이렇게 하면 승인된 버전이 초안 버전으로 바뀌고 초안 버전이 삭제됩니다. 사용자 지정 개체 승인에 대한 자세한 내용은 제품 설명서 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)를 참조하세요.

사용자 정의 객체 유형이 승인되면 다음을 수행할 수 없습니다.

* `displayName` 또는 `apiName` 업데이트
* 링크 필드 추가 또는 제거
* 중복 제거 필드 추가 또는 제거

이러한 이유로 사용할 스키마와 명명 규칙을 신중히 고려하는 것이 중요합니다.

### 승인 유형

[사용자 지정 개체 유형 승인](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/approveCustomObjectTypeUsingPOST) 끝점을 사용하여 초안 버전을 새로운 승인 버전으로 게시하십시오.  **apiName**&#x200B;은(는) 경로 매개 변수로서 유일한 필수 매개 변수입니다.  형식이 초안 상태가 아니면 승인할 수 없으며 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)에서 설명한 유효성 검사 규칙 집합을 충족합니다.

```
POST /rest/v1/customobjects/schema/{apiName}/approve.json
```

```json
{
    "requestId": "11d86#1685304a983",
    "result": [],
    "success": true
}
```

### 버리기 유형

[사용자 지정 개체 유형 무시](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/discardCustomObjectTypeUsingPOST) 끝점을 사용하여 초안 버전을 삭제합니다. `apiName`은(는) 경로 매개 변수로서 유일한 필수 매개 변수입니다. 유형은 삭제할 초안 상태여야 합니다. 즉, 승인된 유형은 삭제할 수 없습니다.

```
POST /rest/v1/customobjects/schema/{apiName}/discardDraft.json
```

```json
{
    "requestId": "5228#1684edde793",
    "result": [],
    "success": true
}
```

### 유형 삭제

[사용자 지정 개체 유형 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST) 끝점을 사용하여 승인된 버전을 삭제합니다.  `apiName`은(는) 경로 매개 변수로서 유일한 필수 매개 변수입니다.  이는 파괴적인 작업이므로 실행을 취소할 수 없습니다.  트리거 또는 필터와 같은 에셋에서 유형을 사용하지 않도록 제거하지 않으면 유형을 삭제할 수 없습니다.  사용자 지정 개체 종속 Assets 끝점 가져오기를 사용하여 지정된 유형에 대한 종속 에셋 목록을 검색할 수 있습니다.

POST /rest/v1/customobjects/schema/{apiName}/delete.json

```json
{
    "requestId": "14e36#1684efc4227",
    "result": [],
    "success": true
}
```

## 사용자 정의 오브젝트 필드

기본적으로 모든 사용자 지정 객체 유형에는 다음 표준 필드가 포함되어 있습니다.

* Marketo GUID - 사용자 지정 개체 유형에 대한 고유 식별자
* 생성 시간 - 사용자 지정 개체 유형을 만든 날짜/시간
* 업데이트된 시간 - 사용자 지정 개체 유형을 마지막으로 업데이트한 날짜/시간

아래에 설명된 끝점을 사용하여 사용자 정의 필드를 자유롭게 추가/변경/삭제할 수 있습니다.

* 허용되는 최대 필드 수는 50개입니다.
* 사용자 지정 개체가 승인되면 사용자 지정 개체에 최대 20개의 추가 필드를 추가할 수 있습니다
* 최소 1개의 데이터 중복 제거 필드가 필요합니다. 최대 3개까지 허용됩니다.
* 필드 API 이름 및 표시 이름에는 영숫자와 밑줄(_)이 포함될 수 있습니다.

사용자 지정 개체 필드에 대한 자세한 내용은 제품 설명서 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하세요.

### 필드 추가

[사용자 지정 개체 유형 필드 추가](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/addCustomObjectTypeFieldsUsingPOST) 끝점을 사용하면 사용자 지정 개체에 하나 이상의 필드를 추가할 수 있습니다.  요청 본문에 하나 이상의 요소가 있는 `input` 배열이 있습니다.  각 요소는 필드를 설명하는 속성이 있는 JSON 개체입니다. 필수 `name` 특성은 필드의 API 이름이며 사용자 지정 개체에 고유해야 합니다.   이 규칙은 다른 텍스트 문자열을 구분하는 데 도움이 되도록 소문자 또는 카멜 대/소문자를 사용하는 것입니다. 필수 `displayName` 특성은 사람이 인식할 수 있는 필드의 이름이며 사용자 지정 개체에 고유해야 합니다. 필수 `dataType` 특성은 필드의 데이터 형식입니다.  A  허용되는 데이터 형식 목록은 [사용자 지정 개체 형식 필드 데이터 형식 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) 끝점을 호출하여 가져올 수 있습니다.  사용자 지정 개체에는 데이터 형식이 &quot;link&quot;인 필드가 포함될 수 있습니다.  링크 필드는 사용자 지정 오브젝트와 시스템의 다른 오브젝트 유형(예: Lead, Company) 간의 관계를 설정하는 데 사용됩니다.  링크 필드에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하십시오. 선택적 `description` 특성은 필드에 대한 설명입니다. 선택적 `isDedupeField` 부울 특성은 사용자 지정 개체 업데이트 작업 중에 필드가 중복 제거에 사용되는지 여부를 지정합니다.  기본 설정은 false입니다.  일대다 관계의 경우 중복 제거 필드가 필요합니다. 선택적 `relatedTo` 개체 특성은 링크 필드를 지정합니다.  일대다 관계의 경우 이 개체에는 연결할 &quot;링크 개체&quot; 또는 부모 개체인 `name` 특성과 &quot;링크 필드&quot;인 `field` 특성이 포함됩니다.  또는 키 속성으로 사용할 부모 개체 내의 필드입니다.  허용되는 링크 개체 목록을 검색하려면 [사용자 지정 개체 연결 가능 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) 끝점을 호출하십시오.  링크 필드에 대한 자세한 내용은 제품 설명서 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하세요. 사용자 지정 개체는 기존 링크 필드가 있는 다른 사용자 지정 개체에 연결할 수 없습니다.

### 일대다 관계

일대다 사용자 지정 개체 구조의 경우 사용자 지정 개체의 링크 필드를 사용하여 표준 개체(리드 또는 회사)에 연결합니다. Marketo 제품 설명서 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)의 자동차 소유자 예제를 사용하여 리드에 연결할 자동차 관련 정보가 포함된 사용자 지정 개체를 만듭니다.

1. **Car** 개체 만들기
1. **Car** 개체에 필드 추가: **VIN**&#x200B;에서 중복 제거, **잠재 고객**&#x200B;**/잠재 고객 ID에 연결**
1. **자동차** 개체 승인

먼저, 차량별 정보를 포함할 사용자 지정 개체 유형을 만듭니다.

```
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action":"createOnly",
    "displayName": "Car",
    "pluralName": "Cars"
    "apiName": "car",
    "description": "Automobile owned",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "cbaa#16876dd3da6",
    "result": [],
    "success": true
}
```

이제 Car 사용자 정의 오브젝트 유형에 필드를 추가합니다. 링크 필드를 사용하여 연결할 객체와 필드를 모두 지정합니다. 이 경우 링크 개체는 리드이고 링크 필드는 ID입니다. 중복 제거(VIN)에 문자열 필드를 사용합니다.  추가 자동차 속성(Make, Model, Year)을 저장하기 위해 세 개의 필드를 더 추가합니다.

```
POST /rest/v1/customobjects/schema/car/addField.json
```

```json
{
  "input": [
    {
      "displayName": "Lead ID",
      "description": "Link field to Lead object",
      "name": "leadID",
      "dataType": "link",
      "relatedTo": {
        "field": "id",
        "name": "lead"
      }
    },
    {
      "displayName": "VIN",
      "description": "Vehicle ID number",
      "name": "vin",
      "dataType": "string",
      "isDedupeField": true
    },
    {
      "displayName": "Make",
      "description": "Vehicle make",
      "name": "make",
      "dataType": "string"
    },
    {
      "displayName": "Model",
      "description": "Vehicle model",
      "name": "model",
      "dataType": "string"
    },
    {
      "displayName": "Year",
      "description": "Vehicle year",
      "name": "year",
      "dataType": "integer"
    }
  ]
}

{
    "requestId": "b359#16876f17996",
    "result": [],
    "success": true
}
```

마지막으로 사용자 지정 개체 유형을 승인합니다.

```
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

### 다대다 관계

다대다 관계는 Lead 또는 Company와 같은 표준 사용자 지정 개체와 &quot;edge&quot; 사용자 지정 개체 사이에 있는 &quot;bridge&quot; 또는 intermediate 사용자 지정 개체를 사용하여 표시됩니다. Edge 객체는 설명 속성(필드)이 포함된 기본 엔티티입니다. 브리지 객체에는 2개의 링크 필드를 사용하여 객체 관계를 해결하는 데이터가 포함됩니다.  링크 필드 하나는 에서와 마찬가지로 상위 표준 개체를 다시 가리킵니다.  일대다 관계 구성.  다른 링크 필드는 링크가 없는 사용자 지정 객체인 Edge 객체를 가리킵니다.  브리지 객체에는 설명 속성(필드)도 포함될 수 있습니다. Marketo 제품 설명서 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)의 대학 과정 등록 예제를 사용하여 과정 관련 정보를 포함하는 Edge 사용자 지정 개체와 과정을 리드와 연결하는 데 사용되는 등록 브리지 개체를 만듭니다. 단계는 다음과 같습니다.

1. **Course** Edge 개체 만들기
1. **과정 ID**&#x200B;에서 **과정:** 중복 제거에 필드 추가
1. **과정** 승인
1. **등록** 브리지 개체 만들기
1. **등록:** **등록 ID**&#x200B;에 대한 중복 제거, **과정**&#x200B;**/과정 ID** 필드 및 **잠재 고객**&#x200B;**/잠재 고객 ID에 대한 링크 추가**
1. **등록** 승인

먼저 과정별 정보를 포함할 Edge 객체 유형을 생성합니다.

```
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action":"createOnly",
    "displayName": "Course",
    "pluralName": "Courses",
    "apiName": "course",
    "description": "Modeling a college course, an edge object in Marketo",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "4aec#168879ede00",
    "result": [],
    "success": true
}
```

다음으로 Edge 객체 유형에 사용자 정의 필드를 추가하겠습니다.  이 예제에서는 4개의 사용자 정의 필드를 추가하여 대학 과정을 모델링합니다. 강의 ID, 강의 강사, 강의 위치, 강의 이름.  하나 이상의 데이터 중복 제거 필드가 필요하므로 과정 ID 를 데이터 중복 제거 필드로 지정합니다.

```
POST /rest/v1/customobjects/schema/course/addField.json
```

```json
{
    "input": [
        {
            "displayName": "Course ID",
            "name": "courseID",
            "dataType": "string",
            "isDedupeField": true
        },
        {
            "displayName": "Course Instructor",
            "name": "courseInstructor",
            "dataType": "string"
        },
        {
            "displayName": "Course Location",
            "name": "courseLocation",
            "dataType": "string"
        },
        {
            "displayName": "Course Name",
            "name": "courseName",
            "dataType": "string"
        }
    ]
}
```

```
{
    "requestId": "cc36#16895b82a41",
    "result": [],
    "success": true
}
```

이제 브리지 오브젝트 유형에 연결할 때 나중에 참조할 수 있도록 에지 오브젝트 유형을 승인해야 합니다.  사용자 지정 개체 유형은 링크 개체로 선택할 수 있도록 승인되어야 합니다.

```
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

Edge 개체가 완료되었습니다.  이제 계속해서 등록별 정보를 포함할 Bridge 개체 유형을 만들어 보겠습니다.

```
POST /rest/v1/customobjects/schema.json
```

```json
{
    "action": "createOnly",
    "displayName": "Enrollment",
    "pluralName": "Enrollments",
    "apiName": "enrollment",
    "description": "Bridge object for Course custom object",
    "showInLeadDetail": true
}
```

```json
{
    "requestId": "8fbb#168960f671b",
    "result": [],
    "success": true
}
```

Bridge 개체 유형에 사용자 정의 필드를 추가하려면 두 개의 링크 필드를 추가합니다. 하나는 Lead 개체에 연결되는 링크이고 다른 하나는 방금 만든 Course 개체에 연결되는 링크입니다. Lead 객체에 연결하려면 Lead Id 필드를 사용합니다. 과정 오브젝트에 연결하려면 과정 ID 필드를 사용하십시오.  그런 다음 하나 이상의 중복 제거 필드가 필요하므로 등록 ID 고유 식별자를 중복 제거 필드로 추가합니다. 마지막으로, 성적 필드를 추가하여 학생이 어떻게 했는지 추적합니다.

```
POST /rest/v1/customobjects/schema/enrollment/addField.json
```

```json
{
    "input": [
        {
            "displayName": "Lead ID",
            "description": "Link field to Lead object",
            "name": "leadID",
            "dataType": "link",
            "relatedTo": {
                "field": "id",
                "name": "lead"
            }
        },
        {
            "displayName": "Course ID",
            "description": "Link field to Course object",
            "name": "courseID",
            "dataType": "link",
            "relatedTo": {
                "field": "courseID",
                "name": "course"
            }
        },
        {
            "displayName": "Enrollment ID",
            "description": "Unique ID for deduplication",
            "name": "enrollmentID",
            "dataType": "string",
            "isDedupeField": true
        },
        {
            "displayName": "Grade",
            "description": "Grade for the course",
            "name": "grade",
            "dataType": "string"
        }
    ]
}
```

```json
{
    "requestId": "7be5#168973f5052",
    "result": [],
    "success": true
}
```

마지막으로 브리지 개체를 승인합니다.

```
POST /rest/v1/customobjects/schema/enrollment/approve.json
```

```json
{
    "requestId": "9a76#16897b0e84b",
    "result": [],
    "success": true
}
```

[사용자 지정 개체 동기화](#create_and_update) 또는 [사용자 지정 개체 일괄 가져오기](https://experienceleague.adobe.com/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import.html?lang=en)를 사용하여 프로그래밍 방식으로 사용자 지정 개체 레코드를 채울 수 있습니다. 또는 Marketo UI 기능 [사용자 지정 개체 데이터 가져오기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/import-custom-object-data)를 사용할 수 있습니다.

## 필드 업데이트

[사용자 지정 개체 유형 필드 업데이트](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/updateCustomObjectTypeFieldUsingPOST) 끝점을 사용하면 초안 사용자 지정 개체의 필드를 업데이트할 수 있습니다.  필수 경로 매개 변수 `apiName`은(는) 사용자 지정 개체 형식의 API 이름입니다.  필수 경로 매개 변수 `fieldAPIName`은(는) 사용자 지정 개체 유형 필드의 API 이름입니다.  요청 본문에는 업데이트할 필드 속성을 지정하는 키/값 쌍이 포함된 JSON 오브젝트가 포함됩니다.

```
POST /rest/v1/customobjects/schema/{apiName}/{fieldApiName}/updateField.json
```

```json
{
  "displayName": "Very Long Title",
  "dataType": "text"
}
```

```json
{
    "requestId": "d523#1684f355db9",
    "result": [],
    "success": true
}
```

## 필드 삭제

[사용자 지정 개체 유형 필드 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectTypeFieldsUsingPOST) 끝점을 사용하면 사용자 지정 개체에서 하나 이상의 필드를 삭제할 수 있습니다.  필수 경로 매개 변수 `apiName`은(는) 사용자 지정 개체 형식의 API 이름입니다.  요청 본문에 하나 이상의 요소가 있는 `input` 배열이 있는 JSON 개체가 있습니다.  각 요소는 삭제할 필드의 API 이름을 지정하는 `name` 특성이 있는 JSON 개체입니다.

```
POST /rest/v1/customobjects/schema/{apiName}/deleteField.json
```

```json
{
    "input":
    [
        {
            "name": "title"
        },
        {
            "name": "author"
        }
    ]
}
```

```json
{
"requestId": "b359#19934f17996",
"result": [],
"success": true
}
```

## 목록 필드 데이터 유형

[사용자 지정 개체 형식 필드 데이터 형식 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) 끝점은 허용되는 모든 필드 데이터 형식 목록을 반환합니다. 이 기능은 지원되는 사용자 지정 필드 데이터 유형을 식별하기 위해 사용자 지정 개체 유형을 모델링할 때 유용합니다.

```
GET /rest/v1/customobjects/schema/fieldDataTypes.json
```

```json
{
    "requestId": "c405#167ed49e866",
    "result": [
        "string",
        "boolean",
        "integer",
        "float",
        "link",
        "email",
        "currency",
        "date",
        "datetime",
        "phone",
        "text"
    ],
    "success": true
}
```

## 연결 가능한 사용자 지정 개체 나열

[사용자 지정 개체 연결 가능한 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) 끝점은 허용되는 모든 링크 개체 목록과 해당 링크 필드를 반환합니다.  이 목록에는 표준 개체(리드, 회사)와 인스턴스에서 만든 모든 사용자 지정 개체가 포함됩니다.

```
GET /rest/v1/customobjects/schema/linkableObjects.json
```

```json
{
    "requestId": "11e62#167f1160e4e",
    "result": [
        {
            "name": "lead",
            "displayName": "Lead",
            "fields": [
                {
                    "name": "Account Balance",
                    "displayName": "Account Balance",
                    "dataType": "integer"
                },
                {
                    "name": "Email Address",
                    "displayName": "Email Address",
                    "dataType": "email"
                },
                {
                    "name": "Id",
                    "displayName": "Id",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Display Name",
                    "displayName": "Marketo Social Facebook Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Id",
                    "displayName": "Marketo Social Facebook Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Photo URL",
                    "displayName": "Marketo Social Facebook Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Profile URL",
                    "displayName": "Marketo Social Facebook Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Facebook Reach",
                    "displayName": "Marketo Social Facebook Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Referred Enrollments",
                    "displayName": "Marketo Social Facebook Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Facebook Referred Visits",
                    "displayName": "Marketo Social Facebook Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Gender",
                    "displayName": "Marketo Social Gender",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Display Name",
                    "displayName": "Marketo Social LinkedIn Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Id",
                    "displayName": "Marketo Social LinkedIn Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Photo URL",
                    "displayName": "Marketo Social LinkedIn Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Profile URL",
                    "displayName": "Marketo Social LinkedIn Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social LinkedIn Reach",
                    "displayName": "Marketo Social LinkedIn Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social LinkedIn Referred Enrollments",
                    "displayName": "Marketo Social LinkedIn Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social LinkedIn Referred Visits",
                    "displayName": "Marketo Social LinkedIn Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Syndication Id",
                    "displayName": "Marketo Social Syndication Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Total Referred Enrollments",
                    "displayName": "Marketo Social Total Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Total Referred Visits",
                    "displayName": "Marketo Social Total Referred Visits",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Display Name",
                    "displayName": "Marketo Social Twitter Display Name",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Id",
                    "displayName": "Marketo Social Twitter Id",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Photo URL",
                    "displayName": "Marketo Social Twitter Photo URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Profile URL",
                    "displayName": "Marketo Social Twitter Profile URL",
                    "dataType": "string"
                },
                {
                    "name": "Marketo Social Twitter Reach",
                    "displayName": "Marketo Social Twitter Reach",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Referred Enrollments",
                    "displayName": "Marketo Social Twitter Referred Enrollments",
                    "dataType": "integer"
                },
                {
                    "name": "Marketo Social Twitter Referred Visits",
                    "displayName": "Marketo Social Twitter Referred Visits",
                    "dataType": "integer"
                }
            ]
        },
        {
            "name": "company",
            "displayName": "Company",
            "fields": [
                {
                    "name": "Id",
                    "displayName": "Id",
                    "dataType": "integer"
                }
            ]
        },
        {
            "name": "car_c",
            "displayName": "Car",
            "fields": [
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string"
                },
                {
                    "name": "vin",
                    "displayName": "VIN",
                    "dataType": "string"
                }
            ]
        }
    ],
    "success": true
}
```

## 사용자 지정 개체 종속 Assets 가져오기

[사용자 지정 개체 종속 Assets 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectTypeDependentAssetsUsingGET) 끝점은 인스턴스 내 위치를 포함하여 사용자 지정 개체 유형의 종속 자산 목록을 반환합니다.  이 기능은 통합을 제거할 때 유용하며 사용자 지정 오브젝트 유형이 사용 중인 모든 곳을 식별해야 합니다.

```
GET /rest/v1/customobjects/schema/{apiName}/dependentAssets.json
```


```json
{
    "requestId": "71cf#16a21f30ed6",
    "result": [
        {
            "assetType": "Smart Campaign",
            "assetId": 3773,
            "assetName": "CarTest.HasCar (Smart List)"
        },
        {
            "assetType": "Smart Campaign",
            "assetId": 3773,
            "assetName": "CarTest.HasCar (Smart List)",
            "usedFields": [
                "leadID",
                "make",
                "model",
                "vin",
                "year"
            ]
        }
    ],
    "success": true
}
```

## 시간 초과

* 사용자 지정 개체 엔드포인트는 아래에 명시되지 않는 한 30초의 시간 제한을 갖습니다
   * 사용자 지정 개체 동기화: 120s 
   * 사용자 지정 개체 삭제: 60초
