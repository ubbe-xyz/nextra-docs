# providers/tiktok

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Tiktok</b> integration.</span>
<a href="https://www.tiktok.com/">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/tiktok.svg" height="48" />
</a>
</div>

## Contents

- [Interfaces](tiktok.md#interfaces)
    - [TiktokProfile](tiktok.md#tiktokprofile)
- [Functions](tiktok.md#functions)
    - [default](tiktok.md#default)

## Interfaces

### TiktokProfile

[More info](https://developers.tiktok.com/doc/tiktok-api-v2-get-user-info/)

#### Extends

- `Record`\<`string`, `any`\>

## Functions

### default()

> **default**\<`P`\>(`options`): `OAuthConfig`\<`P`\>

Add Tiktok login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/tiktok
```

#### Configuration
```js
import Auth from "@auth/core"
import Tiktok from "@auth/core/providers/tiktok"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Tiktok({ clientId: TIKTOK_CLIENT_KEY, clientSecret: TIKTOK_CLIENT_SECRET })],
})
```

### Resources
 - [Tiktok app console](https://developers.tiktok.com/)
 - [Tiktok login kit documentation](https://developers.tiktok.com/doc/login-kit-web/)
 - [Avaliable Scopes](https://developers.tiktok.com/doc/tiktok-api-scopes/)

### Notes

:::tip

Production applications cannot use localhost URLs to sign in with Tiktok. You need add the domain and Callback/Redirect url's to your Tiktok app and have them review and approved by the Tiktok Team.

:::

:::tip

Email address is not supported by Tiktok.

:::

:::tip

Client_ID will be the Client Key in the Tiktok Application

:::

By default, Auth.js assumes that the Tiktok provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

:::tip

The Tiktok provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/tiktok.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

#### Type parameters

• **P** extends [`TiktokProfile`](tiktok.md#tiktokprofile)

#### Parameters

• **options**: `OAuthUserConfig`\<`P`\>

#### Returns

`OAuthConfig`\<`P`\>