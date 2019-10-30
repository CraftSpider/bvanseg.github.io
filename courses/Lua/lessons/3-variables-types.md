# Variables and Types
There are two kinds of variables in Lua: global and local. Lua has lexical scoping, so local variables can shadow global ones, and this can nest within functions inside of functions, and so on. For some of you, that alone is enough to fully describe Lua variables, but for the rest, don't sweat it too much – you and I are concerned with *global variables* right now, which can be accessed anywhere, any time.

Lua is a strongly- and dynamically-typed language. In other words, variables are not made specifically for one type of data. Instead, values carry their type implicitly, and so the type a variable represents can change on-the-fly. This makes code easy and fast to write, at the cost of needing a runtime. Thankfully, Lua's interpreter is a very small runtime, so it's not much of a concern.

Unlike other languages, a variable needn't be initialized before accessing it; referencing a variable before it gets made simply reveals the first type in Lua: `nil`

## nil
Many languages have values representing null data, and usually it's written `null` or something similar. In Lua, it's `nil`, and when a variable isn't initialized, this is the value it will hold. Notice I said "the value it will hold", not "the value it will be assigned" because any variable that represents `nil` is considered non-initialized. If you want to be smart about RAM usage and help out the garbage collector, simply set your variables to `nil` when you're done with them.

That whole paragraph was about the value `nil`, but nil is also a type. It is the type of the value `nil`, and the only value that can hold the type nil is `nil`. To add to the confusion, `nil` is a reserve word, whereas all other types and most other values in Lua are not.

## boolean
Boolean values are easy in Lua. If you've used any C-like language before, you're already well-acquainted with Lua's boolean type.

Only two possible values exist to hold the boolean type: `true`, and `false`, both of which are reserve words. Honestly, that one sentence is the complete introduction, lecture, and dissertation on Boolean values in Lua. That said, logical operators and truth values will come up in a later lesson, so stay on your toes.

## number
Lua has *one type* for all numeric values. In ye olde days, the number type always represented a floating-point number (in the usual 64-bit implementation of Lua, this would be identical to a `double` in C). As of 5.3, however, a number could be either an integer *or* floating-point. There are some integer values that floating-point numbers can't represent on computers, so this dichotomy allows those numbers to be represented.

Whether a variable will hold an integer or a floating-point (called "float" in Lua) value depends on the variable's assignment and manipulation. In context, a number will bounce back-and-forth between integer and float most of the time (and usually that means integers will be converted to floats. Integers are generally unstable in Lua). Unsurprisingly, this conversion can result in loss of data depending on the conversion made.

## string
Text in Lua holds the string type. String literals are surrounded either by single- or double-quotes, and there is no real difference between them. Lua strings are also format-agnostic, so it doesn't matter how the characters are converted to binary under the hood. There is an official UTF-8 library, but ASCII and UTF-16BE and whatever else is totally acceptable. Also unlike other languages, Lua's strings are highly optimized, so don't be afraid to load a several-megabyte file as a single string and manipulate it!

## table
Some programming languages have more than one type for lists of things. Python immediately comes to mind, with one type for an ordered, mutable list (list); one type for an ordered, immutable list (tuple); and one type for an unordered, mutable list (dict). Conversely, Lua has one type for lists of things, table. Tables do not care what types the items are, how they are accessed (e.g. "is the data at position 2, or do I have to ask for the 'size' data?"), or how often you change them. Tables are made with *table constructors*, lists of data separated by commas and surrounded by braces. For example, here's a table containing the first ten prime numbers, followed by some words:

```lua
{2, 3, 5, 7, 11, 13, 17, 19, 23, 29, "text", "example"}
```

Tables act differently from the list types of other languages, however, so Python programmers be warned: it's not a list object, so don't treat it like one.

## function
Functions are first-class values in Lua! They can be used and passed around in just the same way as any other type can, which is *extremely* powerful, and if you've never used a language with this property, it will rock your world. The name of a function is a variable that you can do whatever you need to do with (use it as parameters to another function, check its type, print it, etc) because the usual function definition is actually just syntactic sugar for making an anonymous function and setting it as a variable. Functions are usually declared like this:

```lua
function name(parameter, list)
	--[[
		code
		goes
		here
	]]
end
```

## thread
Concurrent programming is done via threads. Threads are a complicated topic that will be covered in a later lesson, so don't worry about them right now. Just know that, like any other type in Lua, they are first-class and can be used with just as much flexibility as a string.

## userdata
If somehow the other seven data types aren't enough for you to do your work, you can still count on userdata. This type is reserved for atypical data in C, and so we won't bother with it until the C API lesson quite a long way down the road. We'll deal with *some* userdata values in the I/O lesson, but for now, you can set that aside.

---

And… that's it! Eight basic types, including a null value and C utilities. Honestly, I make it a lot more complicated than it needs to be, largely because I don't want to expect that you're already fluent in another programming language. For whatever aspects of Lua's types aren't straightforward, trust that you'll understand them with practice and a little bit of experimentation.

You can check a variable's type by calling `type` function, which always returns a string containing the variable's type.

```lua
type(var)		--check the type of a variable `var`
type(1.3)		--or a literal. Unhelpfully.
type(type)		--remember: functions are variables
type(type(x))	--regardless of `x`, the result is "string"
```