---
title: 시작하기
description: 리드, 활동, 프로그램, 태그, 목록, REST 지침 및 SOAP 사용 중단 알림을 포함한 Marketo Engage API 및 데이터 모델을 시작합니다.
exl-id: 78c44c32-4e59-4d55-a45c-ef0d7dac814d
TQID: https://experienceleague.adobe.com/0lfzor5EQJ0VqIh4fqlK29OiPmRCy6fnEtncJ38r-OM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c954475c-8548-4e33-a0b8-6b550d956115id: d1d0a9cd-295d-4976-8c39-ddae266f240eid: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1225
ht-degree: 2%

---

# 시작하기

Marketo Engage은 잠재 고객 및 고객을 위한 개인화된 멀티채널 프로그램 및 캠페인을 관리하기 위한 마케팅 자동화 플랫폼입니다. 통합 지점을 통해 플랫폼을 확장할 수 있습니다.

이 페이지에서는 핵심 Marketo Engage 엔티티와 해당 관계를 소개합니다.

>[!NOTE]
>
>SOAP API는 더 이상 사용되지 않으며 2026년 7월 31일 이후부터 더 이상 사용할 수 없습니다. 모든 새로운 개발에는 Marketo [REST API](./rest-api/rest-api.md)를 사용하십시오. 서비스 중단을 방지하려면 해당 날짜까지 기존 서비스를 마이그레이션하십시오. 서비스에서 SOAP API를 사용하는 경우 SOAP API [마이그레이션 안내서](./soap-api/migration.md)를 참조하십시오.
>

Marketo Engage 인스턴스에서 기본 SFDC 또는 MS Dynamics CRM 연결을 활성화하면 다음 개체가 읽기 전용입니다.

- 회사
- 기회
- 영업 기회 역할
- 영업사원

![데이터 모델](assets/data_model.png)

## 개인(잠재 고객)

사람은 마케팅 자동화의 기반입니다. Marketo은 판매에서 가망 고객, 잠재 고객, 잠재 고객, 잠재 고객 또는 연락 고객을 고려하는지 여부에 관계없이 모든 비판매 개인 레코드를 가망 고객으로 참조합니다.

잠재 고객 객체에는 이메일, 이름 및 성과 같은 표준 필드가 포함됩니다. 필드를 추가하여 다른 정보를 저장할 수 있으며 표준 필드와 같은 방식으로 사용자 지정 특성을 읽고 쓸 수 있습니다. Marketo의 **[!UICONTROL Admin]** > **[!UICONTROL Field Management]**&#x200B;에서 전체 필드 목록을 찾으십시오.

Marketo은 id 필드로 리드를 고유하게 식별합니다. 시스템 외부에 다른 고유 키를 적용해야 합니다.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads), [JavaScript](javascript-api/lead-tracking.md#lead-tracking-api)

## 활동

리드는 웹 페이지 방문, 박람회 참가, 백서 다운로드 등 여러 방식으로 귀사와 상호 작용할 수 있습니다. Marketo은 이러한 작업을 활동으로 캡처하여 마케터가 리드가 수행한 작업과 발생 시기를 이해할 수 있도록 합니다.

활동은 항상 leadId별로 리드와 관련되어 있습니다.

사용자 지정 활동을 정의할 수도 있습니다. 사용자 지정 활동을 만들고 게시한 후 Marketo API를 통해 해당 활동의 인스턴스를 추가할 수 있습니다. 자세한 내용은 [사용자 지정 활동 이해](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-activities/understanding-custom-activities)를 참조하십시오.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities), [JavaScript](javascript-api/lead-tracking.md#munchkin-behavior)

## 프로그램 및 캠페인

프로그램은 한 위치에서 마케터의 관련 마케팅 활동을 구성합니다. 예를 들어 이메일 폭발은 프로그램일 수 있습니다.

리드는 프로그램과 관련된 여러 작업 또는 활동을 수행할 수 있습니다. 이 프로세스를 잠재 고객 진행이라고 합니다. 이메일 강타 프로그램의 경우, 진행률은 Marketo이 이메일을 전송하는 시점, 사용자가 이메일을 여는 시점 및 사용자가 링크를 클릭하는지 여부를 기록할 수 있습니다.

캠페인은 프로그램 내에서 특정 목적과 목표를 제공합니다. 예를 들어 Campaign은 리드 그룹을 선택하고 이메일 알림을 보낼 수 있습니다. 다른 Campaign은 잠재 고객이 이메일 폭발의 링크를 클릭할 때 영업 담당자에게 알릴 수 있습니다.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Campaigns)

## 태그

태그는 보고를 위해 프로그램 데이터를 그룹화하고 분류합니다. 태그를 사용하여 프로그램 효율성 및 ROI를 측정합니다.

Marketo 관리자는 사용자가 프로그램을 만들 때 선택하는 필수 및 선택적 태그 유형을 만들 수 있습니다. 회사의 보고 요구 사항에 따라 각 태그 유형에 가능한 값을 정의합니다.

