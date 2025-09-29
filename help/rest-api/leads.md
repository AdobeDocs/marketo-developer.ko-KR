---
title: 잠재 고객
feature: REST API
description: 설명, ID 또는 필터별 쿼리, 기본 필드, 제한 및 ECID 검색을 포함한 Marketo Leads REST API 기능을 살펴봅니다.
exl-id: 0a2f7c38-02ae-4d97-acfe-9dd108a1f733
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '3351'
ht-degree: 2%

---

# 잠재 고객

[리드 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)

Marketo 잠재 고객의 API는 잠재 고객 레코드에 대한 간단한 CRUD 애플리케이션을 위한 대규모 기능 세트를 제공하며, 정적 목록 및 프로그램에서 잠재 고객의 멤버십을 수정하고 잠재 고객에 대한 스마트 캠페인 처리를 시작하는 기능을 제공합니다.

## 설명

Lead API 의 주요 기능 중 하나는 Describe 메서드입니다. 리드 설명을 사용하여 REST API와 각 REST API에 대한 메타데이터를 모두 통해 상호 작용에 사용할 수 있는 필드의 전체 목록을 검색합니다.

* 데이터 유형
* REST API 이름
* 길이(해당되는 경우)
* 읽기 전용
* 알기 쉬운 레이블

설명 은 필드를 사용할 수 있는지 여부에 대한 기본 소스로 해당 필드에 대한 메타데이터입니다.

### 요청

```
GET /rest/v1/leads/describe.json
```

### 응답

```json
{
   "requestId":"37ca#1475b74e276",
   "success":true,
   "result":[
      {
         "id":2,
         "displayName":"Company Name",
         "dataType":"string",
         "length":255,
         "rest":{
            "name":"company",
            "readOnly":false
         },
         "soap":{
            "name":"Company",
            "readOnly":false
         }
      }
}
```

일반적으로 응답에는 결과 배열에 훨씬 큰 필드 집합이 포함되지만 데모용으로 생략됩니다. 결과 배열의 각 항목은 리드 레코드에서 사용할 수 있는 필드에 해당하며 최소한 ID, displayName 및 데이터 형식을 갖게 됩니다. rest 및 soap 하위 개체는 주어진 필드에 대해 존재할 수 있거나 존재하지 않을 수 있으며, 해당 존재는 필드가 REST 또는 SOAP API에서 사용하기에 유효한지 여부를 나타냅니다. `readOnly` 속성은 해당 API(REST 또는 SOAP)를 통해 필드가 읽기 전용인지 여부를 나타냅니다. length 속성은 필드의 최대 길이(있는 경우)를 나타냅니다. dataType 속성은 필드의 데이터 형식을 나타냅니다.

## 쿼리

리드 검색에는 ID별 리드 가져오기 및 필터 유형별 리드 가져오기 두 가지 기본 방법이 있습니다. Id별 Lead 가져오기 는 단일 Lead ID 를 경로 매개 변수로 사용하고 단일 Lead 레코드를 반환합니다.

선택적으로 반환할 필드 이름의 쉼표로 구분된 목록이 포함된 필드 매개 변수를 전달할 수 있습니다. 필드 매개 변수가 이 요청에 포함되지 않으면 `email`, `updatedAt`, `createdAt`, `lastName`, `firstName` 및 `id` 기본 필드가 반환됩니다. 필드 목록을 요청할 때 특정 필드가 요청되었지만 반환되지 않은 경우 값이 null로 간주됩니다.

### 요청

```
GET /rest/v1/lead/{id}.json
```

### 응답

```json
{
   "requestId": "10226#14d3049e51b",
   "success": true,
   "result": [
      {
         "id": 318581,
         "updatedAt":"2015-05-07T11:47:30-08:00"
         "lastName": "Doe",
         "email": "jdoe@marketo.com",
         "createdAt": "2015-05-01T16:47:30-08:00",
         "firstName": "John"
      }
   ]
}
```

이 메서드의 경우 결과 배열의 첫 번째 위치에 항상 단일 레코드가 있습니다.

필터 유형별 리드 가져오기는 동일한 유형의 레코드를 반환하지만, 페이지당 최대 300개를 반환할 수 있습니다. `filterType` 및 `filterValues` 쿼리 매개 변수가 필요합니다.

`filterType`은(는) 모든 사용자 지정 필드 또는 일반적으로 사용되는 대부분의 필드를 허용합니다. `Describe2`에서 사용할 수 있는 검색 가능한 필드의 포괄적인 목록을 가져오려면 `filterType` 끝점을 호출하십시오. 사용자 지정 필드로 검색할 때 `string`, `email`, `integer` 데이터 형식만 지원됩니다. 위에서 설명한 Describe 방법을 사용하여 필드 세부 사항(설명, 유형 등)을 가져올 수 있습니다.

`filterValues`은(는) 쉼표로 구분된 형식으로 최대 300개의 값을 허용합니다. 호출은 잠재 고객 필드가 포함된 `filterValues` 중 하나와 일치하는 레코드를 검색합니다. 리드 필터와 일치하는 리드 수가 1,000보다 크면 &quot;1003, 필터와 일치하는 결과가 너무 많습니다.&quot;라는 오류가 반환됩니다.

