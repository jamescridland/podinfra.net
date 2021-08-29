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

## For podcast app developers
{% include_relative app-developers/section-index.md %}

### Don't confuse podcasters with your app

* **Please ensure you do not change or remove any query strings** that have been added to the audio URL: the audio may not play without them.
* **With audio, ensure you call a bot for what it is**. If your app takes a copy of the audio for analysis purposes, please clearly mark that in the user agent. Podnews's bot uses a useragent like `PodnewsBot/1.0 +https://podnews.net/bot` which is clear that this is not a human listen and should not be categorised as one.

### The RSS feed

There are many elements to a podcast RSS feed, especially when you consider the podcast namespace extensions.

It's tempting to ask that a podcast app considers implementing everything; but this guide aims to be a pragmatic, developer-friendly list of best practices, not an implementation guide to every tag.

Accordingly, this list of best practices is a specific guide to the bare minimum requirements that podcast publishers expect. Your podcast app will benefit from implementing much more than these items.

