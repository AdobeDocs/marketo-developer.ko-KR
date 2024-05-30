---
title: "일괄 프로그램 멤버 추출"
feature: REST API
description: "멤버 데이터 추출의 일괄 처리"
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 2%

---


# 일괄 프로그램 멤버 추출

[벌크 프로그램 멤버 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members)

REST API의 벌크 프로그램 멤버 추출 세트는 Marketo에서 큰 프로그램 멤버 레코드 세트를 검색할 수 있는 프로그래밍 인터페이스를 제공합니다. ETL, 데이터 웨어하우징 및 보관 목적으로 Marketo과 하나 이상의 외부 시스템 간에 데이터를 지속적으로 교환해야 하는 사용 사례에 권장되는 인터페이스입니다.

## 권한

벌크 프로그램 멤버 추출 API를 사용하려면 소유 API 사용자에게 읽기 전용 리드 또는 읽기-쓰기 리드 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

## 설명

[프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Program-Members/operation/describeProgramMemberUsingGET2) 는 필드를 사용할 수 있는지 여부와 해당 필드에 대한 메타데이터에 대한 기본 소스로 사용됩니다. 다음 `name` 속성에는 REST API 이름이 포함됩니다.

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

## 필터

프로그램 멤버는 다양한 필터 옵션을 지원합니다. 작업에 대해 여러 필터 유형을 지정할 수 있으며, 이 경우 필터 유형은 함께 AND됩니다. 다음 중 하나를 지정해야 합니다 `programId` 또는 `programIds` 필터. 다른 모든 필터는 선택 사항입니다. 다음 `updatedAt` 필터를 사용하려면 모든 구독에 아직 롤아웃되지 않은 추가 인프라 구성 요소가 필요합니다.

<table>
  <tbody>
    <tr>
      <td>필터 유형</td>
      <td>데이터 유형</td>
      <td>참고 사항</td>
    </tr>
    <tr>
      <td>programId</td>
      <td>정수</td>
      <td>프로그램 ID를 허용합니다. 작업은 작업이 처리를 시작할 때 프로그램의 구성원인 액세스 가능한 모든 레코드를 반환합니다 <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs">프로그램 가져오기</a> endpoint.를 programIds 필터와 함께 사용할 수 없습니다.</td>
    </tr>
    <tr>
      <td>programIds</td>
      <td>배열[정수]</td>
      <td>최대 10개의 프로그램 ID 배열을 허용합니다. 작업은 작업이 처리를 시작할 때 프로그램의 구성원인 액세스 가능한 모든 레코드를 반환합니다. 내보내기 파일에 첫 번째 필드로 "programId" 필드가 추가됩니다. 이 필드는 프로그램 멤버십 레코드가에서 추출된 프로그램을 식별합니다.다음을 사용하여 프로그램 ID 검색 <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs">프로그램 가져오기</a> endpoint.를 programId 필터와 함께 사용할 수 없습니다.</td>
    </tr>
    <tr>
      <td>isExhausted</td>
      <td>부울</td>
      <td>다음에 대한 프로그램 멤버십 레코드를 필터링하는 데 사용되는 부울을 허용합니다. <a href="https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content">콘텐츠가 소진된 사람</a>.</td>
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
              <td>반송됨</td>
            </tr>
            <tr>
              <td>클릭됨</td>
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
              <td>보냄</td>
              <td>구독 등록됨</td>
              <td>주소 삭제</td>
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

일부 구독에서는 필터 유형을 사용할 수 없습니다. 구독에 사용할 수 없는 경우 내보내기 프로그램 구성원 작업 만들기 끝점을 호출할 때 오류가 발생합니다(&quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot;). 고객은 Marketo 지원 센터에 문의하여 구독에서 이 기능을 활성화할 수 있습니다.

## 옵션

내보내기 프로그램 구성원 작업 만들기 끝점은 몇 가지 서식 옵션을 제공합니다. 이러한 옵션을 통해 사용자는 다음과 같은 작업을 수행할 수 있습니다.

- 내보낸 파일에 포함할 필드 지정
- 이 필드의 열 헤더 이름 바꾸기
- 내보낸 파일의 형식 지정

