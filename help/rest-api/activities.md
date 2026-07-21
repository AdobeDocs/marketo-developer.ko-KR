---
title: 활동
feature: REST API
description: Marketo Engage 활동 REST API를 사용하여 활동 유형을 나열하고, 페이징 토큰으로 리드 활동을 가져오고, 사용자 지정 및 데이터 값 변경을 처리합니다.
exl-id: 1e69af23-2b0c-467a-897c-1dcf81343e73
TQID: https://experienceleague.adobe.com/62keaj4uNoxIPCzr9AQzKrIsfuHBvC25knYisZRUvF4
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1758
ht-degree: 0%

---

# 활동

Marketo은 리드 레코드와 관련된 다양한 활동 유형을 지원합니다. 거의 모든 변경, 작업 또는 흐름 단계가 리드의 활동 로그에 기록됩니다. API를 통해 이러한 활동을 검색하거나 스마트 목록 및 스마트 캠페인 필터 및 트리거에서 사용할 수 있습니다.

각 활동에는 고유한 `id`이(가) 있으며 레코드의 ID 필드에 해당하는 `leadId`을(를) 통해 잠재 고객 레코드에 연결합니다. 모든 활동에도 `activityDate`이(가) 있습니다.

사용 가능한 활동 유형은 가입에 따라 다르며 각 유형에는 자체 정의가 있습니다. `primaryAttributeValueId` 및 `primaryAttributeValue`의 의미는 활동 유형에 따라 다릅니다.

사용자 지정 활동 메타데이터 API를 사용하여 사용자 지정 활동 유형을 만듭니다. 사용자 정의 활동 추가 API를 사용하여 사용자 정의 활동 레코드를 추가할 수 있습니다.

대부분의 활동은 일정 기간 후에 삭제됩니다.

## 설명

[활동 유형 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET) 끝점을 사용하여 인스턴스에 대해 사용 가능한 활동 유형과 해당 정의를 검색합니다.

```
GET /rest/v1/activities/types.json
```

