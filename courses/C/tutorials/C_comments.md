# Comments
It's important to remember that we don't necessarily always create code for just ourselves. Like math classes in schools, it's important to show your work, so others can understand how you did something, what you were trying to do, and, if you didn't finish something, what your end-goal was.

**Comments** on programming are how programmers convey these notes to other programmers. There is a proportional relationship to the quality of someone's code and how much documentation via commenting the code has.

Note that when your code is converted to machine language, comments are ignored and do not become part of the compiled program. They are purely for humans to read.

That being said, let's create some comments in C.

## Single-Line Comments
Single line comments are the easiest in C:
```c
int age = 21; // The age of the person in years.
```

## Multi-Line Comments
Rather than having a bunch of single line comments, you can have a multi-line comment like so:
```c
#include <stdio.h>
#include <stdlib.h>

/** The main function is where our program starts.
This simple program will print "Hello, world!".
**/
int main() {
    printf("Hello, world!");
    return 0;
}
```

## Good Commenting Techniques
Note that the program above is not necessarily a good example of commenting. There's a time when you comment, and a time when you don't comment on code. If your variables already explain enough of what is going on for others to get the gist of it, comments become unnecessary. Therefore, it's important that you:
- Name your variables so that they make sense.
- Comment only on things that may not be clear.
- Try to avoid commenting **inside** of ``functions`` or if-statements. If you have to do either of these to make your code understandable, you should instead reconsider the structure of your ``functions`` and ``if``-statements, and the variables used within them.
- Go straight to the point. The shorter a comment is, the better.
- Don't make repetitive comments. If you already explained what variable ``x`` does at the top of the file, it should be assumed that it maintains that explained usage in the rest of the file.
- If you need to quickly "remove" code for testing, simply comment it out and then uncomment it later, rather than deleting and then retyping.
- Remember that comments can be for yourself, too! If you didn't finish something, comment your progress so that when future you comes back to it, you can read and remember what you were doing.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)