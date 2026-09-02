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

## Fans

The prototype displays the reported values for:

- part-cooling fan;
- auxiliary fan;
- chamber fan.

Raw fan values are normalized for a small percentage-based display. The prototype does not command fan speeds.

## Speed mode

The currently reported printer speed mode is converted into a concise physical-key view. This is monitoring only in the demonstrated scope.

## AMS

The AMS view represents:

- four material slots;
- reported filament colors;
- empty slots;
- the currently active tray.

The active tray receives a visual highlight so the selected material can be recognized without opening the slicer.

## Chamber light

The light view is the only bidirectional feature in the demonstrated prototype:

- it reads and displays the reported chamber-light state;
- a key press requests light ON or OFF.

No other printer command is claimed by the current demonstration.

