# User Story

**As a hub operator**, I want to enable merchants to register themselves in the system so that they can streamline the onboarding process, avoid bottlenecks at DFSP sites, and easily monitor the status of their applications.

## Acceptance Criteria

- A user account creation process is implemented for merchants to control their registration processes, with one user account tied to one merchant.

- On the register page, to add Google Re-captcha (this is just to stop any bot-type attacks)
- First step when the merchant is trying to apply the system will check
  - No merchant is already there with the same email
  - No merchant registration request is pending with the same email
- If these checks pass then
  - Merchant registration application is stored with "Verification Status = Pending"  (this will be separated from Merchant records which we have now)
  - Merchant verified using OTP on email and then they are "Activated"
- Now Merchant will submit the application
  - 1 Merchant can submit one application only.
- If merchant's application is not fully submitted or partially submitted, they can come again to complete it.
- If merchant's application is pending review, and they login, they will see the status "DFSP Reviewing Stage" and QR or Alias won't be displayed.

- To create a portal user account, the following information will be collected:
  - Name
  - Option to select either an email or phone number for registration.
  - Password and confirmation of the password.


- It is required that the phone number or email used during registration be unique.
- For the initial implementation, email verification will be the sole verification method. SMS OTP verification is excluded due to potential complexity variations in different countries.
- After signing up on the portal, account activation will be required via an email confirmation process.

- Once the account is activated, 
  - merchants will be able to register for the merchant acquiring system
  - Choose their preferred DFSP from a drop-down menu.
  - Check the status of their registration application.
  - Continue working on draft application functions, allowing them to complete their registration in a step-by-step manner.
- A single application is permitted for each merchant.

## Design File
* [Merchant Portal User Creation](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=3829%3A43204&type=design&node-id=3829-43205&viewport=-834%2C-320%2C0.39&t=8gVdoQiP5ycCLhOI-1&scaling=scale-down&starting-point-node-id=3829%3A43205&show-proto-sidebar=1&mode=design)
* [Progress Status](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=3829%3A43204&type=design&node-id=3840-46018&viewport=-834%2C-320%2C0.39&t=8gVdoQiP5ycCLhOI-1&scaling=scale-down&starting-point-node-id=3840%3A46018&show-proto-sidebar=1&mode=design)