GET 요청의 총 길이가 8KB를 초과하는 경우 HTTP 오류: &quot;414, URI 너무 김&quot;(RFC 7231에 따라)이 반환됩니다. 해결 방법으로, GET을 POST로 변경하고, _method=GET 매개 변수를 추가하고, 요청 본문에 쿼리 문자열을 배치할 수 있습니다.

### 요청

```
GET /rest/v1/leads.json?filterType=id&filterValues=318581,318592
```

### 응답

```json
{
    "requestId": "12951#15699db5c97",
    "result": [
        {
            "id": 318581,
            "updatedAt": "2016-05-17T22:11:45Z",
            "lastName": "Lincoln",
            "email": "abe@usa.gov",
            "createdAt": "2015-03-17T00:18:40Z",
            "firstName": "Abraham"
        },
        {
            "id": 318592,
            "updatedAt": "2016-05-17T22:20:51Z",
            "lastName": "Washington",
            "email": "george@usa.gov",
            "createdAt": "2015-04-06T16:29:21Z",
            "firstName": "George"
        }
    ],
    "success": true
}
```

이 호출은 `filterValues`에 포함된 ID와 일치하는 레코드를 검색하고 일치하는 레코드를 반환합니다.

레코드가 없으면 응답은 성공을 나타내지만 결과 배열은 비어 있습니다.

### 응답

```json
{
"requestId": "177a1#1578b643357",
"result": [],
"success": true
}
```

ID로 리드 가져오기 및 필터 유형별로 리드 가져오기 는 모두 쉼표로 구분된 API 필드 목록을 수락하는 필드 쿼리 매개 변수도 수락합니다. 이 필드가 포함된 경우 응답의 각 레코드에는 나열된 필드가 포함됩니다.  생략하면 기본 필드 집합인 `id`, `email`, `updatedAt`, `createdAt`, `firstName` 및 `lastName`이(가) 반환됩니다.

## ADOBE ECID

Adobe Experience Cloud 대상 공유 기능이 활성화되면 Adobe Experience Cloud ID(ECID)를 Marketo 리드와 연결하는 쿠키 동기화 프로세스가 발생합니다.  위에 언급된 리드 검색 방법은 연관된 ECID 값을 검색하는 데 사용할 수 있습니다.  필드 매개 변수에 `ecids`을(를) 지정하여 이 작업을 수행합니다. 예: `&fields=email,firstName,lastName,ecids`.

## 만들기 및 업데이트

리드 데이터를 검색하는 것 외에도 API를 통해 리드 레코드를 생성, 업데이트 및 삭제할 수 있습니다. 리드 생성 및 업데이트는 요청에 정의된 작업 유형과 동일한 끝점을 공유하며 최대 300개의 레코드를 동시에 생성 또는 업데이트할 수 있습니다.

>[!NOTE]
>
> [동기화 리드](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/syncLeadUsingPOST) 끝점을 사용하여 회사 필드를 업데이트할 수 없습니다. 대신 [회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies/operation/syncCompaniesUsingPOST) 끝점을 사용하십시오.

>[!NOTE]
>
> 개인 레코드에서 전자 메일 값을 만들거나 업데이트할 때 전자 메일 주소 필드에는 ASCII 문자만 지원됩니다.

### 요청

```
POST /rest/v1/leads.json
```

### 본문

```json
{
   "action":"createOnly",
   "lookupField":"email",
   "input":[
      {
         "email":"kjashaedd-1@klooblept.com",
         "firstName":"Kataldar-1",
         "postalCode":"04828"
      },
      {
         "email":"kjashaedd-2@klooblept.com",
         "firstName":"Kataldar-2",
         "postalCode":"04828"
      },
      {
         "email":"kjashaedd-3@klooblept.com",
         "firstName":"Kataldar-3",
         "postalCode":"04828"
      }
   ]
}
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "id":50,
         "status":"created"
      },
      {
         "id":51,
         "status":"created"
      },
      {
         "id":52,
         "status":"created"
      }
   ]
}
```

이 요청에는 두 개의 중요한 필드 `action`과(와) `lookupField`이(가) 표시됩니다.  `action`은(는) 요청의 작업 형식을 지정하며 `createOrUpdate`, `createOnly`, `updateOnly` 또는 `createDuplicate`일 수 있습니다. 생략하면 작업의 기본값이 `createOrUpdate`(으)로 설정됩니다.  `lookupField` 매개 변수는 작업이 `createOrUpdate` 또는 `updateOnly`일 때 사용할 키를 지정합니다. `lookupField`을(를) 생략하면 기본 키는 `email`입니다.

기본적으로 기본 파티션이 사용됩니다. 선택적으로 `partitionName` 매개 변수를 지정할 수 있습니다. 이 매개 변수는 작업이 `createOnly` 또는 `createOrUpdate`인 경우에만 작동합니다. `partitionName`이(가) 추가 중복 제거 기준으로 작동하려면 사용자 지정 중복 제거 규칙에서 소스 유형의 일부여야 합니다. 업데이트 작업 중에 지정된 파티션에 잠재 고객이 없으면 오류가 반환됩니다. API 전용 사용자에게 지정된 파티션에 액세스할 수 있는 권한이 없는 경우 오류가 반환됩니다.

`id`은(는) 시스템 관리 고유 키이므로 `updateOnly` 작업을 사용할 때만 `id` 필드를 매개 변수로 포함할 수 있습니다.

