# CPS
## Payment Plus
### Create Payments
#### Request Message
Example SOAP request message:
#### Response Message
Example SOAP response message:
'''
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <pay:PaymentPlusInterface xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0"/>
   </soap:Header>
   <soap:Body>
      <pay:PaymentPlusCreateResponse xmlns:pay="http://soa.usbank.com/PaymentPlus/PaymentPlusInterface_V_1_0">
         <pay:ClientMsgID>ClientMsgID</pay:ClientMsgID>
         <pay:USBRequestID>678345359013836800000000000000000000</pay:USBRequestID>
         <pay:ReferenceID>B1IIfVrZrE</pay:ReferenceID>
         <pay:PaymentType>PaymentType</pay:PaymentType>
         <pay:ControlNumber>2xo8lVBMc1cwcOPD</pay:ControlNumber>
         <pay:PaymentAccountNumber>PaymentAccountNumber</pay:PaymentAccountNumber>
         <pay:ExpirationDate>ExpirationDate</pay:ExpirationDate>
         <pay:MerchantName>Qpr1jPbAJQYVqthT</pay:MerchantName>
         <pay:SUAAccountNumber>UO0Um0tWPBwfHbFQ</pay:SUAAccountNumber>
         <pay:SUAExpirationDate>8/1/2022</pay:SUAExpirationDate>
      </pay:PaymentPlusCreateResponse>
   </soap:Body>
</soap:Envelope>
'''
#### Implementation
Flow chart:
Response Field Details:
-ClientMsgID: Copied from the request message
-USBRequestID: Randomly generated numeric field with a length of 36
-ReferenceID: Randomly generated alpha-numeric field with a length of 10
-PaymentType: Copied from the request message
-ControlNumber: Randomly generated alpha-numeric field with a length of 16
-PaymentAccountNumber: Copied from the request message
-ExpirationDate: Copied from the request message
-MerchantName: Randomly generated alpha-numeric field with a length of 16
-SUAAccountNumber: Randomly generated alpha-numeric field with a length of 16
-SUAExpirationDate: Randomly generated date field between now and the year 2026

### Request CSC

#### Request Message

#### Response Message

#### Implementation

### SUA Activation

#### Request Message

#### Response Message

#### Implementation

### SUA Modification

#### Request Message

#### Response Message

#### Implementation

### SUA Request CSC

#### Request Message

#### Response Message

#### Implementation

## HR Integration