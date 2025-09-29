---
title: 페이징 토큰
feature: REST API
description: Marketo REST API 페이징 토큰을 사용하여 날짜 기반 및 위치 기반 토큰, ISO 8601 sinceDatetime 및 414 오류를 포함하는 활동 및 리드를 검색합니다.
exl-id: 63fbbf03-8daf-4add-85b0-a8546c825e5b
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 페이징 토큰

결과를 페이징하거나 주어진 데이터와 관련하여 업데이트된 데이터를 검색하기 위해 Marketo에서는 페이징 토큰을 제공합니다.

경우에 따라 긴 페이징 토큰 문자열이 반환될 수 있습니다. 이로 인해 HTTP 414 오류 코드가 발생할 수 있습니다. 이러한 [오류](error-codes.md)를 처리하는 방법에 대한 자세한 정보를 찾을 수 있습니다.

[페이징 토큰 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) 설명서를 참조하십시오.

## 토큰 유형

Marketo에서 제공하는 서로 관련되지만 고유한 두 가지 유형의 페이징 토큰이 있습니다.

- 날짜 기반
- 위치 기반

## 날짜 기반

첫 번째는 날짜를 나타내는 페이징 토큰입니다. 페이징 토큰이 나타내는 일자 이후에 발생한 활동, 데이터 값 변경 및 삭제된 리드를 검색하는 데 사용됩니다. 이 유형의 페이징 토큰은 [페이징 토큰 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET) 끝점을 호출하고 날짜/시간을 포함하여 생성됩니다.

```
GET /rest/v1/activities/pagingtoken.json?sinceDatetime=2014-10-06T13:22:17-08:00
```

```json
{
    "requestId": "1607c#14884f3e74e",
    "success": true,
    "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
}
```

`sinceDateTime` 매개 변수의 형식은 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 표준 날짜 표기법을 준수해야 합니다. 최상의 결과를 얻으려면 시간대가 포함된 전체 날짜/시간을 사용하십시오. 시간대는 다음 형식을 사용하여 GMT로부터의 오프셋으로 표시할 수 있습니다.

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

또는 다음과 같이 대문자 &quot;Z&quot;를 속기로 사용하여 UTC를 나타냅니다.

`yyyy-mm-ddThh:mm:ssZ`

예

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

`sinceDateTime`은(는) 쿼리 매개 변수이므로 URL로 인코딩되어야 합니다.

그런 다음 `nextPageToken` 문자열이 [잠재 고객 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadActivitiesUsingGET), [잠재 고객 변경 사항 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getLeadChangesUsingGET) 또는 [삭제된 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) 호출에 제공되며, 활동은 페이징 토큰 가져오기 API에 제공된 날짜/시간 이후부터 검색됩니다.

```
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 위치 기반

제2 유형의 페이징 토큰은 리드 데이터베이스 API에 대한 임의의 배치 검색 호출에 의해 반환될 수 있다. 이 유형의 페이징 토큰은 레코드 순회를 활성화하는 데이터베이스 커서와 개념상 유사합니다. 예를 들어 필터 유형별 리드 가져오기 호출은 주어진 배치 크기보다 큰 집합(일반적으로 최대 및 기본값 300)을 나타낼 수 있습니다. 결과가 많으면 moreResult 필드가 응답에 true이고 `nextPageToken`이(가) 반환됩니다. 결과 집합에서 추가 레코드를 검색하려면 새 호출의 이전 응답에서 받은 값이 있는 `nextPageToken`을(를) 포함하는 추가 호출이 필요합니다. 결과 응답은 결과 세트의 다음 페이지를 반환합니다.
