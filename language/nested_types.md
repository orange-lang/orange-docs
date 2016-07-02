# Nested Types

When a type is declared inside another type, like an enum inside of a class, the type must be referenced via its parent, such as `ParentType.ChildType`.

For example:

    class Run {
         enum RunType {
             TEST,
             REAL
         }
    }

    Run.RunType ty = Run.RunType.TEST

This also applies to nested namespaces; a namespace `NamespaceB` inside namespace `NamespaceA`'s full path is `NamespaceA.NamespaceB`. 
