# Yue code style guidelines

## Import
Prefer to import when possible.
#### Good
```moon
import a, b, c from my_library
```

print string.format( arg1, arg2, func ), string.match( str, pattern )
a b c "hello world"

myFunc = async ->

private await myFunc!
#### Bad
```moon
local a, b, c = my_library.a, my_library.b, my_library.c
```

## Complex function calls
Prefer using brackets in complex function calls.
#### Good
```moon
print string.format( arg1, arg2 ), string.match( str, pattern )
```

#### Bad
```moon
print string.format( arg1, arg2 ), string.find str, pattern
```
