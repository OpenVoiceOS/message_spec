# OVOS GGWave

GGWave is a audio transformer plugin, it consumes the microphone feed

## Listens to

| Message Type          | Message Data | Description                   | Emitted Response Type  | Handled By              |
|-----------------------|--------------|-------------------------------|------------------------|-------------------------|
| `ovos.ggwave.enable`  |              | Enable GGWave functionality.  | `ovos.ggwave.enabled`  | handle_enable function  |
| `ovos.ggwave.disable` |              | Disable GGWave functionality. | `ovos.ggwave.disabled` | handle_disable function |

## Emits

| Message Type                        | Message Data                              | Description                                   | Trigger Message Type  | Handled By        |
|-------------------------------------|-------------------------------------------|-----------------------------------------------|-----------------------|-------------------|
| `ovos.ggwave.enabled`               |                                           | Notification that GGWave has been enabled.    | `ovos.ggwave.enable`  | handle_enable     |
| `ovos.ggwave.disabled`              |                                           | Notification that GGWave has been disabled.   | `ovos.ggwave.disable` | handle_disable    |
| `mycroft.audio.play_sound`          | "uri": str                                | Play an acknowledgment / error sound.         |                       |                   |
| `ovos.skills.install`               | "url": str                                | Install a skill from the specified URL.       |                       | handle_skill      |
| `ovos.pip.install`                  | "packages":List[str]                      | Install a pip package.                        |                       | handle_pip        |
| `ovos.pip.uninstall`                | "packages": List[str]                     | Uninstall a pip package.                      |                       | handle_remove_pip |
| `recognizer_loop:utterance`         | "utterances": List[str]                   | Emit an utterance to the recognizer loop.     |                       | handle_utt        |
| `speak`                             | "utterance": str                          | Speak the specified text.                     |                       | handle_speak      |
| `ovos.phal.nm.connect.open.network` | "connection_name": str                    | Connect to an open WiFi network.              |                       | handle_wifi_pswd  |
| `ovos.phal.nm.connect`              | "connection_name": str<br>"password": str | Connect to a password-protected WiFi network. |                       | handle_wifi_pswd  |
