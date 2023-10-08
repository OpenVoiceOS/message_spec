# skill_manager.py

| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| ovos.skills.settings_changed     | {"skill_id": string}               | Notifies a change in skill settings.json   | None                                   |
| ovos.setup.state.get             |                                    | Requests the setup state from the ovos-setup skill | ovos.setup.state|
| mycroft.skills.list              | {"<skill_id>": {"active": bool, "id": string}, ...} | Provides a list of loaded skills  | None                           |
| mycroft.skills.error             | {"internet_loaded": bool, "network_loaded": bool} | Indicates an error in skill loading status | None                    |
| mycroft.skills.initialized       | None                               | Indicates that skills have been initialized | None                                  |
| mycroft.internet.connected       | None                               | Indicates that the internet is connected    | None                                  |
| mycroft.network.connected        | None                               | Indicates that the network is connected     | None                                  |
| mycroft.gui.available            | {"permanent": bool}                | Indicates that the GUI is available         | None                                  |
| mycroft.internet.disconnected    | None                               | Indicates that the internet is disconnected | None                                  |
| mycroft.network.disconnected     | None                               | Indicates that the network is disconnected  | None                                  |
| mycroft.gui.unavailable          | None                               | Indicates that the GUI is unavailable       | None                                  |
| mycroft.ready                    | None                               | Signals that Mycroft is ready               | None                                  |
| mycroft.skills.trained           | None                               | Indicates that skills have been trained     | None                                  |
| ovos.setup.finished              | None                               | Indicates the completion of the setup process | None                                |
| skillmanager.activate            | {"skill_id": string}               | Activates a skill, if it is available       | skillmanager.activate.response        |
| skillmanager.deactivate          | {"skill_id": string}               | Deactivates a skill, if it is active        | skillmanager.deactivate.response      |
| skillmanager.keep                | {"skill_id": string}               | Deactivates all skills but the provided     | None directly                         |
| skillmanager.list                | None                               | Returns a list of all loaded skills         | mycroft.skills.list                   |

# skill_installer.py

| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| ovos.skills.install              | {"url": str}                       | Installs a skill from a GitHub URL.         | ovos.skills.install.complete, ovos.skills.install.failed |
| ovos.skills.uninstall            | None                | Uninstalls a skill.                         | ovos.skills.uninstall.failed            |
| ovos.pip.install                | {"packages": list}                 | Installs Python packages using pip.         | ovos.pip.install.complete, ovos.pip.install.failed |
| ovos.pip.uninstall              | {"packages": list}                 | Uninstalls Python packages using pip.       | ovos.pip.uninstall.complete, ovos.pip.uninstall.failed |

# intent_services/__init__.py


| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| register_vocab                  | {entity_value: str, entity_type: str, regex: str, alias_of: str, lang: str} | Register vocabulary for the Adapt intent service | N/A |
| register_intent                 | {intent_type: str, ...}            | Register an intent for the Adapt intent service | N/A |
| detach_intent                   | {intent_name: str}                 | Remove a registered intent from the intent service | N/A |
| detach_skill                    | {skill_id: str}                    | Remove all intents registered for a specific skill from the intent service | N/A |
| add_context                     | {context: str, word: str, origin: str} | Add context to the session context manager | N/A |
| remove_context                  | {context: str}                     | Remove specific context from the session context manager | N/A |
| clear_context                   | N/A                                | Clear all keywords from the session context manager | N/A |
| intent.service.intent.get       | {utterance: str}                   | Get intent information for a given utterance | intent.service.intent.reply |
| intent.service.skills.get       | N/A                                | Get a list of registered skills | intent.service.skills.reply |
| intent.service.adapt.get        | {utterance: str}                   | Get Adapt intent information for a given utterance | intent.service.adapt.reply |
| intent.service.adapt.manifest.get | N/A                              | Get the manifest of registered Adapt intents | intent.service.adapt.manifest |
| intent.service.adapt.vocab.manifest.get | N/A                      | Get the manifest of registered Adapt vocabulary | intent.service.adapt.vocab.manifest |
| intent.service.padatious.get    | {utterance: str, norm_utt: str}    | Get Padatious intent information for a given utterance | intent.service.padatious.reply |
| intent.service.padatious.manifest.get | N/A                       | Get the manifest of registered Padatious intents | intent.service.padatious.manifest |
| intent.service.padatious.entities.manifest.get | N/A             | Get the manifest of registered Padatious entities | intent.service.padatious.entities.manifest |



# commonqa_service.py


| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| `question:query`                | `{'phrase': str}`                  | Initiates a common query for a specific phrase. | `question:query.response`, `question:query.timeout` |
| `common_query.question`         | `{'utterance': str}`               | Handles common query questions and initiates searches. | `question:query`                       |
| `question:query.response`       | `{'phrase': str, 'skill_id': str, 'searching': bool, 'answer': str, 'conf': float, 'callback_data': dict}` | Provides a response to a common query with search information and the answer. | N/A                                    |
| `question:query.timeout`        | `{'phrase': str, 'skill_id': str}` | Indicates that a common query has timed out with no response. | N/A                                    |


