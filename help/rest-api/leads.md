---
title: 잠재 고객
feature: REST API
description: 설명, ID 또는 필터별 쿼리, 기본 필드, 제한 및 ECID 검색을 포함한 Marketo Leads REST API 기능을 살펴봅니다.
exl-id: 0a2f7c38-02ae-4d97-acfe-9dd108a1f733
TQID: https://experienceleague.adobe.com/jZ-ecWTmHwq9gvp4fMaeuuGba6cgwYx0QCCyfkrEDHQ
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b0bb9048-d951-48d8-8232-45cf248a7e27id: c5f60233-d5ea-4453-a799-0ad258b4d399id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 2728
ht-degree: 3%

---

# 잠재 고객

[리드 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads)

Marketo 리드 API는 리드 레코드에서 CRUD 작업을 지원합니다. 또한 정적 목록 및 프로그램에서 잠재 고객의 멤버십을 수정하고 잠재 고객에 대한 스마트 캠페인 처리를 시작할 수 있습니다.

## 설명

Describe Lead 를 사용하여 REST API 를 통해 사용할 수 있는 필드와 각 필드의 메타데이터를 검색합니다.

- 데이터 유형
- REST API 이름
- 길이(해당하는 경우)
- 읽기 전용 상태
- 알기 쉬운 레이블

기술 은 필드 가용성 및 메타데이터에 대한 신뢰할 수 있는 기본 소스입니다.

### 요청

```http
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

실제 응답에는 결과 배열에 더 많은 필드가 포함됩니다. 각 항목은 잠재 고객 레코드에서 사용할 수 있는 필드를 나타내며 적어도 ID, displayName 및 데이터 유형을 포함합니다.

나머지 및 soap 하위 개체는 해당 API에 대해 필드가 유효한 경우에만 표시됩니다. `readOnly` 속성은 해당 API가 필드를 업데이트할 수 있는지 여부를 나타냅니다. length 속성이 있으면 필드의 최대 길이가 제공되고 dataType 속성은 필드의 데이터 형식이 제공됩니다.

## 쿼리

다음 두 가지 기본 방법 중 하나를 사용하여 리드를 검색합니다.

- Id별 Lead 가져오기 는 하나의 Lead ID 를 경로 매개 변수로 가져와서 하나의 Lead 레코드를 반환합니다.
- 필터 유형별 리드 가져오기는 선택한 필드가 제공된 값 중 하나와 일치하는 레코드를 찾습니다.

ID로 리드 가져오기의 경우 선택적으로 반환할 필드 이름의 쉼표로 구분된 목록과 함께 필드 매개 변수를 전달합니다. 요청에 필드가 누락된 경우 응답에는 `email`, `updatedAt`, `createdAt`, `lastName`, `firstName` 및 `id`이(가) 포함됩니다. 요청한 필드가 반환되지 않으면 해당 값은 null이 됩니다.

### 요청

```http
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

Id로 Lead 를 가져오면 항상 결과 배열의 첫 번째 위치에 있는 하나의 레코드를 반환합니다.

필터 유형별 리드 가져오기는 동일한 레코드 유형을 반환하며 페이지당 최대 300개의 레코드를 반환할 수 있습니다. `filterType` 및 `filterValues` 쿼리 매개 변수가 필요합니다.

`filterType`은(는) 모든 사용자 지정 필드 및 가장 일반적으로 사용되는 필드를 허용합니다. `filterType`에 허용된 검색 가능한 필드를 검색하려면 `Describe2` 끝점을 호출하십시오. 사용자 지정 필드로 검색할 때 지원되는 데이터 형식은 `string`, `email` 및 `integer`입니다. 설명 및 유형과 같은 필드 세부 사항을 검색하려면 Describe 메서드를 사용하십시오.

`filterValues`은(는) 최대 300개의 쉼표로 구분된 값을 허용합니다. 이 호출은 선택한 리드 필드가 해당 값 중 하나와 일치하는 레코드를 반환합니다. 1,000개 이상의 리드가 필터와 일치하는 경우 API는 &quot;1003, 너무 많은 결과가 필터와 일치함&quot;을 반환합니다.

