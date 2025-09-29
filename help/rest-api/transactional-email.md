---
title: 트랜잭션 이메일
feature: REST API
description: 설정 단계 및 Java 코드 예제를 사용하여 트랜잭션 이메일에 대해 Marketo을 구성하고 REST API 요청 캠페인을 통해 이를 트리거하는 방법에 대해 알아봅니다.
exl-id: 057bc342-53f3-4624-a3c0-ae619e0c81a5
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 트랜잭션 이메일

Marketo API의 일반적인 사용 사례는 [캠페인 요청](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/triggerCampaignUsingPOST) API 호출을 통해 트랜잭션 이메일을 특정 레코드로 보내는 것입니다. Marketo REST API를 사용하여 필요한 호출을 실행하기 위한 Marketo 내에는 몇 가지 구성 요구 사항이 있습니다.

- 수신자는 Marketo 내에 레코드가 있어야 합니다.
- Marketo 인스턴스에 만들고 승인된 트랜잭션 이메일이 있어야 합니다.
- &quot;캠페인이 요청됨, 1&quot;인 활성 트리거 캠페인이 있어야 합니다. Source: 이메일을 보내도록 설정된 웹 서비스 API&quot;

먼저 [전자 메일을 만들고 승인](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ko)하세요. 이메일이 실제로 트랜잭션된 경우, 이를 작동 상태로 설정해야 하지만, 이 경우 적법하게 작동 상태가 됩니다. 이는 이메일 작업 > 이메일 설정 아래의 편집 화면에서 구성됩니다.

![Request-Campaign-Email-Settings](assets/request-campaign-email-settings.png)

![Request-Campaign-Operative](assets/request-campaign-operational.png)

승인하면 캠페인을 만들 준비가 되었습니다.

![RequestCampaign-Apply-Draft](assets/request-campaign-approve-draft.png)

캠페인을 처음 만드는 경우 [새 스마트 캠페인 만들기](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/creating-a-smart-campaign/create-a-new-smart-campaign.html?lang=ko) 문서를 확인하십시오. 캠페인을 만들었으면 다음 단계를 수행해야 합니다. Campaign이 요청됨 트리거를 사용하여 스마트 목록을 구성합니다.

![Request-Campaign-Smart-List](assets/request-campaign-smart-list.png)

이제 이메일을 보내기 단계를 이메일에 가리키도록 흐름을 구성해야 합니다.

![Request-Campaign-Flow](assets/request-campaign-flow.png)

활성화하기 전에 예약 탭에서 일부 설정을 결정해야 합니다. 이 특정 이메일을 지정된 레코드로 한 번만 전송해야 하는 경우 자격 설정을 그대로 둡니다. 하지만 이메일을 여러 번 받아야 하는 경우 매번 또는 사용 가능한 케이던스 중 하나로 조정할 수 있습니다.

이제 활성화할 준비가 되었습니다.

![Request-Campaign-Schedule](assets/request-campaign-schedule.png)

## API 호출 전송

