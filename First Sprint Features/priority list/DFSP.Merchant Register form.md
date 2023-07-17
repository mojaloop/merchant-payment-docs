# Simple merchant registration 
## Registration Form 
As a DFSP maker, I want to register simple merchant to the acquirer system with 2 methods [ single form input or bulk input by excel file] so that its data can be transferred to registry system and generate alias. 

### Acceptance Criteria

* Simple merchant can be identified as following criteria
    * Merchant with single location/single checkout counter, single payintoID, account and contact person. 

* #### Registry Form flow

    * When maker click "save and proceed" button and filled out all necessary field in the first page, merchant ID will be generated and registration status will change to "Draft".
    * everytime user click "save and proceed", the filled fields in the form will be updated in the record of generated merchant ID.
    * After being submitted, the merchant record will be with registration status as "Review".  
* following data points will be captured in the acquiring step.

    * Business information  
        * Doing Business As Name  [Single line, Required]
        * Registered Name [Single line, Not Required]
        * Payinto Account
        * number of employee [Dropdown, Required]
            * 0-5 
            * 6-10 
            * 11-50 
            * 51-100 
            * 100++ 
        * monthly turn over [Dropdown, Required , populated from SIC merchant type table]
        * Merchant category  [ Dropdown, Required] 
            * [SIC merchant catagories](https://resources.companieshouse.gov.uk/sic/)
        * merchant Type [Dropdown, Not Required ]
            * Individual
            * Small Shop
            * Chain Store
        * Registered DFSP name [Dropdown, Not Required ] 
            * Populated from DFSP table
        * Currency [ Dropdown, Required]
            * populated from currency table
    * Location information 
    * Location type  [Dropdown, Required ] 
        * Virtual  
        * Physical  
    * Country [dropdown ,Not Required ]  
    * Website URL [Not Required ] 
    * Physical business address [ group ]
        * Department [Not Required ]
        * Sub Department [Not Required ]
        * Street Name [Not Required ]
        * Building Number [Not Required ]
        * Building Name [Not Required ]
        * Floor Number [Not Required ]
        * Room Number [Not Required ]
        * Post Box [Not Required ]
        * Postal Code [Not Required ]
        * Township [Not Required ]
        * District [Not Required ]
        * Country Subdivision(State/division) [Not Required ]//remark : state list should be reflected to chosen country 
        * Country  [Dropdown, Required ]
        * Longitude [Not Required ]
        * Latitude [Not Required ]
    * Check out counter description[ to display in customer app/ussd] [single line, Required]
* Business owner information 
    * Name  
    * National ID  
    * Nationality [dropdown, Required ] 
    * Physical Address  [visual - sub group]
        * Department [Not Required ]
        * Sub Department [Not Required ]
        * Street Name [Not Required ]
        * Building Number [Not Required ]
        * Building Name [Not Required ]
        * Floor Number [Not Required ]
        * Room Number [Not Required ]
        * Post Box [Not Required ]
        * Postal Code [Not Required ]
        * Township [Not Required ]
        * District [Not Required ]
        * Country Subdivision(State/division) [Not Required ]
        * Country  [Dropdown, Required ]
        * Longitude [Not Required ]
        * Latitude [Not Required ]
    * Phone number [phone number, Required ]
    * Email [Not Required ] 
* Contact person  
    * //Remark==> condition : if user click: same as business owner, copy business owner information into contact person 
    * Name  
    * Phone number 
    * Email  
* Business license 
    * Do you have Business license? 
        * Yes  
        * No 
    * Condition : if user choose, No, following fields will be disabled 
    * License number 
    * License document [field type : file] 
    * Reference CSV format should be able to downloaded  

## Design file 
* [registration form](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1435-15900&viewport=528%2C298%2C0.35&t=3AEfehrhNBILWl7q-1&scaling=scale-down&starting-point-node-id=1517%3A10353&show-proto-sidebar=1&mode=design)