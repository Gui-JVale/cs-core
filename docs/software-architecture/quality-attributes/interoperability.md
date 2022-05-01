---
sidebar_position: 3
---

# Interoperability

## Principles

Interoperability is about the degree to which different systems can communicate with each other.

Two systems are interoperable if (1) they can exchange data, and (2) they can meaningfully interpret the exchanged data.

Interoperability is a very important attribute of computer networks, more famously the internet, where different end systems (with different operating systems), must exchange meaningful data.

Here are some reasons you might want systems to interoperate:

- Your system provides a service to be used by a collection of unknown systems.
- You are constructing capabilities from existing systems.

These examples highlight two important aspects of interoperability:

1. **Discovery**: The consumer of a service must discover the services location, identity, and its interface. This can happen either at runtime or beforehand.
2. **Handling of response**: There are three possibilities:
   1. The service reports back with a response
   2. The service sends its response on to another system
   3. The service broadcasts its response to any interested parties

## General Scenario

- _Source of stimulus_: A system initiates a request to interoperate with another system
- _Stimulus_: The request to exchange information among system(s)
- _Artifacts_: The systems that wish to interoperate
- _Environment_: The systems that wish to interoperate are discovered at runtime of are known prior to runtime.
- _Response_: The request to interoperate results in the exchange of information. The information is understood by the receiving party. Alternatively, the request is rejected and appropriate entities are notified
- _Response Measure_: The percentage of information exchanged correctly, or rejected.

| Portion of Scenario | Possible Values                                                                                                                                                                                                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source              | A system initiates a request to interoperate with another system.                                                                                                                                                                                                                                                       |
| Stimulus            | A request to exchange information among system(s).                                                                                                                                                                                                                                                                      |
| Artifact            | The systems that wish to interoperate.                                                                                                                                                                                                                                                                                  |
| Environment         | System(s) wishing to interoperate are discovered at runtime or known prior to runtime.                                                                                                                                                                                                                                  |
| Response            | One or more of the following: <ul><li> The request is (appropriately) rejected and appropriate entities (people or systems) are notified. </li><li> The request is (appropriately) accepted and information is exchanged successfully.</li><li> The request is logged by one or more of the involved systems.</li></ul> |
| Response Measure    | One or more of the following:<ul><li> Percentage of information exchanges correctly processed</li><li> Percentage of information exchanges correctly rejected</li></ul>                                                                                                                                                 |

## Tactics

We identify two categories of interoperability tactics: locate and manage interfaces.

### Locate

There is only one tactic in this category: discover service. It is used when the
systems that interoperate must be discovered at runtime.

- **Discover service**. Locate a service through searching a known directory service. (By “service,” we simply mean a set of capabilities that is accessible via some kind of interface.) There may be multiple levels of indirection in this location process—that is, a known location points to another location that in turn can be searched for the service. The service can be located by type of service, by name, by location, or by some other attribute.

### Manage Interfaces

Managing interfaces consists of two tactics: orchestrate and tailor interface.

- **Orchestrate**. Orchestrate is a tactic that uses a control mechanism to coordinate and manage and sequence the invocation of particular services (which could be ignorant of each other). Orchestration is used when the interoperating systems must interact in a complex fashion to accomplish a complex task; orchestration “scripts” the interaction. Workflow engines are an example of the use of the orchestrate tactic. The mediator design pattern can serve this function for simple orchestration. Complex orchestration can be specified in a language such as BPEL.
- **Tailor interface**. Tailor interface is a tactic that adds or removes capabilities to an interface. Capabilities such as translation, adding buffering, or smoothing data can be added. Capabilities may be removed as well. An example of removing capabilities is to hide particular functions from untrusted users. The decorator pattern is an example of the tailor interface tactic.

## Checklist

| Category                             | Checklist                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Allocation of Responsibilities       | Determine which of your system responsibilities will need to interoperate with other systems. Ensure that responsibilities have been allocated to detect a request to interoperate with known or unknown external systems. Ensure that responsibilities have been allocated to carry out the following tasks:<ul><li>Accept the request </li><li>Exchange information </li><li>Reject the request </li><li>Notify appropriate entities (people or systems) </li><li>Log the request (for interoperability in an untrusted environment, logging fornonrepudiation is essential)</li></ul>                                                                              |
| Coordination Model                   | Ensure that the coordination mechanisms can meet the critical quality attribute requirements. Considerations for performance include the following:<ul><li> Volume of traffic on the network both created by the systems under your control and generated by systems not under your control </li><li> Timeliness of the messages being sent by your systems </li><li> Currency of the messages being sent by your systems </li><li> Jitter of the messages’ arrival times </li><li> Ensure that all of the systems under your control make assumptions about protocols and underlying networks that are consistent with the systems not under your control.</li></ul> |
| Data Model                           | Determine the syntax and semantics of the major data abstractions that may be exchanged among interoperating systems. Ensure that these major data abstractions are consistent with data from the interoperating systems. (If your system’s data model is confidential and must not be made public, you may have to apply transformations to and from the data abstractions of systems with which yours interoperates.)                                                                                                                                                                                                                                               |
| Mapping among Architectural Elements | For interoperability, the critical mapping is that of components to processors. Beyond the necessity of making sure that components that communicate externally are hosted on processors that can reach the network, the primary considerations deal with meeting the security, availability, and performance requirements for the communication. These will be dealt with in their respective chapters.                                                                                                                                                                                                                                                              |
| Resource Management                  | Ensure that interoperation with another system (accepting a request and/or rejecting a request) can never exhaust critical system resources (e.g., can a flood of such requests cause service to be denied to legitimate users?). Ensure that the resource load imposed by the communication requirements of interoperation is acceptable. Ensure that if interoperation requires that resources be shared among the participating systems, an adequate arbitration policy is in place.                                                                                                                                                                               |
| Binding Time                         | Determine the systems that may interoperate, and when they become known to each other. For each system over which you have control: <ul><li> Ensure that it has a policy for dealing with binding to both known and unknown external systems. </li><li> Ensure that it has mechanisms in place to reject unacceptable bindings and to log such requests. </li><li> In the case of late binding, ensure that mechanisms will support the discovery of relevant new services or protocols, or the sending of information using chosen protocols.</li></ul>                                                                                                              |
| Choice of Technology                 | For any of your chosen technologies, are they “visible” at the interface boundary of a system? If so, what interoperability effects do they have? Do they support, undercut, or have no effect on the interoperability scenarios that apply to your system? Ensure the effects they have are acceptable. Consider technologies that are designed to support interoperability, such as web services. Can they be used to satisfy the interop                                                                                                                                                                                                                           |
