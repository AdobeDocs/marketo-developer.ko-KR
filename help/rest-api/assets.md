---
title: 자산
feature: REST API
description: ID 또는 이름별로 쿼리, 페이징으로 검색 및 폴더, 이메일, 양식, 템플릿, 파일, 토큰 만들기 또는 업데이트를 위한 Marketo Asset REST API의 개요입니다.
exl-id: 4273a5b1-1904-46e8-b583-fc6f46b388d2
TQID: https://experienceleague.adobe.com/gRhXvFtG1FHtGJ4tFQxOyGMkEiOX0K1S0VpjcB6s6xM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: d65b4a73-87a3-4d56-b638-74e74d9939ce
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 631
ht-degree: 3%

---

# 자산

Marketo Asset REST API를 사용하여 마케팅 및 조직 에셋을 쿼리하고 관리합니다.

## 자산

Marketo 자산은 다음과 같습니다.

- 폴더
- 프로그램
- 이메일
- 이메일 템플릿
- 조각
- 랜딩 페이지
- 랜딩 페이지 템플릿
- 스니펫
- 양식
- 토큰
- 파일

## API

매개 변수 및 모델링 정보를 포함한 자산 API 끝점의 전체 목록은 [자산 API 끝점 참조](endpoint-reference.md)를 참조하십시오.

## 쿼리

에셋 API는 일반적으로 ID, 이름 및 탐색의 세 가지 검색 패턴을 지원합니다. ID 또는 이름별 쿼리는 지정된 매개 변수에 대해 하나의 에셋을 검색합니다. 검색 엔드포인트는 해당 유형의 자산의 페이지가 매겨진 목록을 반환합니다.

필터링 매개 변수는 자산 유형에 따라 다릅니다. 지원되는 필터에 대해서는 각 자산 유형에 대한 설명서를 참조하십시오.

일부 검색 엔드포인트는 태그에 대해 허용되는 값과 같은 하위 자산을 반환하지 않습니다. 이름 또는 ID로 이러한 자산을 개별적으로 검색하여 전체 메타데이터를 가져옵니다. 다른 에셋 유형은 양식 필드 등 종속 개체에 대해 별도의 끝점을 제공합니다.

### ID별

```http
GET /rest/asset/v1/folder/{id}.json?type=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1241b#14e21ca814a",
    "result": [
        {
            "name": "Social Media",
            "description": null,
            "createdAt": "2011-03-04T17:01:32Z+0000",
            "updatedAt": "2011-03-04T17:01:32Z+0000",
            "url": null,
            "folderId": {
                "id": 341,
                "type": "Folder"
            },
            "folderType": "Email",
            "parent": {
                "id": 11,
                "type": "Folder"
            },
            "path": "/Design Studio/Default/Emails/Social Media",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 341
        }
    ]
}
```

### 이름별

자산 API는 쉼표가 포함된 자산 이름을 검색할 수 없습니다. 자산 이름에서 쉼표를 제외합니다.

```http
GET /rest/asset/v1/file/byName.json?name=My File
```

```json
{
   "success":true,
   "warnings":[ ],
   "errors":[ ],
   "requestId":null,
   "result":[
      {
         "id":148,
         "size":270313,
         "mimeType":"image/jpeg",
         "url":"http://mlm.devlocal.marketo.com/rs/test/assets/piKLbhVFvW",
         "folder":{
            "type":"Email",
            "id":10614
         },
         "name":"My File",
         "description":null,
         "createdAt":"2014-12-09T22:33:57Z+0000",
         "updatedAt":"2014-12-09T22:33:57Z+0000"
      }
   ]
}
```

### 찾아보기

에셋 검색 엔드포인트는 다음 쿼리 매개 변수를 지원합니다.

- `offset` - 결과 반환을 시작할 정수 오프셋입니다.
- `maxReturn` - 반환할 최대 레코드 수입니다. 기본값은 20이고 최대값은 200입니다.

```http
GET /rest/asset/v1/emailTemplates.json?offset=10&maxReturn=50
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
      }
   ]
}
```

## 만들기 및 업데이트

폴더, 토큰 및 파일과 같은 간단한 에셋 유형은 일반적으로 만들기 위한 하나의 종단점과 ID별 업데이트를 위한 다른 종단점을 제공합니다. 자산을 만들 때 이름이 필요합니다. 만들기 또는 업데이트 응답은 에셋 메타데이터와 ID를 반환합니다.

