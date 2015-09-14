# CPS
## HR Integraion
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

### Card Holder Account Setup

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/OSB/Schema.xsd" xmlns:sch1="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
   <soapenv:Header>
      <sch:userNameToken>?</sch:userNameToken>
      <sch1:USBSOAPHeader>
         <sch1:TransactionIdentifier>?</sch1:TransactionIdentifier>
         <sch1:ClientShortName>?</sch1:ClientShortName>
         <sch1:RequestDate>?</sch1:RequestDate>
      </sch1:USBSOAPHeader>
   </soapenv:Header>
   <soapenv:Body>
      <sch1:CardholderMaintenanceRequest>
         <sch1:CardholderAccountIdentifier>
            <sch1:CardholderAccountID>?</sch1:CardholderAccountID>
         </sch1:CardholderAccountIdentifier>
         <!--Optional:-->
         <sch1:Demographics>
            <!--Optional:-->
            <sch1:PersonalInfo>
               <!--Optional:-->
               <sch1:IDNumber>?</sch1:IDNumber>
               <!--Optional:-->
               <sch1:TaxExemptNumber>?</sch1:TaxExemptNumber>
               <!--Optional:-->
               <sch1:CardholderCategory>?</sch1:CardholderCategory>
            </sch1:PersonalInfo>
            <!--Optional:-->
            <sch1:OptionalFields>
               <!--Optional:-->
               <sch1:OptionalField1>?</sch1:OptionalField1>
               <!--Optional:-->
               <sch1:OptionalField2>?</sch1:OptionalField2>
               <!--Optional:-->
               <sch1:OptionalField3>?</sch1:OptionalField3>
            </sch1:OptionalFields>
            <!--Optional:-->
            <sch1:Address>
               <sch1:AddressLine1>?</sch1:AddressLine1>
               <!--Optional:-->
               <sch1:AddressLine2>?</sch1:AddressLine2>
               <sch1:City>?</sch1:City>
               <sch1:StateOrProvince>?</sch1:StateOrProvince>
               <sch1:Country>?</sch1:Country>
               <sch1:PostalCode>?</sch1:PostalCode>
            </sch1:Address>
            <!--Optional:-->
            <sch1:ContactInfo>
               <!--Optional:-->
               <sch1:HomePhone>?</sch1:HomePhone>
               <!--Optional:-->
               <sch1:WorkPhone>?</sch1:WorkPhone>
               <!--Optional:-->
               <sch1:AlternatePhone>?</sch1:AlternatePhone>
               <!--Optional:-->
               <sch1:Fax>?</sch1:Fax>
               <!--Optional:-->
               <sch1:EmailAddress>?</sch1:EmailAddress>
            </sch1:ContactInfo>
            <!--Optional:-->
            <sch1:DemographicComments>?</sch1:DemographicComments>
         </sch1:Demographics>
         <!--Optional:-->
         <sch1:AccountInfo>
            <!--Optional:-->
            <sch1:ReorderChecks>?</sch1:ReorderChecks>
            <!--Optional:-->
            <sch1:ChecksValidation>
               <!--You have a CHOICE of the next 2 items at this level-->
               <sch1:ChecksValidDollarAmt>?</sch1:ChecksValidDollarAmt>
               <sch1:ChecksValidNoOfDays>?</sch1:ChecksValidNoOfDays>
            </sch1:ChecksValidation>
            <!--Optional:-->
            <sch1:PlasticReoder>?</sch1:PlasticReoder>
            <!--Optional:-->
            <sch1:PINReorder>?</sch1:PINReorder>
            <!--Optional:-->
            <sch1:MailToPlanAdministrator>?</sch1:MailToPlanAdministrator>
            <!--Optional:-->
            <sch1:PlasticLanguage>?</sch1:PlasticLanguage>
            <!--Optional:-->
            <sch1:RegionCode>?</sch1:RegionCode>
            <!--Optional:-->
            <sch1:AccountStatus>?</sch1:AccountStatus>
            <!--Optional:-->
            <sch1:OrganizationName>?</sch1:OrganizationName>
            <!--Optional:-->
            <sch1:ReportingHierarchy>
               <!--Optional:-->
               <sch1:ReportingLevel1>?</sch1:ReportingLevel1>
               <!--Optional:-->
               <sch1:ReportingLevel2>?</sch1:ReportingLevel2>
               <!--Optional:-->
               <sch1:ReportingLevel3>?</sch1:ReportingLevel3>
               <!--Optional:-->
               <sch1:ReportingLevel4>?</sch1:ReportingLevel4>
               <!--Optional:-->
               <sch1:ReportingLevel5>?</sch1:ReportingLevel5>
               <!--Optional:-->
               <sch1:ReportingLevel6>?</sch1:ReportingLevel6>
               <!--Optional:-->
               <sch1:ReportingLevel7>?</sch1:ReportingLevel7>
            </sch1:ReportingHierarchy>
            <!--Optional:-->
            <sch1:Dates>
               <!--Optional:-->
               <sch1:ExpiryDate>?</sch1:ExpiryDate>
               <!--Optional:-->
               <sch1:TempAuthStartDate>?</sch1:TempAuthStartDate>
               <!--Optional:-->
               <sch1:TempAuthEndDate>?</sch1:TempAuthEndDate>
            </sch1:Dates>
            <!--Optional:-->
            <sch1:AuthorizedUser>
               <sch1:FirstNameAuthUser>?</sch1:FirstNameAuthUser>
               <sch1:LastNameAuthUser>?</sch1:LastNameAuthUser>
               <!--Optional:-->
               <sch1:MiddleInitialAuthUser>?</sch1:MiddleInitialAuthUser>
            </sch1:AuthorizedUser>
            <!--Optional:-->
            <sch1:AccountInfoComments>?</sch1:AccountInfoComments>
         </sch1:AccountInfo>
         <!--Optional:-->
         <sch1:HierarchyNodeMovement>
            <sch1:ProcessingHierarchy>
               <sch1:BankNumber>?</sch1:BankNumber>
               <sch1:AgentNumber>?</sch1:AgentNumber>
               <sch1:CompanyNumber>?</sch1:CompanyNumber>
            </sch1:ProcessingHierarchy>
            <!--Optional:-->
            <sch1:ProcessingSubHierarchy>
               <sch1:DivisionNumber>?</sch1:DivisionNumber>
               <sch1:DepartmentNumber>?</sch1:DepartmentNumber>
            </sch1:ProcessingSubHierarchy>
            <!--Optional:-->
            <sch1:ReportingHierarchy>
               <!--Optional:-->
               <sch1:ReportingLevel1>?</sch1:ReportingLevel1>
               <!--Optional:-->
               <sch1:ReportingLevel2>?</sch1:ReportingLevel2>
               <!--Optional:-->
               <sch1:ReportingLevel3>?</sch1:ReportingLevel3>
               <!--Optional:-->
               <sch1:ReportingLevel4>?</sch1:ReportingLevel4>
               <!--Optional:-->
               <sch1:ReportingLevel5>?</sch1:ReportingLevel5>
               <!--Optional:-->
               <sch1:ReportingLevel6>?</sch1:ReportingLevel6>
               <!--Optional:-->
               <sch1:ReportingLevel7>?</sch1:ReportingLevel7>
            </sch1:ReportingHierarchy>
            <!--Optional:-->
            <sch1:DefaultAccountingCode>
               <!--0 to 150 repetitions:-->
               <sch1:AccountingCodeSegment>
                  <sch1:SegmentName>?</sch1:SegmentName>
                  <sch1:SegmentValue>?</sch1:SegmentValue>
               </sch1:AccountingCodeSegment>
            </sch1:DefaultAccountingCode>
            <!--Optional:-->
            <sch1:AccountInfoComments>?</sch1:AccountInfoComments>
         </sch1:HierarchyNodeMovement>
         <!--Optional:-->
         <sch1:DefaultAccountingCode>
            <!--0 to 150 repetitions:-->
            <sch1:AccountingCodeSegment>
               <sch1:SegmentName>?</sch1:SegmentName>
               <sch1:SegmentValue>?</sch1:SegmentValue>
            </sch1:AccountingCodeSegment>
            <!--Optional:-->
            <sch1:DACComments>?</sch1:DACComments>
         </sch1:DefaultAccountingCode>
         <!--Optional:-->
         <sch1:AuthLimits>
            <!--Optional:-->
            <sch1:ReferToParent>
               <!--Optional:-->
               <sch1:MerchantAuthorizationControls>?</sch1:MerchantAuthorizationControls>
               <!--Optional:-->
               <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
               <!--Optional:-->
               <sch1:Velocity>?</sch1:Velocity>
            </sch1:ReferToParent>
            <!--Optional:-->
            <sch1:AuthLimits>
               <!--Optional:-->
               <sch1:CreditLimit>?</sch1:CreditLimit>
               <!--Optional:-->
               <sch1:PercentCash>?</sch1:PercentCash>
               <!--Optional:-->
               <sch1:QuarterlyLimit>?</sch1:QuarterlyLimit>
               <!--Optional:-->
               <sch1:QuarterlyTransLimit>?</sch1:QuarterlyTransLimit>
               <!--Optional:-->
               <sch1:YearlyLimit>?</sch1:YearlyLimit>
               <!--Optional:-->
               <sch1:YearlyTransLimit>?</sch1:YearlyTransLimit>
            </sch1:AuthLimits>
            <!--Optional:-->
            <sch1:CommonAuthLimits>
               <!--Optional:-->
               <sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:DailyLimit>?</sch1:DailyLimit>
                  <!--Optional:-->
                  <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                  <!--Optional:-->
                  <sch1:CycleLimit>?</sch1:CycleLimit>
                  <!--Optional:-->
                  <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                  <!--Optional:-->
                  <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                  <!--Optional:-->
                  <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
               </sch1:BaseAuthLimits>
               <!--Optional:-->
               <sch1:Velocity>
                  <!--Optional:-->
                  <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                  <!--Optional:-->
                  <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                  <!--Optional:-->
                  <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                  <!--Optional:-->
                  <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                  <!--Optional:-->
                  <sch1:RefreshToDate>?</sch1:RefreshToDate>
               </sch1:Velocity>
            </sch1:CommonAuthLimits>
            <!--0 to 9 repetitions:-->
            <sch1:MerchantAuthControls>
               <sch1:Action>?</sch1:Action>
               <sch1:Name>?</sch1:Name>
               <sch1:AuthAction>?</sch1:AuthAction>
               <sch1:ReferToParent>
                  <!--Optional:-->
                  <sch1:MerchantAuthorizationControls>?</sch1:MerchantAuthorizationControls>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:Velocity>?</sch1:Velocity>
               </sch1:ReferToParent>
               <sch1:MerchantLimits>
                  <!--Optional:-->
                  <sch1:BaseAuthLimits>
                     <!--Optional:-->
                     <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                     <!--Optional:-->
                     <sch1:DailyLimit>?</sch1:DailyLimit>
                     <!--Optional:-->
                     <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                     <!--Optional:-->
                     <sch1:CycleLimit>?</sch1:CycleLimit>
                     <!--Optional:-->
                     <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                     <!--Optional:-->
                     <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                     <!--Optional:-->
                     <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
                  </sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:Velocity>
                     <!--Optional:-->
                     <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                     <!--Optional:-->
                     <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                     <!--Optional:-->
                     <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                     <!--Optional:-->
                     <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                     <!--Optional:-->
                     <sch1:RefreshToDate>?</sch1:RefreshToDate>
                  </sch1:Velocity>
               </sch1:MerchantLimits>
            </sch1:MerchantAuthControls>
            <!--Optional:-->
            <sch1:AuthLimitsComments>?</sch1:AuthLimitsComments>
         </sch1:AuthLimits>
      </sch1:CardholderMaintenanceRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <sch:HRIntegrationSOAP xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd"/>
   </soap:Header>
   <soap:Body>
      <sch:CardholderMaintenanceReply xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
         <sch:RequestStatus>
            <sch:USBRequestID>422322664905418400000000000000000000</sch:USBRequestID>
            <sch:Status>Processing</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>768755555453</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
      </sch:CardholderMaintenanceReply>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* USBRequestID: Randomly generated numeric field with a length of 36
