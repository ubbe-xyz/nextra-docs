# providers/azure-ad-b2c

<div style={{backgroundColor: "#0072c6", display: "flex", justifyContent: "space-between", color: "#fff", padding: 16}}>
<span>Built-in <b>Azure AD B2C</b> integration.</span>
<a href="https://learn.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-tenant">
  <img style={{display: "block"}} src="https://authjs.dev/img/providers/azure.svg" height="48" width="48"/>
</a>
</div>

## default()

```ts
function default(options): OIDCConfig<AzureADB2CProfile>
```

Add Azure AD B2C login to your page.

## Configuration

### Basic

Basic configuration sets up Azure AD B2C to return an ID Token. This should be done as a prerequisite prior to running through the Advanced configuration.

1. [Azure AD B2C Tenant](https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-tenant)
2. [App Registration](https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-register-applications)
3. [User Flow](https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-user-flows)

For the step "User attributes and token claims" set the following:

- Collect attribute:
  - Email Address
  - Display Name
  - Given Name
  - Surname
- Return claim:
  - Email Addresses
  - Display Name
  - Given Name
  - Surname
  - Identity Provider
  - Identity Provider Access Token
  - User's Object ID

### Parameters

• **options**: `OIDCUserConfig`\<[`AzureADB2CProfile`](/reference/core/providers/azure-ad-b2c.md#azureadb2cprofile)\> & \{
  `primaryUserFlow`: `string`;
  `tenantId`: `string`;
  }

### Returns

[`OIDCConfig`](/reference/core/providers.md#oidcconfigprofile)\<[`AzureADB2CProfile`](/reference/core/providers/azure-ad-b2c.md#azureadb2cprofile)\>

### Example

```ts
import { Auth } from "@auth/core"
import AzureADB2C from "@auth/core/providers/azure-ad-b2c"

const request = new Request("https://example.com")
const response = await AuthHandler(request, {
  // optionally, you can pass `tenantId` and `primaryUserFlow` instead of `issuer`
  providers: [AzureADB2C({ clientId: "", clientSecret: "", issuer: "" })],
})
```

---

### Resources

- [Azure Active Directory B2C documentation](https://learn.microsoft.com/en-us/azure/active-directory-b2c)

---

### Notes

By default, Auth.js assumes that the Azure AD B2C provider is
based on the [OIDC](https://openid.net/specs/openid-connect-core-1_0.html) specification.

:::tip

The Azure AD B2C provider comes with a [default configuration](https://github.com/nextauthjs/next-auth/blob/main/packages/core/src/providers/azure-ad-b2c.ts).
To override the defaults for your use case, check out [customizing a built-in OAuth provider](https://authjs.dev/guides/providers/custom-provider#override-default-options).

:::

:::info **Disclaimer**

If you think you found a bug in the default configuration, you can [open an issue](https://authjs.dev/new/provider-issue).

Auth.js strictly adheres to the specification and it cannot take responsibility for any deviation from
the spec by the provider. You can open an issue, but if the problem is non-compliance with the spec,
we might not pursue a resolution. You can ask for more help in [Discussions](https://authjs.dev/new/github-discussions).

:::

***

## AzureADB2CProfile

### See

[Claims](https://learn.microsoft.com/en-us/azure/active-directory-b2c/tokens-overview#claims)