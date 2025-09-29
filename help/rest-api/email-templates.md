---
title: 이메일 템플릿
feature: REST API
description: HTML 요구 사항, ID 또는 이름별 쿼리 및 폴더 탐색을 포함하여 Marketo REST API 이메일 템플릿을 만들고 관리하는 방법을 알아봅니다
exl-id: 0ecf4da6-eb7e-43c1-8d5c-0517c43b47c8
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 1%

---

# 이메일 템플릿

[전자 메일 템플릿 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates)

이메일 템플릿은 Marketo의 각 새 이메일에 대한 기반을 구성합니다.  HTML 대체를 통해 템플릿에서 이메일의 연결을 해제할 수 있지만 처음에는 템플릿을 기반으로 이메일을 만들어야 합니다.  템플릿은 이름 및 설명과 같은 메타데이터를 사용하여 Marketo에서 순수 HTML 문서로 만들어집니다.  콘텐츠에 대한 제한은 거의 없지만 템플릿의 HTML이 유효해야 하며 [여기에 요약된](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-editable-sections-to-email-templates-v1-0) 요구 사항을 따르는 편집 가능한 섹션을 하나 이상 포함해야 합니다.

## 쿼리

전자 메일 템플릿 쿼리는 에셋의 표준 패턴을 따르며, 지정된 폴더에 대해 [ID별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getTemplateByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getTemplateByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getEmailTemplatesUsingGET) 쿼리를 허용합니다.

### ID별

