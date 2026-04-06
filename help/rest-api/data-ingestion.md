---
title: 데이터 수집
feature: REST API, Dynamic Content
description: 개인, 사용자 지정 개체, 회사 및 프로그램 구성원의 대량, 짧은 지연 시간 수집을 위해 Marketo 데이터 수집 API를 사용하십시오.
exl-id: 1d501916-53ac-42d8-a804-abb4ab01c7e8
source-git-commit: 6dc068f92d5b0c94035ca484fd1508dfe87bbd76
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 13%

---

# 데이터 수집 API

데이터 수집 API는 대량의 개인 및 개인 관련 데이터 수집을 효율적이고 최소한의 지연으로 처리하도록 설계된 대량의 짧은 지연 시간 고가용성 서비스입니다.

비동기적으로 실행되는 요청을 제출하면 데이터가 수집됩니다. [Marketo Observability 데이터 스트림](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup)에서 이벤트를 구독하여 요청 상태를 검색할 수 있습니다.

인터페이스는 개인, 사용자 정의 객체, 회사 및 프로그램 멤버의 네 가지 객체 유형에 대해 제공됩니다. 레코드 작업은 삭제를 지원하는 프로그램 멤버를 제외하고 &quot;삽입 또는 업데이트&quot;만 가능합니다.

>[!NOTE]
>
>데이터 수집 API에 액세스하려면 [Marketo Engage 성능 계층](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835) 패키지에 대한 권한이 필요합니다.

## 인증

데이터 수집 API는 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용하여 액세스 토큰을 생성하지만, HTTP 헤더 `X-Mkto-User-Token`을(를) 통해 액세스 토큰을 전달해야 합니다. 쿼리 매개 변수를 통해 액세스 토큰을 전달할 수 없습니다.

헤더를 통한 액세스 토큰 예:

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## 권한

데이터 수집은 Marketo REST API와 동일한 권한 모델을 사용하며, 각 끝점에 특정 권한이 필요하지만 사용할 추가적인 특수 권한이 필요하지 않습니다.

| 엔드포인트 | 사용 권한 |
| --- | --- |
| 개인 | 리드 읽기-쓰기 |
| 사용자 정의 오브젝트 | 사용자 지정 개체 읽기-쓰기 |
| 회사 | 읽기-쓰기 회사 |
| 프로그램 구성원 | 리드 읽기-쓰기 |

## 지원되는 오브젝트 유형

| 오브젝트 유형 | 지원되는 작업 |
| --- | --- |
| 개인 | 업데이트(삽입 또는 업데이트) |
| 사용자 정의 오브젝트 | 업데이트(삽입 또는 업데이트) |
| 회사 | 동기화(`createOnly`, `updateOnly`, `createOrUpdate`) |
| 프로그램 구성원 | 동기화(업데이트 상태), 삭제(프로그램에서 제거) |

## 헤더

데이터 수집은 다음 사용자 지정 HTTP 헤더를 사용합니다.

### 요청

| 키 | 값 | 필수 | 설명 |
| --- | --- | --- | --- |
| `X-Correlation-Id` | 임의 문자열(최대 길이 255자). | 아니요 | 시스템을 통해 요청을 추적하는 데 사용할 수 있습니다. Marketo Observability 데이터 스트림 참조 |
| `X-Request-Source` | 임의 문자열(최대 길이 50자). | 아니요 | 시스템을 통해 요청 소스를 추적하는 데 사용할 수 있습니다. Marketo Observability 데이터 스트림 참조 |

### 응답

| 키 | 값 | 필수 |
| --- | --- | --- |
| `X-Request-Id` | 고유 요청 ID. | 예 |

## 요청

HTTP POST 메서드를 사용하여 데이터를 서버로 전송합니다.

데이터 표현은 요청 본문에 application/json으로 포함됩니다.

도메인 이름: `mkto-ingestion-api.adobe.io`

경로는 MunchkinId가 Marketo 인스턴스에만 해당되는 `/subscriptions/MunchkinId`(으)로 시작됩니다. Munchkin ID는 Marketo Engage UI의 **관리자** > **내 계정** > **지원 정보**&#x200B;에서 찾을 수 있습니다.  경로의 나머지 부분은 관심 리소스를 지정하는 데 사용됩니다.

개인용 예제 URL:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

사용자 지정 개체의 URL 예:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

회사의 예제 URL:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/companies`

프로그램 멤버의 URL 예:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/programmembers`

### 응답

