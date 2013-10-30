# Building an Extensible UI
Front-end development is hard.
You can take some of the edge off by:

- Leveraging templating systems
- Adopting shared pattern libraries
- Writing modular CSS
- Extending CSS with a pre-processor
- Leveraging the Rails Asset Pipeline
- Sticking to Progressive Enhancement
- Componentize your JavaScript

## Templating Systems
Rails has a [templating system](http://guides.rubyonrails.org/layouts_and_rendering.html).
Put the tools it gives you to good use:

  - [Nest layouts](http://guides.rubyonrails.org/layouts_and_rendering.html#using-nested-layouts) e.g. [define a header and multi-column page layout](https://github.com/ndlib/curate/blob/master/app/views/layouts/curate_nd.html.erb) and render it inside the [page boilerplate](https://github.com/ndlib/curate/blob/master/app/views/layouts/boilerplate.html.erb).
  - [Yield blocks between views and layouts](http://guides.rubyonrails.org/layouts_and_rendering.html#understanding-yield).
  You can use `:yield` and `:content_for` to let content in a partial bubble up into its containing layout.

## Shared Pattern Libraries
There are [lots](http://foundation.zurb.com) [of](http://www.blueprintcss.org) [different](http://firezenk.github.io/zimit) CSS pattern libraries out there.
The 800 pound gorilla is [twitter bootstrap](http://getbootstrap.com).
Bootstrap 3 addresses may of the limitations of bootstrap 2.
We will be using Bootstrap 3 as the underlying framework for Curate.

The [official twitter bootstrap](https://github.com/twbs/bootstrap) project uses LESS.

### Integrating With Twitter Bootstrap
Twitter Bootstrap is an actively developed project.
This is especially true right now as version 3 is being finalized.
We have three options for assimilating these files:

- Freeze a copy of the precompiled CSS and JavaScript in the Curate gem
- Use the [bower](http://bower.io) package of twitter bootstrap in our application
- Use a third-party gem to manage the bootstrap assets

#### Static Assets
Freezing the static assets into our gem is a bad idea.
It is not extensible and will force design assumptions onto the gem adopters.

#### Bower Integration
[Bower](http://bower.io) is a package manager for front-end code.
There are some [simple](https://gist.github.com/benschwarz/5874031) [ways](http://stackoverflow.com/questions/16772167/bower-and-rails-asset-pipeline-import) to feed bower packages into the asset pipeline.
There are also utilities to [help manage your bower packages in a Rails project](https://github.com/42dev/bower-rails/) or even [replace the asset pipeline entirely with a bower-centric toolchain](https://github.com/d-i/half-pipe).

Twitter bootstrap is officially distributed as a [bower package](http://sindresorhus.com/bower-components/) so there would be some advantages to sticking with the canonical version.
Integrating with bower at the application level seems tenable but it is not clear how one would do this inside a [rails engine](http://edgeguides.rubyonrails.org/engines.html).

#### Use a gem
Since LESS can be converted to SASS without too much pageantry there are several SASS ports of twitter bootstrap.
Of the actively-maintained projects Thomas McDonald's [bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass) appears to be the most popular.
It is also nicely structured to take advantage of the Rails Asset Pipeline.
As twitter bootstrap v3 has not been finalized we would have to track the [bootstrap 3 branch](https://github.com/thomas-mcdonald/bootstrap-sass/tree/3) of this gem.

## Write Modular CSS
There are [several](http://smacss.com) [approaches](https://github.com/stubbornella/oocss/wiki) to making CSS code more manageable.
The idea is that if you alter the way you code CSS it can be reused more effectively, even if the reuse is in a different context.
For this project we will be adopting many of the guidelines outlined by [SMACSS](http://smacss.com).
Some rules of note are:

- [Categorize CSS Rules](http://smacss.com/book/categorizing)
- [Minimize Depth of Applicability](http://smacss.com/book/applicability)
- [CSS Formatting](http://smacss.com/book/formatting)

## CSS Pre-Processors
CSS is great.
CSS is also very limited.
Basic tools like variables and reusable patterns are absent to all but the [most recent versions of CSS](http://dev.w3.org/csswg/css-variables/).
Because we have to accommodate the lowest common denominator across browsers we can't build our stylesheets on new capabilities in CSS.
[LESS](http://lesscss.org) and [SASS](http://sass-lang.com) both try to address this problem.
They provide something _like_ CSS that gives us variables, modularity, and inheritance but compiles to plain CSS.

### LESS vs. SASS _fight!_
[LESS](http://lesscss.org) and [SASS](http://sass-lang.com) have similar design goals --- they even look pretty similar.
For our purposed SASS is a better fit because of the way variables work.
In LESS variables are scoped by context; to extend a LESS project you have to override the file where the variables are declared.
In SASS variables have the `!default` option which allows them to be set from _outside_ their context.
This is great because it is a simpler way to override just the properties you need to.

## Using the Asset Pipeline
The Rails [Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html) is really helpful.
There are three things that it excels at:

- Enabling pre-processors like LESS, SASS, and CoffeeScript
- Consolidating and compressing CSS and JavaScript files
- Managing the [load path](https://github.com/sstephenson/sprockets#the-load-path) for assets

Of these managing the load path is perhaps the most powerful.

## Progressive Enhancement
[Progressive Enhancement](http://en.wikipedia.org/wiki/Progressive_enhancement) is a design philosophy that has been around for a while.
The idea is simple: make your website work for the lowest common denominator and add features, decoration, and behavior on top of the baseline for those who can take advantage of it.
In 2006 this meant that you had to make sure it worked in IE6 with a 1024x768 screen.
This is no longer the case.
Modern web development has coalesced on the idea of [mobile-first responsive design](http://bradfrostweb.com/blog/web/mobile-first-responsive-web-design/).

There is a lot to discuss here but the immediate takeaways are:

- Your website should still work if JavaScript is turned off.
- At the very least all _public_ pages should treat mobile devices  as a first-class citizen.
- Use tools like [modernizer](http://modernizr.com) to enable features for more advanced browsers.
- It is perfectly fine for a page to look different from browser to browser.
  It is _not_ ok for it to break.

## Componentize your JavaScript
Each widget, tool, or behavior that can't be trivially implemented in jQuery should be encapsulated on its own right.
The [jQuery widget factory](http://api.jqueryui.com/jQuery.widget/) is a great way to do this.
The widget factory provides connivence methods for managing its instantiation, event watching, and scopes `this` appropriately.
On top of this if you keep the jQuery widgets in separate files they can be overridden entirely in the parent application using the asset pipeline.