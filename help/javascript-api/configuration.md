---
title: 구성
description: JavaScript API를 사용하여 Marketo Munchkin을 구성합니다. altIds, anonymizeIP, asyncOnly, 쿠키 수명, domainLevel, 비콘 API와 같은 Munchkin.init 설정에 대해 알아봅니다.
feature: Munchkin Tracking Code, Javascript
exl-id: 4700ce7b-f624-4f27-871e-9a050f203973
TQID: https://experienceleague.adobe.com/ip2cCGgoa83v8m9GYLYXe132veYxS1C6UWX1iLB6X5Q
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 541
ht-degree: 5%

---

# 구성

Munchkin은 동작을 사용자 지정하는 구성 설정을 허용합니다. [Munchkin.init()](api-reference.md#munchkin_init)의 두 번째 매개 변수에서 설정을 JavaScript 개체의 속성으로 전달합니다.

```json
Munchkin.init("AAA-BBB-CCC", {
        "configName":"configValue",
        "configName2":"configValue2"
    }
);
```

구성 설정 객체에는 다음 표의 등록 정보가 포함될 수 있습니다.

## 속성

| 이름 | 데이터 유형 | 설명 |
| --- | --- | --- |
| altIds | 배열 | Munchkin ID 문자열 배열을 허용합니다. 활성화되면 모든 웹 활동이 해당 Munchkin ID로 식별되는 가입에 복제됩니다. |
| 익명화 | 부울 | 신규 방문자를 위해 Marketo에 기록된 IP 주소를 익명화합니다. |
| apiOnly | 부울 | true로 설정하면 `Munchkin.Init()` 함수가 `visitsWebPage`을(를) 호출하지 않습니다. 모든 `visitsWebPage` 이벤트를 완벽하게 제어해야 하는 단일 페이지 웹 응용 프로그램에 유용합니다. |
| asyncOnly | 부울 | true로 설정하면 가 XMLHttpRequests를 비동기적으로 전송합니다. 기본값은 false입니다. |
| clickTime | 정수 | 클릭 추적 요청이 완료될 수 있도록 클릭 후 차단할 시간(밀리초)을 설정합니다. 이 값을 줄이면 클릭 추적 정확도가 줄어듭니다. 기본값은 350ms입니다. |
| cookieAnon | 부울 | false로 설정하면, 새로운 익명 리드에 대한 추적 및 쿠키 생성이 금지됩니다. 리드는 쿠키를 수신하고 Marketo 양식을 제출하거나 Marketo 이메일에서 클릭스루한 후 추적됩니다. 기본값은 true입니다. |
| cookieLifeDays | 정수 | 새로 생성된 Munchkin 추적 쿠키의 만료 날짜를 미래의 이 요일로 설정합니다. 기본값은 730일(2년)입니다. |
| customName | 문자열 | 사용자 지정 페이지 이름. 시스템 전용. |
| <a name="domainlevel"></a>domainLevel | 정수 | 쿠키의 도메인 속성에 사용할 페이지 도메인의 부분 수를 설정합니다.<br><br>www.example.com의 경우 `domainLevel: 2`은(는) 쿠키 도메인을 &quot;.example.com&quot;으로 설정하고 `domainLevel: 3`은(는) 쿠키 도메인을 &quot;.www.example.com&quot;으로 설정합니다.<br><br>기본적으로 Munchkin은 최상위 도메인에 세 개의 문자가 있을 때 두 부분을 사용합니다. 예를 들어 &quot;www.example.com&quot;은 &quot;.example.com&quot;을 사용합니다.<br><br>&quot;.jp&quot;, &quot;.us&quot;, &quot;.cn&quot; 및 &quot;.uk&quot;와 같은 두 글자 국가 코드의 경우 Munchkin은 세 부분을 사용합니다. 예를들어, &quot;www.example.co.jp&quot;은 &quot;.example.co.jp&quot;을 사용합니다.<br><br>도메인 패턴에 다른 동작이 필요한 경우 `domainLevel` 매개 변수를 사용합니다. |
| domainSelectorV2 | 부울 | true로 설정하면 는 향상된 방법을 사용하여 쿠키 도메인 속성을 설정하는 방법을 결정합니다. |
| https만 | 부울 | 기본값은 false입니다. true로 설정되면 은 추적된 페이지가 https를 통해 제공되었을 때 보안 설정을 사용하도록 쿠키를 설정합니다. |
| useBeaconAPI | 부울 | 기본값은 false입니다. true로 설정하면 [Beacon API](https://developer.mozilla.org/en-US/docs/Web/API/Beacon_API)를 사용하여 [XMLHttpRequest](https://developer.mozilla.org/ko_KR/docs/Web/API/XMLHttpRequest) 대신 비차단 요청을 보냅니다. 브라우저가 Beacon API를 지원하지 않으면 Munchkin은 XMLHttpRequest를 사용합니다. |
| wsInfo | 문자열 | 작업 영역을 타깃팅합니다. 관리 > 통합 > Munchkin 메뉴에서 작업 공간을 선택하여 작업 공간 ID를 얻습니다.<br><br>이 설정은 익명 잠재 고객 레코드를 처음 만들 때만 적용됩니다. 해당 잠재 고객 레코드에 대해 Munchkin 쿠키 값이 설정된 후에는 wsInfo 매개 변수가 해당 파티션을 변경할 수 없습니다.<br><br>이 설정은 익명 리드에만 영향을 주므로 파티션별 [웹 보고서의 익명 방문자](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/reporting/basic-reporting/report-activity/display-people-or-anonymous-visitors-in-web-reports)에만 관련됩니다. |

## 예

### 여러 구독에 활동 보내기

이 예제는 모든 웹 활동을 Munchkin ID가 &quot;AAA-BBB-CCC&quot; 및 &quot;XXX-YYY-ZZZ&quot;인 인스턴스에 보냅니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      // Add configuration settings to the init method
      Munchkin.init('AAA-BBB-CCCC', { 'altIds': ['XXX-YYY-ZZZ'] });
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
```

### 추적을 비동기식으로 설정

이 예제에서는 모든 XMLHttpRequests를 기본 스레드에서 비동기적으로 보냅니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      // Add configuration settings to the init method
      Munchkin.init('AAA-BBB-CCC', { 'asyncOnly': true });
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin-beta.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```
