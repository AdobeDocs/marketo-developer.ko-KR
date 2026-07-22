---
title: 필드
feature: REST API, Field Management
description: REST 및 SOAP 리드 필드 이름 지정, REST를 통한 목록 필드 리드 설명, 기능 매핑, sfdcId가 null인 이유 및 sfdcLeadId 또는 sfdcContactId를 사용하는 방법을 알아봅니다.
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
TQID: https://experienceleague.adobe.com/H2Bvhy-67U8JJ1V3JwYJ0O0vj4i11fwUCyYQtjxm8u0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 2%

---

# 필드

REST API 및 SOAP API는 리드 필드에 서로 다른 이름 지정 규칙을 사용합니다. 각 통합 기능에 필요한 필드 이름 규칙을 사용합니다.

## 필드 이름 목록 검색

REST &#39;Describe Lead&#39; 엔드포인트를 사용하여 리드 레코드에 대해 지원되는 모든 필드 이름을 검색합니다.

## 필드 이름 유형을 사용할 위치

필수 필드 이름 유형은 통합 기능에 따라 다릅니다. 다음 표는 각 기능이 REST 또는 SOAP 필드 이름을 사용하는지 여부를 식별합니다.

| 기능 | 사용할 필드 이름 유형 |
| --- | --- |
| 잠재 고객 추적 API(Munchkin) | SOAP |
| Forms 2.0 API | SOAP |
| 목록 가져오기(UI) | SOAP |
| 목록 가져오기(REST API) | 나머지 |
| 웹후크 응답 매핑 | SOAP |
| 이메일 스크립팅(속도) | SOAP |
| SOAP API | SOAP |
| REST API | 나머지 |

### REST API 필드 sfdcId가 항상 null 값을 반환하는 이유는 무엇입니까?

`sfdcId` 필드는 REST API의 원래 필드 맵에 포함된 수식 필드입니다. REST API를 통해 검색된 레코드는 수식 필드 값을 계산하지 않으므로 `sfdcId`은(는) 항상 null을 반환합니다.

SFDC ID를 검색하려면 `sfdcLeadId` 및 `sfdcContactId` 필드를 사용하십시오.
