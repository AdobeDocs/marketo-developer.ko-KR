---
title: 인앱 메시지
feature: Mobile Marketing
description: Mobile SDK으로 Marketo In-App 메시지 설정, 사용자 지정 이벤트 트리거 구성, 탭 활동 추적 및 첫 번째 앱 열기 초기화 문제 해결.
exl-id: 73c9f862-d154-4b37-94ce-92311aa756e8
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# 인앱 메시지

Marketo의 인앱 메시지 기능을 사용하려면 다음 단계를 수행해야 합니다.

1. [모바일 설치](installation.md)에 설명된 대로 Marketo Mobile SDK을 설치합니다.
1. [모바일 앱 추가](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)에 설명된 대로 모바일 앱을 Marketo에 추가하십시오.
1. 모바일 앱에 코드를 추가하여 [사용자 지정 작업](custom-actions.md)을(를) 캡처할 수도 있습니다.

Marketo Mobile SDK을 설치하고 Marketo에 앱 추가를 완료하면 사용자가 앱을 열 때 표시되는 인앱 메시지를 전송할 수 있습니다.

기본적으로 인앱 메시지는 앱이 열릴 때 트리거됩니다. 특정 페이지를 볼 때 또는 특정 단추를 누를 때와 같은 다른 이벤트에 대해 인앱 메시지를 트리거하려면 코드에 사용자 지정 작업을 추가해야 합니다. 이에 대한 코드 샘플은 [사용자 지정 작업](custom-actions.md) 섹션을 참조하십시오.

## 문제 해결

**인앱 메시지가 표시되지 않음**

Marketo은 Marketo Mobile SDK이 Marketo Platform으로 초기화된 후에만 앱의 트리거에 응답합니다. 초기화 프로세스는 앱을 처음 설치하고 열 때 발생합니다. 초기화는 첫 번째 앱이 열린 후에 발생하므로 앱이 두 번째로 열릴 때까지 &quot;App Open&quot; 이벤트가 트리거되지 않습니다. 앱을 닫고 다시 열면 앱 열기에 의해 트리거된 메시지가 장치에 표시됩니다.

사용자 지정 이벤트는 앱이 열린 후 사용자 상호 작용에 의해 트리거됩니다. 사용자 지정 이벤트는 첫 번째 세션 동안 Marketo에서 인식됩니다.

**인앱 탭 활동 추적**

탭 활동을 추적하고 탭 수에 따라 기본 표시 빈도를 사용하려면 기본 또는 보조 단추 중 하나에 &quot;닫기&quot; 이외의 작업을 할당해야 합니다.

자세한 내용은 제품 설명서의 [인앱 메시지](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/mobile-marketing/in-app-messages/creating-in-app-messages/create-an-in-app-message) 섹션을 참조하십시오.
