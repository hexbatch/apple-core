# Token types

A token type is a template to make a token from, it can also be used to select tokens from a set, if the tokens are made from it, or has an ancestor that is this

Token types can have many parents, but the attributes have to allow this to happen (conflicts or contract conditions)

Token types can have one or more parents, they can have many ancestors.
Ancestors (which includes parent) cannot be cyclic by having their ancestors be something they are an ancestor of.

Token types do not record location, only sets of tokens do

    So: a token-type:
        user: one user owns the type
        options:
            allow_bounds: boolean
            allow_actions: boolean
        attributes: []
        parents: []