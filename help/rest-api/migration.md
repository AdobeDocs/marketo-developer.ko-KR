---
title: 리드 API 업데이트 가져오기
feature: REST API
description: 리드 가져오기 활동 및 리드 변경 사항 엔드포인트 제한에 대한 변경 사항을 알아봅니다.
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 리드 API 업데이트 가져오기

2026년 9월 30일부터 대상 목록에 10,000개 이상의 잠재 고객이 포함된 경우 `listId` 매개 변수를 포함하는 [잠재 고객 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadActivitiesUsingGET) 또는 [잠재 고객 변경 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadChangesUsingGET) 엔드포인트에 대한 호출이 실패합니다. 끝점은 대상 정적 목록에 레코드가 너무 많음을 나타내는 1003 오류 코드를 반환합니다.

하나 이상의 최근 API 호출이 이 변경의 영향을 받습니다. 서비스 중단을 방지하려면 2026년 9월 30일까지 애플리케이션이 Marketo과 통합하는 방법을 업데이트해야 할 수 있습니다.

이러한 쿼리는 종종 잠재적 결과가 없는 검색을 만들거나 결과를 찾기 전에 시간을 초과합니다. 설정된 크기를 제한하면 쿼리 응답성이 향상되고 검색이 적시에 완료됩니다.

## 영향을 받았는지 어떻게 알 수 있습니까?

이 변경 사항은 적은 수의 Marketo Engage 인스턴스에만 영향을 줍니다. 영향을 받는 구독의 관리자는 변경 사항이 적용되기 전에 적용 내 알림을 받게 됩니다.

## 어떻게 해야 합니까?

Marketo Engage 통합을 담당하는 사람 또는 팀과 이 문서를 공유합니다.

사용 사례에 따라 다음 마이그레이션 옵션 중 하나를 사용합니다.

* 활동 추출에 사용되는 정적 목록을 10,000명의 멤버로 제한합니다. 기존 목록을 더 작은 목록으로 분할하여 동일한 대상을 활동에 대해 계속 폴링합니다.
* 일괄 활동 추출 또는 데이터 스트림을 사용하여 활동 또는 데이터 값 변경 사항을 추출합니다. [getLeadByListId](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadsByListIdUsingGET_1) 또는 [잠재 고객 대량 추출](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/rest/bulk-extract/bulk-lead-extract)을 사용하여 정적 목록 멤버십에 결과를 참여하십시오.

## 내가 아무것도 안 하면 어떻게 될까?

많은 수의 멤버가 있는 정적 목록에서 활동을 쿼리할 때 처리되지 않은 오류로 인해 API 통합이 중단될 수 있습니다.
