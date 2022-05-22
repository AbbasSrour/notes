 # View
 In some cases it is not desirable for all users to see the entire logical model, so we use a *view*  which is any relation that is not of the conceptual model but is made visible to a user as a "virtual relation".
 A view is defined using the create view statement which is has the form 
 ```sql
 create view v as <query expression>
``` 
where query expression is any legal relation algebra query expression., and v being the view name.