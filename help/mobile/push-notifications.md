---
title: 푸시 알림
feature: Mobile Marketing
description: Marketo Mobile용 푸시 알림 활성화
exl-id: 41d657d8-9eea-4314-ab24-fd4cb2be7f61
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# 푸시 알림

푸시 알림을 활성화하는 방법

## iOS에서 푸시 알림 설정

푸시 알림을 활성화하는 세 가지 단계가 있습니다.

1. Apple 개발자 계정에서 푸시 알림을 구성합니다.
1. xCode에서 푸시 알림을 활성화합니다.
1. Marketo SDK을 사용하여 앱에서 푸시 알림을 활성화합니다.

### Apple 개발자 계정에서 푸시 알림 구성

1. Apple 개발자 [구성원 센터](http://developer.apple.com/membercenter)에 로그인합니다.
1. 인증서, 식별자 및 프로필 을 클릭합니다.
1. &quot;iOS, tvOS, watchOS&quot; 아래의 &quot;Certificates->All&quot; 폴더를 클릭합니다.
1. 인증서 ![](assets/certificates-plus.png) 옆의 왼쪽 상단 화면에서 &quot;+&quot;를 선택합니다.
1. &quot;Apple 푸시 알림 서비스 SSL(샌드박스 및 프로덕션)&quot; 확인란을 활성화하고 &quot;계속&quot;을 클릭합니다.
1. 앱 빌드를 사용 중인 응용 프로그램 식별자를 선택합니다.![](assets/push-appid.png)
1. 푸시 인증서를 생성하려면 CSR을 만들고 업로드하십시오. ![](assets/push-ssl.png)
1. 로컬 컴퓨터에 인증서를 다운로드하고 두 번 클릭하여 설치합니다. ![](assets/certificate-download.png)
1. &quot;키체인 액세스&quot;를 열고 인증서를 마우스 오른쪽 단추로 클릭한 다음 2개의 항목을 `.p12` 파일로 내보냅니다.![key_chain](assets/key-chain.png)
1. Marketo Admin Console을 통해 이 파일을 업로드하여 알림을 구성합니다.
1. 앱 프로비저닝 프로필을 업데이트합니다.

### xCode에서 푸시 알림 활성화

xCode 프로젝트에서 푸시 알림 기능을 사용하도록 설정합니다.![](assets/push-xcode.png)

### Marketo SDK을 사용하여 앱에서 푸시 알림 활성화

`AppDelegate.m` 파일에 다음 코드를 추가하여 고객의 장치에 푸시 알림을 전달합니다.

**참고** - [!DNL Adobe Launch] 확장을 사용하는 경우 `ALMarketo`을(를) classname으로 사용

`AppDelegate.h`에서 다음을 가져옵니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
#import <UserNotifications/UserNotifications.h>
```

>[!TAB Swift]

```
import UserNotifications
```

>[!ENDTABS]

아래와 같이 `UNUserNotificationCenterDelegate`을(를) `AppDelegate`에 추가합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
@interface AppDelegate : UIResponder <UIApplicationDelegate, UNUserNotificationCenterDelegate>
```

>[!TAB Swift]

```
class AppDelegate: UIResponder, UIApplicationDelegate , UNUserNotificationCenterDelegate
```

>[!ENDTABS]

푸시 알림 서비스를 시작합니다. 푸시 알림을 활성화하려면 아래 코드를 추가하십시오.

>[!BEGINTABS]

>[!TAB 목표 C]

```objectivec
BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge) completionHandler:^(BOOL granted, NSError * _Nullable error){
            if(!error){
                dispatch_async(dispatch_get_main_queue(), ^{
                    [[UIApplication sharedApplication] registerForRemoteNotifications];
                });
            }
        }];

    return YES;
}
```

>[!TAB Swift]

```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound,    .badge]) { granted, error in
            if let error = error {
                print("\(error.localizedDescription)")
            } else {
                DispatchQueue.main.async {
                    application.registerForRemoteNotifications()
                }
            }
        }

        return true
}
```

>[!ENDTABS]

이 메서드를 호출하여 Apple Push Service로 등록 프로세스를 시작합니다. 등록이 성공하면 앱에서 앱 위임 개체의 `application:didRegisterForRemoteNotificationsWithDeviceToken:` 메서드를 호출하고 장치 토큰을 전달합니다.

등록이 실패하면 앱은 앱 위임자의 `application:didFailToRegisterForRemoteNotificationsWithError:` 메서드를 대신 호출합니다.

Marketo에 푸시 토큰 등록 Marketo에서 푸시 알림을 받으려면 Marketo에 장치 토큰을 등록해야 합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    // Register the push token with Marketo
    [[Marketo sharedInstance] registerPushDeviceToken:deviceToken];
}
```

>[!TAB Swift]

```
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    // Register the push token with Marketo
    Marketo.sharedInstance().registerPushDeviceToken(deviceToken)
}
```

>[!ENDTABS]

사용자가 로그아웃할 때 토큰의 등록을 취소할 수도 있습니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
[[Marketo sharedInstance] unregisterPushDeviceToken];
```

