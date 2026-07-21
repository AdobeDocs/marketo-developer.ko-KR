---
title: 사용자 정의 오브젝트
feature: REST API, Custom Objects
description: 엔드포인트, 메타데이터, 관계, 필드 및 쿼리를 나열하고 설명하는 등 REST API를 통해 Marketo 사용자 지정 개체를 만들고 관리하는 방법에 대해 알아봅니다.
exl-id: 88e8829b-f8f1-46d7-a753-5aa6e20e2c40
TQID: https://experienceleague.adobe.com/NWm9CjFVqQdVDJRrnE4nA299-Lg53-JR7xvY-82dUqY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
subfeature_v2:
  - id: ea4e3ff5-e7b9-4b4c-a5a0-dc27cc3f4275
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 2938
ht-degree: 0%

---

# 사용자 정의 오브젝트

[**사용자 지정 개체 끝점 참조**](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects)

Marketo 사용자 지정 오브젝트는 리드 및 회사와 같은 Marketo Standard 오브젝트 또는 기타 Marketo 사용자 지정 오브젝트와 관련될 수 있습니다. [Marketo UI](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)에서 또는 이 문서에 설명된 사용자 지정 개체 메타데이터 API를 사용하여 Marketo 사용자 지정 개체를 만드십시오.

사용자 지정 개체 메타데이터 API에 액세스하려면 적절한 Marketo 구독 유형이 필요합니다. 자세한 내용은 CSM에 문의하십시오.

## List

리드 데이터베이스 개체에 대한 표준 설명, 쿼리, 업데이트 및 삭제 호출 외에도 사용자 지정 개체는 [목록 호출](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectsUsingGET)을 제공합니다. 끝점은 대상 인스턴스에서 사용할 수 있는 사용자 지정 개체와 각 개체에 대한 메타데이터를 반환합니다.

```http
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

응답에는 각 객체의 관계가 나열됩니다. 각 관계에는 다음이 포함됩니다.

- `field`: 링크 값이 있는 개체의 필드입니다.
- `type`: 관련 개체가 부모 개체인지 자식 개체인지 여부.
- `relatedTo`: 관련 개체의 이름과 해당 링크 필드.

## 설명

사용자 지정 개체에 대한 [Describe 호출](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1)은(는) 두 개의 추가 기능이 있는 Opportunities 및 Companies와 동일한 패턴을 따릅니다.

- `apiName` 경로 매개 변수는 설명할 사용자 지정 개체 형식의 API 이름을 지정합니다.
- 응답에는 사용자 지정 개체 형식에 사용할 수 있는 관계를 나열하는 `relationships` 배열이 포함되어 있습니다.

```http
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

[사용자 지정 개체 쿼리](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectsUsingGET)는 다른 리드 데이터베이스 개체 쿼리와 약간 다릅니다. Describe와 마찬가지로 요청도 `apiName` 경로 매개 변수를 사용합니다.

일반 filterType의 경우 필수 `filterType` 및 `filterValues` 매개 변수와 함께 GET 요청을 보냅니다. 선택적 `**fields**`, `batchSize` 및 `nextPageToken` 매개 변수도 포함할 수 있습니다.

필드 목록을 요청할 때 반환되지 않은 요청된 필드는 null의 묵시적 값을 갖습니다.

```http
GET /rest/v1/customobjects/{apiName}.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa,dff23271-f996-47d7-984f-f2676861b5fb
```

```json
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

복합 키로 쿼리할 때 API는 Opportunity Roles API처럼 작동하며 JSON 본문이 있는 POST 요청을 수락합니다. 본문에는 `filterValues`을(를) 제외하고 GET 쿼리와 동일한 멤버가 포함될 수 있습니다.

필터 값 대신 `input` 개체 배열을 제공하십시오. 각 개체에는 개체 형식의 `dedupeFields`에 있는 모든 필드에 대한 멤버가 포함되어 있습니다.

```http
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

[사용자 지정 개체 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) 끝점을 사용하여 사용자 지정 개체를 만들거나 업데이트합니다. `action` 매개 변수로 작업을 지정하십시오. 각 호출은 최대 300개의 레코드를 만들거나 업데이트할 수 있습니다.

