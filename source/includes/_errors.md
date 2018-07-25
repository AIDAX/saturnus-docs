# Errors

The Saturnus API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- Something disallowed the request.
404 | Not Found -- The specified endpoint could not be found.
405 | Method Not Allowed -- You tried to access a endpoint with an invalid method.
429 | Too Many Requests -- Rate limiter(5 reqs/s)
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
