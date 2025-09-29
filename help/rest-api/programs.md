---
title: 프로그램
feature: REST API, Programs
description: 유형, 채널, 태그, 멤버 상태 및 엔드포인트를 다루는 Asset REST API에 대한 Marketo 프로그램 안내서를 참조하여 id 또는 이름별로 가져오고, 찾아보고, 상태별로 필터링합니다.
exl-id: 30700de2-8f4a-4580-92f2-7036905deb80
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 1%

---

# 프로그램

[프로그램 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs)

프로그램은 Marketo 마케팅 활동의 핵심 조직 구성 요소입니다. 대부분의 에셋 유형의 부모가 될 수 있으며, 개별 마케팅 이니셔티브의 컨텍스트 내에서 멤버 자격 및 잠재 고객 성공 여부를 추적할 수 있습니다. 프로그램은 LP, 이메일 템플릿 및 파일을 제외한 모든 유형의 레코드에 대한 상위 프로그램일 수 있습니다.

## 프로그램 유형

Marketo에는 5가지 핵심 유형의 프로그램이 있습니다.

- 기본
- 이벤트
- 웨비나를 사용하는 이벤트
- 참여
- 이메일

참여 프로그램은 서로 다른 유형의 프로그램에 대한 상위 항목일 수 있지만 웨비나를 사용하는 기본값, 이벤트 및 이벤트는 이메일 프로그램에 대한 상위 항목일 수 있습니다.

프로그램은 항상 채널을 가지며, 채널 가져오기 API를 사용하여 검색할 수 있는 로 만든 채널에서 가능한 프로그램 멤버 상태 설정을 가져옵니다. 프로그램은 또한 연관된 태그들의 세트를 가질 수 있다. 태그는 사용자 정의 가능한 필드로, 지정된 프로그램 유형에 대해 선택 사항이나 필수로 구성할 수 있으며, Marketo 관리자에 구성된 목록에서 값을 선택합니다.

## 쿼리

프로그램은 태그 유형 및 값별로 쿼리할 수 있는 추가 옵션과 함께 에셋 쿼리에 대한 표준 패턴을 따릅니다. 사용 가능한 태그 및 값은 [태그 유형 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Tags/operation/getTagTypesUsingGET)를 통해 검색할 수 있습니다.

### ID별

