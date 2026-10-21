<p align="center">
  <img src="./assets/bambudeck-cover.png" alt="BambuDeck — Bambu Lab monitoring on Stream Deck" width="720">
</p>

<p align="center">
  <strong>Live Bambu Lab printer and AMS telemetry directly on Stream Deck.</strong>
</p>

<p align="center">
  <a href="https://marketplace.elgato.com/product/bambudeck-1279275e-0239-488d-b7b3-cca63f8a4c7f">
    <img src="./assets/badges/elgato-marketplace.svg" alt="Get it on Marketplace" height="48">
  </a>
  &nbsp;&nbsp;
  <a href="https://www.elgato.com/stream-deck">
    <img src="./assets/badges/works-with-stream-deck.svg" alt="Works with Stream Deck" height="48">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.3.0-4ADE80?style=for-the-badge" alt="BambuDeck version 1.3.0">
  <img src="https://img.shields.io/badge/Tested-P1S_%2B_AMS-63E6FF?style=for-the-badge" alt="Tested with P1S and AMS">
  <img src="https://img.shields.io/badge/Connection-Local_MQTT_%2B_FTPS-334155?style=for-the-badge" alt="Local MQTT and FTPS">
</p>

## What is BambuDeck?

BambuDeck is an independent Stream Deck integration for Bambu Lab printers. It turns live printer, print-job and AMS information into compact physical-key displays so the most useful information remains visible without keeping Bambu Studio or a mobile app in the foreground.

