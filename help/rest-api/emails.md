---
title: 이메일
feature: REST API
description: 이메일 에셋 조작을 위한 API입니다.
exl-id: 6875730d-c74a-42cf-a3d2-dad7a3ac535d
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 1%

---

# 이메일

[전자 메일 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails) 전자 메일 자산을 조작하기 위해 전체 REST 끝점 집합이 제공됩니다.

참고: [Marketo Predictive Content](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/predictive-content/working-with-predictive-content/understanding-predictive-content)을(를) 사용하는 경우 예측 콘텐츠가 포함된 이메일을 참조하는 경우 다음 끝점이 실패합니다. [이메일 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET), [이메일 콘텐츠 업데이트 섹션](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST), [이메일 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/approveDraftUsingPOST). 호출은 709 오류 코드와 해당 오류 메시지를 반환합니다.

## 쿼리

전자 메일의 쿼리 패턴은 템플릿의 쿼리 패턴과 동일하여 [id](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET), [이름](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET) 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET)와(과) 찾아보기 및 이름 API가 있는 폴더를 기준으로 필터링을 허용합니다.

참고: 전자 메일이 [A/B 테스트](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/email-test-a-b-test/add-an-a-b-test)를 사용하는 전자 메일 프로그램의 일부인 경우 [Id로 전자 메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByIdUsingGET), [이름별로 전자 메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailByNameUsingGET), [전자 메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailUsingGET) 끝점을 사용하여 해당 전자 메일을 쿼리할 수 없습니다. 호출은 성공을 나타내지만 다음 경고를 포함합니다. &quot;지정된 검색 기준에 대한 에셋을 찾을 수 없습니다.&quot;

### ID별

```
GET /rest/asset/v1/email/1351.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"9ad0#14a1832af8c",
   "result":[
      {
         "id":1356,
         "name":"sakZxhxkwV",
         "description":"sample description",
         "createdAt":"2014-12-05T02:06:21Z+0000",
         "updatedAt":"2014-12-05T02:06:21Z+0000",
         "subject":{
            "type":"Text",
            "value":"sample subject"
         },
         "fromName":{
            "type":"Text",
            "value":"RBxEtmdQZz"
         },
         "fromEmail":null,
         "replyEmail":{
            "type":"Text",
            "value":"Qlikf@testmail.com"
         },
         "folder":{
            "type":"folder",
            "value":10421
         },
         "operational":false,
         "textOnly":false,
         "publishToMSI":false,
         "webView":false,
         "status":false,
         "template":338,
         "workspace":"Default",
         "isOpenTrackingDisabled": false,
         "version": 2,
         "autoCopyToText": true,
         "ccFields": [
            {
              "attributeId": "157",
              "objectName": "lead",
              "displayName": "Lead Owner Email Address",
              "apiName": null
            }
          ],
         "preHeader": "My awesome preheader!"
      }
   ]
}
```

### 이름별

이름별의 경우 선택적으로 폴더를 전달하여 해당 폴더에서만 검색할 수 있습니다.

```
GET /rest/asset/v1/email/byName.json?name=My Email&folder={"id":1056,"type"="Folder"}
```

```json
{
   "success":true,
   "warnings":[
   ],
   "errors":[
   ],
   "requestId":"3a7f#14c484de875",
   "result":[
      {
         "id":1032,
         "name":"My Email",
         "description":"eCjxjIHmYPLtecoSphkvIXlrygOBDLhgyQKnsKMpiKWgSCKhkPMUFvFPUvEylmFiLjQGnffXGaiNLxAwiFOmIDvxEINoaSYascJw",
         "createdAt":"2015-03-23T20:23:25Z+0000",
         "updatedAt":"2015-03-23T20:23:25Z+0000",
         "subject":{
            "type":"Text",
            "value":"ezyKBmDcyCcUIrXASrLSvRuWQgWpRZxQstJoStgMSLEBASGKMpAnVeWrgJsaVFoFJUEXhEIPpDAWpzajzingUruFpiMcRRwtoBzU"
         },
         "fromName":{
            "type":"Text",
            "value":"dAiqRNJOdY"
         },
         "fromEmail":{
            "type":"Text",
            "value":"ilZxG@testmail.com"
         },
         "replyEmail":{
            "type":"Text",
            "value":"VYsCS@testmail.com"
         },
         "folder":{
            "type":"folder",
            "value":1056
         },
         "operational":false,
         "textOnly":false,
         "publishToMSI":false,
         "webView":false,
         "status":"draft",
         "template":32,
         "workspace":"Default",
         "isOpenTrackingDisabled": false,
        "version": 2,
         "autoCopyToText": true,
         "ccFields": [
            {
              "attributeId": "157",
              "objectName": "lead",
              "displayName": "Lead Owner Email Address",
              "apiName": null
            }
          ],
         "preHeader": "My awesome preheader!"
      }
   ]
}
```

