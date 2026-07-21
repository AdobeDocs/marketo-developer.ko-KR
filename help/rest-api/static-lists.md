---
title: 정적 목록
feature: REST API, Static Lists
description: Marketo REST API를 사용하여 ID, 이름 및 찾아보기, 폴더 범위, 페이징 및 날짜 필터에 대한 끝점이 있는 정적 목록을 쿼리, 만들기, 업데이트 및 삭제합니다.
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
TQID: https://experienceleague.adobe.com/DSV9h6d4F3ZrIUT-VtqlmFAnpdxOuTf05ajCqiGegqk
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 1%

---

# 정적 목록

[정적 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists)

정적 목록 REST API를 사용하여 정적 목록을 쿼리, 만들기, 업데이트 및 삭제합니다.

목록 구성원의 잠재 고객 데이터베이스 작업에 대해서는 [목록 구성원](list-membership.md)을 참조하십시오.

## 쿼리

[ID별](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) 또는 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)별로 정적 목록을 쿼리합니다.

### ID별

[ID별 쿼리](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET)에서 하나의 정적 목록 `id` 경로 매개 변수를 사용하고 일치하는 레코드를 반환합니다.

```http
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

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET)에서 정적 목록 `name` 매개 변수를 사용합니다. 끝점은 정적 목록 이름에 대해 정확한 일치를 수행하고 일치하는 레코드를 반환합니다.

```http
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

찾아보기 끝점을 사용하여 [정적 목록을 일괄적으로 검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)하세요. 선택적 `folder` 매개 변수는 쿼리의 범위를 부모 폴더로 지정합니다. 폴더를 `id` 및 `type`이(가) 포함된 JSON 개체로 전달합니다.

페이지 매김에 `offset` 및 `maxReturn`을(를) 사용합니다. `earliestUpdatedAt` 및 `latestUpdatedAt`을(를) 낮음 및 높음 날짜-시간 경계로 사용합니다. 이러한 매개 변수는 범위 내에서 만들어지거나 업데이트된 목록을 반환합니다. 밀리초 없이 ISO-8601 값을 사용합니다.

```http
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

`application/x-www-form-urlencoded` POST 요청을 [정적 목록 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/createStaticListUsingPOST)에 보냅니다. `folder` 및 `name` 매개 변수가 필요합니다.

`id` 및 `type`이(가) 포함된 JSON 개체로 `folder`을(를) 전달합니다. `name`은(는) 고유해야 합니다. 선택적 `description` 매개 변수는 목록을 설명합니다.

```http
POST /rest/asset/v1/staticLists.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

업데이트 끝점을 사용하여 [정적 목록을 변경](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/updateStaticListUsingPOST)하세요. 선택적 `description` 매개 변수는 설명을 변경합니다. 선택적 `name` 매개 변수는 이름을 변경하며 고유해야 합니다.

```http
POST /rest/asset/v1/staticList/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

## 삭제

[정적 목록을 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST)하려면 `id`을(를) 경로 매개 변수로 전달하십시오. 가져오기, 내보내기 또는 다른 에셋에서 사용하는 목록은 삭제할 수 없습니다.

```http
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
