---
title: "딥 링크 활성화"
feature: "Mobile Marketing"
description: "딥 링크 활성화 지침"
source-git-commit: cb000968c78e062b3c17be7d0faa6236c73e7358
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 딥링크 활성화

딥링크를 사용하면 사람을 앱 내의 특정 콘텐츠(리소스)로 리디렉션할 수 있습니다. 예를 들어 사용자가 자주색 티셔츠를 광고하는 모바일 푸시 메시지를 클릭하면 앱이 바로 자주색 티셔츠 콘텐츠(홈 페이지가 아님)로 열릴 수 있습니다.

프로세스는 다음과 같이 작동합니다.

1. Marketo 사용자는 푸시 메시지에 대한 탭 작업에 사용자 지정 URI를 배치합니다.
1. 사용자가 장치에서 푸시 메시지를 탭하면 Marketo MME SDK가 사용자 지정 URI로 이벤트를 트리거합니다.
1. 그런 다음 앱에서 이벤트를 처리하고 사용자를 앱 내의 적절한 콘텐츠로 리디렉션합니다.

이렇게 하려면 앱에 대한 사용자 지정 URI 구조를 정의하고, 앱의 매니페스트 내에서 스키마를 등록한 다음 딥링크 이벤트를 처리하고 앱의 적절한 위치로 라우팅하는 코드를 추가해야 합니다.

iOS의 경우 다음에 대한 Apple 설명서를 참조하십시오. [앱에 대한 사용자 지정 URL 체계 정의](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app).

Android의 경우 다음에 대한 Google 설명서 를 참조하십시오. [앱 컨텐츠에 대한 딥링크 활성화](https://developer.android.com/training/app-links/deep-linking).

PhoneGap 앱의 경우 딥링크가 기본 iOS 또는 Android 앱만큼 바로 연결되지 않지만, 하이브리드 앱이 iOS 및 Android 모두에서 딥링크 사용자 지정 URL 체계 및 범용/앱 링크에 응답할 수 있도록 하는 플러그인이 있습니다. 고려 [이러한 플러그인](https://cordova.apache.org/plugins/?q=deeplink).

앱에서 딥링크를 활성화한 경우 푸시 메시지에 대한 탭 작업에 삽입할 수 있도록 사용자 지정 URI를 Marketo 사용자와 공유합니다.

Marketo은 테스트 장치를 설정할 때 사전 정의된 URI 구조를 사용합니다. 의 &quot;테스트 장치&quot; 섹션을 참조하십시오. [설치 안내서](installation.md) 추가 정보.

## URI 구조 정의에 대한 우수 사례

브랜드에 기존 모바일 사이트가 있는 경우, 가장 좋은 방법은 딥링크 URI에 대한 URL 구조를 따라가는 것입니다. 예를 들어 다음과 같습니다. `https://myappname.com/products/purple-shirt` 해당 제품의 웹 사이트 주소입니다. `myappname://products/purple-shirt` 는 앱에서 사용하기에 좋은 딥링크 URI 구조입니다.

일반적으로 귀하의 계획은 귀하의 브랜드에 고유해야 합니다. 현재 전 세계적으로 스키마를 고유하게 만드는 규정은 없지만 스키마가 고유한지 확인할 수 있는 한 가지 방법은 도메인 이름(예: `org.companyname`).