모든 응답은 `X-Request-Id` 헤더를 통해 고유한 요청 ID를 반환합니다.

헤더를 통한 요청 ID 예:

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 성공

호출이 성공하면 202 상태가 반환됩니다.  응답 본문이 반환되지 않습니다.

성공 응답의 예:

```
HTTP/1.1 202 Accepted
X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598
Content-Length: 0
Date: Wed, 18 Oct 2023 18:56:49 GMT
```

### 오류

호출에서 오류가 발생하면 추가 오류 세부 정보가 있는 응답 본문과 함께 비202 상태가 반환됩니다. 응답 본문은 `application/json`이며 구성원 `error_code` 및 `message`이(가) 있는 단일 개체를 포함합니다.

다음은 Adobe Developer Gateway에서 재사용되는 오류 코드입니다.

| HTTP 상태 코드 | error_code | 메시지 |
| --- | --- | --- |
| 401 | 401013 | Oauth 토큰이 잘못되었습니다. |
| 403 | 403010 | Oauth 토큰 누락 |
| 404 | 404040 | 리소스를 찾을 수 없음 |
| 429 | 429001 | 서비스 사용 한도 도달 |

다음은 데이터 수집 API에 고유하며 3개의 세그먼트로 구성된 오류 코드입니다.  처음 세 자리 수는 상태(Adobe Developer Gateway에서 반환됨), 그 뒤에는 0 &quot;0&quot;이 오고 세 자리 수가 옵니다.

| HTTP 상태 코드 | error_code | 메시지 |
| --- | --- | --- |
| 400 | 4000801 | 잘못된 요청 |
| 400 | 4000802 | 잘못된 데이터 |
| 403 | 4030801 | 인증되지 않음 |
| 429 | 4290801 | 일일 할당량에 도달함 |
| 500 | 5000801 | 내부 서버 오류 |

## 재시도

일시적인 오류가 감지되면 서비스는 작업을 다시 시도합니다. 재시도는 주로 종속 서비스가 시간 초과되거나 일시적으로 사용할 수 없을 때 다양한 이유로 발생합니다.

재시도 간격:

* 초기 작업 및 첫 번째 재시도 : 5분
* 1일과 2일 : 15분
* 2일과 3일 : 20분
* 3일과 4일 : 20분
* 4일과 5일 : 2시간
* 5번째 재시도 후 -> 3시간

## 엔드포인트

수집 엔드포인트는 사용자, 사용자 지정 개체, 회사 및 프로그램 멤버에 대해 사용할 수 있습니다.

### 개인

개인 레코드를 업데이트하는 데 사용되는 종단점입니다.

| 메서드 | 경로 |
| --- | --- |
| POST | /subscriptions/{munchkinId}/persons |

#### 헤더

| 키 | 값 |
| --- | --- |
| `Content-Type` | application/json |
| `X-Mkto-User-Token` | {accessToken} |

#### 요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본값 |
| --- | --- | --- | --- | --- |
| `priority` | 문자열 | 아니요 | 요청의 우선 순위: 보통 또는 높음 | 표준 |
| `partitionName` | 문자열 | 아니요 | 개인 파티션 이름 | 기본 |
| `dedupeFields` | 오브젝트 | 아니요 | 중복을 제거할 속성입니다. 하나 또는 두 개의 속성 이름이 허용됩니다. <br/> AND 작업에는 두 가지 속성이 사용됩니다. 예를 들어 `email`과(와) `firstName`이(가) 모두 지정된 경우 AND 작업을 사용하여 사람을 찾는 데 모두 사용됩니다. <br/>지원되는 특성: `id`, `email`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId` `sfdcLeadOwnerId`, 사용자 지정 특성(&quot;string&quot; 및 &quot;integer&quot; 형식만 해당), `email` |  |
| `persons` | 개체 배열 | 예 | 개인용 속성 이름-값 쌍 목록 | - |

필요한 권한은 `Read-Write Lead`입니다.

### 개인 예

#### 요청

`POST /subscriptions/{munchkinId}/persons`

#### 헤더

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 본문

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
         "lastName": "Parker",
         "company": "Karnv"
      },
      {
         "email": "johnny.neal@yvu30.com",
         "firstName": "Johnny",
         "lastName": "Neal",
         "company": "Acme Inc"
      }
   ]
}
```

#### 응답

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 사용자 정의 오브젝트

사용자 지정 개체 레코드를 업데이트하는 데 사용되는 끝점입니다.

