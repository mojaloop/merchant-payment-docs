## Enable, disable DFSP  

**As a** hub user, **I want to** enable DFSP **so that** I can DFSP users can start using merchant registry portal to handle their merchant data.  

**As a** hub  user, **I want to** disable DFSP profile including all users who are handing from DFSP side **so that** DFSP users cannot use the portal anymore in case DFSP is no longer in the system. 

### Acceptance criteria 

* When hub user enable a DFSP, hub user(checker) will have to check the action and approve/reject. If checker has approved the action, DFSP will be enabled.  

* Enabled DFSP will be able to upload acquired merchant lists, manage existing merchants of allow list and blocked list and handle self-registered merchants.  

* Disabled DFSP will not be able to update merchants list, or any other actions. Merchants from disabled DFSP won’t be able to participate in mojaloop system.  


## Adding default user admin user for DFSP 

**As a** hub user, **I want to** add default user admin user for onboarded DFSP, **so that** they can start managing DFSP portal.  

### Acceptance Criteria 

* Default DFSP user admin user will be able to add new DFSP users, management merchant lists and all other actions that are available to the DFSP.  