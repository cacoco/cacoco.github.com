---
layout: post
title: "Apache Buildr and Annotation Processing for AWS Simple Workflow"
date: 2012-08-01 20:44
comments: false
categories: 
published: true
---

I recently wrote [an article](http://mechanics.flite.com/blog/2012/07/26/using-apache-buildr-for-annotation-processing-for-amazon-simple-workflow/) about how to use [Apache Buildr](http://buildr.apache.org) to process Amazon's custom annotations via [APT](http://docs.oracle.com/javase/6/docs/technotes/guides/apt/) specifically for working with the [AWS Simple Workflow Service](http://docs.aws.amazon.com/amazonswf/2012-01-25/developerguide/swf-welcome.html) -- check it out. 

<!-- more -->

####TL;DR 

You can use the following gist to generate Java sources using [APT](http://docs.oracle.com/javase/6/docs/technotes/guides/apt/) in Apache Buildr:

<div class="row-fluid">
	<div class="span12">
		<script src="https://gist.github.com/cacoco/3137530.js"></script>
	</div>
</div>
