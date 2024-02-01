# providers/netlify

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Netlify</b> integration.</span>
<a href="https://netlify.com">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/netlify.svg" height="48" width="48"/>
</a>
</div>

## default()

```ts
function default(config): OAuthConfig<Record<string, any>>
```

Add Netlify login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/netlify
```

#### Configuration
```js
import Auth from "@auth/core"
import Netlify from "@auth/core/providers/netlify"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Netlify({ clientId: NETLIFY_CLIENT_ID, clientSecret: NETLIFY_CLIENT_SECRET })],
})
```

### Resources

 - [Netlify OAuth blog](https://www.netlify.com/blog/2016/10/10/integrating-with-netlify-oauth2/)
 - [Netlify OAuth example](https://github.com/netlify/netlify-oauth-example/)

### Notes

By default, Auth.js assumes that the Netlify provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

:::tip

The Netlify provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/netlify.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

### Parameters

• **config**: `OAuthUserConfig`\<`Record`\<`string`, `any`\>\>

### Returns

`OAuthConfig`\<`Record`\<`string`, `any`\>\>