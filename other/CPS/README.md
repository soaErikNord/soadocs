# CPS
## Payment Plus
### Installation and Configuration
The CPS projects are being stored in a organization structure that looks like the following:<br>
--> Registry<br>
&nbsp;&nbsp;--> US Bank<br>
&nbsp;&nbsp;&nbsp;&nbsp;--> CPS

The services, scripts and required policies are all stored in the CPS organization.  These are all imported with the extracted archive file and will be replicated when these are uploaded into an existing PM environment.

When uploading to the PM environment, it is required to include the import property file.  This import will allow the virtual service endpoints to be hosted on the proper ND environment.

Follow these steps to properly import the services into a valid PM and ND environment:

1. Log into the PM environment with a proper user that has administrator rights.
2. From the left hand organization tree, select the ND cluster (or container) that will be hosting these services.
3. Take not of the Container Key field.
4. Open the migration.properties file.
5. Update '<replace this with your key>' with Container Key field that was copied in the step above.
6. Save this file.
7. From the left hand navigation pane, click on the Registry organization.  Note: this is the top parent organization, in some cases this could be renamed.
8. From the right hand actions portlet, click on the Import Package option.
9. For the Package Location, select the archive file that contains the services.
10. For the Migration Properties Location, select the migration.properties file that was update above.
11. Click on the Import button.  This will import everything properly into this PM environment.
12. Go to the following directory, US Bank --> CPS --> Policies --> Organizational Policies, and select the 'SchemaValidation' policy.
13. From the Workflow Actions on the right hand side, click on the Activate Policy link.
14. Go to the following directory, US Bank --> CPS --> Contracts --> Provided Contracts, and select the 'CPS Anonymous' contract.
15. From the Workflow Actions on the right hand side, click on the Activate Contract link.
16. Validate the service is properly deployed by click on the container that should be hosting this service.  The service should be listed on the Hosted Services tab.

### Create Payments

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0" xmlns:pay1="http://www.usbank.com/PaymentPlusments/ws/schemas/PaymentPluswebservice">
   <soapenv:Header>
       <pay:PaymentPlusCreateHeader> 
         <pay:TransactionIdentifier>Test</pay:TransactionIdentifier> 
         <!--Optional:--> 
         <pay:MessageIdentifier>Test</pay:MessageIdentifier> 
         <!--Optional:--> 
         <pay:ProviderInfo>Test</pay:ProviderInfo> 
      </pay:PaymentPlusCreateHeader> 
      <pay1:userNameToken>usbc.uatsjmarsh</pay1:userNameToken> 
   </soapenv:Header>
   <soapenv:Body>
      <pay:PaymentPlusCreateRequest> 
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID> 
         <pay:OrgShortName>ADMIN7</pay:OrgShortName> 
         <pay:PaymentType>PA</pay:PaymentType> 
         <pay:RequestDate>2015-06-30</pay:RequestDate> 
         <pay:ControlNumber>ETMWSDLTEST</pay:ControlNumber> 
         <!--Optional:--> 
         <pay:PaymentAccountNumber>5330385000000237</pay:PaymentAccountNumber> 
         <pay:PaymentAmount>1.00</pay:PaymentAmount> 
         <pay:ExpirationDate>2015-07-10</pay:ExpirationDate> 
         <pay:MerchantName>ETM TEST</pay:MerchantName> 
         <pay:Comments>TEST</pay:Comments> 
         <!--0 to 20 repetitions:--> 
         <pay:CustomAttribute> 
            <pay:AttributeKey>TEST</pay:AttributeKey> 
            <pay:AttributeValue>123456</pay:AttributeValue> 
         </pay:CustomAttribute> 
      </pay:PaymentPlusCreateRequest> 
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:PaymentPlusCreateResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:USBRequestID>330750703429375750000000000000000000</pay:USBRequestID>
         <pay:ReferenceID>q1YivWy7ts</pay:ReferenceID>
         <pay:PaymentType>PA</pay:PaymentType>
         <pay:ControlNumber>2hKpY3z</pay:ControlNumber>
         <pay:PaymentAccountNumber>5330385000000237</pay:PaymentAccountNumber>
         <pay:ExpirationDate>2015-07-10</pay:ExpirationDate>
         <pay:MerchantName>UFdbYtn5bzbiPXV</pay:MerchantName>
         <pay:SUAAccountNumber>q4BbQn4Wjk1YYKV1</pay:SUAAccountNumber>
         <pay:SUAExpirationDate>07-2016</pay:SUAExpirationDate>
      </pay:PaymentPlusCreateResponse>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* ClientMsgID: Copied from the request message
