# User Story:

**As a hub system administrator**, I want to create super admin users using email, password, and role. Once a second super admin user is created, the default super admin user should be disabled so that I can ensure the security and functionality of the system.

## Acceptance Criteria:

- When the hub system is initially deployed, a default super admin user account should be automatically created and enabled.

- The default super admin user should have the ability to create a new super admin user with the following information:
- Email address.
- Password.
- Role designation as "Super Admin."

- Once the second super admin user is successfully created and activated, the default super admin user should be automatically disabled to prevent further use.

- Super admin user creation should follow standard security practices, including password requirements and email validation.

- The system should support user account activation for newly created super admin users and any other users following the existing activation flow.

- User account activation should ensure that the new super admin user is properly authenticated.

- The process for disabling the default super admin user should be secure and irreversible, ensuring that the default super admin account **CANNOT** be re-enabled without appropriate authorization.

- All actions related to super admin user management should be logged and audited for accountability and security monitoring.
