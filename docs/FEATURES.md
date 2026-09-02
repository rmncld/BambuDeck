# Feature behaviour

This document separates demonstrated behaviour from future possibilities.

## Connection state

BambuDeck exposes four connection-level views:

- **missing** — required printer settings are not available;
- **connecting** — the local connection is being established;
- **ready** — telemetry is being received;
- **disconnected** — the previously available printer cannot currently be reached.

The connection view is deliberately explicit so stale values are not mistaken for live printer data.

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

The print view presents:

- current percentage;
- estimated time remaining;
- a visual progress indicator;
- a state-dependent label.

It is a telemetry view. It does not start, pause, resume or stop a print.

## Temperatures

Separate views display the reported:

- nozzle temperature;
- bed temperature;
- chamber temperature.

Temperatures are read from printer reports. BambuDeck does not change temperature targets.

Each temperature key includes a dynamic accent bar. Its color changes with the displayed thermal state so a cold, active or higher value can be recognized before reading the number. Final release thresholds will be documented only after they are validated across supported printer models.

## Fans

The prototype displays the reported values for:

- part-cooling fan;
- auxiliary fan;
- chamber fan.

Raw fan values are normalized for a small percentage-based display. The prototype does not command fan speeds.

The fan bar also changes color with the reported output. The real-hardware gallery demonstrates blue at 0%, green at moderate output, orange at higher output and red at maximum output. This is an intensity indicator, not an alarm or safety classification.

## Speed mode

The currently reported printer speed mode is converted into a concise physical-key view. This is monitoring only in the demonstrated scope.

The mode view changes its label, symbol and accent instead of showing every mode with the same static artwork.

## AMS

The AMS view represents:

- four material slots;
- reported filament colors;
- empty slots;
- the currently active tray.

The active tray receives a visual highlight so the selected material can be recognized without opening the slicer.

## Planned AMS detail views

The current compact AMS key is intended to become the entry point to richer monitoring views:

- one detailed view per tray;
- exact reported filament color;
- material and spool information when exposed by the printer;
- empty and unavailable tray states;
- active-tray state;
- AMS humidity level;
- AMS internal temperature;
- navigation across multiple AMS units.

These items are planned integrations. Their final availability depends on the data actually reported by each supported printer, AMS model and filament type. Third-party spools may expose less metadata than recognized spools.

## Planned job detail views

Future read-only job views may include:

- file or job name;
- current and total layer;
- expanded time-remaining information;
- print-stage detail;
- dedicated layouts for larger Stream Deck models.

## Chamber light

The light view is the only bidirectional feature in the demonstrated prototype:

- it reads and displays the reported chamber-light state;
- a key press requests light ON or OFF.

No other printer command is claimed by the current demonstration.
