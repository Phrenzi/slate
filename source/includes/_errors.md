# Errors

The Phrenzi API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
405 | Method Not Allowed -- You tried to access a resource with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The resource requested has been removed from our servers
422 | Unprocessable Entity, this happend while request params have validation errors
429 | Too Many Requests -- You're requesting too many resources! Slow down!
479 | Staff Not Login / Staff Not Setup -- the endpoint protected by staff authenticated, you got to login staff first, and make sure staff is properly setup, then call this api
480 | Only manager staff are authorized to this operation
490 | Super Manager not signed any establishment yet
491 | Super Manager not allow to operate as current Establishment owner to update/delete
492 | Current Manager is not a super manager
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
