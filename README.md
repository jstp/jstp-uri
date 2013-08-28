JSTP URI Scheme RFC
===================

Current version: 0.1

This document describes a draft standard.

Rationale
---------


In order to simplify the description of JSTP dispatches, it would be nice to have a JSTP uri scheme.

JSTP is similar enough to HTTP to be described with similar structure in an uri, the main exceptions being the multiple hosts header and the complex nature of the Dispatch Body.

Samples
-------

Local PUT Dispatch to User resource: `PUT jstp:///User`

Remote (one host) POST Dispatch to Article: `POST jstp://db:8000:tcp/Article`

Binding to double remote DELETE of Library: `BIND DELETE jstp://hub:80:ws,building:80:ws/Library`

In many cases, the `jstp://`prefix is verbose and avoidable, such as application logs. A simplified form will be:

`POST db:8000:tcp/Article`

Should any other type of data be listed in the URL? This looks ok, but maybe the Dispatch Body could be added using some kind of encoding, such as base64 or URL encoding, after a `?`.

Also: Resources should be URL encoded when using URLs. Mainly because of the `/` char that can legally be used within a Resource Item.
