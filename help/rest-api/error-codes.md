---
title: 오류 코드
feature: REST API
description: Marketo 오류 코드 설명.
exl-id: a923c4d6-2bbc-4cb7-be87-452f39b464b6
source-git-commit: 9012135dc7a295c2462574dad1aca2d06a9077ea
workflow-type: tm+mt
source-wordcount: '2320'
ht-degree: 3%

---

# 오류 코드

다음은 REST API 오류 코드 목록과 오류가 다시 애플리케이션으로 반환되는 방법에 대한 설명입니다.

## 예외 처리 및 로깅

Marketo용으로 개발할 때 예기치 않은 예외가 발생할 때 요청 및 응답이 기록되는 것이 중요합니다. 만료된 인증과 같은 특정 유형의 예외는 재인증을 통해 안전하게 처리할 수 있지만 다른 예외는 지원 상호 작용이 필요할 수 있으며 이 시나리오에서는 항상 요청 및 응답이 요청됩니다.

## 오류 유형

Marketo REST API는 일반 작업 시 세 가지 유형의 오류를 반환할 수 있습니다.

* HTTP 수준: 이러한 오류는 `4xx` 코드로 표시됩니다.
* 응답 수준: 이러한 오류는 JSON 응답의 &quot;오류&quot; 배열에 포함됩니다.
* 레코드 수준: 이러한 오류는 JSON 응답의 &quot;result&quot; 배열에 포함되며 &quot;status&quot; 필드 및 &quot;reasons&quot; 배열과 함께 개별 레코드 단위로 표시됩니다.

응답 수준 및 레코드 수준 오류 유형의 경우 HTTP 상태 코드 200이 반환됩니다. 모든 오류 유형의 경우 HTTP 이유 구는 선택 사항이며 변경될 수 있으므로 평가해서는 안 됩니다.

### HTTP 수준 오류

일반적인 운영 환경에서는 Marketo이 HTTP 상태 코드 오류 `413 Request Entity Too Large` 및 `414 Request URI Too Long`만 반환해야 합니다. 이러한 기능은 모두 오류를 추적하고, 요청을 수정하고, 다시 시도하는 것을 통해 복구할 수 있지만, 스마트 코딩 사례를 사용하면 이러한 기능이 야생에서 발생하지 않아야 합니다.

Marketo은 요청 페이로드가 1MB를 초과하는 경우 413, 리드 가져오기의 경우 10MB를 반환합니다. 대부분의 시나리오에서는 이러한 제한에 도달할 가능성이 낮지만 요청 크기에 대한 검사를 추가하고 레코드를 이동하면 제한이 새 요청으로 초과되어 종단점에서 이 오류가 반환되는 상황을 방지해야 합니다.

