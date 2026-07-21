---
title: 방문자 데이터 가져오기
description: 매개 변수, 콜백 예 및 세그먼트, ABM 및 위치에 대한 샘플 응답이 있는 RTP User Context API를 사용하여 실시간 방문자 식별을 가져옵니다.
feature: Javascript
exl-id: 39a2446d-8a31-461e-bbe6-a7edf24b4d52
TQID: https://experienceleague.adobe.com/B-JMACtMs3aRVsb1eJKaRoQGgVKB6MTbd0KBoZ7Ay6k
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 214
ht-degree: 4%

---

# 방문자 데이터 가져오기

이 방법을 사용하여 방문자 식별 데이터를 실시간으로 가져옵니다.

- User Context API를 사용하기 전에 웹 Personalization 고객이고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- RTP는 계정 기반 마케팅 명명된 계정 목록을 지원하지 않습니다. ABM 목록 및 코드는 RTP 내에서 관리되는 업로드된 계정 목록(CSV 파일)에만 해당됩니다.

오류가 발생하면 응답 JSON에 오류 메시지가 포함됩니다. API에서 500 코드를 반환하는 경우 지원팀에 문의하고 오류를 발생시킨 요청을 제공합니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
| --- | --- | --- | --- |
| `get` | 필수 | 문자열 | 메서드 작업. |
| `visitor` | 필수 | 문자열 | 메서드 이름입니다. |
| `callback` | 필수 | 함수 | 반환된 각 캠페인에 대해 트리거될 콜백 함수입니다. |

## 예

다음 예제에서는 방문자 식별 데이터를 가져옵니다.

```javascript
function callbackFunction() {
    console.log('RTP is awesome!');
}
rtp('get', 'visitor', callbackFunction);
```

세그먼트 일치가 있는 응답:

방문자가 방문자 데이터 가져오기 API 호출 전에 실시간 세그먼트와 일치하므로 다음 응답에는 `matchedSegments`이(가) 포함됩니다.

```json
{
    "status": 200,
    "results": {
        "matchedSegments": [
            {
                "name": "first click",
                "id": 177
            }
        ],
        "abm": [
            {
                "code": 4,
                "name": "abm_saleforce_customers"
            },
            {
                "code": 5,
                "name": "abm_top_customers"
            }
        ],
        "org": "Marketo",
        "location": {
            "country": "United States",
            "city": "San Mateo",
            "state": "CA"
        },
        "industries": [
            "Software & Internet"
        ],
        "isp": false
    }
}
```

세그먼트 일치가 없는 응답:

방문자가 방문자 데이터 가져오기 API 호출 전에 실시간 세그먼트와 일치하지 않으므로 다음 응답에는 `matchedSegments`이(가) 포함되지 않습니다.

```json
{
    "status": 200,
    "results": {
        "abm": [
            {
                "code": 4,
                "name": "abm_saleforce_customers"
            },
            {
                "code": 5,
                "name": "abm_top_customers"
            }
        ],
        "org": "Marketo",
        "location": {
            "country": "United States",
            "city": "San Mateo",
            "state": "CA"
        },
        "industries": [
            "Software & Internet"
        ],
        "isp": false
    }
}
```
