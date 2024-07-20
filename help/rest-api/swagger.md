---
title: Swagger 정의 다운로드
feature: REST API, Programs
description: 로컬 사용을 위한 Swagger 정의 파일을 다운로드합니다.
source-git-commit: 85062243d57a3fc6d15251163e926495858edf2a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Swagger 정의 다운로드

[Swagger](https://swagger.io/) 또는 [OpenAPI](https://www.openapis.org/) 정의는 REST API의 모든 메서드와 매개 변수를 설명하는 데이터 파일입니다. 이러한 데이터 파일을 로컬에서 개인 API 참조로 다운로드하여 사용할 수 있습니다.

Marketo Engage Swagger/OpenAPI 정의를 사용하려면 각 문서의 `host` 필드를 Marketo Engage 인스턴스의 REST API 호스트 이름과 일치하도록 업데이트해야 합니다.

먼저 사용할 OpenAPI 정의를 다운로드합니다.

* [자산](assets/swagger-asset.json)
* [리드](assets/swagger-mapi.json)
* [ID          ](assets/swagger-identity.json)
* [사용자 관리](assets/swagger-user.json)

다음으로 Marketo 관리자로부터 REST API 호스트 이름을 가져옵니다. Marketo Engage의 _관리자_-> _웹 서비스_ 메뉴로 이동한 다음 끝점 필드에서 호스트 이름을 복사합니다. `hostname`은(는) 프로토콜 `https://`과(와) `/rest` 사이의 문자열이며 `AAA-999-AAA.mktorest.com`과(와) 비슷합니다.

텍스트 편집기에서 OpenAPI 파일을 열고 JSON에서 `host` 필드를 찾은 다음 해당 값을 REST API 호스트 이름 `"host":"localhost:8080"`에서 `"host":"AAA-999-AAA.mktorest.com"`(으)로 변경합니다.

저장되면 Swagger UI 인스턴스 또는 다른 OpenAPI 소프트웨어에서 정의 파일을 실행할 수 있습니다.
