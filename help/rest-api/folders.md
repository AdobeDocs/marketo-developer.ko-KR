---
title: 폴더
feature: REST API
description: 만들기, 업데이트, 삭제, ID 및 이름별 쿼리, 루트, 작업 공간, maxDepth 및 페이지 매김을 사용하여 벌크 찾아보기 등에 대한 Marketo REST API 안내서.
exl-id: 4b55c256-ef0a-42b4-9548-ff8a4106f064
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 1%

---

# 폴더

[폴더 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders)

폴더는 Marketo의 핵심 조직 에셋이며 다른 모든 에셋 유형에는 상위 폴더로 하나 이상의 폴더가 있습니다. 이 상위 폴더는 순전히 조직적인 폴더 또는 다른 자산 유형과 기능 관계를 맺고 다른 자산의 상위 폴더가 될 수 있는 프로그램일 수 있습니다. API를 통해 폴더를 만들고, 쿼리하고, 업데이트하고, 삭제할 수 있으며 컨텐츠 목록을 검색할 수도 있습니다. 폴더 API 쿼리를 통해 프로그램을 반환할 수 있지만 프로그램 API를 통해 프로그램을 만들고, 업데이트하고, 삭제해야 합니다.

## 쿼리

폴더를 쿼리하면 [ID별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET)의 자산에 대한 표준 쿼리 형식을 따릅니다.

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

형식 매개 변수는 필수이며 &quot;Folder&quot; 또는 &quot;Program&quot; 중 하나여야 합니다.  유형은 폴더 ID 또는 프로그램 ID에 대해 폴더 조회가 수행되는지 여부를 나타냅니다. 이 끝점의 경우 결과 배열에 단일 레코드만 반환됩니다. 응답에서 folderType 매개 변수를 확인합니다. 이는 여러 유형의 폴더를 나타낼 수 있습니다. Marketo 활동 폴더에는 다양한 유형의 에셋을 포함할 수 있는 마케팅 폴더 또는 프로그램 유형이 있지만 Design Studio 폴더에는 보유할 수 있는 에셋 유형에 해당하는 유형이 있습니다. 예를 들어 folderType이 &quot;Email&quot;인 폴더에는 Email 또는 folderType의 Email 또는 Email Template이 있을 수 있는 기타 하위 폴더만 포함될 수 있습니다. 유형은 다음과 같습니다.

- 이메일
- 이메일 템플릿
- 랜딩 페이지
- 랜딩 페이지 템플릿
- 스니펫
- 파일

### 이름별

[이름별 쿼리](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET)도 허용됩니다. 이름별 쿼리 끝점의 이름이 유일한 필수 매개 변수로 있습니다. Name은 인스턴스에 있는 폴더의 이름 필드에 대해 정확한 문자열 일치를 수행하고 해당 이름과 일치하는 각 폴더에 대한 결과를 반환합니다. 또한 폴더 또는 프로그램, 검색할 폴더의 ID &quot;루트&quot; 또는 검색할 작업 공간의 이름 &quot;작업 공간&quot;일 수 있는 &quot;유형&quot;의 선택적 쿼리 매개 변수가 있습니다. 루트 매개 변수가 설정되면 형식 매개 변수도 설정해야 합니다.

```
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

이름으로 검색할 때 마케팅 활동과 Design Studio는 모두 자체 루트 폴더이므로 이름으로 검색하고 대상 인스턴스의 나머지 폴더 계층 구조를 탐색하는 데 사용할 수 있습니다.

### 찾아보기

폴더는 [일괄적으로 검색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderUsingGET)할 수도 있습니다. &quot;root&quot; 매개 변수는 쿼리가 수행될 상위 폴더를 지정하는 데 사용할 수 있으며 쿼리 매개 변수의 값으로 포함된 JSON 개체로 서식이 지정됩니다. Root에는 두 개의 멤버가 있습니다.

1. id - 폴더 또는 프로그램의 ID입니다.
1. 유형 - 브라우저에 대한 루트 폴더 유형에 따라 폴더 또는 프로그램 중 하나입니다.

루트 폴더를 알 수 없거나 특정 영역의 모든 폴더를 검색하려는 경우 루트를 &quot;마케팅 활동&quot;, &quot;Design Studio&quot; 또는 &quot;리드 데이터베이스&quot; 영역으로 지정할 수 있습니다. [이름별 폴더 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/getFolderByNameUsingGET) API를 통해 원하는 영역의 이름을 지정하여 각 ID를 검색할 수 있습니다.

다른 대량 자산 검색 끝점과 마찬가지로 offset 및 maxReturn은 페이징을 위한 선택적 매개 변수입니다.   기타 선택적 매개 변수는 다음과 같습니다.

- workSpace - 필터링할 작업 공간의 이름.
- maxDepth - 폴더 계층에서 트래버스할 최대 레벨 수. 0으로 설정하면 root에 지정된 폴더만 반환됩니다. 지정하지 않으면 기본값은 2입니다.

```
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

