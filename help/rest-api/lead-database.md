---
title: "잠재 고객 데이터베이스"
feature: REST API, Database
description: "기본 리드 데이터베이스를 조작합니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---


# 잠재 고객 데이터베이스

Marketo 리드 데이터베이스 API는 활동, 기회 및 회사와 같은 Marketo의 개인 및 개인 관련 데이터를 교환할 수 있도록 Marketo에서 제공하는 가장 자주 사용되는 API입니다.

## 오브젝트

리드 데이터베이스 객체에는 다음이 포함됩니다.

- 잠재 고객
- 회사/계정
- 명명된 계정
- 기회
- OpportunityRoles
- SalesPerson
- 사용자 지정 개체
- 활동
- 목록 및 프로그램 멤버십

이러한 개체에는 Create, Read, Update 및 Delete 메서드가 대부분 포함되어 있습니다. 또한 각 유형에 대해 사용 가능한 필드 목록과 중복 제거에 사용되는 필드 목록(비잠재 고객 개체의 경우)을 제공하고 레코드 검색을 위해 검색할 수 있는 &quot;설명&quot; 방법도 포함되어 있습니다. 잠재 고객의 경우 Marketo 애플리케이션 내에서 가장 다양한 기능을 제공하므로 가장 풍부한 세트가 제공됩니다.

## API

매개 변수 및 모델링 정보를 포함한 리드 데이터베이스 API 끝점의 전체 목록은 다음을 참조하십시오. [잠재 고객 데이터베이스 API 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/).

기본 CRM 통합이 활성화된 인스턴스(Microsoft Dynamics 또는 Salesforce.com)의 경우 Company, Opportunity, Opportunity Role 및 Sales Person API가 비활성화됩니다. 이 레코드는 활성화되면 CRM을 통해 관리되며 Marketo의 API를 통해 액세스하거나 업데이트할 수 없습니다.

- 최대 배치 크기(표준): 300개 레코드
- 최대 배치 크기(벌크): 10MB 파일
- 기본 배치 크기: 레코드 300개
- Content-type 헤더(standard): application/json
- Content-type 헤더(bulk): multipart/form-data

## 설명

리드, 회사, 기회, 역할, SalesPersons 및 사용자 정의 객체의 경우 description API가 제공됩니다. 이를 호출하면 개체의 메타데이터와 업데이트 및 쿼리에 사용할 수 있는 필드 목록이 검색됩니다. 설명은 Marketo과의 적절한 통합을 디자인하는 데 있어 중요한 부분입니다. 또한 객체를 생성, 업데이트 및 쿼리할 수 있는 방법뿐만 아니라 객체와 상호 작용할 수 있고 상호 작용할 수 없는 방법에 대한 풍부한 메타데이터를 제공합니다. Describe Leads 외에에서 사용할 수 있는 키 목록을 각각 반환합니다. `deduplication` 다음에서 `dedupeFields` 응답 매개 변수. 필드 목록은 의 쿼리를 위한 키로 사용할 수 있습니다. `searchableFields` 응답 매개 변수.

```
GET /rest/v1/opportunities/roles/describe.json
```

```json
{  
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[  
      {  
         "name":"opportunityRole",
         "displayName":"Opportunity Role",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"marketoGUID",
         "dedupeFields":[  
            "externalOpportunityId",
            "leadId",
            "role"
         ],
         "searchableFields":[  
            [  
               "externalOpportunityId",
               "leadId",
               "role"
            ],
            [  
               "marketoGUID"
            ],
            [  
               "leadId"
            ],
            [  
               "externalOpportunityId"
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
               "name":"externalOpportunityId",
               "displayName":"External Opportunity Id",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {  
               "name":"leadId",
               "displayName":"Lead Id",
               "dataType":"integer",
               "updateable":false
            },
            {  
               "name":"role",
               "displayName":"Role",
               "dataType":"string",
               "length":50,
               "updateable":false
            },
            {  
               "name":"isPrimary",
               "displayName":"Is Primary",
               "dataType":"boolean",
               "updateable":true
            },
            {  
               "name":"externalCreatedDate",
               "displayName":"External Created Date",
               "dataType":"datetime",
               "updateable":true
            }
         ]
      }
   ]
}
```

이 예에서는 `dedupeFields` 는 실제로 복합 키입니다. 즉, 나중에 를 사용할 때 를 업데이트하고 만듭니다. `dedupeFields` 모드, 다음 세 가지를 모두 포함해야 합니다. `externalOpportunityId`, `leadId`, 및 `role` 각 역할에 대해 다음 `searchableFields` 배열은 또한 역할 레코드를 쿼리하는 데 사용할 수 있는 필드 목록을 제공합니다. 여기에 의 복합 키도 포함됩니다. `externalOpportunityId`, `leadId`, 및 `role`.

