# Job service



| Job step                | Core call               | Description       | Args                                             |
|-------------------------|-------------------------|-------------------|--------------------------------------------------|
| job_services.create_job | core.user.token.create  | get token for job | passes in data to tie this job to this new token |
| job_step.destroy_token  | core.user.token.destroy | deletes its token |                                                  |



| Job step                | Layer call                         | Description                      | Args |
|-------------------------|------------------------------------|----------------------------------|------|
| job_services.create_job | user_services.get_basic_user_token | gets the token to make a new one |      |
| job_services.create_job | permissions_core.can_i_do_this     | checks to see if job can be done |      |

