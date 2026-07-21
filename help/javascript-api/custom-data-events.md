---
title: 사용자 지정 데이터 이벤트
description: Web Personalization용 RTP JavaScript API로 사용자 지정 이벤트를 보내고 매개 변수, 최대 4개의 항목 및 클릭 기반 트리거를 포함한 문자열 또는 배열 데이터를 보냅니다.
feature: Javascript
exl-id: ef7cab9c-3bd0-450e-9247-9324b1e6f9ab
TQID: https://experienceleague.adobe.com/oWDmtMF94xG5HYXeTwkx5zF9PWo98bpwoVB6kAKLYDo
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 241
ht-degree: 3%

---

# 사용자 지정 데이터 이벤트

이 메서드를 사용하여 추적 및 실시간 개인화를 위한 사용자 지정 이벤트를 전송합니다. 방문자 행동에 따라 서드파티 데이터를 보내거나 사용자 지정 이벤트를 트리거할 수 있습니다.

각 사용자 지정 데이터 이벤트는 방문자 세션 중에 한 번 계산됩니다.

User Context API를 사용하기 전에 웹 Personalization 고객이고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| `send` | 필수 | 문자열 | 메서드 작업. |
| `event` | 필수 | 문자열 | 메서드 이름입니다. |
| `customData` | 필수 | 문자열 또는 배열 | 사용자 지정 데이터. |

## 예

### 사용자 지정 데이터에 대한 문자열을 사용하여 이벤트 보내기

```javascript
var customData = {value: 'MyEvent'};
rtp('send', 'event', customData);
```

### 사용자 지정 데이터에 대한 문자열 배열을 사용하여 이벤트 보내기

사용자 지정 데이터 배열에는 최대 4개의 요소가 포함될 수 있습니다. 4개 이상의 요소를 전송하려면 각 호출에 4개 이하의 항목을 사용하여 이벤트 전송 API를 반복적으로 호출하십시오.

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### 단추 클릭에 따라 이벤트 보내기

이 예에서는 방문자가 특정 백서를 다운로드하기 위해 버튼을 선택할 때 사용자 지정 데이터 이벤트를 보냅니다. RTP는 이벤트를 사용하여 이러한 방문자를 실시간으로 세그먼트화할 수 있습니다.

그런 다음 웹 사이트에서 두 번 더 클릭하면 개인화된 캠페인을 표시할 수 있습니다. 예를 들어 캠페인은 다운로드한 백서와 관련된 다른 콘텐츠를 제공할 수 있습니다.

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
