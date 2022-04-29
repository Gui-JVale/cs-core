---
sidebar_position: 7
---

# Implementation & Testing

## Introduction

Architecture is not a goal unto itself, but only the means to an end. Building systems from the architecture is the end game, systems that have the qualities necessary to meet the concerns of their stakeholders. From the point of view of the architecture, there are two critical areas in system-building: implementation and testing.

## Implementation

Architecture is intended to serve as a blueprint for implementation. However, it's very easy for code and it's intended architecture to drift apart; this is sometimes called "architecture erosion". We'll go through four techniques to help keep the code and architecture consistent.

### Embedding the Design in the Code

A key task for implementers is to faithfully execute the prescriptions of the architecture. Throughout the code, implementers can document the architectural concept or guidance that they're reifying.

**Making the architecture explicit in the codebase helps keeping things consistent.**

### Frameworks

Frameworks are a reusable set of libraries or classes, and they have broad architectural implications - **they are the place where architecture and implementation meet**. And so frameworks can assist a lot into keeping the codebase consistent with the architecture.

However, it's also very important to understand it's tradeoffs. While usually frameworks can bring a lot of reusable and robust code to the table, they can have a steep learning curve, and be very opinionated, having lots of constraints.

### Code Templates

A template provides a structure within which some architecture-specific functionality is achieved, in a consistent fashion system-wide. Many code generators, such as user interface builders, produce a template into which a developer inserts code.

Using a template has architectural implications: it makes it simple to add new applications to the system with a minimum of concern for the actual workings of teh fault-tolerant mechanisms design into the approach. Coders and maintainers of applications do not need to know about message-handling mechanisms except abstractly, and they do not need to ensure that their applications are fault tolerant -- that has been handled architecturally.

Code templates have implications for reliability: once the template is debugged, then entire classes of coding errors across the entire system disappear. Templates represent a true common ground where the architecture and the implementation come together in a consistent and useful fashion.

### Keeping Code and Architecture Consistent

Code can drift away from architecture in a depressingly large number of ways. First, there may be no constraints imposed on the coders to follow the architecture. Second, some projects use the published architecture to start out, but when problems are encountered, the architecture is abandoned and coders scramble to field the system as best they can. Third, after the system has been fielded, changes to it are accomplished with code changes only, but theses changes affect the architecture. However, the published architecture is not updated to guide the changes, nor updated afterward to keep up with them.

Parts of the architecture may become out of date, but it will help enormously if those parts are marked as "no longer applicable" or "to be revised". In addition, strong management and process discipline will help prevent erosion. The alternatives for achieving code alignment with the architecture include the following:

- _Sync at life-cycle milestone_: Developers change the code until the end of some phase, such as a release or end of an iteration. At that point, when the schedule pressure is less, the architecture is updated.
- _Sync at crisis_: This undesirable approach happens when a projects has found itself in a technical quagmire and needs architectural guidance to get itself going again.
- _Sync at check-in_: Rules for this architecture are codified and used to vet any check-in. When a change to the code "breaks" the architecture rules, key project stakeholders are informed and then either the code or the architecture rules must be modified. This process is typically automated by tools.

These alternatives can work only if the implementation follows the architecture mostly, departing from it only here and there and in small ways.

## Testing

### Levels of Testing and the Role of the Architecture

There are "levels" of testing, which range from testing small, individual pieces in isolation to an entire system.

- _Unit testing_ refers to tests run on specific pieces of software. Unit testing is usually a part of the job of implementing those pieces. When the tests are written before developing the unit, this practice is known as test-driven development. Unit tests won't usually catch errors dealing with the interaction between elements, but unit tests provide confidence that each of the system's building block is exhibiting as much correctness as is possible on its own. A unit corresponds to an architectural element in one of the architecture's module views. <br/> Architecture plays a strong role in unit testing. First, it defines the units: they are architectural elements in one or more of the module views. Second, it defines the responsibilities and requirements assigned to each unit.
- _Integration testing_ tests what happens when separate software units start wto work together. Integration testing concentrates on finding problems related to the interfaces between elements in a design. Integration testing is intimately connected to the specific increments of subsets that are planned in a system' development.<br/> The case where only one increment is planned, meaning that integration of the entire system will occur in a single step, is called "big band integration" and has largely been discredited in favor of integrating many incrementally larger subsets. Incremental integration makes locating errors much easier, because any new error that shows up in an integrated subset is likely to live in whatever new parts were added this time around.<br/> At the end of integration testing, the project has confidence that the pieces of software work together correctly and provide at least some correct system-wide functionality.<br/>Once again, architecture cannot help but play a strong role in integration testing. First, the increments that will be subject to integration testing must be planned, and this plan will be based on the architecture. The uses view is particularly helpful for this, as it shows what elements must be present for a particular piece of functionality to be fielded. Second, the interfaces between elements are part of th architecture, and those interfaces determine the integration tests that are created and run. Integration testing is where runtime quality attribute requirements can be tested. Performance and reliability testing can be accomplished. Integration testing is also the time to test what happens when the system runs for an extended period.
- _Acceptance testing_ is a kind of system testing that is performed by users, often in the setting in which the system will run. Two special cases of acceptance testing are alpha and beta testing. In both of these, users are given free rein to use the system however they like, as opposed to testing that occurs under a preplanned regimen of a specific suite of test. Alpha testing usually occurs in-house, whereas beta testing makes the system available to a select set of end users under a "user beware" proviso. <br/> Architecture plays less of a role in acceptance testing than at the other levels, but still an important one. Acceptance testing involves stressing the system's quality attribute behavior by running it at extremely heavy loads, subjecting it to security attacks, depriving it of resources at critical times, and so forth.

