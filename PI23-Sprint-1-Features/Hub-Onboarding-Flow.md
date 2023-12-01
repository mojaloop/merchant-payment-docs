# User Story

**As a hub system administrator**, **I want to** be able to access to a default super admin user and able to create additional super admin users using email, password, and role. Once a second super admin user is created, the default super admin user should be disabled. User account activation follows the same flow as before.

## Acceptance Criteria

- When the hub system is initially deployed, a default super admin user account should be automatically created and enabled.
- By Default we will have a "Default Super Admin" user who is assigned a role "Super Admin" and that role can only create 3 users with "Hub Admin Maker" or "Hub Admin Checker" role with the following information:
  - Name
  - Email address.
  - listing down pre-configured Roles in the system
- System will send email from the form a new email that instruct to set password
- New user set password and confirm password
- New user login to the portal with new password and start performing available actions


- Hub operator pre-configured roles
  - Super admin
    - Create 3 users of either Hub admin maker or Hub admin checker role
    - Once three users are created - disable "Default Super Admin" as it is not needed any further.

  - Hub admin user
    - First 3 users of this role are created by Super admin
    - Further hub admins can make more users
    - A single user can have both Admin Maker and Admin checker role but can't approve at both levels


- Super admin user creation should follow standard security practices, including password requirements and email validation.

- The process for disabling the default super admin user should be secure and irreversible.

- All actions related to super admin user management should be logged and audited for accountability and security monitoring.

- Hub admin users can 
  - initiate and complete the onboarding process for DFSPs.
  - create new users with the "DFSP Admin Role", giving them specific DFSP management permissions.
  - create new users with the "Hub Admin Role", allowing them to manage administrative tasks at the hub level.
  - cannot create any new user with "Super Admin Role"
  - update the status of users they have created, with available status options including:
    - **Active**: Representing a normal operational status.
    - **Inactive**: Temporarily disabling user access.
    - **Block**: Permanently disabling user access.
    - Status Transitions:
      - Active to Inactive: Users can be temporarily disabled.
      - Inactive to Block: Users can be permanently disabled.
      - Active to Block: Users can be directly blocked.
      - Inactive to Active: Users can be reactivated after being temporarily disabled.
- Hub admin users should have the ability to view all merchant records, inclusive of filter options.
- However, they are restricted from performing any updates, edits, or modifications to the displayed data.