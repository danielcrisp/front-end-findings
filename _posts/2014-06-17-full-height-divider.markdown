---
layout: post
title:  "Full height column backgrounds"
categories: css
disqus: y
share: y
published: true
---

Sometimes you need a vertical dividing line between two floated columns, but the line must always be the same height as the tallest column. 
Or maybe you have two columns with different background colours and you want both columns to extend to the height of the container, regardless of their contents.

Previously the solution was using a repeating background image on the parent container to simulate a border or background.

Nowadays most of my projects only support IE8+ which means I can use a pure-CSS solution using the `:before` and `:after` pseudo-elements.

This is how to do it:

### Version 1 - Dividing border

#### HTML

{% highlight html %}
    <div class="container">
        <div class="left-column"></div>
        <div class="right-column"></div>
        <div class="clear"></div>
    </div>
{% endhighlight %}

#### CSS

{% highlight css %}
    .container {
        position: relative;
    }

    /* this creates the dividing line */
    .container:before {
        content: '';
        position: absolute;
        top: 0;
        left: 25%;
        width: 1px;
        height: 100%;
        background: blue; /* or you could use a border */
    }

    .left-column {
        float: left;
        width: 25%;
        height: 500px; /* just for example */
        background: #ccc;
    }

    .right-column {
        float: left;
        width: 75%;
        height: 800px; /* just for example */
        background: #eee;
    }

    .clear {
        clear: both;
    }
{% endhighlight %}

#### Demo

<a href="http://jsfiddle.net/danielcrisp/3L66P/" target="_blank">Demo on JSFiddle &raquo;</a>

<hr>

### Version 2 - Same height background

In this is example I have used `.clearfix` instead of `.clear`, but you can use whichever you prefer.

{% highlight html %}
    <div class="container">
        <div class="clearfix">
            <div class="left-column"></div>
            <div class="right-column"></div>
        </div>
    </div>
{% endhighlight %}

#### CSS

{% highlight css %}
    .container {
        position: relative;
    }

    /* this creates the background colour for the left column */
    .container:before {
        content: '';
        position: absolute;
        z-index: 1; /* make sure it is behind the column */
        top: 0;
        left: 0;
        width: 25%;
        height: 100%;
        background: red; /* our column background colour */
    }

    .left-column {
        position: relative;
        z-index: 2; /* make sure it is in front of the background */
        float: left;
        width: 25%;
        height: 200px; /* just for example */
        background: rgba(0, 0, 0, 0.2); /* so you can see where the column stops */
    }

    .right-column {
        float: left;
        width: 75%;
        height: 2000px; /* just for example */
        background: #eee;
    }

    .clearfix:before,
    .clearfix:after {
        content: " ";
        display: table;
    }

    .clearfix:after {
        clear: both;
    }
{% endhighlight %}

#### Demo

<a href="http://jsfiddle.net/danielcrisp/7drd9/4/" target="_blank">Demo on JSFiddle &raquo;</a>

<hr>

### Caveats

It is a nice solution that I've used in several projects but it does have some limitations:

 - Because it uses `:before` / `:after` you can't use `.clearfix` on the container, so you need to add another `<div>` unsemantic clearing element
 - You are limited to two dividing lines per container as we only have `:before` and `:after` available to us
 - The container element must be `position: relative;` which might be problematic if you have elements inside it that need to _escape_