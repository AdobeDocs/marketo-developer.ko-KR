---
title: Marketo Engage MCP 서버
description: Marketo Engage MCP 서버를 사용하여 AI 도우미를 Marketo에 연결하는 방법에 대해 알아봅니다. Marketo 자격 증명으로 Cloud Desktop, Cursor, Cloud Code 또는 VS 코드를 구성합니다.
badgeBeta: label="제한 공개" type="informative" tooltip="이 기능은 현재 제한된 베타 릴리스에 있습니다"
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
autotag-review: '2026-06-02T13:31:15.329Z'
TQID: 'https://experienceleague.adobe.com/PJJm7yv8HmbwMB2fsnfDCXs8zprDJK5Q5z2uiiCJRZI'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: c2dbad80-0f5c-4d96-a798-2a65f93b8721
  - id: dca84292-69e9-4116-a575-667d31fa060d
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
source-git-commit: af0a3c77654f74d7cb5d2077518d764468a53ae0
workflow-type: tm+mt
source-wordcount: 1985
ht-degree: 1%

---

# [!DNL Marketo Engage] MCP 서버

>[!AVAILABILITY]
>
> 이 기능은 제한적으로 사용할 수 있습니다. 액세스를 요청하려면 [이 양식](https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Y-uSf63sAxCmWyqMJg8eMFUMVZSVExSNDA3T0I4SEcwRDFSVTBGWU01Uy4u&origin=QRCode){target="_blank"}을(를) 입력하십시오. 구독의 Munchkin ID를 준비해야 합니다.

모델 컨텍스트 프로토콜(MCP)은 AI 도구를 외부 서비스에 연결하는 개방형 표준이다. [!DNL Marketo] MCP 서버가 AI 도우미를 [!DNL Marketo]에 연결합니다. 양식, 프로그램, 스마트 캠페인, 리드, 이메일, 코드 조각, 목록 및 폴더에 대해 100개 이상의 작업을 제공합니다.

AI 도구가 MCP 서버를 호출하면 서버는 해당 요청의 자격 증명을 사용하여 해당 REST API 호출을 실행합니다. 서버측 소프트웨어를 설치, 배포 또는 실행할 필요가 없습니다.

Marketo AI 및 Marketo Engage MCP 서버로 데이터를 처리하는 방법에 대한 자세한 내용은 [데이터 정보](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-ai/data-information) 페이지를 참조하십시오.

>[!IMPORTANT]
>
>MCP(Model Context Protocol)는 새로운 오픈 소스 표준이며 보안 또는 신뢰성 위험을 제시할 수 있습니다. Adobe MCP 서버 통합 및 관련 설명서는 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공됩니다.
>MCP 클라이언트 또는 서버를 Adobe 제품에 연결하는 것은 고객이 선택한 구성이며 고객은 MCP 통합의 보안 및 적합성을 평가할 책임이 있습니다. Adobe은 잘못된 구성, MCP 오용, 서드파티 구현의 취약점 또는 MCP 지원 워크플로우를 통해 수행된 의도하지 않은 작업으로 인해 발생하는 문제에 대해 책임을 지지 않습니다.
>위험을 줄이기 위해 Adobe에서는 생산적인 사용을 시작하기 전에 샌드박스 환경에서 통합을 테스트하고, 확인하거나 의존하기 전에 모든 MCP에서 시작한 작업과 응답을 주의 깊게 검토하고 확인하는 것이 좋습니다.

## MCP 기본 사항

