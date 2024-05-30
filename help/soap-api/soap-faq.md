---
title: "SOAP FAQ"
feature: SOAP
description: "SOAP FAQ"
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# SOAP FAQ

**Q:** Marketo에 있는 모든 프로그램 목록과 메타데이터를 함께 가져오려면 어떻게 해야 합니까?

**A:** 모든 프로그램 목록을 검색하려면 [getMObjects](./getmobjects.md) &quot;Program&quot;과 같은 형식을 전달하고 includeDetails를 true로 설정합니다.

**Q:** getMultipleLeads의 성능을 가속화할 수 있는 방법이 있습니까?

**A:** getMultipleLeads 호출의 성능을 가속화하는 몇 가지 옵션이 있습니다. 첫 번째는 각 호출에 대해 요청하는 batchSize를 줄이는 것입니다. 200이 권장되는 배치 크기입니다. 두 번째 옵션은 includeAttributes 필터를 사용하여 원하는 필드를 지정하는 것입니다. 이렇게 하면 쿼리 속도가 빨라지고 수신하는 응답의 페이로드가 줄어듭니다. 마지막 접근 방법은 LastUpdateAtSelector를 사용하고 oldestUpdatedAt 및 latestUpdatedAt를 지정하는 것입니다. 서로 다른 날짜 범위를 지정한 다음 여러 요청을 동시에 스레드할 수 있습니다. 스레드 접근 방식을 사용하는 경우 SOAP/WSDL 클라이언트가 을 지원하는지 확인합니다. [영구 연결](https://www.w3.org/Protocols/rfc2616/rfc2616-sec8.html).

**Q:** SalesForce 또는 Microsoft Dynamics와 같은 CRM과 통합되지 않은 경우 SOAP API를 통해 기회를 만들려면 어떻게 해야 합니까?

**A:** 다음을 사용하여 SOAP API를 사용하여 Opportunity 를 만들 수 있습니다. [syncMObjects](syncmobjects.md) opportunityPersonRole 및 Opportunity에 대한 호출 쓰기 [오브젝트](marketo-objects.md) 유형.

**Q:** Marketo에서 이메일을 프로그래밍 방식으로 보낼 수 있습니까? 그렇다면 각 이메일 수신자에 대한 사용자 지정 콘텐츠를 보내려면 어떻게 해야 합니까?

**A:** 당연하지 다음 중 하나를 사용하여 Marketo에서 전송할 이메일을 요청할 수 있습니다. [request캠페인](requestcampaign.md) 또는 복합물 [가져오기 대상 목록](importtolist.md) 및 [scheduleCampaign](schedulecampaign.md) SOAP API. 한 명 이상의 사용자에게 이메일을 즉시 보내려면 [request캠페인](requestcampaign.md). 지정된 날짜 및 시간에 이메일을 전송하도록 예약하려면 다음을 사용합니다. [가져오기 대상 목록](importtolist.md) 이메일 수신자 지정 및 [scheduleCampaign](schedulecampaign.md) 받는 사람에게 해당 이메일을 보낼 시기를 지정합니다.

각 이메일 수신자에 대한 콘텐츠를 사용자 정의하려면 의 값을 재정의하여 이를 수행할 수 있습니다. [프로그램 토큰](../rest-api/tokens.md) 이메일 템플릿 내에서 설정됩니다.
