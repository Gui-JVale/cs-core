---
sidebar_position: 1
---

# Economic Analysis

## Introduction

This far we have been primarily investigating the relationships between architectural decisions and the quality attributes that the architecture's stakeholders have deemed important: if I make this architectural decision, what effect will it have on the quality attributes? If I have to achieve that quality attribute requirements, what architectural decision will do the trick?

As important as this effort is, this perspective is missing a crucial consideration: What are the economic implications of an architectural decision?

Usually an economic discussion is focused on costs, primarily the costs of building the system in the first place. Other costs, often but not always down-played, include the long-term costs incurred through cycles of maintenance and upgrade.

Given that the resources for building and maintaining a system are finite, there must be a rational process that helps us choose among architectural options, during both an initial design phase and subsequent upgrade periods.

## Decision-Making Context

Business goals play a key role in requirements for architectures. Because major architectural decisions have technical and economic implications, the business goals behind a software system should be used to directly guide those decisions. The most immediate economic implication of a business goal decision on an architecture is hot it affects the cost of implementing the system.

Knowing the costs and benefits associated with particular decision enables reasoned selection from among competing alternatives. The economic analysis does not make decision for the stakeholders, it simply aids in the elicitation and documentation of value for cost (VFC). It gives stakeholders a framework withing which they can apply a rational decision-making process that suits their needs and their risk aversion.

Economic analysis isn't something to apply to every architectural decision, but rather to the most basic ones that put an overarching architectural strategy in place.

## The Basis for Economical Analysis

We now describe the key ideas that form the basis for the economic analyses.

We begin by considering a collection of scenarios generated as a portion of requirements elicitation, an architectural evaluation, or specifically for the economic analysis. We examine how these scenarios differ in the values of their projected responses and we then assign utility to those values. The utility is based on the importance of each scenario being considered with respect to its anticipated response value.

Armed with our scenarios, we next consider the architectural strategies that lead to the various projected responses. Each strategy has a cost, and each impacts multiple quality attributes. The utility of these "side effects" must be taken in account when considering a strategy's overall utility. It is this overall utility that we combine with the project cost of an architectural strategy to calculate a final VFC measure.

### Utility-Response Curves

Our economic analysis uses quality attribute scenarios as the way to concretely express and represent specific quality attributes. We vary the values of the responses, and ask what the utility is of each response. This leads to the concept of a utility-response curve.

Each scenario's stimulus-response pair provides some utility (value) to the stakeholders, and the utility of different possible values for the response can be compared.

We portray each relationship between a set of utility measures and a corresponding set of set of response measures as a graph -- a utility-response curve.

The utility-response curve depicts how the utility derived from a particular response varies as the response varies.

### Weighting the Scenarios

Different scenarios will have different importance to the stakeholders; ikn order to make a choice of architectural strategies that is best suited to the stakeholders' desires, we must weight the scenarios.

### Side Effects

Every architectural strategy affects not only the quality attributes it was selected to achieve, but also other quality attributes as well. As you know by now, theses side effects on other quality attributes are often negative. If those effects are too negative , we must make sure there is a scenario for the side effect attribute and determine its utility-response curve so that we can add its utility to the decision-making mix. We calculate the benefit of applying an architectural strategy by summing its benefits to all relevant quality attributes.

### Determining Benefit and Normalization

The overall benefit of an architectural strategy across quality attribute scenarios is the sum of the utility associated with each one, weighted by the importance of the scenario.

### Calculating Value for Cost

The VFC for each architectural strategy is the ratio of the total benefit, to the cost of implementing it.

The cost is estimated using a model appropriate for the system and the environment being developed, such as a cost model that estimates implementation cost by measuring an architecture's interaction complexity.

## Putting Theory into Practice: The CBAM

With the concepts in place we can now describe techniques for putting them into practice, in the form of a method we call the Cost Benefit Analysis Method (CBAM).

### Practicalities of Utility Curve Determination

To build the utility-response curve, we first determine the quality attribute levels for the best-case and worst-case situations. The base-case quality attribute level is that above which the stakeholders foresee no further utility.

These levels == best-case and worst-case -- are assigned utility values of 100 and 0, respectively. We then determine the current and desired utility levels for the scenario. The respective utility values (between 0 and 100) for various alternative strategies are elicited from the stakeholders, using the best-case and worst-case values as reference points.

In this manner th utility curves are generated for all of the scenarios.

### Practicalities of Weighting Determination

One method of weighting the scenarios is to prioritize them and use their priority ranking as the weight. The stakeholders can determine the priorities through a variety of voting schemes.

### Practicalities of Cost Determination

One of the shortcomings of the field of software architecture is that there are very few cost models for various architectural strategies. There are many software cost models, but they are based on overall system characteristics such as size or function points. These are inadequate to answer te question of how much does it cost. More widely used in practice are corporate cost models based on previous experience with the same or similar architectures, or the experience and intuition of senior architects.

Lacking cost models whose accuracy can be assured, architects often turn to estimation techniques. To proceed, remember that an absolute number for cost isn't necessary to rank candidate architecture strategies. You can often say something like "Suppose strategy A costs $x. It looks like strategy be will cost $2x, and strategy C will cost $0.5x." That's enormously helpful. A second approach is to use very coarse estimates. Or if you lack confidence for that degree of certainty, you can say something like "Strategy A will cost a lot, strategy B shouldn't cost very much, and strategy C is probably somewhere in the middle."

### CBAM

Now we describe the method we use for economic analysis: the Cost Benefit Analysis Method. CBAM has for the most part been applied when a n organization was considering a major upgrade to an existing system and they wanted to understand the utility and value for cost of making the upgrade, of they wanted to choose between competing architectural strategies for the upgrade. CBAM is also applicable for new system as well, especially for helping to choose among competing strategies. Its key concepts (quality attribute response curves, cost, and utility) do not depend on the setting.

#### Steps

The description of CBAM assumes that a collection of quality attribute scenarios already exists. This collection might have come from a previous elicitation exercise such as an ATAM exercise or quality attribute utility tree construction.

The steps are as follows:

1. **Collate scenarios.** Give the stakeholders the chance to contribute new scenarios. Ask the stakeholders to prioritize the scenarios based on satisfying the business goals of the system.
2. **Refine scenarios.** Refine the scenarios chosen in step 1, focusing on their stimulus-response measures. Elicit the worst-case, current, desired, and best-case quality attribute response level for each scenario.
3. **Prioritize scenarios.** Prioritize the refined scenarios, based on stakeholder votes. Make a list of the quality attributes that concern the stakeholders.
4. **Assign utility.** Determine the utility for each quality attribute response level (worst-case, current, desired, best-case) for the scenarios from step 3. You can conveniently capture the utility curves in a table.
5. **Map architectural strategies to scenarios and determine their expected quality attribute response levels.** For each architectural strategy under consideration, determine the expected quality attribute response levels that will result for each scenario.
6. **Determine the utility of the expected quality attribute response levels by interpolation.** Using the elicited utility values t ( that form a utility curve)., determine the utility of the expected quality attribute response level for the architectural strategy. Do thi for ech relevant quality attribute enumerated in step 3.
7. **Calculate the total benefit obtained from an architectural strategy.** SUbtract the utility value of the "current" level from the expected level and normalize it using the votes elicited in step 3. Sum the benefit due to a particular architectural strategy across all scenarios anc across all relevant quality attributes.
8. **Choose architectural strategies based on VFC subject to cost and schedule constraints.**
9. **Confirm results with intuition.** For the chosen architectural strategies, consider whether these seem to align with the organization's business goals.
