# Simple merchant registration 
## Simple Merchant Bulk Input
**As a** DFSP maker, **I want to** add new merchant records into acquiring system by bulk input **so that** I can save more time. 

### Acceptance Criteria
* following file types should be available for bulk input
    * .csv
    * .xlsx
* user should be able to download a sample csv template file that they can refer to. 
* after the upload process, success record and failed record should be shown via alert box. 
    * Message : XX merchant records are successfully added to the system. There are XX  fail records. 
    * If there is no failed record, only "OK" button will be there. 
    * If there are any failed records, "See more" button will be there where user can click to see detail of failed records. 
    * If user click "see more" button , show details of that failed record in table form with pop up window.