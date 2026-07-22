---
title: 이메일
feature: REST API
description: 예측 콘텐츠 및 A/B 테스트 제한에 대한 메모를 사용하여 Marketo Asset REST API를 사용하여 ID, 이름 또는 폴더 탐색별로 이메일 에셋을 쿼리하고 관리하는 방법에 대해 알아봅니다.
exl-id: 6875730d-c74a-42cf-a3d2-dad7a3ac535d
TQID: https://experienceleague.adobe.com/t2FyPbwS836MvOe5rL0rVS7ibtzzZMmXwmgHBDZEr8Q
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1813
ht-degree: 1%

---

# 이메일

[이메일 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails)

이메일 REST 엔드포인트를 사용하여 이메일 에셋을 쿼리하고 관리합니다.

전자 메일에 [Marketo 예측 콘텐츠](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/predictive-content/working-with-predictive-content/understanding-predictive-content)가 포함된 경우 다음 끝점이 실패하고 오류 코드 709와 해당 오류 메시지가 표시됩니다.

- [이메일 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET)
- [이메일 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailComponentContentUsingPOST)
- [이메일 초안 승인](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/approveDraftUsingPOST)

## 쿼리

전자 메일은 템플릿과 동일한 쿼리 패턴을 지원합니다. [ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByIdUsingGET), [이름](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailUsingGET). 이름 기준 및 검색 엔드포인트는 폴더 필터링도 지원합니다.

전자 메일이 [A/B 테스트](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/email-test-a-b-test/add-an-a-b-test)를 사용하는 전자 메일 프로그램에 속하는 경우 다음 엔드포인트는 해당 전자 메일을 반환하지 않습니다.

- [ID로 이메일 받기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByIdUsingGET)
- [이름으로 이메일 받기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailByNameUsingGET)
- [이메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailUsingGET)

호출은 성공을 나타내지만 경고 `No assets found for the given search criteria.`을(를) 포함합니다.

### ID별

```http
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

이름별로 쿼리할 때 필요한 경우 폴더를 전달하여 해당 폴더로 검색을 제한합니다.

```http
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

이메일 찾아보기는 표준 자산 API 패턴을 따르며, 다음과 같은 선택적 필터를 지원합니다.

- `status`: `Approved` 또는 `Draft`.
- `folder`: `id` 및 `type`을(를) 포함하는 JSON 개체입니다.
- `earliestUpdatedAt` 및 `latestUpdatedAt`: 업데이트 시간 범위입니다.
- `maxReturn`: 반환할 결과 수. 기본값은 20이고 최대값은 200입니다.
- `offset`: 큰 결과 집합을 통해 페이지로 이동하는 `maxReturn`에서 작동합니다. 기본값은 0입니다.

```http
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

[전자 메일의 편집 가능한 섹션을 검색하려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET) 해당 콘텐츠를 쿼리합니다. 선택적으로 상태별로 필터링하여 승인됨 또는 초안 버전에서 섹션을 반환합니다.

```http
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

섹션은 `dynamicContent` 형식을 가질 수 있습니다. 자세한 내용은 [다이내믹 콘텐츠](dynamic-content.md)를 참조하세요.

## 쿼리 CC 필드

대상 인스턴스의 전자 메일 CC에 대해 활성화된 필드를 검색하려면 [전자 메일 CC 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailCCFieldsUsingGET) 끝점을 호출하십시오.

```http
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

원본 템플릿에서 [전자 메일을 만듭니다](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/createEmailUsingPOST). 전자 메일의 편집 가능한 섹션은 `mktEditable` 클래스와 고유한 `id` 속성이 있는 템플릿의 HTML 요소에서 가져옵니다.

이메일 만들기 호출에는 다음 매개 변수가 필요합니다.

- `name`: 전자 메일 이름입니다.
- `template`: 원본 템플릿입니다.
- `folder`: 상위 폴더입니다.

선택적 만들기 매개 변수는 `subject`, `fromName`, `fromEmail`, `replyEmail`, `operational` 및 `isOpenTrackingDisabled`입니다. 이러한 매개 변수가 생략되면 다음 기본값이 적용됩니다.

- `subject`이(가) 비어 있습니다.
- `fromName`, `fromEmail` 및 `replyEmail`은(는) 인스턴스 기본값을 사용합니다.
- `operational` 및 `isOpenTrackingDisabled`은(는) `false`입니다.

`isOpenTrackingDisabled` 매개 변수는 보낸 이메일에 열린 추적 픽셀이 포함되어 있는지 여부를 결정합니다.

```http
POST /rest/asset/v1/emails.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[전자 메일을 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailContentUsingPOST)하려면 해당 ID를 전달하고 전자 메일의 설명 또는 이름을 업데이트하십시오.

