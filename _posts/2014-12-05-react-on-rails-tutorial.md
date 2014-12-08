---
layout: post
title:  "React on Rails Tutorial"
date:   2014-12-05 14:27:00
categories: react.js javascript
image: 'http://i.imgur.com/hG49emr.jpg'
---

React.JS is a JavaScript library that allows us to build reuseable components.  It is powerful, fast, and really easy to get started with. In contrast to full blown front-end MVC (Model View Controller) frameworks like Angular, Ember, and Backbone; React.js is only the view layer and actually can be used in any of those frameworks.  The learning curve for React.js isn't as steep as it is with MVC frameworks. With React.js we can replace particular components on our site, without having to rewire the whole front-end.  This makes it perfect for Rails.  Getting it setup on your Rails app is a lot easier than you might think too, in this post we will walk through that process.


To learn more about React.js and why you should consider it further check out [Learning React.js](http://scotch.io/tutorials/javascript/learning-react-getting-started-and-concepts) and [6 Reasons Why We Love React.js](http://www.syncano.com/reactjs-reasons-why-part-1/)

##Installing React.js

Add the gem to your gem file
{% highlight ruby %}
gem 'react-rails', '~> 1.0.0.pre', github: 'reactjs/react-rails'
{% endhighlight %}  

Run the installation script
{% highlight ruby %}
rails g react:install
{% endhighlight %}

Include the following in your application.js
{% highlight ruby %}
//= require react
//= require react_ujs
{% endhighlight %}


#Structuring React.js Files

Add the following into your application.js
{% highlight ruby %}
//= require_tree ./react/components
{% endhighlight %}

This will allow us to put our react components in 
{% highlight ruby %}
/app/assets/javascripts/react/components
{% endhighlight %}

##Implementing React.js

Creating out first React component is easy.  Create the following file `/app/assets/javascripts/react/hello_world.js.jsx`.  Inside of this file let's write the following code.

  {% highlight javascript %}
  {% raw %}
    /** @jsx React.DOM */

    var HelloMessage = React.createClass({
      render: function() {
        var welcome = 'Hello, ';

        return (
          <div>
            <h3>
              {welcome} { this.props.name }
            </h3>
          </div>
        );
      }
    });
  {% endraw %}
  {% endhighlight %}


Implementing react components in our rails view is very straightforward, and thanks to the react-rails gem it gives us a nice view helper called react_component.  To lay down our react component all we have to do is add the following to our view `<%=react_component('HelloMessage', name: 'world!')%>`

That's it!  Save your changes and refresh the page and you should have your first React Component!  Now you are ready to unleash the power of React.js!