---
title: Marketo Engage MCP 작업
description: AI 도우미와 함께 사용할 수 있는 Marketo Engage MCP 작업을 알아봅니다.
autotag-review: '2026-06-02T13:31:42.084Z'
TQID: 'https://experienceleague.adobe.com/qvrWbHOCsCCHctduNDxMhkE8JAKxZk8FCYfKvzxfcYA'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
source-git-commit: 1cdb28422994b772a0fa430e213facaf26817952
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%
---

# [!DNL Marketo Engage] MCP 작업

[!DNL Marketo Engage] MCP 서버는 자산 관리, 리드 데이터 및 캠페인 자동화에 대해 182개의 작업을 지원합니다.



## 지원되는 작업

연결된 AI 비서를 통해 사용 가능한 작업을 검색할 수 있습니다.

연결에 검색 도구가 표시되면 다음 프롬프트를 사용하십시오.

* &quot;Marketo MCP `list_tool_categories` 도구를 사용하여 사용 가능한 작업 범주를 나열하십시오.&quot;
* &quot;Marketo MCP `search_tools` 도구를 사용하여 스마트 캠페인을 관리하기 위한 작업을 찾으십시오.&quot;

두 번째 프롬프트의 작업을 필요한 작업으로 바꿉니다. 검색 도구가 노출되지 않은 경우 AI 도우미에 [!DNL Marketo] MCP 서버에서 사용할 수 있는 도구 목록을 요청하십시오.

연결의 사용 권한 및 기능 가용성을 반영한 결과입니다. 전체 [!DNL Marketo] REST API가 아니라 사용 가능한 MCP 도구에 대해 설명합니다.

[!DNL Marketo] 클라이언트 자격 증명을 사용하는 연결의 경우 다음 기능이 지원되지 않습니다.

* SMS 도구
* 푸시 알림 도구
* 인앱 메시지 및 인앱 프로그램 도구
* `schedule_smart_campaign`(으)로 스마트 캠페인 예약
* 사용자 관리 및 벌크 서비스 도구

`schedule_campaign` 작업은 클라이언트 자격 증명 연결에 대해 지원됩니다.

사용 가능한 작업은 API 사용자 권한, [!DNL Marketo] 인스턴스에 대해 설정된 기능 및 MCP 클라이언트의 제한 사항에 따라 다릅니다. 데이터를 변경하거나 삭제하는 일부 작업은 확인 및 추가 액세스가 필요합니다. 범주를 지원한다고 해서 모든 REST 끝점에 대한 액세스를 의미하지는 않습니다.

연결 지침 및 예제 프롬프트는 [MCP 서버](mcp-server.md#available-operations) 페이지를 참조하십시오. [!DNL Marketo] AI 및 [!DNL Marketo Engage] MCP 서버로 데이터를 처리하는 방법에 대한 자세한 내용은 [데이터 정보](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/marketo-ai/data-information) 페이지를 참조하십시오.