---
title: 페이징 토큰
feature: REST API
description: Marketo REST API 페이징 토큰을 사용하여 날짜 기반 및 위치 기반 토큰, ISO 8601 sinceDatetime 및 414 오류를 포함하는 활동 및 리드를 검색합니다.
exl-id: 63fbbf03-8daf-4add-85b0-a8546c825e5b
TQID: https://experienceleague.adobe.com/Ut05n-Y-qPJnvcNRs9liwE3NVBMbJlvaGyv-nExRsek
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 387
ht-degree: 0%

---

# 페이징 토큰

Marketo은 특정 날짜를 기준으로 업데이트된 결과 또는 검색 데이터를 통해 페이지에 페이징 토큰을 제공합니다.

일부 응답은 긴 페이징 토큰 문자열을 반환하며, 이로 인해 HTTP 414 오류가 발생할 수 있습니다. 이 [오류](error-codes.md) 처리에 대한 정보를 참조하세요.

[페이징 토큰 API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getActivitiesPagingTokenUsingGET) 설명서를 참조하십시오.

## 토큰 유형

Marketo은 서로 관련성이 있지만 고유한 두 가지 유형의 페이징 토큰을 제공합니다.

- 날짜 기반 토큰은 지정된 날짜/시간 이후에 발생하는 레코드를 검색합니다.
- 위치 기반 토큰은 결과 세트의 레코드를 트래버스합니다.

## 날짜 기반

날짜 기반 페이징 토큰은 날짜/시간을 나타냅니다. 해당 날짜/시간 이후에 발생하는 활동, 데이터 값 변경 및 삭제된 잠재 고객을 검색하는 데 사용합니다.

날짜/시간으로 [페이징 토큰 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getActivitiesPagingTokenUsingGET) 끝점을 호출하여 날짜 기반 토큰을 생성합니다.

```http
GET /rest/v1/activities/pagingtoken.json?sinceDatetime=2014-10-06T13:22:17-08:00
```

```json
{
    "requestId": "1607c#14884f3e74e",
    "success": true,
    "nextPageToken": "GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
}
```

`sinceDateTime` 매개 변수는 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 표준 날짜 표기법을 사용해야 합니다. 최상의 결과를 얻으려면 시간대가 포함된 전체 날짜/시간을 제공하십시오.

시간대를 다음 형식으로 GMT로부터의 오프셋으로 나타냅니다.

`yyyy-mm-ddThh:mm:ss+|-hh:mm`

또는 대문자 &quot;Z&quot;를 사용하여 UTC를 나타냅니다.

`yyyy-mm-ddThh:mm:ssZ`

예:

`2016-09-15T15:53:00+05:00`

`2016-09-15T10:53:00Z`

`sinceDateTime`은(는) 쿼리 매개 변수이므로 해당 값을 URL 인코딩하십시오.

반환된 `nextPageToken` 문자열을 [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadActivitiesUsingGET), [리드 변경 사항 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getLeadChangesUsingGET) 또는 [삭제된 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET) 호출에 전달합니다. 이 호출은 페이징 토큰 가져오기 API에 제공된 날짜/시간 이후에 발생하는 레코드를 검색합니다.

```http
GET /rest/v1/activities.json?nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ&activityTypeIds=1&activityTypeIds=12
```

## 위치 기반

배치 검색 호출에서 리드 데이터베이스 API로 위치 기반 페이징 토큰을 반환할 수 있습니다. 토큰은 데이터베이스 커서처럼 작동하며 레코드 순회를 활성화합니다.

예를 들어 필터 유형별 리드 가져오기 호출은 요청된 배치 크기보다 큰 결과 세트를 반환할 수 있습니다. 이 크기는 일반적으로 최대 및 기본값이 300입니다. 더 많은 결과를 사용할 수 있는 경우 응답은 moreResult 필드를 true로 설정하고 `nextPageToken`을(를) 반환합니다.

다음 페이지를 검색하려면 다른 호출을 수행하고 이전 응답의 `nextPageToken` 값을 전달하십시오. 응답은 결과 세트의 다음 페이지를 반환합니다.
