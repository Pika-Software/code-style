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

## Spacing around operators
Spaces must be around operators, operators should not "stick" together.
#### Good
```lua
local x = a * b + c
```

#### Bad
```lua
local x = a* b+c
```

## Spacing inside parentheses
Spaces must be inside parentheses and curly brackets if they contain content.
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

## Spacing after commas
Spaces must be after commas.
#### Good
```lua
myFunc( 10, { 3, 5 } )
```

#### Bad
```lua
myFunc( 10,{ 3,5 } )
```

## Spacing inside square brackets
Spaces must be inside square brackets.
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

## Spacing in comments
Single space after comment operators and before if not at start of line.
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
## Newlines limits
New lines should never have more than 2 empty new lines between them.
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

## Top level blocks
Top level blocks should have either 1 or 2 newlines between them.
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

## Nested blocks
Non top level blocks/lines should never have more than 1 newline between them.
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

## Returns
Returns should have one newline before them unless the codeblock is only one line.
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

## Chunking
Code should be split into managable chunks using a single new line.
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
## Operators
Only vanilla Lua operators should be used in the code.
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

## Comments
Comments should be written in vanilla Lua style.
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

## Continue
Don't use garry's `continue`, which is a flawed implementation that [is prone to errors when used in repeat-until loops](https://wiki.facepunch.com/gmod/Specific_Operators).
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

#### Bad
```lua
local result = 0
for i = 1, 10 do
    if i % 2 == 0 then continue end
    result = result + i
end

print( result ) -- 25
```

# Naming conventions
## Local variables and functions
Local variables and functions should always be written in [lowerCamelCase](https://en.wiktionary.org/wiki/CamelCase).
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

## Global variables and functions
Global variables should be written in [PascalCase](https://en.wiktionary.org/wiki/Pascal_case)/[UpperCamelCase](https://en.wiktionary.org/wiki/CamelCase).
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

## Global library names
Global library names should be written in [snake_case](https://en.wiktionary.org/wiki/snake_case).
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

## Constants
Constants should be written in [SCREAMING_SNAKE_CASE](https://en.wiktionary.org/wiki/screaming_snake_case).
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

## Table keys
By default, table keys should be written in [snake_case](https://en.wiktionary.org/wiki/snake_case). The exception is library functions and values, they should be written in [PascalCase](https://en.wiktionary.org/wiki/Pascal_case)/[UpperCamelCase](https://en.wiktionary.org/wiki/CamelCase). Keys should not start with numbers or special symbols.
#### Good
```lua
tbl.my_awesome_key = 1
tbl["my_awesome_key2"] = 0

my_cool_library.Key = "V293LCB5b3UgZGVjb2RlZCB0aGF0LCBjb25ncmF0dWxhdGlvbnMu"
my_cool_library.Function = function() end
```

### Bad
```lua
tbl.MyAwesomeKey = 1
tbl["my-awesome-key"] = 0

my_cool_library.key = "V293LCB5b3UgZGVjb2RlZCB0aGF0LCBjb25ncmF0dWxhdGlvbnMu"
my_cool_library.function = function() end
```

## Throwaway variables
Use `_` as a variable to "throwaway" values that will not be used.
#### Good
```lua
for _, value in ipairs( lst ) do
    print( value )
end

for _, value in pairs( tbl ) do
    print( value )
end

local _, folders = file.Find( "*", "DATA" )
print( folders )
```

#### Also good solution for functions that returns few arguments
```lua
print( select( 2, file.Find( "*", "DATA" ) ) )
```

#### Bad
```lua
-- index isn't used
for index, value in ipairs( lst ) do
    print( value )
end

-- key isn't used
for key, value in pairs( tbl ) do
    print( value )
end

-- files isn't used
files, folders = file.Find( "*", "DATA" )
print( folders )
```

## Hook naming
Hook naming rules:
- All hook names must be unique.
- Hook names should not start with numbers or special symbols.
- `[ Optional ]` Hook names must contain short phrase that describes the purpose of the hook.
- `[ Tip ]` You can create a local variable with the addon name and use it as/in the hook name.
#### Good
```lua
hook.Add( "EventName", "MyAddon", function() end )
hook.Add( "OtherEventName", "MyAddon", function() end )
hook.Add( "AnotherEventName", "MyAddon", function() end )
hook.Add( "EventName", "MyAddon::Init", function() end )
hook.Add( "EventName", "MyAddon::Player Search", function() end )
```

#### Bad
```lua
hook.Add( "EventName", "", function() end )
hook.Add( "EventName", "__===!!!@22", function() end )
hook.Add( "EventName", "Init", function() end )
hook.Add( "EventName", "EventName", function() end )
hook.Add( "EventName", "AnotherEventName", function() end )
hook.Add( "EventName", "OtherAddon", function() end )
hook.Add( "EventName", "OtherAddon::Init", function() end )
```

# General
## Quotations
You may use single or double quotes, but be consistent.
#### Good with double quotes
```lua
MsgN( "Hello", " ", "World", "!" )
local a, b, c = 1, " ", ""
```

#### Good with single quotes
```lua
MsgN( 'Hello', ' ', 'World', '!' )
local a, b, c = 1, ' ', ''
```

#### Bad, different quotes are used interchangeably
```lua
MsgN( "Hello", ' ', 'World', "!" )
local a, b, c = 1, ' ', ""
```

## Redundant parenthesis
You don't need to put meaningless brackets that don't do anything, except math operations and more complex logic.

#### Good
```lua
if a == b then
    -- do something
end

if not a then
    -- do something
end

if b() then
    -- do something
end

if a then
    -- do something
end

if tbl.key then
    -- do something
end
```

#### Bad
```lua
if ( a == b ) then
    -- do something
end

if ( not a ) then
    -- do something
end

if ( b() ) then
    -- do something
end

if ( a ) then
    -- do something
end

if ( tbl.key ) then
    -- do something
end
```

### Redundant parenthesis may be used if it makes the order of operations clear. The author should use their best judgement
It's important for the author to remember who their target audience is. Not every reader will be good with maths, and it can be helpful to make equations easy to follow.

#### Good
```lua
local result = ( a * b ) + ( c * c )
local result2 = ( ( a * 2 ) + ( b * 2 ) ) - ( c * 2 )

if not ( a and b ) or c then
    -- do something
end

if ( a or b ) and ( c and d ) then
    -- do something
end
```

#### Bad
```lua
local result = a * b + c * c
local result2 = ( a * 2 + b * 2 ) - c * 2

if not a or not b or c then
    -- do something
end

if a or b and c and d then
    -- do something
end
```

## Multiline tables
Elements should begin on the next line and the last line should contain only a closing bracket. Elements inside should be indented once.

#### Good
```lua
local lst = { 1, 2, 3 }

local lst2 = {
    [ 1 ] = 1,
    [ 2 ] = 2,
    [ 3 ] = 3
}

local tbl = {
    a = 1,
    b = 2,
    c = 3
}

local tbl2 = {
    { name = "John", age = 30 },
    { name = "Jane", age = 25 },
    { name = "Bob", age = 40 }
}
```

#### Bad
```lua
local lst = {
    1,
    2,
    3
}

local lst2 = { [ 1 ] = 1, [ 2 ] = 2, [ 3 ] = 3 }

local tbl = { a = 1, b = 2, c = 3 }

local tbl2 = { { name = "John", age = 30 }, { name = "Jane", age = 25 }, { name = "Bob", age = 40 } }
```

## Multiline function calls
Multiline function calls should follow the same guidelines as Multiline tables.
#### Good
```lua
myFunc(
    "First arg",
    secondArg,
    { third, arg }
)
```

```lua
myFunc( "First arg", secondArg, {
    key = 1,
    key2 = 2
} )
```

```lua
timer.Simple( 0, function()
    -- do something
end )
```

#### Bad
```lua
myFunc( "First arg",
    secondArg, { third, arg } )
```

```lua
myFunc( "First arg",
    secondArg,
    { third, arg } )
```

```lua
myFunc( "First arg", secondArg, { third,
arg } )
```

```lua
timer.Simple( 0,
    function()
        -- do something
    end )
```

```lua
timer.Simple( 0, function() -- do something end )
```

## Return early from functions
##### Good
```lua
function example()
    if cond1 then return end
    if cond2 then return end
    if cond3 then return end

    -- do something
end
```

```lua
function example()
    if not ( cond1 or cond2 or cond3 ) then return end
    -- do something
end
```

#### Not too bad, but it adds an extra level of indentation, it's worth using if it's possible not to call `not`
```lua
function example()
    if cond1 and cond2 and cond3 then
        -- do something
    end
end
```

##### Bad, we don't need to make meaningless code pyramids
```lua
function example()
    if cond1 then
        if cond2 then
            if cond3 then
                -- do something
            end
        end
    end
end
```

## Never use semicolons
Semicolons provide no functional value in Lua. While they can be used to delimit table items, a comma is preferred.
#### Good
```lua
local str = "hello world"
print( str )

return str
```

#### Bad, this exclusively makes the code harder to read
```lua
local str = "hello world"; print( str );

return str;
```

## Constants
Use existing constants where possible.
##### Good
```lua
local x = y * math.pi
local radians = math.rad( deg )
```

#### Bad, the meaning of `3.142` may not be immediately clear. It also suffers a loss in precision compared to `math.pi`
```lua
local x = y * 3.142
local radians = deg * ( 3.142 / 180 )
```

## Function calls
Functions must be called a minimum of times necessary for correct code execution. Also, I recommend to avoid calling universal functions if we know exactly what result we are expecting.
#### Good
```lua
local textData1 = {
    pos = { 50, 50 }
}

local textData2 = {
    pos = { 50, 100 }
}

hook.Add( "HUDPaint", "Example", function()
    local ply = LocalPlayer()
    if ply and ply:IsValid() then
        textData1.text = ply:Health()
        textData2.text = ply:Armor()

        draw.Text( textData1 )
        draw.Text( textData2 )
    end
end )
```

#### Bad
```lua
hook.Add( "HUDPaint", "Example", function()
    if IsValid( LocalPlayer() ) then
        draw.Text( {
            text = LocalPlayer():Health()
            pos = { 50, 50 }
        } )

        draw.Text( {
            text = LocalPlayer():Armor()
            pos = { 50, 100 }
        } )
    end
end )
```

# Numbers
## Decimals
Prefer decimals with leading 0s. Lua can understand when a number starts with `.`, but it looks very strange to humans and doesn't make sense.
#### Good
```lua
local float = 0.125
```

#### Bad
```lua
local float = .125
```

## Starting zeros
Prefer whole numbers without leading 0s. Lua numbers can technically be prefixed with as many 0s as you'd like, but in most cases it's completely unnecessary.
#### Good
```lua
local factor = 1024
```

#### Bad, just why?
```lua
local factor = 000001024
```

## Trailing zeros
Prefer decimals with no trailing 0s. There is no sense in adding zeros at the end of decimal numbers, please just don't do it.
#### Good
```lua
local decimal = 0.2
```

#### Bad
```lua
local decimal = 0.200
```

## Negative numbers
In cases where you need negation, use `-` instead of multiplying ( `*` ) by `-1`.
#### Good
```lua
local a = -128
local b = -a
local c = Vector( b, b, b )
local d = -c
```

#### Bad
```lua
local a = 128
local b = a * -1
local c = Vector( b, b, b )
local d = c * -1
```

# Comments
## Useless comments
Good variable and function names can make comments unecessary. Strive for self commenting code. Save comments for complicated code that may not be clear on its own.
#### Good
```lua
for _, ply in pairs( players ) do
    print( ply )

    if ply:Alive() then
        ply:Kill
    end
end
```

#### Bad, the code explains itself without comments
```lua
-- loop through players
for _, v in pairs( stuff ) do
    -- print the player
    print( v )

    -- kill player if player is alive
    if v:Alive() then
        v:Kill()
    end
end
```
