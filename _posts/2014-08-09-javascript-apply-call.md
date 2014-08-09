---
layout: post
title: JavaScript apply and call
published: true
categories: [javascript, programming]
tags: [apply, call]
---

## Apply

The apply() method calls a function with a given `this` value and arguments provided as an **array**. NOTE: While the syntax of this function is almost identical to that of call(), the fundamental difference is that call() accepts an argument list, while apply() accepts a single array of arguments. This difference kicks in when we need arrays instead of independent values. Such a function is `mergeAll` which flattens arrays and works only for array arguments.

## Call

The call() method calls a function with a given `this` value and arguments provided individually. With call, you can write a method once and then inherit it in another object, without having to rewrite the method for the new object. This function is usuful when you want to imitate multiple inheritance on an object. Its somehow like mixins. In JavaScript inheritance you can assign the prototype property only to a single object, but you can use call() to inherit other classes members.

```javascript
// first superclass
function superClass( name, other ) {
    this.name = name || "superclass1";
    this.other = other || "someproperty1";
}

// second superclass
function superClassOther(name, other) {
    this.otherName = name || "superclass2";
    this.other = other || "someproperty2";
}

// subclass
function myClass(ownProperty, name, other) {
    this.ownProperty = ownProperty;
    superClass.call(this, name);
    superClassOther.call(this, name);
}

var my = new myClass("myOwnPropertyValue", "sub", 2);
// expect(my.name).to.be('sub')
// expect(my.otherName).to.be('sub')
// expect(my.other).to.be('someproperty2')
alert(my.name + " " + my.otherName + " " + my.other);
```