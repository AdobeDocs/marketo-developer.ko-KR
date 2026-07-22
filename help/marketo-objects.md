---
title: Marketo 개체
feature: Email Programs
description: 리드, 기회 및 사용자 지정 개체와 함께 Marketo Velocity 사용, 필드 로드, 상위 10개 목록 액세스, SFDC 관계 및 $TriggerObject에 대해 안내합니다.
exl-id: 88c63d72-7aa5-4550-9e1a-887a479872e1
TQID: https://experienceleague.adobe.com/PvLJb-AOk6DKaNINycpzk5ojZiL8UNcanRg3vXmsGCI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 0%

---

# Marketo 개체

Marketo의 Velocity 구현은 다음 Marketo 소스의 데이터를 사용할 수 있습니다.

- 잠재 고객
- 기회
- 사용자 정의 오브젝트
- 모바일 앱
- 모바일 앱 설치

## 필드 로드 중

스크립트에서 필드를 사용하려면 스크립트 토큰 편집기의 해당 목록 아래에서 필드를 선택합니다.

스크립트가 로드되지 않은 필드를 참조하는 경우 런타임 시 스크립트가 실패합니다. 필드 메뉴에서 스크립트로 필드를 끌어 놓아 로드하고 커서에 참조를 추가합니다.

## 영업 기회 및 사용자 지정 개체 목록

Opportunities 및 Custom Objects의 경우 Marketo은 각 유형에서 가장 최근에 업데이트된 10개의 객체만 로드합니다. 여기에 설명된 단계에 따라 사용 가능한 사용자 지정 개체의 수를 늘릴 수 있습니다.

Marketo은 가장 최근에 업데이트된 레코드에서 가장 최근에 업데이트된 레코드로 정렬된 `<objectName>List` 목록의 개체를 제공합니다. 가장 최근에 업데이트된 기회에서 금액 필드에 액세스하려면 다음을 사용합니다.

`${OpportunityList.get(0).Amount}`

이 예제에서는 OpportunityList 개체를 참조하고 get 메서드를 사용하여 인덱스 0에 있는 레코드에 액세스한 다음 해당 레코드에서 Amount 속성을 검색합니다.

Opportunity 또는 Custom Object 필드를 편집기로 드래그하면 인덱스 0의 레코드에서 필드가 자동으로 Marketo에 검색됩니다.

## SFDC 사용자 지정 개체 관계

SFDC 사용자 지정 개체를 사용하려면 개체에 Marketo 리드에 대한 관계가 하나만 있어야 합니다. 오브젝트는 종종 연락처와 계정을 통해 연결됩니다. 리드/연락처 관계가 활성화된 개체만 동기화합니다.

## 트리거 개체

캠페인에서 Added to Opportunity, Opportunity가 업데이트되거나 `<Custom Object Name>` 트리거에 추가되면 트리거 캠페인에서 실행되는 스크립트 토큰에 `$TriggerObject` 변수를 사용할 수 있습니다. `<Custom Object Name>`이(가) 업데이트된 트리거에는 이 변수가 지원되지 않습니다.

이 변수는 캠페인을 트리거한 개체를 참조합니다. 다른 변수 이름을 통해 개체에 액세스할 때 사용할 수 있는 것과 동일한 레코드 데이터가 포함되어 있습니다.

일괄 처리 캠페인에서 `$TriggerObject`을(를) 참조하는 토큰을 사용하지 마십시오. 배치 캠페인에서는 개체를 사용할 수 없으며 이메일 전송이 실패합니다.

예를 들어 제품 주문에 대한 사용자 지정 개체에서 캠페인을 트리거하면 `$TriggerObject` 변수가 리드가 추가된 순서를 표시합니다.

다음 예제는 주문 후속 이메일에 대한 스크립트를 보여 줍니다.

```html
<div>
<strong>Your order information:</strong>
##pull information from the Triggering Order and format it in a list
<ul>
<li>Product Ordered: $!{TriggerObject.ProductName}</li>
<li>Product Quantity: $!{TriggerObject.Quanitity}</li>
<li>Shipping Address: $!{TriggerObject.ShippingAddress}</li>
<li>Billing Address: $!{TriggerObject.BillingAddress}</li>
<li>Order Total: $!{TriggerObject.Amount}</li>
</ul>
<p><a href="$!{TriggerObject.OrderURL}">View Your Order Online</a></p>
</div>
```

트리거 작업은 개체를 결정합니다. 로컬 데이터가 포함된 사용 가능한 개체를 결정하는 데 추가 코드가 필요하지 않습니다. 참조할 개체를 명시적으로 식별하므로 사용 가능하고 적절한 경우 `$TriggerObject`을(를) 사용합니다.

참고: `$TriggerObject`을(를) 사용하는 경우 편집 창에서 개체의 필드를 선택하여 스크립트에서 사용할 수 있도록 하십시오.

참고 2: `$TriggerObject`은(는) &quot;업데이트된&quot; 트리거가 아닌 &quot;추가된&quot; 트리거에만 작동합니다.
