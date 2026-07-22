---
title: 지정 계정
feature: REST API
description: 설명, 쿼리, 업데이트 예 만들기, 검색 가능한 필드, 중복 제거 규칙 및 리드 연결 없음을 포함하여 ABM의 명명된 계정에 대한 Marketo REST 안내서.
exl-id: 2aa1d2a0-9e54-4a9a-abb1-0d0479ed3558
TQID: https://experienceleague.adobe.com/iY3UYVelm3aKuuDBCTxaVCbkXfwnJzDjV3Kvn9rcNbA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 1%

---

# 지정 계정

[명명된 계정 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts)

Marketo은 Marketo ABM에서 사용할 명명된 계정에 대해 CRUD 작업을 수행하기 위한 API를 제공합니다. 이러한 API는 표준 리드 데이터베이스 인터페이스 패턴을 따르며 설명, 생성/업데이트, 삭제 및 쿼리 옵션을 제공합니다.

현재 Marketo API는 명명된 계정에 대한 CRUD 작업만 지원합니다. API를 통해 지정된 계정에 리드를 연결할 수 없습니다.

## 설명

명명된 계정 설명 은 Marketo API를 통해 명명된 계정을 사용하기 위한 메타데이터를 반환합니다. 응답에는 유효한 검색 가능한 필드와 API에 사용할 수 있는 모든 필드가 포함됩니다.

명명된 계정의 `idField`은(는) 항상 `marketoGUID`입니다. 개체의 `name` 필드만 사용할 수 있는 `dedupeField` 및 생성 키입니다.

```http
GET /rest/v1/namedaccounts/describe.json
```

```json
{
   "requestId":"d65e#156c27ac57d",
   "result":[
      {
         "name":"Named Account",
         "description":"Marketo standard account attribute map",
         "createdAt":"2016-08-18T20:16:41Z",
         "updatedAt":"2016-08-18T20:16:41Z",
         "idField":"marketoGUID",
         "dedupeFields":[
            "name"
         ],
         "searchableFields":[
            [
               "marketoGUID",
            ],
            [
               "annualRevenue"
            ],
            [
               "city"
            ],
            [
               "country"
            ],
            [
               "domainName"
            ],
            [
               "industry"
            ],
            [
               "logoUrl"
            ],
            [
               "membershipCount"
            ],
            [
               "name"
            ],
            [
               "numberOfEmployees"
            ],
            [
               "opptyAmount"
            ],
            [
               "opptyCount"
            ],
            [
               "score1"
            ],
            [
               "score2"
            ],
            [
               "score3"
            ],
            [
               "score4"
            ],
            [
               "score5"
            ],
            [
               "sicCode"
            ],
            [
               "state"
            ]
         ],
         "fields":[
            {
               "name":"marketoGUID",
               "displayName":"Marketo GUID",
               "dataType":"string",
               "length":36,
               "updateable":false
            },
            {
               "name":"annualRevenue",
               "displayName":"annualRevenue",
               "dataType":"currency",
               "updateable":true
            },
            {
               "name":"city",
               "displayName":"city",
               "dataType":"string",
               "length":255,
               "updateable":true
            },
            {
               "name":"country",
               "displayName":"country",
               "dataType":"string",
               "length":255,
               "updateable":true
            }
         ]
      }
   ],
   "success":true
}
```

### 쿼리

filterType 및 최대 300개의 쉼표로 구분된 filterValues를 사용하여 명명된 계정을 쿼리합니다. filterType은 Describe 응답의 `searchableFields` 멤버에서 반환된 단일 필드일 수 있습니다. 각 filterValues 항목은 필드의 데이터 형식에 유효한 값이어야 합니다.

특정 필드를 반환하려면 쉼표로 구분된 필드 목록과 함께 필드 매개 변수를 전달하십시오. 쿼리 페이지에는 최대 300개의 레코드가 포함됩니다. 추가 레코드를 검색하려면 호출에서 반환된 nextPageToken을 사용합니다.

```http
GET /rest/v1/namedaccounts.json?filterType=name&filterValues=Google,Yahoo
```

```json
{
    "requestId": "6dac#157d4ddc9d7",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "16efafdd-0148-4ea7-8782-f451d7c6345d",
            "createdAt": "2016-10-17T22:49:04Z",
            "name": "Google",
            "updatedAt": "2016-10-17T22:49:04Z"
        },
        {
            "seq": 1,
            "marketoGUID": "44d62353-7f9d-4d43-b9cc-7ef0f7a09137",
            "createdAt": "2016-10-17T22:49:04Z",
            "name": "Yahoo",
            "updatedAt": "2016-10-17T22:49:04Z"
        }
    ],
    "success": true
}
```

### 만들기 및 업데이트

표준 리드 데이터베이스 패턴을 사용하여 명명된 계정을 만들고 업데이트합니다. POST 요청의 JSON 본문의 입력 멤버에 레코드를 전달합니다. 최대 300개의 레코드를 포함할 수 있습니다.