요청에는 리드 레코드 배열인 `input` 매개 변수도 있어야 합니다. 각 리드 레코드는 리드 필드가 수에 관계없이 있는 JSON 개체입니다. 레코드에 포함된 키는 해당 레코드에 대해 고유해야 하며 모든 JSON 문자열은 UTF-8로 인코딩되어야 합니다. `externalCompanyId` 필드는 잠재 고객 레코드를 회사 레코드에 연결하는 데 사용할 수 있습니다. `externalSalesPersonId` 필드는 잠재 고객 레코드를 영업 사원 레코드에 연결하는 데 사용할 수 있습니다.

주: 가망 고객 갱신 요청을 동시에 또는 빠르게 연속하여 수행할 때, 동일한 값을 가진 후속 호출이 첫 번째 반환 전에 수행되면 동일한 키 값으로 여러 요청을 수행할 때 중복 레코드가 발생할 수 있습니다. 필요에 따라 `createOnly` 또는 `updateOnly`을(를) 사용하거나, 같은 키로 후속 업데이트를 호출하기 전에 호출을 큐에 넣고 호출이 반환되기를 기다리면 이 문제를 방지할 수 있습니다.

## 필드

리드 오브젝트에는 표준 필드와 선택적으로 사용자 정의 필드가 포함됩니다. 표준 필드는 모든 Marketo Engage 구독에 표시되지만 사용자 지정 필드는 사용자가 필요에 따라 생성됩니다. 각 필드 정의는 필드를 설명하는 속성 세트로 구성됩니다. 속성의 예로는 디스플레이 이름, API 이름 및 dataType이 있습니다. 이러한 속성을 통칭하여 메타데이터라고 합니다.

다음 엔드포인트를 사용하면 리드 오브젝트에서 필드를 쿼리하고 만들고 업데이트할 수 있습니다. 이러한 API를 사용하려면 소유 API 사용자에게 읽기-쓰기 스키마 표준 필드 또는 읽기-쓰기 스키마 사용자 정의 필드 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

## 쿼리 필드

리드 필드 쿼리는 간단합니다. API 이름으로 단일 리드 필드를 쿼리하거나 모든 리드 필드의 집합을 쿼리할 수 있습니다. 사용 중인 역할 권한에 따라 표준 필드와 사용자 지정 필드를 모두 검색할 수 있습니다. 숨겨진 필드도 검색됩니다.

## 이름별

Get Lead Field by Name 끝점은 리드 오브젝트의 단일 필드에 대한 메타데이터를 검색합니다. 필수 fieldApiName 경로 매개 변수는 필드의 API 이름을 지정합니다. 응답은 Describe Lead 엔드포인트와 유사하지만 필드가 사용자 정의 필드인지 여부를 나타내는 isCustom 속성과 같은 추가 메타데이터를 포함합니다.

### 요청

```
GET /rest/v1/leads/schema/fields/{fieldApiName}.json
```

### 응답

```json
{
    "requestId": "cd97#1793ee0fec4",
    "result": [
        {
            "displayName": "Email Address",
            "name": "email",
            "description": null,
            "dataType": "email",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        }
    ],
    "success": true
}
```

## 찾아보기

