# Errors 

use the https://datatracker.ietf.org/doc/rfc9457/ 
sample format 

    {
        type: url to explanation related about the issue
        status: echos the http code
        title: short readable summary
        instance: the error code
        "errors": {
                //optional with key=>value pairs as object
        }
    }


    {
    "title": "The username field must be at least 3 characters. (and 2 more errors)",
    "instance": 1,
    "status": 422,
    "errors": {
        "username": [
            "The username field must be at least 3 characters.",
            "name should have only letters and numbers and underscrores and not start with a number "
        ],
        "password": [
            "The password field confirmation does not match."
        ]
    }
}


