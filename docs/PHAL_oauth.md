# PHAL OAuth

## Listens To

| Message Type                            | Message Data                                                                                                                                                                                          | Description                                                   | Emitted Response Type          | Handled By               |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|--------------------------------|--------------------------|
| `oauth.register`                        | "skill_id": str<br>"app_id": str<br>"auth_endpoint": str<br>"token_endpoint": str<br>"refresh_endpoint": str<br>"scope": str<br>"client_id": str<br>"client_secret": str<br>"shell_integration": bool | Register OAuth credentials for a skill's app.                 |                                | handle_oauth_register    |
| `oauth.start`                           | "skill_id": str<br>"app_id": str                                                                                                                                                                      | Start the OAuth authentication process.                       |                                | handle_start_oauth       |
| `oauth.get`                             | "skill_id": str<br>"app_id": str                                                                                                                                                                      | Get the OAuth authentication URL.                             | `oauth.url`                    | handle_get_auth_url      |
| `ovos.shell.oauth.register.credentials` | "skill_id": str<br>"app_id": str<br>"client_id": str<br>"client_secret": str                                                                                                                          | Register OAuth credentials from the shell.                    |                                | handle_client_secret     |
| `oauth.get.app.host.info`               |                                                                                                                                                                                                       | Get information about the app's host (IP and port).           | `oauth.app.host.info.response` | handle_get_app_host_info |
| `oauth.generate.qr.request`             | "skill_id": str<br>"app_id": str                                                                                                                                                                      | Request the generation of a QR code for OAuth authentication. | `oauth.generate.qr.response`   | handle_generate_qr       |

## Emits

| Message Type                            | Message Data                                                                | Description                                                      | Trigger Message Type         |
|-----------------------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------|------------------------------|
| `oauth.token.response.{munged_id}`      | token_response: dict                                                        | Notify registered apps/skills about OAuth token response.        |                              |   
| `oauth.url`                             | "url": str                                                                  | Reply containing the OAuth authentication URL.                   | `oauth.get`                  |                         
| `ovos.shell.oauth.start.authentication` | "url": str<br>"skill_id": str<br>"app_id": str<br>"needs_credentials": bool | Start the OAuth authentication process from the shell.           |                              |  
| `oauth.app.host.info.response`          | "host": str<br>"port": int                                                  | Reply containing information about the app's host (IP and port). | `oauth.get.app.host.info`    | 
| `oauth.generate.qr.response`            | "skill_id": str<br>"app_id": str<br>"qr": str                               | Reply containing the generated QR code for OAuth authentication. | `oauth.generate.qr.request`  |  
| `ovos.shell.oauth.display.qr.code`      | "skill_id": str<br>"app_id": str<br>"qr": str                               | Display the OAuth QR code in the shell.                          | `oauth.generate.qr.response` |  

