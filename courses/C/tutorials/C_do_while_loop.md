# The Do-While Loop
The ``do-while`` loop is essentially the same as the ``while`` loop. The only difference is that its overall structure is flipped:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    do {
        printf("Infinite loop\n");
    } while(0);
        

    return 0;
}
```
Why the funky, backwards syntax? Because this type of loop will **always** run at least one time before the ``condition`` block is checked. In the case above, the ``do-while`` loop **does** run at least once, but since the condition is ``false``, it does not run a second time, and the program ends.

As can be expected, the ``do-while`` loop runs fine without brackets:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    do
        printf("Infinite loop\n");
    while(0);
        

    return 0;
}
```

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)