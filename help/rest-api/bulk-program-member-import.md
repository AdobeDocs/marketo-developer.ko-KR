---
title: 일괄 프로그램 구성원 가져오기
feature: REST API
description: 10MB 이하의 CSV TSV 또는 SSV 파일을 사용하여 Marketo REST API를 통해 프로그램 구성원을 일괄로 가져오는 방법, 큐 제한, 필수 매개 변수 및 폴링 작업 상태에 대해 알아봅니다.
exl-id: b0e1039a-fe9b-4fb7-9aa6-9980a06da673
TQID: https://experienceleague.adobe.com/T1PAzLN1mnp38kJ0jwh6kPv6r1Uvxc7-o9zeTHetIV0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 771
ht-degree: 0%

---

# 일괄 프로그램 구성원 가져오기

[벌크 프로그램 멤버 가져오기 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members)

[일괄 API](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members)를 사용하여 많은 수의 프로그램 구성원 레코드를 비동기적으로 가져옵니다. 쉼표, 탭 또는 세미콜론으로 구분된 10MB 미만의 플랫 파일로 레코드를 제공합니다.

일괄 프로그램 멤버 가져오기는 &quot;삽입 또는 업데이트&quot; 레코드 작업만 지원합니다.

## 처리 제한

각 벌크 가져오기 요청은 선입선출(FIFO) 큐에 작업으로 추가됩니다. 다음과 같은 제한이 적용됩니다.

- 최대 두 개의 작업을 동시에 처리할 수 있습니다.
- 처리 중인 두 작업을 포함하여 최대 10개의 작업이 대기열에 있을 수 있습니다.

최대 작업 10개를 초과하면 API에서 `1016, Too many imports` 오류를 반환합니다.

## 파일 가져오기

파일의 첫 행은 각 행의 값이 매핑되는 REST API 필드 이름을 나열하는 헤더여야 합니다. [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeUsingGET_2) 및 [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi#tag/Leads/operation/describeProgramMemberUsingGET) 끝점을 사용하여 이러한 이름을 검색합니다.

레코드에는 리드 필드, 사용자 정의 리드 필드 및 사용자 정의 프로그램 멤버 필드가 포함될 수 있습니다.

일반적인 파일은 다음 패턴을 따릅니다.

```text
email,firstName,lastName
test@example.com,John,Doe
```

`multipart/form-data` 콘텐츠 형식을 사용하여 요청을 보냅니다. 기존 라이브러리 구현을 사용하여 다중 파트 요청을 구성합니다.

## 작업 생성

[프로그램 구성원 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/importProgramMemberUsingPOST) 끝점이 파일에서 프로그램 구성원 레코드를 읽고 지정된 상태의 프로그램에 추가합니다. 레코드에는 리드 필드와 사용자 지정 프로그램 구성원 필드가 포함될 수 있습니다.

모든 레코드에는 중복 제거에 사용되는 이메일 필드가 포함되어야 합니다.

`programId` 경로 매개 변수는 멤버가 추가되는 프로그램을 지정합니다.

요청에는 세 개의 쿼리 매개 변수가 필요합니다.

- `format`: 가져오기 파일 형식(`CSV`, `TSV` 또는 `SSV`)입니다.
- `programMemberStatus`: 가져온 구성원에 할당된 프로그램 상태입니다.
- `file`: 프로그램 구성원 레코드가 포함된 파일의 이름입니다.

```http
POST /bulk/v1/program/{programId}/members/import.json?format=csv&programMemberStatus=On List
```

```text
Content-Type: multipart/form-data; boundary=--------------------------118046853683028616211319
Content-Length: 772
Host: <munchkinId>.mktorest.com
```

```text
----------------------------118046853683028616211319
Content-Disposition: form-data; name="file"; filename="Lead-House-Lannister.csv"
Content-Type: text/csv

firstName,lastName,email,title,company,leadScore
Joanna,Lannister,Joanna@Lannister.com,Lannister,House Lannister,0
Tywin,Lannister,Tywin@Lannister.com,Lannister,House Lannister,0
Cersei,Lannister,Cersei@Lannister.com,Lannister,House Lannister,0
Jamie,Lannister,Jamie@Lannister.com,Lannister,House Lannister,0
Tyrion,Lannister,Tyrion@Lannister.com,Lannister,House Lannister,0
Kevan,Lannister,Kevan@Lannister.com,Lannister,House Lannister,0
Dorna,Lannister,Dorna@Lannister.com,Lannister,House Lannister,0
Lancel,Lannister,Lancel@Lannister.com,Lannister,House Lannister,0

----------------------------118046853683028616211319--
```

```json
{
    "requestId": "17f4a#16f87f87325",
    "result": [
        {
            "batchId": 1040,
            "importId": "1040",
            "status": "Queued"
        }
    ],
    "success": true
}
```

끝점이 비동기적이므로 응답에 `batchId` 및 `status` 필드가 포함되어 있습니다. 상태는 `Queued`, `Importing` 또는 `Failed`일 수 있습니다.

가져오기 상태를 확인하고 완료 후 오류 또는 경고를 검색하려면 `batchId`을(를) 유지합니다. `batchId`은(는) 7일 동안 유효합니다.

다음 명령줄 cURL 요청은 예제 작업을 제출합니다.

```bash
curl -i -F format='csv' -F programMemberStatus='On List' -F file='@Lead-House-Lannister.csv' -F access_token='<Access Token>' <REST API Endpoint Base URL>/bulk/v1/program/{programId}/members/import.json
```

이 예제에서 `Lead-House-Lannister.csv` 가져오기 파일에는 다음 데이터가 포함되어 있습니다.

```text
firstName,lastName,email,title,company,leadScore
Joanna,Lannister,Joanna@Lannister.com,Lannister,House Lannister,0
Tywin,Lannister,Tywin@Lannister.com,Lannister,House Lannister,0
Cersei,Lannister,Cersei@Lannister.com,Lannister,House Lannister,0
Jamie,Lannister,Jamie@Lannister.com,Lannister,House Lannister,0
Tyrion,Lannister,Tyrion@Lannister.com,Lannister,House Lannister,0
Kevan,Lannister,Kevan@Lannister.com,Lannister,House Lannister,0
Dorna,Lannister,Dorna@Lannister.com,Lannister,House Lannister,0
Lancel,Lannister,Lancel@Lannister.com,Lannister,House Lannister,0
```

## 폴링 작업 상태

가져오기 작업을 만든 후 5~30초마다 폴링합니다. `batchId` 경로 매개 변수를 [가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 끝점에 전달합니다.

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
    "requestId": "e0cb#16f87f8b177",
    "result": [
        {
            "batchId": 1040,
            "importId": "1040",
            "status": "Complete",
            "numOfLeadsProcessed": 8,
            "numOfRowsFailed": 0,
            "numOfRowsWithWarning": 0,
            "message": "Import succeeded, 8 records imported (8 members)"
        }
    ],
    "success": true
}
```

이 응답은 완료된 가져오기를 표시합니다. 상태는 `Complete`, `Queued`, `Importing` 또는 `Failed`일 수 있습니다.

작업이 완료되면 응답에는 처리, 실패 및 처리된 행 수가 경고와 함께 나열됩니다. 상태가 `Failed`인 경우 `message` 매개 변수가 오류 메시지를 제공할 수도 있습니다.

## 실패

[가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 응답의 `numOfRowsFailed` 특성은 실패한 행 수를 나타냅니다. 값이 0보다 크면 오류가 발생했음을 의미합니다.

`batchId` 경로 매개 변수를 가져오기 프로그램 멤버 실패 가져오기 끝점에 전달하여 실패한 레코드 및 원인을 검색합니다.

```http
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

끝점은 실패한 각 행을 식별하고 레코드가 실패한 이유를 설명하는 파일을 반환합니다. 파일이 작업을 만드는 동안 `format` 매개 변수로 지정된 형식을 사용합니다. 각 레코드의 추가 필드는 오류를 설명합니다.

예를 들어 리드 점수가 잘못된 다음 파일을 가져오고 있다고 가정해 보겠습니다.

```text
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD
```

작업 상태가 `numOfRowsFailed`을(를) 1로 반환하여 오류가 발생했음을 나타냅니다.

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
    "requestId": "4c2d#16f8b32c8ef",
    "result": [
        {
            "batchId": 1046,
            "importId": "1046",
            "status": "Complete",
            "numOfLeadsProcessed": 0,
            "numOfRowsFailed": 1,
            "numOfRowsWithWarning": 0,
            "message": "Import completed with errors, 0 records imported (0 members), 1 failed"
        }
    ],
    "success": true
}
```

자세한 내용은 오류 파일을 참조하십시오.

```http
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

