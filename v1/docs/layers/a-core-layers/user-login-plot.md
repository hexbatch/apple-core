# Registration jobs


Calls to core from different outer api

| Login step    | Core call      | Description            | Args |
|---------------|----------------|------------------------|------|
| user_login.me | core.user.read | gets current user info |      |



| Login step          | Layer call                   | Description         | Args |
|---------------------|------------------------------|---------------------|------|
| user_login.do_login | user_services.read_user_data | gets data to verify |      |

