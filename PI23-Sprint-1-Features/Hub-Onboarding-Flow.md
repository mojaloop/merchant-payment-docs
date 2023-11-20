# User Story

**As a hub system administrator**, **I want to** be able to access to a default super admin user and able to create additional super admin users using email, password, and role. Once a second super admin user is created, the default super admin user should be disabled. User account activation follows the same flow as before.

## Acceptance Criteria

- When the hub system is initially deployed, a default super admin user account should be automatically created and enabled.
- By Default we will have a "Default Super Admin" user who is assigned a role "Super Admin" and that role can only create 2 users with "Hub Admin Maker" or "Hub Admin Checker" role with the following information:
  - Name
  - Email address.
  - Password.
  - listing down pre-configured Roles in the system

- Hub operator pre-configured roles
  - Super admin
    - Create 2 users of either Hub admin maker or Hub admin checker role

  - Hub admin user
    - First 2 users of this role are created by Super admin
    - Further hub admins can make more users
    - A single user can have both Admin Maker and Admin checker role but can't approve at both levels

- Once two users are created - disable "Default Super Admin" as it is not needed any further.

- Super admin user creation should follow standard security practices, including password requirements and email validation.

- The process for disabling the default super admin user should be secure and irreversible.

- All actions related to super admin user management should be logged and audited for accountability and security monitoring.

- Hub Admin Users (Maker/Checker) can
  - Onboard DFSP
    - Create Additional Users with the following roles only
      - DFSP admin user
      - Hub Admin user
- Hub Admin Users cannot
  - Create any new user with "Super Admin Role"