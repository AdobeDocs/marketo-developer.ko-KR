---
title: 양식
feature: REST API, Forms
description: 양식 만들기 및 관리, id 또는 이름별로 검색, 상태 필터 찾아보기, 필드, 필드 세트 및 규칙 관리를 위한 Marketo Forms REST API 안내서.
exl-id: 2e5dfa70-3163-4ab4-b269-3112417714c3
TQID: https://experienceleague.adobe.com/56tc1a14d8okxweS7TK7SzfGB8G03WAI2KBlFKQbSdM
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615
feature_v2: id: a7170d27-32ab-462b-a333-269abc654483id: b0bb9048-d951-48d8-8232-45cf248a7e27id: d65b4a73-87a3-4d56-b638-74e74d9939ceid: e64968b2-4ee5-47f9-8cae-0588f184b9eb
subfeature_v2: id: d0251300-e25f-466f-9856-7e11ce8fa7aa
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 3e6d310c5aec1a3435424fb122b71d825db5af0e
workflow-type: tm+mt
source-wordcount: 1494
ht-degree: 2%

---

# 양식

[Forms 엔드포인트 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms)

[양식 필드 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields)

양식 끝점을 사용하여 원격 시스템에서 양식을 관리합니다. 양식에는 다음과 같은 여러 객체 유형이 포함될 수 있습니다.

- 양식
- 필드
- 필드 세트
- 가시성 규칙
- 후속 페이지 규칙

## 쿼리

Forms은 표준 자산 검색 메서드를 지원합니다. [id별](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET) 및 [검색](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/browseForms2UsingGET). 양식 응답에는 필드 목록을 제외한 모든 양식 속성이 포함됩니다.

### ID별

`id` 양식을 [Id로 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByIdUsingGET)에 경로 매개 변수로 전달합니다. 끝점은 일치하는 양식 레코드를 반환합니다.

```http
GET /rest/asset/v1/form/{id}.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

### 이름별

`name` 양식을 [이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getLpFormByNameUsingGET)에 전달합니다. 끝점은 일치하는 양식 레코드를 반환합니다.

```http
GET /rest/asset/v1/form/byName.json?name=newForm
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

### 찾아보기

[Forms 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/browseForms2UsingGET)는 표준 에셋 API 찾아보기 패턴을 따릅니다. 다음과 같은 선택 필터를 지원합니다.

- `status`: `approved`, `approved with draft` 또는 `draft`별 필터
- `maxReturn`: 반환된 레코드의 수를 제한합니다.
- `offset`: 결과 집합을 통과하는 페이지입니다.

```http
GET /rest/asset/v1/forms.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "645d#154e3d499ac",
    "result": [
        {
            "id": 227,
            "name": "aKAUVDfbsX",
            "description": "",
            "createdAt": "2016-05-18T20:36:20Z+0000",
            "updatedAt": "2016-05-18T20:36:20Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO227B2",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        },
        {
            "id": 695,
            "name": "AoMXgfFbma",
            "description": "",
            "createdAt": "2016-05-19T18:50:40Z+0000",
            "updatedAt": "2016-05-19T18:50:40Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO695B2",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": true,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 565,
                "folderName": "WfUvYmlcyT"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        }
    ]
}
```

### 필드 목록

양식 ID를 전달하여 각 양식에 대해 필드 목록을 별도로 검색합니다.

```http
GET /rest/asset/v1/form/{id}/fields.json
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "2165#154eee00d01",
    "result": [
        {
            "id": "FirstName",
            "label": "First Name:",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 0,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "LastName",
            "label": "Last Name:",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 1,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "Email",
            "label": "Email Address:",
            "dataType": "email",
            "validationMessage": "Must be valid email. <span class='mktoErrorDetail'>example@yourdomain.com</span>",
            "rowNumber": 2,
            "columnNumber": 0,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        },
        {
            "id": "Profiling",
            "dataType": "profiling",
            "rowNumber": 3,
            "columnNumber": 0
        }
    ]
}
```

필드를 업데이트 또는 삭제하거나 동작을 변경하기 전에 양식의 필드 목록을 검색하십시오. 후속 요청에서 반환된 필드 ID를 사용합니다.

