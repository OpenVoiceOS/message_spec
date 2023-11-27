# PHAL Home Assistant

NOTE: this plugin is a placeholder, it will be deprecated / refactored once the CommonIOT framework is developed

# Listens to

| Message Type                                                   | Message Data                                                      | Description                                                      | Emitted Response Type                                                              | Handled by                           |
| -------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------ |
| `ovos.phal.plugin.homeassistant.get.devices`                   |                                                                   | Requests the list of devices from Home Assistant.                | `ovos.phal.plugin.homeassistant.get.devices.response`                              | handle_get_devices                   |
| `ovos.phal.plugin.homeassistant.get.device`                    | 'device_id': str                                                  | Requests information about a specific device.                    | `ovos.phal.plugin.homeassistant.get.device.response`                               | handle_get_device                    |
| `ovos.phal.plugin.homeassistant.device.turn_on`                | 'device_id': str                                                  | Sends a command to turn on a specific device.                    | `ovos.phal.plugin.homeassistant.device.turn_on.response`                           | handle_turn_on                       |
| `ovos.phal.plugin.homeassistant.device.turn_off`               | 'device_id': str                                                  | Sends a command to turn off a specific device.                   | `ovos.phal.plugin.homeassistant.device.turn_off.response`                          | handle_turn_off                      |
| `ovos.phal.plugin.homeassistant.get.device.display.model`      | 'device_id': str                                                  | Requests the display model of a specific device.                 | `ovos.phal.plugin.homeassistant.get.device.display.model.response`                 | handle_get_device_display_model      |
| `ovos.phal.plugin.homeassistant.get.device.display.list.model` |                                                                   | Requests a list of display models for all devices.               | `ovos.phal.plugin.homeassistant.get.device.display.list.model.response`            | handle_get_device_display_list_model |
| `ovos.phal.plugin.homeassistant.call.supported.function`       | 'device_id': str<br>'function_name': str<br>'function_args': dict | Calls a supported function on a device.                          | `ovos.phal.plugin.homeassistant.call.supported.function.response`                  | handle_call_supported_function       |
| `ovos.phal.plugin.homeassistant.start.oauth.flow`              | 'instance': str                                                   | Initiates the OAuth flow for a specific Home Assistant instance. | `oauth.get.app.host.info`<br>`oauth.generate.qr.request`<br>`oauth.token.response` | handle_start_oauth_flow              |
| `ovos.phal.plugin.homeassistant.assist.intent`                 | 'command': str                                                    | Passes an assist message to Home Assistant's Assist API.         | `ovos.phal.plugin.homeassistant.assist.intent.response`                            | handle_assist_message                |
| `ovos.phal.plugin.homeassistant.get.light.brightness`          | 'device_id': str                                                  | Requests the brightness level of a light device.                 | `ovos.phal.plugin.homeassistant.get.light.brightness.response`                     | handle_get_light_brightness          |
| `ovos.phal.plugin.homeassistant.set.light.brightness`          | 'device_id': str<br>'brightness': int                             | Sets the brightness level of a light device.                     | `ovos.phal.plugin.homeassistant.set.light.brightness.response`                     | handle_set_light_brightness          |
| `ovos.phal.plugin.homeassistant.increase.light.brightness`     | 'device_id': str                                                  | Increases the brightness of a light device.                      | `ovos.phal.plugin.homeassistant.increase.light.brightness.response`                | handle_increase_light_brightness     |
| `ovos.phal.plugin.homeassistant.decrease.light.brightness`     | 'device_id': str                                                  | Decreases the brightness of a light device.                      | `ovos.phal.plugin.homeassistant.decrease.light.brightness.response`                | handle_decrease_light_brightness     |
| `ovos.phal.plugin.homeassistant.get.light.color`               | 'device_id': str                                                  | Requests the color of a light device.                            | `ovos.phal.plugin.homeassistant.get.light.color.response`                          | handle_get_light_color               |
| `ovos.phal.plugin.homeassistant.set.light.color`               | 'device_id': str<br>'color': str                                  | Sets the color of a light device.                                | `ovos.phal.plugin.homeassistant.set.light.color.response`                          | handle_set_light_color               |
| `ovos.phal.plugin.homeassistant.check_connected`               | 'connected': bool                                                 | Is the PHAL plugin is currently connected to Home Assistant?     | `ovos.phal.plugin.homeasssistant.check_connected.response`                         | handle_check_connected               |
| `ovos.phal.plugin.homeassistant.integration.query_media`       | 'phrase': str                                                     | Queries the media player for the requested media.                | `ovos.phal.plugin.homeassistant.integration.query_media.result`                    | handle_query_media                   |
| `ovos-PHAL-plugin-homeassistant.home`                          |                                                                   | Handles the show dashboard message.                              | N/A                                                                                | handle_show_dashboard                |
| `ovos-PHAL-plugin-homeassistant.close`                         |                                                                   | Closes the Home Assistant dashboard in the GUI.                  | N/A                                                                                | handle_close_dashboard               |
| `ovos.phal.plugin.homeassistant.show.device.dashboard`         | 'device_type': str                                                | Shows the dashboard for a specific device.                       | `ovos.phal.plugin.homeassistant.change.dashboard` (GUI bus)                        | handle_show_device_dashboard         |
| `ovos.phal.plugin.homeassistant.show.area.dashboard`           | 'area': str                                                       | Shows the dashboard for a specific area.                         | `ovos.phal.plugin.homeassistant.change.dashboard` (GUI bus)                        | handle_show_area_dashboard           |
| `ovos.phal.plugin.homeassistant.update.device.dashboard`       | 'device_type': str                                                | Updates the dashboard for a specific device.                     | `ovos.phal.plugin.homeassistant.update.device.dashboard`                           | handle_update_device_dashboard       |
| `ovos.phal.plugin.homeassistant.update.area.dashboard`         | 'area_type': str                                                  | Updates the dashboard for a specific area.                       | N/A                                                                                | handle_update_area_dashboard         |
| `ovos.phal.plugin.homeassistant.set.group.display.settings`    | 'use_group_display': bool                                         | Sets the group display settings.                                 | N/A                                                                                | handle_set_group_display_settings    |
| `ovos.phal.plugin.homeassistant.setup.instance`                | 'url': str<br>'api_key': str<br>'assist_only': bool               | Sets up a new Home Assistant instance.                           | `ovos-PHAL-plugin-homeassistant.home`                                              | setup_configuration                  |
| `configuration.updated`                                        | See `ovos.phal.plugin.homeassistant.setup.instance`               | Responds to changes to configuration by re-initializing HA       | See `ovos.phal.plugin.homeassistant.setup.instance`                                | init_configuration                   |
| `configuration.patch`                                          | See `ovos.phal.plugin.homeassistant.setup.instance`               | Responds to changes to configuration by re-initializing HA       | See `ovos.phal.plugin.homeassistant.setup.instance`                                | init_configuration                   |

# Emits

Emits all of the messages that it listens to, plus the following:

| Message Type                                    | Message Data                     | Description                                                             | Trigger Message Type                                  | Handled by                   |
| ----------------------------------------------- | -------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------- | ---------------------------- |
| `ovos.phal.plugin.homeassistant.ready`          |                                  | Signals that the Home Assistant plugin is ready.                        | `ovos.phal.plugin.homeassistant.setup.instance`       | init_configuration           |
| `ovos.phal.plugin.homeassistant.device.updated` | 'device_id': str                 | Signals that a device has been updated, requesting a new display model. | `ovos.phal.plugin.homeassistant.device.state.updated` | device_updated               |
| `oauth.get.app.host.info`                       |                                  | Requests host information for OAuth registration.                       | `oauth.get.app.host.info.response`                    | request_host_info_from_oauth |
| `oauth.generate.qr.request`                     | 'app_id': str<br>'skill_id': str | Requests QR code for OAuth registration.                                | `oauth.generate.qr.response`                          | start_oauth_flow             |
| `oauth.token.response.munged_id`                | 'access_token': str              | Receives the OAuth token response.                                      |                                                       | handle_token_oauth_response  |