>[!TAB Swift]

```
Marketo.sharedInstance().unregisterPushDeviceToken
```

>[!ENDTABS]

푸시 토큰을 다시 등록하려면 3단계의 코드를 AppDelegate 메서드에 추출하고 ViewController 로그인 메서드에서 를 호출합니다.

푸시 알림을 처리합니다. Marketo에서 푸시 알림을 받으려면 Marketo에 장치 토큰을 등록해야 합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [[Marketo sharedInstance] handlePushNotification:userInfo];
}
```

>[!TAB Swift]

```
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
    Marketo.sharedInstance().handlePushNotification(userInfo)
}
```

>[!ENDTABS]

AppDelegate에 다음 메서드 추가

이 방법을 사용하면 앱이 포그라운드에 있는 동안 경고, 사운드를 제공하거나 배지를 늘릴 수 있습니다. 이 메서드에서 선택한 completionHandler를 호출해야 합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
-(void)userNotificationCenter:(UNUserNotificationCenter *)center
    willPresentNotification:(UNNotification *)notification
        withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{

    completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}
```

>[!TAB Swift]

```
func userNotificationCenter(_ center: UNUserNotificationCenter,
            willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (
    UNNotificationPresentationOptions) -> Void) {
    completionHandler([.alert, .sound,.badge])
}
```

>[!ENDTABS]

AppDelegate에서 새로 받은 푸시 알림 처리

