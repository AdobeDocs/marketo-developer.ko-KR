---
title: "다이내믹 콘텐츠"
feature: REST API, Dynamic Content
description: "Marketo API를 사용하여 다이내믹 콘텐츠를 구성합니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# 다이내믹 콘텐츠

Marketo은 여러 에셋 유형에 대한 리드 세분화를 통해 다이내믹 콘텐츠를 쉽게 사용할 수 있습니다.

- 이메일
- 랜딩 페이지
- 코드 조각

## 개요

다이내믹 콘텐츠는 선택한 세분화 내의 세그먼트에서 자격을 기반으로 잠재 고객에게 제공될 섹션의 특정 변형을 지정하여 섹션 수준에서 구현됩니다. 컨텐츠 조각이 특정 세그먼테이션을 기반으로 다이내믹 컨텐츠를 제공하도록 구성된 경우 해당 컨텐츠를 보는 리드는 해당 컨텐츠에 속하는 세그먼트와 일치하는 컨텐츠 변형 또는 세그먼트에 적합하지 않은 경우 기본 컨텐츠를 제공합니다.

## 예

이메일 사례를 통해 지역(미국) 세분화가 있으며 캘리포니아, 네바다, 유타, 콜로라도, 애리조나 및 뉴멕시코 리드를 포함하는 남서부 세그먼트에 속하는 리드에 대해서만 이벤트 프로모션을 표시하려고 합니다. 이를 위해 ID가 &quot;Q1-promotion-banner&quot;인 이메일의 섹션을 DynamicContent 섹션으로 편집 가능하게 만듭니다. 이렇게 하려면 다음을 사용해야 합니다. [이메일 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailComponentContentUsingPOST) 이메일의 엔드포인트. 다음 `value` 매개 변수는 세그먼테이션의 ID를 지정하는 데 사용됩니다.

참고: 이메일과 랜딩 페이지 모두 이 패턴을 따릅니다. 스니펫에는 다른 패턴이 있으며, 자세한 내용은 스니펫 API 설명서를 참조하십시오.

다음 예제는 섹션을 세그먼테이션(1001)에 의해 세그먼트화된 다이내믹 콘텐츠 섹션으로 설정합니다.

```
POST /rest/asset/v1/email/{id}/content/Q1-promotion-banner.json
```

```
type=DynamicContent&value=1001
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "891b#1729b34b9a5",
  "warnings": [],
  "result": [
    {
      "id": 1909
    }
  ]
}
```

개별 세그먼트에 대한 컨텐츠를 추가하려면 를 호출해야 합니다. [이메일 다이내믹 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails/operation/updateEmailDynamicContentUsingPOST) 특정 섹션의 끝점입니다.

다음 예제에서는 섹션이 기본값이 아닌 남서부 세그먼트에 있는 리드에 대한 특수 배너 이미지를 표시하도록 설정합니다. 더 많은 세그먼트에 대해 더 많은 변형을 만들려면 각 세그먼트 및 섹션에 대해 이 엔드포인트를 다시 호출합니다.

```
POST /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json
```

```
segment=Southwest&type=HTML&value=<img src='//www.example.com/SuperSpecialBannerForAmericanSouthwestLeads.jpg'/>
```

```json
{
  "success": true,
  "errors": [],
  "requestId": "891b#1729b34b9a5",
  "warnings": [],
  "result": [
    {
      "id": 1637
    }
  ]
}
```

## 세분화

세그먼테이션은 Marketo 다이내믹 컨텐츠의 핵심입니다. 세분화는 전체 리드 데이터베이스에 대해 위에서 아래로 평가되는 개별 규칙 세트의 사용자 정의 목록입니다. 리드는 각 세그먼테이션에서 한 개의 세그먼트로만 구성될 수 있으며 각 세그먼테이션에서 자격을 얻은 첫 번째 세그먼트의 멤버가 됩니다. 세그먼트에 적합하지 않은 경우 기본 세그먼트의 멤버가 되며, 해당 세그먼테이션을 사용하여 주어진 동적 컨텐츠에 대한 기본 컨텐츠를 받게 됩니다.

### 목록

세그먼트에는 사용 가능한 세그먼트 목록과 함께 응답을 반환하는 목록 끝점이 있습니다.

```
GET /rest/asset/v1/segmentation.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "78eb#14e9de95868",
  "result": [
    {
      "id": 1001,
      "name": "My Industry Segmentation",
      "description": "",
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:10Z+0000",
      "url": "https://app-abm.marketo.com/#SG1001A1",
      "folder": {
        "type": "Program",
        "value": 396,
        "folderName": null
      },
      "status": "approved",
      "workspace": "Default"
    },
    {
      "id": 1002,
      "name": "My Country Segmentation",
      "description": "",
      "createdAt": "2015-04-06T18:28:23Z+0000",
      "updatedAt": "2015-04-06T18:37:18Z+0000",
      "url": "https://app-abm.marketo.com/#SG1002A1",
      "folder": {
        "type": "Program",
        "value": 396,
        "folderName": null
      },
      "status": "approved",
      "workspace": "Default"
    }
  ]
}
```

세그먼트에는 상위 세그먼테이션의 세그먼트 목록과 함께 응답을 반환하는 엔드포인트도 있습니다.

```
GET /rest/asset/v1/segmentation/1001/segments.json
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "2031#14e9df08796",
  "result": [
    {
      "id": 1001,
      "name": "Manufacturing",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1002,
      "name": "Healthcare",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769688A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1003,
      "name": "Financial",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769690A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1004,
      "name": "Technology",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769692A1",
      "status": "approved",
      "segmentationId": 1001
    },
    {
      "id": 1005,
      "name": "Default",
      "description": null,
      "createdAt": "2015-04-06T18:23:32Z+0000",
      "updatedAt": "2015-04-06T18:37:09Z+0000",
      "url": "https://app-abm.marketo.com/#SL769694A1",
      "status": "approved",
      "segmentationId": 1001
    }
  ]
}
```
