# Filters that are dynamic

Creates filters from set(s)

Create a requirements structure from one or more sets of tokens using a filter

Allow for a system defined attribute to have a family of attributes used for searching:

An attribute definition can give a range (min max) and weight (priority) for a token or attribute, and set for exact or allow descendants (null)
its live value can hold the target token type or attribute type

Any attributes of this kind in a token or set can be an "and"
To put or conditions then have those in a child related sets. To have only or then have the first set by empty of this attribute family

There is another attribute family that is for ordering search results and prioritizing filters. If I have some or filters, and a match in more than one, I can pick the higher priority one
Keep most of the current requirement api, but make this above instead of the requirements structure