* Status: Randomly picked from Processing, Complete, Failure, Unknown Request, Indeterminate
* Message: Always returns 'Mock Service Created'
* AccountID: Randomly generated numeric field with a length of 12

### Maintain Cardholder Account

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/OSB/Schema.xsd" xmlns:sch1="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
   <soapenv:Header>
      <sch:userNameToken>?</sch:userNameToken>
      <sch1:USBSOAPHeader>
         <sch1:TransactionIdentifier>?</sch1:TransactionIdentifier>
         <sch1:ClientShortName>?</sch1:ClientShortName>
         <sch1:RequestDate>?</sch1:RequestDate>
      </sch1:USBSOAPHeader>
   </soapenv:Header>
   <soapenv:Body>
      <sch1:CardholderSetupRequest>
         <sch1:ManagingAccountIdentifier>
            <!--You have a CHOICE of the next 2 items at this level-->
            <sch1:ManagingAccountID>?</sch1:ManagingAccountID>
            <sch1:ProcessingHierarchy>
               <sch1:BankNumber>?</sch1:BankNumber>
               <sch1:AgentNumber>?</sch1:AgentNumber>
               <sch1:CompanyNumber>?</sch1:CompanyNumber>
            </sch1:ProcessingHierarchy>
         </sch1:ManagingAccountIdentifier>
         <sch1:Demographics>
            <sch1:SetupName>
               <sch1:FirstName>?</sch1:FirstName>
               <sch1:LastName>?</sch1:LastName>
               <!--Optional:-->
               <sch1:MiddleInitial>?</sch1:MiddleInitial>
            </sch1:SetupName>
            <sch1:PersonalInfo>
               <!--Optional:-->
               <sch1:DateOfBirth>?</sch1:DateOfBirth>
               <!--Optional:-->
               <sch1:IDNumber>?</sch1:IDNumber>
               <!--Optional:-->
               <sch1:SSN>?</sch1:SSN>
               <!--Optional:-->
               <sch1:TaxExemptNumber>?</sch1:TaxExemptNumber>
               <!--Optional:-->
               <sch1:CardholderCategory>?</sch1:CardholderCategory>
            </sch1:PersonalInfo>
            <sch1:OptionalFields>
               <!--Optional:-->
               <sch1:OptionalField1>?</sch1:OptionalField1>
               <!--Optional:-->
               <sch1:OptionalField2>?</sch1:OptionalField2>
               <!--Optional:-->
               <sch1:OptionalField3>?</sch1:OptionalField3>
            </sch1:OptionalFields>
            <sch1:Address>
               <sch1:AddressLine1>?</sch1:AddressLine1>
               <!--Optional:-->
               <sch1:AddressLine2>?</sch1:AddressLine2>
               <sch1:City>?</sch1:City>
               <sch1:StateOrProvince>?</sch1:StateOrProvince>
               <sch1:Country>?</sch1:Country>
               <sch1:PostalCode>?</sch1:PostalCode>
            </sch1:Address>
            <sch1:ContactInfo>
               <!--Optional:-->
               <sch1:HomePhone>?</sch1:HomePhone>
               <sch1:WorkPhone>?</sch1:WorkPhone>
               <!--Optional:-->
               <sch1:AlternatePhone>?</sch1:AlternatePhone>
               <!--Optional:-->
               <sch1:Fax>?</sch1:Fax>
               <!--Optional:-->
               <sch1:EmailAddress>?</sch1:EmailAddress>
            </sch1:ContactInfo>
            <!--Optional:-->
            <sch1:DemographicComments>?</sch1:DemographicComments>
         </sch1:Demographics>
         <sch1:AccountInfo>
            <sch1:Checks>?</sch1:Checks>
            <!--Optional:-->
            <sch1:ChecksValidation>
               <!--You have a CHOICE of the next 2 items at this level-->
               <sch1:ChecksValidDollarAmt>?</sch1:ChecksValidDollarAmt>
               <sch1:ChecksValidNoOfDays>?</sch1:ChecksValidNoOfDays>
            </sch1:ChecksValidation>
            <sch1:Plastic>?</sch1:Plastic>
            <!--Optional:-->
            <sch1:MailToPlanAdministrator>?</sch1:MailToPlanAdministrator>
            <!--Optional:-->
            <sch1:PlasticLanguage>?</sch1:PlasticLanguage>
            <!--Optional:-->
            <sch1:RegionCode>?</sch1:RegionCode>
            <!--Optional:-->
            <sch1:CycleDay>?</sch1:CycleDay>
            <!--Optional:-->
            <sch1:OrganizationName>?</sch1:OrganizationName>
            <!--Optional:-->
            <sch1:ReportingHierarchy>
               <!--Optional:-->
               <sch1:ReportingLevel1>?</sch1:ReportingLevel1>
               <!--Optional:-->
               <sch1:ReportingLevel2>?</sch1:ReportingLevel2>
               <!--Optional:-->
               <sch1:ReportingLevel3>?</sch1:ReportingLevel3>
               <!--Optional:-->
               <sch1:ReportingLevel4>?</sch1:ReportingLevel4>
               <!--Optional:-->
               <sch1:ReportingLevel5>?</sch1:ReportingLevel5>
               <!--Optional:-->
               <sch1:ReportingLevel6>?</sch1:ReportingLevel6>
               <!--Optional:-->
               <sch1:ReportingLevel7>?</sch1:ReportingLevel7>
            </sch1:ReportingHierarchy>
            <sch1:ProductName>?</sch1:ProductName>
            <!--Optional:-->
            <sch1:Dates>
               <!--Optional:-->
               <sch1:ExpiryDate>?</sch1:ExpiryDate>
               <!--Optional:-->
               <sch1:TempAuthStartDate>?</sch1:TempAuthStartDate>
               <!--Optional:-->
               <sch1:TempAuthEndDate>?</sch1:TempAuthEndDate>
            </sch1:Dates>
            <!--Optional:-->
            <sch1:AlternateAddress>
               <sch1:AddressLine1>?</sch1:AddressLine1>
               <!--Optional:-->
               <sch1:AddressLine2>?</sch1:AddressLine2>
               <sch1:City>?</sch1:City>
               <sch1:StateOrProvince>?</sch1:StateOrProvince>
               <sch1:Country>?</sch1:Country>
               <sch1:PostalCode>?</sch1:PostalCode>
            </sch1:AlternateAddress>
            <!--Optional:-->
            <sch1:AuthorizedUser>
               <sch1:FirstNameAuthUser>?</sch1:FirstNameAuthUser>
               <sch1:LastNameAuthUser>?</sch1:LastNameAuthUser>
               <!--Optional:-->
               <sch1:MiddleInitialAuthUser>?</sch1:MiddleInitialAuthUser>
            </sch1:AuthorizedUser>
            <!--Optional:-->
            <sch1:AccountInfoComments>?</sch1:AccountInfoComments>
         </sch1:AccountInfo>
         <sch1:DefaultAccountingCode>
            <!--0 to 150 repetitions:-->
            <sch1:AccountingCodeSegment>
               <sch1:SegmentName>?</sch1:SegmentName>
               <sch1:SegmentValue>?</sch1:SegmentValue>
            </sch1:AccountingCodeSegment>
            <!--Optional:-->
            <sch1:DACComments>?</sch1:DACComments>
         </sch1:DefaultAccountingCode>
         <!--Optional:-->
         <sch1:AuthLimits>
            <sch1:ReferToParent>
               <!--Optional:-->
               <sch1:MerchantAuthorizationControls>?</sch1:MerchantAuthorizationControls>
               <!--Optional:-->
               <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
               <!--Optional:-->
               <sch1:Velocity>?</sch1:Velocity>
            </sch1:ReferToParent>
            <sch1:AuthLimits>
               <!--Optional:-->
               <sch1:CreditLimit>?</sch1:CreditLimit>
               <!--Optional:-->
               <sch1:PercentCash>?</sch1:PercentCash>
               <!--Optional:-->
               <sch1:QuarterlyLimit>?</sch1:QuarterlyLimit>
               <!--Optional:-->
               <sch1:QuarterlyTransLimit>?</sch1:QuarterlyTransLimit>
               <!--Optional:-->
               <sch1:YearlyLimit>?</sch1:YearlyLimit>
               <!--Optional:-->
               <sch1:YearlyTransLimit>?</sch1:YearlyTransLimit>
            </sch1:AuthLimits>
            <sch1:CommonAuthLimits>
               <!--Optional:-->
               <sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:DailyLimit>?</sch1:DailyLimit>
                  <!--Optional:-->
                  <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                  <!--Optional:-->
                  <sch1:CycleLimit>?</sch1:CycleLimit>
                  <!--Optional:-->
                  <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                  <!--Optional:-->
                  <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                  <!--Optional:-->
                  <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
               </sch1:BaseAuthLimits>
               <!--Optional:-->
               <sch1:Velocity>
                  <!--Optional:-->
                  <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                  <!--Optional:-->
                  <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                  <!--Optional:-->
                  <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                  <!--Optional:-->
                  <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                  <!--Optional:-->
                  <sch1:RefreshToDate>?</sch1:RefreshToDate>
               </sch1:Velocity>
            </sch1:CommonAuthLimits>
            <!--0 to 9 repetitions:-->
            <sch1:MerchantAuthControls>
               <sch1:Name>?</sch1:Name>
               <sch1:AuthAction>?</sch1:AuthAction>
               <sch1:ReferToParent>
                  <!--Optional:-->
                  <sch1:MerchantAuthorizationControls>?</sch1:MerchantAuthorizationControls>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:Velocity>?</sch1:Velocity>
               </sch1:ReferToParent>
               <sch1:MerchantLimits>
                  <!--Optional:-->
                  <sch1:BaseAuthLimits>
                     <!--Optional:-->
                     <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                     <!--Optional:-->
                     <sch1:DailyLimit>?</sch1:DailyLimit>
                     <!--Optional:-->
                     <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                     <!--Optional:-->
                     <sch1:CycleLimit>?</sch1:CycleLimit>
                     <!--Optional:-->
                     <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                     <!--Optional:-->
                     <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                     <!--Optional:-->
                     <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
                  </sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:Velocity>
                     <!--Optional:-->
                     <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                     <!--Optional:-->
                     <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                     <!--Optional:-->
                     <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                     <!--Optional:-->
                     <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                     <!--Optional:-->
                     <sch1:RefreshToDate>?</sch1:RefreshToDate>
                  </sch1:Velocity>
               </sch1:MerchantLimits>
            </sch1:MerchantAuthControls>
            <!--Optional:-->
            <sch1:AuthLimitsComments>?</sch1:AuthLimitsComments>
         </sch1:AuthLimits>
      </sch1:CardholderSetupRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <sch:HRIntegrationSOAP xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd"/>
   </soap:Header>
   <soap:Body>
      <sch:CardholderSetupReply xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
         <sch:RequestStatus>
            <sch:USBRequestID>759579214440996500000000000000000000</sch:USBRequestID>
            <sch:Status>Failure</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>322625425494</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
      </sch:CardholderSetupReply>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* USBRequestID: Randomly generated numeric field with a length of 36
