# Heroku

## Deploying Docker Images

1. Log into Heroku
~~~
heroku login
~~~
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

## Deploying Python Applications

1. Add control / metadata files
    - app.json
    ~~~
    {
        "name": "NAME",
        "description": "DESCRIPTION",
        "repository": "HTTP_PATH_TO_REPO",
        "logo": "HTTP_PATH_TO_LOGO",
        "keywords": [ "KEYWORD1", "KEYWORD2"]
    }
    ~~~
    - Profile
    ~~~
    web: gunicorn WSGI_CLASS_TO_LOAD:app
    ~~~
    - update requirements.txt to add
    ~~~
    gunicorn
    ~~~
    - runtime.txt
    ~~~
    python-3.8.3
    ~~~
~~~
git commit -am 'add Heroku files'
~~~
1. Log into Heroku
~~~
heroku login
~~~
1. Create your Heroku application
~~~
heroku create APP_NAME
~~~
1. Push your branch (if master you can just use 'heroku master') for deployment
~~~
git push heroku BRANCH:master
~~~
