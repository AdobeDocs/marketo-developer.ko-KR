---
title: Marketo 개체
feature: SOAP
description: 영업 기회, 프로그램 및 관련 레코드에 대한 유형, 속성, 외부 키 동작 및 지원되는 SOAP API를 포함한 Marketo MObject에 대한 개요입니다.
exl-id: 99b9aed4-94e8-46e8-84d9-2cc5215b0c13
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Marketo 개체

Marketo은 Marketo 개체(MObjects)를 사용하여 Program, Opportunity 및 OpportunityPersonRole과 같은 다양한 클래스를 나타냅니다.

## 개체의 구조

개체는 표준, 사용자 지정 또는 가상, 이렇게 세 가지 유형 중 하나일 수 있습니다. 표준 및 사용자 지정 MObject는 Lead 또는 Company와 같은 고유한 엔티티를 나타내고 LeadRecord와 같은 가상 객체는 하나 이상의 객체의 필드로 구성됩니다. 가상 개체는 API 내에서 사용되는 편의 개체이지만 Marketo 애플리케이션 내에는 없습니다.

MObject는 다음으로 구성됩니다.

- 모든 오브젝트에 공통되는 작은 고정 속성 세트
   - 필수 유형
   - 선택적 externalKey
   - 읽기 전용 id, createdAt, updatedAt
- 하나 이상의 객체별 속성 목록(이름/값 쌍)이며 일부는 필요할 수 있습니다. 예를 들어 Opportunity에 이름을 지정합니다.
- 개체 이름과 더하기 형식의 연결된 개체 참조 목록
   - Marketo ID 또는
   - 속성-이름/속성-값 쌍으로서의 외부 키.

### 외부 키

외부 키는 Lead 또는 Opportunity 와 같이 Marketo 객체에 정의된 사용자 정의 필드입니다. 이름은 필드 이름이고 값은 외부 시스템에서 생성된 필드 값입니다. **Marketo에서는 이러한 값에 대해 UNIQUE 제약 조건을 적용하지 않습니다.** 값이 고유한지 확인하는 것은 API 사용자의 책임입니다. 중복이 발생하면 Marketo에서 가장 최근에 추가된 개체를 사용합니다. 이는 이메일 주소 표준 필드의 동작과 유사합니다.

### 사용 가능한 API

| API | 다음에서 작동 가능 |
|---|---|
| describeMObject | ActivityRecord, LeadRecord, Opportunity, OpportunityPerson역할 |
| getMObjects | 영업 기회, OpportunityPersonRole, 프로그램 |
| syncMObjects | 영업 기회, OpportunityPersonRole, 프로그램 |
| deleteMObject | 영업 기회, OpportunityPersonRole |
| listMObjects | ActivityRecord, LeadRecord, Opportunity, OpportunityPerson역할 |
