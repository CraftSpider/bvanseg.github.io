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

## Structs with Pointers
We can combine ``struct``s and ``pointer``s to do powerful and complex data handling.

Recall that data is data. No matter what type you're working with in C, at the end of the day, it's just a bunch of bytes.

Since the above is true, it is also true that ``struct``s are bytes, and therefore, have a starting address in memory. Since this is also true, we can create ``pointer``s of ``struct``s. And if we can do that, then we can also allocate huge chunks of data for multiple ``struct``s in a row.

Consider the following scenario. You are a teacher. You need to make a program in which you associate ``Courses`` with ``Students``. We know that a ``Course`` as they pertain to a student have a **name** and a numeric **grade** associated with them:
```c
struct Course {
    char* name;
    float grade;
};
```
Now consider a ``Student``. A ``Student`` can have a **name**, **id**, **GPA**, and, most importantly, a set of **courses**:
```c
struct Student {
    char* name;
    int id;
    float gpa;
    struct Course* courses; // Notice the struct keyword, because we have not made Course a type definition (typedef).
};
```
How interesting. We are already familiar with how ``pointer``s and memory allocation behave. So we can guess that the ``courses`` for the ``Student`` ``struct`` are gonna need some room in our RAM!

So when we create a ``Student``, it's very important that we make sure to allocate space for the student's courses. Let's just say for now that students can have 7 courses:
```c
#include <stdio.h>
#include <stdlib.h>

struct Course {
    char* name;
    float grade;
};
struct Student {
    char* name;
    int id;
    float gpa;
    struct Course* courses;
};

int main() {

    struct Student student;
    student.name = "John Doe";
    student.id = 0;
    student.gpa = 4.00;
    student.courses = malloc(sizeof(struct Course) * 7);

    return 0;
}
```
Note that, we could have also set up our student this way, too:
```c
struct Student student = {"John Doe", 0, 4.00, malloc(sizeof(struct Course) * 7)};
```
Either way is fine. Just recall that for both methods, the initial ``string`` name you give the student will be considered the maximum possible size that string can be. So if you don't want to set the name of the student, but merely allocate space, you can do this:
```c
struct Student student = { malloc(50), 0, 4.00, malloc(sizeof(struct Course) * 7)};
```

Now that we have our student set up, we can just access our courses from the student as ``array`` elements and manipulate them as usual. Let's set the first course for our student:

```c
*(student.courses) = (struct Course){ "Computer Science", 100.0 };
```
Notice that we do ``(struct Course)`` to explicitly tell C "hey, this data right here? This is a course. In case you didn't know.". C will then be perfectly content with doing this.

## The ``->`` Operator
From the previous section, you may have also noticed that we are dereferencing the **courses** itself, not the actual student, since:
 1. The student is not a pointer.
 2. The entire statement becomes whatever the ``type`` of the last data referenced in the chain call. That is to say, since we referenced ``courses`` last in that chain, C sees ``student.courses`` as the type ``Course*``, aka the type of the last data referenced.

But yuck! That syntax ``*(student.courses)`` is pretty annoying to type! And what's worse is, consider if we had to change our course grade if the student failed a paper:

``(*(student.courses)).grade = 55.0;``

(This is probably the worst C code I've ever written!).

Luckily, the people that created C *also* agree that this code is horrendous. So, they gave us a nifty little operator called the **arrow operator** (``->``) to simplify it:

``student.courses->grade = 55.0;``

The ``->`` is just another way to **dereference** ``courses`` without using the ``*`` around the entire statement.

Alternatively, we could have very easily also done this:

``student.courses[0].grade = 55.0;``

It's up to you how you want to set up your code! But trust me, the last two are *probably* better. ;)

## Helpful Tips
- **"I'm getting strange numbers when using my struct! What's going on?"**
    - You have likely not **initialized** your ``struct``'s data to their respective values. This is especially true if you're working with nested ``struct``s, and had to ``malloc`` space for them. When you do that, don't forget that you should probably populate all of the ``struct``s in your memory with data, **even if you don't plan on using all them!** Because then you can use numbers like ``-1`` for a course ID to signify that the course is just blank/empty.
- **"Can you nest struct brackets in brackets?"**
    - Absolutely. Consider if we only had one course for students for our student/course example above. We could have very well just done this:
```c
#include <stdio.h>
#include <stdlib.h>

struct Course {
    char* name;
    float grade;
};
struct Student {
    char* name;
    int id;
    float gpa;
    struct Course course;
};

int main() {

    struct Student student = {"John Doe", 0, 4.00, { "Computer Science", 100.0 }};

    student.course.grade = 55.0;

    return 0;
}
```

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)