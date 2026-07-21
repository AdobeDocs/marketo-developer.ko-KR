---
title: 영업 담당자
feature: REST API
description: externalSalesPersonId를 사용하여 리드에 연결하고 쿼리, 업데이트 및 삭제를 수행하는 SFDC 또는 Dynamics 동기화를 통해 영업 담당자 레코드에 대한 Marketo REST API 안내서입니다.
exl-id: f8ed5aa5-63c1-4c5b-8683-bf47eed1ea18
TQID: https://experienceleague.adobe.com/JwLNgM0zgztyoYJotCiSdGxMixnzA0kvkFbvq8kEkzE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 0%

---

# 영업 담당자

[영업 직원 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Sales-Persons)

영업 담당자 API는 [SFDC 동기화](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync)가 활성화된 구독에 대해 읽기 전용 액세스를 제공합니다.

영업 사원은 잠재 고객 레코드의 영업 사원을 나타내는 개인 레코드입니다. 각 잠재 고객 레코드의 externalSalesPersonId 필드는 영업 담당자와 관련이 있습니다. 이 필드가 채워지면 Marketo이 리드 레코드에서 해당 리드 소유자 조회 필드를 채웁니다. 그런 다음 관련 필터 및 토큰을 사용할 수 있습니다.

externalSalesPersonId 속성을 해당 끝점에 전달하여 영업 담당자를 다른 레코드와 연결합니다.

- 리드 레코드: [리드 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST).
- 영업 기회 레코드: [기회 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/syncOpportunitiesUsingPOST).
- 회사 레코드: [회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/syncCompaniesUsingPOST).

영업 사원 레코드는 API를 통해서만 편집할 수 있습니다.

## 설명

가망 고객 데이터베이스 객체에 대한 표준 패턴을 사용하여 영업사원 레코드를 설명합니다.

```http
GET /rest/v1/salespersons/describe.json
```

```json
{
   "requestId":"185d6#14b51985ff0",
   "success":true,
   "result":[
      {
         "name":"SalesPerson",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:24Z",
         "idField":"id",
         "dedupeFields":[
            "externalSalesPersonId"
         ],
         "searchableFields":[
            [
               "email"
            ],
            [
               "id"
            ],
            [
               "externalSalesPersonId"
            ]
         ],
         "fields":[
            {
               "name":"id",
               "displayName":"Marketo Id",
               "dataType":"integer",
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
               "name":"email",
               "displayName":"Email",
               "dataType":"string",
               "length":255,
               "updateable":false
            },
            {
               "name":"externalSalesPersonId",
               "displayName":"External Sales Person Id",
               "dataType":"string",
               "length":255,
               "updateable":false
            }
         ]
      }
   ]
}
```

기본적으로 영업 담당자 `idField`은(는) &quot;id&quot;이고 `dedupeFields`은(는) &quot;externalSalesPersonId&quot;입니다.

## 쿼리

단순 키에 대한 표준 쿼리 패턴을 사용하여 영업 개인을 쿼리합니다. 다음 예제에서는 사용자의 이메일을 externalSalesPersonId로 사용합니다.

기본적으로 이 쿼리는 일치하는 레코드에 대해 채워진 모든 필드를 반환합니다.

```http
GET /rest/v1/salespersons.json?filterType=dedupeFields&filterValues=david@test.com,sam@test.com
```

```json
 {
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "id":53453,
         "externalSalesPersonId":"sam@test.com",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:23Z"
      },
      {
         "seq":1,
         "id":53454,
         "externalSalesPersonId":"david@test.com",
         "createdAt":"2015-02-03T22:36:23Z",
         "updatedAt":"2015-02-03T22:36:23Z"
      }
   ]
}
```

## 만들기 및 업데이트

표준 갱신 패턴을 사용하여 영업 개인을 생성 또는 갱신합니다.

```http
POST /rest/v1/salespersons.json
```

```json
{
   "action":"createOrUpdate",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "externalSalesPersonId":"sam@test.com",
         "email":"sam@test.com",
         "firstName":"Sam",
         "lastName":"Sanosin"
      },
      {
         "externalSalesPersonId":"david@test.com",
         "email":"david@test.com",
         "firstName":"David",
         "lastName":"Aulassak"
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
         "id":45232
      },
      {
         "seq":1,
         "status": "created",
         "id":45236
      }
   ]
}
```

## 삭제

표준 삭제 패턴을 사용하여 영업 사원을 삭제합니다.

&quot;사용 중&quot;인 영업 사원은 삭제할 수 없습니다. 다음과 같은 경우 영업 담당자를 건너뜁니다.

- 영업 사원은 활성 잠재 고객과 연관됩니다.
- 영업 담당자는 삭제된 회사와 연결되어 있습니다.

```http
POST /rest/v1/salespersons/delete.json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "externalSalesPersonId":"sam@test.com"
      },
      {
         "externalSalesPersonId":"david@test.com"
      },
      {
         "externalSalesPersonId":"raj@test.com"
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
         "id":56343,
         "status": "deleted"
      },
      {
         "seq":1,
         "id":53453,
         "status": "deleted"
      },
      {
         "seq":2,
         "status": "skipped"
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

- Sales Person 엔드포인트에는 별다른 언급이 없는 한 시간 제한이 30초입니다.
- 동기화 영업 직원의 시간 제한은 60초입니다.
- Sales Persons 삭제 의 시간 제한은 60초입니다.
