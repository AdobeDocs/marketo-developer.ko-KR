---
title: PhoneGap
feature: Mobile Marketing
description: 모바일 장치에서 Marketo과 PhoneGap 사용
exl-id: 99f14c76-9438-4942-9309-643bca434d07
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# PhoneGap

Marketo PhoneGap 플러그인 통합

## 필요 조건

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)(응용 프로그램 비밀 키 및 Munchkin Id 얻기).
1. 푸시 알림 설정([iOS](push-notifications.md) | [Android](push-notifications.md)).
1. [PhoneGap/Cordova CLI를 설치합니다](https://cordova.apache.org/docs/en/latest/guide/cli/).

## 설치 지침

1. Marketo PhoneGap 플러그인 설정

   Cordova CLI가 설치되어 있다고 가정할 경우 PhoneGap 애플리케이션 디렉토리로 이동하고 다음 명령을 실행하여 Marketo 플러그인을 애플리케이션에 추가합니다.

   `$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. FCM 플러그인 설치

   `$ cordova plugin add cordova-plugin-fcm`

   플러그인이 애플리케이션에 추가되었는지 확인하려면 다음 명령을 실행하고 확인합니다

   `$ cordova plugin ls com.marketo.plugin 0.X.0 "MarketoPlugin" cordova-plugin-fcm 2.1.2 "FCMPlugin"`

**최신 버전으로 마이그레이션(선택 사항)**

기존 플러그인을 제거하려면 다음 명령을 실행합니다.

`$ cordova plugin remove com.marketo.plugin`

플러그인을 다시 추가하려면 다음 명령을 실행합니다.

`$ cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

**Cordova 버전 8.0.0(Cordova@Android7.0.0) 이상**

Cordova Android 플랫폼이 빌드되면 Android Studio로 앱을 열고 `com.marketo.plugin` 폴더에 있는 `Marketo.gradle` 파일의 `dirs` 값을 업데이트합니다.

```
repositories{    
  jcenter()
  flatDir{
      dirs '../app/src/main/aar'
   }
}
```

`$cordova platform add android` `$ cordova platform add ios` 앱에 대해 타깃팅할 플랫폼 추가

추가된 플랫폼 목록 `$cordova platform ls` 확인

1. Firebase 클라우드 메시징 지원

1. Firebase 콘솔에서 Firebase 앱을 구성합니다.
   1. [&#128279;](https://console.firebase.google.com/)Firebase 콘솔에서 프로젝트를 만들거나 추가합니다.
      1. [Firebase 콘솔](https://console.firebase.google.com/)에서 **[!UICONTROL Add Project]**&#x200B;을(를) 선택합니다.
      1. 기존 Google Cloud 프로젝트 목록에서 GCM 프로젝트를 선택하고 **[!UICONTROL Add Firebase]**&#x200B;을(를) 선택합니다.
      1. Firebase 시작 화면에서 &#39;Android 앱에 Firebase 추가&#39;를 선택합니다.
      1. 패키지 이름과 SHA-1을 입력하고 **[!UICONTROL Add App]**&#x200B;을(를) 선택하십시오. Firebase 앱에 대한 새 `google-services.json` 파일이 다운로드되었습니다.
   1. [!UICONTROL Project Overview]의 **[!UICONTROL Project Settings]**(으)로 이동
      1. **[!UICONTROL General]** 탭을 클릭합니다. &quot;google-services.json&quot; 파일을 다운로드합니다.
      1. **[!UICONTROL Cloud Messaging]** 탭을 클릭합니다. [!UICONTROL Server Key] 및 [!UICONTROL Sender ID]을(를) 복사합니다. 이 [!UICONTROL Server Key] 및 [!UICONTROL Sender ID]을(를) Marketo에 제공하십시오.
   1. Phonegap 앱에서 FCM 변경 사항 구성
      1. 다운로드한 &#39;google-services.json&#39; 파일을 Phonegap 앱 모듈 루트 디렉토리로 이동합니다
      1. `platforms/android/app/src/main/java/com/gae/scaffolder/plugin` 위치에서 &#39;MyFirebaseInstanceIDService&#39; 파일을 제거합니다(사용하지 않음).
      1. `platforms/android/app/src/main/java/com/gae/scaffolder/plugin` 위치의 &#39;MyFirebaseMessagingService&#39; 파일을 다음과 같이 수정합니다.

         ```
         import com.marketo.Marketo;
         
         public class MyFirebaseMessagingService extends FirebaseMessagingService{
         
         @Override
         public void onNewToken(String s){
           super.onNewToken(s);
           MarketoExtension.setPushNotificaitonTokens(s);
           //Add your code here
         }
         
         @Override
         public void onMessageReceived(RemoteMessage remoteMessage) {
           MarketoExtension.showPushNotificaiton(remoteMessage);
           //Add your code here
         }
         }
         ```

         1. 다음과 같이 plugins/cordova-plugin-fcm/scripts 위치에서 &#39;fcm_config_files_process.js&#39; 파일을 수정합니다

            ```
            //change
            var strings = fs.readFileSync("platforms/android/res/values/strings.xml").toString();
            //to
            var strings = fs.readFileSync("platforms/android/app/src/main/res/values/strings.xml").toString();
            
            //AND change
            fs.writeFileSync("platforms/android/res/values/strings.xml", strings);
            //to
            fs.writeFileSync("platforms/android/app/src/main/res/values/strings.xml", strings);
            ```


### 3. xCode에서 푸시 알림 활성화

xCode 프로젝트에서 푸시 알림 기능을 켭니다.

### 4. 푸시 알림 추적

`application:didFinishLaunchingWithOptions:` 함수 내에 다음 코드를 붙여넣습니다.

>[!BEGINTABS]

>[!TAB 목표 C]

아래와 같이 `applicationDidBecomeActive` 메서드 업데이트

```
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

아래와 같이 `applicationDidBecomeActive` 메서드 업데이트

```
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotification(launchOptions)
```

>[!ENDTABS]

### 5. Marketo 프레임워크 초기화

앱 시작 시 Marketo 프레임워크가 시작되도록 하려면 기본 JavaScript 파일의 `onDeviceReady` 함수 아래에 다음 코드를 추가하십시오.

PhoneGap 앱에 대한 프레임워크 유형으로 `phonegap`을(를) 전달해야 합니다.

### 구문

```
// This method will Initialize the Marketo Framework using Your MunchkinId and Secret Key
marketo.initialize(
  function() { console.log("MarketoSDK Init done."); },
  function(error) { console.log("an error occurred:" + error); },
  'YOUR_MUNCHKIN_ID',
  'YOUR_SECRET_KEY', 
  'FRAMEWORK_TYPE'
);

// For session tracking, add following. 
marketo.onStart(
  function(){ console.log("onStart."); },
  function(error){ console.log("Failed to report onStart." + error); }
);
```

### 매개 변수

- Success Callback : Marketo 프레임워크가 성공적으로 초기화된 경우 실행할 함수입니다.
- Failure Callback : Marketo 프레임워크를 초기화하지 못할 경우 실행할 함수입니다.
- MUNCHKIN ID : 등록 시 Marketo에서 받은 Munchkin ID입니다.
- 비밀 키 : 등록 시 Marketo에서 받은 비밀 키.

### 6. Marketo 푸시 알림 초기화

Marketo 푸시 알림이 시작되었는지 확인하려면 기본 JavaScript 파일에서 초기화 함수 뒤에 다음 코드를 추가합니다.

### 구문

```
// This function will Enable user notifications (prompts the user to accept push notifications in iOS)
marketo.initializeMarketoPush(
    function() { console.log("Marketo push successfully initialized."); },
    function(error) { console.log("an error occurred:" + error); },
    'YOUR_GCM_PROJECT_ID' // This is required for Android and will be ignored in iOS
);
```

### 매개 변수

- Success Callback : Marketo 푸시 알림이 성공적으로 초기화된 경우 실행되는 함수입니다.
- Failure Callback : Marketo 푸시 알림이 초기화되지 않는 경우 실행할 함수입니다.
- GCM_PROJECT_ID : 앱을 만든 후 [Google 개발자 콘솔](https://console.developers.google.com/)에서 GCM 프로젝트 ID를 찾았습니다.

로그아웃 시 토큰의 등록을 취소할 수도 있습니다.

```
marketo. uninitializeMarketoPush(
  function() { console.log("Marketo push successfully uninitialized."); } ,
  function(error) { console.log("an error occurred:" + error); }
);
```

## 리드 연결

associateLead 함수를 호출하여 Marketo Lead 를 생성할 수 있습니다.

### 구문

```
marketo.associateLead(
  function(){ console.log("MarketoSDK : Lead Added"); },
  function(error){ console.log("an error occurred:" + error); },
  'Lead_Data_JSON_String'
);
```

### 매개 변수

- Success Callback : Marketo 프레임워크가 리드를 성공적으로 연결하면 실행되는 함수입니다.
- Failure Callback : Marketo 프레임워크가 리드를 연결하지 못할 경우 실행할 함수입니다.
- 잠재 고객 데이터 : JSON 문자열 형식의 잠재 고객 데이터.

### 예

```
// First create a lead as shown below
var lead = {};
lead[marketo.KEY_FIRST_NAME] = "Phone";
lead[marketo.KEY_LAST_NAME] = "Gap";
lead[marketo.KEY_EMAIL] = email;
lead[marketo.KEY_ADDRESS] = "demo address";
lead[marketo.KEY_CITY] = "city";
lead[marketo.KEY_STATE] = "state";
lead[marketo.KEY_COUNTRY] = "country";
lead[marketo.KEY_POSTAL_CODE] = "postalCode";
lead[marketo.KEY_GENDER] = "gender";
// To use lead custom field, use the REST API NAME as key
lead["REST API NAME"] = "value";

// Use associateLead function to associate it.
marketo.associateLead(
  function() { console.log("MarketoSDK : Lead Associated"); },
  function(error) { console.log("an error occurred:" + error); },
  JSON.stringify(lead)
);
```

## 보고서 작업

`reportaction` 함수를 호출하여 사용자가 수행한 작업을 보고할 수 있습니다.

### 구문

```
marketo.reportaction(
  function(){ console.log("MarketoSDK : New event sent "); },
  function(error){ console.log("an error occurred:" + error); },
  'Action_Name',
  'Action_Data_JSON_String'
);
```

### 매개 변수

- 성공 콜백 : Marketo 프레임워크가 작업을 성공적으로 보고하면 실행할 함수입니다.
- 실패 콜백 : Marketo 프레임워크가 작업을 보고하지 못하는 경우 실행할 함수입니다.
- 작업 이름 : 작업 이름입니다.
- 작업 데이터 : JSON 문자열 형식의 작업 데이터.

### 예

```
// First create an event as below
var event = {
    "Action Type":"Add To Cart",
    "Action Details":"Adding Product in cart",
    "Action Metric":"10",
    "Action Length":"1"
}

marketo.reportaction(
    function(){ console.log("Reported action successfully."); },
    function(error){ console.log("Failed to report action." + error); },
    "Add To Cart",
    JSON.stringify(event)
);
```

## 세션 보고

아래 표시된 대로 &quot;일시 중지&quot; 및 &quot;다시 시작&quot; 이벤트 유형을 바인딩하여 시작 및 중지 이벤트를 보고합니다.  모바일 애플리케이션에서 보낸 시간을 추적하는 데 사용됩니다. 참고: Android에서 필수입니다.

```
//Add the following code in your www/js/index.js

bindEvents: function() {
   document.addEventListener('pause', this.onStop, false);
   document.addEventListener('resume', this.onStart, false);
},
onStop: function() {
   marketo.onStop(
       function(){ console.log("onStop"); },
       function(error){ console.log("Failed to report onStop." + error); }
   );
},
onStart: function() {
   marketo.onStart(
       function(){ console.log("onStart."); },
       function(error){console.log( "Failed to report onStart." + error); }
   );
},
```

## 리드 생성

하이브리드 앱에서 리드를 만드는 방법에는 세 가지가 있습니다.

1. MARKETO MME SDK
1. MARKETO REST API
1. 양식 제출

사용된 방법에 따라 새로 생성된 리드가 다른 트리거 및 필터에 의해 인식됩니다. MME SDK 또는 REST API를 사용하여 생성된 리드는 &quot;생성된 리드&quot; 트리거 및 필터에 표시됩니다. 양식 제출로 생성된 리드는 &quot;양식 작성&quot; 트리거 및 필터에 표시됩니다.

가장 좋은 방법은 리드를 만들 때 웹 앱에서 사용하는 방법과 일관되게 유지하는 것입니다. 양식 제출을 리드를 만드는 메커니즘으로 사용하는 웹 앱이 이미 있는 경우 하이브리드 앱에서 리드를 만들 때 동일한 메커니즘을 사용합니다. REST API를 리드 생성 메커니즘으로 사용하는 웹 앱이 이미 있는 경우 하이브리드 앱에서 리드를 생성할 때도 이와 동일한 메커니즘을 사용합니다. 양식 제출이나 REST API를 웹 앱에서 리드를 만드는 메커니즘으로 사용하지 않는 경우 MME SDK를 사용하여 Marketo에서 리드를 만드는 것이 좋습니다.
