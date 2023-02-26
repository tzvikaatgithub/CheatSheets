:oauth2:

## Resources

Lunch n' Learn: OAuth - by Mark Ali - 2021-08-13 - very good overview:
    * [GSlides](https://docs.google.com/presentation/d/1Zv_j4UpOjyxMhfrObWj6l_afK6byNEFWXd7wZ5txu78/edit#slide=id.ge1e03fa542_0_218)
    *  [Video](https://drive.google.com/drive/folders/1Ezand7xrME1CysePnygSISjOYpFYrXEo)
    * https://oauth.net/2/
    * https://connect2id.com/learn/oauth-2
    * https://ngrok.com/ - to create a temporary encrypted tunnel to local host
* [OAuth 2 Workflow — Requests-OAuthlib 1.0.0 documentation](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html)
        * `pip install requests requests_oauthlib`
    * [Create a Flask Application With Google Login – Real Python](https://realpython.com/flask-google-login/)
    * [Authentication — Requests 2.25.1 documentation](https://docs.python-requests.org/en/latest/user/authentication/#basic-authentication)
    * [OAuth2 in Python | TestDriven.io](https://testdriven.io/blog/oauth-python/)

## Generate Tokens

You can generate an oauth2 token using cURL or HTTPie:

https://www.daimto.com/how-to-get-a-google-access-token-with-curl/
    * the most important part is the refresh token - it doesn't expire
    * autorization tokens are temporary

https://www.ctl.io/developers/blog/post/curl-vs-httpie-http-apis

https://httpie.io

## Summary

4 Roles in OAuth:
    * Resource Owner: end-user
    * Resource Server: protected asset (ex: web API) requiring a token to be accessed
    * Client: the application which needs a token to access resource server
    * Authorization Server: server issuing access tokens to the client, after authentication of end user

    * client presents a valid credential to the autorization server
        - type of credential will depend on the type of client application

Process of obtaining a token:
    1. The client initiates the code flow by redirecting the browser to the authorisation server with an authorisation request.
        - At the authorisation server, the user will be authenticated
        - autorization server calls the client redirect_uri sending it the state and code parameter
        - client validates the state parameter and use the code parameter to proceed to next step
    2. The client initiates code-for-token exchange on the token endpoint of authorization server
        - client ID and secret are passed via the Authorization header
            + this can be basic or JWT authentication
        - on success, authorization server will return a JSON object with the issued access token
            + if it returns also a refresh token, then it can be used to obtain a new token without initiating the code flow again
    3. Client accesses a protected resource using access token
        - access tokens are commonly of type Bearer - just pass it with each request
        - Authorization header is the recommended method (GET)
    4. Resource server validates the token
        - it was issued by the authorization server
        - token hasn't expired
        - the scope covers the request

Bearer tokens are the keys to the castle, they must be protected, and submitted over TLS/HTTPS.
