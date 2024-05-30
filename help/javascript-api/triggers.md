---
title: "트리거"
description: "트리거"
feature: Javascript
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 8%

---


# 트리거

전역 rtp 개체의 특정 상태에서 함수를 트리거하는 기능을 추가합니다.

Web Personalization 고객이고 [RTP 태그 배포됨](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) User Context API를 사용하기 전에 사이트에 게시합니다.

## 사용량

`rtp('triggerName', function_to_trigger);`

| 매개 변수 | 선택 사항/필수 | 유형 | 설명 |
|---------------------|-------------------|----------|----------------------|
| &#39;triggerName&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| function_to_trigger | 필수 | 함수 | 트리거할 함수입니다. |


### 사용자 컨텍스트 준비 트리거

사용자 위치를 기반으로 사용자 지정 변수를 설정합니다. 이 함수는 &quot;rtpUserContext&quot; 전역 개체가 준비되면 호출됩니다.

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
