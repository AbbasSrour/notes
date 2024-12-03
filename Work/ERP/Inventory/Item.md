## Form
### General
- [x] Barcode Type is cleared by track inventory by field.
- [x] When adding a category it should close the tab by default and assign it.
- [x] Fix the error message for category/family/brand giving expected number received NAN
- [x] Unit of measure doesn't give any message when required is there just red style for label.
- [x] Have UOM directly close to after the cost strategy since it is required
- [x] Specs add option permission path is empty
- [x] Should auto set category on creation and close the popup
- [x] Should auto set the family on creation and close the popup
- [x] Should auto set the brand on creation and close the popup 
- [x] Should auto set the tags on creation and close the popup
- [x] Add option on spec throws an error
- [x] Should auto set the specs on creation and close the popup
- [x] Move cost strategy to purchase/sales
- [x] Uom is empty
- [x] Close on select on Tags

### Inventory
- [x] Move the weight, length, height, and width to general
- [x] Rename the tab to stock
- [x] Warranty/Minimum Quantity /Weight /Length/ Height/ Width
- [x] Warranty Period input with dropdown sets the value of to 0 with expected number, received string error message.
- [x] Months spills of the input with dropdown 
- [x] Warranty period keeps being set to 0 after changing tabs
- [x] Track inventory by is reset when selecting a barcode


### Accounting
- [x] When creating a tax, tax percentage allows text and values > 100 move to number input
- [x] When creating a tax, no tax debtor/creditor balance account is shown
- [x] When creating Account Group, the header is transparent 
- [x] On asterisk on the required fields in create account group 

### Purchase
- [x] Two cost fields exist
- [x] Nan on cost fields minimum quantity and lead time
- [x] Required message in minimum quantity and lead time is expected number recieved NAN
- [x] no error message on default purchase unit of measure
- [x] saving the form causes lead time to become 0
- [x] no asterisk on minimum quantity order , lead time or default purchase unit of measure

### Sales 
- [x] Two selling Price fields exist 
- [x] No error message for default purchase unit of measure 
- [x] Name default purchase should be changed to default sale unit of measure ???
- [x] No asterisk on maximum discount or default purchase unit of measure

### POS 
- [x] Expected number recieved NAN error message, also add asterisk if required on the fields.
- [x] Expected number received string, in shelf life when changing value, same goes for end of life.
- [ ] Can input text in the fields


## Form
- [ ] Styles for description and input field should be the same.
- [ ] Remove arrows form number fields that have pickers.
- [ ] Weight - Height - Length - Width should not allow characters.
- [ ] Move Cost strategy to before cost field in purchase field.
- [ ] Remove arrows from Warranty Period, it also allows alphabetical characters.
- [ ] Weight - Height - Length - Width units when not submit doesn't show an error, also maybe add pulse animation to them so that the user can better notice them.
- [ ] Tax Debtor still doesn't show accounts.
- [ ] Barcode and uom keeps getting cleared
- [ ] Sales doesn't show accounts.
- [ ] Expenses doesn't show accounts.
- [ ] Purchase doesn't show accounts.
- [ ] POS doesn't show accounts.
- [ ] Assets doesn't show accounts.
- [ ] Label of options in input with dropdown should be uppercase in case of month/day...
- [ ] Input with dropdown allows adding alphabatical characters in week/days/.. fields.
- [ ] 