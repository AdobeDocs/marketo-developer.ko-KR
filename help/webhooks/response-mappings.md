---
title: 응답 매핑
feature: Webhooks
description: JSON 및 XML에 대한 Marketo 웹후크 응답 매핑, SOAP API 이름, 점 및 배열 표기법 및 유형 호환성을 사용하여 속성을 리드 필드에 매핑합니다.
exl-id: 95c6e33e-487c-464b-b920-3c67e248d84e
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 응답 매핑

Marketo은 Webhook에서 두 개의 콘텐츠 유형에서 수신한 데이터를 번역하고 이러한 값을 다시 리드 필드(JSON 및 XML)로 반환할 수 있습니다. Marketo 필드 매개 변수는 항상 필드의 [SOAP API 이름](../rest-api/fields.md)을(를) 사용합니다. 각 Webhook에는 Webhook의 응답 매핑 창에서 [!UICONTROL Edit] 버튼을 클릭하여 추가 및 편집되는 응답 매핑이 무제한으로 있을 수 있습니다.

![응답 매핑](assets/response-mapping.png)

응답 매핑은 &quot;응답 속성&quot;, XML 또는 JSON 문서에서 원하는 속성에 대한 경로 및 응답 속성에서 값이 기록된 잠재 고객 필드를 지정하는 &quot;Marketo 필드&quot;의 쌍을 통해 만들어집니다.

속성 키는 Marketo 응답 매핑을 통해 액세스할 수 있는 영숫자, 대시(-), 밑줄(_), 콜론(:) 및 공백으로 구성되어야 합니다.

## JSON 매핑

JSON 속성은 점 표기법 및 배열 표기법을 사용하여 액세스됩니다. Marketo의 배열 표기법은 문자열을 입력으로 허용하지 않으며 정수만 허용합니다. JSON 문서에서 데이터를 검색하려면 응답 유형을 JSON으로 설정해야 합니다.

```json
{ "foo":"bar"}
```

응답 매핑의 `foo` 속성에 액세스하려면 속성의 `name`을(를) 사용하십시오. 이 속성은 JSON 개체의 첫 번째 수준인 `foo`에 있기 때문입니다. Marketo의 모습은 다음과 같습니다.

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

`foo`에 액세스하기 전에 먼저 예제 요소를 참조해야 합니다. 속성에 액세스하려면 매핑에서 계층 구조의 모든 요소를 참조해야 합니다. 배열이 있는 XML 문서는 좀 더 복잡합니다. 다음 예를 사용하십시오.

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

이 문서는 부모 배열 `elementList`(자식 포함)로 구성되며, 하나의 속성이 포함된 요소입니다. `foo`. Marketo 응답 매핑을 위해 배열이 `elementList.element`(으)로 참조되므로 elementList의 자식은 `elementList.element[i]`을(를) 통해 액세스됩니다. elementList의 첫 번째 자식에서 foo 값을 가져오려면 이 응답 특성을 사용합니다. `elementList.element[0].foo` 이 특성은 지정된 필드에 &quot;baz&quot; 값을 반환합니다. 고유한 요소 이름과 고유하지 않은 요소 이름이 모두 포함된 요소 내의 속성에 액세스하려고 하면 정의되지 않은 동작이 발생합니다. 각 요소는 단일 속성 또는 배열이어야 하며 형식을 혼합할 수 없습니다.

## 유형

속성을 필드에 매핑할 때 Webhook 응답의 유형이 대상 필드와 호환되는지 확인해야 합니다. 예를 들어 응답의 값이 문자열이고 선택한 필드가 정수 유형인 경우 값이 기록되지 않습니다. [필드 형식](../rest-api/field-types.md)에 대해 읽어 보십시오.
