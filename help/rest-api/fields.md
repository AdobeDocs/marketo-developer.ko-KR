---
title: "필드"
feature: REST API, Field Management
description: "지원되는 필드 이름 목록입니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---


# 필드

REST API 및 SOAP API는 리드 필드에 대해 서로 다른 이름 지정 규칙을 사용합니다.

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

필드 `sfdcId` 는 REST API에 대한 원래 필드 맵에 잘못 포함된 공식 필드입니다. REST API를 통해 검색된 레코드는 공식 필드의 값을 계산하지 않으므로 값은 항상 null입니다. 실제 SFDC ID를 캡처하려면 다음 필드를 사용해야 합니다 `sfdcLeadId` 및 `sfdcContactId`.
