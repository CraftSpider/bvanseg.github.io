# Pass by Value vs Pass by Reference
When we "pass" data to functions in C, the variables we put into the functions are copied, and then used in the function. This is both a good and bad thing:
- It's good, because the raw data we put into our function won't change after the function is done executing.
- It's bad, because in certain instances, we **want** our data to change after it has gone through the function.

Hearing the phrase "pass by reference vs pass by value" might be confusing, so let's settle what each part of the phrase actually means.

## "Pass by Value"
This means that data we pass into functions is copied just for the use of that function, and then the copy is discarded when the function finishes. All data in C is pass-by-value.

## "Pass by Reference"
This is where things get interesting. We have just learned about ``pointer``s. Even though when we pass a ``pointer`` into a function, a copy of an address is still just the address. So we can use that address to find the location in memory of the variable we passed into the function.

In this regard, ``pointer``s can be used to "pass by reference", where the address of a variable (``pointer``) is the **reference** to that variable in memory.

So the next time you hear both of these phrases, just recall this tutorial. This tutorial is just a clarification on the meaning of these phrases, since you may often hear them used in business settings or even in formal classroom settings.


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)