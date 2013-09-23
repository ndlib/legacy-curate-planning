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

### Commit Messages

* Commits should reference the relevant Github Issue(s). For example:

> Adds tests for issue ndlib/planning#1

This will automatically create links between your commit and the issue. 
See https://github.com/ndlib/curate/commit/25a37311265461f757cb304b69132d767ac427f3 for an example.

We have multiple codebases, but a single repo for issues, so without this cross-linking between 
commits and issues, it's quite difficult to track what's happening where.

* If appropriate, use commit messages to close the relevant issue. For example:

> Closes ndlib/planning#2

See https://help.github.com/articles/closing-issues-via-commit-messages for more details. 
Note that you may *not* want to do this if you need a pull request to clear before closing the issue.

### Pull Requests

PROPOSED:

We will use the [Contributing Guidelines for Project Hydra][4] with the following caveat:

* A Pull Request must be reviewed and ultimately merged by a person that is not of the submitter's institution (i.e. Notre Dame cannot merge Notre Dame's work)

[1]:http://robots.thoughtbot.com/post/50655960596/sandi-metz-rules-for-developers "Sandi Metz' Rules for Developers"
[2]:https://github.com/projecthydra-2013-partner-sprints "A Temporary Github Organization"
[3]:https://github.com/projecthydra
[4]:https://github.com/projecthydra/hydra/blob/master/CONTRIBUTING.md
