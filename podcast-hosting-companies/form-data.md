---
title: Form data
authors: jamescridland
---

* Consider normalising podcast names or artists to remove trailing spaces or double-spaces. <code>"My Amazing Podcast"</code> is not the same as <code>"My&nbsp;  Amazing Podcast"</code> nor is it the same as <code>"My Amazing Podcast "</code>. In PHP, `$str = preg_replace('/ {2,}/', ' ', trim($input));` will trim and remove double-spaces.
