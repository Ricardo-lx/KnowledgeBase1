 the greater precision
with the decimal type by trying the following code:
C#
The M suffix on the numbers is how you indicate that a constant should use the decimal
type. Otherwise, the compiler assumes the double type.
Notice that the math using the decimal type has more digits to the right of the decimal
point.
Challenge
Now that you've seen the different numeric types, write code that calculates the area of
a circle whose radius is 2.50 centimeters. R emember that the area of a circle is the radius
squared multiplied by PI. One hint: .NET contains a constant for PI, Math.PI  that you can
use for that value. Math.PI , like all constants declared in the System.Math namespace, is
a double value. For that reason, you should use double instead of decimal values for
this challenge.
You should get an answer between 19 and 20. Y ou can check your answer by looking at
the finished sample code on GitHub .
Try some other formulas if you'd like.
You've completed the "Numbers in C#" quickstart. Y ou can continue with the Branches
and loops  quickstart in your own development environment.
You can learn more about numbers in C# in the following articles:Console.WriteLine( $"The range of the decimal type is {min} to {max}"); 
double a = 1.0; 
double b = 3.0; 
Console.WriteLine(a / b);  
decimal c = 1.0M; 
decimal d = 3.0M; 
Console.WriteLine(c / d);  
７ Note
The letter M was chosen as the most visually distinct letter between the double and
decimal keywords.
Integral numeric types
Floating-point numeric types
Built-in numeric conversionsC# if statemen ts and loops -
conditional logic tutorial
Article •10/15/2022
This tutorial teaches you how to write C# code that examines variables and changes the
execution path based on those variables. Y ou write C# code and see the results of
compiling and running it. The tutorial contains a series of lessons that explore branching
and looping constructs in C#. These lessons teach you the fundamentals of the C#
language.
The tutorial expects that you have a machine set up for local development. See Set up
your local environment  for installation instructions and an overview of application
development in .NET.
If you prefer to run the code without having to set up a local environment, see the
interactive-in-browser version of this tutorial .
Create a directory named branches-tut orial. Make that the current directory and run the
following command:
.NET CLI Tip
To paste a code snippet inside the focus mode  you should use your keyboard
shortcut ( Ctrl + v, or cmd + v).
Prerequisites
Make decisions using the if statement
dotnet new console  -n BranchesAndLoops  -o . 
） Impor tant
The C# templates for .NET 6 use top lev el statements . Your application may not
match the code in this article, if you've already upgraded to the .NET 6. For more
information see the article on New C# t emplat es generat e top lev el stat ementsThis command creates a new .NET console application in the current directory. Open
Program.cs  in your favorite editor, and replace the contents with the following code:
C#
Try this code by typing dotnet run in your console window. Y ou should see the message
"The answer is greater than 10." printed to your console. Modify the declaration of b so
that the sum is less than 10:
C#
Type dotnet run again. Because the answer is less than 10, nothing is printed. The
condition  you're testing is false. Y ou don't have any code to execute because you've
only written one of the possible branches for an if statement: the true branch.
This first sample shows the power of if and Boolean types. A Boolean  is a variable that
can have one of two values: true or false. C# defines a special type, bool for BooleanThe .NET 6 SDK also adds a set of implicit  global using directives for projects that
use the following SDKs:
Microsoft.NET.Sdk
Microsoft.NET.Sdk.W eb
Microsoft.NET.Sdk.W orker
These implicit global using directives include the most common namespaces for
the project type.
int a = 5; 
int b = 6; 
if (a + b > 10) 
    Console.WriteLine( "The answer is greater than 10." ); 
int b = 3; 
 Tip
As you explore C# (or any programming language), you'll make mistakes when you
write code. The compiler will find and report the errors. Look closely at the error
output and the code that generated the error. The compiler error can usually help
you find the problem.variables. The if statement checks the value of a bool. When the value is true, the
statement following the if executes. Otherwise, it's skipped. This process of checking
conditions and executing statements based on those conditions is powerful.
To execute different code in both the true and false branches, you create an else
branch that executes when the condition is false. T ry an else branch. Add the last two
lines in the code below (you should already have the first four):
C#
The statement following the else keyword executes only when the condition being
tested is false. Combining if and else with Boolean conditions provides all the power
you need to handle both a true and a false condition.
Because indentation isn't significant, you need to use { and } to indicate when you
want more than one statement to be part of the block that executes conditionally. C#
programmers typically use those braces on all if and else clauses. The following
example is the same as the one you created. Modify your code above to match the
following code:
C#Make if and else work together
int a = 5; 
int b = 3; 
if (a + b > 10) 
    Console.WriteLine( "The answer is greater than 10" ); 
else 
    Console.WriteLine( "The answer is not greater than 10" ); 
