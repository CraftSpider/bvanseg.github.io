# Welcome to Lua
*The fast, portable, embeddable, powerful, small FOSS language named after the moon*

## Brief introduction
Lua is an easy-to-learn, lightweight scripting language. It employs strongly- and dynamically-typed multi-paradigm programming with lexical scoping and first-class functions.

### Lua syntax makes sense
Lua's syntax feels somewhat natural to math, and often times pseudocode translates almost directly into Lua script. Understanding Lua is straightforward to anyone with prior experience in another scripting language (especially shell or Python).

### Lua types make sense
Instead of laying down half a dozen types for essentially the same data, Lua wraps it all up into one versatile, effective type. Why have 12 types for integer numbers, plus six types for floating-point numbers? Why have one type to hold a single character, and another type to hold a string of characters? Why can't threads and functions be first-class types? Why have all these types, and still enable more types to be made -- are the existing types not enough? Are arrays types, or pointers, or something else?

Lua answers these questions reasonably: a `number` type for numbers, a `string` type for text, a `thread` type for threads, a `function` type for functions, and a `table` type for lists of data. All first-class, all highly versatile, and if somehow you *still* need more, there's a `userdata` type built just for you.

### Lua paradigms make sense
At its heart, Lua is an imperative language: it will run its chunks, in order, top-to-bottom, left-to-right. Despite the simplicity, Lua's syntax and first-class function and thread types enable some powerful functional and concurrent programming. Clever use of tables and functions that have `self` parameters allow for the emulation of object-oriented programming. For the few of you that are familiar with proper tail calling, you can rejoice that Lua supports this fully (beyond just recursion).

### Lua scoping makes sense
All variables exist. Always. Whether or not it has been declared, you can try to access a variable called `jellyfish` without fear of compiler errors or runtime exceptions. You are always free to assign this variable a value to make it useful, and it will be accessible anywhere, in any script file, within any function. You can declare variables as local, scoping it only to the current level and inner functions.

*But*, once you've had your fun, you can declare a local variable with the same name as a global variable to shadow it. You can do this again within a function to add a new layer, then declare a function in your existing function with the same local variable to add yet another shadow, and scoping will *still* make sense! This is called **lexical scoping**, and once you've mastered it, you can write closures: functions in functions, returned as values, that have access to variables that aren't in-scope anywhere else in your script, and which other languages' garbage collection would sweep away.

---

Hopefully, I've sold you on this marvellous language, and you're ready to dive right in. All of these tutorials are written for Lua 5.3.5, but most of the information applies to any version of Lua 5.0+

Most of these lessons are adapted from Programming In Lua, 4th Edition. I highly advise you buy the book – it goes into far more detail than I do, and was written by someone with *years* of experience teaching Lua. Plus, it is a major source of financially supporting the language.

Cheers!  
—wundrweapon

---

Tutorials:
- [Chunks and Execution](lessons/1-chunks-execution.md)
- [Conventions](2-conventions.md)

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)
