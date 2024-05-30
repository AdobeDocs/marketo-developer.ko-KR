---
title: "구성"
description: "구성 API"
feature: Javascript
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 3%

---


# 구성

Munchkin은 다양한 구성 설정을 사용하여 동작을 사용자 지정할 수 있습니다. 구성 설정은 호출 시 두 번째 매개 변수로 전달되는 JavaScript 개체의 속성입니다 [Munchkin.init()](lead-tracking.md#munchkin-behavior)

```json
Munchkin.init("AAA-BBB-CCC", {
        "configName":"configValue",
        "configName2":"configValue2"
    }
);
```

구성 설정 객체에는 아래 표의 속성을 원하는 수만큼 포함할 수 있습니다.

## 속성

| 이름 | 데이터 유형 | 설명 |
|---|---|---|
| altIds | 배열 | Munchkin ID 문자열 배열을 허용합니다. 활성화되면 Munchkin ID를 기반으로 타겟팅된 구독에 모든 웹 활동이 복제됩니다. |
| 익명화 | 부울 | 신규 방문자를 위해 Marketo에 기록된 IP 주소를 익명으로 표시합니다. 다음을 확인하면 구독이 Munchkin V2로 프로비저닝되는지 확인할 수 있습니다. `{Munchkin-Id}.mktoresp.com` 도메인에는 다음 주소 중 하나가 있습니다. `192.28.144.124` `134.213.193.62` `192.28.147.68` `103.237.104.82`. 또는 nslookup {munchkin-id}.mktoresp.com에서 아래 스크립트를 실행할 수 있습니다. | grep -E -c -e &quot;(192.28.144.124,134.213.193.62,192.28.147.68,103.237.104.82)&quot; 명령이 &#39;0&#39;을 출력하면 구독이 Munchkin V2로 프로비저닝되지 않습니다. 1 이상을 출력하면 구독이 프로비저닝됩니다. |
| apiOnly | 부울 | true로 설정하면 `Munchkin.Init()` 함수는 를 호출하지 않습니다. `visitsWebPage`. 이 기능은 다음을 모두 완벽하게 제어해야 하는 단일 페이지 웹 애플리케이션에 유용합니다 `visitsWebPage` 이벤트. |
| asyncOnly | 부울 | true로 설정하면 가 XMLHttpRequest의 를 비동기적으로 전송합니다. 기본값은 false입니다. |
| clickTime | 정수 | 클릭 추적 요청을 허용하기 위해 클릭 후 차단할 시간(밀리초)을 설정합니다. 이를 줄이면 클릭 추적의 정확도가 줄어듭니다. 기본값은 350ms입니다. |
| cookieAnon | 부울 | false로 설정하면, 새로운 익명 리드의 추적 및 쿠키 생성이 금지됩니다. 잠재 고객은 쿠키를 가지며, Marketo 양식을 작성한 후 또는 Marketo 이메일에서 클릭스루하여 추적됩니다. 기본값은 true입니다. |
| cookieLifeDays | 정수 | 새로 생성된 Munchkin 추적 쿠키의 만료 날짜를 미래의 일 수로 설정합니다. 기본값은 730일(2년)입니다. |
| customName | 문자열 | 사용자 지정 페이지 이름. 시스템 전용. |
| domainLevel | 정수 | 쿠키의 도메인 속성을 설정할 때 사용할 페이지의 도메인 부분 수를 설정합니다.예를 들어 현재 페이지 도메인이 &quot;www.example.com&quot;이라고 가정해 보겠습니다.domainLevel: 2는 쿠키 도메인 속성을 &quot;.example.com&quot;으로 설정합니다.domainLevel: 3은 쿠키 도메인 속성을 &quot;.www.example.com&quot;으로 설정합니다.Background:Munchkin은 두 문자로 이루어진 특정 최상위 도메인을 자동으로 관리합니다. 최상위 도메인이 3자인 일반적인 경우 기본적으로 두 부분으로 설정됩니다. 예를 들어 &quot;www.example.com&quot;과 같이 가장 오른쪽에 있는 두 부분을 사용하여 쿠키 &quot;.example.com&quot;을 설정합니다. &quot;.jp&quot;, &quot;.us&quot;, &quot;.cn&quot; 및 &quot;.uk&quot;와 같은 두 문자 국가 코드의 경우 기본값은 세 부분으로 설정됩니다. 예를 들어 &quot;www.example.co.jp&quot;은 세 개의 가장 오른쪽 도메인 부분 &quot;.example.co.jp&quot;을 사용합니다. 도메인 패턴에 다른 동작이 필요한 경우 다음을 사용하여 지정해야 합니다. `domainLevel` 매개 변수. |
| domainSelectorV2 | 부울 | true로 설정하면 는 향상된 방법을 사용하여 쿠키 도메인 속성을 설정하는 방법을 결정합니다. |
| https만 | 부울 | 기본값은 false입니다. true로 설정되면 은 추적된 페이지가 https를 통해 제공되었을 때 보안 설정을 사용하도록 쿠키를 설정합니다. |
| useBeaconAPI | 부울 | 기본값은 false입니다. true로 설정되면 는 비콘 API를 사용하여 XMLHttpRequest 대신 비차단 요청을 보냅니다. 브라우저가 이 API를 지원하지 않는 경우 Munchkin은 XMLHttpRequest 사용으로 돌아갑니다. |
| wsInfo | 문자열 | 작업 영역을 타깃팅할 문자열을 가져옵니다. 이 작업 공간 ID는 관리 > 통합 > Munchkin 메뉴에서 작업 공간을 선택하여 가져옵니다. 이 설정은 익명 잠재 고객 레코드의 초기 생성에만 적용됩니다. 해당 잠재 고객 레코드에 대해 Munchkin 쿠키 값이 설정되면 wsInfo 매개 변수를 사용하여 해당 파티션을 변경할 수 없습니다. 이 설정은 익명 리드에만 영향을 주므로 웹 보고서의 파티션 특정 익명 방문자에만 관련이 있습니다. |

## 예시

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

이 예제에서는 모든 XMLHttpRequest가 기본 스레드에서 비동기적으로 전송됩니다.

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
