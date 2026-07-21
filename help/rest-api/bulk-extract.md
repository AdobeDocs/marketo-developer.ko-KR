---
title: 일괄 추출
feature: REST API
description: Marketo 벌크 추출 REST API를 사용하여 OAuth, 작업 큐 및 500MB 일일 제한으로 리드, 활동, 프로그램 멤버 및 사용자 지정 개체를 내보내는 방법에 대해 알아봅니다.
exl-id: 6a15c8a9-fd85-4c7d-9f65-8b2e2cba22ff
TQID: https://experienceleague.adobe.com/ECSchsjqp8fyxXbUGl5DgXHUkXuN0sIUc3yJfVaIe1E
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1549
ht-degree: 0%

---

# 일괄 추출

Marketo Bulk Extract는 대규모 개인 및 개인 관련 데이터 세트를 검색하는 인터페이스를 제공합니다. 인터페이스는 현재 다음 네 가지 객체 유형에 사용할 수 있습니다.

- 잠재 고객 (개인)
- 활동
- 프로그램 구성원
- 사용자 정의 오브젝트

벌크 추출을 수행하려면 다음을 수행합니다.

1. 작업을 만들고 검색할 데이터를 정의합니다.
1. 작업을 큐에 넣습니다.
1. 작업이 파일 쓰기를 완료할 때까지 기다립니다.
1. HTTP를 통해 파일을 검색합니다.

대량 추출 작업이 비동기적으로 실행됩니다. 내보내기 상태를 검색하기 위해 작업을 폴링합니다.

`Note:` 대량 API 끝점에는 다른 끝점처럼 &#39;/rest&#39; 접두사가 없습니다.

## 인증

벌크 추출 API는 다른 Marketo REST API와 동일한 OAuth 2.0 인증 방법을 사용합니다. `Authorization: Bearer {_AccessToken_}` HTTP 헤더에서 올바른 액세스 토큰을 보냅니다.

>[!IMPORTANT]
>
>**access_token** 쿼리 매개 변수를 사용하는 인증 지원이 2026년 8월 31일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 **인증** 헤더를 사용하도록 업데이트해야 합니다. 새 개발에서는 **Authorization** 헤더만 사용해야 합니다.

## 제한

- 최대 동시 내보내기 작업 수: 2
- 현재 내보내기 중인 작업을 포함하여 큐에 있는 최대 내보내기 작업: 10
- 파일 보존 기간: 7일
- 기본 일별 내보내기 할당: 500MB. 할당은 매일 오전 12시(CST)에 재설정됩니다. 증액은 구매할 수 있습니다.
- 날짜 범위 필터(`createdAt` 또는 `updatedAt`)의 최대 시간 범위: 31일

UpdatedAt 및 Smart List에 대한 대량 리드 추출 필터는 일부 구독 유형에서 사용할 수 없습니다. 이 필터를 사용할 수 없는 경우 리드 작업 내보내기 만들기 끝점이 &quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot; 오류를 반환합니다. 구독에 대해 이 기능을 활성화하려면 Marketo 지원 센터에 문의하십시오.

### 큐

벌크 추출 API는 리드, 활동, 프로그램 멤버 및 사용자 지정 개체 간에 공유되는 하나의 작업 큐를 사용합니다. 먼저 내보내기 리드/활동/프로그램 멤버 작업 만들기 엔드포인트를 호출하여 추출 작업을 생성합니다. 그런 다음 해당 대기열에 넣기 내보내기 리드/활동/프로그램 멤버 작업 끝점을 호출하여 작업을 대기열에 넣습니다. 컴퓨팅 리소스를 사용할 수 있게 되면 작업이 시작됩니다.

큐에는 최대 10개의 작업이 포함될 수 있습니다. 대기열이 가득 찼을 때 작업을 대기열에 넣으려고 하면 대기열에 넣기 내보내기 작업 끝점이 &quot;1029, 큐에 작업이 너무 많습니다&quot; 오류를 반환합니다. 최대 두 개의 작업이 &quot;처리 중&quot; 상태로 동시에 실행될 수 있습니다.

### 파일 크기

