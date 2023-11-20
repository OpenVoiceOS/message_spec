# PHAL IP Geolocation

## Listens to

| Message Type                 | Message Data      | Description                                                                                                                                                               | Emitted Response Type                                    | Handled by |
|------------------------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|------------|
| `mycroft.internet.connected` |                   | Triggers a reset of the IP geolocation with the existing location taking precedence if available.                                                                         | `configuration.updated`<br> `ovos.ipgeo.update.response` | on_reset   |
| `ovos.ipgeo.update`          | "overwrite": bool | Triggers a reset of the IP geolocation with an option to overwrite existing location. If 'overwrite' is False and an existing location is available, it takes precedence. | `configuration.updated`<br> `ovos.ipgeo.update.response` | on_reset   |

## Emits

| Message Type                 | Message Data                   | Description                                                                                   | Emitted by          |
|------------------------------|--------------------------------|-----------------------------------------------------------------------------------------------|---------------------|
| `configuration.updated`      |                                | Signals that the configuration has been updated, typically after a successful IP geolocation. | on_reset            |
| `ovos.ipgeo.update.response` | "error": str, "location": dict | IP geolocation data                                                                           | `ovos.ipgeo.update` |
