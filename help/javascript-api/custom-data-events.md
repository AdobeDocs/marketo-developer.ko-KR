---
title: 사용자 지정 데이터 이벤트
description: 고유한 이벤트를 추적하려면 사용자 지정 데이터 이벤트 Javascript API를 사용하십시오.
feature: Javascript
exl-id: ef7cab9c-3bd0-450e-9247-9324b1e6f9ab
source-git-commit: e609f9d5d58f656298412acef5e2106a19765396
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# 사용자 지정 데이터 이벤트

이 메서드는 추적 및 실시간 개인화를 위한 사용자 지정 이벤트를 보냅니다. 타사 데이터를 보내거나 방문자 행동을 기반으로 사용자 지정 이벤트를 트리거하는 데 사용할 수 있습니다. 사용자 지정 데이터 이벤트는 방문자 세션에서 한 번 계산됩니다.

User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| `send` | 필수 여부 | 문자열 | 메서드 작업. |
| `event` | 필수 여부 | 문자열 | 메서드 이름입니다. |
| `customData` | 필수 여부 | 문자열 또는 배열 | 사용자 지정 데이터. |

## 예시

### 사용자 지정 데이터에 대한 문자열을 사용하여 이벤트 보내기

```javascript
var customData = {value: 'MyEvent'};
rtp('send', 'event', customData);
```

### 사용자 지정 데이터에 대한 문자열 배열을 사용하여 이벤트 보내기

사용자 지정 데이터 배열에는 최대 4개의 요소가 포함될 수 있습니다.  4개 이상의 요소를 보내야 하는 경우 모든 항목이 전송될 때까지 이벤트 API 보내기(최대 4개 항목 포함)를 반복적으로 호출합니다.

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### 단추 클릭에 따라 이벤트 보내기

Marketo은 웹 사이트의 콘텐츠를 특정 백서를 다운로드하는 웹 방문자에게 개인화합니다. 이렇게 하려면 사용자 지정 데이터 이벤트를 보내는 방문자의 백서 다운로드 버튼 클릭을 캡처합니다. 다운로드 백서 단추를 클릭한 모든 방문자의 RTP 세그먼트로, 각 방문자에게 2번의 클릭을 제공하는 개인화된 캠페인을 표시합니다. 다운로드한 백서와 관련된 다른 내용을 표시하면 됩니다.

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
