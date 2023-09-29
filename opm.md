# GUIExtension

## Listens to
| Message Type                | Message Data                    | Description                                             | Response Type(s)    | Handled by                   |
|-----------------------------|--------------------------------|---------------------------------------------------------|----------------------|------------------------------|
| mycroft.gui.screen.close    | {"skill_id": str}              | Handles the event to close the GUI screen in a skill.   | gui.clear.namespace  | self.handle_remove_namespace |

## Emits
| Message Type                | Message Data                    | Description                                            | In Response to           |
|-----------------------------|--------------------------------|---------------------------------------------------------|--------------------------|
| gui.clear.namespace         | {"__from": str}                | Clears a skill's namespace in the GUI.                  | mycroft.gui.screen.close |

# PHALPlugin

| Message Type                         | Message Data                                           | Description                                                                          |  Handled by                |
|--------------------------------------|--------------------------------------------------------|--------------------------------------------------------------------------------------|----------------------------|
| 'recognizer_loop:record_begin'       | None                                                   | Listening started                                                                    | `on_record_begin`          |
| 'recognizer_loop:record_end'         | None                                                   | Listening ended                                                                      | `on_record_end`            |
| 'recognizer_loop:audio_output_start' | None                                                   | Speaking started                                                                     | `on_audio_output_start`    |
| 'recognizer_loop:audio_output_end'   | None                                                   | Speaking started                                                                     | `on_audio_output_end`      |
| 'recognizer_loop:sleep'              | None                                                   | On naptime animation                                                                 | `on_sleep`                 |
| 'mycroft.awoken'                     | None                                                   | On wakeup animation                                                                  | `on_awake`                 |
| 'speak'                              | None                                                   | On speak messages, intended for enclosures                                           | `on_speak`                 |
| 'enclosure.notify.no_internet'       | None                                                   |                                                                                      | `on_no_internet`           |
| 'enclosure.reset'                    | None                                                   | The enclosure should restore itself to a started state.                              | `on_reset`                 |
| 'enclosure.system.reset'             | None                                                   | The enclosure hardware should reset any CPUs, etc.                                   | `on_system_reset`          |
| 'enclosure.system.mute'              | None                                                   | Mute (turn off) the system speaker.                                                  | `on_system_mute`           |
| 'enclosure.system.unmute'            | None                                                   | Unmute (turn on) the system speaker.                                                 | `on_system_unmute`         |
| 'enclosure.system.blink'             | None                                                   | The 'eyes' should blink the given number of times.                                   | `on_system_blink`          |
| 'enclosure.eyes.on'                  | None                                                   | Illuminate or show the eyes.                                                         | `on_eyes_on`               |
| 'enclosure.eyes.off'                 | None                                                   | Turn off or hide the eyes.                                                           | `on_eyes_off`              |
| 'enclosure.eyes.fill'                | None                                                   | Fill the eyes                                                                        | `on_eyes_fill`             |
| 'enclosure.eyes.blink'               | {"side": str}                                          | Make the eyes blink                                                                  | `on_eyes_blink`            |
| 'enclosure.eyes.narrow'              | None                                                   | Make the eyes look narrow, like a squint                                             | `on_eyes_narrow`           |
| 'enclosure.eyes.look'                | {"side": str}                                          | Make the eyes look to the given side                                                 | `on_eyes_look`             |
| 'enclosure.eyes.color'               | {"r": int, "g": int, "b": int}                         | Change the eye color to the given RGB color                                          | `on_eyes_color`            |
| 'enclosure.eyes.brightness'          | {"level": int}                                         | Set the brightness of the eyes in the display                                        | `on_eyes_brightness`       |
| 'enclosure.eyes.volume'              | {"volume": int}                                        | Indicate the volume using the eyes                                                   | `on_eyes_volume`           |
| 'enclosure.eyes.spin'                | None                                                   |                                                                                      | `on_eyes_spin`             |
| 'enclosure.eyes.timedspin'           | {"length": int}                                        | Make the eyes 'roll' for the given time                                              | `on_eyes_timed_spin`       |
| 'enclosure.eyes.setpixel'            | None                                                   | Set pixel on the eyes                                                                | `on_eyes_set_pixel`        |
| 'enclosure.eyes.reset'               | None                                                   | Restore the eyes to their default (ready) state.                                     | `on_eyes_reset`            |
| 'enclosure.mouth.events.activate'    | None                                                   | Enable movement of the mouth with speech                                             | `_activate_mouth_events`   |
| 'enclosure.mouth.events.deactivate'  | None                                                   | Disable movement of the mouth with speech                                            | `_deactivate_mouth_events` |
| 'enclosure.mouth.reset'              | None                                                   | reset mouth to default state                                                         | `on_display_reset`         |
| 'enclosure.mouth.talk'               | None                                                   | Show a generic 'talking' animation for non-synched speech                            | `on_talk`                  |
| 'enclosure.mouth.think'              | None                                                   | Show a 'thinking' image or animation                                                 | `on_think`                 |
| 'enclosure.mouth.listen'             | None                                                   | Show a 'thinking' image or animation                                                 | `on_listen`                |
| 'enclosure.mouth.smile'              | None                                                   | Show a 'smile' image or animation                                                    | `on_smile`                 |
| 'enclosure.mouth.viseme'             | {"code": int}                                          | Display a viseme mouth shape for synched speech                                      | `on_viseme`                |
| 'enclosure.mouth.viseme_list'        | {"start": int, "viseme_pairs": List[Tuple[int, int]]}  | Mouth visemes as a list in a single message                                          | `on_viseme_list`           |
| 'enclosure.mouth.text'               | {"text": str}                                          | Display text (scrolling as needed)                                                   | `on_text`                  |
| 'enclosure.mouth.display'            | {"img_code": str, "x": int, "y": int, "refresh": bool} | Display images on faceplate. Currently supports images up to 16x8, or half the face. | `on_display`               |
| 'enclosure.weather.display'          | {"img_code": char, "temp": int}                        | Show a the temperature and a weather icon                                            | `on_weather_display`       |
