---
title: 데이터 스트림
description: 데이터 스트림 개요
exl-id: 5617b6a5-ebc8-4d97-a290-e3b87f83e360
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 1%

---

# 데이터 스트림

>[!NOTE]
> 이제 데이터 스트림에 대한 현재 정보를 [데이터 스트림 사용](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-data-streams/)에서 찾을 수 있습니다.
>

Dell 고객의 마케팅 조직은 적시에 집중하는 마케팅 캠페인에 의존하여 비즈니스를 주도하고 경쟁력을 확보합니다. 신속한 의사 결정을 지원하고 전략적으로 신속하게 변경하려면 집중되고 타깃팅된 캠페인을 제공하는 주요 의사 결정을 지원하고 유도할 데이터를 확보하는 것이 중요합니다. 또한 Marketo Engage 내부와 외부 모두에서 고객 세그먼트 수준에서 마케팅 활동을 수행하는 고객이 있습니다. 이러한 다양한 작업을 지원하기 위해 Marketo은 데이터 스트림을 통해 거의 실시간으로 대량의 데이터를 획득하는 기능을 개발했습니다.

실시간에 가까운 데이터의 이점 이외에도 제품과 관련된 다음과 같은 이점이 있습니다.

- 스트리밍이 대신 사용되므로 API 제한의 병목 현상을 완화합니다.
- API 제한 시나리오를 줄여 경고 메시지를 덜 생성합니다.
- 데이터 스트리밍 기능으로 인해 데이터를 추출하기 위해 대량 내보내기를 수행할 필요는 없습니다.

데이터 스트림은 [Marketo Engage 성능 계층 패키지](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835)를 구입한 사용자가 사용할 수 있습니다.

## 잠재 고객 활동 데이터 스트림 개요

리드 활동 데이터 스트림은 대량의 리드 활동을 고객의 외부 시스템으로 보낼 수 있는 감사 추적 리드 활동을 거의 실시간으로 스트리밍합니다. Streams를 사용하면 고객이 Lead 관련 이벤트, 사용 패턴을 효과적으로 감사하고, Lead 변경 사항을 조회하고, 다양한 유형의 Lead 이벤트를 기반으로 프로세스 및 워크플로우를 트리거할 수 있습니다. 구독할 수 있고 스트림을 통해 전송할 수 있는 활동 유형은 144개가 넘습니다.

스트리밍되는 잠재 고객 데이터 유형:

1. 잠재 고객 변경 - 모든 필드의 모든 변경 사항 및 새 잠재 고객
1. 가망 고객 활동 - 문서에 설명된 모든 가망 고객 활동 유형
1. 삭제된 리드
1. 잠재 고객의 모든 사용자 지정 개체(필요한 경우). 지금은 전부 아니면 아무것도 아니다.

리드 변경 사항에 대한 보기를 제공함으로써 고객은 전반적인 마케팅 전략에 대해 더 빠른 결정을 내리고 더 집중적인 타겟팅 캠페인을 만들 수 있습니다. 다음은 일반적인 사용 사례입니다.

- 사용자 지정 경고: 특정 잠재 고객이 일관되지 않은 상태로 발견되면 목록에 추가할 수 있습니다. 활동 스트림은 이러한 항목을 선택하여 고객의 &quot;목록에 추가&quot; 활동을 모든 후속 작업에 푸시할 수 있습니다.
- ML 모델 강화: 일부 고객은 활동 인사이트를 사용하는 채점 모델을 빌드하고 이를 Marketo에 다시 제공하거나 원하는 대로 자체 내부 채점 모델에서 사용할 계획입니다. 그런 다음 고객은 잠재 고객을 점수화하여 Marketo에 고객을 육성 캠페인에 추가하여 점수를 높일 수 있습니다.

스트리밍된 활동 목록:

| ObjectiveInReferral | ClickPredictiveContent | ReceivedForwardToFriendEmail |
|--- |--- |--- |
| 목록 추가 | ClickRTPCallToAction | ReceiveSalesEmail |
| AddToGrooth | ClickSalesEmail | ReferToSocialApp |
| AddToOpportunity | ClickSharedLink | RemoveFromList |
| AddToSalesCampaign | 잠재 고객 전환 | RemoveFromOpportunity |
| CallWebhook | DeleteLead | 요청 캠페인 |
| ChangeDataValue | DisqualificationSweepstakes | SalesEmailBounded |
| ChangeLeadPartition | EarnEntryInSocialApp | SendAlert |
| ChangeGroothCadence | 반송된 이메일 | SendEmail |
| ChangeGroothTrack | EmailBoundedSoft | SendSalesEmail |
| 소유자 변경 | EmailDelivered | SentForwardToFriendEmail |
| 프로그램 데이터 변경 | EnrichWithDataDotCom | SFDCAactivity |
| ChangeProgramMemberData | 경품 추첨 | ShareContent |
| 변경 수익 단계 | FillOutFacebookLeadAdsForm | SignUpForReferralOffer |
| ChangeRevenueStageManually | 양식 채우기 | SyncLeadToMicrosoft |
| 점수 변경 | InterestMoment | SyncLeadToSFDC |
| 세그먼트 변경 | 잠재 고객 병합 | 이메일 구독 취소 |
| 진행 상태 변경 | NewLead | UpdateOpportunity |
| ChangeStatusInSalesCampaign | OpenEmail | 웹 페이지 방문 |
| ClickEmail | OpenSalesEmail | 투표 인폴 |
| ClickLink | PushLeadToMarketo | WinSweepstakes |

