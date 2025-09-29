---
title: scheduleCampaign
feature: SOAP, Smart Campaigns
description: scheduleCampaign을 사용하여 지금 또는 나중에 Marketo 배치 스마트 캠페인을 실행하고, 토큰을 재정의하고, 프로그램을 복제하고, PHP 및 Java 샘플이 포함된 SOAP XML을 통해 구현합니다.
exl-id: a9ef2c16-34ef-4e0f-b765-e332335b0b81
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 3%

---

# scheduleCampaign

이 함수는 즉시 또는 미래 날짜에 실행되도록 배치 스마트 캠페인의 일정을 설정합니다. 성공적으로 완료하려면 기존 스마트 캠페인이 필요합니다. ImportToList와 함께 사용하여 리드 목록을 업로드한 다음 새로 생성된 해당 목록에 대해 배치 캠페인을 실행할 수 있습니다.

## 선택적 프로그램 토큰

requestCampaign 함수와 유사하게 기존 토큰을 재정의하는 내 토큰 배열을 이 API 호출에 전달할 수 있습니다. 캠페인 실행 후 토큰이 삭제됩니다.

이 선택적 매개 변수를 [importToList](importtolist.md)과(와) 함께 사용하는 경우 토큰의 우선 순위는 다음과 같습니다.

1. 리드 토큰당 importToList
1. 캠페인 토큰당 scheduleCampaign
1. 프로그램의 내 토큰

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| programName | 필수 | 포함된 프로그램의 이름 |
| campaignName | 필수 | 스마트 캠페인의 이름 |
| 캠페인 실행 | 선택 사항입니다 | 예약된 캠페인을 실행하는 시간(W3C WSDL 날짜 형식)입니다. |
| cloneToProgramName | 선택 사항입니다 | 이 속성이 있으면 캠페인의 상위 프로그램이 복제되고 새로 생성된 캠페인이 예약됩니다. 속성은 결과 프로그램에 대해 원하는 이름을 지정합니다. 참고: 이 필드를 사용하는 경우 하루에 10번만 호출할 수 있습니다. |
| programTokenList->attrib->name | 선택 사항입니다 | 새 값을 보낼 토큰의 이름입니다. Marketo UI 내에서처럼 전체 토큰 형식을 사용합니다. 즉, &quot;{{my.message}}&quot; |
| programTokenList->attrib->value | 선택 사항입니다 | 연결된 토큰 이름의 값입니다. |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809224544BFABAE58E5D27</mktowsUserId>
      <requestSignature>b578495dfdd03231455bb7671f02d2fe0a9edf79</requestSignature>
      <requestTimestamp>2013-08-03T21:39:34-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsScheduleCampaign>
      <programName>Trav-Demo-Program</programName>
      <campaignName>Batch Campaign Example</campaignName>
      <campaignRunAt>2013-08-03T21:39:34-07:00</campaignRunAt>
      <cloneToProgramName>TestProgramCloneFromSOAP</cloneToProgramName>
      <programTokenList>
        <attrib>
          <name>{{my.message}}</name>
          <value>Updated message</value>
        </attrib>
        <attrib>
          <name>{{my.other token}}</name>
          <value>Value for other token</value>
        </attrib>
      </programTokenList>
    </ns1:paramsScheduleCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successScheduleCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successScheduleCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 샘플 코드 - PHP

```php
 <?php

  $debug = true;

  $marketoSoapEndPoint     = "";  // CHANGE ME
  $marketoUserId           = "";  // CHANGE ME
  $marketoSecretKey        = "";  // CHANGE ME
  $marketoNameSpace        = "http://www.marketo.com/mktows/";

  // Create Signature
  $dtzObj = new DateTimeZone("America/Los_Angeles");
  $dtObj  = new DateTime('now', $dtzObj);
  $timeStamp = $dtObj->format(DATE_W3C);
  $encryptString = $timeStamp . $marketoUserId;
  $signature = hash_hmac('sha1', $encryptString, $marketoSecretKey);

  // Create SOAP Header
  $attrs = new stdClass();
  $attrs->mktowsUserId = $marketoUserId;
  $attrs->requestSignature = $signature;
  $attrs->requestTimestamp = $timeStamp;
  $authHdr = new SoapHeader($marketoNameSpace, 'AuthenticationHeader', $attrs);
  $options = array("connection_timeout" => 20, "location" => $marketoSoapEndPoint);
  if ($debug) {
    $options["trace"] = true;
  }

  // Create Request
  $params = new stdClass();
  $params->programName = "Trav-Demo-Program";
  $params->campaignName = "Batch Campaign Example";
  $dtObj = new DateTime('now', $dtzObj);
  $params->campaignRunAt = $dtObj->format(DATE_W3C);
  $params->cloneToProgramName = "TestProgramCloneFromSOAP";

  $token = new stdClass();
  $token->name = "{{my.message}}";
  $token->value = "Updated message";

  $params->programTokenList = array("attrib" => $token);
  $params = array("paramsScheduleCampaign" => $params);

  $soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
  try {
    $response = $soapClient->__soapCall('scheduleCampaign', $params, $options, $authHdr);
  }
  catch(Exception $ex) {
    var_dump($ex);
  }
  if ($debug) {
    print "RAW request:\n" .$soapClient->__getLastRequest() ."\n";
    print "RAW response:\n" .$soapClient->__getLastResponse() ."\n";
  }
  print_r($response);

?>
```

