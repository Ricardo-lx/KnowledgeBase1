sual S tudio 2019 for these tutorials, you'll choose a Visual S tudio menu
selection when a tutorial directs you to run one of these CLI commands:
File > New  > Project  creates an application.
The Console Application project template is recommended.
You will be given the option to specify a target framework. The tutorials below
work best when targeting .NET 5 or higher.
Build  > Build Solution  builds the executable.
Debug  > Start Without Debugging  runs the executable.
You can start with any of the following tutorials:
Basic application development flow
Pick your tutorialIn the Numbers in C#  tutorial, you'll learn how computers store numbers and how to
perform calculations with different numeric types. Y ou'll learn the basics of rounding and
how to perform mathematical calculations using C#.
This tutorial assumes that you have finished the Hello world  lesson.
The Branches and loops  tutorial teaches the basics of selecting different paths of code
execution based on the values stored in variables. Y ou'll learn the basics of control flow,
which is the basis of how programs make decisions and choose different actions.
This tutorial assumes that you have finished the Hello world  and Numbers in C#  lessons.
The List collection  lesson gives you a tour of the List collection type that stores
sequences of data. Y ou'll learn how to add and remove items, search for items, and sort
the lists. Y ou'll explore different kinds of lists.
This tutorial assumes that you have finished the lessons listed above.Numbers in C#
Branches and loops
List collectionHow to use integer and floating point
numbers in C#
Article •10/15/2022
This tutorial teaches you about the numeric types in C#. Y ou'll write small amounts of
code, then you'll compile and run that code. The tutorial contains a series of lessons that
explore numbers and math operations in C#. These lessons teach you the fundamentals
of the C# language.
The tutorial expects that you have a machine set up for local development. See Set up
your local environment  for installation instructions and an overview of application
development in .NET.
If you don't want to set up a local environment, see the interactive-in-browser version of
this tutorial .
Create a directory named number s-quickst art. Make it the current directory and run the
following command:
.NET CLI Tip
To paste a code snippet inside the focus mode  you should use your keyboard
shortcut ( Ctrl + v, or cmd + v).
Prerequisites
Explore integer math
dotnet new console  -n NumbersInCSharp  -o . 
） Impor tant
The C# templates for .NET 6 use top lev el statements . Your application may not
match the code in this article, if you've already upgraded to the .NET 6. For more
information see the article on New C# t emplat es generat e top lev el stat ementsOpen Program.cs  in your favorite editor, and replace the contents of the file with the
following code:
C#
Run this code by typing dotnet run in your command window.
You've seen one of the fundamental math operations with integers. The int type
represents an integer, a zero, positive, or negative whole number. Y ou use the + symbol
for addition. Other common mathematical operations for integers include:
- for subtraction
* for multiplication
/ for division
Start by exploring those different operations. Add these lines after the line that writes
the value of c:
C#The .NET 6 SDK also adds a set of implicit  global using directives for projects that
use the following SDKs:
Microsoft.NET.Sdk
Microsoft.NET.Sdk.W eb
Microsoft.NET.Sdk.W orker
These implicit global using directives include the most common namespaces for
the project type.
int a = 18; 
int b = 6; 
int c = a + b;  
Console.WriteLine(c);  
// subtraction  
c = a - b;  
Console.WriteLine(c);  
// multiplication  
c = a * b;  
Console.WriteLine(c);  
// division  Run this code by typing dotnet run in your command window.
You can also experiment by writing multiple mathematics operations in the same line, if
you'd like. T ry c = a + b - 12 * 17; for example. Mixing variables and constant
numbers is allowed.
You've finished the first step. Before you start the next section, let's move the current
code into a separate method . A method is a series of statements grouped together and
given a name. Y ou call a method by writing the method's name followed by ().
Organizing your code into methods makes it easier to start working with a new example.
When you finish, your code should look like this:
C#c = a / b;  
Console.WriteLine(c);  
 Tip
