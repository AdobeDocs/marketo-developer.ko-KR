---
title: REST API
feature: REST API
description: REST API 개요
exl-id: 4b9beaf0-fc04-41d7-b93a-a1ae3147ce67
source-git-commit: 8ad3e3f0958ea705375651b1c8a75967d807ca80
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# REST API

Marketo은 시스템 기능 중 대부분을 원격으로 실행할 수 있도록 하는 REST API를 노출합니다. 프로그램 제작에서 리드 일괄 가져오기에 이르기까지 Marketo 인스턴스를 세밀하게 제어할 수 있는 많은 옵션이 있습니다.

이러한 API는 일반적으로 [리드 데이터베이스](https://developer.adobe.com/marketo-apis/api/mapi/) 및 [에셋](https://developer.adobe.com/marketo-apis/api/asset/)의 두 가지 광범위한 범주에 속합니다. 잠재 고객 데이터베이스 API를 사용하면 Marketo 개인 레코드 및 관련 객체 유형(예: 영업 기회 및 회사)을 검색하고 상호 작용할 수 있습니다. 에셋 API를 사용하면 마케팅 자료 및 워크플로우 관련 레코드와 상호 작용할 수 있습니다.

>[!NOTE]
>SOAP API는 더 이상 사용되지 않으며 2025년 10월 31일 이후부터 더 이상 사용할 수 없습니다. 모든 새 개발은 Marketo [REST API](./rest-api.md)를 사용하여 수행해야 하며, 서비스가 중단되지 않도록 기존 서비스를 해당 날짜까지 마이그레이션해야 합니다. SOAP API를 사용하는 서비스가 있는 경우 마이그레이션 방법에 대한 자세한 내용은 SOAP API [마이그레이션 안내서](../soap-api/migration.md)를 참조하십시오.
>

- **일일 할당량:** 구독에는 하루에 50,000개의 API 호출이 할당됩니다(매일 오전 12시(CST) 재설정됨). 계정 관리자를 통해 일일 할당량을 늘릴 수 있습니다.
- 인스턴스당 **속도 제한:** API 액세스가 20초당 100개의 호출로 제한됩니다.
- **동시 실행 제한:**  최대 10개의 동시 API 호출.

표준 호출의 크기는 URI 길이 8KB, 본문 크기가 1MB로 제한되지만 본문은 벌크 API의 경우 10MB일 수 있습니다. 호출에 오류가 있는 경우 API는 일반적으로 상태 코드 200을 반환하지만 JSON 응답에는 값이 `false`인 &quot;성공&quot; 멤버와 &quot;오류&quot; 멤버의 오류 배열이 포함됩니다. 오류 [여기](error-codes.md)에 대한 자세한 정보.

## 시작하기

다음 단계에는 Marketo 인스턴스에서 관리자 권한이 필요합니다.

Marketo에 대한 첫 번째 호출의 경우 리드 레코드를 검색합니다. Marketo 작업을 시작하려면 인스턴스에 대해 인증된 호출을 수행하기 위한 API 자격 증명을 획득해야 합니다. 인스턴스에 로그인하고 **[!UICONTROL Admin]** -> **[!UICONTROL Users and Roles]**(으)로 이동합니다.

![관리자 사용자 및 역할](assets/admin-users-and-roles.png)

**[!UICONTROL Roles]** 탭을 클릭한 다음 새 역할을 클릭하고 Access API 그룹의 역할에 적어도 &quot;읽기 전용 리드&quot;(또는 &quot;읽기 전용 사용자&quot;) 권한을 할당합니다. 수사적 이름을 지정하고 **[!UICONTROL Create]**&#x200B;을(를) 클릭하십시오.

![새 역할](assets/new-role.png)

이제 [!UICONTROL Users] 탭으로 돌아가서 **[!UICONTROL Invite New User]**&#x200B;을(를) 클릭합니다. 사용자에게 API 사용자임을 나타내는 수사적 이름과 전자 메일 주소를 지정하고 **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.

![새 사용자 정보](assets/new-user-info.png)

그런 다음 [!UICONTROL API Only] 옵션을 선택하고 만든 API 역할을 사용자에게 부여한 다음 **[!UICONTROL Next]**&#x200B;을(를) 클릭합니다.

![새 사용자 권한](assets/new-user-permissions.png)

사용자 만들기 프로세스를 완료하려면 **[!UICONTROL Send]**&#x200B;을(를) 클릭하십시오.

![새 사용자 메시지](assets/new-user-message.png)

[!UICONTROL Admin] 메뉴로 이동한 다음 **[!UICONTROL LaunchPoint]**&#x200B;을(를) 클릭합니다.

![시작 지점](assets/admin-launchpoint.png)

**[!UICONTROL New]** 메뉴를 클릭하고 **[!UICONTROL New Service]**&#x200B;을(를) 선택합니다. 서비스에 수사적 이름을 지정하고 [!UICONTROL Service] 드롭다운 메뉴에서 **[!UICONTROL Custom]**&#x200B;을(를) 선택합니다. 설명을 입력한 다음 [!UICONTROL API Only User] 드롭다운 메뉴에서 새 사용자를 선택하고 **[!UICONTROL Create]**&#x200B;을(를) 클릭합니다.

![새 Launchpoint 서비스](assets/admin-launchpoint-new-service.png)

새 서비스에 대한 **[!UICONTROL View Details]**&#x200B;을(를) 클릭하여 클라이언트 ID 및 클라이언트 암호에 액세스합니다. 지금은 **[!UICONTROL Get Token]** 단추를 클릭하여 1시간 동안 사용할 수 있는 액세스 토큰을 생성할 수 있습니다. 지금은 메모에 토큰을 저장합니다.

![토큰 가져오기](assets/get-token.png)

**[!UICONTROL Admin]** 메뉴로 이동한 다음 **[!UICONTROL Web Services]**(으)로 이동합니다.

![웹 서비스](assets/admin-web-services.png)

REST API 상자에서 [!UICONTROL Endpoint]을(를) 찾아 메모에 저장합니다.

![REST 끝점](assets/admin-web-services-rest-endpoint-1.png)

REST API 메서드를 호출할 때 호출이 성공하려면 모든 호출에 액세스 토큰을 포함해야 합니다. 액세스 토큰은 HTTP 헤더로 전송해야 합니다.

```
Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int
```

>[!IMPORTANT]
>
>**access_token** 쿼리 매개 변수를 사용하는 인증 지원이 2025년 6월 30일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 **인증** 헤더를 사용하도록 업데이트해야 합니다. 새 개발에서는 **Authorization** 헤더만 사용해야 합니다.

새 브라우저 탭을 열고 다음 정보를 입력하여 [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET)를 호출합니다.

```
<Your Endpoint URL>/rest/v1/leads.json?&filterType=email&filterValues=<Your Email Address>
```

데이터베이스에 전자 메일 주소가 있는 잠재 고객 레코드가 없는 경우, 해당 레코드가 있는 것으로 대체하십시오. URL 막대에서 enter 키를 누르면 다음과 유사한 JSON 응답을 다시 받아야 합니다.

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

각 API 사용자는 API 사용 보고서에 개별적으로 보고되므로, 사용자별로 웹 서비스를 분할하면 각 통합의 사용을 쉽게 고려할 수 있습니다. 인스턴스에 대한 API 호출 수가 제한을 초과하여 후속 호출이 실패하는 경우 이 방법을 사용하면 각 서비스의 볼륨을 고려하고 문제를 해결하는 방법을 평가할 수 있습니다. **[!UICONTROL Admin]** -> **[!UICONTROL Integration]** > **[!UICONTROL Web Services]**(으)로 이동하여 지난 7일 동안의 통화 수를 클릭하여 사용량을 확인하세요.
