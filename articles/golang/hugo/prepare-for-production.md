# Rails: Prepare for production
After you have an application (app) running locally in a development (dev) environment with nanobox, and you've developed it to a point where you're beginning to think about production, nanobox can help you test your app as if it were running in production using the simulation (sim) environment.

This guide is broken down into three sections:

1. [Dev vs Sim](dev-vs-sim)
2. [Setting up sim](setting-up-a-sim-environment)
3. [Sim: up and running](sim-up-and-running)

## Dev vs. Sim
The nanobox dev environment is just that. It's a local running instance of your app. It doesn't compile assets or run a web server.

The nanobox sim environment is an exact replica of a production environment running locally. All this means is your app will run in sim as if it were running in production, just not on a live server. If your app runs in `sim` *it will run in production*. Guaranteed.

## Setting up sim
You use `nanobox sim` in the same way you use `nanobox dev`, it just needs a little extra setup. Add a web component to your `boxfile.yml` like in the following example:

#### Adding a web server
```yaml
# because we're using hugo we need to tell nanobox that we need golang in our
# container
code.build:
  engine: "golang"

# specify that we need a data component (called "db"); for this example we'll
# use postgresql as our database
data.db:
  image: nanobox/postgresql

# we need to specify a web component to run our app in and tell nanobox how to
# start our server
web.site:
  start: 'hugo server --baseUrl=hugo.nanobox.dev --bind=0.0.0.0 --port=8080'
```

## Sim: up and running
With our sim environment created and deployed lets test it!

```bash
# build a golang runtime
nanobox build

# compile the app
nanobox compile

# add a convenient way to access your app from a browser
nanobox sim dns add hugo.nanobox.sim

# deploy the golang runtime into the sim environment
nanobox sim deploy
```

Visit the app from your favorite browser at: `hugo.nanobox.sim:8080`

## Now what?
With an app running in a sim environment with nanobox, whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Launch your app](launch-your-app.html)
* [Back to hugo overview](overview.html)