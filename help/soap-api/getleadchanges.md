---
title: "getLeadChanges"
feature: SOAP
description: "getLeadChanges SOAP 호출"
source-git-commit: d335bdd9f939c3e557a557b43fb3f33934e13fef
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---


# getLeadChanges

이 API는 다음과 같습니다 `getLeadActivity` 한 번에 여러 리드에서 작동한다는 점을 제외하면, 이 작업에서는 생성된 새 리드, 리드 필드 업데이트 및 기타 활동을 확인합니다.

결과에는 변경 사항을 초래한 활동과 [스트림 위치](stream-position.md) 큰 결과 세트의 페이지를 매깁니다.

결과에 반환할 활동 필터를 식별하는 입력 매개 변수를 포함해야 합니다. 모든 활동을 원하는 경우 빈 값이 전달될 수 있습니다. 두 개 이상의 활동 필터의 경우 활동 필터 목록을 전달하십시오.

일부 활동 유형은 &quot;웹 페이지 방문&quot;, &quot;양식 작성&quot; 및 &quot;링크 클릭&quot;입니다.

SOAP API 버전 2_2 이후에 다음을 포함할 수 있습니다. `leadSelector`.

대상 `LastUpdateAtSelector`, `oldestUpdatedAt` 값은 다음에 해당합니다. `oldestCreatedAt` 의 값 `startPosition`. 및 `latestUpdatedAt` 값은 다음에 해당합니다. `latestCreatedAt` 의 값 `startPosition`.

참고: 다음에서 지원되는 잠재 고객 수 제한: `LeadKeySelector` 은 100입니다. 리드 수가 100개를 초과하는 경우 API에 잘못된 매개 변수 예외가 발생하고 SOAP 오류가 반환됩니다.

## 요청

| 필드 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- |
| activityFilter->includeAttributes->activityType | 선택 사항(더 이상 사용되지 않음) 사용 `activityNameFilter` 대신 | 지정된 활동 유형만 포함하도록 응답을 제한합니다. 모든 활동 유형에 대해서는 WSDL을 참조하십시오. |
| activityFilter->excludeAttributes->activityType | 선택 사항 | 지정된 활동 유형을 제외하도록 응답을 제한합니다. 모든 활동 유형에 대해서는 WSDL을 참조하십시오. 참고: 둘 다 지정할 수는 없습니다 `includeAttributes` 및 `excludeAttributes` 동일한 호출 내에서. |
| activityNameFilter | 선택 사항 | 지정된 활동 필터만 포함하도록 응답을 제한합니다. |
| batchSize | 선택 사항 | 반환할 최대 레코드 수. 시스템이 1,000개로 제한됨 `batchSize`, 둘 중 더 적은 것. |
| startPosition | 필수 | 많은 수의 활동 응답을 통해 페이지를 매기는 데 사용됩니다. |
| startPosition->offset | 선택 사항 | 오프셋 값은 이전 호출 응답 필드 newStartPosition->offset에 의해 반환됩니다. |
| startPosition->oldestCreatedAt | 선택 사항 | oldestCreatedAt 이후 생성된 리드만 포함하도록 결과를 필터링하는 데 사용되는 타임스탬프입니다. 참고: 다음을 사용할 수 있습니다 `LastUpdateAtSelector->oldestUpdatedAt` 지정할 타임스탬프 `oldestCreatedAt`. |
| startPosition->activityCreatedAt | 선택 사항 | activityCreatedAt 이후 활동이 있는 리드만 포함하도록 결과를 필터링하는 데 사용되는 타임스탬프입니다. 참고: 다음을 사용할 수 있습니다 `LastUpdateAtSelector->latestUpdatedAt` 지정할 타임스탬프 `activityCreatedAt`. |
| leadSelector | 선택 사항 | 다음 3가지 유형 중 하나일 수 있습니다. `LeadKeySelector`, `StaticListSelector`, `LastUpdateAtSelector` |
| LeadKeySelector: leadSelector->keyType | 필수 | 쿼리할 ID 유형입니다. 값은 다음과 같습니다 `IDNUM`, `COOKIE`, `EMAIL`, `LEADOWNEREMAIL`, `SFDCACCOUNTID`, `SFDCCONTACTID`, `SFDCLEADID`, `SFDCLEADOWNERID`, `SFDCOPPTYID`. |
| LeadKeySelector: leadSelector->keyValues->stringItem | 필수 | 키 값 목록. 즉, &quot;lead@email.com&quot; |
| StaticListSelector: leadSelector->staticListName | 선택 사항인 경우 `leadSelector->staticListId` 있음 | 정적 목록의 이름 |
| StaticListSelector: leadSelector->staticListId | 선택 사항인 경우 `leadSelector->staticListName` 있음 | 정적 목록의 ID |

