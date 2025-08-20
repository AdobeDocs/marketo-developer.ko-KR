---
title: Marketo 개체
feature: Email Programs
description: Velocity 스크립팅과 함께 Marketo 개체 사용에 대한 개요
source-git-commit: 3ccb27a0d184e0c1314979d404022bc4e0794f7b
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Marketo 개체

Marketo의 Velocity 구현은 리드, 기회, 사용자 지정 개체, 모바일 앱, 모바일 앱 설치 등 Marketo 내의 여러 소스에서 가져온 데이터에 대해 작동할 수 있습니다.

## 필드 로드 중

스크립트에서 사용할 필드를 로드하려면 스크립트 토큰 편집기의 해당 목록에서 해당 필드를 선택해야 합니다.

필드를 로드하지 않고 스크립트 내에서 참조되는 경우 런타임 시 스크립트 실행이 실패합니다. 필드 메뉴에서 스크립트로 필드를 끌어다 놓을 수 있습니다. 이렇게 하면 필드를 로드할 수 있고 커서의 필드에 참조를 추가합니다.

## 영업 기회 및 사용자 지정 개체 목록

Opportunities 또는 Custom Objects에서 를 검색하는 경우 가장 최근에 업데이트된 유형의 10개 객체만 로드됩니다. 여기에 설명된 단계에 따라 사용 가능한 사용자 정의 객체의 수를 늘릴 수 있습니다. 이 목록은 이름이 `<objectName>List`인 목록으로 제공되며 가장 최근에 업데이트된 레코드에서 가장 최근에 업데이트된 레코드로 순서가 지정됩니다. 따라서 가장 최근에 업데이트된 기회에서 금액 필드에 액세스하려면 다음을 사용합니다.

`${OpportunityList.get(0).Amount}`

이 예제에서는 OpportunityList 개체를 참조하고 get 메서드를 사용하여 0에서 인덱싱된 레코드에 액세스한 다음 반환된 개체에서 Amount 속성을 검색합니다. Opportunity 또는 Custom Object에서 필드를 편집기로 드래그하면 0에서 인덱싱된 레코드에서 필드가 자동으로 검색됩니다.

## SFDC 사용자 지정 개체 관계

SFDC 사용자 지정 개체를 사용할 수 있으려면 Marketo 리드에 대해 하나의 관계만 있어야 합니다. 오브젝트는 종종 연락처와 계정을 통해 연결되므로 리드/연락처 관계가 활성화된 Marketo에만 오브젝트를 동기화하는 것이 중요합니다.

## 트리거 개체

캠페인이 Added to Opportunity, Opportunity가 Updated 또는 Added to `<Custom Object Name>` 트리거를 통해 트리거되면 트리거 캠페인 컨텍스트 내에서 실행되는 스크립트 토큰에서 특수 변수를 사용할 수 있습니다. `$TriggerObject `(`<Custom Object Name>`에 대해 지원되지 않는 Updated 트리거가 업데이트됨).  `$TriggerObject` 참조를 사용하는 토큰을 일괄 캠페인에 사용하면 이 개체를 모든 종류의 일괄 캠페인에서 사용할 수 없으므로 전자 메일 전송이 실패합니다.  캠페인을 트리거한 개체에 대한 참조입니다. 개체에는 다른 변수 이름을 통해 액세스할 때 레코드에 있는 모든 데이터가 포함됩니다.

예를 들어 제품 주문에 대한 사용자 지정 개체를 통해 캠페인이 트리거된 경우 리드가 추가된 순서가 `$TriggerObject` 변수에 표시됩니다.

다음은 주문 후속 이메일에 대한 샘플 스크립트입니다.

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

`$TriggerObject` 변수를 사용하면 로컬 데이터를 가져올 사용 가능한 개체 중 하나를 결정하기 위해 전용 코드를 사용할 필요가 없다는 이점이 있습니다.  개체는 트리거 작업에 의해 결정됩니다. 이는 참조할 오브젝트를 선택하는 가장 명시적 방법이며, 사용 가능하고 적절한 경우 항상 사용해야 합니다.

참고: `$TriggerObject`을(를) 사용하는 경우 스크립트에서 개체를 사용할 수 있도록 하려면 편집 창에서 필드를 선택해야 합니다.

참고 2: `$TriggerObject`은(는) &quot;추가된&quot; 트리거에만 작동하고 &quot;업데이트된&quot; 트리거에는 작동하지 않습니다.
