# Technical architecture

## Stack

- TypeScript
- Elgato Stream Deck SDK v2
- MQTT v5
- Rollup build pipeline
- Dynamic SVG key rendering

## Data path

1. A local MQTT client connects to the configured printer.
2. Printer reports and initial state messages enter a single adapter.
3. The adapter normalizes raw payloads into a stable printer-state model.
4. State listeners notify Stream Deck actions when their relevant values change.
5. Actions render updated SVG views on their physical keys.

## State model

The internal state tracks the values needed by the current views:

- connection and printer status;
- progress and remaining time;
- nozzle, bed and chamber temperatures;
- part, auxiliary and chamber fan values;
- speed mode;
- chamber-light state;
- AMS slots and active tray.

## Command boundary

The architecture deliberately separates telemetry updates from commands.

- Telemetry flows from the printer into the state model.
- The chamber-light action is the only current path that sends a command back.
- Additional command paths are not part of the demonstrated scope.

## Rendering

Key interfaces are rendered as SVG rather than static bitmaps. This makes it possible to update numbers, labels, colors, rings and progress indicators without maintaining a large collection of pre-rendered images.

