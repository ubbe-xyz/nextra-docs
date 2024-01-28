# providers/box

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Box</b> integration.</span>
<a href="https://box.com/">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/box.svg" height="48" width="48"/>
</a>
</div>

## Contents

- [Functions](box.md#functions)
    - [default](box.md#default)

## Functions

### default()

> **default**(`options`): `OAuthConfig`\<`Record`\<`string`, `any`\>\>

Add Box login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/box
```

#### Configuration
```js
import Auth from "@auth/core"
import Box from "@auth/core/providers/box"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Box({ clientId: BOX_CLIENT_ID, clientSecret: BOX_CLIENT_SECRET })],
})
```

### Resources

 - [Box developers documentation](https://developer.box.com/reference/)
 - [Box OAuth documentation](https://developer.box.com/guides/sso-identities-and-app-users/connect-okta-to-app-users/configure-box/)

### Notes

By default, Auth.js assumes that the Box provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

:::tip

The Box provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/box.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

#### Parameters

• **options**: `OAuthUserConfig`\<`Record`\<`string`, `any`\>\>

#### Returns

`OAuthConfig`\<`Record`\<`string`, `any`\>\>