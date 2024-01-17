# Merchant Registry System
The Merchant Registry serves as a centralized repository, storing vital data on Digital Financial Service Providers (DFSPs) and merchant alias mappings. The Acquiring Portal, an additional module for DFSPs, facilitates efficient merchant information management and QR code generation. 
When a consumer initiates a payment, Mojaloop's Account Lookup Service interacts with the Merchant Registry, identifying if that merchant exist in the system and associated DFSP. This information is relayed to the payer DFSP and the rest of the payment transaction workflow follow.

#### For the development repository
[Merchant Payment Development Repository](https://github.com/mojaloop/merchant-registry-svc)

## Feature Summary

* Merchant Management:
  * Registry Form
    * This feature is for registering a simple merchant to the acquirer system.
Registration Save As Draft Feature
This feature allows DFSP maker usres to save an application form that is still in process as a draft.
Registry form records reports
It shows relevant reports that include data from users' own organizations.
DFSP maker can view all merchant records that are already successfully registered and those that were approved or rejected by DFSP checker.
DFSP checker can view all merchant records that have already been successfully registered, and he can approve or reject the records that the maker added.
Draft Application List
This feature is for showing the draft application list in a table and allowing users to reload the work-in-progress of the saved draft form.
Back and Update Record Feature
This feature allows users to edit the data of the previous page of the form by providing a “back” button.
Report Download
This feature is for downloading filtered records from each report based on selected criteria.
Revert Record Feature
This feature allows users to fill out the revert form applications by selecting the one for which new information is received.
Data Retrieval
This feature allows the DFSP checker to review the data that is related to his DFSP to be aware of which records have been approved and which have been rejected.
Alias allocation to merchants
QR code generation upon alias allocation
QR codes are generated based on EMV Co standard

- Entity Management:
	- DFSP (created by Hub Admin)
	- Merchants (created by DFSP)

- User Management:
	- Hub Users (creation, update, status change)
	- DFSP Users (creation, update, status change)


## QA Test Case Results
* [Final Result for first sprint and second sprint](https://docs.google.com/spreadsheets/d/1piKniAwkdBTP5Vgk1KH5ERYXyUujrHVLQ2j_Fz9fQm8/edit?usp=sharing)
* [Final Result for third sprint](https://docs.google.com/spreadsheets/d/1Kv1YHTfS8JW4gBPKd-ZvQmWiMfgl2OmNsiwd9Ux9ls0/edit?usp=sharing)

## Some features that can be added in future
* Although the development has covered complex merchants according to data structure, it still needs to connect with the UI and backend. Complex merchants mean merchants with multiple locations and multiple check-out counters.
* QR code generation for merchant alias 
* 2 Factor Authentication in merchant acquiring system portal
* Connecting with Keycloak, mojaloop authentication and authorization methods
Bulk data input in merchant acquiring system


![ERD Design](./Entity-Relations-Diagram.png)


