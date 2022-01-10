---
title: RSS scrapers
authors: jamescridland
---

## Ensure your RSS crawler is identifiable

It is important to indicate to a server where its traffic is coming from. It helps podcast hosting companies understand who is consuming their RSS feeds, and can also help podcasters know where their podcast is being consumed.

* If you run a central RSS crawler, please **ensure this is identified [with a user-agent](/app-developers/user-agents.html).** This is normally one line of code, and a minor change, but makes all the difference to podcasters.

Here's [how to set it in Go](https://stackoverflow.com/questions/13263492/set-useragent-in-http-request), and in [Python's feedparser module](https://pythonhosted.org/feedparser/http-useragent.html), and in [the Axios library](https://github.com/axios/axios/issues/2560#issuecomment-555778304).

A best-practice user-agent for your RSS scraper would be something like:

`MyAppNameCrawler/1.2 +http://mypodcastapp.example.com`

## Consider...

* Consider reporting back subscriber counts, like [this example from Overcast](https://overcast.fm/podcasterinfo):

`Overcast/1.0 Podcast Sync (123 subscribers; feed-id=456789; +http://overcast.fm/`

* Consider saving your bandwidth, and that of podcast hosts, by using the [accept-encoding header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) to request that RSS feeds are GZIPped. RSS feeds are highly compressible.

* Consider using PodPing or WebSub to be alerted when a new episode of a podcast is published. This will help your server infrastructure avoid unnecessary feed polling, and ensure that podcasts are promptly updated with new episodes. Using either PodPing or WebSub, you can cut your bandwidth and server load by 99% - by parsing new RSS feeds on request, when new episodes are published.