### 찾아보기

폴더 검색은 다른 Asset API 검색 끝점과 마찬가지로 작동하며, `status`, `folder`, `earliestUpdatedAt`/`latestUpdatedAt`, `maxReturn` 및 `offset`에서 선택적 필터링을 허용합니다. `status`은(는) 승인됨 또는 초안입니다. `folder`은(는) `id` 및 `type`을(를) 포함하는 JSON 개체입니다. `maxReturn`은(는) 결과 수를 제한하는 정수입니다(기본값은 20이고, 최대값은 200). `offset`은(는) 큰 결과 집합을 읽는 데 `maxReturn`과(와) 함께 사용할 수 있는 정수입니다(기본값은 0).

```
GET /rest/asset/v1/emails.json?maxReturn=3&folder={"id":341,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "17576#14e22eb29cb",
    "result": [
        {
            "id": 2137,
            "name": "Social Sharing in Email",
            "description": "",
            "createdAt": "2011-03-04T17:12:42Z+0000",
            "updatedAt": "2011-03-04T19:04:36Z+0000",
            "url": null,
            "subject": {
                "type": "Text",
                "value": "Republish this content to your favorite social site!"
            },
            "fromName": {
                "type": "Text",
                "value": "Demo Master Marketo"
            },
            "fromEmail": {
                "type": "Text",
                "value": "demomaster@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "demomaster@marketo.com"
            },
            "folder": {
                "type": "Folder",
                "value": 341,
                "folderName": "Social Media"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": true,
            "status": "approved",
            "template": null,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": true,
            "ccFields": [
               {
                 "attributeId": "157",
                 "objectName": "lead",
                 "displayName": "Lead Owner Email Address",
                 "apiName": null
               }
             ],
            "preHeader": "My awesome preheader!"
        }
    ]
}
```

## 쿼리 콘텐츠

콘텐츠를 쿼리하여 전자 메일에 대해 [편집 가능한 섹션을 검색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET)할 수 있으며 선택적으로 상태를 필터링하여 승인됨 또는 초안 버전에 대한 섹션을 가져올 수 있습니다.

```
GET /rest/asset/v1/email/1356/content.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"8a44#14c484de8c8",
   "result":[
      {
         "htmlId":"edit_text_3",
         "value":[
            {
               "type":"HTML",
               "value":"Content from testCreateEmailTemplate2"
            },
            {
               "type":"Text",
               "value":"Content from testCreateEmailTemplate2"
            }
         ],
         "contentType":"Text"
      }
   ]
}
```

섹션은 dynamicContent 유형을 갖는 것으로 반환될 수 있습니다. 자세한 내용은 [다이내믹 콘텐츠](dynamic-content.md) 섹션을 참조하십시오.

## 쿼리 CC 필드

[전자 메일 CC 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailCCFieldsUsingGET) 끝점을 호출하여 대상 인스턴스의 전자 메일 CC에 대해 활성화된 필드 집합을 검색할 수 있습니다.

```
GET /rest/asset/v1/email/ccFields.json
```

```json
{  
   "success":true,
   "errors":[ ],
   "requestId":"e54b#16796fdbd4e",
   "warnings":[ ],
   "result":[  
      {  
         "attributeId":"157",
         "objectName":"lead",
         "displayName":"Lead Owner Email Address",
         "apiName":"leadOwnerEmailAddress"
      },
      {  
         "attributeId":"396",
         "objectName":"company",
         "displayName":"Account Owner Email Address",
         "apiName":"accountOwnderEmailAddress"
      }
   ]
}
```

## 만들기 및 업데이트

[전자 메일은 원본 템플릿을 기반으로 만들어짐](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailUsingPOST)이며, 해당 템플릿의 각 개별 HTML 요소에서 파생된 편집 가능한 섹션 목록과 &quot;mktEditable&quot; 클래스와 고유 ID 속성을 포함합니다. API를 사용하여 이메일을 만들면 전달된 추가 메타데이터와 함께 템플릿을 기반으로 레코드가 만들어집니다. 성공적인 이메일 만들기 호출을 위해서는 이름, 템플릿, 폴더 매개 변수가 필요합니다.

