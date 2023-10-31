# General api usage

* ata input is json, and output is json
* ata input is json, and output is json
* Some api calls can generate web pages, this is set by options in the call
* When there is too much data to display in one api call, [iterators](iterators.md) are used
* [locations](locations.md) are done via geo json
* [Input times](times.md) are unix timestamp or ISO 8601
* Output times are always ISO 8601
* [Errors](errors.md) are formatted in a certain way
* Language is optionally set in the header of the call