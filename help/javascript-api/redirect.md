---
title: 리디렉션
description: RTP 리디렉션 API를 구현하여 예제와 팁이 있는 ABM, 조직, 위치 및 세그먼트와 같은 필드를 사용하여 분할된 방문자를 타깃팅된 URL로 보냅니다.
feature: Javascript
exl-id: bbf91245-42e5-47ae-a561-e522cc65ff49
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 7%

---

# 리디렉션

RTP Redirect API를 사용하면 분할된 대상을 대상 URL로 리디렉션할 수 있습니다.

- User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- RTP는 계정 기반 마케팅 명명된 계정 목록을 지원하지 않습니다. ABM 목록 및 코드는 RTP 내에서 관리되는 업로드된 계정 목록(CSV 파일)에만 해당됩니다.

## 사용

`rtp('send' , 'redirect' , 'field_name' , [ 'values_array' , '...' , '...' ] , 'www.redirect_url.com' , true/false )`

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---------------------------|-------------------|---------|-----------------------------|
| &#39;보내기&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;리디렉션&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| field_name | 필수 | 문자열 | 일치시킬 필드 이름. 예: &#39;abm.name&#39;(아래 참조) |
| values_array | 필수 | 배열 | 필드와 일치시킬 값 목록(대/소문자 구분 안 함). |
| redirect_url | 필수 | 문자열 | 조건에 일치하는 방문자를 리디렉션할 대상 URL. |
| redirect_matched_visitors | 선택 사항입니다 | 부울 | true인 경우 일치하는 방문자 조건이 리디렉션됩니다. false인 경우 일치하지 않는 방문자 조건이 리디렉션됩니다. 기본값: true. |

조직, 업계, ABM 목록, 위치, ISP, 일치하는 세그먼트

