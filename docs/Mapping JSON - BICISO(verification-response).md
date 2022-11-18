# RTC

## Mapping ISO20022 JSON API - BICISO

### Verification Response (PACS002)

(Incoming to BankservAfrica)

#### Group Header

Name | JSON  Identifier | BICISO |          |
|-|-|-|-|
**Group Header**    |  **groupHeader**     |          |     **[1..1]**  
Message Identification   |     messageIdentification    | n/a |     [1..1]    |
Creation Date Time             |     creationDateTime    | P12 & P13 Local transaction date and time |     [1..1]    | 
Transaction | transactionInformation<br>*see below* | | [1..*] |  

#### Transaction Section

| Name | JSON  identifier | BICISO | |
|-|-|-|-|
|**Transaction** | **transactionInformation** |      | **[1..*]** |
Original Message Identification   |     originalMessageIdentification    | n/a |     [1..1]    |
Original End To End Identification | originalEndToEndIdentification| P37 - Retrieval Reference number | [1..1]
Original UETR | originalUETR | generated uetr from verification request | [1..1]
Transaction Status | transactionStatus | ACCP or RJCT|[1..1]
Reason | statusReasonCode | P39 - Response Code<br>**Only populated for rejected transactions**|[0..1]
Instructing Agent | instructingAgent.<br>memberIdentification | S100 - Receiving Institution Identification Code| [1..1]
Instructed Agent | instructedAgent.<br>memberIdentification | BankservAfrica<br>member id = 210100| [1..1]
Original Transaction Reference | originalTransactionReference | see details below | [1..1]

#### Original Transaction Reference

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Original Transaction Reference** | **originalTransactionReference** | | **[1..1]**
Remittance Information | remittanceInformation |see breakdown below | [1..1]
Debtor Account | debtorAccount|see breakdown below | [0..1]|
Debtor Agent | debtorAgent|see breakdown below |[1..1]|
Creditor Agent | creditorAgent|see breakdown below |[1..1]|
Creditor Account |creditorAccount|see breakdown below |[0..1]|

#### Remittance Information

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Remittance Information** | **remittanceInformation** ||**[1..1]**
Unstructured | unstructured[0] |R1 token - User Reference| [0..1]
| | unstructured[1] |R1 token - Business Reference| [0..1]
Structured[0] |creditorReference | R1 token - Beneficiary Echo Data| [0..1]
|| additionalRemittanceInformation | R1 token - Originator Echo Data|[0..1]
Structured[1] | creditorReference | p38 - Authorisation response | [1..1]

#### Debtor Account

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Debtor Account** | **debtorAccount** ||**[1..1]**
Identification |identification|R1 token - From Account|[0..1]
Type |type|P3 - Processing code<br> Position 3 & 4|[0..1]
Name |name|n/a|[0..1]
Proxy |proxy|n/a|[0..1]
Proxy Type |proxyType|n/a|[0..1]


#### Debtor Agent

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Debtor Agent** | **debtorAgent** || **[1..1]**
|BIC code| BICFI |n/a|[0..1]
|Member Identification| memberIdentification | P32 - Originating Bank Identification Code | [1..1]
|LEI| LEI |n/a|[0..1]
|Name| name | P43 - Card acceptor name<br>Pos 1-22|[0..1]
Address | address. || [0..1]
|| department ||[0..1]
|| subDepartment ||[0..1]
|| streetName ||[0..1]
|| buildingNumber ||[0..1]
|| buildingName || [0..1]
|| floor ||[0..1]
|| postBox ||[0..1]
|| postCode ||[0..1]
|| townName |P43 - Card acceptor name/location<br>Pos 23-35 |[0..1]
|| townLocationName ||[0..1]
|| districtName || [0..1]
|| countrySubDivision |P43 - Card acceptor name/location <br>Pos 36-38| [0..1]
|| country |P43 - Card acceptor name/location<br>Pos 39-40|[0..1]
|Branch Number| branchNumber | R1 token - From Branch| [0..1]
|Domain| domain |n/a|[0..1]


#### Creditor Agent

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Creditor Agent** | **creditorAgent** || **[1..1]**
|BIC code| BICFI |n/a|[0..1]
|Member Identification| memberIdentification | S100 - Receiving Institution Identification Code | [1..1]
|LEI| LEI |n/a|[0..1]
|Name| name ||[0..1]
Address | address. || [0..1]
|| department ||[0..1]
|| subDepartment ||[0..1]
|| streetName ||[0..1]
|| buildingNumber ||[0..1]
|| buildingName || [0..1]
|| floor ||[0..1]
|| postBox ||[0..1]
|| postCode ||[0..1]
|| townName ||[0..1]
|| townLocationName ||[0..1]
|| districtName || [0..1]
|| countrySubDivision || [0..1]
|| country ||[0..1]
|Branch Number| branchNumber | P35 - Track 2 data (first 6 chars)| [0..1]
|Domain| domain |n/a|[0..1]

#### Creditor Account

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Creditor Account** | **creditorAccount** ||**[1..1]**
Identification |identification|R1 token - To Account|[0..1]
Type |type|P3 - Processing code<br> Position 5 & 6|[0..1]
Name |name|n/a|[0..1]
Proxy |proxy|n/a|[0..1]
Proxy Type |proxyType|n/a|[0..1]

