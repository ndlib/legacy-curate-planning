# Coding Rules and Procedures

* [The Rules for Code](#the-rules-for-code)
* [Can I Break These Rules?](#can-i-break-these-rules)

## The Rules for Code

We will be following [Sandi Metz' Rules for Developers][1].

> Here are the rules:
>
> * Classes can be no longer than one hundred lines of code.
> * Methods can be no longer than five lines of code.
> * Pass no more than four parameters into a method. Hash options are parameters.
> * Controllers can instantiate only one object. Therefore, views can only know about one instance variable and views should only send messages to that object (@object.collaborator.value is not allowed).

## Can I Break These Rules?

Yes. But the person merging your code is the one that will decide if it is okay to do so.

[1]:http://robots.thoughtbot.com/post/50655960596/sandi-metz-rules-for-developers "Sandi Metz' Rules for Developers"