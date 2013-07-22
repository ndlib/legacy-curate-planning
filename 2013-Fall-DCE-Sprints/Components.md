# Curate Components
Curate is a Institutional Repository (IR) solution.
It's goal is to accommodate a wide variety of data and metadata without forfeiting the ability to craft management and discovery experiences for very specific use cases.
To that end the design of Curate will deliberately provide seams between functional concerns.
This should allow the application to scale horizontally by adding components that share a common interface.

We will be using three methods to ensure modularity and consistency between the components of Curate:

- The Linter as Interface Pattern
- The Mountable Engine Pattern
- The Background Worker Pattern

These three design conventions will be explained in more detail elsewhere.

## User Management
User account management must negotiate the intersection between authentication, authorization, and authority control.
Our initial user base will be people that have an active on-campus status.
This means we can just lean on our campus CAS to handle authentication.

In the future we will be expanding our services to other groups e.g. alumni or researchers at other institutions.
When that happens we will need to support more than one authentication system.
The hierarchy of authentication systems will probably be:

1. CAS
2. Shibboleth
3. OAuth/OmniAuth (e.g. Log in with Google, Facebook, etc.)
4. Local Accounts

While technically feasible this is a thorny UX proposition.
Perhaps we can consolidate some of these options to smooth over the experience.

Let's get some terms straight:

A User is someone actively interacting with the repository.  
A User object will be persisted using ActiveRecord.  
A User has a one-to-one relationship with a Person.

A Person is the canonical representation of someone in the repository.  
A Person object will be persisted in Fedora.  
A Person can exist without an associated User account.

There will need to be some sort of "account manager" that negotiates the relationship integrity and data synchronization between a User and a Person.

Controlling what options are available to a User is another set of concerns.
We will need some sort of role-based authorization service.
There are lots of options for implementing this sort of thing.

## Content Types
We want to accommodate the deposit, description, preservation, and dissemination of a wide variety of data.
We are using Curation Concerns to address different types data or repository use cases.

Alex Papson, our metadata librarian, has identified 13 kinds of "content primitives".
Content Primitives contain the metadata schema and template for persisting the description a work.
A Curation Concern bundles a Content Primitive with instructions about how to present a type of work in different contexts e.g. as a form, as JSON, as HTML.

We would like to have reference implementation of Curation Concerns for all of the Content Primitives.
We would also like the ability to create Curation Concerns that are tailored for specific contexts or purposes.

### Content Type Registry
We want to have a single controller than handles the creation and management of items via Curation Concerns.
An actor or service will mediate the interaction between this controller and each type of Curation Concern.
This style of implementation reduces the overhead for adding new Curation Concerns as well as sharing Curation Concerns between different installations of the Curate framework.

In order for this to function there needs to be a notion of a "type registry" for Curation Concerns.
This registry provides a way for all the Curation Concerns in an application to stand up and be counted.
Because the registry is created at runtime you can add new Curation Concerns to an application without having to alter the application code.

### Interface
A CurationConcern should provide:

- An "owner" or responsible party (`#responsible_party`) e.g. `User`, `Group`, `#notifiable`
- A presenter that takes the raw object and exposes a tidy representation of it ([Draper](https://github.com/drapergem/draper) is one way to do this).
- A form builder (or view partial) for each mode of interaction (new, edit, review, etc.). View partials are preferably built using [SimpleForm](https://github.com/plataformatec/simple_form).
- A Workflow Mediator (this can return `nil` if there aren't any workflow states)
- A Dissemination Mediator (the simplest implementation can just return the object itself)

## [Activity Monitoring & Messaging](https://github.com/ndlib/satchel)
We need a way of instrumenting actions performed while users interact with repository content.
The resulting activity logs will allow us to measure user engagement with the repository.
They will also allow us to provide detailed usage reports for individual depositors.
Similarly the activity monitoring system will provide a mechanism for reporting on workflow state.

This component will probably look something like [PublicActivity](https://github.com/pokonski/public_activity).
The primary difference is that we need separate storage engines for watching (ActiveFedora) and logging (ActiveRecord) while PublicActivity assumes the storage engine will be the same for watching _and_ logging (both are ActiveRecord).
The design may also take some cues from the Event system in 
[sufia](https://github.com/projecthydra/sufia).

Setting up Activity Monitoring will look something like:

    ActivityEngine.config do |config|
      config.register_activity(controller_name, action_name) do |controller, observed_object, current_user|
        # Construct the message
      end
    end

Ruby doesn't have a strict equivalent of an [interface in Java](http://en.wikipedia.org/wiki/Interface_%28Java%29).
However, you _can_ test the API conformance of an object by using a Linter e.g. [ActiveModel::Lint::Test](http://api.rubyonrails.org/classes/ActiveModel/Lint/Tests.html).
A Linter for the ActivityEngine would give us a way to codify the desired object interface.
This makes Activity Monitoring available to any object that passes the tests present in our linting class (ActivityEngine::Lint::Test).

### Interface
The ActivityEngine will deliver:

- A mountable, namespaced engine
- `<%= render_activtiy_for %>`
- `/?/activity/:object_class/:pid/all`
- `/?/activity/:object_class/:pid/(?q=:q)`
- authentication & authorization for route will be determined by the`:object_class` and `:pid`
- `Activity.stats_for(object)`

## Authority Management
We are building a graph.
We are building it bigger.[*](http://en.wikipedia.org/wiki/Comfort_Eagle)

In order to maintain the referential integrity of the graph we need good authority control.
This has implications for the construction of authority objects (like Person) and for controlled vocabularies present in our metadata editing interfaces. At the very least we will need to support:

- Authority-backed controlled vocabularies stored by reference (URI, not string value)
- Locally managed controlled vocabularies e.g. a list of programs of study for an ETD
- Multiple unique identifiers for Authority Objects e.g. PID, ORCID, and Google Plus ID for a Person

## Mediation Channels
Mediation Channels are state machines that describe the processing of a work irrespective of its type.
A Curation Concern can have a default mediation channel.
However, which Mediation Channel is presently applicable for a given work is determined by a Mediation Broker.
This interaction could be implemented like this: 

    MediationBroker.get_mediator_for(concern.responsible_party)

## Dissemination Systems
Capturing, describing, and preserving data is only half of the equation.
Leveraging the data and metadata present in an IDR is central to the value proposition of the entire system.
Dissemination Systems should be able to be freely associated with Curation Concerns.
This lays the foundation for providing a constellation of services that consume repository data.

### File Dissemination
Most files suitable for preservation do not make good access copies.
The preservation files are either too large or have non-web-friendly MIME types.
For both of these reasons we will need to build dissemination systems for different sets of file types:

- Documents (Word, PDF, etc.)
	- Generate a PDF from the original file
	- Expose the PDF directly
	- Present the content via a native web interface like the [DocumentCloud DocViewer](https://github.com/documentcloud/document-viewer)
- [Images](http://www3.nd.edu/~dbrubak1/planning/building-an-image-pipeline/)
- [Audio & Video](http://www.avalonmediasystem.org)

### Metadata Dissemination
We want the metadata schema and templates for the works being deposited in the IR to be as descriptive as possible.
This is great for preservation and discovery purposes but we will also want more concise representations of this information.
Each work should be able to be cast into other contexts like:

- Citation generation
- [Google Scholar tags](http://www.google.com/intl/en/scholar/inclusion.html#indexing)
- [Schema.org](http://schema.org) attributes
- [Twitter Cards](https://dev.twitter.com/docs/cards)

There are also times when we want to return representations of a work in another format like:

- XML
- JSON
- [collection+json](http://www.amundsen.com/media-types/collection/)
- Hypermedia-compliant XHTML
