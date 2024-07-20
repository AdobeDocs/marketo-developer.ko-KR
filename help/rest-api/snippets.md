---
title: 코드 조각
feature: REST API, Snippets
description: Marketo API를 통해 코드 조각 관리.
exl-id: 87901c29-ee59-4224-848d-3bd6a6c52718
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# 코드 조각

[코드 조각 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets)

스니펫은 이메일 및 랜딩 페이지에 임베드할 수 있고, 동적 콘텐츠용으로 세그먼트화할 수 있는 재사용 가능한 HTML 구성 요소입니다. 스니펫에는 연결된 템플릿이 없으며 Marketo 내의 다른 에셋 내에서 만들고 배포할 수 있습니다.

## 쿼리

코드 조각 쿼리는 By Name 메서드가 없다는 점을 제외하면 자산의 표준 패턴을 따릅니다. [ID별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/getSnippetByIdUsingGET) 및 [찾아보기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/getSnippetUsingGET) 메서드를 사용하면 상태 필드를 사용하여 코드 조각의 승인된 버전 또는 초안 버전을 검색할 수 있습니다.

### ID별

```
GET /rest/asset/v1/snippet/{id}.json?status=approved
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"fa0f#14b04375f0a",
   "result":[
      {
         "id":83,
         "name":"BYkHVJEedl",
         "description":"yzSLvNFyrmeVmyLzqryUfGlDOJTnvyyfsQTXPDCGdCwcWUlfoCNApUqYgwZGElrUFoxBHJcMdXdqTKvtjtfsmPgokyRgVLeHyJCw",
         "createdAt":"2015-01-19T22:01:52Z+0000",
         "updatedAt":"2015-01-19T22:01:52Z+0000",
         "folder":{
            "type":"Folder",
            "value":662
         },
         "status":"approved",
         "workspace":"Default"
      }
   ]
}
```

### 찾아보기

```
GET /rest/asset/v1/snippets.json?maxReturn=3
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"f9cc#14b04376181",
   "result":[
      {
         "id":23,
         "name":"ADJvMLBMpS",
         "description":"XkzFUVLXVHrojLGLJVLPpwguOXuDvhAqaaSkBUVzgHrgDhqqRzyXlULIXSHJvfBHjCSaMwjyEdrdxcjFCRoNFVvdBBTDfSrUJzaR",
         "createdAt":"2015-01-15T20:10:39Z+0000",
         "updatedAt":"2015-01-15T20:10:39Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":620,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      },
      {
         "id":46,
         "name":"Biswa Snippet",
         "description":"",
         "createdAt":"2015-01-16T05:18:55Z+0000",
         "updatedAt":"2015-01-16T05:19:27Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":630,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      },
      {
         "id":12,
         "name":"dJJQkKbUYq",
         "description":"VXuHkYMREHrhxUSgYbKfaNeLisdFxOromCXQNrgmModvkuoyZdQjtAbXxDUbBvoDVCZmAVbasiHyWoWfTwgrGxnzpKepGrAUvfen",
         "createdAt":"2015-01-15T05:12:33Z+0000",
         "updatedAt":"2015-01-15T05:12:33Z+0000",
         "url": null,
         "folder":{
            "type":"Folder",
            "value":615,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      }
   ]
}
```

## 쿼리 콘텐츠

지정된 코드 조각의 콘텐츠는 코드 조각 ID를 기반으로 검색할 수 있습니다.

```
GET /rest/asset/v1/snippet/{id}/content.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"5c50#14b04376159",
   "result":[
      {
         "type":"HTML",
         "content":"draft testUpdateSnippetContent1 HTML Content"
      },
      {
         "type":"Text",
         "content":"draft testUpdateSnippetContent1 Text Content"
      }
   ]
}
```

이 호출은 콘텐츠 섹션 목록을 반환합니다.  HTML 또는 DynamicContent 형식의 섹션과 선택적으로 텍스트 형식의 섹션으로 구성됩니다.

## 만들기 및 업데이트

코드 조각은 [코드 조각 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/createSnippetUsingPOST)를 호출하는 복잡한 자산 만들기 패턴을 따르며 해당 내용은 별도로 만들어지므로 첫 번째 호출은 선택적 설명과 함께 만들기 끝점에 대한 것이어야 합니다.   데이터는 JSON이 아닌 x-www-form-urlencoded로 전달됩니다.

