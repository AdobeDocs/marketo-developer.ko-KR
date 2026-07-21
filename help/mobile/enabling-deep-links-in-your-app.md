---
title: 딥링크 활성화
feature: Mobile Marketing
description: iOS, Android 및 PhoneGap의 지침 및 모범 사례를 통해 사용자 지정 URI 체계를 사용하여 Marketo 푸시 메시지에 대한 앱의 딥링크를 활성화하는 방법에 대해 알아봅니다.
exl-id: c3647416-d81d-4f15-b660-bcb3e54cb9bc
TQID: https://experienceleague.adobe.com/UswOvHXGlfTrTUqr4Gsf3j2Z7Xpv2FF2luXeygT4qE0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 363
ht-degree: 1%

---

# 딥링크 활성화

딥링크는 사용자를 앱의 특정 콘텐츠로 안내합니다. 예를 들어, 사용자가 자주색 티셔츠를 광고하는 모바일 푸시 메시지를 선택하면 앱이 홈 페이지 대신 자주색 티셔츠 콘텐츠를 열 수 있습니다.

프로세스는 다음과 같이 작동합니다.

1. Marketo 사용자는 푸시 메시지에 대한 탭 작업에 사용자 지정 URI를 배치합니다.
1. 사용자가 장치에서 푸시 메시지를 탭하면 Marketo MME SDK이 사용자 지정 URI로 이벤트를 트리거합니다.
1. 앱에서 이벤트를 처리하고 사용자를 해당 콘텐츠로 안내합니다.

이 프로세스를 활성화하려면

1. 앱에 대한 사용자 지정 URI 구조를 정의합니다.
1. 앱 매니페스트에서 스키마를 등록합니다.
1. 딥링크 이벤트를 처리하고 사용자를 해당 콘텐츠로 라우팅하는 코드를 추가합니다.

iOS의 경우 [앱에 대한 사용자 지정 URL 체계 정의](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)에서 Apple 설명서를 참조하십시오.

Android의 경우 [앱 컨텐츠에 대한 딥링크 사용](https://developer.android.com/training/app-links/deep-linking)에 대한 Google 설명서를 참조하십시오.

PhoneGap 앱의 경우 플러그인을 사용하여 하이브리드 앱이 iOS 및 Android에서 사용자 지정 URL 체계 및 범용/앱 링크에 응답할 수 있도록 합니다. 사용 가능한 [딥링크 플러그인](https://cordova.apache.org/plugins/?q=deeplink)을 확인하세요.

앱에서 딥링크를 활성화한 경우 푸시 메시지에 대한 탭 작업에 삽입할 수 있도록 사용자 지정 URI를 Marketo 사용자와 공유합니다.

Marketo은 테스트 장치를 설정할 때 사전 정의된 URI 구조를 사용합니다. 자세한 내용은 [설치 안내서](installation.md)의 &quot;테스트 장치&quot;를 참조하십시오.

## URI 구조 정의에 대한 우수 사례

브랜드에 모바일 사이트가 있는 경우 딥링크 URI를 정의할 때 해당 URL 구조를 따르십시오. 예를 들어 제품 URL이 `https://myappname.com/products/purple-shirt`인 경우 `myappname://products/purple-shirt`을(를) 해당 딥링크 URI로 사용합니다.

내 브랜드에 고유한 스키마를 사용합니다. 전역적으로 고유한 스키마를 요구하는 규정은 없지만 `org.companyname`과 같은 도메인 이름을 반대로 하여 고유한 스키마를 만드는 데 도움이 될 수 있습니다.
