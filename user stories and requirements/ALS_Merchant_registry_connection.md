## User Story:
**As a** Payer Financial Service Provider (FSP), **I want to** retrieve merchant information from the Merchant Registry using the merchant alias provided by the customer, **so that** I can update the party information for the merchant to complete payment transaction in the Mojaloop system.

## Acceptance Criteria:
* Given that a customer provides a merchant alias, when the PayerFSP sends a GET request to /parties/<idType>/id in Mojaloop_ALS, the request should include the merchant alias in the path.
* Given that the FSPIOP-Destination header is set to "Merchant_Registry", when Mojaloop_ALS receives the GET request, it should accept the request and respond with an HTTP 202 Accepted status.
* Given that the idType is "TILL_CODE" and the destination header is set, when Mojaloop_ALS receives the request, it should route the request to the Merchant Registry by sending a GET request to /parties/TILL_CODE/123456.
* Given that the Merchant Registry receives the GET request, it should accept the request and respond with an HTTP 202 Accepted status.
* Given that the Merchant Registry processes the request, when it has the required information, it should return the following data:
  * DFSP_ID
  * Extension Data: Merchant_ID
  * Checkout_Counter_ID
  * Other merchant information
* Given that the Merchant Registry has retrieved the required information, when it responds to Mojaloop_ALS, it should return an HTTP 200 OK status.
* Given that Mojaloop_ALS receives the response from the Merchant Registry, when it has the DFSP_ID and other party information, it should send a PUT request to /parties/TILL_CODE/123456 (DFSP-ID) (Party Information) to update the party information for the merchant.
* Given that PayerFSP receives the response from Mojaloop_ALS, it should receive an HTTP 200 OK status, indicating that the party information update was successful.