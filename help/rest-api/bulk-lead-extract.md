---
title: 벌크 납 추출
feature: REST API
description: 리드 데이터의 일괄 추출.
exl-id: 42796e89-5468-463e-9b67-cce7e798677b
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 2%

---

# 벌크 납 추출

[잠재 고객 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads)

REST API의 벌크 리드 추출 세트는 Marketo에서 대규모 리드/개인 레코드 세트를 검색하는 프로그래밍 방식 인터페이스를 제공합니다. 또한 레코드의 생성 날짜, 가장 최근 업데이트, 정적 목록 멤버십 또는 스마트 목록 멤버십에 따라 점진적으로 리드를 검색하는 데 사용할 수 있습니다. ETL, 데이터 웨어하우징 및 보관 목적으로 Marketo과 하나 이상의 외부 시스템 간에 데이터를 지속적으로 교환해야 하는 사용 사례에 권장되는 인터페이스입니다.

## 권한

벌크 리드 추출 API를 사용하려면 소유 API 사용자에게 읽기 전용 리드 또는 읽기-쓰기 리드 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

## 필터

리드는 다양한 필터 옵션을 지원합니다. `updatedAt`, `smartListName` 및 `smartListId`을(를) 포함한 특정 필터에는 모든 구독으로 아직 롤아웃되지 않은 추가 인프라 구성 요소가 필요합니다. 내보내기 작업당 하나의 필터 유형만 지정할 수 있습니다.

| 필터 유형 | 데이터 유형 | 참고 사항 |
|---|---|---|
| createdAt | 날짜 범위 | `startAt` 및 `endAt` 멤버를 사용하여 JSON 개체를 허용합니다. `startAt`은(는) 로우 워터마크를 나타내는 날짜/시간을 수락하고 `endAt`은(는) 하이 워터마크를 나타내는 날짜/시간을 수락합니다. 범위는 31일 이하여야 합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다. 이 필터 유형의 작업은 날짜 범위 내에서 만든 액세스 가능한 모든 레코드를 반환합니다. |
| updatedAt* | 날짜 범위 | `startAt` 및 `endAt` 멤버를 사용하여 JSON 개체를 허용합니다. `startAt`은(는) 로우 워터마크를 나타내는 날짜/시간을 수락하고 `endAt`은(는) 하이 워터마크를 나타내는 날짜/시간을 수락합니다. 범위는 31일 이하여야 합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다. 참고: 이 필터는 표준 필드에 대한 업데이트만 반영하는 표시되는 &quot;updatedAt&quot; 필드를 필터링하지 않습니다. 이 필터는 잠재 고객 레코드에 대한 가장 최근 필드 업데이트가 이루어진 시점을 기준으로 필터링합니다.이 필터 유형을 가진 작업은 날짜 범위 내에서 가장 최근 업데이트된 액세스 가능한 모든 레코드를 반환합니다. |
| staticListName | 문자열 | 정적 목록의 이름을 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 이름을 검색합니다. |
| staticListId | 정수 | 정적 목록의 ID를 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 ID를 검색합니다. |
| smartListName* | 문자열 | 스마트 목록의 이름을 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 스마트 목록의 구성원인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 끝점을 사용하여 스마트 목록 이름을 검색합니다. |
| smartListId* | 정수 | 스마트 목록의 ID를 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 스마트 목록의 구성원인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 끝점을 사용하여 스마트 목록 ID를 검색합니다. |


일부 구독에서는 필터 유형을 사용할 수 없습니다. 구독에 사용할 수 없는 경우 리드 작업 내보내기 만들기 엔드포인트를 호출할 때 오류가 발생합니다(&quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot;). 고객은 Marketo 지원 센터에 문의하여 구독에서 이 기능을 활성화할 수 있습니다.

## 옵션

리드 작업 내보내기 만들기 엔드포인트는 사용자에게 내보낸 파일 내에 특정 필드를 포함할 수 있는 기능, 이러한 필드의 열 헤더 이름을 바꿀 수 있는 기능 및 내보낸 파일의 형식을 제공하는 몇 가지 서식 옵션을 제공합니다.

| 매개 변수 | 데이터 유형 | 필수 | 참고 사항 |
|---|---|---|---|
| 필드 | 배열[문자열] | 예 | 필드 매개 변수는 JSON 문자열 배열을 수락합니다. 각 문자열은 Marketo 리드 필드의 REST API 이름이어야 합니다. 나열된 필드는 내보낸 파일에 포함됩니다. columnHeader로 재정의되지 않는 한, 각 필드의 열 헤더는 각 필드의 REST API 이름이 됩니다. 참고: [!DNL Adobe Experience Cloud Audience Sharing] 기능을 사용하면 [!DNL Adobe Experience Cloud] ID(ECID)를 Marketo 리드와 연결하는 쿠키 동기화 프로세스가 발생합니다. 내보내기 파일에 ECID를 포함하도록 &quot;ecids&quot; 필드를 지정할 수 있습니다. |
| 열 머리글 이름 | 오브젝트 | 아니요 | 필드 및 열 헤더 이름의 키-값 쌍을 포함하는 JSON 개체입니다. 키는 내보내기 작업에 포함된 필드 이름이어야 합니다. Describe Lead 를 호출하여 검색할 수 있는 필드의 API 이름입니다. 값은 해당 필드에 대해 내보낸 열 헤더의 이름입니다. |
| 형식 | 문자열 | 아니요 | CSV, TSV, SSV 중 하나를 허용합니다. 내보낸 파일은 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값 파일로 렌더링됩니다(설정된 경우). 설정하지 않으면 기본값이 CSV로 설정됩니다. |


