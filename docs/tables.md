# Enumerations

The following tables show the possible enumeration values catered for in the verification service.

## Member Identifiers 

These are the agent identifiers

Bank Name | Institution Identifier | File literal | RTC Bank code
--- | --- | --- | ---
ABSA Bank | 210016 | T0 | 16
African Bank | 210007  | AN | 36
Albaraka Bank | 210052  | LB | 38
Bank of Windhoek | 210014 | R0 | 03
Bidvest Bank | 210044 | R1 | 07,37
Capitec Bank | 210010 | N0 | 54
Citibank |210033 | AG | 47
Discovery Bank | 210063 |  DB | 56
Finbond Mutual Bank | 210055 | FM| 49,52
FirstRand Bank | 210003 | A0 | 02,05,06, 2
Grindrod Bank |210047 | GL | 29,42
Grobank | 210006 | H0 | 29, 30, 44
HBZ Bank Limited | 210036 | AJ | 43
Investec Bank | 210039 | AM | 51
Ithala Bank | 210030 | AD | 35
Mercantile Bank  |210009 | J0 | 01,28
Nedbank | 210002 | D0 | 21,45
South African Post Office (SAPO) | 210013 | A0 | 09,57
SASFIN Bank | 210058 | S5 | 50
Standard Bank of South Africa (SBSA) | 210001 | B0 | 18,20,23,24
Standard Charter Bank | 210042 | AQ | 55
Tyme Digital | 210061 | CW | 54
UBank | 210019 | X0 | 31

## Account Type

These indicate the type of account

ISO8583 Code | Description | ISO20022 Code | Description
------------ | ---------- | ------------- | -----------
00 | No account specified | OTHR | Other - not specified
01 | Cheque account type |CACC | Current
02 | Savings account type | SVGS | Savings
03 | Transmission account | TRAN | Transactional
04 | Bond account  | LOAN | Loan:Bond  
06 | Subscription share | TRAS | Share trading

## Verification Response Codes

The table below details the possible ISO20022 External Verification Reason Codes to be used in the verification response message.

|Code | Name | AVS
---- | ---------- | ----
0000 | VerificationSuccessful | 00
AB07 | Offline Agent(Bank offline) | 91
AB05 | Timeout Creditor Agent | 68
AG01 | Transaction Forbidden | 05
AG03 | Transaction Not supported | 12
DT01 | Invalid Date | Q0
FF02 | Syntax Error | 06
FF10 | Bank System Processing Error | 96
RC02 | Invalid Bank Identifier | 31
TD03 | Incorrect File structure(insufficient detail) | 30

## RTC Response Codes

Code | Description |  ISO20022 Name | RTC
--- | --- | --- | ---
0000 | Approved or completed successfully |  n/a  |  
  |  |  |
AB07 | Issuer not available | OfflineAgent | 91
AB05 | Response received too late |TimeoutCreditorAgent | 68
AC12 | No universal Account| InvalidAccountType | 42
AC01 | No such account | IncorrectAccountNumber | 14
AC04 | Account closed | ClosedAccount  | 12
AC06 | Account frozen | BlockedAccount | 06
AC17 | Account in liquidation/sequestration | AccountInLiquidation | 08
AG01 | Do not honour | TransactionNotAllowed | 05
AM02 | Invalid amount | NotAllowedAmount | 13
DS0G | Credit not allowed | NotAllowedPayment | 03
DT01 | Invalid date | InvalidDate | Q0
FF01 | Format Error | InvalidFileFormat | 30
FF10 | Error/System malfunction | BankSystemProcessingError | 96
MD07 | Account Holder deceased | EndCustomerDeceased | 33
RC02 | Bank not supported by Switch | InvalidBankIdentifier | 31
RR04 | Not FICA compliant | RegulatoryReason | 56

## Private Identification Type

These following ISO20022 codes are used to indicate the type of identification to be verified

Type | Description
------------- | -----------
NIDN | National Identity Number
CCPT | Passport

## HTTP Response Codes

The following default HTTP response codes will be used in the HTTP response messages

Code | Description | gRPC response | Detailed description
----| -----------| -------------| --------
200 | A successful response. | OK | Transaction accepted
400 | Bad request. | INVALID_ARGUMENT | The contents of the message were invalid
404 | Resource does not exist. | NOT_FOUND | Endpoint invalid or not found
412 | Precondition Failed. | FAILED_PRECONDITION | Payload content failed basic validation, message rejected
500 | Internal Server Error.

## Status Codes

Code | Description
---- | ----------
ACCP | Accepted
RJCT | Rejected

## Recommended layout for Message Identification

The following is the proposed format for the Message Identification field:  
YYYYMMDD_XXXX_SSSSS_nnnnnnnnnn  

YYYYMMDD is the date the message is created  

XXXX is a bank identifier – the first 4 digits of the BICCODE or some agreed on bank identifier  

SSSSS – is a 5 digit service identifier, as listed below:  
 
RTCVQ – verification request  
RTCVR – verification response  
RTCCT – credit transfer request  
RTCCR – credit transfer response/delivery status report  
*AVSVQ - AVS verificationrequest  
AVSVR - AVS verification response*

 
For the remaining numeric identifier, a 15 digit sequence number  