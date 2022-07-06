# Register User
The procedure of registering a new user starts with the user sending a post request with the data of the new user, which is then validated and parsed using the [[Middleware#Schema#Validation And Parsing|Validate Middleware Function]].
```ts
// src/routes/auth.route.ts
Router.post("/register", Validate(RegisterUserSchema), registerUserHandler);
```

The next function is the controller which decomposes the request body for the user data then creates a user entity with the data using the `createUser` function in the user entity, if an error occurs at this step then it will most likely be because of a database error. Then the verification code is generated, hashed, and saved to the user entity. Email verification is then sent to the user, if an error occurs because of this then the verification code is set to null.

```ts
// src/controllers/auth.controller.ts
export const registerUserHandler = async (
  req: Request<{}, {}, RegisterUserInput>,
  res: Response,
  next: NextFunction
) => {
  try {
    const { email, password, userName, age, firstName, lastName } = req.body;
    const user = await createUser({
      email: email.toLowerCase(),
      password: password,
      userName: userName,
      age: age,
      firstName: firstName,
      lastName: lastName,
    });

    // email verification process
    const { hashedVerificationCode, verificationCode } = Users.createVerificationCode();
    user.verificationCode = hashedVerificationCode;
    await user.save();
    const redirectUrl = `${config.get<string>(
      'origin'
    )}/verifyemail/${verificationCode}`;
    try {
      await new Email(user, redirectUrl).sendVerificationCode();
      res.status(201).json({
        status: 'success',
        message:
          'An email with a verification code has been sent to your email',
      });
    } catch (error) {
      user.verificationCode = null;
      await user.save();

      return res.status(500).json({
        status: 'error',
        message: 'There was an error sending email, please try again',
      });
    }
  } catch (error: any) {
    if (error.code === "23505") {
      return res.status(409).json({
        status: "fail",
        message: "User with that email already exist",
      });
    }
    next(error);
  }
};
```

# Login User
The procedure of logging 
```ts
// src/routes/auth.route.ts
Router.post("/login", Validate(LoginUserSchema), loginUserHandler);
```

```ts
// src/controllers/auth.controller.ts
const cookiesOptions: CookieOptions = {
  httpOnly: true,
  sameSite: 'lax',
};

if (process.env.NODE_ENV === 'production') cookiesOptions.secure = true;
```

```ts
// src/controllers/auth.controller.ts
const accessTokenCookieOptions: CookieOptions = {
  ...cookiesOptions,
  expires: new Date(
    Date.now() + config.get<number>('accessTokenExpiresIn') * 60 * 1000
  ),
  maxAge: config.get<number>('accessTokenExpiresIn') * 60 * 1000,
};
```

```ts
const refreshTokenCookieOptions: CookieOptions = {
  ...cookiesOptions,
  expires: new Date(
    Date.now() + config.get<number>('refreshTokenExpiresIn') * 60 * 1000
  ),
  maxAge: config.get<number>('refreshTokenExpiresIn') * 60 * 1000,
};
```

```ts
// src/controllers/auth.controller.ts
export const loginUserHandler = async (
  req: Request<{}, {}, LoginUserInput>,
  res: Response,
  next: NextFunction
) => {
  try {
    const { email, password } = req.body;
    const user = await findUserByEmail({ email });

    if (!user || !(await Users.comparePasswords(password, user.password))) {
      return next(new AppError(400, "Invalid email or password"));
    }

    const { accessToken, refreshToken } = await signTokens(user);
    res.cookie("access_token", accessToken, accessTokenCookieOptions);
    res.cookie("refresh_token", refreshToken, refreshTokenCookieOptions);
    res.cookie("logged_in", true, {
      ...accessTokenCookieOptions,
      httpOnly: false,
    });

    res.status(200).json({
      status: "success",
      accessToken,
    });
  } catch (error: any) {
    next(error);
  }
};
```


# Refresh Access Token

```ts
// src/routes/auth.route.ts
router.get('/refresh', refreshAccessTokenHandler);
```

```ts
// src/controllers/auth.controller.ts
const cookiesOptions: CookieOptions = {
  httpOnly: true,
  sameSite: 'lax',
};

if (process.env.NODE_ENV === 'production') cookiesOptions.secure = true;
```

```ts
// src/controllers/auth.controller.ts
const accessTokenCookieOptions: CookieOptions = {
  ...cookiesOptions,
  expires: new Date(
    Date.now() + config.get<number>('accessTokenExpiresIn') * 60 * 1000
  ),
  maxAge: config.get<number>('accessTokenExpiresIn') * 60 * 1000,
};
```

```ts
// src/controllers/auth.controller.ts
export const refreshAccessTokenHandler = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const message = "Could not access the refresh token";

    const refreshToken = req.cookies.refreshToken;
    if (!refreshToken) return next(new AppError(403, message));

    const decoded = verifyJwt<{ sub: string }>(
      refreshToken,
      "refreshTokenPublicKey"
    );
    if (!decoded) return next(new AppError(403, message));

    const session = await RedisClient.get(decoded.sub);
    if (!session) return next(new AppError(403, message));

    const user = await findUserById(JSON.parse(session).userId);
    if (!user) return next(new AppError(403, message));

    const accessToken = signJwt({ sub: user.userId }, "accessTokenPrivateKey", {
      expiresIn: `${config.get<number>("accessTokenExpiresIn")}m`,
    });

    res.cookie('accessToken', accessToken, accessTokenCookieOptions);
    res.cookie('logged_in', true, { ...accessTokenCookieOptions, httpOnly: false, })

    res.status(200).json({
      status: 'success',
      accessToken,
    });
  } catch (error) {
    next(error);
  }
};
```

# Logout User

```ts
// src/routes/auth.route.ts
router.get('/logout', deserializeUser, requireUser, logoutHandler);
```

```ts
// src/controllers/auth.controller.ts
export const logoutHandler = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const user = res.locals.user;

    await RedisClient.del(user.id);

    res.cookie('accessToken', '', { maxAge: -1 });
    res.cookie('refreshToken', '', { maxAge: -1 });
    res.cookie('logged_in', '', { maxAge: -1 });

    res.status(200).json({
      status: 'success',
    });
  } catch (err: any) {
    next(err);
  }
};
```


#  Get User
```ts
// src/routes/users.route.ts
Router.get("/me", deserializeUser, requireUser, getMeHandler);
```

```ts
// src/controllers/users.controller.ts
import { NextFunction, Request, Response } from 'express';

export const getMeHandler = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const user = res.locals.user;

    res.status(200).status(200).json({
      status: 'success',
      data: {
        user,
      },
    });
  } catch (err: any) {
    next(err);
  }
};
```
