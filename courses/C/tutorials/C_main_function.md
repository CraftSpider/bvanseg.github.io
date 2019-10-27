# Main Function

In C, the ``main function`` is the function in which your program starts running. It looks a little something like this:

```c
#include <stdio.h>

int main() {
    printf("Hello, world!");
    return 0;
}
```
To  better understand this code, let's break it down line-by-line:

 ``#include <stdio.h>`` - A library file that is built presumably bundled with the compiler. This allows our C program to safely use ``printf``.
 
 The next line after that is just empty space. C does not care about new lines or extra white space.
 
``int main() {`` - This is the start of a function. It has a **return type** (``int``) and a **name** (also known as an identifier, ``main``). Its body is then opened with the ``{``.

- A function like this is special to C; C will specifically look for this function when compiling your program, and start building your program from there.

``printf("Hello, world!");`` - ``printf`` is another function, used to print out given output to the console. In this case, we are printing ``Hello, world!`` to the console.

``return 0;`` - This tells the function to exit with a value of 0. Any code in the function after this line will **not** execute. Since there is no more code after this line, the program simply ends.

- Because the ``main`` function is special, you can omit the ``return`` line and C will not complain about it being missing. Like so:
```c
int main() {
    printf("Hello, world!");
}
```
- returning a value of ``0`` from the ``main`` function is generally a signal to C that the program ran without error. If any other number is returned, such as ``-1``, it's treated as if the program had an error while running.

``}`` - This is the end of the function's body. If this is reached, the function is done executing.

After that line, the end of the file is reached, there is no more code to execute.
 

[Home](https://bvanseg.github.io)