대량 추출 API는 대량 추출 작업이 검색하는 데이터의 디스크 크기에 따라 측정됩니다. 파일 크기를 바이트 단위로 확인하려면 내보내기 작업에 대한 완료된 상태 응답에서 `fileSize` 특성을 읽으십시오.

일일 할당량은 500MB이며 리드, 활동, 프로그램 구성원 및 사용자 지정 개체 간에 공유됩니다. 할당량을 초과하면 할당량이 자정 [중부 시간](https://en.wikipedia.org/wiki/Central_Time_Zone)에 재설정될 때까지 다른 작업을 만들거나 대기열에 넣을 수 없습니다. 재설정될 때까지 API는 &quot;1029, 일일 내보내기 할당량 초과&quot; 오류를 반환합니다. 일일 할당량 외에 최대 파일 크기는 없습니다.

작업이 큐에 올라가거나 처리 후, 오류가 발생하거나 작업을 취소하지 않는 한 작업이 완료될 때까지 실행됩니다. 작업이 실패하면 다시 만들어야 합니다.

API는 작업이 완료된 상태에 도달할 때만 전체 파일을 기록합니다. 부분 파일을 쓰지 않습니다. 파일을 확인하려면 해당 SHA-256 해시를 계산하고 작업 상태 끝점이 반환하는 체크섬과 비교합니다.

현재 날짜에 사용된 총 디스크 공간을 확인하려면 Get Export Lead/Activity/Program Member Jobs 엔드포인트를 호출합니다. 이러한 엔드포인트는 지난 7일의 모든 작업을 반환합니다.

`status` 및 `finishedAt` 특성을 사용하여 현재 일 동안 완료된 작업으로 목록을 필터링합니다. 그런 다음 해당 작업에 대한 파일 크기를 추가합니다. 파일을 삭제하여 디스크 공간을 확보할 수 없습니다.

## 권한

벌크 추출에서는 Marketo REST API와 동일한 권한 모델을 사용합니다. 추가적인 특수 권한은 필요하지 않지만 각 엔드포인트 세트에는 특정 권한이 필요합니다.

대량 추출 작업을 만든 API 사용자만 액세스할 수 있고, 상태를 폴링하거나, 파일 콘텐츠를 검색할 수 있습니다.

벌크 추출 종단점이 Marketo 작업 공간을 인식하지 못합니다. 추출 요청에는 사용자 정의 서비스에 대한 API 전용 사용자를 정의하는 방법에 관계없이 모든 작업 영역의 데이터가 포함됩니다.

## 작업 생성

Marketo 벌크 추출 API는 작업을 사용하여 데이터 추출을 시작하고 실행합니다. 다음 요청은 리드 내보내기 작업을 생성합니다.

```http
POST /bulk/v1/leads/export/create.json
```

```json
{
   "fields": [
      "firstName",
      "lastName"
   ],
   "format": "CSV",
   "columnHeaderNames": {
      "firstName": "First Name",
      "lastName": "Last Name"
   },
   "filter": {
      "createdAt": {
         "startAt": "2023-01-01T00:00:00Z",
         "endAt": "2023-01-31T00:00:00Z"
      }
   }
}
```

이 요청은 2023년 1월 1일부터 2023년 1월 31일 사이에 생성된 각 리드를 내보내는 작업을 생성합니다. CSV 파일은 &quot;firstName&quot; 및 &quot;lastName&quot; 필드의 값을 포함하며, 열 머리글인 &quot;First Name&quot; 및 &quot;Last Name&quot;을 사용합니다.

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Created",
         "createdAt": "2023-01-21T11:47:30-08:00",
         "queuedAt": "2023-01-21T11:48:30-08:00",
         "format": "CSV",
      }
   ]
}
```

응답이 `exportId` 특성에서 작업 ID를 반환합니다. 이 작업 ID를 사용하여 작업을 큐에 넣거나 취소하거나, 해당 상태를 확인하거나, 완료된 파일을 검색할 수 있습니다.

### 일반 매개 변수

각 작업 생성 끝점에는 파일 형식, 필드 이름 및 필터를 구성하기 위한 일반적인 매개 변수가 있습니다. 각 추출 작업 하위 유형에는 추가 매개 변수도 있을 수 있습니다.

| 매개변수 | 데이터 유형 | 참고 |
| --- | --- | --- |
| 형식 | 문자열 | 쉼표로 구분된 값, 탭으로 구분된 값 및 세미콜론으로 구분된 값에 대한 옵션을 사용하여 추출된 데이터의 파일 형식을 결정합니다. CSV, SSV, TSV 중 하나를 허용합니다. 형식은 기본적으로 CSV로 설정됩니다. |
| 열 머리글 이름 | 오브젝트 | 반환된 파일에서 열 헤더의 이름을 설정할 수 있습니다. 각 멤버 키는 이름을 바꿀 열 헤더의 이름이고 값은 열 헤더의 새 이름입니다. 예를 들어 &quot;columnHeaderNames&quot;: { &quot;firstName&quot;: &quot;First Name&quot;, &quot;lastName&quot;: &quot;Last Name&quot; }, |
| filter | 오브젝트 | 추출 작업에 적용된 필터. 작업 유형에 따라 유형과 옵션이 달라집니다. |

## 작업 검색 중

해당 개체 유형에 대한 내보내기 작업 가져오기 끝점을 사용하여 최근 작업을 검색합니다. 각 내보내기 작업 가져오기 끝점은 다음 매개 변수를 지원합니다.

- `status`이(가) 내보내기 상태별로 작업을 필터링합니다. 유효한 값은 생성, 대기 중, 처리, 취소, 완료 및 실패입니다.
- `batchSize`은(는) 반환되는 작업 수를 제한합니다. 기본값과 최대값은 300입니다.
- 큰 결과 집합을 통해 `nextPageToken`페이지.

다음 요청은 완료 또는 실패 상태의 가망 고객 내보내기 작업을 검색합니다.

```http
GET /bulk/v1/leads/export.json?status=Completed,Failed
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
         "numberOfRecords": 122323,
         "fileSize": 123424,
         "fileChecksum": "sha256:c16514c7e80fcac5ea055dacae9617fc3c29aff5365e3743071313ce0ed2a815"
      }
      ...
   ]
}
```

결과 배열에는 지난 7일 동안 해당 오브젝트 유형에 대해 생성된 각 작업에 대한 상태 응답이 포함되어 있습니다. 응답에는 호출을 수행하는 API 사용자가 소유한 작업만 포함됩니다.

## 작업 시작

작업을 만든 후 해당 작업 ID를 사용하여 대기열에 넣고 시작합니다.

```http
POST /bulk/v1/leads/export/{exportId}/enqueue.json
```

요청이 작업을 시작하고 상태 응답을 반환합니다. 내보내기가 비동기적으로 실행되므로 내보내기 완료 시기를 확인하려면 작업 상태를 폴링하십시오.

## 폴링 작업 상태

상태 끝점을 폴링하여 작업 진행 상황을 확인합니다. 작업을 생성한 API 사용자만 상태를 폴링할 수 있습니다.

작업 상태는 60초마다 두 번 이상 업데이트되지 않습니다. 이보다 더 자주 투표하지 마십시오. 대부분의 사용 사례에서는 5분에 한 번 폴링하면 충분합니다. 성공한 각 내보내기의 데이터는 10일 동안 유지됩니다.

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
         "status": "Completed",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "startedAt": "2017-01-21T11:51:30-08:00",
         "finishedAt": "2017-01-21T12:59:30-08:00",
         "format": "CSV",
         "numberOfRecords": 122323,
         "fileSize": 123424,
         "fileChecksum": "sha256:d9c73f0b6960c71623c8bafe29603b3e8e20fd0e4eeaefd119c0227506ea9be4"
      }
   ]
}
```

