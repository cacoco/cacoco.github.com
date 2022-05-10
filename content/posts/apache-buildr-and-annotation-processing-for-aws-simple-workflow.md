---
title: "Apache Buildr and Annotation Processing for Aws Simple Workflow"
date: "2012-08-01"
draft: false
tags: ["Apache", "build systems", "buildr"]
---

I recently wrote [an article](https://mechanics.flite.com/blog/2012/07/26/using-apache-buildr-for-annotation-processing-for-amazon-simple-workflow/) about how to use [Apache Buildr](https://buildr.apache.org) to process Amazon's custom annotations via [APT](https://docs.oracle.com/javase/6/docs/technotes/guides/apt/) specifically for working with the [AWS Simple Workflow Service](https://docs.aws.amazon.com/amazonswf/2012-01-25/developerguide/swf-welcome.html) -- check it out.

<!-- more -->

#### TL;DR

You can use the following gist to generate Java sources using [APT](https://docs.oracle.com/javase/6/docs/technotes/guides/apt/) in Apache Buildr:

```gist {cols="12", id="3137530"}
 https://gist.github.com/cacoco/3137530
```