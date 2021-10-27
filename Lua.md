# Lua

## Basic functions

```lua
print("Hello world")
```



## CLI commands

lua -i prog //for debugging (run interactive shell)
dofile("filename.lua")  #in the interactive shell

## Comments

--[[ multiline comment]]

```lua
--[[multiline comment
]]
-- single line comment 
```

## Global Variables

```lua
-- by default non initialized variables return nil
b --> nil
b = 10
b --> 10 
```

## Types

- nil
- Boolean
- number
- string
- userdata
- function
- thread
- table

we can get the type using type(var_name)

## Logic Operators

- or 
- and
- not
- x > y? x : y equavalent (x > y ) and x or y

## Numbers

in lua 1 and 1.0 are equal to distinguish between int and float user math.type(1) and math.type(1.0)

## Arithmetics

- we have + , - , / , *  user ^ for expo
- use // for int division

## Relational Operator

- <  > <=  >= == ~=

## Math Module

```lua
math.sin()
math.pi()
math.max()
math.abs()
math.huge -> infinity
-- all are cumputed in radian
math.deg()
math.rad()
math.random() -- math.random(6) math.random(1,10)
math.randomseed(os.time())
math.floor()
math.ceil()
math.modf() --math.mod(3.3) -> 3 0.3
```

## Useful Print Functions

```lua
print(string.format("%d %d", 3, 15))
```

## Conversion

```lua
math.tointeger(-23.0)
```



## Strings

in lua strings are immutable we cannot change a character inside a string yet we create a new string

```lua
a = "one string"
b = string.gsub(a, "one", "another") 
print(b) --> another string

--lenght os strings with #
a = "Hello"
print(#a) --> 5 returns in byte

--concatenation with ..
"Hello" .. "world"
"hello " .. 3 -- converts 3 to string automatically 

--more 
page = [[
<html>
<head>
<title>An HTML Page</title>
</head>
<body>
<a href="http://www.lua.org">Lua</a>
</body>
</html>
]]
write(page)

--string to number
tonumber("3")
tonumber("100101", 2) --> 37
tonumber("fff", 16) --> 4095

--useful function
string.rep("abc", 3) --repeat
string.reverse("hello world")
string.upper("hello")
string.lower("lower")
string.sub(s, 1, -1) --1 first character -1 last character
-- in lua strings are not 0 based in the sub and -1 is included not exluded 

--more useful functions
string.char(97) --converts to character ascii returns a
string.byte("abc") --converts to ascii returns 97 (a)
string.byte("abc",2 ) --returns 98 (b)
--[[note : A nice idiom is {string.byte(s, 1, -1)}, which creates a list with the codes of all characters in
s.]]


--pattern matching
string.find("hello world", "wor") --> 7 9
string.find("hello world", "asd") --> nil
```



## utf8

string functions don't work on utf9 are reverse, byte, char, lower, upper because they assume 1 byte for each char , string.format exept %c, string.rep string.len string.sub works perfectly 

```lua
utf.len("resume")
utf8.char(114, 233, 115, 117, 109, 233) --> résumé
utf8.codepoint("résumé", 6, 7) --> 109 233
utf8.codes("ajs"') --> code 
```



## Tables

in lua we use tables to represent sets, arrays, packages , objects,etc..
tables in lua are objects

```lua
--we create a table with {}
a = {}
k = "x"
a[k] = 10 --> new entry
a[20] ="great" --> new entry with key 20 
```

### references to tables

```lua
a = {}
b = a --> reference to table
a["x"] = 10
b["x"] --> 10
b["x"] = 20
a["x"] --> 20
a = nil --> only b still refers the table
b = nil --> no table references left
```



### creating multiple entries

```lua
a = {}
for i = 1, 1000 do a[i] = i*2 end
a[9] --> 18
```

we can also use a.x instead of a["x"]

### tables inside tables

```lua 
polypoint = { color="red",
thickness = 2,
points = 2,
{x=0, y = 0},
{x = 1, y = 1},
}
--polyline[1].x --> 0
--polyline[2].x --> 1
--polyline.color --> red
```

