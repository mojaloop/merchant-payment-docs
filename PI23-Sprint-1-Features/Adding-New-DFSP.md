# User Story

**As a hub operator**, **I want to** onboard new DFSPs via the portal interface **so that** I can efficiently and effectively add their information to the merchant registry system.

## Acceptance Criteria

- When onboarding a new DFSP, the following information will be requested:
  - DFSP ID [Dropdown, which will also need to be captured and this should be the same as the DFSP ID used in Mojaloop.]
  - DFSP Name
  - DFSP Business License ID
  - Business Logo (image file)
  - Whether the DFSP will use the Mojaloop Merchant Acquiring Portal (Yes/No)
- DFSP User Management 
  - Adding DFSP users must be performed individually in the user management menu.
  - The system will prompt to select either Hub user or DFSP user.
  - If "DFSP user" has been selected, the system should present a DFSP name dropdown featuring a list of available DFSPs.
  - This dropdown should be a mandatory selection to ensure proper association with the relevant DFSP during user creation.
- A single admin user can perform both maker and checker functions but can't approve the activity which she/he does. 

- After successfully adding a new DFSP, the DFSP will be automatically activated in the system.
- If the DFSP will use the Mojaloop Merchant Acquiring System, first super admin user will receive account activation email where she/he can activate their account and set the password.
- If the DFSP is not using the Mojaloop Merchant Acquiring System, an API key will be generated for the ALIAS registration process.

- All actions related to onbording DFSP should be logged and audited for accountability and security monitoring.
  - onboarding new DFSP (who, when, which DFSP)
  - new user added ( by which user,added which user)

## Design File
* [Adding New DFSP](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=3813%3A7463&type=design&node-id=3813-8029&viewport=448%2C-248%2C0.3&t=fWGudwyGAVnciDsB-1&scaling=scale-down&starting-point-node-id=3813%3A8029&show-proto-sidebar=1&mode=design)