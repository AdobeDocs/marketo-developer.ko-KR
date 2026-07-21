---
title: 목록 멤버십(정적 목록)
feature: REST API, Static Lists
description: Marketo 리드 데이터베이스 REST API를 사용하여 정적 목록에 리드를 추가하고, 리드를 제거하고, 목록 구성원을 검색하고, 목록 구성원을 확인합니다.
exl-id: b8f74bcf-834a-44db-81fd-621048afeba4
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# 목록 멤버십(정적 목록)

[목록 멤버십 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists)

목록 멤버십 API는 정적 목록 멤버를 관리하기 위한 리드 데이터베이스 엔드포인트를 제공합니다. 이 엔드포인트를 사용하여 다음을 수행합니다.

- 리드를 목록에 추가합니다.
- 목록에서 리드를 제거합니다.
- 목록의 구성원을 검색합니다.
- 잠재 고객이 목록의 구성원인지 여부를 확인합니다.

## 엔드포인트

| 엔드포인트 | 메서드 | 경로 |
| --- | --- | --- |
| 목록에 추가 | POST | `/rest/v1/lists/{listId}/leads.json` |
| 목록에서 제거 | DELETE | `/rest/v1/lists/{listId}/leads.json` |
| 목록 ID로 리드 가져오기 | GET | `/rest/v1/lists/{listId}/leads.json` |
| 목록 멤버 | GET | `/rest/v1/lists/{listId}/leads/ismember.json` |

## 목록에 추가

[목록에 추가](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/addLeadsToListUsingPOST) 끝점을 사용하여 하나 이상의 구성원을 목록에 추가하십시오. 필수 `listId` 경로 매개 변수와 리드 ID가 포함된 하나 이상의 `id` 쿼리 매개 변수를 전달합니다. 최대 리드 ID 수는 300개입니다.

응답에는 요청에 있는 각 잠재 고객 ID의 상태로 `result` 배열이 포함되어 있습니다.

```http
POST /rest/v1/lists/{listId}/leads.json?id=318594&id=318595
```

```json
{
    "requestId": "6860#1706170ba29",
    "result": [
        {
            "id": 318594,
            "status": "added"
        },
        {
            "id": 318595,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

## 목록에서 제거

[목록에서 제거](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) 끝점을 사용하여 목록에서 하나 이상의 구성원을 제거합니다. 필수 `listId` 경로 매개 변수와 리드 ID가 포함된 하나 이상의 `id` 쿼리 매개 변수를 전달합니다. 최대 리드 ID 수는 300개입니다.

응답에는 요청에 있는 각 잠재 고객 ID의 상태로 `result` 배열이 포함되어 있습니다.

```http
DELETE /rest/v1/lists/{listId}/leads.json?id=318603&id=318595&id=999999
```

```json
{
    "requestId": "9e79#17061689ac3",
    "result": [
        {
            "id": 318603,
            "status": "removed"
        },
        {
            "id": 318595,
            "status": "removed"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

## 목록 ID로 리드 가져오기

[목록 ID로 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/getLeadsByListIdUsingGET) 끝점을 사용하여 목록의 구성원을 검색합니다. 필요한 `listId` 경로 매개 변수를 전달합니다. 선택적 쿼리 매개 변수를 전달하여 필터링 기준을 지정할 수도 있습니다.

선택적 쿼리 매개 변수는 다음과 같습니다.

- `batchSize`: 한 번의 호출로 반환할 잠재 고객 레코드 수를 지정합니다. 기본값과 최대값은 300입니다.
- `nextPageToken`: 큰 결과 집합을 통해 페이지를 매깁니다. 첫 번째 호출에서 이 매개 변수를 생략하고 후속 호출에 포함하십시오.
- `fields`: 반환할 필드 이름의 쉼표로 구분된 목록을 지정합니다. 이 매개 변수를 생략하면 응답에는 `email`, `updatedAt`, `createdAt`, `lastName`, `firstName` 및 `id`이(가) 포함됩니다.

요청에 지정된 리드 필드가 있는 `result` 배열이 응답에 포함되어 있습니다.

```http
GET /rest/v1/lists/{listId}/leads.json?batchSize=3
```

```json
{
    "requestId": "ddae#170615ba0cc",
    "result": [
        {
            "id": 318594,
            "firstName": "Hanna",
            "lastName": "Crawford",
            "email": "208161Robert.L.Deacon@pookmail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318595,
            "firstName": "Bertha",
            "lastName": "Fulton",
            "email": "208160Tyrone.V.Dyer@trashymail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318596,
            "firstName": "Faith",
            "lastName": "England",
            "email": "208159Rex.M.Bailey@dodgit.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        }
    ],
    "success": true,
    "nextPageToken": "PS5VL5WD4UOWGOUCJR6VY7JQO24LC2U5DRBU4WO4RQMPHDHTK2T3BEZOR75VLQXYB3245WW2GMDSK==="
}
```

## 목록 멤버

[Member of List](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET) 끝점을 사용하여 하나 이상의 리드가 목록의 구성원인지 여부를 확인합니다. 필수 `listId` 경로 매개 변수와 리드 ID가 포함된 하나 이상의 `id` 쿼리 매개 변수를 전달합니다. 최대 리드 ID 수는 300개입니다.

응답에는 요청에 있는 각 잠재 고객 ID의 상태로 `result` 배열이 포함되어 있습니다.

```http
GET /rest/v1/lists/{listId}/leads/ismember.json?id=309901&id=318603&id=999999
```

```json
{
    "requestId": "693a#17061475cf9",
    "result": [
        {
            "id": 309901,
            "status": "memberof"
        },
        {
            "id": 318603,
            "status": "notmemberof"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```
