---
layout: post
title:  "WebKit border-radius bumpy edges"
categories: webkit css android
disqus: y
share: y
---

Older versions of WebKit do not render borders correctly when combining `border-radius` and a large border width.

The following code creates a large black border masking a yellow square. This in itself is a workaround because certain versions of WebKit (Android) don't honour `overflow: hidden;` with `border-radius`, so you can't just _crop_ the contents of a `div` as it were.

#### HTML

{% highlight html %}
    <div class="container">
        <div class="mask"></div>
    </div>
{% endhighlight %}

#### CSS

{% highlight css %}
    .container {
        display: block;
        position: relative;
        width: 400px;
        height: 400px;
        background: yellow;
        overflow: hidden;
    }
    
    .mask {
        position: absolute;
        top: -950px;
        right: -950px;
        bottom: -950px;
        left: -950px;
        border: 1000px solid black;
        
        border-top-left-radius: 100%;
        border-top-right-radius: 100%;
        border-bottom-left-radius: 100%;
        border-bottom-right-radius: 100%
    }
{% endhighlight %}

So, what should look like this:

![Correct]({{ site.url }}/images/posts/border_radius_correct.png)

Looks like this, pretty but not what I'm after:

![Incorrect]({{ site.url }}/images/posts/border_radius_incorrect.png)

Here is a fiddle with the above code:

<iframe width="100%" height="300" src="http://jsfiddle.net/danielcrisp/uKN88/embedded/html,css,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

The fix is to reduce the border width... if you can.

My border width of 1000px is obviously completely unnecessary, so I can reduce it to about 85px and the problem is sorted (almost, its not perfect but its much better).

The <strike>fixed</strike> improved version:

<iframe width="100%" height="300" src="http://jsfiddle.net/danielcrisp/uKN88/3/embedded/html,css,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Of course this only helps you if you _can_ reduce the border width.