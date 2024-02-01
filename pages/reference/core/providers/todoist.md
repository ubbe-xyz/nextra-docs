# providers/todoist

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Todoist</b> integration.</span>
<a href="https://www.todoist.com/">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/todoist.svg" height="48" />
</a>
</div>

## default()

```ts
function default<P>(options): OAuthConfig<P>
```

Add Todoist login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/todoist
```

#### Configuration
```js
import Auth from "@auth/core"
import Todoist from "@auth/core/providers/todoist"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Todoist({ clientId: TODOIST_CLIENT_ID, clientSecret: TODOIST_CLIENT_SECRET })],
})
```

### Resources

- [Todoist OAuth documentation](https://developer.todoist.com/guides/#oauth)
- [Todoist configuration](https://developer.todoist.com/appconsole.html)

### Notes

By default, Auth.js assumes that the Todoist provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

:::tip

The Todoist provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/todoist.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

### Type parameters

• **P** extends `TodoistProfile`

### Parameters

• **options**: `OAuthUserConfig`\<`P`\>

### Returns

`OAuthConfig`\<`P`\>