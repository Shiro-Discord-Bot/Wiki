---
description: 'Before Shiro''s software can run, some preparations have to be done'
---

# Preparations

Shiro is hosted on a virtual private server at [GalaxyGate](https://galaxygate.net). With the use of Docker on our debian 9 server each software can be easily setup, monitored and updated.

#### Installing Docker

More information [here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-9)

```bash
apt-get update && apt-get upgrade -y
apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
apt-get update
apt-get install docker-ce -y
docker login docker.pkg.github.com -u GITHUB_USER -p GITHUB_TOKEN
```

#### Keeping containers updated with Watchtower

More information [here](https://containrrr.github.io/watchtower/)

```bash
docker pull containrrr/watchtower
docker run -d --name watchtower --restart=always -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --cleanup
```

#### Hosting MongoDB

More information [here](https://linuxize.com/post/how-to-install-mongodb-on-debian-9/)

```bash
apt-get install software-properties-common dirmngr -y
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
add-apt-repository 'deb http://repo.mongodb.org/apt/debian stretch/mongodb-org/4.0 main'
apt-get update
apt-get install mongodb-org -y
systemctl start mongod
systemctl enable mongod

mongo
use admin
db.createUser(
  {
    user: "<user>", 
    pwd: "<password>", 
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
quit()
```

#### Providing credentials

This file is placed in the root directory to provide credentials for each container

{% code title="/root/env.list" %}
```bash
# MongoDB
MONGODB_CONNECTION=

# Sentry
SENTRY_BOT_DSN=
SENTRY_SCRAPER_DSN=

# Reddit API
REDDIT_CLIENT_ID=
REDDIT_CLIENT_SECRET=
REDDIT_USER_AGENT=

# Discord Bot
DISCORD_BOT_TOKEN=
```
{% endcode %}

