---
title: 정적 목록
feature: REST API, Static Lists
description: Marketo REST API를 사용하여 ID, 이름 및 찾아보기, 폴더 범위, 페이징 및 날짜 필터에 대한 끝점이 있는 정적 목록을 쿼리, 만들기, 업데이트 및 삭제합니다.
exl-id: 20679fd2-fae2-473e-84bc-cb4fdf2f5151
source-git-commit: 59684e1c5a8082ad12f1e4bfc854c0d2dde35d2a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# 정적 목록

[정적 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists)

Marketo은 정적 목록에서 CRUD 작업을 수행하기 위한 REST API 세트를 제공합니다. 이러한 API는 쿼리, 만들기, 업데이트 및 삭제 옵션을 제공하는 에셋 API에 대한 표준 인터페이스 패턴을 따릅니다.

목록 구성원의 잠재 고객 데이터베이스 작업에 대해서는 [목록 구성원](list-membership.md)을 참조하십시오.

## 쿼리

정적 목록을 쿼리하면 [ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)의 자산에 대한 표준 쿼리 형식을 따릅니다.

### ID별

[ID별 쿼리](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET)은(는) 단일 정적 목록 `id`을(를) 경로 매개 변수로 사용하고 단일 정적 목록 레코드를 반환합니다.

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

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET)은(는) 정적 목록 `name`을(를) 매개 변수로 사용하고 단일 정적 목록 레코드를 반환합니다. 인스턴스의 모든 정적 목록 이름에 대해 정확한 문자열 일치를 수행하고 해당 이름과 일치하는 정적 목록에 대한 결과를 반환합니다.

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

정적 목록은 [일괄적으로 검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListsUsingGET)할 수도 있습니다. `folder` 매개 변수는 쿼리가 수행될 상위 폴더를 지정하는 데 사용할 수 있으며 `id` 및 `type`을(를) 포함하는 JSON 개체로 서식이 지정됩니다. 다른 대량 자산 검색 끝점과 마찬가지로 `offset` 및 `maxReturn`은(는) 페이징에 사용할 수 있는 선택적 매개 변수입니다. `earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수를 사용하면 지정된 범위 내에서 만들어지거나 업데이트된 정적 목록을 반환하기 위해 낮음 및 높음 날짜/시간 워터마크를 설정할 수 있습니다. 날짜/시간 값은 유효한 ISO-8601 문자열이어야 하며 밀리초를 포함해서는 안 됩니다.

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

[정적 목록 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/createStaticListUsingPOST)는 두 개의 필수 매개 변수가 있는 `application/x-www-form-urlencoded` POST를 사용하여 실행됩니다. `folder` 매개 변수는 정적 목록을 만들 상위 폴더를 지정하는 데 사용되며 `id` 및 `type`을(를) 포함하는 JSON 개체로 서식이 지정됩니다. `name` 매개 변수는 정적 목록의 이름을 지정하는 데 사용되며 고유해야 합니다. 선택적으로 `description` 매개 변수를 사용하여 정적 목록을 설명할 수 있습니다.

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

[정적 목록 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/updateStaticListUsingPOST)는 두 개의 선택적 매개 변수를 사용하여 별도의 끝점을 통해 수행됩니다. `description` 매개 변수는 정적 목록 설명을 업데이트하는 데 사용할 수 있습니다. `name` 매개 변수는 정적 목록 이름을 업데이트하는 데 사용할 수 있으며 고유해야 합니다.

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

[정적 목록을 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST)하면 단일 정적 목록 `id`이(가) 경로 매개 변수로 사용됩니다. 가져오기 또는 내보내기 작업에서 사용 중이거나 다른 자산에서 사용 중인 정적 목록은 삭제할 수 없습니다.

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
