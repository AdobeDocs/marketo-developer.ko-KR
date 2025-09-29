---
title: 방문자 데이터 가져오기
description: 매개 변수, 콜백 예 및 세그먼트, ABM 및 위치에 대한 샘플 응답이 있는 RTP User Context API를 사용하여 실시간 방문자 식별을 가져옵니다.
feature: Javascript
exl-id: 39a2446d-8a31-461e-bbe6-a7edf24b4d52
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 4%

---

# 방문자 데이터 가져오기

이 방법은 실시간 방문자 식별 데이터를 가져오는 데 사용됩니다.

- User Context API를 사용하기 전에 웹 Personalization 고객이 되어 있고 사이트에 [RTP 태그가 배포](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)되어 있어야 합니다.
- RTP는 계정 기반 마케팅 명명된 계정 목록을 지원하지 않습니다. ABM 목록 및 코드는 RTP 내에서 관리되는 업로드된 계정 목록(CSV 파일)에만 해당됩니다.

오류가 발생하면 응답 JSON의 일부로 오류 메시지가 표시됩니다. 500 코드가 반환되면 지원 센터에 문의 하여 요청을 접수합니다.

| 매개변수 | 선택 사항/필수 | 유형 | 설명 |
|---|---|---|---|
| `get` | 필수 | 문자열 | 메서드 작업. |
| `visitor` | 필수 | 문자열 | 메서드 이름입니다. |
| `callback` | 필수 | 함수 | 반환된 각 캠페인에 대해 트리거될 콜백 함수입니다. |

## 예

방문자 식별 데이터 가져오기:

```javascript
function callbackFunction() {
    console.log('RTP is awesome!');
}
rtp('get', 'visitor', callbackFunction);
```

세그먼트 일치가 있는 응답:

다음은 방문자가 방문자 데이터 가져오기 API 호출 전에 실시간 세그먼트와 일치하는 경우 반환되는 예제 응답입니다.

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

다음은 방문자가 방문자 데이터 가져오기 API 호출 전에 실시간 세그먼트와 일치하지 않는 경우 반환되는 예제 응답입니다.

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
