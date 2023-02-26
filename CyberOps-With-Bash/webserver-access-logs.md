# Webserver Access Logs

Typical (there is also the Common Log Format, which excludes fields for referring page or user agent) record in apache2 log file:

`127.0.0.1 - - [16/May/2019:17:39:24 -0400] "GET / HTTP/1.1" 200 11173 "-" "curl/7.64.0"`

`127.0.0.1` IP address of the requesting host

`-` RFC protocol ID; `-` if not present

`-` HTTP authenticated user ID; `-` if not present

`[16/May/2019:17:39:24 -0400]` date time and GMT offset

`"GET /` the page that was requested

`HTTP/1.1"` the HTTP protocol version

`200` server's response status code:

    - `200` OK
    - `401` Unauthorized
    - `404` Page Not Found
    - `500` Internal Server Error
    - `502` Bad Gateway
    - [more status codes](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)

`11173` size of the file returned in bytes

`"-"` the referring page

`"curl/7.64.0"` user agent identifying the browser

