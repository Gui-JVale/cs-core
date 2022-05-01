---
sidebar_position: 11
---

# Quality Attribute Model & Analysis

## Overview

In the introduction of the section, we've talked about the importance of architecture, and listed some of the reasons on why spending time designing the architecture of a system can be so valuable. One of the reasons is the ability to predict and analyze a system's quality attributes. Now that's huge! Imagine having to build the entire system just to test it out, and then find out that quality attribute requirements aren't met, talk about cost.

Quality attribute model and analysis lets us look at a system's quality attribute(s), and reason about it's effectiveness (or lack thereof).

However, while some quality attributes have very well-defined models and analysis methods, others do not enjoy such tangible and specific analysis. As an example, performance and availability have well defined ways of being analyzed, while modifiability, testability, and usability are more abstract in analysis.

Because of that, the nature of the analysis for each quality attribute can vary a lot. As an example, for performance, you can analyze the system with queueing theory and other known methods, for security, you may have a checklist to ensure that the system meets that attribute, for modifiability you may need to have some thought experiments to validate it, and so on.

## Analyzing Performance & Availability

Performance and availability have well-defined ways of modeling and analyzing.

For performance, you may use queueing and real-time scheduling theory. You can gather concrete parameters of the system, and test them accordingly to predict with a satisfactory precision the performance of the system.

For modifiability, the main way of analyzing is using probability and statistics by measuring the system's _mean time between failures_ and it's _mean time to recover_. Based on that, you can also predict with a satisfactory precision the availability of a system based on it's architecture.

The point is that both of these quality attributes have more tangible and concrete ways of being analyzed. We'll see that other quality attributes don't enjoy such concreteness.

## Quality Attribute Checklists

Another way to analyze an architecture for a given quality attribute is to go over a checklist for that quality attribute., These checklists can come in many forms, it could be industry consortia, comes from government organizations or private ones. In large organizations, they may be developed in house.

Checklists can focus on one quality attribute, or multiple at a time. They can be used not only to ensure certain quality attributes by the architect, but also for the purposes of certifications and regulations.

Checklists are common for security, safety and usability.

## Thought Experiments and Back-of-the-Envelope Analysis

Thought experiments is a formal term to more informal discussions that can happen in the office or when the architect is going over the architecture by himself.

They usually begin by going over a specific use case in which the system must carry out a functionality. At each step of this scenario, we must try and find as much problems as we can in the light of the current quality attribute being analyzed, this can be done by asking questions to see what can go wrong, what can fail, what's some unexpected behavior we're not considering, etc.

After uncovering these problems that may rise up during the thought experiment, we may ask:

- Are there mechanisms to detect that problem?
- Are there mechanisms to prevent or avoid that problem?
- Are there mechanisms to repair or recover from that problem if it occurs?
- Is this a problem we are willing to live with?

## Experiments, Simulations, and Prototypes

Another way of modeling or analyzing an architecture for quality attributes is by having experiments, simulation and prototypes. As you may imagine, these are more costly then the methods stated before, but they can be crucial when you must understand a parameter (or multiple) that's not very easy to predict.

As an example, on a performance critical website, one may wonder if it's best to deliver one big bundled compressed css and/or javascript file, or if it's best to code split it and deliver many modules. This may be tricky to predict, and so experiments can be made to better understand what's the best approach.

On a more complex architecture, for example a web-conferencing system, one may wonder things such as if

- Moving to a distributed database would negatively affect performance?
- How many participants can be hosted be a single conferencing server?
- What's the correct ratio between database servers and conferencing servers?

Some of these questions are really hard to answer with precision, and at the same time are crucial for the architecture. So the architect may decide to build a prototype that includes simulations to be able to benchmark and further understand the effects of each decision.

## Analysis at Different Stages in the Life-Cycle

Analysis can happen at every stage of the life cycle. However, it's very important to understand the costs that come with analyzing a system at different stages.

| Life-Cycle     | Stage Form of Analysis   | Cost        | Confidence  |
| -------------- | ------------------------ | ----------- | ----------- |
| Requirements   | Experience-based analogy | Low         | Low–High    |
| Requirements   | Back-of-the-envelope     | Low         | Low–Medium  |
| Architecture   | Thought experiment       | Low         | Low–Medium  |
| Architecture   | Checklist                | Low         | Medium      |
| Architecture   | Analytic model           | Low–Medium  | Medium      |
| Architecture   | Simulation               | Medium      | Medium      |
| Architecture   | Prototype                | Medium      | Medium–High |
| Implementation | Experiment               | Medium–High | Medium–High |
| Fielded System | Instrumentation          | Medium–High | High        |

The table above gives some insight on that. As you can see, the later in the life-cycle and the more complex the method, the more cost it takes. It's the job of the architect to understand how important is the achievement of the given quality attribute, and how worried are you about being able to achieve the goals of this attribute? And how much budget and schedule can you afford to allocate to this form of risk mitigation.
