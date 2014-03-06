# XRAP-ZMTP - Remote Resource Access via ZeroMQ

This document proposes XRAP-ZMTP, a mapping for XRAP over the ZeroMQ Message Transfer Protocol. XRAP-ZMTP encodes the XRAP methods and headers in binary frames, and carries content bodies as JSON.

* Name: UnifyProject/draft/RFC-4
* Contributors: Pieter Hintjens <ph@travelping.com>

## Preamble

Copyright (c) 2014 all Contributors.

This text is published under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) (CC BY-SA 4.0). You are free to: share (copy and redistribute the material in any medium or format), and adapt (remix, transform, and build upon the material for any purpose, even commercially). The licensor cannot revoke these freedoms as long as you follow the license terms.

This text is governed by [UnifyProject/draft/RFC-1](https://github.com/UnifyProject/RFC/blob/master/draft/rfc-1.md).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119), "Key words for use in RFCs to Indicate Requirement Levels".

## Overall Design

To be defined. The idea is to encode each method as a formal message, with headers as fixed strings (the set of headers for each request and reply are well-defined by XRAP and do not change). Then, the payload is carried as a blob holding JSON (it could be XML, YAML or some other encoding).

This allows us to build a fixed XRAP-ZMTP library to carry payloads for any schema.

POST - create a new, dynamically named resource.
POST-OK
* Location - a URI that identifies newly created resource.
GET - retrieve the representation of a known resource.
* If-Modified-Since - a conditional GET using resource date.
* If-None-Match - a conditional GET using resource ETag.
* When-Modified-After - GET on resource date change.
* When-None-Match - GET on resource ETag change.
GET-OK
* ETag - an opaque hash tag that identifies a resource instance.
* Date-Modified - the date and time that resource was modified.
PUT - update a known resource.
* If-Unmodified-Since - a conditional PUT or DELETE using resource date.
* If-Match - a conditional PUT or DELETE using resource ETag.
PUT-OK
DELETE - remove a known resource.
* If-Unmodified-Since - a conditional PUT or DELETE using resource date.
* If-Match - a conditional PUT or DELETE using resource ETag.
DELETE-OK
ERROR

## Profiles

This specification does not specify the semantics of function, join, and switch types. These semantics are covered in separate *profile* specifications. Profiles are the main area of extension and experimentation in SUNS. Profiles follow these rules:

* The profile name is the specification name (number/Name).
* The server MUST list all the profiles it supports, in the node document.
* The server MUST NOT implement two profiles that have overlapping resource types.
* The client SHOULD check that the profiles it plans to use are implemented.

A profile defines the semantics of a set of function, join, and switch types. As part of that, the profile specification MAY extend the properties of functions, joins, or switches. A profile SHOULD work within the constraints defined by XARP as far as possible.

Profiles may depend on other profiles. The profile specification MUST list the profiles it directly depends on. When a server implements a particular profile it MUST implement all profiles that profile depends on, recursively until all dependencies are resolved.