## 요청 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>59e88471266a7495590941586ef6a96849ea8e11</requestSignature>
      <requestTimestamp>2013-08-02T17:22:53-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsGetLeadChanges>
      <startPosition>
        <oldestCreatedAt>2013-08-01T00:13:13+00:00</oldestCreatedAt>
      </startPosition>
      <activityNameFilter>
        <stringItem>Visit Webpage</stringItem>
        <stringItem>Click Link</stringItem>
      </activityNameFilter>
      <batchSize>10</batchSize>
    </ns1:paramsGetLeadChanges>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successGetLeadChanges>
      <result>
        <returnCount>10</returnCount>
        <remainingCount>576</remainingCount>
        <newStartPosition>
          <latestCreatedAt xsi:nil="true" />
          <oldestCreatedAt>2013-08-01T00:13:13+00:00</oldestCreatedAt>
          <activityCreatedAt xsi:nil="true" />
          <offset>ID:1086173</offset>
        </newStartPosition>
        <leadChangeRecordList>
          <leadChangeRecord>
            <id>1037189</id>
            <activityDateTime>2013-08-01T00:00:09-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Lead Score</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>402</attrValue>
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>403</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Japanese form fillout.test time zone action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Step ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>19582</attrValue>
              </attribute>
              <attribute>
                <attrName>Choice Number</attrName>
                <attrType xsi:nil="true" />
                <attrValue>0</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>84105</attrValue>
              </attribute>
            </activityAttributes>
            <campaign>Japanese form fillout.test time zone</campaign>
            <mktPersonId>84105</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1037190</id>
            <activityDateTime>2013-08-01T02:37:17-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Marketo Social Facebook Reach</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Marketo Social Facebook Reach</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>574</attrValue>
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>571</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Form fill-out, URL: <unknown></attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1086478</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1086478</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1037193</id>
            <activityDateTime>2013-08-01T11:19:26-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Lead Score</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Visit any web page action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Step ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>11156</attrValue>
              </attribute>
              <attribute>
                <attrName>Choice Number</attrName>
                <attrType xsi:nil="true" />
                <attrValue>0</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090235</attrValue>
              </attribute>
            </activityAttributes>
            <campaign>Visit any web page</campaign>
            <mktPersonId>1090235</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1082831</id>
            <activityDateTime>2013-08-01T13:10:17-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>First Name</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>First Name</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>George</attrValue>
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Travis</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>SOAP API</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1089965</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1089965</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1082843</id>
            <activityDateTime>2013-08-01T13:10:19-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Last Name</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Last Name</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>of the Jungle</attrValue>
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Kaufman</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>SOAP API</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1089965</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1089965</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1086153</id>
            <activityDateTime>2013-08-01T13:21:51-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Urgency</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Urgency</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>25</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Operational Campaign - ML action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Source</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead update</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090236</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1090236</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1086166</id>
            <activityDateTime>2013-08-01T13:21:53-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Relative Urgency</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Relative Urgency</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Operational Campaign - ML action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Source</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead update</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090236</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1090236</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1086167</id>
            <activityDateTime>2013-08-01T13:21:53-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Relative Score</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Relative Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Operational Campaign - ML action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Source</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead update</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090236</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1090236</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1086169</id>
            <activityDateTime>2013-08-01T13:21:53-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Priority</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Priority</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>70</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Operational Campaign - ML action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Source</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead update</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090236</attrValue>
              </attribute>
            </activityAttributes>
            <mktPersonId>1090236</mktPersonId>
          </leadChangeRecord>
          <leadChangeRecord>
            <id>1086173</id>
            <activityDateTime>2013-08-01T13:21:53-05:00</activityDateTime>
            <activityType>Change Data Value</activityType>
            <mktgAssetName>Lead Score</mktgAssetName>
            <activityAttributes>
              <attribute>
                <attrName>Attribute Name</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Lead Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Old Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue />
              </attribute>
              <attribute>
                <attrName>New Value</attrName>
                <attrType xsi:nil="true" />
                <attrValue>25</attrValue>
              </attribute>
              <attribute>
                <attrName>Reason</attrName>
                <attrType xsi:nil="true" />
                <attrValue>Changed by Smart Campaign Operational Campaign - ML action Change Score</attrValue>
              </attribute>
              <attribute>
                <attrName>Step ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>12259</attrValue>
              </attribute>
              <attribute>
                <attrName>Choice Number</attrName>
                <attrType xsi:nil="true" />
                <attrValue>0</attrValue>
              </attribute>
              <attribute>
                <attrName>Lead ID</attrName>
                <attrType xsi:nil="true" />
                <attrValue>1090236</attrValue>
              </attribute>
            </activityAttributes>
            <campaign>Operational Campaign - ML</campaign>
            <mktPersonId>1090236</mktPersonId>
          </leadChangeRecord>
        </leadChangeRecordList>
      </result>
    </ns1:successGetLeadChanges>
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
$options = array("connection_timeout" => 600, "location" => $marketoSoapEndPoint);
if ($debug) {
  $options["trace"] = 1;
}
 
