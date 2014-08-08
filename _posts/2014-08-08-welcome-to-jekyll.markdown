---
layout: post
title:  "Welcome to Jekyll!"
date:   2014-08-08 14:34:46
categories: jekyll update
---

You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

{% highlight javascript %}
var _tasks = w('.task');

[].forEach.call(_tasks, function(task) {

  task.addEventListener('click', function(event) {
    // ajax returns a Promise object
    var promise = w.ajax({
      url: 'backend/get',
      type: 'GET',
      contentType: "text/html"
    });

    promise.onFulfill(function(result) {
      // onfulfill
    });

    promise.onReject(function(err) {
      // onrejection
    });
  });

});
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll]:    http://jekyllrb.com
