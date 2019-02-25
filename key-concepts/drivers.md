# Drivers

_Drivers_ are Ruby code modules designed specifically to work with ACAEngine and imported into backoffice. A wide selection of open source drivers is available online. There are three types of drivers:

* **Logic Drivers** define how a system should operate. A logic device \(instance of a logic driver associated with a specific system\) will take the settings defined for that system and its devices and will automate the actions defined in the logic driver \(Ruby code\). The logic will also perform any actions that are bound to inputs from a user interface and provide feedback to that interface.
* **Device Drivers** define how objects \(usually physical devices\) that are communicated with using TCP/UDP should be controlled. The driver will define the communication protocol used, the available commands/responses and the processes that should occur upon connection/disconnection/power-up. Devices are instances of device drivers and often represent a single physical device of that type that is being controlled. Logic modules will control Devices in the same System with any parameters defined in Settings.
* **SSH Drivers** are similar to Device Drivers, using SSH \(Secure Shell\) for command transport.
* **Service Drivers** are similar to Device Drivers but use HTTP/S \(REST\) for communication instead of a custom TCP/UDP protocol.

