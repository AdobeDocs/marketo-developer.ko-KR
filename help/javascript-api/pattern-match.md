---
title: 패턴 일치
description: RTP rtp.checkPattern 유틸리티를 사용하여 비율 와일드카드로 문자열 패턴을 테스트합니다. 동기화 제한 사항, 사용 및 URL 예제, 필수 RTP 태그 설정을 참조하십시오.
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
TQID: https://experienceleague.adobe.com/-HopUg6-2EchL9kJrPDbz62mRlrqYaXYdufILjkvP1Y
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
source-wordcount: 188
ht-degree: 4%

---

# 패턴 일치

RTP는 패턴이 문자열과 일치하는지 여부를 확인하는 유틸리티 함수를 제공합니다. 유틸리티는 일치 결과를 동기식으로 반환하며 비동기식으로 사용할 수 없습니다.

User Context API를 사용하기 전에 웹 Personalization 고객이고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.

## 사용

> rtp.checkPattern(check_by, pattern);

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| check_about | 필수 | 문자열 | 패턴을 일치시킬 문자열입니다(예: 현재 페이지 URL 또는 제품 이름). |
| 패턴 | 필수 | 문자열 | 일치시킬 패턴입니다. 문자열의 시작, 끝 또는 내용과 일치하도록 와일드카드로 `%`을(를) 추가하십시오. 전체 일치 항목을 보려면 `%`을(를) 생략하십시오. |

## 예

이 예에서는 현재 페이지 URL이 &quot;productA&quot;로 끝나는 경우 색인 1에 사용자 지정 변수를 설정합니다.

```javascript
if (rtp.checkPattern(window.location.href, '%productA')) {
    rtp('set', 'custom1', 'productA');
}
```

다음 예에서 현재 URL 경로는 &#39;/products/productB&#39;입니다. 이 예제에서는 경로에 &quot;products&quot;가 포함되어 있는지 확인한 다음 사용자 지정 변수를 설정합니다.

```javascript
var currentURLPath = '/products/productB';
if (rtp.checkPattern(currentURLPath, '%products%')) {
    rtp('set', 'custom1', 'products');
}
```
