FINICKY
:finicky:

# Contents

- [Installation](#Installation)
- [Console](#Console)
- [Sample finicky.js file](#Sample finicky.js file)

# Installation

Install with `brew install --cask finicky`

[GitHub - johnste/finicky: A macOS app for customizing which browser to start](https://github.com/johnste/finicky)

# Console

Finicky app has a console, you can use it to test URL.

# Sample finicky.js file

This is from Fabio Germann

```
// Use https://finicky-kickstart.now.sh to generate basic configuration
// Learn more about configuration options: https://github.com/johnste/finicky/wiki/Configuration
// and https://github.com/johnste/finicky/wiki/Configuration-ideas

module.exports = {
  defaultBrowser: "Google Chrome",
  rewrite: [
    // Redirect all urls to use https
    {
      match: ({ url }) => url.protocol === "http",
      url: { protocol: "https" }
    },
    // Remove tracking
    {
      match: () => true, // Execute rewrite on all incoming urls to make this example easier to understand
      url: ({url}) => {
        const removeKeysStartingWith = ["utm_", "uta_"]; // Remove all query parameters beginning with these strings
        const removeKeys = ["fbclid", "gclid"]; // Remove all query parameters matching these keys

        const search = url.search
            .split("&")
            .map((parameter) => parameter.split("="))
            .filter(([key]) => !removeKeysStartingWith.some((startingWith) => key.startsWith(startingWith)))
            .filter(([key]) => !removeKeys.some((removeKey) => key === removeKey));

        return {
          ...url,
          search: search.map((parameter) => parameter.join("=")).join("&"),
        };
      },
    }
  ],
  handlers: [
    {
      // Open apple.com and example.org urls in Safari
      match: ["apple.com/*", "itunes.com/*"],
      browser: "Safari"
    },
    {
      // Asana
      match: "app.asana.com/app/*",
      url: ({url}) => {
        const match = url.search.match(/dest=(.+)/)
        const uriInfo = decodeURIComponent(decodeURIComponent(match[1]))
        const rwInfo = uriInfo.replace('https://app.asana.com', 'asanadesktop:///app')
        return !match ? url : rwInfo;
      },
      browser: "Asana"
    },
    {
      // Asana II
      match: "app.asana.com/0/*",
      url: ({url}) => {
        return "asanadesktop:///app/" + url.pathname;
      },
      browser: "Asana"
    },
    {
      // Zoom
      // zoommtg://scalepad.zoom.us/join?action=join&confno=00000000&confid=...base64...&browser=chrome
      match: "scalepad.zoom.us/*",
      url: ({url}) => {
        const match = url.pathname.match(/\/j\/([0-9]+).*/)
        const confId = match[1]
        const rwInfo = "zoommtg://scalepad.zoom.us/join?action=join&confno=" + confId
        return !match ? url : rwInfo;
      },
      browser: "/Applications/zoom.us.app"
    },
    {
      // Open google.com and *.google.com urls in Google Chrome
      match: [
        "google.com/*", // match google.com urls
        "*.google.com/*", // match google.com subdomains
      ],
      browser: "Google Chrome"
    }
  ]
};
```
