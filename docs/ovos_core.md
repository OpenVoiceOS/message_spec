# ovos-core

## SkillManager

### Listens to

| Message Type                    | Message Data      | Description                                        | Response Type(s)                   |
|---------------------------------|-------------------|----------------------------------------------------|------------------------------------|
| `ovos.setup.state.get`          |                   | Requests the setup state from the ovos-setup skill | `ovos.setup.state`                 |
| `mycroft.internet.connected`    |                   | Indicates that the internet is connected           |                                    |
| `mycroft.network.connected`     |                   | Indicates that the network is connected            |                                    |
| `mycroft.gui.available`         | "permanent": bool | Indicates that the GUI is available                |                                    |
| `mycroft.internet.disconnected` |                   | Indicates that the internet is disconnected        |                                    |
| `mycroft.network.disconnected`  |                   | Indicates that the network is disconnected         |                                    |
| `mycroft.gui.unavailable`       |                   | Indicates that the GUI is unavailable              |                                    |
| `mycroft.skills.trained`        |                   | Indicates that skill intents have been trained     |                                    |
| `ovos.setup.finished`           |                   | Indicates the completion of the setup process      |                                    |
| `skillmanager.activate`         | "skill_id": str   | Loads a skill, if it is available                  | `skillmanager.activate.response`   |
| `skillmanager.deactivate`       | "skill_id": str   | Unloads a skill, if it is loaded                   | `skillmanager.deactivate.response` |
| `skillmanager.keep`             | "skill_id": str   | Unloads all skills but the provided                |                                    |
| `skillmanager.list`             |                   | Returns a list of all loaded skills                | `mycroft.skills.list`              |

### Emits

| Message Type                   | Message Data                                      | Description                                                                     | In Response to / sent by           |
|--------------------------------|---------------------------------------------------|---------------------------------------------------------------------------------|------------------------------------|
| `ovos.skills.settings_changed` | "skill_id": str                                   | Notifies a change in skill settings.json                                        | self._handle_settings_file_change  |
| `mycroft.skills.list`          | List["<skill_id>": "active": bool, "id": string]  | Provides a list of loaded skills                                                | `skillmanager.list`                |
| `mycroft.skills.error`         | "internet_loaded": bool<br>"network_loaded": bool | Indicates an error waiting for internet skills to load at startup               | self.run                           |
| `mycroft.skills.initialized`   |                                                   | Indicates that skills have been initialized                                     |                                    |
| `mycroft.internet.connected`   |                                                   | when ovos-phal-plugin-connectivity-events missing perform direct network checks |                                    |
| `mycroft.network.connected`    |                                                   | when ovos-phal-plugin-connectivity-events missing perform direct network checks |                                    |
| `mycroft.ready`                |                                                   | Signals that Mycroft is ready                                                   | self.handle_check_device_readiness |

## SkillsStore

### Listens to

| Message Type            | Message Data     | Description                           | Response Type(s)                                           |
|-------------------------|------------------|---------------------------------------|------------------------------------------------------------|
| `ovos.skills.install`   | "url": str       | Installs a skill from a GitHub URL.   | `ovos.skills.install.complete, ovos.skills.install.failed` |
| `ovos.skills.uninstall` |                  | Uninstalls a skill.                   | `ovos.skills.uninstall.failed`                             |
| `ovos.pip.install`      | "packages": list | Installs Python packages using pip.   | `ovos.pip.install.complete, ovos.pip.install.failed`       |
| `ovos.pip.uninstall`    | "packages": list | Uninstalls Python packages using pip. | `ovos.pip.uninstall.complete, ovos.pip.uninstall.failed`   |

### Emits

