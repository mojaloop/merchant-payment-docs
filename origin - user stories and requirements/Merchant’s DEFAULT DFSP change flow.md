## Merchant’s DEFAULT DFSP change flow
 
**As a** merchant, **I want to** be able to change DEFAULT DFSP that I set **so that** I can receive payments from more suitable DFSP for me. 

### Acceptance Criteria
* Process flow 
    * Initial stage : merchant registered with DFSP A
    * Merchant request to change default DFSP to DFSP B 
    * Merchant acquition portal send necessary data attributes that  are already collected to DFSP B
    * Registration Status will be changed to “DFSP_CHANGE_PENDING” 
    * While Registration Status is being “DFSP_CHANGE_PENDING”, merchant will receive payments via existing DEFAULT DFSP A
    * After DFSP B has confirmed the change, merchant will be able to receive payments via DFSP B.
