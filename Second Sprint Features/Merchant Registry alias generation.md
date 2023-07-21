# Merchant Registry receives request

## Process flow

* When merchant record's registry status change to " Approved" from merchant acquisition system, OR DFSP with existing acquiring system use API to add new merchant record in merchant registry,
  * call the API of writing merchant record to "Merchant Registry" database.
    * following attributes will be transfer to the merchant registry system. [ check ERD ]
      * merchant ID
      * alias
      * location
  * check alias field
    * if alias is unique [ checking if there is any existing merchant record with the same alias]
      * no further action is taken.
    * Else If alias is NULL OR not unique
      * generate new alias. [to add further detail]
  * If the records came from the acquising system,
    * reflect "alias[ payinto ID ]" field of acquiring system with newly generated alias.
  * If the records came from DFSP's merchant registry API
    * return the records with updated ALIAS in the json. 
