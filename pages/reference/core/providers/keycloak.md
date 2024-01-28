# providers/keycloak

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Keycloak</b> integration.</span>
<a href="https://keycloak.com">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/keycloak.svg" height="48" width="48"/>
</a>
</div>

## Contents

- [Functions](keycloak.md#functions)
    - [default](keycloak.md#default)

## Functions

### default()

> **default**\<`P`\>(`options`): `OAuthConfig`\<`P`\>

Add Keycloak login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/keycloak
```

#### Configuration
```js
import Auth from "@auth/core"
import Keycloak from "@auth/core/providers/keycloak"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [Keycloak({ clientId: KEYCLOAK_CLIENT_ID, clientSecret: KEYCLOAK_CLIENT_SECRET, issuer: KEYCLOAK_ISSUER, })],
})
```

### Resources

 - [Keycloak OIDC documentation](https://www.keycloak.org/docs/latest/server_admin/#_oidc_clients)

:::tip

Create an openid-connect client in Keycloak with "confidential" as the "Access Type".

:::

:::note

issuer should include the realm – e.g. https://my-keycloak-domain.com/realms/My_Realm

:::
### Notes

By default, Auth.js assumes that the Keycloak provider is
based on the [Open ID Connect](https://openid.net/specs/openid-connect-core-1_0.html) specification.

:::tip

The Keycloak provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/keycloak.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

#### Type parameters

• **P** extends `KeycloakProfile`

#### Parameters

• **options**: `OAuthUserConfig`\<`P`\>

#### Returns

`OAuthConfig`\<`P`\>