# Typedef
Back in the ``struct``s tutorial, we temporarily glanced over a keyword called ``typedef``. In this tutorial, we're going to elaborate on what that keyword actually does for you.

So by now, you may have noticed a couple of things:
- There is no ``byte`` keyword for a single byte. We are forced to use a ``unsigned char`` to represent a ``byte``.
- There is no ``boolean`` data type without introducing the ``stdbool.h`` header file, which gives us access to ``bool``.
- ``typedef`` in the tutorial on ``struct``s (when used on the definition of a ``struct``) allowed us to omit the ``struct`` keyword prior to creating a new ``struct`` of data.

So what's going on here?

Well, ``typedef`` in plain English means **type definition**. And what does *that* mean? Well, it means it's used to define your own types!

Suddenly it makes sense. This must be how the people who wrote ``stdbool.h`` were able to create a ``bool`` type for us to use.

This also means that ``struct``s we use ``typedef`` on are custom types, which is why we could ignore having to use the ``struct`` keyword **in addition** to the ``struct`` definition's name.

## Let's Create!
So, we don't have a ``byte`` type, right? Then let's fix that!
```c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char byte;

int main() {

    byte exampleByte = 65;

    printf("%d", exampleByte);
    return 0;
}
```
Which outputs: ``65``

Now **that** is powerful. This opens up so many doors to us and what we can create:
```c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char byte;
typedef char* string;

int main() {

    byte exampleByte = 65;
    string exampleString = "Hello, world!";

    printf("%d\n", exampleByte);
    printf("%s\n", exampleString);
    return 0;
}
```
Which outputs:
```
65
Hello, world!
```
The sky is the limit with what you can do with this. Go nuts!

## Typedef or #define?
There are times when you should use ``typedef``, and times where you should use the ``#define`` ``macro``. Suppose you wanted to create ``typedef``s for ``true`` or ``false``. The problem is, these two types have default types of ``1`` and ``0`` respectively. And when creating a ``typedef``, you can **not** initialize them.

So, you're better of just creating ``macro``s for them:
```c
#define true 1
#define false 0
```

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)