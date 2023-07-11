# Simple merchant registration 
## Registration Save As Draft Feature 

**As a** merchant and DFSP operator, **I want to** get save as draft feature for my work-in-progress application form **so that** I can save my progress and prevent any loss of work when my work gets interrupted. 

### Acceptance Criteria
* Save work-in-progress application form as draft and reload the progress when user want to continue filling out the form.
* When user click "save as draft" button, system ask user to confirm the action.
    * Message : " Are you sure you want to save the progress as draft?"
    * If user choose "Yes", system will respond with " Saving form progress as draft is successful", in case of failed action, system will respond with " something went wrong while saving as draft, Try again"
* Next time user enter the system and navigate to add new merchant page, user will see " continue saved draft application", " add new record" buttons.  
* when user click " continue saved draft application", work-in-progress of saved draft will be reloaded and user can continue filling the form. 