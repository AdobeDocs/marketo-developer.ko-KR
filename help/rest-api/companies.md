---
title: 회사
feature: REST API
description: Marketo 회사 REST API를 사용하여 회사 레코드를 설명, 쿼리 및 동기화하고, externalCompanyId로 필드 및 중복 제거를 관리하고, 읽기 전용 CRM 동기화를 메모합니다.
exl-id: 80e514a2-1c86-46a7-82bc-e4db702189b0
TQID: https://experienceleague.adobe.com/LdJYN4lx9JfcE-02zTz8ktfYXm4EdPtxMYOx9gGR0sg
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 582
ht-degree: 1%

---

# 회사

[회사 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies)

회사는 잠재 고객 레코드가 속한 조직을 나타냅니다. 회사에 리드를 추가하려면 [리드 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST) 또는 [리드 일괄 가져오기](bulk-lead-import.md) 끝점을 사용하여 해당 `externalCompanyId` 필드를 채웁니다.

리드를 다른 회사에 추가하지 않으면 회사에서 리드를 제거할 수 없습니다. 회사 레코드에 연결된 리드는 해당 레코드에서 값이 리드 레코드에 있는 것처럼 값을 상속합니다.

회사 API는 [SFDC 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en)가 활성화된 구독에 대해 읽기 전용 액세스를 제공합니다.

## 설명

회사 레코드와 상호 작용하는 데 필요한 정보를 검색할 회사 개체를 설명합니다.

```http
GET /rest/v1/companies/describe.json
```

```json
{
   "success":true,
   "requestId":"5847#14d44113ad7",
   "result":[
      {
         "name":"Company",
         "description":"Company object",
         "createdAt":"2015-05-11T17:11:32Z",
         "updatedAt":"2015-05-11T17:11:32Z",
         "idField":"id",
         "dedupeFields":[
            "externalCompanyId"
         ],
         "searchableFields":[
            [
               "externalCompanyId"
            ],
            [
               "id"
            ],
            [
               "company"
            ]
         ],
         "fields":[
            {
               "name":"createdAt",
               "displayName":"Created At",
               "dataType":"datetime",
               "updateable":false
            },
            {
               "name":"externalCompanyId",
               "displayName":"External Company Id",
               "dataType":"string",
               "length":100,
               "updateable":false
            },
            {
               "name":"id",
               "displayName":"Id",
               "dataType":"integer",
               "updateable":false
            },
            {
               "name":"updatedAt",
               "displayName":"Updated At",
               "dataType":"datetime",
               "updateable":false
            },
            {
               "name":"annualRevenue",
               "displayName":"Annual Revenue",
               "dataType":"currency",
               "updateable":true
            }
            {
               "name":"company",
               "displayName":"Company Name",
               "dataType":"string",
               "length":255,
               "updateable":true
            }
         ]
      }
   ]
}
```

## 쿼리

[회사에 쿼리](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompaniesUsingGET)하는 패턴은 리드 API를 거의 따릅니다. 그러나 `filterType` 매개 변수는 회사 설명 응답 또는 dedupeFields의 searchableFields 배열에 나열된 필드만 허용합니다.

쿼리 매개 변수는 다음과 같습니다.

- `filterType` 및 `filterValues`: 필수 매개 변수입니다.
- `fields`, `nextPageToken` 및 `batchSize`: Leads 및 Opportunities API의 해당 매개 변수와 같은 기능을 하는 선택적 매개 변수입니다.

`fields` 목록을 요청할 때 반환되지 않은 요청된 필드에 null의 묵시적 값이 있습니다.

필드 매개 변수를 생략하면 기본적으로 다음 필드가 반환됩니다.

- ID
- 데이터 중복 제거 필드
- updatedAt
- createdAt

```http
GET /rest/v1/companies.json?filterType=id&filterValues=3433,5345
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "id":3433,
         "externalCompanyId":"19UYA31581L000000",
         "company":"Google"
      },
      {
         "seq":1,
         "id":5345,
         "externalCompanyId":"29UYA31581L000000",
         "company":"Yahoo"
      }
   ]
}
```

## 만들기 및 업데이트