* Status: Randomly picked from Processing, Complete, Failure, Unknown Request, Indeterminate
* Message: Always returns 'Mock Service Created'
* AccountID: Randomly generated numeric field with a length of 12

### Maintain Setup Account

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/OSB/Schema.xsd" xmlns:sch1="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
   <soapenv:Header>
      <sch:userNameToken>?</sch:userNameToken>
      <sch1:USBSOAPHeader>
         <sch1:TransactionIdentifier>?</sch1:TransactionIdentifier>
         <sch1:ClientShortName>?</sch1:ClientShortName>
         <sch1:RequestDate>?</sch1:RequestDate>
      </sch1:USBSOAPHeader>
   </soapenv:Header>
   <soapenv:Body>
      <sch1:ManagingAccountSetupRequest>
         <sch1:Demographics>
            <sch1:SetupName>
               <sch1:FirstName>?</sch1:FirstName>
               <sch1:LastName>?</sch1:LastName>
               <!--Optional:-->
               <sch1:MiddleInitial>?</sch1:MiddleInitial>
            </sch1:SetupName>
            <sch1:PersonalInfo>
               <!--Optional:-->
               <sch1:DateOfBirth>?</sch1:DateOfBirth>
               <!--Optional:-->
               <sch1:IDNumber>?</sch1:IDNumber>
               <!--Optional:-->
               <sch1:TaxExemptNumber>?</sch1:TaxExemptNumber>
            </sch1:PersonalInfo>
            <sch1:OptionalFields>
               <!--Optional:-->
               <sch1:OptionalField1>?</sch1:OptionalField1>
               <!--Optional:-->
               <sch1:OptionalField2>?</sch1:OptionalField2>
               <!--Optional:-->
               <sch1:OptionalField3>?</sch1:OptionalField3>
            </sch1:OptionalFields>
            <sch1:Address>
               <sch1:AddressLine1>?</sch1:AddressLine1>
               <!--Optional:-->
               <sch1:AddressLine2>?</sch1:AddressLine2>
               <sch1:City>?</sch1:City>
               <sch1:StateOrProvince>?</sch1:StateOrProvince>
               <sch1:Country>?</sch1:Country>
               <sch1:PostalCode>?</sch1:PostalCode>
            </sch1:Address>
            <sch1:ContactInfo>
               <!--Optional:-->
               <sch1:HomePhone>?</sch1:HomePhone>
               <sch1:WorkPhone>?</sch1:WorkPhone>
               <!--Optional:-->
               <sch1:AlternatePhone>?</sch1:AlternatePhone>
               <!--Optional:-->
               <sch1:Fax>?</sch1:Fax>
               <!--Optional:-->
               <sch1:EmailAddress>?</sch1:EmailAddress>
            </sch1:ContactInfo>
            <!--Optional:-->
            <sch1:DemographicComments>?</sch1:DemographicComments>
         </sch1:Demographics>
         <sch1:ProcessingHierarchy>
            <sch1:BankNumber>?</sch1:BankNumber>
            <sch1:AgentNumber>?</sch1:AgentNumber>
         </sch1:ProcessingHierarchy>
         <sch1:AccountInfo>
            <!--Optional:-->
            <sch1:OrganizationName>?</sch1:OrganizationName>
            <sch1:ProductName>?</sch1:ProductName>
            <!--Optional:-->
            <sch1:ReportingHierarchy>
               <!--Optional:-->
               <sch1:ReportingLevel1>?</sch1:ReportingLevel1>
               <!--Optional:-->
               <sch1:ReportingLevel2>?</sch1:ReportingLevel2>
               <!--Optional:-->
               <sch1:ReportingLevel3>?</sch1:ReportingLevel3>
               <!--Optional:-->
               <sch1:ReportingLevel4>?</sch1:ReportingLevel4>
               <!--Optional:-->
               <sch1:ReportingLevel5>?</sch1:ReportingLevel5>
               <!--Optional:-->
               <sch1:ReportingLevel6>?</sch1:ReportingLevel6>
               <!--Optional:-->
               <sch1:ReportingLevel7>?</sch1:ReportingLevel7>
            </sch1:ReportingHierarchy>
            <!--Optional:-->
            <sch1:Dates>
               <!--Optional:-->
               <sch1:TempAuthStartDate>?</sch1:TempAuthStartDate>
               <!--Optional:-->
               <sch1:TempAuthEndDate>?</sch1:TempAuthEndDate>
            </sch1:Dates>
            <!--Optional:-->
            <sch1:AccountInfoComments>?</sch1:AccountInfoComments>
         </sch1:AccountInfo>
         <!--Optional:-->
         <sch1:ExtractInfo>
            <!--Optional:-->
            <sch1:CostTransfer>?</sch1:CostTransfer>
            <!--Optional:-->
            <sch1:SendCostTransfer>?</sch1:SendCostTransfer>
            <!--Optional:-->
            <sch1:CreditInv>?</sch1:CreditInv>
            <!--Optional:-->
            <sch1:SendCreditInv>?</sch1:SendCreditInv>
            <!--Optional:-->
            <sch1:Inv>?</sch1:Inv>
            <!--Optional:-->
            <sch1:SendInv>?</sch1:SendInv>
            <!--Optional:-->
            <sch1:Oblig>?</sch1:Oblig>
            <!--Optional:-->
            <sch1:SendOblig>?</sch1:SendOblig>
            <!--Optional:-->
            <sch1:ExtractInfoComments>?</sch1:ExtractInfoComments>
         </sch1:ExtractInfo>
         <!--Optional:-->
         <sch1:ManagingAccountDefaultAccountingCode>
            <!--Optional:-->
            <sch1:AVC>?</sch1:AVC>
            <!--Optional:-->
            <sch1:ReallocMethod>?</sch1:ReallocMethod>
            <!--Optional:-->
            <sch1:DefaultAccountingCode>
               <!--0 to 150 repetitions:-->
               <sch1:AccountingCodeSegment>
                  <sch1:SegmentName>?</sch1:SegmentName>
                  <sch1:SegmentValue>?</sch1:SegmentValue>
               </sch1:AccountingCodeSegment>
            </sch1:DefaultAccountingCode>
            <!--Zero or more repetitions:-->
            <sch1:AACName>?</sch1:AACName>
            <!--Optional:-->
            <sch1:DACComments>?</sch1:DACComments>
         </sch1:ManagingAccountDefaultAccountingCode>
         <!--Optional:-->
         <sch1:AuthLimits>
            <sch1:AuthLimits>
               <!--Optional:-->
               <sch1:CreditLimit>?</sch1:CreditLimit>
               <!--Optional:-->
               <sch1:PercentCash>?</sch1:PercentCash>
               <!--Optional:-->
               <sch1:QuarterlyLimit>?</sch1:QuarterlyLimit>
               <!--Optional:-->
               <sch1:QuarterlyTransLimit>?</sch1:QuarterlyTransLimit>
               <!--Optional:-->
               <sch1:YearlyLimit>?</sch1:YearlyLimit>
               <!--Optional:-->
               <sch1:YearlyTransLimit>?</sch1:YearlyTransLimit>
            </sch1:AuthLimits>
            <sch1:CommonAuthLimits>
               <!--Optional:-->
               <sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:DailyLimit>?</sch1:DailyLimit>
                  <!--Optional:-->
                  <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                  <!--Optional:-->
                  <sch1:CycleLimit>?</sch1:CycleLimit>
                  <!--Optional:-->
                  <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                  <!--Optional:-->
                  <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                  <!--Optional:-->
                  <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
               </sch1:BaseAuthLimits>
               <!--Optional:-->
               <sch1:Velocity>
                  <!--Optional:-->
                  <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                  <!--Optional:-->
                  <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                  <!--Optional:-->
                  <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                  <!--Optional:-->
                  <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                  <!--Optional:-->
                  <sch1:RefreshToDate>?</sch1:RefreshToDate>
               </sch1:Velocity>
            </sch1:CommonAuthLimits>
            <!--0 to 9 repetitions:-->
            <sch1:MerchantAuthControls>
               <sch1:Name>?</sch1:Name>
               <sch1:AuthAction>?</sch1:AuthAction>
               <sch1:MerchantLimits>
                  <!--Optional:-->
                  <sch1:BaseAuthLimits>
                     <!--Optional:-->
                     <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                     <!--Optional:-->
                     <sch1:DailyLimit>?</sch1:DailyLimit>
                     <!--Optional:-->
                     <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                     <!--Optional:-->
                     <sch1:CycleLimit>?</sch1:CycleLimit>
                     <!--Optional:-->
                     <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                     <!--Optional:-->
                     <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                     <!--Optional:-->
                     <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
                  </sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:Velocity>
                     <!--Optional:-->
                     <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                     <!--Optional:-->
                     <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                     <!--Optional:-->
                     <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                     <!--Optional:-->
                     <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                     <!--Optional:-->
                     <sch1:RefreshToDate>?</sch1:RefreshToDate>
                  </sch1:Velocity>
               </sch1:MerchantLimits>
            </sch1:MerchantAuthControls>
            <!--Optional:-->
            <sch1:AuthLimitsComments>?</sch1:AuthLimitsComments>
         </sch1:AuthLimits>
      </sch1:ManagingAccountSetupRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <sch:HRIntegrationSOAP xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd"/>
   </soap:Header>
   <soap:Body>
      <sch:ManagingAccountSetupReply xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
         <sch:RequestStatus>
            <sch:USBRequestID>603745035487761900000000000000000000</sch:USBRequestID>
            <sch:Status>Failure</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>887850799147</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
      </sch:ManagingAccountSetupReply>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* USBRequestID: Randomly generated numeric field with a length of 36
