# PHAL Connectivity Events

## Listens to

| Message Type               | Message Data | Description                                            | Response Type                       | Handled By   |
|----------------------------|--------------|--------------------------------------------------------|-------------------------------------|--------------|
| `ovos.PHAL.internet_check` |              | Requests a check of internet and network connectivity. | `ovos.PHAL.internet_check.response` | handle_check |

## Emits

| Message Type                        | Message Data                                             | Description                                      | Trigger Message Type       |
|-------------------------------------|----------------------------------------------------------|--------------------------------------------------|----------------------------|
| `ovos.PHAL.internet_check.response` | "internet_connected": bool <br> "network_connected":bool | report current network status                    | `ovos.PHAL.internet_check` |
| `mycroft.network.connected`         |                                                          | Emits when network connectivity is established.  |                            |
| `mycroft.internet.connected`        |                                                          | Emits when internet connectivity is established. |                            |
| `mycroft.network.disconnected`      |                                                          | Emits when network connectivity is lost.         |                            |
| `mycroft.internet.disconnected`     |                                                          | Emits when internet connectivity is lost.        |                            |
| `enclosure.notify.no_internet`      |                                                          | Tell other PHAL plugins about lack of internet   |                            |
| `mycroft.internet.state`            | "state": str                                             | Emits the state of internet connectivity.        |                            |
| `mycroft.network.state`             | "state": str                                             | Emits the state of local network connectivity.   |                            |