리드 필드 가져오기 끝점은 를 포함하여 리드 오브젝트의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드가 반환됩니다. `batchSize` 쿼리 매개 변수를 사용하여 이 수를 줄일 수 있습니다. `moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. `moreResult` 특성이 false를 반환할 때까지 이 끝점을 계속 호출하십시오. 즉, 사용 가능한 결과가 없습니다. 이 API에서 반환된 `nextPageToken`은(는) 항상 이 호출의 다음 반복에 재사용해야 합니다.

### 요청

```
GET /rest/v1/leads/schema/fields.json
```

### 응답(잘림)

```json
{
    "requestId": "142c3#1793eb976d8",
    "result": [
        {
            "displayName": "Salutation",
            "name": "salutation",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "First Name",
            "name": "firstName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Middle Name",
            "name": "middleName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Last Name",
            "name": "lastName",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Date of Birth",
            "name": "dateOfBirth",
            "description": null,
            "dataType": "date",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Email Address",
            "name": "email",
            "description": null,
            "dataType": "email",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Phone Number",
            "name": "phone",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Mobile Phone Number",
            "name": "mobilePhone",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Fax Number",
            "name": "fax",
            "description": null,
            "dataType": "phone",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Job Title",
            "name": "title",
            "description": null,
            "dataType": "string",
            "length": 255,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": true,
            "isCustom": false
        },
        {
            "displayName": "Unsubscribed",
            "name": "unsubscribed",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": true,
            "isCustom": false
        },
        ...
    ],
    "success": true,
    "moreResult": false
}
```

## 필드 만들기

리드 필드 만들기 엔드포인트는 리드 오브젝트에 하나 이상의 사용자 정의 필드를 만듭니다. 이 끝점은 Marketo Engage UI에서 사용할 수 있는 것과 비슷한 기능을 제공합니다. 이 끝점을 사용하여 최대 100개의 사용자 지정 필드를 만들 수 있습니다.
API를 사용하여 Marketo Engage의 프로덕션 인스턴스에서 만드는 각 필드를 신중하게 고려합니다.  필드가 만들어지면 삭제할 수 없습니다(숨길 수만 있습니다). 사용하지 않는 필드의 확산은 인스턴스에 혼란을 가중시킬 나쁜 관행입니다.

필수 입력 매개 변수는 리드 필드 개체의 배열입니다. 각 객체에는 하나 이상의 속성이 포함됩니다. 필수 특성은 각각 필드의 UI 표시 이름, 필드의 API 이름 및 필드 형식에 해당하는 `displayName`, `name` 및 `dataType`입니다.  선택적으로 `description`, `isHidden`, `isHtmlEncodingInEmail` 및 `isSensitive`을(를) 지정할 수 있습니다.

이름 및 `displayName` 명명과 관련된 규칙이 몇 가지 있습니다. 이름 속성은 고유해야 하며 문자로 시작하고 문자, 숫자 또는 밑줄만 포함해야 합니다. `displayName`은(는) 고유해야 하며 특수 문자를 포함할 수 없습니다.  일반적인 명명 규칙은 `displayName`에 낙타 대소문자를 적용하여 이름을 생성하는 것입니다. 예를 들어 `displayName`의 &quot;내 사용자 지정 필드&quot;는 &quot;myCustomField&quot;라는 이름을 생성합니다.

### 요청

```
POST /rest/v1/leads/schema/fields.json
```

### 본문

```json
{
  "input": [
      {
        "displayName": "Acme Access Code",
        "name": "acmeAccessCode",
        "description": "Acme Direct Mail Integration",
        "dataType": "string"
      },
      {
        "displayName": "Acme Mail Date",
        "name": "acmeMailDate",
        "description": "Acme Direct Mail Integration",
        "dataType": "string"
      }
  ]
}
```

### 응답

```json
{
    "requestId": "d9f1#17943666811",
    "result": [
        {
            "name": "acmeAccessCode",
            "status": "created"
        },
        {
            "name": "acmeMailDate",
            "status": "created"
        }
    ],
    "success": true
}
```

## 필드 업데이트

리드 필드 업데이트 엔드포인트는 리드 오브젝트의 단일 사용자 정의 필드를 업데이트합니다. 대부분의 경우 Marketo Engage UI를 사용하여 수행된 필드 업데이트 작업은 API를 사용하여 달성할 수 있습니다. 아래 표에 요약된 몇 가지 차이점이 있다.

<table>
<tbody>
<tr>
<td style="width: 26.5306%;" rowspan="2"><strong>속성</strong></td>
<td style="width: 35%;" colspan="2"><strong>표준 필드</strong></td>
<td style="width: 38.2654%;" colspan="2"><strong>사용자 정의 필드</strong></td>
</tr>
<tr>
<td style="width: 17.449%;"><strong>API로 업데이트할 수 있습니까?</strong></td>
<td style="width: 17.551%;"><strong>UI로 업데이트할 수 있습니까?</strong></td>
<td style="width: 19.3878%;"><strong>API로 업데이트할 수 있습니까?</strong></td>
<td style="width: 18.8776%;"><strong>UI로 업데이트할 수 있습니까?</strong></td>
</tr>
<tr>
<td style="width: 26.5306%;">dataType</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">아니요</td>
<td style="width: 19.3878%;">아니요</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">설명</td>
<td style="width: 17.449%;">예</td>
<td style="width: 17.551%;">예</td>
<td style="width: 19.3878%;">예</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">displayName</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">아니요</td>
<td style="width: 19.3878%;">예</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">isCustom</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">아니요</td>
<td style="width: 19.3878%;">아니요</td>
<td style="width: 18.8776%;">아니요</td>
</tr>
<tr>
<td style="width: 26.5306%;">isHidden</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">예</td>
<td style="width: 19.3878%;">예(API로 생성된 경우)</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">isHtmlEncodingInEmail</td>
<td style="width: 17.449%;">예</td>
<td style="width: 17.551%;">예</td>
<td style="width: 19.3878%;">예</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">중요</td>
<td style="width: 17.449%;">예</td>
<td style="width: 17.551%;">예</td>
<td style="width: 19.3878%;">예</td>
<td style="width: 18.8776%;">예</td>
</tr>
<tr>
<td style="width: 26.5306%;">length</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">아니요</td>
<td style="width: 19.3878%;">아니요</td>
<td style="width: 18.8776%;">아니요</td>
</tr>
<tr>
<td style="width: 26.5306%;">이름</td>
<td style="width: 17.449%;">아니요</td>
<td style="width: 17.551%;">아니요</td>
<td style="width: 19.3878%;">아니요</td>
<td style="width: 18.8776%;">아니요</td>
</tr>
</tbody>
</table>

필수 `fieldApiName` 경로 매개 변수는 업데이트할 필드의 API 이름을 지정합니다. 필수 입력 매개 변수는 단일 리드 필드 개체를 포함하는 배열입니다.  필드 개체에는 하나 이상의 특성이 포함되어 있습니다.

### 요청

```
POST /rest/v1/leads/schema/fields/{fieldApiName}.json
```

### 본문

```json
{
  "input": [
      {
        "displayName": "Acme Access Code",
        "description": "Acme Direct Mail Integration",
        "isHtmlEncodingInEmail": true
      }
  ]
}
```

### 응답

```json
{
    "requestId": "9f57#1794324f44c",
    "result": [
        {
            "name": "acmeAccessCode",
            "status": "updated"
        }
    ],
    "success": true
}
```

## Marketo으로 리드 푸시

푸시 리드는 Marketo에 리드 동기화를 위한 대안으로서, 기본적으로 표준 동기화 리드(Marketo 양식과 사용 방식 유사)보다 더 많은 트리거 기능을 허용하도록 설계되었습니다. 리드 필드의 동기화 외에도 이 엔드포인트는 엔드포인트에 전달되는 쿠키 값을 기반으로 리드 연결을 허용합니다. 이 작업은 Marketo 이메일을 클릭하거나 호출에서 프로그램 이름을 전달하여 생성된 `mkt_tok` 값을 전달함으로써 수행됩니다. 이 끝점은 또한 Marketo의 프로그램 및/또는 캠페인에 연결된 단일 트리거 가능 활동을 만듭니다. 이를 통해 특정 캠페인 또는 프로그램에 기인한 리드 캡처 이벤트를 트리거하여 Marketo 내에서 관련 워크플로우를 시작할 수 있습니다.

푸시 리드 인터페이스는 동기화 리드와 매우 유사합니다. 동일한 기본 키가 모두 유효하며 필드에 동일한 API 이름이 사용됩니다(항상 업데이트 작업이므로 작업 매개 변수는 없음). `programName` 및 입력 매개 변수가 필요하며 `lookupField`, `source` 및 `reason` 매개 변수는 선택 사항입니다. 입력 매개변수는 리드 객체의 배열입니다. 결과 활동은 이름이 지정된 해당 프로그램에 기인합니다. `source` 및 `reason` 매개 변수는 요청에 추가하여 결과 활동에 해당 값을 포함할 수 있는 임의의 문자열 필드입니다. 해당 트리거(리드가 Marketo으로 푸시됨) 및 필터(리드가 Marketo으로 푸시됨)의 제약 조건으로 사용할 수 있습니다.

익명 활동에 대한 참고 사항. 이전 익명 활동을 새로 생성된 리드와 연결하려면 리드 개체에 쿠키 속성을 지정하지 말고 푸시 리드 다음에 리드 연결을 호출하십시오. 활동 내역이 없는 새 리드를 만들려면 리드 개체에 cookies 속성을 지정하기만 하면 됩니다.

### 요청

```
POST /rest/v1/leads/push.json
```

### 본문

```json
{
    "programName": "Big Blue Thing Product Launch",
    "source": "Cool Sales Site",
    "reason": "Downloaded pricing sheet",
    "lookupField": "email",
    "input": [
        {
             "email": "Theresa.May@westminister.gov.uk",
             "country": "united kingdom",
             "firstName": "Theresa",
             "website": "www.brexit.com",
             "leadScore": 45,
             "marketoSocialFacebookProfileURL": "http://www.facebook.com/id/23434456",
             "jobTitle": "Prime Minister"
         },
         {
             "email": "Justin.Trudeau@ottowa.gov.ca",
             "country": "canada",
             "firstName": "Justin",
             "website": "www.take-off-eh.com",
             "leadScore": 92,
             "marketoSocialFacebookProfileURL": "http://www.facebook.com/id/42434",
             "jobTitle": "Sonny"
         }
     ]
}
```

### 응답

```json
{
    "requestId": "939079529805",
    "success": true,
    "warnings": [],
    "result": [
       {
           "id": 483894,
           "status": "created"
       },
       {
           "id": 1087425,
           "status": "updated"
       },
       {
           "id": 3525,
           "reasons": [
                    {
                        "code": "501",
                        "message": "Bad stuff happened"
                    }
           ]
       }
    ]
}
```

`mkt_tok` 매개 변수를 전달하려면 다음과 같이 입력 매개 변수의 잠재 고객 레코드 내에 있는 mktToken 멤버에 값을 지정하십시오.

### 본문

```json
{
  "programName": "Big Blue Thing Product Launch",
  "source": "Cool Sales Site",
  "reason": "Downloaded pricing sheet",
  "lookupField": "mktToken",
  "input" : [
     {
       "mktToken" : "<tokenValue>",
       "firstName" : "Thelma"
     },
     {
       "mktToken" : "<tokenValue>",
       "firstName" : "Louise"
     }
   ]
}
```

## 양식 제출

양식 제출은 Marketo 리드를 동기화하는 다른 대안이며, Marketo 양식 제출과 동등한 기능을 제공하도록 설계되었습니다. 이를 통해 특정 캠페인 또는 프로그램에 기인한 리드 캡처 이벤트를 트리거하여 Marketo 내에서 관련 워크플로우를 시작할 수 있습니다.

양식 제출 엔드포인트는 다음 기능을 지원합니다.

* 이메일 필드를 기본 키로 사용하여 잠재 고객 레코드 업데이트
* 프로그램 및/또는 캠페인에 연결된 &quot;양식 작성&quot; 활동을 만듭니다.
* 쿠키 값을 기반으로 잠재 고객 연결 허용
* 양식 필드 유효성 검사 수행

양식을 제출하는 것은 표준 리드 데이터베이스 패턴을 따릅니다. 단일 오브젝트 레코드가 POST 요청의 JSON 본문의 필수 입력 멤버로 전달됩니다. 필수 `formId` 구성원에 대상 Marketo 양식 ID가 포함되어 있습니다.

선택적 `programId`을(를) 사용하여 리드를 추가할 프로그램을 지정하거나 프로그램 멤버 사용자 지정 필드를 추가할 프로그램을 지정할 수 있습니다. `programId`을(를) 제공하면 프로그램에 잠재 고객이 추가되고 양식에 포함된 모든 프로그램 멤버 필드도 추가됩니다. 지정된 프로그램은 양식과 동일한 작업 영역에 있어야 합니다. 양식에 프로그램 멤버 사용자 지정 필드가 없고 `programId`이(가) 제공되지 않으면 프로그램에 잠재 고객이 추가되지 않습니다. 양식이 프로그램에 있고 `programId`이(가) 제공되지 않은 경우 양식에 하나 이상의 프로그램 멤버 사용자 정의 필드가 있으면 해당 프로그램이 사용됩니다.

입력 레코드 내에서 `leadFormFields` 개체가 필요합니다. 이 개체에는 채울 양식 필드에 해당하는 이름/값 쌍이 하나 이상 포함되어 있습니다.  지정된 모든 필드는 지정된 양식 내에서 정의되어야 합니다. 이름은 필드에 대한 REST API 이름입니다. `email` 필드는 필수입니다.

`visitorData` 멤버 개체는 선택 사항이며 `pageURL`, `queryString`, `leadClientIpAddress` 및 `userAgentString`을(를) 포함한 페이지 방문 데이터에 해당하는 이름/값 쌍을 포함합니다. 필터링 및 트리거를 위해 추가 활동 필드를 채우는 데 사용할 수 있습니다.

쿠키 멤버 문자열은 선택 사항이며 Munchkin 쿠키를 Marketo의 개인 레코드와 연결할 수 있습니다. 새 잠재 고객을 만들 때 쿠키 값이 이전에 알려진 다른 레코드와 연결되어 있지 않은 경우 이전의 모든 익명 활동은 해당 잠재 고객과 연결됩니다. 쿠키 값이 이전에 연결된 경우 새 활동이 레코드에 대해 추적되지만 이전 활동은 알려진 기존 레코드에서 마이그레이션되지 않습니다. 활동 내역이 없는 새 잠재 고객을 만들려면 쿠키 구성원을 생략하면 됩니다.

양식이 있는 작업 영역의 기본 파티션에 새 잠재 고객이 만들어집니다.

### 요청

```
POST /rest/v1/leads/submitForm.json
```

### Header

```
Content-Type: application/json
```

### 본문

```json
{
  "formId": 1029,
  "input": [
    {
      "leadFormFields": {
        "firstName": "Marge",
        "lastName": "Simpson",
        "email": "marge.simpson@fox.com",
        "pMCFField": "PMCF value"
      },
      "visitorData": {
        "pageURL": "https://na-sjst.marketo.com/lp/063-GJP-217/UnsubscribePage.html",
        "queryString": "Unsubscribed=yes",
        "leadClientIpAddress": "192.150.22.5",
        "userAgentString": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.89 Safari/537.36"
      },
      "cookie": "id:063-GJP-217&token:_mch-marketo.com-1594662481190-60776"
    }
  ]
}
```

### 응답

```json
{
  "requestId": "10667#173bc585ca5",
  "result": [
    {
      "id": 319174,
      "status": "updated"
    }
  ],
  "success": true
}
```

여기에서는 Marketo Engage UI 내에서 해당 &quot;양식 작성&quot; 활동 세부 사항을 볼 수 있습니다.

![양식 UI 작성](assets/fill_out_form_activity_details.png)

## 병합

경우에 따라 중복 레코드를 병합해야 하며 Marketo은 리드 병합 API를 통해 이를 용이하게 합니다. 리드를 병합하면 활동 로그, 프로그램, 캠페인, 목록 멤버십 및 CRM 정보가 결합되고 모든 필드 값이 단일 레코드로 병합됩니다. 병합 리드는 리드 ID를 경로 매개 변수로 사용하고, 단일 `leadId`을(를) 쿼리 매개 변수로 사용하거나, `leadIds` 매개 변수에 쉼표로 구분된 ID 목록을 사용합니다.

### 요청

```
POST /rest/v1/leads/{id}/merge.json?leadId=1324
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

