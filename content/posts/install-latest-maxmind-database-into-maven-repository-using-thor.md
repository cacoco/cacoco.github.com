---
title: "Install Latest Maxmind Database Into Maven Repository Using Thor"
date: "2013-05-04"
draft: false
tags: ["maven", "thor", "maxmind"]
header: true
---

In a previous life, my company used the [MaxMind](https://www.maxmind.com/en/home) GeoIP database for geo-location information based on client IP addresses. We packaged the .dat as a JAR included on the classpath for use in instantiating a [com.maxmind.geoip.LookupService](https://github.com/maxmind/geoip-api-java/blob/master/source/com/maxmind/geoip/LookupService.java) object which we wrapped with a custom service.

Generally, we updated the database once a quarter so I wrote a [Thor](https://github.com/wycats/thor) script to download the .dat file, put it into a JAR, and upload the JAR as a Maven artifact to a Maven-compatible repository (we used [Nexus](https://www.sonatype.org/nexus/)). The default download location is ```~/Downloads``` but it's configurable via the passed in 'temp' argument: ```--temp=/tmp```.

#### Thor File

```gist {cols="10", id="5518012"}
 https://gist.github.com/cacoco/5518012
```

We used an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) timestamp as the version, i.e., _2011-02-25_.

#### Including as a Maven dependency

```gist {cols="8", id="5518076"}
 https://gist.github.com/cacoco/5518076
```

By including as a Maven dependency the JAR will be on the classpath and access to the .dat file can happen as a classpath resource.

#### Loading the File

Most of our applications were written in Java using [Spring](https://www.springsource.org/documentation) for dependency injection. We wrapped the ```com.maxmind.geoip.LookupService``` in a thin layer of our own code to provide our applications with a simple interface. To do this we made our service inherit from Spring's ApplicationContextAware Interface and override the ```setApplicationContext(..)``` method like such:

```gist {cols="10", id="5518218"}
 https://gist.github.com/cacoco/5518218
```
