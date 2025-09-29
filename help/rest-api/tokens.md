---
title: 토큰
feature: REST API, Tokens
description: Asset REST API를 사용하여 Marketo 내 토큰을 관리합니다. 지원되는 데이터 유형, 폴더 또는 프로그램별로 가져오기, 양식으로 인코딩된 POST를 통해 만들기 또는 업데이트 및 이름별 삭제 를 참조하십시오.
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 3%

---

# 토큰

[토큰 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens)

Marketo의 토큰은 런타임에 별도의 데이터로 대체되는 단축 코드와 유사한 특수 문자열입니다. Marketo에는 여러 유형의 토큰이 사용할 수 있지만 API를 통해 내 토큰만 편집할 수 있습니다. 내 토큰은 특정 폴더 또는 프로그램에 대해 로컬인 하위 토큰입니다. API를 통해 토큰을 읽고, 만들고, 삭제할 수 있습니다.

## 데이터 유형

다음 데이터 유형을 사용하여 토큰을 만들 수 있습니다.

| 유형 | 설명 |
|---------------|----------------------------------------------------|
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

API를 통해 토큰을 생성할 때 사용할 수 있는 유일한 데이터 유형입니다.

## 쿼리

[폴더 ID별 토큰 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/getTokensByFolderIdUsingGET)에서는 `id`을(를) 프로그램 또는 폴더 유형의 경로 매개 변수로 사용합니다. 이 형식은 `folderType` 매개 변수에 의해 지정됩니다.

```curl
GET /rest/asset/v1/folder/{id}/tokens.json?folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "4fbe#14e27fc9bbf",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "AprilFool - deverly",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}
```

## 만들기 및 업데이트

[토큰 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/addTokenTOFolderUsingPOST) 끝점이 토큰을 만들거나 토큰이 존재하는 경우 제출된 값으로 업데이트합니다. 토큰은 폴더 또는 프로그램의 컨텍스트에서 만들어집니다. 필수 `id` 경로 매개 변수는 토큰이 연결될 폴더의 ID입니다. `name`, `type`, `value` 및 `folderType`은(는) 모두 토큰의 필수 매개 변수입니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다. 토큰의 `name` 필드는 50자를 초과할 수 없습니다.

```
POST /rest/asset/v1/folder/{id}/tokens.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=April Fools&type=date&value=2015-04-01&folderType=Folder
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

## 삭제

[이름별 Delete 토큰](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/deleteTokenByNameUsingPOST)은(는) ID를 프로그램 또는 폴더 형식의 경로 매개 변수로 사용합니다. 이 형식은 `folderType` 매개 변수에 의해 지정됩니다. 토큰은 상위 폴더, `name` 및 토큰의 `type`을(를) 기반으로 삭제되며, 각 폴더는 필수입니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

```
POST /rest/asset/v1/folder/{id}/tokens/delete.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=AprilFool - deverly&type=date&folderType=Program
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "12ed2#14e2800f89c",
    "result": [
        {
            "id": 416
        }
    ]
}
```
