
## User Story:  
**As** a DFSP system admin I **want to** add small merchants in merchant registry system **so that** they can be included in mojaloop system.

## Acceptance Criteria:
* Merchant Full KYB information is stored in the Merchant Acquirer System Portal.
* The DFSP extracts the necessary merchant data from the merchant acquirer system to submit to merchant registry.
    - ** to define necessary data to upload in merchant registry module **
* The DFSP Maker imports the merchant records to merchant registry system.
* The DFSP Maker receives a pending status notification from the Merchant Acquirer System Portal.
* The DFSP Checker performs the Know Your Business (KYB) process.
* If approved:
   - The DFSP Checker approves the data.
   - The Merchant Acquirer System Portal updates the status of the merchant as 'successful'.
   - The data is sent to the Merchant Registry System for registration.
   - If a unique alias is provided from DFSP:
     - The Merchant Registry System checks for a unique alias.
     - The Merchant Registry System informs the Merchant Acquirer System Portal about successful registration with the provided alias.
   - If a new alias is generated:
     - The Merchant Registry System creates a new alias.
     - The Merchant Registry System informs the Merchant Acquirer System Portal about successful registration with the new alias.
   - If the merchant is on the block list:
     - The Merchant Registry System identifies the merchant as blocked.
     - The Merchant Registry System informs the Merchant Acquirer System Portal about the need for further agreement.
   - The Merchant Acquirer System Portal is notified of the updated registration status of the records.
* If rejected:
    - The DFSP Checker rejects the action.
    - The Merchant Acquirer System Portal asks for the reason for rejection.
    - The DFSP Checker updates the reasons for rejection.
    - The Merchant Acquirer System Portal updates the registration status of the rejected action records as 'rejected'.
    - The Merchant Acquirer System Portal is notified that the registration status of each record remains the same as prior to the status change request.

**remark:** current acceptance criteria is written with the assumption that merchant registry module is part of merchant acquisition. If we want to seperate merchant registry from merchant acquisition completely, we will need to refine the acceptance criteria. 


[sequence diagram](https://github.com/mojaloop/merchant-payment-docs/blob/master/DFSP%20merchant%20onboard%20Sequence%20Diagram.md)

