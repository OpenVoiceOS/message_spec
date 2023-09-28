# service.py

# Listens to
| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| mycroft.mic.mute                | None                               | Produces empty audio stream                  | N/A                                    |
| mycroft.mic.unmute              | None                               | Uses real audio stream                      | N/A                                    |
| mycroft.mic.listen              | None                               | Wakes up mycroft and starts recording voice command | N/A                                    |
| recognizer_loop:awoken          | None                               | Reports that mycroft is now awake           | N/A                                    |
| recognizer_loop:wake            | None                               | Reports wake word used to wake up mycroft    | N/A                                    |
| recognizer_loop:record_begin    | None                               | Reports that voice command recording has begun | N/A                                    |
| recognizer_loop:record_end      | None                               | Reports that voice command recording has ended | N/A                                    |
| recognizer_loop:utterance       | {"utterances": [str], "lang": str} | Result from speech to text of voice command  | N/A                                    |
| recognizer_loop:speech.recognition.unknown | None                      | Sent when empty result from speech to text is returned | N/A                                    |
| voice.service.connected         | None                               |                                           | voice.service.connected.response        |
| voice.initialize.started         | None                               |                                           | N/A                                    |
| voice.initialize.ended           | None                               |                                           | N/A                                    |
| recognizer_loop:audio_output_start | None                            | Audio output started                         | N/A                                    |
| recognizer_loop:audio_output_end | None                             | Audio output ended                           | N/A                                    |
| mycroft.stop                    | None                               | Handler for mycroft.stop, i.e. button press | N/A                                    |
| recognizer_loop:sleep           | None                               | Put the voice loop to sleep                 | N/A                                    |
| recognizer_loop:wake_up         | None                               | Wake up the voice loop                      | mycroft.awoken                         |
| recognizer_loop:record_stop     | None                               | Stop current recording session               | N/A                                    |
| recognizer_loop:state.set       | {"state": str, "mode": str}         | Set listening state and mode                | N/A                                    |
| recognizer_loop:state.get       | None                               | Query listening state                       | recognizer_loop:state                   |
| intent.service.skills.activated | None                               | When a skill is activated, reset the timeout until wakeword is needed again (only used when in hybrid listening mode) | N/A |
| ovos.languages.stt              | None                               | Handle a request for supported STT languages | ovos.languages.stt.response             |
| opm.stt.query                   | None                               | Query supported STT languages and plugins   | opm.stt.query.response                  |
| opm.ww.query                    | None                               | Query supported wake word languages and plugins | opm.ww.query.response                  |
| opm.vad.query                   | None                               | Query supported VAD plugins and options     | opm.vad.query.response                 |

# Emits
| Message Type                    | Message Data                        | Description                                 | In Response to          |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| recognizer_loop:record_begin    | None                               | Reports that voice command recording has begun | mycroft.mic.listen                   |
| recognizer_loop:wakeword        | {"utterance": str, "lang": str}    | Reports wake word used to wake up mycroft    | N/A                                    |
| recognizer_loop:hotword         | {"utterance": str, "lang": str}    | Reports hotword used to wake up mycroft      | N/A                                    |
| recognizer_loop:stopword        | {"utterance": str, "lang": str}    | Reports stop word used to end recording     | N/A                                    |
| recognizer_loop:wakeupword      | {"utterance": str, "lang": str}    | Reports wake-up word used to wake up mycroft | N/A                                    |
| recognizer_loop:record_end      | None                               | Reports that voice command recording has ended | N/A                                    |
| recognizer_loop:utterance       | {"utterances": [str], "lang": str} | Result from speech to text of voice command  | N/A                                    |
| recognizer_loop:speech.recognition.unknown | None                      | Sent when empty result from speech to text is returned | N/A                                    |
| mycroft.audio.play_sound        | {"uri": str}                       | Play a sound                                | N/A                                    |
| mycroft.awoken                  | None                               | Notify that mycroft is awake                | recognizer_loop:wake_up                |
| recognizer_loop:state            | {"mode": str, "state": str}        | Query listening state                       | recognizer_loop:state.get               |
| ovos.languages.stt.response     | {"langs": [str]}                   | Response for supported STT languages       | ovos.languages.stt                   |
| opm.stt.query.response          | {"langs": [{"name": str, "module": str, "languages": [str]}]} | Response for supported STT languages and plugins | opm.stt.query                       |
| opm.ww.query.response           | {"langs": [{"name": str, "module": str, "languages": [str]}]} | Response for supported wake word languages and plugins | opm.ww.query                        |
| opm.vad.query.response          | {"langs": [{"name": str, "module": str, "plugins": [{"name": str, "description": str, "default": bool, "active": bool, "sample_rate": int, "frame_ms": int}]}]} | Response for supported VAD plugins and options | opm.vad.query                       |


