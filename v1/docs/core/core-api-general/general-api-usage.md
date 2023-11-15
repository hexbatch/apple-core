# General api usage

* data input is json 
* data output is usually json, but some layers can change that, and some layers allow to specify
  * allowed data returns are json, xml, html 
* [Iterators](iterators.md) are used when there is too much data to display in one api call, 
* [Locations](locations.md) are done via geo json
* [Input times](times.md) are unix timestamp or ISO 8601
  * Output times are always ISO 8601
* [Errors and warnings](errors.md) are formatted in a certain way
* [language](language.md) is optionally set in the header of the call