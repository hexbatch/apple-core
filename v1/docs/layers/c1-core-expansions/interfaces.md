# What are interfaces?

# (changelist todo or ponder about)
------------------------

* containers do not need to be mutual sets, containers can hold the token to any group of sets, and they can be unrelated
  * container can hold the tokens directly, or do the below
  * there can be set tokens there, any set tokens directly added to the container will look at the tokens inside each set
  * the set relations will work here. Adding a parent set will also have its children and descendants and links looked at too
  * can optionally specify when adding each set to ignore some|all relations too

* regular actions on sets can hold a container (set) of interfaces. The container will try to react to containers in other actions.
  * If they click this can be a pipeline, how it attaches
  * Additionally, should the containers click, they can emmit another event that is processed at the same api call, and anything can listen to this event,
      * event is custom, but can be listened to while being on something else in the same set, on in the set. 
      * This allows reacting interfaces to be able to change the set they are in
        * for example, reacting interfaces can make two shapes be next to each other

* An interface definition can include option to only allow reacting if all the reads to writes match up, and not just some
* the identities can specify in the path that there are no descendants to match

## Concept of binders

Need a way to connect two or more perhaps incompatible interfaces together and get them to react, indirectly
Binders provide a mechanism to construct larger and more complex things based on how two or more interfaces are coordinating
They do this through custom actions fired on the binder's container's set token, which can keep state, alter other attributes which act as flags to non interface stuff

* Concept of binders
  * Binders have no tokens in their own container, but have two or more interface definitions, and a way to map from one definition to another.
    * reads in A to writes in B, and vice versa . Not just one on one though. Can have mappings for each interface going to one, some or all of the other interfaces
  * Binders have an off and on state for each interface, when its on, then the interface is open to react.
    * once its reacting then it will stay reacting until the other interface from the other container  stops
    * or can turn off its interface 
  * Binders have custom events fired to the binder that starts or stops a reaction, to allow logic to be processed when the interfaces are turned on or off
    * Each interface defined in the binder has a matching attribute on the container token whose truthful value turns on the interface and whose falsy value turns it off
  * Binders can also be attachment points to pipes, but I am not sure how that works yet
---------------------------------------------
---------------------------------------------

# description

We can pick any token, and one or two attributes. The attributes do not have to be on the token, or related to the token, or in the same set as the token
If we pick one attribute, it can be used for reading and writing, or just writing or just reading.
If we use the second attribute it has to be used for the opposite (if first is reading, the second must write, and vice versa)

The token and the two attributes do not have to be related or connected

Now we have an identifier (the token) and a way to read something or a way to write something or a way to do both reading and writing.
The reading and writing and token do not have to be connected, associated or have anything to do with each other.

We can also specify the bounds and path of each of the three things. So, sometimes there is not a way to read, write or identify.

An interface definition is one or more of these Identities .
The individual attributes and tokens can repeat, in different Identities, but each Identity is unique in an interface definition.

      Identity:
         N: path to a token, that can have bounds. Required
         R: path to a read attribute, that can be on any token that could have bounds. Can be missing if W
                time bounds (not on parent attribute, or is there?), timeout, setting to only allow read when there is different data
         W: path to a write, also on any token and cna have bound. Can be missing if R
                time bounds, timeout, setting to only write if different data from before

    
    Clicking:
        name of this clicking: string
        indentities:
            paths we click with here: [path]
        clickings:
            paths we click with here: [path]


     Interface Definition
         user: one user owns the definition
         name: using the naming rules
         identities: [identity]
         clusters: [clicking names]   


An interface is created when we apply an interface definition to a mutual set. If all the identities can be located in the mutual, then we have an interface connected tto this mutual.
The interface has the pointers to the things it finds, and it, and the mutual are put into a set called the container. This set is an interface, and only other interfaces can enter it.

The interface remembers the last write value to each of its writes, and last write time that the data was accepted

When two or more interfaces are put into any one set, they can react to other interfaces if one or more read/write attributes, on different interfaces, match up.
The reading attribute can send data to the writing attribute. The reading attribute can be a descendant of the writing attribute, or the same type.
The reading cannot be a base type of the writing
(if I want to take in data for only an Algerian description, then I do not want a Japanese description. But if I am taking data for any description, then the Japanese will be fine)

If I have set up a clicking of one interface, then if that interface is in the set, and the paths allow it, then I will only listen to that set, and not another interface that can write to me.
If I have more than one clicking, then I will only click to all of them at the same time, or not at all (inactive).

I can also click with clusters, so I will read/write only if that cluster is there in the set

