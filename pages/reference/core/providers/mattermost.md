# providers/mattermost

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Mattermost</b> integration.</span>
<a href="https://mattermost.com">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/mattermost.svg" height="48" width="48"/>
</a>
</div>

## default()

```ts
function default<P>(config): OAuthConfig<P>
```

Add Mattermost login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/mattermost
```

#### Configuration
```js
import Auth from "@auth/core"
import Mattermost from "@auth/core/providers/mattermost"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Mattermost({ clientId: MATTERMOST_CLIENT_ID, clientSecret: MATTERMOST_CLIENT_SECRET, issuer: MATTERMOST_ISSUER // The base url of your Mattermost instance. e.g `https://my-cool-server.cloud.mattermost.com` })],
})
```

### Resources

 - [Mattermost OAuth documentation](https://example.com)

### Notes

By default, Auth.js assumes that the Mattermost provider is
based on the [OAuth 2](https://www.rfc-editor.org/rfc/rfc6749.html) specification.

To create your Mattermost OAuth2 app visit `http://<your Mattermost instance url>/<your team>/integrations/oauth2-apps`

:::warning

The Mattermost provider requires the `issuer` option to be set. This is the base url of your Mattermost instance. e.g https://my-cool-server.cloud.mattermost.com

:::

:::tip

The Mattermost provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/mattermost.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

### Type parameters

• **P** extends [`MattermostProfile`](/reference/core/providers/mattermost.md#mattermostprofile)

### Parameters

• **config**: `OAuthUserConfig`\<`P`\> & \{
  `issuer`: `string`;
  }

### Returns

`OAuthConfig`\<`P`\>

***

## MattermostProfile

[Get a user](https://api.mattermost.com/#tag/users/operation/GetUser)

### Properties

#### create\_at

```ts
create_at: number;
```

The time in milliseconds a user was created

#### delete\_at

```ts
delete_at: number;
```

The time in milliseconds a user was deleted

#### update\_at

```ts
update_at: number;
```

The time in milliseconds a user was last updated

#### terms\_of\_service\_create\_at?

```ts
terms_of_service_create_at?: number;
```

The time in milliseconds the user accepted the terms of service

#### terms\_of\_service\_id?

```ts
terms_of_service_id?: string;
```

ID of accepted terms of service, if any. This field is not present if empty.