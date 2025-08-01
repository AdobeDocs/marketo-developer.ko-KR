---
title: 사용자 컨텍스트
feature: REST API
description: 사용자 컨텍스트 개요 및 API 설명
exl-id: b8daace2-07a5-4621-aa3a-03fa9f66ea73
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 5%

---

# 사용자 컨텍스트

User Context JavaScript API는 사용자 및 방문자 수준 데이터를 여러 세션에 노출하여 기록 사용자 동작 및 데이터를 사용하는 고급 개인화 기능을 활성화합니다. API는 데이터 읽기를 넘어 고급 세분화 및 개인화 목적을 위해 의미 있는 데이터 및 이벤트를 RTP 백엔드에 푸시할 수 있는 사용자 지정 변수를 표시합니다. 추가 기능: [트리거](../javascript-api/triggers.md), [패턴 일치](../javascript-api/pattern-match.md).

- User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- 사용자 컨텍스트 API는 요청 시 Marketo 지원에서 활성화해야 하는 기능입니다. API가 활성화되면 RTP 전역 개체 아래의 userContext 개체가 표시됩니다.

## 사용자 컨텍스트 속성

| 이름 | 유형 | 설명 |
|------------------|-------------|------|
| customVar[1-5] | 문자열 | 사용자 컨텍스트에 사용자 정의 데이터가 저장되었습니다. |
| viewedCampaigns | 캠페인 ID를 쉼표로 구분된 문자열로 | 현재 또는 이전 방문에서 캠페인을 확인했습니다. |
| 클릭된 캠페인 | 캠페인 ID를 쉼표로 구분된 문자열로 | 현재 또는 이전 방문에서 캠페인을 클릭함. |

## 사용자 지정 변수 설정

사용자 컨텍스트에 사용자 정의 데이터 추가.

### 사용

`rtp('set', 'customVar'[1-5], my_custom_value);`

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|-----------------|-------------------|--------|-----------------|
| &#39;설정&#39; | 필수 | 문자열 | 메서드 작업. |
| customVar | 필수 | 문자열 | 사용자 지정 변수 이름입니다. |
| my_custom_value | 필수 | 문자열 | 인덱스 1-5의 사용자 지정 변수에 저장할 사용자 지정 값입니다. |

참고: 사용자 지정 변수는 보기 호출 시에만 RTP로 전송되므로 보기를 호출하기 전에 사용자 지정 변수를 설정하는 것이 좋습니다. 그렇지 않으면 다음 보기 호출에서만 전송됩니다.

사용자 지정 Var 제한

- 사용자 지정 변수 길이는 100자를 초과할 수 없습니다.
- 캠페인 데이터는 방문당 캠페인이 10개인 마지막 10개 방문으로 제한됩니다.

### 사용

`rtp('set', 'customVar', 'A');`

```javascript
// Set and get customVars
rtp('set', 'customVar1', 'foo');

// Read location
if (rtp.userContext.location.state == 'CA')  {
    // Do something
}

// Check if user viewed campaign id 45:
// The campaign id is exposed in the RTP UI when hovering over a campaign name.
if (rtp.userContext.viewedCampaign('45')) {
    // Do something
}
```
