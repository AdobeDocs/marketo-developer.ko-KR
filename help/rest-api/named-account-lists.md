---
title: 명명된 계정 목록
feature: REST API
description: 명명된 계정 목록을 구성합니다.
exl-id: 98f42780-8329-42fb-9cd8-58e5dbea3809
source-git-commit: 3649db037a95cfd20ff0a2c3d81a3b40d0095c39
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---

# 명명된 계정 목록

[명명된 계정 목록 끝점 참조](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Named-Account-Lists)

Marketo의 [명명된 계정 목록](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/target-account-management/target/account-lists)은(는) 명명된 계정의 컬렉션을 나타냅니다. 분류, 데이터 보강 및 스마트 캠페인 필터링을 포함하여 다양한 경우에 사용할 수 있습니다. 명명된 계정 목록 API를 사용하면 이러한 목록 에셋과 해당 멤버십을 원격으로 관리할 수 있습니다.
`Content`

## 권한

명명된 계정 목록을 쿼리하려면 읽기 전용 명명된 계정 목록 또는 읽기-쓰기 명명된 계정 목록 권한이 필요합니다. 목록을 만들거나 업데이트하거나 삭제하려면 명명된 계정 목록 읽기-쓰기 권한이 필요합니다. 목록 구성원을 쿼리하려면 읽기 전용 이름 지정 계정 또는 읽기-쓰기 이름 지정 계정 권한이 필요하며 구성원 자격을 관리하려면 읽기-쓰기 이름 지정 계정 권한이 필요합니다.

## 모델

명명된 계정 목록에는 제한된 수의 표준 필드가 있으며 사용자 지정 필드로 확장할 수 없습니다.
`Named Account List Field`

| 이름 | 데이터 유형 | 업데이트 가능 | 참고 |
|---|---|---|---|
| marketoGUID | 문자열 | False | 명명된 계정 목록의 고유 문자열 식별자입니다. 이 필드는 시스템에서 관리되며 레코드를 만들 때 필드로 허용되지 않습니다. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;idField&quot;에서 사용하는 필드. |
| 이름 | 문자열 | True | 목록 이름. 만들기 또는 업데이트를 수행할 때 &quot;dedupeBy&quot;:&quot;dedupeFields&quot;에서 사용하는 필드. |
| createdAt | 날짜/시간 | False | 목록 작성의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| updatedAt | 날짜/시간 | False | 목록에 대한 최신 업데이트의 날짜/시간입니다. 이 필드는 시스템 관리이며, 레코드를 만들거나 업데이트할 때 필드로 사용할 수 없습니다. |
| 유형 | 문자열 | False | 목록 유형. 값은 &quot;default&quot; 또는 &quot;external&quot;일 수 있습니다. 외부 목록은 CRM 계정 보기에서 만든 목록입니다. |

## 쿼리

계정 목록 쿼리는 간단하고 쉽습니다. 현재 명명된 계정 목록을 쿼리하기 위해 유효한 filterType은 &quot;dedupeFields&quot;와 &quot;idField&quot;뿐입니다. 필터링할 필드가 쿼리의 `filterType` 매개 변수에 설정되고 값은 `filterValues as`에 쉼표로 구분된 목록으로 설정됩니다. `nextPageToken` 및 `batchSize` 필터도 선택적 매개 변수입니다.

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

명명 계정 목록 레코드를 생성하고 갱신하면 다른 리드 데이터베이스 생성 및 갱신 작업에 대해 설정된 패턴을 따릅니다. 명명된 계정 목록에는 업데이트할 수 있는 필드 `name`이(가) 하나만 있습니다.

끝점은 &quot;createOnly&quot;와 &quot;updateOnly&quot;의 두 가지 표준 작업 유형을 허용합니다.  `action defaults`에서 &quot;createOnly&quot;로 변경되었습니다.

작업이 `dedupeBy parameter`인 경우 선택적 `updateOnly`을(를) 지정할 수 있습니다.  허용되는 값은 &quot;dedupeFields&quot;(&quot;name&quot;에 해당함) 또는 &quot;idField&quot;(&quot;marketoGUID&quot;에 해당함)입니다.  `createOnly` 모드에서는 &quot;name&quot;만 `dedupeBy` 필드로 허용됩니다. 한 번에 최대 300개의 레코드를 제출할 수 있습니다.

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

명명 계정 목록은 간단하게 삭제할 수 있으며, 목록의 `name` 또는 `marketoGUID`을(를) 기반으로 삭제할 수 있습니다. 사용할 키를 선택하려면 요청의 `deleteB` 멤버에서 이름에 &quot;dedupeFields&quot;를 전달하거나 marketoGUID에 &quot;idField&quot;를 전달합니다. 설정을 해제하면 dedupeFields가 기본값으로 설정됩니다. 한 번에 최대 300개의 레코드를 삭제할 수 있습니다.

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

특정 키에 대한 레코드를 찾을 수 없는 경우 해당 결과 항목의 `status`은(는) &quot;생략됨&quot;이며, 위의 예제와 같이 오류를 설명하는 코드와 메시지가 포함된 이유가 있습니다.

## 멤버십 관리

### 쿼리 멤버십

명명된 계정 목록의 구성원 자격 쿼리는 간단하며 계정 목록의 `i`만 필요합니다. 선택적 매개 변수는 다음과 같습니다.

-`field` - 응답 레코드에 포함할 쉼표로 구분된 필드 목록
-`nextPageToke` - 결과 집합을 통해 페이징용
-`batchSiz` - 반환할 레코드 수를 지정합니다.

`field`이(가) 설정되지 않으면 `marketoGUI`,`nam`, `createdA` 및`updatedA`이(가) 반환됩니다. `batchSiz`의 최대 및 기본값은 300입니다.

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

계정 목록에서 레코드를 제거하면 경로는 다르지만 동일한 인터페이스가 있으므로 삭제할 각 레코드에 대해 `marketoGUI`이(가) 필요합니다. 한 번에 최대 300개의 레코드를 제거할 수 있습니다.

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
