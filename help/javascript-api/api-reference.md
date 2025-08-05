---
title: Munchkin API 참조
description: Munchkin Javascript API를 사용하여 Munchkin 데이터를 사용자 지정합니다.
feature: Munchkin Tracking Code, Javascript
exl-id: e9727691-5501-4223-bc98-2b4bacc33513
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 7%

---

# Munchkin API 참조

Munchkin은 Javascript를 통해 수동으로 호출할 수 있는 여러 기능을 제공합니다. 이를 통해 비디오 재생 또는 링크가 아닌 클릭 수와 같은 브라우저 이벤트를 사용자 지정할 수 있습니다.

## 함수

Munchkin API는 다음 함수로 구성됩니다. `init`, `createTrackingCookie`, `munchkinFunction`.

<a name="munchkin_init"></a>

### Munchkin.init()

`Munchkin.init()`을(를) 다른 함수 앞에 호출해야 합니다. 활동을 특정 인스턴스로 보내도록 현재 페이지에서 Munchkin을 설정하고 현재 페이지에 대한 &quot;방문 웹 페이지&quot; 활동을 생성합니다.

| 매개 변수 이름 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| Munchkin ID | 필수 | 문자열 | Munchkin 계정 ID는 관리 > 통합 > Munchkin 메뉴에서 찾을 수 있습니다. 활동을 보낼 대상 인스턴스를 설정합니다. |
| [구성 설정](configuration.md) | 선택 사항입니다 | 오브젝트 | Munchkin에 대한 대체 동작 설정을 활성화합니다. |

```javascript
Munchkin.init('299-BYM-827');
```

### Munchkin.createTrackingCookie()

호출되면 브라우저에 `_mkto_trk` 쿠키가 있는지 확인하고 없는 경우 만듭니다. `cookieAnon`이(가) false로 설정된 경우 등록 또는 에셋 다운로드와 같은 특정 작업 동안 사용자를 추적하는 데 유용합니다.

| 매개 변수 이름 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| forceCreate | 필수 | 부울 | `cookieAnon`이(가) false로 설정된 경우에도 쿠키를 만듭니다. |

```javascript
Munchkin.createTrackingCookie(true);
```

### Munchkin.munchkinFunction()

비디오 플레이어 재생 및 일시 중단과 같은 사용자 지정 추적 비헤이비어 또는 해시 코드와 같은 비표준 탐색을 위한 페이지 방문 횟수를 생성하는 데 사용됩니다.

| 매개 변수 이름 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| 함수 유형 | 필수 | 문자열 | 기록할 활동을 결정합니다. 허용되는 값: `visitWebPage`, `clickLink`, `associateLead` |
| 데이터 | 필수 | 오브젝트 | 기록할 활동에 대한 데이터를 포함합니다. |

#### visitWebpage

`munchkinFunction()`(으)로 `visitWebPage`을(를) 호출하면 현재 사용자에 대한 &#39;방문&#39; 활동이 Marketo으로 전송됩니다. 두 번째 인수의 데이터 개체와 함께 전송되는 URL 및 `querystring`을(를) 사용자 지정할 수 있습니다.

| 데이터 속성 이름 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| url | 필수 | 문자열 | 페이지 방문을 기록하는 데 사용되는 URL 파일 경로입니다.  이 값은 전체 페이지 이름을 만들기 위해 현재 도메인 이름에 추가됩니다. 예를 들어 URL이 `/index.html`이고 도메인 이름이 `www.example.com`인 경우 방문한 페이지는 `www.example.com/index.html`(으)로 기록됩니다. |
| params | 선택 사항입니다 | 문자열 | 기록할 원하는 매개 변수의 쿼리 문자열입니다. |

예: `foo=bar&biz=baz`.

```javascript
Munchkin.munchkinFunction('visitWebPage', {
        'url': '/Football/Team/Seahawks',
        'params': 'defense=legion_of_boom&qb=wilson'
    }
);
```

#### clickLink

`munchkinFunction()`(으)로 `clickLink`을(를) 호출하면 현재 사용자에 대한 클릭 활동이 Marketo으로 전송됩니다. 데이터 개체에서 `href` 속성을 사용하여 클릭 URL을 사용자 지정할 수 있습니다.

| 데이터 속성 이름 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| href | 필수 | 문자열 | 링크 클릭을 기록하는 데 사용되는 URL 파일 경로입니다. 이 값은 전체 링크를 만들기 위해 현재 도메인 이름에 추가됩니다. |

예를 들어 href가 `/index.html`이고 도메인 이름이 `www.example.com`인 경우 링크 클릭은 `www.example.com/index.html`(으)로 기록됩니다.

```javascript
Munchkin.munchkinFunction('clickLink', {
        'href': '/Football/Team/Seahawks'
    }
);
```

#### associateLead

이 메서드는 더 이상 사용되지 않으며 더 이상 사용할 수 없습니다.
