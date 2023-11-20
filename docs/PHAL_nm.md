# PHAL Network Manager

## Listens To

| Message Type                        | Message Data                                                      | Description                                  | Response Type                                                                   | Handled By                          |
|-------------------------------------|-------------------------------------------------------------------|----------------------------------------------|---------------------------------------------------------------------------------|-------------------------------------|
| `ovos.phal.nm.scan`                 |                                                                   | Allows client to request for a network scan  | `ovos.phal.nm.scan.complete`                                                    | handle_network_scan_request         |
| `ovos.phal.nm.connect`              | "connection_name": str<br>"password": str<br>"security_type": str | Allows clients to connect to a given network | `ovos.phal.nm.connection.successful`<br>`ovos.phal.nm.connection.failure`       | handle_network_connect_request      |
| `ovos.phal.nm.connect.open.network` | "connection_name": str                                            | Allows clients to connect to an open network | `ovos.phal.nm.connection.successful`<br>`ovos.phal.nm.connection.failure`       | handle_open_network_connect_request |
| `ovos.phal.nm.reconnect`            | "connection_name": str                                            | Allows clients to reconnect to a network     | `ovos.phal.nm.connection.successful`<br>`ovos.phal.nm.connection.failure`       | handle_network_reconnect_request    |
| `ovos.phal.nm.disconnect`           | "connection_name": str                                            | Allows clients to disconnect from a network  | `ovos.phal.nm.disconnection.successful`<br>`ovos.phal.nm.disconnection.failure` | handle_network_disconnect_request   |
| `ovos.phal.nm.forget`               | "connection_name": str                                            | Allows a client to forget a network          | `ovos.phal.nm.forget.successful`<br>`ovos.phal.nm.forget.failure`               | handle_network_forget_request       |
| `ovos.phal.nm.get.connected`        |                                                                   | Allows querying if connected to a network    | `ovos.phal.nm.is.connected`<br>`ovos.phal.nm.is.not.connected`                  | handle_network_connected_query      |

## Emits

| Message Type                            | Message Data                                 | Description                                                      | Trigger Message Type                                                                      |
|-----------------------------------------|----------------------------------------------|------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| `ovos.phal.nm.scan.complete`            | "networks": [{"ssid": str, "security": str}] | Emitted when the requested scan is completed with a network list | `ovos.phal.nm.scan`                                                                       | 
| `ovos.phal.nm.connection.successful`    | "connection_name": str                       | Emitted when a connection is successfully established            | `ovos.phal.nm.connect`<br>`ovos.phal.nm.reconnect`<br>`ovos.phal.nm.connect.open.network` |  
| `ovos.phal.nm.connection.failure`       | "errorCode": int<br>"errorMessage": str      | Emitted when a connection fails to establish                     | `ovos.phal.nm.connect`<br>`ovos.phal.nm.reconnect`<br>`ovos.phal.nm.connect.open.network` |  
| `ovos.phal.nm.disconnection.successful` | "connection_name": str                       | Emitted when a connection successfully disconnects               | `ovos.phal.nm.disconnect`                                                                 | 
| `ovos.phal.nm.disconnection.failure`    |                                              | Emitted when a connection fails to disconnect                    | `ovos.phal.nm.disconnect`                                                                 |  
| `ovos.phal.nm.forget.successful`        | "connection_name": str                       | Emitted when a connection successfully is forgotten              | `ovos.phal.nm.forget`                                                                     |  
| `ovos.phal.nm.forget.failure`           |                                              | Emitted when a connection fails to forget                        | `ovos.phal.nm.forget`                                                                     |  
| `ovos.phal.nm.is.connected`             | "connection_name": str                       | Emitted when the query indicates connection                      | `ovos.phal.nm.get.connected`                                                              | 
| `ovos.phal.nm.is.not.connected`         |                                              | Emitted when the query indicates no connection                   | `ovos.phal.nm.get.connected`                                                              | 

