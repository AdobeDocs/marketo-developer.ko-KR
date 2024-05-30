---
title: "기본 URL"
feature: REST API
description: "Marketo용 URL을 사용하는 방법을 설명합니다."
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 기본 URL

다음 [끝점 참조](endpoint-reference.md) 각 API 호출에 대한 설명서에는 요청을 형성하기 위해 기본 URL에 추가해야 하는 REST 메서드, 경로, 리소스 및 매개 변수가 표시됩니다.

다음은 올바른 형식의 REST URL의 예입니다.

`https://284-RPR-133.mktorest.com/rest/v1/lead/318581.json?fields=email,firstName,lastName`

다음 부품으로 구성됩니다.

- 기본 URL: `https://284-RPR-133.mktorest.com/rest`
- 경로: `/v1/lead/`
- 리소스: `318582.json`
- 쿼리 매개 변수: `fields=email,firstName,lastName`

기본 URL은 계정 ID(Munchkin ID라고도 함)를 포함하므로 각 Marketo 구독에 대해 고유합니다. 기본 URL은 Marketo에 로그인한 다음 로 이동하여 찾습니다. **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]** 메뉴 아래의 제품에서 사용할 수 있습니다. 다음 스크린샷에 표시된 대로 &quot;REST API&quot; 섹션 아래에 &quot;Endpoint:&quot;로 레이블이 지정됩니다.

![웹 서비스 기본 URL 끝점](assets/rest-api-base-url-web-services.png)

기본 URL을 찾으면 이를 복사하여 REST API를 호출할 때 사용하는 URL에 포함합니다.
