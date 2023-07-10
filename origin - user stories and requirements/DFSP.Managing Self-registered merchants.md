## Managing Self-registered merchants
**As a** DFSP user, **I want to** be able to review merchant registration requests and approve or decline them to ensure that only authorized merchants enter the system.
**As a** DFSP checker, **I want to** be able to review rejected pending/approved pending self-registered merchants done by maker **so that** I can approve/reject the action.

### Acceptance Criteria
* Self-registry workflow
    * responsible person from merchant entity will create an account in the portal with following inforamtion 
        * email/phone number
        * password 
    * after successfully created the account, merchant will start filling out the application for merchant acquisition.
    * Self-registered merchant will be with registration status “PENDING”
    * DFSP maker will approve/reject the merchants’ applications 
    * When DFSP maker approved/rejected the application registration status will changed to “APPROVE_PENDING” or “REJECT_PENDING”
    * Sub-user story for "Registration Status" notification
        * **As a** merchant, **I want to** be notified and able to check status of my registry( pending,successful,rejected)  **so that** I can take further action to receive payment from my clients
        * Acceptance Criteria 
            * Email/phone number notification about registration status change notification.
            * Registration status progress should be up to date reflection on portal.
    * "Approved" or "Rejected" registration status will be notified to the merchant. 
        * Approved merchants will be abled to access their alias and QR codes from the portal 
        * Registration status of Rejected merchants by DFSP checker will be rejected and will be notify to merchant to refine the application form
