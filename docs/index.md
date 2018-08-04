# How Do I Heroku?

How do I use heroku? How do I deploy python apps? ruby apps? bots? How do I push to deploy with heroku? How do I set up custom domains with heroku?

A how-to guide for using heroku.

HTML pages for this tutorial (you are here): <https://pages.charlesreid1.com/how-do-i-heroku/>

Source code for this tutorial: <https://git.charlesreid1.com/charlesreid1/how-do-i-heroku>

Mirror on Github: <https://github.com/charlesreid1/how-do-i-heroku>


## Frequently Asked Questions

### Basics: What is heroku and how do I use it?

Heroku is a service that offers to run your code in the cloud.

In practice, this means that you can provide Heroku with a packaged
application, in your language of choice, and have Heroku deploy
and run the packaged application on their servers.

(This is similar to Google App Engine.)

The one catch is that your application is run as a stateless application,
meaning it cannot write to or read from disk dynamically; Heroku must 
be able to tear it down and restart it from scratch.

### Basics: heroku paid vs free accounts

The paid tier gets you access to machines (dynamos) with more resources,
and prevents your apps from shutting off or "spinning down" after a period
of inactivity.

The difference is not that significant, but _is_ important for _some_ applications.

### Basics: installing heroku

Heroku offers a command line interface. To install it, see the page below:

[**Installing the heroku toolbelt**](toolbelt.md) - a guide to installing the
Heroku toolbelt and getting it set up.

### Python: how do I deploy python apps to heroku?

If you want to deploy a Python application to Heroku, it is recommended that you
write a Flask application as the backend service, and wrap it with Gunicorn
on the frontend.

Basically, Flask is a simple, single-threaded application that is intended
for prototyping but doesn't do very well as a production service. Gunicorn
acts as middleware, more gracefully handling connections from clients and 
making requests to the Flask app on their behalf.

[**Deploying flask apps on heroku**](flask.md) - a customizable python server

### Python: how do I use OAuth from a flask application on heroku?

If you are using flask as your web server, there are many libraries
that plug in to flask and offer OAuth authentication with various
third-party API services.

One that provides authentication with a variety of services is
[flask-dance](https://github.com/singingwolfboy/flask-dance.git).
This adds a blueprint (basically, a set of routes at `/login`)
to the Flask app.

This enables your app to request permissions from the user,
have the user authenticate with Github, and gain access
to the information about the user that you requested.

[**Deploying Github OAuth flask app on heroku**](github_flaskdance.md) - authenticating users 
and controlling access to web content via github-based means (i.e., organization/team membership).

### Push to Deploy: how does push-to-deploy work with heroku?

Before you begin, install the heroku toolbelt:

[**Installing the heroku toolbelt**](toolbelt.md) - a guide to installing the
Heroku toolbelt and getting it set up.

Make sure you are authenticated:

```
heroku login
```

Now from your git repository, add your Heroku project as a git remote:

```
heroku git:remote -a my-cool-heroku-project
```

The github repository will now have a remote named `heroku`.

Locally, the repository will have a branch named `heroku-pages`
that will store all of the actual content being deployed to Heroku.
(This is the only branch deployed to Heroku, all others are ignored.)

On Heroku, this branch is called `master`, so the heroku command above
keeps this from getting overly confusing. It sets up the branch
`heroku-pages` to track the branch `master` on the `heroku` remote.

Now, when you're ready to deploy, you add/commit changes to the
`heroku-pages` branch. Then you just push the `heroku-pages` branch
on your local machine to the `master` branch on the Heroku remote
with the command:

```
git push heroku heroku-pages:master
```

### Example: protecting a page with flask-oauth-dance

Also see the answer to the OAuth question above.

[**Deploying Github OAuth flask app on heroku**](github.flask.md) - authenticating users 
and controlling access to web content via github-based means (i.e., organization/team membership).

### Databases: how do I use an SQL database with a heroku app?

(TODO)

### Custom Domains: how do I set up custom domains with heroku?

(TODO)

### Custom Domains + SSL: how do I set up https with a custom domain?

(TODO)

