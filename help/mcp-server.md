---
title: MCP 서버
description: MCP 서버를 사용하여 AI 도우미를 Marketo에 연결하는 방법에 대해 알아봅니다. Marketo 자격 증명으로 Cloud Desktop, Cursor, Cloud Code 또는 VS 코드를 구성합니다.
hidefromtoc: true
badgeBeta: label="Beta" type="informative" tooltip="이 기능은 현재 비공개 베타 릴리스에 있습니다"
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
source-git-commit: c21ba0db3115c453f8ec35e18d4a8fd4c1ad8745
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 1%

---

# [!DNL Marketo] MCP 서버

>[!NOTE]
>
>MCP 서버는 현재 비공개 베타 릴리스에 있습니다. 현재 모든 사용자가 사용할 수 있는 것은 아닙니다.

모델 컨텍스트 프로토콜(MCP)은 AI 도구가 외부 서비스와 통신할 수 있도록 하는 개방형 표준이다. [!DNL Marketo] MCP 서버는 AI 길잡이와 [!DNL Marketo] 사이의 다리 역할을 합니다. 양식, 프로그램, 스마트 캠페인, 리드, 이메일, 코드 조각, 목록 및 폴더에 100개 이상의 작업을 노출합니다.

AI 도구가 MCP 서버를 호출하면 서버는 각 요청에서 제공한 자격 증명을 사용하여 사용자를 대신하여 해당 REST API 호출을 실행합니다. 서버측 소프트웨어를 설치, 배포 또는 실행할 필요가 없습니다.

>[!IMPORTANT]
>
>MCP(Model Context Protocol)는 새로운 오픈 소스 표준이며 보안 또는 신뢰성 위험을 제시할 수 있습니다. Adobe MCP 서버 통합 및 관련 설명서는 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공됩니다.
>MCP 클라이언트 또는 서버를 Adobe 제품에 연결하는 것은 고객이 선택한 구성이며 고객은 MCP 통합의 보안 및 적합성을 평가할 책임이 있습니다. Adobe은 잘못된 구성, MCP 오용, 서드파티 구현의 취약점 또는 MCP 지원 워크플로우를 통해 수행된 의도하지 않은 작업으로 인해 발생하는 문제에 대해 책임을 지지 않습니다.
>위험을 줄이기 위해 Adobe에서는 생산적인 사용을 시작하기 전에 샌드박스 환경에서 통합을 테스트하고, 이를 확인하거나 의존하기 전에 모든 MCP에서 시작한 작업과 응답을 주의 깊게 검토하고 확인하는 것을 권장합니다.

## 사전 요구 사항

- REST API 액세스가 활성화된 [!DNL Marketo] 인스턴스
- [!DNL Marketo] LaunchPoint에서 API 자격 증명을 만드는 관리자 액세스
- Cloud Desktop, Cursor, Cloud Code(CLI) 또는 GitHub Copilot을 사용한 VS Code AI 도구 중 하나
- MCP 서버 URL에 대한 네트워크 액세스: `https://marketo-mcp.adobe.io/mcp`

## Marketo 자격 증명 가져오기

[!DNL Marketo] 인스턴스에서 다음 값이 필요합니다.

- **클라이언트 ID**
- **클라이언트 암호**
- **Munchkin 계정 ID**

이미 있는 경우 [AI 도구 구성](#configure-your-ai-tool)으로 건너뜁니다.

### 클라이언트 ID 및 클라이언트 암호

1. **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**(으)로 이동합니다.
1. API 서비스를 클릭합니다. 계정이 없는 경우 **[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;을(를) 선택하고 **[!UICONTROL Custom]**&#x200B;을(를) 서비스 유형으로 선택한 다음 전용 API 사용자를 지정하십시오.
1. **[!UICONTROL View Details]**&#x200B;을(를) 클릭하고 **[!UICONTROL Client ID]** 및 **[!UICONTROL Client Secret]** 값을 복사합니다.

### Munchkin 계정 ID

1. **[!UICONTROL Admin]** > **[!UICONTROL Munchkin]**(으)로 이동합니다.
1. **[!UICONTROL Munchkin Account ID]** 복사 형식은 `XXX-XXX-XXX`이며 인스턴스 URL의 접두사와 일치합니다.

## AI 도구 구성

각 AI 도구는 다른 위치에서 MCP 서버 구성을 읽습니다. 아래에서 도구를 찾아 단계에 따라 [!DNL Marketo] MCP 서버를 추가합니다.

### 클라우드 데스크탑

구성 파일이 `claude_desktop_config.json`입니다. 다음 위치 중 하나에서 엽니다.

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

파일에 이미 다른 MCP 서버가 있는 경우 `mcpServers` 아래에 `marketo` 항목을 추가하십시오. 다음 예제에서는 전체 `mcpServers` 블록을 보여 줍니다.

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
      }
    }
  }
}
```

파일을 저장하고 클라우드 데스크톱을 종료한 다음 다시 엽니다.

### 커서

커서 MCP 구성에 이미 다른 서버가 있는 경우 `mcpServers` 아래에 `marketo` 항목을 추가하십시오. 다음 예제에서는 프로젝트 디렉터리의 **[!UICONTROL Settings]** > **[!UICONTROL MCP]** 또는 `.cursor/mcp.json`에 있는 전체 `mcpServers` 블록을 보여 줍니다.

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
      }
    }
  }
}
```

