---
title: 일괄 프로그램 구성원 가져오기
feature: REST API
description: 멤버 데이터의 일괄 가져오기.
exl-id: b0e1039a-fe9b-4fb7-9aa6-9980a06da673
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 일괄 프로그램 구성원 가져오기

[일괄 프로그램 구성원 가져오기 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members)

대량의 프로그램 구성원 레코드의 경우 [일괄 API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members)를 사용하여 프로그램 구성원을 비동기적으로 가져올 수 있습니다. 이렇게 하면 구분 기호(쉼표, 탭 또는 세미콜론)가 있는 플랫 파일을 사용하여 레코드 목록을 Marketo에 가져올 수 있습니다. 파일 합계가 10MB 미만인 한 파일에는 여러 개의 레코드가 포함될 수 있습니다. 레코드 작업은 &quot;삽입 또는 업데이트&quot;만 가능합니다.

## 처리 제한

제한이 있는 두 개 이상의 일괄 가져오기 요청을 제출할 수 있습니다. 각 요청은 처리할 FIFO 대기열에 작업으로 추가됩니다. 최대 두 개의 작업이 동시에 처리됩니다. 지정된 시간에 큐에 최대 10개의 작업이 허용됩니다(현재 처리 중인 2개 포함). 최대 10개의 작업 수를 초과하면 &quot;1016, 너무 많은 가져오기&quot; 오류가 반환됩니다.

## 파일 가져오기

파일의 첫 번째 행은 각 행의 값을 매핑할 필드로 해당 REST API 이름을 나열하는 헤더여야 합니다. REST API 이름은 [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2) 및/또는 [프로그램 구성원 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeProgramMemberUsingGET) 끝점을 사용하여 검색할 수 있습니다. 레코드에는 리드 필드, 사용자 정의 리드 필드 및 사용자 정의 프로그램 멤버 필드가 포함될 수 있습니다.

일반적인 파일은 다음 기본 패턴을 따릅니다.

```
email,firstName,lastName
test@example.com,John,Doe
```

호출 자체는 `multipart/form-data` 콘텐츠 형식을 사용하여 수행됩니다.

이 요청 유형은 구현하기 어려울 수 있으므로 기존 라이브러리 구현을 사용하는 것이 좋습니다.

## 작업 생성

[프로그램 구성원 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/importProgramMemberUsingPOST) 끝점이 프로그램 구성원 레코드가 포함된 파일을 읽고 지정된 상태의 프로그램에 추가합니다. 레코드에는 리드 필드와 프로그램 멤버 사용자 정의 필드가 모두 포함될 수 있습니다. 모든 레코드에는 중복 제거를 위해 사용되는 이메일 필드가 포함되어야 합니다.

`programId` 경로 매개 변수는 멤버가 추가되는 프로그램을 지정합니다.

세 가지 필수 쿼리 매개 변수가 있습니다. `format` 매개 변수는 가져오기 파일 형식(CSV, TSV 또는 SSV)을 지정하고 `programMemberStatus` 매개 변수는 프로그램에 추가되는 구성원의 프로그램 상태를 지정하며 `file` 매개 변수에는 프로그램 구성원 레코드가 포함된 가져오기 파일의 이름이 들어 있습니다.

```
POST /bulk/v1/program/{programId}/members/import.json?format=csv&programMemberStatus=On List
```

```
Content-Type: multipart/form-data; boundary=--------------------------118046853683028616211319
Content-Length: 772
Host: <munchkinId>.mktorest.com
```

```
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

호출에 대한 응답으로 결과 배열의 레코드에 대한 `batchId` 및 `status` 필드가 있습니다. 이 끝점은 비동기적이므로 큐에 있음, 가져오기 또는 실패 상태를 반환할 수 있습니다. 가져오기 작업의 상태를 가져오고 완료 시 오류 및/또는 경고를 검색하려면 `batchId`을(를) 유지해야 합니다. `batchId`은(는) 7일 동안 유효합니다.

위의 예를 사용하면 명령줄에서 cURL을 사용하여 끝점을 호출하는 간단한 방법이 있습니다.

```bash
curl -i -F format='csv' -F programMemberStatus='On List' -F file='@Lead-House-Lannister.csv' -F access_token='<Access Token>' <REST API Endpoint Base URL>/bulk/v1/program/{programId}/members/import.json
```

가져오기 파일 &quot;Lead-House-Lannister.csv&quot;에 다음이 포함된 경우:

```
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