각 필드의 이름인 을 제공하는 필드 응답 매개 변수도 있습니다. `displayName` Marketo UI에 표시되는 대로 필드의 데이터 형식, 생성 후 업데이트할 수 있는지 여부 및 해당하는 경우 필드의 길이.

## 쿼리

리드 데이터베이스 개체는 모두 하나의 필드만 참조되는 단순 키에 대한 쿼리를 위한 기본 패턴을 공유합니다.

```
GET /rest/v1/{type}.json?filterType={field to query}&filterValues={comma-separated list of possible values}
```

리드를 제외한 모든 오브젝트에 대해 해당 설명 호출의 searchableFields에서 {쿼리할 필드}를 선택하고 최대 300개의 값을 쉼표로 구분한 목록을 구성할 수 있습니다. 다음과 같은 선택적 쿼리 매개 변수도 있습니다.

- `batchSize` - 반환할 결과 수의 정수 카운트입니다. 기본값과 최대값은 300입니다.
- `nextPageToken` - 페이징을 위한 이전 호출에서 반환된 토큰입니다. 다음을 참조하십시오 [페이징 토큰](paging-tokens.md) 추가 세부 정보.
- `fields` - 각 레코드에 대해 반환할 필드 이름을 쉼표로 구분한 목록입니다. 유효한 필드 목록은 해당 설명을 참조하십시오. 특정 필드가 요청되었지만 반환되지 않은 경우 이 값은 null로 간주됩니다.
- `_method` - POST HTTP 메서드를 사용하여 쿼리를 제출하는 데 사용됩니다. 사용법은 아래의 _method=GET 섹션을 참조하십시오.

간단한 예를 위해 기회 쿼리를 살펴보겠습니다.

