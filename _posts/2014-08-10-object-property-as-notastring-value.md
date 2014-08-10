---
layout: post
title: Object property as "not a string" value
published: true
categories: [javascript]
tags: [object, interesting]
---

JavaScript objects with !string keys issue. Worth a look.

{% highlight js %}
var foo = new Object();
var bar = new Object();
var map = new Object();

map[foo] = "foo"; // --> map["[Object object]"] = "foo";
map[bar] = "bar"; // --> map["[Object object]"] = "bar";
// NOTE: second mapping REPLACES first mapping!

alert(map[foo]); // --> alert(map["[Object object]"]);
// and since map["[Object object]"] = "bar",
// this will alert "bar", not "foo"!!
{% endhighlight %}

Try it out

<iframe width="100%" height="250" src="http://jsfiddle.net/Jim_Y/fffgohyy/embedded/result,js/presentation/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>