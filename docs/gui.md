# ovos-gui

- [Homescreen Manager](#homescreen-manager)
- [Extensions Manager](#extensions-manager)
- [Namespace Manager](#namespace-manager)

## Homescreen Manager

### Listens To

| Message Type                        | Message Data               | Description                                   | Response Type(s)                         |
|-------------------------------------|----------------------------|-----------------------------------------------|------------------------------------------|
| `homescreen.manager.add`            | "id": str<br> "class": str | Add a homescreen to the manager.              |                                          |
| `homescreen.manager.remove`         | "id": str                  | Remove a homescreen from the manager.         |                                          |
| `homescreen.manager.list`           |                            | Request a list of loaded homescreens.         | `homescreen.manager.list.response`       |
| `homescreen.manager.get_active`     |                            | Request the active homescreen.                | `homescreen.manager.get_active.response` |
| `homescreen.manager.set_active`     | "id": str                  | Change the configured homescreen.             |                                          |
| `homescreen.manager.disable_active` |                            | Disable the active homescreen.                |                                          |
| `homescreen.manager.show_active`    |                            | Show the active homescreen.                   |                                          |
| `mycroft.ready`                     |                            | Signal that OVOS is ready.                 | `homescreen.manager.show_active`         |
| `mycroft.mark2.register_idle`       |                            | DEPRECATED: Register an old-style homescreen. |                                          |

### Emits

| Message Type                             | Message Data             | Description                                              | In Response to                  |
|------------------------------------------|--------------------------|----------------------------------------------------------|---------------------------------|
| `homescreen.manager.reload.list`         |                          | Emit a request for homescreens to register.              |                                 |
| `homescreen.manager.activate.display`    | "homescreen_id": str     | Activate and display a homescreen.                       |                                 |
| `{active_homescreen_id}.idle`            |                          | DEPRECATED: Activate an old-style homescreen.            |                                 |
| `mycroft.mark2.collect_idle`             |                          | DEPRECATED: Trigger collection of older resting screens. |                                 |
| `homescreen.manager.get_active.response` | "homescreen": str        | report the currently active homescreen                   | `homescreen.manager.get_active` |
| `homescreen.manager.show_active`         |                          | Show the active homescreen.                              | `mycroft.ready`                 |
| `homescreen.manager.list.response`       | "homescreens": List[str] | report list of loaded homescreens.                       | `homescreen.manager.list`       |

## Extensions Manager

### Listens To

| Message Type            | Message Data | Description                | Response Type(s)        |
|-------------------------|--------------|----------------------------|-------------------------|
| `mycroft.gui.connected` |              | A GUI client app connected | `mycroft.gui.available` |

### Emits

| Message Type                  | Message Data      | Description                                          | In Response to                                   |
|-------------------------------|-------------------|------------------------------------------------------|--------------------------------------------------|
| `extension.manager.activated` | "id": str         | Reports the active GUI extension                     | during initial loading                           |
| `mycroft.gui.available`       | "permanent": bool | signal GUI available to trigger resource file upload | during initial loading / `mycroft.gui.connected` |

## Namespace Manager

### Listens To

| Message Type                | Message Data                       | Description                                                                            | Response Type(s)                 | Handled by                      |
|-----------------------------|------------------------------------|----------------------------------------------------------------------------------------|----------------------------------|---------------------------------|
| `gui.clear.namespace`       |                                    | remove a namespace.                                                                    |                                  | self.handle_clear_namespace     |
| `gui.event.send`            |                                    | send a message to the GUI message bus.                                                 |                                  | self.handle_send_event          |
| `gui.page.delete`           |                                    | remove one or more pages from a namespace.                                             |                                  | self.handle_delete_page         |
| `gui.page.show`             |                                    | show one or more pages on the screen.                                                  |                                  | self.handle_show_page           |
| `gui.page.upload`           |                                    | makes pages accessible via HTTP server, may be mounted to a volume in container setups | `homescreen.manager.show_active` | self.handle_receive_gui_pages   |
| `gui.volunteer_page_upload` |                                    | skill or plugin advertising that it has GUI pages available to upload                  |                                  | self.handle_gui_pages_available |
| `gui.status.request`        |                                    | check if there are connected GUI client apps                                           |                                  | self.handle_status_request      |
| `gui.value.set`             |                                    | set the value of namespace data attributes.                                            |                                  | self.handle_set_value           |
| `gui.page_interaction`      | "skill_id": str                    | a page has been interacted with.                                                       |                                  | self.handle_page_interaction    |
| `gui.page_gained_focus`     | "skill_id": str                    | GUI app indicating a page has gained focus                                             |                                  | self.handle_page_gained_focus   |
| `mycroft.skills.trained`    |                                    | Once all skills loaded, trigger a page upload                                          |                                  | self.handle_ready               |
| `mycroft.gui.connected`     | "gui_id": str<br> "framework": str | DEPRECATED: old gui clients connected to wrong bus                                     |                                  | self.handle_client_connected    |

### Emits

| Message Type                     | Message Data                  | Description                                                          | In Response to                                         |
|----------------------------------|-------------------------------|----------------------------------------------------------------------|--------------------------------------------------------|
| `homescreen.manager.show_active` |                               | Configured home screen skill just uploaded pages, show it            | `gui.page.upload`                                      |
| `gui.request_page_upload`        |                               | request pages for each connected GUI framework.                      | `gui.volunteer_page_upload`  / `mycroft.gui.connected` |
| `gui.status.request.response`    | "connected": bool             | report if any GUI app is connected                                   | `gui.status.request`                                   |
| `gui.namespace.displayed`        |                               | Message to notify core of changes.                                   | self._emit_namespace_displayed_event                   |
| `mycroft.gui.port`               | "port": int<br> "gui_id": str | DEPRECATED: tell old gui clients what port the real gui websocket is | `mycroft.gui.connected`                                |


