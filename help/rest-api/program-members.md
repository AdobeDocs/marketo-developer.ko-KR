---
title: "프로그램 구성원"
feature: REST API
description: "프로그램 구성원을 만들고 관리합니다."
source-git-commit: 2185972a272b64908d6aac8818641af07c807ac2
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 0%

---


# 프로그램 구성원

[프로그램 멤버 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members)

Marketo은 프로그램 멤버 레코드를 읽고, 만들고, 업데이트하고, 삭제하기 위한 API를 노출합니다. 프로그램 구성원 레코드는 잠재 고객 ID 필드를 통해 잠재 고객 레코드와 관련되어 있습니다. 레코드는 표준 필드 세트와 선택적으로 최대 20개의 추가 사용자 정의 필드로 구성됩니다. 필드에는 각 멤버에 대한 프로그램별 데이터가 포함되어 있으며 양식, 필터, 트리거 및 흐름 작업에 사용할 수 있습니다. 이 데이터는 프로그램의 [구성원 탭](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/manage-and-view-members) Marketo Engage UI에서

## 설명

다음 [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) 엔드포인트는 리드 데이터베이스 개체의 표준 패턴을 따릅니다. 다음 `searchableFields` 배열은 쿼리에 유효한 필드 집합을 제공합니다. 다음 `fields` 배열에는 REST API 이름, 표시 이름 및 필드 업데이트 기능을 포함한 필드 메타데이터가 포함되어 있습니다.

```
GET /rest/v1/programs/members/describe.json
```

