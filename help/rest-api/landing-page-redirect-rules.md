---
title: 랜딩 페이지 리디렉션 규칙
feature: REST API, Landing Pages
description: API를 통해 랜딩 페이지 리디렉션 규칙을 구성합니다.
exl-id: f63aa5ef-5872-4401-be75-6fb9b2977734
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 2%

---

# 랜딩 페이지 리디렉션 규칙

[랜딩 페이지 리디렉션 규칙 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules)

Marketo은 랜딩 페이지 리디렉션 URL에서 CRUD 작업을 수행하기 위한 REST API 세트를 제공합니다. 이러한 API는 쿼리, 만들기, 업데이트 및 삭제 옵션을 제공하는 에셋 API에 대한 표준 인터페이스 패턴을 따릅니다.

랜딩 페이지 리디렉션 규칙은 랜딩 페이지 URL을 다른 페이지 URL로 리디렉션하는 기능을 제공합니다. Marketo 랜딩 페이지, Marketo이 아닌 랜딩 페이지 또는 이들의 조합을 리디렉션할 수 있습니다. 리디렉션 랜딩 페이지 규칙에 대한 추가 정보는 [여기](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ko)에서 확인할 수 있습니다.

## 쿼리

랜딩 페이지 리디렉션 규칙 쿼리는 [ID](#by_id) 및 [검색](#browse)의 자산에 대한 표준 쿼리 형식을 따릅니다.

### ID별

[ID별 랜딩 페이지 리디렉션 규칙 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET) 끝점은 단일 랜딩 페이지 규칙 리디렉션 `id` 경로 매개 변수를 사용하고 단일 랜딩 페이지 리디렉션 규칙 레코드를 반환합니다.

```
GET /rest/asset/v1/redirectRule/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "3d0#1707b2521e4",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5559
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage2.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T06:56:44Z+0000"
        }
    ]
}
```

### 찾아보기

[랜딩 페이지 리디렉션 규칙 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET) 끝점이 랜딩 페이지 리디렉션 규칙 레코드 목록을 반환합니다.

필터 결과로 전달할 수 있는 몇 가지 선택적 쿼리 매개 변수가 있습니다.

`offset` 매개 변수는 반환할 최대 항목 수를 지정하는 정수입니다(기본값은 20). 최대값은 200입니다. `maxReturn` 매개 변수는 항목 검색을 시작할 위치를 지정하는 정수입니다. offset과 함께 사용할 수 있습니다(기본값은 0).

`hostname` 매개 변수를 사용하여 랜딩 페이지의 호스트 이름을 필터링할 수 있습니다.

`redirectToLandingPageId`은(는) 리디렉션하는 랜딩 페이지의 ID를 필터링하는 데 사용할 수 있는 정수입니다. `redirectToPath`을(를) 사용하여 리디렉션하는 랜딩 페이지의 경로를 필터링할 수 있습니다.

`earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수를 사용하면 지정된 범위 내에서 업데이트되었거나 처음에 만들어진 랜딩 페이지 리디렉션 규칙을 반환하기 위한 낮음 및 높은 날짜/시간 워터마크를 설정할 수 있습니다.

```
GET /rest/asset/v1/redirectRules.json&maxReturn=3
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "12213#1707b27efb5",
    "warnings": [],
    "result": [
        {
            "id": 5,
            "redirectFromUrl": "https://www.kirtideep.contact/LandingPage2.html",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5406
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectToUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "createdAt": "2019-11-14T06:26:29Z+0000",
            "updatedAt": "2019-11-14T06:26:29Z+0000"
        },
        {
            "id": 6,
            "redirectFromUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectTo": {
                "type": "url",
                "value": "www.contactLogs.com"
            },
            "redirectToUrl": "www.contactLogs.com",
            "createdAt": "2019-11-14T06:27:10Z+0000",
            "updatedAt": "2019-11-14T06:27:10Z+0000"
        },
        {
            "id": 7,
            "redirectFromUrl": "https://www.kirtideep.contact/contact/log/check",
            "hostname": "www.kirtideep.contact",
            "redirectFrom": {
                "type": "path",
                "value": "/contact/log/check"
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5404
            },
            "redirectToUrl": "https://www.kirtideep.contact/www.showLogs.com.html",
            "createdAt": "2019-11-14T06:27:49Z+0000",
            "updatedAt": "2019-11-14T06:27:49Z+0000"
        }
    ]
}
```

## 만들기

[랜딩 페이지 리디렉션 규칙 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST) 끝점은 다음 세 가지 필수 매개 변수가 있는 application/x-www-form-urlencoded POST로 실행됩니다.

`hostname` 매개 변수는 랜딩 페이지의 호스트 이름을 지정합니다. 브랜딩 도메인 또는 별칭에 속해야 합니다. 최대 길이는 255자입니다.

`redirectFrom` 매개 변수는 원본 랜딩 페이지를 지정합니다. 소스가 Marketo 랜딩 페이지인지 또는 Marketo이 아닌 랜딩 페이지인지를 결정하는 유형/값 쌍을 포함하는 JSON 개체입니다. `type` 특성은 &quot;landingPageId&quot; 또는 &quot;path&quot;일 수 있습니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| &#39;get&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;visitor&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| callback | 필수 | 함수 | 반환된 각 캠페인에 대해 트리거될 콜백 함수입니다. |

`redirectTo` 매개 변수는 대상 랜딩 페이지를 지정합니다. 소스가 Marketo 랜딩 페이지인지 또는 Marketo이 아닌 랜딩 페이지인지를 결정하는 유형/값 쌍을 포함하는 JSON 개체입니다. `type` 특성은 &quot;landingPageId&quot; 또는 &quot;url&quot;일 수 있습니다.

| 랜딩 페이지 유형 | redirectTo 유형 | 예 |
|---|---|---|
| Marketo | 랜딩 페이지 ID | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| 비 Marketo | url | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

랜딩 페이지 리디렉션 규칙을 만드는 방법에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html)에서 확인할 수 있습니다.

```
POST /rest/asset/v1/redirectRules.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
hostname=calqeauto.com&redirectFrom={"type":"landingPageId", "value":"5483"}&redirectTo={"type":"landingPageId", "value":"5559"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d7c6#1707b223522",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5559
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage2.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T06:56:44Z+0000"
        }
    ]
}
```

## 업데이트

[랜딩 페이지 리디렉션 규칙 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST) 끝점은 하나의 랜딩 페이지 리디렉션 규칙 `id` 경로 매개 변수를 사용합니다. 이 끝점은 application/x-www-form-urlencoded POST로 실행됩니다.

위에서 설명한 만들기 호출과 마찬가지로, 업데이트할 규칙의 특성을 지정하기 위해 하나 이상의 쿼리 매개 변수가 전달됩니다. `hostname`, `redirectFrom`, `redirectTo`.

업데이트된 랜딩 페이지 리디렉션 규칙 레코드가 응답에서 반환됩니다.

```
POST /rest/asset/v1/redirectRule/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
redirectTo={"type":"landingPageId", "value":"5561"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "57b2#1707b3852d7",
    "warnings": [],
    "result": [
        {
            "id": 20,
            "redirectFromUrl": "https://calqeauto.com/DefDelPro1_LandingPage1.html",
            "hostname": "calqeauto.com",
            "redirectFrom": {
                "type": "landingPageId",
                "value": 5483
            },
            "redirectTo": {
                "type": "landingPageId",
                "value": 5561
            },
            "redirectToUrl": "https://calqeauto.com/DefDelPro1_LandingPage3.html",
            "createdAt": "2020-02-25T06:56:44Z+0000",
            "updatedAt": "2020-02-25T07:20:53Z+0000"
        }
    ]
}
```

## 삭제

[ID별 랜딩 페이지 리디렉션 규칙 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST) 끝점은 하나의 랜딩 페이지 규칙 리디렉션 `id` 경로 매개 변수를 사용합니다.

```
POST /rest/asset/v1/redirectRule/{id}/delete.json
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "d505#154d01c8364",
  "result": [
    {
      "id": 2
    }
  ]
}
```

## 랜딩 페이지 도메인 찾아보기

[랜딩 페이지 도메인 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET) 끝점이 랜딩 페이지 도메인 레코드 목록을 반환합니다.

필터 결과에 전달할 수 있는 두 개의 선택적 쿼리 매개 변수가 있습니다.

`offset` 매개 변수는 반환할 최대 항목 수를 지정하는 정수입니다(기본값은 20이고, 최대값은 200임).

`maxReturn` 매개 변수는 항목 검색을 시작할 위치를 지정하는 정수입니다. `offset`과(와) 함께 사용할 수 있습니다(기본값은 0).

```
POST /rest/asset/v1/landingPageDomains.json?maxReturn=3
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "6eb8#1707b43d3cb",
    "warnings": [],
    "result": [
        {
            "hostname": "calqeauto.com",
            "type": "domain"
        },
        {
            "hostname": "www.google.com",
            "type": "domain-alias"
        },
        {
            "hostname": "www.kirti.com",
            "type": "domain-alias"
        }
    ]
}
```
