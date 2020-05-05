---
title: Deploying Docker containers to Heroku
modified: 2020-05-04
tags: [docker, containers, heroku]
layout: post
---

Follow the below steps to deploy a docker image to Heroku

1. Create your Heroku application   
{% highlight bash %}
heroku create APP_NAME
{% endhighlight %}
2. Log into the Heroku container registry   
{% highlight bash %}
heroku container:login -a APP_NAME
{% endhighlight %}
3. Build & push the container image   
{% highlight bash %}
heroku container:push -a APP_NAME web
{% endhighlight %}
4. Release the container   
{% highlight bash %}
heroku container:release -a APP_NAME web
{% endhighlight %}