## 작업 생성

[내보내기 리드 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/createExportLeadsUsingPOST) 끝점을 사용하여 내보내기를 시작하기 전에 작업에 대한 매개 변수를 정의합니다. 내보내기에 필요한 `fields`, `filter`의 매개 변수 유형, 파일의 `format` 및 열 헤더 이름(있는 경우)을 정의해야 합니다.

```
POST /bulk/v1/leads/export/create.json
```

```json
{
   "fields": [
      "firstName",
      "lastName",
      "id",
      "email"
   ],
   "format": "CSV",
   "columnHeaderNames": {
      "firstName": "First Name",
      "lastName": "Last Name",
      "id": "Marketo Id",
      "email": "Email Address"
   },
   "filter": {
      "createdAt": {
         "startAt": "2017-01-01T00:00:00Z",
         "`endAt`": "2017-01-31T00:00:00Z"
      }
   }
}
```

이 요청은 해당 `firstName`, `lastName`, `id` 및 `email` 필드의 값을 포함하여 2017년 1월 1일부터 2017년 1월 31일 사이에 생성된 리드 집합 내보내기를 시작합니다.

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

작업이 생성되었음을 나타내는 상태 응답이 반환됩니다. 작업이 정의되고 생성되었지만 아직 시작되지 않았습니다. 이렇게 하려면 만들기 상태 응답의 exportId를 사용하여 [큐 내보내기 리드 작업](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/enqueueExportLeadsUsingPOST) 끝점을 호출해야 합니다.

```
POST /bulk/v1/leads/export/{exportId}/enqueue.json
```

```json
{
    "requestId": "147e4#16b24d9b913",
    "result": [
        {
            "exportId": "fad2cd1b-e822-4025-be1e-9caa9cf1d4b8",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2019-06-04T23:35:43Z",
            "queuedAt": "2019-06-04T23:36:17Z"
        }
    ],
    "success": true
}
```

&quot;큐에 있음&quot;의 `status`에 응답합니다. 이 응답 후에는 사용 가능한 내보내기 슬롯이 있는 경우 &quot;처리 중&quot;으로 설정됩니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 `Note:` 상태를 검색할 수 있습니다.

비동기 끝점이므로 작업을 만든 후 상태를 폴링하여 진행률을 확인해야 합니다. [리드 내보내기 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) 끝점을 사용하여 폴링합니다. 상태는 60초마다 한 번만 업데이트되므로 이보다 낮은 폴링 빈도는 권장되지 않으며 거의 모든 경우에 여전히 과도합니다. 투표를 간단히 살펴봅시다.

```
GET /bulk/v1/leads/export/{exportId}/status.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Processing",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

상태 끝점은 작업이 아직 처리 중이므로 파일을 검색할 수 없다는 것을 나타냅니다. 작업 상태가 &quot;완료됨&quot;으로 변경되면 다운로드를 준비했습니다.

상태 필드는 다음 중 하나로 응답할 수 있습니다.

- 제작
- 대기열에 추가됨
- 처리 중
- 취소됨
- 완료
- 실패

## 데이터 검색 중

완료된 잠재 고객 내보내기의 파일을 검색하려면 `exportId`을(를) 사용하여 [잠재 고객 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/getExportLeadsFileUsingGET) 끝점을 호출하면 됩니다.

```
GET /bulk/v1/leads/export/{exportId}/file.json
```

응답에는 작업이 구성된 방식으로 포맷된 파일이 포함됩니다. 끝점이 파일의 내용에 응답합니다.

요청한 리드 필드가 비어 있으면(데이터 없음) `null`이(가) 내보내기 파일의 해당 필드에 배치됩니다. 아래 예에서는 반환된 리드에 대한 이메일 필드가 비어 있습니다.

```csv
firstName,lastName,email,cookies
Russell,Wilson,null,_mch-localhost-1536605780000-12105
```

추출된 데이터의 부분 검색 및 재시작 친화성을 지원하기 위해 파일 엔드포인트는 선택적으로 바이트 유형의 HTTP 헤더 범위를 지원합니다. 헤더가 설정되지 않은 경우 전체 콘텐츠가 반환됩니다. Marketo [일괄 추출](bulk-extract.md)에서 범위 헤더를 사용하는 방법에 대해 자세히 알아보십시오.

## 작업 취소

작업이 잘못 구성되었거나 불필요하게 된 경우 [리드 작업 내보내기 취소](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Leads/operation/cancelExportLeadsUsingPOST) 끝점을 사용하여 작업을 쉽게 취소할 수 있습니다.

```
POST /bulk/v1/leads/export/{exportId}/cancel.json
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

작업이 취소되었음을 나타내는 상태로 응답합니다.
