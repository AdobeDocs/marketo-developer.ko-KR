---
title: 인앱 메시지
feature: Mobile Marketing
description: Mobile SDK으로 Marketo In-App 메시지 설정, 사용자 지정 이벤트 트리거 구성, 탭 활동 추적 및 첫 번째 앱 열기 초기화 문제 해결.
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
TQID: https://experienceleague.adobe.com/RVkEUBaFb-PHd0gE9ngzYc5zOojINwSI7ic2TmcU7-8
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 321
ht-degree: 2%

---

# 인앱 메시지

Marketo 인앱 메시지를 사용하려면 다음 단계를 완료하십시오.

1. [모바일 설치](installation.md)에 설명된 대로 Marketo Mobile SDK을 설치합니다.
1. [모바일 앱 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)에 설명된 대로 모바일 앱을 Marketo에 추가하십시오.
1. 선택 사항: 모바일 앱에 코드를 추가하여 [사용자 지정 작업](custom-actions.md)을 캡처합니다.

Marketo Mobile SDK을 설치하고 Marketo에 앱을 추가한 후 사용자가 앱을 열 때 표시되는 인앱 메시지를 보낼 수 있습니다.

기본적으로 인앱 메시지는 앱이 열릴 때 트리거됩니다. 특정 페이지 보기 또는 특정 버튼 선택과 같은 다른 이벤트에 대한 메시지를 트리거하려면 코드에 사용자 지정 작업을 추가합니다. 코드 샘플은 [사용자 지정 작업](custom-actions.md)을 참조하세요.

## 문제 해결

**인앱 메시지가 표시되지 않음**

Marketo은 Marketo Mobile SDK이 Marketo Platform으로 초기화된 후에만 앱 트리거에 응답합니다. 앱을 처음 설치하고 열 때 초기화가 발생합니다.

초기화는 첫 번째 앱이 열린 후에 발생하므로 앱을 두 번째로 열 때까지 &quot;앱 열기&quot; 이벤트가 트리거되지 않습니다. 앱을 닫았다가 다시 엽니다. 그러면 앱 열기에 의해 트리거된 메시지가 장치에 표시됩니다.

사용자 지정 이벤트는 앱이 열린 후 사용자 상호 작용에 의해 트리거됩니다. 사용자 지정 이벤트는 첫 번째 세션 동안 Marketo에서 인식됩니다.

**인앱 탭 활동 추적**

탭 활동을 추적하고 탭 수에 따른 표시 빈도를 지정하려면 기본 또는 보조 단추에 &quot;닫기&quot; 이외의 작업을 할당합니다.

자세한 내용은 제품 설명서에서 [인앱 메시지](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message)를 참조하세요.
