---
title: 정적 목록
feature: REST API, Static Lists
description: "정적 목록에서 CRUD 작업을 수행합니다."
source-git-commit: e8bb45a7b3bee71c3d0ab6117296a75c8959d72e
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# 정적 목록

[정적 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

[목록 멤버십 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)

Marketo은 정적 목록에서 CRUD 작업을 수행하기 위한 REST API 세트를 제공합니다. 이러한 API는 쿼리, 만들기, 업데이트 및 삭제 옵션을 제공하는 에셋 API에 대한 표준 인터페이스 패턴을 따릅니다.

## 쿼리

정적 목록 쿼리는 자산의 표준 쿼리 유형을 따릅니다. [id 기준](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET), [이름순](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET), 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET).

### ID별

[ID별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) 단일 정적 목록 사용 `id` 를 경로 매개 변수로 사용하고, 정적 목록 레코드를 하나만 반환합니다.

```
GET /rest/asset/v1/staticList/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "843c#1641f969e96",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### 이름별

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) 정적 목록을 가져옵니다. `name` 를 매개 변수로 반환하고, 단일 정적 목록 레코드를 반환합니다. 인스턴스의 모든 정적 목록 이름에 대해 정확한 문자열 일치를 수행하고 해당 이름과 일치하는 정적 목록에 대한 결과를 반환합니다.

```
GET /rest/asset/v1/staticList/byName.json?name=Foundation Seed List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "28ab#1641fa246b9",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### 찾아보기

정적 목록은 다음과 같을 수도 있습니다. [일괄로 검색됨](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET). 다음 `folder` 매개 변수를 사용하여 쿼리가 수행될 상위 폴더를 지정할 수 있으며, 이 폴더는 id 및 유형을 포함하는 JSON 개체로 포맷됩니다. 다른 일괄 에셋 검색 엔드포인트와 마찬가지로 `offset` 및 `maxReturn` 는 페이징에 사용할 수 있는 선택적 매개 변수입니다. 다음 `earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수를 사용하면 지정된 범위 내에서 작성되거나 업데이트된 정적 목록을 반환하기 위한 하한 및 상한 날짜/시간 워터마크를 설정할 수 있습니다. 날짜/시간 값은 유효한 ISO-8601 문자열이어야 하며 밀리초를 포함해서는 안 됩니다.

```
GET /rest/asset/v1/staticLists.json?folder={"id":13,"type":"Folder"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2dc0#1641f846633",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        },
        {
            "id": 1022,
            "name": "Blacklist Seed List",
            "createdAt": "2017-07-27T23:19:33Z+0000",
            "updatedAt": "2017-07-27T23:21:29Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1022A1"
        },
        {
            "id": 1023,
            "name": "Possible Duplicates Seed List",
            "createdAt": "2017-07-28T00:10:02Z+0000",
            "updatedAt": "2017-07-28T00:11:22Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1023A1"
        }
    ]
}
```

## 만들기 및 업데이트

[정적 목록 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/createStaticListUsingPOST) 는 두 개의 필수 매개 변수가 있는 application/x-www-form-urlencoded POST으로 실행됩니다. 다음 `folder` 매개 변수는 정적 목록을 만들 상위 폴더를 지정하는 데 사용되며 id 및 유형이 포함된 JSON 개체로 서식이 지정됩니다. 다음 `name` 매개 변수는 정적 목록의 이름을 지정하는 데 사용되며 고유해야 합니다. 필요한 경우 `description` 매개 변수는 정적 목록을 설명하는 데 사용할 수 있습니다.

```
POST /rest/asset/v1/staticLists.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
folder={"id":1034,"type":"Program"}&name=My Static List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1269d#164209d6e1e",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "createdAt": "2018-06-21T04:32:25Z+0000",
            "updatedAt": "2018-06-21T04:32:25Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

[정적 목록에 대한 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/updateStaticListUsingPOST) 는 두 개의 선택적 매개 변수로 별도의 끝점을 통해 수행됩니다. 다음 `description` 매개 변수는 정적 목록 설명을 업데이트하는 데 사용할 수 있습니다. 다음 `name` 매개 변수는 정적 목록 이름을 업데이트하는 데 사용할 수 있으며 고유해야 합니다.

