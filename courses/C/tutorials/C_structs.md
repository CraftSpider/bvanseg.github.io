# Structs
As data in a program grows more and more complex, there becomes a growing need to have a better way to store it all.

Even with ``pointer``s and arrays, having a bunch of those floating around the project code can get messy.

``struct``s are a way to group our data together in a more cohesive and collective way. Consider the following example of where a ``struct`` could be useful:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int* studentId = malloc(50*sizeof(int));
    float* courseGrade = malloc(50*sizeof(float));

    return 0;
}
```
This is a simple program that doesn't do anything, but, you could presume what it's going to do. This is deliberate; as we program, we should analyze our code as we go along. So let's analyze the start of this program.

We notice that this might be a program to store a maximum of 50 student ID's, and 50 course grades presumably associated with those student IDs in a 1:1 in terms of indexes (that is to say, studenetId[0] corresponds to courseGrade[0]).

But this code is already messy. Why? Because the data is bound together using nothing more than a number, which isn't quite useful. So this is a good example of using a ``struct`` to "bind" the two data together.

A ``struct`` is a "blueprint" that defines what a student *is* in our code:
```C
struct student {
    int studentId;
    float courseGrade;
};
```
As we can see, this data has the type ``struct`` and an identifier ``student``. This is merely a **TEMPLATE**. This isn't a variable in the traditional sense, but rather, it's used to make variables.

With a ``struct``, it holds variables which we can call ``members``. These members can be of **ANY** type. Even other ``struct``s! Additionally, since this ``struct`` is merely a template, we do not need to set the value for them. In fact, C won't even let you do so.

Also notice that the ``struct`` needs a semi-colon at the end of its brackets, unlike a ``function``. This is because the ``struct`` is not treated as a ``scope``, but rather as a ``variable`` (it's just a really complex one).

See the following code below:
```c
#include <stdio.h>
#include <stdlib.h>

struct student {
    int studentId;
    float courseGrade;
};

int main() {

    struct student students[50];

    for(int i = 0; i < 50; i++ ) {
        students[i].studentId = i;
        students[i].courseGrade = 100.0;
        printf("Student's ID: %d\n", students[i].studentId);
        printf("Student's Grade: %f\n", students[i].courseGrade);
    }
    return 0;
}
```
Wow! At a glance, we've managed to condense those pointers into a single line of code. Let's look at this code carefully:

```c
struct student {
    int studentId;
    float courseGrade;
};
```
This is the ``struct`` we went over earlier. It holds all of the data that defines our student.

``struct student students[50];`` - Here we define an array of these students. That's an ``array`` of 50 ``struct``s.

within the loop...

`` students[i]`` - We access our ``array`` of ``struct``s and get the one at index ``i``.

The dot (``.``) operator we use on the ``struct`` is known as the **access operator**. Once we do this, we can then grab the variables associated with our ``struct``, like so:

``students[i].studentId = i;`` - Here we set the ``studentId`` of the student at index ``i`` to whatever ``i`` is. This means all students in the ``for`` loop will get an id corresponding to when the loop accessed them from the ``array`` (0, 1, 2, 3... 50).

``students[i].courseGrade = 100.0;`` - We do the same thing for the student's grade. In this case, we give everyone an A+, because they took this course. :D

``printf("Student's ID: %d\n", students[i].studentId);`` - We access the student from the array again, and then also get their studentId to print it out.

We also can set up our student ``struct``s similar to arrays:

``struct student aStudent = { 42, 95.0 };`` - C will correspond the values put in between these brackets to the order of the variables declared inside the ``struct`` template. In this case, ``42`` corresponds to ``studentId`` and ``95.0`` corresponds to ``courseGrade``.

We can also declare some student ``struct`` variables along with our declaration of the struct:
```c
struct student {
    int studentId;
    float courseGrade;
} student1, student2; // These are two student structs we can use immediately.
```

And then we can use them like so:
```c
student1.studentId = 0;
student1.courseGrade = 75.0;
student2.studentId = 1;
student2.courseGrade = 87.0;
```

However, we could **not** do this with those two student ``struct``s:
```
student1 = { -1, 95.0 };
student2 = { -1, 95.0 };
```
C treats ``struct``s like ``arrays`` in that you can't reassign them. C sees these two lines of code as reassigning the student ``struct``s, and therefore will error if you try to do this. If you want to set them up like ``array``s, you'll need to redefine them like so:
```
struct student student1 = { -1, 95.0 };
struct student student2 = { -1, 95.0 };
```
Try experimenting with ``struct``s and what you can do with them! And Remember, they can hold variables with any ``type``, even other ``struct``s and ``pointer``s!


[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)