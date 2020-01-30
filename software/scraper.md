---
description: Scrapes animes and themes from the web and adds them to the database
---

# Scraper

### About

The subreddit [/r/AnimeThemes](https://www.reddit.com/r/AnimeThemes/) holds about 10.000 anime openings and endings. This scraper reads each wiki page and parses them. The found themes will be downloaded and compressed whereupon there are stored in the filesystem and it's metadata in the database. Also, an anime a theme belongs to will be fetched from [MAL](https://myanimelist.net/). Furthermore, themes can be grouped by popularity and rank through the anime metadata. Because of this, the scraper can guarantee a seamless song stream without any rate limits for the bot.

We try to reduce our requests to [Jikan](https://jikan.moe/) and [AnimeThemes](https://animethemes.moe/) because we don't want to put their free service under heavy load. Requests are delayed with timers and already scraped songs are not fetched every time.

### Setup

Install the Docker image

```text
docker pull shirodiscordbot/scraper
mkdir /root/themes
docker run -d --name scraper --restart=always --env-file /root/env.list --network="host" -v /root/themes/:/src/themes/ shirodiscordbot/scraper
```

{% hint style="info" %}
Shiro's software is not purposed for self-hosting, please use the official bot
{% endhint %}