### 필드 유형

| UI 유형 | API 이름 |
| --- | --- |
| 확인란 | 확인란 |
| 라디오 단추 | 라디오 |
| 텍스트 영역 | 텍스트 영역 |
| 선택 목록 | 선택 목록 |
| 문자열 | 문자열 |
| 이메일 | 이메일 |
| 일자 | 날짜 |
| 숫자 | 번호 |
| 더블 | 중복 |
| 전화 | 전화 |
| URL | url |
| 통화 | 통화 |
| 확인란 | single_checkbox |
| 슬라이더 | 범위 |

### 종속성

`id` 양식을 [사용한 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/getFormUsedByUsingGET)에 경로 매개 변수로 전달합니다. 끝점은 양식에 의존하는 자산을 반환합니다.

다음 자산 유형에서 양식을 사용할 수 있습니다.

- 랜딩 페이지
- 스마트 목록
- 스마트 캠페인
- 보고서
- 이메일 프로그램

```http
GET /rest/asset/v1/form/{id}/usedBy.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "fdf4#17285b25038",
    "warnings": [],
    "result": [
        {
            "id": 1038,
            "name": "LP Redirect Rules Program.LP Test 01",
            "type": "Landing Page",
            "status": "approved",
            "updatedAt": "2020-02-23T01:31:21Z+0000"
        }
    ]
}
```

## 만들기 및 업데이트

[양식을 만들기](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/createLpFormsUsingPOST)하려면 두 개의 필수 필드를 입력하십시오.

- 양식의 상위 폴더입니다.
- 양식 이름.

다른 모든 매개 변수는 선택 사항이며 기본값을 가집니다. 새 양식에는 이름, 성 및 이메일의 세 가지 기본 필드가 포함됩니다.

```http
POST /rest/asset/v1/forms.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=newForm&description=test&folder={"type": "Folder","id": 293}&language=French
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "948f#154e3bad8e3",
    "result": [
        {
            "id": 736,
            "name": "newForm",
            "description": "test",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:05:54Z+0000",
            "url": "https://app-devlocal1.marketo.com/#FO736B2",
            "status": "draft",
            "theme": "simple",
            "language": "French",
            "locale": "fr_FR",
            "progressiveProfiling": false,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Envoyer",
            "waitingLabel": "Veuillez patienter"
        }
    ]
}
```

[양식을 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/updateFormsUsingPOST)하려면 해당 ID를 전달하십시오. 만들거나 업데이트하는 동안 폼이 사용자에게 표시되는 방식을 제어하는 기본 스타일 매개 변수를 설정할 수 있습니다.

```http
POST /rest/asset/v1/form/736.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=updated name&description=This is a test for updateapi&language=English&progressiveProfiling=true&locale=en_US
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "6307#154e3cf6efe",
    "result": [
        {
            "id": 736,
            "name": "updated name",
            "description": "This is a test for update api",
            "createdAt": "2016-05-24T17:05:54Z+0000",
            "updatedAt": "2016-05-24T17:28:23Z+0000",
            "status": "draft",
            "theme": "simple",
            "language": "English",
            "locale": "en_US",
            "progressiveProfiling": true,
            "labelPosition": "left",
            "fontFamily": "Helvetica",
            "fontSize": "13px",
            "folder": {
                "type": "Folder",
                "value": 293,
                "folderName": "yyLNLHzgOM"
            },
            "knownVisitor": {
                "type": "form",
                "template": null
            },
            "thankYouList": [
                {
                    "followupType": "none",
                    "followupValue": null,
                    "default": true
                }
            ],
            "buttonLocation": 120,
            "buttonLabel": "Submit",
            "waitingLabel": "Please Wait"
        }
    ]
}
```

양식 엔드포인트 만들기 및 업데이트에서는 알려진 방문자 또는 감사 페이지 동작을 수정하지 않습니다. 해당 동작을 관리하려면 해당 엔드포인트를 사용합니다.

## 필드 메타데이터

양식 필드를 추가하거나 편집하기 전에 대상 인스턴스에 대한 유효한 필드를 검색합니다. 필드 작업에서는 각 필드에 대해 반환된 `id` 속성을 사용합니다.

