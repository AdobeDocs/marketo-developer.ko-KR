---
title: 활동
feature: SOAP
description: getLeadActivities 및 getLeadChanges를 사용하여 SOAP을 사용하여 활동과 상호 작용하고 리드 활동을 검색하고 리드 변경을 추적하는 방법에 대해 알아봅니다
exl-id: fd695ab6-e7be-4ced-89c9-c4cd2d4c2ab0
TQID: https://experienceleague.adobe.com/6zUkvoDCqlRmblFDPWzLjdwITsyWxcXrJBKbLux76WI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: e71bcf289229867bc969345d79c8f014761aaaf9
workflow-type: tm+mt
source-wordcount: 79
ht-degree: 2%

---

# 활동

다음 SOAP 호출을 사용하여 활동과 상호 작용할 수 있습니다.

- [getLeadActivities](getleadactivity.md)
- [getLeadChanges](getleadchanges.md)

>[!CAUTION]
>
>2026-12-30부터 대상 목록에 10,000개 이상의 리드가 포함된 경우 `listId` 매개 변수를 포함하는 `Get Lead Activities` 및 `Get Lead Changes` 끝점에 대한 호출이 실패합니다(오류 코드 1003). 서비스 중단을 방지하려면 이 제한을 피하기 위해 호출 범위가 제대로 지정되었는지 확인하십시오. [마이그레이션 안내서](migration.md)를 참조하세요.
