---  
sidebar_position: 2  
sidebar_label: Account Mapping
title: Account Mapping Samples
date: 2023-07-05 10:18:26
author: Rob Reeve
description: 
---  


## Introduciton  

This document articulates the scenarios that exist and the design has factored.

## Different Stages of a merchant

Starting with a Simple merchant that has one location and counter, working to a complex merchant with multiple locations and counters.

The design considers whether the receiving account is mapped to a Merchant (Merchant Account), a location/region (Location Account) or a unique counter (Counter account). The counter sequencing also considers whether it is reset for each location (Unique counter - Location) or if every counter is unique (Merchant).

| **Name**        | **ID** | **Locations** | **Counters per location** | **Merchant account** | **Location account** | **Counter account** | **Unique Counter** |
|-----------------|--------|---------------|---------------------------|----------------------|----------------------|---------------------|--------------------|
| **Merchant 1**  | **M001**   | Single        | Single                    | Yes                  | Yes                  | Yes                 | Both               |
| **Merchant 2**  | **M002**   | Single        | Multiple                  | Yes                  | Yes                  | No                  | Both               |
| **Merchant 3**  | **M003**   | Single        | Multiple                  | No                   | No                   | Yes                 | Both               |
| **Merchant 4**  | **M004**   | Multiple      | Single                    | Yes                  | No                   | No                  | Location           |
| **Merchant 5**  | **M005**   | Multiple      | Single                    | Yes                  | No                   | No                  | Merchant           |
| **Merchant 6**  | **M006**   | Multiple      | Single                    | No                   | Yes                  | Yes                 | Location           |
| **Merchant 7**  | **M007**   | Multiple      | Single                    | No                   | Yes                  | Yes                 | Merchant           |
| **Merchant 8**  | **M008**   | Multiple      | Multiple                  | Yes                  | No                   | No                  | Location           |
| **Merchant 9**  | **M009**   | Multiple      | Multiple                  | Yes                  | No                   | No                  | Merchant           |
| **Merchant 10** | **M010**   | Multiple      | Multiple                  | No                   | Yes                  | No                  | Location           |
| **Merchant 11** | **M011**   | Multiple      | Multiple                  | No                   | Yes                  | No                  | Merchant           |
| **Merchant 12** | **M012**   | Multiple      | Multiple                  | No                   | No                   | Yes                 | Location           |
| **Merchant 13** | **M013**   | Multiple      | Multiple                  | No                   | No                   | Yes                 | Merchant           |

This allows us to create the following sample data for each of these merchants.

