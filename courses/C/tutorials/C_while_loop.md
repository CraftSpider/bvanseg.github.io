# The While Loop
A ``while`` loop is extremely similar to a ``for`` loop, but there are two differences:
- They have no ``initialization`` block.
- They have no ``expression`` block.

Which means they are left only with the ``condition`` block.

Consider the following:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    while(1)
        printf("Infinite loop\n");

    return 0;
}
```
Recall from the **Data Types** tutorial that ``boolean`` data (``true`` or ``false``) can also be represented with ``X`` or ``0``, respectively, where ``X`` is any number besides ``0``.

This means that the ``condition`` block for that ``while`` loop above is ``true``, therefore, it is an infinite loop.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)