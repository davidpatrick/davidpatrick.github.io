---
layout: post
title:  "Custom Filters in Angular"
date:   2014-10-21 00:01:00
categories: angular javascript
image: 'http://i.imgur.com/mPoMR6l.jpg'
---

In Angular using the [https://docs.angularjs.org/api/ng/filter/filter](filter) in views can be pretty straight forward when wanting to search for key terms, but what about when we want to do some thing a little more involved? What about Filter that does not equal data? In this post I am going to describe how you can build a custom filter that will let us dive a little more into the data.


### Filtering Out Records
Basically to create a custom filter, we create a function that we pass data into and return true or false.  To filter out records that don't match a specific set of data we need to build a custom function that will evaluate our records and then pass that function into the filter.


Let's goto our `view-controller.js` and add our custom function that will evaluate the records passed into it.

```
$scope.removeSelectedFriends = function(friend) {
  return (friend.id !== $scope.selectedFriendOneId && friend.id !== $scope.selectedFriendTwoId);
};
```
Here we are binding our custom function to our $scope variable `removeSelectedFriends`.  This function takes a friend object and compares it's `id` against the selected friends and returns true or false. This allows us to prevent our user from selecting the same friend twice.


In our view we will have:

{% highlight html %}
{% raw %}
  <a class="friend"
     collection-repeat="friend in friends | 
     filter: removeSelectedFriends">
     {{friend.name}}
</a>
{% endraw %}
{% endhighlight %}


Since we bound our function to `$scope.removeSelectedFriends`, we can now just pass in removeSelectedFriends to the filter and it will evaluate every recod in the friends collection with our custom function.

### Adding multiple filters
I still want my users to be able to search their friends list, to add additional filters you just separate them with an additional pipe.  My final code looks something like this:

{% highlight html %}
{% raw %}
  <a class="friend"
     collection-repeat="friend in friends
     | filter: data.search
     | filter: removeSelectedFriends">
     {{friend.name}}
</a>
{% endraw %}
{% endhighlight %}