>MCP를 AI 애플리케이션용 USB-C 포트와 같이 생각해 보십시오. USB-C는 장치를 다양한 주변 장치와 액세서리에 연결하는 표준화된 방법을 제공하며, MCP는 AI 모델을 데이터 소스 및 도구에 연결하는 표준화된 방법을 제공합니다. — [모델 컨텍스트 프로토콜](https://modelcontextprotocol.io/docs/getting-started/intro){target="_blank"}

MCP는 AI 도구가 여러 외부 서비스에 동시에 연결되도록 한다. 예를 들어 AI 비서는 다음을 수행할 수 있습니다.

* AI 지원 문서 생성을 위해 워드 프로세서에 연결
* 빌드 시각화를 위해 Blender와 같은 애니메이션 도구에 연결합니다
* 비디오 편집을 위해 Adobe After Effects에 연결

모든 애플리케이션은 AI 도구에 데이터와 작업을 노출하기 위해 MCP를 구현할 수 있습니다.

## [!DNL Marketo Engage] MCP가 수행하는 작업과 수행하지 않는 작업

MCP의 범위를 이해하면 AI 도구를 연결하기 전에 기대치를 설정하는 데 도움이 됩니다.

**MCP:**

* 표준 REST API를 통해 [!DNL Marketo] 데이터 및 기능에 대한 액세스 제공
* 각 요청과 함께 제공한 자격 증명을 사용하여 사용자를 대신하여 API 호출 실행
* 각각 고유한 자격 증명으로 연결된 여러 동시 사용자 지원
* OAuth 토큰 새로 고침을 자동으로 처리합니다. 토큰 만료를 관리할 필요가 없습니다.
* 테넌트가 격리된 환경 내에서 작동하여 데이터가 다른 사용자의 세션과 교차하지 않도록 합니다

**MCP:**

* AI 또는 머신 러닝 모델을 사용, 호스팅 또는 실행합니다. 모든 AI 처리는 MCP가 아닌 AI 도구에서 발생합니다
* 고객 데이터를 포함한 모든 데이터를 교육하거나 학습합니다.
* 예측, 권장 사항 또는 의사 결정을 생성합니다. 의사 결정은 다운스트림 AI 도구 또는 사용자의 책임입니다
* 자격 증명, 요청 데이터 또는 요청 간 세션 상태 저장 또는 유지
* 서버 측 소프트웨어를 설치, 배포 또는 관리해야 함

MCP는 API 사용에 따라 잠재적으로 민감한 필드를 포함한 데이터를 전송할 수 있지만 B2B 데이터는 고객 비즈니스 데이터를 포함하며 PII 데이터를 포함하지 않습니다.

## 사전 요구 사항

* REST API 액세스가 활성화된 [!DNL Marketo] 인스턴스
* [!DNL Marketo] LaunchPoint에서 API 자격 증명을 만드는 관리자 액세스
* Cloud Desktop, Cursor, Codex, Claude Code(CLI) 또는 GitHub Copilot을 사용한 VS Code AI 도구 중 하나
* MCP 서버 URL에 대한 네트워크 액세스: `https://marketo-mcp.adobe.io/mcp`

## Marketo 자격 증명 가져오기

[!DNL Marketo] 인스턴스에서 다음 값이 필요합니다.

* **클라이언트 ID**
* **클라이언트 암호**
* **Munchkin 계정 ID**

이미 있는 경우 [AI 도구 구성](#configure-your-ai-tool)으로 건너뜁니다.

### 클라이언트 ID 및 클라이언트 암호

1. **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**(으)로 이동합니다.
1. API 서비스를 선택합니다. 계정이 없는 경우 **[!UICONTROL New]** > **[!UICONTROL New Service]**&#x200B;을(를) 선택하고 **[!UICONTROL Custom]**&#x200B;을(를) 서비스 유형으로 선택한 다음 전용 API 사용자를 지정하십시오.
1. **[!UICONTROL View Details]**&#x200B;을(를) 선택하고 **[!UICONTROL Client ID]** 및 **[!UICONTROL Client Secret]** 값을 복사합니다.

### Munchkin 계정 ID

1. **[!UICONTROL Admin]** > **[!UICONTROL Munchkin]**(으)로 이동합니다.
1. **[!UICONTROL Munchkin Account ID]** 복사 형식은 `XXX-XXX-XXX`이며 인스턴스 URL의 접두사와 일치합니다.

## AI 도구 구성

구성은 AI 도구에 따라 다릅니다. 다음 섹션에서는 일반적인 도구에 대한 연결 예를 제공합니다.

* [클라우드 데스크탑](#claude-desktop)
* [커서](#cursor)
* [클라우드 코드 CLI](#claude-code)
* [OpenAI 코드](#codex)
* [GitHub Copilot이 포함된 VSCode](#vscode)
* [군침](#glean)
* [기타 도구](#other-tools)

>[!TIP]
>
>여러 [!DNL Marketo] 인스턴스에 연결하려면 MCP 구성에 고유한 이름을 가진 개별 항목 `marketo-prod` 및 `marketo-staging`을(를) 추가하십시오. 각 항목에는 해당 자격 증명이 있습니다.

### 클라우드 데스크탑 {#claude-desktop}

클라우드 데스크톱에 연결하려면 [marketo-mcp-bridge.zip](assets/marketo-mcp-bridge.zip)을 다운로드하고 압축을 풉니다. 다음 단계에서 참조할 수 있도록 알려진 위치에 `marketo-mcp-bridge.mjs`을(를) 넣습니다.

또한 다음이 필요합니다.

* Node.js v18+
* npm

1. 클라우드 데스크탑을 엽니다.
1. **설정 > 개발자 > 구성 편집**(으)로 이동합니다.
1. `claude_desktop_config.json`에 다음 추가:

```json
{
  "preferences": {
    ...
  },
  "mcpServers": {
    "marketo-mcp": {
      "command": "node",
      "args": ["/path/to/marketo-bridge/bridge.mjs"],
      "env": {
        "MARKETO_MCP_PROD_CLIENT_ID": "<your-client-id>",
        "MARKETO_MCP_PROD_CLIENT_SECRET": "<your-client-secret>",
        "MARKETO_MCP_PROD_MUNCHKIN_ID": "<your-munchkin-id>"
      }
    }
  }
}
```

1. 클라우드 데스크탑을 다시 시작합니다.

### 커서 {#cursor}

커서 MCP 구성에 이미 다른 서버가 있는 경우 `mcpServers` 아래에 `marketo` 항목을 추가하십시오.
다음 예제에서는 프로젝트 디렉터리의 **[!UICONTROL Settings]** > **[!UICONTROL MCP]** 또는 `.cursor/mcp.json`에 있는 전체 `mcpServers` 블록을 보여줍니다.

>[!BEGINTABS]

>[!TAB IMS 토큰]

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-IMS-TOKEN",
        "x-gw-ims-org-id": "YOUR-IMS-ORG-ID"
      }
    }
  }
}
```

>[!TAB Marketo 클라이언트 자격 증명]

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

>[!ENDTABS]

커서를 재시작합니다.

### 클라우드 코드(CLI) {#claude-code}

터미널에서 다음 명령을 실행하여 자격 증명을 대체하십시오.

>[!BEGINTABS]

>[!TAB IMS 토큰]

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "Authorization: Bearer YOUR-IMS-TOKEN" \
  --header "x-gw-ims-org-id: YOUR-IMS-ORG-ID"
```

>[!TAB Marketo 클라이언트 자격 증명]

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
```

>[!ENDTABS]

### OpenAI 코드 {#codex}

1. 설정 > MCP 서버 > 서버 추가 로 이동합니다.
1. 서버 URL `https://marketo-mcp.adobe.io/mcp`을(를) 추가합니다.
1. 인증 방법에 대한 헤더를 추가합니다.

>[!BEGINTABS]

>[!TAB IMS 토큰]

* 인증: &quot;Bearer YOUR-IMS-TOKEN&quot;
* x-gw-ims-org-id: &quot;YOUR-IMS-ORG-ID&quot;

>[!TAB Marketo 클라이언트 자격 증명]

* X-Marketo-Client-Id: &quot;YOUR-CLIENT-ID&quot;
* X-Marketo-Client-Secret: &quot;YOUR-CLIENT-SECRET&quot;
* X-Marketo-Munchkin-Id: &quot;YOUR-MUNCHKIN-ID&quot;

>[!ENDTABS]

1. 저장 을 선택하여 프로세스를 완료합니다.


### GitHub Copilot이 포함된 VS 코드 {#vscode}

**[!UICONTROL Ctrl+Shift+P]**(또는 macOS의 **[!UICONTROL Cmd+Shift+P]**)을 누르고 **[!UICONTROL MCP: Open User Configuration]**&#x200B;을(를) 입력한 다음 Enter 키를 누릅니다. `mcp.json`을(를) 엽니다. `servers` 개체 내에 `marketo` 항목 추가:

>[!BEGINTABS]

>[!TAB IMS 토큰]

```json
{
  "servers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-IMS-TOKEN",
        "x-gw-ims-org-id": "YOUR-IMS-ORG-ID"
      }
    }
  }
}
```

>[!TAB Marketo 클라이언트 자격 증명]

```json
{
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
```

>[!ENDTABS]

>[!NOTE]
>
>보안을 위해 자격 증명을 직접 붙여넣는 대신 구성 파일에 환경 변수 보간을 사용합니다. `${MARKETO_CLIENT_SECRET}`과(와) 같은 구문을 사용하여 변수를 참조하고 환경에서 설정할 수 있습니다. 이렇게 하면 버전 제어 파일의 일반 텍스트에 자격 증명이 저장되지 않습니다.

### 군침 {#glean}

Glean을 Marketo Engage MCP 서버에 연결하려면 [Glean 지원 팀](https://docs.glean.com/release-notes/releases/2026-04-22-april-release#admin-features)이 다음 사용자 지정 헤더를 구성해야 합니다.

| Header | 값 |
| ------ | ----- |
| `X-Marketo-Client-Id` | 클라이언트 ID |
| `X-Marketo-Client-Secret` | 클라이언트 암호 |
| `X-Marketo-Munchkin-Id` | Munchkin 계정 ID |

### 기타 도구 {#other-tools}

Adobe은 [!DNL Marketo] MCP 서버를 호스팅하고 공개 URL에 노출합니다. 스트리밍 가능한 HTTP 전송을 통해 원격 서버를 지원하는 모든 MCP 클라이언트가 연결할 수 있습니다.
도구별 브리지나 로컬에 설치된 소프트웨어는 필요하지 않습니다. 도구가 위에 나열되지 않으면 아래 연결 세부 정보를 사용하여 수동으로 구성하십시오.

**연결 세부 정보:**

| 설정 | 값 |
| ------- | ----- |
| 전송 | HTTP(스트리밍 가능 HTTP) |
| 서버 URL | `https://marketo-mcp.adobe.io/mcp` |

**인증 헤더:**

각 요청에 대해 다음 인증 방법 중 하나에 대한 헤더를 보냅니다. 서버 URL 및 헤더를 입력하는 위치는 도구에 따라 다르므로 MCP 설명서를 참조하십시오.

>[!BEGINTABS]

>[!TAB IMS 토큰]

| Header | 값 |
| ------ | ----- |
| `Authorization` | `Bearer YOUR-IMS-TOKEN` |
| `x-gw-ims-org-id` | IMS 조직 ID |

>[!TAB Marketo 클라이언트 자격 증명]

| Header | 값 |
| ------ | ----- |
| `X-Marketo-Client-Id` | 클라이언트 ID |
| `X-Marketo-Client-Secret` | 클라이언트 암호 |
| `X-Marketo-Munchkin-Id` | Munchkin 계정 ID |

>[!ENDTABS]

도구가 JSON 구성을 허용하는 경우 [Cursor](#cursor) 또는 [VS 코드](#vscode) 예제로 시작하고 도구의 스키마와 일치하도록 키(`mcpServers`, `servers`)를 조정합니다.

## 사용 가능한 작업

연결되면 AI 도우미에 다음 카테고리의 작업을 수행하도록 요청할 수 있습니다. API 참조를 사용한 지원되는 작업의 전체 목록은 [지원되는 MCP 작업](mcp-server-operations.md)을 참조하십시오.

### 양식

양식을 검색, 생성, 복제 및 승인합니다. 필드를 추가 또는 제거하고, 필드 가시성 규칙을 구성하고, 양식이 포함된 위치를 식별합니다.

프롬프트 예:

* &quot;승인된 모든 양식 표시&quot;
* &quot;연락처 양식을 Q2 Campaign 폴더로 복제&quot;
* &quot;데모 요청 양식에 회사 필드 추가&quot;

### 스마트 캠페인

스마트 캠페인을 만들고, 스마트 목록 필터를 구성하고, 흐름 단계를 추가하고, 캠페인을 활성화 또는 비활성화합니다.

프롬프트 예:

* &quot;현재 어떤 스마트 캠페인이 활성화되어 있습니까?&quot;
* &quot;작업 폴더에 잠재 고객 점수 업데이트라는 새 스마트 캠페인 만들기&quot;
* &quot;환영 이메일 캠페인에서 흐름 단계 표시&quot;

### 리드 및 목록

이메일 주소로 리드를 찾고, 리드 레코드를 만들거나 업데이트하고, 정적 목록 멤버십을 관리합니다.

프롬프트 예:

* &quot;jane@example.com으로 이메일을 보내 잠재 고객 찾기&quot;
* &quot;Q2 MQL 목록에 리드 ID 12345 추가&quot;
* &quot;여름 이벤트 참석자라는 새 정적 목록 만들기&quot;

### 프로그램

프로그램 생성, 복제 및 태그 지정 유형, 채널 또는 날짜 범위별로 프로그램을 찾아봅니다.

프롬프트 예:

* &quot;Q4 웨비나 프로그램을 2026년 이벤트 폴더에 복제&quot;
* &quot;캠페인 폴더에 여름 세일이라는 새 이메일 프로그램 만들기&quot;
* &quot;웨비나로 태그가 지정된 모든 프로그램 표시&quot;

### 이메일 및 스니펫

이메일을 검색하고, 템플릿에서 이메일을 만들고, 콘텐츠 섹션을 업데이트하고, 재사용 가능한 스니펫을 관리합니다.

프롬프트 예:

* &quot;모든 초안 이메일 표시&quot;
* &quot;시작 이메일의 헤더 섹션 업데이트&quot;
* &quot;Holiday Promo 코드 조각을 사용하는 자산은 무엇입니까?&quot;

### 인스턴스 구조

[!DNL Marketo] 구성을 이해하려면 폴더, 채널, 태그 유형 및 활동 유형을 찾아보십시오.

프롬프트 예:

* &quot;Marketo의 모든 폴더 나열&quot;
* &quot;사용 가능한 모든 채널 표시&quot;
* &quot;어떤 태그 유형이 구성됩니까?&quot;

### 대량 작업

리드 데이터를 일괄로 내보내고 가져오기 또는 내보내기 작업 상태를 확인합니다.

프롬프트 예:

* &quot;지난 30일 동안 생성된 리드의 벌크 내보내기 만들기&quot;
* &quot;내보내기 작업 xx의 상태 확인&quot;

## 문제 해결

| 오류 | 원인 | 고정 |
| ------- | ------- | ----- |
| &quot;Marketo 자격 증명이 제공되지 않음&quot; | `X-Marketo-Client-Id`, `X-Marketo-Client-Secret` 또는 `X-Marketo-Munchkin-Id` 중 하나 이상이 없습니다. | 모든 Marketo 클라이언트 자격 증명 헤더가 구성에 있는지 확인합니다. |
| &quot;401 인증되지 않음&quot; | 자격 증명이 없거나, 잘못되었거나, 만료되었습니다. Marketo 클라이언트 자격 증명을 사용할 때 클라이언트 ID 또는 클라이언트 암호가 올바르지 않습니다. IMS 토큰을 사용하면 토큰이 잘못되거나 만료됩니다. | 인증 방법에 대한 자격 증명을 확인합니다. 클라이언트 자격 증명의 경우 **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;에서 **[!UICONTROL Client ID]** 및 **[!UICONTROL Client Secret]**&#x200B;을(를) 다시 확인하십시오. IMS 토큰의 경우 새 토큰을 생성하고 `Authorization` 헤더를 업데이트하십시오. |
| &quot;403 금지됨&quot; | 자격 증명은 유효하지만 [!DNL Marketo] 인스턴스가 MCP 액세스용으로 활성화되지 않았습니다. | [!DNL Marketo] MCP 관리자에게 문의하여 Munchkin 계정 ID에 대한 MCP 액세스를 활성화하십시오. |
| &quot;요청이 너무 많음&quot;(비율 제한) | 단기간에 너무 많은 요청을 보내거나 동시에 너무 많은 요청을 보내 [!DNL Marketo] 인스턴스의 API 제한에 도달했습니다. | 한 번에 보낼 요청의 빈도와 수를 줄이고 잠시 기다린 후 다시 시도하십시오. 전용 API 사용자를 사용하여 할당량을 추적하고 관리합니다. |
| 연결 시간 초과 또는 거부됨 | 네트워크에서 MCP 서버에 연결할 수 없습니다. | 사용자 환경에서 서버 URL에 연결할 수 있는지 확인합니다. 해당되는 경우 VPN 요구 사항을 확인하십시오. |
| 도구 호출이 빈 결과를 반환합니다. | API 사용자에게 요청된 에셋 유형에 대한 권한이 없습니다. | [!DNL Marketo] 관리자에게 API 사용자 역할 및 권한을 검토하도록 요청하십시오. |

## 보안 고려 사항

>[!IMPORTANT]
>
>작업에 필요한 권한만 있는 [!DNL Marketo]의 전용 API 사용자를 사용하십시오. API 액세스를 위해 관리자 자격 증명을 재사용하지 마십시오.

* **요청당 자격 증명** 클라이언트 ID, 클라이언트 암호, Munchkin ID 및 REST API 끝점은 각 요청과 함께 HTTP 헤더로 전송됩니다. 서버는 이러한 정보를 저장하거나 캐시하지 않습니다.
* **다중 테넌트 격리** 각 요청은 자체 자격 증명 세트를 사용합니다. 데이터가 다른 사용자의 세션과 교차하지 않습니다.
* **Munchkin ID 허용 목록** 서버는 승인된 [!DNL Marketo]개 인스턴스에 대한 요청만 허용합니다. 승인되지 않은 Munchkin ID를 사용하는 요청은 403 오류로 거부됩니다.
* **API 속도 제한.** MCP 서버가 [!DNL Marketo] 인스턴스의 API 속도 제한을 상속합니다. 전용 API 사용자를 사용하여 할당량 소비를 추적하고 관리합니다.
* **자격 증명을 버전 제어에서 벗어나게 합니다.** AI 도구에서 지원하는 경우 환경 변수 보간(`${MARKETO_CLIENT_SECRET}`)을 사용하므로 자격 증명이 저장소 파일의 일반 텍스트에 저장되지 않습니다.

## 거버넌스 및 데이터 보존

### 자격 증명 처리

* 고객 자격 증명은 서버측에서 지속되지 않으며 요청에 따라 클라이언트가 제공하므로 서비스 내에서 자격 증명 노출을 제한하는 데 도움이 됩니다.

### API 상호 작용 모델

* 에이전트 사용: 에이전트는 MCP 서버를 사용하여 지원되는 Marketo API를 호출할 수 있습니다.
* 인증 모델 정렬: 이 서비스는 Marketo API에 대해 문서화된 것과 동일한 외부 API 인증 모델을 사용합니다.

### 인증 및 권한 부여

* 최소 권한: 유효 권한은 고객의 LaunchPoint 서비스에 할당된 Marketo API 전용 사용자로부터 상속되어 고객의 Marketo 구성 내에서 최소 권한 관리를 가능하게 합니다.
* 서버측 토큰 지속성 없음: 이 서비스는 고객 자격 증명 또는 토큰의 서버측 저장을 계속 방지합니다.  

### 로깅 및 모니터링

* 보안 로깅: 구조화된 JSON 로그는 Fluent Bit를 통해 Splunk로 라우팅되며, 민감한 데이터 마스킹과 추가적인 필터링을 통해 규정 준수 요구 사항을 지원합니다.
* 감사 지원: 서비스 가용성, 보안 관련 이벤트 및 운영 품질에 대한 지속적인 모니터링을 지원합니다.
* 서버측 암호 저장 없음: 고객 자격 증명은 MCP 배포에 의해 저장되지 않으며 요청에 따라 클라이언트가 제공해야 합니다.
* 토큰 처리: 액세스 토큰은 수명이 짧고, 토큰 응답은 no-store로 표시되며, 토큰은 쿼리 문자열 전송이 아닌 표준 인증 메커니즘을 통해 수락됩니다.
* 역할 기반 운영 액세스: 관리 배포 액세스는 Adobe 인프라 역할 및 그룹 기반 제어를 통해 제어되지만 데이터 평면 권한은 고객의 Marketo API 사용자 구성에서 상속됩니다.
* 감사 및 가시성: 보안 로깅, 마스킹, 모니터링 및 경고 기능을 사용하여 조사, 서비스 상태 추적 및 운영 감독을 지원할 수 있습니다.
