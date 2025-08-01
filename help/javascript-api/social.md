---
title: 소셜
description: 소셜
feature: Social, Javascript
exl-id: 82d2b86f-5efe-4434-b617-d27f76515a79
source-git-commit: 981ed9b254f277d647a844803d05a1a2549cbaed
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 2%

---

# 소셜

[Marketo 소셜 마케팅](https://business.adobe.com/products/marketo/social-marketing.html)을 통해 마케터는 웹 사이트 및 랜딩 페이지 내에 소셜 위젯을 포함할 수 있습니다. 소셜 위젯에는 투표, 소셜 공유 버튼, 비디오, 경품 및 추천 오퍼와 같은 프로모션이 포함됩니다.

## 샘플 임베드된 공유 위젯

```html
<!-- Marketo Widget Loader Script -->

<script type="text/javascript" src="//b2c-mlm.marketo.com/jsloader/271d8232-1500-4305-b7ed-05d451b9ee0c/loader.php.js">
</script>

 <!-- The Location of the Social Widget -->

<divclass='cf_widgetloader cf_w_245d8f3c0955454cbd26abc39d0d874c'="" options="{&quot;outerHeight&quot;:400, &quot;outerWidth&quot;:600}">
</divclass='cf_widgetloader'>
```

![소셜 공유 위젯](assets/social-share-widget.png)

소셜 위젯을 사용자 정의하는 기본 방법에는 두 가지가 있습니다.

1. 제품의 일반 UI를 사용하고 이벤트 리스너를 연결하여 UI에서 특정 작업이 발생할 때 알림을 받아 추가 비즈니스 논리를 수행합니다.
1. 제품의 일반 UI를 사용자 정의 UI로 교체하고 원할 경우 UI의 팝업 &quot;단계&quot;를 활성화합니다.

## 일반 UI에 이벤트 첨부

CF JavaScript 라이브러리의 이벤트를 전역적으로 또는 단일 위젯에 가입하는 두 가지 방법이 있습니다. 이벤트는 아래에 이벤트 테이블에 설명되어 있습니다.

### 글로벌 이벤트 구독

```html
<script>
cf_scripts.afterload(function(){
    CF.events.listen("event_name_here",
        function(event, arg1){
            //Your code to do something on the event goes here.
            //It will be fired whenever ANY widget fires the event "event_name_here".
        }
    );
});
</script>
```

### 위젯당 이벤트 구독

```html
<script>
cf_scripts.afterload(function(){
    CF.widget.listen("widget_name_here", "event_name_here",
        function(event, arg1){
            //Your code to do something on the event goes here.
            //It will be fired whenever the widget named "widget_name_here" fires the event "event_name_here".
        }
    );
});
</script>
```

## 예

이 예는 사용자가 &quot;referral_SignUp&quot;이라는 위젯에 대한 오퍼 등록을 완료한 후 ID가 &quot;signedUp&quot;인 이전에 숨겨진 요소를 보여 줍니다.

```html
<div id='signedUp'style='display:none; color:green;'>This is a custom message to let you know that you signed up!</div>
<div class='cf_widgetLoader cf_w_referral_SignUp'></div>

<script>
    cf_scripts.afterload(function(){
        CF.widget.listen("referral_SignUp", "offer_enrolled", function(){
        cf_jq("#signedUp").show();
    });
});
</script>
```

## 기본 이벤트 테이블

| 이벤트 이름 | 설명 | 이 이벤트를 사용하는 위젯 | 지원되는 인수(이벤트 콜백 함수에 전달됨) |
| --- | --- | --- | --- |
| share_sent | 처리를 위해 공유 요청이 서버로 전송될 때마다 실행됩니다 | 공유 권한이 있는 모든 위젯 | 1.&quot;share_sent&quot;(문자열)<br>2. 전송된 매개변수(객체) |
| share_success | 공유 요청이 성공적으로 처리되면 실행됩니다. | 공유 권한이 있는 모든 위젯입니다. | 1.&quot;share_success&quot;(String)<br>2. 보낸 메시지와 단축된 URL이 포함된 응답 개체 공유(개체) |
| 투표 성공 | 사용자가 투표에 성공하면 실행됩니다. | 투표, 투표 위젯 및 투표 위젯 | &#x200B;1. &quot;vote_success&quot;(문자열)<br>2. 제목, 설명, 엔티티 식별자(오브젝트) 등 투표 항목 |
| offer_registered | 사용자가 오퍼에 성공적으로 등록되면 발생합니다. | 모든 오퍼 위젯 | 1.&quot;offer_registered&quot;(String)<br>2. 사용자 속성(개체),<br>3을 변경했습니다. 변경된 사용자 특성(객체) |
| profile_saved | 사용자가 프로필 캡처에서 프로필을 업데이트한 경우 실행됩니다 | 프로필 캡처가 활성화된 모든 비오퍼 위젯 | 1.&quot;profile_saved&quot;(String)<br>2. 사용자 속성(개체)<br>3을 변경했습니다. 변경된 사용자 특성(객체) |
| video_loaded | 포함된 비디오가 완전히 로드되고 초기화될 때 발생합니다. | VideoShare 위젯 | &#x200B;1. &quot;video_loaded&quot; (String) 2. 비디오를 포함하는 &quot;.cf_videoshare_wrap&quot; 요소(jQuery 개체) |

## UI를 사용자 정의 UI로 바꾸기

UI를 사용자 지정 UI로 바꾸려면 먼저 일반 UI를 꺼야 합니다. 이 작업은 _popupUIOnly_ 옵션을 _true_(으)로 설정하여 수행됩니다. 이 옵션을 설정하면 페이지 로드 시 표준 UI가 렌더링되지 않고, 대신 위젯이 데이터를 가져와서 _CF.widget.activate_ 함수를 호출하고 수행해야 할 작업에 대한 옵션을 제공하여 팝업 단계 중 하나를 시작할 때까지 기다립니다.

다음은 _referral_SignUp_(이)라는 레퍼러 오퍼 위젯에 대한 레퍼러 오퍼 등록 플로우를 시작하는 사용자 지정 단추를 만드는 예입니다.

```html
<button id="myNewSignUpButton">My newSign Up button</button>

<!-- Turn off the defaultreferral offer UI by setting popupUIOnly to true-->
<div class="cf_widgetLoader cf_w_referral_SignUp" options="{popupUIOnly:true}"></div>

<script>
cf_scripts.afterload(function($, CF){
    // After the cf script library has loaded, find the button with
    // id="myNewSignUpButton", and attach a click listener to it.
    $("#myNewSignUpButton").click(function(){
        // When it is clicked, activate the popup widget flow for the referral,
        // asking it to point to the clicked button.
        CF.widget.activate("referral_SignUp", {pointTo:$(this)});
    });
});
</script>
```

클릭 처리기를 추가하는 것은 일반적이므로 바로 가기 메서드를 사용하여 추가합니다. 다음은 앞의 예제와 기능적으로 동일합니다.

```html
<button id="myNewSignUpButton">My newSign Up button</button>
<div class="cf_widgetLoader cf_w_referral_SignUp" options="{popupUIOnly:true}"></div>

<script>
cf_scripts.afterload(function($, CF){
    // Use the addClickActivate convenience method, which will
    // automatically make the popup point at the clicked item with id myNewSignUpButton.
    CF.widget.addClickActivate("#myNewSignUpButton", "referral_SignUp", {});
});
</script>
```

## 대체 UI에 배치할 위젯 UI 데이터 가져오기

대체 UI를 그리는 데 위젯에 대한 데이터가 필요한 경우 특수 이벤트 _ui_data_&#x200B;에서 데이터를 가져올 수 있습니다. 일반적인 `CF.widget.listen` 함수를 사용하여 이 이벤트를 수신할 수 있지만, 그렇게 하면 위젯이 이미 _ui_data_ 이벤트를 실행한 후 이벤트 리스너가 추가되어 데이터를 받지 못할 수 있는 경합 상태가 발생할 수 있습니다. 이 경합을 방지하려면 `CF.widget.uiData_ method instead, which will give you the most recent available _ui_data_, and listen for all future updates as well. The _ui_data` 옵션으로 해당 UI를 비활성화했더라도 위젯의 표준 UI가 다시 그려지는 작업을 수행할 때마다 `popupUIOnly` 이벤트가 실행됩니다.

`uiData` 함수를 사용하여 위젯 이름이 _sweeps_Sweepstakes_&#x200B;인 경품 추첨에 대해 사용자가 보유한 항목 수를 표시하는 예입니다.

```html
<span>You have <span id="entryCount">?</span> entries.</span>

<div class="cf_widgetLoader cf_w_sweeps_Sweepstakes"></div>

<button id='myNewSweepsButton'>New Sweeps Up Button!</button>

<script>
cf_scripts.afterload(function($, CF){
    CF.widget.uiData("sweeps_Sweepstakes", function(uiData){
        if(uiData.user && uiData.userStatus && uiData.userEntries){
            $("entryCount").html(""+ uiData.userEntries);
        }
        else{
            $("entryCount").html("0");
        }
    });
});
</script>
```

## 레퍼러 오퍼 등록 UI 데이터 참조

| 유형 | 설명 |
|---------------|----------------------------------------------------|
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

## 레퍼러 오퍼 TrackProgress UI 데이터 참조

| 유형 | 설명 |
|---------------|----------------------------------------------------|
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

## Sweepstakes UI 데이터 참조(LM 경품이 아닌 소셜 캠페인 경품용)

| 유형 | 설명 |
|---------------|----------------------------------------------------|
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

## Social Sign-On(양식 채우기 위젯) 데이터 참조

| 유형 | 설명 |
|---------------|----------------------------------------------------|
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

```javascript
{
"alt_id": "http://www.facebook.com/profile.php?id=1526228678",
"provider_name": "facebook",
"default_photo_url": "https://graph.facebook.com/1526228678/picture?type=large",
"email": "ian.b.taylor@gmail.com",
"verified_email": "ian.b.taylor@gmail.com",
"gender": "male",
"preferred_user_name": "IanTaylor",
"display_name": "Ian Taylor",
"birth_date": 343954800000,
"first_name": "Ian",
"last_name": "Taylor",
"city": null,
"state": null,
"region": null,
"postal_code": null,
"country": null,
"time_zone": null,
"connection_count": 0,
"credentials": {
"uid": "1526228678",
"scopes": "publish_actions",
"expires": "1371994082",
"accessToken": "BAAGFJ0KUFpcBABuNMptmYY...",
"type": "Facebook"
},
"about_me": null,
"cur_pos_title": "Senior Staff Engineer",
"phone_number": null,
"company": "Marketo",
"cur_pos_start_date": 1333231200000,
"cur_pos_summary": null
}
```
