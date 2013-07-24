# Hydra Based IR: Baseline Functionality

The [three V's of big data](http://en.wikipedia.org/wiki/Big_data#Definition) are:

- Volume: the amount of data
- Velocity: the speed of data in and out
- Variety: the range of data types and sources

The institutional repository of a research university has low velocity, medium to high volume, and high variety.
Accommodating high data variety is critical to the success of an institutional repository.
As such accommodating data variety should be a central tenant of institutional repository design.

We want to help faculty, staff, and students when they ask us: how can I deposit my article?
my dataset?
my presentation?
my poster?
my final project?
my video?
my audio files?
my master's thesis?
my simulation?
Our patrons have not been asking for a lot, just a place to preserve and share a wide variety of content.
Once we have a foundation where we can accept, describe, preserve, and present a wide variety of content we can start adding more sophisticated capabilities to the repository ecosystem.

We would like to accommodate library collection development in addition to serving the needs of the broader campus community. 
While management workflows for licensed and purchased content will have to wait until the self-deposits foundation is laid, library employees can also utilize the system to host collections of digital materials.

## Towards and Extensible Architecture
We want this IR solution to be easy to theme, customize, and extend.
That said Curate, much like [Blacklight](http://projectblacklight.org), is meant to be a developer-friendly framework -- not a turn-key solution.

The core of the IR functionality is contained in the "[curate](https://github.com/ndlib/curate)" gem.
[CurateND](https://github.com/ndlib/curate_nd) is a reference implementation of a full IR solution. 

### Components
Building an extensible system is complicated.
The encapsulation of and interfaces between functions and systems are critically important.
Initially we believe that we will need to address the following:

- [User management](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#user-management)
- [Content types](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#content-types)
  - [Content type registry](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#content-type-registry)
- [Activity monitoring & messaging](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#activity-monitoring--messaging)
- [Authority management](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#authority-management)
- [Mediation channels](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#mediation-channels)
- [Dissemination systems](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Components.md#dissemination-systems)

## Features
- Support basic deposit, description, view, search, and access of the major types of formats and works (we call them Curation Concerns).
	- Works include theses, dissertations, articles, tabular datasets, posters, presentations, final projects, other (**we can still provide preservation level support even if we cannot provide appropriate viewers yet**)
- Basic services for deposit, view, and search of images, videos, documents, audio files
- Support format-specific workflows including ingestion, generation of access derivatives, access policies, and retention policies.
- Provide basic user profiles
	- Allow user profiles to be linked to existing "sibling profiles" such as ORCID
- Create a collection that contains a set of multiple types of works.
- Collect metadata for all collections, profiles, works, and format types that are comprehensively indexed for searching.
- Full-text indexing support for certain types of content
- Enable searching of approved CurateND content within OneSearch (Notre Dame's Primo instance)
- Presentation pages for profiles, collections, works, and individual items.
- Generate citations and DOI’s on an as-needed basis for works
- Generate sharable links for collection, profile, work level, and format level views.
- Support uploading content directly.
- Support linking to content hosted elsewhere on the open web.
- Be able to set levels of access on a per-item level to: private, campus only, embargoed, and public.
- Access levels can vary within the hierarchy of a collection (e.g. a public collection may contain campus-only items. Those items would only be visible to people on campus but the rest would always be visible. )
- Basic preservation standards, common metadata fields, and file format requirements enforced.
