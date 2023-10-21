# Iterators and long lists of results

Often, an api call will result back in too many items to list in one result, so the results are paginated

It's faster for big data results to use the iterator concept rather than pagination

here, all search results give back iterators to get the next page contents, use the iterator id to get the next page,

iteration is one way only and can have duplicates in the results as things are updated in between calls for a page