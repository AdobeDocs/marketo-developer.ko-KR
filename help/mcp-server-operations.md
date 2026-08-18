---
title: Marketo Engage MCP 작업
description: AI 도우미와 함께 사용할 수 있는 Marketo Engage MCP 작업을 알아봅니다.
autotag-review: '2026-06-02T13:31:42.084Z'
TQID: 'https://experienceleague.adobe.com/qvrWbHOCsCCHctduNDxMhkE8JAKxZk8FCYfKvzxfcYA'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: dca84292-69e9-4116-a575-667d31fa060d
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
source-git-commit: c631b7c3d571f29083673f9b97d22230d109abfc
workflow-type: tm+mt
source-wordcount: 1228
ht-degree: 25%

---


# [!DNL Marketo Engage] MCP 작업

[!DNL Marketo Engage] MCP 서버를 통해 다음 작업을 사용할 수 있습니다. 서버는 읽기 전용 또는 비파괴인 끝점을 제공합니다. AI 시스템은 `Delete` 또는 다른 파괴적 작업을 사용할 수 없습니다.

>[!NOTE]
>
>스마트 목록 및 스마트 캠페인 `create` 및 `update` 도구는 2026년 9월 릴리스가 타깃팅되었습니다.

Marketo AI 및 Marketo Engage MCP 서버로 데이터를 처리하는 방법에 대한 자세한 내용은 [데이터 정보](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/marketo-ai/data-information) 페이지를 참조하십시오.

## 일괄 내보내기

