---
title: SOAP FAQ
feature: SOAP
description: SOAP FAQ
exl-id: a2d8f144-cd5f-41bc-8231-29c42af935b8
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# SOAP FAQ

**Q:** Marketo 내의 모든 프로그램 목록과 해당 메타데이터를 가져오려면 어떻게 해야 합니까?

**A:** 모든 프로그램 목록을 검색하려면 [getMObjects](./getmobjects.md)을(를) 사용하여 &quot;Program&quot;과 같은 형식을 전달하고 includeDetails를 true로 설정합니다.

**Q:** getMultipleLeads의 성능을 빠르게 할 수 있는 방법이 있습니까?

**A:** getMultipleLeads 호출의 성능을 빠르게 하기 위한 몇 가지 옵션이 있습니다. 첫 번째는 각 호출에 대해 요청하는 batchSize를 줄이는 것입니다. 200이 권장되는 배치 크기입니다. 두 번째 옵션은 includeAttributes 필터를 사용하여 원하는 필드를 지정하는 것입니다. 이렇게 하면 쿼리 속도가 빨라지고 수신하는 응답의 페이로드가 줄어듭니다. 마지막 접근 방법은 LastUpdateAtSelector를 사용하고 oldestUpdatedAt 및 latestUpdatedAt를 지정하는 것입니다. 서로 다른 날짜 범위를 지정한 다음 여러 요청을 동시에 스레드할 수 있습니다. 스레드 접근 방식을 사용하는 경우 SOAP/WSDL 클라이언트가 [영구 연결](https://www.w3.org/Protocols/rfc2616/rfc2616-sec8.html)을 지원하는지 확인하십시오.

**Q:** SalesForce 또는 Microsoft Dynamics와 같은 CRM과 통합되지 않은 경우 SOAP API를 통해 기회를 만들려면 어떻게 해야 합니까?

**A:** OpportunityPersonRole 및 Opportunity [MObject](marketo-objects.md) 유형에 쓰는 [syncMObjects](syncmobjects.md) 호출을 사용하여 SOAP API를 사용하여 기회를 만들 수 있습니다.

**Q:** Marketo에서 이메일을 프로그래밍 방식으로 보낼 수 있습니까? 그렇다면 각 이메일 수신자에 대한 사용자 지정 콘텐츠를 보내려면 어떻게 해야 합니까?

**A:**&#x200B;입니다. [requestCampaign](requestcampaign.md) 또는 [importToList](importtolist.md)와 [scheduleCampaign](schedulecampaign.md) SOAP API의 조합을 사용하여 Marketo에서 보낼 전자 메일을 요청할 수 있습니다. 한 명 이상의 사용자에게 전자 메일을 즉시 보내려면 [requestCampaign](requestcampaign.md)을(를) 사용합니다. 지정된 날짜와 시간에 전자 메일을 전송하도록 예약하려면 [importToList](importtolist.md)를 사용하여 전자 메일 받는 사람을 지정하고 [scheduleCampaign](schedulecampaign.md)을(를) 사용하여 받는 사람에게 전자 메일을 보낼 시기를 지정합니다.

각 전자 메일 받는 사람에 대한 콘텐츠를 사용자 지정하려면 전자 메일 서식 파일 내에 설정된 [프로그램 토큰](../rest-api/tokens.md)의 값을 재정의하면 됩니다.
