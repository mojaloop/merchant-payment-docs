## Merchant Location and checkout counter connection  

**As a** system implementor, **I want to** cover following scenarios for merchant and location registration **so that** any size of merchants can take part in the merchant registration process in an inclusive manner.  

### Acceptance Criteria
* Merchant <=> Location <=> Checkout Counter  

    * Since merchant can have one to multiple locations 
    * Single location can have zero checkout to multiple checkout counters.  
    * Each checkout counter will have a unique ID and alias so that they can receive payment and notified when they have received the fund.   