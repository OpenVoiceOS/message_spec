# ovos-dinkum-listener

## OVOSDinkumVoiceService

### Listens to

| Message Type                         | Message Data                 | Description                                                                                                           | Response Type(s)              |
|--------------------------------------|------------------------------|-----------------------------------------------------------------------------------------------------------------------|-------------------------------|
| `mycroft.mic.mute`                   |                              | Produces empty audio stream                                                                                           |                               |
| `mycroft.mic.unmute`                 |                              | Uses real audio stream                                                                                                |                               |
| `mycroft.mic.listen`                 |                              | Wakes up OVOS and starts recording voice command                                                                      |                               |
| `recognizer_loop:audio_output_start` |                              | Audio output started                                                                                                  |                               |
| `recognizer_loop:audio_output_end`   |                              | Audio output ended                                                                                                    |                               |
| `mycroft.stop`                       |                              | Handler for OVOS.stop, i.e. button press                                                                              |                               |
| `recognizer_loop:sleep`              |                              | Put the voice loop to sleep                                                                                           |                               |
| `recognizer_loop:wake_up`            |                              | Wake up the voice loop                                                                                                | `mycroft.awoken`              |
| `recognizer_loop:record_stop`        |                              | Stop current recording session                                                                                        |                               |
| `recognizer_loop:state.set`          | "state": str<br> "mode": str | Set listening state and mode                                                                                          |                               |
| `recognizer_loop:state.get`          |                              | Query listening state                                                                                                 | `recognizer_loop:state`       |
| `intent.service.skills.activated`    |                              | When a skill is activated, reset the timeout until wakeword is needed again (only used when in hybrid listening mode) |                               |
| `ovos.languages.stt`                 |                              | Handle a request for supported STT languages                                                                          | `ovos.languages.stt.response` |
| `opm.stt.query`                      |                              | Query supported STT languages and plugins                                                                             | `opm.stt.query.response`      |
| `opm.ww.query`                       |                              | Query supported wake word languages and plugins                                                                       | `opm.ww.query.response`       |
| `opm.vad.query`                      |                              | Query supported VAD plugins and options                                                                               | `opm.vad.query.response`      |

### Emits

| Message Type                                 | Message Data                                                            | Description                                            | In Response to              |
|----------------------------------------------|-------------------------------------------------------------------------|--------------------------------------------------------|-----------------------------|
| `recognizer_loop:record_begin`               |                                                                         | Reports that voice command recording has begun         | `mycroft.mic.listen`        |
| `recognizer_loop:wakeword`                   | "utterance": str<br> "lang": str                                        | Reports wake word used to wake up OVOS                 |                             |
| `recognizer_loop:hotword`                    | "utterance": str<br> "lang": str                                        | Reports hotword used to wake up OVOS                   |                             |
| `recognizer_loop:stopword`                   | "utterance": str<br> "lang": str                                        | Reports stop word used to end recording                |                             |
| `recognizer_loop:wakeupword`                 | "utterance": str<br> "lang": str                                        | Reports wake-up word used to wake up OVOS              |                             |
| `recognizer_loop:record_end`                 |                                                                         | Reports that voice command recording has ended         |                             |
| `recognizer_loop:utterance`                  | "utterances": List[str]<br> "lang": str                                 | Result from speech to text of voice command            |                             |
| `recognizer_loop:speech.recognition.unknown` |                                                                         | Sent when empty result from speech to text is returned |                             |
| `mycroft.audio.play_sound`                   | "uri": str                                                              | Play a sound                                           |                             |
| `mycroft.awoken`                             |                                                                         | Notify that OVOS is awake                              | `recognizer_loop:wake_up`   |
| `recognizer_loop:state`                      | "mode": str<br> "state": str                                            | Query listening state                                  | `recognizer_loop:state.get` |
| `ovos.languages.stt.response`                | "langs": List[str]                                                      | Response for supported STT languages                   | `ovos.languages.stt`        |
| `opm.stt.query.response`                     | "langs": List <br>"plugins": List<br>"configs": List<br>"options": List | Response for supported STT plugins and options         | `opm.stt.query`             |
| `opm.ww.query.response`                      | "langs": List <br>"plugins": List<br>"configs": List<br>"options": List | Response for supported wake word plugins and options   | `opm.ww.query`              |
| `opm.vad.query.response`                     | "plugins": List<br>"configs": List<br>"options": List                   | Response for supported VAD plugins and options         | `opm.vad.query`             |
| `mycroft.mic.get_status.response`            | "muted": bool                                                           | Report mic mute status (OVOS software side)            | `mycroft.mic.get_status`    |

