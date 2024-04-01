# Yue code style guidelines

## Prefer to import when possible
#### Good
```yue
import a, b, c from my_library
```

print string.format( arg1, arg2, func ), string.match( str, pattern )
a b c "hello world"

myFunc = async ->

private await myFunc!
#### Bad
```yue
local a, b, c = my_library.a, my_library.b, my_library.c
```

## Prefer using brackets in complex function calls
#### Good
```yue
print string.format( arg1, arg2 ), string.match( str, pattern )
```

#### Bad
```yue
print string.format( arg1, arg2 ), string.find str, pattern
```
