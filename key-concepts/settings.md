# Settings

_Settings_ are simple key, value pairs and are used to associate configuration information or metadata to [zones](zones.md), [systems](systems.md), [drivers](drivers.md) and [devices](devices.md). They define the properties of that system/device and how it should be controlled by the system’s logic or the device’s driver.

Settings defined for zones are inherited by all systems in that zone. Settings defined for drivers are inherited by all devices of that driver. When settings are inherited from a zone/driver they will be aggregated with any settings defined for that system/device. If an inherited setting has the same attribute as one that is defined specifically for that system/device, the latter will override the inherited attribute.

Examples of settings that could be assigned to systems include: available video inputs/outputs and functions, input source names, their corresponding video matrix switcher input, DSP control block IDs, lighting control addresses, etc…

Examples of settings that could be assigned to devices include: MAC addresses, device login credentials, limits, identifiers, flags, etc…

