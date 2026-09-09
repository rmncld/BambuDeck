<p align="center">
  <img src="./assets/bambudeck-cover.svg" alt="BambuDeck — Bambu Lab monitoring on Stream Deck" width="720">
</p>

<p align="center">
  <strong>A local-first Stream Deck dashboard for Bambu Lab printers and AMS.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.2.0.0-4ADE80?style=for-the-badge" alt="Version 1.2.0.0">
  <img src="https://img.shields.io/badge/Tested-P1S_%2B_AMS-63E6FF?style=for-the-badge" alt="Tested with P1S and AMS">
  <img src="https://img.shields.io/badge/Connection-Local_MQTT_%2B_FTPS-334155?style=for-the-badge" alt="Local MQTT and FTPS">
  <img src="https://img.shields.io/badge/Marketplace-Candidate-8B5CF6?style=for-the-badge" alt="Marketplace candidate">
</p>

## BambuDeck 1.2

BambuDeck turns a Stream Deck into a compact live dashboard for a Bambu Lab printer. Printer state, job progress, temperatures, cooling, Wi-Fi, errors and AMS information are rendered directly on physical keys with dynamic SVG views.

Version **1.2.0.0** introduces dedicated **Home**, **Print** and **AMS** profiles, built-in navigation, a much larger telemetry library and one of BambuDeck's signature features: **Print Preview**.

> **Monitoring-first:** the current release is intentionally read-only for printer operations except for the chamber-light ON/OFF action. It does not start, pause, resume or stop prints and does not change temperatures, fans or motion settings.

## Print Preview — the model on the key

<p align="center">
  <img src="./assets/v12-print-preview.svg" alt="BambuDeck Print Preview displayed on a Stream Deck key" width="735">
</p>

During an active print, BambuDeck can identify the current `.gcode.3mf`, retrieve it from the printer over the local network using **read-only FTPS**, extract the plate preview image from the 3MF archive, cache it, and display the model directly on a Stream Deck key.

The preview is tied to the active job. When there is no usable active print image, the key returns to a clear fallback state rather than keeping stale artwork.

## Three ready-to-use profiles

BambuDeck ships with three default Stream Deck profiles:

| Profile | Purpose |
| --- | --- |
| **Home** | Printer overview and entry point to the detailed views |
| **Print** | Job name, progress, layers, preview, temperatures, cooling and print telemetry |
| **AMS** | AMS overview, colors, slots and detailed AMS telemetry |

The profiles include built-in navigation. The distributed **BambuDeck Back** action uses a custom navigation icon and returns from Print or AMS to the Home profile.

## v1.2 action library

<p align="center">
  <img src="./assets/v12-feature-grid.svg" alt="BambuDeck v1.2 telemetry key artwork" width="800">
</p>

The v1.2 build adds a large set of dedicated read-only actions while keeping the original live dashboard actions:

| Area | Actions / information |
| --- | --- |
| **Printer** | Printer Status, Wi-Fi Signal, Printer Error Codes |
| **Print** | Print Progress, Print Preview, Job Name, Print Layers, Print Speed Factor |
| **Temperature** | Nozzle Temperature, Nozzle Target, Bed Temperature, Bed Target, Chamber Temperature |
| **Cooling** | Part Fan, Auxiliary Fan, Chamber Fan, Hotend Fan |
| **Speed** | Current Speed Mode |
| **AMS overview** | AMS Colors, active tray highlight, AMS Slot |
| **AMS environment** | AMS Humidity, AMS Temperature |
| **AMS filament** | Remaining estimate, Material, Filament Profile |
| **AMS diagnostics** | Calibration metadata, Drying information |
| **Control** | Chamber Light ON/OFF |

Some AMS fields depend on what the connected printer, AMS generation, firmware and spool metadata actually report. Profile temperatures, nominal spool data and remaining estimates are presented as reported metadata/estimates, not as additional physical sensor measurements.

## Local setup — no Bambu Cloud login

<p align="center">
  <img src="./assets/v12-local-setup.svg" alt="BambuDeck local Device Network Access configuration" width="872">
