# GUI on mobile extension

Handles mycroft-gui running on android

# Listens to

| Message Type                           | Message Data | Description                                              | Emitted Response Type | Handled by             |
|----------------------------------------|--------------|----------------------------------------------------------|-----------------------|------------------------|
| `mycroft.gui.screen.close`             |              | Forces the display of the home screen in the GUI.        |                       | handle_show_homescreen |
| `mycroft.gui.forceHome`                |              | Forces the display of the home screen in the GUI.        |                       | handle_show_homescreen |
| `mycroft.gui.screen.request.page.back` |              | Handles a request to navigate back to previous GUI page. |                       | handle_page_back       |