| 메서드 | 경로 |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/customobjects/{customObjectAPIName}` |

#### 헤더

| 키 | 값 |
| --- | --- |
| `Content-Type` | application/json |
| `X-Mkto-User-Token` | {accessToken} |

#### 요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본값 |
| --- | --- | --- | --- | --- |
| `priority` | 문자열 | 아니요 | 요청의 우선 순위: 보통, 높음 | 표준 |
| `dedupeBy` | 문자열 | 아니요 | 중복 제거할 속성: dedupeFields, marketoGUID | 데이터 중복 제거 필드 |
| `customObjects` | 개체 배열 | 예 | 개체의 특성 이름-값 쌍 목록입니다. | - |

필요한 권한은 `Read-Write Custom Object`입니다.

개인에 대한 링크 필드가 요청에 지정되어 있고 해당 개인이 존재하지 않는 경우 몇 번의 재시도가 발생합니다. 재시도 기간(65분) 동안 해당 개인이 추가되면 성공적으로 갱신됩니다. 예를 들어, 연결 필드가 사용자에 대해 `email`이고 Person이 없는 경우 다시 시도됩니다.

### 사용자 지정 개체 예

#### 요청

`POST /subscriptions/{munchkinId}/customobjects/{customObjectAPIName}`

#### 헤더

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 본문

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

#### 응답

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 회사

회사 레코드를 동기화하는 데 사용되는 끝점입니다. 외부 회사 ID 또는 Marketo 내부 ID별 중복 제거를 사용하여 만들기, 업데이트 및 업데이트 작업을 지원합니다.

| 메서드 | 경로 |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/companies` |

#### 헤더

| 키 | 값 | 필수 |
| --- | --- | --- |
| `Content-Type` | application/json | 예 |
| `X-Mkto-User-Token` | {accessToken} | 예 |
| `X-Correlation-Id` | 임의 문자열(최대 길이 255자) | 아니요 |
| `X-Request-Source` | 임의 문자열(최대 길이 50자) | 아니요 |

#### 요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본값 |
| --- | --- | --- | --- | --- |
| `action` | 문자열 | 아니요 | 동기화 작업: `createOnly`, `updateOnly` 또는 `createOrUpdate` | `createOrUpdate` |
| `dedupeBy` | 문자열 | 아니요 | 중복을 제거할 필드: `dedupeFields` 또는 `idField`(대/소문자 구분 안 함). `createOnly` 및 `createOrUpdate`의 경우 `dedupeFields`만 허용됩니다. `updateOnly`의 경우 둘 다 허용됩니다. | `dedupeFields` |
| `input` | 개체 배열 | 예 | 회사 속성 이름-값 쌍 목록입니다. JSON 키 `input` 또는 `companies`을(를) 허용합니다. | - |

`input` 배열의 각 회사 개체는 다음 필드를 지원합니다.

| 키 | 데이터 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| `externalCompanyId` | 문자열 | 조건부 | 외부 회사 식별자. `dedupeBy`이(가) `dedupeFields`인 경우 필요합니다. `dedupeBy`이(가) `idField`인 경우 허용되지 않습니다. |
| `id` | Long | 조건부 | Marketo 내부 회사 ID. `dedupeBy`이(가) `idField`이고 `action`이(가) `updateOnly`인 경우 필요합니다. `dedupeBy`이(가) `dedupeFields`인 경우 허용되지 않습니다. |
| `company` | 문자열 | 아니요 | 회사 이름. |
| (모든 필드) | Any | 아니요 | [회사 설명](companies.md)에 정의된 추가 표준 또는 사용자 지정 회사 필드입니다. 필드 이름은 대소문자를 구분하지 않습니다. |

필요한 권한은 `Read-Write Company`입니다.

### 회사 예

#### 요청

`POST /subscriptions/{munchkinId}/companies`

#### 헤더

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 본문

```json
{
   "action": "createOrUpdate",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "externalCompanyId": "ext-company-001",
         "company": "Acme Corporation",
         "industry": "Technology",
         "numberOfEmployees": 5000,
         "annualRevenue": 100000000
      },
      {
         "externalCompanyId": "ext-company-002",
         "company": "Globex Industries",
         "industry": "Manufacturing",
         "numberOfEmployees": 1200
      }
   ]
}
```

#### 응답

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### 회사 업데이트-ID 예

```json
{
   "action": "updateOnly",
   "dedupeBy": "idField",
   "input": [
      {
         "id": 12345,
         "company": "Acme Corporation (Renamed)",
         "numberOfEmployees": 5500
      }
   ]
}
```

