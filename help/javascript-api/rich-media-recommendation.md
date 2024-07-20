---
title: 리치 미디어 권장 사항
description: 리치 미디어 권장 사항
feature: Javascript
exl-id: ee92e46d-e529-40a2-a0d0-ee233916f004
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 3%

---

# 리치 미디어 권장 사항

리치 미디어 권장 사항 템플릿을 표시할 페이지에서 다음 태그 및 API 호출을 설정해야 합니다.

1. 페이지 머리글에서
   1. RTP 태그가 설치되어 있습니다.
   1. GET 호출을 페이지에 추가하여 권장 사항을 채웁니다
   1. SET 호출을 추가하여 템플릿 구성
1. 페이지 본문에서
   1. 템플릿을 표시할 위치에 템플릿 태그(div 클래스)를 배치합니다

자세한 내용은 [여기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/predictive-content/enabling-predictive-content/enable-predictive-content-for-web-rich-media)를 참조하세요.

## 템플릿 태그

| 속성 | 선택 사항/필수 | 설명 |
|---|---|---|
| 클래스 | 필수 | 이 div HTML 요소가 RTP 권장 div라고 지정합니다. |
| data-rtp-template-id | 필수 | 템플릿 ID입니다. 이렇게 하면 권장 사항의 맞춤이 결정됩니다. 가로 정렬에는 &quot;template1&quot;, 세로 정렬에는 &quot;template2&quot; 또는 제목과 설명만 포함하는 세로 정렬에는 &quot;template3&quot;을 사용합니다. 스크립트는 이 `div.Permissible` 값(template1, template2, template3)에 일치하는 템플릿을 삽입합니다. |

### 예시

권장 사항을 수평 정렬로 표시하려면 &quot;template1&quot;을 사용합니다.

```html
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
```

권장 사항을 세로 정렬로 표시하려면 &quot;template2&quot;를 사용합니다.

```html
<div class="RTP_RCMD2" data-rtp-template-id="template2"></div>
```

권장 사항을 제목과 설명만 세로로 정렬하여 표시하려면 &quot;template3&quot;을 사용합니다.

```html
<div class="RTP_RCMD2" data-rtp-template-id="template3"></div>
```