| Message Type                         | Message Data | Description                                     | In Response to / sent by                         |
|--------------------------------------|--------------|-------------------------------------------------|--------------------------------------------------|
| `mycroft.audio.play_sound`           | "uri": str   | play sounds via ovos-audio                      | self.play_error_sound<br>self.play_success_sound |
| `ovos.skills.install.failed`         | "error": str | signal that installation failed                 | self.handle_install_skill                        |
| `ovos.skills.install.complete`       |              | signal that installation was successful         | self.handle_install_skill                        |
| `ovos.skills.uninstall.failed`       | "error": str | signal that skill uninstallation failed         | self.handle_uninstall_skill                      |
| `ovos.skills.uninstall.complete`     |              | signal that skill uninstallation was successful | self.handle_uninstall_skill                      |
| `ovos.skills.pip.install.failed`     | "error": str | signal that pypi installation failed            | self.handle_install_python                       |
| `ovos.skills.pip.install.complete`   |              | signal that pypi installation was successful    | self.handle_install_python                       |
| `ovos.skills.pip.uninstall.failed`   | "error": str | signal that pypi uninstallation failed          | self.handle_uninstall_python                     |
| `ovos.skills.pip.uninstall.complete` |              | signal that pypi uninstallation was successful  | self.handle_uninstall_python                     |

## IntentService

### Listens to

| Message Type                                     | Message Data                                                                      | Description                                                                | Response Type(s)                             |
|--------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------|----------------------------------------------|
| `recognizer_loop:utterance`                      | utterances: list<br> lang: str                                                    | Handle a natural language question from the user                           |                                              |
| `register_vocab`                                 | entity_value: str<br>entity_type: str<br>regex: str<br>alias_of: str<br>lang: str | Register vocabulary for the Adapt intent service                           |                                              |
| `register_intent`                                | intent_type: str                                                                  | Register an intent for the Adapt intent service                            |                                              |
| `detach_intent`                                  | intent_name: str                                                                  | Remove a registered intent from the intent service                         |                                              |
| `detach_skill`                                   | skill_id: str                                                                     | Remove all intents registered for a specific skill from the intent service |                                              |
| `add_context`                                    | context: str<br> word: str<br>origin: str                                         | Add context to the session context manager                                 |                                              |
| `remove_context`                                 | context: str                                                                      | Remove specific context from the session context manager                   |                                              |
| `clear_context`                                  |                                                                                   | Clear all keywords from the session context manager                        |                                              |
| `intent.service.intent.get`                      | utterance: str                                                                    | DEPRECATED: Get intent information for a given utterance                   | `intent.service.intent.reply`                |
| `intent.service.skills.get`                      |                                                                                   | DEPRECATED: Get a list of registered skills                                | `intent.service.skills.reply`                |
| `intent.service.adapt.get`                       | utterance: str                                                                    | DEPRECATED: Get Adapt intent information for a given utterance             | `intent.service.adapt.reply`                 |
| `intent.service.adapt.manifest.get`              |                                                                                   | DEPRECATED: Get the manifest of registered Adapt intents                   | `intent.service.adapt.manifest`              |
| `intent.service.adapt.vocab.manifest.get`        |                                                                                   | DEPRECATED: Get the manifest of registered Adapt vocabulary                | `intent.service.adapt.vocab.manifest`        |
| `intent.service.padatious.get`                   | utterance: str<br> norm_utt: str                                                  | DEPRECATED: Get Padatious intent information for a given utterance         | `intent.service.padatious.reply`             |
| `intent.service.padatious.manifest.get`          |                                                                                   | DEPRECATED: Get the manifest of registered Padatious intents               | `intent.service.padatious.manifest`          |
| `intent.service.padatious.entities.manifest.get` |                                                                                   | DEPRECATED: Get the manifest of registered Padatious entities              | `intent.service.padatious.entities.manifest` |

### Emits

Selected intents have their own messages that can not be listed here

