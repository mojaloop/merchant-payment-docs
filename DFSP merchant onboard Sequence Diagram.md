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

## DFSP onboarding their merchant and assign an alias  

DFSP onboard their Merchant into Central Merchant Registry via API/portal interface

Working assumption for now is that the merchant KYB process is manual, however the system can consider this being done automatically

```mermaid

sequenceDiagram
    actor merc as Small Merchant
    participant dfspapp as DFSP Application process
    actor DFSPMake as DFSP Maker
    actor DFSPCheck as DFSP Checker
    participant macq as Merchant Acquirer System Portal
    participant oracle as Merchant Registry System

    merc ->> dfspapp: application process 
    
    Note over dfspapp: not related to switch

    dfspapp ->> DFSPMake: extract merchant data

    Note over DFSPMake: Import merchant records

    DFSPMake ->> macq: enter Merchant Data

    macq ->> macq: data stored
    macq->>DFSPMake: pending

    macq-->>DFSPCheck: You have things to review

    DFSPCheck->>DFSPCheck: KYB process

    alt Approved
        DFSPCheck->>macq: approves data
        macq ->> macq: Update status 'succesful'
        macq->>oracle: data for registation

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

        macq -->> DFSPMake: Notify updated registration status of records
    else Rejected
        DFSPCheck->>macq: Rejected action
        macq -->>DFSPCheck: Ask reason for rejection
        DFSPCheck -->> macq: Update reasons for rejections
        macq -->> macq: Registration status of rejected action records will change as 'rejected'
        macq -->> DFSPMake: Notify that registration status of each record will be remain the same as prior to status change request    
    end
    
```

## DFSP onboarding their merchant and reuse an alias  

## Medium Merchant

aliases

## Complex Merchant

aliases
