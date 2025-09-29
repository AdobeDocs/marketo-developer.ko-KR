---
title: 자산
feature: REST API
description: ID 또는 이름별로 쿼리, 페이징으로 검색 및 폴더, 이메일, 양식, 템플릿, 파일, 토큰 만들기 또는 업데이트를 위한 Marketo Asset REST API의 개요입니다.
exl-id: 4273a5b1-1904-46e8-b583-fc6f46b388d2
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 2%

---

# 자산

Marketo은 Marketo 내의 대부분의 마케팅 및 조직 에셋과 상호 작용하는 API를 제공합니다.

## 자산

Marketo 자산은 다음과 같습니다.

- 폴더
- 프로그램
- 이메일
- 이메일 템플릿
- 랜딩 페이지
- 랜딩 페이지 템플릿
- 스니펫
- 양식
- 토큰
- 파일

## API

매개 변수 및 모델링 정보를 포함한 자산 API 끝점의 전체 목록은 [자산 API 끝점 참조](endpoint-reference.md)를 참조하십시오.

## 쿼리

Assets에는 일반적으로 id, 이름 및 탐색의 세 가지 패턴이 있습니다.  ID별 및 이름별 은 모두 지정된 매개변수에 대한 단일 자산을 검색하는 반면, 브라우징은 를 반환하고 해당 유형의 전체 자산 목록을 통한 페이징을 허용합니다.  개별 자산 유형에는 필터링할 수 있는 다양한 매개 변수가 있으므로 자세한 내용은 개별 문서를 참조하십시오.

경우에 따라 일부 에셋 유형의 검색 끝점은 태그에 대해 허용되는 값과 같은 하위 에셋을 반환하지 않으며 전체 메타데이터 세트를 반환하려면 이름별 또는 ID별 끝점을 사용하여 개별적으로 검색해야 합니다.  다른 끝점에는 양식 필드와 같은 종속 개체를 검색하기 위한 별도의 끝점이 있을 수 있습니다.

### ID별

```
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

기술적인 이유로 에셋 API는 쉼표(,)가 포함된 에셋 이름을 검색할 수 없습니다.  명명 규칙에서 모든 에셋 유형에 대해 쉼표를 제외하는 것이 좋습니다.

```
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

에셋을 검색할 때 항상 두 개의 쿼리 매개 변수가 허용됩니다.

- offset - 결과를 반환할 정수 오프셋입니다.
- maxReturn - 반환되는 레코드 수를 제한합니다.  설정하지 않으면 기본값이 20으로 설정되고 에는 최대 200이 있습니다.

```
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

폴더, 토큰 및 파일과 같은 간단한 에셋 유형의 경우, 일반적으로 만들기 위한 단일 끝점만 있고 ID별로 레코드를 업데이트하기 위한 추가 끝점이 있습니다.  Assets은 항상 필요한 이름으로 만들어지며, 만들기 또는 업데이트 응답에 의해 모든 메타데이터와 ID가 반환됩니다.

예를 들어 토큰을 만드는 방법은 다음과 같습니다.

```
POST /rest/asset/v1/folder/{id}/tokens.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

폴더를 업데이트하려면 다음 작업을 수행합니다.

```
POST /rest/asset/v1/folder/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

다른 에셋은 구조가 더 복잡하며 추가 하위 섹션 또는 하위 객체에 대한 업데이트가 필요한 경우 사용을 시작하기 전에 궁극적으로 승인을 받아야 합니다.  이러한 에셋 유형에는 Forms, 이메일, 이메일 템플릿, 랜딩 페이지 및 랜딩 페이지 템플릿이 포함됩니다.  이러한 각 엔드포인트에는 레코드를 만들기 위한 단일 엔드포인트가 있고 메타데이터, 콘텐츠 및 콘텐츠 섹션을 업데이트하기 위한 추가 엔드포인트가 있습니다.

예를 들어 랜딩 페이지를 만들려면 템플릿 ID를 사용하여 해당 만들기 엔드포인트를 호출한 다음 해당 콘텐츠 섹션을 검색하고, 콘텐츠를 라이브로 배포할 수 있도록 승인하기 전에 각 템플릿을 개별적으로 업데이트하여 콘텐츠를 추가해야 합니다.

### 복잡한 만들기

랜딩 페이지는 먼저 상위 템플릿을 사용하여 랜딩 페이지 자산을 만들어야 합니다.  이렇게 하면 각 콘텐츠 섹션에 대한 템플릿의 기본 콘텐츠가 포함된 새 랜딩 페이지가 만들어집니다.

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

#### 섹션 가져오기

랜딩 페이지의 콘텐츠를 채우려면 콘텐츠 섹션 목록을 검색한 다음 템플릿을 벗어난 섹션에 대해 개별 업데이트를 수행해야 합니다.

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

#### 섹션 업데이트

```
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

이메일, 랜딩 페이지, 코드 조각, Forms 및 해당 템플릿을 포함하여 많은 에셋 유형에 관련 초안 및 승인 시스템이 있습니다.  에셋을 승인하려고 하면 특정 검증 규칙 세트에 대해 에셋을 평가한 다음 이를 승인됨 상태로 설정하거나 실패 이유를 반환합니다.  이러한 유형의 에셋의 경우 특정 에셋의 콘텐츠가 업데이트될 때마다 에셋의 초안이 변경되며, 이는 승인된 버전에 영향을 주지 않습니다.  이를 통해 에셋의 라이브 버전에 영향을 주지 않고 콘텐츠를 안전하게 변경할 수 있습니다.  그런 다음 승인 끝점을 사용하여 변경 사항을 라이브 버전에 적용할 수 있습니다.  또한 추가 업데이트가 적용될 때까지 자산의 초안 상태가 지워집니다.

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

승인이 성공하면 이전 라이브 버전이 업데이트된 버전으로 바뀝니다.

각 유효한 에셋 유형에 대한 끝점을 통해 초안 삭제를 사용할 수도 있습니다.  초안이 있는 승인됨 상태의 에셋에서 이 옵션을 사용하면 현재 초안과 보류 중인 모든 변경 사항이 무시됩니다.  현재 승인된 버전이 없는 에셋에서 이 버전을 사용하면 아무 작업도 수행되지 않고 오류가 반환됩니다.  초안 전용 에셋은 삭제할 수 있지만 삭제할 수는 없습니다.

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

Assets이 승인 전용 상태인 경우 승인되지 않을 수도 있습니다.  이렇게 하면 에셋의 모든 라이브 버전이 삭제되고 에셋이 초안 전용 상태로 돌아가며 연결된 초안도 모두 삭제됩니다.  이 작업은 이메일 전송 흐름 단계에서 참조되는 이메일 또는 이메일에 임베드되는 스니펫과 같이 Marketo의 어느 곳에서도 사용되지 않는 대부분의 에셋에 대해서만 수행할 수 있습니다.

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

## 삭제

양식을 제외한 승인 및 초안 상태의 Assets은 승인 중에 삭제할 수 없으며 삭제하기 전에 승인되지 않아야 합니다.  일반적으로 삭제는 에셋이 승인되지 않아 사용하지 않을 때 및 폴더의 경우 에셋이 비어 있는 경우에만 수행할 수 있습니다.  한 가지 주목할 만한 예외는 프로그램 및 해당 콘텐츠가 프로그램 범위 밖에서는 사용되지 않는 한 모든 하위 콘텐츠와 함께 삭제할 수 있는 프로그램입니다.

```
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
