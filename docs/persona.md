# ovos-persona

## Persona

NOTE: Persona is under development and did not yet have a stable release, messages below might change at any time
without warning

### Listens to

| Message Type              | Message Data                  | Description                                                          | Emits response              | handled by |
|---------------------------|-------------------------------|----------------------------------------------------------------------|-----------------------------|------------|
| `ovos.persona.register`   | "name": str<br>"persona":dict | Registers a new persona with the given name.                         |                             |            |
| `ovos.persona.deregister` | "name": str                   | Deregisters an existing persona with the given name.                 |                             |            |
| `ovos.persona.enable`     | "name": str                   | Activates the specified persona for use.                             |                             |            |
| `ovos.persona.disable`    |                               | Deactivates the currently active persona.                            |                             |            |
| `ovos.persona.ask`        | "utterance": str              | Sends a user's input utterance to the active persona for a response. | `ovos.persona.ask.response` |            |

### Emits

| Message Type                | Message Data                    | Description                                                                | In Response to / sent by |
|-----------------------------|---------------------------------|----------------------------------------------------------------------------|--------------------------|
| `ovos.persona.ask.response` | "utterance": str<br>"lang": str | Contains the response from the active persona to a user's input utterance. |                          |

"