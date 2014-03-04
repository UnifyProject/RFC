# A Specification Process

This document proposes a process for building interoperable technical specifications. This process is lightweight, and seeks to engage the widest possible range of interested parties, moving rapidly to consensus through working code.

* Name: UnifyProject/draft/RFC-1
* Contributors: Pieter Hintjens <ph@travelping.com>

## Preamble

Copyright (c) 2014 all Contributors.

This text is published under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) (CC BY-SA 4.0). You are free to: share (copy and redistribute the material in any medium or format), and adapt (remix, transform, and build upon the material for any purpose, even commercially). The licensor cannot revoke these freedoms as long as you follow the license terms.

This text is governed by UnifyProject/RFC-1.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119), "Key words for use in RFCs to Indicate Requirement Levels".

## Goals

The primary goal of this document is to make it simple to write, prove, and improve new technical specifications. A "technical specification" defines a protocol, a process, an API, a use of language, a methodology, or any other aspect of a technical environment that can usefully be documented for the purposes of technical or social interoperability.

We intend this process above all to be economical and rapid, so that it is useful to small teams with little time to spend on more formal processes, as well as larger teams. 

Our principles are:

* We aim for rough consensus and running code.
* Specifications are small pieces, made by small teams.
* Specifications should have clearly responsible contributors.
* The process should be visible, objective, and accessible to anyone.
* The process should clearly separate experiments from solutions.
* The process should allow deprecation of old specifications.

Specifications should take minutes to explain, hours to design, days to write, weeks to prove, months to become mature, and years to replace.

Lastly, specifications have no special status except that accorded by the community.

This process resolves natural conflicts between teams and vendors by allowing anyone to define, improve, or choose to implement a new specification. There is no editorial control process except that practised by the contributors to a new specification.

## Overall Process

The project SHOULD require a statement from each contributor that their contributions will conform to the project's copyright, patent, and trademark policies.

Each specification SHALL BE a separate text file, in Markdown format.

Specifications SHALL be named "<state>/rfc-<number>.md" where <state> is one of "raw", "draft", "stable", "legacy", or "retired", and where <number> is a cardinal integer starting at 1.

A new version of a specification SHALL be a new specification, with a new number.

Lower numbers SHALL thus indicate more mature specifications, and higher numbers more experimental specifications.

Any contributor SHALL have the right to create a new specification, either from scratch, or by forking an existing specification.

The project SHALL have a well-defined process for editing and contributing to specifications.

## Specification Lifecycle

Every specification has an independent lifecycle. A specification has six possible states that reflect its maturity and contractual weight:

* New specifications are considered *raw*. Changes to raw specifications can be unilateral and arbitrary. Those seeking to implement a raw specification should ask for it to be made a draft specification. Raw specifications have no contractual weight.

* When raw specifications can be demonstrated, they become *draft* specifications. Changes to draft specifications should be done in consultation with users. Draft specifications are contracts between contributors and implementers.

* When draft specifications have at least two implementations, they become *stable* specifications. Changes to stable specifications should be restricted to errata and clarifications. Stable specifications are contracts between contributors, implementers, and end-users.

* When stable specifications are replaced by newer draft specifications, they become *legacy* specifications. Legacy specifications should not be changed except to indicate their replacements, if any. Legacy specifications are contracts between contributors, implementers and end-users.

* When legacy specifications are no longer used in products, they become *retired* specifications. Retired specifications are part of the historical record. They should not be changed except to indicate their replacements, if any. Retired specifications have no contractual weight.

* When raw or draft specifications are abandoned, they become *deleted* specifications. To change a deleted specification, the contributors should first change it to a raw specification. Deleted specifications have no contractual weight.

Raw and draft specifications SHOULD BE considered abandoned if they are not changed or used within a period of 3-6 months for raw specifications, and 9-18 months for draft specifications.

To change the state of a specification, a contributor SHALL rename it as appropriate.

Forked specifications, including added contributions, are derived works, and thus licensed under the same terms as the original specification. This means that contributors are guaranteed the right to merge changes made in branches back into their original specifications.

## Conventions

Contributors SHOULD where possible:

* Refer to and build on existing work when possible, especially IETF specifications.
* Contribute to existing raw or draft specifications rather than reinvent their own.
* Use collaborative branching and merging as a tool for experimentation.

## History and References

This document is inspired by the [Consensus Oriented Specification Process](http://www.digistan.org/spec:1), COSS, from the Digital Standards Organization.

The COSS process has been used successfully to drive the [ZeroMQ community specification](http://rfc.zeromq.org) process, with the development of successful lightweight standards like [ZMTP](zmtp.org).
