---
sidebar_position: 5
---

# Designing an Architecture

"In most people's vocabulary, design means _veneer_. It's interior decorating. It's the fabric of the curtains or the sofa. But to me, nothing could be further from the meaning of design. Design is the fundamental soul of a human-made creation that ends up expressing itself in successive outer layers of the product or service."
\- _Steve Jobs_

## Introduction

We've taken a look at quality attributes and patterns/tactics to satisfy them, we've seen how to assemble ASRs from different sources, and we also saw how architecture can fit with Agile. However, up until now, all this pieces seem to be floating around, we need a way to connect the dots.

We'll see on this section how all of this pieces come together into designing an architecture, and we'll package everything nicely inside of a method.

## Design Strategy

We present three ideas that are key to architecture design methods: decomposition, designing to architecturally significant requirements, and generate and test.

### Decomposition

You're likely already familiar with decomposition, in the form of functional decomposition, when a certain functionality gets divided into a set of responsibilities and given to modules, submodules, or functions so that the functionality as a whole gets carried out successfully. While that kind of decomposition is valuable to the architect too, usually the architect is also concerned with a higher levels of decomposition.

To ensure the fulfillment of quality attributes, the system gets decomposed into a set of elements, and each element or set of elements, gets assigned the responsibility of fulfilling a quality attribute. This is a way to ensure that the system as a whole fulfill it's quality attribute requirements.

Also, besides module decomposition, there are other kinds of decompositions that come up frequently in the architecture as well, such as C&C decomposition, where one component may be decomposed into subcomponents.

You as the designer must keep in mind the constraints given to you and arrange the decomposition so that it will accommodate those constraints.

### Designing to Architecturally Significant Requirements

We've already went over on how to gather the ASRs, now **you must design to satisfy them**.

Should you design for one ASR at a time or multiple? This is usually a matter of experience. Similar to chess, when you're just getting started, you're learning and getting used to how each piece moves, and so you may focus only on you're next step. However, the best players are those that are able to see many moves ahead of a decision. Novice architects may design with only one ASR in mind at a time, but eventually with time and education, he or she should will develop a design intuition, and will be able to tackle multiple ASRs with the aid of patterns.

### Generate and Test

One way to view design is of "generate and test". That is your design is a hypothesis, and so you test it to see if it meets the requirements. If it does, good you're done! If it doesn't, you must learn from the failed hypothesis and come up with a new hypothesis. You keep iterating this until the design passes the test.

Observe that the coupling between the previous hypothesis and the new one is crucial. The new hypothesis must learn from the previous one and provide an improved designed, else you're just guessing and testing.

This strategy give rise to some questions:

- Where does the initial hypothesis comes from?
- What are the tests that are applied?
- How is the next hypothesis generated?
- When are you done?

#### Generating the Initial Hypothesis

Design solutions are generated using "collateral" that is available for the project. Collateral can include existing systems, frameworks, tactics/patterns, design checklists, or a domain decomposition.

- _Existing systems_: Very few systems are completely unprecedented. Existing systems provide the most powerful collateral, because business context and requirements for the existing system are likely to be similar to the new system, and many of the problems that occur have already been solved in the existing system. <br/>A common special case is when the existing system is the same you're designing for, that is, you're evolving the system. In which case it serves as the initial hypothesis, and the tests will show the parts of the system that fails to meet requirements.
- _Frameworks_: Frameworks are everywhere. Some of them are very opinionated, such as only allowing communication through publish-subscribe, or callbacks. The design of the framework provides the initial design hypothesis.
- _Patterns and Tactics_: As discussed previously, a pattern is a solution to a known problem in a given context, and so a pattern, possibly augmented with one or more tactics, can be a good candidate to the first design hypothesis.
- _Domain Decomposition_: Another option of the first design hypothesis comes from domain decomposition. This decomposition will divide the responsibilities to make certain modifications easier.
- _Design checklists_: The checklists given in the quality attributes section can serve as a base to a initial hypothesis.

#### Choosing Tests

Three sources provide tests to be applied to the hypothesis:

