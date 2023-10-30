# Search

Does searching.
A search is owned by the user, and the only ones who can use the search later, or read it is in the user's group as members
Searches can be copied and edited.

Searches can be deleted by anyone in the user admin group

Searches can be used to count or to get results, the results are iterated


| Method | Path               | Route Name | Operation                             | Args                                                           |
|--------|--------------------|------------|---------------------------------------|----------------------------------------------------------------|
| Post   | search             |            | Creates a search                      | The search info, optional flag to immediately run the search   |
| Post   | search/from_string |            | Creates a search from string notation | The string search, optional flag to immediately run the search |
| put    | search/:id/filter  |            | Set or remove filter                  | set filter, id of filter, or clear filter with null            |
| put    | search/:id/order   |            | Set or remove order                   | set order by, id of order, or clear order with null            |
| patch  | search/:id/part    |            | Add or change a part                  | one or more parts, processed in order of the post data         |
| Delete | search/:id/part    |            | Remove a part                         | array of part indexes                                          |
| get    | search/:id/count   |            | Counts search results                 |                                                                |
| get    | search/:id/results |            | gets the iteration of results         | iteration id provided by earlier, or if missing from the start |
| post   | search/:id/copy    |            | Copies a search                       |                                                                |
| Delete | search/:id         |            | Deletes the search                    |                                                                |
| GET    | search:id/read     |            | lists the search                      | optional requirements filter                                   |
| GET    | searches/list      |            | lists the searches of a user          | optional filters                                               |






a search

    id
    user
    [search parts],
    optional requirement to order
    optional requirement to filter

each search part is:

    index: 
    skip: > or / (optinal if left out then > )
    set conditions:
        owner:
        relationship_to: search part
    token name: (optional )
    token_id: (optional)
    attributes:
        [{
            attribute name or id,
            value (literal or range or regex)
        }]


Search results is
    
    search_id,
    iterator_next


Adding parts that have the same index
    if a part is added that has the same index as one already there, the part will be inserted before the same index, and all the other parts are bumped up one index

Removing parts
    The index places are removed, and then the parts are re-indexed to start at 0

Listing searches
    can filter by token id, or attribute or owner

results can have options to show different amount of data in the results (-wide option)