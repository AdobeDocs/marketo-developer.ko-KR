---
title: 지정 계정
feature: REST API
description: 설명, 쿼리, 업데이트 예 만들기, 검색 가능한 필드, 중복 제거 규칙 및 리드 연결 없음을 포함하여 ABM의 명명된 계정에 대한 Marketo REST 안내서.
exl-id: 2aa1d2a0-9e54-4a9a-abb1-0d0479ed3558
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# 지정 계정

[명명된 계정 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts)

Marketo은 Marketo ABM에서 사용하기 위해 명명된 계정에 대해 CRUD 작업을 수행하기 위한 API 세트를 제공합니다. 이러한 API는 리드 데이터베이스 API에 대한 표준 인터페이스 패턴을 따르며 설명, 만들기/업데이트, 삭제 및 쿼리 옵션을 제공합니다.

현재 Marketo의 API를 통해 사용할 수 있는 유일한 ABM 관련 함수는 명명된 계정에 대한 CRUD 작업입니다. 리드는 API를 통해 명명된 계정에 연결할 수 없습니다.

## 설명

명명된 계정을 설명하는 것은 쿼리할 때 유효한 검색 가능한 필드 목록과 API 사용에 사용 가능한 모든 필드 목록을 포함하여 Marketo의 API를 통해 명명된 계정 사용과 관련된 메타데이터를 반환합니다. 명명된 계정의 `idField`은(는) 항상 `marketoGUID`이며 `dedupeField`만 사용할 수 있으며 만들기에 대한 키는 개체의 `name` 필드입니다.

```
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

명명된 계정에 대한 쿼리는 filterType 및 최대 300개의 쉼표로 구분된 filterValues 집합을 사용하는 것을 기반으로 합니다. `filterType`은(는) 명명된 계정에 대한 설명 결과의 `searchableFields` 멤버에서 반환된 단일 필드일 수 있지만 filterValues는 필드의 데이터 형식에 대해 올바른 입력일 수 있습니다. 에서 특정 필드 집합을 반환하려면 필드 매개 변수를 전달해야 합니다. 여기서 값은 응답에서 반환될 필드를 쉼표로 구분한 목록입니다. 다른 쿼리 옵션과 마찬가지로 단일 쿼리 페이지에 대한 최대 레코드 수는 300개이며 호출에서 반환된 nextPageToken의 사용으로 집합의 추가 레코드를 요청해야 합니다.

```
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

명명 계정을 생성하고 업데이트하는 것은 표준 리드 데이터베이스 패턴을 따릅니다. 레코드는 POST 요청에서 JSON 본문의 입력 멤버에 전달해야 합니다. `input`은(는) `action` 및 `dedupeBy`을(를) 선택적 멤버로 사용하는 유일한 필수 멤버입니다. 최대 300개의 레코드가 입력에 포함될 수 있습니다. 작업은 createOnly, updateOnly 또는 createOrUpdate 중 하나일 수 있습니다. 지정되지 않은 경우, 작업은 기본적으로 createOrUpdate로 설정됩니다. dedupeBy는 action이 updateOnly일 때만 지정할 수 있으며 name 및 marketoGUID 필드에 각각 해당하는 dedupeFields 또는 idField 중 하나만 허용합니다.

```
POST /rest/v1/namedaccounts.json
```

```
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

명명된 계정 개체에는 필드 집합이 포함되어 있습니다. 각 필드 정의는 필드를 설명하는 속성 세트로 구성됩니다. 속성의 예로는 디스플레이 이름, API 이름 및 dataType이 있습니다. 이러한 속성을 통칭하여 메타데이터라고 합니다.

다음 엔드포인트를 사용하면 회사 개체의 필드를 쿼리할 수 있습니다. 이러한 API를 사용하려면 소유 API 사용자에게 읽기-쓰기 스키마 표준 필드 또는 읽기-쓰기 스키마 사용자 정의 필드 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

### 쿼리 필드

명명된 계정 필드를 쿼리하는 것은 간단합니다. API 이름으로 단일 명명된 계정 필드를 쿼리하거나 모든 회사 필드 집합을 쿼리할 수 있습니다.

#### 이름별

[이름별 명명된 계정 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) 끝점은 명명된 계정 개체의 단일 필드에 대한 메타데이터를 검색합니다. 필수 fieldApiName 경로 매개 변수는 필드의 API 이름을 지정합니다. 응답은 Describe Named Account 끝점과 유사하지만 필드가 사용자 정의 필드인지 여부를 나타내는 isCustom 속성과 같은 추가 메타데이터를 포함합니다.

```
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

[명명된 계정 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Accounts/operation/getNamedAccountFieldByNameUsingGET) 끝점은 명명된 계정 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드가 반환됩니다. batchSize 쿼리 매개 변수를 사용하여 이 숫자를 줄일 수 있습니다. moreResult 속성이 true이면 더 많은 결과를 사용할 수 있음을 의미합니다. moreResult 특성이 false를 반환할 때까지 이 끝점을 계속 호출합니다. 즉, 사용 가능한 결과가 없습니다. 이 API에서 반환된 nextPageToken은 항상 이 호출의 다음 반복에 재사용되어야 합니다.

```
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

삭제는 JSON POST 요청을 통해 수행되며 필수 입력 멤버와 선택적 deleteBy 멤버가 있습니다. deleteBy는 각각 이름 또는 marketoGUID에 해당하는 &quot;dedupeFields&quot; 또는 &quot;idField&quot; 중 하나일 수 있으며, 설정이 해제된 경우 기본값으로 dedupeFields가 됩니다. 입력 멤버는 deleteBy의 설정에 따라 각각 이름 또는 marketoGUID인 멤버를 하나씩 포함하는 최대 300개의 레코드 배열을 허용합니다.

```
POST /rest/v1/namedaccounts/delete.json
```

```
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

- 아래에 명시하지 않은 경우 명명된 계정 끝점의 시간 제한은 30초입니다
   - 명명된 계정 동기화: 120s
   - 명명 계정 삭제: 60초
