
# Persona

| **Message Type**            | **Msg Data**                                                                                       | **Description**                                                            | **Response Type**           |
|-----------------------------|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|-----------------------------|
| `ovos.persona.register`     | - `name`: The name of the persona to register.<br>- `persona`: The persona data.                   | Registers a new persona with the given name.                               |                             |
| `ovos.persona.deregister`   | - `name`: The name of the persona to deregister.                                                   | Deregisters an existing persona with the given name.                       |                             |
| `ovos.persona.enable`       | - `name`: The name of the persona to enable.                                                       | Activates the specified persona for use.                                   |                             |
| `ovos.persona.disable`      |                                                                                                    | Deactivates the currently active persona.                                  |                             |
| `ovos.persona.ask`          | - `utterance`: The user's input utterance.                                                         | Sends a user's input utterance to the active persona for a response.       | `ovos.persona.ask.response` |
| `ovos.persona.ask.response` | - `utterance`: The response utterance from the persona.<br>- `lang`: The language of the response. | Contains the response from the active persona to a user's input utterance. |                             |

