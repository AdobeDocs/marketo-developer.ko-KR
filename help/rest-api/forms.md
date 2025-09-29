---
title: 양식
feature: REST API, Forms
description: 양식 만들기 및 관리, id 또는 이름별로 검색, 상태 필터 찾아보기, 필드, 필드 세트 및 규칙 관리를 위한 Marketo Forms REST API 안내서.
exl-id: 2e5dfa70-3163-4ab4-b269-3112417714c3
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 1%

---

# 양식

[Forms 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms)

[양식 필드 끝점 참조](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields)

Marketo forms에는 원격 시스템에서 양식 관리를 완전히 제어할 수 있는 복잡한 엔드포인트 세트가 있습니다. 양식의 일부로 관리해야 하는 Forms, 필드, 필드 세트, 가시성 규칙 및 후속 페이지 규칙과 같은 다양한 유형의 개체가 있으므로 양식의 구조는 복잡할 수 있습니다.

## 쿼리

Forms은 자산 검색의 표준 방법인 [id별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET), [이름별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET) 및 [탐색별](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET)을 지원합니다. 각 양식 응답에는 필드 목록을 제외한 모든 속성이 포함됩니다.

### ID별

[ID별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByIdUsingGET)는 `id` 양식을 경로 매개 변수로 사용하고 양식 레코드를 반환합니다.

```
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

[이름별 양식 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET)에서는 `name` 양식을 경로 매개 변수로 사용하고 양식 레코드를 반환합니다.

```
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

[Forms 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/browseForms2UsingGET) 양식은 다른 Asset API 검색 끝점과 동일하게 작동하며 `status`, `maxReturn` 및 `offset`에서 선택적 필터링을 허용합니다. 상태는 승인됨, 승인됨, 초안 또는 초안일 수 있습니다.

```
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

양식의 필드 목록 검색은 양식별로 수행됩니다.

```
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

필드 또는 양식 내 해당 동작을 편집할 때 편집을 시도하기 전에 필드 목록을 항상 검색해야 합니다. 이렇게 하면 업데이트하거나 삭제할 때 적절한 필드 ID를 제공할 수 있습니다.

### 필드 유형

| UI 유형 | API 이름 |
|--------------|-----------------|
| 확인란 | 확인란 |
| 라디오 단추 | 라디오 |
| 텍스트 영역 | 텍스트 영역 |
| 선택 목록 | 선택 목록 |
| 문자열 | 문자열 |
| 이메일 | 이메일 |
| Date | 날짜 |
| 숫자 | 번호 |
| 더블 | 더블 |
| 전화 | 전화 |
| URL | url |
| 통화 | 통화 |
| 확인란 | single_checkbox |
| 슬라이더 | 범위 |

### 종속성

[Get Form Used By](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getFormUsedByUsingGET) 끝점은 `id` 양식을 경로 매개 변수로 사용하고 양식에 종속된 자산 목록을 반환합니다. Forms은 랜딩 페이지, 스마트 목록, 스마트 캠페인, 보고서, 이메일 프로그램 등의 자산 유형에서 사용할 수 있습니다.

```
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

[양식을 만들 때](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/createLpFormsUsingPOST) 필수 필드에는 양식의 상위 폴더와 양식 이름이 두 개만 있습니다. 다른 모든 매개 변수는 기본값과 함께 선택 사항입니다. 양식이 만들어지면 세 개의 기본 필드(이름, 성, 이메일)가 제공됩니다.

```
POST /rest/asset/v1/forms.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

Forms이 id를 통해 유사한 호출을 사용하여 [업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormsUsingPOST)되었습니다. 만들거나 업데이트하는 동안 기본 스타일 매개 변수에 액세스하고 이를 편집할 수 있으므로 양식을 최종 사용자에게 표시하는 방법을 수정할 수 있습니다.

```
POST /rest/asset/v1/form/736.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

알려진 방문자 및 감사 페이지 동작은 만들기 또는 업데이트 양식 호출을 통해 수정할 수 없으며 해당 끝점을 통해 액세스해야 합니다.

## 필드 메타데이터

양식에 속하는 필드를 올바르게 추가하거나 편집하려면 대상 인스턴스에 대해 유효한 필드 목록을 검색해야 합니다. 필드 상호 작용은 항상 결과의 각 항목에 대해 표시되는 필드의 ID 속성을 기반으로 수행됩니다.

리드 필드의 경우 [사용 가능한 양식 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllFieldsUsingGET) 끝점을 사용하여 이 작업을 수행하고, 양식에 추가될 때 필드의 데이터 형식 및 기본 메타데이터를 포함합니다.

```
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

