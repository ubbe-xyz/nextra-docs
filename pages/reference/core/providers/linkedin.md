# providers/linkedin

<div style={{backgroundColor: "#000", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Linkedin</b> integration.</span>
<a href="https://linkedin.com">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/linkedin.svg" height="48" width="48"/>
</a>
</div>

## Contents

- [Interfaces](linkedin.md#interfaces)
    - [LinkedInProfile](linkedin.md#linkedinprofile)
- [Functions](linkedin.md#functions)
    - [default](linkedin.md#default)

## Interfaces

### LinkedInProfile

#### See

https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/sign-in-with-linkedin-v2#response-body-schema

#### Extends

- `Record`\<`string`, `any`\>

## Functions

### default()

> **default**\<`P`\>(`options`): [`OIDCConfig`](../providers.md#oidcconfigprofile)\<`P`\>

Add LinkedIn login to your page.

### Setup

#### Callback URL
```
https://example.com/api/auth/callback/linkedin
```

#### Configuration
```js
import Auth from "@auth/core"
import LinkedIn from "@auth/core/providers/linkedin"

const request = new Request(origin)
const response = await Auth(request, {
  providers: [LinkedIn({ clientId: LINKEDIN_CLIENT_ID, clientSecret: LINKEDIN_CLIENT_SECRET })],
})
```

### Resources

 - [LinkedIn OAuth documentation](https://docs.microsoft.com/en-us/linkedin/shared/authentication/authorization-code-flow)
 - [LinkedIn app console](https://www.linkedin.com/developers/apps/)

### Notes

By default, Auth.js assumes that the LinkedIn provider is
based on the [OIDC](https://openid.net/specs/openid-connect-core-1_0.html) specification.

:::tip

The LinkedIn provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/linkedin.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

#### Type parameters

• **P** extends [`LinkedInProfile`](linkedin.md#linkedinprofile)

#### Parameters

• **options**: `OIDCUserConfig`\<`P`\>

#### Returns

[`OIDCConfig`](../providers.md#oidcconfigprofile)\<`P`\>