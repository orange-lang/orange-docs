# Builtin Types

The builtin plain types in Orange are the following:

```
int    int8   int16  int32  int64
uint   uint8  uint16 uint32 uint64
float  double char   bool   string
void
```

Note that `string` is actually an [alias](aliases.md) to `char[]`, which means that any operation that can be done on a `char[]` can also be done on a `string`.
