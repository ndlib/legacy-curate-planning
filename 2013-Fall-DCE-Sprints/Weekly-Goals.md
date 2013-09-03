# Week 1

Overarching Goal: Allow Deposit of Multiple Container Types; Before we can do anything more we have to show that we can accept things.

- Identify if we should be doing coding to Curate or Sufia; This will require reconciling the Glossary and Personas.
- Define the interface for Container, Content, and Collection
	- For data entry (via ActiveFedora::DelegateAttributes)
	- For anonymous display (via Hydra::ObjectViewer)
	- For authorized display (via Hydra::ObjectViewer)
- Ability to Create a **Project**
	- Given I am logged in, when I submit a valid form for a **Project**, then a **Project** is created.
	- Given I am logged in, and have indicated I am working on a **Project**, when I submit a valid form for a **Container**, then that **Container** is automatically associated with the **Project**
- Ability to deposit multipe types of **Containers**
	- Given I am logged in, when I submit a valid form for a **Container**, then a **Container** and its **Content** are created.
- Ability to search for **Containers**
	- Given I am not logged in, and one **Container** is "Open Access", and one **Container** is "Private", when I search the IR, then I the "Private" **Container** will not be in the search results.

- Ability to display contents of **Containers**
	- Given I am not logged in, and a **Container** is "Private", when I go to that **Container**'s public URL, then I will see only a stub of the **Container**'s information.
	- Given I logged in, and I created a "Private" **Container** , when I go to that **Container**'s public URL, then I will see the full information for the **Container**.


# Week 2

Overarching Goal: Record and Report the Activity that is happening; In doing this we can help highlight that things are happening.

- Generate Activity Entries on a Collectible
	- Given I am logged in, when I create a Container, then the IR will create an Activity Entry stating I created the Container.
	- Given I am logged in, when I update a Container, then the IR will create an Activity Entry stating I updated the Container.
	- Given I created a Container, when an anoymous user views the Container, then the IR will create an Activity Entry stating someone viewed the Container.
	- Given I created a Content, when an anoymous user downloads the Content, then the IR will create an Activity Entry stating someone downloaded the Content.
- Display Activity Entries for a User
	- Given I am logged in, and I create a Container, then I will see an Activity Entry for the Container in my Activity Stream
	- Given I am logged in, and someone else has downloaded Content that I created, then I will see an Activity Entry for the Content in my Activity Stream

# [Week 3 (3 September)](https://github.com/ndlib/planning/issues?milestone=6&page=1&state=open)

Overarching Goal: Meet the [General Faculty Persona](https://github.com/ndlib/planning/blob/master/2013-Fall-DCE-Sprints/Personas.md#general-faculty) use case.

- As a Faculty member, I can
	- Submit/add a work
	- Have that work be displayed on my profile page
	- Link one of my Articles to any of my Datasets (and vice versa)
- As a Faculty member, I can view metrics related to number of views, downloads of my Works.
- As a Faculty member, I can discover the Works (e.g. of my peers, subjects of interest) and Profiles

# Week 4 (9 September)

Week 6

Week 7

Week 8

Week 9