템플릿 정렬의 스크린샷을 [여기](#example_of_rich_media_recommendation_template_1)에서 확인하세요.

## 권장 사항 채우기

이 메서드는 페이지의 모든 리치 미디어 `<divs>`을(를) 권장 사항으로 채웁니다.

### 사용량

`rtp('get', 'rcmd', 'richmedia');`

| 매개 변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| &#39;get&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;rcmd&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| &#39;richmedia&#39; | 필수 | 문자열 | 하위 메서드 이름. |


## 템플릿 구성 변경

이 메서드는 템플릿에 대한 기본 구성을 변경합니다.

참고: 이 메서드를 사용할 때는 rtp(&#39;get&#39;,&#39;rcmd&#39;, &#39;richmedia&#39;)를 호출하기 전에 호출해야 합니다.

### 사용량

`rtp('set', 'rcmd', 'richmedia', 'template_id', conf_obj);`

| 매개 변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| &#39;설정&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;rcmd&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| &#39;richmedia&#39; | 필수 | 문자열 | 하위 메서드 이름. |
| template_id | 선택 사항 | 문자열 | 구성 변경에 대한 템플릿 ID입니다. 한 템플릿에 대한 설정 변경 사항을 지정하는 데 사용합니다. |
| conf_obj | 필수 | 오브젝트 | 새 구성. 개체에는 모든 구성이 키/값 쌍으로 저장됩니다. |


### 예시

이 코드 조각은 템플릿의 제목 텍스트를 변경합니다.

```javascript
rtp("set", "rcmd", "richmedia","template1",
    {
        "rcmd.title.text": "RECOMMENDED CONTENT"
    }
);
```

이 코드 조각은 템플릿에 대한 여러 구성이 있는 범주 설정을 보여 줍니다.

```javascript
rtp("set", "rcmd", "richmedia",
    {
        "template1": 
        {
            "rcmd.title.text": "RECOMMENDED CONTENT",
            "rcmd.general.font.family": "arial",
            "category":
            [
                "webinar",
                "blog posts",
                "pricing_page_category",
                "product_a_category"
            ]
        }
    }
);
```

참고: &quot;범주&quot;를 사용하여 예측 콘텐츠 권장 사항의 결과에 표시되는 콘텐츠를 필터링합니다. 활성화된 모든 콘텐츠 조각에 예측 콘텐츠를 적용하려면 &quot;범주&quot;를 비워 둡니다. 리치 미디어 템플릿의 출력에 대해 특정 콘텐츠만 추천하려면 콘텐츠 설정 페이지에서 콘텐츠에 대한 범주를 추가하고 권장 템플릿 코드 내에서 해당 범주를 연결합니다. 웹 사이트(제품 또는 솔루션)의 섹션에 따라 관련 컨텐츠를 분류합니다.

이 코드 조각은 템플릿에 대한 여러 템플릿 구성 설정을 보여 줍니다.

```javascript
rtp("set", "rcmd", "richmedia",
    {
        "template1":
        {
            "rcmd.title.text": "RECOMMENDED CONTENT",
            "rcmd.general.font.family": "arial"
        }
    }
);
```

#### 구성 속성

| 구성 | 예 | 설명 |
|---|---|---|
| rcmd.general.font.family | &quot;rcmd.general.font.family&quot; : &quot;arial&quot; | 템플릿의 모든 텍스트에 대한 글꼴 모음을 변경합니다. 이 속성은 브라우저 유형별로 모든 CSS 값을 지원합니다. 사용자 정의 글꼴 패밀리가 페이지에 있는 경우 이를 사용할 수 있습니다. |
| rcmd.content.background.color | &quot;rcmd.content.background.color&quot; : &quot;black&quot; | 템플릿 내부 상자의 배경색을 변경합니다. 이 속성은 브라우저 유형별로 모든 CSS 값을 지원합니다. |
| rcmd.title.text | &quot;rcmd.title.text&quot; : &quot;권장 컨텐츠&quot; | 템플릿 제목을 변경합니다. |
| rcmd.title.background.color | &quot;rcmd.title.background.color&quot; : &quot;blue&quot; | 제목 상자 배경색을 변경합니다. 이 속성은 모든 css 색상 값(색상 이름, rgb, ...)을 지원합니다. |
| rcmd.title.font.size | &quot;rcmd.title.font.size&quot; : &quot;26px&quot; | 제목 글꼴 크기를 변경합니다. 속성은 가능한 모든 글꼴 크기 CSS 값(px, em, ...)을 지원합니다. |
| rcmd.title.font.color | &quot;rcmd.title.font.color&quot; : &quot;white&quot; | 제목 글꼴 색상을 변경합니다. 이 속성은 모든 글꼴 색상 값(rgb, hex, ...)을 지원합니다. |
| rcmd.description.font.color | &quot;rcmd.description.font.color&quot; : &quot;white&quot; | 설명 글꼴 색상을 변경합니다. 이 속성은 모든 글꼴 색상 값(rgb, hex, ...)을 지원합니다. |
| rcmd.cta.background.color | &quot;rcmd.cta.background.color&quot; : &quot;녹색&quot; | 단추 배경색을 변경합니다. 이 속성은 모든 css 색상 값(색상 이름, rgb, ...)을 지원합니다. |
| rcmd.cta.font.color | &quot;rcmd.cta.font.color&quot; : &quot;rgb(90, 84, 164)&quot; | 단추 글꼴 색상을 변경합니다. 이 속성은 모든 글꼴 색상 값(rgb, hex, ...)을 지원합니다. |
| rcmd.cta.text | &quot;rcmd.cta.text&quot; : &quot;푸시&quot; | 단추 텍스트를 변경합니다. 텍스트는 모든 단추에 대해 동일합니다. |
| 범주 | &quot;category&quot; : [&quot;one category&quot;] | 이 템플릿이 지원하는 권장 사항 범주를 변경합니다. 템플릿에는 이 구성에 의해 설정된 카테고리 중 하나가 있는 권장 사항만 표시됩니다. |


참고: 구성 지원은 템플릿별로 변경될 수 있습니다.

#### 기본 예

이 예에는 세 개의 권장 사항이 있는 한 개의 템플릿이 있습니다. 이 예제를 HTML 페이지에 복사한 다음 RTP 태그를 태그로 바꿉니다.

```html
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>RTP recommendation</title>
<!-- RTP tag --> 
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i,e){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;c[a].e=e;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//example.rtp.com/rtp-api/v1/rtp.js","account_id");

// Send page view (required by  the recommendation)
rtp('send','view');
// Populate recommendation
rtp('get','rcmd', 'richmedia');
</script>
<!-- End of RTP tag -->
</head>
<body>
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
</body>
</html>
```

#### 고급 예

이 예에는 세 개의 권장 사항이 있는 한 개의 템플릿이 있습니다. 템플릿 제목은 &quot;권장 콘텐츠&quot;이고 버튼 텍스트는 &quot;자세히 읽기&quot;입니다. 이 예제를 HTML 페이지에 복사한 다음 RTP 태그를 태그로 바꿉니다.

```html
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>RTP recommendation</title>
<!-- RTP tag --> 
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i,e){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;c[a].e=e;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//example.rtp.com/rtp-api/v1/rtp.js","account_id");

// Send page view (required by  the recommendation)
rtp('send','view');
// Populate the recommendation zone
rtp('get', 'campaign',true);
// Change template configuration
rtp('set', 'rcmd', 'richmedia',
    {
        template1 :
        {
            "rcmd.title.text" : "RECOMMENDED CONTENT",
            "rcmd.cta.text" : "Read More"
        }
    }
);
// Populate recommendation
rtp('get','rcmd', 'richmedia');
</script>
<!-- End of RTP tag -->
</head>
<body>
<div class="RTP_RCMD2" data-rtp-template-id="template1"></div>
</body>
</html>
```

#### 리치 미디어 추천 템플릿 #1의 예

**이름**: template1 **설명**: 이미지, 제목, 설명 및 콜 투 액션 단추를 포함하는 가로 콘텐츠.

![리치 미디어 템플릿](assets/rich-media-template1.png)

#### 리치 미디어 추천 템플릿 #2의 예

**이름**: template2 **설명**: 이미지, 제목, 설명 및 콜 투 액션 단추를 포함하는 세로 콘텐츠

![리치 미디어 템플릿](assets/rich-media-template2.png)

#### 리치 미디어 추천 템플릿 #3의 예

**이름**: template3 **설명**: 제목과 설명만 포함하는 세로 콘텐츠 마우스를 가져가면 헤더가 색상을 변경하고 콘텐츠 URL에 하이퍼링크됩니다. 설명 또한 색상을 변경하지 않은 콘텐츠에 대한 링크입니다. ![리치 미디어 템플릿](assets/rich-media-template3.png)
