---
title: 랜딩 페이지
feature: REST API, Landing Pages
description: Marketo REST API를 사용하여 안내식 및 자유 형식 유형을 비롯한 랜딩 페이지를 쿼리하고, 만들고, 업데이트하고, 승인하고, 삭제하고, 복제합니다.
exl-id: 2f986fb0-0a6b-469f-b199-1c526cd5a882
TQID: https://experienceleague.adobe.com/NssOtB6BEMGOQzzauLI7AszLpN3fVcEeJcr9VNTkpJE
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 917
ht-degree: 2%

---

# 랜딩 페이지

[랜딩 페이지 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages)

랜딩 페이지는 Marketo에서 호스팅하는 웹 페이지입니다. 랜딩 페이지 REST API를 사용하여 메타데이터, 콘텐츠, 라이프사이클 및 미리보기를 쿼리하고 관리합니다.

## 쿼리

[이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/getLandingPageByNameUsingGET), [ID별](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/getLandingPageByIdUsingGET) 또는 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/browseLandingPagesUsingGET)별로 랜딩 페이지를 쿼리합니다. 이러한 쿼리는 메타데이터만 반환합니다. 랜딩 페이지의 콘텐츠 섹션을 페이지 ID별로 별도로 쿼리합니다.

랜딩 페이지 콘텐츠를 쿼리하면 사용 가능한 콘텐츠 섹션이 반환됩니다. 업데이트하려면 먼저 섹션이 이 목록에 표시되어야 합니다.

```http
GET /rest/asset/v1/landingPage/{id}/content.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "6307#154ea1689d7",
    "result": [
        {
            "id": "67",
            "type": "Form",
            "index": 1,
            "content": {
                "content": "189",
                "contentType": "Form",
                "contentUrl": "https://app-devlocal1.marketo.com/#FO189A1ZN13LA1"
            },
            "formattingOptions": {
                "zIndex": 15,
                "left": "359px",
                "top": "122px"
            }
        }
    ]
}
```

안내식 랜딩 페이지에는 템플릿으로 정의된 섹션이 포함됩니다. 자유 형식 페이지에는 사전 정의된 섹션이 없으므로 편집하기 전에 해당 콘텐츠를 추가하십시오.

`content` 특성의 형식은 `type` 특성과 필드가 정적인지 또는 동적인지에 따라 다릅니다.

## 만들기 및 업데이트

템플릿에서 [랜딩 페이지 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/createLandingPageUsingPOST). 페이지 이름, 템플릿 ID 및 대상 폴더가 필요합니다. 선택적 메타데이터에 대해서는 끝점 참조를 참조하십시오.

[랜딩 페이지 콘텐츠](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content) 끝점은 다음 콘텐츠 형식을 지원합니다. `richText`, `HTML`, `Form`, `Image`, `Rectangle` 및 `Snippet`.

```http
POST rest/asset/v1/landingPages.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=createLandingPage&folder={"type": "Folder", "id": 11}&template=1&description=this is a test&workspace=default&title=test create&keywords=awesome&formPrefill=false
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "7a39#154cf7922c6",
    "result": [
        {
            "id": 27,
            "name": "createLandingPage",
            "description": "this is a test",
            "createdAt": "2016-05-20T18:41:43Z+0000",
            "updatedAt": "2016-05-20T18:41:43Z+0000",
            "folder": {
                "type": "Folder",
                "value": 11,
                "folderName": "Landing Pages"
            },
            "workspace": "Default",
            "status": "draft",
            "template": 1,
            "title": "test create",
            "keywords": "awesome",
            "robots": "index, nofollow",
            "formPrefill": false,
            "mobileEnabled": false,
            "URL": "https://app-devlocal1.marketo.com/lp/622-LME-718/createLandingPage.html",
            "computedUrl": "https://app-devlocal1.marketo.com/#LP27B2"
        }
    ]
}
```

랜딩 페이지 메타데이터는 [랜딩 페이지 메타데이터 끝점 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/updateLandingPageUsingPOST)로 업데이트할 수 있습니다.

## 승인

랜딩 페이지는 표준 초안 및 승인된 모델을 사용합니다. 업데이트는 초안에 적용되며 승인 후에만 활성화됩니다.

## 삭제

랜딩 페이지를 삭제하기 전에 승인되지 않았는지, 다른 Marketo 에셋이 이를 참조하지 않는지 확인하십시오. [랜딩 페이지 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/deleteLandingPageByIdUsingPOST) 끝점을 사용하여 개별적으로 페이지를 삭제합니다. 이 API를 사용하여 포함된 소셜 단추가 있는 페이지를 삭제할 수 없습니다.

## 복제

`application/x-www-url-formencoded` POST 요청으로 랜딩 페이지를 복제합니다.

