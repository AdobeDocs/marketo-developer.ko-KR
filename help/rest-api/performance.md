---
title: 성능
feature: REST API
description: Marketo API 작업에 대한 성능 팁입니다.
exl-id: 173a398a-9d36-4e8d-9dd3-7d0d375b085a
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 성능

이 페이지에는 통합의 성능을 향상시키는 데 사용할 수 있는 성능 관련 항목 목록이 포함되어 있습니다.

## HTTP 압축

Marketo REST API는 HTTP 1.1 사양에 정의된 표준을 사용하여 응답 본문의 HTTP 압축을 지원합니다. 압축을 사용하면 대역폭 사용량과 데이터 검색에 소요되는 시간이 감소하므로 압축을 사용하는 것이 좋습니다.

>[!NOTE]
>
>1024바이트 미만의 페이로드는 압축되지 않으며 벌크 API는 압축을 지원하지 않습니다.

압축을 사용하려면 요청에 다음 HTTP 헤더를 포함하십시오.

```html
Accept-Encoding: gzip
```

Marketo REST API는 응답 본문을 압축하며 다음 헤더를 포함합니다.

```html
Content-Encoding: gzip
```

다음은 Curl을 사용하여 [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET) 끝점을 호출하여 5개의 리드를 검색하는 예입니다.

```bash
curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
