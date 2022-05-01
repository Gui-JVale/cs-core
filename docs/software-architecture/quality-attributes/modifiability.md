---
sidebar_position: 4
---

# Modifiability

## Principles

Change happens.

Study shows again and again that most of the cost of development happens after initial deployment, that means that designing a modifiable system can lead to a lot of cost reduction. However, as each system is unique, the architect must weigh the cost of making a system modifiable vs having a not so modifiable system.

**Modifiability is can be summarized by the cost and risk involved in making a change in the system**.

To design for modifiability, an architect must know the following things about the system:

- _What can change?_: Basically any part of the system can change, from source code, to hardware, storage, and so on.
- _What's likely to change?_: An architect can't design a system where everything will change, it's just inviable. Instead, the architect must focus on the parts of the system that are more likely to change, and increase the modifiability there.
- _When is the change made and who makes it?_: Changes in a system can happen at any time, during development, compile-time, build time, or execution time. It's important to know when the change's made, and who makes it. A change can be made by a developer, a user, or a system administrator
- _What's the cost of making the change_: When it comes to making changes, there are generally two costs involved:
  - The cost of introducing the mechanism(s) to make the system more modifiable
  - The cost of making the modification using the mechanism(s)

## General Scenario

- _Source of stimulus_: Who makes the change.
- _Stimulus_: The change to be made.
- _Artifact_: The part of the system that is to be changed. This could be a module, or a runtime component.
- _Environment_: When the change is to be made
- _Response_: Make the change, test it , deploy it.
- _Response Measure_: Time and money to make the change.

| Portion of Scenario | Possible Values                                                                                                                                                                                                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source              | End user, developer, system administrator                                                                                                                                                                                                                                                                           |
| Stimulus            | A directive to add/delete/modify functionality, or change a quality attribute, capacity, or technology                                                                                                                                                                                                              |
| Artifacts           | Code, data, interfaces, components, resources, configurations, . . .                                                                                                                                                                                                                                                |
| Environment         | Runtime, compile time, build time, initiation time, design time                                                                                                                                                                                                                                                     |
| Response            | One or more of the following:<ul><li> Make modification </li><li> Test modification </li><li> Deploy modification</li></ul>                                                                                                                                                                                         |
| Response Measure    | Cost in terms of the following: <ul><li>Number, size, complexity of affected artifacts </li><li>Effort </li><li>Calendar time </li><li>Money (direct outlay or opportunity cost) </li><li>Extent to which this modification affects other functions or quality attributes</li> <li>New defects introduced</li></ul> |

## Tactics

Modifiability tactics have as their goal controlling the complexity of making changes, as well as reducing costs and time to make changes.

To understand modifiability, let's understand couping and cohesion.

Modules have responsibilities. When a change causes a module to be modified, it means it's responsibilities were change in some way. Generally, a change that affects only one module is easier and less expensive then one that may affect multiple modules. However, if two module responsibilities overlap in some way, changes on one module may require changes on another module. This is called coupling, and high coupling is an enemy of modifiability.

Cohesion measures how strongly the responsibilities of a module are relate. Informally, it measures the modules 'unity of purpose'. The higher the cohesion, the less likely that a given change will affect multiple responsibilities. High cohesion is good, low cohesion is bad.

Given this framework, we can now identify the parameters that we will use
to motivate modifiability tactics:

- _Size of a module_. Tactics that split modules will reduce the cost of making
  a modification to the module that is being split as long as the split is chosen
  to reflect the type of change that is likely to be made.
- _Coupling_. Reducing the strength of the coupling between two modules A
  and B will decrease the expected cost of any modification that affects A.
  Tactics that reduce coupling are those that place intermediaries of various
  sorts between modules A and B.
- _Cohesion_. If module A has a low cohesion, then cohesion can be improved
  by removing responsibilities unaffected by anticipated changes.

Finally we need to be concerned with when in the software development life cycle a change occurs. If we ignore the cost of preparing the architecture for the modification, we prefer that a change is bound as late as possible. Changes can only be successfully made (that is, quickly and at lowest cost) late in the life cycle if the architecture is suitably prepared to accommodate them. Thus the fourth and final parameter in a model of modifiability is this:

- _Binding time of modification_. An architecture that is suitably equipped to accommodate modifications late in the life cycle will, on average, cost less than an architecture that forces the same modification to be made earlier. The preparedness of the system means that some costs will be zero, or very low, for late life-cycle modifications. This, however, neglects the cost of preparing the architecture for the late binding.

Now we may understand tactics and their consequences as affecting one or more of the previous parameters: reducing the size of a module, increasing cohesion, reducing coupling, and deferring binding time.

