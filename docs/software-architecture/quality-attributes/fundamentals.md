---
sidebar_position: 1
---

# Fundamentals

## Introduction

So far we've used the term Quality Attribute loosely, so let's provide a more formal definition:

**A Quality Attribute is a measurable or testable property of a system that's used to identify how well the system satisfy the needs of it's stakeholders.**

You can think of a quality attribute as measure the "goodness" of a product along some dimension of interest to a stakeholder.

## Architecture and Requirements

Requirements comes in all kinds of forms: text documents, user stories/scenarios, organization needs, and so on. Further on, we'll see what are they _architecturally significant requirements_, and how to identify those. Even though requirements come in many forms, they can be categorized into three buckets:

1. _Functional Requirements_: This requirements specify what the systems must do, what end result it should achieve, and how it must behave or react at runtime.
2. _Quality Attribute Requirements_: While functional requirements are concerned on what to do, QA requirements are concerned with how well the system carries that functionality.
3. _Constraints_: These are decisions that have already been made, and so the project must abide to it.

What's the architecture response to these three types of requirements?

1. Functional requirements are met by assigning functional responsibilities to units of the system. Assigning responsibilities to architectural elements is a fundamental architectural design decision
2. Quality attribute requirements are satisfied by the various structures designed into the architecture, and how the behavior and interactions of the elements that populate these structures
3. Constraints are met by accepting the design decisions and reconciling it with other affected design decisions

## Functionality

Functionality is the ability of the system to do the work it was intended.

One may think that functionality determines architecture, but that's not true at all. Given a set of functionalities, that are an infinite amount of architectures that can be created to satisfy those functionalities. Although functionality is independent of any particular structure, **functionality is achieved by assigning responsibilities to architectural elements**.

## Specifying Quality Attribute Requirements

As we've seen, functionality is the purpose of the system, and quality attributes specify how well that functionality gets carried out.

Quality Attributes can be divides into two categories: those that specify how well the system functions at runtime, such as availability and performance, and those that describe some property of the development of the system, such as modifiability and testability.

With complex systems, quality attributes can never be achieved in isolation, that is decisions about one quality attribute will positively or negatively affect other quality attributes. As an example, almost every other quality attribute affects performance, improving modifiability by decoupling components can introduce overhead, same with portability.

Discussing quality attributes can become really subjective, and so we'll use a framework to make our discussion more concrete. This framework will specify a generic quality attribute scenario, which each QA will use to specialize to it's own needs. Further we'll also discuss tactics for each QA, as well as QA decisions to be made on 7 specific categories.

Let's first look at the general quality attribute scenario:

1. _Stimulus_: First there's a stimulus on the systems (which can come from a human, or another computer for example).
2. _Stimulus Source_: Each stimulus must have a source
3. _Response_: How does the system responds to that stimulus?
4. _Response Measure_: Specifies if the response was satisfactory or not, and how to measure or test it
5. _Environment_: Specifies which environment was the system when it received the stimulus
6. _Artifact_: Finally, this is the part of the system to which the requirement applies. Frequently this is the entire system, but in some occasions it can only be a portion of the system

## Achieving Quality Attributes Through Tactics

We've briefly talked about architecture patterns, and how they can generate a reliable way to achieve given quality attributes. However, patterns are like a bundle of already made decisions, which come with their own tradeoffs. To successfully must understand the original problem it solves, and see if that matches your current system's problems, usually the pattern will need some tweaking to fit your needs. So instead of focusing on patterns, we will focus on what we call **tactics**.

A tactic is a design decision that influences the achievement of a quality attribute.

Tactics are the small building blocks of patterns, a pattern is composed of a bunch of tactics. While patterns are used to achieve multiple quality attributes, the focus of a tactic is on a single quality attribute.

You can see that by understanding the building blocks of patters, we can be much more resilient and have a more solid knowledge foundation, because we're then able to take a pattern and add or remove a few of it's tactics according to our needs. Further, if no pattern happens to solve our problems, we can derive an architecture from tactics.

By understanding the fundamental building blocks of patterns, we're understanding **principles**, and that's the best way to master anything.

## Guiding Quality Design Decisions

A software architecture can be viewed as a collection of design decisions. These decisions can be divided essentially into seven categories:

