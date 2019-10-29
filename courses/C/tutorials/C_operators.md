# Operators

In C, an ``operator`` is a symbol that takes some operands and does work on them, producing a result.

There are multiple sets of operators. Below, the operators have been grouped into tables accordingly. Take time to study them, and experiment with all of them!

## Arithmetic Operators

Symbol | Description | Usage
:---: | :---: | :---:
+ | Adds two numbers together | 1 + 1 = 2;
- | Subtracts two numbers together | 1 - 1 = 0;
* | Multiplies two numbers together | 2 * 2 = 4;
/ | Divides two numbers. Denominator can not be 0. | 2 / 2 = 1;
% | Divides a number by a number, the result being the remainder. | 10 % 2 = 0;<br>10 % 3 = 1;
++ | Increments a variable (adds 1 to it) | A = 3;<br>A++;
-\- | Decerements a variable (subtracts 1 to it) | A = 3;<br>A-\-;

### Pre vs Post Increment/Decrement Operators
With the last two operators above (``++`` and ``--``), it's important to note the two various ways to use each. Suppose we have a variable ``x`` of type ``int`` that has a value of ``3``. Then suppose we are using x as follows:

``int c = 15 * x++;``

The type of ``++`` operator being used here is the **post**-increment operator, because it comes *after* the variable being incremented. ``c`` will result in a value of ``45``, since C does the multiplication ``15 * 3`` and *then* increments ``x``. If we print out ``x`` after setting ``c``, we get ``4``.

If we wanted to first increment ``x`` and **then** use it in the multiplication, we would use the **pre**-increment operator:

``int c = 15 * ++x;``

Which results in ``60``, as expected. This principle also applies to the decrement (``--``) operator.

## Relational Operators

Symbol | Description | Usage
:---: | :---: | :---:
== | Checks if two things are equal. | 1 == 1; // True
!= | Checks if two things are equal. | 1 != 1; // False
\> | Checks if a number is greater than another. | 1 > 3; // False
< | Checks if a number is less than another. | 1 < 0; // False
>= | Checks if a number is greater than or equal to another. | 1 >= 1; // True
<= | Checks if a number is less than or equal to another. | 1 <= 2;  // True

## Conditional / Logical Operators

Symbol | Description | Usage
:---: | :---: | :---:
&& | Checks if the left AND right-hand side are true | (1 == 1 && 1 == 2); // False
&#124;&#124; | Checks if the left OR right-hand side are true. | (1 == 1 &#124;&#124; 1 == 2); // True
! | Checks if a condition is NOT true. | !(2 != 2); // True

## Bitwise Operators

Symbol | Description | Usage
:---: | :---: | :---:
& | Combines the bits of two numbers if the bits in the same position per number are the same. | 1 & 2 = 0;
&#124; | Combines the bits of two numbers if either bit in a position from both numbers is 1. | 1 &#124; 2 = 3;
^ | Combines the bits of two numbers if one bit is found in the same position in one number but NOT the other. | 2 ^ 2 = 0;<br>2 ^ 3 = 1;
~ | 'flips' the bits of a number | let A = 5; (0000 1001) <br>~A = -6; // (1000 0110)
\<\< | Shifts bits of a number to the left | 2 \<\< 2 = 8;
\>\> | Shifts bits of a number to the right | 2 \>\> 1 = 1;

## Assignment Operators (Arithmetic)

For this data, let X = 20 and Y = 5. # represents any number.

Symbol | Description | Usage
:---: | :---: | :---:
= | Sets a variable equal to a value. | X = Y; // X is now  5.
+= | Equivalent to var = var + #. |  X += 5; // Same as X = X + 5, so X is now 25. 
-= | Equivalent to var = var - #. |  X -= 5; // Same as X = X - 5, so X is now 15.
*= | Equivalent to var = var * #. |  X *= 5; // Same as X = X * 5, so X is now 100.
/= | Equivalent to var = var / #. |  X /= 5; // Same as X = X / 5, so X is now 4.
%= | Equivalent to var = var % #. |  X %= 5; // Same as X = X % 5, so X is now 0.

## Assignment Operators (Bitwise)

For this data, let A = 2 and B = 3. # represents any number.

Symbol | Description | Usage
:---: | :---: | :---:
\<\<= | Equivalent to var = var << #. | A \<\<= B // Same as A = A \<\< B, so A is now 16.
\>\>= | Equivalent to var = var >> #. | B \>\>= A // Same as B = B \>\> A, so B is now 0.
&= | Equivalent to var = var & #. | A &= B // Same as A = A & B, so A is now 2.
&#124;= | Equivalent to var = var &#124; #. | A &#124;= B // Same as A = A &#124; B, so A is now 3.
^= | Equivalent to var = var ^ #. | A ^= B // Same as A = A ^ B, so A is now 1.

## Miscellaneous Operators

Symbol | Description | Usage
:---: | :---: | :---:
sizeof() | Takes the size of a given variable or keyword and returns the size of it as a number of bytes | sizeof(int) equals 4.
& | Returns the address of a variable. | int A = 3;<br>&A gives the address of A.
* | Multiple uses. See pointers tutorials for a deeper explanation. |N/A

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)