we can specify keys like this

```lua
opnames = {
  ["+"] = "add",
  ["-"] = "sub".
}
--more general way
{x=0, y = 0} --> {["x"] = 0, ["y"] = 0}

```

## Sequence and array List

to make array lists in lua we create a table wich the keys are integers

```lua
a = {}
for i = 1, 10 do
  a[i] = io.read()
 end
```

an array list without a hole meaning from 1,, to n with no empty element in the middle is called a sequence , his lenght can be computed as follow with the # 

```lua
--print the lines from 1 to 10
for i = 1, #a do
  print(a[i])
 end
--we can apped to the last element in the sequence with
a[#a + 1] = 11 --append 11 to the end of the sequence
```

### traversing tables

```lua
--use the pais
t = {10, print, x = 12, k = "hi"}
for k, v in pairs(t) do
  print(k, v)
 end
--[[
1	--> 10
k --> hi
2 --> function: 0x42010
x --> 12
the order they appear is random and not known
]]
```

### traversing list

```lua
--use the ipairs
for k, v in ipairs(t) do
  print(k,v)
 end
--[[
in this way lua ensures the order of the list
]]
```



### another way

```lua
--use the # operator
for k = 1, #t do
  print(k, t[k])
 end

```

### table functions

```lua
--table.insert(table, position, value)
t = {}
for line in io.lines() do
  table.insert(t, line)
 end
print(#t) --> number of line read
------------------------------------
--table.remove(table, pos) remove from gives position
table.remove(t)
-----------------------------------
--table.move(a,f,e,t) moves element in table a from index f until e (both inclusive to position t)
```

## Functions

in lua you can return multiple values 

### Variadic functions

a function that can take any number of arguments example

```lua
function add(...)
  local s = 0
  for _, v in ipairs{...} do
    s = s + v
   end 
  return s
 end
print(add(3, 4, 10, 25, 12))
```

### table.pack

this function to know if a variable in a given sequence of parameter is nil

```lua
function nonils(...)
  local arg = table.pack(...)
  for i = 1, arg.n do
    if argv[i] == nil then return false end
   end
  reurn true
 end
```



### using select

```lua
function add(...)
  local s = 0
  for i = 1, select("#", ...) do
    s = s + select(i, ...)
   end
 return s
 end 
```



### table.unpack

```lua
--reverse of table.pack()
print(table.unpack({10,20,30})) -- 10 20 30 
a, b = table.unpack({10,20,30}) --30 is discarted
```

## Standard Library

```lua
io.read()
io.write() --write to current output stream
--change input output steam
io.input(filename)
io.output(filename)
-----
io.lines() -- file lines 
--example
local count = 0 
for line in io.lines() do
  count = count + 1
  io.write(etc...)
 end
```

### io.read

- "a" reads the whole file
- "l" reads the next line dropping the new line
- "L" reads the next line keeping the new line
- "n" reads a number
- "N" reads a number string

### io.open

to open a file 

```lua
io.open() --fopen in c takes a filename and a model string
```

mode string 

- r reading
- w writing 
- a append
- b (optional) binary file 

### assert

to check for io.open() error file use assert

```lua
local f = assert(io.open(filename, mode))
```

if open fails the error msg foes as the second argument to the assert function which shows the message

### reading writing to files

```lua 
local f = assert(io.open(filename, "r"))
local t = f:read("a")
f:close()
--io.stderr:write(msg) write error msg to the error stream
```

### Other operations

- io.tmpfile()  #returns over a temporary file, open in read/write mode
- io.flush #executes all pending writes to a file 
- setvbuf #set buffering mode of a stream
- seek f:seek() #set position of a stream in a file 
- f>seek("set") #reset the position to the begining of the file and returns 0
- f:seek("end") #set the position to the end and return the size 

## Os 

- os.rename
- os.remove
- os.exit
- os.getenv("HOME") --> /home/lua
- os.execute("command_name")
- os.popen()

