# Boundaries in the core

A boundary can be an area on the map, or some period(s) of time, or if something is in a certain set

By default, there is no boundaries for anything made. But it's easy to add in boundaries to attributes, types, tokens, and requirements.
A boundary can only be set on an attribute. But attributes make the things that have the boundaries.

Something can have many attributes, so any boundary is always the sum of all the boundaries of all the attributes.
When an attribute is turned off, in a token, the bounds are still counted from it.

## Time bounds

When an attribute exists can be set up by cron tasks, and ranges of times.

## Map bounds

Can be any combination of shapes on the map, these have latitude and longitude coordinates

## Path bounds

An attribute only exists if the token is being acted on in a set with some characteristics, such a content, relationship, or type of tag making the sets
