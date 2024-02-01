# providers/descope

<div style={{display: "flex", justifyContent: "space-between", alignItems: "center"}}>
<span style={{fontSize: "1.35rem" }}>
 Built-in sign in with <b>Descope</b> integration.
</span>
<a href="https://descope.com" style={{backgroundColor: "#000000", padding: "12px", borderRadius: "100%" }}>
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/descope.svg" width="24"/>
</a>
</div>

## default()

```ts
function default(config): OIDCConfig<DescopeProfile>
```

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/descope
```

#### Configuration

Import the provider and configure it in your **Auth.js** initialization file:

```ts title="pages/api/auth/[...nextauth].ts"
import NextAuth from "next-auth"
import DescopeProvider from "next-auth/providers/descope";

export default NextAuth({
 providers: [
   DescopeProvider({
     clientId: process.env.DESCOPE_ID,
     clientSecret: process.env.DESCOPE_SECRET,
   }),
 ],
})
```

### Configuring Descope

Follow these steps:

1. Log into the [Descope console](https://app.descope.com)
2. Follow the [OIDC instructions](https://docs.descope.com/customize/auth/oidc)

Then, create a `.env.local` file in the project root add the following entries:

Get the following from the Descope's console:
```
DESCOPE_ID="<Descope Issuer's last url segment>" # Descope's Issuer can be found in "Authentication Methods > SSO > Identity Provider" (Can also be taken from "Project > Project ID")
DESCOPE_SECRET="<Descope Access Key>" # Manage > Access Keys
```

### Resources

- [Descope OIDC](https://docs.descope.com/customize/auth/oidc)
- [Descope Flows](https://docs.descope.com/customize/flows)

### Notes

The Descope provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/descope.ts). To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::info
By default, Auth.js assumes that the Descope provider is based on the [OIDC](https://openid.net/specs/openid-connect-core-1_0.html) spec
:::

## Help

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

### Parameters

• **config**: `OIDCUserConfig`\<[`DescopeProfile`](/reference/core/providers/descope.md#descopeprofile)\>

### Returns

[`OIDCConfig`](/reference/core/providers.md#oidcconfigprofile)\<[`DescopeProfile`](/reference/core/providers/descope.md#descopeprofile)\>

***

## DescopeProfile

The returned user profile from Descope when using the profile callback.
[See Load User](https://docs.descope.com/api/openapi/usermanagement/operation/LoadUser/)

### Indexable

 \[`claim`: `string`\]: `unknown`

### Properties

#### email

```ts
email: string;
```

The user's email

#### email\_verified

```ts
email_verified: boolean;
```

A boolean indicating if the user's email is verified

#### name

```ts
name: string;
```

The user's name

#### phone\_number

```ts
phone_number: string;
```

The user's phone number

#### phone\_number\_verified

```ts
phone_number_verified: boolean;
```

A boolean indicating if the user's phone number is verified

#### picture

```ts
picture: string;
```

The user's picture

#### sub

```ts
sub: string;
```

The user's unique Descope ID