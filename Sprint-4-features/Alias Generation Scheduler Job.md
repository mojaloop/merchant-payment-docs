# Alias Generation Checklist

## acceptance criteria

* to update oracle database
* to create API end points that are mentioned in the powerpoint
* to create scheduler job

## current focus

* To create alias_generation API (input : DFSP_ID,merchant ID, checkout_counter_ID, PayInto_ID [nullable])
  * Reference: get/participant, post/participant API development. 
  * To discuss [merchant ID and checkout_counter_ID from external DFSP [outside of merchant acquiring system] might not be aligned with merchant acquiring system]
  * One possible solution: making merchant ID, checkout_counter_ID as nullable as well since the major objective of Oracle is to store mapping information of alias and DFSP.
* To update merchant registry database
  * Reference: Slide number 5


## out of scope

* PUT /parties interface
  * Reason is that it assumes that Participant will create Alias and put in Oracle. Currently, we are only developing “CreateAlias” end-point which creates an Alias and links it to requesting DFSP also.
  * Secondly, PUT /parties interface currently does not support extension information which we need to capture i.e. Merchant Identifier.

### Done
 * Acceptance Criteria pass 
 * Designs are up-to date 
 * Code Style & Coverage meets standards 
 * QA pass 
 * Unit Tests [Not Yet]
 * Integration Tests [Not Yet] 
 * Changes made to config (default.json) are broadcast to team and follow-up tasks added to update helm charts and other deployment config. [Not Yet]


### Follow-up 
 * N/A 
  

### Dependencies
 * N/A 

  
### Accountability
 * Owner: Si Thu Myo, Naing Linn Khant
 * QA: Hsu Yee Mon, Phyu Sin Myat  
 * Review: Karim