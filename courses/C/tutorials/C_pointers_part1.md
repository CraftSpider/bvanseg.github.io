# Introduction to Pointers
First and foremost, congratulations. You've made it this far. 

But in this tutorial, things are about to ramp up. Why? Because pointers are some of the most powerful tools that C can offer you. But they can also be the most confusing to people that are new to memory management. Therefore...

**It is with the most emphasis that you read this tutorial VERY, VERY carefully.**

So, where to begin? Well, let's take a step back for a minute. Before arrays, before we discussed functions, before we even started our first program. And let's start with memory.

## Sweet Memory
What's actually happening when we run the program we've just made? Well, it's loaded into the **RAM**. The **RAM** of your computer is a quick-access memory component that allows your computer to very quickly work with data, must faster than working straight from the hard drive, which can be especially slower if it has moving parts (which can't move as fast as electricity can within RAM or a solid state drive).

When your computer program is put into the RAM by your computer's operating system, it allocates a fixed amount of space in the RAM that that program can take up.

All your RAM is is just large blocks of data. In fact, there's billions of bytes that can be used in RAM. These bytes have their own addresses in memory, kind of like a city where each house gets its own address.

To further strengthen the analogy, when you want a friend to come over, what is the first thing you give them? An address, correct? And then they know where to find your house. The same is true with data. Whenever the computer wants to find data in its memory, it first has to be made aware of the address, so it can have **directions** on where to go.

### Now Come the Pointers
So, furthering our analogy from the last section, a **pointer** is an address to the computer. It's a number, specifically. And what it represents is a location somewhere in memory. Since there are billions of bytes in your RAM, and since the data type ``int`` can hold numbers up to the billions, it therefore makes sense that ``pointer``s can be represented as ``int``s, and they are. 

So down the road, if you get weird, huge numbers printing out, remember that they are likely addresses (unless they're negative, because remember, physical space can't be negative).

If ``pointer``s sound foreign and alien to you, don't be disheartened! You've actually encountered these before when using ``scanf``! That's right, when you use ``&`` on a variable, you are getting a pointer to that variable's position in your RAM. This allows ``scanf`` to find your variable in memory, and therefore change its value to whatever the user inputs.

So now we realize that ``&`` just turns a variable into a ``pointer``.

### Getting Dirty with Pointers
So now that we have a theoretical understanding of pointers, how do we actually *use* them? Simple enough. Consider the following:

``int x = 3;``

Just a normal ``int`` variable, right? We've seen these before. Now let's make a pointer for that variable:
```c
int x = 3;
int* pointerToX = &x;
```
Simple enough, right? Now, a couple things to note here:
- A pointer is denoted by the ``*`` symbol. This is what makes our pointer a ``pointer`` and not simply just an ``int``. It does not matter *where* the asterisk is placed, just so long as it's between the ``type`` of the variable and the ``identifier`` (name) of the variable.
- An ``int`` does **not** equal an ``int*``. One is an integer, the other is an integer BUT with special information associated with it. They are not equal in usage (but can be equal in value).
- You can have a pointer to any type. So, you can have a ``float*``, a ``char*``, a ``long*``, a pointer to anything! Because at the end of the day, data is data. It's all bytes, even when sometimes it doesn't seem like it!

Okay, well that's great, but so what? What does this pointer really do? It doesn't seem all that useful, yet.

Admittedly, you can't do much with an address. It's just a place in memory. What you care about, though, is the value at the address. But the ``pointer`` itself doesn't tell you the value at the address, it simply just tells you the address. Just like your friend's home address doesn't really tell who is in the house (in other words, the "value" of the house).

But what you *can* do with an address is get the value at it, like so:
```c
int x = 3;
int* pointerToX = &x;
printf("%d", *pointerToX);
```
which outputs: ``3``

Now, there's a couple things of nuance going on here. The first thing to note is that we are again using a ``*`` when we get the value of the pointer **from** the address. This is known as **dereferencing the pointer**. What's really happening is C sees our ``*pointerToX`` and says, "Oh, okay, you want me to go get the value of that address, then. Alright!", hence, the program above prints out ``3``.

Additionally, earlier it was stated that an address represents only one byte in memory. And yet, our pointer is an ``int*``, where we know an ``int`` is 4 bytes. So what's going on here?

Well, the situation is that the ``pointer`` is pointing to the **starting** address of 4 bytes in memory. No matter what the size of the data you are working with, a pointer will point to the start of it, unless you manually change the address of the pointer. So when you **dereference** the pointer, C will check the size of the type the pointer is (in this case, an ``int``), and read X number of bytes, where X is the size of the type (in this case, ``4`` bytes).

For example, let's consider a theoretical idea. Suppose we have a custom numeric ``data type``, and we call this type the ``blob`` type. We declare that, "the ``blob`` type is 20 bytes in size!".

Now let's suppose we want to make a pointer to our ``blob`` type. We would do it like so:
```c
blob aBlob = 40;
blob* pointerToABlob = &aBlob;
```
Now what we've done is we've created a ``blob`` variable, and it now exists somewhere in memory as soon as we give it a name. So we have 20 bytes dedicated to it, each with their own address.

Then we create a pointer to it. The pointer starts at the beginning address of ``aBlob``'s 20 reserved bytes in memory.

If we dereference ``aBlob`` by doing ``*pointerToABlob``, C **knows** our pointer's type is the ``blob`` type, which it also **knows** for a fact is ``20`` bytes in size. So, from the starting address of ``aBlob``'s bytes, it will read that address and then the next 19 after it to get our value of ``40``.

## Interesting Pointer Behavior
So far, we know how to:
- Get the address of a variable and store it to a pointer.
- Get the value back from an address.

