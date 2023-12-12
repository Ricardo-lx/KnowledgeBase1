ors, the precedenc e of the operators
controls the order in which the individual operators are evaluated. For example, the
expression x + y * z is evaluated as x + (y * z) because the * operator has higher
precedence than the + operator.
When an operand occurs between two operators with the same precedence, the
associativity  of the operators controls the order in which the operations are performed:
Except for the assignment and null-coalescing operators, all binary operators are
left-associativ e, meaning that operations are performed from left to right. For
example, x + y + z is evaluated as (x + y) + z.
The assignment operators, the null-coalescing ?? and ??= operators, and the
conditional operator ?: are right-associativ e, meaning that operations are
performed from right to left. For example, x = y = z is evaluated as x = (y = z).
Precedence and associativity can be controlled using parentheses. For example, x + y *
z first multiplies y by z and then adds the result to x, but (x + y) * z first adds x
and y and then multiplies the result by z.
Most operators can be overloaded . Operator overloading permits user-defined operator
implementations to be specified for operations where one or both of the operands are
of a user-defined class or struct type.
C# provides operators to perform arithmetic , logical , bitwise and shift  operations and
equality  and order  comparisons.
For the complete list of C# operators ordered by precedence level, see C# operators .
The actions of a program are expressed using statements . C# supports several different
kinds of statements, a number of which are defined in terms of embedded statements.Expressions
StatementsA block  permits multiple statements to be written in contexts where a single
statement is allowed. A block consists of a list of statements written between the
delimiters { and }.
Declar ation st atements  are used to declare local variables and constants.
Expression st atements  are used to evaluate expressions. Expressions that can be
used as statements include method invocations, object allocations using the new
operator, assignments using = and the compound assignment operators,
increment and decrement operations using the ++ and -- operators and await
expressions.
Selection st atements  are used to select one of a number of possible statements for
execution based on the value of some expression. This group contains the if and
switch statements.
Iteration st atements  are used to execute repeatedly an embedded statement. This
group contains the while, do, for, and foreach statements.
Jump st atements  are used to transfer control. This group contains the break,
continue, goto, throw, return, and yield statements.
The try...catch statement is used to catch exceptions that occur during execution
of a block, and the try...finally statement is used to specify finalization code that
is always executed, whether an exception occurred or not.
The checked and unchecked statements are used to control the overflow-checking
context for integral-type arithmetic operations and conversions.
The lock statement is used to obtain the mutual-exclusion lock for a given object,
execute a statement, and then release the lock.
The using statement is used to obtain a resource, execute a statement, and then
dispose of that resource.
The following lists the kinds of statements that can be used:
Local variable declaration.
Local constant declaration.
Expression statement.
if statement.
switch statement.
while statement.
do statement.
for statement.
foreach statement.
break statement.
continue statement.goto statement.
return statement.
yield statement.
throw statements and try statements.
checked and unchecked statements.
lock statement.
using statement.
 Previous Next
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
 Provide product feedbackC# major language areas