## 샘플 코드 - Java

```java
import com.marketo.mktows.*;
import java.net.URL;
import javax.xml.namespace.QName;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.GregorianCalendar;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;
import javax.xml.datatype.DatatypeFactory;
import javax.xml.datatype.XMLGregorianCalendar;

public class ScheduleCampaign {


    public static void main(String[] args) {
        System.out.println("Executing Schedule Campaign");
        try {
            URL marketoSoapEndPoint = new URL("CHANGE ME" + "?WSDL");
            String marketoUserId = "CHANGE ME";
            String marketoSecretKey = "CHANGE ME";

            QName serviceName = new QName("http://www.marketo.com/mktows/", "MktMktowsApiService");
            MktMktowsApiService service = new MktMktowsApiService(marketoSoapEndPoint, serviceName);
            MktowsPort port = service.getMktowsApiSoapPort();

            // Create Signature
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
            String text = df.format(new Date());
            String requestTimestamp = text.substring(0, 22) + ":" + text.substring(22);
            String encryptString = requestTimestamp + marketoUserId ;

            SecretKeySpec secretKey = new SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");
            Mac mac = Mac.getInstance("HmacSHA1");
            mac.init(secretKey);
            byte[] rawHmac = mac.doFinal(encryptString.getBytes());
            char[] hexChars = Hex.encodeHex(rawHmac);
            String signature = new String(hexChars);

            // Set Authentication Header
            AuthenticationHeader header = new AuthenticationHeader();
            header.setMktowsUserId(marketoUserId);
            header.setRequestTimestamp(requestTimestamp);
            header.setRequestSignature(signature);

            // Create Request
            ParamsScheduleCampaign request = new ParamsScheduleCampaign();

            request.setProgramName("Trav-Demo-Program");
            request.setCampaignName("Batch Campaign Example");

            // Create setCampaignRunAt timestamp
            GregorianCalendar gc = new GregorianCalendar();
            gc.setTimeInMillis(new Date().getTime());

            DatatypeFactory factory = DatatypeFactory.newInstance();
            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<XMLGregorianCalendar> setCampaignRunAtValue = objectFactory.createParamsScheduleCampaignCampaignRunAt(factory.newXMLGregorianCalendar(gc));
            request.setCampaignRunAt(setCampaignRunAtValue);

            request.setCloneToProgramName("TestProgramCloneFromSOAP");

            ArrayOfAttrib aoa = new ArrayOfAttrib();

            Attrib attrib = new Attrib();
            attrib.setName("{{my.message}}");
            attrib.setValue("Updated message");

            aoa.getAttribs().add(attrib);

            JAXBElement<ArrayOfAttrib> arrayOfAttrib = objectFactory.createParamsScheduleCampaignProgramTokenList(aoa);
            request.setProgramTokenList(arrayOfAttrib);

            SuccessScheduleCampaign result = port.scheduleCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessScheduleCampaign.class);
            Marshaller m = context.createMarshaller();
            m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
            m.marshal(result, System.out);

        }
        catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 샘플 코드 - 루비

```ruby
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "http://www.marketo.com/mktows/"

#Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

#Create SOAP Header
headers = {
    'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,
    "requestTimestamp"  => requestTimestamp
    }
}

client = Savon.client(wsdl: 'http://app.marketo.com/soap/mktows/2_3?WSDL', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

#Create Request
request =  {
    :program_name => "Trav-Demo-Program",
    :campaign_name => "Batch Campaign Example",
    :campaign_run_at => requestTimestamp,
    :clone_to_program_name => "TestProgramCloneFromSOAP",
    :program_token_list => {
        :attrib => {
            :name => "{{my.message}}",
            :value => "Updated message" },
        :attrib! => {
            :name => "{{my.other token}}",
            :value => "Value for other token" }
    }
}

response = client.call(:schedule_campaign, message: request)

puts response
```
