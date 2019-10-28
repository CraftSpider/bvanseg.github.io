# Switches
Switches are a different take on ``if`` statements, where they take a variable and compare it against certain values.

Here is an example of a ``switch`` statement:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    switch(age) {
        case 18:
            printf("You are 18 years old!");
            break;
        case: 19:
            printf("You are 19 years old!");
            break;
        case: 20:
            printf("You are 20 years old!");
            break;
        default:
            printf("You are NOT 18, 19, or 20 years old!");
    }
    return 0;
}
```
Immediately, we notice a huge number of differences from the ``if`` statement. Let's break it down line-by-line.

``switch(age) {`` - The opening of the ``switch`` statement. It takes one and **only** one parameter, which is a variable you are going to switch on.

``case 18:`` - Equivalent to ``if(age == 18)``

``printf("You are 18 years old!");`` - Prints if the case is true.

``break;`` - Exits the entire ``switch`` statement. Unlike the ``if`` statement, the ``switch`` statement does not automatically end when one conditional statement is handled. Were this break not here, every ``case`` below it would execute, until it hits a ``break;``. This is known as **falling through** or **cascade execution**.

skipping down to the ``default``...

``default:`` - This is the equivalent of an ``else`` block. You don't need a break here if it's the last case in the ``switch`` chain.

The code above outputs the following: ``You are 19 years old!``


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)