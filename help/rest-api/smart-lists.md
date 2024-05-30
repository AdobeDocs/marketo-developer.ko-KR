---
title: "스마트 목록"
feature: REST API
description: "스마트 목록을 만들고 편집합니다."
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# 스마트 목록

[스마트 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists)

Marketo은 스마트 목록에서 작업을 수행하기 위한 일련의 REST API를 제공합니다. 이러한 API는 쿼리, 삭제 및 복제 옵션을 제공하는 에셋 API에 대한 표준 인터페이스 패턴을 따릅니다.

참고: 이러한 API는 사용자가 만든 스마트 목록에서만 지원됩니다. 다음 용도로는 사용할 수 없습니다. [기본 제공/시스템 스마트 목록](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/using-smart-lists/use-built-in-system-smart-lists).

## 쿼리

스마트 목록 쿼리는 자산의 표준 쿼리 유형을 따릅니다. [id 기준](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET), [이름순](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET), 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET).

### ID별

[ID별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByIdUsingGET) 단일 스마트 목록 사용 `id` 를 경로 매개 변수로 사용하고, 단일 스마트 목록 레코드를 반환합니다. 선택적으로 다음을 전달할 수 있습니다. `includeRules` 응답에 스마트 목록 규칙을 포함하는 부울 매개 변수.

![Smartlist 규칙](assets/smartlist-rules.png)

