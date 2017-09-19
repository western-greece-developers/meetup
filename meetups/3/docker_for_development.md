# Developing applications using containers/docker workshop

**Saturday 30th of September 2017 - POS coworking space - Patras**

## Prerequisites

- SSH Client
- Git
- Docker, docker-compose
- Text editor
- https://wgsdg.slack.com (Register here: https://wgsdg.herokuapp.com/)

## Setting up Ruby

Get the application code:

```
$ git clone https://github.com/jimmykarily/wgsdg_meetup_3_sample_app.git
$ cd wgsdg_meetup_3_sample_app
```

First requirement: Ruby

```
$ git checkout 3ac6184
$ docker build -t wgsdg development/.
$ docker run --rm -it wgsdg
```

or run irb inside a container to test:

```
$ docker run --rm -it wgsdg irb
```

## Setting up Rails

# TODO: Quick Intro to Rails

Requirements:
  - Vanilla Rails in place
  - Access to the source code directory

Add bundler to your Dockerfile and rebuild the image:

https://github.com/jimmykarily/wgsdg_meetup_3_sample_app/commit/5c9053456360df772a783b552fd245cac7ab4edf#diff-c92a9f5278c2a9463788c4ddf11d871c

Tip: `docker build -t wgsdg development/.`

Setup Rails:

```
$ docker run --rm -it -v $PWD:/usr/src/app wgsdg
container> gem install rails
container> rails new -s -B .
container> bundle install --path=/usr/src/app/bundle_cache/
container> exit
$ pushd development && docker-compose up -d && popd
```

Open `http://localhost:3000/` on your browser (or curl it)

TIP: You can skip this section with:

```
$ git checkout 5c90534
$ docker build -t wgsdg development/.
```

## Add PostgreSQL

- Add PostgreSQL dependency in your Dockefile and rebuild the image.
- Add a model to get stored in the database.
- Add PostgreSQL in your docker-compose.yml.

TIP: Skip this section with:

```
$ git checkout fa89965
$ docker build -t wgsdg development/.
```

## Add Redis

- Add redis gem
- Add Redis in docker-compose file
- Add methods to use redis

TIP: Skip the section with:

```
$ git checkout 8d93c9c
$ docker build -t wgsdg development/.
```

## Add background workers (Sidekiq)

- Add sidekiq gem
- Add worker
- Add background workers container
- Add jobs
- Check result

TIP: Skip this section with:

```
$ git checkout f5958c8
$ pushd development && docker-compose up -d && popd
```

## Containerize your test suite

```
$ git checkout a618e71
$ ./development/dex bundle exec rails test
```

## Make it automatic

```
$ git checkout f50aa28
$ ./development/dex bundle
$ pushd development && docker-compose up -d && popd
```

## Share your environment with your team

- Use the commit id as the image tag and push it
- Benefits:
  - Easier QA
  - Save time by using a local registry (people will just pull the images instead of building them)

## Improvisation: Containerize your own application

Ask for help if you need it :)
