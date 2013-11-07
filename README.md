Rails meets Docker
==================

Here is everything you need to build the Docker image from the [Rails meets Docker](http://blog.gemnasium.com/post/65599561888/rails-meets-docker) blog post.

This repository contains:

* a Dockerfile and some files needed for the build
* some scripts to build, run and publish your "rails-getting-started" Docker image

Here are the files referenced by the Dockerfile:

* scripts/start
* scripts/setup

These scripts are for the image you build using Docker. The others are for you!

Prerequisite
------------

Get and [install Docker](http://www.docker.io/gettingstarted/)!

You also need a profile on the [Docker Index](https://index.docker.io/) in order to push your images.

You should be able to run the `docker` command line without `sudo`. Otherwise you will have to make some adjustments.

Usage
-----

Clone this repository, enter the directory, and "prepare":

```
$ git clone https://github.com/gemnasium/rails-meets-docker.git
$ cd rails-meets-docker
$ ./prepare
```

It will clone the [Getting Started Rails application](https://github.com/rails/docrails/tree/master/guides/code/getting_started) locally.

Now, export you Docker login or use a fake one:

```
$ export DOCKER_LOGIN=fcat
```

You should then be able to build the "rails-getting-started-image":

```
$ ./build
...
19b49aad2eff
```

Here is the new image:

```
$ docker images | grep getting-started
fcat/rails-getting-started   latest   19b49aad2eff ...
```

We can now fire a new container based on this image:

```
$ ./run
c035bf447200
```

The container runs in the background.

Visit `http://localhost:5000/` with your web browser.
You should be able to connect to the Rails application.

Your "rails-getting-stared" image can be pushed to the [Docker Index](https://index.docker.io/):

```
$ ./push
```

There's also a script to start the container in console mode. Then you can make some changes to the Rails application. Let's say you are turning pirate, like in the [blog post](http://blog.gemnasium.com/post/65599561888/rails-meets-docker):

```
$ ./console
rails@c4ee37242238:/$ vim /rails/app/views/welcome/index.html.erb
rails@c4ee37242238:/$ exit
```

When this is done, you can commit your changes as a new image:

```
$ ./commit c4ee37242238
5502dd9b6a8d
```

The new image should be there:

```
$ docker images | grep pirate
fcat/rails-getting-started-pirate   latest  5502dd9b6a8d ...
```

And now, you can be a pirate everyday:

```
$ ./run-pirate
```