```http
POST /rest/asset/v1/email/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

각 이메일 콘텐츠 섹션을 개별적으로 업데이트합니다. [전자 메일 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailContentUsingPOST) 끝점을 사용하여 `subject`, `fromName`, `fromEmail` 및 `replyEmail`을(를) 업데이트합니다. 또한 이 끝점을 사용하면 이러한 값을 설정하여 정적 콘텐츠 대신 동적 콘텐츠를 사용할 수 있습니다.

각 매개 변수는 유형/값 JSON 개체입니다. 형식은 `Text` 또는 `DynamicContent`입니다. 값은 해당 텍스트 또는 다이내믹 컨텐츠에 사용되는 세그멘테이션의 ID입니다. 데이터를 JSON이 아닌 `application/x-www-form-urlencoded`이(가) 있는 게시물로 보냅니다. 전자 메일 콘텐츠를 업데이트하여 `isOpenTrackingDisabled`을(를) 설정할 수도 있습니다.

```http
POST /rest/asset/v1/email/{id}/content.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

다이내믹 콘텐츠를 사용하도록 섹션을 구성하려면 먼저 이메일 콘텐츠 가져오기로 섹션 ID를 검색합니다.

### 편집 가능한 섹션 업데이트

편집 가능한 섹션을 해당 `htmlId`(으)로 업데이트합니다. 전자 메일 `id` 및 섹션 `htmlId`은(는) 필수 경로 매개 변수입니다. `type`, `value` 및 `textValue` 매개 변수는 선택 사항입니다.

`type`이(가) `value`의 내용을 결정합니다.

- `Text`: `value`은(는) 섹션의 HTML 콘텐츠를 포함하는 문자열입니다.
- `DynamicContent`: `value`은(는) `DynamicContent`(으)로 설정된 `type`, 세분화 ID로 설정된 `segmentation` 및 기본 HTML 콘텐츠로 설정된 `default`을(를) 포함하는 JSON 개체입니다.
- `Snippet`: 지원되는 섹션 유형입니다.

선택적 `textValue` 매개 변수에 섹션의 텍스트 버전이 포함되어 있습니다. 데이터를 JSON이 아닌 `application/x-www-form-urlencoded`이(가) 있는 게시물로 보냅니다.

