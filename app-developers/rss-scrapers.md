---
title: RSS scrapers
authors: jamescridland
---

* If you run a central RSS crawler, please **ensure this is identified [with a user-agent](/app-developers/user-agents.html).**

* Consider reporting back subscriber counts, like [this example from Overcast](https://overcast.fm/podcasterinfo):

`Overcast/1.0 Podcast Sync (123 subscribers; feed-id=456789; +http://overcast.fm/`

* Consider saving your bandwidth, and that of podcast hosts, by using the [accept-encoding header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) to request that RSS feeds are GZIPped. RSS feeds are highly compressible.

* Consider using PodPing or WebSub to be alerted when a new episode of a podcast is published. This will help your server infrastructure avoid unnecessary feed polling, and ensure that podcasts are promptly updated with new episodes.
