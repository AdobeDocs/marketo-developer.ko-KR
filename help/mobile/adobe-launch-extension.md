---
title: ' [!DNL Adobe Launch]용 Marketo Mobile 확장'
feature: Mobile Marketing
description: 푸시 알림 및 인앱 메시지 설정을 포함하여 iOS 및 Android용 Adobe Launch에 Marketo Mobile SDK 확장 기능을 설치 및 구성합니다.
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# [!DNL Adobe Launch]용 Marketo Mobile 확장

[!DNL Adobe Launch]의 Marketo Mobile SDK 확장 설치 지침입니다. 아래 단계는 푸시 알림 및/또는 인앱 메시지를 보내는 데 필요합니다.

## 사전 요구 사항

- [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)&#x200B;(응용 프로그램 비밀 키 및 Munchkin ID 얻기)
- 설치를 위해 [!DNL Adobe Launch] 포털에 제공된 지침을 따르십시오.
- [푸시 알림 설정](push-notifications.md)(선택 사항)

## iOS

### Swift 브리징 헤더 설정

1. 파일 > 새로 만들기 > 파일로 이동하고 &quot;헤더 파일&quot;을 선택합니다.
1. 파일 이름을 &quot;&lt;_ProjectName_>-Bridging-Header&quot;로 지정합니다.
1. 프로젝트 > Target > 빌드 단계 > Swift 컴파일러 > 코드 생성으로 이동합니다. Objective-Bridging 헤더에 다음 경로를 추가합니다.

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift 사용자의 경우: 위의 단계에서 브리징 헤더가 추가되므로 다음 가져오기 구문을 제거합니다.

`import Marketo/ALMarketo`

### iOS 테스트 장치

[iOS 테스트 장치 추가](installation.md#ios_test_devices)의 지침을 따르십시오.

### AppDelegate에서 사용자 지정 Url 유형 처리

지침 [여기](installation.md#ios_test_devices) 준수

### iOS에서 푸시 알림 설정

지침 [여기](push-notifications.md)를 따르고 &quot;Marketo&quot; 대신 클래스 이름 &quot;ALMarketo&quot;를 사용하십시오.

## Android

### 권한 구성

`AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 이러한 권한을 요청하는 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 구성(선택 사항)

앱에 ProGuard를 사용하는 경우 `proguard.cfg` 파일에 다음 줄을 추가합니다. 파일은 프로젝트 폴더 내에 있습니다. 이 코드를 추가하면 난독화 프로세스에서 Marketo SDK이 제외됩니다.

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android 테스트 장치

지침 [여기](installation.md#android_test_devices) 준수

## Android에서 푸시 알림 설정

지침 [여기](installation.md#android_firebase_cloud_messaging_support)를 따르고 &quot;Marketo&quot; 대신 클래스 이름 &quot;ALMarketo&quot;를 사용하십시오.

사용자 프로필을 설정하려면 [여기](user-profiles.md)의 지침을 따르고 사용자 지정 작업에 대해서는 [여기](custom-actions.md#android_custom_action)의 지침을 따릅니다. 다음 지침에서는 &quot;Marketo&quot; 대신 &quot;ALMarketo&quot; 클래스 이름을 사용합니다.