```http
POST /rest/asset/v1/email/{id}/content/{htmlId}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

포함된 코드 조각에 대해 텍스트에 대한 자동 복사가 비활성화된 경우 코드 조각 HTML을 업데이트한 다음 다른 섹션의 텍스트 버전을 업데이트하면 이메일 텍스트 버전에 업데이트된 코드 조각 HTML이 반영됩니다. 자동 복사가 비활성화될 때 예상대로 이전 코드 조각 텍스트가 유지되지 않습니다.

## 모듈

이메일 편집기 1.0에서 모듈은 템플릿에 정의된 이메일 섹션입니다. 모듈은 [전자 메일 템플릿 구문](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Modules)에 설명된 대로 요소, 변수 및 기타 HTML 콘텐츠를 포함할 수 있습니다.

모듈 API를 사용하여 이메일 내 모듈을 관리합니다. HTTP POST를 사용하는 모듈 끝점의 경우 요청 본문을 JSON이 아닌 `application/x-www-form-urlencoded`(으)로 형식을 지정합니다.

대부분의 모듈 끝점에는 경로 매개 변수로 `moduleId`이(가) 필요합니다. [전자 메일 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET) 끝점이 `htmlId` 특성에 모듈 ID를 반환합니다. [쿼리](#modules_query)를 참조하세요.

### 쿼리

모듈을 사용하려면 모듈을 고유하게 식별하는 `moduleId`을(를) 지정하십시오. 이메일에서 모듈의 순서를 설명하는 정수 모듈 인덱스가 필요할 수도 있습니다.

[모듈 ID 및 해당 인덱스를 검색하려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailContentByIdUsingGET) 경로 매개 변수로 전자 메일 ID를 지정하십시오.

다음 예제에서는 템플릿 선택기 UI의 스타터 템플릿 섹션에서 `Skeleton` 템플릿을 기반으로 1.0 이메일을 쿼리합니다.

```http
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
          "value": "<p style=\"text-align: center;\"><span style=\"color: #333333;\"><strong>Acme, Inc<\/strong><\/span><\/p> \n<div style=\"text-align: center;\">\n  You received this because you have subscribed to our newsletter. Click \n <a href=\"{{system.unsubscribeLink}}\" target=\"_blank\" class=\"mktNoTrack\">here<\/a> to unsubscribe. \n <br> \n<\/div>"
        },
        {
          "type": "Text",
          "value": "Acme, Inc \n You received this because you have subscribed to our newsletter. Click here <{{system.unsubscribeLink}}> to unsubscribe."
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

결과 배열에는 모듈 및 HTML 요소 설명이 모두 포함됩니다. 모듈 요소에 `Module`의 `contentType`이(가) 있고 `index`을(를) 포함합니다. `htmlId` 특성에 `moduleId`이(가) 포함되어 있습니다.

`Skeleton` 예제의 경우 다음 테이블은 각 `moduleId`을(를) 전자 메일의 해당 인덱스에 매핑합니다.

| moduleId (htmlId라고도 함) | 색인 |
| --- | --- |
| 스페이서 | 0 |
| 무료 이미지 | 1 |
| 비디오 | 2 |
| 자유 텍스트 | 3 |
| CTA | 4 |
| 시간 | 5 |
| 문서 | 6 |
| 꼬리말 | 7 |

#### 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

[모듈을 추가](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/addModuleUsingPOST)하려면 전자 메일의 템플릿에서 기존 모듈을 선택하십시오. 전자 메일 ID와 `moduleId`을(를) 경로 매개 변수로 지정하십시오. 필요한 `index` 쿼리 매개 변수가 모듈의 위치를 결정합니다. `index`이(가) 가장 큰 기존 인덱스를 초과하는 경우 API가 모듈을 전자 메일에 추가합니다.

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/add.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
index=10
```

```json
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

[모듈을 삭제](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/deleteModuleUsingPOST)하려면 전자 메일 ID와 `moduleId`을(를) 경로 매개 변수로 지정하십시오.

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/delete.json
```

```json
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

[모듈을 복제](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/duplicateModuleUsingPOST)하려면 전자 메일 ID와 `moduleId`을(를) 경로 매개 변수로 지정하십시오. API는 복제본을 원래 모듈 아래에 배치하고 나머지 모듈을 아래로 이동합니다.

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/duplicate.json
```

```json
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

[모듈을 다시 정렬](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/rearrangeModulesUsingPOST)하려면 모든 모듈과 원하는 위치를 포함하는 배열을 제출하세요. 각 배열 요소는 `{ "index": <_index_>, "moduleId": "<_moduleId_>" }` 형식의 JSON 개체입니다. 여기서 `<_index_>`은(는) 0부터 시작하는 모듈 위치이고 `<_moduleId_>`은(는) 모듈 ID입니다.

```http
POST /rest/asset/v1/email/{id}/content/rearrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[ {"index": 0, "moduleId": "free-image"}, {"index": 1, "moduleId": "title"}, {"index": 2, "moduleId": "mkvideo"}, {"index": 3, moduleId": "free-text"}, {"index": 4, "moduleId": "blankSpace"}, {"index": 5, "moduleId": "Separator"}, {"index": 6, "moduleId": "callToAction"}, {"index": 7, "moduleId": "blankSpace2"}, {"index": 8, "moduleId": "blankSpace3"} ]
```

```json
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

[모듈 이름을 바꾸려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/renameUsingPOST) `name` 매개 변수에 새 이름을 전달합니다. 전자 메일 ID와 기존 `moduleId`을(를) 경로 매개 변수로 지정하십시오.

```http
POST /rest/asset/v1/email/{id}/content/{moduleId}/rename.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=MarketoVideo
```

```json
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

이메일 편집기 1.0에서 변수는 이메일 요소에 대한 값을 저장합니다. [이메일 템플릿 구문](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax#EmailTemplateSyntax-Variables)에 설명된 대로 Marketo 관련 구문을 HTML에 추가하여 각 변수를 정의합니다. 변수 API를 사용하여 이메일 내 변수를 관리합니다.

### 쿼리

[변수를 검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailVariablesUsingGET)하려면 전자 메일 ID를 경로 매개 변수로 지정하십시오.

다음 예제에서는 템플릿 선택기 UI의 스타터 템플릿 섹션에서 `Skeleton` 템플릿을 기반으로 1.0 이메일을 쿼리합니다.

```http
GET /rest/asset/v1/email/{id}/variables.json
```

```json
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

결과 배열의 각 요소는 하나의 변수를 설명합니다.

변수에는 전체 이메일에 대한 전역 범위나 모듈에 대한 로컬 범위가 있을 수 있습니다. 모든 변수에는 `name`, `value` 및 `moduleScope` 특성이 있습니다. 부울 `moduleScope` 특성은 전역 변수의 경우 `false`이고 로컬 변수의 경우 `true`입니다. 로컬 변수에는 연결된 모듈의 `moduleId`도 포함됩니다.

#### 업데이트

[변수를 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateVariableUsingPOST)하려면 `value` 매개 변수에 새 값을 전달하십시오. 이메일 ID 및 변수 이름을 경로 매개 변수로 지정합니다. 모듈 변수를 업데이트할 때 `moduleId`을(를) 전달하여 연결된 모듈을 식별하십시오.

다음 예제에서는 전역 변수 `hrBorderSize`을(를) 업데이트합니다.

```http
POST /rest/asset/v1/email/{id}/variable/{name}.json
```

```text
Content-Type: application/x-www-form-urlencoded; charset=utf-8
```

```text
value=2
```

```json
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

다음 예제에서는 `CTA` 모듈의 로컬 변수 `ctaLinkText`을(를) `Click this button!`(으)로 업데이트합니다.

```http
POST /rest/asset/v1/email/1032/variable/ctaLinkText.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

이메일은 표준 자산 승인 라이프사이클을 따릅니다. 별도의 끝점을 사용하여 초안을 승인하거나, 승인된 버전의 승인을 취소하거나, 기존 초안을 폐기할 수 있습니다.

### 승인

승인 종단점은 Marketo 이메일 규칙에 대해 이메일을 확인합니다. 승인 전에 `from name`, `from email`, `reply to email` 및 `subject`을(를) 채워야 합니다.

```http
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

승인된 이메일에서만 `unapprove` 작업을 사용하십시오.

```http
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

초안 상태의 이메일만 삭제할 수 있습니다. 승인된 이메일은 취소할 수 없습니다.

```http
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

```http
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

이메일을 복제하려면 다음 매개 변수와 함께 `application/x-www-form-urlencoded` POST 요청을 보냅니다.

- `name`: 필수 항목입니다. 복제된 이메일 이름.
- `folder`: 필수 항목입니다. `id` 및 `type`이(가) 포함된 JSON 개체입니다.
- `description`: 선택 사항입니다. 복제된 전자 메일 설명.

소스 이메일에 승인된 버전이 없는 경우 엔드포인트는 초안 버전을 복제합니다.

```http
POST /rest/asset/v1/email/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

샘플 전자 메일을 보내려면 `emailAddress` 쿼리 매개 변수에서 받는 사람을 지정하십시오. 다음과 같은 선택적 매개 변수를 포함할 수도 있습니다.

- `leadId`: 데이터베이스의 특정 리드를 가장합니다.
- `textOnly`: 전자 메일의 텍스트 버전만 보냅니다.

```http
POST /rest/asset/v1/email/{id}/sendSample.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[전자 메일 전체 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/getEmailFullContentUsingGET) 끝점을 사용하여 수신자가 전자 메일을 받을 때 전자 메일의 실시간 미리 보기를 검색합니다. 이 끝점은 버전 1.0 이메일만 지원합니다.

필수 `id` 경로 매개 변수는 미리 볼 전자 메일을 식별합니다. 끝점은 세 개의 선택적 쿼리 매개 변수도 허용합니다.

- `status`: `draft` 또는 `approved`을(를) 허용합니다. 기본값은 승인된 이메일의 승인 버전 또는 승인되지 않은 이메일의 초안 버전입니다.
- `type`: `Text` 또는 `HTML`을(를) 허용합니다. 기본값은 `HTML`입니다.
- `leadId`: 잠재 고객의 정수 ID를 수락하고 해당 잠재 고객이 받은 것처럼 이메일을 미리 봅니다.

```http
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

[전자 메일 전체 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/createEmailFullContentUsingPOST) 끝점을 사용하여 전자 메일 에셋의 모든 콘텐츠를 바꿉니다. 이 끝점은 UI에서 코드 편집 기능을 사용하고 더 이상 상위 템플릿에 연결되지 않은 버전 1.0 이메일만 지원합니다.

끝점은 주로 표준 콘텐츠 끝점으로 변경할 수 없는 프로그램의 일부로 복제된 자산을 위한 것입니다. 다이내믹 콘텐츠가 포함된 이메일은 지원하지 않습니다. 이메일이 템플릿에 여전히 연결되어 있는 경우 엔드포인트는 오류를 반환합니다.

경로에 있는 전자 메일 `id`을(를) 사용하여 `multipart/form-data` 요청을 보냅니다. 요청 본문에는 전체 HTML 전자 메일 문서 및 콘텐츠 형식이 `text/html`인 `content` 매개 변수가 1개 포함되어야 합니다.

잘못된 형식의 HTML 문서는 경고를 발생시키며, 이로 인해 승인이 차단될 수 있습니다. JavaScript 또는 `<script>` 태그를 포함하면 오류가 발생하여 호출이 실패합니다.

```http
POST /rest/asset/v1/email/{id}/fullContent.json
```

```text
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
