---
title: Deploying Docker Images on Heroku
tags:
    - cloud
    - heroku
    - docker
---

# Deploying Docker Images on Heroku

1. Log into Heroku
~~~ bash
heroku login
~~~
1. Create your Heroku application
~~~ bash
heroku create APP_NAME
~~~
1. Log into the Heroku container registry
~~~ bash
heroku container:login -a APP_NAME
~~~
1. Build & push the container image
~~~ bash
heroku container:push -a APP_NAME web
~~~
1. Release the container
~~~ bash
heroku container:release -a APP_NAME web
~~~