프로그램 구성원 사용자 지정 필드의 경우 [사용 가능한 양식 프로그램 구성원 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getAllProgramMemberFieldsUsingGET)를 호출하십시오.  프로그램 멤버 사용자 지정 필드 데이터 형식 및 기본 메타데이터를 검색할 종단점입니다. 폼에서 이러한 필드를 사용하려면 폼이 Design Studio가 아닌 프로그램 아래에 있어야 합니다. 이러한 필드를 사용하는 양식이 포함된 랜딩 페이지는 프로그램 아래에도 있어야 합니다(Design Studio에 상주하거나 Design Studio에 복제할 수 없음).

```
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

각 양식에는 로드할 때 최종 사용자에게 표시되는 편집 가능한 필드 목록이 포함되어 있습니다. 각 필드는 해당 끝점을 통해 필드 목록에서 한 번에 하나씩 추가, 업데이트 또는 삭제됩니다.

[필드를 추가](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldToAFormUsingPOST)하려면 부모 폼의 ID와 필드의 fieldId만 필요합니다. 다른 모든 필드는 비어 있거나 데이터 형식 및 필드 메타데이터를 기반으로 하는 기본값을 가집니다. 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

```
POST /rest/asset/v1/form/{id}/fields.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

업데이트는 필드를 추가할 때와 동일한 모든 필드를 편집할 수 있으며, 필드 ID가 경로 매개 변수이고 업데이트 수행 시 쿼리 매개 변수가 아니라는 점을 제외하고 마찬가지로 양식 ID와 필드 ID가 필요합니다.

```
POST /rest/asset/v1/form/{id}/field/LastName.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

위의 예에서는 간단한 문자열인 LastName 필드를 업데이트합니다. 일부 양식 필드는 더 복잡합니다. 예를 들어 인사말 필드는 항목 목록과 기본값을 포함하는 &quot;select&quot; 필드 유형입니다. 선택 항목 중 하나를 true의 `isDefault` 값으로 설정하지 않는 한 선택 항목 필드를 추가하거나 업데이트하면 첫 번째 선택 항목에 값이 없고 &quot;선택...&quot;이라는 레이블이 지정됩니다.

![인사말](assets/form-field-salutation.png)

목록 항목을 업데이트하기 위해 &quot;values&quot; 매개 변수의 형식은 다음과 같습니다.

```
POST /rest/asset/v1/form/{id}/field/Salutation.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

복잡한 양식 필드의 형식을 지정하는 방법을 결정하려면 양식에 필드 추가에서 응답을 확인하십시오.

### 필드 재정렬

양식의 필드는 [양식 필드 위치 변경](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST) 끝점을 통해 모두 단일 단위로 재배열해야 합니다. 끝점에는 다음 3개의 멤버가 있는 개체의 JSON 배열인 `positions` 매개 변수가 필요합니다.

- 열 번호
- rowNumber
- fieldName( 필드 ID 참조 )

양식의 필드는 최대 3개의 열과 최대 10개의 행이 있는 테이블형 인터페이스로 배열됩니다. 행과 열 모두 0부터 인덱싱되므로 첫 번째 행과 첫 번째 열은 모두 0을 전달하여 나타냅니다. 모든 필드는 고유한 위치를 차지해야 합니다.

대상 필드가 필드 집합인 경우 위치 배열 내의 해당 레코드에도 fieldList라는 매개 변수, 동일한 columnNumber, rowNumber 및 fieldName 멤버를 포함하는 개체 배열이 포함되어야 합니다. 필드 집합 자체는 상위 목록에서 해당 위치에 대한 단일 필드로 처리되지만, 하위 필드는 fieldList 매개 변수에서 지정된 위치에 따라 배치됩니다.

```
POST /rest/asset/v1/form/{id}/reArrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

리치 텍스트 필드가 리드 필드와 [개별 엔드포인트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addRichTextFieldUsingPOST)를 통해 추가됩니다. 필드 콘텐츠는 다중 파트/양식 데이터로 전달됩니다. 스크립트, 메타 태그 또는 링크 태그를 포함하지 않는 HTML 콘텐츠로 구조화해야 합니다.

```
POST /rest/asset/v1/form/{id}/richText.json
```

```
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

Marketo forms에는 필드 세트라는 선택적 구성 요소가 있습니다. 필드 세트는 가시성 규칙에 의한 이동 및 처리를 위해 최상위 필드 목록 내에서 단일 필드로 처리되는 필드 그룹입니다. 예를 들어 준수 요구 사항에 대한 필드가 있고 클라이언트가 예 를 선택하면 HIPAA 및 PCI 준수 요구 사항에 대한 필드가 포함된 필드 세트가 표시될 수 있습니다.

