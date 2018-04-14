---
layout: post
title: Blocitoff
thumbnail-path: "img/blocitoff.png"
short-description: An application that creates self-destructing to-do lists.

---

{:.center}
![]({{ site.baseurl }}/img/blocitoff.png)

##Summary
Blocitoff is an application that allows users to create self-destructing to-do lists. It helps motivate users and keep lists manageable by automatically deleting to-do items more than seven days old.

##Explanation
Blocitoff allows users to do the following:
1. Sign in and out of Blocitoff
2. View their profile page
3. Create multiple to-do items and have them appear immediately
4. Mark to-do items as completed and have them deleted immediately
5. See how old items are with items older than 7 days deleted automatically

##Problem
The main issue I had in implementing creation and deletion of items was having both actions occur immediately using AJAX without the need for reloading a page. Having worked with Ruby and Ruby on Rails for awhile, I had to refresh myself on frontend DOM manipulation.

##Solution
After implementing my create and destroy solutions, I was able to create and delete items, which I was able to verify using my local server.

{% highlight javascript %}

$('.js-items').empty().append("<%= j render(@item) %>");
$('.new-item').html("<%= j render partial: 'items/form', locals: { item: @new_item } %>");

{% endhighlight %}

However, both actions were still not updating on the user profile page without refreshing. I was able to fix this issue by adding both the AJAX and jQuery CDNs on the application view via script tags.

##Results
After implementing both script tags, item creation and deletion work immediately without requiring a page reload. Everything works as expected.

##Conclusion
This was my second backend specialization project as a part of the Bloc curriculum, and gave me another chance to work with Ruby on Rails as well as refresh my skills with frontend DOM manipulation.
[Click here](https://github.com/thejonlee/blocitoff) to access the code repository on Github.
