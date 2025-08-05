---
title: 랜딩 페이지
feature: REST API, Landing Pages
description: Marketo의 랜딩 페이지를 쿼리합니다.
exl-id: 2f986fb0-0a6b-469f-b199-1c526cd5a882
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# 랜딩 페이지

[랜딩 페이지 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages)

랜딩 페이지는 Marketo에서 호스팅하는 웹 페이지입니다.

## 쿼리

다른 대부분의 자산과 마찬가지로 랜딩 페이지도 [이름](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByNameUsingGET), [ID](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageByIdUsingGET) 및 [탐색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/browseLandingPagesUsingGET)별로 쿼리할 수 있습니다. 이 쿼리는 메타데이터만 반환하며 랜딩 페이지의 콘텐츠 섹션 목록은 랜딩 페이지의 ID로 별도로 쿼리해야 합니다.

랜딩 페이지의 콘텐츠를 쿼리하면 랜딩 페이지에서 사용할 수 있는 콘텐츠 섹션 목록이 반환됩니다. 콘텐츠를 업데이트하려면 페이지의 콘텐츠 목록에 섹션이 있어야 합니다.

```
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

안내식 랜딩 페이지에는 파생된 템플릿으로 정의된 섹션 집합이 제공되지만 자유 형식 페이지에는 사전 정의된 섹션이 제공되지 않으므로 편집하기 전에 콘텐츠를 추가해야 하므로 결과는 안내식 템플릿과 자유 형식 템플릿 간에 달라집니다.  &quot;content&quot; 속성의 형식은 &quot;type&quot; 속성과, 필드가 정적인지 또는 동적인지에 따라 달라질 수 있습니다.

## 만들기 및 업데이트

템플릿을 다시 참조하여 [랜딩 페이지가 만들어집니다](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/createLandingPageUsingPOST). 만들기 위해 필요한 필드는 이름, 템플릿(템플릿의 ID) 및 페이지를 배치할 폴더뿐입니다. 채울 수 있는 추가 메타데이터는 끝점 참조를 참조하십시오.

[랜딩 페이지 콘텐츠](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content) 끝점에 유효한 콘텐츠 형식은 richText, HTML, Form, Image, Rectangle, Snippet입니다.

```
POST rest/asset/v1/landingPages.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

랜딩 페이지 메타데이터는 [랜딩 페이지 메타데이터 끝점 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/updateLandingPageUsingPOST)로 업데이트할 수 있습니다.

## 승인

랜딩 페이지는 초안 버전 및/또는 승인된 버전이 있을 수 있는 표준 초안 승인 모델을 따릅니다. 업데이트는 페이지에 적용될 때마다 항상 초안 버전에 먼저 적용되며 페이지가 승인된 경우에만 라이브로 표시됩니다.

## 삭제

랜딩 페이지를 삭제하려면 먼저 사용 중이고 다른 Marketo 에셋에서 참조하지 않아야 하며 승인되지 않아야 합니다. 페이지는 [랜딩 페이지 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/deleteLandingPageByIdUsingPOST) 끝점을 사용하여 개별적으로 삭제됩니다. 이 API를 통해 포함된 소셜 단추가 있는 랜딩 페이지를 삭제할 수 없습니다.

## 복제

Marketo은 랜딩 페이지를 복제하는 간단한 방법을 제공합니다. application/x-www-url-formencoded POST 요청입니다.

`id` 경로 매개 변수는 복제할 소스 랜딩 페이지의 ID를 지정합니다.

`name` 매개 변수는 새 랜딩 페이지의 이름을 지정하는 데 사용됩니다.

`folder` 매개 변수는 새 랜딩 페이지를 만들 상위 폴더를 지정하는 데 사용됩니다. `id` 및 `type`을(를) 포함하는 포함된 JSON 개체의 형식입니다.

`template` 매개 변수는 원본 랜딩 페이지 템플릿 ID를 지정하는 데 사용됩니다.

선택적 `description` 매개 변수는 새 랜딩 페이지를 설명하는 데 사용됩니다.

