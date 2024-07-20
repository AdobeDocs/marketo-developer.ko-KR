---
title: 영업 기회 역할
feature: REST API
description: Marketo에서 영업 기회 역할 처리.
exl-id: 2ba84f4d-82d0-4368-94e8-1fc6d17b69ed
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 영업 기회 역할

[영업 기회 역할 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities/operation/getOpportunityRolesUsingGET)

리드는 중간 `opportunityRole` 개체를 통해 기회에 연결됩니다.

영업 기회 역할 API는 기본 CRM 동기화가 활성화되지 않은 구독에만 노출됩니다.

## 설명

기회와 마찬가지로 설명 호출 및 CRUD 작업은 기회 역할에 노출됩니다.

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

## 쿼리

`dedupeFields`과(와) `searchableFields`이(가) 모두 기회와 약간 다릅니다. `dedupeFields`은(는) 실제로 복합 키를 제공하므로 `externalOpportunityId`, `leadId` 및 `role`의 세 가지 키가 모두 필요합니다. 레코드 만들기에 성공하려면 ID 필드를 통한 영업 기회와 잠재 고객 링크가 모두 대상 인스턴스에 있어야 합니다. `searchableFields`의 경우 `marketoGUID`, `leadId` 및 `externalOpportunityId`은(는) 모두 자체 쿼리에 유효하며 Opportunities와 동일한 패턴을 사용하지만 쿼리에 복합 키를 사용하는 추가 옵션이 있습니다. 이 경우 추가 쿼리 매개 변수 `_method=GET`을(를) 사용하여 POST을 통해 JSON 개체를 제출해야 합니다.

```
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

이렇게 하면 표준 GET 쿼리와 동일한 유형의 응답이 생성되며, 단순히 요청을 수행하기 위한 다른 인터페이스가 있습니다.

## 만들기 및 업데이트

Opportunity 역할에는 Opportunity 로 레코드를 만들고 업데이트하는 동일한 인터페이스가 있습니다.

```
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

데이터 중복 제거 필드 또는 ID 필드를 통해 영업 기회 역할을 삭제할 수 있습니다. dedupeFields 또는 idField 값이 있는 deleteBy 매개 변수를 사용하여 지정합니다. 지정하지 않으면 기본값은 dedupeFields입니다. 요청 본문에는 삭제할 영업 기회 역할의 입력 배열이 포함되어 있습니다. 호출당 최대 300개의 영업 기회 역할이 허용됩니다.

```
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

- 아래에 명시되지 않은 경우 Opportunity Role Endpoints 의 시간 제한은 30초입니다.
   - 동기화 영업 기회 역할: 60초 
   - 영업 기회 역할 삭제: 60초