예를 들어 북동부 및 남동부와 같은 값으로 사용자 지정 &quot;지역&quot; 태그 유형을 만들어 가장 많은 리드를 생성하는 지역을 분석합니다. Maria, David 또는 John과 같은 프로그램 소유자가 리드 및 기회를 만드는 데 가장 큰 영향을 미치는 &quot;소유자&quot; 태그 유형을 만듭니다. 자세한 내용은 [태그 이해](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/understanding-tags)를 참조하십시오.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/asset)

## 목록

잠재 고객 컬렉션을 구성합니다. Marketo은 두 가지 유형을 제공합니다.

- 정적 목록은 마케터가 리드를 추가하거나 제거할 수 있는 고정 컬렉션입니다.
- 스마트 목록은 정의된 특성을 기반으로 하는 동적 컬렉션입니다.

예를 들어 &quot;당사 웹 사이트의 가격 책정 페이지를 방문한 모든 잠재 고객&quot;이라는 스마트 목록은 더 많은 잠재 고객이 해당 페이지를 방문함에 따라 계속 증가하고 있습니다. 자세한 내용은 [Marketo Engage 설명서](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하세요.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists)

## 기회

영업 기회는 마케터가 영업에 제공하는 잠재적 판매 거래를 나타냅니다. Marketo에서 영업 기회는 잠재 고객 또는 연락처 및 조직과 연결되어 있습니다.

Opportunity 역할은 Lead 를 조직과 연결하고 해당 조직에서 Lead 의 기능을 설명합니다.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Opportunities)

## 회사

Marketo에서 계정이라고도 하는 조직은 개인이 속한 조직입니다.

Marketo ROI 보고 또는 RCA(Revenue Cycle Analytics)의 정확한 ROI 속성을 위해 사람들을 조직 및 기회와 연결하십시오.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies)

## 자산

Assets에는 프로그램에 사용되는 랜딩 페이지, 이메일, 양식 및 이미지가 포함됩니다. 자산은 특정 프로그램에 대해 로컬이거나 전역일 수 있습니다. 글로벌 자산은 모든 프로그램에서 사용할 수 있습니다.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/asset)

## 토큰

토큰을 사용하면 마케터가 자산을 사용하여 메시지를 개인화하고 플로우 액션에 논리를 추가할 수 있습니다. Marketo은 전체 시스템, 프로그램, 리드 및 회사에 대한 토큰을 제공합니다.

예를 들어 잠재 고객 이름 `{{lead.First Name}}`을(를) 전자 메일에 넣어 잠재 고객의 이름을 표시합니다.

프로그램 또는 폴더 수준에서 정의된 토큰을 Marketo에서 &quot;내 토큰&quot;이라고 합니다. 내 토큰에는 세 가지 유형이 있습니다.

- 로컬: 특정 캠페인 폴더 또는 프로그램에서 생성되며 해당 폴더 또는 프로그램에서만 사용할 수 있습니다.
- 상속됨: 캠페인 폴더 수준에서 만들어지며 해당 폴더의 모든 프로그램에서 사용할 수 있습니다.
- 재정의됨: 프로그램 폴더 수준에서 상위 내 토큰 값을 변경하지 않고 프로그램 수준에서 사용자 지정 값으로 수정되었습니다.

내 토큰은 토큰 이름의 시작 부분에 &quot;my&quot;라는 단어와 함께 이름 지정 규칙 `{{my.My Token}}`을(를) 사용합니다. 예를들어 EventDate라는 Date 형식의 My Token은 토큰 이름이 `{{my.EventDate}}`입니다. 자세한 내용은 [프로그램의 내 토큰 이해](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program)를 참조하십시오.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens)

## 사용자 정의 오브젝트

Marketo 사용자 지정 개체는 Marketo 리드와 사용자 지정 개체 레코드 간에 일대다 또는 다대다(Edge-Bridge-Edge) 관계를 만듭니다.

Marketo 사용자 지정 개체를 만들어 게시한 후 Marketo API를 통해 이 개체에 대한 CRUD 작업을 수행할 수 있습니다. 새 레코드가 추가되면 스마트 목록 트리거를 사용하여 응답할 수 있습니다. 사용자 지정 개체 데이터를 [전자 메일 스크립팅](email-scripting.md)을 통해 전자 메일 또는 세분화를 위한 스마트 목록 필터로 사용할 수도 있습니다. 사용자 지정 개체 만들기에 대한 자세한 내용은 [Marketo Engage 설명서](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하세요.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Custom-Objects)

## 영업 담당자

기본 CRM 통합이 활성화되어 있지 않을 때 Marketo에서 영업 사원 레코드 및 해당 리드 관계를 관리할 수 있습니다. 이러한 레코드에는 이름, 이메일 및 직책 등의 정보가 포함되어 있습니다. 영업 담당자가 리드를 소유하는 경우 이 정보를 필터링 및 토큰에 사용할 수 있습니다.

&quot;externalSalesPersonId&quot; 필드를 통해 잠재 고객 수준에서 영업 사원에 대한 관계를 관리합니다. [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST) API를 통해 이 필드를 업데이트하십시오.

관련 API: [REST](https://developer.adobe.com/marketo-apis/api/mapi#tag/Sales-Persons)
