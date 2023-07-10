## Portal User Management 

**As a** super admin of DFSP, **I want** to be able to assign users to different roles **so that** people from my DFSP organization can start managing merchant records.

**As a** super admin of DFSP, **I want** to be able to delete an existing user from my DFSP organization **so that** deleted user cannot be able to access the portal.  

**As a** super admin/admin of DFSP, **I want** to be able to reassign role of an existing users from my DFSP organization **so that** newly assigned user can start peroforming action available to new role.  

 

### Acceptance Criteria 

* Default Roles 
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
* creating new role 
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
                * 