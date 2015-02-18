---
layout: api
title: "OAuth2 Authentication - Beta"
slug: "OAuth2"
category: basics
date: 2014-02-20 11:22:06
---

We are working on bring OAuth authentication to the OnePageCRM API.

To use the OAuth authentication, you will need to register an application.

To register an application, visit

`app.onepagecrm.com/oauth/applications`

Create your application and set a callback URL.

When you create your app, you will be show two long strings, your application id and secret.

Use these to test with your OAuth2 client.

The first step is to authorize the client. The exact steps will depend on your OAuth2 client, but here are the steps I've used with the ruby [OAuth2][1] gem

Install the OAuth2 gem:
`gem install oauth2`

Fire up a terminal and require this gem:
`irb -r oauth2`

Set the callback_url, app_id and secret variables:

{% highlight ruby %}
  callback = "http://yourapp/callback"
  app_id = "2a514a754809f926b2c0fe4bb2f5f29adfa2684331b433f468f8fa4b8dbb20d5"
  secret = "ac516ef825cfc0f57f0b679dc8c2a0cf6eb79163d9b74708a205a4504b4b2a48"
{% endhighlight %}

Set up the client:
{% highlight ruby %}
 client = OAuth2::Client.new(app_id, secret, site: "http://app.onepagecrm.com/")
{% endhighlight  %}

Get redirect URL
{% hightlight ruby %}
 client.auth_code.authorize_url(redirect_uri: callback)
  => "http://yourapp/oauth/authorize?response_type=code&client_id=2a514a754809f926b2c0fe4bb2f5f29adfa2684331b433f468f8fa4b8dbb20d5&redirect_uri=http%3A%2F%2Flocalhost%3A3001%2Fauth%2Ftodo%2Fcallback"
{% endhightlight %}

Redirect to this URL and authorize the app. You must be logged in to OnePageCRM for this to work.
When you click authorize, you will be brought back to your callback url, with an access token parameter.

Use this access token in subsequent requests to access the API.


  [1]: https://github.com/intridea/oauth2


