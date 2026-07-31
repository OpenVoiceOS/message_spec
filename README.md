# message_spec

This repository documents the message bus used by [OpenVoiceOS](https://github.com/OpenVoiceOS). It lists the message types that each OVOS component sends and receives.

For each message type, it gives the data the message carries and the response it triggers. The bus is how OVOS components talk to each other. A skill, a service, or a GUI does not call another component directly. It sends a message with a type and a data payload, and it listens for messages of the types it cares about.

This repository is the reference for those message types.

## Contents

Each file covers the messages for one component or group of components:

- [`ovos_core.md`](ovos_core.md): the skill manager, intent service, and other core services.
- [`ovos_audio.md`](ovos_audio.md): audio playback and text-to-speech.
- [`skills.md`](skills.md): the base skill classes from `ovos-workshop` (`OVOSSkill`, `FallbackSkill`, `OVOSCommonPlaybackSkill`, `CommonQuerySkill`, `IdleDisplaySkill`, `SkillLoader`).
- [`gui.md`](gui.md): the GUI service and enclosure (hardware) messages.
- [`opm.md`](opm.md): the OVOS Plugin Manager.
- [`persona.md`](persona.md): persona registration and querying.
- [`dinkum.md`](dinkum.md): Dinkum-specific services.

Each file lists, for a given component, the messages it listens to and the messages it emits. A table row gives the message type, its data, a description of the message, and its response type (if any).

## Using this reference

To find out how a component reacts to the bus, open the file for that component and read the "Listens to" table. To find out what a component announces to the rest of the system, read the "Emits" table.

Message types and payload fields in these tables are normative. A skill or service that implements a message type must match the type name and payload shown here.

## Related projects

- [OpenVoiceOS/ovos-core](https://github.com/OpenVoiceOS/ovos-core): the core services described in `ovos_core.md`.
- [OpenVoiceOS/ovos-audio](https://github.com/OpenVoiceOS/ovos-audio): the audio service described in `ovos_audio.md`.
- [OpenVoiceOS/ovos-workshop](https://github.com/OpenVoiceOS/ovos-workshop): the base skill classes described in `skills.md`.
- [OpenVoiceOS/ovos-gui](https://github.com/OpenVoiceOS/ovos-gui): the GUI service described in `gui.md`.
- [OpenVoiceOS/ovos-plugin-manager](https://github.com/OpenVoiceOS/ovos-plugin-manager): the plugin manager described in `opm.md`.
- [OpenVoiceOS/ovos-persona](https://github.com/OpenVoiceOS/ovos-persona): the persona system described in `persona.md`.

A rendered version of this reference is published at [openvoiceos.github.io/message_spec](https://openvoiceos.github.io/message_spec/).
