# Alias Generation Checklist

## acceptance criteria

* to update oracle database
* to create API end points that are mentioned in the powerpoint
* to create scheduler job

## out of scope

* PUT /parties interface
  * Reason is that it assumes that Participant will create Alias and put in Oracle. Currently, we are only developing “CreateAlias” end-point which creates an Alias and links it to requesting DFSP also.
  * Secondly, PUT /parties interface currently does not support extension information which we need to capture i.e. Merchant Identifier.
