[Back to Table of Contents](index.md)

---

Syntax
======

The JSTP URI describes a [JSTP Endpoint](https://github.com/jstp/jstp-rfc/blob/master/version/0.6/syntax/endpoint.md) and it is divided into parts according to each of the elements in the Endpoint.

The overall structure of the JSTP URI can be described in [Augmented Backus-Naur Form](https://www.ietf.org/rfc/rfc2234.txt) as follow:

```abnf
jstp-uri = scheme [ methods ] [ to-addresses ] resource [ from-addresses ]

scheme = "jstp:"
methods = method [method-pattern]
method = "GET#" / "POST#" / "PUT#" / "PATCH#" / "DELETE#"
method-pattern = method / "*#"
to-addresses = address *comma-address "//"
address = host-name [ ":" host-port ":" transport-protocol ] / "*" / "..."
host-name = 1*ALPHA
host-port = 1*DIGIT
transport-protocol = 1*ALPHA
comma-address = "," address
from-addresses = ";" address *comma-address
resource = resource-element *slash-resource-element
resource-element = asterisk / ellipsis / ":" 1*ALPHA / 1*(ASCII character except URL reserved ones)
slash-resource-element = "/" resource-element
```

Scheme
------

The URI Scheme part of the URI is just the string `jstp:`.

Methods
-------

The URI Methods represent the Method Header in all dispatches and also the Method Pattern in a Subscription Dispatch. The method is represented in the URI by the method string followed by `#`. 

For example, the URI Methods of a Dispatch with a `BIND` Method Header and a `*` Method Pattern will be described as `BIND#*#`. An Answer Dispatch URI Methods will be described as `ANSWER#`.

The URI Methods are optional. If left out, a `GET` Method is assumed.

To Addresses
------------

The URI To Addresses represent the To Header of the Dispatch. Each element in the To Header is separated by a `,` and after the last address is listed, two slashes must be added: `//`. Each element in the To Addresses is called an Address.

For example, the URI To Addresses of a Dispatch with a `["localhost:80:tcp", "monje"]` To Header will be `localhost:80:tcp,monje//`. 

The URI To Addresses are optional. If left out, no To Header is assumed.

Resource
--------

The URI Resource represent the Resource Header of the Dispatch, or in the case of a Subscription Dispatch, the Resource Pattern of the Endpoint Header. Each Resource Element gets URL encoded if needed and are separated from each other by slashes `/`. Is noteworthy than in the URI Resource some information from the actual Dispatch Resource Header may be lost, since JSON `true` and `false` values are transformed to strings, and the same happens to `null`, which is transformed into the `"null"` string, and numbers.

For example, the Resource `["user", 80, true, null]` is described as `user/80/true/null`. 

The URI Resource is _required_. 

From Addresses
--------------

The URI From Addresses represent the From Header of the Dispatch. Each element in the From Header is separated by a `,` and before the first address is listed a semicolon must be added: `;`. Like in the To Addresses, each element in the From Addresses is called an Address.

For example, the URI From Addresses of a Dispatch with a `["2354s324d2134", "remote"]` From Header will be `;2354s324d2134,remote`.

The URI From Address is _optional_. If left out, no From Header is assumed.

Address
-------

An URI Address is the representation of an internet address and port number along with a transport communication protocol. Both the port number and transport protocol label are optional. Each part is separated from the others by a `:` colon.

### Host Name

The first element in the address is the host name. It can be any valid [domain name](http://www.ietf.org/rfc/rfc1035.txt) or [Internet Protocol](http://www.ietf.org/rfc/rfc791.txt) address. It also can be used to represent virtual resources within an application. 

The Host Name is _required_.

### Port Number

The Port Number is a positive integer representing the port number of the target destination. It is _optional_.

### Transport Protocol Label

Since JSTP can be sent over several Transport Protocols, the desired Transport Protocol can be represented with a label in the Address.

All lower case a-z strings are valid but three protocol handlers are supported:

- `ws` for WebSocket
- `tcp` for a plain TCP Socket
- `http` for polling over an HTTP connection.

---

[Back to Table of Contents](index.md)
