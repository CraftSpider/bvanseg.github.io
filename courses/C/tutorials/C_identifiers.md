# Identifiers

The term "Identifiers" is just a fancy way of saying "the names of variables, functions, and other things". In C, these identifiers have certain rules about them; that is to say, the names can be a certain way.

## Rules
- Identifiers can consist of the following:
     - lowercase letters (a-z).
     - uppercase letters (A-Z).
     - numbers (0-9).
     - underscores (_).
     - Can **NOT** begin with a number.
     - Can be as long as you want.
     
- Identifiers can NOT be keywords.
    - For example, you can't have a variable named ``int``.
    
- Identifiers are also **CASE SENSITIVE**. What does this mean? Well it means that a variable with the name ``foo`` is NOT the same as a variable with the name ``Foo``. C will see them as different variables and will therefore treat them as such.

## Conventions
While not important to running a program, it *is* important to know some conventions of how to name variables or functions for the sake of readability.

### Camel Case
Camel case is a convention that has been used for decades, and is still preferred and strongly advised for variables and functions. Consider the following:
```c
int foobar = 0;
int fooBar = 0;
int FooBar = 0;
```
The middle variant of these names is camel case, where the first word in a multi-word variable name is lowercase, and any words after that are capitalized. The other two are not preferred, as they can reduce readability:
```c
int thisisalongvariablename = 0;
int thisIsALongVariableName = 0;
int ThisIsALongVariableName = 0;
```
While the third one is just as readable, that convention is not used for variables or functions. It's used for constructs like ``struct``s or ``union``s. More on those later.

So the takeaway here is to use the middle convention for variables and functions, and the third convention for other types of data later on down the road.

### Constants
Any data that is marked as ``const`` should be made to have all uppercase letters, like so:
```c
const int FOO = 0;
```


[Home](https://bvanseg.github.io)