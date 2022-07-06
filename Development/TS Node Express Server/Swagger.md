## Swagger
Swagger is a suite of APIs to document and develop web apis, to use swagger in a node express two packages must be installed:
```bash 
pnpm install swagger-ui-express swagger-jsdoc
```

```ts
// src/index.ts
const swaggerUI = require("swagger-ui-express");
const swaggerDocs = require("./docs/swagger.ts");

const swaggerOpts = {
  explorer: true,
};
app.use("/docs", swaggerUI.serve, swaggerUI.setup(swaggerDocs));
```

```ts
// src/docs/swagger.ts
module.exports = {
  openapi: "3.0.1",
  info: {
    version: "1.0.0",
    title: "Dionysus",
    description: "Movie Streaming Service",
    contact: {
      name: "Abbas Srour",
      email: "abbas.mj.srour@gmail.com",
      url: "https://abbassrour.ml",
    },
  },
};
```
