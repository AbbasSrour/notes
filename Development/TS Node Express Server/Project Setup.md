## Node
We first start by generation the `package.json` file which is responsible for handling the project details and settings.
```bash
pnpm init -y && pnpm add -D @types/node
```

Some useful scripts to have in the `package.json`
```json
// package.json
{
  "scripts": {
    "start": "pnpm cross-env NODE_ENV=production node build/src/index.js",
    "dev:ts": "pnpm cross-env NODE_ENV=development ts-node-dev --respawn --transpile-only --exit-child src/index.ts",
    "dev:js": "concurrently -k \"pnpm tsc --watch\" \"pnpm cross-env NODE_ENV=development nodemon './build/src/index.js'\"",
    "test": "jest --watchAll --coverage --verbose",
    "build": "pnpm tsc",
	}
}
```

## Typescript
To add typescript for the project and setup some its settings we use:
```bash
pnpm add -D typescript ts-node ts-node-dev && pnpm tsc --init
```

The `tsconfig.json` is the file responsible for the ts settings should be added the root of the project, it is of utmost importance to set the build path and root directory:
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "es2017",
    //...
    "outDir": "./build",
    "rootDir": "."
  },
}
```

The second important thing is adding the exclude and include to make sure not everything gets compiled, `node_modules` folder should be compiled though.
```json
{
  "compilerOptions": {
 //...
  },
  "exclude": ["tests", "./jest.config.ts", "src/migrations"],
  "inculde": [/*I usually don't add anything here*/]
}
```

Third thing to take notice is to setup the `ts-node` to make sure that during development and testing everything goes smoothly and to make sure not everything gets transpiled:
```json
 {
	//...
  "ts-node": {
    "transpileOnly": true,
    "files": true,
    "compilerOptions": {
      "rootDir": "."
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules", "tests"]
  }
}
```

### Issues
* When the test is done two times making sure the `"exclude"` and `"include"` in the `tsconfig.json`  `ts-node` section are defined will alleviate that.

## Environment

### Setting Up The Environment 
Environment variables are a fundamental part of developing with Node. js, **allowing your app to behave differently based on the environment you want them to run in**. Wherever your app needs configuration, you use environment variables.

The secret environment variables are set in `*.env` files that are placed in the root of the project, usually `.env` being the default one and used if the environment is not defined with the command that starts the backend process.

```env
// *.env
NODE_ENV=<production/development/stage>
```

The environmental variables are usually initialized in the *main* file (index.ts/js) of the project or the file that needs initialization variables and runs first. The `dotenv module` which is also installed as a production dependency, is first called to load the environmental variables based on the environmental stage.
```bash
pnpm add dotenv
```

```ts
// src/index.js/ts
import path from "path";
import dotenv from "dotenv";
dotenv.config({
  path: path.resolve(__dirname, `../${process.env.NODE_ENV}.env`),
});
```

The command used to set the environment is usually:
```bash
NODE_ENV=<projectstage> pnpm run ...
```

Although `cross-env module` can be used to make this work across different Operating Systems, and is installed as a *dev dependency*:
```bash
pnpm add -D cross-env
```
```bash
pnpm cross-env NODE_ENV=<projectstage> node/nodmon/ts...
```

To get the value of an environmental variable in the `*.env` file we use:
```ts
process.env.env-variable-of-choice
```

### Extending The Functionality
The `config module` is used to extend the functionality of the environmental variables, and is installed as a production dependency. It requires a folder called config placed at the root of the project and it's responsible for the handling of environment variables by the project and delivering it to them. This is done through two functionalities:
```bash
pnpm add config && pnpm add -D @types/config
```

- The first one is done by the different `config/<environmentstage>.ts` files which hold different not secret variables, to be used in the project.
```ts
// config/produciton.ts
export default {
  origin: "http://localhost:3000",
  accessTokenExpiresIn: 15,
  refreshTokenExpiresIn: 60,
  redisCacheExpiresIn: 60,
};
```

- The second one is mapping the secret environmental to a json like object, the value of these objects will change based on the set environment.
```ts
// config/custom-environment-variables.ts
export default {
  port: 'PORT',
  enviroment: 'NODE_ENV',
	...
  postgresConfig: {
    host: 'PSQL_DB_URL',
    ...
  },
  accessTokenPrivateKey: 'JWT_ACCESS_TOKEN_PRIVATE_KEY',
	...
};
```

Then to load the values of a specific variable using the `config module`: 
```ts
import config from "config";
const port = config.get<number>("port");
```

```ts
//  or if a variable is part of an object
const dbName = config.get<{ database: string }("postgresConfig")["database"];
```

```ts
// multiple values from an object 
const dbProps = config.get<{database:string; name: string; port:number}>("postgresConfig")["database"];
```

### Environment Validation 
The validation of the environment can be done with a `envalid module` a production dependency that will throw an error if an environment variable type is not correct. *It is important to catch the error*.

```bash
pnpm add envalid
```

```ts
// src/utils/validate-env.util.ts
import { cleanEnv, port, str } from 'envalid';
const ValidateEnv = () => {
  cleanEnv(process.env, {
    NODE_ENV: str(),
    PORT: port(),
    PSQL_DB_URL: str(),
    //...
    JWT_REFRESH_TOKEN_PUBLIC_KEY: str(),
  });
};
export default ValidateEnv;
```
```ts
// src/index.ts/js
import ValidateEnv from "./utils/validate-env.utl"
ValidateENV();
```

### Issues
* Making sure to use the `dotenv.config({})` is a file is initialized before the `index.ts/js` to alleviate issues related to missing environment variables. 
