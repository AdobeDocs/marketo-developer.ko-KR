---
title: 잠재 고객 추적
description: Marketo Munchkin JavaScript을 포함하고, 방문 횟수 및 클릭 수를 추적하고, 알려진 리드와 익명 리드를 관리하고, 도메인 간 쿠키를 관리하고, 스마트 캠페인을 옵트아웃하는 방법에 대해 알아봅니다.
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
TQID: https://experienceleague.adobe.com/nGUcLLgL9X7PBKf2E5IzppDj8e-SyEtxmkQaESd90mE
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
subfeature_v2:
  - id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 718
ht-degree: 0%

---

# 잠재 고객 추적 API

Marketo의 Munchkin JavaScript은 Marketo 랜딩 페이지 및 외부 웹 페이지에서 페이지 방문 및 링크 클릭을 추적합니다. Marketo은 이러한 상호 작용을 &quot;웹 페이지 방문&quot; 및 &quot;웹 페이지에서 링크를 클릭함&quot; 활동으로 기록합니다.

스마트 캠페인 및 스마트 목록용 트리거 및 필터의 활동을 사용합니다.

## 코드 포함

Marketo 인스턴스는 외부 페이지에서 활동을 추적하기 위해 사전 구성된 코드 조각을 제공합니다. 포함 코드 사용은 이 [라이선스 계약](../munchkin-license.pdf)의 적용을 받습니다.

다음 세 가지 추적 코드 유형을 사용할 수 있습니다.

1. 단순(Simple) - 동기식으로 로드합니다.
1. 비동기(Asynchronous) - 비동기적으로 로드됩니다.
1. 비동기 jQuery - 비동기적으로 로드되며 먼저 로드하려면 jQuery가 필요합니다.

비동기 추적 코드를 사용하여 외부 페이지에 Munchkin을 포함합니다. 실행 성공률이 가장 높으면 각 페이지의 `<head>` 요소에 코드를 넣습니다.

일부 컨텐츠 관리 시스템은 임의의 스크립트를 포함할 때 특정 방법이나 제한을 가질 수 있습니다.

최종 페이지에는 HTML 문서의 `<head>` 요소에 있는 다음 예제와 유사한 코드가 포함되어야 합니다.

```html
<head>
    <script type="text/javascript">
    (function() {
        var didInit = false;
        function initMunchkin() {
            if(didInit === false) {
                didInit = true;
                Munchkin.init('CHANGE-ME');
            }
        }
        var s = document.createElement('script');
        s.type = 'text/javascript';
        s.async = true;
        s.src = '//munchkin.marketo.net/munchkin.js';
        s.onreadystatechange = function() {
            if (this.readyState == 'complete' || this.readyState == 'loaded') {
                initMunchkin();
            }
        };
        s.onload = initMunchkin;
        document.getElementsByTagName('head')[0].appendChild(s);
        })();
    </script>
    ...
</head>
```

## Munchkin 동작

기본적으로 Marketo Munchkin은 페이지가 로드될 때 다음 작업을 수행합니다.

1. 현재 브라우저에 Munchkin 쿠키가 있는지 확인하고 필요한 경우 만듭니다.
1. 현재 페이지와 브라우저의 정보를 사용하여 지정된 Marketo 인스턴스에 &quot;웹 페이지 방문&quot; 이벤트를 보냅니다. 이 이벤트는 해당 Marketo 레코드에 대한 활동을 기록합니다.
1. 사용자가 링크를 선택하면 &quot;웹 페이지에서 클릭한 링크&quot; 이벤트를 보냅니다.

이 동작을 변경하려면 Munchkin [구성 설정](configuration.md)을 사용하세요. 예를 들어 `cookieAnon`을(를) 사용하여 Munchkin이 페이지를 방문하는 모든 리드에 대해 쿠키를 만들지 여부를 제어하거나 `clickTime`을(를) 사용하여 클릭 지연을 변경할지 여부를 제어합니다.

방문 활동을 비활성화하려면 `apiOnly`을(를) true로 설정합니다. 버전 162(2022년 8월)부터 Munchkin은 `http/s`개의 링크 외에 `tel` 및 `mailto`개의 링크에 대한 클릭 수를 추적합니다.

