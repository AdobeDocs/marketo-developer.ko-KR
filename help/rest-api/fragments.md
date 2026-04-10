---
title: 조각
feature: REST API
description: Marketo Asset REST API를 사용하여 조각에 대한 종속성을 쿼리, 만들기, 업데이트, 복제, 삭제, 승인 및 검사합니다.
exl-id: 9dd532d1-1dd7-4581-86dd-1943fab66cbb
source-git-commit: e2606d6cb12c572603ff069617de58417e43ca63
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 9%

---

# 조각

조각은 이메일과 같은 다른 에셋에서 참조할 수 있는 재사용 가능한 콘텐츠 에셋입니다.

## 액세스

이 문서에 설명된 끝점에는 액세스 토큰이 필요합니다.

```text
?access_token=<access_token>
```

요청에는 `x-app-type` 헤더도 필요합니다.

```text
x-app-type: <app-type>
```

## 쿼리

자산 ID별로 또는 필터 끝점을 사용하여 조각 메타데이터를 검색할 수 있습니다.

### ID별

#### 요청

```http
GET /rest/asset/v2/fragment/{id}
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "fa0f#1900ab15001",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "description": "Reusable hero block",
      "status": "approved"
    }
  ]
}
```

### 필터

필터 끝점은 작업 영역 내에서 검색하고 추가 쿼리 매개 변수로 결과 범위를 좁힐 수 있습니다. `workspaceId`은(는) 필수입니다.

todo: 표로 만들기
지원되는 필터에는 `folderId`, 반복된 `folderIds`, 반복된 `status`, `pageIndex`, `pageSize`, `createdBy`, `createdAtStart`, `createdAtEnd`, `modifiedBy`, `modifiedAtStart`, `modifiedAtEnd`, `name`, `fragmentType`, `sortKey`, `sortOrder`, `isCreatedByMe`, `isModifiedByMe`, `scriptEngine`, `isValueNonNullable` 및 `includeArchived`이(가) 포함됩니다.

#### 요청

```http
GET /rest/asset/v2/fragment/filter?workspaceId=1001&fragmentType=email&pageIndex=0&pageSize=20
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "f9cc#1900ab1504a",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "status": "approved"
    }
  ]
}
```

이름으로 조각을 찾아야 할 때는 `name` 매개 변수를 사용하십시오.

## 만들기

JSON 페이로드를 전송하여 조각을 만듭니다. `name`, `appData` 및 `settings`이(가) 필요합니다. `settings`은(는) `fragmentType` 및 `supportedChannels`을(를) 포함해야 합니다.

### 요청

```http
POST /rest/asset/v2/fragment
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment",
  "description": "Reusable hero block",
  "appData": {
    "workspaceId": "1001",
    "folderId": "395",
    "editorType": "fragment"
  },
  "settings": {
    "fragmentType": "email",
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "bd57#1900ab1509d",
  "result": [
    {
      "id": "13",
      "name": "Hero Banner Fragment",
      "status": "draft"
    }
  ]
}
```

요청 본문에는 `data`, `editorContext`, `themeId`, `appType` 및 `status`도 포함될 수 있습니다.

### 필드 만들기

* `appData`은(는) 조각이 저장된 위치와 편집 방법을 식별합니다.
* `settings.fragmentType`은(는) 전자 메일 조각과 같은 조각 범주를 식별합니다.
* `settings.fragmentSubType`을(를) 사용하여 조각 형식을 추가로 정의할 수 있습니다.
* `settings.supportedChannels`은(는) 조각을 사용할 수 있는 채널을 나열합니다.

## 업데이트

자산 ID별로 조각을 업데이트합니다.

### 요청

```http
POST /rest/asset/v2/fragment/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment v2",
  "description": "Updated reusable hero block",
  "settings": {
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "73d9#1900ab150f0",
  "result": [
    {
      "id": "13"
    }
  ]
}
```

## 상태 관리

조각은 초안 및 승인된 주기를 사용합니다. 상태 전환 끝점을 사용하여 조각을 승인하거나, 승인을 취소하거나, 초안을 삭제하거나, 새 초안을 만듭니다.

유효한 `action` 값은 다음과 같습니다.

* `approve`
* `unapprove`
* `discard`
* `create_draft`

### 요청

```http
POST /rest/asset/v2/fragment/state/transition
Content-Type: application/json
```

### 응답

```json
{
  "contentId": "13",
  "action": "approve"
}
```

## 복제

클론 끝점을 사용하여 기존 조각의 복제본을 생성합니다.

### 요청

```http
POST /rest/asset/v2/fragment/clone
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "13",
  "newAsset": {
    "name": "Hero Banner Fragment Copy",
    "description": "Cloned fragment"
  }
}
```

## 삭제

자산 ID로 조각을 삭제합니다.

### 요청

```http
POST /rest/asset/v2/fragment/{id}/delete
Content-Type: application/json
```

이 끝점은 경로에서 조각 ID를 가져오며 요청 본문을 정의하지 않습니다.

## 사용 주체

지정된 조각을 참조하는 자산을 검색하려면 `usedby` 끝점을 사용하십시오.

### 요청

```http
POST /rest/asset/v2/fragment/usedby
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "13",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```
