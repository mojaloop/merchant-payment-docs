# Registry form records reports
## DFSP maker
* **As a** DFSP maker, **I want to** see[view and export only] following reports **so that** I can perform other related activities.
* all of the following reports only include data from own organization/DFSP. 
    * Registered Merchants
        * all merchant records which are already successfully registered to both acquiring system and registry system. 
    * Approval Pending Merchants
        * merchant records which are added to merchant acquiring system with "registration status" as "Pending" AND added by particular Maker who is currently logged in. 
    * Rejected Merchants
        * merchant records which were added by currently logged in Maker and rejected by DFSP checker. 

## DFSP checker
* **As a** DFSP checker, **I want to** see following reports **so that** I can perform other related activities.
    * Pending Merchants 
        * merchant records which have been added by DFSP makers and waiting for approval. 
        * Possible actions 
            * view
            * export 
            * approve/reject
        * After one checker has already approved/rejected the records, it shouldn't be appeared in this report anymore[in other words,ONLY records with registration status "Pending" will be appeared in the report.]
    * Registered Merchants
        * all merchant records which are already successfully registered to both acquiring system and registry system. 

## Design File
* [view_records](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-8023&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1435%3A8023&show-proto-sidebar=1)