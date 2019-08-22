# Table of contents

* [What is ACAEngine](README.md)
* [Key Concepts](key-concepts/README.md)
  * [Drivers](key-concepts/drivers.md)
  * [Modules](key-concepts/modules.md)
  * [Systems](key-concepts/systems.md)
  * [Zones](key-concepts/zones.md)
  * [Settings](key-concepts/settings.md)
  * [Interfaces](key-concepts/interfaces.md)
  * [Triggers](key-concepts/triggers.md)
* [Backoffice](backoffice/README.md)
  * [Managing Systems](backoffice/systems.md)
  * [Managing Devices](backoffice/devices.md)
  * [Managing Drivers](backoffice/drivers.md)
  * [Zones](backoffice/zones.md)
  * [Triggers](backoffice/triggers.md)
  * [Metrics](backoffice/metrics.md)
  * [Users](backoffice/users.md)
  * [Debugging Systems/Devices](backoffice/debugging.md)

## Deployment

* [System Architecture](deployment/architecture.md)
* [SSL Certificates](deployment/signed-ssl.md)  
* [Load Balancer Config](deployment/load-balancer.md)  
* [Single Sign-On](deployment/sso/README.md)  
  * [SAML2 with Azure AD](deployment/sso/saml2-azure.md)
  * [SAML2 with ADFS](deployment/sso/saml2-adfs.md)
  * [SAML2 with GSuite](deployment/sso/saml2-gsuite.md)
  * [OAuth2](deployment/sso/oauth2.md)
* [Engine Web Apps](deployment/frontend/README.md)  

## Integrations

* [Directory Services](integrations/directory/README.md)
  * [Microsoft Office365](integrations/directory/office365.md)
* [IoT](integrations/iot.md)
  * [Device Drivers](integrations/device-drivers.md)
* [Location Services](integrations/location/README.md)
  * [Locating Users on a Network](integrations/location/locating-users-on-a-network.md)
  * [SVG Map Creation](integrations/location/svg-map-creation.md)
  * [Cisco CMX](integrations/location/cisco-cmx.md)
  * [Cisco Meraki RTLS](integrations/location/cisco-meraki.md)
  * [Desk Sensors](integrations/location/desk-sensors.md)
* [Email Notifications](integrations/email-notifications.md)

## Administration
* [Domains](administration/domain.md)
  * [Applications](administration/applications.md)
* [Systems](administration/systems/README.md)
  * [Adding a bookable room](administration/systems/add-room.md)
* [User Roles](administration/user-roles.md)

## Developer Guide

* [Development Environment](developer-guide/getting-started.md)
* [Building Drivers](developer-guide/drivers/README.md)
  * [Discovery and Metadata](developer-guide/drivers/metadata.md)
  * [State](developer-guide/drivers/state.md)
  * [Scheduling Actions](developer-guide/drivers/scheduling.md)
  * [Device Drivers](developer-guide/drivers/device.md)
  * [SSH Drivers](developer-guide/drivers/ssh.md)
  * [Service Drivers](developer-guide/drivers/service.md)
  * [Logic Drivers](developer-guide/drivers/logic.md)
  * [Testing and Debugging](developer-guide/drivers/testing.md)
  * [Response Tokenisation](developer-guide/drivers/response-tokenisation.md)
  * [Logging](developer-guide/drivers/logging.md)
  * [Security](developer-guide/drivers/security.md)
  * [Utilities and Helpers](developer-guide/drivers/utilities-and-helpers.md)
* [User Interfaces](developer-guide/user-interfaces/README.md)
  * [Composer](developer-guide/user-interfaces/composer.md)
  * [Virtual Systems](developer-guide/user-interfaces/virtual-systems.md)
  * [Widgets](developer-guide/user-interfaces/widgets.md)

## API

* [Authentication](api/auth.md)
* [Control](api/control/README.md)
  * [Systems](api/control/systems/README.md)
    * [Module Interaction](api/control/systems/actions.md)
* [Realtime API](api/ws/README.md)
  * [Commands](api/ws/commands/README.md)
    * [bind](api/ws/commands/bind.md)
    * [unbind](api/ws/commands/unbind.md)
    * [exec](api/ws/commands/exec.md)
    * [debug](api/ws/commands/debug.md)
    * [ignore](api/ws/commands/ignore.md)
  * [Heartbeat](api/ws/heartbeat.md)
  * [Errors](api/ws/errors.md)

## Support

* [Service Desk](https://support.acaprojects.com)
* [Tech Chat](support/chat.md)

