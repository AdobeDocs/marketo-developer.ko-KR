---
title: 인증
feature: REST API
description: 2개의 legged OAuth 2.0으로 Marketo REST API를 인증하고, 액세스 토큰을 생성 및 사용하고, 인증 헤더로 전환하고, 만료를 관리하고, 601 및 602 오류를 처리합니다.
exl-id: f89a8389-b50c-4e86-a9e4-6f6acfa98e7e
TQID: https://experienceleague.adobe.com/cIeI0m61CyIWq4HEosZ-QAsxzZb0WcrQRpCud2qysfY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 519
ht-degree: 0%

---

# 인증

Marketo REST API는 인증을 위해 두 개의 OAuth 2.0을 사용합니다. 사용자 지정 서비스는 액세스 토큰을 얻는 데 사용되는 클라이언트 ID와 클라이언트 암호를 제공합니다.

각 사용자 정의 서비스는 API 전용 사용자에 속합니다. 사용자의 역할 및 권한은 서비스가 특정 작업을 수행하도록 승인합니다. 액세스 토큰은 단일 사용자 정의 서비스에 속하며 만료는 인스턴스의 다른 사용자 정의 서비스에 대한 토큰과 독립적입니다.

## 액세스 토큰 만들기

`Client ID` 및 `Client Secret`을(를) 찾으려면 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL LaunchPoint]**(으)로 이동하십시오. 사용자 지정 서비스를 선택한 다음 **[!UICONTROL View Details]**&#x200B;을(를) 선택합니다.

![REST 서비스 세부 정보 가져오기](assets/authentication-service-view-details.png)

![Launchpoint 자격 증명](assets/admin-launchpoint-credentials.png)

`Identity URL`을(를) 찾으려면 **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]**(으)로 이동합니다. URL이 REST API 섹션에 표시됩니다.

HTTP GET 또는 POST 요청으로 액세스 토큰 만들기:

```http
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

응답에는 다음 필드가 포함됩니다.

- `access_token`: 대상 인스턴스를 인증하기 위해 후속 호출로 전달하는 토큰입니다.
- `token_type`: OAuth 인증 방법입니다.
- `expires_in`: 현재 토큰의 남은 수명(초)입니다. 새 액세스 토큰의 수명은 3,600초 또는 1시간입니다.
- `scope`: 인증에 사용된 사용자 정의 서비스를 소유하고 있는 사용자입니다.

## 액세스 토큰 사용

모든 REST API 호출은 HTTP 헤더에 액세스 토큰을 포함해야 합니다.

>[!IMPORTANT]
>
>`access_token` 쿼리 매개 변수를 사용한 인증 지원이 2026년 8월 31일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 [인증 헤더](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/authentication#using-an-access-token)를 사용하도록 업데이트해야 합니다. 새 개발에서는 `Authorization` 헤더만 사용해야 합니다.

### 인증 헤더로 전환

`access_token` 쿼리 매개 변수를 인증 헤더로 바꾸려면 요청이 토큰을 보내는 방법을 업데이트하십시오.

다음 cURL 예제에서는 `-F` 플래그가 있는 양식 매개 변수로 `access_token` 값을 보냅니다.

```bash
curl ...  -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

다음 예제에서는 `-H` 플래그를 사용하여 `Authorization: Bearer` HTTP 헤더에 동일한 값을 보냅니다.

```bash
curl ... -H 'Authorization: Bearer <Access Token>' <REST API Endpoint Base URL>/bulk/v1/apiCall.json
```

## 팁 및 모범 사례

ID 응답의 액세스 토큰 및 만료 기간을 저장합니다. 토큰 만료를 관리하면 일반 작업 중 예기치 않은 인증 오류를 방지할 수 있습니다.

REST를 호출하기 전에 토큰의 남은 수명을 확인하십시오. 토큰이 만료되면 [Identity](https://developer.adobe.com/marketo-apis/api/identity/#tag/Identity/operation/identityUsingGET) 끝점을 호출하여 갱신합니다. 사전 예방적 갱신은 만료된 토큰으로 인한 실패를 방지하고 REST 호출 지연을 예측 가능하게 하므로 최종 사용자 대면 애플리케이션에 중요합니다.

인증 오류는 다음 코드를 반환합니다.

- `602`: 액세스 토큰이 만료되었습니다.
- `601`: 액세스 토큰이 잘못되었습니다.

클라이언트에서 코드를 받으면 ID 끝점을 호출하여 토큰을 갱신합니다.

토큰이 만료되기 전에 ID 끝점을 호출하는 경우 응답은 동일한 토큰과 나머지 수명을 반환합니다.

액세스 토큰은 사용자가 아닌 사용자 정의 서비스에 속합니다. 서로 다른 두 서비스의 자격 증명으로 인해 동일한 사용자에게 범위가 지정된 ID 응답이 생성되는 경우 액세스 토큰과 만료 기간은 독립적으로 유지됩니다.

응용 프로그램에서 여러 자격 증명 집합을 사용하는 경우 클라이언트 ID를 키로 사용하여 각 토큰을 독립적으로 관리합니다.
