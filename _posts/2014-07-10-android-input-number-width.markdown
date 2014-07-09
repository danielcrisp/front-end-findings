---
layout: post
title:  'Android renders input[type="number"] the wrong width'
categories: css quirk
disqus: y
share: y
published: true
---

I recently had a strange problem where some number input boxes weren't filling the available space.
It was fine in every other browser I tested.

Turns out there is an `outer-spin-button` that affects the layout.

The quick fix is:

{% highlight css %}
    input[type=number]::-webkit-outer-spin-button { 
        margin: 0;
    }
{% endhighlight %}

Once again StackOverflow saves the day:

Source: [http://stackoverflow.com/questions/20766418/when-input-type-number-android-browsers-render-the-input-box-smaller](http://stackoverflow.com/questions/20766418/when-input-type-number-android-browsers-render-the-input-box-smaller)