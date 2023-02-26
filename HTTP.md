# Basic HTTP info
:http:

https://www.w3schools.com/tags/ref_httpmethods.asp
* GET is used to request data from a specified resource
    - sends data in URL `?name1=value1&name2=value2`
    - can be cached
    - remains in the browser history
    - can be bookmarked
    - should never be used when dealing with sensitive data
    - has length restrictions
    - is only used to request data (not modify)
* POST send data to a server to create/update a resource
    - is never cached
    - does not remain in the browser history
    - cannot be bookmarked
    - has no restrictions on data length
    - calling POST request repeatedly has side effects of creating the same resource multiple times
* PUT is used to send data to a server to create/update a resource
    - PUT requests are idempotent, calling them multiple times produces the same result
* HEAD is almost identical to GET, but without the response body
* DELETE method deletes the specified resource
* OPTIONS method describes the communication options for the target resource

# List of Response Codes

https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

# Get vs Post
:get:post:

https://www.geeksforgeeks.org/get-post-requests-using-python/