When interfaces click, the one that is reading is in the interface set of the other. If they are mutually clicking, they are in each other's interface set.
When the click paths different, even if just for one, then the clicking will end. Otherwise, the attached sets can change the set, as a group, that they swim in.

Clicked together interfaces can be very nested and complex, or simple.

Clicked attributes are not readable or writable by anything except their pairings. Any attributes that are not clicked on an interface are called exposed.

A token can have more than one write attributes in a mutual, they are all written to at the same time.
A write attribute can have more than one unique data being sent to them at one time, if there are
multiple read attributes in other interfaces that meshes with it.
If a write attribute is a json type, then these values are put into key value pairs. If the write attribute is a number or string or identity then it will get a random read from 2 or more sources.
When reading from multiple same read attributes, can use an iterator attribute

A write attribute can have a time bounds, or a time-out between writes, or can only write when there is a different value
A read attribute cannot be read if it has a time bounds, and can also have a timeout
---------

There are api operations to build up interfaces, and how they click

--------------

Can set a container to be read only.
Can set a container to be read only after it's not, and flip it back and forth as needed.

Can set a container to be const. Cannot write.
The last reads are saved, and that cache is used without asking the attributes for more recent info

----------------
Events for this are sent to the container. The events can elect to now allow the operation,
and the events are given all the outputs or inputs at the time for the attribute paths they are listening.

Events can be used for blocking something, regulating it (being an iterator), forwarding all the interface changes somewhere.
Write actions are only sent when the action is writable (in its own bounds and the write bounds for it)


----------------------------
Can make a wrapper for the interface. Given a container, can connect read and/or write either way .
A wrapper will make a new interface definition, a temporary one, that changes according to the wrapped container's exposed interface, to encompass all the container's exposed read/writes
Can also limit this wrapper by filtering it with other interface definitions.

The wrappers are their own interfaces.

There are api operations to make wrappers.

A wrapper does not affect what they wrap, and to the container they wrap, are invisible. However can find the wrappers of a container via api call.

Wrappers can be chained together to allow alternate paths for read and writes, and can be done to create pipelines between containers in different sets.

Can have listening script or remote on a wrapper to do side jobs as conditions happen.

---------------------

once created, a container is just a token to be put into any set, or sets. The reads are activated in an interface when their read attributes, found in the mutual they are attached to,
are written to in other api operations.

The activated read interfaces drive the write interfaces


--------------------------
Interfaces have to always be attached to live mutuals. If the mutual is changed (evolves) so that one or more identities cannot be fulfilled, then the interface is evaporated (destroyed)
There is an event that is fired (cannot cancel that event) to allow remote to learn and act on this

If a wrapper is using a container that has no more interfaces, then that wrapper is evaporated. Constructs made out of the wrappers, such as a pipeline can be cascaded evaporated too

----------------------
A container in a set is not affected by other tokens entering or leaving the set. A container entering or leaving the set does not trigger any events on the host set.
However, other tokens in the set can be affected by the presence or absence of that container set based on their listeners

----
using any interface definition, and can select on a search path for groups using this.
If this interface definition finds any interfaces in the sets that their read attributes match all the given interface definition writes,
then it will return the matched interfaces to a set or to be listed out

can take an interface and do same as above, and any matched interface that can react to all the first interface's writes will write to it, one at a time
This is a one way react, the targets are only read from.

Can do boolean matching this way too, for more than one interface definitions.
Take a nested group operation for or and xor, with the logic connecting tests to be able to react one way, then will return this filtered list
This filtered list can be put into a set, where they only one way react. Or can be listed out
---------------------------
can aggregate an interface current write values (the container will remember the last write values) using aggregation operations

when having one interface be written by several, can do operation where this results in selected attributes being aggregated

----------------------------

interface operations can be created and used later in a structured environment, like the mutual group operations. Here do and or and xor.
where a match to be able to write to all the source interface is a 1, and not being able to is a 0.
Can put a 1 or 0 as a constant to help make other bool operations

This ultimately produces a true or false result


This can be used to drive goals, and make promises

----

# Pipelines

Pipelines copy or transfer interfaces from one set to another. They are a set themselves.

* They are one way
* They can have a filter using an interface type that must match the reads or the writes, or both, of other interfaces to let them in
    * Can optionally use an interface expression to filter through

Pipeline joints allow more than one pipeline to be joined, inputs match outputs.
Each pipeline at the joint can select to copy the action and also move the token in its pipeline, or make sure its the only pipeline to process the container

can be any order of joints and pipelines
A container can only get into the same pipeline one time only, before its put into a set, and then its can start over again

## Pipeline events

When an instance enters the pipeline, the regular events for having the container enter and leave can be activated.