```json
  "requestId": "6e78#148ad3b76f1",
  "success": true,
  "result": [
    {
      "id": 2,
      "name": "Fill Out Form",
      "description": "User fills out and submits form on web page",
      "primaryAttribute": {
        "name": "Webform ID",
        "dataType": "integer"
      },
      "attributes": [
        {
          "name": "Client IP Address",
          "dataType": "string"
        },
        {
          "name": "Form Fields",
          "dataType": "text"
        },
        {
          "name": "Query Parameters",
          "dataType": "string"
        },
        {
          "name": "Referrer URL",
          "dataType": "string"
        },
        {
          "name": "User Agent",
          "dataType": "string"
        },
        {
          "name": "Webpage ID",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

실제 응답에는 더 많은 정의가 포함됩니다. 이 예에서는 &quot;양식 작성&quot; 활동 유형을 보여 줍니다. 기본 속성인 &quot;Webform ID&quot;는 제출된 양식의 Marketo ID를 참조하고 활동을 해당 자산에 연결합니다.

또한 이 응답은 활동 유형과 해당 데이터 유형에 대해 가능한 각 속성을 정의합니다. 필드가 비어 있으면 해당 속성은 개별 활동 레코드에서 생략됩니다.

## 쿼리

[리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET) 끝점을 사용하여 활동을 검색합니다. 먼저 활동 검색이 시작되는 날짜/시간에 대한 페이징 토큰을 검색합니다. `nextPageToken` 쿼리 매개 변수에 해당 토큰을 전달합니다.

`activityTypeIds` 쿼리 매개 변수에서 최대 10개의 활동 유형 ID를 쉼표로 구분된 목록으로 전달합니다.

필요한 경우 다음 매개 변수 중 하나를 사용하여 쿼리 범위를 좁힙니다.

- `listId`은(는) 결과를 특정 정적 목록의 레코드로 제한합니다.
- `leadIds`은(는) 쉼표로 구분된 목록으로 제공되는 최대 30개의 잠재 고객에 대한 활동으로 결과를 제한합니다.

>[!CAUTION]
>
>2026-12-30부터 대상 목록에 10,000개 이상의 리드가 포함된 경우 `listId` 매개 변수를 포함하는 `Get Lead Activities` 및 `Get Lead Changes` 끝점에 대한 호출이 실패합니다(오류 코드 1003). 서비스 중단을 방지하려면 이 제한을 피하기 위해 호출 범위가 제대로 지정되었는지 확인하십시오. [마이그레이션 안내서](migration.md)를 참조하세요.

```
GET /rest/v1/activities.json?activityTypeIds=1&nextPageToken=WQV2VQVPPCKHC6AQYVK7JDSA3I3LCWXH3Y6IIZ7YSGQLXHCPVE5Q====
```

```json
{
  "requestId": "24fd#15188a88d7f",
  "result": [
    {
      "id": 102988,
      "marketoGUID": "102988",
      "leadId": 1,
      "activityDate": "2023-01-16T23:32:19Z",
      "activityTypeId": 1,
      "primaryAttributeValueId": 71,
      "primaryAttributeValue": "localhost/munchkintest2.html",
      "attributes": [
        {
          "name": "Client IP Address",
          "value": "10.0.19.252"
        },
        {
          "name": "Query Parameters",
          "value": ""
        },
        {
          "name": "Referrer URL",
          "value": ""
        },
        {
          "name": "User Agent",
          "value": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36"
        },
        {
          "name": "Webpage URL",
          "value": "/munchkintest2.html"
        }
      ]
    }
  ],
  "success": true,
  "nextPageToken": "WQV2VQVPPCKHC6AQYVK7JDSA3J62DUSJ3EXJGDPTKPEBFW3SAVUA====",
  "moreResult": false
}
```

첫 번째 호출의 경우 페이징 토큰 가져오기 API를 사용하여 `nextPageToken`을(를) 가져옵니다. 후속 호출마다 이전 응답이 반환하는 `nextPageToken`을(를) 전달합니다. 이 끝점은 항상 `nextPageToken`을(를) 반환합니다.

`moreResult`이(가) true이면 더 많은 결과를 사용할 수 있습니다. `moreResult`이(가) false가 될 때까지 반환된 `nextPageToken`을(를) 사용하여 끝점을 계속 호출합니다.

API는 `moreResult`을(를) true로 설정하는 동안 300개 미만의 활동 항목을 반환할 수 있습니다. 이 경우 반환된 `nextPageToken`을(를) 다른 호출에 포함시켜 보다 최근 활동을 검색하십시오.

각 결과 배열 항목 내에서 `marketoGUID` 문자열 특성이 `id` 정수 특성을 고유 식별자로 바꿉니다.

### 데이터 값 변경

리드 필드의 데이터 값 변경 레코드를 검색하려면 [리드 변경 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadChangesUsingGET) 끝점을 사용하십시오. 이 인터페이스의 인터페이스는 다음과 같은 두 가지 면에서 리드 활동 가져오기 API의 인터페이스와 다릅니다.

- 데이터 값 변경 및 새 잠재 고객 활동만 반환하므로 끝점에 `activityTypeIds` 매개 변수가 없습니다.
- 필수 `fields` 쿼리 매개 변수는 검색할 변경 내용을 쉼표로 구분한 필드 목록을 허용합니다.

>[!CAUTION]
>
>2026-12-30부터 대상 목록에 10,000개 이상의 리드가 포함된 경우 `listId` 매개 변수를 포함하는 `Get Lead Activities` 및 `Get Lead Changes` 끝점에 대한 호출이 실패합니다(오류 코드 1003). 서비스 중단을 방지하려면 이 제한을 피하기 위해 호출 범위가 제대로 지정되었는지 확인하십시오. [마이그레이션 안내서](migration.md)를 참조하세요.

```http
GET /rest/v1/activities/leadchanges.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&fields=firstName,lastName,department
```

```json
{
  "requestId": "a9ae#148add1e53d",
  "success": true,
  "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBRGA3TQ===",
  "moreResult": true,
  "result": [
    {
      "id": 1078,
      "marketoGUID": "1078",
      "leadId": 775,
      "activityDate": "2014-09-17T22:31:49+0000",
      "activityTypeId": 13,
      "fields": [
        {
          "id": 48,
          "name": "firstName",
          "newValue": "FirstName_6176",
          "oldValue": "FirstName_4914"
        }
      ],
      "attributes": [
        {
          "name": "Reason",
          "value": "Web service API"
        },
        {
          "name": "Source",
          "value": "Web service API"
        },
        {
          "name": "Lead ID",
          "value": 775
        }
      ]
    }
  ]
}
```

응답의 각 활동에는 변경 사항을 나열하는 필드 배열이 있습니다. 각 변경 사항은 필드의 `id` 및 `name`을(를) 새 값 및 이전 값과 함께 지정합니다.

각 결과 배열 항목 내에서 `marketoGUID` 문자열 특성이 `id` 정수 특성을 고유 식별자로 바꿉니다.

### 삭제된 리드

[삭제된 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET) 끝점을 사용하여 Marketo에서 삭제된 리드 활동을 검색합니다.

```http
GET /rest/v1/activities/deletedleads.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ
```

```json
{
  "requestId": "a9ae#148add1e53d",
  "success": true,
  "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBRGA3TQ===",
  "moreResult": true,
  "result": [
    {
      "id": 2,
      "marketoGUID": "2",
      "leadId": 6,
      "activityDate": "2013-09-26T06:56:35+0000",
      "activityTypeId": 37,
      "primaryAttributeValueId": 6,
      "primaryAttributeValue": "Owyliphys Iledil",
      "attributes": []
    },
    {
      "id": 3,
      "marketoGUID": "3",
      "leadId": 9,
      "activityDate": "2013-12-28T00:39:45+0000",
      "activityTypeId": 37,
      "primaryAttributeValueId": 4,
      "primaryAttributeValue": "First Last",
      "attributes": []
    }
  ]
}
```

각 결과 배열 항목 내에서 `marketoGUID` 문자열 특성이 `id` 정수 특성을 고유 식별자로 바꿉니다.

### 페이지 스루 결과

기본적으로 이 섹션의 끝점은 한 번에 300개의 활동 항목을 반환합니다. `moreResult`이(가) true이면 더 많은 결과를 사용할 수 있습니다. `moreResult`이(가) false가 될 때까지 후속 호출마다 반환된 `nextPageToken`을(를) 전달합니다.

끝점은 `moreResult`을(를) true로 설정하는 동안 300개 미만의 활동 항목을 반환할 수 있습니다. 이 경우 반환된 `nextPageToken`을(를) 다른 호출에 포함시켜 보다 최근 활동을 검색하십시오. 요청의 `nextPageToken` URL 인코딩이 완료되었습니다.

## 사용자 지정 활동 유형

사용자 지정 활동은 표준 활동처럼 작동하지만 타사에서 해당 스키마를 관리합니다. 사용자 지정 활동 레코드는 `leadId`을(를) 통해 잠재 고객 레코드로 연결되며 기본 및 보조 특성이 사용자 정의됩니다.

사용자 지정 활동 유형이 승인되면 Marketo은 해당 스마트 목록 트리거 및 필터를 만듭니다. 그런 다음 현재 또는 과거 사용자 지정 활동 데이터를 기반으로 리드를 처리할 수 있습니다.

- 최대 사용자 지정 활동: 10개
- 사용자 지정 활동당 최대 속성: 20

표준 활동을 검색하는 것과 같은 방식으로 [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET) API를 통해 사용자 지정 활동 데이터를 검색합니다.

## 쿼리 유형

[사용자 지정 활동 유형 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getCustomActivityTypeUsingGET)를 사용하여 Marketo 인스턴스에 제공된 유형에 대한 세부 정보를 검색합니다. [사용자 지정 활동 유형 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/describeCustomActivityTypeUsingGET)을(를) 사용하여 특정 유형에 대한 특성 메타데이터를 검색합니다.

표준 [활동 유형 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET) 끝점도 사용자 지정 활동 메타데이터를 반환하지만, 유형이 사용자 지정인지 여부는 식별하지 않습니다.

### 유형 가져오기

```http
GET /rest/v1/activities/external/types.json
```

```json
{
  "requestId": "185d6#14b51985ff0",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved"
    }
  ]
}
```

### 유형 설명

형식을 설명하려면 `apiName`을(를) 경로 매개 변수로 전달하십시오. 기본적으로 엔드포인트는 활동의 승인된 버전을 반환합니다. 초안 버전을 검색하려면 선택적 `draft=true` 매개 변수를 전달하십시오.

```http
GET /rest/v1/activities/external/type/{apiName}/describe.json
```

```json
{
  "requestId": "185d6#14b51985ff0",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendees",
          "name": "Number of Attendees",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

## 유형 만들기

각 사용자 지정 활동 유형에는 표시 이름, API 이름, 트리거 이름, 필터 이름 및 기본 속성이 필요합니다. 유형을 Marketo 규칙과 일관되게 유지하고 이름 지정 충돌을 방지하려면 다음 지침을 따르십시오.

- **표시 이름:** &quot;전자 메일 보내기&quot; 또는 &quot;데이터 값 변경&quot;과 같은 활동 레코드가 나타내는 내용을 간략하게 설명합니다. &quot;Attend Event&quot;와 같은 무한대 형식을 사용하십시오. 표시 이름에는 영숫자, 공백 및 밑줄이 포함되며 최소 한 자 이상이어야 합니다.

- **API 이름:** 영숫자를 사용하며 최대 길이는 255자입니다. LaunchPoint 파트너인 경우 대표 네임스페이스를 활동 유형 API 이름 앞에 추가하여 고객이 프로비저닝한 유형과의 충돌을 피하십시오. API 이름을 다른 문자열과 구분하려면 소문자 또는 카멜 문자를 사용하십시오.

- **설명:** 알 수 없는 동작이 있는 활동의 경우 잠재 고객과 관련하여 활동 유형이 나타내는 내용을 설명하십시오.

- **트리거 이름:** &quot;이벤트에 참석함&quot;과 같이 사람이 읽을 수 있는 고유한 이름을 서드파티 시제로 제공합니다. LaunchPoint 파트너에는 &quot;웨비나 참석 - Acme Company&quot;와 같은 회사 이름이 포함되어야 합니다.

- **필터 이름:** &quot;이벤트에 참석함&quot;과 같이 사람이 인식할 수 있는 고유한 이름을 3인칭 과거형으로 제공합니다. LaunchPoint 파트너에는 &quot;출석한 웨비나 - Acme Company&quot;와 같은 회사 이름이 포함되어야 합니다.

- **기본 특성:** 활동 유형에 가장 중요한 필드를 선택합니다. &quot;출석한 이벤트&quot; 활동의 경우 이 필드는 이벤트 이름입니다. 기본 속성은 활동 유형에 대한 모든 트리거 또는 필터에서 기본적으로 매개 변수로 표시됩니다. 해당 값은 활동을 드릴다운하지 않아도 개인의 활동 로그에도 표시됩니다.

새 사용자 지정 활동 유형이 초안으로 만들어집니다. 해당 유형의 활동 레코드를 추가하기 전에 유형을 승인합니다. 업데이트는 초안 버전에 적용되며 라이브 버전에 표시되기 전에 승인되어야 합니다. 사용자 지정 활동 유형이 승인되어 사용 중이면 이전 필드를 변경할 수 없습니다.

유형을 만들 때 설명 매개 변수는 선택 사항입니다. 필수 매개 변수는 `apiName`, `name`, `triggerName`, `filterName` 및 `primaryAttribute`입니다.

```http
POST /rest/v1/activities/external/type.json
```

```json
{
  "apiName": "attendConference",
  "name": "Attend Conference",
  "description": "Attend the conference",
  "triggerName": "Attends Conference",
  "filterName": "Attended Conference",
  "primaryAttribute": {
    "apiName": "conferenceName",
    "name": "Conference Name",
    "description": "Name of the conference"
  }
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attends Conference",
      "filterName": "Attended Conference",
      "status": "draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## 업데이트 유형

유형을 업데이트하려면 필수 apiName을 경로 매개 변수로 전달합니다. 다른 필드는 요청 본문에 제공할 수 있습니다.

```http
POST /rest/v1/activities/external/type/{apiName}.json
```

```json
{
  "name": "Attend Conference",
  "description": "Attend the conference",
  "triggerName": "Attend Conference",
  "filterName": "Attended Conference",
  "primaryAttribute": {
    "apiName": "conferenceName",
    "name": "Conference Name",
    "description": "Name of the conference"
  }
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "status": "draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## 승인 유형

Marketo 에셋의 표준처럼 사용자 지정 활동 유형 승인, 사용자 지정 활동 유형 초안 삭제 및 사용자 지정 활동 유형 삭제 를 사용하여 유형을 관리합니다.

## 사용자 지정 활동 유형 속성

각 사용자 지정 활동 유형에는 0~20개의 보조 속성이 있을 수 있습니다. 보조 속성은 모든 유효한 Marketo 필드 유형을 사용할 수 있습니다. 보조 속성을 상위 유형과 별도로 추가, 업데이트 및 제거합니다.

활동 유형이 사용 중인 동안 속성을 편집한 다음 변경 사항을 승인할 수 있습니다. 승인 후 생성된 활동은 새 보조 속성 세트를 사용합니다. 변경 사항은 해당 유형의 기존 활동에 소급하여 적용되지 않습니다.

속성을 제거하면 해당 필터에서 사용할 수 없게 됩니다.

보조 속성 목록에 대한 업데이트는 각 속성의 API 이름을 기본 키로 사용합니다. API 이름을 변경하려면 속성을 삭제하고 원하는 API 이름으로 다시 추가합니다.

속성에 유효한 데이터 유형은 문자열, 부울, 정수, 부동 소수점, 링크, 이메일, 통화, 날짜, 날짜, 날짜, 시간, 전화, 텍스트입니다.

활동 유형의 기본 특성을 변경하기 전에 `isPrimary`을(를) false로 설정하여 기존 기본 특성의 수준을 내립니다.

### 속성 만들기

특성을 만들려면 필요한 `apiName` 경로 매개 변수를 전달하십시오. `name` 및 `dataType` 매개 변수도 필요합니다. 설명 및 `isPrimary` 매개 변수는 선택 사항입니다.

```http
POST /rest/v1/activities/external/type/{apiName}/attributes/create.json
```

```json
{
  "attributes": [
    {
      "apiName": "conferenceDate",
      "name": "Conference Date",
      "description": "Date of the conference",
      "dataType": "datetime"
    },
    {
      "apiName": "numberOfAttendees",
      "name": "Number of Attendees",
      "description": "Number of people attending conference",
      "dataType": "integer"
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendees",
          "name": "Number of Attendees",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

### 속성 업데이트

특성을 업데이트할 때 `apiName` 특성은 기본 키이며 이미 존재해야 합니다. 업데이트로 `apiName`을(를) 변경할 수 없습니다.

```http
POST /rest/v1/activities/external/type/{apiName}/attributes/update.json
```

```json
{
  "attributes": [
    {
      "apiName": "conferenceDate",
      "name": "Conference Date",
      "description": "Date of the conference",
      "dataType": "datetime"
    },
    {
      "apiName": "numberOfAttendee",
      "name": "Number of Attendee",
      "description": "Number of people attending conference",
      "dataType": "integer"
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      },
      "attributes": [
        {
          "apiName": "conferenceDate",
          "name": "Conference Date",
          "description": "Date of the conference",
          "dataType": "datetime"
        },
        {
          "apiName": "numberOfAttendee",
          "name": "Number of Attendee",
          "description": "Number of people attending conference",
          "dataType": "integer"
        }
      ]
    }
  ]
}
```

### 속성 삭제

특성을 삭제하려면 사용자 지정 활동에 필요한 `apiName` 경로 매개 변수를 전달합니다. 필요한 속성 매개 변수를 속성 객체의 배열로 전달합니다. 각 개체에는 사용자 지정 활동 유형에 대한 `apiName` 매개 변수가 있어야 합니다.

```http
POST /rest/v1/activities/external/type/{apiName}/attributes/delete.json
```

```json
{ "attributes":[ { "apiName":"conferenceDate" }, { "apiName":"numberOfAttendees" } ] }
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 100001,
      "apiName": "attendConference",
      "name": "Attend Conference",
      "description": "Attend the conference",
      "triggerName": "Attend Conference",
      "filterName": "Attended Conference",
      "createdAt": "2016-02-03T22:36:23Z",
      "updatedAt": "2016-02-03T22:36:23Z",
      "status": "approved with draft",
      "primaryAttribute": {
        "apiName": "conferenceName",
        "name": "Conference Name",
        "description": "Name of the conference",
        "dataType": "string"
      }
    }
  ]
}
```

## 사용자 지정 활동 추가

사용자 지정 활동은 개별 개인 레코드에 대한 이전 활동을 한 번 기록하는 기록입니다. Marketo 관리자는 Marketo에서 스키마를 관리하거나 API 통합으로 원격으로 관리할 수 있습니다.

[사용자 지정 활동 추가](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/addCustomActivityUsingPOST) 끝점을 사용하여 리드 레코드에 사용자 지정 활동을 추가합니다. `leadId` 필드는 각 활동을 잠재 고객과 연결합니다. 잠재 고객의 활동 로그에서 사용자 정의 활동을 보거나 사용자 정의 활동 유형 ID를 지정하여 잠재 고객 활동 가져오기 를 통해 해당 활동을 검색합니다.

업데이트하거나 덮어쓸 필요가 없는 한 사람과 관련된 데이터에 대해 사용자 지정 활동을 사용하십시오. 예를 들어 이벤트 출석을 &quot;출석한 이벤트&quot; 활동으로 기록합니다.

학생 등록과 같이 변경될 수 있는 개인 관련 레코드에 사용자 정의 객체를 사용합니다. 사용자 지정 개체는 업데이트할 수 있지만 사용자 지정 활동은 업데이트할 수 없습니다.

입력 멤버는 활동 객체의 배열입니다. 한 번에 최대 300개의 활동 레코드를 제출할 수 있습니다.

`leadId`, `activityDate`, `activityTypeId`, `primaryAttributeValue` 및 특성 멤버가 필요합니다. 특성 배열에는 기본이 아닌 특성이 포함되어야 합니다. 이름(필드 이름) 또는 apiName(API 이름) 중 하나와 설정할 값에 대한 값을 사용하여 지정합니다.

```http
POST /rest/v1/activities/external.json
```

```json
{
  "input": [
    {
      "leadId": 1001,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Game Giveaway",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    },
    {
      "leadId": 1200,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Game Giveaway",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    },
    {
      "leadId": 3000,
      "activityDate": "2016-09-26T06:56:35+07:00",
      "activityTypeId": 1001,
      "primaryAttributeValue": "Contest Form",
      "attributes": [
        {
          "apiName": "uRL",
          "value": "http://www.nvidia.com/game-giveaway"
        }
      ]
    }
  ]
}
```

```json
{
  "requestId": "e42b#14272d07d78",
  "success": true,
  "result": [
    {
      "id": 50,
      "marketoGUID": "50",
      "status": "added"
    },
    {
      "id": 51,
      "marketoGUID": "51",
      "status": "added"
    },
    {
      "status": "skipped",
      "errors": [
        {
          "code": "1004",
          "message": "Lead not found"
        }
      ]
    }
  ]
}
```

## 시간 초과

활동 엔드포인트에는 30초의 시간 제한이 있습니다. 단, 다음 엔드포인트는 예외입니다.

- 페이징 토큰 가져오기: 300s
- 사용자 지정 활동 추가: 90초