총 GET 요청이 8KB를 초과하는 경우 API는 RFC 7231에 대해 &quot;414, URI가 너무 깁니다&quot;를 반환합니다. 이 제한을 해결하려면 GET을 POST로 변경하고 _method=GET 매개 변수를 추가한 다음 쿼리 문자열을 요청 본문에 넣습니다.

### 요청

```http
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

이 호출은 ID가 `filterValues`의 값과 일치하는 레코드를 반환합니다.

일치하는 레코드가 없으면 응답이 성공을 나타내고 빈 결과 배열이 포함됩니다.

### 응답

```json
{
"requestId": "177a1#1578b643357",
"result": [],
"success": true
}
```

ID별 리드 가져오기 및 필터 유형별 리드 가져오기는 모두 쉼표로 구분된 API 필드 목록이 포함된 필드 쿼리 매개 변수를 허용합니다. 필드가 있으면 각 응답 레코드에는 나열된 필드가 포함됩니다. 생략하면 응답에 `id`, `email`, `updatedAt`, `createdAt`, `firstName` 및 `lastName`이(가) 포함됩니다.

## ADOBE ECID

Adobe Experience Cloud 대상 공유 가 활성화되면 쿠키 동기화는 Adobe Experience Cloud ID(ECID) 값을 Marketo 리드와 연결합니다. 이전 리드 검색 방법을 사용하여 연결된 ECID 값을 검색하려면 필드 매개 변수에 `ecids`을(를) 포함하십시오. 예: `&fields=email,firstName,lastName,ecids`.

## 만들기 및 업데이트

리드 API는 리드 레코드를 생성, 업데이트 및 삭제할 수 있습니다. 만들기 및 업데이트 작업은 요청에 정의된 작업 유형과 동일한 끝점을 사용합니다. 한 개의 요청으로 최대 300개의 레코드를 만들거나 업데이트할 수 있습니다.

>[!NOTE]
>
> [동기화 리드](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/syncLeadUsingPOST) 끝점을 사용하여 회사 필드를 업데이트할 수 없습니다. 대신 [회사 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Companies/operation/syncCompaniesUsingPOST) 끝점을 사용하십시오.

>[!NOTE]
>
> 개인 레코드에서 전자 메일 값을 만들거나 업데이트할 때 전자 메일 주소 필드에는 ASCII 문자만 지원됩니다.

### 요청

```http
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

이 요청에서는 두 가지 중요한 필드를 사용합니다.

- `action`이(가) 작업 형식(`createOrUpdate`, `createOnly`, `updateOnly` 또는 `createDuplicate`)을 지정합니다. 생략하면 기본값은 `createOrUpdate`입니다.
- `lookupField`은(는) 작업이 `createOrUpdate` 또는 `updateOnly`인 경우 키를 지정합니다. 생략하면 기본값은 `email`입니다.

기본적으로 작업에서는 기본 파티션을 사용합니다. 선택적 `partitionName` 매개 변수는 작업이 `createOnly` 또는 `createOrUpdate`인 경우에만 작동합니다. `partitionName`을(를) 추가 중복 제거 기준으로 사용하려면 사용자 지정 중복 제거 규칙의 소스 유형에 포함하십시오.

업데이트하는 동안 지정된 파티션에 잠재 고객이 없거나 API 전용 사용자가 해당 파티션에 액세스할 수 없는 경우 API가 오류를 반환합니다.

`id`은(는) 시스템 관리 고유 키이므로 `updateOnly` 작업에만 포함하십시오.

요청에는 리드 레코드 배열을 포함하는 `input` 매개 변수가 포함되어야 합니다. 각 리드 레코드는 리드 필드가 수에 관계없이 있는 JSON 개체입니다. 키는 각 레코드 내에서 고유해야 하며 모든 JSON 문자열은 UTF-8 인코딩을 사용해야 합니다.

`externalCompanyId`을(를) 사용하여 잠재 고객 레코드를 회사 레코드에 연결합니다. `externalSalesPersonId`을(를) 사용하여 잠재 고객 레코드를 영업 사원 레코드에 연결합니다.

동시 또는 시간이 비슷한 업데이트 요청은 여러 요청이 동일한 키 값을 사용한 경우 첫 번째 요청이 반환되기 전에 중복 레코드를 만들 수 있습니다. 중복을 방지하려면 `createOnly` 또는 `updateOnly`을(를) 적절하게 사용하십시오. 또는 동일한 키를 사용하여 다른 업데이트를 제출하기 전에 호출을 큐에 넣고 각 호출이 반환되기를 기다립니다.

