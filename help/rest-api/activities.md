---
title: 활동
feature: REST API
description: Marketo Engage 활동 관리를 위한 API입니다.
exl-id: 1e69af23-2b0c-467a-897c-1dcf81343e73
source-git-commit: 6baf62bc8881470eca597899e3228c377fb597d0
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 0%

---

# 활동

Marketo은 리드 레코드와 관련된 매우 다양한 활동 유형을 허용합니다.  거의 모든 변경, 작업 또는 흐름 단계가 리드의 활동 로그에 기록되며 API를 통해 검색되거나 Smart List 및 Smart Campaign 필터 및 트리거에서 활용될 수 있습니다.  활동은 항상 레코드의 ID 필드에 해당하는 leadId를 통해 잠재 고객 레코드와 다시 관련되며 고유한 자체 ID도 있습니다.

잠재적인 활동 유형은 매우 많으며, 구독마다 다를 수 있으며 각각에 대해 고유한 정의가 있습니다. 모든 활동에는 고유한 `id`, `leadId` 및 `activityDate`이(가) 있지만 `primaryAttributeValueId` 및 `primaryAttributeValue` 값은 의미가 다릅니다.

또한 Marketo에서는 사용자 지정 활동 메타데이터 API를 통해 사용자 지정 활동 유형을 만들 수 있습니다. 사용자 정의 활동 추가는 사용자 정의 활동 추가 API를 통해 수행됩니다.

대부분의 활동은 일정 기간 후에 삭제됩니다.

## 설명

인스턴스에 대해 사용 가능한 형식 목록과 해당 정의를 검색하려면 [활동 형식 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET) 끝점을 사용합니다.

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

현실 세계의 반응은 훨씬 더 많은 정의를 포함한다. 이 예제에서 보여 주는 유형은 &quot;Fill Out Form&quot;으로, &quot;Webform ID&quot;의 기본 속성이 있으며, 이는 채워진 양식의 Marketo ID를 다시 참조하고 Marketo에서 해당 특정 에셋과 다시 연결하는 데 사용할 수 있습니다. 또한 이 유형의 특정 활동 레코드와 해당 데이터 유형의 가능한 각 속성에 대한 정의가 있습니다. 필드가 비어 있으면 개별 활동 레코드에서 해당 특정 속성이 생략됩니다.

## 쿼리

Marketo에서 활동을 검색하려면 [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET) 끝점을 호출하십시오. 먼저 활동 검색을 시작할 날짜/시간에 대한 페이징 토큰을 검색해야 합니다. 그런 다음 `nextPageToken` 쿼리 매개 변수에 페이징 토큰을 전달합니다. 또한 `activityTypeIds` 쿼리 매개 변수에 최대 10개의 활동 유형 ID를 쉼표로 구분된 목록으로 전달합니다.

선택적으로 listId 쿼리 매개 변수를 포함하여 특정 정적 목록에 포함된 레코드로만 검색 범위를 좁히거나, leadIds 쿼리 매개 변수를 포함하여 지정된 리드 집합에서만 활동을 검색할 수 있습니다. 최대 30개의 leadId를 쉼표로 구분된 목록으로 전달할 수 있습니다.

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

첫 번째 호출의 경우 Get Paging Token API를 사용하여 `nextPageToken`을(를) 가져옵니다. 이 끝점에 대한 후속 호출의 경우 응답의 `nextPageToken returned`을(를) 사용하십시오. 이 끝점은 항상 `the nextPageToken`을(를) 반환합니다.

`moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. `moreResult` 특성이 false를 반환할 때까지 이 끝점을 계속 호출하십시오. 즉, 사용 가능한 결과가 없습니다. 이 API에서 반환된 `nextPageToken`은(는) 항상 이 호출의 다음 반복에 재사용해야 합니다.

경우에 따라 이 API는 300개 미만의 활동 항목으로 응답할 수 있지만 `moreResult` 특성도 true로 설정되어 있습니다.  이는 반환할 수 있는 활동이 더 있으며 반환된 `nextPageToken`을(를) 후속 호출에 포함하여 더 최근의 활동에 대해 끝점을 쿼리할 수 있음을 나타냅니다.

각 결과 배열 항목 내에서 `id` 정수 특성은 고유 식별자로 `marketoGUID` 문자열 특성으로 대체됩니다. 

### 데이터 값 변경

데이터 값 변경 활동의 경우 활동 API의 전문 버전이 제공됩니다. [잠재 고객 변경 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET) 끝점은 데이터 값 변경 레코드의 활동만 잠재 고객 필드에 반환합니다. 인터페이스는 두 가지 차이점이 있는 리드 활동 가져오기 API와 동일합니다.

* 끝점이 데이터 값 변경 및 새 잠재 고객 활동만 반환하므로 `activityTypeIds` 매개 변수가 없습니다.
* `fields` 쿼리 매개 변수가 필요합니다. 여기서 쉼표로 구분된 필드 목록을 전달하여 변경 내용을 검색할 필드를 나타낼 수 있습니다.

```
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

응답의 각 활동에는 변경된 필드의 `id` 및 `name`과(와) 변경 내용에 상대적인 새 값 및 이전 값을 지정하는 활동의 변경 내용 목록을 포함하는 필드 배열이 있습니다.

각 결과 배열 항목 내에서 `id` 정수 특성은 고유 식별자로 `marketoGUID` 문자열 특성으로 대체됩니다.

### 삭제된 리드

또한 Marketo에서 삭제된 활동을 검색하기 위한 특수 엔드포인트 [삭제된 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET)가 있습니다.

```
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

각 결과 배열 항목 내에서 `id` 정수 특성은 고유 식별자로 `marketoGUID` 문자열 특성으로 대체됩니다.

### 페이지 스루 결과

기본적으로 이 섹션에 언급된 종단점은 한 번에 300개의 활동 항목을 반환합니다.  `moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. `moreResult` 특성이 false를 반환할 때까지 끝점을 호출합니다. 즉, 사용 가능한 결과가 더 이상 없습니다. 이 끝점에서 반환된 `nextPageToken`은(는) 항상 이 호출의 다음 반복에 재사용되어야 합니다.

경우에 따라 이 끝점은 300개 미만의 활동 항목으로 응답할 수 있지만 `moreResult` 특성도 true로 설정되어 있습니다.  이는 반환할 수 있는 추가 활동이 있으며 반환된 `nextPageToken`을(를) 후속 호출에 포함하여 더 최근의 활동에 대해 끝점을 쿼리할 수 있음을 나타냅니다. `nextPageToken`은(는) 요청에 URL로 인코딩되어야 합니다.

## 사용자 지정 활동 유형

사용자 지정 활동은 Marketo이 아닌 서드파티가 스키마를 관리한다는 점을 제외하고 표준 활동과 동일하게 작동합니다. 사용자 지정 활동의 인스턴스는 표준 활동처럼 `leadId`을(를) 통해 잠재 고객 레코드에 연결되지만 기본 특성과 보조 특성은 모두 임의로 정의됩니다. 사용자 지정 활동 유형이 승인되면 해당 스마트 목록 트리거 및 필터가 생성되므로 현재 또는 과거 사용자 지정 활동 데이터를 기반으로 리드를 처리할 수 있습니다.

* 최대 사용자 지정 활동 수: 10
* 사용자 지정 활동당 최대 속성 수: 20

사용자 지정 활동 데이터 검색은 [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET) API를 통해 표준 활동과 동일한 방식으로 수행됩니다.

## 쿼리 유형

표준 Get Activity Types 끝점 외에 [Get Custom Activity Types](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getCustomActivityTypeUsingGET) 및 [Describe Custom Activity Type](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/describeCustomActivityTypeUsingGET) 끝점은 Marketo 인스턴스에 제공된 활동 유형에 대한 세부 정보와 지정된 유형의 속성에 대한 메타데이터를 반환합니다. 일반 [활동 유형 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET)에서는 여전히 사용자 지정 활동에 대한 메타데이터를 반환하지만 지정된 유형이 사용자 지정인지 여부는 나타내지 않습니다.

### 유형 가져오기

```
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

형식 설명의 경우 `apiName`을(를) 경로 매개 변수로 전달해야 합니다. 기본적으로 활동의 승인된 버전을 받게 됩니다. 필요에 따라 `draft=true` 매개 변수를 전달하여 활동의 초안 버전을 검색할 수 있습니다.

```
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

