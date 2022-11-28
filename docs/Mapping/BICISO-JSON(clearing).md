# RTC

## Mapping BICISO - JSON API

The following abbreviations are used for field length:  

* N = numeric characters
* X+N = Signed numeric
* AN = Includes spaces and the Alpha characters can be in upper or lower case
* ANS = AN as above plus special characters
* A ‘++’ before the length of the field, indicates a variable length field. This means that the field length needs to be specified at the start of the field.

## Clearing: Credit-transfer Request 

Field Name | Description | BICISO<br>Length/ <br> Other | Credit-transfer Request<br>to JSON  | Credit-transfer Request<br>from JSON |
--- | --- | --- | --- | --- 
P-1|Secondary Bitmap| ANS 16 | n/a | Built up as per BICISO rules  
P-3|Processing Code| N 6 |  |  
| | Position 1-2 | '42' = payment | creditTransferTransaction.<br>localInstrumentCode |creditTransferTransaction.<br>localInstrumentCode
| | Position 3-4 | Account type - from | creditTransferTransaction.<br>debtorAccount.type | creditTransferTransaction.<br>debtorAccount.type 
| | Position 5-6 | Account type - to | creditTransferTransaction.<br>creditorAccount.type | creditTransferTransaction.<br>creditorAccount.type 
P-4|Transaction Amount| N 12 | creditTransferTransaction.<br>settlementAmount | creditTransferTransaction.<br>settlementAmount  
P-7|Transmission Date and Time| N 10 |  | current date and time |  
P-11|Systems Trace Audit number| N 6 | | randomly generated number 
P-12|Local Transaction Time| N 6 | time in groupHeader.<br>creationDateTime | time from groupHeader.<br>creationDateTime  
P-13|Local Transaction Date| N 4 | date in groupHeader.<br>creationDateTime | date from groupHeader.<br>creationDateTime  
P-14|Expiration Date| N 4 | | '  ' for RTC  
P-15|Settlement Date | N 4  | creditTransfer.<br>settlementDate  | creditTransfer.<br>settlementDate 
P-17|Capture Date | N 4 | |current date
P-27|Authorization I.D. Response Length | N 1 | n/a | n/a
P-32|Originating Bank Identification Code | N ++11 | creditTransferTransaction.<br>debtorAgent.<br>memberIdentification | creditTransferTransaction.<br>debtorAgent.<br>memberIdentification
P-35|Track 2 Data (First 6 characters = Branch Code)| ANS ++37 | creditTransferTransaction.<br>creditorAgent.<br>branchNumber | creditTransferTransaction.<br>creditorAgent.<br>branchNumber
P-37|Retrieval Reference Number | N 12 | creditTransferTransaction.<br>endToEndIdentification | creditTransferTransaction.<br>endToEndIdentification
P-38|Authorization Identification Response | N 6 | creditTransferTransaction.<br>remittanceInformation.<br>structured[1].<br>creditorReference | creditTransferTransaction.<br>remittanceInformation.<br>structured[1].<br>creditorReference
P-39|Response Code | AN 2 | n/a | n/a
P-41|Card Acceptor Terminal Identification | ANS 16 | | 'RTCAPI INTERFACE'
P-43|Card Acceptor Name / Location | ANS 40 | creditTransferTransaction.<br>debtorAgent.address | creditTransferTransaction.<br>debtorAgent.address
| | Position 1-22 | Institution | creditTransferTransaction.<br>debtorAgent.name | creditTransferTransaction.<br>debtorAgent.name
| | Position 23-35 | City | creditTransferTransaction.<br>debtorAgent.address.<br>townName|creditTransferTransaction.<br>debtorAgent.address.<br>townName
| | Position 36-38 | Province | creditTransferTransaction.<br>debtorAgent.address.<br>countrySubDivision | creditTransferTransaction.<br>debtorAgent.address.<br>countrySubDivision
| | Position 39 - 40 | Country | creditTransferTransaction.<br>debtorAgent.address.country| creditTransferTransaction.<br>debtorAgent.address.country
P-48|Additional Data Retailer Data | ANS +++30 | | 0 - filled for RTC
P-49|Transaction Currency Code | N 3 | 710 = ZAR <br> creditTransferTransaction.<br>settlementAmount.currency<br>**Only ZAR currently** | 710
P-60|Terminal Data | ANS +++19 | | 0 - filled for RTC
P-61|Card Issuer Category Response Code | ANS +++22
P-63|Additional Data |ANS +++999 | Contains Token Data<br>See below for R1 Token mapping | See below for R1 Token mapping
S-100|Receiving Institution Identification Code | N ++11 | n/a
S-121|CRT Authorisation Data | ANS+++ 23 | |0 - filled for RTC
S-124|Batch and Shift Data | ANS+++ 12 || 0 - filled for RTC
S-125|Settlement Data | ANS +++15 ||' . . . . . . . . . . 1 .'
S-126|Pre-authorisation and Chargeback Data | ANS +++41 | | '...................................000'
S-128| Secondary MAC Code | N 16 || 

## RTC Token

