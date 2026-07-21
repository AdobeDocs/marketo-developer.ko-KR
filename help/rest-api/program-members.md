---
title: 프로그램 구성원
feature: REST API
description: Marketo REST API를 사용하여 프로그램 구성원을 읽고, 만들고, 업데이트하고, 삭제하고, 표준 및 사용자 정의 필드를 관리하고, 검색 가능한 필드를 사용하여 쿼리합니다.
exl-id: 22f29a42-2a30-4dce-a571-d7776374cf43
TQID: https://experienceleague.adobe.com/scEHyXYq9C7cCS1kIX810wG7ahT9fsa448NwIfBmzQM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1670
ht-degree: 2%

---

# 프로그램 구성원

[프로그램 멤버 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members)

Marketo은 프로그램 멤버 레코드를 읽고, 만들고, 업데이트하고, 삭제하기 위한 API를 제공합니다. 잠재 고객 ID 필드는 프로그램 구성원 레코드와 잠재 고객 레코드와 관련시킵니다.

각 레코드에는 표준 필드가 포함되어 있으며 최대 20개의 사용자 지정 필드를 포함할 수 있습니다. 이러한 필드에는 폼, 필터, 트리거 및 흐름 작업에서 사용할 프로그램별 멤버 데이터가 저장됩니다. Marketo Engage UI의 프로그램 [구성원 탭](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/manage-and-view-members)에서 이 데이터를 볼 수 있습니다.

## 설명

[프로그램 멤버 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) 끝점은 리드 데이터베이스 개체에 대한 표준 패턴을 따릅니다.

- `searchableFields` 배열은 쿼리에 유효한 필드를 식별합니다.
- `fields` 배열에 REST API 이름, 표시 이름 및 필드를 업데이트할 수 있는지 여부와 같은 메타데이터가 포함되어 있습니다.

```http
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

[프로그램 구성원 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMembersUsingGET) 끝점을 사용하여 프로그램 구성원을 검색합니다. 요청에는 `programId` 경로 매개 변수와 `filterType` 및 `filterValues` 쿼리 매개 변수가 필요합니다.

`programId`은(는) 검색할 프로그램을 지정합니다.

`filterType`은(는) 검색 필터로 사용할 필드를 지정합니다. [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) 끝점에서 반환된 &quot;searchableFields&quot; 목록의 모든 필드를 허용합니다. 사용자 지정 필드의 경우 dataType은 &quot;문자열&quot; 또는 &quot;정수&quot;여야 합니다.

filterType이 &quot;leadId&quot;가 아닌 경우 요청은 최대 100,000개의 프로그램 멤버 레코드를 처리할 수 있습니다. Marketo 인스턴스 구성에 따라 다음 오류 중 하나가 표시됩니다.

- 총 프로그램 구성원 수가 100,000명을 초과하는 경우 &quot;1003, 총 구성원 크기: 100,001이 필터에 허용되는 제한 100,000명을 초과합니다.&quot;라는 오류가 반환됩니다.
- 필터&#x200B;_과(와) 일치하는 총 프로그램 구성원 수_&#x200B;이(가) 100,000명을 초과하는 경우 &quot;1003, 일치하는 구성원 크기: 100,001이 이 API에 허용된 제한(100,000)을 초과합니다.&quot;라는 오류가 반환됩니다.

구성원 수가 한도를 초과하는 프로그램을 쿼리하려면 [일괄 프로그램 구성원 추출 API](bulk-program-member-extract.md)를 대신 사용하십시오.

`filterValues`은(는) 검색할 값을 지정하며 최대 300개의 쉼표로 구분된 값을 허용합니다. 호출은 프로그램 멤버 필드가 포함된 filterValues 중 하나와 일치하는 레코드를 검색합니다.

또는 `updatedAt`을(를) filterType으로 지정하고 `startAt` 및 `endAt` datetime 매개 변수를 제공하여 날짜 범위별로 필터링합니다. 범위는 7일 이하여야 합니다. datetime 값에 밀리초 없이 ISO-8601 형식을 사용하십시오.

선택적 `fields` 쿼리 매개 변수는 [Describe Program Member](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) 끝점에서 반환된 필드 API 이름의 쉼표로 구분된 목록을 허용합니다. 포함되는 경우 각 응답 레코드에는 지정된 필드가 포함됩니다. 생략하면 기본적으로 응답은 `acquiredBy`, `leadId`, `membershipDate`, `programId` 및 `reachedSuccess`을(를) 반환합니다.

기본적으로 끝점은 최대 300개의 레코드를 반환합니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

**moreResult** 특성이 true인 경우 더 많은 결과를 사용할 수 있습니다. moreResult가 false가 될 때까지 반환된 `nextPageToken`을(를) 사용하여 끝점을 계속 호출합니다.

GET 요청의 총 길이가 8KB를 초과하는 경우 끝점은 HTTP 오류 &quot;414, URI가 너무 깁니다&quot;를 반환합니다. 이 제한을 해결하려면 요청을 GET에서 POST로 변경하고 `_method=GET` 매개 변수를 추가한 다음 쿼리 문자열을 요청 본문에 배치합니다.

```http
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

