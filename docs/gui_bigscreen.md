# Plasma Bigscreen GUI Extension

Provides window management for Plasma Bigscreen

## Listens to

| Message Type                    | Message Data                  | Description                                                      | Emitted Response Type     | Handled by              |
|---------------------------------|-------------------------------|------------------------------------------------------------------|---------------------------|-------------------------|
| `mycroft.gui.screen.close`      |                               | Closes the current skill window on Plasma Bigscreen              | `screen.close.idle.event` | close_window_by_event   |
| `mycroft.gui.force.screenclose` | 'skill_id': str               | Forces the closure of a specific skill window on Bigscreen       | `screen.close.idle.event` | close_window_by_force   |
| `gui.page.show`                 | 'page': str<br>'__idle': bool | Tracks the idle timeout / override idle flag for displayed pages |                           | on_gui_page_show        |
| `gui.page_interaction`          | 'skill_id': str               | Tracks the current skill displaying a page                       |                           | on_gui_page_interaction |
| `gui.namespace.removed`         | 'skill_id': str               | Closes the window of the skill                                   | `screen.close.idle.event` | close_current_window    |

## Emits

| Message Type              | Message Data               | Description                                | Trigger Message Type                                                                   | Handled by                                                                                                                           |
|---------------------------|----------------------------|--------------------------------------------|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `screen.close.idle.event` | 'skill_idle_event_id': str | Asks mycroft-gui to close the skill window | `gui.clear.namespace`<br>`mycroft.gui.screen.close`<br>`mycroft.gui.force.screenclose` | [mycroft-gui](https://github.com/OpenVoiceOS/mycroft-gui-qt5/blob/e3e87b22be62e009ff227a86d6e4731e4ad5a5d8/application/main.qml#L68) |
