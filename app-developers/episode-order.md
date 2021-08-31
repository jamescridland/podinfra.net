---
title: Get the episode order right, respecting serial podcasts
---

## Get the order right, and respect serial podcasts

Ensure that your app supports the `itunes:type` field. Serial podcasts, where a story slowly unfolds over a period of shows, are a growing part of podcasting, and the order of these shows is important. (Nobody wants to find out whodunnit by mistake!)

If you see `<itunes:type>serial</itunes:type>` in the RSS feed, ensure that your app behaves as a user expects:
1. Ensure you use the `<itunes:episode>` tag to order the episodes so that the first episode is visible at the top of the list.
2. If a show has more than one **season**, ensure you use the the `<itunes:season>` tag to show the newest season to a user first. So if a podcast is up to season five, a new listener should initially see Season 5.

Consider showing a trailer, if one exists, prominently at the top of any episode list. Consider hiding this trailer once a user has listened to it.

<i class="far fa-lightbulb"></i>  The PodClock podcast app testing feed has two seasons. Season one contains a number of esoteric tests; season two contains one episode with a 'clock' download timer. 

<i class="far fa-lightbulb"></i>  Tip: RSS feeds are usually ordered in date order, with the newest episode first: but apps shouldn't rely on the order of the RSS feed for display purposes. If season and episode numbers are being used, use those instead to order your episodes.
  
### <i class="fas fa-book-open"></i> Further reading

* [Information from Podbean about itunes:type](https://help.podbean.com/support/solutions/articles/25000010756-how-to-set-ios11-itunes-feed-tags-in-your-podcast)
* Evo Terra's [podcast app manifesto](https://podcastpontifications.com/helpful-info/podcast-app-manifesto#:~:text=respect%20rss%20feeds%20tagged%20as%20serial) about serial podcasts
