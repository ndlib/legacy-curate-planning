# Site Structure

## Home (/)
- Login
- Search
- About
- Contact
- Report a Problem

## Login (/login)
User session management will be managed with [devise](https://github.com/plataformatec/devise).

[OmniAuth](https://github.com/intridea/omniauth) provides an API for multi-provider authentication and can be [used with devise](https://github.com/plataformatec/devise/wiki/OmniAuth:-Overview).
There are many [OmniAuth strategies](https://github.com/intridea/omniauth/wiki/List-of-Strategies) including several of interest to Hydra partners:

- [CAS](https://github.com/dlindahl/omniauth-cas)
- [Shibboleth](https://github.com/toyokazu/omniauth-shibboleth)
- [Kerberos](https://github.com/naffis/omniauth-krb5)
- [LDAP](https://github.com/intridea/omniauth-ldap)

CurateND only has need for CAS integration during the first phase of development.

### Feature Evolution
- Allow the user to choose login strategy and persist strategy choice via cookie OR prompt for *login* only and determine authentication system from provided identifier
- Request an account
- Account recovery

## After Login
- Accept terms of service (if required)
- Prompt to update profile (if required)

## Profile
- Add authentication mechanisms
- Add personal identifiers e.g. ORCID, google plus
	- Validate identities via OAuth with the external services
- Authorize external storage systems e.g. [Box](https://www.box.com), [Dropbox](https://www.dropbox.com/), [Transporter](http://www.filetransporter.com/)
- Enrich Person metadata
- Manage avatar (delegate to [gravatar](http://en.gravatar.com/) for now)
- Notification settings
- Manage account delegation

## Dashboard
- Submit a Work
- Search
- About
- Contact
- Report a Problem
- Profile
- What's going on / What's happening
	- My Activity
	- My Notifications

## Activity & Notifications
### My Activity (What's happening?)
- What have I done?
	- Search actions
	- Display actions as tabular data
	- Graph actions
- What are others doing with things I observe?
	- The things I observe include but are not limited to works I have submitted
	- Implied `observers` table with pid, class, user_id/user_pid, owner_pid
	- Search usage
	- Display usage as tabular data
	- Graph usage

### My Notifications (What to do?)
- link to notification settings
- list of tasks that are waiting on me: title, state, snooze
- list of things I care about that are "in process"
	- Search list of in process items
	- Allow a user to "follow" up on an item waiting for approval
- list of things I care about that have been recently marked "done"
	- Search list of recently "done" items

## Mediation
- Notify both sending and receiving parties on state change
- Allow for changes in authorization based on item state
	- (Can a non-owner alter an item? Probably not; but they can make comments.)
- Render form for state & concern
	- ActionView lookup
- Support "locked" state (only privileged users can alter it)

## Authority Management
Controlled Vocabulary use cases:

- Metadata enrichment
- Search enhancement (synonym expansion)

Types of vocabularies:

- Locally managed term lists e.g. list of programs of study for ETD submission maintained by a Curate user.
- Fixed terminologies e.g. locally chosen list of Library of Congress subject headings
- External services e.g. [VIAF](http://www.oclc.org/viaf.en.html), [CONA](http://www.getty.edu/research/tools/vocabularies/cona/), [GeoNames](http://www.geonames.org)

Fields should ask an AuthorityBroker where to get their information.

There are two types of inputs:

- Single term e.g. select box
- Multiple term e.g. multi-select box wrapped with [chosen](https://github.com/harvesthq/chosen)

Should we support extensible vocabularies? (No)  
Can terms be used as a suggestion with a free-form input fallback? (No)  
Are new terms are added to the global list? (No)

When possible terms should be stored should be stored by _refernce_ (URI) not _value_ (string).
Object presenters then have the option of passing the terms as URI's or their string values.

## Content Identifiers
- PID (default)
- DOI (already implemented)
- ARK (optional)

### PURL Service
A "short URL" style service would be nice.

## Syndication
When an item is marked as "done" (:complete) it _may_ be syndicated to another discovery or preservation system.
Services providers include:

- Primo
- Google Scholar
- APTrust

Who chooses where it goes?
- Each curation concern has knowledge of its possible syndication channels
- The Owner of the object can opt-out of any or all syndication channels before the object is :complete.

There should be a way to edit object syndication preferences:

- on a per-item basis
- in bulk

## File Dissemination
- Document conversion e.g. to PDF
- Presentation derivatives e.g. image crops 
- Bags/BagIt export (not a priority)

## Metadata Dissemination
Crosswalk item metadata to other formats:

- DC:XML
- [Collection+JSON](http://amundsen.com/media-types/collection/), [DocJSON](https://github.com/docjson/docjson), or other hypermedia content types
- Citation generation

External service integration:

- [schema.org](http://schema.org) microdata
- Google Scholar meta tags
- Twitter cards

## Scholarly Use
### Citation
Common citation formats should be supported via metadata dissemination (or possibly the existing Blacklight helpers).

### Annotation
Annotation can be more sophisticated than just item-level comments.  
Rich annotation tools may be more appropriate for stand-alone applications than Curate proper.

- Annotations should be persisted in Fedora. (Right?)
- Access permissions for annotations must be equivalent or _more_ restrictive than those of the subject.

### Arrangement
There are three types of "collections" used by Curate.

- Containers or "administrative collections" that bind together objects that can be considered a single unit e.g. a metadata record and two file records.
- Collections or "intellectual arrangements" are user-created groupings based on some theme, concept, or arbitrary criteria.
- Projects contain a working set of Containers or Items that supports ongoing research

Containers are first-order collections whose existence should be largely transparent to the end-user.

Collections are essentially an arbitrary arrangement of the material.
An Annotation defines the relationship between a Collection and the Items in that collection.
An Annotation and a Collection have basically the same metadata but an Annotation is a leaf and a Collection is a node.
Collections have several characteristics:

- Items are presented in an user-sortable list.
- Collections can link to other Collections.
- Collections can be presented in different ways e.g. list, gallery.
- A Collection can choose _one_ item to provide "representive media" for the collection e.g. image, video

Collections should adopt or adapt [Sufia's](https://github.com/projecthydra/sufia) notion of a Collection.

## API Design
Hypothesis: it would be cleaner to build a rich API in Curate that supports the development of client applications than to make many applications that talk to the same Fedora and Solr instances directly.

Dan has [written some about this](http://www3.nd.edu/~dbrubak1/planning/a-serviceable-digital-repository/).
There are still a lot of unanswered questions --- the proposed solution may just be moving complexity around rather than making the entire system better.

API implmentiaton should employ something like [JSON API](http://jsonapi.org).

