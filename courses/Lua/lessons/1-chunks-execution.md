# Chunks and Execution
Lua is a scripting language, so all it needs to start executing code is some code to execute.  
There's no need to write excess code just to convince the computer to run it – just give Lua's interpreter some code, and it will run. Easy!

Most POSIX distributions will have a Lua build in their main repositories. I can personally vouch that Void Linux has Lua 5.3.5 and Pop!_OS has Lua 5.3.3 at-the-ready. These installs should provide a `lua5.3` executable and a `lua` symlink to it, both in `/usr/bin`.

This executable is the Lua interpreter. It is small, but it is mighty, and you mustn't forget that! For these first several tutorials, you should only run code in one of two ways: either save it to a file (the conventional file extension is `.lua`) and give that file as the argument to the interpreter, or call the interpreter itself to start it in interactive mode. For now, I advise using the interactive interpreter because most of the code snippets won't be that long and the nature of an interactive interpreter is to be played with for learning.

---

Of course, I am bound by the limits of tradition. Let's write a Hello World:

```lua
print("Hello, World!")
```

That's it. Actually, you can drop the parentheses if you want to (which will be discussed in more detail in the Functions lesson). In case it isn't obvious enough, the `print` function displays the text it is given, and the quotes provide the text.

## Chunks
Each piece of code (read: sequence of commands and/or statements) in Lua is called a chunk. This could mean a script file, a single line of text, or a line input to the interactive interpreter. There isn't any limit to a chunk's size, and the Lua interpreter is designed to handle massive chunks with ease, which is great for the not-uncommon chunk that clocks in at several megabytes in size.

## The interactive interpreter
When running interactively, every command entered is a chunk, and chunks are executed immediately. If you input the previous hello world example, it will print the text before giving you the chance to provide more code.  
There are three ways to exit the interactive interpreter: use end-of-file (Ctrl+D on POSIX or Ctrl+Z on Windows), call `os.exit()`, or use interrupt (Ctrl+C).

The interactive interpreter will print the value of an expression even when `print` is not explicitly called. For instance, try inputting any of these:

```lua
math.pi/4
"Hhhh" .. "g"
not false
```

You'll see that, because these are just expressions of constant values, they will be evaluated and printed. If these expressions were in a file being executed, you would have to explicitly call `print` to get any output (which should calm your nerves about flooding stdout). Conversely, assignments do not print:

```lua
k = math.pi/4
str = "Hhhh"
bool = not false
```

These will execute but print nothing. That said, you can use `k`, `str`, and `bool` as expressions to print their values.

Here's a trick: you can save code in a file, then call that file with the function `dofile`. For instance, say I have the following code in a file called `func.lua`

```lua
function hypotenuse(a, b)
	return math.sqrt(a^2 + b^2)
end

print("Hypotenuse length function created!")
```

and I ran `dofile("func.lua")` in the interactive interpreter (pedant watch: the interpreter is assumed to have been executed in the same directory as `func.lua` exists). The print statement will execute, and you can now call the `hypotenuse` function.  
Perhaps the opposite of `dofile` is calling the Lua interpreter with the `-i` option and giving it a file. Doing this executes the file and then starts the interactive interpreter without clearing what was done before. In our example, running `lua -i func.lua` would print the text and then start up the interactive interpreter with the `hypotenuse` function still available.

Here's another trick, just for POSIX users: if the **first character** in a Lua script is `#`, then the first line will be interpreted as a comment. Give you any ideas?

```lua
#!/usr/bin/lua
--[[
	code
	goes
	here
]]
```

You can shebang a Lua script! From there, just add execution permisisons (possibly via `chmod +x`) and you can execute the file directly without having to explicitly call the interpreter.

This is the only time the `#` character is used in an abnormal manner (it **does** have another use, which we will see in a later lesson), so don't get used to shell comments!!