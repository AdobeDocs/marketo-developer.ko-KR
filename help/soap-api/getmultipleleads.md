---
title: getMultipleLead
feature: SOAP
description: getMultipleLeads SOAP 호출
exl-id: db9aabec-8705-40c6-b264-740fdcef8a52
source-git-commit: 66add4c38d0230c36d57009de985649bb67fde3e
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# getMultipleLead

`getLead`과(와) 마찬가지로 `getMultipleLeads`은(는) Marketo에서 잠재 고객 레코드를 검색합니다. 이 호출에서는 단일 리드에 대한 데이터 대신 leadSelector 매개 변수에 전달된 기준과 일치하는 리드 배치에 대한 데이터를 반환합니다. 기준은 마지막 업데이트 날짜, 리드 키 배열 또는 정적 목록과 같은 날짜 범위일 수 있습니다.

참고: 리드 키 배열을 사용하는 경우 배치당 100개로 제한됩니다. 추가 키는 무시됩니다.

리드 필드의 하위 집합만 필요한 경우 `includeAttributes` 매개 변수를 사용하여 원하는 필드를 지정해야 합니다.

각 `getMultipleLeads` 함수 호출은 최대 1000개의 리드를 반환합니다. 1000개가 넘는 리드를 검색해야 하는 경우 결과는 [스트림 위치](stream-position.md)를 반환합니다. 이 위치는 이후 호출에서 1000개의 다음 배치를 검색하는 데 사용할 수 있습니다. 결과의 나머지 수는 남아 있는 잠재 고객 수를 정확히 알려줍니다. 정적 목록에서 가져올 때 종료 조건은 remainingCount == 0입니다.

