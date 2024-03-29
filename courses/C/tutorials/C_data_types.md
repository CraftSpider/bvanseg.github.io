# Data Types

The phrase "data types" refers to the possible ways a computer can group/read a set of bytes, of which that set of bytes can have a varying size depending on the type.

Below, there are some basic data types that are available for usage in C that you should be familiar with. Possible values are not necessary to memorize exactly, but byte size of the types are important, as well as the special behaviors of certain types.

## Basic Types

### Whole Number Types

Type | Bytes | Possible Values
:---: | :---: | :---:
byte | 1 | -128 to 127
short | 2 | -32,768 to 32,767
int | 4 | -2,147,483,648 to 2,147,483,647
long | 4 | -2,147,483,648 to 2,147,483,647
long long | 8 | -9,223,372,036,854,775,807 to 9,223,372,036,854,775,806

**"int and long are the same size?! What gives?"**
- For historical reasons with 32-bit systems (especially with Windows), a long was typically around the same size as an int. The general rule with data is the following:
    - byte <= short <= int <= long
- For higher level languages, these types have a fixed and enforced size. But in C, they can change based on the compiler. Hence, with some compilers, in order to store larger data, you can make a ``long long``.
- It's also worth noting that the above values are SIGNED (negatives and positives). If you wanted them to be unsigned, you can prefix the types with ``unsigned``. Since this will make them only positive, that means their positive maximum doubles in size!
    
    - These bullet points are also true for floating point types, as well.

### Floating Point Types

Type | Bytes | Possible Values
:---: | :---: | :---:
float | 4 | 1.2E-38 to 3.4E+38
double | 8 | 2.3E-308 to 1.7E+308
long double | 12 | 3.4E-4932 to 1.1E+4932

**"Besides size, what else is the difference between these types?"**
- Precision is an important factor for using these types. Generally speaking, ``float``s are relatively inaccurate when it comes to calculations for things such as currency. ``double``s have many more bytes to work with, which means they can afford to be a lot more precise than their ``float`` counterparts. The same can be said between ``double`` and ``long double``.

### Character Type
There's only one character type called ``char``, and its size is 1 byte. Characters can hold any character on your keyboard, and are declared like so:
```c
char foo = 'y';
```
Note that you must use single quotes and not double quotes when declaring a character. This, for example:
```c
char foo = "y";
```
will throw a warning and additionally will **not** print correctly.

### The 'Void' Type
The ``void`` type is used to represent an empty value. These aren't typically used for variables, and are more-so used for functions and wild-card pointers. Don't worry too much about knowing what this does quite yet.

## Other Types
**"What about ``boolean``s in C?"**
- A ``boolean`` data type (which represents ``true`` or ``false``) can be used with ``_Bool`` anywhere within your code.
- Booleans can also be represented as true or false with either 1 or 0, respectively. 0 is generally regarded as ``false``, while any other number besides 0 is ``true``. Any numeric type (even floating point types!) can be used to represent ``true`` or ``false``.
- Additionally, you can do ``#include <stdbool.h>`` at the top of your file and use ``bool`` as you would with ``_Bool``. For example:

```c
#include <stdio.h>
#include <stdbool.h> // Include the boolean header file.

int main() {
    _Bool foo = true; // Create a boolean here.
    bool foo2 = false; // Create a boolean here.

    if(foo == true) { // True.
        printf("foo is true!\n"); // The statement was true, so this will print.
    }

    if(foo2 == false) {
        printf("foo2 is false!\n");
    }

    if(0) {
        printf("I should NOT print!\n");
    }

    if(1) {
        printf("I SHOULD print!");
    }
}
```
which outputs:
```
foo is true!
foo2 is false!
I SHOULD print!
```

**"What about ``string``s in C?"**
- Strings are a complicated "type" and require further analysis in a different tutorial. Right now this tutorial is meant to cover just the basic ones to understand.

**"What about ``NULL``?"**
- ``NULL`` is a special type in relations to pointers, which will be covered later on down the road in those tutorials.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)
