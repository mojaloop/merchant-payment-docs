## Report filters
**As a** DFSP user, **I want to** be able to filter out records from each report based on my selected criteria. 
### Acceptance Criteria
* following filters should be available in all reports. 
    * added by 
    * approved by
    * added time
    * updated time
    * DAB name
    * Merchant ID
    * Payinto ID
    * Registration status
* Multiple filters should be able to select at once. 
    * example ==> added by "xxx" AND updated time "hh:mm dd/mm/yyyy"
* When the user clicks the "Clear Filter" button, the values in each filter should be reset to null, and all data should be reflected in the tables. 

## Report download
**As a** DFSP user, **I want to** be able to download filtered records from each report based on my selected criteria. 
### Acceptance Criteria
* reports should be downloadable by following formats
    * csv
    * pdf
    * excel

## Design file
* [report_filter](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-8023&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1435%3A8023&show-proto-sidebar=1)