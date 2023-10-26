# Aliases 

It's hard to switch some languages and reference a token in another language (easy enough for things that share same alphabet, harder for different character sets)
Aliases allow setting different names using different languages

A user can set aliases for his name, attributes, token types

Each alias must be unique.

After an alias is made, any searches can accept the alternate name, and if the user selects a language for the results to be in, if there is a language match, that alias will be used.
Additionally, the alias can be used as the token|token type|attribute id in api calls

Aliases can only be set for each language-family: totally different character sets

## Aliases operations

| Method | Path                                 | Route Name         | Operation                                        | Args                   | Notes |
|--------|--------------------------------------|--------------------|--------------------------------------------------|------------------------|-------|
| Post   | alias/{type}/guid/{lang-code}/create | alias.create       | Create Alias for the resource for that language  | alias (must be unique) |       |
| Delete | alias/{alias name}                   | user.destroy_token | Remove the alias, if user owns this              |                        |       |
| Get    | aliases                              | alias.list         | Lists the aliases the user has made can be paged |                        |       |

## System aliases

Some system defined attributes have names that have no user or dots, these cannot be edited by anyone

