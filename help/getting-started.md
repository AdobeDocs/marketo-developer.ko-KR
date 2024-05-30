---
title: "시작하기"
description: "Marketo API 시작하기"
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# 시작하기

Marketo은 마케터가 잠재 고객 및 고객에게 개인화된 멀티채널 프로그램 및 캠페인을 관리할 수 있도록 하는 마케팅 자동화 플랫폼입니다. 통합 포인트를 사용하여 Marketo 플랫폼을 확장할 수 있습니다. 아래에서 핵심 엔티티와 해당 관계를 찾을 수 있습니다.

기본 동기화가 활성화된 경우 REST API를 통해 회사, 영업 기회, 영업 기회 역할, 영업 사원과 같은 개체를 사용할 수 없습니다.

![데이터 모델](assets/data_model.png)

## 개인(잠재 고객)

사람은 모든 마케팅 자동화 플랫폼의 기반입니다. Marketo 내에서는 영업 관점에서 잠재 고객, 잠재 고객, 잠재 고객, 연락처 등으로 지정되었는지 여부에 관계없이 모든 비영업 개인 레코드를 잠재 고객이라고 합니다. 리드 오브젝트는 다음 세트와 함께 제공됩니다. [표준 필드](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadFieldsUsingGET) 이메일, 이름 및 성 등. 리드 오브젝트 유형에 필드를 추가하여 시스템의 레코드와 연관된 정보 유형을 확장할 수 있습니다. 사용자 지정 속성은 표준 필드처럼 읽고 쓸 수 있습니다. 전체 필드 목록은 Marketo 내에서 찾을 수 있습니다 **[!UICONTROL Admin]** > **[!UICONTROL Field Management]** 메뉴 아래의 제품에서 사용할 수 있습니다. 리드는 Marketo에서 id 필드로 고유하게 식별됩니다. 다른 고유 키는 시스템 외부에서 적용되어야 합니다.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads), [SOAP](soap-api/leads.md), [JavaScript](javascript-api/lead-tracking.md#lead-tracking-api)

## 활동

리드는 몇 가지 방법으로 조직과 상호 작용합니다. 잠재 고객은 회사 웹 사이트의 페이지를 방문하거나, 무역 박람회에 참석하거나, 백서를 다운로드할 수 있습니다. 이러한 각 작업은 Marketo 내에서 캡처하여 마케터가 리드가 수행한 활동과 그 시기를 더 잘 이해하여 적절하고 관련 있는 커뮤니케이션을 조정할 수 있도록 할 수 있습니다. 활동은 항상 leadId를 통해 리드와 관련이 있습니다.

사용자 지정 활동을 정의할 수 있습니다. 사용자 지정 활동을 만들어 게시하면 Marketo API를 통해 사용자 지정 활동을 추가할 수 있습니다. 사용자 지정 활동에 대한 자세한 내용을 찾을 수 있습니다 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-activities/understanding-custom-activities).

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities), [SOAP](soap-api/activities.md), [JavaScript](javascript-api/lead-tracking.md#munchkin-behavior)

## 프로그램 및 캠페인

프로그램은 마케터가 하나의 중앙 위치에서 모든 다른 유형의 마케팅 활동을 조직하는 메커니즘입니다. 프로그램의 예로는 이메일 폭발이 있습니다. 리드는 해당 프로그램과 관련하여 프로그램과 연계되는 여러 작업/활동을 수행할 수 있습니다. 이를 잠재 고객 진행률이라고 합니다. 이메일 돌발 프로그램의 예제 진행은 잠재 고객이 이메일을 보낸 시점, 이메일을 연 시점 또는 이메일의 링크를 클릭했는지 여부를 기록합니다.

캠페인은 프로그램 내에서 특정 목적과 특정 목표를 제공하기 위해 만들어집니다. 캠페인의 예로는 잠재 고객 그룹 범위를 좁혀 이메일 폭발 보고서를 보내거나 잠재 고객이 이메일 폭발 프로그램 내의 링크를 클릭하는 경우 후속 조치를 위해 영업 담당자에게 알리는 작업이 있습니다.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns), [SOAP](soap-api/getcampaignsforsource.md)

## 태그

태그는 보고 목적으로 데이터를 그룹화하는 방법입니다. 이러한 식별자는 데이터를 분류하고 프로그램에 대해 보고할 방법을 정의하여 프로그램 효과성과 ROI를 이해하는 기능을 제공합니다.

Marketo 관리자는 Marketo 사용자가 프로그램을 만들 때 선택할 수 있는 필수 및 선택적 태그 유형을 만들 수 있습니다. 이러한 각 태그 유형에 대해 가능한 값은 사용자가 정의하며, 회사에서 보고 목적으로 사용자 정의 태그를 사용하는 방법을 반영합니다.

예를 들어, 가장 많은 리드를 생성하는 영역을 분석할 수 있도록 여러 태그 값(예: 북동부, 남동부)으로 사용자 정의 &quot;영역&quot; 태그 유형을 만들 수 있습니다. 또는 예를 들어 &quot;소유자&quot; 태그 유형을 만들어 리드 및 기회를 만드는 데 가장 큰 영향을 미치는 프로그램 소유자(예: Maria, David 또는 John)를 평가하고 이해할 수 있습니다. 태그에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/understanding-tags).

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/asset/), [SOAP](soap-api/gettags.md)

