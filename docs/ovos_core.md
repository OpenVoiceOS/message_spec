# skill_manager.py

| Message Type                    | Message Data                                        | Description                                        | Response Type(s)                   |
|---------------------------------|-----------------------------------------------------|----------------------------------------------------|------------------------------------|
| `ovos.skills.settings_changed`  | {"skill_id": string}                                | Notifies a change in skill settings.json           |                                    |
| `ovos.setup.state.get`          |                                                     | Requests the setup state from the ovos-setup skill | `ovos.setup.state`                 |
| `mycroft.skills.list`           | {"<skill_id>": {"active": bool, "id": string}, ...} | Provides a list of loaded skills                   |                                    |
| `mycroft.skills.error`          | {"internet_loaded": bool, "network_loaded": bool}   | Indicates an error in skill loading status         |                                    |
| `mycroft.skills.initialized`    |                                                     | Indicates that skills have been initialized        |                                    |
| `mycroft.internet.connected`    |                                                     | Indicates that the internet is connected           |                                    |
| `mycroft.network.connected`     |                                                     | Indicates that the network is connected            |                                    |
| `mycroft.gui.available `        | {"permanent": bool}                                 | Indicates that the GUI is available                |                                    |
| `mycroft.internet.disconnected` |                                                     | Indicates that the internet is disconnected        |                                    |
| `mycroft.network.disconnected`  |                                                     | Indicates that the network is disconnected         |                                    |
| `mycroft.gui.unavailable`       |                                                     | Indicates that the GUI is unavailable              |                                    |
| `mycroft.ready`                 |                                                     | Signals that Mycroft is ready                      |                                    |
| `mycroft.skills.trained`        |                                                     | Indicates that skills have been trained            |                                    |
| `ovos.setup.finished`           |                                                     | Indicates the completion of the setup process      |                                    |
| `skillmanager.activate`         | {"skill_id": string}                                | Loads a skill, if it is available                  | `skillmanager.activate.response`   |
| `skillmanager.deactivate`       | {"skill_id": string}                                | Unloads a skill, if it is loaded                   | `skillmanager.deactivate.response` |
| `skillmanager.keep`             | {"skill_id": string}                                | Unloads all skills but the provided                |                                    |
| `skillmanager.list`             |                                                     | Returns a list of all loaded skills                | `mycroft.skills.list`              |

# skill_installer.py

| Message Type            | Message Data       | Description                           | Response Type(s)                                           |
|-------------------------|--------------------|---------------------------------------|------------------------------------------------------------|
| `ovos.skills.install`   | {"url": str}       | Installs a skill from a GitHub URL.   | `ovos.skills.install.complete, ovos.skills.install.failed` |
| `ovos.skills.uninstall` |                    | Uninstalls a skill.                   | `ovos.skills.uninstall.failed`                             |
| `ovos.pip.install`      | {"packages": list} | Installs Python packages using pip.   | `ovos.pip.install.complete, ovos.pip.install.failed`       |
| `ovos.pip.uninstall`    | {"packages": list} | Uninstalls Python packages using pip. | `ovos.pip.uninstall.complete, ovos.pip.uninstall.failed`   |

# intent_services/__init__.py

| Message Type                                     | Message Data                                                                | Description                                                                | Response Type(s)                             |
|--------------------------------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------|----------------------------------------------|
| `register_vocab`                                 | {entity_value: str, entity_type: str, regex: str, alias_of: str, lang: str} | Register vocabulary for the Adapt intent service                           |                                              |
| `register_intent`                                | {intent_type: str, ...}                                                     | Register an intent for the Adapt intent service                            |                                              |
| `detach_intent`                                  | {intent_name: str}                                                          | Remove a registered intent from the intent service                         |                                              |
| `detach_skill`                                   | {skill_id: str}                                                             | Remove all intents registered for a specific skill from the intent service |                                              |
| `add_context`                                    | {context: str, word: str, origin: str}                                      | Add context to the session context manager                                 |                                              |
| `remove_context`                                 | {context: str}                                                              | Remove specific context from the session context manager                   |                                              |
| `clear_context`                                  |                                                                             | Clear all keywords from the session context manager                        |                                              |
| `intent.service.intent.get`                      | {utterance: str}                                                            | Get intent information for a given utterance                               | `intent.service.intent.reply`                |
| `intent.service.skills.get`                      |                                                                             | Get a list of registered skills                                            | `intent.service.skills.reply`                |
| `intent.service.adapt.get`                       | {utterance: str}                                                            | Get Adapt intent information for a given utterance                         | `intent.service.adapt.reply`                 |
| `intent.service.adapt.manifest.get`              |                                                                             | Get the manifest of registered Adapt intents                               | `intent.service.adapt.manifest`              |
| `intent.service.adapt.vocab.manifest.get`        |                                                                             | Get the manifest of registered Adapt vocabulary                            | `intent.service.adapt.vocab.manifest`        |
| `intent.service.padatious.get`                   | {utterance: str, norm_utt: str}                                             | Get Padatious intent information for a given utterance                     | `intent.service.padatious.reply`             |
| `intent.service.padatious.manifest.get`          |                                                                             | Get the manifest of registered Padatious intents                           | `intent.service.padatious.manifest`          |
| `intent.service.padatious.entities.manifest.get` |                                                                             | Get the manifest of registered Padatious entities                          | `intent.service.padatious.entities.manifest` |

# commonqa_service.py