# converse_service.py

| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| mycroft.speech.recognition.unknown   | None               | Reset the conversation when speech recognition is unknown.  | None                             |
| intent.service.skills.deactivate | {"skill_id": str}  | Deactivate a skill.                         | intent.service.skills.deactivated         |
| intent.service.skills.activate   | {"skill_id": str}  | Activate a skill.                           | intent.service.skills.activated           |
| active_skill_request            | None               | Activate a skill (backward compatibility).   | intent.service.skills.activated           |
| intent.service.active_skills.get | None               | Request a list of active skills.           | intent.service.active_skills.reply        |
| skill.converse.ping             | None               | Ping all skills to check if they want to converse. | skill.converse.pong                       |
| skill.converse.pong             | {"skill_id": str, "can_handle": bool} | Acknowledge skill's ability to handle conversation. | None                             |
| skill.converse.request          | {"skill_id": str, "utterances": list, "lang": str} | Request a skill to handle a conversation. | skill.converse.response                   |
| skill.converse.response         | {"result": bool, "error": str}  | Response from a skill about handling a conversation. | None                             |
| intent.service.skills.deactivated | {"skill_id": str}  | Notification that a skill has been deactivated. | None                             |
| intent.service.skills.activated   | {"skill_id": str}  | Notification that a skill has been activated.   | None                             |
| intent.service.active_skills.reply | {"skills": list}   | Reply to a request for a list of active skills. | None                             |


# fallback_service.py

| Message Type                       | Message Data                                      | Description                                                                                     | Response Type(s)  |
|------------------------------------|--------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------|
| `ovos.skills.fallback.register`    | `{"skill_id": str, "priority": int}`            | Registers a skill for fallback handling with an optional priority level.                        | N/A                |
| `ovos.skills.fallback.deregister`  | `{"skill_id": str}`                              | Deregisters a skill from fallback handling.                                                       | N/A                |
| `ovos.skills.fallback.ping`        | `{"skill_id": str, ...}`                        | Requests skills to acknowledge their willingness to handle fallback for a specific skill.      | `ovos.skills.fallback.pong` |
| `ovos.skills.fallback.pong`        | `{"skill_id": str, "can_handle": bool, ...}`    | Acknowledges a skill's willingness to handle fallback and whether it can handle it.             | N/A                |
| `ovos.skills.fallback.{skill_id}.request` | `{"skill_id": str, "utterances": list, "utterance": str, "lang": str}` | Requests a specific skill to attempt fallback handling for the given utterances and language. | `ovos.skills.fallback.{skill_id}.response` |
| `ovos.skills.fallback.{skill_id}.response` | `{"result": bool, "error": str, ...}`    | Indicates the result of the specific skill's fallback handling attempt and any potential errors.  | N/A                |
| `mycroft.skills.fallback`           | `{"utterance": str, "lang": str, "fallback_range": tuple}` | Deprecated message for fallback handling by a legacy fallback skill singleton class.   | N/A                |


# padacioso_service.py

| Message Type                      | Message Data                   | Description                                               | Response Type(s)         |
|-----------------------------------|--------------------------------|-----------------------------------------------------------|---------------------------|
| `padatious:register_intent`       | - `name` (str): Name of intent<br>- `file_name` (str, optional): File containing intent samples<br>- `samples` (List[str], optional): List of intent samples<br>- `lang` (str, optional): Language for the intent | Register a new intent with Padacioso.                    |                           |
| `padatious:register_entity`       | - `name` (str): Name of entity<br>- `file_name` (str, optional): File containing entity samples<br>- `samples` (List[str], optional): List of entity samples<br>- `lang` (str, optional): Language for the entity | Register a new entity with Padacioso.                    |                           |
| `detach_intent`                   | - `intent_name` (str): Name of the intent to detach      | Detach a specific intent from Padacioso.                 |                           |
| `detach_skill`                    | - `skill_id` (str): Skill identifier                     | Detach all intents associated with a skill from Padacioso. |                           |

# padatious_service.py

| Message Type                    | Message Data                        | Description                                 | Response Type(s)                      |
|---------------------------------|------------------------------------|---------------------------------------------|----------------------------------------|
| `padatious:register_intent`   | `{'name': str, 'file_name': str, 'samples': List[str], 'lang': str}` | Register an intent with Padatious for intent recognition. | None |
| `padatious:register_entity`   | `{'name': str, 'file_name': str, 'samples': List[str], 'lang': str}` | Register an entity with Padatious for entity recognition. | None |
| `detach_intent`              | `{'intent_name': str}`             | Remove a registered intent from Padatious. | None |
| `detach_skill`               | `{'skill_id': str}`                | Remove all intents registered by a specific skill from Padatious. | None |
| `mycroft.skills.initialized`  | None                               | Triggered when skills are initialized, used to initiate training. | `mycroft.skills.trained` (Response message) |
| `mycroft.skills.trained`     | None                               | Indicates that skills have been trained. | None |

