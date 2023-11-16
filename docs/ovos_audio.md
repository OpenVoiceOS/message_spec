# ovos-audio message SPEC

- [PlaybackService](#playbackservice)
    * [Listens To](#listens-to)
    * [Emits](#emits)
- [AudioService](#audioservice)
    * [Listens to](#listens-to-1)
    * [Emits](#emits-1)

# PlaybackService

## Listens To

| Message Type                 | Message Data                                                | Description                                         | Response Type(s)              | handled by                    |
|------------------------------|-------------------------------------------------------------|-----------------------------------------------------|-------------------------------|-------------------------------|
| `opm.tts.query`              |                                                             | Responds with TTS plugin data.                      | `opm.tts.query.response`      | self.handle_opm_tts_query     |
| `opm.g2p.query`              |                                                             | Responds with G2P plugin data.                      | `opm.g2p.query.response`      | self.handle_opm_g2p_query     |
| `opm.audio.query`            |                                                             | Responds with audio service plugin data.            | `opm.audio.query.response`    | self.handle_opm_audio_query   |
| `speak`                      | 'utterance': str, 'expect_response': bool                   | generates and queues TTS audio for playback         |                               | self.handle_speak             |
| `mycroft.stop`               |                                                             | Handles global stop and shuts down speech.          | `mycroft.stop.handled`        | self.handle_stop              |
| `mycroft.audio.speech.stop`  |                                                             | stops speech.                                       |                               | self.handle_stop              |
| `mycroft.audio.speak.status` |                                                             | reports if Mycroft is speaking.                     | `mycroft.audio.is_speaking`   | self.handle_speak_status      |
| `mycroft.audio.queue`        | 'uri': str, 'listen': bool, 'viseme': str, 'audio_ext': str | Queues a sound file to play in the speech thread.   |                               | self.handle_queue_audio       |
| `mycroft.audio.play_sound`   | 'uri': str                                                  | Plays a sound file immediately (may play over TTS). |                               | self.handle_instant_play      |
| `ovos.languages.tts`         |                                                             | Handles a request for supported TTS languages.      | `ovos.languages.tts.response` | self.handle_get_languages_tts |

## Emits

| Message Type                  | Message Data                                                                                         | Description                                                 | In Response To               |
|-------------------------------|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|------------------------------|
| `opm.tts.query.response`      | 'langs': List, 'plugins': {lang: List}, configs: {plugin_name: {lang: List}}, options: {lang: List}} | Responds to opm.tts.query with TTS plugin data.             | `opm.tts.query`              |
| `opm.g2p.query.response`      | 'langs': List, 'plugins': {lang: List}, configs: {plugin_name: {lang: List}}, options: {lang: List}} | Responds to opm.g2p.query with G2P plugin data.             | `opm.g2p.query`              |
| `opm.audio.query.response`    | 'plugins': List, configs: {backend_name: Dict}, options: {lang: List}}                               | Responds to opm.audio.query with audio service plugin data. | `opm.audio.query`            |
| `mycroft.audio.is_speaking`   | 'speaking': bool                                                                                     | Reports whether Mycroft is currently speaking.              | `mycroft.audio.speak.status` |
| `ovos.languages.tts.response` | 'langs': List                                                                                        | Handles a request for supported TTS languages.              | `ovos.languages.tts`         |

# AudioService

## Listens to

| Message Type                               | Message Data                   | Description                                               | Response Type(s)                         | handled by                        |
|--------------------------------------------|--------------------------------|-----------------------------------------------------------|------------------------------------------|-----------------------------------|
| `mycroft.audio.service.play`               | 'tracks': List, 'repeat': bool | Starts playback of a tracklist.                           |                                          | self._play                        |
| `mycroft.audio.service.queue`              | 'tracks': List                 | Queues up tracks for playback.                            |                                          | self._queue                       |
| `mycroft.audio.service.pause`              |                                | Pauses the current audio service.                         |                                          | self._pause                       |
| `mycroft.audio.service.resume`             |                                | Resumes playback of the paused audio.                     |                                          | self._resume                      |
| `mycroft.audio.service.stop`               |                                | Stops any playing audio service.                          |                                          | self._stop                        |
| `mycroft.audio.service.next`               |                                | Skips the current track and plays the next.               |                                          | self._next                        |
| `mycroft.audio.service.prev`               |                                | Starts playing the previous track.                        |                                          | self._prev                        |
| `mycroft.audio.service.track_info`         |                                | Requests track information.                               | `mycroft.audio.service.track_info_reply` | self._track_info                  |
| `mycroft.audio.service.list_backends`      |                                | Requests a list of available audio backends.              |                                          | self._list_backends               |
| `mycroft.audio.service.set_track_position` | 'position': int                | Sets the track position in milliseconds.                  |                                          | self._set_track_position          |
| `mycroft.audio.service.get_track_position` |                                | Requests the current track position.                      |                                          | self._get_track_position          |
| `mycroft.audio.service.get_track_length`   |                                | Requests the duration of the audio in milliseconds.       |                                          | self._get_track_length            |
| `mycroft.audio.service.seek_forward`       | 'seconds': int                 | Seeks forward by the specified number of seconds.         |                                          | self._seek_forward                |
| `mycroft.audio.service.seek_backward`      | 'seconds': int                 | Seeks backward by the specified number of seconds.        |                                          | self._seek_backward               |
| `recognizer_loop:audio_output_start`       |                                | Triggered when audio output starts and lowers the volume. |                                          | self._lower_volume                |
| `recognizer_loop:record_begin`             |                                | Triggered when recording begins and lowers the volume.    |                                          | self._lower_volume                |
| `recognizer_loop:audio_output_end`         |                                | Triggered when audio output ends and restores the volume. |                                          | self._restore_volume              |
| `recognizer_loop:record_end`               |                                | Restores the volume after recording is done.              |                                          | self._restore_volume_after_record |

## Emits

| Message Type                             | Message Data                 | Description                                       | In Response to                     |
|------------------------------------------|------------------------------|---------------------------------------------------|------------------------------------|
| `mycroft.audio.playing_track`            | 'track': str                 | Informs about the track about to start playing.   | self.track_start                   |
| `mycroft.audio.queue_end`                |                              | Indicates the end of the playlist.                | self.track_start                   |
| `mycroft.stop.handled`                   | 'by': "audio:{service_name}" | Indicates that audio playback was stopped.        | `mycroft.audio.service.stop`       |
| `mycroft.audio.service.track_info_reply` | 'data': Dict                 | Sends track information in response to a request. | `mycroft.audio.service.track_info` |

