# Strings
In general, programmers do not refer to text as "text". That's too broad. After all, the entire file is text, so if another developer says "text", the only question that follows is, "what do you mean?"

So, we programmers when talking about a **collection** of characters in order, we refer to them as ``string``s.

In C, there is no type for a ``string``. Instead, ``string``s are represented as a ``char[]`` OR additionally as a ``char*``.

We understand the first one as an ``array``, and the second one as a ``pointer``, which also ultimately can boil down to an ``array``.

## Creating Strings
There are 2-3 ways to create Strings (``char arrays``). The first way is to use ``array``s:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    char aString[14] = "Hello, world!";
    printf("%s", aString); // Notice the format specifier for strings.

    return 0;
}
```
Which outputs: ``Hello, world!``

Notice that the size of the ``char array`` is the amount of characters in the ``string`` +1 more in size. There's a reason for that, and we'll get into it soon.

Because this type of ``string`` is seen as an ``array`` to C, all the rules that apply to ``array``s apply to this ``string``, as well. This includes not being able to reassign ``aString`` to a new string.

Also, note that you do not have to specify the size of the array when creating strings like above:

``char aString[] = "Hello, world!";``

Just know that the size will automatically be set for you if you do that.

Additionally, we could have created the ``string`` like this:

``char aString[14] = { 'H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!', '\0'};``

again, being omitting the size of the array is allowed:

``char aString[] = { 'H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!', '\0'};``

**"What's that funky symbol at the end of the string?"**

Ah, now that's the reason for creating the ``char array`` to include an additional char. If you can remember from our ``escap characters`` table back in the tutorial about printing data, that is called a **null terminator**. What it does is it signifies the end of the string. Why is this needed, you ask?
- Because remember, all we're doing is just giving a name to what is essentially a bunch of bytes in memory. If C were to try to read that ``string`` from memory, well, unlike an ``int`` and other types, a ``string`` has no fixed size! So how would it know how many bytes to read until it stops? **IT DOESN'T**, is the answer.
- Since C doesn't know when to stop reading a ``string``, we have to **tell** it when to stop, and we do so by putting that fancy character at the end of our ``string``s. You **only** have to do this when creating ``string``s per-character like above. When you use double quotation marks (``""``), C is generous enough to do it for you.
- So, whenever you work with the size of a string, remember to add 1 to it.

You may want to remember those bullet points when working with ``string``s in the future!

Continuing on, the second method of creating ``string``s is using ``pointer``s:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    char* aString = "Hello, world!";
    printf("%s", aString);

    return 0;
}
```

Like ``char arrays`` obey the rules of ``array``s, ``string``s made using ``pointer``s obey the rules of ``pointer``s. Which means that these kinds of ``string``s (when combined with some fancy reallocation code) can be resized, unlike their array counterparts. We'll be covering such examples later on in the memory management tutorial.

For now, just know that these are the different ways to make ``string``s.

## String Manipulation
When we create ``string``s, we may want to sometimes change them. Due to how memory works in C, this can be a bit of a challenge. Luckily, the ``string.h`` header file provides some utility functions for us to manipulate our ``string``s. We'll be looking more specifically at ``strcpy()`` and ``strcat()``, which copy and concatenate ``string``s respectively.

### Copying Strings With strcpy()
Suppose we have the following code setup:
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {

    char woman[] = "Mary";
    char womanLastName[] = "Jane";
    char man[] = "John";
    char manLastName[] = "Doe";

    int isMarried = 0;

    printf("Hello, my name is %s %s, and I am %s %s's girlfriend.", woman, womanLastName, man, manLastName);

    return 0;
}
```
Right now, this code prints out ``Hello, my name is Mary Jane, and I am John Doe's girlfriend.``

This is fine as is, but, suppose our lovely couple gets married. Well, then one of their last name's needs to change.

So the wife's name will be presumed to change to "Doe". However, look at our types. They're ``array``s. We can't reassign them like so:

``womanLastName = manLastName;``

C won't let us do that, since C is not sure if the new array will be of a larger size, which would break the rule that ``array``s can't change in size.

But, we can **copy** the man's last name to the woman's last name:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {

    char woman[] = "Mary";
    char womanLastName[] = "Jane";
    char man[] = "John";
    char manLastName[] = "Doe";

    int isMarried = 0;

    printf("Hello, my name is %s %s, and I am %s %s's girlfriend.\n", woman, womanLastName, man, manLastName);

    isMarried = 1;

    if(isMarried) {
        strcpy(womanLastName, manLastName);
    }

    printf("We are now married! My last name is now %s!", womanLastName);
    return 0;
}

```
Which outputs:
```
Hello, my name is Mary Jane, and I am John Doe's girlfriend.
We are now married! My last name is now Doe!
```
And tada! We were able to change the woman's last name.

#### However...
Recall that ``string``s have ``\0`` at their end. Since we are copying a shorter ``string`` (``manLastName``, which is ``Doe\0``) into a larger ``string`` (``womanLastName``, which is ``Jane\0``), we are in actuality printing out the ``string`` ``"Doe\0\0"``.

C will never see that last ``\0`` because it stops at the first. But consider this: What happens if we copy a much larger string into a much smaller string, and the ``\0`` within the string are accidentally removed?

Well, then we get the issue of C not knowing when to stop reading the ``string`` from memory. For this reason, ``strcpy()`` is considered an unsafe way of copying ``string``s. If you want to look for safer alternatives, you are challenged to do some research into different ``string`` copying methods, of which there are plenty provided by C!

### Concatenating Strings With strcat()
First, let's get something out of the way. **String concatenation** just means joining strings together. That's all it means.

That being said, let's dive into the code:
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {

    char* part1 = "I once was lost...";
    char* part2 = " but now I'm found!";

    printf("%s%s", part1, part2);

    return 0;
}
```
Which outputs: ``I once was lost... but now I'm found!``

This code *looks* good, but if we have to print out ``part1`` and ``part2`` multiple times, that can become rather frustrating to use two ``%s`` every single time in our printing.

So what we can do is join them together into a 3rd string, like so:
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {

    char part1[50] = "I once was lost...";
    strcat(part1, " but now I'm found!");

    printf("%s", part1);

    return 0;
}
```
Which outputs: ``I once was lost... but now I'm found!``

Same code, but a little cleaner, don't you think?

There's only one catch here. The ``string` array we are copying into **must** be big enough to allow the other string to be added to it. Notice our ``part`` ``char array`` was given 50 characters worth of space, even though it's value is nowhere near that amount. We've allocated more memory to it than is necessary in anticipation of adding more text to it.

``strcat()`` has the same issues with null terminators as with ``strcpy()``, so you are encouraged to find safer methods to work with.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)