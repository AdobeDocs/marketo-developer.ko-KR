---
title: 일괄 프로그램 멤버 추출
feature: REST API
description: Marketo 일괄 프로그램 멤버 추출 REST API를 사용하여 권한 및 필드 메타데이터와 함께 ETL, 데이터 웨어하우징 및 아카이브에 대한 대규모 멤버 레코드를 내보낼 수 있습니다.
exl-id: 6e0a6bab-2807-429d-9c91-245076a34680
TQID: https://experienceleague.adobe.com/w4qaVTKSe0EORaSiURB6WbJXi29JUdEgfkb2dnfuVFw
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1026
ht-degree: 2%

---

# 일괄 프로그램 멤버 추출

[벌크 프로그램 멤버 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members)

벌크 프로그램 멤버 추출 REST API는 Marketo에서 큰 프로그램 멤버 레코드 집합을 검색합니다. Marketo과 외부 시스템, ETL, 데이터 웨어하우징 및 아카이빙 간의 지속적인 데이터 교환을 위해 이러한 API를 사용합니다.

## 권한

API 사용자는 읽기 전용 리드 권한, 읽기-쓰기 리드 권한 또는 둘 다 있는 역할이 있어야 합니다.

## 설명

[프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Program-Members/operation/describeProgramMemberUsingGET2)을(를) 사용하여 사용 가능한 필드를 확인하고 해당 메타데이터를 검색하십시오. `name` 특성에 REST API 필드 이름이 포함되어 있습니다.

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

## 필터

프로그램 멤버 내보내기는 여러 필터 옵션을 지원합니다. 작업에서 여러 필터 유형을 지정하는 경우 API는 이러한 유형을 AND 작업과 결합합니다.

모든 작업은 `programId` 또는 `programIds`을(를) 지정해야 합니다. 다른 모든 필터는 선택 사항입니다. `updatedAt` 필터에 일부 구독에서는 사용할 수 없는 인프라가 필요합니다.

<table>
  <tbody>
    <tr>
      <td>필터 유형</td>
      <td>데이터 유형</td>
      <td>참고</td>
    </tr>
    <tr>
      <td>programId</td>
      <td>정수</td>
      <td>프로그램 ID를 허용합니다. 작업은 작업 처리를 시작할 때 프로그램의 구성원인 액세스 가능한 모든 레코드를 반환합니다.<a href="https://developer.adobe.com/marketo-apis/api/asset#tag/Programs">프로그램 가져오기</a> 끝점을 사용하여 프로그램 ID를 검색합니다.programIds 필터와 함께 사용할 수 없습니다.</td>
    </tr>
    <tr>
      <td>programIds</td>
      <td>배열[정수]</td>
      <td>최대 10개의 프로그램 ID 배열을 허용합니다. 작업은 작업 처리를 시작할 때 프로그램의 구성원인 액세스 가능한 모든 레코드를 반환합니다.내보내기 파일에 첫 번째 필드로 추가 필드 "programId"가 추가됩니다. 이 필드는 프로그램 멤버십 레코드를 추출한 프로그램을 식별합니다.<a href="https://developer.adobe.com/marketo-apis/api/asset#tag/Programs">프로그램 가져오기</a> 끝점을 사용하여 프로그램 ID를 검색합니다.programId 필터에는 사용할 수 없습니다.</td>
    </tr>
    <tr>
      <td>isExhausted</td>
      <td>부울</td>
      <td><a href="https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content">콘텐츠를 모두 사용한 사용자</a>의 프로그램 멤버십 레코드를 필터링하는 데 사용되는 부울을 허용합니다.</td>
    </tr>
    <tr>
      <td>양육케이던스</td>
      <td>문자열</td>
      <td>지정된 육성 케이던스에 대한 프로그램 멤버십 레코드를 필터링하는 데 사용되는 문자열을 허용합니다. 허용되는 값은 다음과 같습니다.
        <ul>
          <li>일시 중지 - 케이던스가 일시 중지됨</li>
          <li>표준 - 케이던스가 정상임</li>
        </ul></td>
    </tr>
    <tr>
      <td>상태 이름</td>
      <td>Array[String]</td>
      <td>프로그램 멤버 상태 이름의 배열을 허용합니다. 여러 상태 이름이 함께 OR됩니다.이 필터 유형의 작업은 프로그램 멤버 상태가 지정된 상태 이름과 일치하는 액세스 가능한 모든 레코드를 반환합니다. 기본 및 사용자 정의 상태 이름을 모두 사용할 수 있습니다. statusNames 필터를 'programIds' 필터와 함께 사용하면 각 프로그램에서 상태 이름과 일치하는 멤버십 레코드를 확인합니다. 프로그램에서 상태 이름을 찾을 수 없으면 "1003, Invalid Data" 오류가 반환됩니다.
        <table>
          <tbody>
            <tr>
              <td>출석함</td>
              <td>온디맨드 출석</td>
              <td>바운스됨</td>
            </tr>
            <tr>
              <td>클릭함</td>
              <td>연락함</td>
              <td>전환됨</td>
            </tr>
            <tr>
              <td>참여</td>
              <td>작성된 양식</td>
              <td>영향을 받음</td>
            </tr>
            <tr>
              <td>초대됨</td>
              <td>멤버</td>
              <td>표시 안 함</td>
            </tr>
            <tr>
              <td>프로그램에 없음</td>
              <td>목록에서</td>
              <td>열림</td>
            </tr>
            <tr>
              <td>등록됨</td>
              <td>등록 중</td>
              <td>등록 오류</td>
            </tr>
            <tr>
              <td>전송됨</td>
              <td>구독 등록됨</td>
              <td>구독 취소</td>
            </tr>
            <tr>
              <td>조회함</td>
              <td>방문함</td>
              <td>방문 부스</td>
            </tr>
            <tr>
              <td>대기자 명단 등록됨</td>
              <td>웹 컨텐츠</td>
              <td></td>
            </tr>
          </tbody>
        </table></td>
    </tr>
    <tr>
      <td>updatedAt*</td>
      <td>날짜 범위</td>
      <td>startAt 및 endAt 멤버가 있는 JSON 개체를 수락합니다. startAt 는 로우 워터마크를 나타내는 날짜/시간을 수락하고 endAt 는 하이 워터마크를 나타내는 날짜/시간을 수락합니다. 범위는 31일 이하여야 합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다.이 필터 유형의 작업은 날짜 범위 내에서 가장 최근에 업데이트된 액세스 가능한 모든 레코드를 반환합니다.</td>
    </tr>
  </tbody>
