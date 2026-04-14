---
title: 이메일 템플릿
feature: REST API
description: Marketo Asset REST API를 사용하여 이메일 템플릿에 대한 종속성을 쿼리, 생성, 업데이트, 복제, 삭제, 승인 및 검사할 수 있습니다.
exl-id: 50bb0047-d6ea-4c94-a900-18c37b17a147
source-git-commit: 59684e1c5a8082ad12f1e4bfc854c0d2dde35d2a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 9%

---

# 이메일 템플릿

[이메일 템플릿 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Email-Templates)

이메일 템플릿은 이메일을 만들 때 사용되는 구조 및 재사용 가능한 레이아웃을 정의합니다.

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

자산 ID별로 또는 필터 끝점을 사용하여 이메일 템플릿 메타데이터를 검색할 수 있습니다.

### ID별

#### 요청

```http
GET /rest/asset/v2/emailtemplate/{id}
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "14f9e#1900ab14001",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "description": "Core responsive template",
      "status": "draft"
    }
  ]
}
```

### 필터

필터 끝점은 작업 영역 내에서 검색하고 추가 쿼리 매개 변수로 결과 범위를 좁힐 수 있습니다. `workspaceId`은(는) 필수입니다.

지원되는 필터에는 `folderId`, 반복된 `folderIds`, 반복된 `status`, `pageIndex`, `pageSize`, `createdBy`, `createdAtStart`, `createdAtEnd`, `modifiedBy`, `modifiedAtStart`, `modifiedAtEnd`, `name`, `sortKey`, `sortOrder`, `isCreatedByMe`, `isModifiedByMe`, `scriptEngine`, `isValueNonNullable` 및 `includeArchived`이 포함됩니다.

#### 요청

```http
GET /rest/asset/v2/emailtemplate/filter?workspaceId=1001&name=Newsletter&pageIndex=0&pageSize=20
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "33c4#1900ab1402f",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

이름별로 템플릿을 찾아야 하는 경우에는 `name` 매개 변수를 사용하십시오.

## 만들기

JSON 페이로드를 전송하여 이메일 템플릿을 만듭니다. `name` 및 `appData`은(는) 필수입니다. `appData`에는 `folderId` 또는 `workspaceId` 이상이 포함되어야 합니다.

### 요청

```http
POST /rest/asset/v2/emailtemplate
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template",
  "description": "Core responsive template",
  "appData": {
    "workspaceId": "1001",
    "folderId": "15",
    "editorType": "emailTemplate"
  },
  "themeId": "42"
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "a99f#1900ab1407e",
  "result": [
    {
      "id": "1022",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

요청 본문에는 `data`, `editorContext`, `appType` 및 `status`도 포함될 수 있습니다.

### 필드 만들기

`appData`은(는) 서식 파일이 저장된 위치와 편집 방법을 식별합니다.

해당되는 경우 `themeId`을(를) 사용하여 테마와 템플릿을 연결할 수 있습니다.

## 업데이트

자산 ID로 템플릿을 업데이트합니다.

### 요청

```http
POST /rest/asset/v2/emailtemplate/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template v2",
  "description": "Updated responsive template",
  "appData": {
    "folderId": "15"
  }
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "cf10#1900ab140b3",
  "result": [
    {
      "id": "1022"
    }
  ]
}
```

## 상태 관리

이메일 템플릿은 초안 및 승인된 라이프사이클을 사용합니다. 상태 전환 끝점을 사용하여 템플릿을 승인하거나, 승인을 취소하거나, 초안을 삭제하거나, 새 초안을 만듭니다.

유효한 `action` 값은 다음과 같습니다.

- `approve`
- `unapprove`
- `discard`
- `create_draft`

### 요청

```http
POST /rest/asset/v2/emailtemplate/state/transition
Content-Type: application/json
```

### 응답

```json
{
  "contentId": "1022",
  "action": "approve"
}
```

## 복제

복제 끝점을 사용하여 기존 템플릿의 사본을 생성합니다.

### 요청

```http
POST /rest/asset/v2/emailtemplate/clone
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "1022",
  "newAsset": {
    "name": "Base Newsletter Template Copy",
    "description": "Cloned template"
  }
}
```

## 삭제

자산 ID로 템플릿을 삭제합니다.

### 요청

```http
POST /rest/asset/v2/emailtemplate/{id}/delete
Content-Type: application/json
```

이 끝점은 경로에서 템플릿 ID를 가져오며 요청 본문을 정의하지 않습니다.

## 사용 주체

지정된 템플릿을 참조하는 자산을 검색하려면 `usedby` 끝점을 사용하십시오.

### 요청

```http
POST /rest/asset/v2/emailtemplate/usedby
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "1022",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```

## 참고

쿼리 끝점이 에셋에 대한 메타데이터를 반환합니다. 전체 응답 스키마 및 환경별 속성에 대해 끝점 참조를 사용합니다.
