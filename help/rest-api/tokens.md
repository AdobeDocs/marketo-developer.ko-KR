---
title: "토큰"
feature: REST API, Tokens
description: "Marketo에서 토큰을 관리합니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

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

[폴더 ID별 토큰 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/getTokensByFolderIdUsingGET) 다음 항목 가져오기 `id` 를 프로그램 또는 폴더 유형의 경로 매개 변수로 사용합니다. 이 유형은 다음에서 지정합니다. `folderType` 매개 변수.

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

다음 [토큰 만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/addTokenTOFolderUsingPOST) 끝점은 토큰을 만들거나 존재하는 경우 제출된 값으로 업데이트합니다. 토큰은 폴더 또는 프로그램의 컨텍스트에서 만들어집니다. 필수 `id` path 매개 변수는 토큰이 연결될 폴더의 id입니다. 다음 `name`, `type`, `value`, 및 `folderType` 는 토큰의 모든 필수 매개 변수입니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다. 다음 `name` 토큰의 필드는 50자를 초과할 수 없습니다.

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

[이름별 토큰 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tokens/operation/deleteTokenByNameUsingPOST) 는 id를 프로그램 또는 폴더 유형의 경로 매개 변수로 사용합니다. 이 유형은 다음에서 지정합니다. `folderType` 매개 변수. 토큰은 상위 폴더인 `name`및 `type` 각 토큰이 필요합니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

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
