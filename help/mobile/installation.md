---
title: 설치
feature: Mobile Marketing
description: 푸시 및 인앱 메시지를 활성화하면서 CocoaPods, Swift Package Manager 또는 Gradle을 사용하여 iOS 및 Android에서 Marketo Mobile SDK을 설치하고 초기화하는 방법에 대해 안내합니다.
exl-id: e0b79d85-3509-46d2-a77d-cee211c5ec7f
TQID: https://experienceleague.adobe.com/zYNoGPwJTQnqmP6CH0NDbmb-b8vAKRScMmms6vy0Sb4
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 765
ht-degree: 0%

---

# 설치

Marketo Mobile SDK을 설치 및 초기화하여 푸시 알림, 인앱 메시지 또는 둘 다를 전송합니다.

## iOS에 Marketo SDK 설치

### 사전 요구 사항

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.
1. 선택 사항: [푸시 알림 설정](push-notifications.md).

### CocoaPod를 통해 프레임워크 설치

1. CocoaPod를 설치합니다. `$ sudo gem install cocoapods`
1. 디렉터리를 프로젝트 디렉터리로 변경하고 스마트 기본값으로 Podfile을 만듭니다. `$ pod init`
1. Podfile을 엽니다. `$ open -a Xcode Podfile`
1. Podfile에 다음 줄을 추가합니다. `$ pod 'Marketo-iOS-SDK'`
1. Podfile을 저장하고 닫습니다.
1. Marketo iOS SDK을 다운로드하여 설치합니다. `$ pod install`
1. Xcode에서 작업 영역을 엽니다. `$ open App.xcworkspace`

### Swift 패키지 관리자를 사용하여 프레임워크 설치

1. 프로젝트 탐색기에서 프로젝트를 선택합니다. &quot;패키지 종속성 추가&quot;에서 &#39;+&#39;를 선택합니다.

   ![종속성 추가](assets/dependency-manager-add.png)

1. <https://github.com/Marketo/ios-sdk>에서 Marketo 패키지를 추가합니다.

   ![저장소 URL](assets/dependency-manager-url.png)

1. 리소스 번들을 추가합니다. Project Navigator에서 `MarketoFramework.XCframework`을(를) 찾아 Finder에서 엽니다. `MKTResources.bundle`을(를) 끌어 번들 리소스를 복사합니다.

### Swift 브리징 헤더 설정

1. 파일 > 새로 만들기 > 파일로 이동하고 &quot;헤더 파일&quot;을 선택합니다.

   ![헤더 파일 선택](assets/choose-header-file.png)

1. 파일 이름을 &quot;&lt;_ProjectName_>-Bridging-Header&quot;로 지정합니다.

1. 프로젝트 > Target > 빌드 단계 > Swift 컴파일러 > 코드 생성으로 이동합니다. Objective-Bridging 헤더에 다음 경로를 추가합니다.

   `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

   ![빌드 단계](assets/build-phases.png)

## SDK 초기화

Munchkin 계정 ID 및 앱 비밀 키로 Marketo iOS SDK을 초기화합니다. Marketo 관리자의 &quot;모바일 앱 및 장치&quot;에서 두 값을 모두 찾습니다.

1. Objective-C에 대한 AppDelegate.m 파일 또는 Swift에 대한 브리징 파일을 엽니다. Marketo.h 헤더 파일을 가져옵니다.

   ```
   #import <MarketoFramework/MarketoFramework.h>
   ```

1. `application:didFinishLaunchingWithOptions` 내에 다음 코드를 붙여넣습니다. 함수.

   기본 앱의 프레임워크 유형으로 &quot;native&quot;를 전달합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance initializeWithMunchkinID:@"munchkinAccountId" appSecret:@"secretKey" mobileFrameworkType:@"native" launchOptions:launchOptions];
```

>[!TAB Swift]

```swift
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.initialize(withMunchkinID: "munchkinAccountId", appSecret: "secretKey", mobileFrameworkType: "native", launchOptions: launchOptions)
```

>[!ENDTABS]

1. `munkinAccountId` 및 `secretKey`을(를) Marketo **[!UICONTROL Admin]** > **[!UICONTROL Mobile Apps and Devices]**&#x200B;에서 &quot;Munchkin 계정 ID&quot; 및 &quot;비밀 키&quot;로 바꾸십시오.

## iOS 테스트 장치

1. [프로젝트] > [Target] > [정보] > [URL 유형]을 선택합니다.
1. 식별자 ${PRODUCT_NAME}을(를) 추가합니다.
1. URL 체계를 `mkto-<Secret Key_>`(으)로 설정합니다.
1. Objective-C에 대한 AppDelegate.m 파일에 application:openURL:sourceApplication:annotation:을(를) 추가합니다.

## AppDelegate에서 사용자 지정 Url 유형 처리

>[!BEGINTABS]

>[!TAB 목표 C]

```objectivec
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{

    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];
}
```

>[!TAB Swift]

```swift
private func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool
    {
        return Marketo.sharedInstance().application(app, open: url, options: options)
    }
```

>[!ENDTABS]

## Android에 Marketo SDK을 설치하는 방법

