---
title: Forms API 참조
description: MktoForms2 및 양식 메서드, 매개 변수, 콜백, 양식 로드 및 렌더링에 대한 반환 등을 자세히 설명하는 Marketo Forms 2.0 API에 대한 포괄적인 참조입니다.
feature: Forms, Javascript
exl-id: 0f8d242f-0b27-4087-b080-3d41ebaa25b3
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 1%

---

# Forms API 참조

Forms 2.0 API를 사용하여 상호 작용할 두 개의 기본 개체가 있습니다. `MktoForms2` 개체와 `Form` 개체. `MktoForms2` 개체는 Forms2 기능에 대해 공개적으로 표시되는 최상위 네임스페이스이며, Form 개체를 만들고, 로드하고, 가져오는 함수를 포함합니다.

## MktoForms2 메서드

<table>
  <tbody>
    <tr valign="top">
      <td><strong>메서드</strong></td>
      <td><strong>설명</strong></td>
      <td><strong>매개변수</strong></td>
      <td><strong>반환</strong></td>
    </tr>
    <tr valign="top">
      <td>.loadForm(baseUrl, munchkinId, formId, callback)</td>
      <td>Marketo 서버에서 양식 설명자를 로드하고 새 양식 개체를 만듭니다.</td>
      <td> baseUrl(String) - 구독의 Marketo 서버 인스턴스에 대한 URL</td>
      <td>정의되지 않음</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>munchkinId(문자열) - 구독의 Munchkin ID</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>formId(문자열 또는 숫자) - 로드할 양식의 양식 버전 ID(Vid)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback (선택 사항) (함수) - 생성된 양식 개체가 로드되고 초기화되면 이를 전달하는 콜백 함수입니다.</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.lightbox(form, opts)</td>
      <td>Form 개체가 있는 Lightbox 스타일 모달 대화 상자를 렌더링합니다.</td>
      <td>form(양식 개체) - lightbox에서 렌더링하려는 Form 개체의 인스턴스입니다.</td>
      <td>.show() 및 .hide() 메서드가 있는 lightbox 개체입니다.</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>opts (optional)(Object) - lightbox 개체에 전달된 옵션 개체</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>onSuccess(Function) - 양식 제출 시 트리거되는 콜백입니다.</td>
      <td></td>
    </tr>
    <tr>
          <td></td>
      <td></td>
      <td>closeBtn(Boolean) default true - Lightbox 대화 상자에 닫기 단추(X)가 표시되는지 여부를 제어합니다.</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.newForm(formData, callback)</td>
      <td>Form Descriptor JS 개체에서 새 Form 개체를 만듭니다. 모든 스타일시트와 알려진 리드 정보를 가져오고 Form 개체가 생성되면 호출되는 콜백 함수를 추가합니다.</td>
      <td>formData (Form Descriptor Object) - Marketo Forms V2 편집기에서 만든 양식 설명자 개체</td>
      <td>정의되지 않음</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>callback (선택 사항)(함수) - 이 콜백은 Form 개체의 새로 만든 인스턴스인 단일 인수로 호출됩니다.</td>
      <td></td>
    </tr>
    <tr valign="top">
      <td>.getForm(formId)</td>
      <td>양식 식별자로 이전에 만든 양식 개체를 가져옵니다.</td>
      <td> formId(숫자 또는 문자열) - 양식 Vid 식별자.</td>
      <td>양식 개체</td>
    </tr>
    <tr valign="top">
      <td>.allForms()</td>
      <td>페이지에서 이전에 구성한 모든 양식 개체의 배열을 가져옵니다.</td>
      <td>해당 사항 없음</td>
      <td>양식 개체 배열</td>
    </tr>
    <tr valign="top">
      <td>.getPageFields()</td>
      <td>URL 및 레퍼러의 데이터가 포함된 JS 개체를 가져옵니다. 이 개체는 추적 목적으로 유용할 수 있습니다.</td>
      <td>해당 사항 없음</td>
      <td>오브젝트</td>
    </tr>
    <tr valign="top">
      <td>.whenReady(callback)</td>
      <td>페이지에서 "준비"된 각 양식에 대해 정확히 한 번 호출되는 콜백을 추가합니다. 준비 는 양식이 존재하고, 처음에 렌더링되고, 초기 콜백이 호출되었음을 의미합니다. 이 함수를 호출할 때 이미 준비된 양식이 있으면 전달된 콜백이 즉시 호출됩니다.</td>
      <td>callback(Function) - 콜백에 단일 인수인 양식 개체가 전달됩니다.</td>
      <td>MktoForms2 개체</td>
    </tr>
    <tr valign="top">
      <td>.onFormRender(callback)</td>
      <td>페이지의 모든 양식이 렌더링될 때마다 호출되는 콜백을 추가합니다. Forms은 처음 만들 때 렌더링되며, 표시 규칙 이 양식의 구조를 변경할 때마다 렌더링됩니다.</td>
      <td>callback (함수) - 콜백에 렌더링된 양식의 양식 객체인 단일 인수가 전달됩니다.</td>
      <td>MktoForms2 개체</td>
    </tr>
    <tr valign="top">
      <td>.whenRendered(callback)</td>
      <td>onFormRender와 마찬가지로 이 함수는 양식이 렌더링될 때마다 호출되는 콜백을 추가합니다. 또한 이미 렌더링된 모든 양식에 대해 콜백을 즉시 호출합니다.</td>
      <td>callback(Function) - 콜백이 렌더링된 양식의 양식 객체인 단일 인수로 전달됩니다.</td>
      <td></td>
    </tr>
