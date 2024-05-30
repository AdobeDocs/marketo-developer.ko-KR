---
title: "대량 사용자 지정 개체 추출"
feature: REST API, Custom Objects
description: "사용자 지정 Marketo 개체를 일괄 처리 중입니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 1%

---


# 대량 사용자 지정 개체 추출

[대량 사용자 지정 개체 추출 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects)

대량 사용자 지정 개체 추출 REST API 세트는 Marketo에서 대량의 사용자 지정 개체 레코드를 검색할 수 있는 프로그래밍 방식 인터페이스를 제공합니다. ETL, 데이터 웨어하우징 및 보관 목적으로 Marketo과 하나 이상의 외부 시스템 간에 데이터를 지속적으로 교환해야 하는 사용 사례에 권장되는 인터페이스입니다.

이 API는 리드에 직접 연결된 첫 번째 수준 Marketo 사용자 지정 개체 레코드 내보내기를 지원합니다. 사용자 지정 개체의 이름과 개체가 연결된 리드 목록을 전달합니다. 목록의 각 리드에 대해 지정된 사용자 지정 개체 이름과 일치하는 연결된 사용자 지정 개체 레코드는 내보내기 파일에 행으로 기록됩니다. 사용자 지정 개체 데이터는 [Marketo UI 내 잠재 고객 세부 정보 페이지의 사용자 지정 개체 탭](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects).

## 권한

대량 사용자 지정 개체 추출 API를 사용하려면 API 사용자에게 &quot;읽기 전용 사용자 지정 개체&quot; 또는 &quot;읽기-쓰기 사용자 지정 개체&quot; 권한 중 하나 또는 둘 다를 가진 역할이 있어야 합니다.

## 필터

사용자 지정 개체 추출은 사용자 지정 개체에 연결된 리드 목록을 지정하는 데 사용되는 여러 필터 옵션을 지원합니다. 목록의 리드가 지정된 사용자 지정 개체 이름과 일치하는 사용자 지정 개체 레코드에 연결되어 있는 경우 해당 레코드는 내보내기 파일에 기록됩니다. 내보내기 작업당 하나의 필터 유형만 지정할 수 있습니다.

| 필터 유형 | 데이터 유형 | 참고 사항 |
|---|---|---|
| `updatedAt` | 날짜 범위 | 멤버가 있는 JSON 개체 수락 `startAt` 및 `endAt` nbsp(&amp;n);`startAt` 에서는 로우 워터마크를 나타내는 날짜/시간을 수락하고 `endAt` 하이 워터마크를 나타내는 날짜/시간을 허용합니다. 범위는 31일 이하여야 합니다. 이 필터 유형의 작업은 날짜 범위 내에서 업데이트된 액세스 가능한 모든 레코드를 반환합니다. 날짜/시간은 밀리초 없이 ISO-8601 형식이어야 합니다. |
| `staticListName` | 문자열 | 정적 목록의 이름을 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 이름을 검색합니다. |
| `staticListId` | 정수 | 정적 목록의 ID를 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 정적 목록의 멤버인 액세스 가능한 모든 레코드를 반환합니다. 목록 가져오기 끝점을 사용하여 정적 목록 ID를 검색합니다. |
| `smartListName`* | 문자열 | 스마트 목록의 이름을 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 스마트 목록의 구성원인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 끝점을 사용하여 스마트 목록 이름을 검색합니다. |
| `smartListId`* | 정수 | 스마트 목록의 ID를 허용합니다. 이 필터 유형의 작업은 작업 처리를 시작할 때 스마트 목록의 구성원인 액세스 가능한 모든 레코드를 반환합니다. 스마트 목록 가져오기 끝점을 사용하여 스마트 목록 ID를 검색합니다. |

일부 구독에서는 필터 유형을 사용할 수 없습니다. 구독에 사용할 수 없는 경우 리드 작업 내보내기 만들기 엔드포인트를 호출할 때 오류가 발생합니다(&quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot;). 고객은 Marketo 지원 센터에 문의하여 구독에서 이 기능을 활성화할 수 있습니다.

## 옵션

다음 [사용자 지정 개체 내보내기 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) endpoint는 몇 가지 서식 옵션을 제공합니다. 이러한 옵션을 통해 사용자는 다음과 같은 작업을 수행할 수 있습니다.