리드 필드의 경우 [사용 가능한 양식 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getAllFieldsUsingGET) 끝점을 사용하십시오. 응답에는 각 필드의 데이터 형식과, 필드가 양식에 추가될 때 적용되는 기본 메타데이터가 포함됩니다.

```http
GET /rest/asset/v1/form/fields.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "176ca#167a9808f4c",
    "warnings": [],
    "result": [
        {
            "id": "AnnualRevenue",
            "isRequired": false,
            "dataType": "currency"
        },
        {
            "id": "City",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Company",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Country",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Description",
            "isRequired": false,
            "dataType": "textarea",
            "maxLength": 32000,
            "visibleRows": 2
        },
        {
            "id": "Email",
            "isRequired": false,
            "dataType": "email"
        },
        {
            "id": "Fax",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "FirstName",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Industry",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "LastName",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "LeadSource",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "MobilePhone",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "NumberOfEmployees",
            "isRequired": false,
            "dataType": "int"
        },
        {
            "id": "Phone",
            "isRequired": false,
            "dataType": "phone"
        },
        {
            "id": "PostalCode",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Rating",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "Salutation",
            "isRequired": false,
            "dataType": "picklist",
            "picklistValues": "Mr.,Ms.,Mrs.,Dr.,Prof."
        },
        {
            "id": "State",
            "isRequired": false,
            "dataType": "picklist",
            "picklistValues": "AK::AK,AL::AL,AR::AR,AZ::AZ,CA::CA,CO::CO,CT::CT,DE::DE,FL::FL,GA::GA,HI::HI,IA::IA,ID::ID,IL::IL,IN::IN,KS::KS,KY::KY,LA::LA,MA::MA,MD::MD,ME::ME,MI::MI,MN::MN,MO::MO,MS::MS,MT::MT,NC::NC,ND::ND,NE::NE,NH::NH,NJ::NJ,NM::NM,NV::NV,NY::NY,OH::OH,OK::OK,OR::OR,PA::PA,RI::RI,SC::SC,SD::SD,TN::TN,TX::TX,UT::UT,VA::VA,VT::VT,WA::WA,WI::WI,WV::WV,WY::WY"
        },
        {
            "id": "Street",
            "isRequired": false,
            "dataType": "textarea",
            "maxLength": 2000,
            "visibleRows": 2
        },
        {
            "id": "Title",
            "isRequired": false,
            "dataType": "picklist"
        }
    ]
}
```

프로그램 구성원 사용자 지정 필드의 경우 [사용 가능한 양식 프로그램 구성원 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getAllProgramMemberFieldsUsingGET) 끝점을 호출하십시오. 응답에는 프로그램 멤버 사용자 지정 필드 데이터 형식 및 기본 메타데이터가 포함됩니다.

이러한 필드를 사용하려면 양식이 Design Studio가 아닌 프로그램 아래에 있어야 합니다. 이러한 필드가 있는 양식이 포함된 랜딩 페이지는 프로그램 아래에 있어야 합니다. Design Studio에 있거나 복제할 수 없습니다.

```http
GET /rest/asset/v1/form/programMemberFields.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "109c6#16fa0b9c51a",
    "warnings": [],
    "result": [
        {
            "id": "pMCFCustomField01",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "pMCFCustomField02",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        },
        {
            "id": "myPMCF",
            "isRequired": false,
            "dataType": "string",
            "maxLength": 255
        }
    ]
}
```

### 필드 편집

각 양식에는 양식이 로드될 때 사용자에게 표시되는 편집 가능한 필드 목록이 있습니다. 해당 끝점을 사용하여 한 번에 하나의 필드를 추가, 업데이트 또는 삭제합니다.

[필드를 추가](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFieldToAFormUsingPOST)하려면 부모 양식 ID와 필드 `fieldId`을(를) 제공하세요. 다른 모든 속성은 비어 있거나 필드의 데이터 형식 및 메타데이터를 기반으로 기본값을 사용합니다.

데이터를 JSON이 아닌 `application/x-www-form-urlencoded`이(가) 있는 게시물로 보냅니다.

