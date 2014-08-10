---
layout: post
title: Vanilla.js class methods
published: true
categories: [javascript]
tags: [jquery, vanillajs]
---

jQuery's `addClass`, `hasClass`, `removeClass` and `toggleClass` methods are very useful, but sometimes, we do not want to import jQuery, but we would like to use these methods. In this post, i will share these little snippets to replace jQuery's methods with them.

## hasClass

{% highlight js %}
function hasClass( ele, cls ) {
  return ele.className.match(new RegExp('(\\s|^)' + cls + '(\\s|$)'));
}
{% endhighlight %}

## addClass

{% highlight js %}
function addClass( ele, cls ) {
  if ( !hasClass( ele, cls ) ) {
    ele.className += " " + cls;
  }
}
{% endhighlight %}

## removeClass

{% highlight js %}
function removeClass( ele, cls ) {
  if ( hasClass( ele, cls ) ) {
    var reg = new RegExp( '(\\s|^)' + cls + '(\\s|$)' );
    ele.className = ele.className.replace( reg, ' ' );
  }
}
{% endhighlight %}

## toggleClass

{% highlight js %}
function toggleClass( ele, cls ) {
  if( hasClass( ele, cls ) ) {
    removeClass( ele, cls );
  } 
  else {
    addClass( ele, cls );
  }
}
{% endhighlight %}

## Usage

jsfiddle/gist here