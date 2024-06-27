---
title: 잠재 고객 추적
description: 잠재 고객 추적 API
feature: Munchkin Tracking Code, Javascript
exl-id: 7ece5133-9d32-4be3-a940-4ac0310c4d8b
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# 잠재 고객 추적 API

Marketo의 Munchkin JavaScript를 사용하면 Marketo 랜딩 페이지 및 외부 웹 페이지에 대한 최종 사용자 페이지 방문 수 및 클릭 수를 추적할 수 있습니다. 이러한 기록은 Marketo에 &quot;웹 페이지 방문&quot; 및 &quot;웹 페이지에서 링크를 클릭함&quot; 활동으로 기록되며, 이 활동은 스마트 캠페인 및 스마트 목록의 트리거 및 필터에서 사용할 수 있습니다.

## 코드 포함

Marketo 인스턴스는 Marketo 인스턴스로 활동을 추적하는 외부 페이지에 코드를 포함하도록 사전 구성된 추적 코드 조각을 자동으로 제공합니다. 포함 코드 사용은 이에 의해 제어됩니다. [라이센스 계약](../munchkin-license.pdf).

다음 세 가지 추적 코드 유형을 사용할 수 있습니다.

1. 단순 - 동기적으로 로드합니다.
1. 비동기 - 비동기적으로 로드됨
1. 비동기 jQuery - 비동기적으로 로드되며 jQuery를 미리 로드해야 합니다.

외부 페이지에 Munchkin을 포함하는 데 비동기 추적 코드를 사용하는 것이 좋습니다. 실행 성공률을 최대한 높이려면 비동기 추적 코드를 `<head>` 을 참조하십시오.

일부 컨텐츠 관리 시스템은 임의의 스크립트를 포함할 때 특정 방법이나 제한을 가질 수 있습니다.

참조를 위해 최종 페이지에는 다음과 유사한 코드가 포함되어야 합니다 `<head>` HTML 문서:

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

Marketo Munchkin의 기본 동작은 페이지 로드 시 다음을 수행하는 것입니다.

1. 현재 브라우저에 Munchkin 쿠키가 있는지 확인하고 없는 경우 만듭니다.
1. 현재 페이지 및 브라우저의 정보를 사용하여 지정된 Marketo 인스턴스로 &quot;웹 페이지 방문&quot; 이벤트를 보냅니다. 활동을 Marketo의 해당 레코드에 기록합니다.
1. 링크에서 발생하는 모든 사용자 클릭에 대해 &quot;웹 페이지에서 클릭한 링크&quot; 이벤트를 보냅니다.

Munchkin의 동작은 Munchkin 사용을 통해 수정할 수 있습니다 [구성 설정](lead-tracking.md#lead-tracking-api)를 사용하여 페이지를 방문할 때 모든 잠재 고객에 대해 쿠키가 생성되는지 여부 등 `cookieAnon` 클릭 지연 설정 또는 수정 `clickTime` 설정. apiOnly 설정을 true로 설정하여 방문 활동 전송을 비활성화할 수 있습니다. 버전 162(2022년 8월)부터 클릭 수 `tel` 및 `mailto` 링크 추적 외 `http/s` 링크.

## 알려진 리드 및 익명 리드

도메인의 페이지에 대한 잠재 고객의 첫 번째 방문 시 Marketo에 새로운 익명 잠재 고객 레코드가 생성됩니다. 이 레코드의 기본 키는 Munchkin 쿠키(`_mkto_trk`)을 클릭하여 제품에서 사용할 수 있습니다. 해당 브라우저의 모든 후속 웹 활동은 이 익명 레코드에 대해 기록됩니다. Marketo의 알려진 레코드에 연결하려면 다음 중 하나가 발생해야 합니다.

- 잠재 고객은 다음을 사용하여 Munchkin 추적 페이지를 방문해야 합니다. `mkt_tok` 추적된 Marketo 이메일 링크의 쿼리 문자열에서 매개 변수.
- 잠재 고객은 Marketo Form을 작성해야 합니다.
- A SOAP [syncLead](../soap-api/leads.md) 또는 REST [리드 연결](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST) 호출을 전송해야 합니다.

이러한 조건 중 하나가 충족되면 쿠키 및 연결된 모든 웹 활동이 알려진 리드와 연결됩니다.

각 개별 브라우저에 대해 새로운 익명 웹 활동 레코드가 생성되므로 잠재 고객이 새 컴퓨터 및/또는 브라우저를 사용하여 도메인을 처음 방문하는 경우 이 연결이 다시 수행되어야 합니다.

## 도메인

Munchkin은 도메인 단위로 개별 쿠키를 만들고 추적하므로 알려진 리드 추적이 도메인 간에 발생하려면 각 도메인에 대해 리드 연결 이벤트가 발생해야 합니다. 예를 들어, 두 개의 도메인을 제어하는 경우 `marketo.com`, 및 `example.com`, 그리고 리드가 다음에 대한 양식을 작성합니다. `marketo.com`로 이동한 다음 로 이동합니다. `example.com` 나중에 해당 활동이 `marketo.com` 알려진 잠재 고객 레코드에서 추적되지만, 활동이 `example.com` 은(는) 익명입니다. 알려진 리드는 하위 도메인 간에 유지되므로 알려진 리드 `www.example.com` 은(는) 에도 알려진 리드 입니다. `info.example.com`.

최상위 도메인이 다음과 같은 두 부분인 경우 `.co.uk`를 클릭한 다음 코드가 올바르게 추적되도록 Munchkin 코드 조각에 domainLevel 매개 변수를 추가합니다. 다음을 참조하십시오 [여기](lead-tracking.md#domains) 을 참조하십시오.

## 쿠키

Munchkin 쿠키는 키를 사용합니다 `_mkto_trk`에는 이 패턴 다음의 값이 있습니다.

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

Munchkin 쿠키는 각 두 번째 수준 도메인에 한정됩니다. 즉, `example.com`. 쿠키의 기본 수명은 2년(730일)입니다.

## Beta

랜딩 페이지에 대한 Munchkin 베타 채널을 옵트인하려면 다음 위치로 이동하십시오. [책임자 -> 보물 상자](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) 을(를) 메뉴에 추가하고 &quot;랜딩 페이지의 Munchkin Beta&quot; 설정을 활성화합니다. 이렇게 하려면에서 새 코드 조각을 제공합니다 **[!UICONTROL Admin]** ->  **[!UICONTROL Munchkin]** 외부 사이트에서 beta 버전을 사용할 수 있는 메뉴입니다.

## 옵트아웃

방문자는 다음을 추가하여 Munchkin 추적을 완전히 거부할 수 있습니다. `querystring` 매개 변수 &quot;marketo_opt_out=true&quot;를 브라우저에 있는 URL에 추가합니다. Munchkin JavaScript가 이 설정을 감지하면 값이 인 새 쿠키 &quot;mkto_opt_out&quot;을 설정하려고 합니다. `true`. 이 설정이 검색되면 다른 모든 Marketo 추적 쿠키가 삭제되고, 새 쿠키가 설정되지 않으며, Munchkin에서 HTTP 요청을 수행하지 않습니다.
