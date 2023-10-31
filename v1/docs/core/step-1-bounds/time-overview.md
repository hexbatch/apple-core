# Time boundaries

Time bounds is defined by both a range to start and stop using this bounds, and an option period that includes a duration.

When creating a bounds, it can have 0 , 1 or many time bounds.

The union of the times is when that attribute is active

Bounds can also have a location part, so that means even if the attribute is at the right time, it also must be at the right place too

Time bounds always exists inside a created bounds

    so a time-bound:
        
        name: name of the bounds (unique to any bounds owned by the user)
        start: when to apply this bounds, inclusive
        stop: when to stop this bounds, inclusive
        cron: optional crontab string
        period_length: only used and required when the cron is defined, is how long this time is allowed per cron run
        timezone_to_use: if empty will be set by standard attribute of user_timezone


The time bounds calculates out the periods of being on, using the timezone to convert this to unix timestamps