# OVOS Utils

## OCPInterface

For skills and applications that want to interact with OCP

### Emits

| Message Type                      | Message Data                                               | Description                               | Emitted by |
|-----------------------------------|------------------------------------------------------------|-------------------------------------------|------------|
| `ovos.common_play.playlist.queue` | {'tracks': [dict, ...]}                                    | Queue up a track to OCP playing playlist. | queue      |
| `ovos.common_play.play`           | {"media": dict, "playlist": [dict, ...], "utterance": str} | Start playback.                           | play       |

## ClassicAAudioServiceInterface

Used internally by OCP / ovos-audio, usage not recommended for third party integrations


### Emits

| Message Type                             | Message Data                                                      | Description                               | Emitted by           |
|------------------------------------------|-------------------------------------------------------------------|-------------------------------------------|----------------------|
| mycroft.audio.service.queue              | {'tracks': [str or (str, str)]}                                   | Queue up a track to the playing playlist. | `queue`              |
| mycroft.audio.service.play               | {'tracks': [str or (str, str)], 'utterance': str, 'repeat': bool} | Start playback.                           | `play`               |
| mycroft.audio.service.stop               |                                                                   | Stop the track.                           | `stop`               |
| mycroft.audio.service.next               |                                                                   | Change to the next track.                 | `next`               |
| mycroft.audio.service.prev               |                                                                   | Change to the previous track.             | `prev`               |
| mycroft.audio.service.pause              |                                                                   | Pause playback.                           | `pause`              |
| mycroft.audio.service.resume             |                                                                   | Resume paused playback.                   | `resume`             |
| mycroft.audio.service.seek_forward       | {'seconds': int or float}                                         | Skip ahead X seconds.                     | `seek_forward`       |
| mycroft.audio.service.seek_backward      | {'seconds': int or float}                                         | Rewind X seconds.                         | `seek_backward`      |
| mycroft.audio.service.set_track_position | {'position': int or float}                                        | Seek X seconds.                           | `set_track_position` |

## AudioServiceInterface

DEPRECATED: backwards compat layer for skills in the wild that interfaced with audio service instead of OCP

### Emits

| Message Type                        | Message Data                                                        | Description                                       | Emitted by                         |
|-------------------------------------|---------------------------------------------------------------------|---------------------------------------------------|------------------------------------|
| ovos.common_play.playlist.queue     | {'tracks': List[Dict]}                                              | Queue up a track to playing playlist.             | `queue`                            |
| ovos.common_play.play               | {'media': Dict, 'playlist': List, 'utterance': str, 'repeat': bool} | Start playback.                                   | `play`                             |
| ovos.common_play.stop               |                                                                     | Stop the track.                                   | `stop`                             |
| ovos.common_play.next               |                                                                     | Change to the next track.                         | `next`                             |
| ovos.common_play.previous           |                                                                     | Change to the previous track.                     | `prev`                             |
| ovos.common_play.pause              |                                                                     | Pause playback.                                   | `pause`                            |
| ovos.common_play.resume             |                                                                     | Resume paused playback.                           | `resume`                           |
| ovos.common_play.seek               | {'seconds': int}                                                    | Skip ahead or rewind X seconds.                   | `seek_forward`<br> `seek_backward` |
| ovos.common_play.get_track_length   |                                                                     | Get the duration of the audio in milliseconds.    | `get_track_length`                 |
| ovos.common_play.get_track_position |                                                                     | Get the current position in milliseconds.         | `get_track_position`               |
| ovos.common_play.set_track_position | {'position': int}                                                   | Go to X position in milliseconds.                 | `set_track_position`               |
| ovos.common_play.track_info         |                                                                     | Request information of the current playing track. | `track_info`                       |
| ovos.common_play.list_backends      |                                                                     | Return available audio backends.                  | `available_backends`               |

## IntentQueryApi

DEPRECATION NOTICE: this class / bus messages are marked for heavy refactoring/deprecation in ovos-core 0.0.9 with the
introduction of intent pipelines

### Listens To

