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

Marketo의 Munchkin JavaScript을 사용하면 Marketo 랜딩 페이지 및 외부 웹 페이지에 대한 최종 사용자 페이지 방문 수 및 클릭 수를 추적할 수 있습니다. 이러한 기록은 Marketo에 &quot;웹 페이지 방문&quot; 및 &quot;웹 페이지에서 링크를 클릭함&quot; 활동으로 기록되며, 이 활동은 스마트 캠페인 및 스마트 목록의 트리거 및 필터에서 사용할 수 있습니다.

## 코드 포함

Marketo 인스턴스는 Marketo 인스턴스로 활동을 추적하는 외부 페이지에 코드를 포함하도록 사전 구성된 추적 코드 조각을 자동으로 제공합니다. 포함 코드 사용은 이 [라이선스 계약](../munchkin-license.pdf)의 적용을 받습니다.

다음 세 가지 추적 코드 유형을 사용할 수 있습니다.

1. 단순 - 동기적으로 로드합니다.
1. 비동기 - 비동기적으로 로드됨
1. 비동기 jQuery - 비동기적으로 로드되며 jQuery를 미리 로드해야 합니다.

외부 페이지에 Munchkin을 포함하는 데 비동기 추적 코드를 사용하는 것이 좋습니다. 실행 성공률을 최대한 높이려면 각 페이지의 `<head>`에 비동기 추적 코드를 포함하십시오.

일부 컨텐츠 관리 시스템은 임의의 스크립트를 포함할 때 특정 방법이나 제한을 가질 수 있습니다.

참조를 위해 최종 페이지에는 HTML 문서의 `<head>`에서 이와 유사한 코드가 포함되어야 합니다.

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

Munchkin [구성 설정](lead-tracking.md#lead-tracking-api)을 사용하여 Munchkin의 동작을 수정할 수 있습니다. 예를 들어 `cookieAnon` 설정으로 페이지를 방문할 때 모든 잠재 고객에 대해 쿠키가 생성되는지 또는 `clickTime` 설정으로 클릭 지연을 수정하는지 여부입니다. apiOnly 설정을 true로 설정하여 방문 활동 전송을 비활성화할 수 있습니다. 버전 162(2022년 8월)부터 클릭 수 `tel` 및 `mailto`개와 링크 `http/s`개가 추적됩니다.

## 알려진 리드 및 익명 리드

도메인의 페이지에 대한 잠재 고객의 첫 번째 방문 시 Marketo에 새로운 익명 잠재 고객 레코드가 생성됩니다. 이 레코드의 기본 키는 사용자 브라우저에서 만들어진 Munchkin 쿠키(`_mkto_trk`)입니다. 해당 브라우저의 모든 후속 웹 활동은 이 익명 레코드에 대해 기록됩니다. Marketo의 알려진 레코드에 연결하려면 다음 중 하나가 발생해야 합니다.

- 잠재 고객은 추적된 Marketo 이메일 링크의 쿼리 문자열에 `mkt_tok` 매개 변수가 있는 Munchkin 추적 페이지를 방문해야 합니다.
- 잠재 고객은 Marketo Form을 작성해야 합니다.
- SOAP [syncLead](../soap-api/leads.md) 또는 REST [리드 연결](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST) 호출을 보내야 합니다.

이러한 조건 중 하나가 충족되면 쿠키 및 연결된 모든 웹 활동이 알려진 리드와 연결됩니다.

각 개별 브라우저에 대해 새로운 익명 웹 활동 레코드가 생성되므로 잠재 고객이 새 컴퓨터 및/또는 브라우저를 사용하여 도메인을 처음 방문하는 경우 이 연결이 다시 수행되어야 합니다.

## 도메인

Munchkin은 도메인 단위로 개별 쿠키를 만들고 추적하므로 알려진 리드 추적이 도메인 간에 발생하려면 각 도메인에 대해 리드 연결 이벤트가 발생해야 합니다. 예를 들어 두 개의 도메인 `marketo.com`과(와) `example.com`을(를) 제어하고 `marketo.com`에서 잠재 고객이 양식을 작성한 후 나중에 `example.com`(으)로 이동하면 `marketo.com`의 해당 활동이 알려진 잠재 고객 레코드에서 추적되지만 `example.com`의 해당 활동은 익명입니다. 알려진 리드는 하위 도메인 간에 유지되므로 `www.example.com`의 알려진 리드는 `info.example.com`의 알려진 리드이기도 합니다.

최상위 도메인이 `.co.uk`과(와) 같은 두 부분인 경우 코드가 올바르게 추적되도록 Munchkin 코드 조각에 domainLevel 매개 변수를 추가하십시오. 자세한 내용은 [여기](lead-tracking.md#domains)를 참조하세요.

## 쿠키

Munchkin 쿠키는 키 `_mkto_trk`을(를) 사용하며 다음 패턴 값을 가집니다.

`id:561\-HYG\-937&token:_mch\-marketo.com\-1374552656411\-90718`

Munchkin 쿠키는 각 두 번째 수준 도메인, 즉 `example.com`에 한정됩니다. 쿠키의 기본 수명은 2년(730일)입니다.

## Beta

랜딩 페이지에 대해 Munchkin 베타 채널을 옵트인하려면 [관리자 -> 보물 상자](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) 메뉴로 이동하여 &quot;랜딩 페이지에 Munchkin Beta&quot; 설정을 활성화하십시오. **[!UICONTROL Admin]** ->에 새 코드 조각을 제공합니다.  외부 사이트에서 Beta 버전을 사용할 수 있는 **[!UICONTROL Munchkin]** 메뉴.

## 옵트아웃

방문자는 브라우저의 URL에 `querystring` 매개 변수 &quot;marketo_opt_out=true&quot;를 추가하여 Munchkin 추적을 완전히 옵트아웃할 수 있습니다. Munchkin JavaScript이 이 설정을 감지하면 값이 `true`인 새 쿠키 &quot;mkto_opt_out&quot;을 설정하려고 합니다. 이 설정이 검색되면 다른 모든 Marketo 추적 쿠키가 삭제되고, 새 쿠키가 설정되지 않으며, Munchkin에서 HTTP 요청을 수행하지 않습니다.
