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

## SUNS Resource Types

### Nodes

Nodes follow these rules:

* A node is a public collection of switches and functions.
* The server MAY implement multiple nodes.
* Nodes MAY be used to partition resources for authenticated access control.
* Nodes are configured resources: clients do not create or destroy nodes.
* Nodes act as containers (namespaces) for switches and functions.
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

Functions follow these rules:

* A function is a named computation resource, e.g. a thread, a process, a virtual machine.
* The server MAY implement a set of configured public functions.
* Clients MAY create private functions for their own use.
* To create a new function the client POSTs a function document to the parent node URI.

SUNS allows these methods on a function URI:

* GET - retrieves the function definition.
* PUT - updates the function. The function name and type cannot be modified.
* DELETE - deletes the function.

The XML specification for a function has this format:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
      <function
        name="{function name}"              mandatory function name
        [ type="{function type}" ]          optional type
        [ title="{short title}" ]           optional title
        />
    </suns>

The type defines the implementation of the function, and are defined by the server configuration. We do not at this stage standardize function types. If the client attempts to create a function with an unknown type, the server responds with "400 Bad Request". If the client specifies no type, the server shall use a suitable default type.

- number of CPUs
- CPU quota (usec)
- memory (bytes)
- disk elements (preconfigured)
--> all physical elements preconfigured as profiles
- for compute, storage, memory


### Switches

Switches follow these rules:

* A switch is a named network traffic management resource, and can be virtual or physical.
* The server MAY implement a set of configured public switches.
* Clients MAY create private switches for their own use.
* To create a new switch the client POSTs a switch document to the parent node URI.

SUNS allows these methods on a switch URI:

* GET - retrieves the switch representation.
* PUT - updates the switch. The switch name and type cannot be modified.
* POST - creates a new port in the switch.
* DELETE - deletes the switch.

The XML specification for a new switch has this format:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
      <switch
        name="{switch name}"                mandatory switch name
        [ type="{switch type}" ]            optional type
        [ title="{short title}" ]           optional title
        />
    </suns>

The XML description of an existing switch has this format:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
      <switch
        name="{switch name}"                switch name
        type="{switch type}"                actual switch type
        [ title="{short title}" ]           title, if specified
        >
        [ <port href="{port URI}"
            type="{port type}" /> ] ...
      </switch>
    </suns>

The type defines the implementation of the switch, and are defined by the server configuration. We do not at this stage standardize switch types. If the client attempts to create a switch with an unknown type, the server responds with "400 Bad Request". If the client specifies no type, the server shall use a suitable default type.

### Ports

Ports follow these rules:

* To be defined.

SUNS allows these methods on a port URI:

* GET - retrieves the port representation.
* PUT - updates the port.
* DELETE - deletes the port.

The XML specification for a new port has this format:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
      <port
        [ type="{port type}" ]              optional type
        [ title="{short title}" ]           optional title
        />
    </suns>

The XML description of an existing port has this format:

    <?xml version="1.0"?>
    <suns xmlns="http://digistan.org/schema/suns">
      <port
        name="{port name}"                  server-generated hash
        type="{port type}"                  actual port type
        [ title="{short title}" ]           title, if specified
        >
      </port>
    </suns>