각 사용자 지정 활동 유형에는 표시 이름, API 이름, 트리거 이름, 필터 이름 및 기본 속성이 필요합니다.

Marketo 규칙과 유형의 일관성을 보장하고 충돌을 방지하려면 유형을 생성할 때 다음 몇 가지 지침을 따르는 것이 중요합니다.

**표시 이름:** 활동 유형의 표시 이름에는 &quot;전자 메일 보내기&quot; 또는 &quot;데이터 값 변경&quot;과 같이 활동 레코드가 나타내는 것이 간략하게 설명되어 있습니다. 이러한 이름은 일반적으로 &quot;Attend Event&quot;와 같은 무한대 형식이어야 합니다.  표시 이름에는 영숫자, 공백 및 밑줄이 사용됩니다. 표시 이름에는 문자가 하나 이상 포함되어야 합니다.

**API 이름:** API 이름은 영숫자 문자(최대 길이 255)로 구성됩니다. LaunchPoint 파트너인 경우 활동 유형 API 이름에 대표 네임스페이스를 앞에 추가해야 합니다. 고객이 프로비저닝한 유형과의 충돌을 방지하기 위한 것입니다.  이 규칙은 다른 텍스트 문자열을 구분하는 데 도움이 되도록 모든 소문자 또는 카멜 대/소문자를 사용하는 것입니다.

**설명:** 알 수 없는 동작이 있을 수 있는 활동의 경우 잠재 고객과 관련하여 활동 유형이 나타내는 내용에 대한 설명이 포함되어야 합니다.

**트리거 이름:** 각 활동 유형에는 사람이 읽을 수 있는 고유한 트리거 이름이 있어야 합니다. 트리거 이름은 &quot;이벤트 참석&quot;과 같이 3인칭 현재 시제로 해야 합니다. LaunchPoint 파트너는 &quot;웨비나 참석 - Acme Company&quot;와 같이 회사 이름을 활동에 포함해야 합니다.

**필터 이름:**  각 활동 유형에는 사람이 읽을 수 있는 고유한 필터 이름이 있어야 합니다. 필터 이름은 &quot;이벤트에 참석함&quot;과 같이 세 번째 사람 과거형으로 표시되어야 합니다. LaunchPoint 파트너는 활동에 회사 이름, 즉 &quot;출석한 웨비나 - Acme Company&quot;를 포함해야 합니다.

**기본 특성:** 사용자 지정 활동의 기본 특성은 활동 유형에 가장 중요한 필드여야 합니다. 예를 들어 &quot;출석한 이벤트&quot; 활동의 경우 이 이름은 이벤트의 이름이 됩니다. 기본 속성은 해당 활동 유형에 대한 트리거 또는 필터의 모든 인스턴스에 기본적으로 매개 변수로 포함되며, 이 값은 활동에 대한 드릴다운이 필요 없이 개인 레코드의 활동 로그에 표시됩니다.

사용자 지정 활동이 만들어지면 초안으로 만들어지므로 해당 유형의 활동 레코드를 추가하는 데 사용하려면 먼저 승인을 받아야 합니다. 모든 업데이트는 유형의 초안 버전에 암시적으로 적용됩니다. 유형의 라이브 버전에서 변경된 사항을 반영하려면 승인을 받아야 합니다. 사용자 지정 활동 유형이 승인되어 사용 중인 경우 위의 필드를 변경할 수 없습니다.

형식을 만들 때 설명 매개 변수는 선택 사항이지만 `apiName`, `name`, `triggerName`, `filterName`, `primaryAttribute` 매개 변수는 모두 필요합니다.

```
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

apiName이 경로 매개 변수로서 유일한 필수 매개 변수라는 점을 제외하면 형식을 업데이트하는 것은 매우 유사합니다.

```
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

유형은 표준 Marketo 에셋과 마찬가지로 사용자 지정 활동 유형 승인, 사용자 지정 활동 유형 초안 폐기 및 사용자 지정 활동 유형 삭제로 관리할 수 있습니다.


## 사용자 지정 활동 유형 속성