이 끝점의 일반적인 사용 사례는 특정 날짜에 업데이트된 리드를 찾는 것입니다. `LastUpdateAtSelector`을(를) 사용하면 이 작업을 수행할 수 있습니다.

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| leadSelector | 필수 | 다음 세 가지 형식 중 하나일 수 있습니다.`LeadKeySelector`, `StaticListSelector`,`LastUpdateAtSelector` |
| 키 유형 | 필수 | 쿼리할 ID 유형입니다. 값에는 IDNUM, COOKIE, EMAIL, LEADOWNEEREMAIL, SFDCACCOUNTID, SFDCCONTACTID, SFDCLEADID, SFDCLEADOWNERID, SFDCOPPTYID가 포함됩니다. |
| 키 값->문자열 항목 | 필수 | 키 값 목록. 즉, &quot;lead@email.com&quot; |
| 마지막 업데이트: leadSelector->oldestUpdatedAt | 필수 | &quot;이후&quot; 기준을 지정하는 타임스탬프입니다. 즉, 지정된 시간 이후 업데이트된 모든 리드 반환 (W3C WSDL 날짜-시간 형식) |
| 마지막 업데이트: leadSelector->latestUpdatedAt | 선택 사항 | &quot;종료&quot; 기준을 지정하는 타임스탬프입니다. 즉, 지정된 시간까지 업데이트된 모든 리드를 반환합니다. (W3C WSDL 날짜-시간 형식) |
| StaticListSelector: leadSelector->staticListName | `leadSelector->staticListId`이(가) 있는 경우 선택 사항 | 정적 목록의 이름 |
| StaticListSelector: leadSelector->staticListId | `leadSelector->staticListName`이(가) 있는 경우 선택 사항 | 정적 목록의 ID |
| lastUpdatedAt | **사용되지 않음** | 대신 `LastUpdateAtSelector` 사용 |
| includeAttributes | 선택 사항 | 가져오려는 속성 목록입니다. 반환되는 리드 필드를 제한하면 API의 응답 시간을 향상시킬 수 있습니다. |
| batchSize | 선택 사항 | 반환할 최대 레코드 수. 시스템이 100 또는 `batchSize` 중 더 작은 값으로 제한됩니다. |
| streamPosition | 선택 사항 | 많은 수의 잠재 고객 응답을 통해 페이지를 매기는 데 사용됩니다. 이전 호출 응답 필드 `newStreamPosition`에서 `streamPosition` 값을 반환했습니다. |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>146ec93f4f1e2a45f7a545f7e42e2d053c0457e7</requestSignature>
      <requestTimestamp>2013-08-02T15:47:06-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsGetMultipleLeads>
      <leadSelector xsi:type="ns1:LeadKeySelector">
        <keyType>EMAIL</keyType>
        <keyValues>
          <stringItem>formtest1@marketo.com</stringItem>
          <stringItem>joe@marketo.com</stringItem>
        </keyValues>
      </leadSelector>
      <batchSize>100</batchSize>
    </ns1:paramsGetMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successGetMultipleLeads>
      <result>
        <returnCount>2</returnCount>
        <remainingCount>0</remainingCount>
        <newStreamPosition />
        <leadRecordList>
          <leadRecord>
            <Id>65835</Id>
            <Email>formtest1@marketo.com</Email>
            <ForeignSysPersonId xsi:nil="true" />
            <ForeignSysType xsi:nil="true" />
            <leadAttributeList>
              <attribute>
                <attrName>Company</attrName>
                <attrType>string</attrType>
                <attrValue>Marketo Test</attrValue>
              </attribute>
              <attribute>
                <attrName>FirstName</attrName>
                <attrType>string</attrType>
                <attrValue>FnameForm1</attrValue>
              </attribute>
              <attribute>
                <attrName>LastName</attrName>
                <attrType>string</attrType>
                <attrValue>LnameForm1</attrValue>
              </attribute>
              <attribute>
                <attrName>LeadScore</attrName>
                <attrType>integer</attrType>
                <attrValue>16</attrValue>
              </attribute>
              <attribute>
                <attrName>Website</attrName>
                <attrType>url</attrType>
                <attrValue>marketo.com</attrValue>
              </attribute>
            </leadAttributeList>
          </leadRecord>
          <leadRecord>
            <Id>67508</Id>
            <Email>joe@marketo.com</Email>
            <ForeignSysPersonId xsi:nil="true" />
            <ForeignSysType xsi:nil="true" />
            <leadAttributeList>
              <attribute>
                <attrName>Company</attrName>
                <attrType>string</attrType>
                <attrValue>Marketo</attrValue>
              </attribute>
              <attribute>
                <attrName>Date_of_purchase</attrName>
                <attrType>date</attrType>
                <attrValue>2012-04-04</attrValue>
              </attribute>
              <attribute>
                <attrName>FirstName</attrName>
                <attrType>string</attrType>
                <attrValue>Joe</attrValue>
              </attribute>
              <attribute>
                <attrName>LastName</attrName>
                <attrType>string</attrType>
                <attrValue>Orante</attrValue>
              </attribute>
              <attribute>
                <attrName>LeadScore</attrName>
                <attrType>integer</attrType>
                <attrValue>11</attrValue>
              </attribute>
            </leadAttributeList>
          </leadRecord>
        </leadRecordList>
      </result>
    </ns1:successGetMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 샘플 코드 - PHP

