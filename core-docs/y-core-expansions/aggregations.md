# aggregations

Adds new set operations

* take a set of elements apply an operation to them
* can be all the elements, or use a filter to sort by attribute family and or element type
* result is an attached attribute (new or already existing) to an element
* Can be done just for the elements in one set, if the elements have some ordering then this affects the json

## Types of aggregations supported:


### working on numeric type data (works on attributes that have values of numeric type)
* average
* sum
* max
* min
* standard deviation
* variance
* group concat (distinct or all)
* json array (distinct or all)


### working on json
* JSON_ARRAY AGG()	Return result set as a single JSON array
* JSON_OBJECT AGG()	Return result set as a single JSON object
* json Arrays that are ordered can be made by using the agg operations


### Working on strings
* concat (distinct or all)


## New set operations

* Use group operations on selected attributes in a set to calculate one value which then is written to a target element attribute as a live attribute on the element.
* take a set of elements, can do operations on it to reduce this to a single value. The operation can be filtered
