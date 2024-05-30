---
title: "끝점 참조"
feature: REST API
description: "Marketo API 끝점 참조"
source-git-commit: 2454f126dc4275697ef6773420453ad8853eae73
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# 끝점 참조

- [자산](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [잠재 고객 데이터베이스](https://developer.adobe.com/marketo-apis/api/mapi/)
- [사용자 관리](https://developer.adobe.com/marketo-apis/api/user/)

## 끝점 참조

Marketo은 Swagger를 사용하여 REST API에 대한 공용 인터페이스의 공식 정의를 제공합니다. Swagger는 URL 구조, 요청 모델 및 응답 모델에 대한 풍부한 정의 모델을 제공하며 API 상호 작용, 테스트 및 클라이언트 생성에 사용할 수 있는 도구 에코시스템을 개발했습니다.

끝점 참조는 [Swagger-UI](https://swagger.io/tools/swagger-ui/) 클라이언트측에서 참조 페이지를 생성하는 JavaScript 패키지 각 공개 엔드포인트가 나열되고 필요한 경우 응답 모델, 필수 요청 매개 변수 및 요청 모델의 구조를 제공합니다.

## Marketo의 Swagger 정의 사용

Swagger 표준에서는 호스트를 제공하거나 파일을 제공하는 호스트에서 호스트를 생성해야 합니다. Marketo에서 정의에 빈 호스트 매개 변수를 제공하므로 기존 도구를 사용하기 전에 정의에서 호스트를 수정하는 것이 중요합니다. 각 Marketo 인스턴스에 대한 REST API 호스트는 고유하며, 다음 패턴을 따릅니다.

`{Munchkin ID}.mktorest.com`

## 자산 API

Marketo Asset API 사용 `application/x-www-url-formencoded` POST 메서드가 필요한 끝점에 대한 요청의 스타일 매개 변수입니다. 그러나 폴더 매개 변수와 같은 일부 경우에는 매개 변수에 대한 값이 JSON 배열 또는 개체일 수 있습니다. 이러한 매개 변수는 끝점 참조에 기록됩니다.
