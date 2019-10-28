# If, Else-If, and Else Statements
When we want the program to make a choice, we use logical statements to control the flow of the program's execution. Such logical statements or controllers are called if-elseif-else statements.

## If Statements
Let's unpack that by starting with the ``if`` statement. An ``if`` statement is a block of code that takes a condition, and then if that condition is ``true``, the block of code will execute. Here's a demonstration. Suppose we have some imaginary person with an age, and their age is 17. We can do checks on their age to print out some information based on certain conditions, like below:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 17;

    if(age < 18) {
        printf("You are not yet an adult!");
    }
    return 0;
}
```
Which outputs: ``You are not yet an adult!``

Looking at the condition in the ``if`` statement, we notice that is indeed true that the ``age`` variable is less than 18. So, the block of code will run.

## Else Statements
Now, what if we want to print something out even if that first statement is not true? That's where the ``else`` statement comes into play. The ``else`` statement is a a "last resort" block of code that will be handled if all of the other previous checks are false. They **must** accompany an ``if`` statement.

Examine the following:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18) {
        printf("You are not yet an adult!\n");
    }else {
        printf("You are an adult!\n");
    }
    return 0;
}
```
Which outputs: ``You are an adult!``

Notice that ``age`` is now ``19``. The first condition will most certainly be false, since 19 is not greater than 18. So, the computer will use the fallback ``else`` statement since the first one failed.

## Else-If Statements
The above program is pretty good. It has logic that models a real-world scenario in which we may need to use a user's age to execute different blocks of code. But we can't have 2 ``if`` statements together, nor can we have two ``else`` statements together, so how do we add more possible paths? The answer is ``else-if`` statements. Consider the following:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18) {
        printf("You are not yet an adult!\n");
    } else if(age < 21) {
        printf("You are an adult, but you can not legally drink alcohol yet!\n");
    }else {
        printf("You are an adult and can do everything legal!\n");
    }
    return 0;
}
```
Which outputs: ``You are an adult, but you can not legally drink alcohol yet!``

Now our program is becoming more and more refined! Now that it has 3 logical branches, it can handle more scenarios that the user might throw at it. But, if you keep doing this with more and more conditions, you start to notice odd behavior, such as in this alteration of the program:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18) {
        printf("You are not yet an adult!\n");
    } else if(age < 21) {
        printf("You are an adult, but you can not legally drink alcohol yet!\n");
    }else if(age < 62) {
        printf("Not only can you not drink, but you are also ineligible for social security!\n");
    }else {
        printf("You are an adult and can do everything legal!\n");
    }
    return 0;
}
```
Which outputs: ``You are an adult, but you can not legally drink alcohol yet!``

Hm... what's going on? The two ``else-if`` statements are true, so why is it only printing the first one?

The reason is simple, actually: In C (and most programming languages), ``if-elseif-else`` blocks only execute a single condition. C is reading those conditions line-by-line, and when it gets to ``age < 21``, it executes that code, but then skips all the way down to ``return 0;``, which ends the program. So how can this be fixed? Well, we can **nest** our ``if`` statements.


## Nesting Conditional Statements

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18) {
        printf("You are not yet an adult!\n");
    } else if(age < 21) {
        printf("You are an adult, but you can not legally drink alcohol yet!\n");
        if(age < 62) {
            printf("Not only can you not drink, but you are also ineligible for social security!\n");
        }
    }else {
        printf("You are an adult and can do everything legal!\n");
    }
    return 0;
}
```
Which outputs:
```
You are an adult, but you can not legally drink alcohol yet!
Not only can you not drink, but you are also ineligible for social security!
```
By using nesting, (and also rewriting our print-out to better make sense), we've successfully been able to handle different cases based on the user's age.

## Making Conditional Statements Cleaner 
The more complex your conditions become, the more clutter your eyes have to look at. A simple trick to reduce this clutter is to remove the brackets of ``if-elseif-else`` statements that only execute a single line of code if true:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18)
        printf("You are not yet an adult!\n");
    else if(age < 21)
        printf("You are an adult, but you can not legally drink alcohol yet!\n");
    else if(age < 62)
            printf("Not only can you not drink, but you are also ineligible for social security!\n");
    else
        printf("You are an adult and can do everything legal!\n");

    return 0;
}
```
Note that this trick **only** works properly when the conditional statement's body has 1 line of code; The reason this is so is because a conditional statement will only consider the next line of code after it as part of its body. All other code is not considered related to the conditional statement. Take this, for example:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int age = 19;

    if(age < 18)
        printf("You are not yet an adult!\n");
        printf("%d", age);

    return 0;
}
```
While it _looks_ like both ``printf``s are under the same condition statement, it is actually only the first that is. The second will print out no matter what.

## The Ternary Operator
Ternary operator... sounds intimidating. Is it? Nah. It's actually just a fancy way to write conditional statements. See this?
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int a = 1; int b = 2; int c = 3;

    if(a < b)
        c = a;
    else
        c = b;

    return 0;
}
```
This can be simplified to:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int a = 1; int b = 2; int c = 3;

    c = (a < b) ? a : b;

    return 0;
}
```
WOW, look how much cleaner that is! Is it more readable to humans? Well... no, not quite. But it's more minimal than using clunky ``if-else`` chains. We can even chain them, too:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int a = 1; int b = 2; int c = 3;

    c = (a < b) ? ((a == b) ? 3: 4) : b;

    return 0;
}
```
Which is just the same as:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int a = 1; int b = 2; int c = 3;

    if(a < b)
        if(a == b)
            c = 3;
        else
            c = 4;
    else
        c = b;

    return 0;
}
```
While ternary operator chaining is cool, the fact that you can nest no-bracket ``if`` statements under other no-bracket ``if`` statements is cooler. Play around with how you can structure your conditional statements, and see what you like the most!

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)