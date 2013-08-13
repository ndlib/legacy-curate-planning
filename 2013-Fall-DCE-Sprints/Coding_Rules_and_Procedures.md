# Coding Rules and Procedures

* [The Rules for Coding](#the-rules-for-code)
* [The Procedures for Collaboration](#the-procedures-for-collaboration)

## The Rules for Coding

We will be following [Sandi Metz' Rules for Developers][1]:

> Here are the rules:
>
> * Classes can be no longer than one hundred lines of code.
> * Methods can be no longer than five lines of code.
> * Pass no more than four parameters into a method. Hash options are parameters.
> * Controllers can instantiate only one object. Therefore, views can only know about one instance variable and views should only send messages to that object (@object.collaborator.value is not allowed).

### Can I Break These Rules?

Yes. But the person merging your code is the one that will decide if it is okay to do so.

## The Procedures for Collaboration

Given that this is a multi-institution collaboration, we will be leveraging Github for our development process.

* Pull Requests will be accepted/discussed on Github.
* Milestones will be created in Github.
* Issues will be tracked in Github.

To best facilitate this, we will be collaborating via the [ProjectHydra 2013 Partner Sprints Github Organization][2].
It is envisioned that some of the components created as part of this Github Organization will be migrated to the [Project Hydra organization][3].

### Pull Requests

PROPOSED:

We will use the [Contributing Guidelines for Project Hydra][4] with the following caveat:

* A Pull Request must be reviewed and ultimately merged by a person that is not of the submitter's institution (i.e. Notre Dame cannot merge Notre Dame's work)

[1]:http://robots.thoughtbot.com/post/50655960596/sandi-metz-rules-for-developers "Sandi Metz' Rules for Developers"
[2]:https://github.com/projecthydra-2013-partner-sprints "A Temporary Github Organization"
[3]:https://github.com/projecthydra
[4]:https://github.com/projecthydra/hydra/blob/master/CONTRIBUTING.md
