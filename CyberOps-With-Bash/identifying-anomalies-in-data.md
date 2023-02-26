IDENTIFYING ANOMALIES IN DATA

user-agent is a small piece of textual info sent by a browser to web server, which identifies the client's OS, browser type, version, and other info.

List of most common user agents: [link](https://techblog.willshouse.com/2012/01/03/most-common-user-agents/)

Now if you compile a list of common user agents and compare a web server log against it, you can find unusual ones. If you find anomaly you can print it along with an IP address of the system making this request.

Take a look at ~/Dropbox/configurations/scripts/bash-cyber/11-useragents.sh