// Create Request
$params = new stdClass();
$filter = new stdClass();

$keyValues = array("Visit Webpage", "Click Link");
$filter->stringItem = $keyValues;
$params->activityNameFilter = $filter;

$streamPos = new stdClass();
$streamPos->oldestCreatedAt = "2013-08-01T00:13:13+00:00";
$params->startPosition = $streamPos;
$params->batchSize = 10;
$authHdr = new SoapHeader($marketoNameSpace, 'AuthenticationHeader', $attrs);
$client = new SoapClient($marketoSoapEndPoint ."?WSDL", $options);
$doPage = true;
while($doPage) {
  $success = $client->__soapCall('getLeadChanges', array($params), null, $authHdr);
  $result = $success->result;
  $doPage = ($result->remainingCount > 0);
  $streamPos = $result->newStartPosition;
  $params->startPosition = $streamPos;
  if ($debug) {
    print "RAW request:\n" .$client->__getLastRequest() ."\n";
    print "RAW response:\n" .$client->__getLastResponse() ."\n";
  }
}
return;
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
import javax.xml.datatype.XMLGregorianCalendar;
import javax.xml.datatype.DatatypeFactory;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Hex;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBElement;
import javax.xml.bind.Marshaller;
import java.util.GregorianCalendar;
 
 
public class GetLeadChanges {
 
    public static void main(String[] args) {
        System.out.println("Executing Get Lead Changes");
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
            String encryptString = requestTimestamp + marketoUserId;
             
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
            ParamsGetLeadChanges request = new ParamsGetLeadChanges();
 
            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> batchSize = objectFactory.createParamsGetLeadActivityBatchSize(10);
            request.setBatchSize(batchSize);
             
            ArrayOfString activities = new ArrayOfString();
            activities.getStringItems().add("Visit Webpage");
            activities.getStringItems().add("Click Link");
            
            JAXBElement<ArrayOfString> activityFilter = objectFactory.createParamsGetLeadChangesActivityNameFilter(activities);
            request.setActivityNameFilter(activityFilter);
             
            // Create oldestCreateAt timestamp from 5 days ago
            GregorianCalendar gc = new GregorianCalendar();
            gc.setTimeInMillis(new Date().getTime());
            gc.add( GregorianCalendar.DAY_OF_YEAR, -5);
             
            DatatypeFactory factory = DatatypeFactory.newInstance();
            JAXBElement<XMLGregorianCalendar> oldestCreateAtValue =objectFactory.createStreamPositionOldestCreatedAt(factory.newXMLGregorianCalendar(gc));
 
            StreamPosition sp = new StreamPosition();
            sp.setOldestCreatedAt(oldestCreateAtValue);
            request.setStartPosition(sp);
             
            SuccessGetLeadChanges result = port.getLeadChanges(request, header);
 
            JAXBContext context = JAXBContext.newInstance(SuccessGetLeadChanges.class);
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
    :start_position => {
        :oldest_created_at => "2013-08-01T00:13:13+00:00" },
    :activity_name_filter => {
        :stringItem => ["Visit Webpage", "Click Link"] },
    :batch_size => "10"
}

response = client.call(:get_lead_changes, message: request)

puts response
```
