---
title: 웹훅
feature: Webhooks
description: 타사 서비스를 호출하도록 Marketo 웹후크를 구성하고, 페이로드 템플릿, 인코딩, 응답 매핑, 토큰, 사용자 지정 헤더 및 팁을 설정하는 방법에 대해 알아봅니다.
exl-id: fd283c66-05a1-4aa4-8412-0d41b8d1e3c8
TQID: https://experienceleague.adobe.com/r-GpAqhYPKvlDtMw5l23jeJWzlSqycP65eYJPA3m9EM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
subfeature_v2:
  - id: ad89fb33-8541-4339-afe7-bb13d1633714
  - id: fc9b09fe-b844-4544-887b-e420c3b82065
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 3%

---

# 웹훅

Marketo 웹후크는 타사 웹 서비스와 통신합니다. Webhook은 GET 또는 POST HTTP 동사를 사용하여 데이터를 특정 URL로 보내거나 특정 URL에서 데이터를 검색합니다.

웹후크를 만들고 Smart Campaign에 추가하는 방법에 대한 지침은 다음을 참조하십시오.

- [웹후크 만들기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [웹후크 호출](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [스마트 캠페인에서 웹후크 사용](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

다음 속성으로 각 Webhook를 구성합니다.

- **[!UICONTROL URL]** - 웹 서비스 요청을 제출하는 URL.
- **[!UICONTROL Request Type]** - HTTP 메서드.
- **[!UICONTROL Payload Template]** - POST 본문에 전송된 정보의 템플릿입니다. XML, JSON 또는 SOAP 등 HTTP POST를 지원하는 모든 데이터 형식을 사용합니다. 직렬화 형식은 문자열에서 큰따옴표를 허용해야 합니다. 토큰을 삽입하려면 **[!UICONTROL Insert Token]**&#x200B;을(를) 선택합니다. Marketo은 문자열 유형 토큰을 큰따옴표로 자동으로 묶습니다.
- **[!UICONTROL Request Token Encoding]** - 앰퍼샌드, &#39;&amp;&#39;와 같은 특수 문자가 포함된 토큰 값을 인코딩하는 데 사용되는 JSON 또는 Form/Url 요청 형식입니다. Webhook이 웹 서비스와 올바르게 통신할 수 있도록 올바른 본문 인코딩을 선택합니다.
- **[!UICONTROL Response Type]** - 응답 형식, JSON 또는 XML. 응답 속성을 Marketo의 리드 필드에 매핑하려면 올바른 유형을 선택합니다.
- **[!UICONTROL Custom Headers]** - 키-값 쌍이 **[!UICONTROL Webhooks Actions]** > **[!UICONTROL Set Custom Header]**&#x200B;을(를) 통해 HTTP 헤더로 추가되었습니다. 사용자 지정 헤더를 원하는 수만큼 추가할 수 있습니다.

[응답 매핑](response-mappings.md)을(를) 사용하여 웹 서비스 응답의 데이터를 리드에 다시 씁니다.

## 토큰

URL, 템플릿 및 사용자 지정 헤더를 포함한 모든 발신 웹후크 필드는 흐름 단계와 동일한 컨텍스트에서 토큰 컨텐츠를 채웁니다.

리드 및 시스템 토큰은 항상 사용할 수 있습니다. 트리거, 캠페인 및 프로그램 토큰은 해당 범위에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [토큰 개요](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [시스템 토큰 용어집](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [즐거운 순간을 위한 토큰](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

예를 들어 프로그램이나 캠페인이 서드파티 리소스에 매핑되는 경우 프로그램 수준의 ID를 `My Token`(으)로 설정합니다. 그런 다음 ID를 웹후크 요청에 토큰으로 전달합니다.

## 사용자 지정 헤더

Webhooks는 보내는 요청과 함께 사용자 지정 헤더 필드를 보낼 수 있습니다. **[!UICONTROL Webhooks Actions]** > **[!UICONTROL Set Custom Header]**&#x200B;을(를) 통해 헤더를 추가합니다.

각 헤더는 키-값 쌍이며 토큰을 포함할 수 있습니다.

![사용자 지정 머리글](assets/custom-headers.png)

## 팁

- 트리거 캠페인에서만 Webhook 호출 흐름 단계를 사용합니다.
- 응답 매핑은 웹 서비스가 2xx HTTP 응답 코드를 반환하는 경우에만 레코드를 업데이트합니다.
- 웹 서비스를 사용하여 내부 또는 외부 서비스에서 사용자 지정 데이터 보강, 유효성 검사 또는 표준화를 수행할 수 있습니다.
- 웹후크 실행 시간은 서비스의 응답 시간에 따라 다르며 긴 캠페인 실행 지연을 발생시킬 수 있습니다. 서비스가 실행되는 데 50ms만 걸리더라도 10만건 실행은 1.5시간이 걸린다.
- Marketo은 호출을 종료하기 전에 지정된 서비스 호출을 최대 30초 동안 기다립니다(시간 초과라고도 함).
- Marketo은 URL 필드의 문자를 기록된 대로 전달합니다. 예를 들어 &#39;&amp;&#39;는 &#39;&amp;&#39;로 전송되고 &#39;%26&#39;은 &#39;%26&#39;로 전송됩니다.
  - 퍼센트 인코딩된 문자를 받는 사람 서버로 보내려면 해당 문자를 나타내는 문자열을 명시적으로 전달하십시오.
