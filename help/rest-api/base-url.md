---
title: 기본 URL
feature: REST API
description: Marketo REST API 요청을 빌드하고, 기본 URL 경로 리소스 및 매개 변수를 이해하고, 고유한 기본 URL을 찾는 방법에 대해 알아봅니다.
exl-id: 6c3f122c-3ace-4ed3-bed0-a6b89cedc99a
TQID: https://experienceleague.adobe.com/NZisV6V-FMPi0RHpdaFrc1kZc3nb15YomwRgohaQmEE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 3%

---

# 기본 URL

[끝점 참조](endpoint-reference.md)의 각 API 호출은 REST 메서드, 경로, 리소스 및 매개 변수를 지정합니다. 이러한 구성 요소를 기본 URL에 추가하여 요청을 구성합니다.

다음은 올바른 형식의 REST URL의 예입니다.

`https://284-RPR-133.mktorest.com/rest/v1/lead/318581.json?fields=email,firstName,lastName`

이 예에는 다음 구성 요소가 포함되어 있습니다.

- **기본 URL:** `https://284-RPR-133.mktorest.com/rest`
- **경로:** `/v1/lead/`
- **리소스:** `318582.json`
- **쿼리 매개 변수:** `fields=email,firstName,lastName`

기본 URL은 Munchkin ID라고도 하는 계정 ID를 포함하며 각 Marketo 구독에 대해 고유합니다.

기본 URL을 찾으려면 Marketo에 로그인하고 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]**(으)로 이동합니다. 기본 URL은 다음 이미지에 표시된 대로 &quot;REST API&quot; 섹션에서 &quot;Endpoint:&quot; 레이블이 지정됩니다.

![웹 서비스 기본 URL 끝점](assets/rest-api-base-url-web-services.png)

기본 URL을 복사하여 각 REST API 호출의 URL에 포함합니다.
