---
description: >-
  Steps required for enabling SAML2 sign on for users logging in to all
  ACAEngine web apps
---

# Configuring ACAEngine for SAML2

By default, ACAEngine uses local authentication. An admin account is generated upon initial deployment and the administrator can manually create additional user accounts in the ACAEngine Backoffice \(on the Users tab\).

Switching to federated authentication is recommended. There are 3 steps required:

1. In ACAEngine Backoffice, create a new SAML2 Identitiy provider entry.
2. In your organisation's SAML2 Identity provider dashboard \(e.g. Azure AD, ADFS, Auth0\), create the SAML2 Service provider for entry for ACAEngine.
3. Back in ACAEngine Backoffice, update the SAML2 Identity provider entry with the new details retrieved from step 2.

## Prerequisites

1. The domain where users will visit to login must exist as a valid **DNS** entry 
2. Browsers should consider the domain secure: Valid **SSL certificates** should be in place and served by either your load balancer or the web server in front of ACAEngine.

## Step 1

1. Login as an admin to backoffice \(https://&lt;engine-url&gt;/backoffice/\)
2. On the **Domains** tab, select the Domain that represents the URL you wish to enable SAML2 for.
3. In the Authentication section click "Add new", select "**SAML2 / ADFS**"
4. In the "New Authentication Source" Window, 

   1. Enter a descriptive **Name** that represents your SAML2 Identity provider, e.g. "MyCompany ADFS"
   2. Enter some temporary text \(any text\) into the "**IDP Target URL**" field. It will be edited later with the correct details.
   3. Enter some temporary text \(any text\) into the "**Assertion URL**" field. It will be edited later with the correct details.

5. Click **Save**
6. The new Authentication source will now appear in the list. **Copy the URL** to your clipboard.
7. Click edit on the Authentication source which was just created.
   1. In the Assertion URL field, paste the URL which was copied in the previous step, but edit it to include "/callback"
   2. Example: If you copied _"https://engine.myorganisation.com/auth/adfs?id=adfs-XXXXXXXX"_ then set the Assertion URL to "_https://engine.myorganisation.com/auth/adfs/callback?id=adfs-XXXXXXXX"_
   3. Click Save

## Step 2

You will need to enter these details from Step 1 into your SAML2 Identity provider dashboard:

1. 
Follow the instructions for your Identity Provider:

* [Azure AD](https://app.gitbook.com/@acaengine/s/docs/~/drafts/-LwHHdlhyEubZB8JHLVU/deployment/single-sign-on/saml2-with-azure-ad)
* [ADFS](https://app.gitbook.com/@acaengine/s/docs/~/drafts/-LwHHdlhyEubZB8JHLVU/deployment/single-sign-on/saml2-with-adfs)
* [Auth0](https://app.gitbook.com/@acaengine/s/docs/~/drafts/-LwHHdlhyEubZB8JHLVU/deployment/single-sign-on/saml2-with-auth0)
* [GSuite](https://app.gitbook.com/@acaengine/s/docs/~/drafts/-LwHHdlhyEubZB8JHLVU/deployment/single-sign-on/saml2-with-gsuite)

## Step 3

You will enter these details from Step 2 into ACAEngine Backoffice:

1. Issuer
2. IDP Target URL