* USBRequestID: Randomly generated numeric field with a length of 36
* ReferenceID: Randomly generated alpha-numeric field with a length of 10
* PaymentType: Copied from the request message
* ControlNumber: Randomly generated alpha-numeric field with a length of 16
* PaymentAccountNumber: Copied from the request message
* ExpirationDate: Copied from the request message
* MerchantName: Randomly generated alpha-numeric field with a length of 16
* SUAAccountNumber: Randomly generated alpha-numeric field with a length of 16
* SUAExpirationDate: Randomly generated date field between now and the year 2026

### Request CSC

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0" xmlns:pay1="http://www.usbank.com/PaymentPlusments/ws/schemas/PaymentPluswebservice">
   <soapenv:Header>
      <pay:PaymentPlusCSCHeader>
         <pay:TransactionIdentifier>?</pay:TransactionIdentifier>
         <!--Optional:-->
         <pay:MessageIdentifier>?</pay:MessageIdentifier>
         <!--Optional:-->
         <pay:ProviderInfo>?</pay:ProviderInfo>
      </pay:PaymentPlusCSCHeader>
      <pay1:userNameToken>?</pay1:userNameToken>
   </soapenv:Header>
   <soapenv:Body>
      <pay:PaymentPlusCSCRequest>
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:OrgShortName>ADMIN7</pay:OrgShortName>
         <pay:ReferenceID>q1YivWy7ts</pay:ReferenceID>
      </pay:PaymentPlusCSCRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:PaymentPlusCSCResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:USBRequestID>304128123796807200000000000000000000</pay:USBRequestID>
         <pay:ReferenceID>w2XEjKa0Kn</pay:ReferenceID>
         <pay:SecurityCode>6229</pay:SecurityCode>
      </pay:PaymentPlusCSCResponse>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* ClientMsgID: Copied from the request message
* USBRequestID: Randomly generated numeric field with a length of 36
* ReferenceID: Randomly generated alpha-numeric field with a length of 10
* SecurityCode: Randomly generated numeric field with a length of 4

### SUA Activation

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0" xmlns:pay1="http://www.usbank.com/PaymentPlusments/ws/schemas/PaymentPluswebservice">
   <soapenv:Header>
      <pay:SUAServiceHeader>
         <pay:TransactionIdentifier>?</pay:TransactionIdentifier>
         <!--Optional:-->
         <pay:MessageIdentifier>?</pay:MessageIdentifier>
         <!--Optional:-->
         <pay:ProviderInfo>?</pay:ProviderInfo>
      </pay:SUAServiceHeader>
      <pay1:userNameToken>?</pay1:userNameToken>
   </soapenv:Header>
   <soapenv:Body>
      <pay:SUAActivateRequest>
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:OrgShortName>ADMIN7</pay:OrgShortName>
         <pay:RequestDate>2015-07-20</pay:RequestDate>
         <pay:PaymentAccountNumber>5330385000000237</pay:PaymentAccountNumber>
         <pay:RequestedAmount>100.00</pay:RequestedAmount>
      </pay:SUAActivateRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:SUAActivateResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:USBRequestID>512756113365536000000000000000000000</pay:USBRequestID>
         <pay:SUAReferenceID>6KN4HBJSnmpj</pay:SUAReferenceID>
         <pay:SUAAccountNumber>47eM4WGSo8xqOydf</pay:SUAAccountNumber>
         <pay:SUAExpirationDate>08-2016</pay:SUAExpirationDate>
      </pay:SUAActivateResponse>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* ClientMsgID: Copied from the request message
* USBRequestID: Randomly generated numeric field with a length of 36
* SUAReferenceID: Randomly generated alpha-numeric field with a length of 12
* SUAAccountNumber: Randomly generated alpha-numeric field with a length of 16
* SUAExpirationDate: Randomly generated date field between now and the year 2026

