# Actions


Actions are remotes tied together, the below api is for making custom actions, and is wrong.
Actions and remotes need a think about the api here, because they are just existing types

| Method | Path                     | Route name | TO Do | Description                        |
|--------|--------------------------|------------|:------|------------------------------------|
| Post   | events/send_custom_event |            | *     | event attribute, target element    |
| Post   | events/custom/create     |            | *     | make custom event                  |
| delete | events/custom/remove     |            | *     | unregister custom event            |
| get    | events/custom/list       |            | *     | list custom events in admin group  |
| get    | events/standard/list     |            | *     | list standard events               |

    

# Sending custom events
events can be sent to a search path, and if too many in search, events can be sent to the next page.
There needs to be some tracking here of pages when they are done. Which implies here for the custom there is a log going on somewhere
