---
title: "A Simple Finatra Example Project"
date: "2015-07-12T21:50:36-07:00"
draft: false
tags: ["finatra", "scala"]
---

Over the past year-and-a-half I've helped to develop a [Scala](https://www.scala-lang.org/) framework for writing services on-top of parts of the Twitter stack, namely [twitter-server](https://github.com/twitter/twitter-server) and [Finagle](https://github.com/twitter/finagle). This framework is called [Finatra](https://github.com/twitter/finatra) and we've recently published a [second milestone release](https://oss.sonatype.org/#nexus-search;gav~com.twitter.finatra~~2.0.0.M2~~) of the completely-rebuilt-from-the-ground-up version 2.x.

I recently wrote a small [Finatra](https://github.com/twitter/finatra) example service that is a [simple URL-shortener](https://github.com/cacoco/smally-finatra) using [Redis](https://redis.io/). The example builds with [sbt](https://www.scala-sbt.org/) and can be easily deployed to [Heroku](https://heroku.com).

<!-- more -->
<p/><p/>
#### The [`smally-finatra`](https://github.com/cacoco/smally-finatra) service.<p/>

At a high-level, the service accepts JSON input through a POST endpoint that represents the URL to be shortened. It then returns a JSON response with the shortened representation of the URL. The service also then supports GET requests to a shortened URL returning a 301 response to the expanded URL. Browsers will generally follow this redirect by default, thus it's simplest to just hit the shortened URL in a browser window.

The service uses [Jedis](https://github.com/xetorthio/jedis) as a client to Redis. We set up a server that looks like this:

```gist {cols="8", id="e6b93886631988350abb"}
  https://gist.github.com/cacoco/e6b93886631988350abb
```

You'll notice we configure a few [modules](https://github.com/twitter/finatra/blob/master/inject/inject-core/src/main/scala/com/twitter/inject/TwitterModule.scala) here. The Finatra `LogbackModule` which sets [`logback`](https://logback.qos.ch/) as our logging implementation for [slf4j](https://www.slf4j.org/). A `JedisClientModule` which configures the Jedis client to talk to a Redis server. And a generic sounding, `SmallyModule`. The last module defines business-logic configuration for the service. In this case, you can choose to always return `https` protocol shortened URLs. The `SmallyModule` defines a flag which you can set on the command line to toggle this behavior. The default is false.

We then configure the [`HttpRouter`](https://github.com/twitter/finatra/blob/master/http/src/main/scala/com/twitter/finatra/http/routing/HttpRouter.scala), setting up a few filters including the Finatra [`CommonFilters`](https://github.com/twitter/finatra/blob/master/http/src/main/scala/com/twitter/finatra/http/filters/CommonFilters.scala). We then add the `SmallyController` and a custom [`ExceptionMapper`](https://github.com/twitter/finatra/blob/master/http/src/main/scala/com/twitter/finatra/http/exceptions/ExceptionMapper.scala).

Now, let's look at the controller:

```gist {cols="8", id="4abd49ac71e7a2bd3b23"}
  https://gist.github.com/cacoco/4abd49ac71e7a2bd3b23
```

The controller defines two endpoints: `POST(/url)` and a `GET(/:id)`. The `POST` endpoint accepts JSON input in the form of a [`PostUrlRequest`](https://github.com/cacoco/smally-finatra/blob/master/src/main/scala/io/angstrom/smally/domain/http/PostUrlRequest.scala) case class:

```json
{
  "url" : "https://www.google.com"
}
```
This endpoint captures the URL posted to the service, storing it in Redis keyed by an atomically increasing Long value. This long value is then converted into a 32-radix String and returned as the path of the shortened URL. The response is an `HTTP/1.1 201 Created` with a  [`PostUrlResponse`](https://github.com/cacoco/smally-finatra/blob/master/src/main/scala/io/angstrom/smally/domain/http/PostUrlResponse.scala) body:

```json
{
  "smally_url" : "https://127.0.0.1:8080/9h5k4"
}
```

The `GET` endpoint deferences the id given in the path, looking up the corresponding expanded URL that maps to the Long value represented by the given id. If a mapped URL is found an `HTTP 301 Moved Permanently` is returned with the expanded URL set in the `Location` header. Otherwise an `HTTP/1.1 404 Not Found` is returned for an id that cannot be properly expanded. You can see the various test cases [here](https://github.com/cacoco/smally-finatra/blob/master/src/test/scala/io/angstrom/smally/SmallyServerFeatureTest.scala).

<p/><p/>
#### Deploying to [Heroku](https://heroku.com).

You'll need to have the [Heroku Toolbelt](https://toolbelt.heroku.com/) [installed](https://devcenter.heroku.com/articles/getting-started-with-scala#set-up).

Clone the [`smally-finatra`](https://github.com/cacoco/smally-finatra) service locally, and change into the directory, e.g.,

```bash
$ git clone https://github.com/cacoco/smally-finatra.git
$ cd smally-finatra
```

Create a new app in Heroku:

```bash
$ heroku create
Creating nameless-lake-8055 in organization heroku... done, stack is cedar-14
https://nameless-lake-8055.herokuapp.com/ | https://git.heroku.com/nameless-lake-8055.git
Git remote heroku added
```

Create a Redis add-on:

```bash
$ heroku addons:create heroku-redis:hobby-dev
```

You can then deploy application to Heroku:

```bash
$ git push heroku master
Counting objects: 480, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (376/376), done.
Writing objects: 100% (480/480), 27.68 MiB | 16.24 MiB/s, done.
Total 480 (delta 101), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
...
```

Tail the Heroku logs:

```bash
$ heroku logs -t
```

Then curl the service to create a shortened URL. Once created, paste the returned URL in a browser to be redirected to the expanded URL. To create with curl:

```bash
$ curl -i -H "Content-Type: application/json" \
  -X POST -d '{"url":"https://www.nytimes.com/2012/05/06/travel/36-hours-in-barcelona-spain.html"}' \
  https://nameless-lake-8055.herokuapp.com/url
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Content-Length: 44

{"smally_url":"https://nameless-lake-8055.herokuapp.com/9h5k4"}
```


Full project source available [on github](https://github.com/cacoco/smally-finatra).
