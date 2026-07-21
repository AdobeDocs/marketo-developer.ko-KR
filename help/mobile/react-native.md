---
title: React Native
feature: Mobile Marketing
description: Android Gradle 및 iOS CocoaPods 단계, 기본 모듈 브리징, 푸시 및 리드 연결이 있는 React Native 앱에 Marketo SDK을 설치하고 설정합니다.
exl-id: 462fd32e-91f1-4582-93f2-9efe4d4761ff
TQID: https://experienceleague.adobe.com/SPuVFgs5Z-H6f6VYORxyqAVjwTXI-ZHI-q123FU1SLg
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 580
ht-degree: 1%

---

# React Native

Marketo 기본 SDK을 설치 및 구성하여 React Native 모바일 앱을 Marketo과 통합합니다.

## 필요 조건

[Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)하고 응용 프로그램 비밀 키 및 Munchkin ID를 가져옵니다.

## SDK 통합

### Android SDK 통합

**Gradle을 사용하여 설정**

응용 프로그램 수준 `build.gradle` 파일의 종속성 섹션 아래에 최신 Marketo SDK 종속성을 추가하십시오. 적절한 SDK 버전을 포함합니다.

```groovy
implementation 'com.marketo:MarketoSDK:0.x.x'
```

**mavencentral 저장소 추가**

