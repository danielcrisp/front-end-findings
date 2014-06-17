---
layout: post
title:  "Responsive content inside iFrame"
categories: css responsive
disqus: y
share: y
---

I needed to find out if it was possible to embed a responsive site inside an iFrame whilst maintaining the responsive-ness of the target site.

Turns out it works but you need to make sure the host page has the following:

{% highlight html %}
    <meta name="viewport" content="width=device-width">
{% endhighlight %}

Otherwise you end up with the desktop view on iOS because the browser zooms out.

In order to fill the page so you can't see that the site is in an iFrame you can style the host page like this:

{% highlight css %}
    html, body {
        height: 100%;
    }
    body {
        margin: 0;
        overflow: hidden;
    }
    iframe {
        width: 100%;
        height: 100%;
        border: none;
    }
{% endhighlight %}

The target site will _respond_ according to the iFrame's dimensions. So if your iFrame is only 320px wide but the host page is 1280px wide you will see the mobile version of the site in the iFrame.

### Issues

Although not strictly related it seems that elements that use `-webkit-overflow-scrolling: touch;` in the target site will not be scrollable. I've noticed this behaviour on an iOS 7 iPad (tested using the iOS Simulator only). iOS 6.1 seems to work but the scrolling effect can be a bit jittery.

I've also found that iOS will sometimes crash or fail to completely load the target site. Again I have only been testing on the iOS Simulator and this only occured when the host page was on `localhost` but the target site was on the web. Using a local target site fixed the problem but of course this would be no good for production sites.

With IE7 I had two sets of scrollbars visible but it is probably possible to fix this.

### Browsers tested

**OSX:** Chrome v33, Chrome v35 (canary), Firefox v27, Safari v6

**Windows 7:** IE11, IE10, IE9, IE8

**Windows Vista:** IE7

**iOS:** Safari Mobile (iOS 6.1 and 7), Chrome v32, Opera Mini v7

Note: My test target site uses [Respond.js](https://github.com/scottjehl/Respond) to enable CSS3 Media Query support in older browsers.

Also note: My test target site does not support IE7 but it seems it worked anyway