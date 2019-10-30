# Compile Time vs Runtime
What truly happens when we click those buttons to make our program run? If you don't regard it as important, think again; Because what happens when you click "Build and Run" in your IDE is **Compilation and Execution**.

## Compile Time
First, let's address some computer jargon. What does it mean for a program to "compile"? Well what it means is that your code is run through a program called a **Compiler** (of which there are multiples of these program for C), and that human-readable code is turned into a binary mess that only the computer can read.

**Compilation** is what happens when you "build" your project/program. C's compiler consists of multiple steps during this time:
- Preprocessing the files (Ex. ``#define PI 3.14``, C's preprocessor will replace all text references of ``PI`` with ``3.14``)
- Linking files together (Ex. ``#include <stdlib.h>`` declarations are associated with your code)
- Compiling the C code to some form of ``bytecode`` (binary).
- Outputting the results of compilation (success or failure, with warnings/errors).

If your program fails to compile, it means that something is wrong with your code. In which case, your IDE will be smart enough to warn you, showing the errors in the console and potentially highlighting the line that the C Compiler tells it is erroneous. These are known as **compile-time errors**.

## Runtime
However, if your program has no compile-time errors, it means it can be ran without any foreseen issues from the compiler's view. When you run it, and the program starts, this is known as the **Runtime**.

![Compile-time vs Runtime](https://i.pinimg.com/originals/4c/68/1e/4c681e62914cc2b2b89d0762d7e5ea08.png)

Based on the silly cartoon above, which do you think is more dangerous?

If you thought runtime errors, you'd be correct. Runtime errors are a lot more dangerous, because they can:
- Make your program appear broken to users.
- Be harmful to the computer, if you're working intensively with memory (memory leaks, segfault errors, etc.)

So it is important that your C code be safe. Don't worry *too* much about harming your computer, since  and your computer's operating system takes precautions to ensure that won't happen.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)