### Verification Response (PACS002)

(Outgoing from BankservAfrica)

#### Group Header

Name | JSON  Identifier | BICISO |   |
|-|-|-|-|
**Group Header** | **groupHeader** | | **[1..1]**  
Message Identification   |     messageIdentification    | R1 token: Business Reference |     [1..1]    |
Creation Date Time             |     creationDateTime    | P12 & P13 Local transaction date and time |     [1..1]    | 
Transaction | transactionInformation<br>*see below* | | [1..*] |  

#### Transaction Section

| Name | JSON  identifier | BICISO | |
|-|-|-|-|
|**Transaction** | **transactionInformation** |      | **[1..*]** |
Original Message Identification   |     originalMessageIdentification    | R1 token: Business Reference |     [1..1]    |
Original End To End Identification | originalEndToEndIdentification| P37 - Retrieval Reference number | [1..1]
Original UETR | originalUETR | generated uetr | [1..1]
Transaction Status | transactionStatus | ACCP or RJCT|[1..1]
Reason | statusReasonCode | P39 - Response Code<br>**Only populated for rejected transactions**|[0..1]
Instructing Agent | instructingAgent.<br>memberIdentification | BankservAfrica<br>member id = 210100 | [1..1]
Instructed Agent | instructedAgent.<br>memberIdentification | S100 - Receiving Institution Identification Code | [1..1]
Original Transaction Reference | originalTransactionReference | see details below | [1..1]

#### Original Transaction Reference
Name | JSON identifier | BICISO | |
|-|-|-|-|
**Original Transaction Reference** | **originalTransactionReference** | | **[1..1]**
Remittance Information | remittanceInformation ||[1..1]
Debtor Account | debtorAccount|see breakdown below | [0..1]|
Debtor Agent | debtorAgent|see breakdown below |[1..1]|
Creditor Agent | creditorAgent|see breakdown below |[1..1]|
Creditor Account |creditorAccount|see breakdown below |[0..1]|


#### Remittance Information

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Remittance Information** | **remittanceInformation** ||**[1..1]**
Unstructured | unstructured[0] |R1 token - User Reference| [0..1]
| | unstructured[1] |R1 token - Business Reference| [0..1]
Structured[0] |creditorReference | R1 token - Beneficiary Echo Data| [0..1]
|| additionalRemittanceInformation | R1 token - Originator Echo Data|[0..1]
Structured[1] | creditorReference | p38 - Authorisation response

#### Debtor Account

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Debtor Account** | **debtorAccount** ||**[1..1]**
Identification |identification|R1 token - From Account|[0..1]
Type |type|P3 - Processing code<br> Position 3 & 4|[0..1]
Name |name|n/a|[0..1]
Proxy |proxy|n/a|[0..1]
Proxy Type |proxyType|n/a|[0..1]


#### Debtor Agent

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Debtor Agent** | **debtorAgent** || **[1..1]**
|BIC code| BICFI |n/a|[0..1]
|Member Identification| memberIdentification | P32 - Originating Bank Identification Code | [1..1]
|LEI| LEI |n/a|[0..1]
|Name| name | P43 - Card acceptor name<br>Pos 1-22|[0..1]
Address | address. || [0..1]
|| department ||[0..1]
|| subDepartment ||[0..1]
|| streetName ||[0..1]
|| buildingNumber ||[0..1]
|| buildingName || [0..1]
|| floor ||[0..1]
|| postBox ||[0..1]
|| postCode ||[0..1]
|| townName |P43 - Card acceptor name/location<br>Pos 23-35 |[0..1]
|| townLocationName ||[0..1]
|| districtName || [0..1]
|| countrySubDivision |P43 - Card acceptor name/location <br>Pos 36-38| [0..1]
|| country |P43 - Card acceptor name/location<br>Pos 39-40|[0..1]
|Branch Number| branchNumber | R1 token - From Branch| [0..1]
|Domain| domain |n/a|[0..1]


#### Creditor Agent

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Creditor Agent** | **creditorAgent** || **[1..1]**
|BIC code| BICFI |n/a|[0..1]
|Member Identification| memberIdentification | S100 - Receiving Institution Identification Code | [1..1]
|LEI| LEI |n/a|[0..1]
|Name| name ||[0..1]
Address | address. || [0..1]
|| department ||[0..1]
|| subDepartment ||[0..1]
|| streetName ||[0..1]
|| buildingNumber ||[0..1]
|| buildingName || [0..1]
|| floor ||[0..1]
|| postBox ||[0..1]
|| postCode ||[0..1]
|| townName ||[0..1]
|| townLocationName ||[0..1]
|| districtName || [0..1]
|| countrySubDivision || [0..1]
|| country ||[0..1]
|Branch Number| branchNumber | P35 - Track 2 data (first 6 chars)| [0..1]
|Domain| domain |n/a|[0..1]

#### Creditor Account

Name | JSON identifier | BICISO | |
|-|-|-|-|
**Creditor Account** | **creditorAccount** ||**[1..1]**
Identification |identification|R1 token - To Account|[0..1]
Type |type|P3 - Processing code<br> Position 5 & 6|[0..1]
Name |name|n/a|[0..1]
Proxy |proxy|n/a|[0..1]
Proxy Type |proxyType|n/a|[0..1]