---
title: EXL 미리보기 테스트
description: 확장 미리 보기 테스트를 위한 Adobe EXL Markdown 구문의 예입니다.
source-git-commit: 8f7ff2e1b6d0a4d8f63affb7bd1a2d0abbcc118c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 7%

---


# EXL 미리보기 테스트

## 경고 블록

>[!NOTE]
>
>이것은 노트입니다. 독자가 알고 있어야 하는 보충 정보에 대해서는 참고 사항을 활용한다.

>[!TIP]
>
>팁입니다. 팁은 선택적이지만 유용한 정보를 제공합니다.

>[!IMPORTANT]
>
>이는 중요한 경고입니다. 독자가 간과해서는 안 되는 정보를 위해 사용한다.

>[!WARNING]
>
>이것은 경고입니다. 잠재적 문제에 대한 정보에 사용됩니다.

>[!CAUTION]
>
>이것은 주의사항입니다. 잠재적 위험에 대한 정보를 보려면 를 사용하십시오.

>[!ADMIN]
>
>관리자 경고입니다. 관리자 전용 컨텐츠용.

>[!AVAILABILITY]
>
>가용성 정보입니다. 기능 가용성에 대한 세부 정보.

>[!PREREQUISITES]
>
>필수 구성 요소 블록입니다. 시작하기 전에 독자에게 필요한 사항을 나열하십시오.

## 음영 상자

>[!BEGINSHADEBOX &quot;선택적 제목&quot;]

이 콘텐츠는 회색 배경으로 나타납니다. 음영 상자를 사용하여 관련 콘텐츠를 시각적으로 그룹화합니다.

다음 목록을 포함할 수 있습니다.

- 항목 1
- 항목 2
- 항목 3

>[!ENDSHADEBOX]

>[!BEGINSHADEBOX]

제목이 없는 음영 상자.

>[!ENDSHADEBOX]

## 축소 가능한 섹션

+++확장하려면 클릭 — 기본 예

이 콘텐츠는 사용자가 제목을 선택할 때까지 숨겨집니다.

여기에 코드 블록을 포함한 모든 콘텐츠를 포함할 수 있습니다.

```javascript
const example = 'hello world';
console.log(example);
```

+++

+++고급 구성

기본 흐름을 흐리게 하는 선택적 또는 고급 콘텐츠에 대해 축소 가능한 섹션을 사용합니다.

| 설정 | 값 | 설명 |
| --- | --- | --- |
| timeout | 30 | 요청 제한 시간(초) 전 |
| 다시 시도 | 3 | 재시도 횟수 |

{style="table-layout:auto"}

+++

## 포함된 비디오

>[!VIDEO](https://video.tv.adobe.com/v/3427028/?quality=12&learn=on)

## 로컬라이제이션 매크로

지역화되지 않도록 제품 이름을 래핑하려면 [!DNL Marketo]을(를) 사용하십시오.

UI 요소 레이블에 **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**&#x200B;을(를) 사용합니다.

결합 예: [!DNL Adobe Analytics]에서 **[!UICONTROL Workspace]** > **[!UICONTROL Create project]**&#x200B;을(를) 선택합니다.

## 배지

[!BADGE Beta]{type=Informative}

[!BADGE 일반적으로 사용 가능]{type=Positive}

[!BADGE 사용되지 않음]{type=Negative}

[!BADGE 실험]{type=Caution}

## 탭

>[!BEGINTABS]

>[!TAB 요구 사항]

>[!IMPORTANT]
>
>이 작업을 완료하려면 관리자 권한이 있어야 합니다.

필수 필드:

| 필드 | 유형 | 필수 여부 |
| --- | --- | --- |
| 이름 | 문자열 | 예 |
| 이메일 | 문자열 | 예 |
| 역할 | 열거형 | 아니요 |

>[!TAB 단계]

1. Admin Console 을 엽니다.
1. **[!UICONTROL Users]** > **[!UICONTROL Add user]**&#x200B;을(를) 선택합니다.
1. 필수 필드를 입력합니다.
1. **[!UICONTROL Save]**&#x200B;를 선택합니다.

>[!NOTE]
>
>변경 사항은 즉시 적용됩니다.

>[!TAB 결과]

새 사용자는 암호를 설정할 수 있는 링크가 포함된 시작 이메일을 받게 됩니다.

- 링크는 24시간 후에 만료됩니다.
- 사용자는 로그인 페이지에서 새 링크를 요청할 수 있습니다.

>[!ENDTABS]

## 코드 블록

```json
{
  "name": "example",
  "version": "1.0.0",
  "enabled": true
}
```

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}
```

## 테이블

| 열 1 | 열 2 | 열 3 |
| --- | --- | --- |
| 행 1, 셀 1 | 행 1, 셀 2 | 행 1, 셀 3 |
| 행 2, 셀 1 | 행 2, 셀 2 | 행 2, 셀 3 |