GET 요청의 URI가 8KB를 초과하면 414가 반환됩니다. 이를 방지하려면 쿼리 문자열의 길이를 확인하여 이 제한을 초과하는지 확인하십시오. 요청이 POST 메서드로 변경되면 쿼리 문자열을 추가 매개 변수 `_method=GET`과(와) 함께 요청 본문으로 입력합니다. URI에 대한 제한을 무시합니다. 대부분의 경우 이 제한에 도달하는 것은 드물지만 GUID와 같은 긴 개별 필터 값이 있는 큰 레코드 일괄 처리를 검색하는 경우에는 다소 일반적입니다.
[ID](https://developer.adobe.com/marketo-apis/api/identity/) 끝점은 승인되지 않은 401 오류를 반환할 수 있습니다. 이는 일반적으로 잘못된 클라이언트 ID 또는 잘못된 클라이언트 암호 때문입니다. HTTP 수준 오류 코드

<table>
  <thead>
    <tr>
      <th> 응답 코드 </th>
      <th> 설명 </th>
      <th colspan="1"> 댓글 </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a name="413"></a>413</td>
      <td>요청 엔티티가 너무 큼</td>
      <td>페이로드가 1MB 제한을 초과했습니다.</td>
    </tr>
    <tr>
      <td><a name="414"></a>414</td>
      <td>Request-URI가 너무 김</td>
      <td>요청의 URI가 8k를 초과했습니다. URL에 매개 변수 '_method=GET'가 있고 요청 본문에 나머지 쿼리 문자열이 있는 POST로 요청을 다시 시도해야 합니다.</td>
    </tr>
  </tbody>
</table>


#### 응답 수준 오류

응답의 `success` 매개 변수가 false로 설정되어 있으면 응답 수준 오류가 표시되며 다음과 같이 구성됩니다.

```json
{
    "requestId": "e42b#14272d07d78",
    "success": false,
    "errors": [
        {
            "code": "601",
            "message": "Unauthorized"
        }
    ]
}
```

&quot;errors&quot; 배열의 각 개체에는 두 개의 멤버 `code`이(가) 있습니다. 이 두 멤버는 601에서 799까지의 따옴표 붙은 정수입니다. `message`은(는) 오류에 대한 일반 텍스트 이유를 제공합니다. 6xx 코드는 요청이 완전히 실패하여 실행되지 않았음을 항상 나타냅니다. 예를 들어, 요청을 사용하여 새 액세스 토큰을 다시 인증하고 전달하여 복구할 수 있는 601, &quot;유효하지 않은 액세스 토큰&quot;이 있습니다. 7xx 오류는 데이터가 반환되지 않았거나 요청이 잘못된 날짜를 포함하거나 필수 매개 변수가 누락되는 등 잘못 매개 변수화되었기 때문에 요청이 실패했음을 나타냅니다.

#### 응답 수준 오류 코드

이 응답 코드를 반환하는 API 호출은 일별 할당량 또는 요금 한도에 대해 계산되지 않습니다.

<table>
  <thead>
    <tr>
      <th> 응답 코드 </th>
      <th> 설명 </th>
      <th> 댓글 </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a name="502"></a>502</td>
      <td>잘못된 게이트웨이</td>
      <td>원격 서버에서 오류를 반환했습니다. 시간 초과일 수 있습니다. 지수 백오프를 사용하여 요청을 다시 시도해야 합니다.</td>
    </tr>
    <tr>
      <td><a name="601"></a>601*</td>
      <td>잘못된 액세스 토큰</td>
      <td>액세스 토큰 매개 변수가 요청에 포함되었지만 값이 올바른 액세스 토큰이 아닙니다.</td>
    </tr>
    <tr>
      <td><a name="602"></a>602*</td>
      <td>액세스 토큰 만료됨</td>
      <td>호출에 포함된 액세스 토큰이 만료로 인해 더 이상 유효하지 않습니다.</td>
    </tr>
    <tr>
      <td><a name="603"></a>603</td>
      <td>액세스 거부됨</td>
      <td>인증에 성공했지만 사용자에게 이 API를 호출할 권한이 없습니다. [추가 권한](custom-services.md)을 사용자 역할에 할당하거나 <a href="https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-an-allowlist-for-ip-based-api-access">IP 기반 API 액세스에 대한 허용 목록</a>을 사용하도록 설정할 수 있습니다.</td>
    </tr>
    <tr>
      <td><a name="604"></a>604*</td>
      <td>시간 초과 요청</td>
      <td>요청이 너무 오래 실행되었거나(예: 데이터베이스 경합 발생) 호출 헤더에 지정된 시간 초과 기간을 초과했습니다.</td>
    </tr>
    <tr>
      <td><a name="605"></a>605*</td>
      <td>HTTP 메서드가 지원되지 않음</td>
      <td>GET은 동기화 리드 끝점에 대해 지원되지 않습니다. POST를 사용해야 합니다.</td>
    </tr>
    <tr>
      <td><a name="606"></a>606</td>
      <td>최대 속도 제한 &grave;%s';이(가) '%s'초 단위로 초과되었습니다.</td>
      <td>지난 20초 동안의 호출 수가 100보다 컸습니다.</td>
    </tr>
    <tr>
      <td><a name="607"></a>607</td>
      <td>일일 할당량에 도달함</td>
      <td>오늘 통화 수가 구독의 할당량을 초과했습니다(매일 오전 12시(CST 기준)).&gt;할당량은 관리자-&gt;웹 서비스 메뉴에서 찾을 수 있습니다. 계정 관리자를 통해 할당량을 늘릴 수 있습니다.</td>
    </tr>
    <tr>
      <td><a name="608"></a>608*</td>
      <td>API를 일시적으로 사용할 수 없음</td>
      <td></td>
    </tr>
    <tr>
      <td><a name="609"></a>609</td>
      <td>잘못된 JSON</td>
      <td>요청에 포함된 본문이 유효한 JSON이 아닙니다.</td>
    </tr>
    <tr>
      <td><a name="610"></a>610</td>
      <td>요청한 리소스를 찾을 수 없음</td>
      <td>호출의 URI가 REST API 리소스 유형과 일치하지 않습니다. 이는 종종 철자가 잘못되거나 형식이 잘못된 요청 URI로 인해 발생합니다</td>
    </tr>
    <tr>
      <td><a name="611"></a>611*</td>
      <td>시스템 오류</td>
      <td>처리되지 않은 모든 예외</td>
    </tr>
    <tr>
      <td><a name="612"></a>612</td>
      <td>잘못된 콘텐츠 유형</td>
      <td>이 오류가 표시되면 JSON 형식을 지정하는 콘텐츠 유형 헤더를 요청에 추가합니다. 예를 들어 'content type: application/json'을 사용해 보십시오. 자세한 내용은 <a href="https://stackoverflow.com/questions/28181325/why-invalid-content-type">이 StackOverflow 질문을 참조하세요</a>.</td>
    </tr>
    <tr>
      <td><a name="613"></a>613</td>
      <td>잘못된 다중 파트 요청</td>
      <td>POST의 다중 부분 콘텐츠의 형식이 올바르지 않습니다.</td>
    </tr>
    <tr>
      <td><a name="614"></a>614</td>
      <td>잘못된 구독</td>
      <td>대상 구독을 찾을 수 없거나 연결할 수 없습니다. 이는 일반적으로 일시적으로 액세스할 수 없음을 나타냅니다.</td>
    </tr>
    <tr>
      <td><a name="615"></a>615</td>
      <td>동시 액세스 한도 도달</td>
      <td>최대 한 번에 모든 구독 10에 의해 요청이 처리됩니다. 이미 10개의 진행 중인 요청이 있는 경우 반환됩니다.</td>
    </tr>
    <tr>
      <td><a name="616"></a>616</td>
      <td>잘못된 구독 유형</td>
      <td>사용자 지정 개체 메타데이터 API에 액세스하려면 적절한 Marketo 구독 유형이 필요합니다. 자세한 내용은 CSM에 문의하십시오.</td>
    </tr>
    <tr>
      <td><a name="701"></a>701</td>
      <td>%s은(는) 비워둘 수 없습니다.</td>
      <td>요청에서 보고된 필드는 비워둘 수 없습니다.</td>
    </tr>
    <tr>
      <td><a name="702"></a>702</td>
      <td>특정 검색 시나리오에 대한 데이터를 찾을 수 없음</td>
      <td>지정된 검색 매개 변수와 일치하는 레코드가 없습니다.
        참고: 실패한 검색 작업 중에는 'success = true'를 반환하고 오류가 없으며 경고 정보 문자열을 설정하는 경우가 많습니다.</td>
    </tr>
    <tr>
      <td><a name="703"></a>703</td>
      <td>이 기능은 구독에 사용할 수 없습니다.</td>
      <td>사용자 구독에서 활성화되지 않은 베타 기능</td>
    </tr>
    <tr>
      <td><a name="704"></a>704</td>
      <td>잘못된 날짜 형식</td>
      <td><ul>
          <li>올바른 형식이 아닌 날짜가 지정되었습니다.</li>
          <li>잘못된 다이내믹 콘텐츠 ID가 지정되었습니다.</li>
        </ul></td>
    </tr>
    <tr>
      <td><a name="709"></a>709</td>
      <td>비즈니스 규칙 위반</td>
      <td>템플릿 없이 이메일을 만들려고 하는 등 에셋을 만들거나 업데이트하는 요구 사항을 위반하기 때문에 호출을 수행할 수 없습니다. 다음 작업을 수행하려고 할 때 이 오류가 발생할 수도 있습니다.
        <ul>
          <li>소셜 콘텐츠가 포함된 랜딩 페이지의 콘텐츠를 검색합니다.</li>
          <li>특정 자산 유형이 포함된 프로그램을 복제합니다(자세한 내용은 <a href="programs.md#clone">프로그램 복제</a> 참조).</li>
          <li>초안이 없는(즉, 이미 승인된) 에셋을 승인합니다.</li>
        </ul></td>
    </tr>
    <tr>
      <td><a name="710"></a>710</td>
      <td>상위 폴더를 찾을 수 없음</td>
      <td>지정한 상위 폴더를 찾을 수 없습니다.</td>
    </tr>
    <tr>
      <td><a name="711"></a>711</td>
      <td>호환되지 않는 폴더 유형</td>
      <td>지정된 폴더가 요청을 이행하는 올바른 유형이 아닙니다.</td>
    </tr>
    <tr>
      <td><a name="712"></a>712</td>
      <td>개인 계정에 병합 작업이 잘못되었습니다.</td>
      <td>Salesforce 개인 계정인 리드를 병합하려는 시도로 인해 리드 병합 호출이 실패했습니다.  Salesforce 개인 계정은 Salesforce에서 병합되어야 합니다.</td>
    </tr>
    <tr>
      <td><a name="713"></a>713</td>
      <td>일시적 오류</td>
      <td>API 호출 시 시스템 리소스를 일시적으로 사용할 수 없습니다. 이 오류가 발생하면 시간을 기다린 다음 요청을 다시 시도하는 것이 좋습니다.</td>
    </tr>
    <tr>
      <td><a name="714"></a>714</td>
      <td>기본 레코드 유형을 찾을 수 없음</td>
      <td>기본 레코드 유형을 찾을 수 없어 잠재 고객 병합 호출이 실패했습니다.</td>
    </tr>
    <tr>
      <td><a name="718"></a>718</td>
      <td>ExternalSalesPersonID를 찾을 수 없음</td>
      <td>존재하지 않는 'ExternalSalesPersonID' 값으로 동기화 영업 기회 호출이 생성되었습니다.</td>
    </tr>
    <tr>
      <td>719</td>
      <td>잠금 대기 시간 초과 예외</td>
      <td>복제 프로그램 호출이 수행되었으며 잠금 대기 시간이 초과되었습니다.</td>
    </tr>
  </tbody>
</table>

### 레코드 수준 {#record_level_errors}

레코드 수준 오류는 개별 레코드에 대한 작업을 완료할 수 없지만 요청 자체는 유효했음을 나타냅니다. 레코드 수준 오류가 있는 응답은 다음 패턴을 따릅니다.


#### 응답

```json
{  
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[  
      {  
         "id":50,
         "status":"created"
      },
      {  
         "id":51,
         "status":"created"
      },
      {  
         "status":"skipped",
         "reasons":[  
            {  
               "code":"1005",
               "message":"Lead already exists"
            }
         ]
      }
   ]
}
```

호출 결과 배열에 포함된 레코드는 요청의 입력 배열과 동일한 방식으로 정렬됩니다.
성공적인 요청의 각 레코드는 개별적으로 성공하거나 실패할 수 있으며, 이는 응답의 결과 배열에 포함된 각 레코드의 상태 필드에 의해 표시됩니다. 이러한 레코드의 &quot;상태&quot; 필드는 &quot;생략&quot;되며 &quot;이유&quot; 배열이 있습니다. 각 이유에는 &quot;code&quot; 멤버와 &quot;message&quot; 멤버가 포함되어 있습니다. 코드는 항상 1xxx이며 메시지는 레코드가 생략된 이유를 나타냅니다. 예를 들어 동기화 리드 요청에 &quot;action&quot;이 &quot;createOnly&quot;로 설정되어 있지만 제출된 레코드의 키 중 하나에 대한 리드가 이미 있는 경우가 있습니다. 이 경우 코드 1005를 반환하며 위에 표시된 대로 &quot;Lead 가 이미 존재합니다&quot; 라는 메시지를 반환합니다.

#### 레코드 수준 오류 코드

>[!NOTE]
>
><table>
><tbody>
>    <tr>
>      <td>응답 코드</td>
>      <td>설명</td>
>      <td>댓글</td>
>    </tr>
>    <tr>
>      <td><a name="1001"></a>1001</td>
>      <td>값 '%s'이(가) 잘못되었습니다. '%s' 유형의 필수 항목</td>
>      <td>매개 변수 값에 형식이 일치하지 않을 때마다 오류가 발생합니다. 예를 들어 정수 매개 변수에 대해 지정된 문자열 값입니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1002"></a>1002</td>
>      <td>필수 매개 변수 '%s'에 대한 값이 없습니다.</td>
>      <td>요청에서 필수 매개 변수가 누락되면 오류가 생성됩니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1003"></a>1003</td>
>      <td>잘못된 데이터</td>
>      <td>작업이 createOnly로 지정된 잠재 고객에 대해 ID가 제출되거나 배치 캠페인에서 요청 캠페인을 사용할 때와 같이 제출된 데이터가 지정된 엔드포인트 또는 모드에 대해 유효한 유형이 아닌 경우.</td>
>    </tr>
>    <tr>
>      <td><a name="1004"></a>1004</td>
>      <td>리드를 찾을 수 없음</td>
>      <td>syncLead 의 경우 작업이 "updateOnly"이고 lead 를 찾을 수 없는 경우</td>
>    </tr>
>    <tr>
>      <td><a name="1005"></a>1005</td>
>      <td>리드가 이미 있음</td>
>      <td>syncLead 의 경우 작업이 "createOnly"이고 잠재 고객이 이미 있는 경우</td>
>    </tr>
>    <tr>
>      <td><a name="1006"></a>1006</td>
>      <td>'%s' 필드를 찾을 수 없습니다.</td>
>      <td>호출에 포함된 필드가 올바른 필드가 아닙니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1007"></a>1007</td>
>      <td>여러 잠재 고객이 조회 기준과 일치함</td>
>      <td>여러 잠재 고객이 조회 기준과 일치합니다. 키가 단일 레코드와 일치하는 경우에만 업데이트를 수행할 수 있습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1008"></a>1008</td>
>      <td>'%s' 파티션에 대한 액세스가 거부되었습니다.</td>
>      <td>사용자 정의 서비스의 사용자는 레코드가 존재하는 파티션이 있는 작업 영역에 액세스할 수 없습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1009"></a>1009</td>
>      <td>파티션 이름을 지정해야 합니다.</td>
>      <td></td>
>    </tr>
>    <tr>
>      <td><a name="1010"></a>1010</td>
>      <td>파티션 업데이트가 허용되지 않음</td>
>      <td>지정한 레코드가 별도의 잠재 고객 파티션에 이미 있습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1011"></a>1011</td>
>      <td>'%s' 필드는 지원되지 않습니다.</td>
>      <td>조회 필드 또는 'filterType'이 지원되지 않는 표준 필드로 지정된 경우(예: firstName, lastName)</td>
>    </tr>
>    <tr>
>      <td><a name="1012"></a>1012</td>
>      <td>잘못된 쿠키 값 '%s'</td>
>      <td>'cookie' 매개 변수에 대해 잘못된 값으로 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/associateLeadUsingPOST">리드 연결</a>을 호출할 때 발생할 수 있습니다.
>        이는 'filterType=cookies' 및 'filterValues' 매개 변수에 대한 잘못된 값이 있는 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET">필터 유형별 리드 가져오기</a>를 호출할 때도 발생합니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1013"></a>1013</td>
>      <td>오브젝트를 찾을 수 없음</td>
>      <td>ID별 개체(목록, 캠페인) 가져오기에서 이 오류 코드를 반환합니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1014"></a>1014</td>
>      <td>개체를 만들지 못했습니다.</td>
>      <td>개체(목록)를 만들지 못했습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1015"></a>1015</td>
>      <td>리드가 목록에 없음</td>
>      <td>지정된 잠재 고객이 대상 목록의 구성원이 아닙니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1016"></a>1016</td>
>      <td>가져오기가 너무 많음</td>
>      <td>대기 중인 가져오기가 너무 많습니다. 최대 10개가 허용됩니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1017"></a>1017</td>
>      <td>개체가 이미 있습니다.</td>
>      <td>레코드가 이미 있으므로 만들지 못했습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1018"></a>1018</td>
>      <td>CRM 활성화됨</td>
>      <td>인스턴스에 기본 CRM 통합이 활성화되어 있으므로 작업을 수행할 수 없습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1019"></a>1019</td>
>      <td>가져오기 진행 중</td>
>      <td>대상 목록을 이미 (으)로 가져오고 있습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1020"></a>1020</td>
>      <td>너무 많은 클론이 프로그램에 할당됨</td>
>      <td>구독이 당일 일정 프로그램에서 할당된 'cloneToProgramName' 용도에 도달했습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1021"></a>1021</td>
>      <td>회사 업데이트가 허용되지 않음</td>
>      <td>syncLead 중에는 회사 업데이트가 허용되지 않음</td>
>    </tr>
>    <tr>
>      <td><a name="1022"></a>1022</td>
>      <td>사용 중인 오브젝트</td>
>      <td>다른 오브젝트에서 오브젝트를 사용 중이면 삭제가 허용되지 않습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1025"></a>1025</td>
>      <td>프로그램 상태를 찾을 수 없음</td>
>      <td>프로그램 채널에 사용 가능한 상태와 일치하지 않는 잠재 고객 프로그램 상태 변경에 상태가 지정되었습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1026"></a>1026</td>
>      <td>사용자 지정 개체가 활성화되지 않음</td>
>      <td>인스턴스에 사용자 지정 개체 통합이 활성화되어 있지 않아 작업을 수행할 수 없습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1027"></a>1027</td>
>      <td>최대 활동 유형 제한에 도달했습니다.</td>
>      <td>구독이 사용 가능한 최대 사용자 지정 활동 유형 수에 도달했습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1028"></a>1028</td>
>      <td>최대 필드 제한에 도달했습니다.</td>
>      <td>사용자 지정 활동에는 최대 20개의 보조 속성이 있습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1029"></a>1029</td>
>      <td><ul>
>          <li>큐에 작업이 너무 많음</li>
>          <li>일일 내보내기 할당량 초과</li>
>          <li>작업이 이미 큐에 추가됨</li>
>        </ul></td>
>      <td><ul>
>          <li>구독에는 지정된 시간에 큐에 최대 10개의 대량 추출 작업이 허용됩니다.</li>
>          <li>기본적으로 추출 작업은 하루에 500MB로 제한됩니다(매일 오전 12:00CST에 재설정).</li>
>          <li>내보내기 ID는 이미 큐에 있습니다.</li>
>        </ul></td>
>    </tr>
>    <tr>
>      <td><a name="1035"></a>1035</td>
>      <td>지원되지 않는 필터 유형</td>
>      <td>일부 구독에서는 updateAt, smartListId, smartListName과 같은 대량 리드 추출 필터 유형이 지원되지 않습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1036"></a>1036</td>
>      <td>입력에서 중복 개체가 발견되었습니다.</td>
>      <td>동일한 외래 키를 사용하여 두 개 이상의 레코드를 업데이트하라는 호출이 발생했습니다. 예를 들어 동기화 회사는 둘 이상의 회사에 대해 동일한 externalCompanyId를 사용하여 를 호출합니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1037"></a>1037</td>
>      <td>잠재 고객 건너뜀</td>
>      <td>이미 이 상태 또는 그 이후이므로 잠재 고객을 건너뛰었습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1042"></a>1042</td>
>      <td>잘못된 runAt 날짜</td>
>      <td>일정 캠페인에 대해 지정된 runAt 날짜가 너무 먼 미래입니다(최대 2년).</td>
>    </tr>
>    <tr>
>      <td><a name="1048"></a>1048</td>
>      <td>사용자 지정 개체 초안 삭제 실패</td>
>      <td>사용자 지정 개체의 초안 버전을 삭제하라는 호출이 수행되었습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1049"></a>1049</td>
>      <td>활동을 만들지 못했습니다.</td>
>      <td>특성 배열이 너무 깁니다.
>        레코드에 전달된 특성의 배열이 최대 길이(65536바이트)를 초과했습니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1076"></a>1076</td>
>      <td>mergeInCRM 플래그가 있는 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/mergeLeadsUsingPOST">잠재 고객 병합</a> 호출은 4입니다.</td>
>      <td>중복 레코드를 만들고 있습니다. 기존 레코드를 대신 사용하는 것이 좋습니다.
>        Salesforce에서 병합할 때 Marketo에서 수신하는 오류 메시지입니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1077"></a>1077</td>
>      <td>'SFDC 필드' 길이로 인해 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/mergeLeadsUsingPOST">리드 병합</a> 호출이 실패했습니다.</td>
>      <td>'SFDC 필드'가 허용된 문자 제한을 초과하여 mergeInCRM이 true로 설정된 병합 리드 호출이 실패했습니다. 수정하려면 'SFDC 필드'의 길이를 줄이거나 mergeInCRM을 false로 설정하십시오.</td>
>    </tr>
>    <tr>
>      <td><a name="1078"></a>1078</td>
>      <td>잠재 고객/연락처가 아닌 삭제된 엔터티로 인해 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/mergeLeadsUsingPOST">잠재 고객 병합</a> 호출에 실패했습니다. 또는 필드 필터 기준이 일치하지 않습니다.</td>
>      <td>병합 실패, 고유하게 동기화된 CRM에서 병합 작업을 수행할 수 없음
>        Salesforce에서 병합할 때 Marketo에서 수신하는 오류 메시지입니다.</td>
>    </tr>
>    <tr>
>      <td><a name="1079"></a>1079</td>
>      <td>중복 레코드의 개인화된 URL 충돌로 인해 <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/mergeLeadsUsingPOST">리드 병합</a> 호출이 실패했습니다.</td>
>      <td>병합 리드 호출에서 동일한 개인화된 URL을 사용하는 여러 리드를 지정했습니다. 해결하려면 Marketo Engage 사용자 인터페이스를 사용하여 이러한 레코드를 병합합니다.</td>
>    </tr>
>  </tbody>
></table>

