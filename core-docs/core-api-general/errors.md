# Errors and warnings

errors and warnings will show up in expected areas in any response

both errors and warnings have a int status, message string, code string ,and more_info url

Example:

        {
        "status": 400,
        "message": "No to number is specified",
        "code": 21201,
        "more_info": "http:\/\/www.twilio.com\/docs\/errors\/21201"
        "errors": []
        }

errors array are additional errors, and can be missing

Errors are under the api_errors, in the response. A response may have this missing if no errors. There can be more than one error here,
so this is an array

Warnings are same, but under api_warnings.

the status of both uses regular http codes, but only the errors will change the call result past 399.
If multiple errors, then the highest status will be used.

warnings will change the call http code itself to the highest warning status. Warning codes are always below 400 