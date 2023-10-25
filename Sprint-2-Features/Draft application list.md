# Registration Save As Draft Feature

As a DFSP maker, I want to continue to fill out the draft applications by selecting the one for which I receive new information so that I can save time and complete that application without unnecessary steps.

## Acceptance Criteria

* The "continue saved draft application" button will be disabled when there is no draft application.
* If the draft applications are more than one, the number of records will be shown at the top right corner of the button.
* When the user clicks the "continue saved draft application" button, the draft applications will be shown in a table.
* In the table, the record with status "DRAFT" that has been filled out in the merchant registry form is shown.
* When the user clicks the "View detail" button, all of the data that has been filled out in the merchant registry form is shown in order.
* When the user clicks the "Proceed" button, the work-in-progress of the saved draft will be reloaded, and the user can continue filling out the form.
* As long as status is in "DRAFT", the records will be shown in Draft table even though DFSP maker update the form second or third time.
* only after final "submission", the status of the record will change to " Review" and maker name will be updated with final maker who submitted the form. 
* __Draft count calculation__
  * Draft count = number of record where Status =Draft and DFSP_ID=login user's DFSP ID

## Design File

* [save_as_draft_merchant_records_table](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1865-10059&viewport=417%2C2269%2C0.3&t=JLfMpLlDsQxIs2Um-1&scaling=scale-down&starting-point-node-id=1865%3A10059&show-proto-sidebar=1)