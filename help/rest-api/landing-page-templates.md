---
title: 랜딩 페이지 템플릿
feature: REST API, Landing Pages
description: 자유 형식 및 안내 유형에 대한 REST API 엔드포인트를 통해 Marketo 랜딩 페이지 템플릿을 관리하고 ID 또는 이름별로 쿼리하며, HTML을 만들고, 업데이트하고, 복제하고, Munchkin합니다.
exl-id: f9d1255e-ec13-4b75-96d5-b4cc9457a51b
TQID: https://experienceleague.adobe.com/U9K1MG-q2gIgJMgfM3lt1S4olETt8ln9seOIKZUncBY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 519
ht-degree: 2%

---

# 랜딩 페이지 템플릿

[랜딩 페이지 템플릿 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates)

랜딩 페이지 템플릿은 Marketo 랜딩 페이지의 상위 리소스입니다. 각 랜딩 페이지는 상위 템플릿에서 초기 콘텐츠 구조를 파생합니다.

## 템플릿 유형

Marketo은 자유 형식의 안내 랜딩 페이지 템플릿을 제공합니다. 자유 형식 템플릿은 느슨한 구조의 편집 환경을 제공합니다. 안내식 템플릿은 템플릿 수준에서 요소 유형 및 위치를 제한할 수 있습니다.

자세한 비교는 [자유 형식 페이지와 안내식 랜딩 페이지 비교](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/understanding-landing-pages/understanding-free-form-vs-guided-landing-pages)를 참조하십시오.

## 쿼리

랜딩 페이지 템플릿 [ID별](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplateByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplateByNameUsingGET) 또는 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/getLandingPageTemplatesUsingGET)을(를) 쿼리합니다. 이러한 끝점은 템플릿 메타데이터를 반환합니다. ID별로 각 템플릿에 대해 개별적으로 HTML 컨텐츠를 검색합니다.

## 만들기 및 업데이트

템플릿은 메타데이터가 있는 빈 에셋으로 만들어집니다. `name` 및 `folder` 매개 변수가 필요합니다. `description`, `templateType` 및 `enableMunchkin` 매개 변수는 선택 사항입니다.

`templateType` 값은 `freeform` 또는 `guided`일 수 있으며 기본값은 `freeForm`입니다. `enableMunchkin` 값은 기본적으로 `false`(으)로 설정됩니다. 활성화되면 템플릿의 하위 랜딩 페이지에서 Munchkin 추적이 방지됩니다.

```http
POST /rest/asset/v1/landingPageTemplates.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=New LPT - PHP&folder={"id":12,"type":"Folder"}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "11b7#14dfe1e3bcf",
    "result": [
        {
            "id": 286,
            "name": "assetAPITest",
            "description": "test",
            "createdAt": "2015-06-16T20:45:03Z+0000",
            "updatedAt": "2015-06-16T20:45:03Z+0000",
            "url": "https://app-devlocal1.marketo.com/#LT286B2ZN12",
            "folder": {
                "type": "Folder",
                "value": 12,
                "folderName": "Templates"
            },
            "status": "draft",
            "workspace": "Default"
        }
    ]
}
```

[랜딩 페이지 템플릿 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/updateLandingPageTemplateContentUsingPOST) 끝점을 사용하여 템플릿 콘텐츠를 별도로 추가하십시오.

### 메타데이터 업데이트

[랜딩 페이지 템플릿 메타데이터 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Landing-Page-Templates/operation/updateLpTemplateUsingPOST) 끝점을 사용하여 이름, 설명 또는 `enableMunchkin` 설정을 변경합니다.

### 컨텐츠 업데이트

템플릿 콘텐츠를 업데이트하면 기존의 모든 HTML 콘텐츠가 바뀝니다. `content` 매개 변수에서 대체 요소를 `multipart/form-data`(으)로 전달합니다.

```http
POST /rest/asset/v1/landingPageTemplate/286/content.json
```

```html
content-type: multipart/form-data; boundary=--------------------------435851813185237176536801
----------------------------435851813185237176536801
Content-Disposition: form-data; name="content"; filename="content.txt"
Content-Type: text/plain

<html>
<head>
</head>
<body>
<div>Placeholder Content</div>
</body>
</html>
----------------------------435851813185237176536801--
```

```json
 {
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7516#14e0dc60bbc",
  "result": [
    {
      "id": 286
    }
  ]
}
```

## 복제

`application/x-www-url-formencoded` POST 요청으로 랜딩 페이지 템플릿을 복제합니다.

`id` 경로 매개 변수는 원본 랜딩 페이지 템플릿을 지정합니다.

`name` 매개 변수는 새 랜딩 페이지 템플릿의 이름을 지정합니다.

`folder` 매개 변수는 새 템플릿의 상위 폴더를 지정합니다. `id` 및 `type`을(를) 포함하는 포함된 JSON 개체로 전달합니다.

선택적 `description` 매개 변수는 새 템플릿을 설명합니다.

```http
POST /rest/asset/v1/landingPageTemplate/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=Standard Template Clone&folder={"type": "Folder", "id": 732}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "dee6#1683e9fd410",
    "warnings": [],
    "result": [
        {
            "id": 61,
            "name": "Standard Template Clone",
            "createdAt": "2019-01-11T20:34:48Z+0000",
            "updatedAt": "2019-01-11T20:34:48Z+0000",
            "url": "https://app-abm.marketo.com/#LT61B2ZN732",
            "folder": {
                "type": "Folder",
                "value": 732,
                "folderName": "Test LP Template Clone"
            },
            "status": "draft",
            "workspace": "Default",
            "templateType": "freeForm",
            "enableMunchkin": true
        }
    ]
}
```

## 승인

랜딩 페이지 템플릿은 표준 초안 및 승인된 모델을 사용합니다. 업데이트는 먼저 초안에 적용되며 템플릿이 승인된 후에만 라이브가 됩니다.

승인하기 전에 템플릿은 안내식 또는 자유 형식 유형에 대한 요구 사항을 충족해야 합니다. 다음 리소스를 참조하십시오.

- [자유 양식 랜딩 페이지 템플릿](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-free-form-landing-page-template)
- [가이드 랜딩 페이지 템플릿](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)
- [안내식 템플릿 예](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/guided-landing-page-template-list)

## 삭제

템플릿을 삭제하려면 템플릿이 승인되지 않았는지, 그리고 템플릿을 참조하는 하위 랜딩 페이지가 없는지 확인합니다. 이 API를 사용하여 소셜 버튼이 포함된 랜딩 페이지 템플릿을 삭제할 수 없습니다.
