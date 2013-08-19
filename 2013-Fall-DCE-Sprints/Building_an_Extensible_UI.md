# Building an Extensible UI
Front-end development is hard.
You can take some of the edge off by:

- Leveraging templating systems
- Adopting shared pattern libraries
- Writing modular CSS
- Extending CSS with a pre-processor
- Leveraging the Rails Asset Pipeline

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
In SASS variables have the `!default` option which allows them to be overridden from _outside_ their context.
This is great because it is a simpler way to override just the properties you need to.

The [official twitter bootstrap](https://github.com/twbs/bootstrap) project uses LESS but there are still options.

### Which SASS Implementation?
Since LESS can be converted to SASS without too much pageantry there are several SASS ports of twitter bootstrap.
Of the actively-maintained projects Thomas McDonald's [bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass) appears to be the most popular.
It is also nicely structured to take advantage of the Rails Asset Pipeline.
As twitter bootstrap v3 has not been finalized we will be tracking the [bootstrap 3 branch](https://github.com/thomas-mcdonald/bootstrap-sass/tree/3) of this gem.

## Using the Asset Pipeline
The Rails [Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html) is really helpful.
There are three things that it excels at:

- Enabling pre-processors like LESS, SASS, and CoffeeScript
- Consolidating and compressing CSS and JavaScript files
- Managing the [load path](https://github.com/sstephenson/sprockets#the-load-path) for assets

Of these managing the load path is perhaps the most powerful.
