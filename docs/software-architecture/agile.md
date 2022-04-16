---
sidebar_position: 3
---

# Architecture in Agile

## Introduction

Agile has been one of the most popular development methodologies in the past years. One of the reasons for that is because it responds to the needs of many business and startups, such as being able to deal with changing requirements, dealing with uncertainty, having a customer-centric approach, and being resilient.

The traditional way of building systems was to do a lot of up-front planning and documentation. While this still has it's place on the software world, it can lead to very strict projects, not leaving much room for creativity.

Because of the nature of the agile methodology of getting working software deployed as soon as possible, people may think that you should decide between agile vs architecture. We'll see why that's not true, and that architecture can, and in fact should, go hand in hand with the agile methodology. The true questions and decisions are: "How much architecture should I do now, and how much should I defer until requirements are somewhat clear?", "When, and how should I refactor?", "What aspects of the architecture are truly worth documenting at this moment, and for whom?".

Let's first take a closer look at agile. Agile methodology was born with the release of the agile manifesto, a simple and short document specifying 12 principles:

1. Our highest priority is to satisfy the customer through early and continuous delivery of valuable software.
2. Welcome changing requirements, even late in development. Agile processes harness change for the customer's competitive advantage.
3. Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
4. Business people and developers must work together daily throughout the project.
5. Build projects around motivated individuals. Give them the environment and support they need, and trust them to get the job done.
6. The most efficient and effective method of conveying information to and within a development team is face-to-face conversation.
7. Working software is the primary measure of progress.
8. Agile processes promote sustainable development. The sponsors, developers, and users should be able to maintain a constant pace indefinitely.
9. Continuous attention to technical excellence and good design enhances agility.
10. Simplicity--the art of maximizing the amount of work not done--is essential.
11. The best architectures, requirements, and designs emerge from self-organizing teams.
12. At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behavior accordingly.

In practice, the truth is that **successful projects enjoy a sweet spot mix of agile and architecture**. The exception to that are large projects who have clear and hard-to-change requirements, in those kinds of projects all the up-front planning and documentation pays off. To understand the reason behind that, imagine having to build a large building, or an airplane, it's undoubted that a big a mount of up-front planning should be done.

## How Much Architecture?

Too much upfront planning can lead to a strict project and a lot of time to have working software. On the other hand, too mich agile is chaos. Successful projects enjoy a mixture of both.

There isn't a prescribed formula or method to tell how much architecture is good for an agile project. However, every project has a **sweet spot**, where the project has **just enough architecture**. Just enough architecture to get the project going. The architecture can evolve with the project, and change as needed.

### Architecture Documentation

One of the aspects of the architecture that doesn't seem to have a place in agile is documentation. However, as stated previously, documentation should only be written when it provides value, and it should be written with the reader in mind. This goes hand in hand with agile principles, documentation can evolve with the project, and it doesn't have to be extremely thorough.

### Architecture Evaluation

Another aspect that doesn't seem to have a place in agile is architecture evaluation, but that's also not true. The reason for that is that there are many simple ways to evaluate an architecture to see if it's most important quality attributes are on it's way to getting achieved. Again, this also can go hand in hand with agile, provide just enough evaluation, that's made quickly, to provide feedback on the project for the important stakeholders

## Guidelines for the Agile Architect

A successful agile architecture is resilient and loosely-couple. It is composed of a set of well-reasoned design decisions but still has some "wiggle room" that allows modifications to be made and refactoring to be done without ruining the original structure.

An effective agile process will allow for the architecture to grow incrementally as the system grows and matures. The key to success is to have decomposability, separation of concerns, and near-independence of parts of the architecture (not surprisingly all modifiability tactics).

Further, to be agile the architecture should be well defined and self-evident in the code, this means making the design patterns, cross-cutting concerns, and other important decisions obvious, well communicated, and defended.

1. If you are building a large and complex system with relatively stable and well-understood requirements, it is probably optimal to do a large amount of architecture work up front (see Figure 15.1 for some sample values for “large”).
2. On big projects with vague or unstable requirements, start by quickly designing a complete candidate architecture even if it is just a “PowerPoint architecture,” even if it leaves out many details, and even if you design it in just a couple of days. Alistair Cockburn has introduced a similar idea in his Crystal Clear method, called a “walking skeleton,” which is enough architecture to be able to demonstrate end-to-end functionality, linking together the major system functions. Be prepared to change and elaborate this architecture as circumstances dictate, as you perform your spikes and experiments, and as functional and quality attribute requirements emerge and solidify. This early architecture will help guide development, help with early problem understanding and analysis, help in requirements elicitation, help teams coordinate, and help in the creation of coding templates and other project standards.
3. On smaller projects with uncertain requirements, at least try to get agreement on the central patterns to be employed, but don’t spend too much time on construction, documentation, or analysis up front. In Chapter 21 we will show how analysis can be done in a relatively lightweight and “just-intime” fashion.
