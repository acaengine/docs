# SAML2 with Azure AD

If using Azure Active Directory for SSO, [these instructions](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-optional-claims) can be followed for understanding and adding the above 4 optional claims to the the SAML2 token. Generally, two fields of the app Manifest need to be edited and the below steps can be followed to update the Manifest:

* Login to portal.azure.com and browse to [Azure AD &gt; App Registrations](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)
* Locate the existing app that was created for [o365 Graph API access](https://github.com/acaprojects/docs/tree/be220954cefb53b2ac2ca82f775a56993117e99d/deployment/single-sign-on/integrations/directory-services/microsoft-office365.md). If none has been created yet, then create a new app registration now, as this app can be used for both SSO and o365 Graph API access.
* Select the new/existing app and then select Manfiest from the menu.
* In the editor, set [groupMembershipClaims](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-optional-claims#configuring-group-optional-claims) to either `“All”` or `“SecurityGroup”`. [This page](https://blogs.msdn.microsoft.com/waws/2017/03/13/azure-app-service-authentication-aad-groups/) may help you decide which is most suitable for your organisation:
  * `“SecurityGroup”` - groups claim will contain the identifiers of all security groups of which the user is a member.
  * `“All”` - groups claim will contain the identifiers of all security groups and all distribution lists of which the user is a member
* Set the value of the `optionalClaims"`to include the above 4 claims \(firstname, lastname, user ID, email address\) in the saml2Token. An example is below:

  ```text
    "optionalClaims": {      "idToken": [],      "accessToken": [],      "saml2Token": [          {              "name": "email",              "essential": true,          },          {              "name": "upn",              "essential": true,          },          {              "name": "family_name",              "essential": true,          },          {              "name": "given_name",              "essential": true          }      ]  },
  ```

