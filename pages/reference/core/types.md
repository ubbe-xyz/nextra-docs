# types

This module contains public types and interfaces of the core package.

## Installation

```bash npm2yarn
npm install @auth/core
```

You can then import this submodule from `@auth/core/type`.

## Usage

Even if you don't use TypeScript, IDEs like VSCode will pick up types to provide you with a better developer experience.
While you are typing, you will get suggestions about what certain objects/functions look like,
and sometimes links to documentation, examples, and other valuable resources.

Generally, you will not need to import types from this module.
Mostly when using the `Auth` function and optionally the `AuthConfig` interface,
everything inside there will already be typed.

:::tip
Inside the `Auth` function, you won't need to use a single type from this module.

## Example

```ts title=index.ts
import { Auth } from "@auth/core"

const request = new Request("https://example.com")
const response = await Auth(request, {
  callbacks: {
    jwt(): JWT { // <-- This is unnecessary!
      return { foo: "bar" }
    },
    session(
       { session, token }: { session: Session; token: JWT } // <-- This is unnecessary!
    ) {
      return session
    },
  }
})
```
:::

:::info
We are advocates of TypeScript, as it will help you catch errors at build-time, before your users do. 😉
:::

## Resources

- [TypeScript - The Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html)
- [Extending built-in types](https://authjs.dev/getting-started/typescript#module-augmentation)

## AuthAction

```ts
type AuthAction: 
  | "callback"
  | "csrf"
  | "error"
  | "providers"
  | "session"
  | "signin"
  | "signout"
  | "verify-request";
```

Supported actions by Auth.js. Each action map to a REST API endpoint.
Some actions have a `GET` and `POST` variant, depending on if the action
changes the state of the server.

- **`"callback"`**:
  - **`GET`**: Handles the callback from an [OAuth provider](https://authjs.dev/reference/core/providers/oauth).
  - **`POST`**: Handles the callback from a [Credentials provider](https://authjs.dev/reference/core/providers/credentials).
- **`"csrf"`**: Returns the raw CSRF token, which is saved in a cookie (encrypted).
It is used for CSRF protection, implementing the [double submit cookie](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#double-submit-cookie) technique.
:::note
Some frameworks have built-in CSRF protection and can therefore disable this action. In this case, the corresponding endpoint will return a 404 response. Read more at [`skipCSRFCheck`](https://authjs.dev/reference/core#skipcsrfcheck).
_⚠ We don't recommend manually disabling CSRF protection, unless you know what you're doing._
:::
- **`"error"`**: Renders the built-in error page.
- **`"providers"`**: Returns a client-safe list of all configured providers.
- **`"session"`**:
  - **`GET**`: Returns the user's session if it exists, otherwise `null`.
  - **`POST**`: Updates the user's session and returns the updated session.
- **`"signin"`**:
  - **`GET`**: Renders the built-in sign-in page.
  - **`POST`**: Initiates the sign-in flow.
- **`"signout"`**:
  - **`GET`**: Renders the built-in sign-out page.
  - **`POST`**: Initiates the sign-out flow. This will invalidate the user's session (deleting the cookie, and if there is a session in the database, it will be deleted as well).
- **`"verify-request"`**: Renders the built-in verification request page.

***

## ErrorPageParam

```ts
type ErrorPageParam: "Configuration" | "AccessDenied" | "Verification";
```

TODO: Check if all these are used/correct

***

## SignInPageErrorParam

```ts
type SignInPageErrorParam: 
  | "Signin"
  | "OAuthSignin"
  | "OAuthCallbackError"
  | "OAuthCreateAccount"
  | "EmailCreateAccount"
  | "Callback"
  | "OAuthAccountNotLinked"
  | "EmailSignin"
  | "CredentialsSignin"
  | "SessionRequired";
```

TODO: Check if all these are used/correct

***

## TokenSet

```ts
type TokenSet: Partial<OAuth2TokenEndpointResponse | OpenIDTokenEndpointResponse> & {
  expires_at: number;
};
```

Different tokens returned by OAuth Providers.
Some of them are available with different casing,
but they refer to the same value.

### Type declaration

#### expires\_at?

```ts
expires_at?: number;
```

Date of when the `access_token` expires in seconds.
This value is calculated from the `expires_in` value.

##### See

https://www.ietf.org/rfc/rfc6749.html#section-4.2.2

***

## Account

Usually contains information about the provider being used
and also extends `TokenSet`, which is different tokens returned by OAuth Providers.

### Extends

- `Partial`\<`OpenIDTokenEndpointResponse`\>

### Properties

#### provider

```ts
provider: string;
```

Provider's id for this account. Eg.: "google"

#### providerAccountId

```ts
providerAccountId: string;
```

This value depends on the type of the provider being used to create the account.
- oauth/oidc: The OAuth account's id, returned from the `profile()` callback.
- email: The user's email address.
- credentials: `id` returned from the `authorize()` callback

#### type

```ts
type: ProviderType;
```

Provider's type for this account

#### expires\_at?

```ts
expires_at?: number;
```

Calculated value based on OAuth2TokenEndpointResponse.expires_in.

It is the absolute timestamp (in seconds) when the OAuth2TokenEndpointResponse.access_token expires.

This value can be used for implementing token rotation together with OAuth2TokenEndpointResponse.refresh_token.

##### See

 - https://authjs.dev/guides/basics/refresh-token-rotation#database-strategy
 - https://www.rfc-editor.org/rfc/rfc6749#section-5.1

#### userId?

```ts
userId?: string;
```

id of the user this account belongs to

##### See

https://authjs.dev/reference/core/adapters#user

***

## CallbacksOptions\<P, A\>

Override the default session creation flow of Auth.js

### Type parameters

• **P** = [`Profile`](/reference/core/types.md#profile)

• **A** = [`Account`](/reference/core/types.md#account)

### Properties

#### jwt

```ts
jwt: (params: {
  account: null | A;
  token: JWT;
  user: User | AdapterUser;
  isNewUser: boolean;
  profile: P;
  session: any;
  trigger: "signIn" | "signUp" | "update";
}) => Awaitable<null | JWT>;
```

This callback is called whenever a JSON Web Token is created (i.e. at sign in)
or updated (i.e whenever a session is accessed in the client).
Its content is forwarded to the `session` callback,
where you can control what should be returned to the client.
Anything else will be kept from your front-end.

The JWT is encrypted by default.

[Documentation](https://next-auth.js.org/configuration/callbacks#jwt-callback) |
[`session` callback](https://next-auth.js.org/configuration/callbacks#session-callback)

##### Parameters

• **params**: \{
  `account`: `null` \| `A`;
  `token`: [`JWT`](/reference/core/jwt.md#jwt);
  `user`: [`User`](/reference/core/types.md#user) \| [`AdapterUser`](/reference/core/adapters.md#adapteruser);
  `isNewUser`: `boolean`;
  `profile`: `P`;
  `session`: `any`;
  `trigger`: `"signIn"` \| `"signUp"` \| `"update"`;
  }

• **params\.account**: `null` \| `A`

Contains information about the provider that was used to sign in.
Also includes [TokenSet](/reference/core/types.md#tokenset)

**Note**
available when `trigger` is `"signIn"` or `"signUp"`

• **params\.token**: [`JWT`](/reference/core/jwt.md#jwt)

When `trigger` is `"signIn"` or `"signUp"`, it will be a subset of [JWT](/reference/core/jwt.md#jwt),
`name`, `email` and `image` will be included.

Otherwise, it will be the full [JWT](/reference/core/jwt.md#jwt) for subsequent calls.

• **params\.user**: [`User`](/reference/core/types.md#user) \| [`AdapterUser`](/reference/core/adapters.md#adapteruser)

Either the result of the OAuthConfig.profile or the [CredentialsConfig.authorize](/reference/core/providers/credentials.md#authorize) callback.

**Note**
available when `trigger` is `"signIn"` or `"signUp"`.

Resources:
- [Credentials Provider](https://authjs.dev/reference/core/providers/credentials)
- [User database model](https://authjs.dev/reference/core/adapters#user)

• **params\.isNewUser?**: `boolean`

**Deprecated**
use `trigger === "signUp"` instead

• **params\.profile?**: `P`

The OAuth profile returned from your provider.
(In case of OIDC it will be the decoded ID Token or /userinfo response)

**Note**
available when `trigger` is `"signIn"`.

• **params\.session?**: `any`

When using [AuthConfig.session](/reference/core#session) `strategy: "jwt"`, this is the data
sent from the client via the [`useSession().update`](https://next-auth.js.org/getting-started/client#update-session) method.

⚠ Note, you should validate this data before using it.

• **params\.trigger?**: `"signIn"` \| `"signUp"` \| `"update"`

Check why was the jwt callback invoked. Possible reasons are:
- user sign-in: First time the callback is invoked, `user`, `profile` and `account` will be present.
- user sign-up: a user is created for the first time in the database (when [AuthConfig.session](/reference/core#session).strategy is set to `"database"`)
- update event: Triggered by the [`useSession().update`](https://next-auth.js.org/getting-started/client#update-session) method.
In case of the latter, `trigger` will be `undefined`.

##### Returns

`Awaitable`\<`null` \| [`JWT`](/reference/core/jwt.md#jwt)\>

#### redirect

```ts
redirect: (params: {
  baseUrl: string;
  url: string;
}) => Awaitable<string>;
```

This callback is called anytime the user is redirected to a callback URL (e.g. on signin or signout).
By default only URLs on the same URL as the site are allowed,
you can use this callback to customise that behaviour.

[Documentation](https://authjs.dev/guides/basics/callbacks#redirect-callback)

##### Parameters

• **params**: \{
  `baseUrl`: `string`;
  `url`: `string`;
  }

• **params\.baseUrl**: `string`

Default base URL of site (can be used as fallback)

• **params\.url**: `string`

URL provided as callback URL by the client

##### Returns

`Awaitable`\<`string`\>

#### session

```ts
session: (params: {
  session: {
     user: AdapterUser;
  } & AdapterSession;
  user: AdapterUser;
  } & {
  session: Session;
  token: JWT;
  } & {
  newSession: any;
  trigger: "update";
}) => Awaitable<Session | DefaultSession>;
```

This callback is called whenever a session is checked.
(Eg.: invoking the `/api/session` endpoint, using `useSession` or `getSession`)

⚠ By default, only a subset (email, name, image)
of the token is returned for increased security.

If you want to make something available you added to the token through the `jwt` callback,
you have to explicitly forward it here to make it available to the client.

##### Parameters

• **params**: \{
  `session`: \{
     `user`: [`AdapterUser`](/reference/core/adapters.md#adapteruser);
  } & [`AdapterSession`](/reference/core/adapters.md#adaptersession);
  `user`: [`AdapterUser`](/reference/core/adapters.md#adapteruser);
  } & \{
  `session`: [`Session`](/reference/core/types.md#session-2);
  `token`: [`JWT`](/reference/core/jwt.md#jwt);
  } & \{
  `newSession`: `any`;
  `trigger`: `"update"`;
  }

##### Returns

`Awaitable`\<[`Session`](/reference/core/types.md#session-2) \| `DefaultSession`\>

##### See

[`jwt` callback](https://authjs.dev/reference/core/types#jwt)

#### signIn

```ts
signIn: (params: {
  account: null | A;
  user: User | AdapterUser;
  credentials: Record<string, CredentialInput>;
  email: {
     verificationRequest: boolean;
  };
  profile: P;
}) => Awaitable<string | boolean>;
```

Controls whether a user is allowed to sign in or not.
Returning `true` continues the sign-in flow.
Returning `false` or throwing an error will stop the sign-in flow and redirect the user to the error page.
Returning a string will redirect the user to the specified URL.

Unhandled errors will throw an `AuthorizedCallbackError` with the message set to the original error.

##### Parameters

• **params**: \{
  `account`: `null` \| `A`;
  `user`: [`User`](/reference/core/types.md#user) \| [`AdapterUser`](/reference/core/adapters.md#adapteruser);
  `credentials`: `Record`\<`string`, [`CredentialInput`](/reference/core/providers/credentials.md#credentialinput)\>;
  `email`: \{
     `verificationRequest`: `boolean`;
  };
  `profile`: `P`;
  }

• **params\.account**: `null` \| `A`

• **params\.user**: [`User`](/reference/core/types.md#user) \| [`AdapterUser`](/reference/core/adapters.md#adapteruser)

• **params\.credentials?**: `Record`\<`string`, [`CredentialInput`](/reference/core/providers/credentials.md#credentialinput)\>

If Credentials provider is used, it contains the user credentials

• **params\.email?**: \{
  `verificationRequest`: `boolean`;
  }

If Email provider is used, on the first call, it contains a
`verificationRequest: true` property to indicate it is being triggered in the verification request flow.
When the callback is invoked after a user has clicked on a sign in link,
this property will not be present. You can check for the `verificationRequest` property
to avoid sending emails to addresses or domains on a blocklist or to only explicitly generate them
for email address in an allow list.

• **params\.email\.verificationRequest?**: `boolean`

• **params\.profile?**: `P`

If OAuth provider is used, it contains the full
OAuth profile returned by your provider.

##### Returns

`Awaitable`\<`string` \| `boolean`\>

##### See

[`AuthorizedCallbackError`](https://authjs.dev/reference/errors#authorizedcallbackerror)

##### Example

```ts
callbacks: {
 async signIn({ profile }) {
  // Only allow sign in for users with email addresses ending with "yourdomain.com"
  return profile?.email?.endsWith("@yourdomain.com")
}
```

***

## CookieOption

[Documentation](https://authjs.dev/reference/core#cookies)

***

## CookiesOptions

[Documentation](https://authjs.dev/reference/core#cookies)

***

## EventCallbacks

The various event callbacks you can register for from next-auth

[Documentation](https://authjs.dev/guides/basics/events)

### Properties

#### session

```ts
session: (message: {
  session: Session;
  token: JWT;
}) => Awaitable<void>;
```

The message object will contain one of these depending on
if you use JWT or database persisted sessions:
- `token`: The JWT for this session.
- `session`: The session object from your adapter.

##### Parameters

• **message**: \{
  `session`: [`Session`](/reference/core/types.md#session-2);
  `token`: [`JWT`](/reference/core/jwt.md#jwt);
  }

• **message\.session**: [`Session`](/reference/core/types.md#session-2)

• **message\.token**: [`JWT`](/reference/core/jwt.md#jwt)

##### Returns

`Awaitable`\<`void`\>

#### signIn

```ts
signIn: (message: {
  account: null | Account;
  user: User;
  isNewUser: boolean;
  profile: Profile;
}) => Awaitable<void>;
```

If using a `credentials` type auth, the user is the raw response from your
credential provider.
For other providers, you'll get the User object from your adapter, the account,
and an indicator if the user was new to your Adapter.

##### Parameters

• **message**: \{
  `account`: `null` \| [`Account`](/reference/core/types.md#account);
  `user`: [`User`](/reference/core/types.md#user);
  `isNewUser`: `boolean`;
  `profile`: [`Profile`](/reference/core/types.md#profile);
  }

• **message\.account**: `null` \| [`Account`](/reference/core/types.md#account)

• **message\.user**: [`User`](/reference/core/types.md#user)

• **message\.isNewUser?**: `boolean`

• **message\.profile?**: [`Profile`](/reference/core/types.md#profile)

##### Returns

`Awaitable`\<`void`\>

#### signOut

```ts
signOut: (message: {
  session: undefined | null | void | AdapterSession;
  } | {
  token: null | JWT;
}) => Awaitable<void>;
```

The message object will contain one of these depending on
if you use JWT or database persisted sessions:
- `token`: The JWT for this session.
- `session`: The session object from your adapter that is being ended.

##### Parameters

• **message**: \{
  `session`: `undefined` \| `null` \| `void` \| [`AdapterSession`](/reference/core/adapters.md#adaptersession);
  } \| \{
  `token`: `null` \| [`JWT`](/reference/core/jwt.md#jwt);
  }

##### Returns

`Awaitable`\<`void`\>

***

## LoggerInstance

Override any of the methods, and the rest will use the default logger.

[Documentation](https://authjs.dev/reference/core#authconfig#logger)

### Extends

- `Record`\<`string`, `Function`\>

***

## Profile

The user info returned from your OAuth provider.

### See

https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims

***

## Session

The active session of the logged in user.

### Extends

- `DefaultSession`

***

## Theme

Change the theme of the built-in pages.

[Documentation](https://authjs.dev/reference/core#authconfig#theme) |
[Pages](https://authjs.dev/guides/basics/pages)

***

## User

The shape of the returned object in the OAuth providers' `profile` callback,
available in the `jwt` and `session` callbacks,
or the second parameter of the `session` callback, when using a database.

### Extended by

- [`AdapterUser`](/reference/core/adapters.md#adapteruser)