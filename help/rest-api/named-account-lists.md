---
title: 명명된 계정 목록
feature: REST API
description: 쿼리, 만들기, 업데이트 및 삭제를 위한 권한, 필드, 필터링 및 엔드포인트를 포함하여 REST API를 사용하여 Marketo 명명된 계정 목록을 관리하는 방법을 알아봅니다.
exl-id: 98f42780-8329-42fb-9cd8-58e5dbea3809
TQID: https://experienceleague.adobe.com/18lMhheW21Gz1-3TMHwleHhmLTOqJsZSQ5aqkbbchhM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2:
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 686
ht-degree: 2%

---

# 명명된 계정 목록

[명명된 계정 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi#tag/Named-Account-Lists)

[명명된 계정 목록](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/target-account-management/target/account-lists)은(는) Marketo의 명명된 계정 컬렉션입니다. 분류, 데이터 보강 및 스마트 캠페인 필터링에 사용합니다.

명명된 계정 목록 API를 사용하여 목록 에셋과 해당 멤버십을 원격으로 관리할 수 있습니다.
`Content`

## 권한

필요한 권한은 작업에 따라 다릅니다.

- 명명된 계정 목록 쿼리: 읽기 전용 명명된 계정 목록 또는 명명된 계정 목록 읽기-쓰기.
- 목록 만들기, 업데이트 또는 삭제: 명명된 계정 목록 읽기-쓰기.
- 쿼리 목록 멤버십: 읽기 전용 명명된 계정 또는 읽기-쓰기 명명된 계정입니다.
- 목록 멤버십 관리: 명명된 계정을 읽기-씁니다.

## 모델

명명된 계정 목록에는 제한된 표준 필드 세트가 있으며 사용자 지정 필드를 지원하지 않습니다.
`Named Account List Field`

| 이름 | 데이터 유형 | 업데이트 가능 | 참고 |
| --- | --- | --- | --- |
| marketoGUID | 문자열 | False | 명명된 계정 목록의 고유 문자열 식별자입니다. 이 필드는 시스템에서 관리되며 레코드를 만들 때 필드로 허용되지 않습니다. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;idField&quot;에서 사용하는 필드. |
| 이름 | 문자열 | True | 목록 이름. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;dedupeFields&quot;에서 사용하는 필드. |
| createdAt | 날짜/시간 | False | 목록 작성의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| updatedAt | 날짜/시간 | False | 목록에 대한 최신 업데이트의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| 유형 | 문자열 | False | 목록 유형. 값은 &quot;default&quot; 또는 &quot;external&quot;일 수 있습니다. 외부 목록은 CRM 계정 보기에서 만든 목록입니다. |

## 쿼리

명명된 계정 목록 쿼리는 &quot;dedupeFields&quot;와 &quot;idField&quot;라는 두 가지 filterType을 지원합니다. `filterType` 쿼리 매개 변수에서 필드를 설정하고 `filterValues as`의 값을 쉼표로 구분된 목록으로 제공하십시오.

`nextPageToken` 및 `batchSize` 필터는 선택 사항입니다.

```http
GET /rest/v1/namedAccountLists.json?filterType=idField&filterValues=dff23271-f996-47d7-984f-f2676861b5fb,dff23271-f996-47d7-984f-f2676861b5fc
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "name": "Saas List",
         "createdAt": "xxxxxxxx",
         "updatedAt": "xxxxxxxx",
         "type": "default",
         "updateable": true
      },
      {
         "seq": 1,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc",
         "name": "My Account List",
         "createdAt": "xxxxxxxx",
         "updatedAt": "xxxxxxxx",
         "type": "default",
         "updateable": true
      }
   ]
}
```

## 만들기 및 업데이트

표준 리드 데이터베이스 패턴을 사용하여 명명된 계정 목록 레코드를 만들고 업데이트합니다. 명명된 계정 목록에는 업데이트할 수 있는 필드가 하나만 있습니다. `name`.

끝점은 &quot;createOnly&quot;와 &quot;updateOnly&quot;의 두 가지 표준 작업 유형을 지원합니다. `action defaults`에서 &quot;createOnly&quot;로 변경되었습니다.

작업이 `updateOnly`인 경우 선택적 `dedupeBy parameter`을(를) 지정할 수 있습니다. 허용되는 값은 &quot;name&quot;에 해당하는 &quot;dedupeFields&quot;와 &quot;marketoGUID&quot;에 해당하는 &quot;idField&quot;입니다.

`createOnly` 모드에서는 &quot;name&quot;만 `dedupeBy` 필드로 허용됩니다. 한 번에 최대 300개의 레코드를 제출할 수 있습니다.

```http
POST /rest/v1/namedAccountLists.json
```

```json
{
   "action": "createOnly",
   "dedupeBy": "dedupeFields",
   "input": [
      {
         "name": "SAAS List"
      },
      {
         "name": "Manufacturing (Domestic)"
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "status": "created",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
      },
      {
         "seq": 1,
         "status": "created",
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc"
      }
   ]
}
```

## 삭제

목록의 `name` 또는 `marketoGUID`을(를) 사용하여 명명된 계정 목록을 삭제합니다. 키를 선택하려면 요청의 `deleteB` 멤버에서 이름에 &quot;dedupeFields&quot; 또는 marketoGUID에 &quot;idField&quot;를 전달하십시오.

설정하지 않으면 기본값은 dedupeFields로 설정됩니다. 한 번에 최대 300개의 레코드를 삭제할 수 있습니다.

```http
POST /rest/v1/namedAccountLists/delete.json
```

```json
{
   "deleteBy": "dedupeFields",
   "input": [
      {
         "name": "Saas List"
      },
      {
         "name": "B2C List"
      },
      {
         "name": "Launchpoint Partner List"
      }
   ]
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "status": "deleted"
      },
      {
         "seq": 1,
         "id": "dff23271-f996-47d7-984f-f2676861b5fc",
         "status": "deleted"
      },
      {
         "seq": 2,
         "status": "skipped",
         "reasons": [
            {
               "code": "1013",
               "message": "Record not found"
            }
         ]
      }
   ]
}
```

키에 대한 레코드를 찾을 수 없는 경우 해당 결과 항목의 `status`은(는) &quot;건너뜀&quot;입니다. 또한 실패를 설명하는 코드와 메시지에 원인이 포함됩니다.

## 멤버십 관리

### 쿼리 멤버십

계정 목록의 `i`을(를) 제공하여 이름이 지정된 계정 목록 구성원을 쿼리합니다. 선택적 매개 변수는 다음과 같습니다.

-`field` - 응답 레코드에 포함할 쉼표로 구분된 필드 목록
-`nextPageToke` - 결과 집합을 통해 페이징용
-`batchSiz` - 반환할 레코드 수를 지정합니다.

`field`이(가) 설정되지 않으면 `marketoGUI`,`nam`, `createdA` 및`updatedA`이(가) 반환됩니다. `batchSiz`의 최대 및 기본값은 300입니다.

```http
GET /rest/v1/namedAccountList/{id}/namedAccounts.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "seq": 0,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
         "name": "Saas List",
         "createdAt": "2017-02-01T00:00:00Z",
         "updatedAt": "2017-03-05T17:21:15Z"
      },
      {
         "seq": 1,
         "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fc",
         "name": "My Account List",
         "createdAt": "2017-02-01T00:00:00Z",
         "updatedAt": "2017-03-05T17:21:15Z"
      }
   ]
}
```

### 구성원 추가

marketoGUID를 사용하여 명명된 계정을 명명된 계정 목록에 추가합니다. 한 번에 최대 300개의 레코드를 추가할 수 있습니다.

```http
POST /rest/v1/namedAccountList/{id}/namedAccounts.json
```

```json
{
    "input": [
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        },
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        }
    ]
}
```

```json
{
    "requestId": "string",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        },
        {
            "seq": 1,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        }
    ],
    "success": true,
}
```

### 멤버 제거

계정 목록에서 레코드를 제거하면 다른 경로가 사용되지만 동일한 인터페이스가 사용됩니다. 제거할 각 레코드에 대해 `marketoGUI`을(를) 제공하십시오. 한 번에 최대 300개의 레코드를 제거할 수 있습니다.

```http
POST /rest/v1/namedAccountList/{id}/namedAccounts/remove.json
```

```json
{
    "input": [
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        },
        {
             "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb"
        }
    ]
}
```

```json
{
    "requestId": "string",
    "result": [
        {
            "seq": 0,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        },
        {
            "seq": 1,
            "marketoGUID": "dff23271-f996-47d7-984f-f2676861b5fb",
            "status": "added"
        }
    ],
    "success": true
}
```

## 시간 초과

- 명명된 계정 목록 엔드포인트의 시간 제한은 별도로 명시되지 않는 한 30초입니다.
- 이름이 지정된 계정 목록 동기화에 60초의 시간 제한이 있습니다.
- 명명된 계정 목록 삭제의 시간 제한은 60초입니다.
- 명명된 계정 목록 가져오기의 시간 제한은 60초입니다.
- 명명된 계정 목록 구성원 추가의 시간 제한은 60초입니다.
- 명명된 계정 목록 구성원 제거의 시간 제한은 60초입니다.
- 명명된 계정 목록 구성원 가져오기의 시간 제한은 60초입니다.
