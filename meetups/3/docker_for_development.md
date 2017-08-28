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
$ docker build -t wgsdg .
$ docker run --rm -it wgsgd
$ docker run --rm -it wgsgd irb
```

## Setting up Rails

Requirements:
  - Vanilla Rails in place
  - Access to the source code directory

Add bundler to your Dockerfile and rebuild the image:

https://github.com/jimmykarily/wgsdg_meetup_3_sample_app/commit/5c9053456360df772a783b552fd245cac7ab4edf#diff-c92a9f5278c2a9463788c4ddf11d871c

Tip: `docker build -t wgsdg .`

Setup Rails:

```
$ docker run --rm -it -v $PWD:/usr/src/app wgsdg
container> gem install rails
container> rails new -s -B .
container> bundle install --path=/usr/src/app/bundle_cache/
container> exit
$ docker-compose up -d
```

Open `http://localhost:3000/` on your browser

TIP: You can skip this section with:

```
$ git checkout 5c90534
$ docker build -t wgsdg .
```
