JSTP URI: JSTP/0.6 URI 1.0
=======================

This document specifies an independently created Uniform Resource Identifier standard aimed at the Internet community. 

The JSTP URI version described here is major version `1` and minor version `0` for JSTP version `0.6`, referred to as `JSTP/0.6 Engine 0.1`.

This document and the specified standard are released by the JSTP collaborators under the [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/deed).

Introduction
---------------

The JSTP URI is a uniform and portable description for the JSTP Endpoints as described in the [JSTP Endpoint Header](//github.com/jstp/jstp-rfc/blob/master/version/0.6/syntax/endpoint.md).

### Design goals

- Standardize description of JSTP Endpoints
- Simplify human communication of JSTP Dispatch descriptions

A crucial concern of the JSTP URI is to enable user agents to provide easy access to JSTP Resources, such as the HTTP URL has enabled the World Wide Web.

### Related specifications

[JSON Transfer Protocol RFC](//github.com/jstp/jstp-rfc): The main specification in the suite, it describes a communication protocol based in [JSON](http://www.json.org/) that aims to provide an uniform description language for resource access across the entire application stack.

[JSTP Engine Specification](https://github.com/jstp/jstp-engine): The JSON Transfer Protocol is the core standard in an specification suite along with the [JSTP Engine Specification](https://github.com/jstp/jstp-engine).

### Requirements

The key words "must", "must not", "required", "shall", "shall not", "should", "should not", "recommended", "may", and "optional" in this document are to be interpreted as described in [Key words for use in RFCs to Indicate Requirement Level _RFC 2119_](http://www.ietf.org/rfc/rfc2119.txt).

An implementation is not compliant if it fails to satisfy one or more of the _must_ or _required_ level requirements for the protocols it implements. An implementation that satisfies all the _must_ or _required_ level and all the _should_ level requirements for its protocols is said to be "unconditionally compliant"; one that satisfies all the _must_ level requirements but not all the _should_ level requirements for its protocols is said to be "conditionally compliant."

### Roadmap

You can find the [Roadmap](https://github.com/jstp/jstp-uri/issues/5) and the updated status of its implementation as an [issue in the issue tracker](https://github.com/jstp/jstp-uri/issues/5) for the specification repository.

Table of Contents
-----------------

2. [Syntax](syntax.md)


Acknowledgements
----------------

### Collaborators

- [Fernando Vía Canel](https://github.com/xaviervia)
- [Luciano Bertenasco](https://github.com/lbertenasco)

### Organizations

- [SouthLogics](http://southlogics.com)

License
-------

[Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/legalcode).