Marketo SDK은 [Maven 중앙 저장소](https://mvnrepository.com/)에서 사용할 수 있습니다. `mavencentral` 리포지토리를 루트 `build.gradle` 파일에 추가합니다.

```groovy
build script {
  repositories {
    google()
    mavencentral()
  }
}
```

프로젝트를 Gradle 파일과 동기화합니다.

#### iOS SDK 통합

React Native 프로젝트에 대한 브리지를 만들기 전에 Xcode 프로젝트에서 SDK을 설정하십시오.

**SDK 통합 - CocoaPod 사용**

[CocoaPods](https://cocoapods.org/)을(를) 사용하여 앱의 Xcode 프로젝트에 iOS SDK을 추가하십시오. CocoaPods는 Objective-C 및 Swift의 Ruby 종속성 관리자입니다.

1. CocoaPod를 설치합니다.

`$ sudo gem install cocoapods`

1. ReactNative 프로젝트의 iOS 폴더에서 Podfile을 엽니다.

`$ open -a Xcode Podfile`

1. Podfile에 다음 줄을 추가합니다.

`$ pod 'Marketo-iOS-SDK'`

1. Podfile을 저장하고 닫습니다.

1. Marketo iOS SDK을 다운로드하여 설치합니다.

`$ pod install`

1. Xcode에서 작업 영역을 엽니다.

`$ open App.xcworkspace`

## 기본 모듈 설치 지침

React Native 앱이 JavaScript에 노출되지 않는 플랫폼 API 또는 기본 라이브러리에 액세스해야 하는 경우 기본 모듈을 사용합니다. NativeModule 시스템은 Java, Objective-C 또는 C++ 클래스를 JavaScript 개체로 노출합니다.

React Native 브리지는 JSX와 기본 앱 레이어를 연결합니다. 호스트 앱은 JSX 코드를 사용하여 이 브리지를 통해 Marketo SDK 메서드를 호출할 수 있습니다.

### Android

제공된 매개 변수를 사용하여 Marketo SDK을 호출하는 래퍼 메서드가 포함된 파일을 만듭니다.

```java
public class RNMarketoModule extends ReactContextBaseJavaModule {

   final Marketo marketoSdk;
   RNMarketoModule(ReactApplicationContext context) {
       super(context);
       marketoSdk = Marketo.getInstance(context);
   }

   @NonNull
   @Override
   public String getName() {
       return "RNMarketoModule";
   }

   @ReactMethod
   public void associateLead(ReadableMap leadData) {

       MarketoLead mLead = new MarketoLead();
       try {
           mLead.setCity(leadData.getString(MarketoLead.KEY_CITY));
           mLead.setFirstName(leadData.getString(MarketoLead.KEY_FIRST_NAME));
           mLead.setLastName(leadData.getString(MarketoLead.KEY_LAST_NAME));
           mLead.setAddress(leadData.getString(MarketoLead.KEY_ADDRESS));
           mLead.setEmail(leadData.getString(MarketoLead.KEY_EMAIL));
           mLead.setBirthDay(leadData.getString(MarketoLead.KEY_BIRTHDAY));
           mLead.setCountry(leadData.getString(MarketoLead.KEY_COUNTRY));
           mLead.setFacebookId(leadData.getString(MarketoLead.KEY_FACEBOOK));
           mLead.setGender(leadData.getString(MarketoLead.KEY_GENDER));
           mLead.setState(leadData.getString(MarketoLead.KEY_STATE));
           mLead.setPostalCode(leadData.getString(MarketoLead.KEY_POSTAL_CODE));
           mLead.setTwitterId(leadData.getString(MarketoLead.KEY_TWITTER));
           marketoSdk.associateLead(mLead);
       }
       catch (MktoException e){
       }
   }
   @ReactMethod
   public void setSecureSignature(ReadableMap readableMap) {
       MarketoConfig.SecureMode secureMode = new MarketoConfig.SecureMode();
       secureMode.setAccessKey(readableMap.getString("accessKey"));
       secureMode.setEmail(readableMap.getString("email"));
       secureMode.setSignature(readableMap.getString("signature"));
       secureMode.setTimestamp(readableMap.getInt("timeStamp"));
       marketoSdk.setSecureSignature(secureMode);
   }
   @ReactMethod
      public void initializeSDK(String frameworkType, String munchkinId, String appSecreteKey){
          marketoSdk.initializeSDK(munchkinId,appSecreteKey,frameworkType);
    }


   @ReactMethod
   public void initializeMarketoPush(String projectId){
       marketoSdk.initializeMarketoPush( projectId);
   }

   @ReactMethod
   public void initializeMarketoPush(String projectId, String channelName){
       marketoSdk.initializeMarketoPush( projectId, channelName);
   }

   @ReactMethod
   public void uninitializeMarketoPush(){
       marketoSdk.uninitializeMarketoPush();
   }

   @ReactMethod
   public void reportAction(String action){
       Marketo.reportAction(action, null);
   }

   @ReactMethod
   public void reportAction(String action, ReadableMap readableMap){
       MarketoActionMetaData marketoActionMetaData = new MarketoActionMetaData();
       marketoActionMetaData.setActionDetails(readableMap.getString("setMetric"));
       marketoActionMetaData.setActionMetric(readableMap.getString("setLength"));
       marketoActionMetaData.setActionLength(readableMap.getString("actionDetails"));
       marketoActionMetaData.setActionType(readableMap.getString("actionType"));
       Marketo.reportAction(action, marketoActionMetaData);
   }
}
```

**패키지 등록**

React Native에 Marketo 패키지를 등록합니다.

```java
public class MarketoPluginPackage implements ReactPackage {

   @NonNull
   @Override
   public List createNativeModules(@NonNull ReactApplicationContext reactContext) {
           List modules = new ArrayList<>();

           modules.add(new RNMarketoModule(reactContext));

           return modules;
   }

   @NonNull
   @Override
   public List createViewManagers(@NonNull ReactApplicationContext reactContext) {
       return Collections.emptyList();
   }
}
```

MarketoPluginPackage 를 애플리케이션 클래스의 React 패키지 목록에 추가합니다.

```java
public class MainApplication extends Application implements ReactApplication {

  private final ReactNativeHost mReactNativeHost =
      new ReactNativeHost(this) {
        @Override
        public boolean getUseDeveloperSupport() {
          return BuildConfig.DEBUG;
        }

        @Override
        protected List getPackages() {
          @SuppressWarnings("UnnecessaryLocalVariable")
          List packages = new PackageList(this).getPackages();
          packages.add(new MarketoPluginPackage());     //Add the Marketo Package here.
          // Packages that cannot be autolinked yet can be added manually here, for example:
          return packages;
        }
}
```

### iOS

JavaScript에서 Marketo API에 액세스하려면 기본 모듈 _RNMarketoModule_&#x200B;을(를) 만드십시오.

Xcode에서 React Native 애플리케이션용 iOS 프로젝트를 엽니다. Xcode를 사용하여 네이티브 코드를 작성하고 구문 오류를 식별합니다.

사용자 지정 기본 모듈 헤더 및 구현 파일을 만듭니다. `MktoBridge.h`을(를) 만들고 다음 콘텐츠를 추가합니다.

```objectivec
//
//  MktoBridge.h
//
//  Created by Marketo, An Adobe company.
//

#import <Foundation/Foundation.h>
#import <React/RCTBridgeModule.h>

NS_ASSUME_NONNULL_BEGIN

@interface MktoBridge : NSObject

@end

NS_ASSUME_NONNULL_END
```

같은 폴더에 `MktoBridge.m`을(를) 만들고 다음 콘텐츠를 추가합니다.

```objectivec
//
//  MktoBridge.h
//  Created by Marketo, An Adobe company.
//

#import <Foundation/Foundation.h>
#import <React/RCTBridgeModule.h>

NS_ASSUME_NONNULL_BEGIN

@interface MktoBridge : NSObject <RCTBridgeModule>

@end

NS_ASSUME_NONNULL_END


//
//  MktoBridge.m
//  Created by Marketo, An Adobe company.
//

#import "MktoBridge.h"
#import <MarketoFramework/Marketo.h>
#import <React/RCTBridge.h>
#import "ConstantStringsHeader.h"

@implementation MktoBridge

RCT_EXPORT_MODULE(RNMarketoModule);

+(BOOL)requiresMainQueueSetup{
  return NO;
}

RCT_EXPORT_METHOD(initializeSDK:(NSString *) munchkinId SecretKey: (NSString *) secretKey andFrameworkType: (NSString *) frameworkType){
  [[Marketo sharedInstance] initializeWithMunchkinID:munchkinId appSecret:secretKey mobileFrameworkType:frameworkType launchOptions:nil];
}

RCT_EXPORT_METHOD(reportAction:(NSString *)actionName withMetaData:(NSDictionary *)metaData){
  MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
  [meta setType:[metaData objectForKey:KEY_ACTION_TYPE]];
  [meta setDetails:[metaData objectForKey:KEY_ACTION_DETAILS]];
  [meta setLength:[metaData valueForKey:KEY_ACTION_LENGTH]];
  [meta setMetric:[metaData valueForKey:KEY_ACTION_METRIC]];
  [[Marketo sharedInstance] reportAction:actionName withMetaData:meta];
}

RCT_EXPORT_METHOD(associateLead:(NSDictionary *)leadDetails){
  MarketoLead *lead = [[MarketoLead alloc] init];
  if ([leadDetails objectForKey:KEY_EMAIL] != nil) {
    [lead setEmail:[leadDetails objectForKey:KEY_EMAIL]];
  }
  if ([leadDetails objectForKey:KEY_FIRST_NAME] != nil) {
    [lead setFirstName:[leadDetails objectForKey:KEY_FIRST_NAME]];
  }

  if ([leadDetails objectForKey:KEY_LAST_NAME] != nil) {
    [lead setLastName:[leadDetails objectForKey:KEY_LAST_NAME]];
  }

  if ([leadDetails objectForKey:KEY_CITY] != nil) {
    [lead setCity:[leadDetails objectForKey:KEY_CITY]];
  }
    [[Marketo sharedInstance] associateLead:lead];
}

RCT_EXPORT_METHOD(uninitializeMarketoPush){
  [[Marketo sharedInstance] unregisterPushDeviceToken];
}

RCT_EXPORT_METHOD(reportAll){
  [[Marketo sharedInstance] reportAll];
}

RCT_EXPORT_METHOD(setSecureSignature:(NSDictionary *)secureSignature){
  MKTSecuritySignature *secSignature = [[MKTSecuritySignature alloc]
                                        initWithAccessKey:[secureSignature objectForKey:KEY_ACCESSKEY]
                                        signature:[secureSignature objectForKey:KEY_SIGNATURE]
                                        timestamp: [secureSignature objectForKey:KEY_EMAIL]
                                        email:[secureSignature objectForKey:KEY_EMAIL]];

    [[Marketo sharedInstance] setSecureSignature:secSignature];
}

RCT_EXPORT_METHOD(requestPermission:(RCTPromiseResolveBlock)resolve rejecter:(RCTPromiseRejectBlock)reject) {
  UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
  [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert + UNAuthorizationOptionSound + UNAuthorizationOptionBadge)
                        completionHandler:^(BOOL granted, NSError * _Nullable error) {
    if (error) {
      reject(@"PERMISSION_ERROR", @"Permission request failed", error);
    } else {
      resolve(@(granted));
    }
  }];
}

RCT_EXPORT_METHOD(registerForRemoteNotifications) {
  dispatch_async(dispatch_get_main_queue(), ^{
    [[UIApplication sharedApplication] registerForRemoteNotifications];
  });
}


@end
```

#### Marketo SDK 초기화

네이티브 모듈의 createCalendarEvent() 메서드에 대한 호출을 추가합니다. 다음 예제에서는 NewModuleButton 구성 요소를 추가하고 onPress() 함수에서 네이티브 모듈을 호출합니다.

```javascript
import React from 'react';
import { NativeModules, Button } from 'react-native';

const NewModuleButton = () => {
  const onPress = () => {
    console.log('We will invoke the native module here!');
  };

  return (

  );
  };

export default NewModuleButton;
```

기본 모듈을 JavaScript 레이어에 로드합니다.

```javascript
import React from 'react';
import {Node} from 'react';
import { NativeModules } from 'react-native';

const { RNMarketoModule } = NativeModules;
```

파일을 배치한 후 JavaScript 모듈을 JavaScript 클래스로 가져오고 해당 메서드를 직접 호출합니다.

React Native 앱에 대한 프레임워크 유형으로 &quot;reactNative&quot;를 전달합니다.

```javascript
// Initialize marketo SDK with Munchkin & Seretkey you have from step 1.
RNMarketoModule.initializeSDK("MunchkinID","SecreteKEY","FrameworkType")

//You can create a Marketo Lead by calling the associateLead function.
RNMarketoModule.associateLead({ email: "", firstName: "", lastName:"", city:""})

//You can report any user performed action by calling the reportaction function.
RNMarketoModule.reportAction("Bought Shirt", {actionType:"Shopping", actionDetails: "Red Shirt", setLength : 20, setMetric : 30 })

//You can set Secure Signature by calling this method.
RNMarketoModule.setSecureSignature({accessKey: "Key102", email: "testleadrk@001.com", signature : "asdfghjkloiuytds", timeStamp: "12345678987654"})

//This function will Enable user notifications (Only Android)
RNMarketoModule.initializeMarketoPush("350312872033", "MKTO")

//The token can also be unregistered on logout.
RNMarketoModule.uninitializeMarketoPush()
```

#### 푸시 알림 구성

프로젝트 ID 및 채널 이름으로 푸시 알림을 초기화합니다.

```javascript
RNMarketoModule.initializeMarketoPush("ProjectId", "Channel_name")
```

`AndroidManifest.xml`에 다음 서비스를 추가하십시오.

```xml
<service android:exported="true" android:name=".MyFirebaseMessagingService" android:stopWithTask="true">
    <intent-filter>
        <action  android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter/>
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT"/>
    </intent-filter/>
</activity/>
```

이름이 `FirebaseMessagingService.java`인 클래스를 만들고 다음 코드를 추가합니다.

```java
import com.google.firebase.messaging.FirebaseMessagingService;
import com.google.firebase.messaging.RemoteMessage;
import com.marketo.Marketo;

public class MyFirebaseMessagingService extends FirebaseMessagingService {

   @Override
   public void onNewToken(String token) {
       super.onNewToken(token);
       Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
       marketoSdk.setPushNotificationToken(token);
   }

   @Override
   public void onMessageReceived(RemoteMessage remoteMessage) {
       Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
       marketoSdk.showPushNotification(remoteMessage);
   }
}
```

Xcode 프로젝트에서 사용자의 장치로 푸시 알림을 전송할 권한을 활성화합니다.

푸시 알림을 보내려면 [푸시 알림을 추가](push-notifications.md)하세요.

iOS 푸시 알림을 설정하려면 PushNotifications.tsx를 만들고 다음 코드를 추가합니다.

```javascript
import { NativeModules } from 'react-native';
const { RNMarketoModule } = NativeModules;

const requestPermission = (): Promise<boolean> => {
return RNMarketoModule.requestPermission()
.then((granted: boolean) => {
console.log('Permission granted:', granted);
return granted;
})
.catch((error: any) => {
console.error('Permission error:', error);
throw error;
});
};

const registerForRemoteNotifications = (): void => {
RNMarketoModule.registerForRemoteNotifications();
};

export { requestPermission, registerForRemoteNotifications };
```

푸시 알림을 허용하려면 `App.tsx`에 다음 코드를 추가하십시오.

```javascript
import React, { useEffect } from 'react';

useEffect(() => {
requestPermission().then(granted => {
if (granted) {
registerForRemoteNotifications();
}
});
}, []);
```

APNS 위임 메서드로 `AppDelegate.mm`을(를) 업데이트합니다.

```objectivec
#import "AppDelegate.h"
#import "MktoBridge.h"
#import <MarketoFramework/Marketo.h>
#import <React/RCTBundleURLProvider.h>

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  self.moduleName = @"MyNewApp";
  // You can add your custom initial props in the dictionary below.
  // They will be passed down to the ViewController used by React Native.
  self.initialProps = @{};

  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (NSURL *)sourceURLForBridge:(RCTBridge *)bridge
{
  return [self bundleURL];
}

-(void)userNotificationCenter:(UNUserNotificationCenter *)center
      willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
    completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}

- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void(^)(void))completionHandler {
    [[Marketo sharedInstance] userNotificationCenter:center
                      didReceiveNotificationResponse:response
                               withCompletionHandler:completionHandler];
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // Register the push token with Marketo
    [[Marketo sharedInstance] registerPushDeviceToken:deviceToken];
}

- (void)applicationWillTerminate:(UIApplication *)application {
    [[Marketo sharedInstance] unregisterPushDeviceToken];
}

-(void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error{
  NSLog(@"Failed to register for remote notification - %@", [error userInfo]);
}

- (NSURL *)bundleURL
{
#if DEBUG
  return [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index"];
#else
  return [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
#endif
}

@end
```

### 테스트 장치 추가

**Android**

응용 프로그램 태그 내의 `AndroidManifest.xml`에 &quot;MarketoActivity&quot;를 추가합니다.

```xml
<activity android:name="com.marketo.MarketoActivity" android:configChanges="orientation|screenSize" android:exported="true">
    <intent-filter android:label="MarketoActivity">
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto"/>
    </intent-filter/>
</activity/>
```

**iOS**

1. [프로젝트] > [Target] > [정보] > [URL 유형]을 선택합니다.

1. 식별자 ${PRODUCT_NAME}을(를) 추가합니다.

1. URL 체계를 `mkto-<S_ecret Key_>`(으)로 설정합니다.

1. Objective-C에 대한 `AppDelegate.m` 파일에 `application:openURL:sourceApplication:annotation:`을(를) 추가합니다.

**iOS - AppDelegate에서 사용자 지정 Url 형식/딥링크 처리**

```objectivec
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary *)options{

    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];
}
```

상수 파일을 만들고 JavaScript API 호출에 대해 다음 상수를 추가합니다.

```objectivec
// Lead attributes.
static NSString *const KEY_FIRST_NAME = @"firstName";
static NSString *const KEY_LAST_NAME = @"lastName";
static NSString *const KEY_ADDRESS = @"address";
static NSString *const KEY_CITY = @"city";
static NSString *const KEY_STATE = @"state";
static NSString *const KEY_COUNTRY = @"country";
static NSString *const KEY_GENDER = @"gender";
static NSString *const KEY_EMAIL = @"email";
static NSString *const KEY_TWITTER = @"twitterId";
static NSString *const KEY_FACEBOOK = @"facebookId";
static NSString *const KEY_LINKEDIN = @"linkedinId";
static NSString *const KEY_LEAD_SOURCE = @"leadSource";
static NSString *const KEY_BIRTHDAY = @"dateOfBirth";
static NSString *const KEY_FACEBOOK_PROFILE_URL = @"facebookProfileURL";
static NSString *const KEY_FACEBOOK_PROFILE_PIC = @"facebookPhotoURL";

// Custom actions
static NSString *const KEY_ACTION_TYPE = @"actionType";
static NSString *const KEY_ACTION_DETAILS = @"actionDetails";
static NSString *const KEY_ACTION_LENGTH = @"setLength";
static NSString *const KEY_ACTION_METRIC = @"setMetric";

//Secure Signature
static NSString *const KEY_ACCESSKEY = @"accessKey";
static NSString *const KEY_SIGNATURE = @"signature";
static NSString *const KEY_TIMESTAMP = @"timeStamp";
```

다음 예제와 같이 상수를 사용합니다.

```javascript
//You can create a Marketo Lead by calling the associateLead function.
RNMarketoModule.associateLead({ email: "", firstName: "", lastName:"", city:""})
```
