# ovos-workshop message SPEC

- [OVOSSkill](#ovosskill)
- [FallbackSkill](#fallbackskill)
- [OVOSCommonPlaybackSkill](#ovoscommonplaybackskill)
- [CommonQuerySkill](#commonqueryskill)
- [IdleDisplaySkill](#idledisplayskill)
- [SkillLoader](#skillloader)

## OVOSSkill

### Listens to

| Message Type                          | Message Data                                   | Description                                                                   | Emits response                      | handled by                       |
|---------------------------------------|------------------------------------------------|-------------------------------------------------------------------------------|-------------------------------------|----------------------------------|
| `mycroft.stop`                        |                                                | The skill stops everything it is doing                                        | `mycroft.stop.handled`              | self.stop                        |
| `self.skill_id.converse.ping`         |                                                | Informs ConverseService if the skill supports `converse`.                     | `skill.converse.pong`               | self._handle_converse_ack        |
| `self.skill_id.converse.request`      | 'utterances': list<br>'lang': str              | Handles user input with the `converse` method if skill is active              | `skill.converse.response`           | self.converse                    |
| `self.skill_id.activate`              |                                                | Callback when the skill is considered active by the intent service.           |                                     | self.handle_activate             |
| `self.skill_id.deactivate`            |                                                | Callback when the skill is no longer considered active by the intent service. |                                     | self.handle_deactivate           |
| `intent.service.skills.deactivated`   | 'skill_id': str                                | Intent service deactivated a skill.                                           | `self.skill_id.deactivate`          | self._handle_skill_deactivated   |
| `intent.service.skills.activated`     | 'skill_id': str                                | Intent service activated a skill.                                             | `self.skill_id.activate`            | self._handle_skill_activated     |
| `mycroft.skill.enable_intent`         | 'intent_name': str                             | Re-registers a disabled intent (intent_name contains munged skill_id)         |                                     | self.handle_enable_intent        |
| `mycroft.skill.disable_intent`        | 'intent_name': str                             | Disables a registered intent (intent_name contains munged skill_id)           |                                     | self.handle_disable_intent       |
| `mycroft.skill.set_cross_context`     | 'context': str<br>'word': str<br>'origin': str | Sets a skill specific context (with munged skill_id)                          |                                     | self.handle_set_cross_context    |
| `mycroft.skill.remove_cross_context`  | 'context': str                                 | removes skill specific context (with munged skill_id)                         |                                     | self.handle_remove_cross_context |
| `mycroft.skills.settings.changed`     | 'skill_id': dict                               | Update settings if a remote settings change applies to this skill.            |                                     | self.handle_settings_change      |
| `self.skill_id.public_api`            |                                                | Responds with the skill's public API.                                         | `self.skill_id.public_api.response` | self._send_public_api            |
| `self.skill_id.idle`                  |                                                | callback to trigger homescreen provided by this skill                         |                                     | @resting_handler decorator       |
| `mycroft.mark2.collect_idle`          |                                                | responds to ovos-gui letting it know skill provides a homescreen              | `mycroft.mark2.register_idle`       | self._handle_collect_resting     |
| `self.skill_id.converse.get_response` | 'utterances': List<br>'lang': str              | communicates user response (`get_response`) to the skill                      |                                     | self.get_response                |
| `mycroft.skills.abort_question`       |                                                | Force self.get_response to return None immediately                            |                                     | self.get_response                |

### Emits

| Message Type                          | Message Data                                                                     | Effect                                                                                                          | In Response to / sent by            |
|---------------------------------------|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|-------------------------------------|
| `self.skill_id.activate`              |                                                                                  | Emits a message to activate the skill.                                                                          | `intent.service.skills.activated`   |
| `self.skill_id.deactivate`            |                                                                                  | Emits a message to deactivate the skill.                                                                        | `intent.service.skills.deactivated` |
| `intent.service.skills.activate`      | 'skill_id': str                                                                  | Marks the skill as active and pushes it to the top of the active skills list.                                   | self._activate                      |
| `active_skill_request`                | 'skill_id': str                                                                  | (classic core) same as intent.service.skills.activate                                                           | self._activate                      |
| `intent.service.skills.deactivate`    | 'skill_id': str                                                                  | Marks the skill as inactive and removes it from the active skills list.                                         | self._deactivate                    |
| `skill.converse.pong`                 | 'skill_id': str<br>'can_handle': bool                                            | Informs the skills service whether the skill can handle `converse`.                                             | `skill.converse.ping`               |
| `skill.converse.response`             | 'skill_id': str<br>'result': bool                                                | Responds to a `skill.converse.request` with the result of `converse`.                                           | `skill.converse.request`            |
| `skill.converse.get_response.enable`  | "skill_id": self.skill_id                                                        | Enables getting a response from the user during a conversation.                                                 | self.get_response                   |
| `skill.converse.get_response.disable` | "skill_id": self.skill_id                                                        | Disables getting a response from the user during a conversation.                                                | self.get_response                   |
| `mycroft.mic.listen`                  |                                                                                  | Triggers listening for user input.                                                                              | self.speak + self.get_response      |
| `mycroft.skill.set_cross_context`     | 'context': str<br>'word': str<br>'origin': self.skill_id                         | Emits a message to set cross-context data.                                                                      | self.set_cross_skill_context        |
| `mycroft.skill.remove_cross_context`  | 'context': str`                                                                  | Emits a message to remove cross-context data.                                                                   | self.remove_cross_skill_context     |
| `speak`                               | "utterance": str<br>"expect_response": bool<br>"meta": dict<br>"lang": self.lang | Initiates speech synthesis to speak the provided utterance.                                                     | self.speak                          |
| `detach_skill`                        | "skill_id": self.skill_id                                                        | Tell IntentService to remove all intents from this skill                                                        | self.default_shutdown               |
| `{self.skill_id}.public_api.response` | '{method_name}': {'help': str, 'type': str, 'func': str}                         | Reports skill api data                                                                                          | `self.skill_id.public_api`          |
| `mycroft.audio.queue`                 | "uri": str                                                                       | Queue an audio file for playback.                                                                               | self.play_audio                     |
| `mycroft.audio.play_sound`            | "uri": str                                                                       | Play an audio file instantly.                                                                                   | self.play_audio                     |
| `mycroft.stop`                        |                                                                                  | Stop everything skills are doing                                                                                | self.send_stop_signal               |
| `mycroft.audio.speech.stop`           |                                                                                  | Stop the speech synthesis process.                                                                              | self.send_stop_signal               |
| `recognizer_loop:record_stop`         |                                                                                  | Instruct ovos-listener to stop recording.                                                                       | self.send_stop_signal               |
| `mycroft.mic.mute`                    |                                                                                  | DEPRECATED: (classic core only) Mute the microphone, possibly used to stop recording during speech recognition. | self.send_stop_signal               |
| `mycroft.mic.unmute`                  |                                                                                  | DEPRECATED: (classic core only) Unmute the microphone.                                                          | self.send_stop_signal               |
| `mycroft.mark2.register_idle`         | "name": self.resting_name<br>"id": self.skill_id                                 | DEPRECATED: Registers a resting screen for the skill.                                                           | `mycroft.mark2.collect_idle`        |

## FallbackSkill

### Listens to

| Message Type                     | Message Data                     | Description                                                                                        | Response Type(s)                                                                | handled by                                           |
|----------------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|------------------------------------------------------|
| `ovos.skills.fallback.ping`      | "utterances": []<br> "lang": str | Informs the skills service that the FallbackSkill can handle fallbacks.                            | `ovos.skills.fallback.pong`                                                     | self._handle_fallback_ack                            |
| `ovos.skills.fallback.skill_id ` |                                  | Handles a fallback request, calling registered handlers in priority order until one is successful. | `ovos.skills.fallback.skill_id.start`, `ovos.skills.fallback.skill_id.response` | @fallback_handler decorator / self.register_fallback |

### Emits

| Message Type                             | Message Data                               | Description                                                                                                                                           | In Response to                          |
|------------------------------------------|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------|
| `ovos.skills.fallback.register`          | "skill_id": str<br>"priority": int         | Registers the FallbackSkill with the skills service, specifying its skill ID and priority.                                                            | self._register_system_event_handlers    |
| `ovos.skills.fallback.pong`              | "skill_id": str<br>"can_handle": bool      | Informs the skills service whether the FallbackSkill can handle fallbacks for a given set of utterances and language.                                 | `ovos.skills.fallback.ping`             |
| `ovos.skills.fallback.deregister`        | "skill_id": str`                           | Deregisters the FallbackSkill with the skills service.                                                                                                | self.default_shutdown                   |
| `ovos.skills.fallback.skill_id.start`    |                                            | Indicates the start of the fallback handling process for a specific skill.                                                                            | `ovos.skills.fallback.skill_id.request` |
| `ovos.skills.fallback.skill_id.response` | "result": bool<br> "fallback_handler": str | Indicates the result of the fallback handling process for a specific skill, including whether it was successful and the name of the fallback handler. | `ovos.skills.fallback.skill_id.request` |

## OVOSCommonPlaybackSkill

### Listens To

| Message Type                              | Message Data                          | Description                                                        | Response Type(s)                                                           | handled by                    |
|-------------------------------------------|---------------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------|-------------------------------|
| `ovos.common_play.query`                  | "phrase": str<br>"question_type": str | Query skill if it can start playback from the given phrase.        | `ovos.common_play.skill.search_start`, `ovos.common_play.skill.search_end` | @ocp_search decorator         |
| `ovos.common_play.featured_tracks.play`   | "skill_id": str                       | Play featured tracks from a skill with the specified skill_id.     |                                                                            | @ocp_featured_media decorator |
| `ovos.common_play.skills.get`             |                                       | Request information about the skills that support common playback. | `ovos.common_play.announce`                                                | self.__handle_ocp_skills_get  |
| `ovos.common_play.self.skill_id.play`     |                                       | Handle the playback of media.                                      | `ovos.common_play.player.state`                                            | @ocp_play  decorator          |
| `ovos.common_play.self.skill_id.pause`    |                                       | Handle the pause of media playback.                                | `ovos.common_play.player.state`                                            | @ocp_pause decorator          |
| `ovos.common_play.self.skill_id.resume`   |                                       | Handle the resume of media playback.                               | `ovos.common_play.player.state`                                            | @ocp_resume decorator         |
| `ovos.common_play.self.skill_id.next`     |                                       | Handle the request to play the next track.                         |                                                                            | @ocp_next decorator           |
| `ovos.common_play.self.skill_id.previous` |                                       | Handle the request to play the previous track.                     |                                                                            | @ocp_previous decorator       |
| `ovos.common_play.self.skill_id.stop`     |                                       | Handle the stop of media playback.                                 | `ovos.common_play.player.state`                                            | self.stop                     |
| `ovos.common_play.search.stop`            |                                       | Stop a media search.                                               |                                                                            | self.__handle_stop_search     |
| `mycroft.stop`                            |                                       | Stop a media search in response to a global stop                   |                                                                            | self.__handle_stop_search     |

### Emits

| Message Type                          | Message Data                                                                                                        | Description                                                                | In Response to                                                                                                                                                |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ovos.common_play.announce`           | "skill_id": str<br>"skill_name": str<br>"thumbnail": str<br> "media_types": list<br> "featured_tracks": bool        | Announce skill information to the common playback framework.               | `ovos.common_play.skills.get`                                                                                                                                 |
| `ovos.common_play.skill.search_start` | "skill_id": str<br> "skill_name": str<br>"thumbnail": str                                                           | Signal the start of a media search initiated by the skill.                 | `ovos.common_play.query`                                                                                                                                      |
| `ovos.common_play.query.response`     | "phrase": str<br>"skill_id": str<br>"skill_name": str<br>"thumbnail": str<br> "results": list<br> "searching": bool | Respond to a media search query with search results.                       | `ovos.common_play.query`                                                                                                                                      |
| `ovos.common_play.skill.search_end`   | "skill_id": str                                                                                                     | Signal the end of a media search initiated by the skill.                   | `ovos.common_play.query`                                                                                                                                      |
| `ovos.common_play.player.state`       | "state": str                                                                                                        | Signal changes in the media player state (e.g., playing, paused, stopped). | `ovos.common_play.self.skill_id.play`, `ovos.common_play.self.skill_id.pause`, `ovos.common_play.self.skill_id.resume`, `ovos.common_play.self.skill_id.stop` |

## CommonQuerySkill

### Listens to

| Message Type      | Message Data                           | Description                                                | Response Type(s)          | Handled by                  |
|-------------------|----------------------------------------|------------------------------------------------------------|---------------------------|-----------------------------|
| `question:query`  | "phrase": str                          | Handles incoming user queries and attempts to answer them. | `question:query.response` | self.CQS_match_query_phrase |
| `question:action` | "phrase": str<br>"callback_data": dict | Skill selected to answer question callback                 |                           | self.CQS_action             |

### Emits

| Message Type              | Message Data                                                                                   | Description                                    | In Response to   |
|---------------------------|------------------------------------------------------------------------------------------------|------------------------------------------------|------------------|
| `question:query.response` | "phrase": str<br> "skill_id": str<br>"answer": str<br> "callback_data": dict<br> "conf": float | Report id the skill can answer the user query. | `question:query` |

## IdleDisplaySkill

### Listens to

| Message Type                          | Message Data         | Description                                                                    | Response Type(s)       | handled by                          |
|---------------------------------------|----------------------|--------------------------------------------------------------------------------|------------------------|-------------------------------------|
| `mycroft.ready`                       |                      | Shows idle screen when the device is ready for use.                            | `skill.idle.displayed` | self.handle_idle                    |
| `homescreen.manager.activate.display` | "homescreen_id": str | Display this home screen if requested by the Home Screen Manager.              | `skill.idle.displayed` | self.handle_idle                    |
| `homescreen.manager.reload.list`      |                      | Reloads this skill's homescreen entry and sends it to the Home Screen Manager. |                        | self._reload_homescreen_entry       |
| `mycroft.skills.shutdown`             | "id": str            | Removes this homescreen from the Home Screen Manager if requested.             |                        | self._remove_homescreen_on_shutdown |

### Emits

| Message Type                     | Message Data                             | Description                                                           | In Response to                        |
|----------------------------------|------------------------------------------|-----------------------------------------------------------------------|---------------------------------------|
| `skill.idle.displayed`           |                                          | Indicates that the idle display is shown.                             | `homescreen.manager.activate.display` |
| `homescreen.manager.add`         | "class": str<br>"name": str<br>"id": str | Registers this skill's homescreen entry with the Home Screen Manager. | self._register_system_event_handlers  |
| `homescreen.manager.remove`      | "class": str<br>"name": str<br>"id": str | Removes this skill's homescreen entry from the Home Screen Manager.   | `mycroft.skills.shutdown`             |
| `homescreen.manager.reload.list` |                                          | Requests a reload of this skill's homescreen entry.                   | self._register_system_event_handlers  |

## SkillLoader

### Listens to

| Message Type    | Message Data | Description                             |
|-----------------|--------------|-----------------------------------------|
| `mycroft.ready` |              | Event indicating that OVOS is ready. |

### Emits

| Message Type                     | Message Data                              | Description                                          |
|----------------------------------|-------------------------------------------|------------------------------------------------------|
| `mycroft.skills.is_ready`        | "status": bool                            | Checks if the skills service is ready.               |
| `mycroft.skills.loaded`          | "path": str<br> "id": str<br> "name": str | Indicates that a skill has been successfully loaded. |
| `mycroft.skills.loading_failure` | "path": str<br> "id": str                 | Indicates that a skill failed to load.               |
| `mycroft.skills.shutdown`        | "path": str<br> "id": str                 | Notifies that a skill is being shutdown.             |
