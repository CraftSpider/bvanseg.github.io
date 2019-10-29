# Functions
After adding an extensive amount of code in the ``main`` function, it can become quite an eyesore to have the entirety of your code crammed between two particular brackets. Fortunately in C, we can create more functions than just the ``main`` function to organize our code.

Before diving head-first into functions, first we should establish what functions even *are*. So:
- A function in C is a block of code that has a ``type`` it can return, a name (identifier), parameters, and a body (``{}``), by which said body performs a certain task with said parameters and then spits (``return``s) out a result that is equal to the ``type``.

## Functions By Example
The best way to demonstrate functions are by example:
```c
#include <stdio.h>
#include <stdlib.h>

int sum(int a, int b) {
    return a + b;
}

int main()
{
   printf("Sum: %d", sum(2, 3));

   return 0;
}
```
Which outputs: ``Sum: 5``


So let's walk through what's going on here. We are doing ``printf`` as per the usual, but instead of passing a variable to ``printf`` to print out, we have instead put a function. This gives a sudden realization that, ``printf`` can accept not just variables or values, but expressions in general (which a **function call** is, an expression).

Before the main function, we have declared a function called ``sum``. This function **requires** two parameters, since our function declaration specifies two (variables/values that it needs to be given). In this case, we give it ``2`` and another ``3``. While our function only has 2 parameters, **be aware that a function can have as many parameters as you like.**

Inside the function, it corresponds the input of the function (``2, 3``) in order to the names of the parameters declared in the function (In other words, ``int a`` is now ``2``, and ``int b`` is now ``3``).

Then, again within the function, it returns the sum of ``a`` and ``b``  (``a + b``). C then jumps out of the function, **back** to our ``printf``, and now uses the sum (``5``) to print in place of ``%d``.

If this still seems confusing, think of functions in terms of mathematics. Remember ``f(x)``?:
```c
#include <stdio.h>
#include <stdlib.h>

int f(int y) {
    return y*y;
}

int main()
{
    int x = 3;
    printf("x squared is: %d", f(x));

   return 0;
}
```
Which outputs: ``x squared is: 9``

Ah, so now a function becomes a little more familiar. **However**, unlike mathematics, our functions here are not related to pure computational math. They can be, but, we can do whatever we want within that function just as we can in ``main``.

## Further Examining Functions
So, we can create functions like the one seen above. But what does that *mean*? What does it mean when we say ``int`` before the function name? What does it mean when we ``return`` that value?

When we specify the ``type`` of a function, we are telling C that "this function should produce this type of result". Therefore, when we ``return`` a value from the function, it must be an expression, variable, or value equal to that type. So an int function requires an int to be returned, a float function requires a float to be returned, and so on.

Look back at the example above. You may notice that the parameter for the function is ``int y``, and yet in the ``main`` function, we have another ``int x`` that is set to ``3``, and passed into the function. 
- **"Are they the same?"** The answer is **no**, they are not the same. That also means that **setting the variable to a value in the function does NOT change it in the ``main`` function**. They exist in completely different scopes that aren't related in any way. Any data you pass into a function **lose** their original name, and take on a different name based on the function. In the example above, ``x`` is passed into function ``f``, which takes the value and assigns it to a new int variable called ``y``. Notice that the two variables must be the same ``type``, in this case ``int``.

## Function Returns
So now we have a good grasp on what this stuff means. What can we do with it? Well, a function can ``return`` a value. It is therefore possible to capture this value into a variable, like so:
```c
#include <stdio.h>
#include <stdlib.h>

int f(int y) {
    return y*y;
}

int main()
{
    int x = 3;
    int z = f(x);
    printf("x squared is: %d", z);

   return 0;
}
```
Which outputs: ``x squared is: 9``

Pretty neat, huh?

Now, looking at this function:
```c
int f(int y) {
    return y*y;
}
```
When we ``return`` from it, what we are telling C to do is jump out of the function with a value that we can make use of. Therefore, any code after a ``return``, **ANY** code at all, will not execute.
```c
int f(int y) {
    return y*y;
    printf("y: %d", y); /* We return before this, so this code will never be reached. This known as called "dead code", aka, code that never has a chance to run, ever. */
}
```
Yes, this also means that ``return`` stops a function dead in its tracks, even if it is inside a loop:
```c
int f(int y) {
    for(;;) { /* This is normally an infinite loop. HOWEVER, because of the return function, the loop is canceled, and the function is terminated with the value 9. */
        return y*y;
    }
}
```