사용자 정의 객체를 스트리밍해야 하는 경우 모든 Lead 관련 사용자 정의 객체여야 합니다. 현재 시점에서는 어떤 것을 원하는지 선택할 방법이 없다.

## 사용자 감사 데이터 스트림 개요

사용자 감사 데이터 스트림은 사용자의 자산 변경 사항에 대한 거의 실시간 감사 추적을 제공합니다&#x200B;. 이를 통해 고객은 에셋 이벤트를 효과적으로 감사하고, 사용자 변경 사항을 확인하고, 다양한 유형의 감사 이벤트를 기반으로 프로세스 또는 워크플로우를 트리거할 수 있습니다. 거의 실시간 자산 변경 사항은 Adobe I/O 이벤트를 통해 구성 가능한 엔드포인트로 전송됩니다. 감사 이벤트는 자산 유형별로 분류되며 중요한 감사 이벤트에 가입할 수 있습니다.

이 스트림을 구독하는 데 좋은 사용 사례는 다음과 같습니다.

- 여러 마케팅 시스템 사용 시 변경 사항 추적: Salesforce과 같은 CRM과 같은 다른 시스템에서 일부 수준의 마케팅 활동을 수행한 다음 잠재 고객을 Marketo으로 전달하는 고객이 있습니다. 잠재 고객이 때때로 업데이트되고 동기화되므로 최근 변경한 시스템을 추적하는 것이 중요합니다.

스트리밍된 사용자 감사 이벤트 목록:

| 구성 요소 | 이벤트 유형 목록 |
|--- |--- |
| 기본 프로그램 | 복제, 생성, 삭제, 채널 편집, 내보내기, 프로그램 설정 수정, 프로그램 토큰 수정, 이름 바꾸기 |
| 이메일 | 승인, 복제, 생성, 삭제, 편집, 이동, 이름 변경, 승인 취소 |
| 이메일 일괄 처리 프로그램 | 승인, 하위 업데이트, 복제, 만들기, 삭제, 편집, 채널 편집, 프로그램 일정 수정, 프로그램 설정 수정, 프로그램 토큰 수정, 이름 바꾸기, 승인 취소 |
| 이메일 템플릿 | 승인, 복제, 생성, 삭제, 초안생성, 초안삭제, 편집, 이름 바꾸기, 승인 취소 |
| 참여 프로그램 | 복제, 생성, 삭제, 채널 편집, 프로그램 설정 수정, 프로그램 스트림 수정, 프로그램 토큰 수정, 이름 바꾸기 |
| 이벤트 프로그램 | 복제, 생성, 삭제, 채널 편집, 프로그램 일정 수정, 프로그램 설정 수정, 프로그램 토큰 수정, 이름 바꾸기 |
| 폴더 | 만들기, 삭제, 편집, 이름 바꾸기 |
| 양식 | 승인, 복제, 생성, 삭제, 초안생성, 편집, 이동, 이름 바꾸기 |
| 양식 -> 랜딩 페이지 양식 | 생성, 복제, 편집, 삭제, 승인, 이름 변경 |
| 랜딩 페이지 | 승인, 복제, 생성, 삭제, 초안Discard, 편집, 이름 바꾸기, 승인 취소 |
| 랜딩 페이지 템플릿 | 승인, 복제, 생성, 삭제, 초안생성, 초안삭제, 편집, 이름 바꾸기, 승인 취소 |
| 스마트 목록 | 복제, 생성, 삭제, 편집, 내보내기, 스마트 목록 설정 수정, 이름 바꾸기 |
| 마케팅 폴더 | 만들기, 편집, 삭제 |
| 육성 프로그램 | 복제, 생성, 삭제, 채널 편집, 프로그램 설정 수정, 프로그램 스트림 수정, 프로그램 토큰 수정, 이름 바꾸기 |
| 세그먼트 | 만들기, 삭제, 편집, 이름 바꾸기 |
| 세분화 | 승인, 만들기, 삭제, 초안 작성, 초안 삭제됨, 이름 바꾸기, 승인 취소 |
| 스마트 캠페인 | 중단, 활성화, 복제, 생성, 비활성화, 삭제, 편집, 캠페인 일정 수정, 흐름 단계 작업 수정, 스마트 목록 설정 수정, 이동, 이름 바꾸기 |
| 코드 조각 | 승인, 초안이 없는 승인, 복제, 생성, 삭제, 편집, 이름 변경, 승인 취소 |
| 관리자 UI -> Launchpoint -> 통합 | 만들기, 삭제, 편집 |
| 관리자 UI -> 사용자 | 만들기, 편집, 삭제(API 전용 사용자와 동일) |
| 관리자 로그인 -> 사용자 | 로그인 성공, 로그인 실패 |
| 프로그램 -> 이메일 일괄 처리 프로그램 | 자산 API 편집(선택한 이메일 주소 변경용) |
| 프로그램 -> 마케팅 프로그램 | 생성, 복제 |