- 내보낸 파일에 포함할 필드 지정
- 이 필드의 열 헤더 이름 바꾸기
- 내보낸 파일의 형식 지정

| 매개 변수 | 데이터 유형 | 필수 | 참고 사항 |
|---|---|---|---|
| `fields` | 배열[문자열] | 예 | 사용자 지정 개체 설명 끝점에서 반환된 사용자 지정 개체 특성 이름의 값이 포함된 문자열 배열입니다. 나열된 필드는 내보낸 파일에 포함됩니다. |
| `columnHeaderNames` | 오브젝트 | 아니요 | 필드 및 열 헤더 이름의 키-값 쌍을 포함하는 JSON 개체입니다. 키는 내보내기 작업에 포함된 필드 이름이어야 합니다. 값은 해당 필드에 대해 내보낸 열 헤더의 이름입니다. |
| `format` | 문자열 | 아니요 | CSV, TSV, SSV 중 하나를 허용합니다. 내보낸 파일은 쉼표로 구분된 값, 탭으로 구분된 값 또는 공백으로 구분된 값 파일로 렌더링됩니다(설정된 경우). 설정하지 않으면 기본값이 CSV로 설정됩니다. |


## 작업 생성

작업에 대한 매개 변수는 를 사용하여 내보내기를 시작하기 전에 정의합니다. [사용자 지정 개체 내보내기 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) 엔드포인트.

필수 `apiName` path 매개 변수는 [사용자 지정 개체 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) 엔드포인트. 내보낼 Marketo 사용자 지정 개체를 지정합니다. CRM 사용자 지정 개체는 허용되지 않습니다. 필수 `filter` 매개 변수에는 사용자 지정 개체에 연결된 잠재 고객 목록이 포함됩니다. 정적 목록 또는 스마트 목록을 참조할 수 있습니다. 필수 `fields` 매개 변수에는 내보내기 파일에 포함할 사용자 지정 개체 속성의 API 이름이 포함됩니다. 필요한 경우 다음을 정의할 수 있습니다. `format` 및 `columnHeaderNames`.

예를 들어 색상, 제조, 모델, VIN 필드가 있는 &quot;Car&quot;이라는 사용자 지정 개체를 만들었다고 가정해 보겠습니다. 링크 필드는 리드 ID이고 중복 제거 필드는 VIN입니다.

사용자 지정 개체 정의

![사용자 지정 개체](assets/custom-object-car.png)


사용자 정의 오브젝트 필드

![사용자 정의 오브젝트 필드](assets/custom-object-car-fields.png)

전화를 할 수 있습니다 [사용자 지정 개체 설명](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/describeUsingGET_1) 에 표시되는 사용자 지정 개체 특성을 프로그래밍 방식으로 검사하려면 `fields` 응답의 속성입니다.

```
GET /rest/v1/customobjects/car_c/describe.json
```

```json
{
    "requestId": "148ef#1793e00f64f",
    "result": [
        {
            "name": "car_c",
            "displayName": "Car",
            "description": "It's a car.",
            "createdAt": "2021-05-05T16:14:41Z",
            "updatedAt": "2021-05-05T16:14:42Z",
            "idField": "marketoGUID",
            "dedupeFields": [
                "vIN"
            ],
            "searchableFields": [
                [
                    "vIN"
                ],
                [
                    "marketoGUID"
                ],
                [
                    "leadID"
                ]
            ],
            "relationships": [
                {
                    "field": "leadID",
                    "type": "child",
                    "relatedTo": {
                        "name": "Lead",
                        "field": "Id"
                    }
                }
            ],
            "fields": [
                {
                    "name": "createdAt",
                    "displayName": "Created At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "marketoGUID",
                    "displayName": "Marketo GUID",
                    "dataType": "string",
                    "length": 36,
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "updatedAt",
                    "displayName": "Updated At",
                    "dataType": "datetime",
                    "updateable": false,
                    "crmManaged": false
                },
                {
                    "name": "color",
                    "displayName": "Color",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "leadID",
                    "displayName": "Lead ID",
                    "dataType": "integer",
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "make",
                    "displayName": "Make",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "model",
                    "displayName": "Model",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                },
                {
                    "name": "vIN",
                    "displayName": "VIN",
                    "dataType": "string",
                    "length": 255,
                    "updateable": true,
                    "crmManaged": false
                }
            ]
        }
    ],
    "success": true
}
```

