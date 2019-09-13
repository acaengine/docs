# SAML2 with ADFS

If using ADFS, [these steps](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust) can generally be followed. ACA Engine will use these four SAML2 claims:
  * Firstname
  * Lastname
  * Email Address
  * User ID (usually a login name, e.g. UPN or WindowsAccountName)
