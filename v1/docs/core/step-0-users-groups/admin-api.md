# Admin api

can only be used on localhost, or via command

## Users operations

| Method | Path                       | Route Name                 | Operation                                   | Description                             | Args                              | Notes |
|--------|----------------------------|----------------------------|---------------------------------------------|-----------------------------------------|-----------------------------------|-------|
| delete | admin/users/destroy_tokens | admin.users.destroy_tokens | Revokes all tokens for the given users      | Used by the layers to regenerate tokens | user id or guids to do this for   |       |
| post   | admin/users/create_tokens  | admin.users.create_tokens  | Makes/returns new token for each given user | Used by the layers to regenerate tokens | user id or guids to do this for   |       |
| get    | admin/users/list           | admin.users.list_users     | Returns user info in pages, can filter      | Used by the layers to regenerate tokens | page number, optional search path |       |