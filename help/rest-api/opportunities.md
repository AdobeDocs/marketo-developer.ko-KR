---
title: 기회
feature: REST API
description: ' Marketo API를 사용하여 기회를 구성합니다.'
exl-id: 46451285-4125-4857-890a-575069a68288
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 기회

[영업 기회 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)

Marketo은 영업 기회 레코드를 읽고, 쓰고, 만들고, 업데이트하는 API를 표시합니다. Marketo에서 기회 레코드는 중간 Opportunity Role 객체를 통해 Lead 및 Contact Records에 연결되므로 Opportunity 는 많은 개별 Lead에 연결될 수 있습니다.  이러한 객체 유형은 모두 API를 통해 노출되며 대부분의 리드 데이터베이스 객체 유형과 마찬가지로 둘 다 해당 Describe 호출을 가지고 있습니다. 이 호출은 객체 유형에 대한 메타데이터를 반환합니다.

영업 기회 API는 [SFDC 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en)가 활성화된 구독에 대한 읽기 전용 액세스입니다.

## 설명

Opportunity 레코드를 설명하는 것은 리드 데이터베이스 객체에 대한 표준 패턴을 따릅니다.

```
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

이 응답 형식에 가장 중요한 필드는 `idField`, `dedupeFields` 및 `searchableFields`입니다.  idField는 영업 기회의 기본 키인 marketoGUID를 나타냅니다.  이 키는 시스템에서 생성한 고유 키로, 읽기 및 업데이트 작업에는 사용할 수 있지만 시스템 관리이므로 삽입에는 사용할 수 없습니다.  dedupeFields 배열은 삽입 작업에 유효한 필드를 나타냅니다. 기회의 경우 externalOpportunityId일 뿐입니다.  searchableFields 배열은 쿼리용으로 유효한 필드 집합, externalOpportunityId 및 marketoGUID를 제공합니다.

## 쿼리

[기회 쿼리](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunitiesUsingGET)에 대한 패턴은 `filterType` 매개 변수가 `searchableFields` 배열 또는 해당 설명 호출에 나열된 필드 또는 dedupeFields를 수락하는 추가 제한 사항을 가진 잠재 고객 API의 패턴을 거의 따릅니다.  사용자 정의 영업 기회 필드를 사용하는 경우 문자열 또는 정수 유형의 사용자 정의 영업 기회 필드만 searchableFields 배열에 나열됩니다.

```
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

또한 기본 및 최대 300인 배치 크기 `fields`보다 큰 집합을 통해 페이징하기 위한 추가 영업 기회 필드 반환용 선택적 쿼리 매개 변수 `nextPageToken`, `batchSize`을(를) 포함할 수 있습니다.  `fields` 목록을 요청할 때 특정 필드가 요청되었지만 반환되지 않은 경우 값이 null인 것으로 간주됩니다.

## 만들기 및 업데이트

영업 기회는 몇 가지 제한 사항을 제외하고 리드 API 패턴을 면밀히 따릅니다.  `action`에 사용할 수 있는 값은 createOnly, createOrUpdate 및 updateOnly입니다.  createOnly 또는 createOrUpdate 모드를 사용할 때 externalOpportunityId 필드를 각 레코드에 포함해야 합니다.  updateOnly 모드의 경우 marketoGUID 또는 externalOpportunityId 중 하나를 사용할 수 있습니다.  지정되지 않은 경우 모드는 기본적으로 createOrUpdate로 설정됩니다.

리드 API의 `lookupField` 매개 변수는 사용할 수 없으며, action이 updateOnly인 경우에만 유효한 dedupeBy 매개 변수로 대체됩니다.  dedupeBy에 사용할 수 있는 값은 externalOpportunityId 및 marketoGUID로 각각 설명 호출에 의해 지정된 &quot;dedupeFields&quot; 또는 &quot;idField&quot;입니다.  dedupeBy가 지정되지 않은 경우 dedupeFields 모드로 기본 설정됩니다.  &#39;name&#39; 필드는 null이 아니어야 합니다.

한 번에 최대 300개의 레코드를 제출할 수 있습니다.

```
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

API는 각 레코드에 대한 `marketoGUID`, 각 레코드의 개별 성공 또는 실패를 나타내는 `status` 필드 및 제출된 레코드를 응답 순서에 연결하는 데 사용되는 `seq` 필드와 함께 응답합니다.  필드의 숫자는 요청에서 제출된 레코드의 색인입니다.

### 필드

회사 개체에는 필드 집합이 포함되어 있습니다.  각 필드 정의는 필드를 설명하는 속성 세트로 구성됩니다.  속성의 예로는 디스플레이 이름, API 이름 및 dataType이 있습니다.  이러한 속성을 통칭하여 메타데이터라고 합니다.

다음 엔드포인트를 사용하면 회사 개체의 필드를 쿼리할 수 있습니다. 이러한 API를 사용하려면 소유 API 사용자에게 `Read-Write Schema Standard Field` 또는 `Read-Write Schema Custom Field` 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

### 쿼리 필드

영업 기회 필드를 쿼리하는 것은 간단합니다.  API 이름으로 단일 회사 필드를 쿼리하거나 모든 회사 필드 집합을 쿼리할 수 있습니다.

#### 이름별

[이름별 영업 기회 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldByNameUsingGET) 끝점은 회사 개체에서 단일 필드에 대한 메타데이터를 검색합니다.  필수 `fieldApiName` 경로 매개 변수는 필드의 API 이름을 지정합니다.  응답은 Describe Opportunity 끝점과 비슷하지만 필드가 사용자 지정 필드인지 여부를 나타내는 `isCustom` 특성과 같은 추가 메타데이터를 포함합니다.

```
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

[영업 기회 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityFieldsUsingGET) 끝점은 회사 개체의 모든 필드에 대한 메타데이터를 검색합니다.  기본적으로 최대 300개의 레코드가 반환됩니다.  `batchSize` 쿼리 매개 변수를 사용하여 이 수를 줄일 수 있습니다.  `moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다.  moreResult 특성이 false를 반환할 때까지 이 끝점을 계속 호출합니다. 즉, 사용 가능한 결과가 없습니다.  이 API에서 반환된 `nextPageToken`은(는) 항상 이 호출의 다음 반복에 재사용해야 합니다.

```
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

데이터 중복 제거 필드 또는 ID 필드를 통해 영업 기회를 삭제할 수 있습니다. dedupeFields 또는 idField 값이 있는 `deleteBy` 매개 변수를 사용하여 지정합니다. 지정하지 않으면 기본값은 dedupeFields입니다. 요청 본문에 삭제할 `input` 기회의 배열이 있습니다. 호출당 최대 300개의 기회가 허용됩니다.

```
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

- 아래에 명시되지 않는 한 영업 기회 엔드포인트의 시간 제한은 30초입니다.
   - 동기화 기회: 60초 
   - 기회 삭제: 60초
