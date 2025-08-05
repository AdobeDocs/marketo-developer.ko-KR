---
title: 영업 담당자
feature: REST API
description: 영업 사원에 대한 데이터를 읽습니다.
exl-id: f8ed5aa5-63c1-4c5b-8683-bf47eed1ea18
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 영업 담당자

[영업 사용자 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Sales-Persons)

영업 담당자 API는 [SFDC 동기화](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync) 또는 [Microsoft Dynamics 동기화](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync)가 활성화된 구독에 대한 읽기 전용 액세스입니다. 영업 사원은 가망 고객 레코드의 영업 담당자인 개인 레코드의 유형입니다. 각 잠재 고객 레코드에서 externalSalesPersonId 필드를 통해 잠재 고객 레코드와 연결됩니다. 잠재 고객이 채워진 externalSalesPersonId 필드로 영업 사원과 연결된 경우 Marketo의 해당 잠재 고객 레코드에 대해 해당 잠재 고객 소유자 조회 필드가 채워져 해당 필터 및 토큰을 사용할 수 있습니다.

영업 직원은 [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) 끝점을 사용하고 externalSalesPersonId 특성을 전달하여 잠재 고객 레코드와 관련되어 있습니다.

영업 사원은 [영업 기회 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/syncOpportunitiesUsingPOST) 끝점을 사용하고 externalSalesPersonId 특성을 전달하여 영업 기회 레코드에 연결됩니다.

영업 직원은 [회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) 끝점을 사용하고 externalSalesPersonId 특성을 전달하여 회사 레코드와 관련되어 있습니다.

영업 사원 레코드는 API를 통해서만 편집할 수 있습니다.

## 설명

영업 사원 레코드 설명은 리드 데이터베이스 객체에 대한 표준 패턴을 따릅니다.

```
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

기본적으로 영업 직원의 `idField`은(는) &quot;id&quot;이고 `dedupeFields`은(는) &quot;externalSalesPersonId&quot;입니다.

## 쿼리

단순 키에 표준 쿼리 패턴을 사용하는 영업 사원. 이 예에서는 externalSalesPersonId로 사용되는 사용자 이메일을 보여 줍니다. 기본적으로 쿼리는 반환된 레코드에 대해 채워지는 모든 필드를 반환합니다.

```
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

업데이트에 대한 패턴은 표준입니다.

```
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

삭제 패턴은 표준입니다.

&quot;사용 중&quot;인 경우 영업 사원의 삭제가 허용되지 않습니다. 이 경우 영업 사원은 생략됩니다. 예:

- 영업 사원이 활성 가망 고객과 연관된 경우
- 영업 사원이 삭제된 회사와 연결된 경우

```
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

- 아래에 명시되지 않는 한 영업 담당자 엔드포인트는 30초입니다
   - 영업 담당자 동기화: 60대
   - 영업 직원 삭제: 60대