경로 매개 변수에 지정된 리드는 우승 리드이므로 병합되는 레코드 사이에 충돌하는 필드가 있으면 우승 레코드의 필드가 비어 있고 손실 레코드의 해당 필드가 아닌 경우를 제외하고 우승자의 값이 사용됩니다. `leadId` 또는 `leadIds` 매개 변수에 지정된 잠재 고객이 손실 중인 잠재 고객입니다.

SFDC 동기화가 활성화된 구독이 있는 경우 요청에서 `mergeInCRM` 매개 변수를 사용할 수도 있습니다. true로 설정하면 CRM의 해당 병합도 수행됩니다. 두 리드가 모두 SFDC에 있고 하나는 CRM 리드이고 다른 하나는 CRM 연락처인 경우 승자는 CRM 연락처입니다(어떤 리드가 승자로 지정되었는지에 관계없이). 리드 중 하나가 SFDC에 있고 다른 하나는 Marketo에만 있는 경우 우승자는 SFDC 리드입니다(우승자로 지정된 리드에 관계없이).

## 웹 활동 연결

Marketo은 리드 추적(Munchkin)을 통해 웹 사이트 및 Marketo 랜딩 페이지 방문자에 대한 웹 활동을 기록합니다. 방문 및 클릭이라는 이러한 활동은 잠재 고객의 브라우저에 설정된 &quot;_mkto_trk&quot; 쿠키에 해당하는 키로 기록되며, Marketo은 이 키를 사용하여 동일한 사용자의 활동을 추적합니다. 일반적으로 잠재 고객 레코드와 연결은 잠재 고객이 Marketo 이메일을 통해 클릭스루하거나 Marketo 양식을 작성할 때 발생하지만, 경우에 따라 다른 유형의 이벤트에 의해 연결이 트리거될 수 있으며 연결된 잠재 고객 끝점을 사용하여 이 작업을 수행할 수 있습니다. 끝점은 알려진 잠재 고객 레코드의 ID를 경로 매개 변수로 사용하고 쿠키 쿼리 매개 변수의 &quot;_mkto_trk&quot; 쿠키 값을 사용합니다.