### SUA Modification

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0" xmlns:pay1="http://www.usbank.com/PaymentPlusments/ws/schemas/PaymentPluswebservice">
   <soapenv:Header>
      <pay:SUAServiceHeader>
         <pay:TransactionIdentifier>?</pay:TransactionIdentifier>
         <!--Optional:-->
         <pay:MessageIdentifier>?</pay:MessageIdentifier>
         <!--Optional:-->
         <pay:ProviderInfo>?</pay:ProviderInfo>
      </pay:SUAServiceHeader>
      <pay1:userNameToken>?</pay1:userNameToken>
   </soapenv:Header>
   <soapenv:Body>
      <pay:SUAModifyRequest>
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:OrgShortName>ADMIN7</pay:OrgShortName>
         <pay:PaymentType>PS</pay:PaymentType>
         <pay:RequestDate>2015-07-20</pay:RequestDate>
         <pay:ControlNumber>?</pay:ControlNumber>
         <pay:SUAReferenceID>6KN4HBJSnmpj</pay:SUAReferenceID>
         <pay:PaymentAmount>100.00</pay:PaymentAmount>
         <pay:ExpirationDate>2016-08-20</pay:ExpirationDate>
         <pay:MerchantName>?</pay:MerchantName>
         <!--Optional:-->
         <pay:SupplierID>?</pay:SupplierID>
         <!--Optional:-->
         <pay:SupplierPostalCode>68028</pay:SupplierPostalCode>
         <!--Optional:-->
         <pay:Notes>?</pay:Notes>
         <!--0 to 20 repetitions:-->
         <pay:CustomAttribute>
            <pay:AttributeKey>?</pay:AttributeKey>
            <pay:AttributeValue>?</pay:AttributeValue>
         </pay:CustomAttribute>
      </pay:SUAModifyRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:SUAModifyResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:USBRequestID>505410851013440800000000000000000000</pay:USBRequestID>
         <pay:ReferenceID>LnUI5R8Br3</pay:ReferenceID>
         <pay:PaymentType>PS</pay:PaymentType>
         <pay:ControlNumber>rYjT6</pay:ControlNumber>
         <pay:SUAReferenceID>6KN4HBJSnmpj</pay:SUAReferenceID>
         <pay:ExpirationDate>2016-08-20</pay:ExpirationDate>
         <pay:MerchantName>?</pay:MerchantName>
      </pay:SUAModifyResponse>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* ClientMsgID: Copied from the request message
* USBRequestID: Randomly generated numeric field with a length of 36
* ReferenceID: Randomly generated alpha-numeric field with a length of 10
* PaymentType: Copied from the request message
* ControlNumber: Randomly generated alpha-numeric field with a length of 16
* SUAReferenceID: Randomly generated alpha-numeric field with a length of 12
* ExpirationDate: Copied from the request message
* MerchantName: Randomly generated alpha-numeric field with a length of 16

### SUA Request CSC

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0" xmlns:pay1="http://www.usbank.com/PaymentPlusments/ws/schemas/PaymentPluswebservice">
   <soapenv:Header>
      <pay:SUAServiceHeader>
         <pay:TransactionIdentifier>?</pay:TransactionIdentifier>
         <!--Optional:-->
         <pay:MessageIdentifier>?</pay:MessageIdentifier>
         <!--Optional:-->
         <pay:ProviderInfo>?</pay:ProviderInfo>
      </pay:SUAServiceHeader>
      <pay1:userNameToken>?</pay1:userNameToken>
   </soapenv:Header>
   <soapenv:Body>
      <pay:SUACSCRequest>
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:OrgShortName>ADMIN7</pay:OrgShortName>
         <pay:SUAReferenceID>6KN4HBJSnmpj</pay:SUAReferenceID>
      </pay:SUACSCRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:SUACSCResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>WEBSERVICEPRJ0000000000001213SJMARSH</pay:ClientMsgID>
         <pay:USBRequestID>452681787153785900000000000000000000</pay:USBRequestID>
         <pay:SUAReferenceID>6KN4HBJSnmpj</pay:SUAReferenceID>
         <pay:SecurityCode>73685</pay:SecurityCode>
      </pay:SUACSCResponse>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* ClientMsgID: Copied from the request message
* USBRequestID: Randomly generated numeric field with a length of 36
* SUAReferenceID: Randomly generated alpha-numeric field with a length of 12
* SecurityCode: Randomly generated numeric field with a length of 4

## HR Integration