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
resource-element = asterisk / ellipsis / ":" 1*ALPHA / 1*(ASCII character except reserved ones)
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

The URI To Addresses represent the To Header of the Dispatch. Each element in the To Header is separated by a `,` and after the last address is listed, two slashes must be added: `//`.

For example, the URI To Addresses of a Dispatch with a `["localhost:80:tcp", "monje"]` To Header will be `localhost:80:tcp,monje//`. 

The URI To Addresses are optional. If left out, no To Header is assumed.

Resource
--------

The URI Resource represent the Resource Header of the Dispatch, or in the case of a Subscription Dispatch, the Resource Pattern of the Endpoint Header. Each Resource Element gets URL encoded if needed and are separated from each other by slashes `/`. Is noteworthy than in the URI Resource some information from the actual Dispatch Resource Header may be lost, since JSON `true` and `false` values are transformed to strings, and the same happens to `null`, which is transformed into the `"null"` string, and numbers.

For example, the Resource `["user", 80, true, null]` is described as `user/80/true/null`. 

The URI Resource is _required_. 

From Addresses
--------------

**TODO**

Rationale
---------

In order to simplify the description of JSTP dispatches, it would be nice to have a JSTP uri scheme.

JSTP is similar enough to HTTP to be described with similar structure in an uri, the main exceptions being the multiple hosts header and the complex nature of the Dispatch Body.

Samples
-------

Local PUT Dispatch to User resource: `PUT jstp:User`

Remote (one host) POST Dispatch to Article: `POST jstp:db:8000:tcp/Article`

Binding to double remote DELETE of Library: `BIND DELETE jstp:hub:80:ws,building:80:ws/Library`

In many cases, the `jstp:`prefix is verbose and avoidable, such as application logs. A simplified form will be:

`POST db:8000:tcp/Article`

Should any other type of data be listed in the URL? This looks ok, but maybe the Dispatch Body could be added using some kind of encoding, such as base64 or URL encoding, after a `?`.

PUT from a certain referer: `PUT Book//library`

Also: Resources should be URL encoded when using URLs. Mainly because of the `/` char that can legally be used within a Resource Item.

From the JSTP RFC
-----------------

JSTP Dispatches are designed from the bottom up to be as compatible with HTTP as possible, so JSTP resources can be represented as URLs. 

This sample Dispatch:

```javascript
{
  "protocol":   ["JSTP", "0.4"],      // The protocol and version
  "method":     "GET",                // The method. Headers are case-insensitive but is customary to user uppercase
                                      // in this one after the HTTP convention
  "resource":   ["foods", "pizza"],   // The selected resource which is to be retrieved (since the method is GET)
  "timestamp":  1365647440759,        // The milliseconds since the 1970-01-01 00:00:00.000 (also known as the UNIX timestamp)
  "token":      ["3434h5098asr34h3"], // [optional] An UUID called the Transaction ID, used to track back Answer Dispatches
  "host":       ["pizza.com.ar"],     // [optional] The destination host to which the Dispatch is to be sent
  "body":       {                     // [optional] A message body
    "message": "Let the cheese melt!"       
  }
}
```

...may be represented as an URL like this:

    jstp://pizza.com.ar/foods/pizza

This notation is useful to quickly build JSTP Dispatches from user input, as writing down the JSON by hand can be quite a burden.

---

[Back to Table of Contents](index.md)
