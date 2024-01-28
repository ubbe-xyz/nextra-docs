# errors

## Contents

- [Classes](errors.md#classes)
    - [AdapterError](errors.md#adaptererror)
    - [AuthError](errors.md#autherror)
    - [AuthorizedCallbackError](errors.md#authorizedcallbackerror)
    - [CallbackRouteError](errors.md#callbackrouteerror)
    - [CredentialsSignin](errors.md#credentialssignin)
    - [EmailSignInError](errors.md#emailsigninerror)
    - [ErrorPageLoop](errors.md#errorpageloop)
    - [EventError](errors.md#eventerror)
    - [InvalidCallbackUrl](errors.md#invalidcallbackurl)
    - [InvalidCheck](errors.md#invalidcheck)
    - [InvalidEndpoints](errors.md#invalidendpoints)
    - [InvalidProvider](errors.md#invalidprovider)
    - [JWTSessionError](errors.md#jwtsessionerror)
    - [MissingAdapter](errors.md#missingadapter)
    - [MissingAdapterMethods](errors.md#missingadaptermethods)
    - [MissingAuthorize](errors.md#missingauthorize)
    - [MissingCSRF](errors.md#missingcsrf)
    - [MissingSecret](errors.md#missingsecret)
    - [OAuthAccountNotLinked](errors.md#oauthaccountnotlinked)
    - [OAuthCallbackError](errors.md#oauthcallbackerror)
    - [OAuthProfileParseError](errors.md#oauthprofileparseerror)
    - [OAuthSignInError](errors.md#oauthsigninerror)
    - [SessionTokenError](errors.md#sessiontokenerror)
    - [SignOutError](errors.md#signouterror)
    - [UnknownAction](errors.md#unknownaction)
    - [UnsupportedStrategy](errors.md#unsupportedstrategy)
    - [UntrustedHost](errors.md#untrustedhost)
    - [Verification](errors.md#verification)

## Classes

### AdapterError

One of the database [`Adapter` methods](https://authjs.dev/reference/core/adapters#methods)
failed during execution.

:::tip
If `debug: true` is set, you can check out `[auth][debug]` in the logs to learn more about the failed adapter method execution.

#### Example

```sh
[auth][debug]: adapter_getUserByEmail
{ "args": [undefined] }
```
:::

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### AuthError

Base error class for all Auth.js errors.
It's optimized to be printed in the server logs in a nicely formatted way
via the [`logger.error`](https://authjs.dev/reference/core#logger) option.

#### Extends

- `Error`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

***

### AuthorizedCallbackError

Thrown when the execution of the [`signIn` callback](https://authjs.dev/reference/core/types#signin) fails
or if it returns `false`.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### CallbackRouteError

This error occurs when the user cannot finish login.
Depending on the provider type, this could have happened for multiple reasons.

:::tip
Check out `[auth][details]` in the logs to know which provider failed.

#### Example

```sh
[auth][details]: { "provider": "github" }
```
:::

For an [OAuth provider](https://authjs.dev/reference/core/providers/oauth), possible causes are:
- The user denied access to the application
- There was an error parsing the OAuth Profile:
  Check out the provider's `profile` or `userinfo.request` method to make sure
  it correctly fetches the user's profile.
- The `signIn` or `jwt` callback methods threw an uncaught error:
  Check the callback method implementations.

For an [Email provider](https://authjs.dev/reference/core/providers/email), possible causes are:
- The provided email/token combination was invalid/missing:
  Check if the provider's `sendVerificationRequest` method correctly sends the email.
- The provided email/token combination has expired:
  Ask the user to log in again.
- There was an error with the database:
  Check the database logs.

For a [Credentials provider](https://authjs.dev/reference/core/providers/credentials), possible causes are:
- The `authorize` method threw an uncaught error:
  Check the provider's `authorize` method.
- The `signIn` or `jwt` callback methods threw an uncaught error:
  Check the callback method implementations.

:::tip
Check out `[auth][cause]` in the error message for more details.
It will show the original stack trace.
:::

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### CredentialsSignin

The `authorize` callback returned `null` in the [Credentials provider](https://authjs.dev/getting-started/providers/credentials-tutorial).
We don't recommend providing information about which part of the credentials were wrong, as it might be abused by malicious hackers.

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### EmailSignInError

Happens when the login by an [Email provider](https://authjs.dev/getting-started/providers/email-tutorial) could not be started.

Possible causes are:
- The email sent from the client is invalid, could not be normalized by [`EmailConfig.normalizeIdentifier`](https://authjs.dev/reference/core/providers/email#normalizeidentifier)
- The provided email/token combination has expired:
  Ask the user to log in again.
- There was an error with the database:
  Check the database logs.

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### ErrorPageLoop

Thrown when Auth.js is misconfigured and accidentally tried to require authentication on a custom error page.
To prevent an infinite loop, Auth.js will instead render its default error page.

To fix this, make sure that the `error` page does not require authentication.

Learn more at [Guide: Error pages](https://authjs.dev/guides/basics/pages)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### EventError

One of the [`events` methods](https://authjs.dev/reference/core/types#eventcallbacks)
failed during execution.

Make sure that the `events` methods are implemented correctly and uncaught errors are handled.

Learn more at [`events`](https://authjs.dev/reference/core/types#eventcallbacks)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### InvalidCallbackUrl

Thrown when Auth.js is unable to verify a `callbackUrl` value.
The browser either disabled cookies or the `callbackUrl` is not a valid URL.

Somebody might have tried to manipulate the callback URL that Auth.js uses to redirect the user back to the configured `callbackUrl`/page.
This could be a malicious hacker trying to redirect the user to a phishing site.
To prevent this, Auth.js checks if the callback URL is valid and throws this error if it is not.

There is no action required, but it might be an indicator that somebody is trying to attack your application.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### InvalidCheck

Thrown when a PKCE, state or nonce OAuth check could not be performed.
This could happen if the OAuth provider is configured incorrectly or if the browser is blocking cookies.

Learn more at [`checks`](https://authjs.dev/reference/core/providers#checks)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### InvalidEndpoints

One of the configured OAuth or OIDC providers is missing the `authorization`, `token` or `userinfo`, or `issuer` configuration.
To perform OAuth or OIDC sign in, at least one of these endpoints is required.

Learn more at [`OAuth2Config`](https://authjs.dev/reference/core/providers#oauth2configprofile) or [Guide: OAuth Provider](https://authjs.dev/guides/providers/custom-provider)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### InvalidProvider

Thrown when the callback endpoint was incorrectly called without a provider.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### JWTSessionError

Logged on the server when Auth.js could not decode or encode a JWT-based (`strategy: "jwt"`) session.

Possible causes are either a misconfigured `secret` or a malformed JWT or `encode/decode` methods.

:::note
When this error is logged, the session cookie is destroyed.
:::

Learn more at [`secret`](https://authjs.dev/reference/core#secret), [`jwt.encode`](https://authjs.dev/reference/core/jwt#encode) or [`jwt.decode`](https://authjs.dev/reference/core/jwt#decode) for more information.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### MissingAdapter

Thrown if Auth.js is misonfigured. This could happen if you configured an Email provider but did not set up a database adapter,
or tried using a `strategy: "database"` session without a database adapter.
In both cases, make sure you either remove the configuration or add the missing adapter.

Learn more at [Database Adapters](https://authjs.dev/getting-started/adapters), [Email provider](https://authjs.dev/reference/core/providers/email) or [Concept: Database session strategy](https://authjs.dev/concepts/session-strategies#database)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### MissingAdapterMethods

Thrown similarily to [`MissingAdapter`](https://authjs.dev/reference/core/errors#missingadapter), but only some required methods were missing.

Make sure you either remove the configuration or add the missing methods to the adapter.

Learn more at [Database Adapters](https://authjs.dev/reference/core/adapters)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### MissingAuthorize

Thrown when a Credentials provider is missing the `authorize` configuration.
To perform credentials sign in, the `authorize` method is required.

Learn more at [Credentials provider](https://authjs.dev/reference/core/providers/credentials)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### MissingCSRF

Error for missing CSRF tokens in client-side actions (`signIn`, `signOut`, `useSession#update`).
Thrown when actions lack the double submit cookie, essential for CSRF protection.

CSRF ([Cross-Site Request Forgery](https://owasp.org/www-community/attacks/csrf))
is an attack leveraging authenticated user credentials for unauthorized actions.

Double submit cookie pattern, a CSRF defense, requires matching values in a cookie
and request parameter. More on this at [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Security/CSRF).

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### MissingSecret

Auth.js requires a secret or multiple secrets to be set, but none was not found. This is used to encrypt cookies, JWTs and other sensitive data.

:::note
If you are using a framework like Next.js, we try to automatically infer the secret from the `AUTH_SECRET`, `AUTH_SECRET_1`, etc. environment variables.
Alternatively, you can also explicitly set the [`AuthConfig.secret`](https://authjs.dev/reference/core#secret) option.
:::

:::tip
To generate a random string, you can use the Auth.js CLI: `npx auth secret`
:::

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### OAuthAccountNotLinked

Thrown when an Email address is already associated with an account
but the user is trying an OAuth account that is not linked to it.

For security reasons, Auth.js does not automatically link OAuth accounts to existing accounts if the user is not signed in.

:::tip
If you trust the OAuth provider to have verified the user's email address,
you can enable automatic account linking by setting [`allowDangerousEmailAccountLinking: true`](https://authjs.dev/reference/core/providers#allowdangerousemailaccountlinking)
in the provider configuration.
:::

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### OAuthCallbackError

Thrown when an OAuth provider returns an error during the sign in process.
This could happen for example if the user denied access to the application or there was a configuration error.

For a full list of possible reasons, check out the specification [Authorization Code Grant: Error Response](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.2.1)

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### OAuthProfileParseError

This error occurs during an OAuth sign in attempt when the provider's
response could not be parsed. This could for example happen if the provider's API
changed, or the [`OAuth2Config.profile`](https://authjs.dev/reference/core/providers/oauth#profile) method is not implemented correctly.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### OAuthSignInError

Happens when login by [OAuth](https://authjs.dev/getting-started/providers/oauth-tutorial) could not be started.

Possible causes are:
- The Authorization Server is not compliant with the [OAuth 2.0](https://www.ietf.org/rfc/rfc6749.html) or the [OIDC](https://openid.net/specs/openid-connect-core-1_0.html) specification.
  Check the details in the error message.

:::tip
Check out `[auth][details]` in the logs to know which provider failed.

#### Example

```sh
[auth][details]: { "provider": "github" }
```
:::

#### Extends

- `SignInError`

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

`SignInError.type`

***

### SessionTokenError

Logged on the server when Auth.js could not retrieve a session from the database (`strategy: "database"`).

The database adapter might be misconfigured or the database is not reachable.

Learn more at [Concept: Database session strategy](https://authjs.dev/concepts/session-strategies#database)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### SignOutError

Represents an error that occurs during the sign-out process. This error
is logged when there are issues in terminating a user's session, either
by failing to delete the session from the database (in database session
strategies) or encountering issues during other parts of the sign-out
process, such as emitting sign-out events or clearing session cookies.

The session cookie(s) are emptied even if this error is logged.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### UnknownAction

Auth.js was requested to handle an operation that it does not support.

See [`AuthAction`](https://authjs.dev/reference/core/types#authaction) for the supported actions.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### UnsupportedStrategy

Thrown when a Credentials provider is present but the JWT strategy (`strategy: "jwt"`) is not enabled.

Learn more at [`strategy`](https://authjs.dev/reference/core#strategy) or [Credentials provider](https://authjs.dev/reference/core/providers/credentials)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### UntrustedHost

Thrown when the `trustHost` option was not set to `true`.

Auth.js requires the `trustHost` option to be set to `true` since it's relying on the request headers' `host` value.

:::note
Official Auth.js libraries might attempt to automatically set the `trustHost` option to `true` if the request is coming from a trusted host on a trusted platform.
:::

Learn more at [`trustHost`](https://authjs.dev/reference/core#trusthost) or [Guide: Deployment](https://authjs.dev/getting-started/deployment)

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)

***

### Verification

The user's email/token combination was invalid.
This could be because the email/token combination was not found in the database,
or because the token has expired. Ask the user to log in again.

#### Extends

- [`AuthError`](errors.md#autherror)

#### Properties

##### type

> **type**: `ErrorType`

The error type. Used to identify the error in the logs.

###### Inherited from

[`errors.AuthError.type`](errors.md#type-1)