```text
firstName,lastName,email,title,company,leadScore,Import Failure Reason
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD,Invalid data type in field Lead Score
```

## 경고

[가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 응답의 `numOfRowsWithWarning` 특성은 경고가 있는 행 수를 나타냅니다. 값이 0보다 크면 경고가 발생한 것입니다.

`batchId` 경로 매개 변수를 [가져오기 프로그램 구성원 경고 가져오기](https://developer.adobe.com/marketo-apis/api/mapi#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberWarningsUsingGET) 끝점에 전달하여 영향을 받는 레코드와 그 원인을 검색합니다.

```http
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

끝점은 경고가 있는 각 행을 식별하고 경고가 발생한 이유를 설명하는 파일을 반환합니다. 파일이 작업을 만드는 동안 `format` 매개 변수로 지정된 형식을 사용합니다. 각 레코드의 추가 필드는 경고를 설명합니다.

예를 들어 잘못된 이메일 주소를 사용하여 다음 파일을 가져오고 있다고 가정해 보겠습니다.

```text
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0
```

작업 상태가 경고가 발생했음을 나타내는 `numOfRowsWithWarning`을(를) 1로 반환합니다.

```http
GET /bulk/v1/program/members/import/{batchId}/status.json
```

```json
{
   "requestId":"4ca1#16f883c2003",
   "result":[
      {
         "batchId":1041,
         "importId":"1041",
         "status":"Complete",
         "numOfLeadsProcessed":1,
         "numOfRowsFailed":0,
         "numOfRowsWithWarning":1,
         "message":"Import succeeded, 1 records imported (1 members), 1 warning."
      }
   ],
   "success":true
}
```

자세한 내용은 경고 파일을 참조하십시오.

```http
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

```text
firstName,lastName,email,title,company,leadScore,Import Warning Reason
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0,Invalid email address
```
