---
title: '[!DNL Adobe Launch] 확장 설치'
feature: Mobile Marketing
description: 모바일용 Adobe Launch Marketo 확장 설치 푸시 및 인앱에 대해 iOS 및 Android 설정, 테스트 장치, 권한 및 FCM 단계를 따릅니다.
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
TQID: https://experienceleague.adobe.com/UZRHaRBISIZsE6E25Ee7CnnYwyZwi6w2YgOQJ-JL00U
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 696
ht-degree: 1%

---

# [!DNL Adobe Launch] 확장 설치

푸시 알림, 인앱 메시지 또는 둘 다를 전송하려면 [!DNL Adobe Launch] Marketo 확장을 설치하십시오.

## 필요 조건

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.
1. [ [!DNL Adobe Launch] 포털](https://experience.adobe.com/#/@amc/data-collection/home)에서 속성을 구성하십시오.
1. [!DNL Adobe Launch] 포털에서 속성에 대한 응용 프로그램 암호 키 및 Munchkin ID를 구성합니다.
1. 선택 사항: [푸시 알림 설정](push-notifications.md).

## iOS에 Marketo 확장 기능을 설치하는 방법

### Swift 브리징 헤더 설정

1. [!UICONTROL File] > [!UICONTROL New] > [!UICONTROL File]&#x200B;(으)로 이동한 다음 **[!UICONTROL Header File]**&#x200B;을(를) 선택합니다.

1. 파일 이름을 &quot;&lt;_ProjectName_>-Bridging-Header&quot;로 지정합니다.

1. [!UICONTROL Project] > [!UICONTROL Target] > [!UICONTROL Build Settings] > [!UICONTROL Swift Compiler] > [!UICONTROL Code Generation]&#x200B;(으)로 이동합니다.
1. &quot;Objective-Bridging&quot; 헤더에 다음 경로를 추가합니다.

`$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## 확장 초기화

>[!BEGINTABS]

>[!TAB 목표 C]

`applicationDidBecomeActive` 메서드를 다음과 같이 업데이트합니다.

```objectivec
(void)applicationDidBecomeActive:(UIApplication*) application
{
 [[ALMarketo sharedInstance] initializeMarketo:nil];
}
```

>[!TAB Swift]

`applicationDidBecomeActive` 메서드를 다음과 같이 업데이트합니다.

```objectivec
func applicationDidBecomeActive(_ application: UIApplication)
{
 ALMarketo.sharedInstance().initializeMarketo(nil)
}
```

>[!ENDTABS]

## iOS 테스트 장치

1. **[!UICONTROL Project]** > **[!UICONTROL Target]** > **[!UICONTROL Info]** > **[!UICONTROL URL Types]**&#x200B;을(를) 선택합니다.
1. 식별자 ${PRODUCT_NAME}을(를) 추가합니다.
1. URL 체계를 mkto-&lt;S_ecret Key_>로 설정합니다.
1. Objective-C에 대해 `AppDelegate.m file`에 `application:openURL:sourceApplication:annotation:`을(를) 추가합니다.

### AppDelegate에서 사용자 지정 Url 유형 처리

>[!BEGINTABS]

>[!TAB 목표 C]

```objectivec
#ifdef __IPHONE_10_0
-(BOOL)application:(UIApplication *)application
           openURL:(NSURL *)url
           options:(NSDictionary *)options{
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}
#endif

- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication
         annotation:(id)annotation {
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}
```

>[!TAB Swift]

```objectivec
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return ALMarketo.sharedInstance().application(application, open: url, sourceApplication: nil, annotation: nil)
}
```

>[!ENDTABS]

## Android에 Marketo SDK을 설치하는 방법

### Android 확장 설정

[!DNL Adobe Launch] 포털의 지침을 따르십시오.

### 권한 구성

`AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 요청한 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 확장 초기화

ProGuard 구성(선택 사항)