```
POST /rest/asset/v1/staticList/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=This is a static list used for testing
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "f84f#16420b4c746",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "description": "This is a static list used for testing",
            "createdAt": "2018-06-21T04:32:26Z+0000",
            "updatedAt": "2018-06-21T04:57:55Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

### 삭제

[정적 목록 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST) 단일 정적 목록 사용 `id` 를 경로 매개 변수로 사용하십시오. 가져오기 또는 내보내기 작업에서 사용 중이거나 다른 자산에서 사용 중인 정적 목록은 삭제할 수 없습니다.

```
POST /rest/asset/v1/staticList/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2c79#16420ded0e9",
    "result": [
        {
            "id": 1027
        }
    ]
}
```

## 목록 멤버십

목록 멤버십 끝점은 정적 목록 멤버를 추가, 제거 및 쿼리하는 기능을 제공합니다. 또한 정적 목록 멤버십을 쿼리할 수 있습니다.

### 목록에 추가

다음 [목록에 추가](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/addLeadsToListUsingPOST) 끝점은 목록에 하나 이상의 구성원을 추가하는 데 사용됩니다. 끝점은 필수 항목입니다. `listId` 경로 매개 변수 및 리드 id가 포함된 하나 이상의 id 쿼리 매개 변수(최대 허용 수는 300임).

이 응답에는 `result` 요청에 지정된 각 잠재 고객 id에 대한 상태와 함께 JSON 개체로 구성된 배열입니다.

```
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

### 목록에서 제거

다음 [목록에서 제거](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) endpoint는 목록에서 하나 이상의 멤버를 제거하는 데 사용됩니다. 끝점은 필수 항목입니다. `listId` 경로 매개 변수 및 하나 이상 `id` 리드 id가 포함된 쿼리 매개 변수(최대 허용 수는 300임).

이 응답에는 `result` 요청에 지정된 각 잠재 고객 id에 대한 상태와 함께 JSON 개체로 구성된 배열입니다.

```
DELETE /rest/v1/lists/{listId}/leads.json?id=318603&id=318595&id=999999
```

```
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

### 쿼리 목록

다음 [목록 Id로 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET) endpoint는 목록의 멤버를 검색하는 데 사용됩니다. 끝점은 필수 항목입니다. `listId` 경로 매개 변수 및 여러 선택적 쿼리 매개 변수를 사용하여 필터링 기준을 지정할 수 있습니다.

다음 `batchSize` 매개 변수는 한 번의 호출로 반환할 잠재 고객 레코드 수를 지정하는 데 사용됩니다(기본값은 300이며, 최대값은 300임).

다음 `nextPageToken` 매개 변수는 큰 결과 세트의 페이지를 매기는 데 사용됩니다. 이 매개 변수는 첫 번째 호출에서는 전달되지 않고, 페이지 매김을 위한 후속 호출에서만 전달됩니다.

다음 `fields` 매개 변수에는 응답에서 반환될 필드 이름의 쉼표로 구분된 목록이 포함되어 있습니다. 필드 매개 변수가 이 요청에 포함되지 않으면 email, updatedAt, createdAt, lastName, firstName 및 id의 기본 필드가 반환됩니다.

이 응답에는 `result` 요청에 지정된 리드 필드가 포함된 JSON 개체로 구성된 배열입니다.

```
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

#### 잠재 고객 ID별 목록 멤버십 쿼리

다음 [목록 구성원](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET) 엔드포인트는 하나 이상의 리드가 목록의 멤버인지 확인하는 데 사용됩니다. 끝점은 필수 항목입니다. `listId` 경로 매개 변수 및 하나 이상 `id` 리드 id가 포함된 쿼리 매개 변수(최대 허용 수는 300임).

이 응답에는 `result` 요청에 지정된 각 잠재 고객 id에 대한 상태와 함께 JSON 개체로 구성된 배열입니다.

```
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
