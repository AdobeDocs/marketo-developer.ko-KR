---
title: 사용자 지정 개체
feature: SOAP
description: 사용자 지정 개체 만들기
exl-id: 29d65841-4b44-4d94-b14e-c583d433d015
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 사용자 지정 개체

Marketo 사용자 지정 개체를 사용하면 Marketo 리드와 사용자 지정 개체 레코드 간에 일대다 관계를 만들 수 있습니다. 예를 들어 잠재 고객이 참석하는 모든 로드쇼를 추적할 수 있습니다. 잠재 고객이 여러 해에 걸쳐 여러 로드쇼에 참가할 수 있으므로 사용자 정의 객체가 이 정보를 저장하는 데 더 적합합니다.

사용자 지정 오브젝트는 Spark를 제외한 모든 Marketo 버전에서 지원됩니다. Marketo 사용자 지정 개체가 계정에 성공적으로 프로비저닝되면 다음을 수행할 수 있습니다.

- Marketo SOAP API를 통해 사용자 지정 개체에서 레코드 만들기/읽기/업데이트/삭제
- 새 레코드가 사용자 지정 개체에 추가될 때 스마트 목록 트리거 사용
- 스마트 목록에서 사용자 지정 개체 데이터를 필터로 사용
- Marketo 이메일 스크립팅을 사용하여 이메일에 사용자 지정 개체 데이터 사용

## 사용자 지정 개체의 구조

사용자 정의 객체는 다음과 같이 구성됩니다.

- 모든 사용자 지정 개체에 공통되는 작은 고정 특성 집합입니다.
   - 객체 이름(예: 객체 유형 이름)
   - 개체 설명
   - Marketo 잠재 고객 링크 필드 이름에 대한 사용자 지정 개체 - 사용자 지정 개체가 참조하는 잠재 고객 (개인) 개체의 필드입니다.
   - 개체 키 필드 이름 - 개체에서 사용하는 기본 키
- 하나 이상의 오브젝트별 필드(이러한 필드는 최대 50개까지 지원)

## 사용자 지정 개체 작업

다음 호출은 CO와 상호 작용하는 데 사용할 수 있습니다.

- [getCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/getCustomObjectsUsingGET)
- [syncCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST)
- [deleteCustomObjects](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/deleteCustomObjectsUsingPOST)
