---
kep-number: 2
short-desc: Support editing of functions written in different languages
title: Support Multiple Languages
authors:
  - "@DanielMSchmidt"
owners:
  - "@DanielMSchmidt"
  - "@dbanck"
creation-date: 2020-09-08
last-updated: 2020-09-08
status: provisional
---

# Support Multiple Languages

## Table of Contents

A table of contents is helpful for quickly jumping to sections of a KEP and for highlighting any additional information provided beyond the standard KEP template.
[Tools for generating][] a table of contents from markdown are available.

- [Support Multiple Languages](#support-multiple-languages)
  - [Table of Contents](#table-of-contents)
  - [Summary](#summary)
  - [Motivation](#motivation)
    - [Goals](#goals)
    - [Non-Goals](#non-goals)
  - [Proposal](#proposal)
    - [Implementation Details/Notes/Constraints](#implementation-detailsnotesconstraints)
      - [Deployed FAAS is the single source of truth](#deployed-faas-is-the-single-source-of-truth)
      - [Central configuration](#central-configuration)
  - [Graduation Criteria](#graduation-criteria)

[tools for generating]: https://github.com/ekalinin/github-markdown-toc

## Summary

To make Fide useful to a wide audience we need to support inline editing for FAAS written in different languages. The editor integration should work and the user needs access to a terminal to run helpers like code generators or linters.

## Motivation

Fide is all about giving a good overview on your FAAS and making it easy to iterate on functions. Having a great user experience when reading and editing files is key to this, but at the same time it's a topic big enough for its own project. This is the reason why we want to leverage open source projects for this feature instead of building it on our own.

### Goals

- Have an editor integration with support for the most popular languages
- Allow deploying the functions directly from Fide

### Non-Goals

- Handle differnet deployment mechanisms
- Support different sources for functions. Initially we will stick with GitHub
- Work with different revisions of the software

## Proposal

We want to use [GitPod](https://www.gitpod.io/) in the self-hosted version.
We will deploy it when deploying fide and we will integrate it for a seamless usage.
As the deployment mechanism will vary from platform to platform each provider needs to be capable of deploying GitPod on their own. As there are only limited platforms Fide will provide helpers to facilitate with installing GitPod on the three supported Platforms Kubernetes, AWS and Google Cloud.

For a great user experience GitPod will need to tightly integrate with Fide. We want to have a one-click experience on each function that brings you directly to the GitPod editor.
For this to happen we need to make the connection between a deployed function and it's location in a repository.
This means we need to enable GitPod to fetch the repository, credentials need to be configured for that.

### Implementation Details/Notes/Constraints

The information that needs to be exposed is the url to the git repo and the path to the file. We can neglect the revision for now as we expect the deployed version to be in sync with the master branch of the repositories.

We have two options to solve this:

#### Deployed FAAS is the single source of truth

Each platform has its own way to add meta information to the deployed FAAS. Kubernetes has annotations and labels, AWS has cloud tags and other platforms have other mechanisms. Choosing this way means we need to implement this functionality on every provider.

#### Central configuration

Fide could be configured by a single config file that connects the repositories to the functions deployed.

```yaml
repositories:
  - url: https://github.com/demo/faas
    functions:
      first-function: ./path/to/func.ts
      another: ./path/to/func.go
```

## Graduation Criteria

The implementation is finished when a user can directly change the source code of their function in the browser.
