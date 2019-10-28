# The For Loop
Sometimes when we program, we take a step back and notice that we have a lot of repetitive code. Consider this repetitive code:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int counter = 0;

    printf("counter is now %d\n", counter);
    counter++;
    printf("counter is now %d\n", counter);
    counter++;
    printf("counter is now %d\n", counter);
    counter++;
    printf("counter is now %d\n", counter);
    counter++;
    printf("counter is now %d\n", counter);
    counter++;
    printf("counter is now %d\n", counter);
    counter++;

    return 0;
}
```
Which outputs:
```
counter is now 0
counter is now 1
counter is now 2
counter is now 3
counter is now 4
counter is now 5
```
So looking at this, how can we reduce this long block of code? Well, we can use a ``for`` loop to simplify it:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0; counter < 6; counter++) {
        printf("counter is now %d\n", counter);
    }

    return 0;
}
```
This code has the same output as the code above. Let's break that ``for`` loop down step by step, and really understand what it means.

``for(`` - We declare our ``for`` loop, and open a pair of parentheses.

``int counter = 0;`` - Counter is declared in the ``initialization`` block. This is where we can create multiple variables separated by ``,`` to be used in the loop. Note that variables created here can not be used outside of the loop.

``counter < 6;`` - This is known as the ``condition`` block. This is like an ``if`` statement that is checked every time right before the loop iterates (that is to say, every time it loops). In this scenario, the loop will stop executing when ``counter`` is no longer less than ``6``.

``counter++)`` - This is the final block, the end being denoted by the ``)``. This block is known as the ``expression`` block. **Code here is executed every loop iteration.** You can do any expression here, such as ``counter++``, which would allow our loop up there to eventually end. You can even call functions there!

You can do almost anything in that ``expression`` block, such as ``counter *= 2``, ``counter--``, so on and so forth. So long as it is an **expression**, it's fine.

## Omitting For Loop Components
These components of the for loop are not required at all. You can omit some of them, like so:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0; counter < 6;) {
        printf("counter is now %d\n", counter);
    }

    return 0;
}
```
Now that ``counter`` is no longer changed, it will be forever ``0``. Which means the ``condition`` block will never be false. Which means the loop will execute infinitely.

You get the same infinite loop issue with this code, as well:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0;;) {
        printf("counter is now %d\n", counter);
    }

    return 0;
}
```
Notice that, even through the statements themselves are not required, the semicolons still very much are required.

And this would be just a straight-up infinite loop:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(;;) {
        printf("Infinite loop!\n");
    }

    return 0;
}
```

Even the body is not required:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(;;);

    return 0;
}
```
Though, it's unclear why anyone would ever need a loop that looks like that.

## Keeping Code Clean
Like ``conditional`` statements, you can also omit the brackets if the loop is only doing work on one statement:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0; counter < 6; counter++)
        printf("counter is now %d\n", counter);

    return 0;
}
```
And it still works just as well.

## Loop Control
Sometimes we may want to prematurely exit the loop, or, skip to the next iteration.

To exit the loop, we can use the ``break`` keyword anywhere within the loop:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0; counter < 6; counter++) {
        if(counter == 3)
            break;

        printf("counter is now %d\n", counter);
    }

    return 0;
}
```
This will cause the loop to only print up until ``counter`` is ``3.``

If we want to skip the loop when ``counter`` is a certain number, we can also do this:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    for(int counter = 0; counter < 6; counter++) {
        if(counter == 3)
            continue;

        printf("counter is now %d\n", counter);
    }

    return 0;
}
```
This will skip that iteration of the loop when ``counter`` is equal to ``3``. However, notice that it will still keep executing for when ``counter`` is ``4`` and ``5``.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)