1. [The analysis techniques given in the QA section](./quality-atributes//model-and-analysis.md)
2. The checklists for each QA
3. The ASRs. If the hypothesis does not provide a solution for the ASRs, then it must be improved

#### Generating the Next Hypothesis

After applying the tests, you might be done -- everything looks good. However, if that's not the case, you can look for tactics to generate a new hypothesis based on what you learned so far. Remember to weight the tradeoffs of each tactic, and try to see ahead as much as possible.

#### Terminating the Process

You're done with the generate-and-test when you're either have a design that satisfies the ASRs or you have exhausted the budget for producing the design.

If you do not produce such a design within budget, you have two options. Your first option is to proceed to implementation with the best hypothesis you came up with, with the realization that some ASRs may not be met, and may need to be relaxed or eliminated. Your second option is to argue for more budget. If all else fails, you could suggest that the project terminate, there's no point in continuing with a project that's doomed to not fulfill it's critical requirements.

## The Attribute Driven Design (ADD) Method

The Attribute Driven Design method is a package of the design strategies defined above. It's an iterative method in which at each step you:

- Choose a part of the system to design
- Identify it's ASRs
- Generate and test the design for that part

The output of ADD is not not an architecture complete in every detail, but an architecture where the main design approaches have been selected and vetted. It produces a "workable" architecture early and quickly, one that allows work to be assigned to teams for implementation while the architect or architects continue to refine it.

### Inputs to ADD

Before beginning the process, the requirements - architectural, functional, and constraints - should be known. Realistically, the architect can't wait for all requirements to be known beforehand, this is virtually impossible because a lot of requirements are generated after initial deployment.

With that in mind, the architect must start working with a set of requirements. You probably can see the importance of having the correct set of requirements. If the set of requirements change after the design has begun, it may very well need to be reworked.

Aside from ASRs, your input to ADD should include:

- _What are the boundaries of the system being designed?_ What's inside and what's outside the system must be known to constrain the problem and establish the scope of the architecture you're designing.
- _What are the external systems, users, devices, and environment conditions with which the system must interact with?_ By environment condition we're referring to the runtime environment, this is comprised of where inputs come from, where do outputs go, which form they take, what quality attributes they have, and what are the forces that influence the system. An example of this could be systems that are sent to space, which have to operate under gamma radiation

### Output of ADD

The output of ADD is a set of sketches and architectural views. The views together will identify a set of architectural elements and their relationships or interactions. One of the views produced will be the modular decomposition view, which will include a set of elements that have their responsibilities enumerated.

The other views will be produced according to the design solutions chosen along the way.

The interaction of the elements are described in terms of the information passing between them. This could be a protocol, async or sync, level of encryption, and so forth.

We say that ADD generates sketches because it doesn't go as far as defining public interfaces and the names of their methods and parameters. This can be decided later on. ADD does identify the information passing through the interfaces and important characteristics of it.

When the method comes to an end, you'll have a full-fledged architecture that is roughly documented as a set of views. You can then polish this collection, merging views where necessary. In an Agile project, this set of views might be all you need for a while, or for the full life of the project.

### Steps of ADD

ADD is a five-step method:

1. Choose an element of the system to design
2. Identify the ASRs of that element
3. Generate the design for that element
4. Inventory remaining requirements and select input for the next iteration
5. Repeat steps 1-4 until all ASRs have been satisfied

#### Step 1: Choose an Element of the System to Design

On a "green-field" design, in the first step this will be the entire system. The result of this first iteration will be a collection of elements, you'll then choose one of these elements for the next iteration. After that you'll have even more fine-grained elements born from the element you chose, and now you can choose one of these new generated elements to the next step, or one of the elements generated on the first iteration, and so on.

This leads to the question: should I go breadth-first or depth-first? That is, should I choose an element, and then design it all the way to the end, or should I design the architecture in a more balanced fashion, focusing on high level elements equally. Here are some factors that play a role in that decision:

- _Availability of specialized teams/personnel_: It may be the case that you have available on the beginning of the design specialized personnel that can contribute to the design of a part of the system, or an implementation team that will only be available early on, in which case you'll want to go depth-first in that part of the system. On the same note, you may have access to this kind of help later on, and so you can defer the design of that part of the system to that point in time.
- _Risk Mitigation_: Another important aspect to consider is mitigating the risk of the system by going depth-first in the most challenging or risky parts, this can help finding problems, obstacles or blockers early on.
- _Deferral of some functionality or quality attribute may dictate a mixed approach_: As an example, if a set of elements have availability as a medium requirement, you can choose to use redundancy, but not specify further details, deferring this to later on.

All else being equal, the breadth-first approach is better because it allows work to be divided between teams sooner, and it also allows to consider communication between same-level elements.

#### Step 2: Identify the ASRs for this Element

If the element is the whole system, then the [utility tree](./requirements.md#capturing-asrs-in-a-utility-tree) of the system should do it. Otherwise, you'll want to build a utility tree for the specific element you're currently designing. Those that are labeled (H, H) (High, High) are the ASRs for this element, be mindful, however of (H, M) or (M, H) ASRs.

#### Step 3: Generate a Design Solution for the Chosen Element

This is the heart of the ADD method. It's the application of the generate and test strategy.

For each ASR we develop a solution by choosing a candidate design approach. Your initial candidate design solution will likely be inspired by a pattern and tactics, and can further be refined by checklists. By using that as sources, you'll likely tackle many of the elements ASRs at once.

The design decisions made on this step now become constraints on all future steps of the method.

#### Step 4: Verify and Refine Requirements and Generate Input for the Next Iteration

In this step you'll test the design generated for the current chosen element. As stated before, this can be done by analysis, checklists or seeing if the ASRs for this element were satisfied.

One of the possible outcomes of step 4 is "backtrack", this happens when an important requirement hasn't been satisfied and can't be satisfied with further design, and so you must go back and reconsider.

The ASRs you have not yet satisfied can be related to the following:

1. A quality attribute requirement allocated to the parent element
2. A functional responsibility of the parent element
3. One or more constraints imposed to the parent element

Here are some recommended actions for each:

| Type of ASR Not Met              | Action Recommended                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Quality attribute requirement | Consider applying (more) tactics to improve the design with respect to the quality attribute. For each candidate tactic, ask: <ul><li> Will this tactic improve the quality attribute behavior of the current design sufficiently? </li> <li> Should this tactic be used in conjunction with another tactic? </li> <li> What are the tradeoff considerations when applying this tactic?</li> </ul>                                                                                  |
| 2. Functional responsibility     | Add responsibilities either to existing modules or to newly created modules: <ul> <li> Assign the responsibility to a module containing similar responsibilities. </li> <li> Break a module into portions when it is too complex. </li> <li> Assign the responsibility to a module containing responsibilities with similar quality attribute characteristics—for example, similar timing behavior, similar security requirements, or similar availability requirements.</li> </ul> |
| 3. Constraint                    | Modify the design or try to relax the constraint: <ul> <li> Modify the design to accommodate the</li> constraint. <li> Relax the constraint.</li> </ul>                                                                                                                                                                                                                                                                                                                             |

Step 4 is about taking stock and seeing what requirements are left that haven't been satisfied yet by the design. At this point you should sequence through the quality attribute requirements, responsibilities, and constraints of the element just designed. For each, there are four possibilities:

- _The quality attribute requirement, functional requirement, or constraint has been satisfied._ In that case, the requirement with respect to that requirement is complete; the next time around, when you further refine the design, that requirement won't be considered
- _The quality attribute requirement, functional requirement, or constraint is delegated to one of the children._
- _The quality attribute requirement, functional requirement, or constraint is distributed among its children._
- _The quality attribute requirement, functional requirement, or constraint can be satisfied with the current design._ In which case you'll need to backtrack or push back on the requirement. Just have in mind that if you push back, you must have good arguments.

#### Step 5: Repeat Steps 1-4 Until Done

After the prior steps, each element has it's set of quality attribute requirement, functional requirements, and constraints. If it's clear that all requirements have been satisfied, then the ADD is over.

In a project with a high degree of confidence between the architecture team and the implementation team, a of sketches of the architecture will suffice. However, if that's not the case, then further refinements and specifications must be needed to represent the architecture, the level of detail on this may be specified by contracts.

Another way of terminating the design is when the budget has been exhausted, we already covered this scenario above.

Choosing when to terminate ADD and when to start releasing the architecture that you've sketched are not the same decision. You can, and in many cases should, release architecture sketches early on so that they can be socialized with other teams, and even start implementation early on. In this cases, you should release the documentation with the caveat of how likely it is to change.

## Bonus: What Makes a "Good" Architecture?
