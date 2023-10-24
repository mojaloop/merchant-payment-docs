# User Story

- As a DFSP user, I want to register merchants with multiple locations and multiple checkout counters in the merchant acquiring system portal so that those merchants can also be a part of the payment system.

Acceptance Criteria:

- When I log in to the merchant acquiring portal, I should have the option to register a new merchant.
- While registering a merchant, I should be able to provide information about multiple locations for that merchant, including the location name, address, and other relevant details in ISO format.
- For each location, I should be able to specify the checkout counters associated with that location. Each checkout counter should be associated with a unique ID.
- The system should automatically generate a unique alias for each checkout counter.If there is at least one checkout counter for a location, there must be an alias for that checkout counter.
- After registering the merchant with its locations and checkout counters, there should be a clear association and connection link established between the different locations and checkout counters in the system's database.
- The system should allow me to filter the list of accounts by merchant ID, location ID, and checkout counter ID. This filtering functionality should be easily accessible and user-friendly.
- If a location has multiple checkout counters, I should be able to see the details of each checkout counter, including its alias, when I view the merchant's information.
- If a location has no checkout counters, it should be clearly indicated in the system from user interface.
- The alias for each checkout counter should be displayed and stored alongside the checkout counter's ID in the system.
- The system should ensure that each checkout counter's alias is unique and not duplicated.