## 알려진 리드 및 익명 리드

잠재 고객이 도메인의 페이지를 처음 방문하면 Marketo에서 익명 잠재 고객 레코드를 만듭니다. 이 레코드의 기본 키는 사용자의 브라우저에서 만들어진 Munchkin 쿠키(`_mkto_trk`)입니다.

Marketo은 해당 브라우저의 후속 웹 활동을 익명 레코드에 기록합니다. 활동을 알려진 Marketo 레코드와 연결하려면 다음 이벤트 중 하나가 발생해야 합니다.

- 잠재 고객은 추적된 Marketo 이메일 링크의 쿼리 문자열에 `mkt_tok` 매개 변수가 있는 Munchkin 추적 페이지를 방문해야 합니다.
- 잠재 고객은 Marketo Form을 작성해야 합니다.
- REST [리드 연결](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/associateLeadUsingPOST) 호출을 보내야 합니다.

이러한 이벤트 중 하나가 발생하면 Marketo은 쿠키 및 모든 관련 웹 활동을 알려진 리드와 연결합니다.

Marketo은 각 브라우저에 대해 익명 웹 활동 레코드를 만듭니다. 잠재 고객이 새 컴퓨터 또는 브라우저에서 도메인을 방문하는 경우 연결이 다시 수행되어야 합니다.

## 도메인

Munchkin은 도메인별로 쿠키를 만들고 추적합니다. 도메인 간에 알려진 리드를 추적하려면 각 도메인에서 리드 연결 이벤트가 발생해야 합니다.

예를 들어 `marketo.com` 및 `example.com`을(를) 제어한다고 가정합니다. 잠재 고객이 `marketo.com`에 양식을 제출하고 나중에 `example.com`(으)로 이동합니다. `marketo.com`의 활동이 알려진 잠재 고객과 연결되어 있지만 `example.com`의 활동은 익명입니다.

알려진 리드는 하위 도메인 간에 유지됩니다. `www.example.com`의 알려진 잠재 고객 또한 `info.example.com`의 알려진 잠재 고객입니다.

최상위 도메인에 `.co.uk`과(와) 같은 두 부분이 있는 경우 `domainLevel` 매개 변수를 Munchkin 코드 조각에 추가하십시오. 자세한 내용은 [구성](configuration.md#domainlevel)을 참조하세요.

## 쿠키

Munchkin 쿠키에서는 `_mkto_trk` 키와 다음 패턴 중 하나를 따르는 값을 사용합니다.

`id:561-HYG-937&token:_mch-marketo.com-1374552656411-90718`

Or

`id:561-HYG-937&token:_mch-marketo.com-97bf4361ef4433921a6da262e8df45a`

Munchkin 쿠키는 `example.com`과(와) 같은 각 두 번째 수준 도메인에만 적용됩니다. 기본 쿠키 수명은 2년(730일)입니다.

## Beta

랜딩 페이지에 Munchkin 베타 채널을 옵트인하려면 [관리자 -> 보물 상자](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features)&#x200B;(으)로 이동하여 &quot;랜딩 페이지에 Munchkin Beta&quot; 설정을 활성화하십시오.

이 설정은 **[!UICONTROL Admin]** -> **[!UICONTROL Munchkin]** 메뉴에 코드 조각을 추가합니다. 이러한 코드 조각을 사용하여 외부 사이트에서 베타 버전을 실행할 수 있습니다.

## 옵트아웃

방문자는 브라우저의 URL에 `querystring` 매개 변수 &quot;marketo_opt_out=true&quot;를 추가하여 Munchkin 추적을 옵트아웃할 수 있습니다. Munchkin JavaScript에서 이 설정을 감지하면 값이 `true`인 새 &quot;mkto_opt_out&quot; 쿠키를 설정하려고 합니다.

그런 다음 Munchkin은 다른 모든 Marketo 추적 쿠키를 삭제하고, 새 쿠키를 설정하지 않으며, HTTP 요청을 하지 않습니다.
