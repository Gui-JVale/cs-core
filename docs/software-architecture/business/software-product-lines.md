---
sidebar_position: 3
---

# Software Product Lines

## Introduction

A software architecture represents a significant investment of time and effort usually by senior talent. So it is natural to want to maximize the return on this investment by reusing an architecture across multiple systems.

This section shows a way to reuse software architecture across a family or related systems, and the benefits that doing so can bring. Many software-producing organizations tend to produce systems or products that resemble each other more than they differ. This is an opportunity for reusing the architecture across these similar products. These software product lines simplify the creation of new members of a family of similar systems.

This kind of reuse has been shown to bring substantial benefits that include reduced cost of construction, higher quality, and greatly reduced time to market.

**The vision is of a set of reusable assets (called core assets) based on a common architecture and the software elements that populate that architecture**. The core assets also include designs and their documentation, user manuals, project management artifacts such as budgets and schedules, software test plans and test cases, and more.

**Core assets, including the architecture, are usually designed with built-in variation points -- places where they can be quickly tailored in preplanned ways.**

Once the core assets are in place, system building becomes a matter of

- Accessing the appropriate assets in the core asset base
- Exercising the variation points to configure them as required for the system being built
- Assembling that system

Creating a successful product line depends on a coordinated strategy involving software engineering, technical management, and organization management.

## What Makes a Software Product Line Work?

What makes product lines succeed is that the commonalities shared by the products can be exploited through reuse to achieve production economies. The potential for reuse is broad and far-ranging, including the following:

- Requirements
- Architectural Design
- Software Elements
- Modeling and analysis
- Testing
- Project planning artifacts

All of these represent valuable core assets, each of which can be imbued with its own variation points that can be exercised to build a product. Any artifact represented by text can consist of text blocks that are exposed or hidden for a particular product. Thus, the artifact that is maintained in the core asset base represents a superset of nay version that will be produced for a product. Artifacts reuse in turn enables reuse of knowledge:

- _Processes, methods, and tools_. Configuration control procedures and facilities, documentation plans and approval processes, tool environments, system generation and distribution procedures, coding standards, and many other day-to-day engineering support activities can all be carrie d over from product to product.
- _People_. Because of the commonality of applications, personnel can be transferred among projects as required. Their expertise is applicable across the entire line.
- _Exemplar systems._ Deployed products serve as high-quality demonstration prototypes or engineering models of performance, security, safety, and reliability.
- _Defect elimination._ Product lines enhance quality because each new system takes advantage of the defect elimination in its forebears.

All of this reuse helps products launch more quickly, with higher quality, lower cost, and more predictable budget and schedule.

## Product Line Scope

One of the most important inputs to an architect building an architecture for a software product line is the product line's scope. A product line's scope is a statement about what systems an organization is willing to build aas part of its line and what system it is not willing to build.

The scope represents the organization's best prediction about what products will be asked to build in the foreseeable future. Input to the scoping process comes from the organization's strategic planners, marketing staff, domain analysis who can catalog similar systems and technology experts.

A product line scope is a critical factor in the success of the product line. Scope to narrowly and an insufficient number of products will be derived to justify the investment in the development. Scope too broadly and the effort required to develop individual products from the core assets is too great to lead to significant savings.

The problem in defining the scope is not in finding commonality, but in finding commonality that can be exploited to substantially reduce the cost of construction the systems that an organization intends to build. when considering scope, more than just the system being build should be considered. Market implementation and types of customer interactions assumed will help determine the scope of any particular product line.

The scope definition is vital to the product line architect because the scope defines what is common across all members of the product line, and the specific ways in which the products differ from each other. the fixed part of a product line architecture reflects what is constant, and the architecture's variation points accommodate the variations among products.

## The Quality Attribute Variability

The quality attribute of variability is most closely associated with product lines. All product lines feature variability aimed at satisfying the commonalities and variations identified by the product line's scope.

Variability is a special form of modifiability, pertaining to the ability of a core asset to adapt to usages in the different product context that are within the product line scope. The goal of variability in a software product line is to make it easy to build and maintain products in the product line over time.

Product line architectures feature variability as an important quality attribute. They achieve this by incorporation of variation mechanisms, which we will discuss in more detail shortly.

The General Scenario for Variability:

| Portion of Scenario | Possible Values                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source              | Actor requesting variability                                                                                                                                                                                                                                                                                                                                                    |
| Stimulus            | Requests to support variations in the following:<ul><li> Hardware</li><li> Feature sets</li><li> Technologies</li><li> User interfaces</li><li> Quality attributes</li><li> . . . and more</li></ul>for the range of products affected, such as: \<ul> \<li> All</li> \<li> A specified subset</li> \<li> Those that include feature set x </li> \<li> New products</li> \</ul> |
| Environment         | Variants are to be created at:<ul><li> Runtime</li><li> Build time</li><li> Development time</li></ul>                                                                                                                                                                                                                                                                          |
| Artifact            | Asset(s) affected, such as:<ul><li> Requirements</li><li> Architecture</li><li> Component x</li><li> Test suite y</li><li> Project plan z </li><li> . . . and more</li></ul>                                                                                                                                                                                                    |
| Response            | The requested variants can be created.                                                                                                                                                                                                                                                                                                                                          |
| Response measure    | A specified cost and/or time to create the core assets and to create the variants using these core assets                                                                                                                                                                                                                                                                       |

