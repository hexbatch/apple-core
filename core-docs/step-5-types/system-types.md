# There are some system defined types

system types have no owner

# Base type
All types inherit from the base type, which has no attributes. This always has the same uuid across all servers

# System type
Each install has its own system type that has unique uuid



# User Type 

For types of users, this is base.system.user

# Server Type
All servers are users
The token for the server user inherits from this, and all registered remotes inherit from this too

for servers, this is base.system.user.server

## Remote type  (standard_type.remote)
When a remote has an element type, then it inherits from this and the user type
base.system.remote




