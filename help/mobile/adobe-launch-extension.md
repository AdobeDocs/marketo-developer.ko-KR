---
title: ' [!DNL Adobe Launch]용 Marketo Mobile 확장'
feature: Mobile Marketing
description: 푸시 알림 및 인앱 메시지 설정을 포함하여 iOS 및 Android용 Adobe Launch에 Marketo Mobile SDK 확장 기능을 설치 및 구성합니다.
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
TQID: https://experienceleague.adobe.com/Bk5GTnQjm6NDosl5Iw6TS-NRjH8owNRUKoE0mZ-H3pY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 0%

---

# [!DNL Adobe Launch]용 Marketo Mobile 확장

푸시 알림, 인앱 메시지 또는 둘 다를 전송하려면 [!DNL Adobe Launch]에 Marketo Mobile SDK 확장을 설치하십시오.

## 필요 조건

- [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.
- [!DNL Adobe Launch] 포털의 설치 지침을 따르십시오.
- 선택 사항: [푸시 알림 설정](push-notifications.md).

## iOS

### Swift 브리징 헤더 설정

1. 파일 > 새로 만들기 > 파일로 이동하고 &quot;헤더 파일&quot;을 선택합니다.
1. 파일 이름을 &quot;&lt;_ProjectName_>-Bridging-Header&quot;로 지정합니다.
1. 프로젝트 > Target > 빌드 단계 > Swift 컴파일러 > 코드 생성으로 이동합니다.
1. Objective-Bridging 헤더에 다음 경로를 추가합니다.

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift의 경우 이전 단계에서 브리징 헤더를 추가하므로 다음 가져오기 구문을 제거합니다.

`import Marketo/ALMarketo`

### iOS 테스트 장치

[iOS 테스트 장치 추가](installation.md#ios_test_devices)의 지침을 따릅니다.

### AppDelegate에서 사용자 지정 Url 유형 처리

[사용자 지정 URL 지침](installation.md#ios_test_devices)을 따르십시오.

### iOS에서 푸시 알림 설정

[푸시 알림 지침](push-notifications.md)을 따르십시오. &quot;Marketo&quot; 대신 &quot;ALMarketo&quot; 클래스 이름을 사용하십시오.

## Android

### 권한 구성

`AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 요청한 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 구성(선택 사항)

앱에서 ProGuard를 사용하는 경우 프로젝트 폴더의 `proguard.cfg` 파일에 다음 줄을 추가합니다. 이 구성에서는 Marketo SDK이 난독화에서 제외됩니다.

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android 테스트 장치

[Android 테스트 장치](installation.md#android_test_devices)의 지침을 따르십시오.

## Android에서 푸시 알림 설정

[Android Firebase Cloud Messaging 지침](installation.md#android_firebase_cloud_messaging_support)을 따르십시오. &quot;Marketo&quot; 대신 &quot;ALMarketo&quot; 클래스 이름을 사용하십시오.

사용자 프로필을 설정하려면 [사용자 프로필 지침](user-profiles.md)을 따르십시오. 사용자 지정 작업을 설정하려면 [사용자 지정 작업 지침](custom-actions.md#android_custom_action)을 따르십시오. 두 지침 세트에서 모두 &quot;Marketo&quot; 대신 &quot;ALMarketo&quot; 클래스 이름을 사용합니다.
