---
title: 벌크 리드 가져오기
feature: REST API
description: CSV TSV 또는 SSV를 사용하여 Marketo에서 비동기 대량 리드 가져오기를 만들고 모니터링합니다.
exl-id: 615f158b-35f9-425a-b568-0a7041262504
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# 벌크 리드 가져오기

[잠재 고객 가져오기 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads)

많은 양의 잠재 고객 레코드의 경우 [bulk API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads/operation/importLeadUsingPOST)를 사용하여 비동기적으로 잠재 고객을 가져올 수 있습니다. 이렇게 하면 구분 기호(쉼표, 탭 또는 세미콜론)가 있는 플랫 파일을 사용하여 레코드 목록을 Marketo에 가져올 수 있습니다. 파일 합계가 10MB 미만인 한 파일에는 여러 개의 레코드가 포함될 수 있습니다. 레코드 작업은 &quot;삽입 또는 업데이트&quot;만 가능합니다.

## 처리 제한

제한이 있는 두 개 이상의 일괄 가져오기 요청을 제출할 수 있습니다. 각 요청은 처리할 FIFO 대기열에 작업으로 추가됩니다. 최대 두 개의 작업이 동시에 처리됩니다. 지정된 시간에 큐에 최대 10개의 작업이 허용됩니다(현재 처리 중인 2개 포함). 최대 10개의 작업 수를 초과하면 &quot;1016, 너무 많은 가져오기&quot; 오류가 반환됩니다.

## 파일 가져오기

파일의 첫 번째 행은 각 행의 값을 로 매핑할 해당 REST API 필드를 나열하는 헤더여야 합니다. 일반적인 파일은 다음 기본 패턴을 따릅니다.

```
email,firstName,lastName
test@example.com,John,Doe
```

`externalCompanyId` 필드는 잠재 고객 레코드를 회사 레코드에 연결하는 데 사용할 수 있습니다. `externalSalesPersonId` 필드는 잠재 고객 레코드를 영업 사원 레코드에 연결하는 데 사용할 수 있습니다.

호출 자체는 `multipart/form-data` 콘텐츠 형식을 사용하여 수행됩니다.

이 요청 유형은 구현하기 어려울 수 있으므로 기존 라이브러리 구현을 사용하는 것이 좋습니다.

## 작업 생성

일괄 가져오기 요청을 수행하려면 콘텐츠 유형 헤더를 &quot;multipart/form-data&quot;로 설정하고 파일 콘텐츠가 있는 파일 매개 변수와 파일 형식을 나타내는 &quot;csv&quot;, &quot;tsv&quot; 또는 &quot;ssv&quot; 값이 있는 형식 매개 변수를 적어도 포함해야 합니다.

```
POST /bulk/v1/leads.json?format=csv
```

```
Content-Type: multipart/form-data; boundary=------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Length: 311
Host: <munchkinId>.mktorest.com
```

```
------WebKitFormBoundaryBQACkJZyaiIAXogC
Content-Disposition: form-data; name="file"; filename="leads.csv"
Content-Type: text/csv

FirstName,LastName,Email,Company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
------WebKitFormBoundaryBQACkJZyaiIAXogC--
```

```json
{
    "requestId": "d01f#15d672f8560",
    "result": [
        {
            "batchId": 3404,
            "importId": "3404",
            "status": "Queued"
        }
    ],
    "success": true
}
```

이 끝점은 [multipart/form-data를 content-type](https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html)&#x200B;(으)로 사용합니다. 이 방법은 올바른 이해에 까다로울 수 있으므로 가장 좋은 방법은 선택한 언어에 HTTP 지원 라이브러리를 사용하는 것입니다. 명령줄에서 cURL을 사용하여 이 작업을 수행하는 간단한 방법은 다음과 같습니다.

```
curl -i -F format=csv -F file=@lead_data.csv -F access_token=<Access Token> <REST API Endpoint Base URL>/bulk/v1/leads.json
```

가져오기 파일 &quot;lead_data.csv&quot;에 다음이 포함된 경우:

```
FirstName,LastName,Email,Company
Able,Baker,ablebaker@marketo.com,Marketo
Charlie,Dog,charliedog@marketo.com,Marketo
Easy,Fox,easyfox@marketo.com,Marketo
```

