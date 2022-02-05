---
title: Cloud
---

# Google Cloud

## Get All IAM Policies For a Service Account

~~~ bash
gcloud \
    projects \
    get-iam-policy \
    ${project_name} \
    --flatten="bindings[].members" \
    --format="table(bindings.roles)" \
    --filter="bindings.members:${service_account}"
~~~

# Heroku

## Deploying Docker Images

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

## Deploying Python Applications

1. Add control / metadata files
    - app.json
    ~~~ json
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
~~~ bash
git commit -am 'add Heroku files'
~~~
1. Log into Heroku
~~~ bash
heroku login
~~~
1. Create your Heroku application
~~~ bash
heroku create APP_NAME
~~~
1. Push your branch (if master you can just use 'heroku master') for deployment
~~~ bash
git push heroku BRANCH:master
~~~
