---
layout: post
title: Parameterized event handlers
published: true
categories: [javascript]
tags: [events, bind]
---

I found an interesting issue today, while coding some educational stuff at my work. The excercise was really simple, and easy, so i finished it fast. The task was to attach some click events to a bunch of buttons, and make a *location* forward in the handler. The target url was queried. First, i made some really basic event listeners with anonimous handlers, and to be honest these made their job well. However, i made my mind around, and realized, that attaching anonimous event handler functions in a loop is not memory friendly, becouse in every loop i create a new function object, instead using only one (i.e polluting the GC). I really wanted to solve this issue, despite it was not important to think about memory issues.

## Preface and Solvation

My first version was:

```javascript
var aButtons = document.getElementsByClassName('a'),
    bButtons = document.getElementsByClassName('b'),
    cButton = document.getElementById('c'),
    dDropdown = document.getElementById('d');

for(var i = 0; i < aButtons.length; ++i) {
  
  aButtons[i].addEventListener('click', function(event) {
    var target = event.target,
        queryParam = target.getAttribute("data-myImportantValue");

    window.document.location.href = 'localhost:myport/myservice/..etc/myFun&query=' + queryParam;
    return false;
  });

}
```

So i wanted to give a named (and parameterized) function as a handler insted of creating new anonimous functions. The problem was, that i was not able to pass the reference of the caller to the function as a `thisArg` with this syntax:

```javascript
elements[i].addEventListener( 'click', handler.bind(thisArg, param1, param2, ...) );
```

One possible solvation could be:

```javascript
elements[i].addEventListener( 'click', handler.bind(elements[i], param1, param2, ...) );
```

But there is code duplication here, so a better aprroach could be:

```javascript
elements[i].addEventListener( 'click', handler.bind(null, param1, param2, ...) );
```

Why? Becouse `addEventListener` attach the event object to the handler automatically, so the handler could be written as:

    function handler(param1, param2, ..., ev) { }

where `ev` stand for the original event object.