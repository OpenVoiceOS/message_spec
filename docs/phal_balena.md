# WIFI Balena

provides a hotspot for wifi setup via balena

## Listens To

| Message Type                                        | Message Data               | Description                                                    | Emitted Response Type                        | Handled By                       |
|-----------------------------------------------------|----------------------------|----------------------------------------------------------------|----------------------------------------------|----------------------------------|
| `ovos.phal.wifi.plugin.stop.setup.event`            |                            | Stops the Balena WiFi setup process.                           | `ovos.phal.wifi.plugin.remove.active.client` | handle_stop_setup                |
| `ovos.phal.wifi.plugin.client.registered`           | "client": str<br>"id": str | Triggered when a client is registered with the WiFi plugin.    | `ovos.phal.wifi.plugin.activate.{client_id}` | handle_registered                |
| `ovos.phal.wifi.plugin.client.deregistered`         |                            | Triggered when a client is deregistered from the WiFi plugin.  |                                              | handle_deregistered              |
| `ovos.phal.wifi.plugin.client.registration.failure` | "error": str               | Triggered when client registration with the WiFi plugin fails. | `ovos.phal.wifi.plugin.remove.active.client` | handle_registration_failure      |
| `ovos.phal.wifi.plugin.alive`                       |                            | Sent to keep the client alive with the WiFi plugin.            |                                              | register_client                  |
| `ovos.phal.wifi.plugin.activate.{self.client_id}`   |                            | Activates Balena as the wifi setup provider                    |                                              | handle_activate_client_request   |
| `ovos.phal.wifi.plugin.deactivate.{self.client_id}` |                            | Deactivates Balena as the wifi setup provider                  |                                              | handle_deactivate_client_request |

## Emits

| Message Type                                 | Message Data                                                                                                                                    | Description                                                                | Trigger Message Type                              | Handled By            |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|---------------------------------------------------|-----------------------|
| `ovos.phal.wifi.plugin.register.client`      | "client": "ovos-PHAL-plugin-balena-wifi"<br>"type": "Remote"<br>"display_text": "On Mobile Setup"<br>"has_gui": True<br>"requires_input": False | Registers a client with the WiFi plugin.                                   | `ovos.phal.wifi.plugin.alive`                     | register_client       |
| `ovos.phal.wifi.plugin.remove.active.client` | "client": "ovos-PHAL-plugin-balena-wifi"                                                                                                        | Requests the removal of the active client registered with the WiFi plugin. |                                                   | request_deactivate    |
| `ovos.wifi.setup.completed`                  |                                                                                                                                                 | Indicates that WiFi setup is completed successfully.                       | `ovos.phal.wifi.plugin.activate.{self.client_id}` | report_setup_complete |
| `ovos.phal.wifi.plugin.user.activated`       |                                                                                                                                                 | Restart WiFi setup on failure.                                             |                                                   | handle_stop_setup     |