） Impor tant
The indentation under the if and else statements is for human readers. The C#
language doesn't treat indentation or white space as significant. The statement
following the if or else keyword will be executed based on the condition. All the
samples in this tutorial follow a common practice to indent lines based on the
control flow of statements.
int a = 5; 
int b = 3; 
if (a + b > 10) You can test more complicated conditions. Add the following code after the code you've
written so far:
C#
The == symbol tests for equality . Using == distinguishes the test for equality from
assignment, which you saw in a = 5.
The && represents "and". It means both conditions must be true to execute the
statement in the true branch. These examples also show that you can have multiple
statements in each conditional branch, provided you enclose them in { and }. You can
also use || to represent "or". Add the following code after what you've written so far:
C#{ 
    Console.WriteLine( "The answer is greater than 10" ); 
} 
else 
{ 
    Console.WriteLine( "The answer is not greater than 10" ); 
} 
 Tip
Through the rest of this tutorial, the code samples all include the braces, following
accepted practices.
int c = 4; 
if ((a + b + c > 10) && (a == b))  
{ 
    Console.WriteLine( "The answer is greater than 10" ); 
    Console.WriteLine( "And the first number is equal to the second" ); 
} 
else 
{ 
    Console.WriteLine( "The answer is not greater than 10" ); 
    Console.WriteLine( "Or the first number is not equal to the second" ); 
} 
if ((a + b + c > 10) || (a == b))  
{ 
    Console.WriteLine( "The answer is greater than 10" ); 
    Console.WriteLine( "Or the first number is equal to the second" ); 
} 
else 
{ Modify the values of a, b, and c and switch between && and || to explore. Y ou'll gain
more understanding of how the && and || operators work.
You've finished the first step. Before you start the next section, let's move the current
code into a separate method. That makes it easier to start working with a new example.
Put the existing code in a method called ExploreIf(). Call it from the top of your
program. When you finished those changes, your code should look like the following:
C#    Console.WriteLine( "The answer is not greater than 10" ); 
    Console.WriteLine( "And the first number is not equal to the second" ); 
} 
ExploreIf();  
void ExploreIf () 
{ 
    int a = 5; 
    int b = 3; 
    if (a + b > 10) 
    { 
        Console.WriteLine( "The answer is greater than 10" ); 
    } 
    else 
    { 
        Console.WriteLine( "The answer is not greater than 10" ); 
    } 
    int c = 4; 
    if ((a + b + c > 10) && (a > b))  
    { 
        Console.WriteLine( "The answer is greater than 10" ); 
        Console.WriteLine( "And the first number is greater than the  
second"); 
    } 
    else 
    { 
        Console.WriteLine( "The answer is not greater than 10" ); 
        Console.WriteLine( "Or the first number is not greater than the  
second"); 
    } 
    if ((a + b + c > 10) || (a > b))  
    { 
        Console.WriteLine( "The answer is greater than 10" ); 
        Console.WriteLine( "Or the first number is greater than the second" ); 
    } 
    else 
    { 
        Console.WriteLine( "The answer is not greater than 10" ); Comment out the call to ExploreIf(). It will make the output less cluttered as you work
in this section:
C#
The // starts a comment  in C#. Comments are any text you want to keep in your source
code but not execute as code. The compiler doesn't generate any executable code from
comments.
In this section, you use loops  to repeat statements. Add this code after the call to
ExploreIf:
C#
The while statement checks a condition and executes the statement or statement block
following the while. It repeatedly checks the condition, executing those statements until
the condition is false.
There's one other new operator in this example. The ++ after the counter variable is the
increment  operator. It adds 1 to the value of counter and stores that value in the
counter variable.        Console.WriteLine( "And the first number is not greater than the  
second"); 
    } 
} 
//ExploreIf();  
Use loops to repeat operations
int counter = 0; 
while (counter < 10) 
{ 
    Console.WriteLine( $"Hello World! The counter is {counter} "); 
    counter++;  
} 
） Impor tant
Make sure that the while loop condition changes to false as you execute the code.
Otherwise, you create an infinit e loop  where your program never ends. That is notThe while loop tests the condition before executing the code following the while. The
do ... while loop executes the code first, and then checks the condition. The do while
loop is shown in the following code:
C#
This do loop and the earlier while loop produce the same output.
The for loop is commonly used in C#. T ry this code:
C#
The previous code does the same work as the while loop and the do loop you've
already used. The for statement has three parts that control how it works.
The first part is the for initializer : int index = 0; declares that index is the loop
variable, and sets its initial value to 0.
The middle part is the for condition : index < 10 declares that this for loop continues
to execute as long as the value of counter is less than 10.
The final part is the for it erator: index++ specifies how to modify the loop variable after
executing the block following the for statement. Here, it specifies that index should be
incremented by 1 each time the block executes.
Experiment yourself. T ry each of the following variations:demonstrated in this sample, because you have to force your program to quit using
CTRL-C  or other means.
int counter = 0; 
do 
{ 
    Console.WriteLine( $"Hello World! The counter is {counter} "); 
    counter++;  
} while (counter < 10); 
Work with the for loop
for (int index = 0; index < 10; index++)  
{ 
    Console.WriteLine( $"Hello World! The index is {index}"); 
} Change the initializer to start at a different value.
Change the condition to stop at a different value.
When you're done, let's move on to write some code yourse