# Operations 

Runs set operations

Anyone can run set operations on any sets or tokens they can read. The destination sets have to be writable by the user.
For the write operations (attributes, change owner) this only works when the user can write to those attributes being changed or is admin for the token



| Method | Path                   | Route Name | Operation                                | Args                                                           |
|--------|------------------------|------------|------------------------------------------|----------------------------------------------------------------|
| Post   | operation/combine      |            | Combines two sets                        | see docs                                                       |
| Post   | operation/difference   |            | Intersection of two sets                 | see docs                                                       |
| Post   | operation/remove       |            | Removes tokens from a set                | see docs                                                       |
| Post   | operation/copy         |            | Adds tokens found in A to B              | see docs                                                       |
| Post   | operation/attributes   |            | Modifies all token attribute(s) in a set | see docs                                                       |
| Post   | operation/change_owner |            | Changes all token owners in a set        | see docs                                                       |
| Post   | operation/results      |            | Puts search results (per page) in a set  | see docs                                                       |


Sets are referenced by their token id
Requirements are referenced by their id (and not their token)

* T is the requirement and is always optional, if missing it means all are operated on
* G is a group of users, and is always optional, who must own the tokens to be used in the operation
* S is a token representing bounds for the filter in the set operations. This can be used in any operations. The tokens must be in these bounds.
  Can specify if using map, time or both (path not used). This is always optional
* A is the source set
* B is a second source set
* D is the destination set

        combine/add: A source, B source (optional),  T pattern, G group, D destination
        difference: A source, B source ,  G group, T pattern, D destination
        remove: A source,  G group, T pattern, D destination / removes tokens from a set puts it in another (optional) set
        edit_attributes => [attribute name, attribute value or other attribute id] , A source, T pattern , G group
        change_owner => new owner id, A source,  G group, T pattern
        copy => A source, B source ,  G group, T pattern, D destination
        results => search ,   G group, T Pattern , D destination