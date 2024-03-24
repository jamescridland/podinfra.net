---
title: Don't mess with the audio file request
---

## Don't mess with the audio file request

While a podcaster publishes an RSS feed to be reproduced inside your app to help you link to their episode, their audio file is their property, and must not be changed. In particular:

* **Ensure you do not change or remove any query strings** that have been added to the audio URL: the audio may not play without them.

* **Ensure you never cache audio files in your system** - a podcaster relies on the statistics from their podcast host, and may deliver specific versions to listeners. As one example, NPR produces a [localised afternoon news podcast](https://podnews.net/update/daily-localised-podcast) which uses geo-location of the listener, based on their IP address, to deliver local news stories. Advertising may also be geo-targeted. Of course, locally cache a file on the user's device: but don't take one copy of the audio file and store it in your own systems for user delivery.

* **Ensure you’re not downloading the audio more often than necessary** - a podcaster uses download numbers as a performance metric, so avoid distorting these figures by requesting the audio more than is needed. For browser-based players, set the `audio` element’s `preload` attribute to `none` (not `metadata`, `auto`, or blank). Alternatively, cache the audio locally on the users device.

* **Ensure you call a bot for what it is**. If your app takes a copy of the audio for analysis purposes, please clearly mark that in the user agent. Podnews's bot uses a useragent like `PodnewsBot/1.0 +https://podnews.net/bot` which is clear that this is not a human listen and should not be categorised as one.

Most audio files will be in either MP3 format or AAC-HE format; and podcast loudness should be set between -16 and -14 LUFS.

Many podcast apps contain individual playback enhancements. Consider storing these as separate settings for each podcast - a user may wish to set these based on individual podcast production or host delivery:
* dynamic processing to help listeners in noisy environments or with poorly-produced audio
* 'silence skipping' to help speed up listens
* adjustable playback speed (consider offering this fine-grained, 1.0x, 1.1x, 1.2x etc).
