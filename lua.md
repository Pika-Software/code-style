# Lua code style guidelines
Plagiarized from [CFC Style Guidelines](https://github.com/CFC-Servers/cfc_glua_style_guidelines)

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

## Non top level blocks/lines should never have more than 1 newline between them
#### Good
```lua
function example( a, b, c )
    local result = ( a + b ) ^ c
    local result2 = result % c

    print( result, result2 )
end
```

#### Bad
```lua
function example( a, b, c )
    local result = ( a + b ) ^ c
    local result2 = result % c


    print( result, result2 )
end
```

## Returns should have one newline before them unless the codeblock is only one line
#### Good
```lua
function example1( a, b )
    local c = a + b
    local d = a - b

    return c, d
end

function example2( a, b )
    return a + b, a - b
end
```

#### Bad
```lua
function example1( a, b )
    local c = a + b
    local d = a - b
    return c, d
end
```

## Code should be split into managable chunks using a single new line
#### Good
```lua
function example( a, b, c )
    if not a then
        a = 0
    elseif a > 100 then
        a = 100
    elseif a < 0 then
        a = 0
    end

    if not b then
        b = 0
    elseif b > 1 then
        b = 1
    elseif b < 0 then
        b = 0
    end

    if not c then
        c = 1
    elseif c > 10 then
        c = 10
    elseif c < 1 then
        c = 1
    end

    return a, b, c
end
```

#### Bad, far too dense and difficult to read at a glance
```lua
function example( a, b, c )
    if not a then
        a = 0
    elseif a > 100 then
        a = 100
    elseif a < 0 then
        a = 0
    end
    if not b then
        b = 0
    elseif b > 1 then
        b = 1
    elseif b < 0 then
        b = 0
    end
    if not c then
        c = 1
    elseif c > 10 then
        c = 10
    elseif c < 1 then
        c = 1
    end
    return a, b, c
end
```

# GLua Additions
## Use only vanilla Lua operators
#### Good
```lua
if not b then
    return "definitely not b"
end

if i ~= a then
    return "i is not equal to a"
end

if a and b then
    return "a and b are true"
end

if a or b then
    return "a or b is true"
end
```

#### Bad
```lua
if !b then
    return "definitely not b"
end

if i != a then
    return "i is not equal to a"
end

if a && b then
    return "a and b are true"
end

if a || b then
    return "a or b is true"
end
```

## Use only vanilla Lua comments
#### Good
```lua
-- This is a comment
local a = 1

-- This is another comment
local b = 2

--[[


    One big comment


]]
local c = 3
```

#### Bad, gmod comments aren't recognized by standard Lua highlighting
```lua
// This is a comment
local a = 1

/* This is another comment */
local b = 2

/*


    One big comment


*/
local c = 3
```

## Don't use garry's `continue`
#### Good
```lua
local result = 0
for i = 1, 10 do
    if i % 2 ~= 0 then
        result = result + i
    end
end

print( result ) -- 25
```

#### Also good solution with goto, where goto replaces continue
```lua
local result = 0
for i = 1, 10 do
    if i % 2 == 0 then goto skip end
    result = result + i
    ::skip::
end

print( result ) -- 25
```

#### Bad, garry's `continue` is a flawed implementation that [is prone to errors when used in repeat-until loops](https://wiki.facepunch.com/gmod/Specific_Operators)
```lua
local result = 0
for i = 1, 10 do
    if i % 2 == 0 then continue end
    result = result + i
end

print( result ) -- 25
```

# Naming conventions
## Local variables and functions should always be written in [lowerCamelCase](https://en.wiktionary.org/wiki/CamelCase)
#### Good
```lua
local myVariable = "hello world"
local myFunction = function()
    print( myVariable )
end

myFunction() -- "hello world"
```

#### Bad
```lua
local MyVariable = "hello world"
local MyFunction = function()
    print( MyVariable )
end

MyFunction() -- "hello world"
```

## Global variables should be written in [PascalCase](https://en.wiktionary.org/wiki/Pascal_case)/[UpperCamelCase](https://en.wiktionary.org/wiki/CamelCase)
#### Good
```lua
MyLittleGlobalVariable = 14
MyLittleGlobalFunction = function()
    print( MyLittleGlobalVariable + 10 )
end
```

#### Bad
```lua
my_little_global_variable = 14
my_little_global_function = function()
    print( my_little_global_variable + 10 )
end
```

```lua
mylittleglobalvariable = 14
mylittleglobalfunction = function()
    print( mylittleglobalvariable + 10 )
end
```

## Global library names should be written in [snake_case](https://en.wiktionary.org/wiki/snake_case)
#### Good
```lua
my_cool_library = {}
module( "my_cool_library" )
```

#### Bad
```lua
MyCoolLibrary = {}
module( "MyCoolLibrary" )
```

```lua
mycoollibrary = {}
module( "mycoollibrary" )
```

## Constants should be written in [SCREAMING_SNAKE_CASE](https://en.wiktionary.org/wiki/screaming_snake_case)
#### Good
```lua
ENUM1 = 0
ENUM2 = 1

local LOCAL_ENUM1 = 2
local LOCAL_ENUM2 = 3
```

#### Bad
```lua
enum1 = 0
enum2 = 1

local localEnum1 = 2
local localEnum2 = 3
```
