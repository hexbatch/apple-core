# Registrations

Each registration process should be an agent that takes the info, creates the user, and fills the element and set with pertinent info.

This means, the plugins below will not be needed.

Each registration agent will handle the login, logout, pw resetting (if applicable) and cancelling of the user account if required.
This allows all login and registration types to be standalone programs or webpages that are approved for this higher priv access.
These agents can also update user info based on outside changes.

The agents here store the non expiring tokens of the users they handle.

Because this is a regular agent other than creating the user, the user can later cancel this agent, or keep the agent but add additional user-agents

User-agents set their own pw requirements, if they even use passwords
See agents.


## Advantages

This keeps the gui and outside calls away from this api, and allow flexibility, mixing and matching.
The first user-agent for registration is only for testing, requiring a username and a password.
The api for here is the agent api

