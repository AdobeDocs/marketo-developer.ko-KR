---
title: "Webhooks"
feature: Webhooks
description: "Webhooks 개요"
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# 웹훅

Marketo에서는 웹후크를 사용하여 서드파티 웹 서비스와 통신할 수 있습니다. Webhooks는 GET 또는 POST HTTP 동사를 사용하여 특정 URL에서 데이터를 푸시하거나 검색할 수 있도록 지원합니다. Webhooks의 애플리케이션 내 생성 및 Smart Campaign에 추가하는 방법에 대한 자세한 지침은 다음 문서를 참조하십시오.

- [Webhook 만들기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook)
- [Webhook 호출](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/call-webhook)
- [스마트 캠페인에서 웹후크 사용](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/use-a-webhook-in-a-smart-campaign)

각 개별 웹후크에는 다음 속성이 있습니다.

- URL - 요청을 웹 서비스에 제출하는 데 사용하는 URL을 입력합니다.
- 요청 유형 - HTTP 메서드입니다.
- 페이로드 템플릿 - POST 본문에 있는 정보를 전송하려면 템플릿을 입력합니다. XML, JSON 또는 SOAP를 포함하여 HTTP POST을 지원하는 모든 데이터 형식을 사용합니다. 직렬화 형식은 문자열에서 큰따옴표를 허용해야 합니다. 템플릿에 토큰을 삽입하려면 토큰 삽입을 클릭합니다.  문자열 유형 토큰은 큰따옴표로 자동 묶입니다.
- 요청 토큰 인코딩 - 토큰 값에 특수 문자(예: 앰퍼샌드, &#39;&amp;&#39;)가 포함된 경우 요청 형식(JSON 또는 양식/URL)을 나타냅니다. Webhook이 웹 서비스와 올바르게 통신할 수 있도록 본문에 대해 올바른 인코딩을 선택해야 합니다.
- 응답 유형 - 서비스에서 받은 응답의 형식(JSON 또는 XML)을 선택합니다. 응답의 속성을 Marketo의 리드 필드에 다시 매핑하려면 올바른 응답 유형을 선택해야 합니다.
- 사용자 지정 헤더 - Webhooks Actions -> Set Custom Header를 통해 액세스되며, 이 메뉴를 통해 사용자 지정 키-값 쌍을 HTTP 헤더로 추가할 수 있습니다.

를 사용하여 웹 서비스 응답의 리드에 데이터를 다시 쓸 수 있습니다. [응답 매핑](response-mappings.md)

## 토큰

Webhook의 모든 발신 필드(URL, 템플릿 및 사용자 지정 헤더)는 흐름 단계의 동일한 컨텍스트에서 토큰 콘텐츠를 채웁니다. 즉, 리드 및 시스템 토큰은 항상 사용할 수 있는 반면 트리거, 캠페인 및 프로그램 토큰은 해당 범위에서 사용할 수 있습니다. 토큰 관련 문서 를 참조하십시오.

- [토큰 개요](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/personalizing-landing-pages/tokens-overview)
- [시스템 토큰 용어집](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/using-tokens/system-tokens-glossary)
- [즐거운 순간을 위한 토큰](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-sales-insight/msi-for-salesforce/features/tabs-in-the-msi-panel/interesting-moments/trigger-tokens-for-interesting-moments)

일반적인 사례는 프로그램 또는 캠페인이 서드파티 리소스에 명시적으로 매핑된 경우입니다. 프로그램 수준에서 ID를 로 설정할 수 있습니다. `My Token`를 클릭한 다음 토큰으로 Webhook 요청에 전달됩니다.

## 사용자 지정 헤더

Webhooks를 사용하면 보내는 요청과 함께 사용자 지정 헤더 필드를 보낼 수 있습니다. 다음을 통해 추가할 수 있습니다. **[!UICONTROL Webhooks Actions]** > **[!UICONTROL Set Custom Header]**. 각 헤더는 간단한 키-값 쌍으로 기록됩니다. 이 영역에서는 토큰을 사용할 수 있습니다.

![사용자 지정 헤더](assets/custom-headers.png)

## 팁

- 웹후크 호출 흐름 단계는 트리거 캠페인에서만 유효합니다.
- 응답 매핑을 통한 업데이트는 웹 서비스가 2xx HTTP 응답 코드로 응답하는 경우에만 발생합니다. 다른 유형의 코드는 레코드를 업데이트하지 않습니다.
- 웹 서비스를 사용하여 내부 또는 외부 서비스에서 사용자 지정 데이터 보강, 유효성 검사 또는 표준화를 수행할 수 있습니다.
- 웹후크 실행 시간은 사용 중인 서비스의 응답 시간에 좌우되며 캠페인 실행이 오래 지연될 수 있습니다. 서비스가 실행되는 데 50ms만 걸리더라도 10만회 실행되면 1.5시간이 된다.
- Marketo은 호출을 종료하기 전에 지정된 서비스 호출을 최대 30초 동안 기다립니다(시간 초과).
- URL 필드에 포함된 문자는 기록된 대로 전달됩니다. 예를 들어 &#39;&amp;&#39;는 &#39;&amp;&#39;로 전송되고 &#39;%26&#39;은 &#39;%26&#39;(으)로 전송됩니다
   - 수신자 서버에서 문자를 받을 때 퍼센트 인코딩해야 하는 경우 해당 문자를 나타내는 문자열로 명시적으로 전달해야 합니다