**참고:** 아래 Java 예제에서 [minimal-json 패키지](https://github.com/ralfstx/minimal-json)를 사용하여 코드에서 JSON 표현을 처리하고 있습니다.

API를 통해 트랜잭션 이메일을 보내는 첫 번째 부분은 해당 이메일 주소가 있는 레코드가 Marketo 인스턴스에 있는지, 리드 ID에 액세스할 수 있는지 확인하는 것입니다. 이 게시물의 목적상 이메일 주소가 이미 Marketo에 있으며 레코드의 ID만 검색해야 한다고 가정합니다. 이를 위해 [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET) 호출을 사용합니다. 캠페인을 요청하기 위한 의 주요 방법을 살펴보겠습니다.

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
        //Create an instance of Auth so that we can authenticate with our Marketo instance
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("requestCampaign.test@marketo.com");

        //Create and parameterize an instance of Leads
        //Set your email filterValue appropriately
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("test.requestCamapign@example.com");

        //Get the inner results array of the response
        JsonArray leadsResult = leadsRequest.getData().get("result").asArray();

        //Get the id of the record indexed at 0
        int lead = leadsResult.get(0).asObject().get("id").asInt();

        //Set the ID of your campaign from Marketo
        int campaignId = 0;
        RequestCampaign rc = new RequestCampaign(auth, campaignId).addLead(lead);

        //Send the request to Marketo
        rc.postData();
    }
}
```

leadsRequest 의 JsonObject 응답에서 이러한 결과를 얻으려면 일부 코드 를 작성해야 합니다. Array에서 첫 번째 결과를 검색하려면 JsonObject에서 Array를 추출하고 0에서 개체 인덱싱을 가져와야 합니다.

```java
JsonArray leadsResult = leadsRequest.getData().get("result").asArray();
int leadId = leadsResult.get(0).asObject().get("id").asInt();
```

이제부터 해야 하는 것은 요청 캠페인 호출입니다. 이를 위해 필수 매개 변수는 요청의 URL에 있는 ID와 하나의 멤버인 &quot;id&quot;가 포함된 JSON 개체의 배열입니다. 이에 대한 코드를 살펴보겠습니다.

```java
package dev.marketo.blog_request_campaign;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class RequestCampaign {
    private String endpoint;
    private Auth auth;
    public ArrayList leads = new ArrayList();
    public ArrayList tokens = new ArrayList();

    public RequestCampaign(Auth auth, int campaignId) {
        this.auth = auth;
        this.endpoint = this.auth.marketoInstance + "/rest/v1/campaigns/" + campaignId + "/trigger.json";
    }
    public RequestCampaign setLeads(ArrayList leads) {
        this.leads = leads;
        return this;
    }
    public RequestCampaign addLead(int lead){
        leads.add(lead);
        return this;
    }
    public RequestCampaign setTokens(ArrayList tokens) {
        this.tokens = tokens;
        return this;
    }
    public RequestCampaign addToken(String tokenKey, String val){
        JsonObject jo = new JsonObject().add("name", tokenKey);
        jo.add("value", val);
        tokens.add(jo);
        return this;
    }
    public JsonObject postData(){
        JsonObject result = null;
        try {
            JsonObject requestBody = buildRequest(); //builds the Json Request Body
            System.out.println("Executing RequestCampaign call\n" + "Endpoint: " + endpoint + "\nRequest Body:\n"  + requestBody);
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
            urlConn.setRequestMethod("POST");
            urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
            OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
            wr.write(requestBody.toString());
            wr.flush();
            InputStream inStream = urlConn.getInputStream(); //get the inputStream from the URL connection
            Reader reader = new InputStreamReader(inStream);
            result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
            System.out.println("Result:\n" + result);
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return result;
    }

    private JsonObject buildRequest(){
        JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
        JsonObject input = new JsonObject();
        JsonArray leadsArray = new JsonArray();
        for (int lead : leads) {
            JsonObject jo = new JsonObject().add("id", lead);
            leadsArray.add(jo);
        }
        input.add("leads", leadsArray);
        JsonArray tokensArray = new JsonArray();
        for (JsonObject jo : tokens) {
            tokensArray.add(jo);
        }
        input.add("tokens", tokensArray);
        requestBody.add("input", input);
        return requestBody;
    }

}
```

이 클래스에는 인증을 받는 생성자 1명과 캠페인 ID가 있습니다. Leads는 setLeads에 레코드의 ID가 포함된 `ArrayList<Integer>`을(를) 전달하거나 addLead를 사용하여 개체에 추가됩니다. addLead는 하나의 정수를 사용하여 leads 속성의 기존 ArrayList에 추가합니다. 리드 레코드를 캠페인에 전달하기 위해 API 호출을 트리거하려면, 요청의 응답 데이터가 포함된 JsonObject를 반환하는 postData를 호출해야 합니다. 요청 캠페인이 호출되면 호출에 전달된 모든 리드는 Marketo의 Target 트리거 캠페인에 의해 처리되고 이전에 만든 이메일로 전송됩니다. 축하합니다. Marketo REST API를 통해 이메일을 트리거했습니다. 요청 캠페인을 통해 이메일 콘텐츠를 동적으로 사용자 지정하는 2부를 살펴보십시오.

### 이메일 작성

콘텐츠를 사용자 지정하려면 먼저 Marketo에서 [프로그램](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/create-a-program.html?lang=ko) 및 [이메일](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ko)을 구성해야 합니다. 사용자 지정 콘텐츠를 생성하려면 프로그램 내에 토큰을 만든 다음 전송할 이메일에 배치해야 합니다. 간결성을 위해 이 예제에서는 하나의 토큰만 사용하고 있지만, 보낸 사람 이메일, 보낸 사람 이름, 회신 주소 또는 이메일의 모든 콘텐츠에서 토큰의 숫자를 바꿀 수 있습니다. 그러면 교체를 위해 하나의 리치 텍스트 토큰을 만들고 이를 &quot;bodyReplacement&quot;라고 하겠습니다. 리치 텍스트를 사용하면 토큰의 모든 컨텐츠를 입력하려는 임의의 HTML으로 바꿀 수 있습니다.

![새 토큰](assets/New-Token.png)

비어 있는 동안에는 토큰을 저장할 수 없습니다. 먼저 여기에 자리 표시자 텍스트를 삽입하십시오. 이제 이메일에 토큰을 삽입해야 합니다.

![추가 토큰](assets/Add-Token.png)

이제 이 토큰은 요청 캠페인 호출을 통해 대체할 수 있습니다. 이 토큰은 이메일별로 대체해야 하는 단일 텍스트 행만큼 단순하거나 이메일의 거의 전체 레이아웃을 포함할 수 있습니다.

### 코드

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
        //Create an instance of Auth so that we can authenticate with our Marketo instance
        Auth auth = new Auth("Client ID - CHANGE ME", "Client Secret - CHANGE ME", "Host - CHANGE ME");

        //Create and parameterize an instance of Leads
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("requestCampaign.test@marketo.com");

        //get the inner results array of the response
        JsonArray leadsResult = leadsRequest.getData().get("result").asArray();

        //get the id of the record indexed at 0
        int lead = leadsResult.get(0).asObject().get("id").asInt();

        //Set the ID of our campaign from Marketo
        int campaignId = 1578;
        RequestCampaign rc = new RequestCampaign(auth, campaignId).addLead(lead);

        //Create the content of the token here, and add it to the request
        String bodyReplacement = "<div class=\"replacedContent\"><p>This content has been replaced</p></div>";
        rc.addToken("{{my.bodyReplacement}}", bodyReplacement);
        rc.postData();
    }
}
```

코드가 익숙해 보이는 경우 위의 기본 메서드에서 추가된 두 줄만 포함되기 때문입니다. 이번에는 bodyReplacement 변수에 토큰 콘텐츠를 만든 다음 addToken 메서드를 사용하여 요청에 추가합니다. addToken은 키 및 값을 사용한 다음 JsonObject 표현식을 만들고 내부 토큰 배열에 추가합니다. 그런 다음 postData 메서드 동안 serialize되고 다음과 같은 본문이 만들어집니다.

```json
{
    "input":
    {
        "leads": [
            {
                "id": 1
            }
        ],
        "tokens": [
            {
                "name": "{{my.bodyReplacement}}",
                "value": "<div class=\"replacedContent\"><p>This content has been replaced</p></div>"
            }
        ]
    }
}
```

결합된 콘솔 출력은 다음과 같습니다.

```bash
Token is empty or expired. Trying new authentication
Trying to authenticate with ...
Got Authentication Response: {"access_token":"19d51b9a-ff60-4222-bbd5-be8b206f1d40:st","token_type":"bearer","expires_in":3565,"scope":"apiuser@mktosupport.com"}
Executing RequestCampaign call
Endpoint: .../rest/v1/campaigns/1578/trigger.json
Request Body:
{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class=\"replacedContent\"><p>This content has been replaced</p></div>"}]}}
Result:
{"requestId":"1e8d#14eadc5143d","result":[{"id":1578}],"success":true}
```

## 요약

이 방법은 여러 가지 방법으로 확장할 수 있으며, 개별 레이아웃 섹션 내 이메일 또는 외부 이메일 내의 콘텐츠를 변경하여 사용자 지정 값을 작업 또는 관심 있는 순간에 전달할 수 있습니다. 프로그램 내에서 토큰을 사용할 수 있는 모든 위치에서 이 방법을 사용하여 사용자 지정할 수 있습니다. [캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Campaigns/operation/scheduleCampaignUsingPOST) 호출에서도 유사한 기능을 사용할 수 있습니다. 이렇게 하면 전체 일괄 처리 캠페인에서 토큰을 처리할 수 있습니다. 각 리드를 기준으로 사용자 정의할 수 없지만, 다양한 리드 세트에서 콘텐츠를 사용자 정의하는 데 유용합니다.