As you explore C# (or any programming language), you'll make mistakes when you
write code. The compiler  will find those errors and report them to you. When the
output contains error messages, look closely at the example code and the code in
your window to see what to fix. That exercise will help you learn the structure of C#
code.
WorkWithIntegers();  
void WorkWithIntegers ()
{ 
    int a = 18; 
    int b = 6; 
    int c = a + b;  
    Console.WriteLine(c);  
    // subtraction  
    c = a - b;  
    Console.WriteLine(c);  
    // multiplication  
    c = a * b;  
    Console.WriteLine(c);  
    // division  
    c = a / b;  
    Console.WriteLine(c);  
} The line WorkWithIntegers(); invokes the method. The following code declares the
method and defines it.
Comment out the call to WorkingWithIntegers(). It will make the output less cluttered as
you work in this section:
C#
The // starts a comment  in C#. Comments are any text you want to keep in your source
code but not execute as code. The compiler doesn't generate any executable code from
comments. Because WorkWithIntegers() is a method, you need to only comment out
one line.
The C# language defines the precedence of different mathematics operations with rules
consistent with the rules you learned in mathematics. Multiplication and division take
precedence over addition and subtraction. Explore that by adding the following code
after the call to WorkWithIntegers(), and executing dotnet run:
C#
The output demonstrates that the multiplication is performed before the addition.
You can force a different order of operation by adding parentheses around the
operation or operations you want performed first. Add the following lines and run again:
C#
Explore more by combining many different operations. Add something like the following
lines. T ry dotnet run again.Explore order of operations
//WorkWithIntegers();  
int a = 5; 
int b = 4; 
int c = 2; 
int d = a + b * c;  
Console.WriteLine(d);  
d = (a + b) * c;  
Console.WriteLine(d);  C#
You may have noticed an interesting behavior for integers. Integer division always
produces an integer result, even when you'd expect the result to include a decimal or
fractional portion.
If you haven't seen this behavior, try the following code:
C#
Type dotnet run again to see the results.
Before moving on, let's take all the code you've written in this section and put it in a
new method. Call that new method OrderPrecedence. Your code should look something
like this:
C#d = (a + b) - 6 * c + ( 12 * 4) / 3 + 12; 
Console.WriteLine(d);  
int e = 7; 
int f = 4; 
int g = 3; 
int h = (e + f) / g;  
Console.WriteLine(h);  
// WorkWithIntegers();  
OrderPrecedence();  
void WorkWithIntegers ()
{ 
    int a = 18; 
    int b = 6; 
    int c = a + b;  
    Console.WriteLine(c);  
    // subtraction  
    c = a - b;  
    Console.WriteLine(c);  
    // multiplication  
    c = a * b;  
    Console.WriteLine(c);  
    // division  
    c = a / b;  
    Console.WriteLine(c);  That last sample showed you that integer division truncates the result. Y ou can get the
remainder  by using the modulo  operator, the % character. T ry the following code after
the method call to OrderPrecedence():
C#
The C# integer type differs from mathematical integers in one other way: the int type
has minimum and maximum limits. Add this code to see those limits:
C#} 
void OrderPrecedence () 
{ 
    int a = 5; 
    int b = 4; 
    int c = 2; 
    int d = a + b * c;  
    Console.WriteLine(d);  
    d = (a + b) * c;  
    Console.WriteLine(d);  
    d = (a + b) - 6 * c + ( 12 * 4) / 3 + 12; 
    Console.WriteLine(d);  
    int e = 7; 
    int f = 4; 
    int g = 3; 
    int h = (e + f) / g;  
    Console.WriteLine(h);  
} 
Explore integer precision and limits
int a = 7; 
int b = 4; 
int c = 3; 
int d = (a + b) / c;  
int e = (a + b) % c;  
Console.WriteLine( $"quotient: {d}"); 
Console.WriteLine( $"remainder: {e}"); 
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine( $"The range of integers is {min} to {max}"); If a calculation produces a value that exceeds those limits, you have an under flow or
overflow condition. The answer appears to wrap from one limit to the other. Add these
two lines to see an example:
C#
Notice that the answer is very close to the minimum (negative) integer. It's the same as
min + 2. The addition operation overflowed the allowed values for integers. The answer
is a very large negative number because an overflow "wraps around" from the largest
possible integer value to the smallest.
There are other numeric types with different limits and precision that you would use
when the int type doesn't meet your needs. Let's explore those other types next.
Before you start the next section, move the code you wrote in this section into a
separate method. Name it TestLimits.
The double numeric type represents a double-precision floating point number. Those
terms may be new to you. A floating point  number is useful to represent non-integral
numbers that may be very large or small in magnitude. Double-pr ecision  is a relative
term that describes the number of binary digits used to store the value. Double
precision  numbers have twice the number of binary digits as single-pr ecision . On
modern computers, it's more common to use double precision than single precision
numbers. Single pr ecision  numbers are declared using the float keyword. Let's explore.
Add the following code and see the result:
C#
Notice that the answer includes the decimal portion of the quotient. T ry a slightly more
complicated expression with doubles:
C#int what = max + 3; 
Console.WriteLine( $"An example of overflow: {what}"); 
Work with the double type
double a = 5; 
double b = 4; 
double c = 2; 
double d = (a + b) / c;  
Console.WriteLine(d);  The range of a double value is much greater than integer values. T ry the following code
below what you've written so far:
C#
These values are printed in scientific notation. The number to the left of the E is the
significand. The number to the right is the exponent, as a power of 10. Just like decimal
numbers in math, doubles in C# can have rounding errors. T ry this code:
C#
You know that 0.3 repeating finite number of times isn't exactly the same as 1/3.
Challenge
Try other calculations with large numbers, small numbers, multiplication, and division
using the double type. T ry more complicated calculations. After you've spent some time
with the challenge, take the code you've written and place it in a new method. Name
that new method WorkWithDoubles.
You've seen the basic numeric types in C#: integers and doubles. There's one other type
to learn: the decimal type. The decimal type has a smaller range but greater precision
than double. Let's take a look:
C#double e = 19; 
double f = 23; 
double g = 8; 
double h = (e + f) / g;  
Console.WriteLine(h);  
double max = double.MaxValue;  
double min = double.MinValue;  
Console.WriteLine( $"The range of double is {min} to {max}"); 
double third = 1.0 / 3.0; 
Console.WriteLine(third);  
Work with decimal types
decimal min = decimal.MinValue;  
decimal max = decimal.MaxValue;  Notice that the range is smaller than the double type. Y ou can see