---
title: "명명된 계정 목록"
feature: REST API
description: "명명된 계정 목록을 구성합니다."
source-git-commit: 8c1ffb6db05da49e7377b8345eeb30472ad9b78b
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---


# 명명된 계정 목록

[명명된 계정 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Account-Lists)

[명명된 계정 목록](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/target-account-management/target/account-lists) Marketo에서 는 명명된 계정의 컬렉션을 나타냅니다. 분류, 데이터 보강 및 스마트 캠페인 필터링을 포함하여 다양한 경우에 사용할 수 있습니다. 명명된 계정 목록 API를 사용하면 이러한 목록 에셋과 해당 멤버십을 원격으로 관리할 수 있습니다.
`Content`

## 권한

명명된 계정 목록을 쿼리하려면 읽기 전용 명명된 계정 목록 또는 읽기-쓰기 명명된 계정 목록 권한이 필요합니다. 목록을 만들거나 업데이트하거나 삭제하려면 명명된 계정 목록 읽기-쓰기 권한이 필요합니다. 목록 구성원을 쿼리하려면 읽기 전용 이름 지정 계정 또는 읽기-쓰기 이름 지정 계정 권한이 필요하며 구성원 자격을 관리하려면 읽기-쓰기 이름 지정 계정 권한이 필요합니다.

## 모델

명명된 계정 목록에는 제한된 수의 표준 필드가 있으며 사용자 지정 필드로 확장할 수 없습니다.
`Named Account List Field`

| 이름 | 데이터 유형 | 업데이트 가능 | 참고 사항 |
|---|---|---|---|
| marketoGUID | 문자열 | 거짓 | 명명된 계정 목록의 고유 문자열 식별자입니다. 이 필드는 시스템에서 관리되며 레코드를 만들 때 필드로 허용되지 않습니다. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;idField&quot;에서 사용하는 필드. |
| 이름 | 문자열 | 참 | 목록 이름. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;dedupeFields&quot;에서 사용하는 필드. |
| createdAt | 날짜/시간 | 거짓 | 목록 작성의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| updatedAt | 날짜/시간 | 거짓 | 목록에 대한 최신 업데이트의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| 유형 | 문자열 | 거짓 | 목록 유형. 값은 &quot;default&quot; 또는 &quot;external&quot;일 수 있습니다. 외부 목록은 CRM 계정 보기에서 만든 목록입니다. |


## 쿼리

계정 목록 쿼리는 간단하고 쉽습니다. 현재 명명된 계정 목록을 쿼리하기 위해 유효한 filterType은 &quot;dedupeFields&quot;와 &quot;idField&quot;뿐입니다. 필터링할 필드가 다음에 설정됨 `filterType` 쿼리의 매개 변수와 값이 `filterValues as` 쉼표로 구분된 목록입니다. 다음 `nextPageToken` 및 `batchSize` 필터는 또한 선택적 매개 변수입니다.

```
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

명명 계정 목록 레코드를 생성하고 갱신하면 다른 리드 데이터베이스 생성 및 갱신 작업에 대해 설정된 패턴을 따릅니다. 명명된 계정 목록에는 업데이트할 수 있는 필드가 하나만 있습니다. `name`.

끝점은 &quot;createOnly&quot;와 &quot;updateOnly&quot;의 두 가지 표준 작업 유형을 허용합니다.  다음 `action defaults` to &quot;createOnly.&quot;

선택 사항 `dedupeBy parameter` 작업이 인 경우 지정할 수 있습니다. `updateOnly`.  허용되는 값은 &quot;dedupeFields&quot;(&quot;name&quot;에 해당함) 또는 &quot;idField&quot;(&quot;marketoGUID&quot;에 해당함)입니다.  위치 `createOnly` 모드, &quot;name&quot;만 (으)로 허용됩니다. `dedupeBy` 필드. 한 번에 최대 300개의 레코드를 제출할 수 있습니다.

```
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

명명 계정 목록의 삭제는 간단하며 다음 중 하나를 기반으로 수행할 수 있습니다. `name`또는 `marketoGUID` 목록에 있는 모든 세그먼트를 표시합니다. 사용할 키를 선택하려면 의 이름에 &quot;dedupeFields&quot; 또는 marketoGUID에 &quot;idField&quot;를 전달합니다.`deleteB` 요청 구성원. 설정을 해제하면 dedupeFields가 기본값으로 설정됩니다. 한 번에 최대 300개의 레코드를 삭제할 수 있습니다.

```
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

특정 키에 대한 레코드를 찾을 수 없는 경우 해당 결과 항목에는`status` 위의 예에서 보듯이 실패를 설명하는 코드와 메시지가 있는 &quot;건너뜀&quot; 및 이유.

## 멤버십 관리

### 쿼리 멤버십

명명된 계정 목록의 구성원을 쿼리하는 것은 간단하며`i` 계정 목록. 선택적 매개 변수는 다음과 같습니다.

-`field` - 응답 레코드에 포함할 쉼표로 구분된 필드 목록 -`nextPageToke` - 결과 집합을 통해 페이징할 경우 -`batchSiz` - 반환할 레코드 수를 지정합니다.

If`field` 설정이 해제된 경우`marketoGUI`,`nam`, `createdA`, 및`updatedA` 반환됩니다. `batchSiz` 에는 최대 및 기본값이 300입니다.

```
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

명명 계정은 명명 계정 목록에 쉽게 추가할 수 있습니다. 계정은 marketoGUID를 사용해야만 추가할 수 있습니다. 한 번에 최대 300개의 레코드를 추가할 수 있습니다.

```
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

계정 목록에서 레코드를 제거하면 경로는 다르지만 동일한 인터페이스가 사용되므로`marketoGUI` 삭제할 각 레코드에 대해. 한 번에 최대 300개의 레코드를 제거할 수 있습니다.

```
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

- 아래에 명시하지 않은 경우 명명된 계정 목록 엔드포인트의 시간 제한은 30초입니다.
   - 명명된 계정 목록 동기화: 60s 
   - 명명 계정 목록 삭제: 60s 
   - 명명된 계정 목록 가져오기: 60s 
   - 명명된 계정 목록 구성원 추가: 60s 
   - 명명된 계정 목록 구성원 제거: 60s 
   - 명명된 계정 목록 구성원 가져오기: 60s
