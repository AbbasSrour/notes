## Test
- [ ] Test that the dynamic keys for fields don't conflict with pre existing dynamic keys
- [ ] Test the system if we have more than 100 dynamic fields or dynamic groups
- [ ] Q2 Form With Add Groups
- [x] A6
- [x] A7
- [x] A8
- [x] A13 annual difference 
- [ ] A14 Non Life and unit linked
- [x] A16
- [ ] A21 and change dynamic fields to groups because it allows for same levels
- [ ] Percentage And Rate
- [ ] lower case and upper case dynamic key labels are treated the same
- [ ] If a form depepends on a second form and the form is not yet created its going to log an error, we want it to not log that error, A7 A6 A19 BPB are an example of that.
- [ ] IMPORTANT: if a report depends on a prior report we need to have it so that it creates it before creating the current one
- [ ] A13 Mics and Other branches I have no fucking way of calculating something over other branches, maybe new algo type????
- [ ] F2 Reports need to be recheck 
## Implement

- [ ] We need to make sure the operation is always safe to evaluate
- [ ] Change how we go about creating the form, we need to generate a json file, that is loaded and filled at each form creation
- [ ] During the form creation step we can have it so that we add field dependencies for auto calculated fields, this ways only triggered dependencies will be recalculated
- [ ] We change algorithms to an id instead of array for form field, and a have an object with a represention of the algo, i.e. field_algo = field_uuid * field_2_uuid + field_3_uuid for the frontend, or even the calculation on the backend. This can be a hasel for dynamic fields and groups because the algo will need to accomodated for that, example if before it field_uuid + field_2_uuid and then we added another field the algo will need to become field_uuid + field_2_uuid + field_3_uuid.
- [ ] We have it so that on updates only the fields mutated will be saved, this will help with the issue of quick burst of requests
- [ ] A6 - A7 dynamic keys are interlinked and this may cause an issue