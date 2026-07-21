---
title: 토큰
feature: REST API, Tokens
description: Asset REST API를 사용하여 Marketo 내 토큰을 관리합니다. 지원되는 데이터 유형, 폴더 또는 프로그램별로 가져오기, 양식으로 인코딩된 POST를 통해 만들기 또는 업데이트 및 이름별 삭제 를 참조하십시오.
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
TQID: https://experienceleague.adobe.com/uqOpu2vDuiQiZhILKuxZJQGadd0K14zwIaAdmNfK1-I
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 290
ht-degree: 3%

---

# 토큰

[토큰 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens)

토큰은 Marketo이 런타임에 다른 데이터로 대체하는 문자열입니다. API는 폴더 또는 프로그램에 대해 로컬인 하위 토큰인 내 토큰만 편집할 수 있습니다.

토큰 API를 사용하여 내 토큰을 읽고, 만들고, 업데이트하고, 삭제합니다.

## 데이터 유형

다음 데이터 유형을 사용하여 토큰을 만들 수 있습니다.

| 유형 | 설명 |
| --- | --- |
| 날짜 | &quot;yyyy-MM-dd&quot; 형식의 날짜 값 |
| 번호 | 정수 또는 부동 소수점 숫자 |
| 리치 텍스트 | HTML 문자열 |
| 점수 | 부호 있는 32비트 정수 |
| sfdc 캠페인 | Salesforce 캠페인 관리 통합에 사용됨 |
| 텍스트 | 텍스트 문자열 |

API는 토큰을 생성할 때 이러한 데이터 유형만 지원합니다.

## 쿼리

[폴더 ID별 토큰 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/getTokensByFolderIdUsingGET)는 프로그램 또는 폴더의 ID를 경로 매개 변수로 사용합니다. `folderType` 매개 변수를 사용하여 형식을 지정하십시오.

```http
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

[토큰 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/addTokenTOFolderUsingPOST) 끝점은 토큰을 만들거나 기존 토큰을 제출된 값으로 업데이트합니다. 토큰은 폴더 또는 프로그램에 속합니다.

`id` 경로 매개 변수는 상위 폴더를 식별합니다. `name`, `type`, `value` 및 `folderType` 매개 변수가 필요합니다. 데이터를 JSON이 아닌 POST `x-www-form-urlencoded`(으)로 전달합니다. 토큰 `name`은(는) 50자를 초과할 수 없습니다.

```http
POST /rest/asset/v1/folder/{id}/tokens.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

[이름별 Delete 토큰](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/deleteTokenByNameUsingPOST)은(는) 프로그램 또는 폴더의 ID를 경로 매개 변수로 사용합니다. `folderType`을(를) 사용하여 형식을 지정하십시오.

상위 폴더, 토큰 `name` 및 토큰 `type`이(가) 필요합니다. 데이터를 JSON이 아닌 POST `x-www-form-urlencoded`(으)로 전달합니다.

```http
POST /rest/asset/v1/folder/{id}/tokens/delete.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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
