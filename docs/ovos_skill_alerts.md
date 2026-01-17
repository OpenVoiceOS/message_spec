# ovos-skill-alerts
## Alerts

### Listens To

| Message Type                                  | Message Data         | Description                                                         | Response Type(s)                                       | handled by |
|-----------------------------------------------|----------------------|---------------------------------------------------------------------|--------------------------------------------------------|------------|
| `ovos.alerts.get_alerts`                      | 'alert_type': str (def: 'all')<br>'disposition': str (def: 'pending') | Retrieve saved alerts of a given type and/or state<br>elligible: [type/state](https://github.com/OpenVoiceOS/ovos-skill-alerts/blob/b3e35df82aef67803636fec8a632a94970e9ffbd/util/__init__.py#L33)  | `ovos.alerts.get_alerts.response` | self._event_get_alerts |
| `ovos.alerts.cancel_alarm` | 'alarmIndex': str<br>(optional) | cancel specific/all running alarm(s)  | | self._event_cancel_alarm |
| `ovos.alerts.snooze_alarm` | 'alarmIndex': str<br>(optional) | snooze specific/all running alarms  | | self._event_snooze_alarm |
| `ovos.gui.show.active.timers` | | Display pending timers per GUI | | self._on_display_gui |
| `ovos.gui.show.active.alarms` | | Display pending alarms per GUI | | self._on_display_gui |

Notification system
| Message Type                                  | Message Data         | Description                                                         | Response Type(s)                                       | handled by |  Miscellaneous |
|-----------------------------------------------|----------------------|---------------------------------------------------------------------|--------------------------------------------------------|------------|---------------|
| `ovos.alerts.dismiss_notification` | 'alert': Alert (serialized) | dismiss an alert notification from the system | | self._gui_dismiss_notification | also removes the pending/missed alert |

### Emits

| Message Type                                           | Message Data         | Description                                                                             | In Response To                                         | Miscellaneous |
|--------------------------------------------------------|----------------------|-----------------------------------------------------------------------------------------|--------------------------------------------------------|---------------|
| `ovos.alerts.get_alerts.response` | 'alert_id': dict   | Responds with uuid keyed alert dictionaries. | `ovos.alerts.get_alerts`  | on error: {"error": ..} |