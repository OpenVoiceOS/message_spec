# PHAL System

## Listens to

| Message Type                         | Message Data                                                                                                                                  | Description                                         | Emitted Response Type                | Handled By                        |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|--------------------------------------|-----------------------------------|
| `system.ntp.sync`                    | "display": bool                                                                                                                               | Requests synchronization of the system clock        |                                      | handle_ntp_sync_request           |
| `system.ssh.status`                  |                                                                                                                                               | Checks SSH service status and emits a response      |                                      | handle_ssh_status                 |
| `system.ssh.enable`                  | "display": bool                                                                                                                               | Requests enabling the SSH service                   |                                      | handle_ssh_enable_request         |
| `system.ssh.disable`                 | "display": bool                                                                                                                               | Requests disabling the SSH service                  |                                      | handle_ssh_disable_request        |
| `system.reboot`                      | "display": bool                                                                                                                               | Requests a system reboot                            |                                      | handle_reboot_request             |
| `system.shutdown`                    | "display": bool                                                                                                                               | Requests a system shutdown                          |                                      | handle_shutdown_request           |
| `system.factory.reset`               | "wipe_cache": bool<br>"wipe_data":bool<br> "wipe_logs":bool<br>"wipe_configs":bool<br>"reset_hardware":bool<br>"script":bool<br>"reboot":bool | Requests a factory reset of the system              |                                      | handle_factory_reset_request      |
| `system.factory.reset.register`      | "skill_id": str                                                                                                                               | Registers a hardware specific factory reset handler |                                      | handle_reset_register             |
| `system.configure.language`          | "language_code": str <br> "display": bool                                                                                                     | Requests global language configuration              | `system.configure.language.complete` | handle_configure_language_request |
| `system.mycroft.service.restart`     | "display": bool                                                                                                                               | Requests a restart of the Mycroft service           |                                      | handle_mycroft_restart_request    |
| `system.factory.reset.phal.complete` | "skill_id": str                                                                                                                               | Indicates completion of PHAL-based factory reset    | `system.factory.reset.phal`          | handle_factory_reset_request      |

## Emits

| Message Type                    | Message Data    | Description                                                 | Trigger Message Type            | Emitted by                   |
|---------------------------------|-----------------|-------------------------------------------------------------|---------------------------------|------------------------------|
| `system.ntp.sync.complete`      |                 | Indicates completion of NTP synchronization                 | `system.ntp.sync`               | handle_ntp_sync_request      |
| `system.ssh.status.complete`    | "enabled": bool | Indicates SSH service status                                | `system.ssh.status`             | handle_ssh_status            |
| `system.factory.reset.ping`     |                 | Scan for extra factory reset plugins                        | `system.factory.reset.register` | handle_reset_register        |
| `system.factory.reset.start`    |                 | Indicates the start of the factory reset process            | `system.factory.reset`          | handle_factory_reset_request |
| `system.factory.reset.phal`     | "skill_id": str | Triggers extra hardware specific factory reset PHAL plugins | `system.factory.reset`          | handle_factory_reset_request |
| `system.factory.reset.complete` |                 | Indicates completion of the factory reset process           | `system.factory.reset`          |                              |
| `ovos.shell.exec.factory.reset` | "script": str   | Ask ovos-shell to run a script as part of factory reset     | `system.factory.reset`          |                              |
| `system.reboot`                 |                 | Requests a system reboot                                    | `system.factory.reset`          | handle_reboot_request        |