</table>

## 양식 메서드

<table>
  <tbody>
    <tr valign="top">
      <td><strong>메서드</strong></td>
      <td><strong>설명</strong></td>
      <td><strong>매개변수</strong></td>
      <td><strong>반환</strong></td>
    </tr>
    <tr valign="top">
      <td>.render(formElem)</td>
      <td>양식 개체를 렌더링하여 양식이 포함된 양식 요소를 래핑하는 jQuery 개체를 반환합니다. formElem을 전달하면 양식 요소로 사용되고, 그렇지 않으면 새 양식이 만들어집니다.</td>
      <td>formElem (선택 사항) - 렌더링할 jQuery 개체가 래핑된 양식 요소입니다.</td>
      <td> 렌더링된 양식이 들어 있는 jQuery 개체가 래핑된 양식 요소입니다.</td>
    </tr>
    <tr valign="top">
      <td>.getId()</td>
      <td>양식 ID를 가져옵니다.</td>
      <td>해당 사항 없음</td>
      <td>숫자 - 이 양식이 나타내는 양식 개체의 ID입니다.</td>
    </tr>
    <tr valign="top">
      <td>.getFormElem()</td>
      <td>렌더링된 양식의 jQuery 래핑된 양식 요소를 가져옵니다.</td>
      <td>해당 사항 없음</td>
      <td>jQuery 개체가 래핑된 양식 요소이거나 아직 render() 메서드를 사용하여 양식을 렌더링하지 않은 경우 null입니다.</td>
    </tr>
    <tr valign="top">
      <td>.validate()</td>
      <td>양식의 유효성을 검사하여 존재할 수 있는 오류를 강조 표시하고 결과를 반환합니다. 양식을 제출하지 않습니다.</td>
      <td>해당 사항 없음</td>
      <td>부울 - 양식의 모든 유효성 검사기가 전달되면 true를 반환하고 그렇지 않으면 false를 반환합니다.</td>
    </tr>
    <tr valign="top">
      <td>.onValidate(callback)</td>
      <td>유효성 검사가 트리거될 때마다 호출되는 유효성 검사 콜백을 추가합니다.</td>
      <td>callback(Function) - 유효성 검사가 발생할 때마다 트리거되는 콜백입니다. 콜백에는 유효성 검사가 성공했는지 여부를 나타내는 부울 매개 변수 하나가 전달됩니다.</td>
      <td>양식 개체 - 체인 목적으로 메서드가 호출된 동일한 양식 개체.</td>
    </tr>
    <tr valign="top">
      <td>.submit()</td>
      <td>양식의 제출 이벤트를 트리거합니다. 이렇게 하면 양식 제출이 성공적으로 수행된 경우 제출 플로우에서 가 시작되고, 유효성 검사가 수행되며, 모든 onSubmit 이벤트가 실행되고, 양식이 제출되고, 모든 onSuccess 이벤트가 실행됩니다.</td>
      <td>해당 사항 없음</td>
      <td>양식 개체 - 체인 목적으로 메서드가 호출된 동일한 양식 개체.</td>
    </tr>
    <tr valign="top">
      <td>.onSubmit(callback)</td>
      <td>양식 제출 시 호출될 콜백을 추가합니다. 요청의 성공/실패를 알리기 전에 제출이 시작되면 이 작업이 실행됩니다.</td>
      <td>callback - 양식 제출 시 호출되는 함수입니다. 이 콜백에는 하나의 인수, 이 Form 개체가 전달됩니다.</td>
      <td>양식 개체 - 체인 목적으로 메서드가 호출된 동일한 양식 개체.</td>
    </tr>
    <tr valign="top">
      <td>.onSuccess(callback)</td>
      <td>양식이 성공적으로 제출되었지만 잠재 고객이 후속 페이지로 전달되기 전에 호출될 콜백을 추가합니다. 제출 후 잠재 고객이 후속 페이지로 전달되지 않도록 하는 데 사용할 수 있습니다.</td>
      <td>callback - 양식이 성공적으로 제출되었을 때 호출되는 함수입니다. 이 콜백에는 인수 두 개가 전달됩니다. 제출된 값과 사용자가 전달될 후속 페이지의 문자열 URL이 포함된 JS 개체이거나, 구성된 후속 페이지가 없는 경우 null 또는 빈 문자열입니다. 특수 동작: 이 콜백이 'false'(===으로 측정됨)를 반환하는 경우 방문자가 후속 페이지로 전달되지 않고 페이지가 다시 로드되지 않습니다. 이렇게 하면 구현자는 후속 URL에 대한 추가 처리를 수행하거나 페이지를 종료하지 않고 JavaScript을 사용하여 페이지에서 작업을 수행할 수 있습니다.</td>
      <td>양식 개체 - 체인 목적으로 메서드가 호출된 동일한 양식 개체.</td>
    </tr>
    <tr valign="top">
      <td>.submittable(canSubmit) <em>다음 항목으로도 사용 가능:</em> <em>.submitable(canSubmit)</em></td>
      <td>양식을 제출할 수 있는지 여부를 가져오거나 설정합니다. 인수를 사용하지 않고 를 호출하면 값을 가져오고, 인수를 사용하여 를 호출하면 값을 설정합니다. 이렇게 하면 일반 양식 이외의 다른 기준이 충족되는 동안 양식이 제출되지 않도록 방지할 수 있습니다.</td>
      <td>canSubmit (선택 사항) (부울) - 양식을 제출할 수 있도록 설정하거나 제출할 수 없도록 설정합니다.</td>
      <td>부울 또는 양식 개체 - 인수 없이 호출되면 양식을 제출할 수 있는지 여부를 나타내는 부울을 반환합니다. 하나의 인수를 사용하여 호출되면 체인 목적으로 이 양식 개체를 반환합니다. </td>
    </tr>
    <tr valign="top">
      <td>.allFieldsFilled()</td>
      <td>양식의 모든 필드에 비어 있지 않은 값이 설정되어 있으면 true를 반환합니다.</td>
      <td>해당 사항 없음</td>
      <td>부울 - 모든 필드에 비어 있지 않은/비어 있는/unset/null 값이 있으면 True이고, 그렇지 않으면 False입니다.</td>
    </tr>
    <tr valign="top">
      <td>.setValues(vals)</td>
      <td>양식에 있는 하나 이상의 필드에 값을 설정합니다.</td>
      <td>vals - JS 개체. 개체의 각 키/값 쌍에 대해 이름이 key인 양식 필드는 value로 설정됩니다.</td>
      <td>정의되지 않음</td>
    </tr>
    <tr valign="top">
      <td>.getValues()</td>
      <td>양식에 있는 모든 필드의 값을 모두 가져옵니다.</td>
      <td>해당 사항 없음</td>
      <td>개체 - 양식에 있는 필드의 이름과 값을 나타내는 키/값 쌍을 포함하는 JS 개체입니다.</td>
    </tr>
    <tr valign="top">
      <td>.addHiddenFields(values)</td>
      <td>입력 type=hidden 필드를 양식에 추가합니다.</td>
      <td>값 - 양식에 추가할 숨겨진 필드의 이름 및 값을 나타내는 키/값 쌍이 포함된 JS 개체입니다.</td>
      <td>정의되지 않음</td>
    </tr>
    <tr valign="top">
      <td>.vals(values)</td>
      <td>jQuery style .vals() setter/getter. 인수를 사용하지 않고 를 호출하는 경우 는 getValues()를 호출하는 것과 같습니다. 하나의 인수로 호출되는 경우 는 setValues()를 호출하는 것과 같습니다</td>
      <td>값(선택 사항) - 오브젝트</td>
      <td>정의되지 않음</td>
    </tr>
    <tr valign="top">
      <td>.showErrorMessage(msg, elem)</td>
      <td>요소를 가리키는 오류 메시지를 표시합니다.</td>
      <td>msg (HTML의 문자열) - 표시할 오류 텍스트가 포함된 문자열입니다.</td>
            <td>양식 개체 - 이 양식 개체(체인용).</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>elem (선택 사항)(jQuery 개체) - 가리킬 오류에 대한 요소입니다. 설정을 해제하면 양식의 제출 버튼이 사용됩니다.</td>
<td></td>
    </tr>
  </tbody>
</table>
