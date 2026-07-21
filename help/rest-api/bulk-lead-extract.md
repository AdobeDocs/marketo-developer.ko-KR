---
title: 벌크 납 추출
feature: REST API
description: Marketo 대량 리드 추출 REST API를 사용하여 날짜, 목록 및 스마트 목록 필터, 사용자 정의 필드 및 CSV/TSV 형식으로 리드를 대량 내보내는 방법에 대해 알아봅니다.
exl-id: 42796e89-5468-463e-9b67-cce7e798677b
TQID: https://experienceleague.adobe.com/4eMJR87fHDdccrVid3wHtspvBVQmrBGHYMlIwFCSdEI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 2%

---

# 벌크 납 추출

[벌크 리드 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads)

벌크 리드 추출 REST API는 Marketo에서 큰 리드/개인 레코드 세트를 검색합니다. 레코드 생성 날짜, 가장 최근 업데이트, 정적 목록 멤버십 또는 스마트 목록 멤버십에 따라 가망 고객을 점진적으로 검색할 수도 있습니다.

ETL, 데이터 웨어하우징 및 아카이빙 워크플로우를 포함한 외부 시스템과 Marketo 간에 데이터를 지속적으로 교환하려면 Bulk Lead Extract 를 사용합니다.

## 권한

작업을 소유하는 API 사용자에게는 읽기 전용 리드 권한, 읽기-쓰기 리드 권한 또는 두 권한이 모두 있는 역할이 있어야 합니다.

## 필터

리드 내보내기 작업은 여러 필터 유형을 지원합니다. 각 내보내기 작업에서는 하나의 필터 유형만 사용할 수 있습니다.

`updatedAt`, `smartListName` 및 `smartListId` 필터에는 일부 구독에서는 사용할 수 없는 인프라가 필요합니다.

| 필터 유형 | 데이터 유형 | 참고 |
| --- | --- | --- |
| createdAt | 날짜 범위 | `startAt` 및 `endAt` 구성원이 있는 JSON 개체입니다. `startAt`은(는) 로우 워터마크 날짜/시간이고 `endAt`은(는) 하이 워터마크 날짜/시간입니다. 밀리초 없이 ISO-8601 날짜 및 시간 값을 사용합니다. 범위는 31일 이하여야 합니다. 이 작업은 날짜 범위 내에서 만든 액세스 가능한 모든 레코드를 반환합니다. |
| updatedAt* | 날짜 범위 | `startAt` 및 `endAt` 구성원이 있는 JSON 개체입니다. `startAt`은(는) 로우 워터마크 날짜/시간이고 `endAt`은(는) 하이 워터마크 날짜/시간입니다. 밀리초 없이 ISO-8601 날짜 및 시간 값을 사용합니다. 범위는 31일 이하여야 합니다. 이 필터는 표준 필드에 대한 업데이트만 반영하는 표시되는 `updatedAt` 필드를 사용하지 않습니다. 대신 리드 레코드에 대한 가장 최근 필드 업데이트 시간을 사용합니다. 이 작업은 날짜 범위 내에서 가장 최근에 업데이트된 액세스 가능한 모든 레코드를 반환합니다. |
| staticListName | 문자열 | 정적 목록의 이름입니다. 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 이름을 검색합니다. |
| staticListId | 정수 | 정적 목록의 ID입니다. 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 ID를 검색합니다. |
| smartListName* | 문자열 | 스마트 목록의 이름입니다. 이 작업은 작업 처리를 시작할 때 스마트 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 엔드포인트를 사용하여 스마트 목록 이름을 검색합니다. |
| smartListId* | 정수 | 스마트 목록의 ID입니다. 이 작업은 작업 처리를 시작할 때 스마트 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 엔드포인트를 사용하여 스마트 목록 ID를 검색합니다. |

일부 구독에서는 별표가 표시된 필터 유형을 사용할 수 없습니다. 구독에 필터 유형을 사용할 수 없는 경우 리드 작업 내보내기 만들기 끝점이 &quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot; 오류를 반환합니다. 구독에 대해 이 기능을 활성화하려면 Marketo 지원 센터에 문의하십시오.

## 옵션

리드 작업 내보내기 만들기 엔드포인트는 내보낸 필드를 선택하고, 열 헤더의 이름을 바꾸고, 파일 형식을 설정하는 옵션을 제공합니다.

