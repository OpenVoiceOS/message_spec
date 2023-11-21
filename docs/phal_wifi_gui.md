# WIFI GUI setup

provides on device QML GUI for wifi setup

## Listens To

| Message Type                                          | Message Data               | Description                                                     | Emitted Response Type | Handled By                            |
|-------------------------------------------------------|----------------------------|-----------------------------------------------------------------|-----------------------|---------------------------------------|
| `ovos.phal.wifi.plugin.stop.setup.event`              |                            | Handles the stop setup event for the WIFI plugin                |                       | handle_stop_setup                     |
| `ovos.phal.wifi.plugin.client.registered`             | "client": str<br>"id": str | Handles the registration of a client with the WIFI plugin       |                       | handle_registered                     |
| `ovos.phal.wifi.plugin.client.deregistered`           |                            | Handles the deregistration of a client with the WIFI plugin     |                       | handle_deregistered                   |
| `ovos.phal.wifi.plugin.client.registration.failure`   | "error": str               | Handles the failure of client registration with the WIFI plugin |                       | handle_registration_failure           |
| `ovos.phal.wifi.plugin.alive`                         |                            | Handles the alive event from the WIFI plugin                    |                       | register_client                       |
| `ovos.phal.nm.connection.successful`                  |                            | Handles the successful connection event from the NM plugin      |                       | display_success                       |
| `ovos.phal.nm.connection.failure`                     | "errorCode": str           | Handles the failure connection event from the NM plugin         |                       | display_failure                       |
| `ovos.phal.gui.network.client.back`                   |                            | Handles the back event in the GUI network client                |                       | display_path_exit                     |
| `ovos.phal.gui.display.connected.network.settings`    | "connection_details": dict | Handles the display of connected network settings in the GUI    |                       | display_connected_network_settings    |
| `ovos.phal.gui.display.disconnected.network.settings` | "connection_details": dict | Handles the display of disconnected network settings in the GUI |                       | display_disconnected_network_settings |
| `ovos.phal.gui.network.client.internal.back`          |                            | Handles the internal back event in the GUI network client       |                       | display_internal_back                 |
| `system.display.homescreen`                           |                            | Forcefully abort wifi setup GUI                                 |                       | clean_shutdown                        |
| `mycroft.device.settings`                             |                            | Forcefully abort wifi setup GUI                                 |                       | clean_shutdown                        |

## Emits

| Message Type                                 | Message Data                                                                                                                                            | Description                                                | Emitted By         |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|--------------------|
| `ovos.phal.wifi.plugin.register.client`      | "client": "ovos-PHAL-plugin-gui-network-client"<br>"type": "onDevice"<br>"display_text": "On Device Setup"<br>"has_gui": True<br>"requires_input": True | Registers the client with the WIFI plugin                  | register_client    |
| `ovos.phal.wifi.plugin.remove.active.client` | "client": "ovos-PHAL-plugin-gui-network-client"                                                                                                         | Requests removal of the active client from the WIFI plugin | request_deactivate |
| `ovos.phal.wifi.plugin.user.activated`       |                                                                                                                                                         | Restart WiFi setup on failure.                             | display_path_exit  |
| `ovos.wifi.setup.completed`                  |                                                                                                                                                         | Indicates that WiFi setup is completed successfully.       | display_success    |