필드 세트 내의 필드는 전체적으로 양식에 고유하므로 중복 필드가 양식의 상위 필드 목록과 하위 필드 세트 모두에 있지 않을 수 있습니다. 필드 집합은 [Form](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFieldSetUsingPOST) 끝점에 필드 집합 추가를 통해 추가되며 [Form에 대한 필드 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/getFormFieldByFormVidUsingGET)의 결과에 나타납니다. [필드 위치 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/updateFieldPositionsUsingPOST)를 통해 필드를 필드 집합의 fieldList로 이동하여 필드 집합에 추가합니다. 이러한 엔드포인트의 경우 데이터는 JSON이 아닌 POST x-www-form-urlencoded로 전달됩니다.

## 가시성 규칙

각 필드에는 양식에 입력한 값에 따라 방문자가 필드를 볼 수 있는지 여부를 결정하는 가시성 규칙 세트가 있을 수 있습니다. 규칙은 양식에 있는 subjectField의 값과 규칙에 지정된 값 목록을 비교합니다. 각 필드에는 가시성 규칙, 표시, 숨기기 또는 항상 표시 유형이 있을 수 있으며, 그런 다음 평가할 규칙 목록이 있을 수 있습니다. 규칙은 위에서 아래로 평가되며 true로 평가되는 첫 번째 규칙이 적용됩니다.

가시성 규칙을 변경하는 것은 파괴적인 업데이트입니다.

```
POST /rest/asset/v1/form/{id}/field/Email/visibility.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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

사용 가능한 연산자의 전체 목록을 보려면 [양식 필드 가시성 규칙 추가](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/operation/addFormFieldVisibilityRuleUsingPOST)에 대한 끝점 참조 페이지를 참조하십시오.

## 후속 작업

Marketo forms에는 제출 시 지정된 필드의 내용에 따라 지정된 페이지로 리디렉션하거나 현재 페이지에 머무르는 규칙이 적용되는 동적 후속 페이지 동작이 있을 수 있습니다. 규칙은 서로 바꿔서 감사 페이지 규칙 또는 후속 페이지 규칙이라고 할 수 있습니다. 이러한 규칙은 `followupType`, `followupValue`, `operator`, `subjectField`, `values` 및 `default` 멤버와 함께 JSON 배열로 표시됩니다. `default`은(는) 배열에 있는 하나의 레코드만 true일 수 있는 부울 값입니다. 방문자가 다른 규칙을 사용할 수 없는 경우 기본값으로 지정된 규칙이 사용됩니다. `followupType`은(는) lp 또는 url일 수 있습니다. 여기서 lp는 `followupValue`에 대한 Marketo 랜딩 페이지 id를 나타내고 url은 다른 페이지에 대한 URL을 나타냅니다. 연산자는 제공된 값 목록과 주제 필드의 값을 비교하는 데 사용됩니다.

## 전송 단추

양식의 전송 단추 스타일은 [전송 단추 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/updateFormSubmitButtonUsingPOST) 끝점으로 관리됩니다. buttonPosition, buttonStyle, label 및 waitingLabel(제출이 보류 중일 때 표시되는 레이블)은 수정할 수 있습니다.

파괴적인 업데이트입니다.

## 승인

다른 대부분의 에셋과 마찬가지로 양식도 초안 버전 및/또는 승인된 버전이 있을 수 있는 초안 승인 모델을 따릅니다. 업데이트는 양식에 적용될 때마다 항상 초안 버전에 먼저 적용되며 양식이 승인된 경우에만 실시간으로 표시됩니다. 양식을 승인하면 현재 초안 버전이 사용되고 승인된 버전이 있는 경우 초안으로 바뀝니다. 양식을 라이브에서 내려야 하는 경우 먼저 승인을 취소해야 하며, 이렇게 하면 현재 초안이 삭제되고 승인된 버전은 초안 전용 상태로 강등됩니다. Forms은 삭제를 시도하기 전에 항상 승인되지 않아야 합니다.

## 점진적 프로파일링

양식에 대해 점진적 프로파일링이 활성화되면 필드 목록에 &quot;프로파일링&quot;이라는 필드 세트가 포함됩니다. 점진적 프로파일링 목록에서 필드를 추가하거나 제거하려면 필드 위치 갱신 끝점을 사용해야 합니다. 이 끝점은 파괴적인 업데이트를 수행하므로 양식의 모든 필드가 각 요청에 포함되어야 합니다. 아래 예제에서는 &quot;Phone&quot; 필드를 점진적 프로파일링 목록에 추가합니다.

```
POST /rest/asset/v1/form/{id}/reArrange.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
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