Overlaying all of these types of testing is regression testing, which is testing that occurs after a change has been made to the system.

### Black-Box and White-Box Testing

Testing (at any level) can be "black box" or "white box". Black-box testing treats the software as an opaque "black box", not using any knowledge about the internal design, structure, or implementations. The tester's only source of information about the software is its requirements.

Architecture plays a role in black-box testing, because it is often the architecture document where the requirements for a piece of the system are described.

White-box testing makes full use of the internal structures, algorithms, and control and data flows of a unit of software. Tests that exercie all control paths of a unit of software are a primary example of white-box testing. White-box testing is most often associated with unit testing, but it has a role at higher levels as well,. In integration testing, for example, white-box testing can be used to construct tests that attempt to overload the connection between two components by exploiting knowledge about how a component (for example) manages multiple simultaneous interactions.

There are advantages and disadvantages with each kind of testing. Black-box testing is not biased by a design or implementation, and it concentrates on running many unit tests that a simple code inspection would reveal to be unnecessary. White-box testing often keys in on critical errors more quickly, but it can suffer from a loss of perspective by concentrating tests to make the implementation break, but not concentrating on the software delivering full functionality under all points in its input space.

### Risk-based Testing

Risk-based testing concentrates effort on areas where risk is perceived to be the highest. Architects can identify areas where architectural decisions (if wrong) would have a widespread impact, where architecture requirements are uncertain, quality attributes are demanding on the architecture, technology selections risky, or third-party software sources unreliable.

### Test Activities

Testing, depending on the project, can consume from 30 to 90 percent of a development's schedule and budget. Any activity that gobbles resources as voraciously as that doesn't just happen, of course, but needs to be planned and carried out purposefully and as efficiently as possible. Here are some of teh activities associated with testing:

- _Test planning._ Test activities have to be planned so that appropriate resources can be allocated.
- _Test development._ This is an activity in which the test procedures are written, test cases are chosen, test datasets are created, and test suites are scripted. The tests can be developed either before or after development.
- _Test execution._ Here, testers apply the tests to the software anc capture and record errors.
- _Test reporting and defect analysis._ Testers report the results of specific tests to developers, and they report overall metrics about the test results to the project's technical management. The analysis might include a judgement about wehther the software is ready for release.
- _Test harness creation._ One of the architect's common responsibilities is to create, along with the architecture, a set of test harnesses through which elements of the architecture may be conveniently tested. Such test harnesses typically permit setting up the environment for the elements to be tested, along with controlling their state and the data flowing into and out of the elements.

Once again, architecture plays a role and informs each of these activities, the architect can contributes useful information and suggestions for each. For test planning, the architecture provides the list of software units and incremental subsets. The architect can also provide insight as to the complexity or, if the software does not yet exist, the expected complexity of each of the software units. The architect can also suggest useful test technologies that will be compatible with the architecture. For test development, the architecture can make it easy to swap datasets in and out of the system.

### The Architect's Role

Here are some of the things an architect can do to facilitate quality testing. First, and foremost, the architect can design the system so that it is highly testable. The architect can also do these other things to help the test effort:

- Insure that testers have access to the source code, design documents, and the change records.
- Give testers the ability to control and reset the entire dataset that a program stores in a persistent database. Reverting the database to a known state is essential for reproducing bugs or running regression tests. One way to achieve this is to design a "persistence layer" so that whe whole program is database independent. In this way, the entire database can be swapped out for testing, even using an in-memory database if desired.
- Give testers the ability to instal multiple versions of a software product on a single machine. This helps testers compare versions, isolating when a bug was introduced.