### 사전 요구 사항

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.
1. 선택 사항: [푸시 알림 설정](push-notifications.md#android_setup_push).
1. [Android용 Marketo SDK 다운로드](https://codeload.github.com/Marketo/android-sdk/zip/refs/heads/master)

### Gradle로 Android SDK 설정

1. 애플리케이션 수준의 build.gradle 파일에서 dependencies 섹션 아래에 종속성을 추가합니다.

   `implementation 'com.marketo:MarketoSDK:0.8.9'`

1. 루트 `build.gradle` 파일에 다음 구성을 추가하십시오.

   ```
   buildscript {
       repositories {
           google()
           mavenCentral()
       }
   ```

1. 프로젝트를 Gradle 파일과 동기화합니다.

### 권한 구성

`AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 요청한 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### SDK 초기화

1. Application 또는 Activity 클래스를 엽니다. setContentView 전 또는 애플리케이션 컨텍스트에서 Marketo SDK을 활동으로 가져옵니다.

   ```java
   // Initialize Marketo
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   marketoSdk.initializeSDK("native","munchkinAccountId","secretKey");
   ```

1. ProGuard 구성(선택 사항)

   앱에서 ProGuard를 사용하는 경우 프로젝트 폴더의 `proguard.cfg` 파일에 다음 줄을 추가합니다. 이 구성에서는 Marketo SDK이 난독화에서 제외됩니다.

   ```
   -dontwarn com.marketo.*
   -dontnote com.marketo.*
   -keep class com.marketo.`{ *; }
   ```

## Android 테스트 장치

응용 프로그램 태그 내의 `AndroidManifest.xml`에 &quot;MarketoActivity&quot;를 추가합니다.

```xml
<activity android:name="com.marketo.MarketoActivity"  android:configChanges="orientation|screenSize" >
    <intent-filter android:label="MarketoActivity" >
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto" />
    </intent-filter>
</activity>
```

## Firebase 클라우드 메시징 지원

Android용 MME SDK은 Google의 [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/)&#x200B;(FCM)을 직접 사용할 수 있도록 지원합니다.

### 애플리케이션에 FCM 추가

1. 최신 Marketo Android SDK을 Android 앱에 통합합니다. [GitHub](https://github.com/Marketo/android-sdk)의 단계를 참조하세요.
1. Firebase 콘솔에서 Firebase 앱을 구성합니다.
   1. [&#128279;](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase 콘솔에서 프로젝트를 만들거나 추가합니다.
      1. [Firebase 콘솔](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)에서 `Add Project`을(를) 선택합니다.
      1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 `Add Firebase`을(를) 선택합니다.
      1. Firebase 시작 화면에서 `Add Firebase to your Android App`을(를) 선택합니다.
      1. 패키지 이름과 SHA-1을 입력하고 `Add App`을(를) 선택하십시오. Firebase 앱에 대한 새 `google-services.json` 파일이 다운로드되었습니다.
      1. `Continue`을(를) 선택하고 Android Studio에서 Google 서비스 플러그인을 추가하는 자세한 지침을 따릅니다.

   1. 프로젝트 개요에서 &#39;프로젝트 설정&#39;으로 이동
      1. &#39;일반&#39; 탭을 클릭합니다. &quot;google-services.json&quot; 파일을 다운로드합니다.
      1. &#39;클라우드 메시징&#39; 탭을 클릭합니다. &#39;서버 키&#39; 및 &#39;보낸 사람 ID&#39;를 복사합니다. Marketo에 이러한 &#39;서버 키&#39; 및 &#39;보낸 사람 ID&#39;를 제공하십시오.
   1. Android 앱에서 FCM을 구성합니다.
      1. Android Studio의 프로젝트 보기로 전환하여 프로젝트 루트 디렉터리를 확인합니다.
         1. 다운로드한 &#39;google-services.json&#39; 파일을 Android 앱 모듈 루트 디렉토리로 이동합니다
         1. 프로젝트 수준 build.gradle에서 다음을 추가합니다.

            ```
            buildscript {
              dependencies {
                classpath 'com.google.gms:google-services:4.0.0'
              }
            }
            ```

         1. 앱 수준 build.gradle에서 다음을 추가합니다.

            ```
            dependencies {
              compile 'com.google.firebase:firebase-core:17.4.0'
            }
            // Add to the bottom of the file
            apply plugin: 'com.google.gms.google-services'
            ```

         1. 마지막으로 ID에 나타나는 막대에서 **[!UICONTROL Sync now]**&#x200B;을(를) 선택합니다
   1. 앱 매니페스트를 편집합니다. FCM SDK은 필요한 권한 및 수신자 기능을 자동으로 추가합니다. 메시지가 중복될 수 있는 다음 오래된 요소를 제거합니다.

      ```xml
      <uses-permission android:name="android.permission.WAKE_LOCK" />
      <permission android:name="<your-package-name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
      <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
      
      ...
      
      <receiver>
        android:name="com.google.android.gms.gcm.GcmReceiver"
        android:exported="true"
        android:permission="com.google.android.c2dm.permission.SEND"
        <intent-filter>
          <action android:name="com.google.android.c2dm.intent.RECEIVE" />
          <category android:name="<your-package-name> />
        </intent-filter>
      </receiver>
      ```
