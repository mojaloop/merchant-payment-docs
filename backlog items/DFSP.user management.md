## Portal User Management 

**As a** super admin of DFSP, **I want** to be able to assign users to different roles **so that** people from my DFSP organization can start managing merchant records.

**As a** super admin of DFSP, **I want** to be able to delete an existing user from my DFSP organization **so that** deleted user cannot be able to access the portal.  

**As a** super admin of DFSP, **I want** to be able to reassign role of an existing users from my DFSP organization **so that** newly assigned user can start performing action available to new role.  

 

### Acceptance Criteria 

* Default Roles 
    * Super Admin
        * assigned by Hub user
        * assign roles and create roles
        * view records and reports of every record in related DFSP
    * Maker 
        * add new merchant records
        * edit existing merchant records
        * disable/enable merchants
        * view related reports
    * Checker
        * approve/reject newly added merchant records
        * view related reports
    * explorer
        * view reports
* creating new role [should be able to be done ONLY by super admin]
    * process flow 
        * user will have to create a role with following information 
            * role name
            * description of the role
            * available actions [ check box]
                * add new merchant records
                * edit existing merchant records
                * disable/enable merchants
                * view reports
                    * pending merchants
                    * registered merchants
                    * rejected merchants
                * Approve/reject newly added merchants

## Design File
* [role_management](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-8023&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1435%3A8023&show-proto-sidebar=1)
* [user_management](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-8023&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1435%3A8023&show-proto-sidebar=1)