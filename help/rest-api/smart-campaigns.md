---
title: "스마트 캠페인"
feature: REST API, Smart Campaigns
description: "스마트 캠페인 개요"
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---


# 스마트 캠페인

[스마트 캠페인 엔드포인트 참조(자산)](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns)

[Campaigns 엔드포인트 참조 (리드)](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns)

Marketo은 스마트 캠페인에서 작업을 수행하기 위한 일련의 REST API를 제공합니다. 이러한 API는 쿼리, 만들기, 복제 및 삭제 옵션을 제공하는 에셋 API에 대한 표준 인터페이스 패턴을 따릅니다. 또한 일괄 캠페인을 예약하거나 트리거 캠페인을 요청하여 스마트 캠페인 실행을 관리할 수 있습니다.

## 쿼리

스마트 캠페인 쿼리는 자산의 표준 쿼리 유형을 따릅니다. [id 기준](#by_id), [이름순](#by_name), 및 [브라우징](#browse).

### ID별

다음 [ID별 스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByIdUsingGET) 종단점은 단일 스마트 캠페인을 사용합니다. `id` 를 경로 매개 변수로 사용하고, 단일 스마트 캠페인 레코드를 반환합니다.

```
GET /rest/asset/v1/smartCampaign/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "7883#169838a32f0",
    "warnings": [],
    "result": [
        {
            "id": 1001,
            "name": "Process Bounced Emails",
            "description": "System smart campaign for processing bounced email events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1001,
            "flowId": 1001,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1001A1"
        }
    ]
}
```

이 끝점을 사용하면 의 첫 번째 위치에 항상 단일 레코드가 있습니다. `result` 배열입니다.

### 이름별

다음 [이름별 스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getSmartCampaignByNameUsingGET) 종단점은 단일 스마트 캠페인을 사용합니다. `name` 를 매개 변수로 사용하고, 단일 스마트 캠페인 레코드를 반환합니다.

```
GET /rest/asset/v1/smartCampaign/byName.json?name=Test Trigger Campaign
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "14494#16c886ffa44",
    "warnings": [],
    "result": [
        {
            "id": 1069,
            "name": "Test Trigger Campaign",
            "description": "",
            "createdAt": "2018-02-16T01:34:39Z+0000",
            "updatedAt": "2019-08-13T00:45:21Z+0000",
            "folder": {
                "id": 327,
                "type": "Folder"
            },
            "status": "Inactive",
            "type": "trigger",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 2747,
            "flowId": 1088,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1069A1"
        }
    ]
}
```

이 끝점을 사용하면 의 첫 번째 위치에 항상 단일 레코드가 있습니다. `result` 배열입니다.

### 찾아보기

다음 [스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/getAllSmartCampaignsGET) 끝점은 다른 Asset API 검색 끝점과 마찬가지로 작동하며, 몇 가지 선택적 쿼리 매개 변수를 사용하여 필터링 기준을 지정할 수 있습니다.

다음 `earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수 accept `datetimes` (밀리초 없이). 둘 다 설정된 경우 earliestUpdatedAt가 latestUpdatedAt 앞에 와야 합니다.

다음 `folder` 매개 변수는 아래에서 검색할 상위 폴더를 지정합니다. 형식은 을 포함하는 JSON 블록입니다. `id` 및 `type` 속성.

다음 `maxReturn` 매개 변수는 반환할 최대 항목 수를 지정하는 정수입니다. 기본값은 20입니다. 최대값은 200입니다.

다음 `offset` 매개 변수는 항목 검색을 시작할 위치를 지정하는 정수입니다. 과 함께 사용할 수 있습니다. `maxReturn`. 기본값은 0입니다.

다음 `isActive` 매개 변수는 활성 트리거 캠페인만 반환하도록 지정하는 부울입니다.

```
GET /rest/asset/v1/smartCampaigns.json?earliestUpdatedAt=2016-09-10T23:15:00-00:00&latestUpdatedAt=2016-09-10T23:17:00-00:00
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "626#16983a92965",
    "warnings": [],
    "result": [
        {
            "id": 1001,
            "name": "Process Bounced Emails",
            "description": "System smart campaign for processing bounced email events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1001,
            "flowId": 1001,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1001A1"
        },
        {
            "id": 1002,
            "name": "Process Unsubscribes",
            "description": "System smart campaign for processing unsubscribe events",
            "createdAt": "2016-09-10T23:16:19Z+0000",
            "updatedAt": "2016-09-10T23:16:19Z+0000",
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 1002,
            "flowId": 1002,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1002A1"
        }
    ]
}
```

이 끝점을 사용하면 `result` 배열입니다.

## 만들기

다음 [스마트 캠페인 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/createSmartCampaignUsingPOST) 끝점은 두 개의 필수 매개 변수가 있는 application/x-www-form-urlencoded POST으로 실행됩니다. 다음 `name` 매개 변수는 만들 스마트 캠페인의 이름을 지정합니다. 다음 `folder` 매개 변수는 스마트 캠페인이 만들어지는 상위 폴더를 지정합니다. 형식은 을 포함하는 JSON 블록입니다. `id` 및 `type` 속성.

필요한 경우 다음을 사용하여 스마트 캠페인을 설명할 수 있습니다. `description` 매개 변수(최대 2,000자)입니다.

```
POST /rest/asset/v1/smartCampaigns.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Smart Campaign 02&folder={"type": "folder","id": 640}&description=This is a smart campaign creation test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "25bc#16c9138f148",
    "warnings": [],
    "result": [
        {
            "id": 1076,
            "name": "Smart Campaign 02",
            "description": "This is a smart campaign creation test.",
            "createdAt": "2019-08-14T17:42:04Z+0000",
            "updatedAt": "2019-08-14T17:42:04Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": true,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5132,
            "flowId": 1095,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1076A1"
        }
    ]
}
```

## 업데이트

다음 [스마트 캠페인 업데이트](https://developer.adobe.com/marketo-apis/api/asset/) 끝점은 application/x-www-form-urlencoded POST으로 실행됩니다. 하나의 스마트 캠페인이 필요합니다. `id` 를 경로 매개 변수로 사용하십시오. 다음을 사용할 수 있습니다. `name` 스마트 캠페인의 이름을 업데이트하는 매개 변수 또는 `description` 스마트 캠페인의 설명을 업데이트하는 매개 변수입니다.

```
POST /rest/asset/v1/smartCampaign/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Smart Campaign 02 Update&description=This is a smart campaign update test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "14b6a#16c924b992f",
    "warnings": [],
    "result": [
        {
            "id": 1076,
            "name": "Smart Campaign 02 Update",
            "description": "This is a smart campaign update test.",
            "createdAt": "2019-08-14T17:42:04Z+0000",
            "updatedAt": "2019-08-14T22:42:04Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Never Run",
            "type": "batch",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": true,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5132,
            "flowId": 1095,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1076A1"
        }
    ]
}
```

## 복제

다음 [스마트 캠페인 복제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 끝점은 세 개의 필수 매개 변수가 있는 application/x-www-form-urlencoded POST으로 실행됩니다. 다음이 필요합니다. `id` 복제할 스마트 캠페인을 지정하는 매개 변수 `name` 새 스마트 캠페인의 이름을 지정하는 매개 변수 `folder` 새 스마트 캠페인이 만들어지는 상위 폴더를 지정하는 매개 변수입니다. 형식은 을 포함하는 JSON 블록입니다. `id` 및 `type` 속성.

필요한 경우 다음을 사용하여 스마트 캠페인을 설명할 수 있습니다. `description` 매개 변수(최대 2,000자)입니다.

```
POST /rest/asset/v1/smartCampaign/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Test Trigger Campaign Clone&folder={"type": "folder","id": 640}&description=This is a smart campaign clone test.
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "681d#16c9339499b",
    "warnings": [],
    "result": [
        {
            "id": 1077,
            "name": "Test Trigger Campaign Clone",
            "description": "This is a smart campaign clone test.",
            "createdAt": "2019-08-15T03:01:41Z+0000",
            "updatedAt": "2019-08-15T03:01:41Z+0000",
            "folder": {
                "id": 640,
                "type": "Folder"
            },
            "status": "Inactive",
            "type": "trigger",
            "isSystem": false,
            "isActive": false,
            "isRequestable": false,
            "isCommunicationLimitEnabled": false,
            "recurrence": {
                "weekdayOnly": false
            },
            "qualificationRuleType": "once",
            "workspace": "Default",
            "smartListId": 5135,
            "flowId": 1096,
            "computedUrl": "https://app-sjqe.marketo.com/#SC1077A1"
        }
    ]
}
```

## 삭제

다음 [스마트 캠페인 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deleteSmartCampaignUsingPOST) 종단점은 단일 스마트 캠페인을 사용합니다. `id` 를 경로 매개 변수로 사용하십시오.

```
POST /rest/asset/v1/smartCampaign/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d757#16c934216ac",
    "warnings": [],
    "result": [
        {
            "id": 1077
        }
    ]
}
```

## 배치

일괄 스마트 캠페인은 특정 시간에 시작되며 특정 리드 세트에 한 번에 영향을 줍니다.

## 예약

사용 [캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/scheduleCampaignUsingPOST) 배치 캠페인을 즉시 또는 미래 날짜에 실행하도록 예약하는 끝점입니다. 캠페인 `id` 는 필수 경로 매개 변수입니다. 선택적 매개 변수는 `tokens`, `runAt`, 및 `cloneToProgram` 요청 본문에 application/json으로 전달됩니다.

tokens array 매개 변수는 기존 프로그램 토큰을 재정의하는 My 토큰의 배열입니다. 캠페인 실행 후 토큰이 삭제됩니다.  각 토큰 배열 항목에는 이름/값 쌍이 포함되어 있습니다. 토큰 이름의 형식은 &quot;여야 합니다.{{my.name}}&quot;.

runAt datetime 매개 변수는 캠페인을 실행할 시기를 지정합니다. 지정하지 않으면 끝점이 호출된 후 5분 후에 캠페인이 실행됩니다. datetime 값은 미래까지 2년을 초과할 수 없습니다.

이 API를 통해 예약된 캠페인은 항상 실행 전 최소 5분 동안 대기합니다.

다음 `cloneToProgram` string 매개 변수에는 결과 프로그램의 이름이 포함됩니다.  설정하면 캠페인, 상위 프로그램 및 모든 자산이 결과 새 이름으로 만들어집니다. 상위 프로그램이 복제되고 새로 생성된 캠페인이 예약됩니다. 결과 프로그램은 상위 아래에 만들어집니다. 코드 조각, 푸시 알림, 인앱 메시지, 정적 목록, 보고서 및 소셜 자산이 있는 프로그램은 이러한 방식으로 복제되지 않을 수 있습니다. 이 끝점을 사용하면 하루에 20회 호출로 제한됩니다. 다음 [복제 프로그램](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 엔드포인트는 권장되는 대안입니다.

```
POST /rest/v1/campaigns/{id}/schedule.json
```

```json
{
   "input":
      {
         "runAt": "2018-03-28T18:05:00+0000",
         "tokens": [
            {
               "name": "{{my.message}}",
               "value": "Updated message"
            },
            {
               "name": "{{my.other token}}",
               "value": "Value for other token"
            }
          ]
      }
}
```

```json
{
    "requestId": "52b#161d90e1743",
    "result": [
        {
            "id": 3713
        }
    ],
    "success": true
}
```

## 트리거

스마트 캠페인 트리거는 트리거된 이벤트를 기반으로 한 번에 한 명에게 영향을 줍니다.

### 요청

사용 [캠페인 요청](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/triggerCampaignUsingPOST) 리드 집합을 캠페인 흐름을 통해 실행할 트리거 캠페인으로 전달하는 종단점입니다. 캠페인에는 &quot;웹 서비스 API&quot;를 소스로 하는 &quot;캠페인 요청&quot; 트리거가 있어야 합니다.

이 끝점에는 캠페인이 필요합니다. `id` 를 경로 매개 변수로 사용하고 `leads` 리드 id 를 포함하는 정수 배열 매개 변수 호출당 최대 100개의 리드가 허용됩니다.

필요한 경우 `tokens` 배열 매개 변수를 사용하여 캠페인의 상위 프로그램에 로컬인 내 토큰을 재정의할 수 있습니다. `tokens` 은 최대 100개의 토큰을 허용합니다. 각 `tokens` 배열 항목에 이름/값 쌍이 포함되어 있습니다. 토큰 이름의 형식은 &quot;여야 합니다.{{my.name}}&quot;. 를 사용하는 경우 [시스템 토큰을 이메일에 링크로 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/using-tokens/add-a-system-token-as-a-link-in-an-email) &quot;viewAsWebpageLink&quot; 시스템 토큰을 추가하려면 다음을 사용하여 재정의할 수 없습니다. `tokens`. 대신 사용 [전자 메일에 웹 페이지로 보기 링크 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-a-view-as-web-page-link-to-an-email) 을 사용하여 &quot;viewAsWebPageLink&quot;를 재정의할 수 있는 접근 방식 `tokens`.

다음 `leads` 및 `tokens` 매개 변수는 요청 본문에 application/json으로 전달됩니다.

```
POST /rest/v1/campaigns/{id}/trigger.json
```

```json
{
   "input":
      {
         "leads" : [
            {
               "id" : 318592
            },
            {
               "id" : 318593
            }
         ],
         "tokens" : [
            {
               "name": "{{my.message}}",
               "value": "Updated message"
            },
            {
               "name": "{{my.other token}}",
               "value": "Value for other token"
            }
         ]
      }
}
```

```json
{
    "requestId": "9e01#161d922f1aa",
    "result": [
        {
            "id": 3712
        }
    ],
    "success": true
}
```

### 활성화

다음 [스마트 캠페인 활성화](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/activateSmartCampaignUsingPOST) 끝점은 간단합니다. An `id` 경로 매개 변수가 필요합니다. 활성화가 성공하려면 캠페인에 대해 다음 내용이 충족되어야 합니다.

- 비활성화해야 함
- 하나 이상의 트리거와 흐름 단계가 있어야 합니다.
- 오류를 사용하지 않는 트리거, 필터 및 흐름 단계가 있어야 합니다.

```
POST /rest/asset/v1/smartCampaign/{id}/activate.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "a33a#161d9c0dcf3",
    "result": [
        {
            "id": 1069
        }
    ]
}
```

### 비활성화

다음 [스마트 캠페인 비활성화](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Campaigns/operation/deactivateSmartCampaignUsingPOST) 간단합니다. An `id` 경로 매개 변수가 필요합니다. 비활성화가 성공하려면 캠페인이 활성화되어야 합니다.

```
POST /rest/asset/v1/smartCampaign/{id}/deactivate.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6228#161d9c29fbf",
    "result": [
        {
            "id": 1069
        }
    ]
}
```
