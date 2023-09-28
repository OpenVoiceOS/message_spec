# service.py

## Listens To
| Message Type           | Message Data   | Description                                       | Response Type(s) |
|------------------------|----------------|---------------------------------------------------|-------------------|
| `opm.tts.query`        | None           | Responds to opm.tts.query with TTS plugin data.  | `opm.tts.query.response` |
| `opm.g2p.query`        | None           | Responds to opm.g2p.query with G2P plugin data.  | `opm.g2p.query.response` |
| `opm.audio.query`      | None           | Responds to opm.audio.query with audio plugin data. | `opm.audio.query.response` |
| `speak`                | {'utterance': str, 'expect_response': bool} | reports is_speaking status| `mycroft.audio.is_speaking`|
| `mycroft.stop`         | None           | Handles the "stop" message and shuts down speech. | `mycroft.stop.handled` |
| `mycroft.audio.speech.stop` | None     | Handles the "mycroft.audio.speech.stop" message and stops speech. | None |
| `mycroft.audio.speak.status` | None     | Handles the "mycroft.audio.speak.status" message and reports if Mycroft is speaking. | `mycroft.audio.is_speaking` |
| `mycroft.audio.queue`  | {'uri': str, 'listen': bool, 'viseme': str, 'audio_ext': str} | Queues a sound file to play in the speech thread. | None |
| `mycroft.audio.play_sound` | {'uri': str} | Plays a sound file immediately (may play over TTS). | None |
| `ovos.languages.tts`   | None           | Handles a request for supported TTS languages.  | `ovos.languages.tts.response` |

## Emits
| Message Type           | Message Data   | Description                                       | In Response To |
|------------------------|----------------|---------------------------------------------------|----------------|
| `opm.tts.query.response` | {'langs': list} | Responds to opm.tts.query with TTS plugin data. | `opm.tts.query` |
| `opm.g2p.query.response` | {'langs': list} | Responds to opm.g2p.query with G2P plugin data. | `opm.g2p.query` |
| `opm.audio.query.response` | {'plugins': list} | Responds to opm.audio.query with audio plugin data. | `opm.audio.query` |
| `mycroft.audio.is_speaking` | {'speaking': bool} | Reports whether Mycroft is currently speaking. | `mycroft.audio.speak.status` |

# audio.py

# Listens to
| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| mycroft.audio.service.play      | {'tracks': list, 'repeat': bool}   | Starts playback of a tracklist.            | None                                   |
| mycroft.audio.service.queue     | {'tracks': list}                   | Queues up tracks for playback.             | None                                   |
| mycroft.audio.service.pause     | None                               | Pauses the current audio service.         | None                                   |
| mycroft.audio.service.resume    | None                               | Resumes playback of the paused audio.      | None                                   |
| mycroft.audio.service.stop      | None                               | Stops any playing audio service.           | None                                   |
| mycroft.audio.service.next      | None                               | Skips the current track and plays the next. | None                                   |
| mycroft.audio.service.prev      | None                               | Starts playing the previous track.         | None                                   |
| mycroft.audio.service.track_info| None                               | Requests track information.                | mycroft.audio.service.track_info_reply  |
| mycroft.audio.service.list_backends | None                          | Requests a list of available audio backends.| None                                  |
| mycroft.audio.service.set_track_position | {'position': int}            | Sets the track position in milliseconds.   | None                                   |
| mycroft.audio.service.get_track_position | None                      | Requests the current track position.       | None                                   |
| mycroft.audio.service.get_track_length | None                        | Requests the duration of the audio in milliseconds. | None                             |
| mycroft.audio.service.seek_forward | {'seconds': int}                | Seeks forward by the specified number of seconds. | None                               |
| mycroft.audio.service.seek_backward | {'seconds': int}               | Seeks backward by the specified number of seconds. | None                              |
| recognizer_loop:audio_output_start | None                             | Triggered when audio output starts and lowers the volume. | None                           |
| recognizer_loop:record_begin    | None                               | Triggered when recording begins and lowers the volume. | None                           |
| recognizer_loop:audio_output_end | None                               | Triggered when audio output ends and restores the volume. | None                           |
| recognizer_loop:record_end       | None                               | Restores the volume after recording is done. | None                           |

# Emits
| Message Type                    | Message Data                        | Description                                 | In Response to          |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| mycroft.audio.playing_track     | {'track': str}                     | Informs about the track about to start playing. | mycroft.audio.service.play          |
| mycroft.audio.queue_end         | None                               | Indicates the end of the playlist.          | mycroft.audio.service.stop          |
| mycroft.stop.handled            | {'by': str}                        | Indicates that audio playback was stopped.   | mycroft.audio.service.stop          |
| mycroft.audio.service.track_info_reply | {'data': dict}               | Sends track information in response to a request. | mycroft.audio.service.track_info  |

