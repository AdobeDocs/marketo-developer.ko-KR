---
title: 폴더
feature: REST API
description: 만들기, 업데이트, 삭제, ID 및 이름별 쿼리, 루트, 작업 공간, maxDepth 및 페이지 매김을 사용하여 벌크 찾아보기 등에 대한 Marketo REST API 안내서.
exl-id: 4b55c256-ef0a-42b4-9548-ff8a4106f064
TQID: https://experienceleague.adobe.com/OxCNdy8qW6jwq8u57RF9mqVKPVvH99UmuiOBjFprHCM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d65b4a73-87a3-4d56-b638-74e74d9939ce
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 806
ht-degree: 1%

---

# 폴더

[폴더 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders)

폴더는 Marketo의 핵심 조직 에셋입니다. 다른 모든 에셋 유형에는 폴더 또는 프로그램인 상위 항목이 하나 이상 있습니다. 폴더는 순전히 조직적이지만 프로그램은 다른 자산 유형과 기능적 관계를 가지며 자산을 포함할 수도 있습니다.

폴더 API를 사용하여 폴더를 생성, 쿼리, 업데이트 및 삭제하거나 해당 컨텐츠를 검색합니다. 폴더 쿼리는 프로그램을 반환할 수 있지만 프로그램 API를 사용하여 프로그램을 생성, 업데이트 또는 삭제해야 합니다.

## 쿼리

폴더는 표준 에셋 쿼리 패턴을 지원합니다. [ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByIdUsingGET), [이름](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderUsingGET)별.

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

`type` 매개 변수는 필수이며 `Folder` 또는 `Program`이어야 합니다. 끝점이 폴더 ID를 검색하는지 또는 프로그램 ID를 검색하는지 여부를 결정합니다. 끝점은 결과 배열에서 하나의 레코드를 반환합니다.

`folderType` 응답은 폴더에 포함될 수 있는 내용을 식별합니다. 마케팅 활동 폴더에는 마케팅 폴더 또는 프로그램 유형이 있으며 여러 에셋 유형이 포함될 수 있습니다. Design Studio 폴더에는 포함할 수 있는 자산에 해당하는 유형이 있습니다. 예를 들어 이메일 폴더에는 폴더 유형이 이메일 또는 이메일 템플릿인 이메일 및 하위 폴더가 포함될 수 있습니다.

폴더 유형은 다음과 같습니다.

- 이메일
- 이메일 템플릿
- 랜딩 페이지
- 랜딩 페이지 템플릿
- 스니펫
- 파일

### 이름별

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET) 끝점에는 폴더 이름과 정확히 일치하는 모든 폴더를 반환하는 `name`이(가) 필요합니다.

끝점은 다음 선택적 매개 변수도 허용합니다.

- `type`: 폴더 유형(`Folder` 또는 `Program`)입니다.
- `root`: 검색할 폴더의 ID입니다. `root`을(를) 설정하는 경우 `type`도 설정해야 합니다.
- `workspace`: 검색할 작업 영역의 이름입니다.

```http
GET /rest/asset/v1/folder/byName.json?name=Test%2010%20-%20deverly
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "19#14e1f2f3688",
    "result": [
        {
            "name": "Test 10 - deverly",
            "description": "This is a test",
            "createdAt": "2015-06-23T06:27:04Z+0000",
            "updatedAt": "2015-06-23T06:27:04Z+0000",
            "url": "https://app-abm.marketo.com/#MF1070A1",
            "folderId": {
                "id": 454,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 416,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Marketing Programs - deverly/Test 10 - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 454
        }
    ]
}
```

마케팅 활동 및 Design Studio는 루트 폴더입니다. 루트를 이름별로 검색한 다음 이 루트를 사용하여 대상 인스턴스의 폴더 계층 구조를 탐색합니다.

### 찾아보기

[폴더를 일괄적으로 검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderUsingGET)할 수도 있습니다. `root` 매개 변수를 사용하여 쿼리할 상위 폴더를 지정하십시오. 다음 두 멤버가 포함된 JSON 개체로 `root`을(를) 전달합니다.

1. `id`: 폴더 또는 프로그램의 ID.
1. `type`: 루트 폴더 유형에 따라 `Folder` 또는 `Program`입니다.

루트 폴더를 모르거나 영역에 있는 모든 폴더를 검색하려면 마케팅 활동, Design Studio 또는 리드 데이터베이스 루트를 사용합니다. [이름별 폴더 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/getFolderByNameUsingGET) API에 영역 이름을 전달하여 루트 ID를 검색합니다.

다른 대량 자산 검색 끝점과 마찬가지로 페이지 매김에 선택적 `offset` 및 `maxReturn` 매개 변수를 사용합니다. 기타 선택적 매개 변수는 다음과 같습니다.

- `workSpace`: 필터링할 작업 영역의 이름입니다.
- `maxDepth`: 폴더 계층에서 이동할 최대 수준 수입니다. 값이 0이면 `root`에 의해 지정된 폴더만 반환됩니다. 기본값은 2입니다.