요청 멤버는 다음과 같습니다.

- `input`: 유일한 필수 구성원입니다.
- `action`: createOnly, updateOnly 또는 createOrUpdate를 허용하는 선택적 멤버입니다. 기본값은 createOrUpdate입니다.
- `dedupeBy`: action이 updateOnly인 경우에만 사용할 수 있는 선택적 멤버입니다. 이 코드는 각각 이름 및 marketoGUID 필드에 해당하는 dedupeFields 또는 idField를 허용합니다.

```http
POST /rest/v1/namedaccounts.json
```

```text
Content-Type: application/json
```

```json
{
   "action":"updateOnly",
   "dedupeBy":"dedupeFields",
   "input":[
      {
         "name":"Google",
         "domainName":"www.google.com"
      },
      {
         "name":"Yahoo",
         "domainName":"www.yahoo.com"
      }
   ]
}
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "status":"updated",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq":1,
         "status":"created",
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fc"
      }
   ]
}
```

### 필드

명명된 계정 개체에는 표시 이름, API 이름 및 dataType과 같은 특성으로 정의된 필드가 포함되어 있습니다. 이러한 특성을 함께 메타데이터라고 합니다.

다음 엔드포인트는 회사 개체의 쿼리 필드를 나타냅니다. API 사용자는 읽기-쓰기 스키마 표준 필드 권한, 읽기-쓰기 스키마 사용자 정의 필드 권한 또는 둘 다 있는 역할이 있어야 합니다.

### 쿼리 필드

API 이름으로 명명된 계정 필드 하나를 쿼리하거나 모든 회사 필드를 검색합니다.

#### 이름별

[이름별 명명된 계정 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) 끝점은 명명된 계정 개체의 한 필드에 대한 메타데이터를 검색합니다. 필수 fieldApiName 경로 매개 변수는 필드의 API 이름을 지정합니다.

이 응답은 Describe Named Account 응답과 유사하지만 추가 메타데이터를 포함합니다. 예를 들어 isCustom 속성은 필드가 사용자 지정인지 여부를 나타냅니다.

```http
GET /rest/v1/namedaccounts/schema/fields/annualRevenue.json
```

```json
{
    "requestId": "371c#17e979c5d1f",
    "result": [
        {
            "displayName": "Annual Revenue",
            "name": "annualRevenue",
            "description": null,
            "dataType": "currency",
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true
}
```

#### 찾아보기

[명명된 계정 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) 끝점은 명명된 계정 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드를 반환합니다. batchSize 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

moreResult 속성이 true이면 더 많은 결과를 사용할 수 있습니다. moreResult가 false가 될 때까지 반환된 nextPageToken으로 끝점을 계속 호출합니다.

```http
GET /rest/v1/namedaccounts/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "f287#17e995bd0c5",
    "result": [
        {
            "displayName": "Name",
            "name": "name",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Domain Name",
            "name": "domainName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Industry",
            "name": "industry",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "SIC Code",
            "name": "sicCode",
            "description": null,
            "dataType": "string",
            "length": 40,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "City",
            "name": "city",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        }
    ],
    "success": true,
    "nextPageToken": "N42LHXWEULHZ3N2I77DKOJUVOY======",
    "moreResult": true
}
```

### 삭제

JSON 본문이 있는 POST 요청을 전송하여 명명된 계정을 삭제합니다. 요청에는 필수 입력 멤버와 선택적 deleteBy 멤버가 포함되어 있습니다.

deleteBy 멤버가 각각 name 및 marketoGUID에 해당하는 &quot;dedupeFields&quot; 또는 &quot;idField&quot;를 허용합니다. 설정하지 않으면 기본값은 dedupeFields로 설정됩니다. 입력 멤버는 최대 300개의 레코드를 허용합니다. 각 레코드에는 deleteBy 설정에 따라 name 또는 marketoGUID가 포함됩니다.

```http
POST /rest/v1/namedaccounts/delete.json
```

```text
Content-Type: application/json
```

```json
{
   "deleteBy":"dedupeFields",
   "input":[
      {
         "name":"Google"
      },
      {
         "name":"Yahoo"
      },
      {
         "name":"Marketo"
      }
   ]
}
```

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "seq":0,
         "marketoGUID":"dff23271-f996-47d7-984f-f2676861b5fb",
         "status":"deleted"
      },
      {
         "seq":1,
         "id":"dff23271-f996-47d7-984f-f2676861b5fc",
         "status":"deleted"
      },
      {
         "seq":2,
         "status":"skipped",
         "reasons":[
            {
               "code":"1013",
               "message":"Record not found"
            }
         ]
      }
   ]
}
```

## 시간 초과

- 달리 지정하지 않는 한 명명된 계정 끝점의 시간 제한은 30초입니다.
- 명명 계정 동기화에 120초의 시간 제한이 있습니다.
- 명명 계정 삭제의 시간 제한은 60초입니다.
