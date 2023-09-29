# ovos-audio message SPEC


- [PlaybackService](#playbackservice)
  * [Listens To](#listens-to)
  * [Emits](#emits)
- [AudioService](#audioservice)
- [Listens to](#listens-to)
- [Emits](#emits-1)


# PlaybackService

## Listens To
| Message Type                 | Message Data                                                  | Description                                         | Response Type(s)              | handled by                    |
|------------------------------|---------------------------------------------------------------|-----------------------------------------------------|-------------------------------|-------------------------------|
| `opm.tts.query`              | N/A                                                           | Responds with TTS plugin data.                      | `opm.tts.query.response`      | self.handle_opm_tts_query     |
| `opm.g2p.query`              | N/A                                                           | Responds with G2P plugin data.                      | `opm.g2p.query.response`      | self.handle_opm_g2p_query     |
| `opm.audio.query`            | N/A                                                           | Responds with audio service plugin data.            | `opm.audio.query.response`    | self.handle_opm_audio_query   |
| `speak`                      | {'utterance': str, 'expect_response': bool}                   | reports is_speaking status                          | `mycroft.audio.is_speaking`   | self.handle_speak             |
| `mycroft.stop`               | N/A                                                           | Handles global stop and shuts down speech.          | `mycroft.stop.handled`        | self.handle_stop              |
| `mycroft.audio.speech.stop`  | N/A                                                           | stops speech.                                       | N/A                           | self.handle_stop              |
| `mycroft.audio.speak.status` | N/A                                                           | reports if Mycroft is speaking.                     | `mycroft.audio.is_speaking`   | self.handle_speak_status      |
| `mycroft.audio.queue`        | {'uri': str, 'listen': bool, 'viseme': str, 'audio_ext': str} | Queues a sound file to play in the speech thread.   | N/A                           | self.handle_queue_audio       |
| `mycroft.audio.play_sound`   | {'uri': str}                                                  | Plays a sound file immediately (may play over TTS). | N/A                           | self.handle_instant_play      |
| `ovos.languages.tts`         | N/A                                                           | Handles a request for supported TTS languages.      | `ovos.languages.tts.response` | self.handle_get_languages_tts |


## Emits
| Message Type                | Message Data                                                                                          | Description                                                 | In Response To               |
|-----------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|------------------------------|
| `opm.tts.query.response`    | {'langs': list, 'plugins': {lang: list}, configs: {plugin_name: {lang: list}}, options: {lang: list}} | Responds to opm.tts.query with TTS plugin data.             | `opm.tts.query`              |
| `opm.g2p.query.response`    | {'langs': list, 'plugins': {lang: list}, configs: {plugin_name: {lang: list}}, options: {lang: list}} | Responds to opm.g2p.query with G2P plugin data.             | `opm.g2p.query`              |
| `opm.audio.query.response`  | {'plugins': list, configs: {backend_name: dict}, options: {lang: list}}                               | Responds to opm.audio.query with audio service plugin data. | `opm.audio.query`            |
| `mycroft.audio.is_speaking` | {'speaking': bool}                                                                                    | Reports whether Mycroft is currently speaking.              | `mycroft.audio.speak.status` |

# AudioService

# Listens to
| Message Type                             | Message Data                     | Description                                               | Response Type(s)                       | handled by                        |
|------------------------------------------|----------------------------------|-----------------------------------------------------------|----------------------------------------|-----------------------------------|
| mycroft.audio.service.play               | {'tracks': list, 'repeat': bool} | Starts playback of a tracklist.                           | N/A                                    | self._play                        |
| mycroft.audio.service.queue              | {'tracks': list}                 | Queues up tracks for playback.                            | N/A                                    | self._queue                       |
| mycroft.audio.service.pause              | N/A                              | Pauses the current audio service.                         | N/A                                    | self._pause                       |
| mycroft.audio.service.resume             | N/A                              | Resumes playback of the paused audio.                     | N/A                                    | self._resume                      |
| mycroft.audio.service.stop               | N/A                              | Stops any playing audio service.                          | N/A                                    | self._stop                        |
| mycroft.audio.service.next               | N/A                              | Skips the current track and plays the next.               | N/A                                    | self._next                        |
| mycroft.audio.service.prev               | N/A                              | Starts playing the previous track.                        | N/A                                    | self._prev                        |
| mycroft.audio.service.track_info         | N/A                              | Requests track information.                               | mycroft.audio.service.track_info_reply | self._track_info                  |
| mycroft.audio.service.list_backends      | N/A                              | Requests a list of available audio backends.              | N/A                                    | self._list_backends               |
| mycroft.audio.service.set_track_position | {'position': int}                | Sets the track position in milliseconds.                  | N/A                                    | self._set_track_position          |
| mycroft.audio.service.get_track_position | N/A                              | Requests the current track position.                      | N/A                                    | self._get_track_position          |
| mycroft.audio.service.get_track_length   | N/A                              | Requests the duration of the audio in milliseconds.       | N/A                                    | self._get_track_length            |
| mycroft.audio.service.seek_forward       | {'seconds': int}                 | Seeks forward by the specified number of seconds.         | N/A                                    | self._seek_forward                |
| mycroft.audio.service.seek_backward      | {'seconds': int}                 | Seeks backward by the specified number of seconds.        | N/A                                    | self._seek_backward               |
| recognizer_loop:audio_output_start       | N/A                              | Triggered when audio output starts and lowers the volume. | N/A                                    | self._lower_volume                |
| recognizer_loop:record_begin             | N/A                              | Triggered when recording begins and lowers the volume.    | N/A                                    | self._lower_volume                |
| recognizer_loop:audio_output_end         | N/A                              | Triggered when audio output ends and restores the volume. | N/A                                    | self._restore_volume              |
| recognizer_loop:record_end               | N/A                              | Restores the volume after recording is done.              | N/A                                    | self._restore_volume_after_record |


# Emits
| Message Type                           | Message Data                   | Description                                       | In Response to                   |
|----------------------------------------|--------------------------------|---------------------------------------------------|----------------------------------|
| mycroft.audio.playing_track            | {'track': str}                 | Informs about the track about to start playing.   | self.track_start                 |
| mycroft.audio.queue_end                | N/A                            | Indicates the end of the playlist.                | self.track_start                 |
| mycroft.stop.handled                   | {'by': "audio:{service_name}"} | Indicates that audio playback was stopped.        | mycroft.audio.service.stop       |
| mycroft.audio.service.track_info_reply | {'data': dict}                 | Sends track information in response to a request. | mycroft.audio.service.track_info |