### 회사 유효성 검사 규칙

| 규칙 | 세부 정보 |
| --- | --- |
| 액션 | `createOnly`, `updateOnly`, `createOrUpdate` 중 하나여야 합니다. 대/소문자를 구분합니다. |
| 중복 제거 기준 | `dedupeFields` 또는 `idField`이어야 합니다(대/소문자 구분 안 함). 기본값은 `dedupeFields`입니다. |
| dedupeBy + 작업 | `createOnly` 및 `createOrUpdate`은(는) `dedupeFields`만 허용합니다. `updateOnly`은(는) `dedupeFields`과(와) `idField`을(를) 모두 허용합니다. |
| `dedupeBy=dedupeFields`일 때 | 각 회사에 `externalCompanyId`이(가) 있어야 합니다. 필드 `id`이(가) 없어야 합니다. |
| `dedupeBy=idField`일 때 | 각 회사에 `id`이(가) 있어야 합니다. 필드 `externalCompanyId`이(가) 없어야 합니다. |
| `input` / `companies` | Null이거나 비워 둘 수 없습니다. |
| 요청당 최대 오브젝트 수 | 1,000 |

### 프로그램 구성원(동기화)

프로그램 구성원 상태를 동기화하는 데 사용되는 끝점으로, 프로그램에 잠재 고객을 추가하거나 프로그램 상태를 업데이트합니다.

