---
title: 프로그램
feature: REST API, Programs
description: 유형, 채널, 태그, 멤버 상태 및 엔드포인트를 다루는 Asset REST API에 대한 Marketo 프로그램 안내서를 참조하여 id 또는 이름별로 가져오고, 찾아보고, 상태별로 필터링합니다.
exl-id: 30700de2-8f4a-4580-92f2-7036905deb80
TQID: https://experienceleague.adobe.com/5ILyahSn3Pp-lF6YPogVnkXjXP-QLtEmyLm7iKMIgo0
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f82558ea-6af5-44eb-a424-5b3389abb0a3
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 741
ht-degree: 1%

---

# 프로그램

[프로그램 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs)

프로그램은 Marketo 마케팅 활동을 조직하고 개별 마케팅 이니셔티브에 대한 리드 멤버십과 성공을 추적합니다. 프로그램에는 랜딩 페이지, 이메일 템플릿 및 파일을 제외한 대부분의 에셋 유형이 포함될 수 있습니다.

## 프로그램 유형

Marketo에는 5가지 핵심 유형의 프로그램이 있습니다.

- 기본
- 이벤트
- 웨비나를 사용하는 이벤트
- 참여
- 이메일

참여 프로그램에는 다른 모든 프로그램 유형이 포함될 수 있습니다. 웨비나 프로그램이 있는 기본, 이벤트 및 이벤트는 이메일 프로그램만 포함할 수 있습니다.

모든 프로그램에는 채널이 있습니다. 채널은 사용 가능한 프로그램 멤버 상태를 정의하고 채널 가져오기 API를 통해 검색할 수 있습니다.

프로그램에는 태그가 있을 수도 있습니다. 태그는 사용자 정의 가능한 필드로, 프로그램 유형에 선택 사항이거나 필요할 수 있습니다. 각 태그는 Marketo Admin에 구성된 목록의 값을 사용합니다.

## 쿼리

ID, 이름, 검색 또는 태그 유형 및 값별로 프로그램을 쿼리합니다. 사용 가능한 태그 및 값을 검색하려면 [태그 유형 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Tags/operation/getTagTypesUsingGET)를 사용하십시오.

### ID별

[ID별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) 끝점에는 `id` 경로 매개 변수가 필요합니다.

해당 UI URL에서 프로그램 ID를 가져올 수 있습니다(예: `https://app-\*\*\*.marketo.com/#PG1001A1`). 이 예제에서 ID는 첫 번째 문자와 두 번째 문자 집합 사이의 `1001`입니다.

```http
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

[이름별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset) 끝점에는 `name` 쿼리 매개 변수가 필요합니다. 선택적 부울 매개 변수 `includeTags` 및 `includeCosts`을(를) 설정하여 각각 태그와 비용을 반환합니다.

```http
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

[프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5) 끝점을 사용하여 프로그램을 찾아봅니다.

선택적 `status` 매개 변수는 상태별로 참여 및 전자 메일 프로그램을 필터링합니다. 유효한 값은 참여 프로그램의 경우 `on` 및 `off`이고 전자 메일 프로그램의 경우 `unlocked`입니다.

선택적 `maxReturn` 매개 변수는 반환된 프로그램의 수를 제어합니다. 기본값은 20이고 최대값은 200입니다. 페이지 매김에 선택적 `offset` 매개 변수를 사용하십시오. 기본값은 0입니다.

이 끝점은 프로그램 태그를 반환하지 않습니다. [ID별로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByIdUsingGET) 또는 [이름별로 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramByNameUsingGET)로 태그를 검색합니다.

```http
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

[프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Sales-Persons/operation/describeUsingGET_5)와 함께 `earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수를 사용하여 낮음 및 높은 날짜-시간 경계를 설정합니다. 끝점은 범위 내에서 만들어지거나 업데이트된 프로그램을 반환합니다.

```http
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

[태그별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/getProgramListByTagUsingGET) 끝점은 지정된 태그 형식 및 값과 일치하는 프로그램을 반환합니다.

`tagType` 및 `tagValue` 매개 변수가 필요합니다. 선택적 정수 `maxReturn`은(는) 반환되는 프로그램 수를 제어합니다. 기본값은 20이고, 최대값은 200입니다. 페이지 매김에 선택적 정수 `offset`을(를) 사용하십시오. 기본값은 0입니다. 결과는 임의 순서로 반환됩니다.

```http
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

[프로그램을 만드는 중](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/createProgramUsingPOST)에는 `folder`, `name`, `type` 및 `channel`이(가) 필요합니다. 선택적 매개 변수는 `description`, `costs` 및 `tags`입니다. 일부 구독에는 특정 프로그램 유형에 대한 태그가 필요합니다. 태그 가져오기 를 사용하여 인스턴스 요구 사항을 확인합니다.

[업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/updateProgramUsingPOST)할 때 설명, 이름, `tags` 및 `costs`만 변경할 수 있습니다. 생성하는 동안에만 채널과 유형을 설정할 수 있습니다. `costsDestructiveUpdate`을(를) `true`(으)로 설정하면 기존 비용이 모두 지워지고 요청에 포함된 비용으로 바뀝니다.

전자 메일 프로그램을 만들거나 업데이트할 때 `startDate` 및 `endDate`도 UTC 날짜/시간으로 전달될 수 있습니다.

`"startDate": "2022-10-19T15:00:00.000Z"`
`"endDate": "2022-10-19T15:00:00.000Z"`

### 만들기

```http
POST /rest/asset/v1/programs.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

프로그램 비용을 추가하려면 `costs` 배열에 추가하십시오. 기존 비용을 바꾸려면 새 비용을 전달하고 `costsDestructiveUpdate`을(를) `true`(으)로 설정합니다. 모든 비용을 지우려면 `costs`을(를) 생략하고 `costsDestructiveUpdate`을(를) `true`(으)로 설정하십시오.

```http
POST /rest/asset/v1/program/{id}.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

전자 메일 프로그램을 원격으로 승인하거나 승인하지 않을 수 있습니다. 승인된 프로그램은 `startDate`에서 실행되고 `endDate`에 종료됩니다.

승인 전에 두 날짜를 모두 설정하고 UI에서 유효하고 승인된 이메일 및 스마트 목록을 구성합니다.

### 승인

```http
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

```http
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

[프로그램을 복제하려면](https://developer.adobe.com/marketo-apis/api/asset#tag/Programs/operation/cloneProgramUsingPOST)새 이름과 상위 폴더가 필요합니다. 설명은 선택 사항입니다. `name`은(는) 전체적으로 고유해야 하며 255자를 초과할 수 없습니다.

`folder` 매개 변수의 형식 특성을 `Folder`(으)로 설정합니다. 대상 폴더는 소스 프로그램과 동일한 작업 영역에 있어야 합니다.

이 API를 사용하여 인앱 프로그램 또는 푸시 알림, 인앱 메시지, 보고서 또는 소셜 에셋이 포함된 프로그램을 복제할 수 없습니다.

```http
POST /rest/asset/v1/program/{id}/clone.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
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

```http
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
