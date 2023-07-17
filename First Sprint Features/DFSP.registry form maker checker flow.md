# Simple merchant registration 

## Maker Checker Assignment

* **As A** DFSP user, **I want to** create users with maker checkers with following contraints **so that** Merchant Registry system has lesser human errors.
 
### Acceptance Criteria

* there will be no specific fixed role as maker and checker.
* If one person has done certain actions such as add a new record or edit an existing record, the other users in the system can check the result [ updated record or newly added record] and approve or reject the action. 
* One user can be maker and checker at the same time.The same person who is action taker CANNOT review the same records he or she modified.
* If one person has already reviewing the modified record, it should be showing to the other checkers that the one person is currently reviewing the record.
* If user A have added a new record, the pending records will appear in user B and user C review list. After user B start reviewing the record and user C open the same record, there should be an alert that "user B is reviewing the current record" for user C so that they can avoid double job and inconsistant approvals. User C can still review, but cannot APPROVE/REJECT the record.
* all the users can check approved, rejected records in the system.
* user A can check pending records, but she or he cannot take REVIEW or APPROVE/REJECT actions.



## Registry form maker checker flow

* **As a** DFSP checker, **I want to** be notified when there is new record or updated record from DFSP makers with registration status "Pending" **so that** I can check and approve/reject the records and updated actions. 

* **As a** DFSP checker,**I want** registration status to change into "Approved/Rejected" after I have approved or rejected the status **so that** further steps can be performed for those records. 
    * When DFSP checker reject the record, system will have to ask the reason so that DFSP makers can update the record or do further actions accordingly. 
        * Message : "Enter the rejection reason"
    * After DFSP checker has approved/rejected the record, system will notify the results to the maker who added the records
        * notification message : " username XXX has approved xxx records ". 
        * notification message : " username XXX has rejected xxx records". 
    * When DFSP checker has approved the records, the data should be reflected to Merchant Registry oracle system and perform alias generation process.[alias generation process will be added after alias generation flows have been finalized] 
    * When maker clicks those notifications, maker can see details of the records, in case of rejected records, makers will see the record details along with rejection reason. 

## Design file
* [Maker_Checker](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1504-14308&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1517%3A10353&show-proto-sidebar=1)