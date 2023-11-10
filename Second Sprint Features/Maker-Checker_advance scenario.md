# Maker, Checker  advanced scenario

## Case 1

* DFSP1 : D1U1, D1U2, D1U3,D1U4
* D1U1 created a record for merchant 001 saved as draft application.
  * in Merchant 001 table : maker => D1U1
  * in audit table,
    * Marchant_ID => 001
    * Action taken by => D1U1
    * Action Taken => Created record
    * entity name => xx [ one record for each entity for create records]
    * if the action is "Update"
      * new value will be merchant object after update action as JSON string
      * old value will be merchant object before update action as JSON string
* D1U2 update the record of 001 and submit the application.
  * in Merchant 001 table : maker =>D1U2, Status => "Review"
  * in audit table,
    * Marchant_ID =>001
    * Action taken by => D1U2
    * Action Taken => Updated record
* D1U3/D1U1 check the record of 001 merchant. [D1U1 can also be a checker for 001 since final submitter of that form is not D1U1]
  * in Merchant 001 table : Maker => D1U2, Checker =>D1U3, Status => "Reverted"/"Waiting for Alias generation","Rejected"
  * in audit table, 
    * Marchant_ID => 001
    * Action taken by =>D1U3
    * Action taken => Review the record
  * In case of "Revert"
    * D1U1, U1U2,U1U3[all of the users of the system can edit the form, ie 001 merchant record with status "REVERT" will appear in to be reverted report of all the users.]
    * After D1U1/D1U2 resubmit the form, the other users who do not make final submission of the form can check the form and continue the approval process.

| Error Message | Condition | Screen |
|----------|----------|----------|
| You cannot be as checker for the record you have updated as a maker | when user try to check the record he has updated (maker= login user while he is trying to take "approve" action) | Approval screen |
