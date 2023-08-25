# Portal User Management 

**As a** super admin of DFSP, **I want** to be able to assign users to different roles **so that** people from my DFSP organization can start managing merchant records.

* As a defualt state, one super admin user of that DFSP users will be assigned at DFSP onboarding state.

## Acceptance Criteria 

* following permissions and roles will be included in the system. 
* Keycloak will be used for user identity management and data access and action permission management will be done by own backend system.
* following are the list of default roles and permission list in merchant acquiring sytem. 
  * Super Admin User  
    * write(create,edit) access to acqquring registry form
    * approve,reject,revert action for merchant records.
      * exception: records created by the same user CANNOT be approved by the user.
    * Read access to table of all merchant table
    * Read access to "to-be-reverted merchants" table
    * Read access to "Pending-Merchants"table
    * Assign new users[Admin,Operators,Auditors] to roles
    * Update,Delete user records in their organization
    * merchant data export
  * Admin user
    * write(create,edit) access to acqquring registry form
    * approve,reject,revert action for merchant records.
      * exception: records created by the same user CANNOT be approved by the user.
    * Read access to table of all merchant table
    * Read access to "to-be-reverted merchants" table
    * Read access to "Pending-Merchants"table
    * Assign new users[Operators,Auditors] to roles
    * Update,Delete user records in their organization
    * merchant data export
  * Operator  
    * write(create,edit) access to acqquring registry form [can create new merchant records]
    * approve,reject,revert action for merchant records.
    * exception: records created by the same user CANNOT be approved by the user.
    * Read access to table of all merchant table
    * Read access to "to-be-reverted merchants" table
    * Read access to "Pending-Merchants"table
    * merchant data export
  * Auditor  
    * Read access to table of all merchant table
    * Read access to "to-be-reverted merchants" table
    * Read access to "Pending-Merchants"table

## Adding new users to the system workflow

* Adding email, username and assigned role in user management screen
* System will send email from the form a new email that instruct to set password
* New user set password and confirm password
* New user login to the portal with new password and start performing available actions

## Checking For Strong password

* following creteria will be validated while user set their password for the sysytem
  * minimum number of character : 8
  * there must be AT LEAST one capital letter, number,special charater and small letter.

## Out of scope items

* editing roles and permissions
* adding new roles
* 2 factor authentication

## Design file

* [Role Management](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-8023&viewport=644%2C-1531%2C0.48&t=3nzJNy4MNiGvPOBV-1&scaling=scale-down&starting-point-node-id=1435%3A8023&show-proto-sidebar=1&mode=design)
* [User Management](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-13552&viewport=644%2C-1531%2C0.48&t=3nzJNy4MNiGvPOBV-1&scaling=scale-down&starting-point-node-id=1435%3A13552&show-proto-sidebar=1&mode=design)