</table>

일부 구독은 이 필터 유형을 지원하지 않습니다. 사용할 수 없는 경우 내보내기 프로그램 구성원 작업 만들기 끝점이 `1035, Unsupported filter type for target subscription`을(를) 반환합니다. 구독에 대해 이 기능을 요청하려면 Marketo 지원 센터에 문의하십시오.

## 옵션

내보내기 프로그램 멤버 작업 만들기 엔드포인트는 다음을 위한 옵션을 제공합니다.

- 내보내기 파일에 포함할 필드를 지정합니다.
- 내보낸 열 헤더의 이름을 변경합니다.
- 내보내기 파일 형식을 지정합니다.

| 매개변수 | 데이터 유형 | 필수 | 참고 |
| --- | --- | --- | --- |
| 필드 | 배열[문자열] | 예 | 필드 매개 변수는 JSON 문자열 배열을 수락합니다. 나열된 필드는 내보낸 파일에 포함됩니다. `LeadCustom` `LeadProgram` MemberCustom `ProgramMember` 필드 형식을 내보낼 수 있습니다. 리드2 설명 및/또는 프로그램 멤버 엔드포인트 설명을 사용하여 검색할 수 있는 REST API 이름으로 필드를 지정합니다. |
| 열 머리글 이름 | 오브젝트 | 아니요 | 필드 및 열 헤더 이름의 키-값 쌍을 포함하는 JSON 개체입니다. 키는 내보내기 작업에 포함된 필드 이름이어야 합니다. 값은 해당 필드에 대해 내보낸 열 헤더의 이름입니다. |
| 형식 | 문자열 | 아니요 | CSV, TSV, SSV 중 하나를 허용합니다. 내보낸 파일은 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값 파일로 렌더링됩니다(설정된 경우). 설정하지 않으면 기본값이 CSV로 설정됩니다. |

## 작업 생성

[내보내기 프로그램 구성원 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/createExportProgramMembersUsingPOST) 끝점을 사용하여 내보내기 작업을 정의합니다. 내보낼 프로그램 ID와 `fields`이(가) 포함된 `filter`을(를) 지정하십시오. `format` 및 `columnHeaderNames`을(를) 지정할 수도 있습니다.

```http
POST /bulk/v1/program/members/export/create.json
```

```json
{
   "format": "CSV",
   "fields": [
        "firstName",
        "lastName",
        "email",
        "membershipDate",
        "program",
        "statusName",
        "leadId",
        "reachedSuccess",
        "leadCustomField01",
        "leadCustomField02",
        "pMCustomField01",
        "pMCustomField02"
   ],
   "filter": {
      "programId":1044
   }
}
```

```json
{
    "requestId": "4d44#16f92734f6e",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Created",
            "createdAt": "2020-01-11T02:33:48Z"
        }
    ],
    "success": true
}
```