So let's crank it up a notch. Suppose we have this situation:
```c
int x = 0;
int y = 1;

int* pointerToX = &x;
*pointerToX++;
printf("%d", x);
```
This code outputs ``1``.

**"Wait a minute! X is 0! You can't fool me, Mr. tutorial writer!"**
- Certainly not, but C can. The output actually *is* 1, because think about it. X has **ONE** and only one set of bytes reserved in memory. We create a pointer to the starting address of those bytes, then we **change the value of those bytes**. So when we use ``x`` again, is it not true that ``x``'s values must have also changed?

This opens the doors to a whole new set of power that is unprecedented. If we can bind multiple ``pointer``s to a single variable, when we change the value of one ``pointer``, **all** of the pointer's values will also change! Because they all share the same data in memory!

For example:
```c
int x = 0;

int* pointerToX = &x;
int* anotherPointerToX = pointerToX;
*anotherPointerToX++;
printf("%d\n", *anotherPointerToX);
printf("%d\n", *pointerToX);
printf("%d", x);
```
Which outputs:
```
1
1
1
```
The two pointers and the variable they point to are all linked.

## Changing Values across Functions
Let's go even further. Remember in our earlier tutorial about **functions**, that changing the value of a parameter does **not** change the value back from where we called it? So if we had a function ``foo`` and passed ``x`` into it from the ``main`` function, and tried changing the value of ``x`` from inside the ``main`` function, it wouldn't change back over in ``main``, only for the rest of ``foo``'s execution up until a ``return`` or the ending bracket.

Well, now with pointers, what we can do is pass along a ``pointer`` to ``x`` and then change the value at that address from inside ``foo``. Then when our function is done, back in the ``main`` function, ``x`` will also be updated there, as well. Here is the code demonstrating this awesome behavior:
```c
#include <stdio.h>
#include <stdlib.h>

void foo(int*); // Remember your prototype! Also notice the type here is an int pointer.

int main() {

    int x = 0;
    foo(&x); // Use & on our x variable to get a pointer to it.
    printf("%d", x); // Outputs 3.
    return 0;
}

void foo(int *x) { // x is a pointer variable.
    *x = 3;
}
```
And yes, it does indeed output ``3``! We were able to change ``x`` even though it was not in the same scope! This is because, while certain code may not be visible or accessible to change, **memory**, on the other hand, is accessible from **anywhere** in the program, and can therefore be changed **somewhere** like at the bytes of ``x`` and that change be visible **everywhere** (hence ``x`` in the ``main`` function changes, albeit indirectly).

### scanf() with Pointers
Let's revisit ``scanf``. We're well aware that the user can scan a number into a variable. But, now that we know that ``pointers`` are what we were using with ``scanf``, it makes sense that, if we are scanning numbers into a ``pointer``, we do not need to use the ``&`` operator of it. That would be the address of the pointer itself, which is... weird.

So we can actually do something like this:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int x = 0;
    int* input = &x;
    scanf("%d", input); // Notice, there is no & here, since input is already an address.
    printf("%d\n", x); // Outputs whatever the user puts in.
    return 0;
}
```
Go ahead and give it a try!

## malloc()
So here's some interesting truths to tell. It is true that a pointer can point to data of any size. It is also true that it can point to any type. It is true that the type of pointer tells C how many bytes to read forward when dereferencing.

So is it not true that a ``pointer`` can *technically* hold 2 ``int``s? Or, two ``float``s? If a ``pointer`` can point to the beginning of 8 bytes, and an ``int`` is 4 bytes, then it must be able to hold two ``int``s.

And that's exactly right. But how do we do that? How can we tell a pointer of type ``int*`` to point **not** to a variable of 4 bytes, but to a block of 8 or however many bytes we want? Well, we use the ``malloc`` function.

``malloc`` ("memory allocate") is an interesting function. It takes a single parameter, and that's the amount of bytes you want to allocate (or, "reserve") for your pointer. So when you call ``malloc``, C will go try to find the amount of bytes you request, and then it will give you a ``pointer`` back to the **starting address* of that block of memory you just asked for.

Let's see this in action:

``int* pointerToSomewhere = malloc(8);``

Okay, so we got our ``pointer``, which is ``8`` bytes in size, and it's of the type ``int*``, so 8 (bytes allocated) / 4 (size of an int in bytes) = 2. So this pointer holds 2 ``int``s.

We know we can set the first 4 bytes by just doing ``*pointerToSomewhere = 3;`` But... what about those other 4 bytes at the end? How can we set those?

Well, we can actually do this: 

``pointerToSomewhere[1] = 4;``

GASP! A ``pointer`` can be used **just** like an ``array``! So this must also mean that ``*pointerToSomewhere = 3;`` is just the same as doing ``pointerToSomewhere[0] = 3;`` **And it is!**

So therefore, **dereferencing** is just the same as getting the first element of a ``pointer``, which functions somewhat like an ``array``.

And, just like an ``array``, if we tried to access ``pointerToSomewhere[2]``, we would get data that is beyond the size of our pointer (``pointerToSomewhere[2]`` gets the bytes 9-12 offset from the starting address). However, we did not ``malloc`` that memory; we did not allocate it. So it is considered dangerous to use that memory, as that memory may be reserved by somewhere else in our program, or, some other program. So don't access bytes beyond the size of your pointer, or bad things may happen!

That's about all to cover on pointers for this tutorial. Since pointers are such a huge deal, the next couple of tutorials are also dedicated to learning about them. If anything in this tutorial was confusing, be sure to visit our discord or github repository, and leave a comment or issue on what to clarify!


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)