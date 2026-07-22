---
title: 채널
feature: REST API
description: Asset REST API를 통해 Marketo 채널을 쿼리하고, 페이지 매김 또는 이름별로 가져오기로 탐색하고, 진행 상태를 보고, 프로그램 유형 규칙을 이해하는 방법에 대해 알아봅니다.
exl-id: ec6c279f-a7b4-4a7c-b980-1a68045f37ce
TQID: https://experienceleague.adobe.com/e9TnbxgJCT5X2r5MjTdC49uVz4wvxDy2jhdQP5JOFTI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 117
ht-degree: 3%

---

# 채널

[채널 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels)

채널은 모든 프로그램 유형에 필요한 필드입니다. 채널은 지정된 `applicableProgramType`(으)로만 사용할 수 있습니다. 또한 채널은 프로그램 구성원이 사용할 수 있는 프로그램 상태를 정의합니다.

프로그램을 만든 후 채널의 상태를 변경하면 프로그램은 향후 상태 변경을 위해 업데이트된 목록을 사용합니다. 기존 프로그램 멤버십 레코드는 현재 상태를 유지합니다.

## 쿼리

채널을 표준 자산으로 쿼리합니다. API는 ID로 채널을 검색하기 위한 끝점을 제공하지 않습니다.

### 찾아보기

```http
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

```http
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
