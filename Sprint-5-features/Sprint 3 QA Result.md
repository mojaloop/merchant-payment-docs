## Bug lists to fix form sprint 3 QA results


* “Reset Password” api shouldn’t allow users to create a password that is less than 8 characters.
* Super admin users shouldn’t have permission to assign super admin roles.
* Admin users shouldn’t have permission to assign super admin roles.
* Admin users shouldn’t have permission to assign admin roles.
* In “create new merchant draft” api, "dba_trading_name" should be mandatory.
* When “Update the status of a Merchant to Reject" api is called, the registration status of the filled draft id should be changed to rejected. [“Bulk Rejected the registration status of multiple merchant records” api works properly.]
* When the “Export with ids” api is called, the reports of the filled ids should be downloaded properly. [Right now, when this api is called, "socket hang up" error occurs. When I test it from swagger, it shows “failed to fetch”.]