# Merchant Registry receives request

## Process flow

* There will be two endpoints that will call Alias generation APIs
  * Mojaloop's merchant acquiring system with records of acquiring status "Approved"
  * DFSP with existing acquring system. 

* There will be a scheduler job in Merchant Acquiring system doing following step.
  * Fetch records from Database that are submitted by Checker.
  * Call services of Merchant Registry to authenticate and then call Register Alias.
  * RegisterAlias API will have following input parameters
    * DFSPID,
    * MerchantID
    * CheckOutCounterID
    * PAYINTOID [if user submit it in acquiring form response]
* if PAYINTOID from acquiring form is null, then Merchant registry will generate Alias and return it back in API response
  * Response Code  
  * Response Description
  * PAYINTOID

* ## RegisterAlias Service API

  * Check if same DFSPID, Merchant ID, CheckOutCounterID is already in Registry
  * If present return http/200 with 
    *Response Code – 01 
    * Response Description “Merchant already registered”
    * PAYINTOID  - “Existing Alias assigned”
  * If not present then
    * Generate Alias as a unique sequence number
      * auto incremental
    * Add in Database
    * Reply with Response Code = 00;  Description;  Merchant Registered;   PAYINTOID =  “New Alias registered”.
