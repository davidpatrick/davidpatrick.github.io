---
layout: post
title:  "Creating a Launch Page with Angular + Mailchimp"
date:   2014-12-08 01:27:00
categories: angular javascript
image: 'http://i.imgur.com/ZF8GFdm.png'
---

# Using Angular & Mailchimp for your Launch Page

This tutorial we are going to create a landing page for our potential customers to fill in their email, using HTML, Angular, and Mailchimp.  The resources available to Angular developers is amazing. We will be using an [Angular Module for Mailchimp](https://github.com/keithio/angular-mailchimp). If you are familair with Ruby on Rails, Angular Modules are very much like Ruby Gems.

## What's Required?
You will already need to have [Node Package Manger](http://www.nodejs.org) and [Bower](http://www.bower.io) installed on your machine.  If you have never used these tools before, you are in for a wonderful surprise.


## First Step - Create the Skeleton
We are going to build this launch page off a free template from [BlackTie](http://www.blacktie.co/2014/03/counter-coming-soon-page/).  [Download](https://dl.dropboxusercontent.com/u/105401917/BlackTie/counter.zip) this template and extract it into a new directory.

## Second Step - Install Angular components
Open up terminal and CD into the directory that contains the index.html you just extracted. Run the following commands:

{% highlight javascript %}
bower install angular
bower install angular-mailchimp
bower init
{% endhighlight %}

To include what Bower just downloaded for us, copy the following html into your `<head></head>`
{% highlight javascript %}
<script src="bower_components/angular/angular.min.js"></script>
<script src="bower_components/angular-mailchimp/angular-mailchimp.js"></script>
<script src="bower_components/angular-resource/angular-resource.min.js"></script>
<script src="bower_components/angular-sanitize/angular-sanitize.min.js"></script>
<script src="js/app.js"></script>
{% endhighlight %}

## Third Step - Loading Angular
To load our Angular App and inject the mailchimp module, it's as easy as writing the following code into our `<head></head>`.

{% highlight javascript %}  
<script type="text/javascript">
  angular.module("productLaunch", ["mailchimp"])
</script>
{% endhighlight %}

Here we are defining the name of our app *productLaunch* and injecting the module *mailchimp*.  Next we will load the app by passing our app name to the ng-app directtive  `<body ng-app="productLaunch">`.  This allows us to use the Mailchimp module anywhere inside of our body.

##Fourth Step - Setting up Mailchimp
To learn how to use the Mailchimp module visit [angular-mailchimp](https://github.com/keithio/angular-mailchimp). This will walk you through putting in your credentials for your Mailchimp account.  Which is basically filling out the following 4 hidden input fields
{% highlight javascript %}
<input class="hidden" type="hidden" ng-model="mailchimp.username" ng-init="mailchimp.username=''">
<input class="hidden" type="hidden" ng-model="mailchimp.dc" ng-init="mailchimp.dc=''">
<input class="hidden" type="hidden" ng-model="mailchimp.u" ng-init="mailchimp.u=''">
<input class="hidden" type="hidden" ng-model="mailchimp.id" ng-init="mailchimp.id=''">
{% endhighlight %}

The Mailchimp module gave us a new controller MailchimpSubscriptionCtrl. Let's add it to the following
{% highlight javascript %}
<section id="header" ng-controller="MailchimpSubscriptionCtrl">
{% endhighlight %}

This will allow us to manipulate the content inside of this section based off what happens with the Mailchimp Subscription Controller.  Let's start by making the "Let Me Know When You Launch" text smarter with ng-hide and ng-show.
{% highlight javascript %}
<h4 ng-hide="mailchimp.result ==='success'">LET ME KNOW WHEN YOU LAUNCH</h4>
<h4 ng-show="mailchimp.result ==='success'">THANKS FOR SIGNING UP!</h4>
{% endhighlight %}

Let's also hide the input box when mailchimp has a successful response.
{% highlight javascript %}
<form class="form-inline" role="form" ng-hide="mailchimp.result === 'success'">
{% endhighlight %}

We can also add a Mailchimp error message to the page.  Add the following after your submit button
{% highlight javascript %}
<div ng-show="mailchimp.result === 'error'">
  <p ng-bind-html="mailchimp.errorMessage" class="error"></p>
</div>
{% endhighlight %}

Now to hook in our form on the page to the our mailchimp module we need to add `ng-model="mailchimp.email"` to our input for the email and hookup the submit button.
{% highlight javascript %}
<input type="email" class="form-control" id="exampleInputEmail2" placeholder="Enter email" ng-model="mailchimp.email">
<button type="submit" class="btn btn-info" ng-disabled="MailchimpSubscriptionForm.$invalid" ng-click="addSubscription(mailchimp)" type="submit" value="SIGN UP" disabled="disabled">Submit</button>
{% endhighlight %}

That's it!  You are good to go.  This page can not be tested by simply opening up the file, it needs to be served to test it.  I am using Jekyll to run a local webserver, which is what Github pages uses, which will be the hosting platform for this landing page.  If you want to know more about Jekyll please check my first blog post about [starting a blog](http://dponrails.com/jekyll/poole/ruby/2014/09/15/staring-a-blog-with-jekyll.html).

You can view the code for this tutorial at [https://github.com/davidpatrick/angular-mailchimp-landing](https://github.com/davidpatrick/angular-mailchimp-landing)