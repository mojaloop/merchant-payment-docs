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

A DFSP will onboard their Merchant into a Central Merchant Registry via API/portal interface. The expectation is that this flow will also capture all the relevant information required to acquire the merchant.

The working assumption is that the merchant Know your Business (KYB) process is manual, however the system can consider this being done automatically in a future iteration

Note the merchant registry is now populated with data from the Merchant acquirer system, but the assignment of an alias will need to be completed, and once the state of a registration is complete, the information will be provided back to the maker, so they can now inform the merchant of their aliases.

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

        macq ->> DFSPMake: Notify updated registration status of records, including all aliases that have been established for a merchant
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
