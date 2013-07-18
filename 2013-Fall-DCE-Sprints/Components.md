# Curate Components

## User Management

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

## Authority Management

## Mediation Channels
Mediation Channels are state machines that describe the processing of a work irrespective of its type.
A Curation Concern can have a default mediation channel.
However, which Mediation Channel is presently applicable for a given work is determined by a Mediation Broker.
This interaction could be implemented like this: 

    MediationBroker.get_mediator_for(concern.user)

## Dissemination Systems

### File Dissemination

### Metadata Dissemination