| 매개 변수 | 데이터 유형 | 필수 | 참고 사항 |
|---|---|---|---|
| 필드 | 배열[문자열] | 예 | 필드 매개 변수는 JSON 문자열 배열을 수락합니다. 나열된 필드는 내보낸 파일에 포함됩니다. 다음과 같은 필드 유형을 내보낼 수 있습니다.`LeadCustom` `LeadProgram` MemberCustom `ProgramMember`. 리드2 설명 및/또는 프로그램 멤버 엔드포인트 설명을 사용하여 검색할 수 있는 REST API 이름을 사용하여 필드를 지정합니다. |
| 열 머리글 이름 | 오브젝트 | 아니요 | 필드 및 열 헤더 이름의 키-값 쌍을 포함하는 JSON 개체입니다. 키는 내보내기 작업에 포함된 필드 이름이어야 합니다. 값은 해당 필드에 대해 내보낸 열 헤더의 이름입니다. |
| 형식 | 문자열 | 아니요 | CSV, TSV, SSV 중 하나를 허용합니다. 내보낸 파일은 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값 파일로 렌더링됩니다(설정된 경우). 설정하지 않으면 기본값이 CSV로 설정됩니다. |


## 작업 생성

작업에 대한 매개 변수는 를 사용하여 내보내기를 시작하기 전에 정의합니다. [내보내기 프로그램 구성원 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/createExportProgramMembersUsingPOST) 엔드포인트. 다음을 정의해야 합니다. `filter` 프로그램 id 및 `fields` 내보내기에 필요합니다. 필요한 경우 다음을 정의할 수 있습니다. `format` 및 `columnHeaderNames`.

```
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

작업이 생성되었음을 나타내는 상태 응답이 반환됩니다. 작업이 정의되고 생성되었지만 아직 시작되지 않았습니다. 이렇게 하려면 [프로그램 구성원 작업 큐 내보내기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/enqueueExportProgramMembersUsingPOST) 끝점은 다음을 사용하여 호출해야 합니다. `exportId` 생성 상태 응답에서:

```
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

이 경우 이니셜로 응답합니다. `status` 사용 가능한 내보내기 슬롯이 있는 경우 &quot;대기 중&quot; 이후 &quot;처리 중&quot;으로 설정됩니다.

## 폴링 작업 상태

참고: 동일한 API 사용자가 만든 작업에 대해서만 상태를 검색할 수 있습니다.

비동기 끝점이므로 작업을 만든 후 상태를 폴링하여 진행률을 확인해야 합니다. 을(를) 사용하여 투표 [내보내기 프로그램 멤버 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) 엔드포인트. 상태는 60초마다 한 번만 업데이트되므로 이보다 낮은 폴링 빈도는 권장되지 않으며 거의 모든 경우에 여전히 과도합니다. 상태 필드는 생성됨, 대기 중, 처리 중, 취소됨, 완료됨, 실패 중 하나로 응답할 수 있습니다.

```
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

상태 끝점은 작업이 아직 처리 중이므로 파일을 검색할 수 없다는 것을 나타냅니다. 작업 한 번 `status` &quot;완료됨&quot;에 대한 변경 사항을 다운로드할 수 있습니다.

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

완료된 프로그램 멤버 내보내기의 파일을 검색하려면 [내보내기 프로그램 멤버 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/getExportProgramMembersFileUsingGET) 엔드포인트 `exportId`.

응답에는 작업이 구성된 방식으로 포맷된 파일이 포함됩니다. 끝점이 파일의 내용에 응답합니다. 요청한 프로그램 멤버 필드가 비어 있으면(데이터 없음) `null` 는 내보내기 파일의 해당 필드에 배치됩니다.

```
GET /bulk/v1/program/members/export/{exportId}/file.json
```

```
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

추출된 데이터의 부분 검색 및 재시작 친화성을 지원하기 위해 파일 엔드포인트는 선택적으로 바이트 유형의 HTTP 헤더 범위를 지원합니다. 헤더가 설정되지 않은 경우 전체 콘텐츠가 반환됩니다. Marketo에서 범위 헤더 사용에 대한 자세한 내용을 볼 수 있습니다 [일괄 추출](bulk-extract.md).

## 작업 취소

작업이 잘못 구성되었거나 필요하지 않은 경우 를 사용하여 쉽게 취소할 수 있습니다. [프로그램 구성원 내보내기 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Program-Members/operation/cancelExportProgramMembersUsingPOST) 끝점:

```
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

다음으로 응답함: `status` 작업이 취소되었음을 나타냅니다.
