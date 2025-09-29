---
title: syncLead
feature: SOAP
description: Marketo SOAP syncLead 를 사용하여 요청 필드, XML 및 PHP 예제를 통해 단일 리드를 삽입하거나 업데이트하고, 식별자 및 작업 공간을 처리하는 방법을 알아봅니다.
exl-id: e6cda794-a9d4-4153-a5f3-52e97a506807
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 2%

---

# syncLead

이 함수는 단일 리드 레코드를 삽입하거나 업데이트합니다. 기존 리드를 업데이트할 때 리드는 다음 키 중 하나로 식별됩니다.

- Marketo ID
- 외래 시스템 ID(`foreignSysPersonId`(으)로 구현됨)
- Marketo 쿠키(Munchkin JS 스크립트로 생성)
- 이메일

기존 일치 항목이 발견되면 호출에서 업데이트를 수행합니다. 그렇지 않으면 리드를 삽입하고 생성합니다. 익명 리드는 Marketo 쿠키 ID를 사용하여 업데이트할 수 있으며 업데이트 시 알려지게 됩니다.

이메일을 제외하고 이러한 모든 식별자는 고유 키로 처리됩니다. Marketo ID가 다른 모든 키보다 우선합니다. `foreignSysPersonId`과(와) Marketo ID가 모두 잠재 고객 레코드에 있는 경우 Marketo ID가 우선하며 해당 잠재 고객에 대해 `foreignSysPersonId`이(가) 업데이트됩니다. `foreignSysPersonId`만 지정된 경우 고유 식별자로 사용됩니다. `foreignSysPersonId`과(와) 전자 메일이 모두 있지만 Marketo ID가 없는 경우 `foreignSysPersonId`이(가) 우선하며 해당 잠재 고객에 대해 전자 메일이 업데이트됩니다.

원할 경우 컨텍스트 헤더를 지정하여 대상 작업 공간의 이름을 지정할 수 있습니다.

Marketo 작업 영역이 활성화되고 헤더를 사용하면 다음 규칙이 적용됩니다.

- 지정 규칙이 설정되어 있고 새 가망 고객이 구성된 규칙에 적격인 경우, 지정 규칙으로 정의된 분할 영역에 새 가망 고객이 생성됩니다. 그렇지 않으면 이름이 지정된 작업 영역의 기본 파티션에 새 리드가 만들어집니다.
- Marketo 리드 ID, 외부 시스템 ID 또는 Marketo 쿠키가 일치한 리드는 명명된 작업 영역의 기본 파티션에 존재해야 합니다. 그렇지 않으면 오류가 반환됩니다
- 기존 리드가 이메일에 의해 일치하는 경우 이름이 지정된 작업 영역은 무시되고 리드는 해당 의 현재 파티션에서 업데이트됩니다

Marketo 작업 영역이 활성화되고 헤더를 사용하지 않으면 다음 규칙이 적용됩니다.

- 지정 규칙이 설정되어 있고 새 가망 고객이 구성된 규칙에 적격인 경우, 지정 규칙으로 정의된 분할 영역에 새 가망 고객이 생성됩니다. 그렇지 않으면 &quot;기본&quot; 작업 영역의 기본 파티션에 새 리드가 만들어집니다.
- 기존 리드는 현재 파티션에서 업데이트됩니다.

