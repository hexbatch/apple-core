# Set operations

Do things with sets, great for filtering, comparing collections, or mass altering union


When having a token join or leave a set, the actions of each token can run

When changing attributes, mass attribute change actions can run on each token


Set operations:

* T is the requirement and is always optional, if missing it means all are operated on
* A is the source set
* B is a second source set
* D is the destination set
* S is a token representing bounds for the filter in the set operations. This can be used in any operations. The tokens must be in these bounds.
    Can specify if using map, time or both (path not used)



        combine/add: A source, B source (optional),  T pattern, D destination
        difference: A source, B source ,  T pattern, D destination
        remove: A source, T pattern, D destination / removes tokens from a set puts it in another (optional) set
        edit_attribute => attribute name, attribute value , A source, T pattern
        change_owner => new owner id, A source, T pattern
        copy => A source, B source ,  T pattern, D destination
        results => search ,  T Pattern , D destination
