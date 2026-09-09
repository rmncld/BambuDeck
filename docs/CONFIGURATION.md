# Setup and local authentication

BambuDeck is configured from the **Printer Status** Property Inspector built into the Stream Deck application.

The v1.2 setup is deliberately local-first: BambuDeck does **not** request a Bambu Cloud account, email address or cloud password. The information entered here is used to connect directly to the printer on the local network.

## Device

The setup provides model selections for:

- A1
- P1P
- P1S
- X1C

A custom user-facing printer name can also be entered. This is the name shown by BambuDeck; it is separate from the connection credentials.

## Network

The Network block contains two local connection fields:

- **IP address** — the printer's address on the local network;
- **Serial number** — used for the printer MQTT report/request topic.

The v1.2 Property Inspector help text points the user to the printer's device information for the serial number.

## Access

The Access block contains the printer's **LAN access code**. The v1.2 Property Inspector points the user to the printer WLAN settings for this value.

Internally, the local MQTT connection uses the printer address over MQTTS and authenticates using the LAN access code. No Bambu Cloud credential is collected by BambuDeck.

## READY / incomplete / missing state

The setup validates the presence of the required local fields and displays a visible state:

- **READY** — device, IP address, serial number and access code are present;
- **INCOMPLETE** — only part of the required configuration is present;
- **MISSING CONFIG** — the required setup has not been entered.

This visible state is a configuration-readiness indicator. Live connection state is still determined by communication with the printer.

## Shared connection

The bundled Home profile's **Printer Status** action is the main configuration point. Once the shared BambuDeck Core is connected, the Print and AMS detail actions use the same live printer session rather than requiring the user to enter the printer information on every key.

## Print Preview and FTPS

The Print Preview feature uses the same local printer address and access code when it needs to retrieve the active print archive. The implementation performs **read-only FTPS retrieval** of candidate `.gcode.3mf` files, extracts a `Metadata/plate_*.png` preview from the 3MF/ZIP archive, then caches the resulting image for display on the Stream Deck key.

BambuDeck does not upload or alter the print file as part of this feature.

## Public-media and security rule

Screenshots, documentation examples and bug reports must never expose real connection secrets. Public material should hide or redact:

- printer access codes;
- local IP addresses;
- printer serial numbers when they are not required for the report;
- authentication values;
- other private network information.

The repository screenshots intentionally leave those fields blank.

## Physical layout

Actions can be rearranged by the user in Stream Deck. Empty keys in the demonstrated profiles are intentional spacing/layout choices, not missing data or failed actions.
