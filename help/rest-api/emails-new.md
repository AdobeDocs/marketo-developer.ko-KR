---
title: 이메일
feature: REST API
description: Marketo Asset REST API를 사용하여 이메일 에셋에 대한 종속성을 쿼리, 생성, 업데이트, 복제, 삭제, 승인 및 검사할 수 있습니다.
exl-id: b41a3ae5-2b25-4103-84b4-320fc2c44bd6
source-git-commit: e2606d6cb12c572603ff069617de58417e43ca63
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# 이메일

[이메일 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails_New)

이메일은 메시지 메타데이터, 콘텐츠 구성, 설정 및 승인 상태를 정의하는 에셋 레코드입니다.

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

자산 `id` 또는 필터 끝점을 사용하여 전자 메일 메타데이터를 검색할 수 있습니다.

### ID별

#### 요청

```http
GET /rest/asset/v2/email/{id}
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7b3c#1900ab12cd3",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "description": "Main announcement email",
      "status": "draft"
    }
  ]
}
```

### 필터

필터 끝점은 작업 영역 내에서 검색하고 추가 쿼리 매개 변수로 결과 범위를 좁힐 수 있습니다.

`workspaceId`은(는) 필수입니다.

지원되는 쿼리 매개 변수:

| 매개변수 | 설명 |
| - | - |
| `workspaceId` | 필터 요청의 범위를 지정하는 데 사용되는 필수 작업 영역 식별자입니다. |
| `folderId` | 결과를 단일 폴더로 필터링합니다. |
| `folderIds` | 필터링하는 반복된 매개 변수로 인해 여러 폴더가 생성됩니다. |
| `status` | 하나 이상의 이메일 상태별로 필터링하는 반복된 매개 변수입니다. |
| `pageIndex` | 페이지 매김된 결과에 대한 0부터 시작하는 페이지 인덱스입니다. |
| `pageSize` | 페이지당 반환할 최대 결과 수. |
| `createdBy` | 생성 사용자로 결과를 필터링합니다. |
| `createdAtStart` | 이 타임스탬프에서 또는 그 이후에 생성된 에셋을 반환합니다. |
| `createdAtEnd` | 이 타임스탬프나 그 이전에 생성된 에셋을 반환합니다. |
| `modifiedBy` | 마지막 수정 사용자로 결과를 필터링합니다. |
| `modifiedAtStart` | 이 타임스탬프에서 또는 그 이후에 수정된 자산을 반환합니다. |
| `modifiedAtEnd` | 이 타임스탬프에서 또는 그 이전에 수정된 자산을 반환합니다. |
| `name` | 결과를 이메일 이름으로 필터링합니다. |
| `sortKey` | 결과 정렬에 사용되는 필드를 선택합니다. |
| `sortOrder` | 정렬 방향을 설정합니다. |
| `isCreatedByMe` | 현재 사용자가 만든 에셋으로 결과를 제한합니다. |
| `isModifiedByMe` | 현재 사용자가 마지막으로 수정한 에셋으로 결과를 제한합니다. |
| `templateId` | 템플릿 식별자로 결과를 필터링합니다. |
| `scriptEngine` | 결과를 스크립트 엔진 구성으로 필터링합니다. |
| `isValueNonNullable` | 값이 Null을 허용하지 않는지 여부를 기준으로 필터링합니다. |
| `includeArchived` | 결과에 보관된 에셋을 포함합니다. |

#### 요청

```http
GET /rest/asset/v2/email/filter?workspaceId=1001&name=Spring%20Launch&status=draft&status=approved&pageIndex=0&pageSize=20
```

#### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "5dd1#1900ab13011",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

이름으로 전자 메일을 찾아야 할 때는 `name` 매개 변수를 사용하십시오.

## 만들기

JSON 페이로드를 전송하여 이메일을 만듭니다. `name`, `appData` 및 `headers`이(가) 필요합니다. `headers.subject`은(는) 필수이며 `appData`은(는) `folderId`, `workspaceId` 또는 `programId` 중 하나 이상을 포함해야 합니다.