### Reduce the Size of a Module

- Split module. If the module being modified includes a great deal of capability, the modification costs will likely be high. Refining the module into
  several smaller modules should reduce the average cost of future changes.

### Increase Cohesion

Several tactics involve moving responsibilities from one module to another. The
purpose of moving a responsibility from one module to another is to reduce the
likelihood of side effects affecting other responsibilities in the original module.

- **Increase semantic coherence**. If the responsibilities A and B in a module
  do not serve the same purpose, they should be placed in different modules.
  This may involve creating a new module or it may involve moving a responsibility to an existing module. One method for identifying responsibilities to be moved is to hypothesize likely changes that affect a module. If
  some responsibilities are not affected by these changes, then those responsibilities should probably be removed.

### Reduce Coupling

We now turn to tactics that reduce the coupling between modules.

- **Encapsulate**. Encapsulation introduces an explicit interface to a module.
  This interface includes an application programming interface (API) and its
  associated responsibilities, such as “perform a syntactic transformation on
  an input parameter to an internal representation.” Perhaps the most common
  modifiability tactic, encapsulation reduces the probability that a change to
  one module propagates to other modules. The strengths of coupling that
  previously went to the module now go to the interface for the module.
  These strengths are, however, reduced because the interface limits the ways
  in which external responsibilities can interact with the module (perhaps
  through a wrapper). The external responsibilities can now only directly interact with the module through the exposed interface (indirect interactions,
  however, such as dependence on quality of service, will likely remain unchanged). Interfaces designed to increase modifiability should be abstract
  with respect to the details of the module that are likely to change—that is,
  they should hide those details.
- **Use an intermediary** breaks a dependency. Given a dependency between responsibility A and responsibility B (for example, carrying out A first requires
  carrying out B), the dependency can be broken by using an intermediary.
  The type of intermediary depends on the type of dependency. For example,
  a publish-subscribe intermediary will remove the data producer’s knowledge of its consumers. So will a shared data repository, which separates readers of
  a piece of data from writers of that data. In a service-oriented architecture in
  which services discover each other by dynamic lookup, the directory service
  is an intermediary

- **Restrict dependencies** is a tactic that restricts the modules that a given module interacts with or depends on. In practice this tactic is achieved by restricting a module’s visibility (when developers cannot see an interface, they
  cannot employ it) and by authorization (restricting access to only authorized
  modules). This tactic is seen in layered architectures, in which a layer is only
  allowed to use lower layers (sometimes only the next lower layer) and in the
  use of wrappers, where external entities can only see (and hence depend on)
  the wrapper and not the internal functionality that it wraps.
- **Refactor** is a tactic undertaken when two modules are affected by the same
  change because they are (at least partial) duplicates of each other. Code refactoring is a mainstay practice of Agile development projects, as a cleanup
  step to make sure that teams have not produced duplicative or overly complex code; however, the concept applies to architectural elements as well.
  Common responsibilities (and the code that implements them) are “factored
  out” of the modules where they exist and assigned an appropriate home of
  their own. By co-locating common responsibilities—that is, making them
  submodules of the same parent module—the architect can reduce coupling.
- **Abstract common services**. In the case where two modules provide not-quite-the-same but similar services, it may be cost-effective to implement
  the services just once in a more general (abstract) form. Any modification
  to the (common) service would then need to occur just in one place, reducing modification costs. A common way to introduce an abstraction is by parameterizing the description (and implementation) of a module’s activities.
  The parameters can be as simple as values for key variables or as complex
  as statements in a specialized language that are subsequently interpreted.

### Defer Binding

Because the work of people is almost always more expensive than the work of computers, letting computers handle a change as much as possible will almost always reduce the cost of making that change. If we design artifacts with built-in flexibility, then exercising that flexibility is usually cheaper than hand-coding a specific change. Parameters are perhaps the best-known mechanism for introducing flexibility, and that is reminiscent of the abstract common services tactic. A parameterized function f(a, b) is more general than the similar function f(a) that assumes b = 0. When we bind the value of some parameters at a different phase in the life cycle than the one in which we defined the parameters, we are applying the defer binding tactic.

In general, the later in the life cycle we can bind values, the better. However,
putting the mechanisms in place to facilitate that late binding tends to be more
expensive—yet another tradeoff. And so the equation on page 118 comes into
play. We want to bind as late as possible, as long as the mechanism that allows it
is cost-effective.
Tactics to bind values at compile time or build time include these:

- Component replacement (for example, in a build script or makefile)
- Compile-time parameterization
- Aspects
  Tactics to bind values at deployment time include this:
- Configuration-time binding
  Tactics to bind values at startup or initialization time include this:
