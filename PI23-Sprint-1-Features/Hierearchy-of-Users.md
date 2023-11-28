# Hierearchy of Users

To create users and subsequent groups in a multi-tenant scenario, the goal is to reduce the administrative burden of Hub Admins, and allow the users to be self sufficient

The creation of each of the Super Users should be supported by a documented approval process, to prevent authority being granted inadvertently.

## Super Users  

Once a Super User has been created, they can create only three Hub admin accounts. Once three Hub Admin accounts have been created, the SuperUser is disabled

## Hub Admin Users

Once a Hub Admin has been created they can create other Hub Admins or a DFSP super user and assign that user account to a specific DFSP and the groups it manages. Each user creation will have a maker and checker step

```mermaid

flowchart TD
    SU["Super User"]
    HA1["Hub Admin 1
    Maker or Checker"]
    HA2["Hub Admin 2
    Maker or Checker"]
    HA3["Hub Admin 3
    Maker or Checker"]
    DS1SU["DFSP 1 Super User"]
    DS2SU["DFSP 2 Super User"]


    SU -->|can create|HA1
    SU -->|can create|HA2
    SU -->|can create|HA3
    HA1-->|can create|HA3 
    HA2-->|can create|HA3 
    HA1-->|can create|DS1SU 
    HA2-->|can create|DS1SU
    HA3-->|can create|DS1SU
    HA1-->|can create|DS2SU
    HA2-->|can create|DS2SU
    HA3-->|can create|DS2SU
 
```

## DFSP Admin Users

It is worth noting that a DFSP Admin can only assign membership to groups of that DFSP

```mermaid

flowchart TD
    DS1SU["DFSP 1 Super User"]
    DS1A1["DFSP 1 Admin 1"]
    DS1A2["DFSP 1 Admin 2"]
    DS1A3["DFSP 1 Admin 3"]
    DS1U1["DFSP 1 User 1"]
    DS1U2["DFSP 1 User ..."]
    DS1U3["DFSP 1 User n"]


    DS1SU -->|can create|DS1A1
    DS1SU -->|can create|DS1A2
    DS1SU -->|can create|DS1A3
    DS1A1 --> DS1A3
    DS1A1 --> DS1U1
    DS1A1 --> DS1U2
    DS1A1 --> DS1U3
    DS1A2 --> DS1A3
    DS1A2 --> DS1U1
    DS1A2 --> DS1U2
    DS1A2 --> DS1U3
    DS1A3 --> DS1U1
    DS1A3 --> DS1U2
    DS1A3 --> DS1U3

```