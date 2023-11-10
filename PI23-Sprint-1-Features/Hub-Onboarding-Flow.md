# User Story

**As a hub system administrator**, **I want to** be able to access to a default super admin user and able to create additional super admin users using email, password, and role. Once a second super admin user is created, the default super admin user should be disabled. User account activation follows the same flow as before.

## Acceptance Criteria

- When the hub system is initially deployed, a default super admin user account should be automatically created and enabled.

- The default super admin user should have the ability to create a new super admin user with the following information:
  - Name
  - Email address.
  - Password.
  - Role designation as "Super Admin."

- Once the second super admin user is successfully created, the default super admin user should be automatically disabled to prevent further use.

- Super admin user creation should follow standard security practices, including password requirements and email validation.

- User account activation should ensure that the new super admin user is properly authenticated and has access to the necessary system resources.

- The process for disabling the default super admin user should be secure and irreversible, ensuring that the default super admin account cannot be re-enabled without appropriate authorization.

- All actions related to super admin user management should be logged and audited for accountability and security monitoring.