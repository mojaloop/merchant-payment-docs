
## Data needed to create a record  

As we are creating a merchant, it's locations and tills, we would need to consider the following data elements

1. PayIntoID (Alias) - 12345678 (system generated or DFSP provided)
1. MerchantID (system) - 87654321 (system generated)
1. Bank Account (not capturing)
1. CheckOut Counter ID - 000001

## Simple - 1 location, 1 counter  

Data exposed by Merchant Registry
| Item | Sample Data |
|------|-------------|
| DFSP ID | 87654321 |
| MerchantID | 87654321 |
| PayIntoID (Alias) | 12345678 |
| Name of Merchant | ABC Store |
| Location | {full address} |
| MobileNumber | |

Data exposed by DFSP
| Item | Sample Data |
|------|-------------|
| PayIntoID (Alias) | 12345678 |
| Pay Into Account Number | PK23HABB12313123121132 |
| CheckOutCounterID | 000001 |
| Name of Merchant | ABC Store |
| Location | {full address} |

## Making a payment to a merchant in USSD (customer initiated)

### Finding DFSP that maintains this Merchant ID

```mermaid
sequenceDiagram

Title: Lookup Merchant
autonumber

# declare actors
actor cust as Customer
participant PayerFSP as User's<br/>FSP
participant Switch as Switch
participant ALS as Account<br/>Lookup<br/>Service
participant oracle as Merchant<br/>Registry
participant PayeeFSP as Merchant's<br/>DFSP
actor merc as Small Merchant

# start flow
cust->>merc: I would like to buy<br/>this goods or service
merc ->> cust: The goods or service cost<br/>100 USD before any fees,<br/>please initiate the transaction
note over cust,PayerFSP: Question 1<br/>On a USSD flow, how do I add<br/>a counter when I have a Merchant ID?
note over cust,PayerFSP: Question 2<br/>On a USSD flow, how do I add<br/>an alternative currency?
rect rgb(100, 100, 100)
    cust ->> PayerFSP: I would like to pay<br/>$100 to Merchant ID 0123456789
    activate PayerFSP
    note over cust:Customer Participant<br/>Merchant Alias<br/>[PayIntoID](12345678)
    cust ->> PayerFSP : Pay Till No [Till_ID]
    note over cust:Customer provides<br/>Till Number<br/>[CheckOutCounterID](000001)
end

PayerFSP ->> PayerFSP: 0123456789 is not<br/>within this system
PayerFSP ->> Switch: GET /parties/Merchant/0123456789
activate Switch
Switch -->> PayerFSP: HTTP 202 (Accepted)
Switch ->> ALS: GET /participants/Merchant/0123456789
activate ALS
ALS -->> Switch: HTTP 202 (Accepted)
ALS ->> ALS: Lookup which FSP Merchant<br/>0123456789 belongs to.
ALS ->> Switch: PUT /participants/Merchant/0123456789<br/>(Merchant's DFSP)
Switch -->> ALS: HTTP 200 (OK)
deactivate ALS
Switch ->> PayeeFSP: GET /parties/Merchant/0123456789
activate PayeeFSP
PayeeFSP -->> Switch: HTTP 202 (Accepted)
PayeeFSP -> PayeeFSP: Lookup party information<br/>for 0123456789
PayeeFSP ->> Switch: PUT /parties/Merchant/0123456789<br/>(Party information)
    note over Switch: Extension list:<br/>MERCHANTID, DBAName, ClientID etc, location etc.
Switch -->> PayeeFSP: HTTP 200 (OK)
deactivate PayeeFSP
Switch ->> PayerFSP: PUT /parties/Merchant/0123456789<br/>(Party information)
    note over PayerFSP: Extension list:<br/>MERCHANTID, DBAName, ClientID etc, location etc.
PayerFSP -->> Switch: HTTP 200 (OK)
deactivate Switch
PayerFSP ->> cust: Is "name" correct?
deactivate PayerFSP


```

### Quotes and Transfer  


