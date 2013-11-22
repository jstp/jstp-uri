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

---

**CONTINUE**

---

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
