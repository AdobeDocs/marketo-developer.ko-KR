---
title: 파일
feature: REST API
description: ID 또는 이름별로 Marketo REST API 파일 쿼리, 폴더 및 오프셋으로 검색, 다중 부분 업로드를 통해 만들기 또는 업데이트, insertOnly, MIME 유형, 스트리밍 없음 등에 대한 안내서입니다.
exl-id: 17361cdc-2309-442c-803c-34ce187aee1a
TQID: https://experienceleague.adobe.com/qH8zFwjJkTWHlCj1VHNiTiLK3mNOJFS83cnjEj2qjpA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 1%

---

# 파일

[파일 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Files)

파일 REST API를 사용하여 Marketo 구독에 저장된 이미지, 스크립트, 문서, 스타일 시트 및 기타 파일을 관리합니다.

Marketo 파일 스토리지는 대역폭 사용량이 많은 애플리케이션에 최적화되어 있지 않습니다. 오디오 및 비디오에 전용 스트리밍 서비스를 사용합니다.

## 쿼리

쿼리 파일 [ID별](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFileByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFileByNameUsingGET) 또는 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/getFilesUsingGET)입니다.

### ID별

```http
GET /rest/asset/v1/file/{id}.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":null,
   "result":[
      {
         "id":147,
         "size":61346,
         "mimeType":"image/jpeg",
         "url":"http://mlm.devlocal.marketo.com/rs/test/assets/rYXNeQFFVu",
         "folder":{
            "type":"Email",
            "id":10613
         },
         "name":"rYXNeQFFVu",
         "description":null,
         "createdAt":"2014-12-09T22:33:57Z+0000",
         "updatedAt":"2014-12-09T22:33:57Z+0000"
      }
   ]
}
```

### 이름별

필수 `name` 매개 변수를 사용하여 파일 이름을 지정하십시오.

```http
GET /rest/asset/v1/file/byName.json?name=foo.png
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "9049#15918a76619",
    "result": [
        {
            "id": 46488,
            "size": 13987,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/foo.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images"
            },
            "name": "foo.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T22:16:58Z+0000",
            "updatedAt": "2015-05-06T22:19:29Z+0000"
        }
    ]
}
```

### 찾아보기

찾아보기 끝점은 세 개의 선택적 매개 변수를 허용합니다.

- `folder` - `id` 및 `type` 특성을 포함하는 JSON 개체로서의 상위 폴더입니다.
- `offset` - 항목 검색을 시작할 위치입니다. 기본값은 0입니다. `maxReturn`에 사용합니다.
- `maxReturn` - 반환할 최대 항목 수입니다. 기본값은 20이고 최대값은 200입니다.

```http
GET /rest/asset/v1/files.json?folder={"id":436, "type": "Folder"}&maxReturn=3
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "17e4e#14e23372d80",
    "result": [
        {
            "id": 46484,
            "size": 1454,
            "mimeType": "text/plain",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/websites.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "websites.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T20:15:58Z+0000",
            "updatedAt": "2015-06-22T02:12:36Z+0000"
        },
        {
            "id": 46486,
            "size": 4169,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/mobile.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "mobile.png",
            "description": null,
            "createdAt": "2015-05-06T22:13:33Z+0000",
            "updatedAt": "2015-05-06T22:13:33Z+0000"
        },
        {
            "id": 46488,
            "size": 13987,
            "mimeType": "image/png",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/foo.png",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "foo.png",
            "description": "This is a test file.",
            "createdAt": "2015-05-06T22:16:58Z+0000",
            "updatedAt": "2015-05-06T22:19:29Z+0000"
        }
    ]
}
```

## 만들기 및 업데이트

`multipart/form-data` 요청을 사용하여 [파일을 만듭니다](https://developer.adobe.com/marketo-apis/api/asset#tag/Files/operation/createFileUsingPOST). `name`, `folder` 및 `file` 매개 변수가 필요합니다. `description` 및 `insertOnly` 매개 변수는 선택 사항입니다. true인 경우 `insertOnly`은(는) 요청에서 같은 이름의 기존 파일을 업데이트하지 못하도록 합니다.

`file` 매개 변수의 경우 `Content-Disposition` 헤더에 `filename`을(를) 포함하십시오. 또한 파일의 `Content-Type` 헤더도 포함합니다. Marketo은 파일을 제공할 때 이 MIME 유형을 사용합니다.

```http
POST /rest/asset/v1/files.json
```

```html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="file"; filename="marketo.html"
Content-Type: text/html
<html>
<body>
<h1>Test Page - marketo.html</h1>
</body>
</html>
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="name"
marketo.html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="folder"
{"id":436,"type":"Folder"}
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="description"
This is a test file
------WebKitFormBoundary2VyWOacQSupl4gUL—
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "278d#14e23316f63",
    "result": [
        {
            "id": 46960,
            "size": 69,
            "mimeType": "text/html",
            "url": "http://na-abm.marketo.com/rs/mktodemoaccount88/assets/marketo.html",
            "folder": {
                "type": "Image",
                "id": 436,
                "name": "My Images - deverly"
            },
            "name": "marketo.html",
            "description": "This is a test file",
            "createdAt": "2015-06-24T01:31:59Z+0000",
            "updatedAt": "2015-06-24T01:31:59Z+0000"
        }
    ]
}
```

[파일을 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/File-Contents/operation/updateContentUsingPOST)하려면 해당 ID를 지정하십시오. `file` 매개 변수의 요구 사항이 파일 생성과 동일합니다.

```http
POST /rest/asset/v1/file/{id}/content.json
```

```html
------WebKitFormBoundary2VyWOacQSupl4gUL
Content-Disposition: form-data; name="file"; filename="marketo.html"
Content-Type: text/html
<html>
<body>
<h1>Test Page - marketo.html</h1>
</body>
</html>
------WebKitFormBoundary2VyWOacQSupl4gUL--
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": null,
    "result": [
        {
            "id": 67,
            "size": 512000,
            "mimeType": "image/png",
            "url": "http://pages.devlocal.marketo.com/rs/test/assets/aLZiwCkXor",
            "folder": {
                "type": "Email",
                "id": 10391
            },
            "name": "aLZiwCkXor",
            "description": null,
            "createdAt": "2014-12-18T09:03:43Z+0000",
            "updatedAt": "2015-01-07T04:40:20Z+0000"
        }
    ]
}
```
