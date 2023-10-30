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



        combine/add: A source, B source (optional),  T pattern, D destination
        difference: A source, B source ,  T pattern, D destination
        remove: A source, T pattern, D destination / removes tokens from a set puts it in another (optional) set
        edit_attributes => [attribute name, attribute value or other attribute id] , A source, T pattern
        change_owner => new owner id, A source, T pattern
        copy => A source, B source ,  T pattern, D destination
        results => search ,  T Pattern , D destination