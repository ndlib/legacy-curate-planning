# Planning

These repo contain high-level functional and technical requirements related to the development of public-facing projects.
This allows the development roadmap to be visible to all those with interest.

## What gets put here?
As the project life cycle progresses the documents in this repository may not continue to be the source or record for ongoing development.
The process will work something like this:

1. Articulate the purpose and technical goals of project as a whole.
2. Identify the components needed to fulfill the project needs.
3. Create epic-level feature descriptions for each component.
4. Create story-level feature development for each epic.
5. Write one or more tests for each story.
6. Write code to make the tests work.

1--2 will be present in this repo.  
3--4 will be documented as issues in the component repos.  
5--6 will be contained in the components repos themselves as they are the actual deliverables of this process.

## Conventions
The documents themselves should be written in [github-flavored markdown][1].
That way they will be rendered as web pages by github itself.
This also allow in-browser edits to be made by those who aren't comfortable the full git toolchain.

### Prose
The text in this repo follows the "one sentence per line rule".
This is helpful for two reasons:

1. In prose the sentence is the atomic unit of meaning.
   Moving sentences around is a great way to refactor text.
   Having one sentence per line makes manipulating sentences easier.
2. Soft wrap serves as a gentle reminder that your sentence is getting too long.

### Diagrams
Diagrams should be included as SVG files.
[Inkscape][2] is a reasonable FOSS drawing program for creating SVG files.
You can also export to SVG using Adobe Illustrator.
Visio doesn't export to SVG very well.
There are lots of other options.

[1]: http://github.github.com/github-flavored-markdown/
[2]: http://inkscape.org
