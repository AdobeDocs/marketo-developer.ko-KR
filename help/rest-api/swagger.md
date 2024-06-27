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

[Swagger](https://swagger.io/) 또는 [오픈 API](https://www.openapis.org/) 정의는 REST API의 모든 메서드 및 매개 변수를 설명하는 데이터 파일입니다. 이러한 데이터 파일을 로컬에서 개인 API 참조로 다운로드하여 사용할 수 있습니다.

Marketo Engage Swagger/OpenAPI 정의를 사용하려면 `host` Marketo Engage 인스턴스의 REST API 호스트 이름과 일치하도록 각 문서의 필드를 업데이트해야 합니다.

먼저 사용할 OpenAPI 정의를 다운로드합니다.

* [자산](assets/swagger-asset.json)
* [리드](assets/swagger-mapi.json)
* [ID          ](assets/swagger-identity.json)
* [사용자 관리](assets/swagger-user.json)

다음으로 Marketo 관리자로부터 REST API 호스트 이름을 가져옵니다. 로 이동 _관리자_-> _웹 서비스_ Marketo Engage의 메뉴를 클릭하고 끝점 필드에서 호스트 이름을 복사합니다. 다음 `hostname` 는 프로토콜 사이의 문자열입니다. `https://`, 및 `/rest`, 다음과 같음 `AAA-999-AAA.mktorest.com`

텍스트 편집기에서 OpenAPI 파일을 열고 `host` json의 필드 및 값을 REST API 호스트 이름으로 변경합니다. `"host":"localhost:8080"` 끝 `"host":"AAA-999-AAA.mktorest.com"`.

저장되면 Swagger UI 인스턴스 또는 다른 OpenAPI 소프트웨어에서 정의 파일을 실행할 수 있습니다.
