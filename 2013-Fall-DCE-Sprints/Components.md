# Curate Components
Provide seams between functional concerns  
Scale horizontally by adding components that share a common interface  
Mountable Engine Pattern  
Background Worker Pattern

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
Doing it this way will reduce the overhead for adding new Curation Concerns and sharing them between implementations of Curate.

In order for this to function there needs to be a notion of a "type registry" for Curation Concerns.
This registry provides a way for all the Curation Concerns in an application to stand up and be counted.
Because the registry is created at runtime you can add new Curation Concerns to an application without having to alter the application code.

### Presentation
Each Curation Concern contains a presenter that takes the raw object and exposes a tidy representation of it ([Draper](https://github.com/drapergem/draper) is one way to do this).
They also contain a form for editing the work---preferably built using [SimpleForm](https://github.com/plataformatec/simple_form).

## Monitoring & Event Messaging
Log activity  
Conditional alerts  
Notification engine

## Authority Management
We are building a graph.
We are building it bigger.[*](http://en.wikipedia.org/wiki/Comfort_Eagle)

In order to maintain the referential integrity of the graph we need good authority control.
This has implications for the construction of authority objects (like Person) and for controlled vocabularies present in our metadata editing interfaces. At the very least we will need to support:

- Authority-backed controlled vocabularies stored by reference (URI, not string value)
- Locally managed controlled vocabularies e.g. a list of programs of study for an ETD
- Multiple unique identifiers for Authority Objects e.g. PID, ORCHID, Google Plus ID for a Person

## Mediation Channels
Mediation Channels are state machines that describe the processing of a work irrespective of its type.
A Curation Concern can have a default mediation channel.
However, which Mediation Channel is presently applicable for a given work is determined by a Mediation Broker.
This interaction could be implemented like this: 

    MediationBroker.get_mediator_for(concern.user)

## Dissemination Systems
Capturing, describing, and preserving data is only half of the equation.
Leveraging the data and metadata present in an IDR is central to the value proposition of the entire system.
Dissemination Systems should be able to be freely associated with Curation Concerns.
This lays the foundation for providing a constellation of services that consume repository data.

### File Dissemination
MIME Type

### Metadata Dissemination
Citation generation  
Display medium (accepts headers)
