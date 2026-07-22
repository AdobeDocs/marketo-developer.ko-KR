---
title: '[!DNL Ionic]'
feature: Mobile Marketing
description: Marketo Cordova 플러그인을 Ionic과 통합하고, 푸시 알림을 활성화하고, SDK을 초기화하고, 세션을 추적하고, 리드를 연결하는 단계별 안내서입니다.
exl-id: 204e5fb4-c9d6-43a6-9d77-0b2a67ddbed3
TQID: https://experienceleague.adobe.com/UTNWd69NliR896RcO-XM2GG35liuLeNNhTXo9GRtB4o
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 581
ht-degree: 2%

---

# 이온-

Marketo Cordova 플러그인을 [!DNL Ionic] 앱과 통합합니다. [!DNL Ionic] 커패시터는 현재 지원되지 않습니다.

## 필요 조건

1. [Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.
1. [iOS](push-notifications.md) 또는 [Android](push-notifications.md)에 대한 푸시 알림을 설정합니다.
1. [[!DNL Ionic]](https://ionicframework.com/getting-started/) 및 [Cordova CLI](https://cordova.apache.org/docs/en/latest/guide/cli/)를 설치합니다.

## 설치 지침

### Marketo [!DNL Ionic] 플러그 인 설정

1. [!DNL Ionic] 응용 프로그램 디렉터리로 이동하고 다음 명령을 실행하여 Marketo 플러그인을 추가합니다.

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

1. 다음 명령을 실행하여 플러그인이 추가되었는지 확인합니다.

   `$ ionic plugin list com.marketo.plugin 0.X.0 "MarketoPlugin"`

### 최신 버전으로 마이그레이션(선택 사항)

1. 기존 플러그인을 제거하려면 다음 명령을 실행합니다.

   `$ ionic plugin remove com.marketo.plugin`

1. 플러그인을 다시 추가하려면 다음 명령을 실행합니다.

   `$ ionic plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"`

### xCode에서 푸시 알림 활성화

1. xCode 프로젝트에서 푸시 알림 기능을 켭니다.![알림 기능](assets/notification-capability.png)

### 푸시 알림 추적

`application:didFinishLaunchingWithOptions:` 함수 내에 다음 코드를 붙여넣습니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];

[sharedInstance trackPushNotification:launchOptions];
```

>[!TAB Swift]

```swift
let sharedInstance: Marketo = Marketo.sharedInstance()

sharedInstance.trackPushNotfication(launchOptions)
```

>[!ENDTABS]

### Marketo 프레임워크 초기화

앱이 시작될 때 Marketo 프레임워크를 초기화하려면 기본 JavaScript 파일의 `onDeviceReady` 함수 아래에 다음 코드를 추가하십시오.

[!DNL Ionic] Cordova 앱에 대한 프레임워크 유형으로 `ionicCordova`을(를) 전달합니다.

#### 구문

```javascript
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

#### 매개변수

- Success Callback: Marketo 프레임워크가 성공적으로 초기화된 경우 실행할 함수입니다.
- Failure Callback: Marketo 프레임워크를 초기화하지 못할 경우 실행할 함수입니다.
- MUNCHKIN ID: 등록하는 동안 Marketo에서 받은 Munchkin ID입니다.
- 비밀 키: 등록 중에 Marketo에서 받은 비밀 키.

### Marketo 푸시 알림 초기화

Marketo 푸시 알림을 초기화하려면 기본 JavaScript 파일에서 초기화 함수 뒤에 다음 코드를 추가합니다.

#### 구문

```javascript
// This function will Enable user notifications (prompts the user to accept push notifications in iOS)
marketo.initializeMarketoPush(
    function() { console.log("Marketo push successfully initialized."); },
    function(error) { console.log("an error occurred:" + error); },
    'YOUR_GCM_PROJECT_ID' // This is required for Android and will be ignored in iOS
);
```

#### 매개변수

- Success Callback: Marketo 푸시 알림이 성공적으로 초기화된 경우 실행할 함수입니다.
- Failure Callback: Marketo 푸시 알림이 초기화되지 않을 경우 실행할 함수입니다.
- GCM_PROJECT_ID: 앱을 만든 후 [Google 개발자 콘솔](https://accounts.google.com/ServiceLogin?service=cloudconsole&passive=1209600&osid=1&continue=https://console.cloud.google.com/apis/dashboard&followup=https://console.cloud.google.com/apis/dashboard)에서 찾은 GCM 프로젝트 ID입니다.

로그아웃 시 토큰 등록을 취소할 수도 있습니다.

```javascript
marketo.uninitializeMarketoPush(
  function() { console.log("Marketo push successfully uninitialized."); } ,
  function(error) { console.log("an error occurred:" + error); }
);
```

## 리드 연결

associateLead 함수를 호출하여 Marketo 리드를 만듭니다.

### 구문

```javascript
marketo.associateLead(
  function(){ console.log("MarketoSDK : Lead Added"); },
  function(error){ console.log("an error occurred:" + error); },
  'Lead_Data_JSON_String'
);
```

### 매개변수

- Success Callback: Marketo 프레임워크가 리드를 성공적으로 연결하면 실행되는 함수입니다.
- Failure Callback: Marketo 프레임워크가 리드를 연결하지 못하는 경우 실행할 함수입니다.
- 잠재 고객 데이터: JSON 문자열 형식의 잠재 고객 데이터.

### 예

```javascript
// First create a lead as shown below
var lead = {};
lead[marketo.KEY_FIRST_NAME] = "Ionic";
lead[marketo.KEY_LAST_NAME] = "App";
lead[marketo.KEY_EMAIL] = email;
lead[marketo.KEY_ADDRESS] = "demo address";
lead[marketo.KEY_CITY] = "city";
lead[marketo.KEY_STATE] = "state";
lead[marketo.KEY_COUNTRY] = "country";
lead[marketo.KEY_POSTAL_CODE] = "postalCode";
lead[marketo.KEY_GENDER] = "gender";

// Use associateLead function to associate it.
marketo.associateLead(
  function() { console.log("MarketoSDK : Lead Associated"); },
  function(error) { console.log("an error occurred:" + error); },
  JSON.stringify(lead)
);
```

## 보고서 작업

사용자 작업을 보고하려면 `reportaction` 함수를 호출하십시오.

### 구문

```javascript
marketo.reportaction(
  function(){ console.log("MarketoSDK : New event sent "); },
  function(error){ console.log("an error occurred:" + error); },
  'Action_Name',
  'Action_Data_JSON_String'
);
```

### 매개변수

- Success Callback: Marketo 프레임워크가 작업을 성공적으로 보고하면 실행되는 함수입니다.
- Failure Callback: Marketo 프레임워크가 작업을 보고하지 못하는 경우 실행할 함수입니다.
- 작업 이름: 작업 이름입니다.
- 작업 데이터: JSON 문자열 형식의 작업 데이터.

### 예

```javascript
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

&quot;pause&quot; 및 &quot;resume&quot; 이벤트 유형을 보고 시작 및 중지 이벤트에 바인딩합니다. 이러한 이벤트는 모바일 애플리케이션에서 사용한 시간을 추적하며 Android에서 필요합니다.

```javascript
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

새 리드를 인식하는 트리거와 필터는 만들기 방법에 따라 다릅니다.

- MME SDK 또는 REST API로 생성된 리드는 &quot;생성된 리드&quot; 트리거 및 필터에 표시됩니다.
- 양식 제출로 생성된 리드는 &quot;양식 작성&quot; 트리거 및 필터에 표시됩니다.

하이브리드 앱과 웹 앱에서 동일한 리드 생성 방법을 사용합니다. 웹 앱에서 양식 제출 또는 REST API를 사용하는 경우 하이브리드 앱에서 해당 메서드를 사용합니다. 웹 앱에서 두 방법 모두 사용하지 않는 경우 MME SDK을 사용하여 Marketo에서 리드를 만드는 것이 좋습니다.
