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

### Set a clear user agent throughout

It is very important for podcaster publishers that they have accurate statistics about podcast consumption. Stats help publishers market their show or monetise it; in some cases, knowing that someone is listening is the difference between doing a podcast and giving up. Making it clear what consumption comes from your app will help publishers know where their audience discovered them, and may result in publishers advertising in your app or service, or promoting it more.

**Please ensure you set clear and identifiable HTTP user agents** every time your app, or associated APIs, connects to a third-party service to download the RSS feed or audio. 

There are [best practices for user agents](https://developers.whatismybrowser.com/learn/user-agent-best-practices/) detailed elsewhere on the internet. A good user agent for a podcast app looks like:

`MyPodcastApp/1.2 iPhone/13 +http://mypodcastapp.example.com`

It should include:
* an obvious name of your podcast app, and its version number
* some form of identification of OS and hardware
* a URL for more information about your app
* no personal information or overly-detailed device information that could be used to identify your user

If you run a central RSS crawler, please ensure this is identified. Consider reporting back subscriber counts, like [this example from Overcast](https://overcast.fm/podcasterinfo):

`Overcast/1.0 Podcast Sync (123 subscribers; feed-id=456789; +http://overcast.fm/`

*Tip:* Your app may have different methods of downloading audio - from an auto-download that your app performs on a schedule, to a listener-initiated download ("a stream") that grabs audio for someone to listen to when they press play. Ensure that each of these methods has a correct user-agent.

*Tip:* You can hear your audio user-agent being read back to you in season 1, episode 1, of the PodClock podcast app testing feed at https://podnews.net/clock-rss which is also in all major podcast directories. This episode will also display your RSS crawler's useragent in the item description.

There are some circumstances where you are unable to change the user agent: whether using the `AppleCoreMedia` library or on browser-based services. In these circumstances, consider adding a clear player identification slug in an additional value to the audio URL request, in the form: `_from=com.example.mypodcastapp` - a consistent reverse-URI identifier for your app. Some podcast analytics companies may use this to identify your app.

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

