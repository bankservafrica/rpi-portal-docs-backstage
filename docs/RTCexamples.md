# RTC Example messages

## Verification Request

### JSON - PACS008

Created from BICISO message below

~~~json
{
  "groupHeader":  {
    "messageIdentification":  "20201019_XXXX_RTCVQ_000000000000123",
    "creationDateTime":  "2020-10-19T00:00:09.000000",
    "numberOfTransactions":  1,
    "settlementMethod":  "CLRG",
    "clearingSystem":  "RTC"
  },
  "creditTransferTransaction":  [
    {
      "endToEndIdentification":  "021785278712",
      "uetr": "dd0399fc-9d4f-457f-84f5-f52d56e6c525",
      "localInstrumentCode":  "42",
      "settlementAmount":  {
        "currency":  "ZAR",
        "amount":  13000.00
      },
      "chargeBearer":  "SLEV",
      "instructingAgent":  {
        "memberIdentification":  "210010"
      },
      "instructedAgent":  {
        "memberIdentification":  "210100"
      },
      "debtorAccount":  {
        "identification":  "1111111111",
        "type":  "OTHR"
      },
      "debtorAgent":  {
        "memberIdentification":  "210010",
        "name":  "CAPITEC BANK          ",
        "address":  {
          "townName":  "STELLENBOSCH ",
          "countrySubDivision":  "WC ",
          "country":  "ZA"
        },
        "branchNumber":  "470010"
      },
      "creditorAgent":  {
        "memberIdentification":  "210003",
        "branchNumber":  "250655"
      },
      "creditorAccount":  {
        "identification":  "22222222222",
        "type":  "OTHR"
      },
      "remittanceInformation": {
        "unstructured": [
          "USER REFERENCE      ",
          "bdefda31de"
        ],
        "structured": [
          {
            "additionalRemittanceInformation": "             CAPITEC"
          }
        ]
      }
    }
  ]
}
~~~

### Corresponding BICISO 200 message

~~~bash
  3 [Processing Code] "420000"
  4 [Transaction Amount] "000001300000"
  7 [Transmission Date and Time] "1019000009"
 11 [System Trace Audit Number] "814074"
 12 [Local Transaction Time] "000009"
 13 [Local Transaction Date] "1019"
 17 [Capture Date] "1019"
 22 [Point of Service Entry Mode] "000"
 32 [Acquiring Institution Identification Code] (02)"34"
 35 [Track 2 Data] (21)"2506550000000000=0000"
 37 [Retrieval Reference Number] "021785278712"
 41 [Card Acceptor Terminal Identification] "12340001        "
 42 [Card Acceptor Identification Code] "000000000000000"
 43 [Card Acceptor Name or Location] "CAPITEC BANK          STELLENBOSCH WC ZA"
 48 [Additional Data - atm/ptr/network] (027)"000000000000000            "
 49 [Transaction Currency Code] "710"
 60 [BASE24-atm/pos Terminal Data] (016)"0034Dev2+0000000"
 61 [BASE24-atm/ps Card Issuer (and Authorizer Data/Category-Response Code Data)] (019)"0034Dev2000        "
 63 [BASE24-atm PIN Offset or BASE24-POS Additional Data] (174)"& 0000300174! R100130 USER REFERENCE      bdefda31de470010000000000000001111111111000000000000022222222222       
      CAPITEC                          ! C400012 100110000200"
