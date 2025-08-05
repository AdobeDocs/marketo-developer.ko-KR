---
title: Triggers
description: Triggers
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 13%

---

# Triggers

전역 rtp 개체의 특정 상태에서 함수를 트리거하는 기능을 추가합니다.

User Context API를 사용하기 전에 웹 Personalization 고객이고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.

## 사용

`rtp('triggerName', function_to_trigger);`

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
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
