# HOMescreen.py

# Listens To
| Message Type                    | Message Data                        | Description                                 | Response Type(s)                  |
|---------------------------------|------------------------------------|---------------------------------------------|------------------------------------|
| homescreen.manager.add          | {"id": str, "class": str}          | Add a homescreen to the manager.            | -                                |
| homescreen.manager.remove       | {"id": str}                        | Remove a homescreen from the manager.       | -                                |
| homescreen.manager.list         | -                                  | Request a list of loaded homescreens.       | homescreen.manager.list.response |
| homescreen.manager.get_active   | -                                  | Request the active homescreen.              | homescreen.manager.get_active.response |
| homescreen.manager.set_active   | {"id": str}                        | Change the configured homescreen.           | -                                |
| homescreen.manager.disable_active | -                                | Disable the active homescreen.              | -                                |
| mycroft.mark2.register_idle     | -                                  | Register an old-style homescreen.           | -                                |
| homescreen.manager.show_active  | -                                  | Show the active homescreen.                 | -                                |
| mycroft.ready                   | -                                  | Signal that Mycroft is ready.               | homescreen.manager.show_active      |

# Emits
| Message Type                    | Message Data                        | Description                                 | In Response to          |
|---------------------------------|------------------------------------|---------------------------------------------|--------------------------|
| homescreen.manager.reload.list  | -                                  | Emit a request for homescreens to register.  | -                        |
| homescreen.manager.activate.display | {"homescreen_id": str}           | Activate and display a homescreen.          | -                        |
| {active_homescreen_id}.idle     | -                                  | Activate an old-style homescreen.           | -                        |
| mycroft.mark2.collect_idle      | -                                  | Trigger collection of older resting screens.| -                        |

