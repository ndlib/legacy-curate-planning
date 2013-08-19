# Building an Extensible UI
Front-end development is hard.
You can take some of the edge off by:

- Leveraging templating systems
- Adopting shared pattern libraries
- Writing modular CSS code
- Extending CSS with a pre-processor

## Templating Systems
Rails has a [templating system](http://guides.rubyonrails.org/layouts_and_rendering.html).
Put the tools it gives you to good use:

  - [Nest layouts](http://guides.rubyonrails.org/layouts_and_rendering.html#using-nested-layouts) e.g. [define a header and multi-column page layout](https://github.com/ndlib/curate/blob/master/app/views/layouts/curate_nd.html.erb) and render it inside the [page boilerplate](https://github.com/ndlib/curate/blob/master/app/views/layouts/boilerplate.html.erb) 
  - [Yield blocks between views and layouts](http://guides.rubyonrails.org/layouts_and_rendering.html#understanding-yield).
  You can use `:yield` and `:content_for` to let content in a partial bubble up into it's containing layout.

## Shared Pattern Libraries
There are [lots](http://foundation.zurb.com) [of](http://www.blueprintcss.org) [different](http://firezenk.github.io/zimit) CSS pattern libraries out there.
The 800 pound gorilla is [twitter bootstrap](http://getbootstrap.com).
Bootstrap 3 addresses may of the limitations of bootstrap 2.
We will be using Bootstrap 3 as the underlying framework for Curate.

## Write Modular CSS Code
There are [several](http://smacss.com) [approaches](https://github.com/stubbornella/oocss/wiki) to making CSS code more manageable.
The idea is that if you alter the way you code CSS it can be reused more effectively, even if the reuse is in a different context.
