:ngrok:

* [How to Use ngrok: Easily Share Your Local Server :Step-by-Step - SitePoint](https://www.sitepoint.com/use-ngrok-test-local-site/)
* [ngrok – documentation](https://ngrok.com/docs)

`ngrok http 80` expose a web server on port 80 on your local machine

open http://localhost:4040 in your browser to introspect traffic going over your tunnels

Now you also need to run some web server..

`ngrok help` to learn more

# Authentication

The default way to authenticate is to store the token in the ngrok.yml

Yes, you can authenticate ngrok using an environment variable instead of storing the authentication token in the ngrok.yml file. Here's how you can do it:
* Create an environment variable named NGROK_AUTH_TOKEN with the value of your ngrok authentication token.
* Start ngrok with the following command: `ngrok http 3000 -authtoken=$NGROK_AUTH_TOKEN` This will start ngrok and use the authentication token stored in the NGROK_AUTH_TOKEN environment variable.