`subject`, `fromName`, `fromEmail`, `replyEmail`, `operational`, `isOpenTrackingDisabled` 매개 변수는 만들 때 선택 사항입니다. 설정하지 않으면 `subject`이(가) 비어 있고 `fromName`, `fromEmail` 및 `replyEmail`이(가) 인스턴스 기본값으로 설정되며 `operational` 및 `isOpenTrackingDisabled`은(는) false입니다. `isOpenTrackingDisabled`은(는) 전송 시 공개 추적 픽셀이 전자 메일에 포함되는지 여부를 결정합니다.

```
POST /rest/asset/v1/emails.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=My New Email 02 - deverly&folder={"id":1017,"type":"Program"}&template=24&description=This is a test email&subject=Hey There&fromName=SomeBody&fromEmail=somebody@marketo.com&replyEmail=somebody@marketo.com
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "f557#14e22db88d9",
    "result": [
        {
            "id": 2212,
            "name": "My New Email 02 - deverly",
            "description": "This is a test email",
            "createdAt": "2015-06-23T23:58:09Z+0000",
            "updatedAt": "2015-06-23T23:58:09Z+0000",
            "url": "https://app-abm.marketo.com/#EM2212A1LA1",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Program",
                "value": 1017,
                "folderName": "Landing Page - promotion"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": false,
            "ccFields": null,  
            "preHeader": null
        }
    ]
}
```

[전자 메일](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST) 레코드를 업데이트하는 작업은 ID로 수행할 수 있습니다. 이를 통해 이메일의 설명 또는 이름을 업데이트할 수 있습니다.

```
POST /rest/asset/v1/email/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=This is an Email&name=Updated Email
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "f557#14e22db88d9",
    "result": [
        {
            "id": 2212,
            "name": "Updated Email",
            "description": "This is an Email",
            "createdAt": "2015-06-23T23:58:09Z+0000",
            "updatedAt": "2015-06-23T23:58:09Z+0000",
            "url": "https://app-abm.marketo.com/#EM2212A1LA1",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Program",
                "value": 1017,
                "folderName": "Landing Page - promotion"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false,
            "version": 2,
            "autoCopyToText": false,
            "ccFields": null,  
            "preHeader": null
        }
    ]
}
```

### 콘텐츠 섹션, 유형 및 업데이트

[전자 메일 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailContentUsingPOST) 끝점을 사용하여 업데이트되는 전자 메일의 각 섹션 콘텐츠는 제목과 별도로 fromName, fromEmail 및 replyEmail을 개별적으로 업데이트해야 합니다. 이 끝점을 사용할 때 이러한 값은 정적 콘텐츠 대신 동적 콘텐츠를 사용하도록 설정할 수도 있습니다. 각 매개 변수는 유형/값 JSON 개체이며, 여기서 유형은 &quot;Text&quot; 또는 &quot;DynamicContent&quot;이고 값은 적절한 텍스트 값 또는 동적 콘텐츠에 사용할 세그먼테이션의 ID입니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.  isOpenTrackingDisabled는 업데이트 이메일 콘텐츠로 설정할 수 있습니다.

```
POST /rest/asset/v1/email/{id}/content.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
subject={"type":"Text","value":"Gettysburg Address"}&fromEmail={"type":"Text","value":"abe@testmail.com"}&fromName={"type":"Text","value":"Abe Lincoln"}&replyTO={"type":"Text","value":"replies@testmail.com"}
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"c865#14a1832afac",
   "result":[
      {
         "id":1356
      }
   ]
}
```

다이내믹 콘텐츠를 사용하도록 섹션을 설정하는 경우 이메일 콘텐츠 가져오기 호출을 통해 섹션 ID를 검색해야 합니다.

### 편집 가능한 섹션 업데이트

편집 가능한 섹션은 개별 htmlId로 업데이트됩니다. 경로 매개 변수로는 이메일 ID와 섹션의 htmlId만 필요하지만 유형, 값 및 textValue는 선택 사항입니다. 유형은 &quot;Text&quot;, &quot;DynamicContent&quot; 또는 &quot;Snippet&quot; 중 하나일 수 있으며 값에 전달되는 내용에 영향을 줍니다. 유형이 텍스트이면 값은 섹션의 HTML 콘텐츠를 포함하는 문자열입니다. DynamicContent이면 3개의 멤버가 있는 JSON 블록이며, 유형은 &quot;DynamicContent&quot;이고, 콘텐츠는 사용할 세그먼테이션의 ID인 세그먼테이션이며, 기본값은 섹션의 기본 HTML 콘텐츠를 포함하는 문자열입니다. 선택적 textValue 매개 변수는 섹션의 텍스트 버전을 포함하는 문자열입니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