## Void Functions
**"But what if we don't want the function to return anything?"**
- Good question! There is a special type for a function that doesn't need to return anything, and that type is called ``void``. ``void`` functions do not need a ``return`` call at the end of them. Additionally, because these functions can not return anything, they also can not be assigned to variables.
    - **"But if that's true, how can the ``main`` function get away with no ``return`` type?"**
        - The ``main`` function has special privileges that other functions don't, because it is the function that starts the program. Even if you don't ``return`` a number in ``main``, C actually adds ``return 0;`` at the bottom of the function for you during compile time.

## Chain Calling
Like functions in mathematics, we can also call functions inside of functions. Continuing with our previous example:
```c
#include <stdio.h>
#include <stdlib.h>

int f(int y) {
    return y*y;
}

int g(int a) {
    return a + 3;
}

int h(int q) {
    return q - 4;
}

int main()
{
    int x = f(g(h(3)));;
    printf("x squared is: %d", f(x));

   return 0;
}
```
Which outputs: ``x squared is: 16``

Do realize that, when you pass a function into a function, it is expected that the function being passed in has the same type as the parameter of the function you're passing it into. In other words, our function ``g`` takes an ``int`` parameter, and our other function ``h`` returns an ``int``, therefore, we can pass ``h`` into ``g`` as a parameter.

## Recursive Functions
There is an unofficial type of "loop" that we have neglected to talk about until now. That "loop" turns out to actually be a recursive function. What does that look like? Something like this:
```c
#include <stdio.h>
#include <stdlib.h>

int someFunction(int y) {
    if(y > 42) return y;
    return someFunction(y * y);
}

int main()
{
    int x = someFunction(3);
    printf("x is: %d", x);

   return 0;
}
```
Which outputs: ``x is: 81``
Notice that we are calling the same function within itself. This property is known as **recursion**. Without that check (``if(y > 42) return y;``) in the function, the recursive function would execute forever, just as an infinite loop would. To better understand what's going on here, let's break it down:

- We first call ``someFunction(3);`` in the ``main`` function when setting the value of ``x``. So we jump to ``someFunction``, and presume ``y`` to be ``3``. 3 is not bigger than 42, so we continue to ``someFunction(y * y);``, which is actually ``someFunction(3 * 3);`` 

- We move **back** to the top of the function. ``y`` is now ``9``. Is 9 bigger than 42? Nope. Keep going. We hit ``someFunction(y * y);`` Well this time, y is 9. So we call ``someFunction(9 * 9);``

- We move **back** to the top of the function. ``y`` is now ``81``. Hey, this time ``y`` is bigger than ``42``! That means that check will be ``true``, which means we return with ``y`` still as ``81``. But remember, our last position before we jumped into the 3rd level of the function was the ``return`` at the end of the function. So we jump back there. Then we return from there, and then from the next level, until we are **finally** back at where we called the function in the first place, when setting ``x`` to it. ``x`` is now ``81``, and therefore, the output checks out and is logically sound!

## Function Prototypes
A watchful eye may have noticed that the functions defined in all of the examples so far have been *above* the ``main`` function. This was intended design.

You see, when C compiles your code, it reads the file from top to bottom. So imagine you have code like this:

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
   foo();
   return 0;
}

int foo() {
    printf("Hello, world!\n");
}
```
This code will actually fail to compile. Why? Well, the reason is because C reads the file line by line.

So what happens when it gets to the line ``foo();``? It doesn't know the function ``foo`` exists, **yet**. But it throws an error regardless. So how do we let C know that the function *does* exist, and  when it encounters references to it? We use **prototypes**.

A **prototype** is a declaration of a function, but not quite a definition of its body or what the function does:
```c
#include <stdio.h>
#include <stdlib.h>

int foo(); // This is the prototype.

int main()
{
   foo();
   return 0;
}

int foo() {
    printf("Hello, world!\n");
}
```
Now, when C reads the file line-by-line when compiling, it wil see this prototype, and any references of the function from that point onward will be fine with C.

If ``foo`` had a parameter or multiple parameters, then you would need to also specify **AT LEAST** type of the parameters used:
```c
#include <stdio.h>
#include <stdlib.h>

int foo(int, int, int); // This is will still work.

int main()
{
   foo();
   return 0;
}

int foo(int x, int y, int z) {
    printf("Hello, world!\n");
}
```
Alternatively,
```c
int foo(int a, int b, int c);
```
Prototypes can put names to the function's parameters, but note that these names do not need to be the same as the function's declaration and are purely for reading purposes.


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)