### 요청

```
POST /rest/v1/leads/{id}/associate.json?cookie=id:287-GTJ-838%26token:_mch-marketo.com-1396310362214-46169
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

쿠키가 이미 알려진 잠재 고객 레코드와 연결된 경우 다른 잠재 고객 레코드에서 이 API를 사용하면 해당 레코드에 대해 새 웹 활동이 기록되지만 기존 웹 활동은 새 레코드로 이동하지 않습니다.
멤버십

잠재 고객 레코드는 정적 목록 또는 프로그램의 구성원을 기반으로 검색할 수도 있습니다. 또한 잠재 고객이 멤버인 모든 정적 목록, 프로그램 또는 스마트 캠페인을 검색할 수 있습니다.

응답 구조 및 선택적 매개 변수는 필터 유형별 리드 가져오기의 매개 변수와 동일하지만 filterType 및 filterValues를 이 API와 함께 사용할 수 없습니다.
Marketo UI를 통해 목록 ID에 액세스하려면 목록으로 이동합니다. `id` 목록은 정적 목록 `https://app-****.marketo.com/#ST1001A1`의 URL에 있습니다. 이 예제에서 1001은 목록의 `id`입니다.

### 요청

```
GET /rest/v1/list/{listId}/leads.json?batchSize=3
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "nextPageToken":
"PS5VL5WD4UOWGOUCJR6VY7JQO2KUXL7BGBYXL4XH4BYZVPYSFBAONP4V4KQKN4SSBS55U4LEMAKE6===",
    "result":[
       {
            "id":50,
            "email":"kjashaedd@klooblept.com",
            "firstName":"Kataldar",
             "postalCode":"04828"
       },
       {
           "id":2343,
           "email":"kjashaedd@klooblept.com",
           "firstName":"Kataldar",
           "postalCode":"04828"
       },
      {
           "id":88498,
           "email":"kjashaedd@klooblept.com",
           "firstName":"Kataldar",
         "postalCode":"04828"
         }
    ]
}
```

