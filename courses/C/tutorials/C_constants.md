# Constants

## The ``const`` Keyword
Sometimes when we create data, we may not ever want it to change. By default, any variables you change can be re-assigned to a new value. If you don't want this behavior, you should add the ``const`` keyword before the ``type`` of your variable:
```c
const int PI = 3.14159;
```
This will enforce PI to remain the value that you give it.

It's important that you initialize (assign a value to) your constant **immediately**. The reason is that you can't do this later on after you declare your constant, because it's, well, constant! C's compiler will forbid you to try an alter it later on down the road:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    const float PI;
    PI = 3.14;
    return 0;
}
```
Even the above will throw an error at ``PI = 3.14;``, since we are trying to change a ``const`` after creating it.

## A Briefing on Macros
Another way to declare a ``const`` is to create a ``macro``. It's not important that you know what that means, but right now, know that you can do this:
```c
#include <stdio.h>
#include <stdlib.h>

#define PI 3.14

int main() {
    printf("%f", PI);
    return 0;
}
```
Which is the same thing as using a ``const``, except that this kind of ``PI`` can be accessed throughout the entire file.


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)