여러 사용자 지정 개체 레코드를 만들고 다음을 사용하여 각 레코드를 다른 리드에 연결합니다. [사용자 지정 개체 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Custom-Objects/operation/syncCustomObjectsUsingPOST) 엔드포인트. 하나의 리드가 여러 사용자 지정 개체 레코드에 연결될 수 있습니다. 이를 &quot;일대다&quot; 관계라고 합니다.

```
POST /rest/v1/customobjects/car_c.json
```

```json
{
   "action":"createOrUpdate",
   "input":[
       {
           "leadId": 11,
           "color": "Pearl White",
           "make": "Tesla",
           "model": "Model S",
           "vIN": "5YJSA1E41FF156789"
       },
       {
           "leadId": 12,
           "color": "Midnight Silver Metallic",
           "make": "Tesla",
           "model": "Model X",
           "vIN": "LRWXB2B41FF198765"
       },
       {
           "leadId": 13,
           "color": "Fusion Red",
           "make": "Tesla",
           "model": "Roadster",
           "vIN": "SFGRC3C41FF154321"
       }
    ]
}
```

```json
{
    "requestId": "50d9#1793e066088",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "d911eaa1-fd0b-4a99-9b71-c6a7233c782c",
            "status": "created"
        },
        {
            "seq": 1,
            "marketoGUID": "20d04ffb-51f0-4336-924c-c783b9bb4215",
            "status": "created"
        },
        {
            "seq": 2,
            "marketoGUID": "e7da4331-8e7a-473b-85c8-047638eb6c7f",
            "status": "created"
        }
    ],
    "success": true
}
```

위에서 참조된 세 개의 리드 각각은 다음과 같은 &quot;자동차 구매자&quot;라는 정적 목록에 속합니다. `id` 를 호출하여 아래에서 볼 수 있듯이 은 1081입니다. [목록 Id로 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET_1) 엔드포인트.

```
GET /rest/v1/lists/1081/leads.json
```

```json
{
    "requestId": "d023#1793e1e982b",
    "result": [
        {
            "id": 11,
            "firstName": "Hanna",
            "lastName": "Crawford",
            "email": "208161Hanna.Crawford@pookmail.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        },
        {
            "id": 12,
            "firstName": "Bertha",
            "lastName": "Fulton",
            "email": "208160Bertha.Fulton@trashymail.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        },
        {
            "id": 13,
            "firstName": "Faith",
            "lastName": "England",
            "email": "208159Faith.England@dodgit.com",
            "updatedAt": "2020-01-16T02:38:22Z",
            "createdAt": "2017-07-27T01:38:42Z"
        }
    ],
    "success": true
}
```

이제 이러한 레코드를 검색하는 내보내기 작업을 만들겠습니다. 사용 [사용자 지정 개체 내보내기 작업 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/createExportCustomObjectsUsingPOST) 엔드포인트에서 사용자 지정 개체 속성을 `fields` 매개 변수 및 의 정적 목록 id `filter` 매개 변수.

```
POST /bulk/v1/customobjects/car_c/export/create.json
```

```json
{
    "fields": [
        "leadId",
        "color",
        "make",
        "model",
        "vIN"
    ],
    "filter": {
        "staticListId": 1081
    }
}
```

```json
{
    "requestId": "8d2f#1793e289e87",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Created",
            "createdAt": "2021-05-05T20:12:01Z"
        }
    ],
    "success": true
}
```

작업이 생성되었음을 나타내는 상태가 응답에 반환됩니다. 작업이 정의되고 생성되었지만 아직 시작되지 않았습니다. 이렇게 하려면 [사용자 지정 개체 내보내기 작업 큐에 넣기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/enqueueExportCustomObjectsUsingPOST) 끝점은 다음을 사용하여 호출해야 합니다. `apiName`및 `exportId` 만들기 상태 응답에서

```
POST /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/enqueue.json
```

```json
{
    "requestId": "cfaf#1793e2a0762",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Queued",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z"
        }
    ],
    "success": true
}
```

