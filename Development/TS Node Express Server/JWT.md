# JWT
Jsonwebtoken is a standard to create and save user sessions to allow the users of a site not to authenticate and login every time they send a request to the server after the initial login stage. Jsonwebtokens can used node by installing the jsonwebtoken module.
```bash
pnpm install jsonwebtoken
```

## Creating JWT
Jwt utilities can be created to generate token that user will use to access the site. 
We first start by creating a wrapper utility function around `jwt.sign()` to create new refresher/access token, the function takes:
-  ***Payload:*** Which is some claims about an entity usually the user entity. Claims are just information about this entity they might be the userId, uuid, email, username... 
- ***Key Name:*** The second part is the key name  which specifies if the service needs to create a refresher token or a new access token.
- ***Options:*** Specifies the options with which the jwt will be created.

The function takes the params, retrieves the key specified from the environmental variables and changes it from its `hex` encoding to `ascii` encoding then passes it the `jwt.sign()` function where it generates the token. 
```ts
// src/utils/jwt.util
export const signJwt = async (payload: object, keyName: "accessTokenPrivateKey" | "refreshTokenPrivateKey",options: SignOptions) => {
  const privateKey = Buffer.from(config.get<string>(keyName), "hex").toString("acsii");
  return jwt.sign(payload, privateKey, {
    ...(options && options),
    algorithm: "RS256",
  });
};
```

## Verifying The JWT
Since the user will have to send back the jwt token every time it needs to access something on the server the verification of the token is needed, thus we create a wrapper function around `jwt.verify` to make our lives easier.

The function takes a the *token* and the type of the token then it retrieves the key assigned to each situation, changes it to ASCII encoding and passes it back to `jwt.verify()`. The`jwt.verify` function will either return decoded message or will throw an error if the token is not valid and return a null. Thus we return the decoded as a generic type in case of everything going well or return null if we caught an error.

```ts
// src/utils/jwt.util.ts
export const verifyJwt = <T>(token: string, keyName: "accessTokenPublicKey" | "refreshTokenPublicKey"): T | null => {
  try {
    const publicKey = Buffer.from(config.get<string>(keyName), "hex").toString("ascii");
    const decoded = jwt.verify(token, publicKey) as T;
    return decoded;
  } catch (error) {
    return null;
  }
};
```

## Services To Handle JWT
We create a function to create a session in the redis database with the userId of the user as a key and the user data as the data. Which is then used to create a refresher token and an access token.
```ts
// src/services/users.services.ts
export const signTokens = async (user: User) => {
  // 1. Create Session
  redisClient.set(`${user.id}`, JSON.stringify(user), {
    EX: config.get<number>('redisCacheExpiresIn') * 60,
  });

  // 2. Create Access and Refresh tokens
  const access_token = signJwt({ sub: user.userId }, 'accessTokenPrivateKey', {
    expiresIn: `${config.get<number>('accessTokenExpiresIn')}m`,
  });

  const refresh_token = signJwt({ sub: user.id }, 'refreshTokenPrivateKey', {
    expiresIn: `${config.get<number>('refreshTokenExpiresIn')}m`,
  });

  return { access_token, refresh_token };
};
```