[회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/syncCompaniesUsingPOST) 끝점은 회사 개체 배열을 포함하는 필수 `input` 매개 변수를 허용합니다.

끝점은 기회와 마찬가지로 createOnly, updateOnly 및 createOrUpdate의 세 가지 만들기 및 업데이트 모드를 지원합니다. 요청의 `action` 매개 변수에 모드를 지정하십시오.

`dedupeBy` 및 `action` 매개 변수는 선택 사항입니다. 각각 dedupeFields 및 createOrUpdate로 기본 설정됩니다.

```http
POST /rest/v1/companies.json
```

```text
Content-Type: application/json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalCompanyId":"19UYA31581L000000",
         "company":"Google"
      },
      {
         "externalCompanyId":"29UYA31581L000000",
         "company":"Yahoo"
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
         "id":1232
      },
      {
         "seq":1,
         "status":"created",
         "id":1323
      }
   ]
}
```

### 필드

회사 개체에는 표시 이름, API 이름 및 dataType과 같은 특성으로 정의된 필드가 포함되어 있습니다. 이러한 특성을 함께 메타데이터라고 합니다.

다음 엔드포인트는 회사 개체의 쿼리 필드를 나타냅니다. API 사용자에게는 `Read-Write Schema Standard Field` 권한, `Read-Write Schema Custom Field` 권한 또는 둘 다 있는 역할이 있어야 합니다.

### 쿼리 필드

API 이름으로 한 회사 필드를 쿼리하거나 모든 회사 필드를 검색합니다.

#### 이름별

[이름별 회사 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompanyFieldByNameUsingGET) 끝점은 회사 개체에서 한 필드에 대한 메타데이터를 검색합니다. 필수 `fieldApiName` 경로 매개 변수는 필드의 API 이름을 지정합니다.

응답은 회사 설명 응답과 유사하지만 추가 메타데이터를 포함합니다. 예를 들어 `isCustom` 특성은 필드가 사용자 지정인지 여부를 나타냅니다.

```http
GET /rest/v1/companies/schema/fields/industry.json
```

```json
{
    "requestId": "88f6#17e976d6ab4",
    "result": [
        {
            "displayName": "Industry",
            "name": "industry",
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
    "success": true
}
```

#### 찾아보기

[회사 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/getCompanyFieldsUsingGET) 끝점은 회사 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드를 반환합니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

`moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. `moreResult`이(가) false가 될 때까지 반환된 `nextPageToken`을(를) 사용하여 끝점을 계속 호출합니다.

```http
GET /rest/v1/companies/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "b50e#17e995c2d35",
    "result": [
        {
            "displayName": "Company Name",
            "name": "company",
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
            "displayName": "Site",
            "name": "site",
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
            "displayName": "Website",
            "name": "website",
            "description": null,
            "dataType": "url",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Main Phone",
            "name": "mainPhone",
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
            "displayName": "Annual Revenue",
            "name": "annualRevenue",
            "description": null,
            "dataType": "currency",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "L7XD3EFJ3OLFZKXKJBWYULOTRA======",
    "moreResult": true
}
```

### 삭제

`input` 배열의 검색 값 목록으로 삭제 조건을 지정하십시오. `deleteBy` 매개 변수에서 삭제 메서드를 지정하십시오.

허용되는 값은 dedupeFields 및 idField입니다. 기본값은 dedupeFields 입니다.

```text
Content-Type: application/json
```

```http
POST /rest/v1/companies/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "externalCompanyId":"19UYA31581L000000"
      },
      {
         "externalCompanyId":"29UYA31581L000000"
      },
      {
         "externalCompanyId":"39UYA31581L000000"
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
         "id":1234,
         "status":"deleted"
      },
      {
         "seq":1,
         "id":56456,
         "status":"deleted"
      },
      {
         "seq":2,
         "status":"skipped",
         "reasons":[
            {
               "code":"1013",
               "message":"Record not found"
            }
         ]
      }
   ]
}
```

## 시간 초과

- 회사 엔드포인트에는 특별한 언급이 없는 한 30초의 시간 제한이 있습니다.
- 동기화 회사의 시간 제한은 60초입니다.
- 회사 삭제의 시간 제한은 60초입니다.
