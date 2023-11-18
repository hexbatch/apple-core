# Core expansions add plugins into the core

* Expansions can be added to the plugins folder in the core, and toggled on and off in the composer json 
* Once added, the modules add new api operations that the layers and others can call just like normal core api
* The api for managing extensions is added to the admin api

see [core expansions.md](../../core/core-api-general/expansions.md)


Expansions are done here because not everything needs them, but some layers do

# Api

## add expansion
    core_expansions.list
Give info about the expansions used