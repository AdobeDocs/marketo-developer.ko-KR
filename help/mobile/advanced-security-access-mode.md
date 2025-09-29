---
title: 고급 보안 액세스 모드
feature: Mobile Marketing
description: HMAC 서명 생성, 서버 엔드포인트 설정, 장치 ID 사용 및 Marketo과 SDK의 예를 포함하는 iOS 모바일 Android용 고급 보안 액세스 모드에 대해 알아봅니다
exl-id: bd4730ff-708b-465e-b494-485a4dbf67ff
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 고급 보안 액세스 모드

Marketo SDK은 보안 서명을 설정하고 제거하는 메서드를 노출합니다. 장치 ID를 검색하는 유틸리티 메서드도 있습니다. 보안 서명 계산에 사용할 수 있도록 장치 ID를 전자 메일과 함께 고객 서버에 전달해야 합니다. SDK은 위에 나열된 알고리즘을 가리키는 새 끝점을 히트하여 서명 개체를 인스턴스화하는 데 필요한 필드를 검색해야 합니다. Marketo Mobile Admin에서 보안 액세스 모드가 활성화된 경우 SDK에서 이 서명을 설정하는 것이 필요한 단계입니다.

## 보안 액세스 모드 설정

Marketo 관리 > 모바일 앱 및 장치 페이지를 통해 보안 액세스 모드를 활성화하기 전에 이 설정을 구현해야 합니다. 다음 추가 단계에서는 보안 유효성 검사 프로세스를 완료하는 데 필요한 프로세스를 설명합니다.

보안 액세스 모드에서는 액세스 키, 계산된 서명, 만료 타임스탬프 및 이메일을 검색하기 위한 끝점을 제공하는 고객 서버측 서명 알고리즘을 구현해야 합니다. 이 알고리즘을 사용하려면 계산을 수행하기 위해 사용자 액세스 키, 액세스 암호, 이메일, 타임스탬프 및 장치 ID가 필요합니다. 고객은 엔드포인트를 설정하고, 알고리즘을 구현하여 서명 계산을 수행하고, 만료 타임스탬프를 최신 상태로 유지할 책임이 있습니다.

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

Marketo SDK은 보안 서명을 설정하고 제거하는 새로운 메서드를 노출합니다. 장치 ID를 검색하는 유틸리티 메서드도 있습니다. 보안 서명 계산에 사용할 수 있도록 장치 ID를 전자 메일과 함께 고객 서버에 전달해야 합니다. SDK은 위에 나열된 알고리즘을 가리키는 새 끝점을 히트하여 서명 개체를 인스턴스화하는 데 필요한 필드를 검색해야 합니다. Marketo Mobile Admin에서 보안 액세스 모드가 활성화된 경우 SDK에서 이 서명을 설정하는 것이 필요한 단계입니다.

### iOS

```
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

```
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

```
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
