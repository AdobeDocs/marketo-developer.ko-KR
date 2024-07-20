---
title: "데이터 수집"
description: "데이터 수집 API 개요"
source-git-commit: 6fc45ff98998217923e2a5b02d00d1522fe3272c
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 9%

---


# 데이터 수집

데이터 수집 API는 대량의 개인 및 개인 관련 데이터 수집을 효율적이고 최소한의 지연으로 처리하도록 설계된 대량의 짧은 지연 시간 고가용성 서비스입니다. 

비동기적으로 실행되는 요청을 제출하면 데이터가 수집됩니다. [Marketo Observability 데이터 스트림](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup/)에서 이벤트를 구독하여 요청 상태를 검색할 수 있습니다&#x200B;.

인터페이스는 사용자, 사용자 정의 객체, 이렇게 두 가지 객체 유형에 대해 제공됩니다. 레코드 작업은 &quot;삽입 또는 업데이트&quot;만 가능합니다.

데이터 수집 API는 비공개 베타에 있습니다. 초대자는 [Marketo Engage 성능 계층 패키지](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835)에 대한 권한이 있어야 합니다.

## 인증

데이터 수집 API는 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용하여 액세스 토큰을 생성하지만, HTTP 헤더 `X-Mkto-User-Token`을(를) 통해 액세스 토큰을 전달해야 합니다. 쿼리 매개 변수를 통해 액세스 토큰을 전달할 수 없습니다.

헤더를 통한 액세스 토큰 예:

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## 권한

데이터 수집은 Marketo REST API와 동일한 권한 모델을 사용하며, 각 끝점에 특정 권한이 필요하지만 사용할 추가적인 특수 권한이 필요하지 않습니다.

| 엔드포인트 | 권한 |
|---|---|
| 개인 | 리드 읽기-쓰기 |
| 사용자 지정 개체 | 사용자 지정 개체 읽기-쓰기 |

## 헤더

데이터 수집은 다음 사용자 지정 HTTP 헤더를 사용합니다.

### 요청

| 키 | 값 | 필수 | 설명 |
|---|---|---|---|
| X-Correlation-Id | 임의 문자열(최대 길이 255자). | 아니요 | 시스템을 통해 요청을 추적하는 데 사용할 수 있습니다. Marketo Observability 데이터 스트림 참조 |
| X-Request-Source | 임의 문자열(최대 길이 50자). | 아니요 | 시스템을 통해 요청 소스를 추적하는 데 사용할 수 있습니다. Marketo Observability 데이터 스트림 참조 |

### 응답

| 키 | 값 | 필수 | 설명 |
|---|---|---|---|
| X-Request-Id | 고유 요청 ID. | 예 | |

## 요청

HTTP POST 메서드를 사용하여 서버로 데이터를 전송합니다.

데이터 표현은 요청 본문에 application/json으로 포함됩니다.

도메인 이름: `mkto-ingestion-api.adobe.io`

경로는 `/subscriptions/_MunchkinId_`로 시작합니다. 여기서 `_MunchkinId_`은(는) Marketo 인스턴스에만 해당됩니다. Marketo Engage UI의 **관리자** >**내 계정** > **지원 정보**&#x200B;에서 Munchkin ID를 찾을 수 있습니다. 경로의 나머지 부분은 관심 리소스를 지정하는 데 사용됩니다.

개인용 예제 URL:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

사용자 지정 개체의 URL 예:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

## 응답

모든 응답은 `X-Request-Id` 헤더를 통해 고유한 요청 ID를 반환합니다.

헤더를 통한 요청 ID 예:

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 성공

호출이 성공하면 202 상태가 반환됩니다. 응답 본문이 반환되지 않습니다.

성공 응답의 예:

`HTTP/1.1 202 Accepted` `X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598` `Content-Length: 0` `Date: Wed, 18 Oct 2023 18:56:49 GMT`

### 오류

호출에서 오류가 발생하면 추가 오류 세부 정보가 있는 응답 본문과 함께 비202 상태가 반환됩니다. 응답 본문은 application/json이며 멤버 `error_code` 및 `message`이(가) 포함된 단일 개체를 포함합니다.

다음은 Adobe Developer Gateway에서 재사용되는 오류 코드입니다.

| HTTP 상태 코드 | error_code | 메시지 |
|--- |--- |--- |
| 401 | 401013 | Oauth 토큰이 잘못되었습니다. |
| 403 | 403010 | Oauth 토큰 누락 |
| 404 | 404040 | 리소스를 찾을 수 없음 |
| 429 | 429001 | 서비스 사용 한도 도달 |

다음은 데이터 수집 API에 고유하며 3개의 세그먼트로 구성된 오류 코드입니다. 처음 세 자리 수는 상태(Adobe IO Gateway에서 반환됨), 그 뒤에 0이 뒤따르고 세 자리 수가 옵니다.

| HTTP 상태 코드 | error_code | 메시지 |
|--- |--- |--- |
| 400 | 4000801 | 잘못된 요청 |
| 400 | 4000802 | 잘못된 데이터 |
| 403 | 4030801 | 인증되지 않음 |
| 429 | 4290801 | 일일 할당량에 도달함 |
| 500 | 5000801 | 내부 서버 오류 |

오류 응답의 예:

`HTTP/1.1 403 Forbidden` `Content-Type: application/json` `Content-Length: 54` `Date: Wed, 18 Oct 2023 19:10:07 GMT` `X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw` `{"error_code":"403010","message":"Oauth token is missing"}`

## 재시도