```json
{
    "requestId": "f813#1791563c7cc",
    "result": [
        {
            "name": "API Program Membership",
            "description": "Map for API program membership fields",
            "createdAt": "2021-03-20T01:30:05Z",
            "updatedAt": "2021-03-20T01:30:05Z",
            "dedupeFields": [
                "leadId",
                "programId"
            ],
            "searchableFields": [
                [
                    "leadId"
                ],
                [
                    "myCustomField"
                ],
                [
                    "reachedSuccess"
                ],
                [
                    "statusName"
                ]
            ],
            "fields": [
                {
                    "name": "acquiredBy",
                    "displayName": "acquiredBy",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "attendanceLikelihood",
                    "displayName": "attendanceLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "createdAt",
                    "displayName": "createdAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "isExhausted",
                    "displayName": "isExhausted",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "leadId",
                    "displayName": "leadId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "membershipDate",
                    "displayName": "membershipDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "nurtureCadence",
                    "displayName": "nurtureCadence",
                    "dataType": "string",
                    "length": 4,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "program",
                    "displayName": "program",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "programId",
                    "displayName": "programId",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccess",
                    "displayName": "reachedSuccess",
                    "dataType": "boolean",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "reachedSuccessDate",
                    "displayName": "reachedSuccessDate",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "registrationLikelihood",
                    "displayName": "registrationLikelihood",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusName",
                    "displayName": "statusName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "statusReason",
                    "displayName": "statusReason",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "trackName",
                    "displayName": "trackName",
                    "dataType": "string",
                    "length": 255,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "updatedAt",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "waitlistPriority",
                    "displayName": "waitlistPriority",
                    "dataType": "integer",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "myCustomField",
                    "displayName": "myCustomField",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "registrationCode",
                    "displayName": "registrationCode",
                    "dataType": "string",
                    "length": 100,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "webinarUrl",
                    "displayName": "webinarUrl",
                    "dataType": "string",
                    "length": 2000,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

## 쿼리

다음 [프로그램 구성원 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMembersUsingGET) 끝점을 사용하면 프로그램의 멤버를 검색할 수 있습니다. 이 작업을 수행하려면 `programId` 경로 매개 변수 및 `filterType` 및 `filterValues` 쿼리 매개 변수.

`programId` 검색할 프로그램을 지정하는 데 사용됩니다.

`filterType` 검색 필터로 사용할 필드를 지정하는 데 사용됩니다. 은(는) 다음에 의해 반환된 &quot;searchableFields&quot; 목록의 모든 필드를 수락합니다. [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) 엔드포인트. 사용자 지정 필드인 filterType을 지정하는 경우 사용자 지정 필드의 dataType은 &quot;string&quot; 또는 &quot;integer&quot;여야 합니다. filterType을 &quot;leadId&quot; 이외의 값으로 지정하면 요청으로 최대 100,000개의 프로그램 멤버 레코드를 처리할 수 있습니다. Marketo 인스턴스 구성 방법에 따라 다음 오류 중 하나를 받게 됩니다.

- 총 프로그램 구성원 수가 100,000명을 초과하는 경우 &quot;1003, 총 구성원 크기: 100,001이 필터에 허용되는 제한 100,000명을 초과합니다.&quot;라는 오류가 반환됩니다.
- 총 프로그램 구성원 수인 경우 _필터와 일치하는_ 100,000을 초과합니다. &quot;1003, 일치하는 멤버십 크기: 100,001이 이 api에 허용된 제한(100,000)을 초과합니다.&quot; 오류가 반환됩니다.

멤버십 수가 한도를 초과하는 프로그램을 쿼리하려면 [벌크 프로그램 멤버 추출 API](bulk-program-member-extract.md) 대신,

`filterValues` 는 검색할 값을 지정하는 데 사용되며, 쉼표로 구분된 형식으로 최대 300개의 값을 허용합니다. 호출은 프로그램 멤버의 필드가 포함된 filterValues 중 하나와 일치하는 레코드를 검색합니다.

또는 을 지정하여 날짜 범위별로 필터링할 수 있습니다 `updatedAt` 을 필터 유형으로 `startAt` 및 `endAt` datetime 매개 변수. 범위는 7일 이하여야 합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다.

선택 사항 `fields` 쿼리 매개변수는 다음에 의해 반환되는 쉼표로 구분된 필드 API 이름 목록을 수락합니다. [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) 엔드포인트. 포함되는 경우 응답의 각 레코드에는 지정된 필드가 포함됩니다. 생략하면 반환되는 기본 필드 세트는 다음과 같습니다 `acquiredBy`, `leadId`, `membershipDate`, `programId`, 및 `reachedSuccess`.

기본적으로 최대 300개의 레코드가 반환됩니다. 다음을 사용할 수 있습니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오. 다음과 같은 경우 **moreResult** 속성이 true이면 더 많은 결과를 사용할 수 있음을 의미합니다. moreResult 특성이 false를 반환할 때까지 이 끝점을 계속 호출합니다. 즉, 사용 가능한 결과가 없습니다. 다음 `nextPageToken` 이 API에서 반환된 내용은 항상 이 호출의 다음 반복에 재사용되어야 합니다.

GET 요청의 총 길이가 8KB를 초과하면 HTTP 오류 &quot;414, URI too long&quot;(단위 [RFC 7231](https://datatracker.ietf.org/doc/html/rfc72316.5.12)). 해결 방법으로, GET을 POST 로 변경하고 를 추가할 수 있습니다. `_method=GET` 매개 변수를 반환하고 요청 본문에 쿼리 문자열을 추가합니다.

```
GET /rest/v1/programs/{programId}/members.json?filterType=statusName&filterValues=Influenced
```

```json
{
    "requestId": "109da#17915eec072",
    "result": [
        {
            "seq": 0,
            "leadId": 1789,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 1,
            "leadId": 1790,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 2,
            "leadId": 1791,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 3,
            "leadId": 1792,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 4,
            "leadId": 1793,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 5,
            "leadId": 1794,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 6,
            "leadId": 1795,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 7,
            "leadId": 1796,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 8,
            "leadId": 1797,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 9,
            "leadId": 1798,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 10,
            "leadId": 1799,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        },
        {
            "seq": 11,
            "leadId": 1800,
            "reachedSuccess": true,
            "programId": 1044,
            "acquiredBy": true,
            "membershipDate": "2020-01-08T18:10:26Z"
        }
    ],
    "success": true,
    "moreResult": false
}
```

## 만들기 및 업데이트

프로그램 멤버에 대한 만들기/업데이트 작업을 지원하는 두 개의 끝점이 있습니다. 하나는 프로그램 멤버 상태만 업데이트할 수 있도록 해줍니다. 다른 하나는 &quot;업데이트 가능&quot;으로 표시된 프로그램 멤버 필드 집합을 업데이트할 수 있도록 해줍니다. 두 종단점을 사용하면 호출당 최대 300개의 프로그램 멤버 레코드를 수정할 수 있습니다.

### 프로그램 구성원 상태

다음 [동기화 프로그램 구성원 상태](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberStatusUsingPOST) endpoint는 하나 이상의 멤버에 대한 프로그램 상태를 만들거나 업데이트하는 데 사용됩니다.

필수 `programId` path 매개 변수는 만들거나 업데이트할 멤버가 포함된 프로그램을 지정합니다.

필수 `statusName` 매개 변수는 잠재 고객 목록에 적용할 프로그램 상태를 지정합니다. statusName은(는) 프로그램 채널에 사용 가능한 상태와 일치해야 합니다. 유효한 상태는 다음을 사용하여 검색할 수 있습니다. [채널 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Channels/operation/getAllChannelsUsingGET) 엔드포인트. 잠재 고객의 상태가 지정된 statusName보다 큰 단계 값을 가지면 해당 잠재 고객을 건너뜁니다.

필수 `input` 매개 변수는 의 배열입니다. `leadId` 프로그램 구성원에 해당합니다. 호출당 최대 300개의 leadId를 제출할 수 있습니다. 각 레코드에 대해 업데이트 작업이 수행됩니다. leadId가 프로그램 구성원과 연결된 경우 해당 구성원 상태가 업데이트됩니다. 그렇지 않은 경우 새 프로그램 구성원 레코드가 생성되고 해당 레코드가 leadId와 연결되며 구성원 상태가 할당됩니다.

끝점이 응답함 `status` / &quot;업데이트됨&quot;, &quot;생성됨&quot; 또는 &quot;건너뜀&quot; 건너뛴 경우 `reasons` 배열도 포함됩니다. 끝점은 또한 `seq` 필드는 제출된 레코드를 응답 순서에 연결하는 데 사용할 수 있는 색인입니다.

호출이 성공하면 &quot;프로그램 상태 변경&quot; 활동이 잠재 고객의 활동 로그에 기록됩니다.

```
POST /rest/v1/programs/{programId}/members/status.json
```

```
Content-Type: application/json
```

```json
{
    "statusName":"Influenced",
    "input":[
        {
            "leadId": 1800
        },
        {
            "leadId": 1801
        },
        {
            "leadId": 1235
        }
    ]
}
```

```json
{
    "requestId": "14b2d#17916378ec5",
    "result": [
        {
            "seq": 0,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1037",
                    "message": "Lead skipped because it is already in or past this status"
                }
            ]
        },
        {
            "seq": 1,
            "status": "updated",
            "leadId": 1801
        },
        {
            "seq": 2,
            "status": "created",
            "leadId": 1235
        }
    ],
    "success": true
}
```

### 프로그램 멤버 데이터

다음 [프로그램 구성원 데이터 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/syncProgramMemberDataUsingPOST) endpoint는 하나 이상의 멤버에 대한 프로그램 멤버 필드 데이터를 업데이트하는 데 사용됩니다. 사용자 정의 필드 또는 &quot;업데이트 가능한&quot; 표준 필드를 수정할 수 있습니다( 참조) [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) endpoint).

필수 `programId` path 매개 변수는 업데이트할 멤버가 포함된 프로그램을 지정합니다.

필수 `input` 매개 변수는 배열입니다. 각 배열 요소에는 `leadId` 업데이트할 하나 이상의 필드(API 이름 사용). 각 레코드에 대해 업데이트 작업이 수행됩니다. leadId는 프로그램 구성원과 연결되어 있어야 합니다. 필드를 업데이트할 수 있어야 합니다. 호출당 최대 300개의 leadId를 제출할 수 있습니다.

끝점이 응답함 `status` / &quot;업데이트됨&quot; 또는 &quot;건너뜀&quot; 건너뛴 경우 `reasons` 배열도 포함됩니다. 끝점은 또한 `seq` 필드는 제출된 레코드를 응답 순서에 연결하는 데 사용할 수 있는 색인입니다.

호출이 성공하면 &quot;프로그램 구성원 데이터 변경&quot; 활동이 잠재 고객의 활동 로그에 기록됩니다.

```
POST /rest/v1/programs/{programId}/members.json
```

```
Content-Type: application/json
```

```json
{
    "input":[
        {
            "leadId": 1789,
            "registrationCode": "dcff5f12-a7c7-11eb-bcbc-0242ac130002"
        },
        {
            "leadId": 1790,
            "registrationCode": "c0404b78-d3fd-47bf-82c4-d16f3852ab3a"
        },
        {
            "leadId": 1003,
            "registrationCode": "aa880c57-75b8-426b-a33a-fbf6302d7cb4"
        }
    ]
}
```

```json
{
    "requestId": "edc3#1791659b8d2",
    "result": [
        {
            "seq": 0,
            "status": "updated",
            "leadId": 1789
        },
        {
            "seq": 1,
            "status": "updated",
            "leadId": 1790
        },
        {
            "seq": 2,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1013",
                    "message": "Membership not found"
                }
            ]
        }
    ],
    "success": true
}
```

## 필드

프로그램 멤버 개체에는 표준 필드와 선택적 사용자 지정 필드가 포함되어 있습니다. 표준 필드는 모든 Marketo Engage 구독에 표시되지만 사용자 지정 필드는 사용자가 필요에 따라 생성됩니다. 각 필드 정의는 필드를 설명하는 속성 세트로 구성됩니다. 속성의 예로는 디스플레이 이름, API 이름 및 dataType이 있습니다. 이러한 속성을 통칭하여 메타데이터라고 합니다.

다음 끝점을 사용하면 프로그램 멤버 개체의 필드를 쿼리하고 만들고 업데이트할 수 있습니다. 이러한 API를 사용하려면 소유 API 사용자에게 다음 중 하나 또는 모두를 포함하는 역할이 있어야 합니다. **읽기-쓰기 스키마 표준 필드** 또는 **읽기-쓰기 스키마 사용자 정의 필드** 사용 권한.

### 쿼리 필드

프로그램 멤버 필드를 쿼리하는 방법은 간단합니다. API 이름으로 단일 프로그램 멤버 필드를 쿼리하거나 모든 프로그램 멤버 필드의 집합을 쿼리할 수 있습니다. 사용 중인 역할 권한에 따라 표준 필드와 사용자 지정 필드를 모두 검색할 수 있습니다. 숨겨진 필드도 검색됩니다.

#### 이름별

다음 [이름별 프로그램 구성원 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldByNameUsingGET) endpoint는 프로그램 멤버 개체의 단일 필드에 대한 메타데이터를 검색합니다. 필수 `fieldApiName` path 매개 변수는 필드의 API 이름을 지정합니다. 응답은 프로그램 멤버 설명 끝점과 유사하지만 다음과 같은 추가 메타데이터를 포함합니다. `isCustom` 필드가 사용자 지정 필드인지 여부를 나타내는 특성입니다.

```
GET /rest/v1/programs/members/schema/fields/{fieldApiName}.json
```

```json
{
    "requestId": "15416#17e955554de",
    "result": [
        {
            "displayName": "Status",
            "name": "statusName",
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
    "success": true
}
```

#### 찾아보기

다음 [프로그램 구성원 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/getProgramMemberFieldsUsingGET) endpoint는 프로그램 멤버 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드가 반환됩니다. 다음을 사용할 수 있습니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오. 다음과 같은 경우 `moreResult` 속성이 true이면 더 많은 결과를 사용할 수 있음을 의미합니다. moreResult 특성이 false를 반환할 때까지 이 끝점을 계속 호출합니다. 즉, 사용 가능한 결과가 없습니다. 다음 `nextPageToken` 이 API에서 반환된 내용은 항상 이 호출의 다음 반복에 재사용되어야 합니다.

```
GET /rest/v1/programs/members/schema/fields.json?batchSize=5
```

```json
{
    "requestId": "102f6#17e9557f123",
    "result": [
        {
            "displayName": "Acquired By",
            "name": "acquiredBy",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Nurture Cadence",
            "name": "nurtureCadence",
            "description": null,
            "dataType": "string",
            "length": 4,
            "isHidden": false,
            "isHtmlEncodingInEmail": true,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Nurture Exhausted",
            "name": "isExhausted",
            "description": null,
            "dataType": "boolean",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Member Date",
            "name": "membershipDate",
            "description": null,
            "dataType": "datetime",
            "isHidden": false,
            "isHtmlEncodingInEmail": false,
            "isSensitive": false,
            "isCustom": false,
            "isApiCreated": false
        },
        {
            "displayName": "Program",
            "name": "program",
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
    "nextPageToken": "BC7J6EPVLT6T4B5FKUU3APCYN4======",
    "moreResult": true
}
```

### 필드 만들기

다음 [프로그램 구성원 필드 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/createProgramMemberFieldUsingPOST) endpoint는 프로그램 멤버 개체에 하나 이상의 사용자 지정 필드를 만듭니다. 이 끝점은 와(과) 유사한 기능을 제공합니다. [Marketo Engage UI에서 사용 가능](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/program-member-custom-fields). 이 끝점을 사용하여 최대 20개의 사용자 지정 필드를 만들 수 있습니다.

API를 사용하여 Marketo Engage의 프로덕션 인스턴스에서 만드는 각 필드를 신중하게 고려합니다. 필드가 만들어지면 삭제할 수 없습니다([숨길 수만 있습니다.](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/delete-a-custom-field-in-marketo)). 사용하지 않는 필드의 확산은 인스턴스에 혼란을 가중시킬 나쁜 관행입니다.

필수 `input` 매개 변수는 프로그램 멤버 필드 개체의 배열입니다. 각 객체에는 하나 이상의 속성이 포함됩니다. 필수 속성은 다음과 같습니다. `displayName`, `name`, 및 `dataType` 필드의 UI 표시 이름, 필드의 API 이름 및 필드 유형에 각각 해당합니다. 선택적으로 다음을 지정할 수 있습니다. `description`, `isHidden`, `isHtmlEncodingInEmail`, 및 `isSensitive`.

다음과 관련된 몇 가지 규칙이 있습니다. `name` 및 `displayName` 이름 지정. 다음 `name` 속성은 고유해야 하며 문자로 시작하고 문자, 숫자 또는 밑줄만 포함해야 합니다. *`isplayName` 은(는) 고유해야 하며 특수 문자를 포함할 수 없습니다. 일반적인 명명 규칙은 다음과 같이 적용됩니다 [카멜 대/소문자](https://en.wikipedia.org/wiki/Camel_case#) 끝 `displayName` 생성 `name`. 예: `displayName` /내 사용자 지정 필드 -에서 `name` / &quot;myCustomField&quot;

```
POST /rest/v1/programs/members/schema/fields.json
```

```json
{
  "input": [
    {
        "displayName": "PMCF Custom Field 03",
        "name": "pMCFCustomField03",
        "description": "My third custom field",
        "dataType": "string"
    }
  ]
}
```

```json
{
    "requestId": "13a7#17e955fcb44",
    "result": [
        {
            "name": "pMCFCustomField03",
            "status": "created"
        }
    ],
    "success": true
}
```

### 필드 업데이트

다음 [프로그램 구성원 필드 업데이트](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/updateProgramMemberFieldUsingPOST) endpoint는 프로그램 멤버 개체의 단일 사용자 지정 필드를 업데이트합니다. 일반적으로 Marketo Engage UI를 사용하여 수행된 필드 업데이트 작업은 API를 사용하여 달성할 수 있습니다. 아래 표에 요약된 몇 가지 차이점이 있다.

| 속성 | API로 업데이트할 수 있습니까? | UI로 업데이트할 수 있습니까? | API로 업데이트할 수 있습니까? | UI로 업데이트할 수 있습니까? |
|---|---|---|---|---|
| dataType | 아니요 | 아니요 | 아니요 | 예 |
| 설명 | 예 | 예 | 예 | 예 |
| displayName | 아니요 | 아니요 | 예 | 예 |
| isCustom | 아니요 | 아니요 | 아니요 | 아니요 |
| isHidden | 아니요 | 예 | 예(API로 생성된 경우) | 예 |
| isHtmlEncodingInEmail | 예 | 예 | 예 | 예 |
| 중요 | 예 | 예 | 예 | 예 |
| length | 아니요 | 아니요 | 아니요 | 아니요 |
| 이름 | 아니요 | 아니요 | 아니요 | 아니요 |

필수 `fieldApiName` path 매개 변수는 업데이트할 필드의 API 이름을 지정합니다. 필수 `input` parameter는 단일 리드 필드 개체를 포함하는 배열입니다. 필드 개체에는 하나 이상의 특성이 포함되어 있습니다.

```
POST /rest/v1/programs/members/schema/fields/pMCFCustomField03.json
```

```json
{
  "input": [
      {
        "displayName": "Lunch Preference",
        "description": "Attendee food preference",
        "isHtmlEncodingInEmail": true
      }
  ]
}
```

```json
{
    "requestId": "215f#17e95663955",
    "result": [
        {
            "name": "pMCFCustomField03",
            "status": "updated"
        }
    ],
    "success": true
}
```

## 삭제

다음 [프로그램 구성원 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/deleteProgramMemberUsingPOST) 끝점은 프로그램 멤버 레코드를 삭제하는 데 사용됩니다. 필수 `programId` path 매개 변수는 삭제할 멤버가 포함된 프로그램을 지정합니다. 요청 본문에는 `input` 리드 id 배열. 호출당 최대 300개의 리드 ID가 허용됩니다.

끝점이 응답함 `status` / &quot;삭제됨&quot; 또는 &quot;건너뜀&quot;. 건너뛴 경우 `reasons` 배열도 포함됩니다. 끝점은 또한 `seq` 필드는 제출된 레코드를 응답 순서에 연결하는 데 사용할 수 있는 색인입니다.

```
POST /rest/v1/programs/{programId}/members/delete.json
```

```
Content-Type: application/json
```

```json
{
    "input":[
        {
            "leadId": 1235
        },
        {
            "leadId": 77
        }
    ]
}
```

```json
{
    "requestId": "302a#17916619417",
    "result": [
        {
            "seq": 0,
            "status": "deleted",
            "leadId": 1235
        },
        {
            "seq": 1,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1037",
                    "message": "Lead not in program"
                }
            ]
        }
    ],
    "success": true
}
```
