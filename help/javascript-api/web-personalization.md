---
title: 웹 Personalization
description: 웹 Personalization
feature: Web Personalization, Javascript
exl-id: b2c26b28-e9bf-4faf-8b6e-c102f41aeaa1
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 4%

---

# 웹 Personalization

웹 Personalization JavaScript API는 플랫폼의 자동화된 개인화 기능을 확장합니다. 웹 페이지의 이벤트 추적 및 동적 사용자 지정을 허용합니다. 추가 기능: [사용자 지정 데이터 이벤트](custom-data-events.md), [동적 콘텐츠](web-personalization.md), [방문자 데이터 가져오기](get-visitor-data.md), [특정 봇에 대한 태그 제외](#exclude_tag_for_specific_bots).

- User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- RTP는 계정 기반 마케팅 명명된 계정 목록을 지원하지 않습니다. ABM 목록 및 코드는 RTP 내에서 관리되는 업로드된 계정 목록(CSV 파일)에만 해당됩니다.

## 태그 설정

RTP 태그는 개인화된 페이지의 헤더에 삽입해야 합니다.

```javascript
<!-- RTP tag --> 
<script type='text/javascript'>
(function(c,h,a,f,e,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].p=e;c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b)})
(window,document,"rtp","[rtp-js-cdn-url]","[pod-url]","[accountId]");
</script>
<!-- End of RTP tag -->
```

## 계정 설정

이 메서드는 관련 계정 ID를 설정하기 위해 태그 수준에서 자동으로 호출됩니다. 다른 도메인 간에 분할하려는 경우 계정 ID를 설정할 수 있습니다.

| 매개 변수 | 선택 사항/필수 | 유형 | 설명 |
|--------------|-------------------|--------|--------------|
| &#39;setAccount&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| accountId | 필수 | 문자열 | 계정 ID. |


```javascript
var accountId = '561-HYG-937';
rtp('setAccount', accountId);
```

## 이벤트 전송 기능

이 메서드는 페이지 추적에 사용되는 보기 이벤트를 보냅니다. 아래 예에서 현재 페이지 URL은 방문자 페이지 보기로 추적됩니다.

이 메서드에서 선택적 &quot;page&quot; 매개 변수를 전달하여 현재 페이지를 재정의할 수 있습니다.

| 매개 변수 | 선택 사항/필수 | 유형 | 설명 |
|-----------|-------------------|--------|---------------------------------|
| &#39;보내기&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;보기&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| 페이지 | 선택 사항 | 문자열 | 상대 경로 또는 전체 페이지 URL. |


```javascript
// Example for Default Page
rtp('send', 'view');

// Example for Overriding Default Page
var page = 'my-page?param=1';
rtp('send', 'view', page);
```

## 특정 봇에 대한 태그 제외(사용자 에이전트)

특정 브라우저가 웹 Personalization 플랫폼으로 데이터를 보내지 못하게 하려면(식별된 보트의 경우) 태그 스크립트에 다음 IF 문을 추가합니다.

아래 코드 예제에서 &quot;Googlebot|msnbot&quot;은 웹 Personalization 활동에서 제외하는 봇 예제로 사용됩니다.

```javascript
<!-- RTP tag --> 
<script type='text/javascript'>
if(navigator.userAgent.match(/.(Googlebot|msnbot)./gi) == null){
    (function(c,h,a,f,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
    c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
    g.src=f+'?rh='+c.location.hostname+'&aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//[cdn-pod-X-url]/rtp-api/v1/rtp.js","[accountId]");

    rtp('send','view');
    rtp('get', 'campaign', true);
}
</script>
<!-- End of RTP tag -->
```

## JavaScript 호출 설명

웹 JavaScript 및 예측 콘텐츠를 사용할 때 웹 사이트에 추가되는 Personalization에 대한 설명입니다.

### 코어/종속 JavaScript

| 이름 | 설명 | 제어 |
|---------------------------|-------------|--------------------------------------------------------|
| rtp.js | - | Marketo에 의해 제어됨 |
| jquery.min.js | v1.8.3 | Marketo 고객 지원 센터에 문의하여 비활성화할 수 있습니다. |
| jquery-custom-ui-min.js | v1.9.2 | Marketo 고객 지원 센터에 문의하여 비활성화할 수 있습니다. |
| query-ui-1.8.17-dialog.js | v1.9.2* | Marketo 고객 지원 센터에 문의하여 비활성화할 수 있습니다. |


*jQuery UI에 대화 상자가 없는 경우에만 사용됩니다.

### 온디맨드 JavaScript

| 이름 | 설명 | 제어 |
|-------------------------|-----------------------------------------------------------------------|-----------------------|
| ga-integration-2.0.1.js | Google Analytics/Facebook/SiteCatalyst 통합이 활성화된 경우 사용됨 | Marketo에 의해 제어됨 |
| insightera-bar-2.1.js | 예측 콘텐츠 권장 사항 표시줄이 활성화된 경우 사용됩니다. | Marketo에 의해 제어됨 |
| froogaloop2.min.js | 콘텐츠 추적이 활성화되어 있고 Vimeo 플레이어가 페이지에 있는 경우 사용됩니다. | - |
| iframe-api-v1.js | 컨텐츠 추적이 활성화되어 있고 YouTube 플레이어가 페이지에 있는 경우 사용됩니다. | - |
