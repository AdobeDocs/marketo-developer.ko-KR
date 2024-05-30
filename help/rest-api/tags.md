---
title: "태그"
feature: REST API, Tags
description: "Marketo의 프로그램에 대한 태그를 관리합니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# 태그

[태그 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tags)

태그는 프로그램에 대해 사용자가 정의한 필드입니다. 각 태그는 하나 이상의 프로그램 유형에 적용될 수 있으며, 태그 정의 방법에 따라 필수 또는 선택 사항일 수 있습니다. 태그는 사용을 위해 선택해야 하는 허용 값 목록을 제공할 수도 있습니다.

## 쿼리

태그는 표준 자산 패턴으로 쿼리되지만 ID별 끝점이 없습니다. 태그에 대해 허용되는 값 목록은 이름별로 태그를 쿼리할 때만 반환됩니다.

### 태그 가져오기

```
GET /rest/asset/v1/tagTypes.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1488a#1504ecfccf8",
    "result": [
        {
            "tagType": "AAA1 Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": true
        },
        {
            "tagType": "AAA2 Required Event Tag Type",
            "applicableProgramTypes": "[event]",
            "required": true
        },
        {
            "tagType": "AAA3 Not Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": false
        }
    ]
}
```

### 이름별

```
GET /rest/asset/v1/tagType/byName.json?name=AAA1 Required Tag Type
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "8a44#1504ed0da2f",
    "result": [
        {
            "tagType": "AAA1 Required Tag Type",
            "applicableProgramTypes": "[program,email_batch,nurture,event,webinar]",
            "required": true,
            "allowableValues": "[AAA1 RT1, AAA1 RT2, AAA1 RT3, AAA1 RT4]"
        }
    ]
}
```

## 업데이트

다음 [프로그램 태그 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) 끝점을 사용하면 지정된 태그 유형의 값을 업데이트할 수 있습니다. 끝점은 `id` 및 `tagType` 업데이트할 프로그램 id와 태그 유형을 지정하는 경로 매개 변수입니다. A `tagValue` 쿼리 매개 변수는 태그 유형의 새 값을 지정하는 데 사용됩니다. 모든 매개 변수가 필요합니다.

```
POST /rest/asset/v1/program/{id}/tag/{tagType}.json?tagValue=David
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "fd84#17f84a885a6",
    "warnings": [],
    "result": [
        {
            "id": 1067
        }
    ]
}
```

태그를 일괄적으로 업데이트할 수 있는 방법은 [프로그램 메타데이터 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) 엔드포인트. 예를 찾을 수 있습니다. [여기](programs.md#update).

## 삭제

다음 [프로그램 태그 삭제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/deleteProgramUsingPOST) 끝점을 사용하면 필요하지 않은 태그 유형을 삭제할 수 있습니다. 끝점은 다음을 수행합니다. `id` 및 `tagType` 삭제할 프로그램 id 및 태그 유형을 지정하는 경로 매개 변수입니다.

```
POST /rest/asset/v1/program/{id}/tag/{tagType}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "d998#17f84ad36a7",
    "warnings": [],
    "result": [
        {
            "id": 1067
        }
    ]
}
```