```
GET /rest/v1/opportunities.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb
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

다음 `filterType` 이 호출에 지정된 은(는) &quot;marketoGUID&quot;가 아닌 &quot;idField&quot;입니다. 이 및 &quot;dedupeFields&quot;는 모두 idField 또는 dedupeFields에 해당하는 필드에 이러한 방식으로 별칭을 지정할 수 있는 특별한 경우입니다. &quot;marketoGUID&quot;는 여전히 호출에서 결과 조회 필드이지만 호출에서는 명시적으로 설정되지 않습니다. 필드 및/또는 필드에 의해 표시되는 세트 `idField` 및 `dedupeFields` 개체 설명은 항상 유효합니다. `filterTypes` 쿼리의 경우. 이 호출은 filterValues에 포함된 GUID와 일치하는 레코드를 검색하고 일치하는 레코드를 반환합니다. 이 방법을 사용하여 찾은 레코드가 없는 경우 응답은 여전히 성공을 나타내지만, 검색이 성공적으로 실행되었으므로 결과 배열은 비어 있지만 반환할 레코드가 없습니다.

쿼리의 레코드 집합이 300개를 초과하는 경우 또는 `batchSize` 둘 중 더 작은 것이 지정되면 응답에 멤버가 포함됩니다 `moreResult` 값을 true로 설정하고 `nextPageToken`: 더 많은 세트를 검색하기 위해 후속 호출에 포함될 수 있습니다. 다음을 참조하십시오 [페이징 토큰](paging-tokens.md) 을 참조하십시오.

### 긴 URI

GUID로 쿼리할 때와 같이 URI가 길고 REST 서비스에서 허용하는 8KB를 초과할 수도 있습니다. 이 경우 GET 대신 HTTP POST 메서드를 사용하고 쿼리 매개 변수를 추가해야 합니다 `_method=GET`. 또한 쿼리 매개 변수의 나머지 부분을 POST 본문에 &quot;application/x-www-form-urlencoded&quot; 문자열로 전달하고 관련 Content-type 헤더를 전달해야 합니다.

```
POST /rest/v1/opportunities.json?_method=GET
```

```
Content-Type: application/x-www-form-urlencoded
```

```
filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb,544fb7f5-2ddf-4fca-ae32-7e6ef1415e9f,f1ba41a2-69d1-4a35-9807-0e159d66f2c9,f7521272-3331-4a89-a768-222baff2f894
```

긴 URI 외에 복합 키를 쿼리할 때도 이 매개 변수가 필요합니다.

### 복합 키

복합 키를 쿼리하는 패턴은 JSON 본문이 있는 POST을 제출해야 하므로 단순 키와 다릅니다. 모든 경우에 이러한 작업이 필요한 것은 아니며 `dedupeFields` 여러 필드가 있는 옵션은 `filterType`. 현재 복합 키는 Opportunity 역할과 일부 사용자 지정 개체에서만 사용됩니다. 의 복합 키가 있는 Opportunity Roles에 대한 쿼리의 예를 살펴보겠습니다. `dedupeFields`:

```
POST /rest/v1/opportunities/roles.json?_method=GET
```

```json
{  
   "filterType":"dedupeFields",
   "fields":[  
      "marketoGuid",
      "externalOpportunityId",
      "leadId",
      "role"
   ],
   "input":[  
      {  
        "externalOpportunityId":"Opportunity1",
        "leadId": 1,
        "role": "Captain"
      },
      {  
        "externalOpportunityId":"Opportunity2",
        "leadId": 1872,
        "role": "Commander"
      },
      {  
        "externalOpportunityId":"Opportunity3",
        "leadId": 273891,
        "role": "Lieutenant Commander"
      }
   ]
}
```

JSON 개체의 구조는 대부분 평면이며, 단순 키가 있는 쿼리에 대한 모든 쿼리 매개 변수는 유효한 멤버입니다. 단, `filterValues`. 필터 값 대신 JSON 개체의 &quot;입력&quot; 배열이 있으며, 각 배열에는 복합 키의 각 필드에 대한 멤버가 있어야 합니다. 이 경우 다음과 같습니다. `externalOpportunityId`, `leadId`, 및 `role`. 다음에 대한 쿼리를 실행합니다. `roles`을 클릭하고, 제공된 입력을 확인한 후 일치하는 결과를 반환합니다. 응답이 을 사용하여 매개 변수를 반환하는 경우 `moreResult=true`, 및 `nextPageToken`, 모든 원래 입력 및 `nextPageToken` 쿼리가 제대로 실행되도록 합니다.

## 만들기 및 업데이트

리드 데이터베이스 레코드에 대한 생성 및 업데이트는 모두 JSON 본문이 있는 POST를 통해 수행됩니다. Opportunity, Roles, Custom Object, Company 및 SalesPersons에 대한 인터페이스는 각각 동일합니다. Lead 의 인터페이스가 약간 다르며 그에 대한 자세한 내용은 여기에서 자세히 읽어볼 수 있습니다.

유일한 필수 매개 변수는 라는 배열입니다. `input` 멤버로 삽입/업데이트할 필드가 있는 개체를 최대 300개까지 포함할 수 있습니다. 다음을 선택적으로 포함할 수도 있습니다. `action` 다음 중 하나가 될 수 있는 매개 변수: `createOnly`, `updateOnly`, 또는 `createOrUpdate`. 작업이 생략되면 모드의 기본값은 `createOrUpdate`. `dedupeBy` action이 createOnly 또는 `createOrUpdate`. ` dedupeBy` 다음 중 하나일 수 있습니다. `idField`, 또는 `dedupeFields`. If `idField` 이 선택된 다음 `idField` 설명에 나와 있는 이(가) 중복 제거에 사용되며 각 레코드에 포함되어야 합니다. `idField` 모드가 와(과) 호환되지 않음 `createOnly` 모드. If `dedupeFields` 이(가) 선택된 후 `dedupeFields` 사용된 개체 설명에 나열되며 각 레코드는 반드시 포함되어야 합니다. 다음과 같은 경우 `dedupeBy` 매개 변수가 생략되고 모드의 기본값은 입니다. `dedupeFields`.

필드 값 목록을 전달할 때 값 `null`또는 빈 문자열은 다음과 같이 데이터베이스에 기록됩니다. `null`.

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

리드 API 이외의 리드 데이터베이스 개체를 만들거나 업데이트하는 호출은 `seq` 의 각 개체에 있는 필드 `result` 배열입니다. 나열된 숫자는 요청에서 업데이트된 레코드의 순서에 해당합니다. 각 항목은 다음 값을 반환합니다. `idField` 객체 유형의 경우 및 `status`. 상태 필드는 &quot;생성됨&quot;, &quot;업데이트됨&quot; 또는 &quot;건너뜀&quot; 중 하나를 나타냅니다.  상태를 건너뛸 경우, 레코드를건너뛴 이유를 나타내는 코드와 메시지를 포함하는 하나 이상의 이유 오브젝트가 있는 해당 &quot;이유&quot; 배열도 있습니다. 다음을 참조하십시오 [오류 코드](error-codes.md) 추가 세부 정보.

### 삭제

삭제 인터페이스는 리드 이외의 리드 데이터베이스 개체에 대해 표준입니다. 입력 외에 필요한 매개 변수는 하나만 있습니다 `deleteBy,` idField 또는 dedupeFields 값을 가질 수 있습니다. 몇 가지 사용자 지정 개체 삭제를 살펴보겠습니다.

```
POST /rest/v1/customobjects/{name}/delete.json
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
```

```json
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

다음 `seq`, `status`, `marketoGUID`, 및 `reasons` 지금쯤 모두 익숙하실 겁니다.

각 개별 객체 유형에 대한 CRUD 작업 작업에 대한 자세한 내용은 해당 페이지를 확인하십시오.
