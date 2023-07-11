## Enable, disable DFSP  

**As a** hub user, **I want to** enable DFSP **so that** DFSP users can start using merchant registry portal to handle their merchant data.  

**As a** hub  user, **I want to** disable DFSP profile including all users from that DFSP at once **so that** DFSP users cannot use the portal anymore in case DFSP is no longer in the system. 

### Acceptance criteria 

* When hub user enable a DFSP, hub user(checker) will have to review and approve/reject the action. If checker has approved the action, DFSP will be enabled.  

* Enabled DFSP will be able to upload acquired merchant lists, manage existing merchants of allowlist and blocklist and handle self-registered merchants.  

* Disabled DFSP will not be able to update merchants list, or any other actions. Merchants from disabled DFSP won’t be able to participate in mojaloop system.  


## Adding default super admin user for DFSP 

**As a** hub user, **I want to** add default super admin user for onboarded DFSP, **so that** they can start managing merchant acquiring system.  

### Acceptance Criteria 

* Default DFSP user admin user will be able to add new DFSP users, manage merchant lists and all other actions that are available to the DFSP.  