1. Allocation of responsibilities
2. Coordination Model
3. Data Model
4. Management of Resources
5. Mapping among Architectural Elements
6. Binding Time Decisions
7. Choice of Technology

### Allocation of Responsibilities

These category comprises decisions related to the **assignment and/or division of responsibilities to software elements of the system**. These are the decisions that ensure (or not) that the system's requirements get carried out.

This includes the following:

- Identifying the important responsibilities, including basic system's functions, architecture infrastructure, and satisfaction of quality attributes
- Determining how these responsibilities are allocated to non-runtime and runtime elements.

Strategies for making these decisions include functional decomposition, real-world objects, grouping based on the major modes of system operation, or grouping based on similar quality requirements, processing frame rate, security level, or expected changes.

### Coordination Model

On a software system, elements interact with each other, and these depending on the size of the system, coordinating all these interactions can get quite complex. Decisions on **how the elements should interact** are Coordination Model decisions, and these include:

- Identifying elements in the system that must coordinate, or are prohibited from coordinating
- Determining the properties of coordination, such as timeliness, completeness, correctness, currency, and consistency
- Choosing the communication mechanisms (between systems, or a system and external entities, or between elements inside the system) that fulfill the coordination properties. Important properties of the communication mechanisms are stateful vs stateless, synchronous vs asynchronous, guaranteed delivery vs non-guaranteed delivery, and performance related properties such as latency and throughput.

### Data Model

Every system has data in some fashion, **the collection of representation of data and how to interpret them is called data model**. This includes decisions such as:

- Choosing the major data abstractions, their operations, and their properties. This includes determining how the data items are created, initialized, accessed, persisted, manipulated, translated and destroyed.
- Compiling metadata needed for consistent interpretation of data
- Organizing the data. This includes determining if the data is going to be stored in a relational database, a collection of objects, or both. If both, then mapping between the two different locations must be determined

### Management of Resources

An architect may need to arbitrate the use of shared resources in the architecture. These may include hard resources (CPU, memory, battery, hardware buffers, etc) and soft resources (system locks, software buffers, thread pools, and non-thread-safe code). This includes the following:

- Identifying the resources that must be managed and determining the limits for each.
- Determining which system elements manages each resource
- Determining how resources are sharing and the arbitration strategies employed when there is contention
- Determining the impact of saturation on different resources

### Mapping among Architectural Elements

As we've seen, there are three kinds of architectural structures: modules, C&C, and allocation structures. With that, there must be a mapping between them, mappings between a module and it's runtime elements, mapping between modules and the system file structure, mapping between a runtime component and a processor for example. This includes:

- The mapping of modules and runtime elements to each other - that is, the runtime elements that are created from each module; the module that contains the code for each runtime element
- The assignment of runtime elements to processors
- The assignment of items in the data model to data stores
- The mapping of modules and runtime elements to units of delivery

### Binding Time Decisions

Binding time decisions introduce allowable ranges of variant. This variation can be bound at different times by different entities. For example, a user may download a plugin to extend the system's functionality, or when installing the user may choose an array of settings, which leads to the system selectively initiating it's modules,and so on.

**A binding time decision establishes the scope, the point in the life cycle, and the mechanism for achieving the variation.**

The decision in the other six categories have associated binding time decisions. This includes the following:

- For allocation of responsibilities, you can have build-time selection of modules through a parametrized makefile
- For choice of coordination model, you can design runtime negotiation of protocols
- For resource management, you can design a system to accept new peripheral devices at plugged in at runtime, after which the system recognizes them and downloads and installs required drivers.
- For choice of technology, you can build an app store for a smartphone that automatically downloads the version of the app appropriate for the phone of the customer buying the app.

**When making binding time decisions, you must consider the costs to implement the decision, and the costs to make a modification after you have implemented the decision.**

### Choice of Technology

Finally, there's choice of technologies decisions. These are decisions of the practical technologies that are going to be used to carry out the system's requirements. For example, if you choose to use a relational database for the data model, are you going to use MySQL or PostgresSQL, or something else?

This includes:

- Deciding which technologies are available to realize the decisions made on the other categories
- Determining whether the available tools to support this technology choice are adequate for development to proceed
- Determining if the level of internal familiarity, as well as external support is adequate to proceed with the technology
- Determining the side effects of choosing the technology, such as an opinionated framework with a strict coordination model.
- Determining if whether the new technology is compatible with the existing tech stack.
