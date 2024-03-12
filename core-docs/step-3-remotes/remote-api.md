# Remotes

remote api defined at


Remotes cannot change ownership
Remotes can be fully edited if not used anywhere in any element types or elements. They can be turned off though (things happen to the remote). Or given a redirect
Remotes deletable if the remote not used in any element or type

Remotes can be tested with a test context. When created the test context will be set used to remember stats to follow the rules of cool-down
There can be multiple test_contexts for each remote.




| Method | Path                              | Route Name                   | ToDo | Operation                                             | Args                                                                     |
|--------|-----------------------------------|------------------------------|:-----|-------------------------------------------------------|--------------------------------------------------------------------------|
| Post   | remote                            | core.remotes.create          |      | Makes a new remote                                    | Required name                                                            |
| Patch  | remote/:id/edit                   | core.remotes.edit            |      | Edit part of value, if possible, sparse               | Any detail , sparse update                                               |
| Get    | remote/:id/get                    | core.remotes.get             |      | returns full remote info                              | flags for detail level                                                   |
| Get    | remotes/list                      | core.remotes.list            |      | searches for remotes that can use                     | iterator                                                                 |
| Get    | remote/:id/test                   | core.remotes.test            |      | Sends to the Remote, returns remote activity to track | add json body for the values it draws on                                 |
| Delete | remote/:id/destroy                | core.remotes.destroy         |      | Delete Remote, if the user can                        |                                                                          |
| POST   | remotes/activity/:activity/update | core.remotes.activity.update |      | completes a manual waiting remote                     | json or xml or http code or headers or text                              |
| get    | remotes/activity/list/:status     | core.remotes.activity.list   |      | lists activity                                        | iterator,can filter it for manual(types), activity state (or all states) |
| get    | remotes/activity/:activity/get    | core.remotes.activity.get    |      | gets a remote activity                                |                                                                          |
| get    | remotes/stack/:stack/get          |                              | *    | shows the activities in a stack, and how the stack is |                                                                          |



# List activity 
can optionally list for status or just the single activity
can also show all remotes in system  if flag passed and the user has that admin attribute to see other remotes

# See the status of a remote stack
each activity has a stack, show the entire stack status if one is in usage group of any remotes in the stack.
The call should also show how the values and logic for the calls are, and call statis.
