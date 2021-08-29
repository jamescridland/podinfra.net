---
title: Best practice for everyone in podcasting
---

## An open ecosystem with best practice

A work in progress, this website is intended to be a non-opinionated guide to being the best citizen in the open podcast ecosystem. It is a Github website, open for anyone to edit, add to, or debate.

Give feedback by either [opening an 'issue'](https://github.com/jamescridland/podinfra.net/issues) or by submitting a pull request with an edit; this site at the moment is a single-page, but in time will be split into different sections.

### Language used here

This website is guided by **independence, pragmatism and minimalism**. Minimum features should be simple to implement and require no specific skills or libraries.

"Ensure" - this is **the minimum that the industry expects.** While you won't be blocked for not doing this (in most cases), you'll show respect for the ecosystem if you complete these bare minimum requirements.

"Consider" - it **would be great if you can also do this.** Not every part of the ecosystem relies on this, but advanced podcasters and hosting companies will make use of additional features if you can implement them.

## For app developers

* [Set a clear user agent throughout your app](/app-developers/user-agents.html)

### Don't confuse podcasters with your app

* **Please ensure you do not change or remove any query strings** that have been added to the audio URL: the audio may not play without them.
* **With audio, ensure you call a bot for what it is**. If your app takes a copy of the audio for analysis purposes, please clearly mark that in the user agent. Podnews's bot uses a useragent like `PodnewsBot/1.0 +https://podnews.net/bot` which is clear that this is not a human listen and should not be categorised as one.

### The RSS feed

There are many elements to a podcast RSS feed, especially when you consider the podcast namespace extensions.

It's tempting to ask that a podcast app considers implementing everything; but this guide aims to be a pragmatic, developer-friendly list of best practices, not an implementation guide to every tag.

Accordingly, this list of best practices is a specific guide to the bare minimum requirements that podcast publishers expect. Your podcast app will benefit from implementing much more than these items.

#### Get the order right, and respect serial podcasts

Ensure that your app supports the `itunes:type` field. Serial podcasts, where a story slowly unfolds over a period of shows, are a growing part of podcasting, and the order of these shows is important. (Nobody wants to find out whodunnit by mistake!)

If you see `<itunes:type>serial</itunes:type>` in the RSS feed, ensure that your app behaves as a user expects:
1. Ensure you use the `<itunes:episode>` tag to order the episodes so that the first episode is visible at the top of the list.
2. If a show has more than one **season**, ensure you use the the `<itunes:season>` tag to show the newest season to a user first. So if a podcast is up to season five, a new listener should initially see Season 5.

Consider showing a trailer, if one exists, prominently at the top of any episode list. Consider hiding this trailer once a user has listened to it.

*Tip:* The PodClock podcast app testing feed has two seasons. Season one contains a number of esoteric tests; season two contains one episode with a 'clock' download timer. 

* [Information from Podbean about itunes:type](https://help.podbean.com/support/solutions/articles/25000010756-how-to-set-ios11-itunes-feed-tags-in-your-podcast)
* Evo Terra's [podcast app manifesto](https://podcastpontifications.com/helpful-info/podcast-app-manifesto#:~:text=respect%20rss%20feeds%20tagged%20as%20serial) about serial podcasts

#### Display descriptions properly in your app

Podcasters often monetise their shows by linking to websites. It is important that episode descriptions are displayed in full, with links intact. In show and episode descriptions, ensure that your app:
1. Displays any naked URLs as clickable links
2. Supports `<A>` anchor links
3. Support rudimentary `<P>` and `<BR>` formatting tags where HTML is seen
4. If no HTML is seen, respect CR/LF linebreaks
5. Consider supporting `<ul>` `<li>` bullet point lists

Some episode descriptions may be long. Consider displaying the entire description if possible; ensure you display at least the first 4,000 characters (Apple Podcasts's limit) or first 5,000 characters (Google Podcasts's limit).

Consider adding [noopener](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/noopener) and [nofollow](https://developers.google.com/search/docs/advanced/guidelines/qualify-outbound-links) to any links from podcast descriptions, so that links are secure and are signalled to Google and other search engines as being untrusted.

Some podcasters may embed images and other content into episode descriptions. This may risk your users' privacy, or your app's reputation. Consider either removing them, or displaying them after a user has requested them.

* [This page details current behaviour by major podcast apps](https://podnews.net/article/html-episode-notes-in-podcast-rss). Seek to do better.