일시적인 오류가 감지되면 서비스는 작업을 세 번 다시 시도합니다. 첫 번째 재시도는 5분의 대기 시간 후 발생하며, 두 번째는 30분 후 발생하며, 마지막으로 세 번째는 30분 후 발생합니다. 재시도는 주로 종속 서비스가 시간 초과되거나 일시적으로 사용할 수 없을 때 다양한 이유로 발생합니다.

## 엔드포인트

수집 끝점은 사용자 및 사용자 지정 개체에 사용할 수 있습니다.

### 개인

개인 레코드를 업데이트하는 데 사용되는 종단점입니다.

| 방법 |
|---|
| POST |

| 경로 |
|---|
| `/subscriptions/{munchkinId}/persons` |

| HeadersKey | 값 |
|---|---|
| Content-Type | application/json |
| X-Mkto-User-Token | {accessToken} |

요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본 값 |
|---|---|---|---|---|
| 우선 순위 | 문자열 | 아니요 | 요청의 우선 순위:보통 높음 | 표준 |
| partitionName | 문자열 | 아니요 | 개인 파티션 이름 | 기본 |
| 데이터 중복 제거 필드 | 오브젝트 | 아니요 | 중복을 제거할 속성입니다. 하나 또는 두 개의 속성 이름이 허용됩니다. AND 작업에는 두 가지 속성이 사용됩니다. 예를 들어 `email`과(와) `firstName`이(가) 모두 지정된 경우 AND 작업을 사용하여 사람을 찾는 데 둘 다 사용됩니다. 지원되는 특성은 다음과 같습니다. `idemail`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerIdCustom` 특성(&quot;string&quot; 및 &quot;integer&quot; 형식만 해당) | 이메일 |
| 개인 | 개체 배열 | 예 | 개인용 속성 이름-값 쌍 목록 | - |

| 권한 |
|---|
| 리드 읽기-쓰기 |

#### 개인 예

```
POST /subscriptions/{munchkinId}/persons
```

```
Content-Type: application/json
X-Mkto-User-Token: {accessToken}
```

```json
{
   "priority": "high",
   "partitionName": "EMEA",
   "dedupeFields": {
      "field1": "email",
      "field2": "firstName"
   },
   "persons":[
      {
         "email": "brooklyn.parker@karnv.com",
         "firstName": "Brooklyn",
         "lastName": "Parker"
      },
      {
         "email": "johnny.neal@yvu30.com",
         "firstName": "Johnny",
         "lastName": "Neal"
      }
   ]
}
```

```
HTTP/1.1 202
X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw
```

### 사용자 지정 개체

사용자 지정 개체 레코드를 업데이트하는 데 사용되는 끝점입니다.

| 방법 |
|---|
| POST |

| 경로 |
|---|
| `/subscriptions/{munchkinId}/customobjects/{customObjectAPIName}` |

헤더

| 키 | 값 |
|---|---|
| Content-Type | application/json |
| X-Mkto-User-Token | {accessToken} |

요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본 값 |
|---|---|---|---|---|
| 우선 순위 | 문자열 | 아니요 | 요청의 우선 순위:보통 높음 | 표준 |
| 중복 제거 기준 | 문자열 | 아니요 | 중복 제거할 속성:dedupeFieldsmarketoGUID | 데이터 중복 제거 필드 |
| 사용자 지정 개체 | 개체 배열 | 예 | 개체의 특성 이름-값 쌍 목록입니다. | - |

| 권한 |
|---|
| 사용자 지정 개체 읽기-쓰기 |

#### 사용자 없음

개인에 대한 링크 필드가 요청에 지정되어 있고 해당 개인이 존재하지 않는 경우 몇 번의 재시도가 발생합니다. 재시도 기간(65분) 동안 해당 개인이 추가되면 성공적으로 갱신됩니다. 예를 들어, 연결 필드가 사용자에 대해 `email`이고 Person이 없는 경우 다시 시도됩니다.

#### 사용자 지정 개체 예

```
POST /subscriptions/{munchkinId}/customobjects/{customObjectAPIName}
```

```
Content-Type: application/json
X-Mkto-User-Token: {accessToken}
```

```json
{
   "dedupeBy": "dedupeFields",
   "priority": "high",
   "customObjects": [
      {
         "email": "brooklyn.parker@karnv.com",
         "vin": "20UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 330i",
         "year": 2003
      },
      {
         "email": "johnny.neal@yvu30.com",
         "vin": "19UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 325i",
         "year": 1989
      }
   ]
}
```

```
HTTP/1.1 202
X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw
```

## 제한

다음은 보호 기능 사용 목록입니다.

- 최대 요청 크기: 1MB
- 오브젝트 유형당 요청당 최대 오브젝트 수: 1,000
- 클라이언트 ID당 초당 최대 요청 수: 5,000
- 일별 최대 개체 수: 10,000,000

## 데이터 수집 API와 REST API

다음은 데이터 수집 API와 기타 Marketo REST API의 차이점 목록입니다.

- 전체 CRUD 인터페이스가 아니며, &#39;업데이트&#39;만 지원합니다.
- 인증하려면 `X-Mkto-User-Token` 헤더를 사용하여 액세스 토큰을 전달해야 합니다.
- URL 도메인 이름은 `mkto-ingestion-api.adobe.io`입니다.
- URL 경로는 `/subscriptions/_MunchkinId_`(으)로 시작합니다.
- 쿼리 매개 변수가 없습니다.
- 호출이 성공하면 202 상태가 반환되고 응답 본문이 비어 있습니다
- 호출이 실패하면 202가 아닌 상태가 반환되고 응답 본문에 `{ "error_code" : "_Error Code_", "message" : "_Message_" }`이(가) 포함됩니다.
- 요청 ID가 `X-Request-Id` 헤더를 통해 반환됩니다.
