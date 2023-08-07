 ## Non-happy path for checker [revert, reject] 
 **As a** DFSP checker,  **I want to** see “To be Reverted Report” and “Rejected Merchant Report” **so that** I can check easily which reports have been reverted and which were rejected.  

## Acceptance Criteria 
* To be Reverted Report
    * After one checker has already changed the records to be reverted from the pending merchant records, those records will appear in the “To be Reverted Report,” and the registration status will be changed to reverted. 
    * Makers are allowed to edit those records. 
* Rejected Merchant Report 
    * After one checker has already rejected the records from the pending merchant records, those rejected records will appear in the “Rejected Merchant Report,” and the registration status will be changed to rejected. 
    * Rejected records cannot be done any action except export and view details. 
    * After DFSP checker has approved/rejected the record, system will notify the results to the maker who added the records. 
        * Notification message : " username XXX has rejected xxx records". 


 ## Data Retrieval  
 **As a** DFSP checker, **I want to** review the data that is related to my DFSP **so that** I can see which records have been approved and which have been rejected and determine what to do next.  

 ## Acceptance Criteria 
 * When the data loads, it should only display data that is relevant to the user. 
* Determine which DFSP this user is from, and then display the data associated with that DFSP
* all merchant records 
    * Display all the data that is relevant to the DFSP that the user is from, regardless of registration status 
* Pending merchant 
    * Display the merchant list that is included in the DFSP where the user is from and is waiting for merchant acquisition approval. 
    * Registration status must be “Review”. 
    * If the maker of the displayed records is the same as the log-in user, those records will be displayed in gray, and approved or rejected actions cannot be done for those records. 
* Approved merchant records 
    * Display the merchant list that is included in the DFSP where the user is from and has been approved by the checker. 
    * Registration status must be “Approved”. 
* Rejected Merchant Report   
    * Display the merchant list that is included in the DFSP where the user is from and has been rejected by the checker. 
    * Registration status must be “Rejected”. 
* To be Reverted Report   
    * Display the merchant list that is included in the DFSP where the user is from and related to that user; in other words, the maker of the displayed records must be the same as the log-in user. 
    * Registration status must be “Reverted”. 