```http
POST /rest/asset/v1/form/{id}/fields.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
fieldId=NumberOfEmployees&maxLength=125&defaultValue=this is default&required=true&fieldWidth=100&validationMessage=hey, you there?&label=employee count&hintText=Hint me&minValue=10
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "1826e#154f41b214c",
    "result": [
        {
            "id": "NumberOfEmployees",
            "label": "employee count",
            "fieldWidth": 100,
            "dataType": "number",
            "defaultValue": "this is default",
            "validationMessage": "hey, you there?",
            "rowNumber": 5,
            "columnNumber": 0,
            "required": true,
            "formPrefill": true,
            "fieldMetaData": {
                "minValue": 10,
                "maxValue": null
            },
            "visibilityRules": {
                "ruleType": "alwaysShow"
            },
            "hintText": "Hint me"
        }
    ]
}
```

업데이트는 필드를 추가할 때 사용되는 것과 동일한 속성을 편집할 수 있습니다. 또한 양식 ID와 `fieldId`이(가) 필요하지만 업데이트 끝점은 쿼리 매개 변수가 아닌 경로 매개 변수로 `fieldId`을(를) 전달합니다.

```http
POST /rest/asset/v1/form/{id}/field/LastName.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
label=enter the last name here
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "5634#15508303abb",
    "result": [
        {
            "id": "LastName",
            "label": "enter the last name here",
            "dataType": "text",
            "validationMessage": "This field is required.",
            "rowNumber": 0,
            "columnNumber": 0,
            "maxLength": 255,
            "required": false,
            "formPrefill": true,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            }
        }
    ]
}
```

앞의 예제에서는 간단한 문자열 필드인 `LastName`을(를) 업데이트합니다. 다른 양식 필드에는 더 복잡한 메타데이터가 있습니다. 예를 들어 `Salutation`은(는) 항목 목록과 기본값이 있는 `select` 필드입니다.

선택 필드를 추가하거나 업데이트할 때 선택 항목의 `isDefault` 값을 `true`(으)로 설정하십시오. 그렇지 않으면 첫 번째 선택 항목에 값이 없고 레이블이 `Select...`(으)로 지정됩니다.

![인사말](assets/form-field-salutation.png)

목록 항목을 업데이트하려면 다음 예제와 같이 `values` 매개 변수의 형식을 지정하십시오.

