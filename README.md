# RAILS 6 SANDBOX IN DOCKER

A docker setup for a simple Rails 6 Application running with postgres.
I've set it up to work with Bootstrap as well as described on my blog [Bootstrap 5 with Rails 6](https://whatapalaver.co.uk/bootstrap-5-rails-6)
To be used to spin up mini apps for testing.

The base application was create (with minor tweaks) from a Nick Janetakis blog post - [Dockerizing Ruby Tutorial](https://semaphoreci.com/community/tutorials/dockerizing-a-ruby-on-rails-application#:~:text=Creating%20a%20Rails%20Image,that%20is%20easy%20to%20read.)

## Local setup

Prepare environment, for dev version you can use the example environment:

`$ cp env-example .env`
Start the server:

`$ docker-compose up --build`
Browse http://localhost:8010

You will need to set up the rails database:

`$ docker­-compose run --­­user "$(id ­-u):$(id -­g)" sandbox rake db:reset`
`$ docker­-compose run --­­user "$(id ­-u):$(id -­g)" sandbox rake db:migrate`

## Working with Rails in docker

All you commands need to be prefixed with `docker­-compose run --user "$(id ­-u):$(id -­g)" sandbox`
eg. to get the console up `docker­-compose run --­­user "$(id ­-u):$(id -­g)" sandbox rails c`

## Production image

Prepare production environment, set you production values:

`$ cp env-example .env`
Build an image:

nginx: http server
`$ docker build --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) -t $DOCKER_USERNAME/dockerizing-ruby-nginx:latest -f Dockerfile.nginx .`
