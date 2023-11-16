# ovos-homescreen message SPEC

- [HomeScreen](#homescreen)
    * [Listens To](#listens-to)
    * [Emits](#emits)

# HomeScreen

## Listens To

| Message Type                                  | Message Data           | Description                                                         | Response Type(s)                                       | handled by |
|-----------------------------------------------|------------------------|---------------------------------------------------------------------|--------------------------------------------------------|------------|
| `ovos.homescreen.main_view.current_index.get` |                        | Responds with the index of the current page selected in the display | `ovos.homescreen.main_view.current_index.get.response` | idle.qml   |
| `ovos.homescreen.main_view.current_index.set` | {'current_index': int} | Sets the index of the current page  in the display                  | `ovos.homescreen.main_view.current_index.get.response` | idle.qml   |

## Emits

| Message Type                                           | Message Data           | Description                                                                             | In Response To                                          |
|--------------------------------------------------------|------------------------|-----------------------------------------------------------------------------------------|---------------------------------------------------------|
| `ovos.homescreen.main_view.current_index.get.response` | {'current_index': int} | Responds to ovos.homescreen.main_view.current_index.get with the index of current page. | `ovos.homescreen.main_view.current_index.get.responsey` |