```
GET /rest/asset/v1/smartList/{id}.json?includeRules=true
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default",
            "rules": {
                "filterMatchType": "all",
                "triggers": [],
                "filters": [
                    {
                        "id": 459,
                        "name": "Visited Web Page",
                        "ruleTypeId": 1,
                        "ruleType": "Activity",
                        "operator": "occurs",
                        "conditions": [
                            {
                                "activityAttributeId": 1,
                                "activityAttributeName": "Web Page",
                                "operator": "is",
                                "values": [
                                    "Program Test.Landing Page Test 01"
                                ],
                                "isPrimary": true
                            },
                            {
                                "activityAttributeId": 6,
                                "activityAttributeName": "Browser",
                                "operator": "is",
                                "values": [
                                    "Chrome"
                                ],
                                "isPrimary": false
                            },
                            {
                                "activityAttributeId": -101,
                                "activityAttributeName": "Date of Activity",
                                "operator": "in past",
                                "values": [
                                    "30 days"
                                ],
                                "isPrimary": false
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

### 스마트 캠페인 ID별

[스마트 캠페인 ID로 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartListBySmartCampaignIdUsingGET) 단일 스마트 캠페인을 사용합니다. `id` 를 경로 매개 변수로 사용하고, 단일 스마트 목록 레코드를 반환합니다. 선택적으로 다음을 전달할 수 있습니다. `includeRules` 응답에 스마트 목록 규칙을 포함하는 부울 매개 변수.

```
GET /rest/asset/v1/smartCampaign/{smartCampaignId}/smartList.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default"
         }
    ]
}
```

### 프로그램 ID별

[프로그램 ID별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getSmartListByProgramIdUsingGET) 단일 이메일 프로그램 사용 `id` 를 경로 매개 변수로 사용하고, 단일 스마트 목록 레코드를 반환합니다. 선택적으로 다음을 전달할 수 있습니다. `includeRules` 응답에 스마트 목록 규칙을 포함하는 부울 매개 변수.

```
GET /rest/asset/v1/program/{programId}/smartList.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6efc#16c8967a21f",
    "warnings": [],
    "result": [
        {
            "id": 4363,
            "name": "Smart List Test 01",
            "createdAt": "2019-06-03T23:01:13Z+0000",
            "updatedAt": "2019-06-04T17:37:45Z+0000",
            "url": "https://app-sjqe.marketo.com/#SL4363A1LA1",
            "folder": {
                "id": 1041,
                "type": "Program"
            },
            "workspace": "Default"
         }
    ]
}
```

### 이름별

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) 스마트 목록을 가져옵니다. `name` 를 매개 변수로 사용하고, 단일 스마트 목록 레코드를 반환합니다.  인스턴스의 모든 스마트 목록 이름에 대해 정확한 문자열 일치가 수행되고 해당 이름과 일치하는 스마트 목록에 대한 결과가 반환됩니다.

```
GET /rest/asset/v1/smartList/byName.json?name=2018 Leads
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "115d7#16423bc13b4",
    "result": [
        {
            "id": 283988,
            "name": "2018 Leads",
            "createdAt": "2008-10-07T15:20:39Z+0000",
            "updatedAt": "2010-04-13T15:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL283988A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

### 찾아보기

스마트 목록은 다음과 같을 수도 있습니다. [일괄로 검색됨](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListsUsingGET). 다음 `folder` 매개 변수는 쿼리가 수행될 상위 폴더를 지정하는 데 사용됩니다. 다음을 포함하는 JSON 개체로 포맷됩니다. `id` 및 `type`. 다른 일괄 에셋 검색 엔드포인트와 마찬가지로 `offset` 및 `maxReturn` 는 페이징에 사용할 수 있는 선택적 매개 변수입니다. 선택 사항 `earliestUpdatedAt` 및 `latestUpdatedAt` datetime 매개 변수를 사용하여 UpdatedAt 날짜 범위별로 결과를 필터링할 수 있습니다.

```
GET /rest/asset/v1/smartLists.json?folder={"id":31,"type":"Folder"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "9aa4#16423c0e969",
    "result": [
        {
            "id": 283988,
            "name": "2018 Leads",
            "createdAt": "2008-10-07T15:20:39Z+0000",
            "updatedAt": "2010-04-13T15:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL283988A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        },
        {
            "id": 299697,
            "name": "Active Prospects",
            "createdAt": "2008-10-17T02:09:49Z+0000",
            "updatedAt": "2010-03-27T18:27:46Z+0000",
            "url": "https://app-abm.marketo.com/#SL299697A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        },
        {
            "id": 400517,
            "name": "Leads by Score",
            "createdAt": "2009-01-07T18:52:52Z+0000",
            "updatedAt": "2010-04-13T15:36:09Z+0000",
            "url": "https://app-abm.marketo.com/#SL400517A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

## 복제

[스마트 목록 복제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/cloneSmartListUsingPOST) 는 application/x-www-form-urlencoded POST으로 실행됩니다. 복제할 스마트 목록이 `id` 경로 매개 변수. 다음 `folder` 매개 변수는 스마트 목록을 만들 상위 폴더를 지정하는 데 사용되며 id 및 유형이 포함된 JSON 개체로 서식이 지정됩니다. 상위 폴더는 프로그램 또는 스마트 목록 폴더여야 합니다. 다음 `name` 매개 변수는 새 스마트 목록의 이름을 지정하는 데 사용되며 고유해야 합니다. 필요한 경우 `description` 파라미터는 스마트 리스트를 설명하는 데 사용될 수 있다.

```
POST /rest/asset/v1/smartList/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
folder={"id":31,"type":"Folder"}&name=2018 Leads Qualified
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "a672#16423d755ed",
    "result": [
        {
            "id": 788645,
            "name": "2018 Leads Qualified",
            "createdAt": "2018-06-21T19:34:32Z+0000",
            "updatedAt": "2018-06-21T19:34:32Z+0000",
            "url": "https://app-abm.marketo.com/#SL788645A1",
            "folder": {
                "id": 31,
                "type": "Folder"
            },
            "workspace": "Default"
        }
    ]
}
```

## 삭제

[스마트 목록 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/deleteSmartListByIdUsingPOST) 단일 스마트 목록 사용 `id` 를 경로 매개 변수로 사용하십시오.

```
POST /rest/asset/v1/smartList/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "8f5#16423dd0fbe",
    "result": [
        {
            "id": 788645
        }
    ]
}
```