Token (R1) : "USER REFERENCE      bdefda31de470010000000000000001111111111000000000000022222222222             CAPITEC                          "
UserReference : "USER REFERENCE      "
DebtorID : "bd"
Reference : "efda31de"
DebtorBranch : "470010"
DebtorAccount : "1111111111"
CreditorAccount : "22222222222"
DebtorEchoData : "             CAPITEC"
CreditorEchoData : ""
Filler : ""`
Generic Token
C4 : "100110000200"
121 [POS auth indicators] (020)"RTCTES              "
124 [Batch and Shift data] (009)"074000000"
125 [POS settlement data] (012)"          1 "
126 [Pre-Auth and Chargeback] (038)"                                   000"
~~~

--- 
## Verification Response

### JSON - PACS002

Created from BICISO message below

~~~json
{
  "groupHeader":  {
    "messageIdentification":  "20201019_XXXX_RTCVR_000000000000087",
    "creationDateTime":  "2020-10-19T00:00:09.000000"
  },
  "transactionInformation":  [
    {
      "originalMessageIdentification": "20201019_XXXX_RTCVQ_000000000000123",
      "originalMessageName": "pacs.008:RtcVerificationRequest",
      "originalEndToEndIdentification": "021785278712",
      "originalUETR": "dd0399fc-9d4f-457f-84f5-f52d56e6c525",
      "transactionStatus": "ACCP",
      "instructingAgent":  {
        "memberIdentification":  "210010"
      },
      "instructedAgent":  {
        "memberIdentification":  "210100"
      },
      "originalTransactionReference":  {
        "remittanceInformation":  {
          "unstructured": [
            "USER REFERENCE",
            "bdefda31d5"
          ],
          "structured":  [
            {
              "creditorReference":  "CREDITOR ECHO       ",
              "additionalRemittanceInformation":  "             CAPITEC"
            },
            {
              "creditorReference": "123456"
            }
          ]
        },
        "debtorAgent":  {
          "memberIdentification":  "210010",
          "branchNumber":  "470010"
        },
        "creditorAgent":  {
          "memberIdentification":  "210003",
          "branchNumber":  "250655"
        },
        "creditorAccount": {
          "identification": "22222222222"
        },
        "debtorAccount": {
          "identification": "1111111111"
        }
      }
    }
  ]
}
~~~

### Corresponding BICISO 210 message

~~~bash
Header: ISO0260000660210
  3 [Processing Code] "420000"
  4 [Transaction Amount] "000001300000"
  7 [Transmission Date and Time] "1019000009"
 11 [System Trace Audit Number] "814074"
 12 [Local Transaction Time] "000009"
 13 [Local Transaction Date] "1019"
 15 [Settlement Date] "1019"
 17 [Capture Date] "1019"
 32 [Acquiring Institution Identification Code] (02)"34"
 35 [Track 2 Data] (37)"2506550000000000=0000   0000000000000"
 37 [Retrieval Reference Number] "021785278712"
 38 [Authorization Identification Response] "123456"
 39 [Response Code] "00"
 41 [Card Acceptor Terminal Identification] "12340001        "
 49 [Transaction Currency Code] "710"
 60 [BASE24-atm/pos Terminal Data] (016)"0034Dev2+0000000"
 61 [BASE24-atm/ps Card Issuer (and Authorizer Data/Category-Response Code Data)] (019)"                   "
 63 [BASE24-atm PIN Offset or BASE24-POS Additional Data] (152)"& 0000200152! R100130 USER REFERENCE      bdefda31d5470010000000000000001111111111000000000000022222222222             CAPITECCREDITOR ECHO             "
Token (R1) : "USER REFERENCE      bdefda31d5470010000000000000001111111111000000000000022222222222             CAPITECCREDITOR ECHO             "
UserReference : "USER REFERENCE      "
DebtorID : "bd"
Reference : "efda31d5"
DebtorBranch : "470010"
DebtorAccount : "1111111111"
CreditorAccount : "22222222222"
DebtorEchoData : "             CAPITEC"
CreditorEchoData : "CREDITOR ECHO       "
Filler : ""
100 [Receiving Institution Identification Code] (02)"05"
121 [POS auth indicators] (020)"RTCTES              "
~~~

---
## Clearing Credit Transfer

### JSON - PACS008

Created from BICISO message below

~~~json
{
  "groupHeader":  {
    "messageIdentification":  "20201019_XXXX_RTCCT_000000000000145",
    "creationDateTime":  "2020-10-19T00:00:09.000000",
    "numberOfTransactions":  1,
    "settlementMethod":  "CLRG",
    "clearingSystem":  "RTC"
  },
  "creditTransferTransaction":  [
    {
      "endToEndIdentification":  "021785278712",
      "uetr":  "dd0399fc-9d4f-457f-84f5-f52d56e6c525",
      "localInstrumentCode":  "42",
      "settlementAmount":  {
        "currency":  "ZAR",
        "amount":  13000
      },
      "chargeBearer":  "SLEV",
      "instructingAgent":  {
        "memberIdentification":  "210010"
      },
      "instructedAgent":  {
        "memberIdentification":  "210100"
      },
      "debtorAccount":  {
        "identification":  "1111111111",
        "type":  "OTHR"
      },
      "debtorAgent":  {
        "memberIdentification":  "210010",
        "name":  "CAPITEC BANK          ",
        "address":  {
          "townName":  "STELLENBOSCH ",
          "countrySubDivision":  "WC ",
          "country":  "ZA"
        },
        "branchNumber":  "470010"
      },
      "creditorAgent":  {
        "branchNumber":  "250655"
      },
      "creditorAccount":  {
        "identification":  "22222222222",
        "type":  "OTHR"
      },
      "remittanceInformation":  {
        "unstructured": [
          "USER REFERENCE",
          "bdefda31d5"
        ],
        "structured":  [
          {
            "creditorReference":  "CREDITOR ECHO       ",
            "additionalRemittanceInformation":  "             CAPITEC"
          },
          {  
            "creditorReference": "123456"
          }
        ]
      },
    }
  ]
}
~~~

### Corresponding BICISO 220 message

~~~bash
Header: ISO0260000000220
  3 [Processing Code] "420000"
  4 [Transaction Amount] "000001300000"
  7 [Transmission Date and Time] "1019000009"
 11 [System Trace Audit Number] "814076"
 12 [Local Transaction Time] "000009"
 13 [Local Transaction Date] "1019"
 17 [Capture Date] "1019"
 22 [Point of Service Entry Mode] "000"
 27 [Authorization Identification Response Length] "6"
 32 [Acquiring Institution Identification Code] (02)"34"
 35 [Track 2 Data] (21)"2506550000000000=0000"
 37 [Retrieval Reference Number] "021785278712"
 38 [Authorization Identification Response] "123456"
 39 [Response Code] "00"
 41 [Card Acceptor Terminal Identification] "12340001        "
 42 [Card Acceptor Identification Code] "000000000000000"
 43 [Card Acceptor Name or Location] "CAPITEC BANK          STELLENBOSCH WC ZA"
 48 [Additional Data - atm/ptr/network] (027)"000000000000000            "
 49 [Transaction Currency Code] "710"
 60 [BASE24-atm/pos Terminal Data] (016)"0034Dev2+0000000"
 61 [BASE24-atm/ps Card Issuer (and Authorizer Data/Category-Response Code Data)] (019)"0034Dev2000        "
 63 [BASE24-atm PIN Offset or BASE24-POS Additional Data] (174)"& 0000300174! R100130 USER REFERENCE      bdefda31d5470010000000000000001111111111000000000000022222222222       
      CAPITECCREDITOR ECHO             ! C400012 100110000200"
Token (R1) : "USER REFERENCE      bdefda31d5470010000000000000001111111111000000000000022222222222             CAPITECCREDITOR ECHO             "
UserReference : "USER REFERENCE      "
DebtorID : "bd"
Reference : "efda31d5"
DebtorBranch : "470010"
DebtorAccount : "1111111111"
CreditorAccount : "22222222222"
DebtorEchoData : "             CAPITEC"
CreditorEchoData : "CREDITOR ECHO       "
Filler : ""
Generic Token
C4 : "100110000200"
100 [Receiving Institution Identification Code] (11)"10269859898"
121 [POS auth indicators] (020)"RTCTES              "
124 [Batch and Shift data] (009)"076000000"
125 [POS settlement data] (012)"          1 "
126 [Pre-Auth and Chargeback] (038)"                                   000"
~~~

---
## Clearing Delivery Status Report

### JSON - PACS008

Created from BICISO message below

~~~json
{
  "groupHeader":  {
    "messageIdentification":  "20201019_XXXX_RTCCR_000000000000132",
    "creationDateTime":  "2020-10-19T00:00:09.000000"
  },
  "transactionInformation":  [
    {
      "originalMessageIdentification": "20201019_XXXX_RTCCT_000000000000145",
      "originalMessageName": "pacs.008:RtcCreditTransfer",
      "originalEndToEndIdentification": "021785278712",
      "originalUETR": "dd0399fc-9d4f-457f-84f5-f52d56e6c525",
      "transactionStatus": "ACCP",
      "instructingAgent":  {
        "memberIdentification":  "210010"
      },
      "instructedAgent":  {
        "memberIdentification":  "210100"
      },
      "originalTransactionReference":  {
        "debtorAgent":  {
          "memberIdentification":  "210010"
        },
        "creditorAgent":  {
         "memberIdentification":  "210003",
        }
      }
    }
  ]
}
~~~

### Corresponding BICISO 230 message

~~~bash
Header: ISO0260000660230
  3 [Processing Code] "420000"
  4 [Transaction Amount] "000001300000"
  7 [Transmission Date and Time] "1019000009"
 11 [System Trace Audit Number] "814076"
 32 [Acquiring Institution Identification Code] (02)"34"
 37 [Retrieval Reference Number] "021785278712"
 39 [Response Code] "00"
 41 [Card Acceptor Terminal Identification] "12340001        "
 49 [Transaction Currency Code] "710"
 61 [BASE24-atm/ps Card Issuer (and Authorizer Data/Category-Response Code Data)] (019)"                   "
100 [Receiving Institution Identification Code] (02)"05"
~~~

---
## Minimum Required Fields for RTC API message

### Verification Request (PACS008)

#### groupHeader  

    messageIdentification  :  unique identifier, alphanumeric
    creationDateTime  : format YYYY-MM-DDThh:mm:ss.ssssss
    numberOfTransactions  - only 1 for now
    settlementMethod  = CLRG
    clearingSystem  = RTC   

#### creditTransferTransaction[]

    endToEndIdentification  : max length 12
    uetr  
    settlementAmount.amount  
    settlementDate
    chargeBearer = SLEV  
    instructingAgent.memberIdentification : length of 6 , numeric  
    instructedAgent.memberIdentification  : length of 6 , numeric
    debtorAccount.identification : max length of 24, numeric
    debtorAgent.branchNumber : length of 6 , numeric
    debtorAgent.memberIdentification : length of 6 , numeric
    creditorAgent.branchNumber : length of 6 , numeric
    creditorAccount.identification : max length of 24, numeric
    remittanceInformation.unstructured[0] - if present : max length 20, alphanumeric
    remittanceInformation.unstructured[1] - if present : max length 10, alphanumeric
    remittanceInformation.structured[0].additionalRemittanceInformation - if present : max length 20, alphanumeric 
  

### Verification Response (PACS002)

#### groupHeader

    messageIdentification : unique identifier, alphanumeric 
    creationDateTime  : format YYYY-MM-DDThh:mm:ss   

#### transactionInfo[]

    originalMessageIdentification 
    originalMessageName - content still to be defined
    originalEndToEndIdentification
    originalUETR
    transactionStatus - ACCP or RJCT
        If RJCT then statusReasonCode is required
    instructingAgent.memberIdentification : length of 6 , numeric
    instructedAgent.memberIdentification  : length of 6 , numeric

#### originalTransactionReference

    debtorAgent.memberIdentification : length of 6 , numeric
    creditorAgent.memberIdentification  : length of 6 , numeric
    remittanceInformation.unstructured[0] : max length 20, alphanumeric 
    remittanceInformation.unstructured[1]  : -if present - max length 10, alphanumeric
    remittanceInformation.structured[0].creditorReference  if present : max length 20, alphanumeric
    remittanceInformation.structured[1].creditorReference : max length 6, alphanumeric
    remittanceInformation.structured[0].additionalRemittanceInformation - if present : max length 20, alphanumeric 
    remittanceInformation.structured[0].creditorReference - if present : max length 20, alphanumeric  

### Clearing Request - credit-transfer (PACS008)

#### groupHeader  

    messageIdentification  :  unique identifier, alphanumeric
    creationDateTime  : format YYYY-MM-DDThh:mm:ss
    numberOfTransactions  - only 1 for now
    settlementMethod  = CLRG
    clearingSystem  = RTC

#### creditTransferTransaction[]

    endToEndIdentification  : max length 12
    uetr  
    settlementAmount.amount  
    settlementDate
    chargeBearer = SLEV
    instructingAgent.memberIdentification : length of 6 , numeric
    instructedAgent.memberIdentification  : length of 6 , numeric
    debtorAccount.identification : max length of 24, numeric
    debtorAgent.branchNumber : length of 6 , numeric
    debtorAgent.memberIdentification : length of 6 , numeric
    creditorAgent.branchNumber : length of 6 , numeric
    creditorAgent.memberIdentification : length of 6 , numeric
    creditorAccount.identification : max length of 24, numeric
    remittanceInformation.unstructured[0]  : max length 20, alphanumeric
    remittanceInformation.unstructured[1] - if present : max length 10, alphanumeric
    remittanceInformation.structured[0].creditorReference - if present : max length 20, alphanumeric
    remittanceInformation.structured[1].creditorReference : max length 6, alphanumeric
    remittanceInformation.structured[0].additionalRemittanceInformation - if present : max length 20, alphanumeric

### Clearing Response - delivery-status-report (PACS002)

#### groupHeader

    messageIdentification : unique identifier, alphanumeric 
    creationDateTime : format YYYY-MM-DDThh:mm:ss  

#### transactionInfo[]

    originalMessageIdentification 
    originalMessageName - content still to be defined
    originalEndToEndIdentification
    originalUETR
    transactionStatus - ACCP or RJCT
        If RJCT then statusReasonCode is required
    instructingAgent.memberIdentification : length of 6 , numeric
    instructedAgent.memberIdentification  : length of 6 , numeric

#### originalTransactionReference

    debtorAgent.memberIdentification : length of 6 , numeric
    creditorAgent.memberIdentification  : length of 6 , numeric
    remittanceInformation.unstructured[1] - if present : max length 10, alphanumeric
    remittanceInformation.structured[0].creditorReference - if present : max length 20, alphanumeric
    remittanceInformation.structured[0].additionalRemittanceInformation - if present : max length 20, alphanumeric
    remittanceInformation.structured[1].creditorReference - if present : max length 6, alphanumeric