</p>

BambuDeck is configured from the **Printer Status** Property Inspector inside the Stream Deck application. The setup is split into three clear blocks:

- **Device** — printer model and a user-facing printer name;
- **Network** — the printer's local IP address and serial number;
- **Access** — the printer's LAN access code.

BambuDeck **does not ask for a Bambu Cloud account, email or cloud password**. The plugin connects directly to the printer on the local network. Once the required local fields are present, the setup reports a visible **READY** state; incomplete or missing configuration is shown separately.

The same local printer connection is shared by the detailed telemetry actions. Print Preview additionally uses the same local printer address/access information for its read-only FTPS retrieval.

> Public screenshots intentionally hide the real IP address, serial number and access code.

## Real-hardware proof

BambuDeck is tested on a physical **Bambu Lab P1S + AMS**, not only with simulated telemetry.

| Ready | Printing · 29% | Printing · 35% |
| :---: | :---: | :---: |
| <img src="./assets/state-ready.jpg" alt="BambuDeck ready state on a real Stream Deck" width="280"> | <img src="./assets/state-printing-29.jpg" alt="BambuDeck showing print progress and live fan values" width="280"> | <img src="./assets/state-printing-35.jpg" alt="BambuDeck showing print progress and active AMS slot" width="280"> |

### Animated demonstration

<p align="center">
  <img src="./assets/bambudeck-demo-final.gif" alt="BambuDeck animated real-hardware demonstration" width="560">
</p>

The demonstration shows the interface reacting to live printer state, progress, temperatures, fan values, speed mode, AMS colors and the active tray during a real print.

## Dynamic physical-key UI

BambuDeck uses dynamic SVG rendering rather than relying on static labels. Depending on the action and data available, keys can update progress indicators, telemetry values, accent bars, spool colors, active-tray highlighting, connection states and preview artwork.

The current Marketplace build deliberately keeps the **Original** visual style fixed. The internal Core / Action / Theme Engine separation remains in the project architecture for future visual expansion, but user-facing theme selection is not advertised as a v1.2 feature.

## How it works

<p align="center">
  <img src="./assets/architecture.svg" alt="BambuDeck local architecture" width="720">
</p>

1. **Printer Status** stores the local printer configuration.
2. BambuDeck connects to the printer using local **MQTTS** and subscribes to its telemetry reports.
3. Incoming partial reports are normalized into a shared internal printer state.
4. Stream Deck actions render only the data they need as dynamic key images.
5. **Print Preview** can additionally use local read-only **FTPS** to retrieve the current `.gcode.3mf` and extract its plate image.
6. The chamber-light action is the only current printer write command.

The implementation is written in **TypeScript**, targets **Stream Deck SDK 3 / Stream Deck 7.1+**, uses **MQTT v5**, and the packaged plugin declares Windows 10+ and macOS 12+ support.

## Compatibility

The current real-device validation is performed on **Bambu Lab P1S + AMS**.

The v1.2 setup provides model selections for **A1, P1P, P1S and X1C**. BambuDeck is designed around Bambu Lab local telemetry, but the exact values available can differ by printer model, firmware and AMS hardware. Models beyond the tested P1S + AMS should therefore be treated as intended compatibility until validated on real hardware.

## Marketplace status

**BambuDeck v1.2.0.0** is the current Elgato Marketplace candidate build. The package has passed the Elgato CLI validation and packaging workflow and is being prepared for review.

This repository is the public product showcase and technical documentation for BambuDeck. The proprietary plugin source code is not distributed here.

## Documentation

- [Detailed feature behaviour](./docs/FEATURES.md)
- [Technical architecture](./docs/ARCHITECTURE.md)
- [Setup and local authentication](./docs/CONFIGURATION.md)
- [Safety and data boundaries](./docs/SAFETY.md)
- [Development roadmap](./docs/ROADMAP.md)

## Independence

BambuDeck is an independent project. It is not affiliated with, endorsed by or sponsored by Bambu Lab or Elgato. Product and company names belong to their respective owners.
