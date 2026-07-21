---
title: 영업 기회 역할
feature: REST API
description: 설명, 복합 중복 제거 필드가 있는 쿼리, 업데이트 삭제 만들기, 시간 초과, CRM 동기화 안 함 등 REST API를 통해 Marketo 기회 역할을 관리합니다.
exl-id: 2ba84f4d-82d0-4368-94e8-1fc6d17b69ed
TQID: https://experienceleague.adobe.com/aE27mBhsrn-0SO41M-pV5NFjoMq--1Lp-L2TQGL7-8Y
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 254
ht-degree: 0%

---

# 영업 기회 역할

[영업 기회 역할 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities/operation/getOpportunityRolesUsingGET)

중간 `opportunityRole` 개체 링크가 기회로 연결됩니다.

영업 기회 역할 API는 기본 CRM 동기화가 활성화되지 않은 구독에만 사용할 수 있습니다.

## 설명

기회와 마찬가지로 API는 기회 역할에 대해 설명 호출 및 CRUD 작업을 제공합니다.

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

## 쿼리

`dedupeFields` 및 `searchableFields` 값이 기회와 다릅니다. `dedupeFields`에서 `externalOpportunityId`, `leadId` 및 `role`이(가) 필요한 복합 키를 제공합니다. 레코드를 성공적으로 만들려면 ID 필드에서 참조한 영업 기회와 잠재 고객이 대상 인스턴스에 있어야 합니다.

`searchableFields` 값 `marketoGUID`, `leadId` 및 `externalOpportunityId`은(는) Opportunities와 동일한 패턴을 사용하는 개별 쿼리에 유효합니다. 복합 키를 사용하여 쿼리할 수도 있습니다. 이 쿼리에는 `_method=GET` 쿼리 매개 변수와 함께 POST를 통해 제출된 JSON 개체가 필요합니다.

```http
POST /rest/v1/opportunities/roles.json?_method=GET
```

```json
{
   "filterType": "dedupeFields",
   "fields": [
      "marketoGuid",
      "externalOpportunityId",
      "leadId",
      "role"
   ],
   "input": [
      {
        "externalOpportunityId": "Opportunity1",
        "leadId": 1,
        "role": "Captain"
      },
      {
        "externalOpportunityId": "Opportunity2",
        "leadId": 1872,
        "role": "Commander"
      },
      {
        "externalOpportunityId": "Opportunity3",
        "leadId": 273891,
        "role": "Lieutenant Commander"
      }
   ]
}
```

이 요청은 표준 GET 쿼리와 동일한 응답 유형을 생성하지만 다른 요청 인터페이스를 사용합니다.

## 만들기 및 업데이트

기회와 동일한 인터페이스를 사용하여 기회 역할을 만들고 업데이트합니다.

```http
POST /rest/v1/opportunities/roles.json
```

```json
{
   "action": "createOrUpdate",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "externalOpportunityId": "19UYA31581L000000",
         "leadId": 456783,
         "role": "Technical Buyer",
         "isPrimary": false
      },
      {
         "externalOpportunityId": "19UYA31581L000000",
         "leadId": 456784,
         "role": "Technical Buyer",
         "isPrimary": false
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result":[
      {
         "seq": 0,
         "status": "updated",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq": 1,
         "status": "created",
         "marketoGUID": "cff23271-f996-47d7-984f-f2676861b5fb"
      }
   ]
}
```

## 삭제

데이터 중복 제거 필드 또는 ID 필드로 영업 기회 역할을 삭제합니다. deleteBy 매개 변수를 dedupeFields 또는 idField로 설정합니다. 기본값은 dedupeFields 입니다.

요청 본문에는 삭제할 영업 기회 역할의 입력 배열이 포함되어 있습니다. 각 호출에는 최대 300개의 영업 기회 역할이 허용됩니다.

```http
POST /rest/v1/opportunities/roles/delete.json
```

```json
{
   "deleteBy": "dedupeFields",
   "input": [
      {
        "externalOpportunityId": "19UYA31581L000000",
        "leadId": 456783,
        "role": "Technical Buyer"
      }
   ]
}
```

```json
{
    "requestId": "10f7c#173264db42d",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
            "status": "deleted"
        }
    ]
    "success": true
}
```

## 시간 초과

- Opportunity Role 엔드포인트는 별도로 명시하지 않는 한 30초의 시간 제한을 갖습니다.
- 동기화 영업 기회 역할의 시간 제한은 60초입니다.
- Delete Opportunity 역할의 시간 제한은 60초입니다.
