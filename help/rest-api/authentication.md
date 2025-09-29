---
title: 인증
feature: REST API
description: 2개의 legged OAuth 2.0으로 Marketo REST API를 인증하고, 액세스 토큰을 생성 및 사용하고, 인증 헤더로 전환하고, 만료를 관리하고, 601 및 602 오류를 처리합니다.
exl-id: f89a8389-b50c-4e86-a9e4-6f6acfa98e7e
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# 인증

Marketo의 REST API는 2개의 레그 OAuth 2.0으로 인증됩니다. 클라이언트 ID 및 클라이언트 암호는 사용자가 정의하는 사용자 정의 서비스에서 제공합니다. 각 사용자 정의 서비스는 서비스가 특정 작업을 수행하도록 권한을 부여하는 역할 및 권한 집합을 가진 API 전용 사용자가 소유합니다. 액세스 토큰은 단일 사용자 정의 서비스에 연결됩니다. 액세스 토큰 만료는 인스턴스에 있을 수 있는 다른 사용자 지정 서비스와 연결된 토큰과 독립적입니다.

## 액세스 토큰 만들기

사용자 지정 서비스를 선택하고 `Client ID`을(를) 클릭하여 `Client Secret` > **[!UICONTROL Admin]** > **[!UICONTROL Integration]** 메뉴에서 **[!UICONTROL LaunchPoint]** 및 **[!UICONTROL View Details]**&#x200B;을(를) 찾을 수 있습니다.

![REST 서비스 세부 정보 가져오기](assets/authentication-service-view-details.png)

![Launchpoint 자격 증명](assets/admin-launchpoint-credentials.png)

`Identity URL`은(는) REST API 섹션의 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]** 메뉴에 있습니다.

다음과 같이 HTTP GET(또는 POST) 요청을 사용하여 액세스 토큰을 만듭니다.

```
GET <Identity URL>/oauth/token?grant_type=client_credentials&client_id=<Client Id>&client_secret=<Client Secret>
```

요청이 유효한 경우 다음과 유사한 JSON 응답을 받게 됩니다.

```json
{
    "access_token": "cdf01657-110d-4155-99a7-f986b2ff13a0:int",
    "token_type": "bearer",
    "expires_in": 3599,
    "scope": "apis@acmeinc.com"
}
```

응답 정의

- `access_token` - 대상 인스턴스를 인증하기 위해 후속 호출로 전달하는 토큰입니다.
- `token_type` - OAuth 인증 방법입니다.
- `expires_in` - 현재 토큰의 남은 수명(초)입니다(그 이후에는 유효하지 않음). 액세스 토큰이 원래 생성될 때 그 수명은 3600초 또는 1시간이다.
- `scope` - 인증에 사용된 사용자 지정 서비스의 소유 사용자입니다.

## 액세스 토큰 사용

REST API 메서드를 호출할 때 호출이 성공하려면 모든 호출에 액세스 토큰을 포함해야 합니다.
액세스 토큰은 HTTP 헤더로 전송해야 합니다.

>[!IMPORTANT]
>
>`access_token` 쿼리 매개 변수를 사용한 인증 지원이 2026년 1월 31일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 [인증 헤더](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/rest/authentication#using-an-access-token)를 사용하도록 업데이트해야 합니다. 새 개발에서는 `Authorization` 헤더만 사용해야 합니다.

### 인증 헤더로 전환

`access_token` 쿼리 매개 변수를 사용에서 인증 헤더로 전환하려면 작은 코드 변경이 필요합니다.

CURL을 예로 들면 이 코드는 `access_token` 값을 양식 매개 변수로 보냅니다(-F 플래그).

```bash
curl ...  -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

이 코드는 `Authorization: Bearer` http 헤더와 동일한 값(-H 플래그)을 보냅니다.

```bash
curl ... -H 'Authorization: Bearer <Access Token>' <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

## 팁 및 모범 사례

통합이 원활하게 작동하고 정상 작동 중에 예기치 않은 인증 오류가 발생하지 않도록 하려면 액세스 토큰 만료 관리가 중요합니다. 통합을 위한 인증을 디자인할 때 ID 응답에 포함된 토큰과 만료 기간을 저장해야 합니다.

REST 호출을 수행하기 전에 토큰의 남은 수명을 기준으로 토큰의 유효성을 확인해야 합니다. 토큰이 만료되면 [Identity](https://developer.adobe.com/marketo-apis/api/identity/#tag/Identity/operation/identityUsingGET) 끝점을 호출하여 갱신합니다. 이렇게 하면 만료된 토큰으로 인해 REST 호출이 실패하지 않도록 하는 데 도움이 됩니다. 이를 통해 최종 사용자 대면 애플리케이션에 중요한 예측 가능한 방식으로 REST 호출 지연을 관리할 수 있습니다.

만료된 토큰을 사용하여 REST 호출을 인증하면 REST 호출이 실패하고 602 오류 코드를 반환합니다. REST 호출을 인증하는 데 잘못된 토큰이 사용되는 경우 601 오류 코드가 반환됩니다. 이러한 코드 중 하나를 받으면 클라이언트는 ID 끝점을 호출하여 토큰을 갱신해야 합니다.

토큰이 만료되기 전에 ID 끝점을 호출하는 경우 동일한 토큰과 남은 수명이 응답에서 반환됩니다.

액세스 토큰은 사용자 단위가 아닌 사용자 정의 서비스 단위로 소유합니다. 두 개의 ID 응답이 동일한 사용자에게 범위가 지정될 수 있지만 두 개의 다른 서비스에서 만든 자격 증명으로 액세스 토큰과 만료 기간이 만들어진 경우에는 서로 독립적입니다. 동일한 애플리케이션에 자격 증명 세트가 여러 개 있는 경우 이 점을 염두에 두십시오. 클라이언트 ID는 이러한 세트를 독립적으로 관리하는 데 유용한 키가 될 수 있습니다.
