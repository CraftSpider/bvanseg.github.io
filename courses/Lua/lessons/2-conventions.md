# Conventions
Identifiers (variable names) can be any sequence of letters, numbers, and underscores, as long as they don't begin with a digit.  
It is advised that you avoid all-caps identifiers that begin with an underscore (e.g. `_VARIABLE`) because these are expected to serve special purposes, and some have preset values that shouldn't be overridden. Also, a standalone underscore is a valid identifier, but that tends to be reserved for variables that need to be declared (such as in for loops) but go unused.

## Reserve words
Lua, like most languages, has reserve words. These cannot be used as identifiers and the interpreter will treat them as syntax:

```lua
and		break	do		else		elseif
end		false	for		function	goto
if		in		local	nil			not
or		repeat	return	then		true
until	while
```

That said, Lua is case-sensitive, so while `if`, `then`, and `else` are all reserved, `If`, `THEN`, and `elsE` are not. PL/1 fans, this is your time to shine!

```lua
if If then THEN = elsE else elsE = THEN end
```

(Please, do not write code that bad, even if it runs…)

## Comments
Lua takes a **very** abnormal approach to comments. Most programmers are familiar with C-like comments (prefixed with `//` or circumfixed with `/* */`) or shell comments (prefixed with `#`, also called Pythonic). Lua comments, however, start with `--` or are circumfixed with `--[[ ]]`  
Yes, I'm serious.

```lua
--line comment

--[[
	ranged
	comment
]]
```

Because of the `--` line comment prefix, it is common to use `-->` to show what a chunk might print. This is done in the Programming In Lua textbook, and will be done from here on in these lessons.

Despite the madness, there is good news – the block comment toggling trick from C-like comments still works in Lua, though it looks a little different. Ranged comments in Lua *must* begin with `--[[` and end with `]]`, and the only exception is adding a number of equals signs in between those brackets (which will be discussed more in the Strings lesson). Because of this specificity, it is common to circumfix code like this:

```lua
--[[
	disabled
	code
	block
--]]
```

By adding the `--` to the end of the ranged comment, the code block can be toggled. To enable the code, just add one more `-` to the beginning of the ranged comment. Because there are now three instead of two dashes (per the strict definition), the first line is now just a line comment, and the end of the ranged comment gets interpreted that way, too. Remove the extra dash to disable the code again.

```lua
---[[
	reenabled
	code
	block
--]]
```

That all said, it's worth nothing that this isn't the only way to use triple-dashed ranged comments, but that doesn't need to be explained for a long time.

## Semicolons
You may have noticed in the previous lesson that Lua does not need semicolons at the end of statements, as some other languages do. Much like Python, these semicolons are allowed but optional, and most Lua developers don't use them at all. Sometimes it feels nice to put two statements on the same line, and a semicolon can help to separate them, but the interpreter actually doesn't need that! All of these lines are identical as far as the interpreter is concerned:

```lua
a = 4 b = 5
a = 4  			b = 5
a = 4; b = 5
```

(You might have noticed I teased Lua's liberal spacing, too. So long as whitespace separates reserved words, the interpreter can usually just handle whatever terrible indentation you give it.)