```
POST /rest/asset/v1/email/{id}/content/{htmlId}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
type=Text&value=<h1>Hello World!</h1>&textValue=Hello World!
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "155ac#14d58dfa9ad",
    "result": [
        {
            "id": 2179
        }
    ]
}
```

참고: 이메일에 포함된 코드 조각에 대해 텍스트에 대한 자동 복사가 비활성화되면 코드 조각의 HTML 값이 업데이트되고, 이메일에 있는 다른 섹션의 텍스트 버전이 업데이트되므로 이메일의 텍스트 버전에는 자동 복사가 비활성화되는 경우 예상대로 이전 버전이 아닌 코드 조각 HTML의 업데이트된 값이 반영된 텍스트가 표시됩니다.

## 모듈

이메일 편집기 1.0에서 모듈은 템플릿에 정의된 이메일의 섹션입니다. 모듈은 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Modules)에서 설명한 대로 요소, 변수 및 기타 HTML 컨텐츠의 조합을 포함할 수 있습니다. Marketo은 이메일 내의 모듈 관리를 위한 API 세트를 제공합니다. HTTP POST 메서드가 필요한 모듈 관련 끝점의 경우 본문의 형식은 &quot;application/x-www-form-urlencoded&quot;(JSON이 아님)로 지정됩니다.

