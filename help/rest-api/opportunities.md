---
title: 기회
feature: REST API
description: SFDC 또는 Dynamics 동기화를 통해 기회, 중복 제거 및 검색 가능한 필드, 제한 사항, 읽기 전용 동작을 설명, 쿼리, 만들기 및 업데이트하는 Marketo REST API입니다.
exl-id: 46451285-4125-4857-890a-575069a68288
TQID: https://experienceleague.adobe.com/rBDJcXWQrN5qyKRWHyzVC-sc9BH2mQFLm7fKUk-NUn8
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 708
ht-degree: 0%

---

# 기회

[영업 기회 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities)

Marketo은 영업 기회 레코드를 읽고, 쓰고, 만들고, 업데이트하는 API를 제공합니다. Marketo에서 중간 영업 기회 역할 개체는 영업 기회 레코드를 리드 및 연락처 레코드에 연결합니다. 따라서 영업 기회는 많은 개별 리드에 연결될 수 있습니다.

API는 두 개체 유형을 노출합니다. 대부분의 리드 데이터베이스 객체 유형과 마찬가지로 각 유형에는 객체 메타데이터를 반환하는 해당 Describe 호출이 있습니다.

영업 기회 API는 [SFDC 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en)가 활성화된 구독에 대해 읽기 전용 액세스를 제공합니다.

## 설명

잠재 고객 데이터베이스 객체에 대한 표준 패턴을 사용하여 영업 기회 레코드를 설명합니다.

```http
GET /rest/v1/opportunities/describe.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"opportunity",
         "displayName":"Opportunity",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":[
            "externalOpportunityId"
         ],
         "searchableFields":[
            [
               "externalOpportunityId"
            ],
            [
               "marketoGUID"
            ]
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
               "name":"externalOpportunityId",
               "displayName":"External Opportunity Id",
               "dataType":"string",
               "length":50,
               "updateable":false
            }
         ]
      }
   ]
}
```

주요 응답 필드는 다음과 같습니다.

- `idField`: 영업 기회 기본 키인 marketoGUID를 식별합니다. 이 시스템 생성 키는 읽기 및 업데이트 작업을 지원하지만 삽입은 지원하지 않습니다.
- `dedupeFields`: 삽입 작업에 유효한 키를 식별합니다. 영업 기회의 경우 유일한 키는 externalOpportunityId 입니다.
- `searchableFields`: 쿼리에 유효한 필드를 식별합니다. 이러한 필드는 externalOpportunityId 및 marketoGUID입니다.

## 쿼리

[기회 쿼리](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunitiesUsingGET)의 패턴은 리드 API를 거의 따릅니다. 그러나 `filterType` 매개 변수는 해당 Describe 응답 또는 dedupeFields의 `searchableFields` 배열에 나열된 필드만 허용합니다.

사용자 정의 영업 기회 필드의 경우 String 또는 Integer 유형의 필드만 searchableFields 배열에 나타납니다.

```http
GET /rest/v1/opportunities.json?filterType=marketoGUID&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fa ",
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {
         "seq":1,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc ",
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
      }
   ]
}
```

다음과 같은 선택적 쿼리 매개 변수를 포함할 수 있습니다.

- `fields`: 추가 영업 기회 필드를 반환합니다.
- `nextPageToken`: 결과 집합의 페이지가 일괄 처리 크기보다 큽니다.
- `batchSize`: 일괄 처리 크기를 지정합니다. 기본값과 최대값은 300입니다.

`fields` 목록을 요청할 때 반환되지 않은 요청된 필드에 null의 묵시적 값이 있습니다.

## 만들기 및 업데이트

Opportunity 는 몇 가지 제한 사항이 있는 Leads API 패턴을 따릅니다. `action` 값은 createOnly, createOrUpdate 및 updateOnly입니다.

- createOnly 또는 createOrUpdate 모드의 경우 각 레코드에 externalOpportunityId 필드를 포함합니다.
- updateOnly 모드의 경우 marketoGUID 또는 externalOpportunityId를 사용합니다.
- 지정하지 않으면 기본값은 createOrUpdate입니다.

리드 API의 `lookupField` 매개 변수를 사용할 수 없습니다. dedupeBy 매개 변수는 이 매개 변수를 대체하며 action이 updateOnly인 경우에만 유효합니다.