이 경우 이니셜로 응답합니다. `status` 사용 가능한 내보내기 슬롯이 있는 경우 그 이후에 &quot;처리 중&quot;으로 설정됩니다.

## 폴링 작업 상태

동일한 API 사용자가 만든 작업에 대해서만 상태를 검색할 수 있습니다.

비동기 끝점이므로 작업을 만든 후 상태를 폴링하여 진행률을 확인해야 합니다. 을(를) 사용하여 투표 [내보내기 사용자 지정 개체 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsStatusUsingGET) 엔드포인트. 상태는 60초마다 한 번만 업데이트되므로 이보다 낮은 폴링 빈도는 권장되지 않으며 거의 모든 경우에 여전히 과도합니다. 상태 필드는 생성됨, 대기 중, 처리 중, 취소됨, 완료됨 또는 실패 중 하나로 응답할 수 있습니다.

```
GET /bulk/v1/customobjects/{apiName}/export/{exportId}/status.json
```

```json
{
    "requestId": "14daa#1793e2cf9de",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z",
            "startedAt": "2021-05-05T20:14:15Z"
        }
    ],
    "success": true
}
```

상태 끝점은 작업이 아직 처리 중이므로 파일을 검색할 수 없다는 것을 나타냅니다. 작업 한 번 `status` &quot;완료됨&quot;에 대한 변경 사항을 다운로드할 수 있습니다.

```json
{
    "requestId": "14daa#1793e2cf9de",
    "result": [
        {
            "exportId": "f2c03f1d-226f-47c1-a557-357af8c2b32a",
            "format": "CSV",
            "status": "Completed",
            "createdAt": "2021-05-05T20:12:01Z",
            "queuedAt": "2021-05-05T20:13:32Z",
            "startedAt": "2021-05-05T20:14:15Z",
            "finishedAt": "2021-05-05T20:14:28Z",
            "numberOfRecords": 3,
            "fileSize": 182,
            "fileChecksum": "sha256:fac0cabc2352229c12e18b2fde03d1f24178bc71e9e926f520ae8d61bbe98c01"
        }
    ],
    "success": true
}
```

## 데이터 검색 중

완료된 사용자 지정 개체 내보내기의 파일을 검색하려면 [내보내기 사용자 지정 개체 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingGET) 엔드포인트 `apiName` 및 `exportId`.

응답에는 작업이 구성된 방식으로 포맷된 파일이 포함됩니다. 끝점이 파일의 내용에 응답합니다. 요청한 사용자 지정 개체 속성이 비어 있으면(데이터 없음) `null` 는 내보내기 파일의 해당 필드에 배치됩니다.

```
GET /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/file.json
```

```csv
leadId,color,make,model,vIN
11,Pearl White,Tesla,Model S,5YJSA1E41FF156789
12,Midnight Silver Metallic,Tesla,Model X,LRWXB2B41FF198765
13,Fusion Red,Tesla,Roadster,SFGRC3C41FF154321
```

추출된 데이터의 부분 검색 및 재시작 친화성을 지원하기 위해 파일 엔드포인트는 선택적으로 바이트 유형의 HTTP 헤더 범위를 지원합니다. 헤더가 설정되지 않은 경우 전체 콘텐츠가 반환됩니다. Marketo에서 범위 헤더 사용에 대한 자세한 내용을 볼 수 있습니다 [일괄 추출](bulk-extract.md).

## 작업 취소

작업이 잘못 구성되었거나 필요하지 않은 경우 를 사용하여 쉽게 취소할 수 있습니다. [사용자 지정 개체 내보내기 작업 취소](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Custom-Objects/operation/getExportCustomObjectsFileUsingPOST) 엔드포인트. 다음으로 응답함: `status` 작업이 취소되었음을 나타냅니다.

```
POST /bulk/v1/customobjects/car_c/export/f2c03f1d-226f-47c1-a557-357af8c2b32a/cancel.json
```

```json
{
    "requestId": "e5f9#179391286a7",
    "result": [
        {
            "exportId": "4a8cdd80-0d16-4dd6-9923-6ec97e30e91b",
            "format": "CSV",
            "status": "Cancelled",
            "createdAt": "2021-05-04T20:24:33Z"
        }
    ],
    "success": true
}
```
