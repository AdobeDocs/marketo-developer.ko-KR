---
title: 스마트 캠페인
feature: REST API, Smart Campaigns
description: ID 또는 이름별 쿼리, 필터 찾아보기, 복제 삭제 만들기, 일정 또는 요청 트리거 등 스마트 캠페인용 Marketo REST API를 사용하는 방법에 대해 알아봅니다
exl-id: 540bdf59-b102-4081-a3d7-225494a19fdd
TQID: https://experienceleague.adobe.com/iysRjtqd9plkreyIMuNjAF3YVFHtDUIrc-GInB4V8mg
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
subfeature_v2:
  - id: ad89fb33-8541-4339-afe7-bb13d1633714
  - id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1009
ht-degree: 1%

---

# 스마트 캠페인

[스마트 캠페인 엔드포인트 참조(자산)](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns)

[Campaigns 엔드포인트 참조 (리드)](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns)

스마트 캠페인 REST API를 사용하여 스마트 캠페인을 쿼리, 생성, 복제 및 삭제합니다. 또한 일괄 캠페인을 예약하고, 캠페인을 트리거하고, 캠페인 활성화를 관리할 수 있습니다.

## 쿼리

스마트 캠페인을 [ID별](#by_id), [이름별](#by_name) 또는 [검색](#browse)별로 쿼리합니다.

### ID별

[ID별 Smart Campaign 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getSmartCampaignByIdUsingGET) 끝점은 단일 Smart Campaign `id`을(를) 경로 매개 변수로 사용하고 단일 Smart Campaign 레코드를 반환합니다.

```http
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

끝점은 `result` 배열의 첫 번째 위치에 레코드 한 개를 반환합니다.

### 이름별

[이름별 스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getSmartCampaignByNameUsingGET) 끝점은 단일 스마트 캠페인 `name`을(를) 매개 변수로 사용하고 단일 스마트 캠페인 레코드를 반환합니다.

```http
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

끝점은 `result` 배열의 첫 번째 위치에 레코드 한 개를 반환합니다.

### 찾아보기

[스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/getAllSmartCampaignsGET) 끝점은 필터링 및 페이지 매김을 위한 선택적 쿼리 매개 변수를 지원합니다.

`earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수는 ISO-8601 형식(밀리초 없음)으로 `datetimes`을(를) 허용합니다. 둘 다 설정된 경우 earliestUpdatedAt가 latestUpdatedAt 앞에 와야 합니다.

`folder` 매개 변수는 검색할 상위 폴더를 지정합니다. `id` 및 `type`이(가) 포함된 JSON 개체로 전달합니다.

`maxReturn` 정수는 최대 항목 수를 지정합니다. 기본값은 20이고 최대값은 200입니다.

`offset` 정수는 항목 검색을 시작할 위치를 지정합니다. `maxReturn`에 사용합니다. 기본값은 0입니다.

활성 트리거 캠페인만 반환하도록 `isActive` 부울 매개 변수를 설정하십시오.

```http
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

끝점이 `result` 배열에서 하나 이상의 레코드를 반환합니다.

## 만들기

[스마트 캠페인 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/createSmartCampaignUsingPOST) 끝점으로 `application/x-www-form-urlencoded` POST 요청을 보냅니다. `name` 및 `folder` 매개 변수가 필요합니다. `id` 및 `type`이(가) 포함된 JSON 개체로 `folder`을(를) 전달합니다.

필요한 경우 `description` 매개 변수(최대 2,000자)를 사용하여 스마트 캠페인을 설명할 수 있습니다.

```http
POST /rest/asset/v1/smartCampaigns.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[스마트 캠페인 업데이트](https://developer.adobe.com/marketo-apis/api/asset) 끝점으로 `application/x-www-form-urlencoded` POST 요청을 보냅니다. 스마트 캠페인 `id` 경로 매개 변수가 필요합니다. 이름을 변경하려면 `name`을(를) 사용하고 설명을 변경하려면 `description`을(를) 사용하십시오.

```http
POST /rest/asset/v1/smartCampaign/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
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

`application/x-www-form-urlencoded` POST 요청을 [Clone Smart Campaign](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) 끝점으로 보냅니다. `id`, `name` 및 `folder` 매개 변수가 필요합니다. 소스 캠페인, 새 캠페인 이름 및 상위 폴더를 지정합니다. `id` 및 `type`이(가) 포함된 JSON 개체로 `folder`을(를) 전달합니다.

필요한 경우 `description` 매개 변수(최대 2,000자)를 사용하여 스마트 캠페인을 설명할 수 있습니다.

```http
POST /rest/asset/v1/smartCampaign/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[스마트 캠페인 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/deleteSmartCampaignUsingPOST) 끝점은 단일 스마트 캠페인 `id`을(를) 경로 매개 변수로 사용합니다.

```http
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

일괄 스마트 캠페인은 지정된 시간에 실행되며 정의된 리드 세트를 함께 처리합니다.

## 예약

일괄 캠페인을 예약하려면 [캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/scheduleCampaignUsingPOST)을 사용하세요. 캠페인 `id` 경로 매개 변수가 필요합니다. 선택적 `tokens`, `runAt` 및 `cloneToProgram` 매개 변수를 JSON 요청 본문에 전달합니다.

`tokens` 배열은 이 실행에 대해 기존 프로그램 내 토큰을 재정의합니다. Marketo은 캠페인이 실행된 후 재정의를 삭제합니다. 각 항목에는 이름/값 쌍이 있으며 토큰 이름에는 `{{my.name}}` 형식을 사용해야 합니다.

`runAt` 날짜-시간 매개 변수는 캠페인을 실행할 시기를 지정합니다. 생략하면 캠페인이 요청 후 5분 후에 실행됩니다. 값은 앞으로 2년을 초과할 수 없습니다.

이 API를 통해 예약된 캠페인은 항상 실행 전 최소 5분 동안 대기합니다.

`cloneToProgram` 문자열 매개 변수에 결과 프로그램의 이름이 포함되어 있습니다.  설정하면 캠페인, 상위 프로그램 및 모든 자산이 결과 새 이름으로 만들어집니다. 상위 프로그램이 복제되고 새로 생성된 캠페인이 예약됩니다. 결과 프로그램은 상위 아래에 만들어집니다. 코드 조각, 푸시 알림, 인앱 메시지, 정적 목록, 보고서 및 소셜 자산이 있는 프로그램은 이러한 방식으로 복제되지 않을 수 있습니다. 이 끝점을 사용하면 하루에 20회 호출로 제한됩니다. [복제 프로그램](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) 끝점이 권장되는 대안입니다.

```http
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

스마트 캠페인 트리거 는 이벤트에 대한 응답으로 한 번에 한 명씩 처리합니다.

### 요청

[캠페인 요청](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns/operation/triggerCampaignUsingPOST)을 사용하여 트리거 캠페인의 흐름을 통해 리드를 전달합니다. 캠페인은 웹 서비스 API를 소스로 하는 캠페인 요청 트리거를 사용해야 합니다.

캠페인 `id` 경로 매개 변수 및 `leads` 정수 계열 리드 ID가 필요합니다. 각 호출에는 최대 100개의 리드가 허용됩니다.

선택적으로 `tokens` 배열 매개 변수를 사용하여 캠페인의 상위 프로그램에 로컬인 내 토큰을 재정의할 수 있습니다. `tokens`은(는) 최대 100개의 토큰을 허용합니다. 각 `tokens` 배열 항목에는 이름/값 쌍이 있습니다. 토큰 이름의 형식은 &quot;`{{my.name}}`&quot;이어야 합니다. [전자 메일에 시스템 토큰을 링크로 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/using-tokens/add-a-system-token-as-a-link-in-an-email) 접근 방식을 사용하여 &quot;viewAsWebpageLink&quot; 시스템 토큰을 추가하는 경우 `tokens`을(를) 사용하여 재정의할 수 없습니다. 대신 `tokens`을(를) 사용하여 &quot;viewAsWebPageLink&quot;를 재정의할 수 있는 [전자 메일에 웹 페이지로 보기 링크를 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-a-view-as-web-page-link-to-an-email) 방법을 사용하십시오.

JSON 요청 본문에 `leads` 및 `tokens` 매개 변수를 전달합니다.

```http
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

[스마트 캠페인 활성화](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/activateSmartCampaignUsingPOST) 끝점은 간단합니다. `id` 경로 매개 변수가 필요합니다. 활성화가 성공하려면 캠페인에 대해 다음 내용이 충족되어야 합니다.

- 캠페인이 비활성화되었습니다.
- 캠페인에는 하나 이상의 트리거와 흐름 단계가 있습니다.
- 캠페인에 오류 없는 트리거, 필터 및 흐름 단계가 있습니다.

```http
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

[스마트 캠페인 비활성화](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns/operation/deactivateSmartCampaignUsingPOST)는 간단합니다. `id` 경로 매개 변수가 필요합니다. 비활성화가 성공하려면 캠페인이 활성화되어야 합니다.

```http
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