각 사용자 지정 활동 유형에는 0~20개의 보조 속성이 있을 수 있습니다. 보조 속성에는 Marketo 필드에 대한 유효한 필드 유형이 있을 수 있습니다. 상위 유형과 별도로 추가, 업데이트 및 제거되지만, 활동 유형이 사용 중인 동안 편집한 다음 승인될 수 있습니다. 라이브 유형에서 필드를 편집할 때 승인 후 생성된 해당 유형의 모든 활동에는 새 보조 속성이 설정됩니다. 변경 사항은 해당 유형을 공유하는 기존 활동에 소급하여 적용되지 않습니다.

특성 제거는 해당 필터에서의 사용 가능 여부에 영향을 주므로 주의하십시오.

보조 속성 목록에 대한 업데이트는 각 속성의 API 이름을 기본 키로 사용합니다. 속성에 대한 API 이름은 변경할 수 없으며 삭제했다가 원하는 API 이름으로 다시 추가해야 합니다.

속성에 유효한 데이터 유형은 문자열, 부울, 정수, 부동 소수점, 링크, 이메일, 통화, 날짜, 날짜, 날짜, 시간, 전화, 텍스트입니다.

활동 유형의 기본 특성을 변경할 때 먼저 `isPrimary`을(를) false로 설정하여 기존의 모든 기본 특성을 강등해야 합니다.

### 속성 만들기

특성을 만들려면 필요한 `apiName` 경로 매개 변수가 필요합니다. `name` 및 `dataType` 매개 변수도 필요합니다.` The description and` `isPrimary` 매개 변수는 선택 사항입니다.

```
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

특성에 대한 업데이트를 수행할 때 특성의 `apiName`이(가) 기본 키입니다. 업데이트가 성공하려면 `apiName` 매개 변수가 있어야 합니다. 즉, 업데이트를 사용하여 `apiName` 매개 변수를 변경할 수 없습니다.

```
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

특성을 삭제하면 사용자 지정 활동 API 이름인 필수 `apiName` 경로 매개 변수가 사용됩니다.  속성 객체의 배열인 속성 매개 변수도 필요합니다.  각 개체에는 사용자 지정 활동 유형 API 이름인 `apiName` 매개 변수가 있어야 합니다.

```
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

사용자 지정 활동은 Marketo의 개별 개인 레코드와 관련된 기록 활동을 한 번 기록한 기록입니다. 이러한 활동에는 Marketo 관리자가 관리하거나 API 통합을 통해 원격으로 관리하는 스키마가 있습니다. 사용자 지정 활동은 [사용자 지정 활동 추가](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/addCustomActivityUsingPOST) 끝점을 통해 잠재 고객 레코드에 추가되며 `leadId` 필드를 통해 각 잠재 고객 레코드와 관련되어 있습니다. 사용자 지정 활동은 잠재 고객의 활동 로그를 통해 사용자 인터페이스에서 보거나 사용자 지정 활동의 유형 ID를 지정하여 잠재 고객 활동 가져오기 엔드포인트를 통해 검색할 수 있습니다.

사용자 지정 활동은 한 사람 레코드와 관련되어 있으며 업데이트하거나 덮어쓸 필요가 없는 데이터를 기록하는 데 적합합니다. 예를 들어 이벤트에 참석하는 사람을 &quot;출석한 이벤트&quot; 활동으로 기록하는 것입니다. 학생 등록과 같이 변경될 수 있는 개인과 관련된 레코드의 경우, 사용자 지정 활동이 없을 수 있는 경우, 사용자 지정 객체를 대신 사용해야 합니다.

입력 멤버는 활동 객체의 배열입니다. 한 번에 최대 300개의 활동 레코드를 제출할 수 있습니다.

`leadId`, `activityDate`, `activityTypeId`, `primaryAttributeValue` 및 특성 멤버가 필요합니다. 특성 배열에는 기본이 아닌 특성이 포함되어야 합니다. 이름(필드 이름) 또는 apiName(API 이름) 및 설정 중인 값에 해당하는 값을 사용하여 지정할 수 있습니다.

```
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

아래에 명시하지 않는 한 활동 엔드포인트에 30초의 시간 제한이 있습니다.

* 페이징 토큰 가져오기: 300s 
* 사용자 지정 활동 추가: 90초
