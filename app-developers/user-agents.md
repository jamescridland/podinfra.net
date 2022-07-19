---
title: Set a clear user-agent throughout your app
authors: jamescridland
---

## Set a clear user-agent throughout your app

It is very important for podcaster publishers that they have accurate statistics about podcast consumption. Stats help publishers market their show or monetise it; in some cases, knowing that someone is listening is the difference between doing a podcast and giving up. Making it clear what consumption comes from your app will help publishers know where their audience discovered them, and may result in publishers advertising in your app or service, or promoting it more.

**Please ensure you set clear and identifiable HTTP user agents** every time your app, or associated APIs, connects to a third-party service to download the RSS feed or audio. 

There are [best practices for user agents](https://developers.whatismybrowser.com/learn/user-agent-best-practices/) detailed elsewhere on the internet. A good user agent for a podcast app looks like:

`MyPodcastApp/1.2 iPhone/13 +http://mypodcastapp.example.com`

It should include:
* an obvious name of your podcast app, and its version number
* some form of identification of OS and hardware
* a URL for more information about your app
* no personal information or overly-detailed device information that could be used to identify your user

<i class="far fa-lightbulb"></i> Your app may have different methods of downloading audio - from an auto-download that your app performs on a schedule, to a listener-initiated download ("a stream") that grabs audio for someone to listen to when they press play. Ensure that each of these methods has a correct user-agent.

<i class="far fa-lightbulb"></i> You can hear your audio user-agent being read back to you in season 1, episode 1, of the PodClock podcast app testing feed at https://podnews.net/clock-rss which is also in all major podcast directories. This episode will also display your RSS crawler's useragent in the item description.

## Settings for commonly-used libraries

* If you use `axios` to fetch files, [you should use the 'headers' option](https://masteringjs.io/tutorials/axios/user-agent).
* If youre using `react-native`, then [here's something that should help](https://stackoverflow.com/questions/36590207/set-user-agent-with-webview-with-react-native) for both Android and iOS.

## Using AppleCoreMedia? Here's how to change it

If you use the `AppleCoreMedia` library to stream files, historically this has sent an opaque user agent that has been unable to be changed. With with iOS 16, you can [set the user agent correctly using the `AVURLAssetHTTPUserAgentKey`](https://developer.apple.com/documentation/avfoundation/avurlassethttpuseragentkey). Please do so: AppleCoreMedia user agents give creators no clue about how big your podcast app is and whether they should be promoting your app more.

## Can't change it?

There are some circumstances where you are unable to change the user agent, particularly on browser-based services. In these circumstances, consider adding a clear player identification slug in an additional GET parameter to the audio URL request, in the form: `_from=com.example.mypodcastapp` - a consistent reverse-URI identifier for your app. Some podcast analytics companies may use this to identify your app. Your app may already have [an identification slug in this Github repository](https://github.com/opawg/podcast-rss-useragents).
