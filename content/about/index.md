---
title: About
permalink: /about/
date: 2013-03-12 21:02
draft: false
footer: true
---

I am a [Principal](https://www.linkedin.com/pulse/what-principal-engineer-anyway-douglas-w-arcuri/)-level Software Engineer located in San Francisco, CA. I have many years of experience specializing in Distributed Systems, Platform Infrastructure, API Design & Frameworks, and Open Source Software. I pride myself on serving as a mentor and I get a great sense of accomplishment from helping others realize they belong.

I was inspired by a former colleague to put together a public version of a [brag document](https://jvns.ca/blog/brag-documents/). Below are some highlights from my most recent time in my career at Twitter.

### Twitter [2012-2022]

#### Company Building

Throughout my time at Twitter and in my various roles, I have actively participated in many company and culture-building efforts, including:

* [@Blackbirds](https://twitter.com/blackbirds) Employee Resource Group Lead [2015-2016]
* [Black Executive Leadership Program](https://www.credly.com/badges/822c231c-6e31-4c80-b361-79272d48c352?source=linked_in_profile) [2021]
* Volunteer and volunteer coordinator - [Tenderloin Technology Lab](https://www.stanthonysf.org/services/tech-lab/) at St. Anthony's [2012 - 2016]
* Twitter Engineering Mentor program mentor
* Twitter "Wingmates" (New Hire) mentor
* Multiple time [Code2040](https://www.code2040.org/) Mentor [2016, 2018]
* Twitter Open Source Shepherd
* Serial summer and fall intern mentor [2014, 2015, 2016, 2018, 2019, 2021]
* Founding member of Engineering Interview Process standardization (The "Luna" Process) and founding interview shepherd (+1 reviewer model)
* _Introduction to the [Topgrading](https://en.wikipedia.org/wiki/Topgrading) Engineering Interview at Twitter_ course instructor
* Many time attendee to the [Tapia](http://tapiaconference.org/), [NSBE](https://nsbe.org/home.aspx), and [Grace Hopper](https://ghc.anitab.org/) conferences for recruiting and candidate interviewing on behalf of multiple teams [^1] [^2] [^3] [^4] [^5] [^6] [^7]
* Twitter [Earlybird Camp interviewer, mentor & judge](https://twitterearlybirdcamp.splashthat.com/), Twitter [#FirstFlight interviewer and panelist](https://nov2017firstflight.splashthat.com/), & Twitter Academy cultural mentor
* Introduction to [Finatra](https://github/twitter/finatra) course instructor
* Open source at Twitter course material reviewer and instructor
* Mentor for multiple University of San Francisco Computer Science [Capstone Projects](https://www.usfca.edu/arts-sciences/programs/undergraduate/computer-science/capstone-project) [2018]
* Technical Design Shepherd for many infrastructure and product projects
* Member of the Technical Architecture Group (TAG)
* Member of the Senior-IC Platform Group (Platforum)
	- Co-chair and author of membership and working group guidelines
* Member of the Twitter Migrations Working Group (MWG)
	- Helped plan, execute and track technology migrations across engineering
* Constant cross-team work to improve the developer experience and the ability to deliver with better velocity

#### Technical Lead - Compute Integrations Team [2022]

The Compute organization provided a scalable, efficient, and cost-effective computing platform for all of Twitter. The main goal was to provide hardware leverage by abstracting the maintenance and administration of commodity hardware machines such that application engineers do not need to deal with host administration or remediation when hosts fail. This was for years provided by multiple [Aurora+Mesos](https://aurora.apache.org/) clusters and later augmented by [Kubernetes](https://kubernetes.io/) clusters both on-premise and in [GCP](https://cloud.google.com/). 

The Compute Integrations Team was responsible for integrating Kubernetes with various Twitter-specific technologies like Service Discovery, application configuration federation, application observability, and chargeback. The team was also fully responsible for the Compute-org-managed Kubernetes clusters in GCP.

* Work to optimize service discovery in Kubernetes clusters by moving the service discovery infrastructure in Kubernetes to be _regional_ (in this case per data center) rather than per cluster (since there are multiple Kubernetes clusters in a "region").
* Work to design an automated way of on-premise Kubernetes cluster discovery and registration for better integration into existing Twitter infrastructure and more visibility and introspection into the running clusters.
* High-priority work to secure the global package store infrastructure ("Packer"):
	 - Java-based Finatra service with a python client (distributed on developer laptops, via the package store, itself, for other infrastructure components, e.g. CI/CD components for package retrieval, and via a Linux RPM for data center host management infrastructure services).
	 - Work involved updating the server to support both internal mutual-TLS (mTLS) and TLS (in addition to Kerberos) and updating the Python client to ensure it negotiated connections from the various locations of deployment correctly (either mTLS where a client certificate could be presented or via TLS where Kerberos was also in use).
	 - Massive undertaking to update all instances of the distributed Python client which involved multiple Puppet runs to release new versions to the data center machines (with minimal documentation and a dwindling number of experts around to ensure that catastrophe was avoided).

#### Technical Lead - Twitter Open Source Program Office [2021-2022]

* Developed internal GitHub API HTTP client in Scala.
* Developed Open Source project cataloging service pulling data from GitHub on Twitter Open Source projects and uploading to a set of BigQuery tables to allow Product Managers access for developing insights into Twitter's open source landscape.
* Summer intern mentor and mentor to junior team members.
* Unowned 3rd Party dependency Working Group Lead:
	- helped to come up with the definition and tiers of ownership for 3rd party libraries in the central code monorepo
	- worked to catalog and find owners for all unowned JVM 3rd party libraries in the central code monorepo.
* Work to serve Open Source GitHub pages at [opensource.twitter.dev/](https://opensource.twitter.dev/) domain.
* Creator of the [Open Source Project status](https://opensource.twitter.dev/status/#active) model and associated labels.
* Led the discussion and work to decide on a [standard metadata description](https://github.com/twitter/opensource-website/blob/main/codemeta.yaml) for Open Source projects extensible to internal projects to help with the "system comprehension" work to register and catalog internal services.
* Proposed, led, and assisted various technology migration efforts across engineering as part of the Twitter Migrations Working Group (MWG) including the move [from Pants to Bazel](https://opensourcelive.withgoogle.com/events/bazelcon2020/watch?talk=day1-talk2) [^15]
* Maintained and improved the internal "GitHub Manager" service -- originally an intern project written in Python. Added mTLS support and distributed logging as well as Okta integration for login.
* Served as company GitHub administrator, supporting engineers open sourcing new projects and GitHub repository membership maintenance and administration.
* Wrote the primer on "How to open source code at Twitter" and technical documentation on using GitHub actions and performing open source releases via the OSSRH. 

#### Twitter Architecture Group [2020-2022]

* Project to have teams document and share product, infrastructure, and service architecture. Identifying upstream and downstream dependencies. Worked to integrate this work with Zipkin (microservice tracing) data to start to build comprehensive and digestible diagrams of the many-interconnected systems. Work superseded by the "System Comprehension" initiative (work to ensure ongoing FTC compliance via registration and system tracking).
* Company-wide Technology Radar reviewer and recommendation author
* Language Support at Twitter, e.g., "what is the Future of Scala at Twitter?"

#### Senior Member - Core Systems Libraries (CSL) Team [2016-2021]

The Core Systems Libraries team was responsible for developing, supporting, and maintaining the foundational Twitter-stack libraries for distributed systems. Thousands of internal Twitter microservices and numerous Open Source consumers consumed and extended these libraries. 

* The Open Source Twitter-stack projects owned by the CSL team include:
	- [Util](https://github.com/twitter/util)
	- [Scrooge](https://github.com/twitter/scrooge)
	- [Finagle](https://github.com/twitter/finagle)
	- [TwitterServer](https://github.com/twitter/twitter-server)
	- [Finatra](https://github.com/twitter/finatra)
	- [Dodo](https://github.com/twitter/dodo)
* Creator and maintainer of internal microservice scaffolding library ("Beaker") for easily creating new Finatra-based microservices and applications.
* Creator and maintainer of the [Finatra framework](https://github.com/twitter/finatra/graphs/contributors) & primary [Documentation](https://twitter.github.io/finatra/) author
* Provided internal and [external](https://gitter.im/twitter/finatra) Finatra support to users
* Creator and maintainer of the [Dodo](https://github.com/twitter/dodo/graphs/contributors) project builder
* Creator and maintainer of several [Twitter Util](https://github.com/twitter/util) projects:
	- [util-slf4j-api](https://github.com/twitter/util/tree/develop/util-slf4j-api)
	- [util-slf4j-jul-bridge](https://github.com/twitter/util/tree/develop/util-slf4j-jul-bridge)
	- [util-validator](https://github.com/twitter/util/tree/develop/util-validator) & primary [Documentation](https://twitter.github.io/util/guide/util-validator/index.html) author
	- [util-jackson](https://github.com/twitter/util/tree/develop/util-jackson) & primary [Documentation](https://twitter.github.io/util/guide/util-jackson/index.html) author
	- [util-reflect](https://github.com/twitter/util/tree/develop/util-reflect)
	- [util-mock](https://github.com/twitter/util/tree/develop/util-mock)
* A primary maintainer of the Twitter [Util App](https://github.com/twitter/util/tree/develop/util-app) framework library
* A primary maintainer of the [TwitterServer](https://github.com/twitter/twitter-server/commits?author=cacoco) server framework
* A maintainer of the [Scrooge](https://github.com/twitter/scrooge/commits?author=cacoco) thrift generator library
* A maintainer of the [Finagle](https://github.com/twitter/finagle/commits?author=cacoco) protocol-agnostic RPC library
* Helped various technology migration efforts including the move from the deprecated [`c.t.c.application.AbstractApplication`](https://maven.twttr.com/com/twitter/common/application/) to Finatra

#### Technical Lead - Data API Team [2013-2016]

* Architect and Senior Engineer - [Nielsen Twitter TV Rating (NTTR) System](https://blog.twitter.com/official/en_us/a/2012/coming-soon-nielsen-twitter-tv-rating.html) ("Project Kingfisher") [^8] [^9] [^10]
	- Led requirements gathering with Nielsen company, SocialGuide [^11] -- functioning as PM, and TL through the first 3 phases of the project. The team eventually expanded to 4 full-time engineers, a PM, TPM, and a partner engineer.
		+ Phase 1 was a [skunkworks](https://en.wikipedia.org/wiki/Skunkworks_project) project between a Twitter TPM and Nielsen which involved the TPM manually culling data with Pig scripts and emailing CSVs to Nielsen counterparts.
		+ Phase 2 introduced a two-person engineering team (myself and one other senior engineer) to implement a set of APIs backed by an extensible system that would first serve only Nielsen in the US market but expand to other partners in other markets across the globe.
		+ Phase 3 expanded to other partners in different global markets: [VideoResearch](https://www.videor.co.jp/eng/company/index.html) and [Kantar](https://www.kantar.com/en-cn) serving: Japan, Italy, Spain, Great Britain, Australia, and France in addition to Nielsen in the US [^12] [^13].
	- The design is a self-repairing task system that ingested Tweet IDs about particular TV shows in a market from partners. These came in hourly buckets for reporting which the system would use to then crank over Twitter's engagement data on each Tweet to return anonymized hourly bucketed information on authors and user engagements. 
	- The results were uploaded to the internal Twitter equivalent of [AWS S3](https://aws.amazon.com/pm/serv-s3/) buckets ("Blobstore") which had a public API accessible via OAuth for partners to retrieve the information and feed into their rating models. 
	- The system maintained a "sandbox" set of endpoints which were the first to be rolled with updates such that partners could validate against incoming changes without affecting production workloads.
	- The project included creating one of the first Scala clients for the internal Blobstore
	- Additionally included creating one of the first Scala clients to the internal "NoSQL" K/V store: [Manhattan](https://www.wired.com/2014/04/twitter-manhattan/)
* Architect and Senior Engineer - [Twitter 2014 Midterm Election](https://blog.twitter.com/en_us/a/2014/introducing-the-twitter-us-2014-election-website) framework powering the 2014 Midterm election dashboard
* Maintainer of the primary client event ingestion system ("Rufous") which powered all company metrics and ML models
	- Created testing harness with fake service endpoints ("Rufaux") with configurable data sink for use with external client event validation system ("Echidna"). Worked across teams on design and integration. 
* Performed due diligence on [GNIP acquisition](https://blog.twitter.com/en_us/a/2014/twitter-welcomes-gnip-to-the-flock) [^14]
* Created and open-sourced the [v2 of the Finatra framework](https://blog.twitter.com/engineering/en_us/a/2015/finatra-20-the-fast-testable-scala-services-framework-that-powers-twitter)

#### Senior Member - The API Team [2012-2013]

* Ported many Twitter [Ruby-on-Rails](https://rubyonrails.org/) application API endpoints to new [Scala](https://www.scala-lang.org/)-based service (while learning Scala)
* Helped create a ["tap compare"](https://medium.com/@lfgcampos/tap-compare-testing-2b8bedce1779) system for validating new Scala-based API endpoints against existing Rails endpoints
* Optimized bare-metal deployments of massive Scala application ("Woodstar") serving migrated Twitter API endpoints
* Summer intern mentor
* Active in interviewing and hiring new engineers

### More Work History
A full work history is available on my [LinkedIn profile](https://www.linkedin.com/in/cacoco/).

******

### Patents 

* Live Updates of Embeddable Units [US 20130007108 · Filed Jun 26, 2012](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/20130007108)
* SYSTEM AND METHOD FOR A DELIVERY NETWORK ARCHITECTURE SYSTEM AND METHOD FOR A DELIVERY NETWORK ARCHITECTURE [US 20090327079 · Filed Jun 25, 2008](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/20090327079)

[^1]: https://blog.twitter.com/engineering/en_us/topics/insights/2016/twitter-goes-to-nsbe42
[^2]: https://twitter.com/judyc/status/568240999409037313
[^3]: https://twitter.com/Tapia_con/status/568271071931187200
[^4]: https://twitter.com/Blackbirds/status/713034148663824384
[^5]: https://twitter.com/Blackbirds/status/713107693360119808
[^6]: https://twitter.com/Blackbirds/status/713516437692764160
[^7]: https://twitter.com/gpena/status/713525245680832516
[^8]: https://martech.org/nielsen-launches-twitter-tv-ratings-potentially-a-key-social-metric-for-advertisers/
[^9]: https://www.theverge.com/web/2013/10/7/4811410/nielsen-tv-twitter-rating-starts-today
[^10]: https://www.nielsen.com/insights/2013/new-study-confirms-correlation-between-twitter-and-tv-ratings/
[^11]: https://www.forbes.com/sites/michaelhumphrey/2012/11/12/nielsen-acquires-social-tv-metrics-company-socialguide/
[^12]: https://www.digitaltveurope.com/2014/10/02/kantar-media-readies-twitter-tv-ratings-tools/
[^13]: https://thenextweb.com/news/twitter-tv-ratings-heading-to-japan-next-year-in-move-to-attract-more-advertisers
[^14]: https://techcrunch.com/2014/04/15/twitter-acquires-longtime-partner-and-social-data-analytics-provider-gnip
[^15]: https://eed3si9n.com/2years-at-twitter/