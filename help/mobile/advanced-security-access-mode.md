---
title: 고급 보안 액세스 모드
feature: Mobile Marketing
description: HMAC 서명 생성, 서버 엔드포인트 설정, 장치 ID 사용 및 Marketo과 SDK의 예를 포함하는 iOS 모바일 Android용 고급 보안 액세스 모드에 대해 알아봅니다
exl-id: bd4730ff-708b-465e-b494-485a4dbf67ff
TQID: https://experienceleague.adobe.com/F6lH1aGbCakK-E6IU4wLwYw58BG2-CRE-Ras2bMHeO8
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 217
ht-degree: 1%

---

# 고급 보안 액세스 모드

고급 보안 액세스 모드를 사용하려면 Marketo SDK에서 보안 서명을 검색하고 설정해야 합니다. SDK은 서명을 설정 및 제거하는 메서드와 장치 ID를 검색하는 유틸리티 메서드를 제공합니다.

로그인 시 장치 ID와 이메일 주소를 고객 서버에 전송하여 보안 서명을 계산합니다. 그런 다음 SDK은 고객 끝점을 호출하여 서명 개체를 인스턴스화하는 데 필요한 필드를 검색합니다. Marketo Mobile Admin에서 보안 액세스 모드가 활성화된 경우 SDK에서 이 서명을 설정해야 합니다.

## 보안 액세스 모드 설정

Marketo 관리 > 모바일 앱 및 장치 페이지에서 보안 액세스 모드를 활성화하기 전에 이 설정을 구현하십시오.

보안 액세스 모드에서는 서버측 서명 알고리즘 및 고객 엔드포인트가 필요합니다. 끝점은 다음 값을 반환합니다.

- 액세스 키
- 계산된 서명
- 만료 타임스탬프
- 이메일 주소

이 알고리즘은 사용자 액세스 키, 액세스 암호, 이메일 주소, 타임스탬프 및 장치 ID를 사용합니다. 고객은 끝점을 설정하고 서명 계산을 구현하며 만료 타임스탬프를 최신 상태로 유지해야 합니다.

```python
import argparse
import datetime
import hashlib
import hmac


ACCESS_KEY = 'Your Access Key'
ACCESS_SECRET = 'Your access secret'

# Key should not be unicode
def get_signing_key(timestamp):
    return 'MKTO' + ACCESS_SECRET + str(timestamp)

def get_string_to_sign(email, uuid):
    return email + uuid

def get_hmac(key, string_to_sign):
    return hmac.new(key, string_to_sign.encode('utf-8'), hashlib.sha256).hexdigest()

def get_epoch_plus_day():
    epoch = datetime.datetime.utcfromtimestamp(0)
    valid_until_dt = datetime.datetime.utcnow() + datetime.timedelta(days=1)
    return long((valid_until_dt - epoch).total_seconds())

if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument("-e", "--email", required=True, help="email address")
    parser.add_argument("-u", "--uuid", required=True, help="Device install id")
    parser.add_argument("-t", "--timestamp", type=int, help="Valid until timestamp")
    args = parser.parse_args()
    string_to_sign = get_string_to_sign(args.email, args.uuid)
    if not args.timestamp:
        valid_until = get_epoch_plus_day()
    else:
        valid_until = args.timestamp
    signing_key = get_signing_key(valid_until)
    hmac_string = get_hmac(signing_key, string_to_sign)
    print 'HMAC is ', hmac_string
```

플랫폼별 메서드를 사용하여 보안 서명을 설정 또는 제거하고 장치 ID를 검색합니다.

### iOS

```objectivec
Marketo * sharedInstance =[Marketo sharedInstance];

// set secure signature
MKTSecuritySignature *signature =
[[MKTSecuritySignature alloc] initWithAccessKey:<ACCESS_KEY> signature:<SIGNATURE_TOKEN> timestamp:<EXPIRY_TIMESTAMP> email:<EMAIL>];
[sharedInstance setSecureSignature:signature];

// remove signature
[sharedInstance removeSecureSignature];

// get device id
[sharedInstance getDeviceId];
```

```swift
let sharedInstance = Marketo.sharedInstance()

 // set secure signature
let signature = MKTSecuritySignature(accessKey: <ACCESS_KEY>, signature: <SIGNATURE_TOKEN> , timestamp: <EXPIRY_TIMESTAMP>, email: <EMAIL>)
sharedInstance.setSecureSignature(signature)

// remove signature
[sharedInstance removeSecureSignature];

// get device id
sharedInstance.getDeviceId()
```

### Android

```java
Marketo sdk = Marketo.getInstance(getApplicationContext());

// set signature
MarketoConfig.SecureMode secureMode = new MarketoConfig.SecureMode();
secureMode.setAccessKey(<ACCESS_KEY>);
secureMode.setEmail(<EMAIL_ADDRESS>);
secureMode.setSignature(<SIGNATURE_TOKEN>);
secureMode.setTimestamp(<EXPIRY_DATE>);
if (secureMode.isValid()) {
  sdk.setSecureSignature(secureMode);
}

// remove signature
sdk.removeSecureSignature();

// get device id
sdk.getDeviceId();
```