* Status: Randomly picked from Processing, Complete, Failure, Unknown Request, Indeterminate
* Message: Always returns 'Mock Service Created'
* AccountID: Randomly generated numeric field with a length of 12

### Maintain Managing Account

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/OSB/Schema.xsd" xmlns:sch1="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
   <soapenv:Header>
      <sch:userNameToken>?</sch:userNameToken>
      <sch1:USBSOAPHeader>
         <sch1:TransactionIdentifier>?</sch1:TransactionIdentifier>
         <sch1:ClientShortName>?</sch1:ClientShortName>
         <sch1:RequestDate>?</sch1:RequestDate>
      </sch1:USBSOAPHeader>
   </soapenv:Header>
   <soapenv:Body>
      <sch1:ManagingAccountMaintenanceRequest>
         <sch1:ManagingAccountIdentifier>
            <!--You have a CHOICE of the next 2 items at this level-->
            <sch1:ManagingAccountID>?</sch1:ManagingAccountID>
            <sch1:ProcessingHierarchy>
               <sch1:BankNumber>?</sch1:BankNumber>
               <sch1:AgentNumber>?</sch1:AgentNumber>
               <sch1:CompanyNumber>?</sch1:CompanyNumber>
            </sch1:ProcessingHierarchy>
         </sch1:ManagingAccountIdentifier>
         <!--Optional:-->
         <sch1:Demographics>
            <!--Optional:-->
            <sch1:Name>
               <sch1:FirstName>?</sch1:FirstName>
               <sch1:LastName>?</sch1:LastName>
               <!--Optional:-->
               <sch1:MiddleInitial>?</sch1:MiddleInitial>
            </sch1:Name>
            <!--Optional:-->
            <sch1:PersonalInfo>
               <!--Optional:-->
               <sch1:DateOfBirth>?</sch1:DateOfBirth>
               <!--Optional:-->
               <sch1:IDNumber>?</sch1:IDNumber>
               <!--Optional:-->
               <sch1:TaxExemptNumber>?</sch1:TaxExemptNumber>
            </sch1:PersonalInfo>
            <!--Optional:-->
            <sch1:OptionalFields>
               <!--Optional:-->
               <sch1:OptionalField1>?</sch1:OptionalField1>
               <!--Optional:-->
               <sch1:OptionalField2>?</sch1:OptionalField2>
               <!--Optional:-->
               <sch1:OptionalField3>?</sch1:OptionalField3>
            </sch1:OptionalFields>
            <!--Optional:-->
            <sch1:Address>
               <sch1:AddressLine1>?</sch1:AddressLine1>
               <!--Optional:-->
               <sch1:AddressLine2>?</sch1:AddressLine2>
               <sch1:City>?</sch1:City>
               <sch1:StateOrProvince>?</sch1:StateOrProvince>
               <sch1:Country>?</sch1:Country>
               <sch1:PostalCode>?</sch1:PostalCode>
            </sch1:Address>
            <!--Optional:-->
            <sch1:ContactInfo>
               <!--Optional:-->
               <sch1:HomePhone>?</sch1:HomePhone>
               <!--Optional:-->
               <sch1:WorkPhone>?</sch1:WorkPhone>
               <!--Optional:-->
               <sch1:AlternatePhone>?</sch1:AlternatePhone>
               <!--Optional:-->
               <sch1:Fax>?</sch1:Fax>
               <!--Optional:-->
               <sch1:EmailAddress>?</sch1:EmailAddress>
            </sch1:ContactInfo>
            <!--Optional:-->
            <sch1:DemographicComments>?</sch1:DemographicComments>
         </sch1:Demographics>
         <!--Optional:-->
         <sch1:AccountInfo>
            <!--Optional:-->
            <sch1:AccountStatus>?</sch1:AccountStatus>
            <!--Optional:-->
            <sch1:OrganizationName>?</sch1:OrganizationName>
            <!--Optional:-->
            <sch1:ReportingHierarchy>
               <!--Optional:-->
               <sch1:ReportingLevel1>?</sch1:ReportingLevel1>
               <!--Optional:-->
               <sch1:ReportingLevel2>?</sch1:ReportingLevel2>
               <!--Optional:-->
               <sch1:ReportingLevel3>?</sch1:ReportingLevel3>
               <!--Optional:-->
               <sch1:ReportingLevel4>?</sch1:ReportingLevel4>
               <!--Optional:-->
               <sch1:ReportingLevel5>?</sch1:ReportingLevel5>
               <!--Optional:-->
               <sch1:ReportingLevel6>?</sch1:ReportingLevel6>
               <!--Optional:-->
               <sch1:ReportingLevel7>?</sch1:ReportingLevel7>
            </sch1:ReportingHierarchy>
            <!--Optional:-->
            <sch1:Dates>
               <!--Optional:-->
               <sch1:TempAuthStartDate>?</sch1:TempAuthStartDate>
               <!--Optional:-->
               <sch1:TempAuthEndDate>?</sch1:TempAuthEndDate>
            </sch1:Dates>
            <!--Optional:-->
            <sch1:AccountInfoComments>?</sch1:AccountInfoComments>
         </sch1:AccountInfo>
         <!--Optional:-->
         <sch1:ExtractInfo>
            <!--Optional:-->
            <sch1:CostTransfer>?</sch1:CostTransfer>
            <!--Optional:-->
            <sch1:SendCostTransfer>?</sch1:SendCostTransfer>
            <!--Optional:-->
            <sch1:CreditInv>?</sch1:CreditInv>
            <!--Optional:-->
            <sch1:SendCreditInv>?</sch1:SendCreditInv>
            <!--Optional:-->
            <sch1:Inv>?</sch1:Inv>
            <!--Optional:-->
            <sch1:SendInv>?</sch1:SendInv>
            <!--Optional:-->
            <sch1:Oblig>?</sch1:Oblig>
            <!--Optional:-->
            <sch1:SendOblig>?</sch1:SendOblig>
            <!--Optional:-->
            <sch1:ExtractInfoComments>?</sch1:ExtractInfoComments>
         </sch1:ExtractInfo>
         <!--Optional:-->
         <sch1:ManagingAccountDefaultAccountingCode>
            <!--Optional:-->
            <sch1:AVC>?</sch1:AVC>
            <!--Optional:-->
            <sch1:ReallocMethod>?</sch1:ReallocMethod>
            <!--Optional:-->
            <sch1:SiteCode>?</sch1:SiteCode>
            <!--Optional:-->
            <sch1:DefaultAccountingCode>
               <!--0 to 150 repetitions:-->
               <sch1:AccountingCodeSegment>
                  <sch1:SegmentName>?</sch1:SegmentName>
                  <sch1:SegmentValue>?</sch1:SegmentValue>
               </sch1:AccountingCodeSegment>
            </sch1:DefaultAccountingCode>
            <!--Optional:-->
            <sch1:FDAC>
               <!--0 to 150 repetitions:-->
               <sch1:AccountingCodeSegment>
                  <sch1:SegmentName>?</sch1:SegmentName>
                  <sch1:SegmentValue>?</sch1:SegmentValue>
               </sch1:AccountingCodeSegment>
            </sch1:FDAC>
            <!--Optional:-->
            <sch1:TDAC>
               <!--0 to 150 repetitions:-->
               <sch1:AccountingCodeSegment>
                  <sch1:SegmentName>?</sch1:SegmentName>
                  <sch1:SegmentValue>?</sch1:SegmentValue>
               </sch1:AccountingCodeSegment>
            </sch1:TDAC>
            <!--Optional:-->
            <sch1:AlternateAccountingCodes>
               <!--1 or more repetitions:-->
               <sch1:AlternateAccountingCode>
                  <sch1:AACName>?</sch1:AACName>
                  <sch1:Action>?</sch1:Action>
               </sch1:AlternateAccountingCode>
            </sch1:AlternateAccountingCodes>
            <!--Optional:-->
            <sch1:DACComments>?</sch1:DACComments>
         </sch1:ManagingAccountDefaultAccountingCode>
         <!--Optional:-->
         <sch1:AuthLimits>
            <!--Optional:-->
            <sch1:AuthLimits>
               <!--Optional:-->
               <sch1:CreditLimit>?</sch1:CreditLimit>
               <!--Optional:-->
               <sch1:PercentCash>?</sch1:PercentCash>
               <!--Optional:-->
               <sch1:QuarterlyLimit>?</sch1:QuarterlyLimit>
               <!--Optional:-->
               <sch1:QuarterlyTransLimit>?</sch1:QuarterlyTransLimit>
               <!--Optional:-->
               <sch1:YearlyLimit>?</sch1:YearlyLimit>
               <!--Optional:-->
               <sch1:YearlyTransLimit>?</sch1:YearlyTransLimit>
            </sch1:AuthLimits>
            <!--Optional:-->
            <sch1:CommonAuthLimits>
               <!--Optional:-->
               <sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                  <!--Optional:-->
                  <sch1:DailyLimit>?</sch1:DailyLimit>
                  <!--Optional:-->
                  <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                  <!--Optional:-->
                  <sch1:CycleLimit>?</sch1:CycleLimit>
                  <!--Optional:-->
                  <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                  <!--Optional:-->
                  <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                  <!--Optional:-->
                  <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
               </sch1:BaseAuthLimits>
               <!--Optional:-->
               <sch1:Velocity>
                  <!--Optional:-->
                  <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                  <!--Optional:-->
                  <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                  <!--Optional:-->
                  <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                  <!--Optional:-->
                  <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                  <!--Optional:-->
                  <sch1:RefreshToDate>?</sch1:RefreshToDate>
               </sch1:Velocity>
            </sch1:CommonAuthLimits>
            <!--0 to 9 repetitions:-->
            <sch1:MerchantAuthControls>
               <sch1:Action>?</sch1:Action>
               <sch1:Name>?</sch1:Name>
               <sch1:AuthAction>?</sch1:AuthAction>
               <sch1:MerchantLimits>
                  <!--Optional:-->
                  <sch1:BaseAuthLimits>
                     <!--Optional:-->
                     <sch1:SinglePurchaseLimit>?</sch1:SinglePurchaseLimit>
                     <!--Optional:-->
                     <sch1:DailyLimit>?</sch1:DailyLimit>
                     <!--Optional:-->
                     <sch1:DailyTransLimit>?</sch1:DailyTransLimit>
                     <!--Optional:-->
                     <sch1:CycleLimit>?</sch1:CycleLimit>
                     <!--Optional:-->
                     <sch1:CycleTransLimit>?</sch1:CycleTransLimit>
                     <!--Optional:-->
                     <sch1:MonthlyLimit>?</sch1:MonthlyLimit>
                     <!--Optional:-->
                     <sch1:MonthlyTransLimit>?</sch1:MonthlyTransLimit>
                  </sch1:BaseAuthLimits>
                  <!--Optional:-->
                  <sch1:Velocity>
                     <!--Optional:-->
                     <sch1:OtherDollarAmount>?</sch1:OtherDollarAmount>
                     <!--Optional:-->
                     <sch1:OtherTranLimit>?</sch1:OtherTranLimit>
                     <!--Optional:-->
                     <sch1:RefreshFromDate>?</sch1:RefreshFromDate>
                     <!--Optional:-->
                     <sch1:DaysInRefreshCycle>?</sch1:DaysInRefreshCycle>
                     <!--Optional:-->
                     <sch1:RefreshToDate>?</sch1:RefreshToDate>
                  </sch1:Velocity>
               </sch1:MerchantLimits>
            </sch1:MerchantAuthControls>
            <!--Optional:-->
            <sch1:AuthLimitsComments>?</sch1:AuthLimitsComments>
         </sch1:AuthLimits>
      </sch1:ManagingAccountMaintenanceRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <sch:HRIntegrationSOAP xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd"/>
   </soap:Header>
   <soap:Body>
      <sch:ManagingAccountMaintenanceReply xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
         <sch:RequestStatus>
            <sch:USBRequestID>530013533957185340000000000000000000</sch:USBRequestID>
            <sch:Status>Indeterminate</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>628069015107</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
      </sch:ManagingAccountMaintenanceReply>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* USBRequestID: Randomly generated numeric field with a length of 36
