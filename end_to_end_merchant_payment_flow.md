---  
sidebar_position: 2  
sidebar_label: Merchant Payment - Data
title: Data Flows for a Merchant Payment
date: 2023-07-07 09:52:28
author: Rob Reeve
description: flows for a merchant payment
tags: 
---  

## Making a payment to a merchant via USSD (customer initiated)

In the following scenario, we are going to test the boundaries a little, by assuming that the Payment to the merchant will be from a user in one country to a merchant in another country. We provide the data that is needed below and the sequence and the flow of information between the various parties.

The design currently assumes each party has an account identifier that only maps to a single currency. Further design would be required to support an identifier that maps to multiple currencies and any potential resolution that might be required. The receiving DFSP will initiate the conversion of the foreign exchange currency (equally this could be facilitated by the paying DFSP, but this will be explored later).

## Data needed to create a record  

As we are creating a merchant, it's locations and tills, we would need to consider the following data elements

1. PayIntoID (Alias) - 12345678 (system generated or DFSP provided)
1. MerchantID (system) - 87654321 (system generated)
1. Bank Account (not capturing)
1. CheckOut Counter ID - 000001

## Simple - 1 location, 1 counter  

We will assume our customer is in Malawi, and our merchant is in Zambia.

As the merchant will be displaying their price in the transacting currency, it will be necessary to send a "receive" request, to ensure that the merchant gets the price expected.

The transaction will be for 100 ZMK, with an exchange rate of 1 ZMK equal to 57.31 MWK.
The Merchant FSP will charge 1ZMK for the merchant transaction.

### Data exposed by Merchant Registry

| Item              | Sample Data    |
| ----------------- | -------------- |
| DFSP ID           | DFSP2          |
| MerchantID        | 87654321       |
| PayIntoID (Alias) | 12345678       |
| Name of Merchant  | ABC Store      |
| Location          | {full address} |
| MobileNumber      |                |

### Data exposed by Payee DFSP

| Item                    | Sample Data            |
| ----------------------- | ---------------------- |
| PayIntoID (Alias)       | 12345678               |
| Pay Into Account Number | PK23HABB12313123121132 |
| CheckOutCounterID       | 000001                 |
| Name of Merchant        | ABC Store              |
| Location                | {full address}         |

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
cust->>merc: I would like to buy<br/>these goods or services
merc ->> cust: The goods or service cost<br/>ZMK 100 before any fees,<br/>please send me the money, by initiating the transaction
note over cust,PayerFSP: Question 1<br/>On a USSD flow, how do I add<br/>a counter when I have a Merchant ID?
note over cust,PayerFSP: Question 2<br/>On a USSD flow, how do I add<br/>an alternative currency?
rect rgb(100, 100, 100)
    cust ->> PayerFSP: I would like Merchant ID 12345678 <br/>to receive ZMK 100
    activate PayerFSP
    note over cust:Customer Participant<br/>Merchant Alias<br/>[PayIntoID](12345678)
    cust ->> PayerFSP : Pay CheckOutCounterID [000001]
    note over cust:Customer provides<br/>Till Number<br/>[CheckOutCounterID](000001)
end

