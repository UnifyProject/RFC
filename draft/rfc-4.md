# XRAP/ZMTP - An XRAP Mapping over ZeroMQ

This document proposes XRAP/ZMTP, a mapping for XRAP over the ZeroMQ Message Transfer Protocol. XRAP/ZMTP encodes the XRAP methods and headers in binary frames, and carries content bodies as JSON, XML, YAML, or any other suitable encoding.

* Name: UnifyProject/draft/RFC-4
* Contributors: Pieter Hintjens <ph@travelping.com>

## Preamble

Copyright (c) 2014 all Contributors.

This text is published under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) (CC BY-SA 4.0). You are free to: share (copy and redistribute the material in any medium or format), and adapt (remix, transform, and build upon the material for any purpose, even commercially). The licensor cannot revoke these freedoms as long as you follow the license terms.

This text is governed by [UnifyProject/draft/RFC-1](https://github.com/UnifyProject/RFC/blob/master/draft/rfc-1.md).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119), "Key words for use in RFCs to Indicate Requirement Levels".

## Formal Grammar

The following ABNF grammar defines the XRAP/ZMTP protocol:

    xrap-zmtp       = *( create | retrieve | update | delete )

    create          = C:POST ( S:POST-OK / S:ERROR )

    retrieve        = C:GET ( S:GET-OK / S:GET-EMPTY / S:ERROR )

    update          = C:PUT ( S:PUT-OK / S:ERROR )

    delete          = C:DELETE ( S:DELETE-OK / S:ERROR )

    ;   Create a new, dynamically named resource in some parent
    POST            = signature %x01 parent content
    signature       = %xAA %xA5
    parent          = string        ; Schema/type/name
    string          = size *VCHAR
    size            = OCTET
    content         = content-type content-body
    content-type    = string        ; Content type
    content-body    = *OCTET        ; Resource spec, ZeroMQ frame

    ;   Success response for POST
    POST-OK         = signature %x02 status-code location
                    etag date-modified content
    status-code     = 2OCTET        ; Response status code 2xx
    location        = string        ; Schema/type/name
    etag            = string        ; Opaque hash tag
    date-modified   = 8OCTET        ; Date and time modified

    ;   Retrieve a known resource
    GET             = signature %x03 resource
                    if-modified-since if-none-match
                    content-type
    resource        = string        ; Schema/type/name
    if-modified-since = 8OCTET      ; GET if more recent
    if-none-match   = string        ; GET if changed

    ;   Success response for GET
    GET-OK          = signature %x04 status-code content

    ;   Conditional GET returned 304 Not Modified.
    GET-EMPTY       = signature %x05 status code

    ;   Update a known resource.
    PUT             = signature %x06 resource
                    if-unmodified-since if-match
                    content
    if-unmodified-since = 8OCTET    ; Update if same date
    if-match        = string        ; Update if same ETag

    ;   Success response for PUT
    PUT-OK          = signature %x07 status-code location
                    etag date-modified

    ;   Remove a known resource
    DELETE          = signature %x08 resource
                    if-unmodified-since if-match

    ;   Success response for DELETE
    DELETE-OK       = signature %x09 status-code

    ;   Error response for any request, 4xx or 5xx
    ERROR           = signature %x10 status-code status-text
    status-text     = string        ; Response status text

## ZeroMQ Socket Types

The server SHALL create a ROUTER socket and SHOULD bind it to port <to be specified>, which is the registered Internet Assigned Numbers Authority (IANA) port for XRAP. The server MAY bind its ROUTER socket to other ports in the ephemeral port range (%C000x - %FFFFx). The client SHALL create a DEALER socket and connect it to the server ROUTER host and port.

Note that the ROUTER socket provides the caller with the connection identity of the sender for any message received on the socket, as an identity frame that precedes other frames in the message.

## Protocol Signature

Every ZeroMQ message SHALL start with the XRAP/ZMTP protocol signature, %xAA %xA5. The server and client SHALL silently discard any message received that does not start with these two octets.

This mechanism is designed particularly for servers that bind to ephemeral ports which may have been previously used by other protocols, and to which there are still peers attempting to connect. It is also a general fail-fast mechanism to detect ill-formed messages.

## Semantics for Methods and Fields

All semantics are directly taken from UnifyProject/draft/RFC-2.

## Security Aspects

XRAP/ZMTP uses the ZMTP transport layer security mechanisms (NULL, PLAIN, CURVE, etc.) There are no specific security aspects in this protocol.