앱에서 ProGuard를 사용하는 경우 `project` 폴더의 `proguard.cfg` 파일에 다음 줄을 추가하십시오. 이 구성에서는 Marketo SDK이 난독화에서 제외됩니다.

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
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
   1. [](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase 콘솔에서 프로젝트를 만들거나 추가합니다.
      1. [Firebase 콘솔](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)에서 **[!UICONTROL Add Project]**&#x200B;을(를) 선택합니다.
      1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 **[!UICONTROL Add Firebase]**&#x200B;을(를) 선택합니다.
      1. Firebase 시작 화면에서 **[!UICONTROL Add Firebase to your Android App]**&#x200B;을(를) 선택합니다.
      1. 패키지 이름과 SHA-1을 입력하고 **[!UICONTROL Add App]**&#x200B;을(를) 선택하십시오. Firebase 앱에 대한 새 `google-services.json` 파일이 다운로드되었습니다.
      1. **[!UICONTROL Continue]**&#x200B;을(를) 선택하고 Android Studio에서 Google 서비스 플러그인을 추가하는 자세한 지침을 따릅니다.

   1. [!UICONTROL Project Overview]의 **[!UICONTROL Project Settings]**(으)로 이동합니다.
      1. **[!UICONTROL General]** 탭을 선택하고 `google-services.json`을(를) 다운로드합니다.
      1. **[!UICONTROL Cloud Messaging]** 탭을 선택합니다. [!UICONTROL Server Key] 및 [!UICONTROL Sender ID]을(를) 복사하여 Marketo에 제공합니다.
   1. Android 앱에서 FCM을 구성합니다.
      1. Android Studio의 프로젝트 보기로 전환하여 프로젝트 루트 디렉터리를 표시합니다.
         1. 다운로드한 `google-services.json` 파일을 Android 앱 모듈 루트 디렉터리로 이동합니다.
         1. 프로젝트 수준 `build.gradle`에서 다음을 추가하십시오.

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

         1. IDE에 나타나는 막대에서 **[!UICONTROL Sync now]**&#x200B;을(를) 선택합니다.
   1. 앱 매니페스트를 편집합니다. FCM SDK은 필요한 권한 및 수신자 기능을 자동으로 추가합니다. 메시지가 중복될 수 있는 다음 오래된 요소를 제거합니다.

      ```xml
      <uses-permission android:name="android.permission.WAKE_LOCK" />
      <permission android:name="<your-package-name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
      <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
      
      ...
      
      <receiver>
        android:name="com.google.android.gms.gcm.GcmReceiver"
        android:exported="true"
        android:permission="com.google.android.c2dm.permission.SEND">
        <intent-filter>
          <action android:name="com.google.android.c2dm.intent.RECEIVE" />
          <category android:name="<your-package-name> />
        </intent-filter>
      </receiver>
      ```

### FCM FAQ

이러한 질문에는 Firebase Cloud Messaging 지원이 포함됩니다.

**Q: MME SDK 최신 버전으로 업데이트하는 지침은 어디에서 찾을 수 있습니까?** Marketo 개발자 사이트에서 [설치 지침](installation.md)을 참조하십시오.

**Q: 최신 버전의 SDK으로 업데이트하려면 기존 사용자에게 업데이트된 버전의 Android 애플리케이션을 게시해야 합니까?** 아니요.

**Q: Marketo Android SDK을 사용하는 게시된 Android 앱을 사용하는 기존 MME 고객에게 어떤 영향을 미칩니까?** 기존 Android GCM 클라이언트 앱을 다음과 같이 Firebase Cloud Messaging(FCM)으로 마이그레이션합니다.

1. [Firebase 콘솔](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)에서 **[!UICONTROL Add Project]**&#x200B;을(를) 선택합니다.
1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 **[!UICONTROL Add Firebase]**&#x200B;을(를) 선택합니다.
1. Firebase 시작 화면에서 **[!UICONTROL Add Firebase to your Android App]**&#x200B;을(를) 선택합니다.
1. 패키지 이름과 SHA-1을 입력하고 **[!UICONTROL Add App]**&#x200B;을(를) 선택하십시오. Firebase 앱용 새 google-services.json 파일이 다운로드됩니다.
1. **[!UICONTROL Continue]**&#x200B;을(를) 선택하고 Android Studio에서 Google 서비스 플러그인을 추가하는 자세한 지침을 따릅니다.

**Q: GCM 앱을 사용한 이전 Marketo SDK으로 만들어진 리드를 타깃팅할 수 있습니까?** 예. 푸시 알림을 위해 Marketo SDK으로 생성된 모든 리드를 타깃팅할 수 있습니다.
