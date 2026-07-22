---
title: 사용량
feature: REST API
description: 사용자당 카운트 및 오류 코드 합계를 포함하여 일별 및 마지막 7일 통계 엔드포인트로 Marketo REST API 사용 및 오류를 모니터링합니다.
exl-id: 935a00a4-1e1e-4b48-ae9c-72c5e578312a
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 8%

---

# 사용

[사용 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Usage)

사용 API는 구독에 대한 REST API 사용량 및 오류 활동을 요약합니다. 이러한 엔드포인트를 사용하여 통합을 모니터링하고, 일일 호출 볼륨을 추적하고, 오류 트렌드를 식별합니다.

사용 데이터에는 총 API 호출 수 및 사용자별 분류가 포함됩니다. 오류 데이터에는 오류의 총 횟수와 오류 코드별 분류가 포함됩니다.

사용 API는 다른 Marketo REST API와 동일한 인증 방법을 사용합니다. `Authorization: Bearer {accessToken}` 헤더에 액세스 토큰을 전달합니다.

## 엔드포인트

| 메서드 | 경로 | 설명 |
| --- | --- | --- |
| GET | `/rest/v1/stats/usage.json` | 현재 날짜의 API 사용을 검색합니다. |
| GET | `/rest/v1/stats/usage/last7days.json` | 지난 7일 동안의 API 사용을 검색합니다. |
| GET | `/rest/v1/stats/errors.json` | 현재 날짜의 API 오류를 검색합니다. |
| GET | `/rest/v1/stats/errors/last7days.json` | 지난 7일 동안의 API 오류를 검색합니다. |

## 일일 사용량

현재 날짜의 API 사용을 검색합니다.

```http
GET /rest/v1/stats/usage.json
```

```json
{
   "requestId": "5f7f#17d7d8f2b6f",
   "success": true,
   "result": [
      {
         "date": "2015-10-17",
         "total": 1120,
         "users": [
            {
               "userId": "some.body@yahoo.com",
               "count": 200
            },
            {
               "userId": "some.body@marketo.com",
               "count": 200
            },
            {
               "userId": "some.body@gmail.com",
               "count": 720
            }
         ]
      }
   ]
}
```

`result` 배열의 각 개체에는 하루 동안의 사용 합계와 사용자별 분류가 포함되어 있습니다.

## 최근 7일 사용

지난 7일 동안의 API 사용을 검색합니다. `result` 배열의 각 요소는 1일을 나타냅니다.

```http
GET /rest/v1/stats/usage/last7days.json
```

## 일일 오류

현재 날짜의 API 오류를 검색합니다.

```http
GET /rest/v1/stats/errors.json
```

```json
{
   "requestId": "5f7f#17d7d8f2b6f",
   "success": true,
   "result": [
      {
         "date": "2015-10-17",
         "total": 73,
         "errors": [
            {
               "errorCode": "604",
               "count": 1
            },
            {
               "errorCode": "609",
               "count": 56
            },
            {
               "errorCode": "610",
               "count": 16
            }
         ]
      }
   ]
}
```

`result` 배열의 각 개체에는 하루 동안의 오류 합계와 오류 코드별 분류가 포함되어 있습니다.

## 최근 7일 오류

지난 7일 동안의 API 오류를 검색합니다. `result` 배열의 각 요소는 1일을 나타냅니다.

```http
GET /rest/v1/stats/errors/last7days.json
```

## 응답 멤버

### 사용 결과 개체

| 이름 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `date` | 문자열 | `YYYY-MM-DD` 형식의 사용 요약 날짜입니다. |
| `total` | 정수 | 해당 날짜의 총 API 호출 수 |
| `users` | 배열 | 해당 날짜의 사용자당 사용량 목록. |

### 사용 사용자 개체

| 이름 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `userId` | 문자열 | API 사용자 식별자. |
| `count` | 정수 | 해당 사용자가 하루 동안 수행한 API 호출 수입니다. |

### 오류 결과 개체

| 이름 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `date` | 문자열 | 오류 요약 날짜가 `YYYY-MM-DD` 형식입니다. |
| `total` | 정수 | 해당 날짜의 총 API 오류 수입니다. |
| `errors` | 배열 | 해당 날짜의 오류 코드당 카운트 목록입니다. |

### 오류 오브젝트

| 이름 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `errorCode` | 문자열 | Marketo 오류 코드. |
| `count` | 정수 | 해당 날짜에 오류가 발생한 횟수입니다. |

## 참고

사용 응답은 각 API 사용자를 개별적으로 보고합니다. 통합을 별도의 API 사용자에게 할당하면 할당량을 소모하고 오류를 생성하는 서비스를 보다 쉽게 식별할 수 있습니다.