| 메서드 | 경로 |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/programmembers` |

#### 헤더

| 키 | 값 | 필수 |
| --- | --- | --- |
| Content-Type | application/json | 예 |
| X-Mkto-User-Token | {accessToken} | 예 |
| X-Correlation-Id | 임의 문자열(최대 길이 255자) | 아니요 |
| X-Request-Source | 임의 문자열(최대 길이 50자) | 아니요 |

#### 요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본값 |
| --- | --- | --- | --- | --- |
| 프로그램 | 개체 배열 | 예 | 프로그램 작업 목록입니다. 각각은 프로그램, 대상 상태 및 동기화 잠재 고객을 지정합니다. | - |

`programs` 배열의 각 개체는 다음을 포함합니다.

| 키 | 데이터 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| programId | Long | 예 | Marketo 프로그램 ID입니다. 양의 정수여야 합니다. |
| 상태 | 문자열 | 예 | 설정할 프로그램 멤버 상태(예: `"Member"` 또는 `"Influenced"`)입니다. JSON 키 `statusName` 또는 `status`을(를) 허용합니다. 값은 `"Not in Program"`이(가) 아니어야 합니다. 삭제 끝점을 대신 사용하십시오. |
| 구성원 | 개체 배열 | 예 | 프로그램에서 추가하거나 업데이트할 잠재 고객 참조 목록입니다. JSON 키 `input` 또는 `members`을(를) 허용합니다. |

`members` 배열의 각 개체는 다음을 포함합니다.

| 키 | 데이터 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| leadId | Long | 예 | Marketo 리드 ID. |
| (모든 필드) | Any | 아니요 | 추가 사용자 정의 프로그램 멤버 필드. 필드 이름은 대소문자를 구분하지 않습니다. |

필요한 권한은 `Read-Write Lead`입니다.

### 프로그램 구성원 동기화 예

#### 요청

`POST /subscriptions/{munchkinId}/programmembers`

#### 헤더

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 본문

```json
{
   "programs": [
      {
         "programId": 1001,
         "status": "Member",
         "members": [
            {
               "leadId": 10001
            },
            {
               "leadId": 10002
            }
         ]
      },
      {
         "programId": 1002,
         "status": "Influenced",
         "members": [
            {
               "leadId": 10003
            }
         ]
      }
   ]
}
```

#### 응답

`HTTP/1.1 202`
`X-Request-ID: e3d92152-0fb1-444a-8f8f-29d5a2338598`

### 프로그램 구성원 동기화 유효성 검사 규칙

| 규칙 | 세부 정보 |
| --- | --- |
| 프로그램 | Null이거나 비워 둘 수 없습니다. |
| programId | 필수 여부. 양의 정수여야 합니다. |
| 상태 | 필수 여부. 비워 둘 수 없습니다. `"Not in Program"`이(가) 아니어야 합니다(대/소문자 구분 안 함). 삭제 끝점을 대신 사용하십시오. |
| 구성원 | Null이거나 비워 둘 수 없습니다. |
| leadId | 입력 배열의 각 멤버에 필요합니다. |
| 요청당 최대 리드 수 | 모든 프로그램에서 총 1,000명의 멤버. |

### 프로그램 구성원(삭제)

프로그램에서 리드를 제거하는 데 사용되는 끝점입니다. 잠재 고객의 멤버십 상태를 `"Not in Program"`(으)로 설정하고 해당 프로그램에서 구성원을 제거합니다.

>[!NOTE]
>
>요청에는 구조화된 데이터가 있는 JSON 본문이 필요하므로 이 종단점은 DELETE이 아닌 POST를 사용합니다.

| 메서드 | 경로 |
| --- | --- |
| POST | `/subscriptions/{munchkinId}/programmembers/delete` |

#### 헤더

| 키 | 값 | 필수 |
| --- | --- | --- |
| Content-Type | application/json | 예 |
| X-Mkto-User-Token | {accessToken} | 예 |
| X-Correlation-Id | 임의 문자열(최대 길이 255자) | 아니요 |
| X-Request-Source | 임의 문자열(최대 길이 50자) | 아니요 |

#### 요청 본문

| 키 | 데이터 유형 | 필수 | 값 | 기본값 |
| --- | --- | --- | --- | --- |
| 프로그램 | 개체 배열 | 예 | 프로그램 삭제 작업 목록입니다. 각각 프로그램과 제거할 리드를 지정합니다. | - |

`programs` 배열의 각 개체는 다음을 포함합니다.

| 키 | 데이터 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| programId | Long | 예 | Marketo 프로그램 ID입니다. 양의 정수여야 합니다. |
| 구성원 | 개체 배열 | 예 | 프로그램에서 제거할 잠재 고객 참조 목록입니다. JSON 키 `input` 또는 `members`을(를) 허용합니다. |

`members` 배열의 각 개체는 다음을 포함합니다.

| 키 | 데이터 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| leadId | Long | 예 | Marketo 리드 ID. |

필요한 권한은 `Read-Write Lead`입니다.

### 프로그램 멤버 삭제 예

#### 요청

`POST /subscriptions/{munchkinId}/programmembers/delete`

#### 헤더

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### 본문

```json
{
   "programs": [
      {
         "programId": 1001,
         "members": [
            {
               "leadId": 10001
            },
            {
               "leadId": 10002
            }
         ]
      },
      {
         "programId": 1002,
         "members": [
            {
               "leadId": 10003
            }
         ]
      }
   ]
}
```

#### 응답

`HTTP/1.1 202`
`X-Request-ID: a1b2c3d4-e5f6-7890-abcd-ef1234567890`

### 프로그램 구성원이 유효성 검사 규칙을 삭제합니다.

| 규칙 | 세부 정보 |
| --- | --- |
| 프로그램 | Null이거나 비워 둘 수 없습니다. |
| programId | 필수 여부. 양의 정수여야 합니다. |
| 구성원 | Null이거나 비워 둘 수 없습니다. |
| leadId | 입력 배열의 각 멤버에 필요합니다. |
| 요청당 최대 리드 수 | 모든 프로그램에서 총 1,000명의 멤버. |

## 제한

다음은 보호 기능의 업데이트된 목록입니다.

* 최대 요청 크기: 1MB
* 오브젝트 유형당 요청당 최대 오브젝트 수: 1,000
* 클라이언트 ID당 초당 최대 요청 수: 5,000
* 일별 최대 개체 수: 10,000,000

이러한 제한은 개인, 사용자 정의 객체, 회사 및 프로그램 멤버에 걸쳐 균일하게 적용됩니다. Program Members의 경우 &quot;요청 당 개체&quot;는 단일 요청의 모든 프로그램에 대한 총 잠재 고객 참조 수입니다.

## 데이터 수집 API와 REST API

다음은 데이터 수집 API와 기타 Marketo REST API의 차이점 목록입니다.

* 인증하려면 `X-Mkto-User-Token` 헤더를 사용하여 액세스 토큰을 전달해야 합니다.
* URL 도메인 이름은 `mkto-ingestion-api.adobe.io`입니다.
* URL 경로는 `/subscriptions/MunchkinId`(으)로 시작합니다.
* 쿼리 매개 변수가 없습니다.
* 호출이 성공하면 202 상태가 반환되고 응답 본문이 비어 있습니다
* 호출이 실패하면 202가 아닌 상태가 반환되고 응답 본문에 `{ "error_code" : "Error Code", "message" : "Message" }`이(가) 포함됩니다.
* 요청 ID가 `X-Request-Id` 헤더를 통해 반환됩니다.