| Message Type                                 | Message Data                       | Description                                           | Emitted Response Type                            | Handled By               |
|----------------------------------------------|------------------------------------|-------------------------------------------------------|--------------------------------------------------|--------------------------|
| `intent.service.adapt.reply`                 | {"intent": str}                    | Reply with the best adapt intent for an utterance     | `intent.service.adapt.get`                       | `get_adapt_intent`       |
| `intent.service.padatious.reply`             | {"intent": str}                    | Reply with the best padatious intent for an utterance | `intent.service.padatious.get`                   | `get_padatious_intent`   |
| `intent.service.intent.reply`                | {"intent": str}                    | Reply with the best intent for an utterance           | `intent.service.intent.get`                      | `get_intent`             |
| `intent.service.skills.reply`                | {"skills": list}                   | Reply with the skills manifest                        | `intent.service.skills.get`                      | `get_skills_manifest`    |
| `intent.service.active_skills.reply`         | {"skills": list}                   | Reply with the active skills                          | `intent.service.active_skills.get`               | `get_active_skills`      |
| `intent.service.adapt.manifest`              | {"intents": list}                  | Reply with the adapt manifest                         | `intent.service.adapt.manifest.get`              | `get_adapt_manifest`     |
| `intent.service.padatious.manifest`          | {"intents": list}                  | Reply with the padatious manifest                     | `intent.service.padatious.manifest.get`          | `get_padatious_manifest` |
| `intent.service.intent.manifest`             | {"adapt": list, "padatious": list} | Reply with the intent manifest                        | `intent.service.intent.manifest.get`             | `get_intent_manifest`    |
| `intent.service.adapt.vocab.manifest`        | {"vocab": list}                    | Reply with the vocabulary manifest                    | `intent.service.adapt.vocab.manifest.get`        | `get_vocab_manifest`     |
| `intent.service.adapt.vocab.manifest`        | {"vocab": list}                    | Reply with the regex manifest                         | `intent.service.adapt.vocab.manifest.get`        | `get_regex_manifest`     |
| `intent.service.padatious.entities.manifest` | {"entities": list}                 | Reply with the entities manifest                      | `intent.service.padatious.entities.manifest.get` | `get_entities_manifest`  |
| `intent.service.padatious.entities.manifest` | {"keywords": list}                 | Reply with the keywords manifest                      | `intent.service.padatious.entities.manifest.get` | `get_keywords_manifest`  |

### Emits

| Message Type                                     | Message Data                    | Description                                     | Trigger Message Type                         | Handled By               |
|--------------------------------------------------|---------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------|
| `intent.service.adapt.get`                       | {"utterance": str, "lang": str} | Get the best adapt intent for a given utterance | `intent.service.adapt.reply`                 | `get_adapt_intent`       |
| `intent.service.padatious.get`                   | {"utterance": str, "lang": str} | Get the best padatious intent for an utterance  | `intent.service.padatious.reply`             | `get_padatious_intent`   |
| `intent.service.intent.get`                      | {"utterance": str, "lang": str} | Get the best intent for a given utterance       | `intent.service.intent.reply`                | `get_intent`             |
| `intent.service.skills.get`                      |                                 | Get the skills manifest                         | `intent.service.skills.reply`                | `get_skills_manifest`    |
| `intent.service.active_skills.get`               |                                 | Get the active skills                           | `intent.service.active_skills.reply`         | `get_active_skills`      |
| `intent.service.adapt.manifest.get`              |                                 | Get the adapt manifest                          | `intent.service.adapt.manifest`              | `get_adapt_manifest`     |
| `intent.service.padatious.manifest.get`          |                                 | Get the padatious manifest                      | `intent.service.padatious.manifest`          | `get_padatious_manifest` |
| `intent.service.intent.manifest.get`             |                                 | Get the intent manifest                         |                                              | `get_intent_manifest`    |
| `intent.service.adapt.vocab.manifest.get`        |                                 | Get the vocabulary manifest                     | `intent.service.adapt.vocab.manifest`        | `get_vocab_manifest`     |
| `intent.service.adapt.vocab.manifest.get`        |                                 | Get the regex manifest                          | `intent.service.adapt.vocab.manifest`        | `get_regex_manifest`     |
| `intent.service.padatious.entities.manifest.get` |                                 | Get the entities manifest                       | `intent.service.padatious.entities.manifest` | `get_entities_manifest`  |
| `intent.service.padatious.entities.manifest.get` |                                 | Get the keywords manifest                       |                                              | `get_keywords_manifest`  |

## IntentServiceInterface

DEPRECATION NOTICE: this class / bus messages are marked for heavy refactoring/deprecation in ovos-core 0.0.9 with the
introduction of intent pipelines

### Emits