- Resource files
  Tactics to bind values at runtime include these:
- Runtime registration
- Dynamic lookup (e.g., for services)
- Interpret parameters
- Startup time binding
- Name servers
- Plug-ins
- Publish-subscribe
- Shared repositories
- Polymorphism

Separating building a mechanism for modifiability from using the mechanism to make a modification admits the possibility of different stakeholders being involved—one stakeholder (usually a developer) to provide the mechanism and another stakeholder (an installer, for example, or a user) to exercise it later, possibly in a completely different life-cycle phase. Installing a mechanism so that someone else can make a change to the system without having to change any code is sometimes called externalizing the change.

## Checklist

| Category                             | Checklist                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Allocation of Responsibilities       | Determine which changes or categories of changes are likely to occur through consideration of changes in technical, legal, social, business, and customer forces. For each potential change or category of changes: <ul><li> Determine the responsibilities that would need to be added, modified, or deleted to make the change. </li><li> Determine what responsibilities are impacted by the change. </li><li> Determine an allocation of responsibilities to modules that places, as much as possible, responsibilities that will be changed (or impacted by the change) together in the same module, and places responsibilities that will be changed at different times in separate modules.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Coordination Model                   | Determine which functionality or quality attribute can change at runtime and how this affects coordination; for example, will the information being communicated change at runtime, or will the communication protocol change at runtime? If so, ensure that such changes affect a small number set of modules. Determine which devices, protocols, and communication paths used for coordination are likely to change. For those devices, protocols, and communication paths, ensure that the impact of changes will be limited to a small set of modules. For those elements for which modifiability is a concern, use a coordination model that reduces coupling such as publish/subscribe, defers bindings such as enterprise service bus, or restricts dependencies such as broadcast.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Data Model                           | Determine which changes (or categories of changes) to the data abstractions, their operations, or their properties are likely to occur. Also determine which changes or categories of changes to these data abstractions will involve their creation, initialization, persistence, manipulation, translation, or destruction. For each change or category of change, determine if the changes will be made by an end user, a system administrator, or a developer. For those changes to be made by an end user or system administrator, ensure that the necessary attributes are visible to that user and that the user has the correct privileges to modify the data, its operations, or its properties. For each potential change or category of change: <ul><li> Determine which data abstractions would need to be added,modified, or deleted to make the change. </li><li> Determine whether there would be any changes to the creation, initialization, persistence, manipulation, translation, or destruction of these data abstractions. </li><li> Determine which other data abstractions are impacted by the change. For these additional data abstractions,determine whether the impact would be on the operations,their properties, their creation, initialization, persistence,manipulation, translation, or destruction. </li><li> Ensure an allocation of data abstractions that minimizes the number and severity of modifications to the abstractions by the potential changes.</li></ul>Design your data model so that items allocated to each element of the data model are likely to change together. |
| Mapping among Architectural Elements | Determine if it is desirable to change the way in which functionality is mapped to computational elements (e.g., processes, threads, processors) at runtime, compile time, design time, or build time. Determine the extent of modifications necessary to accommodate the addition, deletion, or modification of a function or a quality attribute. This might involve a determination of the following, for example:<ul><li> Execution dependencies </li><li> Assignment of data to databases </li><li> Assignment of runtime elements to processes, threads, or processors</li></ul>Ensure that such changes are performed with mechanisms that utilize deferred binding of mapping decisions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Resource Management                  | Determine how the addition, deletion, or modification of a responsibility or quality attribute will affect resource usage. This involves, for example:<ul><li> Determining what changes might introduce new resources or remove old ones or affect existing resource usage </li><li> Determining what resource limits will change and howEnsure that the resources after the modification are sufficient to meet the system requirements.</li></ul>Encapsulate all resource managers and ensure that the policies implemented by those resource managers are themselves encapsulated and bindings are deferred to the extent possible.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Binding Time                         | For each change or category of change:<ul><li> Determine the latest time at which the change will need to be made.</li><li> Choose a defer-binding mechanism (see Section 7.2) that delivers the appropriate capability at the time chosen. </li><li> Determine the cost of introducing the mechanism and the cost of making changes using the chosen mechanism. Use the equation on page 118 to assess your choice of mechanism. </li><li> Do not introduce so many binding choices that change is impeded because the dependencies among the choices are complex and unknown.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Choice of Technology                 | Determine what modifications are made easier or harder by your technology choices.<ul><li> Will your technology choices help to make, test, and deploy modifications?</li><li> How easy is it to modify your choice of technologies (in case some of these technologies change or become obsolete)? Choose your technologies to support the most likely modifications. For example, an enterprise service bus makes it easier to change how elements are connected but may introduce vendor lock-in.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