## 필드

잠재 고객 개체에는 표준 필드와 선택적 사용자 지정 필드가 포함되어 있습니다. 표준 필드는 모든 Marketo Engage 구독에 있지만 사용자는 필요에 따라 사용자 정의 필드를 만듭니다.

각 필드 정의에는 표시 이름, API 이름 및 dataType과 같은 메타데이터 속성이 포함됩니다.

리드 오브젝트의 필드를 쿼리하고 만들고 업데이트하려면 다음 끝점을 사용하십시오. API 사용자의 역할에는 읽기-쓰기 스키마 표준 필드 권한, 읽기-쓰기 스키마 사용자 정의 필드 권한 또는 둘 다가 있어야 합니다.

## 쿼리 필드

API 이름으로 리드 필드 하나를 쿼리하거나 모든 리드 필드를 쿼리합니다. 역할 권한에 따라, 응답에는 표준 필드, 사용자 지정 필드 및 숨겨진 필드가 포함될 수 있습니다.

## 이름별

Get Lead Field by Name 끝점은 하나의 Lead 필드에 대한 메타데이터를 검색합니다. 필수 fieldApiName 경로 매개 변수는 필드의 API 이름을 지정합니다.

응답은 리드 설명 응답과 유사하지만 추가 메타데이터를 포함합니다. 예를 들어 isCustom 속성은 필드가 사용자 지정인지 여부를 나타냅니다.

### 요청

```http
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

리드 필드 가져오기 엔드포인트는 리드 오브젝트의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드를 반환합니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

`moreResult`이(가) true이면 더 많은 결과를 사용할 수 있습니다. `moreResult`이(가) false가 될 때까지 후속 호출마다 반환된 `nextPageToken`을(를) 전달합니다.

### 요청

```http
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

리드 필드 만들기 엔드포인트는 리드 오브젝트에 하나 이상의 사용자 정의 필드를 만들고 Marketo Engage UI와 비슷한 기능을 제공합니다. 이 끝점으로 최대 100개의 사용자 지정 필드를 만들 수 있습니다.

프로덕션 인스턴스에서 생성하기 전에 각 필드를 신중하게 고려합니다. 필드를 만든 후에는 숨길 수 있지만 삭제할 수는 없습니다. 사용하지 않는 필드는 인스턴스에 혼란을 추가합니다.

필수 입력 매개 변수는 리드 필드 개체의 배열입니다. 각 객체에는 다음 속성이 필요합니다.

- `displayName`은(는) 필드의 UI 표시 이름입니다.
- `name`은(는) 필드의 API 이름입니다.
- `dataType`은(는) 필드 형식입니다.

선택적 특성은 `description`, `isHidden`, `isHtmlEncodingInEmail` 및 `isSensitive`입니다.

이름 속성은 고유해야 하며 문자로 시작하고 문자, 숫자 또는 밑줄만 포함해야 합니다. `displayName`은(는) 고유해야 하며 특수 문자를 포함할 수 없습니다.

일반적인 규칙에서는 `displayName`에 카멜 대/소문자를 적용하여 이름을 생성합니다. 예를 들어 `displayName`의 &quot;내 사용자 지정 필드&quot;는 &quot;myCustomField&quot;라는 이름을 생성합니다.

### 요청

```http
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

리드 필드 업데이트 엔드포인트는 리드 오브젝트에서 하나의 사용자 정의 필드를 업데이트합니다. Marketo Engage UI에서 사용할 수 있는 대부분의 필드 업데이트는 API를 통해서도 사용할 수 있습니다. 다음 표에는 차이점이 요약되어 있습니다.

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

필수 `fieldApiName` 경로 매개 변수는 업데이트할 필드의 API 이름을 지정합니다. 필수 입력 매개변수는 하나 이상의 속성을 가진 하나의 리드 필드 객체를 포함하는 배열입니다.

### 요청

```http
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

