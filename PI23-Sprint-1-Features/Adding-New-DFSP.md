# User Story

**As a hub operator**, **I want to** onboard new DFSPs via the portal interface **so that** I can efficiently and effectively add their information to the merchant registry system.

## Acceptance Criteria

- When onboarding a new DFSP, the following information will be requested:
  - DFSP Name
  - DFSP Business License ID
  - Super Admin User Information
    - Name
    - Phone Number
    - Email
  - Business Logo (image file)
  - Whether the DFSP will use the Mojaloop Merchant Acquiring Portal (Yes/No)

- After successfully adding a new DFSP, the DFSP will be automatically activated in the system.
- If the DFSP will use the Mojaloop Merchant Acquiring System, first super admin user will receive account activation email where she/he can activate their account and set the password.
- If the DFSP is not using the Mojaloop Merchant Acquiring System, an API key will be generated for the ALIAS registration process.
- For both scenarios (super admin user or API key generation), there should be a "Copy to Clipboard" option beside the text to allow easy copying of the generated information.
- All actions related to onbording DFSP should be logged and audited for accountability and security monitoring.
  - onboarding new DFSP (who, when, which DFSP)
  - new user added ( by which user,added which user)
