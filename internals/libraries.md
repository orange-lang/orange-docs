# Library Format

When a library is built in Orange, it is compiled in an intermediate representation of the AST with type information for the entirety of the AST. This allows for Orange to read in the IR and skip right to compiling for your native architecture, independent of the original platform the library was written on.

One of the benefits of delivering libraries this way is that the libraries can be recompiled by users at will with various settings toggled. See [Compiler Extensions](extensions.md) for more information.

The IR format Orange uses for libraries is currently undefined.
