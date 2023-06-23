---  
sidebar_position: 2  
sidebar_label: register_merchant
title: Register Merchant
date: 2023-06-01 09:53:33
author: Rob Reeve
description: high level overview of the process to register a merchant
---  

## Merchant Acquiring to Oracle

```mermaid
---
title: Merchant to Switch Relatiions
---
flowchart LR
    merc[Merchant]
    fsp1[DFSP Acquirer 1]
    fsp2[DFSP Acquirer 2]
    switch[Switch]

merc-->fsp1
merc-->fsp2
fsp1-->switch
fsp2-->switch

```

A merchant should be given the flexibility to have more than one DFSP acquiring them - to provide resiliency, and commercial leverage.

```mermaid
---
title: Merchant acquirer to Switch system Relatiions
---
flowchart LR

corebank[Core banking]
hosted[Hosted Merchant Acquiring]
own[Self managed acquiring]
subgraph DFSP domain
corebank-->own
end
corebank-->hosted
```

The above diagram identifies the different models we need to consider in the creation of a service. A merchant acquirer might have its own services, which simplifies the interaction with the switch as it should all happen with the DFSP domain.

The design needs to consider how information from the Hosted Merchant Acquiring is provided back to the DFSP so they can 

## Overview

The onboarding of a merchant in to the merchant registry, means that they are first acquired (or accepted) by a Digital Financial Service Provider (DFSP). We achieve this in different ways, we cover these in the following documentation.

- DFSP onboards merchant entering data in to the portal
- DFSP onboards merchant in their own system and shares the information with the Merchant registry.
- Merchant self registration (they enter their details in to a scheme portal and then enter a portal to be acquired by DFSP(s))

As a DFSP may not have an acquiring system, this document covers onboard by a DFSP in a portal first. 

## DFSP onboarding their merchant and assign an alias  

A DFSP will onboard their Merchant into a Central Merchant Registry via API/portal interface. The expectation is that this flow will also capture all the relevant information required to acquire the merchant.

The working assumption is that the merchant Know your Business (KYB) process is manual, the system can consider this could be done automatically in a future iteration

> It is worth highlighting the anticipated payment flow would have potentially two parts for a payment - the first step capturing the merchant alias (for all merchants), the second capturing the final till to allow for payment reconciliation (for merchants that have more than one payment point). The actual detail of these flows will be covered in other stories, but it is highlighted to point out that the Merchant Registry will use the Merchant ID and the information to support reconciliation (```CheckoutCounterID```) will be part of the transaction, but not relevant to the Switch.

Once the merchant or the DFSP has registered the information in the Acquirer system, the portal passes the necessary information to the Merchant Registry, where an alias is either validated or created

```mermaid

sequenceDiagram
    actor merc as Small Merchant
    participant dfspapp as DFSP Application process
    actor DFSPMake as DFSP Maker
    actor DFSPCheck as DFSP Checker
    participant macq as Merchant Acquirer System
    participant oracle as Merchant Registry System

    merc ->> dfspapp: application process 
    
    Note over dfspapp: not related to switch

    dfspapp ->> DFSPMake: extract merchant data
    
    Note over DFSPMake: Import merchant records

    DFSPMake ->> macq: enter Merchant Data

    macq ->> macq: data stored
    macq->>DFSPMake: pending

    macq-->>DFSPCheck: You have information to review

    DFSPCheck->>DFSPCheck: KYB process

    alt Approved
        DFSPCheck->>macq: approves data
        macq ->> macq: Update status 'succesful'
        macq->>oracle: submit data for registation

        oracle->>oracle: registered
        alt alias provided
            oracle->>oracle: check unique alias
            oracle->>macq: registered with alias
        else new alias
            oracle->>oracle: new alias created
            oracle->>macq: registered and new alias
        else FUTURE - blocked
            oracle->>oracle: merchant on block list
            oracle->>macq: NEED TO AGREE
        end

        macq ->> DFSPMake: Notify updated registration status of records, including alias created for a merchant
        DFSPMake->>dfspapp: Notification account created and alias assigned
    else Rejected
        DFSPCheck->>macq: Rejected action
        macq -->>DFSPCheck: Ask reason for rejection
        DFSPCheck -->> macq: Update reasons for rejections
        macq -->> macq: Registration status of rejected action records will change as 'rejected'
        macq -->> DFSPMake: Notify that registration status of each record will be remain the same as before the  status change request    
    end
    
```

## DFSP onboarding their merchant and reuse an alias  

## Medium Merchant

aliases

## Complex Merchant

aliases
