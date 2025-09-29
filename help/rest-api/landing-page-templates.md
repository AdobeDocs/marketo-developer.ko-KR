---
title: 랜딩 페이지 템플릿
feature: REST API, Landing Pages
description: 자유 형식 및 안내 유형에 대한 REST API 엔드포인트를 통해 Marketo 랜딩 페이지 템플릿을 관리하고 ID 또는 이름별로 쿼리하며, HTML을 만들고, 업데이트하고, 복제하고, Munchkin합니다.
exl-id: f9d1255e-ec13-4b75-96d5-b4cc9457a51b
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# 랜딩 페이지 템플릿

[랜딩 페이지 템플릿 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates)

랜딩 페이지 템플릿은 개별 Marketo 랜딩 페이지에 대한 상위 리소스 및 종속성입니다. 랜딩 페이지는 상위 템플릿에서 해당 콘텐츠의 골격을 가져옵니다.

## 템플릿 유형

Marketo에는 자유 양식과 안내식의 두 가지 유형의 랜딩 페이지 템플릿이 있습니다. 자유 양식 랜딩 페이지 템플릿은 템플릿에서 파생된 페이지에 느슨한 구조의 편집 환경을 제공합니다. 안내식 템플릿은 템플릿 수준에서 요소 유형 및 위치를 제한할 수 있는 상당히 구조화된 경험을 제공합니다. 차이점에 대한 자세한 내용은 [이 문서](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/understanding-landing-pages/understanding-free-form-vs-guided-landing-pages)를 참조하세요.

## 쿼리

랜딩 페이지 템플릿은 [ID별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplateByNameUsingGET) 및 [탐색](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/getLandingPageTemplatesUsingGET)의 자산에 대한 표준 쿼리 유형을 지원합니다. 이러한 엔드포인트는 템플릿에 대한 메타데이터를 반환합니다. 템플릿의 HTML 컨텐츠 검색은 해당 ID를 통해 템플릿별로 수행해야 합니다.

## 만들기 및 업데이트

템플릿은 연결된 메타데이터가 있는 빈 에셋으로 만들어집니다. 템플릿을 만들 때 선택적 설명, templateType 및 enableMunchkin 매개 변수와 함께 이름 및 폴더를 포함해야 합니다. templateType은 자유 형식 또는 안내식 중 하나일 수 있으며 기본값은 freeForm입니다. 유형 간의 차이점에 대해서는 안내식 및 자유 형식 섹션을 참조하십시오. enableMunchkin의 기본값은 false이며, 이 경우 템플릿의 하위 랜딩 페이지에서 Munchkin 추적이 수행되지 않습니다.

```
POST /rest/asset/v1/landingPageTemplates.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

템플릿의 콘텐츠는 [랜딩 페이지 템플릿 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLandingPageTemplateContentUsingPOST) 끝점을 통해 별도로 채워야 합니다.

### 메타데이터 업데이트

랜딩 페이지 템플릿의 메타데이터는 [랜딩 페이지 템플릿 메타데이터 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Landing-Page-Templates/operation/updateLpTemplateUsingPOST) 끝점을 통해 업데이트할 수 있습니다. 이름, 설명 및 enableMunchkin 설정은 이러한 방식으로 업데이트할 수 있습니다.

### 컨텐츠 업데이트

랜딩 페이지 템플릿의 콘텐츠는 HTML 콘텐츠 전체에 대한 파괴적인 업데이트로 만들어집니다. 컨텐츠는 multipart/form-data로 전달되어야 하며 유일한 매개 변수는 content입니다.

```
POST /rest/asset/v1/landingPageTemplate/286/content.json
```

```
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

```
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

Marketo에서는 랜딩 페이지 템플릿을 복제하는 간단한 방법을 제공합니다. application/x-www-url-formencoded POST 요청입니다.

`id` 경로 매개 변수는 복제할 소스 랜딩 페이지 템플릿의 ID를 지정합니다.

`name` 매개 변수는 새 랜딩 페이지 템플릿의 이름을 지정하는 데 사용됩니다.

`folder` 매개 변수는 새 랜딩 페이지 템플릿이 위치할 상위 폴더를 지정하는 데 사용됩니다. 다음을 포함하는 포함된 JSON 개체의 형식입니다  `id` 및 `type`.

선택적 `description` 매개 변수는 새 랜딩 페이지 템플릿을 설명하는 데 사용됩니다.

```
POST /rest/asset/v1/landingPageTemplate/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

랜딩 페이지 템플릿은 초안 버전 및/또는 승인된 버전이 있을 수 있는 표준 초안 승인 모델을 따릅니다. 템플릿에 업데이트가 적용될 때마다 항상 초안 버전에 먼저 적용되며 템플릿이 승인된 경우에만 실시간으로 표시됩니다.

템플릿을 승인하려면 유형에 대한 규칙(자유 형식의 안내)을 준수해야 합니다. 해당 유형의 템플릿을 만들고 승인하기 위한 요구 사항에 대한 자세한 내용은 해당 만들기 문서를 참조하십시오.

- [자유 형식 랜딩 페이지 템플릿](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-free-form-landing-page-template)
- [안내 랜딩 페이지 템플릿](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/create-a-guided-landing-page-template)
- [안내식 템플릿 예제](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/landing-pages/landing-page-templates/guided-landing-page-template-list)

## 삭제

템플릿을 삭제하려면 해당 템플릿이 사용 중이 아니어야 하며 승인되지 않아야 합니다. 즉, 하위 랜딩 페이지에서 템플릿을 참조할 수 없습니다.  이 API를 사용하면 소셜 버튼이 포함된 랜딩 페이지 템플릿을 삭제할 수 없습니다.