사용자 감사 이벤트의 예:

```json
{
    "event_id": "a1b2c3d4-zyxw-9876-9z8y-a1b2c3d4e5f6",
    "event": {
        "specversion": "1.0",
        "id": "b77c743a-8e28-40f2-8aab-9541bbc85e68",
        "type": "com.adobe.platform.marketo.audit.user.email",
        "source": "https://www.marketo.com",
        "time": "2020-05-28T19:20:47.28Z",
        "datacontenttype": "application/json",
        "dataschema": "V1.0",
        "data": {
            "componentId": 232459,
            "componentType": "Email",
            "eventAction": "approve",
            "munchkinId": "123-ABC-456",
            "imsOrgId": "ADOBEORGID@AdobeOrg",
            "user": 253,
            "userId": "example@marketo.com"
        }
    }
}
```

## 알림 데이터 스트림 개요

알림 데이터 스트림은 Marketo Engage의 성능 수준 서비스의 일부로 사용할 수 있습니다.

현재 Marketo의 알림 센터는 이메일 주소로 알림을 보내도록 구성할 수 있습니다. 알림 데이터 스트림을 사용하면 Adobe I/O 이벤트를 통해 구성 가능한 엔드포인트로 알림을 직접 전송할 수 있습니다. 알림은 오늘 UI를 통해 제공되며 화면 오른쪽 상단의 주황색 벨에서 참조할 수 있습니다. 이 스트림은 이러한 알림을 가져와 스트림을 통해 전송합니다.

알림 이벤트 목록:

| 구성 요소 | 이벤트 유형 목록 |
|--- |--- |
| 알림 | 캠페인 중단, 캠페인 실패, 육성(프로그램 소진), salesforce 동기화 실패, 테스트 그룹(A/B 테스트 결과), 웹 서비스(일일 할당량) |

알림 이벤트의 예:

```json
{
    "event_id": "a1b2c3d4-zyxw-9876-9z8y-a1b2c3d4e5f6",
    "event": {
        "specversion": "1.0",
        "type": "com.adobe.platform.marketo.notification.campaign_abort",
        "source": "https://www.marketo.com",
        "time": "2021-05-27T10:22:37.489-5:00",
        "datacontenttype": "application/json",
        "dataschema": "V1.0",
        "data": {
            "componentType": "campaign_abort",
            "subType": "user_campaign_abort",
            "eventAction": {
                "campaignId":1234,
                "userId":"example@marketo.com",
            }
            "imsOrgId":"ADOBEORGID@AdobeOrg",
            "munchkinId":"123-ABC-456"
        }
    }
}
```

## 기술 세부 정보

이 섹션에서는 필요한 항목, 각 스트림에 대한 스트리밍 데이터를 연결하고 받는 방법에 대한 지침을 제공합니다. 각각에 대해 일정 수준의 코딩 및 설정이 포함됩니다.

### 잠재 고객 활동 데이터 스트림

잠재 고객 활동 스트림은 Marketo 잠재 고객 활동 이벤트의 거의 실시간 스트리밍을 제공하고 구성 가능한 속성으로 구독한 활동 유형 변경 사항을 보냅니다.

- 기본적으로 데이터 푸시의 빈도는 2초마다 입니다.
- 구독당 100~500개 배치.
- 고객 REST 서비스의 시간 제한은 3분마다 3회 다시 시도하여 20초이며, 성공 시 자동으로 활성화됩니다. 그렇지 않으면 이 작업 후 일시 중지됩니다. 일시 중지되면 서비스는 수동으로 프로비전을 해제하지 않는 한 다시 활성화하기 위해 3분마다 다시 시도합니다.
- 최대 7일 동안 대기열에 있는 데이터 보존.

리드 활동 데이터 스트림을 구현하려면 고객이 따라야 할 단계가 있습니다.

