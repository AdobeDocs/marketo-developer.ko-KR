---
title: 가져오기 대상 목록
feature: SOAP
description: importToList SOAP 호출
exl-id: 7e4930a9-a78f-44a3-9e8c-eeca908080c8
source-git-commit: 8a019985fc9ce7e1aa690ca26bfa263cd3c48cfc
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 3%

---

# 가져오기 대상 목록

이 함수를 사용하면 Marketo UI의 목록 가져오기 함수와 유사한 Marketo의 기존 정적 목록으로 리드 목록을 가져올 수 있습니다.

**가져오기 형식:** 이 값은 목록 가져오기에 사용된 CSV의 구조와 동일합니다.

**예:**

| 이메일 | 첫 번째 | 마지막 |
| --- | --- | --- |
| joe@company.com | Joe | Smith |
| mary@company.com | Mary | 로저스 |
| wanda@megacorp.com | 완다 | 윌리엄스 |

`name` 값이 아닌 `importFileHeader`에서 `displayName` 값을 사용해야 합니다.

**다이내믹 전자 메일 콘텐츠:** 선택적으로, 전자 메일에서 내 토큰에 대한 대체 요소로 작용하는 리드별로 값을 전달할 수 있습니다.

| 이메일 | 첫 번째 | 마지막 | {{my.specialToken}} | {{my.otherToken}} |
| --- | --- | --- | --- | --- |
| joe@company.com | Joe | Smith | 물고기 | 파랑 |
| mary@company.com | Mary | 로저스 | 치킨 | 갈색 |
| wanda@megacorp.com | 완다 | 윌리엄스 | 채소 | 헤이즐 |

**중요:** 잠재 고객에 대한 토큰을 추가하는 경우 해당 토큰을 사용하는 Smart Campaign을 지정해야 합니다. 다음에 지정된 스마트 캠페인이 실행될 때 일반 내 토큰 값 대신 목록의 값이 사용됩니다. 단일 Campaign 실행 후 토큰이 삭제됩니다.

`importToList`은(는) 특히 큰 목록의 경우 완료하는 데 시간이 걸릴 수 있습니다. 다른 API 호출에서 새로 가져온 목록을 사용하려면 `importToListStatus`을(를) 사용하여 작업이 완료되었는지 확인해야 합니다.

**참고:** CSV 파일의 숫자 필드에 대해 NULL 값을 가져오면 해당 필드에 대해 &quot;데이터 값 변경&quot; 활동이 생성될 수 있습니다. 필드가 이미 비어 있는 경우에도 마찬가지입니다. &quot;데이터 값 변경됨&quot; 필터 또는 &quot;데이터 값 변경&quot; 트리거를 사용하는 모든 스마트 캠페인은 데이터가 실제로 변경되지 않더라도 해당 캠페인에 대한 잠재 고객의 자격을 초래할 수 있습니다. 이러한 필터/트리거에 대한 제한을 사용하여 가져오기를 수행할 때 리드가 잘못된 캠페인에 적합하지 않도록 하십시오.

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| programName | 필수 여부 | 정적 목록이 포함된 프로그램 이름 |
| campaignName | 선택 사항입니다 | 내 토큰 재정의를 사용하는 경우 이는 해당 토큰이 사용될 캠페인의 이름입니다. 캠페인은 지정된 프로그램 내에 있어야 합니다. |
| listName | 필수 여부 | 리드가 추가되는 Marketo의 정적 목록 이름 |
| importFileHeader | 필수 여부 | 리드 속성 및 내 토큰 이름을 포함하여 가져올 리드에 대한 열 헤더입니다. |
| importFileRows->stringItem | 필수 여부 | 쉼표로 구분된 값, 리드당 하나의 행 포함 |
| importListMode | 필수 여부 | 유효한 옵션: `UPSERTLEADS` 및 `LISTONLY` |
| clearList | 선택 사항입니다 | true인 경우 가져오기 전에 정적 목록이 지워지고 false인 경우 잠재 고객이 추가됩니다. |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>17bf0b9e412e58eec836dc557ca9433f666944b6</requestSignature>
      <requestTimestamp>2013-08-05T14:56:58-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsImportToList>
      <programName>Trav-Demo-Program</programName>
      <importFileHeader>Last Name,First Name,Job Title,Company Name,Email Address</importFileHeader>
      <importFileRows>
        <stringItem>Awesomesauce,Developer,Code Slinger,Marketo,dawesomesauce@marketo.com</stringItem>
        <stringItem>Doe,Jane,VP Marketing,Jane Consulting,jdoe@janeconsulting.com</stringItem>
      </importFileRows>
      <importListMode>UPSERTLEADS</importListMode>
      <listName>Trav-Test-List</listName>
      <clearList>false</clearList>
      <campaignName>Batch Campaign Example</campaignName>
    </ns1:paramsImportToList>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successImportToList>
      <result>
        <!-- Possible Values: COMPLETE/PROCESSING/FAILED/CANCELED -->
        <importStatus>PROCESSING</importStatus>
      </result>
    </ns1:successImportToList>
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
  $request = new stdClass();
  $request->programName = "Trav-Demo-Program";
  $request->campaignName = "Batch Campaign Example";
  $request->importFileHeader = "Last Name,First Name,Job Title,Company Name,Email Address";
 
 
  $request->importFileRows = array("Awesomesauce,Developer,Code Slinger,Marketo,dawesomesauce@marketo.com","Doe,Jane,VP Marketing,Jane Consulting,jdoe@janeconsulting.com");
  $request->importListMode = "UPSERTLEADS"; // UPSERTLEADS or LISTONLY
  $request->listName = "Trav-Test-List";
  $request->clearList = false;
  $params = array("paramsImportToList" => $request);
 
  $soapClient = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
  try {
    $response = $soapClient->__soapCall('importToList', $params, $options, $authHdr);
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
import java.util.ArrayList;
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
 
public class ImportToList {
 
    public static void main(String[] args) {
        System.out.println("Executing Import To List");
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
            ParamsImportToList request = new ParamsImportToList();
             
            request.setProgramName("Trav-Demo-Program");
            request.setCampaignName("Batch Campaign Example");
            request.setImportFileHeader("Last Name,First Name,Job Title,Company Name,Email Address");
             
            ArrayOfString rows = new ArrayOfString();
            rows.getStringItems().add("Awesomesauce,Developer,Code Slinger,Marketo,dawesomesauce@marketo.com");
            rows.getStringItems().add("Doe,Jane,VP Marketing,Jane Consulting,jdoe@janeconsulting.com");
            request.setImportFileRows(rows);
             
            request.setImportListMode(ImportToListModeEnum.UPSERTLEADS);
            request.setListName("Trav-Test-List");
            request.setClearList(false);
             
            SuccessImportToList result = port.importToList(request, header);
 
 
            JAXBContext context = JAXBContext.newInstance(SuccessImportToList.class);
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
    :program_name => "Trav-Demo-Program",
    :import_file_header => "Last Name,First Name,Job Title,Company Name,Email Address",
    :import_file_rows => {
        :string_item => ["Awesomesauce,Developer,Code Slinger,Marketo,dawesomesauce@marketo.com", "Doe,Jane,VP Marketing,Jane Consulting,jdoe@janeconsulting.com"] },
    :import_list_mode => "UPSERTLEADS",
    :list_name => "Trav-Test-List",
    :clear_list => "false",
    :campaign_name => "Batch Campaign Example"
}

response = client.call(:import_to_list, message: request)

puts response
```
