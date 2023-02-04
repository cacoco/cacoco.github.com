---
title: "Have TwitterServer Will Test"
date: "2016-02-01"
draft: false
tags: ["TwitterServer", "finatra", "scala", "Twitter"]
---

Did you know you can use [Finatra](https://twitter.github.io/finatra)’s [Feature Tests](https://twitter.github.io/finatra/user-guide/testing/feature_tests.html) utilities for testing any [TwitterServer](https://twitter.github.io/twitter-server/)? That is, you can start a locally running server and write tests which issue requests to it as long the server extends from `c.t.server.TwitterServer`. It doesn’t specifically have to be a Finatra server.

[Recent changes](https://github.com/twitter/finatra/commit/1878cbd00b20e71651f4b970b3dfb391d26e6d6b) to [Finatra](https://twitter.github.io/finatra) testing utilities allow for any arbitrary [TwitterServer](https://twitter.github.io/twitter-server/) to be able to create [Feature Tests](https://twitter.github.io/finatra/user-guide/testing/feature_tests.html) and a very useful type of Feature Test is a simple [Startup Test](https://twitter.github.io/finatra/user-guide/testing/startup_tests.html) where you can verify your server starts and is configured how you would expect.

Some advanced features which require use of injection will not be available but you’ll be able to start the server under test in a controlled environment.

Here’s an example of writing a test which starts a TwitterServer and asserts that it reports itself “healthy”.

Given a simple TwitterServer:

```gist {cols="8", id="fba99528917a17283d1f5f9c3d390585"}
 https://gist.github.com/cacoco/fba99528917a17283d1f5f9c3d390585
```

A Feature Test which asserts the server starts healthy would look like so:

```gist {cols="8", id="7a7f957a498b702d478b095ac6a3099d"}
 https://gist.github.com/cacoco/7a7f957a498b702d478b095ac6a3099d
``` 

Keep in mind that you have the option to explicitly start the server or let the framework start the server. In the example above, the framework will ensure the server under test has started when we call `server.isHealthy`. Otherwise, we can add a `beforeAll()` which will explicitly start the server.


```gist {cols="8", id="0768394ecf9a6e352ba1d3a5ab43a5e6"}
 https://gist.github.com/cacoco/0768394ecf9a6e352ba1d3a5ab43a5e6
```

Note, if you have [Finagle clients](https://twitter.github.io/finagle/guide/Clients.html) defined in your server and want to keep them from making remote connections when your server starts you can override the dtab of the clients by passing the `dtab.add` flag to your server under test:

```gist {cols="8", id="47ff96165061682322ab728a8ec9ed9a"}
 https://gist.github.com/cacoco/47ff96165061682322ab728a8ec9ed9a
```

To create a client to your server under test, you’ll need the bound port of the server (which is only bound after the server is started and thus you’ll want to delay the client creation until the server has started). You can easily obtain the bound port for the TwitterServer [HTTP Admin Interface](https://twitter.github.io/twitter-server/Admin.html) directly via `EmbeddedTwitterServer#httpAdminPort`.

You could then create a Finagle HTTP client to the TwitterServer admin:

```gist {cols="8", id="32db7fc43768b58de1900aa1c163ce93"}
https://gist.github.com/cacoco/32db7fc43768b58de1900aa1c163ce93
```

To get the bound external port of the server under test, you’ll need to structure your code to expose it for your test to be able to read once the server has been started. That is, the ListeningServer started in your server `main` needs to be exposed such that you can call `server.boundAddress`.

This is where using the Finatra [`HttpServer`](https://twitter.github.io/finatra/user-guide/http/server.html) or [`ThriftServer`](https://twitter.github.io/finatra/user-guide/thrift/server.html) can help as much of the client creation work can then be done for you by the framework.