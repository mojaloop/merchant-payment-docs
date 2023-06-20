## Portal User Management 

**As a** super admin of DFSP, **I want** to be able to assign users to different roles **so that** people from my DFSP organization can start managing merchant records 

**As a** super admin of DFSP, **I want** to be able to delete an existing user from my DFSP organization **so that** deleted user cannot be able to access the portal.  

**As a** super admin/admin of DFSP, **I want** to be able to reassign role of an existing users from my DFSP organization **so that** newly assigned user can start peroforming action available to new role.  

 

### Acceptance Criteria 

* Default Roles 
* Admin  
    * Read/write access for all reports and form  
    * Assign new users to different roles 

* Operator  
    * Read/write access for all reports and forms 
    * Remark: if an operator make a perticular action, they cannot check that action and reject/approve it.  

* Auditor  
    * Read access for merchant records and check audit logs  
    * Assigning roles process sequence flow 

* Admin/Super admin assign new users to a role by  
    * Adding email, name and assigned role 
    * System will send assigned email a new email that instruct to reset password 
    * New user reset password 
    * New user login to the portal with new password and start performing available actions 