```mermaid
sequenceDiagram
Title: Lookup Merchant

autonumber

# declare actors
actor cust as Customer
participant PayerFSP as User's<br/>FSP
participant Switch as Switch
participant ALS as Account<br/>Lookup<br/>Service
participant oracle as Merchant<br/>Registry
participant PayeeFSP as Merchant's<br/>DFSP
actor merc as Small Merchant

cust->>merc: I would like to buy<br/>this goods or service
merc ->> cust: The goods or service cost<br/>100 USD before any fees,<br/>please initiate the transaction

rect rgb(100, 100, 100)
    cust ->> PayerFSP: I would like to pay<br/>$100 to Merchant ID 0123456789
    activate PayerFSP
    note over cust:Customer Participant<br/>Merchant Alias<br/>[PayIntoID](12345678)
    cust ->> PayerFSP : Pay Till No [Till_ID]
    note over cust:Customer provides<br/>Till Number<br/>[CheckOutCounterID](000001)
end
PayerFSP->>PayerFSP: Lookup 0123456789 (outlined above)
PayerFSP ->> Switch: POST /quotes<br/>(amountType=RECEIVE,<br/>amount=100 USD)
Switch -->> PayerFSP: HTTP 202 (Accepted)
activate Switch
Switch ->> PayeeFSP: POST /quotes<br/>(amountType=RECEIVE,<br/>amount=100 USD)
activate PayeeFSP
PayeeFSP -->>Switch: HTTP 202 (Accepted)
PayeeFSP -> PayeeFSP: Interoperable fee is 0 USD in<br/>Payee FSP for Merchant<br/>Payment, but 1 USD in<br/>internal Payee fee for Merchant
PayeeFSP ->> Switch: PUT /quotes/<ID><br/>(transferAmount=100 USD)
Switch -->> PayeeFSP: HTTP 200 (OK)
deactivate PayeeFSP
Switch ->> PayerFSP: PUT /quotes/<ID><br/>(transferAmount=100 USD)
PayerFSP -->> Switch: HTTP 200 (OK)
deactivate Switch
PayerFSP -> PayerFSP: Fee is 1 USD in Payer<br/>FSP for Merchant Payment,<br/>total fee is 1 USD
PayerFSP->>cust: Will you approve Merchant Payment<br/>of 100 USD to Payee? It will<br/>cost you 1 USD in fees.
deactivate PayerFSP
cust ->> PayerFSP: Perform transaction
activate PayerFSP
PayerFSP -> PayerFSP: Reserve 101 USD from Payer<br/>account, 100 USD to Switch<br/>account and 1 USD to<br/>fee account
PayerFSP ->> Switch: POST /transfers<br/>(amount=100 USD)
activate Switch
Switch -->> PayerFSP: HTTP 202 (Accepted)
Switch -> Switch: Reserve 100 USD from Payer FSP<br/>account to Payee FSP account
Switch ->> PayeeFSP: POST /transfers<br/>(amount=100 USD)
activate PayeeFSP
PayeeFSP --> Switch: HTTP 202 (Accepted)
PayeeFSP -> PayeeFSP: Transfer 100 USD from Switch<br/>account to Payee account, 1 USD<br/>from Payee to fee account
PayeeFSP -> Payee: You have received 100 USD<br/>from Payer and paid 1 USD<br/>in internal fee. Please give<br/>goods or service to Payer.
Payee ->> cust: Here are your goods or services
PayeeFSP ->> Switch: PUT /transfers/<ID>
Switch -->> PayeeFSP: HTTP 200 (OK)
deactivate PayeeFSP
Switch -> Switch: Commit reserved transfer
Switch ->> PayerFSP: PUT /transfers/<ID>
PayerFSP -->> Switch: HTTP 200 (OK)
deactivate Switch
PayerFSP -> PayerFSP: Commit reserved transfer
PayerFSP ->> cust : Payment successful, you<br/>have paid 100 USD to Payee<br/>plus 1 USD in fees
deactivate PayerFSP

```

```nano
PAYINTOID  -->  PAYINTOID, MERCHANTID, DFSPID
PayerFSP -> ALS - MerchantRegistry ---> 12345678       (12345678,87654321, DFSP-A)

GET /parties  (PAYINTOID, Extension Data ?)
-------------------------------------------
PayerFSP -> MOJALOOP --> DFSPA   (PayintoID --> ClientID, Name of Store (PayeeInfo) )

QUOTE

TRANSFER
PayerFSP -> Amount, AccountNumber, TillNumber,  (DFSP notifies the merchant about payment using TillNumber matched to CheckOutCounterID)
========================================================================================================================================

====================================================================================================================
Complex - Multi location, Multi counter  (4)  -  
 Loc 1 - Count 1,2
 Loc 2 - Count 3
 Loc 3 - Count 4
====================================================================================================================
MerchantID, PayIntoID, CheckOutCounterID, Location, MerchantContact, ClientID  
87654321, 12345677, 000001,  ABC Store, Location 1 MobileNumber              -   PK23HABB12313123121132
87654321, 12345677, 000002,  ABC Store, Location 1, MobileNumber             -   PK23HABB12313123121132
87654321, 12345678, 000003,  ABC Store, Location 2, MobileNumber             -   PK23HABB12313123121134
87654321, 12345679, 000004,  ABC Store, Location 3, MobileNumber             -   PK23HABB12313123121135

User (Customer)
--> Enter Merchant Alias: 12345678
--> Enter Till No. 000003 

GET /participants
							PAYINTOID  -->  PAYINTOID, MERCHANTID, DFSPID
PayerFSP -> ALS - MerchantRegistry ---> 12345678       (12345678,87654321, DFSP-A)

GET /parties  (PAYINTOID, Extension Data ?)
-------------------------------------------
PayerFSP -> MOJALOOP --> DFSPA   (PayintoID --> IBAN/AccountNumber, Name of Store (PayeeInfo) )

QUOTE

TRANSFER
PayerFSP -> Amount, AccountNumber, TillNumber,  (DFSP notifies the merchant about payment using TillNumber matched to CheckOutCounterID)
========================================================================================================================================
```