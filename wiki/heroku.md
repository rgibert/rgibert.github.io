# Heroku

## Deploying Docker Images

1. Create your Heroku application
~~~
heroku create APP_NAME
~~~
1. Log into the Heroku container registry
~~~
heroku container:login -a APP_NAME
~~~
1. Build & push the container image
~~~
heroku container:push -a APP_NAME web
~~~
1. Release the container
~~~
heroku container:release -a APP_NAME web
~~~
