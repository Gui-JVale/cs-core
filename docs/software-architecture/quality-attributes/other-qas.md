---
sidebar_position: 9
---

# Other Quality Attributes

## Other Important Quality Attributes

### Variability

Variability is a special form of modifiability. It refers to the ability of a system and its supporting artifacts such as requirements, test plans, and configuration specifications to support the production of a set of variants that differ from each other in a preplanned fashion. Variability is an especially important quality attribute in a software product line (this will be explored in depth in Chapter 25), where it means the ability of a core asset to adapt to usages in the different product contexts that are within the product line scope. The goal of variability in a software product line is to make it easy to build and maintain products in the product line over a period of time. Scenarios for variability will deal with the binding time of the variation and the people time to achieve it.

### Portability

Portability is also a special form of modifiability. Portability refers to the ease with which software that was built to run on one platform can be changed to run on a different platform. Portability is achieved by minimizing platform dependencies in the software, isolating dependencies to well-identified locations, and writing the software to run on a “virtual machine” (such as a Java Virtua Machine) that encapsulates all the platform dependencies within. Scenarios describing portability deal with moving oftware to a new platform by expending no more than a certain level of effort or by counting the number of places in the software that would have to change.

### Development Distributability

Development distributability is the quality of designing the software to support distributed software development. Many systems these days are developed using globally distributed teams. One problem that must be overcome when developing with distributed teams is coordinating their activities. The system should be designed so that coordination among teams is minimized. This minimal coordination needs to be achieved both for the code and for the data model. Teams working on modules that communicate with each other may need to negotiate the interfaces of those modules. When a module is used by many other modules, each developed by a different team, communication and negotiation become more complex and burdensome. Similar considerations apply for the data model. Scenarios for development distributability will deal with the compatibility of the communication structures and data model of the system being developed and the coordination mechanisms of the organizations doing the development.

### Scalability

Two kinds of scalability are horizontal scalability and vertical scalability. Horizontal scalability (scaling out) refers to adding more resources to logical units, such as adding another server to a cluster of servers. Vertical scalability (scaling up) refers to adding more resources to a physical unit, such as adding more memory to a single computer. The problem that arises with either type of scaling is how to effectively utilize the additional resources. Being effective means that the additional resources result in a measurable improvement of some system quality, did not require undue effort to add, and did not disrupt operations. In cloud environments, horizontal scalability is called elasticity. Elasticity is a property that enables a customer to add or remove virtual machines from the resource pool . These virtual machines are hosted on a large collection of upwards of 10,000 physical machines that are managed by the cloud provider. Scalability scenarios will deal with the impact of adding or removing resources, and the measures will reflect associated availability and the load assigned to existing and new resources.

### Deployability

Deployability is concerned with how an executable arrives at a host platform and how it is subsequently invoked. Some of the issues involved in deploying software are: How does it arrive at its host (push, where updates are sent to users unbidden, or pull, where users must explicitly request updates)? How is it integrated into an existing system? Can this be done while the existing system is executing? Mobile systems have their own problems in terms of how they are updated, because of concerns about bandwidth. Deployment scenarios will deal with the type of update (push or pull), the form of the update (medium, such as DVD or Internet download, and packaging, such as executable, app, or plug-in), the resulting integration into an existing system, the efficiency of executing the process, and the associated risk.

### Mobility

Mobility deals with the problems of movement and affordances of a platform (e.g., size, type of display, type of input devices, availability and volume of bandwidth, and battery life). Issues in mobility include battery management, reconnecting after a period of disconnection, and the number of different user interfaces necessary to support multiple platforms. Scenarios will deal with specifying the desired effects of mobility or the various affordances. Scenarios may also deal with variability, where the same software is deployed on multiple (perhaps radically different) platforms.

### Monitorability

Monitorability deals with the ability of the operations staff to monitor the system while it is executing. Items such as queue lengths, average transaction processing time, and the health of various components should be visible to the operations staff so that they can take corrective action in case of potential problems. Scenarios will deal with a potential problem and its visibility to the operator, and potential corrective action.

