---
title: syncCustomObjects
feature: SOAP
description: Marketo syncCustomObjects SOAP을 사용하여 레코드당 상태 결과와 XML 및 PHP 예제를 사용하여 호출당 최대 100개의 사용자 지정 개체를 삽입, 업데이트 또는 업데이트할 수 있습니다.
exl-id: dbdd7ee6-f83f-4e20-b847-25a61f0f6046
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---

# syncCustomObjects

생성 또는 업데이트할 사용자 지정 개체 배열을 수락합니다(호출당 최대 100개). 작업의 결과(상태)(생성됨, 업데이트됨, 실패, 변경되지 않음, 건너뜀) 및 처리된 사용자 정의 객체가 반환됩니다. API는 다음 세 가지 작업 모드 중 하나에서 호출됩니다.

1. 삽입 - 새 객체만 삽입하고 기존 객체를 건너뜁니다.
1. 업데이트 - 기존 개체만 업데이트하고 새 개체를 건너뜁니다.
1. 업데이트 - 새 개체 삽입 및 기존 개체 업데이트

단일 API 호출에서 일부 업데이트는 성공하고 일부는 실패할 수 있습니다. 각 실패에 대해 오류 메시지가 반환됩니다.

새 사용자 지정 개체 UI로 제공된 사용자 지정 개체의 경우 UI에서 `dedupe` 필드로 지정된 필드만 `CustomObjKeyList`의 특성으로 전달될 수 있습니다. `dedupe` 필드가 아닌 링크 필드는 `customObjAttributeList`에서 특성으로 전달해야 합니다.

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| 작업 | 필수 | &quot;삽입&quot;, &quot;업데이트&quot; 또는 &quot;업데이트&quot; |
| 개체 유형 이름 | 필수 | 사용자 지정 개체 이름 |
| customObjectList->customObject->customObjKeyList->attribute | 필수 | 속성은 사용자 지정 개체를 식별하는 데 사용되는 키/값 쌍입니다. customObjKeyList에는 여러 속성이 있을 수 있습니다. |
| customObjectList->customObject->customObjAttributeList->attribute | 필수 | 키/값 쌍. 여기서 name은 필드 이름이고 value는 customObject에 삽입할 값입니다 |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>ca67d597ced5bfce7f638e96204d6e1f38d3ffe7</requestSignature>
      <requestTimestamp>2013-08-20T10:26:07-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncCustomObjects>
      <objTypeName>RoadShow</objTypeName>
      <customObjList>
        <customObj>
          <customObjKeyList>
            <attribute>
              <attrName>MKTOID</attrName>
              <attrValue>1090177</attrValue>
            </attribute>
            <attribute>
              <attrName>rid</attrName>
              <attrValue>rid1</attrValue>
            </attribute>
          </customObjKeyList>
          <customObjAttributeList>
            <attribute>
              <attrName>city</attrName>
              <attrValue>SanMateo</attrValue>
            </attribute>
            <attribute>
              <attrName>zip</attrName>
              <attrValue>94404</attrValue>
            </attribute>
            <attribute>
              <attrName>state</attrName>
              <attrValue>California</attrValue>
            </attribute>
          </customObjAttributeList>
        </customObj>
      </customObjList>
      <operation>UPSERT</operation>
    </ns1:paramsSyncCustomObjects>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncCustomObjects>
      <result>
        <syncCustomObjStatusList>
          <syncCustomObjStatus>
            <objTypeName>Roadshow</objTypeName>
            <customObjKeyList>
              <attribute>
                <attrName>MKTOID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090177</attrValue>
              </attribute>
              <attribute>
                <attrName>rid</attrName>
                <attrType xsi:nil="true" />
                <attrValue>rid1</attrValue>
              </attribute>
            </customObjKeyList>
            <status>UPDATED</status>
            <error xsi:nil="true" />
          </syncCustomObjStatus>
        </syncCustomObjStatusList>
      </result>
    </ns1:successSyncCustomObjects>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 샘플 코드 - PHP

