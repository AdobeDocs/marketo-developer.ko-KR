---
title: "Marketo 모바일 확장 [!DNL Adobe Launch]"
feature: Mobile Marketing
description: "Marketo 모바일 확장 [!DNL Adobe Launch] 개요"
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 용 Marketo Mobile 확장 [!DNL Adobe Launch]

에서 Marketo Mobile SDK 확장에 대한 설치 지침 [!DNL Adobe Launch]. 아래 단계는 푸시 알림 및/또는 인앱 메시지를 보내는 데 필요합니다.

## 필요 조건

- [Marketo Admin에서 애플리케이션 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) (애플리케이션 암호 키 및 Munchkin Id 얻기)
- 에 제공된 지침을 따르십시오. [!DNL Adobe Launch] 설치를 위한 포털
- [푸시 알림 설정](push-notifications.md) (선택 사항)

## iOS

### Swift 브리징 헤더 설정

1. 파일 > 새로 만들기 > 파일로 이동하고 &quot;헤더 파일&quot;을 선택합니다.
1. 파일 이름을 &quot;&lt;_프로젝트 이름_>-Bridging-Header&quot;.
1. 프로젝트 > Target > 빌드 단계 > Swift 컴파일러 > 코드 생성으로 이동합니다. Objective-Bridging 헤더에 다음 경로를 추가합니다.

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

Swift 사용자의 경우: 위의 단계에서 브리징 헤더가 추가되므로 다음 가져오기 구문을 제거합니다.

`import Marketo/ALMarketo`

### iOS 테스트 장치

다음 지시 사항을 따르십시오. [iOS 테스트 장치 추가](installation.md#ios_test_devices)

### AppDelegate에서 사용자 지정 Url 유형 처리

지침 준수 [여기](installation.md#ios_test_devices)

### iOS에서 푸시 알림 설정

지침 준수 [여기](push-notifications.md) 및 에는 &quot;Marketo&quot; 대신 &quot;ALMarketo&quot;라는 클래스 이름을 사용하십시오.

## Android

### 권한 구성

열기 `AndroidManifest.xml` 및 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 이러한 권한을 요청하는 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard 구성(선택 사항)

앱에 ProGuard를 사용하는 경우 다음 줄을 추가합니다 `proguard.cfg` 파일. 파일은 프로젝트 폴더 내에 있습니다. 이 코드를 추가하면 난독화 프로세스에서 Marketo SDK가 제외됩니다.

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android 테스트 장치

지침 준수 [여기](installation.md#android_test_devices)

## Android에서 푸시 알림 설정

지침 준수 [여기](installation.md#android_firebase_cloud_messaging_support) 및 에는 &quot;Marketo&quot; 대신 &quot;ALMarketo&quot;라는 클래스 이름을 사용하십시오.

사용자 프로필 설정의 경우 다음 지침을 따르십시오 [여기](user-profiles.md) 사용자 지정 작업의 경우 지침을 따르십시오 [여기](custom-actions.md#android_custom_action). 다음 지침에서는 &quot;Marketo&quot; 대신 &quot;ALMarketo&quot; 클래스 이름을 사용합니다.
