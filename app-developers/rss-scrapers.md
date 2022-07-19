---
title: RSS scrapers
authors: jamescridland
---

## Ensure your RSS crawler is identifiable

It is important to indicate to a server where its traffic is coming from. It helps podcast hosting companies understand who is consuming their RSS feeds, and can also help podcasters know where their podcast is being consumed.

You can **see your current scraper's user agent** by looking at the episode notes in Season 1, Episode 1 of the **PodClock** podcast, which is a podcast testing feed. Here's the [RSS feed](https://podnews.net/clock-rss), though it's in all the normal directories.

* If you run a central RSS crawler, please **ensure this is identified [with a user-agent](/app-developers/user-agents.html).** This is normally one line of code, and a minor change, but makes all the difference to podcasters.

Here's [how to set it in Go](https://stackoverflow.com/questions/13263492/set-useragent-in-http-request), in [Python's feedparser module](https://pythonhosted.org/feedparser/http-useragent.html), using [Python feed requests](https://stackoverflow.com/questions/10606133/sending-user-agent-using-requests-library-in-python), and in [the Axios library](https://github.com/axios/axios/issues/2560#issuecomment-555778304).

A best-practice user-agent for your RSS scraper would be something like:

`MyAppNameCrawler/1.2 +http://mypodcastapp.example.com`

There's no evidence that any podcast host is banning any podcast app based on their useragent: and there is no need to include `Mozilla/5.0` or any similar obfuscation.

## Use etag for caching

When you retrieve an RSS feed, store the [etag header value](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag) in your database. The etag header value changes when the content changes.

When polling it, send the etag value back [as an `If-None-Match` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match).
* If there's new content in the RSS feed, you'll get the full RSS feed back for you to parse and ingest (along with a new etag).
* If there is NO new content in the RSS feed, you'll just get a `304: Not Modified` back. No need to parse or ingest anything.

## Consider...

* Consider reporting back subscriber counts, like [this example from Overcast](https://overcast.fm/podcasterinfo):

`Overcast/1.0 Podcast Sync (123 subscribers; feed-id=456789; +http://overcast.fm/`

* Consider saving your bandwidth, and that of podcast hosts, by using the [accept-encoding header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) to request that RSS feeds are GZIPped. RSS feeds are highly compressible.

* Consider using PodPing or WebSub to be alerted when a new episode of a podcast is published. This will help your server infrastructure avoid unnecessary feed polling, and ensure that podcasts are promptly updated with new episodes. Using either PodPing or WebSub, you can cut your bandwidth and server load by 99% - by parsing new RSS feeds on request, when new episodes are published.
