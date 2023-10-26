# Aliases 

Aliases allow setting different names using different languages

Api calls can have an optional language set in the call.
If there is no language, then no aliases will be used. However, if there is a language set, then the aliases will be looked for, if missing the non-alias will be needed.

Cannot mix aliases from different languages in same api call




A user can set aliases for his name, attributes, token types

Each alias must be unique:
* for usernames, the alias must be unique for each username, using a collation that reduces lookalikes
* for other resources, the alias must be unique for that user's resource (they still must begin with the username alias that shares the same language code )
  * for this reason, if any alias are made in a language, the username must be an alias in that language too

After an alias is made, any searches and id calls can accept the alternate name, should the api be made in that language

Additionally, the alias can be used as the token|token type|attribute id in api calls

api results that return names that have aliases for the selected language will use those for the id



## Aliases operations

| Method | Path                                 | Route Name         | Operation                                        | Args                   | Notes |
|--------|--------------------------------------|--------------------|--------------------------------------------------|------------------------|-------|
| Post   | alias/{type}/guid/{lang-code}/create | alias.create       | Create Alias for the resource for that language  | alias (must be unique) |       |
| Delete | alias/{alias name}                   | user.destroy_token | Remove the alias, if user owns this              |                        |       |
| Get    | aliases                              | alias.list         | Lists the aliases the user has made can be paged |                        |       |

## System aliases

Some system defined attributes have names that have no user or dots, these cannot be edited by anyone