```php
<?php
$debug = true;
$marketoSoapEndPoint    = "";  // CHANGE ME
$marketoUserId      = "";  // CHANGE ME
$marketoSecretKey   = "";  // CHANGE ME
$marketoNameSpace   = "http://www.marketo.com/mktows/";
 
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
$options = array("connection_timeout" => 15, "location" => $marketoSoapEndPoint);
if ($debug) {
  $options["trace"] = 1;
}
 
// Create Request
/*  
//Query by Email
$leadSel = new stdClass();
$leadSel->keyType = 'EMAIL';
$keyValues = array("formtest1@marketo.com", "joe@marketo.com");
$leadKeys = new stdClass();
$leadKeys->stringItem = $keyValues;
$leadSel->keyValues = $leadKeys;
$leadSelSoap = new stdClass();
$leadSelSoap = array("leadSelector" => $leadSel);
// $leadSelParams = array("leadSelector" => $leadSelSoap, "batchSize" => 10, "streamPosition" => $startPosition);
// $params = array("paramsGetMultipleLeads" => $leadSelParams);
$leadSelSoap = new SoapVar($leadSel, SOAP_ENC_OBJECT, "LeadKeySelector", "http://www.marketo.com/mktows/");
*/
 
/*
// Query by Update time
$leadSel = new stdClass();
$leadSel->latestUpdatedAt = "2013-08-06T15:45:00-07:00";
$leadSel->oldestUpdatedAt = "2013-08-06T12:00:00-07:00";
$leadSelSoap = new stdClass();
$leadSelSoap = array("leadSelector" => $leadSel);
$leadSelSoap = new SoapVar($leadSel, SOAP_ENC_OBJECT, "LastUpdateAtSelector", "http://www.marketo.com/mktows/");
*/
 
// Query from a Static List
$leadSel = new stdClass();
//ProgramName.ListName
$leadSel->staticListName = "SMSProgram.listForTesting";
$leadSelSoap = new stdClass();
$leadSelSoap = array("leadSelector" => $leadSel);
$leadSelSoap = new SoapVar($leadSel, SOAP_ENC_OBJECT, "StaticListSelector", "http://www.marketo.com/mktows/");
 
$params->leadSelector = $leadSelSoap;
$params->streamPosition = $startPosition;
$params->batchSize = 100;
$soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
try {
  $leads = $soapClient->__soapCall('getMultipleLeads', array($params), $options, $authHdr);
}
catch(Exception $ex) {
  var_dump($ex);
}
if ($debug) {
  print "RAW request:\n" .$soapClient->__getLastRequest() ."\n";
  print "RAW response:\n" .$soapClient->__getLastResponse() ."\n";
}
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
 
 
public class GetMultipleLeads {
 
    public static void main(String[] args) {
        System.out.println("Executing GetMultipleLeads");
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
            ParamsGetMultipleLeads request = new ParamsGetMultipleLeads();
             
            // Request Using LeadKey Selector
            ////////////////////////////////////////////////////////
            LeadKeySelector keySelector = new LeadKeySelector();
            keySelector.setKeyType(LeadKeyRef.EMAIL);
             
            ArrayOfString aos = new ArrayOfString();
            aos.getStringItems().add("formtest1@marketo.com");
            aos.getStringItems().add("joe@marketo.com");
            keySelector.setKeyValues(aos);
            request.setLeadSelector(keySelector);
 
            /*
            // Request Using LastUpdateAtSelector
            ////////////////////////////////////////////////////////
            LastUpdateAtSelector leadSelector = new LastUpdateAtSelector();
             
            GregorianCalendar gc = new GregorianCalendar();
            gc.setTimeInMillis(new Date().getTime());
            gc.add( GregorianCalendar.DAY_OF_YEAR, -2);
             
            DatatypeFactory factory = DatatypeFactory.newInstance();
 
            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<XMLGregorianCalendar> until =objectFactory.createLastUpdateAtSelectorLatestUpdatedAt(factory.newXMLGregorianCalendar(gc));            
             
            GregorianCalendar since = new GregorianCalendar();
            since.setTimeInMillis(new Date().getTime());
            since.add( GregorianCalendar.DAY_OF_YEAR, -5);
             
            leadSelector.setOldestUpdatedAt(factory.newXMLGregorianCalendar(since));
            leadSelector.setLatestUpdatedAt(until);     
             
            request.setLeadSelector(leadSelector);
            */
 
            /*
            // Request Using StaticList Selector
            ////////////////////////////////////////////////////////
            StaticListSelector staticListSelector = new StaticListSelector();
 
            //staticListSelector.setStaticListId(value)
            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<String> listName = objectFactory.createStaticListSelectorStaticListName("SMSProgram.listForTesting");
            staticListSelector.setStaticListName(listName);
             
            // JAXBElement<Integer> listId = objectFactory.createStaticListSelectorStaticListId(6926);
            // staticListSelector.setStaticListId(listId);
             
            request.setLeadSelector(staticListSelector);
            */
 
 
            ArrayOfString attributes = new ArrayOfString();
            attributes.getStringItems().add("FirstName");
            attributes.getStringItems().add("AnonymousIP");
            attributes.getStringItems().add("Company");
             
            request.setIncludeAttributes(attributes);
             
            JAXBElement<Integer> batchSize = new ObjectFactory().createParamsGetMultipleLeadsBatchSize(10);
            request.setBatchSize(batchSize);
             
            SuccessGetMultipleLeads result = port.getMultipleLeads(request, header);
             
            JAXBContext context = JAXBContext.newInstance(SuccessGetLead.class);
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
request = {
    :lead_selector => {
        :key_type => "EMAIL",
        :key_values => {
            :string_item => ["formtest1@marketo.com", "joe@marketo.com"]
        }
        
    },
    :batch_size => "100"
}

response = client.call(:get_multiple_leads, message: request)

puts response
```