가져오기 작업이 생성되면 해당 상태를 쿼리해야 합니다. 가져오기 작업을 5-30초마다 폴링하는 것이 가장 좋습니다. 이렇게 하려면 `batchId` 경로 매개 변수를 [가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 끝점에 전달하십시오.

```
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

이 응답은 완료된 가져오기를 표시합니다. 상태는 완료, 대기 중, 가져오기, 실패 중 하나일 수 있습니다.

작업이 완료되면 처리, 실패 또는 경고가 발생한 행 수 목록이 표시됩니다. 메시지 매개변수는 상태가 실패인 경우 실패 메시지를 제공할 수도 있습니다.

## 실패

[가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 응답에서 `numOfRowsFailed` 특성으로 오류가 표시됩니다. numOfRowsFailed가 0보다 크면 해당 값은 발생한 실패 횟수를 나타냅니다.

[가져오기 프로그램 구성원 실패 가져오기](http://TODO) 끝점을 사용하여 `batchId` 경로 매개 변수를 전달하여 실패한 행의 레코드와 원인을 검색합니다.

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

끝점은 레코드가 실패한 이유를 나타내는 메시지와 함께 실패한 행을 나타내는 파일로 응답합니다. 파일 형식은 작업을 만드는 동안 `format` 매개 변수에 지정된 형식과 동일합니다. 각 레코드에 오류에 대한 설명과 함께 추가 필드가 추가됩니다.

예를 들어 리드 점수가 잘못된 다음 파일을 가져오고 있다고 가정해 보겠습니다.

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD
```

작업 상태를 확인하면 오류가 발생했음을 나타내는 `numOfRowsFailed`이(가) 1입니다.

```
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

그런 다음 실패 파일을 검색하여 실패에 대한 추가 세부 정보를 확인하십시오.

```
GET /bulk/v1/program/members/import/{batchId}/failures.json
```

```
firstName,lastName,email,title,company,leadScore,Import Failure Reason
Aerys,Targaryen,Aerys@Targaryen.com,Targaryen,House Targaryen,TEXT_VALUE_IN_INTEGER_FIELD,Invalid data type in field Lead Score
```

## 경고

[가져오기 프로그램 구성원 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberStatusUsingGET) 응답에서 `numOfRowsWithWarning` 특성에 경고가 표시됩니다. `numOfRowsWithWarning`이(가) 0보다 큰 경우 해당 값은 발생한 경고 수를 나타냅니다.

[가져오기 프로그램 구성원 경고 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Program-Members/operation/getImportProgramMemberWarningsUsingGET) 끝점을 사용하여 `batchId` 경로 매개 변수를 전달하여 레코드 및 경고 행 원인을 검색합니다.

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

끝점은 레코드에서 경고를 생성한 이유를 나타내는 메시지와 함께 경고를 생성한 행을 나타내는 파일로 응답합니다. 파일 형식은 작업을 만드는 동안 `format` 매개 변수에 지정된 형식과 동일합니다. 각 레코드에 경고에 대한 설명과 함께 추가 필드가 추가됩니다.

예를 들어 잘못된 이메일 주소를 사용하여 다음 파일을 가져오고 있다고 가정해 보겠습니다.

```
firstName,lastName,email,title,company,leadScore
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0
```

작업 상태를 확인하면 경고가 발생했음을 나타내는 `numOfRowsWithWarning`이(가) 1로 표시됩니다.

```
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

그런 다음 경고에 대한 추가 세부 정보를 보려면 경고 파일을 검색합니다.

```
GET /bulk/v1/program/members/import/{batchId}/warnings.json
```

```
firstName,lastName,email,title,company,leadScore,Import Warning Reason
Aerys,Targaryen,INVALID_EMAIL,Targaryen,House Targaryen,0,Invalid email address
```
