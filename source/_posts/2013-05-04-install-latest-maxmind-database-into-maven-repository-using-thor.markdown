---
layout: post
title: "MaxMind, Maven, and Thor"
date: 2013-05-04 09:36
comments: false
categories: 
published: true
---

<!-- more -->

In a previous life, my company used the [MaxMind](http://www.maxmind.com/en/home) GeoIP database for geo-location information based on client IP addresses. We packaged the .dat file into a JAR which we included on the classpath for use in instantiating a [com.maxmind.geoip.LookupService](https://github.com/maxmind/geoip-api-java/blob/master/source/com/maxmind/geoip/LookupService.java) object. 

We generally updated the database once a quarter, so I wrote a [Thor](https://github.com/wycats/thor) script to download the .dat file, put it into a JAR, and then upload the JAR as a Maven artifact to a Maven-compatible repository (Nexus or Artifactory). The default download location is ```~/Downloads``` but it's configurable via the passed in 'temp' argument: ```--temp=/tmp```.

####Thor File

<div class="row-fluid">
  <div class="span10">
    <script src="https://gist.github.com/cacoco/5518012.js"></script>
  </div>
</div>

We used an [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) timestamp as the version, i.e., _2011-02-25_  

####Including as a Maven dependency

<div class="row-fluid">
  <div class="span8">
	<script src="https://gist.github.com/cacoco/5518076.js"></script>
  </div>
</div>  

where we define: ```<geocity.version>2011-02-25</geocity.version>``` in the ```<properties/>``` section of the pom.xml.

####Loading the File

Most of our applications were written in Java and we used Spring for dependency injection. We wrapped the ```com.maxmind.geoip.LookupService``` in a thin layer of our own code to provide our applications with a stable interface. To do this we made our service inherit from Spring's ApplicationContextAware Interface and override the ```setApplicationContext(..)``` method like such:

<div class="row-fluid">
  <div class="span10">
    <script src="https://gist.github.com/cacoco/5518218.js"></script>
  </div>
</div> 