잠재 고객 ID별 목록 가져오기 끝점은 잠재 고객 레코드 `id` 경로 매개 변수를 사용하고 잠재 고객이 멤버인 모든 정적 목록 레코드를 반환합니다.

### 요청

```
GET /rest/v1/leads/{id}/listMembership.json?batchSize=3
```

### 응답

```json
{
    "requestId": "1184b#1706f0ec23f",
    "result": [
        {
            "listId": 3379,
            "createdAt": "2016-05-17T19:32:44Z",
            "updatedAt": "2016-05-17T19:32:44Z"
        },
        {
            "listId": 2792,
            "createdAt": "2009-05-19T18:29:15Z",
            "updatedAt": "2009-05-19T18:29:15Z"
        },
        {
            "listId": 42,
            "createdAt": "2009-04-22T19:24:22Z",
            "updatedAt": "2009-04-22T19:24:22Z"
        }
    ],
    "success": true,
    "nextPageToken": "BFRV7OMVSNJWDVKVTUFS3XHT4E======",
    "moreResult": true
}
```

## 프로그램

프로그램 멤버십은 목록과 유사한 방식으로 검색할 수 있습니다. 프로그램 ID 끝점별 리드 가져오기 를 호출하고 `programId` 경로 매개 변수를 전달할 때 동일한 선택적 요청 매개 변수를 사용할 수 있습니다.

선택적으로 반환할 필드 이름의 쉼표로 구분된 목록이 포함된 필드 매개 변수를 전달할 수 있습니다. 필드 매개 변수가 이 요청에 포함되지 않으면 `email`, `updatedAt`, `createdAt`, `lastName`, `firstName`, `membership` 및 `id` 기본 필드가 반환됩니다. 필드 목록을 요청할 때 특정 필드가 요청되었지만 반환되지 않은 경우 값이 null로 간주됩니다.