1. 공개 인터넷으로부터 JSON 본문이 있는 POST 요청을 수신할 수 있는 HTTP 끝점을 노출합니다. 활동 푸시 데이터 스트림 은 다음 사용자에게 요청을 보냅니다.
1. Adobe에 다음 정보를 제공합니다.
   1. 구독용 Marketo Munchkin ID
   1. 1단계에서 끝점의 URL
   1. 수신하려는 활동 유형(위의 전체 목록)
   1. 고객이 요청이 합법적인지 확인할 수 있는 인증 수단입니다. 다음 중 하나를 수행합니다.
      1. OAuth [클라이언트 자격 증명 인증](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)에 대한 ID 공급자 URL, 클라이언트 ID 및 클라이언트 암호
      1. 인증 http 헤더의 잠재 고객 활동 데이터 스트림에서 보낸 요청에 포함될 수 있는 API 토큰

그런 다음 Adobe은 데이터 스트림을 활성화하므로 고객은 이 지점에서 데이터를 받기 시작합니다.

일반적인 리드 활동 데이터 스트림 호출의 UML 다이어그램:

![리드 활동 데이터 스트림 다이어그램](assets/lead-activity-data-stream.png)

URL 끝점 생성의 예:

```javascript
/*
Copyright 2022 Adobe
All Rights Reserved.

NOTICE: Adobe permits you to use, modify, and distribute this file in
accordance with the terms of the Adobe license agreement accompanying
it.
*/
constexpress=require('express')
constwinston=require('winston');
constport=3000

constapp=express().use(express.json())

constlogger=winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: {service: 'activity-stream-consumer-example'},
  transports: [
    // - Write all logs with level `error` and below to `error.log`
    newwinston.transports.File({filename: 'error.log',level: 'error'}),
    // - Write all logs with level `info` and below to `combined.log`
    newwinston.transports.File({filename: 'combined.log'}),
    newwinston.transports.Console({format: winston.format.simple()})
  ],
});

app.get('/',(req,res)=>{
  logger.info(JSON.stringify(req.query))
  res.sendStatus(200)
})

app.post('/',(req,res)=>{
  logger.info(JSON.stringify(req.body))
  res.sendStatus(200)
})

app.listen(port,()=>{
  logger.info(`app listening on port ${port}`)
})
```

Marketo 잠재 고객 활동 데이터 스트림을 사용하는 응용 프로그램의 코드 샘플을 [여기](https://github.com/ihgrant/activity-stream-consumer-example)에서 찾을 수 있습니다.

### 사용자 감사 데이터 스트림 및 알림 데이터 스트림

사용자 감사 이벤트는 Adobe IO로 전송되며 Adobe ID으로 로그인하여 사용할 수 있습니다. 다음은 따라야 할 단계입니다.

1. 고객은 Adobe에 다음 사항을 제공합니다.
   1. Adobe ID
   1. 구독용 Marketo Munchkin ID
1. 고객은 REST 끝점을 노출하여 일반적으로 웹후크 형태로 이벤트를 소비합니다.
1. 제공되면 Adobe에서 고객의 구독에 대한 스트림을 활성화합니다.
1. 그런 다음 고객은 Adobe IO에서 스트림을 설정합니다(제공될 지침).
   1. 이 단계에는 Adobe 조직이 필요합니다
   1. Adobe 조직 사용자에게 개발자 또는 시스템 관리자 역할이 있어야 함

Adobe IO를 설정하려면 공개 설명서 섹션에서 [Adobe IO를 사용하여 Marketo 사용자 감사 데이터 스트림 설정](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-user-audit-data-stream-setup/)을 참조하십시오.

### Marketo에서 사용자 감사 데이터 스트림 설정

사용자 감사 데이터 스트림은 현재 다른 3개의 데이터 스트림과 함께 성능 패키지의 일부로 사용할 수 있습니다. 패키지에 대한 자세한 내용은 제품 제한 및 기능에 대한 [제품 설명 페이지](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-marketo-engage---product-description.html)를 참조하세요.

### Adobe I/O 설정

[Adobe I/O Events 시작](https://developer.adobe.com/runtime/docs/guides/getting-started/)

이 사용 사례에 대한 기본 지침은 [console.adobe.io](https://developer.adobe.com/console)부터 시작됩니다.

메시지가 표시되면 **[!UICONTROL Create New Project]** 또는 **[!UICONTROL Add Event]**&#x200B;을(를) 선택합니다.

### 새 프로젝트 시작

Adobe 서비스를 사용하려면 API, 이벤트 또는 런타임을 추가하려면 [설명서](https://developer.adobe.com/runtime/docs/)를 참조하세요.

## 공개 설명서

- [Marketo 데이터 스트림](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-data-streams/)
- [Adobe IO 이벤트 및 웹후크 소개](https://developer.adobe.com/events/docs/guides/)
- [데이터 스트림 블로그](https://blog.developer.adobe.com/introducing-the-adobe-marketo-engage-data-streams-61198b567fbb)