`id` 경로 매개 변수는 원본 랜딩 페이지를 지정합니다.

`name` 매개 변수는 새 랜딩 페이지 이름을 지정합니다.

`folder` 매개 변수는 부모 폴더를 지정합니다. `id` 및 `type`을(를) 포함하는 포함된 JSON 개체로 전달합니다.

`template` 매개 변수는 원본 랜딩 페이지 템플릿 ID를 지정합니다.

선택적 `description` 매개 변수는 새 랜딩 페이지를 설명합니다.

```http
POST /rest/asset/v1/landingPage/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=MyNewLandingPage&folder={"type":"Program","id":1119}&template=57
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1078d#1683e4881c6",
    "warnings": [],
    "result": [
        {
            "id": 3291,
            "name": "MyNewLandingPage",
            "createdAt": "2019-01-11T18:59:25Z+0000",
            "updatedAt": "2019-01-11T18:59:25Z+0000",
            "folder": {
                "type": "Program",
                "value": 1119,
                "folderName": "DefaultProgramWithGuidedLP"
            },
            "workspace": "Default",
            "status": "draft",
            "template": 57,
            "robots": "index, nofollow",
            "formPrefill": false,
            "mobileEnabled": false,
            "URL": "http://na-abm.marketo.com/lp/284-RPR-133/DefaultProgramWithGuidedLPPerkutoTestLP-Clone-1.html",
            "computedUrl": "https://app-abm.marketo.com/#LP3291A1LA1"
        }
    ]
}
```

## 콘텐츠 관리 섹션

콘텐츠 섹션은 `index` 속성으로 정렬되며 클라이언트의 CSS 규칙에 따라 표시됩니다. 섹션을 관리하려면 [추가](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/addLandingPageContentUsingPOST), [업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST) 및 [삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/removeLandingPageContentUsingPOST) 끝점을 사용하세요. [랜딩 페이지 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET)를 사용하여 쿼리합니다.

각 섹션에는 `type` 및 `value` 매개 변수가 있습니다. `type`이(가) 필요한 `value`을(를) 결정합니다. JSON이 아닌 POST `x-www-form-urlencoded`(으)로 이러한 끝점에 데이터를 전달합니다.

**섹션 유형**

| 유형 | 값 |
| --- | --- |
| DynamicContent | 세분화 ID. |
| 양식 | 양식 ID. |
| HTML | 텍스트 HTML 컨텐츠. |
| 이미지 | 이미지 에셋의 ID입니다. |
| 사각형 | 비어 있음. |
| 리치 텍스트 | 텍스트 HTML 컨텐츠.  리치 텍스트 요소만 포함할 수 있습니다. |
| 스니펫 | 코드 조각 ID입니다. |
| SocialButton | 소셜 단추의 ID입니다. |
| 비디오 | 비디오의 ID입니다. |

자유 형식 페이지의 경우 필요한 각 콘텐츠 섹션을 추가합니다. Marketo은 ID가 `mktoContent`인 `div` 요소에 이를 임베드합니다.

안내식 페이지에는 [랜딩 페이지 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET)에서 반환된 미리 정의된 요소가 포함될 수 있습니다. 해당 끝점을 사용하여 요소를 추가하거나 [해당 콘텐츠를 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)하십시오.

### 동적 콘텐츠

섹션을 동적으로 만들려면 먼저 랜딩 페이지의 콘텐츠 목록에 표시되는지 확인하십시오. [랜딩 페이지 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)를 사용하여 해당 형식을 `DynamicContent`(으)로 설정합니다.

Marketo은 변환된 요소의 기본 형식과 콘텐츠를 상속하는 기본 동적 섹션을 만듭니다.

```http
GET /rest/asset/v1/landingPage/{id}/dynamicContent/RVMtNDg=.json
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "46e#1560fa169d9",
  "result": [
    {
      "createdAt": "2016-07-21",
      "updatedAt": "2016-07-21",
      "segmentation": 1007,
      "segments": [
        {
          "segmentId": 1018,
          "segmentName": "Default",
          "type": "RichText",
          "content": "\n\t\t\t\t\t\t\tAlice was beginning to get very tired of sitting by her sister on the bank, and having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it.\n\t\t\t\t\t\t"
        },
        {
          "segmentId": 1017,
          "segmentName": "New Segment",
          "type": "RichText",
          "content": "\n\t\t\t\t\t\t\tAlice was beginning to get very tired of sitting by her sister on the bank, and having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it.\n\t\t\t\t\t\t"
        }
      ]
    }
  ]
}
```

각 개별 세그먼트에 대한 [콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Content/operation/updateLandingPageDynamicContentUsingPOST)는 세그먼트 ID를 기반으로 수행됩니다.

```http
POST /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
segment=New Segment&value=New Content
```