## 목록

목록을 사용하면 마케터가 리드 컬렉션을 구성할 수 있습니다. Marketo 내에는 정적 및 스마트라는 두 가지 유형의 목록이 있습니다. 정적 목록은 마케터가 선택한 대로 추가하거나 제거할 수 있는 고정 리드 목록입니다. 스마트 목록은 지정된 특성 세트를 기반으로 하는 잠재 고객의 동적 컬렉션입니다. 스마트 목록의 예로는 &quot;웹 사이트의 가격 책정 페이지를 방문한 모든 잠재 고객&quot;이 있습니다. 이 스마트 목록은 더 많은 잠재 고객이 가격 페이지를 방문함에 따라 지속적으로 증가하고 있습니다. 목록에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/home).

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists), [SOAP](soap-api/getimporttoliststatus.md)

## 기회

마케터는 영업 기회의 형태로 잠재 고객을 판매합니다. 영업 기회는 잠재적 판매 거래를 나타내며 Marketo의 잠재 고객 또는 연락처 및 조직과 연결됩니다. 영업 기회 역할은 해당 리드와 조직 간의 교차입니다. 영업 기회 역할은 잠재 고객의 조직 내 활동과 관련이 있습니다.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities), [SOAP](soap-api/getmobjects.md)

## 회사

Marketo에서 계정이라고도 하는 조직은 개인이 속한 조직을 의미합니다. Marketo 또는 RCA(Revenue Cycle Analytics)에서 ROI 보고를 사용할 때 적절한 ROI 속성을 결정할 수 있도록 사람을 조직 및 기회와 연결하는 것이 중요합니다.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies), [SOAP](soap-api/leads.md)

## 자산

에셋은 프로그램 내에서 사용되는 랜딩 페이지, 이메일, 양식 및 이미지를 나타냅니다. 자산은 주어진 프로그램에 대해 로컬이거나 전역일 수 있습니다. 글로벌 자산은 모든 프로그램에서 사용할 수 있습니다.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/asset/)

## 토큰

토큰을 사용하면 마케터가 자산을 사용하여 메시지를 개인화하고 흐름 작업 내에 논리를 추가할 수 있습니다. 전체 시스템, 프로그램, 리드, 회사를 위한 토큰이 있습니다. 리드 토큰의 예는 다음과 같습니다. {{lead.First Name}}. 잠재 고객의 이름을 표시하기 위해 이 토큰을 이메일 내에 배치할 수 있습니다.

프로그램 또는 폴더 수준에서 정의된 토큰을 Marketo 내의 &quot;내 토큰&quot;이라고 합니다. 내 토큰은 로컬, 상속 또는 재정의된 세 가지 유형 중 하나일 수 있습니다.

특정 캠페인 폴더 또는 프로그램 내에서 로컬로 생성된 내 토큰은 해당 특정 프로그램 또는 캠페인 폴더(로컬)에서 사용할 수 있습니다. 캠페인 폴더 수준에서 만든 내 토큰은 해당 캠페인 폴더(상속됨)에 포함된 모든 프로그램에서 사용할 수 있습니다. 프로그램 수준에서 사용자 지정 값으로 수정된 내 토큰은 프로그램 폴더 수준에서 토큰의 상위 내 토큰 값을 변경하지 않습니다(재정의됨).

내 토큰은 명명 규칙을 사용합니다. {{my.My Token}}, with the word "my" added to the beginning of the token name. For example, if you create a Date type My Token with the name EventDate, the name of the token is {{my.EventDate}}. 내 토큰에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program).

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens), [SOAP](soap-api/getcampaignsforsource.md)

## 사용자 지정 개체

Marketo 사용자 지정 개체를 사용하면 Marketo 리드와 사용자 지정 개체 레코드 간에 일대다 또는 다대다(Edge-Bridge-Edge) 관계를 만들 수 있습니다. Marketo 사용자 지정 개체를 만들어 게시하면 Marketo API를 통해 사용자 지정 개체에 대해 CRUD 작업을 수행할 수 있습니다. 사용자 지정 개체 작성에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/home). 사용자 지정 개체에 새 레코드가 추가되면 스마트 목록 트리거를 사용하여 응답할 수 있습니다. 사용자 지정 개체 데이터를 스마트 목록(세그먼테이션)이나 다음을 사용하여 이메일에서 필터로 사용할 수도 있습니다. [이메일 스크립팅](email-scripting.md).

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects), [SOAP](soap-api/custom-objects.md)

## 영업 담당자

기본 CRM 통합이 활성화되어 있지 않을 때 Marketo에서 영업 사원 레코드 및 리드 관계를 관리할 수 있습니다. 이러한 레코드에는 이름, 이메일 및 직책과 같은 영업 사원에 대한 기본 정보가 포함되어 있으며, 잠재 고객이 Marketo에 있을 때 필터링 및 토큰에 사용할 수 있습니다. 영업 사원과의 관계는 &quot;externalSalesPersonId&quot; 필드를 통해 리드 수준에서 관리되며, 다음을 통해 업데이트되어야 합니다. [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) API.

관련 API: [나머지](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Sales-Persons)
