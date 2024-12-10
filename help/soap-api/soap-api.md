---
title: SOAP API
feature: SOAP
description: Marketo SOAP 개요
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: 7a3df193e47e7ee363c156bf24f0941879c6bd13
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# SOAP API

SOAP API는 더 이상 사용되지 않으며 2025년 10월 31일 이후부터 더 이상 사용할 수 없습니다.  모든 새 개발은 Marketo [REST](https://developer.adobe.com/marketo-apis/) API로 수행해야 하며, 서비스가 중단되지 않도록 기존 서비스를 해당 날짜까지 마이그레이션해야 합니다.

## SOAP WSDL

SOAP WSDL 문서를 검색하려면 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]** 메뉴에서 SOAP API 끝점을 가져옵니다.

![SOAP 끝점](assets/endpoint-soap.png)

WSDL URL은

`<SOAP API Endpoint> + ?WSDL`

WSDL에 정의된 끝점을 사용하지 마십시오. 각 Marketo 인스턴스에는 를 호출할 수 있는 고유한 끝점이 있습니다.

## 제한

- **일일 할당량:** 대부분의 구독에는 하루에 10,000개의 API 호출이 할당됩니다(매일 오전 12시(CST) 재설정됨). 계정 관리자를 통해 일일 할당량을 늘릴 수 있습니다.
- **속도 제한:** 인스턴스당 API 액세스가 20초당 100개의 호출로 제한되었습니다.
- **동시 실행 제한:**  최대 10개의 동시 API 호출.

권장 사항은 배치 크기가 300을 초과하지 않는 것입니다. 더 큰 크기는 지원되지 않으며 이로 인해 시간 초과가 발생하고 경우에 따라 조절됩니다.

## Marketo의 SOAP API 설정

1. **[!UICONTROL Admin]** 섹션으로 이동한 다음 **[!UICONTROL Web Services]**&#x200B;을(를) 클릭합니다.

![admin-web-services2](assets/admin-web-services2.png)

1. 적절한 [!UICONTROL Encryption Key]을(를) 설정하고 **[!UICONTROL Save Changes]**&#x200B;을(를) 클릭한 다음 SOAP API [!UICONTROL Endpoint], [!UICONTROL User ID] 및 [!UICONTROL Encryption Key] 값을 사용하여 각 SOAP API 호출에 대한 올바른 [인증 서명](authentication-signature.md)을(를) 생성합니다.

![admin-web-services3](assets/admin-web-services3.png)
