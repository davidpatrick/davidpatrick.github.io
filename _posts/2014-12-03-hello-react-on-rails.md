---
layout: post
title:  "Hello, React on Rails!"
date:   2014-12-03 04:27:00
categories: react.js javascript
image: 'http://i.imgur.com/hG49emr.jpg'
---
React.js

#Installing React.js

1. Add the gem to your gem file

  `gem 'react-rails', '~> 1.0.0.pre', github: 'reactjs/react-rails'`

2. Run the installation script

  `rails g react:install`

3.  Include the following in your application.js

{% highlight ruby %}
//= require react
//= require react_ujs
{% endhighlight %}


#Structuring React.js Files

Add the following into your application.js

  `//= require_tree ./react/components`

This will allow us to put our react components in 

  `/app/assets/javascripts/react/components`

#Implementing React.js

First we are going to want to create our first React component.  First create  `/app/assets/javascripts/react/hello_world.js.jsx`.  Inside of this file lets paste the following code

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


Implementing react components in our rails view is very straightforward.  Thanks to the react-rails gem it gives us a nice view helper `<%=react_component('HelloMessage', name: 'world!')%>`

And that's it!  Save your changes and refresh the page and you should have your first React Component!
    
    
  