---
title: 블로그 아카이브
description: 2014-2023의 Marketo 개발자 블로그 아카이브
exl-id: d7ae88dd-9938-4957-9798-db43090dab4e
source-git-commit: 36e768d562e6f69aeb70a83253dfcf41653f217a
workflow-type: tm+mt
source-wordcount: '61712'
ht-degree: 0%

---

# 블로그 아카이브

>[!INFO]
>
>Marketo 블로그의 보관 파일이며, 2014년부터 2023년까지 걸쳐 진행됩니다. 여기에서는 역사적 참조로만 제공됩니다.
>&#x200B;>일부 정보가 최신 정보가 아닐 수 있습니다.  항상 최신 기능에 대한 최신 설명서를 확인하십시오.
>

>[!IMPORTANT]
>SOAP API는 더 이상 사용되지 않으며 2026년 1월 31일 이후부터 더 이상 사용할 수 없습니다. 모든 새로운 개발은 Marketo REST API를 사용하여 수행해야 하며, 서비스가 중단되지 않도록 기존 서비스를 해당 날짜까지 마이그레이션해야 합니다. SOAP API를 사용하는 서비스가 있는 경우 마이그레이션 방법에 대한 자세한 내용은 [SOAP API 마이그레이션 안내서](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/soap/migration)를 참조하십시오.
>

>[!IMPORTANT]
>`access_token` 쿼리 매개 변수를 사용한 인증 지원이 2026년 1월 31일에 제거됩니다. 프로젝트에서 쿼리 매개 변수를 사용하여 액세스 토큰을 전달하는 경우 가능한 한 빨리 [인증 헤더](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/rest/authentication#using-an-access-token)를 사용하도록 업데이트해야 합니다. 새 개발에서는 Authorization 헤더만 사용해야 합니다.
>

## Marketo 개발자 블로그 시작

Marketo 개발자를 환영합니다! 마케터가 그 어느 때보다 성공적일 수 있도록 지원하기 위한 새로운 기능을 출시하는 Marketo에서 매우 바빴습니다. 오늘날 마케터는 뛰어난 개발자 커뮤니티의 지원을 받습니다. 이 블로그는 현대 마케터의 급속히 발전하는 요구 사항을 지원하는 웹 개발자와 소프트웨어 엔지니어를 위한 것입니다. Marketo 플랫폼이 발전함에 따라 새로운 통합 옵션과 API 버전 업데이트가 출시됩니다. 또한 Marketo 플랫폼과의 통합에 대한 코드 샘플 및 모범 사례를 공유하는 새로운 방법 문서 시리즈를 소개할 예정입니다. 이 시리즈의 첫 번째 문서에서는 API를 사용하여 Marketo 내에 저장된 사람(고객/연락처/잠재 고객)에 대한 정보를 효율적으로 검색하는 방법을 설명합니다. 위의 양식을 사용하여 구독하면 최신 정보를 유지할 수 있습니다. 새로운 문서가 게시되면 업데이트를 이메일로 보냅니다.

_David_&#x200B;이(가) _2014-03-06_&#x200B;에 게시함

## 2014년 1월 릴리스 업데이트

### Forms 2.0

Forms 2.0은 마케팅 담당자가 프로그래밍 지식 없이도 아름답고 안정적이며 유연한 웹 양식을 만들 수 있도록 해줍니다. 크게 향상된 편집기, 조건부 논리 및 강력한 디자인 외에도 이제 웹 사이트의 모든 페이지에 Marketo을 임베드하는 것이 그 어느 때보다 쉽습니다. 개발자는 JavaScript을 사용하여 핵심 기능을 확장할 수 있습니다. 사용 사례는 다음과 같습니다.

* 성공적인 제출 후 양식을 숨김으로써 방문자가 양식을 작성한 후 페이지에 남아 있게 합니다.
* 사용자 정의 비즈니스 논리를 기반으로 제출 시 사용자 정의 오류 메시지 표시
* 라이트박스 스타일 대화 상자에 양식 표시

개발자 설명서는 [여기](/help/javascript-api/forms-api-reference.md)에서 사용할 수 있습니다.

### 이제 SOAP API 버전 2_3을 사용할 수 있습니다.

* [getLeadChanges:](/help/soap-api/getleadchanges.md) 요청 필드 `activityNameFilter`을(를) 도입했습니다.
* [ListOperation:](/help/soap-api/listoperation.md) 요청 필드 `skipActivityLog`을(를) 제거함

**참고:** SOAP API 수정 버전이 이전 버전과 호환됩니다.

_Travis Kaufman_&#x200B;이(가) _2014-01-26_&#x200B;에 게시함

## Zapier Part II: Marketo 통합 발표

이전 게시물에서는 Zapier를 사용하여 외부 데이터 소스를 Marketo과 통합하는 방법에 대해 논의했습니다. 이 게시물에는 Marketo 및 기타 앱을 통합하기 위해 처음부터 나만의 Zapier 워크플로우(또는 &quot;Zap&quot;)를 구축하는 방법에 대한 실습이 제시되었습니다. Marketo에서 Zapier를 사용하는 것은 좋지만 시작하는 데 도움이 필요하십니까? 좋은 소식! Zapier는 빠르게 진행할 수 있는 Marketo용 Zaps의 몇 가지 예시를 발표했습니다.

* 새 리드 캡처
* 고객 육성
* 연락처 정보 배포
* 새로운 잠재 고객에 대한 대응

이러한 예제 외에도 Zapier의 수백 개의 다른 앱과 함께 [Marketo 통합](https://zapier.com/apps/marketo/integrations) 페이지를 탐색하고 몇 분 안에 자체 자동화된 워크플로우를 빌드할 수 있습니다. 코딩이 필요하지 않습니다. 시간을 절약하고 자동화를 통해 수동 작업을 수행할 수 있습니다. 창의력을 발휘하십시오. 하늘이 한계야!

_David_&#x200B;에 의해 _2016-06-01_&#x200B;에 게시됨

## API를 사용하여 Marketo에서 고객 및 잠재 고객 정보 검색

`getLead` 및 [`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads) SOAP API를 사용하여 Marketo 내에 저장된 고객 및 잠재 고객에 대한 정보를 검색할 수 있습니다. 고객 및 잠재 고객 정보가 업데이트되거나 Marketo에서 새 레코드가 생성될 때 다른 시스템을 업데이트하기 위해 이 정보를 정기적으로 추출해야 하는 경우가 많습니다. Marketo에서 업데이트를 폴링하기 위해 반복적으로 실행되는 코드 샘플을 보여 줍니다. 아래 다이어그램은 설정된 정기 타이머에서 발생하는 API 호출을 보여 줍니다. 사용 사례에 따라 주기적 타이머를 설정하여 10분마다 아래 코드를 실행할 수 있습니다.

[`getMultipleLeads`](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads)에 대한 첫 번째 호출은 시간 범위, batchSize 및 반환할 필드를 설정합니다. 지정된 시간 범위에서 업데이트된 Marketo 내의 모든 리드는 지정된 batchSize보다 더 많은 레코드를 사용할 수 있을 때 streamPosition과 함께 반환됩니다.

**getMultipleLeads에 대한 첫 번째 호출에 대한 SOAP 요청:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadSelector xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ns2:LastUpdateAtSelector">
    <latestUpdatedAt>2014-02-13T11:51:08.710-08:00</latestUpdatedAt>
    <oldestUpdatedAt>2014-02-12T11:51:08.713-08:00</oldestUpdatedAt>
  </leadSelector>
  <batchSize>2</batchSize>
  <includeAttributes>
    <stringItem>FirstName</stringItem>
    <stringItem>LastName</stringItem>
    <stringItem>Email</stringItem>
  </includeAttributes>
</ns2:paramsGetMultipleLeads>
```

**getMultipleLeads에 대한 첫 번째 호출의 SOAP 응답:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:successGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <result>
 <returnCount>2</returnCount><remainingCount>24</remainingCount><newStreamPosition>id:1089965:to:1392234668:tl:1392321068:os:2:rc:24</newStreamPosition><leadRecordList>
      <leadRecord>
        <Id>84105</Id>
        <Email>eimang@marketo.com</Email>
        <ForeignSysPersonId xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <ForeignSysType xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <leadAttributeList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true">
          <attribute>
            <attrName>FirstName</attrName>
            <attrType>string</attrType>
            <attrValue>French</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrType>string</attrType>
            <attrValue>Lead</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
      <leadRecord>
        <Id>1089965</Id>
        <Email>t@t.com</Email>
        <ForeignSysPersonId xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <ForeignSysType xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
        <leadAttributeList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true">
          <attribute>
            <attrName>FirstName</attrName>
            <attrType>string</attrType>
            <attrValue>George</attrValue>
          </attribute>
          <attribute>
            <attrName>LastName</attrName>
            <attrType>string</attrType>
            <attrValue>of the Jungle</attrValue>
          </attribute>
        </leadAttributeList>
      </leadRecord>
    </leadRecordList>
  </result>
</ns2:successGetMultipleLeads>
```

`<remainingCount/>` 값이 0보다 크면 `getMultipleLeads`을(를) 후속 호출하여 이전 호출에서 반환된 `<newStreamPosition/>` 값을 `<streamPosition/>` 매개 변수에 전달하여 나머지 값을 페이지로 나눕니다. **getMultipleLeads에 대한 후속 호출에 대한 SOAP 요청:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsGetMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadSelector xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ns2:LastUpdateAtSelector">
    <latestUpdatedAt>2014-02-13T11:51:08.710-08:00</latestUpdatedAt>
    <oldestUpdatedAt>2014-02-12T11:51:08.713-08:00</oldestUpdatedAt>
  </leadSelector><streamPosition>id:1089965:to:1392234668:tl:1392321068:os:2:rc:24</streamPosition><batchSize>2</batchSize>
  <includeAttributes>
    <stringItem>FirstName</stringItem>
    <stringItem>LastName</stringItem>
    <stringItem>Email</stringItem>
  </includeAttributes>
</ns2:paramsGetMultipleLeads>
```

이 논리는 `<remainingCount/>`이(가) 0보다 큰 한 계속됩니다. **위에서 설명한 시나리오를 실행하는 샘플 Java 프로그램을 아래를 참조하십시오.**

```java
import com.marketo.mktows.\*;
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
        QName serviceName = new QName("<http://www.marketo.com/mktows/>",
        "MktMktowsApiService");
        MktMktowsApiService service = new
        MktMktowsApiService(marketoSoapEndPoint, serviceName);
        MktowsPort port = service.getMktowsApiSoapPort();

        // Create Signature
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String text = df.format(new Date());
        String requestTimestamp = text.substring(0, 22) + ":" +         text.substring(22);
        String encryptString = requestTimestamp + marketoUserId ;

        SecretKeySpec secretKey = new         SecretKeySpec(marketoSecretKey.getBytes(), "HmacSHA1");

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

        // Build Request Using LastUpdateAtSelector
        LastUpdateAtSelector leadSelector = new LastUpdateAtSelector();
        GregorianCalendar gc = new GregorianCalendar();
        gc.setTimeInMillis(new Date().getTime());
        gc.add( GregorianCalendar.DAY_OF_YEAR, -20);
        DatatypeFactory factory = DatatypeFactory.newInstance();
        ObjectFactory objectFactory = new ObjectFactory();
        JAXBElement<XMLGregorianCalendar> until =         objectFactory.createLastUpdateAtSelectorLatestUpdatedAt(factory.newXMLGregorianCalendar(gc));

        GregorianCalendar since = new GregorianCalendar();
        since.setTimeInMillis(new Date().getTime());
        since.add( GregorianCalendar.DAY_OF_YEAR, -21);
        leadSelector.setOldestUpdatedAt(factory.newXMLGregorianCalendar(since));
        leadSelector.setLatestUpdatedAt(until);
        request.setLeadSelector(leadSelector);

        ArrayOfString attributes = new ArrayOfString();
        attributes.getStringItems().add("FirstName");
        attributes.getStringItems().add("LastName");
        attributes.getStringItems().add("Email");
        request.setIncludeAttributes(attributes);

        JAXBElement<Integer> batchSize = new
        ObjectFactory().createParamsGetMultipleLeadsBatchSize(2);
        request.setBatchSize(batchSize);

        SuccessGetMultipleLeads result = null;

        int count = 0;

        do {
        if (count > 0) {
        // Set the streamPosition on subsequent calls to paginate
        through large result sets
        String pos = result.getResult().getNewStreamPosition();
        JAXBElement<String> streamPos = new
        ObjectFactory().createParamsGetMultipleLeadsStreamPosition(pos);
        request.setStreamPosition(streamPos);
        }

        JAXBContext context =
        JAXBContext.newInstance(ParamsGetMultipleLeads.class);
        Marshaller m = context.createMarshaller();
        m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
        System.out.println("REQUEST:");
        m.marshal(request, System.out);
        result = port.getMultipleLeads(request, header);
        System.out.println("RESPONSE:");
        m.marshal(result, System.out);
        count = result.getResult().getReturnCount();
        } while (result.getResult().getRemainingCount() > 0);
        }

        catch(Exception e) {
        // Update to include appropriate retry/error handling
        e.printStackTrace();
        }

  }

}
```

### 팁 및 요령

Marketo에서 대량의 연락처를 추출할 때 다음 매개 변수에 따라 API 요청을 조정하는 것이 좋습니다.

* `<includeAttributes/>`: 시스템과 계속 동기화하려는 필드만 요청하는 것이 좋습니다. 이렇게 하면 응답의 페이로드가 줄어들고 쿼리 성능이 향상됩니다.
* `<batchSize/>`: API는 한 번의 호출로 최대 1000개의 레코드를 반환할 수 있도록 지원합니다. 이 값을 500개의 레코드로 조정하면 응답의 페이로드도 줄어듭니다.
* `<LastUpdatedAtSelector/>`: 날짜 범위를 제한하려면 `<oldestUpdatedAt/>`을(를) `<latestUpdatedAt/>` 매개 변수와 함께 설정하는 것이 좋습니다. 예를 들어 1년 동안의 데이터에 대해 한 번의 요청을 하는 대신 더 작은 날짜 범위를 요청하기 위해 API 호출을 분류합니다.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_Travis Kaufman_&#x200B;이(가) _2014-03-05_&#x200B;에 게시함

## 2014년 2월 릴리스 업데이트

### SOAP API 업데이트

* [syncMObjects](/help/soap-api/syncmobjects.md): 이제 기존 프로그램의 태그와 채널을 추가하고 업데이트할 수 있습니다.

업데이트가 [2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL)에 통합됩니다.

_Travis Kaufman_&#x200B;이(가) _2014-02-26_&#x200B;에 게시함

## 2014년 3월 릴리스 업데이트

### SOAP API 업데이트

* [syncLead](/help/soap-api/synclead.md) 및 [syncMultipleLeads](/help/soap-api/syncmultipleleads.md)에 대한 성능 개선

업데이트가 [2_3 WSDL](http://app.marketo.com/soap/mktows/2_3?WSDL)에 통합됩니다.

_Travis Kaufman_&#x200B;이(가) _2014-03-20_&#x200B;에 게시함

## 방문자가 양식을 작성할 때 익명 방문자 활동 병합

&quot;비즈니스 논리를 기반으로 한 익명 방문자 활동 캡처&quot;라는 블로그 게시물에서 사용자 지정 이벤트를 기반으로 Marketo에서 익명 리드 레코드를 만드는 방법에 대해 논의했습니다. 이 블로그 게시물에서는 해당 게시물을 기반으로 하며, 사용자 연락처 정보를 받은 후 익명의 리드 레코드를 알려진 사용자와 연결합니다. Marketo의 [Munchkin 추적 코드](/help/javascript-api/lead-tracking.md)는 웹 사이트 방문 횟수를 추적하는 데 도움이 됩니다. Munchkin 추적 코드가 있는 웹 사이트의 페이지를 처음 방문하면 Marketo은 익명 리드를 만들고 브라우저 쿠키를 사용하여 이를 추적합니다. 사용자가 자신을 식별하면 알려진 리드가 되고 브라우저 쿠키와 관련된 기록이 Marketo 리드 레코드에 병합됩니다. **다른 사용자가**&#x200B;할 때 익명 잠재 고객이 만들어집니다.

1. Marketo 랜딩 페이지를 처음 방문합니다.
1. Munchkin 추적 코드가 있는 페이지를 방문합니다
1. Marketo 이메일에서 웹 페이지로 보기 링크를 클릭합니다

**다른 사람이**&#x200B;일 때 익명 잠재 고객이 알려진 새 잠재 고객 또는 기존 잠재 고객에 병합됩니다.

1. Marketo 이메일에 대한 링크 클릭
1. Marketo 양식 작성
1. 아래 방법 중 하나를 사용하여 익명의 잠재 고객을 알려진 레코드와 연결합니다.

개인 데이터를 제출하거나 브라우저 웹 추적 쿠키를 Marketo의 해당 개인 레코드와 연결하려면 다음 기법 중 하나를 사용하십시오. **브라우저측 제출** 사용 사례에서 브라우저에서 개인 데이터를 제출해야 하는 경우 백그라운드 양식 제출을 사용해야 합니다. **서버측 제출** 브라우저측 제출이 필요하지 않은 경우 REST API는 개인 데이터 제출을 위한 다양한 방법과 쿠키를 개인 레코드와 연결하기 위한 특별 제공 방법을 제공합니다.

_2014-04-22_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 2014년 4월 릴리스 업데이트

### Marketo Forms 보안 업데이트

단일 IP 주소에서 양식 게시물 제출 횟수와 빈도에 대한 제한을 도입했습니다. 이 제한은 이제 프로그램 양식 제출을 악의적으로 사용하지 않도록 고객을 보호하기 위해 분당 30회 게시물로 적용됩니다. [syncLead API](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/soap/leads/synclead)는 Marketo에서 새 연락처를 프로그래밍 방식으로 제출하기 위한 권장 통합 수단입니다.

_Travis Kaufman_&#x200B;이(가) _2014-04-29_&#x200B;에 게시함

## 통합 후 양식을 Marketo API로 바꾸기

일반적으로 Marketo을 사용하는 마케터는 특정 웹 양식을 작성한 연락처/잠재 고객 수를 기반으로 주어진 마케팅 캠페인의 성공을 연결합니다. 마케터는 단순히 새 Marketo 양식을 만들어 랜딩 페이지에 넣은 다음 Marketo에서 트리거 캠페인을 설정하여 특정 양식을 작성한 모든 연락처를 해당 마케팅 프로그램에 대한 성공으로 연결하면 됩니다. (아래 스크린샷 참조). 캠페인 성공이 양식을 작성하는 누군가의 외부에 있는 경우에도 프로그램 성공을 기록할 때 이와 동일한 접근 방식을 사용하는 것은 자연스러운 확장입니다. 예를 들어 마케터가 프로모션 오퍼를 실행하고 전환을 통해 약속을 호출하고 예약하는 것입니다. 잠재 고객은 이 프로세스의 어느 시점에서도 양식을 작성하지 않습니다. 아래 문서에서는 Marketo syncLead API를 사용하여 새 연락처가 새 연락처인 경우 새 연락처를 만든 다음 requestCampaign API를 사용하여 주어진 마케팅 프로그램에 대한 성공을 기록하는 방법을 보여 줍니다.

_Travis Kaufman_&#x200B;이(가) _1970-01-01_&#x200B;에 게시함

## Marketo API를 사용하여 잠재 고객 삭제

Marketo API를 통해 리드를 삭제한다고 가정해 보겠습니다. 리드를 삭제하기 위해 사전 정의된 흐름 작업이 있는 캠페인에서 requestCampaign API를 호출하여 이를 수행할 수 있습니다. 먼저 스마트 캠페인을 만드는 방법, 두 번째로 API를 통해 캠페인을 실행하는 트리거를 설정하는 방법, 세 번째 흐름 작업의 일부로 리드 삭제를 정의하는 방법, 네 번째 이 캠페인을 실행하는 데 사용되는 코드 샘플을 보여 줍니다. **Marketo에서 새 스마트 캠페인을 만드는 방법** Marketo의 스마트 캠페인은 모든 마케팅 활동을 실행합니다. Smart Campaign에서는 일련의 자동화된 작업을 설정하여 스마트 연락처 목록에 추가할 수 있습니다. 리드를 삭제하는 경우 아래와 같이 캠페인에서 트리거를 설정합니다. 먼저 Smart Campaign을 설정하겠습니다.

1. 마케팅 활동에서 프로그램을 선택한 다음 새로 만들기 드롭다운 아래에서 새 로컬 자산 1 을 클릭합니다. 스마트 캠페인 클릭
1. 스마트 캠페인 이름을 입력하고 스마트 캠페인에 트리거 추가 만들기 를 클릭합니다** 스마트 캠페인에 트리거를 추가하면 라이브 이벤트를 기반으로 한 번에 한 사람씩 스마트 캠페인을 실행할 수 있습니다. 이 경우 이 이벤트는 requestCampaign API를 통한 요청입니다.
1. &quot;캠페인이 요청됨&quot; 트리거를 검색한 다음 캔버스로 드래그하여 놓습니다.
1. 트리거에서 &quot;is&quot; 및 &quot;웹 서비스 API&quot;를 선택합니다.

**Campaign에서 잠재 고객 흐름 삭제 작업을 만드는 방법** 상단 메뉴에서 흐름을 클릭합니다. 오른쪽의 메뉴에서 리드 삭제를 검색한 다음 가운데로 드래그하여 캠페인에 트리거로 추가합니다. 참고: Marketo에서만 리드를 삭제하고 CRM에 두는 경우 해당 리드의 데이터가 업데이트되면 리드가 Marketo에서 다시 만들어집니다.  **requestCampaign API를 호출하는 코드 샘플** Marketo 인터페이스에서 캠페인 및 트리거를 설정한 후 API를 사용하여 이 캠페인을 실행하는 방법을 보여 줍니다. 첫 번째 샘플은 XML 요청이고, 두 번째 샘플은 XML 응답이며, 마지막 샘플은 XML 요청을 생성하는 데 사용할 수 있는 Java 코드 샘플입니다. requestCampaign API를 호출할 때 사용되는 캠페인 ID를 찾는 방법도 보여 줍니다. 또한 API를 호출하려면 Marketo 캠페인의 ID를 미리 알고 있어야 합니다. 다음 방법 중 하나를 사용하여 캠페인 ID를 결정할 수 있습니다.

1. [getCampaignsForSource](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) API 사용
1. 브라우저에서 Marketo 캠페인을 열고 URL 주소 표시줄을 봅니다. 캠페인 ID(4자리 정수로 표시됨)는 &quot;SC&quot; 바로 다음에 찾을 수 있습니다. 예, `https://app-stage.marketo.com/#SC**1025**A1`. 굵게 표시된 부분은 캠페인 ID - &quot;1025&quot;입니다. requestCampaign에 대한 SOAP 요청

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign에 대한 SOAP 응답

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

위에서 설명한 시나리오를 실행하는 샘플 Java 프로그램 아래를 참조하십시오.

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


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
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
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
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

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-05-16_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Munchkin AP를 사용한 사용자 지정 활동 추적 -

Marketo에서 사용자 지정 활동을 추적해 보겠습니다. 예를 들어 웹 페이지에 비디오가 있고 50% 이상의 비디오를 시청하는 방문자를 추적하려고 합니다. Munchkin의 사용자 지정 활동 추적 기능을 사용하여 이 작업을 수행할 수 있습니다. 이는 50%에 달하는 비디오인 페이지에서 이벤트를 수신한 다음 Munchkin API를 호출하여 구현됩니다. 이렇게 하려면 페이지의 이 이벤트를 기반으로 호출할 Marketo의 사용자 지정 활동을 설정해야 합니다. 비디오 플레이어에 YouTube을 사용하고 해당 [YouTube Iframe API](https://developers.google.com/youtube/iframe_api_reference)를 사용하여 Munchkin API에서 메서드를 호출합니다.

먼저 Marketo에서 Munchkin 추적 코드를 생성하는 방법, 두 번째 페이지 이벤트를 기반으로 트리거하기 위해 Munchkin 샘플 코드를 수정하는 방법, 세 번째 흐름 단계가 있는 페이지의 작업으로 정의되는 스마트 목록으로 캠페인을 설정하는 방법, 다섯 번째 익명 사용자의 페이지 방문이 Marketo에 기록되었는지 확인하는 방법을 보여 줍니다. ==== 이 블로그 게시물은 설명되는 코드의 라이브 예입니다. Marketo에서 잘 알려진 사용자이오니 이 양식을 작성해 주십시오. 이렇게 하면 비디오의 50%를 시청하면 나머지 비디오를 전송하고 비디오의 100%를 시청하면 다른 블로그 게시물로 연결되는 링크를 전송합니다. ===0&rbrace; 사용<https://developers.google.com/youtube/iframe_api_reference>

**Munchkin 추적 코드를 생성하는 방법** Munchkin 추적 코드를 사용하면 웹 사이트 방문 횟수를 추적할 수 있습니다. 아래에 세 가지 유형의 Munchkin 코드가 설명되어 있지만 이 예제에서는 비동기 Munchkin 추적 코드를 사용합니다. A) 단순: 가장 적은 코드 줄이 있지만 웹 페이지 로드 시간에 최적화되지 않습니다. 이 코드는 웹 페이지가 로드될 때마다 jQuery 라이브러리를 로드합니다. B) 비동기: 웹 페이지 로드 시간을 줄입니다. 이 코드는 jQuery 라이브러리가 이미 있는지 확인하고 누락된 경우 로드한 다음 웹 페이지의 나머지 부분이 로드되면 추적 코드를 실행하는 데 사용합니다. C) 비동기 jQuery: 웹 페이지 로드 시간을 줄이고 시스템 성능도 향상시킵니다. 이 코드는 사용자가 이미 jQuery를 가지고 있다고 가정하고 로드를 선택하지 않습니다.

1. 앱 오른쪽 상단에 있는 관리자 를 클릭합니다.
1. 왼쪽의 트리에서 Munchkin 를 클릭합니다.
1. 추적 코드 유형에 대해 비동기 를 선택합니다.
1. 을(를) 클릭하고 JavaScript 추적 코드를 복사하여 웹 사이트에 넣습니다. **YouTube 코드** <https://developers.google.com/youtube/js_api_reference#EventHandlers> <https://developers.google.com/youtube/iframe_api_reference> 플레이어.

`getCurrentTime()` 비디오가 재생을 시작한 이후 경과된 시간(초)을 반환합니다. `player.getDuration()` 현재 재생 중인 비디오의 지속 시간(초)을 반환합니다. `getDuration()`은(는) 비디오의 메타데이터가 로드될 때까지 0을 반환합니다. 일반적으로 비디오 재생이 시작된 직후에 발생합니다. 쿠키가 아닌 사용자가 Munchkin 추적 코드가 있는 페이지로 이동하면 사용자의 브라우저에 새 쿠키가 생성되고 Marketo에 새 익명 잠재 고객이 생성됩니다. 사용자가 이미 쿠키를 했으며 사용자가 Marketo의 기존 잠재 고객인 경우, 페이지 방문은 Marketo의 사용자 활동 로그에 기록됩니다. **쿠키 사용자 및 추적 이벤트에 대한 코드 샘플** 추적 코드를 `</body>` 태그 바로 앞에 웹 페이지에 배치합니다. Marketo에서 만든 랜딩 페이지에는 추적 코드가 자동으로 포함되어 있으므로 이 코드를 추가할 필요가 없습니다. 이 코드 샘플은 스크립트가 로드된 후 Munchkin API를 호출합니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('XXX-XXX-XXX');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```

이 코드 샘플은 사용자가 페이지에 5초 동안 있고 500픽셀을 페이지 아래로 스크롤한 후 Munchkin API를 호출합니다.

```javascript
<script src="https://code.jquery.com/jquery-2.1.0.min.js"></script>
<script type="text/javascript">
$(function(){
 setTimeout(function(){
  $(window).scroll(function() {
      var y_scroll_position = window.pageYOffset;
      var scroll_position = 500; //Sets number of pixels user must scroll to be tracked

  if(y_scroll_position > scroll_position) {
  //Munchkin tracking code
   (function() {
     var didInit = false;
     function initMunchkin() {
      if(didInit === false) {
        didInit = true;
        Munchkin.init('XXX-XXX-XXX');
      }
     }

     var s = document.createElement('script');
     s.type = 'text/javascript';
     s.async = true;
    s.src = '//munchkin.marketo.net/munchkin.js';
     s.onreadystatechange = function() {
      if (this.readyState == 'complete' || this.readyState == 'loaded') {
          initMunchkin();
      }
     };
     s.onload = initMunchkin;
     document.getElementsByTagName('head')[0].appendChild(s);
   })();
   }
 },5000); //Sets time delay before tracking user
});
</script>
```

**익명 사용자의 페이지 방문이 Marketo에 기록되었는지 확인하는 방법**

1. 상단 메뉴에서 Analytics를 클릭한 다음 새 보고서를 클릭합니다. 보고서 유형으로 웹 페이지 활동 을 선택한 다음 보고서에 이름을 지정합니다.
1. 보고서를 만든 후 Smart List를 클릭합니다. 그런 다음 오른쪽 상자에서 방문한 웹 페이지 필터를 선택합니다. Munchkin 추적 코드를 넣을 웹 페이지를 입력합니다.
1. 설정 을 클릭합니다. ISP에서 익명 방문자 를 선택하고 옵션을 표시로 변경합니다.
1. 보고서를 클릭합니다. 이제 선택한 웹 페이지에서 추적된 활동이 표시됩니다.
1. 잠재 고객 레코드를 두 번 클릭하면 익명 사용자가 방문한 특정 페이지를 볼 수 있는 활동 로그가 표시됩니다.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

예를 들어 멀티미디어 컨텐츠가 있는 페이지의 경우 사용자 지정 추적을 수행할 수 있습니다. 한 가지 일반적인 예는 페이지에 Munchkin 추적 코드를 추가하고 Munchkin API를 사용하여 비디오 재생이나 오디오 클립 청취와 같은 활동을 위해 Marketo 인스턴스에서 이벤트를 생성하는 것입니다. 대부분의 웹 페이지 또는 모든 웹 페이지에 Munchkin 추적 코드를 적용하는 것이 좋습니다. Munchkin 추적 코드는 Marketo을 사용하여 만드는 랜딩 페이지에 자동으로 포함됩니다. 이 호출을 사용하여 사용자가 Ajax, Flash 또는 기타 RIA 환경의 페이지 방문과 같은 작업을 수행했음을 기록합니다. URL에는 &quot; 또는 도메인이 포함되어서는 안 되지만, 존재하지 않는 페이지를 가리키는 것은 아닙니다. URL 매개 변수를 추가하려면 params 인수를 사용합니다.
이 이벤트는 호출 웹 페이지의 도메인 아래에 있는 사용자 활동 로그에 웹 페이지 방문 이벤트로 표시됩니다. 참고 `mktoMunchkin()`을(를) 처음 호출하면 항상 현재 페이지에 대한 [웹 페이지 방문] 이벤트가 만들어집니다. 추가 웹 페이지 방문을 추적하지 않으려면 `visitWebPage`을(를) 호출할 필요가 없습니다. `mktoMunchkinFunction('visitWebPage', { url: '/MyFlashMovie/Story1', params: 'x=y&2=3' });` 참고 숙련된 JavaScript 개발자에게 액세스할 수 있는지 확인하십시오. Marketo 기술 지원이 사용자 지정 JavaScript 문제 해결을 지원하도록 설정되지 않았습니다. Munchkin JavaScript API를 사용하면 서드파티 웹 시스템을 Marketo 계정과 통합할 수 있습니다. 일부 웹 개발을 사용하면 웹 사이트에서 새 리드를 캡처하거나 기존 애플리케이션으로 현재 리드를 업데이트할 수 있습니다. 새로운 고객 정보를 캡처하는 고객 등록용 웹 애플리케이션이 있다고 가정해 보겠습니다. 약간의 프로그래밍만으로도 Marketo에서 캡처한 해당 사용자에 대한 리드 정보와 향후 웹 추적을 위해 설정된 Marketo 쿠키를 보유할 수 있습니다.

또한 웹 개발자는 다른 기능을 사용하여 Flash 또는 Ajax와 같은 다양한 웹 환경에서 웹 활동 정보를 캡처하고 추적할 수 있습니다. 참고: 적절한 개발 리소스가 있는 경우 이 API 대신 통합을 위해 SOAP API를 사용하는 것이 좋습니다. SOAP API는 Munchkin API보다 더 강력하고 더 많은 기능을 제공합니다. Marketo SOAP API 요구 사항 이 작업을 수행하려면 웹 페이지에 Munchkin JavaScript 코드를 포함해야 합니다. Munchkin 자습서에서 필요한 스크립트 태그를 찾을 수 있습니다. 또한 자습서에 설명된 Munchkin API를 활성화합니다.
Munchkin API 호출을 수행하면 쿠키가 없는 사용자에게 자동으로 쿠키가 쿠키됩니다. Marketo에서는 개인의 활동 로그에 이벤트(링크 클릭, 웹 페이지 방문 또는 새 잠재 고객)를 기록합니다. 클릭 링크를 사용하거나 웹 페이지 호출을 방문하는 경우 해당 잠재 고객의 활동 로그(알려진 항목 또는 익명의 항목)에 이벤트가 추가됩니다. 새 잠재 고객이고 연결된 잠재 고객 호출을 사용하는 경우 해당 잠재 고객이 알려진 잠재 고객이 되고 활동 내역이 보존됩니다. 기존 잠재 고객인 경우(이메일 주소 일치 기반) 변경 또는 새 값은 해당 잠재 고객의 레코드에서 업데이트됩니다.

다음은 `munchkinFunction` 호출의 일반적인 형식입니다. 호출하려는 웹 페이지에 태그로 포함하십시오. 다른 JavaScript 함수와 같이 이 함수를 호출할 수 있습니다. 그러나 `mktoMunchkin()`을(를) 호출하기 전에 Munchkin 추적 함수 `mktoMunchkinFunction()`을(를) 호출해야 합니다.

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"> mktoMunchkin("###-###-###"); mktoMunchkinFunction('function', { key: 'value', key2: 'value'}, 'hash');
```

여기서 `###-###-###`은(는) 매개 변수를 호출 해시에 필요한 매개 변수의 배열로 만들려는 호출인 계정 함수의 Munchkin 계정 ID입니다. 이 매개 변수는 `associateLead`에만 필요합니다.

_1970-01-01_&#x200B;에 _Murta_&#x200B;에 게시됨

## Marketo으로 데이터 가져오기

아래 프레젠테이션은 Marketo으로 데이터를 가져오는 다양한 방법을 보여 줍니다. 양식, 사용자 정의 개체 및 통합에 중점을 둡니다.

[Murtza Manzur](https://www.slideshare.net/MurtzaManzur/getting-data-into-marketo-35662408)에서 [Marketo으로 데이터 가져오기](https://www.slideshare.net/MurtzaManzur)

_2014-06-06_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Workspace에서 리드 만들기

북미와 유럽이라는 두 개의 부서가 있습니다. Marketo의 회사 분할을 기준으로 리드를 세그먼트화하려고 합니다. 잠재 고객에 대한 액세스를 제한할 수 있는 Marketo의 기능인 작업 공간을 사용하여 이를 수행할 수 있습니다. 이를 위해 북미 및 유럽에 대한 작업 공간을 만듭니다. 그런 다음 [syncLead API](/help/soap-api/synclead.md)를 사용하여 특정 작업 영역에서 리드를 만들 수 있습니다. 조직에 다음이 있는 경우 작업 공간 및 리드 분할 영역 사용을 고려해야 합니다.

1. 여러 제품 라인에 대해 별도의 마케팅 팀
1. 다른 지역 또는 국가에 대해 별도의 마케팅 팀
1. 모회사 및 자회사
1. 상위 회사 및 리셀러

리드 분할 영역 및 작업 영역을 사용하는 경우 다음 작업을 수행할 수 있습니다.

1. 조직의 잠재 고객에 대한 액세스 제한
1. 조직의 자산에 대한 액세스 제한
1. 마케팅 팀 간 에셋 공유

UI를 통해 Marketo에서 작업 영역을 만드는 방법을 먼저 보여 주고, [syncLead API](/help/soap-api/synclead.md)를 사용하여 해당 작업 영역에 리드를 작성하는 방법을 두 번째로 보여 줍니다. **Workspace 만들기** 작업 영역은 리드 및 Marketo 자산 집합입니다. 작업 공간에서는 해당 작업 공간의 리드 및 해당 작업 공간의 에셋(이메일, 캠페인, 목록 등)만 볼 수 있습니다. 해당 작업 공간의 스마트 캠페인은 해당 작업 공간의 리드에만 영향을 줍니다. 계정의 작업 영역을 보려면 다음을 수행합니다.

1. 관리 섹션의 작업 공간 및 리드 파티션 페이지로 이동합니다. 작업공간이 작업공간(Workspaces) 탭에 나타납니다. 1. 새 작업 영역을 만들려면 [작업 영역] 탭의 메뉴 표시줄에서 [새 Workspace] 단추를 클릭합니다.
1. 대화 상자에서 새 작업 공간에 대한 몇 가지 정보를 추가해야 합니다.

* **Workspace 이름** - 인터페이스에 표시되는 이 작업 영역의 이름입니다.
* **설명** - 작업 영역에 대한 선택적 텍스트 설명
* **잠재 고객 파티션** - 이 파티션에 표시되는 잠재 고객.
* **모든 잠재 고객 파티션** - 현재 및 향후 모든 파티션의 잠재 고객을 봅니다.
* **개별 파티션 선택** - 해당 파티션의 리드만(이후 파티션은 표시되지 않음) 표시
* **기본 잠재 고객 파티션** - 랜딩 페이지를 방문하는 잠재 고객은 기본적으로 이 파티션에 추가됩니다.
* **언어** - 작업 영역의 비즈니스 언어

API 쓰기 를 사용하는 방법을 보여 주면 특정 작업 영역으로 연결됩니다. 첫 번째 샘플은 XML 요청이고, 두 번째 샘플은 XML 응답이며, 마지막 샘플은 XML 요청을 생성하는 데 사용할 수 있는 Ruby 코드 샘플입니다. 1. 가망 고객을 생성한 후 가망 고객 분할은 가망 고객 정보의 필드입니다. `requestCampaign`에 대한 SOAP 요청

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign에 대한 SOAP 응답

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

위에서 설명한 시나리오를 실행하는 샘플 Java 프로그램 아래를 참조하십시오.

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


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
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
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
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

**작업 영역 및 잠재 고객 파티션에 어떻게 등록합니까?** Marketo Enterprise 고객의 경우 작업 공간 및 리드 파티션에 무료로 액세스할 수 있습니다. 활성화 및 구현에 대한 자세한 내용은 고객 지원 관리자에게 문의하십시오. 다른 고객의 경우, 이 제품에 대한 자세한 내용은 Marketo 영업 담당자에게 문의하거나 Dell 영업 팀으로 이메일을 보내주십시오.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_1970-01-01_&#x200B;에 _Murta_&#x200B;에 게시됨

## 2014년 6월 릴리스 업데이트

### Marketo 실시간 Personalization API

Marketo 실시간 Personalization(RTP) JavaScript API는 플랫폼의 자동화된 개인화 기능을 확장합니다. 웹 페이지의 이벤트 추적 및 동적 사용자 지정을 허용합니다. 전체 설명서 [여기](/help/javascript-api/web-personalization.md)를 참조하세요.

_Travis Kaufman_&#x200B;이(가) _2014-06-20_&#x200B;에 게시함

## Marketo에 외래 키 저장

독점 CRM 또는 데이터 웨어하우스와 같은 시스템 간에 연락처 및 리드 레코드를 동기화할 때 리드 레코드를 고유한 시스템 식별자와 연결하는 것이 일반적인 요구 사항입니다. Marketo에서는 고유한 시스템 식별자를 사용하여 [syncMultipleLeads API](/help/soap-api/syncmultipleleads.md) 호출을 통해 리드 레코드를 만들거나 업데이트할 수 있습니다. 이를 위해 고유한 시스템 식별자(기본 키)를 Marketo에 외래 키로 저장합니다. 외래 키를 저장할 Marketo의 이 필드 이름은 foreignSysPersonId입니다. 다음 세 가지 중요 사항을 알아 두어야 합니다.

1. foreignSysPersonId가 Marketo의 UI에 표시되지 않습니다. 따라서 사용자 지정 속성 필드도 이 값으로 채우는 것이 좋습니다.
1. foreignSysPersonId는 리드에 고유하지만 리드에 두 개 이상의 foreignSysPersonId가 있을 수 있습니다.
1. foreignSysPersonId를 업데이트하거나 삭제할 수 없지만 다른 레코드에 다시 할당할 수 있습니다.

Marketo의 기존 리드 레코드 두 개에 foreignSysPersonId 값을 쓰기 위해 [syncMultipleLeads API](/help/soap-api/syncmultipleleads.md)를 호출하는 방법을 보여 줍니다. **syncMultipleLeads API를 사용하여 foreignSysPersonId를 작성하는 방법** 새 리드 레코드를 삽입하고 foreignSysPersonId를 지정할 수 있습니다. Marketo ID와 foreignSysPersonId를 모두 지정하여 기존 리드에 추가할 수도 있습니다. 후자의 경우를 소개합니다. **syncMultipleLeads SOAP API 호출을 위한 요청 XML**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809934544BFABAE58E5D27</mktowsUserId>
      <requestSignature>b5e21953ae9f1b263e644da5eccce9ff33802513</requestSignature>
      <requestTimestamp>2013-08-01T18:22:30-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsSyncMultipleLeads>
      <leadRecordList>
        <leadRecord>
          <leadId>1090240</leadId>
          <foreignSysPersonId>1224191</foreignSysPersonId>
          <leadAttributeList>
            <attribute>
              <attrName>Company</attrName>
              <attrValue>Marketo1000</attrValue>
            </attribute>
            <attribute>
              <attrName>Phone</attrName>
              <attrValue>650-555-1000</attrValue>
            </attribute>
          </leadAttributeList>
        </leadRecord>
        <leadRecord>
          <leadId>1090239</leadId>
          <foreignSysPersonId>1224192</foreignSysPersonId>
          <leadAttributeList>
            <attribute>
              <attrName>Company</attrName>
              <attrValue>Marketo1001</attrValue>
            </attribute>
            <attribute>
              <attrName>Phone</attrName>
              <attrValue>650-555-1001</attrValue>
            </attribute>
          </leadAttributeList>
        </leadRecord>
      </leadRecordList>
      <dedupEnabled>true</dedupEnabled>
    </ns1:paramsSyncMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**syncMultipleLeads SOAP API 호출에 대한 응답 XML**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncMultipleLeads>
      <result>
        <syncStatusList>
          <syncStatus>
            <leadId>1090240</leadId>
            <status>UPDATED</status>
            <error xsi:nil="true" />
          </syncStatus>
          <syncStatus>
            <leadId>1090239</leadId>
            <status>UPDATED</status>
            <error xsi:nil="true" />
          </syncStatus>
        </syncStatusList>
      </result>
    </ns1:successSyncMultipleLeads>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**위의 요청 XML을 출력하는 샘플 Ruby 프로그램을 참조하십시오.**

```java
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "<http://www.marketo.com/mktows/>"

# Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

# Create SOAP Header
headers = {
 'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,
 "requestTimestamp"  => requestTimestamp
 }
}

client = Savon.client(wsdl: '<http://app.marketo.com/soap/mktows/2_3?WSDL>', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

# Create Request
request = {
        :lead_record_list => {
                :lead_record => {
                        :lead_id => "1090240",
                        :foreign_sys_person_id => "1224191",
                :lead_attribute_list => {
                        :attribute => {
                                :attr_name => "Company",
                                :attr_value => "Marketo1000" },
                         :attribute! => {
                                :attr_name => "Phone",
                                :attr_value => "650-555-1000" }
                }
        },
        :lead_record! => {
                        :lead_id => "1090239",
                        :foreign_sys_person_id => "1224192",
                :lead_attribute_list => {
                        :attribute => {
                                :attr_name => "Company",
                                :attr_value => "Marketo1001" },
                         :attribute! => {
                                :attr_name => "Phone",
                                :attr_value => "650-555-1001" }
                }
        }
        },
    :dedup_enabled => "True"
}

response = client.call(:sync_multiple_leads, message: request)

puts response
```

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-06-27_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 잠재 고객 이메일 주소 업데이트

사용자가 사이트에서 Marketo 양식을 작성한다고 가정해 보겠습니다. 무슨 일이 일어납니까? Marketo은 사용자를 쿠키하고 쿠키를 제공한 이메일과 연결합니다. 다음에 사용자가 웹 사이트를 방문할 때 동일한 양식을 다른 이메일로 다시 작성하는 경우 어떻게 합니까? 무슨 일이 일어날까요? Marketo은 새 잠재 고객 레코드를 만들고, 사용자 브라우저의 첫 번째 쿠키를 덮어씁니다. 이제 사용자는 Marketo의 새로운/다른 리더입니다. [syncLead API 메서드](/help/soap-api/synclead.md), 양식 방법의 사용자 지정 필드, Marketo UI를 포함하여 Marketo에서 목록을 가져와서 잠재 고객의 이메일 주소를 업데이트하는 네 가지 방법을 보여 줍니다. **syncLead API를 통해** [syncLead API](/help/soap-api/synclead.md)를 사용하여 Marketo ID와 새 전자 메일 주소를 사용하여 잠재 고객 레코드를 업데이트할 수 있습니다. `syncMultipleLeads` SOAP API 호출에 대한 XML 요청

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
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
        <leadId>1090240</leadId>
        <Email>t@t.com</Email>
      </leadRecord>
      <returnLead>false</returnLead>
    </ns1:paramsSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

syncMultipleLeads SOAP API 호출에 대한 응답 XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successSyncLead>
      <result>
        <leadId>1090240</leadId>
        <syncStatus>
          <leadId>1090240</leadId>
          <status>UPDATED</status>
          <error xsi:nil="true" />
        </syncStatus>
        <leadRecord xsi:nil="true" />
      </result>
    </ns1:successSyncLead>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

위의 요청 XML을 출력하는 샘플 Ruby 프로그램을 아래를 참조하십시오.

```java
require 'savon' # Use version 2.0 Savon gem
require 'date'

mktowsUserId = "" # CHANGE ME
marketoSecretKey = "" # CHANGE ME
marketoSoapEndPoint = "" # CHANGE ME
marketoNameSpace = "<http://www.marketo.com/mktows/>"

# Create Signature
Timestamp = DateTime.now
requestTimestamp = Timestamp.to_s
encryptString = requestTimestamp + mktowsUserId
digest = OpenSSL::Digest.new('sha1')
hashedsignature = OpenSSL::HMAC.hexdigest(digest, marketoSecretKey, encryptString)
requestSignature = hashedsignature.to_s

# Create SOAP Header
headers = {
 'ns1:AuthenticationHeader' => { "mktowsUserId" => mktowsUserId, "requestSignature" => requestSignature,
 "requestTimestamp"  => requestTimestamp
 }
}

client = Savon.client(wsdl: '<http://app.marketo.com/soap/mktows/2_3?WSDL>', soap_header: headers, endpoint: marketoSoapEndPoint, open_timeout: 90, read_timeout: 90, namespace_identifier: :ns1, env_namespace: 'SOAP-ENV')

# Create Request
request = {
 :lead_record => {
  :Email => "<t@t.com>",
  :lead_id => "1090240",
 :return_lead => "false"
}

response = client.call(:sync_lead, message: request)

puts response
```

**양식의 사용자 지정 필드를 통해** Marketo에서 &quot;새 전자 메일 주소&quot;에 대한 사용자 지정 필드를 만들 수 있습니다. 그런 다음 사용자에게 이 새 필드가 포함된 양식을 작성하도록 요청합니다. 그런 다음 새 사용자 지정 필드 &quot;새 전자 메일 주소&quot;가 변경되면 토큰 `{{lead.newEmailAddress}}`을(를) 사용하여 시스템 전자 메일 주소 필드의 데이터 값을 변경하는 프로그램을 Marketo에서 만듭니다. **Marketo UI를 통해** Marketo UI를 통해 잠재 고객의 이메일 주소를 수동으로 업데이트할 수 있습니다. 이 작업을 수행하는 방법을 설명하는 [도움말 문서](https://nation.marketo.com/)가 있습니다(문서를 보려면 Marketo 로그인이 필요). **목록 가져오기를 통해** [여기](https://nation.marketo.com/)에 설명된 Marketo에서 목록 가져오기 메서드를 사용하여 잠재 고객의 전자 메일 주소를 업데이트할 수 있습니다(문서를 보려면 Marketo 로그인이 필요).  

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_1970-01-01_&#x200B;에 _Murta_&#x200B;에 게시됨

## 잠재 고객의 두 번째 이메일 주소 저장

API를 사용하여 Marketo에서 잠재 고객의 점수를 변경하려고 한다고 가정해 보겠습니다. 리드 만들기/업데이트 끝점을 사용하여 REST API로 수행할 수 있습니다. 잠재 고객 레코드에 두 개 이상의 이메일을 저장하려면 사용자 정의 필드를 만들고 두 번째 이메일을 해당 필드에 저장해야 합니다. 다음은 추가 정보가 포함된 도움말 문서입니다. 다음은 이 호출을 수행하는 방법을 보여 주는 Ruby의 코드 샘플입니다.

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
request_url = marketo_instance + endpoint + auth_token

# Build request body
data = { "action" => "updateOnly", "input" => [ { "email" => "<example@email.com>", "leadScore" => "30" } ] }

# Make request
response = RestClient.post request_url, data.to_json, :content_type => :json, :accept => :json

# Returns Marketo API response
puts response
```

_2015-02-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo에서 사용자 정의 필드를 만들고 AP를 통해 이 필드 업데이트

표준 Marketo 필드에 맞지 않는 잠재 고객에 대한 추가 데이터가 있다고 가정해 보겠습니다. 예를 들어 이 사용자 지정 필드는 서드파티 점수일 수 있습니다. Marketo에서 타사 점수에 대한 사용자 지정 필드를 만든 다음, Marketo [REST API](https://developer.adobe.com/marketo-apis/) 또는 [SOAP API](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/soap/activity-type-filters)를 통해 이 필드의 값을 업데이트할 수 있습니다. 먼저 Marketo에서 사용자 정의 필드를 만드는 방법을 보여 주고, 두 번째로 REST API를 사용하여 이 필드를 업데이트하는 방법을 보여 줍니다.

### Marketo에서 사용자 정의 필드를 만드는 방법

1. 관리자 아래에서 필드 관리 를 클릭합니다.
1. 새 사용자 정의 필드 단추를 클릭합니다.
1. 필드 유형을 선택합니다. 따라서 Marketo의 스마트 목록 및 Forms에서 렌더링되는 방식이 변경됩니다.
1. Marketo에 표시할 이름을 입력합니다. 필드 이름을 바꾸는 것은 어려울 수 있고 경우에 따라 가능하지 않을 수 있으므로 이름 및 API 이름을 신중하게 선택하십시오.
1. 만든 사용자 정의 필드는 이제 API를 통해 액세스할 수 있습니다.

### REST API를 통해 사용자 정의 필드를 업데이트하는 방법

이전 섹션에서 데이터 형식 문자열을 사용하여 사용자 지정 필드 `myCustomField`을(를) 만들었습니다. 해당 필드의 값을 업데이트하려면 리드 만들기 / 업데이트 라는 REST API 엔드포인트를 사용합니다. REST API에 요청하려면 먼저 인증해야 합니다. 이 문서는 이 문서의 범위를 벗어나지만 자세한 정보 [은(는) Marketo 개발자의 사이트](/help/rest-api/authentication.md)에서 사용할 수 있습니다.

**끝점**

`/rest/v1/leads.json`

**요청 본문**

```json
{
   "action":"createOrUpdate",
   "input":[
      {
         "email":"<example@example.com>",
         "myCustomField":"examplestring"
      }
   ]
}
```

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-08-19_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 언바운스 및 Marketo 통합

**참고: Fab Capodicasa의 게스트 블로그 게시물입니다. B2C를 전문으로 하는 Marketo LaunchPoint 에이전시 파트너인 [Hoosh Marketing](http://hooshmarketing.com.au/)의 Marketo 인증 컨설턴트입니다. 그는 지난 13년 동안 SaaS와 마케팅에 모두 종사했습니다. 그의 배경에는 하드코어 IT, 다이렉트 마케팅, 기업영업이 혼재돼 있다. Fab도 이전 Marketo 직원입니다.**

**개요** 이 문서에서는 인기 있는 랜딩 페이지 도구인 Unbounce를 Marketo과 통합하는 방법을 보여 줍니다. 먼저 Marketo 추적을 언바운스에 삽입하는 방법을 보여 주고, 다음으로 언바운스 양식을 수정하여 데이터를 Marketo에 직접 삽입하는 방법을 보여 줍니다. Marketo과 Unbounce를 통합하기 위해서는 Unbounce에서 기본 필드의 이름을 바꿀 수 없다는 문제가 발생합니다(예: first_name을 FirstName으로 변경할 수 없음). 또한 필드 레이블이 필드 이름과 달라지는 것을 허용하지 않습니다. 이 통합에는 JavaScript이 포함되며, 기존 양식을 변경하여 Marketo과 호환되도록 합니다. 이 문서의 작업을 완료하려면 적어도 JavaScript의 초급 수준과 Marketo의 중간 수준 지식을 갖춘 것이 좋습니다.
**1부: 언바운스에 Marketo 추적 코드 추가** 언바운스 페이지에 Marketo Munchkin 추적 스크립트를 추가하는 것은 analytics와 양식 통합이 모두 작동하기 위해 필요합니다. 다음 단계를 따르십시오. Marketo에서 Munchkin 코드를 복사합니다. 관리 -> Munchkin으로 이동하여 JavaScript의 &#39;단순&#39; 버전을 복사합니다. 언바운스 랜딩 페이지를 열고 JavaScript-> 새 JavaScript 추가 를 클릭합니다.  추가 를 클릭하고, 스크립트 &#39;Munchkin&#39;를 호출하고, &#39;본문 끝 태그 전&#39;을 선택한 다음 Munchkin 코드를 붙여넣습니다. 완료(Done) 단추를 누릅니다. 이후 언바운스 페이지의 경우 JavaScript으로 이동하여 만든 Munchkin 스크립트를 활성화합니다. 다시 만들 필요가 없습니다.
**2부: 언바운스 양식을 Marketo 양식으로 변환** 이제 언바운스 랜딩 페이지에서 잠재 고객 정보를 Marketo에 직접 제출할 수 있도록 몇 가지 새로운 숨겨진 필드와 JavaScript을 추가하여 언바운스 양식을 수정해야 합니다. 먼저 Marketo 자리 표시자 양식을 만듭니다. Marketo에서 빈 양식을 만들고 승인합니다.

언바운스 양식을 나타내는 Marketo의 프록시 양식입니다. 바운스 취소 양식에 숨겨진 필드를 추가합니다. Marketo에서는 이 양식 제출이 적용될 Marketo 인스턴스, 양식 및 사용자 세션을 결정하기 위해 이러한 숨김 필드가 필요합니다. 언바운스에서 두 번 클릭하여 양식을 엽니다. `_mkt_trk`(이)라는 숨겨진 필드를 추가합니다. `formid`(이)라는 두 번째 숨겨진 필드를 추가합니다.  233은 양식 id로 대체해야 합니다. 이 id는 Marketo의 Marketo 양식 포함 코드에서 찾을 수 있습니다. Marketo에서 양식을 열고 양식 작업->포함 코드 를 선택합니다. `returnurl`(이)라는 숨겨진 필드를 추가합니다. `http://hooshmarketing.com.au/thank-you`은(는) 후속 URL로 대체해야 합니다. 양식을 제출한 후 사용자가 리디렉션될 URL입니다. 예를 들어 감사 인사 페이지일 수 있습니다.
**3부: Marketo에 직접 바운스 취소 양식** 후속 URL은 리드가 Marketo에 제출된 후 리드가 리디렉션되는 페이지입니다. 언바운스에서 다음 단계를 따르십시오. 양식을 클릭합니다. 양식 확인 섹션을 수정합니다. 양식 데이터를 URL에 게시하는 확인을 변경합니다. URL을 원하는 후속 페이지로 설정합니다. `fpmarkets`은(는) Marketo 계정 문자열로 대체해야 합니다. 이 문자열은 관리자->랜딩 페이지 아래의 Marketo에 있습니다.
**파트 4: JavaScript을 바운스 해제 페이지에 추가** 이 JavaScript은 양식을 Marketo과 호환되도록 변환하고 Marketo에 제출합니다. 언바운스에서 다음 단계를 따르십시오. 언바운스 랜딩 페이지를 열고 JavaScript-> 새 JavaScript 추가를 클릭합니다. 추가를 클릭하고 &#39;Marketo 양식 변환&#39; 스크립트를 호출한 다음 &#39;본문 끝 태그 전&#39;을 선택합니다. 아래에 JavaScript 코드를 붙여넣습니다.

```javascript
var MARKETO_MUNCHKIN_ID='614-CGT-700';
var MARKETO_ACCOUNT_STRING = 'fpmarkets';

var UNBOUNCE_MARKETO_FIELD_MAP = new Object();

//default field mappings
UNBOUNCE_MARKETO_FIELD_MAP['first_name'] = 'FirstName';
UNBOUNCE_MARKETO_FIELD_MAP['email'] = 'Email';
UNBOUNCE_MARKETO_FIELD_MAP['last_name'] = 'LastName';
UNBOUNCE_MARKETO_FIELD_MAP['phone_number'] = 'Phone';

function getMarketoField(k) {
    return UNBOUNCE_MARKETO_FIELD_MAP[k];
}


var formFields = [];
var hiddenClonedFields = [];
var firstForm = document.forms[0];

//Convert Unbounce form names to Marketo field names
for(i=0; i<firstForm.elements.length; i++){
 var formField = firstForm.elements[i];
 var newFieldName = getMarketoField(formField.name);

  if(newFieldName != undefined) {


    //save original field as hidden field
    var hiddenField = document.createElement("input");
    hiddenField.setAttribute("type", "hidden");
    hiddenField.setAttribute("name", formField.name);
    hiddenField.setAttribute("id", formField.id);
    hiddenClonedFields.push(hiddenField);

    //change original field
    console.log ( 'Changed form field name: ' + formField.name + '=>' + newFieldName );
    formField.name = newFieldName;
    formField.id = newFieldName;
    formFields.push(formField);


  } else {
    console.log ( 'Couldn't map:' + formField.name );
  }
}

//Add hidden cloned Unbounce fields to form
//for Unbounce validation
for(i=0; i<hiddenClonedFields.length; i++){
    firstForm.appendChild(hiddenClonedFields[i]);
    formFields[i].onchange = (function(hf) {
        return function(event) {
            hf.value = event.target.value;
          console.log('Changed hidden cloned field:' + hf.name + '=>' + hf.value);
        };
    }(hiddenClonedFields[i]));
    console.log ( 'Added cloned field: ' + hiddenClonedFields[i].name );
}


//Add MunchkinId to form
var input = document.createElement("input");
input.setAttribute("type", "hidden");
input.setAttribute("name", "munchkinId");
input.setAttribute("value", MARKETO_MUNCHKIN_ID);
firstForm.appendChild(input);
console.log('Added hidden field:' + input.name + '=' + input.value);
```

언바운스와 호환되지 않는 API 이름이 있는 사용자 지정 필드가 있는 경우, JavaScript에서 해당 필드를 매핑에 추가할 수 있습니다. 예를 들어, Marketo에서 사용자 정의 필드 중 하나가 `Comments_c`인데 필드 레이블을 주석으로 표시하려는 경우 Unbounce를 사용하면 필드 이름을 `Comments_c`(으)로 변경할 수 없습니다.

```
//default field mappings
UNBOUNCE_MARKETO_FIELD_MAP['comments'] = 'Comments_c';
UNBOUNCE_MARKETO_FIELD_MAP['first_name'] = 'FirstName';
UNBOUNCE_MARKETO_FIELD_MAP['email'] = 'Email';
```

_comments는 언바운스에 있는 필드의 이름입니다. _Comments_c_은(는) Marketo의 필드 이름입니다. 나중에 언바운스 페이지의 경우 JavaScript으로 이동하여 만든 Munchkin 스크립트를 활성화하면 됩니다. 다시 만들 필요가 없습니다.
**파트5: 테스트** 마지막 단계는 이 양식 통합이 제대로 작동하는지 테스트하는 것입니다. Marketo 양식 채우기에서 활성화되고 리드가 Marketo에 올바르게 삽입되는지 확인하는 Marketo 트리거를 만듭니다. 양식 제출 후 페이지는 후속 URL로 리디렉션되어야 합니다.

_2014-08-04_&#x200B;에 게시한 사람: _

## 2014년 7월 릴리스 업데이트

### Munchkin 업데이트

Munchkin의 새 버전은 141입니다. 버전 142는 지원되지 않으며 2011년 9월 초에 제거됩니다. 버전 142에는 개발자 사이트에 문서화되지 않은 공개적으로 액세스할 수 있는 기능이 있었다. 문서화되지 않은 기능은 더 이상 공개적으로 사용할 수 없습니다. 개발자 사이트에 문서화된 기능은 장기적으로 계속 지원됩니다.

### RTP 업데이트

RTP API에는 방문자 데이터 가져오기 라는 새로운 기능이 있습니다. 이 RTP API 호출을 사용하면 조직, 업계, 위치 및 세그먼트 코드와 같은 실시간 방문자 데이터를 가져올 수 있습니다.

_2014-07-30_&#x200B;에 _Murta_&#x200B;에 게시됨

## 단일 페이지에서 여러 Munchkin 추적 코드 사용

여러 Marketo 인스턴스가 있고 이러한 여러 인스턴스에 대한 페이지 방문 또는 클릭한 링크와 같은 웹 추적 이벤트를 전송하려고 한다고 가정해 보겠습니다. Munchkin을 사용하면 이러한 작업을 수행할 수 있습니다. Marketo은 도메인별로 웹 사이트 방문자를 추적합니다(예: &quot;marketo.com&quot;). 기본 도메인과 다른 도메인(예: &quot;company.com&quot;)에서 이 Munchkin 스크립트를 호스팅하는 경우 해당 방문자가 다른 도메인에서 양식을 작성할 때까지 익명 리드로 표시됩니다. 이렇게 하려면 `altIds` 호출에 `Munchkin.init` 매개 변수를 추가하십시오. altIds 매개 변수에는 웹 이벤트를 전송해야 하는 추가 Munchkin ID 배열이 포함됩니다. 아래 예를 사용하여 강조 표시된 Munchkin ID(XXX-XXX-XXX, YYY-YYY 및 ZZZ-ZZZ-ZZZ)를 추적 정보를 전송해야 하는 각 Marketo 인스턴스의 Munchkin ID로 교체합니다.

```javascript
<script src="http://munchkin.marketo.net/munchkin.js" type="text/javascript"></script>
<script>Munchkin.init('XXX-XXX-XXX', { altIds:['YYY-YYY-YYY', 'ZZZ-ZZZ-ZZZ'] });</script>
```

Munchkin 초기화 매개 변수에 대한 자세한 내용은 [이 문서](/help/javascript-api/configuration.md)를 참조하십시오.

_2014-08-08_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Munchkin과 Google Tag Manage 통합

Google Tag Manger를 사용하면 웹 사이트에 태그를 추가할 수 있습니다. Munchkin과 같은 각 추적 스크립트를 웹 사이트의 소스 코드에 수동으로 추가하는 대신 사이트에 [Google 태그 관리자](https://marketingplatform.google.com/about/tag-manager/)를 추가한 다음 Google 태그 관리자의 UI를 통해 [Munchkin](/help/javascript-api/lead-tracking.md)과 같은 태그를 추가할 수 있습니다. 이 게시물에서는 먼저 Marketo에서 Munchkin 추적 코드를 생성하는 방법을 보여 준 다음, 이 Munchkin 추적 코드를 Google 태그 관리자에 추가하는 방법을 보여 줍니다.

### Munchkin 추적 코드를 생성하는 방법

1. 앱 오른쪽 상단의 **관리자**&#x200B;를 클릭합니다.
1. 왼쪽의 트리에서 **Munchkin**&#x200B;을(를) 클릭합니다.
1. 추적 코드 유형으로 **비동기**&#x200B;을(를) 선택하십시오.
1. 을(를) 클릭하고 JavaScript 추적 코드를 복사합니다.

**Google 태그 관리자에 Munchkin 추적 코드를 추가하는 방법**

1. Google 태그 관리자 계정에 로그인하고 **새 태그를 추가합니다.**
1. 새 **사용자 지정 HTML 태그**&#x200B;를 만듭니다.
1. Munchkin 코드를 복사하여 **HTML** 필드에 붙여넣은 다음 **계속**&#x200B;을 클릭합니다.
1. **모든 페이지에서 실행**&#x200B;을 선택하고 **태그 만들기를 클릭합니다.** 참고: 트래픽이 많은 웹 사이트의 경우 **일부 페이지에서 실행**&#x200B;을 사용하여 사이트의 섹션을 제외할 수 있습니다.
1. 저장 을 클릭한 다음 Munchkin 추적 코드가 이제 웹 사이트에 로드되는지 확인합니다.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-08-05_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 양식 제출 후 Lightbox 숨기기

### 개요

Marketo에서 생성한 현재 lightbox 포함 코드는 양식을 제출할 때 사라지지 않습니다. 양식 제출 후 페이지가 다시 로드되고 양식이 다시 표시됩니다. 양식 제출 후 숨겨진 Lightbox를 만들려면 아래 단계를 따르십시오.

### 방법 안내서

1. Marketo에서 양식을 만든 후 포함 코드를 생성합니다. 이렇게 하려면 폼 액션을 클릭한 다음 코드 유형으로 Lightbox를 클릭합니다. 다음 단계에서 편집할 수 있도록 이 코드를 복사하여 텍스트 편집기에 붙여넣습니다.
1. 포함 코드의 &quot;(form)&quot; 뒤에 있는 모든 코드를 아래 코드로 바꿉니다.

```javascript
{
var lightbox = MktoForms2.lightbox(form).show();
form.onSuccess(function(){
lightbox.hide();
return false;
});
});
</script>
```

2단계 이후에는 완성된 버전이 아래 코드와 같아야 합니다. 이제 코드를 웹 사이트에서 사용할 준비가 되었습니다.

```javascript
<script src="http://app-sj04.marketo.com/js/forms2/js/forms2.js"></script>
<form id="mktoForm_0000"></form>
<script>MktoForms2.loadForm("http://app-sj04.marketo.com", "AAA-BBB-CCC", 0000, function (form){
var lightbox = MktoForms2.lightbox(form).show();
form.onSuccess(function(){
lightbox.hide();
return false;
});
});
</script>
```

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-08-21_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo REST API에 대한 빠른 시작 안내서

이 안내서에서는 10분 내에 Marketo REST API를 처음 호출하는 방법을 보여 줍니다. [ID별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) REST API 끝점을 사용하여 단일 리드를 검색하는 방법을 보여 줍니다. 이렇게 하려면 인증 프로세스를 통해 액세스 토큰을 생성합니다. 이 액세스 토큰은 [ID로 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)에 대한 HTTP GET 요청을 만드는 데 사용됩니다. 그런 다음 JSON 형식의 리드 정보를 반환하는 요청을 만드는 코드를 제공합니다.

### 인증 토큰을 생성하는 방법

>[!NOTE]
> 2025년 6월부터 인증 토큰은 더 이상 지원되지 않습니다. Authentication 헤더를 사용해야 합니다.
>

Marketo의 사용자 정의 서비스를 사용하면 애플리케이션이 액세스할 데이터를 설명하고 정의할 수 있습니다. 사용자 정의 서비스를 만들고 단일 API 전용 사용자와 해당 서비스를 연결하려면 Marketo 관리자로 로그인해야 합니다.

1. Marketo 애플리케이션의 관리 영역으로 이동합니다.
1. 왼쪽 패널의 사용자 및 역할 노드를 클릭합니다.
1. 새 역할을 만듭니다. API 액세스를 클릭하여 역할 권한 목록을 표시합니다. 이제 아래로 스크롤하여 필요한 권한만 선택합니다. 이 경우 읽기 전용 리드 권한을 선택하기만 하면 됩니다.
1. 다음 단계는 API 전용 사용자를 만들고 이전 단계에서 만든 API 역할과 연결하는 것입니다. 이렇게 하려면 사용자 생성 시 API 전용 사용자 확인란을 선택하면 됩니다.
1. 클라이언트 애플리케이션을 고유하게 식별하려면 사용자 정의 서비스가 필요합니다. 사용자 지정 응용 프로그램을 만들려면 관리 > LaunchPoint 화면으로 이동하여 새 서비스를 만드십시오.
1. 표시 이름을 입력하고 &quot;사용자 정의&quot; 서비스 유형을 선택하고 설명을 입력한 다음 1단계에서 만든 사용자 이메일 주소를 입력합니다. 이 사용자 정의 REST API 서비스의 회사 또는 목적을 나타내는 수사적 표시 이름을 사용하는 것이 좋습니다.
1. 그리드에서 &quot;세부 정보 보기&quot; 링크를 클릭하여 클라이언트 ID 및 클라이언트 암호를 가져옵니다. 클라이언트 애플리케이션은 클라이언트 ID와 클라이언트 암호를 사용하여 액세스 토큰을 생성할 수 있습니다.
1. 인증 토큰을 복사하여 텍스트 편집기에 붙여넣습니다. 인증 토큰은 아래 예와 유사합니다.

`cdf01657-110d-4155-99a7-f986b2ff13a0:int`

### 끝점 URL을 확인하는 방법

Marketo API에 요청할 때 끝점 URL에 Marketo 인스턴스를 지정해야 합니다. Marketo REST API에 대한 모든 비벌크 API 요청은 아래 형식을 따릅니다.

`<REST API Endpoint URL>/rest/`

REST API 끝점 URL은 Marketo 관리 > 웹 서비스 패널에서 찾을 수 있습니다. Marketo 엔드포인트 URL 구조는 아래 예와 유사해야 합니다.

`https://100-AEK-913.mktorest.com/rest/v1/lead/{id}.json`

**참고: 대량 API URL에는 &#39;/rest/&#39; 접두사가 붙지 않습니다. Bulk API의 경우 다음과 같이 호스트만 사용하고 적절한 경로를 추가해야 합니다.**

`https://100-AEK-913.mktorest.com/bulk/v1/leads/export/create.json`

### 인증 토큰을 사용하여 Id로 리드 가져오기 AP를 호출하는 방법

이전 섹션에서는 인증 토큰을 생성하고 엔드포인트 URL을 찾았습니다. 이제 REST API 엔드포인트에 대해 [Get Lead by Id](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)&#x200B;(이)라는 요청을 수행합니다. Marketo REST API에 대한 요청을 수행하는 가장 쉬운 방법은 웹 브라우저 주소 표시줄에 URL을 붙여넣는 것입니다. 아래 형식을 따르십시오.

`https://<REST API Endpoint URL for your Marketo instance>/rest/v1/<API that you are calling>?access_token=<access_token>`

### 예

`https://100-AEK-913.mktorest.com/rest/v1/lead/318581.json?access_token=cdf01657-110d-4155-99a7-f986b2ff13a0:int`

호출이 성공하면 아래 형식으로 JSON을 반환합니다.

```json
{
    "requestId": "d82a#14e26755a9c",
    "result": [
        {
            "id": 318581,
            "updatedAt": "2015-06-11T23:15:23Z",
            "lastName": "Doe",
            "email": "<jdoe@marketo.com>",
            "createdAt": "2015-03-17T00:18:40Z",
            "firstName": "John"
        }
    ],
    "success": true
}
```

Marketo REST API에 대해 자세히 알아보려면 [좋은 시작 위치](https://developer.adobe.com/marketo-apis/)입니다.

_David_&#x200B;이(가) _2015-09-04_&#x200B;에 게시함

## Marketo 추적 쿠키를 삭제하는 방법

질문: &quot;영업팀이 구두로 이메일 메시지에서 제거해달라고 요청한 개인에 대한 구독을 취소할 수 있는 양식을 웹 사이트에 설정했습니다. 하지만 우리가 발견하는 것은 그들이 이메일에 입력하고 그 이메일 주소로 요리되고 우리 웹사이트에서 그들의 활동에 대한 경고를 받기 시작한다는 것을 제출하는 것입니다. 우리가 가지고 있는 양식은 현재 임베드된 양식이다. 임베드된 양식에서 쿡 추적을 비활성화하는 방법을 알고 있는 사람이 있다면, 나는 Marketo 랜딩 페이지로 그것을 하는 방법을 이해한다.&quot; 우린 할 수 있어 이를 구현하려면 쿠키 만료 속도를 높입니다. 양식에 의해 쿠키가 만들어지면 즉시 만료되도록 할 수 있습니다. 쿠키가 만료되었으므로 브라우저가 쿠키를 자동으로 삭제합니다. 이 프로세스를 시작하려면 네이티브 양식 기능을 사용하여 `deleteCookie` 함수에서 호출합니다.

_Travis Kaufman_&#x200B;이(가) _2014-08-26_&#x200B;에 게시함

## 워드 프레스와 Marketo 랜딩 페이지 통합

웹 사이트가 Wordpress를 사용하여 작성되었으며 Marketo 랜딩 페이지를 페이지 중 하나에 포함한다고 가정해 보겠습니다. 이는 iframe을 사용하여 가능합니다. iframe을 사용하면 다른 페이지 내에 페이지를 포함할 수 있습니다. 이 게시물에서, 당신은 워드 프레스 페이지에 Marketo 랜딩 페이지를 포함 하는 방법을 보여줍니다. **워드 프레스 플러그인을 선택** 워드 프레스의 수는 다음과 같은 워드 프레스 플러그인이 있습니다 : `http://wordpress.org/plugins/iframe/` 여기 이 접근 방법을 사용하는 데 대한 몇 가지 프로와 콘이 있습니다: `http://www.elixiter.com/marketo-landing-page-and-form-hosting-options/` 좋은 게시물 Murtza! 콜비, iframe에서는 양식을 제출한 후 PDF으로 리디렉션되는 부분이 유지됩니다. 우리는 오랫동안 사이트에서 iframe을 사용했습니다. 훌륭한 포스트 머트자! 콜비, iframe에서는 양식을 제출한 후 PDF으로 리디렉션되는 부분이 유지됩니다. 우리는 오랫동안 사이트에서 iframe을 사용했습니다. 주 URL에서 iframe으로 URL 매개 변수를 전달하려면 코딩을 수행해야 합니다. 또한 Google Analytics이 제대로 설정되어 있는지 확인하십시오. iframe을 사용하여 페이지를 방문할 때마다 페이지 보기가 두 번 카운트되지 않도록 하려는 경우

_1970-01-01_&#x200B;에 _Murta_&#x200B;에 게시됨

## Marketo 랜딩 페이지와 최적 통합

[최적화](https://www.optimizely.com/)은(는) 사이트에서 A/B 테스트, 다중 페이지 및 다변량 테스트를 수행할 수 있는 기능을 제공합니다. Marketo 랜딩 페이지에서 최적 을 사용할 수 있습니다. 방법은 다음과 같습니다.

1. Optimizely 코드 조각을 찾아 복사합니다.** Optimizly로 이동하여 프로젝트 코드 링크를 클릭합니다. 팝업에 표시되는 코드 행을 복사합니다.
1. Marketo에 로그인하고 랜딩 페이지 템플릿을 선택합니다. 그런 다음 &quot;초안 편집&quot;을 클릭합니다.**
1. 랜딩 페이지 작업 을 클릭합니다. 그런 다음 페이지 메타 태그 편집 을 클릭합니다**
1. 최적화 코드 조각을 사용자 지정 HEAD HTML 섹션에 붙여 넣은 다음 저장을 클릭합니다.
1. 랜딩 페이지를 테스트하여 최적 스니펫이 작동하는지 확인합니다.

_2014-09-18_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo REST API를 통해 전체 이름으로 검색

**질문:** 잠재 고객의 전체 이름으로 Marketo API를 사용하여 잠재 고객을 쿼리할 수 있는 방법이 있습니까?
**답변:** 직접 사용할 수 없습니다. 그러나 아래에 설명된 해결 방법을 사용하면 이 작업을 수행할 수 있습니다.

1. Marketo에서 &quot;Fullname&quot;이라는 사용자 지정 필드를 만듭니다.
1. [getMultipleLeads](/help/soap-api/getmultipleleads.md) SOAP API 또는 [필터 유형별 여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET)를 사용하여 리드 데이터베이스를 쿼리합니다. REST 또는 SOAP API에 대한 요청에 이름과 성을 속성으로 포함하십시오.
1. 리드 데이터베이스를 쿼리한 후 각 리드에 대해 &quot;First Name&quot;과 &quot;Last Name&quot;을 연결하고 이 데이터를 &quot;Fullname&quot; 열에 저장합니다. 1. [syncMultipleLeads](/help/soap-api/syncmultipleleads.md) SOAP API를 사용하여 이 데이터를 &quot;Fullname&quot; 사용자 지정 필드에 푸시합니다. 또는 [리드 가져오기](/help/rest-api/leads.md) API를 사용하거나 Marketo UI를 사용하여 CSV 또는 XLS를 가져올 수 있습니다.
1. 이제 [필터 유형별 다중 리드 가져오기 API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 사용하여 전체 이름별로 쿼리하여 이 사용자 지정 필드를 검색할 수 있습니다. 필터 유형별 Get Multiple Leads by Filter Type REST API 호출로 &quot;Fullname&quot;을 &quot;filterType&quot;으로 지정하고 &quot;filterValue&quot;를 &quot;Joe Johnson&quot;으로 지정합니다.

_2014-09-09_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo 추적 쿠키 삭제

이 방법은 원하는 효과가 쿠키를 완전히 제거하는 경우에만 사용해야 합니다.

이 코드 샘플은 Marketo 양식 제출 후 사용자의 브라우저에서 Marketo 추적 쿠키를 삭제하는 데 사용할 수 있습니다. 사용자가 양식을 제출한 후 `deleteMarketoCookie` 메서드를 호출하면 작동합니다. 이 메서드는 만료 날짜를 과거의 날짜로 설정하여 쿠키를 만료합니다. 그러면 이 쿠키가 만료되었기 때문에 브라우저의 기본 동작이 삭제됩니다.

_2014-09-09_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 양식 작성에서 무료 이메일 도메인 제한

사이트 방문자가 Gmail 또는 Yahoo와 같은 무료 이메일 도메인을 사용하는 양식을 제출하는 것을 제한한다고 가정해 보겠습니다. 이렇게 하려면 Marketo 양식이 있는 페이지의 소스 코드에 아래 스크립트를 포함하십시오. 사용자가 비업무용 이메일(Gmail, Hotmail 등)을 입력했는지 확인하고, 입력한 경우 Marketo 양식을 제출하지 못하도록 합니다. 제한할 도메인을 포함하도록 9줄을 수정하여 차단된 이메일 도메인 목록을 확장할 수 있습니다.

_2014-09-09_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## API를 통해 액세스할 수 없는 필드 디버깅

이 필드 <https://nation.marketo.com/>(으)로 이동하는 경우 SOAP API를 사용하여 AnnualRevenue 필드를 업데이트하려고 하면 응답이 레코드가 업데이트되었다고 표시하지만 AnnualRevenue 필드는 변경 사항을 유지하지 않습니다. 리드 데이터베이스를 사용하여 필드를 수동으로 업데이트하려고 하면 이 필드에 대한 변경 사항도 지속되지 않습니다. 필드가 Admin에서 차단되었는지 확인합니다. 경우에 따라 발생할 수 있는 다른 하나는 SFDC에서 동기화된 계정 필드일 수 있다는 것입니다. SFDC은 대부분의 경우 이러한 필드의 기록 시스템이므로 기본적으로 이러한 필드의 변경 사항을 차단합니다. 1) 생성일 2) Marketo SFDC ID 3) Marketo 고유 코드 4) SFDC 유형 5) 업데이트일 6) 긴급도 7) 우선 순위 8) 판매 생성일

_1970-01-01_&#x200B;에 _Murta_&#x200B;에 게시됨

## Marketo 랜딩 페이지에 사용자 지정 코드 추가

Marketo 랜딩 페이지에 Google Analytics과 같은 서드파티 추적 스크립트를 추가한다고 가정해 보겠습니다. Marketo UI를 통해 가능합니다. 보다 일반적으로 아래 지침에 따라 모든 사용자 지정 코드(HTML, CSS, JavaScript)를 Marketo 랜딩에 추가할 수 있습니다.

1. 랜딩 페이지를 선택하고 초안 편집 을 클릭합니다.
1. HTML 요소에서 를 드래그합니다.
1. 사용자 지정 코드를 입력하고 [저장]을 클릭합니다.

_2014-09-10_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 서버측 양식 게시물

`https://community.marketo.com/MarketoResource?id=kA650000000GsXXCA0`

_2014-09-11_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Forms 2.0 제출에서 Marketo 추적 쿠키 지우기

### 개요

Forms 1.0에는 Munchkin 추적 쿠키 값이 DOM의 필드로 포함되어 있습니다. 이는 다른 모든 입력과 함께 제출되었습니다. [Forms 2.0](/help/javascript-api/forms-api-reference.md)에서는 이 필드를 생략하고 양식 로드 대신 제출 시 값을 동적으로 채웁니다. 일반적으로 사용할 수 있는 것이지만, 사용 사례 클래스를 만듭니다. 이 클래스를 사용하려면 의도하지 않은 추적 및 미리 채우기를 방지하기 위해 추적 쿠키를 지워야 합니다. 예를 들어 Marketo 고객이 동일한 장치에서 동일한 양식을 사용하고 여러 사람으로부터 연락처 정보를 받는 박람회 등에서 이러한 일이 발생할 수 있습니다. 아래 스니펫을 사용하면 사용자의 브라우저에서 쿠키 자체를 삭제하지 않고도 양식 제출 시 쿠키 값을 지울 수 있습니다.

### 코드 샘플

이 코드 조각은 페이지에 단일 양식 로드를 예상합니다. 양식이 여러 개인 경우 [loadForm 또는 getForm 메서드](/help/javascript-api/forms-api-reference.md)를 사용하여 콜백을 구현해야 합니다.

```javascript
<script>
//add a callback to the first ready form on the page
MktoForms2.whenReady( function(form){
 //add the tracking field to be submitted
        form.addHiddenFields({"_mkt_trk":""});
        //clear the value during the onSubmit event to prevent tracking association
 form.onSubmit( function(form){
  form.vals({"_mkt_trk":""});
 })
})
</script>
```

_케니_&#x200B;이(가) _2014-09-11_&#x200B;에 게시함

## 2014년 9월 릴리스 업데이트

### REST API 업데이트

[여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) API에 새로운 선택적 필드 값을 추가했습니다. 이 API는 리드 레코드와 연결된 Munchkin 쿠키 값을 반환합니다. 요청에 &quot;?fields=cookies&quot;를 추가하기만 하면 됩니다.

_2014-09-16_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## RTP API의 위치 데이터를 Marketo 양식 채우기에 추가합니다.

**이 블로그 게시물에 설명된 사용 사례를 구현하려면 활성 RTP 및 MLM 구독이 필요합니다.**
[RTP JavaScript API](/help/javascript-api/web-personalization.md) 및 [Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md)을 사용하면 RTP에서 유추된 위치 데이터를 가져와서 양식 작성을 통해 Marketo에 푸시할 수 있습니다. 이를 통해 가장 최근의 양식 활동 중에 IP 주소를 기반으로 하여 유추한 사용자의 위치를 볼 수 있습니다. 시작하려면 Marketo에서 세 개의 사용자 지정 문자열 필드를 만들어야 합니다. Marketo과 기본 통합이 있는 경우 CRM을 통하거나 Marketo의 관리 섹션에 있는 필드 관리 메뉴에서 이 작업을 수행할 수 있습니다. 이러한 필드의 이름을 &#39;가장 최근 국가&#39;, &#39;가장 최근 주&#39; 및 &#39;가장 최근 도시&#39;로 지정하는 것이 좋습니다. 이 블로그는 명명 규칙을 사용하여 계속합니다. 이러한 필드의 API 이름은 &#39;mostRecentCountry&#39;, &#39;mostRecentState&#39; 및 &#39;mostRecentCity&#39;입니다. 위치 데이터를 검색하려면 [RTP 메서드를 사용하여 방문자의 위치 데이터를 가져온](/help/javascript-api/web-personalization.md)다음, Marketo Forms 2.0에서 [addHiddenFields 및 vals 메서드](/help/javascript-api/forms-api-reference.md)를 사용하여 해당 데이터를 양식으로 전달합니다. 페이지에서 RTP JS 태그와 Marketo 양식을 추가합니다. 그런 다음 아래 스크립트를 포함하십시오. 위에서 설명한 것과 다른 이름 지정 규칙을 사용하는 경우 예제 코드에서 대상 양식 필드의 이름을 변경해야 합니다.

```javascript
<script>
//modify the form and grab the user
MktoForms2.whenReady( function(form) {
        //add the hidden fields to the form
 form.addHiddenFields({
  "mostRecentCountry":"",
  "mostRecentState":"",
  "mostRecentCity":""});
 //Grab the visitor data, a JS object with it is passed in the callback function of the third argument
 rtp('get','visitor',function(visitor){
  //add the desired info from the visitor object to the form fields
  form.vals({
   "mostRecentCountry":visitor.results.location.country,
   "mostRecentCity":visitor.results.location.city,
   "mostRecentState":visitor.results.location.state});
  }
  );
 });
</script>
```

_케니_&#x200B;이(가) _2014-09-17_&#x200B;에 게시함

## Marketo 랜딩 페이지의 블록 크롤링 및 검색 인덱싱

Google과 같은 검색 엔진이 Marketo 랜딩 페이지를 크롤링하여 결과에 표시하는 것을 차단하려고 한다고 가정해 보겠습니다. 방법은 다음과 같습니다.

1. Marketo에 로그인한 다음 랜딩 페이지를 선택합니다. 그런 다음 &quot;초안 편집&quot;을 클릭합니다.
1. 랜딩 페이지 작업 을 클릭합니다. 그런 다음 페이지 메타 태그 편집 을 클릭합니다
1. Robots 필드를 No Index, No Follow로 변경합니다. 그런 다음 [저장]을 클릭합니다.

_2014-09-19_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo REST 및 SOAP API FAQ

**업데이트됨: 2016년 3월** Marketo [REST](/help/rest-api/rest-api.md) 및 [SOAP](/help/soap-api/soap-api.md) API에 대해 가장 자주 묻는 질문에 대한 답변입니다. **Q: Marketo REST와 SOAP API의 주요 차이점은 무엇입니까?** A: REST 및 SOAP API를 통해 특정 데이터를 푸시/가져오는 기능은 대부분 겹치지만 REST 또는 SOAP API에만 있는 특정 기능이 있습니다. 성능 측면에서 REST API는 SOAP API보다 [처리량](https://en.wikipedia.org/wiki/Throughput)이(가) 더 좋습니다. 인증 모델 측면에서 REST API는 만료되는 토큰을 사용하는 인증 모델을 가지고 있다. REST API는 또한 Marketo [자산](https://developer.adobe.com/marketo-apis/api/asset/)에 대한 액세스를 제공합니다.   **Q: SOAP API에서 사용할 수 없는 REST API에서 사용할 수 있는 기능은 무엇입니까?** A: [목록 API 목록](/help/rest-api/list-of-standard-fields.md), [목록 API에서 리드 제거](/help/rest-api/lead-database.md), [사용 API](/help/rest-api/rest-api.md) 및 [오류 API](/help/rest-api/rest-api.md)는 REST API에서만 사용할 수 있습니다. **Q: SOAP API에 사용할 수 있는 API의 수를 늘릴 계획이 있습니까?** A: 아니요. **Q: REST API에 사용할 수 있는 API의 수를 늘릴 계획이 있습니까?** A: 예. REST는 현재 Marketo의 API 개발에 있어 가장 우선적으로 중점을 두고 있습니다.

_2014-09-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 서버측 양식 게시물

**참고: 이 API는 공개되지 않고 지원되지 않으며 지원되지 않으며 해당 동작이 언제든지 변경될 수 있습니다.** 웹 사이트에서 사용자의 양식을 사용하는 경우에도 서버측 게시물을 사용하여 이 데이터를 Marketo으로 보낼 수 있습니다. 이 접근 방식의 이점은 기존 양식 및 애플리케이션 논리를 유지할 수 있지만 Marketo에 대한 실제 양식 게시물을 계속 사용할 수 있다는 것입니다. 이렇게 하면 Marketo 사용자에게 &quot;양식 작성&quot; 이벤트를 제공하는데, 이 이벤트는 자동화된 프로세스를 트리거하거나 세분화하는 데 사용할 수 있습니다. **참고: 하나의 IP 주소에서 분당 30개의 서버측 양식 게시물 속도가 제한됩니다.** 각 스크립팅 또는 프로그래밍 언어에는 서버측 양식 제출을 위한 다양한 옵션이 있으며 Post 호출을 수행하는 데 사용할 수 있는 다양한 개체/메서드가 있을 수 있습니다. 예를 들어, PHP에서는 많은 사람들이 cURL 라이브러리를 사용합니다. 모든 경우 이름-값 쌍을 지정된 URL에 게시합니다. 이름은 Marketo 필드의 API 이름과 동일해야 합니다. 또한 양식 제출을 올바르게 캡처하기 위해 포함해야 하는 시스템 필드가 두 개 있습니다.

1. 양식을 만듭니다. 첫 번째 단계는 Marketo에서 양식을 만들거나 제출하려는 기존 양식을 사용하는 것입니다. 양식 이름은 설명적이어야 하지만 실제로 양식 필드가 필요하지는 않습니다. 새 양식을 만드는 경우 이름을 입력하고 &quot;양식 편집기 열기&quot; 상자를 선택 취소하면 됩니다.
1. 양식 ID를 찾습니다. Marketo UI에서 양식을 선택하고 URL을 확인합니다. `https://app-x.marketo.com/#FO8B2ZN12` 형식이어야 합니다. # 기호 뒤에서 &quot;FO&quot; 바로 다음에 오는 숫자를 확인하여 양식 ID를 찾으십시오. 이 경우 양식 ID는 8입니다. 경우에 따라 첫 번째 양식에 1001이라는 번호가 매겨져 있을 수 있습니다. 양식 ID는 변수이므로 다른 양식 제출을 트리거할 수 있습니다.
1. Marketo 계정 ID를 가져옵니다. 관리 > Munchkin 로 이동하여 Munchkin 계정 ID가 000-AAA-000 형식인 를 복사합니다. 이 ID가 있어야 양식이 올바른 Marketo 인스턴스에 제출됩니다.
1. 게시물 URL을 결정합니다. Marketo 사용자 인터페이스를 사용할 때는 위치 표시줄의 도메인(일반적으로 `<http://app-x.marketo.com/>` 형식)을 확인합니다. 슬래시 뒤에 있는 모든 항목을 삭제한 다음 &quot;index.php/leadCapture/save&quot;를 추가하여 전체 양식 POST URL을 가져옵니다. 참고 1: 대소문자를 구분합니다. 참고 2: Marketo 샌드박스는 프로덕션 Marketo 시스템과 다른 도메인을 가질 수 있습니다. 예 URL은 `http://app-x.marketo.com/index.php/leadCapture/save`입니다. HTTP 대신 HTTPS를 사용할 수도 있습니다(보안 예외를 제공하므로 CNAME를 사용하지 마십시오).
1. 양식 필드 이름 찾기** 관리자 > 필드 관리로 이동하고 &quot;필드 이름 내보내기&quot; 버튼을 클릭하여 API 필드 이름이 포함된 스프레드시트를 다운로드합니다. API 이름을 이름-값 쌍의 이름으로 사용합니다.
1. 게시할 필드를 결정합니다. 양식 제출에 모든 Marketo 리드 필드를 포함할 수 있습니다. 필드 이름은 대소문자를 구분합니다. 제출하려는 필드 외에도 두 개의 필수 필드와 두 개의 권장 필드가 있습니다. (1) `munchkinId` - 이 필드는 Munchkin 계정 ID에 사용됩니다. (2) `formid` - 이 필드는 Marketo에서 제출된 양식을 나타냅니다. 양식의 권장 필드: (1) 이메일 - 이 필드는 중복 제거를 위한 기본 키로 사용됩니다. Marketo이 Marketo 데이터베이스에서 일치하는 이메일 주소를 찾으면 기존 레코드를 업데이트하고, 그렇지 않으면 새 레코드를 만듭니다. 일치하는 항목이 여러 개일 경우 가장 최근에 업데이트된 레코드(2) `_mkt_trk`이(가) 업데이트됩니다. 이 필드에는 쿠키 정보가 포함되어 있으므로 개인의 웹 페이지 방문 횟수를 추적할 수 있습니다. 양식 페이지에 Munchkin이 있는 경우 Munchkin에서 이 숨겨진 양식 필드에 값을 자동으로 입력합니다. 그렇지 않은 경우 쿠키에서 동일한 이름으로 읽고 이 필드의 Marketo에 전달합니다. 참고: Marketo 양식에 대한 게시물 본문은 URL로 인코딩되어야 합니다.
1. 응답을 참조하십시오** 양식 게시물에 대한 응답은 HTTP 302 리디렉션 코드가 됩니다. 일부 시스템에서는 오류가 표시됩니다. 단, 이 경우 잠재 고객이 정상적으로 생성 또는 업데이트되었음을 의미합니다. 오류가 발생하면 4xx 또는 5xx 오류 코드를 받습니다.

다음은 구독 취소 시나리오에 이 기술을 사용하는 방법에 대한 [게시물](https://nation.marketo.com:443/t5/product-blogs/how-to-build-an-external-subscription-center/ba-p/242185)입니다. [Justin Cooperman, Sr. Product Manager]

_2014-11-07_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 특정 일자 범위에서 업데이트된 리드 찾기

[Marketo API](/help/soap-api/soap-api.md)를 통해 특정 날짜에 업데이트된 잠재 고객을 찾고 싶다고 가정해 보겠습니다. 이는 [getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md)에서 가능합니다. 이 메서드는 요청한 날짜 범위에 대해 Marketo에서 데이터 값 변경 또는 새 활동이 있는 모든 리드를 반환합니다. `leadSelector`에 대해 `LastUpdateAtSelector`을(를) 지정합니다. 그런 다음 날짜 범위를 `oldestUpdatedAt` 및 `latestUpdatedAt` 시간 범위로 정의합니다. 2014년 6월 6일 오전 12시 PST와 2011년 6월 7일 오전 12시 PST 사이에 업데이트된 잠재 고객을 찾는 방법을 보여 주는 아래 샘플 요청 XML을 참조하십시오. 참고: 날짜 범위는 30일을 초과할 수 없습니다.

**날짜별로 업데이트된 리드를 찾기 위한 샘플 요청 XML**

```xml
<soapenv:Envelope xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
<soapenv:Header>
<mkt:AuthenticationHeader>
<mktowsUserId>REPLACE</mktowsUserId>
<requestSignature>REPLACE</requestSignature>
<requestTimestamp>2014-10-23T12:19:51-07:00</requestTimestamp>
</mkt:AuthenticationHeader>
</soapenv:Header>
<soapenv:Body>
<mkt:paramsGetMultipleLeads>
<leadSelector xsi:type="mkt:LastUpdateAtSelector">
<oldestUpdatedAt>2014-06-06T00:00:00-08:00</oldestUpdatedAt>
<latestUpdatedAt>2014-06-07T00:00:00-08:00</latestUpdatedAt>
</leadSelector>
</mkt:paramsGetMultipleLeads>
</soapenv:Body>
</soapenv:Envelope>
```

_2014-09-24_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 이메일에 동적 콘텐츠 추가

일별 이메일을 발송하고 이메일 템플릿에 해당 날짜의 날짜를 자동으로 포함한다고 가정해 보겠습니다. 이렇게 하려면 Marketo에서 토큰 및 이메일 스크립팅을 사용합니다.

1. 토큰을 만듭니다.** 토큰을 사용할 프로그램으로 이동합니다. 내 토큰 을 클릭합니다.
1. 이메일 스크립트를 두 번 클릭합니다. 그런 다음 이 토큰의 이름을 지정합니다. 그런 다음 [편집]을 클릭합니다.
1. 아래의 이메일 스크립트를 이 창에 붙여넣습니다. 그런 다음 [저장]을 클릭합니다.

## Velocity의 캘린더 개체에 액세스

`set($x = $date.calendar)`

## 날짜 형식 지정

`set($current_date = $date.format('dd-MM-yyyy', $x.getTime()))`

## 오늘 일자를 반환합니다.

`$current_date`

1. 이메일 템플릿에서 토큰을 참조합니다.** 토큰의 이름을 확인합니다. 이메일 초안으로 이동합니다. 토큰을 포함합니다.  이메일을 보내면 토큰의 값이 채워집니다. 자세한 내용은 [전자 메일 스크립팅 개발자 설명서](https://experienceleague.adobe.com/ko/docs/marketo-developer/marketo/email-scripting)를 참조하세요.

_2014-11-22_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Bash 보안 자문

Marketo은 [Shellshock(CVE-2014-6271)](https://nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-6271)이라고도 하는 Bash 취약성에 대한 철저한 조사를 수행했으며 이러한 공격에 취약하지 않다고 결론을 내렸습니다. 또한 [CERT 권장 사항](https://www.cisa.gov/news-events/alerts/2014/09/25/gnu-bourne-again-shell-bash-shellshock-vulnerability-cve-2014-6271)을 준수하도록 소프트웨어를 최신 버전으로 업데이트하여 예방 조치를 취했습니다.

_2014-09-26_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## SOAP API 자격 증명을 업데이트하는 방법

[SOAP API](/help/soap-api/soap-api.md) 자격 증명을 정기적으로 업데이트하는 것이 좋습니다. 현재 Marketo API를 통해 프로그래밍 방식으로 이 작업을 수행할 방법은 없습니다. 아래 지침은 Marketo UI를 통해 SOAP API 자격 증명을 업데이트하는 방법을 보여줍니다.

1. 관리 섹션으로 이동하고 웹 서비스를 클릭합니다.
1. 10자 이상의 암호화 키를 설정한 다음 변경 내용 저장을 클릭합니다.

_2014-09-29_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo 데이터베이스를 정리하는 방법

**참고: 게스트 블로그 게시물입니다. Josh Hill 은 마케팅 자동화 에이전시인 Perkuto 의 Marketo Practice Lead 입니다. Josh는 마케팅, 판매, 기술의 교차점에서 수익 창출 시스템을 제공합니다. [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/)에서 마케팅 자동화 및 수요 창출에 대해 작성합니다.** Marketo 데이터베이스를 깔끔하게 유지하는 것은 이 강력한 시스템을 관리하는 데 중요한 부분입니다. Marketo 데이터가 더럽거나 CRM 데이터가 더러우면 캠페인이 잘못된 사람에게 갔거나 보고서가 &quot;방향&quot;인 이유를 설명할수록 마케팅 관리자로서의 작업이 훨씬 어려워집니다. [2011년 Gartner 연구 결과](https://www.data.com/export/sites/data/common/assets/pdf/DS_Gartner.pdf)의 낮은 데이터 품질이 노동 생산성을 20% 낮췄다고 지적했습니다. 이는 데이터를 수정해야 했기 때문에 낭비되는 시간의 20%(주 8시간 또는 주 1일)입니다. 하지만 이러한 손실은 타겟팅이 잘못되어 손실된 매출과 비교하여 적습니다. 데이터를 깔끔하게 유지하는 데 투자해야 하는 5가지 주요 이유는 다음과 같습니다. - 리드 및 클라이언트의 세분화를 개선하여 적시에 적절한 사람에게 메시지를 집중할 수 있습니다. 그 20% 할인 쿠폰은 당신의 최고의 고객이 아닌 새로운 잠재 고객에게만 갈 것입니다, 맞죠? - 이메일을 중복 보내지 마십시오. 모든 예방 조치에도 불구하고 일반적으로 중복 레코드가 병합되지 않으므로 동일한 잠재 고객에게 여러 개의 이메일을 보낼 수 있습니다. - 상사에게 정확한 보고. CMO는 매출 표에 좌석을 가지고 있으므로 정확하고 일관되고 반복 가능한 보고서가 있어야 합니다. 그렇지 않으면 더 이상 매출 마케터가 될 수 없습니다. - 영업 협상 중에 잘못된 마케팅 자료를 주요 잠재 고객에게 이메일로 보내면 보류 중인 딜에 타격을 줄 수 있습니다.

데이터베이스에서 라이프사이클 단계에서 이러한 세부 정보를 제공하지 않는 경우 거래가 한두 개가 될 수 있습니다. - 불량하거나 오래된 리드를 제거하여 가격 임계값 이하를 유지합니다. 잘못된 데이터의 비용에 대해서는 많은 내용이 작성되었다. 가장 직접적인 우려는 너무 많은 불량, 중복 또는 오래된 리드가 Marketo 또는 Salesforce 가격 책정 계층을 압박하고 있다는 것입니다. 이로 인해 매년 수천 건의 요금이 발생할 수 있습니다. 그럼 어떻게 데이터베이스를 깔끔하게 유지하나요? 이러한 데이터 청렴의 원칙을 따를 수 있지만, Marketo 내부에서는 어떻게 해야 합니까? 시스템에 대해 몇 가지 가정을 합니다. - 표준 Marketo 시스템이 있습니다. - 일반적인 잠재 고객 연락처 계정 Salesforce 설정이 있습니다. - 시스템 간에 모든 레코드를 동기화하고 있습니다. - 의도적인 중복을 사용하고 있지 않습니다.

해결할 수 있는 올바른 리드 찾기** 먼저 잠재적인 문제가 있는 리드를 찾아보겠습니다. 각각의 고객들과 함께 일련의 스마트 목록을 살펴보고 데이터베이스의 상태를 파악합니다. 월별로 같은 일을 하는 것이 좋습니다. 스마트 목록이 작동하면 한 달에 15분 이상 걸리지 않습니다. 이는 작업 및 Marketo의 ROI를 입증할 수 있는 좋은 방법입니다. 데이터베이스에 미치는 총 영향을 파악하는 테이블을 만듭니다. 아래 예에는 내가 찾는 기준이 포함되어 있으므로 귀하의 비즈니스에 중요한 다른 필드를 포함해야 합니다. Marketo 전용, SFDC 리드 및 SFDC 연락처별로 각 그룹을 분류합니다.

자동화를 사용하여 데이터 값 수정: 일반적인 철자 오류 또는 누락된 데이터를 수정하기 위한 자동화 규칙 사용은 수십 년 전으로 거슬러 올라갑니다. 1960년대에는 DM을 보낼 때 데이터 품질이 떨어지면 수천 달러가 낭비될 수 있습니다. 오늘날 데이터 품질 실수는 잘못된 메일 조각보다 더 빨리 평판을 망치고 있습니다. 이메일 신뢰도, 언어 선택, 고객 경험은 중요하며 실수는 몇 분 안에 공개적으로 입소문이 날 수 있기 때문에 더욱 중요합니다. 자동화된 데이터 정리를 통해 회사의 평판을 보호할 수 있습니다. 이러한 데이터 관리 흐름은 Marketo에서 가장 먼저 설정하는 항목 중 하나입니다. 대부분의 회사에서는 다음과 유사한 플로우를 설정합니다. - 국가 정정자(이 설정이 필요하지 않도록 원칙 1을 따랐어야 하지만) - 상태 정정자 또는 매퍼 - 국가 및 유추 상태가 있는 경우 종종 유용합니다. - 직원 범위에 대한 직원 수. - Source을 좋은 리드 Source으로 이끌 수 없음 - 이메일이 변경된 경우 유효하지 않은 이메일을 보내는 것이 좋습니다. - 이전 필드 값을 새 필드로 변환합니다(전체를 빈 필드로 변환). 예를 들어, 이 플로우는 사원 번호를 기준으로 사원 범위를 조정합니다.

데이터 추가 도구 빈 필드를 채우는 것은 데이터베이스를 더 잘 세그먼트화하는 데 중요합니다. 리드가 항상 올바른 업계, 함수 또는 양식의 제목 을 채우는 것은 아닙니다. 이전 시스템의 이전 데이터를 가지고 있는 경우가 있습니다. 이러한 데이터 부족은 더 적은 수의 사람에게 이메일을 보내야 하거나 아마도 잘못된 사람에게 보내야 함을 의미합니다. 이 문제를 해결하려면 데이터 추가 도구가 필요합니다.

옵션 1: 직접 작성하십시오. 데이터를 보간하여 빈 필드를 채울 수 있습니다. 업계 이름이나 연간 매출과 연간 매출 범위 대신 SIC 코드가 있을 수 있습니다. Marketo은 이러한 수정 사항을 쉽게 자동화할 수 있습니다.

옵션 2: LaunchPoint를 통해 데이터 추가/데이터 보강 공급업체 찾기 NetProspex 및 ReachForce와 같이 리드 데이터를 보강하는 데 도움이 되는 [Launchpoint에 여러 공급업체가 있습니다](https://exchange.adobe.com/apps/browse/ec?product=MRKTO). 일부는 데이터 시트를 요청하고 정리한 후 다시 보냅니다. 더 나은 옵션은 원하는 필드를 확인한 다음 올바른 데이터를 푸시하는 Marketo 또는 Salesforce의 자동화된 도구입니다. 대부분의 공급업체는 이를 수행하기 위해 [Marketo API 또는 Webhooks](/help/home.md)를 사용합니다.

옵션 3: Marketo API를 사용하여 리드 업데이트 Marketo API를 사용하여 정리해야 하는 리드를 식별한 다음 API를 통해 업데이트할 수 있습니다. [필터 유형별 여러 리드 가져오기 REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)는 특정 기준과 일치하는 Marketo의 데이터를 가져올 수 있는 좋은 시작점입니다. 리드를 업데이트하려면 [리드 REST API 만들기/업데이트](/help/rest-api/leads.md)를 참조하세요.

또는 양식 작성과 같은 특정 이벤트가 발생했음을 외부 시스템에 알리도록 [Marketo Webhook](/help/webhooks/webhooks.md)을(를) 설정할 수 있습니다. 그런 다음 값을 사용하여 응답을 다시 수행하여 리드 를 로 업데이트할 수 있습니다.

무엇을 자동화해야 합니까? 1단계에서 몇 가지 제안을 제공했습니다. 그러나 우리가 더 많은 데이터베이스를 정리하려면, 우리는 데이터 값을 수정하는 것을 넘어설 필요가 있다. - 경쟁업체 블랙리스트: 경쟁업체의 컬렉션 및 블랙리스트를 자동화하는지 확인합니다. 경쟁사-파트너가 있는 경우 해당 파트너에 적절한 표시를 하고 목록에 배치하여 무시할 수 있습니다.  - 여러 하드 바운스: 확실히 이 흐름을 자동화합니다. 30일 동안 리드 하드가 두 번 이상 튀는 경우 일시 중단됨 또는 잘못됨으로 설정합니다. 그런 다음 한 달에 한 번 문제에 오타가 있는지 아니면 다른 문제가 있는지 검토하십시오.  - 30일 후 여러 소프트 바운스: 30일 동안 마케팅 일시 중단=TRUE로 설정합니다.  - 스팸 트랩 일시 중단/삭제: 제품이 사람들이 스팸 트랩 주소를 사용한다는 의미인 경우 주의하십시오. 스팸 트랩 목록을 확인합니다. 스마트 목록입니다.

**자동화하지 않을 사항** 실수로 잘못된 레코드를 대량으로 삭제할 위험이 너무 높으므로 가망 고객 삭제를 자동화하지 마십시오. 대신, 휴지통으로 표시된 리드를 한 달에 한 번 검토하십시오. 그러나 휴지통으로 이동된 리드를 삭제하려면 30일 대기와 함께 이와 같은 흐름을 실행하십시오.

주의 사항: 자동화를 사용하면 시간을 절약하고 데이터베이스를 깔끔하게 유지할 수 있습니다. 자동화는 양날의 칼이다. 잘못 설정하면 몇 분 안에 혼란이 올 수 있기 때문이다. 이러한 프로세스를 진행할 때 주의하고 모든 사람에게 알리십시오. 일반적으로 SFDC 연락처는 활성 영업 기회, 클라이언트 또는 이전 클라이언트일 가능성이 높으므로 삭제하지 않는 것이 좋습니다. Finance 또는 Legal에서 특정 레코드를 보관하도록 요구할 수 있으며 해당 레코드에 연락처가 첨부됩니다. 대신 하드 바운스가 유효하지 않거나 더 이상 존재하지 않는 연락처에 집중합니다. 이제 Marketo 데이터베이스를 깔끔하게 유지하는 몇 가지 방법에 대해 알아보았습니다. API 또는 Webhooks를 사용하여 이러한 프로세스를 자동화할 수 있는 다른 방법이 있는지 알려 주십시오.

_2014-10-08_&#x200B;에 _Josh_&#x200B;에 의해 게시됨

## 2014년 10월 릴리스 업데이트

### 외부 페이지 미리 채우기

Marketo forms는 Marketo 랜딩 페이지 외부에서 로드할 때 기본 미리 채우기 기능을 제공하지 않습니다. 그러나 [Marketo API](/help/rest-api/rest-api.md) 및 [Forms 2.0 JavaScript API](/help/javascript-api/forms-api-reference.md/)를 사용하여 이를 계속 구현할 수 있습니다. 첫 번째 단계는 서버의 REST 호출을 통해 Marketo에서 리드 데이터를 검색하는 것입니다. 잠재 고객 ID나 서버의 다른 고유 식별자를 상호 참조할 수 있는 즉각적인 방법이 없다고 가정할 경우 [필터 유형별 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 사용하여 Munchkin 쿠키 &#39;_mkto_trk&#39;를 사용하여 Marketo 서버에서 데이터를 검색해야 합니다.
이 호출을 수행하려면 인스턴스의 인증 및 REST 끝점이 필요합니다. Marketo 인스턴스로 인증되면 `https://<host>/rest/v1/leads.json`에서 리드 API를 호출해야 합니다. 그런 다음 이 `?filterType=cookie&filterValues=`과(와) 같은 Marketo 쿠키를 필터링할 쿼리 문자열을 만들어야 합니다. 클라이언트가 서버에 보낸 &#39;_mkto_trk&#39; 키에서 특정 값을 검색해야 합니다. 참고: _mkto_trk 쿠키 값에는 앰퍼샌드가 포함되어 있으며 Marketo 끝점에서 올바르게 허용하려면 `%26`에 URL로 인코딩되어야 합니다. 기본적으로 리드 API는 `id`, `email`, `firstName` 및 `updatedAt`의 4개 필드를 반환합니다. 특정 필드 집합을 설정하려면 다음과 같이 필드 이름이 쉼표로 구분된 `fields` 쿼리 매개 변수를 포함해야 합니다. `&fields=email,firstName,lastName,company`. 궁극적으로 우리의 요구는 다음과 같이 보일 것입니다.

`https://<host>/rest/v1/leads.json?filterType=cookie&filterValues=<cookie>&fields=email,firstName,lastName,company&access_token=<token>`

이 호출을 수행하면 다음과 같은 JSON 개체가 반환됩니다.

```json
{
    "requestId":"e42b#14272d07d78",
    "success":true,
    "result":[
        {
        "id":50,
        "firstName":"Kenny",
 "lastName":"Elkington",
        "email":"<mkto@example.com>",
 "company":"Marketo Inc."
        }]
};
```

이제 리드 세부 정보가 준비되었으므로 JavaScript의 whenReady 및 vals 메서드를 사용하여 이러한 정보를 Marketo 양식으로 매핑할 수 있습니다. 먼저 Lead 결과를 페이지의 변수로 설정해야 합니다.

```javascript
<script>
//print your JSON object dynamically as the mktoLead variable
var mktoLead = {
    "requestId":"e42b#14272d07d78",
    "success":true,
    "result":[
        {
        "id":50,
        "firstName":"Kenny",
  "lastName":"Elkington",
        "email":"mkto@example.com",
  "company":"Marketo Inc."
        }]
}
</script>
```

이제 페이지에 결과가 있으므로 양식 필드에 매핑할 수 있습니다.

```javascript
<script>
MktoForms2.whenReady( function(form) {
 //set the first result as local variable
 var mktoLeadFields = mktoLead.result[0];
    //map your results from REST call to the corresponding field name on the form
 var prefillFields = {
   "Email" : mktoLeadFields.email,
   "FirstName" : mktoLeadFields.firstName,
   "LastName" : mktoLeadFields.lastName,
   "Company" : mktoLeadFields.company
   };
 //pass our prefillFields objects into the form.vals method to fill our fields
 form.vals(prefillFields);
 }
 );
</script>
```

_케니_&#x200B;이(가) _2014-10-24_&#x200B;에 게시함

## 이메일 HTML 바꾸기

이 게시물은 이메일에 대해 Marketo에서 생성한 HTML을 제거하는 방법을 보여 줍니다. 그런 다음 Marketo에서 다시 서식을 지정하지 않고 자체 HTML을 사용할 수 있습니다.

1. 전자 메일로 이동한 다음 초안 편집을 클릭합니다.
1. 이메일 작업, HTML 도구, HTML 바꾸기 를 차례로 클릭합니다.
1. 이 상자의 코드를 HTML으로 바꿉니다. 그런 다음 [저장]을 클릭합니다.

_2014-10-28_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 방문자의 쿠키 ID를 가져온 다음 관련 리드 데이터를 쿼리합니다.

[필터 유형별 여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) REST 끝점을 사용하여 사용자의 쿠키 ID를 기반으로 리드 데이터를 쿼리할 수 있습니다. 예를 들어 이 접근 방식을 사용하여 Marketo이 아닌 랜딩 페이지에서 양식을 미리 채울 수 있습니다. 이 게시물은 웹 페이지 방문 중에 사용자의 쿠키 값을 캡처하고 해당 쿠키 ID로 [여러 리드 REST API 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 쿼리한 다음 사용자의 리드 데이터를 반환하는 방법을 보여 줍니다. 먼저 사용자의 Munchkin 쿠키인 &#39;_mkto_trk&#39;의 값이 필요합니다. 다음은 쿠키 값을 가져오는 데 사용할 수 있는 JavaScript 함수의 예입니다. 이 방법에 대한 자세한 내용은 [이 StackOverflow 페이지](https://stackoverflow.com/questions/10730362/get-cookie-by-name)를 참조하십시오. 이 함수를 호출하기 전에 페이지 로드 이벤트 후 500ms의 지연을 설정하는 것이 좋습니다. 이를 통해 Munchkin에서 로드할 시간을 확보하고 사용자에게 쿠키를 제공할 수 있습니다.

```javascript
//Function to read value of a cookie
function readCookie(name) {
    var cookiename = name + "=";
    var ca = document.cookie.split(';');
    for(var i=0;i < ca.length;i++) {
        var c = ca[i];
        while (c.charAt(0)==' ') c = c.substring(1,c.length);
        if (c.indexOf(cookiename) == 0) return c.substring(cookiename.length,c.length);
    }
    return null;
}

//Call readCookie function to get value of user's Marketo cookie
var value = readCookie('_mkto_trk');
```

그런 다음 &#39;_mkto_trk&#39; 쿠키의 값을 서버에 전달합니다. 리드 데이터를 검색하려면 서버에서 이 쿠키 값을 사용하여 [여러 리드 REST API 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 호출합니다. 인스턴스의 인증 및 REST 끝점이 필요합니다. 호출을 다음과 같이 구조화해야 합니다.

참고: `_mkto_trk` 쿠키 값에는 앰퍼샌드가 포함되어 있으며 Marketo 끝점에서 올바르게 수락하려면 `%26`(으)로 URL 인코딩이 필요합니다.

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "cde42eff-aca0-48cf-a1ac-576ffec65a84:ab"
# Replace with filter type and values
filter_type_and_values = "&filterType=cookies&filterValues=id:AAA-BBB-CCC%26token:_mch-marketo.com-1418418733122-51548&fields=cookies,email"
request_url = marketo_instance + endpoint + auth_token + filter_type_and_values

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

위의 예는 사용자와 연결된 이메일 및 모든 쿠키를 반환합니다. 그런 다음 이 데이터를 사용하여 사용자가 방문하는 후속 페이지를 개인화할 수 있습니다.

`{"requestId":"aa00#14a405aa786","result":[{"id":583,"email":"<testaccount@gmail.com>","cookies":"_mch-marketo.com-1418418733122-51548"}],"success":true}`

_2014-10-30_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 마케팅 자동화에 도움이 되는 개발자가 필요한 경우

참고: 게스트 블로그 게시물입니다. Josh Hill 은 마케팅 자동화 에이전시인 Perkuto 의 Marketo Practice Lead 입니다. Josh는 마케팅, 판매, 기술의 교차점에서 수익 창출 시스템을 제공합니다. [MarketingRockstarGuides.com](https://www.marketingrockstarguides.com/)에서 마케팅 자동화 및 수요 창출에 대해 작성합니다.

마케팅 자동화 플랫폼은 즉시 그리고 숙련된 운영자의 손에서 매우 강력합니다. 기본적으로 플랫폼은 확장 애플리케이션을 사용하여 시스템이 팀에 보다 놀라운 작업을 수행하도록 합니다. Marketo의 논리 엔진은 매우 많은 (그리고 그것은) 능력을 가지고 있다고 생각할 수 있지만 한계가 있습니다. Marketo이 모든 것을 여러분을 위해 할 수는 없으며, 그래서도 안 됩니다.

Marketo이 빌드할 수 있는 것보다 더 나은 기능을 수행하는 다른 도구가 있습니다. Marketo의 플랫폼이 매우 열려 있으므로 [LaunchPoint 에코 시스템(응용 프로그램 ](https://exchange.adobe.com/apps/browse/ec?product=MRKTO))이 존재할 수 있습니다. 또한 이러한 개방성을 사용하여 비즈니스 요구 사항에 맞게 사이트와 Marketo의 기능을 확장할 수도 있습니다. Marketo과 같은 플랫폼의 가장 큰 장점은 일반적인 마케터가 완전한 프로그래머가 되지 않고도 페이지, 이메일 및 라우팅 논리를 작성할 수 있다는 것입니다.
요즘 마케터는 논리를 이해해야 하지만 실제 프로그래밍은 전문가에게 맡기는 것이 가장 좋다. 개발자를 언제 호출해야 하는지 어떻게 알 수 있습니까? 프로그래머가 개입해야 하는 시기를 결정하는 몇 가지 기본 규칙 또는 휴리스틱이 있습니다. - Marketo에 필요성에 대한 명백한 필터, 트리거 또는 기능이 없는 경우 일부 JavaScript 또는 jQuery로 수행할 수 있습니다. - 이 작업이 Marketo에 비해 너무 복잡합니까? - Marketo이 이렇게 할 수 있습니까? - 이 웹 사이트 사용자 지정은 쉽게 지원되지 않습니까? - Marketo이 웹 사이트 또는 다른 데이터베이스와 이야기해야 합니까? &quot; 컴퓨터가 할 수 있는 것처럼 들리지만 Marketo에는 이에 대한 기능이 없습니까?&quot; Marketo은 기본 기능을 제공하지 않지만 많은 타사 통합 및 사용자 정의 연결에 연결합니다.

[LaunchPoint 마켓플레이스](https://exchange.adobe.com/apps/browse/ec?product=MRKTO)에서 다음 범주 중 일부를 살펴보십시오. - [분석 도구](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [데이터 추가](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) - [콘텐츠 관리 시스템](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) 일부 타사 애플리케이션은 플랫폼(GoToWebinar) 내에서 직관적인 컨트롤 패널 및 설정 도구를 제공합니다. 이러한 &quot;기본&quot; 통합은 로그인을 설정한 다음 Marketo에서 사용하면 가장 많은 작업을 수행해야 합니다. 그러나 다른 확장에서는 직접 프로그래밍해야 하는 보다 복잡한 API를 사용해야 합니다.

**Marketo의 통합 옵션** - LaunchPoint 통합 - 일반적으로 로그인 또는 간단한 설정입니다. - API 통합 - API 및 프로그래밍 설정 필요: (1) [REST API](/help/rest-api/rest-api.md) (2) [SOAP API](/help/soap-api/soap-api.md) (3) [Webhook 통합](/help/webhooks/webhooks.md) - 특수 코드를 설정해야 하지만 매우 쉽습니다. (4) [이메일 스크립팅](./email-scripting.md)(속도) - JavaScript 및 jQuery: (1) [Forms 2.0](/help/javascript-api/forms-api-reference.md) (2) [리드 추적(Munchkin)](/help/javascript-api/lead-tracking.md) (3) [RTP JS](/help/javascript-api/web-personalization.md) 개발자를 사용하여 Marketo 플랫폼의 기능을 확장하는 몇 가지 사용 사례입니다. 이러한 사용 사례가 있습니까? 그렇다면 개발자와 이야기할 시간이 될 수 있습니다. [LaunchPoint의 서비스 파트너 섹션을 방문하십시오](https://exchange.adobe.com/apps/browse/ec?product=MRKTO).

_2014-11-06_&#x200B;에 _Josh_&#x200B;에 의해 게시됨

## Slack과 Marketo 통합

[Slack은 엔터프라이즈 공동 작업 플랫폼입니다](https://slack.com/). 팀이 Slack을 사용하는 경우 Marketo 알림을 워크플로우로 쉽게 가져올 수 있습니다. 이 게시물은 Marketo에서 특정 잠재 고객 활동이 발생할 때 채팅 로그에 알림을 추가하는 방법을 보여줍니다. 잠재적 사용 사례로는 전체 팀에 양식 채우기, 가격 책정 페이지 방문 또는 30일 동안 연락하지 않은 잠재 고객에 대해 알리는 작업이 있습니다. 아래 스크린샷은 이 도움말 문서의 단계를 수행한 후 Marketo 알림이 Slack에서 어떻게 표시되는지 보여 줍니다.

1. Slack에 로그인. Slack의 통합 클릭
1. 수신 Webhooks에 대한 추가 단추를 클릭합니다.
1. Marketo 알림에 대한 채널을 선택합니다. 그런 다음 수신 Webhook 통합 추가 를 클릭합니다.
1. 웹후크 URL 복사 및 붙여넣기(8단계에 필요)
1. 알림 이름 선택
1. Marketo에 로그인. 관리자로 이동합니다. 웹후크를 클릭합니다.
1. New Webhook 클릭
1. Webhook의 이름을 입력합니다. 4단계에서 Webhook URL을 입력합니다. 요청 유형으로 게시물을 입력합니다. 페이로드 템플릿을 입력합니다.

다음은 스크린샷의 페이로드 템플릿입니다. 리드 수준의 이름, 회사 및 이메일 주소 토큰을 사용합니다.

`payload={"text": "DEVELOPER SITE ALERT: {{lead.First Name:default=edit me}} {{lead.Company=edit me}}, {{lead.Email Address:default=no email address}}" }`

1. Marketo에서 트리거 캠페인을 설정합니다. 흐름 단계는 Webhook을 호출하여 Slack에 전달하는 것입니다. 스마트 목록은 웹 페이지 방문입니다.
1. 작동하는지 확인합니다.

Marketo의 Webhooks에 대한 자세한 내용은 [개발자 설명서](./webhooks/webhooks.md)를 참조하십시오.

_2014-11-10_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Litmus와 Marketo 통합

[Litmus는 브라우저 및 이메일 클라이언트에서 이메일을 테스트하는 서비스](https://www.litmus.com/)입니다. Litmus는 클릭, 열기 및 삭제를 포함하여 이메일에 대한 분석도 제공합니다. 이 게시물은 Marketo을 Litmus와 통합하는 방법을 보여 줍니다.

1. Marketo에서 이메일 프로그램을 설정할 때 프로그램 대시보드에서 &quot;내 토큰&quot;을 클릭합니다
1. &quot;이메일 스크립트&quot; 토큰을 중간 패널로 드래그하여 추가합니다.
1. 토큰 이름을 지정하고 &quot;편집하려면 클릭하십시오.&quot;
1. 오른쪽의 &quot;표준 개체&quot; 아래에서 &quot;잠재 고객&quot; 범주를 확장합니다. &quot;이메일 주소&quot; 필드를 찾아 상자를 선택합니다. 동일한 페이지 왼쪽의 빈 스크립트 공간에 Litmus에서 제공하는 추적 코드에 붙여넣습니다. Litmus 코드에서 `{{lead.Email Address}}`의 모든 인스턴스를 `${lead.Email}`(으)로 바꿉니다. Save 를 클릭하여 Lightbox 창을 닫고 토큰 페이지에서 &quot;Save&quot; 를 다시 클릭합니다.
1. 토큰 `{{my.LitmusToken}}`의 이름을 메모해 두십시오. 추적할 이메일을 엽니다. 이메일의 맨 아래에 새 스크립트 토큰을 배치합니다. Litmus 버전 `{{my.LitmusToken:default=editme}}`과(와) 일치하도록 기본 정보를 추가할 수도 있습니다.

이메일을 전송하면 스크립트는 Marketo에서 이메일에 배치됩니다.

_2014-11-18_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo 랜딩 페이지가 Facebook에 공유될 때 이미지 지정

Facebook에서 Marketo 랜딩 페이지를 공유할 때 이미지가 자동으로 표시되게 하려고 한다고 가정해 보겠습니다. 또한 이 이미지가 Marketo 랜딩 페이지 자체가 아니라 Facebook 공유에 있기를 원할 수도 있습니다. Marketo 랜딩 페이지에 오픈 그래프 메타 태그를 추가하여 이렇게 할 수 있습니다. 이 작업을 수행하는 단계는 아래에 나와 있습니다.

1. 랜딩 페이지를 선택합니다. 그런 다음 초안 편집을 클릭합니다.
1. 페이지 메타 태그 편집을 클릭합니다.
1. Facebook OG 태그 섹션에 오픈 그래프 메타 추가 . 그런 다음 [저장]을 클릭합니다. 형식은 다음과 같습니다. `<meta property="og:image" content="http://example.com/example.jpg"/>`

자세한 내용은 Facebook의 개발자 설명서를 참조하십시오[ 오픈 그래프 메타 태그에 대한 정보.](https://developers.facebook.com/docs/sharing/best-practices)

_2014-11-17_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 레퍼러 기반 페이지 리디렉션

Marketo 랜딩 페이지로 직접 이동하는 것을 방지한다고 가정해 보겠습니다. 이 페이지에 PDF과 같이 다운로드 가능한 콘텐츠가 포함되어 있으며 사용자가 받기 전에 양식을 먼저 작성하기를 원한다고 상상해 보십시오. 사용자가 특정 페이지에서 왔는지 확인하여 해결할 수 있습니다. 이 경우 사용자가 양식을 작성해야 하는 페이지가 됩니다. 사용자가 해당 페이지에서 오지 않을 경우 사용자를 양식 작성 페이지로 리디렉션할 수 있습니다. 이를 수행하려면 콘텐츠가 있는 랜딩 페이지의 레퍼러 페이지가 양식 채우기 페이지인지 확인해야 합니다.
아래 코드 조각에 있는 `http://example.com/PageWithForm`의 두 인스턴스를 모두 사용자를 연결하려는 페이지에 대한 링크로 바꾸십시오. 이 양식은 페이지 작성 양식일 수 있습니다.**

```javascript
<script>
window.onload = function() {
  if (document.referrer !== "http://example.com/PageWithForm") {
    document.location.href = "http://example.com/PageWithForm";
  };
 };
</script>
```

콘텐츠가 있는 Marketo 랜딩 페이지의 닫기 태그 앞에 사용자 지정된 JavaScript 코드 조각을 포함합니다.** 사용자가 양식 작성 페이지의 콘텐츠와 함께 랜딩 페이지로 전송되지 않으면 사용자는 이제 양식 작성 페이지로 리디렉션됩니다.

_2014-11-18_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Trello와 Marketo 통합

Trello는 [인기 있는 웹 기반 프로젝트 관리 응용 프로그램](https://trello.com/)입니다. 팀이 Trello를 사용하는 경우 Marketo 알림을 워크플로우로 쉽게 가져올 수 있습니다. 이 게시물은 Marketo 알림이 있는 카드를 Trello 보드에 추가하는 방법을 보여줍니다. Marketo에서 특정 리드 활동이 발생하면 이 카드가 추가됩니다. 잠재적 사용 사례로는 전체 팀에 양식 채우기, 가격 책정 페이지 방문 또는 30일 동안 연락하지 않은 잠재 고객에 대해 알리는 작업이 있습니다.

1. Trello에 로그인합니다. Marketo 알림을 추가할 Trello 보드로 이동합니다. 목록 추가를 클릭한 다음 이름을 지정합니다.
1. 사이드바 표시를 클릭합니다. Email-to-board Settings 를 클릭합니다. &quot;이 게시판의 이메일 주소&quot; 상자에 이메일을 기록합니다. 이 이메일은 6단계에서 사용됩니다. Marketo 알림을 추가할 목록을 선택하십시오.
1. Marketo에 로그인. 새 스마트 캠페인을 클릭합니다. 이름을 입력한 다음 [저장]을 클릭합니다.
1. 스마트 목록으로 이동합니다. 이 스마트 캠페인에 대한 트리거를 선택합니다. 이 예제에서는 양식 채우기 트리거를 사용합니다. [양식 채우기] 트리거를 가운데 패널로 드래그합니다. 이 알림을 트리거할 양식을 선택하십시오.
1. 이메일을 만듭니다. 새로 만들기를 클릭합니다. 로컬 자산을 클릭합니다. 새 이메일을 클릭합니다. 이메일 이름을 지정합니다. 그런 다음 만들기를 클릭합니다.
1. 5단계에서 생성한 이메일에 대해 &quot;초안 편집&quot;을 클릭합니다. Trello 카드에 표시할 관련 토큰을 드래그합니다. Marketo 이메일의 제목 줄은 Trello 카드의 제목에 나타나며 Marketo 이메일의 본문은 Trello 카드의 설명에 나타납니다. 예를 들어 잠재 고객의 이름과 성을 Trello 카드 제목에 포함하려면 &quot;잠재 고객 경고: `{{lead.First Name:default=edit me}}` `{{lead.Last Name:default=edit me}}`을(를) 사용할 수 있습니다. 그런 다음 이메일을 승인합니다.
1. Smart Campaign으로 이동합니다. 흐름을 클릭합니다. 경고 보내기를 가운데 패널로 드래그합니다. 방금 만든 이메일을 선택합니다. 없음으로 &quot;전송 대상&quot;을 선택합니다. 2단계에서 Trello 이메일로 &quot;다른 이메일로&quot;를 선택합니다.
1. 상단 메뉴에서 예약을 클릭합니다. 활성화 를 클릭합니다. 확인을 클릭합니다.
1. 통합을 테스트합니다. 리드의 이름과 성이 제목에 있는 카드가 Trello 보드에 표시됩니다. 자세한 내용은 [Trello의 설명서](https://support.atlassian.com/trello/)를 참조하세요.

_2014-11-18_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 사용자 정의 필드 값으로 리드 찾기

특정 활동 또는 비활성 기준과 일치하는 Marketo API의 리드를 가져오려고 한다고 가정해 보겠습니다. 예를 들어 지난 30일 동안 점수가 변경되지 않은 잠재 고객을 찾고 싶을 수 있습니다. 이 게시물의 단계를 수행하면 이 리드 목록을 가져올 수 있습니다. 이를 위해 Marketo에서 지난 30일 동안 점수가 변경되지 않은 리드를 식별하는 스마트 캠페인을 만든 다음 이러한 리드에 값을 저장하여 식별하게 됩니다. 그런 다음 이 값으로 API를 쿼리합니다.

1. customLeadStatus** 라는 새 사용자 정의 필드를 만들고 Marketo에 로그인한 다음 Admin Panel로 이동합니다. 필드 관리를 클릭합니다. &quot;새 사용자 정의 필드&quot;를 클릭합니다.  필드 이름을 지정합니다. 그런 다음 만들기를 클릭합니다.
1. 30일 동안 업데이트되지 않은 리드를 찾는 스마트 목록으로 스마트 캠페인을 만듭니다.** 스마트 캠페인을 클릭합니다. 새 스마트 캠페인의 이름을 지정합니다. [악보 없는 드래그]가 오른쪽 패널에서 중간 패널로 변경되었습니다.
1. 3단계에서 스마트 캠페인에 흐름 단계를 추가하여 customLeadStatus 필드를 새 값으로 업데이트합니다.** [데이터 값 변경]을 오른쪽 패널에서 중간 패널로 드래그합니다.
1. Smart Campaign을 업데이트하여 리드가 여러 번 실행되도록 합니다.**을 클릭합니다. 그런 다음 [편집]을 클릭합니다.  항상 를 선택합니다. 그런 다음 [저장]을 클릭합니다. 이제 캠페인 실행이 시작됩니다.
1. 필터 유형 REST API별로 [여러 리드를 가져옵니다](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 쿼리합니다. filterType=customLeadStatus &amp; filterValue=needsEnrichment.** 매개 변수를 제공합니다.

이 데이터를 반환하는 예제 요청입니다.

`<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?access_token=><yourAccessToken>&filterType=customLeadStatus&filterValues=needsEnrichment`

성공적인 API 호출은 customLeadStatus 필드가 needsEnrichment 값과 일치하는 리드가 있는 JSON 데이터를 반환합니다. 자세한 내용은 [필터 유형별 여러 리드 가져오기 REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 검토하십시오.

_2014-11-22_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## SOAP API를 통한 영업 기회 동기화

이 게시물에서는 SOAP API를 통해 Marketo에 영업 기회를 삽입하고 회사 및 리드와 연결하는 방법을 설명합니다. 이 프로세스는 이 프로세스의 작동 방식에 대한 설명으로 시작하여 각 시나리오에 대한 코드 샘플을 제공합니다.

**테이블 구조 다이어그램** 먼저 아래 다이어그램은 테이블 구조를 설명합니다. 이 ID는 레코드(일련 번호) 생성 시 자동으로 생성됩니다. 굵게 표시된 필드는 필수 필드입니다. 영업 기회 직원 역할에만 필수 필드가 있습니다. 괄호로 묶인 필드는 선택 사항이며 점선이 있는 연결도 마찬가지입니다.

**기본 영업 기회 삽입** 먼저 영업 기회를 삽입한 다음 영업 기회를 잠재 고객에 연결하는 영업 기회 사용자 역할을 삽입합니다. 이 예에서는 가망 고객 ID와 기회 ID를 사용하여 기회 사용자 역할을 지정합니다. Opportunity 를 만들면 SOAP Response에서 Opportunity Id 를 가져옵니다. 잠재 고객 ID는 Marketo 잠재 고객 데이터베이스의 모든 잠재 고객에 표시됩니다.

**회사 연결** 대부분의 경우 개인 외에 회사에 기회를 연결하려고 합니다. Marketo에서는 SOAP API를 통해 회사 레코드에 액세스할 수 없으며 리드 레코드만(리드 레코드에 회사 필드가 포함됨) 액세스할 수 있습니다. 각 Lead에 고유한 Company Identifier 를 추가하고 Opportunity에서 해당 ID 를 사용하여 Opportunity 를 Company에 연결할 수 있습니다. 1단계는 리드 레코드에 &#39;회사 ID&#39; 필드를 만들고 이를 일반적으로 백엔드 시스템의 고유 식별자로 채우는 것입니다. 2단계는 영업 기회에 &#39;회사 ID&#39; 필드를 만드는 것입니다. Marketo 지원 또는 컨설팅 팀에 이러한 필드를 만들어 달라고 요청해야 합니다. 그런 다음 Opportunity 를 생성할 때 이 필드를 채웁니다. 그러면 Opportunity 가 Company에 연결됩니다. 이는 Marketo Revenue Cycle Analytics 를 사용하고 Opportunity Influence Analyzer 를 사용하려는 경우 특히 중요합니다. 이 분석은 회사 정보에 따라 다릅니다.

**외부 식별자 사용** 대부분의 경우 백엔드 시스템과 통합할 때 고유한 식별자가 있을 수 있습니다. 외래 키를 통해 Marketo에서 이러한 고유 식별자를 사용할 수 있습니다. 잠재 고객의 경우 일반적으로 고유 식별자로 Marketo ID 또는 이메일 주소 대신 사용되는 외부 시스템 사용자 ID(FSPID)를 사용합니다. FSPID는 Marketo 내부에 표시되지 않는 숨겨진 시스템 필드입니다. 아직 저장하지 않았다면 Opportunity 동기화가 FSPID를 사용자 지정 필드(예: &quot;Foreign ID&quot;)에 저장해야 합니다(필드 이름을 무엇이든 지정할 수 있음). Marketo 관리자로서 이 필드를 직접 만들 수 있습니다. Opportunity 의 경우 Marketo Support 가 Opportunity에 다른 사용자 정의 필드 ( 예: &quot;Foreign Id&quot;) 를 생성하게 합니다. 그런 다음 Opportunities 를 삽입할 때 이 필드를 채웁니다. 마지막으로, 영업 기회 직원 역할을 만들 때는 Marketo ID를 사용하는 대신 두 개의 외래 키를 사용하여 가망 고객과 영업 기회 간 링크를 지정합니다. 외래 키를 사용하여 Opportunity 의 Lead 를 업데이트할 수도 있습니다. 현재는 영업 기회 직원 역할 레코드에 외래 키를 추가할 수 없으므로 이에 대해 자동 생성된 Marketo ID(영업 기회 직원 역할을 만든 후 SOAP 응답에 표시됨)를 사용해야 합니다.

**코드 예제** 단계: 1. 외래 키 및 회사 ID 1로 잠재 고객을 삽입/업데이트합니다. 외래 키 1을 사용하여 영업 기회를 삽입합니다. 외래 키가 있는 영업 기회 직원 역할 1을 삽입합니다. SOAP 요청 - 외래 키 및 회사 Id로 기존 잠재 고객 업데이트 외래 키 &quot;12346&quot; 및 계정/회사 Id &quot;C123&quot;으로 기존 잠재 고객(Marketo Id &quot;6&quot;)을 업데이트합니다. 또한 영업 기회 직원 역할에 필요하기 때문에 사용자 지정 필드에 외래 키를 저장하고 있습니다. 외래 키 사용은 선택 사항입니다. Marketo ID를 사용하여 이 리드를 Opportunity에 연결할 수도 있습니다. 회사 ID 사용도 선택 사항이지만 RCA에서 Opportunity Influence Analyzer 를 사용하려는 경우 필요합니다. 요청:

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:18:30-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncLead>
         <leadRecord>
            <Id>6</Id>
            <ForeignSysPersonId>12346</ForeignSysPersonId>
            <leadAttributeList>
               <attribute>
                  <attrName>FSPID</attrName>
                  <attrValue>12346</attrValue>
               </attribute>
               <attribute>
                  <attrName>cAccountFSID</attrName>
                  <attrValue>C123</attrValue>
               </attribute>
            </leadAttributeList>
         </leadRecord>
         <returnLead>false</returnLead>
      </mkt:paramsSyncLead>
   </soapenv:Body>
</soapenv:Envelope>
```

응답:

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncLead>
         <result>
            <leadId>6</leadId>
            <syncStatus>
               <leadId>6</leadId>
               <status>UPDATED</status>
               <error xsi:nil="true"/>
            </syncStatus>
            <leadRecord xsi:nil="true"/>
         </result>
      </ns1:successSyncLead>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

SOAP 요청 - 영업 기회 만들기 이 경우 영업 기회 테이블에 2개의 사용자 지정 필드가 만들어졌습니다. - `opportunityId` → 영업 기회 고유 ID 보유 - `cAccountFSID` → 고유한 영업 기회 ID를 지정하는 대신 회사 참조 보유. Marketo에서 생성한 Opportunity ID 를 사용할 수도 있습니다. 이 경우 외부 키 노드를 제외합니다. 회사 연관도 선택 사항이지만 RCA에서 Opportunity Influence Analyzer 를 사용하려면 필수입니다. 요청:

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:03:28-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>Opportunity</type>
               <externalKey>
                  <name>opportunityId</name>
                  <value>Opportunity_4</value>
               </externalKey>
               <attribList>
                  <attrib>
                     <name>opportunityId</name>
                     <value>Opportunity_4</value>
                  </attrib>
                  <attrib>
                     <name>Name</name>
                     <value>Opportunity 4 for ACME</value>
                  </attrib>
                  <attrib>
                     <name>IsClosed</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>IsWon</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Amount</name>
                     <value>501.00</value>
                  </attrib>
                  <attrib>
                     <name>CloseDate</name>
                     <value>2014-10-24</value>
                  </attrib>
                  <attrib>
                     <name>ExpectedRevenue</name>
                     <value>501</value>
                  </attrib>
                  <attrib>
                     <name>Probability</name>
                     <value>100</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Company</mObjType>
                     <externalKey>
                        <name>cAccountFSID</name>
                        <value>C123</value>
                     </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

응답:

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>40</id>
                  <externalKey>
                     <name>opportunityId</name>
                     <value>Opportunity_4</value>
                  </externalKey>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

SOAP 요청 - 영업 기회 직원 역할 이 요청은 잠재 고객을 영업 기회에 연결합니다. 단일 SOAP 요청에서 여러 링크를 지정할 수 있습니다(이 예에서는 Opportunity 를 1 개의 Lead 에만 연결함). 외래 키를 사용하여 링크를 지정하지만 주석에는 실제 ID를 사용하는 방법도 표시됩니다(이 경우 잠재 고객 ID는 6, 영업 기회 ID는 40). 이 &quot;IsPrimary&quot; 및 &quot;Role&quot; 필드는 선택 사항입니다. 요청:

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:18:30-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>OpportunityPersonRole</type>
               <attribList>
                  <attrib>
                     <name>IsPrimary</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Role</name>
                     <value>Marketing Manager</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Lead</mObjType>
                     <!--id>6</id-->
                     <externalKey>
                      <name>FSPID</name>
                      <value>12346</value>
                     </externalKey>
                  </mObjAssociation>
                  <mObjAssociation>
                     <mObjType>Opportunity</mObjType>
                     <!--id>40</id-->
                     <externalKey>
                      <name>opportunityId</name>
                      <value>Opportunity_4</value>
                    </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

응답:

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>11</id>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**대체 방법(한 번의 호출로 2단계 및 3단계 수행)** 먼저 영업 기회를 삽입한 다음 영업 기회 사용자 역할을 삽입할 수 있지만 한 번의 SOAP 호출에서도 이 작업을 수행할 수 있습니다. 그러나 영업 기회에 외래 키를 사용해야 합니다(영업 기회가 아직 생성되지 않았기 때문에 영업 기회 사용자 역할에는 자동 생성된 영업 기회 ID를 사용할 수 없음). 물론 동일한 API 호출에서 여러 개의 Lead 를 이 Opportunity에 연결할 수도 있습니다 (이 예에서는 Opportunity 를 1 개의 Lead 에만 연결함). 요청:

```xml
<soapenv:Envelope xmlns:soapenv="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:mkt="<http://www.marketo.com/mktows/">
   <soapenv:Header>
      <mkt:AuthenticationHeader>
         <mktowsUserId>\*\*\*</mktowsUserId>
         <requestSignature>\*\*\*</requestSignature>
         <requestTimestamp>2014-11-20T15:44:08-07:00</requestTimestamp>
      </mkt:AuthenticationHeader>
   </soapenv:Header>
   <soapenv:Body>
      <mkt:paramsSyncMObjects>
         <mObjectList>
            <!--Zero or more repetitions:-->
            <mObject>
               <type>Opportunity</type>
               <externalKey>
                  <name>opportunityId</name>
                  <value>Opportunity_5</value>
               </externalKey>
               <attribList>
                  <attrib>
                     <name>opportunityId</name>
                     <value>Opportunity_5</value>
                  </attrib>
                  <attrib>
                     <name>Name</name>
                     <value>Opportunity 5 for ACME</value>
                  </attrib>
                  <attrib>
                     <name>IsClosed</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>IsWon</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Amount</name>
                     <value>1500</value>
                  </attrib>
                  <attrib>
                     <name>CloseDate</name>
                     <value>2014-10-24</value>
                  </attrib>
                  <attrib>
                     <name>ExpectedRevenue</name>
                     <value>1500</value>
                  </attrib>
                  <attrib>
                     <name>Probability</name>
                     <value>100</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Company</mObjType>
                     <externalKey>
                        <name>cAccountFSID</name>
                        <value>C123</value>
                     </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
             <mObject>
               <type>OpportunityPersonRole</type>
               <attribList>
                  <attrib>
                     <name>IsPrimary</name>
                     <value>1</value>
                  </attrib>
                  <attrib>
                     <name>Role</name>
                     <value>Marketing Manager</value>
                  </attrib>
               </attribList>
               <associationList>
                  <mObjAssociation>
                     <mObjType>Lead</mObjType>
                     <!--id>6</id-->
                     <externalKey>
                      <name>FSPID</name>
                      <value>12346</value>
                     </externalKey>
                  </mObjAssociation>
                  <mObjAssociation>
                     <mObjType>Opportunity</mObjType>
                     <externalKey>
                      <name>opportunityId</name>
                      <value>Opportunity_5</value>
                    </externalKey>
                  </mObjAssociation>
               </associationList>
            </mObject>
         </mObjectList>
         <operation>UPSERT</operation>
      </mkt:paramsSyncMObjects>
   </soapenv:Body>
</soapenv:Envelope>
```

응답:

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
   <SOAP-ENV:Body>
      <ns1:successSyncMObjects>
         <result>
            <mObjStatusList>
               <mObjStatus>
                  <id>41</id>
                  <externalKey>
                     <name>opportunityId</name>
                     <value>Opportunity_5</value>
                  </externalKey>
                  <status>CREATED</status>
               </mObjStatus>
               <mObjStatus>
                  <id>12</id>
                  <status>CREATED</status>
               </mObjStatus>
            </mObjStatusList>
         </result>
      </ns1:successSyncMObjects>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

_Jep_&#x200B;이(가) _2014-11-26_&#x200B;에 게시함

## 다중 스레드 REST API 요청

Marketo API를 호출할 때 성능을 개선하려면 동시 요청을 수행할 수 있습니다. 이 접근 방식을 사용하면 더 짧은 기간에 더 많은 데이터를 얻을 수 있습니다. API 요청 시 클라이언트와 서버 간 왕복 시간의 일부는 유선 전송 시간입니다. 따라서, 요청을 종합하여 전송하는데 걸리는 전송 시간을 줄일 수 있다면, 우리는 성능을 향상시킬 수 있습니다. 아래 샘플 코드는 Ruby에서 이 작업을 수행하는 방법을 보여 줍니다. 다중 스레드 요청을 만드는 데 사용되는 [이벤트 처리 라이브러리](https://github.com/igrigorik/em-http-request/wiki/Parallel-Requests)인 EventMachine을 사용합니다. 아래 예제에서는 [리드 활동 API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)를 호출하고 두 개의 동시 요청을 수행합니다. 이 접근 방식에서는 두 번째 요청에 대해 클라이언트에서 서버로 전송하는 시간이 줄어듭니다. 이는 첫 번째 요청과 동시에 두 번째 요청을 포함시킴으로써 수행됩니다. API 응답은 텍스트 파일에 기록됩니다.

```java
require 'em-http-request'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify datetime needed as nextPageToken
since_date_time = ["&nextPageToken=A5YMOYZQBOGD2OSYYBYDAQGEMGLBDGDANAABQGRAQWAAKKID", "&nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"]
# Specify activities needed
activity_type_ids = "&activityTypeIds=1&activityTypeIds=12"
requesturl_a = marketo_instance + endpoint + auth_token + since_date_time.at(0) + activity_type_ids
requesturl_b = marketo_instance + endpoint + auth_token + since_date_time.at(1) + activity_type_ids

# Make request
EventMachine.run do
  http1 = EventMachine::HttpRequest.new(requesturl_a).get
  http2 = EventMachine::HttpRequest.new(requesturl_b).get

# When API response is received, write response to a text file
  http1.callback {
  File.open('response1.txt', 'w') do |t|
  t.puts http1.response
  end }

  http2.callback {
  File.open('response2.txt', 'w') do |t|
  t.puts http2.response
  end }
end
```

_2014-12-03_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 성능 조정 API 요청

이 게시물에서는 Marketo API에서 데이터를 요청할 때 성능을 개선하기 위한 전략에 대해 설명합니다. 그러나 Marketo API의 일일 제한 작업 제한과 비교하여 이러한 전략의 이점을 평가해야 합니다.
**전략 1 - 각 API 호출에서 더 적은 데이터 요청** 일반적으로 API 호출에서 더 많은 데이터를 요청하면 Marketo 서버가 데이터베이스에서 데이터를 조회하는 데 걸리는 시간이 늘어납니다. [getMultipleLeads SOAP API](/help/soap-api/getmultipleleads.md)와 같은 날짜 범위로 API를 호출하는 경우 호출당 시간 범위를 줄이고 더 많은 호출을 보상하십시오. 예를 들어, 6월 1일부터 7월 1일까지의 데이터를 요청하는 대신, 6월 1일부터 2일까지의 한 번의 호출과 6월 2일부터 1일까지의 다른 호출과 같이 한 번에 하루씩 요청합니다. Marketo 리드 필드의 데이터를 반환하는 API 호출을 수행하는 경우 해당 필드만 필요합니다. 모든 추가 리드 필드는 API 호출에 걸리는 시간을 점진적으로 증가시킵니다. 또 다른 접근법은 배치 크기, 또는 호출당 요청되는 리드의 수를 감소시키는 것이다.
**전략 2 - 동시 요청 만들기** 성능을 개선하고 한 번에 더 많은 데이터를 가져오려면 API에 대한 동시 요청을 수행할 수 있습니다. 이 접근 방식은 API 요청을 유선으로 연결하는 데 소요되는 시간을 줄여 집계합니다. 예를 들어 필터 유형별 다중 리드 가져오기에 대한 요청을 한다고 가정해 보겠습니다. 한 개의 요청 질의 리드 1 - 300 및 다른 요청 질의 리드 301 - 600에 대해 동시 요청을 수행할 수 있습니다.
**전략 3 - 데이터 캐시** Marketo의 일부 데이터는 리드 활동 데이터와 같은 다른 데이터보다 리드 필드 목록과 같이 변경되는 빈도가 더 적습니다. 덜 자주 업데이트되는 데이터를 캐시하는 경우 수행해야 하는 API 호출 수를 줄입니다. 또한 일반적으로 원격 웹 서비스에서 액세스하는 것보다 로컬에서 데이터를 조회하는 것이 더 빠르기 때문에 성능이 향상됩니다.

_2014-12-05_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo 양식 데이터를 Google Analytics으로 보내기

Google Analytics에서 사용자 지정 데이터 이벤트를 보낸 다음 데이터를 활용하여 웹 사이트 성능을 세그먼트화하고 분석할 수 있습니다. 아래의 JavaScript 코드 스니펫을 사용하면 방문자가 웹 양식을 제출한 후 Marketo 2.0 양식 데이터를 Google Analytics에 자동으로 푸시할 수 있습니다. 설정 방법은 다음과 같습니다.

**1단계** 코드 맨 아래(태그 앞)에 Marketo Forms이 포함된 페이지에 JavaScript 태그를 삽입합니다. JavaScript은 숨겨지지 않은 필드만 보냅니다(sendHiddenFields : false). sendHiddenFields를 false에서 true로 변경하여 조정할 수 있습니다. &#39;fieldsToExclude&#39; 배열에 필드 ID를 추가하여 제외할 필드를 선택할 수도 있습니다.

```javascript
function pushFormDataToGa(a){
setTimeout(function () {
document.getElementsByTagName('form')[0].getElementsByClassName(a.submitButton)[0].addEventListener('click', function() {
  allFields = document.getElementsByTagName('form')[0].getElementsByTagName('input');
  for(i=0;i<allFields.length;i++){
   if( (allFields[i].type !="hidden" && allFields[i].type !="submit" && allFields[i].value !="" && a.fieldsToExclude.indexOf(allFields[i].id) === -1  ) || (allFields[i].type === "hidden" && a.sendHiddenFields) ){
    console.log( allFields[i].name + ": "  + allFields[i].value);
    if(typeof(_gaq) != "undefined"){
    //Classic
    _trackEvent("Marketo Form Submission", allFields[i].value , allFields[i].name
{'nonInteraction': 1});
    }else if(typeof(ga) !="undefined"){
    //Universal
    ga('send', 'event',"Marketo Form Submission", allFields[i].value , allFields[i].name, {'nonInteraction': 1});
}}}}, false);
}, 3000);}
pushFormDataToGa({
 submitButton: "mktoButton",
 fieldsToExclude: ["Email","LastName", "FirstName"],
 sendHiddenFields : false
});
```

**2단계** GA의 데이터가 보고 섹션에 표시됩니다. 비헤이비어 > 이벤트 > 상위 이벤트로 이동합니다. **스크립트 제한:** - 이 코드 샘플은 [Marketo Forms 2.0](/help/javascript-api/forms-api-reference.md)과만 호환됩니다. - Google의 개인정보 처리방침으로 인해 개인 정보(이메일 또는 이름)를 전송할 수 없습니다. 잠재적인 개인 정보 보호 문제를 제외하고, 이는 개인 식별 정보이므로 [Google Analytics의 서비스 약관](https://marketingplatform.google.com/about/analytics/terms/us/)을 위반합니다.

&quot;귀하는 본 서비스를 사용하여 개인을 개인적으로 식별하는 데이터(이름, 이메일 주소 또는 청구 정보 등) 또는 Google이 이러한 정보에 합리적으로 연결할 수 있는 기타 데이터를 추적, 수집 또는 업로드하지 않습니다(그리고 제3자가 그러한 정보를 수집하는 것을 허용하지 않습니다).&quot;

_Yanir_&#x200B;이(가) _2014-12-16_&#x200B;에 게시

## Marketo 양식에 전체 이름 필드 추가

짧은 웹 양식이 전환율을 향상시킨다는 것을 알고 있습니다. 아래 JavaScript 코드 샘플을 사용하면 이름 및 성 필드를 하나의 전체 이름 필드에 병합하여 양식을 더 짧게 만들 수 있습니다. 방문자가 전체 이름을 입력할 때 스크립트는 자동으로 텍스트를 이름과 성 필드로 나눕니다. 알려진 방문자의 경우 스크립트는 이름과 성을 연결한 다음 새 필드에 복사하여 필드를 다시 채우지 않아도 됩니다. 설정 방법은 다음과 같습니다.

**1단계** Marketo에서 전체 이름(Full Name)이라는 새 사용자 지정 필드를 만듭니다. 스크립트는 이 필드를 사용하여 전체 이름을 표시하므로 CRM 플랫폼에서 만들 필요가 없습니다.
**2단계** 이 필드를 모든 웹 양식에 추가합니다. 이름과 성 필드를 숨김으로 설정합니다. JavaScript에서 3개의 필드 이름을 포함하도록 &quot;splitFullName&quot; 구성을 변경합니다. 참고: 이러한 이름이 페이지의 다른 위치에 표시되지 않도록 하십시오.
**3단계** 코드 하단의 태그 앞에 있는 모든 랜딩 페이지에 JavaScript을 삽입합니다.

```javascript
<script>
MktoForms2.whenReady(function (form){
        function splitFullName(a,b,c){
                String.prototype.capitalize = function(){
                        return this.replace( /(^|s)([a-z])/g , function(m,p1,p2){ return p1+p2.toUpperCase(); } );
                };
                document.getElementsByName[c](0).oninput=function(){
                        var fullName = document.getElementsByName[c](0).value;
                        if((fullName.match(/ /g) || []).length ===0 || fullName.substring(fullName.indexOf(" ")+1,fullName.length) === ""){
                                var first = fullName.capitalize();;
                                var last = "null";
                        }else if(fullName.substring(0,fullName.indexOf(" ")).indexOf(".")>-1){
                                var first = fullName.substring(0,fullName.indexOf(" ")).capitalize() + " " + fullName.substring(fullName.indexOf(" ")+1,fullName.length).substring(0,fullName.substring(fullName.indexOf(" ")+1,fullName.length).indexOf(" ")).capitalize();
                                var last = fullName.substring(first.length +1,fullName.length).capitalize();
                        }else{
                                var first = fullName.substring(0,fullName.indexOf(" ")).capitalize();
                                var last = fullName.substring(fullName.indexOf(" ")+1,fullName.length).capitalize();
                        }
                        document.getElementsByName[a](0).value = first;
                        document.getElementsByName[b](0).value = last;
                };
                //Initial Values
                if(document.getElementsByName[c](0).value.length < 2 && document.getElementsByName[b](0).value.length.length >2 && document.getElementsByName[a](0).value.length.length >2 ){
                        var first = document.getElementsByName[a](0).value.capitalize();
                        var last = document.getElementsByName[b](0).value.capitalize();
                        var fullName =  first + " " + last ;
                        console.log(fullName);
                        document.getElementsByName[c](0).value = fullName;
                }
        }
        splitFullName("FirstName","LastName","leadFullName");
});
</script>
```

참고: 이 코드는 Marketo Forms 2.0에서만 작동합니다.

_Yanir_&#x200B;이(가) _2014-12-16_&#x200B;에 게시

## cURL을 사용하여 REST API를 통해 리드 가져오기

REST API를 통해 CSV 파일에서 리드를 가져오시겠습니까? 하지만 Postman Chrome 확장을 사용하면 이 작업이 어려워집니다. 이 게시물에서는 cURL을 사용하여 이 작업을 수행하는 방법에 대해 설명합니다.

1. [Marketo의 REST API로 데이터를 푸시하는 데 사용하는 명령줄 도구인 cURL을 다운로드하여 설치](https://curl.se/download.html)합니다.
1. 명령줄을 연 다음 CSV 파일이 있는 위치로 이동합니다. CSV 파일의 열 헤더는 Marketo 필드 이름이 아닌 API 필드 이름과 일치해야 합니다.
1. 액세스 토큰이 필요합니다. Marketo에 로그인하고 관리자로 이동한 다음 LaunchPoint로 이동합니다. REST API 사용자를 찾아 &quot;세부 정보 보기&quot;를 클릭합니다. &quot;토큰 가져오기&quot; 단추를 클릭합니다.
1. 또한 Marketo 인스턴스에 고유한 REST 엔드포인트가 필요합니다. Marketo에 로그인하고 관리자, 웹 서비스 순으로 이동합니다. &quot;REST API&quot;로 표시된 섹션에서 끝점 URL을 찾습니다.
1. 명령줄에서 cURL 호출에 대해 이 형식을 따릅니다. `<accesstoken>`을(를) 3단계의 액세스 토큰으로 바꾸고 `<REST API Endpoint URL>`을(를) 4단계의 REST API 끝점 URL로 바꿉니다. 추가 정보는 [여기에서 사용 가능](https://developer.adobe.com/marketo-apis/api/mapi/#operation/importLeadUsingPOST)합니다. 여기에서 &quot;/bulk&quot;는 끝점 URL의 끝에 있는 &quot;/rest&quot;를 대체합니다. /rest/bulk에 대한 엔드포인트가 설정되어 있으면 오류를 반환합니다.

`curl -i -F format=csv -F file=@leaddata.csv -F access_token=<accesstoken> <REST API Endpoint URL>/bulk/v1/leads.json`

_요르단_&#x200B;이 _2014-12-16_&#x200B;에 게시함

## Marketo에 확인 경고 추가

사용자가 Marketo 양식에서 &quot;보내기&quot; 버튼을 클릭하면 사용자에게 &quot;보내도 됩니까?&quot;라고 묻는 알림이 표시된다고 가정해 보겠습니다. 이는 JavaScript의 몇 줄을 구현하면 가능합니다. 이 몇 줄은 누군가가 [보내기] 단추를 클릭할 때 확인 상자를 표시합니다. 다음은 이 작업을 수행하는 방법의 예입니다. 아래 표시된 대로 onSubmit 함수를 Marketo 양식에 추가합니다. Marketo Forms API에 대한 자세한 내용은 [개발자 설명서를 확인](/help/javascript-api/forms-api-reference.md)하십시오.

```javascript
<script src="//app-e.marketo.com/js/forms2/js/forms2.js"></script>
<form id="mktoForm_19"></form>
<script>
MktoForms2.loadForm("//app-e.marketo.com", "212-RBI-463", 19,function(form){

//Add this function to your Marketo form script
form.onSubmit(function(){
alert("Do you really want to submit the form?");
});
});
</script>
```

_David_&#x200B;이(가) _2014-12-17_&#x200B;에 게시함

## 후속 랜딩 페이지 없이 감사 메시지 표시

일반적으로 Marketo Forms를 사용할 때 두 개의 랜딩 페이지(양식을 배치하기 위한 페이지와 양식이 완료된 후 리디렉션하기 위한 페이지)를 만듭니다. 그러나 경우에 따라 유지 관리하기 위해 두 개의 서로 다르지만 매우 유사한 랜딩 페이지를 원하지 않을 수 있습니다. 실제로 Forms 2.0 JavaScript API를 사용하여 양식과 감사 메시지에 대해 동일한 랜딩 페이지를 사용할 수 있습니다. 이렇게 하려면 먼저 등록 랜딩 페이지와 양식을 만들고 일반적인 방법으로 랜딩 페이지에 양식을 배치합니다. 그런 다음 페이지에 HTML 요소를 추가합니다. 이 요소에서는 양식이 제출되는 순간 활성화되는 일부 코드를 추가합니다. 그런 다음 양식을 숨기고 숨겨진 을 표시합니다 <div> 여기에는 감사 메시지가 포함되어 있습니다. JavaScript은 다음과 같아야 합니다.

```javascript
//Edit host with your Marketo instance info
<script src="//<host>/js/forms2/js/forms2.js"></script>
<script>
MktoForms2.whenReady(function (form){
 //Add an onSuccess handler
  form.onSuccess(function(values, followUpUrl){
   //get the form's jQuery element and hide it
   form.getFormElem().hide();
   document.getElementById('confirmform').style.visibility = 'visible';
   //return false to prevent the submission handler from taking the lead to the follow up url.
   return false;
 });
});
</script>
```

감사 인사 메시지 텍스트를 편집합니다.

`<div id="confirmform" style="visibility:hidden;"><p><strong>Thank you. Check your email for details on your request.</strong></p></div>`

코드 샘플에서 호스트 이름 및 감사 메시지를 편집하려고 합니다. 첫 번째는 Marketo 인스턴스(예: &quot;//app-sj06.marketo.com/js/forms2/js/forms2.js&quot;)를 참조하고 두 번째는 양식이 완료되면 표시할 감사 텍스트를 포함해야 합니다. 텍스트는 랜딩 페이지에 HTML 요소를 배치하는 정확한 위치에 표시되므로 속성 시트에서 편집해야 합니다. 또한 HTML 요소의 레이어가 양식의 레이어보다 작은지 확인해야 합니다. 기본적으로 둘 다 레이어 15에 배치되므로 HTML 요소 레이어 11을 만드는 경우 안전합니다. 이렇게 하지 않으면 감사 메시지와 겹치는 양식 필드 상자를 입력할 수 없습니다. JavaScript이 이러한 설정을 덮어쓰게 되므로 양식이나 랜딩 페이지에서 후속 유형을 변경할 필요는 없습니다. Marketo Forms API에 대한 자세한 내용은 [개발자 설명서](/help/javascript-api/forms-api-reference.md)를 참조하십시오.

_Kristin_&#x200B;이(가) _2014-12-19_&#x200B;에 게시함

## Marketo Platform에 빌드된 열린 Source 프로젝트 강조 표시

개발자 커뮤니티에 의해 Marketo 플랫폼을 기반으로 빌드된 오픈 소스 프로젝트를 강조 표시하는 지속적인 시리즈의 첫 번째 게시물입니다. Marketo 개발자 커뮤니티에서 만든 클라이언트 라이브러리 및 프로젝트를 추적하는 [Marketo의 GitHub 계정에 있는 목록](https://github.com/Marketo/Community-Supported-Client-Libraries)을 유지 관리합니다. 다음은 Marketo REST 및 SOAP API를 중심으로 개발된 세 가지 프로젝트입니다. Daniel Chesterton이 PHP에서 Marketo REST API용 [클라이언트 라이브러리를 만들었습니다](https://github.com/dchesterton/marketo-rest-api). 클라이언트 라이브러리는 현재 12개의 REST API 끝점에 대한 범위를 가지고 있습니다.**의 카일 할스트베트(Kyle Halstvedt)가 [Marketo 정적 목록에서 Google 스프레드시트로 잠재 고객을 가져오기 위한 프로젝트를 만들었습니다](https://github.com/Elixiter/mkto_google-spreadsheet). Kyle의 프로젝트에서는 Marketo REST API를 사용합니다.  David Santoso는 Marketo SOAP API용 [Ruby gem을 만들었습니다.](https://github.com/davidsantoso/markety) 이 프로젝트를 통해 Marketo SOAP API를 Ruby on Rails 앱과 보다 빠르게 통합할 수 있습니다.  Marketo 플랫폼에서 개발자 커뮤니티가 만드는 더 많은 프로젝트를 보게 되어 기쁘게 생각합니다. Marketo 플랫폼용 오픈 소스 프로젝트를 작업하는 경우 [끌어오기 요청을 통해 이 GitHub 리포지토리에 제출](https://github.com/Marketo/Community-Supported-Client-Libraries)하십시오.

_2015-01-02_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 사용자 위치에 따라 페이지 콘텐츠를 동적으로 변경

사용자가 있는 위치에 따라 랜딩 페이지의 전화 번호를 동적으로 변경한다고 가정해 보겠습니다. 예를 들어, 해당 사용자가 캘리포니아에 있는 경우 랜딩 페이지에 캘리포니아 사무실 전화번호를 표시하고 싶지만 일본에 있는 경우 일본 사무실 전화번호를 표시합니다.  이를 구현하는 한 가지 방법은 JavaScript 및 [HTML5 지리적 위치 API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)를 사용하는 것입니다. 이 접근 방식의 이점은 여러 정적 랜딩 페이지 대신 하나의 랜딩 페이지를 만들고 사용자의 위치에 따라 동적으로 변경할 수 있다는 것입니다. 아래 기술 구현 세부 사항을 안내합니다. 위도와 경도 좌표가 있는 사무실 위치에 대한 개체를 만들고, 사무실 전화 번호가 있는 두 번째 개체를 만듭니다. 프로덕션에서는 이 두 객체를 하나의 객체로 결합하는 것이 더 나을 것입니다.

```json
//Coordinates for Marketo offices
var officeLocations = {
    "San Mateo": {latitude: 37.5596465, longitude: -122.2870142},
    "Atlanta": {latitude: 33.8547013, longitude: -84.35552349999999},
    "Tokyo": {latitude: 35.6895, longitude: 139.6917},
    "Dublin": {latitude: 53.3478, longitude: -6.2603097},
    "Sydney": {latitude: -33.873651, longitude: 151.2068896},
    "Portland": {latitude: 45.512089, longitude: -122.6763367},
    "Tel Aviv": {latitude: 32.0852999, longitude: 34.78176759999999}
}

//Phone numbers for Marketo offices
var officePhoneNumbers = {
    "San Mateo": "+1-650-376-2300",
    "Atlanta": "+1-877-260-6586",
    "Tokyo": "+81-03-6759-8280",
    "Dublin": "+353-1-242-3000",
    "Sydney": "+61-2-9045-2711",
    "Portland": "+1-877-260-6586",
    "Tel Aviv": "+1-877-260-6586"
}
```

사용자의 위치를 요청하는 메서드를 만듭니다. 오류를 처리하기 위해 사용자의 위치에 액세스할 수 없는 경우 기본적으로 Marketo 본사와 전화 번호가 사용됩니다.

```javascript
//Method to get user's current location. Returns a position object with user's geo coordinates
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(findNearestOffice);
    } else {
        x.innerHTML = "Marketo Location: San Mateo
Marketo Phone Number: +1-877-260-6586";
    }
}
```

마지막으로 사용자 위치에서 가장 가까운 사무실을 찾는 방법을 만든 다음 페이지에서 가장 가까운 사무실의 전화번호를 반환합니다. 이 메서드는 [Geolib의 findNearest 메서드를 사용합니다. 이 메서드는 지리공간 작업을 제공하는 JavaScript 라이브러리입니다](https://github.com/manuelbieh/Geolib).

```javascript
//Find nearest Marketo office to user's location
function findNearestOffice(position) {
        var nearestOffice = geolib.findNearest({latitude: position.coords.latitude, longitude: position.coords.longitude}, officeLocations);
        x.innerHTML = "Marketo Location: " + nearestOffice.key + "
Marketo Phone Number: " +  officePhoneNumbers[nearestOffice.key];
}
```

전체 구현은 다음과 같습니다. 사용자가 페이지에서 버튼을 클릭하면 getLocation 메서드가 트리거됩니다. 이 [GitHub 저장소](https://github.com/MurtzaM/Find-Nearest-Marketo-Office)에는 이 데모를 설정하는 데 필요한 파일이 있습니다.

_2014-12-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 잠재 고객 추적 및 여러 도메인

Marketo의 Munchkin 추적 코드는 웹 사이트 방문을 추적하는 데 도움이 됩니다. 웹 사이트의 대부분 또는 모든 페이지에 대해 Munchkin 추적 코드를 사용하여 익명 리드를 쿠키에 추가할 수 있습니다. Munchkin의 작동 방식을 살펴보겠습니다. 페이지 방문은 기존 잠재 고객에 대해 기록되며, 비쿠키 방문자의 페이지 방문으로 인해 새 쿠키가 생성되고 저장되고, Marketo 데이터베이스에 새 익명 잠재 고객이 생성됩니다. 현재 도메인에 대한 기존 쿠키가 없는 경우 Munchkin 추적기에서 방문자에게 자동으로 쿠키를 제공합니다. Marketo에서는 잠재 고객의 활동 로그에 이벤트(링크 클릭, 웹 페이지 방문 또는 새 잠재 고객)를 기록합니다. 쿠키 내에 저장된 값은 지정된 방문자에 대해 고유합니다. 이 값은 고유한 Munchkin 계정 추적 ID, 도메인 이름, 타임스탬프 및 임의의 정수의 조합입니다.
**여러 도메인이 있는 경우 어떻게 됩니까?** 추적할 사이트가 두 개 있다고 가정합니다. `<www.apples.com>` 및 `<www.bananas.com>`. 두 사이트 모두에 추적 코드를 넣을 수 있지만, 다음 사항을 고려해야 합니다. Marketo 쿠키는 &#39;자사 쿠키&#39;이므로 도메인별로 다릅니다. 즉, 사이트 1에 대한 방문자가 Marketo에서 익명 잠재 고객으로 만들어지고, 동일한 잠재 고객이 사이트 2로 이동하면 Marketo에 두 번째 개별 익명 잠재 고객이 만들어집니다. 리드가 사이트 1의 양식을 작성한 후 이 레코드를 알려면 사이트 2에 대한 익명 레코드가 유지되며 이후 해당 사이트에 대한 방문이 계속 누적됩니다. 그런 다음 잠재 고객이 사이트 1에서 사용된 것과 동일한 이메일 주소로 사이트 2의 양식을 작성하면 알려진 두 잠재 고객이 자동으로 병합되고 Marketo의 단일 레코드에서 모든 과거 및 향후 동작이 추적됩니다. 두 쿠키 ID는 동일한 리드에 연결되고 모든 웹 활동(두 도메인 중 하나의 활동)은 해당 리드에 있습니다.
**여러 하위 도메인은 어떻습니까?** 하위 도메인은 문제가 아닙니다. 예를 들어 Marketo.com 을 사용하겠습니다. 여기에는 fr.marketo.com 및 de.marketo.com과 같이 서로 다른 언어를 위한 여러 하위 도메인이 있습니다. 하위 도메인을 사용하면 모든 활동이 동일한 리드 레코드/쿠키에 대해 기록됩니다.

_David_&#x200B;이(가) _2015-01-13_&#x200B;에 게시함

## Marketo Form에서 힌트 텍스트 색상 변경

Forms 2.0에서 힌트 텍스트 색상(자리 표시자 텍스트라고도 함)을 변경하려고 한다고 가정해 보겠습니다. 이는 사용자 지정 CSS를 통해 가능합니다. 예를 들어 아래 스크린샷에서 이 Marketo Form의 힌트 텍스트를 파란색으로 만들었습니다. 이 작업을 수행하는 방법은 Marketo Forms을 사용하는 방법에 따라 세 가지 옵션이 있습니다.

**옵션 1: Marketo 양식을 포함하는 경우 아래 CSS를 기본 CSS 파일에 직접 추가하십시오.**

```css
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
```

**옵션 2: Marketo 양식을 포함할 때 `<style></style>` 섹션의 `<head>` 태그 사이에 페이지에서 직접 CSS를 추가할 수 있습니다.**

```css
<style>
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
</style>
```

**옵션 3: Marketo 랜딩 페이지에서 Marketo 양식을 사용하는 경우, Marketo UI를 통해 이 사용자 지정 CSS를 추가할 수 있습니다.** Marketo 탐색 트리에서 랜딩 페이지를 찾습니다. 그런 다음 초안 편집을 클릭합니다. 페이지 메타 태그 편집을 클릭합니다. 아래의 CSS를 사용자 지정 HEAD HTML 섹션에 추가합니다. `<style></style>` 태그를 포함해야 합니다.

```css
<style>
::-webkit-input-placeholder {
  color: blue;
}
::-moz-placeholder {
  color: blue;
}
:-ms-input-placeholder {
  color: blue;
}
:-moz-placeholder {
  color: blue;
}
</style>
```

초안 승인 을 클릭합니다. 이제 Marketo 랜딩 페이지를 방문할 때 힌트 텍스트는 CSS에서 정의한 색상입니다. Marketo Forms에 대한 자세한 내용은 [설명서를 참조하십시오](/help/javascript-api/forms-api-reference.md).

_2015-01-14_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## REST API를 통해 활동 데이터 가져오기

이번 달에 목록에 추가된 모든 리드를 가져오려고 한다고 가정해 보겠습니다. [리드 활동 가져오기 REST API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)를 사용하면 이 데이터를 가져올 수 있습니다. 리드 활동 가져오기 API를 호출하기 전에 인증 API에서 액세스 토큰을 가져와야 하며 [페이징 토큰 가져오기 API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getActivitiesPagingTokenUsingGET)에서 시작 날짜 토큰을 가져와야 합니다. 다음은 이번 달 목록에 추가된 모든 리드를 반환하기 위해 호출해야 하는 개별 API 엔드포인트를 안내하는 Ruby의 예제 코드입니다. 1. 액세스 토큰 **

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com/identity/oauth/token?grant_type=client_credentials>"
# Relace with your client id
client_id = "99985d09-22a9-3jl2-84av-f5baae7c3a45"
# Replace with your your  client secret
client_secret = "tZPVrKiEmUDezE18yZfeaPlTJ2vKn2fw"
request_url = marketo_instance + "&client_id=" + client_id + "&client_secret=" + client_secret

# Make request
response = RestClient.get request_url

# Parse reponse and return only access token
results = JSON.parse(response.body)
access_token = results["access_token"]
puts access_token
```

1. 페이징 토큰 가져오기

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities/pagingtoken.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify date
since_date_time = "&sinceDatetime=2015-01-01T00:00:00-08:00"
request_url = marketo_instance + endpoint + auth_token + since_date_time

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. 활동 데이터 가져오기** 이 호출에 필요한 활동 유형 ID를 확인하려면 [가져온 활동 유형 API](/help/rest-api/activities.md)를 쿼리하십시오. 활동 유형 가져오기 API는 모든 활동 유형과 관련 ID가 있는 스키마를 반환합니다. 예를 들어 생성된 새 리드에 대해 id 12 를 반환하고 웹 페이지 방문에 대해 id 1 을 반환합니다.

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/activities.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Specify datetime needed as nextPageToken
since_date_time = "&nextPageToken=GIYDAOBNGEYS2MBWKQYDAORQGA5DAMBOGAYDAKZQGAYDALBQ"
# Specify activities needed
activity_type_ids = "&activityTypeIds=24"
request_url = marketo_instance + endpoint + auth_token + since_date_time + activity_type_ids

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. 리드 활동 가져오기 API는 결과 세트를 통해 페이지를 매기는 데 사용할 수 있는 각 응답과 함께 페이지 지정 토큰을 반환합니다.** 자세한 내용은 [REST API 설명서](/help/rest-api/rest-api.md)를 참조하세요.

_2015-01-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo Platform을 기반으로 구축된 개방형 Source 프로젝트 강조 표시: 2부

개발자 커뮤니티에 의해 Marketo 플랫폼을 기반으로 빌드된 오픈 소스 프로젝트를 강조 표시하는 지속적인 시리즈 중 두 번째 게시물입니다. Marketo 개발자 커뮤니티에서 만든 클라이언트 라이브러리 및 프로젝트를 추적하는 [Marketo의 GitHub 계정에 있는 목록](https://github.com/Marketo/Community-Supported-Client-Libraries)을 유지 관리합니다. 다음은 Marketo SOAP 및 Munchkin API를 중심으로 개발된 세 가지 프로젝트입니다. [PunchTab](https://www.punchtab.com/)에서 Marketo SOAP API용 Python에 [클라이언트 라이브러리를 만들었습니다](https://github.com/PunchTab/suds-marketo). [Flickerbox](https://www.flickerbox.com/)이(가) Marketo SOAP API용 PHP에 클라이언트 라이브러리를 [만들었습니다](https://github.com/flickerbox/marketo).* [Richard Morrison](https://x.com/mozz100)이(가) Marketo SOAP API에서 리드 데이터를 가져온 다음 JavaScript을 사용하여 이 데이터를 클라이언트에 전달하는 PHP 스크립트를 [만들었습니다.](https://github.com/mozz100/marketo-whodat) 이 프로젝트를 통해 Marketo의 사용자 데이터를 기반으로 페이지를 수정할 수 있습니다.  Marketo 플랫폼에서 개발자 커뮤니티가 만드는 더 많은 프로젝트를 보게 되어 기쁘게 생각합니다. Marketo 플랫폼용 오픈 소스 프로젝트를 작업하는 경우 [끌어오기 요청을 통해 이 GitHub 리포지토리에 제출](https://github.com/Marketo/Community-Supported-Client-Libraries)하십시오.

_2015-01-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Google Analytic으로 RTP 권장 사항 엔진 클릭 수 전송

다음은 Marketo 실시간 Personalization(RTP) 사용자가 Google Analytics 내의 컨텐츠 권장 사항 엔진에서 클릭을 볼 수 있는 솔루션입니다. 방문자가 컨텐츠 권장 사항 표시줄을 클릭하면 이벤트가 이벤트 카테고리 &quot;RTP-Recommendations&quot; 아래의 Google Analytics으로 전송됩니다. Analytics에서는 권장 사항 텍스트(표시줄에 표시됨)가 이벤트 레이블에 추가되고 권장 에셋의 URL이 이벤트 작업에 추가됩니다. 이 스크립트는 클래식 Google Analytics 및 Google Universal Analytics 모두에서 작동합니다. 이 태그는 `</body>` 태그 앞의 마지막 태그가 되도록 HTML 페이지 코드의 끝에 붙여 넣어야 합니다.

```javascript
$( document ).ready(function() {
if(document.getElementsByClassName("insightera-bar-content").length
 >0){
document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].addEventListener("click",
 function(){
assetName
 = document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].innerText;
assetURL
 = document.getElementsByClassName("insightera-bar-content")[0].getElementsByTagName('a')[0].href;
assetURL=
 assetURL.substring(assetURL.lastIndexOf("/"),assetURL.indexOf("?iesrc"));
console.log(assetName

 * " | " + assetURL);
if(typeof(_gaq)
 != "undefined"){
//Classic
_trackEvent("RTP-Recommendations",
 assetName , assetURL , {'nonInteraction': 1});
}else
 if(typeof(ga) !="undefined"){
//Universal
ga('send',
 'event',"RTP-Recommendations", assetName , assetURL, {'nonInteraction': 1});
}
});
}
});
```

_Yanir_&#x200B;이(가) _2015-01-22_&#x200B;에 게시

## Boomi에서 Marketo REST API 사용: REST 인증 토큰 가져오기 및 저장

특정 기준을 충족하는 잠재 고객의 자동 내보내기를 설정하는 것은 Marketo의 매우 일반적인 사용 사례입니다. 현재 Marketo 인터페이스에서는 이 작업을 수행할 수 없지만 Dell Boomi, 일부 데이터 관리 캠페인이 포함된 정적 목록, Marketo REST API와 같은 타사 도구를 사용하여 수행하는 것은 매우 간단합니다. REST API? 부미에는 Marketo REST API 커넥터가 없는 줄 알았습니다! 글쎄요, 현재는 아니지만, HTTP 커넥터를 사용하고 jSON 응답 모양을 수동으로 정의하는 방식으로 동일한 작업을 수행할 수 있습니다. 첫 번째 단계는 [REST API Marketo 개발자 페이지](/help/rest-api/rest-api.md)에 설명된 대로 REST API를 사용하도록 Marketo 인스턴스를 설정하는 것입니다. 또한 Dell Boomi 계정에 액세스할 수 있으며 이러한 유형의 통합 프로세스를 만들 수 있는 Boomi 기술을 보유하고 있다고 가정합니다. 최종 프로세스는 다음과 유사하며, 각각 개발자 사이트에서 찾을 수 있는 관련 jSON 응답 셰이프를 갖는 다음 Marketo REST API 작업에 대한 호출을 포함합니다. 시간을 절약하기 위해 [인증](/help/rest-api/authentication.md)에 대한 JSON 예제 아래에 나열했습니다.

```json
{
  "access_token": "",
  "token_type": "",
  "expires_in": 0,
  "scope": ""
}
```

[목록 ID로 여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)에 대한 JSON 예

```json
{
  "requestId": "",
  "success": true,
  "nextPageToken": "",
  "result": [
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    }
  ]
}
```

[목록에서 리드 제거](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)에 대한 JSON 예

```json
{
  "requestId": "",
  "success": true,
  "result": [
    {
      "id": 1,
      "status": ""
    },
    {
      "id": 2,
      "status": "",
      "reasons": [
        {
          "code": "",
          "message": ""
        }
      ]
    }
  ]
}
```

속성 정의: REST를 호출하기 전에 사용 중인 변수를 외부화하고 캡슐화하는 것이 중요합니다. 아래에 표시된 다음 항목을 정의했습니다.

* ClientID: REST Launchpoint 서비스에서 가져오기
* 클라이언트 암호: REST Launchpoint 서비스에서 가져오기
* AccessToken: REST 호출에서 가져옵니다.
* 정적 목록 ID: 작업할 정적 목록의 목록 ID입니다. Marketo의 URL에서 다운로드
* 필드: 나머지 서비스가 각 리드에 대해 Marketo에서 가져오는 필드를 쉼표로 구분한 목록입니다. 내 이름은 &quot;id, email,firstName,lastName&quot;입니다. * IDStringToDelete: 결국에는 목록에서 제거하는 데 사용할 정적 목록에 있는 모든 리드의 ID가 포함됩니다.
* ActivityTypes: 이 블로그의 2부에서 사용되며 여기에서 확장하겠습니다.
* SinceDateTime: 이 블로그의 2부에서 사용되며 여기에서 확장됩니다!
* PagingToken: 이 블로그의 2부에서 사용됩니다.
* 폴더 - 발신: SFTP 서버의 발신 폴더에 대한 경로입니다. 이 예제에서는 &quot;/data/outgoing&quot;을 사용합니다. 이를 통해 SFTP 작업을 매개 변수화하여 제네릭으로 만들 수 있습니다.

인증 토큰: 언급했듯이 &quot;데이터 없음&quot; 시작 셰이프로 프로세스를 만든 후 캔버스에 커넥터를 배치합니다(개인적인 선택일 뿐, 모든 커넥터가 영국 플러그처럼 보이는 것을 좋아합니다).
커넥터는 다음과 같이 구성해야 합니다. - 커넥터는 HTTP GET 클라이언트입니다. - 연결은 URL을 사용합니다. `https://123-ABC-456.mktorest.com`(끝에 /rest가 없음). 이를 REST 호출 및 ID 액세스 토큰을 가져오는 데 사용할 수 있도록 이 작업을 끝냅니다. 및 123-ABC-456을 Marketo 인스턴스에 대한 올바른 매개 변수로 변경) - 작업이 &quot;oAuth 토큰 가져오기&quot;(new!) - 요청 프로필 = 없음 - 응답 프로필 = JSON - 새 프로필 &quot;인증 토큰 응답&quot; - 콘텐츠 유형: 일반 - HTTP 메서드: GET - 리소스 경로(따옴표 없이 4개 추가): &quot;identity/oAuth/token?grant_type=client_credentials&amp;client_id=&quot;; &quot;ClientID(대체 변수)&quot;; &quot;&amp;client_secret=&quot;; &quot;ClientSecret(대체 변수)&quot; - 구성 —> 매개 변수 —>(+): Set ClientID = Process Property Client ID; clientSecret = Process Property Client Secret 설정 이 작업을 수행한 후 성공 토큰을 프로세스 속성 &quot;AccessToken&quot; 변수에 저장하고 jSON 응답에서 추출합니다.
이 단계의 패턴은 다음 단계에 대해 반복되지만, 다른 jSON 반환 프로필과 함께 새 작업을 사용합니다. 사실, 많은 REST 호출은 사소한 변경 사항과 같은 방식으로 처리됩니다! 다음 분부에서는 이를 확장하고 REST를 사용하여 정적 목록에서 잠재 고객 목록을 가져옵니다! 지금은 프로세스를 실행하지만 &quot;속성 설정&quot; 뒤에 중지 모양을 놓은 다음 디버그에서 실행하여 Marketo에 표시되는 것과 동일한 토큰을 확인합니다. 그들은 완벽하게 일치해야 합니다!

_John_&#x200B;이(가) _2015-01-26_&#x200B;에 게시함

## Google 글꼴 API를 사용하여 Marketo 랜딩 페이지에 사용자 지정 글꼴 추가

**참고: [Murtza Manzur](https://www.linkedin.com/in/murtzam)의 블로그 게시물입니다. Murtza는 샌프란시스코 베이 지역에 본사를 둔 Marketo 개발자 전도사입니다.**
Marketo에서 랜딩 페이지를 만들고 사용자 정의 글꼴을 사용한다고 가정해 보겠습니다. 이는 Google 글꼴 API를 사용하여 가능합니다.  Google 글꼴을 참조하여 CSS 파일에 가져오기 방법을 추가합니다.

`@import url(http://fonts.googleapis.com/css?family=Open+Sans:400,300,600);`

_2015-01-26_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 이메일 스크립팅을 사용하여 잠재 고객의 이름 대문자로 바꾸기

잠재 고객이 &quot;John doe&quot;와 같이 소문자로 이름을 입력한다고 가정해 보겠습니다. 그러나 이메일 캠페인을 보낼 때 John Doe와 같이 이메일에 있는 잠재 고객의 이름을 대문자로 사용하려고 합니다. 이메일 스크립팅을 사용하여 잠재 고객의 이름을 대문자로 바꿀 수 있습니다. 방법은 다음과 같습니다.

1. 이메일 프로그램에서 &quot;내 토큰&quot; 탭을 클릭합니다.
1. 오른쪽 패널에서 중간 패널로 &quot;이메일 스크립트&quot;를 드래그하여 새 이메일 스크립트 토큰을 만듭니다. 토큰에 이름을 지정합니다.
1. 스크립트 토큰 편집 텍스트 상자에 아래 코드를 붙여넣습니다. 오른쪽 패널의 리드 오브젝트에서 이름 확인란을 선택합니다. 그런 다음 [저장]을 클릭합니다.

```javascript
# set($name = ${lead.FirstName})
# set($formattedFirstName = $name.substring(0).toUpperCase())
$formattedFirstName
```

1. 이메일 에셋의 토큰을 참조합니다. 첫 번째 문자가 대문자로 표시된 잠재 고객의 이름을 출력합니다. 전자 메일 스크립팅에 대한 자세한 내용은 [전자 메일 스크립팅 설명서](/help/email-scripting.md)를 참조하세요.

_2015-01-26_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo REST API에서 모든 리드 가져오기

REST API를 통해 Marketo에서 모든 잠재 고객 목록을 가져오는 방법을 묻는 [질문이 StackOverflow에 있습니다](https://stackoverflow.com/questions/28184900/how-do-i-get-the-list-of-all-the-leads-in-marketo). 필터 유형 REST API 끝점별 [여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 사용하여 이 데이터를 쿼리할 수 있습니다. Marketo의 잠재 고객에는 1부터 시작하여 순차적 순서로 잠재 고객 ID가 지정됩니다. [필터 유형별 여러 리드 가져오기 REST API 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)을 사용하여 각 호출에서 리드 ID별로 300개의 리드를 쿼리할 수 있습니다. 이 끝점에 대한 각 호출에서 id를 filterType으로 지정하고 리드 id를 filterValues로 지정해야 합니다. 모든 리드를 가져오려면 한 번에 총 리드 수 300개를 반복합니다. Y
Marketo UI를 통해 Marketo 인스턴스의 총 리드 수를 가져올 수 있습니다. Marketo UI에서 리드 데이터베이스 탭으로 이동하여 시스템 스마트 목록을 클릭하고 모든 리드 스마트 목록을 클릭한 다음 마지막으로 &quot;리드&quot; 탭을 클릭합니다. 그런 다음 ID 열을 클릭하고 내림차순으로 정렬합니다. 리드가 정렬되면 모든 리드를 쿼리할 때 첫 번째 리드의 ID가 리드 ID의 상한이 됩니다. 총 리드 수를 가져올 수 있는 Marketo UI에 대한 액세스 권한이 없는 경우 리드 활동 가져오기 REST API[를 사용하여 이 값을 가져올 수 있는 ](https://stackoverflow.com/questions/28419967/get-all-leads-programmatically-in-marketo-v1)대체 방법이 있습니다.

1. 첫 번째 API 호출: 바꾸기 ...를 다음 범위의 모든 값으로 바꿉니다.

`/rest/v1/leads.json?filterType=Id&filterValues=1,2,3,...,298,299,300`

다음은 첫 번째 호출에 대한 Ruby의 샘플 코드입니다.

```java
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "<https://AAA-BBB-CCC.mktorest.com>"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
# Replace with filter type and values
ids_needed = (1..300).to_a.join(",")
filter_type_and_values = "&filterType=Id&filterValues=" + ids_needed
request_url = marketo_instance + endpoint + auth_token + filter_type_and_values

# Make request
response = RestClient.get request_url

# Returns Marketo API response
puts response
```

1. 두 번째 API 호출 및 각 후속 API 호출은 총 리드 수에 도달할 때까지 동일한 패턴을 따릅니다.

```
//replace ... with all the values in between
/rest/v1/leads.json?filterType=Id&filterValues=301,302,303,...,598,599,600
```

자세한 내용은 [REST API 설명서](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 참조하세요.

_2015-01-28_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Iframe에서 상위 페이지로 양식 제출 작업 실행

사용자가 iframe 양식을 사용하고 양식을 채운 방문자를 감사 페이지 또는 PDF, 비디오 등으로 안내하려는 경우가 있었습니다. 문제는 양식이 상위 페이지와 다른 랜딩 페이지에 임베드되므로 해당 양식이 있는 내부 페이지에서만 작업이 수행된다는 것입니다. 이 문제를 해결하기 위해 만든 JavaScript 태그 2개는 다음과 같습니다. iframe 페이지에 HTML 요소로 삽입하거나 iframe에 사용하는 랜딩 페이지 템플릿에 직접 삽입합니다. 마지막 `</body>` 태그 앞에 배치합니다. 첫 번째 태그는 상위 페이지에서 작업을 수행하고 두 번째 태그는 새 탭에서 엽니다.

**상위 페이지의 양식 동작**

```javascript
<script>
MktoForms2.whenReady(function (form){
form.onSuccess(function (values, url){
window.parent.location.assign(url);
return false;
           });
});
</script>
```

**새 탭에서 양식 작업**

```javascript
<script>
MktoForms2.whenReady(function (form){
var newWin;
form.onSubmit(function (){
newWin = window.open('about:blank', 'myWindow');
});
form.onSuccess(function (values, url){
newWin.location.replace(url);
return
 false;
});
});
</script>
```

_Yanir_&#x200B;이(가) _2015-02-02_&#x200B;에 게시

## YouTube 비디오에서 보기 데이터를 마켓으로 전송

특정 비디오를 시작했는지 또는 완료했는지 여부에 따라 Marketo의 리드를 세그먼트화한다고 가정해 보겠습니다. Munchkin, YouTube의 Iframe API 및 Marketo의 스마트 목록을 사용하여 수행할 수 있습니다. 이 게시물의 예제 코드를 사용하면 비디오 시작 및 비디오 완료 이벤트를 Munchkin을 통해 Marketo으로 보낼 수 있습니다. 이렇게 하려면 비디오 보기 이벤트를 Munchkin으로 보내기 전에 Marketo도 페이지에 로드해야 합니다. 시작되고 완료된 비디오가 잠재 고객의 활동 로그에 표시됩니다. 데이터가 Marketo에 있으면 비디오를 시작하거나 완료한 스마트 목록 및 세그먼트 리드를 만들 수 있습니다.

1. 포함할 YouTube 비디오의 ID를 가져옵니다.** 사용하려는 YouTube 비디오의 URL에서 `v=` 뒤에 일련의 임의의 문자인 ID를 확인합니다.
1. 1단계의 YouTube 비디오 id를 이 코드 샘플의 8번째 줄에 배치합니다. 그런 다음 페이지의 HTML에서 `</body>` 앞에 코드를 넣습니다.

```javascript
<div id="player"></div>
<script>
var tag = document.createElement('script');
tag.src = "https://www.youtube.com/iframe_api";
document.getElementsByTagName('head')[0].appendChild(tag);

//Change 'iiqxcjxJ5Us' to video needed
var player, videoId = 'iiqxcjxJ5Us';
function onYouTubeIframeAPIReady() {
player = new YT.Player('player', {
height: '390',
width: '640',
videoId: videoId,
events: {
'onStateChange': onPlayerStateChange
}
});
}

function onPlayerStateChange(event) {
switch( event.data ) {
//Send video started event to Marketo
case YT.PlayerState.PLAYING: Munchkin.munchkinFunction('visitWebPage', {
url: '/video/'+videoId
, params: 'video=started'
}
);
break;
//Send video finished event to Marketo
case YT.PlayerState.ENDED: Munchkin.munchkinFunction('visitWebPage', {
url: '/video/'+videoId
, params: 'video=finished'
}
);
break;
}

}
</script>
```

1. &quot;Querystring contains&quot; 값으로 찾고 있는 비디오 URL 및 보기 이벤트를 사용하여 Marketo에서 스마트 목록을 만듭니다. YouTube Iframe API에 대한 자세한 내용은 [YouTube의 API 설명서를 참조하십시오](https://developers.google.com/youtube/iframe_api_reference). Munchkin에 대한 자세한 내용은 [Marketo 개발자 설명서를 검토](/help/javascript-api/lead-tracking.md)하십시오.

_2015-02-02_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo SOAP API 팁 및 요령

참고: 게스트 블로그 게시물입니다. [Ed Blachman은 수석 설계자입니다](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D2777965) [TIBCO Software, 잘 알려진 엔터프라이즈 소프트웨어 공급업체](https://exchange.adobe.com/apps/browse/ec?product=MRKTO). Ed는 Gartner가 &quot;시민 개발자&quot;라고 부르는 서비스를 직접 프로그래밍할 필요 없이 사용하는 클라우드 서비스를 통합할 수 있도록 지원하는 제품을 개발하고 있습니다. [Marketo의 SOAP API](/help/soap-api/soap-api.md)는 개발자가 Marketo의 기능을 활용하고 자체 애플리케이션과 통합할 수 있는 강력한 도구입니다. [정식 설명서](./getting-started.md)와(과) [커뮤니티 리소스](https://nation.marketo.com/) 사이에 사용 방법에 대한 정보가 많이 있습니다. 제가 시작했을 때, 저는 그 정보에 많이 의존했고 그것이 매우 소중하다는 것을 알았습니다. 하지만, 그 과정에서, 저는 그 어느 곳에서도 보지 못한 몇 가지 비법과 요령을 터득했습니다. 제가 알아낸 것이 있습니다.

**개발자의 샌드박스** 샌드박스는 API 개발자를 위한 훌륭한 리소스입니다. Marketo 기능을 실험하고, 조직의 실제 Marketo 사용자가 수행하는 실제 마케팅 활동을 방해하지 않고 개체를 추가 및 제거할 수 있는 안전한 공간입니다. 그러나 샌드박스는 만병통치약이 아닙니다.
예를 들어 다른 개발 그룹과 샌드박스를 공유해야 했는데, 이 작업을 수행하는 데 시간이 좀 걸렸습니다. 왜냐하면 그들이 샌드박스를 소유한다는 개념에 익숙해졌기 때문입니다. 결국 두 가지 공유 모범 사례를 확인했습니다. - 샌드박스의 콘텐츠에 대한 완전한 지식에 따라 테스트는 작성하지 마십시오. 공유 리소스로서 스키마는 리드 데이터베이스나 프로그램 또는 다른 엔터티의 전체 항목뿐만 아니라 공지 없이 변경될 수 있습니다. 테스트가 샌드박스에 대한 완전한 지식을 가정하는 경우 개발 주기는 샌드박스를 공유하는 그룹에 대해 일시 중단 기간을 생성합니다. 일반적으로 개발 주기는 사용자의 개발 주기와 일치하지 않으므로 리소스를 연결하는 것은 용납되지 않습니다. 당신이 끝까지 생각한다면 그것은 또한 필요하지 않습니다. - 규칙을 사용하여 리드, 리드 스키마 필드, 프로그램 등 모든 항목에 레이블을 지정합니다. 각자 자신의 물건을 식별할 수 있고, 공동 임차인이 각자 다른 물건의 물건만 남긴다는 것에 동의할 수 있다면, 공유를 위한 확고한 토대가 되어야 한다. 리드의 경우 사용자 정의 필드를 만들고 이 사용자 정의 필드를 사용하여 규칙을 만들어 이러한 리드를 테스트 리드로 식별할 수 있습니다. 목록이나 프로그램의 경우 해당 객체를 자신의 소유로 식별하는 일부 문자열로 객체의 이름을 시작할 수 있습니다. - 테스트 후 정리하는 테스트를 작성하는 것이 좋습니다. 먼저 관심 있는 개체를 만든 다음 개체를 액세스하거나 업데이트하거나 선택적으로 삭제한 다음 최종적으로 제거하십시오. (SOAP API에서는 100% 달성할 수 없습니다. 이는 샌드박스 또는 해당 문제에 대한 실제 인스턴스의 모든 것을 SOAP API를 통해 관리할 수 없기 때문입니다. 그렇다 하더라도, 할 수 있는 한 이 일을 하는 것은 여전히 가치 있는 일이다.)

**실제 인스턴스** 샌드박스의 문제는 프로덕션 환경에서 사용되지 않기 때문에 Marketo 인스턴스에서 실제 사용이 어떻게 표시되는지 파악하기 어렵다는 것입니다. 이제 운 좋게 팀에 Marketo 고급 사용자가 있다거나 내부 Marketo 사용자를 위해 맞춤형 개발을 하고 있다면 이는 그리 문제가 되지 않습니다. 그런데 우리 팀의 경우 정말 큰 거래였다. 우리 중 누구도 Marketo 전문가는 아니었고, 많은 수의 클라우드 서비스를 이해하라는 요청을 받고 있었기 때문에, 우리는 단지 어떤 것에서도 전문가가 될 수 있는 인원을 확보하지 못했습니다. 다음은 실제 인스턴스에 대한 액세스에서 얻은 통찰력 중 일부입니다. - 대규모 리드 스키마. 액세스한 프로덕션 인스턴스의 리드 스키마에는 200개 이상의 필드가 있습니다. 이를 통해 UI 디자이너는 디자인한 UI가 해당 크기(또는 그 이상)의 스키마를 수용해야 한다는 것을 명확히 할 수 있었습니다. - Bursty 사용 가장 높은 사용 시간과 낮은 사용 시간(생성되거나 업데이트된 잠재 고객 수 기준) 간에 두 자릿수의 차이가 있었습니다. 이 문제는 API 호출에서 반환되는 데이터의 양(명확함)과 API 호출이 응답하는 데 소요되는 시간(명확하지 않을 수 있음)에 모두 영향을 주었습니다.

**API 호출 응답 시간** 시간, API 호출의 세부 정보 및 인스턴스의 내용에 따라 SOAP API의 응답 시간이 평균보다 오래 걸릴 수 있습니다. 때때로 응답하는 데 1분 30분이 걸리는 API 호출이 있었습니다. 당신은 그것을 다룰 가능성을 알고 있어야합니다 : - 테스트. 이것은 당신의 사용에 문제가 되지 않을 수도 있습니다. 하지만 그냥 상정하지 말고, 테스트를 좀 해보세요. - 사용량을 조정합니다. 이 경우 [getMultipleLeads](/help/soap-api/getmultipleleads.md) 호출에 대한 페이지 크기를 API에서 허용하는 만큼 크게 설정하는 것이 가장 큰 문제였습니다. 고객의 API 할당량을 최대한 효율적으로 사용하는 것이 목표이기 때문에 상황에 따라 의미가 있습니다. 그러나 컨텍스트에서 사용자의 API 호출 할당량에 대해 그렇게 심각하게 걱정할 필요는 없습니다. 이 경우 더 작은 데이터 페이지를 요청하여 응답 시간이 향상됩니다.

**리드 파티셔닝** Marketo은 여러 마케팅 그룹이 단일 Marketo 인스턴스를 공유할 수 있는 강력한 도구-파티션 및 작업 공간을 제공합니다. 그러나 이러한 도구는 SOAP API에 직접 반영되지 않습니다. 예를 들어, getMultipleLeads 를 사용하여 특정 날짜 시간 이후 업데이트되거나 생성된 모든 리드를 가져오는 경우 지정된 리드가있는 파티션이나 작업 공간에 관계없이(그리고 표시할 내용이 없는) 인스턴스의 모든 리드를 다시 가져옵니다. 리드 생성 및 리드 추가 목록은 리드 분할이 API 호출이 실제로 수행하는 작업에 영향을 줄 수 있는 다른 컨텍스트입니다. 이는 파티션 및 작업 공간이 위에서 설명한 샌드박스 공유 문제에 필요한 솔루션이 아닐 수 있음을 의미합니다. 그래서, 이 문제가 당신에게 문제인지 어떻게 알 수 있을까요? 이러한 모든 것이 도움이 되는 것으로 나타났습니다. 개발자 전도사는 API를 성공적으로 사용할 수 있도록 최선을 다하고 있으며, 질문이 있는 경우 답변을 찾는 작업에 놀라운 능력을 갖추고 있습니다. - [API 설명서](./getting-started.md). 전도사는 이미 이 문제를 일부 설명서에 포함시켰으며, 성공에 대한 약속의 일환으로 문서를 업데이트할 준비가 되어 있습니다. - 자체 테스트 사례. 샌드박스를 공유하기 위해 파티션과 작업 공간을 사용하는 것은 좋은 생각이 아닐 수 있지만 샌드박스는 파티션과 작업 공간으로 이동하여 의도한 사용에 대한 문제를 제기하는지 여부를 파악하는 데 좋은 장소입니다. (이것은 또한 항상 좋은 생각인 전도사를 위한 질문을 좁히는 좋은 방법입니다.)

**TIMTOWTDI 및 테스트** &quot;두 가지 이상의 방법이 있습니다.&quot; - Perl 프로그래밍 좌우명 - 실제로 특정 컨텍스트에서 Marketo SOAP API에 적용됩니다. 예를 들어, 일련의 리드를 업데이트하는 것과 이러한 리드를 일부 목록에 추가하는 것을 통합하고 싶었습니다. SOAP API는 두 가지 방법을 제공합니다. 1. [importToList](/help/soap-api/importtolist.md) + [getImportToListStatus](/help/soap-api/getimporttoliststatus.md) 설명서를 읽어 보면 이는 분명히 이 작업을 수행하는 &quot;일반적인&quot; 방법입니다. 하지만, 당신이 당신의 가져오기 작업의 상태를 폴링해야 한다는 사실은 나를 위해 노란색 깃발을 올렸습니다. 이것이 정말로 제가 가져오기를 구현하고자 했던 방식이었습니까? 1. [syncMultipleLead](/help/soap-api/syncmultipleleads.md) + [listOperation](/help/soap-api/listoperation.md). 이는 단일 importToList 호출보다 훨씬 덜 우아해 보이지만, 투표에 의존하지 않습니다. 실행 가능한 옵션이었습니까? 이런 사례들은 전도사들이 다루기 어렵습니다. 왜냐하면, 복음주의자들은 정말 여러분이 다루는 사건의 성격과 여러분이 하려고 하는 일에 의존하기 때문입니다. 다행히 강력한 단위 테스트 환경을 설정했다면 이와 같은 질문도 탐색하는 데 사용할 수 있어야 합니다. 이 특별한 경우, 폴링이 아니라 importToList에 대한 필드 지향 제한 사항이 발생했기 때문에 옵션 2가 옵션 1보다 사용 사례에 더 적합했고, 또한 제어권이 없는 컨텍스트 및 인스턴스에서 사용할 수 있는 코드를 작성하려고 했기 때문인 것으로 나타났습니다. 그러나 사용 사례는 다를 수 있으며 테스트만이 확인할 수 있는 유일한 방법입니다.

**결론** 이 비밀은 중요하지 않습니다. 다른 한편으로는, 내가 시작하기 전에 이 모든 것을 알았다면 나는 게임을 앞서 있었을 것이다. 유용하게 쓰시길 바랍니다.

_David_&#x200B;이(가) _2015-02-05_&#x200B;에 게시함

## 부오미에 Marketo REST API 사용: 정적 목록에서 리드 가져오기 및 삭제

이 시리즈의 1부에서는 Boomi HTTP 커넥터와 함께 Boomi를 통해 REST API를 사용할 수 있는 방법, 특히 REST API에 액세스하는 데 필요한 인증 토큰을 얻고 프로세스 변수에 저장하는 방법에 대해 논의했습니다. 다음으로 Marketo에 전화를 걸기 시작합니다. 이 할부에서는 [목록 ID별로 여러 개의 잠재 고객을 확보](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)하는 방법과 [목록에서 잠재 고객을 제거](/help/rest-api/lead-database.md)하는 방법을 보여 줍니다. 목록에서 리드를 제거하는 것에 특별히 주의하십시오. 왜냐하면 그 곳에서 일하는 부미의 매우 &quot;가볍게 문서화된&quot; 미묘한 측면이 있기 때문입니다. 우리가 거기에 가면 확장됩니다.

NEXT 할부에서는 이 기능을 확장하여 리드 활동을 시작하는 것과 같은 흥미로운 작업을 시작하지만, 그것은 다른 날을 위한 블로그입니다. 이번 분부에서는 두 번째와 세 번째 하이라이트 부분에 대해서 살펴보도록 하겠습니다. 리뷰로서 아래에 필요한 JSON 응답을 포함했습니다. 부미에서 JSON 프로필을 만들려면 JSON 유형의 프로필 구성 요소를 만들고 &quot;가져오기&quot;를 클릭하고 파일을 선택하기만 하면 됩니다. 부미는 여러 개의 ID가 허용되어야 하는 경우와 같이 외삽하면서 나머지를 수행합니다. [목록 ID로 여러 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)에 대한 JSON 예

```json
{
  "requestId": "",
  "success": true,
  "nextPageToken": "",
  "result": [
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    },
    {
      "id": 0,
      "email": "",
      "firstName": "",
      "lastName": ""
    }
  ]
}
```

[목록 요청에서 리드 제거](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)에 대한 JSON 예

```json
{
   "input":[
      {
         "id": ""
      },
      {
         "id": ""
      }
   ]
}
```

[목록 응답에서 리드 제거](https://developer.adobe.com/marketo-apis/api/mapi/#operation/removeLeadsFromListUsingDELETE)에 대한 JSON 예

```json
{
  "requestId": "",
  "success": true,
  "result": [
    {
      "id": 1,
      "status": ""
    },
    {
      "id": 2,
      "status": "",
      "reasons": [
        {
          "code": "",
          "message": ""
        }
      ]
    }
  ]
}
```

목록 ID로 여러 리드 가져오기** 이전 문서에 정의된 것과 동일한 연결을 사용하여 다른 커넥터(Get)를 프로세스에 놓습니다. &quot;목록 ID로 여러 잠재 고객 가져오기&quot;(일관성을 유지하기 위해 까다롭습니다.)라는 새 작업을 만듭니다. 해당 속성은 다음과 같습니다. - 요청 프로필: 없음(요청 URL을 사용함) - 응답 프로필 유형: jSON - 응답 프로필: 위의 목록 ID로 여러 잠재 고객 가져오기 응답을 기반으로 새 프로필을 만듭니다. 나열된 필드뿐만 아니라 원하는 필드를 반환하도록 변경할 수 있습니다. JSON 응답 프로필이 REST API에서 요청하는 필드 목록과 실제로 일치해야 하며 필요한 필드만 요청해야 한다는 점을 기억해야 합니다. Process Properties 개체에서 &quot;fields&quot;라는 속성을 정의했습니다. 이 속성은 REST에서 반환할 필드를 쉼표로 구분한 목록입니다. 그리고 그것은 프로필과 일치해야 하는 목록입니다. 콘텐츠 유형: text/plain(URL 요청만 해당) HTTP 메서드: GET(REST API 문서에서 살펴보면 항상 나열됨) 리소스 경로(5개 추가) rest/v1/list/ listID(대체 변수) /leads.json?access_token= access_token(대체 변수) &amp;fields= fields(대체 변수). 그런 다음 커넥터의 매개 변수 탭에서 변수 값을 입력할 수 있습니다. 이 값은 모두 이전에 프로세스 속성에 채워졌습니다. 다음 섹션에서는 이러한 필드를 수동으로 채우는 것을 방지하는 방법에 대해 설명합니다. 간단한 부미 기능이므로 목록 ID로 여러 잠재 고객 가져오기 응답을 플랫 파일 프로필에 매핑하는 프로세스 부분을 건너뛰고 FTP 서버에 고정합니다.

목록에서 잠재 고객 삭제 이 프로그램은 흥미롭습니다. 동료 중 한 명인 [Ken Niwa](https://www.linkedin.com/uas/login?session_redirect=https%3A%2F%2Fwww.linkedin.com%2Fprofile%2Fview%3Fid%3D7429494)이(가) 이 다음 기술을 가르쳐 주었습니다. 매우 멋지고 &quot;RESTful 애플리케이션에 대한 POST 요청을 작성하는 방법&quot;이라는 부미 문서를 기반으로 한 것입니다.  ...하지만 먼저 해야 할 일이 있습니다. 이 프로세스에서는 &quot;목록 ID별 다중 리드 가져오기&quot;에서 나왔으므로 목록 ID 응답 별 다중 리드 가져오기 형태가 있으며, 이를 &quot;목록 요청에서 리드 제거&quot;에 매핑해야 합니다. 이 매핑은 매우 간단하며 원래 목록의 리드에서 가져온 ID를 delete jSON으로 전달하는 ID 목록에 매핑합니다. 다음으로, &quot;Send&quot; 작업으로 다른 커넥터를 삭제하고, 동일한 연결 만들기 &quot;Remove Leads from List Request&quot; 라는 새 작업을 수행합니다. 요청 프로필: jSON 콘텐츠 유형: application/json 요청 프로필: [JSON 프로필] 목록 요청에서 리드 제거(위 파일에서 생성됨) 응답 프로필 유형: jSON 응답 프로필: [JSON 프로필] 목록 응답에서 리드 제거(위 파일에서 생성됨) 콘텐츠 유형: application/json HTTP 메서드: DELETE 리소스 경로(추가 4) rest/v1/lists/ listID(대체 변수) /leads.json?access_token= access_token(대체 변수) 이 커넥터에 대한 흥미로운 사항은 다음과 같습니다. 커넥터 탭에 매개 변수를 명시적으로 추가하지 않습니다. 대신 이 문서에서 설명하는 대로 대체 변수와 이름이 같은 동적 문서 속성을 만듭니다. 이 경우 이러한 변수는 listID 및 access_token입니다. 이렇게 하면 jSON 셰이프가 REST 호출로 연결되고 매개 변수가 URL의 적절한 위치에 나타납니다. 이전 호출은 POST가 아닌 GET이므로 이 작업을 수행할 수 없습니다. 따라서 이 시점에서 GET 및 POST REST API 호출을 보았으므로 이러한 REST 호출을 수행하는 패턴을 볼 수 있습니다. 다음 할부에서는 REST API를 통한 리드 활동 수출을 살펴볼 것이며, 이는 약간 더 관련되어 있습니다.

_John_&#x200B;이(가) _2015-02-06_&#x200B;에 게시함

## Marketo 랜딩 페이지에 리드 추적이 포함된 YouTube 비디오 포함

이전 블로그 게시물에서 특정 YouTube 비디오가 시작되었는지 또는 완료되었는지에 따라 Marketo의 잠재 고객을 세그먼트화하는 방법을 설명했습니다. 이 블로그 게시물에서는 해당 게시물에서 구현을 가져와서 Marketo 랜딩 페이지에서 사용하는 방법을 안내합니다.

1. 새 랜딩 페이지를 만들 Marketo의 프로그램으로 이동합니다. 새 로컬 자산 을 클릭한 다음 랜딩 페이지 를 클릭합니다.
1. 랜딩 페이지 이름을 지정합니다. 페이지 URL을 할당합니다. 템플릿을 선택합니다. 그런 다음 만들기를 클릭합니다.
1. 랜딩 페이지가 만들어지면 초안 편집 을 클릭합니다.
1. 오른쪽 패널에서 HTML 버튼을 왼쪽의 기본 캔버스로 드래그합니다.
1. 표시되는 사용자 지정 HTML 편집기 상자에서 그런 다음 [저장]을 클릭합니다.
1. 상자 윤곽선을 드래그하여 HTML 요소의 크기를 조정합니다. 그런 다음 승인 및 닫기를 클릭합니다.
1. 승인된 페이지 보기 를 클릭하여 랜딩 페이지의 라이브 버전을 테스트합니다. YouTube이 포함된 랜딩 페이지가 새 창에 열립니다. 시작되고 완료된 비디오는 아래 첫 번째 및 두 번째 스크린샷과 같이 잠재 고객의 활동 로그에 표시됩니다. 데이터가 Marketo에 있으면 아래 스크린샷과 같이 비디오를 시작하거나 완료한 스마트 목록 및 세그먼트 리드를 만들 수 있습니다. YouTube Iframe API에 대한 자세한 내용은 [YouTube의 API 설명서를 참조하십시오](https://developers.google.com/youtube/iframe_api_reference). Munchkin에 대한 자세한 내용은 [Marketo 개발자 설명서를 검토하십시오](/help/javascript-api/lead-tracking.md).

_2015-02-09_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Munchkin을 사용한 단일 페이지 애플리케이션 웹 추적

단일 페이지 애플리케이션 은 첫 번째 페이지 로드 시 사이트를 탐색하는 데 필요한 모든 리소스를 로드하는 웹 사이트입니다. 사용자가 링크를 클릭하면 첫 번째 페이지 로드 데이터에서 콘텐츠가 로드됩니다. 주소 표시줄의 URL이 기존 페이지 탐색과 유사하기 때문에 사용자에게 웹 사이트는 예상대로 동작합니다. MunchkinMunchkin 는 사용자가 새 페이지를 로드할 때마다 실행되므로 기존 웹 사이트와 잘 호환됩니다. 그러나 단일 페이지 애플리케이션으로 새 페이지를 로드하지 않는 경우 Munchkin이 한 번만 실행됩니다. 이 게시물에서 다루는 접근 방식은 사용자가 링크를 클릭했을 때를 추적한 다음 이 정보를 Munchkin으로 전송하는 것입니다. `clickLink` Munchkin 함수를 사용하여 이를 구현합니다. 다음은 클릭 이벤트에 대해 `clickLink` Munchkin 메서드에 바인딩하는 jQuery의 예제 구현입니다. `clickLink` Munchkin 메서드를 호출할 때 클릭한 URL에 대한 매개 변수를 전달합니다.

```javascript
<script>
$("a").on('click', function(event) {
    var urlThatWasClicked = $(this).attr('href');
    Munchkin.munchkinFunction('clickLink', { href: urlThatWasClicked});
});
</script>
```

_2015-02-11_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## REST API를 통해 잠재 고객의 점수 변경

API를 사용하여 Marketo에서 잠재 고객의 점수를 변경하려고 한다고 가정해 보겠습니다. 리드 만들기/업데이트 끝점을 사용하여 REST API로 수행할 수 있습니다. 다음은 이 호출을 수행하는 방법을 보여 주는 Ruby의 코드 샘플입니다.

```ruby
require 'rest_client'
require 'json'

# Build request URL
# Replace AAA-BBB-CCC with your Marketo instance
marketo_instance = "https://AAA-BBB-CCC.mktorest.com"
endpoint = "/rest/v1/leads.json"
# Replace with your access token
auth_token =  "?access_token=" + "ac756f7a-d54d-41ac-8c3c-f2d2a39ee325:ab"
request_url = marketo_instance + endpoint + auth_token

# Build request body
data = { "action" => "updateOnly", "input" => [ { "email" => "<example@email.com>", "leadScore" => "30" } ] }

# Make request
response = RestClient.post request_url, data.to_json, :content_type => :json, :accept => :json

# Returns Marketo API response
puts response
```

요청의 JSON 본문에서 `updateOnly`을(를) 작업으로 지정합니다. 즉, 잠재 고객이 존재하는 경우에만 요청이 작동하고, 그렇지 않으면 요청이 실패합니다. 잠재 고객이 없는 경우 잠재 고객을 만들려면 `createOrUpdate`을(를) 작업으로 지정하십시오. 잠재 고객의 이메일을 기본 식별자로 사용하여 Marketo에서 잠재 고객 레코드를 찾습니다. 마지막으로 `leadScore` 키를 사용하여 잠재 고객의 점수 값을 지정합니다. 이 방법을 사용하여 한 번에 300개의 리드를 업데이트하는 것이 가능합니다.

_2015-02-19_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## Marketo Platform을 기반으로 구축된 개방형 Source 프로젝트 강조 표시: 3부

개발자 커뮤니티에 의해 Marketo 플랫폼을 기반으로 빌드된 오픈 소스 프로젝트를 강조 표시하는 지속적인 시리즈 중 세 번째 게시물입니다. Marketo 개발자 커뮤니티에서 만든 클라이언트 라이브러리 및 프로젝트를 추적하는 [Marketo의 GitHub 계정에 있는 목록](https://github.com/Marketo/Community-Supported-Client-Libraries)을 유지 관리합니다. 다음은 Marketo REST API를 중심으로 개발된 세 가지 프로젝트입니다. **[Usermind](http://www.usermind.com/)에서 Marketo REST API에 대한 [Node.js 클라이언트 라이브러리를 만들었습니다](https://github.com/MadKudu/node-marketo).** **[Arunim Samat](https://github.com/asamat)이(가) Marketo REST API용 Python에 [클라이언트 라이브러리를 만들었습니다](https://github.com/asamat/python_marketo).** **[Marketo의 Jacques Lemieux](https://www.linkedin.com/in/jalemieux)에서 Marketo REST API용 Ruby에 [클라이언트 라이브러리를 만들었습니다.](https://github.com/jalemieux/mkto_rest)** Marketo 플랫폼에서 개발자 커뮤니티에 의해 만들어진 더 많은 프로젝트를 보게 되어 기쁘게 생각합니다. Marketo 플랫폼용 오픈 소스 프로젝트를 작업하는 경우 [끌어오기 요청을 통해 이 GitHub 리포지토리에 제출](https://github.com/Marketo/Community-Supported-Client-Libraries)하십시오.

_2015-02-20_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## RTP 캠페인에 Marketo 양식 삽입

많은 마케터가 Marketo Form을 Marketo 실시간 Personalization(RTP) 캠페인에 배치하는 데 관심이 있습니다. 대화 상자, 영역 내 또는 위젯 RTP 캠페인 유형이든 양식 HTML 코드를 복사하여 RTP의 캠페인 편집기에 붙여 넣을 수 있습니다. 이러한 사례는 다음과 같습니다. - 사이트를 두 번째 또는 세 번째 클릭한 후 방문자가 뉴스레터에 등록하도록 하기 - 웨비나를 위한 빠르고 효과적인 등록 양식 - 제어된 사례 연구 다운로드 - 과거에 구독 취소한 리드를 다시 구독하도록 제공 캠페인에서 양식을 작성하고 요청한 감사 또는 콘텐츠를 받아 클릭 수를 한 번 줄여 목표를 달성하는 것입니다. 여기에서는 이렇게 하고 Marketo Form 2.0을 Marketo RTP 캠페인에 포함하는 방법에 대한 설명을 제공합니다. 방문자에게 감사 페이지로 안내하지 않고 한 단계 더 나아간 RTP 사용자가 RTP 캠페인 내에 감사 메시지를 표시하도록 결정한 경우 아래의 좋은 예를 봅니다. 이 옵션의 코드도 아래에 있습니다. 즐기십시오. 귀하의 경험에 대해 알게 되어 기쁩니다!

1. 승인된 양식을 마우스 오른쪽 버튼으로 클릭합니다. **포함 코드 선택**
1. **코드를 복사합니다.**
1. Marketo RTP에서 **캠페인**(으)로 이동합니다.
1. **새 캠페인 만들기**&#x200B;를 클릭합니다.
1. 리치 텍스트 편집기에서 **HTML 아이콘**&#x200B;을 클릭합니다.
1. 양식 포함 코드를 HTML Source 편집기에 붙여넣습니다. **업데이트를 클릭합니다**.
1. 양식이 편집기 보기에 표시되지 않지만, 양식을 미리 보고 캠페인에서 어떻게 렌더링될지 확인할 수 있습니다.
1. 캠페인을 시작하려면 **시작**&#x200B;을 클릭하세요.

### 메모

양식에 대한 모든 변경 사항은 양식 초안 편집에서 Marketo의 마케팅 활동 내에서 수행해야 합니다.

### 관련 문서

* [Forms 2.0](/help/javascript-api/forms-api-reference.md)

_Yanir_&#x200B;이(가) _2015-12-20_&#x200B;에 게시

## Marketo 양식에 재설정 단추 추가

```javascript
<script src="//app-sj01.marketo.com/js/forms2/js/forms2.min.js"></script>
<form id="mktoForm_116"></form>
<script>MktoForms2.loadForm("//app-sj01.marketo.com", "410-XOR-673", 116,
function(form) { form.getFormElem()[0].querySelector('button[type="submit"]').insertAdjacentHTML('afterend','<button type="reset" class="mktoButton">Reset</button>') });
</script>
```

_2015-03-18_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 2015년 3월 릴리스 업데이트

[Marketo REST 자산 API는 2015년 3월 릴리스](https://developer.adobe.com/marketo-apis/api/asset/)에서 릴리스되었습니다. 이 API를 사용하면 Marketo의 파일, 폴더, 토큰, 이메일 및 이메일 템플릿 개체에 액세스할 수 있습니다. 자산 API 엔드포인트에 대한 액세스를 제공하기 위해 읽기 전용 Assets, 읽기-쓰기 Assets, 이렇게 두 개의 역할 권한이 추가되었습니다. API 사용자 역할이 에셋 API 릴리스 이전인 경우 액세스 권한을 활성화하려면 이러한 권한으로 새 API 사용자 역할을 만들어야 합니다. 그렇지 않으면 603 &quot;액세스 거부됨&quot; 오류 응답을 받게 됩니다. REST 자산 API의 릴리스 외에도 기존 REST API 엔드포인트에 대한 업데이트가 있었습니다. [병합 리드 REST API 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST)이(가) 업데이트되어 여러 리드의 병합을 허용합니다. 캠페인을 예약하는 동안 캠페인을 복제할 수 있도록 [Campaign REST API 끝점 예약](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)이(가) 업데이트되었습니다.

_2015-03-23_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 지연으로 RTP 캠페인 트리거

이 사용자 지정 JavaScript을 사용하면 RTP 사용자가 웹 페이지가 로드된 후 몇 초 후에 캠페인을 표시할 수 있습니다. 대화 상자 및 위젯 캠페인에 권장됩니다. 방문자가 페이지에서 일반 콘텐츠를 본 후 지연 후 캠페인을 표시하는 데 사용할 수 있습니다. 캠페인이 표시되어야 하는 특정 페이지에서만 이 코드를 구현하는 것이 좋습니다. 성능에 영향을 줄 수 있으므로 모든 페이지에서 이 코드를 사용하는 것은 권장되지 않습니다. **설정 지침** 사용자 지정 코드는 RTP 사용자 지정 데이터 이벤트(t=timeOnPage, 즉, t=60)를 보낸 다음 이 이벤트와 일치하는 캠페인을 로드합니다. 기본적으로 60초 후에 트리거됩니다. sendCustomRTPEvent 매개 변수를 다른 숫자로 변경하여 사용자 지정할 수 있습니다. 표준 RTP 코드 바로 뒤에 코드를 배치합니다.

```javascript
<script>
function sendCustomRTPEvent(a){
 var eventValue="t="+a;
 setTimeout(function(){
  rtp('send', 'event', {value: eventValue});
  rtp('get', 'campaign',true);
 }, 1000 \* a);
}
sendCustomRTPEvent(60); //Seconds
</script>
```

시간 지연 후에 반응하도록 RTP 캠페인을 설정하려면 다음 작업을 수행하십시오. 1. RTP 계정 1에 로그인합니다. 새 세그먼트 만들기 1. 세그먼트 이벤트 섹션에서 `t=60`을(를) 추가합니다. 방문자는 세션당 각 RTP 세그먼트를 한 번만 일치시킬 수 있으므로 각 캠페인은 한 번만 표시됩니다(고정으로 설정되지 않은 경우).

_Yanir_&#x200B;이(가) _2015-03-24_&#x200B;에 게시

## 2015년 4월 릴리스 업데이트

### Marketo Mobile Engagement SDK v0.3.2

Marketo에는 이제 모바일 앱에 대한 마케팅 자동화 및 사용자 참여가 포함됩니다. iOS 또는 Android 앱에 [Marketo Mobile SDK](/help/mobile/mobile.md)를 설치하면 마케터가 앱 이벤트에서 수신 대기하고 관련 푸시 알림을 보낼 수 있습니다.

### REST API 개선 사항

* 사용자 지정 개체

Marketo 사용자 지정 개체에 있는 데이터를 프로그래밍 방식으로 나열하고 설명하고 CRUD할 수 있는 새로운 [사용자 지정 개체 끝점](/help/rest-api/custom-objects.md)이 도입되었습니다.

사용자 지정 개체 API 엔드포인트에 대한 액세스를 제공하기 위해 역할 권한(읽기 전용 사용자 지정 개체, 읽기-쓰기 사용자 지정 개체)이 추가되었습니다. API 사용자 역할이 사용자 지정 개체 API의 릴리스를 앞둔 경우, 액세스를 활성화하려면 해당 권한으로 새 API 사용자 역할을 만들어야 합니다. 그렇지 않으면 603 &quot;액세스 거부됨&quot; 오류 응답을 받게 됩니다.

* 캠페인 예약 - 프로그램 복제

새로운 선택적 매개 변수 &quot;cloneToProgramName&quot;이 [일정 캠페인 API](/help/rest-api/data-ingestion.md)에 도입되었습니다. 이 매개 변수가 있으면 캠페인의 상위 프로그램이 복제되고 새로 만든 캠페인이 예약됩니다. 매개 변수는 결과 프로그램의 원하는 이름을 지정합니다.

_Travis Kaufman_&#x200B;이(가) _2015-04-28_&#x200B;에 게시함

## 인스턴스 간 이메일 구독 취소 동기화

Marketo의 여러 인스턴스를 관리합니까? 인스턴스 간 리드 정보를 동기화하려면 어려울 수 있습니다. 외부 웹 서비스를 호출하는 웹후크를 사용하여 인스턴스 간에 이메일 구독 취소를 동기화하는 방법입니다. 외부 웹 서비스는 구독 취소 이벤트를 트리거한 알려진 리드를 찾기 위해 각 인스턴스를 반복합니다. 일치하는 리드가 발견되면 해당 리드 레코드의 &quot;구독 취소&quot; 필드가 업데이트됩니다. 여기 그 아이디어를 보여주는 도표가 있다.  웹 서비스를 구현하는 것은 귀하의 책임이지만 아래 코드는 프로세스를 바로 시작하는 데 도움이 될 것입니다!

### 외부 웹 서비스

외부 웹 서비스는 동기화해야 하는 각 Marketo 인스턴스에 대해 다음 단계를 수행합니다.

1. 인스턴스별 REST API [끝점 URL](/help/rest-api/endpoint-reference.md) 구성
1. [ID](/help/rest-api/authentication.md)을(를) 사용하여 액세스 토큰 가져오기
1. [필터 유형별 여러 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 사용하여 이메일 주소와 일치하는 잠재 고객 레코드 목록을 가져옵니다.
1. 리드 만들기/업데이트를 사용하여 각 리드 레코드의 &quot;구독 취소됨&quot; 필드를 업데이트합니다.

다음은 외부 웹 서비스 호출 및 Marketo REST API 호출을 자세히 보여주는 다른 다이어그램입니다.  아래의 샘플 코드는 기본 제공 웹 서비스가 아닙니다. 대신 명령줄을 통해에 인수를 전달할 수 있는 콘솔 모드 프로그램입니다. 여기의 목적은 적절한 Marketo API를 호출하여 인스턴스 간 리드 레코드를 업데이트하는 방법을 보여 주기 위한 것입니다. 웹 서비스 구현은 독자를 위한 연습으로 남겨져 있다.
**샘플 코드** 샘플 코드를 시작하고 실행하려면 즐겨 찾는 IDE에서 Java 프로젝트를 만들어야 합니다. 그 후에는 다음 사항을 변경해야 합니다. 1. 샘플 코드는 [json-simple](https://code.google.com/archive/p/json-simple)을 사용하여 JSON 문자열을 구문 분석합니다. Java 프로젝트에 json-simple jar를 추가합니다. 1. 샘플 코드에는 각 Marketo 인스턴스에 대한 메타데이터를 보유하는 구조가 있습니다. 인스턴스의 실제 값을 다음과 같이 구조에 배치합니다.

```java
public static String instanceInfo[][] = {
{ "AccountId1", "ClientId1","ClientSecret1" },    // Instance 1 metadata
{ "AccountId2", "ClientId2","ClientSecret2" },    // Instance 2 metadata
{ "AccountId3", "ClientId3","ClientSecret3" }     // Instance 3 metadata
};
```

Marketo 관리 패널에서 인스턴스에 대한 메타데이터를 찾을 수 있습니다.

* 계정 ID 관리자 > 통합 > Munchkin > Munchkin 계정
* 클라이언트 Id 및 클라이언트 암호 관리자 > 통합 > LaunchPoint > 이메일 구독 취소 동기화 > 세부 정보 보기

샘플 코드는 위에서 설명한 외부 웹 서비스에 대한 &quot;id&quot; 및 &quot;email&quot; 쿼리 매개 변수를 시뮬레이션하는 두 개의 명령줄 인수를 사용합니다.

1. args[0] = 계정 ID
1. args[1] = 전자 메일 주소

인스턴스의 실제 값을 프로그램에 인수로 전달합니다. 다음은 Intellij IDEA의 프로젝트 구성 스크린샷입니다.

**SyncEmailUnsubscribe.java**

```java
package com.marketo;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;

import javax.net.ssl.HttpsURLConnection;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Iterator;
import java.util.NoSuchElementException;
import java.util.Scanner;

public class SyncEmailUnsubscribe {
    // Define Marketo instance meta data here.
    // Each row contains three elements: Account Id, Client Id, Client Secret.
    // For example:
    //  public static String instanceData[][] = {
    //    {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"},
    //    {"222-BBB-333", "5f4a6657-f6fa-4cd9-4356-123083238821", "gfjgfIVE9h4Jjcl59cOMAKFSk78ut12W"},
    //    {"444-CCC-444", "9f4a4678-f6fa-4dd9-7735-908713247721", "xzcxvbVE9h4Jjcl59cOMAKFSk78ut12W"}
    //  };
    //
    public static String instanceData[][] = {
            // ADD YOUR INSTANCE META DATA HERE
    };

    public static void main(String[] args) {
        String accountId = args[0];     // Account id that processed the unsubscribe
        String emailAddress = args[1];  // Email address of lead that unsubscribed

        SyncEmailUnsubscribe seu = new SyncEmailUnsubscribe();

        // Loop through each Marketo instance
        for (int i = 0; i < instanceData.length; i++) {

            // Make sure we skip instance that triggered the webhook
            if (!accountId.equals(instanceData[i][0])) {
                String endpointUrl = String.format("https://%s.mktorest.com", instanceData[i][0]);

                // Generate access token
                String identityUrl = String.format("%s/identity/oauth/token?grant_type=client_credentials&client_id=%s&client_secret=%s", endpointUrl, instanceData[i][1], instanceData[i][2]);
                String token = seu.getToken(identityUrl);

                // Get lead records for given email address (may be duplicates)
                String getLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s&filterType=email&filterValues=%s", endpointUrl, token, emailAddress);
                String leads = seu.getLeads(getLeadsUrl);

                // Update unsubscribed field in lead record
                String updateLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s", endpointUrl, token);
                seu.updateLeads(updateLeadsUrl, leads, accountId);
            }
        }

        System.exit(0);
    }

    // Call Identity Service to generate access token
    public String getToken(String url) {
        // Call Identity Service
        String tokenData = getData(url);

        // Convert response into JSONObject
        JSONParser parser = new JSONParser();
        Object obj = null;
        try {
            obj = parser.parse(tokenData);
        } catch (ParseException pe) {
            System.out.println("position: " + pe.getPosition());
            System.out.println(pe);
        }

        // Retrieve access_token
        JSONObject jsonObject = (JSONObject)obj;
        return jsonObject.get("access_token").toString();
    }

    // Call Get Multiple Leads by Filter Type Service to get lead records
    public String getLeads(String url) {
        return getData(url);
    }

    // Call Create/Update Lead Service to update "unsubscribed" flag in lead record
    public void updateLeads(String url, String leads, String account) {
        JSONObject body = composeBody(leads, account);
        if (body != null) {
            postData(url, body);
        }
    }

    // Compose JSON body for Create/Update Leads Service
    private JSONObject composeBody(String leads, String account) {
        JSONObject body = new JSONObject();

        // Convert leads into JSONObject
        JSONParser parser = new JSONParser();
        Object obj = null;
        try {
            obj = parser.parse(leads);
        } catch (ParseException pe) {
            System.out.println("position: " + pe.getPosition());
            System.out.println(pe);
        }
        JSONObject leadsObj = (JSONObject)obj;

        Object success = leadsObj.get("success");
        if (success.equals(true)) {
            body.put("action", "updateOnly");
            body.put("lookupField", "id");
            body.put("asyncProcessing", "true");

            // Build array of lead objects
            JSONArray input = new JSONArray();
            JSONArray result = (JSONArray) leadsObj.get("result");
            Iterator<JSONObject> iterator = result.iterator();
            while (iterator.hasNext()) {
                JSONObject leadIn = (JSONObject)iterator.next();
                JSONObject lead = new JSONObject();
                lead.put("id", leadIn.get("id"));
                lead.put("unsubscribed", "true");
                lead.put("unsubscribedReason", "Cross instance synch triggered by webhook from: " + account);
                input.add(lead);
            }

            body.put("input", input);
        }
        return body;
    }

    // HTTP POST request
    private String postData(String endpoint, JSONObject body) {
        String data = "";
        try {
            // Make request
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("POST");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            urlConn.setRequestProperty("Content-type", "application/json");
            urlConn.setRequestProperty("accept", "application/json");
            urlConn.connect();
            OutputStream os = urlConn.getOutputStream();
            os.write(body.toJSONString().getBytes());
            os.close();
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                System.out.println("Status: 200");
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
                System.out.println(data);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    // HTTP GET request
    private String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                System.out.println("Status: 200");
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
                System.out.println(data);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

### Marketo 설정

동기화할 각 Marketo 인스턴스에 대해 다음 단계를 수행합니다.

1. 리드 읽기-쓰기 역할 권한으로 사용자 정의 서비스를 만듭니다. 사용자 지정 서비스 만들기에 익숙하지 않은 경우 [여기](/help/rest-api/custom-services.md)를 클릭하세요.
1. 외부 웹 서비스를 호출하는 웹후크를 만듭니다. 웹후크 만들기에 익숙하지 않은 경우 [여기](/help/webhooks/webhooks.md)를 클릭하세요.
1. Smart Campaign에서 흐름 단계로 Webhook을 추가합니다.

아래 스크린샷은 토큰을 사용하여 위에 지정된 서비스를 호출하는 웹후크를 생성하여 쿼리 매개 변수를 자동으로 채우는 방법을 보여 줍니다. 이제 웹후크를 만들었으므로 흐름 작업으로 Smart Campaign에 추가할 수 있습니다.  스마트 목록에는 &quot;전자 메일에서 구독 취소&quot; 트리거가 포함되어야 합니다.

### 유효성 검사

이 모든 것을 테스트하려면 여러 Marketo 인스턴스에서 동일한 이메일 주소로 리드를 만듭니다. 이메일 주소를 소유하고 있는지 확인하십시오! 한 인스턴스에서 이메일 흐름 보내기 작업을 트리거하고 결과 이메일을 열고 구독 취소를 클릭합니다. 결과를 확인하려면 다른 각 인스턴스에 로그인하고 이메일 주소와 연결된 잠재 고객 레코드를 검사하십시오. &quot;구독 취소됨&quot; 확인란을 선택하고 &quot;구독 취소됨 사유&quot; 필드에는 동기화를 시작한 소스 계정 ID가 포함된 메모가 있어야 합니다.

_David_&#x200B;이(가) _2015-05-11_&#x200B;에 게시함

## REST API를 사용하여 리드 데이터 변경 동기화

해당 게시물에는 업데이트를 위해 Marketo을 폴링하기 위해 반복적으로 실행할 수 있는 코드 샘플이 표시되었습니다. 아이디어는 Marketo API를 사용하여 잠재 고객 데이터의 변경 사항을 식별하고 변경된 잠재 고객 데이터를 추출하는 것이었습니다. 그런 다음 이 데이터를 동기화 목적으로 외부 시스템에 푸시할 수 있습니다. 제공된 코드 샘플은 SOAP API를 사용했습니다. [새로운 걷는 방법](https://www.youtube.com/watch?v=G-7ZJjLy5D8&feature=youtu.be)이 있으며, [Marketo REST API](/help/rest-api/rest-api.md)를 사용합니다. 이 게시물은 두 개의 REST 끝점을 사용하여 동일한 목표를 달성하는 방법을 보여 줍니다. [잠재 고객 변경 가져오기](/help/rest-api/rest-api.md), [ID로 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET). 프로그램에는 다음 두 가지 주요 단계가 포함되어 있습니다.

1. Get Lead Changes 를 호출하여 특정 리드 필드가 변경되었거나 주어진 기간 동안 추가된 모든 리드 ID 목록을 생성합니다.
1. 목록에서 각 리드 ID에 대한 리드 ID 가져오기 를 호출하여 리드 레코드에서 필드 데이터를 검색합니다.

2단계에서 검색된 데이터를 외부 시스템에서 사용할 수 있도록 포맷합니다.  **프로그램 입력** 기본적으로 프로그램은 변경 내용을 찾기 위해 현재 날짜로부터 하루 후에 &quot;뒤로&quot; 이동합니다. 따라서 이 프로그램을 매일 같은 시간에 실행할 수 있습니다. 시간을 거슬러 올라가기 위해 일 수를 명령줄 인수로 지정하여 시간 창을 효과적으로 늘릴 수 있습니다. 프로그램에는 수정할 수 있는 여러 변수가 포함되어 있습니다. CUSTOM_SERVICE_DATA - 여기에는 Marketo [사용자 지정 서비스](/help/rest-api/custom-services.md) 데이터(계정 ID, 클라이언트 ID, 클라이언트 암호)가 포함되어 있습니다. LEAD_CHANGE_FIELD_FILTER - 변경 사항을 검사할 Lead 필드를 쉼표로 구분한 목록이 들어 있습니다. READ_BATCH_SIZE - 한 번에 검색할 레코드 수입니다. 이 옵션을 사용하여 본문 크기에 대한 응답을 조정합니다. **프로그램 출력** 프로그램은 변경된 리드 레코드를 모두 수집하고 다음과 같이 리드 오브젝트 배열로 JSON에 포맷합니다.

```json
{
    "result": [
        {
            "leadId": "318592",
            "updatedAt": "2015-07-22T19:19:07Z",
            "firstName": "David",
            "lastName": "Everly",
            "email": "<deverly@marketo.com>"
        },

        ...more lead objects here...
    ]
}
```

그런 다음 이 JSON을 외부 웹 서비스에 요청 페이로드로 전달하여 데이터를 동기화할 수 있다는 이점이 있습니다. **프로그램 논리** 먼저 시간 창을 설정하고, REST 끝점 URL을 구성하고, 인증 액세스 토큰을 얻습니다. 다음으로 잠재 고객 변경 공급량을 소진할 때까지 실행되는 페이징 토큰 가져오기/잠재 고객 변경 사항 가져오기 루프를 실행합니다. 이 루프의 목적은 고유한 잠재 고객 ID 목록을 누적하여 나중에 프로그램에서 ID로 잠재 고객 가져오기 로 전달할 수 있도록 하는 것입니다. 이 예에서는 잠재 고객 변경 사항 가져오기에 대해 firstName, lastName, email 필드에 대한 변경 사항을 확인하겠습니다. 목적에 맞는 필드 조합을 자유롭게 선택할 수 있습니다. Get Lead Changes는 결과를 필터링하는 데 사용할 수 있는 활동 유형 ID가 포함된 &quot;result&quot; 개체를 반환합니다. 참고: [활동 유형 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getAllActivityTypesUsingGET) REST 끝점을 호출하여 활동 유형 목록을 가져올 수 있습니다. 반환된 2개의 활동 유형(1)에 관심이 있습니다. 새 잠재 고객 (12)

```json
{
    "id": 12024682,
    "leadId": 318581,
    "activityDate": "2015-03-17T00:18:41Z",
    "activityTypeId": 12,
    "primaryAttributeValueId": 318581,
    "primaryAttributeValue": "David Everly",
    "attributes": [
        {
            "name": "Created Date",
            "value": "2015-03-16"
        },
        {
            "name": "Source Type",
            "value": "New lead"
        }
    ]
}
```

1. 변경 데이터 값 (13) 변경 데이터 값 응답에서 &quot;name&quot; 속성을 검사하여 변경된 필드를 파악할 수 있습니다.

```json
{
    "id": 12024689,
    "leadId": 318581,
    "activityDate": "2015-03-17T22:58:18Z",
    "activityTypeId": 13,
    "fields": [
        {
            "id": 31,
            "name": "lastName",
            "newValue": "Evely",
            "oldValue": "Everly"
        }
    ],
    "attributes": [
        {
            "name": "Source",
            "value": "Web form fillout"
        }
    ]
}
```

이 두 가지 유형의 활동 중 하나가 반환되면 연결된 리드 ID가 목록에 저장됩니다. 목록이 준비되면 각 항목에 대한 Id별 리드 가져오기를 호출하여 반복할 수 있습니다. 목록의 각 리드에 대한 최신 리드 데이터를 검색합니다. 이 예제에서는 `leadId`, `updatedAt`, `firstName`, `lastName` 및 `email` 리드 필드를 검색합니다. 목적에 맞는 필드 조합을 자유롭게 선택할 수 있습니다. 이 작업은 ID로 잠재 고객을 가져오기 위해 필드 매개 변수를 지정하여 수행합니다. 그리고 마지막으로 위에 설명된 대로 결과를 리드 오브젝트의 배열로 JSONify합니다.

**프로그램 코드**

```java
package com.marketo;

// minimal-json library (<https://github.com/ralfstx/minimal-json>)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;
import com.eclipsesource.json.JsonValue;

import java.io.\*;
import java.net.MalformedURLException;
import java.net.URL;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.\*;

import javax.net.ssl.HttpsURLConnection;

public class LeadChanges {
    //
    // Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    //    public static String CUSTOM_SERVICE_DATA[] =
    //      {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"};
    //
    private static final String CUSTOM_SERVICE_DATA[] =
            {INSERT YOUR CUSTOM SERVICE DATA HERE};

    // Lead fields that we are interested in
    private static final String LEAD_CHANGE_FIELD_FILTER = "firstName,lastName,email";

    // Number of lead records to read at a time
    private static final String READ_BATCH_SIZE = "200";

    // Activity type ids that we are interested in
    private static final int ACTIVITY_TYPE_ID_NEW_LEAD = 12;
    private static final int ACTIVITY_TYPE_ID_CHANGE_DATA_VALE = 13;

    public static void main(String[] args) {
        // Command line argument to set how far back to look for lead changes (number of days)
        int lookBackNumDays = 1;
        if (args.length == 1) {
            lookBackNumDays = Integer.parseInt(args[0]);
        }

        // Establish "since date" using current timestamp minus some number of days (default is 1 day)
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DAY_OF_MONTH, -lookBackNumDays);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String sinceDateTime = sdf.format(cal.getTime());

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
                CUSTOM_SERVICE_DATA[0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[1], CUSTOM_SERVICE_DATA[2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(getData(identityUrl));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URLs for Get Lead Changes, and Get Paging Token
        String leadChangesUrl = String.format("%s/rest/v1/activities/leadchanges.json?access_token=%s&fields=%s&batchSize=%s",
                baseUrl, accessToken, LEAD_CHANGE_FIELD_FILTER, READ_BATCH_SIZE);
        String pagingTokenUrl = String.format("%s/rest/v1/activities/pagingtoken.json?access_token=%s&sinceDatetime=%s",
                baseUrl, accessToken, sinceDateTime);

        HashSet leadIdList = new HashSet();

        // Call Get Paging Token API
        JsonObject pagingTokenObj = JsonObject.readFrom(getData(pagingTokenUrl));
        if (pagingTokenObj.get("success").asBoolean()) {

            String nextPageToken = pagingTokenObj.get("nextPageToken").asString();
            boolean moreResult;

            do {
                moreResult = false;

                // Call Get Lead Changes API
                JsonObject leadChangesObj = JsonObject.readFrom(getData(String.format("%s&nextPageToken=%s",
                        leadChangesUrl, nextPageToken)));
                if (leadChangesObj.get("success").asBoolean()) {
                    moreResult = leadChangesObj.get("moreResult").asBoolean();
                    nextPageToken = leadChangesObj.get("nextPageToken").asString();

                    if (leadChangesObj.get("result") != null) {
                        JsonArray resultAry = leadChangesObj.get("result").asArray();
                        for (JsonValue resultObj : resultAry) {
                            int activityTypeId = resultObj.asObject().get("activityTypeId").asInt();


                            // Store lead ids for later use
                            boolean storeThisId = false;
                            if (activityTypeId == ACTIVITY_TYPE_ID_NEW_LEAD) {
                                storeThisId = true;
                            } else if (activityTypeId == ACTIVITY_TYPE_ID_CHANGE_DATA_VALE) {
                                // See if any of the changed fields are of interest to us
                                JsonArray fieldsAry = resultObj.asObject().get("fields").asArray();
                                for (JsonValue fieldsObj : fieldsAry) {
                                    String name = fieldsObj.asObject().get("name").asString();
                                    if (LEAD_CHANGE_FIELD_FILTER.contains(name)) {
                                        storeThisId = true;
                                    }
                                }

                            }

                            if (storeThisId) {
                                leadIdList.add(resultObj.asObject().get("leadId").toString());
                            }
                        }
                    }
                }

            } while (moreResult);
        }

        JsonObject result = new JsonObject();
        JsonArray leads = new JsonArray();

        for (Object o : leadIdList) {
            String leadId = o.toString();

            // Compose Get Lead by Id URL
            String getLeadUrl = String.format("%s/rest/v1/lead/%s.json?access_token=%s",
                    baseUrl, leadId, accessToken);

            // Call Get Lead by Id API
            JsonObject leadObj = JsonObject.readFrom(getData(getLeadUrl));
            if (leadObj.get("success").asBoolean()) {
                if (leadObj.get("result") != null) {
                    JsonArray resultAry = leadObj.get("result").asArray();
                    for (JsonValue resultObj : resultAry) {

                        // Create lead object
                        JsonObject lead = new JsonObject();
                        lead.add("leadId", leadId);
                        lead.add("updatedAt", resultObj.asObject().get("updatedAt").asString());
                        lead.add("firstName", resultObj.asObject().get("firstName").asString());
                        lead.add("lastName", resultObj.asObject().get("lastName").asString());
                        lead.add("email", resultObj.asObject().get("email").asString());

                        // Add lead object to leads array
                        leads.add(lead);
                    }
                }
            }
        }

        // Add leads array to result object
        result.add("result", leads);

        // Print out result object
        System.out.println(result);

        System.exit(0);
    }

    // Perform HTTP GET request
    private static String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

[즐거운 노래](https://www.youtube.com/watch?v=zFaBwZDywLk)입니다. 맛있게 드십시오!

_David_&#x200B;이(가) _2015-07-31_&#x200B;에 게시함

## 2015년 5월 릴리스 업데이트

### REST API

* 영업 기회 API. Marketo 영업 기회 개체 내에 있는 데이터를 프로그래밍 방식으로 나열하고 설명하고 CRUD할 수 있는 새로운 [영업 기회 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Opportunities)이 도입되었습니다.

참고: Opportunity 엔드포인트에 대한 액세스 권한을 제공하기 위해 역할 권한 (읽기 전용 Opportunity, 읽기-쓰기 Opportunity)이 추가되었습니다. API 사용자 역할이 Opportunity API 의 릴리스 이전인 경우 액세스를 활성화하려면 이러한 권한으로 새 API 사용자 역할을 만들어야 합니다. 그렇지 않으면 603 &quot;액세스 거부됨&quot; 오류 응답을 받게 됩니다.

* 자산 API - 코드 조각. 코드 조각 개체를 프로그래밍 방식으로 조작할 수 있도록 코드 조각에 대한 [자산 끝점](https://developer.adobe.com/marketo-apis/api/asset/#snippet_endpoints)이 새로 도입되었습니다. 스니펫은 이메일 및 랜딩 페이지에서 동적 콘텐츠 블록으로 사용할 수 있습니다.
* 리드 API - 리드 파티션 업데이트. 하나 이상의 리드에 대해 파티션을 업데이트할 수 있도록 파티션에 대한 [리드 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updatePartitionsUsingPOST)이 새로 추가되었습니다.
* &quot;createdAt&quot; 및 &quot;updatedAt&quot; 속성에서 리드 관련 API에 시간대 오프셋이 누락되었던 문제가 수정되었습니다.
* 일일 최대 호출 수를 초과하면 일정 캠페인이 적절한 오류 코드를 반환하지 않는 문제가 해결되었습니다.
* Id별 폴더 가져오기에서 &quot;상위&quot; 및 &quot;설명&quot; 속성에 대해 때때로 null을 반환하는 문제가 해결되었습니다.
* ID로 이메일 승인을 수행하면 특정 경우에 시스템 오류가 발생하는 문제가 해결되었습니다.
* 폴더 ID로 토큰 만들기 가 특정 경우에 사용할 수 없었던 토큰을 생성하는 문제를 수정했습니다.

### 실시간 Personalization(RTP)

* 리치 미디어 추천 API. 새 [리치 미디어 권장 사항](/help/javascript-api/web-personalization.md) 기능이 RTP JavaScript API에 추가되었습니다. 리치 미디어 콘텐츠 권장 사항은 웹 방문자를 머신 러닝 및 예측 분석을 통해 제공되는 가장 관련성이 높은 콘텐츠로 참여하게 합니다. 텍스트 설명 및 이미지로 콘텐츠 에셋을 개선하고 웹 사이트에 여러 콘텐츠 권장 사항을 임베드합니다.

### Mobile Engagement SDK

iOS v0.3.4/Android v0.3.3

* 사용자 지정 작업. 사용자 지정 작업을 전송하여 사용자 상호 작용을 추적하는 기능이 추가되었습니다. 자세한 내용은 &quot;사용자 지정 작업 보내기&quot; [여기](/help/mobile/mobile.md)를 참조하십시오.
* trackPushNotification 메서드는 더 이상 사용되지 않습니다.

_David_&#x200B;이(가) _2015-05-26_&#x200B;에 게시함

## 2015년 6월 릴리스 업데이트

### REST API

* 회사 API

Marketo 회사 개체 내에 있는 데이터를 프로그래밍 방식으로 나열하고 설명하고 CRUD할 수 있는 새 [회사 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Companies)이 도입되었습니다.

참고: 프로그램 엔드포인트에 대한 액세스 권한을 제공하기 위해 역할 권한(읽기 전용 회사, 읽기-쓰기 회사)이 추가되었습니다. API 사용자 역할이 회사 API의 릴리스보다 이전인 경우 액세스를 활성화하려면 해당 권한으로 API 사용자 역할을 업데이트해야 합니다. 그렇지 않으면 603 &quot;액세스 거부됨&quot; 오류 응답을 받게 됩니다

* 자산 API - 프로그램

애플리케이션 폴더와 프로그램 폴더를 모두 지원하도록 자산 API가 업데이트되었습니다. 여러 자산 API가 정수 형식으로 요청에서 폴더 ID를 수락했습니다. 폴더 ID는 API에 따라 URI의 일부 또는 요청 본문의 일부로 전달될 수 있습니다.

이제 폴더 ID와 함께 폴더 유형을 지정해야 합니다. 폴더 유형은 &quot;Program&quot; 또는 &quot;Folder&quot;입니다. &quot;Folder&quot;는 응용 프로그램 폴더를 지정하는 반면, &quot;Program&quot;은 프로그램 폴더를 지정합니다. 폴더 유형은 호출하는 API에 따라 두 가지 방법으로 지정됩니다.

1. &quot;FolderIdType&quot; 데이터 구조를 사용합니다. FolderIdType은 다음과 같이 ID 및 유형 쌍을 포함하는 간단한 JSON 블록입니다.

`{ "id" : **id**, "type" : "**type**" }`

여기서 **id**&#x200B;은(는) 폴더 ID이고 &quot;**type**&quot;은(는) 폴더 유형입니다. &quot;**type**&quot;에 허용되는 값은 &quot;Folder&quot; 또는 &quot;Program&quot;입니다.

예제 - 폴더 만들기

`POST /asset/v1/folders.json`

`parent={"id":416,"type":"Folder"}&name=Test Folder&description=This is a test folder`

1. 기존 id 매개 변수를 사용하고 &quot;type&quot; 쿼리 매개 변수를 사용하여 형식을 지정합니다.

예 - Id로 폴더 가져오기

`GET /rest/asset/v1/folder/1016.json?type=Program`

이제 결과 개체에 폴더 ID가 들어 있던 모든 API 응답에는 값이 FolderIdType인 folderId 속성도 포함됩니다. 이 값은 주어진 폴더 ID에 대한 폴더 유형을 결정하는 데 사용할 수 있습니다.

예 - 이름별 폴더 가져오기

`GET /rest/asset/v1/folder/byName.json?name=Social Media`

```json
"result": [
{
...

"folderId": {"id":341, "type": "Program"},
...

"id":"341"
}
]
```

특정 ID의 폴더 유형을 확인하려면 [폴더 찾아보기](https://developer.adobe.com/marketo-apis/api/asset/browse-folders/) API를 사용할 수 있습니다.

API 응답의 &quot;type&quot; 특성 이름이 &quot;folderType&quot;으로 변경되었습니다. 이는 FolderIdType에 포함된 &quot;type&quot; 요소와의 혼동을 방지하기 위한 것입니다.

예를 들어, 다음에서:

&quot;**type**&quot;:&quot;마케팅 폴더&quot;

아래와 같이 변경하는 것을 의미합니다.

&quot;**folderType**&quot;: &quot;마케팅 폴더&quot;

### Mobile Engagement SDK

iOS 0.3.5

* 주 스레드에서 테스트 장치 설정 대화 상자가 실행되고 있던 문제를 해결했습니다. [MOB-638]
* 테스트 장치 등록 실패 시 오류 처리가 추가되었습니다. [MOB-639]

Android 0.3.3

* 테스트 장치를 추가하고 방향을 변경했을 때 진행 대화 상자가 해제되지 않도록 AndroidManifest.xml :configChanges 요소에 android`<activity>` 특성이 추가되었습니다. [MOB-687]

_David_&#x200B;이(가) _2015-06-30_&#x200B;에 게시함

## RTP API를 사용하는 인앱 웹 Personalization(Beta)

일부 고객은 사용자를 위한 웹 앱 솔루션을 제공하며 보안 웹 앱 환경 내에서 Marketo 실시간 Personalization(RTP)를 사용할 수 있는 경우 요청을 받습니다. 대답은 &#39;예&#39;입니다. 인앱 메시징을 위한 API가 릴리스되었으므로 콘텐츠를 개인화하고 웹 앱 데이터를 기반으로 웨비나, 새로운 기능 릴리스, 상향 판매 및 사용자 참여와 같은 마케팅 활동을 홍보할 수 있습니다. 예를 들어 다음에 대한 인앱 콘텐츠 개인화:

* 사용자 활동을 기반으로 한 평가판 오퍼
* 다양한 구독 유형(상향 판매, 교차 판매 또는 웨비나 교육)
* 사용자 활동과 관련된 새로운 기능

**사용 사례 예** Marketo의 고객 성공 팀은 인앱 웹 Personalization을 사용하여 특정 구독 유형(Spark, Standard, Select 또는 Enterprise)과 개인화된 콘텐츠로 통신하므로, 진행 중인 캠페인을 보고 참여를 기반으로 인앱 사용자를 육성할 수 있습니다. Enterprise 구독 유형을 가진 사용자에 대해 이 작업을 수행하는 방법을 살펴보겠습니다. **필수 구성 요소** [RTP 사용자 컨텍스트 API 이해](/help/javascript-api/web-personalization.md). RTP 계정에 대한 사용자 컨텍스트 API를 활성화하려면 **Marketo 지원에서 사용자 컨텍스트 API를 활성화** 요청을 사용하십시오. **사용자 지정 변수 설정** RTP에서 데이터를 보낼 수 있는 사용자 지정 변수 슬롯이 5개 있습니다. 이 예에서는 사용자 구독 유형 Enterprise를 사용자 지정 변수 1로 보냅니다.

`rtp('set', 'customVar1', 'Enterprise');`

**새 RTP 세그먼트 만들기** **세그먼트**(으)로 이동하여 **새로 만들기**&#x200B;를 클릭합니다.

1. **사용자 컨텍스트 API** 필터를 세그먼트 빌더로 끌어옵니다.
1. **값**&#x200B;이(가) **Enterprise**&#x200B;인 **사용자 지정 변수 1**(구독 유형)을 선택하세요.

**이전 방문 기록을 기반으로 한 캠페인 표시** 방문자가 이전 방문에서 이미 캠페인을 클릭한 경우 다른 캠페인을 표시합니다.

1. **사용자 컨텍스트 API** 내에서 **(+)**&#x200B;을(를) 클릭하여 다른 사용자 컨텍스트 API 특성을 추가하십시오
1. **연산자(AND 또는 OR)를 추가합니다.**
1. **캠페인 - 클릭함 선택.** **캠페인 ID**&#x200B;을(를) 캠페인 ID로 설정합니다. ( 캠페인 ID를 찾는 방법은 아래 참고 사항을 참조하십시오.)
1. 캠페인 크리에이티브를 만들려면 **캠페인 저장 및 정의**&#x200B;를 클릭하세요.

전반적으로, 이 세그먼트는 방문자가 Enterprise와 같은 사용자 지정 변수(구독 유형)와 연결되어 있고 이전 방문에서 캠페인(ID: 5390)을 클릭한 경우 일치합니다. 다음 단계는 이 세그먼트에 대한 개인화된 캠페인을 정의하는 것입니다. 아래 스크린샷은 엔터프라이즈 사용자를 위한 웨비나를 홍보하는 내 Marketo 페이지에 나타나는 RTP 대화 상자 캠페인(왼쪽 하단)을 보여 줍니다.  **참고:** **캠페인 ID 찾기** **캠페인**(으)로 이동한 다음 **캠페인 이름** 위로 마우스를 가져가면 캠페인 ID를 찾을 수 있습니다.
_David_&#x200B;이(가) _2015-06-17_&#x200B;에 게시함

## Marketo REST API를 사용하여 트랜잭션 이메일 보내기: 1부

Marketo REST API를 사용하여 필요한 호출을 실행하기 위한 Marketo 내에는 몇 가지 구성 요구 사항이 있습니다.

* 수신자는 Marketo 내에 레코드가 있어야 합니다.
* Marketo 인스턴스에서 만들고 승인한 트랜잭션 이메일이 있어야 합니다.
* 이메일을 보내도록 설정된 Source: 웹 서비스 API인 캠페인이 요청됨 상태의 활성 트리거 캠페인이 있어야 합니다

먼저 [전자 메일을 만들고 승인](https://experienceleague.adobe.com/ko/docs/marketo/using/home)하세요. 이메일이 실제로 트랜잭션된 경우, 이를 작동 상태로 설정해야 하지만 적법하게 작동 가능한지 확인해야 합니다. 이는 이메일 작업 > 이메일 설정 아래의 편집 화면에서 구성됩니다. 승인하면 캠페인을 만들 준비가 되었습니다. 캠페인을 처음 만드는 경우 docs.marketo.com에서 [새 스마트 캠페인 만들기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/creating-a-smart-campaign/create-a-new-smart-campaign) 문서를 확인하십시오. 캠페인을 만든 후에는 다음 단계를 수행해야 합니다. Campaign이 요청한 트리거를 사용하여 스마트 목록 구성: 이제 이메일을 보내기 단계를 가리키도록 흐름을 구성해야 합니다. 활성화하기 전에 예약 탭에서 일부 설정을 결정해야 합니다. 이 특정 이메일을 지정된 레코드로 한 번만 전송해야 하는 경우 자격 설정을 그대로 둡니다. 그러나 이메일을 여러 번 받아야 하는 경우 매번 또는 사용 가능한 케이던스 중 하나로 조정할 수 있습니다. 이제 활성화할 준비가 되었습니다.

### API 호출 전송

**참고:** 아래 Java 예제에서는 최소 JSON 패키지를 사용하여 코드에서 JSON 표현을 처리하고 있습니다. 이 프로젝트에 대한 자세한 내용은 [https://github.com/ralfstx/minimal-json](https://github.com/ralfstx/minimal-json)에서 확인할 수 있습니다. API를 통해 트랜잭션 전자 메일을 보내는 첫 번째 부분은 해당 전자 메일 주소가 있는 레코드가 Marketo 인스턴스에 있는지, 그리고 해당 리드 ID에 액세스할 수 있는지 확인하는 것입니다. 이 게시물의 목적상 이메일 주소가 이미 Marketo에 있으며 레코드의 ID만 검색하면 된다고 가정합니다. 이를 위해 [필터 유형별 다중 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET) 호출을 사용하고 있으며 이전 게시물의 일부 Java 코드를 재사용하고 있습니다. 캠페인을 요청하기 위한 의 주요 방법을 살펴보겠습니다.

```java
package dev.marketo.blog_request_campaign;

import com.eclipsesource.json.JsonArray;

public class App
{
    public static void main( String[] args )
    {
     //Create an instance of Auth so that we can authenticate with our Marketo instance
        Leads leadsRequest = new Leads(auth).setFilterType("email").addFilterValue("<requestCampaign.test@marketo.com>");

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

leadsRequest 의 JsonObject 응답에서 이러한 결과를 얻으려면 몇 가지 코드를 작성해야 합니다. Array에서 첫 번째 결과를 검색하려면 JsonObject에서 Array를 추출하고 0에서 개체를 인덱싱해야 합니다.

`JsonArray leadsResult = leadsRequest.getData().get("result").asArray();`
`int leadId = leadsResult.get(0).asObject().get("id").asInt();`

여기서부터 Request Campaign 호출만 하면 됩니다. 이를 위해 필수 매개 변수는 요청의 URL에 있는 ID와 하나의 멤버인 &quot;id&quot;가 포함된 JSON 개체의 배열입니다. 이에 대한 코드를 살펴보겠습니다.

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
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   System.out.println("Executing RequestCampaign calln" + "Endpoint: " + s + "nRequest Body:n"  + requestBody);
   URL url = new URL(s);
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
   System.out.println("Result:n" + result);
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

이 클래스에는 인증을 받는 생성자 1명과 캠페인 ID가 있습니다. setLeads에 대한 레코드의 ID가 포함된 ArrayList `<Integer>`을(를) 전달하거나 addLead를 사용하여 개체에 Leads를 추가합니다. addLead는 정수 하나를 사용하여 Leads 속성의 기존 ArrayList에 추가합니다. 리드 레코드를 캠페인에 전달하기 위해 API 호출을 트리거하려면 요청의 응답 데이터가 포함된 JsonObject를 반환하는 postData를 호출해야 합니다. 요청 캠페인이 호출되면 호출에 전달된 모든 리드는 Marketo의 Target 트리거 캠페인에 의해 처리되고 이전에 만든 이메일로 전송됩니다. 축하합니다. Marketo REST API를 통해 이메일을 트리거했습니다. 요청 캠페인을 통해 이메일 콘텐츠를 동적으로 사용자 지정하는 2부를 살펴보십시오.

_케니_&#x200B;이(가) _2015-07-17_&#x200B;에 게시함

## REST API를 사용하여 Marketo에서 리드 데이터 인증 및 검색

**참고:** 아래 Java 예제에서는 최소 JSON 패키지를 사용하여 코드에서 JSON 표현을 처리하고 있습니다. 이 프로젝트에 대한 자세한 내용은 [https://github.com/ralfstx/minimal-json](https://github.com/ralfstx/minimal-json)에서 확인할 수 있습니다. Marketo과 통합할 때 가장 일반적인 요구 사항 중 하나는 리드 데이터를 검색하는 것입니다. 대부분의 경우 모든 통합에서 Marketo 구독의 잠재 고객 데이터를 검색하거나 제출해야 하는 것은 아니므로, 이제 구독을 사용하여 [인증](/help/rest-api/authentication.md)한 다음 해당 구독에서 잠재 고객 데이터를 검색하는 기본 잠재 고객 정보 검색 작업을 살펴보겠습니다. 리드를 검색하려면 먼저 OAuth 2.0을 사용하여 대상 Marketo 인스턴스를 인증해야 합니다. Marketo, 클라이언트 ID, 클라이언트 암호 및 Marketo 인스턴스의 호스트를 사용하여 인증해야 하는 세 가지 정보가 있습니다. 다음은 인증에 사용하는 클래스입니다.

```java
package dev.marketo.blog_leads;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonObject;

public class Auth {
 protected String marketoInstance; //Instance Host obtained from Admin -> Web Service
 private String clientId; //clientId obtained from Admin -> Launchpoint -> View Details for selected service
 private String clientSecret; //clientSecret obtained from Admin -> Launchpoint -> View Details for selected service
 private String idEndpoint; //idEndpoint constructed to authenticate with service when constructor is used
 private String token; //token is stored for reuse until expiration
 private Long expiry; //used to store time of expiration

 //Creates an instance of Auth which is used to Authenticate with a particular service on a particular instance
 public Auth(String id, String secret, String instanceUrl) {
  this.clientId = id;
  this.clientSecret = secret;
  this.marketoInstance = instanceUrl;
  this.idEndpoint = marketoInstance + "/identity/oauth/token?grant_type=client_credentials&client_id=" + clientId + "&client_secret=" + clientSecret;
 }
 //The only public method of Auth, used to check if the current value of Token is valid, and then to retrieve a new one if it is not
 public String getToken(){
  long now  = System.currentTimeMillis();
  if (expiry == null || expiry < now){
   System.out.println("Token is empty or expired. Trying new authentication");
   JsonObject jo = getData();
   System.out.println("Got Authentication Response: " + jo);
   this.token = jo.get("access_token").asString();
                        //expires_in is reported as seconds, set expiry to system time in ms + expires \* 1000
   this.expiry = System.currentTimeMillis() + (jo.get("expires_in").asLong() \* 1000);
  }
  return this.token;
 }
 //Executes the authentication request
 private JsonObject getData(){
  JsonObject jsonObject = null;
  try {
   URL url = new URL(idEndpoint);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
   urlConn.setRequestMethod("GET");
            urlConn.setRequestProperty("accept", "application/json");
            System.out.println("Trying to authenticate with " + idEndpoint);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                Reader reader = new InputStreamReader(inStream);
                jsonObject = JsonObject.readFrom(reader);
            }else {
                throw new IOException("Status: " + responseCode);
            }
  } catch (MalformedURLException e) {
   e.printStackTrace();
  }catch (IOException e) {
            e.printStackTrace();
        }
  return jsonObject;
 }
}
```

이 코드를 사용하면 [관리] -> [실행 지점] (ID 및 암호) 및 [관리] -> [웹 서비스] (호스트)에서 클라이언트 ID, 클라이언트 암호 및 호스트(marketoInstance로서)로 인증 인스턴스를 만들 수 있습니다. 현재 저장된 토큰이 null인지 또는 만료되었는지 테스트한 다음 기존 토큰을 반환하거나 새 인증 요청을 수행한 다음 JSON 응답의 &quot;access_token&quot; 멤버에서 새 토큰을 반환하는 getToken 메서드를 표시합니다. 이제 Marketo 인스턴스를 인증할 수 있으므로 다음 단계는 리드를 검색하는 것입니다. 이 클래스를 사용하고 있습니다.

```java
package dev.marketo.blog_leads;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import javax.net.ssl.HttpsURLConnection;
import com.eclipsesource.json.JsonObject;

public class Leads {
 private StringBuilder endpoint;
 private Auth auth;
 public String filterType;
 public ArrayList filterValues = new ArrayList();
 public Integer batchSize;
 public String nextPageToken;
 public ArrayList fields = new ArrayList();

 public Leads(Auth a) {
  this.auth = a;
  this.endpoint = new StringBuilder(this.auth.marketoInstance + "/rest/v1/leads.json");
 }
 public Leads setFilterType(String filterType) {
  this.filterType = filterType;
  return this;
 }
 public Leads setFilterValues(ArrayList filterValues) {
  this.filterValues = filterValues;
  return this;
 }
 public Leads addFilterValue(String filterVal) {
  this.filterValues.add(filterVal);
  return this;
 }
 public Leads setBatchSize(Integer batchSize) {
  this.batchSize = batchSize;
  return this;
 }
 public Leads setNextPageToken(String nextPageToken) {
  this.nextPageToken = nextPageToken;
  return this;
 }
 public Leads setFields(ArrayList fields) {
  this.fields = fields;
  return this;
 }

 public JsonObject getData() {
        JsonObject result = null;
        try {
         endpoint.append("?access_token=" + auth.getToken() + "&filterType=" + filterType + "&filterValues=" + csvString(filterValues));
         if (batchSize != null && batchSize > 0 && batchSize <= 300){
             endpoint.append("&batchSize=" + batchSize);
            }
            if (nextPageToken != null){
             endpoint.append("&nextPageToken=" + nextPageToken);
            }
            if (fields != null){
             endpoint.append("&fields=" + csvString(fields));
            }
            URL url = new URL(endpoint.toString());
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setRequestProperty("accept", "text/json");
            InputStream inStream = urlConn.getInputStream();
            Reader reader = new InputStreamReader(inStream);
            result = JsonObject.readFrom(reader);
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return result;
    }
 private String csvString(ArrayList fields) {
  StringBuilder fieldCsv = new StringBuilder();
     for (int i = 0; i < fields.size(); i++){
      fieldCsv.append(fields.get(i));
      if (i + 1 != fields.size()){
       fieldCsv.append(",");
      }
     }
  return fieldCsv.toString();
 }
}
```

이 클래스에는 Auth 개체를 수락하는 단일 생성자가 있으며, 그런 다음 선택적 매개 변수와 필수 매개 변수 모두에 대해 여러 개의 설정자를 노출합니다. 이 경우, 이메일 주소로 get 리드를 수행하려면 filterType 및 filterValues를 설정하는 것에만 관여하면 됩니다. 따라서 &quot;email&quot;에는 setFilterType을 사용하고 ID를 검색해야 하는 이메일 주소에는 addFilterValue를 사용합니다. 매개 변수를 설정한 경우 getData 메서드를 사용하여 검색된 잠재 고객 레코드의 JSON 표현식이 있는 결과 배열이 포함된 잠재 고객 끝점에서 JsonObject를 검색할 수 있습니다.

### 결합

사용 중인 샘플 코드를 살펴보았으므로, 테스트 이메일 주소 <testlead@marketo.com>과(와) 일치하는 리드를 검색하는 간단한 예를 살펴보겠습니다. 이를 위해 &quot;email&quot;에 setFilterType을 사용하고 정보를 검색해야 하는 이메일 주소에 addFilterValue를 사용해야 합니다. 매개 변수를 설정한 경우 getData 메서드를 사용하여 검색된 잠재 고객 레코드의 JSON 표현식이 있는 결과 배열이 포함된 잠재 고객 끝점에서 JsonObject를 검색할 수 있습니다.

```java
package dev.marketo.blog_leads;

import com.eclipsesource.json.JsonObject;

public class App
{
    public static void main( String[] args )
    {
     //Create an instance of Auth so that we can authenticate with our Marketo instance
        //Change the credentials here to your own
        Auth auth = new Auth("CHANGE ME", "CHANGE ME", "CHANGE ME");
        //Create and parameterize an instance of Leads
        Leads getLeads = new Leads(auth)
              .setFilterType("email")
              .addFilterValue("<testlead@marketo.com>");
        //get the inner results array of the response
        JsonObject leadsResult = getLeads.getData();
        System.out.println(leadsResult);
    }
}
```

이 기본 메서드 예제에서는 Auth 인스턴스를 만든 다음 새 Leads 생성자에게 전달합니다. setFilterType 및 addFilterValue를 사용하여 Leads 인스턴스를 구성하여 전자 메일 주소 &quot;<testlead@marketo.com>&quot;과(와) 일치하는 리드만 검색합니다. 다음 예에서는 이를 콘솔에 출력합니다.

토큰이 비어 있거나 만료되었습니다. 새 인증 시도 중
<https://299-BYM-827.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id=b417d98f-9289-47d1-a61f-db141bf0267f&client_secret=0DipOvz4h2wP1ANeVjlfwMvECJpo0ZYc>(으)로 인증 시도 중
Got 인증 응답: {&quot;access_token&quot;:&quot;ec0f02c0-28ac-4d6c-b7d7-00e47ae85ff1:st&quot;,&quot;token_type&quot;:&quot;bearer&quot;,&quot;expires_in&quot;:538,&quot;scope&quot;:&quot;<apiuser@mktosupport.com>&quot;}
&lbrace;&quot;requestId&quot;:&quot;14fb6#14e6a7a9ad6&quot;,&quot;result&quot;:[{&quot;id&quot;:1026322,&quot;updatedAt&quot;:&quot;2015-07-07T21:43:25Z&quot;,&quot;lastName&quot;:&quot;Lead&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07-07T21:43:25Z&quot;,&quot;firstName&quot;:&quot;Test&quot;},{&quot;id&quot;:1026323,&quot;updatedAt&quot;:&quot;2015-07-07A t21:43:43Z&quot;,&quot;lastName&quot;:&quot;Lead2&quot;,&quot;email&quot;:&quot;<testlead@marketo.com>&quot;,&quot;createdAt&quot;:&quot;2015-07-07T21:43:43Z&quot;,&quot;firstName&quot;:&quot;Test&quot;}],&quot;success&quot;:true

이제 필요한 방식으로 처리할 수 있는 리드 데이터가 있습니다. 읽어주셔서 감사드리며, 의견을 남겨주시기 바랍니다.

_케니_&#x200B;이(가) _2015-07-10_&#x200B;에 게시함

## 2015년 7월 릴리스 업데이트

REST API

* 영업 담당자 API

Marketo 영업 사용자 개체 내에 있는 데이터를 프로그래밍 방식으로 나열하고 설명하고 CRUD할 수 있는 새 [영업 사용자 끝점](/help/rest-api/sales-persons.md)이 도입되었습니다. 또한 영업 사원은 가망 고객, 기회 또는 회사에 지정할 수 있습니다. 이는 잠재 고객, 기회 또는 회사에 대한 만들기/업데이트/업데이트 엔드포인트를 호출할 때 &quot;externalSalesPersonId&quot; 속성을 지정하여 수행됩니다.

참고: 프로그램 엔드포인트에 대한 액세스 권한을 제공하기 위해 역할 권한(읽기 전용 영업 담당자, 읽기-쓰기 영업 담당자)이 추가되었습니다. API 사용자 역할이 영업사원 API 릴리스 이전인 경우 액세스를 활성화하려면 해당 권한으로 API 사용자 역할을 업데이트해야 합니다. 그렇지 않으면 603 &quot;액세스 거부됨&quot; 오류 응답을 받게 됩니다.

* 자산 API - 랜딩 페이지 템플릿

랜딩 페이지 템플릿과 연결된 데이터를 프로그래밍 방식으로 나열하고 만들고 업데이트할 수 있는 새로운 [랜딩 페이지 템플릿 끝점](https://developer.adobe.com/marketo-apis/api/asset/#landing_page_templates_endpoints)이 도입되었습니다.

* 자산 API - 세그먼트

두 가지 세그먼트 관련 끝점이 도입되었습니다.

[세그먼트 가져오기](https://developer.adobe.com/marketo-apis/api/asset/get-segments)

[ID별 세그먼테이션 가져오기](https://developer.adobe.com/marketo-apis/api/asset/get-segmentation-by-id)

* 이름으로 폴더 가져오기가 &quot;workSpace&quot; 매개 변수를 준수하지 않던 문제를 수정했습니다. [LM-61059]
* 사용자 지정 개체 API에 대한 몇 가지 성능을 개선했습니다.

_David_&#x200B;이(가) _2015-07-17_&#x200B;에 게시함

## Marketo REST API를 사용하여 리드, 회사 및 기회 생성 및 연결

Marketo 분석을 최대한 활용하려면 리드, 회사 및 영업 기회 레코드 간에 정확하고 강력한 연관성을 구축하는 것이 중요합니다. 기본 CRM 동기화를 활용하지 않는 경우 이러한 관계를 구축하면 약간의 문제가 발생할 수 있으므로 현재 이러한 관계를 구축하는 방법을 살펴보겠습니다.

### 개체 관계

Marketo에는 영업 기회 보고를 완전히 수립하는 데 필요한 몇 가지 중요한 관계가 있습니다.

* Lead 및 Opportunity 는 OpportunityRole 오브젝트와 다대다 관계에 있습니다.
* OpportunityRole 에는 LeadId 및 externalopportunityid 필드가 모두 있어 Lead에서 Opportunity로의 관계를 만듭니다.
* Has Opportunity 스마트 목록 필터 자격을 얻으려면 잠재 고객에게 Opportunity 와 관련된 OpportunityRole 이 있어야 합니다.
* 기회는 externalCompanyId 필드를 통해 Company 객체와 다대일 관계를 갖습니다.
* 리드는 externalCompanyId 필드를 통해 회사와 일대다 관계를 갖습니다.
* 영업 기회는 잠재 고객의 확보 프로그램을 기반으로 한 프로그램 또는 해당 멤버십과 프로그램 성공에 기인합니다([속성 이해](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/reporting/revenue-cycle-analytics/revenue-tools/attribution/understanding-attribution) 참조).

리드 데이터베이스 전반에 걸쳐 이러한 관계를 구축하면 Marketo 분석을 완전히 활용하고 프로그램이 기회 창출 및 승률에 미치는 영향을 확인할 수 있습니다.

### 회사

이러한 관계를 구축하는 가장 간단한 방법은 회사 창조를 시작하는 것입니다. 이렇게 하면 기회를 만든 후 업데이트하기 위해 추가 API 호출을 수행해야 하는 대신 만드는 동안 externalCompanyId를 기회에 전달할 수 있습니다. 기존 구성에 따라 이 단계가 필요하거나 필요하지 않을 수 있지만 관계를 구축하려면 연결된 회사와의 새로운 리드 및 연락처에 Marketo 인스턴스에 이러한 레코드를 추가해야 하므로 회사 레코드를 만드는 데 사용되는 몇 가지 코드를 살펴보겠습니다.

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertCompanies {
 public List<JsonObject> input; //a list of Companies to use for input.  Each must have a member "externalCompanyId".
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate
 public String dedupeBy; //select mode of Deduplication, dedupeFields for all dedupe parameters(externalCompanyId), idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object


 //Constructs an UpsertOpportunities with Auth, but with no input set
 public UpsertCompanies(Auth auth){
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/companies.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertCompanies(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 //adds input to existing list, creates arraylist if it was built without a list
 public UpsertCompanies addCompanies(JsonObject... companies){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : companies) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }

 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
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
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 private JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
  JsonArray in = new JsonArray(); //Create a JsonArray for the "input" member to hold Opp records
  for (JsonObject jo : input) {
   in.add(jo); //add our company records to the input array
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action); //add the action member if available
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy); //add the dedupeBy member if available
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertCompanies instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 //sets or replaces existing input with list
 public UpsertCompanies setInput(List input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertCompanies setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertCompanies setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

회사 API는 &quot;dedupeFields&quot; 및 &quot;idField&quot;라는 요청의 dedupeBy 매개 변수로 설정된 두 가지 중복 제거 옵션을 제공합니다. Describe Companies 를 호출하여 명시적으로 검색할 수 있습니다. dedupeBy가 설정되지 않은 경우 dedupeFields가 기본값으로 설정됩니다. 회사 레코드의 경우 dedupeFields는 항상 외부 소스에 의해 설정된 임의의 문자열인 &quot;externalCompanyId&quot;에 해당하고, idField는 생성 후 Marketo에서 생성 및 반환된 정수인 &quot;marketoId&quot; 필드에 해당합니다. dedupeBy에 대한 선택에 따라 externalCompanyId 또는 marketoId 중 하나를 회사 레코드의 업데이트 호출에 포함해야 합니다. 이와 동일한 요구 사항은 Opportunity 및 Opportunity Role Object API에 적용됩니다. 코드는 두 개의 생성자를 노출합니다. 하나는 Auth 개체의 단일 인수를 수락하고 다른 하나는 Auth 및 [JsonObject](https://github.com/ralfstx/minimal-json) 회사 레코드 목록을 수락합니다. 입력 목록 없이 구성된 경우 addCompanies 메서드를 통해 회사 레코드를 추가해야 합니다. 그러면 입력이 null일 경우 새 ArrayList를 만들고 모든 JsonObject 인수를 입력 목록에 추가합니다. 다음은 사용 예입니다.

```java
//Create a new company to associate to
JsonObject myCompany = new JsonObject().add("externalCompanyId", "myCompany");
UpsertCompanies upsertCompanies = new UpsertCompanies(auth).addCompanies(myCompany);
JsonObject companiesResult = upsertCompanies.postData();
System.out.println(companiesResult);
```

필드 `externalCompanyId`이(가) 하나만 있는 단일 회사 JsonObject를 만든 다음 UpdateCompanies 인스턴스를 구성하고 `addCompanies`을(를) 사용하여 입력 목록에 회사를 추가합니다.

### 기회

회사 개체와 마찬가지로 영업 기회 API에는 `dedupeBy` 매개 변수가 있으며, &quot;dedupeFields&quot; 또는 &quot;idField&quot;를 수락하고 각각 &quot;externalopportunityid&quot; 및 &quot;marketoGUID&quot;에 해당합니다. 다음은 UpsertCompanies 클래스와 매우 유사한 코드입니다.

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertOpportunities {
 public List<JsonObject> input; //a list of Opportunities to use for input.  Each must have a member "externalopportunityid".  Each can optionally include "externalCompanyId" for company association
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate
 public String dedupeBy; //select mode of Deduplication, dedupeFields for all dedupe parameters, idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object


 //Constructs an UpsertOpportunities with Auth, but with no input set
 public UpsertOpportunities(Auth auth){
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/opportunities.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertOpportunities(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 public UpsertOpportunities addOpportunities(JsonObject... opp){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : opp) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }

 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
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
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 private JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject(); //Create a new JsonObject for the Request Body
  JsonArray in = new JsonArray(); //Create a JsonArray for the "input" member to hold Opp records
  for (JsonObject jo : input) {
   in.add(jo); //add our Opportunity records to the input array
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action); //add the action member if available
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy); //add the dedupeBy member if available
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertOpportunites instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 public UpsertOpportunities setInput(List<JsonObject> input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertOpportunities setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertOpportunities setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

Auth 또는 `Auth+List<JsonObject>` 및 `addOpportunities` 메서드를 사용하여 JsonObject 기회를 입력하는 동일한 생성자 옵션이 제공됩니다. 다음은 사용 예입니다.

```java
//Create some JsonObjects for Opportunity Data
JsonObject opp1 = new JsonObject().add("name", "opportunity1")
    .add("externalopportunityid", "Opportunity1Test")
    .add("externalCompanyId", "myCompany")
    .add("externalCreatedDate", "2015-01-01T00:00:00z");
JsonObject opp2 = new JsonObject().add("name", "opportunity2")
    .add("externalopportunityid", "Opportunity2Test")
    .add("externalCompanyId", "myCompany")
    .add("externalCreatedDate", "2015-01-01T00:00:00z");

//Create an Instance of UpsertOpportunities and POST it
UpsertOpportunities upsertOpps = new UpsertOpportunities(auth)
                        .setAction("createOnly")
                        .addOpportunities(opp1, opp2);
JsonObject oppsResult = upsertOpps.postData();
System.out.println(oppsResult);
```

여기에서는 두 개의 예제 영업 기회를 만든 다음 이름, externalopportunityid, externalCompanyId 및 externalCreatedDate 필드에 대한 값을 제공합니다. externalCreatedDate에 대해서는 아직 논의하지 않았지만, 기회 생성 시 RCE의 마스터 필드로 처리되어 올바른 속성을 위해 중요해지기 때문에 를 활용하는 것이 중요합니다. 조직의 비즈니스 논리를 사용하여 기존 영업 기회 데이터를 다시 채우거나 즉시 새 영업 기회를 만들지 여부에 따라 이 필드에 입력하는 사항을 결정할 수 있습니다. UpdateOpportunities 인스턴스를 만든 다음 addOpportunities를 통해 JsonObjects를 추가합니다. 이제 인스턴스가 구성되었으므로 postData를 사용하여 Marketo에 푸시하고 결과를 인쇄할 수 있습니다

### 역할

역할은 dedupeBy를 dedupeFields로 설정할 때 요구 사항이 약간 다르다는 점을 제외하면 앞의 두 개체와 매우 유사합니다. 역할을 사용하려면 이 메서드 &quot;leadId&quot;, &quot;role&quot; 및 &quot;externalopportunityid&quot;를 통해 레코드를 만들거나 업데이트할 때 세 개의 필드를 포함해야 합니다. &quot;role&quot;은 어떤 문자열 값이든 사용할 수 있지만 나머지 두 값은 각각 잠재 고객의 유효한 ID와 영업 기회의 유효한 ID를 참조해야 합니다.

```java
package dev.marketo.opportunities;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.Reader;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.net.ssl.HttpsURLConnection;

import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

public class UpsertOpportunityRoles {
 public List<JsonObject> input; //Array of Opportunity Roles as JsonObjects, must have "leadId", "role" and "externalopprtunityid"
 public String action; //specify the action to be undertaken, createOnly, updateOnly, createOrUpdate, defaults to createOrUpdate if unset
 public String dedupeBy;//select mode of Deduplication, dedupeFields for all dedupe parameters, idField for marketoId
 private String endpoint; //endpoint URL created with Constructor
 private Auth auth; //Marketo Auth Object

 //Constructs an UpsertOpportunityRoles with Auth, but with no input set
 public UpsertOpportunityRoles(Auth auth) {
  this.auth = auth;
  this.endpoint = this.auth.marketoInstance + "/rest/v1/opportunities/roles.json";
 }
 //Constructs and UpsertOpportunities with Auth and input set
 public UpsertOpportunityRoles(Auth auth, List<JsonObject> input) {
  this(auth);
  this.input = input;
 }
 public UpsertOpportunityRoles addRoles(JsonObject... role){
  if (this.input == null){
   this.input = new ArrayList();
  }
  for (JsonObject jo : role) {
   System.out.println(jo);
   this.input.add(jo);
  }
  return this;
 }
 //executes the request to Marketo, body will be empty if input is not set
 public JsonObject postData(){
  JsonObject result = null;
  try {
   JsonObject requestBody = buildRequest(); //builds the Json Request Body
   String s = endpoint + "?access_token=" + auth.getToken(); //takes the endpoint URL and appends the access_token parameter to authenticate
   URL url = new URL(s);
   HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection(); //Return a URL connection and cast to HttpsURLConnection
   urlConn.setRequestMethod("POST");
   urlConn.setRequestProperty("Content-type", "application/json");//"application/json" content-type is required.
            urlConn.setRequestProperty("accept", "text/json");
            urlConn.setDoOutput(true);
   OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
   wr.write(requestBody.toString());
   wr.flush();
   InputStream inStream = urlConn.getInputStream();  //get the inputStream from the URL connection
   Reader reader = new InputStreamReader(inStream);
   result = JsonObject.readFrom(reader); //Read from the stream into a JsonObject
   urlConn.disconnect();
  } catch (MalformedURLException e) {
   e.printStackTrace();
  } catch (IOException e) {
   e.printStackTrace();
  }
  return result;
 }

 public JsonObject buildRequest(){
  JsonObject requestBody = new JsonObject();
  JsonArray in = new JsonArray();
  for (JsonObject jo : input) {
   in.add(jo);
  }
  requestBody.add("input", in);
  if (this.action != null){
   requestBody.add("action", action);
  }
  if (this.dedupeBy != null){
   requestBody.add("dedupeBy", dedupeBy);
  }
  return requestBody;
 }
 //Getters and Setters
 //Setters return the UpsertOpportunites instance to allow simple formatting:
 public List<JsonObject> getInput() {
  return input;
 }
 public UpsertOpportunityRoles setInput(List<JsonObject> input) {
  this.input = input;
  return this;
 }
 public String getAction() {
  return action;
 }
 public UpsertOpportunityRoles setAction(String action) {
  this.action = action;
  return this;
 }
 public String getDedupeBy() {
  return dedupeBy;
 }
 public UpsertOpportunityRoles setDedupeBy(String dedupeBy) {
  this.dedupeBy = dedupeBy;
  return this;
 }

}
```

이전 예제와 마찬가지로 생성자 및 addRoles 메서드에 대해서도 유사한 패턴을 따릅니다. 예를 들어 보겠습니다.

```java
//Create Some opp roles now
JsonObject opp1Role = new JsonObject()
                        .add("role", "Captain")
                        .add("externalopportunityid", opp1.get("externalopportunityid").asString())
                        .add("leadId", 318794);
JsonObject opp2Role = new JsonObject()
                        .add("role", "Commander")
                        .add("externalopportunityid", opp2.get("externalopportunityid").asString())
                        .add("leadId", 318795);

//Create an Instance of UpsertOpportunityRoles and POST it
UpsertOpportunityRoles upsertRoles = new UpsertOpportunityRoles(auth)
                        .setAction("createOnly")
                        .addRoles(opp1Role, opp2Role);
JsonObject rolesResult = upsertRoles.postData();
System.out.println(rolesResult);
```

여기에서는 두 가지 예제 역할에 대한 새 JsonObject를 만들고 필요한 dedupeFields를 추가하여 이미 만든 기회에서 externalopportunityid를 가져온 다음 Marketo으로 푸시합니다.

### 모두 합치기

다음은 기본 방법의 전체 예입니다.

```java
package dev.marketo.opportunities;

import com.eclipsesource.json.JsonObject;

public class App
{
    public static void main( String[] args )
    {
     //create an Instance of Auth
        Auth auth = new Auth("CLIENT_ID_CHANGE_ME", "CLIENT_SECRET_CHANGE_ME", "MARKETO_HOST_CHANGE_ME");

        //Create a new company to associate to
        JsonObject myCompany = new JsonObject().add("externalCompanyId", "myCompany");
        UpsertCompanies upsertCompanies = new UpsertCompanies(auth).addCompanies(myCompany);
        JsonObject companiesResult = upsertCompanies.postData();
        System.out.println(companiesResult);

        //Create some JsonObjects for Opportunity Data
        JsonObject opp1 = new JsonObject().add("name", "opportunity1")
           .add("externalopportunityid", "Opportunity1Test")
           .add("externalCompanyId", "myCompany")
           .add("externalCreatedDate", "2015-01-01T00:00:00z");
        JsonObject opp2 = new JsonObject().add("name", "opportunity2")
           .add("externalopportunityid", "Opportunity2Test")
           .add("externalCompanyId", "myCompany")
           .add("externalCreatedDate", "2015-01-01T00:00:00z");

        //Create an Instance of UpsertOpportunities and POST it
        UpsertOpportunities upsertOpps = new UpsertOpportunities(auth)
                                .setAction("createOnly")
                                .addOpportunities(opp1, opp2);
        JsonObject oppsResult = upsertOpps.postData();
        System.out.println(oppsResult);

        //Create Some opp roles now
        JsonObject opp1Role = new JsonObject()
           .add("role", "Captain")
           .add("externalopportunityid", opp1.get("externalopportunityid").asString())
           .add("leadId", 318794);
        JsonObject opp2Role = new JsonObject()
           .add("role", "Commander")
           .add("externalopportunityid", opp2.get("externalopportunityid").asString())
           .add("leadId", 318795);

        //Create an Instance of UpsertOpportunityRoles and POST it
        UpsertOpportunityRoles upsertRoles = new UpsertOpportunityRoles(auth)
           .setAction("createOnly")
           .addRoles(opp1Role, opp2Role);
        JsonObject rolesResult = upsertRoles.postData();
        System.out.println(rolesResult);

    }
}
```

회사, 기회 및 역할을 만드는 순서를 볼 수 있습니다. 이제 회사 및 영업 기회 데이터를 Marketo에 동기화하도록 모두 설정되었습니다.

_케니_&#x200B;이(가) _2015-08-07_&#x200B;에 게시함

## Marketo REST API를 사용하여 트랜잭션 이메일 보내기: 2부, 사용자 지정 콘텐츠

이번 주에는 요청 캠페인 API 호출을 통해 다이내믹 콘텐츠를 이메일에 전달하는 방법을 살펴봅니다. 요청 캠페인을 사용하면 외부에서 전자 메일을 트리거할 수 있을 뿐만 아니라 전자 메일 내의 [내 토큰](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/programs/tokens/understanding-my-tokens-in-a-program)의 콘텐츠를 바꿀 수도 있습니다. 내 토큰은 프로그램 또는 마케팅 폴더 수준에서 사용자 지정할 수 있는 재사용 가능한 콘텐츠입니다. 이는 요청 캠페인 호출을 통해 대체할 자리 표시자로 존재할 수도 있습니다.

### 이메일 작성

콘텐츠를 사용자 지정하려면 먼저 Marketo에서 [프로그램](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/create-a-program) 및 [이메일](https://experienceleague.adobe.com/ko/docs/marketo/using/home)을 구성해야 합니다. 사용자 지정 콘텐츠를 생성하려면 프로그램 내부에 토큰을 만든 다음 전송할 이메일에 배치해야 합니다. 간결성을 위해 이 예제에서는 하나의 토큰만 사용하고 있지만, 보낸 사람 이메일, 보낸 사람 이름, 회신 주소 또는 이메일의 모든 콘텐츠에서 토큰의 숫자를 바꿀 수 있습니다. 그러면 교체를 위해 하나의 리치 텍스트 토큰을 만들고 이를 &quot;bodyReplacement&quot;라고 하겠습니다. 리치 텍스트를 사용하면 토큰의 모든 컨텐츠를 입력하려는 임의의 HTML으로 바꿀 수 있습니다. 비어 있는 동안에는 토큰을 저장할 수 없습니다. 먼저 여기에 자리 표시자 텍스트를 삽입하십시오. 이제 이메일에 토큰을 삽입해야 합니다. 이제 요청 캠페인 호출을 통해 이 토큰을 교체할 수 있습니다. 이 토큰은 이메일별로 대체해야 하는 단일 텍스트 행만큼 단순하거나 이메일의 거의 전체 레이아웃을 포함할 수 있습니다.

### 코드

요청 캠페인 호출에 사용자 지정된 토큰을 전달하기 위해 지난주부터 코드를 확장하고 있습니다.

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
        String bodyReplacement = "<div class="replacedContent"><p>This content has been replaced</p></div>";
        rc.addToken("{{my.bodyReplacement}}", bodyReplacement);
        rc.postData();
    }
}
```

이번에는 bodyReplacement 변수에 토큰 콘텐츠를 만든 다음 addToken 메서드를 사용하여 요청에 추가합니다. addToken은 키 및 값을 사용한 다음 JsonObject 표현식을 만들고 내부 토큰 배열에 추가합니다. 그런 다음 postData 메서드 동안 serialize되고 다음과 같은 본문이 만들어집니다.

`{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class="replacedContent"><p>This content has been replaced</p></div>"}]}}`

결합된 콘솔 출력은 다음과 같습니다.

```bash
Token is empty or expired. Trying new authentication
Trying to authenticate with&nbsp;...
Got Authentication Response: {"access_token":"19d51b9a-ff60-4222-bbd5-be8b206f1d40:st","token_type":"bearer","expires_in":3565,"scope":"<apiuser@mktosupport.com>"}
Executing RequestCampaign call
Endpoint: .../rest/v1/campaigns/1578/trigger.json?access_token=19d51b9a-ff60-4222-bbd5-be8b206f1d40:st
Request Body:
{"input":{"leads":[{"id":1}],"tokens":[{"name":"{{my.bodyReplacement}}","value":"<div class="replacedContent"><p>This content has been replaced</p></div>"}]}}
Result:
{"requestId":"1e8d#14eadc5143d","result":[{"id":1578}],"success":true}
```

### 요약

이 방법은 여러 가지 방법으로 확장할 수 있으며, 개별 레이아웃 섹션 내 이메일 또는 외부 이메일 내의 콘텐츠를 변경하여 사용자 지정 값을 작업 또는 관심 있는 순간에 전달할 수 있습니다. 프로그램 내에서 토큰을 사용할 수 있는 모든 위치에서 이 방법을 사용하여 사용자 지정할 수 있습니다. [캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST) 호출에서도 유사한 기능을 사용할 수 있습니다. 이렇게 하면 전체 일괄 처리 캠페인에서 토큰을 처리할 수 있습니다. 각 리드를 기준으로 사용자 정의할 수 없지만, 다양한 리드 세트에서 콘텐츠를 사용자 정의하는 데 매우 유용합니다.

_케니_&#x200B;이(가) _2015-07-24_&#x200B;에 게시함

## API를 사용하여 Marketo에서 리드 데이터 업데이트

1년 여 전에 API를 사용하여 Marketo에 고객 및 잠재 고객 정보 업데이트를 게시했습니다. 해당 게시물에는 업데이트를 위해 외부 시스템을 폴링하기 위해 반복적으로 실행할 수 있는 코드 샘플이 표시되었습니다. 외부 데이터를 검색하고 Marketo에 푸시하여 리드 정보를 업데이트하는 것이었습니다. 제공된 코드 샘플은 SOAP API를 사용했습니다. 동일한 목표를 달성하기 위한 REST 엔드포인트. **프로그램 입력** 외부 시스템의 데이터를 Marketo REST API에서 사용할 수 있는 형식으로 변환해야 할 수 있습니다. 리드 만들기/업데이트 API를 사용하고 있으므로 데이터는 요청 본문에 전송되는 JSON으로 포맷되어야 합니다. 이는 예제로 가장 잘 설명될 수 있습니다. 아래의 Java 샘플 코드에서는 문자열 배열에 모의 잠재 고객 데이터를 배치했습니다. 각 문자열은 각 잠재 고객에 대한 데이터(이름, 성, 이메일 주소, 직책)를 팔로우합니다.

```java
private static String externalLeadData[] = {
        "Henry, Adams, <henry@superstar.com>, Director of Demand Generation",
        "Suzie, Smith, <ssmith@gmail.com>, VP Marketing"
};
```

샘플 코드는 배열을 아래의 JSON 블록으로 변환합니다.

```json
{
"input":
    [
        {"firstName":"Henry", "lastName":"Adams", "email":"<henry@superstar.com>", "title":"Director of Demand Generation"},
        {"firstName":"Suzie", "lastName":"Smith", "email":"<ssmith@gmail.com>", "title":"VP Marketing"}
    ]
}
```

각 &quot;입력&quot; 배열 항목은 Marketo의 개별 리드에 해당합니다. 배열 항목은 하나 이상의 Marketo 리드 필드 이름과 해당 값을 포함하는 JSON 개체입니다. 지정하려는 필드 이름(이 경우 firstName, lastName, email 및 title)은 Marketo 구독에 대해 정의된 REST API 이름과 일치해야 합니다. 필드 이름을 내보내면 Marketo 관리 패널의 필드 관리 섹션에서 REST API 이름 을 찾을 수 있습니다. 필드 이름은 아래와 같이 Excel 파일로 내보냅니다. 또는 [리드 설명](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2) API를 호출하여 프로그래밍 방식으로 필드 이름을 찾을 수 있습니다. 예를 들어 다음은 이름 필드에 대한 REST API 이름을 포함하는 응답 코드 조각 설명 입니다.

```json
{
    "id": 29,
    "displayName": "First Name",
    "dataType": "string",
    "length": 255,
    "soap": {
        "name": "FirstName",
        "readOnly": false
    },
    "rest": {
        "name": "firstName",
        "readOnly": false
    }
},
```

**프로그램 논리** 페이로드가 적절한 형식이면 리드 만들기/업데이트를 호출할 준비가 되었습니다. 이 샘플에서는 선택적 매개 변수를 지정하지 않습니다. 기본 동작은 리드 레코드(업데이트)를 만들거나 업데이트하고, 중복 제거 목적으로 이메일을 사용하고, 동기 처리를 사용하는 것입니다. 리드 만들기/업데이트 호출이 성공하면 응답 본문에는 Marketo 리드 ID와 만들기/업데이트 작업의 상태가 포함된 &quot;결과&quot; 배열이 포함됩니다. 요청에서 전달한 &quot;action&quot; 매개 변수에 따라 상태는 &quot;updated&quot;, &quot;created&quot; 또는 &quot;skipped&quot;일 수 있습니다. 이 예제를 계속 진행하여 첫 번째 리드가 존재하지 않았다고 가정하고(Henry Adams) 두 번째 리드가 존재했다고 가정합니다(Suzie Smith). 다음과 유사한 응답이 첫 번째 리드가 만들어지고 두 번째 리드가 업데이트되었음을 나타냅니다.

```json
{
    "success":true,
    "requestId":"118f8#14f1a0b82fc",
    "result":[
        {
            "id":318798,
            "status":"created"
        },
        {
            "id":318797,
            "status":"updated"
        }
    ]
}
```

이제 다 됐습니다. 해피 코딩! **프로그램 코드**

```java
package com.marketo;

// minimal-json library (<https://github.com/ralfstx/minimal-json>)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

import javax.net.ssl.HttpsURLConnection;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStreamWriter;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.\*;

public class CreateUpdateLeads {
    //
    // Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    //    public static String CUSTOM_SERVICE_DATA[] =
    //      {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"};
    //
    private static final String CUSTOM_SERVICE_DATA[] =
            { INSERT YOUR CUSTOM SERVICE DATA HERE };

    //
    // Mock up data that could be read from an external data source.
    // An array of CSV strings the form:
    //   "firstName, lastName, email, title"
    private static String externalLeadData[] = {
        "Henry, Adams, henry@superstar.com, Director of Demand Generation",
        "Suzie, Smith, ssmith@gmail.com, VP Marketing"
    };

    public static void main(String[] args) {
        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
                CUSTOM_SERVICE_DATA[0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[1], CUSTOM_SERVICE_DATA[2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(httpRequest("GET", identityUrl, null));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URL for Create/Update Leads
        String createUpdateLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s", baseUrl, accessToken);

        // Convert String array into JsonArray to pass as part of request body
        JsonArray input = convertExternalLeadDataToJson(externalLeadData);

        // Build request body JSON
        JsonObject requestObj = new JsonObject();
        requestObj.add("input", input);

        // Call Create/Update Lead API
        JsonArray result = new JsonArray();
        JsonObject leadObj = JsonObject.readFrom(httpRequest("POST", createUpdateLeadsUrl, requestObj.toString()));
        if (leadObj.get("success").asBoolean()) {
            if (leadObj.get("result") != null) {
                result = leadObj.get("result").asArray();
            }
        }

        // Print out results object
        System.out.println(result);
        System.exit(0);
    }

    // Convert array of CSV formatted Strings into an array of JSON objects
    private static JsonArray convertExternalLeadDataToJson(String input[]) {
        JsonArray output = new JsonArray();

        // Loop through each CSV row in array
        for (int i = 0; i < input.length; i++) {
            // Split CSV row into separate fields
            List items = Arrays.asList(input[i].split(","));

            // Add fields to JSON object
            JsonObject lead = new JsonObject();
            lead.add("firstName", items.get(0));
            lead.add("lastName", items.get(1));
            lead.add("email", items.get(2));
            lead.add("title", items.get(3));
            output.add(lead);
        }
        return output;
    }

    // Perform HTTP request
    private static String httpRequest(String method, String endpoint, String body) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setDoOutput(true);
            urlConn.setRequestMethod(method);
            switch (method) {
                case "GET":
                    break;
                case "POST":
                    urlConn.setRequestProperty("Content-type", "application/json");
                    urlConn.setRequestProperty("accept", "text/json");
                    OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
                    wr.write(body);
                    wr.flush();
                    break;
                default:
                    System.out.println("Error: Invalid method.");
                    return data;
            }
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

_David_&#x200B;이(가) _2015-08-14_&#x200B;에 게시함

## Marketo에 SalesPerson 데이터 추가

새로운 SalesPerson API를 사용하면 기본 CRM 통합 없이 인스턴스에서 Marketo 리드를 SalesPerson 레코드와 자유롭게 연결할 수 있습니다. 이렇게 하면 Marketo 내에서 {{lead.Lead Owner Email Address}} 및 관련 필드와 토큰을 사용할 수 있습니다.

### SalesPerson 레코드 생성

가망 고객을 SalesPerson 레코드와 연결하려면 먼저 SalesPerson 레코드를 Marketo에 입력해야 합니다. 다음은 PHP의 예제 클래스입니다.

```php
<?php

class SalesPerson{
 private $auth;//auth object
 private $action;// string designating request action, createOnly, updateOnly, createOrUpdate
 private $dedupeBy;//dedupeFields or idField
 private $input;//array of salesperson objects for input

 //takes an Auth object as the first argument
 public function _construct($auth, $input){
  $this->auth = $auth;
  $this->input = $input;
 }

 //constructs the json request body
 private function bodyBuilder(){
  $body = new stdClass();
  $body->input = $this->input;
  if (isset($this->action)){
   $body->action = $this->action;
  }
  if (isset($this->dedupeBy)){
   $body->dedupeBy = $this->dedupeBy;
  }
  return json_encode($body);
 }
 //submits the request to Marketo and returns the response as a string
 public function postData(){
  $url = $this->auth->getHost() . "/rest/v1/salespersons.json?access_token=" . $this->auth->getToken();
  $ch = curl_init($url);
  $requestBody = $this->bodyBuilder();
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  curl_setopt($ch, CURLOPT_POST, 1);
  curl_setopt($ch, CURLOPT_POSTFIELDS, $requestBody);
  curl_getinfo($ch);
  $response = curl_exec($ch);
  curl_close($ch);
  return $response;
 }
 //getters and setters
 public function setAction($action){
  $this->action = $action;
 }
 public function getAction($action){
  return $this->action;
 }
 public function setDedupeBy($dedupeBy){
  $this->dedupeBy = $dedupeBy;
 }
 public function getDedupeBy($dedupeBy){
  return $this->dedupeBy;
 }
 public function addSalesPersons($input){
  if($this->input != null){
   if (is_array($input)){
    foreach($input as $item){
     array_push($this->input, $item);
    }
   }else{
    array_push($this->input, $input);
   }
  }else{
   $this->input = $input;
  }
 }
 public function getInput(){
  return $this->input;
 }

}
```

위의 클래스에서 $input 변수는 가능한 멤버가 있는 stdClass 개체의 배열입니다.

* externalSalesPersonId(만들 때만 유효함)
* id(key-in updateOnly 모드로만)
* 이메일
* 팩스
* 이름
* 성
* mobilePhone
* 전화
* 제목

유형 및 필드 길이에 대한 자세한 내용은 Describe SalesPerson 호출을 통해 검색할 수 있습니다.

### 리드 동기화

다음은 필요한 리드를 동기화하는 빠른 예제 클래스입니다.

```php
<?php

class Leads{
 private $auth;//auth object
 private $action;// string designating request action, createOnly, updateOnly, createOrUpdate
 private $lookupField;//dedupeFields or idField
 private $input;//array of salesperson objects for input
 private $asyncProcessing;//specify whether input should be processed asynchronously
 private $partitionName;//partition name for update if requires

 //takes an Auth object as the first argument
 public function _construct($auth, $input){
  $this->auth = $auth;
  $this->input = $input;
 }

 //constructs the json request body
 private function bodyBuilder(){
  $body = new stdClass();
  $body->input = $this->input;
  if (isset($this->action)){
   $body->action = $this->action;
  }
  if (isset($this->lookupField)){
   $body->lookupField = $this->lookupField;
  }
  return json_encode($body);
 }
 //submits the request to Marketo and returns the response as a string
 public function postData(){
  $url = $this->auth->getHost() . "/rest/v1/leads.json?access_token=" . $this->auth->getToken();
  $ch = curl_init($url);
  $requestBody = $this->bodyBuilder();
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  curl_setopt($ch, CURLOPT_POST, 1);
  curl_setopt($ch, CURLOPT_POSTFIELDS, $requestBody);
  curl_getinfo($ch);
  $response = curl_exec($ch);
  curl_close($ch);
  return $response;
 }
 //getters and setters
 public function setAction($action){
  $this->action = $action;
 }
 public function getAction(){
  return $this->action;
 }
 public function setDedupeBy($lookupField){
  $this->dedupeBy = $lookupField;
 }
 public function getDedupeBy(){
  return $this->dedupeBy;
 }
 public function addLeads($input){
  if($this->input != null){
   if (is_array($input)){
    foreach($input as $item){
     array_push($this->input, $item);
    }
   }else{
    array_push($this->input, $input);
   }
  }else if (is_array($input)){
   $this->input = $input;
  }else{
   $this->input = [$input];
  }
 }
 public function getInput(){
  return $this->input;
 }
 public function setAsyncProcessing($asyncProcessing){
  $this->asyncProcessing = $asyncProcessing;
 }
 public function getAsyncProcessing() {
  return $this->asyncProcessing;
 }
 public function setPartitionName($partitionName){
  $this->partitionName = $partitionName;
 }
 public function getPartitionName() {
  return $this->partitionName;
 }

}
```

### 프로세스

다음은 두 개의 영업 사원 레코드를 생성하여 두 개의 가망 고객 레코드에 연관시키는 예입니다.

```php
<?php

require 'Auth.php';
require 'SalesPerson.php';
require 'Leads.php';

//Create an Auth object for authentication
$auth = new Auth("https://284-RPR-133.mktorest.com", "7f99bd49-0e0e-4715-a72a-0c9319f75552", "O5lZHhrQDfDKRhulY89IU42PfdhRSe6m");

//Compose new SalesPerson Records
$sales1 = new stdClass();
$sales1->externalSalesPersonId = "SalesPerson 1";
$sales1->email = "sales1@example.com";
$sales1->firstName = "Jane";
$sales1->lastName = "Doe";

$sales2 = new stdClass();
$sales2->externalSalesPersonId = "SalesPerson 2";
$sales2->email = "sales2@example.com";
$sales2->firstName = "John";
$sales2->lastName = "Doe";

//Compose lead records
$lead1 = new stdClass();
$lead1->email = "marketoDev@example.com";
//Add the external id of the desired salesperson
$lead1->externalSalesPersonId = $sales1->externalSalesPersonId;

$lead2 = new stdClass();
$lead2->email = "devBlog@example.com";
$lead2->externalSalesPersonId = $sales2->externalSalesPersonId;

//Create a new instance of SalesPerson to submit records
$salesPerson = new SalesPerson($auth, [$sales1, $sales2]);
$spResponse = $salesPerson->postData();
print_r($spResponse . "rn");
$json = json_decode($spResponse);

//Check for success on synching SalesPersons
if ($json->success){
 $leads = new Leads($auth, [$lead1, $lead2]);
 $leadsResponse = $leads->postData();
 print_r($leadsResponse . "rn");
}else{
 print_r("SalesPerson request failed with errors:rn");
 foreach ($json->errors as $error){
  print_r("code: " . $error->code . ", message: " . $error->message . "rn");
 }
}
```

예제 클래스의 경우 원하는 각 필드를 멤버로 추가하여 동기화해야 하는 SalesPerson 및 Lead 레코드를 나타내는 stdClass 개체를 생성하고 있습니다. 이 코드를 실행하면 리드 <marketoDev@example.com> 및 <devBlog@example.com>에 리드 소유자 전자 메일, 리드 소유자 이름 및 리드 소유자 성 필드가 모두 채워져 해당 필드에 관련 토큰을 사용하고 관련 스마트 목록 필터로 필터링할 수 있습니다.

### 인증 클래스

```php
<?php

class Auth{
 private $host;//host of the target Marketo instance
 private $clientId;//client Id
 private $clientSecret;//client secret
 private $token;//access_token
 private $expiry;

 function _construct($host, $clientId, $clientSecret){
  $this->host = $host;
  $this->clientId = $clientId;
  $this->clientSecret = $clientSecret;
 }
 public function getToken(){
  if (!isset($this->token) || $this->expiry > time()){
   $data = $this->getData();
   $this->expiry = time() + $data->expires_in;
   $this->token = $data->access_token;
   return $this->token;
  }else{
   return $this->token;
  }
 }
 private function getData(){
  $url = $this->host . "/identity/oauth/token?grant_type=client_credentials&client_id=" . $this->clientId . "&client_secret="
     . $this->clientSecret;
  $ch = curl_init($url);
  curl_setopt($ch,  CURLOPT_RETURNTRANSFER, 1);
  curl_setopt($ch, CURLOPT_HTTPHEADER, array('accept: application/json','Content-Type: application/json'));
  $response = curl_exec($ch);
  $json = json_decode($response);
  curl_close($ch);
  return $json;
 }
 public function getHost(){
  return $this->host;
 }
}
```

_케니_&#x200B;이(가) _2015-08-21_&#x200B;에 게시함

## API 사용자 및 사용자 지정 서비스에 대한 우수 사례

Marketo의 REST API는 인증을 위해 사용자 지정 서비스를 사용하며, 이러한 각 서비스는 API 전용 Marketo 사용자가 소유합니다. 각 사용자 정의 서비스의 기능은 해당 사용자에게 할당된 각 역할의 권한에 의해 결정됩니다. 개별 사용자 및 사용자 정의 서비스를 통합에 할당하면 다음과 같은 여러 가지 이점이 있습니다.

* 사용자에게 지정된 역할을 통해 각 개별 서비스에 지정된 [권한](/help/rest-api/custom-services.md)을(를) 미세 조정할 수 있습니다.
* 해당 사용자 지정 서비스를 삭제하여 개별 웹 서비스가 인스턴스를 호출하지 못하도록 할 수 있으며, 다른 서비스를 비활성화하지 않아도 됩니다.
* API 호출 사용에 대한 보고는 사용자별로 분류되어 활용도가 높고 비정상적인지 확인할 수 있습니다
* 각 웹 서비스에 대한 액세스 권한이 부여되는 데이터를 보다 쉽게 확인할 수 있습니다
* Workspace 지원 인스턴스는 액세스 가능한 작업 공간에 역할만 부여하여 특정 비즈니스 단위에 대한 액세스를 제한할 수 있습니다

### API 사용 정보

각 API 사용자는 API 사용 보고서에 개별적으로 보고되므로, 사용자별로 웹 서비스를 분할하면 각 통합의 사용을 쉽게 고려할 수 있습니다. 인스턴스에 대한 API 호출 수가 제한을 초과하여 후속 호출이 실패하는 경우 이 방법을 사용하면 각 서비스의 볼륨을 고려하고 문제를 해결하는 방법을 평가할 수 있습니다. [관리] -> [웹 서비스]로 이동하여 지난 7일 동안의 호출 수를 클릭하여 사용량을 확인합니다.

### 서비스 비활성화

통합에 원하지 않는 영향이 있는 경우 각 통합에 개별 사용자 정의 서비스를 할당하지 않은 경우 비활성화하는 것은 지루하고 어려울 수 있습니다. 하나씩 세분화하면 관리 -> 시작 지점에서 문제가 되는 서비스를 삭제하는 것처럼 쉬워집니다.

### Workspace 관리

Marketo Enterprise 구독의 경우 서비스는 단일 작업 영역에만 액세스해야 하는 것이 일반적이며 API 사용자에게 [역할 할당에 의해 강제 적용](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/allow-user-access-to-a-workspace)될 수 있습니다. 각 사용자 역할은 전역적으로 또는 작업 영역별로 할당할 수 있으므로, 작업 영역에서 필요한 경우 액세스를 제한할 수 있으며, 가능한 한 가장 최소한의 권한을 제공합니다.

_케니_&#x200B;이(가) _2015-08-28_&#x200B;에 게시함

## REST API를 사용하여 리드 파티션을 지정하는 방법

**리드 파티션 나누기** Marketo 리드 파티션을 사용하면 리드를 편리하게 분리할 수 있습니다. 파티션을 사용하면 조직 내의 다른 마케팅 그룹에서 단일 Marketo 인스턴스를 공유할 수 있습니다. 자세한 내용은 [작업 영역 및 리드 파티션 이해](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions)를 참조하십시오. 리드 파티션을 사용하고 Marketo REST API를 사용하여 프로그래밍 방식으로 리드를 만든다고 가정합니다. 생성한 잠재 고객이 올바른 파티션에 도달하도록 하려면 어떻게 해야 합니까? 이 게시물은 방법을 보여 줍니다! 이 예에서는 작업 공간 및 파티션 을 사용하여 지역을 기준으로 리드를 분리합니다.

먼저 &quot;국가&quot;라는 작업 영역을 정의합니다. 그런 다음 &quot;멕시코&quot;와 &quot;캐나다&quot;라는 작업 영역 내에 두 개의 파티션을 만듭니다.  **파티션에서 잠재 고객 만들기** &quot;멕시코&quot; 파티션에서 두 개의 잠재 고객을 만들려고 한다고 가정합니다. 리드를 만들려면 를 호출합니다. 파티션을 지정하려면 요청 본문에 &quot;partitionName&quot; 특성을 포함해야 합니다. partitionName 값에 사용할 항목을 어떻게 알 수 있습니까? 다음과 같이 [리드 파티션 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeProgramMemberUsingGET) API를 호출하여 인스턴스에 대한 올바른 파티션 이름 값 목록을 검색할 수 있습니다.

`GET /rest/v1/leads/partitions.json`

```json
{
    "requestId": "20ae#14f9a1a5a30",
    "result": [
        {
            "id": 1,
            "name": "Default",
            "description": "Initial system lead partition"
        },
        {
            "id": 2,
            "name": "Mexico",
            "description": "Leads that live in Mexico"
        },
        {
            "id": 3,
            "name": "Canada",
            "description": "Leads that live in Canada"
        }
    ],
    "success": true
}
```

이 경우 올바른 값은 &quot;멕시코&quot;이므로 다음과 같이 리드 생성/업데이트에 전달합니다.

`POST /rest/v1/leads.json`

```json
{
    "input": [
        {"email":"enrique.pena-nieto@gob.mx"},
        {"email":"angelica.rivera@gob.mx"}
    ],
    "action":"createOrUpdate",
    "partitionName":"Mexico"
}
```

다음은 Marketo에서 새로 생성된 리드입니다.  **파티션의 잠재 고객 업데이트** 파티션에서 기존 잠재 고객을 업데이트하려면 Create/Update Leads를 호출하고 이전과 동일하게 partitionName을 지정하십시오. 이 업데이트에서는 위에서 생성한 잠재 고객에 이름, 성 및 제목을 할당합니다.

`POST /rest/v1/leads.json`

```json
{
"input": [
        {"email":"enrique.pena-nieto@gob.mx", "firstName":"Enrique", "lastName":"Pena Neito", "title": "El Presidente"},
        {"email":"angelica.rivera@gob.mx", "firstName":"Angelica", "lastName": "Rivera", "title": "Primera Dama"}
    ],
    "action":"createOrUpdate",
    "partitionName":"Mexico"
}
```

다음은 Marketo에서 새로 업데이트된 잠재 고객입니다.
**잠재 고객에 대한 파티션 식별** 잠재 고객이 속한 파티션을 어떻게 알 수 있습니까? 이를 위해 [ID별 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadByIdUsingGET) API를 사용하고 &quot;fields&quot; 쿼리 매개 변수에 &quot;leadPartitionId&quot;를 지정합니다. 이 경우 위에서 만든 리드 ID 318816에 대한 정보를 검색합니다.

`GET /rest/v1/lead/318816.json?fields=leadPartitionId,email,firstName,lastName,title`

```json
{
    "requestId": "5c57#14f9a495b1f",
    "result": [
        {
            "id": 318816,
            "lastName": "Pena Neito",
            "title": "El Presidente",
            "email": "enrique.pena-nieto@gob.mx",
            "firstName": "Enrique",
            "leadPartitionId": 2
        }
    ],
    "success": true
}
```

partitionName이 아닌 leadPartitionId를 다시 가져옵니다. partitionName을 가져오려면 위에서 리드 파티션 가져오기 API의 출력을 다시 방문해야 합니다.

```json
{
    "id": 2,
    "name": "Mexico",
    "description": "Leads that live in Mexico"
},
```

이 경우 leadPartitionId 값 2는 &quot;Mexico&quot;의 partitionName에 매핑됩니다. 지금은 그게 다예요. 파티셔닝 해피!

_David_&#x200B;이(가) _2015-09-04_&#x200B;에 게시함

## Marketo 이메일 스크립팅의 점수 필드 비교

**참고:** Cathal Moran의 게스트 게시물입니다. Cathal은 아일랜드 더블린에 있는 Marketo EMEA 사무실에서 근무하는 솔루션 컨설턴트입니다.

### 점수 필드 비교

많은 Marketo 고객, 특히 교차 판매에 중점을 둔 고객에게는 여러 개의 점수 필드가 있으며, 이를 통해 특정 제품/영역에 대한 잠재 고객의 관심을 측정하는 데 사용되는 경우가 많습니다. 제가 사과와 바나나를 판매한다고 상상해 보세요. 만약 1의 점수가 사과가 50점이고 바나나가 10점이라면, 선호도가 어디에 있는지를 알 수 있습니다. 제 콘텐츠가 이 선호도를 반영한다면 좋지 않을까요? 이메일 스크립팅은 점수를 비교하고, 이메일을 받는 특정 리드에 대해 가장 높은(또는 가장 낮은) 점수에 따라 이메일의 콘텐츠를 개인화하는 데 사용할 수 있습니다.

### 두 숫자를 비교하려면 필드 값을 정수로 변환해야 합니다

```
#set ($score1 = $math.toInteger(${lead.Apple_Score}))
#set ($score2 = $math.toInteger(${lead.Banana_Score}))
##check if the lead score is greater than feature score
#if($score1 >= $score2)
                ##if Apple score is greater
                #set($Interest = "Special offer on Apples")
##check is the feature score is higher
#elseif($score2 >= $score1)
                ##if Feature score is greater
                #set($Interest = "Special offer on Bananas")
#else
                ##otherwise
                #set($Interest = "Special offer on Fruit")
#end
##display the Interest as content
${Interest}
```

위의 예에서는 텍스트를 개인화하고 있지만, 예를 들어 점수가 높은 다른 이미지를 쉽게 표시할 수 있습니다.

_케니_&#x200B;이(가) _2015-09-14_&#x200B;에 게시함

## 백그라운드에서 Marketo 양식 제출 만들기

조직에 웹 컨텐츠 및 고객 데이터를 호스팅하는 다양한 플랫폼이 있는 경우 결과 데이터를 별도의 플랫폼으로 수집할 수 있도록 양식의 병렬 제출이 필요한 것이 일반화됩니다. 이를 수행하는 방법에는 몇 가지가 있지만 가장 좋은 방법은 종종 Forms 2 API를 사용하여 숨겨진 Marketo 양식을 제출하는 것입니다. 이 작업은 새 Marketo 양식에서 작동하지만, 필드가 없는 빈 양식을 만드는 것이 좋습니다. 이렇게 하면 렌더링할 필요가 없으므로 양식이 필요한 것보다 더 이상 데이터를 로드하지 않습니다. 이제 폼에서 [포함 코드](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 가져와서 원하는 페이지의 본문에 추가하여 약간 수정하십시오. 포함 코드에는 다음과 같은 양식 요소가 포함됩니다.

`<form id="mktoForm_1068"></form>`

다음과 같이 &#39;style=&quot;display:none&quot;&#39;을(를) 요소에 추가하여 표시되지 않도록 할 수 있습니다.

`<form id="mktoForm_1068" style="display:none"></form>`

양식이 임베드되고 숨겨지면 양식을 제출하는 코드는 매우 간단합니다.

```javascript
var myForm = MktoForms2.allForms()[0];
myForm.addHiddenFields({
 //These are the values which will be submitted to Marketo
 "Email":"test@example.com",
 "FirstName":"John",
 "LastName":"Doe"
 });
myForm.submit();
```

이 방식으로 제출된 Forms은 잠재 고객이 양식을 작성하고 제출한 것처럼 정확하게 동작합니다. 제출 트리거는 각 구현에서 프롬프트에 대해 다른 작업을 수행하므로 구현에 따라 다르지만 기본적으로 모든 작업에서 발생할 수 있습니다. 중요한 부분은 필드와 값을 올바르게 설정하는 것입니다. 필드의 SOAP API 이름을 사용하십시오. 이 이름은 [필드 이름 내보내기](/help/rest-api/list-of-standard-fields.md)를 통해 찾을 수 있으므로 값을 올바르게 제출하십시오.

Munchkin Associate Lead에서 마이그레이션

배경 양식 제출은 Munchkin Associate Lead에 대해 권장되는 대체 방법 중 하나입니다. 아래 샘플 HTML 페이지는 Associate Lead에 제출된 동일한 값을 재사용하여 높은 수준에서 마이그레이션을 보여 줍니다.

```html
<html>
<head>
    <!--
      Munchkin Code
      Replace with your own instance code
    -->
    <script type="text/javascript">
        (function() {
          var didInit = false;
          function initMunchkin() {
            if(didInit === false) {
              didInit = true;
              Munchkin.init('CHANGE ME');
            }
          }
          var s = document.createElement('script');
          s.type = 'text/javascript';
          s.async = true;
          s.src = '//munchkin.marketo.net/munchkin-beta.js';
          s.onreadystatechange = function() {
            if (this.readyState == 'complete' || this.readyState == 'loaded') {
              initMunchkin();
            }
          };
          s.onload = initMunchkin;
          document.getElementsByTagName('head')[0].appendChild(s);
        })();
        </script>
</head>

<body>
  <!--
    Start Embed code.
    Pasted from Form Actions -> Embed Code except for addition of 'style="display:none"' to the form tag in order to hide it, and instance-specific codes redacted
    Replace with your own code for testing
  -->
  <script src="CHANGE ME"></script>
  <form id="CHANGE ME" style="display:none"></form>
  <script>MktoForms2.loadForm("CHANGE ME", "CHANGE ME", "CHANGE ME TO AN INTEGER ID");</script>
  <!--End Embed Code-->

  <!--Demo code-->
    <script>
        //The same map which is assembled for the Munchkin submission can be reused for the form submission
        let values = {
            "Email": "email@example.com",
            "FirstName": "Test",
            "LastName": "Record"
        }
        //whenReady lets us apply a callback to all mkto forms on the page
        //the callback function fires whenever a form is completely loaded
        //for most use cases this will just be used to capture a reference to the form for later usage
        //submission is done in line here for demonstration only
        MktoForms2.whenReady(function(form){

            //the addHiddenFields methods lets us add arbitrary fields to the form as well as their values
            form.addHiddenFields(values);

            //submit the form
            form.submit();


        })
    </script>
</body>
</html>
```

_케니_&#x200B;이(가) _2015-09-25_&#x200B;에 게시함

## Marketo REST API 예외 및 오류 처리: 1부

Marketo REST API는 예외 또는 오류를 반환할 수 있으므로 편의상 여기서부터 오류를 호출하겠습니다. 오류는 다음 세 가지 수준에서 발생할 수 있습니다.

* HTTP 수준입니다. 이러한 오류는 4xx 코드로 표시됩니다.
* 응답 수준, 이러한 오류는 JSON 응답의 &quot;오류&quot; 배열에 포함됩니다
* 레코드 수준이며 이러한 오류는 JSON 응답의 &quot;result&quot; 배열에 포함되며 &quot;status&quot; 필드 및 &quot;reasons&quot; 배열과 함께 개별 레코드 단위로 표시됩니다

### HTTP 오류

정상적인 작동 환경에서는 Marketo이 HTTP 상태 오류 413개와 요청 엔티티 너무 큼 및 요청 URI 414개만 반환해야 합니다. 이러한 기능은 모두 오류를 추적하고, 요청을 수정하고, 다시 시도하는 것을 통해 복구할 수 있지만, 스마트 코딩 사례를 사용하면 이러한 기능이 야생에서 발생하지 않아야 합니다. Marketo은 요청 페이로드가 1MB를 초과하는 경우 413을 반환하며, [리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Import-Leads)의 경우 10MB를 반환합니다. 대부분의 시나리오에서 이러한 제한에 도달할 가능성은 낮지만 요청 크기에 대한 검사를 추가하고 제한을 초과하는 레코드를 새 요청으로 이동하면 엔드포인트에서 이 오류가 반환되는 상황을 방지할 수 있습니다. GET 요청의 URI가 8KiB를 초과하면 414가 반환됩니다. 이를 방지하려면 쿼리 문자열의 길이를 확인하여 이 제한을 초과하는지 확인하십시오. 요청을 POST 메서드로 변경한 경우 추가 매개 변수 &#39;_method=GET&#39;를 사용하여 쿼리 문자열을 요청 본문으로 입력합니다. URI에 대한 제한을 무시합니다. 대부분의 경우 이 제한에 도달하는 것은 드물지만 GUID와 같은 긴 개별 필터 값이 있는 큰 레코드 일괄 처리를 검색하는 경우에는 다소 일반적입니다.

### 응답 수준 오류

응답의 &quot;성공&quot; 매개 변수가 false로 설정되어 있으면 응답 수준 오류가 표시됩니다. &quot;errors&quot;의 각 항목에는 6xx 또는 7xx의 두 멤버인 &quot;code&quot;와 오류에 대한 일반 텍스트 이유를 제공하는 &quot;message&quot;가 있습니다. 6xx 코드는 요청이 완전히 실패하여 실행되지 않았음을 항상 나타냅니다. 이것의 예는 601, &quot;유효하지 않은 액세스 토큰&quot;이며, 이는 요청을 통해 새로운 액세스 토큰을 재인증하고 전달하여 복구할 수 있습니다. 7xx 오류는 데이터가 반환되지 않았거나 요청이 잘못된 날짜를 포함하거나 필수 매개 변수가 누락되는 등 잘못 매개 변수화되었기 때문에 요청이 실패했음을 나타냅니다.

### 레코드 수준 오류

레코드 수준 오류는 개별 레코드에 대한 작업을 완료할 수 없지만 요청 자체는 유효했음을 나타냅니다. 응답의 &quot;결과&quot; 배열에 있는 개별 레코드 내에서 발생합니다. 이러한 레코드의 &quot;상태&quot; 필드는 &quot;생략&quot;되고 &quot;이유&quot; 배열이 표시됩니다. 각 이유에는 &quot;code&quot; 멤버와 &quot;message&quot; 멤버가 포함되어 있습니다. 코드는 항상 1xxx이며 메시지는 레코드가 생략된 이유를 나타냅니다. 예를 들어 리드 만들기/업데이트 요청에 &quot;action&quot;이 &quot;createOnly&quot;로 설정되어 있지만 제출된 레코드의 키 중 하나에 대해 리드가 이미 있는 경우가 있습니다. 이 경우 코드 1005를 반환하며 &quot;Lead 가 이미 존재합니다.&quot;라는 메시지가 표시됩니다. 다음 몇 개의 게시물에서는 복구 가능한 오류와 코드 내에서 이러한 오류를 처리하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

_케니_&#x200B;이(가) _2015-10-09_&#x200B;에 게시함

## 게스트 게시물 - Marketo 데이터베이스에 직접 SQL 커넥터

**Sumit Sarkar of Progress, Inc.의 게스트 게시물입니다.**

Marketo 데이터베이스에 대한 **SQL 커넥터** Marketo에는 데이터 액세스에 대한 API가 잘 문서화되어 있습니다. 그러나 조직에서 직접 SQL 액세스를 필요로 하는 경우가 있습니다. Marketing과 IT 사이의 Marketo 상점에서 표준 기반 SQL 연결 수요가 증가하고 있습니다. [Progress DataDirect Cloud](https://www.progress.com/connectors/cloud-data-integration)를 통해 Marketo에 직접 SQL 커넥터를 사용할 수 있습니다. DataDirect Cloud는 ODBC(&quot;Open Database Connectivity&quot;) 또는 JDBC(&quot;Java Database Connectivity&quot;), REST with OData(&quot;Open Data Protocol&quot;)에서 SQL 액세스를 위한 개방형 업계 표준을 통해 Marketo 데이터를 표시하는 데이터 연결 서비스입니다. 다음은 DataDirect Cloud를 사용하여 Marketo 데이터를 즉시 연결할 수 있도록 하는 일반적인 사용 사례입니다.

* 데이터 검색 및 시각화(Qlik, Tableau, SAP Lumira)
* 엔터프라이즈 보고 (SAP 비즈니스 객체, 마이크로전략, Cognos)
* 데이터 통합(SQL Server Integration Services - SSIS, Oracle Data Integrator - ODI, Informatica)
* 데이터 통합(SQL Server Linked Server, SAP Hana SDA, Oracle Database Gateway)
* Ad Hoc 쿼리(Microsoft Office, DB 시각화 도우미, Aqua Data Studio)
* 데이터 준비(Alteryx, Trifecta, Paxata)

**Marketo에 대한 SQL 액세스는 어떻게 작동합니까?**

* DataDirect Cloud는 Marketo의 통합 API로 노출된 데이터에 대한 논리 스키마를 만듭니다.
* DataDirect Cloud는 Marketo API에서 가져온 데이터에 대해 탄력적인 실시간 쿼리 엔진을 사용하여 소규모 ODBC 또는 JDBC 클라이언트의 SQL 요청을 처리합니다.
* DataDirect Cloud 연결은 데이터 중복 없이 직접적이고 실시간으로 수행됩니다.
* DataDirect Cloud Service은 최종 사용자가 API 버전 변경 또는 SOAP과 REST를 사용할 필요가 없도록 Marketo API를 추상화합니다.

DataDirect는 웹 서비스 API 위에 구축된 첫 번째 Salesforce ODBC 드라이버부터 2006년부터 SaaS 데이터 소스에 대한 이러한 연결 방식을 구축해 왔습니다. **Marketo 연결 시작:**

1. [DataDirect 클라우드 로그인에 등록](https://pacific.progress.com/console/register?productName=d2c&ignoreCookie=true)
1. &quot;데이터 소스&quot;를 클릭한 다음 &quot;+새 데이터 Source&quot; 단추
1. &quot;Marketo&quot;를 선택하고 연결 정보를 입력합니다. Marketo 관리자에게 문의하거나 로그인하여 [SOAP 통합에 대한 연결 정보](/help/soap-api/soap-api.md)를 찾을 수 있습니다.
1. &quot;연결 테스트&quot; 단추를 클릭합니다. Marketo에서 OData를 생성하는 OData 탭이 있으며 향후 블로그 게시물에서 논의할 예정입니다.
1. 노출된 Marketo 스키마를 검사하거나 UI 내에서 기본 SQL 쿼리를 실행하려면 &quot;SQL 테스트&quot;를 클릭합니다.
1. 왼쪽의 &quot;다운로드&quot;를 클릭하고 설치할 응용 프로그램 및 플랫폼에 대한 DataDirect Cloud ODBC 또는 JDBC 드라이버를 선택합니다.
1. DataDirect Cloud ODBC 또는 JDBC 드라이버가 설치되면 모든 표준 기반 응용 프로그램을 Marketo에 연결할 수 있습니다.

다음은 [DataDirect Cloud ODBC 클라이언트를 사용하여 연결](https://www.youtube.com/watch?v=H6PHra56Iig)하는 비디오 예입니다. 다음은 Marketo에 적용되는 다른 DataDirect Cloud 튜토리얼입니다.

* [SAP 데이터 분석](http://scn.sap.com/community/lumira/blog/2015/08/05/connect-sap-lumira-to-eloqua-marketo-google-analytics)
* [마이크로전략 엔터프라이즈 보고](https://community.microstrategy.com/t5/Tech-Corner/What-MSTR-developers-should-know-about-Cloud-Data-Sources/ba-p/253083)
* [Oracle 데이터 통합](https://www.ateam-oracle.com/post/a-universal-cloud-applications-adapter-for-odi/)

Marketo과 같은 클라우드 원본 간에 SQL 연결을 빌드하는 데 **R&amp;D 문제**

모든 SaaS API가 표준 쿼리 언어를 노출하는 것은 아닙니다. 이러한 경우 엔지니어링 팀은 각 객체를 개별적으로 봅니다. 각 객체는 호출, 필터링 검색 등을 위한 고유한 규칙을 갖는 상이한 API로 노출될 수 있다. 전체 데이터 모델에서 표준 경험 쿼리를 제공하는 데 상당한 노력이 필요했습니다.

전체 조인 기능 처리 SaaS API가 JOIN 기능이 있는 쿼리 언어를 지원하지 않는 경우 엔지니어링 팀이 해당 작업을 수행해야 합니다. 이렇게 하려면 SQL에서 번역을 수행하여 Marketo API를 효율적으로 호출하여 조인을 수행하기 전에 최소의 데이터 양을 반환해야 합니다. 두 개의 매우 큰 개체를 연결할 때 데이터 액세스 레이어는 응용 프로그램 서버나 데스크탑에서 상당한 리소스를 사용할 수 있습니다. 따라서 DataDirect Cloud와 같은 탄력적인 클라우드 서비스에 데이터 액세스 계층을 배포하는 것은 다음 두 가지 이유로 적절합니다.

1. 클라이언트 애플리케이션 서버 또는 데스크탑에서 더 빠른 성능 및 더 적은 메모리/CPU 리소스 사용
1. 사전 결합된 데이터 세트를 교환하는 DataDirect Cloud와 Marketo 간의 우수한 대역폭을 활용합니다.

데이터 모델을 처리하는 방법 정적입니까, 동적입니까? 변경 사항이 어떻게 감지되고 클라이언트에게 전달됩니까? 각 SaaS 데이터 소스는 서로 다르며, Marketo의 경우 뷰를 통해 특정 객체를 더 잘 쿼리하고 테이블을 통해 다른 객체를 더 잘 쿼리합니다. 모든 SaaS 소스에서 데이터 모델 및 개체의 매트릭스를 처리하는 것은 분명 어려운 일이었습니다.

개발자용 **Marketo 및 DataDirect Cloud 참조:**

* Marketo 연결 속성([문서에 연결](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html))
* Marketo에서 지원되는 SQL 및 확장([문서에 연결](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html,-hubspot,-and-marketo.html))
* 노출된 Marketo 테이블 및 뷰([문서에 연결](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html))
* Marketo에서 반환된 일반적인 오류 메시지([문서에 대한 링크](https://www.progress.com/output/DataDirect/DataDirectCloud/index.html))

**전기:** Sumit Sarkar는 Progress의 최고 데이터 전도사로 데이터 연결 분야에서 10년 이상 근무한 경험이 있습니다. 클라우드 데이터와의 개방형 데이터 표준 연결에 대한 세계 최고의 컨설턴트인 Sumit의 관심사는 분석을 위해 특허 출원 중인 기술을 개발한 데이터 액세스 계층의 성능 조정, SaaS 플랫폼을 위한 비즈니스 인텔리전스 및 데이터 웨어하우징, PaaS 환경을 위한 데이터 연결 등을 포함하며 ODBC, JDBC, ADO.NET 및 ODATA와 같은 표준을 중심으로 합니다. 그는 IBM Cognos Business Intelligence의 IBM 공인 컨설턴트이며 TDWI 멤버입니다. 그는 Dreamforce, Oracle OpenWorld, Strata Hadoop, MongoDB World, SAP Analytics 및 Business Objects Conference 등 다양한 컨퍼런스에서 데이터 연결에 대한 세션을 발표했습니다. Twitter: @SAsInSumit LinkedIn: [www.linkedin.com/in/meetsumit](http://www.linkedin.com/in/meetsumit)

_케니_&#x200B;이(가) _2015-12-07_&#x200B;에 게시함

## API 사용 및 오류 카운트에 대한 대시보드 만들기

Marketo API 소비자로서, 이는 눈여겨봐야 할 유용한 정보입니다. 시간 경과에 따른 트렌드를 감지하는 데 도움이 되는 내역 사용 데이터를 얻을 수 있다면 어떨까요? 통합의 상태를 측정하는 데 도움이 되는 API 오류 코드 요약을 얻을 수 있다면 어떻게 합니까? Marketo 기술 파트너로서 하나의 대시보드에서 모든 고객 계정에 걸쳐 사용 및 오류 데이터를 가져올 수 있다면 어떻게 됩니까? 이 게시물은 위의 질문에 답변할 수 있는 접근 방법을 제공할 것입니다. 안전벨트 매, 간다!
**통계 검색을 위한 예약된 작업** [일별 사용 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLast7DaysErrorsUsingGET) 및 [일별 오류 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyErrorsUsingGET) 끝점을 사용하여 사용 및 오류 데이터를 검색하는 앱을 만들어 보겠습니다. 앱은 하루에 한 번 실행되도록 예약되도록 설계되었습니다. 앱이 실행될 때마다 한 파일에 하루 동안의 사용 데이터를 추가하고 다른 파일에 하루 동안의 오류 데이터를 추가합니다. 매월 초에 새 파일 쌍이 만들어집니다. 이러한 파일은 언제든지 액세스할 수 있는 기록 레코드로 사용됩니다. 다음은 앱 논리입니다.

* 외부 소스에서 Marketo 계정 정보(Munchkin id 및 클라이언트 자격 증명)를 읽습니다. 참고: 이 소스는 다른 사용자가 계정 데이터에 액세스하지 못하도록 보호해야 합니다.
* 각 계정을 반복합니다.
   * 일일 사용량 가져오기 를 호출하여 하루 동안 사용 데이터를 검색합니다.
   * 일별 사용 데이터를 월별 &quot;사용&quot; 파일에 추가
   * 일일 오류 가져오기를 호출하여 하루 동안 오류 데이터를 검색합니다.
   * 일별 오류 데이터를 월별 &quot;오류&quot; 파일에 추가

출력 파일 형식 출력 파일의 형식은 해당 API 호출에서 반환된 &quot;결과&quot; 배열과 일치하는 JSON입니다(사용 및 오류). &quot;result&quot; 배열의 각 요소는 하루 동안의 데이터가 포함된 JSON 개체입니다. 출력 파일 이름 지정 출력 파일의 이름은 다음과 같습니다.

`<type>_<yyyy>_<mm>_<account>.json`

위치,

`<type>` - 데이터 유형(&quot;사용&quot; 또는 &quot;오류&quot;) `<yyyy>` - 연도(4자리) `<mm>` - 월(2자리) `<account>` - 계정 ID(Munchkin id)

출력 파일 예 usage_2015_10_111-AAA-222.json

```json
[
    { "date": "2015-10-15", "total": 0, "users" : [] },
    { "date": "2015-10-16", "total": 9, "users": [ { "userId": "some.body@yahoo.com", "count": 9 } ] },
    { "date": "2015-10-17", "total": 1120, "users": [ { "userId": "some.body@yahoo.com", "count": 200 }, { "userId": "some.body@marketo.com", "count": 200 }, { "userId": "some.body@gmail.com", "count": 720 } ] },
]
```

`errors_2015_10_111-AAA-222.json:`

```json
[
    { "date": "2015-10-15", "total":80, "errors": [ { "errorCode":"1003", "count":80 } ] },
    { "date": "2015-10-16", "total":148, "errors": [ { "errorCode":"612", "count":40 }, { "errorCode":"609", "count":70 }, { "errorCode":"1008", "count":38 } ] },
    { "date": "2015-10-17", "total":73, "errors": [ { "errorCode":"604", "count":1 }, { "errorCode":"609", "count":56 }, { "errorCode":"610", "count":16 } ] },
]
```

이 앱에 대한 코드는 이 게시물(Stats.java)의 끝에 있습니다. **Stats Web Service** 이제 이 데이터를 브라우저에 가져올 수 있는 방법이 필요합니다. 이 제안은 데이터를 전달할 웹 서비스를 만드는 것입니다. 웹 서비스는 앱의 출력 파일을 사용한 다음 데이터를 즉시 표시할 수 있는 양식으로 브라우저에 반환합니다. 단순성을 위해 동일한 원본 정책 제한을 해결하기 위해 [JSONP](https://en.wikipedia.org/wiki/JSONP) 패턴을 활용합니다. 다음은 외부 웹 서비스에 대해 제안된 REST 끝점 사양입니다. **URI**: /stats **메서드**: GET

**매개 변수**

**설명**

**예**

개월

이번 달 데이터를 검색합니다. 포함할 쉼표로 구분된 월 목록(2자리 표시). 기본값은 모든 달로 설정됩니다.

10,11

년

올해의 데이터를 검색합니다. 포함할 쉼표로 구분된 연도 목록(4자리 표시). 기본값은 모든 연도로 설정됩니다.

2015

account

이 계정에 대한 데이터를 검색합니다(Munchkin ID).

111-AAA-222

callback

JSON 콘텐츠를 래핑할 함수의 이름입니다.

processStats

요청 예

`GET //localhost:8080/stats?month=10&year=2015&account=111-AAA-222&callback=processStats`

웹 서비스는 &quot;사용량&quot; 및 &quot;오류&quot; 파일을 읽고 함께 결합하여 다음 형식으로 반환합니다.

```html
**<Name of Callback here>**

<Contents of Usage file here>,

<Contents of Error file here>
```

인수가 2개인 JSONP 콜백입니다. 첫 번째 인수는 usage &quot;result&quot; 배열입니다. 두 번째 인수는 오류 &quot;result&quot; 배열입니다. 응답 예

```json
processStats(
    [
        { "date": "2015-10-15", "total": 0, "users" : [] },
        { "date": "2015-10-16", "total": 9, "users": [ { "userId": "some.body@yahoo.com", "count": 9 } ] },
        { "date": "2015-10-17", "total": 1120, "users": [ { "userId": "some.body@yahoo.com", "count": 200 }, { "userId": "some.body@marketo.com", "count": 200 }, { "userId": "some.body@gmail.com", "count": 720 } ] }
    ],
    [
        { "date": "2015-10-15", "total":80, "errors": [ { "errorCode":"1003", "count":80 } ] },
        { "date": "2015-10-16", "total":148, "errors": [ { "errorCode":"612", "count":40 }, { "errorCode":"609", "count":70 }, { "errorCode":"1008", "count":38 } ] },
        { "date": "2015-10-17", "total":73, "errors": [ { "errorCode":"604", "count":1 }, { "errorCode":"609", "count":56 }, { "errorCode":"610", "count":16 } ] },
    ]
);
```

보시다시피 웹 서비스는 앱의 두 출력 파일 내용을 단순히 래핑했습니다. [Mocky](https://designer.mocky.io)를 사용하여 모의 웹 서비스 응답을 만들었습니다. 웹 서비스의 예제는 [입니다.](http://www.mocky.io/v2/5627b2f9270000f2226eec63?month=10&year=2015&account=111-AAA-222&callback=processStats) 이 웹 서비스 만들기는 독자를 위한 연습으로 남았습니다. **대시보드 웹 페이지** 이제 필요한 것은 웹 서비스를 호출하고 데이터 형식을 지정하는 웹 페이지뿐입니다. JSONP 패턴을 사용하려면 웹 서비스를 호출하는 `<script>` 태그를 추가해야 합니다.

`<script src="http: //<hostname>/stats?month=10&year=2015&account=284-RPR-133&callback=processStats"></script>`

이렇게 하면 웹 서비스 응답 본문이 HTML 페이지에 직접 삽입됩니다. 그런 다음 JSONP 콜백 함수 를 추가합니다.

```javascript
function processStats(usage, errors) {
    var cfg = { maxDepth: 5};
    document.write("<h2>Usage</h2>");
    document.body.appendChild(prettyPrint(usage, cfg));
    document.write("<h2>Errors</h2>");
    document.body.appendChild(prettyPrint(errors, cfg));
;
```

이 함수는 웹 서비스 호출 후에 자동으로 호출됩니다. 이 예제에서는 각 배열에서 [prettyPrint.js](https://github.com/padolsey-archive/prettyprint.js/tree/master)이라는 간단한 JavaScript &quot;variable dumper&quot;를 호출합니다. prettyPrint 함수는 배열의 콘텐츠를 사용하여 HTML 테이블을 생성합니다. 다음은 HTML 테이블의 스크린샷입니다. 보일라, 이게 우리 대시보드야! 이것이 그다지 우아하지는 않다는 것을 인정하지만, 무엇이 가능한지에 대한 생각을 당신에게 줄 것이다. 눈길을 끄는 시각화를 만들기 위해 원하는 방식으로 데이터를 변환하는 데 방해가 되는 것은 없습니다. HTML 페이지는 (Index.html) 아래에 있습니다. 다음 단계를 사용하여 브라우저에서 위의 테이블을 라이브로 볼 수 있습니다.

1. Index.html의 로컬 복사본 저장
1. prettyPrint.js의 로컬 복사본 저장
1. 브라우저에서 Index.html을 엽니다

그게 다에요. 이 게시물이 Marketo API 통계 모니터링에 대한 몇 가지 아이디어를 제공했으면 합니다. 해피 코딩! **Stats.java**

```java
package com.marketo;

// minimal-json library (https://github.com/ralfstx/minimal-json)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;

import java.io.\*;
import java.lang.reflect.Array;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.\*;

import java.nio.file.Files;
import java.nio.file.Paths;

import javax.net.ssl.HttpsURLConnection;

public class Stats {
    //
    // Define Marketo instance meta data here. Each row contains three elements: Account Id, Client Id, Client Secret.
    //
    // Note: that this information would typically be stored read from an external source (i.e. database)
    //
    // For example:
    //
    // private static String final CUSTOM_SERVICE_DATA[][] = {
    // {"111-AAA-222", "2f4a4435-f6fa-4bd9-3248-098754982345", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W"},
    // {"222-BBB-333", "5f4a6657-f6fa-4cd9-4356-123083238821", "gfjgfIVE9h4Jjcl59cOMAKFSk78ut12W"},
    // {"444-CCC-444", "9f4a4678-f6fa-4dd9-7735-908713247721", "xzcxvbVE9h4Jjcl59cOMAKFSk78ut12W"}
    // };
    //
    private static final String CUSTOM_SERVICE_DATA[][] = {
    };

    // Output directory for stats files
    private static final String OUTPUT_DIR = "C:stats";

public static void main(String[] args) {

    // Loop through each Marketo instance
    for (int i = 0; i < CUSTOM_SERVICE_DATA.length; i++) {

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
            CUSTOM_SERVICE_DATA[i][0]);

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
            baseUrl, "client_credentials", CUSTOM_SERVICE_DATA[i][1], CUSTOM_SERVICE_DATA[i][2]);

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(httpRequest("GET", identityUrl, null));
        String accessToken = identityObj.get("access_token").asString();

        // Compose Get Last 7 Days Usage URL
        String usageUrl = String.format("%s/rest/v1/stats/usage/last7days.json?access_token=%s",
            baseUrl, accessToken);

        // Compose Get Last 7 Days Errors URL
        String errorsUrl = String.format("%s/rest/v1/stats/errors/last7days.json?access_token=%s",
            baseUrl, accessToken);

        // Process usage data
        JsonObject usageObj = JsonObject.readFrom(httpRequest("GET", usageUrl, null));
        if (usageObj.get("success").asBoolean()) {
            if (usageObj.get("result") != null) {
                updateFile(usageObj, "usage", CUSTOM_SERVICE_DATA[i][0]);
            }
        }

        // Process errors data
        JsonObject errorsObj = JsonObject.readFrom(httpRequest("GET", errorsUrl, null));
        if (usageObj.get("success").asBoolean()) {
            if (errorsObj.get("result") != null) {
                updateFile(errorsObj, "errors", CUSTOM_SERVICE_DATA[i][0]);
            }
        }
    }
    System.exit(0);
}

// Write yesterday's data to output file
private static void updateFile(JsonObject usageObj, String statsType, String account){

    JsonArray usageResultAry = usageObj.get("result").asArray();
    JsonObject yesterdayUsageResultObj = usageResultAry.get(1).asObject();

    String yesterdayDate = yesterdayUsageResultObj.get("date").asString();
    String[] yesterdayDateAry = yesterdayDate.split("[-]+");

    // "C:statsstats_yyyy_mm_account.json"
    String statsFile = String.format("%s%s_%s_%s_%s.json",
        OUTPUT_DIR, statsType, yesterdayDateAry[0], yesterdayDateAry[1], account);

    // Create file
    File file = new File(statsFile);
    try {
        if (file.createNewFile()) {
            // created new file, seed with empty array
            FileWriter fw = new FileWriter(file.getAbsoluteFile());
            BufferedWriter bw = new BufferedWriter(fw);
            bw.write("[n]");
            bw.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }

    // Read file
    String content = null;
    try {
        content = new String(Files.readAllBytes(Paths.get(statsFile)));
    } catch (IOException e) {
        e.printStackTrace();
    }

    // Remove trailing "]", append new record, append trailing "]"
    content = content.substring(0, content.length() - 1);
    content += yesterdayUsageResultObj.toString();
    content += "n]";

    // Write file
    FileWriter fw = null;
    try {
        fw = new FileWriter(file.getAbsoluteFile());
        BufferedWriter bw = new BufferedWriter(fw);
        bw.write(content);
        bw.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
}

// Perform HTTP request
private static String httpRequest(String method, String endpoint, String body) {
    String data = "";
    try {
        URL url = new URL(endpoint);
        HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
        urlConn.setDoOutput(true);
        urlConn.setRequestMethod(method);
        switch (method) {
            case "GET":
                break;
            case "POST":
                urlConn.setRequestProperty("Content-type", "application/json");
                urlConn.setRequestProperty("accept", "text/json");
                OutputStreamWriter wr = new OutputStreamWriter(urlConn.getOutputStream());
                wr.write(body);
                wr.flush();
                break;
            default:
                System.out.println("Error: Invalid method.");
                return data;
        }
        int responseCode = urlConn.getResponseCode();
        if (responseCode == 200) {
            InputStream inStream = urlConn.getInputStream();
            data = convertStreamToString(inStream);
        } else {
            System.out.println(responseCode);
            data = "Status:" + responseCode;
        }
    } catch (MalformedURLException e) {
        System.out.println("URL not valid.");
    } catch (IOException e) {
        System.out.println("IOException: " + e.getMessage());
        e.printStackTrace();
    }
    return data;
}

private static String convertStreamToString(InputStream inputStream) {
    try {
        return new Scanner(inputStream).useDelimiter("A").next();
    } catch (NoSuchElementException e) {
        return "";
    }
}
}
```

**Index.html**

```html
<html>
<head>
<title>Marketo API Stats</title>
<!-- Browser JavaScript variable dumper                  -->
<!-- https://github.com/padolsey-archive/prettyprint.js  -->
<script src="prettyPrint.js"></script>
</head>
<body>

<h1>Marketo API Stats</h1>

<script>
// JSONP callback that uses prettyPrint to format API stats
function processStats(usage, errors) {
    var cfg = { maxDepth: 5};
    document.write("<h2>Usage</h2>");
    document.body.appendChild(prettyPrint(usage, cfg));
    document.write("<h2>Errors</h2>");
    document.body.appendChild(prettyPrint(errors, cfg));
};
</script>

<!-- Web service for you to implement as an exercise                                                        -->
<!-- <script src="http://localhost:8080/stats?month=10&account=111-AAA-222&callback=processStats"></script> -->

<!-- Mock web service that returns sample payload -->
<!-- http://www.mocky.io/                         -->
<script src="http://www.mocky.io/v2/5627b2f9270000f2226eec63?month=10&year=2015&account=111-AAA-222&callback=processStats"></script>"
</body>
</html>
```

_David_&#x200B;이(가) _2015-10-22_&#x200B;에 게시함

## Marketo REST API 예외 및 오류 처리: 3부

대부분의 경우 Marketo REST API에서 다시 받은 오류는 자동으로 복구할 수 없습니다. 그러나 자동으로 복구되거나 특정 유형의 오류가 표시되지 않는 경우가 있습니다.

### 요청 크기 오류

이 시리즈의 마지막 게시물에서 살펴보았듯이, Marketo은 URI가 길이가 8KiB를 초과하는 경우 414, 요청 본문이 1MB를 초과하는 경우 413 또는 리드 가져오기의 경우 10MB를 HTTP 상태 코드 414를 내보냅니다. 414는 드물지만 필터 유형별 잠재 고객 가져오기 를 사용하여 300개의 개별 GUID 또는 유사한 기준을 기반으로 레코드를 요청하는 경우 이러한 항목이 표시될 수 있습니다. 다음 요청이 있다고 가정해 보겠습니다. `<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?filterType=customGUID&fields=email`, company...firstName, lastName> 요청을 제출하면 URI가 8KiB를 초과하므로 Marketo에서 414 상태를 반환합니다.

이를 처리하려면 이 요청의 패턴을 변경하고 GET 대신 POST를 제출하고, &#39;_method=GET&#39;를 URI에 추가하고, 요청 본문의 쿼리 문자열을 x-www-form-urlencoded 요청으로 대신 전달해야 합니다. URI: `<https://AAA-BBB-CCC.mktorest.com/rest/v1/leads.json?_method=GET>` 요청 본문: filterType=customGUID&amp;fields=email,company...firstName, lastName HTTP 응답에서 이 예외를 catch하는 대신 런타임 시 요청의 총 길이를 확인하고 URI가 8k를 초과하는 경우 이 대체 패턴을 배포할 수 있습니다. 또는 모든 경우에 POST 메서드를 사용하여 레코드를 일괄 검색할 수 있습니다. 413의 경우 유사한 패턴을 따라 직렬화 단계 동안 레코드를 추가할 때 요청 본문의 길이를 확인하고 이 제한을 초과할 경우 요청을 여러 부분으로 분할할 수 있습니다.

### 인증 오류

복구 가능한 오류의 다음 클래스는 인증과 관련이 있습니다. 만료된 후 이전에 유효한 액세스 토큰이 사용되면 첫 번째 사용에서 602, &quot;액세스 토큰이 만료됨&quot;이라는 오류 코드를 반환합니다. 이 경우 동일한 토큰을 사용하면 601, &quot;잘못된 액세스 토큰&quot;이 반환됩니다. 대상 구독에 대해 유효한 액세스 토큰이 아닌 문자열을 다른 방식으로 사용하면 601이 발생합니다. 두 경우 모두 실패한 요청을 다시 시도하여 새 액세스 토큰을 재인증하고 전달하여 에서 이 오류를 복구할 수 있습니다.

### 시간 초과

매우 드문 상황에서 호출은 30초 시간 제한 기간이 경과한 후 604, &quot;요청 시간 초과&quot;를 반환할 수 있습니다. 리드 생성/업데이트와 같은 일괄 처리된 요청의 경우, 요청이 더 작은 배치로 분할되어 성공이 반환될 때까지 재시도할 수 있습니다(배치가 100개 미만의 레코드로 분할되고 요청이 여전히 시간 초과된 경우 지원 사례를 제출해야 할 수 있습니다). 가장 일반적인 다른 사례는 자산 승인 호출입니다. 다른 사용자 또는 서비스에 의해 현재 승인된 레코드에 대한 잠금이 있을 수 있습니다(예: [이메일](https://developer.adobe.com/marketo-apis/api/asset/approve-email-by-id/) 또는 [이메일 템플릿](https://developer.adobe.com/marketo-apis/api/asset/approve-email-template-by-id/)의 경우). 이 경우 기존 잠금을 해결하기 위해 다시 시도에 [지수 백오프](https://en.wikipedia.org/wiki/Exponential_backoff)를 사용해야 합니다. 앞으로 몇 주 이내에 복구할 수 없는 특정 오류를 자세히 살펴볼 시리즈의 마지막 부분을 다시 살펴보십시오.

_케니_&#x200B;이(가) _2015-10-30_&#x200B;에 게시함

## Marketo 보안 개선 사항

Marketo에서는 보안을 중요하게 생각합니다. **[업계 전체 이니셔티브](https://security.googleblog.com/2014/09/gradually-sunsetting-sha-1.html)**&#x200B;의 일부로, Marketo은 보안 보호를 강화하기 위해 웹 인증 및 암호화를 업그레이드하고 있습니다. 롤아웃은 2011년 12월 12일에 발생할 예정입니다. **영향을 받는 사람** 10년 이상이며 최근에 업데이트되지 않은 시스템에서 Marketo에 통합한 사용자만 영향을 받습니다. 지원되는 시스템 및 버전에 대한 자세한 내용은 **[이 목록](https://www.digicert.com/faq/sha2/sha-2-compatibility)**&#x200B;을 참조하세요. **다음 사용자는 영향을 받지 않습니다.**

* 최신 브라우저를 통해 Marketo.com에 액세스하는 최종 사용자([목록 보기](https://www.digicert.com/faq/sha2/sha-2-compatibility))
* Informatica, Dell Boomi, Scribe 등의 통합 파트너를 사용하는 고객
* Launchpoint 파트너를 사용하는 고객.

다른 모든 Marketo 도메인은 이미 SHA2 인증서를 사용합니다.

_케니_&#x200B;이(가) _2015-11-18_&#x200B;에 게시함

## REST API를 사용하는 활동에 대한 폴링

활동은 Marketo Platform의 핵심 개체입니다. 활동은 모든 웹 페이지 방문, 이메일 열기, 웨비나 출석 또는 트레이드 쇼 출석에 대해 저장되는 행동 데이터입니다. 일반적인 사용 사례는 활동 데이터를 조직의 다른 부분에 있는 데이터와 결합하는 것입니다. 이 샘플 프로그램에는 6개의 단계가 포함되어 있습니다.

1. 지정된 날짜/시간에 만든 모든 활동 레코드 목록을 생성하려면 [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)를 호출하십시오. 필터를 사용하여 반환되는 활동 레코드 유형을 제한합니다.
1. 각 활동 레코드에서 관심 필드를 추출합니다.
1. [필터 유형별 여러 잠재 고객 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadsByFilterUsingGET)를 호출하여 1단계의 활동에 해당하는 잠재 고객 레코드 목록을 생성합니다. 2단계의 활동 레코드에서 추출된 leadId 필드를 필터로 사용하여 반환되는 리드를 지정합니다.
1. 각 리드 레코드에서 관심 필드를 추출합니다.
1. 2단계의 활동 데이터를 4단계의 리드 데이터와 결합합니다.
1. 5단계의 데이터를 외부 시스템에서 사용할 수 있는 형식으로 변환합니다.

아래 다이어그램에서 볼 수 있듯이 이 예제에서는 이메일 관련 활동을 캡처하도록 선택했습니다.

**프로그램 입력** 기본적으로 프로그램은 변경 내용을 찾기 위해 현재 날짜로부터 하루 후에 다시 시작됩니다. 따라서 이 프로그램을 매일 같은 시간에 실행할 수 있습니다. 시간을 거슬러 올라가기 위해 일 수를 명령줄 인수로 지정하여 시간 창을 효과적으로 늘릴 수 있습니다. 프로그램에는 수정할 수 있는 여러 변수 CUSTOM_SERVICE_DATA 가 포함되어 있습니다. 이 변수에는 Marketo 사용자 지정 서비스 데이터(계정 ID, 클라이언트 ID, 클라이언트 암호)가 포함되어 있습니다. READ_BATCH_SIZE - 한 번에 검색할 레코드 수입니다. 이 옵션을 사용하여 본문 크기에 대한 응답을 조정합니다. LEAD_FIELDS - 수집하려는 리드 필드 목록이 포함되어 있습니다. ACTIVITY_TYPES - 수집하려는 활동 유형 목록이 포함되어 있습니다.

**프로그램 논리** 먼저 시간 창을 설정하고, REST 끝점 URL을 구성하고, 인증 액세스 토큰을 얻습니다. 다음으로 활동 공급을 소진할 때까지 실행되는 페이징 토큰 가져오기/리드 활동 가져오기 루프를 실행합니다. 이 루프의 목적은 활동 레코드를 검색하고 해당 레코드에서 관심 필드를 추출하는 것입니다. 리드 활동 가져오기에는 다음 활동 유형만 찾도록 지시합니다.

* 이메일 전달됨
* 이메일 구독 취소
* 이메일 열람
* 이메일을 클릭합니다.

각 활동 레코드에서 다음 관심 필드를 추출합니다.

* leadId
* activityType
* activityDate
* primaryAttributeValue

목적에 맞게 활동 유형과 활동 필드의 조합을 자유롭게 선택할 수 있습니다. 다음으로 리드 공급을 소진할 때까지 실행되는 필터 유형별 다중 리드 가져오기 루프를 실행합니다. 일련의 &quot;filterValues&quot; 매개 변수와 함께 &quot;filterType=id&quot; 매개 변수를 사용하여 이전에 검색한 활동과 연관된 잠재 고객으로만 검색된 잠재 고객 레코드를 제한합니다. 각 리드 레코드에서 다음 관심 필드를 추출합니다.

* 이름
* 성
* 이메일

원하는 리드 필드를 선택할 수 있습니다. 다음으로 잠재 고객 ID를 사용하여 함께 연결하여 잠재 고객 필드를 활동 필드와 연결합니다. 마지막으로, 모든 데이터를 반복해서 JSON 형식으로 변환한 다음 콘솔에 인쇄합니다. **프로그램 출력** 다음은 샘플 프로그램의 출력 예입니다. 활동 필드와 잠재 고객 필드가 JSON &quot;결과&quot; 개체로 함께 결합된 것을 보여 줍니다. 여기에서는 이 JSON을 외부 웹 서비스에 요청 페이로드로 전달할 수 있다는 아이디어가 제공됩니다.

```json
{
    "result": [
        {
            "leadId": 318581,
            "activityType": "Email Delivered",
            "activityDate": "2015-03-17T20:00:06Z",
            "primaryAttributeValue": "My Email Program",
            "firstName": "David",
            "lastName": "Everly",
            "email": "everlyd@marketo.com"
        },
        {
            "leadId":318581,
            "activityType":"Open Email",
            "activityDate":"2015-03-17T23:23:12Z",
            "primaryAttributeValue":"My Email Program - Auto Response",
            "firstName":"David",
            "lastName":"Everly",
            "email":"everlyd@marketo.com"
       },
        ... more result objects here...
    ]
}
```

**프로그램 코드**

```java
package com.marketo;

// minimal-json library (https://github.com/ralfstx/minimal-json)
import com.eclipsesource.json.JsonArray;
import com.eclipsesource.json.JsonObject;
import com.eclipsesource.json.JsonValue;

import java.io.\*;
import java.net.MalformedURLException;
import java.net.URL;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.\*;

import javax.net.ssl.HttpsURLConnection;

public class LeadActivities {
//
// Define Marketo REST API access credentials: Account Id, Client Id, Client Secret.  For example:
    private static Map<String, String> CUSTOM_SERVICE_DATA;
    static {
        CUSTOM_SERVICE_DATA = new HashMap<String, String>();
//        CUSTOM_SERVICE_DATA.put("accountId", "111-AAA-222");
//        CUSTOM_SERVICE_DATA.put("clientId", "2f4a4435-f6fa-4bd9-3248-098754982345");
//        CUSTOM_SERVICE_DATA.put("clientSecret", "asdf6IVE9h4Jjcl59cOMAKFSk78ut12W");
    }

    // Number of lead records to read at a time
    private static final String READ_BATCH_SIZE = "200";

    // Lookup lead records using lead id as primary key
    private static final String LEAD_FILTER_TYPE = "id";

    // Lead record lookup returns these fields
    private static final String LEAD_FIELDS = "firstName,lastName,email";

    // Lookup activity records for these activity types
    private static Map<Integer, String> ACTIVITY_TYPES;
    static {
        ACTIVITY_TYPES = new HashMap<Integer, String>();
        ACTIVITY_TYPES.put(7, "Email Delivered");
        ACTIVITY_TYPES.put(9, "Unsubscribe Email");
        ACTIVITY_TYPES.put(10, "Open Email");
        ACTIVITY_TYPES.put(11, "Click Email");
    }

    public static void main(String[] args) {
        // Command line argument to set how far back to look for lead changes (number of days)
        int lookBackNumDays = 1;
        if (args.length == 1) {
            lookBackNumDays = Integer.parseInt(args[0]);
        }

        // Establish "since date" using current timestamp minus some number of days (default is 1 day)
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DAY_OF_MONTH, -lookBackNumDays);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssZ");
        String sinceDateTime = sdf.format(cal.getTime());

        // Compose base URL
        String baseUrl = String.format("https://%s.mktorest.com",
            CUSTOM_SERVICE_DATA.get("accountId"));

        // Compose Identity URL
        String identityUrl = String.format("%s/identity/oauth/token?grant_type=%s&client_id=%s&client_secret=%s",
                baseUrl, "client_credentials", CUSTOM_SERVICE_DATA.get("clientId"), CUSTOM_SERVICE_DATA.get("clientSecret"));

        // Call Identity API
        JsonObject identityObj = JsonObject.readFrom(getData(identityUrl));
        String accessToken = identityObj.get("access_token").asString();

        // Compose URLs for Get Lead Changes, and Get Paging Token
        String activityTypesUrl = String.format("%s/rest/v1/activities/types.json?access_token=%s",
                baseUrl, accessToken);
        String pagingTokenUrl = String.format("%s/rest/v1/activities/pagingtoken.json?access_token=%s&sinceDatetime=%s",
                baseUrl, accessToken, sinceDateTime);

        // Use activity ids to create filter parameter
        String activityTypeIds = "";
        for (Integer id : ACTIVITY_TYPES.keySet()) {
            activityTypeIds += "&activityTypeIds=" + id.toString();
        }

        // Compose URL for Get Lead Activities
        // Only retrieve activities that match our defined activity types
        String leadActivitiesUrl = String.format("%s/rest/v1/activities.json?access_token=%s%s&batchSize=%s",
                baseUrl, accessToken, activityTypeIds, READ_BATCH_SIZE);

        Map<Integer, List> activitiesMap = new HashMap<Integer, List>();
        Set leadsSet = new HashSet();

        // Call Get Paging Token API
        JsonObject pagingTokenObj = JsonObject.readFrom(getData(pagingTokenUrl));
        if (pagingTokenObj.get("success").asBoolean()) {
            String nextPageToken = pagingTokenObj.get("nextPageToken").asString();
            boolean moreResult;
            do {
                moreResult = false;

                // Call Get Lead Activities API to retrieve activity data
                JsonObject leadActivitiesObj = JsonObject.readFrom(getData(String.format("%s&nextPageToken=%s",
                        leadActivitiesUrl, nextPageToken)));
                if (leadActivitiesObj.get("success").asBoolean()) {
                    moreResult = leadActivitiesObj.get("moreResult").asBoolean();
                    nextPageToken = leadActivitiesObj.get("nextPageToken").asString();

                    if (leadActivitiesObj.get("result") != null) {
                        JsonArray activitiesResultAry = leadActivitiesObj.get("result").asArray();
                        for (JsonValue activitiesResultObj : activitiesResultAry) {

                            // Extract activity fields of interest (leadID, activityType, activityDate, primaryAttributeValue)
                            JsonObject leadObj = new JsonObject();
                            int leadId = activitiesResultObj.asObject().get("leadId").asInt();
                            leadObj.add("activityType", ACTIVITY_TYPES.get(activitiesResultObj.asObject().get("activityTypeId").asInt()));
                            leadObj.add("activityDate", activitiesResultObj.asObject().get("activityDate").asString());
                            leadObj.add("primaryAttributeValue", activitiesResultObj.asObject().get("primaryAttributeValue").asString());

                            // Store JSON containing activity fields in a map using lead id as key
                            List leadLst = activitiesMap.get(leadId);
                            if (leadLst == null) {
                                activitiesMap.put(leadId, new ArrayList());
                                leadLst = activitiesMap.get(leadId);
                            }
                            leadLst.add(leadObj);

                            // Store unique lead ids for use as lead filter value below
                            leadsSet.add(leadId);
                        }
                    }
                }
            } while (moreResult);
        }

        // Use unique lead id values to create filter parameter
        String filterValues = "";
        for (Object object : leadsSet) {
            if (filterValues.length() > 0) {
                filterValues += ",";
            }
            filterValues += String.format("%s", object);
        }

        // Compose Get Multiple Leads by Filter Type URL
        // Only retrieve leads that match the list of lead ids that was accumulated during activity query
        String getMultipleLeadsUrl = String.format("%s/rest/v1/leads.json?access_token=%s&filterType=%s&fields=%s&filterValues=%s&batchSize=%s",
                baseUrl, accessToken, LEAD_FILTER_TYPE, LEAD_FIELDS, filterValues, READ_BATCH_SIZE);
        String nextPageToken = "";

        do {
            String gmlUrl = getMultipleLeadsUrl;

            // Append paging token to Get Multiple Leads by Filter Type URL
            if (nextPageToken.length() > 0) {
                gmlUrl = String.format("%s&nextPageToken=%s", getMultipleLeadsUrl, nextPageToken);
            }

            // Call Get Multiple Leads by Filter Type API to retrieve lead data
            JsonObject multipleLeadsObj = JsonObject.readFrom(getData(gmlUrl));
            if (multipleLeadsObj.get("success").asBoolean()) {
                if (multipleLeadsObj.get("result") != null) {
                    JsonArray multipleLeadsResultAry = multipleLeadsObj.get("result").asArray();

                    // Iterate through lead data
                    for (JsonValue leadResultObj : multipleLeadsResultAry) {
                        int leadId = leadResultObj.asObject().get("id").asInt();

                        // Join activity data with lead fields of interest (firstName, lastName, email)
                        List leadLst = activitiesMap.get(leadId);
                        for (JsonObject leadObj : leadLst) {
                            leadObj.add("firstName", leadResultObj.asObject().get("firstName").asString());
                            leadObj.add("lastName", leadResultObj.asObject().get("lastName").asString());
                            leadObj.add("email", leadResultObj.asObject().get("email").asString());
                        }
                    }
                }
            }

            nextPageToken = "";
            if (multipleLeadsObj.asObject().get("nextPageToken") != null) {
                nextPageToken = multipleLeadsObj.get("nextPageToken").asString();
            }
        } while (nextPageToken.length() > 0);

        // Now place activity data into an array of JSON objects
        JsonArray activitiesAry = new JsonArray();
        for (Map.Entry<Integer, List> activity : activitiesMap.entrySet()) {
            int leadId = activity.getKey();
            for (JsonObject leadObj : activity.getValue()) {
                // do something with leadId and each leadObj
                leadObj.add("leadId", leadId);
                activitiesAry.add(leadObj);
            }
        }

        // Print out result objects
        JsonObject result = new JsonObject();
        result.add("result", activitiesAry);
        System.out.println(result);

        System.exit(0);
    }

    // Perform HTTP GET request
    private static String getData(String endpoint) {
        String data = "";
        try {
            URL url = new URL(endpoint);
            HttpsURLConnection urlConn = (HttpsURLConnection) url.openConnection();
            urlConn.setRequestMethod("GET");
            urlConn.setAllowUserInteraction(false);
            urlConn.setDoOutput(true);
            int responseCode = urlConn.getResponseCode();
            if (responseCode == 200) {
                InputStream inStream = urlConn.getInputStream();
                data = convertStreamToString(inStream);
            } else {
                System.out.println(responseCode);
                data = "Status:" + responseCode;
            }
        } catch (MalformedURLException e) {
            System.out.println("URL not valid.");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
            e.printStackTrace();
        }
        return data;
    }

    private static String convertStreamToString(InputStream inputStream) {
        try {
            return new Scanner(inputStream).useDelimiter("A").next();
        } catch (NoSuchElementException e) {
            return "";
        }
    }
}
```

다 됐습니다. 해피 코딩!

_David_&#x200B;이(가) _2015-11-20_&#x200B;에 게시함

## SoundCloud 플레이어와 Munchkin API 통합

SoundCloud는 인디 록 액트를 꿈꾸는 사람부터 음악 산업의 최정상의 EDM 아티스트, 스토리텔링 팟캐스트에 이르기까지 모든 것에 대해 풍부한 분석과 기능을 갖춘 놀라운 오디오 호스팅 플랫폼을 제공합니다. 플랫폼의 놀라운 기본 기능과 함께 데이터를 이동하고 청취 동작을 추적할 수 있는 세계적 수준의 API 프로그램을 제공합니다. 이 기능은 팟캐스트에 특히 유용하며, 이를 통해 재생, 일시 중지 및 공유와 같은 특정 수신 동작을 스크립트 및 오디오의 특정 콘텐츠에 연관시킬 수 있습니다. 오늘은 Marketo에서 이러한 활동을 보내고 추적하기 위해 [SoundCloud의 위젯 API](https://developers.soundcloud.com/docs/api/html5-widget)를 활용하는 방법을 살펴보겠습니다. 먼저 잠재 고객의 활동 로그인 Marketo에 기록될 Munchkin 활동 생성을 살펴보겠습니다. 가장 기본적으로 Munchkin.munchkinFunction을 호출하고 &quot;visitWebPage&quot;를 첫 번째 인수로 전달합니다. 이렇게 하면 Marketo으로 방문 웹 페이지 활동이 기록되고 메서드에 전달되는 임의의 URL 및 쿼리 문자열 데이터가 기록됩니다. 두 번째 인수는 데이터가 포함된 JavaScript 개체를 승인하며, 이 개체에는 두 멤버 &quot;url&quot; 및 &quot;params&quot;가 모두 있습니다. url 멤버는 Marketo 활동의 웹 페이지에 해당하고, params는 쿼리 문자열에 해당합니다. 목적을 위해 url은 SoundCloud 관련 작업, &quot;soundCloudInteraction&quot;의 식별자로 사용되며 매개 변수에는 특정 활동에 대한 추가 데이터가 포함됩니다. 다음은 각 작업을 추적하는 데 사용하는 함수입니다.

```javascript
var trackActivity = function(action){

    //set action param to be the string passed to the function
    var qs = "action=" + action;

    //use getCurrentSound callback to get the name of the current track
    soundCloudMunchkin.widget.getCurrentSound(function(currentSound){

        //add it to our querystring
        qs = qs + "&sound=" + currentSound.title;

        //use the getPosition callback to get the position of the track in ms
        soundCloudMunchkin.widget.getPosition(function(position){

            //add it to the querystring
            qs = qs + "&position=" + position;

            //assemble our data object for the munchkin activity
            var dataObject = {
                "url": "soundCloudInteraction",
                "params": qs
            }

            //call the munchkinFunction to submit the activity
            Munchkin.munchkinFunction("visitWebPage", dataObject);
        });
    });
}
```

표준 SoundCloud 위젯은 iframe에 포함되어 있으므로 위젯은 post 메시지를 사용하여 통신하며 콜백을 사용하여 데이터를 가져와야 합니다. currentSound 및 getPosition 메서드에서 볼 수 있듯이 말이죠. SoundCloud 위젯 API는 플레이어의 개별 이벤트에 응답하고 JavaScript에 제출하는 데 사용할 수 있는 Marketo 콜백 세트를 제공합니다. 우리가 관심을 갖는 이벤트는 사용자가 무엇을 듣는지, 얼마나 오래 듣는지, 그리고 사용자가 플레이어와 어떤 상호 작용을 하는지에 대한 것이므로 우리는 다음의 이벤트를 살펴봅니다.

* 재생
* 일시 중지
* 완료
* 찾기
* CLICK_DOWN
* CLICK_BUY
* OPEN_SHARE_PANEL

또한 위젯에서 bind() 메서드를 사용하여 이러한 각 이벤트에 콜백을 추가해야 합니다. 한 가지 예를 살펴보겠습니다.

```javascript
widget.bind(SC.Widget.Events.PLAY, function(){
    soundCloudMunchkin.trackPlay();
});
```

이렇게 하면 트랙이 재생될 때마다 trackPlay 메서드를 실행하여 현재 트랙에 대한 데이터로 이벤트를 Marketo에 보내게 됩니다. 전체 스크립트는 [여기](https://gist.github.com/kelkingtron/6750bb07c1397d93d9c7#file-soundcloudmunchkin-js)에 있습니다. SoundCloudMunchkin 개체에는 SoundCloud 위젯 개체를 유일한 인수로 허용하는 init 메서드가 있습니다. 이 메서드는 추적 메서드를 관련 콜백에 바인딩하고 Marketo에 대한 활동을 추적하도록 위젯을 설정합니다. 페이지에 [Munchkin 코드](/help/javascript-api/lead-tracking.md)와 [SoundCloud API 라이브러리](https://w.soundcloud.com/player/api.js)를 로드해야 합니다. 실제 SoundCloud 위젯을 포함하는 것 외에도 모든 것을 초기화해야 합니다.

```javascript
window.onload=function(){
var iframe = document.getElementById(iframeId);
    if(iframe) {
        widget = SC.Widget(iframe);
        soundCloudMunchkin.init(widget);
    };
};
```

_케니_&#x200B;이(가) _2015-12-21_&#x200B;에 게시함

## RTP 및 EU E-Privacy Directive

이 게시물에서는 RTP를 사용하여 웹 사이트 방문자에게 추적되고 있음을 알리거나 유럽 방문자에 대한 추적을 자동으로 비활성화하는 방법을 설명합니다. 2012년 이후 유럽 방문자가 이용할 수 있는 모든 웹 사이트는 EU E-Privacy Directive를 준수해야 합니다. 2011년에 새로운 법이 발효되었는데, 이 법은 신원 확인 정보가 사용자의 지식과 동의 없이 사용자의 컴퓨터에 저장되는 것을 방지합니다. 중요하지 않은 추적을 위해 쿠키 또는 기타 기술을 사용하는 경우 다음을 수행해야 합니다.

1. 사용자에게 추적 기술이 사용됨을 알립니다.
1. 이러한 기술을 사용하는 이유를 설명하십시오.
1. 해당 기술을 사용하기 전에 사용자의 동의를 얻고 언제든지 허가를 철회할 수 있도록 한다.

_Yanir_&#x200B;이(가) _1970-01-01_&#x200B;에 게시

## AP를 사용하여 Marketo에서 고객 및 잠재 고객 정보 업데이트

독점 시스템을 사용하여 고객 및 잠재 고객 정보를 업데이트하는 시나리오가 있습니다. 마케팅 팀은 이러한 업데이트를 Marketo에 다시 반영하여 마케팅 캠페인에 사용할 가장 정확한 기록 시스템을 보유하려고 합니다. 아래 접근 방식을 사용하면 Marketo에 정기적으로 업로드하여 해당 소유 시스템에서 수정된 데이터로 Marketo 연락처 정보를 계속 업데이트할 수 있습니다. 아래 다이어그램은 설정된 정기 타이머에서 발생하는 API 호출을 보여 줍니다. 주기적 타이머가 트리거되면 클라이언트 로직은 먼저 독점 시스템에서 업데이트된 연락처를 검색합니다. 이 작업을 수행하는 방법은 API를 사용하거나 독점 시스템의 데이터 내보내기를 사용하는 시스템마다 다릅니다. 업데이트된 연락처 정보가 검색되면 실행되는 Marketo API에 대해 자세히 설명합니다. syncMultipleLead에 대한 SOAP 요청:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:paramsSyncMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <leadRecordList>
    <leadRecord>
      <Email>henry@superstar.com</Email>
      <ns2:leadAttributeList>
        <attribute>
          <attrName>FirstName</attrName>
          <attrValue>Henry</attrValue>
        </attribute>
        <attribute>
          <attrName>LastName</attrName>
          <attrValue>Adams</attrValue>
        </attribute>
        <attribute>
          <attrName>Title</attrName>
          <attrValue>Director of Demand Generation</attrValue>
        </attribute>
      </ns2:leadAttributeList>
    </leadRecord>
    <leadRecord>
      <Email>ssmith@gmail.com</Email>
      <ns2:leadAttributeList>
        <attribute>
          <attrName>FirstName</attrName>
          <attrValue>Suzie</attrValue>
        </attribute>
        <attribute>
          <attrName>LastName</attrName>
          <attrValue>Smith</attrValue>
        </attribute>
        <attribute>
          <attrName>Title</attrName>
          <attrValue>VP Marketing</attrValue>
        </attribute>
      </ns2:leadAttributeList>
    </leadRecord>
  </leadRecordList>
  <dedupEnabled>true</dedupEnabled>
</ns2:paramsSyncMultipleLeads>
```

syncMultilpeLeads의 SOAP 응답:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns2:successSyncMultipleLeads xmlns:ns2="<http://www.marketo.com/mktows/">
  <result>
    <syncStatusList>
      <syncStatus>
        <leadId>1094593</leadId>
        <status>UPDATED</status>
        <error xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
      </syncStatus>
      <syncStatus>
        <leadId>1094594</leadId>
        <status>UPDATED</status>
        <error xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:nil="true" />
      </syncStatus>
    </syncStatusList>
  </result>
</ns2:successSyncMultipleLeads>
```

`syncMultipleLeads`에서 업데이트 작업을 수행합니다. 제출된 이메일 주소를 기반으로 Marketo 내에 이미 연락처가 있는 경우 특성이 업데이트됩니다. 연락처가 없으면 생성됩니다. `syncMultipleLeads`의 응답이 제출된 각 연락처의 상태를 반환합니다. `<attrName/>` 내의 `<leadAttributeList/>` 값은 해당 Marketo 구독에 대해 정의된 SOAP API 이름과 일치해야 합니다. 필드 이름을 내보내서 Marketo 관리 패널의 필드 관리 섹션 내에서 SOAP API 이름을 검색할 수 있습니다.

위에서 설명한 시나리오를 실행하는 아래 샘플 Java 프로그램을 참조하십시오.

```java
 import com.marketo.mktows.\*;
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
import java.util.\*;

public class SyncMultipleLeadsExample {

  public static void main(String[] args) {

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
      ParamsSyncMultipleLeads request = new ParamsSyncMultipleLeads();

      ObjectFactory objectFactory = new ObjectFactory();

      JAXBElement dedup = objectFactory.createParamsSyncMultipleLeadsDedupEnabled(true);
      request.setDedupEnabled(dedup);

      // The list of contacts defined here would be retrieved from the proprietary system
      Contact contact = new Contact("Henry","Adams","henry@superstar.com", "Director of Demand Generation");
      Contact contact2 = new Contact("Suzie","Smith","ssmith@gmail.com", "VP Marketing");

      ArrayList updatedContacts = new ArrayList();
      updatedContacts.add(contact);
      updatedContacts.add(contact2);

      ArrayOfLeadRecord arrayOfLeadRecords = new ArrayOfLeadRecord();

      Iterator it = updatedContacts.iterator();
      while(it.hasNext())
      {
        Contact c = it.next();

        LeadRecord leadRec = new LeadRecord();

        JAXBElement email = objectFactory.createLeadRecordEmail(c.email);
        leadRec.setEmail(email);

        Attribute attr1 = new Attribute();
        attr1.setAttrName("FirstName");
        attr1.setAttrValue(c.fname);

        Attribute attr2 = new Attribute();
        attr2.setAttrName("LastName");
        attr2.setAttrValue(c.lname);

        Attribute attr3 = new Attribute();
        attr3.setAttrName("Title");
        attr3.setAttrValue(c.title);

        ArrayOfAttribute aoa = new ArrayOfAttribute();
        aoa.getAttributes().add(attr1);
        aoa.getAttributes().add(attr2);
        aoa.getAttributes().add(attr3);

        QName qname = new QName("http://www.marketo.com/mktows/", "leadAttributeList");
        JAXBElement attrList = new JAXBElement(qname, ArrayOfAttribute.class, aoa);

        leadRec.setLeadAttributeList(attrList);
        arrayOfLeadRecords.getLeadRecords().add(leadRec);

      }

      request.setLeadRecordList(arrayOfLeadRecords);

      JAXBContext context = JAXBContext.newInstance(SuccessSyncMultipleLeads.class);
      Marshaller m = context.createMarshaller();
      m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
      m.marshal(request, System.out);

      SuccessSyncMultipleLeads result = port.syncMultipleLeads(request, header);

      m.marshal(result, System.out);
    }

    catch(Exception e) {
      e.printStackTrace();
    }
  }

  public static class Contact {
    public String fname, lname, email, title;

      public Contact(String fname, String lname, String email, String title) {
          this.fname = fname;
          this.lname = lname;
          this.email = email;
          this.title = title;
      }
  }
}
```

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_Travis Kaufman_&#x200B;이(가) _2014-03-24_&#x200B;에 게시함

## API를 사용하여 Marketo에서 트랜잭션 이메일 보내기

Marketo UI를 사용하여 기존 스마트 캠페인을 만들어야 합니다. 또한 이메일 수신자가 Marketo에 있어야 합니다. 따라서 requestCampaign API를 호출하기 전에 [getLead API]&#x200B;(/help/soap-api/getlead.md)를 사용하여 이메일이 Marketo에 있는지 확인하십시오. requestCampaign API를 통해 호출한 후 스마트 캠페인이 Marketo에서 실행되었는지 확인하여 확인할 수 있습니다. 먼저 스마트 캠페인을 만드는 방법, 두 번째 API를 통해 캠페인을 전송하는 트리거를 설정하는 방법, 세 번째 흐름 작업의 일부로 이메일을 정의하는 방법 및 네 번째 이 캠페인을 실행하는 데 사용되는 코드 샘플을 보여 줍니다.
**Marketo에서 새 스마트 캠페인을 만드는 방법** Marketo의 스마트 캠페인은 모든 마케팅 활동을 실행합니다. 일련의 자동화된 작업을 설정하여 스마트 연락처 목록에 추가할 수 있습니다. 트랜잭션 이메일을 보내는 경우 아래 표시된 것처럼 API를 사용하여 이메일을 보내도록 캠페인에 트리거를 설정합니다. 먼저 Smart Campaign을 설정하겠습니다. 1. 마케팅 활동에서 프로그램을 선택한 다음 새로 만들기 드롭다운 아래에서 새 로컬 자산을 클릭합니다.

1. 스마트 캠페인 클릭
1. 스마트 캠페인 이름을 입력하고 만들기 를 클릭합니다

**스마트 캠페인에 트리거 추가** 스마트 캠페인에 트리거를 추가하면 라이브 이벤트를 기반으로 한 번에 한 사람씩 스마트 캠페인을 실행할 수 있습니다. 이 경우 라이브 이벤트는 [requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST)를 통한 요청입니다. 1. &quot;캠페인이 요청됨&quot; 트리거를 검색한 다음 캔버스로 드래그하여 놓습니다.

1. 트리거에서 &quot;is&quot; 및 &quot;웹 서비스 API&quot;를 선택합니다.

**Campaign에서 전자 메일 흐름 동작을 만드는 방법** 스마트 캠페인과 전자 메일을 연결하면 마케터는 전자 메일이 표시되는 방식을 관리하고 서드파티 응용 프로그램은 전자 메일을 받는 사람과 시기를 결정할 수 있습니다. 이메일을 새 로컬 자산으로 만든 후 캠페인에서 흐름 작업으로 설정할 수 있습니다.  보낼 이메일을 찾아 선택합니다.

**requestCampaign API를 호출하는 코드 샘플** Marketo 인터페이스에서 캠페인 및 트리거를 설정한 후 API를 사용하여 전자 메일을 보내는 방법을 보여 줍니다. 첫 번째 샘플은 XML 요청이고, 두 번째 샘플은 XML 응답이며, 마지막 샘플은 XML 요청을 생성하는 데 사용할 수 있는 Java 코드 샘플입니다. `requestCampaign` API를 호출할 때 사용되는 캠페인 ID를 찾는 방법도 보여 줍니다.
또한 API를 호출하려면 Marketo 캠페인의 ID를 미리 알고 있어야 합니다. 다음 방법 중 하나를 사용하여 캠페인 ID를 결정할 수 있습니다. 1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1을 사용합니다. 브라우저에서 Marketo 캠페인을 열고 URL 주소 표시줄을 봅니다. 캠페인 ID(4자리 정수로 표시됨)는 &quot;SC&quot; 바로 다음에 찾을 수 있습니다. 예, `<https://app-stage.marketo.com/#SC**1025**A1>`. 굵게 표시된 부분은 캠페인 ID - &quot;1025&quot;입니다. `requestCampaign`에 대한 SOAP 요청

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>anotherlead@company.com</keyValue>
        </leadKey>
      </leadList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign에 대한 SOAP 응답

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

위에서 설명한 시나리오를 실행하는 샘플 Java 프로그램 아래를 참조하십시오.

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


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
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
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            LeadKey key2 = new LeadKey();
            key2.setKeyType(LeadKeyRef.EMAIL);
            key2.setKeyValue("anotherlead@company.com");

            leadKeyList.getLeadKeies().add(key);
            leadKeyList.getLeadKeies().add(key2);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
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

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-03-27_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## AP를 사용하여 Marketo에서 다이내믹 콘텐츠를 사용하여 이메일 보내기-

콜센터 후속 이메일을 자동화하고자 한다고 상상해 보십시오. 지원 담당자가 고객과 이야기를 나눈 후, 회사에 연락한 것에 대해 감사하는 이메일을 자동으로 전송하려고 합니다. 여기서 한 단계 더 나아가, CRM에서 추적하는 고객과 논의된 특정 대화 주제를 포함한다고 가정해 보겠습니다. requestCampaign SOAP API를 사용하여 Marketo에서 다이내믹 콘텐츠가 포함된 이메일을 보낼 수 있습니다. requestCampaign API를 사용하면 리드 또는 리드를 전달할 수 있습니다. 또한 기존 Campaign에서 사용하여 다이내믹 콘텐츠를 전송할 수 있는 프로그램 토큰을 전달할 수 있습니다. requestCampaign SOAP API를 사용하려면 이메일 수신자가 Marketo에 있어야 합니다. 따라서 requestCampaign API를 호출하기 전에 [getLead API](/help/soap-api/getlead.md)를 사용하여 전자 메일이 Marketo에 있는지 확인하십시오. 먼저 스마트 캠페인을 만드는 방법, 두 번째 API를 통해 캠페인을 보내는 트리거를 설정하는 방법, 세 번째 프로그램 토큰을 통해 동적 콘텐츠를 허용하는 이메일을 만드는 방법, 네 번째 플로우 작업의 일부로 이메일을 정의하는 방법, 다섯 번째 이 캠페인을 실행하는 데 사용되는 코드 샘플을 보여 줍니다. **Marketo에서 새 스마트 캠페인을 만드는 방법** Marketo의 스마트 캠페인은 모든 마케팅 활동을 실행합니다. 일련의 자동화된 작업을 설정하여 스마트 연락처 목록에 추가할 수 있습니다. 트랜잭션 이메일을 보내는 경우 아래 표시된 것처럼 API를 사용하여 이메일을 보내도록 캠페인에 트리거를 설정합니다. 먼저 Smart Campaign을 설정하겠습니다. 1. 마케팅 활동에서 프로그램을 선택한 다음 새로 만들기 드롭다운 아래에서 새 로컬 자산을 클릭합니다

1. 스마트 캠페인 클릭
1. 스마트 캠페인 이름을 입력하고 **스마트 캠페인에 트리거 추가** 스마트 캠페인에 트리거를 추가하면 라이브 이벤트를 기반으로 한 번에 한 사람씩 스마트 캠페인을 실행할 수 있습니다. 이 경우 [requestCampaign API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/triggerCampaignUsingPOST)를 통한 요청입니다.
1. &quot;캠페인이 요청됨&quot; 트리거를 검색한 다음 캔버스로 드래그하여 놓습니다.
1. 트리거에서 &quot;is&quot; 및 &quot;웹 서비스 API&quot;를 선택합니다.

**API를 사용하여 다이내믹 콘텐츠를 전달하는 방법** Marketo에서 내 토큰은 프로그램에서 사용할 수 있는 변수입니다. 내 토큰을 사용하면 한 위치에 프로그램과 관련된 정보를 입력하고 해당 정보를 지정한 값으로 대체하며 이 정보를 전자 메일 템플릿과 같은 애플리케이션의 다른 부분에서 검색할 수 있습니다. requestCampaign SOAP API를 사용하여 기존 토큰을 재정의하는 프로그램 토큰 배열을 전달할 수 있습니다. 캠페인 실행 후 토큰이 삭제됩니다. Campaign 폴더 수준 또는 프로그램 수준에서 내 토큰을 만듭니다. Campaign 폴더 수준의 내 토큰은 Campaign 폴더에 포함된 모든 프로그램으로 상속됩니다. Campaign 폴더 수준에서 내 토큰을 만들면 프로그램 수준에서 상속된 값을 덮어쓸 수 있습니다. 예를 들어 캠페인 폴더 수준에서 프로그램 날짜 및 프로그램 설명에 대한 토큰을 정의하는 경우 개별 프로그램 수준에서 이러한 값을 덮어쓸 수 있습니다.

방법은 다음과 같습니다. 1. 마케팅 활동 트리에서 토큰을 생성할 Campaign 폴더 또는 프로그램을 선택합니다. 상단 메뉴 모음에서 내 토큰 을 선택합니다. 그러면 내 토큰 캔버스가 표시됩니다. 오른쪽 트리에서 토큰 유형을 캔버스로 드래그합니다(이 경우 &quot;텍스트&quot;). 토큰 이름 필드에서 내 토큰을 강조 표시하고 고유한 토큰 이름을 입력합니다. 이 경우 &quot;my.conversationtopic&quot;입니다. 값 필드에 토큰에 대한 관련 값을 입력합니다. 이 경우 &quot;오늘 전화해 주셔서 감사합니다.&quot;라고 표시됩니다. API를 사용하면 기본 내 토큰 값이 재정의됩니다. 사용자 지정 토큰을 저장하려면 &quot;저장&quot;을 클릭합니다.  1. 새로 만들기를 클릭하여 새 이메일을 만듭니다. 그런 다음 새 로컬 Assets 를 클릭하고 이메일을 선택합니다. 그런 다음 관련 필드를 작성하여 이메일 이름을 지정하십시오. 이메일 초안을 작성할 때 토큰 아이콘을 클릭하여 이메일에 토큰을 포함합니다. 토큰을 사용하여 템플릿 이메일을 만들었으므로 이제 이메일을 후속 단계에서 Campaign에 대한 흐름 동작으로 추가합니다. 따라서 API를 통해 캠페인을 호출하면 이메일이 발송됩니다.
**Campaign에서 전자 메일 흐름 동작을 만드는 방법** 스마트 캠페인과 전자 메일을 연결하면 마케터는 전자 메일이 표시되는 방식을 관리하고 서드파티 응용 프로그램은 전자 메일을 받는 사람과 시기를 결정할 수 있습니다. 이메일을 새 로컬 자산으로 만든 후 캠페인에서 흐름 작업으로 설정할 수 있습니다. 보낼 이메일을 찾아 선택합니다.
**requestCampaign API를 호출하는 코드 샘플** Marketo 인터페이스에서 캠페인 및 트리거를 설정한 후 API를 사용하여 전자 메일을 보내는 방법을 보여 줍니다. 첫 번째 샘플은 XML 요청이고, 두 번째 샘플은 XML 응답이며, 마지막 샘플은 XML 요청을 생성하는 데 사용할 수 있는 Java 코드 샘플입니다. requestCampaign API를 호출할 때 사용되는 캠페인 ID를 찾는 방법도 보여 줍니다. 또한 API를 호출하려면 Marketo 캠페인의 ID를 미리 알고 있어야 합니다. 다음 방법 중 하나를 사용하여 캠페인 ID를 결정할 수 있습니다. 1. [getCampaignsForSource](/help/soap-api/getcampaignsforsource.md) API 1을 사용합니다. 브라우저에서 Marketo 캠페인을 열고 URL 주소 표시줄을 봅니다. 캠페인 ID(4자리 정수로 표시됨)는 &quot;SC&quot; 바로 다음에 찾을 수 있습니다. 예, `<https://app-stage.marketo.com/#SC&#x200B;**1025**&#x200B;A1>`. 굵게 표시된 부분은 캠페인 ID - &quot;1025&quot;입니다. requestCampaign에 대한 SOAP 요청

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Header>
    <ns1:AuthenticationHeader>
      <mktowsUserId>demo17_1_809939944BFABAE58E5D27</mktowsUserId><requestSignature>48397ad47b71a1439f13a51eea3137df46441979</requestSignature><requestTimestamp>2013-08-01T12:31:14-07:00</requestTimestamp>
    </ns1:AuthenticationHeader>
  </SOAP-ENV:Header>
  <SOAP-ENV:Body>
    <ns1:paramsRequestCampaign>
      <source>MKTOWS</source>
      <campaignId>4496</campaignId>
      <leadList>
        <leadKey>
          <keyType>EMAIL</keyType>
          <keyValue>lead@company.com</keyValue>
        </leadKey>
      </leadList>
      <programTokenList>
        <attrib>
          <name>{{my.conversationtopic}}</name>
          <value>Thank you for calling about adding a line of service to your current plan.</value>
        </attrib>
      </programTokenList>
    </ns1:paramsRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

requestCampaign에 대한 SOAP 응답

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="<http://schemas.xmlsoap.org/soap/envelope/>" xmlns:ns1="<http://www.marketo.com/mktows/">
  <SOAP-ENV:Body>
    <ns1:successRequestCampaign>
      <result>
        <success>true</success>
      </result>
    </ns1:successRequestCampaign>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

위에서 설명한 시나리오를 실행하는 샘플 Java 프로그램 아래를 참조하십시오.

```java
import com.marketo.mktows.\*;
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


public class RequestCampaign {

    public static void main(String[] args) {
        System.out.println("Executing Request Campaign");
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
            ParamsRequestCampaign request = new ParamsRequestCampaign();

            request.setSource(ReqCampSourceType.MKTOWS);

            ObjectFactory objectFactory = new ObjectFactory();
            JAXBElement<Integer> campaignId = objectFactory.createParamsRequestCampaignCampaignId(4496);
            request.setCampaignId(campaignId);

            ArrayOfLeadKey leadKeyList = new ArrayOfLeadKey();
            LeadKey key = new LeadKey();
            key.setKeyType(LeadKeyRef.EMAIL);
            key.setKeyValue("lead@company.com");

            leadKeyList.getLeadKeies().add(key);

            JAXBElement<ArrayOfLeadKey> arrayOfLeadKey = objectFactory.createParamsRequestCampaignLeadList(leadKeyList);
            request.setLeadList(arrayOfLeadKey);

            ArrayOfAttrib aoa = new ArrayOfAttrib();

            Attrib attrib = new Attrib();
            attrib.setName("{{my.conversationtopic}}");
            attrib.setValue("Thank you for calling about adding a line of service to your current plan.");

            aoa.getAttribs().add(attrib);

            JAXBElement<ArrayOfAttrib> arrayOfAttrib = objectFactory.createParamsRequestCampaignProgramTokenList(aoa);
            request.setProgramTokenList(arrayOfAttrib);

            SuccessRequestCampaign result = port.requestCampaign(request, header);

            JAXBContext context = JAXBContext.newInstance(SuccessRequestCampaign.class);
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

requestCampaign API를 통해 호출한 후 스마트 캠페인이 Marketo에서 실행되었는지 확인하여 확인할 수 있습니다.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-04-03_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## 비즈니스 논리를 기반으로 한 익명 방문자 활동 캡처

회사 블로그의 특정 게시물을 방문하는 사용자를 추적하려고 한다고 상상해 보십시오. 게시물을 방문하는 총 사용자 수 중에서 최소 5초를 소비하고 페이지를 아래로 스크롤하여 관심 신호를 보내는 사용자만 추적한다고 가정해 보겠습니다. 익명 사용자의 경우 이 이벤트를 사용하여 Marketo에서 새 잠재 고객을 만들고, 알려진 사용자의 경우 이 이벤트를 사용하여 잠재 고객 활동을 업데이트하려고 합니다. 웹 사이트에서 [Munchkin 추적 코드](/help/javascript-api/lead-tracking.md)를 사용하여 이를 수행할 수 있습니다. 쿠키가 아닌 사용자가 Munchkin 추적 코드가 있는 페이지로 이동하면 사용자의 브라우저에 새 쿠키가 생성되고 Marketo에 새 익명 잠재 고객이 생성됩니다. 사용자가 이미 쿠키를 했으며 사용자가 Marketo의 기존 잠재 고객인 경우, 페이지 방문은 Marketo의 사용자 활동 로그에 기록됩니다. 먼저 Marketo에서 Munchkin 추적 코드를 생성하는 방법, 두 번째 특정 조건이 충족되는 경우에만 트리거하도록 Munchkin 샘플 코드를 수정하는 방법 및 세 번째 익명 사용자의 페이지 방문이 Marketo에 기록되었는지 확인하는 방법을 보여 줍니다.

**Munchkin 추적 코드를 생성하는 방법** Munchkin 추적 코드를 사용하면 웹 사이트 방문 횟수를 추적할 수 있습니다. 아래에 세 가지 유형의 Munchkin 코드가 설명되어 있지만 이 예제에서는 비동기 Munchkin 추적 코드를 사용합니다. A) 단순: 가장 적은 코드 줄이 있지만 웹 페이지 로드 시간에 최적화되지 않습니다. 이 코드는 웹 페이지가 로드될 때마다 jQuery 라이브러리를 로드합니다. B) 비동기: 웹 페이지 로드 시간을 줄입니다. 이 코드는 jQuery 라이브러리가 이미 있는지 확인하고 누락된 경우 로드한 다음 웹 페이지의 나머지 부분이 로드되면 추적 코드를 실행하는 데 사용합니다. C) 비동기 jQuery: 웹 페이지 로드 시간을 줄이고 시스템 성능도 향상시킵니다. 이 코드는 사용자가 이미 jQuery를 가지고 있다고 가정하고 로드를 선택하지 않습니다. 1. 앱 오른쪽 상단에 있는 관리자 를 클릭합니다.  1. 왼쪽의 트리에서 Munchkin을 클릭합니다.  1. 추적 코드 유형에 대해 [비동기]를 선택합니다. 1. JavaScript 추적 코드를 클릭하여 웹 사이트에 게시합니다.
**쿠키 사용자 및 추적 이벤트에 대한 코드 샘플** 추적 코드를 `</body>` 태그 바로 앞에 웹 페이지에 배치합니다. Marketo에서 만든 랜딩 페이지에는 추적 코드가 자동으로 포함되어 있으므로 이 코드를 추가할 필요가 없습니다. 이 코드 샘플은 스크립트가 로드된 후 Munchkin API를 호출합니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('XXX-XXX-XXX');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName('head')[0].appendChild(s);
})();
</script>
```

이 코드 샘플은 사용자가 페이지에 5초 동안 있고 500픽셀을 페이지 아래로 스크롤한 후 Munchkin API를 호출합니다.

```javascript
<script src="https://code.jquery.com/jquery-2.1.0.min.js"></script>
<script type="text/javascript">
$(function(){
 setTimeout(function(){
  $(window).scroll(function() {
      var y_scroll_position = window.pageYOffset;
      var scroll_position = 500; //Sets number of pixels user must scroll to be tracked

  if(y_scroll_position > scroll_position) {
  //Munchkin tracking code
   (function() {
     var didInit = false;
     function initMunchkin() {
      if(didInit === false) {
        didInit = true;
        Munchkin.init('XXX-XXX-XXX');
      }
     }

     var s = document.createElement('script');
     s.type = 'text/javascript';
     s.async = true;
    s.src = '//munchkin.marketo.net/munchkin.js';
     s.onreadystatechange = function() {
      if (this.readyState == 'complete' || this.readyState == 'loaded') {
          initMunchkin();
      }
     };
     s.onload = initMunchkin;
     document.getElementsByTagName('head')[0].appendChild(s);
   })();
   }
 },5000); //Sets time delay before tracking user
});
</script>
```

**익명 사용자의 페이지 방문이 Marketo에 기록되었는지 확인하는 방법**

1. 상단 메뉴에서 Analytics를 클릭한 다음 새 보고서를 클릭합니다. 보고서 유형으로 웹 페이지 활동 을 선택한 다음 보고서에 이름을 지정합니다.
1. 보고서를 만든 후 Smart List를 클릭합니다. 그런 다음 오른쪽 상자에서 방문한 웹 페이지 필터를 선택합니다. Munchkin 추적 코드를 넣을 웹 페이지를 입력합니다.
1. 설정 을 클릭합니다. ISP에서 익명 방문자 를 선택하고 옵션을 표시로 변경합니다.
1. 보고서를 클릭합니다. 이제 선택한 웹 페이지에서 추적된 활동이 표시됩니다.
1. 잠재 고객 레코드를 두 번 클릭하면 익명 사용자가 방문한 특정 페이지를 볼 수 있는 활동 로그가 표시됩니다.

이 문서에는 사용자 정의 통합을 구현하는 데 사용되는 코드가 포함되어 있습니다. 맞춤화된 특성으로 인해 Marketo 기술 지원 팀에서 사용자 정의 작업 문제를 해결할 수 없습니다. 적절한 기술 경험이나 숙련된 개발자 액세스 없이 다음 코드 샘플을 구현하지 마십시오.

_2014-04-17_&#x200B;에 _Murta_&#x200B;에 의해 게시됨

## RTP를 사용하여 로컬 전화 번호를 동적으로 변경

Personalization이 전부입니다. 우리는 오래 전에 이 사실을 파악했습니다. 그 말이 나온 김에, 즉각적인 지원이 필요할 때마다 웹사이트에서 관련 지역 전화번호를 찾는 것이 너무 힘들다는 것이 아직도 저에게는 놀랍습니다. [에 ](https://business.adobe.com/products/marketo/content-personalization.html)Marketo 실시간 Personalization<https://business.adobe.com/products/marketo/adobe-marketo.html>(RTP)이 설치되어 있습니다. [RTP 방문자 API](/help/javascript-api/web-personalization.md)를 활용하여 웹 사이트의 여러 섹션에서 웹 방문자가 보는 전화 번호를 동적으로 변경할 수 있습니다. 와우! 믿겨지니? 이 마법은 어떻게 작동합니까? 먼저 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript)에 설명된 대로 웹 사이트에 RTP를 설치해야 합니다. 그런 다음 아래 지침에 따라 웹 사이트에서 JavaScript 코드를 구현합니다.

1. **defaultPhone** 구성에 국제 전화 번호 삽입
1. **divIds** 구성에 HTML 요소 ID를 삽입합니다.
1. 휴대폰 번호를 모바일 브라우저에 대한 클릭-호출 링크로 설정하려면 **mobileLink** 구성을 **true**(으)로 설정하십시오.
1. **cityPhone**, **statePhone** 및 **countryPhone** 구성에서 다른 위치를 전화 번호로 매핑합니다.

예를 들어 구성 설정에 대한 샘플 값은 다음과 같습니다.

```json
  defaultPhone:"+1.503.608.4679", // Optional
  divIds:["phoneId1","phoneId2"],
  mobileLink: true,
  cityPhone: {
    "<a href="#">yanir</a>": ["San Mateo", "San Francisco"],
    "+353.1.242.3000": ["tel-aviv"]
  },
  statePhone: {
    "+1.650.376.2300": ["CA"],
    "+1.650.376.2302": ["OR"]
  },
  countryPhone: {
    "+1.650.376.2300": ["United States"],
    "+353.1.242.3000": ["Israel"]
  }
```

마지막으로 **divIds**&#x200B;의 ID 중 하나와 일치하는 ID가 포함된 HTML 앵커 태그를 삽입합니다(위의 2단계). 예를 들어 **divIds**&#x200B;에 &quot;phoneId1&quot;을 지정한 경우 HTML 앵커 태그는 다음과 같이 표시됩니다.

`<a href="tel:+1800229933" id="phoneId1">+1800229933</a>`

스크립트는 다음 순서로 일치하는 항목이 있는지 확인합니다. cityPhone > statePhone > countryPhone > defaultPhone 전화 번호를 텍스트로 바꿀 수도 있습니다(예: &quot;샌프란시스코 사용자 그룹에 참여&quot;) 또는 HTML 코드를 실행하고 지리적 위치에 따라 콘텐츠를 동적으로 변경할 수 있습니다. 맛있게 드십시오!

```html
<a href="tel:+1800229933" id="phoneId1">+1800229933</a>
<script>
(function(a){
    rtp('get','visitor',function(yc){
        var location = yc.results.location;
        var loop = true;
        var phoneChanged = false;
        console.log(yc.results);
        function checkObj(obj){
            return Object.getOwnPropertyNames(obj).length >0;
        }
        function changePhone(p){
            d=a.divIds;
            for(i=0;i<d.length;i++){
                if(document.getElementById(d[i]) !== null){
                    document.getElementById(d[i]).innerHTML = p;
                    if(a.mobileLink){
                        document.getElementById(d[i]).href= "tel:" + p;
                    }
                    console.log(p);
                }
            }
            loop = false;
            phoneChanged = true;
        }
        function matchLocation(loc,objc){
            for (var key in objc) {
                for(i=0;i<objc[key].length && loop;i++){
                    if (!loop) { return true;};
                    val = objc[key][i];
                    //console.log(loc + location[loc] + " ? " + val);
                    if(location[loc].toLowerCase() === val.toLowerCase()){
                        changePhone(key);
                    }
                }
            }
        }
        if(checkObj(a.cityPhone)){
            matchLocation("city",a.cityPhone);
        }else if(checkObj(a.statePhone)){
            matchLocation("state",a.statePhone);
        }else if(checkObj(a.countryPhone)){
            matchLocation("country", a.countryPhone);
        }else if(!phoneChanged && a.defaultPhone.length > 0 ){
            changePhone(a.divId,a.defaultPhone);
        }
    });
})({
    defaultPhone:"",  //  [Optional] the number to show if visitor does not match the mapping below
    divIds:["phoneId1","Floater"],  //the phone HTML element ID, can be <div>, <a>, <span>, <p> etc.
    mobileLink: true,  //if you use click to call link (with href="tel:") you can also change its number

    cityPhone: {
        "<a href='#'>yanir</a>": ["San Mateo", "San Francisco"],
        "+353.1.242.3000": ["tel-aviv"]
    },
    statePhone: {
        "+1.650.376.2300": ["CA"],
        "+1.650.376.2302": ["OR"]
    },
    countryPhone: {
        "+1.650.376.2300": ["United States"],
        "+353.1.242.3000": ["Israel"]
    }
});
</script>
```

_Yanir_&#x200B;에 의해 _2016-02-02_&#x200B;에 게시됨

## 2016년 겨울 업데이트

### 사용자 지정 개체

* [사용자 지정 개체 N:N 관계가 이제 지원됨](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/marketo-custom-objects/create-marketo-custom-objects)
   * 이제 리드 또는 계정 레코드는 중간 개체의 정의를 통해 사용자 지정 개체를 통해 다대다 관계를 가질 수 있습니다. 독립형 사용자 정의 객체 유형을 생성한 후, 독립형 객체와 리드 또는 계정 모두에 대한 링크 필드를 사용하여 중간 객체 유형을 생성할 수 있습니다.
   * 이 기능에 대한 새 API 호출은 없지만 API를 통해 이러한 관계를 활용하려면 개체 정의를 올바르게 구성해야 합니다.
* `getLeadActivities` 및 `getLeadChanges`은(는) 더 이상 익명 잠재 고객의 활동을 반환하지 않습니다. 자세한 내용은 [차세대 Munchkin 추적 FAQ](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 참조하십시오

_케니_&#x200B;이(가) _2016-02-05_&#x200B;에 게시함

## REST API를 사용하여 단일 리드에 대한 활동 검색

개발자 커뮤니티에서 반복적으로 묻는 질문이 있습니다.

&quot;개별 리드에 대한 이전 활동 목록을 가져오려면 어떻게 해야 합니까?&quot;

최근까지 REST API를 사용하여 이를 수행하는 간단한 방법은 없었습니다. 하지만 지금은 있습니다! REST API의 2016년 겨울 릴리스에는 약간의 개선 사항이 포함되어 있습니다. [리드 활동 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET)에서 이제 리드 ID를 지정하는 데 사용할 수 있는 **leadIds** 매개 변수를 허용합니다. **leadIds** 매개 변수를 지정하면 해당 잠재 고객 ID에 대한 활동만 반환됩니다. 리드 ID 필터로 생각할 수 있습니다. 둘 이상의 잠재 고객에 대한 결과를 필터링하려는 경우 **leadIds** 매개 변수는 쉼표로 구분된 잠재 고객 ID 목록을 사용할 수 있습니다(최대 30개). 예를 들어 활동을 특정 회사의 리드로 제한할 때 유용합니다. 아래 **예**&#x200B;은(는) [leadIds](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadActivitiesUsingGET) 매개 변수를 포함하는 **리드 활동 가져오기**&#x200B;에 대한 샘플 요청입니다. **leadIds** 매개 변수에 &quot;50&quot; 값을 지정했습니다. 이는 내 Marketo 인스턴스의 임의 리드에 해당합니다. Marketo 인스턴스의 &quot;모바일 앱 세션&quot; 활동에 해당하는 activityTypeIds 매개 변수에 &quot;129&quot; 값을 지정했습니다.

`<https://123-abc-456.mktorest.com/rest/v1/activities.json?leadIds=50&activityTypeIds=129&nextPageToken=WQV2VQVPPCKHC6AQYVK7JDSA3J4SMAZRQO4RKIXCEMLFCM2APRSQ====>`

다음은 위의 요청에서 발췌한 응답입니다. 알 수 있듯이 &quot;leadId&quot;: 50 및 &quot;activityTypeId&quot;: 129인 결과 개체만 포함합니다.

```json
{
    "id": 846,
    "leadId": 50,
    "activityDate": "2015-04-06T21:58:59Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 7
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 879,
    "leadId": 50,
    "activityDate": "2015-04-07T00:45:11Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 5
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1114,
    "leadId": 50,
    "activityDate": "2015-04-08T00:02:41Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 241
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1551,
    "leadId": 50,
    "activityDate": "2015-04-09T23:31:56Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 223
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
{
    "id": 1716,
    "leadId": 50,
    "activityDate": "2015-04-15T22:44:19Z",
    "activityTypeId": 129,
    "primaryAttributeValueId": 13,
    "primaryAttributeValue": "Sample App",
    "attributes": [
        {
            "name": "Device Type",
            "value": "iPhone"
        },
        {
            "name": "Mobile App Session Length",
            "value": 223
        },
        {
            "name": "Platform",
            "value": "ios"
        }
    ]
}
```

## Zapier를 사용하여 Marketo 및 500개 이상의 앱과 원활하게 통합

Marketo의 Principal Solutions Consultant(수석 솔루션 컨설턴트) Philippe Delle Case의 게시물입니다.

### 목표

이 문서에서는 Zapier를 통해 Marketo을 500개 이상의 Cloud 앱과 통합하는 방법에 대해 자세히 설명합니다. 이를 위해 Marketo용 Zapier 커넥터를 처음부터 빌드하고 두 가지 실용적인 통합 사용 사례를 구현합니다. 사용 사례 1: FullContact Card Reader에서 Marketo으로의 단방향 리드 통합

* FullContact 모바일 카드 Reader 앱을 사용하여 연락처의 명함을 검색하고 Marketo에서 자동으로 생성된 리드를 가져옵니다.
* Marketo의 정적 목록에 기존 리드를 추가하고 Google 시트에 자동으로 추가된 리드를 찾습니다.
* Google Sheet에서 리드를 수정하고 Marketo에 다시 반영되는 변경 사항을 찾습니다.

### 사전 요구 사항

**Zapier에서 무료 계정에 등록** [Zapier](https://zapier.com/)은(는) 프로그래머나 IT 리소스 없이 다른 온라인 앱 간의 작업을 쉽게 자동화할 수 있는 웹 앱 자동화 서비스입니다. 간략한 소개가 [여기](https://zapier.com/api/v4/helpdocs/category/redirect/what-is-zapier)에 있습니다. 현재 Zapier는 마케팅, CRM, CMS, 고객 지원, 전자 서명, Forms 등과 같은 다양한 도메인에서 500개 이상의 앱을 지원합니다. 한 앱과 다른 앱 간의 단일 통합을 Zap이라고 합니다. Zapier의 [zapbook](https://zapier.com/apps)에서 지원되는 웹 앱의 전체 목록을 확인하십시오.  무료 계정 [여기](https://zapier.com/sign-up/)에 등록하세요. 15분마다 실행되는 최대 100개의 작업/월, 5개의 Zap 및 Zap에 액세스할 수 있습니다. Zapier의 유료 플랜(기본, 비즈니스, 비즈니스 플러스 등)에 가입하면 더 많은 혜택을 누릴 수 있습니다.

**관리자 자격으로 또는 제공된 API 사용자 계정으로 Marketo 인스턴스에 액세스** Zapier 커넥터는 Marketo REST API를 사용하여 리드 데이터를 Marketo에 푸시합니다. 이 API를 사용하려면 Marketo 인스턴스의 관리자인 경우 직접 만들 수 있는 API 사용자 및 사용자 지정 서비스가 필요합니다. 그렇지 않은 경우 관리자가 제공해야 합니다. 만들 웹후크도 있으며 Marketo 관리자만 액세스할 수 있습니다. Marketo API 사용자 및 사용자 지정 서비스를 만드는 방법에 대한 단계별 설명은 [여기](http://rest-api/custom-services/)에서 확인할 수 있습니다. 완료되면 Marketo REST API를 호출하기 위한 클라이언트 ID, 클라이언트 암호, Munchkin 계정 ID, Munchkin 계정 ID 자격 증명이 있어야 합니다

Munchkin 계정 ID는 Munchkin 또는 웹 서비스 관리 화면에서 가져올 수 있습니다. 패턴은 다음과 같습니다. `000-XXX-000`.  액세스 토큰은 한 시간 동안만 유효하므로 가져올 필요가 없습니다. 커넥터가 자동으로 토큰을 생성합니다.
**Google Docs, Sheets 및 Slides를 사용하여 무료 계정에 등록하면 다양한 종류의 온라인 문서를 만들고, 다른 사람들과 실시간으로 작업하고, 온라인으로 Google 드라이브에 저장할 수 있는 생산성 앱입니다. 사용 사례에는 Google 시트가 필요합니다. [여기](https://workspace.google.com/products/docs/)에서 Google Docs의 다양한 기능과 Google을 사용하여 계정을 만들 수 있습니다.
**FullContact를 사용하여 무료 계정에 등록하세요** FullContact를 사용하면 모든 연락처를 가져와 소셜 프로필, 사진, 전자 메일 서명, 회사 정보 등의 변경 사항과 지속적으로 동기화하여 가장 중요한 사람들과 완전히 연결할 수 있습니다. Zapier를 포함한 250개 이상의 웹 앱으로 카드를 스캔할 수 있는 모바일 명함 판독기를 제공합니다. 무료 계정 [여기](https://app.fullcontact.com/login)에 등록할 수 있습니다. 더 많은 기능과 용량을 제공하는 프리미엄 유료 계정을 구독할 수도 있습니다. 모바일 앱은 [Apple AppStore](https://apps.apple.com/us/app/fullcontact-business-card/id576780807) 또는 [Google Play](https://play.google.com/store/apps/details?id=com.fullcontact.cardreader)에서 다운로드할 수 있습니다. FullContact Zap는 [여기](https://zapier.com/apps/contacts-plus/integrations)에 설명되어 있습니다.

### Zapier용 Marketo 커넥터 구현

**Marketo 앱 만들기** Zapier 웹 인터페이스에서 개발자 포털로 이동합니다. **새 앱 추가**&#x200B;를 클릭하고 적어도 제목(예: &#39;Marketo&#39;)과 설명을 입력하십시오. 로고는 선택 사항이지만, 있으면 좋습니다.\ **인증** 이 섹션에서는 Marketo REST API 인증 및 인증 설정에 사용되는 다양한 필드를 선언합니다. 먼저 다음 필드를 만듭니다.

&#39;인증 설정&#39;을 편집합니다.

* 인증 유형: 세션 인증
* 인증 매핑:

  `{"access_token":"{{access_token}}"}`

* Access Token Placement&#x200B;**:**&#x200B;의 토큰

Marketo 사용자 지정 서비스가 만들어지면 클라이언트 ID 및 클라이언트 암호를 사용할 수 있게 됩니다. 클라이언트 ID와 클라이언트 암호를 사용하여 REST API [인증](/help/rest-api/authentication.md) 끝점을 통해 액세스 토큰을 생성합니다. 그런 다음 이 액세스 토큰을 사용하여 REST API에 대한 후속 요청을 수행할 수 있습니다. 토큰은 1시간 후 만료되며 REST API 호출을 계속하려면 다시 생성해야 합니다. 세션 토큰이 만료될 때마다 사용자 지정 인증 스크립트를 실행할 수 있으므로 인증 유형 = &#39;세션 인증&#39;을 선택했습니다. &#39;스크립팅 API&#39; 섹션에서 이 유형의 인증으로만 작동할 수 있는 이 메커니즘을 구현하는 방법을 살펴보겠습니다.
**트리거** Zapier 트리거를 사용하여 데이터를 Zapier로 가져올 수 있습니다. Marketo Webhook을 대신 활용하므로 사용 사례에 필요하지 않습니다. 그러나 Marketo 커넥터에 대한 필수 테스트로 더미 트리거 를 작성해야 합니다. Marketo REST API [일별 사용 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getDailyUsageUsingGET) 끝점을 호출하는 테스트 트리거를 만듭니다. **새 트리거 추가**&#x200B;를 클릭하여 마법사를 시작하고 다음 필드를 채웁니다(언급하지 않은 필드는 비워 둘 수 있음). 이름 및 설명

* 이름: 테스트 트리거
* 키: test_trigger
* 설명: Marketo 앱의 테스트 트리거입니다
* 중요해요? 선택되지 않음
* 숨어요? 선택됨

필드 트리거

* None

데이터 출처

* 데이터 Source: 폴링
* 폴링 URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/stats/usage.json`

샘플 결과

* 비워 둡니다.

**트리거 설정 관리**&#x200B;를 클릭하고 테스트 트리거를 사용자 자격 증명을 확인하는 데 사용할 트리거로 설정합니다. **작업** Zapier 작업이 있으면 Zapier에서 데이터를 보낼 수 있습니다. Marketo REST API를 호출하는 Create_Update 리드 작업을 구현합니다. 이 작업을 통해 Marketo 내에 새 리드를 만들 수 있습니다. 또는 리드가 이미 있는 경우 제출된 값으로 업데이트됩니다. 데이터 중복 제거에는 &#39;email&#39; 필드를 사용합니다. **새 작업 추가**&#x200B;를 클릭하여 마법사를 시작하고 다음 필드를 채웁니다(언급하지 않은 필드는 비워 둘 수 있음). 이름 및 설명

* 이름: Create_Update 리드
* 명사: 리드
* 키: create-update-lead
* 설명: Marketo 내에 새 리드를 생성하거나 리드가 이미 있는 경우 제출된 값으로 업데이트합니다.
* 중요해요? 선택됨
* 숨어요? 선택되지 않음

작업 필드 작업 필드는 사용자가 데이터에 매핑할 필드입니다. Marketo에서 업데이트할 수 있는 모든 데이터를 표시하므로 자신의 요구 사항에 따라 신중하게 선택하십시오. Zapier에는 최종 사용자에게 Marketo에서 사용할 수 있는 모든 필드를 제공하는 옵션이 있지만, 이는 일회용 커넥터에 필요하지 않고 더 많은 코드와 복잡성을 유발할 수 있습니다. 예를 들어 다음 필드를 선택했습니다.

Marketo 인스턴스에 잠재 고객 파티션이 있으므로 파티션 이름은 필수 사항입니다. 그렇지 않으면 생략할 수 있습니다. 최종 사용자가 동기화할 필드가 아니라는 것을 알 수 있도록 &#39;입력&#39; 그룹에서 분리했습니다. &#39;메모&#39; 필드는 Marketo과 Salesforce 간의 동기화에서 비롯됩니다. Marketo 인스턴스에 없는 경우 사용하지 마십시오. &#39;호출됨&#39; 필드가 Marketo 인스턴스에 생성되었습니다. Marketo 인스턴스에 없는 경우 이 필드를 사용하지 마십시오. 물론 목표는 Marketo에서 필요한 필드를 선택할 수 있도록 하는 것입니다. 작게 시작하고 나중에 추가 필드를 추가하는 것이 좋습니다. 데이터를 보낼 위치

* 작업 끝점 URL: `https://{{munchkin_account_id}}.mktorest.com/rest/v1/leads.json`

샘플 결과

* 비워 둡니다.

### Zapier 스크립팅 API

Zapier의 스크립팅 기능을 사용하면 앱의 API와 Zapier 간에 교환되는 요청 및 응답을 조작할 수 있습니다. HTTP 요청이 전송되기 바로 전에 수정할 수 있으며 Zapier가 해당 요청을 사용하여 작업을 수행하기 전에 응답을 구문 분석할 수 있습니다. Marketo에서 작동하도록 사용자 지정 &#39;세션 인증&#39; 인증을 완료하는 데 필요합니다. 자세한 정보는 [여기](https://zapier.com/developer/documentation/scripting/)를 참조하세요. 다음 코드를 복사하면 나중에 몇 가지 설명을 살펴보겠습니다.

```javascript
var Zap = {

    get_session_info: function(bundle) {

       console.log('Entering get_session_info method ...');

         var access_token,
            access_token_request_payload,
            access_token_response;


        // Assemble the meta data for our Access Token swap request
         console.log('building Request with client_id=' + bundle.auth_fields.client_id + ', and client_secret=' + bundle.auth_fields.client_secret);
        access_token_request_payload = {
            method: 'POST',
            url: 'https://' + bundle.auth_fields.munchkin_account_id + '.mktorest.com/identity/oauth/token',
            params: {
                'grant_type' : 'client_credentials',
                'client_id' : bundle.auth_fields.client_id,
                'client_secret' : bundle.auth_fields.client_secret
            },
            headers: {
                'Content-Type': 'application/json',  // Could be anything.
                Accept: 'application/json'
            }
        };

        // Fire off the Access Token request.
        access_token_response = z.request(access_token_request_payload);

        // Extract the Access Token from returned JSON.
        access_token = JSON.parse(access_token_response.content).access_token;
        console.log('New Access_Token=' + access_token);

        // This will be mixed into bundle.auth_fields in future calls.
        //bundle.auth_fields.access_token=access_token;
        return {'access_token': access_token};
    },


    test_trigger_pre_poll: function(bundle) {

         console.log('Entering test_trigger_pre_poll method ...');

         bundle.request.params = {
         'access_token':bundle.auth_fields.access_token
         };

         return bundle.request;

    },


    test_trigger_post_poll: function(bundle) {

        console.log('Entering test_trigger_post_poll method ...');

        var data = JSON.parse(bundle.response.content);
        if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
            console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);

           throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
        }

        return JSON.parse(bundle.response.content);
    },

    create_update_lead_pre_write: function(bundle) {

       bundle.request.params = {'access_token':bundle.auth_fields.access_token};
       return bundle.request;
    },

    create_update_lead_post_write: function(bundle) {

         var data = JSON.parse(bundle.response.content);
         if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
            console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);
            throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
        }
        return JSON.parse(bundle.response.content);
    }
};
```

**메서드** **get_session_info**

* 이 메서드는 Marketo REST API [인증](/help/rest-api/authentication.md) 끝점을 호출하는 액세스 토큰을 생성하거나 다시 만드는 역할을 합니다.
* 이 메서드는 &#39;post_poll&#39; 메서드에 &#39;액세스 토큰 만료&#39; 오류가 발생할 때마다 호출됩니다. 액세스 토큰은 1시간마다 만료되도록 예약되어 있으므로 이는 예상되었습니다.
* 작업 끝점 URL: https://{{munchkin_account_id}}.mktorest.com/identity/oauth/token

**pre_poll, pre_write**

* Marketo 액세스 토큰을 매개 변수에 추가할 수 있도록 HTTP 요청을 전송하기 직전에 수정하려면 만든 모든 트리거에 대해 &#39;사전 폴링&#39; 메서드를 만들어야 합니다.
* 동일한 이유로 인해 만든 모든 작업에 대해 &#39;사전 쓰기&#39; 메서드를 만들어야 합니다.

**post_poll, post_write**

* Zapier가 응답을 사용해 어떤 작업도 수행하기 전에 응답을 구문 분석하고 결국 &#39;액세스 토큰 만료&#39; 오류를 가로채기 위해 생성한 모든 트리거에서 &#39;사후 폴링&#39; 메서드를 만들어야 합니다.
* 동일한 이유로 인해 만든 모든 작업에 대해 &#39;사후 쓰기&#39; 메서드를 만들어야 합니다.
* 이러한 오류가 발생하면 Japier에서 인증을 재생하고 get_session_info 메서드를 다시 실행하도록 InvalidSessionException을 throw합니다.

화면 오른쪽 상단의 &#39;빠른 링크&#39; 메뉴에서 스크립팅 API의 번들 로그에 액세스할 수 있습니다. 이렇게 하면 스크립트를 디버깅하는 데 유용합니다.

사용 사례 1: Marketo과 FullContact Card Reader 통합

이 통합을 위해 FullContact에서 Marketo으로 하나의 Zap를 만듭니다. 이 Zap를 사용하면 FullContact 모바일 카드 Reader으로 명함을 스캔하고 리드를 Marketo으로 푸시할 수 있습니다.   **Zap FullContact -> Marketo** Zapier 대시보드에서 &#39;새 Zap 만들기&#39; 단추를 클릭합니다.

**Zapier의 트리거**

* 앱 FullContact 선택
* FullContact 트리거 &#39;새 명함&#39; 선택
* FullContact 계정에 연결
* FullContact 앱 테스트

**Zapier의 동작**

* 이전에 만든 Marketo 앱을 선택하십시오. Beta에 표시됩니다.
* Marketo 작업 &#39;Create_Update Lead&#39; 선택
* Marketo 계정에 연결하여 인증 매개 변수(Munchkin 계정 ID, 클라이언트 ID, 클라이언트 암호)를 채웁니다.
* FullContact의 필드를 Marketo에 매핑
* 결국 새 잠재 고객이 이동할 파티션 이름(Marketo 인스턴스에 파티션이 있는 경우에만) 채우기
* Marketo 앱 테스트
* Zap 활성화

참고: FullContact에서 명함 Reader을 다운로드하고 모바일 장치에서 바로 Zapier 통합을 활성화해야 합니다.

사용 사례 2: Marketo과 Google Sheets 통합 -

이 통합을 위해 두 개의 Zap를 만듭니다. 하나는 Marketo에서 Google Sheets로 다른 하나는 Google Sheets에서 Marketo으로 변경되었습니다. 이 Zap를 사용하여 Marketo과 Google Sheet 간에 일부 리드 또는 연락처를 동기화할 수 있습니다.   **Zap Marketo 웹후크 -> Google 시트**
첫 번째 Zap의 경우 Marketo용 사용자 지정 커넥터에 의존하지 않지만 Marketo의 웹훅 및 &#39;Webhooks by Zapier&#39; 트리거를 활용합니다. Zapier 대시보드에서 &#39;새 Zap 만들기&#39; 버튼을 클릭합니다. **Zapier의 트리거 파트 1**

* &#39;Webhooks by Zapier&#39; 트리거 앱 선택
* POST 또는 GET이 Zapier URL이 될 때까지 대기할 수 있는 &#39;Catch Hook&#39;을 선택합니다.
* 하위 키를 선택할 필요 없음
* Zapier가 요청을 (으)로 보내고 클립보드에 복사할 수 있도록 사용자 지정 **웹후크 URL**&#x200B;을(를) 생성했습니다

**Marketo의 Webhook(관리자가 수행하는 단계)**

* [관리] -> [웹후크]로 이동
* &#39;Japier로 리드 푸시&#39;라는 새 Webhook을 만들고 Webhook 양식을 편집합니다.

템플릿 필드에서 Zapier로 전송할 Lead 필드를 모두 선언하고 Marketo 토큰을 활용합니다. 사용 사례에서는 Marketo으로 연결되는 사용자 지정 Zapier 커넥터에 대해 정의한 것과 동일한 필드를 사용합니다.

```json
{
"firstName":"{{lead.First Name}}",
"lastName":"{{lead.Last Name}}",
"email":"{{lead.Email Address}}",
"phone":"{{lead.Phone Number}}",
"leadOwner":"{{lead.Lead Owner First Name}} {{lead.Lead Owner Last Name}}",
"leadOwnerEmail":"{{lead.Lead Owner Email Address}}",
"leadNotes":"{{lead.Lead Notes:default=edit me}}",
"called":"{{lead.Called}}"
}
```

* 양식 저장
* 응답 매핑이 필요 없으므로 Webhook 작업이 완료되었습니다.

**Marketo에서 캠페인 테스트(마케터 또는 관리자가 수행하는 단계)**

* 마케팅 활동에서 새 스마트 캠페인을 만듭니다

테스트 목적으로 리드 상태가 MQL로 변경될 때마다 Webhook을 트리거하는 캠페인을 만들 예정입니다. 물론 Webhook을 다른 비즈니스 목적으로 사용할 수 있습니다.

* 스마트 목록 편집
* 플로우에서 Webhook를 호출합니다.
* 캠페인 예약
* 매번 각 리드가 흐름을 통해 실행될 수 있는지 확인합니다.
* 스마트 캠페인 활성화

**Zapier의 트리거 파트 2**

* &#39;Webhooks by Zapier&#39; 트리거 앱을 완료하려면 Marketo Smart Campaign을 한 번 실행하고 Zapier에서 Webhook을 catch해야 합니다
* 테스트 사례에서는 Marketo 리드 데이터베이스로 이동하여 리드를 열고 상태를 &#39;MQL&#39;로 변경해야 합니다

**Google Sheets에서 스프레드시트 만들기**

* 새 스프레드시트 만들기
* 워크시트를 만들거나 기본 워크시트 사용
* Marketo(Marketo 웹후크에서 선언된 필드)에서 동기화할 각 필드에 대한 열을 추가합니다.

  **Zapier의 동작**

* 앱 Google 시트 선택
* &#39;스프레드시트 행 만들기&#39; 옵션을 선택합니다.
* Google Sheets 계정에 연결
* Google Sheets 스프레드시트 선택
* 워크시트 선택
* &#39;Webhooks by Zapier&#39; 트리거 앱과 Google 시트 사이의 모든 필드를 매핑합니다.

* Google Sheets 앱 테스트
* Zap 활성화

**Zap Google 시트 -> Marketo**

Zapier 대시보드에서 &#39;새 Zap 만들기&#39; 버튼을 클릭합니다.

**Zapier의 트리거**

* &#39;Google 시트&#39; 트리거 앱 선택
* 스프레드시트에서 새 행이 추가되거나 수정될 때 트리거되는 &#39;업데이트된 스프레드시트 행&#39;을 선택합니다
* Google 계정에 연결
* 트리거할 스프레드시트(이전 Zap에서 사용된 것과 동일해야 함)와 워크시트를 선택합니다
* 트리거 열을 &#39;any_column&#39;으로 설정
* Google Sheets 앱 테스트

**Zapier의 동작**

* 이전에 만든 Marketo 앱을 선택하십시오. Beta에 표시됩니다.
* Marketo 작업 &#39;Create_Update Lead&#39; 선택
* Marketo 계정에 연결하여 인증 매개 변수(Munchkin 계정 ID, 클라이언트 ID, 클라이언트 암호)를 채웁니다.
* Google Sheets의 필드를 Marketo에 매핑
* 결국 새 잠재 고객이 이동할 파티션 이름(Marketo 인스턴스에 파티션이 있는 경우에만) 채우기
* Marketo 앱 테스트
* Zap 활성화

### 결론

Zapier용 Marketo 커넥터에 대한 몇 가지 개선 아이디어는 다음과 같습니다.

* 다양한 Marketo 개체(목록, 사용자 지정 개체 등)와 관련된 기타 트리거 및 작업 추가
* Marketo에서 필드를 하드 코딩하는 대신 Marketo에서 필드를 동적으로 가져올 수 있지만 이렇게 하려면 Marketo과 Zapier 간의 기술 번역 작업이 필요합니다.
* 개발 팀과 커넥터를 공유하여 최종적으로 GA(일반 배포)할 수 있습니다.

Zapier가 Premium Marketo 어댑터를 배포하면 사용 사례를 훨씬 쉽게 구현할 수 있습니다. 어떤 경우든 이 문서는 항상 무료 Zapier 플랜이 있는 Zapier와 Marketo을 통합하고 프리미엄 어댑터에서 지원하지 않을 수 있는 사용자 지정 사용 사례를 빌드하는 데 활용할 수 있습니다. 이 글을 재미있게 읽으시길 바라며, Marketo과 자피에를 통해 더욱 성공적인 작업을 하실 수 있도록 많은 도움이 되시길 바랍니다. 감사합니다!

_David_&#x200B;이(가) _2016-04-17_&#x200B;에 게시함

## 2016년 봄 업데이트

**REST API**

* 자산 API - 웹 페이지
   * **랜딩 페이지**&#x200B;이(가) 이제 15개의 새 끝점을 통해 노출되므로 랜딩 페이지를 만들고, 업데이트하고, 삭제하고, 복제하고, 초안 관리를 할 수 있습니다. 이제 랜딩 페이지 템플릿에도 초안 관리 엔드포인트가 노출됩니다
      * 랜딩 페이지 가져오기
      * ID별 랜딩 페이지 가져오기
      * 이름별 랜딩 페이지 가져오기
      * 랜딩 페이지 만들기
      * 랜딩 페이지 메타데이터 업데이트
      * 랜딩 페이지 콘텐츠 가져오기
      * 랜딩 페이지 콘텐츠 섹션 추가
      * 랜딩 페이지 콘텐츠 섹션 업데이트
      * 랜딩 페이지 콘텐츠 섹션 삭제
      * 다이내믹 콘텐츠 섹션 가져오기
      * 다이내믹 콘텐츠 섹션 업데이트
      * 랜딩 페이지 초안 삭제
      * 랜딩 페이지 승인
      * 랜딩 페이지 초안 이름 바꾸기 취소
      * 랜딩 페이지 삭제
   * **랜딩 페이지 템플릿**
      * 랜딩 페이지 템플릿 초안 삭제
      * 랜딩 페이지 템플릿 승인
      * 랜딩 페이지 템플릿 이름 바꾸기 취소
      * 랜딩 페이지 템플릿 삭제
   * **Forms**&#x200B;에는 API를 통해 전체 생성, 편집 및 관리 기능을 제공하는 21개의 새로운 엔드포인트가 릴리스되었습니다. API는 Forms 1.0 양식 변경을 지원하지 않습니다.
      * Forms 가져오기
      * ID로 양식 가져오기
      * 이름별 양식 가져오기
      * 양식 필드 목록 가져오기
      * 양식 필드 목록 업데이트
      * 양식 만들기
      * 감사 인사 페이지 양식 받기
      * 양식 업데이트 감사 페이지
      * 양식 업데이트
      * 양식 초안 삭제
      * 승인 양식
      * 양식 승인 취소
      * 양식 복제
      * 양식 삭제
      * 양식 필드 업데이트
      * 양식 필드 제거
      * 양식 필드 가시성 규칙 업데이트
      * 리치 텍스트 양식 필드 추가
      * 필드 세트 추가
      * 필드 집합에서 필드 제거
      * 사용 가능한 양식 필드 가져오기
      * 양식 필드 위치 변경
      * 업데이트 제출 단추
   * **프로그램 가져오기 또는 찾아보기**&#x200B;를 사용하는 경우 SFDC 캠페인에 연결된 프로그램에 대해 SFDC 캠페인 ID가 반환됩니다

**사용자 지정 개체** 사용자 지정 개체에서 이제 텍스트 영역 데이터 형식을 지원하므로 최대 2000자의 문자열 필드를 이 형식의 사용자 지정 개체 필드에 저장할 수 있습니다. **IP 주소 허용 목록에 추가** 관리자는 API를 통한 권한 없는 액세스를 방지하기 위해 IP 주소 허용 목록을 관리할 수 있습니다. [이 기능에 대한 자세한 내용은 여기를 참조하십시오](https://experienceleague.adobe.com/ko/docs/marketo/using/home). **사용자 지정 활동 UI** 관리자 사용자는 이제 관리 메뉴에서 사용자 지정 활동 유형을 정의하고 [사용자 지정 활동 추가](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST) API를 통해 리드에 레코드를 추가할 수 있습니다. [사용자 지정 활동 형식을 정의하는 방법은 여기를 참조하십시오](https://experienceleague.adobe.com/ko/docs/marketo/using/home).

_케니_&#x200B;이(가) _2016-06-01_&#x200B;에 게시함

## 2016년 여름 업데이트

9월 23일 2016년 여름 릴리스에는 세 가지 개발자 기반 기능이 출시됩니다.

### REST API의 이메일 2.0 지원

v1.0 전자 메일 및 템플릿과만 호환되는 [기존 자산 API](/help/rest-api/assets.md)는 이제 v2.0 전자 메일 자산과 함께 사용할 수 있습니다.

### Marketo으로 리드 푸시

[잠재 고객 푸시](/help/rest-api/leads.md)은(는) 스마트 캠페인에서 더 쉽게 트리거할 수 있도록 고안된 대체 잠재 고객 동기화 방법입니다. 단일 활동 로그 항목을 생성하고 가망 고객을 연결하며 한 번의 호출로 가망 고객 레코드를 업데이트할 수 있습니다. 이는 리드가 작성하는 단일 양식과 유사하며, 기존 동기화 리드 방법을 사용하는 대신 양식 제출을 위한 프록시 방법으로 보다 쉽게 사용할 수 있습니다.

### HTTP 압축

이제 REST API는 HTTP 1.1 사양에 정의된 표준을 사용하여 응답을 압축할 수 있습니다. 이를 통해 전송 속도를 높이고 대역폭 활용도를 최소화하는 응답 크기를 줄일 수 있습니다.  

_케니_&#x200B;이(가) _2016-09-23_&#x200B;에 게시함

## Marketo에서 swagger-codegen 사용

[Swagger-codegen](https://github.com/swagger-api/swagger-codegen)은(는) swagger 정의에서 서버 스텁 및 API 클라이언트를 모두 생성할 수 있는 강력한 Java 라이브러리입니다. 이렇게 하면 특정 언어에 대한 클라이언트를 생성하는 데 드는 어려움과 비용을 획기적으로 줄일 수 있습니다. 시작하여 첫 번째 클라이언트를 생성하려면 먼저 Marketo의 Swagger 정의 중 하나의 인스턴스별 복사본을 가져오십시오. 테스트할 인스턴스의 Munchkin ID를 입력합니다. ID 정의로 시작합니다. 인스턴스에 대한 정의가 있으므로 swagger-codegen을 다운로드하여 설치해야 합니다. 프로세스는 운영 체제에만 해당되며 [여기](https://github.com/swagger-api/swagger-codegen#prerequisites)에서 지침을 얻을 수 있습니다. 기본 설정을 사용하면 codegen이 제공된 모든 끝점 및 모델을 포함하는 클라이언트를 출력합니다. 이러한 ID는 일반적으로 &#39;docs&#39; 폴더에 제공된 예제를 사용하여 사용 가능한 끝점을 호출하는 메서드가 포함된 DefaultApi라는 클래스를 통해 관리됩니다(기본적으로 모든 언어에 이에 대한 템플릿이 포함되는 것은 아님). 이제 첫 번째 클라이언트를 빌드합니다. 코드를 저장할 폴더를 만들고 터미널 세션으로 이동한 다음 generate 명령을 사용하여 원하는 언어로 클라이언트를 작성합니다(homebrew 설치 방법을 사용했다고 가정해 보겠습니다).

swagger-codegen 생성 -i $definitionLocation -l $yourLanguage -o $yourLocation

이렇게 하면 클라이언트 코드가 원하는 위치에 출력됩니다. 이제 ID 끝점을 호출하고 액세스 토큰을 가져오기 위해 사용하는 방법을 살펴보겠습니다.

```java
 public static void main(String[] args){
  String client_id = args[0];
  String client_secret = args[1];
  ApiClient client = new ApiClient();
  DefaultApi id = new DefaultApi();
  try {
   String token = id.identityOauthTokenGet(client_id, client_secret, "client_credentials").getAccessToken();
   System.out.println(token);
  } catch (ApiException e) {
   e.printStackTrace();
  }
 }
```

```php
<?php
require_once(_DIR_ . '/vendor/autoload.php');

$api_instance = new Swagger\\Client\\Api\\DefaultApi();
$client_id = "client_id_example";
$client_secret = "client_secret_example";
$grant_type = "grant_type_example";

try {
    $result = $api_instance->identityOauthTokenGet($client_id, $client_secret, $grant_type);
    print_r($result->getAccessToken);
} catch (Exception $e) {
    echo 'Exception when calling DefaultApi->identityOauthTokenGet: ', $e->getMessage(), "\\n";
}
?>
```

```c#
  public static void Main(string[] args)
  {
      string clientId = "CHANGE ME";
      string clientSecret = "CHANGE ME";

      IdentityApi instance = new IdentityApi();
      ResponseOfIdentity response = instance.IdentityUsingGET(clientId, clientSecret, "client_credentials");

      string message = string.Format("Access Token: {0}, Expires In: {1}, Scope: {2}, Token Type: {3}",
          response.AccessToken, response.ExpiresIn, response.Scope, response.TokenType);
      Console.WriteLine(message);
  }
```

이제 인증을 받는 방법을 알았으므로 앞으로 몇 주 이내에 자동 생성된 클라이언트의 고급 사용 사례를 살펴보겠습니다.

_케니_&#x200B;이(가) _2016-10-10_&#x200B;에 게시함

## Excel 통합 1부: 파워 쿼리를 사용하여 Marketo 데이터 추출 및 셰이핑

Microsoft Excel에 내장된 Power BI 기술을 활용하여 Marketo과 함께 진정한 셀프 서비스 비즈니스 분석 경험을 만드는 방법을 설명하는 일련의 문서 중 첫 번째 것입니다. 이 문서에서 다루는 개념으로 다음을 수행할 수 있습니다.

* Marketo에서 Excel로 데이터 가져오기
* 다른 소스(SaaS 애플리케이션, 데이터베이스, 플랫 파일 등)에서 데이터 가져오기 및 결합
* 비즈니스 요구 및 분석 목적을 위한 모양 데이터
* Excel에서 데이터를 요청 시 새로 고침
* 공식을 사용하여 계산된 열 및 측정값 만들기
* 이기종 데이터 간의 관계 생성
* 피벗 테이블 및 피벗 차트를 사용하여 데이터 분석 및 고급 보고서 작성
* 놀라운 데이터 시각화 제작

### Excel용 파워 쿼리

이 첫 번째 문서에서는 Power Query 기술을 사용한 데이터 가져오기 및 셰이핑 프로세스에 대해 설명합니다. 파워 쿼리는 분석 요구를 충족하도록 데이터 소스를 검색, 연결, 결합 및 세분화할 수 있는 데이터 연결 기술입니다. Power Query의 기능은 Excel 및 Power BI Desktop에서 사용할 수 있습니다. 파워 쿼리는 데이터베이스, Facebook, Salesforce, MS Dynamics CRM 등과 같은 다양한 데이터 소스에 연결할 수 있습니다. Marketo은 즉시 지원되지 않지만, 다행히도 많은 시스템 기능을 원격으로 실행하기 위해 Marketo REST API를 사용할 수 있으며, 파워 쿼리에는 사용자 지정 데이터 소스를 스크립팅할 수 있는 풍부한 수식 집합(비공식적으로 &quot;M&quot;이라고 함)이 포함되어 있습니다.

### 사용자 지정 커넥터

Power Query를 사용하면 단일 REST API 호출을 스크립팅하는 것이 간단하지만 다음 요구 사항을 처리하는 것이 더 어려워집니다.

* 인증 메커니즘 및 주기적 토큰 새로 고침을 포함한 액세스 토큰 관리
* 대용량 데이터 세트에 대한 페이지 매김 메커니즘
* 오류 처리

이 문서에서는 모든 종류의 데이터(리드, 활동, 사용자 지정 개체, 프로그램 등)를 가져오기 위해 Marketo의 REST API를 사용할 수 있는 강력한 사용자 지정 커넥터를 빌드하는 방법을 설명합니다. 유일한 제한 사항은 Marketo API 일일 요청 제한까지 적용됩니다. 여기에서 설명하는 개념은 Marketo에 중점을 두지만, REST API를 제공하는 다른 SaaS 솔루션을 통합하는 데 사용할 수도 있습니다.

### 사전 요구 사항

#### 파워 쿼리

Excel 2016 릴리스 이전에는 Excel용 Microsoft Power Query가 Excel 2010 또는 Excel 2011에 다운로드 및 설치된 Excel 추가 기능으로 작동했습니다. Excel 2016에서 이 기술은 &#39;가져오기 및 변환&#39; 섹션 아래의 &#39;데이터&#39; 리본에 통합된 기본 기능입니다. 이 문서에 대해 제작된 모든 스크립트는 Excel 2016 for Windows에서 테스트되었습니다. Excel 2013 또는 Excel 2010의 개념은 동일해야 하지만 일부 수정이 필요할 수 있습니다.  파워 쿼리는 현재 Excel의 Microsoft Windows 버전에서만 사용할 수 있으며 Mac 버전은 지원되지 않습니다.

#### Marketo

파워 쿼리는 Marketo REST API를 사용하여 Marketo의 데이터에 액세스합니다. 이러한 API를 사용하려면 Marketo 인스턴스의 관리자인 경우 직접 만들 수 있는 API 사용자 및 사용자 지정 서비스가 필요합니다. 그렇지 않은 경우 관리자가 제공해야 합니다. Marketo API 사용자 및 사용자 지정 서비스를 만드는 방법에 대한 단계별 설명은 [여기](/help/rest-api/custom-services.md)에서 확인할 수 있습니다. 완료되면 Marketo REST API를 호출하기 위한 다음 자격 증명이 있어야 합니다. **클라이언트 ID** 및 **클라이언트 암호**. **REST API 끝점**&#x200B;은(는) Marketo의 웹 서비스 관리자에 있는 REST API 섹션에서 찾을 수 있으며 다음 패턴을 가져야 합니다.

`<https://XXX-XXX-XXX.mktorest.com/rest>`

Marketo에는 API에 대한 일일 요청 제한이 있으며, 이 제한은 사용량 보고서와 함께 웹 서비스 관리자에서 찾을 수 있습니다. **보고서의 일부 데이터를 놓칠 수 있으므로 쿼리를 디자인할 때 일일 한도를 절대 초과하지 않도록 합니다**.

### 파워 쿼리 통합 문서 만들기

새 Excel 통합 문서로 시작하겠습니다. 모든 Marketo REST API 설정을 선언하기 위한 특정 구성 워크시트를 만듭니다. 이 워크시트에서는 세 개의 테이블을 만듭니다.

열: **URL**: Marketo REST API 끝점이 있는 테이블 &#39;**REST_API_Authentication**&#39;. **클라이언트 ID**: Marketo REST API OAuth2.0 자격 증명에서 가져온 것입니다. **클라이언트 암호**: Marketo REST API OAuth2.0 자격 증명에서.
다음 열이 있는 테이블 &#39;**Scoping**&#39;: **Paging Token SinceDatetime**: ISO 8601 표준 날짜 표기법 다음의 날짜(예: &quot;2016-10-06T13:22:17-08:00&quot;, &quot;2016-10-06&quot;은 올바른 날짜/시간)입니다. 이 날짜는 초기 &#39;날짜 기반&#39; 페이징 토큰 덕분에 지정된 기간 이후 Marketo 활동을 가져오는 데 사용됩니다. 이 날짜는 주로 통합 문서로 가져올 데이터의 양을 제한하는 데 사용됩니다. **목록 ID**: 처리 중인 모든 리드/연락처를 참조하는 Marketo 내 정적 목록의 ID입니다. 이 정적 목록은 Marketo에서 자유롭게 관리할 수 있습니다(예: 스마트 캠페인이 리드 및 연락처를 통해 정기적으로 또는 실시간으로 제공할 수 있음).
정적 목록의 ID를 가져오려면 Marketo에서 열고 URL에서 해당 숫자 ID를 가져옵니다(예: `<https://myorg.marketo.com/#ST3517A1LA1>`, 목록 ID=3511). **최대 레코드 페이지**: 페이지당 최대 레코드 수가 300개인 &#39;위치 기반&#39; 페이징 토큰을 사용하여 Marketo 출력 데이터를 반복하는 의사 재귀 알고리즘에 사용됩니다. 한 페이지에 가능한 많은 레코드를 저장하는 것이 저희의 관심사이기 때문에 300개를 고수하겠습니다. 따라서 일반적으로 최대 레코드 페이지가 33.333으로 설정되면 최대 레코드 용량은 33.333 X 300 = 9999백만 레코드의 용량을 의미하지만 Marketo API 일일 요청 제한에서도 33.333K를 의미합니다. 쿼리의 모든 데이터가 획득되면 알고리즘은 중지됩니다. 따라서 이 매개 변수는 루프에 대한 안전 제한일 뿐입니다.

`Leads` 테이블(열: **리드 필드**: 리드 및 연락처를 쿼리할 때 Marketo에서 수집할 쉼표로 구분된 리드 필드). Excel에서 표를 선언하는 것은 간단합니다. 스프레드시트에 열 이름과 값을 사용하여 두 행을 입력하고 표의 주변을 마우스로 강조 표시한 다음 &#39;삽입&#39; 메뉴에서 표 아이콘을 선택한 다음 이름을 지정합니다. 테이블과 해당 열에 지정된 이름은 스크립트에서 직접 호출되므로 중요합니다.

## 인증 및 액세스 토큰

### Marketo REST API 인증 기본 정보

Marketo의 REST API는 2개의 레그 OAuth 2.0으로 인증됩니다. 클라이언트 ID 및 클라이언트 암호는 사용자가 정의하는 사용자 정의 서비스에서 제공합니다. 각 사용자 정의 서비스는 서비스가 특정 작업을 수행하도록 권한을 부여하는 역할 및 권한 집합을 가진 API 전용 사용자가 소유합니다. 액세스 토큰은 단일 사용자 정의 서비스에 연결됩니다.
전체 인증 메커니즘은 Marketo 개발자 사이트에 [여기](/help/rest-api/authentication.md)에 설명되어 있습니다. 액세스 토큰이 원래 생성될 때 그 수명은 3600초 또는 1시간이다. 동일한 사용자 지정 서비스에 대한 각 연속 인증 호출은 현재 액세스 토큰과 남은 수명을 반환합니다. 토큰이 만료되면 인증은 완전히 새로운 액세스 토큰을 반환합니다. 통합이 원활하게 작동하고 정상 작동 중에 예기치 않은 인증 오류가 발생하지 않도록 하려면 액세스 토큰 만료 관리가 중요합니다.

#### 쿼리 만들기

&#39;데이터&#39; 메뉴의 &#39;Get&amp;Transform&#39; 섹션에서 &#39;새 쿼리&#39; 아이콘을 클릭하여 새 쿼리를 만듭니다. 시작할 빈 쿼리를 선택하고 &#39;MktoAccessToken&#39;과 같은 이름을 지정합니다. 쿼리 편집기에서 고급 편집기를 시작하여 일부 파워 쿼리 공식을 수동으로 스크립팅할 수 있습니다. 고급 편집기에 다음 코드를 입력합니다.

```
let
    // Get url and credentials from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    clientIdStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client ID],
    clientSecretStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client Secret],

    // Calling Marketo API Get Access Token
    getAccessTokenUrl = mktoUrlStr & "/identity/oauth/token?grant_type=client_credentials&client_id=" & clientIdStr & "&client_secret=" & clientSecretStr,
    TokenJson = try Json.Document(Web.Contents(getAccessTokenUrl)) otherwise "Marketo REST API Authentication failed, please check your credentials",

    // Parsing access token
    accessTokenStr = TokenJson [access_token]

in
    accessTokenStr
```

&quot;/&quot; 앞에 소스 코드에 포함된 주석은 코드를 설명이 가능하도록 합니다. 함수 참조가 필요한 경우 이 문서의 참조 섹션에 제공된 링크를 확인하십시오. &quot;완료&quot; 단추를 클릭합니다. 마지막으로 적용된 단계 &#39;accessTokenStr&#39;에 대한 액세스 토큰이 출력에 성공적으로 표시되는지 확인하십시오.  Excel의 보안에 대한 한 가지 빠른 주석입니다. 노란색 배너에서 외부 데이터 연결을 활성화하라는 메시지가 표시될 수 있습니다. 이 작업은 쿼리가 제대로 작동하도록 하는 데 필요합니다.

#### 쿼리를 함수로 변환

고급 편집기로 돌아가서 다음 함수 선언으로 코드를 래핑합니다.

```
let
    FnMktoGetAccessToken =()=>

        let
            // Get url and credentials from config worksheet - Table REST_API_Authentication
            mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
            clientIdStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client ID],
            clientSecretStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[Client Secret],

            // Calling Marketo API Get Access Token
           getAccessTokenUrl = mktoUrlStr & "/identity/oauth/token?grant_type=client_credentials&client_id=" & clientIdStr & "&client_secret=" & clientSecretStr,
           TokenJson = try Json.Document(Web.Contents(getAccessTokenUrl)) otherwise "Marketo REST API Authentication failed, please check your credentials",

            // Parsing access token from Json
           accessTokenStr = TokenJson [access_token]

        in
            accessTokenStr

in FnMktoGetAccessToken
```

함수는 입력에 매개 변수를 사용하지 않지만 구성 워크시트에서 가져옵니다. 액세스 토큰을 출력으로 생성합니다. 쿼리 이름을 `FnMktoGetAccessToken`로 바꾸고 저장합니다. 데이터 메뉴의 &#39;가져오기 및 변환&#39; 섹션에서 &#39;쿼리 표시&#39; 버튼을 클릭하면 Excel에서 언제든지 모든 쿼리를 볼 수 있습니다. 이제 함수를 함수 아이콘 &#39;Fx&#39;로 표시해야 합니다.

### 정적 목록의 구성원 로드

#### 리드 가져오기

Marketo 리드 API는 리드 레코드에 대한 간단한 CRUD 작업, 정적 목록 및 프로그램에서 리드의 멤버십을 수정하고, 리드에 대한 스마트 캠페인 처리를 시작하는 기능을 제공합니다. 이러한 모든 기능은 [여기](/help/rest-api/leads.md)에 설명되어 있습니다. 정적 목록 또는 프로그램의 멤버십을 기반으로 대규모 잠재 고객 레코드 집합을 검색할 수 있습니다. 정적 목록의 ID를 사용하면 해당 정적 목록의 멤버인 모든 리드 레코드를 검색할 수 있습니다. 목록의 ID는 호출의 경로 매개 변수입니다. 자세한 내용은 Marketo 개발자 설명서의 &quot;목록 및 프로그램 멤버십&quot; 장을 참조하십시오. API 호출당 가져올 수 있는 최대 리드 레코드 수는 300개이므로 페이지 토큰을 활용하여 300개의 레코드 페이지당 레코드를 수집해야 합니다. 첫 번째 호출 후에 Json 응답에 페이징 토큰을 가져오고 페이징 토큰이 더 이상 출력에 없는 경우 완료되었음을 알 수 있습니다.

### 기본 쿼리

정적 목록에서 모든 잠재 고객을 다운로드하는 데 목적이 있는 완전히 기능하는 쿼리를 시작하겠습니다. &#39;MktoLeads&#39;라는 새 빈 쿼리를 만들고 고급 편집기에 다음 코드를 입력합니다.

```
let
    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the number of iterations (pages of 300 records) - Table Scoping
    iterationsNum = Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Max Records Pages],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),
    // Get the Lead fields to extract - Table Leads
    LeadFieldsStr = Excel.CurrentWorkbook(){[Name="Leads"]}[Content]{0}[Lead Fields],


    // Build Multiple Leads by List Id URL
    getMultipleLeadsByListIdUrl = mktoUrlStr & "/rest/v1/list/" & listIdStr & "/leads.json?fields=" & LeadFieldsStr,

    // Build Marketo Access Token URL parameter
    accessTokenParamStr = "&access_token=" & FnMktoGetAccessToken(),

    pagingTokenParamStr = "",

    // Function iterating though the pages
    FnProcessOnePage =
    (accessTokenParamStr, pagingTokenParamStr) as record =>
        let

            // Send REST API Request
            content = Web.Contents(getMultipleLeadsByListIdUrl & accessTokenParamStr & pagingTokenParamStr),

            // Recover Json output and watch if token is expired, in that case, regenerate access token
            newAccessTokenParamStr = if Json.Document(content)[success]=true then accessTokenParamStr else "?access_token=" & FnMktoGetAccessToken(),
            getMultipleLeadsByListIdJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(getMultipleLeadsByListIdUrl & newAccessTokenParamStr & pagingTokenParamStr)),

            // Parse Json outputs: data and next page token
            data = try getMultipleLeadsByListIdJson[result] otherwise null,
            next  = try  "&nextPageToken=" & getMultipleLeadsByListIdJson[nextPageToken] otherwise null,
            res = [Data=data, Next=next, Access=newAccessTokenParamStr]
        in
            res,

    // Generates a list of values given four functions that generate the initial value initial, test against a condition, and if successful select the result and generate the next value next. An optional parameter, selector, may also be specified
    GeneratedList =
        List.Generate(
            ()=>[i=0, res = FnProcessOnePage(accessTokenParamStr, pagingTokenParamStr)],
            each [i]<iterationsNum and [res][Data]<>null,
            each [i=[i]+1, res = FnProcessOnePage([res][Access],[res][Next])],
            each [res][Data])
in
    GeneratedList
```

Power Query는 기존 루프 함수를 제공하지 않습니다(예: For-loop, While-loop) 및 은 재귀를 지원하지 않습니다. List.Generate를 사용하여 For-loop를 구현하는 것이 좋습니다. 이 함수는 [여기](http://msdn.microsoft.com/query-bi/m/list-generate)에 설명되어 있습니다. 목록 포함. 페이지를 반복할 수 있도록 생성합니다. 반복의 각 단계에서 데이터 페이지를 추출하고, 다음 페이지에 대한 페이징 토큰을 포함하는 URL을 유지하고, 결과를 생성된 목록의 다음 항목에 저장합니다. [Datachant](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/)의 블로그는 이 문제를 해결하는 데 유용한 리소스입니다. 매개 변수 &#39;최대 레코드 페이지&#39;는 페이지 수를 제한하고 무한 루프를 피하는 사실적인 범위로 제한하기 위해 여기에 있습니다. 또 다른 과제는 액세스 토큰이 만료되지 않았는지 확인하는 것입니다. 남은 수명을 추적하는 것은 파워 쿼리와 너무 복잡합니다. 따라서 REST API에 대한 모든 호출은 오류 확인과 함께 백업됩니다. 오류가 발생하면 토큰이 만료되었다고 가정하고 먼저 갱신한 다음 호출을 다시 재생합니다. 두 번째 호출이 실패하면 두 번째 실패가 Excel에 통지됩니다(최악의 경우, 데이터가 수신되지 않음). 쿼리를 저장한 후 또는 언제든지 &#39;새로 고침 버튼&#39;을 클릭하여 쿼리를 실행합니다.  우리의 경우 5개 목록 내 5개 데이터 페이지에 1364개의 리드 레코드가 맞춰져 추출되었다.

### 데이터 셰이핑

이러한 모든 레코드를 하나의 단순 레코드 목록에 포함하도록 데이터를 형성해야 합니다. 두 가지 방법으로 이 작업을 수행할 수 있습니다.

* 추가 코드 사용
* 파워 쿼리 UI 활용

출력 그리드를 마우스 오른쪽 단추로 클릭하고 상황별 메뉴에서 &#39;표로&#39;를 선택하여 목록 표로 변환합니다.  &#39;대상 테이블&#39; 팝업에서 2개의 선택 목록에 기본값을 둡니다.  이제 결과 목록 표를 확장합니다. 이제 모든 레코드가 단일 목록에 있습니다. Json 형식으로 인코딩된 레코드에는 필드와 관련 값이 포함됩니다. 다시 확장합니다. 팝업에서 유지할 모든 필드를 선택하고 &#39;원래 열 이름을 접두사로 사용&#39; 확인란의 선택을 취소합니다.  에볼라! 모든 레코드가 우리 테이블에 잘 표시됩니다. 고급 편집기를 다시 열면 데이터를 형성하기 위해 3개의 코드 줄이 추가되었음을 알 수 있습니다.

```
# "Converted to Table" = Table.FromList(GeneratedList, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
# "Expanded Column1" = Table.ExpandListColumn(#"Converted to Table", "Column1"),
# "Expanded Column2" = Table.ExpandRecordColumn(#"Expanded Column1", "Column1", {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"}, {"id", "updatedAt", "lastName", "email", "createdAt", "firstName"})
```

계산된 값으로 추가 열을 만드는 것처럼, 파워 쿼리를 사용하면 더 많은 작업을 수행할 수 있습니다. 나중에 몇 가지 더 많은 가능성을 볼 수 있습니다. 이 쿼리를 저장하고 닫겠습니다. 이제 언제든지 수동으로 새로 고치거나 백그라운드 새로 고침을 통해 자동으로 새로 고칠 수 있습니다.

### 결과 리디렉션

이제 문제는 결과 데이터를 어디로 보낼 것인가 하는 것입니다. 마우스를 쿼리 위에 놓고 상황에 맞는 메뉴에서 &#39;다음으로 로드...&#39; 메뉴를 선택합니다. 팝업에서 다음을 선택할 수 있습니다.

* &#39;테이블&#39; 셰이핑된 모든 데이터를 워크시트(새 데이터 또는 기존 데이터)에 보내려면
* Power Pivot에서 추가 분석을 수행하는 것이 목표인 경우 &#39;연결만 만들기&#39;입니다.

&#39;데이터 모델에 추가&#39; 확인란을 사용하면 Power Pivot에서 데이터를 활용할 수 있습니다. 이 문서의 두 번째 부분에서 원하는 내용입니다.

### 페이지 매김 관리

프로젝트의 목표는 더 많은 쿼리를 작성하는 것이므로 몇 가지 리팩터링을 수행하고 페이지 매김 을 관리하는 재사용 가능한 기능을 추출해 보겠습니다. **FnMktoGetPagedData**&#x200B;이라는 빈 쿼리를 새로 만들고 고급 편집기에 다음 코드를 입력합니다.

```
let
    FnMktoGetPagedData =(url, accessTokenParamStr, pagingTokenParamStr)=>

    let

        // Get the number of iterations (pages of 300 records) - Table Scoping
        iterationsNum = Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Max Records Pages],

        // Sub-function iterating though the REST API service result pages
        FnProcessOnePage =
        (accessTokenParamStr, pagingTokenParamStr) as record =>
            let

                // Send REST API Request
                content = Web.Contents(url& accessTokenParamStr & pagingTokenParamStr),

                // Recover Json output and watch if token is expired, in that case, regenerate access token
                newAccessTokenParamStr = if Json.Document(content)[success]=true then accessTokenParamStr else "?access_token=" & FnMktoGetAccessToken(),
                contentJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(url & newAccessTokenParamStr & pagingTokenParamStr)),

                // Parse Json outputs: data and next page token
                data = try contentJson[result] otherwise null,
                next  = try  "&nextPageToken=" & contentJson[nextPageToken] otherwise null,
                res = [Data=data, Next=next, Access=newAccessTokenParamStr]
            in
                res,

        // Generates a list of values given four functions that generate the initial value initial, test against a condition, and if successful select the result and generate the next value next. An optional parameter, selector, may also be specified
        GeneratedList =
            List.Generate(
                ()=>[i=0, res = FnProcessOnePage(accessTokenParamStr, pagingTokenParamStr)],
                each [i]<iterationsNum and [res][Data]<>null,
                each [i=[i]+1, res = FnProcessOnePage([res][Access],[res][Next])],
                each [res][Data])
    in
        GeneratedList

in FnMktoGetPagedData
```

쿼리를 저장합니다. 우리는 다음에 그것을 사용할 것입니다.

### 간소화된 쿼리

**FnMktoGetPagedData** 함수를 호출하는 &#39;MktoLeads&#39; 쿼리를 다시 작성해 보겠습니다.

```
let
    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),
    // Get the Lead fields to extract - Table Leads
    LeadFieldsStr = Excel.CurrentWorkbook(){[Name="Leads"]}[Content]{0}[Lead Fields],


    // Build Multiple Leads by List Id URL
    getMultipleLeadsByListIdUrl = mktoUrlStr & "/rest/v1/list/" & listIdStr & "/leads.json?fields=" & LeadFieldsStr,

    // Build Marketo Access Token URL parameter
    accessTokenParamStr = "&access_token=" & FnMktoGetAccessToken(),

    // No initial paging token required for this call
    pagingTokenParamStr = "",

    // Invoke the multiple REST API calls through the FnMktoGetPagedData function
    result = FnMktoGetPagedData (getMultipleLeadsByListIdUrl , accessTokenParamStr, pagingTokenParamStr)

in
    result
```

보시다시피, 우리의 쿼리는 이제 읽고 유지 관리하기 정말 간단합니다. 다른 쿼리에 대해 **FnMktoGetPagedData** 함수를 다시 활용하려고 합니다.

### 정의된 기간에서 특정 활동 로드

#### 페이지 매김이 있는 활동 가져오기

Marketo은 리드 레코드와 관련된 매우 다양한 활동 유형을 허용합니다. 거의 모든 변경, 작업 또는 흐름 단계가 리드의 활동 로그에 기록되며 API를 통해 검색되거나 Smart List 및 Smart Campaign 필터 및 트리거에서 활용될 수 있습니다. 활동은 항상 레코드의 ID에 해당하는 leadId를 통해 잠재 고객 레코드와 다시 관련되며 고유한 정수 ID도 있습니다. 전체 REST API 설명서 [여기](/help/rest-api/activities.md)를 찾았습니다.

잠재적인 활동 유형은 매우 많으며, 구독마다 다를 수 있으며 각각에 대해 고유한 정의가 있습니다. 모든 활동에는 고유한 ID, leadId 및 activityDate가 있지만 primaryAttributeValueId 및 primaryAttributeValue의 의미는 달라집니다. 여기에서는 ID 41이 있는 Marketo 추적 활동의 한 종류인 Interesting Moments에 대해 중점적으로 살펴봅니다. 우리가 해결할 새로운 과제는 다음과 같습니다.

* 활동이 발생한 기간을 정의하려면 &#39;날짜 기반&#39; 페이징 토큰을 시작해야 합니다.
* 데이터를 형성하는 것은 활동 유형에 따라 좀 더 까다로우며, 활동별 속성 목록은 Json에 제공되며 분석을 용이하게 하기 위해 구문 분석하고 병합해야 합니다.

#### 날짜 기반 페이징 토큰

먼저 활동 쿼리 기간 범위를 지정하는 데 필요한 초기 &#39;날짜 기반&#39; 페이징 토큰을 생성하기 위해 이 함수를 빌드해야 합니다. 페이징 토큰 [여기](/help/rest-api/paging-tokens.md)에 대한 설명서를 찾았습니다. **FnMktoGetPagingToken**&#x200B;이라는 빈 쿼리를 새로 만들고 고급 편집기에 다음 코드를 입력하십시오.

```
let
    FnMktoGetPagingToken =(accessTokenStr)=>

        let
            // Get url from config worksheet - Table REST_API_Authentication
            mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],

            // Get Paging Token SinceDatetime from config worksheet - Table Scoping
            mktoPTSinceDatetimeStr = DateTime.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[Paging Token SinceDatetime], "yyyy-MM-ddThh:mm:ss"),

            // Building URL for API Call
            getPagingTokenUrl = mktoUrlStr & "/rest/v1/activities/pagingtoken.json?access_token=" & accessTokenStr & "&sinceDatetime=" & mktoPTSinceDatetimeStr,

            // Calling Marketo API Get Paging Token
            content = Web.Contents(getPagingTokenUrl),

            // Recover Json output and watch if access token is expired, in that case, regenerate it
            newAccessTokenStr = if Json.Document(content)[success]=true then accessTokenStr else "?access_token=" & FnMktoGetAccessToken(),
            pagingTokenJson = if Json.Document(content)[success]=true then Json.Document(content) else Json.Document(Web.Contents(mktoUrlStr & "/rest/v1/activities/pagingtoken.json?access_token=" & newAccessTokenStr & "&sinceDatetime=" & mktoPTSinceDatetimeStr)),

            // Parsing Paging Token
            pagingTokenStr = pagingTokenJson[nextPageToken]

        in
            pagingTokenStr

in FnMktoGetPagingToken
```

함수를 저장합니다. 우리는 다음에 그것을 사용할 것입니다.

#### 즐거운 순간 활동

이제 **FnMktoGetPagedData** 및 **FnMktoGetPagingToken** 함수를 호출하는 &#39;MktoInterestMomentsActivities&#39; 쿼리를 작성해 보겠습니다.

```
let

    // Get Url from config worksheet - Table REST_API_Authentication
    mktoUrlStr = Excel.CurrentWorkbook(){[Name="REST_API_Authentication"]}[Content]{0}[URL],
    // Get the List id - Table Scoping
    listIdStr = Number.ToText(Excel.CurrentWorkbook(){[Name="Scoping"]}[Content]{0}[List ID], "D", ""),

    // Build Get Activities URL
    getActivitiesUrl = mktoUrlStr & "/rest/v1/activities.json?ListId=" & listIdStr & "&activityTypeIds=46",

    // Build Marketo Access Token URL parameter
    accessTokenStr = FnMktoGetAccessToken(),
    accessTokenParamStr = "&access_token=" & accessTokenStr,

    // Obtain date-based paging token used to scope in time the activities
    pagingTokenParamStr = "&nextPageToken=" & FnMktoGetPagingToken(accessTokenStr),

    // Invoke the multiple REST API calls through the FnMktoGetPagedData function
    result = FnMktoGetPagedData (getActivitiesUrl , accessTokenParamStr, pagingTokenParamStr)

in
    result
```

이 쿼리의 결과는 다시 목록 목록이므로 분석에 사용할 수 있는 추가 데이터 처리가 필요합니다.

### 데이터 셰이핑

리드에 대해 수행한 것과 동일한 셰이핑 작업을 수행해 보겠습니다.

* 출력 그리드를 마우스 오른쪽 단추로 클릭하고 상황별 메뉴에서 &#39;표로&#39;를 선택하여 목록 표로 변환합니다.
* 결과 목록 표를 확장합니다.
* 팝업에서 유지할 모든 필드를 선택하여 한 번 더 확장합니다(&#39;원래 열 이름을 접두사로 사용&#39; 확인란 선택 취소).

흥미로운 모멘트와 연관된 특정 속성 목록이 여전히 포함된 열 &quot;속성&quot;을 제외하고 해당 값이 있는 열을 볼 수 있습니다. 이러한 속성을 확장해 보겠습니다. 이제 목록이 레코드로 확장되었으며 원하는 필드(각 속성의 이름 및 값)를 선택하여 다시 확장하고 &#39;원래 열 이름을 접두사로 사용&#39; 확인란 선택을 취소합니다.  따라서 속성을 포함하여 모든 데이터가 표시되지만 각 흥미로운 순간 활동은 3행에 걸쳐 있습니다. 이것은 우리의 분석에 사용하기 어려울 것입니다.  모든 속성이 추가 열로 표시되는 활동당 한 줄만 사용하는 것이 이상적입니다. 우리는 우리 표에서 세 가지 속성을 돌려서 쉽게 그렇게 할 수 있다. 활동 속성에서 2개의 열 &quot;이름&quot; 및 &quot;값&quot;을 선택하고 &quot;변형&quot; 메뉴에서 &quot;피벗 열&quot;을 클릭합니다. 팝업에서 고급 옵션을 요청하고 &#39;Values Column&#39; = value 및 &#39;Don&#39;t aggregate&#39; 값 함수를 선택합니다.  &#39;확인&#39;을 클릭하면 활동당 한 줄의 데이터를 출력해야 합니다.  다음 &#39;데이터 셰이핑&#39; 코드 행을 쿼리 스크립트에 자동으로 추가해야 합니다.

```
  #"Converted to Table" = Table.FromList(result, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Expanded Column1" = Table.ExpandListColumn(#"Converted to Table", "Column1"),
    #"Expanded Column2" = Table.ExpandRecordColumn(#"Expanded Column1", "Column1", {"id", "leadId", "activityDate", "activityTypeId", "campaignId", "primaryAttributeValue", "attributes"}, {"id", "leadId", "activityDate", "activityTypeId", "campaignId", "primaryAttributeValue", "attributes"}),
    #"Expanded attributes" = Table.ExpandListColumn(#"Expanded Column2", "attributes"),
    #"Expanded attributes1" = Table.ExpandRecordColumn(#"Expanded attributes", "attributes", {"name", "value"}, {"name", "value"}),
    #"Pivoted Column" = Table.Pivot(#"Expanded attributes1", List.Distinct(#"Expanded attributes1"[name]), "name", "value")
in
    #"Pivoted Column"
```

### 다음 단계

이제 REST API를 통해 사용할 수 있는 특정 Marketo 데이터에 액세스하는 데 필요한 모든 쿼리를 디자인할 수 있습니다. 이 문서를 통해 Excel과 Marketo이 결합된 뛰어난 이점을 활용할 수 있기를 바랍니다. 두 번째 문서에서는 모든 쿼리가 있는 샘플 통합 문서도 제공됩니다.

### 참조

#### 파워 쿼리

* [파워 쿼리 - 개요 및 학습](https://support.microsoft.com/en-us/article/Power-Query-Overview-and-Learning-ed614c81-4b00-4291-bd3a-55d80767f81d)
* [파워 쿼리 수식 참조](http://msdn.microsoft.com/query-bi/m/power-query-m-reference)
* [Matt Masson 블로그](http://www.mattmasson.com/tag/power-query/)에서 파워 쿼리에 대한 유용한 리소스를 제공합니다.
* [DataChant 블로그](https://datachant.com/2016/06/27/cursor-based-pagination-power-query/)는 페이지 매김 메커니즘을 구현하는 데 매우 유용합니다

_2016-10-18_&#x200B;에 _필립_&#x200B;이 게시함

## 2016년 가을 업데이트

2016년 가을 릴리스에서는 이메일 v2 변수 및 모듈에 대한 CRUD 지원과 명명 계정에 대한 CRUD 지원을 추가하고 있습니다. 이제 Marketo REST API를 사용하여 콘텐츠를 로컬에서 읽고 편집하고, 이동, 순서 변경 및 삭제할 수 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 잠재 고객 데이터베이스 API

* [**명명 계정**](/help/rest-api/named-accounts.md)
   * 명명된 계정 읽기, 업데이트 및 삭제를 위한 새 엔드포인트
   * 알려진 문제:
      * 2016년 가을 릴리스부터 리드는 API를 통해 명명 계정과 연결될 수 없습니다

### 자산 API

* [**전자 메일**](https://developer.adobe.com/marketo-apis/api/asset/#operation/describeUsingGET_5)
   * 이메일 v2 변수 조작을 위한 새로운 엔드포인트
   * 이메일 v2 모듈 조작을 위한 새로운 엔드포인트
   * 알려진 문제:
      * 예측 토큰이 포함된 섹션에 대한 쿼리 및 업데이트에서 오류가 반환됩니다
      * 예측 토큰이 포함된 콘텐츠 섹션이 있는 이메일은 API를 사용하여 승인되지 않을 수 있습니다

_케니_&#x200B;이(가) _2016-12-07_&#x200B;에 게시함

## Twitter Handl3@MarketoDev 중단한 이유

트위터의 @MarketoDev 핸들을 폐기하기로 결정했습니다. 계정은 2011년 12월 9일에 비활성화됩니다. 왜 그런지 궁금하신가요? **2014년 초로 되감기...** 개발자가 API를 기반으로 빌드할 수 있도록 Marketo Developers Site를 시작한 지 얼마 되지 않았습니다. Marketo 플랫폼에 대한 인식을 높이고 개발자의 진입 장벽을 낮추고자 했습니다. 이러한 노력과 함께 Marketo@MarketoDev 통합 솔루션을 구축하려는 기술 파트너 및 고객과 협력하기 위해 EMC는 고객을 만들었습니다. 어떤 용감한 새 사업처럼, 우리는 이것이 어떻게 진행될지 확신할 수 없었다. 처음에는 새로운 블로그 게시물과 새로운 API 릴리스를 트윗했습니다. 상황이 좋았습니다. 개발자 사이트 트래픽이 증가했습니다! 우리는 또한 여러 가지 질문을 받기 시작했고, 우리는 이 질문에 정중하게 대답했다. **2016년 후반으로 빠르게 감기...** [LaunchPoint 파트너](https://exchange.adobe.com/apps/browse/ec?product=MRKTO) 에코시스템이 증가함에 따라 트윗 활동의 양이 증가했습니다. @MarketoDev에게 올라온 질문 물량에 대한 답변은 소규모 팀에게 큰 일이 되었습니다. 일반적인 제품 및 판매 관련 질문이 증가하여 @Marketo 또는 @MarketoCares으로 리디렉션되었습니다. 우리는 또한 140자가 단순히 개발 관련 질문에 충분하지 않다는 것을 발견했다. 이에 대한 대답은 종종 확장되지 않은 접근 방식인, 지루하고 연관된 대화의 스레드로 이어졌습니다. 그리고 마지막으로 개발자 사이트 방문자에 대한 트래픽 소스를 분석한 결과 대부분이 유기 검색에서 나왔고 블로그의 &quot;지금 구독&quot; 기능을 발견했습니다. 이러한 이유로, 우리는 그 플러그를 뽑기로 @MarketoDev. **여기에서 나가...** Twitter 팬이라면 걱정하지 마세요! 당사의 기업 Twitter 핸들 @Marketo은 계속 작동하며 고객 지원 팀이 @MarketoCares을 처리합니다.

_David_&#x200B;이(가) _2016-12-02_&#x200B;에 게시함

## Excel 통합 2부: Power Pivot 및 Power View를 사용하여 고급 Marketo 보고서 및 데이터 시각화 구축-

이는 Microsoft Excel에 내장된 Power BI 기술을 활용하여 Marketo과 함께 진정한 셀프 서비스 비즈니스 분석 경험을 만드는 방법을 설명하는 일련의 두 번째 문서입니다. 이 문서에서 다루는 개념으로 다음을 수행할 수 있습니다.

* Marketo에서 Excel로 데이터 가져오기
* 다른 소스(SaaS 애플리케이션, 데이터베이스, 플랫 파일 등)에서 데이터 가져오기 및 결합
* 비즈니스 요구 및 분석 목적을 위한 모양 데이터
* Excel 내에서 필요할 때 데이터 새로 고침
* 공식을 사용하여 계산된 열 및 측정값 만들기
* 이기종 데이터 간의 관계 생성
* 피벗 테이블 및 피벗 차트를 사용하여 데이터 분석 및 고급 보고서 작성
* 놀라운 데이터 시각화 제작

### Excel용 Power Pivot 및 Power View

이 문서에서는 다음을 구축하는 방법의 예를 제공합니다.

* Power Pivot을 사용하여 다양한 Marketo 데이터 컬렉션 간의 관계를 활용하는 고급 Marketo 보고서
* Power View를 사용하여 멋진 정적 및 애니메이션 시각화

**Power Pivot**&#x200B;은(는) Excel 2016에 이미 포함된 Excel 추가 기능으로, 강력한 데이터 분석을 수행하고 정교한 데이터 모델을 만드는 데 사용할 수 있습니다. Power Pivot을 사용하면 다양한 소스에서 대량의 데이터를 병합하고, 정보 분석을 신속하게 수행하고, 통찰력을 쉽게 공유할 수 있습니다. Power Query를 사용하여 다른 데이터 소스에서 추출한 데이터는 데이터 모델, Excel 스프레드시트 또는 두 데이터 모두로 보낼 수 있습니다. 첫 번째 문서에서는 Marketo에서 데이터를 가져와서 형태를 잡고 데이터 모델로 보내 스프레드시트에서 사용하기 전에 보다 정교한 분석을 수행했습니다. **Power View**&#x200B;은(는) Excel 시각화 레이어의 대안입니다. 직관적인 애드혹 보고 및 대시보드를 권장하는 대화형 데이터 탐색, 시각화 및 프레젠테이션 경험입니다.

이 문서에 설명된 모든 단계는 Excel 2016 for Windows에서 테스트되었습니다. 개념은 Excel 2013 또는 Excel 2010(Power View 없음)에 대해 동일해야 하지만 일부 수정이 필요할 수 있습니다. Power Pivot 및 Power View는 현재 Excel 2016의 Microsoft Windows 버전에서만 사용할 수 있으며 Excel 2016의 Office 365 버전은 Power Pivot 및 Power View를 완전히 지원하지 않습니다.

### Marketo 전원 통합 문서

#### 통합 문서 다운로드

첫 번째 문서에서는 Power Query 기술을 사용한 데이터 가져오기 및 셰이핑 프로세스에 대해 설명했습니다. Marketo에서 리드 및 활동을 추출하기 위해 몇 가지 고급 파워 쿼리를 구현하는 방법에 대해 알아보았습니다. 코딩하지 않고 보고서와 시각화를 작성하는 지점으로 직접 이동하려는 사람도 있을 것입니다. 이 통합 문서에는 첫 번째 문서에 자세히 설명된 모든 쿼리와 몇 가지 추가 쿼리가 포함되어 있습니다. 오류 처리를 개선하고 구성 워크시트에 몇 가지 추가 매개 변수를 추가했습니다. 첫 번째 문서를 검토했다면 Marketo 전원 통합 문서를 다운로드하고 추가된 항목을 확인하는 것이 좋습니다.

면책조항: Marketo 전원 통합 문서는 공식 Marketo 제품이 아니므로 Marketo에서 지원하지 않습니다. 개인 비즈니스 요구 사항에 맞게 자유롭게 사용하고 확장할 수 있지만, 위험을 감수하고 사용하십시오.

#### 통합 문서 구성

Marketo 구성 워크시트에서 필요한 모든 정보를 입력합니다.

* **Marketo REST API 인증:** 필요
* **범위 지정:** 페이징 토큰 SinceDatetime과 분석할 모든 리드가 포함된 Marketo 정적 목록의 ID를 설정합니다.
* **리드:** 보고서를 가져오려면 적어도 `id`, `firstName`, `lastName`, `email`, 만들기`edAt`, `updatedAt`, `title`, `company`, `industry`, `inferredCountry`, `inferredCity` 리드 필드를 지정해야 합니다.
   * 사용자 정의 필드 중 하나에서 도시 정보가 더 정확하면 대신 자체 필드를 사용할 수 있습니다
* Marketo 데이터베이스에서 가져올 **활동:** 활동 유형이 각 활동 집합에 대해 여기에 지정되어 있으므로 변경할 필요가 없습니다.
   * 나중에 이 정보를 조정하려는 경우 Excel 통합 문서의 오른쪽에 기존의 모든 활동 유형이 나열되는 통합 문서에 유틸리티 쿼리를 제공했습니다

보안 관련 팝업이 표시될 수 있습니다. 외부 연결을 신뢰하고 &#39;공개&#39;로 설정하십시오. 아래 팝업이 표시되는 경우 &#39;익명&#39; 웹 액세스 콘텐츠를 사용하십시오. Marketo에 대한 인증은 사용자 지정 쿼리로 직접 관리되므로 다른 종류의 액세스를 활성화할 필요가 없습니다.

#### Marketo 데이터 다운로드

먼저 Marketo 구성 워크시트의 범위 영역에서 정의하는 매개 변수로 인해 너무 많은 데이터가 다운로드되어 Marketo API 일일 요청 제한을 초과하지 않도록 하십시오. 준비가 되면 &#39;데이터&#39; 메뉴에서 &#39;모두 새로 고침&#39; 버튼을 클릭하고 모든 데이터가 통합 문서로 다운로드될 때까지 기다립니다. 데이터를 다운로드할 때 &#39;column1 not found&#39;와 유사하게 서식 지정 오류 메시지가 표시되는 경우 하나 이상의 쿼리가 데이터를 가져오지 못하므로 서식 지정도 실패합니다. 나중에 다시 시도하세요. 오류가 계속되면 Excel 버전을 확인하세요(Office 365에서 Excel 2016을 사용하지 않음). Marketo 플랫폼의 지연 시간을 존중하는 것도 중요합니다. 정적 목록 또는 잠재 고객 데이터를 변경하는 경우 파워 쿼리를 실행하기 전에 기다리는 것이 좋습니다.

### Power Pivot에서 데이터 모델링

상단 메뉴 모음에 있는 Power Pivot 메뉴에서 &#39;관리&#39; 단추를 클릭하여 Power Pivot을 엽니다(사용할 수 없는 경우 Excel 버전을 선택하면 일부 Excel 버전에서 추가 기능으로 Power Pivot을 설치할 수 있음). Marketo에서 다운로드하여 데이터 모델로 전송되는 모든 데이터는 Power Pivot 창 하단에 있는 다른 탭에서 액세스할 수 있습니다.

### 데이터 분석 표현식(DAX)

일부 보고서에 대한 데이터를 보강하거나 다시 포맷해야 합니다. Power Pivot 데이터 분석 표현식(DAX)을 사용하여 계산된 열 및 측정값(계산된 필드라고도 함)으로 일부 사용자 지정 계산을 정의해 보겠습니다. DAX에 대한 자세한 내용은 참조 섹션의 &#39;Power Pivot에서 DAX&#39; 링크를 참조하십시오. [계산 영역]이 [파워 피벗] 창에 표시되는지 확인합니다. 표시되지 않으면 [파워 피벗] 홈 메뉴에서 사용하도록 설정합니다.  **MktoLeads** 탭을 선택하고 **리드 수** 측정값을 리드 계산 영역 **리드 수:=**&#x200B;**DISTINCTCOUNT**&#x200B;**([id])**&#x200B;의 어디에나 추가하십시오. 이 측정은 ID를 기반으로 목록에서 사용할 수 있는 개별 리드를 카운트하는 것입니다. 또한 보고서 컨텍스트에서 적용된 최종 필터도 고려합니다. 보고서에서 리드 수를 합할 수 있으므로 이 조치는 실제로 필요하지 않지만 &#39;MktoLeads의 합계&#39;보다 더 나은 이름의 리드 수를 갖도록 했습니다. 또한 특정 유형의 데이터 입력(예: 50보다 높은 점수, 평균 점수 등을 가진 모든 리드)에 대해 평균, 최소, 최대값을 수행하는 보다 복잡한 측정을 쉽게 상상할 수 있도록 해주는 간단한 예입니다. ...)  이제 **MktoWebActivities** 탭을 선택하고 3개의 계산된 열을 만들겠습니다. 표의 맨 오른쪽 끝으로 스크롤하고 &#39;열 추가&#39; 열을 클릭하여 다음 계산된 열을 삽입합니다. **활동:** MktoActivityTypes 테이블에서 활동 ID를 조회하여 사용자에게 친숙한 활동 레이블을 얻습니다. **\=**&#x200B;**LOOKUPVALUE**&#x200B;**(MktoActivityTypes[name],MktoActivityTypes[id],[activityTypeId])** **Year-Month:** 일부 보고서에 더 적합한 &#39;YYYYmm&#39; 패턴으로 활동 날짜를 다시 포맷합니다. **\=**&#x200B;**LEFT**&#x200B;**([activityDate],4)&amp;**&#x200B;**MID**&#x200B;**([activityDate],6,2)** **날짜:** 활동 날짜는 원래 쿼리의 문자열이므로 적절한 날짜로 변환하십시오. **\=**&#x200B;**DATE**&#x200B;**(**&#x200B;**LEFT**&#x200B;**([activityDate],4),**&#x200B;**MID**&#x200B;**([activityDate],6,2),**&#x200B;**MID**&#x200B;**([activityDate],9,2))** 이제 **MktoEmailActivities** 탭에 대해 동일한 세 개의 측정값을 만들고 두 개의 추가 측정값을 추가해 보겠습니다. **캠페인:** MktoCampaigns 테이블에서 캠페인 ID를 조회하여 사용자에게 친숙한 캠페인 이름을 얻으십시오. **\=**&#x200B;**LOOKUPVALUE**&#x200B;**(MktoCampaigns[name],MktoCampaigns[id],[campaignId])** **프로그램:** MktoCampaigns 테이블에서 캠페인 ID를 조회하여 사용자에게 친숙한 프로그램 이름을 얻습니다. MktoPrograms 표에서는 폴더, 작업 영역 등과 같은 프로그램에 대한 자세한 내용을 제공할 수 있습니다. **\=**&#x200B;**LOOKUPVALUE**&#x200B;**(MktoCampaigns[programName],MktoCampaigns[id],[campaignId])**

### 엔티티 관계

이전에 모델 내의 다른 테이블에서 정보를 조회하여 누락된 정보를 완료하는 방법을 보았습니다. Power Pivot은 데이터 모델의 일부 테이블 간의 관계를 정의하는 더 강력한 옵션을 제공하므로 보고서에서 이러한 관계를 직접 활용할 수 있습니다. 보고서의 주요 관계를 정의하겠습니다. 파워 피벗 창에서 다이어그램 보기를 선택합니다. 데이터 모델 다이어그램 내에서 다음 관계를 추적합니다.

* **MktoInterestMomentActivities:leadId →** **MktoLeads:id**
* **MktoScoringActivities:leadId →** **MktoLeads:id**
* **MktoRevenueStageActivities:leadId →** **MktoLeads:id**
* **MktoWebActivities:leadId →** **MktoLeads:id**
* **MktoEmailActivities:leadId →** **MktoLeads: id**

이러한 모든 관계 및 개체는 보고서에 사용되지 않고, 잠재 고객, 웹 활동 및 이메일 활동만 사용됩니다. 이제 몇 가지 보고서를 작성할 때입니다.

### 전자 메일 성능 피벗 차트

이 첫 번째 보고서는 표준 Excel 피벗 차트를 기반으로 이메일 성과 KPI를 보여 줍니다. 이를 통해 업계 및/또는 캠페인별로 데이터를 필터링할 수 있습니다. [피벗 테이블] 선택기에서 [피벗 차트]를 선택하여 [파워 피벗] 메뉴에서 [피벗 차트]를 바로 만들 수 있습니다.  다른 방법은 Excel 스프레드시트에서 직접 피벗 차트를 만들어 &#39;이 통합 문서의 데이터 모델 사용&#39; 옵션을 표시하는 것입니다.  아래 그림과 같이 **MktoEmailActivities** 및 **MktoLeads** 테이블에서 필드를 끌어다 놓습니다. **MktoEmailActivities.Activity →** **Legend** (이 항목은 **MktoEmailActivities**&#x200B;에 구현한 DAX 계산 열을 사용) **MktoEmailActivities.Date →** **Axis** (이 항목은 **MktoEmailActivities**&#x200B;에 구현한 DAX 계산 열을 사용) **MktoEmailActivities.Id→7&rbrace;**∑ 값&#x200B;**&#x200B;** MktoEmailActivities.Campaign →**&#x200B;**&#x200B;필터&#x200B;**&#x200B;** MktoLeads.industry →**&#x200B;**&#x200B;필터&#x200B;**&#x200B;**

드롭된 각 필드에서 &#39;값 필드 설정&#39;을 선택하여 사용자 지정 이름을 만들 수 있습니다. 이 경우 이메일 활동 id 필드를 &#39;∑ 값&#39; 섹션에 삭제하고 사용자 정의 이름을 &#39;활동 수&#39;로 편집했습니다. 이제 피벗 차트를 구성하겠습니다. 차트를 마우스 오른쪽 버튼으로 클릭하고 상황별 메뉴에서 &#39;차트 유형 변경&#39; 옵션을 선택합니다. 모든 데이터 시리즈에 대해 서로 다른 차트 유형을 선택한 방법은 다음과 같습니다.

### Power View가 있는 잠재 고객 맵

두 번째 보고서는 World Map 및 업종별로 Lead 및 Contact 를 표시합니다. 이 보고서에 Power View가 필요합니다. Excel에서 메뉴를 켜려면 아래 참조 링크를 따르십시오. 또는 Excel 검색 상자에 &#39;power view&#39;를 입력하면 됩니다. &quot;Power View 보고서 삽입&quot;을 선택합니다.  빈 Power View 보고서에서 오른쪽 패널의 **MktoLeads** 테이블을 선택하고 잠재 고객 위치 필드(예: **inferredCity**)를 끌어서 놓습니다. 이제 메인 메뉴에 &#39;디자인&#39; 메뉴가 나타납니다.

Power View &#39;Design&#39; 메뉴에서 &#39;Map&#39;을 선택하여 맵 시각화로 전환합니다. 아래 그림과 같이 **MktoLeads** 테이블에서 필드를 드래그 앤 드롭하십시오. **MktoLeads.industry →** **Color** **MktoLeads.inferredCity →** **Locations** **MktoLeads.Leads 수 →** **∑ 크기**(이 방법은 **MktoLeads**&#x200B;에 구현된 DAX 측정값을 사용). 리드 맵이 준비되었습니다! 맵의 크기를 조정하고 제목 및 범례를 사용자 정의하기만 하면 됩니다. Power View를 사용하면 하나의 스프레드시트에 여러 그래프가 있는 고급 대시보드를 작성할 수 있습니다. Power View를 사용하여 더 많은 대시보드 구성 요소를 진행하는 방법을 보려면 &#39;[놀라운 Power View 보고서 만들기](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)&#39; 아래의 참조된 자습서를 확인하십시오.

### 3D 맵에서 애니메이션화된 웹 활동

이 세 번째 보고서는 3D 세계 지도에 업종별로 잠재 고객 웹 활동을 표시합니다. 이 보고서를 위해 3D 맵이 필요합니다. 엑셀 검색창에 &#39;3D&#39;를 입력하고 &#39;3D 맵&#39;을 선택하면 됩니다. 팝업 창에서 새 투어를 만듭니다.  오른쪽 패널에서 버블 차트를 선택합니다. 아래 그림과 같이 **MktoLeads** 및 **MktoWebActivities** 테이블에서 필드를 드래그 앤 드롭하십시오. **MktoLeads.industry →** **Category** **MktoLeads.inferredCity →** **Location** **MktoWebActivities.Activity →** **Time**(이 작업은 **MktoWebActivities**&#x200B;에서 구현한 DAX 계산 열을 사용합니다. ID 필드는 활동 계산에 사용할 수도 있습니다.) **MktoWebActivities.Date →** **Time**(이 항목은 **MktoWebActivities**&#x200B;에 구현한 DAX 계산 열을 사용) **MktoWebActivities.Activity**&#x200B;을(를) 다른 유형의 웹 활동을 필터링하는 필터로 사용할 수도 있습니다.

[테마] 단추를 사용하여 3D 맵의 색상 구성표를 변경합니다. &#39;장면 옵션&#39;을 열어 애니메이션을 사용자 지정합니다.
이제 3D 세계 지도를 완성하셨으니, 전세계에 애니메이션을 적용해서 영상을 만드는 재미가 있으실 겁니다.

### 다음 단계

Excel Power BI 도구로 가능한 작업을 간단히 처리했습니다. 웹에서 다른 훌륭한 문서와 튜토리얼을 검색하여 Excel 기술을 확장하고 비즈니스 목표를 달성하는 데 필요한 보고서를 디자인하는 것이 좋습니다. 이 문서를 통해 Excel과 Marketo이 결합된 유용한 기능을 활용할 수 있기를 바랍니다.

### 참조

#### 파워 피벗

* [Power Pivot: Excel에서 강력한 데이터 분석 및 데이터 모델링](https://support.microsoft.com/en-us/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)
* Power Pivot의 [DAX(데이터 분석 식)](https://support.microsoft.com/en-us/article/Data-Analysis-Expressions-DAX-in-Power-Pivot-bab3fbe3-2385-485a-980b-5f64d3b0f730)

#### Power View

* [Excel 2016에서 Power View 켜기](https://support.microsoft.com/en-us/article/Turn-on-Power-View-in-Excel-2016-for-Windows-f8fc21a6-08fc-407a-8a91-643fa848729a)
* [자습서: 놀라운 파워 뷰 보고서 만들기](https://support.microsoft.com/en-us/article/Tutorial-Create-Amazing-Power-View-Reports-Part-1-e2842c8f-585f-4a07-bcbd-5bf8ff2243a7)

_2017-02-02_&#x200B;에 _필립_&#x200B;이 게시함

## Marketo API의 활동 레코드에 대한 중요 변경 사항

**참고: 이 게시물은 새 인프라로의 마이그레이션으로 인해 API에서 반환된 활동 레코드에 대한 변경 사항을 반영하도록 업데이트됩니다.** **마지막 업데이트: 2018년 9월 13일** 2017년 9월에 시작되는 Marketo의 차세대 Activity Service 롤아웃으로 Marketo API에서 반환되는 활동, 데이터 값 변경 또는 잠재 고객 삭제 레코드에서 정수 &quot;id&quot; 필드의 고유성 또는 존재를 적용할 수 없습니다. 활동 레코드를 검색하는 통합에 대한 서비스 중단을 방지하려면 id 필드를 선택 사항으로 처리해야 합니다. 이 변경 사항의 전환은 구독 및 향후 릴리스에 영향을 미치기 시작합니다. 이 변경 사항은 다음 종단점에 영향을 줍니다. REST API

영향을 받는 SOAP 유형은 `ActivityRecord` 및 `LeadChangeRecord`입니다.

### 예

다음 예는 영향을 받을 레코드 유형을 보여 줍니다. 두 예에서 영향을 주는 필드를 &quot;id&quot;라고 합니다.

**REST 필드 예: id**

```json
  {
      "id" : 102988,
      "leadId" : 1,
      "activityDate" : "2015-01-16T23:32:19Z",
      "activityTypeId" : 1,
      "primaryAttributeValueId" : 71,
      "primaryAttributeValue" : "localhost/munchkintest2.html",
      "attributes" : [
          {
              "name" : "Client IP Address",
              "value" : "10.0.19.252"
          },
          {
              "name" : "Query Parameters",
              "value" : ""
          },
          {
              "name" : "Referrer URL",
              "value" : ""
          },
          {
              "name" : "User Agent",
              "value" : "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36"
          },
          {
              "name" : "Webpage URL",
              "value" : "/munchkintest2.html"
          }
      ]
  }
```

**SOAP 필드 예: id**

```xml
  <activityRecord>
    <id>1030680</id>
    <activityDateTime>2013-07-09T16:44:28-05:00</activityDateTime>
    <activityType>Visit Webpage</activityType>
    <mktgAssetName>ClickDemo</mktgAssetName>
    <activityAttributes>
      <attribute>
        <attrName>Webpage ID</attrName>
        <attrType xsi:nil="true" />
        <attrValue>2547</attrValue>
      </attribute>
      <attribute>
        <attrName>Webpage URL</attrName>
        <attrType xsi:nil="true" />
        <attrValue>/ClickDemo.html</attrValue>
      </attribute>
    </activityAttributes>
    <campaign />
    <personName xsi:nil="true" />
    <mktPersonId>1089965</mktPersonId>
    <foreignSysId xsi:nil="true" />
    <orgName xsi:nil="true" />
    <foreignSysOrgId xsi:nil="true" />
  </activityRecord>
```

_케니_&#x200B;이(가) _2017-03-01_&#x200B;에 게시함

## 2017년 겨울 업데이트

2017년 겨울 릴리스에서는 사용자 지정 개체 데이터를 비동기적으로 대량 가져오고 안내식 랜딩 페이지에서 변수를 조작하는 기능을 추가하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 잠재 고객 데이터베이스 API

#### 사용자 지정 개체의 일괄 가져오기

사용자 지정 개체의 일괄 가져오기를 지원하는 새 끝점입니다. 자세한 내용은 [여기](/help/rest-api/custom-objects.md)에서 확인할 수 있습니다.

#### 예정된 활동 변경 알림

Marketo이 차세대 Activity Service를 출시할 때 발생하는 중요한 변경 사항에 유의하십시오. 이 변경 사항은 다음 끝점에 영향을 줍니다.

SOAP

[getLeadActivity](/help/soap-api/getleadactivity.md), [getLeadChanges](/help/soap-api/getleadchanges.md)

이러한 끝점에서 반환된 레코드에 포함된 정수 &quot;id&quot; 필드는 더 이상 고유하지 않습니다. 이는 활동, 데이터 값 변경 및 잠재 고객 삭제 레코드 유형에 영향을 줍니다. 이러한 레코드 유형을 검색하는 통합에 대한 서비스 중단을 방지하려면 id 필드를 선택 사항으로 처리해야 합니다.

#### 푸시 토큰 제거

SDK API를 통해 푸시 토큰을 제거하는 기능을 추가했습니다. 자세한 내용은 [iOS](/help/mobile/push-notifications.md), [Android](/help/mobile/push-notifications.md)에서 확인할 수 있습니다.

_David_&#x200B;이(가) _2017-03-01_&#x200B;에 게시함

## 2017년 봄 업데이트

2017년 봄 릴리스에서는 리드 및 활동 개체 데이터를 비동기적으로 대량 추출하고 명명된 계정 목록을 조작하는 기능을 추가하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 잠재 고객 벌크 추출

잠재 고객 대량 추출을 지원하는 새 엔드포인트입니다. 다양한 옵션을 사용하여 레코드 선택 기준을 지정합니다. 자세한 내용은 [여기](/help/rest-api/bulk-lead-extract.md)에서 확인할 수 있습니다.

### 일괄 활동 추출

활동의 대량 추출을 지원하는 새 엔드포인트입니다. 날짜 범위 및 활동 목록을 사용하여 레코드 선택 기준을 지정합니다. 자세한 내용은 [여기](/help/rest-api/bulk-extract.md)에서 확인할 수 있습니다.

### 명명된 계정 목록

명명된 계정 목록에서 CRUD 작업을 지원하는 새 끝점입니다. 자세한 내용은 [여기](/help/rest-api/named-account-lists.md)에서 확인할 수 있습니다.

### 기타 개선 사항

* 이제 [캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignByIdUsingGET) 끝점을 사용하여 &quot;트리거 가능한&quot; 캠페인을 필터링할 수 있습니다. 이 작업은 &quot;isTriggerable=true&quot;를 쿼리 매개 변수로 전달하여 수행됩니다.
* [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) 끝점은 이제 SMS 메시지를 제외한 모든 자산 유형을 포함하는 프로그램을 지원합니다.

### 이온-

이제 Marketo Mobile MME와 [Ionic](https://ionicframework.com/) 응용 프로그램 프레임워크를 함께 사용할 수 있습니다. 자세한 내용은 [여기](/help/mobile/ionic.md)에서 확인할 수 있습니다.

### 푸시 알림 토큰 등록 취소

Marketo에 푸시 알림 토큰을 등록 취소할 수 있는 새로운 방법이 SDK에 추가되었습니다. 사용자가 앱에서 로그아웃하는 등의 경우에 유용합니다. 사용법은 `unregisterPushDeviceToken`(iOS) 또는 `uninitializeMarketoPush`(Android) 메서드 [여기](/help/mobile/push-notifications.md)를 참조하십시오.

_David_&#x200B;이(가) _2017-06-16_&#x200B;에 게시함

## IFTTT 및 Zapier를 사용하는 마케터용 사물 인터넷

사물 인터넷(IoT)은 연결된 장치, 가전 기기, 웨어러블, 차량 등의 인터네트워킹이다. 임베디드 전자 제품, 소프트웨어, 센서 및 네트워크 연결 기능을 통해 이러한 오브젝트는 클라우드 정보 시스템과 데이터를 수집하고 교환할 수 있습니다. 이러한 기술은 빠르게 성장하고 있으며 추세에 있어 우리의 생활 방식, 업무 방식 및 비즈니스를 신속하게 수행하는 방식에 영향을 미칠 것입니다. Marketo의 선도적인 Marketing Engagement Platform은 모든 형태의 커뮤니케이션 채널을 확장하고 상호 작용할 수 있는 기능을 갖춘 IoT에 대비합니다. Marketo은 이메일, 웹, 모바일, CRM 등과 관련된 70개 이상의 활동을 추적할 수 있으며, 모든 서드파티 시스템에서 제공할 수 있는 [사용자 지정 활동](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-activities/create-a-custom-activity.html?lang=ko)도 지원합니다. Marketo [사용자 지정 개체](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/marketo-custom-objects/understanding-marketo-custom-objects.html?lang=ko)를 사용하면 비즈니스와 관련된 모든 종류의 타사 지표를 추적할 수 있으며 마케터가 Marketo 스마트 캠페인 필터 및 트리거에서 이러한 지표를 바로 활용할 수 있습니다. 소비자를 위한 IoT를 구현하려면 중앙 서버가 소비자 장치와 상호 작용해야 하며 이 서버는 REST API, 사용자 지정 개체, 사용자 지정 활동 등의 기능을 사용하여 Marketo 오픈 플랫폼과 데이터를 교환해야 합니다. - 문서화된 [여기](http://eto.com/). 블로그 게시물을 통해 시연하는 것은 쉽지 않다. 대신 IFTTT 서비스를 Marketo과 통합하여 다음과 같은 마케터를 위한 멋진 IoT 사용 사례를 구현합니다.

* 사무실에 컬러 조명을 깜박여 잠재 고객이 로드쇼에 등록될 때마다 마케팅 팀을 응원하십시오.
* 연결된 전원 플러그에 연결된 벨을 자동으로 발사하여 거래가 성사될 때마다 영업 팀을 격려합니다.
* LinkedIn, Facebook, Slack 등과 같은 소셜 네트워크에 마케팅 성공 이정표를 자동으로 게시합니다. ...
* 다음을 기반으로 마케팅 캠페인 자동 시작:
   * 기상 경보 발생 시(바람, 온도, 비 등)
   * 뉴욕 타임즈와 같은 신문에 의해 새로운 기사가 실리면, 몇 가지 특정한 기준에 맞추어진다
   * 미국 상원이나 하원이 투표할 때
   * 국제 우주 정거장이 특정 지역을 통과할 때
   * 등 ...

이러한 시나리오가 재미있지만 쓸모가 없다는 것을 알게 될 수도 있지만, 이러한 시나리오는 사람들뿐만 아니라 연결된 세계의 모든 것과도 마케팅을 수행하는 새로운 개념적 방법을 보여 주기 위해 마련되었습니다. 이 문서에서 다루는 또 다른 흥미로운 점은 Zapier와 같은 개방형 웹 통합 플랫폼을 서드파티 시스템과 Marketo 간의 &quot;서비스 해치&quot;로 활용하여 인증을 관리하는 방법입니다.

### IFTTT 서비스

IFTTT는 &quot;IF This Then That&quot;의 약어입니다. 사람들이 애플릿이라고 하는 간단한 조건문 체인을 만들기 위해 사용하는 무료 웹 기반 서비스입니다. 애플릿은 일부 파트너 웹 서비스 내에서 발생하는 변경 사항에 의해 트리거되며 그 결과 다른 파트너 웹 서비스로 작업이 전송됩니다. IFTTT는 2011년 린든 티베츠, 제시 테인, 스콧 통, 알렉산더 티베츠가 샌프란시스코에서 론칭했다. 먼저 IFTTT는 [Zapier](https://zapier.com/)과(와) 같은 서비스와 유사하게 보입니다. 예를 들어, 소비자 및 IoT 장치(원격, 알람, 조명, 온도 조절기, 자동차, 프린터, 휴대폰 등)에 훨씬 더 중점을 둡니다.  먼저 [IFTTT 웹 사이트](https://ifttt.com/explore)에서 IFTTT에 대한 계정을 만들어야 합니다. 확실히 다른 시나리오 아이디어를 제공 할 수있는 이미 사용 가능한 모든 멋진 애플릿을 자유롭게 발견 할 수 있습니다!

### 메이커 채널

IFTTT와의 파트너십을 의미하는 채널이 없는 웹 애플리케이션은 메이커 채널을 사용해야 합니다. 메이커 채널을 사용하면 웹 요청을 만들거나 수신할 수 있는 모든 장치 또는 앱에서 작동하는 애플릿을 만들 수 있습니다. 다음과 같은 통합을 제공합니다.

* 작업을 트리거하기 위해 서드파티 시스템으로부터 웹 요청을 수신하는 인바운드 트리거
* 인터넷에서 공개적으로 액세스할 수 있는 서드파티 시스템에 웹 요청을 하는 아웃바운드 작업

IFTTT에서 &quot;Maker&quot; 서비스를 검색하고 클릭합니다.  처음에 &quot;연결&quot; 버튼을 클릭하여 활성화해야 합니다.  이제 메이커 채널이 활성화됩니다. 메이커 설정 버튼을 클릭하여 비밀 키를 가져올 수 있습니다. 자세한 내용을 보려면 제공된 URL을 복사하여 브라우저에 붙여넣으십시오.

### Market에서 직접 IFTTT 조치 트리거

먼저 Marketo에서 모든 종류의 타사 웹 서비스 작업을 트리거하는 데 중점을 둡니다. 이를 위해 [Marketo Webhook](https://experienceleague.adobe.com/docs/marketo/using/product-docs/administration/additional-integrations/create-a-webhook.html?lang=ko)을(를) 사용합니다. IFTTT 모바일 앱을 통해 휴대폰 또는 태블릿에 푸시 메시지를 표시한 다음 필립스 색조 조명을 깜박이는 IoT 시나리오를 구현합니다.

### Marketo Webhook

IFTTT의 &quot;if&quot; 역할을 하는 Marketo에서 이벤트를 트리거하는 방법은 간단합니다. 이 패턴 URL에 따라 이벤트 이름과 비밀 키를 사용하여 IFTTT에 POST 웹 요청을 전송하기만 하면 됩니다.

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}>`

메이커를 사용하면 웹 요청을 통해 최대 3개의 매개 변수를 통신할 수도 있습니다. 이 작업은 쿼리 매개 변수를 사용하여 수행할 수 있습니다.

`<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={value1}&value2={value2}&value3={value3}>`

또는 최대 3개의 값으로 구성된 JSON 본문을 사용할 수 있습니다.

`{ "value1" : "{value1}", "value2" : "{value2}", "value3" : "{value3}" }`

Marketo의 관리 인터페이스에서 새 Webhook을 만듭니다.  새 Webhook에 대해 다음 정보를 제공합니다.

**Webhook 이름:** IFTTT 프로그램 성공

**설명:** 프로그램 성공을 위해 스마트 캠페인에서 IFTTT에 대한 이벤트를 트리거합니다.

**URL:** `<https://maker.ifttt.com/trigger/{event_name}/with/key/{secret_key}?value1={{program.name}}&value2={{lead.Email> Address}}&value3={{lead.Full Name}}`

event_name, 예를 들어 MarketoProgramSuccess 사용

secret_key, IFTTT Maker 서비스의 비밀 키를 사용합니다.

사용 가능한 세 가지 값에 정적 텍스트 또는 Marketo 토큰을 사용하십시오. 프로그램 수준에서 자체 토큰을 정의하여 더 많은 대화형 메시지를 푸시하고 이러한 값을 전달할 수 있습니다.

**요청 유형:** POST

**템플릿:** 비워 둠

**요청 토큰 인코딩:** 양식/Url

**응답 유형:** 없음

응답 매핑을 정의할 필요가 없습니다.

### IFTTT 애플릿

IFTTT 웹 포털의 메인 메뉴에서 &quot;내 애플릿&quot;을 선택합니다.  &quot;새 애플릿&quot; 단추를 클릭하고 **+this** 섹션을 클릭합니다.  Maker 서비스를 검색합니다.  Maker 서비스가 이벤트를 알리는 웹 요청을 받을 때마다 실행되는 트리거를 만듭니다. Marketo 웹후크의 URL에 지정된 것과 동일한 이벤트 이름(예: &quot;MarketoProgramSuccess&quot;)을 사용하고 &quot;Create trigger&quot; 단추를 클릭합니다.  이제 섹션 **+that**&#x200B;을(를) 클릭하여 작업 서비스를 지정할 차례입니다.  우리는 IoT 기기에 투자하지 않고도 누구나 테스트할 수 있는 간단한 액션 서비스인 알림 서비스를 시작할 것입니다. 알림 서비스를 검색하고 선택합니다.
디바이스에 알림을 보내는 &quot;알림 보내기&quot; 작업을 선택합니다.  아래 예와 같이 Marketo에서 보낸 3개의 값을 구성 요소로 추가하여 사용자에게 의미 있는 알림을 전달한 다음 &quot;작업 만들기&quot; 버튼을 클릭할 수 있습니다. IFTTT 애플릿을 검토하고 완료합니다. 활성화되었는지 확인합니다.

### IFTTT 애플릿 테스트

모바일에서 알림을 받으려면 먼저 장치에 대한 IFTTT 앱을 다운로드해야 합니다.  Marketo Smart Campaign 플로우에서 Webhook을 사용하여 Marketo 프로그램 성공 이벤트를 트리거할 수 있습니다. Marketo Webhooks는 트리거된 스마트 캠페인에서만 작동합니다(예: 연락처 작성 양식이 목록에 추가되면 트리거 등).  다음은 휴대 전화의 IFTTT 알림의 예입니다.

### IFTTT로 Creative 가져오기

IFTTT는 300개 이상의 파트너와 함께 애플릿 작업을 제공하므로 앱과 어플라이언스 포트폴리오와 상상력을 최대한 활용할 수 있습니다. 전자 제품 상점이나 온라인 어디에서나 구매할 수 있는 [필립스의 Hue 조명](https://www.philips-hue.com/en-us)을 예로 들어 보겠습니다. 다음 애플릿은 Marketo이 프로그램 성공을 트리거할 때 할당된 색상으로 조명 중 하나를 깜박이게 하여 사무실 마케팅 팀을 향상시킬 수 있습니다. 이전과 동일한 단계에 따라 새 애플릿을 만듭니다. 여기에서는 Marketo이 webhook으로 트리거되지만, 이번에는 Philips Hue 서비스에서 작업을 선택합니다.

&quot;조명 깜박임&quot; 작업을 선택합니다. 앱은 필립스 휴에 사용 가능한 모든 조명을 요청하므로 깜박일 조명을 선택할 수 있습니다. 먼저 Philips Hue, Hue 브리지, 그리고 적어도 한 개의 Hue 전구, 라이트 스트립, 프로젝터 또는 램프로 계정을 설정해야 합니다.  리드가 로드쇼 또는 웨비나에 등록될 때마다 색상이 있는 표시등이 깜박이는 새로운 애플릿을 방금 추가했습니다. 사무실에서 해당 설정을 사용하여 마케팅 팀이 매일 기운을 낼 수 있습니다.

### Zapie를 통해 IFTTT에서 Marketo 작업 실행

이제 IFTTT 플랫폼에서 Marketo Smart Campaign을 트리거합니다. 이를 위해 [Marketo REST API](/help/rest-api/rest-api.md)를 사용합니다. 이 API는 안전하며 아무것도 호출하기 전에 OAuth2 인증이 필요하므로 IFTTT가 메이커 채널을 사용하여 API에 대한 두 개의 연속 호출을 체인할 수 없기 때문에 Zapier와 같은 다른 플랫폼을 통해 해당 인증을 처리해야 합니다. 이미 Zapier를 도입하고 Zapier용 사용자 지정 Marketo 커넥터를 구현하는 방법을 단계별로 설명한 게시물을 게시했으므로 [Zapier](https://zapier.com/) 웹 앱 자동화 서비스를 선택했습니다. [Workato](https://www.workato.com/integrations/marketo)와 같은 다른 플랫폼도 솔루션이 될 수 있습니다.

### Marketo 캠페인

예약된 스마트 캠페인으로 Marketo 프로그램을 만듭니다. 테스트 목적으로 다음 Smart Campaign을 만들 수 있습니다. **스마트 목록** 트리거가 아닌 필터만 사용합니다. 최소한 자격이 있는지 확인하십시오. **흐름** 전자 메일 또는 다른 종류의 알림을 보냅니다. **예약** 매번 흐름을 실행하여 여러 테스트를 처리할 수 있는지 확인하십시오. URL에서 스마트 캠페인 ID를 가져올 수 있습니다. 예: _https://{{marketo_url}}/#SC4289A1_ - 스마트 캠페인 ID는 4289입니다. Marketo REST API를 통해 이 캠페인을 트리거할 수 있습니다. 예를 들어 Chrome용 [Postman](https://www.postman.com/) 플러그인을 사용하고 다음 2개의 연속 HTTPS 호출을 전송할 수 있습니다. **인증 단계:**

`https://{{Your Munchkin_Account_id}}.mktorest.com/identity/oauth/token?grant_type=client_credentials&client_id={{Your_Client_Id}}&client_secret={{Your_Client_Secret}}`

JSON 응답에서 액세스 토큰을 복구합니다. **캠페인 시작 단계:**

`https://{{Your_Munchkin_Account_id}}.mktorest.com/rest/v1/campaigns/{{Campaign_Id}}/schedule.json?access_token={{access_token}}`

### Marketo 캠페인을 시작할 Intermediate Zapier Custom Connector

Marketo REST API로 인증하고 스마트 캠페인을 시작하는 사용자 지정 Zapier 커넥터를 빌드해야 합니다.

* 사전 요구 사항
* Zapier용 Marketo 커넥터 구현
* &quot;Marketo 캠페인&quot;과 같은 다른 제목 사용
   * &quot;인증&quot; 단계 수행
   * &quot;트리거&quot; 단계 수행(Zapier 테스트 목적에 필요)
   * 아래에 설명된 대로 Marketo 캠페인 시작을 담당하는 다음과 같은 특정 &quot;작업&quot; 단계를 수행합니다.

데이터 작업 끝점 URL을 보내는 위치:

`https://{{munchkin_account_id}}.mktorest.com/rest/v1/campaigns/{{CampaignId}}/schedule.json`

다른 선택 필드는 비워 둡니다.

#### 스크립팅 API

Zapier의 스크립팅 기능을 사용하면 앱의 API와 Zapier 간에 교환되는 요청 및 응답을 조작할 수 있습니다. HTTP 요청이 전송되기 바로 전에 수정할 수 있으며 Zapier가 해당 요청을 사용하여 작업을 수행하기 전에 응답을 구문 분석할 수 있습니다. 사용자 지정 &#39;세션 인증&#39; 인증을 완료하려면 이 인증이 필요합니다. 자세한 내용은 원본 문서에서 확인할 수 있습니다. 다음 코드를 원본과 매우 유사하게 복사합니다. 작업 메서드를 변경했습니다.

```javascript
var Zap = {

 get_session_info: function(bundle) {

 console.log('Entering get_session_info method ...');

 var access_token,
 access_token_request_payload,
 access_token_response;


 // Assemble the meta data for our Access Token swap request
 console.log('building Request with client_id=' + bundle.auth_fields.client_id + ', and client_secret=' + bundle.auth_fields.client_secret);
 access_token_request_payload = {
 method: 'POST',
 url: 'https://' + bundle.auth_fields.munchkin_account_id + '.mktorest.com/identity/oauth/token',
 params: {
 'grant_type' : 'client_credentials',
 'client_id' : bundle.auth_fields.client_id,
 'client_secret' : bundle.auth_fields.client_secret
 },
 headers: {
 'Content-Type': 'application/json', // Could be anything.
 Accept: 'application/json'
 }
 };

 // Fire off the Access Token request.
 access_token_response = z.request(access_token_request_payload);

 // Extract the Access Token from returned JSON.
 access_token = JSON.parse(access_token_response.content).access_token;
 console.log('New Access_Token=' + access_token);

 // This will be mixed into bundle.auth_fields in future calls.
 //bundle.auth_fields.access_token=access_token;
 return {'access_token': access_token};
 },

 test_trigger_pre_poll: function(bundle) {

 console.log('Entering test_trigger_pre_poll method ...');

 bundle.request.params = {
 'access_token':bundle.auth_fields.access_token
 };

 return bundle.request;

 },

 test_trigger_post_poll: function(bundle) {

 console.log('Entering test_trigger_post_poll method ...');

 var data = JSON.parse(bundle.response.content);
 if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
 console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);

 throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
 }

 return JSON.parse(bundle.response.content);
 },

 launch_campaign_pre_write: function(bundle) {

 bundle.request.params = {'access_token':bundle.auth_fields.access_token};
 return bundle.request;
 },

 launch_campaign_post_write: function(bundle) {

 var data = JSON.parse(bundle.response.content);
 if ((!data.success)&&((data.errors[0].code=="601")||(data.errors[0].code=="600"))){
 console.log('Access Token expired or invalid, requesting new one - data.success=' + data.success + ', data.errors[0].code=' + data.errors[0].code);
 throw new InvalidSessionException(); // Calling get_session_info() to regenerate Access Token
 }
 return JSON.parse(bundle.response.content);
 }

};
```

##### 새 Zap

Zapier 대시보드에서 &quot;새 Zap 만들기&quot; 버튼을 클릭합니다. **트리거**

* Webhooks by Zapier 트리거 앱 선택
* &quot;Catch Hook&quot; 확인
* 하위 키를 선택할 필요 없음
* Zapier가 요청을 보낼 사용자 지정 웹후크 URL을 생성했습니다.
* 아래의 &quot;Zapier Webhook를 호출하는 IFTTT 애플릿&quot; 시나리오를 시작하여 웹후크 URL을 테스트합니다. 이를 통해 Zapier가 Webhook 페이로드에 대해 학습하고 캠페인 ID를 작업에 할당할 수 있습니다

**작업**

* 이전에 만든 Marketo Campaign 커넥터 선택
* 사용할 수 있는 작업만 선택하십시오. **캠페인 시작**
* Marketo 계정에 연결하여 인증 매개 변수(Munchkin 계정 ID, 클라이언트 ID, 클라이언트 암호)를 채웁니다.
* 템플릿을 편집하고 트리거의 캠페인 ID를 &quot;캠페인 실행&quot; 캠페인 ID 매개 변수에 연결합니다.
* 단계를 테스트하고 Marketo 캠페인이 시작되었는지 확인합니다.

### Zapier Webhook를 호출하는 IFTTT 애플릿

우리는 테스트하기 쉬운 간단한 시나리오부터 시작합니다. IFTTT에서는 매 시간마다 Marketo Campaign을 시작할 날짜 및 시간 트리거를 선택합니다. 작업은 Zapier Webhook URL에 게시하고 Smart Campaign ID를 전달하는 웹 요청입니다. Zapier Zap 및 IFTTT 애플릿이 모두 활성화되어 있는지 확인하고 모든 것이 예상대로 작동하는지 테스트합니다.

### IFTTT를 통해 Creative을 가져오겠습니다.

IFTTT는 300개 이상의 파트너와 함께 애플릿 트리거를 제공하므로, 앱 및 어플라이언스 포트폴리오와 상상력을 함께 활용해도 한계가 됩니다... 날씨 알림 시 Marketo 캠페인을 시작하는 데 사용할 [Weather Underground](https://www.wunderground.com/) 서비스를 예로 들어 보겠습니다. 다음 트리거는 Rain 조건이 발표되면 시작됩니다. 그런 다음 트리거를 메이커 웹후크 작업과 연결하되, 이전에 Zapier 웹후크 매개 변수를 채우는 것과 같습니다.  에트 볼라, 지금 비가 많이 오셔야겠는데요.

이 글에서 제공하는 개념들을 응용하여 많은 재미를 느끼길 바란다. 그러나 가장 중요한 것은 이 문서의 주요 개념 덕분에 Marketo을 다른 타사 시스템과 통합하려는 모든 사용자에게 도움이 될 것이라는 것입니다.

* MARKETO REST API
* Marketo Webhooks
* 예를 들어, Zapier와 같은 개방형 웹 통합 플랫폼을 서드파티 시스템과 Marketo 간의 &quot;서비스 해치&quot;로 활용하여 인증을 관리하는 방법

_Philippe_&#x200B;이(가) _2017-06-20_&#x200B;에 게시함

## 2017 여름 업데이트

2017년 여름 릴리스에서는 프로그램 API에 대한 몇 가지 사소한 개선 사항이 릴리스됩니다.

### 프로그램 찾아보기

선택적 earliestUpdatedAt 및 latestUpdatedAt 매개 변수의 추가를 통해 날짜 범위별로 프로그램을 가져오는 기능을 [프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/browseProgramsUsingGET) 끝점에 추가하고 있습니다. 선택한 날짜/시간으로 매개 변수 중 하나 또는 둘 다를 설정하여 두 날짜/시간 사이에 작성되거나 업데이트된 프로그램만 반환할 수 있습니다. 이 기능은 새롭고 업데이트된 마케팅 자료 세트를 검색하는 데 유용하며, 특히 번역 및 비즈니스 인텔리전스 사용 사례에 유용합니다.

_케니_&#x200B;이(가) _1970-01-01_&#x200B;에 게시함

## Google Cloud 기능을 사용하여 Marketo 비즈니스 로직 확장-

이 문서에서는 다음의 간단한 예를 기반으로 Google Cloud Platform(GCP)을 사용하여 몇 가지 비즈니스 논리 기능을 Marketo에 확장하는 솔루션을 제안합니다. Marketo 리드 레코드의 3개 사용자 정의 필드:

* **OnLinePreference**: 온라인 커뮤니케이션에 대한 잠재 고객/고객 선호도를 나타내는 증분 점수입니다.
* **OfflinePreference**: 오프라인 커뮤니케이션에 대한 잠재 고객/고객 선호도를 나타내는 증분 점수입니다.
* **환경 설정**: 오프라인 점수가 온라인 점수보다 높으면 &quot;오프라인&quot;을 표시하고 그 반대로는 &quot;온라인&quot;을 표시하는 GCP에서 계산한 필드입니다.

이 기술은 보다 고급 비즈니스 논리를 제공하고 결과적으로 외부 웹 서비스를 호출하여 결과를 Marketo으로 변환 및 통합하는 방법을 엽니다.  

### Google Cloud Platform 및 함수 기본 정보

[Google Cloud Platform](https://cloud.google.com/)&#x200B;(GCP)은 Google Search 및 YouTube과 같이, Google에서 최종 사용자 제품에 대해 내부적으로 사용하는 것과 동일한 인프라에서 실행되는 클라우드 컴퓨팅 서비스 세트입니다. 관리 도구 세트와 함께 컴퓨팅, 데이터 스토리지, 데이터 분석, 머신 러닝, 빅 데이터 등을 포함한 일련의 모듈식 클라우드 서비스를 제공합니다. 컴퓨팅 엔진, 앱 엔진 또는 Kubernetes 엔진과 같은 다양한 GCP 서비스를 필요에 따라 사용할 수 있었지만 다음과 같은 주요 이점을 위해 [클라우드 함수](https://cloud.google.com/functions)&#x200B;(Beta에 계속 있음)를 선택했습니다.

* 서버를 사용하지 않는 클라우드 컴퓨팅에서는 HTTP 호출과 같은 이벤트에 응답하여 필요할 때 논리를 스핀업할 수 있습니다.
* 서버 유지 관리 및 배포로 인한 대부분의 문제를 해결합니다.
* GCP를 각 함수 호출에 대해서만 지불하고 서버를 계속 가동시키는 데는 지불하지 않으므로 비용 효율적입니다.
* 애플리케이션 논리에만 집중하므로 빠르고 간편하게 구현할 수 있습니다.
* 매우 높은 워크로드에 대비한 자동 확장

이 기술과 가격에 대한 자세한 내용은 [GCP 웹 사이트](https://cloud.google.com/)를 확인하세요. 일반적으로 이 자습서는 중요한 비용을 유도해서는 안 되며 GCP 평가판의 무료 크레딧에 완벽하게 부합됩니다.  

### Google Cloud 환경 준비

Google Cloud 계정이 필요합니다. 이 자습서를 실행하기에 충분한 크레딧으로 GCP를 무료로 사용해 볼 수 있습니다. [GCP 웹 사이트](https://cloud.google.com/)에서 &quot;무료로 사용해 보기&quot; 버튼을 클릭하세요. Google의 [HTTP 자습서](https://cloud.google.com/functions/docs/calling)에 있는 &#39;시작하기 전에&#39; 섹션의 모든 단계를 따릅니다.

1. Cloud Platform 프로젝트 만들기: 리소스 관리 페이지로 이동
1. 프로젝트에 대한 청구 활성화: [청구 활성화](https://cloud.google.com/billing/docs/how-to/modify-project?visit_id=638816637273392093-1926929734&rd=1)
1. 클라우드 함수 API 사용: [API 사용](https://accounts.google.com/InteractiveLogin?continue=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&followup=https://console.cloud.google.com/flows/enableapi?apiid%3Dcloudfunctions%26redirect%3Dhttps://cloud.google.com/functions/docs/tutorials/http&osid=1&passive=1209600&service=cloudconsole&ifkv=ASKV5Mh81NGNsqcJqhx7hst0KFnyA0MJ-2zay8ovyluBfpvDoM820nF9Wq_SKbC1m_sjQvvRNoKSuA)
1. [Cloud SDK 설치 및 초기화](https://cloud.google.com/sdk/docs/)
1. Gcloud 구성 요소 업데이트 및 설치

   **gcloud 구성 요소 업데이트 및&amp;** **Gcloud 구성 요소 설치 베타**

1. Node.js 개발을 위한 환경 준비: [설치 안내서로 이동](https://cloud.google.com/nodejs/docs/setup)

### scoreCompare Cloud 함수 구현

1. 클라우드 기능 파일을 준비할 클라우드 저장소 버킷을 만듭니다. 명령줄을 사용하여 이 작업을 수행할 수 있습니다.

   `gsutil mb gs://[YOUR_STAGING_BUCKET_NAME]`

   또는 프로젝트를 선택하고 스토리지 메뉴를 클릭하여 Google Cloud 웹 인터페이스에서 다음을 수행합니다.
   * 저장소 버킷에 고유한 이름을 지정하십시오.
   * 기본 스토리지 클래스 선택
   * 가장 적합한 지역 위치 선택

1. 로컬 시스템에 애플리케이션 코드에 대한 디렉토리를 만듭니다.
1. 다음 JavaScript 코드를 사용하여 이 디렉터리에 &quot;index.js&quot; 파일을 만듭니다. 코드는 정말 이해하기 쉽습니다. JSON의 HTTP 요청 본문에서 두 개의 입력 매개 변수를 구문 분석하고, 처리를 수행하고, HTTP 응답을 JSON에서 인코딩합니다.

```javascript
 /\*\*
     \* HTTP scoreCompare Cloud Function.
     \*
     \* @param {Object} req Cloud Function request context.
     \* @param {Object} res Cloud Function response context.
     \*/
    exports.scoreCompare = function scoreCompare (req, res) {
     var onlineScore=parseInt(req.body.onlineScore);
     var offlineScore=parseInt(req.body.offlineScore);
     console.log('/scoreCompare: got values onlineScore =' + onlineScore + ', offlineScore =' + offlineScore);
     var result;
     if (onlineScore>offlineScore) {result = 'online';} else {result = 'offline';}
     console.log('/scoreCompare: and result is ' + result);
     res.status(200).json({output: result}).end();
    };
```

HTTP 트리거로 scoreCompare 함수를 배포합니다. 디렉토리에서 다음 명령을 실행합니다.

**gcloud beta 함수 배포 [함수] —stage-bucket [YOUR_STAGING_BUCKET_NAME] —trigger-http**

여기서 [YOUR_STAGING_BUCKET_NAME]은(는) 스테이징 클라우드 저장소 버킷의 이름입니다. 이 예제에서는

**gcloud beta 함수 deploy scoreCompare —stage-bucket mktostorage —trigger-http**

1. 콘솔 출력의 클라우드 기능 URL(httpsTrigger URL)을 확인합니다. 이러한 URL은 다음과 같습니다. `https://[YOUR_REGION]-[YOUR_PROJECT_ID].cloudfunctions.net/[FUNCTION]`

   * [YOUR_REGION]은(는) 함수가 배포되는 지역입니다. 함수 배포가 완료되면 터미널에 표시됩니다.
   * [YOUR_PROJECT_ID]은(는) 클라우드 프로젝트 ID입니다. 함수 배포가 완료되면 터미널에 표시됩니다.
   * [FUNCTION]은(는) 함수 이름입니다.

   이 예제에서는 [**https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare**](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)을(를) 사용합니다.
1. [Postman](https://www.postman.com/)과(와) 같은 도구를 사용하여 함수를 테스트합니다.
   * HTTP 동사: POST
   * URL: [https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare](https://us-central1-marketo-cloud-logic.cloudfunctions.net/scoreCompare)
   * 헤더: content-type = application/json
   * 본문: {&quot;onlineScore&quot;:110, &quot;offlineScore&quot;:200}출력에서 제공하는 내용: {&quot;output&quot;: &quot;offline&quot;}.

### Marketo의 Webhook에서 클라우드 함수 호출

Marketo의 잠재 고객 레코드에서 다음 세 개의 사용자 지정 필드를 만들어야 합니다.

* **OnlinePreference**: 정수
* **OfflinePreference**: 정수
* **환경 설정**: 문자열

&#39;scoreCompare&#39; 클라우드 함수 URL과 사용자 지정 필드의 토큰을 사용하여 Marketo 관리 인터페이스에서 다음 웹후크를 만듭니다. Marketo에서 트리거된 스마트 캠페인으로 웹후크를 테스트합니다.

* **일괄 스마트 캠페인이 아닌 트리거된 스마트 캠페인에서만 Marketo 웹후크를 호출할 수 있습니다.**
* **클라우드 기능을 사용하지 않는 경우 이를 삭제하거나 전체 프로젝트를 삭제하여 Google Cloud Platform 계정에 비용이 발생하지 않도록 하십시오.**

이 튜토리얼이 시간을 할애할 가치가 있으며, 이를 통해 복잡한 처리 및 서드파티 서비스와 관련된 보다 고급 시나리오에 대해 생각해 볼 수 있기를 바랍니다. Google의 머신 러닝 서비스인 Google Cloud AI를 활용하는 것이 좋은 예입니다. 예를 들어, Marketo 양식에서 일부 자유 텍스트를 구문 분석하고 Google 자연어 API에 텍스트의 구조와 의미를 밝힌 다음 Marketo에서 이 분석을 다시 저장하도록 요청할 수 있습니다. 아이디어를 위한 수문을 여는 것뿐입니다.

_2017-11-21_&#x200B;에 _필립_&#x200B;이 게시함

## 2017년 가을 업데이트

2017년 가을 릴리스에서는 에셋 API에 대한 몇 가지 개선 사항이 릴리스됩니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 날짜 범위별로 프로그램 찾아보기

날짜 범위별로 프로그램을 가져오는 기능을 [프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST) 끝점에 추가했습니다. 이 작업은 `earliestUpdatedAt` 및 `latestUpdatedAt` 매개 변수를 사용하여 수행됩니다. 선택한 날짜/시간으로 매개 변수 중 하나 또는 둘 다를 설정하여 두 날짜/시간 사이에 작성되거나 업데이트된 프로그램만 반환할 수 있습니다.

### 이메일 미리 보기

이제 많은 사용자가 직렬화된 HTML 버전의 이메일을 반환하는 [이메일 전체 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailFullContentUsingGET) 엔드포인트를 사용하여 이메일을 미리 봅니다. 모든 토큰, 코드 조각, 다이내믹 콘텐츠 및 포함된 구성 요소가 완전히 렌더링됩니다. 지정된 잠재 고객을 가장하기 위해 선택적 **leadId** 매개 변수를 전달할 수 있습니다.

### 이메일 2.0의 HTML 바꾸기

HTML 전자 메일 콘텐츠 블록을 바꿀 수 있도록 [전자 메일 전체 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailFullContentUsingPOST) 끝점을 추가했습니다. Marketo 이메일 2.0 편집기를 사용하여 Marketo 이메일의 HTML 코드를 편집하면 이메일과 해당 템플릿 간의 관계가 끊어집니다. 자세한 내용은 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html)를 참조하세요. 이 끝점을 사용하면 관계가 끊어진 이메일의 HTML 콘텐츠를 프로그래밍 방식으로 업데이트할 수 있습니다. 또한 관계가 끊어진 이메일과 호환되도록 다른 모든 이메일 라이프사이클 관련 엔드포인트를 수정했습니다.

* 이메일 초안 승인
* 이메일 승인 취소
* 이메일 삭제
* 이메일 초안 삭제
* 이메일 복제
* 이메일 메타데이터 업데이트

### 기타 개선 사항

* 날짜 범위 필터의 최대 시간이 31일로 늘어났습니다. [잠재 고객 추출 필터](/help/rest-api/bulk-lead-extract.md)(createdAd 또는 updatedAt) 및 [대량 활동 추출 필터](/help/rest-api/bulk-activity-extract.md)(createdAt)와 관련되어 있습니다.

_David_&#x200B;이(가) _2017-12-15_&#x200B;에 게시함

## 테스트 - 커뮤니티의 외부 비디오 링크

[이메일 전달성 파워 팩 튜토리얼 비디오](https://nation.marketo.com:443/t5/product-space-archive-videos/email-deliverability-power-pack-tutorial-video/m-p/283550)  

_David_&#x200B;에 의해 _1970-01-01_&#x200B;에 게시됨

## 2018년 겨울 업데이트

2018년 겨울 릴리스에서는 API에 대한 몇 가지 개선 사항이 릴리스됩니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 트리거 캠페인 활성화/비활성화

프로그램 템플릿 자동화 프로세스를 간소화할 수 있는 트리거 캠페인을 활성화 및 비활성화하는 기능이 추가되었습니다. 이렇게 하려면 새로 추가된 엔드포인트 두 개([스마트 캠페인 활성화](https://developer.adobe.com/marketo-apis/api/asset/#operation/activateSmartCampaignUsingPOST), [스마트 캠페인 비활성화](https://developer.adobe.com/marketo-apis/api/asset/#operation/deactivateSmartCampaignUsingPOST))를 호출해야 합니다. 자세한 내용은 [캠페인](/help/rest-api/assets.md) 설명서의 트리거 섹션을 참조하십시오.

### 이름으로 프로그램 가져오기

프로그램 비용 및 프로그램 태그를 쉽게 검색할 수 있도록 [이름별 프로그램 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getProgramByNameUsingGET) 끝점에 매개 변수 두 개를 추가했습니다. 자세한 내용은 **프로그램** 설명서의 **includeCosts** 및 [includeTags](/help/rest-api/assets.md) 매개 변수를 참조하십시오.

### 기타 개선 사항

이제 벌크 추출 API가 &quot;작업 공간 인식&quot;입니다. [사용자 지정 서비스](/help/rest-api/custom-services.md)에 대한 API 전용 사용자를 만들 때 하나 이상의 작업 영역에 대해 API 액세스 권한이 있는 사용자 역할을 선택해야 합니다. 이전에는 사용자 정의 서비스에 모든 작업 영역에 대한 액세스 권한이 부여되었습니다. 이제 사용자 지정 서비스에는 API 전용 사용자 생성 중에 선택한 작업 영역에만 액세스할 수 있습니다.

_David_&#x200B;이(가) _2018-03-02_&#x200B;에 게시함

## 2018년 봄 업데이트

2018년 봄 릴리스에서는 새로운 REST API 및 웹 추적 개인 정보 보호 개선 사항을 출시할 예정입니다. 아래의 전체 업데이트 목록을 참조하십시오.

REST API

### 정적 목록 CRUD

사용자가 정적 목록 레코드를 원격으로 만들고, 읽고, 업데이트하고, 삭제할 수 있도록 허용합니다. 멤버십 채우기 및 유지 등 REST API를 통해 정적 목록의 전체 라이프사이클을 관리할 수 있습니다. 자세한 내용은 [여기](/help/rest-api/static-lists.md)에서 확인할 수 있습니다.

### 사용자 지정 활동 메타데이터

사용자가 사용자 지정 활동 레코드를 원격으로 만들 수 있습니다. 유형 및 유형 속성 조작을 포함하여 REST API를 통해 사용자 지정 활동의 전체 라이프사이클을 관리할 수 있습니다. 자세한 내용은 [여기](/help/rest-api/activities.md)에서 확인할 수 있습니다.

### 스마트 목록 메타데이터

사용자가 스마트 목록 레코드를 원격으로 읽고, 복제하고, 삭제할 수 있도록 허용합니다. REST API를 통해 스마트 목록을 관리할 수 있습니다. 자세한 내용은 [여기](/help/rest-api/smart-lists.md)에서 확인할 수 있습니다.

### 웹 추적 개인 정보

Munchkin JavaScript 웹 추적 코드가 다음과 같은 개인 정보 보호 관련 개선 사항을 포함하도록 개선되었습니다.

* 옵트아웃 - 방문자가 웹 추적을 영구적으로 옵트아웃하도록 허용하는 기능. 자세한 내용은 [여기](/help/javascript-api/lead-tracking.md)에서 확인할 수 있습니다.
* IP 주소 익명화 - 웹 방문자의 IP 주소를 익명화할 수 있는 기능을 제공하여 로컬 및 국제 개인정보 보호 규정을 준수합니다. **anonymizeIP** 구성 매개 변수 [여기](/help/javascript-api/configuration.md)를 참조하십시오.

### 기타 개선 사항

* 이제 루트가 아닌 상위 항목과 maxDepth=1이 지정되면 [폴더 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getFolderUsingGET) 끝점이 모든 폴더를 반환합니다.
* 이제 [ID별 랜딩 페이지 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getLandingPageByIdUsingGET) 끝점이 모든 경우에 프로토콜이 있는 URL 특성을 반환합니다(http:// 또는 https://).

_David_&#x200B;이(가) _2018-06-29_&#x200B;에 게시함

## 2018년 여름 업데이트

2018년 여름 릴리스는 주로 사소한 개선 사항 및 결함 해결로 구성된 유지 관리 릴리스입니다. 아래의 전체 업데이트 목록을 참조하십시오.

### REST API

* 원래 불필요하게 생략된 이메일 처리 필드에 대한 지원이 추가되었습니다. 이제 이러한 필드를 REST를 통해 읽고 쓸 수 있습니다.
   * 차단 목록
   * 마케팅 중단
   * 이메일 중단됨
   * 상대 긴급도
* [필터 유형별 리드 가져오기](https://developer.adobe.com/marketo-apis/api/lead-database-endpoint-reference/#/Leads/getLeadsByFilterUsingGET) 끝점은 이제 filterType으로 leadPartionId를 지원합니다.

### 결함 해결

**REST 끝점**

**설명**

[프로그램 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveProgramUsingPOST)

프로그램을 만들 때 [비운영 이메일 차단]을 false로 설정한 경우 프로그램 승인이 호출되면 true로 재설정됩니다.

[일괄 추출](/help/rest-api/bulk-extract.md)

추출 출력 파일에서 특정 유니코드 문자가 손상되었습니다.

[프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

* 이메일 프로그램을 복제한 경우, SmartList 필터 로직은 초기 설정에 관계없이 결과 프로그램에서 &quot;모두&quot;로 재설정되었습니다.
* 삭제된 정적 목록이 포함된 프로그램을 복제하려고 하면 &quot;다음 자산은 지원되지 않습니다:List&quot; 오류가 표시됩니다.
* 작업 영역 간에 프로그램을 복제하려고 하면 611, &quot;프로그램을 복제할 수 없습니다.&quot; 오류가 표시됩니다.

[Id별 정적 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getStaticListByIdUsingGET)

사용자 정의 서비스에 읽기 전용 자산 역할 권한이 있는 경우 603, &quot;액세스 거부&quot; 오류가 표시됩니다.

[Marketo으로 리드 푸시](https://developer.adobe.com/marketo-apis/api/mapi/#operation/pushToMarketoUsingPOST)

**input** 배열 리드 개체에 **cookies** 특성이 지정된 경우 이전 익명 활동은 새로 만든 리드와 연결되어 있지 않습니다.

[캠페인 예약](https://developer.adobe.com/marketo-apis/api/mapi/#operation/scheduleCampaignUsingPOST)

앞으로 **runAt** 날짜를 지정한 경우 캠페인이 실행되지 않았으며 **success=true**&#x200B;이 반환되었습니다. **runAt** 날짜가 앞으로 2년 이상 지난 경우 [1042](/help/rest-api/error-codes.md) 오류가 반환됩니다.

[잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST)

`action=createDuplicate` 및 `externalCompanyId` 매개 변수를 지정하여 새 잠재 고객을 기존 회사와 연결하면 해당 잠재 고객이 지정된 회사가 아닌 빈 회사와 연결됩니다.

#### 기타

* 모든 끝점 응답에서 데이터 변경 값 mktoClientReqId이 제거되었습니다. 이것은 내부용으로만 사용되었습니다.
* 오류 조회 기능이 추가되었습니다. 검색 상자에 REST API 오류 코드를 입력하고 아래의 자동 완성 목록에서 선택하여 오류 설명으로 이동합니다.
* [끝점 참조](/help/rest-api/endpoint-reference.md) 페이지를 추가했습니다. 한 위치에 있는 모든 REST API 엔드포인트의 정렬 가능한 목록입니다. 이 페이지를 사용하여 응용 프로그램에 필요한 최소 권한 집합을 생성할 수도 있습니다. 이 기능은 사용자 정의 서비스를 만들 때 유용합니다.

_David_&#x200B;이(가) _2018-10-12_&#x200B;에 게시함

## 2018년 가을 업데이트

2019년 가을 릴리스는 주로 사소한 개선 사항 및 결함 해결로 구성된 유지 관리 릴리스입니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 향상된 기능

* [자산 API](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-cc)에 대한 [전자 메일 CC 필드](/help/rest-api/assets.md) 지원이 추가되었습니다. CC 필드 설정은 승인/복제 작업(이메일 또는 이메일 템플릿 초안 승인, 이메일 또는 프로그램 복제) 중에 예상대로 전파됩니다. 이제 모든 전자 메일 관련 끝점이 **ccFields** 속성의 CC 필드 값을 반환합니다. 예를 보려면 아래 응답에서 아래로 스크롤합니다. 이 변경 사항은 다음 끝점에 영향을 줍니다. [ID별 이메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByIdUsingGET), [이름별 이메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailByNameUsingGET), [이메일 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailUsingGET), [이메일 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST), [이메일 템플릿 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST_1), [이메일 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST), [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)

```json
{
    "success": true,
    "errors": [],
    "requestId": "cc96#166e836348b",
    "warnings": [],
    "result": [
        {
            "id": 2061,
            "name": "Test Email",
            "description": "This is a test",
            "createdAt": "2018-11-06T05:27:10Z+0000",
            "updatedAt": "2018-11-06T08:33:16Z+0000",
            "url": "<https://app-sjqe.marketo.com/#EM2061A1LA1>",
            "subject": {
                "type": "Text",
                "value": "This is a test with CC Fields"
            },
            "fromName": {
                "type": "Text",
                "value": "Tommy Tester"
            },
            "fromEmail": {
                "type": "Text",
                "value": "<tommy.tester@marketo.com>"
            },
            "replyEmail": {
                "type": "Text",
                "value": "<tommy.tester@marketo.com>"
            },
            "folder": {
                "type": "Program",
                "value": 7494,
                "folderName": "Initiative"
            },
            "operational": false,
            "textOnly": false,
            "publishToMSI": false,
            "webView": false,
            "status": "approved",
            "template": 1218,
            "workspace": "Default",
            "version": 2,
            "autoCopyToText": true,
            "ccFields": [
                {
                    "attributeId": "855",
                    "objectName": "lead",
                    "displayName": "emailcc",
                    "apiName": "emailcc"
                },
                {
                    "attributeId": "857",
                    "objectName": "lead",
                    "displayName": "leadDetails",
                    "apiName": "leadDetails"
                },
                {
                    "attributeId": "859",
                    "objectName": "company",
                    "displayName": "headquarters",
                    "apiName": "headquarters"
                }
            ]
        }
    ]
}
```

### 결함 해결

* [자산 API](https://experienceleague.adobe.com/ko/docs/marketo/using/home)에 대한 [여러 브랜딩 도메인](/help/rest-api/assets.md) 지원을 조정했습니다. 이전에는 이메일 초안 승인, 이메일 복제 또는 프로그램 복제 시 여러 브랜딩 도메인 설정이 전파되지 않았습니다. 이 문제가 해결되었습니다. 이 변경 사항은 다음 끝점에 영향을 줍니다. [이메일 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveDraftUsingPOST), [이메일 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneEmailUsingPOST), [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST)
* [apiOnly](/help/javascript-api/configuration.md) 구성 설정이 추가되었습니다. 기본적으로 Munchkin 태그가 들어 있는 웹 페이지는 웹 페이지가 브라우저에 로드될 때 &quot;웹 페이지 방문 횟수&quot; 이벤트를 실행합니다. 경우에 따라 이는 바람직하지 않습니다. 예를 들어 이 이벤트가 실행되는 시기를 완전히 제어해야 하는 단일 페이지 웹 애플리케이션입니다. 이 사용 사례를 지원하기 위해 새 **apiOnly** 구성 설정을 추가했습니다. true로 설정하면 Munchkin 태그가 페이지 로드 중 &quot;방문 웹 페이지&quot; 활동을 생성하지 않습니다.
* [domainSelectorV2](/help/javascript-api/configuration.md) 구성 설정이 추가되었습니다. 기본적으로 Munchkin 태그는 두 글자 [국가 코드 최상위 도메인](https://en.wikipedia.org/wiki/Country_code_top-level_domain)이 있는 사이트에서 호스팅되는 웹 페이지를 올바르게 처리하지 않습니다(예: .io, .co, .ly). 이로 인해 Munchkin 쿠키 도메인 속성이 잘못 설정됩니다. 더 나은 기본 환경을 제공하기 위해 새 **domainSelectorV2** 구성 설정을 추가했습니다. true로 설정하면 Munchkin 쿠키 도메인 속성을 자동으로 설정하는 개선된 알고리즘이 사용됩니다.
* [옵트아웃](/help/javascript-api/lead-tracking.md) 쿠키 도메인을 조정했습니다. 경우에 따라 Munchkin 옵트아웃 쿠키(mkto_opt_out)의 도메인 속성이 잘못 설정되었습니다. 이제 Munchkin 옵트아웃 쿠키는 Munchkin 쿠키(_mkto_trk)와 동일한 로직을 사용하여 **domainLevel** 구성 설정을 준수하는 등 도메인 쿠키 속성을 결정합니다.
* 이제 Android 애플리케이션 개발자는 이 SDK에서 Google의 [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/)&#x200B;(FCM)을 직접 사용할 수 있습니다. 자세한 내용은 [여기](/help/mobile/installation.md)에서 확인할 수 있습니다.

_David_&#x200B;이(가) _2018-12-07_&#x200B;에 게시함

## 2019년 봄 업데이트

2019년 봄 릴리스는 주로 사소한 개선 사항 및 결함 해결로 구성된 유지 관리 릴리스입니다. 아래의 전체 업데이트 목록을 참조하십시오.

_David_&#x200B;이(가) _2019-03-19_&#x200B;에 게시함

## 2019년 6월 업데이트

2019년 6월 릴리스는 주로 사소한 개선 사항 및 결함 해결로 구성된 유지 관리 릴리스입니다. 아래의 전체 업데이트 목록을 참조하십시오.

### REST API

1. 일괄 내보내기 상태 끝점에 체크섬을 추가했습니다. 체크섬을 검색된 파일의 해시와 비교하여 검색된 파일의 무결성을 확인할 수 있습니다. 체크섬은 내보낸 파일의 SHA-256 해시이며 내보내기 작업이 완료되면 fileCheckSum 속성에 저장됩니다.

다음 끝점은 체크섬을 반환합니다. [리드 내보내기 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET), [리드 내보내기 작업 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET), [활동 내보내기 작업 상태 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET), [활동 내보내기 작업 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportActivitiesUsingGET)

#### 결함 해결

1. 십진수를 정수 필드로 가져올 때 [대량 사용자 지정 개체 가져오기](/help/rest-api/bulk-custom-object-import.md)와 관련된 문제가 해결되었습니다. 수정 전에, 전체 숫자 부분을 할당하고 분수 부분을 폐기함으로써 십진수를 정수로 변환하였다(예를 들어, 5.432가 5로 변환됨). 이제 데이터 불일치가 포함된 각 행에 대해 &quot;필드 Source ID의 데이터 형식이 잘못되었습니다.&quot; 오류가 생성됩니다.
1. [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) 끝점을 사용하여 만든 전자 메일 프로그램이 특정 경우에 통신 제한 설정을 준수하지 않는 문제를 해결했습니다.
1. 611을 반환하는 [랜딩 페이지 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) 엔드포인트와 관련된 문제가 수정되었습니다. 랜딩 페이지에 이메일 구독 취소 양식이 포함된 경우 &quot;시스템 오류&quot;가 발생합니다.
1. 611을 반환하는 [랜딩 페이지 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) 엔드포인트와 관련된 문제가 수정되었습니다. [랜딩 페이지 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneLandingPageUsingPOST) 끝점을 사용하여 랜딩 페이지를 복제할 때 &quot;시스템 오류&quot;가 발생했습니다.

#### 사용 중단

1. [전자 메일 편집기 1.0 사용 중단](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666)의 일부로 1.0 전자 메일 Assets은 2019년 말에 읽기 전용이 됩니다. 모든 1.0 전자 메일 Assets은 다음과 같이 2.0으로 변환해야 합니다. 전자 메일 초안 삭제, 침대 [여기](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666). 개발자가 해당 이벤트를 준비할 수 있도록 1.0 이메일 Assets을 수정하려는 모든 이메일 관련 엔드포인트에 경고를 추가했습니다. 다음은 경고가 포함된 예제 응답입니다.

`{` `"success": true,` `"errors": [],` `"requestId": "15c57#16b338d6e75",` `"warnings": [` `"This is a v1 email asset. API support for modifying v1 emails is being dropped, and this operation will not work on v1 emails in the future. To avoid service interruptions, upgrade this and related assets by editing them in the User Interface."` `],` `"result": [` `"{\"service\":\"sendTestEmail\",\"result\":true}"` `]` `}`

다음 이메일 관련 엔드포인트는 경고를 반환합니다.

* 이메일 전체 콘텐츠 업데이트
* 이메일 콘텐츠 업데이트
* 샘플 이메일 보내기
* 이메일 승인 취소
* 프로그램 복제
* 이메일 복제
* 이메일 초안 승인
* 이메일 다이내믹 콘텐츠 섹션 업데이트
* 이메일 메타데이터 업데이트
* 프로그램 승인

이메일 스크립팅(Apache Velocity)

#### 사용 중단

1. 보안을 위해 Velocity 스크립트 기능의 하위 집합이 비활성화되었습니다. 여기에는 getClass(), $class, $context, $text 메서드와 변수가 포함됩니다. 자세한 내용은 [여기](https://nation.marketo.com:443/t5/knowledgebase/unsupported-velocity-tools-disabled-in-june-2019-release/ta-p/251177)를 참조하세요.

_David_&#x200B;이(가) _2019-06-14_&#x200B;에 게시함

## 2019년 8월 업데이트

2019년 8월에는 새로운 REST API를 출시하고, 기존 API를 개선하고, 결함을 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 향상된 기능

1. 향상된 Smart Campaign 라이프사이클 기능. 스마트 캠페인에 대해 이름별 가져오기, 만들기, 업데이트, 복제 및 삭제와 같은 작업을 수행할 수 있도록 새 엔드포인트가 추가되었습니다. 전체 정보는 [여기](/help/rest-api/smart-campaigns.md)에서 찾을 수 있습니다.
1. 쿼리 기능을 개선하기 위해 스마트 목록 엔드포인트가 개선되었습니다.
   1. [ID별 스마트 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByIdUsingGET) 끝점은 이제 **includeRules** 부울 매개 변수를 전달할 때 스마트 목록 규칙 설명(트리거 및 필터)을 반환합니다.
   1. 이제 [스마트 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListsUsingGET) 끝점을 사용하여 **earliestUpdatedAt** 및 **latestUpdatedAt** 날짜/시간 매개 변수를 전달할 때 날짜 범위별로 결과를 필터링할 수 있습니다. 또한 이제 이 엔드포인트는 캠페인 및 이메일 프로그램의 구성원인 스마트 목록을 반환합니다.
1. 스마트 목록 정의를 추출하기 위한 엔드포인트가 추가되었습니다.
   1. 스마트 캠페인 ID로 [스마트 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListBySmartCampaignIdUsingGET) 끝점은 지정된 스마트 캠페인 ID에 대한 스마트 목록 레코드를 반환합니다.
   1. [프로그램 ID별 스마트 목록 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getSmartListByProgramIdUsingGET) 끝점은 지정된 프로그램 ID에 대한 스마트 목록 레코드를 반환합니다.
1. 서식 파일(제목, 이름, 전자 메일, 회신)에서 손상된 전자 메일의 전자 메일 헤더 필드를 업데이트할 수 있도록 [전자 메일 콘텐츠 업데이트](https://developer.adobe.com/marketo-apis/api/asset/#operation/updateEmailContentUsingPOST) 끝점을 개선했습니다. 템플릿에서 분리된 항목은 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/edit-an-emails-html)에 설명되어 있습니다.

### 결함 해결

1. 승인된 랜딩 페이지에서 [랜딩 페이지 삭제](https://developer.adobe.com/marketo-apis/api/asset/#operation/deleteLandingPageByIdUsingPOST)를 호출하면 랜딩 페이지가 삭제되는 문제를 해결했습니다. 이제 &quot;709, 승인된 랜딩 페이지를 삭제할 수 없습니다&quot; 오류를 올바르게 반환합니다. [LM-127271]
1. 611을 반환하는 [샘플 이메일 보내기](https://developer.adobe.com/marketo-apis/api/asset/#operation/sendSampleEmailUsingPOST) 엔드포인트와 관련된 문제가 수정되었습니다. 템플릿에서 이메일이 손상되었을 때 &quot;시스템 오류&quot; 발생. [LM-127288]
1. 경우에 따라 &quot;709, 프로그램을 삭제할 수 없음&quot;을 발급하지 않고 사용 중인 프로그램을 삭제하는 [프로그램 삭제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) 끝점의 문제를 해결했습니다. 자산이 다른 곳에서 사용 중이거나 삭제할 수 없습니다.&quot; 오류. [LM-125431]

### 사용 중단

1. 이메일 편집기 1.0에 대한 API 지원은 2020년 1월에 더 이상 사용되지 않을 예정입니다. 그 전에 자산을 2.0으로 변환하는 것을 잊지 마십시오. 1월 이후 이메일 1.0 에셋에 쓰거나 복제하려고 하면 경고 대신 오류가 발생합니다. 전자 메일 API에 대해 자세히 알아보세요 [여기](https://nation.marketo.com:443/t5/knowledgebase/email-2-0-and-email-api-faq-s/ta-p/251423).
1. Adobe의 세계적 수준의 보안 표준에 맞게 2019년 12월 13일부터 전송 계층 보안(TLS) 1.0 및 1.1에 대한 지원을 중단합니다. 1.2 프로토콜을 준수하지 않는 Marketo과 통합된 시스템은 잠재적으로 Marketo Engage 서비스에 대한 액세스 권한을 잃을 수 있습니다. Marketo Engage 액세스를 유지하려면 2019년 12월 13일 이전에 모든 클라이언트 시스템이 TLS 1.2를 준수하는지 확인하십시오. 자세한 내용은 [여기](https://nation.marketo.com:443/t5/knowledgebase/tls-1-0-1-1-deprecation-faq/ta-p/249085)를 참조하세요.

1. 이제 모든 스마트 캠페인 관련 콘텐츠가 [스마트 캠페인](/help/rest-api/smart-campaigns.md) 메뉴 항목(REST API > Assets 아래)에 있습니다.

_David_&#x200B;이(가) _2019-08-16_&#x200B;에 게시함

## 2020년 1월 업데이트

2020년 1월에는 새로운 REST API를 출시하여 기존 API를 개선하고 결함을 해결합니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 사용자 지정 개체 스키마 정의를 프로그래밍 방식으로 만드는 기능이 추가되었습니다. 이렇게 하면 사용자 지정 개체를 한 번 정의하고 필요한 만큼 많은 인스턴스에 프로비저닝할 수 있습니다. 이를 통해 사용자는 샌드박스 및 우수성 중심 모델을 효과적으로 활용할 수 있습니다. 또한 ISV는 고객 온보딩 프로세스를 단순화할 수 있습니다. 사용자 지정 개체 메타데이터 API에 액세스하려면 적절한 구독 유형이 필요합니다.
* 프로그램 구성원을 일괄로 가져오고 내보내는 기능이 추가되었습니다. 이 새로운 엔드포인트 세트는 비동기 대량 처리 작업을 생성하기 위한 기존 Marketo REST API 패턴을 따릅니다. 프로그램 구성원 레코드에는 프로그램 구성원 사용자 정의 필드 및/또는 잠재 고객 필드가 포함될 수 있습니다.
* 프로그램 멤버 사용자 정의 필드를 양식 필드로 사용할 수 있도록 사용 가능한 양식 프로그램 멤버 필드 가져오기 엔드포인트가 추가되었습니다. Marketo Form에서 사용할 수 있는 모든 프로그램 멤버 사용자 정의 필드 목록이 반환됩니다.
* 지정된 전자 메일 템플릿에 종속된 전자 메일 에셋 목록을 반환하는 [Get Email Template Used By an](/help/rest-api/email-templates.md) 끝점이 추가되었습니다. 이를 통해 잠재적인 이메일 템플릿 변경의 영향을 빠르게 이해하고 이러한 종속성을 보다 쉽게 해결할 수 있습니다.

_David_&#x200B;이(가) _2020-01-17_&#x200B;에 게시함

## 모든 사용자 지정 개체를 검색하는 방법

Marketo의 API를 사용하여 모든 [사용자 지정 개체](https://experienceleague.adobe.com/ko/docs/marketo/using/home)&#x200B;(CO) 목록을 가져오는 방법에 대한 메시지가 자주 표시됩니다. CO에 대한 쿼리에는 이름 이상이 필요합니다. 각 CO에 대한 _선험적_ 지식도 필요합니다. API에서 직접 쿼리하는 메서드를 제공하지 않으므로 지식을 가져오는 메서드가 명확하지 않을 수 있습니다. Marketo Engage의 많은 목표와 마찬가지로 스마트 목록은 사람(잠재 고객)과 연결된 CO에 대한 답변을 제공합니다. 스마트 목록은 회사와 다르게 작동하며, 필터에 대한 오브젝트 유형에 회사가 연결된 모든 사람 목록이 표시되므로 목표에 따라 회사를 중복 제거해야 할 수도 있습니다. 새 사용자 지정 개체가 승인될 때마다 관련 필터가 만들어집니다. 이름은 &quot;**HAS CO NAME**&quot; 형식으로 지정됩니다. 아래 예에서 사용자 지정 개체 이름은 &quot;**전화 회의 트랙 구독&quot;**&#x200B;이고 해당 필터의 이름은 &quot;**전화 회의 트랙 구독 있음**&quot;입니다. 스마트 목록을 만든 후에는 [사용자 지정 개체 끝점](/help/rest-api/custom-objects.md)을 사용하여 연결된 CO를 쿼리하는 데 필요한 정보를 검색할 수 있습니다. 연결된 필드(ID 또는 이메일 주소)가 포함되도록 목록을 내보냅니다. [smartListName](/help/rest-api/bulk-lead-extract.md) 또는 **smartListId** 필터 또는 **UI에서 내보내기**&#x200B;에 의한 [잠재 고객 추출 API](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/managing-people-in-smart-lists/export-people-to-excel-from-a-list-or-smart-list) 필터링을 사용하여 내보낼 수 있습니다. 다음 단계에서는 연결된 각 필드 값을 사용하여 연결된 사용자 지정 개체를 개별적으로 쿼리합니다. 이 예제에서 사용자 지정 개체의 이름은 **&quot;Conference Track Subscription&quot;**&#x200B;이고 해당 API 이름은 **conferenceTrackSubscription_c**&#x200B;입니다. UI에서 API 이름을 &quot;**API 이름**&quot;으로, API를 통해 &quot;**이름**&quot;으로 찾습니다.  관리자 | Marketo 사용자 지정 개체[/caption] 및 [목록 사용자 지정 개체 API](https://developer.adobe.com/marketo-apis/api/mapi/#operation/listCustomObjectsUsingGET) 끝점에서 반환된 조각은 다음과 같습니다.

```json
{
    "name": "conferenceTrackSubscription_c",
    "displayName": "Conference Track Subscription",
    "description": "Track subscription for conference attendees",
    "createdAt": "2020-01-13T19:50:06Z",
    "updatedAt": "2020-01-13T19:50:06Z",
    "idField": "marketoGUID",
    "dedupeFields": [
        "subscriptionID"
    ],
    "searchableFields": [
        [
            "subscriptionID"
        ],
        [
            "marketoGUID"
        ],
        [
            "leadID"
        ]
    ],
    "relationships": [
        {
            "field": "leadID",
            "type": "child",
            "relatedTo": {
                "name": "Lead",
                "field": "Id"
            }
        }
    ]
}
```

Smart List의 Persons를 사용하여 일대다(1:1) 또는 일대다(1:N)와 연결된 사용자 지정 개체를 검색하려면 다음과 같이 요청하십시오.

`GET /rest/v1/customobjects/conferenceTrackSubscription_c.json?filterType=leadID&filterValues=1000302,1000303,1000304,1000306,1000307`

이 예제에서 이 사용자 지정 개체는 **leadID** 필드를 통해 개인에 연결되므로 필터 유형은 &quot;**leadID**&quot;입니다. 필터 값 매개 변수는 스마트 목록 내보내기에서 가져온 ID를 쉼표로 구분한 목록입니다. 요청에는 단일 요청 URI에 맞출 수 있는 최대 8K자의 필터 값이 포함될 수 있습니다. 이 길이를 초과하는 요청은 414 HTTP 수준 오류 코드를 반환합니다. 응답은 두 개 이상의 청크로 반환될 수 있습니다. 이 경우 **moreResult**&#x200B;은(는) **true**&#x200B;이(가) 되고 **nextPageToken**&#x200B;이(가) 포함됩니다. [moreResult](/help/rest-api/paging-tokens.md)이(가) **false**&#x200B;가 될 때까지 결과를 **페이지 ~**&#x200B;해야 합니다. 다음은 위의 API 요청에 대한 결과의 일부입니다.

```json
"result": [
    {
        "seq": 0,
        "marketoGUID": "d6b3ed3d-4eb8-4066-a9cd-184c8d385cfe",
        "leadID": "1000302",
        "subscriptionID": "4ad59184-6bf1-4eeb-a583-d82aeee68210",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 1,
        "marketoGUID": "e5e0aba4-f27f-494d-93ed-9cb580989bf3",
        "leadID": "1000303",
        "subscriptionID": "fc5596d5-6fa2-4848-b4a2-89d96e245c59",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 2,
        "marketoGUID": "e65007cd-86b1-4c17-8d55-057c96e1788a",
        "leadID": "1000304",
        "subscriptionID": "7e54b8a0-2170-4d81-a809-4eac349508d0",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 3,
        "marketoGUID": "39d956b2-85e2-4c24-94e7-e9fa5a09d3d0",
        "leadID": "1000306",
        "subscriptionID": "644c8e5b-fc0c-4d4a-80f8-358a65ce0a68",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    },
    {
        "seq": 4,
        "marketoGUID": "a2151350-50c8-437f-bc71-7a054bb601f0",
        "leadID": "1000307",
        "subscriptionID": "bf14218c-ae6a-42b3-a14e-f7182903cbcd",
        "createdAt": "2020-01-13T21:24:04Z",
        "updatedAt": "2020-01-13T21:24:04Z"
    }
```

이제 스마트 목록의 사용자와 직접 연결된 각 사용자 지정 개체에 대한 값을 갖게 되었으며 값을 검색하는 것 외에 **marketoGUID**&#x200B;을(를) 사용하여 이러한 개체를 [업데이트](/help/rest-api/custom-objects.md) 또는 [삭제](/help/rest-api/custom-objects.md)할 수 있습니다. 다대다 관계(N:N)의 개인과 연결된 사용자 지정 개체의 경우 위의 기법은 각 개인을 여러 개의 두 번째 수준 CO에 연결하는 중간 개체인 첫 번째 수준 개체를 반환합니다.

이러한 2차 수준 CO를 검색하려면 링크 필드 및 1차 수준 중간 개체에서 추출된 값을 필터링하여 2차 수준 CO 유형에 대한 새 쿼리 세트를 시작하십시오. 예를 들어, 위의 &quot;**전화 회의 트랙 구독&quot;** 개체에는 **subscriptionID**&#x200B;에 의해 연결될 수 있는 **&quot;Session&quot;**&#x200B;이라는 세션을 나타내는 다른 수준의 개체가 있을 수 있습니다. 위의 전화 회의 트랙 구독에 연결된 세션 검색 요청은 다음과 같습니다.

`GET /rest/v1/customobjects/session_c.json?filterType=subscriptionID&filterValues=4ad59184-6bf1-4eeb-a583-d82aeee68210,e5e0aba4-f27f-494d-93ed-9cb580989bf3,e65007cd-86b1-4c17-8d55-057c96e1788a,39d956b2-85e2-4c24-94e7-e9fa5a09d3d0,bf14218c-ae6a-42b3-a14e-f7182903cbcd`

_각주_ _1)**smartListName**&#x200B;및&#x200B;**smartListId**&#x200B;필터 형식을 일부 구독에서 사용할 수 없습니다. 구독에 사용할 수 없는 경우 잠재 고객 만들기 작업 끝점(**&quot;1035, 대상 구독에 대해 지원되지 않는 필터 유형&quot;**)을 호출할 때 오류가 표시됩니다. 고객은 Marketo 지원 팀에 문의하여 구독에서 이 기능을 활성화할 수 있습니다._

_2020-01-14_&#x200B;에 _Tony_&#x200B;에 의해 게시됨

## 모든 사람(잠재 고객)을 검색하는 방법

Marketo Engage 인스턴스에서 모든 사용자(잠재 고객)를 검색하는 데 필요한 프로세스에 대한 많은 질문을 받습니다. 우리는 많은 유용한 해답을 제공했지만 이 해답만큼 완결된 해답은 없었다. Marketo의 Bulk Extract API를 사용하여 모든 리드를 추출하는 데 필요한 몇 가지 주요 개념을 확인했습니다. 다른 모든 세부 사항은 내가 만들었던 데모 코드에서 배울 수 있습니다. 이 게시물을 읽고 데모 코드를 탐색하면 Marketo Engage 인스턴스에서 모든 리드를 검색하는 데 필요한 모든 정보를 얻을 수 있습니다.

### 개요

핵심 기술은 [대량 리드 추출 API](/help/rest-api/bulk-lead-extract.md)를 사용합니다. 필터 없이 일괄 리드 내보내기 작업을 만들 수 있을 것으로 예상되지만, 만들 수 없습니다. **API에 필터 필요**. 사용 가능한 필터는 **createdAt**, **staticListName**, **staticListId,** **updatedAt**, **smartListName** 및 **smartListId**&#x200B;입니다. 필터가 없는 스마트 목록으로 필터링하는 것도 매력적으로 보인다. 그렇게 하면 필터가 없는 스마트 목록을 동일하게 처리할 수 있을 만큼 시스템이 스마트하다는 것을 알 수 있습니다. API에는 여기에도 필터가 필요합니다. 필터가 필요하므로 사용할 신뢰할 수 있고 표준 필터는 **createdAt**&#x200B;입니다. 이 필터 유형은 날짜/시간 범위를 최대 31일까지 허용하므로 여러 작업을 실행하고 결과를 결합해야 합니다. 먼저 대상 인스턴스에서 잠재 고객에 대해 가능한 가장 오래된 생성 날짜를 찾습니다. 가능한 가장 오래된 날짜부터 31일에서 1초를 뺀 기간 동안 작업이 생성됩니다(나중에 더 자세히 설명). 각 작업을 만든 후 대기열에 넣고 작업이 완료될 때까지 기다립니다. 그런 다음 결과 파일을 다운로드하고 체크섬을 사용하여 무결성을 확인합니다. 그리고 마지막으로, ID별로 리드를 중복 제거한 다음 고유한 리드를 출력 CSV 파일에 기록합니다.

### 가장 오래된 잠재 고객 찾기

대상 인스턴스에서 잠재 고객에 대해 가능한 가장 오래된 날짜를 얻기 위해 작은 &quot;트릭&quot;을 사용합니다. 해당 작업 전용 API 엔드포인트가 없기 때문에 약간의 창의성이 필요합니다. **maxDepth = 1**&#x200B;인 모든 폴더를 쿼리하여 인스턴스의 모든 최상위 폴더 목록을 제공합니다. 그런 다음 **createdAt** 날짜를 수집하고 구문 분석하여 가장 오래된 날짜를 찾습니다. 이 방법은 인스턴스와 함께 일부 기본 최상위 폴더가 생성되고 그 이전에는 리드를 생성할 수 없기 때문에 작동합니다.

### 필수 필드 선택

추출할 필드를 결정해야 합니다. [리드 2 설명](https://developer.adobe.com/marketo-apis/api/mapi/#operation/describeUsingGET_2)을 사용하여 대상 인스턴스에 사용할 수 있는 필드를 찾습니다. 해당 요청에 대한 응답에는 &quot;fields&quot;라는 목록이 포함됩니다. 다음은 예제 응답의 일부입니다.

```json
  "fields": [
      {
          "name": "AccountSource",
          "displayName": "Account Source",
          "dataType": "string",
          "length": 40,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "acquisitionProgramId",
          "displayName": "Acquisition Program",
          "dataType": "reference",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "Active_c",
          "displayName": "Active",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "address",
          "displayName": "Address",
          "dataType": "text",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "Address_lead",
          "displayName": "Address (L)",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "annualRevenue",
          "displayName": "Annual Revenue",
          "dataType": "currency",
          "updateable": true,
          "crmManaged": false
      },
      {
          "name": "anonymousIP",
          "displayName": "Anonymous IP",
          "dataType": "string",
          "length": 255,
          "updateable": true,
          "crmManaged": false
      }, ...
```

이 끝점은 표준 및 사용자 지정 필드를 모두 포함하는 전체 목록을 반환합니다. 요청하는 필드가 많을수록 내보내기 작업을 완료하는 데 걸리는 시간이 길어지고 결과 파일의 크기가 커집니다. 일반적으로 필요한 필드만 선택해야 합니다. 아무것도 사용 가능한 모든 필드를 요청하지 않습니다. 그래서 데모하고 있습니다. 내보내기 작업을 만들 때 필요한 필드 식별자가 **name** 값입니다. 모든 필드 이름 목록에 이름 값을 추출하겠습니다. 그러면 각 내보내기 작업을 만들 때 사용 가능한 모든 필드를 요청하는 데 사용할 것입니다.

### 내보내기 작업 날짜 범위: 각각 31일

각 내보내기 작업은 최대 31일에 걸쳐 수행할 수 있습니다. 제가 사용하고 있는 데모 인스턴스는 2016년 8월에 만들어졌기 때문에 저는 오늘 40개 이상의 일자리를 만들어야 합니다. 첫 번째 생성 날짜를 31로 나눈 이후의 일 수입니다. API를 사용하면 두 개의 작업을 동시에 처리할 수 있으므로 두 개의 작업을 동시에 실행하여 추출할 수 있습니다. 대량 추출 작업은 다른 모든 통합과 공유되는 리소스이므로 친절하게 대할 것입니다. 다른 통합에 사용할 수 있는 다른 작업을 종료하고 단일 작업을 차례로 수행하는 방법을 보여 줍니다. **createdAt** 필터에 사용되는 날짜는 [ISO 8601 사양](https://www.w3.org/TR/NOTE-datetime)을 사용하여 형식이 지정됩니다. 시간대는 항상 GMT(Z+0000)이므로 단순히 &quot;Z&quot; 또는 &quot;+00:00&quot;(으)로 표시됩니다. 2016년 8월 1일은 **2016-08-01T00:00:00+00:00**&#x200B;이고 31일 후는 2016년 9월 1일 **2016-09-01T00:00:00+00:00입니다.** 시작 및 종료 시간이 모두 포괄적이므로 해당 종료 시간에서 1초를 빼려고 합니다. **2016-09-01T00:00:00+00:00**&#x200B;은(는) **2016-08-31T23:59:59+00:00**&#x200B;이(가) 됩니다. 1초를 빼면 겹치는 시간이 줄어듭니다. GMT가 기본값이므로 **Z** 또는 **+00:00**&#x200B;을(를) 해제할 수도 있습니다.

### 중복 제거

시간이 겹치는 것을 피하는 데 어려움을 겪었지만 중복 제거 기능도 구현했습니다. 시간이 변경되는 일부 경계 사례([일광 절약 시간](https://en.wikipedia.org/wiki/Daylight_saving_time))가 있어 값이 모호해지고, 그 결과 Marketo의 대량 추출 API가 예기치 않은 중복 리드를 반환할 수 있으므로 이 작업을 수행했습니다. 드물지만 날짜/시간 필터 범위를 사용하는 통합에서 고려해야 합니다. 나는 시간이 포괄적이라는 것을 분명히 하기 위해 1초를 제거했다. 각각 **2016-08-01T00** 00Z **및** 2016-09-01T00 **00Z:00:의** createdAt **및 :00:endAt** 횟수로 작업을 만드는 경우 **2016-09-01T00:00:00Z**&#x200B;에 만들어진 리드가 포함되지 않는다고 생각해서는 안 됩니다.

### 작업 만들기

첫 번째 단계는 [리드 내보내기 작업 끝점 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createExportLeadsUsingPOST)를 사용하여 작업을 만드는 것입니다. 이 데모에서는 첫 번째 내보내기 작업 만들기 요청이 다음과 같이 표시됩니다.

`POST /bulk/v1/leads/export/create.json`

```json
{ "filter": {"createdAt": {"startAt": "2016-08-01T00:00:00",
                           "endAt": "2016-09-01T00:00:00"}},
"fields":["AccountSource","acquisitionProgramId","Active_c","address","Address_lead","annualRevenue","anonymousIP","BillingAddress","billingCity","billingCountry","BillingGeocodeAccuracy","BillingLatitude","BillingLongitude","billingPostalCode","billingState","billingStreet","blackListed","blackListedCause","city","CleanStatus","CleanStatus_account","company","CompanyDunsNumber","contactCompany","cookies","country","createdAt","customfield","DandbCompanyId","DandbCompanyId_account","dateOfBirth","dddS","department","doNotCall","doNotCallReason","dS","dueDate","DunsNumber","email","EmailBouncedDate","EmailBouncedReason","emailInvalid","emailInvalidCause","emailSuspended","emailSuspendedAt","emailSuspendedCause","externalCompanyId","externalSalesPersonId","facebookDisplayName","facebookId","facebookPhotoURL","facebookProfileURL","facebookReach","facebookReferredEnrollments","facebookReferredVisits","fax","firstName","gender","GeocodeAccuracy","holll","id","industry","inferredCity","inferredCompany","inferredCountry","inferredMetropolitanArea","inferredPhoneAreaCode","inferredPostalCode","inferredStateRegion","interested","interestedIn","isAnonymous","IsEmailBounced","isLead","iSTRUE","Jigsaw","JigsawCompanyId_account","JigsawContactId_lead","Jigsaw_account","Languages_c","lastName","LastReferencedDate","LastReferencedDate_account","lastReferredEnrollment","lastReferredVisit","LastViewedDate","LastViewedDate_account","Latitude","leadPartitionId","leadPerson","leadRevenueCycleModelId","leadRevenueStageId","leadRole","leadScore","leadSource","leadStatus","linkedInDisplayName","linkedInId","linkedInPhotoURL","linkedInProfileURL","linkedInReach","linkedInReferredEnrollments","linkedInReferredVisits","links","Longitude","MailingAddress","MailingGeocodeAccuracy","MailingLatitude","MailingLongitude","mainPhone","marketingSuspended","marketingSuspendedCause","middleName","mktoAcquisitionDate","mktocomment1","mktocomments2","mktoCompanyNotes","mktoDoNotCallCause","mktoIsCustomer","mktoIsPartner","mktoName","mktoPersonNotes","mktosync","mktotest1","mobile","mobilePhone","NaicsCode","NaicsDesc","newcustom","numberOfEmployees","originalReferrer","originalSearchEngine","originalSearchPhrase","originalSourceInfo","originalSourceType","OtherAddress","OtherGeocodeAccuracy","OtherLatitude","OtherLongitude","personPrimaryLeadInterest","personTimeZone","personType","phone","PhotoUrl","PhotoUrl_account","postalCode","priority","ProductInterest_c","rating","referal","registrationSourceInfo","registrationSourceType","relativeScore","relativeUrgency","requiredNumberofCylinder","salutation","sfdcAccountId","sfdcContactId","sfdcId","sfdcLeadId","sfdcLeadOwnerId","sfdcType","ShippingAddress","ShippingGeocodeAccuracy","ShippingLatitude","ShippingLongitude","sicCode","SicDesc","site","state","surveyAnswers","syndicationId","testBooleanField","testscore","title","totalReferredEnrollments","totalReferredVisits","Tradestyle","twitterDisplayName","twitterId","twitterPhotoURL","twitterProfileURL","twitterReach","twitterReferredEnrollments","twitterReferredVisits","uNSUBSCIBE","unsubscribed","unsubscribedReason","updatedAt","urgency","url","website","YearStarted"]}
```

응답은 다음과 같습니다.

```json
{
  "requestId": "6902#16fb52118bf",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Created",
          "createdAt": "2020-01-17T20:10:43Z"
      }
  ],
  "success": true
}
```

### 작업 큐에 넣기

그 일은 이제 생겨났지만 그냥 앉아서 아무 것도 하지 않고 있다. 작업을 실행하려면 [exportId](https://developer.adobe.com/marketo-apis/api/mapi/#operation/enqueueExportLeadsUsingPOST) 값을 사용하여 **enqueue 끝점**&#x200B;을 호출하여 요청에 대한 URI를 빌드해야 합니다. 다음과 같습니다.

`POST /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/enqueue.json`

이 POST에 대한 본문이 없으며 여기서는 단순히 POST HTTP 동사를 사용하고 있습니다. 해당 요청은 다음과 같은 응답을 생성합니다.

```json
{
  "requestId": "1836a#16fb5238a48",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Queued",
          "createdAt": "2020-01-17T20:10:43Z",
          "queuedAt": "2020-01-17T20:13:23Z"
      }
  ],
  "success": true
}
```

앞에서 언급했듯이 한 번에 실행할 수 있는 작업 수에 제한이 있습니다. 한 번에 큐에 있는 작업 수(10개)에도 제한이 있습니다. 우리는 40개 이상이 필요하므로 그 제한은 우리가 모든 일자리를 한 번에 창출하지 못하게 한다. 다른 통합도 작업을 실행할 수 있으므로 모든 슬롯이 꽉 찼을 가능성을 고려해야 합니다. 큐에 대기 중인 작업이 10개 있을 때 새 작업을 큐에 넣으려고 하면 [1029](/help/rest-api/error-codes.md) 오류가 발생합니다. **1029**&#x200B;이(가) 발생하면 작업을 큐에 넣을 때까지 지수 백오프를 사용합니다. 요청 사이에 최대 4분까지 **1029** 오류 코드를 가져올 때마다 1분을 기다린 후 해당 값을 두 배로 늘립니다. 단, 그 이상은 안 됩니다. 이 기술을 [잘린 이진 지수 백오프](https://devopedia.org/binary-exponential-backoff)라고 하며 복구 가능한 오류 및 상태 검사에 가장 적합합니다.

### 작업이 완료될 때까지 대기

각 작업을 실행하는 데 시간이 걸리므로 [상태 끝점](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsStatusUsingGET)을 호출하여 진행 상황을 모니터링합니다. 요청 URI에 다음과 같이 **exportId**&#x200B;이(가) 다시 포함됩니다.

`GET /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/status.json`

작업이 완료되기 전에 다음과 같은 응답을 받게 됩니다.

```json
{
    "requestId": "153cb#16fb525435d",
    "result": [
        {
            "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
            "format": "CSV",
            "status": "Processing",
            "createdAt": "2020-01-17T20:10:43Z",
            "queuedAt": "2020-01-17T20:13:23Z",
            "startedAt": "2020-01-17T20:13:49Z"
        }
    ],
    "success": true
}
```

작업 상태가 &quot;큐에 있음&quot;인 동안 동일한 지수 백오프(1분에서 최대 4분)를 실행합니다. 상태는 실시간으로 업데이트되지 않으며, 분당 한 번 업데이트되므로 더 빠르게 폴링할 수 있는 이점이 거의 없습니다. 작업 상태가 &quot;처리 중&quot;으로 변경되면 백오프를 재설정합니다. 다음과 같은 &quot;완료됨&quot; 상태를 기다리는 중입니다.

```json
{
  "requestId": "10ad9#16fb5268f9b",
  "result": [
      {
          "exportId": "4f2b9115-c3f2-4e40-a87c-bf803bbfed99",
          "format": "CSV",
          "status": "Completed",
          "createdAt": "2020-01-17T20:10:43Z",
          "queuedAt": "2020-01-17T20:13:23Z",
          "startedAt": "2020-01-17T20:13:49Z",
          "finishedAt": "2020-01-17T20:15:28Z",
          "numberOfRecords": 59,
          "fileSize": 74436,
          "fileChecksum": "sha256:de553362e7ffad6556ae9ea749655c35010c7f0e944fc5a85782183130dca18d"
      }
  ],
  "success": true
}
```

요청에서 리드가 반환되지 않으면 **numberOfRecords** 값이 0입니다. 이 값을 확인하고 이해가 되는 경우 다음 단계를 건너뜁니다. 리드가 반환되면 **fileChecksum** 값을 추출합니다. 파일을 다운로드할 때 파일의 무결성을 확인하는 데 사용합니다.

### 리드 가져오기

**numberOfRecords**&#x200B;이(가) 0보다 큰 경우 다음과 같은 요청과 함께 [내보내기 리드 파일 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportLeadsFileUsingGET)를 사용하여 내보낸 파일을 다운로드합니다.

`GET /bulk/v1/leads/export/4f2b9115-c3f2-4e40-a87c-bf803bbfed99/file.json`

오류 없이 파일이 전송되었는지 확인: 파일의 체크섬을 계산하고 이전에 저장한 **fileChecksum**&#x200B;과(와) 비교합니다. [SHA-2](https://en.wikipedia.org/wiki/SHA-2) 및 특히 SHA256 해시 함수를 사용하여 체크섬을 계산하십시오. 계산된 체크섬이 일치하지 않으면 파일 전송에 오류가 발생하여 전송을 다시 시도하거나 수동으로 중단하고 복구할 수 있습니다.

### 데이터 집계

첫 번째 리드부터 오늘까지 31일 간격으로 사이클링을 한 후, 완벽한 세트를 즐기실 수 있습니다. 또한 각 범위에 대해 하나의 파일이 있습니다. 모든 리드와 함께 하나의 집계된 파일을 만드는 가장 간단한 방법은 첫 번째 파일을 제외한 모든 파일에 대한 헤더 행을 제거한 후 이러한 파일을 연결하는 것입니다. 그렇게 하는 경우 나중에 데이터 처리 파이프라인에서 잠재적인 중복을 예상하고 계획하는 것을 잊지 마십시오. 데모에서는 파일을 다운로드할 때 파일을 처리합니다. 출력 파일에 각 데이터 행을 추가하기 전에 행의 리드 ID가 이미 작성되었는지 확인하여 중복을 제거합니다.

[여기](https://github.com/Marketo/REST-Sample-Code/tree/master/python/LeadDatabase/Leads)에서 호스팅되는 데모 코드를 개발했습니다. 이 코드를 통해 이 프로세스의 세부 정보를 채우고 자체 개발을 위한 템플릿 역할을 할 수 있습니다. 데모 코드는 학습 도구이므로 프로덕션 시스템에 필요한 견고성에 대한 개선이 있습니다. **코드는 MIT 라이선스에 따라 AS-IS**&#x200B;로 제공되지만 사람의 감독하에 일회성으로 사용하기에 충분할 것입니다. 이제 아무것도 널 방해할 수 없어! 이 프로세스를 수행하면 Marketo의 대량 추출 API와 대상 Marketo Engage 인스턴스에 대한 모든 필드를 사용하여 모든 리드를 추출하게 됩니다. 데이터를 더 확장하려면 기술을 사용하여 각 리드의 활동을 가져옵니다.

_2020-03-05_&#x200B;에 _Tony_&#x200B;에 의해 게시됨

## 2020년 2월 업데이트

2020년 2월에는 새로운 REST API를 출시할 예정입니다. 아래의 전체 업데이트 목록을 참조하십시오.

### 공지

* 2020년 9월 이후에는 [자산 API](/help/rest-api/assets.md) 끝점이 더 이상 **_method** 쿼리 매개 변수를 허용하지 않습니다. URI 길이 제한을 무시하도록 POST 본문에 쿼리 매개 변수를 전달하는 데 사용되었습니다. 이 매개 변수를 필요로 하는 요청을 수용하기 위해 에셋 API에 대한 URI 제한이 6KiB에서 65KiB로 늘어납니다.
* ITP에 대한 우리의 입장과 관련하여 이 Marketo 커뮤니티 게시물: [브라우저 쿠키 업데이트: Marketo/Munchkin이 영향을 받는 방법](https://nation.marketo.com:443/t5/knowledgebase/browser-cookie-updates-how-marketo-munchkin-is-affected/ta-p/251524)을 참조하십시오.
* &quot;진행 중 상태 변경&quot; 활동이 변경되었습니다. 예정된 기능 &quot;프로그램 멤버 사용자 정의 필드&quot;를 지원하기 위해에 &quot;프로그램 멤버 ID&quot; 속성이 추가되었습니다.

_David_&#x200B;에 의해 _2020-02-26_&#x200B;에 게시됨

## Munchkin 리드 연결 방법 사용 중단

Munchkin JavaScript Client 버전 159의 다음 릴리스에서는 Munchkin [리드 연결 방법](/help/javascript-api/api-reference.md)의 사용을 중단할 예정입니다. 이 버전부터 메서드를 호출하면 브라우저 콘솔에서 메서드가 향후 릴리스에서 제거됨을 나타내는 경고가 표시됩니다. 메서드가 제거되면 메서드를 사용하려고 하면 오류가 발생합니다. 최근에 이 방법을 사용한 것으로 확인된 Marketo 고객은 사용 여부를 개별적으로 알려드립니다. Munchkin 159 릴리스에 대한 자세한 내용은 [이 Marketing Nation 게시물](https://nation.marketo.com:443/t5/product-documents/munchkin-javascript-version-159-amp-associate-lead-deprecation/ta-p/299687)을 참조하세요.

### FAQ

영향을 받았는지 어떻게 알 수 있습니까?

Adobe은 구독에서 이 방법을 사용한 고객을 알려주며 사용 중단 기간에 여러 번 알려줍니다.

메서드는 언제 제거됩니까?

이 방법은 2021년 10월 Marketo 릴리스와 함께 Munchkin JS v161에서 제거될 예정이며 일반 출시로 예약됩니다.

이 메서드가 제거되는 이유는 무엇입니까?

이 방법의 도입 이후 동일한 사용 사례를 이행하는 보다 효과적인 방법이 구현되고 출시되었다. 서비스의 성능과 상태를 개선하기 위해 때때로 허용 가능한 표준에 맞지 않는 기능을 제거해야 합니다.

이 방법 대신 사용해야 하는 것은 무엇입니까?

Munchkin Associate Lead 에는 Marketo의 해당 개인 레코드에 대한 브라우저 웹 추적 쿠키의 연결과 개인 데이터 제출, 이렇게 두 가지 기본 사용 사례가 있습니다. Munchkin Associate Lead 가 도입된 이후 데이터 제출 및 쿠키 연결을 수행하는 강력한 방법이 구현되었습니다.

#### 서버측 제출

브라우저 측 제출이 필요하지 않은 경우 REST API는 [개인 데이터 제출](/help/rest-api/leads.md)을 위한 다양한 방법과 쿠키를 개인 레코드와 연결하는 [특별히 빌드된 방법](/help/rest-api/leads.md)을 제공합니다.

Munchkin 버전 159는 언제 출시됩니까?

버전 159는 2020년 10월 Marketo 릴리스 이후 공식 출시되었습니다.

_케니_&#x200B;이(가) _2020-05-06_&#x200B;에 게시함

## 백그라운드에서 Marketo 양식 제출 만들기

조직에 웹 컨텐츠 및 고객 데이터를 호스팅하는 다양한 플랫폼이 있는 경우 결과 데이터를 별도의 플랫폼으로 수집할 수 있도록 양식의 병렬 제출이 필요한 것이 일반화됩니다. 이를 수행하는 방법에는 몇 가지가 있지만 가장 좋은 방법은 종종 Forms 2 API를 사용하여 숨겨진 Marketo 양식을 제출하는 것입니다. 이 작업은 새 Marketo 양식에서 작동하지만, 필드가 없는 빈 양식을 만드는 것이 좋습니다. 이렇게 하면 렌더링할 필요가 없으므로 양식이 필요한 것보다 더 이상 데이터를 로드하지 않습니다. 이제 폼에서 [포함 코드](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 가져와서 원하는 페이지의 본문에 추가하여 약간 수정하십시오. 포함 코드에는 다음과 같은 양식 요소가 포함됩니다.

`<form id="mktoForm_1068"></form>`

다음과 같이 &#39;style=&quot;display:none&quot;&#39;을(를) 요소에 추가하여 표시되지 않도록 할 수 있습니다.

`<form id="mktoForm_1068" style="display:none"></form>`

양식이 임베드되고 숨겨지면 양식을 제출하는 코드는 매우 간단합니다.

```javascript
var myForm = MktoForms2.allForms()[0];
myForm.addHiddenFields({
 //These are the values which will be submitted to Marketo
 "Email":"<test@example.com>",
 "FirstName":"John",
 "LastName":"Doe"
 });
myForm.submit();
```

이 방식으로 제출된 Forms은 잠재 고객이 양식을 작성하고 제출한 것처럼 정확하게 동작합니다. 제출 트리거는 각 구현에서 프롬프트에 대해 다른 작업을 수행하지만 기본적으로 모든 작업에서 발생할 수 있으므로 구현에 따라 달라집니다. 중요한 부분은 필드와 값을 올바르게 설정하는 것입니다. 필드의 SOAP API 이름을 사용하십시오. 이 이름은 필드 이름 내보내기에서 찾아 값을 올바르게 제출합니다.

### Munchkin Associate Lead에서 마이그레이션

배경 양식 제출은 Munchkin Associate Lead에 대해 권장되는 대체 방법 중 하나입니다. 아래 샘플 HTML 페이지는 Associate Lead에 제출된 동일한 값을 재사용하여 높은 수준에서 마이그레이션을 보여 줍니다.

```html
<html>
<head>
    <!--
      Munchkin Code
      Replace with your own instance code
    -->
    <script type="text/javascript">
        (function() {
          var didInit = false;
          function initMunchkin() {
            if(didInit === false) {
              didInit = true;
              Munchkin.init('CHANGE ME');
            }
          }
          var s = document.createElement('script');
          s.type = 'text/javascript';
          s.async = true;
          s.src = '//munchkin.marketo.net/munchkin-beta.js';
          s.onreadystatechange = function() {
            if (this.readyState == 'complete' || this.readyState == 'loaded') {
              initMunchkin();
            }
          };
          s.onload = initMunchkin;
          document.getElementsByTagName['head'](0).appendChild(s);
        })();
        </script>
</head>

<body>
  <!--
    Start Embed code.
    Pasted from Form Actions -> Embed Code except for addition of 'style="display:none"' to the form tag in order to hide it, and instance-specific codes redacted
    Replace with your own code for testing
  -->
  <script src="CHANGE ME"></script>
  <form id="CHANGE ME" style="display:none"></form>
  <script>MktoForms2.loadForm("CHANGE ME", "CHANGE ME", "CHANGE ME TO AN INTEGER ID");</script>
  <!--End Embed Code-->

  <!--Demo code-->
    <script>
        //The same map which is assembled for the Munchkin submission can be reused for the form submission
        let values = {
            "Email": "email@example.com",
            "FirstName": "Test",
            "LastName": "Record"
        }
        //whenReady lets us apply a callback to all mkto forms on the page
        //the callback function fires whenever a form is completely loaded
        //for most use cases this will just be used to capture a reference to the form for later usage
        //submission is done in line here for demonstration only
        MktoForms2.whenReady(function(form){

            //the addHiddenFields methods lets us add arbitrary fields to the form as well as their values
            form.addHiddenFields(values);

            //pass the same set of values to associateLead
            //hashString: secret + email
            Munchkin.munchkinFunction('associateLead', values, "CHANGE ME");

            //submit the form
            form.submit();


        })
    </script>
</body>

</html>
```

_케니_&#x200B;이(가) _2020-05-26_&#x200B;에 게시함

## 2020년 7월 업데이트

2020년 7월에는 새로운 REST API를 출시하고, 기존 API를 개선하고, 결함을 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 아직 초대를 수락하지 않은 사용자(즉, &quot;보류 중인&quot; 사용자)를 쿼리하고 삭제할 수 있도록 해주는 두 개의 엔드포인트가 추가되었습니다. [ID로 초대된 사용자 가져오기](/help/rest-api/user-management.md) 끝점을 사용하면 보류 중인 사용자를 쿼리할 수 있습니다. [초대된 사용자 삭제](/help/rest-api/user-management.md) 끝점을 사용하면 보류 중인 사용자를 삭제할 수 있습니다.
* [사용자 초대](/help/rest-api/user-management.md) 끝점이 **expiresAt** 매개 변수에 대해 ISO 8601 호환 날짜/시간 문자열을 수락하도록 업데이트되었습니다.
* [ID별 사용자 가져오기](/help/rest-api/user-management.md) 및 [사용자 특성 업데이트](/help/rest-api/user-management.md) 끝점이 모두 **lastLoginAt** 특성에서 마지막 사용자 로그인 시간을 반환하도록 업데이트되었습니다.
* 이미 존재하는 정적 목록을 만들려고 할 때 [정적 목록 만들기](https://developer.adobe.com/marketo-apis/api/asset/#operation/createStaticListUsingPOST) 끝점이 오류 &quot;611, 시스템 오류&quot;를 반환하는 문제를 해결했습니다. &quot;709, 같은 이름의 정적 목록이 이미 존재합니다&quot; 오류를 반환하도록 변경되었습니다. [LM-135934]
* 이미 존재하는 전자 메일을 만들려고 할 때 [전자 메일 만들기](https://developer.adobe.com/marketo-apis/api/asset/#operation/createEmailUsingPOST) 끝점이 오류 &quot;611, 시스템 오류&quot;를 반환하는 문제를 해결했습니다. &quot;709, 같은 이름의 이메일이 이미 존재합니다&quot; 오류를 반환하도록 변경되었습니다. [LM-138648]
* 랜딩 페이지 쿼리 끝점이 잘못된 **createdAt** 값을 반환하는 문제가 해결되었습니다. 끝점은 랜딩 페이지가 마지막으로 승인된 시간을 반환합니다. 이제 랜딩 페이지를 만든 시간으로 돌아갑니다. [LM-138648]
* [리드 병합](https://developer.adobe.com/marketo-apis/api/mapi/#operation/mergeLeadsUsingPOST) 끝점이 잘못된 병합 작업에 대해 오류 &quot;611, 시스템 오류&quot;를 반환하는 문제를 해결했습니다. 병합으로 인해 잠재 고객이 중복되고 **mergeinCRM**&#x200B;이(가) true로 설정된 경우 발생했습니다. &quot;712 오류를 반환하도록 변경되었습니다. 중복 레코드를 만들고 있습니다. 대신 기존 레코드를 사용하는 것이 좋습니다.&quot; [LM-137463]

_David_&#x200B;에 의해 _2020-08-01_&#x200B;에 게시됨

## 게스트 게시물 - 심층 분석: 사용자 지정 개체 대 사용자 지정 활동 대 사용자 지정 필드

**Amit Jain, Marketo Champion 2020, MarTech IT Specialist의 게스트 게시물입니다** 엔터프라이즈 수준 마케팅 자동화 플랫폼인 Marketo은 여러 소스에서 획득한 사용자/고객/잠재 고객 정보를 관리하고 더 나은 개인화, 세분화 및 보고를 위해 Marketo에서 이를 유지 관리합니다. 이러한 소스의 범위는 웹 사이트 양식에서 목록 빌드, CRM 데이터, 전자 상거래 데이터에 이르기까지 다양합니다. Marketo은 리드, 회사, 기회 및 활동 등과 같은 표준 개체를 제공합니다. 이러한 표준 오브젝트는 Marketo에서 사용할 수 있는 확장된 데이터 세트의 새로운 마케팅 요구 사항을 충족하기에 충분하지 않은 경우가 있습니다.

예를 들어 장바구니에 추가된 항목, 다른 과정에 신청한 학생, 특정 개인이 소유한 제품, 다른 구독에 대한 동의 등이 있습니다. 이 정보는 마케터가 플랫폼 간에 보다 개인화된 콘텐츠와 통합 사용자 경험을 제공하여 고객/잠재 고객의 참여를 유지하는 데 중요할 수 있습니다. 이러한 비즈니스 요구를 수용하기 위해 Marketo은 사용자 지정 필드, 사용자 지정 활동 및 사용자 지정 개체에 이 유형의 데이터를 저장하는 사용자 지정 방법을 제공합니다. 나는 사람들이 언제 어떤 옵션을 사용해야 하는지 이해하는 데 문제가 있는 것을 관찰했습니다. 이 블로그 게시물에서는 **이 세 가지가 실제로 무엇인지, 몇 가지 예제가 있는 것을 언제 사용할지 자세히 알아봅니다.**

**사용자 지정 필드**

Marketo의 &quot;리드&quot; 개체는 마스터 개체이며 다른 모든 개체는 직접 또는 간접적으로 이 개체와 연결됩니다. Marketo을 사용하면 &quot;리드&quot; 개체, &quot;회사&quot; 개체에 사용자 정의 필드를 만들 수 있으며 최근 &quot;프로그램 멤버&quot; 사용자 정의 필드에 대한 지원을 발표했습니다. 이러한 사용자 정의 필드는 특정 유형의 데이터를 저장해야 하는 요구를 충족합니다. 예를 들어 작업 기능이나 사용자의 다른 동의를 저장해야 할 수 있습니다. Marketo에는 두 가지 유형의 사용자 정의 필드가 있습니다.

1. **CRM 필드에서 동기화됨:** 자동 Marketo ↔︎ SFDC 동기화의 일부로 Marketo은 Lead, Contact, Account 및 Opportunity 개체에 대해 SFDC의 Marketo 사용자가 볼 수 있는 모든 사용자 지정 필드를 동기화합니다.
1. **Marketo 전용 필드:** Marketo에서 직접 필드를 만들 수 있습니다. 이러한 필드의 데이터는 SFDC과 동기화되지 않습니다.

**빠른 팁**

* Marketo 전용 필드가 있으며 이제 SFDC에서 데이터를 동기화하시겠습니까? [이 블로그](https://themarketingautomationblog.com/2019/12/06/field-management-merging-remapping-hiding-marketo-fields/)를 확인해 보세요.
* 사용자 지정 필드 [여기](https://themarketingautomationblog.com/2019/11/15/knowing-your-marketo-fields/)에 대해 자세히 알아보세요.
* Marketo API는 현재 사용자 정의 필드 업데이트/생성을 지원하지 않습니다.

**사용자 지정 개체**

표준 개체 외에도 Marketo에서는 고유한 사용자 지정 개체를 만들 수 있습니다. _사용자 지정 개체를 만들고 Company 또는 Lead 개체 또는 다른 사용자 지정 개체와 연결할 수 있습니다._ 사용자 지정 개체는 표준 리드 및 회사 레코드를 보완하는 사용자 지정 레코드 집합입니다. 사용자 지정 개체를 사용하면 확장 가능한 방식으로 추가 데이터를 저장하고 해당 데이터를 리드 또는 회사 레코드에 연결할 수 있습니다. 표준(링크 필드)과 사용자 지정 필드의 조합으로 사용자 지정 개체를 만들고, 이러한 필드를 채워 사용자 지정 개체 _레코드_&#x200B;을(를) 만든 다음 해당 레코드를 Lead 또는 Company 레코드에 연결할 수 있습니다. 강력하고 유연한 연결 레코드는 리드 필드 및 회사 필드에서 찾을 수 없는 정보로 세그먼트, 스마트 목록 및 캠페인을 빌드할 수 있도록 함으로써 세그먼트, 스마트 목록 및 캠페인을 강화합니다. 사용자 지정 개체에는 다음 관계 유형 중 하나가 있을 수 있습니다.

* **일대일 관계**: 각 사용자 지정 개체에 단일 Lead/Company 개체 레코드가 있습니다.
* **일대다 관계**: 각 사용자 지정 개체에는 잠재 고객/회사와 관련된 여러 사용자 지정 개체 레코드가 포함되어 있습니다.
* **다대다 관계:**. 여기서 여러 사용자 지정 개체 레코드를 여러 잠재 고객/회사 개체와 연결할 수 있습니다. 예를 들어, 여러 학생이 과정 카탈로그의 여러 강의에 등록됩니다.

**빠른 팁**

* 사용자 지정 개체 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/home)를 설정하는 방법에 대해 자세히 알아보세요.
* Marketo 사용자 지정 개체를 중간 개체로 사용할 수 있으며, 사용자 지정 개체의 사용자 지정 개체를 의미할 수도 있습니다.

### 사용자 지정 오브젝트는 무엇입니까?

사용자 정의 객체를 사용하면 회사 또는 리드와 관련이 있지만 회사 또는 리드 자체에 대한 정적 정보는 아닌 고유한 데이터를 컴파일하고 사용할 수 있습니다. 리드 필드는 개인의 리드 정보(_이메일 주소_, _우편 번호_ 등), 비즈니스 정보(_직책_, _업계_ 등) 또는 시스템 기반 정보(_Marketo ID_, SFDC ID 또는 만든 날짜 등)와 관련이 있지만 사용자 지정 개체 필드는 완전히 사용자 지정할 수 있습니다. 예를 들어 사용자 지정 개체를 사용하여 다음과 같은 정보를 저장합니다.

* 사용자의 구매 내역.
* 장바구니 정보.
* 고객이 제한된 기간, 프로모션 할인 코드 중 하나를 사용했는지 여부.
* 설문 조사 결과, 인터뷰 및 행사 참석 등으로 얻은 보완 정보.
* 체험판 인스턴스 URL, 시작 날짜, 종료 날짜, 사용자 수 등을 포함한 사용자의 체험판 정보.

### Marketo 사용자 지정 개체 제한 사항

1. 기본적으로 Marketo에서는 10개의 사용자 지정 개체를 만들 수 있습니다. 추가 구독료로 한도를 늘릴 수 있습니다.
1. 오브젝트당 기본 필드 수는 50이지만 필요한 경우 Marketo에 추가 필드를 요청할 수 있습니다. 추가 정보를 입력해 주셔서 [Michael Florin](https://www.linkedin.com/in/michaelflorin/)에게 감사합니다.
1. 모든 사용자 지정 개체에 대해 가질 수 있는 레코드 수에는 제한이 있습니다. Marketo 구독에 따라 다릅니다. 이 한도는 가입비가 추가되면 더 늘어날 수 있다.
1. API를 사용하여 사용자 지정 개체를 만든 경우 Marketo은 Marketo UI에서 CO 스키마를 편집할 수 없습니다.

**빠른 팁**

* 사용자 지정 개체에 대한 Marketo API의 CRUD(만들기, 읽기, 업데이트 및 삭제) 지원
* Velocity 스크립트를 사용하여 이메일 개인화에 이 사용자 지정 개체 데이터를 사용할 수 있습니다.
* 모든 사용자 지정 개체 관련 끝점은 [여기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getExportProgramMembersStatusUsingGET)에서 찾을 수 있습니다.

### 사용자 지정 개체 용어

**사용자 지정 개체**: 모든 사용자 지정 개체 레코드의 그룹화가 들어 있는 컨테이너입니다. 공식적으로 데이터 카드 세트 또는 사용자 지정 테이블이라고 합니다. **사용자 지정 개체 레코드**: 잠재 고객 또는 회사에 연결할 수 있는 추가 필드 정보를 포함하는 데이터 레코드입니다. 레코드는 표준 리드 또는 회사 필드와 사용자 지정 개체 레코드 필드로 구성할 수 있습니다. 공식적으로 데이터 카드 또는 데이터 테이블 행이라고 합니다. **사용자 지정 개체 레코드 필드**: 고유 정보 또는 임시 정보를 수집하기 위해 완전히 사용자 지정할 수 있는 필드입니다. 이러한 필드는 사용자 정의 객체 자체 내에 생성 및 수용됩니다. 공식적으로 데이터 카드 필드 또는 데이터베이스 테이블 필드/열이라고 합니다. **링크 필드**: 사용자 지정 개체 레코드와 연결된 잠재 고객/회사 개체 레코드 간의 관계를 정의하는 특수 형식의 사용자 지정 개체 레코드 필드입니다. 사용자 지정 개체를 만들 때 사용자 지정 개체 레코드를 올바른 부모 레코드에 연결하기 위한 링크 필드를 제공해야 합니다.

* 일대다 또는 일대일 사용자 지정 구조의 경우 사용자 지정 개체의 링크 필드를 사용하여 개인 또는 회사에 연결합니다.
* 다대다 구조의 경우 별도로 만든 중간 개체(사용자 지정 개체의 유형이기도 함)에서 연결된 두 개의 링크 필드를 사용합니다. 한 링크는 데이터베이스의 사람 또는 회사에 연결되고 다른 링크는 사용자 지정 개체에 연결됩니다. 이 경우 링크 필드는 사용자 지정 개체 자체에 있지 않습니다.

### 사용자 지정 활동

**다른 사람이 조직과 상호 작용할 수 있는 방법에는 여러 가지가 있습니다. 회사 웹 사이트를 방문하거나, 박람회 중 하나에 참석하거나, 귀하가 보낸 이메일의 링크를 클릭할 수 있습니다. 이러한 작업은** 활동이며, 수행하는 작업이 무엇이든 Marketo이 이를 캡처하므로 마케팅 및 영업팀이 개인화되고 통합된 참여를 위해 사용자의 행동을 더 잘 이해할 수 있습니다. **_사용자 지정 활동_** _Marketo 양식, 전자 메일 또는 랜딩 페이지와 관련이 없는 활동을 추적하는 데 도움이 될 수 있습니다_. 예를 들어, 웹 사이트에서 비디오를 보거나 설문을 실시한 시간을 추적하려면 사용자 지정 활동을 사용합니다. 사용자 지정 활동은 사용자 지정 개체와 다릅니다. 값이 변경될 수 있는 경우(즉, &quot;자동차 색상&quot;이 파란색에서 빨간색으로 변경됨) 사용자 지정 개체를 사용합니다. 발생한 순간을 추적하고 해당 세부 사항을 변경할 수 없는 경우(예: &quot;구매한 자동차&quot;) 사용자 지정 활동을 사용합니다. 정의할 수 있는 최대 사용자 지정 활동 수는 기본적으로 10개로 제한됩니다. 이는 가입비가 추가되면 증액될 수 있다. [Marketo 데이터 보존 정책](https://nation.marketo.com/t5/knowledgebase/tkb-p/support_solutions-documents)에 따라 사용자 지정 활동은 25개월 후에 자동으로 삭제됩니다.

**사용자 지정 활동:** Marketo 내에서 추적할 Marketo 이외의 이벤트입니다. **사용자 지정 활동 ID:** Marketo은 Marketo API를 사용하여 활동 데이터를 푸시하거나 가져오는 동안 사용할 수 있는 사용자 지정 활동에 숫자 ID를 할당합니다. **사용자 지정 활동 필드:** 활동 메타데이터를 활동 필드에 저장할 수 있습니다. 예를 들어 비디오에 대한 보기를 추적하는 경우, 필드는 페이지 URL, 비디오 제목 등일 수 있습니다. **사용자 지정 작업 기본 필드:** 스마트 목록 필터 기준으로 사용할 수 있는 사용자 지정 작업 필드입니다.

**빠른 팁**

* 사용자 지정 활동에 대한 API 끝점은 [여기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/addCustomActivityUsingPOST)에서 사용할 수 있습니다.

## 사용자 지정 개체와 사용자 지정 활동 비교

**사용자 지정 개체**

**사용자 지정 활동**

1

인스턴스당 기본적으로 최대 10개의 사용자 지정 개체.

기본적으로 최대 10개의 사용자 지정 활동.

2

사용자 지정 개체당 최대 50개의 사용자 지정 개체 필드.

각 사용자 지정 활동 유형에는 최대 20개의 보조 속성이 있을 수 있습니다.

3

최대 1MM의 사용자 정의 오브젝트 레코드. 구독에 따라 달라질 수 있습니다.

25개월 후 사용자 지정 활동은 Marketo 데이터 보존 정책에 따라 삭제됩니다.

4

스마트 목록 및 스마트 캠페인에서 필터 및 트리거로 사용할 수 있습니다.

스마트 목록 및 스마트 캠페인에서 필터 및 트리거로 사용할 수 있습니다.

5

이메일 콘텐츠를 개인화하는 데 사용할 수 있습니다.

이메일 콘텐츠를 개인화하는 데 사용할 수 없습니다.

6

사용자 지정 개체 레코드에 대해 CRUD 작업을 수행할 수 있습니다.

사용자 지정 활동에는 만들기 및 읽기만 허용됩니다.

7

값이 변경될 수 있는 경우(즉, &quot;자동차 색상&quot;이 파란색에서 빨간색으로 변경됨) 사용자 지정 개체를 사용합니다.

발생한 순간을 추적하고 해당 세부 사항을 변경할 수 없는 경우(예: &quot;구매한 자동차&quot;) 사용자 지정 활동을 사용합니다.

8

사용자 정의 오브젝트는 해당 사실을 알려줍니다. 즉, 현재 값입니다.

사용자 지정 활동은 과거에 발생한 이벤트를 알려줍니다.

_2020-10-18_&#x200B;에 _Amit_&#x200B;에 의해 게시됨

## 2021년 1월 업데이트

2021년 1월에는 새로운 REST API를 출시하고 몇 가지 오류를 해결합니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 프로그래밍 양식 제출을 수행할 수 있는 [양식 제출](/help/rest-api/leads.md) 끝점이 추가되었습니다. 이제 서드파티 양식을 Marketo 양식과 통합하여 기존 마케팅 워크플로우를 활용할 수 있습니다.
* 랜딩 페이지의 직렬화된 HTML 버전을 반환하는 [랜딩 페이지 전체 콘텐츠 가져오기](/help/rest-api/landing-pages.md) 끝점을 추가했습니다. Marketo Engage에 로그인하지 않고도 랜딩 페이지의 완전히 개인화된 미리 보기를 렌더링할 수 있습니다. 이를 통해 통합 애플리케이션 내에서 편집 및 번역 워크플로를 간소화할 수 있습니다.
* 이제 Velocity 스크립트를 통해 액세스할 수 있는 사용자 지정 개체 수를 구성할 수 있습니다. 구성 지침은 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/email-setup/change-custom-object-retrieval-limits-in-velocity-scripting)에서 찾을 수 있습니다.

### 결함 해결

* [사용자 삭제](/help/rest-api/user-management.md) 끝점으로 인해 사용자 지정 서비스에서 사용 중인 API 전용 사용자를 삭제할 수 있는 문제가 해결되었습니다. 이제 &quot;611, API 서비스에서 사용 중인 API 사용자를 삭제할 수 없습니다&quot; 오류가 반환됩니다. [LM-141893]
* 경우에 따라 [사용자 가져오기](/help/rest-api/user-management.md) 끝점이 삭제된 사용자를 반환하는 문제를 해결했습니다. [LM-141542]
* [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/#operation/cloneProgramUsingPOST) 끝점인 문제를 해결했습니다. 255자를 초과하는 프로그램 이름을 지정한 경우 &quot;611, 프로그램을 복제할 수 없음 오류&quot;가 반환됩니다. 이제 &quot;701, 이름은 255자를 초과할 수 없음&quot;을 반환합니다. [LM-143436]
* [랜딩 페이지 초안 승인](https://developer.adobe.com/marketo-apis/api/asset/#operation/approveLandingPageUsingPOST) 엔드포인트와 관련된 문제가 해결되었습니다. 모바일 버전이 활성화된 랜딩 페이지를 승인했을 때 특정 경우에 데스크탑 버전에서 모바일 버전의 콘텐츠가 표시됩니다. [LM-146867]
* 하나 이상의 양식에서 후속 페이지로 사용 중인 랜딩 페이지의 승인을 취소할 수 있는 [랜딩 페이지 승인 취소](https://developer.adobe.com/marketo-apis/api/asset/#operation/unapproveLandingPageByIdUsingPOST) 엔드포인트 문제를 수정했습니다. 이제 오류 &quot;709, 랜딩 페이지 비승인 실패&quot;를 반환합니다. 하나 이상의 양식에서 양식 ID가 [_formId1,formId2,..._]&quot;인 후속 페이지로 랜딩 페이지를 사용하고 있습니다. [LM-143326]

_David_&#x200B;이(가) _2021-01-15_&#x200B;에 게시함

## Munchkin 160 Beta 및 비콘 API

**2021년 1월 27일:** 리드 연결 사용 중지의 영향을 받는 일부 Marketo 사용자가 하나 이상의 인스턴스에서 Munchkin Beta 설정이 활성화되었음을 나타내는 오류 알림을 받았습니다. 이 릴리스는 올바른 대상자에게 알릴 수 있을 때까지 유지됩니다. Munchkin JavaScript 버전 160부터 [Beacon API](https://developer.mozilla.org/en-US/docs/Web/API/Beacon_API)는 Munchkin이 Marketo 백엔드와 통신하는 기본 방법이 됩니다. 이 기능은 **useBeaconAPI** 구성 매개 변수를 통해 버전 159가 릴리스되면서 2020년 여름의 옵션으로 사용할 수 있게 되었습니다. 비콘 API는 이전 XMLHttpRequest 메서드를 사용하는 것보다 몇 가지 이점이 있지만 주요 개선 사항은 모든 최신 인터넷 브라우저에서 사용할 수 있는 HTTP 통신용 비차단 비동기 API라는 것입니다. Munchkin의 대부분의 사용자는 웹 사이트 동작의 변경을 알지 못하지만, 이 업데이트로 인해 Munchkin이 클릭 이벤트를 백엔드에 제출하기 위해 기다리는 동안 탐색을 차단하지 못합니다. 또는 더 간단히 말하면, 이 모든 것이 방지되지만, Munchkin이 새 페이지에 대한 링크를 클릭한 후 브라우저를 &quot;중단&quot;시킬 가능성이 없습니다. 일부 Marketo 고객에게는 드물지만 좌절감을 주는 경우가 있었습니다.

2021년 1월 27일부터 이 버전의 롤아웃은 일정 조정을 보류 중입니다. 이 변경과 관련된 문제는 예상되지 않으며 테스트 중에 식별된 바는 없지만 Marketo에서 Munchkin의 가능한 모든 배포 구성을 테스트하는 것은 불가능하므로 이 변경 사항을 미리 테스트하거나 이 버전의 일반 공급 시까지 이 변경 사항을 취소할 수 있습니다. 다양한 시나리오에 대한 지침은 아래에 나와 있습니다.

### Beacon API 테스트

예정된 버전이 있을 것으로 예상하여 업데이트된 비콘 API를 테스트하려면 외부 테스트 페이지에서 Munchkin 구성에 **useBeaconAPI** 매개 변수를 추가하면 됩니다. 이 테스트는 Munchkin의 GA 또는 베타 버전에서 작동합니다. 구성 매개 변수는 7행 `Munchkin.init()`에서 `{ 'useBeaconAPI': true}` 메서드 호출의 두 번째 인수에 아래에 나와 있습니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('299-BYM-827', {"useBeaconAPI":true});
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName['head'](0).appendChild(s);
})();
</script>
```

### Marketo 랜딩 페이지에서 Munchkin Beta 비활성화

Marketo 랜딩 페이지에서 Munchkin Beta을 비활성화하려면 구독의 관리 섹션에서 [보물 상자](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features) 메뉴에 액세스하고 랜딩 페이지의 Munchkin Beta 설정을 비활성화로 변경해야 합니다.

### 외부 페이지에서 Munchkin Beta 비활성화

Beta 버전의 Munchkin JavaScript을 외부 웹 페이지에 배포한 경우 일반적으로 사용할 수 있을 때까지 이 변경 사항을 취소하려면 **munchkin&quot;을 타깃팅하기 위해 Munchkin JS 코드 조각을 변경해야 합니다.**{munchkin-beta가 아닌 **js**&#x200B;1} 파일을 저장합니다.**&#x200B;**&#x200B;**js** 파일입니다. 아래 예에서는 11행에 있는 **s.src** 변수의 값입니다. 코드 조각이 예제와 유사하지 않거나, 태그 관리자가 외부 페이지에 배포할 수 있으며, IT 리소스 또는 Munchkin 추적이 활성화된 웹 사이트를 관리하는 사람에게 연락해야 할 수 있습니다.

```javascript
<script type="text/javascript">
(function() {
  var didInit = false;
  function initMunchkin() {
    if(didInit === false) {
      didInit = true;
      Munchkin.init('299-BYM-827');
    }
  }
  var s = document.createElement('script');
  s.type = 'text/javascript';
  s.async = true;
  s.src = '//munchkin.marketo.net/munchkin.js';//This line should have the munchkin.js file, not munchkin-beta.js
  s.onreadystatechange = function() {
    if (this.readyState == 'complete' || this.readyState == 'loaded') {
      initMunchkin();
    }
  };
  s.onload = initMunchkin;
  document.getElementsByTagName['head'](0).appendChild(s);
})();
</script>
```

_케니_&#x200B;이(가) _2021-01-08_&#x200B;에 게시함

## 이메일 V1의 최종 API 사용 중단

[이메일 V1의 사용 중단 2년 전부터](https://nation.marketo.com:443/t5/knowledgebase/email-editor-1-0-is-being-deprecated-june-18th/ta-p/250666) 및 2021년 3월 17일 런던 및 네덜란드 구독과 2021년 3월 19일 기타 모든 구독에 대한 3월 유지 관리 릴리스부터 V1 이메일에 대한 모든 API 지원이 종료됩니다. 이 릴리스 이후 Asset API를 통해 V1 이메일과 상호 작용하려고 하면 오류가 발생하고 아무 작업도 수행되지 않습니다. 2021년 2월 24일 이후의 알려진 나머지 모든 사용자에게 알림이 전송되었지만, 이러한 에셋과 상호 작용하려고 하는 통합이 아직 있을 수 있습니다. 영향을 받는 통합의 가장 일반적인 유형은 디지털 에셋 관리, 번역 및 현지화를 제공하는 서비스입니다. 이 변경으로 인해 통합 오류가 발생하는 경우에도 [자산을 편집하고 승인하여 문제가 있는 자산을 업그레이드할 수 있습니다](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/transitioning-to-email-editor-2-0). 이메일 에셋이 V2로 업그레이드되면 통합 서비스와 함께 사용을 재개할 수 있습니다.

_케니_&#x200B;이(가) _2021-03-17_&#x200B;에 게시함

## 2021년 5월 업데이트

2021년 5월에 새로운 REST API를 출시하고, 기존 REST API를 개선하고, 몇 가지 오류를 해결합니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 프로그램 멤버십 레코드를 검색, 업데이트 및 삭제할 수 있는 프로그램 멤버 API가 추가되었습니다. 자세한 내용은 [REST API > 잠재 고객 데이터베이스 > 프로그램 구성원](/help/rest-api/program-members.md)을 참조하세요.
* 일대다 관계의 리드와 연결된 첫 번째 수준 Marketo 사용자 지정 개체 레코드를 내보낼 수 있는 대량 사용자 지정 개체 추출 API가 추가되었습니다. 자세한 내용은 [REST API > 대량 추출 > 대량 사용자 지정 개체 추출](/help/rest-api/bulk-custom-object-extract.md)을 참조하십시오.
* 사용자가 ECID(Adobe Experience Cloud ID)를 검색할 수 있도록 [리드 API](/help/rest-api/leads.md) 및 [리드 추출 API](/help/rest-api/bulk-lead-extract.md)를 모두 개선했습니다. 이를 통해 [Adobe Experience Cloud의 대상자를 동기화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html?lang=ko)하는 사용자는 ECID가 연결된 리드를 식별할 수 있습니다. 이렇게 하면 다른 Adobe Experience Cloud 제품과의 [통합 가능성](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024277392-Adobe-Experience-Cloud-Using-the-ECID-for-integration)이 열립니다.
* 가져오기 프로세스 중에 회사 레코드로 리드를 추가할 수 있도록 [대량 리드 가져오기 API](/help/rest-api/bulk-lead-import.md)를 개선했습니다. 이 작업은 가져오기 파일에 **externalCompanyId** 필드를 포함하여 수행됩니다.
* Marketo Engage UI에서 발견된 기능과 패리티를 제공하기 위해 여러 프로그램 엔드포인트가 향상되었습니다. 이벤트 프로그램에서 만들기, 복제 또는 이동 작업을 허용하도록 [프로그램 만들기](/help/rest-api/assets.md) 및 [프로그램 복제](https://developer.adobe.com/marketo-apis/api/asset/) 끝점을 개선했습니다. 다른 프로그램 유형 아래에 이벤트 프로그램을 &quot;중첩&quot;하여 구성하는 사용자를 위한 것입니다. 또한 푸시 알림, 인앱 메시지, 보고서, 포함된 소셜 Assets이 있는 랜딩 페이지를 포함하는 프로그램을 삭제할 수 있도록 [프로그램 삭제](https://developer.adobe.com/marketo-apis/api/asset/) 끝점을 개선했습니다.
* Marketo 관리자는 [특정 필드를 &quot;중요&quot;로 표시](https://experienceleague.adobe.com/ko/docs/marketo/using/home)할 수 있으므로 해당 값을 [양식에서 미리 채우지 않음](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/forms/form-fields/disable-pre-fill-for-a-form-field)하여 사용자의 중요한 데이터를 보호할 수 있습니다. Marketo Engage UI에 있는 이 기능과 동등하도록 여러 양식 필드 끝점을 개선했습니다.

### 결함 해결

* 프로그램 삭제 엔드포인트 문제를 수정했습니다. 공유 폴더에서 프로그램을 삭제하려고 하면 &quot;611, System Error&quot;가 반환됩니다. 이제 &quot;대상 프로그램이 공유 폴더에 있으므로 삭제할 수 없습니다. 삭제를 시도하기 전에 폴더 공유를 해제해야 합니다.&quot;
* 복제 프로그램 엔드포인트 문제를 수정했습니다. 흐름 단계에 DateTime이 포함된 프로그램을 복제하려고 하면 &quot;611, 시스템 오류&quot;가 반환됩니다. 이제 프로그램을 성공적으로 복제했습니다.
* 실수로 이메일 프로그램 아래에 프로그램을 만들 수 있었던 프로그램 만들기 엔드포인트 문제를 수정했습니다(허용되지 않음).
* 복제 프로그램 엔드포인트 문제를 수정했습니다. 랜딩 페이지가 포함된 프로그램을 복제한 경우, 대상 프로그램의 랜딩 페이지 이름에 프로그램 이름과 랜딩 페이지 이름 사이에 밑줄이 누락되었습니다. 예: `http://<_pod_\>.marketo.com/lp/<_munchkin_\>/<_program name_\>**_**<_LP name_\>.html`

_David_&#x200B;이(가) _2021-05-07_&#x200B;에 게시함

## Adobe Exchange에 참여할 수 있는 제한된 시간 제안

Marketo Engage 파트너 커뮤니티 지원은 고객 성공의 한 축입니다. Marketo Engage 통합 에코시스템이 Exchange 마켓플레이스에서 잘 표현되고 LaunchPoint 파트너를 위한 특별 오퍼가 있는지 확인하고 싶습니다. LaunchPoint 파트너에게 2022년 말까지 Exchange 프로그램의 무료 Innovate 파트너 관계(약 1만 5천 달러)를 제공합니다. LaunchPoint 파트너가 Exchange Partner Portal에서 통합 목록을 만들 수 있도록 장려하기 위해 이 오퍼를 고안했습니다. 이 목록은 Adobe Exchange Marketplace에서 공개적으로 검색할 수 있습니다. 2022년 12월까지 무료로 제공되는 Innovate 파트너십 혜택의 전체 목록을 보려면

1. [Adobe Exchange 파트너 지원 센터](https://adobeexchangeec.zendesk.com/hc/en-us?mkt_tok=NjA4LURIVi05MTUAAAF-P5lIeVWOuBmKMS_uE_NpgFKtC0ukt7z_ksnq_Sbzb6mzXUuXpqpqQeujtPdZ24WcjMdptygQSR9XrYt_Cw)&#x200B;(으)로 이동
1. 오른쪽 상단의 &quot;요청 제출&quot;을 클릭합니다.
1. **아래에서 문제를 선택하십시오** 드롭다운에서 &quot;Adobe Exchange 지원&quot;을 선택하십시오.
1. **전자 메일 주소**&#x200B;에 전자 메일 주소를 입력하십시오.
1. **제목** 상자에 &quot;LaunchPoint 오퍼&quot;를 입력하십시오.
1. **설명** 상자에 &quot;LaunchPoint Offer&quot;를 입력하십시오.
1. **지원 유형** 드롭다운에서 &quot;프로그램 지원&quot;을 선택합니다.
1. **Adobe Exchange 제품** 드롭다운에서 &quot;Adobe Exchange 프로그램&quot;을 선택합니다.
1. 양식을 제출합니다. 우리 팀이 곧 연락을 드립니다!

_David_&#x200B;이(가) _2021-07-22_&#x200B;에 게시함

## 2021년 8월 업데이트

2021년 8월에는 기존 REST API를 개선하고 몇 가지 오류를 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 사용자가 6개의 다른 활동 유형에 대한 기본 특성을 사용하여 필터링할 수 있도록 벌크 활동 추출 API를 개선했습니다. 자세한 내용은 [일괄 활동 추출](/help/rest-api/bulk-activity-extract.md)을 참조하세요.
* Marketo Sales Connect 사용자가 자신의 판매 활동 데이터에 더 많이 액세스할 수 있도록 하기 위해 추가 판매 활동 속성을 활성화했습니다. 판매 이메일을 보내고, 판매 이메일을 열고, 판매 이메일 활동을 클릭하기 위해 다음 속성을 추가했습니다.

* Marketo 영업 담당자 ID - Sales Connect의 개인 레코드에 대한 고유 ID
* 판매 캠페인명 - 이메일이 판매 캠페인의 일부인 경우 판매 캠페인의 이름
* Sales Campaign URL - 이메일이 Sales Campaign의 일부인 경우 Sales Campaign용 Sales Connect URL
* 판매 템플릿 이름 - 템플릿이 사용된 경우 Sales Connect의 이메일 템플릿 이름
* 판매 템플릿 URL - 템플릿이 사용된 경우 이메일 템플릿에 대한 Sales Connect URL

### 이메일

* `earliestUpdatedAt`/`latestUpdatedAt` 필터를 추가하여 전자 메일 가져오기 끝점을 개선했습니다. 이를 통해 `updatedAt` 필드를 사용하여 전자 메일의 하위 집합만 검색할 수 있으므로 증분 동기화를 허용할 수 있습니다.
* [챔피언 및 챌린저](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/email-tests-champion-challenger/add-an-email-champion-challenger) 유형 전자 메일 레코드 검색을 지원하도록 전자 메일 가져오기, 이름별 전자 메일 가져오기, ID 끝점별 전자 메일 가져오기를 개선했습니다.

### 결함 해결

* 사용자 가져오기 엔드포인트 문제를 수정했습니다. [마케팅 일정](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/marketing-calendar/understanding-the-calendar/issue-revoke-a-marketing-calendar-license) 라이선스를 발급받은 사용자가 반환되지 않았습니다. 이제 마케팅 달력 사용자가 올바르게 반환됩니다.
* 양식 제출 엔드포인트 문제를 수정했습니다. 중복 가망 고객 레코드가 있는 경우 제출 양식을 사용하여 &quot;1007, 여러 가망 고객 일치 조회 기준&quot; 오류를 발행합니다. 이제 양식 제출로 [Forms 2.0 API](/help/javascript-api/forms-api-reference.md)와 같은 방식으로 가장 최근에 업데이트된 레코드가 업데이트됩니다.
* 리드 필드 업데이트 및 리드 필드 만들기 엔드포인트에서 반환되는 몇 가지 오해의 소지가 있는 오류 메시지가 개선되었습니다. [LM-151890, LM-151888, LM-151889]
* 이름별 리드 필드 가져오기 및 리드 필드 엔드포인트 가져오기 문제를 수정했습니다. 두 종단점은 잠재적으로 오래된 정보를 반환할 수 있습니다. 이제 항상 현재 정보를 반환합니다.
* 범위의 마지막 바이트가 반환되지 않은 부분 검색에 &quot;범위&quot; HTTP 헤더를 사용할 때 [대량 추출 API](/help/rest-api/bulk-extract.md) 문제를 해결했습니다.
* 업데이트 코드 조각 메타데이터 끝점 문제가 수정되었습니다. 코드 조각 이름 또는 설명을 업데이트할 때 코드 조각 상태가 &quot;승인됨, 초안으로&quot;로 변경되었습니다. 이제 코드 조각 이름 또는 설명을 업데이트한 후에도 스니핑된 상태가 변경되지 않습니다.
* 이메일 모듈 추가 엔드포인트 문제를 수정했습니다. 코드 조각이 포함된 모듈을 추가할 때 &quot;611, System Error&quot;가 반환되었습니다. 이제 모듈이 이메일에 올바르게 추가됩니다.
* 프로그램 삭제 엔드포인트 문제를 수정했습니다. 인앱 메시지 로컬 자산이 포함된 프로그램을 삭제할 때 &quot;611, 시스템 오류&quot;가 반환되었습니다. 이제 프로그램이 올바르게 삭제됩니다.

_David_&#x200B;이(가) _2021-08-22_&#x200B;에 게시함

## Munchkin 버전 161 롤아웃

Munchkin 버전 161은 2021년 9월 7일부터 Munchkin Beta이 활성화되면서 구독률 10%로 롤아웃이 시작되며, 이어 9월 16일 50%, 9월 30일 100%로 롤아웃된다. 이 변경 사항은 Marketo 랜딩 페이지 및 새 버전이 롤아웃된 구독으로부터 로드되는 외부 랜딩 페이지에 제공되는 munchkin-beta.js 파일의 버전에 영향을 줍니다. 이 버전에서는 Munchkin Associate Lead 메서드를 완전히 사용하지 않습니다. 이 메서드는 Marketo 구독에 사용자 데이터를 제출하고 알려진 사용자 레코드와 연결된 웹 검색 기록을 허용하는 기능입니다. [Forms JS API](/help/javascript-api/forms-api-reference.md), 양식 제출 API 및 [리드 REST API 연결](/help/rest-api/leads.md)과 같은 보다 현대적이고 안전한 대안을 위해 리드 연결이 제거됩니다. 귀하 또는 귀사에서 이 방법을 사용하는 경우 10월 릴리스 롤아웃이 시작되도록 예정된 2021년 10월 12일까지 사용을 중단해야 합니다. Munchkin Beta를 더 이상 사용하지 않으려면 `disabled`보물 상자 메뉴[에서 &quot;랜딩 페이지의 Munchkin Beta&quot; 기능을 ](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/settings/enable-or-disable-treasure-chest-features)&#x200B;(으)로 전환하여 Marketo 랜딩 페이지의 사용을 비활성화할 수 있습니다. Munchkin Beta JavaScript을 외부 웹 페이지에 배포하고 기본 Munchkin 릴리스 채널로 전환하려면 코드 조각을 업데이트하여 munchkin-beta.js 대신 munchkin.js에서 Munchkin JavaScript을 로드해야 합니다.

_케니_&#x200B;이(가) _2021-08-24_&#x200B;에 게시함

## Munchkin 서비스의 TLS 1.0 및 TLS 1.1 서비스 종료

2021년 10월 21일부터, Munchkin JavaScript을 방문자에게 제공하는 데 사용되는 munchkin.marketo.net에서는 더 이상 [TLS 1.0 또는 TLS 1.1.](https://en.wikipedia.org/wiki/Transport_Layer_Security)을 사용하는 연결을 허용하지 않습니다. 이러한 암호화 표준은 더 이상 웹 보안 모범 사례의 일부로 허용되지 않으며 더 이상 최신 브라우저 버전에서 지원되지 않습니다. 이 변경의 결과로 예상되는 부정적인 영향은 없습니다.

_케니_&#x200B;이(가) _2021-10-04_&#x200B;에 게시함

## 2021년 10월 업데이트

2021년 10월에는 기존 REST API를 개선하고 몇 가지 오류를 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 양식 제출의 일부로 프로그램 구성원 사용자 지정 필드를 지원하도록 [양식 제출](https://developer.adobe.com/marketo-apis/api/mapi/#operation/SubmitFormUsingPOST) 끝점을 개선했습니다. 선택적으로 [여기](/help/rest-api/leads.md)에 설명된 대로 양식을 추가할 프로그램으로 프로그램을 지정하거나 프로그램 멤버 사용자 정의 필드를 추가할 프로그램으로 지정할 수 있습니다.
updatedAt 특성을 기반으로 날짜 범위 기반 쿼리를 지원하도록 [프로그램 구성원 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getProgramMembersUsingGET) 끝점을 개선했습니다. [여기](/help/rest-api/program-members.md)에 설명된 대로 시작 및 종료 날짜/시간 매개 변수를 전달하여 이 작업을 수행합니다.
* [중요 필드](/help/rest-api/leads.md)을(를) 지원하도록 [리드 필드](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/field-management/mark-a-field-as-sensitive) API를 개선했습니다. [이름별 리드 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldByNameUsingGET), [리드 필드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getLeadFieldsUsingGET), [리드 필드 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) 및 [리드 필드 업데이트](https://developer.adobe.com/marketo-apis/api/mapi/#operation/updateLeadFieldUsingPOST) 엔드포인트는 이제 isSensitive 특성을 지원합니다.

### 결함 해결

* [사용자 관리](/help/rest-api/user-management.md) API 문제를 해결했습니다. [Sales Insight](https://business.adobe.com/products/marketo/sales-insight.html)과(와) 함께 사용하도록 구성된 Marketo 사용자에 관련되어 있습니다. 이제 [사용자 가져오기](https://developer.adobe.com/marketo-apis/api/user/#operation/getUsersUsingGET) 끝점에서 이러한 사용자를 반환했으며, 이제 [사용자 삭제](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST) 끝점을 사용하여 이러한 사용자를 삭제할 수 있습니다. [LM-155864]
* [서식 있는 텍스트 필드](https://developer.adobe.com/marketo-apis/api/asset/#tag/Form-Fields/addRichTextFieldUsingPOST) 끝점 추가 문제를 해결했습니다. 이메일, 랜딩 페이지, 코드 조각 또는 양식에 65k자보다 긴 서식 있는 텍스트 필드를 추가할 때 &quot;611, 시스템 오류&quot;가 반환되었습니다. 이제 오류 &quot;701, 작업을 완료할 수 없습니다. &#39;content&#39;가 최대 길이인 65,535바이트를 초과합니다.&quot;

_David_&#x200B;이(가) _2021-10-25_&#x200B;에 게시함

## 2022년 1월 업데이트

2022년 1월에는 기존 REST API를 개선하고 여러 결함을 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 사용자가 [updatedAt](/help/rest-api/bulk-custom-object-extract.md) 날짜 범위를 사용하여 필터링할 수 있도록 **대량 사용자 지정 개체 추출** API를 개선했습니다.
* 프로그램 멤버 필드에 대한 메타데이터를 만들고, 업데이트하고, 검색할 수 있도록 해 주는 프로그램 멤버 필드 메타데이터 API가 추가되었습니다. 자세한 내용은 [프로그램 구성원 > 필드](/help/rest-api/program-members.md)를 참조하세요.
* 회사 필드에 대한 메타데이터를 검색할 수 있도록 해 주는 회사 필드 메타데이터 API가 추가되었습니다. 자세한 내용은 [회사 > 필드](/help/rest-api/companies.md)를 참조하세요.
* Opportunity 필드에 대한 메타데이터를 검색할 수 있도록 해 주는 Opportunity 필드 메타데이터 API가 추가되었습니다. 자세한 내용은 [기회 > 필드](/help/rest-api/opportunities.md)를 참조하세요.
* 지정된 계정 필드에 대한 메타데이터를 검색할 수 있도록 해 주는 지정된 계정 필드 메타데이터 API를 추가했습니다. 자세한 내용은 [명명된 계정 > 필드](/help/rest-api/named-accounts.md)를 참조하세요.
* 필드가 REST API로 만들어졌는지 여부를 나타내는 새 부울 속성 **isApiCreated**&#x200B;을(를) 반환하도록 필드 메타데이터 끝점이 업데이트되었습니다.

### 결함 해결

* [리드 필드 만들기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST) 엔드포인트에 대한 호출 시간과 새로 만든 리드 필드를 스마트 목록에서 사용할 수 있는 시간 사이의 지연 문제를 해결했습니다. [LM-152838]
* Marketo Engage UI에서 [양식에 필드 추가](https://developer.adobe.com/marketo-apis/api/mapi/#operation/createLeadFieldUsingPOST)에 사용되는 양식 필드 드롭다운 목록에서 생성된 필드를 사용할 수 없는 [리드 필드 만들기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/demand-generation/forms/creating-a-form/add-a-field-to-a-form) 엔드포인트와 관련된 문제가 수정되었습니다. [LM-158243]
* isTriggerable=true 매개 변수가 지정된 경우 트리거 가능한 캠페인이 반환되지 않는 [캠페인 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/getCampaignsUsingGET) 엔드포인트 문제를 수정했습니다. [LM-158283]
* [목록 ID로 리드 가져오기](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteTokenByNameUsingPOST) 끝점이 특정 경우에 오류 &quot;611, 시스템 오류&quot;를 반환하는 문제를 해결했습니다. [LM-157214]
* [리드 필드 업데이트](/help/rest-api/leads.md) 끝점에서 반환된 여러 오류 메시지를 정리했습니다. [LM-151886, LM-151888, LM-151889]

_David_&#x200B;이(가) _2022-01-27_&#x200B;에 게시함

## 2022년 3월 업데이트

2022년 3월에는 기존 REST API를 개선하고 몇 가지 오류를 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 일괄 활동 추출 API에서 생성한 내보내기 파일에 **actionResult** 필드를 추가했습니다. 이 필드는 성공, 건너뜀 및 실패한 활동을 구분하는 데 사용할 수 있습니다.
* **전자 메일 API**&#x200B;의 응답에 [isOpenTrackingDisabled](/help/rest-api/emails.md) 필드를 추가했습니다. 이 필드를 사용하여 [공개 추적 사용 안 함](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-editor-v2-0-overview) 기능을 사용할지 여부를 확인할 수 있습니다.
* 프로그램 태그를 선택적으로 관리할 수 있는 두 가지 끝점이 추가되었습니다. [프로그램 태그 업데이트](/help/rest-api/programs.md) 끝점을 사용하면 프로그램 태그를 선택적으로 업데이트할 수 있습니다. [프로그램 태그 삭제](/help/rest-api/programs.md) 끝점을 사용하면 프로그램 태그를 선택적으로 삭제할 수 있습니다.
* **isExecutable** 매개 변수를 [Clone Smart Campaign](/help/rest-api/smart-campaigns.md) 끝점에 추가했습니다. 이 매개 변수를 사용하면 프로그램을 실행 프로그램으로 복제할 수 있습니다.
* **headStart** 필드를 [프로그램 API](/help/rest-api/programs.md)에 추가했습니다. 이를 통해 전자 메일 프로그램에 대한 [Head Start](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/email-programs/email-program-actions/head-start-for-email-programs) 설정을 만들고, 업데이트하고, 검색할 수 있습니다.

### 결함 해결

* [전자 메일 동적 콘텐츠 가져오기](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET) 엔드포인트와 관련된 문제가 해결되었습니다. 템플릿 관계가 깨진 이메일에서 동적 콘텐츠로 제목 줄을 검색하려고 할 때 오류 709가 반환되었습니다. &quot;&quot;API는 템플릿을 사용하는 이메일에 대한 작업만 허용합니다.&quot; 이제 끝점이 다이내믹 콘텐츠를 반환합니다. [LM-152331]
* [잠재 고객 동기화](https://developer.adobe.com/marketo-apis/api/mapi/#operation/syncLeadUsingPOST) 엔드포인트와 관련된 문제가 해결되었습니다. externalSalesPersonId를 사용하고 action = createDuplicate를 사용하여 sales Person을 리드와 연관시킬 때 Sales Person 연관이 발생하지 않습니다. [LM-158990]

### Adobe IMS 통합

* [Adobe IMS](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/marketo-with-adobe-identity/adobe-identity-management-overview)에 온보딩한 사용자는 [Marketo 사용자 관리 API](/help/rest-api/user-management.md)를 모두 사용할 수 없습니다. 다음 엔드포인트는 Adobe IMS와 통합된 Marketo 인스턴스에서 호출될 때 오류를 반환합니다. [사용자 초대](https://developer.adobe.com/marketo-apis/api/user/#operation/inviteUserUsingPOST), [ID로 초대된 사용자 가져오기](https://developer.adobe.com/marketo-apis/api/user/#operation/getInvitedUserUsingGET), [사용자 특성 업데이트](https://developer.adobe.com/marketo-apis/api/user/#operation/updateUserAttributeUsingPOST), [사용자 삭제](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteUserUsingPOST) 및 [초대된 사용자 삭제](https://developer.adobe.com/marketo-apis/api/user/#operation/deleteInvitedUserUsingPOST). 대신 [Adobe 사용자 관리 API](https://developer.adobe.com/umapi/)를 사용해야 합니다.

_David_&#x200B;이(가) _2022-03-14_&#x200B;에 게시함

## 2022년 5월 업데이트 -

2022년 5월에는 기존 REST API를 개선하고 여러 결함을 해결하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

* Marketo Engage 인스턴스에서 [SFDC 동기화](/help/rest-api/companies.md) 또는 [Microsoft Dynamics 동기화](/help/rest-api/opportunities.md)를 사용하도록 설정한 경우 [회사](/help/rest-api/sales-persons.md), [영업 기회](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/crm-sync/salesforce-sync/sfdc-sync-details/sfdc-sync-field-sync) 및 [영업 사원](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/microsoft-dynamics-sync-details/microsoft-dynamics-sync-user-sync) 레코드를 검색하는 기능을 추가했습니다.
* 이메일 제목줄에서 [다이내믹 콘텐츠](https://developer.adobe.com/marketo-apis/api/asset/#operation/getEmailDynamicContentUsingGET)을(를) 검색할 수 있도록 [이메일 다이내믹 콘텐츠 가져오기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/general/functions-in-the-editor/using-dynamic-content-in-an-email) 끝점을 업데이트했습니다. 이 기능은 지정된 이메일이 이메일 템플릿에 연결되어 있는지 여부에 관계없이 작동합니다.

`POST /rest/asset/v1/form/{id}/field/State.json?values=[{"label":"Alaska"},{"value":"AK"},{"label":"West Virginia","value":"WV"},{"label":"Wyoming","value":"WY"}]`

* [isNot](https://developer.adobe.com/marketo-apis/api/asset/#operation/getAllProgramMemberFieldsUsingGET) 유형 **Invisibility 규칙**&#x200B;에 대해 여러 비교 값을 추가할 수 있도록 [양식 필드 표시 규칙 추가](/help/rest-api/forms.md) 끝점을 업데이트했습니다. 다음은 한 예입니다.

`POST /rest/asset/v1/form/{id}/field/LastName/visibility.json?visibilityRule={"ruleType":"show","rules":[{"subjectField":"LastName","operator":"isNot","values":["A","B","C"]}`

### 결함 해결

* [leadFormFields](/help/rest-api/leads.md) 매개 변수의 특성에 대해 &quot;null&quot;을 전달할 때 발생한 [양식 제출](/help/rest-api/leads.md) 끝점의 문제를 해결했습니다. 반환된 오류는 &quot;611, 시스템 오류&quot;입니다. 이제 올바르게 &quot;1003, 양식 유효성 검사 실패&quot; 오류를 반환합니다. [LM-162213]

_David_&#x200B;이(가) _2022-05-09_&#x200B;에 게시함

## 2022년 8월 업데이트

2022년 8월에는 기존 REST API를 개선하고 있습니다. 아래의 전체 업데이트 목록을 참조하십시오.

LWe가 내보내기 프로그램 멤버 작업 끝점 만들기를 호출할 때 사용할 수 있는 몇 가지 필터를 새로 추가했습니다. 많은 필터들이 추출된 데이터 세트를 정제하기 위해 서로 조합되어 사용될 수 있다는 점에 유의한다.

* **programIds** 필터를 사용하여 처리량을 개선하는 데 도움이 되는 최대 10개의 프로그램 식별자를 지정할 수 있습니다.
* **isExhausted** 필터를 사용하여 [콘텐츠를 모두 사용한 사용자](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/email-marketing/drip-nurturing/using-engagement-programs/people-who-have-exhausted-content)의 레코드를 필터링할 수 있습니다.
* **groothCadence** 필터를 사용하여 [참여 프로그램 케이던스](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/program-flow-actions/change-engagement-program-cadence)를 기준으로 레코드를 필터링할 수 있습니다.
* **statusNames** 필터를 사용하여 하나 이상의 [프로그램 상태](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/programs/creating-programs/understanding-program-membership)에 대한 레코드를 필터링할 수 있습니다.
* **updatedAt** 필터를 사용하여 날짜 범위를 기준으로 레코드를 필터링할 수 있습니다.

### 공지

* [Identity](https://developer.adobe.com/marketo-apis/api/identity/#operation/identityUsingGET) 끝점의 동작이 변경되었습니다. 끝점을 호출하고 **access_token** 매개 변수를 포함하지 않으면 &quot;603, Access denied&quot; 오류가 반환됩니다. 이전에는 &quot;600, 빈 액세스 토큰&quot; 오류가 반환되었습니다. &quot;600, 빈 액세스 토큰&quot; 오류는 더 이상 사용되지 않습니다.

_David_&#x200B;이(가) _2022-09-03_&#x200B;에 게시함

## 2022년 10월 업데이트

2022년 10월에 기존 REST API를 개선합니다. 아래의 전체 업데이트 목록을 참조하십시오.

* 가져오기 프로세스 중에 영업 사원 레코드에 잠재 고객 추가를 지원하도록 [대량 잠재 고객 가져오기 API](/help/rest-api/bulk-lead-import.md)를 개선했습니다. 이 작업은 가져오기 파일에 **externalSalesPersonId** 필드를 포함하여 수행됩니다.
* 점수 유형 필드를 만들 때 발생한 [잠재 고객 필드 만들기](/help/rest-api/leads.md) 엔드포인트 문제를 해결했습니다. 이 필드는 Marketo Engage UI의 [점수 변경](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/change-score) 흐름 작업에서 사용할 수 없습니다. [LM-166815]

### 공지

* 프로그램 구성원 특성 `acquiredBy`을(를) 업데이트할 수 있도록 변경했습니다.

_David_&#x200B;이(가) _2022-10-18_&#x200B;에 게시함

## Marketo Forms REST AP에 대한 향후 변경 사항

Adobe Marketo Engage Forms Asset API는 현재 2023년 3월 24일로 예정된 2022.R2 릴리스부터 양식이 프로그램의 하위 항목인지 여부에 관계없이, 접두사가 있는 프로그램 이름 없이 양식 이름만 일관되게 반환합니다. 이 변경 사항은 에셋 이름과 관련된 Forms API의 동작을 Adobe Marketo Engage Asset API의 나머지 부분과 일관되게 만듭니다. 서비스 중단을 방지하려면 Marketo Engage Forms API를 사용하는 모든 통합을 검토하고 통합자와 협력하여 이를 수용하기 위해 변경 사항이 필요한지 확인해야 합니다. 이러한 변경 이전에 Forms API에서 반환된 이름에는 마케팅 활동의 프로그램 하위 항목인 양식에 대한 프로그램 이름이 일관되지 않게 접두사로 추가되었습니다. 예를 들어 &quot;프로그램 1&quot;의 하위 양식인 &quot;양식 1&quot;이라는 양식의 이름은 API에서 다음과 같이 반환될 수 있습니다. 프로그램 1.Form 1 또는 양식 1 2022.R2 릴리스부터 양식 이름은 항상 접두사가 있는 프로그램 이름 없이 반환됩니다. 동일한 예를 사용할 경우 이름은 항상 양식 1입니다.

_케니_&#x200B;이(가) _2022-11-04_&#x200B;에 게시함

## 2023년 1월 업데이트

2023년 1월에 관리 UI에 대한 API 관련 개선 사항을 완료했으며 두 가지 발표를 할 예정입니다. 아래의 전체 업데이트 목록을 참조하십시오.

관리자 UI

### 벌크 납 추출

* 구독에 대한 대량 추출 API 일일 용량 할당을 볼 수 있도록 Marketo Engage 관리 UI가 향상되었습니다. 또한 지난 7일 동안 API-User의 용량 사용을 볼 수 있습니다. 자세한 내용은 [여기](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/settings/bulk-export-api-information)를 참조하세요.

### 결함 해결

* [기회 삭제](https://developer.adobe.com/marketo-apis/api/mapi/#operation/deleteOpportunitiesUsingPOST) 엔드포인트와 관련된 문제가 해결되었습니다. 경우에 따라 &quot;Remove from Opportunity&quot; 활동이 생성되지 않았습니다. [LM-172208]

### 공지

* REST API 및 HTTP 응답 메시지 변경 [이유 구문](https://nation.marketo.com/t5/product-documents/upcoming-change-to-marketo-rest-api/ta-p/331698)에 대해서는 Marketo 커뮤니티에서 [이 문서](https://www.rfc-editor.org/rfc/rfc7230#section-3.1.2)를 참조하십시오.
* 프로그램 구성원 특성 **statusReason**&#x200B;을(를) 업데이트할 수 있도록 변경했습니다.

_David_&#x200B;이(가) _2023-01-21_&#x200B;에 게시함
