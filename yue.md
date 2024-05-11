# Yue code style guidelines

## Import
Prefer to import when possible.
#### Good
```moon
import tostring, type from _G
import a, b, c from my_library
```

#### Bad
```moon
tostring = tostring
type = type
a, b, c = my_library.a, my_library.b, my_library.c
```

```moon
:a, :b, :c = my_library
```

## Table values
If your table is not a library it is advisable to use `:` to extract the value if possible in order to shorten the code.
#### Good
```moon
tbl = {
    key: true
}

:key = tbl
print key
```

#### Bad, is not a bad solution, it's just that in this case you are writing two `key` instead of one to get the value.
```moon
tbl = {
    key: true
}

key = tbl.key
print key
```

## Complex function calls
Prefer using brackets in complex function calls.
#### Good
```moon
print string.format( arg1, arg2 ), string.match( str, pattern )
print string.match( string.lower( str ), pattern )
```

#### Bad
```moon
print string.format( arg1, arg2 ), string.find str, pattern
-- this one gives wrong results and is hard to read
print string.match string.lower str, pattern
```

## Decorators
If you want to use a decorator, it cannot be called with parentheses.
#### Good
```moon
myFunc = async ( arg1, arg2, ... ) ->
    print arg1, arg2, ...
```

#### Bad
```moon
myFunc = async( ( arg1, arg2, ... ) ->
    print arg1, arg2, ...
)
```