| 조건 | 데이터 계층 | 예 |
|-------------------------------------------------|----------------------|------------------------------------------------------------------------------------------------------------------|
| 일치하는 세그먼트(첫 번째 클릭 후에만 작동) | matchedSegments.name | rtp(&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.name&#39; , [&#39;Fortune 1,000&#39; , &#39;Enterprise&#39;] , &#39;<http://www.marketo.com>&#39;); |
| 일치하는 세그먼트(첫 번째 클릭 후에만 작동) | matchedSegments.id | rtp(&#39;send&#39;, &#39;redirect&#39; , &#39;matchedSegments.id&#39; , [106 , 107 , 190] , &#39;<http://www.marketo.com>&#39;); |
| ABM 목록 | abm.name | rtp(&#39;send&#39;, &#39;redirect&#39; , &#39;abm.name&#39; , [&#39;top_key_accounts&#39;, &#39;active_customers&#39;] , &#39;<http://www.marketo.com>&#39;); |
| ABM 목록 | abm.code | rtp(&#39;send&#39;, &#39;redirect&#39; , &#39;abm.code&#39; , [13 , 15] , &#39;<http://www.marketo.com>&#39;); |
| 조직 | org | rtp(&#39;send&#39;, &#39;redirect&#39;, &#39;org&#39;, [&#39;ebay&#39;], &#39;<http://www.marketo.com>&#39;); |
| 위치 | location.country | rtp(&#39;send&#39;, &#39;redirect&#39;, &#39;location.country&#39;, [&#39;United States&#39;], &#39;<http://www.marketo.com>&#39;); |
| 위치 | location.state | rtp(&#39;send&#39;, &#39;redirect&#39;, &#39;location.state&#39;, [&#39;ca&#39;], &#39;<http://www.marketo.com>&#39;); |
| 위치 | location.city | rtp(&#39;send&#39;, &#39;redirect&#39;, &#39;location.city&#39;, [&#39;San Mateo&#39;], &#39;<http://www.marketo.com>&#39;); |
| 산업 | 업종 | rtp(&#39;send&#39;, &#39;redirect&#39; , &#39;industries&#39; , [&#39;Education&#39;], &#39;<http://www.marketo.com>&#39;); |
| ISP | isp | rtp(&#39;send&#39;, &#39;redirect&#39; , isp , [&#39;False&#39;], &#39;<http://www.marketo.com>&#39;); |

## 참고

- 리디렉션 규칙/조건이 Firmographics(회사, 업계, 위치)를 기반으로 하는 경우 rtp(&#39;send&#39;, &#39;view&#39;) 및 rtp(&#39;get&#39;, &#39;campaign&#39;) 앞에 리디렉션 코드를 삽입하여 지연을 줄일 수 있습니다.
- JavaScript을 통한 리디렉션은 브라우저측 리디렉션이며 최대 속도에 도달하기 위한 웹 사이트의 로드 및 최적화에 따라 다릅니다.
- 가장 좋은 방법은 rtp 태그 바로 뒤에 리디렉션 코드를 설정하여 헤더에 배치하는 것입니다.
- 자체 리디렉션을 실행하고 있지 않은지 확인합니다(rtp에 순환 리디렉션 호출을 차단하는 안전 네트워크가 있음).

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<!-- RTP tag -->
<script type='text/javascript'>

// This tag needs to be replaced with your account tag
(function(c,h,a,f,i){c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
c[a].a=i;var g=h.createElement("script");g.async=true;g.type="text/javascript";
g.src=f+'?rh='+c.location.hostname+'&aid='+i;var b=h.getElementsByTagName("script")[0];b.parentNode.insertBefore(g,b);
})(window,document,"rtp","//xyz.marketo.com/rtp-api/v1/rtp.js","xyz");

// START REDIRECT EXAMPLE
//   - Using a helper redirect function
//   - Redirect based on named account
rtp('send','redirect','org', ['microsoft'],'http://www.marketo.com');

// Redirect based on named account list (ABM)
rtp('send','redirect','abm.name', {
    // Redirect visitors that match 'first_abm' list to www.marketo.com
    'http://www.marketo.com' : ['first_abm'],
    // Redirect visitors that match 'second_abm' list to blog.marketo.com
    'http://blog.marketo.com' : ['second_abm']
});
// END REDIRECT EXAMPLE
rtp('send','view');
rtp('get','campaign');
</script>
<!-- End of RTP tag -->
```

## 추적된 방문자를 리디렉션하는 방법

1. 대상 URL 끝에 매개 변수를 추가합니다. 즉, &lt;www.marketo.com?rtp=redirect>
1. 라는 세그먼트 만들기 - &quot;RTP에 의해 리디렉션됨&quot;
1. 아래 표시된 매개 변수로 페이지를 보는 방문자를 타깃팅하려면 &#39;특정 페이지&#39; 매개 변수를 사용하십시오.

![추적-리디렉션된 방문자](assets/tracking-redirected-vistors.png)

## 서로 다른 대상 URL을 사용하여 두 개 이상의 조건을 정의하는 방법

리디렉션 호출은 여러 호출을 지원합니다. 이렇게 하면 여러 필드로 리디렉션하고 다른 URL 및 값으로 복잡한 조건을 만들 수 있습니다.

### 사용

`rtp('send', 'redirect', field_name, url_values_map);`

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| &#39;보내기&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;리디렉션&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| field_name | 필수 | 문자열 | 일치시킬 필드 이름. 예: &#39;abm.name&#39; (위 참조) |
| url_values_map | 필수 | 오브젝트 | 리디렉션 URL과 값 목록 간에 매핑합니다. 예:{&#39;<http://marketo.com>&#39; : [&#39;first_abm&#39;, &#39;second_abm&#39;]} |

#### 예

```javascript
rtp('send','redirect','abm.name', {
    // Redirect visitors that match 'first_abm' list to www.marketo.com
    'http://www.marketo.com' : ['first_abm'],
    // Redirect visitors that match 'second_abm' list to blog.marketo.com
    'http://blog.marketo.com' : ['second_abm']
});
rtp('send','redirect','org', {
    // Redirect visitors from 'Microsoft' to www.marketo.com/enterprise
    'http://www.marketo.com/enterprise' : ['microsoft']
});
```
