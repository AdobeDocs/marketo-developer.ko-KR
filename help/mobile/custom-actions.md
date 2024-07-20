---
title: 사용자 지정 작업
feature: Mobile Marketing
description: 사용자 지정 작업 개요
exl-id: 8c2698ce-4e39-4b2b-9d36-0864c55be17a
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 사용자 지정 작업

사용자 지정 작업을 전송하여 사용자 상호 작용을 추적할 수 있습니다. 모바일 앱이 Marketo SDK를 호출하여 사용자 지정 작업을 전송하면 사용자 지정 작업이 처음에 디바이스에 저장됩니다. 그런 다음 Marketo SDK는 사용자 지정 작업을 보내기 전에 적절한 인터넷 연결이 있는지 확인합니다. 따라서 사용자 지정 작업을 보낸 시간과 Marketo에서 받은 시간 사이에 지연이 있을 수 있습니다.

사용자 지정 작업은 스마트 캠페인에서 트리거 및 필터로 사용할 수 있습니다. 자세한 내용은 [모바일 앱 활동](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns)을 참조하세요.

## iOS에서 사용자 지정 작업 보내기

사용자 지정 작업을 보냅니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
Marketo *sharedInstance = [Marketo sharedInstance];
[sharedInstance reportAction:@"Login" withMetaData:nil];
```

>[!TAB Swift]

```
sharedInstance.reportAction("Login", withMetaData:nil);
```

>[!ENDTABS]

메타데이터가 포함된 사용자 지정 작업을 보냅니다.

>[!BEGINTABS]

>[!TAB 목표 C]

```
MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
[meta setType:@"Shopping"];
[meta setDetails:@"RedShirt"];
[meta setLength:20];
[meta setMetric:30];

[sharedInstance reportAction:@"Bought Shirt" withMetaData:meta];
```

>[!TAB Swift]

```
let meta = MarketoActionMetaData()
meta.setType("Shopping");
meta.setDetails("RedShirt");
meta.setLength(20);
meta.setMetric(30);

sharedInstance.reportAction("Bought Shirt", withMetaData:meta);
```

>[!ENDTABS]

모든 작업을 즉시 보고합니다(저장된 모든 작업 보내기).

>[!BEGINTABS]

>[!TAB 목표 C]

```
[sharedInstance reportAll];
```

>[!TAB Swift]

```
sharedInstance.reportAll();
```

>[!ENDTABS]

## Android에서 사용자 지정 작업 보내기

1. 사용자 지정 작업을 보냅니다.

   ```
   Marketo.reportAction("Login", null);
   ```

1. 메타데이터가 포함된 사용자 지정 작업을 보냅니다.

   ```
   MarketoActionMetaData meta = new MarketoActionMetaData();
   meta.setActionType("Shopping");
   meta.setActionDetails("RedShirt");
   meta.setActionLength("20");
   meta.setActionMetric("30");
   
   Marketo.reportAction("Bought Shirt", meta);
   ```

1. 모든 사용자 지정 작업을 즉시 보고합니다(저장된 모든 작업 보내기).

   ```
   Marketo.reportAll();
   ```

## 사용자 지정 작업 문제 해결

모바일 사용자 지정 작업을 설정하는 것은 간단하지만, Mobile SDK에서 Marketo으로 보낼 수 있는 문자 수에 대한 제한이 있습니다. Mobile SDK를 통해 Marketo으로 다시 보고하는 모든 사용자 지정 작업의 길이가 20자 미만인지 확인하십시오.

**공유 장치의 다중 사용자 사용 사례에 대한 참고 사항:** 사용자가 Marketo SDK와 통합된 모바일 앱에 로그인할 때 먼저 리드를 앱 설치와 연결하기 위한 호출이 수행됩니다. 이 호출이 성공적으로 완료되면 잠재 고객의 활동 로그에서 앱의 추가 사용자 활동을 볼 수 있습니다. 참고: 이 호출은 비동기 호출이므로 로그인 후 즉시 기록된 사용자 지정 작업이 있으면 연결 호출이 성공할 때까지 이전에 로그인한 사용자와 연결될 수 있습니다.
