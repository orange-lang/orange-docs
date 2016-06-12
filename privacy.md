# Privacy

	privacy_level -> "private" | "protected" | "public"

Every global declaration (classes, functions, enums, etc) can be given a privacy level. This will effect how the type is used outside of the current code file. The valid privacy levels are `private`, `protected`, and `public`.

`private` indicates that the declaration can only be used inside the current file. `protected` means that the declaration can be used inside the current package, and `public` indicates it can be used anywhere.

The privacy indicators have different meanings inside of classes. For more information on classes, see Classes. For more information on packages, see [Namespaces &amp; packages](namespaces.md).

The default privacy level is `protected`.
