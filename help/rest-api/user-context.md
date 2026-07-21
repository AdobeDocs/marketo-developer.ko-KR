---
title: 사용자 컨텍스트
feature: REST API
description: Marketo RTP User Context API를 활성화하고 사용하여 사용자 지정 변수를 설정하고, 방문 간에 사용자 데이터를 읽고, 보고 클릭한 캠페인을 추적하는 방법에 대해 알아봅니다.
exl-id: b8daace2-07a5-4621-aa3a-03fa9f66ea73
TQID: https://experienceleague.adobe.com/Ph0Tw-C9jzWaR4bYyUIXyzzoa2yjHQk2gt6tNA8H2mA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
subfeature_v2:
  - id: a1d50dda-6d94-4e16-8c30-5eb7181c4650
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 5%

---

# 사용자 컨텍스트

User Context JavaScript API는 사용자 수준 및 방문자 수준 데이터를 여러 세션에 노출합니다. 이전 비헤이비어 및 데이터를 사용하여 고급 개인화를 만듭니다.

또한 API는 세분화 및 개인화를 위해 데이터 및 이벤트를 RTP 백엔드로 전송하기 위한 사용자 지정 변수를 제공합니다. 관련 [트리거](../javascript-api/triggers.md) 및 [패턴 일치](../javascript-api/pattern-match.md) 기능을 참조하십시오.

- 웹 Personalization 고객이고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- User Context API를 활성화하려면 Marketo 지원에 요청해야 합니다. 활성화 후에 userContext 개체는 RTP 전역 개체 아래에 노출됩니다.

## 사용자 컨텍스트 속성

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| `customVar[1-5]` | 문자열 | 사용자 컨텍스트에 사용자 정의 데이터가 저장되었습니다. |
| `viewedCampaigns` | 캠페인 ID를 쉼표로 구분된 문자열 | 현재 또는 이전 방문에서 캠페인을 확인했습니다. |
| `clickedCampaigns` | 캠페인 ID를 쉼표로 구분된 문자열 | 현재 또는 이전 방문에서 캠페인을 클릭함. |

## 사용자 지정 변수 설정

사용자 지정 변수를 설정하여 사용자 컨텍스트에 데이터를 추가합니다.

### 사용

`rtp('set', 'customVar'[1-5], my_custom_value);`

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| `'set'` | 필수 | 문자열 | 메서드 작업. |
| `customVar` | 필수 | 문자열 | 사용자 지정 변수 이름입니다. |
| `my_custom_value` | 필수 | 문자열 | 인덱스 1-5의 사용자 지정 변수에 저장할 사용자 지정 값입니다. |

사용자 지정 변수는 보기 호출에서만 RTP로 전송됩니다. 보기 호출 전에 사용자 지정 변수를 설정합니다. 그렇지 않으면 다음 보기 호출에서 변수가 전송됩니다.

사용자 지정 변수에는 다음과 같은 제한 사항이 있습니다.

- 사용자 지정 변수는 100자를 초과할 수 없습니다.
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