폴더 응답 구조의 상당 부분은 자체 설명적이지만, 몇 가지 분야는 개별적으로 주목할 필요가 있다. `folderId` 및 상위 필드는 폴더 자체의 명시적 ID와 유형을 포함하는 JSON 개체입니다. 이 유형은 폴더 및 프로그램 유형의 폴더를 적절히 구분할 수 있도록 API에 의해 쿼리, 루트 및 상위 매개 변수에 사용되는 유형입니다. `folderType`은(는) 폴더의 사용을 반영하며, 이 폴더는 &quot;마케팅 폴더&quot;, &quot;프로그램&quot;, &quot;이메일&quot;, &quot;이메일 템플릿&quot;, &quot;랜딩 페이지&quot;, 랜딩 페이지 템플릿&quot;, &quot;코드 조각&quot;, &quot;이미지&quot;, &quot;영역&quot; 또는 &quot;파일&quot; 중 하나일 수 있습니다.  마케팅 폴더 및 프로그램 유형은 마케팅 활동에 존재하며 여러 유형의 자산을 포함할 수 있음을 나타냅니다. 다른 유형은 해당 유형의 에셋, 하위 폴더 및 해당 유형의 템플릿 버전만 포함할 수 있음을 나타냅니다(해당하는 경우). Zone 유형은 마케팅 활동에 있는 루트 수준 폴더를 나타냅니다.

폴더의 경로는 Unix 스타일 경로와 유사한 폴더 트리의 계층 구조를 보여 줍니다. 경로의 첫 번째 항목은 항상 마케팅 활동 또는 Design Studio입니다. 대상 인스턴스에 작업 공간이 있는 경우 경로의 두 번째 항목은 소유 작업 공간의 이름이 됩니다. `url` 필드에 지정된 인스턴스에 있는 에셋의 명시적 URL이 표시됩니다. 이는 범용 링크가 아니므로 제대로 작동하려면 사용자로 인증되어야 합니다. `isSystem`은(는) 폴더가 시스템 폴더인지 여부를 나타냅니다. 이 값이 true로 설정되면 폴더 자체는 읽기 전용이지만 폴더는 하위 폴더로 만들 수 있습니다.

## 만들기 및 업데이트

[폴더 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Folders/operation/createFolderUsingPOST)는 단순하며 대상 폴더의 유형에 따라 두 개의 멤버, ID 및 유형이 폴더 또는 프로그램인 포함된 JSON 개체인 폴더를 만들 수 있는 두 개의 필수 매개 변수인 &quot;name&quot;, 문자열 및 &quot;parent&quot;가 있는 application/x-www-form-urlencoded POST로 실행됩니다. 원할 경우 문자열인 &quot;설명&quot;도 포함할 수 있으며 최대 2000자일 수 있습니다.

```
POST /rest/asset/v1/folders.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

폴더는 별도의 끝점을 통해 업데이트되며 설명, 이름 및 `isArchive`은(는) 업데이트할 선택적 매개 변수입니다. 업데이트로 인해 `isArchive`이(가) 변경되면 Marketo UI에서 폴더가 보관되거나, true로 변경되면 보관이 취소되거나, false로 변경되면 보관 해제됩니다. 이 API로 프로그램을 업데이트할 수 없습니다.

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

### 삭제

비어 있는 경우 단일 폴더에 대해 삭제할 수 있습니다. 즉, 에셋 또는 하위 폴더가 없습니다. 폴더가 Program 유형이거나 isSystem 필드가 true로 설정된 경우 이 API를 사용하여 삭제할 수 없습니다.

```
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
