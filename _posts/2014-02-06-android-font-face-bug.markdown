---
layout: post
title:  "Android @font-face bug"
categories: android css bug
disqus: y
share: y
---

The version of Chrome used as the default browser in some versions of Android has a bug that means web fonts are not rendered correctly when the tablet is in portrait mode.

If you switch to landscape you should see the correct font.

More details about the bug here:

[https://code.google.com/p/chromium/issues/detail?id=138257#c25](https://code.google.com/p/chromium/issues/detail?id=138257#c25)

The suggested workaround is to add the following CSS:

{% highlight css %}
    * { max-height: 999999px }
{% endhighlight %}

But I've found it doesn't always work.