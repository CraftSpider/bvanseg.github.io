# Scopes
Scopes in programming languages are, very simply a pair of ``{}`` in which all code inbetween them are considered their own scope.

Why are scopes important? Well, let's consider the following.
```
#include <stdio.h>
#include <stdarg.h>

int main()
{
    int foo = 0;

    {
        foo = 1;
        int bar = 2;
    }

    bar = 3;
}
```

Looking at this in terms of scopes as defined above, we see two scopes. The main function's scope, and the scope inside of that.

We define our ``foo`` variable within the main function's scope. In the scope nested within the function, we set ``foo`` equal to ``1``. In that inner scope, we create a new variable called ``bar``, and set it equal to ``2``.

Here comes the interesting part. Outside of the scope where ``bar`` was created, we set ``bar`` to ``3``. However, if we try to build and run this program, we get an error!

Why is this? What's happening? It's actually simple:
- The data of higher scopes is visible to lower scopes.
- The data in lower scopes is NOT visible to higher scopes.

Therefore, when we try to set ``bar`` equal to ``3``, we can't. Because ``bar`` does not exist in that scope.

However, what we're doing with ``foo`` is just fine, because ``foo`` is defined in a scope and then changed to ``1`` in a scope below the one it was defined in. Nested scopes can see the variables declared in the scopes above them.

In terms of vocabulary, we would say the scope ``bar`` is located in is relative to the higher scope of the function ``main``, relatively. In other words, nested scopes are also known as local scopes.

Moving forward, we shall refer to these pairs of brackets as scopes more often.

here is something that might interest you:

```c
#include <stdio.h>
#include <stdarg.h>

int higherFoo = 5;

int main()
{
    int foo = 0;

    {
        foo = 1;
    }

    printf("%d\n", foo);
    printf("%d\n", higherFoo);

    higherFoo = 4;

    printf("%d", higherFoo);
}
```

A variable outside of a function? What is this blasphemy?!

Well, ``higherFoo`` is actually in a default scope for files, which is referred to as a global scope. ALL scopes following that variable (functions and all) will be able to see that variable. Hence, we can change ``higherFoo`` within the main function without issue.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)