요청에 `lookupField`, `listId` 및 `partitionName` 매개 변수를 선택적으로 포함할 수도 있습니다. `lookupField`을(를) 사용하면 동기화 리드와 마찬가지로 중복을 제거할 특정 필드를 선택할 수 있으며 기본값은 이메일입니다. `id`을(를) `lookupField`(으)로 지정하여 &quot;업데이트 전용&quot; 작업을 표시할 수 있습니다. `listId`을(를) 사용하면 잠재 고객 목록을 가져올 정적 목록을 선택할 수 있습니다. 이렇게 하면 가져오기로 인해 만들어진 항목 또는 업데이트뿐만 아니라 목록의 잠재 고객이 이 정적 목록의 구성원이 됩니다. `partitionName`이(가) 가져올 특정 파티션을 선택합니다. 자세한 내용은 작업 공간 및 파티션 섹션을 참조하십시오.

호출에 대한 응답으로 동기화 리드와 같은 성공 또는 실패 목록이 아니라 결과 배열에 있는 레코드에 대한 batchId 및 상태 필드가 있다는 것을 확인합니다. 이는 이 API는 비동기적으로 수행되며 큐에 있음, 가져오기 또는 실패 상태를 반환할 수 있기 때문입니다. 가져오기 작업의 상태를 가져오고 완료 시 실패 및/또는 경고를 검색하려면 batchId를 유지해야 합니다. batchId는 7일 동안 유효합니다.

## 폴링 작업 상태

가져오기 작업의 상태를 보려면 필요한 지연 시간 및 API 호출 제한에 따라 5~30초마다 작업을 폴링하는 것이 좋습니다. 가져오기 리드 상태 가져오기 API를 사용하여 이 작업을 수행할 수 있습니다.

```
GET /bulk/v1/leads/batch/{id}.json
```

```json
{
   "requestId":"8136#146daebc2ed",
   "success":true,
   "result":[
      {
         "batchId":1022,
         "status":"Complete",
         "numOfLeadsProcessed":2,
         "numOfRowsFailed":1,
         "numOfRowsWithWarning":0,
         "message":"Import completed with errors, 2 records imported (2 members), 1 failed"
      }
   ]
}
```

이 응답은 완료된 가져오기를 표시하지만 상태는 다음 중 하나일 수 있습니다.

- 완료
- 대기열에 추가됨
- 가져오는 중
- 실패

작업이 완료되면 처리된 행 수, 실패한 행 수, 경고가 있는 행 수 목록이 표시됩니다. 메시지 매개변수는 상태가 실패인 경우 실패 메시지를 제공할 수도 있습니다.

## 실패

실패는 가져오기 리드 상태 가져오기 응답에서 &quot;numOfRowsFailed&quot; 속성으로 표시됩니다. numOfRowsFailed가 0보다 크면 이 값은 발생한 실패 횟수를 나타냅니다.

실패한 행의 레코드와 원인을 검색하려면 실패 파일을 검색해야 합니다.

```
GET /bulk/v1/leads/batch/{id}/failures.json
```

API는 레코드가 실패한 이유를 나타내는 메시지와 함께 실패한 행을 나타내는 파일로 응답합니다. 파일 형식은 작업을 만드는 동안 &quot;format&quot; 매개 변수에 지정된 형식과 동일합니다. 각 레코드에 오류에 대한 설명과 함께 추가 필드가 추가됩니다.

## 경고

경고는 가져오기 리드 상태 가져오기 응답에서 &quot;numOfRowsWithWarning&quot; 속성으로 표시됩니다. &quot;numOfRowsWithWarning&quot;이 0보다 큰 경우 해당 값은 발생한 경고 수를 나타냅니다.

경고 행의 레코드와 원인을 검색하려면 다음과 같이 하십시오.

```
GET /bulk/v1/leads/batch/{id}/warnings.json
```

API는 레코드가 실패한 이유를 나타내는 메시지와 함께 경고를 생성한 행을 나타내는 파일로 응답합니다. 파일 형식은 작업을 만드는 동안 &quot;format&quot; 매개 변수에 지정된 형식과 동일합니다. 각 레코드에 경고에 대한 설명과 함께 추가 필드가 추가됩니다.