```
GET /rest/asset/v1/emailTemplate/{id}.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "14f9e#14a12955df1",
    "result": [
        {
            "id": 19,
            "name": "aFgSxuZrBI",
            "description": "fUMhVfIyVkhHzRolYzjGyWouTMfjXCPIAZxHMAEmszAjguVKDtbznEeqbqiDuNBzQoHwBJFdXiMzYiMlGUwtuklUhjGfJlDbhaTL",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

#### 이름별

```
GET /rest/asset/v1/emailTemplate/byName.json?name=Test Template
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "14f9e#14a12955df1",
    "result": [
        {
            "id": 19,
            "name": "aFgSxuZrBI",
            "description": "fUMhVfIyVkhHzRolYzjGyWouTMfjXCPIAZxHMAEmszAjguVKDtbznEeqbqiDuNBzQoHwBJFdXiMzYiMlGUwtuklUhjGfJlDbhaTL",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

#### 찾아보기

```
GET /rest/asset/v1/emailTemplates.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"33c4#14a1832b4a8",
   "result":[
      {
         "id":18,
         "name":"AAA0unit3CreateTestEmailTemplateName.2314673e-7bc2-47da-a1e8-66dfdd8a1f1d",
         "description":"AssetAPI: getTemplates test",
         "createdAt":"2014-11-03T19:52:58Z+0000",
         "updatedAt":"2014-11-03T19:52:58Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":177,
         "name":"ABfRGutnwN",
         "description":"HMmHkdTRrGaRpPakdgGKICxfMunCEWDUWiThgAbInfaBXxGxSFfjKQIwerngCHRlGTnAJhKPmwlXLcsjGPtWEiILGyeIJTNVHoHg",
         "createdAt":"2014-11-20T19:31:06Z+0000",
         "updatedAt":"2014-11-20T19:31:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":148,
         "name":"ADVHJBQLyw",
         "description":null,
         "createdAt":"2014-11-20T06:42:57Z+0000",
         "updatedAt":"2014-11-20T06:42:57Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":201,
         "name":"AIpwuwiaqb",
         "description":null,
         "createdAt":"2014-11-25T20:49:06Z+0000",
         "updatedAt":"2014-11-25T20:49:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":240,
         "name":"aqZGoAskEF",
         "description":"uOMEhLpXOEWkwdZxkpcdDjTjKfokxuHEYHPVIVsADFIUEUobzIEaDiqFFxezwfovGfwjuPTJRxUmuHmGpyIklJdDdVosPJdyOVom",
         "createdAt":"2014-11-26T21:11:56Z+0000",
         "updatedAt":"2014-11-26T21:11:56Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":199,
         "name":"BAxnkVfLGi",
         "description":"TzUMQKzKXdgukNCCcaiJHUWASceqlZswhCqDQFDFZULqzYkEiyKcwtQRzKERynReqtMHOhqjnhExCsZopyfzglmXAOjEJdxNURCX",
         "createdAt":"2014-11-25T20:49:06Z+0000",
         "updatedAt":"2014-11-25T20:49:06Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      },
      {
         "id":278,
         "name":"bcBNCUIHrL",
         "description":"UJEPYBRGTSYosZRnMnahMyVtdyxjRpzJMSXyncATKwcLlDAqDnSCFezGVsDZFpZwPzQvBlvaOZzOzBIsIAtqIerZhJFfpqMogoiB",
         "createdAt":"2014-11-30T11:30:07Z+0000",
         "updatedAt":"2014-11-30T11:30:07Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

레코드 자체를 쿼리하면 레코드에 대한 메타데이터만 반환됩니다. 콘텐츠를 가져오려면 #content 섹션을 참조하십시오.

## 만들기 및 업데이트

[템플릿을 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/createEmailTemplateUsingPOST) 또는 [업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST)하는 것은 매우 간단합니다. 각 템플릿의 콘텐츠는 HTML 문서로 저장되며 POST의 다중 부분/양식 데이터 유형을 사용하여 Marketo에 전달되어야 합니다. [multipart](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) 및 [multipart/form-data](https://www.ietf.org/rfc/rfc2388.txt)에 대한 RFC에 설명된 대로 경계가 포함된 적절한 Content-Type 헤더를 전달해야 합니다.

템플릿을 만들려면 이름, 폴더, 컨텐츠의 세 가지 매개 변수를 포함해야 합니다. 선택적인 설명 파라미터(description parameter)가 포함될 수 있다.  HTML 문서는 콘텐츠 매개 변수로 전달되며, 이 매개 변수는 콘텐츠 처리 헤더의 일부로 기존 파일 이름 매개 변수도 포함해야 합니다.

```
POST /rest/asset/v1/emailTemplates.json
```

```
Content-Type: multipart/form-data; boundary=mktoBoundary1480963323998
```

```html
--mktoBoundary1480963323998
Content-Disposition: form-data; name="name"

Sample Email Template
--mktoBoundary1480963323998
Content-Disposition: form-data; name="folder"

{"id":15,"type":"Folder"}
--mktoBoundary1480963323998
Content-Disposition: form-data; name="content"; filename="testHTML.html"
Content-Type: text/html

<html>
<body>
<h1>TEST HTML</h1>
</body>
</html>

--mktoBoundary1480963323998
Content-Disposition: form-data; name="description"

Create email template using API
--mktoBoundary1480963323998--
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "a99f#14e22b2b85e",
    "result": [
        {
            "id": 1022,
            "name": "Sample Email Template",
            "description": "Create email template using API",
            "createdAt": "2015-06-23T23:13:34Z+0000",
            "updatedAt": "2015-06-23T23:13:34Z+0000",
            "url": "https://app-abm.marketo.com/#ET1022B2ZN12",
            "folder": {
                "type": "Folder",
                "value": 15,
                "folderName": "Templates"
            },
            "status": "draft",
            "workspace": "Default",
            "version": 1
        }
    ]
}
```

콘텐츠 업데이트는 전자 메일 템플릿의 ID가 필요한 [개별 끝점](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST)을 사용하여 수행됩니다. 이 끝점은 본문의 콘텐츠 매개 변수만 제출할 수 있도록 허용합니다. 업데이트가 이루어지면 콘텐츠 매개 변수에서 전달되는 모든 것은 승인된 버전을 업데이트하는 경우 새 초안에서 전자 메일의 기존 콘텐츠를 완전히 대체하거나 에셋이 초안 전용 상태인 경우 현재 초안을 대체합니다.

```
POST /rest/asset/v1/emailTemplate/{id}/content.json
```

```
Content-Type: multipart/form-data; boundary=mktoBoundaryEiJFFFPFKK2WovsT
```

```html
--mktoBoundaryEiJFFFPFKK2WovsT
Content-Disposition: form-data; name="content"; filename="testHTML2.html"
Content-Type: text/html

<html>
<body>
<h1>TEST HTML WITH UPDATE</h1>
<div class="mktEditable"></div>
</body>
</html>
--mktoBoundaryEiJFFFPFKK2WovsT--
```

```json
{
   "success": true,
   "warnings": [ ],
   "errors": [ ],
   "requestId": "f8e2#158d0ae24f8",
   "result":[
      {
         "id":1022,
         "status":"Draft",
         "content":"<html>\n<body>\n<h1>TEST HTML WITH UPDATE</h1>\n<div class="mktEditable"></div>\n</body>\n</html>"
      }
   ]
}
```

## 메타데이터 업데이트

[템플릿의 메타데이터 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/updateEmailTemplateUsingPOST), 이름 및 설명을 업데이트하려면 와 동일한 끝점을 사용하여 콘텐츠를 업데이트할 수 있지만 대신 이름 및 설명 매개 변수와 함께 application/x-www-url-formencoded POST를 전달합니다.

```
POST /rest/asset/v1/emailTemplate/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=Updated description&name=New Name
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "17ca5#14a12ab900a",
    "result": [
        {
            "id": 19,
            "name": "New Name",
            "description": "Updated description",
            "createdAt": "2014-11-14T02:41:26Z+0000",
            "updatedAt": "2014-11-14T02:41:26Z+0000",
            "folder": {
                "type": "Folder",
                "value": 15
            },
            "status": "Draft",
            "workspace": "Default"
        }
    ]
}
```

## 승인

이메일 템플릿은 에셋 레코드 승인에 대한 표준 패턴을 따릅니다. 각 엔드포인트를 통해 초안을 승인하고, 승인된 버전의 승인을 취소하며, 이메일 템플릿의 기존 초안을 폐기할 수 있습니다.

### 승인

승인 끝점을 호출하면 Marketo 이메일에 대한 규칙에 대해 이메일의 유효성을 검사합니다. 발신인 이름, 발신인 이메일, 회신 이메일 및 제목을 채워야 이메일을 승인할 수 있습니다.

```
POST /rest/asset/v1/emailTemplate/{id}/approveDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"abe2#14a1832a97d",
   "result":[
      {
         "id":338,
         "name":"lvAVYMZqPS",
         "description":"fZLJQSJRvnYbjGTUpIHHqDOuQgQzXQcWIXoOUPwrVLdMHKcbRqwLoSLkWZTUmaMiCIJSfQiufnnrgITUIqjuAPBLpmliiKuIUFYG",
         "createdAt":"2014-12-05T02:06:21Z+0000",
         "updatedAt":"2014-12-05T02:06:21Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Approved",
         "workspace":"Default"
      }
   ]
}
```

### 승인 취소

승인되지 않은 끝점은 승인된 템플릿에서만 사용할 수 있습니다.

```
POST /rest/asset/v1/emailTemplate/{id}/unapprove.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"17bfa#14a1832b3c4",
   "result":[
      {
         "id":344,
         "name":"LkilkvKrkp",
"description":"yAyUEXuWMtdhpODUmnCkGjpBcyEKnYucxaSoTyYeQzyNbYanxCXWPOzwiIWmeXPUwjfGAUmgnxlhgOPluVqwNittuvxJmNTaHxYM",
         "createdAt":"2014-12-05T02:06:23Z+0000",
         "updatedAt":"2014-12-05T02:06:23Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

### 버리기

템플릿의 초안 버전은 승인된 이메일이 업데이트된 후 생성됩니다.

```
POST /rest/asset/v1/emailTemplate/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"17bfa#14a1832b3c4",
   "result":[
      {
         "id":344,
         "name":"LkilkvKrkp",
         "description":"yAyUEXuWMtdhpODUmnCkGjpBcyEKnYucxaSoTyYeQzyNbYanxCXWPOzwiIWmeXPUwjfGAUmgnxlhgOPluVqwNittuvxJmNTaHxYM",
         "createdAt":"2014-12-05T02:06:23Z+0000",
         "updatedAt":"2014-12-05T02:06:23Z+0000",
         "folder":{
            "type":"Folder",
            "value":15
         },
         "status":"Draft",
         "workspace":"Default"
      }
   ]
}
```

### 삭제

```
POST /rest/asset/v1/emailTemplate/{id}/delete.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"15cef#149d3de83db",
   "result":[
      {
         "id":12
      }
   ]
}
```

## 복제

Marketo은 [전자 메일 템플릿을 복제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/cloneTemplateUsingPOST)하는 간단한 방법을 제공합니다. 작성과 달리, 이 유형의 요청은 application/x-www-url-formeencoded POST로 만들어지며, 두 개의 필수 매개 변수인 이름 및 폴더를 사용하며, ID와 유형이 포함된 JSON 개체를 사용합니다.  설명 또한 선택적 매개 변수입니다.

```
POST /rest/asset/v1/emailTemplate/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Sample Template 01 - deverly&folder={"id":12,"type":"Folder"}&description=This is a sample template
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "905e#14e22c693f8",
    "result": [
        {
            "id": 1024,
            "name": "Sample Template 01 - deverly",
            "description": "This is a sample template",
            "createdAt": "2015-06-23T23:35:16Z+0000",
            "updatedAt": "2015-06-23T23:35:16Z+0000",
            "url": "https://app-abm.marketo.com/#ET1024B2ZN12",
            "folder": {
                "type": "Folder",
                "value": 12,
                "folderName": "Templates"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

## 이메일 종속성 쿼리

[Get Email Template Used By](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates/operation/getEmailTemplateUsedByUsingGET) 엔드포인트를 사용하여 지정된 전자 메일 템플릿에 종속된 전자 메일 목록을 검색합니다.  `id` 경로 매개 변수는 상위 전자 메일 템플릿을 지정합니다.

2개의 선택적 매개 변수가 있습니다. `maxReturn`  는 결과 수를 제한하는 정수입니다(기본값은 20이고, 최대값은 200). `offset`은(는) `maxReturn`과(와) 함께 사용하여 큰 결과 집합을 읽을 수 있는 정수입니다(기본값은 0).

```
GET /rest/asset/v1/emailTemplates/{id}/usedBy.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "18b0#16fa3344169",
    "warnings": [],
    "result": [
        {
            "id": 1022,
            "name": "EmailPr.Email2",
            "type": "Email",
            "status": "approved",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1023,
            "name": "Default.Email1.email1",
            "type": "Email",
            "status": "approved",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1025,
            "name": "Defa.E1",
            "type": "Email",
            "status": "draft",
            "updatedAt": "2019-12-02T00:42:21Z+0000"
        },
        {
            "id": 1052,
            "name": "Email v1 Program.Email v1 Email",
            "type": "Email",
            "status": "draft",
            "updatedAt": "2019-06-07T20:07:16Z+0000"
        }
    ]
}
```
