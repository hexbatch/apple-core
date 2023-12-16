# Scheduling Bounds


Create and manage time bounds. These bounds are made up of cron rules, stop and start time, and length of period
Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names are not public, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user



| Method | Path                       | Route Name                  | Operation                                        | Args                            |
|--------|----------------------------|-----------------------------|--------------------------------------------------|---------------------------------|
| Post   | bounds/schedule            | core.bounds.schedule.create | Makes a new schedule                             | name, cron, start, stop, period |
| Delete | bounds/schedule/:id/delete | core.bounds.schedule.delete | Deletes an unused schedule                       |                                 |
| Get    | bounds/schedule/:id/get    | core.bounds.schedule.get    | shows the time data with maybe list of schedules |                                 |
| Get    | bounds/schedule/:id/edit   | core.bounds.schedule.edit   | edit unused, can always set retired and name     |                                 |
| Get    | bounds/schedules/list      | core.bounds.schedule.list   | Shows a list of all the bounds the user has      | iterator                        |
| Get    | bounds/schedule/:id/ping   | core.bounds.schedule.ping   | returns  if a time in bounds                     | date time or none for now       |


        user: id
        name: name of the bounds (unique to any bounds owned by the user)
        is_retired: default false // if true then cannot be added later
        start: when to apply this bounds, inclusive
        stop: when to stop this bounds, inclusive
        cron: optional crontab string
        period_length: only used and required when the cron is defined, is how long this time is allowed per cron run
        timezone_to_use: if empty will be set by standard attribute of user_timezone


## Time bound operations (runs on the command line)

| Task             | todo | Operation                                   | Args |
|------------------|------|---------------------------------------------|------|
| make_time_spans  |      | Makes new time spans for a given time slice |      |
| clean_time_spans |      | clears out old spans                        |      |