| Message Type              | Message Data                                                                                             | Description                                                                   | Response Type(s)                                    |
|---------------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|-----------------------------------------------------|
| `question:query`          | {'phrase': str}                                                                                          | Initiates a common query for a specific phrase.                               | `question:query.response`, `question:query.timeout` |
| `common_query.question`   | {'utterance': str}                                                                                       | Handles common query questions and initiates searches.                        | `question:query`                                    |
| `question:query.response` | {'phrase': str, 'skill_id': str, 'searching': bool, 'answer': str, 'conf': float, 'callback_data': dict} | Provides a response to a common query with search information and the answer. |                                                     |
| `question:query.timeout`  | {'phrase': str, 'skill_id': str}                                                                         | Indicates that a common query has timed out with no response.                 |                                                     |

# converse_service.py

| Message Type                         | Message Data                                       | Description                                                | Response Type(s)                     |
|--------------------------------------|----------------------------------------------------|------------------------------------------------------------|--------------------------------------|
| `mycroft.speech.recognition.unknown` |                                                    | Reset the conversation when speech recognition is unknown. |                                      |
| `intent.service.skills.deactivate`   | {"skill_id": str}                                  | Deactivate a skill.                                        | `intent.service.skills.deactivated`  |
| `intent.service.skills.activate`     | {"skill_id": str}                                  | Activate a skill.                                          | `intent.service.skills.activated`    |
| `active_skill_request`               |                                                    | Activate a skill (backward compatibility).                 | `intent.service.skills.activated`    |
| `intent.service.active_skills.get`   |                                                    | Request a list of active skills.                           | `intent.service.active_skills.reply` |
| `skill.converse.ping`                |                                                    | Ping all skills to check if they want to converse.         | `skill.converse.pong`                |
| `skill.converse.pong`                | {"skill_id": str, "can_handle": bool}              | Acknowledge skill's ability to handle conversation.        |                                      |
| `skill.converse.request`             | {"skill_id": str, "utterances": list, "lang": str} | Request a skill to handle a conversation.                  | `skill.converse.response`            |
| `skill.converse.response`            | {"result": bool, "error": str}                     | Response from a skill about handling a conversation.       |                                      |
| `intent.service.skills.deactivated`  | {"skill_id": str}                                  | Notification that a skill has been deactivated.            |                                      |
| `intent.service.skills.activated`    | {"skill_id": str}                                  | Notification that a skill has been activated.              |                                      |
| `intent.service.active_skills.reply` | {"skills": list}                                   | Reply to a request for a list of active skills.            |                                      |

# fallback_service.py

| Message Type                               | Message Data                                                         | Description                                                                                      | Response Type(s)                           |
|--------------------------------------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------|
| `ovos.skills.fallback.register`            | {"skill_id": str, "priority": int}                                   | Registers a skill for fallback handling with an optional priority level.                         |                                            |
| `ovos.skills.fallback.deregister`          | {"skill_id": str}                                                    | Deregisters a skill from fallback handling.                                                      |                                            |
| `ovos.skills.fallback.ping`                | {"skill_id": str, ...}                                               | Requests skills to acknowledge their willingness to handle fallback for a specific skill.        | `ovos.skills.fallback.pong`                |
| `ovos.skills.fallback.pong`                | {"skill_id": str, "can_handle": bool, ...}                           | Acknowledges a skill's willingness to handle fallback and whether it can handle it.              |                                            |
| `ovos.skills.fallback.{skill_id}.request`  | {"skill_id": str, "utterances": list, "utterance": str, "lang": str} | Requests a specific skill to attempt fallback handling for the given utterances and language.    | `ovos.skills.fallback.{skill_id}.response` |
| `ovos.skills.fallback.{skill_id}.response` | {"result": bool, "error": str, ...}                                  | Indicates the result of the specific skill's fallback handling attempt and any potential errors. |                                            |
| `mycroft.skills.fallback`                  | {"utterance": str, "lang": str, "fallback_range": tuple}             | Deprecated message for fallback handling by a legacy fallback skill singleton class.             |                                            |

# padacioso_service.py

| Message Type                | Message Data                                                                                                                                                                                                      | Description                                                | Response Type(s) |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|------------------|
| `padatious:register_intent` | - `name` (str): Name of intent<br>- `file_name` (str, optional): File containing intent samples<br>- `samples` (List[str], optional): List of intent samples<br>- `lang` (str, optional): Language for the intent | Register a new intent with Padacioso.                      |                  |
| `padatious:register_entity` | - `name` (str): Name of entity<br>- `file_name` (str, optional): File containing entity samples<br>- `samples` (List[str], optional): List of entity samples<br>- `lang` (str, optional): Language for the entity | Register a new entity with Padacioso.                      |                  |
| `detach_intent`             | - `intent_name` (str): Name of the intent to detach                                                                                                                                                               | Detach a specific intent from Padacioso.                   |                  |
| `detach_skill`              | - `skill_id` (str): Skill identifier                                                                                                                                                                              | Detach all intents associated with a skill from Padacioso. |                  |

# padatious_service.py

| Message Type                 | Message Data                                                       | Description                                                       | Response Type(s)         |
|------------------------------|--------------------------------------------------------------------|-------------------------------------------------------------------|--------------------------|
| `padatious:register_intent`  | {'name': str, 'file_name': str, 'samples': List[str], 'lang': str} | Register an intent with Padatious for intent recognition.         |                          |
| `padatious:register_entity`  | {'name': str, 'file_name': str, 'samples': List[str], 'lang': str} | Register an entity with Padatious for entity recognition.         |                          |
| `detach_intent`              | {'intent_name': str}                                               | Remove a registered intent from Padatious.                        |                          |
| `detach_skill`               | {'skill_id': str}                                                  | Remove all intents registered by a specific skill from Padatious. |                          |
| `mycroft.skills.initialized` |                                                                    | Triggered when skills are initialized, used to initiate training. | `mycroft.skills.trained` |
| `mycroft.skills.trained`     |                                                                    | Indicates that skills have been trained.                          |                          |