```http
GET /rest/asset/v1/folders.json?root={"id":14,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "9bd8#14e1f49047c",
    "result": [
        {
            "name": "Marketing Activities",
            "description": "Root node for the Marketing Activities app area",
            "createdAt": "2010-03-27T18:27:45Z+0000",
            "updatedAt": "2010-03-27T18:27:45Z+0000",
            "url": null,
            "folderId": {
                "id": 14,
                "type": "Folder"
            },
            "folderType": "Zone",
            "parent": null,
            "path": "/Marketing Activities",
            "isArchive": false,
            "isSystem": true,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 14
        },
        {
            "name": "Default",
            "description": "Root node of the Marketing activities Default",
            "createdAt": "2010-03-27T18:27:45Z+0000",
            "updatedAt": "2010-03-27T18:27:45Z+0000",
            "url": null,
            "folderId": {
                "id": 15,
                "type": "Folder"
            },
            "folderType": "Zone",
            "parent": {
                "id": 14,
                "type": "Folder"
            },
            "path": "/Marketing Activities/Default",
            "isArchive": false,
            "isSystem": true,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 15
        },
        {
            "name": "Archive",
            "description": "",
            "createdAt": "2010-03-27T18:28:17Z+0000",
            "updatedAt": "2010-03-27T18:28:17Z+0000",
            "url": "https://app-abm.marketo.com/#MF157A1",
            "folderId": {
                "id": 310,
                "type": "Folder"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 15,
                "type": "Folder"
            },
            "path": "/Marketing Activities/Default/Archive",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 310
        }
    ]
}
```

## 응답 구조

`folderId` 및 `parent` 필드는 폴더 ID 및 유형을 포함하는 JSON 개체입니다. API는 쿼리, `root` 및 `parent` 매개 변수에서 이 형식을 사용하여 폴더 및 프로그램 폴더 형식을 구별합니다.

`folderType` 필드는 폴더 사용 방법을 설명합니다. 마케팅 폴더, 프로그램, 이메일, 이메일 템플릿, 랜딩 페이지, 랜딩 페이지 템플릿, 코드 조각, 이미지, 영역 또는 파일일 수 있습니다. 마케팅 폴더 및 프로그램은 마케팅 활동에 존재하며 여러 에셋 유형을 포함할 수 있습니다. 다른 폴더 유형에는 해당되는 경우 해당 에셋 유형, 하위 폴더 및 해당 에셋 유형의 템플릿 버전만 포함됩니다. 영역은 마케팅 활동의 루트 수준 폴더를 나타냅니다.

`path` 폴더의 계층 구조가 Unix 스타일 경로로 표시됩니다. 첫 번째 항목은 항상 마케팅 활동 또는 Design Studio입니다. 인스턴스에 작업 영역이 있는 경우 두 번째 항목은 소유 작업 영역 이름입니다.

`url` 필드에 지정된 인스턴스의 자산 URL이 포함되어 있습니다. 범용 링크가 아니므로 사용자 인증이 필요합니다. `isSystem` 필드는 폴더가 읽기 전용 시스템 폴더인지 여부를 나타냅니다. 시스템 폴더 아래에 하위 폴더를 만들 수 있습니다.

## 만들기 및 업데이트

[폴더를 만들려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Folders/operation/createFolderUsingPOST) 다음 매개 변수를 사용하여 `application/x-www-form-urlencoded` POST 요청을 보냅니다.

- `name`: 폴더 이름을 포함하는 필수 문자열입니다.
- `parent`: `id` 및 `type`을(를) 포함하는 필수 포함된 JSON 개체입니다. 형식은 부모에 따라 `Folder` 또는 `Program`입니다.
- `description`: 최대 2,000자의 선택적 문자열입니다.

```http
POST /rest/asset/v1/folders.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
parent={"id":416,"type":"Folder"}&name=Test 10 - deverly&description=This is a test
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "111be#14e1f193e31",
    "result": [
        {
            "name": "Test 10 - deverly",
            "description": "This is a test",
            "createdAt": "2015-06-23T06:27:04Z+0000",
            "updatedAt": "2015-06-23T06:27:04Z+0000",
            "url": "https://app-abm.marketo.com/#MF1070A1",
            "folderId": {
                "id": 454,
                "type": "FOLDER"
            },
            "folderType": "Marketing Folder",
            "parent": {
                "id": 416,
                "type": "FOLDER"
            },
            "path": "/Marketing Activities/Default/Test 10 - deverly",
            "isArchive": false,
            "isSystem": false,
            "accessZoneId": 1,
            "workspace": "Default",
            "id": 454
        }
    ]
}
```

업데이트 끝점을 사용하여 선택적 `description`, `name` 또는 `isArchive` 매개 변수를 변경합니다. `isArchive`을(를) `true`(으)로 설정하면 Marketo UI에 폴더가 보관됩니다. `false`(으)로 설정하면 보관 위치에서 폴더가 제거됩니다.

이 API로 프로그램을 업데이트할 수 없습니다.

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

### 삭제

에셋 또는 하위 폴더가 없는 경우에만 단일 폴더를 삭제할 수 있습니다. 이 API를 사용하여 `isSystem` 필드가 `true`인 프로그램 또는 폴더를 삭제할 수 없습니다.

```http
POST /rest/asset/v1/folder/{id}/delete.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "4180#14e1f3fc017",
    "result": [
        {
            "id": 453
        }
    ]
}
```
