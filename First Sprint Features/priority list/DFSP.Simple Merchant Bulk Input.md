# Simple merchant registration 
## Simple Merchant Bulk Input
**As a** DFSP maker, **I want to** add new merchant records into acquiring system by bulk input **so that** I can save more time. 

### Accpetance Criteria
* following file types should be available for bulk input
    * .csv
    * .xlsx
* user should be able to download a sample csv template file that they can refer to. 
* after the upload process, success record and failed record should be shown via alert box. 
    * Message : XX merchant records are successfully added to the system. There are XX records fail record. 
    * If there is no failed record, only "OK" button will be there. 
    * If there are any failed records, "See more" button will be there where user can click to see details of failed records. 
    * If user click "see more" button , show details of that failed record in table form with pop up window.

## Design File
* [Bulk input](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1517-10353&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1517%3A10353&show-proto-sidebar=1&mode=design)
