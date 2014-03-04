# UNIFY PROJECT - RFCs

"The UNIFY project aims at influencing standardization work globally, ensuring that European positions are well represented in the resulting recommendations and standards."

This is a collection of Requests for Comments for the UNIFY project.

## RFC Specification Process

The overall RFC process is defined by [UnifyProject/draft/RFC-1](https://github.com/UnifyProject/RFC/blob/master/draft/rfc-1.md).

The current editing process is:

* All specifications have a single responsible editor.
* All changes should be driven by GitHub issues that clearly identity a single problem, and optionally suggest one or more solutions.

## Current RFCs

### RFC 2: Extensible Resource Access Protocol (XRAP)

Status: raw.

This document proposes the Extensible Resource Access Protocol, a set of conventions for working with remote resources. XRAP divides domain-specific APIs from transport layers (HTTP, ZMTP, IPC, etc.), and ensures that such APIs have a consistent grammar.

* [Read UnifyProject/raw/RFC-2](https://github.com/UnifyProject/RFC/blob/master/raw/rfc-2.md).

### RFC 3: Simple Universal Node Schema (SUNS)

Status: raw.

This document proposes the Simple Universal Node Schema, a resource model for working with UNIFY "Universal Nodes". SUNS defines the resources that a client can create, modify, retrieve, and delete on a node (the "server").

* [Read UnifyProject/raw/RFC-3](https://github.com/UnifyProject/RFC/blob/master/raw/rfc-3.md).

### RFC 4: XRAP-ZMTP - Remote Resource Access via ZeroMQ

Status: raw.

This document proposes XRAP-ZMTP, a mapping for XRAP over the ZeroMQ Message Transfer Protocol. XRAP-ZMTP encodes the XRAP methods and headers in binary frames, and carries content bodies as JSON.

* [Read UnifyProject/raw/RFC-4](https://github.com/UnifyProject/RFC/blob/master/raw/rfc-4.md).

