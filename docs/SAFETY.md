# Safety and data boundaries

## Local communication

The demonstrated prototype communicates with the printer on the local network. Its purpose is to expose useful printer state on a nearby physical interface.

## Read-mostly scope

Monitoring features do not alter:

- print jobs;
- target temperatures;
- motion;
- fan speeds;
- speed modes;
- AMS loading;
- printer configuration.

The chamber light is the only implemented write action.

## Honest status

A value must not appear live when the printer is disconnected. Connection states and unknown values therefore have dedicated interface states instead of silently retaining the last received telemetry.

## Credentials

Public documentation, screenshots and demonstration media must never expose printer credentials, access codes, local addresses or other connection secrets.

## Future commands

Any additional control would require:

- explicit user intent;
- documented availability and error states;
- confirmation for destructive actions;
- hardware testing;
- a clear fallback when the printer rejects or loses the command.