커서를 재시작합니다.

### 클라우드 코드(CLI)

터미널에서 다음 명령을 실행하여 자격 증명을 대체하십시오.

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
```

### GitHub Copilot이 포함된 VS 코드

macOS에서 **[!UICONTROL Ctrl+Shift+P]** 또는 **[!UICONTROL Cmd+Shift+P]**&#x200B;을(를) 누른 다음 **[!UICONTROL Preferences: Open User Settings (JSON)]**&#x200B;을(를) 선택하여 VS 코드 `settings.json`을(를) 엽니다. 다음 예를 추가합니다.

```json
{
  "mcp": {
    "servers": {
      "marketo": {
        "type": "http",
        "url": "https://marketo-mcp.adobe.io/mcp",
        "headers": {
          "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
          "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
          "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
        }
      }
    }
  }
}
```

**[!UICONTROL Ctrl+Shift+P]**(또는 macOS의 **[!UICONTROL Cmd+Shift+P]**)을 누르고 **[!UICONTROL Reload Window]**&#x200B;을(를) 입력한 다음 Enter 키를 누릅니다.

>[!NOTE]
>
>보안을 위해 자격 증명을 직접 붙여넣는 대신 구성 파일에 환경 변수 보간을 사용합니다. `${MARKETO_CLIENT_SECRET}`과(와) 같은 구문을 사용하여 변수를 참조하고 환경에서 설정할 수 있습니다. 따라서 버전 제어에 커밋될 수 있는 파일의 일반 텍스트에 자격 증명이 저장되지 않습니다.

## 사용 가능한 작업

연결되면 AI 도우미에 다음 카테고리의 작업을 수행하도록 요청할 수 있습니다.

### 양식

양식을 검색, 생성, 복제 및 승인합니다. 필드를 추가 또는 제거하고, 필드 가시성 규칙을 구성하고, 양식이 포함된 위치를 식별합니다.

프롬프트 예:

- &quot;승인된 모든 양식 표시&quot;
- &quot;연락처 양식을 Q2 Campaign 폴더로 복제&quot;
- &quot;데모 요청 양식에 회사 필드 추가&quot;

### 스마트 캠페인

스마트 캠페인을 만들고, 스마트 목록 필터를 구성하고, 흐름 단계를 추가하고, 캠페인을 활성화 또는 비활성화합니다.

프롬프트 예:

- &quot;현재 어떤 스마트 캠페인이 활성화되어 있습니까?&quot;
- &quot;작업 폴더에 잠재 고객 점수 업데이트라는 새 스마트 캠페인 만들기&quot;
- &quot;환영 이메일 캠페인에서 흐름 단계 표시&quot;

### 리드 및 목록

이메일 주소로 리드를 찾고, 리드 레코드를 만들거나 업데이트하고, 정적 목록 멤버십을 관리합니다.

프롬프트 예:

- &quot;jane@example.com으로 이메일을 보내 잠재 고객 찾기&quot;
- &quot;Q2 MQL 목록에 리드 ID 12345 추가&quot;
- &quot;여름 이벤트 참석자라는 새 정적 목록 만들기&quot;

### 프로그램

프로그램 생성, 복제 및 태그 지정 유형, 채널 또는 날짜 범위별로 프로그램을 찾아봅니다.

프롬프트 예:

- &quot;Q4 웨비나 프로그램을 2026년 이벤트 폴더에 복제&quot;
- &quot;캠페인 폴더에 여름 세일이라는 새 이메일 프로그램 만들기&quot;
- &quot;웨비나로 태그가 지정된 모든 프로그램 표시&quot;

### 이메일 및 스니펫

이메일을 검색하고, 템플릿에서 이메일을 만들고, 콘텐츠 섹션을 업데이트하고, 재사용 가능한 스니펫을 관리합니다.

프롬프트 예:

- &quot;모든 초안 이메일 표시&quot;
- &quot;시작 이메일의 헤더 섹션 업데이트&quot;
- &quot;Holiday Promo 코드 조각을 사용하는 자산은 무엇입니까?&quot;

### 인스턴스 구조

폴더, 채널, 태그 유형 및 활동 유형을 탐색하여 [!DNL Marketo] 구성을 이해합니다.

프롬프트 예:

- &quot;Marketo의 모든 폴더 나열&quot;
- &quot;사용 가능한 모든 채널 표시&quot;
- &quot;어떤 태그 유형이 구성됩니까?&quot;

### 대량 작업

리드 데이터를 일괄로 내보내고 가져오기 또는 내보내기 작업 상태를 확인합니다.

프롬프트 예:

- &quot;지난 30일 동안 생성된 리드의 벌크 내보내기 만들기&quot;
- &quot;내보내기 작업 xx의 상태 확인&quot;

## 문제 해결

| 오류 | 원인 | 고정 |
| ------- | ------- | ----- |
| &quot;Marketo 자격 증명이 제공되지 않음&quot; | `X-Marketo-Client-Id`, `X-Marketo-Client-Secret` 또는 `X-Marketo-Munchkin-Id` 중 하나 이상이 없습니다. | 4개의 헤더가 모두 구성에 있는지 확인합니다. |
| &quot;인증 오류&quot; | 자격 증명이 잘못되었거나 만료되었습니다. | **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;에서 클라이언트 ID와 클라이언트 암호를 다시 확인하십시오. |
| &quot;403 금지됨&quot; | Munchkin ID가 서버에 없습니다. | [!DNL Marketo] MCP 관리자에게 문의하여 Munchkin ID를 추가하십시오. |
| 연결 시간 초과 또는 거부됨 | 네트워크에서 MCP 서버에 연결할 수 없습니다. | 사용자 환경에서 서버 URL에 연결할 수 있는지 확인합니다. 해당되는 경우 VPN 요구 사항을 확인하십시오. |
| 도구 호출이 빈 결과를 반환합니다. | API 사용자에게 요청된 에셋 유형에 대한 권한이 없습니다. | [!DNL Marketo] 관리자에게 API 사용자 역할 및 권한을 검토하도록 요청하십시오. |

## 자주 묻는 질문

+++내 데이터가 안전합니까?

자격 증명은 각 개별 요청과 함께 HTTP 헤더로 전송됩니다. 서버는 세션 간에 자격 증명을 저장하거나 캐시하지 않으며 각 요청은 완전히 격리됩니다.

+++

+++여러 사람이 동시에 사용할 수 있습니까?

예. 서버가 다중 임차인입니다. 각 사용자는 자체 자격 증명으로 연결되고 요청은 서로 격리됩니다.

+++

+++액세스 토큰이 만료되면 어떻게 됩니까?

클라이언트 ID 및 클라이언트 암호를 사용하여 인증하면 서버에서 토큰 새로 고침을 자동으로 처리합니다. 아무 조치도 취하지 않아도 됩니다.

+++

+++설치하거나 실행해야 합니까?

아니요. MCP 서버는 Adobe에 의해 호스팅됩니다. AI 도구에 연결하려면 AI 도구를 구성해야 합니다.

+++

+++내 API 사용자에게 필요한 [!DNL Marketo] 권한은 무엇입니까?

API 사용자는 관리하려는 에셋 유형에 액세스해야 합니다. 최소한 검색 작업을 위한 읽기 전용 역할과 에셋을 생성하거나 수정하기 위한 읽기-쓰기 역할을 할당하십시오. [!DNL Marketo] 관리자와 함께 적절한 권한을 할당하십시오.

+++

+++요금 제한이 어떻게 되나요?

MCP 서버가 [!DNL Marketo] 인스턴스의 API 속도 제한을 상속합니다. 전용 API 사용자를 사용하여 할당량 소비를 추적하고 관리합니다.

+++

+++어떤 AI 도구가 지원됩니까?

GitHub Copilot을 사용한 클라우드 데스크탑, 커서, 클라우드 코드(CLI) 및 VS 코드. HTTP를 통해 모델 컨텍스트 프로토콜을 지원하는 모든 AI 도구가 작동해야 합니다.

+++

+++여러 [!DNL Marketo]개의 인스턴스에 연결할 수 있습니까?

예. AI 도구의 MCP 구성에 고유한 이름과 해당 인스턴스에 대한 자격 증명이 있는 여러 항목을 추가합니다. 예를 들어 `marketo-prod`과(와) `marketo-staging`을(를) 별도의 서버로 구성할 수 있습니다.

+++

## 보안 고려 사항

>[!IMPORTANT]
>
>작업에 필요한 권한만 있는 [!DNL Marketo]의 전용 API 사용자를 사용하십시오. API 액세스를 위해 관리자 자격 증명을 재사용하지 마십시오.

- **요청당 자격 증명** 클라이언트 ID, 클라이언트 암호, Munchkin ID 및 REST API 끝점은 각 요청과 함께 HTTP 헤더로 전송됩니다. 서버는 이러한 정보를 저장하거나 캐시하지 않습니다.
- **다중 테넌트 격리** 각 요청은 자체 자격 증명 세트를 사용합니다. 데이터가 다른 사용자의 세션과 교차하지 않습니다.
- **Munchkin ID 허용 목록** 서버는 승인된 [!DNL Marketo]개 인스턴스에 대한 요청만 허용합니다. 승인되지 않은 Munchkin ID를 사용하는 요청은 403 오류로 거부됩니다.
- **자격 증명을 버전 제어에서 벗어나게 합니다.** AI 도구가 지원하는 경우 환경 변수 보간(`${MARKETO_CLIENT_SECRET}`)을 사용하면 자격 증명이 리포지토리에 커밋된 파일의 일반 텍스트에 저장되지 않습니다.