* Status: Randomly picked from Processing, Complete, Failure, Unknown Request, Indeterminate
* Message: Always returns 'Mock Service Created'
* AccountID: Randomly generated numeric field with a length of 12

### Status Inquiry

#### Request Message
Example SOAP request message:
```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/OSB/Schema.xsd" xmlns:sch1="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
   <soapenv:Header>
      <sch:userNameToken>?</sch:userNameToken>
      <sch1:USBSOAPHeader>
         <sch1:TransactionIdentifier>?</sch1:TransactionIdentifier>
         <sch1:ClientShortName>?</sch1:ClientShortName>
         <sch1:RequestDate>?</sch1:RequestDate>
      </sch1:USBSOAPHeader>
   </soapenv:Header>
   <soapenv:Body>
      <sch1:GetStatusRequest>
         <!--1 to 25 repetitions:-->
         <sch1:USBRequestID>559561896399713300000000000000000000</sch1:USBRequestID>
         <sch1:USBRequestID>445764276567815550000000000000000000</sch1:USBRequestID>
      </sch1:GetStatusRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

#### Response Message
Example SOAP response message:
```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Header>
      <sch:HRIntegrationSOAP xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd"/>
   </soap:Header>
   <soap:Body>
      <sch:GetStatusReply xmlns:sch="http://access.usbank.com/CPSEAI_HR_INTEG/Schema.xsd">
         <sch:RequestStatus>
            <sch:USBRequestID>559561896399713300000000000000000000</sch:USBRequestID>
            <sch:Status>Processing</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>525960103533</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
         <sch:RequestStatus>
            <sch:USBRequestID>445764276567815550000000000000000000</sch:USBRequestID>
            <sch:Status>Processing</sch:Status>
            <sch:Message>Mock Service Created</sch:Message>
            <sch:AccountData>
               <sch:AccountID>118510015263</sch:AccountID>
            </sch:AccountData>
         </sch:RequestStatus>
      </sch:GetStatusReply>
   </soap:Body>
</soap:Envelope>
```

#### Implementation
Response Field Details:
* USBRequestID: Randomly generated numeric field with a length of 36
* Status: Randomly picked from Processing, Complete, Failure, Unknown Request, Indeterminate
* Message: Always returns 'Mock Service Created'
* AccountID: Randomly generated numeric field with a length of 12

