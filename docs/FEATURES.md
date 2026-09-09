# Feature behaviour

This document describes the behaviour of the current **BambuDeck v1.2.0.0** Marketplace candidate.

## Connection state

BambuDeck exposes four connection-level views:

- **missing** — required printer settings are not available;
- **connecting** — the local connection is being established;
- **ready** — telemetry is being received;
- **disconnected** — the previously available printer cannot currently be reached.

The connection view is deliberately explicit so stale values are not mistaken for live printer data.

## Default profiles and navigation

BambuDeck includes ready-to-use **Home**, **Print** and **AMS** Stream Deck profiles.

The profiles are linked through BambuDeck navigation actions. The custom back action returns from the Print or AMS profile to Home while preserving the plugin's visual language instead of using Stream Deck's default black navigation arrow.

## Printer state

Incoming printer states are normalized into:

- idle;
- printing;
- paused;
- error;
- unknown;
- disconnected.

This normalized state is shared with the relevant keys so the interface stays consistent.

## Print progress

The print progress view presents:

- current percentage;
- estimated time remaining;
- a visual progress indicator;
- a state-dependent label.

It is a telemetry view. It does not start, pause, resume or stop a print.

## Print Preview

The **Print Preview** action displays the image of the plate/model currently being printed when a usable preview is available.

The current implementation:

1. identifies the active print from printer telemetry;
2. connects locally to the printer using read-only FTPS access;
3. downloads the current `.gcode.3mf` archive from a supported printer-side path;
4. extracts the preferred plate preview image from the archive metadata;
5. caches the image for the current print;
6. renders it directly on the Stream Deck key.

If no preview is available, the action falls back to a clear `NO PRINT` state. Failed preview retrieval is retried conservatively rather than repeatedly hammering the printer.

The preview feature is read-only and does not modify the print file or printer state.

## Print job details

Dedicated read-only actions expose additional job telemetry where the printer reports it:

- **Job Name**;
- **Print Layers** — current/total layer information;
- **Print Speed Factor**.

These actions complement the main progress view and do not control the active print.

## Temperatures

Separate views display the reported:

- nozzle temperature;
- nozzle target temperature;
- bed temperature;
- bed target temperature;
- chamber temperature.

Temperature and target values are read from printer reports. BambuDeck does not change temperature targets.

Temperature keys use compact dynamic visual indicators so state changes can be recognized at a glance.

## Fans

BambuDeck displays reported values for:

- part-cooling fan;
- auxiliary fan;
- chamber fan;
- hotend fan.

Raw fan values are normalized for small physical-key displays. BambuDeck does not command fan speeds in v1.2.

## Speed

Two complementary views are available:

- **Speed Mode** — the currently reported printer speed profile;
- **Print Speed Factor** — the reported speed factor value when available.

Both are monitoring-only in this release.

## Printer diagnostics

Additional diagnostic telemetry includes:

- **Wi-Fi Signal**;
- **Printer Error Codes**.

These views report information exposed by the printer and do not replace Bambu Lab's own troubleshooting guidance.

## AMS overview

The AMS Colors view represents:

- four material slots;
- reported filament colors;
- empty slots;
- the currently active tray.

The active tray receives a visual highlight so the selected material can be recognized without opening the slicer.

## AMS Slot

The dedicated **AMS Slot** action can target an AMS/slot selection and expose slot-specific information in a compact key view.

Availability of individual fields depends on what the connected printer, AMS and spool report.

## AMS detail telemetry

BambuDeck v1.2 includes dedicated read-only AMS actions for:

- **AMS Humidity**;
- **AMS Temperature**;
- **AMS Filament Remaining**;
- **AMS Filament Material**;
- **AMS Filament Profile**;
- **AMS Calibration Info**;
- **AMS Drying Info**.

These actions expose available AMS telemetry without sending AMS control commands. Some values may be absent on unsupported AMS hardware or when a spool does not expose the relevant metadata.

## Chamber light

The light view is the only bidirectional printer feature in the current release:

- it reads and displays the reported chamber-light state;
- a key press requests light ON or OFF.

No start, pause, resume, stop, temperature, fan, motion or AMS command is claimed by BambuDeck v1.2.

## Visual behaviour

BambuDeck uses dynamic SVG key rendering for its live interface. Depending on the action, keys can change:

- values;
- labels;
- progress indicators;
- accent bars;
- connection-state visuals;
- AMS colors and active-slot highlights;
- print preview imagery.

The goal is to keep the interface readable at Stream Deck key size while making state changes visible without opening another application.