대부분의 모듈 관련 끝점에는 경로 매개 변수로 &quot;moduleId&quot;가 필요합니다. 모듈을 설명하는 문자열입니다. moduleIds가 [전자 메일 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET) 끝점에 의해 &quot;htmlId&quot; 특성으로 반환됩니다(아래 [쿼리](#modules_query) 섹션 참조).

### 쿼리

모듈로 작업하려면 모듈을 고유하게 식별하는 moduleId 매개 변수를 지정해야 합니다. 이메일에 있는 모듈의 순서를 설명하는 정수인 모듈 인덱스 매개 변수를 지정해야 할 수도 있습니다.

전자 메일 ID를 경로 매개 변수로 지정하여 [moduleIds 및 해당 인덱스를 검색합니다](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailContentByIdUsingGET).

다음 예제에서는 템플릿 선택기 UI의 &quot;Starter Templates&quot; 섹션에 있는 &quot;Skeleton&quot; 템플릿을 기반으로 1.0 이메일을 쿼리합니다.

```
GET /rest/asset/v1/email/{moduleId}/content.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "3d79#158da6492bd",
  "result": [
    {
      "htmlId": "free-image",
      "contentType": "Module",
      "index": 1,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "single",
      "value": {
        "width": "600",
        "altText": "",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 600px"
      },
      "contentType": "Image",
      "parentHtmlId": "free-image",
      "isLocked": false
    },
    {
      "htmlId": "video",
      "contentType": "Module",
      "index": 2,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "video2",
      "value": {
        
      },
      "contentType": "Video",
      "parentHtmlId": "video",
      "isLocked": false
    },
    {
      "htmlId": "free-text",
      "contentType": "Module",
      "index": 3,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "text",
      "value": [
        {
          "type": "HTML",
          "value": "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum officiis dolorum, nulla, mollitia ducimus iure modi perferendis tenetur ea illum veniam aut sapiente deserunt repellendus. Excepturi illo numquam sint harum."
        },
        {
          "type": "Text",
          "value": "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum officiis dolorum, nulla, mollitia ducimus iure modi perferendis tenetur ea illum veniam aut sapiente deserunt repellendus. Excepturi illo numquam sint harum."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "free-text",
      "isLocked": false
    },
    {
      "htmlId": "two-articles",
      "contentType": "Module",
      "index": 6,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "article3",
      "value": {
        "height": "auto",
        "width": "270",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 270px"
      },
      "contentType": "Image",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "articleTitle",
      "value": [
        {
          "type": "HTML",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        },
        {
          "type": "Text",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "text2",
      "value": [
        {
          "type": "HTML",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        },
        {
          "type": "Text",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "article4",
      "value": {
        "height": "auto",
        "width": "270",
        "style": "-ms-interpolation-mode: bicubic; outline: none; border-right-width: 0; border-bottom-width: 0; border-left-width: 0; text-decoration: none; border-top-width: 0; display: block; max-width: 100%; line-height: 100%; height: auto; width: 270px"
      },
      "contentType": "Image",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "articleTitle2",
      "value": [
        {
          "type": "HTML",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        },
        {
          "type": "Text",
          "value": "LOREM IPSUM DOLOR SIT AMET"
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "text3",
      "value": [
        {
          "type": "HTML",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        },
        {
          "type": "Text",
          "value": "Gumbo beet greens corn soko endive gumbo gourd. shallot courgette tatsoi pea sprouts fava bean collard greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "two-articles",
      "isLocked": false
    },
    {
      "htmlId": "footer",
      "contentType": "Module",
      "index": 7,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "footerText",
      "value": [
        {
          "type": "HTML",
          "value": "<p style=\"text-align: center;\"><span style=\"color: #333333;\"><strong>Acme, Inc<\/strong><\/span><\/p> \n<div style=\"text-align: center;\">\n  You received this because you've subscribed to our newsletter. Click \n <a href=\"{{system.unsubscribeLink}}\" target=\"_blank\" class=\"mktNoTrack\">here<\/a> to unsubscribe. \n <br> \n<\/div>"
        },
        {
          "type": "Text",
          "value": "Acme, Inc \n You received this because you've subscribed to our newsletter. Click here <{{system.unsubscribeLink}}> to unsubscribe."
        }
      ],
      "contentType": "Text",
      "parentHtmlId": "footer",
      "isLocked": false
    },
    {
      "htmlId": "spacer",
      "contentType": "Module",
      "index": 0,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "CTA",
      "contentType": "Module",
      "index": 4,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    },
    {
      "htmlId": "hr",
      "contentType": "Module",
      "index": 5,
      "parentHtmlId": "template-wrapper",
      "isLocked": false
    }
  ]
}
```

결과 배열에는 모듈 및 HTML 요소를 함께 설명하는 요소가 포함되어 있습니다. 모듈 요소에는 &quot;contentType&quot;: &quot;Module&quot; 속성과 &quot;index&quot; 속성이 포함됩니다. moduleId는 &quot;htmlId&quot; 속성에 저장됩니다.

위의 &quot;Skeleton&quot; 예제를 계속 진행하면 다음 표에는 이메일에 포함된 moduleIds 및 해당 인덱스에 대한 요약이 나와 있습니다.

| moduleId (htmlId라고도 함) | 색인 |
|---|---|
| 스페이서 | 0 |
| 무료 이미지 | 1 |
| 비디오 | 2 |
| 자유 텍스트 | 3 |
| CTA | 4 |
| 시간 | 5 |
| 문서 | 6 |
| 꼬리말 | 7 |

#### 추가

사용 중인 전자 메일 템플릿에 포함된 기존 모듈 중 하나를 선택하여 전자 메일에 [모듈을 추가](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/addModuleUsingPOST)합니다. 이렇게 하려면 경로 매개 변수로 이메일 ID와 moduleId를 지정합니다. 색인 쿼리 매개 변수는 필수이며 이메일에 있는 모듈의 순서를 결정합니다. 인덱스 값이 기존의 가장 큰 인덱스 값을 초과하는 경우 모듈이 이메일에 추가됩니다.

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/add.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
index=10
```

```
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "1063e#158d6ad2c3f",
    "result": [
        {
            "id": 1028
        }
    ]
}
```

#### 삭제

전자 메일 ID와 moduleId를 경로 매개 변수로 지정하여 [모듈을 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/deleteModuleUsingPOST)합니다.

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/delete.json
```

```
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "2356#158d6f6104a",
    "result": [
        {
            "id":1028
        }
    ]
}
```

#### 복제

[전자 메일 ID와 moduleId를 경로 매개 변수로 지정하여 모듈을 복제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/duplicateModuleUsingPOST)합니다. 이 호출은 모듈을 복제하여 원래 모듈 아래에 배치하고 다른 모듈을 아래로 밉니다.

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json
```

```
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "e740#158d705d967",
    "result": [
        {
            "id":1028
        }
    ]
}
```

#### 재배열

[모듈 다시 정렬](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/rearrangeModulesUsingPOST)모든 모듈을 포함하는 배열과 각 모듈에 대해 전자 메일 내에서 원하는 위치를 지정합니다. 각 배열 요소에는 다음 형식의 JSON 개체가 포함되어 있습니다.  { &quot;index&quot;: &lt;_index_>, &quot;moduleId&quot;: &quot;&lt;_moduleId_>&quot; }. 여기서 &lt;_index_>는 0부터 시작하는 모듈 순서 번호이고 &lt;_moduleId_>은 moduleId입니다.

```
POST /rest/asset/v1/email/{id}/content/rearrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
positions=[ {"index": 0, "moduleId": "free-image"}, {"index": 1, "moduleId": "title"}, {"index": 2, "moduleId": "mkvideo"}, {"index": 3, moduleId": "free-text"}, {"index": 4, "moduleId": "blankSpace"}, {"index": 5, "moduleId": "Separator"}, {"index": 6, "moduleId": "callToAction"}, {"index": 7, "moduleId": "blankSpace2"}, {"index": 8, "moduleId": "blankSpace3"} ]
```

```
{
    "success": true,
    "warnings":[ ],
    "errors":[ ],
    "requestId": "e67a#158d72d1cde",
    "result":[
        {
            "id": 1030
        }
    ]
}
```

#### 이름 바꾸기

[name 매개 변수를 통해 새 이름을 전달하여 전자 메일에서 모듈 이름을 변경](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/renameUsingPOST)합니다. 이메일 ID와 moduleId(기존 이름)를 경로 매개 변수로 지정합니다.

```
POST /rest/asset/v1/email/{id}/content/{moduleId}/rename.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=MarketoVideo
```

```
{
    "success": true,
    "warnings":[ ],
    "errors": [ ],
    "requestId":"11521#158d740abc0",
    "result": [
        {
            "id": 1030
        }
    ]
}
```

## 변수

이메일 편집기 1.0에서는 변수를 사용하여 이메일의 요소에 대한 값을 저장합니다. 각 변수는 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Variables)에서 설명한 대로 HTML에 Marketo 관련 구문을 추가하여 정의됩니다. Marketo은 이메일 내에서 변수를 관리하기 위한 API 세트를 제공합니다.

### 쿼리

전자 메일 ID를 경로 매개 변수로 지정하여 전자 메일에 대한 [변수를 검색합니다](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailVariablesUsingGET).

다음 예제에서는 템플릿 선택기 UI의 &quot;Starter Templates&quot; 섹션에 있는 &quot;Skeleton&quot; 템플릿을 기반으로 1.0 이메일을 쿼리합니다.

```
GET /rest/asset/v1/email/{id}/variables.json
```

```
{
  "success": true,
  "warnings": [ ],
  "errors": [  ],
  "requestId": "756#158dade55e8",
  "result": [
    {
      "name": "twoArticlesSpacer5",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer6",
      "value": "15",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "footerSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer7",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLinkText2",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer8",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLinkText",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "freeTextSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "freeTextSpacer2",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "ctaSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "hrBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "freeTextBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "spacerBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLink2",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "hrBorderColor",
      "value": "#e6e6e6",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaLink",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "freeImageBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "spacerSpacer",
      "value": "40",
      "moduleScope": false
    },
    {
      "name": "footerSpacer",
      "value": "10",
      "moduleScope": false
    },
    {
      "name": "ctaLinkText",
      "value": "CALL TO ACTION",
      "moduleScope": false
    },
    {
      "name": "twoArticlesButtonBackgroundColor2",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "ctaBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "footerBackgroundColor",
      "value": "#ffffff",
      "moduleScope": false
    },
    {
      "name": "twoArticlesLink",
      "value": "http:\/\/mylink",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "ctaBorderColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderColor2",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "hrBorderSize",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "twoArticlesButtonBackgroundColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesBorderSize2",
      "value": "1",
      "moduleScope": false
    },
    {
      "name": "ctaButtonBackgroundColor",
      "value": "#333333",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer4",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer3",
      "value": "15",
      "moduleScope": false
    },
    {
      "name": "twoArticlesSpacer2",
      "value": "20",
      "moduleScope": false
    },
    {
      "name": "ctaSpacer",
      "value": "20",
      "moduleScope": false
    }
  ]
}
```

결과 배열에는 변수를 설명하는 요소가 포함됩니다(요소당 하나의 변수).

변수는 전체 이메일에 전역적으로 또는 특정 모듈에 로컬로 지정할 수 있습니다. 두 범위의 변수에는 &quot;name&quot;, &quot;value&quot; 및 &quot;moduleScope&quot; 속성이 포함됩니다. &quot;moduleScope&quot; 속성은 부울이며, 여기서 false는 글로벌을 나타내고 true는 로컬을 나타냅니다. 로컬 변수에는 변수가 연결된 모듈을 지정하는 추가 &quot;moduleId&quot; 특성이 포함되어 있습니다.

#### 업데이트

값 매개 변수를 통해 새 원하는 값을 전달하여 전자 메일에서 [변수를 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateVariableUsingPOST)합니다. 이메일 ID와 변수 이름을 경로 매개 변수로 지정합니다. 모듈 변수를 업데이트하는 경우 moduleId 매개 변수도 전달하여 변수와 관련된 모듈을 지정해야 합니다.

다음 예제에서는 &quot;hrBorderSize&quot;라는 글로벌 변수를 값 1로 업데이트합니다.

```
POST /rest/asset/v1/email/{id}/variable/{name}.json
```

```
Content-Type: application/x-www-form-urlencoded; charset=utf-8
```

```
value=2
```

```
{
    "success":true,
    "warnings":[ ],
    "errors":[ ],
    "requestId":"feb5#158db4be57e",
    "result": [
        {
            "name":"hrBorderSize",
            "value":"2",
            "moduleScope":false
        }
    ]
}
```

다음 예제에서는 &quot;ctaLinkText&quot; 라는 로컬 변수를 &quot;Click this button!&quot; 값으로 업데이트합니다. in moduleId &quot;CTA&quot;.

```
POST /rest/asset/v1/email/1032/variable/ctaLinkText.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
value=Click this button!&moduleId=CTA
```

```json
{
    "success": true,
    "warnings":[ ],
    "errors":[ ],
    "requestId": "7f34#158dc28d2f7",
    "result": [
        {
            "name":"ctaLinkText",
            "value":"Click this button!",
            "moduleScope":true,
            "moduleId":"CTA"
        }
    ]
}
```

## 승인

이메일은 자산 레코드의 승인에 대한 표준 패턴을 따릅니다. 각 엔드포인트를 통해 초안을 승인하고, 승인된 버전의 승인을 취소하며, 이메일의 기존 초안을 폐기할 수 있습니다.

### 승인

승인 끝점을 호출하면 Marketo 이메일에 대한 규칙에 대해 이메일의 유효성을 검사합니다. 전자 메일을 승인하려면 `from name`, `from email`, `reply to email` 및 `subject`을(를) 채워야 합니다.

```
POST /rest/asset/v1/email/{id}/approveDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"15dbf#14a1832ae86",
   "result":[
      {
         "id":1362
      }
   ]
}
```

#### 승인 취소

승인된 이메일에만 `unapprove` 작업을 수행할 수 있습니다.

```
POST /rest/asset/v1/email/{id}/unapprove.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"3514#14a1832b0fa",
   "result":[
      {
         "id":1364
      }
   ]
}
```

#### 버리기

이메일을 삭제하려면 초안 상태여야 합니다. 승인된 이메일은 삭제할 수 없습니다.

```
POST /rest/asset/v1/email/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"182c0#14a1832af4f",
   "result":[
      {
         "id":1362
      }
   ]
}
```

#### 삭제

```
POST /rest/asset/v1/email/{id}/delete.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"169cd#14a1832adba",
   "result":[
      {
         "id":1361
      }
   ]
}
```

## 복제

Marketo은 이메일을 복제하는 간단한 방법을 제공합니다. 이 유형의 요청은 application/x-www-url-urlencoded POST으로 만들어지며 2개의 필수 매개 변수인 이름 및 폴더를 사용합니다. ID와 유형이 포함된 JSON 개체입니다. 설명은 선택적 매개 변수도 됩니다. 승인된 버전이 없으면 초안 버전이 복제됩니다.

```
POST /rest/asset/v1/email/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Clone of Social Sharing in Email&folder={"id":239,"type":"Folder"}&description=This is a test of clone email
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bd49#15706f43d96",
    "result": [
        {
            "id": 2250,
            "name": "Clone of Social Sharing in Email",
            "description": "This is a test of clone email",
            "createdAt": "2016-09-07T23:20:52Z+0000",
            "updatedAt": "2016-09-07T23:20:52Z+0000",
            "url": "https://app-abm.marketo.com/#EM2250B2",
            "subject": {
                "type": "Text",
                "value": "Hey There"
            },
            "fromName": {
                "type": "Text",
                "value": "SomeBody"
            },
            "fromEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "replyEmail": {
                "type": "Text",
                "value": "somebody@marketo.com"
            },
            "folder": {
                "type": "Folder",
                "value": 239,
                "folderName": "Tradeshows and Events"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "draft",
            "template": 24,
            "workspace": "Default",
            "isOpenTrackingDisabled": false
        }
    ]
}
```

## 샘플 보내기

api를 통해 emailAddress 쿼리 매개 변수로 전송될 샘플 이메일을 트리거할 수 있습니다. 데이터베이스에서 특정 리드를 가장하는 leadId 매개 변수와 이메일의 텍스트 버전만 전송하는 textOnly 매개 변수를 선택적으로 추가할 수도 있습니다.

```
POST /rest/asset/v1/email/{id}/sendSample.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
emailAddress=abe@testmail.com&textOnly=true
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "360b#14cce7d2708",
    "result": [
        {
            "id": 2179
        }
    ]
}
```

## 이메일 미리 보기

Marketo은 받는 사람에게 보낼 이메일의 실시간 미리 보기를 검색할 수 있도록 [이메일 전체 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/getEmailFullContentUsingGET) 엔드포인트를 제공합니다. 이 끝점은 버전 1.0 이메일에서만 사용할 수 있습니다. 한 개의 필수 매개 변수인 id 경로 매개 변수는 미리 보려는 이메일 에셋의 ID입니다. 세 가지 추가 선택적 쿼리 매개 변수가 있습니다.

- 상태: &quot;초안&quot; 또는 &quot;승인됨&quot; 값을 수락합니다. 이 값은 승인되면 승인된 버전으로, 승인되지 않으면 초안으로 기본 설정됩니다.
- 유형: &quot;텍스트&quot; 또는 &quot;HTML&quot;를 허용하며 기본값은 HTML입니다.
- leadId:. 잠재 고객의 정수 ID를 허용합니다. 설정된 경우 지정된 리드에 의해 수신된 것처럼 이메일을 미리 봅니다

```
GET /rest/asset/v1/email/{id}/fullContent.json
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": null,
   "result": [
      {
         "id": 339,
         "status": "draft",
         "content": "<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 1.01 Transitional//EN\" \"http://www.w1.org/TR/html4/loose.dtd\">\n<html>\n  <head>\n    <meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\"/>\n    <title></title>\n  </head>\n  <body>\n      <div style=\"font: 14px tahoma; width: 100%\" class=\"mktEditable\" id=\"edit_text_3\">\n        Content from testCreateEmailTemplate2\n    </div>\n  </body>\n</html>"
      }
   ]
}
```

## HTML 바꾸기

Marketo은 전자 메일 에셋의 전체 콘텐츠를 대체할 [전자 메일 전체 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/createEmailFullContentUsingPOST) 끝점을 제공합니다. 이 엔드포인트는 UI &quot;코드 편집&quot; 기능이 사용된 버전 1.0 이메일과 상위 템플릿과의 관계가 끊어진 이메일에서만 사용할 수 있습니다. 이 API는 주로 프로그램의 일부로 복제된 에셋에서 사용하기 위한 것이며 표준 콘텐츠 끝점으로 수정할 수 없습니다. 다이내믹 콘텐츠가 포함된 이메일은 지원되지 않습니다. 또한 관계가 손상되지 않은 이메일에 대한 HTML을 바꾸려고 하면 오류가 반환됩니다.

이 엔드포인트에는 콘텐츠 유형이 필요합니다. 경로에 id 매개 변수, 이메일 ID를 포함하고 본문에 매개 변수 하나를 포함하는 multipart/form-data가 콘텐츠 유형이 &quot;text/html&quot;인 전체 HTML 이메일 문서입니다. 잘못된 형식의 HTML 문서에서 경고가 발생하지만 승인을 허용하지 않을 수 있지만, 문서에 JavaScript 및/또는 `<script>`태그를 포함하면 호출이 실패하고 오류가 발생합니다.

```
POST /rest/asset/v1/email/{id}/fullContent.json
```

```
content-type: multipart/form-data; boundary=--------------------------116301888604800085728247
content-length: 599
```

```html
----------------------------116301888604800085728247
Content-Disposition: form-data; name="content"; filename="email_content.html"
Content-Type: text/html

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 1.01 Transitional//EN" "http://www.w1.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
 <title></title>
 </head>
 <body>
 <div style="font: 14px tahoma; width: 100%" class="mktEditable" id="edit_text_3">
 EMAIL TEST CONTENT
 </div>
 </body>
 </html>
----------------------------116301888604800085728247--
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": "15dbf#14a1832ae86",
   "result": [
      {
         "id": 1001
      }
   ]
}
```