```php
<?php
$debug = true;
$marketoSoapEndPoint    = "";  // CHANGE ME
$marketoUserId      = "";  // CHANGE ME
$marketoSecretKey   = ""; // CHANGE ME
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
$keyAttrib1 = new stdClass();
$keyAttrib1->attrName = 'MKTOID';
$keyAttrib1->attrValue = '1090177';
$keyAttrib2 = new stdClass();
$keyAttrib2->attrName = 'rid';
$keyAttrib2->attrValue ='rid1';
$keyAttrList = array($keyAttrib1, $keyAttrib2);
$keyList = new stdClass();
$keyList->attribute = $keyAttrList;
$attr1 = new stdClass();
$attr1->attrName = 'city';
$attr1->attrValue = 'SanMateo';
$attr2 = new stdClass();
$attr2->attrName = 'zip';
$attr2->attrValue = '94404';
$attr3 = new stdClass();
$attr3->attrName = 'state';
$attr3->attrValue = 'California';
$attrListArray = array($attr1, $attr2, $attr3);
$attrList = new stdClass();
$attrList->attribute = $attrListArray;
$custObj = new stdClass();
$custObj->customObjKeyList = $keyList;
$custObj->customObjAttributeList = $attrList;
$custObjList = new stdClass();
$custObjList->customObj = array($custObj);
$params = new stdClass();
$params->operation = 'UPSERT';
$params->objTypeName = 'RoadShow';
$params->customObjList = $custObjList;
$soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
try {
  $leads = $soapClient->__soapCall('syncCustomObjects', array($params), $options, $authHdr);
  //      print_r($leads);
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
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;


public class SyncCustomObjects {
    public static void main(String[] args) {
        System.out.println("Executing Sync Custom Objects");
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
            ParamsSyncCustomObjects request = new ParamsSyncCustomObjects();
            request.setObjTypeName("RoadShow");
            JAXBElement<SyncOperationEnum> operation = new ObjectFactory().createParamsSyncCustomObjectsOperation(SyncOperationEnum.UPSERT);
            request.setOperation(operation);

            ArrayOfCustomObj customObjects = new ArrayOfCustomObj();

            CustomObj customObj = new CustomObj();

            ArrayOfAttribute arrayOfKeyAttributes = new ArrayOfAttribute();
            Attribute attr = new Attribute();
            attr.setAttrName("MKTOID");
            attr.setAttrValue("1090177");

            Attribute attr2 = new Attribute();
            attr2.setAttrName("rid");
            attr2.setAttrValue("rid1");

            arrayOfKeyAttributes.getAttributes().add(attr);
            arrayOfKeyAttributes.getAttributes().add(attr2);


            JAXBElement<ArrayOfAttribute> keyAttributes = new ObjectFactory().createCustomObjCustomObjKeyList(arrayOfKeyAttributes);
            customObj.setCustomObjKeyList(keyAttributes);
            ArrayOfAttribute arrayOfValueAttributes = new ArrayOfAttribute();

            Attribute city = new Attribute();
            city.setAttrName("city");
            city.setAttrValue("SanMateo");

            Attribute zip = new Attribute();
            zip.setAttrName("zip");
            zip.setAttrValue("94404");

            Attribute state = new Attribute();
            state.setAttrName("state");
            state.setAttrValue("California");

            arrayOfValueAttributes.getAttributes().add(city);
            arrayOfValueAttributes.getAttributes().add(state);
            arrayOfValueAttributes.getAttributes().add(zip);

            JAXBElement<ArrayOfAttribute> valueAttributes = new ObjectFactory().createCustomObjCustomObjAttributeList(arrayOfValueAttributes);
            customObj.setCustomObjAttributeList(valueAttributes);

            customObjects.getCustomObjs().add(customObj);

            SuccessSyncCustomObjects result = port.syncCustomObjects(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessSyncCustomObjects.class);
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

client = Savon.client(wsdl: 'http://app.marketo.com/soap/mktows/2_3?WSDL', soap_header: headers, endpoint: marketoSoapEndPoint, namespaces: namespaces, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

#Create Request
request = {
    :obj_type_name => "RoadShow",
    :custom_obj_list => {
        :custom_obj => {
            :custom_obj_key_list => {
                :attribute => {
                    :attr_name => "MKTOID",
                    :attr_value => "1090177" },
                :attribute! => {
                    :attr_name => "rid",
                    :attr_value => "rid1" }
            },
            :custom_obj_attribute_list => {
                :attribute => {
                    :attr_name => "city",
                    :attr_value => "SanMateo" },
                :attribute! => {
                    :attr_name => "zip",
                    :attr_value => "94404" },
                :attribute! => {
                    :attr_name => "state",
                    :attr_value => "California" }
            }
        }
    },
    :operation => "UPSERT"
}

response = client.call(:sync_custom_objects, message: request)

puts response
```
