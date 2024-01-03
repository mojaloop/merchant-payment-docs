## User Story:
**As a registered merchant with a DFSP**, **I want** the ability to create a portal user account **so that I can** manage and review my information conveniently online.

### Acceptance Criteria:

1. When a merchant with an existing alias from the DFSP enters the "Alias ID" and "Email" on the portal:
   - If the Alias ID and Email match the registered data:
     - The system should send an email to the provided Email address.
     - OTP validation rules should be applied for additional security.
   - If the Alias ID is correct but the Email is incorrect:
     - A notification email should be sent to the registered Email address and the DFSP.
   - If the Alias ID is incorrect:
     - The system should not send any email and should notify the DFSP.

2. OTP Validation:
   - OTP validation rules should be applied when sending the email.
   - The merchant should receive the OTP and enter it for account verification.

3. Notification Emails:
   - The content of notification emails to the DFSP should include details about the attempted access, indicating whether it was successful or unsuccessful.
   - The notification email to the registered Email address should inform the merchant about the attempted unauthorized access, specifying the Alias ID and the time of the attempt.

4. Security:
   - The system should ensure that access attempts are logged for security monitoring purposes.
   - Proper error messages should be displayed on the portal to guide the merchant based on the outcome of the Alias ID and Email validation.
