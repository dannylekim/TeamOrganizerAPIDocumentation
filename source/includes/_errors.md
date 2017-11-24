# Errors

<aside class="notice">These are just general error codes. Please make sure you read the errors for each api call individually and use this only as a quick reference.</aside>

The Team Organizer API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- You need a token 
403 | Forbidden -- The method requested is hidden for administrators only
404 | Not Found -- The specified request could not be found
405 | Method Not Allowed -- You tried to access a call with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The object requested has been removed from our servers
418 | I'm a teapot
429 | Too Many Requests -- You're requesting too many things! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
