---
title: REST API
feature: REST API
description: Marketo REST API를 사용하고, API 사용자 및 LaunchPoint를 설정하고, 할당량 및 한도를 보고, 인증 헤더로 인증하고, 리드를 검색하는 방법에 대해 알아봅니다.
exl-id: 4b9beaf0-fc04-41d7-b93a-a1ae3147ce67
TQID: https://experienceleague.adobe.com/GqhWI816wWX-2zf89wWj-GXpg9i615HRFVl2ljdYVj0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 765
ht-degree: 2%

---

# REST API

Marketo REST API는 다양한 시스템 기능에 대한 원격 액세스를 제공합니다. 프로그램을 만들고, 리드를 일괄적으로 가져오고, 세부 수준에서 Marketo 인스턴스를 제어하는 데 사용할 수 있습니다.

REST API는 다음 두 가지 광범위한 범주로 분류됩니다.

- [리드 데이터베이스](https://developer.adobe.com/marketo-apis/api/mapi) API는 Marketo 사용자 레코드 및 관련 개체 유형(예: Opportunities 및 Company)을 검색하고 상호 작용합니다.
- [자산](https://developer.adobe.com/marketo-apis/api/asset) API는 마케팅 자료 및 워크플로우 관련 레코드와 상호 작용합니다.

>[!NOTE]
>
>SOAP API는 더 이상 사용되지 않으며 2026년 7월 31일 이후부터 더 이상 사용할 수 없습니다. 모든 새 개발은 Marketo [REST API](./rest-api.md)를 사용하여 수행해야 하며, 서비스가 중단되지 않도록 기존 서비스를 해당 날짜까지 마이그레이션해야 합니다. SOAP API를 사용하는 서비스가 있는 경우 마이그레이션 방법에 대한 자세한 내용은 SOAP API [마이그레이션 안내서](../soap-api/migration.md)를 참조하십시오.
>

>[!IMPORTANT]
>
>API 게이트웨이 URL에서 이중 슬래시를 사용하지 않는 방법은 이 [전국 게시물](https://nation.marketo.com/t5/product-blogs/rest-api-double-slash-deprecation/ba-p/358616)을 참조하세요.
>

- **일일 할당량:** 각 구독에는 하루에 50,000개의 API 호출이 할당됩니다. 할당량은 매일 오전 12:00(CST)에 재설정됩니다. 일일 할당량을 늘리려면 계정 관리자에게 문의하십시오.
- **속도 제한:** 각 인스턴스는 20초당 100개의 API 호출로 제한됩니다.
- **동시 실행 제한:** 각 인스턴스는 최대 10개의 동시 API 호출을 허용합니다.

표준 API 호출의 최대 URI 길이는 8KB이고 최대 본문 크기는 1MB입니다. 벌크 API 호출은 최대 본문 크기 10MB를 지원합니다.

호출에 오류가 포함되어 있는 경우 API는 일반적으로 여전히 HTTP 상태 코드 200을 반환합니다. JSON 응답에 값이 `false`인 `success` 구성원이 포함되어 있고 `errors` 구성원에 오류가 배열되었습니다. 오류에 대한 자세한 내용은 [여기](error-codes.md)를 참조하세요.

## 시작하기

다음 단계를 완료하려면 Marketo 인스턴스에서 관리자 권한이 필요합니다. 이 워크플로우는 API 자격 증명을 만들고 이를 사용하여 잠재 고객 레코드를 검색합니다.

먼저 API 사용자를 만들고 인증된 호출에 대한 자격 증명을 가져옵니다. 인스턴스에 로그인하고 **[!UICONTROL Admin]** > **[!UICONTROL Users and Roles]**(으)로 이동합니다.

![관리자 사용자 및 역할](assets/admin-users-and-roles.png)

**[!UICONTROL Roles]** 탭을 선택한 다음 새 역할을 선택합니다. Access API 그룹에서 &quot;읽기 전용 리드&quot;(또는 &quot;읽기 전용 사용자&quot;) 이상의 권한을 역할에 할당합니다. 역할에 수사적 이름을 지정하고 **[!UICONTROL Create]**&#x200B;을(를) 선택합니다.

![새 역할](assets/new-role.png)

[!UICONTROL Users] 탭으로 돌아가서 **[!UICONTROL Invite New User]**&#x200B;을(를) 선택합니다. 사용자를 API 사용자로 식별하는 수사적 이름을 입력하고 전자 메일 주소를 입력한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![새 사용자 정보](assets/new-user-info.png)

[!UICONTROL API Only] 옵션을 선택하고 만든 API 역할을 할당한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![새 사용자 권한](assets/new-user-permissions.png)

사용자를 만들려면 **[!UICONTROL Send]**&#x200B;을(를) 선택하십시오.

![새 사용자 메시지](assets/new-user-message.png)

그런 다음 [!UICONTROL Admin] 메뉴로 이동하여 **[!UICONTROL LaunchPoint]**&#x200B;을(를) 선택합니다.

![시작 지점](assets/admin-launchpoint.png)

**[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;을(를) 선택합니다. 설명 이름과 설명을 입력하고 [!UICONTROL Service] 메뉴에서 **[!UICONTROL Custom]**&#x200B;을(를) 선택합니다. [!UICONTROL API Only User] 메뉴에서 새 사용자를 선택한 다음 **[!UICONTROL Create]**&#x200B;을(를) 선택합니다.

![새 Launchpoint 서비스](assets/admin-launchpoint-new-service.png)

클라이언트 ID 및 클라이언트 암호에 액세스하려면 새 서비스에 대해 **[!UICONTROL View Details]**&#x200B;을(를) 선택하십시오. 1시간 동안 유효한 액세스 토큰을 생성하려면 **[!UICONTROL Get Token]**&#x200B;을(를) 선택하십시오. 첫 번째 API 호출에 대한 토큰을 저장합니다.

![토큰 가져오기](assets/get-token.png)

**[!UICONTROL Admin]** > **[!UICONTROL Web Services]**(으)로 이동합니다.

![웹 서비스](assets/admin-web-services.png)

REST API 상자에서 [!UICONTROL Endpoint]을(를) 찾아 첫 번째 API 호출에 저장합니다.

![REST 끝점](assets/admin-web-services-rest-endpoint-1.png)

모든 REST API 호출은 HTTP 헤더에 액세스 토큰을 포함해야 합니다.

```text
Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int
```

>[!IMPORTANT]
>
>**access_token** 쿼리 매개 변수를 사용하는 인증 지원이 2025년 6월 30일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 **인증** 헤더를 사용하도록 업데이트해야 합니다. 새 개발에서는 **Authorization** 헤더만 사용해야 합니다.

새 브라우저 탭을 열고 다음 URL을 입력합니다. 자리 표시자를 [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/getLeadsByFilterUsingGET)를 호출할 인스턴스의 끝점 및 전자 메일 주소로 바꿉니다.

```text
<Your Endpoint URL>/rest/v1/leads.json?&filterType=email&filterValues=<Your Email Address>
```

데이터베이스에 전자 메일 주소가 포함된 잠재 고객 레코드가 없는 경우 기존 잠재 고객의 전자 메일 주소를 사용하십시오. URL을 제출하여 다음 예제와 유사한 JSON 응답을 받습니다.

```json
{
    "requestId":"c493#1511ca2b184",
    "result":[
       {
           "id":1,
           "updatedAt":"2015-08-24T20:17:23Z",
           "lastName":"Elkington",
           "email":"developerfeedback@marketo.com",
           "createdAt":"2013-02-19T23:17:04Z",
           "firstName":"Kenneth"
        }
    ],
    "success":true
}
```

## API 사용 정보

API 사용 보고서는 각 API 사용자를 개별적으로 추적합니다. 각 웹 서비스에 별도의 사용자를 할당하면 각 통합의 API 사용을 식별하는 데 도움이 됩니다.

호출이 인스턴스 제한을 초과하고 후속 호출이 실패할 경우 보고서를 사용하여 각 서비스의 호출 볼륨을 식별합니다. **[!UICONTROL Admin]** > **[!UICONTROL Integration]** > **[!UICONTROL Web Services]**(으)로 이동한 다음 지난 7일 동안의 통화 수를 선택합니다.

일별 및 마지막 7일 사용 및 오류 통계를 반환하는 REST 끝점에 대해서는 [사용](usage.md)을 참조하십시오.
