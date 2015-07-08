![Angstrom](favicon.ico)

## cacoco.github.com

Website + Blog using [Octopress](http://octopress.org/) and [Twitter Bootstrap](http://twitter.github.com/bootstrap).

Build
-----------------------------------------------------------
* Pull the latest updates from `gh-pages-source` branch.
* Run `bundle install`.
* Run `rake setup_github_pages`.

Edit
-----------------------------------------------------------
* Make your changes and commit them to the `gh-pages-source` branch.
* We're using [Octopress](http://octopress.org) see the [documentation](http://octopress.org/docs/blogging/) for how to blog with Octopress.

Preview
-----------------------------------------------------------
* Run `rake generate` to compile the documentation.
* Run `rake preview` and point your browser at `localhost:4000` to preview.

Deploy
-----------------------------------------------------------
* Deploy your changes by running: `rake deploy` (make sure to always run `rake generate` **before deploying your changes**).
* Changes should be visible at [https://cacoco.github.io](https://cacoco.github.io) and [http://angstrom.io](http://angstrom.io).

<br/ >
<br/ >
<br/ >
<br/ >
<br/ >

## Documentation  

[Blogging basics](http://octopress.org/docs/blogging/) from Octopress.
