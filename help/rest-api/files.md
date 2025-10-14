---
title: 파일
feature: REST API
description: ID 또는 이름별로 Marketo REST API 파일 쿼리, 폴더 및 오프셋으로 검색, 다중 부분 업로드를 통해 만들기 또는 업데이트, insertOnly, MIME 유형, 스트리밍 없음 등에 대한 안내서입니다.
exl-id: 17361cdc-2309-442c-803c-34ce187aee1a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# 파일

[파일 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files)

Marketo 구독을 통해 이미지, 스크립트, 문서 및 스타일 시트와 같은 임의의 파일을 저장할 수 있습니다. 이러한 모든 작업은 REST API를 통해 원격으로 작업할 수 있습니다. Marketo 구독에서 사용할 수 있는 스토리지는 대역폭 사용량이 많은 애플리케이션에 최적화되어 있지 않으므로 적절한 오디오 및 비디오 스트리밍 애플리케이션에 대체 요소를 사용해야 합니다.

## 쿼리

파일 쿼리는 간단하며 [ID](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFileByIdUsingGET), [이름](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFileByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/getFilesUsingGET)의 자산에 대한 표준 쿼리 형식을 따릅니다.

### ID별

```
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

```
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

세 가지 선택적 매개 변수가 있습니다.

- folder - &quot;id&quot; 및 &quot;type&quot; 속성을 포함하는 JSON 블록으로 지정된 상위 폴더
- offset - 항목 검색을 시작할 위치를 지정하는 정수(기본값은 0), maxReturn 매개 변수와 함께 사용할 수 있음
- maxReturn - 반환할 최대 항목 수를 지정하는 정수(기본값은 20개, 최대값은 200개)

```
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

[다중 파트/양식 데이터 형식의 요청으로 &#x200B;](https://developer.adobe.com/marketo-apis/api/asset/#tag/Files/operation/createFileUsingPOST)파일을 만듭니다. 최소한으로, 이름, 폴더 및 파일은 요청에 필요하며, 선택적 설명과 insertOnly 플래그는 만들기 호출이 같은 이름의 기존 파일을 업데이트하는 것을 방지합니다. file 매개 변수의 경우 name 매개 변수 외에 Content-Disposition 헤더에 &quot;filename&quot;이 필요합니다. 또한 파일에 대한 Content-Type 헤더를 전달해야 합니다. 이 헤더는 Marketo이 파일을 제공하는 데 사용할 MIME 유형입니다.

```
POST /rest/asset/v1/files.json
```

```
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

[파일 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/File-Contents/operation/updateContentUsingPOST)는 해당 ID를 기반으로 할 수 있습니다. 유일한 매개변수는 생성과 동일한 요구 사항이 있는 파일 매개변수입니다.

```
POST /rest/asset/v1/file/{id}/content.json
```

```
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
