---
sidebar_position: 8
---

# Reconstruction & Conformance

## Introduction

We have treated architecture as something largely under your control and shown how to make architectural decisions to achieve the goals and requirements in place for a system under development. But there is another side to the picture. **Suppose you have been given responsibility for a system that already exists, but you do not know its architecture**. Perhaps teh architecture was never recorded by the original developers, now long gone. Perhaps it was recorded but the documentation has been lost. Or perhaps it was recorded but the documentation is no longer synchronized with the system after a series of changes. How do you maintain such a system? How do you manage its evolution to maintain the quality attributes that its architecture (whatever it may be) has provided for us?

This section surveys techniques that allow an analysis to build, maintain, and understand a representation of an existing architecture. This is a process or reverse engineering, typically called architecture reconstruction. Architecture reconstruction is used, by the architect, for two main purposes:

- To document an architecture where the documentation never existed or where it has become hopelessly out of date
- To ensure conformance between the as-built architecture and the-designed architecture

**In practice, architecture reconstruction is a tool-intensive activity.**

**Architecture reconstructions is an interpretive, interactive, and iterative process involving many activities**; it is not automatic. It requires the skills and attention of both the reverse-engineering expert and, in the best case, the architect. And whether the reconstruction is successful or not, there is a price to pay: the tools come with a learning curve that requires time to climb.

## Architecture Reconstruction Process

**Architecture reconstruction requires the skillful application of tools, often with a steep learning curve**. No single tool does the entire job. The first step in the reconstruction process is to set up the workbench.

An architecture reconstruction workbench should be open (making it easy to integrate new tools as required) and provide an integration framework whereby new tools that are added to the tool set do not impact the existing tools or data unnecessarily.

Whether or not an explicit workbench is used, the software architecture reconstruction process comprises the following phases:

1. _Raw view extraction._ In the raw view extraction phase, raw information about the architecture is obtained from various sources, primarily source code, execution traces, and build scripts. Each of these sets of raw information is called a view.
2. _Database construction._ The database construction phase involves converting the raw extracted information into a standard form (because the various extraction tools may each produce their own form of output). This standardized form of the extracted views is then used to populate a reconstruction database. When the reconstruction process is complete, the database will be used to generate authoritative architecture documentation.
3. _View fusion and manipulation._ The view fusion phase combines the various views of the information stored in the database.
4. _Architecture analysis._ View fusion will result in a set of hypothesis about the architecture. There hypotheses take the form of architectural elements (such as layers) and the constraints and relationships among them> theses hypotheses need to be tested to see if they are correct, and that is the function of the analysis step. Some of these hypotheses might be disproven, requiring additional view extraction, fusion, and manipulation.

The four phases of architecture reconstruction are iterative. All of theses activities are greatly facilitated by engaging people who are familiar with the system.

## Raw View Extraction

Raw view extraction involves analyzing a system's existing design and implementation artifacts to construct one or more models of it. The result is a set of information that is used in the view fusion activity to construct more-refined views of the system that directly support the goals of the reconstructions, goals such as these:

- Extracting and representing a target set of architectural views,to support the overall architecture documentation effort.
- Answering specific questions about the architecture.

Information obtained can be categorized as either static or dynamic. Static information is obtained by observing inly the system artifacts, while dynamic information is obtained by observing how the system runs. The goal is to fuse both to create more accurate system views.

| Tool                       | Static or Dynamic | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Parsers                    | Static            | Parsers analyze the code and generate internal representations from it (for the purpose of generating machine code). It is possible to save this internal representation to obtain a view.                                                                                                                                                                                                                                                                                                                     |
| Abstract Syntax Tree (AST) | Static            | Analyzers AST analyzers do a similar job to parsers, but they build an explicit tree representation of the parsed information. We can build analysis tools that traverse the AST and output selected pieces of architecturally relevant information in an appropriate format.                                                                                                                                                                                                                                  |
| Lexical Analyzers          | Static            | Lexical analyzers examine source artifacts purely as strings of lexical elements or tokens. The user of a lexical analyzer can specify a set of code patterns to be matched and output. Similarly, a collection of ad hoc tools such as grep and Perl can carry out pattern matching and searching within the code to output some required information. All of these tools—code-generating parsers, AST-based analyzers, lexical analyzers, and ad hoc pattern matchers—are used to output static information. |
| Profilers                  | Dynamic           | Profiling and code coverage analysis tools can be used to output information about the code as it is being executed, and usually do not involve adding new code to the system.                                                                                                                                                                                                                                                                                                                                 |
| Code Instrumentation Tools | Dynamic           | Code instrumentation, which has wide applicability in the field of testing, involves adding code to the system to output specific information while the system is executing. Aspects, in an aspect-oriented programming language, can serve the same purpose and have the advantage of keeping the instrumentation code separate from the code being monitored.                                                                                                                                                |

## Database Construction

It is helpful to use a database to store the extracted information because the amount of information being stored is large, and the manipulations of the data are tedious and error-prone if done manually.

## View Fusion

Once the raw facts have been extracted and stored in a database, the reconstructor can now perform view fusion. In this phase, the extracted view are manipulated to create fused views,. Fused views combine information from one or more extracted views, each of which may contain specialized information.

The process of creating a fused view is the process of creating a hypothesis about the architecture and a visualization of it to aid in analysis.

By interpreting these fused views and analyzing them, it is possible to produce hypothesized architectural views of the system. These views can be interpreted, further refined, or rejected. There are no universal completion criteria for this process; it is complete when the architectural representation is sufficient to support the analysis needs of its stakeholders.

## Architectural Analysis: Finding Violations

Consider the following situation: You have designed an architecture, but you have suspicious that the developers are not faithfully implementing what you developed. So how do you test and ensure conformance to the design?

There are two major possibilities for maintaining conformance between code and architecture:

- _Conformance by construction._ Ensuring consistency by construction -- that is, automatically generating sa substantial part of the system based on an architectural specification -- is highly desirable because tools can guarantee conformance. Unfortunately, this approach has limited applicability. It can only be applied in situations where engineers can employ specific architecture-based development tools, languages, and implementation strategies.
- _Conformance by analysis._ This technique aims to ensure conformance by analyzing (reverse-engineering) system information to flag nonconforming elements, so that they can be fixed: brought into conformance. Unfortunately, however, this technique is limited in its applicability. There is an inherent mismatch between static, code-based structures such as classes and packages and the runtime structures, such as processes, threads, clients, servers, and databases, that are the essence of most architectural descriptions.

## Guidelines

The following are a set of guidelines for the reconstruction process:

- Have a goal and a set of objectives or questions in mind before undertaking an architecture reconstruction project.
- Obtain some representation, however coarse, of the system before beginning the detailed reconstruction process. This representation serves several purposes, including the following:
  - It identifies what information needs to be extracted from the system
  - It guides the reconstructor in determining what to look for in the architecture and what view sto generate
- In many cases, the existing documentation for a system may not accurately reflect the system as it is implemented. Therefore it may be necessary to disregard the existing documentation and use it only to generate the high-level views of teh system, because it should give an indication of the high-level concepts.
- Tools can support the reconstruction effort and shorten the reconstruction. process, but they cannot do an entire reconstruction effort automatically. The work involved in the effort requires the involvement of people who are familiar with the system. It is important to get these people involved in the effort at an early stage as it helps the reconstructor get a better understanding of the system being reconstructed.
