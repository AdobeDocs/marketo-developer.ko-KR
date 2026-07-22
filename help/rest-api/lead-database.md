---
title: 리드 데이터베이스
feature: REST API, Database
description: 오브젝트, CRUD 및 설명 방법, 쿼리 패턴, 배치 제한 및 CRM 통합 제한을 다루는 Marketo 리드 데이터베이스 API에 대한 안내입니다.
exl-id: e62e381f-916b-4d56-bc3d-0046219b68d3
TQID: https://experienceleague.adobe.com/7lGbhE92lvIE-XkMyUIaK9GrreZVRdM-WVZTpHARhxE
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
source-wordcount: 1058
ht-degree: 1%

---

# 리드 데이터베이스

Marketo 리드 데이터베이스 API는 개인 및 개인 관련 데이터를 Marketo과 교환합니다. 이 데이터에는 활동, 기회 및 회사가 포함됩니다.

## 개체

리드 데이터베이스에는 다음 객체가 포함됩니다.

- 잠재 고객
- 회사/계정
- 지정 계정
- 기회
- OpportunityRoles
- SalesPerson
- 사용자 정의 오브젝트
- 활동
- 목록 및 프로그램 멤버십

대부분의 리드 데이터베이스 객체는 Create, Read, Update 및 Delete 메서드를 지원합니다. Describe 메서드는 각 개체 유형에 사용할 수 있는 필드를 제공합니다. 리드 이외 객체의 경우 중복 제거에 사용되는 필드와 레코드를 검색할 때 검색할 수 있는 필드도 식별합니다.

잠재 고객이 Marketo 애플리케이션에서 가장 다양한 용도로 사용되기 때문에 잠재 고객 개체는 가장 광범위한 기능 세트를 지원합니다.

## API

리드 데이터베이스 API 끝점, 매개 변수 및 모델링 정보에 대한 전체 목록은 [리드 데이터베이스 API 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi)를 참조하십시오.

인스턴스에 기본 Microsoft Dynamics 또는 Salesforce.com CRM 통합이 있는 경우 회사, 영업 기회, 영업 기회 역할 및 영업 사원 API가 비활성화됩니다. CRM에서 이러한 레코드를 관리하므로 Marketo API를 통해 액세스하거나 업데이트할 수 없습니다.

- 최대 배치 크기(표준): 300개 레코드
- 최대 배치 크기(벌크): 10MB 파일
- 기본 배치 크기: 레코드 300개
- Content-type 헤더(standard): application/json
- Content-type 헤더(bulk): multipart/form-data

## 설명

Describe API는 리드, 회사, 기회, 역할, SalesPersons 및 사용자 지정 개체에 사용할 수 있습니다. 개체 메타데이터와 업데이트 및 쿼리에 사용할 수 있는 필드를 검색하는 데 사용합니다.

Describe Leads를 제외하고 각 Describe 엔드포인트는 다음을 반환합니다.

- `dedupeFields`: 중복 제거에 사용할 수 있는 키.
- `searchableFields`: 쿼리에 사용할 수 있는 키.

