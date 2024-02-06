# Formatting

Converts readable attributes of an element set, or search result, into html markup, markdown,json or xml.
This is a read only operation.

Each formatting type will be a plugin

A map for attributes can be given which will correspond to html and xml tags
The tag attributes (not to be confused with element attributes) can be mapped to other attributes on the same element.
Markdown is made by first converting to html

Json mapping can map each attribute in an element to a key value pair, with the value being the attribute value, or json combination of values, or an array


The basic html can produce 

* ordered lists (using a picked attribute to order the list (number or string sorting and direction)) , default is creation date
* links (the element set can have its links to other sets and children)
* paragraphs (ordered similarly to lists default is creation date)
* headers and sections (children and their children can be sections instead of links, header 1 is first level children, header 2 is their children etc.)
* images (ordered similarly to lists default is creation date)



## Plugins 

* json
* xml
* html
* markdown (does not support extra attributes)

### Possible other formatting ideas

* social postings to different sites and systems (including used in element propagation)


### html plugin 

* Block tags correspond to sets with certain attributes.
* Inline tags correspond to elements inside a set
* Ordering is done by selected attribute values

For styling in css:
* sets with certain attributes can be given css rules provided in the mapping
* elements that are not sets can have attributes mapped to different inline css
  * this can include colors or text styles 

