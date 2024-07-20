---
title: React Native
feature: Mobile Marketing
description: Marketo용 React Native 설치
exl-id: 462fd32e-91f1-4582-93f2-9efe4d4761ff
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# React Native

이 문서에서는 모바일 앱을 플랫폼과 통합하기 위해 Marketo의 기본 SDK를 설치하고 설정하는 방법에 대해 설명합니다.

## 필요 조건

[Marketo 관리자에서 응용 프로그램을 추가](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app)(응용 프로그램 비밀 키 및 Munchkin Id 얻기).

## SDK 통합

### Android SDK 통합

**Gradle을 사용하여 설정**

최신 버전으로 Marketo SDK 종속성을 추가합니다. 응용 프로그램 수준 `build.gradle` 파일의 종속성 섹션 아래에 (적절한 Marketo SDK 버전 포함)을 추가합니다.

```
implementation 'com.marketo:MarketoSDK:0.x.x'
```

**mavencentral 저장소 추가**

Marketo SDK는 [maven 중앙 저장소](https://mvnrepository.com/)에서 사용할 수 있습니다. 해당 파일을 동기화하려면 `mavencentral` 리포지토리를 `build.gradle` 루트에 추가하십시오.

```
build script {
  repositories {
    google()
    mavencentral()
  }
}
```

그런 다음 프로젝트를 Gradle 파일과 동기화합니다.

#### iOS SDK 통합

React Native 프로젝트에 대한 브리지를 만들기 전에 Xcode 프로젝트에서 SDK를 설정하는 것이 중요합니다.

**SDK 통합 - CocoaPod 사용**

앱에서 iOS SDK를 쉽게 사용할 수 있습니다. CocoaPods를 사용하여 앱의 Xcode 프로젝트에서 설정하려면 다음 단계를 수행하십시오. 당사의 플랫폼을 앱과 통합할 수 있습니다.

[CocoaPods](https://cocoapods.org/) 다운로드 - Ruby gem으로 배포되는 이 프로그램은 iOS SDK와 같은 코드에서 타사 라이브러리를 사용하는 프로세스를 간소화하는 Objective-C 및 Swift의 종속성 관리자입니다.

다운로드하고 설치하려면 Mac에서 명령줄 단말기를 시작하고 다음 명령을 실행합니다.

1. CocoaPod를 설치합니다.

`$ sudo gem install cocoapods`

1. Podfile을 엽니다. (ReactNative 프로젝트의 iOS 폴더 내)

`$ open -a Xcode Podfile`

1. Podfile에 다음 줄을 추가합니다.

`$ pod 'Marketo-iOS-SDK'`

1. Podfile을 저장하고 닫습니다.

1. Marketo iOS SDK를 다운로드하여 설치합니다.

`$ pod install`

1. Xcode에서 작업 영역을 엽니다.

`$ open App.xcworkspace`

## 기본 모듈 설치 지침

경우에 따라 React Native 앱은 JavaScript에서 기본적으로 사용할 수 없는 기본 플랫폼 API에 액세스해야 합니다(예: Apple 또는 Google 페이에 액세스하기 위한 기본 API). JavaScript에서 다시 구현하거나 이미지 처리와 같은 작업에 대해 고성능, 다중 스레드 코드를 작성하지 않고도 기존의 Objective-C, Swift, Java 또는 C++ 라이브러리를 재사용할 수 있습니다.

NativeModule 시스템은 Java/Objective-C/C++(네이티브) 클래스의 인스턴스를 JavaScript(JS)에 JS 개체로 노출하므로 JS 내에서 임의의 네이티브 코드를 실행할 수 있습니다. 이 기능이 일반적인 개발 프로세스의 일부가 될 것으로 예상하지는 않지만 반드시 있어야 합니다. React Native에서 JS 앱에 필요한 기본 API를 내보내지 않는 경우 직접 내보낼 수 있어야 합니다.

React Native 브리지는 JSX와 기본 앱 레이어 간의 통신에 사용됩니다. 이 경우 호스트 앱은 Marketo SDK의 메서드를 호출할 수 있는 JSX 코드를 작성할 수 있습니다.

### Android

이 파일에는 사용자가 제공하는 매개 변수를 사용하여 내부적으로 Marketo SDK의 메서드를 호출할 수 있는 래퍼 메서드가 포함되어 있습니다.

```
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
   public void initializeSDK(String munchkinId, String appSecreteKey){
       marketoSdk.initializeSDK(munchkinId,appSecreteKey);
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

React-native에 Marketo 패키지에 대해 알립니다.

```
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

패키지 등록을 완료하려면 MarketoPluginPackage를 응용 프로그램 클래스의 React 패키지 목록에 추가합니다.

```
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

다음 안내서에서는 JavaScript에서 Marketo의 API에 액세스할 수 있는 기본 모듈 _RNMarketoModule_&#x200B;을 만듭니다.

시작하려면 Xcode에서 React Native 애플리케이션 내에서 iOS 프로젝트를 엽니다. iOS 프로젝트는 React Native 앱 내에서 여기에서 찾을 수 있습니다. Xcode를 사용하여 네이티브 코드를 작성하는 것이 좋습니다. Xcode는 iOS 개발을 위해 빌드되었으며 이를 사용하면 코드 구문과 같은 사소한 오류를 빠르게 해결하는 데 도움이 됩니다.

기본 사용자 지정 기본 모듈 헤더 및 구현 파일을 만듭니다. `MktoBridge.h`(이)라는 새 파일을 만들고 다음 파일을 추가합니다.

```
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

동일한 폴더에 해당 구현 파일 MktoBridge.m을 만들고 다음 콘텐츠를 포함합니다.

```
//
//  MktoBridge.m
//
//  Created by Marketo, An Adobe company.
//

#import "MktoBridge.h"
#import <MarketoFramework/MarketoFramework.h>
#import <React/RCTBridge.h>
#import "ConstantStringsHeader.h"

@implementation MktoBridge

RCT_EXPORT_MODULE(RNMarketoModule);

+(BOOL)requiresMainQueueSetup{
  return NO;
}

RCT_EXPORT_METHOD(initializeWithMunchkin:(NSString *) munchkinId Secret: (NSString *) secretKey andFrameworkType : (NSString *) frameworkType{
  [[Marketo sharedInstance] initializeWithMunchkinID:munchkinId appSecret:secretKey  mobileFrameworkType:frameworktype launchOptions:nil];
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
@end
```

#### Marketo SDK 초기화

응용 프로그램에서 네이티브 모듈의 createCalendarEvent() 메서드에 대한 호출을 추가할 위치를 찾습니다. 다음은 앱에 추가할 수 있는 구성 요소 NewModuleButton의 예입니다. NewModuleButton의 onPress() 함수 내에서 네이티브 모듈을 호출할 수 있습니다.

```
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

이 JavaScript 파일은 기본 모듈을 JavaScript 레이어에 로드합니다.

```javascript
import React from 'react';
import {Node} from 'react';
import { NativeModules } from 'react-native';

const { RNMarketoModule } = NativeModules;
```

위의 파일을 올바르게 배치하면 모든 js 클래스에서 js 모듈을 가져와 해당 메서드를 직접 호출할 수 있습니다. For example:

React 네이티브 앱에 대한 프레임워크 유형으로 &quot;reactNative&quot;를 전달해야 합니다. 

```
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


프로젝트 ID 및 채널 이름으로 푸시 초기화

```
RNMarketoModule.initializeMarketoPush("ProjectId", "Channel_name")
```

`AndroidManifest.xml`에 다음 서비스 추가


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

사용자의 장치로 푸시 알림을 전송하려면 Xcode 프로젝트에서 권한을 활성화해야 합니다.

푸시 알림을 보내려면 [푸시 알림을 추가](push-notifications.md)하세요.

이제 XCode의 `AppDelegate.m` 파일에서 Marketo을 가져옵니다.

```
#import <MarketoFramework/MarketoFramework.h> 
```

대리자를 처리하려면 다음과 같이 AppDelegate 인터페이스에 `UNUserNotificationCenterDelegate`을(를) 추가하십시오.

```
@interface AppDelegate () <UNUserNotificationCenterDelegate>

@end
```

`didFinishLaunchingWithOptions` 메서드에서 원격 알림을 등록합니다.

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
#ifdef FB_SONARKIT_ENABLED
  InitializeFlipper(application);
#endif

  RCTBridge *bridge = [[RCTBridge alloc] initWithDelegate:self launchOptions:launchOptions];
  RCTRootView *rootView = [[RCTRootView alloc] initWithBridge:bridge
                                                   moduleName:@"HelloRN"
                                            initialProperties:nil];  
  
// asking user permission to send push notifications 
  [self registerForRemoteNotifications];
  
  self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
  UIViewController *rootViewController = [UIViewController new];
  rootViewController.view = rootView;
  self.window.rootViewController = rootViewController;
  [self.window makeKeyAndVisible];

  return YES;
}

- (void)registerForRemoteNotifications {
   UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge) completionHandler:^(BOOL granted, NSError * _Nullable error){
            if(!error){
                dispatch_async(dispatch_get_main_queue(), ^{
                    [[UIApplication sharedApplication] registerForRemoteNotifications];
                });
            }
            else{
                NSLog(@"failed");
            }
        }];
}
```

다음 `UNUserNotificationCenter`개의 대리자 필수 알림 위임 메서드를 포함합니다.

```
-(void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
    completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}

- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void(^)(void))completionHandler {
    [[Marketo sharedInstance] userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // Register the push token with Marketo
    [[Marketo sharedInstance] registerPushDeviceToken:deviceToken];
}

- (void)applicationWillTerminate:(UIApplication *)application {
    [[Marketo sharedInstance] unregisterPushDeviceToken];
}

-(void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error{
    NSLog(@"didFailToRegisterForRemoteNotificationsWithError");
}
```

### 테스트 장치 추가

**Android**

응용 프로그램 태그 내의 `AndroidManifest.xml` 파일에 &quot;MarketoActivity&quot;를 추가합니다.

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

1. 식별자 추가: ${PRODUCT_NAME}

1. URL 체계 설정: `mkto-<S_ecret Key_>`

1. `application:openURL:sourceApplication:annotation:`에서 `AppDelegate.m` 파일 포함(Objective-C)

**iOS - AppDelegate에서 사용자 지정 Url 형식/딥링크 처리** 

```
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary *)options{
   
    return [[Marketo sharedInstance] application:app
                                         openURL:url
                                         options:options];    
}
```

이러한 상수는 Javascript에서 API를 호출할 때 사용됩니다. 상수 파일을 만들고 다음을 추가해야 합니다.

```
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

사용 예

```
//You can create a Marketo Lead by calling the associateLead function.
RNMarketoModule.associateLead({ email: "", firstName: "", lastName:"", city:""})
```