내부 `status` 구성원은 작업의 진행 상황을 나타냅니다. 해당 값은 생성, 대기 중, 처리, 취소, 완료 또는 실패 중 하나일 수 있습니다.

이 예에서는 작업이 완료되므로 폴링을 중지하고 파일을 검색할 수 있습니다. 완료된 작업의 경우 `fileSize` 멤버는 총 파일 길이를 바이트 단위로 나타내고 `fileChecksum` 멤버는 파일의 SHA-256 해시를 포함합니다. 작업 상태는 작업이 완료됨 또는 실패 상태에 도달한 후 30일 동안 사용할 수 있습니다.

## 데이터 검색 중

작업이 완료되면 내보낸 파일을 검색합니다.

```http
GET /bulk/v1/leads/export/{exportId}/file.json
```

응답에는 작업에 대해 구성된 형식의 파일이 포함됩니다. 작업이 완료되지 않았거나 요청에 잘못된 작업 ID가 포함된 경우 파일 끝점은 404 찾을 수 없음 상태와 일반 텍스트 오류 메시지를 반환합니다. 이 응답은 다른 대부분의 Marketo REST 끝점 응답과 다릅니다.

부분 검색 및 다시 시작 가능한 검색을 지원하기 위해 파일 끝점은 [RFC 7233](https://datatracker.ietf.org/doc/html/rfc7233)에 정의된 대로 `bytes` 형식의 선택적 HTTP `Range` 헤더를 지원합니다. 헤더를 설정하지 않으면 끝점이 전체 파일을 반환합니다.

파일의 처음 10,000바이트를 검색하려면 GET 요청에서 다음 헤더를 전달합니다. 범위는 바이트 0에서 시작합니다.

```text
Range: bytes=0-9999
```

부분 파일의 경우 끝점은 상태 코드 206과 Accept-ranges, Content-Length 및 Content-Range 헤더를 반환합니다.

```text
Accept-Ranges: bytes
Content-Length: 10000
Content-Range: bytes 0-9999/123424
```

### 부분 검색 및 재개

`Range` 헤더를 사용하여 파일의 일부를 검색하거나 검색을 다시 시작하십시오. 파일 범위는 바이트 0에서 시작하여 `fileSize`에서 1을 뺀 값으로 끝납니다. 내보내기 파일 가져오기 끝점은 `Content-Range` 응답 헤더의 분모로 파일 길이도 보고합니다.

검색이 부분적으로 실패하면 다시 시작할 수 있습니다. 예를 들어 1000바이트 파일을 검색하려고 하지만 처음 725바이트만 수신하는 경우 끝점을 다시 호출하고 새 범위를 전달합니다.

```text
Range: bytes=725-999
```

이 요청은 파일의 나머지 275바이트를 반환합니다.

#### 파일 무결성 확인

`status`이(가) &quot;완료됨&quot;이면 작업 상태 끝점은 `fileChecksum` 특성에 체크섬을 반환합니다. 체크섬은 내보낸 파일의 SHA-256 해시입니다. 검색된 파일의 SHA-256 해시와 비교하여 파일이 완료되었는지 확인합니다.

다음 응답에는 체크섬이 포함됩니다.

```json
{
    "exportId": "45547609-6732-418a-bb7b-17b0160b2317",
    "format": "CSV",
    "status": "Completed",
    "createdAt": "2019-06-04T23:13:12Z",
    "queuedAt": "2019-06-04T23:14:02Z",
    "startedAt": "2019-06-04T23:15:19Z",
    "finishedAt": "2019-06-04T23:36:40Z",
    "numberOfRecords": 1776,
    "fileSize": 400785,
    "fileChecksum": "sha256:83aca1351c9398d2770330e21a9e278880fd2f1eeaf8c8238bf7676d5c21d1c6"
}
```

다음 예제에서는 sha256sum 명령줄 유틸리티를 사용하여 &quot;bulk_lead_export.csv&quot;라는 검색된 파일의 SHA-256 해시를 만듭니다.

```bash
$ sha256sum bulk_lead_export.csv
83aca1351c9398d2770330e21a9e278880fd2f1eeaf8c8238bf7676d5c21d1c6 *bulk_lead_export.csv
```

## 작업 취소

작업이 잘못 구성되었거나 더 이상 필요하지 않으면 취소합니다.

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
         "format": "CSV",
      }
   ]
}
```

응답 상태는 작업이 취소되었음을 나타냅니다.
