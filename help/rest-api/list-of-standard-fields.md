---
title: 표준 필드
feature: REST API, Field Management
description: REST 및 SOAP 이름, 레이블 및 설명이 포함된 Marketo 표준 리드 필드의 전체 목록과 Describe Lead API를 통해 검색하는 방법을 찾아봅니다.
exl-id: 147dbdff-4bc9-4ab3-8918-c4de3e1aa97a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 11%

---

# 표준 필드

다음은 API를 통해 액세스할 수 있는 Marketo에서 사용할 수 있는 표준 필드 목록입니다.

REST [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/) 끝점을 사용하여 리드 레코드에서 사용할 수 있는 지원되는 모든 필드 이름 목록을 검색할 수 있습니다.

| REST API 이름 | SOAP API 이름 | 알기 쉬운 레이블 | 설명 |
| --- | --- | --- | --- |
| 주소 | 주소 | 주소 | 잠재 고객 주소 |
| annualRevenue | AnnualRevenue | 연간 수익 | 잠재 고객 회사의 연간 수익 |
| anonymousIP | AnonymousIP | 익명 IP | 잠재 고객의 최초 기록된 웹 방문 IP 주소 |
| billingCity | BillingCity | 청구지 시 | 잠재 고객 청구 주소 도시 |
| billingCountry | BillingCountry | 청구지 국가 | 잠재 고객 청구 주소 국가 |
| billingPostalCode | BillingPostalCode | 청구지 우편번호 | 잠재 고객 청구 주소의 우편 번호 |
| billingState | BillingState | 청구지 주 | 잠재 고객 청구 주소 시/도 |
| billingStreet | 청구지 | 청구지 주소 | 잠재 고객 회사의 청구지 주소 |
| 도시 | 구/군/시 | 구/군/시 | 리드의 도시 |
| 회사 | 회사 | 회사 이름 | 잠재 고객의 회사 이름 |
| 국가 | 국가 | 국가 | 잠재 고객 국가 |
| dateOfBirth | 생일 | 생년월일 | 잠재 고객 생년월일 |
| 부서 | 부서 | 부서 | 회사 내 잠재 고객 부서 |
| doNotCall | DoNotCall | 두 낫 콜 | 잠재 고객의 비호출 환경 설정 |
| doNotCallReason | DoNotCallReason | 두 낫 콜 이유 | 잠재 고객의 무-콜 환경 설정에 대한 설명 |
| 이메일 | 이메일 | 이메일 주소 | 잠재 고객의 이메일 주소입니다. 잠재 고객 레코드를 위한 표준 Marketo 키 필드 |
| 팩스 | 팩스 | 팩스 번호 | 잠재 고객의 팩스 번호 |
| 이름 | 이름 | 이름 | 잠재 고객의 이름 |
| 산업 | 업종 | 업종 | 잠재 고객의 업계 |
| investCompany | 회사 유추 | 추론된 회사 | 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 회사 이름을 추정함 |
| investCountry | InferredCountry | 추론된 국가 | 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 국가 유추 |
| 성 | 성 | 성 | 잠재 고객의 성 |
| 리드 역할 | 잠재 고객 역할 | 역할 | 회사에서 잠재 고객의 역할 |
| 잠재 고객 스코어 | 잠재 고객 스코어 | 잠재 고객 점수 | 캠페인 및 프로그램을 채점하여 잠재 고객에게 부여되는 정수 점수 |
| 리드 소스 | 리드 소스 | 잠재 고객 소스 | 잠재 고객의 원본 소스를 기록하는 필드 |
| 잠재 고객 상태 | 잠재 고객 상태 | 잠재 고객 상태 | 잠재 고객의 현재 마케팅/판매 상태를 기록하는 필드 |
| mainPhone | MainPhone | 주요 전화 | 잠재 고객 회사의 기본 전화번호 |
| jigsawContactId | Marketo Jigsaw 연락처 Id | MARKETO Data.com ID | 잠재 고객의 Data.com ID(사용 가능한 경우) |
| jigsawContactStatus | Marketo Jigsaw 연락처 상태 | Marketo Data.com 상태 | 잠재 고객의 Data.com 상태(사용 가능한 경우) |
| facebookDisplayName | MarketoSocialFacebookDisplayName | Marketo 소셜 Facebook 표시 이름 | 잠재 고객의 Facebook 표시 이름입니다. Social 로그인 중 시스템 채워짐 |
| facebookId | MarketoSocialFacebookId | Marketo Social Facebook Id | 잠재 고객의 Facebook Id입니다. Social 로그인 중 시스템 채워짐 |
| facebookPhotoURL | MarketoSocialFacebookPhotourl | Marketo Social Facebook 사진 URL | 잠재 고객의 Facebook 프로필 사진 URL. Social 로그인 중 시스템 채워짐 |
| facebookProfileURL | MarketoSocialFacebookProfileURL | Marketo Social Facebook 프로필 URL | 잠재 고객의 Facebook 프로필 URL. Social 로그인 중 시스템 채워짐 |
| facebookReach | MarketoSocialFacebookReach | Marketo Social Facebook 연결 | 잠재 고객의 Facebook 도달. Social 로그인 중 시스템 채워짐 |
| facebookReferred등록 | MarketoSocialFacebookReferredEnrollments | Marketo Social Facebook 참조 등록 | Facebook을 통한 잠재 고객에 귀속되는 참조 등록 수입니다. 시스템 관리됨 |
| facebook 참조 방문 횟수 | MarketoSocialFacebookReferredVisits | Marketo Social Facebook 참조 방문 | Facebook을 통한 리드에 귀속되는 참조된 방문 수입니다. 시스템 관리됨 |
| 성별 | MarketoSocialGender | Marketo 소셜 젠더 | 잠재 고객의 성별. Social 로그인 중 시스템 채워짐 |
| lastReferencement | MarketoSocialLastReferredEnrollment | Marketo Social 마지막 참조 등록 | 마지막으로 완료된 참조 날짜. 시스템 관리됨 |
| lastReferredVisit | MarketoSocialLastReferredVisit | Marketo Social 마지막 참조 방문 | 마지막으로 참조된 방문일. 시스템 관리됨 |
| linkedInDisplayName | MarketoSocialLinkedInDisplayName | Marketo Social LinkedIn 표시 이름 | 잠재 고객의 LinkedIn 표시 이름입니다. Social 로그인 중 시스템 채워짐 |
| linkedInId | MarketoSocialLinkedInId | Marketo Social LinkedIn Id | 잠재 고객의 LinkedIn Id. Social 로그인 중 시스템 채워짐 |
| linkedInPhotourl | MarketoSocialLinkedInPhotourl | Marketo Social LinkedIn 사진 URL | 리드의 LinkedIn 사진 URL. Social 로그인 중 시스템 채워짐 |
| linkedInProfileURL | MarketoSocialLinkedInProfileURL | Marketo Social LinkedIn 프로필 URL | 잠재 고객의 LinkedIn 프로필입니다. Social 로그인 중 시스템 채워짐 |
| linkedInReach | MarketoSocialLinkedInReach | Marketo Social LinkedIn Reach | 잠재 고객의 LinkedIn 도달 범위. Social 로그인 중 시스템 채워짐 |
| linkedInReferredEnrollments | MarketoSocialLinkedInReferredEnrollments | Marketo Social LinkedIn 참조 등록 | LinkedIn을 통해 잠재 고객에 귀속되는 참조 등록 수입니다. 시스템 관리됨 |
| linkedInReferredVisits | MarketoSocialLinkedInReferredVisits | Marketo Social LinkedIn 참조 방문 | LinkedIn을 통한 리드에 속하는 참조된 방문 수입니다. 시스템 관리됨 |
| 신디케이션 Id |  - | Marketo Social 신디케이션 ID | 잠재 고객의 내부 Marketo Social ID입니다. 시스템 관리됨 |
| totalReferred등록 | MarketoSocialTotalReferredEnrollments | Marketo Social 총 참조된 등록자 수 | 잠재 고객에 귀속된 완료된 참조 등록의 총 수 |
| totalReferredVisits | MarketoSocialTotalReferredVisits | Marketo Social 총 참조된 방문 수 | 잠재 고객에 귀속되는 총 참조 방문 수 |
| twitterDisplayName | MarketoSocialTwitterDisplayName | Marketo 소셜 Twitter 표시 이름 | 잠재 고객의 Twitter 표시 이름입니다. Social 로그인 중 시스템 채워짐 |
| twitterId | MarketoSocialTwitterId | Marketo 소셜 Twitter Id | 잠재 고객의 Twitter Id. Social 로그인 중 시스템 채워짐 |
| twitterPhotourl | MarketoSocialTwitterPhotourl | Marketo 소셜 Twitter 사진 URL | 리드의 Twitter 사진 URL. Social 로그인 중 시스템 채워짐 |
| twitterProfileURL | MarketoSocialTwitterProfileURL | Marketo 소셜 Twitter 프로필 URL | 잠재 고객의 Twitter 프로필 URL. Social 로그인 중 시스템 채워짐 |
| twitterReach | MarketoSocialTwitterReach | Marketo 소셜 Twitter 범위 | 리드의 Twitter 범위. Social 로그인 중 시스템 채워짐 |
| twitterReferred등록 | MarketoSocialTwitterReferred등록 | Marketo Social Twitter 참조 등록 | Twitter를 통한 잠재 고객에 귀속되는 참조 등록 수입니다. 시스템 관리됨 |
| twitter 참조 방문 | MarketoSocialTwitterReferredVisits | Marketo Social Twitter 참조 방문 | Twitter를 통한 잠재 고객 방문 횟수입니다. 시스템 관리됨 |
| 가운데 이름 | 가운데 이름 | 중간 이름 | 잠재 고객의 가운데 이름 |
| mobilePhone | 휴대폰 | 휴대폰 번호 | 잠재 고객의 휴대폰 번호 |
| numberOfEmployees | 직원 수 | 직원 수 | 잠재 고객 회사의 직원 수 |
| 전화 | 전화 | 전화번호 | 잠재 고객 전화번호 |
| 우편번호 | 우편번호 | 우편번호 | 잠재 고객의 우편 번호 |
| 등급 | 등급 | 잠재 고객 등급 | 잠재 고객의 마케팅/판매 등급 |
| 인사말 | 인사말 | 인사말 | 리드가 선호하는 인사말, 즉 미스터, 미스... 등. |
| sicCode | SICCode | SIC 코드 | 잠재 고객 회사의 표준 산업 분류 코드 |
| 사이트 | 위치 | 위치 |  |
| state | 주/도 | 주/도 | 잠재 고객 상태 |
| 제목 | 제목 | 직위 | 잠재 고객의 직책 |
| 구독 취소됨 | 구독 취소 | 구독 취소 | 잠재 고객의 이메일 구독 취소 상태. 부분적으로 시스템이 관리됩니다. true로 설정하면 운영되지 않는 이메일이 수신되지 않습니다. |
| unsubscribedReason | 가입 해지됨 이유 | 구독 취소 이유 | 잠재 고객의 구독 취소 상태에 대한 사유. 부분적으로 시스템이 관리됩니다. 잠재 고객이 Marketo 이메일에서 직접 가입 해지된 경우 이메일 정보로 채워집니다. |
| 웹 사이트 | 웹 사이트 | 웹 사이트 | 잠재 고객 회사 웹 사이트 URL |
| createdAt |  - | 생성 위치 | 잠재 고객 레코드가 처음 생성된 시간입니다. 시스템 관리됨 |
| updatedAt |  - | 업데이트 시간 | 잠재 고객 레코드가 마지막으로 업데이트된 시간입니다. 시스템 관리됨 |
| emailInvalid |  - | 잘못된 이메일 | 이메일 상태가 잘못되었습니다. true로 설정하면 해당 주소의 모든 이메일이 차단됩니다. 이메일이 유효하지 않음을 나타내는 바운스 수는 이 필드를 자동으로 true로 설정합니다. |
| emailInvalidCause |  - | 잘못된 이메일 원인 | 이메일 상태가 잘못되었기 때문입니다. 잘못된 전자 메일이 true로 설정되면 이 필드에 주입 바운스 메시지가 기록됩니다. |
| investCity |  - | 추론된 시 | 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 잠재 고객의 도시를 추정함. |
| investMetropolitanArea |  - | 대도시 지역 유추 | 잠재 고객의 대도시 지역을 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 추정함. |
| investPhoneAreaCode |  - | 전화번호 지역코드 유추 | 잠재 고객의 전화 지역 코드가 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 추론됩니다. |
| 유추우편번호 |  - | 추론된 우편번호 | 잠재 고객의 우편 번호를 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 추정함. |
| investStateRegion |  - | 유추된 주 지역 | 잠재 고객의 최초 기록된 웹 방문 역 IP 조회로 잠재 고객의 상태 지역을 추정함. |
| isAnonymous |  - | 익명 | 잠재 고객 레코드의 익명 상태. 시스템 관리됨. |
| 우선 순위 |  - | 우선순위 | 잠재 고객의 영업 Insight 우선 순위. 시스템 관리됨. |
| relativeScore |  - | 상대 스코어 | 잠재 고객의 판매 Insight 상대 점수. 시스템 관리됨. |
| 긴급도 |  - | 긴급도 | 잠재 고객의 영업 Insight 긴급도. 시스템 관리됨. |
