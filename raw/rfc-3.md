# Simple Universal Node Schema (SUNS)

This document proposes the Simple Universal Node Schema, a resource model for working with UNIFY "Universal Nodes". SUNS defines the resources that a client can create, modify, retrieve, and delete on a node (the "server").

* Name: UnifyProject/draft/RFC-3
* Contributors: Pieter Hintjens <ph@travelping.com>

## Preamble

Copyright (c) 2014 all Contributors.

This text is published under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) (CC BY-SA 4.0). You are free to: share (copy and redistribute the material in any medium or format), and adapt (remix, transform, and build upon the material for any purpose, even commercially). The licensor cannot revoke these freedoms as long as you follow the license terms.

This text is governed by [UnifyProject/draft/RFC-1](https://github.com/UnifyProject/RFC/blob/master/draft/rfc-1.md).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119), "Key words for use in RFCs to Indicate Requirement Levels".

## Overall Design

SUNS is a schema designed to run over XARP, [UnifyProject/draft/RFC-2](https://github.com/UnifyProject/RFC/blob/master/raw/rfc-2.md). XARP specifies standard rules for representing resources, and standard mechanisms for working with them in a RESTful fashion over a client-server network.

Implementors should apply XARP's rules to all resources and methods that SUNS defines, unless this document explicitly states otherwise.

These terms are introduced by, and have specific meaning, in this specification:

* Node - a set of resources managed by one SUNS server, implementing a Universal Node.
* Switch - a virtual or physical network switch contained within a node.
* Function - a virtual or physical computing function contained within a node, or a switch.
* Port - a network port, contained within a switch.

SUNS defines one schema, "suns", with this structure:

    node
        |
        o- switch
        |  |
        |   o- port
        |   |
        |   o- function
        |
        o- function

## SUNS resource types

### Nodes

Nodes follow these rules:

* A node is a public collection of switches and functions.
* The server MAY implement multiple nodes.
* Nodes MAY be used to partition resources for authenticated access control.
* Nodes are configured resources: clients do not create or destroy nodes.
* Nodes act as namespaces for switches and functions.
* The client and server must agree in advance on the nodes that exist.
* The server SHOULD implement a default public node named "default".

The URI for a node is:

    {transport}://{server-name}[:{port}]/suns/node/{node-name}

The URI for the default node is:

    {transport}://{server-name}[:{port}]/suns/node/default

SUNS allows these methods on a node URI:

* GET - retrieves the node representation.
* POST - creates a new function or switch within the node.

A node document specifies the node properties, and has references to all public functions and switches that the node contains. The XML format of this document is:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
    <node title="{description}">
        [ <switch
            name="{name}"
            title="{description}"
            type="{type}"
            href="{URI}" /> ] ...
        [ <function
            name="{name}"
            title="{description}"
            type="{type}"
            href="{URI}" /> ] ...
    </node>
    </suns>

The node document does not necessarily list all functions and switches: clients may create these as private and thus make them inaccessible through discovery.

### Functions

To be defined.

### Switches

To be defined.

### Ports

To be defined.

