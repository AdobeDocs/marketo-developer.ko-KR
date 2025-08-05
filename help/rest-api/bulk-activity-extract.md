---
title: 일괄 활동 추출
feature: REST API
description: Marketo에서 활동 데이터를 일괄 처리합니다.
exl-id: 6bdfa78e-bc5b-4eea-bcb0-e26e36cf6e19
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 3%

---

# 일괄 활동 추출

[일괄 활동 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/)

REST API의 벌크 활동 추출 세트는 Marketo에서 대량의 활동 데이터를 검색하기 위한 프로그래밍 방식 인터페이스를 제공합니다.  짧은 지연 시간이 필요하지 않고 CRM 통합, ETL, 데이터 웨어하우징 및 데이터 보관과 같은 많은 양의 작업 데이터를 Marketo 외부로 전송해야 하는 경우.

## 권한

벌크 활동 추출 API를 사용하려면 API 사용자에게 &quot;읽기 전용 활동&quot; 또는 &quot;읽기-쓰기 활동&quot; 권한이 있어야 합니다.

## 필터

| 필터 유형 | 데이터 유형 | 필수 | 참고 |
| --- | --- | --- | --- |
| createdAt | 날짜 범위 | 예 | `startAt` 및 `endAt` 멤버를 사용하여 JSON 개체를 허용합니다. `startAt`은(는) 로우 워터마크를 나타내는 날짜/시간을 수락하고 `endAt`은(는) 하이 워터마크를 나타내는 날짜/시간을 수락합니다. 범위는 31일 이하여야 합니다. 이 필터 유형의 작업은 날짜 범위 내에서 만든 액세스 가능한 모든 레코드를 반환합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다. |
| activityTypeIds | Array\[Integer\] | 아니요 | 하나의 멤버 `activityTypeIds`이(가) 있는 JSON 개체를 허용합니다. 값은 원하는 활동 유형에 해당하는 정수 배열이어야 합니다. &quot;리드 삭제&quot; 활동은 지원되지 않습니다(대신 [삭제된 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET) 엔드포인트를 사용). [활동 유형 가져오기 엔드포인트](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getAllActivityTypesUsingGET)를 사용하여 활동 유형 ID를 검색합니다. |
| [primaryAttributeValueIds](#primaryattributevalueids-options) | Array\[Integer\] | 아니요 | 하나의 멤버 `primaryAttributeValueIds`이(가) 있는 JSON 개체를 허용합니다. 값은 필터링할 기본 속성을 지정하는 ID 배열입니다. 최대 50개의 ID를 지정할 수 있습니다. ID는 잠재 고객 필드 또는 에셋에 대한 고유 식별자이며 적절한 REST API 끝점을 호출하여 검색할 수 있습니다. 예를 들어 &quot;양식 채우기&quot; 활동에 대한 특정 양식을 필터링하려면 양식 이름을 [이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) 엔드포인트에 전달하여 양식 ID를 검색합니다. 다음은 기본 속성 필터링이 지원되는 활동 유형 목록입니다. |
| [primaryAttributeValue](#primaryattributevalues-options) | Array\[String\] | 아니요 | 하나의 멤버 `primaryAttributeValues`이(가) 있는 JSON 개체를 허용합니다. 값은 필터링할 기본 속성을 지정하는 이름 배열입니다. 최대 50개의 이름을 지정할 수 있습니다. 이름은 리드 필드 또는 에셋의 고유 식별자이며 적절한 REST API 끝점을 호출하여 검색할 수 있습니다. 예를 들어 &quot;양식 채우기&quot; 활동에 대한 특정 양식을 필터링하려면 양식 ID를 [ID별로 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 엔드포인트에 전달하여 양식 이름을 검색합니다. 다음은 기본 속성 필터링이 지원되는 활동 유형 목록입니다. |

### primaryAttributeValueIds 옵션 {#primaryattributevalueids-options}

| 활동 유형 | 기본 속성 값 Id | 검색 끝점 | 자산 그룹 |
| --- | --- | --- | --- |
| 데이터 값 변경 | 리드 필드 ID | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 점수 변경 | 리드 필드 ID | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 진행 상태 변경 | 프로그램 ID | [이름별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET) | 마케팅 프로그램 |
| 목록에 추가 | 정적 목록 ID | [이름별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 정적 목록 |
| 목록에서 제거 | 정적 목록 ID | [이름별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 정적 목록 |
| 양식 작성 | 양식 ID | [이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) | 웹 양식 |

`primaryAttributeValueIds`을(를) 사용하는 경우 `activityTypeIds` 필터가 있어야 하며 해당 자산 그룹과 일치하는 활동 ID만 포함해야 합니다. 예를 들어 웹 양식 자산을 필터링하는 경우 `activityTypeIds`에서 &quot;양식 작성&quot; 활동 유형 ID만 허용됩니다.

예제 요청 본문:

```json
{
  "filter": {
    "createdAt": {
      "startAt": "2021-07-01T23:59:59-00:00",
      "endAt": "2021-07-02T23:59:59-00:00"
    },
    "activityTypeIds": [
      2
    ],
    "primaryAttributeValueIds": [
      16,102,95,8
    ]
  }
}
```

`primaryAttributeValueIds`과(와) `primaryAttributeValues`은(는) 함께 사용할 수 없습니다.

### primaryAttributeValues 옵션 {#primaryattributevalues-options}

| 활동 유형 | 기본 속성 값 | 검색 끝점 | 자산 그룹 |
| --- | --- | --- | --- |
| 데이터 값 변경 | 리드 필드 displayName | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 점수 변경 | 리드 필드 displayName | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 진행 상태 변경 | 프로그램 이름 | [Id로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET) | 마케팅 프로그램 |
| 목록에 추가 | 정적 목록 이름 | [Id별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 정적 목록 |
| 목록에서 제거 | 정적 목록 이름 | [Id별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 정적 목록 |
| 양식 작성 | 양식 이름 | [Id로 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) | 웹 양식 |

&quot;&lt;<em>program</em>>을 사용해야 합니다.마케팅 프로그램, 정적 목록, 웹 폼과 같은 자산 그룹의 이름을 지정하는 &lt;<em>자산</em>>&quot; 표기법 예를 들어 이름이 &quot;GL_OP_ALL_2021&quot;인 프로그램 아래에 있는 이름이 &quot;MPS Outbound&quot;인 양식은 &quot;GL_OP_ALL_2021.MPS Outbound&quot;로 지정됩니다.

예제 요청 본문:

```json
{
  "filter": {
    "createdAt": {
      "startAt": "2021-07-01T23:59:59-00:00",
      "endAt": "2021-07-02T23:59:59-00:00"
    },
    "activityTypeIds": [
      2
    ],
    "primaryAttributeValues": [
      "GL_OP_ALL_2021.MPS Outbound"
    ]
  }
}
```

`primaryAttributeValues`을(를) 사용하는 경우 `activityTypeIds` 필터가 있어야 하며 해당 자산 그룹과 일치하는 활동 ID만 포함해야 합니다. 예를 들어 웹 양식 자산을 필터링하는 경우 `activityTypeIds`에서 &quot;양식 작성&quot; 활동 유형 ID만 허용됩니다. `primaryAttributeValues`과(와) `primaryAttributeValueIds`은(는) 함께 사용할 수 없습니다.

## 옵션

| 매개변수 | 데이터 유형 | 필수 | 참고 |
|---|---|---|---|
| filter | 배열[개체] | 예 | 필터 배열을 허용합니다. 배열에 정확히 하나의 `createdAt` 필터가 포함되어야 합니다. 선택적 `activityTypeIds` 필터가 포함될 수 있습니다. 액세스 가능한 활동 세트에 필터가 적용되고 내보내기 작업에 의해 결과 활동 세트가 반환됩니다. |
| 형식 | 문자열 | 아니요 | CSV, TSV, SSV 중 하나 허용 내보낸 파일은 설정된 경우 각각 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값 파일로 렌더링됩니다. 설정하지 않으면 기본값이 CSV로 설정됩니다. |
| 열 머리글 이름 | 오브젝트 | 아니요 | 필드 및 열 헤더 이름의 키-값 쌍을 포함하는 JSON 개체입니다. 키는 내보내기 작업에 포함된 필드 이름이어야 합니다. 값은 해당 필드에 대해 내보낸 열 헤더의 이름입니다. |
| 필드 | 배열[문자열] | 아니요 | 필드 값을 포함하는 선택적 문자열 배열입니다. 나열된 필드는 내보낸 파일에 포함됩니다. 기본적으로 다음 필드가 반환됩니다. <ul><li>`marketoGUIDleadId`</li><li> `activityDate` </li><li>`activityTypeId` </li><li>`campaignId`</li><li> `primaryAttributeValueId` </li><li>`primaryAttributeValue`</li><li> `attributes`</li></ul>. 이 매개 변수는 위의 목록에서 하위 집합을 지정하여 반환되는 필드 수를 줄이는 데 사용할 수 있습니다. `"fields": ["leadId", "activityDate", "activityTypeId"]`. 활동 작업 `actionResult`을(를) 포함하도록 추가 필드 `("succeeded", "skipped", or "failed")`을(를) 지정할 수 있습니다. |

## 작업 생성

레코드를 내보내려면 먼저 작업과 검색할 레코드 집합을 정의해야 합니다.  [내보내기 활동 만들기 작업](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) 끝점을 사용하여 작업을 만듭니다.  활동을 내보낼 때 적용할 수 있는 기본 필터가 두 개 있습니다. 항상 필요한 `createdAt`과(와) 선택 사항인 `activityTypeIds`입니다.  `createdAt` 필터는 `startAt` 및 `endAt` 매개 변수(모두 datetime 필드)를 사용하여 활동이 만들어진 날짜 범위를 정의하는 데 사용됩니다. 이 매개 변수는 모두 가장 빠른 생성 날짜와 가장 최근 허용된 생성 날짜를 나타냅니다.  `activityTypeIds` 필터를 사용하여 특정 유형의 활동만 선택적으로 필터링할 수도 있습니다.  이 기능은 사용 사례와 관련이 없는 결과를 제거하는 데 유용합니다.

```
POST /bulk/v1/activities/export/create.json
```

```json
{
   "format": "CSV",
   "filter": {
      "createdAt": {
         "startAt": "2017-07-01T23:59:59-00:00",
         "endAt": "2017-07-31T23:59:59-00:00"
      },
      "activityTypeIds": [
         1,
         12,
         13
      ]
   }
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Created",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

이제 작업 상태가 &quot;생성됨&quot;이지만 아직 처리 큐에 있지 않습니다.  처리를 시작할 수 있도록 큐에 넣으려면 만들기 상태 응답에서 exportId를 사용하여 [큐 내보내기 활동 작업](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) 끝점을 호출합니다.

```
POST /bulk/v1/activities/export/{exportId}/enqueue.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Queued",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

이제 상태는 작업이 큐에 있음을 보고합니다.  작업자가 이 작업에 사용 가능해지면 상태가 &quot;처리 중&quot;으로 전환되고 작업이 Marketo의 레코드를 집계하기 시작합니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 작업 상태를 검색할 수 있습니다.

Marketo의 벌크 활동 추출은 비동기 끝점이므로 작업 상태를 폴링하여 작업이 완료되는 시기를 확인해야 합니다.  다음과 같이 [내보내기 활동 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) 끝점을 사용하여 폴링합니다.

```
GET /bulk/v1/activities/export/{exportId}/status.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Completed",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "startedAt": "2017-01-21T11:51:30-08:00",
         "finishedAt": "2017-01-21T12:59:30-08:00",
         "format": "CSV",
         "numberOfRecords": 15423,
         "fileSize": 12342,
         "fileChecksum": "sha256:c16514c7e80fcac5ea055dacae9617fc3c29aff5365e3743071313ce0ed2a815"
      }
   ]
}
```

상태 필드는 다음 값 중 하나로 응답할 수 있습니다.

- 생성됨
- 대기열에 추가됨
- 처리 중
- 취소됨
- 완료
- 실패

## 데이터 검색 중

작업이 완료되면 [내보내기 활동 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) 끝점을 사용하여 데이터를 검색합니다.

```
GET /bulk/v1/activities/export/{exportId}/file.json
```

응답에는 작업이 구성된 방식으로 포맷된 파일이 포함됩니다. 끝점이 파일의 내용에 응답합니다.

요청한 리드 필드가 비어 있으면(데이터 없음) `then null`이(가) 내보내기 파일의 해당 필드에 배치됩니다.  아래 예제에서는 반환된 활동의 `campaignId` 필드가 비어 있습니다.

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

추출된 데이터의 부분 검색과 재시작 친화적 검색을 지원하기 위해 파일 끝점은 선택적으로 `Range` 형식의 HTTP 헤더 `bytes`을(를) 지원합니다.  헤더가 설정되지 않은 경우 전체 콘텐츠가 반환됩니다.  Marketo [일괄 추출](bulk-extract.md)에서 범위 헤더 사용에 대한 자세한 내용을 읽을 수 있습니다.

## 작업 취소

작업이 잘못 구성되었거나 필요하지 않은 경우 [내보내기 활동 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) 끝점을 사용하여 작업을 쉽게 취소할 수 있습니다.

```
POST /bulk/v1/activities/export/{exportId}/cancel.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Cancelled",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "format": "CSV"
      }
   ]
}
```

이 응답에는 작업이 취소되었음을 나타내는 상태가 있습니다.
