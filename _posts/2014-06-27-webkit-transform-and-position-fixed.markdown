---
layout: post
title:  "Using transform with position fixed"
categories: css bug
disqus: y
share: y
published: true
---

Using a combination of `transform` and `position: fixed` produces odd behaviour in Webkit.

Discovered when trying to implement a page zoom control using `transform: scale(0.8)` on the `<body>`.
I noticed that elements with fixed positioning started appearing in the wrong places.

It seems this was reported as a Chromium bug several years ago: <a href="https://code.google.com/p/chromium/issues/detail?id=20574">bug report</a>

However the last comment suggests it isn't a bug, rather a problem with the spec:

<a href="http://meyerweb.com/eric/thoughts/2011/09/12/un-fixing-fixed-elements-with-css-transforms/">Un-fixing fixed elements with CSS transforms</a>