| Message Type                | Message Data                                               | Description                                               | Emitted by                  |
|-----------------------------|------------------------------------------------------------|-----------------------------------------------------------|-----------------------------|
| `register_vocab`            | `{entity_data: dict, compatibility_data: dict              | Register an Adapt keyword with the intent service.        | `register_adapt_keyword`    |
| `register_vocab`            | `{regex: str, lang: str                                    | Register a regex string with the intent service.          | `register_adapt_regex`      |
| `register_intent`           | `intent_parser.__dict__`                                   | Register an Adapt intent parser object.                   | `register_adapt_intent`     |
| `padatious:register_intent` | `{file_name: str, samples: List[str], name: str, lang: str | Register a Padatious intent file with the intent service. | `register_padatious_intent` |
| `padatious:register_entity` | `{file_name: str, samples: List[str], name: str, lang: str | Register a Padatious entity file with the intent service. | `register_padatious_entity` |
| `detach_intent`             | "intent_name": f"{self.skill_id}:{intent_name}"            | Remove an intent from the intent service.                 | `detach_intent`             |
| `add_context`               | `{'context': context, 'word': word, 'origin': origin       | Set an Adapt context.                                     | `set_adapt_context`         |
| `remove_context`            | `{'context': context                                       | Remove an Adapt context.                                  | `remove_adapt_context`      |

## EventSchedulerInterface

API for scheduling bus messages to be emitted by ovos-core, typically used by skills

### Listens to

| Message Type                               | Message Data                                                         | Description                                                    | Emitted Response Type                      | Handled by                   |
|--------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------|--------------------------------------------|------------------------------|
| mycroft.scheduler.schedule_event           | {'time': timestamp, 'event': name, 'repeat': interval, 'data': data} | Schedule a single-shot event.                                  | mycroft.scheduler.schedule_event.response  | `_schedule_event`            |
| mycroft.scheduler.schedule_repeating_event | {'time': timestamp, 'event': name, 'repeat': interval, 'data': data} | Schedule a repeating event.                                    | mycroft.scheduler.schedule_event.response  | `_schedule_event`            |
| mycroft.scheduler.update_event             | {'event': unique_name, 'data': data}                                 | Change data of a scheduled event.                              |                                            | `update_scheduled_event`     |
| mycroft.scheduler.remove_event             | {'event': unique_name}                                               | Cancel a pending event. The event will no longer be scheduled. |                                            | `cancel_scheduled_event`     |
| mycroft.scheduler.get_event                | {'name': event_name}                                                 | Get scheduled event data and return the amount of time left.   | mycroft.event_status.callback.{event_name} | `get_scheduled_event_status` |

### Emits

| Message Type                                        | Message Data                                                | Description                                 | Trigger Message Type | Handled by                   |
|-----------------------------------------------------|-------------------------------------------------------------|---------------------------------------------|----------------------|------------------------------|
| mycroft.scheduler.schedule_event.response           | {'success': True/False, 'event': unique_name, 'data': data} | Response to scheduling a single-shot event. |                      | `_schedule_event`            |
| mycroft.scheduler.schedule_repeating_event.response | {'success': True/False, 'event': unique_name, 'data': data} | Response to scheduling a repeating event.   |                      | `_schedule_event`            |
| mycroft.schedule.update_event.response              | {'success': True/False, 'event': unique_name, 'data': data} | Response to updating a scheduled event.     |                      | `update_scheduled_event`     |
| mycroft.scheduler.remove_event.response             | {'success': True/False, 'event': unique_name}               | Response to canceling a pending event.      |                      | `cancel_scheduled_event`     |
| mycroft.scheduler.get_event.response                | {'success': True/False, 'event': unique_name, 'data': data} | Response to getting scheduled event data.   |                      | `get_scheduled_event_status` |

## GUIWidgets

API for interacting with homescreen skill widgets

### Emits

| Message Type         | Message Data                | Description           | Trigger Message Type | Handled By      |
|----------------------|-----------------------------|-----------------------|----------------------|-----------------|
| ovos.widgets.display | {"type": str, "data": dict} | Display a GUI widget. |                      | `show_widget`   |
| ovos.widgets.remove  | {"type": str, "data": dict} | Remove a GUI widget.  |                      | `remove_widget` |
| ovos.widgets.update  | {"type": str, "data": dict} | Update a GUI widget.  |                      | `update_widget` |

## GUIInterface

Used by skills and any other component that wants to display a GUI in their own namespace

### Listens To

| Message Type            | Message Data | Description                                    | Emitted Response Type | Handled By       |
|-------------------------|--------------|------------------------------------------------|-----------------------|------------------|
| gui.request_page_upload |              | Request to upload GUI pages.                   | gui.page.upload       | upload_gui_pages |
| {skill_id}.set          |              | event sent from GUI client side                |                       |                  |
| {skill_id}.{event}      |              | Skill specific event sent from GUI client side |                       | register_handler |

### Emits

| Message Type                            | Message Data    | Description                                               | Trigger Message Type    | Handled By                       |
|-----------------------------------------|-----------------|-----------------------------------------------------------|-------------------------|----------------------------------|
| gui.volunteer_page_upload               | "skill_id": str | Volunteer to upload GUI pages.                            |                         | `setup_default_handlers`         |
| gui.value.set                           | "__from": str   | Set GUI values for the skill.                             |                         | `gui_set`                        |
| gui.page.upload                         | "__from": str   | Upload GUI pages to the requested infrastructure.         | gui.request_page_upload | `upload_gui_pages`               |
| ovos.notification.api.set               | "__from": str   | Set a notification in the GUI.                            |                         | `show_notification`              |
| ovos.notification.api.set.controlled    | "__from": str   | Set a controlled notification in the GUI.                 |                         | `show_controlled_notification`   |
| ovos.notification.api.remove.controlled | "__from": str   | Remove a controlled notification in the GUI.              |                         | `remove_controlled_notification` |
| gui.clear.namespace                     | "__from": str   | Reset the value dictionary and remove namespace from GUI. |                         | `clear`                          |
| gui.page.show                           | "__from": str   | Show a GUI page.                                          |                         | `show_page`                      |
| gui.page.delete                         | "__from": str   | Remove a GUI page.                                        |                         | `remove_page`                    |
| mycroft.gui.screen.close                | "skill_id": str | Signal that the skill is no longer using the GUI.         |                         | `release`                        |

## IntentLayers

Typically used in skills, TODO move to ovos-workshop

### Emits

| Message Type                   | Message Data       | Description                  | Trigger Message Type | Handled By       |
|--------------------------------|--------------------|------------------------------|----------------------|------------------|
| `mycroft.skill.disable_intent` | "intent_name": str | Disable a registered intent  |                      | `disable_intent` |
| `mycroft.skill.enable_intent`  | "intent_name": str | Reenable a registered intent |                      | `enable_intent`  |

## EnclosureAPI

Typically used in skills, utility to interact with enclosure (usually a mark1 faceplate)

### Emits

| Message Type                        | Message Data                                                                                                   | Description                                         | Trigger Message Type | Handled by                |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|----------------------|---------------------------|
| `enclosure.active_skill`            | "skill_id": str                                                                                                | Registers a skill as active.                        |                      | `register`                |
| `enclosure.reset`                   |                                                                                                                | Restores the enclosure to a started state.          |                      | `reset`                   |
| `enclosure.system.reset`            |                                                                                                                | Resets the enclosure hardware (CPUs, etc.).         |                      | `system_reset`            |
| `enclosure.system.mute`             |                                                                                                                | Mutes (turns off) the system speaker.               |                      | `system_mute`             |
| `enclosure.system.unmute`           |                                                                                                                | Unmutes (turns on) the system speaker.              |                      | `system_unmute`           |
| `enclosure.system.blink`            | "times": int                                                                                                   | Makes the 'eyes' blink the given number of times.   |                      | `system_blink`            |
| `enclosure.eyes.on`                 |                                                                                                                | Illuminates or shows the eyes.                      |                      | `eyes_on`                 |
| `enclosure.eyes.off`                |                                                                                                                | Turns off or hides the eyes.                        |                      | `eyes_off`                |
| `enclosure.eyes.blink`              | "side": str                                                                                                    | Makes the eyes blink on the specified side(s).      |                      | `eyes_blink`              |
| `enclosure.eyes.narrow`             |                                                                                                                | Makes the eyes look narrow, like a squint.          |                      | `eyes_narrow`             |
| `enclosure.eyes.look`               | "side": str                                                                                                    | Makes the eyes look to the given side.              |                      | `eyes_look`               |
| `enclosure.eyes.color`              | "r": r<br>"g": g<br>"b": b                                                                                     | Changes the eye color to the given RGB values.      |                      | `eyes_color`              |
| `enclosure.eyes.setpixel`           | "idx": idx <br> "r": r<br>"g": g<br>"b": b                                                                     | Sets individual pixels of the Mark 1 neopixel eyes. |                      | `eyes_setpixel`           |
| `enclosure.eyes.fill`               | "percentage": percentage                                                                                       | Uses the eyes as a progress meter.                  |                      | `eyes_fill`               |
| `enclosure.eyes.level`              | "level": level                                                                                                 | Sets the brightness of the eyes in the display.     |                      | `eyes_brightness`         |
| `enclosure.eyes.reset`              |                                                                                                                | Restores the eyes to their default (ready) state.   |                      | `eyes_reset`              |
| `enclosure.eyes.spin`               |                                                                                                                | Makes the eyes 'roll'.                              |                      | `eyes_spin`               |
| `enclosure.eyes.timedspin`          | "length": length                                                                                               | Makes the eyes 'roll' for the given time.           |                      | `eyes_timed_spin`         |
| `enclosure.eyes.volume`             | "volume": volume                                                                                               | Indicates the volume using the eyes.                |                      | `eyes_volume`             |
| `enclosure.mouth.reset`             |                                                                                                                | Restores the mouth display to normal (blank).       |                      | `mouth_reset`             |
| `enclosure.mouth.talk`              |                                                                                                                | Shows a generic 'talking' animation.                |                      | `mouth_talk`              |
| `enclosure.mouth.think`             |                                                                                                                | Shows a 'thinking' image or animation.              |                      | `mouth_think`             |
| `enclosure.mouth.listen`            |                                                                                                                | Shows a 'thinking' image or animation.              |                      | `mouth_listen`            |
| `enclosure.mouth.smile`             |                                                                                                                | Shows a 'smile' image or animation.                 |                      | `mouth_smile`             |
| `enclosure.mouth.viseme_list`       | "start": start<br>"visemes": List                                                                              | Sends mouth visemes as a list in a single message.  |                      | `mouth_viseme`            |
| `enclosure.mouth.text`              | "text": str                                                                                                    | Displays text (scrolling as needed).                |                      | `mouth_text`              |
| `enclosure.mouth.display`           | "img_code": "img_code"<br>"xOffset": x<br>"yOffset": y<br>"clearPrev": refresh                                 | Displays images on the faceplate.                   |                      | `mouth_display`           |
| `enclosure.mouth.display_image`     | "img_path": "image_absolute_path"<br>"xOffset": x<br>"yOffset": y,<br>"invert": invert<br>"clearPrev": refresh | Sends an image to the enclosure.                    |                      | `mouth_display_png`       |
| `enclosure.weather.display`         | "img_code": str<br>"temp": temp                                                                                | Shows the temperature and a weather icon.           |                      | `weather_display`         |
| `enclosure.mouth.events.activate`   |                                                                                                                | Enables movement of the mouth with speech.          |                      | `activate_mouth_events`   |
| `enclosure.mouth.events.deactivate` |                                                                                                                | Disables movement of the mouth with speech.         |                      | `deactivate_mouth_events` |
| `enclosure.eyes.rgb.get`            |                                                                                                                | Gets the eye RGB color for all pixels.              | `enclosure.eyes.rgb` | `get_eyes_color`          |

## ProcessStatus

Utility used across OVOS standalone components to report their status, integrates with sdnotify

# Listens to

| Message Type                                       | Message Data | Description                                  | Emitted Response Type                                     | Handled by  |
|----------------------------------------------------|--------------|----------------------------------------------|-----------------------------------------------------------|-------------|
| `{self._namespace}.{self.name}.service.is_alive`   |              | Check if the service is alive                | `{self._namespace}.{self.name}.service.is_alive.response` | check_alive |
| `{self._namespace}.{self.name}.service.is_ready`   |              | Check if the service is ready                | `{self._namespace}.{self.name}.service.is_ready.response` | check_ready |
| `{self._namespace}.{self.name}.service.all_loaded` |              | DEPRECATED: Check if all services are loaded | `{self._namespace}.{self.name}.service.is_ready.response` | check_ready |

# Emits

| Message Type                                              | Message Data         | Description                        | Trigger Message Type                                                                                   | Handled by  |
|-----------------------------------------------------------|----------------------|------------------------------------|--------------------------------------------------------------------------------------------------------|-------------|
| `{self._namespace}.{self.name}.service.is_alive.response` | {'status': is_alive} | Respond to is_alive status request | `{self._namespace}.{self.name}.service.is_alive`                                                       | check_alive |
| `{self._namespace}.{self.name}.service.is_ready.response` | {'status': is_ready} | Respond to is_ready status request | `{self._namespace}.{self.name}.service.is_ready`<br>`{self._namespace}.{self.name}.service.all_loaded` | check_ready |