dedupeBy 값은 Describe 응답이 각각 externalOpportunityId 및 marketoGUID로 식별하는 &quot;dedupeFields&quot; 및 &quot;idField&quot;입니다. dedupeBy가 지정되지 않은 경우 dedupeFields 모드로 기본 설정됩니다. &#39;name&#39; 필드는 null이 아니어야 합니다.

한 번에 최대 300개의 레코드를 제출할 수 있습니다.

```http
POST /rest/v1/opportunities.json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalOpportunityId":"19UYA31581L000000",
         "name":"Chairs",
         "description":"Chairs",
         "amount":"1604.47",
         "source":"Inbound Sales Call/Email"
      },
      {
         "externalOpportunityId":"29UYA31581L000000",
         "name":"Big Dog Day Care-Phase12",
         "description":"Big Dog Day Care-Phase12",
         "amount":"1604.47",
         "source":"Email"
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
         "status":"updated",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":1,
         "status":"created",
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb"
      }
   ]
}
```

응답에는 각 레코드에 대한 다음 값이 포함됩니다.

- `marketoGUID`: 레코드 식별자입니다.
- `status`: 개별 레코드의 성공 또는 실패.
- `seq`: 요청 레코드와 응답 순서를 연결하는 제출된 레코드의 인덱스입니다.

### 필드

회사 개체에는 표시 이름, API 이름 및 dataType과 같은 특성으로 정의된 필드가 포함되어 있습니다. 이러한 특성을 함께 메타데이터라고 합니다.

다음 엔드포인트는 회사 개체의 쿼리 필드를 나타냅니다. API 사용자에게는 `Read-Write Schema Standard Field` 권한, `Read-Write Schema Custom Field` 권한 또는 둘 다 있는 역할이 있어야 합니다.

### 쿼리 필드

API 이름으로 한 회사 필드를 쿼리하거나 모든 회사 필드를 검색합니다.

#### 이름별

[이름별 Get Opportunity 필드](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityFieldByNameUsingGET) 끝점은 회사 개체에서 한 필드에 대한 메타데이터를 검색합니다. 필수 `fieldApiName` 경로 매개 변수는 필드의 API 이름을 지정합니다.

이 응답은 Describe Opportunity 응답과 유사하지만 추가 메타데이터를 포함합니다. 예를 들어 `isCustom` 특성은 필드가 사용자 지정인지 여부를 나타냅니다.

```http
GET /rest/v1/opportunities/schema/fields/externalOpportunityId.json
```

```json
{
    "requestId": "12331#17e9779cb4b",
    "result": [
        {
            "displayName": "SFDC Oppty Id",
            "name": "externalOpportunityId",
            "description": null,
            "dataType": "string",
            "length": 50,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true
}
```

#### 찾아보기

[영업 기회 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityFieldsUsingGET) 끝점은 회사 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드를 반환합니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

`moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. moreResult가 false가 될 때까지 반환된 `nextPageToken`을(를) 사용하여 끝점을 계속 호출합니다.

```http
GET /rest/v1/opportunities/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "b4a#17e995b31da",
    "result": [
        {
            "displayName": "SFDC Oppty Id",
            "name": "externalOpportunityId",
            "description": null,
            "dataType": "string",
            "length": 50,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Name",
            "name": "name",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Description",
            "name": "description",
            "description": null,
            "dataType": "string",
            "length": 2000,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Type",
            "name": "type",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Stage",
            "name": "stage",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "E5ZONGE4SAHALYYW6FS25KB5BM======",
    "moreResult": true
}
```

#### 삭제

중복 제거 필드 또는 ID 필드로 영업 기회를 삭제합니다. `deleteBy` 매개 변수를 dedupeFields 또는 idField로 설정하십시오. 기본값은 dedupeFields 입니다.

요청 본문에 삭제할 `input` 기회의 배열이 있습니다. 각 통화에는 최대 300회의 기회가 허용됩니다.

```http
POST /rest/v1/opportunities/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "externalOpportunityId":"19UYA31581L000000"
      },
      {
         "externalOpportunityId":"29UYA31581L000000"
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
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status":"deleted"
      },
      {
         "seq":1,
         "marketoGUID":"cff23271-f996-47d7-984f-f2676861b5fb",
         "status":"deleted"
      }
   ]
}
```

## 시간 초과

- 달리 명시되지 않는 한 영업 기회 엔드포인트에 30초의 시간 제한이 있습니다.
- 동기화 기회의 시간 제한은 60초입니다.
- Delete Opportunities에는 60s의 시간 제한이 있습니다.
