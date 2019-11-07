# SAML2 with Auth0

## Prerequesites

* You are an administrator of an Auth0 domain and would like ACAEngine user to be redirected to this Auth0 domain for signup and SSO login.

## Auth0 configuration

* Follow [these instructions](https://auth0.com/docs/dashboard/guides/applications/register-app-spa) to create a register a single-page-app for SAML2 SSO using Auth0
* The `Name` of the applicaiton can be the domain name on which your instance of ACAEngine is located.
* On the `Addons` tab, enable SAML2 Web App and use [these steps](https://auth0.com/docs/protocols/saml/saml2webapp-tutorial) as a guide.
* Set the `Application Callback URL` to match ACAEngine's `Assertion URL` \(e.g. [https:///auth/adfs/callback?id=adfs-XXXXXX\](https:///auth/adfs/callback?id=adfs-XXXXXX\)\)
* Paste in the below for `Settings`:

  ```text
  {"mappings": {  "email": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",  "full_name": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",  "upn": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"}}
  ```

