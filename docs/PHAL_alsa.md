# PHAL ALSA

## Listens to

| Message Type                       | Message Data                           | Description                                                             | Emitted Response Type                                       | Handled by                 |
|------------------------------------|----------------------------------------|-------------------------------------------------------------------------|-------------------------------------------------------------|----------------------------|
| `mycroft.volume.get`               |                                        | Requests the current volume level.                                      | `mycroft.volume.get.response`                               | handle_volume_request      |
| `mycroft.volume.set`               | 'percent': float<br>'play_sound': bool | Sets the volume level.                                                  | `mycroft.audio.play_sound`<br>`mycroft.volume.get.response` | handle_volume_change       |
| `mycroft.volume.increase`          | 'percent': float<br>'play_sound': bool | Increases the volume level.                                             | `mycroft.audio.play_sound`<br>`mycroft.volume.get.response` | handle_volume_increase     |
| `mycroft.volume.decrease`          | 'percent': float<br>'play_sound': bool | Decreases the volume level.                                             | `mycroft.audio.play_sound`<br>`mycroft.volume.get.response` | handle_volume_decrease     |
| `mycroft.volume.set.gui`           | 'percent': float<br>'play_sound': bool | Sets the volume level (GUI interaction).                                | `mycroft.audio.play_sound`                                  | handle_volume_change_gui   |
| `mycroft.volume.mute`              |                                        | Mutes the audio.                                                        | `mycroft.volume.get.response`                               | handle_mute_request        |
| `mycroft.volume.unmute`            |                                        | Unmutes the audio.                                                      | `mycroft.volume.get.response`                               | handle_unmute_request      |
| `mycroft.volume.mute.toggle`       |                                        | Toggles between mute and unmute.                                        | `mycroft.volume.get.response`                               | handle_mute_toggle_request |
| `mycroft.volume.get.sliding.panel` |                                        | Requests volume without invoking the shell OSD (for GUI sliding panel). | `mycroft.volume.get.response`                               | handle_volume_request      |

## Emits

| Message Type               | Message Data                        | Description                               | Handled by |
|----------------------------|-------------------------------------|-------------------------------------------|------------|
| `mycroft.audio.play_sound` | 'uri': 'snd/blop-mark-diangelo.wav' | Plays a sound indicating a volume change. | set_volume |