```http
POST /rest/asset/v1/form/{id}/field/Salutation.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```sql
values=[{"label":"Select...","value":"","isDefault":true,"selected":true}, {"label":"MR","value":"MR"}, {"label":"MS","value":"MS"}, {"label":"MRS","value":"MRS"}, {"label":"DR","value":"DR"}, {"label":"PROF","value":"PROF"}]
```

```json
{
  "success": true,
  "warnings": [ ],
  "errors": [ ],
  "requestId": "71fd#1588d9d1b0c",
  "result": [
    {
      "id": "Salutation",
      "label": "Salutation:",
      "dataType": "select",
      "validationMessage": "This field is required.",
      "rowNumber": 3,
      "columnNumber": 0,
      "required": false,
      "formPrefill": true,
      "fieldMetaData": {
        "multiSelect": false,
        "values": [
          {
            "label": "Select...",
            "value": "",
            "isDefault": true,
            "selected": true
          },
          {
            "label": "MR",
            "value": "MR"
          },
          {
            "label": "MS",
            "value": "MS"
          },
          {
            "label": "MRS",
            "value": "MRS"
          },
          {
            "label": "DR",
            "value": "DR"
          },
          {
            "label": "PROF",
            "value": "PROF"
          }
        ],
        "visibleLines": 1
      },
      "visibilityRules": {
        "ruleType": "alwaysShow"
      }
    }
  ]
}
```

양식에 필드 추가 응답을 사용하여 복잡한 양식 필드를 포맷하는 방법을 결정합니다.

### 필드 재정렬

[양식 필드 위치 변경](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/updateFieldPositionsUsingPOST) 끝점을 사용하여 모든 양식 필드를 단일 단위로 다시 정렬하십시오. 끝점에 `positions`이(가) 필요합니다. JSON 개체 배열에는 다음과 같은 3개의 멤버가 있습니다.

- `columnNumber`
- `rowNumber`
- 필드 ID를 참조하는 `fieldName`

양식 필드는 최대 3개의 열과 10개의 행이 있는 표와 같은 배열을 사용합니다. 행 및 열 인덱스는 0에서 시작하므로 첫 번째 행과 열은 모두 0을 사용합니다. 모든 필드는 고유한 위치를 차지해야 합니다.

대상 필드가 필드 집합인 경우 `positions`의 레코드에도 `fieldList`이(가) 있어야 합니다. 이 매개 변수는 동일한 `columnNumber`, `rowNumber` 및 `fieldName` 멤버를 가진 개체 배열입니다.

상위 목록은 필드 세트를 하나의 필드로 처리합니다. `fieldList`의 위치에 따라 자식 필드의 배열이 결정됩니다.

```http
POST /rest/asset/v1/form/{id}/reArrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[{"columnNumber":0,"rowNumber":0,"fieldName":"FirstName"},{"columnNumber":0,"rowNumber":1,"fieldName":"LastName"}, {"columnNumber":0,"rowNumber":2, "fieldName":"Email"}]
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "bb18#15508ef9c04",
    "result": [
        {
            "id": 764
        }
    ]
}
```

### 리치 텍스트

[개별 끝점](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addRichTextFieldUsingPOST)을 사용하여 서식 있는 텍스트 필드를 추가합니다. `multipart/form-data` 요청에서 콘텐츠를 HTML으로 전달합니다. HTML에는 스크립트, 메타 태그 또는 링크 태그가 없어야 합니다.

```http
POST /rest/asset/v1/form/{id}/richText.json
```

```html
Content-Type: multipart/form-data; boundary=---------------------------9051914041544843365972754266
-----------------------------9051914041544843365972754266
Content-Disposition: form-data; name="text"
Content-Type: text/html
<div>Fancy Rich Text Component</div>
-----------------------------9051914041544843365972754266--
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "82c8#154f423bf5c",
    "result": [
        {
            "id": "SHRtbFRleHRfMjAxNi0wNS0yN1QxNDozNDoyNC4xMTVa",
            "labelWidth": 260,
            "dataType": "htmltext",
            "rowNumber": 8,
            "columnNumber": 0,
            "visibilityRules": {
                "ruleType": "alwaysShow"
            },
            "text": "<div>Fancy Rich Text Component</div>"
        }
    ]
}
```

### 필드 세트

필드 세트는 선택적 필드 그룹입니다. 최상위 필드 목록은 위치 지정 및 가시성 규칙을 위한 필드 세트를 하나의 필드로 처리합니다. 예를 들어 준수 요구 사항 필드에 대해 예를 선택하면 HIPAA 및 PCI 준수 필드가 포함된 필드 세트가 표시될 수 있습니다.

필드는 양식 내에서 고유해야 합니다. 동일한 필드가 양식의 상위 필드 목록과 하위 필드 세트 모두에 나타날 수 없습니다.

[Form](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFieldSetUsingPOST) 끝점에 필드 집합 추가를 사용하여 필드 집합을 추가하십시오. 그러면 필드 집합이 [Get Fields for Form](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/getFormFieldByFormVidUsingGET) 응답에 나타납니다. 필드 집합에 필드를 추가하려면 [필드 위치 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/updateFieldPositionsUsingPOST)를 사용하여 해당 필드를 `fieldList`(으)로 이동하세요.

이러한 끝점의 경우 데이터를 JSON이 아닌 `application/x-www-form-urlencoded`이(가) 있는 POST로 보냅니다.

## 가시성 규칙

가시성 규칙은 양식에 입력한 값을 기반으로 방문자가 필드를 볼 수 있는지 여부를 결정합니다. 각 규칙은 양식의 `subjectField` 값을 규칙의 값 목록과 비교합니다.

필드에는 가시성 규칙 유형 `show`, `hide` 또는 `alwaysShow`이(가) 있을 수 있습니다. API는 필드의 규칙을 위에서 아래로 평가하고 참으로 평가하는 첫 번째 규칙을 적용합니다.

가시성 규칙을 변경하는 것은 파괴적인 업데이트입니다.

```http
POST /rest/asset/v1/form/{id}/field/Email/visibility.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
visibilityRule={"ruleType":"show", "rules":[{"subjectField": "LastName", "operator": "isNotEmpty", "values": [], "altLabel": "Email:"}]}
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "ab4a#15509030601",
    "result": [
        {
            "formFieldId": "Email",
            "ruleType": "show",
            "rules": [
                {
                    "subjectField": "LastName",
                    "operator": "isNotEmpty",
                    "values": [],
                    "altLabel": "Email:"
                }
            ]
        }
    ]
}
```

전체 연산자 목록은 [양식 필드 가시성 규칙 추가](https://developer.adobe.com/marketo-apis/api/asset#tag/Form-Fields/operation/addFormFieldVisibilityRuleUsingPOST)를 참조하십시오.

## 후속 작업

동적 후속 규칙은 제출 시 지정된 필드 값을 기반으로 방문자를 페이지로 리디렉션하거나 현재 페이지에 유지할 수 있습니다. 감사 페이지 규칙 및 후속 페이지 규칙은 동일한 동작을 참조합니다.

레코드에 `followupType`, `followupValue`, `operator`, `subjectField`, `values` 및 `default`이(가) 포함된 JSON 배열로 규칙을 나타냅니다. 배열에 있는 한 레코드만 부울 `default`을(를) `true`(으)로 설정할 수 있습니다. 방문자가 다른 규칙에 적합하지 않을 때 양식에서 해당 레코드를 사용합니다.

`followupType` 값은 `lp` 또는 `url`일 수 있습니다. `lp` 값은 `followupValue`이(가) Marketo 랜딩 페이지 ID임을 나타냅니다. `url` 값은 `followupValue`이(가) 다른 페이지의 URL임을 나타냅니다. 연산자는 제목 필드 값을 제공된 값과 비교합니다.

## 전송 단추

[전송 단추 업데이트](https://developer.adobe.com/marketo-apis/api/asset#tag/Forms/operation/updateFormSubmitButtonUsingPOST) 끝점을 사용하여 전송 단추 스타일을 수정합니다. `buttonPosition`, `buttonStyle`, `label` 및 `waitingLabel`을(를) 업데이트할 수 있습니다. 제출이 보류 중인 동안 `waitingLabel`이(가) 나타납니다.

파괴적인 업데이트입니다.

## 승인

Forms은 초안이 승인한 라이프사이클을 따릅니다. 양식에는 초안 버전, 승인된 버전 또는 둘 다가 있을 수 있습니다. 업데이트는 항상 초안에 적용되며 승인 후에만 활성화됩니다.

양식을 승인하면 기존의 승인된 버전이 현재 초안으로 바뀝니다. 라이브 양식 승인을 취소하면 현재 초안이 모두 삭제되고 승인된 버전은 초안 전용 상태로 강등됩니다. 양식을 삭제하기 전에 항상 승인을 취소하십시오.

## 점진적 프로파일링

점진적 프로파일링을 사용하는 경우 양식 필드 목록에 이름이 `Profiling`인 필드 집합이 포함됩니다. 필드 위치 업데이트 끝점을 사용하여 점진적 프로파일링 목록에서 필드를 추가하거나 제거합니다.

이 끝점은 원본에 영향을 주는 업데이트를 수행하므로 모든 요청에는 양식의 모든 필드가 포함되어야 합니다. 다음 예제에서는 `Phone`을(를) 점진적 프로파일링 목록에 추가합니다.

```http
POST /rest/asset/v1/form/{id}/reArrange.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
positions=[{"columnNumber":0,"rowNumber":0,"fieldName":"Email"},{"columnNumber":0,"rowNumber":1,"fieldName":"LastName"},{"columnNumber":0,"rowNumber":2,"fieldName":"Company"},{"columnNumber":0,"rowNumber":3,"fieldName":"Website"},{"columnNumber":0,"rowNumber":4,"fieldName":"Profiling","fieldList":[{"columnNumber":0,"rowNumber":0,"fieldName":"Phone"}]}]
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "3d6a#164190dbdf2",
    "result": [
        {
            "id": 1031
        }
    ]
}
```
