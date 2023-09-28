# gui.py

## Listens to
| Message Type                | Message Data                    | Description                                             | Response Type(s)    |
|-----------------------------|--------------------------------|---------------------------------------------------------|----------------------|
| mycroft.gui.screen.close    | {"skill_id": str}              | Handles the event to close the GUI screen in a skill.   |                      |

## Emits
| Message Type                | Message Data                    | Description                                             | In Response to        |
|-----------------------------|--------------------------------|---------------------------------------------------------|------------------------|
| gui.clear.namespace         | {"__from": str}                | Clears a skill's namespace in the GUI.                  | mycroft.gui.screen.close |

# phal.py

## Listens to
| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| recognizer_loop:record_begin     | None                               | Listening started                           | None                                   |
| recognizer_loop:record_end       | None                               | Listening ended                             | None                                   |
| recognizer_loop:audio_output_start | None                             | Speaking started                            | None                                   |
| recognizer_loop:audio_output_end | None                               | Speaking started                            | None                                   |
| mycroft.awoken                   | None                               | On wakeup animation                         | None                                   |
| recognizer_loop:sleep            | None                               | On naptime animation                        | None                                   |
| speak                            | None                               | On speak messages, intended for enclosures that disregard visemes | None |
| enclosure.notify.no_internet     | None                               |                                       | None                                   |
| enclosure.reset                   | None                               | Restore the enclosure to a started state    | None                                   |
| enclosure.system.reset           | None                               | Reset the enclosure hardware                | None                                   |
| enclosure.system.mute            | None                               | Mute (turn off) the system speaker         | None                                   |
| enclosure.system.unmute          | None                               | Unmute (turn on) the system speaker       | None                                   |
| enclosure.system.blink           | None                               | Make the eyes blink the given number of times | None                               |
| enclosure.eyes.on                | None                               | Illuminate or show the eyes                | None                                   |
| enclosure.eyes.off               | None                               | Turn off or hide the eyes                  | None                                   |
| enclosure.eyes.fill              | None                               | Fill the eyes                               | None                                   |
| enclosure.eyes.blink             | {"side": str}                      | Make the eyes blink                        | None                                   |
| enclosure.eyes.narrow            | None                               | Make the eyes look narrow, like a squint   | None                                   |
| enclosure.eyes.look              | {"side": str}                      | Make the eyes look to the given side       | None                                   |
| enclosure.eyes.color             | {"r": int, "g": int, "b": int}     | Change the eye color to the given RGB color | None                                   |
| enclosure.eyes.brightness         | {"level": int}                     | Set the brightness of the eyes in the display | None                                 |
| enclosure.eyes.reset             | None                               | Restore the eyes to their default (ready) state | None                               |
| enclosure.eyes.timedspin         | {"length": int}                    | Make the eyes 'roll' for the given time     | None                                   |
| enclosure.eyes.volume            | {"volume": int}                    | Indicate the volume using the eyes         | None                                   |
| enclosure.eyes.spin              | None                               | Make the eyes spin                         | None                                   |
| enclosure.eyes.setpixel          | None                               | Set pixel on the eyes                      | None                                   |
| enclosure.mouth.events.activate  | None                               | Enable movement of the mouth with speech   | None                                   |
| enclosure.mouth.events.deactivate | None                              | Disable movement of the mouth with speech  | None                                   |
| enclosure.mouth.talk             | None                               | Show a generic 'talking' animation for non-synched speech | None |
| enclosure.mouth.think            | None                               | Show a 'thinking' image or animation       | None                                   |
| enclosure.mouth.listen           | None                               | Show a 'thinking' image or animation       | None                                   |
| enclosure.mouth.smile            | None                               | Show a 'smile' image or animation          | None                                   |
| enclosure.mouth.viseme           | {"code": int}                      | Display a viseme mouth shape for synched speech | None                             |
| enclosure.mouth.viseme_list      | {"start": int, "viseme_pairs": List[Tuple[int, int]]} | Mouth visemes as a list in a single message | None                      |
| enclosure.mouth.text             | {"text": str}                      | Display text (scrolling as needed)          | None                                   |
| enclosure.mouth.display          | {"img_code": str, "x": int, "y": int, "refresh": bool} | Display images on faceplate. Supports images up to 16x8. Args: img_code (str): text string that encodes a black and white image x (int): x offset for image y (int): y offset for image refresh (bool): specify whether to clear the faceplate before displaying the new image or not. Useful if you'd like to display multiple images on the faceplate at once. | None |
| enclosure.weather.display        | {"img_code": char, "temp": int}   | Show the temperature and a weather icon. Args: img_code (char): one of the following icon codes 0 = sunny 1 = partly cloudy 2 = cloudy 3 = light rain 4 = raining 5 = stormy 6 = snowing 7 = wind/mist temp (int): the temperature (either C or F, not indicated) | None |

