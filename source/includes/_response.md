# HTTP Response Description

The HTTP status code `2XX` represents the request was executed successfully. Otherwise, the HTTP status code `4XX` represents the request unable to execute.

The VMS API uses the following success codes:


Success Code | Meaning
---------- | -------
200 | OK -- The request was executed normally.
201 | Created -- The request has been fulfilled and resulted in a new resource being created.
204 | No Content -- The server successfully processed the request, but is not returning any content.


The VMS API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request
401 | Unauthorized -- Your `X-VMS-API-Key` or `X-VMS-Auth-Token` is wrong.
403 | Forbidden -- The requeste is not able to execute.
404 | Not Found -- The specified VMS could not be found.
409 | Conflict -- There is duplicated resource.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
