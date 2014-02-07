---
layout: post
title:  "Galaxy S4 border-radius"
categories: css android bug
disqus: y
share: y
---

[caniuse.com](http://caniuse.com/#feat=border-radius) reports that an S4 does indeed support `border-radius` however you might find otherwise if you just use the following CSS:

{% highlight css %}
    border-radius: 10px;
{% endhighlight %}

In order to get it working on an S4 you need to specify the property like this:

{% highlight css %}
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
{% endhighlight %}

Go figure!

<sub>Credit: [http://stackoverflow.com/questions/17186158/galaxy-s4-stock-browser-css3-border-radius-support](http://stackoverflow.com/questions/17186158/galaxy-s4-stock-browser-css3-border-radius-support)</sub>