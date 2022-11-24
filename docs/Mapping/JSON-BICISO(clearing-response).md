# RTC

## Mapping ISO20022 JSON API - BICISO

### Clearing: Payment Status Report (PACS002)

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
Original UETR | originalUETR | generated uetr | [1..1]
Transaction Status | transactionStatus | ACCP or RJCT|[1..1]
Reason | statusReasonCode | P39 - Response Code<br>**Only populated for rejected transactions**|[0..1]
Instructing Agent | instructingAgent.<br>memberIdentification | S100 - Receiving Institution Identification Code| [1..1]
Instructed Agent | instructedAgent.<br>memberIdentification | BankservAfrica<br>member id = 210100| [1..1]
Remittance Information | remittanceInformation | | [1..1]

#### Remittance Information

Name | JSON identifier | BICISO | |
|-|-|-|-|
Remittance Information | remittanceInformation ||[1..1]
Unstructured | unstructured[0] |R1 token - User Reference| [0..1]
| | unstructured[1] |R1 token - Business Reference| [0..1]
Structured[0] |creditorReference | R1 token - Beneficiary Echo Data| [0..1]
|| additionalRemittanceInformation | R1 token - Originator Echo Data|[0..1]
Structured[1] | creditorReference | p38 - Authorisation response


### Clearing: Payment Status Report (PACS002)

(Outgoing from BankservAfrica)

#### Group Header

Name | JSON  Identifier | BICISO |          |
|-|-|-|-|
**Group Header** |**groupHeader** |          |     **[1..1]**  
Message Identification   |     messageIdentification    | n/a |     [1..1]    |
Creation Date Time             |     creationDateTime    | P12 & P13 Local transaction date and time |     [1..1]    | 
Transaction | transactionInformation<br>*see below* | | [1..*] |  

#### Transaction Section

| Name | JSON  identifier | BICISO | |
|-|-|-|-|
|**Transaction** | **transactionInformation** |      | **[1..*]** |
Original Message Identification   |     originalMessageIdentification    | n/a  |     [1..1]    |
Original End To End Identification | originalEndToEndIdentification| P37 - Retrieval Reference number | [1..1]
Original UETR | originalUETR | generated uetr | [1..1]
Transaction Status | transactionStatus | ACCP or RJCT|[1..1]
Reason | statusReasonCode | P39 - Response Code<br>**Only populated for rejected transactions**|[0..1]
Instructing Agent | instructingAgent.<br>memberIdentification | BankservAfrica<br>member id = 210100 | [1..1]
Instructed Agent | instructedAgent.<br>memberIdentification |  S100 - Receiving Institution Identification Code| [1..1]
Remittance Information | remittanceInformation | | [1..1]

#### Remittance Information

Name | JSON identifier | BICISO | |
|-|-|-|-|
Remittance Information | remittanceInformation ||[1..1]
Unstructured | unstructured[0] |R1 token - User Reference| [0..1]
| | unstructured[1] |R1 token - Business Reference| [0..1]
Structured[0] |creditorReference | R1 token - Beneficiary Echo Data| [0..1]
|| additionalRemittanceInformation | R1 token - Originator Echo Data|[0..1]
Structured[1] | creditorReference | p38 - Authorisation response