**Approved and listed on the [Elgato Marketplace](https://marketplace.elgato.com/product/bambudeck-1279275e-0239-488d-b7b3-cca63f8a4c7f).**

**This showcase presents BambuDeck v1.3.0.** The Marketplace page still lists **v1.2.5** (8 October 2026), for **Windows** and **Stream Deck 7.1 or later**, as checked on 21 October 2026. Version 1.3.0 is not yet shown as available there. Install the published plugin through Marketplace.

The **v1.2** feature set introduced dedicated **Home**, **Print** and **AMS** profiles, built-in navigation, a much larger telemetry library and one of BambuDeck's signature features: **Print Preview**.

> **Safety scope:** BambuDeck is monitoring-first. The only printer command currently implemented is chamber-light ON/OFF. Print controls, temperature controls, fan controls and motion commands are not part of this release.

## New in v1.3.0

<p align="center">
  <img src="./assets/v130-new-features.png" alt="BambuDeck 1.3.0 overview: P1S camera preview, updated AMS spool graphics and BambuBuddy animation preview" width="960">
</p>

- **P1S camera:** automatically refreshed local camera images on a Stream Deck key. The P1S connection has been checked on real hardware; other camera models remain experimental.
- **Clearer keys and AMS spools:** aligned value sizes, units and visual accents, plus updated filament spool graphics and active-slot highlighting.
- **Multi-plate Print Preview:** selects the current plate rather than defaulting to the first plate, with improved archive detection and a loading state.
- **BambuBuddy animation preview:** a printer-state mascot with ready, printing, paused, finished, error and offline animations. Software checks are complete; physical Stream Deck rendering and perceived animation smoothness still require user verification.

The image above is a presentation assembled from plugin visuals, a P1S camera image and demo filament colors. It is not a photograph of the complete v1.3.0 layout running on a physical Stream Deck. See [visual provenance and validation scope](./docs/VISUAL-ASSETS.md).

## See BambuDeck in action

<p align="center">
  <img src="./assets/bambudeck-demo-final.gif" alt="Real P1S and AMS telemetry displayed on Stream Deck during a print" width="560">
</p>

Recorded on a **Bambu Lab P1S + AMS**: printer state, print progress, temperatures, fans, speed mode and active filament tray. This real-hardware demonstration documents the established monitoring features; it is not a recording of every change in v1.2.5.

## Print Preview — the model on the key

<p align="center">
  <img src="./assets/v12-print-preview.jpg" alt="BambuDeck Print Preview displayed on a Stream Deck key" width="735">
</p>

The **Print Preview** action can retrieve the active print archive from the printer over the local network using read-only FTPS access, extract the plate thumbnail from the current `.gcode.3mf`, cache it and display the model directly on a Stream Deck key.

Instead of seeing only a file name or percentage, the current model is visible beside the live printer telemetry. If no usable preview is available, the key falls back to a clear `NO PRINT` state rather than leaving stale artwork on screen.

## Highlights in v1.2

- Ready-to-use **Home**, **Print** and **AMS** Stream Deck profiles.
- Built-in navigation with a custom BambuDeck back button.
- **Print Preview** showing the current plate/model directly on a Stream Deck key.
- Print job name, layer progress and speed factor.
- Wi-Fi signal and printer error-code monitoring.
- Nozzle and bed **target temperatures** in addition to live temperatures.
- Hotend fan monitoring.
- Expanded AMS telemetry: humidity, temperature, material, remaining filament, profile, calibration and drying information.
- AMS slot view with configurable AMS/slot selection.
- Existing live telemetry retained: printer status, progress, temperatures, fans, speed mode, AMS colors and active tray.

## Ready-to-use profiles

| Profile | Purpose |
| --- | --- |
| **Home** | Main printer overview and entry point |
| **Print** | Print Progress, Print Preview, Job Name, Print Layers, Print Speed Factor |
| **AMS** | AMS colors, slots and detailed AMS information |

Navigation is already configured in the distributed profiles. The custom BambuDeck back action returns from the Print or AMS profile to Home without relying on the default black Stream Deck navigation icon.

## Simple local setup — no Bambu Cloud login

BambuDeck is configured from its **Property Inspector** inside the Stream Deck software. The current setup is divided into **Device**, **Network** and **Access** sections.

<p align="center">
  <img src="./assets/setup-configuration.jpg" alt="BambuDeck setup panel inside Stream Deck" width="650">
</p>

BambuDeck does **not** require the user to sign in to a Bambu Cloud account. The plugin connects directly to the printer over the local network using the printer's local connection details and LAN access code.

The setup panel exposes clear configuration states such as **READY**, while public screenshots and documentation intentionally hide real local addresses, access codes and other authentication values.

The same local printer connection is shared by the detailed telemetry actions. Print Preview additionally uses the same local printer address/access information for its read-only FTPS retrieval.

## Established monitoring feature set

| Area | Action / information | Direction |
| --- | --- | --- |
| Connection | Missing, connecting, ready and disconnected states | Printer → Deck |
| Printer | Printer Status | Printer → Deck |
| Printer | Wi-Fi Signal | Printer → Deck |
| Printer | Printer Error Codes | Printer → Deck |
| Print | Print Progress + estimated remaining time | Printer → Deck |
| Print | Print Preview | Printer → Deck |
| Print | Job Name | Printer → Deck |
| Print | Print Layers | Printer → Deck |
| Print | Print Speed Factor | Printer → Deck |
| Temperature | Nozzle Temperature | Printer → Deck |
| Temperature | Nozzle Target | Printer → Deck |
| Temperature | Bed Temperature | Printer → Deck |
| Temperature | Bed Target | Printer → Deck |
| Temperature | Chamber Temperature | Printer → Deck |
| Cooling | Part Fan Speed | Printer → Deck |
| Cooling | Auxiliary Fan Speed | Printer → Deck |
| Cooling | Chamber Fan Speed | Printer → Deck |
| Cooling | Hotend Fan Speed | Printer → Deck |
| Speed | Current Speed Mode | Printer → Deck |
| AMS | AMS Colors + active tray highlight | Printer → Deck |
| AMS | AMS Slot | Printer → Deck |
| AMS | AMS Humidity | Printer → Deck |
| AMS | AMS Temperature | Printer → Deck |
| AMS | AMS Filament Remaining | Printer → Deck |
| AMS | AMS Filament Material | Printer → Deck |
| AMS | AMS Filament Profile | Printer → Deck |
| AMS | AMS Calibration Info | Printer → Deck |
| AMS | AMS Drying Info | Printer → Deck |
| Control | Chamber Light | Deck ↔ Printer |

## Working proof

BambuDeck is tested on real hardware, not only with simulated telemetry.

| Ready | Printing · 29% | Printing · 35% |
| :---: | :---: | :---: |
| <img src="./assets/state-ready.jpg" alt="BambuDeck ready state on a real Stream Deck" width="280"> | <img src="./assets/state-printing-29.jpg" alt="BambuDeck showing print progress and live fan values" width="280"> | <img src="./assets/state-printing-35.jpg" alt="BambuDeck showing print progress and active AMS slot" width="280"> |

## Dynamic visual language

BambuDeck uses dynamic SVG rendering rather than static text-only keys:

- print progress updates both percentage and progress indicator;
- temperature and fan keys use value-dependent accent bars;
- speed mode changes its label, symbol and accent;
- AMS colors reproduce reported spool colors;
- the active AMS tray receives a visible highlight;
- connection and missing-data states are visually distinct;
- Print Preview renders the active plate image when available.

## How it works

<p align="center">
  <img src="./assets/architecture.svg" alt="BambuDeck local architecture" width="720">
</p>

1. The plugin connects to the printer over the local network.
2. MQTT reports are normalized into one internal printer state.
3. Each Stream Deck action subscribes only to the state it needs.
4. Dynamic SVG views turn live values into readable physical-key interfaces.
5. **Print Preview** can additionally use local read-only **FTPS** to retrieve the current `.gcode.3mf` and extract its plate image.
6. The chamber-light action sends the only currently supported printer command.

The implementation is written in **TypeScript**, **MQTT v5**, and local **FTPS** for print-thumbnail retrieval.

## Compatibility

The current hardware validation is performed on a **Bambu Lab P1S + AMS**.

BambuDeck is designed around telemetry exposed by Bambu Lab printers and is intended to support models such as **A1, P1P, P1S and X1C**, but model-specific values and AMS capabilities can vary. Additional models should be considered compatible only after real-device validation.

## Design principles

- **Glanceable:** useful information must remain readable on a small physical key.
- **Local-first:** printer communication stays on the local network.
- **State-driven:** each key reflects current printer data rather than a static shortcut.
- **Monitoring-first:** write commands are deliberately limited.
- **Hardware-tested:** published behaviour is validated on real equipment.

## Project status

BambuDeck is approved and listed on the **Elgato Marketplace**, where the current listed version is **1.2.5** (checked 21 October 2026).

BambuDeck has received several updates with improvements and new features. The **v1.3.0** presentation above distinguishes real P1S checks from animation previews and experimental camera support. It does not imply that v1.3.0 has been approved or released on Marketplace.

The current release includes dedicated **Home**, **Print** and **AMS** profiles, expanded live telemetry, local MQTT communication, FTPS-based Print Preview and real-hardware validation on a Bambu Lab P1S + AMS.

<p align="center">
  <a href="https://marketplace.elgato.com/product/bambudeck-1279275e-0239-488d-b7b3-cca63f8a4c7f">
    <strong>Get BambuDeck on the Elgato Marketplace</strong>
  </a>
</p>

This repository serves as the public technical showcase and documentation for BambuDeck. It does not publish the proprietary plugin source code.

## Documentation

- [Public visual assets and their scope](./docs/VISUAL-ASSETS.md)

- [Detailed feature behaviour](./docs/FEATURES.md)
- [Technical architecture](./docs/ARCHITECTURE.md)
- [Setup and configuration](./docs/CONFIGURATION.md)
- [Safety and data boundaries](./docs/SAFETY.md)
- [Development roadmap](./docs/ROADMAP.md)

## Independence

BambuDeck is an independent project. It is not affiliated with, endorsed by or sponsored by Bambu Lab or Elgato. Product and company names belong to their respective owners.
