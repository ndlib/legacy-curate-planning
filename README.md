# DEPRECATED
This planning process is no longer in active use.

# Planning

These repo contains high-level functional and technical requirements related to the development of public-facing projects.
This allows the development roadmap to be visible to all those with interest.

## The Process
As the project life cycle progresses the documents in this repository may not continue to be the source or record for ongoing development.
The process will work something like this:

1. Articulate the purpose and technical goals of project as a whole.
2. Identify the components needed to fulfill the project requirements.
3. Create epic-level feature descriptions for each component.
4. Create story-level feature development for each epic.
5. Write one or more tests for each story.
6. Write code to make the tests work.

1--2 will be present in this repo.  
3--4 will be documented as milestones and issues in this repo _or_ in individual component github repos depending on the project (planning tasks for [Curate][2] are logged in this repo).  
5--6 will be contained in the components repos themselves as they are the actual deliverables of this process.

## Conventions
The documents themselves should be written in [github-flavored markdown][1].
That way they will be rendered as web pages by github itself.
This also allow in-browser edits to be made by those who aren't comfortable the full git toolchain.

There are also planning materials in [the wiki][3] for this project.
Speculative documents are usually started there.

### Prose
The text in this repo follows the "one sentence per line rule".
This is helpful for two reasons:

1. In prose the sentence is the atomic unit of meaning.
   Moving sentences around is a great way to refactor text.
   Having one sentence per line makes manipulating sentences easier.
2. Soft wrap serves as a gentle reminder that your sentence is getting too long.

### Diagrams
When possible Diagrams should be included as SVG files.
[Inkscape][4] is a reasonable FOSS drawing program for creating SVG files.
You can also export to SVG using Adobe Illustrator.
Visio doesn't export to SVG very well.
There are lots of other options.

Raster images should be included as either PNG or JPEG as appropriate.

[1]: http://github.github.com/github-flavored-markdown/
[2]: https://github.com/ndlib/curate
[3]: https://github.com/ndlib/planning/wiki
[4]: http://inkscape.org
