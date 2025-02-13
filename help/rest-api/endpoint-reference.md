---
title: 끝점 참조
feature: REST API
description: Marketo API 끝점 참조
exl-id: 27d16b6f-865a-4e40-ab9c-cbabe2927472
source-git-commit: 3632d2b713d97a2c895c65f144c07e62e1d369cb
workflow-type: tm+mt
source-wordcount: '4676'
ht-degree: 3%

---

# 끝점 참조

다음은 Marketo REST API 참조에 대한 링크입니다.

- [자산](https://developer.adobe.com/marketo-apis/api/asset/)
- [ID](https://developer.adobe.com/marketo-apis/api/identity/)
- [리드 데이터베이스](https://developer.adobe.com/marketo-apis/api/mapi/)
- [사용자 관리](https://developer.adobe.com/marketo-apis/api/user/)

## 엔드포인트 목록 {#endpoint_list}

다음은 REST API 엔드포인트의 포괄적인 목록입니다.

| 이름 | 그룹 | 메서드 | URI | 필수 권한 |
|---|---|---|---|---|
| 사용자 지정 활동 추가 | 활동 | POST | /rest/v1/activities/external.json | 읽기-쓰기 활동 |
| 사용자 지정 활동 유형 승인 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/approve.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 속성 만들기 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/attributes/create.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 만들기 | 활동 | POST | /rest/v1/activities/external/type.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 삭제 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/delete.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 속성 삭제 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/attributes/delete.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 설명 | 활동 | GET | /rest/v1/activities/external/type/{apiName}/describe.json | 읽기 전용 활동 메타데이터 |
| 사용자 지정 활동 유형 초안 삭제 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/discardDraft.json | 읽기-쓰기 활동 메타데이터 |
| 활동 유형 가져오기 | 활동 | GET | /rest/v1/activities/types.json | 읽기 전용 활동 |
| 사용자 지정 활동 유형 가져오기 | 활동 | GET | /rest/v1/activities/external/types.json | 읽기 전용 활동 메타데이터 |
| 삭제된 리드 가져오기 | 활동 | GET | /rest/v1/activities/deletedleads.json | 읽기 전용 활동 |
| 리드 활동 가져오기 | 활동 | GET | /rest/v1/activities.json | 읽기 전용 활동 |
| 리드 변경 사항 가져오기 | 활동 | GET | /rest/v1/activities/leadchanges.json | 읽기 전용 활동 |
| 페이징 토큰 가져오기 | 활동 | GET | /rest/v1/activities/pagingtoken.json | 읽기 전용 활동 |
| 사용자 지정 활동 유형 업데이트 | 활동 | POST | /rest/v1/activities/external/type/{apiName}.json | 읽기-쓰기 활동 메타데이터 |
| 사용자 지정 활동 유형 속성 업데이트 | 활동 | POST | /rest/v1/activities/external/type/{apiName}/attributes/update.json | 읽기-쓰기 활동 메타데이터 |
| ID | 인증 | GET 또는 게시물 | /identity/oauth/token | None |
| 활동 내보내기 작업 취소 | 일괄 내보내기 활동 | POST | /bulk/v1/activities/export/{exportid}/cancel.json | 읽기 전용 활동 |
| 내보내기 활동 작업 만들기 | 일괄 내보내기 활동 | POST | /bulk/v1/activities/export/create.json | 읽기 전용 활동 |
| 활동 내보내기 작업 큐에 넣기 | 일괄 내보내기 활동 | POST | /bulk/v1/activities/export/{exportid}/enqueue.json | 읽기 전용 활동 |
| 내보내기 활동 파일 가져오기 | 일괄 내보내기 활동 | GET | /bulk/v1/activities/export/{exportid}/file.json | 읽기 전용 활동 |
| 내보내기 활동 작업 상태 가져오기 | 일괄 내보내기 활동 | GET | /bulk/v1/activities/export/{exportid}/status.json | 읽기 전용 활동 |
| 내보내기 활동 작업 가져오기 | 일괄 내보내기 활동 | GET | /bulk/v1/activities/export.json | 읽기 전용 활동 |
| 사용자 지정 개체 내보내기 작업 취소 | 사용자 지정 개체 일괄 내보내기 | POST | /bulk/v1/customobjects/export/{exportid}/cancel.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 내보내기 작업 만들기 | 사용자 지정 개체 일괄 내보내기 | POST | /bulk/v1/customobjects/export/create.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 내보내기 작업 큐에 넣기 | 사용자 지정 개체 일괄 내보내기 | POST | /bulk/v1/customobjects/export/{exportid}/enqueue.json | 읽기 전용 사용자 지정 개체 |
| 내보내기 사용자 지정 개체 파일 가져오기 | 사용자 지정 개체 일괄 내보내기 | GET | /bulk/v1/customobjects/export/{exportid}/file.json | 읽기 전용 사용자 지정 개체 |
| 내보내기 사용자 지정 개체 작업 상태 가져오기 | 사용자 지정 개체 일괄 내보내기 | GET | /bulk/v1/customobjects/export/{exportid}/status.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 내보내기 작업 가져오기 | 사용자 지정 개체 일괄 내보내기 | GET | /bulk/v1/customobjects/export.json | 읽기 전용 사용자 지정 개체 |
| 리드 내보내기 작업 취소 | 벌크 내보내기 리드 | POST | /bulk/v1/leads/export/{exportid}/cancel.json | 읽기 전용 리드 |
| 내보내기 리드 작업 만들기 | 벌크 내보내기 리드 | POST | /bulk/v1/leads/export/create.json | 읽기 전용 리드 |
| 리드 내보내기 작업 큐에 넣기 | 벌크 내보내기 리드 | POST | /bulk/v1/leads/export/{exportid}/enqueue.json | 읽기 전용 리드 |
| 내보내기 리드 파일 가져오기 | 벌크 내보내기 리드 | GET | /bulk/v1/leads/export/{exportid}/file.json | 읽기 전용 리드 |
| 리드 내보내기 작업 상태 가져오기 | 벌크 내보내기 리드 | GET | /bulk/v1/leads/export/{exportid}/status.json | 읽기 전용 리드 |
| 내보내기 리드 작업 가져오기 | 벌크 내보내기 리드 | GET | /bulk/v1/leads/export.json | 읽기 전용 리드 |
| 프로그램 구성원 내보내기 작업 취소 | 프로그램 구성원 일괄 내보내기 | POST | /bulk/v1/program/members/export/{exportid}/cancel.json | 읽기 전용 리드 |
| 내보내기 프로그램 구성원 작업 만들기 | 프로그램 구성원 일괄 내보내기 | POST | /bulk/v1/program/members/export/create.json | 읽기 전용 리드 |
| 프로그램 구성원 작업 큐 내보내기 | 프로그램 구성원 일괄 내보내기 | POST | /bulk/v1/program/members/export/{exportid}/enqueue.json | 읽기 전용 리드 |
| 내보내기 프로그램 멤버 파일 가져오기 | 프로그램 구성원 일괄 내보내기 | GET | /bulk/v1/program/members/export/{exportid}/file.json | 읽기 전용 리드 |
| 내보내기 프로그램 멤버 작업 상태 가져오기 | 프로그램 구성원 일괄 내보내기 | GET | /bulk/v1/program/members/export/{exportid}/status.json | 읽기 전용 리드 |
| 내보내기 프로그램 멤버 작업 가져오기 | 프로그램 구성원 일괄 내보내기 | GET | /bulk/v1/program/members/export.json | 읽기 전용 리드 |
| 사용자 지정 개체 가져오기 가져오기 실패 | 사용자 지정 개체 일괄 가져오기 | GET | /bulk/v1/customobjects/import/{id}/failures.json | 사용자 지정 개체 읽기-쓰기 |
| 가져오기 사용자 지정 개체 상태 가져오기 | 사용자 지정 개체 일괄 가져오기 | GET | /bulk/v1/customobjects/import/{id}/status.json | 사용자 지정 개체 읽기-쓰기 |
| 가져오기 사용자 지정 개체 경고 | 사용자 지정 개체 일괄 가져오기 | GET | /bulk/v1/customobjects/import/{id}/warnings.json | 사용자 지정 개체 읽기-쓰기 |
| 사용자 지정 개체 가져오기 | 사용자 지정 개체 일괄 가져오기 | POST | /bulk/v1/customobjects/{apiName}/import.json | 사용자 지정 개체 읽기-쓰기 |
| 가져오기 리드 가져오기 실패 | 리드 일괄 가져오기 | GET | /bulk/v1/leads/batch/{id}/failures.json | 리드 읽기-쓰기 |
| 가져오기 리드 상태 가져오기 | 리드 일괄 가져오기 | GET | /bulk/v1/lead/batch/{id}.json | 리드 읽기-쓰기 |
| 가져오기 리드 경고 가져오기 | 리드 일괄 가져오기 | GET | /bulk/v1/leads/batch/{id}/warnings.json | 리드 읽기-쓰기 |
| 리드 가져오기 | 리드 일괄 가져오기 | POST | /bulk/v1/leads.json | 리드 읽기-쓰기 |
| 가져오기 프로그램 멤버 가져오기 실패 | 프로그램 구성원 일괄 가져오기 | GET | /bulk/v1/program/members/import/{id}/failures.json | 리드 읽기-쓰기 |
| 가져오기 프로그램 멤버 상태 가져오기 | 프로그램 구성원 일괄 가져오기 | GET | /bulk/v1/program/members/import/{id}/status.json | 리드 읽기-쓰기 |
| 가져오기 프로그램 멤버 경고 가져오기 | 프로그램 구성원 일괄 가져오기 | GET | /bulk/v1/program/members/import/{id}/warnings.json | 리드 읽기-쓰기 |
| 프로그램 구성원 가져오기 | 프로그램 구성원 일괄 가져오기 | POST | /bulk/v1/program/{programId}/members/import.json | 리드 읽기-쓰기 |
| ID로 캠페인 가져오기 | 캠페인 | GET | /rest/v1/campaigns/{id}.json | 읽기 전용 캠페인 |
| 캠페인 가져오기 | 캠페인 | GET | /rest/v1/campaigns.json | 읽기 전용 캠페인 |
| 캠페인 요청 | 캠페인 | POST | /rest/v1/campaigns/{id}/trigger.json | 캠페인 읽기-쓰기 |
| 캠페인 예약 | 캠페인 | POST | /rest/v1/campaigns/{id}/schedule.json | 캠페인 읽기-쓰기 |
| 이름으로 채널 가져오기 | 채널 | GET | /rest/asset/v1/channel/byName.json | 읽기 전용 자산 |
| 채널 가져오기 | 채널 | GET | /rest/asset/v1/channels.json | 읽기 전용 자산 |
| 회사 삭제 | 회사 | POST | /rest/v1/companies/delete.json | 읽기-쓰기 회사 |
| 회사 설명 | 회사 | GET | /rest/v1/companies/describe.json | 읽기 전용 회사 |
| 회사 가져오기 | 회사 | GET | /rest/v1/companies.json | 읽기 전용 회사 |
| 회사 동기화 | 회사 | POST | /rest/v1/companies.json | 읽기-쓰기 회사 |
| 이름별 회사 필드 가져오기 | 회사 | GET | /rest/v1/company/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 회사 필드 가져오기 | 회사 | GET | /rest/v1/companies/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 사용자 정의 객체 유형 필드 추가 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/addField.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 지정 개체 유형 승인 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/approve.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 지정 개체 삭제 | 사용자 지정 개체 | POST | /rest/v1/customobjects/{name}/delete.json | 사용자 지정 개체 읽기-쓰기 |
| 사용자 지정 개체 유형 삭제 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/delete.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 정의 객체 유형 필드 삭제 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/deleteField.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 지정 개체 설명 | 사용자 지정 개체 | GET | /rest/v1/customobjects/{name}/describe.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 유형 설명 | 사용자 지정 개체 | GET | /rest/v1/customobjects/schema/{apiName}/describe.json | 읽기 전용 사용자 지정 개체 유형 |
| 사용자 정의 객체 유형 초안 삭제 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/discardDraft.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 지정 개체 가져오기 | 사용자 지정 개체 | GET | /rest/v1/customobjects/{name}.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 연결 가능 개체 가져오기 | 사용자 지정 개체 | GET | /rest/v1/customobjects/schema/linkableObjects.json | 읽기 전용 사용자 지정 개체 유형 |
| 사용자 지정 개체 종속 Assets 가져오기 | 사용자 지정 개체 | GET | /rest/v1/customobjects/schema/{apiName}/dependentAssets.json | 읽기 전용 사용자 지정 개체 유형 |
| 사용자 지정 개체 유형 필드 데이터 유형 가져오기 | 사용자 지정 개체 | GET | /rest/v1/customobjects/schema/fieldDataTypes.json | 읽기 전용 사용자 지정 개체 유형 |
| 사용자 지정 개체 목록 | 사용자 지정 개체 | GET | /rest/v1/customobjects.json | 읽기 전용 사용자 지정 개체 |
| 사용자 지정 개체 유형 목록 | 사용자 지정 개체 | GET | /rest/v1/customobjects/schema.json | 읽기 전용 사용자 지정 개체 유형 |
| 사용자 지정 개체 동기화 | 사용자 지정 개체 | POST | /rest/v1/customobjects/{name}.json | 사용자 지정 개체 읽기-쓰기 |
| 사용자 지정 개체 유형 동기화 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 사용자 정의 객체 유형 필드 업데이트 | 사용자 지정 개체 | POST | /rest/v1/customobjects/schema/{apiName}/updateField.json | 사용자 지정 개체 유형 읽기-쓰기 |
| 이메일 템플릿 초안 승인 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 이메일 템플릿 복제 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/clone.json | 자산 읽기-쓰기 |
| 이메일 템플릿 만들기 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplates.json | 자산 읽기-쓰기 |
| 이메일 템플릿 삭제 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/delete.json | 자산 읽기-쓰기 |
| 이메일 템플릿 초안 삭제 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/discardDraft.json | 자산 읽기-쓰기 |
| ID별 이메일 템플릿 가져오기 | 이메일 템플릿 | GET | /rest/asset/v1/emailTemplate/{id}.json | 읽기 전용 자산 |
| 이름별 이메일 템플릿 가져오기 | 이메일 템플릿 | GET | /rest/asset/v1/emailTemplate/byName.json | 읽기 전용 자산 |
| ID별 이메일 템플릿 콘텐츠 가져오기 | 이메일 템플릿 | GET | /rest/asset/v1/emailTemplate/{id}/content.json | 읽기 전용 자산 |
| 다음에서 사용하는 이메일 템플릿 가져오기: | 이메일 템플릿 | GET | /rest/asset/v1/emailTemplates/{id}/usedBy.json | 읽기 전용 자산 |
| 이메일 템플릿 가져오기 | 이메일 템플릿 | GET | /rest/asset/v1/emailTemplates.json | 읽기 전용 자산 |
| 이메일 템플릿 초안 승인 취소 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/unapprove.json | 자산 읽기-쓰기 |
| 이메일 템플릿 콘텐츠 업데이트 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}/content.json | 자산 읽기-쓰기 |
| 이메일 템플릿 메타데이터 업데이트 | 이메일 템플릿 | POST | /rest/asset/v1/emailTemplate/{id}.json | 자산 읽기-쓰기 |
| 이메일 모듈 추가 | 이메일 | POST | /rest/asset/v1/email/{id}/content/{moduleId}/add.json | 자산 읽기-쓰기 |
| 이메일 초안 승인 | 이메일 | POST | /rest/asset/v1/email/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 이메일 복제 | 이메일 | POST | /rest/asset/v1/email/{id}/clone.json | 자산 읽기-쓰기 |
| 이메일 만들기 | 이메일 | POST | /rest/asset/v1/emails.json | 자산 읽기-쓰기 |
| 이메일 삭제 | 이메일 | POST | /rest/asset/v1/email/{id}/delete.json | 자산 읽기-쓰기 |
| 모듈 삭제 | 이메일 | POST | /rest/asset/v1/email/{id}/content/{moduleId}/delete.json | 자산 읽기-쓰기 |
| 이메일 초안 삭제 | 이메일 | POST | /rest/asset/v1/email/{id}/discardDraft.json | 자산 읽기-쓰기 |
| 이메일 모듈 복제 | 이메일 | POST | /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json | 자산 읽기-쓰기 |
| ID로 이메일 받기 | 이메일 | GET | /rest/asset/v1/email/{id}.json | 읽기 전용 자산 |
| 이름으로 이메일 받기 | 이메일 | GET | /rest/asset/v1/email/byName.json | 읽기 전용 자산 |
| 이메일 콘텐츠 가져오기 | 이메일 | GET | /rest/asset/v1/email/{id}/content.json | 읽기 전용 자산 |
| 이메일 다이내믹 콘텐츠 가져오기 | 이메일 | GET | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 읽기 전용 자산 |
| 이메일 전체 콘텐츠 가져오기 | 이메일 | GET | /rest/asset/v1/email/{id}/fullContent.json | 읽기 전용 자산 |
| 이메일 변수 가져오기 | 이메일 | GET | /rest/asset/v1/email/{id}/variables.json | 읽기 전용 자산 |
| 이메일 CC 필드 가져오기 | 이메일 | GET | /rest/asset/v1/email/ccFields.json | 읽기 전용 자산 |
| 이메일 가져오기 | 이메일 | GET | /rest/asset/v1/emails.json | 읽기 전용 자산 |
| 이메일 모듈 재배열 | 이메일 | POST | /rest/asset/v1/email/{id}/content/rearrange.json | 자산 읽기-쓰기 |
| 이메일 모듈 이름 변경 | 이메일 | POST | /rest/asset/v1/email/{id}/content/{moduleId}/rename.json | 자산 읽기-쓰기 |
| 샘플 이메일 보내기 | 이메일 | POST | /rest/asset/v1/email/{id}/sendSample.json | 자산 읽기-쓰기 |
| 이메일 승인 취소 | 이메일 | POST | /rest/asset/v1/email/{id}/unapprove.json | 자산 읽기-쓰기 |
| 이메일 콘텐츠 업데이트 | 이메일 | POST | /rest/asset/v1/email/{id}/content.json | 자산 읽기-쓰기 |
| 이메일 콘텐츠 섹션 업데이트 | 이메일 | POST | /rest/asset/v1/email/{id}/content/{htmlId}.json | 자산 읽기-쓰기 |
| 이메일 다이내믹 콘텐츠 섹션 업데이트 | 이메일 | POST | /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json | 자산 읽기-쓰기 |
| 이메일 전체 콘텐츠 업데이트 | 이메일 | POST | /rest/asset/v1/emails/{id}/fullContent.json | 자산 읽기-쓰기 |
| 이메일 메타데이터 업데이트 | 이메일 | POST | /rest/asset/v1/email/{id}.json | 자산 읽기-쓰기 |
| 이메일 변수 업데이트 | 이메일 | POST | /rest/asset/v1/email/{id}/variable/{name}.json | 자산 읽기-쓰기 |
| 파일 만들기 | 파일 | POST | /rest/asset/v1/files.json | 자산 읽기-쓰기 |
| ID로 파일 가져오기 | 파일 | GET | /rest/asset/v1/file/{id}.json | 읽기 전용 자산 |
| 이름으로 파일 가져오기 | 파일 | GET | /rest/asset/v1/file/byName.json | 읽기 전용 자산 |
| 파일 가져오기 | 파일 | GET | /rest/asset/v1/files.json | 읽기 전용 자산 |
| 파일 콘텐츠 업데이트 | 파일 | POST | /rest/asset/v1/file/{id}/content.json | 자산 읽기-쓰기 |
| 폴더 만들기 | 폴더 | POST | /rest/asset/v1/folders.json | 자산 읽기-쓰기 |
| 폴더 삭제 | 폴더 | POST | /rest/asset/v1/folder/{id}/delete.json | 자산 읽기-쓰기 |
| ID로 폴더 가져오기 | 폴더 | GET | /rest/asset/v1/folder/{id}.json | 읽기 전용 자산 |
| 이름으로 폴더 가져오기 | 폴더 | GET | /rest/asset/v1/folder/byName.json | 읽기 전용 자산 |
| 폴더 컨텐츠 가져오기 | 폴더 | GET | /rest/asset/v1/folder/{id}/content.json | 읽기 전용 자산 |
| 폴더 가져오기 | 폴더 | GET | /rest/asset/v1/folders.json | 읽기 전용 자산 |
| 폴더 메타데이터 업데이트 | 폴더 | POST | /rest/asset/v1/folder/{id}.json | 자산 읽기-쓰기 |
| 양식에 필드 추가 | 양식 필드 | POST | /rest/asset/v1/form/{id}/fields.json | 자산 읽기-쓰기 |
| 양식에 필드 세트 추가 | 양식 필드 | POST | /rest/asset/v1/form/{id}/fieldSet.json | 자산 읽기-쓰기 |
| 양식 필드 가시성 규칙 추가 | 양식 필드 | POST | /rest/asset/v1/form/{formId}/field/{fieldId}/visibility.json | 자산 읽기-쓰기 |
| 리치 텍스트 필드 추가 | 양식 필드 | POST | /rest/asset/v1/form/{id}/richText.json | 자산 읽기-쓰기 |
| 필드 집합에서 필드 삭제 | 양식 필드 | POST | /rest/asset/v1/form/{id}/fieldSet/{fieldSetId}/field/{fieldId}/delete.json | 자산 읽기-쓰기 |
| 양식 필드 삭제 | 양식 필드 | POST | /rest/asset/v1/form/{id}/field/{fieldId}/delete.json | 자산 읽기-쓰기 |
| 사용 가능한 양식 필드 가져오기 | 양식 필드 | GET | /rest/asset/v1/form/fields.json | 읽기 전용 자산 |
| 사용 가능한 양식 프로그램 멤버 필드 가져오기 | 양식 필드 | GET | /rest/asset/v1/form/programMemberFields.json | 읽기 전용 자산 |
| 양식에 대한 필드 가져오기 | 양식 필드 | GET | /rest/asset/v1/form/{id}/fields.json | 읽기 전용 자산 |
| 필드 위치 업데이트 | 양식 필드 | POST | /rest/asset/v1/form/{id}/reArrange.json | 자산 읽기-쓰기 |
| 양식 필드 업데이트 | 양식 필드 | POST | /rest/asset/v1/form/{id}/field/{fieldId}.json | 자산 읽기-쓰기 |
| 양식 초안 승인 | Forms | POST | /rest/asset/v1/form/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 양식 복제 | Forms | POST | /rest/asset/v1/form/{id}/clone.json | 자산 읽기-쓰기 |
| 양식 만들기 | Forms | POST | /rest/asset/v1/forms.json | 자산 읽기-쓰기 |
| 다음에서 양식 사용: | Forms | GET | /rest/asset/v1/form/{id}/usedBy.json | 자산 읽기-쓰기 |
| 양식 삭제 | Forms | POST | /rest/asset/v1/form/{id}/delete.json | 자산 읽기-쓰기 |
| 양식 초안 삭제 | Forms | POST | /rest/asset/v1/form/{id}/discardDraft.json | 자산 읽기-쓰기 |
| ID로 양식 가져오기 | Forms | GET | /rest/asset/v1/form/{id}.json | 읽기 전용 자산 |
| 이름별 양식 가져오기 | Forms | GET | /rest/asset/v1/form/byName.json | 읽기 전용 자산 |
| Forms 가져오기 | Forms | GET | /rest/asset/v1/forms.json | 읽기 전용 자산 |
| 양식 ID로 감사 인사 페이지 받기 | Forms | GET | /rest/asset/v1/form/{id}/thankYouPage.json | 읽기 전용 자산 |
| 양식 메타데이터 업데이트 | Forms | POST | /rest/asset/v1/form/{id}.json | 자산 읽기-쓰기 |
| 업데이트 제출 단추 | Forms | POST | /rest/asset/v1/{id}/submitButton.json | 자산 읽기-쓰기 |
| 감사 인사 페이지 업데이트 | Forms | POST | /rest/asset/v1/form/{id}/thankYouPage.json | 자산 읽기-쓰기 |
| 랜딩 페이지 콘텐츠 섹션 추가 | 랜딩 페이지 콘텐츠 | POST | /rest/asset/v1/landingPage/{id}/content.json | 자산 읽기-쓰기 |
| 랜딩 페이지 콘텐츠 섹션 삭제 | 랜딩 페이지 콘텐츠 | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}/delete.json | 자산 읽기-쓰기 |
| 랜딩 페이지 콘텐츠 가져오기 | 랜딩 페이지 콘텐츠 | GET | /rest/asset/v1/landingPage/{id}/content.json | 읽기 전용 자산 |
| 랜딩 페이지 다이내믹 콘텐츠 가져오기 | 랜딩 페이지 콘텐츠 | GET | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 읽기 전용 자산 |
| 랜딩 페이지 콘텐츠 섹션 업데이트 | 랜딩 페이지 콘텐츠 | POST | /rest/asset/v1/landingPage/{id}/content/{contentId}.json | 자산 읽기-쓰기 |
| 랜딩 페이지 다이내믹 콘텐츠 섹션 업데이트 | 랜딩 페이지 콘텐츠 | POST | /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 승인 초안 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 복제 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/clone.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 만들기 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 삭제 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/delete.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 초안 삭제 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/discardDraft.json | 자산 읽기-쓰기 |
| ID별 랜딩 페이지 템플릿 가져오기 | 랜딩 페이지 템플릿 | GET | /rest/asset/v1/landingPageTemplate/{id}.json | 읽기 전용 자산 |
| 이름별 랜딩 페이지 템플릿 가져오기 | 랜딩 페이지 템플릿 | GET | /rest/asset/v1/landingPageTemplates/byName.json | 읽기 전용 자산 |
| 랜딩 페이지 템플릿 콘텐츠 가져오기 | 랜딩 페이지 템플릿 | GET | /rest/asset/v1/landingPageTemplate/{id}/content.json | 읽기 전용 자산 |
| 랜딩 페이지 템플릿 가져오기 | 랜딩 페이지 템플릿 | GET | /rest/asset/v1/landingPageTemplates.json | 읽기 전용 자산 |
| 랜딩 페이지 템플릿 승인 취소 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/unapprove.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 콘텐츠 업데이트 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}/content.json | 자산 읽기-쓰기 |
| 랜딩 페이지 템플릿 메타데이터 업데이트 | 랜딩 페이지 템플릿 | POST | /rest/asset/v1/landingPageTemplate/{id}.json | 자산 읽기-쓰기 |
| 랜딩 페이지 초안 승인 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 랜딩 페이지 복제 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/clone.json | 자산 읽기-쓰기 |
| 랜딩 페이지 만들기 | 랜딩 페이지 | POST | /rest/asset/v1/landingPages.json | 자산 읽기-쓰기 |
| 랜딩 페이지 삭제 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/delete.json | 자산 읽기-쓰기 |
| 랜딩 페이지 초안 삭제 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/discardDraft.json | 자산 읽기-쓰기 |
| ID별 랜딩 페이지 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/랜딩 페이지/{id}.json | 읽기 전용 자산 |
| 이름별 랜딩 페이지 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/landingPage/byName.json | 읽기 전용 자산 |
| 랜딩 페이지 변수 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/landingPage/{id}/variables.json | 읽기 전용 자산 |
| 랜딩 페이지 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/landingPages.json | 읽기 전용 자산 |
| 랜딩 페이지 미리 보기 | 랜딩 페이지 | GET | /rest/asset/v1/landingPage/{id}/preview.json | 읽기 전용 자산 |
| 랜딩 페이지 승인 취소 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/unapprove.json | 자산 읽기-쓰기 |
| 랜딩 페이지 메타데이터 업데이트 | 랜딩 페이지 | POST | /rest/asset/v1/{id}.json | 자산 읽기-쓰기 |
| 랜딩 페이지 변수 업데이트 | 랜딩 페이지 | POST | /rest/asset/v1/landingPage/{id}/variable/{variableId}.json | 자산 읽기-쓰기 |
| 랜딩 페이지 리디렉션 규칙 만들기 | 랜딩 페이지 | POST | /rest/asset/v1/redirectRules.json | 리디렉션 규칙 읽기-쓰기 |
| 랜딩 페이지 리디렉션 규칙 삭제 | 랜딩 페이지 | POST | /rest/asset/v1/redirectRule/{id}/delete.json | 리디렉션 규칙 읽기-쓰기 |
| 랜딩 페이지 리디렉션 규칙 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/redirectRules.json | 읽기 전용 리디렉션 규칙 |
| ID별 랜딩 페이지 리디렉션 규칙 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/리디렉션 규칙/{id}.json | 읽기 전용 리디렉션 규칙 |
| 랜딩 페이지 리디렉션 규칙 업데이트 | 랜딩 페이지 | POST | /rest/asset/v1/리디렉션 규칙/{id}.json | 리디렉션 규칙 읽기-쓰기 |
| 랜딩 페이지 도메인 가져오기 | 랜딩 페이지 | GET | /rest/asset/v1/landingPageDomains.json | 읽기 전용 리디렉션 규칙 |
| 리드 연결 | 잠재 고객 | POST | /rest/v1/leads/{id}/associate.json | 리드 읽기-쓰기 |
| 잠재 고객 프로그램 상태 변경 | 잠재 고객 | POST | /rest/v1/leads/programs/{programId}/status.json | 리드 읽기-쓰기 |
| 리드 삭제 | 잠재 고객 | POST | /rest/v1/leads.json | 리드 읽기-쓰기 |
| 리드 설명 | 잠재 고객 | GET | /rest/v1/leads/describe.json | 읽기 전용 리드 |
| 리드2 설명 | 잠재 고객 | GET | /rest/v1/leads/describe2.json | 읽기 전용 리드 |
| 프로그램 구성원 설명 | 잠재 고객 | GET | /rest/v1/program/members/describe.json | 읽기 전용 리드 |
| ID로 리드 가져오기 | 잠재 고객 | GET | /rest/v1/lead/{id}.json | 읽기 전용 리드 |
| 리드 파티션 가져오기 | 잠재 고객 | GET | /rest/v1/leads/partitions.json | 읽기 전용 리드 |
| 필터 유형별 리드 가져오기 | 잠재 고객 | GET | /rest/v1/leads.json | 읽기 전용 리드 |
| 프로그램 ID로 리드 가져오기 | 잠재 고객 | GET | /rest/v1/lead/programs/{programId}.json | 읽기 전용 리드 |
| 잠재 고객 병합 | 잠재 고객 | POST | /rest/v1/leads/{id}/merge.json | 리드 읽기-쓰기 |
| 잠재 고객 ID별 목록 가져오기 | 잠재 고객 | GET | /rest/v1/lead/{leadId}.json | 읽기 전용 자산 |
| 리드 ID로 프로그램 가져오기 | 잠재 고객 | GET | /rest/v1/lead/{leadId}programMembership.json | 읽기 전용 자산 |
| 잠재 고객 ID로 스마트 캠페인 가져오기 | 잠재 고객 | GET | /rest/v1/leads/{leadId}/smartCampaignMembership.json | 읽기 전용 자산 |
| Marketo으로 리드 푸시 | 잠재 고객 | POST | /rest/v1/leads/partitions.json | 리드 읽기-쓰기 |
| 양식 제출 | 잠재 고객 | POST | /rest/v1/leads/submitForm.json | 리드 읽기-쓰기 |
| 잠재 고객 동기화 | 잠재 고객 | POST | /rest/v1/leads.json | 리드 읽기-쓰기 |
| 리드 파티션 업데이트 | 잠재 고객 | POST | /rest/v1/leads/partitions.json | 리드 읽기-쓰기 |
| 이름별 잠재 고객 필드 가져오기 | 잠재 고객 | GET | /rest/v1/lead/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 리드 필드 가져오기 | 잠재 고객 | GET | /rest/v1/leads/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 리드 필드 만들기 | 잠재 고객 | POST | /rest/v1/leads/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 리드 필드 업데이트 | 잠재 고객 | POST | /rest/v1/lead/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 명명된 계정 목록 구성원 추가 | 명명된 계정 목록 | POST | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 명명된 계정 읽기-쓰기 |
| 명명된 계정 목록 삭제 | 명명된 계정 목록 | POST | /rest/v1/namedaccountlists/delete.json | 명명된 계정 목록 읽기-쓰기 |
| 명명된 계정 목록 구성원 가져오기 | 명명된 계정 목록 | GET | /rest/v1/namedaccountlist/{id}/namedaccounts.json | 읽기 전용 명명된 계정 |
| 명명된 계정 목록 가져오기 | 명명된 계정 목록 | GET | /rest/v1/namedaccountlists.json | 읽기 전용 명명된 계정 목록 |
| 명명된 계정 목록 구성원 제거 | 명명된 계정 목록 | POST | /rest/v1/namedaccountlist/{id}/namedaccounts/remove.json | 명명된 계정 읽기-쓰기 |
| 명명된 계정 목록 동기화 | 명명된 계정 목록 | POST | /rest/v1/namedaccountlists.json | 명명된 계정 목록 읽기-쓰기 |
| 명명 계정 삭제 | 명명된 계정 | POST | /rest/v1/namedaccounts/delete.json | 명명된 계정 읽기-쓰기 |
| 명명 계정 설명 | 명명된 계정 | GET | /rest/v1/namedaccounts/describe.json | 읽기 전용 명명된 계정 |
| 명명된 계정 가져오기 | 명명된 계정 | GET | /rest/v1/namedaccounts.json | 읽기 전용 명명된 계정 |
| 명명 계정 동기화 | 명명된 계정 | POST | /rest/v1/namedaccounts.json | 명명된 계정 읽기-쓰기 |
| 이름으로 명명된 계정 필드 가져오기 | 명명된 계정 | GET | /rest/v1/namedaccounts/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 명명된 계정 필드 가져오기 | 명명된 계정 | GET | /rest/v1/namedaccounts/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 기회 삭제 | 기회 | POST | /rest/v1/opportunities/delete.json | 읽기-쓰기 영업 기회 |
| 영업 기회 역할 삭제 | 기회 | POST | /rest/v1/opportunities/roles/delete.json | 읽기-쓰기 영업 기회 |
| 영업 기회 설명 | 기회 | GET | /rest/v1/opportunities/describe.json | 읽기 전용 영업 기회 |
| 영업 기회 역할 설명 | 기회 | GET | /rest/v1/opportunities/roles/describe.json | 읽기 전용 영업 기회 |
| 기회 가져오기 | 기회 | GET | /rest/v1/opportunities.json | 읽기 전용 영업 기회 |
| 영업 기회 역할 가져오기 | 기회 | GET | /rest/v1/opportunities/roles.json | 읽기 전용 영업 기회 |
| 기회 동기화 | 기회 | POST | /rest/v1/opportunities.json | 읽기-쓰기 영업 기회 |
| 영업 기회 역할 동기화 | 기회 | POST | /rest/v1/opportunities/roles.json | 읽기-쓰기 영업 기회 |
| 이름별 영업 기회 필드 가져오기 | 기회 | GET | /rest/v1/opportunities/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 영업 기회 필드 가져오기 | 기회 | GET | /rest/v1/opportunities/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 프로그램 구성원 삭제 | 프로그램 구성원 | POST | /rest/v1/programs/{programId}/members/delete.json | 리드 읽기-쓰기 |
| 프로그램 구성원 설명 | 프로그램 구성원 | GET | /rest/v1/programs/members/describe.json | 읽기 전용 리드 |
| 프로그램 구성원 가져오기 | 프로그램 구성원 | GET | /rest/v1/programs/{programId}/members.json | 읽기 전용 리드 |
| 프로그램 구성원 데이터 동기화 | 프로그램 구성원 | POST | /rest/v1/programs/{programId}/members.json | 리드 읽기-쓰기 |
| 동기화 프로그램 구성원 상태 | 프로그램 구성원 | POST | /rest/v1/programs/{programId}/members/status.json | 리드 읽기-쓰기 |
| 이름별 프로그램 구성원 필드 가져오기 | 프로그램 구성원 | GET | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 프로그램 구성원 필드 가져오기 | 프로그램 구성원 | GET | /rest/v1/programs/members/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 프로그램 구성원 필드 만들기 | 프로그램 구성원 | POST | /rest/v1/programs/members/schema/fields.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 프로그램 구성원 필드 업데이트 | 프로그램 구성원 | POST | /rest/v1/programs/members/schema/fields/{fieldApiName}.json | 읽기-쓰기 스키마 사용자 정의 필드 |
| 프로그램 승인 | 프로그램 | POST | /rest/asset/v1/program/{id}/approve.json | 자산 읽기-쓰기 |
| 프로그램 복제 | 프로그램 | POST | /rest/asset/v1/program/{id}/clone.json | 자산 읽기-쓰기 |
| 프로그램 제작 | 프로그램 | POST | /rest/asset/v1/programs.json | 자산 읽기-쓰기 |
| 프로그램 삭제 | 프로그램 | POST | /rest/asset/v1/program/{id}/delete.json | 자산 읽기-쓰기 |
| ID로 프로그램 가져오기 | 프로그램 | GET | /rest/asset/v1/program/{id}.json | 읽기 전용 자산 |
| 이름으로 프로그램 가져오기 | 프로그램 | GET | /rest/asset/v1/program/byName.json | 읽기 전용 자산 |
| 프로그램 가져오기 | 프로그램 | GET | /rest/asset/v1/programs.json | 읽기 전용 자산 |
| 태그로 프로그램 가져오기 | 프로그램 | GET | /rest/asset/v1/program/byTag.json | 읽기 전용 자산 |
| 프로그램 ID별 스마트 목록 가져오기 | 프로그램 | GET | /rest/asset/v1/program/{id}/smartList.json | 읽기 전용 자산 |
| 프로그램 승인 취소 | 프로그램 | POST | /rest/asset/v1/program/{id}/unapprove.json | 자산 읽기-쓰기 |
| 프로그램 메타데이터 업데이트 | 프로그램 | POST | /rest/asset/v1/program/{id}.json | 자산 읽기-쓰기 |
| 프로그램 태그 업데이트 | 프로그램 | POST | /rest/asset/v1/program/{id}/tag/{tagType}.json | 자산 읽기-쓰기 |
| 프로그램 태그 삭제 | 프로그램 | POST | /rest/asset/v1/program/{id}/tag/{tagType}/delete.json | 자산 읽기-쓰기 |
| SalesPerson 삭제 | 영업 담당자 | POST | /rest/v1/salespersons/delete.json | 읽기-쓰기 영업 담당자 |
| SalesPerson 설명 | 영업 담당자 | GET | /rest/v1/salespersons/describe.json | 읽기 전용 영업 담당자 |
| SalesPerson 가져오기 | 영업 담당자 | GET | /rest/v1/salespersons.json | 읽기 전용 영업 담당자 |
| SalesPerson 동기화 | 영업 담당자 | POST | /rest/v1/salespersons.json | 읽기-쓰기 영업 담당자 |
| 세그먼트 가져오기 | 세그먼트 | GET | /rest/asset/v1/segmentation.json | 읽기 전용 자산 |
| 세그먼트화할 세그먼트 가져오기 | 세그먼트 | GET | /rest/asset/v1/segmentation/{id}/segments.json | 읽기 전용 자산 |
| 스마트 캠페인 활성화 | 스마트 캠페인 | POST | /rest/asset/v1/smartCampaign/{id}/activate.json | 캠페인 활성화 |
| 스마트 캠페인 복제 | 스마트 캠페인 | POST | /rest/asset/v1/smartCampaign/{id}/clone.json | 자산 읽기-쓰기 |
| 스마트 캠페인 만들기 | 스마트 캠페인 | POST | /rest/asset/v1/smartCampaigns.json | 자산 읽기-쓰기 |
| 스마트 캠페인 비활성화 | 스마트 캠페인 | POST | /rest/asset/v1/smartCampaign/{id}/deactivate.json | 캠페인 비활성화 |
| 스마트 캠페인 삭제 | 스마트 캠페인 | POST | /rest/asset/v1/smartCampaign/{id}/delete.json | 자산 읽기-쓰기 |
| 스마트 캠페인 가져오기 | 스마트 캠페인 | GET | /rest/asset/v1/smartCampaigns.json | 읽기 전용 자산 |
| ID별 스마트 캠페인 가져오기 | 스마트 캠페인 | GET | /rest/asset/v1/스마트 캠페인/{id}.json | 읽기 전용 자산 |
| 이름별 스마트 캠페인 가져오기 | 스마트 캠페인 | GET | /rest/asset/v1/smartCampaign/byName.json | 읽기 전용 자산 |
| 스마트 캠페인 ID로 스마트 목록 가져오기 | 스마트 캠페인 | GET | /rest/asset/v1/smartCampaign/{id}/smartList.json | 읽기 전용 자산 |
| 스마트 캠페인 업데이트 | 스마트 캠페인 | POST | /rest/asset/v1/스마트 캠페인/{id}.json | 자산 읽기-쓰기 |
| 스마트 목록 복제 | 스마트 목록 | POST | /rest/asset/v1/smartList/{id}/clone.json | 자산 읽기-쓰기 |
| 스마트 목록 삭제 | 스마트 목록 | POST | /rest/asset/v1/smartList/{id}/delete.json | 자산 읽기-쓰기 |
| ID별 스마트 목록 가져오기 | 스마트 목록 | GET | /rest/asset/v1/스마트 목록/{id}.json | 읽기 전용 자산 |
| 이름별 스마트 목록 가져오기 | 스마트 목록 | GET | /rest/asset/v1/smartList/byName.json | 읽기 전용 자산 |
| 스마트 목록 가져오기 | 스마트 목록 | GET | /rest/asset/v1/smartLists.json | 읽기 전용 자산 |
| 코드 조각 초안 승인 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/approveDraft.json | 자산 읽기-쓰기 |
| 코드 조각 복제 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/clone.json | 자산 읽기-쓰기 |
| 코드 조각 만들기 | 스니펫 | POST | /rest/asset/v1/snippets.json | 자산 읽기-쓰기 |
| 코드 조각 삭제 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/delete.json | 자산 읽기-쓰기 |
| 코드 조각 초안 삭제 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/discardDraft.json | 자산 읽기-쓰기 |
| 다이내믹 콘텐츠 가져오기 | 스니펫 | GET | /rest/asset/v1/snippet/{id}/dynamicContent.json | 읽기 전용 자산 |
| ID별 코드 조각 가져오기 | 스니펫 | GET | /rest/asset/v1/snippet/{id}.json | 읽기 전용 자산 |
| 코드 조각 콘텐츠 가져오기 | 스니펫 | GET | /rest/asset/v1/snippet/{id}/content.json | 읽기 전용 자산 |
| 코드 조각 가져오기 | 스니펫 | GET | /rest/asset/v1/snippets.json | 읽기 전용 자산 |
| 코드 조각 승인 취소 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/unapprove.json | 자산 읽기-쓰기 |
| 코드 조각 콘텐츠 업데이트 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/content.json | 자산 읽기-쓰기 |
| 코드 조각 동적 콘텐츠 업데이트 | 스니펫 | POST | /rest/asset/v1/snippet/{id}/dynamicContent/{segmentId}.json | 자산 읽기-쓰기 |
| 코드 조각 메타데이터 업데이트 | 스니펫 | POST | /rest/asset/v1/snippet/{id}.json | 자산 읽기-쓰기 |
| 목록에 추가 | 정적 목록 | POST | /rest/v1/lists/{listId}/leads.json | 리드 읽기-쓰기 |
| 정적 목록 만들기 | 정적 목록 | POST | /asset/v1/staticLists.json | 자산 읽기-쓰기 |
| 정적 목록 삭제 | 정적 목록 | POST | /asset/v1/staticList/{id}/delete.json | 자산 읽기-쓰기 |
| 목록 ID로 리드 가져오기 | 정적 목록 | GET | /rest/v1/lists/{listId}/leads.json | 읽기 전용 리드 |
| ID별 목록 가져오기 | 정적 목록 | GET | /rest/v1/lists/{id}.json | 읽기 전용 리드 |
| 목록 가져오기 | 정적 목록 | GET | /rest/v1/lists.json | 읽기 전용 리드 |
| ID별 정적 목록 가져오기 | 정적 목록 | GET | /asset/v1/staticList/{id}.json | 읽기 전용 자산 |
| 이름별 정적 목록 가져오기 | 정적 목록 | GET | /asset/v1/staticList/byName.json | 읽기 전용 자산 |
| 정적 목록 가져오기 | 정적 목록 | GET | /asset/v1/staticLists.json | 읽기 전용 자산 |
| 목록 구성원 | 정적 목록 | GET | /rest/v1/lists/{listId}/leads/ismember.json | 읽기 전용 리드 |
| 목록에서 제거 | 정적 목록 | DELETE | /rest/v1/lists/{listId}/leads.json | 리드 읽기-쓰기 |
| 정적 목록 메타데이터 업데이트 | 정적 목록 | POST | /asset/v1/staticList/{id}.json | 자산 읽기-쓰기 |
| 이름별 태그 가져오기 | 태그 | GET | /rest/asset/v1/tagType/byName.json | 읽기 전용 자산 |
| 태그 유형 가져오기 | 태그 | GET | /rest/asset/v1/tagTypes.json | 읽기 전용 자산 |
| 토큰 만들기 | 토큰 | POST | /rest/asset/v1/folder/{id}/tokens.json | 자산 읽기-쓰기 |
| 이름별 토큰 삭제 | 토큰 | POST | /rest/asset/v1/folder/{id}/tokens/delete.json | 자산 읽기-쓰기 |
| 폴더 ID별 토큰 가져오기 | 토큰 | GET | /rest/asset/v1/folder/{id}/tokens.json | 읽기 전용 자산 |
| 역할 추가 | 사용자 관리 | POST | /userservice/management/v1/users/{userid}/roles/create.json | 사용자 관리 Api 액세스 |
| 초대된 사용자 삭제 | 사용자 관리 | POST | /userservice/management/v1/users/{userId}/invite/delete.json | 사용자 관리 Api 액세스 |
| 역할 삭제 | 사용자 관리 | POST | /userservice/management/v1/users/{userid}/roles/delete.json | 사용자 관리 Api 액세스 |
| 사용자 삭제 | 사용자 관리 | POST | /userservice/management/v1/users/{userId}/delete.json | 사용자 관리 Api 액세스 |
| Id로 초대된 사용자 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/{userid}/invite.json | 사용자 관리 Api 액세스 |
| 역할 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/roles.json | 사용자 관리 Api 액세스 |
| Id로 역할 및 작업 공간 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/{userid}/roles.json | 사용자 관리 Api 액세스 |
| 사용자 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/allusers.json | 사용자 관리 Api 액세스 |
| ID로 사용자 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/{userid}/user.json | 사용자 관리 Api 액세스 |
| 작업 공간 가져오기 | 사용자 관리 | GET | /userservice/management/v1/users/workspaces.json | 사용자 관리 Api 액세스 |
| 사용자 초대 | 사용자 관리 | POST | /userservice/management/v1/users/invite.json | 사용자 관리 Api 액세스 |
| 사용자 속성 업데이트 | 사용자 관리 | POST | /userservice/management/v1/users/{userId}/update.json | 사용자 관리 Api 액세스 |