```
POST /rest/asset/v1/landingPage/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

콘텐츠 섹션은 색인 속성별로 정렬되며, 최종적으로 클라이언트가 표시할 때 적용되는 CSS 규칙에 따라 배열됩니다. 콘텐츠 섹션은 해당 [추가](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/addLandingPageContentUsingPOST), [업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST) 및 [삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/removeLandingPageContentUsingPOST) 랜딩 페이지 콘텐츠 섹션 끝점으로 포함 및 관리되며 [랜딩 페이지 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET)를 사용하여 쿼리할 수 있습니다. 각 섹션에는 유형 및 값 매개 변수가 있습니다. 유형은 값에 입력할 항목을 결정합니다.  이러한 엔드포인트의 경우 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

**섹션 유형**

| 유형 | 값 |
|--- |--- |
| DynamicContent | 세분화 ID. |
| 양식 | 양식 ID. |
| HTML | 텍스트 HTML 컨텐츠. |
| 이미지 | 이미지 에셋의 ID입니다. |
| 사각형 | 비어 있음. |
| 리치 텍스트 | 텍스트 HTML 컨텐츠.  리치 텍스트 요소만 포함할 수 있습니다. |
| 코드 조각 | 코드 조각 ID입니다. |
| SocialButton | 의 ID  소셜 단추. |
| 비디오 | 비디오의 ID입니다. |

자유 형식 페이지의 경우 원하는 모든 콘텐츠 섹션을 추가해야 하며 ID가 `mktoContent`인 div 요소에 임베드됩니다. 안내 페이지의 경우 [랜딩 페이지 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/getLandingPageContentUsingGET) 끝점의 목록에 사전 정의된 요소 목록이 있을 수 있습니다. 해당 끝점을 통해 더 많은 콘텐츠를 추가하거나 [콘텐츠를 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST)할 수 있습니다.

### 다이내믹 콘텐츠

동적 콘텐츠 섹션을 만들려면 랜딩 페이지의 콘텐츠 목록에 동적 콘텐츠 섹션이 이미 있어야 합니다. [랜딩 페이지 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageContentUsingPOST) 끝점을 사용하여 형식을 &#39;DynamicContent&#39;로 설정해야 합니다. 섹션을 동적 컨텐츠로 설정하면 컨텐츠 섹션 내에 기본 동적 섹션이 만들어지고 이 섹션들은 모두 변환된 요소의 기본 유형을 상속합니다. 각 동적 섹션은 변환된 섹션의 컨텐츠도 상속합니다.

```
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

각 개별 세그먼트에 대한 [콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Content/operation/updateLandingPageDynamicContentUsingPOST)는 세그먼트 ID를 기반으로 수행됩니다.

```
POST /rest/asset/v1/landingPage/{id}/dynamicContent/{dynamicContentId}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

안내식 랜딩 페이지에 도입된 기능 중 하나는 편집 가능한 변수입니다.  변수에는 랜딩 페이지의 요소 값이 포함됩니다.  변수는 아래와 같이 랜딩 페이지 편집기를 사용하여 쉽게 수정할 수 있습니다.

![랜딩 페이지 변수](assets/landing-page-variables.png)

변수는 안내 모드 랜딩 페이지 템플릿의 `<head>` 요소 내에 메타 태그로 정의됩니다. 사용할 수 있는 변수에는 문자열, 색상 및 부울의 세 가지 유형이 있습니다.  다음은 세 가지 변수 정의의 예입니다.

```html
<head>
  <meta charset="utf-8">
  <meta class="mktoString" mktoName="My String Variable" id="stringVar" default="Hello World!">
  <meta class="mktoColor" mktoName="My Color Variable" id="colorVar" default="#ffffff">
  <meta class="mktoBoolean" mktoName="My Boolean Variable" id="boolVar" default="true">
</head>
```

자세한 내용은 [안내 랜딩 페이지 템플릿 만들기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template) 설명서의 &quot;편집 가능한 변수&quot; 섹션을 참조하십시오.

### 쿼리

랜딩 페이지 ID를 전달하여 랜딩 페이지 변수 가져오기 엔드포인트에 대한 변수를 검색합니다.

```
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

위치  이 예에서는 안내 랜딩 페이지에 stringVar, colorVar, boolVar의 3개 변수가 포함되어 있습니다.

### 업데이트

랜딩 페이지 ID, 변수 ID 및 변수 값을 랜딩 페이지 변수 업데이트 엔드포인트에 전달하여 안내식 랜딩 페이지에 대한 변수를 업데이트합니다.

```
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

Marketo은 브라우저에 렌더링되는 대로 랜딩 페이지의 실시간 미리 보기를 검색할 수 있도록 [랜딩 페이지 전체 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Pages/operation/getLandingPageFullContentUsingGET) 끝점을 제공합니다. 필수 매개 변수인 `id` 경로 매개 변수가 있습니다. 이 매개 변수는 미리 보려는 랜딩 페이지의 ID입니다. 다음 두 가지 추가 선택적 쿼리 매개 변수가 있습니다.

- 세그멘테이션: segmentationId 및 segmentId 특성이 포함된 JSON 개체 배열을 허용합니다. 설정되면, 에서는 해당 세그먼트와 일치하는 잠재 고객인 것처럼 랜딩 페이지를 미리 봅니다.
- 리드 ID:  잠재 고객의 정수 ID를 허용합니다. 설정되면, 은 지정된 리드가 본 것처럼 랜딩 페이지를 미리 봅니다.

```
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
