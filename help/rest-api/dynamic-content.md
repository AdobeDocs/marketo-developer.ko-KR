---
title: 동적 콘텐츠
feature: REST API, Dynamic Content
description: 세분화를 사용하여 REST API를 통해 섹션 수준 Marketo 다이내믹 콘텐츠를 구성하여 엔드포인트 및 예를 통해 이메일, 랜딩 페이지 및 코드 조각을 개인화할 수 있습니다
exl-id: 8ab97624-5fb5-4a41-911f-ec8616dd43c9
TQID: https://experienceleague.adobe.com/MwfPxu74qk0bPZMr6yuxQi--e3gMvP1tXQZ5iMil02o
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 329
ht-degree: 3%

---

# 동적 콘텐츠

리드 세그먼트를 사용하여 다음 에셋 유형의 다이내믹 콘텐츠를 제공합니다.

- 이메일
- 랜딩 페이지
- 스니펫

## 개요

다이내믹 콘텐츠는 섹션 수준에서 작동합니다. 각 섹션은 선택한 세그먼테이션의 세그먼트에 대한 변형을 제공할 수 있습니다.

잠재 고객이 자산을 볼 때 Marketo에 잠재 고객의 세그먼트에 대한 변형이 표시됩니다. 잠재 고객이 세그먼트에 적합하지 않은 경우 Marketo에 기본 컨텐츠가 표시됩니다.

## 예

이 예에서는 지역(미국) 세분화를 사용하여 남서부 세그먼트의 리드에 대한 이벤트 판촉을 표시합니다. 해당 부문은 캘리포니아, 네바다, 유타, 콜로라도, 애리조나, 뉴멕시코에서 온 리드가 포함된다.

[전자 메일 콘텐츠 섹션 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailComponentContentUsingPOST) 끝점을 사용하여 ID가 `Q1-promotion-banner`인 편집 가능한 섹션을 `DynamicContent` 섹션으로 변경합니다. `value` 매개 변수는 세그먼테이션 ID를 지정합니다.

이메일 및 랜딩 페이지는 이 패턴을 따릅니다. 스니펫은 스니펫 API 설명서에 설명된 다양한 패턴을 사용합니다.

다음 예제는 섹션을 세그먼테이션(1001)에 의해 세그먼트화된 다이내믹 콘텐츠 섹션으로 설정합니다.

```http
POST /rest/asset/v1/email/{id}/content/Q1-promotion-banner.json
```

```text
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

[전자 메일 동적 콘텐츠 업데이트 섹션](https://developer.adobe.com/marketo-apis/api/asset#tag/Emails/operation/updateEmailDynamicContentUsingPOST) 끝점을 호출하여 특정 섹션의 세그먼트에 대한 콘텐츠를 추가하십시오.

다음 요청은 남서부 세그먼트의 잠재 고객에 대한 기본 콘텐츠 대신 특수 배너를 표시합니다. 변형을 더 만들려면 각 세그먼트 및 섹션에 대한 끝점을 호출합니다.

```http
POST /rest/asset/v1/email/{id}/dynamicContent/{dynamicContentId}.json
```

```text
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

세그멘테이션은 Marketo이 리드 데이터베이스에 대해 위에서 아래로 평가하는 규칙 세트의 사용자 정의 목록입니다. 리드는 각 세분화에서 하나의 세그먼트에만 속할 수 있습니다. 잠재 고객이 적격한 첫 번째 세그먼트에 참여합니다.

잠재 고객이 다른 세그먼트에 적합하지 않은 경우 기본 세그먼트에 참여하고 세그먼테이션의 기본 콘텐츠를 수신합니다.

### List

목록 끝점을 사용하여 사용 가능한 세그먼트를 검색합니다.

```http
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

세그먼트 끝점을 사용하여 상위 세그먼테이션의 세그먼트를 검색합니다.

```http
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
