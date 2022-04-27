---
sidebar_position: 6
---

# Writing Documentation

## Uses and Audiences for Architecture Documentation

Spending time and effort designing a well-thought architecture is of no use if that architecture isn't communicated properly, or if the important stakeholders of the system know nothing about it.

**A good architecture isn't enough, it has to be communicated in a way that lets stakeholders do their jobs.**

That's why documentation is so crucial for an architecture, it's the place where all important design decisions are recorded, it serves as a guide for implementation and work assignment, it serves to reason about the system and provides a base for quality attribute analysis, it serves as the base of communication among stakeholders.

However, it's also no good to document something that will provide no value. That's why you should only document the parts of the architecture that will bring value to one or more stakeholders, and you should write the documentation with that audience in mind.

## Notations for Architecture Documentation

There are three main categories of notations:

1. _Informal notations_: These can range from rough sketches, to more refined box and pointer diagrams.
2. _Semiformal notations_: These provide a standardized way to prescribe graphical elements and rules of construction, but is does not provide a complete semantic treatment of those elements. UML is a semiformal notation in that sense.
3. _Formal notations_: Views are described in a notation that has precise (usually mathematically based) semantics. Generally referred to architecture description languages (ADL). The benefit of using this is that it can lead to automation through code generation. In practice, the use of such notations is rare.

## Views

At the heart of the documentation, and perhaps the more important part of it, are views. **Views define elements and the relationships between them.**

A view can document a set of module elements, C&C elements, or allocation structures. It can also represent a mapping between these kinds of elements.

**Documenting an architecture is a matter of documenting the relevant views and then adding documentation that applies to more than one view.**

Different views expose different quality attributes to different degrees. The quality attributes that are of most concern to you and other stakeholders of the system will affect which views get documented.

Different views have different goals and purposes. Each view has a cost to maintain and a benefit, you should make sure that the benefit should out-weight the costs for the views that you choose to document.

### Module Views

A module is a static implementation unit that provides a coherent set of responsibilities.

Module structures often determine how changes to one part of a system might affect other parts, hence the ability of a system to support modifiability, portability, and reuse.

#### Summary of the module views

| Topic       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Elements    | Modules, which are implementation units of software that provide a coherent set of responsibilities.                                                                                                                                                                                                                                                                                                                                                                    |
| Relations   | <ul> <li> Is part of, which defines a part/whole relationship between the submodule—the part—and the aggregate module—the whole. </li> <li> Depends on, which defines a dependency relationship between two modules. Specific module views elaborate what dependency is meant.</li> <li> Is a, which defines a generalization/specialization relationship between a more specific module—the child—and a more general module—the parent.</li></ul>                      |
| Constraints | Different module views may impose specific topological constraints, such as limitations on the visibility between modules.                                                                                                                                                                                                                                                                                                                                              |
| Usage       | <ul> <li> Blueprint for construction of the code</li> <li> Change-impact analysis</li> <li> Planning incremental development</li> <li> Requirements traceability analysis</li> <li> Communicating the functionality of a system and the structure of its code base </li> <li> Supporting the definition of work assignments, implementation schedules, and budget information </li> <li> Showing the structure of information that the system needs to manage</li></ul> |

Properties that help guide implementation or are input to analysis should be recorded as part of the supporting documentation for a module. The list of properties may vary but is likely to include the following:

- _Name_: Modules name often suggest it's role in the system
- _Responsibilities_: This property is a way to identify it's role in the overall system and establishes an identity for it beyond it's name.
- _Visibility of interface(s)_: When a module has submodules, some interfaces of the submodules are public and some may be private.
- _Implementation Information_: This may include mapping to source code units (file system), testing information, management information (a manager may need information about the module's predicted schedule and budget), implementation constraints, and revision history

Because modules partition the system, it should be possible to determine how the functional requirements are supported by looking at the module responsibilities.

The various levels of granularity of the module decomposition can provide a top-down decomposition of the system and therefore guide the learning process.

On the other hand, it is difficult to make inferences about runtime behavior by looking at module views. Usually modules are mapped to C&C views.

### Component-and-Connector Views

C&C views document the behavior and relationships of elements that have a runtime presence.

Components have interfaces called _ports_. A port defines a point of potential interaction of a component with it's environment. A port usually has an explicit type, which defines which kind of behavior that can take place at that point of interaction. A component's ports should be explicitly documented, by showing them in the diagram and defining them in the diagram's supporting documentation.

Connectors have _roles_, which are its interfaces, defining the ways in which the connector may be used by components to carry out interaction.

The primary relation within a C&C view is _attachment_. Attachment indicates which connectors are attached to which components, thereby defining a system as a graph of component and connectors. Specifically, an attachment is denoted by associating (attaching) a component's port to a connector's role.

An element (component or connector) of a C&C view will have various associated properties. Every element should have a name and a type. Additional properties depend on the type of component or connector. The following are examples of some typical properties and their uses:

- Reliability. What is the likelihood of failure for a given component or connector? This property might be used to help determine overall system availability.
- Performance. What kinds of response time will the component provide under what loads? What kind of bandwidth, latency, jitter, transaction volume, or throughput can be expected for a given connector? This property can be used with others to determine system-wide properties such as response times, throughput, and buffering needs.
- Resource requirements. What are the processing and storage needs of a component or a connector? This property can be used to determine whether a proposed hardware configuration will be adequate.
- Functionality. What functions does an element perform? This property can be used to reason about overall computation performed by a system.
- Security. Does a component or a connector enforce or provide security features, such as encryption, audit trails, or authentication? This property can be used to determine system security vulnerabilities.
- Concurrency. Does this component execute as a separate process or thread? This property can help to analyze or simulate the performance of concurrent components and identify possible deadlocks.
- Modifiability. Does the messaging structure support a structure to cater for evolving data exchanges? Can the components be adapted to process those new messages? This property can be defined to extend the functionality of a component.
- Tier. For a tiered topology, what tier does the component reside in? This property helps to define the build and deployment procedures, as well as platform requirements for each tier.

C&C views are often used to show developers and stakeholders how the system works. They are also used to reason about runtime system quality attributes, such as performance and availability.

#### Summary of C&C Views

| Topic       | Elements                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Elements    | <ul> <li> Components. Principal processing units and data stores. A component has a set of ports through which it interacts with other components (via connectors).</li> <li> Connectors. Pathways of interaction between components. Connectors have a set of roles (interfaces) that indicate how components may use a connector in interactions.</li> </ul>                                                                                                                         |
| Relations   | <ul><li> Attachments. Component ports are associated with connector roles to yield a graph of components and connectors. </li> <li> Interface delegation. In some situations component ports are associated with one or more ports in an “internal” subarchitecture. The case is similar for the roles of a connector.</li></ul>                                                                                                                                                       |
| Constraints | <ul> <li> Components can only be attached to connectors, not directly to other components. </li> <li> Connectors can only be attached to components, not directly to other connectors. </li> <li> Attachments can only be made between compatible ports and roles.</li> <li> Interface delegation can only be defined between two compatible ports (or two compatible roles).</li> <li> Connectors cannot appear in isolation; a connector must be attached to a component.</li> </ul> |
| Usage       | <ul> <li> Show how the system works.</li> <li> Guide development by specifying structure and behavior of runtime elements. </li> <li> Help reason about runtime system quality attributes, such as performance and availability. </li> </ul>                                                                                                                                                                                                                                           |

#### Notations for C&C Views

As always, box-and-line drawings are always available to represent C&C views. Assign each component type and each connector type a separate visual form, and list each of the types in a key.

UML components are a good semantic to C&C components because they permit intuitive documentation of important information like interface properties, and behavioral descriptions.

While C&C connectors are as semantically rich as C&C components, the same is not true of UML connectors. UML connectors cannot have substructure, attributes, or behavioral descriptions. The best approximation is to label the connector ends and use these labels to identify role descriptions that must be documented elsewhere.

You should represent a "rich" C&C connector using a UML component, or by annotating a line UML connector with a tag or other auxiliary documentation that explains the meaning of the complex connector.

### Allocation Views

Allocation views describe the mapping of software units to elements of an environment in which the software is developed or in which it executes.

#### Summary of Allocation Views

| Topic       | Description                                                                                                                                                                                                                                                                                                                              |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Elements    | <ul> <li> Software element. A software element has properties that are required of the environment. </li> <li> Environmental element. An environmental element has properties that are provided to the software.</li> </ul>                                                                                                              |
| Relations   | Allocated to. A software element is mapped (allocated to) an environmental element. Properties are dependent on the particular view.                                                                                                                                                                                                     |
| Constraints | Varies by view                                                                                                                                                                                                                                                                                                                           |
| Usage       | <ul> <li> For reasoning about performance, availability, security, and safety. </li> <li> For reasoning about distributed development and allocation of work to teams. </li> <li> For reasoning about concurrent access to software versions. </li> <li> For reasoning about the form and mechanisms of system installation. </li> </ul> |

The relation in an allocation view is _allocated to_. Allocation views can depict static or dynamic views. A static view depicts a fixed allocation of resources in an environment. A dynamic view depicts the conditions and the triggers for which allocation of resources changes according to loading.

### Quality Views

Another kind of view, which we call _quality view_, can be tailored for specific stakeholders or to address specific concerns. These quality views are formed by extracting the relevant pieces of structural views and packaging them together.

## Choosing Views

Documenting decision during the design process produces views, which are the heart of an architecture document.

By the time you're ready to release an architecture document, you're likely to have a fairly well-worked-out collection of architecture views. AT some point you'll need to decide which to take to completion, with how much detail, and which to include in a given release.

You can determine which views are required, when to create them, and how much detail to include if you know the following:

- What people, and with what skills, are available
- Which standards you have to comply with
- What budget is on hand
- What the schedule is
- What the information needs of the important stakeholders are
- What the driving quality attribute requirements are
- What the size of the system is

At a minimum, expect to have at least one module view, at least one C&C view, and for larger projects, at least one allocation view in your architecture document. Beyond that basic rule of thumb, however, there is a three-step method for choosing the views:

1. **Build a stakeholder/view table**. Enumerate the stakeholders for your project's software architecture documentation won the rows. Be as comprehensive as you can. For the columns, enumerate the views that apply to your system. Once you have the rows and columns defined, fill in each cell to describe how much information the stakeholder requires from the view: none, overview only, moderate detail, or high detail.
2. **Combine Views**. The candidate view list from step 1 is likely to yield an impractically large number of views. This step will winnow the list to manageable size. Look for marginal views in the table: those that require only an overview, or that serve very few stakeholders. Combine each marginal view with another view that has a stronger constituency.
3. **Prioritize and stage**. After step 2 you should have the minimum set of views needed to serve your stakeholder community. At this point you need to decided what to do first. What do you do first depends on your project, but here are some things to consider.
   - The decomposition view is a particularly helpful view to release early.
   - Be aware that you don't have to satisfy all the information needs of all the stakeholders to the fullest extent. Providing 80 percent of the information goes as long way
   - You don't have to complete one view before starting the another. People can make progress with overview-level information, so a bread-first approach is often the best.

## Combining Views

Because all views in an architecture are part of that same architecture and exist to achieve a common purpose, many of them have strong associations with each other. Managing how architectural structures are associated is an important part of the architect’s job, independent of whether any documentation of those structures exists.

Sometimes the most convenient way to show a strong association between two views is to collapse them into a single _combined view_. Combined views can be very useful as long as you do not try to overload them with too many mappings.

The easiest way to merge views is to create an overlay that combines the information that would otherwise have been in two separate views. This works well if the coupling between the two views is tight.

The views below often combine naturally:

- Various C&C views. Because C&C views all show runtime relations among components and connectors of various types, they tend to combine well.
- Deployment view with either SOA or communicating-processes views.
- Decomposition view and any of work assignment, implementation, uses, or layered views. The decomposed modules form the units of work, development, and uses. In addition, these modules populate layers.

## Building the Documentation Package

### Documenting a View

The principle of architecture documentation is to document the relevant views, and to document the information that applies to more than one view.

Here's the template for a view:

![Template for a view](/img/docs/template-for-a-view.png)

No matter what the view, the documentation for a view can be placed into a
standard organization consisting of these parts:

- **Section 1: The Primary Presentation.** The primary presentation shows the elements and relations of the view. The primary presentation should contain the information you wish to convey about the system—in the vocabulary of that view. It should certainly include the primary elements and relations but under some circumstances might not include all of them. The primary presentation is most often graphical. If your primary presentation is graphical, make sure to include a key that explains the notation. Occasionally the primary presentation will be textual, such as a table or a list.
- **Section 2: The Element Catalog.** The element catalog details at least those elements depicted in the primary presentation. In addition, if elements or relations relevant to this view were omitted from the primary presentation, they should be introduced and explained in the catalog. Specific parts of the catalog include the following:

  - _Elements and their properties._ This section names each element in the view and lists the properties of that element.
  - _Elements and their properties._ This section names each element in the view and lists the properties of that element.
  - _Element interfaces._
  - _Element behavior._ This section documents element behavior that is not obvious from the primary presentation

- **Section 3: Context Diagram.** A context diagram shows how the system or portion of the system depicted in this view relates to its environment. The purpose of a **context diagram** is to depict the scope of a view. Here “context” means an environment with which the part of the system interacts. Entities in the environment may be humans, other computer systems, or physical objects, such as sensors or controlled devices.
- **Section 4: Variability Guide.** A variability guide shows how to exercise any variation points that are a part of the architecture shown in this view.
- **Section 5: Rationale.** Rationale explains why the design reflected in the view came to be. The goal of this section is to explain why the design is as it is and to provide a convincing argument that it is sound.

### Documenting Information Beyond Views

Documentation beyond views can be divided into two parts:

1. _Overview of the architecture documentation._ This tells how the documentation is laid out and organized so that a stakeholder of the architecture can find the information he or she needs efficiently and reliably.
2. _Information about the architecture._ Here, the information that remains to be captured beyond the views themselves is a short system overview to ground any reader as to the purpose of the system and the way the views are related to one another, an overview of and rationale behind system-wide design approaches, a list of elements and where they appear, and a glossary and an acronym list for the entire architecture.

Template for documenting beyond views:

![Template for documenting information beyond views](/img/docs/template-for-beyond-views.png)

Documentation beyond views consists of the following sections:

- **Document control information.** List the issuing organization, the current version number, date of issue and status, a change history, and the procedure for submitting change requests to the document. Usually this is captured in the front matter. Change control tools can provide much of this information.
- **Section 1: Documentation Roadmap.** The documentation roadmap tells the reader what information is in the documentation and where to find it. A documentation map consists of four sections:
  - _Scope and summary._ Explain the purpose of the document and briefly summarize what is covered and (if you think it will help) what is not covered. Explain the relation to other documents (such as downstream design documents or upstream system engineering documents).
  - _How the documentation is organized._
  - _View Overview._
  - _How the stakeholders can use the documentation._
- **Section 2: How a View Is Documented.** This is where you explain the standard organization you’re using to document views—either the one described in this chapter or one of your own. It tells your readers how to find information in a view.
- **Section 3: System Overview.** This is a short prose description of the system’s function, its users, and any important background or constraints.
- **Section 4: Mapping Between Views.** Because all the views of an architecture describe the same system, it stands to reason that any two views will have much in common. Helping a reader understand the associations between views will help that reader gain a powerful insight into how the architecture works as a unified conceptual whole.
- **Section 5: Rationale.** This section documents the architectural decisions that apply to more than one view.
- **Section 6: Directory.** The directory is a set of reference material that helps readers find more information quickly.

### Follow a Release Strategy

Your project’s development plan should specify the process for keeping the important documentation, including architecture documentation, current. The architect should plan to issue releases of the documentation to support major project milestones, which usually means far enough ahead of the milestone to give developers time to put the architecture to work.

### Documenting Patterns

Record the fact that the given pattern is being used. Then say why this solution approach was chosen—why it is a good fit to the problem at hand.

## Documenting Behavior

Documenting an architecture requires behavior documentation that complements structural views by describing how architecture elements interact with each other.

There are two kinds of notations available for documenting behavior. The first kind of notation is called trace-oriented languages; the second is called comprehensive languages.

Traces are sequences of activities or interactions that describe the system’s response to a specific stimulus when the system is in a specific state. Below we describe four notations for documenting traces: use cases, sequence diagrams, communication diagrams, and
activity diagrams.

- _Use cases_ describe how actors can use a system to accomplish their goals.
- A UML _sequence diagram_ shows a sequence of interactions among instances of elements pulled from the structural documentation. A sequence diagram has two dimensions: vertical, representing time, and horizontal, representing the various instances. The interactions are arranged in time sequence from top to bottom. Objects (i.e., element instances) have a lifeline, drawn as a vertical dashed line along the time axis. The sequence is usually started by an actor on the far left. The instances interact by sending messages, which are shown as horizontal arrows.
- A UML _communication diagram_ shows a graph of interacting elements and annotates each interaction with a number denoting order. Communication diagrams are useful when the task is to verify that an architecture can fulfill the functional requirements
- UML _activity diagrams_ are similar to flow charts. They show a business process as a sequence of steps (called actions) and include notation to express conditional branching and concurrency, as well as to show sending and receiving events. Arrows between actions indicate the flow of control.

In contrast to trace notations, comprehensive models show the complete behavior of structural elements. Given this type of documentation, it is possible to infer all possible paths from initial state to final state. The state machine diagrams help to model elements of the architecture and help to illustrate their runtime interactions.

## Documenting Quality Attributes

If architecture is largely about the achievement of quality attributes and if one of the main uses of architecture documentation is to serve as a basis for analysis , where do quality attributes show up in the documentation? Short of a full-fledged quality view, there are five major ways:

1. Any major design approach (such as an architecture pattern) will have quality attribute properties associated with it. Explaining the choice of approach is likely to include a discussion about the satisfaction of quality attribute requirements and tradeoffs incurred.
2. Individual architectural elements that provide a service often have quality attribute bounds assigned to them, sometimes in the form of a service-level agreement.
3. Quality attributes often impart a “language” of things that you would look for.
4. Architecture documentation often contains a mapping to requirements that shows how requirements (including quality attribute requirements) are satisfied.
5. Every quality attribute requirement will have a constituency of stakeholders who want to know that it is going to be satisfied. For these stakeholders, the architect should provide a special place in the documentation’s introduction that either provides what the stakeholder is looking for, or tells the stakeholder where in the document to find it.

## Documenting Architectures that Change Too Fast

In many cases systems can change very rapidly at runtime, like systems that utilize dynamic service discovery and binding, systems that are highly dynamic, self-organizing, and reflective. In these cases, the identities of the components interacting with each other cannot be pinned down, let alone their interactions, in any static architecture document.

But knowing the architecture of these systems is every bit as important, and arguably more so, than for systems in the world of more traditional life cycles. Here’s what you can do if you’re an architect in a highly dynamic environment:

- _Document what is true about all versions of your system._
- _Document the ways the architecture is allowed to change._

## Documenting Architectures in Agile

The Views and Beyond and Agile philosophies agree strongly on a central point: If information isn’t needed, don’t document it. All documentation should have an intended use and audience in mind, and be produced in a way that serves both.

When producing Views and Beyond-based architecture documentation using Agile principles, keep the following in mind:

- Adopt a template or standard organization to capture your design decisions.
- Plan to document a view if (but only if) it has a strongly identified stakeholder constituency.
- Fill in the sections of the template for a view, and for information beyond views, when (and in whatever order) the information becomes available.
- Don’t worry about creating an architectural design document and then a finer-grained design document. Produce just enough design information to allow you to move on to code.
- Don’t feel obliged to fill up all sections of the template, and certainly not all at once.
