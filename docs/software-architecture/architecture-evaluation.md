---
sidebar_position: 9
---

# Architecture Evaluation

## Introduction

Analysis lies at the heart of architecture evaluation, which is the process of determining if an architecture is fit for the purpose for which ist is intended. Architecture is such an important contributor to the success of a system and software engineering project that it makes sense to pause and make sure that the architecture you've designed will be able to provide all that's expected of it. That's the role of evaluation. Fortunately there are mature methods to evaluate architectures that use many of the concepts and techniques we've already covered on previous sections.

## Evaluation Factors

Evaluation usually takes one of three forms:

- Evaluation by the designer within the design process
- Evaluation by peers within the design process
- Analysis by outsiders once the architecture has been designed

### Evaluation by the Designer

Every time the designer makes a key design decision or completes a design milestone, the chosen and competing alternatives should be evaluated using the analysis techniques describe in [QA analysis section](./quality-attributes/model-and-analysis.md). Evaluation by the designer is the "test" part of the "generate-and-test" approach to architecture design that we covered in [Designing an Architecture](./designing-architecture.md#generate-and-test).

How much analysis? This depends on the importance of the decision. Performing analysis is a matter of cost and benefit. Do not spend more time on a decision than it is worth, but also do not spend less time on an important decision than it needs. Some specific considerations include these:

- _The importance of the decision._ The more important the decision, the more care should be take in making it and making sure it's right.
- _The number of potential alternatives._ The more alternatives, the more time could be spent in evaluating them. Try to eliminate alternatives quickly so that the number of viable potential alternatives is small.
- _Good enough as opposed to perfect._ Many times, two possible alternatives do not differ dramatically in their consequences. In such a case, it is more important to make a choice and move on with the design process than it is to be absolutely certain that the best choice is being made. Again, do not spend more time on a decision than it is worth.

### Peer Review

Architectural designs can be peer reviewed just as code can be peer reviewed. A peer review can be carried oyt at any point of the design process where a candidate architecture, or at least a coherent reviewable part of one, exists. A peer review has several steps:

1. The reviewers determine a number of quality attribute scenarios to drive the review.
2. The architect presents the portion of the architecture to be evaluated.
3. For each scenario, the designer walks through the architecture and explains how the scenario is satisfied.
4. Potential problems are captured.

If the designers are using the ADD process, then a peer review can be done at then end of step 3 of each ADD iteration.

### Analysis by Outsiders

Outside evaluators can cast an objective eye on a n architecture. They are less likely to be afraid to bring up sensitive problems, or problems that aren't apparent because of organizational culture of because "we've always done it that way".

Often, outsiders are chosen because they possess specialized knowledge or experience.

### Contextual Factors

For peer reviews or outside analysis, there are a number of contextual factors that must be considered when structuring an evaluation.

- _What artifacts are available?_ To perform an architectural evaluation, there must be an artifact that describes the architecture. This must be located and made available.
- _Who sees the results?_ Some evaluations are performed with the full knowledge and participation of all of the stakeholders. Others are performed more privately.
- _Who performs the evaluation?_ Evaluations can be carried out by an individual or a team. In either case, the evaluator(s) should be highly skilled in the domain and the various quality attributes for which teh system is to be evaluated.
- _Which stakeholders will participate?_ The evaluation process should provide a method to elicit the goals and concerns that the important stakeholders have regarding the system.
- _what are the business goals?_ The evaluation should answer whether the system will satisfy the business goals. If the business goals are not explicitly captured and prioritized prior to the evaluation, then there should be a portion of the evaluation dedicated to doing so.

## The Architecture Tradeoff Analysis Method

The Architecture Tradeoff Analysis Method (ATAM) has been used for over a decade to evaluate software architectures in domain ranging from automotive to financial to defense. The ATAM is designed so that evaluators need to be familiar with the architecture or its business goals, the system need not yet be constructed, and there may be a large number ofr stakeholders.

### Participants in the ATAM

The ATAM requires the participation and mutual cooperation of three groups:

- _The evaluation team_. This group is external to the project whose architecture is being evaluated. It usually consists of three to five people. Each member of the team is assigned a number of specific roles to play during the evaluation. In any case, they need to be recognized as competent, unbiased outsiders with no hidden agendas or axes to grind.
- _Project decision makers_. These people are empowered to speak for the development project or have the authority to mandate changes to it.
- _Architecture stakeholders._ Stakeholders have a vested interest in the architecture performing as advertised. Their job during an evaluation is to articulate the specific quality attribute goals that the architecture should meet in order for the system to be considered a success.

Here are ATAM evaluation team roles:

| Role               | Responsibilities                                                                                                                                                                                                                                                                                                              |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Team Leader        | Sets up the evaluation; coordinates with client, making sure client’s needs are met; establishes evaluation contract; forms evaluation team; sees that final report is produced and delivered (although the writing may be delegated)                                                                                         |
| Evaluation Leader  | Runs evaluation; facilitates elicitation of scenarios; administers scenario selection/prioritization process; facilitates evaluation of scenarios against architecture; facilitates on-site analysis                                                                                                                          |
| Scenario Scribe    | Writes scenarios on flipchart or whiteboard during scenario elicitation; captures agreed-on wording of each scenario, halting discussion until exact wording is captured                                                                                                                                                      |
| Proceedings Scribe | Captures proceedings in electronic form on laptop or workstation: raw scenarios, issue(s) that motivate each scenario (often lost in the wording of the scenario itself), and resolution of each scenario when applied to architecture(s); also generates a printed list of adopted scenarios for handout to all participants |
| Questioner         | Raises issues of architectural interest, usually related to the quality attributes in which he or she has expertise.                                                                                                                                                                                                          |

### Outputs of ATAM

In preparation for an ATAM exercise, the project's decision makers must prepare the following:

- _A concise presentation of the architecture_
- _Articulation of the business goals._

The ATAM uses prioritizes quality attributes scenarios as the basis for evaluating the architecture, and if those scenarios do not already exist, they are generated by the participants as part of the ATAM exercise.

- _Prioritized quality attribute requirements expressed as quality attribute scenarios._
- _A set of risks an nonrisks_. A risk is defined in the ATAM as an architectural decision that may lead to undesirable consequences in light of stated quality attribute requirements.
- _A set of risk themes._ WHen the analysis is complete, the evaluation team examines the full set of discovered risks to look for overarching themes that identify system weaknesses in the architecture or even in the architecture process and team. I f left untreated, these risk themes will threaten the project's business goals.
- _Mapping of architectural decisions to quality requirements._
- _A set of identified sensitivity and tradeoff points._ These are architectural decisions that have a marked effect on one or more quality attributes

### Phases of the ATAM

Activities in an ATAM-based evaluation are spread out over four phases:

- In phase 0. "Partnership and Preparation," the evaluation team leadership and the key project decision makers informally meet to work out the details of the exercise. Together, the two groups agree on logistics. They also agree on a preliminary list of stakeholders, and they negotiate on when the final report is to be delivered and to whom. They deal with formalities such as a statement of work or nondisclosure agreements. The evaluation team examines the architecture documentation to gain an understanding of the architecture and the major design approaches that it comprises. Finally, the evaluation team leader explains what information the manager and architect will be expected to show during phase 1.
- Phase 1 and phase 2 are evaluation phases, where everyone gets down to teh business of analysis. These phases comprise a set of specific steps, which are detailed below.
- Phase 3 is a follow-up, in which the evaluation team produces and delivers a written final report.

| Phase | Activity                    | Participants                                               | Typical Duration                                          |
| ----- | --------------------------- | ---------------------------------------------------------- | --------------------------------------------------------- |
| 0     | Partnership and preparation | Evaluation team leadership and key project decision makers | Proceeds informally as required, perhaps over a few weeks |
| 1     | Evaluation                  | Evaluation team and project decision makers                | 1–2 days followed by a hiatus of 1–3 weeks                |
| 2     | Evaluation (continued)      | Evaluation team, project decision makers, and stakeholders | 2 days                                                    |
| 3     | Follow-up                   | Evaluation team and evaluation client                      | 1 week                                                    |

### Steps of the Evaluation Phases

- **Step 1: Present the ATAM.** The first step calls for the evaluation leader to present the ATAM to the assembled project representatives.
- **Step 2: Present the Business Drivers.** Everyone involved in the evaluation needs to understand the context for the system and the primary business drivers motivating its development. The presentation should describe the following:
  - The system's most important functions
  - Any relevant technical, managerial, economic, or political constraints
  - The business goals and context as they relate to the project
  - The major stakeholders
  - The architectural drivers
- **Step 3: Present the Architecture.** Here, the lead architect makes a presentation describing the architecture at an appropriate level of detail.
- **Step 4: Identify Architectural Approaches.** The ATAM focuses on analyzing an architecture by understanding its architectural approaches. By now, the evaluation team will have a good idea of what patterns and tactics the architect used in designing the system in this short step, the evaluation team simply catalogs the patterns and tactics that have been identified.
- **Step 5: Generate Quality Attribute Utility Tree.** IN this step, the quality attribute goals are articulated in detail via a quality attribute utility tree. Utility trees, which were described in [gathering requirements](./requirements.md#capturing-asrs-in-a-utility-tree), serve to make the requirements concrete by defining precisely the relevant quality attribute requirements that the architects were working to provide.
- **Step 6: Analyze Architectural Approaches.** Here the evaluation team examines the highest-ranked scenarios (as identified in the utility tree) one at a time; the architect is asked to explain how the architecture supports each one. Along the way, the evaluation team documents the relevant architectural decisions and identifies and catalogs their risks, nonrisks, sensitivity points, and tradeoffs. The analysis is not meant to be comprehensive. The key is to elicit sufficient architectural information to establish some link between the architectural decisions that have been made and the quality attribute requirements that need to be satisfied.

Here's a template for scenario analysis:

![Template for scenario analysis](/img/docs/template-scenario-analysis.png)

- **Hiatus and Start of Phase 2.** The evaluation team summarizes what it has learned and interacts informally with the architect during a hiatus of a week or two. More scenarios might be analyzed during this period, if desired, or questions of clarification can be resolved.

- **Step 7: Brainstorm and Prioritize Scenarios.** In this step, the evaluation team asks the stakeholders to brainstorm scenarios that are operationally meaningful with respect to the stakeholders' individual roles. SWhile utility tree generation is used primarily to understand how the architect perceived and handled quality attribute architectural drivers, the purpose of scenario brainstorming is to take the pulse of the larges stakeholder community: to understand what system success means for them. Scenario brainstorming works well in larger groups, creating an atmosphere in which the ideas and thoughts of one person stimulate others' ideas. Once the scenarios have been collected, they must be prioritized, for the same reasons that the scenarios in the utility tree needed to be prioritized: the evaluation team needs to know where to devote its limited analytical time. The list of prioritized scenarios is compared with those from the utility tree exercise. If they agree, it indicates good alignment between what the architect had in mind and what the stakeholders actually wanted. If additional driving scenarios are discovered -- and they usually are -- this may itself be a risk, if the discrepancy is large. This would indicated that there was some disagreement in the system's important goals between the stakeholders and the architect.

- **Step 8: Analyze Architectural Approaches.** After the scenarios have been collected and prioritized in step 7, the evaluation team guides the architect in the process of carrying out the highest ranked scenarios. The architect explains how relevant architectural decisions contribute to realizing each one.
- **Step 9: Present Results.** In step 9, the evaluation team groups risks into risk themes, based on some common underlying concern of system deficiency. For each risk theme, the evaluation team identifies which of the business drivers listed in step 2 are affected. The collected information from the evaluation is summarized and presented to stakeholders. Then the following outputs are presented:
  - The architectural approaches documented
  - The set of scenarios and their prioritization from the brainstorming
  - The utility tree
  - The risks discovered
  - The nonrisks discovered
  - The sensitivity points and tradeoff points found
  - Risk themes and the business drivers threatened by each one

## Lightweight Architecture Evaluation

Although we attempt to use time in an ATAM exercise as efficiently as possible, it remains a substantial undertaking. For this reason, a lightweight version of ATAM can be used, called Lightweight Architecture Evaluation, and it serves smaller, less risky projects. A Lightweight Architecture Evaluation exercise may take place in a single day, or even half-day meeting. It may be carried out entirely by members internal to the organization.

| Step                                       | Time Allotted                    | Notes                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------ | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1: Present the ATAM                        | 0 hrs                            | The participants are familiar with the process. This step may be omitted.                                                                                                                                                                                                                                                                                                                     |
| 2: Present Business Drivers                | 0.25 hrs                         | The participants are expected to understand the system and its business goals and their priorities. Fifteen minutes is allocated for a brief review to ensure that these are fresh in everyone’s mind and that there are no surprises.                                                                                                                                                        |
| 3: Present Architecture                    | 0.5 hrs                          | Again, all participants are expected to be familiar with the system and so a brief overview of the architecture, using at least module and C&C views, is presented and 1 to 2 scenarios are traced through these views.                                                                                                                                                                       |
| 4: Identify Architectural Approaches       | 0.25 hrs                         | The architecture approaches for specific quality attribute concerns are identified by the architect. This may be done as a portion of step 3.                                                                                                                                                                                                                                                 |
| 5: Generate Quality Attribute Utility Tree | Variable <br/> 0.5 hrs – 1.5 hrs | Scenarios might exist: part of previous evals, part of design, part of requirements elicitation. If you’ve got ’em, use ’em and make them into a tree. Half hour. Otherwise, it will take longer. A utility tree should already exist; the team reviews the existing tree and updates it, if needed, with new scenarios, new response goals, or new scenario priorities and risk assessments. |
| 6: Analyze Architectural Approaches        | 2–3 hrs                          | This step—mapping the highly ranked scenarios onto the architecture—consumes the bulk of the time and can be expanded or contracted as needed.                                                                                                                                                                                                                                                |
| 7: Brainstorm and Prioritize Scenarios     | 0 hrs                            | This step can be omitted as the assembled (internal) stakeholders are expected to contribute scenarios expressing their concerns in step 5.                                                                                                                                                                                                                                                   |
| 8: Analyze Architectural Approaches        | 0 hrs                            | This step is also omitted, since all analysis is done in step 6.                                                                                                                                                                                                                                                                                                                              |
| 9: Present Results                         | 0.5 hrs                          | At the end of an evaluation, the team reviews the existing and newly discovered risks, nonrisks, sensitivities, and tradeoffs and discusses whether any new risk themes have arisen.                                                                                                                                                                                                          |