푸시 리드는 동기화 리드의 대안이며 Marketo 양식과 유사한 더 많은 트리거 옵션을 제공합니다. 리드 필드를 동기화하는 것 외에도 엔드포인트는 쿠키 값을 기반으로 리드를 연결할 수 있습니다. Marketo 이메일에서 클릭으로 생성된 `mkt_tok` 값을 전달하거나 호출에 프로그램 이름을 전달합니다.

또한 끝점은 Marketo 프로그램, 캠페인 또는 두 프로그램 모두와 연결된 하나의 트리거 가능한 활동을 만듭니다. 이 활동을 사용하여 특정 캠페인 또는 프로그램에 속하는 잠재 고객 캡처 이벤트에서 워크플로우를 시작할 수 있습니다.

푸시 리드는 동기화 리드와 동일한 기본 키 및 필드 API 이름을 사용합니다. 항상 업데이트를 수행하므로 작업 매개 변수가 없습니다.

`programName` 및 입력 매개 변수가 필요합니다. 입력 매개변수는 리드 객체의 배열이며 결과 활동은 명명된 프로그램에 속합니다. `lookupField`, `source` 및 `reason` 매개 변수는 선택 사항입니다. `source` 및 `reason`에 임의 문자열을 추가하여 결과 활동에 해당 값을 포함하십시오. 해당 트리거(리드가 Marketo으로 푸시됨) 및 필터(리드가 Marketo으로 푸시됨)의 제약 조건으로 값을 사용할 수 있습니다.

이전 익명 활동을 새로 생성된 리드와 연결하려면 리드 오브젝트에서 쿠키 속성을 생략하고 푸시 리드 후에 리드 연결을 호출합니다. 활동 내역이 없는 리드를 만들려면 리드 개체에 cookies 속성을 지정합니다.

### 요청

```http
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
             "jobTitle": "Prime Minister"
         },
         {
             "email": "Justin.Trudeau@ottowa.gov.ca",
             "country": "canada",
             "firstName": "Justin",
             "website": "www.take-off-eh.com",
             "leadScore": 92,
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

`mkt_tok` 매개 변수를 전달하려면 해당 값을 입력 매개 변수 내의 잠재 고객 레코드의 mktToken 멤버에 할당하십시오.

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

양식 제출은 가망 고객 동기화를 위한 대안이며 Marketo 양식 제출과 동등한 기능을 제공합니다. 특정 캠페인 또는 프로그램에 기인한 잠재 고객 캡처 이벤트에서 워크플로우를 시작하는 데 사용합니다.

양식 제출 엔드포인트는 다음 기능을 지원합니다.

- 이메일 필드를 기본 키로 사용하여 잠재 고객 레코드를 업데이트합니다.
- 프로그램, 캠페인 또는 두 가지 모두와 연결된 &quot;양식 작성&quot; 활동을 만듭니다.
- 쿠키 값을 기반으로 리드를 연결합니다.
- 양식 필드를 확인합니다.

표준 리드 데이터베이스 패턴이 있는 양식을 제출합니다. POST 요청 JSON 본문의 필수 입력 멤버에 하나의 개체 레코드를 전달합니다. 필수 `formId` 구성원에 대상 Marketo 양식 ID가 포함되어 있습니다.

선택적 `programId`을(를) 사용하여 잠재 고객, 프로그램 멤버 사용자 지정 필드 또는 두 필드를 모두 받는 프로그램을 식별하십시오. `programId`이(가) 있으면 양식의 모든 프로그램 멤버 필드와 함께 리드가 프로그램에 추가됩니다. 프로그램은 양식과 동일한 작업 영역에 있어야 합니다.

양식에 프로그램 멤버 사용자 지정 필드가 없고 `programId`을(를) 생략하면 프로그램에 리드가 추가되지 않습니다. 폼이 프로그램에 속하고 하나 이상의 프로그램 멤버 사용자 지정 필드가 있으며 `programId`을(를) 생략하면 끝점은 폼의 프로그램을 사용합니다.

필수 `leadFormFields` 개체에 채울 필드에 대한 이름/값 쌍이 하나 이상 포함되어 있습니다. 모든 필드는 지정된 양식에서 정의되어야 하며 각 이름은 필드의 REST API 이름이어야 합니다. `email` 필드는 필수입니다.

선택적 `visitorData` 개체에 `pageURL`, `queryString`, `leadClientIpAddress` 및 `userAgentString`을(를) 포함한 페이지 방문 데이터가 있습니다. 이를 사용하여 필터 및 트리거에 대한 추가 활동 필드를 채웁니다.

선택적 쿠키 멤버는 Munchkin 쿠키를 Marketo 개인 레코드와 연결합니다. 끝점이 잠재 고객을 만들면 쿠키가 이전에 알려진 다른 레코드와 연결되어 있지 않은 한 이전 익명 활동을 해당 잠재 고객과 연결합니다.

쿠키가 이전에 연결된 경우에는 새 레코드에 대해 새 활동이 추적되지만 이전 활동은 기존의 알려진 레코드와 함께 유지됩니다. 활동 내역이 없는 리드를 만들려면 쿠키 구성원을 생략합니다.

양식이 있는 작업 영역의 기본 파티션에 새 잠재 고객이 만들어집니다.

### 요청

```http
POST /rest/v1/leads/submitForm.json
```

### Header

```text
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

