# Lua code style guidelines
Plagiarized from [CFC Style Guidelines](https://github.com/CFC-Servers/cfc_glua_style_guidelines)

#
camel_case - variables
blaCase            - functions
BlaCase

func
Func

# Spacing
## Indentation
Use 4 `spaces` are used as one `indent character`.

#### Good
```lua
if cond then
    myFunc()
end
```

#### Bad
```lua
if cond then
  myFunc()
end
```

## Spaces around operators
#### Good
```lua
local x = a * b + c
```

#### Bad
```lua
local x = a* b+c
```

## Spaces inside parentheses and curly braces if they contain content
#### Good
```lua
local x = ( 3 * myFunc() ) + 5
local data = { 5, {} }
```
#### Bad
```lua
local x = (3 * myFunc( )) + 5
local data = {5, { }}
```

## Spaces after commas
#### Good
```lua
myFunc( 10, { 3, 5 } )
```

#### Bad
```lua
myFunc( 10,{ 3,5 } )
```

## Spaces inside square brackets
#### Good
```lua
local value1 = tbl[ 5 ]
local value2 = tbl[ 5 * 3 ]
tbl[ value1 + value2 ] = value3
```

#### Bad
```lua
local value1 = tbl[5]
local value2 = tbl[5 * 3]
tbl[value1 + value2] = value3
```

## Single space after comment operators and before if not at start of line
#### Good
```lua
-- This is a good comment
local a = 1 -- This is also good
```

#### Bad
```lua
--This comment doesn't have a space before it
local a = 1-- This comment starts too close to the 3
```

# Newlines
## Never have more than 2 newlines
#### Good
```lua
local func1, func2, func3 = lib.a, lib2.b, lib3.c

if func1() and func2() then
    func3()
end
```

#### Bad
```lua
local func1, func2, func3 = lib.a, lib2.b, lib3.c






if func1() and func2() then
    func3()
end
```

## Top level blocks should have either 1 or 2 newlines between them
#### Good
```lua
local func1, func2, func3 = lib.a, lib2.b, lib3.c

if func1() and func2() then
    func3()
end
```

#### Bad
```lua
local func1, func2, func3 = lib.a, lib2.b, lib3.c
if func1() and func2() then
    func3()
end
```