Field Name | Length | Credit-transfer Request
--- | --- | ---
User Reference | ANS 20 | creditTransferTransaction<br>.remittanceInformation.unstructured[0] | 
Business Reference |AN 10 | creditTransferTransaction<br>.remittanceInformation.unstructured[1]
From Branch |AN 6 | creditTransferTransaction<br>.debtorAgent.branchNumber
From Account |N 24 | creditTransferTransaction<br>.debtorAccount
To Account| N 24 | creditTransferTransaction<br>.creditorAccount
Originator Echo Data |ANS 20 | creditTransferTransaction<br>.remittanceInformation.structured[0]<br>.additionalRemittanceInformation | 
Beneficiary Echo Data |ANS 20 | transactionInformation<br>.remittanceInformation.structured[0]<br>.creditorReferenceInformation

## Credit-transfer Response

Field Name | Description | BICISO <br>Length/ <br> Other | Credit-transfer Response <br> (BICISO response will echo back values from request except where otherwise indicated below)<br>to JSON  | Credit-transfer Response<br>from JSON
--- | --- | --- | --- | ---
P-1|Secondary Bitmap| ANS 16 | Built up as per BICISO rules | Built up as per BICISO rules  
P-3|Processing Code| N 6 |  |  
| | Position 1-2 | '42' = payment | 
| | Position 3-4 | Account type - from | 
| | Position 5-6 | Account type - to | 
P-4|Transaction Amount| N 12 |   
P-7|Transmission Date and Time| N 10 |  
P-11|Systems Trace Audit number| N 6 | 
P-12|Local Transaction Time| N 6 | time in groupHeader.creationDateTime | time from groupHeader.creationDateTime  
P-13|Local Transaction Date| N 4 | date in groupHeader.creationDateTime | date from groupHeader.creationDateTime  
P-14|Expiration Date| N 4 | | '  ' for RTC  
P-15|Settlement Date | N 4 | 
P-17|Capture Date | N 4 | | current date
P-27|Authorization I.D. Response Length | N 1 | |length of p-38
P-32|Originating Bank Identification Code | N ++11 | transactionInformation.<br>originalTransactionReference.<br>debtorAgent.<br>memberIdentification | transactionInformation.<br>originalTransactionReference.<br>debtorAgent.<br>memberIdentification
P-35|Track 2 Data (First 6 characters = Branch Code)| ANS ++37 | transactionInformation.<br>originalTransactionReference.<br>creditorAgent.branchNumber | transactionInformation.<br>originalTransactionReference.<br>creditorAgent.branchNumber
P-37|Retrieval Reference Number | N 12 | transactionInformation.<br>endToEndIdentification |transactionInformation.<br>endToEndIdentification
P-38|Authorization Identification Response | N 6 |  n/a | n/a
P-39|Response Code | AN 2 | If Response code not '00'<br>transactionInformation.<br>statusReasonCode | transactionInformation.<br>statusReasonCode  
 | | | | If response code = '00' the transactionInformation.<br>transactionStatus will be 'ACCP', else transactionInformation.<br>transactionStatus will be 'RJCT' | If transactionInformation.<br>transactionStatus = 'ACCP' then Response code must be set to '00'
P-41|Card Acceptor Terminal Identification | ANS 16
P-43|Card Acceptor Name / Location | ANS 40 | 
P-48|Additional Data Retailer Data | ANS +++30 | 
P-49|Transaction Currency Code | N 3 |  
P-60|Terminal Data | ANS +++19 | 
P-61|Card Issuer Category Response Code | ANS +++22
P-63|Additional Data |ANS +++999 | Contains Token Data<br>See below for R1 Token mapping | See below for R1 Token mapping
S-100|Receiving Institution Identification Code | N ++11 | transactionInformation.<br>originalTransactionReference.<br>creditorAgent.<br>memberIdentification | transactionInformation.<br>creditorAgent.<br>memberIdentification
S-121|CRT Authorisation Data | ANS +++23 | |0 - filled for RTC
S-124|Batch and Shift Data | ANS +++12 || 0 - filled for RTC
S-125|Settlement Data | ANS +++15 ||'..........1.'
S-126|Pre-authorisation and Chargeback Data | ANS +++41 | | '...................................000'
S-128| Secondary MAC Code | N 16 || 0 - filled for RTC  

## RTC Token

 Field Name | Length |  Credit-transfer Response |
---| --- |--- | 
User Reference | ANS 20  | transactionInformation<br>.originalTransactionReference.<br>remittanceInformation.unstructured[0]
Business Reference |AN 10 | transactionInformation.<br>originalTransactionReference.<br>remittanceInformation.unstructured[1]
From Branch |AN 6 | transactionInformation.<br>originalTransactionReference.<br>debtorAgent.branchNumber
From Account |N 24 | transactionInformation.<br>originalTransactionReference.<br>debtorAccount
To Account| N 24 | transactionInformation.<br>originalTransactionReference.<br>creditorAccount
Originator Echo Data |ANS 20 | transactionInformation.<br>originalTransactionReference.<br>remittanceInformation.structured[0]<br>.additionalRemittanceInformation | transactionInformation<br>.remittanceInformation.structured[0]<br>.additionalRemittanceInformation
Beneficiary Echo Data |ANS 20 | transactionInformation.<br>originalTransactionReference.<br>remittanceInformation.structured[0]<br>.creditorReferenceInformation
