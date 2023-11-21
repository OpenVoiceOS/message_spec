# OVOS Shell Companion

Sure, let's generate the markdown tables for the OpenVoiceOS messagebus messages from the provided code.

# Listens to

| Message Type                                            | Message Data                                 | Description                                       | Emitted Response Type | Handled By                          |
|---------------------------------------------------------|----------------------------------------------|---------------------------------------------------|-----------------------|-------------------------------------|
| `mycroft.gui.screen.close`                              |                                              | Clears the namespace of the specified skill.      |                       | `handle_remove_namespace`           |
| `system.display.homescreen`                             |                                              | Handles the event to display the homescreen.      |                       | `handle_system_display_homescreen`  |
| `mycroft.device.settings`                               |                                              | Displays the device settings page.                |                       | `handle_device_settings`            |
| `ovos.phal.configuration.provider.get.response`         | "settingsMetaData": Dict<br>"groupName": str | Displays advanced configuration for a group.      |                       | `display_advanced_config_for_group` |
| `ovos.phal.configuration.provider.list.groups.response` | "groups": List                               | Displays a list of advanced configuration groups. |                       | `display_advanced_config_groups`    |
| `smartspeaker.extension.extend.about`                   | "display_list": List                         | Extends the about page data.                      |                       | `extend_about_page_data_from_event` |

GUI events, sent via the [gui protocol](https://github.com/OpenVoiceOS/ovos-gui/blob/dev/protocol.md) and
appear in the bus with skill_id prepended, i.e. 'ovos_gui_plugin_shell_companion.{msg_type}'

In the GUI websocket these events look like this

```javascript
{
    "type": "mycroft.events.triggered",
    "namespace": "ovos_gui_plugin_shell_companion",
    "event_name": MSG_TYPE,
    "data": {}
}
```

| GUI Message Type                                   | Message Data               | Description                                       | Emitted Response Type (in regular websocket)           | Handled By                                   |
|----------------------------------------------------|----------------------------|---------------------------------------------------|--------------------------------------------------------|----------------------------------------------|
| `mycroft.device.settings.homescreen`               |                            | Displays homescreen settings page.                |                                                        | handle_device_homescreen_settings            |
| `mycroft.device.settings.ssh`                      |                            | Displays SSH settings page.                       |                                                        | handle_device_ssh_settings                   |
| `mycroft.device.settings.developer`                |                            | Displays developer settings page.                 |                                                        | handle_device_developer_settings             |
| `mycroft.device.show.idle`                         |                            | Shows the homescreen.                             |                                                        | handle_show_homescreen                       |
| `mycroft.device.settings.customize`                |                            | Displays customize settings page.                 |                                                        | handle_device_customize_settings             |
| `mycroft.device.settings.create.theme`             |                            | Displays create theme settings page.              |                                                        | handle_device_create_theme                   |
| `mycroft.device.settings.about.page`               |                            | Displays about page settings.                     |                                                        | handle_device_about_page                     |
| `mycroft.device.settings.display`                  |                            | Displays display settings page.                   |                                                        | handle_device_display_settings               |
| `mycroft.device.settings.factory`                  |                            | Displays factory settings page.                   |                                                        | handle_device_display_factory                |
| `speaker.extension.display.set.wallpaper.rotation` | "wallpaper_rotation": bool | Handles setting wallpaper rotation configuration. | `speaker.extension.display.wallpaper.rotation.changed` | handle_display_wallpaper_rotation_config_set |
| `speaker.extension.display.set.auto.dim`           | "auto_dim": bool           | Handles setting auto dim configuration.           | `speaker.extension.display.auto.dim.changed`           | handle_display_auto_dim_config_set           |
| `speaker.extension.display.set.auto.nightmode`     | "auto_nightmode": bool     | Handles setting auto night mode configuration.    | `speaker.extension.display.auto.nightmode.changed`     | handle_display_auto_nightmode_config_set     |

# Emits

| Message Type                                           | Message Data  | Description                                                     | Trigger Message Type                                           | Handled By                                   |
|--------------------------------------------------------|---------------|-----------------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------|
| `gui.clear.namespace`                                  | "__from": str | Clears the namespace of the specified skill.                    | `mycroft.gui.screen.close`                                     | handle_remove_namespace                      |
| `speaker.extension.display.wallpaper.rotation.changed` |               | Notifies that the wallpaper rotation configuration has changed. | `{namespace}.speaker.extension.display.set.wallpaper.rotation` | handle_display_wallpaper_rotation_config_set |
| `speaker.extension.display.auto.dim.changed`           |               | Notifies that the auto dim configuration has changed.           | `{namespace}.speaker.extension.display.set.auto.dim`           | handle_display_auto_dim_config_set           |
| `speaker.extension.display.auto.nightmode.changed`     |               | Notifies that the auto night mode configuration has changed.    | `{namespace}.speaker.extension.display.set.auto.nightmode`     | handle_display_auto_nightmode_config_set     |

