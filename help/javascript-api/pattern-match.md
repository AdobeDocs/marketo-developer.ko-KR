---
title: 패턴 일치
description: RTP rtp.checkPattern 유틸리티를 사용하여 비율 와일드카드로 문자열 패턴을 테스트합니다. 동기화 제한 사항, 사용 및 URL 예제, 필수 RTP 태그 설정을 참조하십시오.
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---

# 패턴 일치

RTP는 패턴이 특정 문자열과 일치하는지 확인하기 위한 유틸리티 함수를 노출합니다. 일치하는 항목이 있는지 여부를 나타내므로 이 유틸리티는 비동기 방식으로 사용할 수 없습니다.

User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.

## 사용

> rtp.checkPattern(check_by, pattern);

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| check_about | 필수 | 문자열 | 패턴을 일치시킬 문자열입니다. 예: 현재 페이지 url, 제품 이름. |
| 패턴 | 필수 | 문자열 | 와일드카드에 대해 % 추가 패턴은 :start이(가) 포함된 전체 일치 항목일 수 있습니다. |

## 예

현재 페이지 URL이 &quot;productA&quot;로 끝나는 경우 인덱스 1에서 사용자 지정 변수를 설정합니다.

```javascript
if (rtp.checkPattern(window.location.href, '%productA')) {
    rtp('set', 'custom1', 'productA');
}
```

현재 URL 경로는 &#39;/products/productB&#39;입니다. 이 예제에서는 경로에 &quot;products&quot;가 포함되어 있는지 확인하고 사용자 지정 변수를 설정합니다.

```javascript
var currentURLPath = '/products/productB';
if (rtp.checkPattern(currentURLPath, '%products%')) {
    rtp('set', 'custom1', 'products');
}
```