사용자가 애플리케이션을 열거나 알림을 무시하거나 UNNotificationAction을 선택하여 알림에 응답하면 대리자에 대해 메서드가 호출됩니다. 응용 프로그램이 applicationDidFinishLaunch에서 반환되기 전에 대리자를 설정해야 합니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler {
    [[Marketo sharedInstance] userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
}
```

>[!TAB Swift]

```
func userNotificationCenter(_ center: UNUserNotificationCenter,
                                didReceive response: UNNotificationResponse,
                                withCompletionHandler
                                completionHandler: @escaping () -> Void) {
        Marketo.sharedInstance().userNotificationCenter(center, didReceive: response, withCompletionHandler: completionHandler)
}
```

>[!ENDTABS]

푸시 알림 추적

앱이 백그라운드에서 실행 중이거나 활성화되어 있지 않은 경우, 디바이스는 아래와 같이 푸시 알림을 수신합니다. Marketo은 사용자가 알림을 탭할 때를 추적합니다.

![mobile8](assets/mobile8.png)

장치가 푸시 알림을 받으면 앱 대리자의 `application:didReceiveRemoteNotification:` 콜백으로 전달됩니다.

다음은 앱 이벤트와 푸시 알림 이벤트를 보여 주는 Marketo의 Marketo 활동 로그입니다.

![mobile9](assets/mobile9.png)

## Android에서 푸시 알림 설정

1. 애플리케이션 태그 내에 다음 권한을 추가합니다.

   `AndroidManifest.xml`을(를) 열고 다음 권한을 추가합니다. 앱에서 &quot;인터넷&quot; 및 &quot;ACCESS_NETWORK_STATE&quot; 권한을 요청해야 합니다. 앱에서 이미 이러한 권한을 요청하는 경우 이 단계를 건너뜁니다.

   ```xml
   <uses‐permission android:name="android.permission.INTERNET"/>
   <uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
   
   <!‐‐Following permissions are required for push notification.‐‐>
   <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
   <!‐‐Keeps the processor from sleeping when a message is received.‐‐>
   <uses-permission android:name="android.permission.WAKE_LOCK"/>
   <permission android:name="<PACKAGE_NAME>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
   <uses-permission android:name="<PACKAGE_NAME>.permission.C2D_MESSAGE" />
   <!-- This app has permission to register and receive data message. -->
   <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   ```

1. HTTPv1로 FCM 설정(Google은 2023년 6월 12일에 [더 이상 사용되지 않는 XMPP 프로토콜](https://firebase.google.com/docs/cloud-messaging/xmpp-server-ref)이 있으며 2024년 6월에 제거됩니다.)

- Marketo 기능 관리자 ![](assets/feature-manager.png)에서 MME FCM HTTPv1 사용
   - MLM에서 앱에 대한 서비스 계정 Json 파일을 업로드합니다.
   - Firebase 콘솔에서 서비스 계정 JSON 파일을 다운로드할 수 있습니다.   ![](assets/fcm-console.png)
   - 푸시 알림을 전송하기 전에 Marketo에서 서비스 계정 JSON 파일을 업로드한 후 1시간 동안 기다립니다.  

## Android 테스트 장치

매니페스트 파일의 Marketo 활동을 응용 프로그램 태그 내에 추가합니다.

```xml
<activity android:name="com.marketo.MarketoActivity"  android:configChanges="orientation|screenSize">
    <intent-filter android:label="MarketoActivity">
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto"/>
    </intent-filter/>
</activity/>
```

## Marketo 푸시 서비스 등록

1. Marketo에서 푸시 알림을 받으려면 Firebase 메시징 서비스를 `AndroidManifest.xml`에 추가해야 합니다. 닫기 애플리케이션 태그 앞에 를 추가합니다.

   ```xml
   <meta-data
       android:name="com.google.android.gms.version"
       android:value="@integer/google_play_services_version" />
   <service android:name=".MyFirebaseMessagingService">
   <intent-filter>
   <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
   <action android:name="com.google.firebase.MESSAGING_EVENT"/>
   </intent-filter>
   </service>
   ```

1. 다음과 같이 `MyFirebaseMessagingService` 파일에 Marketo SDK 메서드를 추가합니다.

   ```java
   import com.marketo.Marketo;
   
   public class MyFirebaseMessagingService extends FirebaseMessagingService {
   
       @Override
       public void onNewToken(String s) {
           super.onNewToken(s);
           Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
           marketoSdk.setPushNotificaitonToken(s);
           // Add your code here...
       }
   
       @Override
       public void onMessageReceived(RemoteMessage remoteMessage) {
           Marketo marketoSdk = Marketo.getInstance(this.getApplicationContext());
           marketoSdk.showPushNotificaiton(remoteMessage);
           // Add your code here...
       }
   
   }
   ```

   **참고** - Adobe 확장을 사용하는 경우 아래와 같이 추가하십시오.

   ```java
   import com.marketo.Marketo;
   
   public class MyFirebaseMessagingService extends FirebaseMessagingService {
   
       @Override
       public void onNewToken(String token) {
           super.onNewToken(token);
           ALMarketo.setPushNotificationToken(token);
           // Add your code here...
       }
   
       @Override
       public void onMessageReceived(RemoteMessage remoteMessage) {
           ALMarketo.showPushNotification(remoteMessage);
           // Add your code here...
       }
   
   }
   ```

**참고**: FCM SDK은 필요한 받는 사람 기능과 모든 필요한 권한을 자동으로 추가합니다. 이전 버전의 SDK을 사용한 경우 앱의 매니페스트에서 다음 사용되지 않는(또는 메시지 중복을 일으킬 수 있으므로 해로울 수 있는) 요소를 제거해야 합니다

```xml
<receiver android:name="com.marketo.MarketoBroadcastReceiver" android:permission="com.google.android.c2dm.permission.SEND">
    <intent-filter>
        <!‐‐Receives the actual messages.‐‐>
        <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
        <!‐‐Register to enable push notification‐‐>
        <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
        <!‐‐‐Replace YOUR_PACKAGE_NAME with your own package name‐‐>
        <category android:name="YOUR_PACKAGE_NAME"/>
    </intent-filter>
</receiver>

<!‐‐Marketo service to handle push registration and notification‐‐>
<service android:name="com.marketo.MarketoIntentService"/>
```

1. Marketo 푸시 초기화 위의 구성을 저장한 후 Marketo 푸시 알림을 초기화해야 합니다. Application 클래스를 만들거나 열고 아래 코드를 복사하거나 붙여 넣습니다. Firebase 콘솔에서 발신자 ID를 가져올 수 있습니다.

   ```java
   Marketo marketoSdk = Marketo.getInstance(getApplicationContext());
   
   // Enable push notification here. The push notification channel name can by any string
   marketoSdk.initializeMarketoPush(SENDER_ID,"ChannelName");
   ```

   [!DNL Adobe Launch] 확장을 사용하는 경우 다음 지침을 사용하십시오

   ```java
   // Enable push notification here. The push notification channel name can by any string
   ALMarketo.initializeMarketoPush(SENDER_ID,"ChannelName");
   ```

   SENDER_ID가 없는 경우 [이 자습서](https://developers.google.com/cloud-messaging/)에 설명된 단계를 완료하여 Google Cloud Messaging Service를 사용하도록 설정하십시오.

   사용자가 로그아웃할 때 토큰의 등록을 취소할 수도 있습니다.

   ```java
   marketoSdk.uninitializeMarketoPush();
   ```

   [!DNL Adobe Launch] 확장을 사용하는 경우 아래 지침을 사용하십시오.

   ```java
   ALMarketo.uninitializeMarketoPush();
   ```

   참고: 푸시 토큰을 다시 등록하려면 3단계의 코드를 AppDelegate 메서드에 추출하고 ViewController 로그인 메서드에서 를 호출합니다.

1. 알림 아이콘 설정(선택 사항) 사용자 지정 알림 아이콘을 구성하려면 다음 메서드를 호출해야 합니다.

   ```java
   MarketoConfig.Notification config = new MarketoConfig.Notification();
   // Optional bitmap for honeycomb and above
   config.setNotificationLargeIcon(bitmap);
   
   // Required icon Resource ID
   config.setNotificationSmallIcon(R.drawable.notification_small_icon);
   
   // Set the configuration
   //Use the static methods on ALMarketo class when using Adobe Extension
   Marketo.getInstance(context).setNotificationConfig(config);
   
   // Get the configuration set
   Marketo.getInstance(context).getNotificationConfig();
   ```

## 문제 해결

모바일 푸시 메시지를 설정하려면 여러 단계와 개발자와 마케터의 조정이 필요합니다. 어려움을 겪고 있다면 간단히 확인할 수 있는 사항이 몇 가지 있다.

간단한 내용이 올바른지 확인한 후에는 프로그래밍 세부 사항을 자세히 살펴볼 수 있습니다.

### 푸시 메시지가 표시되지 않음

먼저, 핸드셋에서 푸시 메시지가 비활성화되어 있는지 확인합니다. 모바일 사용자는 특정 앱에 대한 메시지를 수신하는지 여부를 제어할 수 있습니다. 종종 개발자(및 마케터)는 개발 중 특정 시점에 이러한 메시지를 비활성화합니다. 따라서 먼저 수신자가 앱에 대한 푸시 메시지를 비활성화했는지 여부를 확인합니다.

두 번째, 앱이 이미 열려 있고 장치에서 활성화되어 있습니까? 앱이 장치에서 활성 앱인 경우 모바일 푸시 메시지가 화면에 표시되지 않습니다. 대신 앱의 &quot;로컬 알림&quot; 영역에 표시됩니다.

### Marketo에서 활동 로그 보기

오류를 추적할 때 가장 먼저 확인할 수 있는 위치는 Marketo 활동 로그입니다. 활동 로그를 사용하여 메시지가 전송되었는지 확인할 수 있습니다.

활동 로그에서 메시지를 수신하기로 한 사용자에 대한 활동 레코드를 확인합니다. 메시지를 보낸 경우 활동 로그에 레코드가 표시됩니다. 그렇지 않은 경우 Marketo 내의 iOS 인증서 또는 Android API 키 구성으로 인해 문제가 발생할 수 있습니다.

### 인증서 또는 키가 잘못됨

구성을 다시 확인하여 샌드박스 또는 프로덕션에 대해 적절한 인증서가 로드되었는지 확인하십시오. 경우에 따라 개발자가 인증서(iOS) 또는 키(Android)를 다시 내보낸 다음 Marketo으로 다시 로드하여 올바른지 확인하는 것이 좋습니다.

### .p12 파일에 인증서 또는 키가 없습니다(iOS).

인증서를 내보낼 때 키 _및_&#x200B;을(를) 인증서로 내보내야 합니다.

### 프로비전 프로필이 오래됨(iOS)

새 장치를 추가할 때마다 프로비저닝 프로필을 업데이트하고 새 인증서를 생성해야 합니다. 그런 다음 Xcode 프로젝트가 올바른 프로필과 인증서를 가리키는지 확인하고 해당 인증서를 Marketo으로 가져옵니다.

### iOS 인증서(IOS)를 업로드할 수 없음

인증서를 내보내는 동안 사용된 암호에 공백이 포함되어 있지 않은지 확인하십시오.  예를 들어, 다음 대신

`Hello World 123`

사용:

`HelloWorld123`

### iOS 인증서 문제 해결

샌드박스 애플리케이션의 경우 &quot;개발자&quot; 또는 &quot;범용&quot; 인증서를 사용할 수 있습니다. 그러나 프로덕션 애플리케이션의 경우 유효한 &quot;배포&quot; 또는 &quot;범용&quot; 인증서를 업로드해야 합니다.

### 푸시 바운스 / 잘못된 토큰

기존 등록 토큰은 다음을 포함한 여러 시나리오에서 유효하지 않을 수 있습니다.

- 클라이언트 앱이 GCM 등록을 취소하는 경우.
- 클라이언트 앱이 자동으로 등록 취소된 경우, 이는 사용자가 애플리케이션을 제거할 때 발생할 수 있습니다. 예를 들어 iOS에서 APNS 피드백 서비스가 APNS 토큰을 유효하지 않은 것으로 보고한 경우
- 등록 토큰이 만료되는 경우. 예를 들어 Google이 등록 토큰을 새로 고치도록 결정하거나 iOS 장치에 대한 APNS 토큰이 만료되었을 수 있습니다.
- 클라이언트 앱이 업데이트되었지만 새 버전이 메시지를 받도록 구성되지 않은 경우.