```http
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

이 예제에서 `dedupeFields`은 복합 키입니다. 나중에 만들고 업데이트하기 위해 `dedupeFields` 모드를 사용하는 경우 각 역할에 대해 `externalOpportunityId`, `leadId` 및 `role`을(를) 포함합니다.

`searchableFields` 배열은 역할 레코드를 쿼리하는 데 사용할 수 있는 필드를 나열합니다. 이 목록에는 `externalOpportunityId`, `leadId` 및 `role`의 복합 키가 포함되어 있습니다.

`fields` 응답 매개 변수는 각 필드에 대해 다음 정보를 제공합니다.

- 이름.
- Marketo UI에 표시된 `displayName`.
- 데이터 유형.
- 필드를 만든 후 업데이트할 수 있는지 여부입니다.
- 해당하는 경우 필드 길이.

## 쿼리

리드 데이터베이스 개체는 한 필드를 참조하는 간단한 키에 대한 기본 쿼리 패턴을 공유합니다.

```http
GET /rest/v1/{type}.json?filterType={field to query}&filterValues={comma-separated list of possible values}
```

리드를 제외한 모든 개체에 대해 해당 설명 응답의 `searchableFields`에서 `{field to query}`을(를) 선택하십시오. 최대 300개의 값을 쉼표로 구분한 목록을 제공합니다.

다음과 같은 선택적 쿼리 매개 변수를 포함할 수도 있습니다.

- `batchSize`: 반환할 결과 수를 지정하는 정수입니다. 기본값과 최대값은 300입니다.
- `nextPageToken`: 페이징에 대한 이전 호출에서 반환된 토큰입니다. 자세한 내용은 [페이징 토큰](paging-tokens.md)을 참조하십시오.
- `fields`: 각 레코드에 대해 반환할 필드 이름을 쉼표로 구분한 목록입니다. 유효한 필드에 대해서는 해당 설명을 참조하십시오. 반환되지 않는 필드를 요청하면 해당 값은 null로 간주됩니다.
- `_method`: POST HTTP 메서드를 사용하여 쿼리를 제출합니다. 사용법은 _method=GET 섹션을 참조하십시오.

다음 예제는 영업 기회를 쿼리합니다.

```http
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

이 호출의 `filterType`은(는) &quot;marketoGUID&quot;가 아닌 &quot;idField&quot;입니다. &quot;idField&quot;와 &quot;dedupeFields&quot;는 모두 해당 필드에 별칭을 사용할 수 있는 특별한 경우입니다. 호출은 &quot;marketoGUID&quot;를 명시적으로 설정하지 않지만 조회 필드로 유지됩니다.

개체 설명의 `idField` 및 `dedupeFields`(으)로 식별되는 필드 또는 필드 집합은 쿼리에 항상 유효한 `filterTypes`입니다. 이 호출은 filterValues의 GUID와 일치하는 레코드를 반환합니다. 일치하는 레코드가 없으면 응답은 성공을 나타내고 빈 결과 배열을 반환합니다.

일치하는 레코드 집합이 300개를 초과하거나 지정된 `batchSize` 중 더 작은 레코드 집합일 경우 응답에는 값이 true인 `moreResult`과(와) `nextPageToken`이(가) 포함됩니다. 더 많은 레코드를 검색하기 위해 후속 호출에 토큰을 포함하십시오. 자세한 내용은 [페이징 토큰](paging-tokens.md)을 참조하십시오.

### 긴 URI

URI는 GUID로 쿼리할 때와 같이 REST 서비스의 8KB 제한을 초과할 수 있습니다. 이 경우 GET 대신 HTTP POST 메서드를 사용하고 `_method=GET` 쿼리 매개 변수를 추가합니다.

POST 본문의 나머지 쿼리 매개 변수를 &quot;application/x-www-form-urlencoded&quot; 문자열로 전달합니다. 연결된 Content-type 헤더도 전달합니다.

```http
POST /rest/v1/opportunities.json?_method=GET
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fa&dff23271-f996-47d7-984f-f2676861b5fc,dff23271-f996-47d7-984f-f2676861b5fb,544fb7f5-2ddf-4fca-ae32-7e6ef1415e9f,f1ba41a2-69d1-4a35-9807-0e159d66f2c9,f7521272-3331-4a89-a768-222baff2f894
```

복합 키를 쿼리할 때도 `_method=GET` 매개 변수가 필요합니다.

### 복합 키

조합 키를 쿼리하려면 JSON 본문과 함께 POST 요청을 제출합니다. `filterType`이(가) 여러 필드가 있는 `dedupeFields` 옵션인 경우에만 이 패턴을 사용하십시오.

