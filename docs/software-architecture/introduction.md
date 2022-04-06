---
sidebar_position: 1
---

# Introduction

Why is there an entire section dedicated to software architecture? Is it that important? What is software architecture in the first place? Do we actually need it? "I've worked on projects where I never had to worry about it, or it never even came up, so it must no be that important, right?"

Well, as we'll see, software architecture is of utmost important in a software project, and **every project has an underlying architecture**, even if it's implicit or just blurry and messy.

Software projects can get very expensive and complex. There's a point in which the codebase becomes so large that it's impossible to keep a clear mental picture of it, and that's where it gets dangerous.

As of 2020, around **66% of all software projects fail**, now that's a big number. Software Architecture (or the lack of it) plays an important role in that, as we'll see, architecture plays an important role in **taming complexity**, estimating project costs, providing ways to measure the system, and much more. It gives all stakeholders a big picture over the entire system, serving not only software engineers, but project managers, and business stakeholders as well. It becomes the basis of communication between all this parties.

Many parallels can be drawn between software engineering and civil engineering. They are both engineering fields, they develop or construct something, they have to deal with complexity, they must have some sort of planning beforehand (even if it's very little). However, a great difference between those two fields is that, while on civil engineering whatever is getting built is tangible, that is you can see the building or the bridge before your eyes, in software engineering the product is intangible, and the effects of that are huge. For example, if you're building a bridge and there's a big crack in the middle of it, you can just see it and evaluate if it's possible to fix it or not before opening up to people or cars to go by. In software, there can be a huge bug in the middle of the project, and it can go unnoticed until it reaches production, and people are actually using it. Now that can get very dangerous, imagine if this system is handling sensitive information such as banking data, or what if it's a software that controls an airplane? For that, an many other factors, architecture is of vital importance in a software project. Nobody would argue that we need architecture plans before constructing a building, and so it should be even more important to have architecture plans to construct a "building" that you can't really see.

Now one may think that while is justifiable to have architecture on large projects, small to medium projects shouldn't have to waste time on that, time to production is of utmost importance, and so architecture can get in the way of that and not provide that much of a benefit. While some part of that is true, we'll see further how to use architecture in Agile projects, and how the project can benefit tremendously of using "just enough" architecture.

So let's begin this journey, what is software architecture in the first place, huh?

## What is Software Architecture?

### What Software Architecture Is and Isn't

Software systems are constructed to satisfy business goals. The architecture plays a role of a bridge between those (often abstract) business goals and the final (concrete) software system. There are tons of technical definitions of software architecture, here's one that we like:

**The software architecture of a system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both.**

#### Architecture is a Set of Software Structures

The first part of the definition says that it's a "set of structures", a structure is a group of elements held together by a relation. In architecture, there are three types of structures that will play an important role in the design, documentation, and analysis of an architecture:

1. **Modules**: some structures partition the system into implementation units. We'll call this **modules**, they become the basis of **work assignment** in a project. This are **static structures** because they focus on the way the system's functionality is divided and assigned to teams for implementation.
2. **Dynamic Structures**: Other structures are dynamic, meaning that they focus on how elements interact with each other at runtime to carry out the systems functionality. We'll call this **component-and-connector (C&C)**
3. **Allocation Structures**: A third kind of structure describes the mapping of software structures to the systems organizational, development, installation, and executional environment. As an example, this can describe which structure will run in a certain processor, or the file system structure used to organize the codebase.

Most importantly, **a structure is architectural if supports reasoning about the system and the system's properties**. The reasoning should be about an attribute of the system that's important to some stakeholder. And so the number of lines that contains the letter "a" is not an architectural structure.

#### Architecture is an Abstraction

The architecture is an abstraction that provides a way to reason about certain elements of the system, highlighting certain element and details, while hiding not useful information. An important part of that is **hiding** elements that aren't useful to reasoning about the system, this plays a crucial role in **taming complexity**, we do not want to reason about all the elements all the time.

#### Every Software System Has a Software Architecture

Every system can be shown to comprise elements and the relations among them. Even when the architecture isn't made explicit or known by the stakeholders, it still exists and manifests itself on the system.

#### Architecture Includes Behavior

A very important aspect needed to reason about the system is understanding it's behavior, and so architecture also comprises the behavior of structures, and how they interact with each other.

With this one can see that only reasoning about modules and separation of concerns is not enough to define an architecture, one must also think and reason about the behavior of this structures at runtime.

The behavior of each element is part of the architecture as far as it can be used to reason about the system.

### Architectural Structures and Views

Orthopedists, hematologists, and dentists all need different views of the human body to do their work. Each view gives insights into different areas of the human architecture, which can be used to reason about the system and make decisions. The same happens with software architecture, we focus on a set of views to reason about some part of the system that's currently being discussed.

#### Structures and Views

We've already talked about structures and their roles in architecture, now with views, one may wonder what's the relation or difference between them:

- A view is a group of a coherent set of architectural elements as written by and read by steak holders. It's a representation of a set of elements and relationships amongst them
- As we've seen, structures are a set of software or hardware elements living in the system itself

**Architectures design structures. They document views of those structures.**

#### Three Kinds of Structures

Let's now revisit the three kinds of structures we went over above and talk about them a little deeper:

1. **Module**: Modules embody decisions as to how the system should be structured into a set of logical units. They represent a static way to reason about the system, each module having a clear functional responsibility. Module structures gives us great insights into the **modifiability** of a system, and usually allows us to answer the following questions:

   - _What is the primary functional responsibility assigned to each module?_
   - _What other software elements is the module allowed to use?_
   - _What other software does it actually use and depends on?_
   - _What modules are related to other modules by generalization or specialization (classes & inheritance)?_

2. **Component-and-Connector**: These structures embody decisions as to how the system is to be structure as a set of elements that have runtime behavior and interactions. These structures can give us insights into a system's performance, availability, security, and more. Some of the questions that it helps us answer are:

   - _What are the major executing components and how do they interact at runtime?_
   - _What are the major shared data stores?_
   - _Which parts of the system are replicated?_
   - _Which parts of the system can run in parallel?_
   - _How does data progress through the system?_
   - _Can the systems structure change as it executes, and, if so, how?_

3. **Allocation Structures**: these embody decision as to how software structures relate to non-software structures in a given environment (such as file systems, processors, etc.). These can help us answer the following questions:
   - _What processor does each software element runs on?_
   - _How the software is organized and divided in a file system?_
   - _How each software element is assigned to development teams?_

#### Structures Provide Insight

Structure provides insights on the **Quality Attributes** of a system, but more importantly choosing the right structures will bring forth the desired quality attributes for a given system.

As always, less is more, and so only design and document structures that bring value to the project, usually in terms of decreased development or maintenance costs.

#### Structure Relations

Elements of one structure will be related to elements of other structures. For example, one module structure can become one component at runtime, or a part of a component, or several components. Usually relations between structures are many-to-many.

## Why is Software Architecture Important?

Hopefully you're already convinced that software architecture is important by some of the things discussed above, however, let's take some time to have a deeper look into the importance of architecture in a software project, and the benefits that we can have from it.

### Inhibiting or Enabling a System's Quality Attributes

One of the most important parts of an architecture, and really something that the architecture itself evolves around it, are **Quality Attributes (QA)**. By looking at a systems architecture, we're able to tell which QAs this systems has and to which degree they're prevalent. For example, by looking at a system architecture, we may be able to tell how performant it is, and how easy it is to modify it.

Further, we'll see that a big part of designing an architecture is gathering QA requirements, and with those in mind, we're able to inhibit or enable certain QAs depending on which structures we choose.

However, architecture by itself does not ensure a systems QAs, a good architecture is necessary, but not sufficient, to ensure quality. Achieving quality must be considered throughout design, implementation, and deployment.

### Reasoning About and Managing Change

These days roughly 80 percent of software systems total costs occur after initial deployment. Now that's a lot of change. Because of that, **modifiability**, a Quality Attribute, is of utmost importance in most systems, and it's the job of the architect to ensure that the system has good modifiability to the extent that it needs it.

There are essentially three kinds of changes:

- _local changes_: these are changes made to local modules or elements, and there's no need to change any other software elements because of it.
- _nonlocal changes_: these changes are the ones in which local changes don't suffice, and so by changing a part of the system, other parts of the system must consequently change as well
- _architectural changes_: now these are the big kinds of changes, ones that change the underlying structure of the entire system, and so virtually all software elements will have to change. An example of this is moving from client-server to peer-to-peer.

With that in mind, the architect wants to anticipate that most of the changes made to the system will be local, having the least cost.

### Enhancing Communication Among Stakeholders

The architecture provides a base of communication between technical and non-technical stakeholders, the abstraction of the system that it provides, allows all stakeholders to have a better grasp and mental model of the system, which improves communication on all parties.

### Carrying Early Design Decisions

Software architecture is a manifestation of the earliest design decisions about a system, and these early bindings carry an enormous weight with respect to the system's remaining development, its deployment, and its maintenance life.

Design at it's core it's about making decisions, designing an architecture is no difference. The thing is that the earliest decisions usually carry the most weight because they restrain all the following decisions down the road, and so it's of extreme importance to a systems health and life that these early decisions are made consciously and mindfully. Changing this early decisions down the road can become extremely costly.

### Defining Constraints on an Implementation

An implementation exhibits an architecture if it conforms to the design decisions prescribed by the architecture. This means that the implementation must be implemented as a set of prescribed elements, and theses elements must interact with each other in a prescribed fashion, and each of these elements must fulfill its responsibility to the others as dictated by the architecture. Each of these prescriptions is a constraint on the implementer.

### Influencing the Organizational Structure

Not only does the architecture prescribes constraints on implementation, it also dictates the organizational development of the project.

Because the architecture is the broader decomposition of a system, it gets used for work-breakdown between development teams, which in turn dictates units of planning, schedule, and budget; as well as configuration control, and file-system organization; integration and test plans and procedures.

### Enabling Evolutionary Prototyping

Once an architecture has been defined, it can be analyzed and prototyped as a skeletal system. A skeletal system is one in which at least some of the systems infrastructure is built before much of the systems functionality is created. This allows for less time to production, and it also reduce risks on the project.

### Improving Costs and Schedule Estimates

Because a lot of the planning and decision making goes into the architecture, we're able better predict costs of development, and catch some of the road blocks or poor decisions early on, as opposed to in the middle of the implementation.

It's the job of the architect to help the project manager to create cost and schedule estimates early on the project life cycle.

### Supplying a Transferable, Reusable Model

The earlier that reuse is applied, the greater the benefit that can be achieved. While code reuse is good, reuse of architectures can provide tremendous leverage to systems with similar requirements. By reusing an architecture that fits the systems requirements, and that has already been through the battlefield, the system inherits all the benefits and quality attributes of that architecture without having to go through the possible trial-and-error period that it took the original architecture to get it's qualities.

### Providing a Basis for Training

The architecture and it's documentation can serve as a basis for training new developers as well as for any other non-technical stakeholders.

By reading through the views of the architecture, a person can become acquainted with the project much more quickly, instead of going directly into the trenches.

## Contexts of Software Architecture

While focusing on software architecture or being an architect, it's tempting to think of the architecture as the most important piece in the software system. However, we shouldn't fall into that trap, we must know that the architecture only plays a role in the system, a role that can be very important as we already saw, but nonetheless a role. On the following parts we'll take a look at this role that architecture plays on different contexts of the system:

- _Technical_: What role does an architecture play in the technical part of the system?
- _Project Life Cycle_: In which part of the life cycle does the architecture fit in, and how does it relate to other phases?
- _Business_: How does the presence of an architecture influences the organization business environment?
- _Professional_: What's the role of an architect in an organization and on a project?

### Technical

From a technical point, the architecture can enable or inhibit a systems quality attributes. We very briefly went over quality attributes, these are things like modifiability, security, performance, usability, testability, and so on.

It's the job of the architect to understand the systems quality attribute requirements (alongside with other requirements), and build an architecture that enables those QAs be present on the system.

Keep in mind that, as we've seen before, only the architecture by itself does not guarantees that the system will have those attributes, for that the implementation must abide to the architecture's prescribed elements, structures and relationships.

### Project Life-Cycle

There are four dominant software development processes:

1. _Waterfall_: This is the first dominant software development process. It organizes the cycles in a series of connected sequential activities, each with entry and exit conditions, and formalized relationships to it's upstream and downstream neighbors. The process began with requirements specifications, followed by design, then implementation, then integration, then testing, then installation, all followed by maintenance.
2. _Iterative_: Out of the feedback generate at each waterfall step, it became clear that it was better to think about development as a series of short cycles through the steps - some requirements lead to some design, that leads to some implementation - these short cycles are called iterations, and must deliver working software at the end of it. The most important and risky decisions are dealt with on the early iterations.
3. _Agile_: Agile Software Development refers to a group of software methodologies which are all incremental and iterative. What distinguishes Agile is early and frequent delivery of working software, close collaboration between developers and customers, self-organizing teams, and a focus on adaptation to changing circumstances. Agile assumes that requirements always change to some extent at some point, so it focus is to be resilient and quick to respond to these changes. This may seem that Agile and architecture cannot coexist, we'll see that that's not actually the case further on.
4. _Model-Driven Development_: This process is based on the idea that humans shouldn't be writing code in programming languages, but instead should be creating models of the domain, from which the code is automatically generated.

As one can see, there's design in a part of all of these processes, and so that's we're the architect will do it's job. There are a number of activities involved in creating an architecture, no matter the development process, and these are:

1. Making a business case for the system
2. Understanding the architecturally significant requirements
3. Creating or selecting the architecture
4. Documenting and communicating the architecture
5. Analyzing or evaluating the architecture
6. Implementing and testing the system based on the architecture
7. Ensuring that the implementation conforms to the architecture

We'll go into each of these deeper in further chapters.

### Business

Architects need to understand who the vested organizations are and what are their goals. Many of these goals will have a profound effect on the architecture, usually arising as quality attributes requirements.

A development organization contributes many of the business goals that influence the architecture. For example, the organization may have already other systems in place that use a certain architecture, and so because it wants to reuse this assets, it wishes to have a similar architecture for future systems. Another case it that an organization has many skilled and experience programmers in P2P architecture, and so it may wish to go into that direction, to **be able to reuse assets it invested on**.

### Professional

What do architects do? As we'll see, producing an architecture is one of the many activities an architect must do, which we call duties. An architect needs to clearly communicate with different stakeholders to explain the difference between certain properties, and explain to a stakeholder why some of his expectations are not being fulfilled. And so the architect must be diplomatic, negotiate, and have good communication skills.

That's not all, an architect must also have up-to-date knowledge about (for example) patters, or database platforms, or web services standards.

This combination of knowledge, skills and duties form the architect's competence.

### Stakeholders

A Stakeholder is **anyone who has a stake on the success of the system**. You'll need to understand the nature, source and priority of constraints of a project as early as possible, and so you identify and engage with stakeholders early on to solicit their needs an expectations.

The underlying problem is that each stakeholder has it's own set of priorities and goals, some of which may be contradictory, an so one of the best advices is:

**Know your stakeholders. Talk to them, engage them, listen to them, and put yourself in their shoes.**

### How is Architecture Influenced?

A software architecture is the result of business and social influences, as well as technical ones. In particular, each of these contexts we just covered all play a role in influencing the architecture. In turn the architecture also influences all of this contexts

### What Do Architectures Influence?

Architectures are influenced by the contexts above, but they also end up influencing them as well. For example, in the technical context, an architecture may enable customers to receive a system in a timely and on budget manner, which may open the organization to loosen up some of it's original constraints. In the business context, a successful architecture may enable a business to set foot in a industry, allowing for further systems to be developed an new goals to arise.

As we've seen the architecture influences the project and organization by dividing the system into implementation units (modules), which then are used to work-breakdown, and form development teams.

Lastly, the architecture will influence the architect by his new experience (being good or bad), which in turn will influence future architectures that he'll design.
