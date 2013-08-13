# Glossary of Terms

IR - Institutional Repository

Account - an entity that can authenticate with the IR
User - An Account that is assigned to a human; A User has a one to one relationship with a Person
Software Agent - a Account that is assigned to a non-human (for API access)
Person - a named singular entity; A Person may have a one to one relationship with a User.

Group - A set of Accounts
Reporting Group - A Group used to aggregate reporting statistics
Access Group - A Group that confers Privileges to its Accounts
Privilege - Defines what an Account can see and what an Account can do 

Content - Abstract; Contains reference to something and metadata; Its encouraged that Content should belong an implementation of a Primitive Container; (i.e. Think of Content as a proton in physics; it prefers to be a part of something);  It is Collectible
Embedded Content - Stores Files, derivatives, and Technical Metadata; It has Access Controls
Linked Content - Stores a reference to the Canonical location, and Descriptive Metadata

Audio File - A type of Embedded Content
Video File - A type of Embedded Content

Primitive Container - Abstract; It contains Descriptive Metadata; A set of references to Content; (e.g. Senior Thesis is an implementation of a Primitive Container); It has Access Controls; It is Collectible

Collectible - A Repository Object (i.e. Content, Primitive Container, Collection) that can be part of a Collection.

Collection - It is a set of Collectibles; It has Access Controls defining which Accounts can add or remove Collectibles; It is Collectible; It contains Descriptive Metadata

Project - It is a synonym for Collection

Dataset - An implementation of a Primitive Container
Senior Thesis - An implementation of a Primitive Container
