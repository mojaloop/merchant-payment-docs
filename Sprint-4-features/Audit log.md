# User Story

**As an auditor, super admin user, or admin user** , **I want to** be able to access the audit log for a specific DFSP (Digital Financial Service Provider) and view a table containing records of actions sorted by the latest updated time. The table should display various attributes for each record, including portal user name, action type, application module, event description, entity name, old value (truncated), new value (truncated), and the timestamp when the action was created.

## Acceptance Criteria:

1. When logged in as an auditor, super admin user, or admin user, there should be a dedicated section or page in the application for accessing the audit log.

2. The user interface for the audit log should provide a filter or selection mechanism to choose a specific user,action type for which to view the audit log records. []

3. action type and portal user name filters should be displayed with drop down populating the options available in the database.

4. The audit log table should display the following attributes for each record:
   - Portal User Name: The name of the user who performed the action.
   - Action Type: The type of action performed (e.g., create, update, delete).
   - Application Module: The module or section of the application where the action occurred.
   - Event Description: A brief description of the action or event.
   - Entity Name: The name of the entity affected by the action (e.g., user account, transaction).
   - Old Value (Truncated): A truncated representation of the old value **before** the action (e.g., "..." if the value is too long).
   - New Value (Truncated): A truncated representation of the new value **after** the action (e.g., "..." if the value is too long).
   - Created At (Time): The timestamp indicating when the action was created.

5. The "Old Value" and "New Value" columns in the table should display ellipsis ("...") to indicate that the full value is available but hidden.

6. Each record in the audit log table should have an option or button, such as "View Detail," that allows the user to see the original JSON format of the "Old Value" and "New Value" for that specific record.

7. Clicking the "View Detail" button for a record should open a modal or detailed view that displays the complete and untruncated JSON format of both the old and new values.

8. Users should be able to paginate through the audit log table if there are a large number of records.

9. The audit log should capture and display records for all relevant actions and events within the selected DFSP, ensuring that the log is comprehensive and up-to-date.

10. The audit log should be accessible only to authorized auditor, super admin, and admin users, and proper authentication and authorization mechanisms should be in place to enforce this access control.

11. Proper error handling and user feedback should be implemented to inform users in case of any issues with accessing or viewing the audit log. When unauthorized user trys to access the audit log, show the error as " you do not have permission to check the audit log".

## Design File
* [Audit Log](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=3401-8507&viewport=156%2C625%2C0.21&t=OSXqRfVnDkbsjz5G-1&scaling=scale-down&starting-point-node-id=3401%3A8507&show-proto-sidebar=1&mode=design)