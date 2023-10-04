# Revert record Feature

As a DFSP maker, I want to continue to fill out the revert form applications by selecting the one for which I receive new information so that merchant data can be updated and continue to Alias generation process. 

## Acceptance Criteria

* Revert records =merchant records with Status =REVERT and DFSP_ID=login user's DFSP ID.
* User will be able to select "Revert" form application by selecting the filter of status as "Revert".
* When the user clicks the "View detail" button, all of the data that has been filled out in the merchant registry form is shown in order.
* When the user clicks the "Proceed" button, the old data of the application will be reloaded, and the user can start editing the out the form..
* After first edit, the status of the record will be changed to "Draft".
* only after final "submission", the status of the record will change to "Review" and maker name will be updated with final maker who submitted the form. 
* [all of the users of the system can edit the form, ie 001 merchant record with status "REVERT" will appear in to be reverted report of all the users.]
* After resubmitting the form, the other users who do not make final submission of the form can check the form and continue the approval process.

## Design File

* [To be reverted report](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=2121-8001&viewport=417%2C2269%2C0.3&t=ez5lM4RJzlmH2YfI-1&scaling=scale-down&starting-point-node-id=2121%3A8001&show-proto-sidebar=1&mode=design)