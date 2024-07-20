---
title: 오류수
feature: Webhooks
description: Webhooks용 오류 코드
exl-id: adce40c3-87b1-4f31-8995-eb64e8a72b55
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---

# 오류수

이 페이지에는 Marketo의 웹후크에 대한 오류 응답 코드가 나열됩니다.

1000 및 1001은 Marketo에서 생성되며, 2xx ~ 5xx는 Marketo 웹후크에서 호출하는 시스템에서 반환된 오류입니다.

Marketo이 값을 필드에 다시 매핑하려면 웹후크 응답 코드가 2xx 유형이어야 합니다. 웹후크의 목적이 응답을 통해 Marketo 리드 레코드의 값을 변경하는 것이라면, 호출되는 웹 서비스는 2xx를 반환해야 하며, 다른 모든 응답 코드는 리드 레코드 값을 업데이트하기 위해 웹후크를 무시하게 됩니다.

| 응답 코드 | 설명 |
| --- | --- |
| 1000 | 이는 &#39;Call Webhook&#39; 흐름 작업이 배치 캠페인 내에 하우징되고 있음을 나타냅니다. Webhooks는 트리거 캠페인에서만 실행할 수 있습니다. |
| 1001 | 웹 서비스가 빈 응답 본문을 보냈음을 나타냅니다. |

## Webhook 오류 잡기

[!UICONTROL Webhook is Called] 트리거에서 Webhooks의 오류를 catch 및 처리할 수 있습니다.

![Webhook이 호출되었습니다](assets/webhook-called.png)

* Response - Response 는 요청에 의해 수신된 리터럴 응답 페이로드입니다.
* 오류 유형 - HTTP 상태 메시지의 Reason-Phrase에 해당합니다.

이를 사용하여 예측 가능한 오류 및 예외를 처리하고 대응할 수 있습니다. 통합하는 서비스에 따라 특정 오류 클래스를 자동으로 복구하는 동시에 예기치 않은 오류를 사용자에게 알리는 경고를 만들 수 있습니다.
