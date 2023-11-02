# Iterators and long lists of results

Often, an api call will result back in too many items to list in one result, so the results are paginated

It's faster for big data results to use the iterator concept rather than pagination

here, all search results give back iterators to get the next and previous page contents, but cannot jump pages.
use the iterator id to get the next page, this is provided in the url, so can call the url

iteration is one way only and can have duplicates in the results as things are updated in between calls for a page.

Each page will have the following attached at the top of the response body. if no extra pages, then the next and previous will be null

    Property	        Description
    uri	                The URI of the current page.
    first_page_uri	    The URI for the first page of this list.
    next_page_uri	    The URI for the next page of this list.
    previous_page_uri	The URI for the previous page of this list.
    page	            The current page number. Zero-indexed, so the first page is 0.
    page_size	        How many items are in each page
