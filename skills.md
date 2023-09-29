# base.py

## Listens to
| Message Type                   | Message Data                           | Effect                         | Emits response            |
|--------------------------------|---------------------------------------|--------------------------------------------|--------------------------------------------------------------|
| mycroft.stop                    | N/A                                   | The skill stops everything it is doing                                         | "mycroft.stop.handled"  |
| skill.converse.ping             | N/A                                   | Informs ConverseService if the skill supports `converse`.                      | skill.converse.pong     |
| skill.converse.request          | {'skill_id': str, 'utterances': list, 'lang': str} | Handles user input with the `converse` method if skill_id matches | skill.converse.response |
| {self.skill_id}.activate        | N/A                                   | Callback when the skill is considered active by the intent service.            | N/A |
| {self.skill_id}.deactivate      | N/A                                   | Callback when the skill is no longer considered active by the intent service.  | N/A |
| intent.service.skills.deactivated | {'skill_id': str}                   | Intent service deactivated a skill.                                            | {self.skill_id}.deactivate |
| intent.service.skills.activated  | {'skill_id': str}                    | Intent service activated a skill.                                              | {self.skill_id}.activate |
| mycroft.skill.enable_intent     | {'intent_name': str}                  | Re-registers a disabled intent (intent_name contains munged skill_id)          | N/A |
| mycroft.skill.disable_intent    | {'intent_name': str}                  | Disables a registered intent (intent_name contains munged skill_id)            | N/A |
| mycroft.skill.set_cross_context | {'context': str, 'word': str, 'origin': str} | Sets a skill specific context (with munged skill_id)                    | N/A |
| mycroft.skill.remove_cross_context | {'context': str}                   | removes skill specific context (with munged skill_id)                          | N/A |
| mycroft.skills.settings.changed  | {'skill_id': dict}                   | Update settings if a remote settings change applies to this skill.             | N/A |
| {self.skill_id}.public_api      |                                       | Responds with the skill's public API.                                          | {self.skill_id}.public_api.response |
| {self.skill_id}.idle            | N/A                                   | callback to trigger homescreen provided by this skill                          | N/A |
| mycroft.mark2.collect_idle      |                                      | responds to ovos-gui letting it know skill provides a homescreen                |  mycroft.mark2.register_idle |
| mycroft.skills.abort_question   |                                      | Force self.get_response to return None immediately                              | N/A |


## Emits
| Message Type                   | Message Data                          | Effect                                     | In Response to / sent by  |
|--------------------------------|---------------------------------------|--------------------------------------------|--------------------------|
| {self.skill_id}.activate       | N/A                                   | Emits a message to activate the skill.     | intent.service.skills.activated |
| {self.skill_id}.deactivate     | N/A                                   | Emits a message to deactivate the skill.   | intent.service.skills.deactivated |
| intent.service.skills.activate | {'skill_id': str}                     | Marks the skill as active and pushes it to the top of the active skills list. | self._activate()  |
| active_skill_request           | {'skill_id': str}                     | (classic core) same as intent.service.skills.activate | self._activate()  |
| intent.service.skills.deactivate| {'skill_id': str}                    | Marks the skill as inactive and removes it from the active skills list. | self._deactivate() |
| skill.converse.pong             | {'skill_id': str, 'can_handle': bool}| Informs the skills service whether the skill can handle `converse`. | skill.converse.ping     |
| skill.converse.response         | {'skill_id': str, 'result': bool}    | Responds to a `skill.converse.request` with the result of `converse`. | skill.converse.request  |
| skill.converse.get_response.enable| {"skill_id": self.skill_id}        | Enables getting a response from the user during a conversation. |                      |
| skill.converse.get_response.disable| {"skill_id": self.skill_id}       | Disables getting a response from the user during a conversation. |                      |
| mycroft.mic.listen             |                                       | Triggers listening for user input.         |           |
| mycroft.mark2.register_idle    | {"name": self.resting_name, "id": self.skill_id}| Registers a resting screen for the skill.  | mycroft.mark2.collect_idle |
| mycroft.skill.set_cross_context | {'context': str, 'word': str, 'origin': self.skill_id} | Emits a message to set cross-context data. | self.set_cross_skill_context |
| mycroft.skill.remove_cross_context | {'context': str}                  | Emits a message to remove cross-context data. | self.remove_cross_skill_context  |
| speak                          | {"utterance": utterance, "expect_response": expect_response, "meta": meta, "lang": self.lang} | Initiates speech synthesis to speak the provided utterance. |  self.speak  |
| detach_skill                   | {"skill_id": self.skill_id} | Tell IntentService to remove all intents from this skill |  self.default_shutdown  |
| {self.skill_id}.public_api.response| {'{method_name}': {'help': str, 'type': str, 'func': str}} | Reports skill api data    | {self.skill_id}.public_api |

# ovos.py

## Emits
| Message Type               | Message Data | Description                                                                                   | sent by                |
|----------------------------|--------------|-----------------------------------------------------------------------------------------------|------------------------|
| mycroft.audio.queue        | {"uri": str} | Queue an audio file for playback.                                                             | self.play_audio        |
| mycroft.audio.play_sound   | {"uri": str} | Play an audio file instantly.                                                                 | self.play_audio        |
| mycroft.stop               |              | Stop everything skills are doing                                                              | self.send_stop_signal  |
| mycroft.audio.speech.stop  |              | Stop the speech synthesis process.                                                            | self.send_stop_signal  |
| mycroft.mic.mute           |              | (classic core) Mute the microphone, possibly used to stop recording during speech recognition.| self.send_stop_signal  |
| mycroft.mic.unmute         |              | (classic core) Unmute the microphone.                                                         | self.send_stop_signal  |
| recognizer_loop:record_stop|              | Instruct ovos-listener to stop recording.                                                     | self.send_stop_signal  |

# skill_launcher.py

## Listens to
| Message Type                 | Message Data                | Description                                           |
|------------------------------|-----------------------------|-------------------------------------------------------|
| mycroft.ready                |                             | Event indicating that Mycroft is ready.               |

## Emits
| Message Type                 | Message Data                | Description                                           |
|------------------------------|-----------------------------|-------------------------------------------------------|
| mycroft.skills.is_ready      | {"status": bool}           | Checks if the skills service is ready.               |
| mycroft.skills.loaded        | {"path": str, "id": str, "name": str} | Indicates that a skill has been successfully loaded. |
| mycroft.skills.loading_failure | {"path": str, "id": str} | Indicates that a skill failed to load.               |
| mycroft.skills.shutdown      | {"path": str, "id": str}   | Notifies that a skill is being shutdown.             |