```json
 {
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7516#14e08fe7cbbc",
  "result": [
    {
      "id": 1012
    }
  ]
}
```

## 변수

안내식 랜딩 페이지는 요소 값이 포함된 편집 가능한 변수를 지원합니다. 랜딩 페이지 편집기에서 변수를 수정합니다.

![랜딩 페이지 변수](assets/landing-page-variables.png)

변수는 안내식 랜딩 페이지 템플릿의 `<head>` 요소에 있는 메타 태그입니다. 지원되는 유형은 문자열, 색상 및 부울입니다. 다음 예제에서는 각 유형의 변수를 하나씩 정의합니다.

```html
<head>
  <meta charset="utf-8">
  <meta class="mktoString" mktoName="My String Variable" id="stringVar" default="Hello World!">
  <meta class="mktoColor" mktoName="My Color Variable" id="colorVar" default="#ffffff">
  <meta class="mktoBoolean" mktoName="My Boolean Variable" id="boolVar" default="true">
</head>
```

자세한 내용은 [안내 랜딩 페이지 템플릿 만들기](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template) 설명서의 &quot;편집 가능한 변수&quot; 섹션을 참조하십시오.

### 쿼리

랜딩 페이지 ID를 전달하여 랜딩 페이지 변수 가져오기 엔드포인트에 대한 변수를 검색합니다.

```http
GET /rest/asset/v1/landingPage/{id}/variables.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "10843#15a6d7e5fa1",
    "result": [
        {
            "id": "stringVar",
            "value": "Hello World!",
            "type": "string"
        },
        {
            "id": "colorVar",
            "value": "#FFFFFF",
            "type": "color"
        },
        {
            "id": "boolVar",
            "value": "true",
            "type": "boolean"
        }
    ]
}
```

이 안내 랜딩 페이지에는 `stringVar`, `colorVar` 및 `boolVar`의 세 가지 변수가 포함되어 있습니다.

### 업데이트

랜딩 페이지 ID, 변수 ID 및 변수 값을 랜딩 페이지 변수 업데이트 엔드포인트에 전달하여 안내식 랜딩 페이지에 대한 변수를 업데이트합니다.

```http
POST /rest/asset/v1/landingPage/{id}/variable/{variableId}.json?value={newValue}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "2b07#15a6db77da3",
    "result": [
        {
            "id": "stringVar",
            "value": "Hello Brave New World!",
            "type": "String"
        }
    ]
}
```

## 랜딩 페이지 미리 보기

[랜딩 페이지 전체 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Pages/operation/getLandingPageFullContentUsingGET)를 사용하여 브라우저에서 렌더링된 미리 보기를 검색합니다. 랜딩 페이지 `id` 경로 매개 변수가 필요합니다. 끝점은 두 개의 선택적 쿼리 매개 변수도 허용합니다.

- `segmentation`: `segmentationId` 및 `segmentId`을(를) 포함하는 JSON 개체의 배열입니다. 미리보기는 해당 세그먼트와 일치하는 리드를 나타냅니다.
- `leadId`: 정수 리드 ID입니다. 미리보기는 지정된 리드를 나타냅니다.

```http
GET /rest/asset/v1/landingPage/{id}/fullContent.json?leadId=1001&segmentation=[{"segmentationId":1030,"segmentId":1103}]
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "119ab#17692849f1e",
  "warnings": [],
  "result": [
    {
      "id": 1023,
      "content": "<!DOCTYPE html>\n<html>\n <head>\n <meta charset=\"utf-8\">\n \n \n <meta name=\"robots\" content=\"index, nofollow\">\n <title></title>\n <style>\n body {background:#FFFFFF} \n #myConditionalDisplayArea {\n display: true;\n }\n </style>\n <link rel=\"shortcut icon\" href=\"/favicon.ico\" type=\"image/x-icon\" >\n<link rel=\"icon\" href=\"/favicon.ico\" type=\"image/x-icon\" >\n\n\n<style>.mktoGen.mktoImg {display:inline-block; line-height:0;}</style>\n </head>\n <body id=\"bodyId\">\n \n Hello Brave New World!\n <div class=\"mktoText\" id=\"exampleText\"><div>This is an example editable text area.</div>\n<div>Lead Full Name = Hanna Crawford</div>\n<div><br /></div>\n <script type=\"text/javascript\" src=\"//munchkin.marketo.net//munchkin.js\"></script><script>Munchkin.init('123-ABC-456', {customName: 'Test-Landing-Page-APIs_Guided-Landing-Page---deverly', PURL_VISIT_TOKEN, wsInfo: 'j1RR'});</script>\n<div id=\"mktoClickBlockingDiv\"></div>\n </body>\n</html>\n"
    }
  ]
}
```
