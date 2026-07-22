---
title: JAVASCRIPT API
description: Munchkin 리드 추적, Forms 2.0, Web Personalization 및 Predictive Content에 대해 포함 코드와 함께 Marketo JavaScript API를 사용하는 방법을 알아봅니다.
feature: Munchkin Tracking Code, Forms, Web Personalization, Predictive Content, Social, Javascript
exl-id: 6129a467-be44-44bd-9e02-62009070c318
TQID: https://experienceleague.adobe.com/R9kIFBiH6jc64ay85QkumV7jCsFnj9J0t5G4IJKEsJM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 1%

---

# Javascript API

Marketo 클라이언트측 JavaScript 통합은 리드 추적, 양식, 웹 개인화 및 예측 콘텐츠 기능을 제공합니다. 이러한 기능을 사용하려면 Marketo 계정이 있어야 합니다.

구현에는 일반적으로 웹 속성에 포함 코드 추가가 포함됩니다. 포함 코드에 의해 노출된 JavaScript 함수를 호출하여 기능을 추가할 수도 있습니다.

포함 코드에는 계정 식별자가 포함되어 있으므로 Marketo 인스턴스에는 고유합니다. Marketo 사용자 인터페이스에서 해당 패널로 이동하여 포함 코드를 클립보드에 복사한 다음 웹 페이지에 붙여 넣습니다.

## 잠재 고객 추적(Munchkin)

Marketo의 [Munchkin JavaScript 추적 코드](lead-tracking.md)은(는) 웹 사이트 방문에서 리드를 생성합니다. 또한 개인 정보를 제공하지 않은 방문자를 추적하고 사용자의 IP 주소 및 기타 정보를 포함하는 익명 리드를 생성합니다.

Munchkin의 관리 영역에 있는 Munchkin 페이지에서 Marketo을 설정합니다.

## Forms 2.0

[Forms 2.0](forms-api-reference.md)을(를) 사용하면 마케터가 프로그래밍 지식 없이도 웹 양식을 만들 수 있습니다. Forms은 Marketo 랜딩 페이지에 있거나 웹 사이트의 모든 페이지에 임베드될 수 있습니다.

Forms 2.0 JavaScript API를 사용하여 Marketo 웹 양식의 핵심 기능을 확장할 수 있습니다.

## 웹 개인화

[Marketo Web Personalization](web-personalization.md)을 통해 잠재 고객의 신원과 활동 내용에 따라 웹 사이트에서 잠재 고객을 실시간으로 참여시킬 수 있습니다.

## 예측 콘텐츠

[Marketo 예측 콘텐츠](predictive-content.md)는 기계 학습 및 예측 분석을 사용하여 웹 방문자에게 관련 콘텐츠를 표시합니다. 콘텐츠에 텍스트 설명 및 이미지를 추가하고 웹 사이트에 여러 콘텐츠 권장 사항을 임베드합니다.