다음 이미지는 Marketo Engage UI에서 해당 &quot;양식 작성&quot; 활동 세부 정보를 보여 줍니다.

![양식 UI 작성](assets/fill_out_form_activity_details.png)

## 병합

>[!NOTE]
>
>2026년 3월 31일부터 병합 리드 API 호출의 `leadIds` 매개 변수에 25개가 넘는 ID를 포함하는 호출은 1080 오류 코드를 발생시키고 호출을 건너뜁니다. 25개 이상의 레코드를 하나로 병합해야 하는 작업은 이러한 호출이 성공할 수 있도록 여러 작업으로 분할해야 합니다.
>

리드 병합 API를 사용하여 중복 레코드를 하나의 레코드로 결합합니다. 병합은 활동 로그, 프로그램, 캠페인 및 목록 멤버십, CRM 정보 및 필드 값을 결합합니다.

우승 리드 ID를 경로 매개 변수로 전달합니다. `leadId` 중 하나를 쿼리 매개 변수로 전달하거나 `leadIds` 매개 변수에 최대 25개의 쉼표로 구분된 ID를 전달합니다.


### 요청

```http
POST /rest/v1/leads/{id}/merge.json?leadId=1324
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

경로 매개 변수의 리드가 우승 리드입니다. 필드 값이 충돌하는 경우 해당 값이 비어 있고 손실된 레코드의 값이 그렇지 않은 경우 병합에서 승자의 값을 사용합니다. `leadId` 또는 `leadIds` 매개 변수의 잠재 고객이 손실 중인 잠재 고객입니다.

SFDC 동기화가 활성화된 구독의 경우 `mergeInCRM` 매개 변수를 사용하여 CRM에서 병합도 수행합니다. 두 레코드가 모두 SFDC에 있고 하나는 CRM 리드이고 다른 하나는 CRM 연락처인 경우 CRM 연락처는 지정된 승자와 관계없이 우승합니다. 한 개의 레코드가 SFDC에 있고 다른 레코드는 Marketo에만 있는 경우 SFDC 리드가 지정된 우승자와 관계없이 우승합니다.

## 웹 활동 연결

잠재 고객 추적(Munchkin)은 웹 사이트 및 Marketo 랜딩 페이지 방문자에 대한 방문 횟수 및 클릭 수를 기록합니다. 이러한 활동은 잠재 고객의 브라우저에서 &quot;_mkto_trk&quot; 쿠키에 해당하는 키를 사용하므로 Marketo이 동일한 사용자의 활동을 추적할 수 있습니다.

잠재 고객 레코드와 연결은 일반적으로 잠재 고객이 Marketo 이메일의 링크를 따라가거나 Marketo 양식을 제출할 때 발생합니다. 다른 유형의 이벤트 다음에 리드를 연결하려면 리드 연결 엔드포인트를 사용합니다. 알려진 잠재 고객 레코드 ID를 경로 매개 변수로 전달하고 쿠키 쿼리 매개 변수의 &quot;_mkto_trk&quot; 쿠키 값을 전달합니다.

### 요청

```http
POST /rest/v1/leads/{id}/associate.json?cookie=id:287-GTJ-838%26token:_mch-marketo.com-1396310362214-46169
```

### 응답

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true
}
```

