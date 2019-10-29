# Scanning Input

Not only can you output data from your program, but you can also await data from an input source, such as a user's console. To do this, we use the ``scanf`` method.

``scanf()`` functions in a similar manner to how ``printf()`` does, format specifiers and all. However, there are a couple of notable differences.

- ``scanf()`` is a little more strict with its formatting.
- Variables you pass into ``scanf()`` must be an address.

Before diving in depth about both points, let's just look at an overview of the function's usage:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int foo = 0;
    scanf("%d", &foo);
    printf("%d", foo);
    return (0);
}

```
In the example above, a variable called ``foo`` is declared. To get the address of ``foo``, we prefix it with ``&``, which is just an operator to get the address of the variable.

``scanf()`` will wait for the user to enter a number. Once they do, that program will output the number they put in, and terminate. So if the user puts in ``42``, then the output will be ``42``.

With ``scanf``, it is expected that the variable you are scanning into has the same type as the format specifier. Otherwise you will get a warning, and some issues further down the road may occur with your variable. Notice that the example above is scanning input as an int (``%d``) into ``foo``, which is of the ``int`` type.

As stated in the previous two points above the example, ``scanf`` is a little strict when it comes to how it parses the input. Consider the following:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int x = 0, y = 0, z = 0;
    scanf("%d-%d-%d", &x, &y, &z);
    printf("%d, %d, %d", x, y, z);
    return (0);
}
```
This particular program scans in 3 ints and assigns them to x, y, and z respectively. Notice the dashes in the template string. These dashes indicate that the user's input MUST be like so:
```
1-2-3
```
Where x is set to 1, y is set to 2, and z is set to 3. If the user does not follow the format specified, the scanning won't happen properly.

It doesn't have to be dashes. It can be whatever format you want them to enter. It could be a time format, for example:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int month = 0, day = 0, year = 0;
    scanf("%d/%d/%d", &month, &day, &year);
    printf("The date is currently %d/%d/%d.", month, day, year);
    return (0);
}
```
Where the user enters ``11/27/2000``, they get an output of:
```
The date is currently 11/27/2000.
```
How you print out the formatted data does **not** need to be the same as how you scanned it in.

### Let's Talk about Addresses
Addresses and what they *actually* are is far outside the scope of this tutorial. For now, you must realize two things about variables:
- Variables are stored in memory. This memory consists of millions of bytes, and each byte has their own address in the machine.
- When you create a variable, it is automatically given an address by C. Depending on the size of the variable, it can be 1 address or span several addresses.
- When you ``&`` a variable, you are requesting the address of that variable. ``scanf`` uses this address so it can know where to store the data it gets from the user. Otherwise, it would have no clue where to put the value.

**"My print functions are printing out crazy numbers! What's happening?!"**
- You are likely forgetting an ``&`` somewhere with your ``scanf``s. Double-check your ``scanf`` calls and make sure you are giving them the addresses of your variables correctly, rather than the variables themselves.

**"I'm trying to use scanf, but for some reason it keeps skipping input. Why is this?"**
- If you are using multiple ``scanf``s in a row, which means your user is pressing ENTER more than once, then that means there are ``\n`` characters leftover from previous ``scanf``s. To ignore those ``\n``s, you can put a space prior to scanning the character or number, like so: ``scanf(" %c", &yourVar);``

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)