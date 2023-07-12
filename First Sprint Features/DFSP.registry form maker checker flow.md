# Simple merchant registration 
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