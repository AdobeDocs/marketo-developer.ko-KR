---
title: '[!DNL Adobe Launch] 확장 설치'
feature: Mobile Marketing
description: '[!DNL Adobe Launch] 확장 설치 개요'
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# [!DNL Adobe Launch] 확장 설치

[!DNL Adobe Launch] Marketo 확장에 대한 설치 지침. 아래 단계는 푸시 알림 및/또는 인앱 메시지를 보내는 데 필요합니다.

## 전제 조건

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)(응용 프로그램 비밀 키 및 Munchkin ID 얻기)
1. [포털에서 속성 구성 [!DNL Adobe Launch] 포털](https://experience.adobe.com/#/@amc/data-collection/home)
1. [!DNL Adobe Launch] 포털에서 속성에 대한 응용 프로그램 비밀 키 및 Munchkin ID를 구성합니다.
1. [푸시 알림 설정](push-notifications.md)(선택 사항)

## iOS에 Marketo 확장 기능을 설치하는 방법

### Swift 브리징 헤더 설정

1. [!UICONTROL File] > [!UICONTROL New] > [!UICONTROL File](으)로 이동한 다음 **[!UICONTROL Header File]**&#x200B;을(를) 선택합니다.

1. 파일 이름을 &quot;&lt;_ProjectName_>-Bridging-Header&quot;로 지정합니다.

1. [!UICONTROL Project] > [!UICONTROL Target] > [!UICONTROL Build Settings] > [!UICONTROL Swift Compiler] > [!UICONTROL Code Generation](으)로 이동합니다. &quot;Objective-Bridging&quot; 헤더에 다음 경로를 추가합니다.

`$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## 확장 초기화

>[!BEGINTABS]

>[!TAB 목표 C]

아래와 같이 `applicationDidBecomeActive` 메서드 업데이트

```
(void)applicationDidBecomeActive:(UIApplication*) application
{
 [[ALMarketo sharedInstance] initializeMarketo:nil];
}
```

>[!TAB Swift]

아래와 같이 `applicationDidBecomeActive` 메서드 업데이트

```
func applicationDidBecomeActive(_ application: UIApplication)
{
 ALMarketo.sharedInstance().initializeMarketo(nil)
}
```

>[!ENDTABS]

## iOS 테스트 장치

1. **[!UICONTROL Project]** > **[!UICONTROL Target]** > **[!UICONTROL Info]** > **[!UICONTROL URL Types]**&#x200B;을(를) 선택합니다.
1. 식별자 추가: ${PRODUCT_NAME}
1. URL 체계 설정: mkto-&lt;S_ecret Key_>
1. `application:openURL:sourceApplication:annotation:` ~ `AppDelegate.m file` 포함(Objective-C)

### AppDelegate에서 사용자 지정 Url 유형 처리

>[!BEGINTABS]

>[!TAB 목표 C]

```
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

```
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return ALMarketo.sharedInstance().application(application, open: url, sourceApplication: nil, annotation: nil)
}
```

>[!ENDTABS]

## Android에 Marketo SDK를 설치하는 방법

### Android 확장 설정

[!DNL Adobe Launch] 포털의 지침 준수

### 권한 구성

`AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 이러한 권한을 요청하는 경우 이 단계를 건너뜁니다.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## 확장 초기화

ProGuard 구성(선택 사항)

앱에 ProGuard를 사용하는 경우 `proguard.cfg` 파일에 다음 줄을 추가합니다. 파일이 `project` 폴더 내에 있습니다. 이 코드를 추가하면 난독화 프로세스에서 Marketo SDK가 제외됩니다.

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

## Android  테스트  장치

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

Android용 MME SDK(Software Development Kit)가 Android 앱 개발자를 위한 보다 유연하고 새로운 엔지니어링 기능을 포함하는 보다 현대적이고 안정적이며 확장 가능한 프레임워크로 업데이트되었습니다.

이제 Android 앱 개발자는 이 SDK로 Google의 [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/)(FCM)을 직접 사용할 수 있습니다.

### 애플리케이션에 FCM 추가

1. Android 앱에서 최신 Marketo Android SDK를 통합합니다.  단계는 [GitHub](https://github.com/Marketo/android-sdk)에서 확인할 수 있습니다.
1. Firebase 콘솔에서 Firebase 앱을 구성합니다.
   1. [](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)Firebase 콘솔에서 프로젝트를 만들거나 추가합니다.
      1. [Firebase 콘솔](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)에서 **[!UICONTROL Add Project]**&#x200B;을(를) 선택합니다.
      1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 **[!UICONTROL Add Firebase]**&#x200B;을(를) 선택합니다.
      1. Firebase 시작 화면에서 **[!UICONTROL Add Firebase to your Android App]**&#x200B;을(를) 선택합니다.
      1. 패키지 이름과 SHA-1을 입력하고 **[!UICONTROL Add App]**&#x200B;을(를) 선택하십시오. Firebase 앱에 대한 새 `google-services.json` 파일이 다운로드되었습니다.
      1. **[!UICONTROL Continue]**&#x200B;을(를) 선택하고 Android Studio에서 Google 서비스 플러그인을 추가하는 자세한 지침을 따릅니다.

   1. [!UICONTROL Project Overview]의 **[!UICONTROL Project Settings]**(으)로 이동
      1. **[!UICONTROL General]** 탭을 클릭합니다. `google-services.json` 파일을 다운로드합니다.
      1. **[!UICONTROL Cloud Messaging]** 탭을 클릭합니다. [!UICONTROL Server Key] 및 [!UICONTROL Sender ID]을(를) 복사합니다. 이 [!UICONTROL Server Key] 및 [!UICONTROL Sender ID]을(를) Marketo에 제공하십시오.
   1. Android 앱에서 FCM 변경 사항 구성
      1. Android Studio의 프로젝트 보기로 전환하여 프로젝트 루트 디렉터리를 확인합니다.
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

         1. 마지막으로 ID에 나타나는 막대에서 **[!UICONTROL Sync now]**&#x200B;을(를) 클릭합니다
   1. 앱의 매니페스트 편집 FCM SDK는 필요한 모든 권한과 필요한 수신기 기능을 자동으로 추가합니다. 앱 매니페스트에서 다음 사용되지 않거나 메시지 중복을 일으킬 수 있으므로 유해할 수 있는 요소를 제거해야 합니다.

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

Firebase 클라우드 메시징 지원에 대한 FAQ입니다.

**Q: MME SDK의 최신 버전으로 업데이트하는 지침은 어디에서 찾을 수 있습니까?** 지침은 Marketo 개발자 사이트 [여기](installation.md)에서 찾을 수 있습니다.

**Q: 최신 버전의 SDK로 업데이트하려면 기존 사용자에게 업데이트된 버전의 Android 애플리케이션을 게시해야 합니까?** 아니요.

**Q: Marketo Android SDK와 통합된 Android 앱을 게시한 기존 MME 고객에게 어떤 영향을 미칩니까?** 다음과 같이 Android의 기존 GCM 클라이언트 앱을 Firebase Cloud Messaging(FCM)으로 마이그레이션할 수 있습니다.

1. [Firebase 콘솔](https://accounts.google.com/ServiceLogin?passive=1209600&amp;osid=1&amp;continue=https://console.firebase.google.com/&amp;followup=https://console.firebase.google.com/)에서 **[!UICONTROL Add Project]**&#x200B;을(를) 선택합니다.
1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 **[!UICONTROL Add Firebase]**&#x200B;을(를) 선택합니다.
1. Firebase 시작 화면에서 **[!UICONTROL Add Firebase to your Android App]**&#x200B;을(를) 선택합니다.
1. 패키지 이름과 SHA-1을 입력하고 **[!UICONTROL Add App]**&#x200B;을(를) 선택하십시오. 에 대한 새 google-services.json 파일
1. Firebase 앱이 다운로드되었습니다.
1. **[!UICONTROL Continue]**&#x200B;을(를) 선택하고 Android Studio에서 Google 서비스 플러그인을 추가하는 자세한 지침을 따릅니다.

**Q: GCM 앱을 사용한 이전 Marketo SDK를 사용하여 만든 잠재 고객을 타깃팅할 수 있습니까?** 예. Marketo SDK를 사용하여 만든 모든 리드를 푸시 알림 전송 대상으로 지정할 수 있습니다.