| 매개변수 | 데이터 유형 | 필수 | 참고 |
| --- | --- | --- | --- |
| 필드 | 배열[문자열] | 예 | 문자열의 JSON 배열입니다. 각 문자열은 Marketo 리드 필드의 REST API 이름이어야 합니다. 내보내기는 나열된 각 필드를 포함하며 `columnHeaderNames`이(가) 재정의하지 않는 한 해당 REST API 이름을 열 헤더로 사용합니다. [!DNL Adobe Experience Cloud Audience Sharing] 기능을 사용하도록 설정하면 쿠키 동기화 프로세스가 [!DNL Adobe Experience Cloud] ID(ECID)를 Marketo 리드와 연결합니다. 내보내기 파일에 ECID를 포함할 `ecids` 필드를 지정합니다. |
| 열 머리글 이름 | 오브젝트 | 아니요 | 필드 및 열-헤더 키-값 쌍의 JSON 개체. 각 키는 내보내기 작업에 포함된 필드의 API 이름이어야 합니다. Describe Lead 를 호출하여 API 이름을 검색합니다. 각 값은 해당 필드에 대한 내보낸 열 헤더입니다. |
| 형식 | 문자열 | 아니요 | 내보내기 파일 형식: 쉼표로 구분된 값의 경우 CSV, 탭으로 구분된 값의 경우 TSV 또는 공백으로 구분된 값의 경우 SSV입니다. 기본값은 CSV입니다. |

## 작업 생성

[리드 내보내기 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/createExportLeadsUsingPOST) 끝점을 사용하여 내보내기 작업을 정의합니다. 내보낼 `fields`, 하나의 `filter` 형식 및 해당 매개 변수, `format` 파일 및 사용자 지정 열 헤더 이름을 지정합니다.

```http
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
         "endAt": "2017-01-31T00:00:00Z"
      }
   }
}
```

이 요청은 2017년 1월 1일부터 2017년 1월 31일 사이에 생성된 리드에 대한 내보내기 작업을 생성합니다. 내보내기에 `firstName`, `lastName`, `id` 및 `email` 필드의 값이 포함됩니다.

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

응답에서 작업이 생성되었지만 시작되지 않았음을 확인합니다. 작업을 시작하려면 만들기 응답에서 `exportId`을(를) 사용하여 [큐 내보내기 리드 작업](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/enqueueExportLeadsUsingPOST) 끝점을 호출합니다.

```http
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

대기열에 넣기 응답의 `status`이(가) &quot;대기 중&quot;입니다. 내보내기 슬롯을 사용할 수 있게 되면 상태가 &quot;처리 중&quot;으로 변경됩니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 상태를 검색할 수 있습니다.

리드 내보내기 작업은 비동기적으로 실행됩니다. [리드 내보내기 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsStatusUsingGET) 끝점을 폴링하여 작업 진행 상황을 추적합니다.

상태는 60초마다 한 번만 업데이트됩니다. 더 자주 투표하지 마십시오. 거의 모든 경우에, 이 간격은 여전히 과도합니다.

```http
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

이 응답은 작업이 아직 처리 중이므로 파일을 사용할 수 없음을 보여줍니다. 작업 상태가 &quot;완료됨&quot;으로 변경되면 파일을 다운로드할 수 있습니다.

`status` 필드는 다음 값 중 하나를 반환할 수 있습니다.

- 생성됨
- 대기열에 추가됨
- 처리 중
- 취소됨
- 완료
- 실패

## 데이터 검색 중

완료된 리드 내보내기를 검색하려면 `exportId`을(를) 사용하여 [리드 내보내기 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/getExportLeadsFileUsingGET) 끝점을 호출하십시오.

```http
GET /bulk/v1/leads/export/{exportId}/file.json
```

응답 본문에는 작업에 대해 구성된 형식의 파일이 포함됩니다.

요청한 리드 필드에 데이터가 없으면 내보내기 파일의 해당 필드에 `null`이(가) 포함됩니다. 다음 예에서는 반환된 리드에 빈 이메일 필드가 있습니다.

```csv
firstName,lastName,email,cookies
Russell,Wilson,null,_mch-localhost-1536605780000-12105
```

부분 검색 또는 다시 시작 가능한 검색의 경우 파일 끝점은 `bytes` 형식의 선택적 HTTP `Range` 헤더를 지원합니다. 헤더를 설정하지 않으면 끝점이 모든 콘텐츠를 반환합니다. Marketo [일괄 추출](bulk-extract.md)에서 `Range` 헤더를 사용하는 방법에 대해 자세히 알아보세요.

## 작업 취소

잘못 구성되었거나 불필요한 작업을 취소하려면 [리드 내보내기 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Export-Leads/operation/cancelExportLeadsUsingPOST) 끝점을 호출하십시오.

```http
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

응답에서 작업이 취소되었음을 확인합니다.
