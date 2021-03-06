# Microsoft Office365

Engine integrates with Microsoft Office 365 via [Graph API](https://docs.microsoft.com/en-us/graph/overview). An Azure Active Directory admin must use Azure Portal to create an "App Registration" for Engine, and then details of this app registration will be configured in Engine.

## Create an App Registration in Azure Portal

The below Microsoft article and video can be referred to for additional context:

* Article: [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)
* Video: [Getting Started with Microsoft Graph and Application Registration](https://www.youtube.com/watch?v=93j0MmRruFo)

An Azure user with admin permissions for Azure Active Directory will need to perform these actions:

### Register the App

1. Login to the Azure Portal and view the ["App Registrations" page of the "Azure Active Directory" blade](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
2. If an existing App has been registered for Engine for use with Azure Single-Sign-On \(SAML2\), then we can re-use this app - select it. If not, then click "New registration"
3. Type a descriptive name for the application, set the Supported account Type to _"Accounts in this organizational directory only"_ and leave the Redirect URI blank. Click "Register".

### Configure App permissions

While still in Azure Portal on the page for the above registered App:

1. In the menu on the left, select “API permissions” and click “Add a permission”. Then select “Microsoft Graph” as the API and select **Application Permissions** as the permission.
2. Typically, allow the below permissions \(the list may vary depending on the desired functionality/restrictions on the web applications that will be using this Graph API integration\):
   * `User.Read.All`
   * `Group.Read.All`
   * `Calendars.ReadWrite`
   * `Contacts.Read.All`
   * `Place.Read.All`
3. After adding the required Application permissions, click "Grant admin consent for ACA Projects" on the "API Permissions" page of the registered App, then click Yes.
4. On the "Overview" page of the App, copy the below two values, which will be used in the next section to configure Engine to connect to this Registered App:
   * `Application (client) ID`
   * `Directory (tenant) ID`
5. On the "Certificates & secrets" page of the App, click "New client secret":
   * Add a meaningful description
   * Set Expiry to "Never", or as appropriate \(ACA will no longer be allowed to use this credential after expiry\)
   * Copy the Value of the secret, as it will be used in the next section to configure Engine.

Now you should have collected 3 text values that will be used in the next section:

* `Application (client) ID`
* `Directory (tenant) ID`
* `Client secret`

### Optional: Restrict App access to specified AD Groups only

To restrict the Graph App's access to only the objects that exist in specified AD groups, [**Application Access Policies**](https://docs.microsoft.com/en-us/powershell/module/exchange/organization/new-applicationaccesspolicy?view=exchange-ps) can be used.

1. Ensure those resources \(users, rooms\) exist in those AD groups 
2. Use Powershell to add the new policy, e.g:

`# Restrict to a group of Rooms    
New-ApplicationAccessPolicy -AppId <Graph App ID> -PolicyScopeGroupId <AD group that all bookable rooms exist in> -AccessRight RestrictAccess -Description "Restrict this app to Engine bookable rooms"`

`# Restrict to a group of Users    
New-ApplicationAccessPolicy -AppId <Graph App ID> -PolicyScopeGroupId <AD group that all staff app users exist in> -AccessRight RestrictAccess -Description "Restrict this app to Engine app users"`

## Configure Engine to connect to Graph API

1. Login to [https://&lt;your-engine-url&gt;/backoffice/\#/drivers/](https://<your-engine-url>/backoffice/#/drivers/) and select an existing or create a new “Office365 Room Booking Panel Logic” driver and click edit \(pen icon at top right\). Note down the driver ID, which you will see in the browser URL bar and looks like “dep-xxxxxxxx” \(you will need this later\)
2. Enter the o365 values \(client, secret, tenant\) into the the placeholders which you should see. These values are on the portal.azure.com page where you created the Azure App Registration \(above\), then click Save.
   * `“office_client_id”`
   * `“office_tenant”`
   * `“office_secret”`
   * Tip: Sensitive values \(like office\_secret\) can be encrypted by inserting `$` in front of the setting name \(e.g. `“$office_secret”: "xxxx"`\)
3. Test the configuration by navigating to a System which has a Device \(module\) instance of the above Driver \(or create a Device instance\).
   * Edit the System: Set the System’s Email to a real email address that exists on the o365 tenant
   * On the About page of the system, Select `Bookings 1` from "Execute command", then select the function `fetch_bookings` and click “Send”. 
   * An array of booking details \(blue\) should be returned \(it might be empty `[]` if there are no bookings\), or an error \(red\), if there is an issue grabbing the events from o365.
   * If blue, then the settings are correct and is currently being used for all Room Booking Panels. In the next step we'll configure Engine Staff API to use the same credentials.
   * If red, capture the error from javascript console \(e.g. Chrome debug tools, Console tab\) which will help yourself, an integration partner or ACA to pinpoint the cause.
4. Navigate to Domains \(menu bar on left\). Select the Domain that you’d like integrated with this Office 365 tenant and click it, then click edit \(pen icon at top right\).
5. In the "Config" box, ensure that the “o365\_driver” value exactly matches the driver ID of the “Office365 Room Booking Panel Logic” driver which you gathered in step 1 \(e.g. "dep-xxxxxxxx”"\). Click Save. If there is none, then create one like this:
   * `"o365_driver": "dep-xxxxxxxx"`
6. Test the Staff API integration by logging into an app that uses Staff API \(e.g. Engine template Staff App\) with a user who’s Calendar exists in the configured o365 tenant’s Exchange directory. You should be able to view/create events as this user.
   * If there are issues, note down the error information from requests like `/api/staff/bookings` which will be shown in Chrome/Firefox Debug tools, on then Network tab.
   * Full backend error logs can also be viewed when ssh'ed into the VM: `docker logs --tail 99 -f engine`