Article •11/14/2023
This article introduces the main features of the C# language.
C# and .NET provide many different collection types. Arrays have syntax defined by the
language. Generic collection types are listed in the System.Collections.Generic
namespace. Specialized collections include System.Span<T>  for accessing continuous
memory on the stack frame, and System.Memory<T>  for accessing continuous memory
on the managed heap. All collections, including arrays, Span<T> , and Memory<T>  share
a unifying principle for iteration. Y ou use the
System.Collections.Generic.IEnumerable<T>  interface. This unifying principle means that
any of the collection types can be used with LINQ queries or other algorithms. Y ou write
methods using IEnumerable<T>  and those algorithms work with any collection.
An array is a data structure that contains a number of variables that are accessed
through computed indices. The variables contained in an array, also called the elements
of the array, are all of the same type. This type is called the element type  of the array.
Array types are reference types, and the declaration of an array variable simply sets
aside space for a reference to an array instance. Actual array instances are created
dynamically at run time using the new operator. The new operation specifies the length
of the new array instance, which is then fixed for the lifetime of the instance. The indices
of the elements of an array range from 0 to Length - 1. The new operator
automatically initializes the elements of an array to their default value, which, for
example, is zero for all numeric types and null for all reference types.
The following example creates an array of int elements, initializes the array, and prints
the contents of the array.
C#Arrays, collections, and LINQ
Arrays
int[] a = new int[10];
for (int i = 0; i < a.Length; i++)
{
    a[i] = i * i;
}
for (int i = 0; i < a.Length; i++)This example creates and operates on a single-dimensional arr ay. C# also supports
multi-dimensional arr ays. The number of dimensions of an array type, also known as
the rank of the array type, is one plus the number of commas between the square
brackets of the array type. The following example allocates a single-dimensional, a two-
dimensional, and a three-dimensional array, respectively.
C#
The a1 array contains 10 elements, the a2 array contains 50 (10 × 5) elements, and the
a3 array contains 100 (10 × 5 × 2) elements. The element type of an array can be any
type, including an array type. An array with elements of an array type is sometimes
called a jagged arr ay because the lengths of the element arrays don't all have to be the
same. The following example allocates an array of arrays of int:
C#
The first line creates an array with three elements, each of type int[] and each with an
initial value of null. The next lines then initialize the three elements with references to
individual array instances of varying lengths.
Collection initializers provide a consistent syntax to initialize elements in an array or a
collection. The following example allocates and initializes an int[] with three elements.
C#
The length of the array is inferred from the expressions between [ and ]. The foreach
statement can be used to enumerate the elements of any collection. The following code
enumerates the array from the preceding example:{
    Console.WriteLine( $"a[{i}] = {a[i]}");
}
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
int[] a = [ 1, 2, 3];C#
The foreach statement uses the IEnumerable<T>  interface, so it can work with any
collection.
C# string int erpolation  enables you to format strings by defining expressions whose
results are placed in a format string. For example, the following example prints the
temperature on a given day from a set of weather data:
C#
An interpolated string is declared using the $ token. S tring interpolation evaluates the
expressions between { and }, then converts the result to a string, and replaces the
text between the brackets with the string result of the expression. The : in the first
expression, {weatherData.Date:MM-dd-yyyy} specifies the format str ing. In the preceding
example, it specifies that the date should be printed in "MM-dd-yyyy" format.
The C# language provides pattern mat ching  expressions to query the state of an object
and execute code based on that state. Y ou can inspect types and the values of
properties and fields to determine which action to take. Y ou can inspect the elements of
a list or array as well. The switch expression is the primary expression for pattern
matching.foreach (int item in a)
{
    Console.WriteLine(item);
}
String interpolation
Console.WriteLine( $"The low and high temperature on {weatherData.Date:MM-dd-
yyyy}");
Console.WriteLine( $"    was {weatherData.LowTemp}  and 
{weatherData.HighTemp} .");
// Output (similar to):
// The low and high temperature on 08-11-2020
//     was 5 and 30.
Pattern matching
Delegates and lambda expressionsA delegat e type  represents references to methods with a particular parameter list and
return type. Delegates make it possible to treat methods as entities that can be assigned
to variables and passed as parameters. Delegates are similar to the concept of function
pointers found in some other languages. Unlike function pointers, delegates are object-
oriented and type-safe.
The following example declares and uses a delegate type named Function.
C#
An instance of the Function delegate type can reference any method that takes a
double argument and returns a double value. The Apply method applies a given
Function to the elements of a double[], returning a double[] with the results. In the
Main method, Apply is used to apply three different functions to a double[].
A delegate can reference either a lambda expression to create an anonymous function
(such as (x) => x * x in the previous example), a static method (such as Math.Sin in
the previous example) or an instance method (such as m.Multiply in the previousdelegate  double Function (double x);
class Multiplier
{
    double _factor;
    public Multiplier (double factor) => _factor = factor;
    public double Multiply (double x) => x * _factor;
}
class DelegateExample
{
    static double[] Apply(double[] a, Function f )
    {
        var result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }
    public static void Main()
    {
        double[] a = { 0.0, 0.5, 1.0 };
        double[] squares = Apply(a, (x) => x * x);
        double[] sines = Apply(a, Math.Sin);
        Multiplier m = new(2.0);
        double[] doubles = Apply(a, m.Multiply);
    }
}example). A delegate that references an instance method also references a particular
object, and when the instance method is invoked through the delegate, that object
becomes this in the invocation.
Delegates can also be created using anonymous functions or lambda expressions, which
are "inline methods" that are created when declared. Anonymous functions can see the
local variables of the surrounding methods. The following example doesn't create a
class:
C#
A delegate doesn't know or care about the class of the method it references. The
referenced method must have the same parameters and return type as the delegate.
C# supports asynchronous programs with two keywords: async and await. You add the
async modifier to a method declaration to declare the method is asynchronous. The
await operator tells the compile