[사용자 지정 개체 설명](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/endpoint-reference#!/Custom_Objects/describeUsingGET_1) 끝점에서 반환된 정보를 기반으로 `input` 배열의 값을 사용합니다. 예제 car 개체에서 중복 제거 필드는 `vin`뿐입니다. dedupeFields 모드를 사용하여 레코드를 만들거나 업데이트하는 경우 입력 배열의 각 개체에 `vin` 이상의 필드를 포함하십시오.

```http
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

`idField` 모드에서 레코드를 업데이트할 때 `idField`은(는) 항상 `marketoGUID`입니다. 모든 레코드에 `marketoGUID` 필드를 포함합니다.

이 필드는 시스템 관리이므로 `idField`은(는) updateOnly 작업 형식에 대해서만 유효합니다. 결과 배열에는 각 레코드의 **상태**&#x200B;가 포함됩니다. 또한 성공적인 작업을 위한 `marketoGUID` 또는 실패한 작업을 위한 `reasons` 배열이 포함됩니다.

## 삭제

[레코드를 삭제](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)하려면 `idField` 또는 `dedupeFields`의 `deleteBy` 모드를 선택하십시오. `input` 배열의 각 레코드에 해당 필드를 포함하십시오. 각 호출에는 최대 300개의 기록이 허용됩니다.

```http
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

업데이트와 마찬가지로 결과에는 각 레코드에 대한 상태가 포함됩니다. 또한 삭제에 성공한 `marketoGUID` 또는 삭제에 실패한 `reasons` 배열이 포함됩니다.

## 사용자 지정 개체 유형

사용자 지정 개체 메타데이터 API를 사용하면 사용자 지정 개체 스키마를 원격으로 관리할 수 있습니다. 사용자 정의 객체 유형을 생성하거나 기존 유형을 수정하는 데 사용합니다. 유형을 만들거나 수정한 후 사용하기 전에 승인합니다.

자세한 내용은 [사용자 지정 개체 제품 설명서](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하세요.

- Marketo UI에서 API로 생성된 사용자 지정 개체 유형은 수정할 수 없습니다.
- 사용자 지정 개체 유형의 최대 수는 10개입니다.
- 사용자 지정 개체 필드의 최대 수는 유형당 50개입니다.
- 사용자 정의 객체 유형 API 이름 및 표시 이름에는 영숫자와 밑줄 문자 &quot;_&quot;가 포함될 수 있습니다.

### 쿼리 유형

다음 방법 중 하나로 사용자 지정 개체 유형 메타데이터를 검색합니다.

- 사용자 지정 개체 유형 설명 은 하나의 사용자 지정 개체 유형 레코드를 반환하며 승인 상태별 필터링을 지원합니다.
- List Custom Object Types는 구독에서 모든 사용자 지정 개체 유형을 반환하고 이름 및 승인 상태별 필터링을 지원합니다.

### 설명 유형

[사용자 지정 개체 유형 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/describeUsingGET_1) 끝점이 하나의 사용자 지정 개체 유형에 대한 메타데이터를 반환합니다. 필수 `apiName` 경로 매개 변수는 설명할 유형의 API 이름을 지정합니다.

승인된 버전이 있으면 끝점이 이를 반환합니다. 그렇지 않으면 초안 버전이 반환됩니다. 선택적 `state` 매개 변수를 사용하여 `draft`, `approved` 또는 `approvedWithDraft`을(를) 요청합니다.

```http
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

응답에는 다음이 포함됩니다.

- 메타데이터: state, displayName, description, apiName, idField, createdAt, updatedAt, dedupeFields, searchableFields, relationships.
- 표준 필드: marketoGUID, createdAt, updatedAt.
- 사용자 정의 필드: leadId, vin, make, model, year.

### 목록 유형

[List Custom Object Types](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/listCustomObjectTypesUsingGET) 끝점이 대상 인스턴스에서 사용할 수 있는 모든 사용자 지정 개체 유형에 대한 메타데이터를 반환합니다. [사용자 지정 개체 나열](https://experienceleague.adobe.com/docs/marketo-developer/marketo/soap/custom-objects/custom-objects.html?lang=en)과(와) 유사하지만 상태, 관계 및 필드와 같은 추가 메타데이터를 포함합니다.

승인된 버전이 있으면 끝점이 이를 반환합니다. 그렇지 않으면 초안 버전이 반환됩니다.

선택적 매개 변수는 다음과 같습니다.

- **state**: 반환할 버전을 지정합니다. 유효한 값은 **초안**, **승인됨** 및 **승인됨**&#x200B;입니다.
- **이름**: 쉼표로 구분된 API 이름 목록으로 반환할 사용자 지정 개체 형식을 지정합니다.

```http
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
            "description": "No really, it is a car!",
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

[사용자 지정 개체 유형 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) 끝점을 사용하여 사용자 지정 개체 유형을 만들거나 업데이트하십시오.

속성은 다음과 같습니다.

- **action**: 레코드 작업을 제어하는 선택적 특성입니다. 유효한 값은 **createOnly**, **createOrUpdate** 및 **updateOnly**&#x200B;입니다. 기본값은 createOrUpdate입니다.
- **displayName** 및 **apiName**: 작업이 updateOnly가 아니면 필요합니다. 고객이 프로비저닝한 유형과의 충돌을 방지하기 위해 둘 다 고유해야 합니다. LaunchPoint 파트너는 대표 네임스페이스를 앞에 추가해야 합니다. apiName의 경우, 소문자 또는 카멜 대소문자를 사용하여 다른 텍스트 문자열과 구분합니다.
- **pluralName**: displayName의 plural 형식을 지정하는 선택적 특성입니다.
- **설명**: 사용자 지정 개체 형식을 설명하는 선택적 특성입니다.
- **showInLeadDetail**: Marketo UI의 [리드 데이터베이스] 페이지에서 사용자 지정 개체 데이터를 활성화하는 선택적 부울 특성입니다. 기본값은 false입니다.

사용자 지정 개체 이름을 신중하게 선택하십시오. 새 사용자 정의 개체 이름 각각에 회사를 식별하는 문자열을 접두사로 추가합니다. 접두사에는 영숫자 문자 또는 밑줄을 사용할 수 있습니다. 이 규칙을 사용하면 개체를 MLM UI에서 더 쉽게 찾을 수 있고 개체의 이름이 고유한지 확인할 수 있습니다.

다음 예제에서는 API 이름이 &quot;transaction&quot;인 사용자 지정 개체 유형을 만듭니다.

```http
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

다음 요청은 새로 생성된 유형을 설명합니다.

```http
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

응답에는 다음이 포함됩니다.

- 메타데이터: state, displayName, description, apiName, idField, createdAt, updatedAt, dedupeFields, searchableFields, relationships.
- 표준 필드: marketoGUID, createdAt, updatedAt.

#### 업데이트 유형

다음 예제에서는 API 이름이 &quot;transaction&quot;인 기존 유형의 설명을 업데이트합니다. **apiName** 특성이 필요합니다. 형식이 이미 있으므로 요청에서는 선택적 **action** 특성에 대해 updateOnly를 사용합니다.

**apiName** 외에 만드는 동안 사용할 수 있는 특성을 업데이트할 수 있습니다.

```http
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

사용하기 전에 사용자 지정 개체 유형을 승인하십시오. [사용자 지정 개체 형식 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/syncCustomObjectTypeUsingPOST) 끝점으로 형식을 만들면 Marketo에서 초안 버전을 만듭니다. 사용자 정의 필드를 추가한 후 초안을 승인합니다. 승인이 승인된 버전을 만들고 초안을 삭제합니다.

사용자 지정 개체 유형 동기화 또는 사용자 지정 개체 유형 필드 추가/업데이트/삭제로 기존 유형을 수정하면 Marketo에서 초안을 만듭니다. 유형 또는 해당 필드를 변경하면 초안 버전에만 영향을 줍니다. 변경 후 초안을 승인합니다. 승인은 승인된 버전을 초안으로 바꾸고 초안을 삭제합니다.

자세한 내용은 [사용자 지정 개체 승인 설명서](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)를 참조하세요.

사용자 정의 객체 유형이 승인되면 다음을 수행할 수 없습니다.

- `displayName` 또는 `apiName` 업데이트.
- 링크 필드를 추가하거나 제거합니다.
- 중복 제거 필드를 추가하거나 제거합니다.

유형을 승인하기 전에 스키마 및 명명 규칙을 신중하게 계획합니다.

### 승인 유형

[사용자 지정 개체 유형 승인](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/approveCustomObjectTypeUsingPOST) 끝점을 사용하여 초안을 새 승인된 버전으로 게시하십시오. **apiName** 경로 매개 변수만 필요합니다.

형식이 초안 상태이고 문서화된 [유효성 검사 규칙](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/approve-a-custom-object)을(를) 충족할 때만 형식을 승인할 수 있습니다.

```http
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

[사용자 지정 개체 유형 무시](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/discardCustomObjectTypeUsingPOST) 끝점을 사용하여 초안 버전을 삭제합니다. `apiName` 경로 매개 변수만 필요합니다.

초안 상태의 유형만 삭제할 수 있습니다. 승인된 유형은 삭제할 수 없습니다.

```http
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

[사용자 지정 개체 유형 삭제](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST) 끝점을 사용하여 승인된 버전을 삭제합니다. `apiName` 경로 매개 변수만 필요합니다.

이 작업은 파괴적이며 실행을 취소할 수 없습니다. 유형을 삭제하기 전에 트리거 및 필터와 같은 에셋에서 해당 사용을 제거하십시오. 사용자 지정 개체 종속 Assets 엔드포인트 가져오기 를 사용하여 유형에 대한 종속 에셋을 검색합니다.

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

- Marketo GUID: 사용자 지정 개체 유형에 대한 고유 식별자입니다.
- 생성 날짜: 사용자 지정 개체 유형을 만든 날짜/시간입니다.
- 업데이트 날짜: 사용자 지정 개체 유형을 마지막으로 업데이트한 날짜/시간입니다.

다음 끝점을 사용하여 사용자 정의 필드를 추가, 변경 또는 삭제합니다.

- 최대 필드 수는 50개입니다.
- 사용자 지정 개체가 승인되면 최대 20개의 추가 필드를 추가할 수 있습니다.
- 하나 이상의 데이터 중복 제거 필드가 필요합니다. 최대 3개의 데이터 중복 제거 필드가 허용됩니다.
- 필드 API 이름 및 표시 이름에는 영숫자와 밑줄 문자 &quot;_&quot;가 포함될 수 있습니다.

자세한 내용은 [사용자 지정 개체 필드 설명서](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하세요.

### 필드 추가

[사용자 지정 개체 유형 필드 추가](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/addCustomObjectTypeFieldsUsingPOST) 끝점을 사용하여 사용자 지정 개체에 하나 이상의 필드를 추가하십시오. 요청 본문에 하나 이상의 요소가 있는 `input` 배열이 있습니다. 각 요소는 필드를 설명하는 속성이 있는 JSON 개체입니다.

필드 속성은 다음과 같습니다.

- `name`: 필수 항목입니다. 사용자 지정 개체에 대해 고유해야 하는 필드의 API 이름입니다. 이름을 다른 텍스트 문자열과 구분하려면 소문자나 카멜 대소문자를 사용하십시오.
- `displayName`: 필수 항목입니다. 사람이 읽을 수 있는 필드 이름으로, 사용자 지정 개체에 고유해야 합니다.
- `dataType`: 필수 항목입니다. 필드의 데이터 형식입니다. [사용자 지정 개체 형식 필드 데이터 형식 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) 끝점을 사용하여 허용된 데이터 형식을 검색합니다.
- `description`: 선택 사항입니다. 필드 설명입니다.
- `isDedupeField`: 사용자 지정 개체 업데이트 작업 중에 필드가 중복 제거에 사용되는지 여부를 지정하는 선택적 부울입니다. 기본값은 false입니다. 일대다 관계에 중복 제거 필드가 필요합니다.
- `relatedTo`: 링크 필드를 지정하는 선택적 개체입니다. 일대다 관계의 경우 `name`은(는) &quot;링크 개체&quot; 또는 상위 개체를 식별하며, `field`은(는) 상위 개체의 &quot;링크 필드&quot; 또는 키 필드를 식별합니다.

사용자 지정 개체에는 데이터 유형이 &quot;link&quot;인 필드가 포함될 수 있습니다. 링크 필드는 사용자 지정 오브젝트와 다른 오브젝트 유형(예: Lead 및 Company) 간의 관계를 설정합니다. 링크 필드에 대한 자세한 내용은 [사용자 지정 개체 필드 설명서](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하세요. [사용자 지정 개체 연결 가능한 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) 끝점을 사용하여 허용된 링크 개체를 검색합니다.

사용자 지정 개체는 기존 링크 필드가 있는 다른 사용자 지정 개체에 연결할 수 없습니다. 자세한 내용은 [링크 필드 설명서](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)를 참조하세요.

### 일대다 관계

일대다 사용자 지정 개체 구조의 경우 링크 필드를 사용하여 사용자 지정 개체를 표준 리드 또는 회사 개체에 연결합니다. 다음 워크플로에서는 [자동차 소유자 예제](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)를 사용하여 자동차 정보를 저장하고 리드에 연결하는 사용자 지정 개체를 만듭니다.

1. **Car** 개체를 만듭니다.
1. **Car** 개체에 필드 추가: **VIN**&#x200B;에서 중복 제거하고 **잠재 고객**&#x200B;**/잠재 고객 ID**&#x200B;에 연결합니다.
1. **Car** 개체를 승인합니다.

먼저, 차량별 정보가 포함된 사용자 지정 개체 유형을 만듭니다.

```http
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

그런 다음 Car 사용자 지정 개체 유형에 필드를 추가합니다. 링크 필드를 사용하여 연결할 객체와 필드를 모두 지정합니다. 이 예제에서 링크 개체는 리드이고 링크 필드는 ID입니다.

중복 제거(VIN)에 문자열 필드를 사용합니다. Make, Model 및 Year 속성을 저장하려면 3개의 필드를 더 추가합니다.

```http
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

```http
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

다대다 관계는 Lead 또는 Company와 같은 표준 개체와 &quot;edge&quot; 사용자 지정 개체 간의 &quot;bridge&quot; 사용자 지정 개체를 사용합니다. Edge 객체는 기본 엔티티이며 설명 필드를 포함합니다.

브리지 개체는 두 링크 필드와의 관계를 해결합니다. 한 필드는 일대다 관계에서와 같이 상위 표준 개체를 가리킵니다. 다른 점은 링크가 없는 사용자 지정 객체인 Edge 객체를 가리킵니다. 브리지 객체에는 설명 필드가 포함될 수도 있습니다.

다음 워크플로에서는 [대학 과정 등록 예제](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-link-fields#AddMarketoCustomObjectLinkFields-CreateaLinkFieldforaOne-to-ManyStructure)를 사용합니다. Courses Edge 객체 및 Courses와 Leads를 연결하는 Enrollment Bridge 객체를 생성합니다.

1. **Course** Edge 개체를 만듭니다.
1. **과정 ID**&#x200B;에서 **과정:** 중복 제거에 필드를 추가합니다.
1. **과정**&#x200B;을(를) 승인합니다.
1. **등록** 브리지 개체를 만듭니다.
1. **등록:** **등록 ID**&#x200B;에 대한 중복 제거, **과정**&#x200B;**/과정 ID** 필드에 대한 링크 및 **잠재 고객**&#x200B;**/잠재 고객 ID**&#x200B;에 대한 링크를 추가하십시오.
1. **등록**&#x200B;을 승인합니다.

먼저 과정별 정보가 포함된 Edge 객체 유형을 작성합니다.

```http
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

다음으로, 4개의 사용자 정의 필드를 추가하여 대학 과정을 모델링합니다(과정 ID, 과정 강사, 과정 위치 및 과정 이름). 하나 이상의 중복 제거 필드가 필요하므로 과정 ID를 중복 제거 필드로 지정합니다.

```http
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

```json
{
    "requestId": "cc36#16895b82a41",
    "result": [],
    "success": true
}
```

브리지 객체 유형에 연결할 때 참조할 수 있도록 에지 객체 유형을 승인합니다. 사용자 지정 개체 유형을 링크 개체로 선택하려면 먼저 승인해야 합니다.

```http
POST /rest/v1/customobjects/schema/course/approve.json
```

```json
{
    "requestId": "460b#16896055fa3",
    "result": [],
    "success": true
}
```

Edge 객체를 완료한 후 등록별 정보가 포함된 Bridge 객체 유형을 작성합니다.

```http
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

Lead 객체에 연결되는 링크 필드와 Course 객체에 연결되는 링크 필드를 bridge 객체 유형에 추가합니다. 잠재 고객 ID 필드를 사용하여 잠재 고객에 연결하고 과정 ID 필드를 사용하여 과정에 연결합니다.

하나 이상의 중복 제거 필드가 필요하므로 등록 ID를 중복 제거 필드로 추가합니다. 그런 다음 성적 필드를 추가하여 학생의 성과를 추적합니다.

```http
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

```http
POST /rest/v1/customobjects/schema/enrollment/approve.json
```

```json
{
    "requestId": "9a76#16897b0e84b",
    "result": [],
    "success": true
}
```

[사용자 지정 개체 동기화](#create_and_update) 또는 [대량 사용자 지정 개체 가져오기](https://experienceleague.adobe.com/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import.html?lang=en)를 사용하여 프로그래밍 방식으로 사용자 지정 개체 레코드를 채웁니다. 또는 Marketo UI에서 [사용자 지정 개체 데이터 가져오기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/import-custom-object-data)를 사용합니다.

## 필드 업데이트

[사용자 지정 개체 유형 필드 업데이트](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/updateCustomObjectTypeFieldUsingPOST) 끝점을 사용하여 초안 사용자 지정 개체의 필드를 업데이트하십시오.

필수 경로 매개 변수는 다음과 같습니다.

- `apiName`: 사용자 지정 개체 형식의 API 이름입니다.
- `fieldAPIName`: 사용자 지정 개체 유형 필드의 API 이름입니다.

요청 본문에는 업데이트할 필드 속성을 지정하는 키/값 쌍이 있는 JSON 오브젝트가 포함됩니다.

```http
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

[사용자 지정 개체 유형 필드 삭제](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/deleteCustomObjectTypeFieldsUsingPOST) 끝점을 사용하여 사용자 지정 개체에서 하나 이상의 필드를 삭제합니다. 필수 `apiName` 경로 매개 변수는 사용자 지정 개체 형식의 API 이름을 지정합니다.

요청 본문에 하나 이상의 요소 배열이 `input`인 JSON 개체가 있습니다. 각 요소는 `name` 특성이 삭제할 필드의 API 이름을 지정하는 JSON 개체입니다.

```http
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

[사용자 지정 개체 형식 필드 데이터 형식 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeFieldDataTypesUsingGET) 끝점은 허용된 모든 필드 데이터 형식을 반환합니다. 이 끝점을 사용하여 사용자 지정 개체 유형을 모델링할 때 사용할 수 있는 사용자 지정 필드 데이터 유형을 식별합니다.

```http
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

[사용자 지정 개체 연결 가능 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeLinkableObjectsUsingGET) 끝점은 허용된 모든 링크 개체와 해당 링크 필드를 반환합니다. 응답에는 Lead 및 Company 와 같은 표준 개체와 인스턴스에서 만든 모든 사용자 지정 개체가 포함됩니다.

```http
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

[사용자 지정 개체 종속 Assets 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects/operation/getCustomObjectTypeDependentAssetsUsingGET) 끝점은 사용자 지정 개체 형식의 종속 자산과 해당 인스턴스의 위치를 반환합니다. 통합을 제거할 때 사용자 지정 오브젝트 유형이 사용 중인 모든 곳에서 식별할 수 있도록 이 유형을 사용하십시오.

```http
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

- 사용자 지정 개체 엔드포인트에는 특별한 언급이 없는 한 30초의 시간 제한이 있습니다.
- 사용자 지정 개체 동기화의 시간 제한은 120초입니다.
- 사용자 지정 개체 삭제의 시간 제한은 60초입니다.