복합 키는 현재 Opportunity Roles 및 일부 사용자 지정 객체에서만 사용됩니다. 다음 예제에서는 `dedupeFields`의 복합 키를 사용하여 Opportunity 역할을 쿼리합니다.

```http
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

JSON 개체는 `filterValues`을(를) 제외한 단순 키 쿼리에 사용되는 모든 쿼리 매개 변수를 허용합니다. `filterValues` 대신 JSON 개체의 &quot;입력&quot; 배열을 제공하세요. 각 개체에는 복합 키의 모든 필드가 포함되어야 합니다. 이 예제에서는 필드가 `externalOpportunityId`, `leadId` 및 `role`입니다.

요청은 제공된 입력에 대해 `roles`을(를) 쿼리하고 일치하는 결과를 반환합니다. 응답에 `moreResult=true` 및 `nextPageToken`이(가) 포함된 경우 모든 원본 입력 및 `nextPageToken`을(를) 다음 요청에 포함하십시오.

## 만들기 및 업데이트

JSON 본문이 있는 POST 요청을 전송하여 리드 데이터베이스 레코드를 만들고 업데이트합니다. Opportunity, Roles, Custom Object, Company 및 SalesPersons 는 동일한 인터페이스를 사용합니다. 리드는 리드 설명서에 설명된 다른 인터페이스를 사용합니다.

필요한 유일한 매개 변수는 최대 300개의 개체 배열인 `input`입니다. 각 개체에는 삽입하거나 업데이트할 필드가 있습니다.

다음과 같은 선택적 매개 변수를 포함할 수도 있습니다.

- `action`: `createOnly`, `updateOnly` 또는 `createOrUpdate` 허용 생략하면 모드는 기본적으로 `createOrUpdate`(으)로 설정됩니다.
- `dedupeBy`: 작업이 createOnly 또는 `createOrUpdate` 중 하나로 설정된 경우 `idField` 또는 `dedupeFields`을(를) 허용합니다. 생략하면 모드는 기본적으로 `dedupeFields`(으)로 설정됩니다.

`dedupeBy`이(가) `idField`인 경우 설명에 나열된 `idField`은(는) 중복 제거에 사용되며 각 레코드에 포함되어야 합니다. `idField` 모드가 `createOnly` 모드와 호환되지 않습니다.

`dedupeBy`이(가) `dedupeFields`인 경우 모든 레코드에 개체 설명에 나열된 각 `dedupeFields` 필드를 포함하십시오.

필드 값을 전달하면 데이터베이스에서 값 `null` 또는 빈 문자열을 `null`(으)로 씁니다.

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

리드 API를 제외하고 만들기 및 업데이트 호출은 `result` 배열의 각 개체에서 `seq` 필드를 반환합니다. 이 숫자는 요청에서 업데이트된 레코드의 위치에 해당합니다.

각 결과는 또한 개체 유형의 `idField` 값과 `status`의 &quot;created&quot;, &quot;updated&quot; 또는 &quot;skipped&quot;를 반환합니다. 상태를 건너뛸 경우 결과에 &quot;reasons&quot; 배열이 포함됩니다. 각 이유 개체에는 레코드를 건너뛴 이유를 설명하는 코드와 메시지가 포함됩니다. 자세한 내용은 [오류 코드](error-codes.md)를 참조하세요.

### 삭제

가망 고객을 제외한 가망 고객 데이터베이스 객체는 표준 삭제 인터페이스를 사용합니다. 입력 외에 idField 또는 dedupeFields를 허용하는 `deleteBy,` 매개 변수만 필요합니다.

다음 예제에서는 사용자 지정 개체를 삭제합니다.

```http
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

응답에는 `seq`, `status` 및 `marketoGUID`이(가) 포함됩니다. 건너뛴 레코드의 경우 `reasons`도 포함됩니다.

특정 객체 유형에 대한 CRUD 작업에 대한 자세한 내용은 해당 객체에 대한 설명서를 참조하십시오.
