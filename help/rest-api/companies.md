---
title: 회사
feature: REST API
description: Marketo 회사 REST API를 사용하여 회사 레코드를 설명, 쿼리 및 동기화하고, externalCompanyId로 필드 및 중복 제거를 관리하고, 읽기 전용 CRM 동기화를 메모합니다.
exl-id: 80e514a2-1c86-46a7-82bc-e4db702189b0
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# 회사

[회사 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)

회사는 잠재 고객 레코드가 속한 조직을 나타냅니다. 리드는 `externalCompanyId`리드 동기화[ 또는 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST)리드 일괄 가져오기[ 끝점을 사용하여 해당 ](bulk-lead-import.md) 필드를 채워 회사에 추가됩니다. 리드가 회사에 추가되면 해당 회사에서 리드를 삭제할 수 없습니다(다른 회사에 리드를 추가하지 않은 경우). 회사 레코드에 연결된 잠재 고객은 잠재 고객의 자체 레코드에 있는 것처럼 회사 레코드에서 값을 직접 상속합니다.

회사 API는 [SFDC 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync.html?lang=en) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync.html?lang=en)가 활성화된 구독에 대한 읽기 전용 액세스입니다.

## 설명

회사 개체를 설명하면 상호 작용해야 하는 모든 정보를 제공합니다.

```
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

[ 매개 변수가 회사 설명 호출의 searchableFields 배열 또는 dedupeFields에 나열된 필드를 수락한다는 추가적인 제한을 사용하여 ](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompaniesUsingGET)회사에 문의`filterType`하는 패턴은 리드 API의 패턴을 따릅니다.

`filterType` 및 `filterValues`은(는) 필수 쿼리 매개 변수입니다.  `fields`, `nextPageToken` 및 `batchSize`은(는) 선택적 매개 변수입니다.  매개 변수는 Leads 및 Opportunities API의 해당 매개 변수와 동일하게 작동합니다. `fields` 목록을 요청할 때 특정 필드가 요청되었지만 반환되지 않은 경우 값이 null인 것으로 간주됩니다.

필드 매개 변수를 생략하면 반환되는 기본 필드 집합은 다음과 같습니다.

- ID
- 데이터 중복 제거 필드
- updatedAt
- createdAt

```
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

[회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) 끝점은 회사 개체 배열을 포함하는 필수 `input` 매개 변수를 허용합니다. 기회와 마찬가지로 회사를 만들고 업데이트하는 모드에는 createOnly, updateOnly 및 createOrUpdate의 세 가지가 있습니다.  요청의 `action` 매개 변수에 모드가 지정되었습니다. `dedupeBy` 및 `action` 매개 변수는 모두 선택 사항이며 각각 dedupeFields 및 createOrUpdate 모드로 기본 설정됩니다.

```
POST /rest/v1/companies.json
```

```
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

회사 개체에는 필드 집합이 포함되어 있습니다. 각 필드 정의는 필드를 설명하는 속성 세트로 구성됩니다. 속성의 예로는 디스플레이 이름, API 이름 및 dataType이 있습니다. 이러한 속성을 통칭하여 메타데이터라고 합니다.

다음 엔드포인트를 사용하면 회사 개체의 필드를 쿼리할 수 있습니다. 이러한 API를 사용하려면 소유 API 사용자에게 `Read-Write Schema Standard Field` 또는 `Read-Write Schema Custom Field` 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

### 쿼리 필드

회사 필드를 쿼리하는 것은 간단합니다. API 이름으로 단일 회사 필드를 쿼리하거나 모든 회사 필드 집합을 쿼리할 수 있습니다.

#### 이름별

[이름별 회사 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldByNameUsingGET) 끝점은 회사 개체에서 단일 필드에 대한 메타데이터를 검색합니다. 필수 `fieldApiName` 경로 매개 변수는 필드의 API 이름을 지정합니다. 응답은 회사 설명 끝점과 유사하지만 필드가 사용자 지정 필드인지 여부를 나타내는 `isCustom` 특성과 같은 추가 메타데이터를 포함합니다.

```
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

[회사 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/getCompanyFieldsUsingGET) 끝점은 회사 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드가 반환됩니다. `batchSize` 쿼리 매개 변수를 사용하여 이 수를 줄일 수 있습니다. `moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. moreResult 특성이 false를 반환할 때까지 이 끝점을 계속 호출합니다. 즉, 사용 가능한 결과가 없습니다. 이 API에서 반환된 `nextPageToken`은(는) 항상 이 호출의 다음 반복에 재사용해야 합니다.

```
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

삭제 기준은 검색 값 목록을 포함하는 `input` 배열에 지정됩니다.  `deleteBy` 매개 변수에 삭제 메서드가 지정되었습니다.  허용되는 값은 dedupeFields, idField입니다.  기본값은 dedupeFields 입니다.

```
Content-Type: application/json
```

```
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

- 회사 엔드포인트는 아래에 명시하지 않은 경우 30초입니다
   - 회사 동기화: 60초
   - 회사 삭제: 60초