| Message Type                                 | Message Data     | Description                                                          | In Response to / sent by                         |
|----------------------------------------------|------------------|----------------------------------------------------------------------|--------------------------------------------------|
| each intent has it's own message_type        |                  | Trigger selected intent                                              | `recognizer_loop:utterance`                      |
| `mycroft.audio.play_sound`                   | "uri": str       | Play error sound                                                     | self.send_complete_intent_failure                |
| `complete_intent_failure`                    |                  | signal we failed to handle an utterance                              | self.send_complete_intent_failure                |
| `intent.service.intent.reply`                | "intent": dict   | DEPRECATED: get intent that would match, excluding converse/fallback | `intent.service.intent.get`                      |
| `intent.service.skills.reply`                | "skills": list   | DEPRECATED: send list of skills with registered intents              | `intent.service.skills.get`                      |
| `intent.service.adapt.reply`                 | "intent": dict   | DEPRECATED: get intent that would match with adapt                   | `intent.service.adapt.get`                       |
| `intent.service.adapt.manifest`              | "intents": list  | DEPRECATED: get list of registered adapt intents                     | `intent.service.adapt.manifest.get`              |
| `intent.service.adapt.vocab.manifest`        | "vocab": list    | DEPRECATED: get list of registered adapt keywords                    | `intent.service.adapt.vocab.manifest.get`        |
| `intent.service.padatious.reply`             | "intent": dict   | DEPRECATED: get intent that would match with padatious               | `intent.service.padatious.get`                   |
| `intent.service.padatious.manifest`          | "intents": list  | DEPRECATED: get list of registered padatious intents                 | `intent.service.padatious.manifest.get`          |
| `intent.service.padatious.entities.manifest` | "entities": list | DEPRECATED: get list of registered padatious entities                | `intent.service.padatious.entities.manifest.get` |

## CommonQAService

### Listens to

| Message Type              | Message Data                                                                                                      | Description                                                                   | Response Type(s) |
|---------------------------|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|------------------|
| `common_query.question`   | 'utterance': str                                                                                                  | Handles common query questions and initiates searches.                        | `question:query` |
| `question:query.response` | 'phrase': str<br> 'skill_id': str<br>'searching': bool<br>'answer': str<br>'conf': float<br>'callback_data': dict | Provides a response to a common query with search information and the answer. |                  |

### Emits

| Message Type             | Message Data                                              | Description                                         | sent by                    |
|--------------------------|-----------------------------------------------------------|-----------------------------------------------------|----------------------------|
| `question:query`         | 'phrase': str                                             | Initiates a common query for a specific phrase.     | self.handle_question       |
| `question:action`        | 'phrase': str<br>'skill_id': str<br>'callback_data': dict | Trigger skill callback after answer was selected    | self._query_timeout        |
| `question:query.timeout` | 'phrase': str<br>'skill_id': str                          | Tell common_qa skills to stop searching             | self.handle_query_response |
| `speak`                  | 'utterance': str                                          | DEPRECATED: speak is now done by the selected skill | self._query_timeout        |

## ConverseService

### Listens to

| Message Type                          | Message Data                          | Description                                            | Response Type(s)                     |
|---------------------------------------|---------------------------------------|--------------------------------------------------------|--------------------------------------|
| `mycroft.speech.recognition.unknown`  |                                       | Reset converse when speech recognition is unknown.     |                                      |
| `intent.service.skills.deactivate`    | "skill_id": str                       | Deactivate a skill.                                    | `intent.service.skills.deactivated`  |
| `intent.service.skills.activate`      | "skill_id": str                       | Activate a skill.                                      | `intent.service.skills.activated`    |
| `intent.service.active_skills.get`    |                                       | Request a list of active skills.                       | `intent.service.active_skills.reply` |
| `skill.converse.get_response.enable`  | "skill_id": str                       | Enable get_response mode for skill_id                  |                                      |
| `skill.converse.get_response.disable` | "skill_id": str                       | Disable get_response mode for skill_id                 |                                      |
| `skill.converse.pong`                 | "skill_id": str<br>"can_handle": bool | Acknowledge skill's ability to handle conversation.    |                                      |
| `skill.converse.response`             | "result": bool, "error": str          | Response from a skill about handling a conversation.   |                                      |
| `active_skill_request`                | "skill_id": str                       | DEPRECATED: Activate a skill (backward compatibility). | `intent.service.skills.activated`    |

### Emits

| Message Type                         | Message Data                                           | Description                                        | In Response to / sent by           |
|--------------------------------------|--------------------------------------------------------|----------------------------------------------------|------------------------------------|
| `skill.converse.ping`                |                                                        | Ping all skills to check if they want to converse. | `skill.converse.pong`              |
| `skill.converse.request`             | "skill_id": str<br> "utterances": list<br> "lang": str | Request a skill to handle a conversation.          | `skill.converse.response`          |
| `intent.service.skills.deactivated`  | "skill_id": str                                        | Notification that a skill has been deactivated.    | `intent.service.skills.deactivate` |
| `intent.service.skills.activated`    | "skill_id": str                                        | Notification that a skill has been activated.      | `intent.service.skills.activate`   |
| `intent.service.active_skills.reply` | "skills": list                                         | Reply to a request for a list of active skills.    | `intent.service.active_skills.get` |
| `{skill_id}.converse.get_response`   | "utterances": list<br> "lang": str                     | send get_response answer for skill_id to handle    | self.converse                      |
| `{skill_id}.converse.request`        | "utterances": list<br> "lang": str                     | send utterance for skill_id to converse            | self.converse                      |

