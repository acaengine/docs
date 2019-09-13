# SAML2 using Auth0.com

## Prerequesites
* You are an administrator of an Auth0 domain and would like Engine user to be redirected to this Auth0 domain for signup and SSO login.

## Auth0 configuration
* Follow [these instructions](https://auth0.com/docs/dashboard/guides/applications/register-app-spa) to create a register a single-page-app for SAML2 SSO using Auth0
* The `Name` of the applicaiton can be the domain name on which your instance of Engine is located.
* On the `Addons` tab, enable SAML2 Web App and use [these steps](https://auth0.com/docs/protocols/saml/saml2webapp-tutorial) as a guide.
* Set the `Application Callback URL` to match Engine's `Assertion URL` (e.g. https://<engine-domain>/auth/adfs/callback?id=adfs-XXXXXX)
* Paste in the below for `Settings`:
```
{
  "mappings": {
    "email": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
    "full_name": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "upn": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
  }
}
```
