lf to use what you've
learned.
There's one other looping statement that isn't covered in this tutorial: the foreach
statement. The foreach statement repeats its statement for every item in a sequence of
items. It's most often used with collections , so it's covered in the next tutorial.
A while, do, or for loop can be nested inside another loop to create a matrix using the
combination of each item in the outer loop with each item in the inner loop. Let's do
that to build a set of alphanumeric pairs to represent rows and columns.
One for loop can generate the rows:
C#
Another loop can generate the columns:
C#
You can nest one loop inside the other to form pairs:
C#Created nested loops
for (int row = 1; row < 11; row++)  
{ 
    Console.WriteLine( $"The row is {row}"); 
} 
for (char column = 'a'; column < 'k'; column++)  
{ 
    Console.WriteLine( $"The column is {column} "); 
} 
for (int row = 1; row < 11; row++)  
{ 
    for (char column = 'a'; column < 'k'; column++)  
    { 
        Console.WriteLine( $"The cell is ( {row}, {column} )"); 
    } 
} You can see that the outer loop increments once for each full run of the inner loop.
Reverse the row and column nesting, and see the changes for yourself. When you're
done, place the code from this section in a method called ExploreLoops().
Now that you've seen the if statement and the looping constructs in the C# language,
see if you can write C# code to find the sum of all integers 1 through 20 that are
divisible by 3. Here are a few hints:
The % operator gives you the remainder of a division operation.
The if statement gives you the condition to see if a number should be part of the
sum.
The for loop can help you repeat a series of steps for all the numbers 1 through
20.
Try it yourself. Then check how you did. Y ou should get 63 for an answer. Y ou can see
one possible answer by viewing the completed code on GitHub .
You've completed the "branches and loops" tutorial.
You can continue with the Arrays and collections  tutorial in your own development
environment.
You can learn more about these concepts in these articles:
Selection statements
Iteration statementsCombine branches and loops
Learn to manage data collections using
List<T> in C#
Article •03/07/2023
This introductory tutorial provides an introduction to the C# language and the basics of
the List<T>  class.
The tutorial expects that you have a machine set up for local development. See Set up
your local environment  for installation instructions and an overview of application
development in .NET.
If you prefer to run the code without having to set up a local environment, see the
interactive-in-browser version of this tutorial .
Create a directory named list-tutorial. Make that the current directory and run dotnet
new console.Prerequisites
A basic list example
） Impor tant
The C# templates for .NET 6 use top lev el statements . Your application may not
match the code in this article, if you've already upgraded to the .NET 6. For more
information see the article on New C# t emplat es generat e top lev el stat ements
The .NET 6 SDK also adds a set of implicit  global using directives for projects that
use the following SDKs:
Microsoft.NET.Sdk
Microsoft.NET.Sdk.W eb
Microsoft.NET.Sdk.W orker
These implicit global using directives include the most common namespaces for
the project type.
For more information, see the article on Implicit using dir ectiv esOpen Program.cs  in your favorite editor, and replace the existing code with the
following:
C#
Replace <name> with your name. Save Program.cs . Type dotnet run in your console
window to try it.
You've created a list of strings, added three names to that list, and printed the names in
all CAPS. Y ou're using concepts that you've learned in earlier tutorials to loop through
the list.
The code to display names makes use of the string interpolation  feature. When you
precede a string with the $ character, you can embed C# code in the string
declaration. The actual string replaces that C# code with the value it generates. In this
example, it replaces the {name.ToUpper()} with each name, converted to capital letters,
because you called the ToUpper  method.
Let's keep exploring.
The collection you created uses the List<T>  type. This type stores sequences of
elements. Y ou specify the type of the elements between the angle brackets.
One important aspect of this List<T>  type is that it can grow or shrink, enabling you to
add or remove elements. Add this code at the end of your program:
C#List<string> names = [ "<name>" , "Ana", "Felipe" ];
foreach (var name in names)
{
    Console.WriteLine( $"Hello {name.ToUpper()} !");
}
Modify list contents
Console.WriteLine();
names.Add( "Maria");
names.Add( "Bill");
names.Remove( "Ana");
foreach (var name in names)
{
    Console.WriteLine( $"Hello {name.ToUpper()} !");
}You've added two more names to the end of the list. Y ou've also removed one as well.
Save the file, and type dotnet run to try it.
The List<T>  enables you to reference individual items by index  as well. Y ou place the
index between [ and ] tokens following the list name. C# uses 0 for the first index. Add
this code directly below the code you just added and try it:
C#
You can't access an index beyond the end of the list. R emember that indices start at 0,
so the largest valid index is one less than the number of items in the list. Y ou can check
how long the list is using the Count  property. Add the following code at the end of your
program:
C#
Save the file, and type dotnet run again to see the results.
Our samples use relatively small lists, but your applications may often create lists with
many more elements, sometimes numbering in the thousands. T o find elements in these
larger collections, you need to search the list for different items. The IndexOf  method
searches for an item and returns the index of the item. If the item isn't in the list,
IndexOf returns -1. Add this code to the bottom of your program:
C#Console.WriteLine( $"My name is {names[0]}");
Console.WriteLine( $"I've added {names[2]} and {names[3]} to the list" );
Console.WriteLine( $"The list has {names.Count}  people in it" );
Search and sort lists
var index = names.IndexOf( "Felipe" );
if (index == -1)
{
    Console.WriteLine( $"When an item is not found, IndexOf returns 
{index}");
}
else
{
    Console.WriteLine( $"The name {names[index]}  is at index {index}");
}
index = names.IndexOf( "Not Found" );The items in your list can be sorted as well. The Sort method sorts all the items in the list
in their normal order (alphabetically for strings). Add this code to the bottom of your
program:
C#
Save the file and type dotnet run to try this latest version.
Before you start the next section, let's move the current code into a separate method.
That makes it easier to start working with a new example. Place all the code you've
written in a new method called WorkWithStrings(). Call that method at the top of your
program. When you finish, your code should look like this:
C#if (index == -1)
{
    Console.WriteLine( $"When an item is not found, IndexOf returns 
{index}");
}
else
{
    Console.WriteLine( $"The name {names[index]}  is at index {index}");
}
names.Sort();
foreach (var name in names)
{
    Console.WriteLine( $"Hello {name.ToUpper()} !");
}
WorkWithStrings();
void WorkWithStrings ()
{
    List<string> names = [ "<name>" , "Ana", "Felipe" ];
    foreach (var name in names)
    {
        Console.WriteLine( $"Hello {name.ToUpper()} !");
    }
    Console.WriteLine();
    names.Add( "Maria");
    names.Add( "Bill");
    names.Remove( "Ana");
    foreach (var name in names)
    {
        Console.WriteLine( $"Hello {name.ToUpper()} !");You've been using the string type in lists so far. Let's make a List<T>  using a different
type. Let's build a set of numbers.
Add the following to your program after you call WorkWithStrings():
C#    }
    Console.WriteLine( $"My name is {names[0]}");
    Console.WriteLine( $"I've added {names[2]} and {names[3]} to the list" );
    Console.WriteLine( $"The list has {names.Count}  people in it" );
    var index = names.IndexOf( "Felipe" );
    if (index == -1)
    {
        Console.WriteLine( $"When an item is not found, IndexOf returns 
{index}");
    }
    else
    {
        Console.WriteLine( $"The name {names[index]}  is at index {index}");
    }
    index = names.IndexOf( "Not Found" );
    if (index == -1)
    {
        Console.WriteLine( $"When an item is not found, IndexOf returns 
{index}");
    }
    else
    {
        Console.WriteLine( $"The name {names[index]}  is at index {index}");
    }
    names.Sort();
    foreach (var name in names)
    {
        Console.WriteLine( $"Hello {name.ToUpper()} !");
    }
}
Lists of other types
List<int> fibonacciNumbers = [ 1, 1];That creates a list of integers, and sets the first two integers to the value 1. These are the
first two values of a Fibonac ci Sequenc e, a sequence of numbers. Each next Fibonacci
number is found by taking the sum of the previous two numbers. Add this code:
C#
Save the file and type dotnet run to see the results.
See if you can put together some of the concepts from this and earlier lessons. Expand
on what you've built so far with Fibonacci Numbers. T ry to write the code to generate
the first 20 numbers in the sequence. (As a hint, the 20th Fibonacci number is 6765.)
You can see an example solution by looking at the finished sample code on GitHub .
With each iteration of the loop, you're taking the last two integers in the list, summing
them, and adding that value to the list. The loop repeats until you've added 20 items to
the list.
Congratulations, you've completed the list tutorial. Y ou can continue with additional
tutorials in your own development environment.var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];
fibonacciNumbers.Add(previous + previous2);
foreach (var item in fibonacciNumbers)
{
    Console.WriteLine(item);
}
 Tip
To concentrate on just this section, you can comment out the code that calls
WorkWithStrings();. Just put two / characters in front of the call like this: //
WorkWithStrings();.
Challenge
Complete challenge
You can learn more about working with the List type in the .NET fundamentals article
on collections . You'll also learn about many other collection types.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide ..NET feedb ack
The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackGeneral Structure of a C# Program
Article •11/14/2023
C# programs consist of one or more files. Each file contains zero or more namespaces. A
namespace contains types such as classes, structs, interfaces, enumerations, and
delegates, or other namespaces. The following example is the skeleton of a C# program
that contains all of these elements.
C#
The preceding example uses top-lev el statements  for the program's entry point. Y ou can
also create a static method named Main as the program's entry point, as shown in the
following example:// A skeleton of a C# program
using System;
// Your program starts here:
Console.WriteLine( "Hello world!" );
namespace  YourNamespace
{
    class YourClass
    {
    }
    struct YourStruct
    {
    }
    interface  IYourInterface
    {
    }
    delegate  int YourDelegate ();
    enum YourEnum
    {
    }
    namespace  YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }
}C#
You learn about these program elements in the types  section of t