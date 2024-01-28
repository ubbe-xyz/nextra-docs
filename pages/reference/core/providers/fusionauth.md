# providers/fusionauth

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>FusionAuth</b> integration.</span>
<a href="https://fusionauth.com">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/fushionauth.svg" height="48" width="48"/>
</a>
</div>

## Contents

- [Interfaces](fusionauth.md#interfaces)
    - [FusionAuthProfile](fusionauth.md#fusionauthprofile)
- [Functions](fusionauth.md#functions)
    - [default](fusionauth.md#default)

## Interfaces

### FusionAuthProfile

This is the default openid signature returned from FusionAuth
it can be customized using [lambda functions](https://fusionauth.io/docs/v1/tech/lambdas)

#### Extends

- `Record`\<`string`, `any`\>

## Functions

### default()

> **default**\<`P`\>(`options`): `OAuthConfig`\<`P`\>

Add FusionAuth login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/fusionauth
```

#### Configuration
```js
import Auth from "@auth/core"
import FusionAuth from "@auth/core/providers/fusionauth"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [FusionAuth({ clientId: FUSIONAUTH_CLIENT_ID, clientSecret: FUSIONAUTH_CLIENT_SECRET, tenantId: FUSIONAUTH_TENANT_ID, issuer: FUSIONAUTH_ISSUER })],
})
```
:::warning
If you're using multi-tenancy, you need to pass in the tenantId option to apply the proper theme.
:::

### Resources

 - [FusionAuth OAuth documentation](https://fusionauth.io/docs/v1/tech/oauth/)

### Notes

By default, Auth.js assumes that the FusionAuth provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

## Configuration
:::tip
An application can be created at https://your-fusionauth-server-url/admin/application.

For more information, follow the [FusionAuth 5-minute setup guide](https://fusionauth.io/docs/v1/tech/5-minute-setup-guide).
:::

In the OAuth settings for your application, configure the following.

- Redirect URL
  - https://localhost:3000/api/auth/callback/fusionauth
- Enabled grants
  - Make sure _Authorization Code_ is enabled.

If using JSON Web Tokens, you need to make sure the signing algorithm is RS256, you can create an RS256 key pair by
going to Settings, Key Master, generate RSA and choosing SHA-256 as algorithm. After that, go to the JWT settings of
your application and select this key as Access Token signing key and Id Token signing key.
:::tip

The FusionAuth provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/fusionauth.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

#### Type parameters

• **P** extends [`FusionAuthProfile`](fusionauth.md#fusionauthprofile)

#### Parameters

• **options**: `OAuthUserConfig`\<`P`\> & `Object`

#### Returns

`OAuthConfig`\<`P`\>