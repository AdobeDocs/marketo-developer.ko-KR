---
title: SOAP API
feature: SOAP
description: Marketo SOAP 개요
exl-id: 6618cc82-15ae-4030-aa00-438e635d8369
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# SOAP API

SOAP API는 더 이상 활성 개발 상태가 아닙니다. 호출은 여전히 작동하지만, 우리의 발전은 [나머지](https://developer.adobe.com/marketo-apis/) 앞으로 나아갑니다.

Marketo SOAP API를 사용하면 Marketo 내에 저장된 엔티티 및 데이터를 생성, 검색 및 제거할 수 있습니다. 다음을 찾을 수 있습니다. [Marketo-SOAP-SDK](https://github.com/Marketo/SOAP-API-Java-Client) GitHub에서. 또한 [클라이언트 라이브러리](https://github.com/Marketo/Community-Supported-Client-Libraries) 시간을 절약하기 위해

최신 API 버전: 3_1

## SOAP WSDL

SOAP SOAP WSDL 문서를 검색하려면 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]** 메뉴 아래의 제품에서 사용할 수 있습니다.

![SOAP 엔드포인트](assets/endpoint-soap.png)

WSDL URL은

`<SOAP API Endpoint> + ?WSDL`

WSDL에 정의된 끝점을 사용하지 마십시오. 각 Marketo 인스턴스에는 를 호출할 수 있는 고유한 끝점이 있습니다.

## 제한

- **일일 할당량:** 대부분의 구독에는 하루에 10,000개의 API 호출이 할당됩니다(매일 오전 12:00CST에 재설정됨). 계정 관리자를 통해 일일 할당량을 늘릴 수 있습니다.
- **속도 제한:** 인스턴스당 API 액세스는 20초당 100개 호출로 제한되었습니다.
- **동시 실행 제한:**  최대 10개의 동시 API 호출.

권장 사항은 배치 크기가 300을 초과하지 않는 것입니다. 더 큰 크기는 지원되지 않으며 이로 인해 시간 초과가 발생하고 경우에 따라 조절됩니다.

## Marketo의 SOAP API 설정

1. 로 이동 **[!UICONTROL Admin]** 섹션 및 클릭 **[!UICONTROL Web Services]**.

![admin-web-services2](assets/admin-web-services2.png)

1. 적절한 설정 [!UICONTROL Encryption Key], 클릭 **[!UICONTROL Save Changes]** 및 SOAP API 사용 [!UICONTROL Endpoint], [!UICONTROL User ID], 및 [!UICONTROL Encryption Key] 정확한 값을 생성하는 값 [인증 서명](authentication-signature.md) 각 SOAP API 호출에 대해.

![admin-web-services3](assets/admin-web-services3.png)
