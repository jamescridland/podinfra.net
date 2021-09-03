---
title: Display audio files correctly
authors: evoterra
---

There are two potential "title" fields in for each episode:
* The standard `<title>` tag from the RSS spec
* A special `<itunes:title>` tag within Apple's podcast namespace

Apple created their name space as a way to encourage podcasters to remove meta information - most commonly episode numbering - from the title field to allow for a more enjoyable reading experience. By way of example, consider these two fields title fields for a single episode of the podcast _Today in iOS_:

`<title>Tii 0505 - WWDC 2021, iOS 15, iPadOS 15, and watchOS 8</title>`

`<itunes:title>WWDC 2021, iOS 15, iPadOS 15, and watchOS 8</itunes:title>`

The first starts with `Tii 0505` - a legacy numbering system that literally means the 505th episode of Today in iOS (Tiii), and is designed to be used by podcast listening apps that do not extract `<itunes:season>` or `<itunes:episode>` values from the item and display along with the title of the episode.

An example from Overcast, a popular podcast listening app that does not extract the optional item tags, showing the full  contents of the standard `<title>` tag:

![Image from iOS](https://user-images.githubusercontent.com/2339588/131421735-b73d4760-9478-4c8a-86a8-6c75759c38d2.jpg)

The second is designed to be use by Apple Podcasts, a listening app that does extract and display the `<itunes:season>` or `<itunes:episode>` values from the item and display along with the title of the episode, as shown in this example, where you can see the value of the `<itunes:episode>` tag has been extracted and placed at the beginning of the `<itunes:title>` tag, followed by a period and a space:

![Image from iOS (1)](https://user-images.githubusercontent.com/2339588/131421849-6bf641e6-f909-4b71-b016-c17a3bc5551a.jpg)

A good rule of thumb is to check the feed for instances of the optional `<itunes:season>` or `<itunes:episode>` tags. If found, use the `<itunes:title>` tag and disregard the default `<title>` tag.
