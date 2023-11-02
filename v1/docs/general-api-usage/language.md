# Language

Choose language in the Accept-Language header, example: `Accept-Language: fr; q=1.0, en; q=0.5`

This is optional, if not there then the system default will be used (for now English)

When provided aliases in that language will be used.

The library will choose the best fitting language, but looking at the weights and what is supported.
So, will choose the highest ranked one that is supported, else will use the default
