---
title: 예
description: 제출 시 숨기거나 리디렉션하고, 필드를 설정하고 읽고, 사용자 지정 오류, Lightbox 및 외부 트리거를 사용하여 유효성 검사를 수행하는 Marketo Forms 2.0 JavaScript 사례입니다.
feature: Javascript
exl-id: dc5f0cc5-ff5a-48b0-be36-52c10e56f798
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 예

아래에는 일련의 데모 가능한 Forms 2.0 웹 양식 예제가 있습니다.

## 제출 후 양식 숨기기

이 예제에서는 방문자를 후속 페이지로 이동하거나 현재 페이지를 다시 로드하지 않습니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Add an onSuccess handler
    form.onSuccess(function(values, followUpUrl) {
        // Get the form's jQuery element and hide it
        form.getFormElem().hide();
        // Return false to prevent the submission handler from taking the lead to the follow up url
        return false;
    });
});
```

## 방문자를 사용자 정의 URL로 이동

이 예에서는 방문자를 구성된 감사 페이지가 아닌 제출 후 JavaScript에서 결정한 URL로 안내합니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    //Add an onSuccess handler
    form.onSuccess(function(values, followUpUrl) {
        // Take the lead to a different page on successful submit, ignoring the form's configured followUpUrl
        location.href = "https://google.com/?q=marketo+forms+v2+examples";
        // Return false to prevent the submission handler continuing with its own processing
        return false;
    });
});
```

## 양식 필드 값 설정

이 예에서는 양식 필드를 설정합니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Set the value of the Phone and Country fields
    form.vals({ "Phone":"555-555-1234", "Country":"USA"});
});
```

## 양식 제출에서 양식 필드 값 읽기

이 예제는 양식 제출의 양식 필드를 읽습니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function(form) {
    // Add an onSubmit handler
    form.onSubmit(function(){
        // Get the form field values
        var vals = form.vals();
        // You may wish to call other function calls here, for example to fire google analytics tracking or the like
        // callSomeFunction(vals);
        // We'll just alert them to show the principle
        alert("Submitted values: " + JSON.stringify(vals));
    });
});
```

## 양식이 아닌 클릭 이벤트에서 양식 제출

이 예제에서는 양식에 속하지 않은 다른 요소나 이벤트의 클릭 이벤트를 기반으로 양식을 제출합니다.

```javascript
// Load the form normally
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057);

// Find the button element that you want to attach the event to
var btn = document.getElementById("MyAlternativeSubmitButtonId");
btn.onclick = function() {
    // When the button is clicked, get the form object and submit it
    MktoForms2.whenReady(function (form) {
        form.submit();
    });
};
```

## 사용자가 양식을 전송하지 못하도록 방지

이 예제에서 양식에 대한 제출 단추가 작동하려면 클릭 카운터 단추를 세 번 이상 클릭해야 합니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) {
    // Check if the form is submittable
    if (form.submittable()) {
        // Set it to be non submittable
        form.submittable(false);
    }
});

var clickCount = 0;
// Wire up the click counter button
var clickCounterBtn = document.getElementById("ClickCounter");
clickCounterBtn.onclick = function() {
    clickCount++;
    // Update the buttons's text
    clickCounterBtn.innerHTML = "Click Counter Button ("+clickCount+")";

    if (clickCount >= 3) {
        // Get the form and set it to be submittable
        MktoForms2.whenReady(function (form) {
            form.submittable(true);
        });
    }
};
```

## 양식의 숨겨진 필드에 값 설정

이 예제에서는 숨겨진 필드에 값을 설정합니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) {
    // Set values for the hidden fields, "userIsAwesome" and "enrollDate"
    // Note that these fields were configured in the form editor as hidden fields already
    form.vals({"userIsAwesome":"true", "enrollDate":"2014-01-01"});
});
```

## LightBox에 양식 표시

이 예제에서는 URL에 `lightboxForm=true` 매개 변수가 포함된 경우 Lightbox 스타일 대화 상자에 양식을 표시합니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) {
    if (location.href.indexOf("lightboxForm=true") != -1) {
        MktoForms2.lightbox(form).show();
    }
});
```

## 사용자 지정 오류 메시지 표시

이 예는 사용자 정의 비즈니스 논리를 기반으로 한 제출 시 사용자 정의 오류 메시지를 보여줍니다.

```javascript
MktoForms2.loadForm("//app-ab00.marketo.com", "785-UHP-775", 1057, function (form) {
    //listen for the validate event
    form.onValidate(function() {
        // Get the values
        var vals = form.vals();
        //Check your condition
        if (vals.Country == "USA" && vals.vehicleSize != "Massive") {
            // Prevent form submission
            form.submittable(false);
            // Show error message, pointed at VehicleSize element
            var vehicleSizeElem = form.getFormElem().find("#vehicleSize");
            form.showErrorMessage("All Americans must have a massive vehicle", vehicleSizeElem);
        }
        else {
            // Enable submission for those who met the criteria
            form.submittable(true);
        }
  });
});
```
