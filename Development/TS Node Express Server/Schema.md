## Schema
Creating schemas for the different entities will add a safety check on data integrity of the data in the database, and parse the data received from the client to make inserting it in the database easier. The npm `zod module` can be used to insure that.

```bash
pnpm install zod
```

Basic usage of `zod` can be as following
```ts
import {number, string, object, TypeOf } from "zod"

export const Schema = object({
	body:object({
		attribute1: string({}).min(x,"").max(x,"").length(x,"");
		...
	}),
});
export type Input = TypeOf<typeof Schema>["body"];
// Or to ommit an attribute in case of password confirmation for example
export type Input = Omit<TypeOf<typeof Schema>["body"], "attribute1">
```

### Validation And Parsing
To validate and parse the data received from the client against a predefined schema we created we create a middleware between the route and the controller. 

The function needs the schema and it will parse the body of the request into the schema and validate the data sent by the client, the params, and the query, then call the next function in the stack.

If a error occurs with respect the data received being of bad value, the middleware will send back the error else if the error is not related to the schema the error will be sent along to the next function in the stack and handled there.
```ts
// src/middleware/validate.middleware.ts
import { AnyZodObject, ZodError } from "zod";
import { Request, Response, NextFunction } from "express";

export const Validate = async (schema: AnyZodObject) => (req: Request, res: Response, next: NextFunction) => {
  try {
    schema.parse({
      params: req.params,
      query: req.query,
      body: req.body,
    })
  } catch (error) {
    if (error instanceof ZodError)
      return res.status(400).json({
        status: "fail",
        error: error.errors,
      });
    next(error);
  }
} 
```