```lua
function createDir(dirname)
  os.execute("mkdir " .. dirname)
 end

local f = io.popen("dir /N", "r")
local dir = {}
for entry in f:lines() do
  fir[#dir + 1] = entry
 end
```



## Local and Global

by default all variables are global , use local to declare variables inside a function or loop



## if then else

```lua 
if age == 18 then 
  print(18)
 elseif age == 24 then
  print(24)
 else
  print("no age")
 end
```

## While

```lua
local i = 1
while a[i] do
  print(a[i])
  i = i+ 1
 end
```



## repeat

```lua
-- print the first non-empty input line
--same ad do while
local line
repeat
	line = io.read()
until line ~= ""
print(line)
```



## Numerical for

```lua
for var = from, to , step do
  something
 end
```



## Generic for

can have multiple variables which are all updated each iteration

## goto

```lua
while some_condition do
  if some_condition then goto continue end
  local var = something
  some code
  ::continue::
 end

--simple maze
goto room1 -- initial room
::room1:: do
local move = io.read()
if move == "south" then goto room3
elseif move == "east" then goto room2
else
print("invalid move")
goto room1 -- stay in the same room
end
end
::room2:: do
local move = io.read()
if move == "south" then goto room4
elseif move == "west" then goto room1
else
print("invalid move")
goto room2
end
end
::room3:: do
local move = io.read()
if move == "north" then goto room1
elseif move == "east" then goto room4
else
print("invalid move")
goto room3
end
end
::room4:: do
print("Congratulations, you won!")
end
```

## Functions as first class values

functions in lua can be assigned to variables 

```lua
a = {p = print}
a.p("Hello world") --> Hello world
math.sin = a.p -->now math.sin refers to print
math.sin(10, 20) --> 10 20

--
foo = function(x) return x*2 end
--in lua all functions are anonymous functions 
```

## table.sort with higher order function

```lua
network = {
{name = "grauna", IP = "210.26.30.34"},
{name = "arraial", IP = "210.26.30.23"},
{name = "lua", IP = "210.26.23.12"},
{name = "derain", IP = "210.26.23.20"},
}
table.sort(network, function (a,b) return (a.name > b.name) end)
```



## local function

```lua 
Lib ] {}
function Lib.foo(x,y) return x * y end

Lib = {
  foo = function(x,y) return x + y end,
}
Lib.foo = function(x,y ) return x+y end
```



## Pattern Matching

### string.find

```lua
---find the position of the match
s = "hello world"
i, j = string.find(s, "hello") --> 1 5
```

### string.match

```lua
--return the patten if found
date = "Today is 17/7/1990"
d = string.match(date, "%d+/%d+/%d+")
print(d) --> 17/7/1990
```



### string.gsub

```lua
--takes a string, pattern, replace string optinal (limits of substrings)
s = string.gsub("hello world", "world", "nour")
print(s) --> hello nour
```

### string.gmatch

```lua
--[[returns a function that iterates all occurences
of a given pattern in a string ]]
s = "hello nour bou nasr"
words = {}
for w in string.gmatch(s, "%a+") do
  words[#words + 1] = w
end
--[[the pattern %a+ matches one or more words so this will loop all over the words giving nour bou nasr]]
```



### escape

lua users % as an escape sequence in pattern matching 

### Table of patterns

```lua
.										all characters
%a									letters
%c									characters
%d									digits
%g									printable characters except space
%l									lowe case letters
%p									punctuation characters
%s									space characters
%u									upper case letter
%w									alphanumeric characters
%x									hexadecimal digits

```





### Things I need

- player sprites ( I can use any sprite from itch for the demo and replace later)
- ground tiles, obstacles, decorations
- Idle, Run, Jump animations for the player
- Dodge anim can be added later as the prototype can be a simple level
- Menu UI (I guess this is the easiest as no animation needed)
- portrait images if there is a dialog system
- more sprites for the cutscenes 









