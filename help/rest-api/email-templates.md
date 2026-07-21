---
title: 이메일 템플릿
feature: REST API
description: HTML 요구 사항, ID 또는 이름별 쿼리 및 폴더 탐색을 포함하여 Marketo REST API 이메일 템플릿을 만들고 관리하는 방법을 알아봅니다
exl-id: 0ecf4da6-eb7e-43c1-8d5c-0517c43b47c8
TQID: https://experienceleague.adobe.com/jKQpibaRP7nAyIsDdjMf8VkNPi5AMFbe7I4Iiy3MGc0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 570
ht-degree: 1%

---

# 이메일 템플릿

[이메일 템플릿 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates)

Marketo의 모든 새 이메일은 처음에 이메일 템플릿을 기반으로 합니다. 나중에 HTML을 교체하여 템플릿에서 이메일의 연결을 해제할 수 있지만 이메일을 만들 때는 템플릿을 선택해야 합니다.

템플릿은 이름 및 설명과 같은 메타데이터가 있는 HTML 문서입니다. 템플릿 HTML은 유효해야 하며 [편집 가능한 섹션 요구 사항](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/add-editable-sections-to-email-templates-v1-0)을 충족하는 편집 가능한 섹션을 하나 이상 포함해야 합니다.

## 쿼리

전자 메일 템플릿은 [ID별](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/getTemplateByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/getTemplateByNameUsingGET) 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/getEmailTemplatesUsingGET)와 같은 표준 자산 쿼리 패턴을 지원합니다.

### ID별

```http
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

```http
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

```http
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

템플릿 쿼리는 레코드 메타데이터만 반환합니다. 콘텐츠 끝점을 사용하여 템플릿 콘텐츠를 검색합니다.

## 만들기 및 업데이트

템플릿을 [만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/createEmailTemplateUsingPOST) 또는 [업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST)하려면 `multipart/form-data` POST 요청으로 HTML 문서를 보내십시오. `Content-Type` 헤더에는 [multipart](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html) 및 [multipart/form-data](https://www.ietf.org/rfc/rfc2388.txt)에 대한 RFC에 설명된 대로 경계가 포함되어야 합니다.

템플릿을 만들려면 다음 매개 변수가 필요합니다.

- `name`: 템플릿 이름입니다.
- `folder`: 상위 폴더입니다.
- `content`: HTML 문서입니다. 해당 `Content-Disposition` 헤더에는 기존 `filename` 매개 변수가 포함되어야 합니다.

선택적 `description` 매개 변수도 포함할 수 있습니다.

```http
POST /rest/asset/v1/emailTemplates.json
```

```text
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

템플릿 콘텐츠를 업데이트하려면 전자 메일 템플릿 ID로 [콘텐츠 끝점](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/updateEmailTemplateContentUsingPOST)을 호출하십시오. 요청 본문은 `content` 매개 변수만 허용합니다.

제출된 콘텐츠는 기존 템플릿 콘텐츠를 완전히 대체합니다. 승인된 버전을 업데이트하면 새 초안이 생성됩니다. 초안 전용 자산을 업데이트하면 현재 초안이 바뀝니다.

```http
POST /rest/asset/v1/emailTemplate/{id}/content.json
```

```text
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

[템플릿의 메타데이터를 업데이트하려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/updateEmailTemplateUsingPOST) `name` 및 `description` 매개 변수를 사용하여 `application/x-www-form-urlencoded` POST 요청을 보냅니다.

```http
POST /rest/asset/v1/emailTemplate/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

이메일 템플릿은 표준 자산 승인 라이프사이클을 따릅니다. 별도의 끝점을 사용하여 초안을 승인하거나, 승인된 버전의 승인을 취소하거나, 기존 초안을 폐기할 수 있습니다.

### 승인

승인 끝점이 Marketo 이메일에 대한 규칙에 대해 템플릿을 확인합니다. 승인 전에 보낸 사람 이름, 보낸 사람 이메일, 회신 이메일 및 제목을 채워야 합니다.

```http
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

승인되지 않은 끝점은 승인된 템플릿에서만 사용하십시오.

```http
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

승인된 템플릿을 업데이트하면 초안 버전이 만들어집니다. 해당 초안을 취소하려면 무시 끝점을 사용하십시오.

```http
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

```http
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

[전자 메일 템플릿을 복제](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/cloneTemplateUsingPOST)하려면 다음 매개 변수를 사용하여 `application/x-www-form-urlencoded` POST 요청을 전송하십시오.

- `name`: 필수 항목입니다. 복제된 템플릿 이름.
- `folder`: 필수 항목입니다. `id` 및 `type`이(가) 포함된 JSON 개체입니다.
- `description`: 선택 사항입니다. 복제된 템플릿 설명.

```http
POST /rest/asset/v1/emailTemplate/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[Get Email Template Used By](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates/operation/getEmailTemplateUsedByUsingGET) 엔드포인트를 사용하여 템플릿에 종속된 이메일을 검색합니다. `id` 경로 매개 변수는 상위 전자 메일 템플릿을 식별합니다.

끝점은 두 개의 선택적 페이지 매김 매개 변수를 지원합니다.

- `maxReturn`: 결과 수를 제한합니다. 기본값은 20이고 최대값은 200입니다.
- `offset`: 큰 결과 집합을 통해 페이지로 이동하는 `maxReturn`에서 작동합니다. 기본값은 0입니다.

```http
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
