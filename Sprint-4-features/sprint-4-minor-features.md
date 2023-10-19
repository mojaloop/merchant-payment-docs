# Sprint-4-minor-features

## Logout

**As a** user (any type of user(hub user, DFSP user, merchant)), **I want** to log out anytime I want with a click of a button.

* After logging out, login page should be redirected and authentication tokens should be removed.

### Design File

* [logout with icon](https://www.figma.com/proto/sEFusJJ4pQedgXvfRixE7b/Merchant-Registry-Prototype?page-id=1435%3A7881&type=design&node-id=1500-8894&viewport=644%2C-1531%2C0.48&t=hCq5f5htO8ZoIX23-1&scaling=scale-down&starting-point-node-id=1500%3A8894)

## session time out

* session timeout limit = 1 day

## adding maker username in merchant table

* adding maker names can help users to check which records they should check and approve, without knowing record maker, they might waste time by checking the records when they don't have permission to give approval or rejection.

## Minor Changes

* In the merchant report table, “STATE” column is removed and “TOWN” column is added.
* Unnecessary checkboxes are removed from all merchant records table, reverted report table, rejected merchant table and approved merchant table. 
* In the pending merchant table, the checkboxes for the rows that the maker made are disabled to prevent checking the records he has updated.
* If a user opens a new tab after having already logged into the merchant payment portal in one tab, he shouldn't have to do it again.
* Additionally, if a user opens two tabs for a merchant payment portal and logs in to one of them, the other tab needs to right away log in as well.