```
POST /rest/asset/v1/snippets.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Test Snippet 09 - deverly&folder={"id":395,"type":"Folder"}&description=This is a test snippet
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bd57#14e231ee3a1",
    "result": [
        {
            "id": 13,
            "name": "Test Snippet 09 - deverly",
            "description": "This is a test snippet",
            "createdAt": "2015-06-24T01:11:43Z+0000",
            "updatedAt": "2015-06-24T01:11:43Z+0000",
            "url": "https://app-abm.marketo.com/#SN13B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

코드 조각의 컨텐츠를 추가하거나 바꾸는 작업은 ID로 수행됩니다. 컨텐츠는 텍스트, HTML 또는 DynamicContent 유형일 수 있습니다. 유형이 텍스트이면 컨텐츠 매개 변수는 일반 텍스트 엔드포인트이며, HTML이 텍스트이면 원하는 마크업 텍스트입니다. 유형이 DynamicContent로 설정된 경우 콘텐츠 매개 변수는 코드 조각과 연결할 세그먼테이션의 ID로 설정해야 합니다.

```
POST /rest/asset/v1/snippet/{id}/content.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
type=HTML&content=draft testUpdateSnippetContent1 HTML Content
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"73d9#14b04376139",
   "result":[
      {
         "id":82
      }
   ]
}
```

[메타데이터 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/updateSnippetUsingPOST)도 ID로 수행됩니다. 이름과 설명만 업데이트할 수 있습니다.

```
POST /rest/asset/v1/snippet/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Test Snippet&description=New Description
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"9ad0#14b043762b1",
   "result":[
      {
         "id":82,
         "name":"Test Snippet",
         "description":"New Description",
         "createdAt":"2015-01-19T22:01:52Z+0000",
         "updatedAt":"2015-01-19T22:01:53Z+0000",
         "url": "https://app-abm.marketo.com/#SN3B2ZN395",
         "folder":{
            "type":"Folder",
            "value":662,
            "folderName": "Snippets"
         },
         "status":"draft",
         "workspace":"Default"
      }
   ]
}
```

## 다이내믹 콘텐츠

스니펫은 다이내믹 컨텐츠에 대한 표준 패턴을 따르지만, 하나의 전체 컨텐츠 섹션만 나타내므로 각 스니펫은 하나의 동적 섹션만 포함할 수 있으며, 사용된 세그먼테이션의 각 세그먼트에 대해 선택적으로 내부 섹션 목록이 포함됩니다. 코드 조각에 동적 콘텐츠 섹션이 하나만 있을 수 있으므로 동적 콘텐츠는 코드 조각 ID만으로 쿼리할 수 있습니다.

```
GET /rest/asset/v1/snippet/{id}/dynamicContent.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "ae3#14c2b499111",
    "result": [
        {
            "createdAt": "2015-03-13T06:24:35Z+0000",
            "updatedAt": "2015-03-17T20:29:42Z+0000",
            "id": 70,
            "segmentation": 1001,
            "content": [
                {
                    "id": "Nzk*",
                    "segmentId": 1001,
                    "segmentName": "Area",
                    "content": "Sample HTML for Area",
                    "type": "HTML"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1001,
                    "segmentName": "Area",
                    "content": "Sample Text for Area",
                    "type": "Text"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1002,
                    "segmentName": "Default",
                    "content": "Sample HTML for Default",
                    "type": "HTML"
                },
                {
                    "id": "Nzk*",
                    "segmentId": 1002,
                    "segmentName": "Default",
                    "content": "Sample Text for Default",
                    "type": "Text"
                }
            ]
        }
    ]
}
```

## 승인

코드 조각에는 표준 에셋 패턴을 따르는 초안을 승인, 승인 취소 및 삭제할 수 있는 엔드포인트가 있습니다. 승인하려면 코드 조각이 초안 상태여야 합니다.

### 승인

```
POST /rest/asset/v1/snippet/{id}/approveDraft.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "11903#14db1af2f6c",
    "result": [
        {
            "id": 3,
            "name": "Test Snippet 02 - deverly",
            "description": "hey this is a test snippet!",
            "createdAt": "2015-06-02T00:32:37Z+0000",
            "updatedAt": "2015-06-02T00:32:37Z+0000",
            "url": "https://app-abm.marketo.com/#SN3B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "approved",
            "workspace": "Default"
        }
    ]
}
```

### 승인 취소

`unapprove` 끝점은 승인된 스니펫에서만 사용할 수 있습니다.

```
POST /rest/asset/v1/snippet/{id}/unapprove.json
```

```json
{
    "success": true,
    "warnings": [ ],
    "errors": [ ],
    "requestId": "7d20#14db1c7a2a9",
    "result": [
        {
            "id": 89,
            "name": "Test Snippet 01 - deverly",
            "description": "",
            "createdAt": "2015-05-15T19:01:22Z+0000",
            "updatedAt": "2015-05-15T19:07:07Z+0000",
            "url": "https://app-abm.marketo.com/#SN1B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

### 초안 삭제

버리기 위해서는 코드 조각이 초안 상태여야 합니다.  승인된 스니펫은 삭제할 수 없습니다.

```
POST /rest/asset/v1/snippet/{id}/discardDraft.json
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":"674c#14b043760de",
   "result":[
      {
         "id":88
      }
   ]
}
```

## 복제

API를 사용하여 [코드 조각을 복제하는](https://developer.adobe.com/marketo-apis/api/asset/#tag/Snippets/operation/cloneSnippetUsingPOST)은(는) 간단하며 필수 이름, 원래 코드 조각 및 폴더의 ID와 선택적 설명을 사용하여 표준 패턴을 따릅니다.  승인된 버전이 없으면 초안 버전이 복제됩니다.

```
POST /rest/asset/v1/snippet/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Test Snippet Clone 3 - deverly&folder={"id":395,"type":"Folder"}&description=This is a test snippet
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "21c9#14e2327e33d",
    "result": [
        {
            "id": 14,
            "name": "Test Snippet Clone 3 - deverly",
            "description": "This is a test snippet",
            "createdAt": "2015-06-24T01:21:33Z+0000",
            "updatedAt": "2015-06-24T01:21:33Z+0000",
            "url": "https://app-abm.marketo.com/#SN14B2ZN395",
            "folder": {
                "type": "Folder",
                "value": 395,
                "folderName": "Snippets"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```