[ID별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 끝점에는 `id` 경로 매개 변수가 필요합니다.

프로그램 ID는 UI의 프로그램 URL에서 가져올 수 있습니다. 여기서 URL은 `https://app-\*\*\*.marketo.com/#PG1001A1`과(와) 비슷합니다. 이 URL에서 `id`은(는) 1001입니다. 항상 URL의 첫 번째 문자 세트와 두 번째 문자 세트 사이에 있습니다.

```
GET /rest/asset/v1/program/{id}.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#14db037ec71",
    "result": [
        {
            "id": 1107,
            "name": "AAA2QueryProgramName",
            "description": "AssetAPI: getProgram tests",
            "createdAt": "2015-05-21T22:45:13Z+0000",
            "updatedAt": "2015-05-21T22:45:13Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1107A1",
            "type": "Default",
            "channel": "Online Advertising",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "",
            "workspace": "Default",
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                }
            ],
            "costs": null,
            "headStart": false
        }
    ]
}
```

### 이름별

[이름별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/) 끝점에는 `name` 쿼리 매개 변수가 필요합니다. 선택적 부울 쿼리 매개 변수는 각각 프로그램 태그 및 프로그램 비용을 반환하는 데 사용되는 `includeTags` 및 `includeCosts`입니다.

```
GET /rest/asset/v1/program/byName.json?name=TestProgramName&includeTags=true
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#14db03e070c",
    "result": [
        {
            "id": 1107,
            "name": "AAA2QueryProgramName",
            "description": "AssetAPI: getProgram tests",
            "createdAt": "2015-05-21T22:45:13Z+0000",
            "updatedAt": "2015-05-21T22:45:13Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1107A1",
            "type": "Default",
            "channel": "Online Advertising",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "",
            "workspace": "Default",
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                }
            ],
            "costs": null,
            "headStart": false
        }
    ]
}
```

### 찾아보기

[프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 끝점을 사용하면 프로그램을 검색할 수 있습니다.

선택적 `status` 매개 변수를 사용하면 프로그램 상태를 필터링할 수 있습니다. 이 매개 변수는 참여 및 이메일 프로그램에만 적용됩니다. 가능한 값은 참여 프로그램의 경우 &quot;on&quot; 및 &quot;off&quot;이고, 이메일 프로그램의 경우 &quot;unlocked&quot;입니다.

선택적 `maxReturn` 매개 변수는 반환할 프로그램 수를 제어합니다(최대값은 200개, 기본값은 20개). 페이징 결과에 사용되는 선택적 `offset` 매개 변수입니다(기본값은 0).

프로그램과 연결된 태그는 이 끝점에서 반환되지 않습니다. [Id로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET) 또는 [이름별로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET)를 사용하여 프로그램 태그를 검색할 수 있습니다.

```
GET /rest/asset/v1/programs.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "7a39#1511bf8a41c",
    "result": [
        {
            "id": 1035,
            "name": "clone it",
            "description": "",
            "createdAt": "2015-11-18T15:25:35Z+0000",
            "updatedAt": "2015-11-18T15:25:46Z+0000",
            "url": "https://app-devlocal1.marketo.com/#NP1035A1",
            "type": "Engagement",
            "channel": "Nurture",
            "folder": {
                "type": "Folder",
                "value": 28,
                "folderName": "Nurturing"
            },
            "status": "on",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1032,
            "name": "email prog",
            "description": "",
            "createdAt": "2015-11-18T14:56:28Z+0000",
            "updatedAt": "2015-11-18T14:56:28Z+0000",
            "url": "https://app-devlocal1.marketo.com/#EBP1032A1",
            "type": "Email",
            "channel": "Email Send",
            "folder": {
                "type": "Folder",
                "value": 26,
                "folderName": "Data Management"
            },
            "status": "unlocked",
            "workspace": "Default",
            "headStart": false
        }
    ]
}
```

### 날짜 범위별

`earliestUpdatedAt`프로그램 가져오기`latestUpdatedAt` 끝점에 대한 [ 및 ](https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5) 매개 변수를 사용하면 지정된 범위 내에서 업데이트되었거나 처음 만들어진 프로그램을 반환하는 데 대해 낮거나 높은 날짜/시간 워터마크를 설정할 수 있습니다.

```
GET /rest/asset/v1/programs.json?earliestUpdatedAt=2017-01-01T00:00:00-05:00&latestUpdatedAt=2017-01-30T00:00:00-05:00
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1225a#15f82a83875",
    "warnings": [],
    "result": [
        {
            "id": 1070,
            "name": "Bulk Import - Test",
            "description": "",
            "createdAt": "2017-01-13T19:34:17Z+0000",
            "updatedAt": "2017-01-13T19:34:18Z+0000",
            "url": "https://app-abm.marketo.com/#PG1070A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 637,
                "folderName": "Avention"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1069,
            "name": "Program With Email",
            "description": "",
            "createdAt": "2017-01-03T22:53:14Z+0000",
            "updatedAt": "2017-01-03T22:53:15Z+0000",
            "url": "https://app-abm.marketo.com/#EBP1069A1",
            "type": "Email",
            "channel": "Email Send",
            "folder": {
                "type": "Folder",
                "value": 621,
                "folderName": "Smartling"
            },
            "status": "unlocked",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1071,
            "name": "Program with Guided Landing Page Template",
            "description": "",
            "createdAt": "2017-01-24T22:59:21Z+0000",
            "updatedAt": "2017-01-24T22:59:22Z+0000",
            "url": "https://app-abm.marketo.com/#PG1071A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 621,
                "folderName": "Smartling"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        },
        {
            "id": 1047,
            "name": "ReachForce List Update",
            "description": "",
            "createdAt": "2016-05-24T19:38:35Z+0000",
            "updatedAt": "2017-01-13T19:28:09Z+0000",
            "url": "https://app-abm.marketo.com/#PG1047A1",
            "type": "Default",
            "channel": "Content",
            "folder": {
                "type": "Folder",
                "value": 407,
                "folderName": "Everly Tests"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
        }
    ]
}
```

### 태그 유형별

[태그별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramListByTagUsingGET) 끝점은 제공된 태그 형식 및 태그 값과 일치하는 프로그램 목록을 검색합니다.

필수 매개 변수에는 필터링할 태그의 종류인 `tagType`과(와) 필터링할 태그 값인 `tagValue`이(가) 있습니다.  반환할 프로그램 수를 제어하는 선택적 정수 `maxReturn` 매개 변수가 있으며(최대 200개, 기본값은 20개), 페이징 결과에 사용되는 선택적 정수 `offset` 매개 변수가 있습니다(기본값은 0임).  결과는 임의 순서로 반환됩니다.

```
GET /rest/asset/v1/program/byTag.json?tagType=Presenter&tagValue=Dennis
```

```json
{
    "success" : true,
    "warnings" : [],
    "errors" : [],
    "requestId" : "13b6d#152b38d5be4",
    "result" : [{
            "id" : 1004,
            "name" : "It's a Program",
            "description" : "",
            "createdAt" : "2013-02-26T00:37:37Z+0000",
            "updatedAt" : "2013-03-11T15:32:02Z+0000",
            "url" : "https://app-sjst.marketo.com/#PG1004A1",
            "type" : "Default",
            "channel" : "Email Blast",
            "folder" : {
                "type" : "Folder",
                "value" : 38,
                "folderName" : "Test"
            },
            "status" : "",
            "workspace" : "Default",
            "tags" : [{
                    "tagType" : "Presenter",
                    "tagValue" : "Dennis"
                }
            ],
                        "headStart": false
    ]
}
```

## 만들기 및 업데이트

[만들기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/createProgramUsingPOST) 및 [업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/updateProgramUsingPOST) 프로그램은 표준 자산 패턴을 따르며 필수 매개 변수로 `folder`, `name`, `type` 및 `channel`을(를) 포함합니다. `description`, `costs` 및 `tags`은(는) 선택 사항입니다. 채널 및 유형은 프로그램 생성 시에만 설정할 수 있습니다. 추가 `tags` 매개 변수가 허용되면 설명, 이름, `costs` 및 `costsDestructiveUpdate`만 업데이트할 수 있습니다. `costsDestructiveUpdate`을(를) true로 전달하면 기존 비용이 모두 지워지고 호출에 포함된 비용으로 대체됩니다. 일부 구독의 일부 프로그램 유형에는 태그가 필요할 수 있지만, 이는 구성에 따라 달라지며 먼저 태그 가져오기 를 사용하여 인스턴스별 요구 사항이 있는지 확인해야 합니다.

전자 메일 프로그램을 만들거나 업데이트할 때 `startDate` 및 `endDate`도 UTC 날짜/시간으로 전달될 수 있습니다.

`"startDate": "2022-10-19T15:00:00.000Z"`
`"endDate": "2022-10-19T15:00:00.000Z"`

### 만들기

```
POST /rest/asset/v1/programs.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=API Test Program&folder={"id":1035,"type":"Folder"}&description=Sample API Program&type=Default&channel=Email Blast&costs=[{"startDate":"2015-01-01","cost":2000}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "d505#14d9bd96352",
    "result": [
        {
            "id": 1207,
            "name": "newProgram",
            "description": "This is a test",
            "createdAt": "2015-05-28T18:47:15Z+0000",
            "updatedAt": "2015-05-28T18:47:15Z+0000",
            "url": "https://app-devlocal1.marketo.com/#ME1207A1",
            "type": "Event",
            "channel": "channelOne",
            "folder": {
                "type": "Folder",
                "value": 59,
                "folderName": "blah blah"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
            "tags": null,
            "costs": [
                {
                    "startDate":"2015-01-01",
                    "cost":2000
                }
            ]
        }
    ]
}
```

### 업데이트

프로그램 비용을 업데이트할 때 새 비용을 추가하려면 `costs` 배열에 추가하기만 하면 됩니다. 원본에 영향을 주는 업데이트를 수행하려면 `costsDestructiveUpdate`(으)로 설정된 `true` 매개 변수와 함께 새 비용을 전달하십시오. 프로그램에서 모든 비용을 지우려면 `costs` 매개 변수를 전달하지 말고 `costsDestructiveUpdate`(으)로 설정된 `true`만 전달하십시오.

```
POST /rest/asset/v1/program/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=This is an updated description&name=Updated Program Name&costs=[{"startDate":"2016-01-01","cost":200,"note":"Google Adwords"}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5c37#14db05608aa",
    "result": [
        {
            "id": 1110,
            "name": "Updated Program Name",
            "description": "This is a updated description",
            "createdAt": "2015-05-21T22:45:14Z+0000",
            "updatedAt": "2015-06-01T18:13:58Z+0000",
            "url": "https://app-devlocal1.marketo.com/#NP1110A1",
            "type": "Engagement",
            "channel": "Nurture",
            "folder": {
                "type": "Folder",
                "value": 1910,
                "folderName": "ProgramQueryTestFolder"
            },
            "status": "on",
            "workspace": "Default",
            "headStart": false,
            "tags": [
                {
                    "tagType": "AAA1 Required Tag Type",
                    "tagValue": "AAA1 RT1"
                },
                {
                    "tagType": "tagTypeOne",
                    "tagValue": "tagTypeValue1"
                }
            ],
            "costs": [
                {
                    "startDate": "2016-01-01",
                    "cost": 200,
                    "note": "Google Adwords"
                }
            ]
        }
    ]
}
```

## 승인

이메일 프로그램은 원격으로 승인되거나 승인되지 않을 수 있으며, 이렇게 하면 프로그램이 지정된 startDate에 실행되고 지정된 endDate에 종료됩니다. 이 두 가지 모두 프로그램을 승인하도록 설정하고, UI를 통해 유효하고 승인된 이메일 및 스마트 목록을 구성해야 합니다.

### 승인

```
POST /rest/asset/v1/program/{id}/approve.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#150b5bf7692",
    "result": [
        {
            "id": 11062
        }
    ]
}
```

### 승인 취소

```
POST /rest/asset/v1/program/{id}/unapprove.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16026#150b5bf7692",
    "result": [
        {
            "id": 11062
        }
    ]
}
```

## 복제

[프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/cloneProgramUsingPOST)는 새 이름과 폴더를 필수 매개 변수 및 선택적 설명으로 표준 자산 패턴을 따릅니다.  `name` 매개 변수는 전역적으로 고유해야 하며 255자를 초과할 수 없습니다.  `folder` 매개 변수는 상위 폴더입니다.  `folder` 매개 변수 형식 특성을 &quot;Folder&quot;로 설정해야 하며 대상 폴더는 복제되는 프로그램과 동일한 작업 영역에 있어야 합니다.

푸시 알림, 인앱 메시지, 보고서 및 소셜 Assets을 포함하여 특정 유형의 자산이 포함된 프로그램은 이 API를 통해 복제되지 않을 수 있습니다. 인앱 프로그램은 이 API를 통해 복제되지 않을 수 있습니다.

```
POST /rest/asset/v1/program/{id}/clone.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
name=Cloned Program - PHP&folder={"id":5562,"type":"Folder"}&description=Description
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "3a7f#14db06990cc",
    "result": [
        {
            "id": 1221,
            "name": "cloneProgram",
            "description": "This is a description for the cloned program",
            "createdAt": "2015-06-01T18:36:57Z+0000",
            "updatedAt": "2015-06-01T18:36:57Z+0000",
            "url": "https://app-devlocal1.marketo.com/#PG1221A1",
            "type": "Default",
            "channel": "Blog",
            "folder": {
                "type": "Folder",
                "value": 59,
                "folderName": "blah blah"
            },
            "status": "",
            "workspace": "Default",
            "headStart": false
            "tags": null,
            "costs": null
        }
    ]
}
```

## 프로그램 삭제

프로그램 삭제는 표준 에셋 삭제 패턴을 따릅니다.

```
POST /rest/asset/v1/program/{id}/delete.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "16501#14db042c6b7",
    "result": [
        {
            "id": 1109
        }
    ]
}
```