두 끝점은 프로그램 멤버에 대한 만들기 및 업데이트 작업을 지원합니다.

- 한 끝점은 프로그램 멤버 상태만 업데이트합니다.
- 한 끝점이 &quot;업데이트 가능&quot;으로 표시된 프로그램 멤버 필드를 업데이트합니다.

각 끝점은 호출당 최대 300개의 프로그램 멤버 레코드를 수정할 수 있습니다.

### 프로그램 구성원 상태

[동기화 프로그램 구성원 상태](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/syncProgramMemberStatusUsingPOST) 끝점을 사용하여 하나 이상의 구성원에 대한 프로그램 상태를 만들거나 업데이트합니다.

필수 매개 변수는 다음과 같습니다.

- `programId`: 만들거나 업데이트할 멤버가 포함된 프로그램을 지정하는 경로 매개 변수입니다.
- `statusName`: 잠재 고객 목록에 적용할 프로그램 상태를 지정합니다. statusName은(는) 프로그램 채널에 사용 가능한 상태와 일치해야 합니다. [채널 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Channels/operation/getAllChannelsUsingGET) 끝점으로 올바른 상태를 검색합니다. 잠재 고객의 상태가 지정된 statusName보다 큰 단계 값을 가지면 요청에서 해당 잠재 고객을 건너뜁니다.
- `input`: 프로그램 멤버에 해당하는 `leadId` 값의 배열입니다. 호출당 최대 300개의 leadId를 제출할 수 있습니다.

끝점은 각 레코드에 대한 업데이트를 수행합니다. leadId가 프로그램 구성원과 연결된 경우 끝점이 멤버십 상태를 업데이트합니다. 그렇지 않으면 프로그램 멤버 레코드를 만들고 레코드를 leadId와 연결하며 멤버십 상태를 할당합니다.

응답에 `status`의 &quot;업데이트됨&quot;, &quot;생성됨&quot; 또는 &quot;건너뜀&quot;이 포함되어 있습니다. 건너뛴 결과에는 `reasons` 배열도 포함됩니다. `seq` 필드는 제출된 각 레코드와 응답 순서를 연결하는 색인입니다.

호출이 성공하면 &quot;프로그램 상태 변경&quot; 활동이 잠재 고객의 활동 로그에 기록됩니다.

```http
POST /rest/v1/programs/{programId}/members/status.json
```

```text
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

[프로그램 구성원 데이터 동기화](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/syncProgramMemberDataUsingPOST) 끝점을 사용하여 하나 이상의 구성원에 대한 프로그램 구성원 필드 데이터를 업데이트합니다. [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2) 끝점에서 &quot;업데이트 가능&quot;으로 표시된 사용자 지정 필드 또는 표준 필드를 수정할 수 있습니다.

필수 매개 변수는 다음과 같습니다.

- `programId`: 업데이트할 멤버가 포함된 프로그램을 지정하는 경로 매개 변수입니다.
- `input`: 요소에 `leadId`과(와) API 이름으로 업데이트할 하나 이상의 필드가 포함된 배열입니다. 호출당 최대 300개의 leadId를 제출할 수 있습니다.

끝점은 각 레코드를 업데이트합니다. leadId는 프로그램 구성원과 연결되어 있어야 하며 각 필드는 업데이트할 수 있어야 합니다.

응답에 `status`의 &quot;업데이트됨&quot; 또는 &quot;건너뜀&quot;이 포함되어 있습니다. 건너뛴 결과에는 `reasons` 배열도 포함됩니다. `seq` 필드는 제출된 각 레코드와 응답 순서를 연결하는 색인입니다.

호출이 성공하면 &quot;프로그램 구성원 데이터 변경&quot; 활동이 잠재 고객의 활동 로그에 기록됩니다.

```http
POST /rest/v1/programs/{programId}/members.json
```

```text
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

프로그램 멤버 개체에는 표준 필드와 선택적 사용자 지정 필드가 포함되어 있습니다. 표준 필드는 모든 Marketo Engage 구독에 표시되지만 사용자는 필요에 따라 사용자 정의 필드를 만듭니다.

각 필드는 표시 이름, API 이름 및 dataType과 같은 특성으로 정의됩니다. 이러한 특성을 함께 메타데이터라고 합니다.

다음 엔드포인트는 프로그램 멤버 개체의 필드를 쿼리하고 만들고 업데이트합니다. API 사용자는 **읽기-쓰기 스키마 표준 필드** 권한, **읽기-쓰기 스키마 사용자 지정 필드** 권한 또는 둘 다 있는 역할이 있어야 합니다.

### 쿼리 필드

API 이름으로 하나의 프로그램 멤버 필드를 쿼리하거나 모든 프로그램 멤버 필드를 검색합니다. 역할 권한은 응답에 표준 필드, 사용자 정의 필드 또는 둘 다를 포함할 수 있는지 여부를 결정합니다. 응답에는 숨겨진 필드도 포함됩니다.

#### 이름별

[이름별 프로그램 멤버 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMemberFieldByNameUsingGET) 끝점은 프로그램 멤버 개체에서 한 필드의 메타데이터를 검색합니다. 필수 `fieldApiName` 경로 매개 변수는 필드의 API 이름을 지정합니다.

