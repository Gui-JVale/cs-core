---
sidebar_position: 10
---

# Management & Governance

## Introduction

The project manager is the person with whom you, as the architect, must work most closely, from an organizational perspective, and consequently it is important for you to have an understanding of the project manager's problems and the techniques available to solve those problems.

**Architecture is most useful in medium-to large-scale projects** -- projects that typically have multiple teams, too much complexity for any individual to fully comprehend, substantial investment, and multiyear duration.

## Planning

The planning for a project proceeds over time. There is an initial plan that is necessarily top-down to convince upper management to build thi system and give them some idea of the cost and schedule. This top-down schedule will inherently be incorrect. According to Dan Paulish, based on his experience iat Siemens Corporation, some rules of thumb that can be used to estimate the top-down schedule for medium-sized projects are these:

- Number of components to be estimated: ~150
- Paper design time per component: ~4 hours
- Time between engineering releases: ~8 weeks
- Overall project development allocation:
  - 40 percent design: 5 percent architectural, 35 percent detailed
  - 20 percent coding
  - 40 percent testing

Once the system has been given a go-ahead and a budget, the architecture team is formed and produces an initial architecture design. One case is that the budget is for the whole project and includes the schedule as well. We will call this case top-down planning. The second case is that the budget is just for the architecture design phase. In this case, the overall project budget emerges from the architecture design phase.

We now describe a merged process that includes both the top-down budget and schedule as well as a bottom-up budget and schedule that emerges from the architecture design phase.

The architecture team produces the initial architecture design and the release plans for the system: what features will be released and when the releases will occur. Then leads for the various pieces of the project can be assigned and they can build their teams. At this point, cost and schedule estimates from the team leads and an overall project schedule can be produced. This bottom-up schedule is usually much more accurate than the top-down schedule. These differences between the top-down adn bottom-up schedules need to be discussed and sometimes negotiated.

## Organizing

Some of the elements of organizing a project are team organization, division of responsibilities between project manager and software architect, and planning for a global or distributed development.

### Software Development Team Organization

Once the architecture design is in place, ikt can be used to define th eproject oranization. Each member of the team that designed the software architecture becomes the elad for a team whose responsibility is to implement a portion of the architecture.

Typical roles withing a software development team are the following:

- _Team leader_ -- manages tasks withing the team.
- _Developer_ -- designs and implements subsystem code.
- _Configuration manager_ -- performs regular builds and integration tests. This role can frequently be shared among multiple software development teams.
- _System test manager_ -- system test and acceptance testing.
- _Product manager_ -- represents marketing: defines feature sets and how system being developed integrates with other systems in a product suite.

### Division of Responsibilities between Project Manager and Software Architect

One of the important relations withing a team is between the software architect and the project manager. You can view the project manager as responsible fo r the external-facing aspects of the project and the software architect as responsible for the internal aspects of the project. This division will only work if the external view accurately reflects the internal situation and the internal activities accurately reflect the expectations of the external stakeholders. that is, the project manager should know, and reflect to management, the progress and the risks within the project, and the software architect should know, and reflect to developers, stakeholder concerns. The relationship between the project manager and the software architect will have a large impact on the success of a project. They need ot have a good working relation and be mindful of the roles they are filling and the boundaries if those roles.

## Implementing

During the implementation phase of a project, the project manager and archigtect have a series of decisions to make.

### Tradeoffs

From the project manager's perspective, tradeoffs are between quality, schedule, functionality, and cost. Which of theses aspects is most important depends on the project context, and one of the project manager's major responsibilities is to make this determination.

Over time, there is always new functionality that someone wants to have added to the project. It is important that the consequences of these new requirements, in terms of cost and schedule, be communicated to all concerned stakeholders. This is an area where the project manager and the architect must cooperate.

The project manager's first response to creeping functionality is to resist it. Acting as a gatekeeper for the project and shielding it from distractions is a portion of the job description. One technique that is frequently used to manage change is a change control board. Bureaucracy can, at times, be your friend.

Any change to the architecture will incur costs, and it is the architect's responsibility to be the gatekeeper for such changes.

### Incremental Development

Recall that the software development plan lays out the overall schedule. Every six to eight weeks a new release should be available and the specifics of the next release are decided,. Forty percent of a typical project's effort is devoted to testing. This means that testing should begin as soon as possible. This leads to a release being in one of three states:

1. _Planning_. This occurs towards the end of the prior development release.
2. _Development_. The planned release is coded.
3. _Test and repair._ The release is tested through exercise of the test plan.

### Tracking progress

The project manager can track progress though personal contact with developers, forma status meetings, metrics, and risk management.

The project manager must prioritize the risks, frequently with the assistance of the architect, and , for the most serious risks, develop a mitigation strategy. Mitigating risks is also a cost, and so implementing the strategy to reduce a risk depends on its priority, likelihood of occurrence, and cost if it does occur.

## Measuring

Metrics are an important tool for project managers. They enable the manager to have an objective basis both for their own decision making and for reporting to upper management on the progress of the project.

Metrics can be global -- pertaining to the whole project -- or they may depend on a particular phase of the project. Another important class of metrics is "cost to complete."

### Global Metrics

Global metrics aid the project manager in obtaining an overall sense of the project and tracking its progress over time. All global metrics should be updated from time to time as the project proceeds.

First, the project manager needs a measure of project size. The three most common measures of a project size are lines of code, function points, and size of a test suite. Schedule deviation is another global metric. By drilling down in this metric and discovering which teams are slipping, the project manager can decide to reallocate resources, if necessary.

Developer productivity is another metric that the project manager can track.

Finally, defects should be tracked. Anomalies in the number rof defects discovered over time indicate a potential problem that should be investigated.

### Phase Metrics and Costs to Complete

OPen issues should be kept for each phase. Unmitigated risks from review are treadn in a similar fashion.

Costs to complete is a bottom-up measure that derives from the bottom-up schedule. Once ghe various pieces of the architecture have been assigned to teams, then the teams take ownership of their schedule and the costs to complete their pieces.
