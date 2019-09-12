# Locating Users on a Network

## Overview

Using existing infrastructure in an organisation, there is typically enough data available to accurately locate staff. Wireless networks provide a rough indication of location and cabled infrastructure accurately shows who is sitting at individual desk locations.

This can also be augmented with sensors, as required, however sensors can only be used to indicate desk usage - falling back to wifi for staff location.

![](https://docs.google.com/a/acaprojects.com/drawings/d/s6_6XidWyamd0Zk0Uf1gAcQ/image?w=642&h=555&rev=1&ac=1&parent=14XIJbnvJBg23Qc_oc3JN5Ub0geETTSmTWr8Sd8YryLM)

### The Lookup Process

1. Lookup the username or email address of the person in question \(staff search\)
2. Grab the device mappings for that user \(as per the diagram above\)
3. Check if any of those devices are plugged in to a switch port \(or have a desk reserved\)
4. Fallback to wireless lookup of username, email or wireless MAC address if no desk is found

## Desk Locating Requirements

* Switch IP addresses
* SNMP or SSH service enabled on the switch \(SSH preferred as it is easier to troubleshoot and secure\)
* A list of switch ports to desk mappings
* A method for pairing staff to their devices

Most switches expose an SNMP service for tracking details of port usage and the devices connected to each port.

This is a standard common to most network hardware manufacturers and defined by the following standard [https://tools.ietf.org/html/rfc4293](https://tools.ietf.org/html/rfc4293)

CISCO switches support SSH and ACAEngine supports SSHv2 for secure data transfer [http://www.cisco.com/c/en/us/support/docs/security-vpn/secure-shell-ssh/4145-ssh.html](http://www.cisco.com/c/en/us/support/docs/security-vpn/secure-shell-ssh/4145-ssh.html)

## Laptop Docking Stations

Desk locating relies on device MAC addresses to identify staff as they move around a building.

As docking stations often sit between the laptop and the switch, we need to ensure that the MAC address exposed by the docking station is unique to each staff member.

All commercial docking solutions offer a method for passing through a unique MAC, if they don’t already do this by default. Two of the more common docking solutions are HP \(BIOS or EFI configuration\) and [Displaylink](http://www.displaylink.com/products/universal-docking-stations) USB docks \(Dell, Lenovo, Fujitsu, Targus, Kensington, HP and Toshiba among others\).

Displaylink provide a Powershell [script](https://drive.google.com/a/room.tools/file/d/1ie_cEe0tP4tmYvhw1vh3YXO45XSFIA3Y/view?usp=sharing) to automate the configuration which can be deployed via SCCM [https://support.displaylink.com/knowledgebase/articles/613455-how-to-configure-displaylink-ethernet\#macclone](https://support.displaylink.com/knowledgebase/articles/613455-how-to-configure-displaylink-ethernet#macclone)

This [alternative script](https://drive.google.com/a/room.tools/file/d/12VqNiXpX_WUoKtrnW-w06mG-dTkAPLbw/view?usp=sharing) provides detailed logging that can be useful when deploying.

## User Device Discovery

We automate the mapping of laptops and phones to staff.

This is a two-step process.

1. Firstly, we need to discover the IP addresses of the devices in use by a user.
2. Once we have the IP address, we need to find the associated MAC addresses.

This maintains a mapping of MAC addresses to user accounts, which can be used in conjunction with port usage to determine the location of users.

## User Account to IP Address Mapping

There are multiple ways to get this information, and these can be used simultaneously.

* Users connecting to the staff application
* Users logging on to their machines triggering an event on the Windows domain controller
* Users connecting to a file share or print server
* Custom tray application tracking the logged in user, any IP address changes, and associated MAC addresses

## Windows Domain Controller

The Windows domain controller is used to authenticate users as they log onto a device. This would typically a laptop, desktop computer or thin client.

By auditing credential validation events [https://technet.microsoft.com/en-us/library/cc787567\(v=ws.10\).aspx](https://technet.microsoft.com/en-us/library/cc787567%28v=ws.10%29.aspx) it is possible to query these logs to inform ACAEngine of the user account and the corresponding IP address associated with the event.

[https://technet.microsoft.com/en-us/library/dd772679%28v=ws.10%29.aspx](https://technet.microsoft.com/en-us/library/dd772679%28v=ws.10%29.aspx)

## File Share or Print Server

Similar to the Windows domain controller method, audit logging can be enabled for file share access events.

[https://technet.microsoft.com/en-us/library/dn311489%28v=ws.11%29.aspx](https://technet.microsoft.com/en-us/library/dn311489%28v=ws.11%29.aspx)

[https://blogs.technet.microsoft.com/mspfe/2013/08/26/auditing-file-access-on-file-servers/](https://blogs.technet.microsoft.com/mspfe/2013/08/26/auditing-file-access-on-file-servers/)

## IP Address to MAC Address Resolution

* ACAEngine will communicate with the switches over UDP port 161 or TCP port 22
* The switches may communicate to ACAEngine over UDP port 162 \(Not required for SSH connections\)

At this point, we have a user account and an IP address. We need to lookup the MAC address associated with the IP address so we can associate the user to the MAC address/device.

## Switch DHCP Snooping Table

We query DHCP snooping tables on level 2 switches as they maintain a list of DHCP allocated IP addresses and the MAC addresses of assigned devices.

DHCP snooping is a [security feature](http://packetpushers.net/five-things-to-know-about-dhcp-snooping/) and enabling it has additional advantages beyond user locating.  
If DHCP snooping is undesirable, DHCP Gleaning can be used instead.

## Example Powershell Scripts

This covers the basics of user discovery using a domain controller. A 3rd party machine can be configured to query server logs remotely - see the detailed scripts for how this is achieved: [https://github.com/acaprojects/ruby-engine/blob/master/docs/capturing\_user\_devices.md](https://github.com/acaprojects/ruby-engine/blob/master/docs/capturing_user_devices.md)

It is possible to use additional events and change scripts as required for security compliance.  
For more details on how this is implemented please see our detailed [configuration guide](https://docs.google.com/document/d/1WJOAMgs8ZppFrIVzlkTWDiV8vgZ_KJf766XSpv9nnzw/edit#heading=h.nocikac03i2d).

