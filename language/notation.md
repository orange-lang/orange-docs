# Documentation Notation

Throughout this document, the following notation will be used:

- Optionals will be wrapped with `[[` and `]]`. For example, `hello [[world]]` would mean the phrases `hello` and `hello world` are both valid.  
- An `*` following optionals indicates that it can be repeated 0 or more times. 
- A `+` following optionals indicates that it must exist at least one time. 
- Terms which can be replaced with any other content are wrapped with `_`. For example, `hello, _name_` means that `hello, Austin` and `hello, April` are both valid strings.
- Anything else is literal, unless otherwise noted.
