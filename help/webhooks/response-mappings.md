---
title: "응답 매핑"
feature: Webhooks
description: "Marketo에 대한 응답 매핑"
source-git-commit: bcc0c0c8e8209cf9fb962a85c8e7da354d95a8fe
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# 응답 매핑

Marketo은 Webhook에서 두 개의 콘텐츠 유형에서 수신한 데이터를 번역하고 이러한 값을 다시 리드 필드(JSON 및 XML)로 반환할 수 있습니다. Marketo 필드 매개 변수는 항상 [SOAP API 이름](../rest-api/fields.md) 필드의 을 참조하십시오. 각 Webhook에는 응답 매핑이 무제한으로 있을 수 있으며, 이 매핑은 [!UICONTROL Edit] Webhook의 Response Mappings 창에 있는 단추:

![응답 매핑](assets/response-mapping.png)

응답 매핑은 &quot;응답 속성&quot;, XML 또는 JSON 문서에서 원하는 속성에 대한 경로 및 응답 속성에서 값이 기록된 잠재 고객 필드를 지정하는 &quot;Marketo 필드&quot;의 쌍을 통해 만들어집니다.

속성 키는 Marketo 응답 매핑을 통해 액세스할 수 있는 영숫자, 대시(-), 밑줄(_), 콜론(:) 및 공백으로 구성되어야 합니다.

## JSON 매핑

JSON 속성은 점 표기법 및 배열 표기법을 사용하여 액세스됩니다. Marketo의 배열 표기법은 문자열을 입력으로 허용하지 않으며 정수만 허용합니다. JSON 문서에서 데이터를 검색하려면 응답 유형을 JSON으로 설정해야 합니다.

```json
{ "foo":"bar"}
```

에 액세스하려면 `foo` 응답 매핑의 속성을 사용하려면 `name` JSON 개체의 첫 번째 수준에 있기 때문에 속성의 `foo`. Marketo의 모습은 다음과 같습니다.

![응답 매핑](assets/json-resp.png)

다음은 배열에 대한 보다 복잡한 예입니다.

```json
{
    "profileId" : 1234,
    "firstName" : "Jane",
    "lastName" : "Doe",
    "orders" : [
        {
            "orderId" : 5678,
            "orderDate" : "2015-01-01",
            "orderProductId" : "4982"
        },
        {
            "orderId" : 5678,
            "orderDate" : "2014-05-07",
            "orderProductId" : "4982"
        }
    ]
}
```

orders 배열의 첫 번째 요소에서 orderDate에 액세스하려고 합니다. 이 속성에 액세스하려면 다음을 사용하십시오. `orders[0].orderDate`

## XML 매핑

XML 문서의 개별 요소에서 값에 액세스할 수 있습니다. JSON 매핑과 유사한 점 표기법을 사용합니다. 이 간단한 예를 살펴보겠습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<example>
    <foo>bar</foo>
</example>
```

여기에서 foo 속성에 액세스하려면 다음을 사용하십시오. `example.foo`

에 액세스하기 전에 먼저 예제 요소를 참조해야 함 `foo`. 속성에 액세스하려면 매핑에서 계층 구조의 모든 요소를 참조해야 합니다. 배열이 있는 XML 문서는 좀 더 복잡합니다. 다음 예를 사용하십시오.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<elementList>
    <element>
        <foo>baz</foo>
    </element>
    <element>
        <foo>bar</foo>
    </element>
    <element>
        <foo>bar</foo>
    </element>
</elementList>
```

문서는 상위 배열로 구성됩니다 `elementList`, 1차 하위 구성요소 포함, 1개의 속성이 포함된 요소: `foo`. Marketo 응답 매핑 목적으로 배열은 (으)로 참조됩니다. `elementList.element`를 통해 elementList의 하위 항목에 액세스할 수 있습니다. `elementList.element[i]`. elementList의 첫 번째 자식에서 foo의 값을 가져오려면 이 응답 특성을 사용합니다. `elementList.element[0].foo` 지정된 필드에 값 &quot;baz&quot;가 반환됩니다. 고유한 요소 이름과 고유하지 않은 요소 이름이 모두 포함된 요소 내의 속성에 액세스하려고 하면 정의되지 않은 동작이 발생합니다. 각 요소는 단일 속성 또는 배열이어야 하며 형식을 혼합할 수 없습니다.

## 유형

속성을 필드에 매핑할 때 Webhook 응답의 유형이 대상 필드와 호환되는지 확인해야 합니다. 예를 들어 응답의 값이 문자열이고 선택한 필드가 정수 유형인 경우 값이 기록되지 않습니다. 읽어보기 [필드 유형](../rest-api/field-types.md).
