---
title: REST API로 마이그레이션
feature: SOAP
description: SOAP에서 REST API로 마이그레이션
exl-id: c2956db3-defe-4163-99f3-58654ce8ee2b
source-git-commit: 8a785b0719e08544ed1a87772faf90bd9dda3077
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# REST API로 마이그레이션

Marketo Engage SOAP API는 2025년 10월 31일 이후에 사용이 중단됩니다. 서비스 중단을 방지하려면 이 날짜까지 SOAP API를 사용하는 기존의 모든 통합을 중단하거나 [Marketo Engage REST API](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/rest-api)&#x200B;(으)로 마이그레이션해야 합니다.

## 마이그레이션

SOAP API는 [REST AP](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/rest-api)I와 비교하여 제한된 범위의 사용 사례를 지원합니다. 사용 사례를 매핑할 끝점을 결정할 때는 [Marketo 통합 모범 사례](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/marketo-integration-best-practices)를 따라야 합니다

[참조 아키텍처](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/reference-architectures)을(를) [CRM 동기화](https://experienceleague.adobe.com/docs/marketo-developer/assets/sync-architecture-whitepaper.pdf?lang=en) 및 [Data Warehouse 내보내기](https://experienceleague.adobe.com/docs/marketo-developer/assets/reference_architecture.pdf?lang=en) 사용 사례에 사용할 수 있습니다.

## 인증

[인증 설명서](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/authentication)

Marketo REST API는 클라이언트 자격 증명 부여 유형의 OAuth 2.0 기반 인증을 사용합니다. 액세스 토큰은 생성 후 1시간 동안 유효합니다.

## 잠재 고객

[리드 API 설명서](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/leads)

SOAP API는 리드 데이터 동기화, [Munchkin 쿠키 연결](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/javascriptapi/leadtracking/lead-tracking) 및 리드 병합을 지원합니다. 응용 프로그램에서 SOAP syncLead 메서드를 호출하고 `marketoCookie` 매개 변수를 설정하는 경우 다음 중 하나를 통해 마이그레이션할 수 있습니다.

1. [리드 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) REST 메서드를 사용한 다음 [연결된 리드](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST)를 사용합니다.
2. 일부 Marketing Assets의 구성과 [Forms API](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/forms)와의 상호 작용이 필요하지만 [양식 제출](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/leads)을 호출할 수 있습니다

`foreignSysPersonId` 키 유형을 사용하는 응용 프로그램은 이 외부 식별자를 나타내기 위해 사용자 지정 잠재 고객 필드로 마이그레이션하고 [잠재 고객 동기화](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/leads#create-and-update) 또는 [대량 잠재 고객 가져오기](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import) REST 메서드를 사용해야 합니다.

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [getLead](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/getlead) | [ID별 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET), [필터 유형별 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) |
| [getMultipleLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/getmultipleleads) | [ID별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET), [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET), [프로그램 ID별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByProgramIdUsingGET), [목록 ID별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByListIdUsingGET), [일괄 리드 내보내기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads) |
| [mergeLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/mergeleads) | [리드 병합](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) |
| [syncLead](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/synclead) | [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) [양식 제출](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST) [잠재 고객 연결](https://developer.adobe.com/marketo-apis/api/mapi/#operation/associateLeadUsingPOST) |
| [syncMultipleLeads](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/leads/syncmultipleleads) | [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) [일괄 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |

## M 오브젝트

M Objects는 외부 분석을 위해 Opportunity Attribution 데이터 내보내기를 지원하는 포괄적인 개념으로, Opportunity, Opportunity Roles 및 Programs의 세 가지 객체 유형으로 작업했습니다.

REST 설명서:

- [기회](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/opportunities)
- [역할](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/opportunity-roles)
- [프로그램](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/programs)

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [deleteMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/deletemobjects) | [기회 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST), [기회 역할 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunityRolesUsingPOST) |
| [describeMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/describemobject) | [영업 기회 설명](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_4), [영업 기회 설명](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [getMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/getmobjects) | [기회 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getOpportunitiesUsingGET), [기회 역할 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeOpportunityRoleUsingGET) |
| [listMObject](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/listmobjects) | N/A |
| [syncMObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/marketo-objects/syncmobjects) | [기회 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunitiesUsingPOST), [기회 동기화 역할](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncOpportunityRolesUsingPOST) |
| [getChannels](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/programs/getchannels) | [채널 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllChannelsUsingGET) |
| [getTags](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/programs/gettags) | [태그 형식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagTypesUsingGET), [이름별 태그 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getTagByNameUsingGET) |

## 정적 목록

SOAP API의 정적 목록 사용 사례는 [목록에 추가](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST), [리드 일괄 가져오기](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-lead-import) 또는 [목록에서 제거](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) REST 메서드를 사용하여 수행할 수 있는 멤버십 및 리드 데이터 수집 및 멤버십 제거로 제한됩니다.

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [getImportToListStatus](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/getimporttoliststatus) | [리드 일괄 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [importToList](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/importtolist) | [목록에 추가](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addLeadsToListUsingPOST) [리드 일괄 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads) |
| [listOperation](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/static-lists/listoperation) | [목록에서 제거](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE) |

## 활동

SOAP API는 활동 검색만 지원합니다.

REST 설명서:

- [동기 활동](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/activities)
- [일괄 활동 추출](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-extract/bulk-activity-extract)

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [getLeadActivity](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/activities/getleadactivity) | [일괄 내보내기 활동](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities) [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) |
| [getLeadChanges](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/activities/getleadchanges) | [일괄 내보내기 활동](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities) [잠재 고객 변경 사항 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadChangesUsingGET) |

## 캠페인

REST 설명서:

- [스마트 캠페인](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns)

SOAP API는 스마트 캠페인에 대한 세 가지 사용 사례만 지원합니다. [요청 가능한 스마트 캠페인에 대한 잠재 고객 충족](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns#trigger), 해당 요청 가능한 캠페인 검색 및 [스마트 캠페인의 향후 실행 예약](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/smart-campaigns#schedule).

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [getCampaignsForSource](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/getcampaignsforsource) | [스마트 캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllSmartCampaignsGET) |
| [requestCampaign](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/requestcampaign) | [캠페인 요청](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST) |
| [scheduleCampaign](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/campaigns/schedulecampaign) | [캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST) |

## 사용자 지정 개체

REST 설명서:

- [사용자 지정 개체](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/custom-objects)

SOAP API는 사용자 지정 개체에 대한 CRUD 작업만 지원합니다.

| SOAP 메서드 | REST 메서드 |
| --- | --- |
| [deleteCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/deletecustomobjects) | [사용자 지정 개체 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteCustomObjectsUsingPOST) |
| [getCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/getcustomobjects) | [사용자 지정 개체 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCustomObjectsUsingGET) |
| [syncCustomObjects](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/soap/custom-objects/synccustomobjects) | [사용자 지정 개체 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncCustomObjectsUsingPOST) [사용자 지정 개체 일괄 가져오기](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-import/bulk-custom-object-import) |