| **Merchant ID** | **Merchant Name** | **PayIntoID (Alias)** | **CheckOutCounter_ID** | **DFSP_ID** | **Account** | **Contact Number** |
|-----------------|-------------------|-----------------------|------------------------|-------------|--------------|--------------------|
| **M001**        | 001 Store         | M001                  | C001                   | DFSP1       | A123         |                    |
|  |  |  |  |  |  |  |
| **M002**        | 002 Store         | M002                  | C001                   | DFSP1       | A124         |                    |
|  |  |  |  |  |  |  |
|         | 002 Store         | M002                  | C002                   | DFSP1       | A124         |                    |
|  |  |  |  |  |  |  |
| **M003**        | 003 Store         | M003                  | C001                   | DFSP1       | A125         |                    |
|         | 003 Store         | M004                  | C002                   | DFSP1       | A126         |                    |
|  |  |  |  |  |  |  |
| **M004**        | 004 Store - Loc 1 | M005                  | C001                   | DFSP1       | A127         |                    |
|         | 004 Store - Loc 2 | M005                  | C001                   | DFSP1       | A127         |                    |
|  |  |  |  |  |  |  |
| **M005**        | 005 Store - Loc 1 | M006                  | C001                   | DFSP1       | A128         |                    |
|         | 005 Store - Loc 2 | M006                  | C002                   | DFSP1       | A128         |                    |
|  |  |  |  |  |  |  |
| **M006**        | 006 Store - Loc 1 | M007                  | C001                   | DFSP1       | A129         |                    |
|         | 006 Store - Loc 2 | M008                  | C001                   | DFSP1       | A130         |                    |
|  |  |  |  |  |  |  |
| **M007**        | 007 Store - Loc 1 | M009                  | C001                   | DFSP1       | A131         |                    |
|         | 007 Store - Loc 2 | M010                  | C002                   | DFSP1       | A132         |                    |
|  |  |  |  |  |  |  |
| **M008**        | 008 Store - Loc 1 | M011                  | C001                   | DFSP1       | A133         |                    |
|         | 008 Store - Loc 1 | M011                  | C002                   | DFSP1       | A133         |                    |
|         | 008 Store - Loc 2 | M011                  | C001                   | DFSP1       | A133         |                    |
|         | 008 Store - Loc 2 | M011                  | C002                   | DFSP1       | A133         |                    |
|  |  |  |  |  |  |  |
| **M009**        | 009 Store - Loc 1 | M012                  | C001                   | DFSP1       | A134         |                    |
|         | 009 Store - Loc 1 | M012                  | C002                   | DFSP1       | A134         |                    |
|         | 009 Store - Loc 2 | M012                  | C003                   | DFSP1       | A134         |                    |
|         | 009 Store - Loc 2 | M012                  | C004                   | DFSP1       | A134         |                    |
|  |  |  |  |  |  |  |
| **M010**        | 010 Store - Loc 1 | M013                  | C001                   | DFSP1       | A135         |                    |
|         | 010 Store - Loc 1 | M013                  | C002                   | DFSP1       | A135         |                    |
|         | 010 Store - Loc 2 | M014                  | C001                   | DFSP1       | A136         |                    |
|         | 010 Store - Loc 2 | M014                  | C002                   | DFSP1       | A136         |                    |
|  |  |  |  |  |  |  |
| **M011**        | 011 Store - Loc 1 | M015                  | C001                   | DFSP1       | A137         |                    |
|         | 011 Store - Loc 1 | M015                  | C002                   | DFSP1       | A137         |                    |
|         | 011 Store - Loc 2 | M016                  | C003                   | DFSP1       | A138         |                    |
|         | 011 Store - Loc 2 | M016                  | C004                   | DFSP1       | A138         |                    |
|  |  |  |  |  |  |  |
| **M012**        | 012 Store - Loc 1 | M017                  | C001                   | DFSP1       | A139         |                    |
|         | 012 Store - Loc 1 | M018                  | C002                   | DFSP1       | A140         |                    |
|         | 012 Store - Loc 2 | M019                  | C001                   | DFSP1       | A141         |                    |
|         | 012 Store - Loc 2 | M020                  | C002                   | DFSP1       | A142         |                    |
|  |  |  |  |  |  |  |
| **M013**        | 013 Store - Loc 1 | M021                  | C001                   | DFSP1       | A143         |                    |
|         | 013 Store - Loc 1 | M022                  | C002                   | DFSP1       | A144         |                    |
|         | 013 Store - Loc 2 | M023                  | C003                   | DFSP1       | A145         |                    |
|         | 013 Store - Loc 2 | M024                  | C004                   | DFSP1       | A146         |
|  |  |  |  |  |  |  |

To ensure that the alias creation works as designed, the following use cases are then worked through to ensure the user experience is acceptable

## Test Scenarios

1. New Merchant - Add Merchant
2. New Merchant Location - Add Location
3. New Counter at a Location - Add Counter
4. Close Merchant Location - Close location
5. Close Merchant Counter - Close Counter

### Complex Scenario - Merchant changes to another DFSP  

The working assumption is if the Merchant changes DFSP the Alias should not change.  

| **Merchant ID** | **Merchant Name** | **PayIntoID (Alias)** | **CheckOutCounter_ID** | **DFSP_ID** | **Account** | **Contact Number** |
|-----------------|-------------------|-----------------------|------------------------|-------------|--------------|--------------------|
| **M00003**      | XYZ Store - Loc 1 | M000030               | C00001                 | DFSP2       | DFSP2AC1     | +923212430237      |
| **M00003**      | XYZ Store - Loc 1 | M000031               | C00002                 | DFSP2       | DFSP2AC1     | +923212430236      |
| **M00003**      | XYZ Store - Loc 2 | M000032               | C00003                 | DFSP2       | DFSP2AC2     | +923212430238      |

### Complex Scenario - Existing Merchant and Counter IDs in Country

The working assumption is that the merchant has the least amount of work to do to support the change to an interoperable system.

MTN has Merchants all with existing IDs at the counter:

* MTN001
* MTN002
* MTN003

AIRTEL has Merchants all with existing IDs at the counter:

* AIRTEL001
* AIRTEL002
* AIRTEL003

This is further complicated as MTN003 and AIRTEL002 are the same merchant - all with two IDs at the counter
