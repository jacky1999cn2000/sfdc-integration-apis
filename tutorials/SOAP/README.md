# SOAP

* Login
  * request
```
POST /services/Soap/c/35.0 HTTP/1.1
Host: login.salesforce.com
Content-Type: text/xml
SOAPAction: ''
Cache-Control: no-cache
Postman-Token: abd96908-a17c-5dbd-8ebc-59ecf4f52952

<?xml version="1.0" encoding="utf-8" ?>
<env:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:env="http://schemas.xmlsoap.org/soap/envelope/">
  <env:Body>
    <n1:login xmlns:n1="urn:enterprise.soap.sforce.com">
      <n1:username>liang.zhao.sfdc.integration.apis@jz.com</n1:username>
      <n1:password>ba76acaHhtf5m1SYhiN0vQ6g1qYkWEGgo</n1:password>
    </n1:login>
  </env:Body>
</env:Envelope>
```
  * response
```
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:enterprise.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Body>
        <loginResponse>
            <result>
                <metadataServerUrl>https://na40.salesforce.com/services/Soap/m/35.0/00D46000000YxRg</metadataServerUrl>
                <passwordExpired>false</passwordExpired>
                <sandbox>false</sandbox>
                <serverUrl>https://na40.salesforce.com/services/Soap/c/35.0/00D46000000YxRg</serverUrl>
                <sessionId>00D46000000YxRg!ARIAQF4ajxRf3mwGQdzwZ3ButRQFhqOVrl5..jhK.zqdmbDSNKDP98U.FOyLh5R8sDw0Ckz1dJrww_HOAytwkSPbqbTk1sv7</sessionId>
                <userId>00546000000piQWAAY</userId>
                <userInfo>
                    <accessibilityMode>false</accessibilityMode>
                    <currencySymbol>$</currencySymbol>
                    <orgAttachmentFileSizeLimit>5242880</orgAttachmentFileSizeLimit>
                    <orgDefaultCurrencyIsoCode>USD</orgDefaultCurrencyIsoCode>
                    <orgDisallowHtmlAttachments>false</orgDisallowHtmlAttachments>
                    <orgHasPersonAccounts>false</orgHasPersonAccounts>
                    <organizationId>00D46000000YxRgEAK</organizationId>
                    <organizationMultiCurrency>false</organizationMultiCurrency>
                    <organizationName>JZ</organizationName>
                    <profileId>00e46000000g2doAAA</profileId>
                    <roleId xsi:nil="true"/>
                    <sessionSecondsValid>7200</sessionSecondsValid>
                    <userDefaultCurrencyIsoCode xsi:nil="true"/>
                    <userEmail>liang.zhao.sfdc01+3@gmail.com</userEmail>
                    <userFullName>LIANG ZHAO</userFullName>
                    <userId>00546000000piQWAAY</userId>
                    <userLanguage>en_US</userLanguage>
                    <userLocale>en_US</userLocale>
                    <userName>liang.zhao.sfdc.integration.apis@jz.com</userName>
                    <userTimeZone>America/Los_Angeles</userTimeZone>
                    <userType>Standard</userType>
                    <userUiSkin>Theme3</userUiSkin>
                </userInfo>
            </result>
        </loginResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

* Query Voter
  * request
```
POST /services/Soap/c/35.0 HTTP/1.1
Host: na40.salesforce.com
Content-Type: text/xml
SOAPAction: ''
Cache-Control: no-cache
Postman-Token: 77a980b3-c601-a937-61f6-50c5e2a684ed

<?xml version="1.0" encoding="utf-8"?>   
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
   xmlns:urn="urn:enterprise.soap.sforce.com">
  <soapenv:Header>
     <urn:SessionHeader>
        <urn:sessionId>00D46000000YxRg!ARIAQF4ajxRf3mwGQdzwZ3ButRQFhqOVrl5..jhK.zqdmbDSNKDP98U.FOyLh5R8sDw0Ckz1dJrww_HOAytwkSPbqbTk1sv7</urn:sessionId>
     </urn:SessionHeader>
  </soapenv:Header>
  <soapenv:Body>
     <urn:query>
        <urn:queryString>SELECT Id, Name, Precinct__r.Name FROM Voter__c</urn:queryString>
     </urn:query>
  </soapenv:Body>
</soapenv:Envelope>
```

  * response
```
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:enterprise.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:sf="urn:sobject.enterprise.soap.sforce.com">
  <soapenv:Header>
      <LimitInfoHeader>
          <limitInfo>
              <current>2</current>
              <limit>15000</limit>
              <type>API REQUESTS</type>
          </limitInfo>
      </LimitInfoHeader>
  </soapenv:Header>
  <soapenv:Body>
      <queryResponse>
          <result>
              <done>true</done>
              <queryLocator xsi:nil="true"/>
              <records xsi:type="sf:Voter__c">
                  <sf:Id>a0146000000u4DBAAY</sf:Id>
                  <sf:Name>Leslie Knope</sf:Name>
                  <sf:Precinct__r xsi:type="sf:Precinct__c">
                      <sf:Id xsi:nil="true"/>
                      <sf:Name>3rd District</sf:Name>
                  </sf:Precinct__r>
              </records>
              <size>1</size>
          </result>
      </queryResponse>
  </soapenv:Body>
</soapenv:Envelope>
```

* SOAP Headers (not HTTP headers, but headers in SOAP request; e.g. MruHeader - whether to include the newly created/updated record in Home tab's `Most Recently Used` records list)
  * request
```
<?xml version="1.0" encoding="utf-8"?>   
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:urn="urn:enterprise.soap.sforce.com"
  xmlns:urn1="urn:sobject.enterprise.soap.sforce.com"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <soapenv:Header>
     <urn:SessionHeader>
        <urn:sessionId>00D46000000YxRg!ARIAQF4ajxRf3mwGQdzwZ3ButRQFhqOVrl5..jhK.zqdmbDSNKDP98U.FOyLh5R8sDw0Ckz1dJrww_HOAytwkSPbqbTk1sv7</urn:sessionId>
     </urn:SessionHeader>
     <urn:MruHeader>
         <urn:updateMru>false</urn:updateMru>
     </urn:MruHeader>
  </soapenv:Header>
  <soapenv:Body>
     <urn:create>
        <urn:sObjects xsi:type="urn1:Voter__c"> <!--Zero or more repetitions:-->
           <!--You may enter ANY elements at this point-->
           <Name>Joan Callamezzo</Name>
           <Precinct__c>a0046000001SQszAAG</Precinct__c>
	   <Mailing_Address__c>3920 255th Place Se, Sammamish WA 98029</Mailing_Address__c>
        </urn:sObjects>
     </urn:create>
  </soapenv:Body>
</soapenv:Envelope>
```
  * response
```
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:enterprise.soap.sforce.com">
  <soapenv:Header>
      <LimitInfoHeader>
          <limitInfo>
              <current>3</current>
              <limit>15000</limit>
              <type>API REQUESTS</type>
          </limitInfo>
      </LimitInfoHeader>
  </soapenv:Header>
  <soapenv:Body>
      <createResponse>
          <result>
              <id>a0146000000u4qgAAA</id>
              <success>true</success>
          </result>
      </createResponse>
  </soapenv:Body>
</soapenv:Envelope>
```
It didn't show up in Home tab's `Recent Records` section - if change the MruHeader to `<urn:updateMru>true</urn:updateMru>`, then the record will show up there.
![1](/imgs/1.png)
