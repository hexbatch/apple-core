# Sessions

* api to sessions and their command pallets


# API

## show session
    session.show

The logged-in user can select a session id, or none to use the default session.
Then the return will show the sets and elements in the working set of the session, along with the command pallet urls

    current_set:
        set_name:
        set_author: (owner)
        Contents:
        elements: ( a page of elements with urls to inspect) the child and linked sets are also elements here, and the set status will show up in the info
        each element has some standard attributes listed (name, image or other appearance, description)
        next_url: ( a url to get this current set but with the next page of the element contents)
        Commands:
        a list of urls and descriptions and names of what can do
        there are navigation commands (go up, go back, home, etc), a create bookmark command url, a bookmark set url, and whatever else plugins add in
