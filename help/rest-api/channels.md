---
title: 채널
feature: REST API
description: Asset REST API를 통해 Marketo 채널을 쿼리하고, 페이지 매김 또는 이름별로 가져오기로 탐색하고, 진행 상태를 보고, 프로그램 유형 규칙을 이해하는 방법에 대해 알아봅니다.
exl-id: ec6c279f-a7b4-4a7c-b980-1a68045f37ce
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 2%

---

# 채널

[채널 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Channels)

채널은 모든 프로그램 유형에 대한 표준 및 필수 필드입니다. 각 채널 유형은 지정된 `applicableProgramType`에서만 사용할 수 있으며 각 프로그램의 프로그램 구성원에 대해 유효한 사용 가능한 프로그램 상태 목록을 제공합니다. 프로그램을 만든 후 채널의 프로그램 상태가 변경되면 리드를 변경할 수 있는 프로그램 상태 목록이 해당 시점에 채널이 제공한 목록과 일치하지만 기존 프로그램 멤버십 레코드에 대한 프로그램 상태는 소급하여 변경되지 않습니다.

## 쿼리

채널은 표준 자산으로 쿼리할 수 있지만 ID로 채널을 검색할 끝점은 없습니다.

### 찾아보기

```
GET /rest/asset/v1/channels.json?offset=10
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "651#1504ebbbfcf",
    "result": [
        {
            "id": 3,
            "name": "Blog",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Visited Booth",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Influenced",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:57Z+0000",
            "updatedAt": "2015-07-15T11:40:57Z+0000"
        },
        {
            "id": 4,
            "name": "Online Advertising",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Registered",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "No Show",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Attended",
                    "step": 40,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:58Z+0000",
            "updatedAt": "2015-07-15T11:40:58Z+0000"
        }
    ]
}
```

### 이름별

```
GET /rest/asset/v1/channel/byName.json?name=Online Advertising
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "394c#1504eb476ed",
    "result": [
        {
            "id": 4,
            "name": "Online Advertising",
            "applicableProgramType": "program",
            "progressionStatuses": [
                {
                    "name": "Not in Program",
                    "step": 0,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Invited",
                    "step": 10,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Registered",
                    "step": 20,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "No Show",
                    "step": 30,
                    "description": null,
                    "hidden": false,
                    "success": false
                },
                {
                    "name": "Attended",
                    "step": 40,
                    "description": null,
                    "hidden": false,
                    "success": true
                }
            ],
            "createdAt": "2015-07-15T11:40:58Z+0000",
            "updatedAt": "2015-07-15T11:40:58Z+0000"
        }
    ]
}
```
