---
title: 일괄 활동 추출
feature: REST API
description: Marketo 벌크 활동 REST API를 추출하여 31일 날짜 범위, 활동 및 ETL 및 CRM에 대한 기본 속성 필터를 사용하여 대용량 활동 데이터를 내보냅니다.
exl-id: 6bdfa78e-bc5b-4eea-bcb0-e26e36cf6e19
TQID: https://experienceleague.adobe.com/lIlXNjatN-F77Dv3xsVkQ3hAWwLZ4wlSW0zKNkFJFMA
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1268
ht-degree: 4%

---

# 일괄 활동 추출

[일괄 활동 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi)

벌크 활동 추출 REST API는 Marketo에서 대량의 활동 데이터를 검색합니다. CRM 통합, ETL, 데이터 웨어하우징 및 데이터 보관과 같이 짧은 지연 시간이 필요하지 않은 프로세스에 이러한 API를 사용합니다.

## 권한

API 사용자에게는 &quot;읽기 전용 활동&quot; 또는 &quot;읽기-쓰기 활동&quot; 권한이 있어야 합니다.

## 필터

| 필터 유형 | 데이터 유형 | 필수 | 참고 |
| --- | --- | --- | --- |
| `createdAt` | 날짜 범위 | 예 | `startAt` 및 `endAt`을(를) 포함하는 JSON 개체입니다. `startAt`은(는) 로우 워터마크 날짜/시간이고 `endAt`은(는) 하이 워터마크 날짜/시간입니다. 범위는 31일 이하여야 합니다. 이 작업은 날짜 범위 내에서 만든 액세스 가능한 모든 레코드를 반환합니다. 밀리초 없이 ISO-8601 날짜/시간 값을 사용합니다. |
| `activityTypeIds` | Array\[Integer\] | 아니요 | 요청된 활동 유형에 대한 정수 배열입니다. &quot;잠재 고객 삭제&quot; 활동은 지원되지 않습니다. 대신 [삭제된 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getDeletedLeadsUsingGET) 끝점을 사용하십시오. [활동 유형 가져오기 엔드포인트](https://developer.adobe.com/marketo-apis/api/mapi#tag/Activities/operation/getAllActivityTypesUsingGET)를 사용하여 활동 유형 ID를 검색합니다. |
| [`primaryAttributeValueIds`](#primaryattributevalueids-options) | Array\[Integer\] | 아니요 | 기본 속성에 대해 최대 50개의 ID를 허용하는 배열입니다. 각 ID는 잠재 고객 필드 또는 자산을 고유하게 식별합니다. 적절한 REST API 끝점을 호출하여 ID를 검색합니다. 예를 들어 &quot;양식 채우기&quot; 활동에 대한 특정 양식을 필터링하려면 양식 이름을 [이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET) 엔드포인트에 전달하여 양식 ID를 검색합니다. 지원되는 활동 유형은 [primaryAttributeValueIds 옵션](#primaryattributevalueids-options)을 참조하십시오. |
| [`primaryAttributeValues`](#primaryattributevalues-options) | Array\[String\] | 아니요 | 기본 속성에 대해 최대 50개의 이름을 사용할 수 있는 배열입니다. 각 이름은 리드 필드 또는 자산을 고유하게 식별합니다. 적절한 REST API 끝점을 호출하여 이름을 검색합니다. 예를 들어 &quot;양식 채우기&quot; 활동에 대한 특정 양식을 필터링하려면 양식 ID를 [ID별로 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET) 엔드포인트에 전달하여 양식 이름을 검색합니다. 지원되는 활동 유형은 [primaryAttributeValues 옵션](#primaryattributevalues-options)을 참조하십시오. |

### primaryAttributeValueIds 옵션 {#primaryattributevalueids-options}

| 활동 유형 | 기본 속성 값 Id | 검색 끝점 | 자산 그룹 |
| --- | --- | --- | --- |
| 데이터 값 변경 | 리드 필드 ID | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 점수 변경 | 리드 필드 ID | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 진행 상태 변경 | 프로그램 ID | [이름별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByNameUsingGET) | 마케팅 프로그램 |
| 목록에 추가 | 정적 목록 ID | [이름별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 정적 목록 |
| 목록에서 제거 | 정적 목록 ID | [이름별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByNameUsingGET) | 정적 목록 |
| 양식 작성 | 양식 ID | [이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET) | 웹 양식 |

`primaryAttributeValueIds`을(를) 사용하는 경우 `activityTypeIds` 필터도 포함해야 합니다. 이 필터에는 해당 자산 그룹과 일치하는 활동 ID만 포함할 수 있습니다. 예를 들어 웹 양식 자산을 필터링할 때 `activityTypeIds`에는 &quot;양식 채우기&quot; 활동 유형 ID만 포함될 수 있습니다.

다음 요청에는 `primaryAttributeValueIds` 필터가 포함되어 있습니다.

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
| 데이터 값 변경 | 리드 필드 displayName | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 점수 변경 | 리드 필드 displayName | [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) | 속성 이름 |
| 진행 상태 변경 | 프로그램 이름 | [Id로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByIdUsingGET) | 마케팅 프로그램 |
| 목록에 추가 | 정적 목록 이름 | [Id별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 정적 목록 |
| 목록에서 제거 | 정적 목록 이름 | [Id별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Static-Lists/operation/getStaticListByIdUsingGET) | 정적 목록 |
| 양식 작성 | 양식 이름 | [Id로 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET) | 웹 양식 |

마케팅 프로그램, 정적 목록 및 웹 양식 자산 그룹의 이름을 지정하려면 `&lt;program&gt;.&lt;asset&gt;` 표기법을 사용하십시오. 예를 들어 &quot;GL_OP_ALL_2021&quot; 프로그램의 &quot;MPS 아웃바운드&quot; 화면을 &quot;GL_OP_ALL_2021.MPS 아웃바운드&quot;로 지정합니다.

다음 요청에는 `primaryAttributeValues` 필터가 포함되어 있습니다.

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

`primaryAttributeValues`을(를) 사용하는 경우 `activityTypeIds` 필터도 포함해야 합니다. 이 필터에는 해당 자산 그룹과 일치하는 활동 ID만 포함할 수 있습니다. 예를 들어 웹 양식 자산을 필터링할 때 `activityTypeIds`에는 &quot;양식 채우기&quot; 활동 유형 ID만 포함될 수 있습니다.

`primaryAttributeValues`과(와) `primaryAttributeValueIds`은(는) 함께 사용할 수 없습니다.

## 옵션

| 매개변수 | 데이터 유형 | 필수 | 참고 |
| --- | --- | --- | --- |
| `filter` | 오브젝트 | 예 | 액세스 가능한 활동 세트에 적용되는 필터가 포함된 객체입니다. `createdAt` 필터를 하나만 포함하십시오. `activityTypeIds` 필터를 포함할 수도 있습니다. 내보내기 작업은 결과 활동 세트를 반환합니다. |
| `format` | 문자열 | 아니요 | 내보내기 파일 형식: CSV, TSV 또는 SSV. 이 값은 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값을 각각 생성합니다. 기본값은 CSV입니다. |
| `columnHeaderNames` | 오브젝트 | 아니요 | 필드 및 열-헤더 키-값 쌍의 JSON 개체. 각 키는 내보내기 작업에 포함된 필드의 이름을 지정해야 합니다. 이 값은 해당 필드에 대해 내보낸 열 헤더를 설정합니다. |
| `fields` | Array\[String\] | 아니요 | 내보내기 파일에 포함할 필드의 배열. 기본적으로 응답에는 `marketoGUID`, `leadId`, `activityDate`, `activityTypeId`, `campaignId`, `primaryAttributeValueId`, `primaryAttributeValue` 및 `attributes`이(가) 포함됩니다. 하위 집합을 반환하려면 이 목록에서 `"fields": ["leadId", "activityDate", "activityTypeId"]` 등의 필드를 지정하십시오. `actionResult`을(를) 지정하여 `("succeeded", "skipped", or "failed")` 활동 작업을 포함할 수도 있습니다. |

## 작업 생성

내보낼 작업을 만들어 검색할 레코드를 정의합니다. [내보내기 활동 만들기 작업](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) 끝점을 사용합니다.

모든 작업에는 `createdAt` 필터가 필요합니다. 해당 `startAt` 및 `endAt` 날짜/시간 매개 변수는 허용되는 활동 생성 날짜를 가장 이른 날짜와 가장 늦은 날짜로 정의합니다. 관련성이 없는 활동 유형을 제외하려면 선택적 `activityTypeIds` 필터도 포함하십시오.

다음 요청은 날짜 범위 내에서 선택한 활동 유형에 대한 CSV 내보내기 작업을 만듭니다.

```http
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

응답이 `exportId` 및 &quot;생성됨&quot; 상태를 반환합니다. 생성된 작업이 아직 처리 큐에 없습니다.

큐에 작업을 추가하려면 만들기 응답에서 `exportId`을(를) 사용하여 [큐 내보내기 활동 작업](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) 끝점을 호출합니다.

```http
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

이제 응답 상태가 &quot;대기 중&quot;입니다. 작업자를 사용할 수 있게 되면 상태가 &quot;처리 중&quot;으로 변경되고 작업이 Marketo의 레코드를 집계하기 시작합니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 작업 상태를 검색할 수 있습니다.

일괄 활동 추출은 작업을 비동기적으로 처리합니다. [내보내기 활동 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) 끝점을 폴링하여 작업이 완료되는 시기를 확인합니다.

```http
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

`status` 필드는 다음 값 중 하나를 반환합니다.

- `Created`
- `Queued`
- `Processing`
- `Canceled`
- `Completed`
- `Failed`

## 데이터 검색 중

작업 상태가 &quot;완료됨&quot;이면 [내보내기 활동 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) 끝점을 사용하여 내보낸 데이터를 검색합니다.

```http
GET /bulk/v1/activities/export/{exportId}/file.json
```

응답 본문에는 작업에 대해 구성된 형식의 파일이 포함됩니다.

요청된 활동 필드에 데이터가 없으면 `null`이(가) 해당 내보내기 파일 필드에 나타납니다. 다음 예제에서는 내보낸 활동 데이터를 보여 줍니다.

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

부분 검색 또는 다시 시작 가능한 검색의 경우 파일 끝점은 `bytes` 범위의 선택적 HTTP `Range` 헤더를 지원합니다. 이 헤더를 생략하면 끝점이 전체 파일을 반환합니다. `Range` 헤더 사용에 대한 자세한 내용은 [일괄 추출](bulk-extract.md)을 참조하십시오.

## 작업 취소

잘못 구성되었거나 불필요한 작업을 중지하려면 [내보내기 활동 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) 끝점을 호출하십시오.

```http
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

응답 상태는 작업이 취소되었음을 나타냅니다.