## FallbackService

### Listens to

| Message Type                               | Message Data                           | Description                                                                                      | Response Type(s) |
|--------------------------------------------|----------------------------------------|--------------------------------------------------------------------------------------------------|------------------|
| `ovos.skills.fallback.register`            | "skill_id": str<br> "priority": int    | Registers a skill for fallback handling with an optional priority level.                         |                  |
| `ovos.skills.fallback.deregister`          | "skill_id": str                        | Deregisters a skill from fallback handling.                                                      |                  |
| `ovos.skills.fallback.{skill_id}.response` | "result": bool<br> "error": str        | Indicates the result of the specific skill's fallback handling attempt and any potential errors. |                  |
| `ovos.skills.fallback.pong`                | "skill_id": str<br> "can_handle": bool | Acknowledges a skill's willingness to handle fallback and whether it can handle it.              |                  |

### Emits

| Message Type                              | Message Data                                                 | Description                                                                                   | Sent by                       |
|-------------------------------------------|--------------------------------------------------------------|-----------------------------------------------------------------------------------------------|-------------------------------|
| `ovos.skills.fallback.ping`               | "skill_id": str                                              | Requests skills to acknowledge their willingness to handle fallback for a specific skill.     | self._collect_fallback_skills |
| `ovos.skills.fallback.{skill_id}.request` | "skill_id": str<br> "utterance": str<br> "lang": str         | Requests a specific skill to attempt fallback handling for the given utterances and language. | self.attempt_fallback         |
| `mycroft.skills.fallback`                 | "utterance": str<br> "lang": str<br> "fallback_range": tuple | DEPRECATED fallback handling by a legacy fallback skill singleton class.                      |                               |

## PadaciosoService

### Listens to

| Message Type                | Message Data                                                            | Description                                                | Response Type(s) |
|-----------------------------|-------------------------------------------------------------------------|------------------------------------------------------------|------------------|
| `padatious:register_intent` | 'name': str<br>'file_name': str<br> 'samples': List[str]<br>'lang': str | Register a new intent with Padacioso.                      |                  |
| `padatious:register_entity` | 'name': str<br>'file_name': str<br> 'samples': List[str]<br>'lang': str | Register a new entity with Padacioso.                      |                  |
| `detach_intent`             | 'intent_name': str                                                      | Detach a specific intent from Padacioso.                   |                  |
| `detach_skill`              | 'skill_id': str                                                         | Detach all intents associated with a skill from Padacioso. |                  |

## PadatiousService

### Listens to

| Message Type                 | Message Data                                                              | Description                                                       | Response Type(s)         |
|------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------|--------------------------|
| `padatious:register_intent`  | 'name': str<br> 'file_name': str<br> 'samples': List[str]<br> 'lang': str | Register an intent with Padatious for intent recognition.         |                          |
| `padatious:register_entity`  | 'name': str<br>'file_name': str<br> 'samples': List[str]<br>'lang': str   | Register an entity with Padatious for entity recognition.         |                          |
| `detach_intent`              | 'intent_name': str                                                        | Remove a registered intent from Padatious.                        |                          |
| `detach_skill`               | 'skill_id': str                                                           | Remove all intents registered by a specific skill from Padatious. |                          |
| `mycroft.skills.initialized` |                                                                           | Triggered when skills are initialized, used to initiate training. | `mycroft.skills.trained` |

### Emits

| Message Type             | Message Data | Description                                           | In Response to / sent by     |
|--------------------------|--------------|-------------------------------------------------------|------------------------------|
| `mycroft.skills.trained` |              | Indicates that intents classifiers have been trained. | `mycroft.skills.initialized` |
