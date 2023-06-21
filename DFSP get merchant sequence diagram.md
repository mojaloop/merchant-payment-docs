---  
sidebar_position: 2  
sidebar_label: register_merchant
title: Register Merchant
date: 2023-06-21 14:53:33
author: Rob Reeve
description: high level overview of the process to get participants to pay merchant
---  

## Merchant Acquiring to Oracle

The following is the sequence that shows how the Merchant Registry would be used in a basic flow

```mermaid
sequenceDiagram

    actor Payer as Customer
    participant PayerFSP as Payer FSP
    participant SWITCH as Payment Switch

    note left of PayerFSP:Customer provides<br/>Merchant Alias<br/>Till_ID
    Payer->>PayerFSP: Pay Merchant X at till ABC
    PayerFSP->>+SWITCH: GET - /participants/Merchant/{ID}<br/>(where ID=Alias)
    SWITCH-->>+PayerFSP: http/202 accepted
    SWITCH->>+Oracle: GET - /participants/Merchant/{ID}
    note left of Oracle: idType="Merchant_ID"<br/>route to Merchant Registry
    Oracle-->>+SWITCH: Return list of Particpant Information
    SWITCH->>+PayerFSP: PUT - /participants/Merchant/{ID}<br/>(where ID=Alias)
```