PayerFSP ->> PayerFSP: 12345678 is not<br/>within this system
PayerFSP ->> Switch: GET /parties/Merchant/12345678
activate Switch
Switch -->> PayerFSP: HTTP 202 (Accepted)
Switch ->> ALS: GET /participants/Merchant/12345678
activate ALS
ALS -->> Switch: HTTP 202 (Accepted)
ALS ->> ALS: Lookup which FSP Merchant<br/>12345678 belongs to.
ALS ->> Switch: PUT /participants/Merchant/12345678<br/>(Merchant's DFSP)
Switch -->> ALS: HTTP 200 (OK)
deactivate ALS
Switch ->> PayeeFSP: GET /parties/Merchant/12345678
activate PayeeFSP
PayeeFSP -->> Switch: HTTP 202 (Accepted)
PayeeFSP -> PayeeFSP: Lookup party information<br/>for 12345678
PayeeFSP ->> Switch: SEE PUT /parties/Merchant/12345678
Switch -->> PayeeFSP: HTTP 200 (OK)
deactivate PayeeFSP
Switch ->> PayerFSP: SEE PUT /parties/Merchant/12345678
PayerFSP -->> Switch: HTTP 200 (OK)
deactivate Switch
PayerFSP ->> cust: Is "ABC Store" correct?
deactivate PayerFSP

```

### PUT /parties/Merchant

```json
PUT /parties
"party"{
    "partyIDInfo": {
        "partyIDType": "Merchant"
        "partyIdentifier": "12345678"
        }
    "name": "ABC Store",
    "receiveCurrencies":[
        "ZMK"
        ]
    "extensionlist": {
        "merchantID": "87654321"
        ,"DBAName": "ABC Store"
        ,"AccountID": "PK23HABB12313123121132"
        ,"location": "{full address}"}

    }
```

### Open Questions

- What if a DFSP has more than one receive currency? In a Smart Phones, I would expect a selection, but how would this work in USSD?
- Extend that problem to consider a merchant account that can receive multiple currencies.
- In a retail transaction, a customer would see a price in a foreign currency - but we need to get that in to a USSD flow somehow, how does the consumer enter correct currency? (whatever is proposed needs to factor the above scenarios)

### Quotes

```mermaid
sequenceDiagram
Title: Process Quotes

autonumber

# declare actors
actor cust as Customer
participant PayerFSP as User's<br/>FSP
participant Switch as Switch
participant ALS as Account<br/>Lookup<br/>Service
participant fxp as FX<br/>Provider
participant PayeeFSP as Merchant's<br/>DFSP
actor merc as Small Merchant

# start flow
cust->>merc: I would like to buy<br/>this goods or service
merc ->> cust: The goods or service cost<br/>100 ZMK before any fees,<br/>please initiate the transaction

rect rgb(100, 100, 100)
    cust ->> PayerFSP: I would like Merchant ID 12345678 <br/>to receive ZMK 100
    activate PayerFSP
    note over cust:Customer Participant<br/>Merchant Alias<br/>[PayIntoID](12345678)
    cust ->> PayerFSP : Pay Till No [Till_ID]
    note over cust:Customer provides<br/>Till Number<br/>[CheckOutCounterID](000001)
end
PayerFSP ->> PayerFSP: Lookup 12345678 (outlined above)
PayerFSP ->> Switch: POST /quotes<br/>(amountType=RECEIVE,<br/>amount=100 ZMK)
note over PayerFSP: SEE POST /quotes
Switch -->> PayerFSP: HTTP 202 (Accepted)
Switch ->> PayeeFSP: POST /quotes<br/>(amountType=RECEIVE,<br/>amount=100 ZMK)
PayeeFSP -->> Switch: HTTP 202 (Accepted)
PayeeFSP ->> PayeeFSP: check inbound currency
PayeeFSP ->> PayeeFSP: I can receive ZMK for this customer,<br/>I do not have MWK - so I need to get an FXP
PayeeFSP ->> Switch: GET /services/FXP
Switch-->> PayeeFSP: HTTP: 202 (Accepted)
Switch ->> ALS: Tell me FXPs
ALS ->> Switch: These are my FXPs: FDH FX
Switch ->> PayeeFSP: These are my FXPs: FDH FX
    note over Switch: SEE PUT /services/FXP
PayeeFSP -->> Switch: HTTP 200
PayeeFSP ->> PayeeFSP: I will use FDH FX
PayeeFSP ->> Switch: Here is the initial version of the transfer.<br/>Please quote me for the currency conversion.
note over PayeeFSP: SEE post /fxQuotes
Switch -->> PayeeFSP: HTTP 202 (Accepted)
Switch ->> fxp: Here is the initial version of the transfer.<br/>Please quote me for the currency conversion.<br/>**POST /fxQuotes**
fxp -->> Switch: HTTP 202 (Accepted)
fxp ->> fxp: OK, so I need to figure this out...
fxp ->> Switch: Send signed conversion object
Switch -->> fxp: HTTP 200 (OK)
Switch ->> PayeeFSP: SEE PUT /fxQuotes
PayeeFSP -->> Switch: HTTP 200 (OK)
PayeeFSP ->> PayeeFSP: Add Fees,<br/>sign the transaction object<br/>and return it to the Debtor FSP
PayeeFSP ->> Switch: SEE PUT /quotes
Switch -->> PayeeFSP: HTTP 200 (OK)
Switch ->> PayerFSP: SEE PUT /quotes
PayerFSP -->> Switch:: HTTP 200 (OK)

```

#### Commentary

During the FX Quote, the FXP can add a fee, they will then set an expiry time and sign the quotation object, create an ILPV4 prepare packet and return it in the intermediary object.

> :exclamation: NOTE: the ILPV4 prepare packet contains the following items, all encoded:  
>  
> - The amount being sent (i.e. in the source currency)  
> - An expiry time  
> - The condition  
> - The name of the fxp  
> - The content of the conversion terms  


### Questions  

- I am reviewing the quotes, and currently I can only see one currency. So in the receive scenario above, the receiving DFSP would get a message saying please accept 100 ZMK. I cannot see where you would say, "but I will send in a currency you need to convert as I am sending in MWF". The receiving DFSP would say great - send it over
- On the Services FXP - are you envisioning the GET /services/FXP to include the desired currency pair (working through that some currency flows are unidirectional and some require a staging currency).
- Or do you see the response to say - FDH FX offers the following Currency Pairs and corridors
- When the Payee DFSP receives the Service response, I assume it might get quotes from all that provide the service pairs. Is that correct?

I see we have a POST fxQuote but a PUT fxQuotes - should they not be the same?

```nano
PayeeFSP -> PayeeFSP: Interoperable fee is 0 ZMK in<br/>Payee FSP for Merchant<br/>Payment, but 1 ZMK in<br/>internal Payee fee for Merchant
PayeeFSP ->> Switch: PUT /quotes/<ID><br/>(transferAmount=100 ZMK)
Switch -->> PayeeFSP: HTTP 200 (OK)
deactivate PayeeFSP
Switch ->> PayerFSP: PUT /quotes/<ID><br/>(transferAmount=100 ZMK)
PayerFSP -->> Switch: HTTP 200 (OK)
deactivate Switch
PayerFSP -> PayerFSP: Fee is 1 ZMK in Payer<br/>FSP for Merchant Payment,<br/>total fee is 1 ZMK
PayerFSP->>cust: Will you approve Merchant Payment<br/>of 100 ZMK to Payee? It will<br/>cost you 1 ZMK in fees.
deactivate PayerFSP

```


### PUT /services/FXP

```json
PUT /services/FXP

"fxpProviders":[
    "FDH FX"
    ]
```

### POST /fxQuotes

```json
    {
    "conversionRequestId": "828cc75f-1654-415e-8fcd-df76cc9329b9"
    , "conversion": {
        "conversionId": "581f68ef-b54f-416f-9161-ac34e889a84b"
        , "counterPartyFsp": "FX Provider"
        , "amountType": "RECEIVE"
        , "sourceAmount": {
            "currency": "MWK",
            "amount": "5731"
            }
        , "targetAmount": {
            "currency": "ZMW"
            }
        , "validity": "2021-08-25T14:17:09.663+01:00"
        }
    }
```

### PUT /fxQuotes  

```json
    PUT /fxQuotes/828cc75f-1654-415e-8fcd-df76cc9329b9

    {
        "condition": "bdbcf517cfc7e474392935781cc14043602e53dc2e8e8452826c5241dfd5e7ab"
        , "conversionTerms": {
            "conversionId": "581f68ef-b54f-416f-9161-ac34e889a84b"
            , "initiatingFsp": "User's FSP"
            , "sourceAmount": {
                "currency": "MWK",
                "amount": "5731"
            }
            , "targetAmount": {
                "currency": "ZMW",
                "amount": "100"
            }
            , "charges": [
                {
                    "chargeType": "Conversion fee"
                    , "sourceAmount": {
                        "currency": "MWK"
                        , "amount": "172"
                    }
                    , "targetAmount": {
                        "currency": "ZMW"
                        , "amount": "3"
                    }
                }
            ]
        }
    }
```

### PUT /quotes  


```json
put /quotes/382987a8-75ce-4037-b500-c475e08c1727

{
    "transferAmount": {
        "currency": "MWS"
        , "amount": "5731"
    }
    , "payeeReceiveAmount": {
        "currency": "ZMW"
        , "amount": "95"
    },
    "payeeFspFee": {
        "currency": "ZMW"
        , "amount": "5"
    }
    , "expiration": "2021-08-25T14:17:09.663+01:00"
    , "ilpPacket:" {
        "transactionId": "d9ce59d4-3598-4396-8630-581bb0551451"
        , "quoteId": "382987a8-75ce-4037-b500-c475e08c1727"
        , "payee": {
            "partyIdInfo": {
            "partyIdType": "MSISDN"
            , "partyIdentifier": "260795390415"
            }
        }
        , "payer": {
            "partyIdInfo": {
                "partyIdType": "MERCHANT"
                , "partyIdentifier": "87654321"
            }
        }
        , "amount": {
            "currency": "MWK"
            , "amount": "5731"
        }
        , "dependents":[
            {
                "intermediary": "FDH_FX"
                , "condition": "bdbcf517cfc7e474392935781cc14043602e53dc2e8e8452826c5241dfd5e7ab"
            }
        ]
        , "transactionType": {
            "scenario": "TRANSFER"
            , "initiator": "PAYER"
            , "initiatorType": "CONSUMER"
        }
    }
        , "condition": "BfNFPRgfKF8Ke9kpoNAagmcI4/Hya5o/rq9/fq97ZiA="
    }


```

## Transfer

```mermaid
sequenceDiagram
Title: Process Transfer

autonumber

# declare actors
actor cust as Customer
participant PayerFSP as User's<br/>FSP
participant Switch as Switch
participant ALS as Account<br/>Lookup<br/>Service
participant fxp as FX<br/>Provider
participant PayeeFSP as Merchant's<br/>DFSP
actor merc as Small Merchant

# start flow
cust ->> PayerFSP: Perform transaction
PayerFSP ->> Switch: SEE POST /transfers
Switch -->> PayerFSP: HTTP 202 (Accepted)
Switch ->> Switch: Does the debtor hold an account in MWK? Yes.
Switch ->> Switch: Make the reservation against their account.
note over Switch: <br/>Reservations:<br/><br/>NBS_Bank has a reservation of 5731 MWK
Switch ->> PayeeFSP: SEE POST /transfers
PayeeFSP -->> Switch: HTTP 202 (Accepted)
PayeeFSP ->> PayeeFSP: Do I need to activate currency conversion?<br/>Yes, I do
PayeeFSP ->> Switch: SEE POST /fxTransfers
Switch -->> PayeeFSP: HTTP 202 (Accepted)
Switch->Switch: OK, so this is an FX confirmation.
Switch->Switch: Does the sender have an account in this currency?<br/>No, it doesn't.
Switch->Switch: Liquidity check and reserve on fxp's account
note over Switch :Reservations:<br/><br/>NBS_Bank has a reservation of 5731 MWK<br/>FDH_FX has a reservation of 97 ZMW
Switch->fxp:Please confirm the currency conversion part of the transfer<br/>** POST /fxTransfers**
fxp-->Switch:202 I'll get back to you
fxp->fxp:Is all this OK?<br/>If so, send the fulfilment back
fxp->Switch:Confirmed. Here's the fulfilment
note over fxp: SEE PUT /fxTransfers
Switch-->fxp:200 Gotcha
Switch->Switch:Check fulfilment matches and cancel if not.
alt Conversion failed
    Switch->PayeeFSP: SEE ERROR PUT/fxTransfers
else Conversion succeeded
Switch->PayeeFSP:Conversion succeeded subject to transfer success<br/>**PUT /fxTransfers/77c9d78d-c26a-4474-8b3c-99b96a814bfc**
end
PayeeFSP-->Switch:200 Gotcha
PayeeFSP->PayeeFSP:Let me check that the terms of the transfer<br/>are the same as the ones I agreed to
PayeeFSP->PayeeFSP:Yes, they do. I approve the transfer
PayeeFSP->Switch: SEE PUT /transfers
Switch-->PayeeFSP:200 Gotcha
Switch->Switch:Is there a dependent transfer?<br/>Yes, there is.
Switch->Switch:Is this dependency against the debtor party to the transfer?<br/>No, it isn't.
Switch->Switch:Create an obligation from<br/>the party named in the dependency (the fxp)<br/>to the creditor party
Switch->Switch:Is the transfer denominated in the currency of the amount?<br/>Yes, it is.
Switch->Switch:Create an obligation from<br/>the debtor party to<br/>the party named in the dependency (the fxp)
Switch->fxp:SEE PATCH /fxTransfers
fxp->fxp: Let's just check: does this match the stuff I sent?
fxp->fxp:It does. Great. I'll clear the conversion
fxp->Switch:200 Gotcha
note over Switch: Ledger positions:<br/>NBS_Bank has a debit of 5731 MWK<br/>FDH_FX has a credit of 5731 MWK<br/>FDH_FX has a debit of 97 ZMW<br/>Zoona has a credit of 97 ZMW
Switch->PayerFSP:Transfer is complete<br/>**PUT /transfers/c720ae14-fc72-4acd-9113-8b601b34ba4d**
PayerFSP-->Switch:200 Gotcha
PayerFSP->PayerFSP:Commit the funds in my ledgers
PayerFSP->Amanda:Transfer was completed successfully

```


### Comments

Check the legacy double entry for the reservations - something feels wrong

### POST /transfers

```json
POST /transfers

    {
        "transferId": "c720ae14-fc72-4acd-9113-8b601b34ba4d"
        , "payeeFsp": "Zoona"
        , "payerFsp": "NBS_Bank"
        , "amount": {
            "currency": "MWK"
            , "amount": "5731"
        }
        , "transaction": {
            "transactionId": "d9ce59d4-3598-4396-8630-581bb0551451"
            , "quoteId": "382987a8-75ce-4037-b500-c475e08c1727"
            , "payee": {
                "fspId": "Zoona"
                , "partyIdInfo": {
                    "partyIdType": "MSISDN"
                    , "partyIdentifier": "260795390415"
                    }
            }
        }
        , "payer": {
             "fspId": "NBS_Bank"
            , "partyIdInfo": {
                "partyIdType": "MSISDN"
                , "partyIdentifier": "265314118010"
            }
        }
        , "dependents":[
            {
                "intermediary": "FDH_FX"
                , "condition": "bdbcf517cfc7e474392935781cc14043602e53dc2e8e8452826c5241dfd5e7ab"
            }
        ]
    }

```

### POST /fxTransfers

```json
POST /fxTransfers

    {
        "commitRequestId": "77c9d78d-c26a-4474-8b3c-99b96a814bfc"
        , "relatedTransactionId": "d9ce59d4-3598-4396-8630-581bb0551451"
        , "requestingFsp": "Zoona"
        , "respondingfxp": "FDH_FX"
        , "sourceAmount": {
            "currency": "MWK",
            "amount": "5731"
        }
        , "targetAmount": {
            "currency": "ZMW",
            "amount": "97"
        }
        , "condition": "bdbcf517cfc7e474392935781cc14043602e53dc2e8e8452826c5241dfd5e7ab"
    }
```

### PUT /fxTransfers

```JSON
**PUT /fxTransfers/77c9d78d-c26a-4474-8b3c-99b96a814bfc**

{
    "fulfilment": "188909ceb6cd5c35d5c6b394f0a9e5a0571199c332fbd013dc1e6b8a2d5fff42"
    , "completedTimeStamp": "2021-08-25T14:17:08.175+01:00"
    , "conversionState": "RESERVED"
}
```

```JSON
PUT /fxTransfers/77c9d78d-c26a-4474-8b3c-99b96a814bfc/error

{
    "errorCode": "9999"
    , "errorDescription": "Whatever the error was"
}
```

### PUT /transfers

```JSON  
PUT /transfers/c720ae14-fc72-4acd-9113-8b601b34ba4d

{
    "fulfilment": "mhPUT9ZAwd-BXLfeSd7-YPh46rBWRNBiTCSWjpku90s"
    , "completedTimestamp": "2021-08-25T14:17:08.227+01:00"
    , "transferState": "COMMITTED"
}
```

### PATCH /fxTransfers

The transfer succeeded.
You can clear it in your ledgers

```JSON
**PATCH /fxTransfers/77c9d78d-c26a-4474-8b3c-99b96a814bfc**

{
    "fulfilment": "2e6870fb4eda9c2a29ecf376ceb5b05c"
    , "completedTimeStamp": "2021-08-25T14:17:08.175+01:00"
    , "conversionState": "COMMITTED"
}
```

## Other text

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