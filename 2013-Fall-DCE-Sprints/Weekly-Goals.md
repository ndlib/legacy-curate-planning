# Week 1

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
- Ability to display contents of **Containers**

# Week 2

- Generate Activity Entries on a Collectible
	- Given I am logged in, when I create a Container, then the IR will create an Activity Entry stating I created the Container.
	- Given I am logged in, when I update a Container, then the IR will create an Activity Entry stating I updated the Container.
	- Given I created a Container, when an anoymous user views the Container, then the IR will create an Activity Entry stating someone viewed the Container.
	- Given I created a Content, when an anoymous user downloads the Content, then the IR will create an Activity Entry stating someone downloaded the Content.
- Display Activity Entries for a User
	- Given I am logged in, and I create a Container, then I will see an Activity Entry for the Container in my Activity Stream
	- Given I am logged in, and someone else has downloaded Content that I created, then I will see an Activity Entry for the Content in my Activity Stream

Week 3

Week 4

Week 6

Week 7

Week 8

Week 9