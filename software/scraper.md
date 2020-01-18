---
description: Scrapes animes and themes from the web and adds them to the database
---

# Scraper

### About

The subreddit [/r/AnimeThemes](https://www.reddit.com/r/AnimeThemes/) holds about 10.000 anime openings and endings. This scraper reads each wiki page and parses them. The found themes will be downloaded and compressed whereupon there are stored in the filesystem and it's metadata in the database. Also, an anime a theme belongs to will be fetched from [MAL](https://myanimelist.net/). Furthermore, themes can be grouped by popularity and rank through the anime metadata. Because of this, the scraper can guarantee a seamless song stream without any rate limits for the bot.

### Setup

Install the Docker image

```text
docker pull shirodiscordbot/scraper
mkdir ./themes
docker run -d --name scraper --env-file env.list -v /themes:/app/themes shirodiscordbot/scraper
```

{% hint style="info" %}
Shiro's software is not optimized for self-hosting
{% endhint %}