응답은 Describe Program Member 응답과 유사하지만 추가 메타데이터를 포함합니다. 예를 들어 `isCustom` 특성은 필드가 사용자 지정인지 여부를 나타냅니다.

```http
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

[프로그램 구성원 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/getProgramMemberFieldsUsingGET) 끝점은 프로그램 구성원 개체의 모든 필드에 대한 메타데이터를 검색합니다. 기본적으로 최대 300개의 레코드를 반환합니다. `batchSize` 쿼리 매개 변수를 사용하여 이 숫자를 줄이십시오.

`moreResult` 특성이 true이면 더 많은 결과를 사용할 수 있습니다. moreResult가 false가 될 때까지 반환된 `nextPageToken`을(를) 사용하여 끝점을 계속 호출합니다.

```http
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

[프로그램 구성원 필드 만들기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/createProgramMemberFieldUsingPOST) 끝점은 프로그램 구성원 개체에 사용자 지정 필드를 만듭니다. [Marketo Engage UI](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/program-member-custom-fields)와 비슷한 기능을 제공합니다. 이 끝점으로 최대 20개의 사용자 지정 필드를 만들 수 있습니다.

프로덕션 Marketo Engage 인스턴스에서 생성하기 전에 각 필드를 신중하게 고려합니다. 필드를 만든 후에는 삭제할 수 없습니다. [숨길 수만 있습니다](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/field-management/delete-a-custom-field-in-marketo). 사용하지 않는 필드는 인스턴스에 혼란을 추가합니다.

필수 `input` 매개 변수는 프로그램 멤버 필드 개체의 배열입니다. 각 객체에는 하나 이상의 속성이 포함됩니다.

- 필수 특성은 `displayName`, `name` 및 `dataType`입니다. 각각 UI 표시 이름, API 이름 및 필드 유형에 해당합니다.
- 선택적 특성은 `description`, `isHidden`, `isHtmlEncodingInEmail` 및 `isSensitive`입니다.

`name` 및 `displayName` 특성에는 다음 명명 규칙이 있습니다.

- `name` 특성은 고유해야 하며 문자로 시작하고 문자, 숫자 또는 밑줄만 포함해야 합니다.
- *`isplayName`은(는) 고유해야 하며 특수 문자를 포함할 수 없습니다.

일반적인 규칙은 `displayName`에 [낙타 사례](https://en.wikipedia.org/wiki/Camel_case#)을(를) 적용하여 `name`을(를) 만드는 것입니다. 예를 들어 `displayName`의 &quot;내 사용자 지정 필드&quot;는 `name`의 &quot;myCustomField&quot;를 생성합니다.

```http
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

[프로그램 구성원 필드 업데이트](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/updateProgramMemberFieldUsingPOST) 끝점은 프로그램 구성원 개체에서 하나의 사용자 지정 필드를 업데이트합니다. Marketo Engage UI에서 사용할 수 있는 대부분의 필드 업데이트는 API를 통해서도 사용할 수 있습니다. 다음 표에는 차이점이 요약되어 있습니다.

| 속성 | API로 업데이트할 수 있습니까? | UI로 업데이트할 수 있습니까? | API로 업데이트할 수 있습니까? | UI로 업데이트할 수 있습니까? |
| --- | --- | --- | --- | --- |
| dataType | 아니요 | 아니요 | 아니요 | 예 |
| 설명 | 예 | 예 | 예 | 예 |
| displayName | 아니요 | 아니요 | 예 | 예 |
| isCustom | 아니요 | 아니요 | 아니요 | 아니요 |
| isHidden | 아니요 | 예 | 예(API로 생성된 경우) | 예 |
| isHtmlEncodingInEmail | 예 | 예 | 예 | 예 |
| 중요 | 예 | 예 | 예 | 예 |
| length | 아니요 | 아니요 | 아니요 | 아니요 |
| 이름 | 아니요 | 아니요 | 아니요 | 아니요 |

요청에는 다음 매개 변수가 필요합니다.

- `fieldApiName`: 업데이트할 필드의 API 이름을 지정하는 경로 매개 변수입니다.
- `input`: 하나 이상의 특성이 있는 리드 필드 개체가 포함된 배열입니다.

```http
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

[프로그램 구성원 삭제](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/deleteProgramMemberUsingPOST) 끝점을 사용하여 프로그램 구성원 레코드를 삭제합니다. 필수 `programId` 경로 매개 변수는 삭제할 멤버가 포함된 프로그램을 지정합니다.

요청 본문에 `input` 리드 ID 배열이 포함되어 있습니다. 각 호출에는 최대 300개의 리드 ID가 허용됩니다.

응답에 `status`의 &quot;삭제됨&quot; 또는 &quot;건너뜀&quot;이 포함되어 있습니다. 건너뛴 결과에는 `reasons` 배열도 포함됩니다. `seq` 필드는 제출된 각 레코드와 응답 순서를 연결하는 색인입니다.

```http
POST /rest/v1/programs/{programId}/members/delete.json
```

```text
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
