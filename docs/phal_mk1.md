# PHAL Mark1 Faceplate

## Listens to

Also see the [PHAL plugin](./opm.md) base class for default events handled by mk1 faceplate

| Message Type                  | Message Data                                                             | Description                                                | Handled by                            |
|-------------------------------|--------------------------------------------------------------------------|------------------------------------------------------------|---------------------------------------|
| `system.factory.reset.ping`   |                                                                          | Report that we can factory reset mk1 faceplate             | handle_register_factory_reset_handler |
| `system.factory.reset.phal`   |                                                                          | Perform faceplate factory reset                            | handle_factory_reset                  |
| `mycroft.internet.connected`  |                                                                          | Show no-internet icon                                      | on_display_reset                      |
| `mycroft.stop`                |                                                                          | Clear faceplate                                            | on_display_reset                      |
| `ovos.common_play.play`       |                                                                          | Show music icon                                            | on_music                              |
| `ovos.common_play.stop`       |                                                                          | Clear music icon                                           | on_display_reset                      |
| `mycroft.audio.service.play`  |                                                                          | Show music icon                                            | on_music                              |
| `mycroft.audio.service.stop`  |                                                                          | Clear music icon                                           | on_display_reset                      |
| `enclosure.eyes.on`           |                                                                          | Illuminate or show the eyes.                               | on_eyes_on                            |
| `enclosure.eyes.off`          |                                                                          | Turn off or hide the eyes.                                 | on_eyes_off                           |
| `enclosure.eyes.fill`         | "percentage": int                                                        | Triggered to fill a percentage of the eyes.                | on_eyes_fill                          |
| `enclosure.eyes.blink`        | "side": str                                                              | Make the eyes blink.                                       | on_eyes_blink                         |
| `enclosure.eyes.narrow`       |                                                                          | Make the eyes look narrow, like a squint.                  | on_eyes_narrow                        |
| `enclosure.eyes.look`         | "side": str                                                              | Make the eyes look to the given side.                      | on_eyes_look                          |
| `enclosure.eyes.color`        | "r": int<br>"g": int<br>"b": int                                         | Change the eye color to the given RGB color.               | on_eyes_color                         |
| `enclosure.eyes.brightness`   | "level": int                                                             | Set the brightness of the eyes in the display.             | on_eyes_brightness                    |
| `enclosure.eyes.reset`        |                                                                          | Restore the eyes to their default (ready) state.           | on_eyes_reset                         |
| `enclosure.eyes.timedspin`    | "length": int                                                            | Make the eyes 'roll' for the given time.                   | on_eyes_timed_spin                    |
| `enclosure.eyes.volume`       | "volume": int                                                            | Indicate the volume using the eyes.                        | on_eyes_volume                        |
| `enclosure.eyes.spin`         |                                                                          | Make the eyes 'spin'.                                      | on_eyes_spin                          |
| `enclosure.eyes.set_pixel`    | "idx": int<br>"r": int<br>"g": int<br>"b": int                           | Set the color of a specific eye pixel.                     | on_eyes_set_pixel                     |
| `enclosure.mouth.reset`       |                                                                          | Restore the mouth display to normal (blank).               | on_display_reset                      |
| `enclosure.mouth.talk`        |                                                                          | Show a generic 'talking' animation for non-synched speech. | on_talk                               |
| `enclosure.mouth.think`       |                                                                          | Show a 'thinking' image or animation.                      | on_think                              |
| `enclosure.mouth.listen`      |                                                                          | Show a 'listening' image or animation.                     | on_listen                             |
| `enclosure.mouth.smile`       |                                                                          | Show a 'smile' image or animation.                         | on_smile                              |
| `enclosure.mouth.viseme`      | "code": int                                                              | Display a viseme mouth shape for synced speech.            | on_viseme                             |
| `enclosure.mouth.viseme_list` | "start": int<br>"visemes": [(int, int)]                                  | Send mouth visemes as a list in a single message.          | on_viseme_list                        |
| `enclosure.mouth.text`        | "text": str                                                              | Display text (scrolling as needed).                        | on_text                               |
| `enclosure.mouth.display`     | "img_code": str<br>"xOffset": int<br>"yOffset": int<br>"clearPrev": bool | Display images on faceplate.                               | on_display                            |
| `enclosure.weather.display`   | "img_code": char<br>"temp": int                                          | Show the temperature and a weather icon.                   | on_weather_display                    |

## Emits

| Message Type                    | Message Data                       | Description                                       | Handled by                            |
|---------------------------------|------------------------------------|---------------------------------------------------|---------------------------------------|
| `system.factory.reset.register` | "skill_id": "ovos-phal-plugin-mk1" | Register the factory reset handler in the system. | handle_register_factory_reset_handler |

