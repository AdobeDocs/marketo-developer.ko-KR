---
title: 오류수
feature: Webhooks
description: Marketo Webhook 오류 코드, 리드 필드를 업데이트하는 데 2xx 응답이 필요한 이유, Webhook에서 오류를 포착하고 처리하는 방법이 호출되는지 알아봅니다.
exl-id: adce40c3-87b1-4f31-8995-eb64e8a72b55
TQID: https://experienceleague.adobe.com/N2jNA4EUMMTUFL9uJHZhOor6Tlz4-EXWciwoXrPml48
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 2%

---

# 오류수

이 페이지에서는 Marketo 웹후크의 오류 응답 코드와 웹후크 오류 처리 방법에 대해 설명합니다.

Marketo은 오류 코드 1000 및 1001을 생성합니다. Marketo 웹후크에서 호출한 시스템은 2xx ~ 5xx 응답 코드를 반환합니다.

Marketo은 웹 서비스가 2xx 응답 코드를 반환하는 경우에만 응답 값을 필드에 매핑합니다. 웹후크 응답이 Marketo 잠재 고객 레코드의 값을 변경하려고 하는 경우 다른 모든 응답 코드는 Marketo이 필드 업데이트에 대한 응답을 무시하도록 합니다.

| 응답 코드 | 설명 |
| --- | --- |
| 1000 | 이는 &#39;Call Webhook&#39; 흐름 작업이 배치 캠페인 내에 하우징되고 있음을 나타냅니다. Webhooks는 트리거 캠페인에서만 실행할 수 있습니다. |
| 1001 | 웹 서비스가 빈 응답 본문을 보냈음을 나타냅니다. |

## Webhook 오류 잡기

**[!UICONTROL Webhook is Called]** 트리거를 사용하여 웹후크 오류를 추적하고 처리합니다.

![Webhook이 호출되었습니다](assets/webhook-called.png)

* **응답** - 요청에서 받은 리터럴 응답 페이로드입니다.
* **오류 유형** - HTTP 상태 메시지의 이유 구문입니다.

이러한 값을 사용하여 예측 가능한 오류 및 예외에 응답합니다. 통합 서비스에 따라 일부 오류 클래스에서 자동으로 복구하고 예기치 않은 오류에 대한 경고를 만들 수 있습니다.