쿠키가 이미 알려진 리드와 연결된 경우 다른 리드에 대해 이 API를 사용하면 새 레코드에 대해 새 웹 활동이 기록됩니다. 기존 웹 활동이 새 레코드로 이동하지 않습니다.
멤버십

정적 목록 또는 프로그램의 멤버십을 기반으로 잠재 고객 레코드를 검색합니다. 특정 리드를 포함하는 모든 정적 목록, 프로그램 또는 스마트 캠페인을 검색할 수도 있습니다.

응답 구조 및 선택적 매개 변수가 필터 유형별 리드 가져오기와 일치하지만 이 API는 `filterType` 또는 `filterValues`을(를) 허용하지 않습니다.

Marketo UI에서 목록 ID를 찾으려면 목록으로 이동하여 URL을 검사합니다. `https://app-****.marketo.com/#ST1001A1`에서 1001은 `id` 목록입니다.

## 리드 ID로 프로그램 가져오기

### 요청

```http
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

## 잠재 고객 ID별 목록 가져오기

잠재 고객 ID별 목록 가져오기 끝점은 잠재 고객 레코드 `id` 경로 매개 변수를 사용하고 잠재 고객을 포함하는 모든 정적 목록을 반환합니다.

### 요청

```http
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

목록 멤버십과 동일한 방법으로 프로그램 멤버십을 검색합니다. 프로그램 ID별 리드 가져오기는 동일한 선택적 요청 매개 변수를 허용하며 `programId` 경로 매개 변수가 필요합니다.

선택적으로, 쉼표로 구분된 필드 이름 목록이 포함된 필드 매개 변수를 전달합니다. 필드를 생략하면 응답에 `email`, `updatedAt`, `createdAt`, `lastName`, `firstName`, `membership` 및 `id`이(가) 포함됩니다. 요청한 필드가 반환되지 않으면 해당 값은 null이 됩니다.

결과 배열의 각 항목은 &quot;membership&quot;이라는 하위 개체가 있는 리드입니다. 이 개체는 요청된 프로그램에 대한 잠재 고객의 관계를 설명하며, 항상 `progressionStatus`, `acquiredBy`, `reachedSuccess` 및 `membershipDate`을(를) 포함합니다.

상위 프로그램이 참여 프로그램인 경우 멤버십에는 해당 프로그램에서 잠재 고객의 위치 및 활동을 설명하는 `stream`, `nurtureCadence` 및 `isExhausted`도 포함됩니다.

### 요청

```http
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

리드 ID별 프로그램 가져오기 엔드포인트는 리드 레코드 ID 경로 매개 변수를 사용하고 리드를 포함하는 모든 프로그램을 반환합니다. 선택적 `filterType` 및 `filterValues` 매개 변수를 사용하여 프로그램 ID를 필터링합니다.

### 요청

```http
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

리드 ID별 스마트 캠페인 가져오기 엔드포인트는 리드 레코드 ID 경로 매개 변수를 사용하고 리드를 포함하는 모든 스마트 캠페인을 반환합니다.

### 요청

```http
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

리드 삭제 엔드포인트를 사용하여 리드 레코드를 제거합니다. ID 속성을 사용하여 본문에 리드 ID를 지정합니다. 요청은 최대 300개의 리드를 삭제할 수 있습니다. Content-Type: application/json 헤더를 보냅니다.

### 요청

```http
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

- 리드 레코드에서 externalCompanyId 필드를 통한 회사
- 잠재 고객 레코드의 externalSalesPersonId 필드를 통한 SalesPerson
- 프로그램 멤버십을 통한 프로그램
- 목록 멤버십을 통한 목록
- 활동의 leadId 필드를 통한 활동
- 잠재 고객 레코드의 개별 세그먼트 필드를 통한 세분화
- 잠재 고객 레코드의 leadPartitionId 필드를 통해 파티션 나누기

## 시간 초과

리드 엔드포인트에는 30s 시간 제한이 있습니다. 단, 다음 엔드포인트는 예외입니다.

- 동기화 리드: 90초
- 리드 연결: 60초
- 리드 병합: 180s
- 리드 파티션 업데이트: 60s
- Marketo으로 리드 푸시: 90초
- 필터 유형별 리드 가져오기: 60s
- 목록 ID로 리드 가져오기: 60s