[대량 내보내기 API 참조](https://developer.adobe.com/marketo-apis/api/mapi){target="_blank"}

- `bulk_export_create`
- `bulk_export_enqueue`
- `bulk_export_file`
- `bulk_export_status`
- `get_import_status`

## 채널 및 태그

[채널 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels){target="_blank"} | [태그 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags){target="_blank"}

- `browse_channels`
- `browse_tag_types`
- `get_channel_by_name`
- `get_tag_type_by_name`

## 이메일

[이메일 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails){target="_blank"}

- `approve_email`
- `browse_emails`
- `create_email`
- `get_email_by_id`
- `get_email_by_name`
- `get_email_content`
- `update_email_content`

## 폴더

[폴더 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders){target="_blank"}

- `browse_folders`
- `create_folder`
- `delete_folder`
- `get_folder_by_id`
- `get_folder_by_name`
- `get_folder_content`
- `update_folder`

## 양식

[Forms API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms){target="_blank"}

- `add_field_set`
- `add_field_to_form`
- `add_field_visibility_rule`
- `add_rich_text_field`
- `approve_form`
- `browse_forms`
- `clone_form`
- `create_form`
- `delete_field_from_fieldset`
- `delete_form`
- `delete_form_field`
- `discard_form_draft`
- `get_form_by_id`
- `get_form_by_name`
- `get_form_field_metadata`
- `get_form_fields`
- `get_forms_used_by`
- `get_program_member_fields`
- `get_thank_you_page`
- `set_field_autofill`
- `update_field_positions`
- `update_form`
- `update_form_field`

## 잠재 고객

[잠재 고객 API 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads){target="_blank"}

- `add_leads_to_list`
- `describe_lead`
- `get_activity_types`
- `get_lead_activities`
- `get_leads_by_filter`
- `get_leads_by_smart_list`
- `get_paging_token`

## 프로그램

[프로그램 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs){target="_blank"}

- `approve_program`
- `browse_email_batch_programs`
- `browse_nurture_programs`
- `browse_program_details`
- `browse_program_events`
- `browse_programs`
- `browse_scheduled_programs`
- `clone_program`
- `create_program`
- `delete_program_tag`
- `get_program_by_id`
- `get_program_by_name`
- `get_program_creation_options`
- `get_program_smart_list`
- `get_programs_by_tag`
- `unapprove_program`
- `update_program`
- `update_program_tag`

## 스마트 캠페인

[스마트 캠페인 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Campaigns){target="_blank"}

- `activate_smart_campaign`
- `add_flow_step`
- `browse_smart_campaigns`
- `create_smart_campaign`
- `facet_smart_campaigns`
- `get_smart_campaign_auto_suggest`
- `get_smart_campaign_by_id`
- `get_smart_campaign_by_name`
- `get_smart_campaign_flow_step_by_name`
- `get_smart_campaign_flow_step_type_by_name`
- `get_smart_campaign_flow_step_types`
- `get_smart_campaign_flow_steps`
- `get_smart_campaign_rule_by_name`
- `get_smart_campaign_rules`
- `get_smart_campaign_scheduled_runs`
- `get_smart_campaign_used_by`
- `get_smart_list_by_campaign_id`
- `schedule_campaign`
- `trigger_campaign`
- `update_flow_step_choice`
- `update_smart_campaign`

## 스마트 목록

[스마트 목록 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Smart-Lists){target="_blank"}

- `add_smart_list_rule`
- `browse_smart_lists`
- `clone_smart_list`
- `create_smart_list`
- `delete_all_smart_list_rules`
- `get_smart_list_auto_suggest`
- `get_smart_list_by_id`
- `get_smart_list_by_name`
- `get_smart_list_rule_by_name`
- `get_smart_list_rules`
- `get_smart_list_used_by`
- `remove_smart_list_rule_constraint`
- `reorder_smart_list_rules`
- `update_smart_list_filter_logic`
- `update_smart_list_rule`

## 스니펫

[코드 조각 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Snippets){target="_blank"}

- `approve_snippet`
- `browse_snippets`
- `clone_snippet`
- `create_snippet`
- `delete_snippet`
- `discard_snippet_draft`
- `facet_snippets`
- `get_snippet_by_id`
- `get_snippet_content`
- `get_snippet_dynamic_content`
- `unapprove_snippet`
- `update_snippet`
- `update_snippet_content`
- `update_snippet_dynamic_content`

## 정적 목록

[정적 목록 API 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Static-Lists){target="_blank"}

- `browse_lists`
- `create_list`
- `get_list_by_id`
- `get_list_by_name`
- `get_list_members`
- `remove_from_list`
- `update_list`

## 토큰

[토큰 API 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens){target="_blank"}

- `create_calendar_token`
- `create_token`
- `delete_token`
- `get_calendar_tokens`
- `get_tokens_by_folder`

## MCP 흐름 단계 도구 활성화됨

<table style="table-layout:auto">
<tr>
<th>흐름 단계</th>
<th>트리거</th>
<th>필터(활동)</th>
<th>필터(속성)</th>
</tr>
<tr>
<td valign="top"><ul><li>필드 집합에 추가</li><li>목록에 추가</li><li>Microsoft 캠페인에 추가</li><li>양육에 추가</li><li>SFDC 캠페인에 추가</li><li>웹후크 호출</li><li>데이터 값 변경</li><li>잠재 고객 파티션 변경</li><li>육성 케이던스 변경</li><li>육성 추적 변경</li><li>소유자 변경</li><li>Microsoft에서 소유자 변경</li><li>프로그램 데이터 변경</li><li>프로그램 멤버 데이터 변경</li><li>수익 단계 변경</li><li>점수 변경</li><li>세그먼트 변경</li><li>진행 상태 변경</li><li>SFDC 캠페인 상태 변경</li><li>잠재 고객 전환</li><li>작업 만들기</li><li>Microsoft에서 작업 만들기</li><li>리드 삭제</li><li>Microsoft에서 리드 삭제</li><li>SFDC에서 리드 삭제</li><li>캠페인 실행</li><li>즐거운 순간</li><li>필드 집합에서 제거</li><li>플로우에서 제거</li><li>목록에서 제거</li><li>Microsoft 캠페인에서 제거</li><li>SFDC 캠페인에서 제거</li><li>캠페인 요청</li><li>경고 보내기</li><li>이메일 보내기</li><li>Microsoft에 리드 동기화</li><li>SFDC에 리드 동기화</li><li>대기</li></ul></td>
<td valign="top"><ul><li>활동이 기록됨</li><li>활동이 업데이트됨</li><li>목록에 추가됨</li><li>Microsoft 캠페인에 추가됨</li><li>양육에 추가됨</li><li>영업 기회에 추가됨</li><li>영업 기회(계정)에 추가됨</li><li>Opportunity(Contact)에 추가됨</li><li>SFDC 캠페인에 추가됨</li><li>이벤트 중 질문하기</li><li>이벤트 참석</li><li>캠페인이 요청됨</li><li>링크 클릭</li><li>이메일의 링크 클릭 수</li><li>영업 이메일의 링크 클릭</li><li>SMS 메시지의 링크 클릭</li><li>링크 클릭</li><li>데이터 값 변경</li><li>에셋 다운로드</li><li>이메일 바운스</li><li>전자 메일 바운스 소프트</li><li>이메일 전달됨</li><li>대화 흐름 참여</li><li>대화 상자 참여</li><li>대화 흐름에서 에이전트와 연결</li><li>대화 상자에서 에이전트 작업</li><li>양식을 작성함</li><li>“즐거운 순간”이 있음</li><li>대화형 흐름에서 문서와 상호 작용</li><li>대화 상자에서 문서와 상호 작용함</li><li>판매 이메일 전송됨</li><li>잠재 고객 전환</li><li>잠재 고객 생성됨</li><li>리드가 Microsoft에서 삭제되었습니다.</li><li>리드가 SFDC에서 삭제되었습니다.</li><li>리드가 Marketo으로 푸시됨</li><li>리드가 Microsoft에 동기화됨</li><li>리드가 SFDC에 동기화됨</li><li>잠재 고객 파티션 변경</li><li>수동 단계 변경</li><li>케이던스 변경 육성</li><li>변경 내용 추적</li><li>이메일 열기</li><li>영업 이메일 열기</li><li>영업 기회(계정)가 업데이트됨</li><li>영업 기회(연락처)가 업데이트되었습니다.</li><li>영업 기회가 업데이트되었습니다.</li><li>소유자 변경 사항</li><li>Microsoft의 소유자 변경</li><li>프로그램 구성원 데이터가 변경됨</li><li>진행 상태가 변경됨</li><li>대화 상자 목표에 도달</li><li>대화 흐름의 목표 도달</li><li>친구에게 이메일 발송</li><li>목록에서 제거됨</li><li>Microsoft 캠페인에서 제거됨</li><li>영업 기회에서 제거됨</li><li>영업 기회(계정)에서 제거됨</li><li>영업 기회 (연락처)에서 제거됨</li><li>SFDC 캠페인에서 제거됨</li><li>판매 이메일에 대한 회신</li><li>설문 조사에 응답</li><li>설문 조사에 응답</li><li>수익 단계 변경됨</li><li>영업 이메일 반송</li><li>영업 이메일 수신</li><li>대화 흐름의 회의 일정</li><li>대화 상자에서 회의 예약</li><li>점수가 변경됨</li><li>세그먼트 변경 사항</li><li>경고 보냄</li><li>친구에게 이메일 발송</li><li>SMS 메시지 반송</li><li>SMS 메시지 전달됨</li><li>SFDC Campaign에서 상태가 변경됨</li><li>이메일에서 구독 취소</li><li>웹 페이지를 방문함</li><li>Webhook이 호출됨</li></ul></td>
<td valign="top"><ul><li>활동이 기록됨</li><li>활동이 업데이트됨</li><li>경고가 전송됨</li><li>캠페인이 실행됨</li><li>캠페인이 요청됨</li><li>링크 클릭</li><li>이메일의 클릭한 링크</li><li>영업 이메일에서 링크를 클릭함</li><li>SMS 메시지에서 클릭한 링크</li><li>링크를 클릭함</li><li>데이터 값 변경됨</li><li>자산 다운로드됨</li><li>반송된 이메일</li><li>가볍게 반송된 이메일</li><li>대화 플로우에 참여함</li><li>대화에 참여함</li><li>대화형 흐름에서 에이전트와 참여</li><li>대화에서 상담원과 상호 작용함</li><li>작성된 양식</li><li>“즐거운 순간”이 있었음</li><li>이벤트 중에 질문함</li><li>이벤트에 참여함</li><li>대화형 흐름에서 문서와 상호 작용</li><li>대화에서 문서와 상호 작용함</li><li>잠재 고객 파티션 변경됨</li><li>잠재 고객 전환됨</li><li>잠재 고객 생성됨</li><li>리드가 Microsoft에서 삭제되었습니다.</li><li>리드가 SFDC에서 삭제되었습니다.</li><li>잠재 고객이 Marketo으로 푸시됨</li><li>리드가 Microsoft에 동기화됨</li><li>리드가 SFDC에 동기화됨</li><li>케이던스 육성 변경됨</li><li>육성 트랙 변경됨</li><li>이메일 열림</li><li>영업 이메일 열림</li><li>영업 기회(계정)가 업데이트되었습니다.</li><li>영업 기회(연락처)가 업데이트되었습니다.</li><li>영업 기회가 업데이트되었습니다.</li><li>소유자가 변경되었습니다.</li><li>Microsoft에서 소유자가 변경되었습니다.</li><li>프로그램 구성원 데이터가 변경됨</li><li>진행 상태가 변경됨</li><li>대화 목표를 달성함</li><li>대화 흐름의 목표 도달</li><li>친구에게 이메일 발송</li><li>판매 이메일에 회신함</li><li>투표에 응답함</li><li>설문 조사에 응답함</li><li>수익 단계 변경됨</li><li>반송된 판매 이메일</li><li>영업 이메일 수신됨</li><li>대화 흐름의 예약된 회의</li><li>대화에서 회의를 예약함</li><li>점수가 변경되었습니다.</li><li>세그먼트 변경됨</li><li>친구에게 이메일 발송</li><li>SMS 메시지 반송됨</li><li>이메일 구독 취소됨</li><li>방문한 웹 페이지</li><li>이(가) 목록에 추가되었습니다.</li><li>양육에 추가됨</li><li>이(가) Opportunity에 추가되었습니다.</li><li>Opportunity(계정)에 추가되었습니다.</li><li>이(가) Opportunity(연락처)에 추가되었습니다.</li><li>게재됨 이메일</li><li>SMS 메시지가 전달됨</li><li>목록에서 제거됨</li><li>이(가) 영업 기회에서 제거되었습니다.</li><li>영업 기회(계정)에서 제거됨</li><li>이(가) 영업 기회(연락처)에서 제거되었습니다.</li><li>이(가) 이메일을 보냈습니다</li><li>이(가) 판매 이메일을 보냈습니다.</li><li>Webhook이 호출됨</li></ul></td>
<td valign="top"><ul><li>계정 소유자 이메일 주소</li><li>계정 소유자의 이름</li><li>계정 소유자 성</li><li>획득 날짜</li><li>확보 프로그램</li><li>고객 확보 프로그램 이름</li><li>주소</li><li>연매출</li><li>익명 IP</li><li>청구지 주소</li><li>청구지 시</li><li>청구지 국가</li><li>청구지 우편번호</li><li>청구지 주</li><li>차단 목록</li><li>도시</li><li>회사 Microsoft 유형</li><li>회사 이름</li><li>국가</li><li>생성 위치</li><li>출생일</li><li>부서</li><li>두 낫 콜</li><li>두 낫 콜 이유</li><li>중복 필드</li><li>이메일 주소</li><li>잘못된 이메일</li><li>잘못된 이메일 원인</li><li>이메일 중단됨</li><li>다음 시간에 이메일 일시 중단됨</li><li>이메일 일시 중단 원인</li><li>팩스 번호</li><li>이름</li><li>전체 이름</li><li>영업 기회 있음</li><li>업종</li><li>추론된 시</li><li>추론된 회사</li><li>추론된 국가</li><li>대도시 지역 유추</li><li>전화번호 지역코드 유추</li><li>추론된 우편번호</li><li>유추된 주 지역</li><li>고객</li><li>파트너</li><li>직위</li><li>성</li><li>잠재 고객 소유자 이메일 주소</li><li>잠재 고객 소유자의 이름</li><li>잠재 고객 소유자 직책</li><li>잠재 고객 소유자 성</li><li>잠재 고객 소유자 전화 번호</li><li>잠재 고객 파티션 이름</li><li>리드 등급</li><li>리드 점수</li><li>리드 소스</li><li>리드 상태</li><li>주요 전화</li><li>마케팅 중단</li><li>필드 집합의 구성원</li><li>목록 멤버</li><li>육성 멤버</li><li>프로그램 멤버</li><li>수익 모델 멤버</li><li>수익 단계 구성원</li><li>SFDC 캠페인 멤버</li><li>스마트 캠페인 멤버</li><li>스마트 목록 멤버</li><li>Microsoft 계정 번호</li><li>Microsoft 생성 날짜</li><li>Microsoft 삭제됨</li><li>Microsoft 유형</li><li>중간 이름</li><li>휴대 전화 번호</li><li>참고</li><li>직원 수</li><li>영업 기회 수</li><li>원래 레퍼러</li><li>원본 검색 엔진</li><li>원본 검색 구문</li><li>원본 소스 정보</li><li>원본 소스 유형</li><li>모회사 이름</li><li>사용자 시간대</li><li>전화 번호</li><li>우편번호</li><li>임의 샘플</li><li>등록 Source 정보</li><li>등록 Source 유형</li><li>역할</li><li>인사말</li><li>SFDC 계정 번호</li><li>SFDC 생성일</li><li>SFDC 삭제됨</li><li>SFDC 유형</li><li>SIC 코드</li><li>사이트</li><li>주/도</li><li>총 영업 기회 금액</li><li>총 영업 기회 예상 수익</li><li>구독 취소</li><li>주소 삭제 이유</li><li>업데이트 시간</li><li>웹 사이트</li></ul></td>
</tr>
</table>
