## Merchant acquision  

**As a** DFSP user, **I want to** add newly acquired merchant to the system **so that** I can onboard new merchant to use the system.  

 ### Acceptance Criteria 

* Process Sequence Flow  
    * user stories and requirements/DFSP onboard merchant.md [merchant registry and acquisition portal connection 
    * Maker will add newly acquired merchant with registration status “PENDING”  
        * Adding new records should be able to performed by following options 
            * Bulk upload by formated CSV,excel  
            * Single record by form  
* Link : Merchant Location and checkout counter connection 
* Following data attributes will be captured in acquisition level  
    * Business information  
        * Doing Business As Name  
        * Registered Name 
        * number of employee [dropdown] 
            * 0-5 
            * 6-10 
            * 11-50 
            * 51-100 
            * 100++ 
        * monthly turn over 
        * merchant category [drowdown] 
            * food and beverage 
            * agricultural 
            * livestock 
            * production 
        * utility 
        * DFSP name [dropdown] 
            * AA 
            * BB 
            * CC 
        * Location information [multiple location] 
        * Location type  
            * Virtual  
            * Physical  
        * Country [dropdown]  
        * State [dropdown] //remark : state list should be reflected to chosen country 
        * City[dropdown] // remark : city list should be reflected to chosen state 
        * Longitude Latitude [optional] 
        * Website URL [optional] 
        * Full address [free text] // need to update according to ERD
        * Check out counter description[ to display in customer app/ussd] [multiple addable]  
    * Business owner information [multiple owner] 
        * Name  
        * National ID  
        * Nationality [dropdown] 
        * Address [full text] 
        * Phone number 
        * Email [optional] 
    * Contact person  
        * // condition : if user click: same as business owner, copy business owner information into contact person, if there are more than one business owner added in biz owner section, ask user with a drop down] 
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