### 요청

```http
POST /rest/asset/v2/email
Content-Type: application/json
```

```json
{
  "name": "Spring Launch Email",
  "description": "Main announcement email",
  "appData": {
    "workspaceId": "1001",
    "folderId": "2002",
    "editorType": "email"
  },
  "headers": {
    "subject": "Introducing the Spring Launch",
    "fromName": "Marketing Team",
    "fromEmail": "marketing@example.com",
    "replyEmail": "reply@example.com",
    "preheader": "See what changed this quarter",
    "ccEmails": [
      "owner@example.com"
    ]
  },
  "settings": {
    "isOperational": false,
    "isTextOnly": false,
    "isWebPageView": true,
    "enableUrlTracking": true
  },
  "templateId": "3003"
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "238c#1900ab1313f",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

요청 본문에는 `data`, `editorContext`, `themeId`, `appType` 및 `status`도 포함될 수 있습니다.

### 필드 만들기

* `appData`은(는) 전자 메일이 만들어진 위치와 편집 방법을 식별합니다.
* `headers`에는 제목, 보낸 사람, 회신 주소, 사전 머리글 및 선택적 참조 받는 사람을 포함한 메시지 머리글 값이 포함되어 있습니다.
* `settings`은(는) 텍스트 전용 모드, 웹 페이지 보기 및 URL 추적과 같은 작동 및 렌더링 동작을 제어합니다.
* `templateId`은(는) 전자 메일을 만들 때 사용되는 전자 메일 템플릿을 식별합니다.

## 업데이트

자산 ID로 이메일을 업데이트합니다. 요청 본문에서 `UpdateEmailRequest` 스키마를 사용하며, 모든 속성은 선택 사항이므로 변경할 필드만 보낼 수 있습니다.

### 요청

```http
POST /rest/asset/v2/email/{id}/update
Content-Type: application/json
```

```json
{
  "description": "Updated announcement email",
  "headers": {
    "subject": "Spring Launch Is Live",
    "preheader": "Read the latest release notes"
  },
  "settings": {
    "enableUrlTracking": true,
    "isWebPageView": true
  }
}
```

### 응답

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "9fd3#1900ab13210",
  "result": [
    {
      "id": "1017"
    }
  ]
}
```

## 상태 관리

이메일은 초안 및 승인된 라이프사이클을 사용합니다. 상태 전환 끝점을 사용하여 이메일을 승인하거나, 승인을 취소하거나, 초안을 삭제하거나, 새 초안을 만듭니다.

유효한 `action` 값은 다음과 같습니다.

* `approve`
* `unapprove`
* `discard`
* `create_draft`

### 요청

```http
POST /rest/asset/v2/email/state/transition
Content-Type: application/json
```

### 응답

```json
{
  "contentId": "1017",
  "action": "approve"
}
```

## 복제

복제 끝점을 사용하여 기존 이메일의 사본을 만듭니다.

### 요청

```http
POST /rest/asset/v2/email/clone
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "1017",
  "newAsset": {
    "name": "Spring Launch Email Copy",
    "description": "Cloned from Spring Launch Email"
  }
}
```

## 삭제

자산 ID로 이메일을 삭제합니다.

### 요청

```http
POST /rest/asset/v2/email/{id}/delete
Content-Type: application/json
```

이 끝점은 경로에서 자산 `id`을(를) 가져오며 요청 본문을 정의하지 않습니다.

## 사용 주체

지정된 전자 메일을 참조하는 자산을 검색하려면 `usedby` 끝점을 사용하십시오.

### 요청

```http
POST /rest/asset/v2/email/usedby
Content-Type: application/json
```

### 응답

```json
{
  "assetId": "1017",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```

## 참고

쿼리 끝점이 에셋에 대한 메타데이터를 반환합니다. 사용 가능한 필드의 전체 스키마 및 환경별 속성에 대해 끝점 참조를 사용합니다.