응답은 작업이 생성되었음을 확인하지만 내보내기가 자동으로 시작되지 않습니다. 반환된 `exportId`을(를) [Enqueue 내보내기 프로그램 구성원 작업](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/enqueueExportProgramMembersUsingPOST) 끝점에 전달하여 작업을 시작합니다.

```http
POST /bulk/v1/program/members/export/{exportId}/enqueue.json
```

```json
{
    "requestId": "d70b#16f9273ae32",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z"
        }
    ],
    "success": true
}
```

대기열에 넣기 응답이 처음에 `Queued` 상태를 반환합니다. 내보내기 슬롯을 사용할 수 있게 되면 상태가 `Processing`(으)로 변경됩니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 상태를 검색할 수 있습니다.

내보내기가 비동기적으로 실행되므로 [내보내기 프로그램 구성원 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) 끝점을 사용하여 진행 상황을 폴링하십시오. 상태는 60초마다 한 번만 업데이트되므로 더 자주 폴링하지 않습니다.

상태는 `Created`, `Queued`, `Processing`, `Canceled`, `Completed` 또는 `Failed`일 수 있습니다.

```http
GET /bulk/v1/program/members/export/{exportId}/status.json
```

```json
{
    "requestId": "9a40#16f9274d250",
    "result": [
        {
            "exportId": "b5ca52a9-5ecb-4966-b5a9-11659a8b4c2b",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z",
            "startedAt": "2020-01-11T02:35:19Z"
        }
    ],
    "success": true
}
```

이 응답은 작업이 아직 처리 중이므로 파일을 사용할 수 없음을 보여줍니다. 작업 상태가 `Completed`(으)로 변경되면 파일을 다운로드할 준비가 되었습니다.

```json
{
    "requestId": "11ad1#16f9ff6da23",
    "result": [
        {
            "exportId": "1118dc83-273b-4d44-becb-4d212fece550",
            "format": "CSV",
            "status": "Completed",
            "createdAt": "2020-01-11T02:33:48Z",
            "queuedAt": "2020-01-11T02:34:13Z",
            "startedAt": "2020-01-11T02:35:19Z"
            "finishedAt": "2020-01-11T02:36:12Z",
            "numberOfRecords": 13,
            "fileSize": 1752,
            "fileChecksum": "sha256:b3c8e70e6e501cf1025e345a66b409d4fd07364c7da773cfa68a2b68ce1a7212"
        }
    ],
    "success": true
}
```

## 데이터 검색 중

완료된 프로그램 구성원 내보내기를 검색하려면 `exportId`을(를) [내보내기 프로그램 구성원 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/getExportProgramMembersFileUsingGET) 끝점에 전달하십시오.

끝점이 작업에 대해 구성된 형식으로 파일을 반환합니다. 요청한 프로그램 멤버 필드에 데이터가 없으면 해당 내보내기 필드에 `null`이(가) 포함됩니다.

```http
GET /bulk/v1/program/members/export/{exportId}/file.json
```

```text
firstName,lastName,email,Member Date,Program,Status,Lead Id,Success,leadCustomField01,leadCustomField02,pMCustomField01,pMCustomField02
Meera,Reed,mree@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1789,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jon,Umber,jumb@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1790,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Lyanna,Mormont,lmor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1791,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rickon,Stark,rsta@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1792,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Hodor,null,hodor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1793,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Osha,null,osha@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1794,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jojen,Reed,Jree@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1795,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rickard,Karstark,rkar@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1796,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Maester,Luwin,mluw@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1797,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Rodrik,Cassel,rcas@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1798,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Jory,Cassel,jcas@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1799,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
Septa,Mordane,smor@housestark.com,2020-01-08T18:10:26Z,PMCF Program,On List,1800,false,Lead01_Value,Lead02_Value,PM01_Value,PM02_Value
```

부분 검색 또는 다시 시작 가능한 검색의 경우 파일 끝점은 범위 유형이 `bytes`인 선택적 HTTP `Range` 헤더를 지원합니다. 헤더를 설정하지 않으면 끝점이 전체 파일을 반환합니다. 자세한 내용은 [일괄 추출](bulk-extract.md)을 참조하세요.

## 작업 취소

잘못 구성되었거나 더 이상 필요하지 않은 작업을 취소하려면 [프로그램 구성원 내보내기 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Program-Members/operation/cancelExportProgramMembersUsingPOST) 끝점을 호출하십시오.

```http
POST /bulk/v1/program/members/export/{exportId}/cancel.json
```

```json
{
    "requestId": "bb4f#16f86727f89",
    "result": [
        {
            "exportId": "f0d3520c-3a60-4568-9e71-2e619d3805a4",
            "format": "CSV",
            "status": "Cancelled",
            "createdAt": "2020-01-07T21:47:35Z"
        }
    ],
    "success": true
}
```

응답 상태는 작업이 취소되었음을 나타냅니다.
