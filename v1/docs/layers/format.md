# Formatting

Converts the attributes of a token set, the attributes the user can read, into html markup, or markdown

Each formatting type will be a plugin for that project

The basic can produce 

* ordered lists (using a picked attribute to order the list (number or string sorting and direction)) , default is creation date
* links (the token set can have its links to other sets and children)
* outside links (pick an attribute to find urls and text)
* paragraphs (ordered similarly to lists default is creation date)
* headers and sections (children and their children can be sections instead of links, header 1 is first level children, header 2 is their children etc)
* images (ordered similarly to lists default is creation date)


then the plugins can render this to html or markdown or other

## Possible formatting ideas

* social postings to different sites and systems (including used in token propagation)

## Side effects with existing

* Pages can be protected to be read by only some users, or made private
* Because token sets can be arranged to only be readable when certain tokens are combined, this makes pages only readable to those that have a certain combination of tokens in their sets
* Pages can be tagged and reorganized , elements of some pages can be combined in a new page
  * For instance, all the images nested N need in the links can be put into a list in a new page
  * or tagged lists can be pulled apart from different pages to be put into one list
 