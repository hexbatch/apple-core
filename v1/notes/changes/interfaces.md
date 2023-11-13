What are interfaces?

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
The interface has the pointers to the things it finds, and it, and the mutual are put into a set. This set is an interface, and only other interfaces can enter it.

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

A token can have more than one write attributes in a mutual, they are all written to at the same time.
A write attribute can have more than one unique data being sent to them at one time, if there are 
multiple read attributes in other interfaces that meshes with it.
If a write attribute is a json type, then these values are put into key value pairs. If the write attribute is a number or string or identity then it will get a random read from 2 or more sources.
When reading from multiple same read attributes, can use an iterator attribute (even a ghost attribute)

A write attribute can have a time bounds, or a time-out between writes, or can only write when there is a different value
A read attribute cannot be read if it has a time bounds, and can also have a timeout
---------

There are api operations to build up interfaces, and how they click



