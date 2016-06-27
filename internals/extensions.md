# Compiler Extensions

Orange supports extending the compiler's various phases, including lexing, parsing, and analysis. These extensions are written in Orange and can be delivered as Orange libraries. Other Orange projects can declare that they use these extensions to enable them in their code.

The extensions use `liborange` to hook into the compiler phases. The API for the extensions is currently undefined.

Extending the compiler is powerful and can support something like adding automatic reference counting as a feature to Orange. A basic idea of how that can be implemented is to keep track of when ARC objects are created, copied, and released.

Since the objects may pass into external libraries, those libraries would need to accomodate ARC checking. When writing an extension that needs to modify external libraries, your code can specify specifically what parts of your extension will and will not effect external libraries.

For example, you will want the external libraries to keep track of objects that have ARC, but not enforce that library to use ARC for all of its objects. The way to handle this is to only modify the `new` keyword for the original program using the extension. The modified `new` keyword will mark an object as being reference counted.

Default features of the compiler can be disabled on a per-project basis. `orange features` will list all of the features (including extensions), and which are enabled/disabled if you're inside of a project. 
