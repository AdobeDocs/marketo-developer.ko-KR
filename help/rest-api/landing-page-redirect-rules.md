---
title: 랜딩 페이지 리디렉션 규칙
feature: REST API, Landing Pages
description: Marketo Asset REST API를 사용하여 필터, 페이지 매김, 호스트 이름 옵션, Marketo 이외의 타겟으로 랜딩 페이지 리디렉션 규칙을 만들고, 쿼리하고, 업데이트하고, 삭제합니다.
exl-id: f63aa5ef-5872-4401-be75-6fb9b2977734
TQID: https://experienceleague.adobe.com/2gePbKA3xeoRdnL8mNnObN-GPTX00Ii4-zcM0lBjs-o
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 626
ht-degree: 3%

---

# 랜딩 페이지 리디렉션 규칙

[랜딩 페이지 리디렉션 규칙 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules)

랜딩 페이지 리디렉션 규칙 REST API를 사용하여 랜딩 페이지 리디렉션 URL을 쿼리, 만들기, 업데이트 및 삭제합니다.

리디렉션 규칙은 한 랜딩 페이지 URL을 다른 페이지 URL로 보냅니다. 소스 및 대상은 Marketo 또는 Marketo이 아닌 페이지일 수 있습니다. 관련 제품 설명서는 [Marketo Engage 설명서](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하세요.

## 쿼리

ID[&#128279;](#by_id) 또는 [검색](#browse)별 랜딩 페이지 리디렉션 규칙을 쿼리합니다.

### ID별

[ID별 랜딩 페이지 리디렉션 규칙 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRuleByIdUsingGET) 끝점은 하나의 리디렉션 규칙 `id` 경로 매개 변수를 사용하고 일치하는 레코드를 반환합니다.

```http
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

[랜딩 페이지 리디렉션 규칙 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageRedirectRulesUsingGET) 끝점이 랜딩 페이지 리디렉션 규칙 레코드를 반환합니다.

선택적 쿼리 매개 변수를 사용하여 결과를 필터링합니다.

`offset` 매개 변수는 반환할 최대 항목 수를 지정하는 정수입니다(기본값은 20). 최대값은 200입니다. `maxReturn` 매개 변수는 항목 검색을 시작할 위치를 지정하는 정수입니다. offset과 함께 사용할 수 있습니다(기본값은 0).

`hostname` 매개 변수는 랜딩 페이지 호스트 이름별로 필터링합니다.

`redirectToLandingPageId` 정수는 대상 랜딩 페이지 ID를 기준으로 필터링합니다. `redirectToPath` 매개 변수는 대상 랜딩 페이지 경로를 기준으로 필터링합니다.

`earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수는 낮음 및 높음 날짜-시간 경계를 설정합니다. 끝점은 범위 내에서 생성되거나 업데이트된 규칙을 반환합니다.

```http
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

`application/x-www-form-urlencoded` POST 요청으로 [랜딩 페이지 리디렉션 규칙 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/createLandingPageRedirectRuleUsingPOST) 끝점을 호출합니다. 요청에는 세 개의 필수 매개 변수가 있습니다.

`hostname` 매개 변수는 랜딩 페이지 호스트 이름을 지정합니다. 브랜딩 도메인 또는 별칭에 속해야 하며 255자를 초과할 수 없습니다.

`redirectFrom` 매개 변수는 소스 랜딩 페이지를 유형/값 쌍을 가진 JSON 개체로 지정합니다. `type` 특성은 Marketo 랜딩 페이지의 경우 `landingPageId`일 수 있고, Marketo이 아닌 페이지의 경우 `path`일 수 있습니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| &#39;get&#39; | 필수 | 문자열 | 메서드 작업. |
| &#39;visitor&#39; | 필수 | 문자열 | 메서드 이름입니다. |
| callback | 필수 | 함수 | 반환된 각 캠페인에 대해 트리거될 콜백 함수입니다. |

`redirectTo` 매개 변수는 유형/값 쌍을 가진 JSON 개체로 대상을 지정합니다. `type` 특성은 Marketo 랜딩 페이지의 경우 `landingPageId`일 수 있고, Marketo이 아닌 페이지의 경우 `url`일 수 있습니다.

| 랜딩 페이지 유형 | redirectTo 유형 | 예 |
| --- | --- | --- |
| Marketo | 랜딩 페이지 ID | {&quot;type&quot;:&quot;landingPageId&quot;,&quot;value&quot;:&quot;1774&quot;} |
| 비 Marketo | url | {&quot;type&quot;:&quot;url&quot;,&quot;value&quot;:&quot;www.contactLogs.com&quot;} |

자세한 내용은 [다른 페이지로 Marketo 랜딩 페이지 리디렉션](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-actions/redirect-a-marketo-landing-page-to-another-page.html?lang=ko)을 참조하십시오.

```http
POST /rest/asset/v1/redirectRules.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[랜딩 페이지 리디렉션 규칙 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/updateLandingPageRedirectRuleUsingPOST) 끝점은 하나의 리디렉션 규칙 `id` 경로 매개 변수를 사용합니다. `application/x-www-form-urlencoded` POST 요청으로 업데이트를 보냅니다.

다음 매개 변수 중 하나 이상을 전달하여 업데이트할 특성을 선택하십시오. `hostname`, `redirectFrom` 또는 `redirectTo`.

응답은 업데이트된 리디렉션 규칙 레코드를 반환합니다.

```http
POST /rest/asset/v1/redirectRule/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

ID별 [랜딩 페이지 리디렉션 규칙 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/deleteLandingPageRedirectRuleUsingPOST) 끝점은 하나의 리디렉션 규칙 `id` 경로 매개 변수를 사용합니다.

```http
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

[랜딩 페이지 도메인 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Redirect-Rules/operation/getLandingPageDomainsUsingGET) 끝점이 랜딩 페이지 도메인 레코드를 반환합니다.

두 개의 선택적 쿼리 매개 변수를 사용하여 결과를 필터링합니다.

`offset` 매개 변수는 반환할 최대 항목 수를 지정하는 정수입니다(기본값은 20이고, 최대값은 200임).

`maxReturn` 매개 변수는 항목 검색을 시작할 위치를 지정하는 정수입니다. `offset`과(와) 함께 사용할 수 있습니다(기본값은 0).

```http
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
