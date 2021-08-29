---
title:Display descriptions properly in your app
---

## Display descriptions properly in your app

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
