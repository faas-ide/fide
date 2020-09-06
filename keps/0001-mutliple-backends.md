---
kep-number: 1
short-desc: Use Fide against different backends (like Tekton, OpenFaas, AWS Lambda, Google Cloud Run)
title: Support Multiple Backends
authors:
  - "@DanielMSchmidt"
owners:
  - "@DanielMSchmidt"
  - "@dbanck"
creation-date: 2020-09-06
last-updated: 2020-09-06
status: provisional
see-also:
replaces:
superseded-by:
---

# Support Multiple Backends


## Table of Contents

A table of contents is helpful for quickly jumping to sections of a KEP and for highlighting any additional information provided beyond the standard KEP template.
[Tools for generating][] a table of contents from markdown are available.

- [Support Multiple Backends](#support-multiple-backends)
  - [Table of Contents](#table-of-contents)
  - [Summary](#summary)
  - [Motivation](#motivation)
    - [Goals](#goals)
    - [Non-Goals](#non-goals)
  - [Proposal](#proposal)
    - [User Stories [optional]](#user-stories-optional)
      - [Story 1](#story-1)
      - [Story 2](#story-2)
    - [Implementation Details/Notes/Constraints [optional]](#implementation-detailsnotesconstraints-optional)
    - [Risks and Mitigations](#risks-and-mitigations)
  - [Graduation Criteria](#graduation-criteria)
  - [Implementation History](#implementation-history)
  - [Drawbacks [optional]](#drawbacks-optional)
  - [Alternatives [optional]](#alternatives-optional)
  - [Infrastructure Needed [optional]](#infrastructure-needed-optional)

[Tools for generating]: https://github.com/ekalinin/github-markdown-toc

## Summary

To make Fide useful to a variety of FAAS enthusiasts we want to support running Fide against multiple backends like Tekton on Kubernetes, OpenFAAS on Kubernetes, AWS Lambda Function, and Google Cloud Run.
Finding an abstraction that supports all of these offerings, leveraging their strengths while also allowing Fide to make use of its features is crucial to having a good development workflow.

## Motivation

To make Fide useful to any user it must at the same time be able to provide its features, e.g. showing an overview of your architecture, CRUD actions on the functions, auto-deploying, or exporting the functions into a deployable format.

Fide must also be able to adjust to the environment it's deployed in. On Kubernetes-based backends, a user would expect information around the pod the function is scheduled in for debugging, whereas on public cloud FAAS offerings one might want to link to their dashboard.

### Goals

- Support Tekton on Kubernetes, OpenFAAS on Kubernetes, AWS Lambda Function, and Google Cloud Run as backends for the FAAS offering in Fide
- Seamlessly integrate into the backend of our choice, showing rich information
- Allow the open source community to extend fide with their own FAAS solution, ideally without needing to add source code to Fide itself.

### Non-Goals

- Support multiple backends at the same point in time. While ideally this option should be achievable with the chosen design it is not a priority as of right now.
- Enhance information shown with external information like logs, or metrics. While this is a goal we pursuit it is outside of the scope of this document.

## Proposal

This is where we get down to the nitty gritty of what the proposal actually is.

### User Stories [optional]

Detail the things that people will be able to do if this KEP is implemented.
Include as much detail as possible so that people can understand the "how" of the system.
The goal here is to make this feel real for users without getting bogged down.

#### Story 1

#### Story 2

### Implementation Details/Notes/Constraints [optional]

What are the caveats to the implementation?
What are some important details that didn't come across above.
Go in to as much detail as necessary here.
This might be a good place to talk about core concepts and how they releate.

### Risks and Mitigations

What are the risks of this proposal and how do we mitigate.
Think broadly.
For example, consider both security and how this will impact the larger kubernetes ecosystem.

## Graduation Criteria

How will we know that this has succeeded?
Gathering user feedback is crucial for building high quality experiences and owners have the important responsibility of setting milestones for stability and completeness.
Hopefully the content previously contained in [umbrella issues][] will be tracked in the `Graduation Criteria` section.

[umbrella issues]: https://github.com/kubernetes/kubernetes/issues/42752

## Implementation History

Major milestones in the life cycle of a KEP should be tracked in `Implementation History`.
Major milestones might include

- the `Summary` and `Motivation` sections being merged signaling owner acceptance
- the `Proposal` section being merged signaling agreement on a proposed design
- the date implementation started
- the first release where an initial version of the KEP was available
- the version of Fide where the KEP graduated to general availability
- when the KEP was retired or superseded

## Drawbacks [optional]

Why should this KEP _not_ be implemented.

## Alternatives [optional]

Similar to the `Drawbacks` section the `Alternatives` section is used to highlight and record other possible approaches to delivering the value proposed by a KEP.

## Infrastructure Needed [optional]

Use this section if you need things from the project/owner.
Examples include a new subproject, repos requested, github details.
Listing these here allows an owner to get the process for these resources started right away.