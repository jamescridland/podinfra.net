---
title: Form data
authors: jamescridland
---

## Sanitise form input

Removing errors when a user enters information can help avoid un-needed support queries later.

* Consider normalising podcast names or artists to remove trailing spaces or double-spaces. <code>"My Amazing Podcast"</code> is not the same as <code>"My&nbsp;  Amazing Podcast"</code> nor is it the same as <code>"My Amazing Podcast "</code>. This can cause problems with in-app searches and services that attempt to match podcast names across different services.

In PHP, the following code will trim and remove double-spaces:
```
$str = preg_replace('/ {2,}/', ' ', trim($input));
```
