# User Story

**As a hub operator**, I want to enable merchants to register themselves in the system so that they can streamline the onboarding process, avoid bottlenecks at DFSP sites, and easily monitor the status of their applications.

## Acceptance Criteria

- A user account creation process is implemented for merchants to control their registration processes, with one user account tied to one merchant.

- To create a portal user account, the following information will be collected:
  - Name
  - Option to select either an email or phone number for registration.
  - Password and confirmation of the password.

- For the initial implementation, email verification will be the sole verification method. SMS OTP verification is excluded due to potential complexity variations in different countries.

- After signing up on the portal, account activation will be required via an email confirmation process.

- Once the account is activated, 
  - merchants will be able to register for the merchant acquiring system
  - Choose their preferred DFSP from a drop-down menu.
  - Check the status of their registration application.
  - Continue working on draft application functions, allowing them to complete their registration in a step-by-step manner.

## Design File
* [Merchant Portal User Creation](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=3829%3A43204&type=design&node-id=3829-43205&viewport=-834%2C-320%2C0.39&t=8gVdoQiP5ycCLhOI-1&scaling=scale-down&starting-point-node-id=3829%3A43205&show-proto-sidebar=1&mode=design)
* [Progress Status](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=3829%3A43204&type=design&node-id=3840-46018&viewport=-834%2C-320%2C0.39&t=8gVdoQiP5ycCLhOI-1&scaling=scale-down&starting-point-node-id=3840%3A46018&show-proto-sidebar=1&mode=design)