각 레코드에 &quot;멤버십&quot;이라는 하위 개체도 있다는 점을 제외하고 결과 배열의 각 항목이 리드이므로 응답 구조는 매우 유사합니다. 이 멤버십 개체에는 호출에 표시된 프로그램에 대한 잠재 고객의 관계에 대한 데이터가 포함되어 있으며 항상 해당 `progressionStatus`, `acquiredBy`, `reachedSuccess` 및 `membershipDate`을(를) 표시합니다. 상위 프로그램도 참여 프로그램인 경우 멤버십에는 참여 프로그램에서의 위치 및 활동을 나타내는 `stream`, `nurtureCadence` 및 `isExhausted` 구성원이 포함됩니다.

### 요청

```
GET /rest/v1/leads/programs/{programId}.json?batchSize=3
```

### 응답

```json
{
    "requestId": "13ad4#1727b748a17",
    "result": [
        {
            "id": 319141,
            "firstName": "Meera",
            "lastName": "Reed",
            "email": "mree@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        },
        {
            "id": 319142,
            "firstName": "Jon",
            "lastName": "Umber",
            "email": "jumb@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        },
        {
            "id": 319143,
            "firstName": "Lyanna",
            "lastName": "Mormont",
            "email": "lmor@housestark.com",
            "updatedAt": "2020-04-21T16:27:14Z",
            "createdAt": "2020-04-21T16:27:14Z",
            "membership": {
                "id": 1127,
                "progressionStatus": "Visited",
                "progressionStatusType": "Visited",
                "isExhausted": false,
                "acquiredBy": true,
                "reachedSuccess": false,
                "membershipDate": "2020-04-21T16:27:16Z",
                "updatedAt": "2020-04-21T16:27:16Z"
            }
        }
    ],
    "success": true,
    "nextPageToken": "SW3PTMBVFCNHSHJGZ7LQH3ZWNUOHKADJZ3MOQ2LOZZVNO3WEIUPDKPRTTHBSMW756KOCWURTOF2XS==="
}
```

리드 ID별 프로그램 가져오기 엔드포인트는 리드 레코드 ID 경로 매개 변수를 사용하고 리드가 멤버로 있는 모든 프로그램 레코드를 반환합니다. 선택적 `filterType` 및 `filterValues` 매개 변수를 사용하면 프로그램 ID를 필터링할 수 있습니다.

### 요청

```
GET /rest/v1/leads/{id}/programMembership.json
```

### 응답

```json
{
    "requestId": "12e84#1706f13a379",
    "result": [
        {
            "id": 1044,
            "progressionStatus": "Sent",
            "isExhausted": false,
            "acquiredBy": false,
            "reachedSuccess": false,
            "membershipDate": "2016-05-27T19:50:29Z",
            "updatedAt": "2016-05-27T19:50:29Z"
        }
    ],
    "success": true,
    "moreResult": false
}
```

## 스마트 캠페인

잠재 고객 ID별 스마트 캠페인 가져오기 엔드포인트는 잠재 고객 레코드 ID 경로 매개 변수를 가져와 잠재 고객이 멤버로 속한 모든 스마트 캠페인 레코드를 반환합니다.

### 요청

```
GET /rest/v1/leads/{id}/smartCampaignMembership.json?batchSize=3
```

### 응답

```json
{
    "requestId": "e7b0#1706f163632",
    "result": [
        {
            "smartCampaignId": 3746,
            "createdAt": "2018-06-01T18:00:04Z",
            "updatedAt": "2018-06-01T18:00:06Z"
        },
        {
            "smartCampaignId": 3678,
            "createdAt": "2015-04-06T18:37:30Z",
            "updatedAt": "2015-04-06T18:37:41Z"
        },
        {
            "smartCampaignId": 3680,
            "createdAt": "2015-04-06T18:37:30Z",
            "updatedAt": "2015-04-06T18:37:40Z"
        }
    ],
    "success": true,
    "nextPageToken": "TNGAH3NKDUFDHNXUVGTNBXJCQM======",
    "moreResult": true
}
```

## 삭제

리드 삭제 끝점을 사용하면 리드를 쉽게 제거할 수 있습니다.  본문의 ID 속성을 사용하여 삭제할 리드 ID를 지정합니다.  요청당 최대 리드 수는 300개입니다.  Content-Type: application/json 헤더를 사용합니다.

### 요청

```
POST /rest/v1/leads/delete.json
```

### 본문

```json
{
   "input":[
      {
         "id": 235
      },
      {
         "id":766
      }
   ]
}
```

### 응답

```json
{
  "requestId":"3608#16664333670",
  "result":[
    {
      "id":235,
      "status":"deleted"
    },
    {
      "id":766,
      "status":"deleted"
    }
  ],
  "success":true
}
```

## 관계

* 리드 레코드의 externalCompanyId 필드를 통한 회사
* 잠재 고객 레코드의 externalSalesPersonId 필드를 통한 SalesPerson
* 프로그램 멤버십을 통한 프로그램
* 목록 멤버십을 통한 목록
* 활동의 leadId 필드를 통한 활동
* 리드 레코드의 개별 세그먼트 필드를 통한 세분화
* 리드 레코드에서 leadPartitionId를 통해 파티션 생성

## 시간 초과

리드 엔드포인트는 아래에 명시되지 않는 한 30초 시간 제한이 있습니다.

* 동기화 리드: 90초
* 리드 연결: 60초
* 리드 병합: 180s
* 리드 파티션 업데이트: 60s
* Marketo으로 리드 푸시: 90초
* 필터 유형별 리드 가져오기: 60s
* 목록 ID로 리드 가져오기: 60s
