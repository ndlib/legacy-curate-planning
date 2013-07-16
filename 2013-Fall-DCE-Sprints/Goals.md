# Hydra Based IR: Baseline Functionality

The [three V's of big data](http://en.wikipedia.org/wiki/Big_data#Definition) are:

- Volume: the amount of data
- Velocity: the speed of data in and out
- Variety: the range of data types and sources

An institutional repository for a research university has low velocity, medium to high volume, and high variety.
Accommodating high data variety is critical to the success of an institutional repository.
To make matters worse the range of data types and sources also varies from university to university.
As such accommodating data variety should be a central tenant of institutional repository design.

Every time we hear the question how can I deposit my article?
my dataset?
my presentation?
my poster?
my final project?
my video?
my audio files?
my master's thesis?
my simulation?
We need to have a clear answer.

They have not been asking for a lot, just a place to preserve and share a wide variety of content.
So, rather than take a depth approach and focus our first release on ETD's or datasets our plan is to take a breadth approach and provide basic coverage of as many of the types above as fast as we can (and do it well).

We have more complex, sophisticated features on our list, but those will come later.

In order to start helping faculty, staff, and students preserve and provide access to articles, images, datasets, documents, videos, and audio files, we will build out basic self-deposit support for a wide variety of works.

For large files this may include a non-web interface.
We also hear many of the above questions from library collection developers as well.
While management workflows for licensed and purchased content are largely deferred for a later phase, we envision library employees may also utilize the system to host collections of digital materials if supported by existing functionality.

- Support basic deposit, description, view, search, and access of the major types of formats and works (we call them Curation Concerns).
- Works include theses, dissertations, articles, tabular datasets, posters, presentations, final projects, other (we can still provide preservation level support even if we cannot provide appropriate viewers yet)

- Basic services for deposit, view, and search of images, videos, documents, audio files
- Support format-specific workflows including ingestion, generation of access derivatives, access policies, and retention policies.
- Provide basic user profiles
- Allow user profiles to be linked to existing “sibling profiles” such as ORCID
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