## The Role of a Product Line Architecture

Of all the assets in a core asset repository, the software architecture plays the most central role. There is both a tactical and a strategic reason for this.

The tactical reason is the importance the architecture plays in building products in a product line. IN a software product line, the architecture has to encompass both the varying and the nonvarying aspects. A product line architecture must be designed to accommodate a set of explicitly allowed variations. Thus, identifying the allowable variations is part of the architect's responsibility, as is providing built-in mechanisms for achieving them.

A product line architect needs to consider three things that are unique to product line architectures:

- _Identifying variation points_. This is done by using the scope definition and product line requirements as input.
- _Supporting variation points_. This is done by introducing variation mechanisms.
- _Evaluation the architecture for product line suitability._

## Variation Mechanisms

In a conventional architecture, the mechanism for achieving different instances often comes down to modifying the code. But in a software product line, modifying code is undesirable, because this leads to a large number of separately maintained implementations that quickly outstrip an organization's ability to keep them up to date and consistent.

Three primary architectural variation mechanisms are these:

- _Inclusion or omission of elements._ This decision can be reflected in the build procedures for different products, or the implementation of an element can be conditionally compiled based on some parameters indicating its presence or absence.
- _Inclusion of a different number of replicated elements._ For instance, high-capacity variants might be produced by adding more servers.
- _Selection of different versions of elements that have the same interface but different behavioral or quality attribute characteristics._ Selection can occur at compile time, build time, or runtime.

Some variation mechanisms can be introduced that chage the aspects of a particulare software elements. techniques include the following:

- _Extension points._ These are identified places in the architecture where additional behavior or functionality can be added safely.
- _Reflection._ This is the ability of a program to manipulate data on itself or its execution environment or state. Reflective programs can adjust their behavior based on their context.
- _Overloading._ This is a means of reusing a named functionality to operate on different types. Overloading promotes code reuse, but at the cost of understability and code complexity.

Choosing the right variation mechanism affects numerous costs:

- The skill set required to implement, or learn and use, the specific variation mechanism.
- Th one-time costs of building or acquiring the tools required to create the variation mechanism.
- The recurring cost and time to exercise the variation mechanism.

The choice of variation mechanism also affects downstream users and developers.

Finally, the choice of variation mechanism affects product quality:

- The impact of the variation mechanism on quality, such as possible performance penalties or memory consumption
- The impact on the mechanism's maintainability.

The architect should document the choice of variation mechanisms. The section called _variability guide_ is reserved for exactly this purpose. The variability guide should describe each variation mechanism, how and when to exercise it, and what allowed variations it supports. The architecture documentation should also describe the architecture's instantiation process == that is, how it's variation points are exercised. Also, if certain combinations of variations are disallowed, then the documentation needs to explain valid and invalid variation choices.

| Variation Mechanism                                          | Properties Relevant to Building the Core Assets       | Properties Relevant to Exercising the Variation Mechanism When Building Products               |
| ------------------------------------------------------------ | ----------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Inheritance; specializing or generalizing a particular class | Cost: Medium <br/>Skills: Object-oriented languages   | Stakeholder: Product developers<br/>Tools: Compiler <br/>Cost: Medium                          |
| Component substitution                                       | Cost: Medium <br/>Skills: Interface definitions       | Stakeholder: Product developer, system administrator <br/>Tools: Compiler <br/>Cost: Low       |
| Add-ons, plugins                                             | Cost: High <br/><br/>Skills: Framework programming    | Stakeholder: End user Tools: None <br/>Cost: Low                                               |
| Templates                                                    | Cost: Medium <br/>Skills: Abstractions                | Stakeholder: Product developer, system administrator <br/>Tools: None <br/>Cost: Medium        |
| Parameters (including text preprocessors)                    | Cost: Medium <br/>Skills: No special skills required  | Stakeholder: Product developer, system administrator, end user <br/>Tools: None <br/>Cost: Low |
| Generator                                                    | Cost: High <br/>Skills: Generative programming        | Stakeholder: System administrator, end user <br/>Tools: Generator <br/>Cost: Low               |
| Aspects                                                      | Cost: Medium <br/>Skills: Aspect-oriented programming | Stakeholder: Product developer <br/>Tools: Aspect-oriented language compiler <br/>Cost: Medium |
| Runtime conditionals                                         | Cost: Medium <br/>Skills: No special skills required  | Stakeholder: None <br/>Tools: None <br/>Cost: No development cost; some performance cost       |
| Configurator                                                 | Cost: Medium <br/>Skills: No special skills required  | Stakeholder: Product developer <br/>Tools: Configurator <br/>Cost: Low to medium               |

## Evaluating a Product Line Architecture

Like any other, the architecture for a software product line should be evaluated for fitness of purpose, robustness and generality, to make sure it meets the specific behavioral and quality requirements of the product at hand.

**What and How to Evaluate.** The evaluation will have to focus on the variation points to make sure they are appropriate, that they offer sufficient flexibility quickly, and that they do not impose unacceptable runtime performance costs. Try to elicit scenarios that capture the quality attributes required of family members.
**When to Evaluate.** An evaluation should be performed on an instance of variation of the architecture that will be used to build one or more products in the product line.