다음 요청은 토큰을 만듭니다.

```http
POST /rest/asset/v1/folder/{id}/tokens.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=April Fools&value=2015-04-01&type=date&folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "e3c2#14e280db5dc",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "April Fools",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}
```

다음 요청은 폴더를 업데이트합니다.

```http
POST /rest/asset/v1/folder/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
type=Folder&description=This is a test (update 01)
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "c5b2#14e1f3954bf",
    "result": [
        {
            "name": "Learning - deverly",
            "description": "This is a test (update 01)",
            "createdAt": "2015-03-17T00:17:02Z+0000",
            "updatedAt": "2015-06-23T07:02:07Z+0000",
            "url": "https://app-abm.marketo.com/#MF1044A1",
            "folderId": {
                "id": 407,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 15,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Learning - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 407
        }
    ]
}
```

Forms, 이메일, 이메일 템플릿, 랜딩 페이지 및 랜딩 페이지 템플릿은 더 복잡한 구조를 갖습니다. 각 유형은 에셋을 만들기 위한 하나의 엔드포인트와 해당 메타데이터, 콘텐츠 및 콘텐츠 섹션을 업데이트하기 위한 추가 엔드포인트를 제공합니다.

이러한 에셋은 사용하기 전에 승인되어야 합니다. 예를 들어 템플릿 ID로 랜딩 페이지를 만들고 해당 콘텐츠 섹션을 검색한 다음 각 필수 섹션을 업데이트하고 배포할 페이지를 승인합니다.

### 복잡한 만들기

상위 템플릿에서 랜딩 페이지를 만듭니다. 새 랜딩 페이지에는 각 섹션에 대한 템플릿의 기본 콘텐츠가 포함되어 있습니다.

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

#### 섹션 가져오기

랜딩 페이지의 콘텐츠 섹션을 검색합니다. 템플릿과 달라야 하는 각 섹션을 업데이트합니다.

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

#### 섹션 업데이트

```http
POST /rest/asset/v1/landingPage/{id}/content/{contentId}.json?type=Form&value=1
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5c37#154ea32cf11",
    "result": [
        {
            "id": 174
        }
    ]
}
```

## 승인

이메일, 랜딩 페이지, 스니펫, 양식 및 해당 템플릿은 초안 및 승인 시스템을 사용합니다. 콘텐츠 업데이트는 승인된 라이브 버전에 영향을 주지 않고 초안을 변경합니다.

승인 끝점이 초안의 유효성을 검사합니다. 검증이 성공하면 라이브 버전이 초안으로 바뀌고 초안 상태가 지워집니다. 유효성 검사가 실패하면 끝점이 이유를 반환합니다.

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

승인이 성공하면 이전 라이브 버전이 업데이트된 버전으로 바뀝니다.

지원되는 각 에셋 유형은 초안 폐기를 위한 끝점을 제공합니다. 초안이 있는 승인된 에셋의 경우 이 끝점은 초안 및 보류 중인 변경 사항을 삭제합니다.

자산에 승인된 버전이 없으면 끝점이 오류를 반환합니다. 초안 전용 에셋을 삭제할 수 있지만 해당 에셋의 초안을 삭제할 수는 없습니다.

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

승인 전용 상태인 에셋의 승인을 취소할 수 있습니다. 승인을 취소하면 라이브 버전이 제거되고, 에셋이 초안 전용 상태로 돌아가며, 연결된 초안이 모두 삭제됩니다.

대부분의 에셋 유형의 경우 에셋이 사용 중이면 안 됩니다. 예를 들어 이메일 전송 흐름 단계에서 참조되는 이메일 또는 이메일에 포함된 스니펫을 승인 취소할 수 없습니다.

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

## 삭제

양식을 제외하고 승인 및 초안 상태가 있는 자산은 삭제하기 전에 승인되지 않아야 합니다. 에셋은 일반적으로 사용하지 않아야 합니다. 폴더는 비어 있어야 합니다.

프로그램은 예외입니다. 프로그램 및 해당 컨텐츠가 프로그램 외부에서 사용되지 않는 경우 프로그램과 해당 하위 컨텐츠를 삭제할 수 있습니다.

```http
POST /rest/asset/v1/program/{id}/delete.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16501#14db042c6b7",
    "result": [
        {
            "id": 1109
        }
    ]
}
```

## 시간 초과

에셋 API의 시간 제한은 300초입니다.
