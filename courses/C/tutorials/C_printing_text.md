# Printing Text

In the previous tutorials, you've often seen ``printf`` being used to print out data. This tutorial aims to cover printing out data to the console, and the types of data you can print out.

## The printf() Function
``printf`` is a function that is included from the ``stdio.h`` (standard I/O header) library file for use in printing to an output stream (printing out the console by default). It can be used a couple of ways:

- Printing out just a string
```c
printf("Hello, world!");
```
outputs: ``Hello, world!``
- Printing out variables
```c
int foo = 2;
printf("I'm foo, and my value is: %d", foo);
```
outputs: ``I'm foo, and my value is: 2``

The latter method of printing is the one that will be elaborated on and emphasized.

``printf`` really stands for "print formatted". "Formatting" basically means making a template string, and then plugging in data to that string, such as variables. Looking back at that second example:
```c
int foo = 2;
printf("I'm foo, and my value is: %d", foo);
```
We can see that printf takes a template string, and uses a ``%d`` to represent ``int`` variables.

What's neat about printf is that it can take as many variables as needed to plug into the template string:
```c
int foo = 2;
int foo2 = 42;
printf("I'm foo, and my value is: %d, but foo2 is: %d", foo, foo2);
```
outputs: ``I'm foo, and my value is: 2, but foo2 is: 42``

We can also do math within the printf function:
```c
int foo = 2;
int foo2 = 42;
printf("With our values combined, we are: %d", foo + foo2);
```
outputs: ``With our values combined, we are: 44``

When C is parsing (or analyzing) the string, it searches for the special character ``%``, which is used to denote a variable that will be shoved into the string. The letters that come after it specify what type of variable to put there.

For your convenience, here is a table of all the formats that ``printf`` can recognize:

Data Type | Format Specifier
:---: | :---:
char | %c
int | %d OR %i
long int | %ld
float | %f
long float | %lf
double | %f OR %e OR %E
long double | %lf
string | %s

Make sure that you match up your format specifiers to your variable data types!

Not only can you specify what type to put into the template string, you can also specify how to print out that data. Consider the following:
```c
#include <stdio.h> 
int main() 
{ 
    char str[] = "test"; 
    printf("%20s\n", str); 
    printf("%-20s\n", str); 
    return 0; 
} 
```
outputs:
```
       test
test       
```
Putting a number before the format specifier will make ``printf`` add X amount of whitespace before/after the data being formatted, where X is the number you specify. This can be useful for formatting text tables in a console.

With floating-point data, you can also **round** the data to however many points you need. For example:
```c
#include <stdio.h> 
int main() 
{ 
    float foo = 0.30000;
    printf("%f\n", foo); //unformatted
    printf("%0.2f\n", foo); //round to 2 decimal points
    printf("%0.4f\n", foo); //round to 4 decimal points
    return 0; 
} 
```
outputs:
```
0.300000
0.30
0.3000
```

**"what the heck was that \n in the code above?"**
- That is what's called an "escape sequence". They are special characters that most programming languages use to present hidden characters you do not see. For example, consider that, when you press TAB or ENTER on your keyboard, while it **looks** like nothing is there, there are actually hidden characters representing your tabs and new lines.
    - With that in mind, pressing ENTER creates a ``\n``, which starts a new line. That's how the output above is on separate lines.
    
Here are a list of escape characters you can use in formatting:

Escape Sequence | Usage
:---: | :---:
\n | Starts a new line
\b | Goes back a space
\t | Horizontal tab
\v | Vertical tab
\\\ | Represents a backslash
\' | Represents a single quote
\" | Represents a double quote
\0 | Represents a NULL

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)