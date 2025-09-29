---
title: 필드 유형
feature: REST API
description: ISO 8601 날짜/시간, 텍스트 영역 제한, 통화 및 부울을 비롯한 정의, 예 및 형식이 포함된 Marketo 필드 유형의 포괄적인 목록입니다.
exl-id: a0ba9e02-ed42-4be3-9cdd-a97fee9a726e
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 7%

---

# 필드 유형

다음은 Marketo의 필드 유형에 대한 설명입니다. 필드 형식에 대한 추가 정보는 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/custom-field-type-glossary)에서 찾을 수 있습니다. 필드 형식 제한에 대한 추가 정보는 [여기](https://nation.marketo.com/t5/knowledgebase/marketo-field-limits-by-field-type/ta-p/251613)에서 찾을 수 있습니다.

| 필드 유형 | 설명 | 예 |
| --- | --- | --- |
| 날짜/시간 | 날짜 및 시간을 입력하는 데 사용됩니다. [W3C 형식](https://www.w3.org/TR/NOTE-datetime)&#x200B;(ISO 8601)을 따릅니다. 가장 좋은 방법은 시간대 오프셋을 포함하는 것입니다. 완료 날짜 및 시간과 분: YYYY-MM-DDThh:mm:ssTZD - 여기서 TZD는 &quot;+hh:mm&quot; 또는 &quot;-hh:mm&quot;입니다. 참고: 일부 에셋 API는 `updatedAt` 및 `createdAt`에 대해 &quot;Z+0000&quot;을 TZD로 반환합니다. | 2010-05-07T15:41:32-05:00 |
| 이메일 | 이메일 주소를 허용하는 문자열 필드 | <example@example.com> |
| 부동 | 숫자 필드에는 실수가 포함되며 소수점 이하 자리를 사용할 수 있습니다. | 10.4 |
| 정수 | 정수 | 10 |
| 공식 | 잠재 고객 레코드에 있는 다른 필드의 데이터를 조작하여 값이 생성된 필드. 내보내지지 않으며 스마트 캠페인에서 사용할 수 없습니다. | 이 [문서](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/create-and-use-a-concatenated-string-formula-field) 보기 |
| 비율 | 정수로 표시되는 백분율 | 30 |
| URL | URL의 프로토콜을 포함하여 URL로 입력을 제한하는 텍스트 필드입니다. | <http://example.com/> |
| 전화 | 전화번호 | 111-111-1111 |
| 텍스트 영역 | 긴 텍스트입니다. | 최대 30,000바이트를 지원합니다. 표준 ASCII 문자는 문자당 1바이트를 사용합니다(최대 30,000자까지 가능). 유니코드 문자는 문자당 최대 4바이트를 사용할 수 있습니다(문자  30,000자 미만이 허용되는 문자 수). |
| 문자열 | 짧은 텍스트 | 최대 255자 텍스트 |
| 점수 | 점수 변경 흐름 단계로 조작할 수 있는 정수 필드 | 10 |
| 부울(이전 확인란) | 사용자가 True(선택됨) 또는 False(선택되지 않음) 값을 선택할 수 있습니다. | True |
| 통화 | Marketo 구독에 대해 선택한 기본 통화 유형을 나타내는 부동 소수점 필드 | 10.40 |
| Date | 날짜에 사용됨. W3C 형식을 따릅니다. | 2010년 5월 7일 |
| 참조 | 다른 레코드에 대한 키(외래 키)가 포함된 문자열 필드. | 담당자 회사 |