### Safety

In 2009 an employee of the Shushenskaya hydroelectric power station in Siberia sent commands over a network to remotely, and accidentally, activate an unused turbine. The offline turbine created a “water hammer” that flooded and then destroyed the plant and killed dozens of workers.

The thought that software could kill people used to belong in the realm of kitschy computers-run-amok science fiction. Sadly, it didn’t stay there. As software has come to control more and more of the devices in our lives, software safety has become a critical concern. Safety is not purely a software concern, but a concern for any system that can affect its environment. As such it receives mention in Section 12.3, where we discuss system quality attributes. But there are means to address safety that are wholly in the software realm, which is why we discuss it here as well. Software safety is about the software’s ability to avoid entering states that cause or lead to damage, injury, or loss of life to actors in the software’s environment, and to recover and limit the damage when it does enter into bad states.

Another way to put this is that safety is concerned with the prevention of and recovery from hazardous failures. Because of this, the architectural concerns with safety are almost identical to those for availability, which is also about avoiding and recovering from failures. Tactics for safety, then, overlap with those for availability to a large degree. Both comprise tactics to prevent failures and to detect and recover from failures that do occur. Safety is not the same as reliability. A system can be reliable (consistent with its specification) but still unsafe (for example, when the specification ignores conditions leading to unsafe action). In fact, paying careful attention to the specification for safety-critical software is perhaps the most powerful thing you can do to produce safe software. Failures and hazards cannot be detected, prevented, or ameliorated if the software has not been designed with them in mind. Safety is frequently engineered by performing failure mode and effects analysis, hazard analysis, and fault tree analysis. These techniques are intended to discover possible hazards that could result from the system’s operation and provide plans to cope with these hazards.

## Understanding a new Quality Attribute

We've covered the quality attributes that usually are most important for software systems, however, you may still face a quality attribute requirement that wasn't listed previously, or that you may not know much about, what then? Well it's an important skill to be able to distinguish and understand a new quality attribute that you haven't particularly encountered before. So let's take a look on how to do that.

### Capture scenarios 

The first step is to talk with stakeholders to understand scenarios for the quality attribute. Also you can build a list of characteristics of the attribute, such as performance has confidentiality, integrity, and availability. Once you understand those, you can use then to abstract it into a general scenario, just as we have on the main QAs we went over previously.

### Assemble Design Approaches

After constructing a general scenario, you can start to think about design approaches to tackle the new quality attribute, for that, you can:

1. Look at patterns that you're familiar with, and think about how they would affect this quality attribute
2. Search for architectures or designs who've had to deal with this quality attribute
3. Ask experts in the area
4. Search the literature on the topic
5. Use the general scenario to try to catalog a list of responses in the response category
6. Use the general scenario to try to understand why some approaches may be problematic for the quality attribute

### Model the Quality Attribute

You can also model the quality attribute, and this could be as simple as understanding the parameters that the attribute is sensitive to. For example, modifiability is sensitive to coupling and cohesion.

### Assemble a Set of Tactics

With the model of the quality attribute, you can understand the parameters that affect it, and then use that to assemble tactics and patterns that tackle those parameters. Aside from the model, another source of tactics are experts.

To get tactics from the model you should:
1. Enumerate the parameters of the model
2. For each parameter, list the architectural design decisions that can affect this parameter

The result is a list of tactics to control the quality attribute we're concerned with. In the case that there's no model, you can do the following:

1. Ask experts
2. Examine systems that have the quality attribute
3. Examine the literature around the quality attribute
4. Examine documented architectural patterns to understand how they achieved the quality attributes responses touted for them

### Construct a Design Checklist 

Finally, you can construct a design checklist by asking yourself how the responses and tactics fit into the seven categories of decisions, and how you specialize your new quality of interest to these categories.
