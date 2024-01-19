# Release Notes: Mojaloop Merchant Registry System

## Merchant Registry and Acquiring Portal

The Merchant Registry serves as a centralized repository, storing vital data on Digital Financial Service Providers (DFSPs) and merchant alias mappings. The Acquiring Portal, an additional module for DFSPs, facilitates efficient merchant information management and QR code generation. 

When a consumer initiates a payment, Mojaloop's Account Lookup Service interacts with the Merchant Registry, identifying if that merchant exist in the system and associated DFSP. This information is relayed to the payer DFSP and the rest of the payment transaction workflow follow.


![Merchant](https://github.com/mojaloop/merchant-payment-docs/assets/145109675/303ebd5b-f38f-4293-ad8c-953ac2cbd129)


## Key Features:

* Merchant Management:
    * Registry Form
        * This feature is for registering a simple merchant to the acquirer system.
    * Registration Save As Draft Feature
        * This feature allows DFSP maker usres to save an application form that is still in process as a draft.
    * Registry form records reports
        * It shows relevant reports that include data from users' own organizations.
        * DFSP maker can view all merchant records that are already successfully registered and those that were approved or rejected by DFSP checker.
        * DFSP checker can view all merchant records that have already been successfully registered, and he can approve or reject the records that the maker added.
    * Draft Application List
        * This feature is for showing the draft application list in a table and allowing users to reload the work-in-progress of the saved draft form.
    * Back and Update Record Feature
        * This feature allows users to edit the data of the previous page of the form by providing a “back” button.
    * Report Download
        * This feature is for downloading filtered records from each report based on selected criteria.
    * Revert Record Feature
        * This feature allows users to fill out the revert form applications by selecting the one for which new information is received.
    * Data Retrieval
        * This feature allows the DFSP checker to review the data that is related to his DFSP to be aware of which records have been approved and which have been rejected.
* Alias allocation to merchants
* QR code generation upon alias allocation
    * QR codes are generated based on EMV Co standard
* Entity Management:
	* DFSP (created by Hub Admin)
	* Merchants (created by DFSP)

* User Management:
	* Hub Users (creation, update, status change)
	* DFSP Users (creation, update, status change)


## Improvements:
* Integration with UI and backend for complex merchants (multiple locations and check-out counters)
* Introduction of 2-Factor Authentication in the merchant acquiring system portal
* Integration with Keycloak, Mojaloop authentication, and authorization methods
* Implementation of bulk data input in the merchant acquiring system
* Integration of the DFSP list with an API from Mojaloop Hub in the DFSP onboarding process instead of adding a text field for the DFSP name.

## In Pipeline:
* Self-registration for new merchants on the portal
* Status tracking for new and existing merchant applications
* Request mechanism for merchants to change their DFSP


