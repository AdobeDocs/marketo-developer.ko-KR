---
title: 성능
feature: REST API
description: HTTP 압축으로 Marketo REST API 성능을 향상시킵니다. gzip을 활성화하여 대역폭을 줄입니다. 벌크 API는 지원되지 않으며 1024바이트 미만이면 압축되지 않습니다.
exl-id: 173a398a-9d36-4e8d-9dd3-7d0d375b085a
TQID: https://experienceleague.adobe.com/foJCTd890HZtL-UzWx2cjRXwTxqgW56A79sB7FPEWis
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 1%

---

# 성능

이 페이지의 성능 옵션을 사용하여 통합의 효율성을 개선합니다.

## HTTP 압축

Marketo REST API는 HTTP 1.1 사양에 정의된 대로 HTTP 응답 본문 압축을 지원합니다. 압축을 활성화하여 대역폭 사용량과 데이터 검색 시간을 줄입니다.

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

다음 cURL 예제는 [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET) 끝점을 호출하여 5개의 리드를 검색합니다.

```bash
curl -H 'Accept-Encoding: gzip' 'https://123-ABC-456.mktorest.com/rest/v1/leads.json?filterType=id&filterValues=4,5,7,12,13'
```
