# providers/auth0

<div style={{display: "flex", justifyContent: "space-between", alignItems: "center"}}>
<span style={{fontSize: "1.35rem" }}>
 Built-in sign in with <b>Auth0</b> integration.
</span>
<a href="https://auth0.com" style={{backgroundColor: "black", padding: "12px", borderRadius: "100%" }}>
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/auth0.svg" width="24"/>
</a>
</div>

## default()

```ts
function default(config): OIDCConfig<Auth0Profile>
```

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/auth0
```

#### Configuration

Import the provider and configure it in your **Auth.js** initialization file:

```ts title="pages/api/auth/[...nextauth].ts"
import NextAuth from "next-auth"
import Auth0Provider from "next-auth/providers/auth0"

export default NextAuth({
  providers: [
    Auth0Provider({
      clientId: process.env.AUTH0_ID,
      clientSecret: process.env.AUTH0_SECRET,
    }),
  ],
})
```

### Resources

- [Auth0 docs](https://auth0.com/docs/authenticate)

### Notes

The Auth0 provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/auth0.ts). To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

## Help

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

### Parameters

• **config**: `OIDCUserConfig`\<[`Auth0Profile`](/reference/core/providers/auth0.md#auth0profile)\>

### Returns

[`OIDCConfig`](/reference/core/providers.md#oidcconfigprofile)\<[`Auth0Profile`](/reference/core/providers/auth0.md#auth0profile)\>

***

## Auth0Profile

The returned user profile from Auth0 when using the profile callback. [Reference](https://auth0.com/docs/manage-users/user-accounts/user-profiles/user-profile-structure).

### Extends

- `Record`\<`string`, `any`\>

### Properties

#### app\_metadata

```ts
app_metadata: object;
```

Custom fields that store info about a user that influences the user's access, such as support plan, security roles (if not using the Authorization Core feature set), or access control groups. To learn more, read Metadata Overview.

#### blocked

```ts
blocked: boolean;
```

Indicates whether the user has been blocked. Importing enables subscribers to ensure that users remain blocked when migrating to Auth0.

#### created\_at

```ts
created_at: Date;
```

Timestamp indicating when the user profile was first created.

#### email

```ts
email: string;
```

(unique) The user's email address.

#### email\_verified

```ts
email_verified: boolean;
```

Indicates whether the user has verified their email address.

#### family\_name

```ts
family_name: string;
```

The user's family name.

#### given\_name

```ts
given_name: string;
```

The user's given name.

#### identities

```ts
identities: {
[key: string]: any;   connection: string;
  isSocial: boolean;
  profileData: object;
  provider: string;
  user_id: string;
  }[];
```

Contains info retrieved from the identity provider with which the user originally authenticates. Users may also link their profile to multiple identity providers; those identities will then also appear in this array. The contents of an individual identity provider object varies by provider. In some cases, it will also include an API Access Token to be used with the provider.

#### last\_ip

```ts
last_ip: string;
```

IP address associated with the user's last login.

#### last\_login

```ts
last_login: Date;
```

Timestamp indicating when the user last logged in. If a user is blocked and logs in, the blocked session updates last_login. If you are using this property from inside a Rule using the user< object, its value will be associated with the login that triggered the rule; this is because rules execute after login.

#### last\_password\_reset

```ts
last_password_reset: Date;
```

Timestamp indicating the last time the user's password was reset/changed. At user creation, this field does not exist. This property is only available for Database connections.

#### logins\_count

```ts
logins_count: number;
```

Number of times the user has logged in. If a user is blocked and logs in, the blocked session is counted in logins_count.

#### multifactor

```ts
multifactor: string;
```

List of multi-factor providers with which the user is enrolled.

#### name

```ts
name: string;
```

The user's full name.

#### nickname

```ts
nickname: string;
```

The user's nickname.

#### phone\_number

```ts
phone_number: string;
```

The user's phone number. Only valid for users with SMS connections.

#### phone\_verified

```ts
phone_verified: boolean;
```

Indicates whether the user has been verified their phone number. Only valid for users with SMS connections.

#### picture

```ts
picture: string;
```

URL pointing to the user's profile picture.

#### sub

```ts
sub: string;
```

The user's unique identifier.

#### updated\_at

```ts
updated_at: Date;
```

Timestamp indicating when the user's profile was last updated/modified. Changes to last_login are considered updates, so most of the time, updated_at will match last_login.

#### user\_id

```ts
user_id: string;
```

(unique) The user's identifier. Importing allows user records to be synchronized across multiple systems without using mapping tables.

#### user\_metadata

```ts
user_metadata: object;
```

Custom fields that store info about a user that does not impact what they can or cannot access, such as work address, home address, or user preferences. To learn more, read Metadata Overview.

#### username

```ts
username: string;
```

(unique) The user's username.