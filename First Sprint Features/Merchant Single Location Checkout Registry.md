# Simple merchant registration 
## Registration Form 
As a DFSP maker, I want to register simple merchant to the acquirer system with 2 methods [ single form input or bulk input by excel file] so that its data can be transferred to registry system and generate alias. 

### Acceptance Criteria
* Simple merchant can be identified as following criteria
    * Merchant with single location/single checkout counter, single payintoID, account and contact person. 
* After submitting the merchant form, system will notify to DFSP checker to check the form. 
    * until DFSP checker has approved/rejected the form, Registration Status of particular merchant will be "Pending" 
    * After DFSP checker has approved/rejected the form, " the registration status " will be changed to " Approved", "Rejected" 
    * Approved merchant records from acquiring system will be reflected to the Registry system. 
* following data points will be captured in the acquiring step. 
    * Business information  
        * Doing Business As Name  [Single line, Requried]
        * Registered Name [Single line, Not Requried]
        * Payinto Account
        * number of employee [Dropdown, Requried]
            * 0-5 
            * 6-10 
            * 11-50 
            * 51-100 
            * 100++ 
        * monthly turn over [Dropdown, Requried]
        * merchant category [Dropdown, Not Requried]
            * Individual
            * Small Shop
            * Chain Store
        * Registered DFSP name [Dropdown, Not Requried] 
            * Populated from DFSP table
    * Location information 
    * Location type  [Dropdown, Requried] 
        * Virtual  
        * Physical  
    * Country [dropdown ,Not Requried]  
    * State [dropdown ,Not Requried] //remark : state list should be reflected to chosen country 
    * City[dropdown ,Not Requried] // remark : city list should be reflected to chosen state 
    * Longitude Latitude [Not Requried] 
    * Website URL [Not Requried] 
    * Full address [free text] // need to update according to ERD
    * Check out counter description[ to display in customer app/ussd] [single line, Required]
* Business owner information 
    * Name  
    * National ID  
    * Nationality [dropdown, Requried] 
    * Physical Address  [visual - sub group]
        * Department [Not Requried]
        * Sub Department [Not Requried]
        * Street Name [Not Requried]
        * Building Number [Not Requried]
        * Building Name [Not Requried]
        * Floor Number [Not Requried]
        * Room Number [Not Requried]
        * Post Box [Not Requried]
        * Postal Code [Not Requried]
        * Township [Not Requried]
        * District [Not Requried]
        * Country Subdivision(State/division) [Not Requried]
        * Country  [Dropdown, Requried]
        * Longitude [Not Requried]
        * Latitude [Not Requried]
    * Phone number [phone number, Requried]
    * Email [Not Requried] 
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