---
title: 필드
feature: REST API, Field Management
description: REST 및 SOAP 리드 필드 이름 지정, REST를 통한 목록 필드 리드 설명, 기능 매핑, sfdcId가 null인 이유 및 sfdcLeadId 또는 sfdcContactId를 사용하는 방법을 알아봅니다.
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 2%

---

# 필드

REST API 및 SOAP API는 리드 필드에 서로 다른 이름 지정 규칙을 사용합니다.

## 필드 이름 목록 검색

REST &#39;Describe Lead&#39; 엔드포인트를 사용하여 리드 레코드에서 사용할 수 있는 모든 지원되는 필드 이름 목록을 검색합니다.

## 필드 이름 유형을 사용할 위치

특정 통합 관련 기능을 활용할 때 사용해야 하는 필드 이름 유형을 알기 어려운 경우가 있습니다. 다음은 REST 또는 SOAP 필드 이름 유형을 사용하는 기능에 대한 빠른 참조입니다.

| 기능 | 사용할 필드 이름 유형 |
|--- |--- |
| 잠재 고객 추적 API(Munchkin) | SOAP |
| Forms 2.0 API | SOAP |
| 목록 가져오기(UI) | SOAP |
| 목록 가져오기(REST API) | 나머지 |
| 웹후크 응답 매핑 | SOAP |
| 이메일 스크립팅(속도) | SOAP |
| SOAP API | SOAP |
| REST API | 나머지 |

### REST API 필드 sfdcId가 항상 null 값을 반환하는 이유는 무엇입니까?

필드 `sfdcId`은(는) REST API의 원래 필드 맵에 잘못 포함된 수식 필드입니다. REST API를 통해 검색된 레코드는 공식 필드의 값을 계산하지 않으므로 값은 항상 null입니다. 실제 SFDC ID를 캡처하려면 `sfdcLeadId` 및 `sfdcContactId` 필드를 사용해야 합니다.
