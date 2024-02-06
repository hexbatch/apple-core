# How to see the state of the system?

Often in building and testing, it is good to see a visual representation of the total state of the system

Here we can call the api to get all the json of all resources seen by a user: bounds, type, attributes, scripts, remotes, types, elements, sets, mutuals, interfaces, pipes

A browser page in another project can call on this to show in 3d the different connections, and be able to navigate through the model of it

The api can be called in the browser, then it can get the json, build the model or change it, and then the tester can see what happened 