Marketo 작업 영역이 활성화되지 않은 경우 대상 작업 영역은 &quot;기본&quot; 작업 영역이어야 합니다. 헤더를 전달할 필요가 없습니다.

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| leadRecord->Id | 필수 - 이메일 또는 `foreignSysPersonId`이(가) 없는 경우에만 | 잠재 고객 레코드의 Marketo ID |
| leadRecord->Email | 필수 - ID 또는 `foreignSysPersonId`이(가) 없는 경우에만 | 잠재 고객 레코드와 연결된 이메일 주소 |
| leadRecord->`foreignSysPersonId` | 필수 - ID 또는 이메일이 없는 경우에만 | 잠재 고객 레코드와 연계된 외부 시스템 ID |
| leadRecord->foreignSysType | 선택 사항 - `foreignSysPersonId`이(가) 있는 경우에만 필요합니다. | 외국 시스템의 유형입니다. 가능한 값: CUSTOM, SFDC, NETSUITE |
| leadRecord->leadAttributeList->attribute->attrName | 필수 | 값을 갱신할 잠재 고객 속성의 이름입니다. |
| leadRecord->leadAttributeList->attribute->attrValue | 필수 | attrName에 지정된 잠재 고객 속성으로 설정할 값입니다. |
| returnLead | 필수 | true이면 업데이트 시 업데이트된 전체 리드 레코드를 반환합니다. |
| marketoCookie | 선택 사항입니다 | [Munchkin javascript](../javascript-api/lead-tracking.md) 쿠키 |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>bigcorp1_461839624B16E06BA2D663</mktowsUserId>
      <requestSignature>92f05a7be4838ae1c0e5aafe814891ee72968a08</requestSignature>
      <requestTimestamp>2013-07-31T12:38:47-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncLead>
      <leadRecord>
        <Email>t@t.com</Email>
        <leadAttributeList>
          <attribute>
            <attrName>FirstName</attrName>
            <attrValue>George</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrValue>of the Jungle</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
      <returnLead>false</returnLead>
    </ns1:paramsSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncLead>
      <result>
        <leadId>1089965</leadId>
        <syncStatus>
          <leadId>1089965</leadId>
          <status>UPDATED</status>
          <error xsi:nil="true" />
        </syncStatus>
        <leadRecord xsi:nil="true" />
      </result>
    </ns1:successSyncLead>
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
  $options = array("connection_timeout" =20, "location" =$marketoSoapEndPoint);
  if ($debug) {
    $options["trace"] = true;
  }

  // Create Request
  $leadKey = new stdClass();
  $leadKey->Email = "george@jungle.com";

  // Lead attributes to update
  $attr1 = new stdClass();
  $attr1->attrName  = "FirstName";
  $attr1->attrValue = "George";

  $attr2= new stdClass();
  $attr2->attrName  = "LastName";
  $attr2->attrValue = "of the Jungle";

  $attrArray = array($attr1, $attr2);
  $attrList = new stdClass();
  $attrList->attribute = $attrArray;
  $leadKey->leadAttributeList = $attrList;

  $leadRecord = new stdClass();
  $leadRecord->leadRecord = $leadKey;
  $leadRecord->returnLead = false;
  $params = array("paramsSyncLead" =$leadRecord);

  $soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
  try {
    $result = $soapClient->__soapCall('syncLead', $params, $options, $authHdr);
  }
  catch(Exception $ex) {
    var_dump($ex);
  }

  if ($debug) {
    print "RAW request:\n" .$soapClient->__getLastRequest() ."\n";
    print "RAW response:\n" .$soapClient->__getLastResponse() ."\n";
  }
  print_r($result);

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
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class SyncLead {

    public static void main(String[] args) {
        System.out.println("Executing syncLead");
        try {
            URL marketoSoapEndPoint = new URL("https://100-AEK-913.mktoapi.com/soap/mktows/2_1" + "?WSDL");
            String marketoUserId = "demo17_1_809934544BFABAE58E5D27";
            String marketoSecretKey = "27272727aa";

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
            ParamsSyncLead request = new ParamsSyncLead();
            LeadRecord key = new LeadRecord();

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Stringemail = objectFactory.createLeadRecordEmail("george@jungle.com");
            key.setEmail(email);
            request.setLeadRecord(key);

            Attribute attr1 = new Attribute();
            attr1.setAttrName("FirstName");
            attr1.setAttrValue("George2");

            Attribute attr2 = new Attribute();
            attr2.setAttrName("LastName");
            attr2.setAttrValue("of the Jungle");

            ArrayOfAttribute aoa = new ArrayOfAttribute();
            aoa.getAttributes().add(attr1);
            aoa.getAttributes().add(attr2);

            QName qname = new QName("http://www.marketo.com/mktows/", "leadAttributeList");
            JAXBElement<ArrayOfAttributeattrList = new JAXBElement(qname, ArrayOfAttribute.class, aoa);
            key.setLeadAttributeList(attrList);

            MktowsContextHeader headerContext = new MktowsContextHeader();
            headerContext.setTargetWorkspace("default");

            SuccessSyncLead result = port.syncLead(request, header, headerContext);

            JAXBContext context = JAXBContext.newInstance(SuccessSyncLead.class);
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
    'ns1:AuthenticationHeader' ={ "mktowsUserId" =mktowsUserId, "requestSignature" =requestSignature,
    "requestTimestamp"  =requestTimestamp
    }
}

client = Savon.client(wsdl: 'http://app.marketo.com/soap/mktows/2_3?WSDL', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

#Create Request
request = {
    :lead_record ={
        :Email ="t@t.com",
          :lead_attribute_list ={
              :attribute ={
                :attr_name ="FirstName",
                :attr_value ="George" },
              :attribute! ={
                :attr_name ="LastName",
                :attr_value ="of the Jungle" }
        }
    },
    :return_lead ="false"
}

response = client.call(:sync_lead, message: request)

puts response
```
