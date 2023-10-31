# Registration jobs


Calls to core from different outer api

| Registration step       | Core call                 | Description                              | Args                     |
|-------------------------|---------------------------|------------------------------------------|--------------------------|
| registrations.form.init | core.standard.family.list | to make signup form input names and info |                          |
| registrations.create    | core.user.create          | when making new account                  | user standard attributes |



| Registration step               | Layer call                         | Description                      | Args |
|---------------------------------|------------------------------------|----------------------------------|------|
| registrations.form.init         | user_services.get_basic_user_token | to get example user id           |      |
| registrations.create            | user_services.store_bearer_token   | when user created                |      |
| registrations.store_credentials | user_services.store_user_data      | when user credentials stored     |      |
| registrations.reset_credentials | user_services.read_user_data       | when verifying id                |      |
| registrations.reset_credentials | user_services.store_user_data      | when new user credentials stored |      |

# Creating the form:

will call the standard args once to cache the fields, this is called using an example user token (found in user services)