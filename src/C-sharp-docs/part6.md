Comparison operators ==, !=, <, >, <=, and >=
For information about pointer types, see Pointer types .
The unary & operator returns the address of its operand:
C#７ Note
Any operation with pointers requires an unsafe  context. The code that contains
unsafe blocks must be compiled with the AllowUnsafeBlocks  compiler option.
Address-of operator &
unsafe 
{ 
    int number = 27; 
    int* pointerToNumber = &number;  
    Console.WriteLine( $"Value of the variable: {number} "); 
    Console.WriteLine( $"Address of the variable:  
{(long)pointerToNumber:X} "); 
} 
// Output is similar to:  The operand of the & operator must be a fixed variable. Fixed variables are variables
that reside in storage locations that are unaffected by operation of the garbage
collector . In the preceding example, the local variable number is a fixed variable, because
it resides on the stack. V ariables that reside in storage locations that can be affected by
the garbage collector (for example, relocated) are called movable variables. Object fields
and array elements are examples of movable variables. Y ou can get the address of a
movable variable if you "fix", or "pin", it with a fixed  statement . The obtained address is
valid only inside the block of a fixed statement. The following example shows how to
use a fixed statement and the & operator:
C#
You can't get the address of a constant or a value.
For more information about fixed and movable variables, see the Fixed and moveable
variables  section of the C# language specification .
The binary & operator computes the logical AND  of its Boolean operands or the bitwise
logical AND  of its integral operands.
The unary pointer indirection operator * obtains the variable to which its operand
points. It's also known as the dereference operator. The operand of the * operator must
be of a pointer type.
C#// Value of the variable: 27  
// Address of the variable: 6C1457DBD4  
unsafe 
{ 
    byte[] bytes = { 1, 2, 3 }; 
    fixed (byte* pointerToFirst = &bytes[ 0]) 
    { 
        // The address stored in pointerToFirst  
        // is valid only inside this fixed statement block.  
    } 
} 
Pointer indirection operator *
unsafe 
{ 
    char letter = 'A'; You can't apply the * operator to an expression of type void*.
The binary * operator computes the product  of its numeric operands.
The -> operator combines pointer indirection  and member access . That is, if x is a
pointer of type T* and y is an accessible member of type T, an expression of the form
C#
is equivalent to
C#
The following example demonstrates the usage of the -> operator:
C#    char* pointerToLetter = &letter;  
    Console.WriteLine( $"Value of the `letter` variable: {letter} "); 
    Console.WriteLine( $"Address of the `letter` variable:  
{(long)pointerToLetter:X} "); 
    *pointerToLetter = 'Z'; 
    Console.WriteLine( $"Value of the `letter` variable after update:  
{letter} "); 
} 
// Output is similar to:  
// Value of the `letter` variable: A  
// Address of the `letter` variable: DCB977DDF4  
// Value of the `letter` variable after update: Z  
Pointer member access operator ->
x->y 
(*x).y 
public struct Coords 
{ 
    public int X; 
    public int Y; 
    public override  string ToString () => $"({X}, {Y})"; 
} 
public class PointerMemberAccessExample  
{ 
    public static unsafe void Main() You can't apply the -> operator to an expression of type void*.
For an expression p of a pointer type, a pointer element access of the form p[n] is
evaluated as *(p + n), where n must be of a type implicitly convertible to int, uint,
long, or ulong. For information about the behavior of the + operator with pointers, see
the Addition or subtraction of an integral value to or from a pointer  section.
The following example demonstrates how to access array elements with a pointer and
the [] operator:
C#
In the preceding example, a stackalloc  expression  allocates a block of memory on the
stack.    { 
        Coords coords;  
        Coords* p = &coords;  
        p->X = 3; 
        p->Y = 4; 
        Console.WriteLine(p->ToString());  // output: (3, 4)  
    } 
} 
Pointer element access operator []
unsafe 
{ 
    char* pointerToChars = stackalloc  char[123]; 
    for (int i = 65; i < 123; i++) 
    { 
        pointerToChars[i] = ( char)i; 
    } 
    Console.Write( "Uppercase letters: " ); 
    for (int i = 65; i < 91; i++) 
    { 
        Console.Write(pointerToChars[i]);  
    } 
} 
// Output:  
// Uppercase letters: ABCDEFGHIJKLMNOPQRSTUVWXYZ  
７ NoteYou can't use [] for pointer element access with an expression of type void*.
You can also use the [] operator for array element or indexer access .
You can perform the following arithmetic operations with pointers:
Add or subtract an integral value to or from a pointer
Subtract two pointers
Increment or decrement a pointer
You can't perform those operations with pointers of type void*.
For information about supported arithmetic operations with numeric types, see
Arithmetic operators .
For a pointer p of type T* and an expression n of a type implicitly convertible to int,
uint, long, or ulong, addition and subtraction are defined as follows:
Both p + n and n + p expressions produce a pointer of type T* that results from
adding n * sizeof(T) to the address given by p.
The p - n expression produces a pointer of type T* that results from subtracting
n * sizeof(T) from the address given by p.
The sizeof  operator  obtains the size of a type in bytes.
The following example demonstrates the usage of the + operator with a pointer:
C#The pointer element access operator doesn't check for out-of-bounds errors.
Pointer arithmetic operators
Addition or subtraction of an integral value to or from a
pointer
unsafe 
{ 
    const int Count = 3; 
    int[] numbers = new int[Count] { 10, 20, 30 }; 
    fixed (int* pointerToFirst = &numbers[ 0]) 
    { 
        int* pointerToLast = pointerToFirst + (Count - 1); For two pointers p1 and p2 of type T*, the expression p1 - p2 produces the difference
between the addresses given by p1 and p2 divided by sizeof(T). The type of the result
is long. That is, p1 - p2 is computed as ((long)(p1) - (long)(p2)) / sizeof(T).
The following example demonstrates the pointer subtraction:
C#
The ++ increment operator adds  1 to its pointer operand. The -- decrement operator
subtracts  1 from its pointer operand.
Both operators are supported in two forms: postfix ( p++ and p--) and prefix ( ++p and -
-p). The result of p++ and p-- is the value of p befor e the operation. The result of ++p
and --p is the value of p after the operation.
The following example demonstrates the behavior of both postfix and prefix increment
operators:
C#        Console.WriteLine( $"Value {*pointerToFirst}  at address  
{(long)pointerToFirst} "); 
        Console.WriteLine( $"Value {*pointerToLast}  at address  
{(long)pointerToLast} "); 
    } 
} 
// Output is similar to:  
// Value 10 at address 1818345918136  
// Value 30 at address 1818345918144  
Pointer subtraction
unsafe 
{ 
    int* numbers = stackalloc  int[] { 0, 1, 2, 3, 4, 5 }; 
    int* p1 = &numbers[ 1]; 
    int* p2 = &numbers[ 5]; 
    Console.WriteLine(p2 - p1);  // output: 4  
} 
Pointer increment and decrement
unsafe 
{ 
    int* numbers = stackalloc  int[] { 0, 1, 2 }; 
    int* p1 = &numbers[ 0]; You can use the ==, !=, <, >, <=, and >= operators to compare operands of any
pointer type, including void*. Those operators compare the addresses given by the two
operands as if they're unsigned integers.
For information about the behavior of those operators for operands of other types, see
the Equality operators  and Comparison operators  articles.
The following list orders pointer related operators starting from the highest precedence
to the lowest:
Postfix increment x++ and decrement x-- operators and the -> and [] operators
Prefix increment ++x and decrement --x operators and the & and * operators
Additive + and - operators
Comparison <, >, <=, and >= operators
Equality == and != operators
Use parentheses, (), to change the order of evaluation imposed by operator
precedence.
For the complete list of C# operators ordered by precedence level, see the Operator
precedence  section of the C# operators  article.
A user-defined type can't overload the pointer related operators &, *, ->, and [].    int* p2 = p1;  
    Console.WriteLine( $"Before operation: p1 - {(long)p1}, p2 - 
{(long)p2}"); 
    Console.WriteLine( $"Postfix increment of p1: {(long)(p1++)} "); 
    Console.WriteLine( $"Prefix increment of p2: {(long)(++p2)} "); 
    Console.WriteLine( $"After operation: p1 - {(long)p1}, p2 - {(long)p2}"); 
} 
// Output is similar to  
// Before operation: p1 - 816489946512, p2 - 816489946512  
// Postfix increment of p1: 816489946512  
// Prefix increment of p2: 816489946516  
// After operation: p1 - 816489946516, p2 - 816489946516  
Pointer comparison operators
Operator precedence
Operator overloadabilityFor more information, see the following sections of the C# language specification :
Fixed and moveable variables
The address-of operator
Pointer indirection
Pointer member access
Pointer element access
Pointer arithmetic
Pointer increment and decrement
Pointer comparison
C# reference
C# operators and expressions
Unsafe code, pointer types, and function pointers
unsafe keyword
fixed statement
stackalloc expression
sizeof operatorC# language specification
See alsoAssignment operators (C# reference)
Article •07/14/2023
The assignment operator = assigns the value of its right-hand operand to a variable, a
property , or an indexer  element given by its left-hand operand. The result of an
assignment expression is the value assigned to the left-hand operand. The type of the
right-hand operand must be the same as the type of the left-hand operand or implicitly
convertible to it.
The assignment operator = is right-associative, that is, an expression of the form
C#
is evaluated as
C#
The following example demonstrates the usage of the assignment operator with a local
variable, a property, and an indexer element as its left-hand operand:
C#a = b = c
a = (b = c)
var numbers = new List<double>() { 1.0, 2.0, 3.0 };
Console.WriteLine(numbers.Capacity);
numbers.Capacity = 100;
Console.WriteLine(numbers.Capacity);
// Output:
// 4
// 100
int newFirstElement;
double originalFirstElement = numbers[ 0];
newFirstElement = 5;
numbers[ 0] = newFirstElement;
Console.WriteLine(originalFirstElement);
Console.WriteLine(numbers[ 0]);
// Output:
// 1
// 5The left-hand operand of an assignment receives the value of the right-hand operand.
When the operands are of value types , assignment copies the contents of the right-
hand operand. When the operands are of reference types , assignment copies the
reference to the object.
This is called value assignment : the value is assigned.
Ref assignment  = ref makes its left-hand operand an alias to the right-hand operand,
as the following example demonstrates:
C#
In the preceding example, the local reference variable  arrayElement is initialized as an
alias to the first array element. Then, it's ref reassigned to refer to the last array
element. As it's an alias, when you update its value with an ordinary assignment
operator =, the corresponding array element is also updated.
The left-hand operand of ref assignment can be a local reference variable , a ref field ,
and a ref, out, or in method parameter. Both operands must be of the same type.
For a binary operator op, a compound assignment expression of the form
C#ref assignment
void Display(double[] s) => Console.WriteLine( string.Join(" ", s));
double[] arr = { 0.0, 0.0, 0.0 };
Display(arr);
ref double arrayElement = ref arr[0];
arrayElement = 3.0;
Display(arr);
arrayElement = ref arr[arr.Length - 1];
arrayElement = 5.0;
Display(arr);
// Output:
// 0 0 0
// 3 0 0
// 3 0 5
Compound assignmentis equivalent to
C#
except that x is only evaluated once.
Compound assignment is supported by arithmetic , Boolean logical , and bitwise logical
and shift  operators.
You can use the null-coalescing assignment operator ??= to assign the value of its right-
hand operand to its left-hand operand only if the left-hand operand evaluates to null.
For more information, see the ?? and ??= operators  article.
A user-defined type can't overload  the assignment operator. However, a user-defined
type can define an implicit conversion to another type. That way, the value of a user-
defined type can be assigned to a variable, a property, or an indexer element of another
type. For more information, see User-defined conversion operators .
A user-defined type can't explicitly overload a compound assignment operator.
However, if a user-defined type overloads a binary operator op, the op= operator, if it
exists, is also implicitly overloaded.
For more information, see the Assignment operators  section of the C# language
specification .
C# reference
C# operators and expressionsx op= y
x = x op y
Null-coalescing assignment
Operator overloadability
C# language specification
See alsoref keyword
Use compound assignment (style rules IDE0054 and IDE0074)
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
 Provide product feedbackLambda expressions and anonymous
functions
Article •03/09/2023
You use a lambda expr ession  to create an anonymous function. Use the lambda
declaration operator => to separate the lambda's parameter list from its body. A
lambda expression can be of any of the following two forms:
Expression lambda  that has an expression as its body:
C#
Statement lambda  that has a statement block as its body:
C#
To create a lambda expression, you specify input parameters (if any) on the left side of
the lambda operator and an expression or a statement block on the other side.
Any lambda expression can be converted to a delegate  type. The delegate type to which
a lambda expression can be converted is defined by the types of its parameters and
return value. If a lambda expression doesn't return a value, it can be converted to one of
the Action delegate types; otherwise, it can be converted to one of the Func delegate
types. For example, a lambda expression that has two parameters and returns no value
can be converted to an Action<T1,T2>  delegate. A lambda expression that has one
parameter and returns a value can be converted to a Func<T,TR esult>  delegate. In the
following example, the lambda expression x => x * x, which specifies a parameter
that's named x and returns the value of x squared, is assigned to a variable of a
delegate type:
C#(input-parameters) => expression
(input-parameters) => { <sequence-of-statements> }
Func<int, int> square = x => x * x;
Console.WriteLine(square( 5));
// Output:
// 25Expression lambdas can also be converted to the expression tree  types, as the following
example shows:
C#
You can use lambda expressions in any code that requires instances of delegate types or
expression trees, for example as an argument to the Task.Run(Action)  method to pass
the code that should be executed in the background. Y ou can also use lambda
expressions when you write LINQ in C# , as the following example shows:
C#
When you use method-based syntax to call the Enumerable.Select  method in the
System.Linq.Enumerable  class, for example in LINQ to Objects and LINQ to XML, the
parameter is a delegate type System.Func<T,TR esult> . When you call the
Queryable.Select  method in the System.Linq.Queryable  class, for example in LINQ to
SQL, the parameter type is an expression tree type
Expression<Func<T Source,TR esult>> . In both cases, you can use the same lambda
expression to specify the parameter value. That makes the two Select calls to look
similar although in fact the type of objects created from the lambdas is different.
A lambda expression with an expression on the right side of the => operator is called an
expression lambda . An expression lambda returns the result of the expression and takes
the following basic form:
C#System.Linq.Expressions.Expression<Func< int, int>> e = x => x * x;
Console.WriteLine(e);
// Output:
// x => (x * x)
int[] numbers = { 2, 3, 4, 5 };
var squaredNumbers = numbers.Select(x => x * x);
Console.WriteLine( string.Join(" ", squaredNumbers));
// Output:
// 4 9 16 25
Expression lambdas
(input-parameters) => expressionThe body of an expression lambda can consist of a method call. However, if you're
creating expression trees  that are evaluated outside the context of the .NET Common
Language Runtime (CLR), such as in SQL Server, you shouldn't use method calls in
lambda expressions. The methods have no meaning outside the context of the .NET
Common Language Runtime (CLR).
A statement lambda resembles an expression lambda except that its statements are
enclosed in braces:
C#
The body of a statement lambda can consist of any number of statements; however, in
practice there are typically no more than two or three.
C#
You can't use statement lambdas to create expression trees.
You enclose input parameters of a lambda expression in parentheses. Specify zero input
parameters with empty parentheses:
C#
If a lambda expression has only one input parameter, parentheses are optional:
C#Statement lambdas
(input-parameters) => { <sequence-of-statements> }
Action<string> greet = name =>
{
    string greeting = $"Hello {name}!";
    Console.WriteLine(greeting);
};
greet("World");
// Output:
// Hello World!
Input parameters of a lambda expression
Action line = () => Console.WriteLine();Two or more input parameters are separated by commas:
C#
Sometimes the compiler can't infer the types of input parameters. Y ou can specify the
types explicitly as shown in the following example:
C#
Input parameter types must be all explicit or all implicit; otherwise, a CS0748  compiler
error occurs.
You can use discards  to specify two or more input parameters of a lambda expression
that aren't used in the expression:
C#
Lambda discard parameters may be useful when you use a lambda expression to
provide an event handler .
Beginning with C# 12, you can provide default v alues  for parameters on lambda
expressions. The syntax and the restrictions on default parameter values are the same as
for methods and local functions. The following example declares a lambda expression
with a default parameter, then calls it once using the default and once with two explicit
parameters:
C#Func<double, double> cube = x => x * x * x;
Func<int, int, bool> testForEquality = (x, y) => x == y;
Func<int, string, bool> isTooLong = ( int x, string s) => s.Length > x;
Func<int, int, int> constant = (_, _) => 42;
７ Note
For backwards compatibility, if only a single input parameter is named _, then,
within a lambda expression, _ is treated as the name of that parameter.You can also declare lambda expressions with params arrays as parameters:
C#
As part of these updates, when a method group that has a default parameter is assigned
to a lambda expression, that lambda expression also has the same default parameter. A
method group with a params array parameter can also be assigned to a lambda
expression.
Lambda expressions with default parameters or params arrays as parameters don't have
natural types that correspond to Func<> or Action<> types. However, you can define
delegate types that include default parameter values:
C#
Or, you can use implicitly typed variables with var declarations to define the delegate
type. The compiler synthesizes the correct delegate type.
For more information on see the feature spec for default parameters on lambda
expressions .var IncrementBy = ( int source, int increment = 1) => source + increment;
Console.WriteLine(IncrementBy( 5)); // 6
Console.WriteLine(IncrementBy( 5, 2)); // 7
var sum = ( params int[] values) =>
{
    int sum = 0;
    foreach (var value in values) 
        sum += value;
    
    return sum;
};
var empty = sum();
Console.WriteLine(empty); // 0
var sequence = new[] { 1, 2, 3, 4, 5 };
var total = sum(sequence);
Console.WriteLine(total); // 15
delegate  int IncrementByDelegate (int source, int increment = 1);
delegate  int SumDelegate (params int[] values );You can easily create lambda expressions and statements that incorporate asynchronous
processing by using the async  and await  keywords. For example, the following Windows
Forms example contains an event handler that calls and awaits an async method,
ExampleMethodAsync.
C#
You can add the same event handler by using an async lambda. T o add this handler, add
an async modifier before the lambda parameter list, as the following example shows:
C#Async lambdas
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += button1_Click;
    }
    private async void button1_Click (object sender, EventArgs e )
    {
        await ExampleMethodAsync();
        textBox1.Text += "\r\nControl returned to Click event handler.\n" ;
    }
    private async Task ExampleMethodAsync ()
    {
        // The following line simulates a task-returning asynchronous  
process.
        await Task.Delay( 1000);
    }
}
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += async (sender, e) =>
        {
            await ExampleMethodAsync();
            textBox1.Text += "\r\nControl returned to Click event  
handler.\n" ;
        };
    }
    private async Task ExampleMethodAsync ()For more information about how to create and use async methods, see Asynchronous
Programming with async and await .
The C# language provides built-in support for tuples . You can provide a tuple as an
argument to a lambda expression, and your lambda expression can also return a tuple.
In some cases, the C# compiler uses type inference to determine the types of tuple
components.
You define a tuple by enclosing a comma-delimited list of its components in
parentheses. The following example uses tuple with three components to pass a
sequence of numbers to a lambda expression, which doubles each value and returns a
tuple with three components that contains the result of the multiplications.
C#
Ordinarily, the fields of a tuple are named Item1, Item2, and so on. Y ou can, however,
define a tuple with named components, as the following example does.
C#
For more information about C# tuples, see Tuple types .    {
        // The following line simulates a task-returning asynchronous  
process.
        await Task.Delay( 1000);
    }
}
Lambda expressions and tuples
Func<(int, int, int), (int, int, int)> doubleThem = ns => ( 2 * ns.Item1, 2 * 
ns.Item2, 2 * ns.Item3);
var numbers = ( 2, 3, 4);
var doubledNumbers = doubleThem(numbers);
Console.WriteLine( $"The set {numbers}  doubled: {doubledNumbers} ");
// Output:
// The set (2, 3, 4) doubled: (4, 6, 8)
Func<(int n1, int n2, int n3), (int, int, int)> doubleThem = ns => ( 2 * 
ns.n1, 2 * ns.n2, 2 * ns.n3);
var numbers = ( 2, 3, 4);
var doubledNumbers = doubleThem(numbers);
Console.WriteLine( $"The set {numbers}  doubled: {doubledNumbers} ");LINQ to Objects, among other implementations, has an input parameter whose type is
one of the Func<TR esult>  family of generic delegates. These delegates use type
parameters to define the number and type of input parameters, and the return type of
the delegate. Func delegates are useful for encapsulating user-defined expressions that
are applied to each element in a set of source data. For example, consider the
Func<T,TR esult>  delegate type:
C#
The delegate can be instantiated as a Func<int, bool> instance where int is an input
parameter and bool is the return value. The return value is always specified in the last
type parameter. For example, Func<int, string, bool> defines a delegate with two
input parameters, int and string, and a return type of bool. The following Func
delegate, when it's invoked, returns Boolean value that indicates whether the input
parameter is equal to five:
C#
You can also supply a lambda expression when the argument type is an
Expression<TDelegate> , for example in the standard query operators that are defined in
the Queryable  type. When you specify an Expression<TDelegate>  argument, the lambda
is compiled to an expression tree.
The following example uses the Count  standard query operator:
C#
The compiler can infer the type of the input parameter, or you can also specify it
explicitly. This particular lambda expression counts those integers ( n) which when
divided by two have a remainder of 1.Lambdas with the standard query operators
public delegate  TResult Func< in T, out TResult>(T arg)
Func<int, bool> equalsFive = x => x == 5;
bool result = equalsFive( 4);
Console.WriteLine(result);   // False
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
int oddNumbers = numbers.Count(n => n % 2 == 1);
Console.WriteLine( $"There are {oddNumbers}  odd numbers in {string.Join(" ", 
numbers)} ");The following example produces a sequence that contains all elements in the numbers
array that precede the 9, because that's the first number in the sequence that doesn't
meet the condition:
C#
The following example specifies multiple input parameters by enclosing them in
parentheses. The method returns all the elements in the numbers array until it finds a
number whose value is less than its ordinal position in the array:
C#
You don't use lambda expressions directly in query expressions , but you can use them in
method calls within query expressions, as the following example shows:
C#int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
var firstNumbersLessThanSix = numbers.TakeWhile(n => n < 6);
Console.WriteLine( string.Join(" ", firstNumbersLessThanSix));
// Output:
// 5 4 1 3
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
var firstSmallNumbers = numbers.TakeWhile((n, index) => n >= index);
Console.WriteLine( string.Join(" ", firstSmallNumbers));
// Output:
// 5 4
var numberSets = new List<int[]>
{
    new[] { 1, 2, 3, 4, 5 },
    new[] { 0, 0, 0 },
    new[] { 9, 8 },
    new[] { 1, 0, 1, 0, 1, 0, 1, 0 }
};
var setsWithManyPositives = 
    from numberSet in numberSets
    where numberSet.Count(n => n > 0) > 3
    select numberSet;
foreach (var numberSet in setsWithManyPositives)
{
    Console.WriteLine( string.Join(" ", numberSet));
}
// Output:When writing lambdas, you often don't have to specify a type for the input parameters
because the compiler can infer the type based on the lambda body, the parameter
types, and other factors as described in the C# language specification. For most of the
standard query operators, the first input is the type of the elements in the source
sequence. If you're querying an IEnumerable<Customer>, then the input variable is
inferred to be a Customer object, which means you have access to its methods and
properties:
C#
The general rules for type inference for lambdas are as follows:
The lambda must contain the same number of parameters as the delegate type.
Each input parameter in the lambda must be implicitly convertible to its
corresponding delegate parameter.
The return value of the lambda (if any) must be implicitly convertible to the
delegate's return type.
A lambda expression in itself doesn't have a type because the common type system has
no intrinsic concept of "lambda expression." However, it's sometimes convenient to
speak informally of the "type" of a lambda expression. That informal "type" refers to the
delegate type or Expression  type to which the lambda expression is converted.
Beginning with C# 10, a lambda expression may have a natur al type . Instead of forcing
you to declare a delegate type, such as Func<...> or Action<...> for a lambda
expression, the compiler may infer the delegate type from the lambda expression. For
example, consider the following declaration:
C#// 1 2 3 4 5
// 1 0 1 0 1 0 1 0
Type inference in lambda expressions
customers.Where(c => c.City == "London" );
Natural type of a lambda expression
var parse = ( string s) => int.Parse(s);The compiler can infer parse to be a Func<string, int>. The compiler chooses an
available Func or Action delegate, if a suitable one exists. Otherwise, it synthesizes a
delegate type. For example, the delegate type is synthesized if the lambda expression
has ref parameters. When a lambda expression has a natural type, it can be assigned to
a less explicit type, such as System.Object  or System.Delegate :
C#
Method groups (that is, method names without parameter lists) with exactly one
overload have a natural type:
C#
If you assign a lambda expression to System.Linq.Expressions.LambdaExpression , or
System.Linq.Expressions.Expression , and the lambda has a natural delegate type, the
expression has a natural type of System.Linq.Expressions.Expression<TDelegate> , with
the natural delegate type used as the argument for the type parameter:
C#
Not all lambda expressions have a natural type. Consider the following declaration:
C#
The compiler can't infer a parameter type for s. When the compiler can't infer a natural
type, you must declare the type:
C#object parse = ( string s) => int.Parse(s);   // Func<string, int>
Delegate parse = ( string s) => int.Parse(s); // Func<string, int>
var read = Console.Read; // Just one overload; Func<int> inferred
var write = Console.Write; // ERROR: Multiple overloads, can't choose
LambdaExpression parseExpr = ( string s) => int.Parse(s); // 
Expression<Func<string, int>>
Expression parseExpr = ( string s) => int.Parse(s);       // 
Expression<Func<string, int>>
var parse = s => int.Parse(s); // ERROR: Not enough type info in the lambda
Func<string, int> parse = s => int.Parse(s);Typically, the return type of a lambda expression is obvious and inferred. For some
expressions that doesn't work:
C#
Beginning with C# 10, you can specify the return type of a lambda expression before the
input parameters. When you specify an explicit return type, you must parenthesize the
input parameters:
C#
Beginning with C# 10, you can add attributes to a lambda expression and its
parameters. The following example shows how to add attributes to a lambda expression:
C#
You can also add attributes to the input parameters or return value, as the following
example shows:
C#
As the preceding examples show, you must parenthesize the input parameters when you
add attributes to a lambda expression or its parameters.Explicit return type
var choose = ( bool b) => b ? 1 : "two"; // ERROR: Can't infer return type
var choose = object (bool b) => b ? 1 : "two"; // Func<bool, object>
Attributes
Func<string?, int?> parse = [ProvidesNullCheck] (s) => (s is not null) ? 
int.Parse(s) : null;
var concat = ([DisallowNull] string a, [DisallowNull] string b) => a + b;
var inc = [ return: NotNullifNotNull( nameof(s))] (int? s) => s.HasValue ? s++  
: null;
） Impor tantLambdas can refer to outer variables . These outer variables  are the variables that are in
scope in the method that defines the lambda expression, or in scope in the type that
contains the lambda expression. V ariables that are captured in this manner are stored
for use in the lambda expression even if the variables would otherwise go out of scope
and be garbage collected. An outer variable must be definitely assigned before it can be
consumed in a lambda expression. The following example demonstrates these rules:
C#Lambda expressions are invoked through the underlying delegate type. That is
different than methods and local functions. The delegate's Invoke method doesn't
check attributes on the lambda expression. Attributes don't have any effect when
the lambda expression is invoked. Attributes on lambda expressions are useful for
code analysis, and can be discovered via reflection. One consequence of this
decision is that the System.Diagnostics.ConditionalA ttribut e cannot be applied to
a lambda expression.
Capture of outer variables and variable scope in
lambda expressions
public static class VariableScopeWithLambdas
{
    public class VariableCaptureGame
    {
        internal  Action< int>? updateCapturedLocalVariable;
        internal  Func<int, bool>? isEqualToCapturedLocalVariable;
        public void Run(int input)
        {
            int j = 0;
            updateCapturedLocalVariable = x =>
            {
                j = x;
                bool result = j > input;
                Console.WriteLine( $"{j} is greater than {input}: {result} ");
            };
            isEqualToCapturedLocalVariable = x => x == j;
            Console.WriteLine( $"Local variable before lambda invocation: 
{j}");
            updateCapturedLocalVariable( 10);
            Console.WriteLine( $"Local variable after lambda invocation: 
{j}");
        }The following rules apply to variable scope in lambda expressions:
A variable that is captured won't be garbage-collected until the delegate that
references it becomes eligible for garbage collection.
Variables introduced within a lambda expression aren't visible in the enclosing
method.
A lambda expression can't directly capture an in, ref, or out parameter from the
enclosing method.
A return  statement in a lambda expression doesn't cause the enclosing method to
return.
A lambda expression can't contain a goto , break , or continue  statement if the
target of that jump statement is outside the lambda expression block. It's also an
error to have a jump statement outside the lambda expression block if the target is
inside the block.
You can apply the static modifier to a lambda expression to prevent unintentional
capture of local variables or instance state by the lambda:
C#    }
    public static void Main()
    {
        var game = new VariableCaptureGame();
        int gameInput = 5;
        game.Run(gameInput);
        int jTry = 10;
        bool result = game.isEqualToCapturedLocalVariable!(jTry);
        Console.WriteLine( $"Captured local variable is equal to {jTry}: 
{result} ");
        int anotherJ = 3;
        game.updateCapturedLocalVariable!(anotherJ);
        bool equalToAnother = game.isEqualToCapturedLocalVariable(anotherJ);
        Console.WriteLine( $"Another lambda observes a new value of captured  
variable: {equalToAnother} ");
    }
    // Output:
    // Local variable before lambda invocation: 0
    // 10 is greater than 5: True
    // Local variable after lambda invocation: 10
    // Captured local variable is equal to 10: True
    // 3 is greater than 5: False
    // Another lambda observes a new value of captured variable: True
}A static lambda can't capture local variables or instance state from enclosing scopes, but
may reference static members and constant definitions.
For more information, see the Anonymous function expressions  section of the C#
language specification .
For more information about these features, see the following feature proposal notes:
Lambda discard parameters
Static anonymous functions
Lambda improvements (C# 10)
Use local function instead of lambda (style rule IDE0039)
C# reference
C# operators and expressions
LINQ (Language-Integrated Query)
Expression trees
Local functions vs. lambda expressions
LINQ sample queries
XQuery sample
101 LINQ samplesFunc<double, double> square = static x => x * x;
C# language specification
See also
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
 Provide product feedbackPattern matching - the is and switch
expressions, and operators and, or and
not in patterns
Article •01/31/2023
You use the is expression , the switch statement  and the switch expression  to match an
input expression against any number of characteristics. C# supports multiple patterns,
including declaration, type, constant, relational, property, list, var, and discard. P atterns
can be combined using Boolean logic keywords and, or, and not.
The following C# expressions and statements support pattern matching:
is expression
switch statement
switch expression
In those constructs, you can match an input expression against any of the following
patterns:
Declaration pattern : to check the run-time type of an expression and, if a match
succeeds, assign an expression result to a declared variable.
Type pattern : to check the run-time type of an expression.
Constant pattern : to test if an expression result equals a specified constant.
Relational patterns : to compare an expression result with a specified constant.
Logical patterns : to test if an expression matches a logical combination of patterns.
Property pattern : to test if an expression's properties or fields match nested
patterns.
Positional pattern : to deconstruct an expression result and test if the resulting
values match nested patterns.
var pattern : to match any expression and assign its result to a declared variable.
Discard pattern : to match any expression.
List patterns : to test if sequence elements match corresponding nested patterns.
Introduced in C# 11.
Logical , property , positional , and list patterns are recursive patterns. That is, they can
contain nested patterns.
For the example of how to use those patterns to build a data-driven algorithm, see
Tutorial: Use pattern matching to build type-driven and data-driven algorithms .You use declaration and type patterns to check if the run-time type of an expression is
compatible with a given type. With a declaration pattern, you can also declare a new
local variable. When a declaration pattern matches an expression, that variable is
assigned a converted expression result, as the following example shows:
C#
A declar ation p attern with type T matches an expression when an expression result is
non-null and any of the following conditions are true:
The run-time type of an expression result is T.
The run-time type of an expression result derives from type T, implements
interface T, or another implicit reference conversion  exists from it to T. The
following example demonstrates two cases when this condition is true:
C#
In the preceding example, at the first call to the GetSourceLabel method, the first
pattern matches an argument value because the argument's run-time type int[]
derives from the Array  type. At the second call to the GetSourceLabel method, the
argument's run-time type List<T>  doesn't derive from the Array  type but
implements the ICollection<T>  interface.Declaration and type patterns
object greeting = "Hello, World!" ;
if (greeting is string message)
{
    Console.WriteLine(message.ToLower());  // output: hello, world!
}
var numbers = new int[] { 10, 20, 30 };
Console.WriteLine(GetSourceLabel(numbers));  // output: 1
var letters = new List<char> { 'a', 'b', 'c', 'd' };
Console.WriteLine(GetSourceLabel(letters));  // output: 2
static int GetSourceLabel<T>(IEnumerable<T> source) => source switch
{
    Array array => 1,
    ICollection<T> collection => 2,
    _ => 3,
};The run-time type of an expression result is a nullable value type  with the
underlying type T.
A boxing  or unboxing  conversion exists from the run-time type of an expression
result to type T.
The following example demonstrates the last two conditions:
C#
If you want to check only the type of an expression, you can use a discard _ in place of
a variable's name, as the following example shows:
C#
For that purpose you can use a type p attern, as the following example shows:
C#int? xNullable = 7;
int y = 23;
object yBoxed = y;
if (xNullable is int a && yBoxed is int b)
{
    Console.WriteLine(a + b);  // output: 30
}
public abstract  class Vehicle {}
public class Car : Vehicle {}
public class Truck : Vehicle {}
public static class TollCalculator
{
    public static decimal CalculateToll (this Vehicle vehicle ) => vehicle 
switch
    {
        Car _ => 2.00m,
        Truck _ => 7.50m,
        null => throw new ArgumentNullException( nameof(vehicle)),
        _ => throw new ArgumentException( "Unknown type of a vehicle" , 
nameof(vehicle)),
    };
}
public static decimal CalculateToll (this Vehicle vehicle ) => vehicle switch
{
    Car => 2.00m,
    Truck => 7.50m,
    null => throw new ArgumentNullException( nameof(vehicle)),Like a declaration pattern, a type pattern matches an expression when an expression
result is non-null and its run-time type satisfies any of the conditions listed above.
To check for non-null, you can use a negated  null constant pattern , as the following
example shows:
C#
For more information, see the Declaration pattern  and Type pattern  sections of the
feature proposal notes.
You use a constant p attern to test if an expression result equals a specified constant, as
the following example shows:
C#
In a constant pattern, you can use any constant expression, such as:
an integer  or floating-point  numerical literal
a char
a string  literal.
a Boolean value true or false    _ => throw new ArgumentException( "Unknown type of a vehicle" , 
nameof(vehicle)),
};
if (input is not null)
{
    // ...
}
Constant pattern
public static decimal GetGroupTicketPrice (int visitorCount ) => visitorCount 
switch
{
    1 => 12.0m,
    2 => 20.0m,
    3 => 27.0m,
    4 => 32.0m,
    0 => 0.0m,
    _ => throw new ArgumentException( $"Not supported number of visitors: 
{visitorCount} ", nameof(visitorCount)),
};an enum  value
the name of a declared const  field or local
null
The expression must be a type that is convertible to the constant type, with one
exception: An expression whose type is Span<char> or ReadOnlySpan<char> can be
matched against constant strings in C# 11 and later versions.
Use a constant pattern to check for null, as the following example shows:
C#
The compiler guarantees that no user-overloaded equality operator == is invoked when
expression x is null is evaluated.
You can use a negated  null constant pattern to check for non-null, as the following
example shows:
C#
For more information, see the Constant pattern  section of the feature proposal note.
You use a relational p attern to compare an expression result with a constant, as the
following example shows:
C#if (input is null)
{
    return;
}
if (input is not null)
{
    // ...
}
Relational patterns
Console.WriteLine(Classify( 13));  // output: Too high
Console.WriteLine(Classify( double.NaN));  // output: Unknown
Console.WriteLine(Classify( 2.4));  // output: Acceptable
static string Classify (double measurement ) => measurement switch
{In a relational pattern, you can use any of the relational operators  <, >, <=, or >=. The
right-hand part of a relational pattern must be a constant expression. The constant
expression can be of an integer , floating-point , char, or enum  type.
To check if an expression result is in a certain range, match it against a conjunctive and
pattern , as the following example shows:
C#
If an expression result is null or fails to convert to the type of a constant by a nullable
or unboxing conversion, a relational pattern doesn't match an expression.
For more information, see the Relational patterns  section of the feature proposal note.
You use the not, and, and or pattern combinators to create the following logical
patterns:
Negation  not pattern that matches an expression when the negated pattern
doesn't match the expression. The following example shows how you can negate a
constant  null pattern to check if an expression is non-null:    < -4.0 => "Too low" ,
    > 10.0 => "Too high" ,
    double.NaN => "Unknown" ,
    _ => "Acceptable" ,
};
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 3, 14)));  // output:  
spring
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 7, 19)));  // output:  
summer
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 2, 17)));  // output:  
winter
static string GetCalendarSeason (DateTime date ) => date.Month switch
{
    >= 3 and < 6 => "spring" ,
    >= 6 and < 9 => "summer" ,
    >= 9 and < 12 => "autumn" ,
    12 or (>= 1 and < 3) => "winter" ,
    _ => throw new ArgumentOutOfRangeException( nameof(date), $"Date with  
unexpected month: {date.Month} ."),
};
Logical patternsC#
Conjunctiv e and pattern that matches an expression when both patterns match the
expression. The following example shows how you can combine relational patterns
to check if a value is in a certain range:
C#
Disjunctiv e or pattern that matches an expression when either pattern matches
the expression, as the following example shows:
C#if (input is not null)
{
    // ...
}
Console.WriteLine(Classify( 13));  // output: High
Console.WriteLine(Classify( -100));  // output: Too low
Console.WriteLine(Classify( 5.7));  // output: Acceptable
static string Classify (double measurement ) => measurement switch
{
    < -40.0 => "Too low" ,
    >= -40.0 and < 0 => "Low",
    >= 0 and < 10.0 => "Acceptable" ,
    >= 10.0 and < 20.0 => "High",
    >= 20.0 => "Too high" ,
    double.NaN => "Unknown" ,
};
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 1, 19)));  // 
output: winter
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 10, 9)));  // 
output: autumn
Console.WriteLine(GetCalendarSeason( new DateTime( 2021, 5, 11)));  // 
output: spring
static string GetCalendarSeason (DateTime date ) => date.Month switch
{
    3 or 4 or 5 => "spring" ,
    6 or 7 or 8 => "summer" ,
    9 or 10 or 11 => "autumn" ,
    12 or 1 or 2 => "winter" ,
    _ => throw new ArgumentOutOfRangeException( nameof(date), $"Date 
with unexpected month: {date.Month} ."),
};As the preceding example shows, you can repeatedly use the pattern combinators in a
pattern.
The pattern combinators are ordered from the highest precedence to the lowest as
follows:
not
and
or
When a logical pattern is a pattern of an is expression, the precedence of logical
pattern combinators is higher  than the precedence of logical operators (both bitwise
logical  and Boolean logical  operators). Otherwise, the precedence of logical pattern
combinators is lower than the precedence of logical and conditional logical operators.
For the complete list of C# operators ordered by precedence level, see the Operator
precedence  section of the C# operators  article.
To explicitly specify the precedence, use parentheses, as the following example shows:
C#
For more information, see the Pattern combinators  section of the feature proposal note.
You use a property pattern to match an expression's properties or fields against nested
patterns, as the following example shows:
C#Precedence and order of checking
static bool IsLetter (char c) => c is (>= 'a' and <= 'z') or (>= 'A' and <= 
'Z');
７ Note
The order in which patterns are checked is undefined. At run time, the right-hand
nested patterns of or and and patterns can be checked first.
Property pattern
static bool IsConferenceDay (DateTime date ) => date is { Year: 2020, Month: A property pattern matches an expression when an expression result is non-null and
every nested pattern matches the corresponding property or field of the expression
result.
You can also add a run-time type check and a variable declaration to a property pattern,
as the following example shows:
C#
A property pattern is a recursive pattern. That is, you can use any pattern as a nested
pattern. Use a property pattern to match parts of data against nested patterns, as the
following example shows:
C#
The preceding example uses the or pattern combinator  and record types .
Beginning with C# 10, you can reference nested properties or fields within a property
pattern. This capability is known as an extended pr operty pattern. For example, you can
refactor the method from the preceding example into the following equivalent code:5, Day: 19 or 20 or 21 };
Console.WriteLine(TakeFive( "Hello, world!" ));  // output: Hello
Console.WriteLine(TakeFive( "Hi!"));  // output: Hi!
Console.WriteLine(TakeFive( new[] { '1', '2', '3', '4', '5', '6', '7' }));  
// output: 12345
Console.WriteLine(TakeFive( new[] { 'a', 'b', 'c' }));  // output: abc
static string TakeFive (object input) => input switch
{
    string { Length: >= 5 } s => s.Substring( 0, 5),
    string s => s,
    ICollection< char> { Count: >= 5 } symbols => new 
string(symbols.Take( 5).ToArray()),
    ICollection< char> symbols => new string(symbols.ToArray()),
    null => throw new ArgumentNullException( nameof(input)),
    _ => throw new ArgumentException( "Not supported input type." ),
};
public record Point(int X, int Y);
public record Segment(Point Start, Point End );
static bool IsAnyEndOnXAxis (Segment segment ) =>
    segment is { Start: { Y: 0 } } or { End: { Y: 0 } };C#
For more information, see the Property pattern  section of the feature proposal note and
the Extended property patterns  feature proposal note.
You use a positional p attern to deconstruct an expression result and match the resulting
values against the corresponding nested patterns, as the following example shows:
C#
At the preceding example, the type of an expression contains the Deconstruct  method,
which is used to deconstruct an expression result. Y ou can also match expressions of
tuple types  against positional patterns. In that way, you can match multiple inputs
against various patterns, as the following example shows:
C#static bool IsAnyEndOnXAxis (Segment segment ) =>
    segment is { Start.Y: 0 } or { End.Y: 0 };
 Tip
You can use the Simplif y proper ty pattern (IDE0170)  style rule to improve code
readability by suggesting places to use extended property patterns.
Positional pattern
public readonly  struct Point
{
    public int X { get; }
    public int Y { get; }
    public Point(int x, int y) => (X, Y) = (x, y);
    public void Deconstruct (out int x, out int y) => (x, y) = (X, Y);
}
static string Classify (Point point ) => point switch
{
    (0, 0) => "Origin" ,
    (1, 0) => "positive X basis end" ,
    (0, 1) => "positive Y basis end" ,
    _ => "Just a point" ,
};The preceding example uses relational  and logical  patterns.
You can use the names of tuple elements and Deconstruct parameters in a positional
pattern, as the following example shows:
C#
You can also extend a positional pattern in any of the following ways:
Add a run-time type check and a variable declaration, as the following example
shows:
C#static decimal GetGroupTicketPriceDiscount (int groupSize, DateTime  
visitDate )
    => (groupSize, visitDate.DayOfWeek) switch
    {
        (<= 0, _) => throw new ArgumentException( "Group size must be  
positive." ),
        (_, DayOfWeek.Saturday or DayOfWeek.Sunday) => 0.0m,
        (>= 5 and < 10, DayOfWeek.Monday) => 20.0m,
        (>= 10, DayOfWeek.Monday) => 30.0m,
        (>= 5 and < 10, _) => 12.0m,
        (>= 10, _) => 15.0m,
        _ => 0.0m,
    };
var numbers = new List<int> { 1, 2, 3 };
if (SumAndCount(numbers) is (Sum: var sum, Count: > 0))
{
    Console.WriteLine( $"Sum of [ {string.Join(" ", numbers)} ] is {sum}");  // 
output: Sum of [1 2 3] is 6
}
static (double Sum, int Count) SumAndCount(IEnumerable< int> numbers)
{
    int sum = 0;
    int count = 0;
    foreach (int number in numbers)
    {
        sum += number;
        count++;
    }
    return (sum, count);
}
public record Point2D(int X, int Y);
public record Point3D(int X, int Y, int Z);The preceding example uses positional records  that implicitly provide the
Deconstruct method.
Use a property pattern  within a positional pattern, as the following example shows:
C#
Combine two preceding usages, as the following example shows:
C#
A positional pattern is a recursive pattern. That is, you can use any pattern as a nested
pattern.
For more information, see the Positional pattern  section of the feature proposal note.
You use a var pattern to match any expression, including null, and assign its result to a
new local variable, as the following example shows:
C#static string PrintIfAllCoordinatesArePositive (object point) => point 
switch
{
    Point2D (> 0, > 0) p => p.ToString(),
    Point3D (> 0, > 0, > 0) p => p.ToString(),
    _ => string.Empty,
};
public record WeightedPoint (int X, int Y)
{
    public double Weight { get; set; }
}
static bool IsInDomain (WeightedPoint point ) => point is (>= 0, >= 0) { 
Weight: >= 0.0 };
if (input is WeightedPoint  (> 0, > 0) { Weight: > 0.0 } p)
{
    // ..
}
var pattern
static bool IsAcceptable (int id, int absLimit ) =>
    SimulateDataFetch(id) is var results A var pattern is useful when you need a temporary variable within a Boolean expression
to hold the result of intermediate calculations. Y ou can also use a var pattern when you
need to perform more checks in when case guards of a switch expression or statement,
as the following example shows:
C#
In the preceding example, pattern var (x, y) is equivalent to a positional pattern  (var
x, var y).
In a var pattern, the type of a declared variable is the compile-time type of the
expression that is matched against the pattern.
For more information, see the Var pattern  section of the feature proposal note.    && results.Min() >= -absLimit 
    && results.Max() <= absLimit;
static int[] SimulateDataFetch (int id)
{
    var rand = new Random();
    return Enumerable
               .Range(start: 0, count: 5)
               .Select(s => rand.Next(minValue: -10, maxValue: 11))
               .ToArray();
}
public record Point(int X, int Y);
static Point Transform (Point point ) => point switch
{
    var (x, y) when x < y => new Point(-x, y),
    var (x, y) when x > y => new Point(x, -y),
    var (x, y) => new Point(x, y),
};
static void TestTransform ()
{
    Console.WriteLine(Transform( new Point(1, 2)));  // output: Point { X =  
-1, Y = 2 }
    Console.WriteLine(Transform( new Point(5, 2)));  // output: Point { X =  
5, Y = -2 }
}
Discard patternYou use a discard pattern _ to match any expression, including null, as the following
example shows:
C#
In the preceding example, a discard pattern is used to handle null and any integer
value that doesn't have the corresponding member of the DayOfW eek enumeration.
That guarantees that a switch expression in the example handles all possible input
values. If you don't use a discard pattern in a switch expression and none of the
expression's patterns matches an input, the runtime throws an exception . The compiler
generates a warning if a switch expression doesn't handle all possible input values.
A discard pattern can't be a pattern in an is expression or a switch statement. In those
cases, to match any expression, use a var pattern  with a discard: var _. A discard
pattern can be a pattern in a switch expression.
For more information, see the Discard pattern  section of the feature proposal note.
You can put parentheses around any pattern. T ypically, you do that to emphasize or
change the precedence in logical patterns , as the following example shows:
C#Console.WriteLine(GetDiscountInPercent(DayOfWeek.Friday));  // output: 5.0
Console.WriteLine(GetDiscountInPercent( null));  // output: 0.0
Console.WriteLine(GetDiscountInPercent((DayOfWeek) 10));  // output: 0.0
static decimal GetDiscountInPercent (DayOfWeek? dayOfWeek ) => dayOfWeek 
switch
{
    DayOfWeek.Monday => 0.5m,
    DayOfWeek.Tuesday => 12.5m,
    DayOfWeek.Wednesday => 7.5m,
    DayOfWeek.Thursday => 12.5m,
    DayOfWeek.Friday => 5.0m,
    DayOfWeek.Saturday => 2.5m,
    DayOfWeek.Sunday => 2.0m,
    _ => 0.0m,
};
Parenthesized pattern
if (input is not (float or double))
{Beginning with C# 11, you can match an array or a list against a sequenc e of patterns, as
the following example shows:
C#
As the preceding example shows, a list pattern is matched when each nested pattern is
matched by the corresponding element of an input sequence. Y ou can use any pattern
within a list pattern. T o match any element, use the discard pattern  or, if you also want
to capture the element, the var pattern , as the following example shows:
C#
The preceding examples match a whole input sequence against a list pattern. T o match
elements only at the start or/and the end of an input sequence, use the slice pattern ..,
as the following example shows:
C#    return;
}
List patterns
int[] numbers = { 1, 2, 3 };
Console.WriteLine(numbers is [1, 2, 3]);  // True
Console.WriteLine(numbers is [1, 2, 4]);  // False
Console.WriteLine(numbers is [1, 2, 3, 4]);  // False
Console.WriteLine(numbers is [0 or 1, <= 2, >= 3]);  // True
List<int> numbers = new() { 1, 2, 3 };
if (numbers is [var first, _, _])
{
    Console.WriteLine( $"The first element of a three-item list is 
{first}.");
}
// Output:
// The first element of a three-item list is 1.
Console.WriteLine( new[] { 1, 2, 3, 4, 5 } is [> 0, > 0, ..]);  // True
Console.WriteLine( new[] { 1, 1 } is [_, _, ..]);  // True
Console.WriteLine( new[] { 0, 1, 2, 3, 4 } is [> 0, > 0, ..]);  // False
Console.WriteLine( new[] { 1 } is [1, 2, ..]);  // False
Console.WriteLine( new[] { 1, 2, 3, 4 } is [.., > 0, > 0]);  // TrueA slice pattern matches zero or more elements. Y ou can use at most one slice pattern in
a list pattern. The slice pattern can only appear in a list pattern.
You can also nest a subpattern within a slice pattern, as the following example shows:
C#
For more information, see the List patterns  feature proposal note.
For more information, see the Patterns and pattern matching  section of the C# language
specification .
For information about features added in C# 8 and later, see the following feature
proposal notes:
Recursive pattern matching
Pattern-matching updates
C# 10 - Extended property patternsConsole.WriteLine( new[] { 2, 4 } is [.., > 0, 2, 4]);  // False
Console.WriteLine( new[] { 2, 4 } is [.., 2, 4]);  // True
Console.WriteLine( new[] { 1, 2, 3, 4 } is [>= 0, .., 2 or 4]);  // True
Console.WriteLine( new[] { 1, 0, 0, 1 } is [1, 0, .., 0, 1]);  // True
Console.WriteLine( new[] { 1, 0, 1 } is [1, 0, .., 0, 1]);  // False
void MatchMessage (string message )
{
    var result = message is ['a' or 'A', .. var s, 'a' or 'A']
        ? $"Message {message}  matches; inner part is {s}."
        : $"Message {message}  doesn't match." ;
    Console.WriteLine(result);
}
MatchMessage( "aBBA");  // output: Message aBBA matches; inner part is BB.
MatchMessage( "apron");  // output: Message apron doesn't match.
void Validate (int[] numbers )
{
    var result = numbers is [< 0, .. { Length: 2 or 4 }, > 0] ? "valid" : 
"not valid" ;
    Console.WriteLine(result);
}
Validate( new[] { -1, 0, 1 });  // output: not valid
Validate( new[] { -1, 0, 0, 1 });  // output: valid
C# language specificationC# 11 - List patterns
C# 11 - P attern match Span<char>  on string literal
C# reference
C# operators and expressions
Pattern matching overview
Tutorial: Use pattern matching to build type-driven and data-driven algorithmsSee also
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
 Provide product feedbackAddition operators - + and +=
Article •04/08/2023
The + and += operators are supported by the built-in integral  and floating-point
numeric types, the string  type, and delegate  types.
For information about the arithmetic + operator, see the Unary plus and minus
operators  and Addition operator +  sections of the Arithmetic operators  article.
When one or both operands are of type string , the + operator concatenates the string
representations of its operands (the string representation of null is an empty string):
C#
String interpolation  provides a more convenient way to format strings:
C#
Beginning with C# 10, you can use string interpolation to initialize a constant string
when all the expressions used for placeholders are also constant strings.
Beginning with C# 11, the + operator performs string concatenation for UTF-8 literal
strings. This operator concatenates two ReadOnlySpan<byte> objects.
For operands of the same delegate  type, the + operator returns a new delegate instance
that, when invoked, invokes the left-hand operand and then invokes the right-handString concatenation
Console.WriteLine( "Forgot"  + "white space" ); 
Console.WriteLine( "Probably the oldest constant: "  + Math.PI);  
Console.WriteLine( null + "Nothing to add." ); 
// Output:  
// Forgotwhite space  
// Probably the oldest constant: 3.14159265358979  
// Nothing to add.  
Console.WriteLine( $"Probably the oldest constant: {Math.PI:F2} "); 
// Output:  
// Probably the oldest constant: 3.14  
Delegate combinationoperand. If any of the operands is null, the + operator returns the value of another
operand (which also might be null). The following example shows how delegates can
be combined with the + operator:
C#
To perform delegate removal, use the - operator .
For more information about delegate types, see Delegates .
An expression using the += operator, such as
C#
is equivalent to
C#
except that x is only evaluated once.
The following example demonstrates the usage of the += operator:
C#Action a = () => Console.Write( "a"); 
Action b = () => Console.Write( "b"); 
Action ab = a + b;  
ab();  // output: ab  
Addition assignment operator +=
x += y 
x = x + y  
int i = 5; 
i += 9; 
Console.WriteLine(i);  
// Output: 14  
string story = "Start. " ; 
story += "End."; 
Console.WriteLine(story);  
// Output: Start. End.  
Action printer = () => Console.Write( "a"); You also use the += operator to specify an event handler method when you subscribe to
an event . For more information, see How to: subscribe to and unsubscribe from events .
A user-defined type can overload  the + operator. When a binary + operator is
overloaded, the += operator is also implicitly overloaded. A user-defined type can't
explicitly overload the += operator.
For more information, see the Unary plus operator  and Addition operator  sections of the
C# language specification .
C# reference
C# operators and expressions
How to concatenate multiple strings
Events
Arithmetic operators
- and -= operatorsprinter();  // output: a  
Console.WriteLine();  
printer += () => Console.Write( "b"); 
printer();  // output: ab  
Operator overloadability
C# language specification
See also- and -= operators - subtraction (minus)
Article •04/08/2023
The - and -= operators are supported by the built-in integral  and floating-point
numeric types and delegate  types.
For information about the arithmetic - operator, see the Unary plus and minus
operators  and Subtraction operator -  sections of the Arithmetic operators  article.
For operands of the same delegate  type, the - operator returns a delegate instance that
is calculated as follows:
If both operands are non-null and the invocation list of the right-hand operand is a
proper contiguous sublist of the invocation list of the left-hand operand, the result
of the operation is a new invocation list that is obtained by removing the right-
hand operand's entries from the invocation list of the left-hand operand. If the
right-hand operand's list matches multiple contiguous sublists in the left-hand
operand's list, only the right-most matching sublist is removed. If removal results
in an empty list, the result is null.
C#
If the invocation list of the right-hand operand isn't a proper contiguous sublist of
the invocation list of the left-hand operand, the result of the operation is the left-
hand operand. For example, removing a delegate that isn't part of the multicast
delegate does nothing and results in the unchanged multicast delegate.Delegate removal
Action a = () => Console.Write( "a"); 
Action b = () => Console.Write( "b"); 
var abbaab = a + b + b + a + a + b;  
abbaab();  // output: abbaab  
Console.WriteLine();  
var ab = a + b;  
var abba = abbaab - ab;  
abba();  // output: abba  
Console.WriteLine();  
var nihil = abbaab - abbaab;  
Console.WriteLine(nihil is null);  // output: True  C#
The preceding example also demonstrates that during delegate removal delegate
instances are compared. For example, delegates that are produced from evaluation
of identical lambda expressions  aren't equal. For more information about delegate
equality, see the Delegate equality operators  section of the C# language
specification .
If the left-hand operand is null, the result of the operation is null. If the right-
hand operand is null, the result of the operation is the left-hand operand.
C#
To combine delegates, use the + operator .
For more information about delegate types, see Delegates .Action a = () => Console.Write( "a"); 
Action b = () => Console.Write( "b"); 
var abbaab = a + b + b + a + a + b;  
var aba = a + b + a;  
var first = abbaab - aba;  
first();  // output: abbaab  
Console.WriteLine();  
Console.WriteLine( object.ReferenceEquals(abbaab, first));  // output:  
True 
Action a2 = () => Console.Write( "a"); 
var changed = aba - a;  
changed();  // output: ab  
Console.WriteLine();  
var unchanged = aba - a2;  
unchanged();  // output: aba  
Console.WriteLine();  
Console.WriteLine( object.ReferenceEquals(aba, unchanged));  // output:  
True 
Action a = () => Console.Write( "a"); 
var nothing = null - a;
Console.WriteLine(nothing is null);  // output: True  
var first = a - null; 
a();  // output: a  
Console.WriteLine();  
Console.WriteLine( object.ReferenceEquals(first, a));  // output: True  An expression using the -= operator, such as
C#
is equivalent to
C#
except that x is only evaluated once.
The following example demonstrates the usage of the -= operator:
C#
You also use the -= operator to specify an event handler method to remove when you
unsubscribe from an event . For more information, see How to subscribe to and
unsubscribe from events .
A user-defined type can overload  the - operator. When a binary - operator is
overloaded, the -= operator is also implicitly overloaded. A user-defined type can't
explicitly overload the -= operator.Subtraction assignment operator -=
x -= y 
x = x - y  
int i = 5; 
i -= 9; 
Console.WriteLine(i);  
// Output: -4  
Action a = () => Console.Write( "a"); 
Action b = () => Console.Write( "b"); 
var printer = a + b + a;  
printer();  // output: aba  
Console.WriteLine();  
printer -= a;  
printer();  // output: ab  
Operator overloadabilityFor more information, see the Unary minus operator  and Subtraction operator  sections
of the C# language specification .
C# reference
C# operators and expressions
Events
Arithmetic operators
+ and += operatorsC# language specification
See also?: operator - the ternary conditional
operator
Article •07/25/2023
The conditional operator ?:, also known as the ternary conditional operator, evaluates a
Boolean expression and returns the result of one of the two expressions, depending on
whether the Boolean expression evaluates to true or false, as the following example
shows:
C#
As the preceding example shows, the syntax for the conditional operator is as follows:
C#
The condition expression must evaluate to true or false. If condition evaluates to
true, the consequent expression is evaluated, and its result becomes the result of the
operation. If condition evaluates to false, the alternative expression is evaluated, and
its result becomes the result of the operation. Only consequent or alternative is
evaluated. Conditional expressions are target-typed. That is, if a target type of a
conditional expression is known, the types of consequent and alternative must be
implicitly convertible to the target type, as the following example shows:
C#string GetWeatherDisplay (double tempInCelsius ) => tempInCelsius < 20.0 ? 
"Cold." : "Perfect!" ;
Console.WriteLine(GetWeatherDisplay( 15));  // output: Cold.
Console.WriteLine(GetWeatherDisplay( 27));  // output: Perfect!
condition ? consequent : alternative
var rand = new Random();
var condition = rand.NextDouble() > 0.5;
int? x = condition ? 12 : null;
IEnumerable< int> xs = x is null ? new List<int>() { 0, 1 } : new int[] { 2, 
3 };If a target type of a conditional expression is unknown (for example, when you use the
var keyword) or the type of consequent and alternative must be the same or there
must be an implicit conversion from one type to the other:
C#
The conditional operator is right-associative, that is, an expression of the form
C#
is evaluated as
C#
A conditional ref expression conditionally returns a variable reference, as the following
example shows:
C#var rand = new Random();
var condition = rand.NextDouble() > 0.5;
var x = condition ? 12 : (int?)null;
a ? b : c ? d : e
a ? b : (c ? d : e)
 Tip
You can use the following mnemonic device to remember how the conditional
operator is evaluated:
text
is this condition true ? yes : no
Conditional ref expression
var smallArray = new int[] { 1, 2, 3, 4, 5 };
var largeArray = new int[] { 10, 20, 30, 40, 50 };
int index = 7;You can ref assign  the result of a conditional ref expression, use it as a reference return
or pass it as a ref, out, in, or ref readonly method parameter . You can also assign to
the result of a conditional ref expression, as the preceding example shows.
The syntax for a conditional ref expression is as follows:
C#
Like the conditional operator, a conditional ref expression evaluates only one of the two
expressions: either consequent or alternative.
In a conditional ref expression, the type of consequent and alternative must be the
same. Conditional ref expressions aren't target-typed.
Use of the conditional operator instead of an if statement  might result in more concise
code in cases when you need conditionally to compute a value. The following example
demonstrates two ways to classify an integer as negative or nonnegative:
C#ref int refValue = ref ((index < 5) ? ref smallArray[index] : ref 
largeArray[index - 5]);
refValue = 0;
index = 2;
((index < 5) ? ref smallArray[index] : ref largeArray[index - 5]) = 100;
Console.WriteLine( string.Join(" ", smallArray));
Console.WriteLine( string.Join(" ", largeArray));
// Output:
// 1 2 100 4 5
// 10 20 0 40 50
condition ? ref consequent : ref alternative
Conditional operator and an if statement
int input = new Random().Next( -5, 5);
string classify;
if (input >= 0)
{
    classify = "nonnegative" ;
}
else
{
    classify = "negative" ;A user-defined type can't overload the conditional operator.
For more information, see the Conditional operator  section of the C# language
specification .
Specifications for newer features are:
Target-typed conditional expression
Simplify conditional expression (style rule IDE0075)
C# reference
C# operators and expressions
if statement
?. and ?[] operators
?? and ??= operators
ref keyword}
classify = (input >= 0) ? "nonnegative"  : "negative" ;
Operator overloadability
C# language specification
See also
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
 Provide product feedback! (null-forgiving) operator (C# reference)
Article •12/02/2022
The unary postfix ! operator is the null-forgiving, or null-suppression, operator. In an
enabled nullable annotation context , you use the null-forgiving operator to suppress all
nullable warnings for the preceding expression. The unary prefix ! operator is the
logical negation operator . The null-forgiving operator has no effect at run time. It only
affects the compiler's static flow analysis by changing the null state of the expression. At
run time, expression x! evaluates to the result of the underlying expression x.
For more information about the nullable reference types feature, see Nullable reference
types .
One of the use cases of the null-forgiving operator is in testing the argument validation
logic. For example, consider the following class:
C#
Using the MSTest test framework , you can create the following test for the validation
logic in the constructor:
C#
Without the null-forgiving operator, the compiler generates the following warning for
the preceding code: Warning CS8625: Cannot convert null literal to non-nullableExamples
#nullable enable  
public class Person 
{ 
    public Person(string name) => Name = name ?? throw new 
ArgumentNullException( nameof(name));  
    public string Name { get; } 
} 
[TestMethod, ExpectedException(typeof(ArgumentNullException)) ] 
public void NullNameShouldThrowTest () 
{ 
    var person = new Person( null!); 
} reference type. By using the null-forgiving operator, you inform the compiler that
passing null is expected and shouldn't be warned about.
You can also use the null-forgiving operator when you definitely know that an
expression can't be null but the compiler doesn't manage to recognize that. In the
following example, if the IsValid method returns true, its argument isn't null and you
can safely dereference it:
C#
Without the null-forgiving operator, the compiler generates the following warning for
the p.Name code: Warning CS8602: Dereference of a possibly null reference.
If you can modify the IsValid method, you can use the NotNullWhen  attribute to
inform the compiler that an argument of the IsValid method can't be null when the
method returns true:
C#
In the preceding example, you don't need to use the null-forgiving operator because the
compiler has enough information to find out that p can't be null inside the if
statement. For more information about the attributes that allow you to providepublic static void Main() 
{ 
    Person? p = Find( "John"); 
    if (IsValid(p))  
    { 
        Console.WriteLine( $"Found {p!.Name} "); 
    } 
} 
public static bool IsValid(Person? person ) 
    => person is not null && person.Name is not null; 
public static void Main() 
{ 
    Person? p = Find( "John"); 
    if (IsValid(p))  
    { 
        Console.WriteLine( $"Found {p.Name} "); 
    } 
} 
public static bool IsValid([NotNullWhen( true)] Person? person)  
    => person is not null && person.Name is not null; additional information about the null state of a variable, see Upgrade APIs with
attributes to define null expectations .
For more information, see The null-forgiving operator  section of the draft of the nullable
reference types specification .
Remove unnecessary suppression operator (style rule IDE0080)
C# reference
C# operators and expressions
Tutorial: Design with nullable reference typesC# language specification
See also?? and ??= operators - the null-
coalescing operators
Article •07/27/2023
The null-coalescing operator ?? returns the value of its left-hand operand if it isn't
null; otherwise, it evaluates the right-hand operand and returns its result. The ??
operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to
non-null. The null-coalescing assignment operator ??= assigns the value of its right-
hand operand to its left-hand operand only if the left-hand operand evaluates to null.
The ??= operator doesn't evaluate its right-hand operand if the left-hand operand
evaluates to non-null.
C#
The left-hand operand of the ??= operator must be a variable, a property , or an indexer
element.
The type of the left-hand operand of the ?? and ??= operators can't be a non-nullable
value type. In particular, you can use the null-coalescing operators with unconstrained
type parameters:
C#List<int> numbers = null;
int? a = null;
Console.WriteLine((numbers is null)); // expected: true
// if numbers is null, initialize it. Then, add 5 to numbers
(numbers ??= new List<int>()).Add( 5);
Console.WriteLine( string.Join(" ", numbers));  // output: 5
Console.WriteLine((numbers is null)); // expected: false        
Console.WriteLine((a is null)); // expected: true
Console.WriteLine((a ?? 3)); // expected: 3 since a is still null 
// if a is null then assign 0 to a and add a to the list
numbers.Add(a ??= 0);
Console.WriteLine((a is null)); // expected: false        
Console.WriteLine( string.Join(" ", numbers));  // output: 5 0
Console.WriteLine(a);  // output: 0         
private static void Display<T>(T a, T backup)
{The null-coalescing operators are right-associative. That is, expressions of the form
C#
are evaluated as
C#
The ?? and ??= operators can be useful in the following scenarios:
In expressions with the null-conditional operators ?. and ?[], you can use the ??
operator to provide an alternative expression to evaluate in case the result of the
expression with null-conditional operations is null:
C#
When you work with nullable value types  and need to provide a value of an
underlying value type, use the ?? operator to specify the value to provide in case a
nullable type value is null:
C#    Console.WriteLine(a ?? backup);
}
a ?? b ?? c
d ??= e ??= f
a ?? (b ?? c)
d ??= (e ??= f)
Examples
double SumNumbers (List<double[]> setsOfNumbers, int indexOfSetToSum )
{
    return setsOfNumbers?[indexOfSetToSum]?.Sum() ?? double.NaN;
}
var sum = SumNumbers( null, 0);
Console.WriteLine(sum);  // output: NaN
int? a = null;
int b = a ?? -1;
Console.WriteLine(b);  // output: -1Use the Nullable<T>.GetV alueOrDefault()  method if the value to be used when a
nullable type value is null should be the default value of the underlying value
type.
You can use a throw  expression  as the right-hand operand of the ?? operator to
make the argument-checking code more concise:
C#
The preceding example also demonstrates how to use expression-bodied
members  to define a property.
You can use the ??= operator to replace the code of the form
C#
with the following code:
C#
The operators ?? and ??= can't be overloaded.
For more information about the ?? operator, see The null coalescing operator  section of
the C# language specification .public string Name
{
    get => name;
    set => name = value ?? throw new 
ArgumentNullException( nameof(value), "Name cannot be null" );
}
if (variable is null)
{
    variable = expression;
}
variable ??= expression;
Operator overloadability
C# language specificationFor more information about the ??= operator, see the feature proposal note .
Null check can be simplified (IDE0029, IDE0030, and IDE0270)
C# reference
C# operators and expressions
?. and ?[] operators
?: operatorSee alsoLambda expression (=>) operator
defines a lambda expression
Article •04/08/2023
The => token is supported in two forms: as the lambda operator  and as a separator of a
member name and the member implementation in an expression body definition .
In lambda expressions , the lambda operator => separates the input parameters on the
left side from the lambda body on the right side.
The following example uses the LINQ  feature with method syntax to demonstrate the
usage of lambda expressions:
C#
Input parameters of a lambda expression are strongly typed at compile time. When the
compiler can infer the types of input parameters, like in the preceding example, you may
omit type declarations. If you need to specify the type of input parameters, you must do
that for each parameter, as the following example shows:
C#
The following example shows how to define a lambda expression without input
parameters:Lambda operator
string[] words = { "bot", "apple", "apricot"  };
int minimalLength = words
  .Where(w => w.StartsWith( "a"))
  .Min(w => w.Length);
Console.WriteLine(minimalLength);   // output: 5
int[] numbers = { 4, 7, 10 };
int product = numbers.Aggregate( 1, (interim, next) => interim * next);
Console.WriteLine(product);   // output: 280
int[] numbers = { 4, 7, 10 };
int product = numbers.Aggregate( 1, (int interim, int next) => interim *  
next);
Console.WriteLine(product);   // output: 280C#
For more information, see Lambda expressions .
An expression body definition has the following general syntax:
C#
where expression is a valid expression. The return type of expression must be implicitly
convertible to the member's return type. If the member:
Has a void return type or
Is a:
Constructor
Finalizer
Property or indexer set accessor
expression must be a statement expr ession . Because the expression's result is discarded,
the return type of that expression can be any type.
The following example shows an expression body definition for a Person.ToString
method:
C#
It's a shorthand version of the following method definition:
C#Func<string> greet = () => "Hello, World!" ;
Console.WriteLine(greet());
Expression body definitio n
member => expression;
public override  string ToString () => $"{fname} {lname}".Trim();
public override  string ToString ()
{
   return $"{fname} {lname}".Trim();
}You can create expression body definitions for methods, operators, read-only properties,
constructors, finalizers, and property and indexer accessors. For more information, see
Expression-bodied members .
The => operator can't be overloaded.
For more information about the lambda operator, see the Anonymous function
expressions  section of the C# language specification .
C# reference
C# operators and expressionsOperator overloadability
C# language specification
See also:: operator - the namespace alias
operator
Article •04/12/2023
Use the namespace alias qualifier :: to access a member of an aliased namespace. Y ou
can use the :: qualifier only between two identifiers. The left-hand identifier can be one
of a namespace alias, an extern alias, or the global alias. For example:
A namespace alias created with a using alias directive :
C#
An extern alias .
The global alias, which is the global namespace alias. The global namespace is the
namespace that contains namespaces and types that aren't declared inside a
named namespace. When used with the :: qualifier, the global alias always
references the global namespace, even if there's the user-defined global
namespace alias.
The following example uses the global alias to access the .NET System  namespace,
which is a member of the global namespace. Without the global alias, the user-
defined System namespace, which is a member of the MyCompany.MyProduct
namespace, would be accessed:
C#using forwinforms = System.Drawing;  
using forwpf = System.Windows;  
public class Converters
{ 
    public static forwpf:: Point Convert(forwinforms::Point point ) => 
new forwpf::Point(point.X, point.Y);  
} 
namespace  MyCompany.MyProduct.System  
{ 
    class Program 
    { 
        static void Main() => global::System.Console.WriteLine( "Using 
global alias" ); 
    } You can also use the . token  to access a member of an aliased namespace. However, the
. token is also used to access a type member. The :: qualifier ensures that its left-hand
identifier always references a namespace alias, even if there exists a type or namespace
with the same name.
For more information, see the Namespace alias qualifiers  section of the C# language
specification .
C# reference
C# operators and expressions    class Console 
    { 
        string Suggestion => "Consider renaming this class" ; 
    } 
} 
７ Note
The global keyword is the global namespace alias only when it's the left-hand
identifier of the :: qualifier.
C# language specification
See alsoawait operator - asynchronously await
for a task to complete
Article •03/22/2023
The await operator suspends evaluation of the enclosing async  method until the
asynchronous operation represented by its operand completes. When the asynchronous
operation completes, the await operator returns the result of the operation, if any.
When the await operator is applied to the operand that represents an already
completed operation, it returns the result of the operation immediately without
suspension of the enclosing method. The await operator doesn't block the thread that
evaluates the async method. When the await operator suspends the enclosing async
method, the control returns to the caller of the method.
In the following example, the HttpClient.GetByteArrayAsync  method returns the
Task<byte[]> instance, which represents an asynchronous operation that produces a
byte array when it completes. Until the operation completes, the await operator
suspends the DownloadDocsMainPageAsync method. When DownloadDocsMainPageAsync
gets suspended, control is returned to the Main method, which is the caller of
DownloadDocsMainPageAsync. The Main method executes until it needs the result of the
asynchronous operation performed by the DownloadDocsMainPageAsync method. When
GetByteArrayAsync  gets all the bytes, the rest of the DownloadDocsMainPageAsync method
is evaluated. After that, the rest of the Main method is evaluated.
C#
using System;  
using System.Net.Http;  
using System.Threading.Tasks;  
public class AwaitOperator  
{ 
    public static async Task Main() 
    { 
        Task< int> downloading = DownloadDocsMainPageAsync();  
        Console.WriteLine( $"{nameof(Main)}: Launched downloading." ); 
        int bytesLoaded = await downloading;  
        Console.WriteLine( $"{nameof(Main)}: Downloaded {bytesLoaded}  
bytes."); 
    } 
    private static async Task<int> DownloadDocsMainPageAsync () 
    { 
        Console.WriteLine( $"{nameof(DownloadDocsMainPageAsync)} : About to  The preceding example uses the async Main  method . For more information, see the
await operator in the Main method  section.
You can use the await operator only in a method, lambda expression , or anonymous
method  that is modified by the async  keyword. Within an async method, you can't use
the await operator in the body of a synchronous function, inside the block of a lock
statement , and in an unsafe  context.
The operand of the await operator is usually of one of the following .NET types: Task,
Task<TR esult> , ValueT ask, or ValueT ask<TR esult> . However, any awaitable expression
can be the operand of the await operator. For more information, see the Awaitable
expressions  section of the C# language specification .
The type of expression await t is TResult if the type of expression t is Task<TR esult>
or ValueT ask<TR esult> . If the type of t is Task or ValueT ask, the type of await t is void.
In both cases, if t throws an exception, await t rethrows the exception.
You use the await foreach statement to consume an asynchronous stream of data. For
more information, see the foreach  statement  section of the Iteration statements  article.start downloading." ); 
        var client = new HttpClient();  
        byte[] content = await 
client.GetByteArrayAsync( "https://learn.microsoft.com/en-us/" ); 
        Console.WriteLine( $"{nameof(DownloadDocsMainPageAsync)} : Finished  
downloading." ); 
        return content.Length;  
    } 
} 
// Output similar to:  
// DownloadDocsMainPageAsync: About to start downloading.  
// Main: Launched downloading.  
// DownloadDocsMainPageAsync: Finished downloading.  
// Main: Downloaded 27700 bytes.  
７ Note
For an introduction to asynchronous programming, see Asynchr onous
programming with async and await . Asynchronous programming with async and
await follows the task-based asynchr onous p attern.
Asynchronous streams and disposablesYou use the await using statement to work with an asynchronously disposable object,
that is, an object of a type that implements an IAsyncDisposable  interface. For more
information, see the Using async disposable  section of the Implement a DisposeAsync
method  article.
The Main  method , which is the application entry point, can return Task or Task<int>,
enabling it to be async so you can use the await operator in its body. In earlier C#
versions, to ensure that the Main method waits for the completion of an asynchronous
operation, you can retrieve the value of the Task<TR esult>.R esult  property of the
Task<TR esult>  instance that is returned by the corresponding async method. For
asynchronous operations that don't produce a value, you can call the Task.W ait method.
For information about how to select the language version, see C# language versioning .
For more information, see the Await expressions  section of the C# language
specification .
C# reference
C# operators and expressions
async
Task asynchronous programming model
Asynchronous programming
Walkthrough: accessing the W eb by using async and await
Tutorial: Generate and consume async streams
.NET blog: How async/await really works in C#await operator in the Main method
C# language specification
See also
default value exp ressions - produce the
default value
Article •04/08/2023
A default value expression produces the default value  of a type. There are two kinds of
default value expressions: the default operator  call and a default literal .
You also use the default keyword as the default case label within a switch  statement .
The argument to the default operator must be the name of a type or a type parameter,
as the following example shows:
C#
You can use the default literal to produce the default value of a type when the compiler
can infer the expression type. The default literal expression produces the same value as
the default(T) expression where T is the inferred type. Y ou can use the default literal
in any of the following cases:
In the assignment or initialization of a variable.
In the declaration of the default value for an optional method parameter .default operator
Console.WriteLine( default(int));  // output: 0  
Console.WriteLine( default(object) is null);  // output: True  
void DisplayDefaultOf<T>()  
{ 
    var val = default(T); 
    Console.WriteLine( $"Default value of {typeof(T)} is {(val == null ? 
"null" : val.ToString())} ."); 
} 
DisplayDefaultOf< int?>(); 
DisplayDefaultOf<System.Numerics.Complex>();  
DisplayDefaultOf<System.Collections.Generic.List< int>>(); 
// Output:  
// Default value of System.Nullable`1[System.Int32] is null.  
// Default value of System.Numerics.Complex is (0, 0).  
// Default value of System.Collections.Generic.List`1[System.Int32] is null.  
default literalIn a method call to provide an argument value.
In a return  statement  or as an expression in an expression-bodied member .
The following example shows the usage of the default literal:
C#
For more information, see the Default value expressions  section of the C# language
specification .T[] InitializeArray<T>( int length, T initialValue = default) 
{ 
    if (length < 0) 
    { 
        throw new ArgumentOutOfRangeException( nameof(length), "Array length  
must be nonnegative." ); 
    } 
    var array = new T[length];  
    for (var i = 0; i < length; i++)  
    { 
        array[i] = initialValue;  
    } 
    return array; 
} 
void Display<T>(T[] values) => Console.WriteLine( $"[ {string.Join(", ", 
values)}  ]"); 
Display(InitializeArray< int>(3));  // output: [ 0, 0, 0 ]  
Display(InitializeArray< bool>(4, default));  // output: [ False, False,  
False, False ]  
System.Numerics.Complex fillValue = default; 
Display(InitializeArray( 3, fillValue));  // output: [ (0, 0), (0, 0), (0, 0)  
] 
 Tip
Use .NET style rule IDE0034  to specify a preference on the use of the default literal
in your codebase.
C# language specification
See alsoC# reference
C# operators and expressions
Default values of C# types
Generics in .NETdelegate operator
Article •11/14/2023
The delegate operator creates an anonymous method that can be converted to a
delegate type. An anonymous method can be converted to types such as System.Action
and System.Func<TR esult>  types used as arguments to many methods.
C#
When you use the delegate operator, you might omit the parameter list. If you do that,
the created anonymous method can be converted to a delegate type with any list of
parameters, as the following example shows:
C#Func<int, int, int> sum = delegate  (int a, int b) { return a + b; };
Console.WriteLine(sum( 3, 4));  // output: 7
７ Note
Lambda expressions provide a more concise and expressive way to create an
anonymous function. Use the => operat or to construct a lambda expression:
C#
For more information about features of lambda expressions, for example, capturing
outer variables, see Lambda expr essions .Func<int, int, int> sum = (a, b) => a + b;
Console.WriteLine(sum( 3, 4));  // output: 7
Action greet = delegate  { Console.WriteLine( "Hello!" ); };
greet();
Action<int, double> introduce = delegate  { Console.WriteLine( "This is  
world!"); };
introduce( 42, 2.7);
// Output:
// Hello!
// This is world!That's the only functionality of anonymous methods that isn't supported by lambda
expressions. In all other cases, a lambda expression is a preferred way to write inline
code. Y ou can use discards  to specify two or more input parameters of an anonymous
method that aren't used by the method:
C#
For backwards compatibility, if only a single parameter is named _, _ is treated as the
name of that parameter within an anonymous method.
You can use the static modifier at the declaration of an anonymous method:
C#
A static anonymous method can't capture local variables or instance state from
enclosing scopes.
You also use the delegate keyword to declare a delegate type .
Beginning with C# 11, the compiler may cache the delegate object created from a
method group. Consider the following method:
C#
When you assign the method group to a delegate, the compiler will cache the delegate:
C#
Before C# 11, you'd need to use a lambda expression to reuse a single delegate object:
C#Func<int, int, int> constant = delegate  (int _, int _) { return 42; };
Console.WriteLine(constant( 3, 4));  // output: 42
Func<int, int, int> sum = static delegate  (int a, int b) { return a + b; };
Console.WriteLine(sum( 10, 4));  // output: 14
static void StaticFunction () { }
Action a = StaticFunction;
Action a = () => StaticFunction();For more information, see the Anonymous function expressions  section of the C#
language specification .
C# reference
C# operators and expressions
=> operatorC# language specification
See also
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
 Provide product feedbackis operator (C# reference)
Article •11/14/2023
The is operator checks if the result of an expression is compatible with a given type.
For information about the type-testing is operator, see the is operator  section of the
Type-testing and cast operators  article. Y ou can also use the is operator to match an
expression against a pattern, as the following example shows:
C#
In the preceding example, the is operator matches an expression against a property
pattern  with nested constant  and relational  patterns.
The is operator can be useful in the following scenarios:
To check the run-time type of an expression, as the following example shows:
C#
The preceding example shows the use of a declaration pattern .
To check for null, as the following example shows:
C#
When you match an expression against null, the compiler guarantees that no
user-overloaded == or != operator is invoked.static bool IsFirstFridayOfOctober (DateTime date ) =>
    date is { Month: 10, Day: <= 7, DayOfWeek: DayOfWeek.Friday };
int i = 34;
object iBoxed = i;
int? jNullable = 42;
if (iBoxed is int a && jNullable is int b)
{
    Console.WriteLine(a + b);  // output 76
}
if (input is null)
{
    return;
}You can use a negation pattern  to do a non-null check, as the following example
shows:
C#
Beginning with C# 11, you can use list patterns  to match elements of a list or array.
The following code checks arrays for integer values in expected positions:
C#
For more information, see The is operator  section of the C# language specification  and
Pattern matching .
C# reference
C# operators and expressionsif (result is not null)
{
    Console.WriteLine(result.ToString());
}
int[] empty = { };
int[] one = { 1 };
int[] odd = { 1, 3, 5 };
int[] even = { 2, 4, 6 };
int[] fib = { 1, 1, 2, 3, 5 };
Console.WriteLine(odd is [1, _, 2, ..]);   // false
Console.WriteLine(fib is [1, _, 2, ..]);   // true
Console.WriteLine(fib is [_, 1, 2, 3, ..]);     // true
Console.WriteLine(fib is [.., 1, 2, 3, _ ]);     // true
Console.WriteLine(even is [2, _, 6]);     // true
Console.WriteLine(even is [2, .., 6]);    // true
Console.WriteLine(odd is [.., 3, 5]); // true
Console.WriteLine(even is [.., 3, 5]); // false
Console.WriteLine(fib is [.., 3, 5]); // true
７ Note
For the complete list of patterns supported by the is operator, see Patterns.
C# language specification
See alsoPatterns
Tutorial: Use pattern matching to build type-driven and data-driven algorithms
Type-testing and cast operators
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
 Provide product feedbacknameof expression (C# reference)
Article •03/15/2023
A nameof expression produces the name of a variable, type, or member as the string
constant. A nameof expression is evaluated at compile time and has no effect at run
time. When the operand is a type or a namespace, the produced name isn't fully
qualified . The following example shows the use of a nameof expression:
C#
You can use a nameof expression to make the argument-checking code more
maintainable:
C#
Beginning with C# 11, you can use a nameof expression with a method parameter inside
an attribute  on a method or its parameter. The following code shows how to do that for
an attribute on a method, a local function, and the parameter of a lambda expression:
C#Console.WriteLine( nameof(System.Collections.Generic));  // output: Generic
Console.WriteLine( nameof(List<int>));  // output: List
Console.WriteLine( nameof(List<int>.Count));  // output: Count
Console.WriteLine( nameof(List<int>.Add));  // output: Add
var numbers = new List<int> { 1, 2, 3 };
Console.WriteLine( nameof(numbers));  // output: numbers
Console.WriteLine( nameof(numbers.Count));  // output: Count
Console.WriteLine( nameof(numbers.Add));  // output: Add
public string Name
{
    get => name;
    set => name = value ?? throw new ArgumentNullException( nameof(value), $"
{nameof(Name)} cannot be null" );
}
[ParameterString(nameof(msg)) ]
public static void Method(string msg)
{
    [ParameterString(nameof(T)) ]
    void LocalFunction<T>(T param) { }
    var lambdaExpression = ([ParameterString( nameof(aNumber))] int aNumber)  A nameof expression with a parameter is useful when you use the nullable analysis
attributes  or the CallerArgumentExpression attribute .
When the operand is a verbatim identifier , the @ character isn't the part of a name, as
the following example shows:
C#
For more information, see the Nameof expressions  section of the C# language
specification , and the C# 11 - Extended nameof  scope  feature specification.
C# reference
C# operators and expressions
Convert typeof  to nameof  (style rule IDE0082)=> aNumber.ToString();
}
var @new = 5;
Console.WriteLine( nameof(@new));  // output: new
C# language specification
See also
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
 Provide product feedbacknew operator - The new operator
creates a new instance of a type
Article •11/14/2023
The new operator creates a new instance of a type. Y ou can also use the new keyword as
a member declaration modifier  or a generic type constraint .
To create a new instance of a type, you typically invoke one of the constructors  of that
type using the new operator:
C#
You can use an object or collection initializer  with the new operator to instantiate and
initialize an object in one statement, as the following example shows:
C#Constructor invocation
var dict = new Dictionary< string, int>();
dict["first"] = 10;
dict["second" ] = 20;
dict["third"] = 30;
Console.WriteLine( string.Join("; ", dict.Select(entry => $"{entry.Key} : 
{entry.Value} ")));
// Output:
// first: 10; second: 20; third: 30
var dict = new Dictionary< string, int>
{
    ["first"] = 10,
    ["second" ] = 20,
    ["third"] = 30
};
Console.WriteLine( string.Join("; ", dict.Select(entry => $"{entry.Key} : 
{entry.Value} ")));
// Output:
// first: 10; second: 20; third: 30
Target-typed newConstructor invocation expressions are target-typed. That is, if a target type of an
expression is known, you can omit a type name, as the following example shows:
C#
As the preceding example shows, you always use parentheses in a target-typed new
expression.
If a target type of a new expression is unknown (for example, when you use the var
keyword), you must specify a type name.
You also use the new operator to create an array instance, as the following example
shows:
C#
Use array initialization syntax to create an array instance and populate it with elements
in one statement. The following example shows various ways how you can do that:
C#List<int> xs = new();
List<int> ys = new(capacity: 10_000);
List<int> zs = new() { Capacity = 20_000 };
Dictionary< int, List<int>> lookup = new()
{
    [1] = new() { 1, 2, 3 },
    [2] = new() { 5, 8, 3 },
    [5] = new() { 1, 0, 4 }
};
Array creation
var numbers = new int[3];
numbers[ 0] = 10;
numbers[ 1] = 20;
numbers[ 2] = 30;
Console.WriteLine( string.Join(", ", numbers));
// Output:
// 10, 20, 30
var a = new int[3] { 10, 20, 30 };
var b = new int[] { 10, 20, 30 };For more information about arrays, see Arrays .
To create an instance of an anonymous type , use the new operator and object initializer
syntax:
C#
You don't have to destroy earlier created type instances. Instances of both reference and
value types are destroyed automatically. Instances of value types are destroyed as soon
as the context that contains them is destroyed. Instances of reference types are
destroyed by the garbage collector  at some unspecified time after the last reference to
them is removed.
For type instances that contain unmanaged resources, for example, a file handle, it's
recommended to employ deterministic clean-up to ensure that the resources they
contain are released as soon as possible. For more information, see the
System.IDisposable  API reference and the using statement  article.
A user-defined type can't overload the new operator.
For more information, see The new operator  section of the C# language specification .
For more information about a target-typed new expression, see the feature proposal
note.var c = new[] { 10, 20, 30 };
Console.WriteLine(c.GetType());  // output: System.Int32[]
Instantiation of anonymous types
var example = new { Greeting = "Hello", Name = "World" };
Console.WriteLine( $"{example.Greeting} , {example.Name} !");
// Output:
// Hello, World!
Destruction of type instances
Operator overloadability
C# language specificationC# reference
C# operators and expressions
Object and collection initializersSee also
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
 Provide product feedbacksizeof operator - determine the memory
needs for a given type
Article •04/12/2023
The sizeof operator returns the number of bytes occupied by a variable of a given type.
The argument to the sizeof operator must be the name of an unmanaged type  or a
type parameter that is constrained  to be an unmanaged type.
The sizeof operator requires an unsafe  context. However, the expressions presented in
the following table are evaluated in compile time to the corresponding constant values
and don't require an unsafe context:
Expr ession Constant v alue
sizeof(sbyte) 1
sizeof(byte) 1
sizeof(short) 2
sizeof(ushort) 2
sizeof(int) 4
sizeof(uint) 4
sizeof(long) 8
sizeof(ulong) 8
sizeof(char) 2
sizeof(float) 4
sizeof(double) 8
sizeof(decimal) 16
sizeof(bool) 1
You also don't need to use an unsafe context when the operand of the sizeof operator
is the name of an enum  type.
The following example demonstrates the usage of the sizeof operator:
C#The sizeof operator returns a number of bytes that would be allocated by the common
language runtime in managed memory. For struct  types, that value includes any
padding, as the preceding example demonstrates. The result of the sizeof operator
might differ from the result of the Marshal.SizeOf  method, which returns the size of a
type in unmanaged  memory.
For more information, see The sizeof operator  section of the C# language specification .
C# reference
C# operators and expressions
Pointer related operators
Pointer typespublic struct Point 
{ 
    public Point(byte tag, double x, double y) => (Tag, X, Y) = (tag, x, y);  
    public byte Tag { get; } 
    public double X { get; } 
    public double Y { get; } 
} 
public class SizeOfOperator  
{ 
    public static void Main() 
    { 
        Console.WriteLine( sizeof(byte));  // output: 1  
        Console.WriteLine( sizeof(double));  // output: 8
        DisplaySizeOf<Point>();  // output: Size of Point is 24  
        DisplaySizeOf< decimal>();  // output: Size of System.Decimal is 16  
        unsafe 
        {  
            Console.WriteLine( sizeof(Point*));  // output: 8  
        }  
    } 
    static unsafe void DisplaySizeOf<T>() where T : unmanaged  
    { 
        Console.WriteLine( $"Size of {typeof(T)} is {sizeof(T)}"); 
    } 
} 
C# language specification
See alsoMemory and span-related types
Generics in .NETstackalloc exp ression (C# reference)
Article •11/17/2023
A stackalloc expression allocates a block of memory on the stack. A stack allocated
memory block created during the method execution is automatically discarded when
that method returns. Y ou can't explicitly free the memory allocated with stackalloc. A
stack allocated memory block isn't subject to garbage collection  and doesn't have to be
pinned with a fixed  statement .
You can assign the result of a stackalloc expression to a variable of one of the
following types:
System.Span<T>  or System.R eadOnlySpan<T> , as the following example shows:
C#
You don't have to use an unsafe  context when you assign a stack allocated
memory block to a Span<T>  or ReadOnlySpan<T>  variable.
When you work with those types, you can use a stackalloc expression in
conditional  or assignment expressions, as the following example shows:
C#
You can use a stackalloc expression or a collection expression inside other
expressions whenever a Span<T>  or ReadOnlySpan<T>  variable is allowed, as the
following example shows:
C#int length = 3;
Span<int> numbers = stackalloc  int[length];
for (var i = 0; i < length; i++)
{
    numbers[i] = i;
}
int length = 1000;
Span<byte> buffer = length <= 1024 ? stackalloc  byte[length] : new 
byte[length];
Span<int> numbers = stackalloc [] { 1, 2, 3, 4, 5, 6 };
var ind = numbers.IndexOfAny( stackalloc [] { 2, 4, 6, 8 });
Console.WriteLine(ind);  // output: 1A pointer type , as the following example shows:
C#
As the preceding example shows, you must use an unsafe context when you work
with pointer types.
In the case of pointer types, you can use a stackalloc expression only in a local
variable declaration to initialize the variable.
The amount of memory available on the stack is limited. If you allocate too much
memory on the stack, a StackOverflowException  is thrown. T o avoid that, follow the rules
below:
Limit the amount of memory you allocate with stackalloc. For example, if the
intended buffer size is below a certain limit, you allocate the memory on the stack;
otherwise, use an array of the required length, as the following code shows:
C#Span<int> numbers2 = [ 1, 2, 3, 4, 5, 6];
var ind2 = numbers2.IndexOfAny([ 2, 4, 6, 8]);
Console.WriteLine(ind2);  // output: 1
７ Note
We recommend using Span<T>  or ReadOnlySp an<T>  types to work with
stack allocated memory whenever possible.
unsafe
{
    int length = 3;
    int* numbers = stackalloc  int[length];
    for (var i = 0; i < length; i++)
    {
        numbers[i] = i;
    }
}
const int MaxStackLimit = 1024;
Span<byte> buffer = inputLength <= MaxStackLimit ? stackalloc  
byte[MaxStackLimit] : new byte[inputLength];Avoid using stackalloc inside loops. Allocate the memory block outside a loop
and reuse it inside the loop.
The content of the newly allocated memory is undefined. Y ou should initialize it before
the use. For example, you can use the Span<T>.Clear  method that sets all the items to
the default value of type T.
You can use array initializer syntax to define the content of the newly allocated memory.
The following example demonstrates various ways to do that:
C#
In expression stackalloc T[E], T must be an unmanaged type  and E must evaluate to
a non-negative int value. When you use the collection expression  syntax to initialize the
span, the compiler may use stack allocated storage for a span if it won't violate ref
safety.
The use of stackalloc automatically enables buffer overrun detection features in the
common language runtime (CLR). If a buffer overrun is detected, the process is
terminated as quickly as possible to minimize the chance that malicious code is
executed.
For more information, see the Stack allocation  section of the C# language specification
and the Permit stackalloc  in nested contexts  feature proposal note.７ Note
Because the amount of memory available on the stack depends on the
environment in which the code is executed, be conservative when you define
the actual limit value.
Span<int> first = stackalloc  int[3] { 1, 2, 3 };
Span<int> second = stackalloc  int[] { 1, 2, 3 };
ReadOnlySpan< int> third = stackalloc [] { 1, 2, 3 };
// Using collection expressions:
Span<int> fourth= [ 1, 2, 3];
ReadOnlySpan< int> fifth= [ 1, 2, 3];
Security
C# language specificationC# reference
C# operators and expressions
Pointer related operators
Pointer types
Memory and span-related types
Dos and Don'ts of stackallocSee also
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
 Provide product feedbackswitch expression - pattern matching
expressions using the switch keyword
Article •12/02/2022
You use the switch expression to evaluate a single expression from a list of candidate
expressions based on a pattern match with an input expression. For information about
the switch statement that supports switch-like semantics in a statement context, see
the switch  statement  section of the Selection statements  article.
The following example demonstrates a switch expression, which converts values of an
enum  representing visual directions in an online map to the corresponding cardinal
directions:
C#
public static class SwitchExample  
{ 
    public enum Direction  
    { 
        Up,  
        Down,  
        Right,  
        Left  
    } 
    public enum Orientation  
    { 
        North,  
        South,  
        East,  
        West  
    } 
    public static Orientation ToOrientation (Direction direction ) => 
direction switch 
    { 
        Direction.Up    => Orientation.North,  
        Direction.Right => Orientation.East,  
        Direction.Down  => Orientation.South,  
        Direction.Left  => Orientation.West,  
        _ => throw new ArgumentOutOfRangeException( nameof(direction), $"Not 
expected direction value: {direction} "), 
    }; 
    public static void Main() 
    { 
        var direction = Direction.Right;  
        Console.WriteLine( $"Map view direction is {direction} "); The preceding example shows the basic elements of a switch expression:
An expression followed by the switch keyword. In the preceding example, it's the
direction method parameter.
The switch expr ession ar ms, separated by commas. Each switch expression arm
contains a pattern, an optional case guar d, the => token, and an expression .
At the preceding example, a switch expression uses the following patterns:
A constant pattern : to handle the defined values of the Direction enumeration.
A discard pattern : to handle any integer value that doesn't have the corresponding
member of the Direction enumeration (for example, (Direction)10). That makes
the switch expression exhaustive .
The result of a switch expression is the value of the expression of the first switch
expression arm whose pattern matches the input expression and whose case guard, if
present, evaluates to true. The switch expression arms are evaluated in text order.
The compiler generates an error when a lower switch expression arm can't be chosen
because a higher switch expression arm matches all its values.
A pattern may be not expressive enough to specify the condition for the evaluation of
an arm's expression. In such a case, you can use a case guar d. A case guar d is another
condition that must be satisfied together with a matched pattern. A case guard must be
a Boolean expression. Y ou specify a case guard after the when keyword that follows a
pattern, as the following example shows:        Console.WriteLine( $"Cardinal orientation is  
{ToOrientation(direction)} "); 
        // Output:  
        // Map view direction is Right  
        // Cardinal orientation is East  
    } 
} 
） Impor tant
For information about the patterns supported by the switch expression and more
examples, see Patterns.
Case guardsC#
The preceding example uses property patterns  with nested var patterns .
If none of a switch expression's patterns matches an input value, the runtime throws an
exception. In .NET Core 3.0 and later versions, the exception is a
System.Runtime.CompilerServices.S witchExpressionException . In .NET Framework, the
exception is an InvalidOperationException . In most cases, the compiler generates a
warning if a switch expression doesn't handle all possible input values. List patterns
don't generate a warning when all possible inputs aren't handled.
For more information, see the switch  expression  section of the feature proposal note .
Use switch expression (style rule IDE0066)
Add missing cases to switch expression (style rule IDE0072)public readonly  struct Point 
{ 
    public Point(int x, int y) => (X, Y) = (x, y);  
     
    public int X { get; } 
    public int Y { get; } 
} 
static Point Transform (Point point ) => point switch 
{ 
    { X: 0, Y: 0 }                    => new Point(0, 0), 
    { X: var x, Y: var y } when x < y => new Point(x + y, y),  
    { X: var x, Y: var y } when x > y => new Point(x - y, y),  
    { X: var x, Y: var y }            => new Point(2 * x, 2 * y), 
}; 
Non-exhaustive switch expressions
 Tip
To guarantee that a switch expression handles all possible input values, provide a
switch expression arm with a discar d pattern.
C# language specification
See alsoC# reference
C# operators and expressions
Patterns
Tutorial: Use pattern matching to build type-driven and data-driven algorithms
switch  statementtrue and false operators - treat your
objects as a Boolean value
Article •04/08/2023
The true operator returns the bool value true to indicate that its operand is definitely
true. The false operator returns the bool value true to indicate that its operand is
definitely false. The true and false operators aren't guaranteed to complement each
other. That is, both the true and false operator might return the bool value false for
the same operand. If a type defines one of the two operators, it must also define
another operator.
A type with the defined true operator can be the type of a result of a controlling
conditional expression in the if, do, while , and for statements and in the conditional
operator ?:. For more information, see the Boolean expressions  section of the C#
language specification .
If a type with the defined true and false operators overloads  the logical OR operator
| or the logical AND operator  & in a certain way, the conditional logical OR operator
|| or conditional logical AND operator  &&, respectively, can be evaluated for the
operands of that type. For more information, see the User-defined conditional logical
operators  section of the C# language specification . Tip
Use the bool? type, if you need to support the three-valued logic (for example,
when you work with databases that support a three-valued Boolean type). C#
provides the & and | operators that support the three-valued logic with the bool?
operands. For more information, see the Nullable Boolean logical operat ors
section of the Boolean logical operat ors article.
Boolean expressions
User-defined conditional logical operators
ExampleThe following example presents the type that defines both true and false operators.
The type also overloads the logical AND operator & in such a way that the && operator
also can be evaluated for the operands of that type.
C#
public struct LaunchStatus  
{ 
    public static readonly  LaunchStatus Green = new LaunchStatus( 0); 
    public static readonly  LaunchStatus Yellow = new LaunchStatus( 1); 
    public static readonly  LaunchStatus Red = new LaunchStatus( 2); 
    private int status;
    private LaunchStatus (int status) 
    { 
        this.status = status;  
    } 
    public static bool operator  true(LaunchStatus x ) => x == Green || x ==  
Yellow; 
    public static bool operator  false(LaunchStatus x ) => x == Red;  
    public static LaunchStatus operator  &(LaunchStatus x, LaunchStatus y)  
    { 
        if (x == Red || y == Red || (x == Yellow && y == Yellow))  
        {  
            return Red; 
        }  
        if (x == Yellow || y == Yellow)  
        {  
            return Yellow;  
        }  
        return Green; 
    } 
    public static bool operator  ==(LaunchStatus x, LaunchStatus y) =>  
x.status == y.status;  
    public static bool operator  !=(LaunchStatus x, LaunchStatus y) => !(x ==  
y); 
    public override  bool Equals(object obj) => obj is LaunchStatus other &&  
this == other;  
    public override  int GetHashCode () => status;  
} 
public class LaunchStatusTest  
{ 
    public static void Main() 
    { 
        LaunchStatus okToLaunch = GetFuelLaunchStatus() &&  Notice the short-circuiting behavior of the && operator. When the GetFuelLaunchStatus
method returns LaunchStatus.Red, the right-hand operand of the && operator isn't
evaluated. That is because LaunchStatus.Red is definitely false. Then the result of the
logical AND doesn't depend on the value of the right-hand operand. The output of the
example is as follows:
Console
C# reference
C# operators and expressionsGetNavigationLaunchStatus();  
        Console.WriteLine(okToLaunch ? "Ready to go!"  : "Wait!"); 
    } 
    static LaunchStatus GetFuelLaunchStatus () 
    { 
        Console.WriteLine( "Getting fuel launch status..." ); 
        return LaunchStatus.Red;  
    } 
    static LaunchStatus GetNavigationLaunchStatus () 
    { 
        Console.WriteLine( "Getting navigation launch status..." ); 
        return LaunchStatus.Yellow;  
    } 
} 
Getting fuel launch status...  
Wait! 
See alsowith expression - Nondestructive
mutation creates a new object with
modified properties
Article •11/14/2023
A with expression produces a copy of its operand with the specified properties and
fields modified. Y ou use the object initializer  syntax to specify what members to modify
and their new values:
C#
using System;
public class WithExpressionBasicExample
{
    public record NamedPoint (string Name, int X, int Y);
    public static void Main()
    {
        var p1 = new NamedPoint( "A", 0, 0);
        Console.WriteLine( $"{nameof(p1)}: {p1}");  // output: p1: NamedPoint  
{ Name = A, X = 0, Y = 0 }
        
        var p2 = p1 with { Name = "B", X = 5 };
        Console.WriteLine( $"{nameof(p2)}: {p2}");  // output: p2: NamedPoint  
{ Name = B, X = 5, Y = 0 }
        
        var p3 = p1 with 
            { 
                Name = "C", 
                Y = 4 
            };
        Console.WriteLine( $"{nameof(p3)}: {p3}");  // output: p3: NamedPoint  
{ Name = C, X = 0, Y = 4 }
        Console.WriteLine( $"{nameof(p1)}: {p1}");  // output: p1: NamedPoint  
{ Name = A, X = 0, Y = 0 }
        var apples = new { Item = "Apples" , Price = 1.19m };
        Console.WriteLine( $"Original: {apples} ");  // output: Original: {  
Item = Apples, Price = 1.19 }
        var saleApples = apples with { Price = 0.79m };
        Console.WriteLine( $"Sale: {saleApples} ");  // output: Sale: { Item =  
Apples, Price = 0.79 }
    }
}The left-hand operand of a with expression can be of a record type . Beginning with C#
10, a left-hand operand of a with expression can also be of a structure type  or an
anonymous type .
The result of a with expression has the same run-time type as the expression's operand,
as the following example shows:
C#
In the case of a reference-type member, only the reference to a member instance is
copied when an operand is copied. Both the copy and original operand have access to
the same reference-type instance. The following example demonstrates that behavior:
C#using System;
public class InheritanceExample
{
    public record Point(int X, int Y);
    public record NamedPoint (string Name, int X, int Y) : Point(X, Y);
    public static void Main()
    {
        Point p1 = new NamedPoint( "A", 0, 0);
        Point p2 = p1 with { X = 5, Y = 3 };
        Console.WriteLine(p2 is NamedPoint);  // output: True
        Console.WriteLine(p2);  // output: NamedPoint { X = 5, Y = 3, Name =  
A }
    }
}
using System;
using System.Collections.Generic;
public class ExampleWithReferenceType
{
    public record TaggedNumber (int Number, List< string> Tags)
    {
        public string PrintTags () => string.Join(", ", Tags);
    }
    public static void Main()
    {
        var original = new TaggedNumber( 1, new List<string> { "A", "B" });
        var copy = original with { Number = 2 };
        Console.WriteLine( $"Tags of {nameof(copy)}: {copy.PrintTags()} ");
        // output: Tags of copy: A, BAny record class type has the copy constr uctor. A copy constr uctor is a constructor with a
single parameter of the containing record type. It copies the state of its argument to a
new record instance. At evaluation of a with expression, the copy constructor gets
called to instantiate a new record instance based on an original record. After that, the
new instance gets updated according to the specified modifications. By default, the copy
constructor is implicit, that is, compiler-generated. If you need to customize the record
copy semantics, explicitly declare a copy constructor with the desired behavior. The
following example updates the preceding example with an explicit copy constructor. The
new copy behavior is to copy list items instead of a list reference when a record is
copied:
C#        original.Tags.Add( "C");
        Console.WriteLine( $"Tags of {nameof(copy)}: {copy.PrintTags()} ");
        // output: Tags of copy: A, B, C
    }
}
Custom copy semantics
using System;
using System.Collections.Generic;
public class UserDefinedCopyConstructorExample
{
    public record TaggedNumber (int Number, List< string> Tags)
    {
        protected  TaggedNumber (TaggedNumber original )
        {
            Number = original.Number;
            Tags = new List<string>(original.Tags);
        }
        public string PrintTags () => string.Join(", ", Tags);
    }
    public static void Main()
    {
        var original = new TaggedNumber( 1, new List<string> { "A", "B" });
        var copy = original with { Number = 2 };
        Console.WriteLine( $"Tags of {nameof(copy)}: {copy.PrintTags()} ");
        // output: Tags of copy: A, B
        original.Tags.Add( "C");
        Console.WriteLine( $"Tags of {nameof(copy)}: {copy.PrintTags()} ");
        // output: Tags of copy: A, BYou can't customize the copy semantics for structure types.
For more information, see the following sections of the records feature proposal note :
with expression
Copy and Clone members
C# reference
C# operators and expressions
Records
Structure types    }
}
C# language specification
See also
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
 Provide product feedbackOperator overloading - predefined
unary, arithmetic, equality and
comparison operators
Article •04/08/2023
A user-defined type can overload a predefined C# operator. That is, a type can provide
the custom implementation of an operation in case one or both of the operands are of
that type. The Overloadable operators  section shows which C# operators can be
overloaded.
Use the operator keyword to declare an operator. An operator declaration must satisfy
the following rules:
It includes both a public and a static modifier.
A unary operator has one input parameter. A binary operator has two input
parameters. In each case, at least one parameter must have type T or T? where T
is the type that contains the operator declaration.
The following example defines a simplified structure to represent a rational number. The
structure overloads some of the arithmetic operators :
C#
public readonly  struct Fraction  
{ 
    private readonly  int num; 
    private readonly  int den; 
    public Fraction (int numerator, int denominator ) 
    { 
        if (denominator == 0) 
        {  
            throw new ArgumentException( "Denominator cannot be zero." , 
nameof(denominator));  
        }  
        num = numerator;  
        den = denominator;  
    } 
    public static Fraction operator  +(Fraction a) => a;  
    public static Fraction operator  -(Fraction a) => new Fraction(-a.num,  
a.den); 
    public static Fraction operator  +(Fraction a, Fraction b)  
        => new Fraction(a.num * b.den + b.num * a.den, a.den * b.den);  You could extend the preceding example by defining an implicit conversion  from int to
Fraction. Then, overloaded operators would support arguments of those two types.
That is, it would become possible to add an integer to a fraction and obtain a fraction as
a result.
You also use the operator keyword to define a custom type conversion. For more
information, see User-defined conversion operators .
The following table shows the operators that can be overloaded:
Operat ors Notes
+x, -x, !x, ~x, ++, --, true, false The true and false operators must be overloaded together.    public static Fraction operator  -(Fraction a, Fraction b)  
        => a + (-b);  
    public static Fraction operator  *(Fraction a, Fraction b)  
        => new Fraction(a.num * b.num, a.den * b.den);  
    public static Fraction operator  /(Fraction a, Fraction b)  
    { 
        if (b.num == 0)
        {  
            throw new DivideByZeroException();  
        }  
        return new Fraction(a.num * b.den, a.den * b.num);  
    } 
    public override  string ToString () => $"{num} / {den}"; 
} 
public static class OperatorOverloading  
{ 
    public static void Main() 
    { 
        var a = new Fraction( 5, 4); 
        var b = new Fraction( 1, 2); 
        Console.WriteLine(-a);   // output: -5 / 4  
        Console.WriteLine(a + b);  // output: 14 / 8  
        Console.WriteLine(a - b);  // output: 6 / 8  
        Console.WriteLine(a * b);  // output: 5 / 8  
        Console.WriteLine(a / b);  // output: 10 / 4  
    } 
} 
Overloadable operatorsOperat ors Notes
x + y , x - y, x * y, x / y, x % y ,  
x & y , x | y, x ^ y ,  
x << y , x >> y , x >>> y
x == y , x != y , x < y , x > y , x <= y ,
x >= yMust be overloaded in pairs as follows: == and !=, < and >,
<= and >=.
The following table shows the operators that can't be overloaded:
Operat ors Alternativ es
x && y , x || y Overload both the true and false operators and the & or |
operators. For more information, see User-defined
conditional logical operators .
a[i], a?[i] Define an indexer .
(T)x Define custom type conversions that can be performed by a
cast expression. For more information, see User-defined
conversion operators .
+=, -=, *=, /=, %=, &=, |=, ^=,
<<=, >>=, >>>=Overload the corresponding binary operator. For example,
when you overload the binary + operator, += is implicitly
overloaded.
^x, x = y , x.y, x?.y, c ? t : f , x ?? y , ??
= y, 
x..y, x->y, =>, f(x), as, await ,
checked , unchecked , default ,
delegate , is, nameof , new,  
sizeof , stackalloc , switch , typeof ,
withNone.
For more information, see the following sections of the C# language specification :
Operator overloading
OperatorsNon overloadable operators
C# language specification
See alsoC# reference
C# operators and expressions
User-defined conversion operators
Design guidelines - Operator overloads
Design guidelines - Equality operators
Why are overloaded operators always static in C#?Declaration statements
Article •06/21/2023
A declaration statement declares a new local variable, local constant, or local reference
variable . To declare a local variable, specify its type and provide its name. Y ou can
declare multiple variables of the same type in one statement, as the following example
shows:
C#
In a declaration statement, you can also initialize a variable with its initial value:
C#
The preceding examples explicitly specify the type of a variable. Y ou can also let the
compiler infer the type of a variable from its initialization expression. T o do that, use the
var keyword instead of a type's name. For more information, see the Implicitly-typed
local variables  section.
To declare a local constant, use the const  keyword , as the following example shows:
C#
When you declare a local constant, you must also initialize it.
For information about local reference variables, see the Reference variables  section.
When you declare a local variable, you can let the compiler infer the type of the variable
from the initialization expression. T o do that use the var keyword instead of the namestring greeting;
int a, b, c;
List<double> xs;
string greeting = "Hello";
int a = 3, b = 2, c = a + b;
List<double> xs = new();
const string Greeting = "Hello";
const double MinLimit = -10.0, MaxLimit = -MinLimit;
Implicitly-typed local variablesof a type:
C#
As the preceding example shows, implicitly-typed local variables are strongly typed.
A common use of var is with a constructor invocation expression . The use of var allows
you to not repeat a type name in a variable declaration and object instantiation, as the
following example shows:
C#
You can use a target-typed new expression  as an alternative:
C#
When you work with anonymous types , you must use implicitly-typed local variables.
The following example shows a query expression  that uses an anonymous type to hold a
customer's name and phone number:
C#var greeting = "Hello";
Console.WriteLine(greeting.GetType());  // output: System.String
var a = 32;
Console.WriteLine(a.GetType());  // output: System.Int32
var xs = new List<double>();
Console.WriteLine(xs.GetType());  // output:  
System.Collections.Generic.List`1[System.Double]
７ Note
When you use var in the enabled nullable awar e cont ext and the type of an
initialization expression is a reference type, the compiler always infers a nullable
reference type even if the type of an initialization expression isn't nullable.
var xs = new List<int>();
List<int> xs = new();
List<int>? ys = new();
var fromPhoenix = from cust in customers
                  where cust.City == "Phoenix"In the preceding example, you can't explicitly specify the type of the fromPhoenix
variable. The type is IEnumerable<T>  but in this case T is an anonymous type and you
can't provide its name. That's why you need to use var. For the same reason, you must
use var when you declare the customer iteration variable in the foreach statement.
For more information about implicitly-typed local variables, see Implicitly-typed local
variables .
In pattern matching, the var keyword is used in a var pattern .
When you declare a local variable and add the ref keyword before the variable's type,
you declare a reference variable , or a ref local:
C#
A reference variable is a variable that refers to another variable, which is called the
referent. That is, a reference variable is an alias to its referent. When you assign a value
to a reference variable, that value is assigned to the referent. When you read the value
of a reference variable, the referent's value is returned. The following example
demonstrates that behavior:
C#                  select new { cust.Name, cust.Phone };
foreach (var customer in fromPhoenix)
{
    Console.WriteLine( $"Name={customer.Name} , Phone= {customer.Phone} ");
}
Reference variables
ref int alias = ref variable;
int a = 1;
ref int alias = ref a;
Console.WriteLine( $"(a, alias) is ( {a}, {alias})");  // output: (a, alias)  
is (1, 1)
a = 2;
Console.WriteLine( $"(a, alias) is ( {a}, {alias})");  // output: (a, alias)  
is (2, 2)
alias = 3;Use the ref assignment operator  = ref to change the referent of a reference variable, as
the following example shows:
C#
In the preceding example, the element reference variable is initialized as an alias to the
first array element. Then it's ref reassigned to refer to the last array element.
You can define a ref readonly local variable. Y ou can't assign a value to a ref readonly
variable. However you can ref reassign such a reference variable, as the following
example shows:
C#
You can assign a reference return  to a reference variable, as the following example
shows:
C#Console.WriteLine( $"(a, alias) is ( {a}, {alias})");  // output: (a, alias)  
is (3, 3)
void Display(int[] s) => Console.WriteLine( string.Join(" ", s));
int[] xs = { 0, 0, 0 };
Display(xs);
ref int element = ref xs[0];
element = 1;
Display(xs);
element = ref xs[^1];
element = 3;
Display(xs);
// Output:
// 0 0 0
// 1 0 0
// 1 0 3
int[] xs = { 1, 2, 3 };
ref readonly  int element = ref xs[0];
// element = 100;  error CS0131: The left-hand side of an assignment must be  
a variable, property or indexer
Console.WriteLine(element);  // output: 1
element = ref xs[^1];
Console.WriteLine(element);  // output: 3In the preceding example, the GetReferenceToMax method is a returns-by-ref method. It
doesn't return the maximum value itself, but a reference return that is an alias to the
array element that holds the maximum value. The Run method assigns a reference
return to the max reference variable. Then, by assigning to max, it updates the internal
storage of the store instance. Y ou can also define a ref readonly method. The callers
of a ref readonly method can't assign a value to its reference return.
The iteration variable of the foreach statement can be a reference variable. For more
information, see the foreach  statement  section of the Iteration statements  article.using System;
public class NumberStore
{
    private readonly  int[] numbers = { 1, 30, 7, 1557, 381, 63, 1027, 2550, 
511, 1023 };
    public ref int GetReferenceToMax ()
    {
        ref int max = ref numbers[ 0];
        for (int i = 1; i < numbers.Length; i++)
        {
            if (numbers[i] > max)
            {
                max = ref numbers[i];
            }
        }
        return ref max;
    }
    public override  string ToString () => string.Join(" ", numbers);
}
public static class ReferenceReturnExample
{
    public static void Run()
    {
        var store = new NumberStore();
        Console.WriteLine( $"Original sequence: {store.ToString()} ");
        
        ref int max = ref store.GetReferenceToMax();
        max = 0;
        Console.WriteLine( $"Updated sequence:  {store.ToString()} ");
        // Output:
        // Original sequence: 1 30 7 1557 381 63 1027 2550 511 1023
        // Updated sequence:  1 30 7 1557 381 63 1027 0 511 1023
    }
}In performance-critical scenarios, the use of reference variables and returns might
increase performance by avoiding potentially expensive copy operations.
The compiler ensures that a reference variable doesn't outlive its referent and stays valid
for the whole of its lifetime. For more information, see the Ref safe contexts  section of
the C# language specification .
For information about the ref fields, see the ref fields  section of the ref structure types
article.
The contextual keyword scoped restricts the lifetime of a value. The scoped modifier
restricts the ref-safe-to-escape or safe-to-escape lifetime , respectively, to the current
method. Effectively, adding the scoped modifier asserts that your code won't extend the
lifetime of the variable.
You can apply scoped to a parameter or local variable. The scoped modifier may be
applied to parameters and locals when the type is a ref struct . Otherwise, the scoped
modifier may be applied only to local reference variables . That includes local variables
declared with the ref modifier and parameters declared with the in, ref or out
modifiers.
The scoped modifier is implicitly added to this in methods declared in a struct, out
parameters, and ref parameters when the type is a ref struct.
For more information, see the following sections of the C# language specification :
Declaration statements
Reference variables and returns
For more information about the scoped modifier, see the Low-level struct improvements
proposal note.
C# reference
Object and collection initializers
ref keywordscoped ref
C# language specification
See alsoReduce memory allocations using new C# features
'var' preferences (style rules IDE0007 and IDE0008)
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
 Provide product feedbackException-handling statements - throw,
try-catch, try-finally, and try-catch-
finally
Article •04/22/2023
You use the throw and try statements to work with exceptions. Use the throw
statement  to throw an exception. Use the try statement  to catch and handle exceptions
that might occur during execution of a code block.
The throw statement throws an exception:
C#
In a throw e; statement, the result of expression e must be implicitly convertible to
System.Exception .
You can use the built-in exception classes, for example, ArgumentOutOfRangeException
or InvalidOperationException . .NET also provides the helper methods to throw
exceptions in certain conditions: ArgumentNullException.ThrowIfNull  and
ArgumentException.ThrowIfNullOrEmpty . You can also define your own exception
classes that derive from System.Exception . For more information, see Creating and
throwing exceptions .
Inside a catch  block , you can use a throw; statement to re-throw the exception that is
handled by the catch block:
C#The throw statement
if (shapeAmount <= 0) 
{ 
    throw new ArgumentOutOfRangeException( nameof(shapeAmount), "Amount of  
shapes must be positive." ); 
} 
try 
{ 
    ProcessShapes(shapeAmount);  
} 
catch (Exception e)  When an exception is thrown, the common language runtime (CLR) looks for the catch
block  that can handle this exception. If the currently executed method doesn't contain
such a catch block, the CLR looks at the method that called the current method, and so
on up the call stack. If no catch block is found, the CLR terminates the executing thread.
For more information, see the How exceptions are handled  section of the C# language
specification .
You can also use throw as an expression. This might be convenient in a number of cases,
which include:
the conditional operator . The following example uses a throw expression to throw
an ArgumentException  when the passed array args is empty:
C#
the null-coalescing operator . The following example uses a throw expression to
throw an ArgumentNullException  when the string to assign to a property is null:
C#{ 
    LogError(e, "Shape processing failed." ); 
    throw; 
} 
７ Note
throw; preserves the original stack trace of the exception, which is stored in the
Exception.S tackT race property. Opposite to that, throw e; updates the StackT race
property of e.
The throw expression
string first = args.Length >= 1  
    ? args[ 0] 
    : throw new ArgumentException( "Please supply at least one  
argument." ); 
public string Name 
{ 
    get => name;  
    set => name = value ?? 
        throw new ArgumentNullException(paramName: nameof(value), an expression-bodied lambda  or method. The following example uses a throw
expression to throw an InvalidCastException  to indicate that a conversion to a
DateTime  value is not supported:
C#
You can use the try statement in any of the following forms: try-catch  - to handle
exceptions that might occur during execution of the code inside a try block, try-finally  -
to specify the code that is executed when control leaves the try block, and try-catch-
finally  - as a combination of the preceding two forms.
Use the try-catch statement to handle exceptions that might occur during execution of
a code block. Place the code where an exception might occur inside a try block. Use a
catch claus e to specify the base type of exceptions you want to handle in the
corresponding catch block:
C#
You can provide several catch clauses:
C#message: "Name cannot be null" ); 
} 
DateTime ToDateTime (IFormatProvider provider ) => 
         throw new InvalidCastException( "Conversion to a DateTime is  
not supported." ); 
The try statement
The try-catch statement
try 
{ 
    var result = Process( -3, 4); 
    Console.WriteLine( $"Processing succeeded: {result} "); 
} 
catch (ArgumentException e)  
{ 
    Console.WriteLine( $"Processing failed: {e.Message} "); 
} When an exception occurs, catch clauses are examined in the specified order, from top
to bottom. At maximum, only one catch block is executed for any thrown exception. As
the preceding example also shows, you can omit declaration of an exception variable
and specify only the exception type in a catch clause. A catch clause without any
specified exception type matches any exception and, if present, must be the last catch
clause.
If you want to re-throw a caught exception, use the throw  statement , as the following
example shows:
C#try 
{ 
    var result = await ProcessAsync( -3, 4, cancellationToken);  
    Console.WriteLine( $"Processing succeeded: {result} "); 
} 
catch (ArgumentException e)  
{ 
    Console.WriteLine( $"Processing failed: {e.Message} "); 
} 
catch (OperationCanceledException)  
{ 
    Console.WriteLine( "Processing is cancelled." ); 
} 
try 
{ 
    var result = Process( -3, 4); 
    Console.WriteLine( $"Processing succeeded: {result} "); 
} 
catch (Exception e)  
{ 
    LogError(e, "Processing failed." ); 
    throw; 
} 
７ Note
throw; preserves the original stack trace of the exception, which is stored in the
Exception.S tackT race property. Opposite to that, throw e; updates the StackT race
property of e.
A when exception filterAlong with an exception type, you can also specify an exception filter that further
examines an exception and decides if the corresponding catch block handles that
exception. An exception filter is a Boolean expression that follows the when keyword, as
the following example shows:
C#
The preceding example uses an exception filter to provide a single catch block to
handle exceptions of two specified types.
You can provide several catch clauses for the same exception type if they distinguish by
exception filters. One of those clauses might have no exception filter. If such a clause
exists, it must be the last of the clauses that specify that exception type.
If a catch clause has an exception filter, it can specify the exception type that is the
same as or less derived than an exception type of a catch clause that appears after it.
For example, if an exception filter is present, a catch (Exception e) clause doesn't need
to be the last clause.
If an exception occurs in an async function , it propagates to the caller of the function
when you await  the result of the function, as the following example shows:
C#try 
{ 
    var result = Process( -3, 4); 
    Console.WriteLine( $"Processing succeeded: {result} "); 
} 
catch (Exception e) when (e is ArgumentException || e is 
DivideByZeroException)  
{ 
    Console.WriteLine( $"Processing failed: {e.Message} "); 
} 
Exceptions in async and iterator methods
public static async Task Run() 
{ 
    try 
    { 
        Task< int> processing = ProcessAsync( -1); 
        Console.WriteLine( "Launched processing." ); 
        int result = await processing;  
        Console.WriteLine( $"Result: {result} ."); If an exception occurs in an iterator method , it propagates to the caller only when the
iterator advances to the next element.
In a try-finally statement, the finally block is executed when control leaves the try
block. Control might leave the try block as a result of
normal execution,
execution of a jump statement  (that is, return, break, continue, or goto), or
propagation of an exception out of the try block.
The following example uses the finally block to reset the state of an object before
control leaves the method:
C#    } 
    catch (ArgumentException e)  
    { 
        Console.WriteLine( $"Processing failed: {e.Message} "); 
    } 
    // Output:  
    // Launched processing.  
    // Processing failed: Input must be non-negative. (Parameter 'input')  
} 
private static async Task<int> ProcessAsync (int input) 
{ 
    if (input < 0) 
    { 
        throw new ArgumentOutOfRangeException( nameof(input), "Input must be  
non-negative." ); 
    } 
    await Task.Delay( 500); 
    return input; 
} 
The try-finally statement
public async Task HandleRequest (int itemId, CancellationToken ct ) 
{ 
    Busy = true; 
    try 
    { 
        await ProcessAsync(itemId, ct);  
    } 
    finally 
    { You can also use the finally block to clean up allocated resources used in the try
block.
In almost all cases finally blocks are executed. The only cases where finally blocks
aren't executed involve immediate termination of a program. For example, such a
termination might happen because of the Environment.F ailFast call or an
OverflowException  or InvalidProgramException  exception. Most operating systems
perform a reasonable resource clean-up as part of stopping and unloading the process.
You use a try-catch-finally statement both to handle exceptions that might occur
during execution of the try block and specify the code that must be executed when
control leaves the try statement:
C#        Busy = false; 
    } 
} 
７ Note
When the type of a resource implements the IDisposable  or IAsyncDisposable
interface, consider the using  statement . The using statement ensures that acquired
resources are disposed when control leaves the using statement. The compiler
transforms a using statement into a try-finally statement.
The try-catch-finally statement
public async Task ProcessRequest (int itemId, CancellationToken ct ) 
{ 
    Busy = true; 
    try 
    { 
        await ProcessAsync(itemId, ct);  
    } 
    catch (Exception e) when (e is not OperationCanceledException)  
    { 
        LogError(e, $"Failed to process request for item ID {itemId} ."); 
        throw; 
    } 
    finally 
    { 
        Busy = false; 
    } When an exception is handled by a catch block, the finally block is executed after
execution of that catch block (even if another exception occurs during execution of the
catch block). For information about catch and finally blocks, see The try-catch
statement  and The try-finally  statement  sections, respectively.
For more information, see the following sections of the C# language specification :
The throw  statement
The try statement
Exceptions
C# reference
Exceptions and exception handling
Handling and throwing exceptions in .NET
throw preferences (style rule IDE0016)
AppDomain.FirstChanceException
AppDomain.UnhandledException
TaskScheduler.UnobservedT askException} 
C# language specification
See alsoIteration statemen ts - for, foreach, do,
and while
Article •11/14/2023
The iteration statements repeatedly execute a statement or a block of statements. The
for statement  executes its body while a specified Boolean expression evaluates to true.
The foreach  statement  enumerates the elements of a collection and executes its body
for each element of the collection. The do statement  conditionally executes its body one
or more times. The while  statement  conditionally executes its body zero or more times.
At any point within the body of an iteration statement, you can break out of the loop
using the break  statement . You can step to the next iteration in the loop using the
continue  statement .
The for statement executes a statement or a block of statements while a specified
Boolean expression evaluates to true. The following example shows the for statement
that executes its body while an integer counter is less than three:
C#
The preceding example shows the elements of the for statement:
The initializer  section that is executed only once, before entering the loop.
Typically, you declare and initialize a local loop variable in that section. The
declared variable can't be accessed from outside the for statement.
The initializer  section in the preceding example declares and initializes an integer
counter variable:
C#The for statement
for (int i = 0; i < 3; i++)
{
    Console.Write(i);
}
// Output:
// 012
int i = 0The condition  section that determines if the next iteration in the loop should be
executed. If it evaluates to true or isn't present, the next iteration is executed;
otherwise, the loop is exited. The condition  section must be a Boolean expression.
The condition  section in the preceding example checks if a counter value is less
than three:
C#
The iterator section that defines what happens after each execution of the body of
the loop.
The iterator section in the preceding example increments the counter:
C#
The body of the loop, which must be a statement or a block of statements.
The iterator section can contain zero or more of the following statement expressions,
separated by commas:
prefix or postfix increment  expression, such as ++i or i++
prefix or postfix decrement  expression, such as --i or i--
assignment
invocation of a method
await  expression
creation of an object by using the new operator
If you don't declare a loop variable in the initializer section, you can use zero or more of
the expressions from the preceding list in the initializer section as well. The following
example shows several less common usages of the initializer and iterator sections:
assigning a value to an external variable in the initializer section, invoking a method in
both the initializer and the iterator sections, and changing the values of two variables in
the iterator section:
C#i < 3
i++
int i;
int j = 3;
for (i = 0, Console.WriteLine( $"Start: i= {i}, j={j}"); i < j; i++, j--,  All the sections of the for statement are optional. For example, the following code
defines the infinite for loop:
C#
The foreach statement executes a statement or a block of statements for each element
in an instance of the type that implements the System.Collections.IEnumerable  or
System.Collections.Generic.IEnumerable<T>  interface, as the following example shows:
C#
The foreach statement isn't limited to those types. Y ou can use it with an instance of
any type that satisfies the following conditions:
A type has the public parameterless GetEnumerator method. The GetEnumerator
method can be a type's extension method .
The return type of the GetEnumerator method has the public Current property and
the public parameterless MoveNext method whose return type is bool.
The following example uses the foreach statement with an instance of the
System.Span<T>  type, which doesn't implement any interfaces:Console.WriteLine( $"Step: i= {i}, j={j}"))
{
    //...
}
// Output:
// Start: i=0, j=3
// Step: i=1, j=2
// Step: i=2, j=1
for ( ; ; )
{
    //...
}
The foreach statement
var fibNumbers = new List<int> { 0, 1, 1, 2, 3, 5, 8, 13 };
foreach (int element in fibNumbers)
{
    Console.Write( $"{element}  ");
}
// Output:
// 0 1 1 2 3 5 8 13C#
If the enumerator's Current property returns a reference return value  (ref T where T is
the type of a collection element), you can declare an iteration variable with the ref or
ref readonly modifier, as the following example shows:
C#
If the source collection of the foreach statement is empty, the body of the foreach
statement isn't executed and skipped. If the foreach statement is applied to null, a
NullR eferenceException  is thrown.
You can use the await foreach statement to consume an asynchronous stream of data,
that is, the collection type that implements the IAsyncEnumerable<T>  interface. Each
iteration of the loop may be suspended while the next element is retrieved
asynchronously. The following example shows how to use the await foreach statement:
C#Span<int> numbers = new int[] { 3, 14, 15, 92, 6 };
foreach (int number in numbers)
{
    Console.Write( $"{number}  ");
}
// Output:
// 3 14 15 92 6
Span<int> storage = stackalloc  int[10];
int num = 0;
foreach (ref int item in storage)
{
    item = num++;
}
foreach (ref readonly  var item in storage)
{
    Console.Write( $"{item} ");
}
// Output:
// 0 1 2 3 4 5 6 7 8 9
await foreach
await foreach (var item in GenerateSequenceAsync ())
{You can also use the await foreach statement with an instance of any type that satisfies
the following conditions:
A type has the public parameterless GetAsyncEnumerator method. That method can
be a type's extension method .
The return type of the GetAsyncEnumerator method has the public Current
property and the public parameterless MoveNextAsync method whose return type is
Task<bool> , ValueT ask<bool> , or any other awaitable type whose awaiter's
GetResult method returns a bool value.
By default, stream elements are processed in the captured context. If you want to
disable capturing of the context, use the
TaskAsyncEnumerableExtensions.ConfigureA wait extension method. For more
information about synchronization contexts and capturing the current context, see
Consuming the T ask-based asynchronous pattern . For more information about
asynchronous streams, see the Asynchronous streams tutorial .
You can use the var keyword  to let the compiler infer the type of an iteration variable in
the foreach statement, as the following code shows:
C#
You can also explicitly specify the type of an iteration variable, as the following code
shows:
C#    Console.WriteLine(item);
}
Type of an iteration variable
foreach (var item in collection) { }
７ Note
Type of var can be inferred by the compiler as a nullable reference type,
depending on whether the nullable awar e cont ext is enabled and whether the type
of an initialization expression is a reference type. For more information see
Implicitly-typed local v ariables .In the preceding form, type T of a collection element must be implicitly or explicitly
convertible to type V of an iteration variable. If an explicit conversion from T to V fails
at run time, the foreach statement throws an InvalidCastException . For example, if T is
a non-sealed class type, V can be any interface type, even the one that T doesn't
implement. At run time, the type of a collection element may be the one that derives
from T and actually implements V. If that's not the case, an InvalidCastException  is
thrown.
The do statement executes a statement or a block of statements while a specified
Boolean expression evaluates to true. Because that expression is evaluated after each
execution of the loop, a do loop executes one or more times. The do loop differs from
the while  loop , which executes zero or more times.
The following example shows the usage of the do statement:
C#
The while statement executes a statement or a block of statements while a specified
Boolean expression evaluates to true. Because that expression is evaluated before each
execution of the loop, a while loop executes zero or more times. The while loop differs
from the do loop , which executes one or more times.
The following example shows the usage of the while statement:
C#IEnumerable<T> collection = new T[5];
foreach (V item in collection) { }
The do statement
int n = 0;
do
{
    Console.Write(n);
    n++;
} while (n < 5);
// Output:
// 01234
The while statementFor more information, see the following sections of the C# language specification :
The for statement
The foreach  statement
The do statement
The while  statement
For more information about these features, see the following feature proposal notes:
Async streams
Extension GetEnumerator  support for foreach  loops
C# reference
Declarations
Iteratorsint n = 0;
while (n < 5)
{
    Console.Write(n);
    n++;
}
// Output:
// 01234
C# language specification
See also
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
 Provide product feedbackSelection statements - if, if-else, and
switch
Article •04/28/2023
The if, if-else and switch statements select statements to execute from many
possible paths based on the value of an expression. The if statement  executes a
statement only if a provided Boolean expression evaluates to true. The if-else
statement  allows you to choose which of the two code paths to follow based on a
Boolean expression. The switch  statement  selects a statement list to execute based on a
pattern match with an expression.
An if statement can be any of the following two forms:
An if statement with an else part selects one of the two statements to execute
based on the value of a Boolean expression, as the following example shows:
C#
An if statement without an else part executes its body only if a Boolean
expression evaluates to true, as the following example shows:
C#The if statement
DisplayWeatherReport( 15.0);  // Output: Cold.
DisplayWeatherReport( 24.0);  // Output: Perfect!
void DisplayWeatherReport (double tempInCelsius )
{
    if (tempInCelsius < 20.0)
    {
        Console.WriteLine( "Cold.");
    }
    else
    {
        Console.WriteLine( "Perfect!" );
    }
}
DisplayMeasurement( 45);  // Output: The measurement value is 45
DisplayMeasurement( -3);  // Output: Warning: not acceptable value! The  
measurement value is -3You can nest if statements to check multiple conditions, as the following example
shows:
C#
In an expression context, you can use the conditional operator ?: to evaluate one of the
two expressions based on the value of a Boolean expression.
The switch statement selects a statement list to execute based on a pattern match with
a match expression, as the following example shows:void DisplayMeasurement (double value)
{
    if (value < 0 || value > 100)
    {
        Console.Write( "Warning: not acceptable value! " );
    }
    Console.WriteLine( $"The measurement value is {value}");
}
DisplayCharacter( 'f');  // Output: A lowercase letter: f
DisplayCharacter( 'R');  // Output: An uppercase letter: R
DisplayCharacter( '8');  // Output: A digit: 8
DisplayCharacter( ',');  // Output: Not alphanumeric character: ,
void DisplayCharacter (char ch)
{
    if (char.IsUpper(ch))
    {
        Console.WriteLine( $"An uppercase letter: {ch}");
    }
    else if (char.IsLower(ch))
    {
        Console.WriteLine( $"A lowercase letter: {ch}");
    }
    else if (char.IsDigit(ch))
    {
        Console.WriteLine( $"A digit: {ch}");
    }
    else
    {
        Console.WriteLine( $"Not alphanumeric character: {ch}");
    }
}
The switch statementC#
At the preceding example, the switch statement uses the following patterns:
A relational pattern : to compare an expression result with a constant.
A constant pattern : test if an expression result equals a constant.
The preceding example also demonstrates the default case. The default case specifies
statements to execute when a match expression doesn't match any other case pattern. If
a match expression doesn't match any case pattern and there's no default case, control
falls through a switch statement.
A switch statement executes the statement list  in the first switch section  whose case
pattern matches a match expression and whose case guard , if present, evaluates toDisplayMeasurement( -4);  // Output: Measured value is -4; too low.
DisplayMeasurement( 5);  // Output: Measured value is 5.
DisplayMeasurement( 30);  // Output: Measured value is 30; too high.
DisplayMeasurement( double.NaN);  // Output: Failed measurement.
void DisplayMeasurement (double measurement )
{
    switch (measurement)
    {
        case < 0.0:
            Console.WriteLine( $"Measured value is {measurement} ; too low." );
            break;
        case > 15.0:
            Console.WriteLine( $"Measured value is {measurement} ; too 
high.");
            break;
        case double.NaN:
            Console.WriteLine( "Failed measurement." );
            break;
        default:
            Console.WriteLine( $"Measured value is {measurement} .");
            break;
    }
}
） Impor tant
For information about the patterns supported by the switch statement, see
Patterns.true. A switch statement evaluates case patterns in text order from top to bottom. The
compiler generates an error when a switch statement contains an unreachable case.
That is a case that is already handled by an upper case or whose pattern is impossible to
match.
You can specify multiple case patterns for one section of a switch statement, as the
following example shows:
C#
Within a switch statement, control can't fall through from one switch section to the
next. As the examples in this section show, typically you use the break statement at the
end of each switch section to pass control out of a switch statement. Y ou can also use
the return  and throw  statements to pass control out of a switch statement. T o imitate
the fall-through behavior and pass control to other switch section, you can use the goto
statement .７ Note
The default case can appear in any place within a switch statement. R egardless of
its position, the default case is evaluated only if all other case patterns aren't
matched or the goto default; statement is executed in one of the switch sections.
DisplayMeasurement( -4);  // Output: Measured value is -4; out of an  
acceptable range.
DisplayMeasurement( 50);  // Output: Measured value is 50.
DisplayMeasurement( 132);  // Output: Measured value is 132; out of an  
acceptable range.
void DisplayMeasurement (int measurement )
{
    switch (measurement)
    {
        case < 0:
        case > 100:
            Console.WriteLine( $"Measured value is {measurement} ; out of an  
acceptable range." );
            break;
        
        default:
            Console.WriteLine( $"Measured value is {measurement} .");
            break;
    }
}In an expression context, you can use the switch  expression  to evaluate a single
expression from a list of candidate expressions based on a pattern match with an
expression.
A case pattern may be not expressive enough to specify the condition for the execution
of the switch section. In such a case, you can use a case guar d. That is an additional
condition that must be satisfied together with a matched pattern. A case guard must be
a Boolean expression. Y ou specify a case guard after the when keyword that follows a
pattern, as the following example shows:
C#
The preceding example uses positional patterns  with nested relational patterns .
For more information, see the following sections of the C# language specification :
The if statement
The switch  statementCase guards
DisplayMeasurements( 3, 4);  // Output: First measurement is 3, second  
measurement is 4.
DisplayMeasurements( 5, 5);  // Output: Both measurements are valid and equal  
to 5.
void DisplayMeasurements (int a, int b)
{
    switch ((a, b))
    {
        case (> 0, > 0) when a == b:
            Console.WriteLine( $"Both measurements are valid and equal to 
{a}.");
            break;
        case (> 0, > 0):
            Console.WriteLine( $"First measurement is {a}, second measurement  
is {b}.");
            break;
        default:
            Console.WriteLine( "One or both measurements are not valid." );
            break;
    }
}
C# language specificationFor more information about patterns, see the Patterns and pattern matching  section of
the C# language specification .
C# reference
Conditional operator ?:
Logical operators
Patterns
switch  expression
Add missing cases to switch statement (style rule IDE0010)See also
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
 Provide product feedbackJump statemen ts - break, continue,
return, and goto
Article •03/15/2023
The jump statements unconditionally transfer control. The break  statement  terminates
the closest enclosing iteration statement  or switch  statement . The continue  statement
starts a new iteration of the closest enclosing iteration statement . The return  statement
terminates execution of the function in which it appears and returns control to the caller.
The goto  statement  transfers control to a statement that is marked by a label.
For information about the throw statement that throws an exception and
unconditionally transfers control as well, see The throw  statement  section of the
Exception-handling statements  article.
The break statement terminates the closest enclosing iteration statement  (that is, for,
foreach, while, or do loop) or switch  statement . The break statement transfers control
to the statement that follows the terminated statement, if any.
C#
In nested loops, the break statement terminates only the innermost loop that contains
it, as the following example shows:
C#The break statement
int[] numbers = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
foreach (int number in numbers)
{
    if (number == 3)
    {
        break;
    }
    Console.Write( $"{number}  ");
}
Console.WriteLine();
Console.WriteLine( "End of the example." );
// Output:
// 0 1 2 
// End of the example.When you use the switch statement inside a loop, a break statement at the end of a
switch section transfers control only out of the switch statement. The loop that contains
the switch statement is unaffected, as the following example shows:
C#for (int outer = 0; outer < 5; outer++)
{
    for (int inner = 0; inner < 5; inner++)
    {
        if (inner > outer)
        {
            break;
        }
        Console.Write( $"{inner} ");
    }
    Console.WriteLine();
}
// Output:
// 0
// 0 1
// 0 1 2
// 0 1 2 3
// 0 1 2 3 4
double[] measurements = { -4, 5, 30, double.NaN };
foreach (double measurement in measurements)
{
    switch (measurement)
    {
        case < 0.0:
            Console.WriteLine( $"Measured value is {measurement} ; too low." );
            break;
        case > 15.0:
            Console.WriteLine( $"Measured value is {measurement} ; too 
high.");
            break;
        case double.NaN:
            Console.WriteLine( "Failed measurement." );
            break;
        default:
            Console.WriteLine( $"Measured value is {measurement} .");
            break;
    }
}
// Output:
// Measured value is -4; too low.The continue statement starts a new iteration of the closest enclosing iteration
statement  (that is, for, foreach, while, or do loop), as the following example shows:
C#
The return statement terminates execution of the function in which it appears and
returns control and the function's result, if any, to the caller.
If a function member doesn't compute a value, you use the return statement without
expression, as the following example shows:
C#// Measured value is 5.
// Measured value is 30; too high.
// Failed measurement.
The continue statement
for (int i = 0; i < 5; i++)
{
    Console.Write( $"Iteration {i}: ");
    
    if (i < 3)
    {
        Console.WriteLine( "skip");
        continue ;
    }
    
    Console.WriteLine( "done");
}
// Output:
// Iteration 0: skip
// Iteration 1: skip
// Iteration 2: skip
// Iteration 3: done
// Iteration 4: done
The return statement
Console.WriteLine( "First call:" );
DisplayIfNecessary( 6);
Console.WriteLine( "Second call:" );
DisplayIfNecessary( 5);
void DisplayIfNecessary (int number)As the preceding example shows, you typically use the return statement without
expression to terminate a function member early. If a function member doesn't contain
the return statement, it terminates after its last statement is executed.
If a function member computes a value, you use the return statement with an
expression, as the following example shows:
C#
When the return statement has an expression, that expression must be implicitly
convertible to the return type of a function member unless it's async . The expression
returned from an async function must be implicitly convertible to the type argument of
Task<TR esult>  or ValueT ask<TR esult> , whichever is the return type of the function. If the
return type of an async function is Task or ValueT ask, you use the return statement
without expression.
By default, the return statement returns the value of an expression. Y ou can return a
reference to a variable. R eference return values (or ref returns) are values that a method
returns by reference to the caller. That is, the caller can modify the value returned by a
method, and that change is reflected in the state of the object in the called method. T o{
    if (number % 2 == 0)
    {
        return;
    }
    Console.WriteLine(number);
}
// Output:
// First call:
// Second call:
// 5
double surfaceArea = CalculateCylinderSurfaceArea( 1, 1);
Console.WriteLine( $"{surfaceArea:F2} "); // output: 12.57
double CalculateCylinderSurfaceArea (double baseRadius, double height)
{
    double baseArea = Math.PI * baseRadius * baseRadius;
    double sideArea = 2 * Math.PI * baseRadius * height;
    return 2 * baseArea + sideArea;
}
Ref returnsdo that, use the return statement with the ref keyword, as the following example
shows:
C#
A reference return value allows a method to return a reference to a variable, rather than
a value, back to a caller. The caller can then choose to treat the returned variable as if it
were returned by value or by reference. The caller can create a new variable that is itself
a reference to the returned value, called a ref local . A reference return value means that a
method returns a reference (or an alias) to some variable. That variable's scope must
include the method. That variable's lifetime must extend beyond the return of the
method. Modifications to the method's return value by the caller are made to the
variable that is returned by the method.
Declaring that a method returns a reference return value indicates that the method
returns an alias to a variable. The design intent is often that calling code accesses that
variable through the alias, including to modify it. Methods returning by reference can't
have the return type void.
In order for the caller to modify the object's state, the reference return value must be
stored to a variable that is explicitly defined as a reference variable .
The ref return value is an alias to another variable in the called method's scope. Y ou
can interpret any use of the ref return as using the variable it aliases:
When you assign its value, you're assigning a value to the variable it aliases.
When you read its value, you're reading the value of the variable it aliases.
If you return it by reference, you're returning an alias to that same variable.var xs = new int[] { 10, 20, 30, 40 };
ref int found = ref FindFirst (xs, s => s == 30);
found = 0;
Console.WriteLine( string.Join(" ", xs));  // output: 10 20 0 40
ref int FindFirst (int[] numbers, Func< int, bool> predicate )
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (predicate(numbers[i]))
        {
            return ref numbers[i];
        }
    }
    throw new InvalidOperationException( "No element satisfies the given  
condition." );
}If you pass it to another method by reference, you're passing a reference to the
variable it aliases.
When you make a ref local  alias, you make a new alias to the same variable.
A ref return must be ref-safe-c ontext to the calling method. That means:
The return value must have a lifetime that extends beyond the execution of the
method. In other words, it can't be a local variable in the method that returns it. It
can be an instance or static field of a class, or it can be an argument passed to the
method. Attempting to return a local variable generates compiler error CS8168,
"Can't return local 'obj' by reference because it isn't a ref local."
The return value can't be the literal null. A method with a ref return can return an
alias to a variable whose value is currently the null (uninstantiated) value or a
nullable value type  for a value type.
The return value can't be a constant, an enumeration member, the by-value return
value from a property, or a method of a class or struct.
In addition, reference return values aren't allowed on async methods. An asynchronous
method may return before it has finished execution, while its return value is still
unknown.
A method that returns a reference return value must:
Include the ref keyword in front of the return type.
Each return  statement in the method body includes the ref keyword in front of the
name of the returned instance.
The following example shows a method that satisfies those conditions and returns a
reference to a Person object named p:
C#
Here's a more complete ref return example, showing both the method signature and
method body.
C#public ref Person GetContactInformation (string fname, string lname)
{
    // ...method implementation...
    return ref p;
}
public static ref int Find(int[,] matrix, Func< int, bool> predicate )
{The called method may also declare the return value as ref readonly to return the value
by reference, and enforce that the calling code can't modify the returned value. The
calling method can avoid copying the returned value by storing the value in a local ref
readonly reference variable.
The following example defines a Book class that has two String  fields, Title and Author.
It also defines a BookCollection class that includes a private array of Book objects.
Individual book objects are returned by reference by calling its GetBookByTitle method.
C#    for (int i = 0; i < matrix.GetLength( 0); i++)
        for (int j = 0; j < matrix.GetLength( 1); j++)
            if (predicate(matrix[i, j]))
                return ref matrix[i, j];
    throw new InvalidOperationException( "Not found" );
}
public class Book
{
    public string Author;
    public string Title;
}
public class BookCollection
{
    private Book[] books = { new Book { Title = "Call of the Wild, The" , 
Author = "Jack London"  },
                        new Book { Title = "Tale of Two Cities, A" , Author =  
"Charles Dickens"  }
                       };
    private Book nobook = null;
    public ref Book GetBookByTitle (string title)
    {
        for (int ctr = 0; ctr < books.Length; ctr++)
        {
            if (title == books[ctr].Title)
                return ref books[ctr];
        }
        return ref nobook;
    }
    public void ListBooks ()
    {
        foreach (var book in books)
        {
            Console.WriteLine( $"{book.Title} , by {book.Author} ");
        }
        Console.WriteLine();When the caller stores the value returned by the GetBookByTitle method as a ref local,
changes that the caller makes to the return value are reflected in the BookCollection
object, as the following example shows.
C#
The goto statement transfers control to a statement that is marked by a label, as the
following example shows:
C#    }
}
var bc = new BookCollection();
bc.ListBooks();
ref var book = ref bc.GetBookByTitle( "Call of the Wild, The" );
if (book != null)
    book = new Book { Title = "Republic, The" , Author = "Plato" };
bc.ListBooks();
// The example displays the following output:
//       Call of the Wild, The, by Jack London
//       Tale of Two Cities, A, by Charles Dickens
//
//       Republic, The, by Plato
//       Tale of Two Cities, A, by Charles Dickens
The goto statement
var matrices = new Dictionary< string, int[][]>
{
    ["A"] = new[]
    {
        new[] { 1, 2, 3, 4 },
        new[] { 4, 3, 2, 1 }
    },
    ["B"] = new[]
    {
        new[] { 5, 6, 7, 8 },
        new[] { 8, 7, 6, 5 }
    },
};
CheckMatrices(matrices, 4);
void CheckMatrices (Dictionary< string, int[][]> matrixLookup, int target)
{
    foreach (var (key, matrix) in matrixLookup)As the preceding example shows, you can use the goto statement to get out of a nested
loop.
You can also use the goto statement in the switch  statement  to transfer control to a
switch section with a constant case label, as the following example shows:
C#    {
        for (int row = 0; row < matrix.Length; row++)
        {
            for (int col = 0; col < matrix[row].Length; col++)
            {
                if (matrix[row][col] == target)
                {
                    goto Found;
                }
            }
        }
        Console.WriteLine( $"Not found {target}  in matrix {key}.");
        continue ;
    Found:
        Console.WriteLine( $"Found {target}  in matrix {key}.");
    }
}
// Output:
// Found 4 in matrix A.
// Not found 4 in matrix B.
 Tip
When you work with nested loops, consider refactoring separate loops into
separate methods. That may lead to a simpler, more readable code without the
goto statement.
using System;
public enum CoffeeChoice
{
    Plain,
    WithMilk,
    WithIceCream,
}
public class GotoInSwitchExample
{
    public static void Main()
    {Within the switch statement, you can also use the statement goto default; to transfer
control to the switch section with the default label.
If a label with the given name doesn't exist in the current function member, or if the
goto statement isn't within the scope of the label, a compile-time error occurs. That is,
you can't use the goto statement to transfer control out of the current function member
or into any nested scope.
For more information, see the following sections of the C# language specification :
The break  statement
The continue  statement
The return  statement
The goto  statement        Console.WriteLine(CalculatePrice(CoffeeChoice.Plain));  // output:  
10.0
        Console.WriteLine(CalculatePrice(CoffeeChoice.WithMilk));  // 
output: 15.0
        Console.WriteLine(CalculatePrice(CoffeeChoice.WithIceCream));  // 
output: 17.0
    }
    private static decimal CalculatePrice (CoffeeChoice choice )
    {
        decimal price = 0;
        switch (choice)
        {
            case CoffeeChoice.Plain:
                price += 10.0m;
                break;
            case CoffeeChoice.WithMilk:
                price += 5.0m;
                goto case CoffeeChoice.Plain;
            case CoffeeChoice.WithIceCream:
                price += 7.0m;
                goto case CoffeeChoice.Plain;
        }
        return price;
    }
}
C# language specification
See alsoC# reference
yield  statement
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
 Provide product feedbackchecked and unchecked statements (C#
reference)
Article •04/08/2023
The checked and unchecked statements specify the overflow-checking context for
integral-type arithmetic operations and conversions. When integer arithmetic overflow
occurs, the overflow-checking context defines what happens. In a checked context, a
System.OverflowException  is thrown; if overflow happens in a constant expression, a
compile-time error occurs. In an unchecked context, the operation result is truncated by
discarding any high-order bits that don't fit in the destination type. For example, in the
case of addition it wraps from the maximum value to the minimum value. The following
example shows the same operation in both a checked and unchecked context:
C#
For more information, see the Arithmetic overflow and division by zero  and User-
defined checked operators  sections of the Arithmetic operators  article.uint a = uint.MaxValue;  
unchecked  
{ 
    Console.WriteLine(a + 3);  // output: 2  
} 
try 
{ 
    checked  
    { 
        Console.WriteLine(a + 3); 
    } 
} 
catch (OverflowException e)  
{ 
    Console.WriteLine(e.Message);  // output: Arithmetic operation resulted  
in an overflow.  
} 
７ Note
The behavior of user-defined operators and conversions in the case of overflow can
differ from the one described in the preceding paragraph. In particular, user-
defined check ed operat ors might not throw an exception in a checked context.To specify the overflow-checking context for an expression, you can also use the
checked and unchecked operators, as the following example shows:
C#
The checked and unchecked statements and operators only affect the overflow-checking
context for those operations that are textually  inside the statement block or operator's
parentheses, as the following example shows:
C#double a = double.MaxValue;  
int b = unchecked ((int)a); 
Console.WriteLine(b);  // output: -2147483648  
try 
{ 
    b = checked(( int)a); 
} 
catch (OverflowException e)  
{ 
    Console.WriteLine(e.Message);  // output: Arithmetic operation resulted  
in an overflow.  
} 
int Multiply (int a, int b) => a * b;  
int factor = 2; 
try 
{ 
    checked  
    { 
        Console.WriteLine(Multiply(factor, int.MaxValue));  // output: -2  
    } 
} 
catch (OverflowException e)  
{ 
    Console.WriteLine(e.Message);
} 
try 
{ 
    checked  
    { 
        Console.WriteLine(Multiply(factor, factor * int.MaxValue));  
    } 
} 
catch (OverflowException e)  
{ At the preceding example, the first invocation of the Multiply local function shows that
the checked statement doesn't affect the overflow-checking context within the Multiply
function as no exception is thrown. At the second invocation of the Multiply function,
the expression that calculates the second argument of the function is evaluated in a
checked context and results in an exception as it's textually inside the block of the
checked statement.
The overflow-checking context affects the following operations:
The following built-in arithmetic operators : unary ++, --, - and binary +, -, *,
and / operators, when their operands are of an integral type (that is, either
integral numeric  or char type) or an enum  type.
Explicit numeric conversions  between integral types or from float or double  to an
integral type.
Beginning with C# 11, user-defined checked operators and conversions. For more
information, see the User-defined checked operators  section of the Arithmetic
operators  article.
If you don't specify the overflow-checking context, the value of the
CheckForOv erflowUnder flow compiler option defines the default context for non-
constant expressions. By default the value of that option is unset and integral-type
arithmetic operations and conversions are executed in an uncheck ed context.    Console.WriteLine(e.Message);  // output: Arithmetic operation resulted  
in an overflow.  
} 
Operations affected by the overflow-checking
context
７ Note
When you convert a decimal value to an integral type and the result is
outside the range of the destination type, an OverflowEx ception  is always
thrown, regardless of the overflow-checking context.
Default overflow-checking contextConstant expressions are evaluated by default in a checked context and a compile-time
error occurs in the case of overflow. Y ou can explicitly specify an unchecked context for
a constant expression with the unchecked statement or operator.
For more information, see the following sections of the C# language specification :
The checked and unchecked statements
The checked and unchecked operators
User-defined checked and unchecked operators - C# 11
C# reference
CheckForOv erflowUnder flow compiler optionC# language specification
See alsofixed statemen t - pin a variable for
pointer operations
Article •04/10/2023
The fixed statement prevents the garbage collector  from relocating a moveable
variable and declares a pointer to that variable. The address of a fixed, or pinned,
variable doesn't change during execution of the statement. Y ou can use the declared
pointer only inside the corresponding fixed statement. The declared pointer is readonly
and can't be modified:
C#
You can initialize the declared pointer as follows:
With an array, as the example at the beginning of this article shows. The initialized
pointer contains the address of the first array element.
With an address of a variable. Use the address-of & operator , as the following
example shows:
C#unsafe 
{ 
    byte[] bytes = { 1, 2, 3 }; 
    fixed (byte* pointerToFirst = bytes)  
    { 
        Console.WriteLine( $"The address of the first array element:  
{(long)pointerToFirst:X} ."); 
        Console.WriteLine( $"The value of the first array element:  
{*pointerToFirst} ."); 
    } 
} 
// Output is similar to:  
// The address of the first array element: 2173F80B5C8.  
// The value of the first array element: 1.  
７ Note
You can use the fixed statement only in an unsafe  context. The code that contains
unsafe blocks must be compiled with the AllowUnsafeBlocks  compiler option.Object fields are another example of moveable variables that can be pinned.
When the initialized pointer contains the address of an object field or an array
element, the fixed statement guarantees that the garbage collector doesn't
relocate or dispose of the containing object instance during the execution of the
statement body.
With the instance of the type that implements a method named
GetPinnableReference. That method must return a ref variable of an unmanaged
type. The .NET types System.Span<T>  and System.R eadOnlySpan<T>  make use of
this pattern. Y ou can pin span instances, as the following example shows:
C#
For more information, see the Span<T>.GetPinnableR eference()  API reference.
With a string, as the following example shows:
C#unsafe 
{ 
    int[] numbers = { 10, 20, 30 }; 
    fixed (int* toFirst = &numbers[ 0], toLast = &numbers[^ 1]) 
    { 
        Console.WriteLine(toLast - toFirst);  // output: 2  
    } 
} 
unsafe 
{ 
    int[] numbers = { 10, 20, 30, 40, 50 }; 
    Span< int> interior = numbers.AsSpan()[ 1..^1]; 
    fixed (int* p = interior)  
    { 
        for (int i = 0; i < interior.Length; i++)  
        {  
            Console.Write(p[i]);   
        }  
        // output: 203040  
    } 
} 
unsafe 
{ 
    var message = "Hello!" ; 
    fixed (char* p = message)  
    { With a fixed-size buffer .
You can allocate memory on the stack, where it's not subject to garbage collection and
therefore doesn't need to be pinned. T o do that, use a stackalloc  expression .
You can also use the fixed keyword to declare a fixed-size buffer .
For more information, see the following sections of the C# language specification :
The fixed statement
Fixed and moveable variables
C# reference
Unsafe code, pointer types, and function pointers
Pointer-related operators
unsafe        Console.WriteLine(*p);  // output: H  
    } 
} 
C# language specification
See alsolock statemen t - ensure exclusive access
to a shared resource
Article •04/28/2023
The lock statement acquires the mutual-exclusion lock for a given object, executes a
statement block, and then releases the lock. While a lock is held, the thread that holds
the lock can again acquire and release the lock. Any other thread is blocked from
acquiring the lock and waits until the lock is released. The lock statement ensures that
at maximum only one thread executes its body at any time moment.
The lock statement is of the form
C#
where x is an expression of a reference type . It's precisely equivalent to
C#
Since the code uses a try-finally  statement , the lock is released even if an exception is
thrown within the body of a lock statement.
You can't use the await  expression  in the body of a lock statement.lock (x) 
{ 
    // Your code...  
} 
object __lockObj = x;  
bool __lockWasTaken = false; 
try 
{ 
    System.Threading.Monitor.Enter(__lockObj, ref __lockWasTaken);  
    // Your code...  
} 
finally 
{ 
    if (__lockWasTaken) System.Threading.Monitor.Exit(__lockObj);  
} 
GuidelinesWhen you synchronize thread access to a shared resource, lock on a dedicated object
instance (for example, private readonly object balanceLock = new object();) or
another instance that is unlikely to be used as a lock object by unrelated parts of the
code. A void using the same lock object instance for different shared resources, as it
might result in deadlock or lock contention. In particular, avoid using the following
instances as lock objects:
this, as it might be used by the callers as a lock.
Type instances, as they might be obtained by the typeof  operator or reflection.
string instances, including string literals, as they might be interned .
Hold a lock for as short time as possible to reduce lock contention.
The following example defines an Account class that synchronizes access to its private
balance field by locking on a dedicated balanceLock instance. Using the same instance
for locking ensures that the balance field can't be updated simultaneously by two
threads attempting to call the Debit or Credit methods simultaneously.
C#Example
using System;  
using System.Threading.Tasks;  
public class Account 
{ 
    private readonly  object balanceLock = new object(); 
    private decimal balance;  
    public Account(decimal initialBalance ) => balance = initialBalance;  
    public decimal Debit(decimal amount) 
    { 
        if (amount < 0)
        {  
            throw new ArgumentOutOfRangeException( nameof(amount), "The debit  
amount cannot be negative." ); 
        }  
        decimal appliedAmount = 0; 
        lock (balanceLock)  
        {  
            if (balance >= amount)  
            {  
                balance -= amount;  
                appliedAmount = amount;  
            }          }  
        return appliedAmount;  
    } 
    public void Credit(decimal amount) 
    { 
        if (amount < 0)
        {  
            throw new ArgumentOutOfRangeException( nameof(amount), "The 
credit amount cannot be negative." ); 
        }  
        lock (balanceLock)  
        {  
            balance += amount;  
        }  
    } 
    public decimal GetBalance () 
    { 
        lock (balanceLock)  
        {  
            return balance;  
        }  
    } 
} 
class AccountTest  
{ 
    static async Task Main() 
    { 
        var account = new Account( 1000); 
        var tasks = new Task[100]; 
        for (int i = 0; i < tasks.Length; i++)  
        {  
            tasks[i] = Task.Run(() => Update(account));  
        }  
        await Task.WhenAll(tasks);  
        Console.WriteLine( $"Account's balance is {account.GetBalance()} "); 
        // Output:  
        // Account's balance is 2000  
    } 
    static void Update(Account account ) 
    { 
        decimal[] amounts = { 0, 2, -3, 6, -2, -1, 8, -5, 11, -6 }; 
        foreach (var amount in amounts)  
        {  
            if (amount >= 0) 
            {  
                account.Credit(amount);  
            }  
            else 
            {  
                account.Debit(Math.Abs(amount));  For more information, see The lock statement  section of the C# language specification .
C# reference
System.Threading.Monitor
System.Threading.SpinLock
System.Threading.Interlocked
Overview of synchronization primitives
Introduction to S ystem.Threading.Channels            }  
        }  
    } 
} 
C# language specification
See also
using statemen t - ensure the correct use
of disposable objects
Article •03/14/2023
The using statement ensures the correct use of an IDisposable  instance:
C#
When the control leaves the block of the using statement, an acquired IDisposable
instance is disposed. In particular, the using statement ensures that a disposable
instance is disposed even if an exception occurs within the block of the using
statement. In the preceding example, an opened file is closed after all lines are
processed.
Use the await using statement to correctly use an IAsyncDisposable  instance:
C#
For more information about using of IAsyncDisposable  instances, see the Using async
disposable  section of the Implement a DisposeAsync method  article.
You can also use a using declar ation  that doesn't require braces:
C#var numbers = new List<int>();
using (StreamReader reader = File.OpenText( "numbers.txt" ))
{
    string line;
    while ((line = reader.ReadLine()) is not null)
    {
        if (int.TryParse(line, out int number))
        {
            numbers.Add(number);
        }
    }
}
await using (var resource = new AsyncDisposableExample())
{
    // Use the resource
}When declared in a using declaration, a local variable is disposed at the end of the
scope in which it's declared. In the preceding example, disposal happens at the end of a
method.
A variable declared by the using statement or declaration is readonly. Y ou cannot
reassign it or pass it as a ref or out parameter.
You can declare several instances of the same type in one using statement, as the
following example shows:
C#
When you declare several instances in one using statement, they are disposed in
reverse order of declaration.
You can also use the using statement and declaration with an instance of a ref struct
that fits the disposable pattern. That is, it has an instance Dispose method, which is
accessible, parameterless and has a void return type.
The using statement can also be of the following form:
C#static IEnumerable< int> LoadNumbers (string filePath )
{
    using StreamReader reader = File.OpenText(filePath);
    
    var numbers = new List<int>();
    string line;
    while ((line = reader.ReadLine()) is not null)
    {
        if (int.TryParse(line, out int number))
        {
            numbers.Add(number);
        }
    }
    return numbers;
}
using (StreamReader numbersFile = File.OpenText( "numbers.txt" ), wordsFile =  
File.OpenText( "words.txt" ))
{
    // Process both files
}
using (expression)
{where expression produces a disposable instance. The following example demonstrates
that:
C#
For more information, see The using statement  section of the C# language specification
and the proposal note about "pattern-based using" and "using declarations" .
C# reference
System.IDisposable
System.IAsyncDisposable
Using objects that implement IDisposable
Implement a Dispose method
Implement a DisposeAsync method
Use simple 'using' statement (style rule IDE0063)
using  directive    // ...
}
StreamReader reader = File.OpenText(filePath);
using (reader)
{
    // Process file content
}
２ Warning
In the preceding example, after control leaves the using statement, a disposable
instance remains in scope while it's already disposed. If you use that instance
further, you might encounter an exception, for example, ObjectDisposedEx ception .
That's why we recommend declaring a disposable variable within the using
statement or with the using declaration.
C# language specification
See also６ Collaborat e with us on
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
 Provide product feedbackyield statemen t - provide the next
elemen t
Article •04/28/2023
You use the yield statement in an iterator  to provide the next value or signal the end of
an iteration. The yield statement has the two following forms:
yield return: to provide the next value in iteration, as the following example
shows:
C#
yield break: to explicitly signal the end of iteration, as the following example
shows:
C#foreach (int i in ProduceEvenNumbers (9))
{
    Console.Write(i);
    Console.Write( " ");
}
// Output: 0 2 4 6 8
IEnumerable< int> ProduceEvenNumbers (int upto)
{
    for (int i = 0; i <= upto; i += 2)
    {
        yield return i;
    }
}
Console.WriteLine( string.Join(" ", TakeWhilePositive( new[] { 2, 3, 4, 
5, -1, 3, 4})));
// Output: 2 3 4 5
Console.WriteLine( string.Join(" ", TakeWhilePositive( new[] { 9, 8, 7 
})));
// Output: 9 8 7
IEnumerable< int> TakeWhilePositive (IEnumerable< int> numbers )
{
    foreach (int n in numbers)
    {
        if (n > 0)
        {
            yield return n;Iteration also finishes when control reaches the end of an iterator.
In the preceding examples, the return type of iterators is IEnumerable<T>  (in non-
generic cases, use IEnumerable  as the return type of an iterator). Y ou can also use
IAsyncEnumerable<T>  as the return type of an iterator. That makes an iterator async.
Use the await foreach  statement  to iterate over iterator's result, as the following
example shows:
C#
IEnumerator<T>  or IEnumerator  can also be the return type of an iterator. That is useful
when you implement the GetEnumerator method in the following scenarios:
You design the type that implements IEnumerable<T>  or IEnumerable  interface.
You add an instance or extension  GetEnumerator method to enable iteration over
the type's instance with the foreach  statement , as the following example shows:
C#        }
        else
        {
            yield break;
        }
    }
}
await foreach (int n in GenerateNumbersAsync (5))
{
    Console.Write(n);
    Console.Write( " ");
}
// Output: 0 2 4 6 8
async IAsyncEnumerable< int> GenerateNumbersAsync (int count)
{
    for (int i = 0; i < count; i++)
    {
        yield return await ProduceNumberAsync (i);
    }
}
async Task<int> ProduceNumberAsync (int seed)
{
    await Task.Delay( 1000);
    return 2 * seed;
}You can't use the yield statements in:
methods with in, ref, or out parameters
lambda expressions  and anonymous methods
methods that contain unsafe blocks
The call of an iterator doesn't execute it immediately, as the following example shows:
C#public static void Example()
{
    var point = new Point(1, 2, 3);
    foreach (int coordinate in point)
    {
        Console.Write(coordinate);
        Console.Write( " ");
    }
    // Output: 1 2 3
}
public readonly  record struct Point(int X, int Y, int Z)
{
    public IEnumerator< int> GetEnumerator ()
    {
        yield return X;
        yield return Y;
        yield return Z;
    }
}
Execution of an iterator
var numbers = ProduceEvenNumbers( 5);
Console.WriteLine( "Caller: about to iterate." );
foreach (int i in numbers)
{
    Console.WriteLine( $"Caller: {i}");
}
IEnumerable< int> ProduceEvenNumbers (int upto)
{
    Console.WriteLine( "Iterator: start." );
    for (int i = 0; i <= upto; i += 2)
    {
        Console.WriteLine( $"Iterator: about to yield {i}");
        yield return i;
        Console.WriteLine( $"Iterator: yielded {i}");
    }As the preceding example shows, when you start to iterate over an iterator's result, an
iterator is executed until the first yield return statement is reached. Then, the
execution of an iterator is suspended and the caller gets the first iteration value and
processes it. On each subsequent iteration, the execution of an iterator resumes after
the yield return statement that caused the previous suspension and continues until
the next yield return statement is reached. The iteration completes when control
reaches the end of an iterator or a yield break statement.
For more information, see The yield statement  section of the C# language specification .
C# reference
Iterators
Iterate through collections in C#
foreach
await foreach    Console.WriteLine( "Iterator: end." );
}
// Output:
// Caller: about to iterate.
// Iterator: start.
// Iterator: about to yield 0
// Caller: 0
// Iterator: yielded 0
// Iterator: about to yield 2
// Caller: 2
// Iterator: yielded 2
// Iterator: about to yield 4
// Caller: 4
// Iterator: yielded 4
// Iterator: end.
C# language specification
See also
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For.NET feedb ack
The .NET documentation is open
source. Provide feedback here.
 Open a documentation issuemore information, see our
contributor guide . Provide product feedbackC# Special Characters
Article •10/27/2021
Special characters are predefined, contextual characters that modify the program
element (a literal string, an identifier, or an attribute name) to which they are prepended.
C# supports the following special characters:
@, the verbatim identifier character.
$, the interpolated string character.
This section only includes those tokens that are not operators. See the operators  section
for all operators.
C# Reference
C# Programming GuideSee alsoCode commen ts - // and /*. */
Article •12/13/2022
C# supports two different forms of comments. Single line comments start with // and
end at the end of that line of code. Multiline comments start with /* and end with */.
The following code shows an example of each:
C#
The multi-line comment can also be used to insert text in a line of code. Because these
comments have an explicit closing character, you can include more executable code
after the comment:
C#
The single line comment can appear after executable code on the same line. The
comment ends at the end of the text line:
C#
Some comments start with three slashes: ///. Triple-slash c omments  are XML
document ation c omments . The compiler reads these to produce human documentation.
You can read more about XML doc comments  in the section on triple-slash comments.// This is a single line comment.
/* This could be a summary of all the  
   code that's in this class.  
   You might add multiple paragraphs, or links to pages  
   like https://learn.microsoft.com/dotnet/csharp.  
    
   You could even include emojis. This example is 🔥 
   Then, when you're done, close with  
   */ 
public static int Add(int left, int right) 
{ 
    return left /* first operand */  + right /* second operand */ ; 
} 
return source++; // increment the source.  String interpolation using $
Article •08/29/2023
The $ character identifies a string literal as an interpolat ed str ing. An interpolated string
is a string literal that might contain interpolation expr essions . When an interpolated
string is resolved to a result string, items with interpolation expressions are replaced by
the string representations of the expression results.
String interpolation provides a more readable, convenient syntax to format strings. It's
easier to read than string composite formatting . The following example uses both
features to produce the same output:
C#
Beginning with C# 10, you can use an interpolated string to initialize a constant  string.
You can do that only if all interpolation expressions within the interpolated string are
constant strings as well.
To identify a string literal as an interpolated string, prepend it with the $ symbol. Y ou
can't have any white space between the $ and the " that starts a string literal.
The structure of an item with an interpolation expression is as follows:
C#
Elements in square brackets are optional. The following table describes each element:var name = "Mark";
var date = DateTime.Now;
// Composite formatting:
Console.WriteLine( "Hello, {0}! Today is {1}, it's {2:HH:mm} now." , name, 
date.DayOfWeek, date);
// String interpolation:
Console.WriteLine( $"Hello, {name}! Today is {date.DayOfWeek} , it's 
{date:HH:mm}  now.");
// Both calls produce the same output that is similar to:
// Hello, Mark! Today is Wednesday, it's 19:40 now.
Structure of an interpolated string
{<interpolationExpression>[,<alignment>][:<formatString>]}Element Descr iption
interpolationExpressionThe expression that produces a result to be formatted. S tring
representation of null is String.Empty .
alignment The constant expression whose value defines the minimum number of
characters in the string representation of the expression result. If
positive, the string representation is right-aligned; if negative, it's left-
aligned. For more information, see the Alignment component  section
of the Composite formatting  article.
formatString A format string that is supported by the type of the expression result.
For more information, see the Format string component  section of the
Composite formatting  article.
The following example uses optional formatting components described above:
C#
Beginning with C# 11, you can use new-lines within an interpolation expression to make
the expression's code more readable. The following example shows how new-lines can
improve the readability of an expression involving pattern matching :
C#Console.WriteLine( $"|{"Left",-7}|{"Right",7}|");
const int FieldWidthRightAligned = 20;
Console.WriteLine( $"{Math.PI,FieldWidthRightAligned}  - default formatting of  
the pi number" );
Console.WriteLine( $"{Math.PI,FieldWidthRightAligned:F3}  - display only three  
decimal digits of the pi number" );
// Output is:
// |Left   |  Right|
//     3.14159265358979 - default formatting of the pi number
//                3.142 - display only three decimal digits of the pi number
string message = $"The usage policy for {safetyScore}  is {
    safetyScore switch
    {
        > 90 => "Unlimited usage" ,
        > 80 => "General usage, with daily safety check" ,
        > 70 => "Issues must be addressed within 1 week" ,
        > 50 => "Issues must be addressed within 1 day" ,
        _ => "Issues must be addressed before continued use" ,
    }
    }";Beginning with C# 11, you can use an interpolated raw string literal , as the following
example shows:
C#
To embed { and } characters in the result string, start an interpolated raw string literal
with multiple $ characters. When you do that, any sequence of { or } characters
shorter than the number of $ characters is embedded in the result string. T o enclose
any interpolation expression within that string, you need to use the same number of
braces as the number of $ characters, as the following example shows:
C#
In the preceding example, an interpolated raw string literal starts with two $ characters.
That's why you need to put every interpolation expression between double braces, {{
and }}. A single brace is embedded into a result string. If you need to embed repeated
{ or } characters into a result string, use an appropriately greater number of $
characters to designate an interpolated raw string literal.
To include a brace, "{" or "}", in the text produced by an interpolated string, use two
braces, "{{" or "}}". For more information, see the Escaping braces  section of theInterpolated raw string literals
int X = 2;
int Y = 3;
var pointMessage = $"""The point " {X}, {Y} " is {Math.Sqrt(X * X + Y * Y):F3}  
from the origin" "";
Console.WriteLine(pointMessage);
// Output is:
// The point "2, 3" is 3.606 from the origin
int X = 2;
int Y = 3;
var pointMessage = $ $"""{The point {{{X}}, {{Y}}} is {{Math.Sqrt(X * X + Y *  
Y):F3}} from the origin}" "";
Console.WriteLine(pointMessage);
// Output is:
// {The point {2, 3} is 3.606 from the origin}
Special charactersComposite formatting  article.
As the colon (":") has special meaning in an interpolation expression item, to use a
conditional operator  in an interpolation expression, enclose that expression in
parentheses.
The following example shows how to include a brace in a result string. It also shows how
to use a conditional operator:
C#
An interpolated verbatim  string starts with the both $ and @ characters. Y ou can use $
and @ in any order: both $@"..." and @$"..." are valid interpolated verbatim strings.
For more information about verbatim strings, see the string  and verbatim identifier
articles.
By default, an interpolated string uses the current culture defined by the
CultureInfo.CurrentCulture  property for all formatting operations.
To resolve an interpolated string to a culture-specific result string, use the
String.Create(IFormatProvider, DefaultInterpolatedS tringHandler)  method, which is
available beginning with .NET 6. The following example shows how to do that:
C#string name = "Horace" ;
int age = 34;
Console.WriteLine( $"He asked, \"Is your name {name}?\", but didn't wait for  
a reply :-{{" );
Console.WriteLine( $"{name} is {age} year{(age == 1 ? "" : "s")} old.");
// Output is:
// He asked, "Is your name Horace?", but didn't wait for a reply :-{
// Horace is 34 years old.
Cultur e-specific formatting
double speedOfLight = 299792.458 ;
System.Globalization.CultureInfo.CurrentCulture =  
System.Globalization.CultureInfo.GetCultureInfo( "nl-NL");
string messageInCurrentCulture = $"The speed of light is {speedOfLight:N3}  
km/s.";
var specificCulture = System.Globalization.CultureInfo.GetCultureInfo( "en-
IN");
string messageInSpecificCulture = string.Create(
    specificCulture, $"The speed of light is {speedOfLight:N3}  km/s.");In .NET 5 and earlier versions of .NET, use implicit conversion of an interpolated string to
a FormattableS tring  instance. Then, you can use an instance
FormattableS tring.T oString(IFormatProvider)  method or a static
FormattableS tring.Invariant  method to produce a culture-specific result string. The
following example shows how to do that:
C#
For more information about custom formatting, see the Custom formatting with
ICustomFormatter  section of the Formatting types in .NET  article.
If you're new to string interpolation, see the String interpolation in C#  interactive
tutorial. Y ou can also check another String interpolation in C#  tutorial. That tutorial
demonstrates how to use interpolated strings to produce formatted strings.string messageInInvariantCulture = string.Create(
    System.Globalization.CultureInfo.InvariantCulture, $"The speed of light  
is {speedOfLight:N3}  km/s.");
Console.WriteLine( $"{System.Globalization.CultureInfo.CurrentCulture, -10} 
{messageInCurrentCulture} ");
Console.WriteLine( $"{specificCulture, -10} {messageInSpecificCulture} ");
Console.WriteLine( $"{"Invariant" ,-10} {messageInInvariantCulture} ");
// Output is:
// nl-NL      The speed of light is 299.792,458 km/s.
// en-IN      The speed of light is 2,99,792.458 km/s.
// Invariant  The speed of light is 299,792.458 km/s.
double speedOfLight = 299792.458 ;
FormattableString message = $"The speed of light is {speedOfLight:N3}  
km/s.";
var specificCulture = System.Globalization.CultureInfo.GetCultureInfo( "en-
IN");
string messageInSpecificCulture = message.ToString(specificCulture);
Console.WriteLine(messageInSpecificCulture);
// Output:
// The speed of light is 2,99,792.458 km/s.
string messageInInvariantCulture = FormattableString.Invariant(message);
Console.WriteLine(messageInInvariantCulture);
// Output is:
// The speed of light is 299,792.458 km/s.
Other resourcesBeginning with C# 10 and .NET 6, the compiler checks if an interpolated string is
assigned to a type that satisfies the interpolat ed str ing handler p attern. An interpolat ed
string handler  is a type that converts the interpolated string into a result string. When an
interpolated string has the type string, it's processed by the
System.Runtime.CompilerServices.DefaultInterpolatedS tringHandler . For the example of
a custom interpolated string handler, see the Write a custom string interpolation
handler  tutorial. Use of an interpolated string handler is an advanced scenario, typically
required for performance reasons.
Prior to C# 10, if an interpolated string has the type string, it's typically transformed
into a String.Format  method call. The compiler may replace String.Format  with
String.Concat  if the analyzed behavior would be equivalent to concatenation.
If an interpolated string has the type IFormattable  or FormattableS tring , the compiler
generates a call to the FormattableS tringF actory.Create  method.
For more information, see the Interpolated string expressions  section of the C#
language specification  and the following new feature specifications:
C# 10 - Improved interpolated strings
C# 11 - Raw string literals
C# 11 - New-lines in string interpolations
C# reference
C# special characters
Strings
Standard numeric format stringsCompilation of interpolated strings
７ Note
One side effect of interpolated string handlers is that a custom handler, including
System.Runtime.CompilerSer vices.DefaultInt erpolat edStringHandler , may not
evaluate all the interpolation expressions within the interpolated string under all
conditions. That means side effects of those expressions may not occur.
C# language specification
See alsoComposite formatting
String.Format
Simplify interpolation (style rule IDE0071)
String interpolation in C# 10 and .NET 6 (.NET blog)
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
 Provide product feedbackVerbatim text - @ in variables,
attributes, and string literals
Article •03/22/2023
The @ special character serves as a verbatim identifier. Y ou use it in the following ways:
1. To indicate that a string literal is to be interpreted verbatim. The @ character in this
instance defines a verbatim str ing lit eral. Simple escape sequences (such as "\\"
for a backslash), hexadecimal escape sequences (such as "\x0041" for an
uppercase A), and Unicode escape sequences (such as "\u0041" for an uppercase
A) are interpreted literally. Only a quote escape sequence ( "") isn't interpreted
literally; it produces one double quotation mark. Additionally, in case of a verbatim
interpolated string  brace escape sequences ( {{ and }}) aren't interpreted literally;
they produce single brace characters. The following example defines two identical
file paths, one by using a regular string literal and the other by using a verbatim
string literal. This is one of the more common uses of verbatim string literals.
C#
The following example illustrates the effect of defining a regular string literal and a
verbatim string literal that contain identical character sequences.
C#string filename1 = @"c:\documents\files\u0066.txt" ; 
string filename2 = "c:\\documents\\files\\u0066.txt" ; 
Console.WriteLine(filename1);  
Console.WriteLine(filename2);  
// The example displays the following output:  
//     c:\documents\files\u0066.txt  
//     c:\documents\files\u0066.txt  
string s1 = "He said, \"This is the last \u0063hance\x0021\"" ; 
string s2 = @"He said, ""This is the last \u0063hance\x0021""" ; 
Console.WriteLine(s1);  
Console.WriteLine(s2);  
// The example displays the following output:  
//     He said, "This is the last chance!"  
//     He said, "This is the last \u0063hance\x0021"  2. To use C# keywords as identifiers. The @ character prefixes a code element that the
compiler is to interpret as an identifier rather than a C# keyword. The following
example uses the @ character to define an identifier named for that it uses in a
for loop.
C#
3. To enable the compiler to distinguish between attributes in cases of a naming
conflict. An attribute is a class that derives from Attribute . Its type name typically
includes the suffix Attribut e, although the compiler doesn't enforce this
convention. The attribute can then be referenced in code either by its full type
name (for example, [InfoAttribute] or its shortened name (for example, [Info]).
However, a naming conflict occurs if two shortened attribute type names are
identical, and one type name includes the Attribut e suffix but the other doesn't.
For example, the following code fails to compile because the compiler can't
determine whether the Info or InfoAttribute attribute is applied to the Example
class. For more information, see CS1614 .
C#string[] @for = { "John", "James", "Joan", "Jamie" }; 
for (int ctr = 0; ctr < @ for.Length; ctr++)  
{ 
   Console.WriteLine( $"Here is your gift, {@for[ctr]}!"); 
} 
// The example displays the following output:  
//     Here is your gift, John!  
//     Here is your gift, James!  
//     Here is your gift, Joan!  
//     Here is your gift, Jamie!  
using System;  
[AttributeUsage(AttributeTargets.Class) ] 
public class Info : Attribute  
{ 
   private string information;  
   public Info(string info) 
   { 
      information = info;  
   } 
} 
[AttributeUsage(AttributeTargets.Method) ] 
public class InfoAttribute  : Attribute  
{ 
   private string information;  C# Reference
C# Programming Guide
C# Special Characters   public InfoAttribute (string info) 
   { 
      information = info;  
   } 
} 
[Info("A simple executable." )] // Generates compiler error CS1614.  
Ambiguous Info and InfoAttribute.
// Prepend '@' to select 'Info' ([@Info("A simple executable.")]).  
Specify the full name 'InfoAttribute' to select it.  
public class Example 
{ 
   [InfoAttribute( "The entry point." )] 
   public static void Main() 
   { 
   } 
} 
See alsoRaw string literal text - """ in string
literals
Article •08/29/2023
A raw string literal starts and ends with a minimum of three double quote ( ")
characters:
C#
Raw string literals can span multiple lines:
C#
The following rules govern the interpretation of a multi-line raw string literal:
Both opening and closing quote characters must be on their own line.
Any whitespace to the left of the closing quotes is removed from all lines of the
raw string literal.
Whitespace following the opening quote on the same line is ignored.
Whitespace only lines following the opening quote are included in the string literal.
You may need to create a raw string literal that has three or more consecutive double-
quote characters. Raw string literals can start and end with a sequence of at least three
double-quote characters. When your string literal contains three consecutive double-
quotes, you start and end the raw string literal with four double quote characters:
C#var singleLine = """This is a " raw string literal ". It can contain  
characters like \, ' and " .""";
var xml = """
        <element attr=" content">
            <body>
            </body>
        </element>
        """;
var moreQuotes = """" As you can see, """Raw string literals" "" can start and 
end with more than three double-quotes when needed. """";If you need to start or end a raw string literal with quote characters, use the multi-line
format:
C#
Raw string literals can also be combined with interpolated strings  to embed the { and
} characters in the output string. Y ou use multiple $ characters in an interpolated raw
string literal to embed { and } characters in the output string without escaping them.
Raw string literals were introduced in C# 11.
C# reference
C# special characters
C# string interpolation
Raw string literals feature specificationvar MultiLineQuotes = """"
               """Raw string literals" "" can start and end with more than  
three double-quotes when needed.
               """";
See alsoAssembly level attributes interpreted by
the C# compiler
Article •12/18/2021
Most attributes are applied to specific language elements such as classes or methods;
however, some attributes are global—they apply to an entire assembly or module. For
example, the AssemblyV ersionAttribute  attribute can be used to embed version
information into an assembly, like this:
C#
Global attributes appear in the source code after any top level using directives and
before any type, module, or namespace declarations. Global attributes can appear in
multiple source files, but the files must be compiled in a single compilation pass. Visual
Studio adds global attributes to the AssemblyInfo.cs file in .NET Framework projects.
These attributes aren't added to .NET Core projects.
Assembly attributes are values that provide information about an assembly. They fall
into the following categories:
Assembly identity attributes
Informational attributes
Assembly manifest attributes
Three attributes (with a strong name, if applicable) determine the identity of an
assembly: name, version, and culture. These attributes form the full name of the
assembly and are required when you reference it in code. Y ou can set an assembly's
version and culture using attributes. However, the name value is set by the compiler, the
Visual S tudio IDE in the Assembly Information Dialog Box , or the Assembly Linker
(Al.exe) when the assembly is created. The assembly name is based on the assembly
manifest. The AssemblyFlagsAttribute  attribute specifies whether multiple copies of the
assembly can coexist.
The following table shows the identity attributes.
Attribute Purpose[assembly: AssemblyVersion( "1.0.0.0" )] 
Assembly identity  attributesAttribute Purpose
AssemblyV ersionAttribute Specifies the version of an assembly.
AssemblyCultureAttribute Specifies which culture the assembly supports.
AssemblyFlagsAttribute Specifies whether an assembly supports side-by-side execution on
the same computer, in the same process, or in the same application
domain.
You use informational attributes to provide additional company or product information
for an assembly. The following table shows the informational attributes defined in the
System.R eflection  namespace.
Attribute Purpose
AssemblyProductAttribute Specifies a product name for an assembly manifest.
AssemblyT rademarkAttribute Specifies a trademark for an assembly manifest.
AssemblyInformationalV ersionAttribute Specifies an informational version for an assembly
manifest.
AssemblyCompanyAttribute Specifies a company name for an assembly manifest.
AssemblyCopyrightAttribute Defines a custom attribute that specifies a copyright for
an assembly manifest.
AssemblyFileV ersionAttribute Sets a specific version number for the Win32 file version
resource.
CLSCompliantAttribute Indicates whether the assembly is compliant with the
Common Language Specification (CLS).
You can use assembly manifest attributes to provide information in the assembly
manifest. The attributes include title, description, default alias, and configuration. The
following table shows the assembly manifest attributes defined in the System.R eflection
namespace.
Attribute Purpose
AssemblyTitleAttribute Specifies an assembly title for an assembly manifest.Informational attributes
Assembly manifest attributesAttribute Purpose
AssemblyDescriptionAttribute Specifies an assembly description for an assembly manifest.
AssemblyConfigurationAttribute Specifies an assembly configuration (such as retail or debug)
for an assembly manifest.
AssemblyDefaultAliasAttribute Defines a friendly default alias for an assembly manifestDetermine caller information using
attributes interpreted by the C#
compiler
Article •06/15/2022
Using info attributes, you obtain information about the caller to a method. Y ou obtain
the file path of the source code, the line number in the source code, and the member
name of the caller. T o obtain member caller information, you use attributes that are
applied to optional parameters. Each optional parameter specifies a default value. The
following table lists the Caller Info attributes that are defined in the
System.Runtime.CompilerServices  namespace:
Attribute Descr iption Type
CallerFileP athAttribute Full path of the source file that contains the
caller. The full path is the path at compile time.String
CallerLineNumberAttribute Line number in the source file from which the
method is called.Integer
CallerMemberNameAttribute Method name or property name of the caller. String
CallerArgumentExpressionAttribute String representation of the argument
expression.String
This information helps you with tracing and debugging, and helps you to create
diagnostic tools. The following example shows how to use caller info attributes. On each
call to the TraceMessage method, the caller information is inserted for the arguments to
the optional parameters.
C#
public void DoProcessing () 
{ 
    TraceMessage( "Something happened." ); 
} 
public void TraceMessage (string message,  
        [CallerMemberName] string memberName = "", 
        [CallerFilePath] string sourceFilePath = "", 
        [CallerLineNumber] int sourceLineNumber = 0) 
{ 
    Trace.WriteLine( "message: "  + message);  
    Trace.WriteLine( "member name: "  + memberName);  
    Trace.WriteLine( "source file path: "  + sourceFilePath);  You specify an explicit default value for each optional parameter. Y ou can't apply caller
info attributes to parameters that aren't specified as optional. The caller info attributes
don't make a parameter optional. Instead, they affect the default value that's passed in
when the argument is omitted. Caller info values are emitted as literals into the
Intermediate Language (IL) at compile time. Unlike the results of the StackT race property
for exceptions, the results aren't affected by obfuscation. Y ou can explicitly supply the
optional arguments to control the caller information or to hide caller information.
You can use the CallerMemberName attribute to avoid specifying the member name as a
String argument to the called method. By using this technique, you avoid the problem
that Rename R efact oring  doesn't change the String values. This benefit is especially
useful for the following tasks:
Using tracing and diagnostic routines.
Implementing the INotifyPropertyChanged  interface when binding data. This
interface allows the property of an object to notify a bound control that the
property has changed. The control can display the updated information. Without
the CallerMemberName attribute, you must specify the property name as a literal.
The following chart shows the member names that are returned when you use the
CallerMemberName attribute.
Calls occur within Member name r esult
Method, property, or
eventThe name of the method, property, or event from which the call
originated.
Constructor The string ".ctor"
Static constructor The string ".cctor"
Finalizer The string "Finalize"    Trace.WriteLine( "source line number: "  + sourceLineNumber);  
} 
// Sample Output:  
//  message: Something happened.  
//  member name: DoProcessing  
//  source file path: c:\Visual Studio  
Projects\CallerInfoCS\CallerInfoCS\Form1.cs  
//  source line number: 31  
Member namesCalls occur within Member name r esult
User-defined operators
or conversionsThe generated name for the member, for example, "op_Addition".
Attribute constructor The name of the method or property to which the attribute is applied.
If the attribute is any element within a member (such as a parameter, a
return value, or a generic type parameter), this result is the name of the
member that's associated with that element.
No containing member
(for example, assembly-
level or attributes that
are applied to types)The default value of the optional parameter.
You use the System.Runtime.CompilerServices.CallerArgumentExpressionAttribute  when
you want the expression passed as an argument. Diagnostic libraries may want to
provide more details about the expressions  passed to arguments. By providing the
expression that triggered the diagnostic, in addition to the parameter name, developers
have more details about the condition that triggered the diagnostic. That extra
information makes it easier to fix.
The following example shows how you can provide detailed information about the
argument when it's invalid:
C#
You would invoke it as shown in the following example:
C#Argument expressions
public static void ValidateArgument (string parameterName, bool condition,  
[CallerArgumentExpression( "condition" )] string? message =null) 
{ 
    if (!condition)  
    { 
        throw new ArgumentException( $"Argument failed validation:  
<{message} >", parameterName);  
    } 
} 
public void Operation (Action func ) 
{ 
    Utilities.ValidateArgument( nameof(func), func is not null); The expression used for condition is injected by the compiler into the message
argument. When a developer calls Operation with a null argument, the following
message is stored in the ArgumentException:
.NET CLI
This attribute enables you to write diagnostic utilities that provide more details.
Developers can more quickly understand what changes are needed. Y ou can also use the
CallerArgumentExpressionAttribute  to determine what expression was used as the
receiver for extension methods. The following method samples a sequence at regular
intervals. If the sequence has fewer elements than the frequency, it reports an error:
C#
The previous example uses the nameof  operator for the parameter sequence. That
feature is available in C# 11. Before C# 11, you'll need to type the name of the
parameter as a string. Y ou could call this method as follows:
C#
The preceding example would throw an ArgumentException  whose message is the
following text:    func();  
} 
Argument failed validation: <func is not null>  
public static IEnumerable<T> Sample<T>( this IEnumerable<T> sequence, int 
frequency,  
    [CallerArgumentExpression(nameof(sequence)) ] string? message = null) 
{ 
    if (sequence.Count() < frequency)  
        throw new ArgumentException( $"Expression doesn't have enough  
elements: {message} ", nameof(sequence));  
    int i = 0; 
    foreach (T item in sequence)  
    { 
        if (i++ % frequency == 0) 
            yield return item; 
    } 
} 
sample = Enumerable.Range( 0, 10).Sample( 100); .NET CLI
Named and Optional Arguments
System.R eflection
Attribute
AttributesExpression doesn 't have enough elements: Enumerable.Range(0, 10) (Parameter  
'sequence ') 
See alsoAttributes for null-state static analysis
interpreted by the C# compiler
Article •05/05/2023
In a nullable enabled context, the compiler performs static analysis of code to determine
the null-st ate of all reference type variables:
not-null: Static analysis determines that a variable has a non-null value.
maybe-null : Static analysis can't determine that a variable is assigned a non-null
value.
These states enable the compiler to provide warnings when you may dereference a null
value, throwing a System.NullR eferenceException . These attributes provide the compiler
with semantic information about the null-st ate of arguments, return values, and object
members based on the state of arguments and return values. The compiler provides
more accurate warnings when your APIs have been properly annotated with this
semantic information.
This article provides a brief description of each of the nullable reference type attributes
and how to use them.
Let's start with an example. Imagine your library has the following API to retrieve a
resource string. This method was originally compiled in a nullable oblivious  context:
C#
The preceding example follows the familiar Try* pattern in .NET. There are two
reference parameters for this API: the key and the message. This API has the following
rules relating to the null-st ate of these parameters:
Callers shouldn't pass null as the argument for key.
Callers can pass a variable whose value is null as the argument for message.bool TryGetMessage (string key, out string message )
{
    if (_messageMap.ContainsKey(key))
        message = _messageMap[key];
    else
        message = null;
    return message != null;
}If the TryGetMessage method returns true, the value of message isn't null. If the
return value is false, the value of message is null.
The rule for key can be expressed succinctly: key should be a non-nullable reference
type. The message parameter is more complex. It allows a variable that is null as the
argument, but guarantees, on success, that the out argument isn't null. For these
scenarios, you need a richer vocabulary to describe the expectations. The NotNullWhen
attribute, described below describes the null-st ate for the argument used for the
message parameter.
Attribute Categor y Meaning
AllowNull Precondition A non-nullable parameter, field, or property
may be null.
DisallowNull Precondition A nullable parameter, field, or property should
never be null.
MaybeNull Postcondition A non-nullable parameter, field, property, or
return value may be null.
NotNull Postcondition A nullable parameter, field, property, or return
value will never be null.
MaybeNullWhen Conditional
postconditionA non-nullable argument may be null when
the method returns the specified bool value.
NotNullWhen Conditional
postconditionA nullable argument won't be null when the
method returns the specified bool value.
NotNullIfNotNull Conditional
postconditionA return value, property, or argument isn't null
if the argument for the specified parameter
isn't null.
MemberNotNull Method and property
helper methodsThe listed member won't be null when the
method returns.
MemberNotNullWhen Method and property
helper methodsThe listed member won't be null when the
method returns the specified bool value.７ Note
Adding these attributes gives the compiler more information about the rules for
your API. When calling code is compiled in a nullable enabled context, the compiler
will warn callers when they violate those rules. These attributes don't enable more
checks on your implementation.Attribute Categor y Meaning
DoesNotR eturn Unreachable code A method or property never returns. In other
words, it always throws an exception.
DoesNotR eturnIf Unreachable code This method or property never returns if the
associated bool parameter has the specified
value.
The preceding descriptions are a quick reference to what each attribute does. The
following sections describe the behavior and meaning of these attributes more
thoroughly.
Consider a read/write property that never returns null because it has a reasonable
default value. Callers pass null to the set accessor when setting it to that default value.
For example, consider a messaging system that asks for a screen name in a chat room. If
none is provided, the system generates a random name:
C#
When you compile the preceding code in a nullable oblivious context, everything is fine.
Once you enable nullable reference types, the ScreenName property becomes a non-
nullable reference. That's correct for the get accessor: it never returns null. Callers
don't need to check the returned property for null. But now setting the property to
null generates a warning. T o support this type of code, you add the
System.Diagnostics.CodeAnalysis.AllowNullAttribute  attribute to the property, as shown
in the following code:
C#Preconditions: AllowNull and DisallowNull
public string ScreenName
{
    get => _screenName;
    set => _screenName = value ?? GenerateRandomScreenName();
}
private string _screenName;
[AllowNull ]
public string ScreenName
{
    get => _screenName;
    set => _screenName = value ?? GenerateRandomScreenName();You may need to add a using directive for System.Diagnostics.CodeAnalysis  to use this
and other attributes discussed in this article. The attribute is applied to the property, not
the set accessor. The AllowNull attribute specifies pre-conditions , and only applies to
arguments. The get accessor has a return value, but no parameters. Therefore, the
AllowNull attribute only applies to the set accessor.
The preceding example demonstrates what to look for when adding the AllowNull
attribute on an argument:
1. The general contract for that variable is that it shouldn't be null, so you want a
non-nullable reference type.
2. There are scenarios for a caller to pass null as the argument, though they aren't
the most common usage.
Most often you'll need this attribute for properties, or in, out, and ref arguments. The
AllowNull attribute is the best choice when a variable is typically non-null, but you need
to allow null as a precondition.
Contrast that with scenarios for using DisallowNull: You use this attribute to specify
that an argument of a nullable reference type shouldn't be null. Consider a property
where null is the default value, but clients can only set it to a non-null value. Consider
the following code:
C#
The preceding code is the best way to express your design that the ReviewComment could
be null, but can't be set to null. Once this code is nullable aware, you can express this
concept more clearly to callers using the
System.Diagnostics.CodeAnalysis.DisallowNullAttribute :
C#}
private string _screenName = GenerateRandomScreenName();
public string ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new 
ArgumentNullException( nameof(value), "Cannot set to null" );
}
string _comment;In a nullable context, the ReviewComment get accessor could return the default value of
null. The compiler warns that it must be checked before access. Furthermore, it warns
callers that, even though it could be null, callers shouldn't explicitly set it to null. The
DisallowNull attribute also specifies a pre-condition , it doesn't affect the get accessor.
You use the DisallowNull attribute when you observe these characteristics about:
1. The variable could be null in core scenarios, often when first instantiated.
2. The variable shouldn't be explicitly set to null.
These situations are common in code that was originally null oblivious . It may be that
object properties are set in two distinct initialization operations. It may be that some
properties are set only after some asynchronous work has completed.
The AllowNull and DisallowNull attributes enable you to specify that preconditions on
variables may not match the nullable annotations on those variables. These provide
more detail about the characteristics of your API. This additional information helps
callers use your API correctly. R emember you specify preconditions using the following
attributes:
AllowNull : A non-nullable argument may be null.
DisallowNull : A nullable argument should never be null.
Suppose you have a method with the following signature:
C#
You've likely written a method like this to return null when the name sought wasn't
found. The null clearly indicates that the record wasn't found. In this example, you'd[DisallowNull ]
public string? ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new 
ArgumentNullException( nameof(value), "Cannot set to null" );
}
string? _comment;
Postconditions: MaybeNull and NotNull
public Customer FindCustomer (string lastName, string firstName )likely change the return type from Customer to Customer?. Declaring the return value as
a nullable reference type specifies the intent of this API clearly:
C#
For reasons covered under Generics nullability  that technique may not produce the
static analysis that matches your API. Y ou may have a generic method that follows a
similar pattern:
C#
The method returns null when the sought item isn't found. Y ou can clarify that the
method returns null when an item isn't found by adding the MaybeNull annotation to
the method return:
C#
The preceding code informs callers that the return value may actually be null. It also
informs the compiler that the method may return a null expression even though the
type is non-nullable. When you have a generic method that returns an instance of its
type parameter, T, you can express that it never returns null by using the NotNull
attribute.
You can also specify that a return value or an argument isn't null even though the type is
a nullable reference type. The following method is a helper method that throws if its first
argument is null:
C#
You could call this routine as follows:public Customer? FindCustomer( string lastName, string firstName)
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
[return: MaybeNull ]
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
public static void ThrowWhenNull (object value, string valueExpression = "")
{
    if (value is null) throw new ArgumentNullException( nameof(value), 
valueExpression);
}C#
After enabling null reference types, you want to ensure that the preceding code
compiles without warnings. When the method returns, the value parameter is
guaranteed to be not null. However, it's acceptable to call ThrowWhenNull with a null
reference. Y ou can make value a nullable reference type, and add the NotNull post-
condition to the parameter declaration:
C#
The preceding code expresses the existing contract clearly: Callers can pass a variable
with the null value, but the argument is guaranteed to never be null if the method
returns without throwing an exception.
You specify unconditional postconditions using the following attributes:
MaybeNull : A non-nullable return value may be null.
NotNull : A nullable return value will never be null.
You're likely familiar with the string method String.IsNullOrEmpty(S tring) . This method
returns true when the argument is null or an empty string. It's a form of null-check:
Callers don't need to null-check the argument if the method returns false. To make a
method like this nullable aware, you'd set the argument to a nullable reference type,
and add the NotNullWhen attribute:
C#public static void LogMessage (string? message )
{
    ThrowWhenNull(message, $"{nameof(message)}  must not be null" );
    Console.WriteLine(message.Length);
}
public static void ThrowWhenNull ([NotNull] object? value, string 
valueExpression = "")
{
    _ = value ?? throw new ArgumentNullException( nameof(value), 
valueExpression);
    // other logic elided
Conditional post-conditions: NotNullWhen,
MaybeNullWhen, and NotNullIfNotNullThat informs the compiler that any code where the return value is false doesn't need
null checks. The addition of the attribute informs the compiler's static analysis that
IsNullOrEmpty performs the necessary null check: when it returns false, the argument
isn't null.
C#
The String.IsNullOrEmpty(S tring)  method will be annotated as shown above for .NET
Core 3.0. Y ou may have similar methods in your codebase that check the state of objects
for null values. The compiler won't recognize custom null check methods, and you'll
need to add the annotations yourself. When you add the attribute, the compiler's static
analysis knows when the tested variable has been null checked.
Another use for these attributes is the Try* pattern. The postconditions for ref and
out arguments are communicated through the return value. Consider this method
shown earlier (in a nullable disabled context):
C#bool IsNullOrEmpty ([NotNullWhen( false)] string? value)
string? userInput = GetUserInput();
if (!string.IsNullOrEmpty(userInput))
{
    int messageLength = userInput.Length; // no null check needed.
}
// null check needed on userInput here.
７ Note
The preceding example is only valid in C# 11 and later. S tarting with C# 11, the
nameo f expr ession  can reference parameter and type parameter names when used
in an attribute applied to a method. In C# 10 and earlier, you need to use a string
literal instead of the nameof expression.
bool TryGetMessage (string key, out string message )
{
    if (_messageMap.ContainsKey(key))
        message = _messageMap[key];
    else
        message = null;
    return message != null;
}The preceding method follows a typical .NET idiom: the return value indicates if message
was set to the found value or, if no message is found, to the default value. If the method
returns true, the value of message isn't null; otherwise, the method sets message to null.
In a nullable enabled context, you can communicate that idiom using the NotNullWhen
attribute. When you annotate parameters for nullable reference types, make message a
string? and add an attribute:
C#
In the preceding example, the value of message is known to be not null when
TryGetMessage returns true. You should annotate similar methods in your codebase in
the same way: the arguments could equal null, and are known to be not null when the
method returns true.
There's one final attribute you may also need. Sometimes the null state of a return value
depends on the null state of one or more arguments. These methods will return a non-
null value whenever certain arguments aren't null. To correctly annotate these
methods, you use the NotNullIfNotNull attribute. Consider the following method:
C#
If the url argument isn't null, the output isn't null. Once nullable references are
enabled, you need to add more annotations if your API may accept a null argument. Y ou
could annotate the return type as shown in the following code:
C#
That also works, but will often force callers to implement extra null checks. The
contract is that the return value would be null only when the argument url is null. Tobool TryGetMessage (string key, [NotNullWhen( true)] out string? message)
{
    if (_messageMap.ContainsKey(key))
        message = _messageMap[key];
    else
        message = null;
    return message is not null;
}
string GetTopLevelDomainFromFullUrl (string url)
string? GetTopLevelDomainFromFullUrl( string? url)express that contract, you would annotate this method as shown in the following code:
C#
The previous example uses the nameof  operator for the parameter url. That feature is
available in C# 11. Before C# 11, you'll need to type the name of the parameter as a
string. The return value and the argument have both been annotated with the ?
indicating that either could be null. The attribute further clarifies that the return value
won't be null when the url argument isn't null.
You specify conditional postconditions using these attributes:
MaybeNullWhen : A non-nullable argument may be null when the method returns
the specified bool value.
NotNullWhen : A nullable argument won't be null when the method returns the
specified bool value.
NotNullIfNotNull : A return value isn't null if the argument for the specified
parameter isn't null.
These attributes specify your intent when you've refactored common code from
constructors into helper methods. The C# compiler analyzes constructors and field
initializers to make sure that all non-nullable reference fields have been initialized before
each constructor returns. However, the C# compiler doesn't track field assignments
through all helper methods. The compiler issues warning CS8618 when fields aren't
initialized directly in the constructor, but rather in a helper method. Y ou add the
MemberNotNullAttribute  to a method declaration and specify the fields that are
initialized to a non-null value in the method. For example, consider the following
example:
C#[return: NotNullIfNotNull(nameof(url)) ]
string? GetTopLevelDomainFromFullUrl( string? url)
Helper methods: MemberNotNull and
MemberNotNullWhen
public class Container
{
    private string _uniqueIdentifier; // must be initialized.
    private string? _optionalMessage;
    public Container ()You can specify multiple field names as arguments to the MemberNotNull attribute
constructor.
The MemberNotNullWhenAttribute  has a bool argument. Y ou use MemberNotNullWhen in
situations where your helper method returns a bool indicating whether your helper
method initialized fields.
Some methods, typically exception helpers or other utility methods, always exit by
throwing an exception. Or, a helper may throw an exception based on the value of a
Boolean argument.
In the first case, you can add the DoesNotR eturnAttribute  attribute to the method
declaration. The compiler's null-st ate analysis doesn't check any code in a method that
follows a call to a method annotated with DoesNotReturn. Consider this method:
C#    {
        Helper();
    }
    public Container (string message )
    {
        Helper();
        _optionalMessage = message;
    }
    [MemberNotNull(nameof(_uniqueIdentifier)) ]
    private void Helper()
    {
        _uniqueIdentifier = DateTime.Now.Ticks.ToString();
    }
}
Stop nulla ble analysis when called method
throws
[DoesNotReturn ]
private void FailFast ()
{
    throw new InvalidOperationException();
}
public void SetState (object containedField )
{
    if (containedField is null)
    {The compiler doesn't issue any warnings after the call to FailFast.
In the second case, you add the
System.Diagnostics.CodeAnalysis.DoesNotR eturnIfAttribute  attribute to a Boolean
parameter of the method. Y ou can modify the previous example as follows:
C#
When the value of the argument matches the value of the DoesNotReturnIf constructor,
the compiler doesn't perform any null-st ate analysis after that method.
Adding nullable reference types provides an initial vocabulary to describe your APIs
expectations for variables that could be null. The attributes provide a richer vocabulary
to describe the null state of variables as preconditions and postconditions. These
attributes more clearly describe your expectations and provide a better experience for
the developers using your APIs.
As you update libraries for a nullable context, add these attributes to guide users of your
APIs to the correct usage. These attributes help you fully describe the null-state of
arguments and return values.
AllowNull : A non-nullable field, parameter, or property may be null.        FailFast();
    }
    // containedField can't be null:
    _field = containedField;
}
private void FailFastIf ([DoesNotReturnIf( true)] bool isNull)
{
    if (isNull)
    {
        throw new InvalidOperationException();
    }
}
public void SetFieldState (object? containedField )
{
    FailFastIf(containedField == null);
    // No warning: containedField can't be null here:
    _field = containedField;
}
SummaryDisallowNull : A nullable field, parameter, or property should never be null.
MaybeNull : A non-nullable field, parameter, property, or return value may be null.
NotNull : A nullable field, parameter, property, or return value will never be null.
MaybeNullWhen : A non-nullable argument may be null when the method returns
the specified bool value.
NotNullWhen : A nullable argument won't be null when the method returns the
specified bool value.
NotNullIfNotNull : A parameter, property, or return value isn't null if the argument
for the specified parameter isn't null.
DoesNotR eturn : A method or property never returns. In other words, it always
throws an exception.
DoesNotR eturnIf : This method or property never returns if the associated bool
parameter has the specified value.Miscellaneous attributes interpreted by
the C# compiler
Article •10/26/2023
The attributes Conditional, Obsolete, AttributeUsage, AsyncMethodBuilder,
InterpolatedStringHandler, ModuleInitializer, and Experimental can be applied to
elements in your code. They add semantic meaning to those elements. The compiler
uses those semantic meanings to alter its output and report possible mistakes by
developers using your code.
The Conditional attribute makes the execution of a method dependent on a
preprocessing identifier. The Conditional attribute is an alias for ConditionalAttribute ,
and can be applied to a method or an attribute class.
In the following example, Conditional is applied to a method to enable or disable the
display of program-specific diagnostic information:
C#Conditional attribute
#define TRACE_ON
using System.Diagnostics;
namespace  AttributeExamples ;
public class Trace
{
    [Conditional( "TRACE_ON" )]
    public static void Msg(string msg)
    {
        Console.WriteLine(msg);
    }
}
public class TraceExample
{
    public static void Main()
    {
        Trace.Msg( "Now in Main..." );
        Console.WriteLine( "Done.");
    }
}If the TRACE_ON identifier isn't defined, the trace output isn't displayed. Explore for
yourself in the interactive window.
The Conditional attribute is often used with the DEBUG identifier to enable trace and
logging features for debug builds but not in release builds, as shown in the following
example:
C#
When a method marked conditional is called, the presence or absence of the specified
preprocessing symbol determines whether the compiler includes or omits calls to the
method. If the symbol is defined, the call is included; otherwise, the call is omitted. A
conditional method must be a method in a class or struct declaration and must have a
void return type. Using Conditional is cleaner, more elegant, and less error-prone than
enclosing methods inside #if…#endif blocks.
If a method has multiple Conditional attributes, compiler includes calls to the method if
one or more conditional symbols are defined (the symbols are logically linked together
by using the OR operator). In the following example, the presence of either A or B
results in a method call:
C#
The Conditional attribute can also be applied to an attribute class definition. In the
following example, the custom attribute Documentation adds information to the
metadata if DEBUG is defined.
C#[Conditional( "DEBUG")]
static void DebugMethod ()
{
}
[Conditional( "A"), Conditional( "B")]
static void DoIfAorB ()
{
    // ...
}
Using Conditional with attribute classes
[Conditional( "DEBUG")]
public class DocumentationAttribute  : System.AttributeThe Obsolete attribute marks a code element as no longer recommended for use. Use
of an entity marked obsolete generates a warning or an error. The Obsolete attribute is
a single-use attribute and can be applied to any entity that allows attributes. Obsolete is
an alias for ObsoleteAttribute .
In the following example, the Obsolete attribute is applied to class A and to method
B.OldMethod. Because the second argument of the attribute constructor applied to
B.OldMethod is set to true, this method causes a compiler error, whereas using class A
produces a warning. Calling B.NewMethod, however, produces no warning or error. For
example, when you use it with the previous definitions, the following code generates
two warnings and one error:
C#{
    string text;
    public DocumentationAttribute (string text)
    {
        this.text = text;
    }
}
class SampleClass
{
    // This attribute will only be included if DEBUG is defined.
    [Documentation( "This method displays an integer." )]
    static void DoWork(int i)
    {
        System.Console.WriteLine(i.ToString());
    }
}
Obsolete attribute
namespace  AttributeExamples
{
    [Obsolete( "use class B" )]
    public class A
    {
        public void Method() { }
    }
    public class B
    {
        [Obsolete( "use NewMethod" , true)]
        public void OldMethod () { }The string provided as the first argument to the attribute constructor is displayed as part
of the warning or error. T wo warnings for class A are generated: one for the declaration
of the class reference, and one for the class constructor. The Obsolete attribute can be
used without arguments, but including an explanation what to use instead is
recommended.
In C# 10, you can use constant string interpolation and the nameof operator to ensure
the names match:
C#
Beginning in C# 12, types, methods, and assemblies can be marked with the
System.Diagnostics.CodeAnalysis.ExperimentalAttribute  to indicate an experimental
feature. The compiler issues a warning if you access a method or type annotated with
the ExperimentalAttribute . All types declared in an assembly or module marked with the        public void NewMethod () { }
    }
    public static class ObsoleteProgram
    {
        public static void Main()
        {
            // Generates 2 warnings:
            A a = new A();
            // Generate no errors or warnings:
            B b = new B();
            b.NewMethod();
            // Generates an error, compilation fails.
            // b.OldMethod();
        }
    }
}
public class B
{
    [Obsolete( $"use {nameof(NewMethod)}  instead" , true)]
    public void OldMethod () { }
    public void NewMethod () { }
}
Experimental attributeExperimental attribute are experimental. The compiler issues a warning if you access
any of them. Y ou can disable these warnings to pilot an experimental feature.
You can read more details about the Experimental attribute in the feature specification .
The SetsRequiredMembers attribute informs the compiler that a constructor sets all
required members in that class or struct. The compiler assumes any constructor with
the System.Diagnostics.CodeAnalysis.SetsR equiredMembersAttribute  attribute initializes
all required members. Any code that invokes such a constructor doesn't need object
initializers to set required members. Adding the SetsRequiredMembers attribute is
primarily useful for positional records and primary constructors.
The AttributeUsage attribute determines how a custom attribute class can be used.
AttributeUsageAttribute  is an attribute you apply to custom attribute definitions. The
AttributeUsage attribute enables you to control:
Which program elements the attribute can be applied to. Unless you restrict its
usage, an attribute can be applied to any of the following program elements:
Assembly
Module
Field
Event
Method
Param
Property
Return
Type
Whether an attribute can be applied to a single program element multiple times.２ Warning
Experimental features are subject to changes. The APIs may change, or they may be
removed in future updates. Including experimental features is a way for library
authors to get feedback on ideas and concepts for future development. Use
extreme caution when using any feature marked as experimental.
SetsRequiredMembers attribute
AttributeUsage attributeWhether derived classes inherit attributes.
The default settings look like the following example when applied explicitly:
C#
In this example, the NewAttribute class can be applied to any supported program
element. But it can be applied only once to each entity. Derived classes inherit the
attribute applied to a base class.
The AllowMultiple  and Inherited  arguments are optional, so the following code has the
same effect:
C#
The first AttributeUsageAttribute  argument must be one or more elements of the
AttributeT argets  enumeration. Multiple target types can be linked together with the OR
operator, like the following example shows:
C#
Attributes can be applied to either the property or the backing field for an
autoimplemented property. The attribute applies to the property, unless you specify the
field specifier on the attribute. Both are shown in the following example:
C#[AttributeUsage(AttributeTargets.All,
                   AllowMultiple = false,
                   Inherited = true) ]
class NewAttribute  : Attribute  { }
[AttributeUsage(AttributeTargets.All) ]
class NewAttribute  : Attribute  { }
[AttributeUsage(AttributeTargets.Property | AttributeTargets.Field) ]
class NewPropertyOrFieldAttribute  : Attribute  { }
class MyClass
{
    // Attribute attached to property:
    [NewPropertyOrField ]
    public string Name { get; set; } = string.Empty;
    // Attribute attached to backing field:
    [field: NewPropertyOrField ]If the AllowMultiple  argument is true, then the resulting attribute can be applied more
than once to a single entity, as shown in the following example:
C#
In this case, MultiUseAttribute can be applied repeatedly because AllowMultiple is set
to true. Both formats shown for applying multiple attributes are valid.
If Inherited  is false, then derived classes don't inherit the attribute from an attributed
base class. For example:
C#
In this case, NonInheritedAttribute isn't applied to DClass via inheritance.
You can also use these keywords to specify where an attribute should be applied. For
example, you can use the field: specifier to add an attribute to the backing field of an
autoimplemented property . Or you can use the field:, property: or param: specifier to
apply an attribute to any of the elements generated from a positional record. For an
example, see Positional syntax for property definition .    public string Description { get; set; } = string.Empty;
}
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true) ]
class MultiUse  : Attribute  { }
[MultiUse ]
[MultiUse ]
class Class1 { }
[MultiUse, MultiUse ]
class Class2 { }
[AttributeUsage(AttributeTargets.Class, Inherited = false) ]
class NonInheritedAttribute  : Attribute  { }
[NonInherited ]
class BClass { }
class DClass : BClass { }
AsyncMethodBuilder attributeYou add the System.Runtime.CompilerServices.AsyncMethodBuilderAttribute  attribute to
a type that can be an async return type. The attribute specifies the type that builds the
async method implementation when the specified type is returned from an async
method. The AsyncMethodBuilder attribute can be applied to a type that:
Has an accessible GetAwaiter method.
The object returned by the GetAwaiter method implements the
System.Runtime.CompilerServices.ICriticalNotifyCompletion  interface.
The constructor to the AsyncMethodBuilder attribute specifies the type of the associated
builder. The builder must implement the following accessible members:
A static Create() method that returns the type of the builder.
A readable Task property that returns the async return type.
A void SetException(Exception) method that sets the exception when a task
faults.
A void SetResult() or void SetResult(T result) method that marks the task as
completed and optionally sets the task's result
A Start method with the following API signature:
C#
An AwaitOnCompleted method with the following signature:
C#
An AwaitUnsafeOnCompleted method with the following signature:
C#void Start<TStateMachine>( ref TStateMachine stateMachine)
          where TStateMachine :  
System.Runtime.CompilerServices.IAsyncStateMachine
public void AwaitOnCompleted<TAwaiter, TStateMachine>( ref TAwaiter  
awaiter, ref TStateMachine stateMachine)
    where TAwaiter : System.Runtime.CompilerServices.INotifyCompletion
    where TStateMachine :  
System.Runtime.CompilerServices.IAsyncStateMachine
      public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>( ref 
TAwaiter awaiter, ref TStateMachine stateMachine)You can learn about async method builders by reading about the following builders
supplied by .NET:
System.Runtime.CompilerServices.AsyncT askMethodBuilder
System.Runtime.CompilerServices.AsyncT askMethodBuilder<TR esult>
System.Runtime.CompilerServices.AsyncV alueT askMethodBuilder
System.Runtime.CompilerServices.AsyncV alueT askMethodBuilder<TR esult>
In C# 10 and later, the AsyncMethodBuilder attribute can be applied to an async method
to override the builder for that type.
Starting with C# 10, you use these attributes to specify that a type is an interpolat ed
string handler . The .NET 6 library already includes
System.Runtime.CompilerServices.DefaultInterpolatedS tringHandler  for scenarios where
you use an interpolated string as the argument for a string parameter. Y ou might have
other instances where you want to control how interpolated strings are processed. Y ou
apply the System.Runtime.CompilerServices.InterpolatedS tringHandlerAttribute  to the
type that implements your handler. Y ou apply the
System.Runtime.CompilerServices.InterpolatedS tringHandlerArgumentAttribute  to
parameters of that type's constructor.
You can learn more about building an interpolated string handler in the C# 10 feature
specification for interpolated string improvements .
The ModuleInitializer attribute marks a method that the runtime calls when the
assembly loads. ModuleInitializer is an alias for ModuleInitializerAttribute .
The ModuleInitializer attribute can only be applied to a method that:
Is static.
Is parameterless.          where TAwaiter :  
System.Runtime.CompilerServices.ICriticalNotifyCompletion
          where TStateMachine :  
System.Runtime.CompilerServices.IAsyncStateMachine
InterpolatedStringHandler and
InterpolatedStringHandlerArguments attributes
ModuleInitializer attributeReturns void.
Is accessible from the containing module, that is, internal or public.
Isn't a generic method.
Isn't contained in a generic class.
Isn't a local function.
The ModuleInitializer attribute can be applied to multiple methods. In that case, the
order in which the runtime calls them is deterministic but not specified.
The following example illustrates use of multiple module initializer methods. The Init1
and Init2 methods run before Main, and each adds a string to the Text property. So
when Main runs, the Text property already has strings from both initializer methods.
C#
C#using System;
internal  class ModuleInitializerExampleMain
{
    public static void Main()
    {
        Console.WriteLine(ModuleInitializerExampleModule.Text);
        //output: Hello from Init1! Hello from Init2!
    }
}
using System.Runtime.CompilerServices;
internal  class ModuleInitializerExampleModule
{
    public static string? Text { get; set; }
    [ModuleInitializer ]
    public static void Init1()
    {
        Text += "Hello from Init1! " ;
    }
    [ModuleInitializer ]
    public static void Init2()
    {
        Text += "Hello from Init2! " ;
    }
}Source code generators sometimes need to generate initialization code. Module
initializers provide a standard place for that code. In most other cases, you should write
a static constructor  instead of a module initializer.
The SkipLocalsInit attribute prevents the compiler from setting the .locals init flag
when emitting to metadata. The SkipLocalsInit attribute is a single-use attribute and
can be applied to a method, a property, a class, a struct, an interface, or a module, but
not to an assembly. SkipLocalsInit is an alias for SkipLocalsInitAttribute .
The .locals init flag causes the CLR to initialize all of the local variables declared in a
method to their default values. Since the compiler also makes sure that you never use a
variable before assigning some value to it, .locals init is typically not necessary.
However, the extra zero-initialization might have measurable performance impact in
some scenarios, such as when you use stackalloc  to allocate an array on the stack. In
those cases, you can add the SkipLocalsInit attribute. If applied to a method directly,
the attribute affects that method and all its nested functions, including lambdas and
local functions. If applied to a type or module, it affects all methods nested inside. This
attribute doesn't affect abstract methods, but it does affect code generated for the
implementation.
This attribute requires the AllowUnsafeBlocks  compiler option. This requirement signals
that in some cases code could view unassigned memory (for example, reading from
uninitialized stack-allocated memory).
The following example illustrates the effect of SkipLocalsInit attribute on a method
that uses stackalloc. The method displays whatever was in memory when the array of
integers was allocated.
C#SkipLocalsInit attribute
[SkipLocalsInit ]
static void ReadUninitializedMemory ()
{
    Span<int> numbers = stackalloc  int[120];
    for (int i = 0; i < 120; i++)
    {
        Console.WriteLine(numbers[i]);
    }
}
// output depends on initial contents of memory, for example:
//0
//0To try this code yourself, set the AllowUnsafeBlocks compiler option in your .csproj file:
XML
Attribute
System.R eflection
Attributes
Reflection//0
//168
//0
//-1271631451
//32767
//38
//0
//0
//0
//38
// Remaining rows omitted for brevity.
<PropertyGroup >
  ...
  <AllowUnsafeBlocks >true</AllowUnsafeBlocks >
</PropertyGroup >
See also
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
 Provide product feedbackUnsafe code, pointer types, and
function pointers
Article •09/29/2022
Most of the C# code you write is "verifiably safe code." Verifiably s afe code means .NET
tools can verify that the code is safe. In general, safe code doesn't directly access
memory using pointers. It also doesn't allocate raw memory. It creates managed objects
instead.
C# supports an unsafe  context, in which you may write unverifiable  code. In an unsafe
context, code may use pointers, allocate and free blocks of memory, and call methods
using function pointers. Unsafe code in C# isn't necessarily dangerous; it's just code
whose safety cannot be verified.
Unsafe code has the following properties:
Methods, types, and code blocks can be defined as unsafe.
In some cases, unsafe code may increase an application's performance by
removing array bounds checks.
Unsafe code is required when you call native functions that require pointers.
Using unsafe code introduces security and stability risks.
The code that contains unsafe blocks must be compiled with the
AllowUnsafeBlocks  compiler option.
In an unsafe context, a type may be a pointer type, in addition to a value type, or a
reference type. A pointer type declaration takes one of the following forms:
C#
The type specified before the * in a pointer type is called the referent type . Only an
unmanaged type  can be a referent type.
Pointer types don't inherit from object  and no conversions exist between pointer types
and object. Also, boxing and unboxing don't support pointers. However, you can
convert between different pointer types and between pointer types and integral types.Pointer types
type* identifier;
void* identifier; //allowed but not recommendedWhen you declare multiple pointers in the same declaration, you write the asterisk ( *)
together with the underlying type only. It isn't used as a prefix to each pointer name. For
example:
C#
A pointer can't point to a reference or to a struct  that contains references, because an
object reference can be garbage collected even if a pointer is pointing to it. The garbage
collector doesn't keep track of whether an object is being pointed to by any pointer
types.
The value of the pointer variable of type MyType* is the address of a variable of type
MyType. The following are examples of pointer type declarations:
int* p: p is a pointer to an integer.
int** p: p is a pointer to a pointer to an integer.
int*[] p: p is a single-dimensional array of pointers to integers.
char* p: p is a pointer to a char.
void* p: p is a pointer to an unknown type.
The pointer indirection operator * can be used to access the contents at the location
pointed to by the pointer variable. For example, consider the following declaration:
C#
The expression *myVariable denotes the int variable found at the address contained in
myVariable.
There are several examples of pointers in the articles on the fixed  statement . The
following example uses the unsafe keyword and the fixed statement, and shows how
to increment an interior pointer. Y ou can paste this code into the Main function of a
console application to run it. These examples must be compiled with the
AllowUnsafeBlocks  compiler option set.
C#int* p1, p2, p3;   // Ok
int *p1, *p2, *p3;   // Invalid in C#
int* myVariable;
// Normal pointer to an object.
int[] a = new int[5] { 10, 20, 30, 40, 50 };You can't apply the indirection operator to a pointer of type void*. However, you can
use a cast to convert a void pointer to any other pointer type, and vice versa.
A pointer can be null. Applying the indirection operator to a null pointer causes an
implementation-defined behavior.
Passing pointers between methods can cause undefined behavior. Consider a method
that returns a pointer to a local variable through an in, out, or ref parameter or as the// Must be in unsafe code to use interior pointers.
unsafe
{
    // Must pin object on heap so that it doesn't move while using interior  
pointers.
    fixed (int* p = &a[ 0])
    {
        // p is pinned as well as object, so create another pointer to show  
incrementing it.
        int* p2 = p;
        Console.WriteLine(*p2);
        // Incrementing p2 bumps the pointer by four bytes due to its type  
...
        p2 += 1;
        Console.WriteLine(*p2);
        p2 += 1;
        Console.WriteLine(*p2);
        Console.WriteLine( "--------" );
        Console.WriteLine(*p);
        // Dereferencing p and incrementing changes the value of a[0] ...
        *p += 1;
        Console.WriteLine(*p);
        *p += 1;
        Console.WriteLine(*p);
    }
}
Console.WriteLine( "--------" );
Console.WriteLine(a[ 0]);
/*
Output:
10
20
30
--------
10
11
12
--------
12
*/function result. If the pointer was set in a fixed block, the variable to which it points may
no longer be fixed.
The following table lists the operators and statements that can operate on pointers in an
unsafe context:
Operat or/Statement Use
* Performs pointer indirection.
-> Accesses a member of a struct through a pointer.
[] Indexes a pointer.
& Obtains the address of a variable.
++ and -- Increments and decrements pointers.
+ and - Performs pointer arithmetic.
==, !=, <, >, <=, and >= Compares pointers.
stackalloc Allocates memory on the stack.
fixed  statement Temporarily fixes a variable so that its address may be found.
For more information about pointer-related operators, see Pointer-related operators .
Any pointer type can be implicitly converted to a void* type. Any pointer type can be
assigned the value null. Any pointer type can be explicitly converted to any other
pointer type using a cast expression. Y ou can also convert any integral type to a pointer
type, or any pointer type to an integral type. These conversions require an explicit cast.
The following example converts an int* to a byte*. Notice that the pointer points to
the lowest addressed byte of the variable. When you successively increment the result,
up to the size of int (4 bytes), you can display the remaining bytes of the variable.
C#
int number = 1024;
unsafe
{
    // Convert to byte:
    byte* p = (byte*)&number;
    System.Console.Write( "The 4 bytes of the integer:" );
    // Display the 4 bytes of the int variable:You can use the fixed keyword to create a buffer with a fixed-size array in a data
structure. Fixed-size buffers are useful when you write methods that interoperate with
data sources from other languages or platforms. The fixed-size buffer can take any
attributes or modifiers that are allowed for regular struct members. The only restriction
is that the array type must be bool, byte, char, short, int, long, sbyte, ushort, uint,
ulong, float, or double.
C#
In safe code, a C# struct that contains an array doesn't contain the array elements. The
struct contains a reference to the elements instead. Y ou can embed an array of fixed size
in a struct  when it's used in an unsafe  code block.
The size of the following struct doesn't depend on the number of elements in the
array, since pathName is a reference:
C#
A struct can contain an embedded array in unsafe code. In the following example, the
fixedBuffer array has a fixed size. Y ou use a fixed  statement  to get a pointer to the first    for (int i = 0 ; i < sizeof(int) ; ++i)
    {
        System.Console.Write( " {0:X2}" , *p);
        // Increment the pointer:
        p++;
    }
    System.Console.WriteLine();
    System.Console.WriteLine( "The value of the integer: {0}" , number);
    /* Output:
        The 4 bytes of the integer: 00 04 00 00
        The value of the integer: 1024
    */
}
Fixed-size buffers
private fixed char name[30];
public struct PathArray
{
    public char[] pathName;
    private int reserved;
}element. Y ou access the elements of the array through this pointer. The fixed statement
pins the fixedBuffer instance field to a specific location in memory.
C#
The size of the 128 element char array is 256 bytes. Fixed-size char buffers always take
2 bytes per character, regardless of the encoding. This array size is the same even when
char buffers are marshalled to API methods or structs with CharSet = CharSet.Auto or
CharSet = CharSet.Ansi. For more information, see CharSet .
The preceding example demonstrates accessing fixed fields without pinning. Another
common fixed-size array is the bool array. The elements in a bool array are always 1
byte in size. bool arrays aren't appropriate for creating bit arrays or buffers.
Fixed-size buffers are compiled with the
System.Runtime.CompilerServices.UnsafeV alueT ypeAttribute , which instructs the
common language runtime (CLR) that a type contains an unmanaged array that caninternal  unsafe struct Buffer
{
    public fixed char fixedBuffer[ 128];
}
internal  unsafe class Example
{
    public Buffer buffer = default;
}
private static void AccessEmbeddedArray ()
{
    var example = new Example();
    unsafe
    {
        // Pin the buffer to a fixed location in memory.
        fixed (char* charPtr = example.buffer.fixedBuffer)
        {
            *charPtr = 'A';
        }
        // Access safely through the index:
        char c = example.buffer.fixedBuffer[ 0];
        Console.WriteLine(c);
        // Modify through the index:
        example.buffer.fixedBuffer[ 0] = 'B';
        Console.WriteLine(example.buffer.fixedBuffer[ 0]);
    }
}potentially overflow. Memory allocated using stackalloc  also automatically enables
buffer overrun detection features in the CLR. The previous example shows how a fixed-
size buffer could exist in an unsafe struct.
C#
The compiler-generated C# for Buffer is attributed as follows:
C#
Fixed-size buffers differ from regular arrays in the following ways:
May only be used in an unsafe context.
May only be instance fields of structs.
They're always vectors, or one-dimensional arrays.
The declaration should include the length, such as fixed char id[8]. You can't use
fixed char id[].
The following example uses pointers to copy bytes from one array to another.
This example uses the unsafe  keyword, which enables you to use pointers in the Copy
method. The fixed  statement is used to declare pointers to the source and destination
arrays. The fixed statement pins the location of the source and destination arrays in
memory so that they will not be moved by garbage collection. The memory blocks forinternal  unsafe struct Buffer
{
    public fixed char fixedBuffer[ 128];
}
internal  struct Buffer
{
    [StructLayout(LayoutKind.Sequential, Size = 256)]
    [CompilerGenerated ]
    [UnsafeValueType ]
    public struct <fixedBuffer>e__FixedBuffer
    {
        public char FixedElementField;
    }
    [FixedBuffer(typeof(char), 128)]
    public <fixedBuffer>e__FixedBuffer fixedBuffer;
}
How to use pointers to copy an array of bytesthe arrays are unpinned when the fixed block is completed. Because the Copy method
in this example uses the unsafe keyword, it must be compiled with the
AllowUnsafeBlocks  compiler option.
This example accesses the elements of both arrays using indices rather than a second
unmanaged pointer. The declaration of the pSource and pTarget pointers pins the
arrays.
C#
static unsafe void Copy(byte[] source, int sourceOffset, byte[] target,
    int targetOffset, int count)
{
    // If either array is not instantiated, you cannot complete the copy.
    if ((source == null) || (target == null))
    {
        throw new System.ArgumentException( "source or target is null" );
    }
    // If either offset, or the number of bytes to copy, is negative, you
    // cannot complete the copy.
    if ((sourceOffset < 0) || (targetOffset < 0) || (count < 0))
    {
        throw new System.ArgumentException( "offset or bytes to copy is  
negative" );
    }
    // If the number of bytes from the offset to the end of the array is
    // less than the number of bytes you want to copy, you cannot complete
    // the copy.
    if ((source.Length - sourceOffset < count) ||
        (target.Length - targetOffset < count))
    {
        throw new System.ArgumentException( "offset to end of array is less  
than bytes to be copied" );
    }
    // The following fixed statement pins the location of the source and
    // target objects in memory so that they will not be moved by garbage
    // collection.
    fixed (byte* pSource = source, pTarget = target)
    {
        // Copy the specified number of bytes from source to target.
        for (int i = 0; i < count; i++)
        {
            pTarget[targetOffset + i] = pSource[sourceOffset + i];
        }
    }
}
static void UnsafeCopyArrays ()
{    // Create two arrays of the same length.
    int length = 100;
    byte[] byteArray1 = new byte[length];
    byte[] byteArray2 = new byte[length];
    // Fill byteArray1 with 0 - 99.
    for (int i = 0; i < length; ++i)
    {
        byteArray1[i] = ( byte)i;
    }
    // Display the first 10 elements in byteArray1.
    System.Console.WriteLine( "The first 10 elements of the original are:" );
    for (int i = 0; i < 10; ++i)
    {
        System.Console.Write(byteArray1[i] + " ");
    }
    System.Console.WriteLine( "\n");
    // Copy the contents of byteArray1 to byteArray2.
    Copy(byteArray1, 0, byteArray2, 0, length);
    // Display the first 10 elements in the copy, byteArray2.
    System.Console.WriteLine( "The first 10 elements of the copy are:" );
    for (int i = 0; i < 10; ++i)
    {
        System.Console.Write(byteArray2[i] + " ");
    }
    System.Console.WriteLine( "\n");
    // Copy the contents of the last 10 elements of byteArray1 to the
    // beginning of byteArray2.
    // The offset specifies where the copying begins in the source array.
    int offset = length - 10;
    Copy(byteArray1, offset, byteArray2, 0, length - offset);
    // Display the first 10 elements in the copy, byteArray2.
    System.Console.WriteLine( "The first 10 elements of the copy are:" );
    for (int i = 0; i < 10; ++i)
    {
        System.Console.Write(byteArray2[i] + " ");
    }
    System.Console.WriteLine( "\n");
    /* Output:
        The first 10 elements of the original are:
        0 1 2 3 4 5 6 7 8 9
        The first 10 elements of the copy are:
        0 1 2 3 4 5 6 7 8 9
        The first 10 elements of the copy are:
        90 91 92 93 94 95 96 97 98 99
    */
}C# provides delegate  types to define safe function pointer objects. Invoking a delegate
involves instantiating a type derived from System.Delegate  and making a virtual method
call to its Invoke method. This virtual call uses the callvirt IL instruction. In
performance critical code paths, using the calli IL instruction is more efficient.
You can define a function pointer using the delegate* syntax. The compiler will call the
function using the calli instruction rather than instantiating a delegate object and
calling Invoke. The following code declares two methods that use a delegate or a
delegate* to combine two objects of the same type. The first method uses a
System.Func<T1,T2,TR esult>  delegate type. The second method uses a delegate*
declaration with the same parameters and return type:
C#
The following code shows how you would declare a static local function and invoke the
UnsafeCombine method using a pointer to that local function:
C#
The preceding code illustrates several of the rules on the function accessed as a function
pointer:
Function pointers can only be declared in an unsafe context.
Methods that take a delegate* (or return a delegate*) can only be called in an
unsafe context.
The & operator to obtain the address of a function is allowed only on static
functions. (This rule applies to both member functions and local functions).
The syntax has parallels with declaring delegate types and using pointers. The * suffix
on delegate indicates the declaration is a function point er. The & when assigning aFunction pointers
public static T Combine<T>(Func<T, T, T> combinator, T left, T right) => 
    combinator(left, right);
public static T UnsafeCombine<T>( delegate *<T, T, T> combinator, T left, T  
right) => 
    combinator(left, right);
static int localMultiply (int x, int y) => x * y;
int product = UnsafeCombine(&localMultiply, 3, 4);method group to a function pointer indicates the operation takes the address of the
method.
You can specify the calling convention for a delegate* using the keywords managed and
unmanaged. In addition, for unmanaged function pointers, you can specify the calling
convention. The following declarations show examples of each. The first declaration uses
the managed calling convention, which is the default. The next four use an unmanaged
calling convention. Each specifies one of the ECMA 335 calling conventions: Cdecl,
Stdcall, Fastcall, or Thiscall. The last declaration uses the unmanaged calling
convention, instructing the CLR to pick the default calling convention for the platform.
The CLR will choose the calling convention at run time.
C#
You can learn more about function pointers in the Function pointer  feature spec.
For more information, see the Unsafe code  chapter of the C# language specification .public static T ManagedCombine<T>( delegate * managed<T, T, T> combinator, T  
left, T right) =>
    combinator(left, right);
public static T CDeclCombine<T>( delegate * unmanaged [Cdecl]<T, T, T>  
combinator, T left, T right) =>
    combinator(left, right);
public static T StdcallCombine<T>( delegate * unmanaged [Stdcall]<T, T, T>  
combinator, T left, T right) =>
    combinator(left, right);
public static T FastcallCombine<T>( delegate * unmanaged [Fastcall]<T, T, T>  
combinator, T left, T right) =>
    combinator(left, right);
public static T ThiscallCombine<T>( delegate * unmanaged [Thiscall]<T, T, T>  
combinator, T left, T right) =>
    combinator(left, right);
public static T UnmanagedCombine<T>( delegate * unmanaged <T, T, T> combinator,  
T left, T right) =>
    combinator(left, right);
C# language specification
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you.NET feedb ack
The .NET documentation is open
source. Provide feedback here.can also create and review
issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackC# preprocessor directives
Article •02/01/2023
Although the compiler doesn't have a separate preprocessor, the directives described in
this section are processed as if there were one. Y ou use them to help in conditional
compilation. Unlike C and C++ directives, you can't use these directives to create
macros. A preprocessor directive must be the only instruction on a line.
The #nullable preprocessor directive sets the nullable annot ation c ontext and nullable
warning c ontext. This directive controls whether nullable annotations have effect, and
whether nullability warnings are given. Each context is either disabled  or enabled .
Both contexts can be specified at the project level (outside of C# source code). The
#nullable directive controls the annotation and warning contexts and takes precedence
over the project-level settings. A directive sets the context(s) it controls until another
directive overrides it, or until the end of the source file.
The effect of the directives is as follows:
#nullable disable: Sets the nullable annotation and warning contexts to disabled .
#nullable enable: Sets the nullable annotation and warning contexts to enabled .
#nullable restore: Restores the nullable annotation and warning contexts to
project settings.
#nullable disable annotations: Sets the nullable annotation context to disabled .
#nullable enable annotations: Sets the nullable annotation context to enabled .
#nullable restore annotations: Restores the nullable annotation context to
project settings.
#nullable disable warnings: Sets the nullable warning context to disabled .
#nullable enable warnings: Sets the nullable warning context to enabled .
#nullable restore warnings: Restores the nullable warning context to project
settings.
You use four preprocessor directives to control conditional compilation:Nullable context
Conditional compilation#if: Opens a conditional compilation, where code is compiled only if the specified
symbol is defined.
#elif: Closes the preceding conditional compilation and opens a new conditional
compilation based on if the specified symbol is defined.
#else: Closes the preceding conditional compilation and opens a new conditional
compilation if the previous specified symbol isn't defined.
#endif: Closes the preceding conditional compilation.
The C# compiler compiles the code between the #if directive and #endif directive only
if the specified symbol is defined, or not defined when the ! not operator is used.
Unlike C and C++, a numeric value to a symbol can't be assigned. The #if statement in
C# is Boolean and only tests whether the symbol has been defined or not. For example,
the following code is compiled when DEBUG is defined:
C#
The following code is compiled when MYTEST is not defined:
C#
You can use the operators == (equality)  and != (inequality)  to test for the bool values
true or false. true means the symbol is defined. The statement #if DEBUG has the
same meaning as #if (DEBUG == true). You can use the && (and) , || (or), and ! (not)
operators to evaluate whether multiple symbols have been defined. Y ou can also group
symbols and operators with parentheses.
#if, along with the #else, #elif, #endif, #define, and #undef directives, lets you
include or exclude code based on the existence of one or more symbols. Conditional
compilation can be useful when compiling code for a debug build or when compiling
for a specific configuration.
A conditional directive beginning with an #if directive must explicitly be terminated
with an #endif directive. #define lets you define a symbol. By using the symbol as the
expression passed to the #if directive, the expression evaluates to true. You can also#if DEBUG 
    Console.WriteLine( "Debug version" ); 
#endif 
#if !MYTEST  
    Console.WriteLine( "MYTEST is not defined" ); 
#endif define a symbol with the DefineConstants  compiler option. Y ou can undefine a symbol
with #undef. The scope of a symbol created with #define is the file in which it was
defined. A symbol that you define with DefineConstants  or with #define doesn't
conflict with a variable of the same name. That is, a variable name shouldn't be passed
to a preprocessor directive, and a symbol can only be evaluated by a preprocessor
directive.
#elif lets you create a compound conditional directive. The #elif expression will be
evaluated if neither the preceding #if nor any preceding, optional, #elif directive
expressions evaluate to true. If an #elif expression evaluates to true, the compiler
evaluates all the code between the #elif and the next conditional directive. For
example:
C#
#else lets you create a compound conditional directive, so that, if none of the
expressions in the preceding #if or (optional) #elif directives evaluate to true, the
compiler will evaluate all code between #else and the next #endif. #endif(#endif) must
be the next preprocessor directive after #else.
#endif specifies the end of a conditional directive, which began with the #if directive.
The build system is also aware of predefined preprocessor symbols representing
different target frameworks  in SDK-style projects. They're useful when creating
applications that can target more than one .NET version.
Target
Framew orksSymbols Additional symbols  
(available in .NE T 5+ SDKs)Platfor m symbols
(available only  
when y ou specif y an
OS-specific TFM)#define VC7 
//... 
#if DEBUG 
    Console.WriteLine( "Debug build" ); 
#elif VC7 
    Console.WriteLine( "Visual Studio 7" ); 
#endif Target
Framew orksSymbols Additional symbols  
(available in .NE T 5+ SDKs)Platfor m symbols
(available only  
when y ou specif y an
OS-specific TFM)
.NET
FrameworkNETFRAMEWORK,
NET48, NET472,
NET471, NET47,
NET462, NET461,
NET46, NET452,
NET451, NET45,
NET40, NET35, NET20NET48_OR_GREATER,
NET472_OR_GREATER,
NET471_OR_GREATER,
NET47_OR_GREATER,
NET462_OR_GREATER,
NET461_OR_GREATER,
NET46_OR_GREATER,
NET452_OR_GREATER,
NET451_OR_GREATER,
NET45_OR_GREATER,
NET40_OR_GREATER,
NET35_OR_GREATER,
NET20_OR_GREATER
.NET
StandardNETSTANDARD,
NETSTANDARD2_1,
NETSTANDARD2_0,
NETSTANDARD1_6,
NETSTANDARD1_5,
NETSTANDARD1_4,
NETSTANDARD1_3,
NETSTANDARD1_2,
NETSTANDARD1_1,
NETSTANDARD1_0NETSTANDARD2_1_OR_GREATER,
NETSTANDARD2_0_OR_GREATER,
NETSTANDARD1_6_OR_GREATER,
NETSTANDARD1_5_OR_GREATER,
NETSTANDARD1_4_OR_GREATER,
NETSTANDARD1_3_OR_GREATER,
NETSTANDARD1_2_OR_GREATER,
NETSTANDARD1_1_OR_GREATER,
NETSTANDARD1_0_OR_GREATER
.NET 5+
(and .NET
Core)NET, NET7_0,
NET6_0, NET5_0,
NETCOREAPP,
NETCOREAPP3_1,
NETCOREAPP3_0,
NETCOREAPP2_2,
NETCOREAPP2_1,
NETCOREAPP2_0,
NETCOREAPP1_1,
NETCOREAPP1_0NET7_0_OR_GREATER,
NET6_0_OR_GREATER,
NET5_0_OR_GREATER,
NETCOREAPP3_1_OR_GREATER,
NETCOREAPP3_0_OR_GREATER,
NETCOREAPP2_2_OR_GREATER,
NETCOREAPP2_1_OR_GREATER,
NETCOREAPP2_0_OR_GREATER,
NETCOREAPP1_1_OR_GREATER,
NETCOREAPP1_0_OR_GREATERANDROID, IOS,
MACCATALYST, MACOS,
TVOS, WINDOWS, 
[OS][version] (for
example IOS15_1), 
[OS]
[version]_OR_GREATER
(for example
IOS15_1_OR_GREATER)
７ Note
Versionless symbols are defined regardless of the version you're targeting.
Version-specific symbols are only defined for the version you're targeting.Other predefined symbols include the DEBUG and TRACE constants. Y ou can override the
values set for the project using #define. The DEBUG symbol, for example, is
automatically set depending on your build configuration properties ("Debug" or
"Release" mode).
The following example shows you how to define a MYTEST symbol on a file and then test
the values of the MYTEST and DEBUG symbols. The output of this example depends on
whether you built the project on Debug  or Release  configuration mode.
C#The <framework>_OR_GREATER symbols are defined for the version you're
targeting and all earlier versions. For example, if you're targeting .NET
Framework 2.0, the following symbols are defined: NET20, NET20_OR_GREATER,
NET11_OR_GREATER, and NET10_OR_GREATER.
These are different from the target framework monikers (TFMs) used by the
MSBuild TargetFramew ork proper ty and NuGet .
７ Note
For traditional, non-SDK-style projects, you have to manually configure the
conditional compilation symbols for the different target frameworks in Visual
Studio via the project's properties pages.
#define MYTEST 
using System;  
public class MyClass 
{ 
    static void Main() 
    { 
#if (DEBUG && !MYTEST)  
        Console.WriteLine( "DEBUG is defined" ); 
#elif (!DEBUG && MYTEST)  
        Console.WriteLine( "MYTEST is defined" ); 
#elif (DEBUG && MYTEST)  
        Console.WriteLine( "DEBUG and MYTEST are defined" );   
#else 
        Console.WriteLine( "DEBUG and MYTEST are not defined" ); 
#endif 
    } 
} The following example shows you how to test for different target frameworks so you can
use newer APIs when possible:
C#
You use the following two preprocessor directives to define or undefine symbols for
conditional compilation:
#define: Define a symbol.
#undef: Undefine a symbol.
You use #define to define a symbol. When you use the symbol as the expression that's
passed to the #if directive, the expression will evaluate to true, as the following
example shows:
C#public class MyClass 
{ 
    static void Main() 
    { 
#if NET40 
        WebClient _client = new WebClient();  
#else 
        HttpClient _client = new HttpClient();  
#endif 
    } 
    //... 
} 
Defining  symbols
#define VERBOSE  
#if VERBOSE  
   Console.WriteLine( "Verbose output version" ); 
#endif 
７ Note
The #define directive cannot be used to declare constant values as is typically
done in C and C++. Constants in C# are best defined as static members of a class
or struct. If you have several such constants, consider creating a separate
"Constants" class to hold them.Symbols can be used to specify conditions for compilation. Y ou can test for the symbol
with either #if or #elif. You can also use the ConditionalAttribute  to perform
conditional compilation. Y ou can define a symbol, but you can't assign a value to a
symbol. The #define directive must appear in the file before you use any instructions
that aren't also preprocessor directives. Y ou can also define a symbol with the
DefineConstants  compiler option. Y ou can undefine a symbol with #undef.
You can define regions of code that can be collapsed in an outline using the following
two preprocessor directives:
#region: Start a region.
#endregion: End a region.
#region lets you specify a block of code that you can expand or collapse when using the
outlining  feature of the code editor. In longer code files, it's convenient to collapse or
hide one or more regions so that you can focus on the part of the file that you're
currently working on. The following example shows how to define a region:
C#
A #region block must be terminated with an #endregion directive. A #region block can't
overlap with an #if block. However, a #region block can be nested in an #if block,
and an #if block can be nested in a #region block.
You instruct the compiler to generate user-defined compiler errors and warnings, and
control line information using the following directives:
#error: Generate a compiler error with a specified message.Defining  regions
#region MyClass definition  
public class MyClass 
{ 
    static void Main() 
    { 
    } 
} 
#endregion  
Error and warning information#warning: Generate a compiler warning, with a specific message.
#line: Change the line number printed with compiler messages.
#error lets you generate a CS1029  user-defined error from a specific location in your
code. For example:
C#
#warning lets you generate a CS1030  level one compiler warning from a specific
location in your code. For example:
C#
#line lets you modify the compiler's line numbering and (optionally) the file name
output for errors and warnings.
The following example shows how to report two warnings associated with line numbers.
The #line 200 directive forces the next line's number to be 200 (although the default is
#6), and until the next #line directive, the filename will be reported as "Special". The
#line default directive returns the line numbering to its default numbering, which
counts the lines that were renumbered by the previous directive.
C##error Deprecated code in this method.  
７ Note
The compiler treats #error version in a special way and reports a compiler error,
CS8304, with a message containing the used compiler and language versions.
#warning Deprecated code in this method.  
class MainClass  
{ 
    static void Main() 
    { 
#line 200 "Special"  
        int i; 
        int j; 
#line default  
        char c; 
        float f; 
#line hidden // numbering not affected  Compilation produces the following output:
Console
The #line directive might be used in an automated, intermediate step in the build
process. For example, if lines were removed from the original source code file, but you
still wanted the compiler to generate output based on the original line numbering in the
file, you could remove lines and then simulate the original line numbering with #line.
The #line hidden directive hides the successive lines from the debugger, such that
when the developer steps through the code, any lines between a #line hidden and the
next #line directive (assuming that it isn't another #line hidden directive) will be
stepped over. This option can also be used to allow ASP.NET to differentiate between
user-defined and machine-generated code. Although ASP.NET is the primary consumer
of this feature, it's likely that more source generators will make use of it.
A #line hidden directive doesn't affect file names or line numbers in error reporting.
That is, if the compiler finds an error in a hidden block, the compiler will report the
current file name and line number of the error.
The #line filename directive specifies the file name you want to appear in the compiler
output. By default, the actual name of the source code file is used. The file name must
be in double quotation marks ("") and must be preceded by a line number.
Beginning with C# 10, you can use a new form of the #line directive:
C#        string s; 
        double d; 
    } 
} 
Special(200,13): warning CS0168: The variable 'i' is declared but never used  
Special(201,13): warning CS0168: The variable 'j' is declared but never used  
MainClass.cs(9,14): warning CS0168: The variable 'c' is declared but never  
used 
MainClass.cs(10,15): warning CS0168: The variable 'f' is declared but never  
used 
MainClass.cs(12,16): warning CS0168: The variable 's' is declared but never  
used 
MainClass.cs(13,16): warning CS0168: The variable 'd' is declared but never  
used 
#line (1, 1) - (5, 60) 10 "partial-class.cs"  
/*34567*/ int b = 0; The components of this form are:
(1, 1): The start line and column for the first character on the line that follows the
directive. In this example, the next line would be reported as line 1, column 1.
(5, 60): The end line and column for the marked region.
10: The column offset for the #line directive to take effect. In this example, the
10th column would be reported as column one. That's where the declaration int b
= 0; begins. This field is optional. If omitted, the directive takes effect on the first
column.
"partial-class.cs": The name of the output file.
The preceding example would generate the following warning:
.NET CLI
After remapping, the variable, b, is on the first line, at character six, of the file partial-
class.cs.
Domain-specific languages (DSLs) typically use this format to provide a better mapping
from the source file to the generated C# output. The most common use of this extended
#line directive is to re-map warnings or errors that appear in a generated file to the
original source. For example, consider this razor page:
razor
The property DateTime.Now was typed incorrectly as DateTime.NowAndThen. The
generated C# for this razor snippet looks like the following, in page.g.cs:
C#
The compiler output for the preceding snippet is:partial-class.cs( 1,5,1,6): warning CS0219: The variable 'b' is assigned but  
its value is never used  
@page "/" 
Time: @DateTime.NowAndThen  
  _builder.Add( "Time: " ); 
#line (2, 6) (2, 27) 15 "page.razor"  
  _builder.Add(DateTime.NowAndThen);  .NET CLI
Line 2, column 6 in page.razor is where the text @DateTime.NowAndThen begins. That's
noted by (2, 6) in the directive. That span of @DateTime.NowAndThen ends at line 2,
column 27. That's noted by the (2, 27) in the directive. The text for
DateTime.NowAndThen begins in column 15 of page.g.cs. That's noted by the 15 in the
directive. Putting all the arguments together, and the compiler reports the error in its
location in page.razor. The developer can navigate directly to the error in their source
code, not the generated source.
To see more examples of this format, see the feature specification  in the section on
examples.
#pragma gives the compiler special instructions for the compilation of the file in which it
appears. The instructions must be supported by the compiler. In other words, you can't
use #pragma to create custom preprocessing instructions.
#pragma warning : Enable or disable warnings.
#pragma checksum : Generate a checksum.
C#
Where pragma-name is the name of a recognized pragma and pragma-arguments is the
pragma-specific arguments.
#pragma warning can enable or disable certain warnings.
C#page.razor( 2, 2, 2, 27)error CS0117: 'DateTime'  does not contain a  
definition for 'NowAndThen'  
Pragmas
#pragma pragma-name pragma-arguments  
#pragma warning
#pragma warning disable warning-list 
#pragma warning restore warning-list Where warning-list is a comma-separated list of warning numbers. The "CS" prefix is
optional. When no warning numbers are specified, disable disables all warnings and
restore enables all warnings.
The disable takes effect beginning on the next line of the source file. The warning is
restored on the line following the restore. If there's no restore in the file, the warnings
are restored to their default state at the first line of any later files in the same
compilation.
C#
Generates checksums for source files to aid with debugging ASP.NET pages.
C#７ Note
To find warning numbers in Visual S tudio, build your project and then look for the
warning numbers in the Output  window.
// pragma_warning.cs  
using System;  
#pragma warning disable 414, CS3021  
[CLSCompliant(false) ] 
public class C 
{ 
    int i = 1; 
    static void Main() 
    { 
    } 
} 
#pragma warning restore CS3021  
[CLSCompliant(false) ]  // CS3021  
public class D 
{ 
    int i = 1; 
    public static void F() 
    { 
    } 
} 
#pragma checksum
#pragma checksum  "filename" "{guid}" " checksum  bytes" Where "filename" is the name of the file that requires monitoring for changes or
updates, "{guid}" is the Globally Unique Identifier (GUID) for the hash algorithm, and
"checksum_bytes" is the string of hexadecimal digits representing the bytes of the
checksum. Must be an even number of hexadecimal digits. An odd number of digits
results in a compile-time warning, and the directive is ignored.
The Visual S tudio debugger uses a checksum to make sure that it always finds the right
source. The compiler computes the checksum for a source file, and then emits the
output to the program database (PDB) file. The debugger then uses the PDB to compare
against the checksum that it computes for the source file.
This solution doesn't work for ASP.NET projects, because the computed checksum is for
the generated source file, rather than the .aspx file. T o address this problem, #pragma
checksum provides checksum support for ASP.NET pages.
When you create an ASP.NET project in Visual C#, the generated source file contains a
checksum for the .aspx file, from which the source is generated. The compiler then
writes this information into the PDB file.
If the compiler doesn't find a #pragma checksum directive in the file, it computes the
checksum and writes the value to the PDB file.
C#
class TestClass  
{ 
    static int Main() 
    { 
        #pragma checksum  "file.cs" "{406EA660-64CF-4C82-B6F0-42D48172A799}"  
"ab007f1d23d9" // New checksum  
    } 
} C# compiler options
Article •09/15/2021
This section describes the options interpreted by the C# compiler. Options are grouped
into separate articles based on what they control, for example, language features, code
generation, and output. Use the table of contents to navigate amongst them.
There are two different ways to set compiler options in .NET projects:
In your *.cspr oj file
You can add MSBuild properties for any compiler option in your *.cspr oj file in XML
format. The property name is the same as the compiler option. The value of the
property sets the value of the compiler option. For example, the following project
file snippet sets the LangVersion property.
XML
For more information on setting options in project files, see the article MSBuild
properties for .NET SDK Projects .
Using the Visual S tudio Pr operty pages
Visual S tudio provides property pages to edit build properties. T o learn more about
them, see Manage project and solution properties - Windows  or Manage project
and solution properties - Mac .
In addition to the mechanisms described above, you can set compiler options using two
additional methods for .NET Framework projects:How to set options
<PropertyGroup > 
  <LangVersion >preview</LangVersion > 
</PropertyGroup > 
.NET Framework projects
） Impor tant
This section applies to .NET Framework projects only.Command line ar guments for .NE T Framew ork pr ojects : .NET Framework projects
use csc.exe instead of dotnet build to build projects. Y ou can specify command
line arguments to csc.exe for .NET Framework projects.
Compiled ASP .NET pages : .NET Framework projects use a section of the web.config
file for compiling pages. For the new build system, and ASP.NET Core projects,
options are taken from the project file.
The word for some compiler options changed from csc.exe and .NET Framework projects
to the new MSBuild system. The new syntax is used throughout this section. Both
versions are listed at the top of each page. For csc.exe, any arguments are listed
following the option and a colon. For example, the -doc option would be:
Console
You can invoke the C# compiler by typing the name of its executable file ( csc.exe) at a
command prompt.
For .NET Framework projects, you can also run csc.exe from the command line. Every
compiler option is available in two forms: -option  and /option . In .NET Framework web
projects, you specify options for compiling code-behind in the web.config file. For more
information, see <compiler> Element .
If you use the Developer Command Pr ompt for Visual S tudio  window, all the necessary
environment variables are set for you. For information on how to access this tool, see
Developer Command Prompt for Visual S tudio .
The csc.exe executable file is usually located in the Microsoft.NET\Framework\ <Version>
folder under the Windo ws directory. Its location might vary depending on the exact
configuration of a particular computer. If more than one version of .NET Framework is
installed on your computer, you'll find multiple versions of this file. For more
information about such installations, see How to: determine which versions of the .NET
Framework are installed .-doc:DocFile.xml  C# Compiler Options for language
feature rules
Article •11/01/2023
The following options control how the compiler interprets language features. The new
MSBuild syntax is shown in Bold . The older csc.exe syntax is shown in code style.
CheckForOv erflowUnder flow / -checked: Generate overflow checks.
AllowUnsafeBlocks  / -unsafe: Allow 'unsafe' code.
DefineConstants  / -define: Define conditional compilation symbol(s).
LangV ersion / -langversion: Specify language version such as default (latest
major version), or latest (latest version, including minor versions).
Nullable  / -nullable: Enable nullable context, or nullable warnings.
The CheckForOv erflowUnder flow option controls the default overflow-checking context
that defines the program behavior if integer arithmetic overflows.
XML
When CheckForOv erflowUnder flow is true, the default context is a checked context
and overflow checking is enabled; otherwise, the default context is an unchecked
context. The default value for this option is false, that is, overflow checking is disabled.
You can also explicitly control the overflow-checking context for the parts of your code
by using the checked and unchecked statements.
For information about how the overflow-checking context affects operations and what
operations are affected, see the article about checked  and unchecked  statements .
The AllowUnsafeBlocks  compiler option allows code that uses the unsafe  keyword to
compile. The default value for this option is false, meaning unsafe code isn't allowed.
XMLCheckForOverflowUnderflow
<CheckForOverflowUnderflow >true</CheckForOverflowUnderflow >
AllowUnsafeBlocksFor more information about unsafe code, see Unsafe Code and P ointers .
The DefineConstants  option defines symbols in all source code files of your program.
XML
This option specifies the names of one or more symbols that you want to define. The
DefineConstants  option has the same effect as the #define  preprocessor directive
except that the compiler option is in effect for all files in the project. A symbol remains
defined in a source file until an #undef  directive in the source file removes the definition.
When you use the -define option, an #undef directive in one file has no effect on other
source code files in the project. Y ou can use symbols created by this option with #if,
#else , #elif, and #endif  to compile source files conditionally. The C# compiler itself
defines no symbols or macros that you can use in your source code; all symbol
definitions must be user-defined.
The default language version for the C# compiler depends on the target framework for
your application and the version of the SDK or Visual S tudio installed. Those rules are
defined in C# language versioning .
The LangV ersion option causes the compiler to accept only syntax that is included in the
specified C# language specification, for example:<AllowUnsafeBlocks >true</AllowUnsafeBlocks >
DefineConstants
<DefineConstants >name;name2 </DefineConstants >
７ Note
The C# #define directive does not allow a symbol to be given a value, as in
languages such as C++. For example, #define cannot be used to create a macro or
to define a constant. If you need to define a constant, use an enum variable. If you
want to create a C++ style macro, consider alternatives such as generics. Since
macros are notoriously error-prone, C# disallows their use but provides safer
alternatives.
LangVersionXML
The following values are valid:
Value Meaning
preview The compiler accepts all valid language syntax from the latest preview version.
latest The compiler accepts syntax from the latest released version of the compiler
(including minor version).
latestMajor
or defaultThe compiler accepts syntax from the latest released major version of the compiler.
12.0 The compiler accepts only syntax that is included in C# 12 or lower.
11.0 The compiler accepts only syntax that is included in C# 11 or lower.
10.0 The compiler accepts only syntax that is included in C# 10 or lower.
9.0 The compiler accepts only syntax that is included in C# 9 or lower.
8.0 The compiler accepts only syntax that is included in C# 8.0 or lower.
7.3 The compiler accepts only syntax that is included in C# 7.3 or lower.
7.2 The compiler accepts only syntax that is included in C# 7.2 or lower.
7.1 The compiler accepts only syntax that is included in C# 7.1 or lower.
7 The compiler accepts only syntax that is included in C# 7.0 or lower.
6 The compiler accepts only syntax that is included in C# 6.0 or lower.
5 The compiler accepts only syntax that is included in C# 5.0 or lower.
4 The compiler accepts only syntax that is included in C# 4.0 or lower.
3 The compiler accepts only syntax that is included in C# 3.0 or lower.
ISO-2
or 2The compiler accepts only syntax that is included in ISO/IEC 23270:2006 C# (2.0).
ISO-1
or 1The compiler accepts only syntax that is included in ISO/IEC 23270:2003 C#
(1.0/1.2).<LangVersion >9.0</LangVersion >
ﾉExpand tableTo ensure that your project uses the default compiler version recommended for
your target framework, don't use the LangV ersion option. Y ou can update the
target framework to access newer language features.
Specifying LangV ersion with the default value is different from omitting the
LangV ersion option. Specifying default uses the latest version of the language
that the compiler supports, without taking into account the target framework. For
example, building a project that targets .NET 6 from Visual S tudio version 17.6 uses
C# 10 if LangV ersion isn't specified, but uses C# 11 if LangV ersion is set to
default.
Metadata referenced by your C# application isn't subject to the LangV ersion
compiler option.
Because each version of the C# compiler contains extensions to the language
specification, LangV ersion doesn't give you the equivalent functionality of an
earlier version of the compiler.
While C# version updates generally coincide with major .NET releases, the new
syntax and features aren't necessarily tied to that specific framework version. Each
specific feature has its own minimum .NET API or common language runtime
requirements that may allow it to run on downlevel frameworks by including
NuGet packages or other libraries.
Regardless of which LangV ersion setting you use, use the current version of the
common language runtime to create your .exe or .dll. One exception is friend
assemblies and ModuleAssemblyName , which work under -langv ersion:ISO-1 .
For other ways to specify the C# language version, see C# language versioning .
For information about how to set this compiler option programmatically, see
LanguageV ersion .） Impor tant
The latest value is generally not recommended. With latest, the compiler
enables the latest features, even if those features depend on updates not included
in the configured target framework.
ConsiderationsVersion Link Descr iption
C# 8.0 and
laterdownload PDF C# Language Specification V ersion 7: .NET Foundation
C# 7.3 download PDF Standard ECMA-334 7th Edition
C# 6.0 download PDF Standard ECMA-334 6th Edition
C# 5.0 Download PDF Standard ECMA-334 5th Edition
C# 3.0 Download DOC C# Language Specification V ersion 3.0: Microsoft
Corporation
C# 2.0 Download PDF Standard ECMA-334 4th Edition
C# 1.2 Download DOC Standard ECMA-334 2nd Edition
C# 1.0 Download DOC Standard ECMA-334 1st Edition
The following table lists the minimum versions of the SDK with the C# compiler that
supports the corresponding language version:
C#
versionMinimum SDK v ersion
C# 12 Microsoft Visual S tudio/Build T ools 2022 version 17.8, or .NET 8 SDK
C# 11 Microsoft Visual S tudio/Build T ools 2022 version 17.4, or .NET 7 SDK
C# 10 Microsoft Visual S tudio/Build T ools 2022, or .NET 6 SDK
C# 9.0 Microsoft Visual S tudio/Build T ools 2019 version 16.8, or .NET 5 SDK
C# 8.0 Microsoft Visual S tudio/Build T ools 2019, version 16.3, or .NET Core 3.0 SDK
C# 7.3 Microsoft Visual S tudio/Build T ools 2017, version 15.7
C# 7.2 Microsoft Visual S tudio/Build T ools 2017, version 15.5C# language specification
ﾉExpand table
Minimum SDK version needed to support all language
features
ﾉExpand tableC#
versionMinimum SDK v ersion
C# 7.1 Microsoft Visual S tudio/Build T ools 2017, version 15.3
C# 7.0 Microsoft Visual S tudio/Build T ools 2017
C# 6 Microsoft Visual S tudio/Build T ools 2015
C# 5 Microsoft Visual S tudio/Build T ools 2012 or bundled .NET Framework 4.5 compiler
C# 4 Microsoft Visual S tudio/Build T ools 2010 or bundled .NET Framework 4.0 compiler
C# 3 Microsoft Visual S tudio/Build T ools 2008 or bundled .NET Framework 3.5 compiler
C# 2 Microsoft Visual S tudio/Build T ools 2005 or bundled .NET Framework 2.0 compiler
C# 1.0/1.2 Microsoft Visual S tudio/Build T ools .NET 2002 or bundled .NET Framework 1.0
compiler
The Nullable  option lets you specify the nullable context. It can be set in the project's
configuration using the <Nullable> tag:
XML
The argument must be one of enable, disable, warnings, or annotations. The enable
argument enables the nullable context. Specifying disable will disable the nullable
context. When you specify the warnings argument, the nullable warning context is
enabled. When you specify the annotations argument, the nullable annotation context
is enabled. The values are described and explained in the article on Nullable contexts .
You can learn more about the tasks involved in enabling nullable reference types in an
existing codebase in our article on nullable migration strategies .
Flow analysis is used to infer the nullability of variables within executable code. The
inferred nullability of a variable is independent of the variable's declared nullability.Nullable
<Nullable >enable</Nullable >
７ Note
When there's no value set, the default value disable is applied, however the .NET 6
templates are by default provided with the Nullable  value set to enable.Method calls are analyzed even when they're conditionally omitted. For instance,
Debug.Assert  in release mode.
Invocation of methods annotated with the following attributes will also affect flow
analysis:
Simple pre-conditions: AllowNullAttribute  and DisallowNullAttribute
Simple post-conditions: MaybeNullAttribute  and NotNullAttribute
Conditional post-conditions: MaybeNullWhenAttribute  and NotNullWhenAttribute
DoesNotR eturnIfAttribute  (for example, DoesNotReturnIf(false) for Debug.Assert )
and DoesNotR eturnAttribute
NotNullIfNotNullAttribute
Member post-conditions: MemberNotNullAttribute(S tring)  and
MemberNotNullAttribute(S tring[])
） Impor tant
The global nullable context does not apply for generated code files. R egardless of
this setting, the nullable context is disabled  for any source file marked as generated.
There are four ways a file is marked as generated:
1. In the .editorconfig, specify generated_code = true in a section that applies to
that file.
2. Put <auto-generated> or <auto-generated/> in a comment at the top of the
file. It can be on any line in that comment, but the comment block must be
the first element in the file.
3. Start the file name with Tempor aryGener atedFile_
4. End the file name with .designer .cs, .gener ated.cs , .g.cs, or .g.i.cs .
Generators can opt-in using the #nullable  preprocessor directive.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For.NET feedb ack
.NET is an open source project.
Select a link to provide feedback:
 Open a documentation issue
 Provide product feedbackmore information, see our
contributor guide .C# Compiler Options that control
compiler output
Article •07/12/2022
The following options control compiler output generation.
MSBuild cs c.ex e Descr iption
DocumentationFile -doc: Generate XML doc file from /// comments.
OutputAssembly -out: Specify the output assembly file.
PlatformT arget -platform: Specify the target platform CPU.
ProduceR eferenceAssembly -refout: Generate a reference assembly.
TargetType -target: Specify the type of the output assembly.
The DocumentationFile  option allows you to place documentation comments in an XML
file. T o learn more about documenting your code, see Recommended T ags for
Documentation Comments . The value specifies the path to the output XML file. The XML
file contains the comments in the source code files of the compilation.
XML
The source code file that contains Main or top-level statements is output first into the
XML. Y ou'll often want to use the generated .xml file with IntelliSense . The .xml filename
must be the same as the assembly name. The .xml file must be in the same directory as
the assembly. When the assembly is referenced in a Visual S tudio project, the .xml file is
found as well. For more information about generating code comments, see Supplying
Code Comments . Unless you compile with <TargetT ype:Module> , file will contain
<assembly> and </assembly> tags specifying the name of the file containing the
assembly manifest for the output file. For examples, see How to use the XML
documentation features .DocumentationFile
<DocumentationFile >path/to/file.xml </DocumentationFile > 
７ NoteThis option can be used in any .NET SDK-style project. For more information, see
DocumentationFile property .
The OutputAssembly  option specifies the name of the output file. The output path
specifies the folder where compiler output is placed.
XML
Specify the full name and extension of the file you want to create. If you don't specify
the name of the output file, MSBuild uses the name of the project to specify the name
of the output assembly. Old style projects use the following rules:
An .exe will take its name from the source code file that contains the Main method
or top-level statements.
A .dll or .netmodule will take its name from the first source code file.
Any modules produced as part of a compilation become files associated with any
assembly also produced in the compilation. Use ildasm.exe  to view the assembly
manifest to see the associated files.
The OutputAssembly  compiler option is required in order for an exe to be the target of
a friend assembly .
Specifies which version of the CLR can run the assembly.
XML
anycpu (default) compiles your assembly to run on any platform. Y our application
runs as a 64-bit process whenever possible and falls back to 32-bit when only thatThe DocumentationFile  option applies to all files in the project. T o disable warnings
related to documentation comments for a specific file or section of code, use
#pragma warning .
OutputAssembly
<OutputAssembly >folder</OutputAssembly > 
PlatformTarget
<PlatformTarget >anycpu</PlatformTarget > mode is available.
anycpu32bitpr eferr ed compiles your assembly to run on any platform. Y our
application runs in 32-bit mode on systems that support both 64-bit and 32-bit
applications. Y ou can specify this option only for projects that target .NET
Framework 4.5 or later.
ARM  compiles your assembly to run on a computer that has an Advanced RISC
Machine (ARM) processor.
ARM64  compiles your assembly to run by the 64-bit CLR on a computer that has
an Advanced RISC Machine (ARM) processor that supports the A64 instruction set.
x64 compiles your assembly to be run by the 64-bit CLR on a computer that
supports the AMD64 or EM64T instruction set.
x86 compiles your assembly to be run by the 32-bit, x86-compatible CLR.
Itanium  compiles your assembly to be run by the 64-bit CLR on a computer with
an Itanium processor.
On a 64-bit Windows operating system:
Assemblies compiled with x86 execute on the 32-bit CLR running under WO W64.
A DLL compiled with the anycpu executes on the same CLR as the process into
which it's loaded.
Executables that are compiled with the anycpu execute on the 64-bit CLR.
Executables compiled with anycpu32bitpr eferr ed execute on the 32-bit CLR.
The anycpu32bitpr eferr ed setting is valid only for executable (.EXE) files, and it requires
.NET Framework 4.5 or later. For more information about developing an application to
run on a Windows 64-bit operating system, see 64-bit Applications .
You set the PlatformT arget option from Build  properties page for your project in Visual
Studio.
The behavior of anycpu has some additional nuances on .NET Core and .NET 5 and later
releases. When you set anycpu, publish your app and execute it with either the x86
dotnet.exe or the x64 dotnet.exe. For self-contained apps, the dotnet publish step
packages the executable for the configure RID.
The ProduceR eferenceAssembly  option controls whether the compiler produces
reference assemblies.
XMLProduceReferenceAssembly
<ProduceReferenceAssembly >true</ProduceReferenceAssembly > Reference assemblies are a special type of assembly that contain only the minimum
amount of metadata required to represent the library's public API surface. They include
declarations for all members that are significant when referencing an assembly in build
tools. R eference assemblies exclude all member implementations and declarations of
private members. Those members have no observable impact on their API contract. For
more information, see Reference assemblies  in the .NET Guide.
The ProduceR eferenceAssembly  and ProduceOnlyR eferenceAssembly  options are
mutually exclusive.
You generally don't need to work directly with reference assembly files. By default,
reference assemblies are generated in a ref subfolder of the intermediate path (i.e.
obj/ref/). To generate them under the output directory instead (i.e. bin/ref/) set
ProduceReferenceAssemblyInOutDir to true in your project.
.NET SDK 6.0.200 made a change  that moved reference assemblies from the output
directory to the intermediate directory by default.
The TargetType compiler option can be specified in one of the following forms:
librar y: to create a code library. librar y is the default value.
exe: to create an .exe file.
module  to create a module.
winex e to create a Windows program.
winmdobj  to create an intermediate .winmdobj  file.
appcontainer exe to create an .exe file for Windows 8.x S tore apps.
XMLTargetType
７ Note
For .NET Framework targets, unless you specify module , this option causes a .NET
Framework assembly manifest to be placed in an output file. For more information,
see Assemblies in .NE T and Common A ttribut es.
<TargetType >library</TargetType > The compiler creates only one assembly manifest per compilation. Information about all
files in a compilation is placed in the assembly manifest. When producing multiple
output files at the command line, only one assembly manifest can be created and it
must go into the first output file specified on the command line.
If you create an assembly, you can indicate that all or part of your code is CLS-compliant
with the CLSCompliantAttribute  attribute.
The librar y option causes the compiler to create a dynamic-link library (DLL) rather than
an executable file (EXE). The DLL will be created with the .dll extension. Unless otherwise
specified with the OutputAssembly  option, the output file name takes the name of the
first input file. When building a .dll file, a Main  method isn't required.
The exe option causes the compiler to create an executable (EXE), console application.
The executable file will be created with the .exe extension. Use winex e to create a
Windows program executable. Unless otherwise specified with the OutputAssembly
option, the output file name takes the name of the input file that contains the entry
point ( Main  method or top-level statements). One and only one entry point is required
in the source code files that are compiled into an .exe file. The StartupObject  compiler
option lets you specify which class contains the Main method, in cases where your code
has more than one class with a Main method.
This option causes the compiler to not generate an assembly manifest. By default, the
output file created by compiling with this option will have an extension of .netmodule . A
file that doesn't have an assembly manifest cannot be loaded by the .NET runtime.
However, such a file can be incorporated into the assembly manifest of an assembly
with AddModules . If more than one module is created in a single compilation, internal
types in one module will be available to other modules in the compilation. When code
in one module references internal types in another module, then both modules must
be incorporated into an assembly manifest, with AddModules . Creating a module isn't
supported in the Visual S tudio development environment.library
exe
module
winexeThe winex e option causes the compiler to create an executable (EXE), Windows
program. The executable file will be created with the .exe extension. A Windows
program is one that provides a user interface from either the .NET library or with the
Windows APIs. Use exe to create a console application. Unless otherwise specified with
the OutputAssembly  option, the output file name takes the name of the input file that
contains the Main  method. One and only one Main method is required in the source
code files that are compiled into an .exe file. The StartupObject  option lets you specify
which class contains the Main method, in cases where your code has more than one
class with a Main method.
If you use the winmdobj  option, the compiler creates an intermediate .winmdobj  file
that you can convert to a Windows Runtime binary ( .winmd ) file. The .winmd  file can
then be consumed by JavaScript and C++ programs, in addition to managed language
programs.
The winmdobj  setting signals to the compiler that an intermediate module is required.
The .winmdobj  file can then be fed through the WinMDExp  export tool to produce a
Windows metadata ( .winmd ) file. The .winmd  file contains both the code from the
original library and the WinMD metadata that is used by JavaScript or C++ and by the
Windows Runtime. The output of a file that’s compiled by using the winmdobj  compiler
option is used only as input for the WimMDExp export tool. The .winmdobj  file itself isn’t
referenced directly. Unless you use the OutputAssembly  option, the output file name
takes the name of the first input file. A Main  method isn’t required.
If you use the appcontainer exe compiler option, the compiler creates a Windows
executable ( .exe) file that must be run in an app container. This option is equivalent to -
target:winexe  but is designed for Windows 8.x S tore apps.
To require the app to run in an app container, this option sets a bit in the Portable
Executable  (PE) file. When that bit is set, an error occurs if the CreateProcess method
tries to launch the executable file outside an app container. Unless you use the
OutputAssembly  option, the output file name takes the name of the input file that
contains the Main  method.winmdobj
appcontainerexeC# Compiler Options that specify inputs
Article •09/15/2021
The following options control compiler inputs. The new MSBuild syntax is shown in Bold .
The older csc.exe syntax is shown in code style.
References  / -reference or -references: Reference metadata from the specified
assembly file or files.
AddModules  / -addmodule: Add a module (created with target:module to this
assembly.)
EmbedInt eropTypes  / -link: Embed metadata from the specified interop
assembly files.
The References  option causes the compiler to import public  type information in the
specified file into the current project, enabling you to reference metadata from the
specified assembly files.
XML
filename is the name of a file that contains an assembly manifest. T o import more than
one file, include a separate Reference  element for each file. Y ou can define an alias as a
child element of the Reference  element:
XML
In the previous example, LS is the valid C# identifier that represents a root namespace
that will contain all namespaces in the assembly filename.dll . The files you import must
contain a manifest. Use AdditionalLibP aths to specify the directory in which one or
more of your assembly references is located. The AdditionalLibP aths topic also
discusses the directories in which the compiler searches for assemblies. In order for the
compiler to recognize a type in an assembly, and not in a module, it needs to be forced
to resolve the type, which you can do by defining an instance of the type. There areReferences
<Reference  Include="filename"  /> 
<Reference  Include="filename.dll" > 
  <Aliases>LS</Aliases> 
</Reference > other ways to resolve type names in an assembly for the compiler: for example, if you
inherit from a type in an assembly, the type name will then be recognized by the
compiler. Sometimes it is necessary to reference two different versions of the same
component from within one assembly. T o do this, use the Aliases  element on the
References  element for each file to distinguish between the two files. This alias will be
used as a qualifier for the component name, and will resolve to the component in one of
the files.
This option adds a module that was created with the <TargetType>module</TargetType>
switch to the current compilation:
XML
Where file, file2 are output files that contain metadata. The file can't contain an
assembly manifest. T o import more than one file, separate file names with either a
comma or a semicolon. All modules added with AddModules  must be in the same
directory as the output file at run time. That is, you can specify a module in any directory
at compile time but the module must be in the application directory at run time. If the
module isn't in the application directory at run time, you'll get a TypeLoadException .
file can't contain an assembly. For example, if the output file was created with
TargetType option of module , its metadata can be imported with AddModules .
If the output file was created with a TargetType option other than module , its metadata
cannot be imported with AddModules  but can be imported with the References  option.
Causes the compiler to make C OM type information in the specified assemblies
available to the project that you are currently compiling.７ Note
In Visual S tudio, use the Add R eference  command. For more information, see How
to: Add or R emov e References By Using the R eference Manager .
AddModules
<AddModule  Include=file1 /> 
<AddModule  Include=file2 /> 
EmbedInteropTypesXML
Where file1;file2;file3 is a semicolon-delimited list of assembly file names. If the file
name contains a space, enclose the name in quotation marks. The EmbedInt eropTypes
option enables you to deploy an application that has embedded type information. The
application can then use types in a runtime assembly that implement the embedded
type information without requiring a reference to the runtime assembly. If various
versions of the runtime assembly are published, the application that contains the
embedded type information can work with the various versions without having to be
recompiled. For an example, see Walkthrough: Embedding T ypes from Managed
Assemblies .
Using the EmbedInt eropTypes  option is especially useful when you're working with
COM interop. Y ou can embed C OM types so that your application no longer requires a
primary interop assembly (PIA) on the target computer. The EmbedInt eropTypes  option
instructs the compiler to embed the C OM type information from the referenced interop
assembly into the resulting compiled code. The C OM type is identified by the CLSID
(GUID) value. As a result, your application can run on a target computer that has
installed the same C OM types with the same CLSID values. Applications that automate
Microsoft Office are a good example. Because applications like Office usually keep the
same CLSID value across different versions, your application can use the referenced
COM types as long as .NET Framework 4 or later is installed on the target computer and
your application uses methods, properties, or events that are included in the referenced
COM types. The EmbedInt eropTypes  option embeds only interfaces, structures, and
delegates. Embedding C OM classes isn't supported.
Like the References  compiler option, the EmbedInt eropTypes  compiler option uses the
Csc.rsp response file, which references frequently used .NET assemblies. Use the
NoConfig  compiler option if you don't want the compiler to use the Csc.rsp file.
C#<References > 
  <EmbedInteropTypes >file1;file2;file3 </EmbedInteropTypes > 
</References > 
７ Note
When you create an instance of an embedded C OM type in your code, you must
create the instance by using the appropriate interface. Attempting to create an
instance of an embedded C OM type by using the CoClass causes an error.Types that have a generic parameter whose type is embedded from an interop assembly
cannot be used if that type is from an external assembly. This restriction doesn't apply to
interfaces. For example, consider the Range  interface that is defined in the
Microsoft.Office.Interop.Excel  assembly. If a library embeds interop types from the
Microsoft.Office.Interop.Excel  assembly and exposes a method that returns a generic
type that has a parameter whose type is the Range  interface, that method must return a
generic interface, as shown in the following code example.
C#
In the following example, client code can call the method that returns the IList generic
interface without error.
C#// The following code causes an error if ISampleInterface is an embedded  
interop type.  
ISampleInterface<SampleType> sample;  
using System;  
using System.Collections.Generic;
using System.Linq;  
using System.Text;  
using Microsoft.Office.Interop.Excel;  
public class Utility 
{ 
    // The following code causes an error when called by a client assembly.  
    public List<Range> GetRange1 () 
    { 
        return null; 
    } 
    // The following code is valid for calls from a client assembly.  
    public IList<Range> GetRange2 () 
    { 
        return null; 
    } 
} 
public class Client 
{ 
    public void Main() 
    { 
        Utility util = new Utility();  
        // The following code causes an error.  
        List<Range> rangeList1 = util.GetRange1();          // The following code is valid.  
        List<Range> rangeList2 = (List<Range>)util.GetRange2();  
    } 
} C# Compiler Options to report errors
and warnings
Article •11/01/2023
The following options control how the compiler reports errors and warnings. The new
MSBuild syntax is shown in Bold . The older csc.exe syntax is shown in code style.
WarningLev el / -warn: Set warning level.
AnalysisLev el: Set optional warning level.
TreatW arningsAsErr ors / -warnaserror: Treat all warnings as errors
WarningsAsErr ors / -warnaserror: Treat one or more warnings as errors
WarningsNotAsErr ors / -warnnotaserror: Treat one or more warnings not as errors
NoW arn / -nowarn: Set a list of disabled warnings.
CodeAnalysisRuleSet  / -ruleset: Specify a ruleset file that disables specific
diagnostics.
ErrorLog  / -errorlog: Specify a file to log all compiler and analyzer diagnostics.
Repor tAnalyzer  / -reportanalyzer: Report additional analyzer information, such as
execution time.
The WarningLev el option specifies the warning level for the compiler to display.
XML
The element value is the warning level you want displayed for the compilation: Lower
numbers show only high severity warnings. Higher numbers show more warnings. The
value must be zero or a positive integer:
Warning
levelMeaning
0 Turns off emission of all warning messages.
1 Displays severe warning messages.
2 Displays level 1 warnings plus certain, less-severe warnings, such as warnings about
hiding class members.WarningLevel
<WarningLevel >3</WarningLevel >Warning
levelMeaning
3 Displays level 2 warnings plus certain, less-severe warnings, such as warnings about
expressions that always evaluate to true or false.
4 (default) Displays all level 3 warnings plus informational warnings.
To get information about an error or warning, you can look up the error code in the
Help Index . For other ways to get information about an error or warning, see C#
Compiler Errors . Use TreatW arningsAsErr ors to treat all warnings as errors. Use
DisabledW arnings  to disable certain warnings.
The AnalysisLev el option specifies additional warning waves  and analyzers to enable.
Warning wave warnings are additional checks that improve your code, or ensure it will
be compatible with upcoming releases. Analyzers provide lint-like capability to improve
your code.
XML
Analysis lev elMeaning
5 Displays all optional warning wave 5 warnings .
6 Displays all optional warning wave 6 warnings .
7 Displays all optional warning wave 7 warnings .
latest
(default)Displays all informational warnings up to and including the current release.
preview Displays all informational warnings up to and including the latest preview
release.２ Warning
The compiler command line accepts values greater than 4 to enable warning wav e
warnings . However, the .NET SDK sets the WarningL evel to match the AnalysisL evel
in your project file.
Analysis level
<AnalysisLevel >preview</AnalysisLevel >Analysis lev elMeaning
none Turns off all informational warnings.
For more information on optional warnings, see Warning waves .
To get information about an error or warning, you can look up the error code in the
Help Index. For other ways to get information about an error or warning, see C#
Compiler Errors . Use TreatW arningsAsErr ors to treat all warnings as errors. Use NoW arn
to disable certain warnings.
The TreatW arningsAsErr ors option treats all warnings as errors. Y ou can also use the
TreatW arningsAsErr ors to set only some warnings as errors. If you turn on
TreatW arningsAsErr ors, you can use WarningsNotAsErr ors to list warnings that
shouldn't be treated as errors.
XML
All warning messages are instead reported as errors. The build process halts (no output
files are built). By default, TreatW arningsAsErr ors isn't in effect, which means warnings
don't prevent the generation of an output file. Optionally, if you want only a few specific
warnings to be treated as errors, you may specify a comma-separated list of warning
numbers to treat as errors. The set of all nullability warnings can be specified with the
Nullable  shorthand. Use WarningLev el to specify the level of warnings that you want
the compiler to display. Use NoW arn to disable certain warnings.TreatWarningsAsErrors
<TreatWarningsAsErrors >true</TreatWarningsAsErrors >
） Impor tant
There are two subtle differences between using the <TreatWarningsAsErrors>
element in your csproj file, and using the warnaserror MSBuild command line
switch. TreatW arningsAsErr ors only impacts the C# compiler, not any other MSBuild
tasks in your csproj file. The warnaserror command line switch impacts all tasks.
Secondly, the compiler doesn't produce any output on any warnings when
TreatW arningsAsErr ors is used. The compiler produces output when the
warnaserror command line switch is used.The WarningsAsErr ors and WarningsNotAsErr ors options override the
TreatW arningsAsErr ors option for a list of warnings. This option can be used with all CS
warnings. The "CS" prefix is optional. Y ou can use either the number, or "CS" followed by
the error or warning number. For other elements that affect warnings, see the Common
MSBuild properties .
Enable warnings 0219 and 0168 as errors:
XML
Disable the same warnings as errors:
XML
You use WarningsAsErr ors to configure a set of warnings as errors. Use
WarningsNotAsErr ors to configure a set of warnings that should not be errors when
you've set all warnings as errors.
The NoW arn option lets you suppress the compiler from displaying one or more
warnings, where warningnumber1, warningnumber2 are warning numbers that you want
the compiler to suppress. Separate multiple warning numbers with a comma.
XML
You need to specify only the numeric part of the warning identifier. For example, if you
want to suppress CS0028 , you could specify <NoWarn>28</NoWarn>. The compiler silently
ignores warning numbers passed to NoW arn that were valid in previous releases, but
that have been removed. For example, CS0679  was valid in the compiler in Visual S tudio
.NET 2002 but was removed later.
The following warnings can't be suppressed by the NoW arn option:WarningsAsErrors and WarningsNotAsErrors
<WarningsAsErrors >0219,CS0168 </WarningsAsErrors >
<WarningsNotAsErrors >0219,CS0168 </WarningsNotAsErrors >
NoWarn
<NoWarn>warningnumber1,warningnumber2 </NoWarn>Compiler W arning (level 1) CS2002
Compiler W arning (level 1) CS2023
Compiler W arning (level 1) CS2029
Note that warnings are intended to be an indication of a potential problem with your
code, so you should understand the risks of disabling any particular warning. Use
NoW arn only when you're certain that a warning is a false positive and can't possibly be
a runtime bug.
You might want to use a more targeted approach to disabling warnings:
Most compilers provide ways to disable warnings just for certain lines of code, so
that you can still review the warnings if they occur elsewhere in the same project.
To suppress a warning only in a specific part of the code in C#, use #pragma
warning .
If your goal is to see more concise and focused output in your build log, you might
want to change the build log verbosity. For more information, see How to: View,
save, and configure build log files .
To add warning numbers to any previously set value for NoW arn without overwriting it,
reference $(NoWarn) as shown in the following example:
XML
Specify a ruleset file that configures specific diagnostics.
XML
Where MyConfiguration.ruleset is the path to the ruleset file. For more information on
using rule sets, see the article in the Visual S tudio documentation on Rule sets .
Specify a file to log all compiler and analyzer diagnostics.   <NoWarn>$(NoWarn);newwarningnumber3;newwarningnumber4 </NoWarn>
CodeAnalysisRuleSet
<CodeAnalysisRuleSet >MyConfiguration.ruleset </CodeAnalysisRuleSet >
ErrorLogXML
The ErrorLog  option causes the compiler to output a Static Analysis R esults Interchange
Format (SARIF) log . SARIF logs are typically read by tools that analyze the results from
compiler and analyzer diagnostics.
You can specify the SARIF format using the version argument to the ErrorLog element:
XML
The separator can be either a comma ( ,) or a semicolon ( ;). Valid values for version
are: "1", "2", and "2.1". The default is "1". "2" and "2.1" both mean SARIF version 2.1.0.
Report additional analyzer information, such as execution time.
XML
The Repor tAnalyzer  option causes the compiler to emit extra MSBuild log information
that details the performance characteristics of analyzers in the build. It's typically used
by analyzer authors as part of validating the analyzer.<ErrorLog >compiler-diagnostics.sarif </ErrorLog >
<ErrorLog >logVersion21.json,version=2.1 </ErrorLog >
ReportAna lyzer
<ReportAnalyzer >true</ReportAnalyzer >
） Impor tant
The extra log information generated by this flag is only generated when the -
verbosity:detailed command line option is used. See the switches article in the
MSBuild documentation for more information.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you.NET feedb ack
The .NET documentation is open
source. Provide feedback here.can also create and review
issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackC# Compiler Options that control code
generation
Article •03/09/2023
The following options control code generation by the compiler. The new MSBuild syntax
is shown in Bold . The older csc.exe syntax is shown in code style.
DebugT ype / -debug: Emit (or don't emit) debugging information.
Optimize  / -optimize: Enable optimizations.
Deterministic  / -deterministic: Produce byte-for-byte equivalent output from the
same input source.
ProduceOnlyR eferenceAssembly  / -refonly: Produce a reference assembly,
instead of a full assembly, as the primary output.
The DebugT ype option causes the compiler to generate debugging information and
place it in the output file or files. Debugging information is added by default.
XML
For all compiler versions starting with C# 6.0, there is no difference between pdbonly
and full. Choose pdbonly . To change the location of the .pdb file, see PdbFile .
The following values are valid:
Value Meaning
full Emit debugging information to .pdb file using default format for the current platform:  
Windows : A Windows pdb file.  
Linux/macOS : A Portable PDB  file.
pdbonly Same as full. See the note below for more information.
portableEmit debugging information to .pdb file using cross-platform Portable PDB  format.
embeddedEmit debugging information into the .dll/.ex e itself ( .pdb file is not produced) using
Portable PDB  format.DebugType
<DebugType >pdbonly</DebugType > 
The Optimize  option enables or disables optimizations performed by the compiler to
make your output file smaller, faster, and more efficient. The Optimize  option is enabled
by default for a Releas e build configuration. It is off by default for a Debug  build
configuration.
XML
You set the Optimize  option from Build  properties page for your project in Visual
Studio.
Optimize  also tells the common language runtime to optimize code at run time. By
default, optimizations are disabled. Specify Optimize+  to enable optimizations. When
building a module to be used by an assembly, use the same Optimize  settings as used
by the assembly. It's possible to combine the Optimize  and Debug  options.
Causes the compiler to produce an assembly whose byte-for-byte output is identical
across compilations for identical inputs.） Impor tant
The following information applies only to compilers older than C# 6.0. The value of
this element can be either full or pdbonly. The full argument, which is in effect if
you don't specify pdbonly , enables attaching a debugger to the running program.
Specifying pdbonly  allows source code debugging when the program is started in
the debugger but will only display assembler when the running program is
attached to the debugger. Use this option to create debug builds. If you use Full,
be aware that there's some impact on the speed and size of JIT optimized code and
a small impact on code quality with full. We recommend pdbonly  or no PDB for
generating release code. One difference between pdbonly  and full is that with full
the compiler emits a DebuggableA ttribut e, which is used to tell the JIT compiler
that debug information is available. Therefore, you will get an error if your code
contains the DebuggableA ttribut e set to false if you use full. For more information
on how to configure the debug performance of an application, see Making an
Image Easier t o Debug .
Optimize
<Optimize >true</Optimize > 
DeterministicXML
By default, compiler output from a given set of inputs is unique, since the compiler adds
a timestamp and an MVID (a Module.ModuleV ersionId . Basically it is a GUID that
uniquely identifies the module and version.) that is generated from random numbers.
You use the <Deterministic> option to produce a deterministic ass embly , one whose
binary content is identical across compilations as long as the input remains the same. In
such a build, the timestamp and MVID fields will be replaced with values derived from a
hash of all the compilation inputs. The compiler considers the following inputs that
affect determinism:
The sequence of command-line parameters.
The contents of the compiler's .rsp response file.
The precise version of the compiler used, and its referenced assemblies.
The current directory path.
The binary contents of all files explicitly passed to the compiler either directly or
indirectly, including:
Source files
Referenced assemblies
Referenced modules
Resources
The strong name key file
@ response files
Analyzers
Rulesets
Other files that may be used by analyzers
The current culture (for the language in which diagnostics and exception messages
are produced).
The default encoding (or the current code page) if the encoding isn't specified.
The existence, non-existence, and contents of files on the compiler's search paths
(specified, for example, by -lib or -recurse).
The Common Language Runtime (CLR) platform on which the compiler is run.
The value of %LIBPATH%, which can affect analyzer dependency loading.
Deterministic compilation can be used for establishing whether a binary is compiled
from a trusted source. Deterministic output can be useful when the source is publicly
available. It can also determine whether build steps that are dependent on changes to
binary used in the build process.<Deterministic >true</Deterministic > The ProduceOnlyR eferenceAssembly  option indicates that a reference assembly should
be output instead of an implementation assembly, as the primary output. The
ProduceOnlyR eferenceAssembly  parameter silently disables outputting PDBs, as
reference assemblies cannot be executed.
XML
Reference assemblies are a special type of assembly. R eference assemblies contain only
the minimum amount of metadata required to represent the library's public API surface.
They include declarations for all members that are significant when referencing an
assembly in build tools, but exclude all member implementations and declarations of
private members that have no observable impact on their API contract. For more
information, see Reference assemblies .
The ProduceOnlyR eferenceAssembly  and ProduceR eferenceAssembly  options are
mutually exclusive.ProduceOnlyReferenceAssembly
<ProduceOnlyReferenceAssembly >true</ProduceOnlyReferenceAssembly > C# compiler options for security
Article •09/29/2022
The following options control compiler security options. The new MSBuild syntax is
shown in Bold . The older csc.exe syntax is shown in code style.
PublicSign  / -publicsign: Publicly sign the assembly.
DelaySign  / -delaysign: Delay-sign the assembly using only the public portion of
the strong name key.
KeyFile  / -keyfile : Specify a strong name key file.
KeyContainer  / -keycontainer: Specify a strong name key container.
HighEntr opyV A / -highentropyva: Enable high-entropy Address Space Layout
Randomization (ASLR)
This option causes the compiler to apply a public key but doesn't actually sign the
assembly. The PublicSign  option also sets a bit in the assembly that tells the runtime
that the file is signed.
XML
The PublicSign  option requires the use of the KeyFile  or KeyContainer  option. The
KeyFile  and KeyContainer  options specify the public key. The PublicSign  and DelaySign
options are mutually exclusive. Sometimes called "fake sign" or "OSS sign", public
signing includes the public key in an output assembly and sets the "signed" flag. Public
signing doesn't actually sign the assembly with a private key. Developers use public sign
for open-source projects. People build assemblies that are compatible with the released
"fully signed" assemblies when they don't have access to the private key used to sign
the assemblies. Since few consumers actually need to check if the assembly is fully
signed, these publicly built assemblies are useable in almost every scenario where the
fully signed one would be used.
This option causes the compiler to reserve space in the output file so that a digital
signature can be added later.PublicSign
<PublicSign >true</PublicSign > 
DelaySignXML
Use DelaySign-  if you want a fully signed assembly. Use DelaySign  if you only want to
place the public key in the assembly. The DelaySign  option has no effect unless used
with KeyFile  or KeyContainer . The KeyContainer  and PublicSign  options are mutually
exclusive. When you request a fully signed assembly, the compiler hashes the file that
contains the manifest (assembly metadata) and signs that hash with the private key.
That operation creates a digital signature that is stored in the file that contains the
manifest. When an assembly is delay signed, the compiler doesn't compute and store
the signature. Instead, the compiler but reserves space in the file so the signature can be
added later.
Using DelaySign  allows a tester to put the assembly in the global cache. After testing,
you can fully sign the assembly by placing the private key in the assembly using the
Assembly Linker  utility. For more information, see Creating and Using S trong-Named
Assemblies  and Delay Signing an Assembly .
Specifies the filename containing the cryptographic key.
XML
file is the name of the file containing the strong name key. When this option is used,
the compiler inserts the public key from the specified file into the assembly manifest
and then signs the final assembly with the private key. T o generate a key file, type sn -k
file at the command line. If you compile with -target:module , the name of the key file
is held in the module and incorporated into the assembly created when you compile an
assembly with AddModules . You can also pass your encryption information to the
compiler with KeyContainer . Use DelaySign  if you want a partially signed assembly. In
case both KeyFile  and KeyContainer  are specified in the same compilation, the compiler
will first try the key container. If that succeeds, then the assembly is signed with the
information in the key container. If the compiler doesn't find the key container, it will try
the file specified with KeyFile . If that succeeds, the assembly is signed with the
information in the key file and the key information will be installed in the key container.
On the next compilation, the key container will be valid. A key file might contain only<DelaySign >true</DelaySign > 
KeyFile
<KeyFile>filename </KeyFile> the public key. For more information, see Creating and Using S trong-Named Assemblies
and Delay Signing an Assembly .
Specifies the name of the cryptographic key container.
XML
container is the name of the strong name key container. When the KeyContainer
option is used, the compiler creates a sharable component. The compiler inserts a public
key from the specified container into the assembly manifest and signs the final assembly
with the private key. T o generate a key file, type sn -k file at the command line. sn -i
installs the key pair into a container. This option isn't supported when the compiler runs
on CoreCLR. T o sign an assembly when building on CoreCLR, use the KeyFile  option. If
you compile with TargetType, the name of the key file is held in the module and
incorporated into the assembly when you compile this module into an assembly with
AddModules . You can also specify this option as a custom attribute
(System.R eflection.AssemblyK eyNameAttribute ) in the source code for any Microsoft
intermediate language (MSIL) module. Y ou can also pass your encryption information to
the compiler with KeyFile . Use DelaySign  to add the public key to the assembly manifest
but signing the assembly until it has been tested. For more information, see Creating
and Using S trong-Named Assemblies  and Delay Signing an Assembly .
The HighEntr opyV A compiler option tells the Windows kernel whether a particular
executable supports high entropy Address Space Layout Randomization (ASLR).
XML
This option specifies that a 64-bit executable or an executable that is marked by the
PlatformT arget compiler option supports a high entropy virtual address space. The
option is enabled by default for all .NET S tandard and .NET Core versions, and .NET
Framework versions starting with .NET Framework 4.5.KeyContainer
<KeyContainer >container </KeyContainer > 
HighEntropyVA
<HighEntropyVA >true</HighEntropyVA > The HighEntr opyV A option enables compatible versions of the Windows kernel to use
higher degrees of entropy when randomizing the address space layout of a process as
part of ASLR. Using higher degrees of entropy means a larger number of addresses can
be allocated to memory regions such as stacks and heaps. As a result, it's more difficult
to guess the location of a particular memory region. The HighEntr opyV A compiler
option requires the target executable and any modules that it depends on can handle
pointer values larger than 4 gigabytes (GB) when they're running as a 64-bit process.C# Compiler Options that specify
resources
Article •09/15/2021
The following options control how the C# compiler creates or imports Win32 resources.
The new MSBuild syntax is shown in Bold . The older csc.exe syntax is shown in code
style.
Win32R esour ce / -win32res: Specify a Win32 resource file (.res).
Win32Icon  / -win32icon: Reference metadata from the specified assembly file or
files.
Win32Manifest  / -win32manifest: Specify a Win32 manifest file (.xml).
NoWin32Manifest  / -nowin32manifest: Don't include the default Win32 manifest.
Resour ces / -resource: Embed the specified resource (Short form: /res).
LinkR esour ces / -linkresources: Link the specified resource to this assembly.
The Win32R esour ce option inserts a Win32 resource in the output file.
XML
filename is the resource file that you want to add to your output file. A Win32 resource
can contain version or bitmap (icon) information that would help identify your
application in the File Explorer. If you don't specify this option, the compiler will
generate version information based on the assembly version.
The Win32Icon  option inserts an .ico file in the output file, which gives the output file
the desired appearance in the File Explorer.
XMLWin32Resource
<Win32Resource >filename </Win32Resource > 
Win32Icon
<Win32Icon >filename </Win32Icon > filename is the .ico file that you want to add to your output file. An .ico file can be
created with the Resource Compiler . The R esource Compiler is invoked when you
compile a Visual C++ program; an .ico file is created from the .rc file.
Use the Win32Manifest  option to specify a user-defined Win32 application manifest file
to be embedded into a project's portable executable (PE) file.
XML
filename is the name and location of the custom manifest file. By default, the C#
compiler embeds an application manifest that specifies a requested execution level of
"asInvoker". It creates the manifest in the same folder in which the executable is built. If
you want to supply a custom manifest, for example to specify a requested execution
level of "highestA vailable" or "requireAdministrator," use this option to specify the name
of the file.
An application that has no application manifest that specifies a requested execution
level will be subject to file and registry virtualization under the User Account Control
feature in Windows. For more information, see User Account Control .
Your application will be subject to virtualization if either of these conditions is true:
You use the NoWin32Manifest  option and you don't provide a manifest in a later
build step or as part of a Windows R esource ( .res) file by using the Win32R esour ce
option.
You provide a custom manifest that doesn't specify a requested execution level.
Visual S tudio creates a default .mani fest file and stores it in the debug and release
directories alongside the executable file. Y ou can add a custom manifest by creating one
in any text editor and then adding the file to the project. Or, you can right-click the
Project  icon in Solution Explor er, select Add New It em, and then select Application
Manifest File . After you've added your new or existing manifest file, it will appear in theWin32Manifest
<Win32Manifest >filename </Win32Manifest > 
７ Note
This option and the Win32R esour ces option are mutually exclusive. If you try to use
both options in the same command line you will get a build error.Manifest  drop down list. For more information, see Application P age, Project Designer
(C#).
You can provide the application manifest as a custom post-build step or as part of a
Win32 resource file by using the NoWin32Manifest  option. Use that same option if you
want your application to be subject to file or registry virtualization on Windows Vista.
Use the NoWin32Manifest  option to instruct the compiler not to embed any application
manifest into the executable file.
XML
When this option is used, the application will be subject to virtualization on Windows
Vista unless you provide an application manifest in a Win32 R esource file or during a
later build step.
In Visual S tudio, set this option in the Application Pr oper ty page by selecting the Create
Application Without a Manifest  option in the Manifest  drop down list. For more
information, see Application P age, Project Designer (C#) .
Embeds the specified resource into the output file.
XML
filename is the .NET resource file that you want to embed in the output file. identifier
(optional) is the logical name for the resource; the name that is used to load the
resource. The default is the name of the file. accessibility-modifier (optional) is the
accessibility of the resource: public or private. The default is public. By default, resources
are public in the assembly when they're created by using the C# compiler. T o make the
resources private, specify private as the accessibility modifier. No other accessibility
other than public or private is allowed. If filename is a .NET resource file created, forNoWin32Manifest
<NoWin32Manifest  /> 
Resources
<Resources  Include=filename > 
  <LogicalName >identifier </LogicalName > 
  <Access>accessibility-modifier </Access> 
</Resources > example, by Resgen.exe  or in the development environment, it can be accessed with
members in the System.R esources  namespace. For more information, see
System.R esources.R esourceManager . For all other resources, use the
GetManifestResource methods in the Assembly  class to access the resource at run time.
The order of the resources in the output file is determined from the order specified in
the project file.
Creates a link to a .NET resource in the output file. The resource file isn't added to the
output file. LinkR esour ces differs from the Resour ce option, which does embed a
resource file in the output file.
XML
filename is the .NET resource file to which you want to link from the assembly.
identifier (optional) is the logical name for the resource; the name that is used to load
the resource. The default is the name of the file. accessibility-modifier (optional) is
the accessibility of the resource: public or private. The default is public. By default, linked
resources are public in the assembly when they're created with the C# compiler. T o
make the resources private, specify private as the accessibility modifier. No other
modifier other than public or private is allowed. If filename is a .NET resource file
created, for example, by Resgen.exe  or in the development environment, it can be
accessed with members in the System.R esources  namespace. For more information, see
System.R esources.R esourceManager . For all other resources, use the
GetManifestResource methods in the Assembly  class to access the resource at run time.
The file specified in filename can be any format. For example, you may want to make a
native DLL part of the assembly, so that it can be installed into the global assembly
cache and accessed from managed code in the assembly. Y ou can do the same thing in
the Assembly Linker. For more information, see Al.exe (Assembly Linker)  and Working
with Assemblies and the Global Assembly Cache .LinkResources
<LinkResources  Include=filename > 
  <LogicalName >identifier </LogicalName > 
  <Access>accessibility-modifier </Access> 
</LinkResources > Miscellaneous C# Compiler Options
Article •01/18/2023
The following options control miscellaneous compiler behavior. The new MSBuild syntax
is shown in Bold . The older csc.exe command-line syntax is shown in code style.
ResponseFiles  / @CustomOpts.RSP : Read the specified response file for more
options.
NoLogo  / -nologo : Suppress compiler copyright message.
NoConfig  / -noconfig : Don't auto include CSC.RSP  file.
The ResponseFiles  option lets you specify a file that contains compiler options and
source code files to compile.
XML
The response_file specifies the file that lists compiler options or source code files to
compile. The compiler options and source code files will be processed by the compiler
as if they had been specified on the command line. T o specify more than one response
file in a compilation, specify multiple response file options. In a response file, multiple
compiler options and source code files can appear on one line. A single compiler option
specification must appear on one line (can't span multiple lines). R esponse files can have
comments that begin with the # symbol. Specifying compiler options from within a
response file is just like issuing those commands on the command line. The compiler
processes the command options as they're read. Command-line arguments can override
previously listed options in response files. Conversely, options in a response file will
override options listed previously on the command line or in other response files. C#
provides the csc.rsp file, which is located in the same directory as the csc.exe file. For
more information about the response file format, see NoConfig . This compiler option
cannot be set in the Visual S tudio development environment, nor can it be changed
programmatically. The following are a few lines from a sample response file:
ConsoleResponseFiles
<ResponseFiles >response_file </ResponseFiles > 
# build the first output file  
-target:exe -out:MyExe.exe source1.cs source2.cs  The NoLogo  option suppresses display of the sign-on banner when the compiler starts
up and display of informational messages during compiling.
XML
The NoConfig  option tells the compiler not to compile with the csc.rsp file.
XML
The csc.rsp file references all the assemblies shipped with .NET Framework. The actual
references that the Visual S tudio .NET development environment includes depend on
the project type. Y ou can modify the csc.rsp file and specify additional compiler options
that should be included in every compilation. If you don't want the compiler to look for
and use the settings in the csc.rsp file, specify NoConfig . This compiler option is
unavailable in Visual S tudio and cannot be changed programmatically.NoLogo
<NoLogo>true</NoLogo> 
NoConfig
<NoConfig >true</NoConfig > Advanced C# compiler options
Article •07/19/2023
The following options support advanced scenarios. The new MSBuild syntax is shown in
Bold . The older csc.exe syntax is shown in code style.
MainEntr yPoint, StartupObject  / -main: Specify the type that contains the entry
point.
PdbFile  / -pdb: Specify debug information file name.
PathMap  / -pathmap: Specify a mapping for source path names output by the
compiler.
ApplicationConfiguration  / -appconfig: Specify an application configuration file
containing assembly binding settings.
AdditionalLibP aths / -lib: Specify additional directories to search in for
references.
Generat eFullP aths / -fullpath: Compiler generates fully qualified paths.
Preferr edUILang  / -preferreduilang: Specify the preferred output language name.
BaseAddr ess / -baseaddress: Specify the base address for the library to be built.
ChecksumAlgorithm  / -checksumalgorithm : Specify algorithm for calculating
source file checksum stored in PDB.
CodeP age / -codepage: Specify the codepage to use when opening source files.
Utf8Output  / -utf8output: Output compiler messages in UTF-8 encoding.
FileAlignment  / -filealign: Specify the alignment used for output file sections.
ErrorEndLocation  / -errorendlocation: Output line and column of the end
location of each error.
NoStandar dLib / -nostdlib: Don't reference standard library mscorlib.dll .
Subsyst emVersion / -subsystemversion: Specify subsystem version of this
assembly.
ModuleAssemblyName  / -moduleassemblyname: Name of the assembly that this
module will be a part of.
Repor tIVTs / -reportivts: Produce additional information on
System.Runtime.CompilerServices.InternalsVisibleT oAttribute  information.
You add any of these options in a <PropertyGroup> element in your *.csproj file:
XML
<PropertyGroup >
    <StartupObject >...</StartupObject >This option specifies the class that contains the entry point to the program, if more than
one class contains a Main method.
XML
or
XML
Where Program is the type that contains the Main method. The provided class name
must be fully qualified; it must include the full namespace containing the class, followed
by the class name. For example, when the Main method is located inside the Program
class in the MyApplication.Core namespace, the compiler option has to be -
main:MyApplication.Core.Program. If your compilation includes more than one type with
a Main  method, you can specify which type contains the Main method.
The PdbFile  compiler option specifies the name and location of the debug symbols file.
The filename value specifies the name and location of the debug symbols file.
XML    ...
</PropertyGroup >
MainEntr yPoint or StartupObject
<StartupObject >MyNamespace.Program </StartupObject >
<MainEntryPoint >MyNamespace.Program </MainEntryPoint >
７ Note
This option can't be used for a project that includes top-lev el stat ements , even if
that project contains one or more Main methods.
PdbFile
<PdbFile>filename </PdbFile>When you specify DebugT ype, the compiler creates a .pdb file in the same directory
where the compiler creates the output file (.exe or .dll). The .pdb file has the same base
file name as the name of the output file. PdbFile  allows you to specify a nondefault file
name and location for the .pdb file. This compiler option can't be set in the Visual S tudio
development environment, nor can it be changed programmatically.
The PathMap  compiler option specifies how to map physical paths to source path
names output by the compiler. This option maps each physical path on the machine
where the compiler runs to a corresponding path that should be written in the output
files. In the following example, path1 is the full path to the source files in the current
environment, and sourcePath1 is the source path substituted for path1 in any output
files. T o specify multiple mapped source paths, separate each with a comma.
XML
The compiler writes the source path into its output for the following reasons:
1. The source path is substituted for an argument when the CallerFileP athAttribute  is
applied to an optional parameter.
2. The source path is embedded in a PDB file.
3. The path of the PDB file is embedded into a PE (portable executable) file.
The ApplicationConfiguration  compiler option enables a C# application to specify the
location of an assembly's application configuration (app.config) file to the common
language runtime (CLR) at assembly binding time.
XML
Where file is the application configuration file that contains assembly binding settings.
One use of ApplicationConfiguration  is advanced scenarios in which an assembly has to
reference both the .NET Framework version and the .NET Framework for Silverlight
version of a particular reference assembly at the same time. For example, a XAML
designer written in Windows Presentation Foundation (WPF) might have to referencePathMap
<PathMap>path1=sourcePath1,path2=sourcePath2 </PathMap>
ApplicationConfiguration
<ApplicationConfiguration >file</ApplicationConfiguration >both the WPF Desktop, for the designer's user interface, and the subset of WPF that is
included with Silverlight. The same designer assembly has to access both assemblies. By
default, the separate references cause a compiler error, because assembly binding sees
the two assemblies as equivalent. The ApplicationConfiguration  compiler option
enables you to specify the location of an app.config file that disables the default
behavior by using a <supportPortability> tag, as shown in the following example.
XML
The compiler passes the location of the file to the CLR's assembly-binding logic.
The following example shows an app.config file that enables an application to have
references to both the .NET Framework implementation and the .NET Framework for
Silverlight implementation of any .NET Framework assembly that exists in both
implementations. The ApplicationConfiguration  compiler option specifies the location
of this app.config file.
XML
The AdditionalLibP aths option specifies the location of assemblies referenced with the
References  option.<supportPortability  PKT="7cec85d7bea7798e"  enable="false"/>
７ Note
To use the app.config file that is already set in the project, add property tag
<UseAppConfigForCompiler> to the .csproj file and set its value to true. To specify a
different app.config file, add property tag <AppConfigForCompiler> and set its value
to the location of the file.
<configuration >
  <runtime>
    <assemblyBinding >
      <supportPortability  PKT="7cec85d7bea7798e"  enable="false"/>
      <supportPortability  PKT="31bf3856ad364e35"  enable="false"/>
    </assemblyBinding >
  </runtime>
</configuration >
AdditionalLibPathsXML
Where dir1 is a directory for the compiler to look in if a referenced assembly isn't
found in the current working directory (the directory from which you're invoking the
compiler) or in the common language runtime's system directory. dir2 is one or more
additional directories to search in for assembly references. Separate directory names
with a comma, and without white space between them. The compiler searches for
assembly references that aren't fully qualified in the following order:
1. Current working directory.
2. The common language runtime system directory.
3. Directories specified by AdditionalLibP aths.
4. Directories specified by the LIB environment variable.
Use Reference  to specify an assembly reference. AdditionalLibP aths is additive.
Specifying it more than once appends to any prior values. Since the path to the
dependent assembly isn't specified in the assembly manifest, the application will find
and use the assembly in the global assembly cache. The compiler referencing the
assembly doesn't imply the common language runtime can find and load the assembly
at run time. See How the Runtime Locates Assemblies  for details on how the runtime
searches for referenced assemblies.
The Generat eFullP aths option causes the compiler to specify the full path to the file
when listing compilation errors and warnings.
Xml
By default, errors and warnings that result from compilation specify the name of the file
in which an error was found. The Generat eFullP aths option causes the compiler to
specify the full path to the file. This compiler option is unavailable in Visual S tudio and
can't be changed programmatically.<AdditionalLibPaths >dir1[,dir2] </AdditionalLibPaths >
GenerateFullPaths
<GenerateFullPaths >true</GenerateFullPaths >
PreferredUILangBy using the Preferr edUILang  compiler option, you can specify the language in which
the C# compiler displays output, such as error messages.
XML
Where language is the language name  of the language to use for compiler output. Y ou
can use the Preferr edUILang  compiler option to specify the language that you want the
C# compiler to use for error messages and other command-line output. If the language
pack for the language isn't installed, the language setting of the operating system is
used instead.
The BaseAddr ess option lets you specify the preferred base address at which to load a
DLL. For more information about when and why to use this option, see Larry Osterman's
WebLog .
XML
Where address is the base address for the DLL. This address can be specified as a
decimal, hexadecimal, or octal number. The default base address for a DLL is set by the
.NET common language runtime. The lower-order word in this address will be rounded.
For example, if you specify 0x11110001, it is rounded to 0x11110000. To complete the
signing process for a DLL, use SN.EXE with the -R option.
This option controls the checksum algorithm we use to encode source files in the PDB.
XML
The algorithm must be either SHA1 (default) or SHA256.<PreferredUILang >language </PreferredUILang >
BaseAddress
<BaseAddress >address</BaseAddress >
ChecksumAlgorithm
<ChecksumAlgorithm >algorithm </ChecksumAlgorithm >
CodePageThis option specifies which codepage to use during compilation if the required page
isn't the current default codepage for the system.
XML
Where id is the ID of the code page to use for all source code files in the compilation.
The compiler first attempts to interpret all source files as UTF-8. If your source code files
are in an encoding other than UTF-8 and use characters other than 7-bit ASCII
characters, use the CodeP age option to specify which code page should be used.
CodeP age applies to all source code files in your compilation. See GetCPInfo  for
information on how to find which code pages are supported on your system.
The Utf8Output  option displays compiler output using UTF-8 encoding.
XML
In some international configurations, compiler output can't correctly be displayed in the
console. Use Utf8Output  and redirect compiler output to a file.
The FileAlignment  option lets you specify the size of sections in your output file. V alid
values are 512, 1024, 2048, 4096, and 8192. These values are in bytes.
XML
You set the FileAlignment  option from the Advanced  page of the Build  properties for
your project in Visual S tudio. Each section is aligned on a boundary that is a multiple of
the FileAlignment  value. There's no fixed default. If FileAlignment  isn't specified, the
common language runtime picks a default at compile time. By specifying the section
size, you affect the size of the output file. Modifying section size may be useful for
programs that run on smaller devices. Use DUMPBIN  to see information about sections
in your output file.<CodePage >id</CodePage >
Utf8Output
<Utf8Output >true</Utf8Output >
FileAlignment
<FileAlignment >number</FileAlignment >Instructs the compiler to output line and column of the end location of each error.
XML
By default, the compiler writes the starting location in source for all errors and warnings.
When this option is set to true, the compiler writes both the starting and end location
for each error and warning.
NoStandar dLib prevents the import of mscorlib.dll, which defines the entire S ystem
namespace.
XML
Use this option if you want to define or create your own S ystem namespace and objects.
If you don't specify NoStandar dLib, mscorlib.dll is imported into your program (same as
specifying <NoStandardLib>false</NoStandardLib>).
Specifies the minimum version of the subsystem on which the executable file runs. Most
commonly, this option ensures that the executable file can use security features that
aren’t available with older versions of Windows.
XMLErrorEndLocation
<ErrorEndLocation >true</ErrorEndLocation >
NoStandardLib
<NoStandardLib >true</NoStandardLib >
SubsystemVersion
７ Note
To specify the subsystem itself, use the TargetType compiler option.
<SubsystemVersion >major.minor </SubsystemVersion >The major.minor specify the minimum required version of the subsystem, as expressed
in a dot notation for major and minor versions. For example, you can specify that an
application can't run on an operating system that's older than Windows 7. Set the value
of this option to 6.01, as the table later in this article describes. Y ou specify the values for
major and minor as integers. Leading zeroes in the minor version don't change the
version, but trailing zeroes do. For example, 6.1 and 6.01 refer to the same version, but
6.10 refers to a different version. W e recommend expressing the minor version as two
digits to avoid confusion.
The following table lists common subsystem versions of Windows.
Windows v ersion Subsyst em v ersion
Windows Server 2003 5.02
Windows Vista 6.00
Windows 7 6.01
Windows Server 2008 6.01
Windows 8 6.02
The default value of the Subsyst emVersion compiler option depends on the conditions
in the following list:
The default value is 6.02 if any compiler option in the following list is set:
-target:appcontainerexe
-target:winmdobj
-platform:arm
The default value is 6.00 if you're using MSBuild, you're targeting .NET Framework
4.5, and you haven't set any of the compiler options that were specified earlier in
this list.
The default value is 4.00 if none of the previous conditions are true.
Specifies the name of an assembly whose nonpublic types a .netmodule  can access.
XMLModuleAssemblyName
<ModuleAssemblyName >assembly_name </ModuleAssemblyName >ModuleAssemblyName  should be used when building a .netmodule , and where the
following conditions are true:
The .netmodule  needs access to nonpublic types in an existing assembly.
You know the name of the assembly into which the .netmodule will be built.
The existing assembly has granted friend assembly access to the assembly into
which the . netmodule  will be built.
For more information on building a .netmodule, see TargetType option of module . For
more information on friend assemblies, see Friend Assemblies .
Enable or disable additional diagnostic information about
System.Runtime.CompilerServices.InternalsVisibleT oAttribute  found during the
compilation:
XML
The diagnostics are enabled if the element content is true, disabled if false, or not
present.
Repor tIVTs reports the following information when enabled:
1. Any inaccessible member diagnostics include their source assembly, if different
than the current assembly.
2. The compiler prints the assembly identity of the project being compiled, its
assembly name and public key.
3. For every reference passed to the compiler, it prints;
a. The assembly identity of the reference
b. Whether the reference grants the current project InternalsVisibleTo
c. The name and all public keys of any assemblies granted InternalsVisibleTo
from this assemblyReportIVTs
<ReportIVTs >true</ReportIVTs >Documentation comments
Article •06/15/2023
C# source files can have structured comments that produce API documentation for the
types defined in those files. The C# compiler produces an XML file that contains
structured data representing the comments and the API signatures. Other tools can
process that XML output to create human-readable documentation in the form of web
pages or PDF files, for example.
This process provides many advantages for you to add API documentation in your code:
The C# compiler combines the structure of the C# code with the text of the
comments into a single XML document.
The C# compiler verifies that the comments match the API signatures for relevant
tags.
Tools that process the XML documentation files can define XML elements and
attributes specific to those tools.
Tools like Visual S tudio provide IntelliSense for many common XML elements used in
documentation comments.
This article covers these topics:
Documentation comments and XML file generation
Tags validated by the C# compiler and Visual S tudio
Format of the generated XML file
You create documentation for your code by writing special comment fields indicated by
triple slashes. The comment fields include XML elements that describe the code block
that follows the comments. For example:
C#
You set either the Generat eDocumentationFile  or DocumentationFile  option, and the
compiler finds all comment fields with XML tags in the source code and creates an XMLCreate XML documentation output
/// <summary>  
/// This class performs an important function.  
/// </summary>  
public class MyClass { } documentation file from those comments. When this option is enabled, the compiler
generates the CS1591  warning for any publicly visible member declared in your project
without XML documentation comments.
The use of XML doc comments requires delimiters that indicate where a documentation
comment begins and ends. Y ou use the following delimiters with the XML
documentation tags:
/// Single-line delimiter: The documentation examples and C# project templates
use this form. If there's white space following the delimiter, it isn't included in the
XML output.
/** */ Multiline delimiters: The /** */ delimiters have the following formatting
rules:
On the line that contains the /** delimiter, if the rest of the line is white space,
the line isn't processed for comments. If the first character after the /**
delimiter is white space, that white-space character is ignored and the rest of
the line is processed. Otherwise, the entire text of the line after the /**
delimiter is processed as part of the comment.
On the line that contains the */ delimiter, if there's only white space up to the
*/ delimiter, that line is ignored. Otherwise, the text on the line up to the */
delimiter is processed as part of the comment.
For the lines after the one that begins with the /** delimiter, the compiler looks
for a common pattern at the beginning of each line. The pattern can consist of
optional white space and/or an asterisk ( *), followed by more optional white
space. If the compiler finds a common pattern at the beginning of each line that
doesn't begin with the /** delimiter or end with the */ delimiter, it ignores
that pattern for each line.XML comment formats
７ Note
Visual S tudio automatically inserts the <summary> and </summary> tags and
positions your cursor within these tags after you type the /// delimiter in the
code editor. Y ou can turn this feature on or off in the Options dialog bo x.The only part of the following comment that's processed is the line that begins
with <summary>. The three tag formats produce the same comments.
C#
The compiler identifies a common pattern of " * " at the beginning of the
second and third lines. The pattern isn't included in the output.
C#
The compiler finds no common pattern in the following comment because the
second character on the third line isn't an asterisk. All text on the second and
third lines is processed as part of the comment.
C#
The compiler finds no pattern in the following comment for two reasons. First,
the number of spaces before the asterisk isn't consistent. Second, the fifth line
begins with a tab, which doesn't match spaces. All text from lines two through
five is processed as part of the comment.
C#/** <summary>text</summary> */  
/** 
<summary>text</summary>  
*/ 
/** 
* <summary>text</summary>  
*/ 
/** 
* <summary>  
* text </summary>*/  
/** 
* <summary>  
   text </summary>  
*/ 
/** 
  * <summary>  
  * text  
*  text2  To refer to XML elements (for example, your function processes specific XML elements
that you want to describe in an XML documentation comment), you can use the
standard quoting mechanism ( &lt; and &gt;). To refer to generic identifiers in code
reference ( cref) elements, you can use either the escape characters (for example,
cref="List&lt;T&gt;") or braces ( cref="List{T}"). As a special case, the compiler
parses the braces as angle brackets to make the documentation comment less
cumbersome to the author when referring to generic identifiers.
The following tools create output from XML comments:
DocFX : DocFX  is an API documentation generator for .NET, which currently
supports C#, Visual Basic, and F#. It also allows you to customize the generated
reference documentation. DocFX builds a static HTML website from your source
code and Markdown files. Also, DocFX provides you with the flexibility to
customize the layout and style of your website through templates. Y ou can also
create custom templates.
Sandcastle : The Sandcastle t ools create help files for managed class libraries
containing both conceptual and API reference pages. The Sandcastle tools are
command-line based and have no GUI front-end, project management features, or
automated build process. The Sandcastle Help File Builder provides standalone GUI
and command-line-based tools to build a help file in an automated fashion. A
Visual S tudio integration package is also available for it so that help projects can
be created and managed entirely from within Visual S tudio.
Doxygen : Doxygen generates an online documentation browser (in HTML) or an
offline reference manual (in LaT eX) from a set of documented source files. There's
also support for generating output in R TF (MS W ord), P ostScript, hyperlinked PDF,
compressed HTML, DocBook, and Unix manual pages. Y ou can configure Doxygen
to extract the code structure from undocumented source files.  *  </summary>  
*/ 
７ Note
The XML documentation comments are not metadata; they are not included in the
compiled assembly and therefore they are not accessible through reflection.
Tools that accept XML documentation input
ID stringsEach type or member is stored in an element in the output XML file. Each of those
elements has a unique ID string that identifies the type or member. The ID string must
account for operators, parameters, return values, generic type parameters, ref, in, and
out parameters. T o encode all those potential elements, the compiler follows clearly
defined rules for generating the ID strings. Programs that process the XML file use the
ID string to identify the corresponding .NET metadata or reflection item that the
documentation applies to.
The compiler observes the following rules when it generates the ID strings:
No white space is in the string.
The first part of the string identifies the kind of member using a single character
followed by a colon. The following member types are used:
Charact er Member
typeNotes
N namespace You can't add documentation comments to a namespace, but
you can make cref ferences to them, where supported.
T type A type is a class, interface, struct, enum, or delegate.
F field
P property Includes indexers or other indexed properties.
M method Includes special methods, such as constructors and operators.
E event
! error string The rest of the string provides information about the error. The
C# compiler generates error information for links that can't be
resolved.
The second part of the string is the fully qualified name of the item, starting at the
root of the namespace. The name of the item, its enclosing type(s), and namespace
are separated by periods. If the name of the item itself has periods, they're
replaced with the hash-sign ('#'). It's assumed that no item has a hash-sign directly
in its name. For example, the fully qualified name of the S tring constructor is
"System.S tring.#ctor".
For properties and methods, the parameter list enclosed in parentheses follows. If
there are no parameters, no parentheses are present. The parameters are
separated by commas. The encoding of each parameter follows directly how it's
encoded in a .NET signature (SeeMicrosoft.VisualS tudio.CorDebugInterop.CorElementT ype for definitions of the all
caps elements in the following list):
Base types. R egular types ( ELEMENT_TYPE_CLASS or ELEMENT_TYPE_VALUETYPE) are
represented as the fully qualified name of the type.
Intrinsic types (for example, ELEMENT_TYPE_I4, ELEMENT_TYPE_OBJECT,
ELEMENT_TYPE_STRING, ELEMENT_TYPE_TYPEDBYREF, and ELEMENT_TYPE_VOID) are
represented as the fully qualified name of the corresponding full type. For
example, System.Int32 or System.TypedReference.
ELEMENT_TYPE_PTR is represented as a '*' following the modified type.
ELEMENT_TYPE_BYREF is represented as a '@' following the modified type.
ELEMENT_TYPE_CMOD_OPT is represented as a '!' and the fully qualified name of the
modifier class, following the modified type.
ELEMENT_TYPE_SZARRAY is represented as "[]" following the element type of the
array.
ELEMENT_TYPE_ARRAY is represented as [ lower bound :size,lower bound :size]
where the number of commas is the rank - 1, and the lower bounds and size of
each dimension, if known, are represented in decimal. If a lower bound or size
isn't specified, it's omitted. If the lower bound and size for a particular
dimension is omitted, the ':' is omitted as well. For example, a two-dimensional
array with 1 as the lower bounds and unspecified sizes is [1:,1:].
For conversion operators only ( op_Implicit and op_Explicit), the return value of
the method is encoded as a ~ followed by the return type. For example: <member
name="M:System.Decimal.op_Explicit(System.Decimal arg)~System.Int32"> is the
tag for the cast operator public static explicit operator int (decimal value);
declared in the System.Decimal class.
For generic types, the name of the type is followed by a backtick and then a
number that indicates the number of generic type parameters. For example:
<member name="T:SampleClass`2"> is the tag for a type that is defined as public
class SampleClass<T, U>. For methods that take generic types as parameters, the
generic type parameters are specified as numbers prefaced with backticks (for
example `0,`1). Each number represents a zero-based array notation for the type's
generic parameters.
ELEMENT_TYPE_PINNED is represented as a '^' following the modified type. The C#
compiler never generates this encoding.
ELEMENT_TYPE_CMOD_REQ is represented as a '|' and the fully qualified name of the
modifier class, following the modified type. The C# compiler never generates
this encoding.ELEMENT_TYPE_GENERICARRAY is represented as "[?]" following the element type of
the array. The C# compiler never generates this encoding.
ELEMENT_TYPE_FNPTR is represented as "=FUNC: type(signatur e)", where type is
the return type, and signatur e is the arguments of the method. If there are no
arguments, the parentheses are omitted. The C# compiler never generates this
encoding.
The following signature components aren't represented because they aren't
used to differentiate overloaded methods:
calling convention
return type
ELEMENT_TYPE_SENTINEL
The following examples show how the ID strings for a class and its members are
generated:
C#
namespace  MyNamespace ; 
/// <summary>  
/// Enter description here for class X.  
/// ID string generated is "T:MyNamespace.MyClass".  
/// </summary>  
public unsafe class MyClass 
{ 
    /// <summary>  
    /// Enter description here for the first constructor.  
    /// ID string generated is "M:MyNamespace.MyClass.#ctor".  
    /// </summary>  
    public MyClass() { } 
    /// <summary>  
    /// Enter description here for the second constructor.  
    /// ID string generated is "M:MyNamespace.MyClass.#ctor(System.Int32)".  
    /// </summary>  
    /// <param name="i"> Describe parameter. </param>  
    public MyClass(int i) { } 
    /// <summary>  
    /// Enter description here for field Message.  
    /// ID string generated is "F:MyNamespace.MyClass.Message".  
    /// </summary>  
    public string? Message;  
    /// <summary>  
    /// Enter description for constant PI.  
    /// ID string generated is "F:MyNamespace.MyClass.PI".  
    /// </summary>  
    public const double PI = 3.14;     /// <summary>  
    /// Enter description for method Func.  
    /// ID string generated is "M:MyNamespace.MyClass.Func".  
    /// </summary>  
    /// <returns> Describe return value. </returns>  
    public int Func() => 1; 
    /// <summary>  
    /// Enter description for method SomeMethod.  
    /// ID string generated is  
"M:MyNamespace.MyClass.SomeMethod(System.String,System.Int32@,System.Void*)"
. 
    /// </summary>  
    /// <param name="str"> Describe parameter. </param>  
    /// <param name="num"> Describe parameter. </param>  
    /// <param name="ptr"> Describe parameter. </param>  
    /// <returns> Describe return value. </returns>  
    public int SomeMethod (string str, ref int nm, void* ptr) { return 1; } 
    /// <summary>  
    /// Enter description for method AnotherMethod.  
    /// ID string generated is  
"M:MyNamespace.MyClass.AnotherMethod(System.Int16[],System.Int32[0:,0:])".  
    /// </summary>  
    /// <param name="array1"> Describe parameter. </param>
    /// <param name="array"> Describe parameter. </param>  
    /// <returns> Describe return value. </returns>  
    public int AnotherMethod (short[] array1, int[,] array ) { return 0; } 
    /// <summary>  
    /// Enter description for operator.  
    /// ID string generated is  
"M:MyNamespace.MyClass.op_Addition(MyNamespace.MyClass,MyNamespace.MyClass)"
. 
    /// </summary>  
    /// <param name="first"> Describe parameter. </param>  
    /// <param name="second"> Describe parameter. </param>
    /// <returns> Describe return value. </returns>  
    public static MyClass operator  +(MyClass first, MyClass second) { return 
first; }  
    /// <summary>  
    /// Enter description for property.  
    /// ID string generated is "P:MyNamespace.MyClass.Prop".  
    /// </summary>  
    public int Prop { get { return 1; } set { } } 
    /// <summary>  
    /// Enter description for event.  
    /// ID string generated is "E:MyNamespace.MyClass.OnHappened".  
    /// </summary>  
    public event Del? OnHappened;  
    /// <summary>  
    /// Enter description for index.  For more information, see the C# Language Specification  annex on documentation
comments.    /// ID string generated is "P:MyNamespace.MyClass.Item(System.String)".  
    /// </summary>  
    /// <param name="str"> Describe parameter. </param>  
    /// <returns> </returns>  
    public int this[string s] => 1; 
    /// <summary>  
    /// Enter description for class Nested.  
    /// ID string generated is "T:MyNamespace.MyClass.Nested".  
    /// </summary>  
    public class Nested { } 
    /// <summary>  
    /// Enter description for delegate.  
    /// ID string generated is "T:MyNamespace.MyClass.Del".  
    /// </summary>  
    /// <param name="i"> Describe parameter. </param>  
    public delegate  void Del(int i); 
    /// <summary>  
    /// Enter description for operator.  
    /// ID string generated is  
"M:MyNamespace.MyClass.op_Explicit(MyNamespace.MyClass)~System.Int32".  
    /// </summary>  
    /// <param name="myParameter"> Describe parameter. </param>  
    /// <returns> Describe return value. </returns>  
    public static explicit  operator  int(MyClass myParameter ) => 1; 
} 
C# language specificationRecommen ded XML tags for C#
documentation comments
Article •08/18/2022
C# documentation comments use XML elements to define the structure of the output
documentation. One consequence of this feature is that you can add any valid XML in
your documentation comments. The C# compiler copies these elements into the output
XML file. While you can use any valid XML in your comments (including any valid HTML
element), documenting code is recommended for many reasons.
What follows are some recommendations, general use case scenarios, and things that
you should know when using XML documentation tags in your C# code. While you can
put any tags into your documentation comments, this article describes the
recommended tags for the most common language constructs. In all cases, you should
adhere to these recommendations:
For the sake of consistency, all publicly visible types and their public members
should be documented.
Private members can also be documented using XML comments. However, it
exposes the inner (potentially confidential) workings of your library.
At a bare minimum, types and their members should have a <summary> tag
because its content is needed for IntelliSense.
Documentation text should be written using complete sentences ending with full
stops.
Partial classes are fully supported, and documentation information will be
concatenated into a single entry for each type.
XML documentation starts with ///. When you create a new project, the templates put
some starter /// lines in for you. The processing of these comments has some
restrictions:
The documentation must be well-formed XML. If the XML isn't well formed, the
compiler generates a warning. The documentation file will contain a comment that
says that an error was encountered.
Some of the recommended tags have special meanings:
The <param> tag is used to describe parameters. If used, the compiler verifies
that the parameter exists and that all parameters are described in the
documentation. If the verification fails, the compiler issues a warning.
The cref attribute can be attached to any tag to reference a code element. The
compiler verifies that this code element exists. If the verification fails, thecompiler issues a warning. The compiler respects any using statements when it
looks for a type described in the cref attribute.
The <summary> tag is used by IntelliSense inside Visual S tudio to display
additional information about a type or member.
Developers are free to create their own set of tags. The compiler will copy these to
the output file.
Some of the recommended tags can be used on any language element. Others have
more specialized usage. Finally, some of the tags are used to format text in your
documentation. This article describes the recommended tags organized by their use.
The compiler verifies the syntax of the elements followed by a single * in the following
list. Visual S tudio provides IntelliSense for the tags verified by the compiler and all tags
followed by ** in the following list. In addition to the tags listed here, the compiler and
Visual S tudio validate the <b>, <i>, <u>, <br/>, and <a> tags. The compiler also
validates <tt>, which is deprecated HTML.
General T ags used for multiple elements - These tags are the minimum set for any
API.
<summary> : The value of this element is displayed in IntelliSense in Visual
Studio.
<remarks>  **
Tags used for members  - These tags are used when documenting methods and
properties.
<returns> : The value of this element is displayed in IntelliSense in Visual S tudio.
<param>  *: The value of this element is displayed in IntelliSense in Visual
Studio.
<paramref>
<exception>  *
<value> : The value of this element is displayed in IntelliSense in Visual S tudio.
Format documentation output  - These tags provide formatting directions for tools
that generate documentation.
<para>
<list>７ Note
The XML file does not provide full information about the type and
members (for example, it does not contain any type information). T o get
full information about a type or member, use the documentation file
together with reflection on the actual type or member.<c>
<code>
<example>  **
Reuse documentation text  - These tags provide tools that make it easier to reuse
XML comments.
<inheritdoc>  **
<include>  *
Generate links and references  - These tags generate links to other documentation.
<see>  *
<seealso>  *
cref
href
Tags for generic types and methods  - These tags are used only on generic types
and methods
<typeparam>  *: The value of this element is displayed in IntelliSense in Visual
Studio.
<typeparamref>
If you want angle brackets to appear in the text of a documentation comment, use the
HTML encoding of < and >, which is &lt; and &gt; respectively. This encoding is
shown in the following example.
C#
XML７ Note
Documentation comments cannot be applied to a namespace.
/// <summary>  
/// This property always returns a value &lt; 1.  
/// </summary>  
General tags
<summary>
<summary>description </summary> The <summary> tag should be used to describe a type or a type member. Use <remarks>
to add supplemental information to a type description. Use the cref attribute  to enable
documentation tools such as DocFX  and Sandcastle  to create internal hyperlinks to
documentation pages for code elements. The text for the <summary> tag is the only
source of information about the type in IntelliSense, and is also displayed in the Object
Browser window.
XML
The <remarks> tag is used to add information about a type or a type member,
supplementing the information specified with <summary> . This information is displayed
in the Object Browser window. This tag may include more lengthy explanations. Y ou may
find that using CDATA sections for markdown make writing it more convenient. T ools
such as docfx  process the markdown text in CDATA sections.
XML
The <returns> tag should be used in the comment for a method declaration to describe
the return value.
XML
name: The name of a method parameter. Enclose the name in double quotation
marks (" "). The names for parameters must match the API signature. If one or
<remarks>
<remarks> 
description  
</remarks> 
Document members
<returns>
<returns>description </returns> 
<param>
<param name="name">description </param> more parameter aren't covered, the compiler issues a warning. The compiler also
issues a warning if the value of name doesn't match a formal parameter in the
method declaration.
The <param> tag should be used in the comment for a method declaration to describe
one of the parameters for the method. T o document multiple parameters, use multiple
<param> tags. The text for the <param> tag is displayed in IntelliSense, the Object
Browser, and the Code Comment W eb Report.
XML
name: The name of the parameter to refer to. Enclose the name in double
quotation marks (" ").
The <paramref> tag gives you a way to indicate that a word in the code comments, for
example in a <summary> or <remarks> block refers to a parameter. The XML file can be
processed to format this word in some distinct way, such as with a bold or italic font.
XML
cref = "member": A reference to an exception that is available from the current
compilation environment. The compiler checks that the given exception exists and
translates member to the canonical element name in the output XML. member must
appear within double quotation marks (" ").
The <exception> tag lets you specify which exceptions can be thrown. This tag can be
applied to definitions for methods, properties, events, and indexers.
XML<paramref>
<paramref  name="name"/> 
<exception>
<exception  cref="member" >description </exception > 
<value>
<value>property-description </value> The <value> tag lets you describe the value that a property represents. When you add a
property via code wizard in the Visual S tudio .NET development environment, it adds a
<summary>  tag for the new property. Y ou manually add a <value> tag to describe the
value that the property represents.
XML
The <para> tag is for use inside a tag, such as <summary> , <remarks> , or <returns> ,
and lets you add structure to the text. The <para> tag creates a double spaced
paragraph. Use the <br/> tag if you want a single spaced paragraph.
XML
The <listheader> block is used to define the heading row of either a table or definition
list. When defining a table, you only need to supply an entry for term in the heading.
Each item in the list is specified with an <item> block. When creating a definition list,Format documentation output
<para>
<remarks> 
    <para> 
        This is an introductory paragraph.  
    </para> 
    <para> 
        This paragraph contains more details.  
    </para> 
</remarks> 
<list>
<list type="bullet|number|table" > 
    <listheader > 
        <term>term</term> 
        <description >description </description >
    </listheader > 
    <item> 
        <term>Assembly </term> 
        <description >The library or executable built from a compilation.
</description > 
    </item> 
</list> you'll need to specify both term and description. However, for a table, bulleted list, or
numbered list, you only need to supply an entry for description. A list or table can have
as many <item> blocks as needed.
XML
The <c> tag gives you a way to indicate that text within a description should be marked
as code. Use <code>  to indicate multiple lines as code.
XML
The <code> tag is used to indicate multiple lines of code. Use <c> to indicate that
single-line text within a description should be marked as code.
XML
The <example> tag lets you specify an example of how to use a method or other library
member. An example commonly involves using the <code>  tag.<c>
<c>text</c> 
<code>
<code> 
    var index = 5;  
    index++;  
</code> 
<example>
<example> 
This shows how to increment an integer.  
<code> 
    var index = 5;  
    index++;  
</code> 
</example> 
Reuse documentation textXML
Inherit XML comments from base classes, interfaces, and similar methods. Using
inheritdoc eliminates unwanted copying and pasting of duplicate XML comments and
automatically keeps XML comments synchronized. Note that when you add the
<inheritdoc> tag to a type, all members will inherit the comments as well.
cref: Specify the member to inherit documentation from. Already defined tags on
the current member are not overridden by the inherited ones.
path: The XP ath expression query that will result in a node set to show. Y ou can
use this attribute to filter the tags to include or exclude from the inherited
documentation.
Add your XML comments in base classes or interfaces and let inheritdoc copy the
comments to implementing classes. Add your XML comments to your synchronous
methods and let inheritdoc copy the comments to your asynchronous versions of the
same methods. If you want to copy the comments from a specific member, you use the
cref attribute to specify the member.
XML
filename: The name of the XML file containing the documentation. The file name
can be qualified with a path relative to the source code file. Enclose filename in
single quotation marks (' ').
tagpath: The path of the tags in filename that leads to the tag name. Enclose the
path in single quotation marks (' ').
name: The name specifier in the tag that precedes the comments; name will have an
id.
id: The ID for the tag that precedes the comments. Enclose the ID in double
quotation marks (" ").
The <include> tag lets you refer to comments in another file that describe the types and
members in your source code. Including an external file is an alternative to placing<inheritdoc>
<inheritdoc  [cref=""] [path=""]/> 
<include>
<include file='filename'  path='tagpath[@name="id"]'  /> documentation comments directly in your source code file. By putting the
documentation in a separate file, you can apply source control to the documentation
separately from the source code. One person can have the source code file checked out
and someone else can have the documentation file checked out. The <include> tag uses
the XML XP ath syntax. R efer to XP ath documentation for ways to customize your
<include> use.
XML
cref="member": A reference to a member or field that is available to be called from
the current compilation environment. The compiler checks that the given code
element exists and passes member to the element name in the output XML. Place
member  within double quotation marks (" "). Y ou can provide different link text for
a "cref", by using a separate closing tag.
href="link": A clickable link to a given URL. For example, <see
href="https://github.com">GitHub</see> produces a clickable link with text GitHub
that links to https://github.com.
langword="keyword": A language keyword, such as true or one of the other valid
keywords .
The <see> tag lets you specify a link from within text. Use <seealso>  to indicate that
text should be placed in a See Also section. Use the cref attribute  to create internal
hyperlinks to documentation pages for code elements. Y ou include the type parameters
to specify a reference to a generic type or method, such as cref="IDictionary{T, U}".
Also, href is a valid attribute that will function as a hyperlink.
XMLGenerate links  and references
<see>
<see cref="member" /> 
<!-- or -->  
<see cref="member" >Link text </see> 
<!-- or -->  
<see href="link">Link Text </see> 
<!-- or -->  
<see langword ="keyword" /> 
<seealso>cref="member": A reference to a member or field that is available to be called from
the current compilation environment. The compiler checks that the given code
element exists and passes member to the element name in the output XML. member
must appear within double quotation marks (" ").
href="link": A clickable link to a given URL. For example, <seealso
href="https://github.com">GitHub</seealso> produces a clickable link with text
GitHub  that links to https://github.com.
The <seealso> tag lets you specify the text that you might want to appear in a See Also
section. Use <see>  to specify a link from within text. Y ou cannot nest the seealso tag
inside the summary tag.
The cref attribute in an XML documentation tag means "code reference." It specifies
that the inner text of the tag is a code element, such as a type, method, or property.
Documentation tools like DocFX  and Sandcastle  use the cref attributes to
automatically generate hyperlinks to the page where the type or member is
documented.
The href attribute means a reference to a web page. Y ou can use it to directly reference
online documentation about your API or library.
XML
TResult: The name of the type parameter. Enclose the name in double quotation
marks (" ").<seealso cref="member" /> 
<!-- or -->  
<seealso href="link">Link Text </seealso> 
cref attribute
href attribute
Generic types and methods
<typeparam>
<typeparam  name="TResult" >The type returned from this method </typeparam > The <typeparam> tag should be used in the comment for a generic type or method
declaration to describe a type parameter. Add a tag for each type parameter of the
generic type or method. The text for the <typeparam> tag will be displayed in
IntelliSense.
XML
TKey: The name of the type parameter. Enclose the name in double quotation
marks (" ").
Use this tag to enable consumers of the documentation file to format the word in some
distinct way, for example in italics.
All the tags outlined above represent those tags that are recognized by the C# compiler.
However, a user is free to define their own tags. T ools like Sandcastle bring support for
extra tags like <event>  and <note> , and even support documenting
namespaces . Custom or in-house documentation generation tools can also be used
with the standard tags, and multiple output formats from HTML to PDF can be
supported.<typeparamref>
<typeparamref  name="TKey"/> 
User-defined tags
Example XML documentation comments
Article •09/15/2021
This article contains three examples for adding XML documentation comments to most
C# language elements. The first example shows how you document a class with different
members. The second shows how you would reuse explanations for a hierarchy of
classes or interfaces. The third shows tags to use for generic classes and members. The
second and third examples use concepts that are covered in the first example.
The following example shows common language elements, and the tags you'll likely use
to describe these elements. The documentation comments describe the use of the tags,
rather than the class itself.
C#Document a class, struct, or interface
    /// <summary>  
    /// Every class and member should have a one sentence  
    /// summary describing its purpose.  
    /// </summary>  
    /// <remarks>  
    /// You can expand on that one sentence summary to  
    /// provide more information for readers. In this case,  
    /// the <c>ExampleClass </c> provides different C#  
    /// elements to show how you would add documentation  
    ///comments for most elements in a typical class.  
    /// <para> 
    /// The remarks can add multiple paragraphs, so you can  
    /// write detailed information for developers that use  
    /// your work. You should add everything needed for  
    /// readers to be successful. This class contains  
    /// examples for the following:  
    /// </para> 
    /// <list type="table">  
    /// <item> 
    /// <term>Summary</term> 
    /// <description>  
    /// This should provide a one sentence summary of the class or member.  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>Remarks</term> 
    /// <description>  
    /// This is typically a more detailed description of the class or member  
    /// </description>  
    /// </item> 
    /// <item>     /// <term>para</term> 
    /// <description>  
    /// The para tag separates a section into multiple paragraphs  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>list</term> 
    /// <description>  
    /// Provides a list of terms or elements  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>returns, param </term> 
    /// <description>  
    /// Used to describe parameters and return values  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>value</term> 
    /// <description> Used to describe properties </description>  
    /// </item> 
    /// <item> 
    /// <term>exception </term> 
    /// <description>  
    /// Used to describe exceptions that may be thrown  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>c, cref, see, seealso </term> 
    /// <description>  
    /// These provide code style and links to other  
    /// documentation elements  
    /// </description>  
    /// </item> 
    /// <item> 
    /// <term>example, code </term> 
    /// <description>  
    /// These are used for code examples  
    /// </description>  
    /// </item> 
    /// </list> 
    /// <para> 
    /// The list above uses the "table" style. You could  
    /// also use the "bullet" or "number" style. Neither  
    /// would typically use the "term" element.  
    /// <br/> 
    /// Note: paragraphs are double spaced. Use the *br*  
    /// tag for single spaced lines.  
    /// </para> 
    /// </remarks>  
    public class ExampleClass  
    { 
        /// <value> 
        /// The <c>Label</c> property represents a label
        /// for this instance.          /// </value>  
        /// <remarks>  
        /// The <see cref="Label"/>  is a <see langword="string"/>  
        /// that you use for a label.  
        /// <para> 
        /// Note that there isn't a way to provide a "cref" to  
        /// each accessor, only to the property itself.  
        /// </para> 
        /// </remarks>  
        public string? Label 
        {  
            get; 
            set; 
        }  
        /// <summary>  
        /// Adds two integers and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The sum of two integers.  
        /// </returns>  
        /// <param name="left">  
        /// The left operand of the addition.  
        /// </param>  
        /// <param name="right">  
        /// The right operand of the addition.  
        /// </param>  
        /// <example>  
        /// <code> 
        /// int c = Math.Add(4, 5);  
        /// if (c > 10)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// <exception cref="System.OverflowException">  
        /// Thrown when one parameter is  
        /// <see cref="Int32.MaxValue"> MaxValue </see> and the other is  
        /// greater than 0.  
        /// Note that here you can also use  
        /// <see 
href="https://learn.microsoft.com/dotnet/api/system.int32.maxvalue"/>  
        ///  to point a web page instead.  
        /// </exception>  
        /// <see cref="ExampleClass"/>  for a list of all  
        /// the tags in these examples.  
        /// <seealso cref="ExampleClass.Label"/>  
        public static int Add(int left, int right) 
        {  
            if ((left == int.MaxValue && right > 0) || (right ==  
int.MaxValue && left > 0)) 
                throw new System.OverflowException();  
            return left + right;  Adding documentation can clutter your source code with large sets of comments
intended for users of your library. Y ou use the <Include> tag to separate your XML
comments from your source. Y our source code references an XML file with the
<Include> tag:
C#
The second file, xml_include_t ag.xml , contains the documentation comments.        }  
    } 
    /// <summary>  
    /// This is an example of a positional record.  
    /// </summary>  
    /// <remarks>  
    /// There isn't a way to add XML comments for properties  
    /// created for positional records, yet. The language  
    /// design team is still considering what tags should  
    /// be supported, and where. Currently, you can use  
    /// the "param" tag to describe the parameters to the  
    /// primary constructor.  
    /// </remarks>  
    /// <param name="FirstName">  
    /// This tag will apply to the primary constructor parameter.  
    /// </param>  
    /// <param name="LastName">  
    /// This tag will apply to the primary constructor parameter.  
    /// </param>  
    public record Person(string FirstName, string LastName ); 
} 
/// <include file='xml_include_tag.xml'  
path='MyDocs/MyMembers[@name="test"]/*' />  
class Test 
{ 
    static void Main() 
    { 
    } 
} 
/// <include file='xml_include_tag.xml'  
path='MyDocs/MyMembers[@name="test2"]/*' />  
class Test2 
{ 
    public void Test() 
    { 
    } 
} XML
The <inheritdoc> element means a type or member inher its documentation comments
from a base class or interface. Y ou can also use the <inheritdoc> element with the cref
attribute to inherit comments from a member of the same type. The following example
shows ways to use this tag. Note that when you add the inheritdoc attribute to a type,
member comments are inherited. Y ou can prevent the use of inherited comments by
writing comments on the members in the derived type. Those will be chosen over the
inherited comments.
C#<MyDocs> 
    <MyMembers  name="test"> 
        <summary> 
        The summary for this type.  
        </summary> 
    </MyMembers > 
    <MyMembers  name="test2"> 
        <summary> 
        The summary for this other type.  
        </summary> 
    </MyMembers > 
</MyDocs> 
Document a hierarchy of classes and interfaces
/// <summary>  
/// A summary about this class.  
/// </summary>  
/// <remarks>  
/// These remarks would explain more about this class.  
/// In this example, these comments also explain the  
/// general information about the derived class.  
/// </remarks>  
public class MainClass  
{ 
} 
///<inheritdoc/>  
public class DerivedClass  : MainClass  
{ 
} 
/// <summary>  
/// This interface would describe all the methods in  
/// its contract.  
/// </summary>  
/// <remarks>  /// While elided for brevity, each method or property  
/// in this interface would contain docs that you want  
/// to duplicate in each implementing class.  
/// </remarks>  
public interface  ITestInterface  
{ 
    /// <summary>  
    /// This method is part of the test interface.  
    /// </summary>  
    /// <remarks>  
    /// This content would be inherited by classes  
    /// that implement this interface when the  
    /// implementing class uses "inheritdoc"  
    /// </remarks>  
    /// <returns> The value of <paramref name="arg" />  </returns>  
    /// <param name="arg"> The argument to the method </param>  
    int Method(int arg); 
} 
///<inheritdoc cref="ITestInterface"/>  
public class ImplementingClass  : ITestInterface  
{ 
    // doc comments are inherited here.  
    public int Method(int arg) => arg;  
} 
/// <summary>  
/// This class shows hows you can "inherit" the doc  
/// comments from one method in another method.  
/// </summary>  
/// <remarks>  
/// You can inherit all comments, or only a specific tag,  
/// represented by an xpath expression.  
/// </remarks>  
public class InheritOnlyReturns  
{ 
    /// <summary>  
    /// In this example, this summary is only visible for this method.  
    /// </summary>  
    /// <returns> A boolean </returns>  
    public static bool MyParentMethod (bool x) { return x; }
    /// <inheritdoc cref="MyParentMethod" path="/returns"/>  
    public static bool MyChildMethod () { return false; } 
} 
/// <Summary>  
/// This class shows an example ofsharing comments across methods.
/// </Summary>  
public class InheritAllButRemarks  
{ 
    /// <summary>  
    /// In this example, this summary is visible on all the methods.  
    /// </summary>  
    /// <remarks>  Use the <typeparam> tag to describe type parameters on generic types and methods.
The value for the cref attribute requires new syntax to reference a generic method or
class:
C#    /// The remarks can be inherited by other methods  
    /// using the xpath expression.  
    /// </remarks>  
    /// <returns> A boolean </returns>  
    public static bool MyParentMethod (bool x) { return x; }
    /// <inheritdoc cref="MyParentMethod" path="//*[not(self::remarks)]"/>  
    public static bool MyChildMethod () { return false; } 
} 
Generic types
/// <summary>  
/// This is a generic class.  
/// </summary>  
/// <remarks>  
/// This example shows how to specify the <see cref="GenericClass{T}"/>  
/// type as a cref attribute.  
/// In generic classes and methods, you'll often want to reference the  
/// generic type, or the type parameter.  
/// </remarks>  
class GenericClass <T> 
{ 
    // Fields and members.  
} 
/// <Summary>  
/// This shows examples of typeparamref and typeparam tags  
/// </Summary>  
public class ParamsAndParamRefs  
{ 
    /// <summary>  
    /// The GetGenericValue method.  
    /// </summary>  
    /// <remarks>  
    /// This sample shows how to specify the <see cref="GetGenericValue"/>  
    /// method as a cref attribute.  
    /// The parameter and return value are both of an arbitrary type,  
    /// <typeparamref name="T"/>  
    /// </remarks>  
    public static T GetGenericValue<T>(T para)  
    { 
        return para; 
    } 
} The following code shows a realistic example of adding doc comments to a math library.
C#Math class example
namespace  TaggedLibrary  
{ 
    /* 
        The main Math class  
        Contains all methods for performing basic math functions  
    */ 
        /// <summary>  
    /// The main <c>Math</c> class. 
    /// Contains all methods for performing basic math functions.  
    /// <list type="bullet">  
    /// <item> 
    /// <term>Add</term> 
    /// <description> Addition Operation </description>  
    /// </item> 
    /// <item> 
    /// <term>Subtract </term> 
    /// <description> Subtraction Operation </description>
    /// </item> 
    /// <item> 
    /// <term>Multiply </term> 
    /// <description> Multiplication Operation </description>  
    /// </item> 
    /// <item> 
    /// <term>Divide</term> 
    /// <description> Division Operation </description>  
    /// </item> 
    /// </list> 
    /// </summary>  
    /// <remarks>  
    /// <para> 
    /// This class can add, subtract, multiply and divide.  
    /// </para> 
    /// <para> 
    /// These operations can be performed on both  
    /// integers and doubles.  
    /// </para> 
    /// </remarks>  
    public class Math 
    { 
        // Adds two integers and returns the result  
        /// <summary>  
        /// Adds two integers <paramref name="a"/>  and <paramref name="b"/>  
        ///  and returns the result.  
        /// </summary>  
        /// <returns>          /// The sum of two integers.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// int c = Math.Add(4, 5);  
        /// if (c > 10)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// <exception cref="System.OverflowException">  
        /// Thrown when one parameter is <see cref="Int32.MaxValue"/>  and 
the other  
        /// is greater than 0.  
        /// </exception>  
        /// See <see cref="Math.Add(double, double)"/>  to add doubles.  
        /// <seealso cref="Math.Subtract(int, int)"/>  
        /// <seealso cref="Math.Multiply(int, int)"/>  
        /// <seealso cref="Math.Divide(int, int)"/>  
        /// <param name="a"> An integer. </param>  
        /// <param name="b"> An integer. </param>  
        public static int Add(int a, int b) 
        {  
            // If any parameter is equal to the max value of an integer  
            // and the other is greater than zero  
            if ((a == int.MaxValue && b > 0) ||  
                (b == int.MaxValue && a > 0)) 
            {  
                throw new System.OverflowException();  
            }  
            return a + b; 
        }  
        // Adds two doubles and returns the result  
        /// <summary>  
        /// Adds two doubles <paramref name="a"/>  and <paramref name="b"/>  
        /// and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The sum of two doubles.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// double c = Math.Add(4.5, 5.4);  
        /// if (c > 10)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// <exception cref="System.OverflowException">  
        /// Thrown when one parameter is max and the other  
        /// is greater than 0. </exception>  
        /// See <see cref="Math.Add(int, int)"/>  to add integers.          /// <seealso cref="Math.Subtract(double, double)"/>  
        /// <seealso cref="Math.Multiply(double, double)"/>  
        /// <seealso cref="Math.Divide(double, double)"/>  
        /// <param name="a"> A double precision number. </param>  
        /// <param name="b"> A double precision number. </param>  
        public static double Add(double a, double b) 
        {  
            // If any parameter is equal to the max value of an integer  
            // and the other is greater than zero  
            if ((a == double.MaxValue && b > 0)  
                || (b == double.MaxValue && a > 0)) 
            {  
                throw new System.OverflowException();  
            }  
            return a + b; 
        }  
        // Subtracts an integer from another and returns the result  
        /// <summary>  
        /// Subtracts <paramref name="b"/>  from <paramref name="a"/>  
        /// and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The difference between two integers.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// int c = Math.Subtract(4, 5);  
        /// if (c > 1)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// See <see cref="Math.Subtract(double, double)"/>  to subtract  
doubles.  
        /// <seealso cref="Math.Add(int, int)"/>  
        /// <seealso cref="Math.Multiply(int, int)"/>  
        /// <seealso cref="Math.Divide(int, int)"/>  
        /// <param name="a"> An integer. </param>  
        /// <param name="b"> An integer. </param>  
        public static int Subtract (int a, int b) 
        {  
            return a - b; 
        }  
        // Subtracts a double from another and returns the result  
        /// <summary>  
        /// Subtracts a double <paramref name="b"/>  from another  
        /// double <paramref name="a"/>  and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The difference between two doubles.  
        /// </returns>          /// <example>  
        /// <code> 
        /// double c = Math.Subtract(4.5, 5.4);  
        /// if (c > 1)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// See <see cref="Math.Subtract(int, int)"/>  to subtract integers.  
        /// <seealso cref="Math.Add(double, double)"/>  
        /// <seealso cref="Math.Multiply(double, double)"/>  
        /// <seealso cref="Math.Divide(double, double)"/>  
        /// <param name="a"> A double precision number. </param>  
        /// <param name="b"> A double precision number. </param>  
        public static double Subtract (double a, double b) 
        {  
            return a - b; 
        }  
        // Multiplies two integers and returns the result  
        /// <summary>  
        /// Multiplies two integers <paramref name="a"/>   
        /// and <paramref name="b"/>  and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The product of two integers.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// int c = Math.Multiply(4, 5);  
        /// if (c > 100)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// See <see cref="Math.Multiply(double, double)"/>  to multiply  
doubles.  
        /// <seealso cref="Math.Add(int, int)"/>  
        /// <seealso cref="Math.Subtract(int, int)"/>  
        /// <seealso cref="Math.Divide(int, int)"/>  
        /// <param name="a"> An integer. </param>  
        /// <param name="b"> An integer. </param>  
        public static int Multiply (int a, int b) 
        {  
            return a * b; 
        }  
        // Multiplies two doubles and returns the result  
        /// <summary>  
        /// Multiplies two doubles <paramref name="a"/>  and 
        /// <paramref name="b"/>  and returns the result.  
        /// </summary>  
        /// <returns>          /// The product of two doubles.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// double c = Math.Multiply(4.5, 5.4);  
        /// if (c > 100.0)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// See <see cref="Math.Multiply(int, int)"/>  to multiply integers.  
        /// <seealso cref="Math.Add(double, double)"/>  
        /// <seealso cref="Math.Subtract(double, double)"/>  
        /// <seealso cref="Math.Divide(double, double)"/>  
        /// <param name="a"> A double precision number. </param>  
        /// <param name="b"> A double precision number. </param>  
        public static double Multiply (double a, double b) 
        {  
            return a * b; 
        }  
        // Divides an integer by another and returns the result  
        /// <summary>  
        /// Divides an integer <paramref name="a"/>  by another  
        /// integer <paramref name="b"/>  and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The quotient of two integers.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// int c = Math.Divide(4, 5);  
        /// if (c > 1)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// <exception cref="System.DivideByZeroException">  
        /// Thrown when <paramref name="b"/>  is equal to 0.  
        /// </exception>  
        /// See <see cref="Math.Divide(double, double)"/>  to divide doubles.  
        /// <seealso cref="Math.Add(int, int)"/>  
        /// <seealso cref="Math.Subtract(int, int)"/>  
        /// <seealso cref="Math.Multiply(int, int)"/>  
        /// <param name="a"> An integer dividend. </param>  
        /// <param name="b"> An integer divisor. </param>  
        public static int Divide(int a, int b) 
        {  
            return a / b; 
        }  
        // Divides a double by another and returns the result  
        /// <summary>  You may find that the code is obscured by all the comments. The final example shows
how you would adapt this library to use the include tag. Y ou move all the
documentation to an XML file:
XML        /// Divides a double <paramref name="a"/>  by another double  
        /// <paramref name="b"/>  and returns the result.  
        /// </summary>  
        /// <returns>  
        /// The quotient of two doubles.  
        /// </returns>  
        /// <example>  
        /// <code> 
        /// double c = Math.Divide(4.5, 5.4);  
        /// if (c > 1.0)  
        /// { 
        ///     Console.WriteLine(c);  
        /// } 
        /// </code> 
        /// </example>  
        /// <exception cref="System.DivideByZeroException">  
        /// Thrown when <paramref name="b"/>  is equal to 0.  
        /// </exception>  
        /// See <see cref="Math.Divide(int, int)"/>  to divide integers.  
        /// <seealso cref="Math.Add(double, double)"/>  
        /// <seealso cref="Math.Subtract(double, double)"/>  
        /// <seealso cref="Math.Multiply(double, double)"/>  
        /// <param name="a"> A double precision dividend. </param>  
        /// <param name="b"> A double precision divisor. </param>  
        public static double Divide(double a, double b) 
        {  
            return a / b; 
        }  
    } 
} 
<docs> 
  <members name="math"> 
   <Math> 
    <summary> 
      The main <c>Math</c> class. 
      Contains all methods for performing basic math functions.  
      </summary> 
      <remarks> 
      <para>This class can add, subtract, multiply and divide. </para> 
      <para>These operations can be performed on both integers and doubles.
</para> 
      </remarks> 
    </Math> 
    <AddInt> 
      <summary>       Adds two integers <paramref  name="a"/> and <paramref  name="b"/>
      and returns the result.  
      </summary> 
      <returns> 
      The sum of two integers.  
      </returns> 
      <example> 
      <code> 
      int c = Math.Add(4, 5);  
      if (c > 10)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      <exception  cref="System.OverflowException" >Thrown when one  
      parameter is max  
      and the other is greater than 0. </exception > 
      See <see cref="Math.Add(double, double)" /> to add doubles.  
      <seealso cref="Math.Subtract(int, int)" /> 
      <seealso cref="Math.Multiply(int, int)" /> 
      <seealso cref="Math.Divide(int, int)" /> 
      <param name="a">An integer. </param> 
      <param name="b">An integer. </param> 
    </AddInt> 
    <AddDouble > 
      <summary> 
      Adds two doubles <paramref  name="a"/> and <paramref  name="b"/> 
      and returns the result.  
      </summary> 
      <returns> 
      The sum of two doubles.  
      </returns> 
      <example> 
      <code> 
      double c = Math.Add(4.5, 5.4);  
      if (c > 10)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      <exception  cref="System.OverflowException" >Thrown when one parameter  
is max  
      and the other is greater than 0. </exception > 
      See <see cref="Math.Add(int, int)" /> to add integers.  
      <seealso cref="Math.Subtract(double, double)" /> 
      <seealso cref="Math.Multiply(double, double)" /> 
      <seealso cref="Math.Divide(double, double)" /> 
      <param name="a">A double precision number. </param> 
      <param name="b">A double precision number. </param> 
    </AddDouble > 
    <SubtractInt > 
      <summary> 
      Subtracts <paramref  name="b"/> from <paramref  name="a"/> and       returns the result.  
      </summary> 
      <returns> 
      The difference between two integers.  
      </returns> 
      <example> 
      <code> 
      int c = Math.Subtract(4, 5);  
      if (c > 1)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      See <see cref="Math.Subtract(double, double)" /> to subtract doubles.  
      <seealso cref="Math.Add(int, int)" /> 
      <seealso cref="Math.Multiply(int, int)" /> 
      <seealso cref="Math.Divide(int, int)" /> 
      <param name="a">An integer. </param> 
      <param name="b">An integer. </param> 
    </SubtractInt > 
    <SubtractDouble > 
      <summary> 
      Subtracts a double <paramref  name="b"/> from another  
      double <paramref  name="a"/> and returns the result.  
      </summary> 
      <returns> 
      The difference between two doubles.  
      </returns> 
      <example> 
      <code> 
      double c = Math.Subtract(4.5, 5.4);  
      if (c > 1)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      See <see cref="Math.Subtract(int, int)" /> to subtract integers.  
      <seealso cref="Math.Add(double, double)" /> 
      <seealso cref="Math.Multiply(double, double)" /> 
      <seealso cref="Math.Divide(double, double)" /> 
      <param name="a">A double precision number. </param> 
      <param name="b">A double precision number. </param> 
    </SubtractDouble > 
    <MultiplyInt > 
      <summary> 
      Multiplies two integers <paramref  name="a"/> and 
      <paramref  name="b"/> and returns the result.  
      </summary> 
      <returns> 
      The product of two integers.  
      </returns> 
      <example> 
      <code>       int c = Math.Multiply(4, 5);  
      if (c > 100)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      See <see cref="Math.Multiply(double, double)" /> to multiply doubles.  
      <seealso cref="Math.Add(int, int)" /> 
      <seealso cref="Math.Subtract(int, int)" /> 
      <seealso cref="Math.Divide(int, int)" /> 
      <param name="a">An integer. </param> 
      <param name="b">An integer. </param> 
    </MultiplyInt > 
    <MultiplyDouble > 
      <summary> 
      Multiplies two doubles <paramref  name="a"/> and 
      <paramref  name="b"/> and returns the result.  
      </summary> 
      <returns> 
      The product of two doubles.
      </returns> 
      <example> 
      <code> 
      double c = Math.Multiply(4.5, 5.4);  
      if (c > 100.0)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      See <see cref="Math.Multiply(int, int)" /> to multiply integers.  
      <seealso cref="Math.Add(double, double)" /> 
      <seealso cref="Math.Subtract(double, double)" /> 
      <seealso cref="Math.Divide(double, double)" /> 
      <param name="a">A double precision number. </param> 
      <param name="b">A double precision number. </param> 
    </MultiplyDouble > 
    <DivideInt > 
      <summary> 
      Divides an integer <paramref  name="a"/> by another integer  
      <paramref  name="b"/> and returns the result.  
      </summary> 
      <returns> 
      The quotient of two integers.  
      </returns> 
      <example> 
      <code> 
      int c = Math.Divide(4, 5);  
      if (c > 1)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> In the above XML, each member's documentation comments appear directly inside a
tag named after what they do. Y ou can choose your own strategy. The code uses the
<include> tag to reference the appropriate element in the XML file:
C#      <exception  cref="System.DivideByZeroException" > 
      Thrown when <paramref  name="b"/> is equal to 0.  
      </exception > 
      See <see cref="Math.Divide(double, double)" /> to divide doubles.  
      <seealso cref="Math.Add(int, int)" /> 
      <seealso cref="Math.Subtract(int, int)" /> 
      <seealso cref="Math.Multiply(int, int)" /> 
      <param name="a">An integer dividend. </param> 
      <param name="b">An integer divisor. </param> 
    </DivideInt > 
    <DivideDouble > 
      <summary> 
      Divides a double <paramref  name="a"/> by another  
      double <paramref  name="b"/> and returns the result.  
      </summary> 
      <returns> 
      The quotient of two doubles.  
      </returns> 
      <example> 
      <code> 
      double c = Math.Divide(4.5, 5.4);  
      if (c > 1.0)  
      { 
        Console.WriteLine(c);  
      } 
      </code> 
      </example> 
      <exception  cref="System.DivideByZeroException" >Thrown when <paramref  
name="b"/> is equal to 0. </exception > 
      See <see cref="Math.Divide(int, int)" /> to divide integers.  
      <seealso cref="Math.Add(double, double)" /> 
      <seealso cref="Math.Subtract(double, double)" /> 
      <seealso cref="Math.Multiply(double, double)" /> 
      <param name="a">A double precision dividend. </param> 
      <param name="b">A double precision divisor. </param> 
    </DivideDouble > 
  </members> 
</docs> 
namespace  IncludeTag  
{ 
    /* 
        The main Math class  
        Contains all methods for performing basic math functions  
    */     /// <include file='include.xml'  
path='docs/members[@name="math"]/Math/*'/>  
    public class Math 
    { 
        // Adds two integers and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/AddInt/*'/>  
        public static int Add(int a, int b) 
        {  
            // If any parameter is equal to the max value of an integer  
            // and the other is greater than zero  
            if ((a == int.MaxValue && b > 0) || (b == int.MaxValue && a >  
0)) 
                throw new System.OverflowException();  
            return a + b; 
        }  
        // Adds two doubles and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/AddDouble/*'/>  
        public static double Add(double a, double b) 
        {  
            // If any parameter is equal to the max value of an integer  
            // and the other is greater than zero  
            if ((a == double.MaxValue && b > 0) || (b == double.MaxValue &&  
a > 0)) 
                throw new System.OverflowException();  
            return a + b; 
        }  
        // Subtracts an integer from another and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/SubtractInt/*'/>  
        public static int Subtract (int a, int b) 
        {  
            return a - b; 
        }  
        // Subtracts a double from another and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/SubtractDouble/*'/>  
        public static double Subtract (double a, double b) 
        {  
            return a - b; 
        }  
        // Multiplies two integers and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/MultiplyInt/*'/>  
        public static int Multiply (int a, int b) 
        {  
            return a * b; 
        }  The file attribute represents the name of the XML file containing the
documentation.
The path attribute represents an XPath query to the tag name present in the
specified file.
The name attribute represents the name specifier in the tag that precedes the
comments.
The id attribute, which can be used in place of name, represents the ID for the tag
that precedes the comments.        // Multiplies two doubles and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/MultiplyDouble/*'/>  
        public static double Multiply (double a, double b) 
        {  
            return a * b; 
        }  
        // Divides an integer by another and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/DivideInt/*'/>  
        public static int Divide(int a, int b) 
        {  
            return a / b; 
        }  
        // Divides a double by another and returns the result  
        /// <include file='include.xml'  
path='docs/members[@name="math"]/DivideDouble/*'/>  
        public static double Divide(double a, double b) 
        {  
            return a / b; 
        }  
    } 
} C# Compiler Errors
Article •05/13/2022
Some C# compiler errors have corresponding topics that explain why the error is
generated, and, in some cases, how to fix the error. Use one of the following steps to
see whether help is available for a particular error message.
If you're using Visual S tudio, choose the error number (for example, CS0029) in the
Output Window , and then choose the F1 key.
Type the error number in the Filter by title  box in the table of contents.
If none of these steps leads to information about your error, go to the end of this page,
and send feedback that includes the number or text of the error.
For information about how to configure error and warning options in C#, see C#
compiler options  or the Visual S tudio Build P age, Project Designer (C#) .
C# Compiler Options
Build P age, Project Designer (C#)
WarningLev el (C# Compiler Options)
NoW arn (C# Compiler Options)７ Note
Your computer might show different names or locations for some of the Visual
Studio user interface elements in the following instructions. The Visual S tudio
edition that you have and the settings that you use determine these elements. For
more information, see Personalizing the IDE .
See alsoC# standard specification
Article •12/09/2023
The C# language specification  is the definitive source for the C# language. The C#
standard committee (T C49-T G2)  produces the specification. The committee is
currently working on version 8 of the standard. The committee uses feature speclets
and language design meeting (LDM) notes  to produce the specification.
This section contains the latest draft of the C# language specification . The latest working
draft is published here before being submitted to ECMA for approval. The committee
works in the dotnet/csharpstandard  repository. Y ou can track the committee's
progress and participate in the standard work there.
Because the committee has fallen behind the latest implementation, this section also
contains the feature specifications  for those newer features that haven't been
incorporated into the standard yet. Y ou can read those specifications to get information
on newer features. The feature specifications are proposals for the design. The C#
language design team and compiler team produce these feature specifications. The
purpose of the proposals was to guide the design and implementation of the feature.
They may include proposed features that haven't yet been implemented. The actual
implementation may have been modified while implementing the feature. Those
changes are captured in the LDM notes. The LDM notes are the minutes of the language
design meetings. In most cases, the pertinent LDM notes are linked from the feature
specifications.
As the committee works on newer versions, the feature specifications are removed from
this site, and those links are redirected to the updated sections of the standard. In the
meantime, the feature specifications represent the best information on those features.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide ..NET feedb ack
.NET is an open source project.
Select a link to provide feedback:
 Open a documentation issue
 Provide product feedbackDetailed table of contents
Article •06/08/2023
Foreword
Introduction
§1 Scope
§2 Normative references
§3 Terms and definitions
§4 General description
§5 Conformance
§6 Lexical structure
§6.1 Programs
§6.2 Grammars
§6.2.1  General
§6.2.2  Grammar notation
§6.2.3  Lexical grammar
§6.2.4  Syntactic grammar
§6.2.5  Grammar ambiguities
§6.3 Lexical analysis
§6.3.1  General
§6.3.2  Line terminators
§6.3.3  Comments
§6.3.4  White space
§6.4 Tokens
§6.4.1  General
§6.4.2  Unicode character escape sequences
§6.4.3  Identifiers
§6.4.4  Keywords
§6.4.5  Literals
§6.4.5.1  General
§6.4.5.2  Boolean literals
§6.4.5.3  Integer literals
§6.4.5.4  Real literals
§6.4.5.5  Character literals
§6.4.5.6  String literals
§6.4.5.7  The null literal
§6.4.6  Operators and punctuators
§6.5 Pre-processing directives
§6.5.1  General
§6.5.2  Conditional compilation symbols§6.5.3  Pre-processing expressions
§6.5.4  Definition directives
§6.5.5  Conditional compilation directives
§6.5.6  Diagnostic directives
§6.5.7  Region directives
§6.5.8  Line directives
§6.5.9  Pragma directives
§7 Basic concepts
§7.1 Application startup
§7.2 Application termination
§7.3 Declarations
§7.4 Members
§7.4.1  General
§7.4.2  Namespace members
§7.4.3  Struct members
§7.4.4  Enumeration members
§7.4.5  Class members
§7.4.6  Interface members
§7.4.7  Array members
§7.4.8  Delegate members
§7.5 Member access
§7.5.1  General
§7.5.2  Declared accessibility
§7.5.3  Accessibility domains
§7.5.4  Protected access
§7.5.5  Accessibility constraints
§7.6 Signatures and overloading
§7.7 Scopes
§7.7.1  General
§7.7.2  Name hiding
§7.7.2.1  General
§7.7.2.2  Hiding through nesting
§7.7.2.3  Hiding through inheritance
§7.8 Namespace and type names
§7.8.1  General
§7.8.2  Unqualified names
§7.8.3  Fully qualified names
§7.9 Automatic memory management
§7.10  Execution order
§8 Types§8.1 General
§8.2 Reference types
§8.2.1  General
§8.2.2  Class types
§8.2.3  The object type
§8.2.4  The dynamic type
§8.2.5  The string type
§8.2.6  Interface types
§8.2.7  Array types
§8.2.8  Delegate types
§8.3 Value types
§8.3.1  General
§8.3.2  The S ystem.V alueT ype type
§8.3.3  Default constructors
§8.3.4  Struct types
§8.3.5  Simple types
§8.3.6  Integral types
§8.3.7  Floating-point types
§8.3.8  The Decimal type
§8.3.9  The Bool type
§8.3.10  Enumeration types
§8.3.11  Tuple types
§8.3.12  Nullable value types
§8.3.13  Boxing and unboxing
§8.4 Constructed types
§8.4.1  General
§8.4.2  Type arguments
§8.4.3  Open and closed types
§8.4.4  Bound and unbound types
§8.4.5  Satisfying constraints
§8.5 Type parameters
§8.6 Expression tree types
§8.7 The dynamic type
§8.8 Unmanaged types
§9 Variables
§9.1 General
§9.2 Variable categories
§9.2.1  General
§9.2.2  Static variables
§9.2.3  Instance variables§9.2.3.1  General
§9.2.3.2  Instance variables in classes
§9.2.3.3  Instance variables in structs
§9.2.4  Array elements
§9.2.5  Value parameters
§9.2.6  Reference parameters
§9.2.7  Output parameters
§9.2.8  Input parameters
§9.2.9  Local variables
§9.2.9.1  Discards
§9.3 Default values
§9.4 Definite assignment
§9.4.1  General
§9.4.2  Initially assigned variables
§9.4.3  Initially unassigned variables
§9.4.4  Precise rules for determining definite assignment
§9.4.4.1  General
§9.4.4.2  General rules for statements
§9.4.4.3  Block statements, checked, and unchecked statements
§9.4.4.4  Expression statements
§9.4.4.5  Declaration statements
§9.4.4.6  If statements
§9.4.4.7  Switch statements
§9.4.4.8  While statements
§9.4.4.9  Do statements
§9.4.4.10  For statements
§9.4.4.11  Break, continue, and goto statements
§9.4.4.12  Throw statements
§9.4.4.13  Return statements
§9.4.4.14  Try-catch statements
§9.4.4.15  Try-finally statements
§9.4.4.16  Try-catch-finally statements
§9.4.4.17  Foreach statements
§9.4.4.18  Using statements
§9.4.4.19  Lock statements
§9.4.4.20  Yield statements
§9.4.4.21  General rules for constant expressions
§9.4.4.22  General rules for simple expressions
§9.4.4.23  General rules for expressions with embedded expressions
§9.4.4.24  Invocation expressions and object creation expressions§9.4.4.25  Simple assignment expressions
§9.4.4.26  && expressions
§9.4.4.27  || expressions
§9.4.4.28  ! expressions
§9.4.4.29  ?? expressions
§9.4.4.30  ?: expressions
§9.4.4.31  Anonymous functions
§9.4.4.32  Throw expressions
§9.4.4.33  Rules for variables in local functions
§9.4.4.34  is-pattern expressions
§9.5 Variable references
§9.6 Atomicity of variable references
§9.7 Reference variables and returns
§9.7.1  General
§9.7.2  Ref safe contexts
§9.7.2.1  General
§9.7.2.2  Local variable ref safe context
§9.7.2.3  Parameter ref safe context
§9.7.2.4  Field ref safe context
§9.7.2.5  Operators
§9.7.2.6  Function invocation
§9.7.2.7  Values
§9.7.2.8  Constructor invocations
§9.7.2.9  Limitations on reference variables
§10 Conversions
§10.1  General
§10.2  Implicit conversions
§10.2.1  General
§10.2.2  Identity conversion
§10.2.3  Implicit numeric conversions
§10.2.4  Implicit enumeration conversions
§10.2.5  Implicit interpolated string conversions
§10.2.6  Implicit nullable conversions
§10.2.7  Null literal conversions
§10.2.8  Implicit reference conversions
§10.2.9  Boxing conversions
§10.2.10  Implicit dynamic conversions
§10.2.11  Implicit constant expression conversions
§10.2.12  Implicit conversions involving type parameters
§10.2.13  Implicit tuple conversions§10.2.14  User-defined implicit conversions
§10.2.15  Anonymous function conversions and method group conversions
§10.2.16  Default literal conversions
§10.2.17  Implicit throw conversions
§10.3  Explicit conversions
§10.3.1  General
§10.3.2  Explicit numeric conversions
§10.3.3  Explicit enumeration conversions
§10.3.4  Explicit nullable conversions
§10.3.5  Explicit reference conversions
§10.3.6  Explicit tuple conversions
§10.3.7  Unboxing conversions
§10.3.8  Explicit dynamic conversions
§10.3.9  Explicit conversions involving type parameters
§10.3.10  User-defined explicit conversions
§10.4  Standard conversions
§10.4.1  General
§10.4.2  Standard implicit conversions
§10.4.3  Standard explicit conversions
§10.5  User-defined conversions
§10.5.1  General
§10.5.2  Permitted user-defined conversions
§10.5.3  Evaluation of user-defined conversions
§10.5.4  User-defined implicit conversions
§10.5.5  User-defined explicit conversions
§10.6  Conversions involving nullable types
§10.6.1  Nullable Conversions
§10.6.2  Lifted conversions
§10.7  Anonymous function conversions
§10.7.1  General
§10.7.2  Evaluation of anonymous function conversions to delegate types
§10.7.3  Evaluation of lambda expression conversions to expression tree types
§10.8  Method group conversions
§11 Patterns and pattern matching
§11.1  General
§11.2  Pattern forms
§11.2.1  General
§11.2.2  Declaration pattern
§11.2.3  Constant pattern
§11.2.4  Var pattern§11.3  Pattern subsumption
§11.4  Pattern exhaustiveness
§12 Expressions
§12.1  General
§12.2  Expression classifications
§12.2.1  General
§12.2.2  Values of expressions
§12.3  Static and Dynamic Binding
§12.3.1  General
§12.3.2  Binding-time
§12.3.3  Dynamic binding
§12.3.4  Types of subexpressions
§12.4  Operators
§12.4.1  General
§12.4.2  Operator precedence and associativity
§12.4.3  Operator overloading
§12.4.4  Unary operator overload resolution
§12.4.5  Binary operator overload resolution
§12.4.6  Candidate user-defined operators
§12.4.7  Numeric promotions
§12.4.7.1  General
§12.4.7.2  Unary numeric promotions
§12.4.7.3  Binary numeric promotions
§12.4.8  Lifted operators
§12.5  Member lookup
§12.5.1  General
§12.5.2  Base types
§12.6  Function members
§12.6.1  General
§12.6.2  Argument lists
§12.6.2.1  General
§12.6.2.2  Corresponding parameters
§12.6.2.3  Run-time evaluation of argument lists
§12.6.3  Type inference
§12.6.3.1  General
§12.6.3.2  The first phase
§12.6.3.3  The second phase
§12.6.3.4  Input types
§12.6.3.5  Output types
§12.6.3.6  Dependence§12.6.3.7  Output type inferences
§12.6.3.8  Explicit parameter type inferences
§12.6.3.9  Exact inferences
§12.6.3.10  Lower-bound inferences
§12.6.3.11  Upper-bound inferences
§12.6.3.12  Fixing
§12.6.3.13  Inferred return type
§12.6.3.14  Type inference for conversion of method groups
§12.6.3.15  Finding the best common type of a set of expressions
§12.6.4  Overload resolution
§12.6.4.1  General
§12.6.4.2  Applicable function member
§12.6.4.3  Better function member
§12.6.4.4  Better parameter-passing mode
§12.6.4.5  Better conversion from expression
§12.6.4.6  Exactly matching expression
§12.6.4.7  Better conversion target
§12.6.4.8  Overloading in generic classes
§12.6.5  Compile-time checking of dynamic member invocation
§12.6.6  Function member invocation
§12.6.6.1  General
§12.6.6.2  Invocations on boxed instances
§12.7  Deconstruction
§12.8  Primary expressions
§12.8.1  General
§12.8.2  Literals
§12.8.3  Interpolated string expressions
§12.8.4  Simple names
§12.8.5  Parenthesized expressions
§12.8.6  Tuple expressions
§12.8.7  Member access
§12.8.7.1  General
§12.8.7.2  Identical simple names and type names
§12.8.8  Null Conditional Member Access
§12.8.9  Invocation expressions
§12.8.9.1  General
§12.8.9.2  Method invocations
§12.8.9.3  Extension method invocations
§12.8.9.4  Delegate invocations
§12.8.10  Null Conditional Invocation Expression§12.8.11  Element access
§12.8.11.1  General
§12.8.11.2  Array access
§12.8.11.3  Indexer access
§12.8.12  Null Conditional Element Access
§12.8.13  This access
§12.8.14  Base access
§12.8.15  Postfix increment and decrement operators
§12.8.16  The new operator
§12.8.16.1  General
§12.8.16.2  Object creation expressions
§12.8.16.3  Object initializers
§12.8.16.4  Collection initializers
§12.8.16.5  Array creation expressions
§12.8.16.6  Delegate creation expressions
§12.8.16.7  Anonymous object creation expressions
§12.8.17  The typeof operator
§12.8.18  The sizeof operator
§12.8.19  The checked and unchecked operators
§12.8.20  Default value expressions
§12.8.21  Stack allocation
§12.8.22  Nameof expressions
§12.8.23  Anonymous method expressions
§12.9  Unary operators
§12.9.1  General
§12.9.2  Unary plus operator
§12.9.3  Unary minus operator
§12.9.4  Logical negation operator
§12.9.5  Bitwise complement operator
§12.9.6  Prefix increment and decrement operators
§12.9.7  Cast expressions
§12.9.8  Await expressions
§12.9.8.1  General
§12.9.8.2  Awaitable expressions
§12.9.8.3  Classification of await expressions
§12.9.8.4  Run-time evaluation of await expressions
§12.10  Arithmetic operators
§12.10.1  General
§12.10.2  Multiplication operator
§12.10.3  Division operator§12.10.4  Remainder operator
§12.10.5  Addition operator
§12.10.6  Subtraction operator
§12.11  Shift operators
§12.12  Relational and type-testing operators
§12.12.1  General
§12.12.2  Integer comparison operators
§12.12.3  Floating-point comparison operators
§12.12.4  Decimal comparison operators
§12.12.5  Boolean equality operators
§12.12.6  Enumeration comparison operators
§12.12.7  Reference type equality operators
§12.12.8  String equality operators
§12.12.9  Delegate equality operators
§12.12.10  Equality operators between nullable value types and the null literal
§12.12.11  Tuple equality operators
§12.12.12  The is operator
§12.12.12.1  The is-type operator
§12.12.12.2  The is-pattern operator
§12.12.13  The as operator
§12.13  Logical operators
§12.13.1  General
§12.13.2  Integer logical operators
§12.13.3  Enumeration logical operators
§12.13.4  Boolean logical operators
§12.13.5  Nullable Boolean & and | operators
§12.14  Conditional logical operators
§12.14.1  General
§12.14.2  Boolean conditional logical operators
§12.14.3  User-defined conditional logical operators
§12.15  The null coalescing operator
§12.16  The throw expression operator
§12.17  Declaration expressions
§12.18  Conditional operator
§12.19  Anonymous function expressions
§12.19.1  General
§12.19.2  Anonymous function signatures
§12.19.3  Anonymous function bodies
§12.19.4  Overload resolution
§12.19.5  Anonymous functions and dynamic binding§12.19.6  Outer variables
§12.19.6.1  General
§12.19.6.2  Captured outer variables
§12.19.6.3  Instantiation of local variables
§12.19.7  Evaluation of anonymous function expressions
§12.19.8  Implementation Example
§12.20  Query expressions
§12.20.1  General
§12.20.2  Ambiguities in query expressions
§12.20.3  Query expression translation
§12.20.3.1  General
§12.20.3.2  Query expressions with continuations
§12.20.3.3  Explicit range variable types
§12.20.3.4  Degenerate query expressions
§12.20.3.5  From, let, where, join and orderby clauses
§12.20.3.6  Select clauses
§12.20.3.7  Group clauses
§12.20.3.8  Transparent identifiers
§12.20.4  The query-expression pattern
§12.21  Assignment operators
§12.21.1  General
§12.21.2  Simple assignment
§12.21.3  Ref assignment
§12.21.4  Compound assignment
§12.21.5  Event assignment
§12.22  Expression
§12.23  Constant expressions
§12.24  Boolean expressions
§13 Statements
§13.1  General
§13.2  End points and reachability
§13.3  Blocks
§13.3.1  General
§13.3.2  Statement lists
§13.4  The empty statement
§13.5  Labeled statements
§13.6  Declaration statements
§13.6.1  General
§13.6.2  Local variable declarations
§13.6.2.1  General§13.6.2.2  Implicitly typed local variable declarations
§13.6.2.3  Explicitly typed local variable declarations
§13.6.2.4  Ref local variable declarations
§13.6.3  Local constant declarations
§13.6.4  Local function declarations
§13.7  Expression statements
§13.8  Selection statements
§13.8.1  General
§13.8.2  The if statement
§13.8.3  The switch statement
§13.9  Iteration statements
§13.9.1  General
§13.9.2  The while statement
§13.9.3  The do statement
§13.9.4  The for statement
§13.9.5  The foreach statement
§13.10  Jump statements
§13.10.1  General
§13.10.2  The break statement
§13.10.3  The continue statement
§13.10.4  The goto statement
§13.10.5  The return statement
§13.10.6  The throw statement
§13.11  The try statement
§13.12  The checked and unchecked statements
§13.13  The lock statement
§13.14  The using statement
§13.15  The yield statement
§14 Namespaces
§14.1  General
§14.2  Compilation units
§14.3  Namespace declarations
§14.4  Extern alias directives
§14.5  Using directives
§14.5.1  General
§14.5.2  Using alias directives
§14.5.3  Using namespace directives
§14.5.4  Using static directives
§14.6  Namespace member declarations
§14.7  Type declarations§14.8  Qualified alias member
§14.8.1  General
§14.8.2  Uniqueness of aliases
§15 Classes
§15.1  General
§15.2  Class declarations
§15.2.1  General
§15.2.2  Class modifiers
§15.2.2.1  General
§15.2.2.2  Abstract classes
§15.2.2.3  Sealed classes
§15.2.2.4  Static classes
§15.2.2.4.1  General
§15.2.2.4.2  Referencing static class types
§15.2.3  Type parameters
§15.2.4  Class base specification
§15.2.4.1  General
§15.2.4.2  Base classes
§15.2.4.3  Interface implementations
§15.2.5  Type parameter constraints
§15.2.6  Class body
§15.2.7  Partial declarations
§15.3  Class members
§15.3.1  General
§15.3.2  The instance type
§15.3.3  Members of constructed types
§15.3.4  Inheritance
§15.3.5  The new modifier
§15.3.6  Access modifiers
§15.3.7  Constituent types
§15.3.8  Static and instance members
§15.3.9  Nested types
§15.3.9.1  General
§15.3.9.2  Fully qualified name
§15.3.9.3  Declared accessibility
§15.3.9.4  Hiding
§15.3.9.5  this access
§15.3.9.6  Access to private and protected members of the containing type
§15.3.9.7  Nested types in generic classes
§15.3.10  Reserved member names§15.3.10.1  General
§15.3.10.2  Member names reserved for properties
§15.3.10.3  Member names reserved for events
§15.3.10.4  Member names reserved for indexers
§15.3.10.5  Member names reserved for finalizers
§15.4  Constants
§15.5  Fields
§15.5.1  General
§15.5.2  Static and instance fields
§15.5.3  Readonly fields
§15.5.3.1  General
§15.5.3.2  Using static readonly fields for constants
§15.5.3.3  Versioning of constants and static readonly fields
§15.5.4  Volatile fields
§15.5.5  Field initialization
§15.5.6  Variable initializers
§15.5.6.1  General
§15.5.6.2  Static field initialization
§15.5.6.3  Instance field initialization
§15.6  Methods
§15.6.1  General
§15.6.2  Method parameters
§15.6.2.1  General
§15.6.2.2  Value parameters
§15.6.2.3  Input parameters
§15.6.2.4  Reference parameters
§15.6.2.5  Output parameters
§15.6.2.6  Parameter arrays
§15.6.3  Static and instance methods
§15.6.4  Virtual methods
§15.6.5  Override methods
§15.6.6  Sealed methods
§15.6.7  Abstract methods
§15.6.8  External methods
§15.6.9  Partial methods
§15.6.10  Extension methods
§15.6.11  Method body
§15.7  Properties
§15.7.1  General
§15.7.2  Static and instance properties§15.7.3  Accessors
§15.7.4  Automatically implemented properties
§15.7.5  Accessibility
§15.7.6  Virtual, sealed, override, and abstract accessors
§15.8  Events
§15.8.1  General
§15.8.2  Field-like events
§15.8.3  Event accessors
§15.8.4  Static and instance events
§15.8.5  Virtual, sealed, override, and abstract accessors
§15.9  Indexers
§15.9.1  General
§15.9.2  Indexer and Property Differences
§15.10  Operators
§15.10.1  General
§15.10.2  Unary operators
§15.10.3  Binary operators
§15.10.4  Conversion operators
§15.11  Instance constructors
§15.11.1  General
§15.11.2  Constructor initializers
§15.11.3  Instance variable initializers
§15.11.4  Constructor execution
§15.11.5  Default constructors
§15.12  Static constructors
§15.13  Finalizers
§15.14  Iterators
§15.14.1  General
§15.14.2  Enumerator interfaces
§15.14.3  Enumerable interfaces
§15.14.4  Yield type
§15.14.5  Enumerator objects
§15.14.5.1  General
§15.14.5.2  The MoveNext method
§15.14.5.3  The Current property
§15.14.5.4  The Dispose method
§15.14.6  Enumerable objects
§15.14.6.1  General
§15.14.6.2  The GetEnumerator method
§15.15  Async Functions§15.15.1  General
§15.15.2  Task-type builder pattern
§15.15.3  Evaluation of a task-returning async function
§15.15.4  Evaluation of a void-returning async function
§16 Structs
§16.1  General
§16.2  Struct declarations
§16.2.1  General
§16.2.2  Struct modifiers
§16.2.3  Ref modifier
§16.2.4  Partial modifier
§16.2.5  Struct interfaces
§16.2.6  Struct body
§16.3  Struct members
§16.4  Class and struct differences
§16.4.1  General
§16.4.2  Value semantics
§16.4.3  Inheritance
§16.4.4  Assignment
§16.4.5  Default values
§16.4.6  Boxing and unboxing
§16.4.7  Meaning of this
§16.4.8  Field initializers
§16.4.9  Constructors
§16.4.10  Static constructors
§16.4.11  Automatically implemented properties
§16.4.12  Safe context constraint
§16.4.12.1  General
§16.4.12.2  Parameter safe context
§16.4.12.3  Local variable safe context
§16.4.12.4  Field safe context
§16.4.12.5  Operators
§16.4.12.6  Method and property invocation
§16.4.12.7  stackalloc
§16.4.12.8  Constructor invocations
§17 Arrays
§17.1  General
§17.2  Array types
§17.2.1  General
§17.2.2  The S ystem.Array type§17.2.3  Arrays and the generic collection interfaces
§17.3  Array creation
§17.4  Array element access
§17.5  Array members
§17.6  Array covariance
§17.7  Array initializers
§18 Interfaces
§18.1  General
§18.2  Interface declarations
§18.2.1  General
§18.2.2  Interface modifiers
§18.2.3  Variant type parameter lists
§18.2.3.1  General
§18.2.3.2  Variance safety
§18.2.3.3  Variance conversion
§18.2.4  Base interfaces
§18.3  Interface body
§18.4  Interface members
§18.4.1  General
§18.4.2  Interface methods
§18.4.3  Interface properties
§18.4.4  Interface events
§18.4.5  Interface indexers
§18.4.6  Interface member access
§18.5  Qualified interface member names
§18.6  Interface implementations
§18.6.1  General
§18.6.2  Explicit interface member implementations
§18.6.3  Uniqueness of implemented interfaces
§18.6.4  Implementation of generic methods
§18.6.5  Interface mapping
§18.6.6  Interface implementation inheritance
§18.6.7  Interface re-implementation
§18.6.8  Abstract classes and interfaces
§19 Enums
§19.1  General
§19.2  Enum declarations
§19.3  Enum modifiers
§19.4  Enum members
§19.5  The S ystem.Enum type§19.6  Enum values and operations
§20 Delegates
§20.1  General
§20.2  Delegate declarations
§20.3  Delegate members
§20.4  Delegate compatibility
§20.5  Delegate instantiation
§20.6  Delegate invocation
§21 Exceptions
§21.1  General
§21.2  Causes of exceptions
§21.3  The S ystem.Exception class
§21.4  How exceptions are handled
§21.5  Common exception classes
§22 Attributes
§22.1  General
§22.2  Attribute classes
§22.2.1  General
§22.2.2  Attribute usage
§22.2.3  Positional and named parameters
§22.2.4  Attribute parameter types
§22.3  Attribute specification
§22.4  Attribute instances
§22.4.1  General
§22.4.2  Compilation of an attribute
§22.4.3  Run-time retrieval of an attribute instance
§22.5  Reserved attributes
§22.5.1  General
§22.5.2  The AttributeUsage attribute
§22.5.3  The Conditional attribute
§22.5.3.1  General
§22.5.3.2  Conditional methods
§22.5.3.3  Conditional attribute classes
§22.5.4  The Obsolete attribute
§22.5.5  Caller-info attributes
§22.5.5.1  General
§22.5.5.2  The CallerLineNumber attribute
§22.5.5.3  The CallerFileP ath attribute
§22.5.5.4  The CallerMemberName attribute
§22.6  Attributes for interoperation§23 Unsafe code
§23.1  General
§23.2  Unsafe contexts
§23.3  Pointer types
§23.4  Fixed and moveable variables
§23.5  Pointer conversions
§23.5.1  General
§23.5.2  Pointer arrays
§23.6  Pointers in expressions
§23.6.1  General
§23.6.2  Pointer indirection
§23.6.3  Pointer member access
§23.6.4  Pointer element access
§23.6.5  The address-of operator
§23.6.6  Pointer increment and decrement
§23.6.7  Pointer arithmetic
§23.6.8  Pointer comparison
§23.6.9  The sizeof operator
§23.7  The fixed statement
§23.8  Fixed-size buffers
§23.8.1  General
§23.8.2  Fixed-size buffer declarations
§23.8.3  Fixed-size buffers in expressions
§23.8.4  Definite assignment checking
§23.9  Stack allocation
§A Grammar
§A.1 General
§A.2 Lexical grammar
§A.3 Syntactic grammar
§A.4 Grammar extensions for unsafe code
§B Portability issues
§B.1 General
§B.2 Undefined behavior
§B.3 Implementation-defined behavior
§B.4 Unspecified behavior
§B.5 Other issues
§C Standard library
§C.1 General
§C.2 Standard Library T ypes defined in ISO/IEC 23271
§C.3 Standard Library T ypes not defined in ISO/IEC 23271§C.4 Format Specifications
§C.5 Library T ype Abbreviations
§D Documentation comments
§D.1 General
§D.2 Introduction
§D.3 Recommended tags
§D.3.1  General
§D.3.2  <c>
§D.3.3  <code>
§D.3.4  <example>
§D.3.5  <exception>
§D.3.6  <include>
§D.3.7  <list>
§D.3.8  <para>
§D.3.9  <param>
§D.3.10  <paramref>
§D.3.11  <permission>
§D.3.12  <remarks>
§D.3.13  <returns>
§D.3.14  <see>
§D.3.15  <seealso>
§D.3.16  <summary>
§D.3.17  <typeparam>
§D.3.18  <typeparamref>
§D.3.19  <value>
§D.4 Processing the documentation file
§D.4.1  General
§D.4.2  ID string format
§D.4.3  ID string examples
§D.5 An example
§D.5.1  C# source code
§D.5.2  Resulting XML
§E Bibliography
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and reviewC# Standar d documentation
feedb ack
The C# S tandard documentation is
open source. Provide feedback here.issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackForeword
Article •03/23/2023
This specification replaces ECMA-334:2022. Changes from the previous edition include
the addition of the following:
Binary integer literals
Embedded digit separators in numeric literals
Leading-digit separators in binary and hexadecimal integer literals
out variables
Discards
Tuple types
Pattern Matching
ref locals and returns, conditional ref expressions, ref with this in extension
methods, and reassignment of ref local variables
Local Functions
More expression-bodied members
throw Expressions
Generalized async return types
async Main method
default literal expressions
Non-trailing named arguments
private protected access modifier
in parameter modifier
readonly structs
ref structs
Indexing movable fixed buffer without pinning
Initializers on stackalloc arrays
Pattern-based fixed statements
System.Delegate and System.Enum as class_type  constraints.
Additional generic constraints
Allow expression variables in more locations
Attach attributes to the backing field of auto-implemented properties
Reduce ambiguity of overload resolutionIntroduction
Article •03/18/2022
This specification is based on a submission from Hewlett-P ackard, Intel, and Microsoft,
that described a language called C#, which was developed within Microsoft. The
principal inventors of this language were Anders Hejlsberg, Scott Wiltamuth, and P eter
Golde. The first widely distributed implementation of C# was released by Microsoft in
July 2000, as part of its .NET Framework initiative.
Ecma T echnical Committee 39 (T C39) [later renamed to T C49] T ask Group 2 (T G2) was
formed in September 2000, to produce a standard for C#. Another T ask Group, T G3, was
also formed at that time to produce a standard for a library and execution environment
called Common Language Infrastructure (CLI). (CLI is based on a subset of the .NET
Framework.) Although Microsoft’s implementation of C# relies on CLI for library and
run-time support, other implementations of C# need not, provided they support an
alternate way of getting at the minimum CLI features required by this C# standard (see
Annex C ).
As the definition of C# evolved, the goals used in its design were as follows:
C# is intended to be a simple, modern, general-purpose, object-oriented
programming language.
The language, and implementations thereof, should provide support for software
engineering principles such as strong type checking, array bounds checking,
detection of attempts to use uninitialized variables, and automatic garbage
collection. Software robustness, durability, and programmer productivity are
important.
The language is intended for use in developing software components suitable for
deployment in distributed environments.
Source code portability is very important, as is programmer portability, especially
for those programmers already familiar with C and C++.
Support for internationalization is very important.
C# is intended to be suitable for writing applications for both hosted and
embedded systems, ranging from the very large that use sophisticated operating
systems, down to the very small having dedicated functions.
Although C# applications are intended to be economical with regard to memory
and processing power requirements, the language was not intended to compete
directly on performance and size with C or assembly language.
The name C# is pronounced “C Sharp”.The name C# is written as the L ATIN CAPIT AL LET TER C (U+0043) followed by the
NUMBER SIGN # (U+0023).1 Scope
Article •01/13/2022
This specification describes the form and establishes the interpretation of programs
written in the C# programming language. It describes
The representation of C# programs;
The syntax and constraints of the C# language;
The semantic rules for interpreting C# programs;
The restrictions and limits imposed by a conforming implementation of C#.
This specification does not describe
The mechanism by which C# programs are transformed for use by a data-
processing system;
The mechanism by which C# applications are invoked for use by a data-processing
system;
The mechanism by which input data are transformed for use by a C# application;
The mechanism by which output data are transformed after being produced by a
C# application;
The size or complexity of a program and its data that will exceed the capacity of
any specific data-processing system or the capacity of a particular processor;
All minimal requirements of a data-processing system that is capable of
supporting a conforming implementation.2 Normative references
Article •03/18/2022
The following normative documents contain provisions, which, through reference in this
text, constitute provisions of this specification. For dated references, subsequent
amendments to, or revisions of, any of these publications do not apply. However, parties
to agreements based on this specification are encouraged to investigate the possibility
of applying the most recent editions of the normative documents indicated below. For
undated references, the latest edition of the normative document referred to applies.
Members of ISO and IEC maintain registers of currently valid specifications.
ISO/IEC 23271:2012, Common L anguage Infr astructur e (CLI), P artition IV : Base Class
Library (BCL), Ext ended Numer ics Libr ary, and Ext ended Arr ay Libr ary.
ISO 80000-2, Quantities and units — P art 2: Mathematical signs and s ymbols t o be us ed
in the natur al scienc es and t echnology .
ISO/IEC 2382, Information t echnology — V ocabular y.
ISO/IEC 60559:2020, Information t echnology — Micr oprocessor Systems — Flo ating-P oint
arithmetic
The Unicode Consortium. The Unicode S tandard,
https://www.unicode.org/standard/standard.html
3 Terms and definitions
Article •10/04/2023
For the purposes of this specification, the following definitions apply. Other terms are
defined where they appear in it alic type or on the left side of a syntax rule. T erms
explicitly defined in this specification are not to be presumed to refer implicitly to similar
terms defined elsewhere. T erms not defined in this specification are to be interpreted
according to ISO/IEC 2382.1. Mathematical symbols not defined in this specification are
to be interpreted according to ISO 80000-2.
application  – assembly with an entry point
application domain  – entity that enables application isolation by acting as a
container for application state
argument  – expression in the comma-separated list bounded by the parentheses
in a method or instance constructor call expression or bounded by the square
brackets in an element access expression
assembly  – one or more files output by the compiler as a result of program
compilation
behavior  – external appearance or action
behavior , implementation-defined  – unspecified behavior where each
implementation documents how the choice is made
behavior , undefined  – behavior, upon use of a non-portable or erroneous
construct or of erroneous data, for which this specification imposes no
requirements
behavior , unspecified  – behavior where this specification provides two or more
possibilities and imposes no further requirements on which is chosen in any
instance
charact er (when used without a qualifier)
In the context of a non-Unicode encoding, the meaning of character in that
encoding; or
In the context of a character literal or a value of type char, a Unicode code point
in the range U+0000 to U+FFFF (including surrogate code points), that is a UTF-
16 code unit; or
Otherwise, a Unicode code point
class librar y – assembly that can be used by other assemblies
compilation unit  – ordered sequence of Unicode characters that is input to a
compiler
diagnostic message  – message belonging to an implementation-defined subset of
the implementation’s output messages
error, compile-time  – error reported during program translationexception  – exceptional condition reported during program execution
implementation  – particular set of software (running in a particular translation
environment under particular control options) that performs translation of
programs for, and supports execution of methods in, a particular execution
environment
module  – the contents of an assembly produced by a compiler. Some
implementations may have facilities to produce assemblies that contain more than
one module. The behavior in such situations is outside the scope of this
specification
namesp ace – logical organizational system grouping related program elements
paramet er – variable declared as part of a method, instance constructor, operator,
or indexer definition, which acquires a value on entry to that function member
program  – one or more compilation units that are presented to the compiler and
are run or executed by an execution environment
unsafe code  – code that is permitted to perform such lower-level operations as
declaring and operating on pointers, performing conversions between pointers
and integral types, and taking the address of variables
warning, compile-time  – informational message reported during program
translation, which is intended to identify a potentially questionable usage of a
program element
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# Standar d documentation
feedb ack
The C# S tandard documentation is
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedback4 Gen eral description
Article •04/08/2022
This t ext is informativ e.
This specification is intended to be used by implementers, academics, and application
programmers. As such, it contains a considerable amount of explanatory material that,
strictly speaking, is not necessary in a formal language specification.
This specification is divided into the following subdivisions: front matter; language
syntax, constraints, and semantics; and annexes.
Examples are provided to illustrate possible forms of the constructions described.
References are used to refer to related clauses. Notes are provided to give advice or
guidance to implementers or programmers. Annexes provide additional information and
summarize the information contained in this specification.
End o f informativ e text.
Informative text is indicated in the following ways:
1. Whole or partial clauses or annexes delimited by “ This clause/t ext is informativ e”
and “ End o f informativ e text”.
2. Example : The following example … code fragment, possibly with some narrative …
end ex ample  The Example:  and end ex ample  markers are in the same paragraph for
single paragraph examples. If an example spans multiple paragraphs, the end
example marker should be its own paragraph.
3. Note: narrative … end not e The Note: and end not e markers are in the same
paragraph for single paragraph notes. If a note spans multiple paragraphs, the end
note marker should be its own paragraph.
All text not marked as being informative is normative.5 Conformance
Article •03/18/2022
Conformance is of interest to the following audiences:
Those designing, implementing, or maintaining C# implementations.
Governmental or commercial entities wishing to procure C# implementations.
Testing organizations wishing to provide a C# conformance test suite.
Programmers wishing to port code from one C# implementation to another.
Educators wishing to teach S tandard C#.
Authors wanting to write about S tandard C#.
As such, conformance is most important, and the bulk of this specification is aimed at
specifying the characteristics that make C# implementations and C# programs
conforming ones.
The text in this specification that specifies requirements is considered normativ e. All
other text in this specification is infor mativ e; that is, for information purposes only.
Unless stated otherwise, all text is normative. Normative text is further broken into
requir ed and conditional  categories. Conditionally nor mativ e text specifies a feature
and its requirements where the feature is optional. However, if that feature is provided,
its syntax and semantics shall be exactly as specified.
Undefined behavior is indicated in this specification only by the words ‘undefined
behavior.’
A strictly c onfor ming pr ogram shall use only those features of the language specified in
this specification as being required. (This means that a strictly conforming program
cannot use any conditionally normative feature.) It shall not produce output dependent
on any unspecified, undefined, or implementation-defined behavior.
A confor ming implement ation  of C# shall accept any strictly conforming program.
A conforming implementation of C# shall provide and support all the types, values,
objects, properties, methods, and program syntax and semantics described in the
normative (but not the conditionally normative) parts in this specification.
A conforming implementation of C# shall interpret characters in conformance with the
Unicode S tandard. Conforming implementations shall accept compilation units encoded
with the UTF-8 encoding form.
A conforming implementation of C# shall not successfully translate source containing a
#error preprocessing directive unless it is part of a group skipped by conditionalcompilation.
A conforming implementation of C# shall produce at least one diagnostic message if
the source program violates any rule of syntax, or any negative requirement (defined as
a “shall” or “shall not” or “error” or “warning” requirement), unless that requirement is
marked with the words “no diagnostic is required”.
A conforming implementation of C# is permitted to provide additional types, values,
objects, properties, and methods beyond those described in this specification, provided
they do not alter the behavior of any strictly conforming program. Conforming
implementations are required to diagnose programs that use extensions that are ill
formed according to this specification. Having done so, however, they can compile and
execute such programs. (The ability to have extensions implies that a conforming
implementation reserves no identifiers other than those explicitly reserved in this
specification.)
A conforming implementation of C# shall be accompanied by a document that defines
all implementation-defined characteristics, and all extensions.
A conforming implementation of C# shall support the class library documented in Annex
C. This library is included by reference in this specification.
A confor ming pr ogram is one that is acceptable to a conforming implementation. (Such
a program is permitted to contain extensions or conditionally normative features.)6 Lexical structure
Article •03/24/2023
A C#  program consists of one or more source files, known formally as compilation units
(§14.2 ). Although a compilation unit might have a one-to-one correspondence with a file
in a file system, such correspondence is not required.
Conceptually speaking, a program is compiled using three steps:
1. Transformation, which converts a file from a particular character repertoire and
encoding scheme into a sequence of Unicode characters.
2. Lexical analysis, which translates a stream of Unicode input characters into a
stream of tokens.
3. Syntactic analysis, which translates the stream of tokens into executable code.
Conforming implementations shall accept Unicode compilation units encoded with the
UTF-8 encoding form (as defined by the Unicode standard), and transform them into a
sequence of Unicode characters. Implementations can choose to accept and transform
additional character encoding schemes (such as UTF-16, UTF-32, or non-Unicode
character mappings).
Note: The handling of the Unicode NULL character (U+0000) is implementation-
specific. It is strongly recommended that developers avoid using this character in
their source code, for the sake of both portability and readability. When the
character is required within a character or string literal, the escape sequences \0 or
\u0000 may be used instead. end not e
Note: It is beyond the scope of this specification to define how a file using a
character representation other than Unicode might be transformed into a sequence
of Unicode characters. During such transformation, however, it is recommended that
the usual line-separating character (or sequence) in the other character set be
translated to the two-character sequence consisting of the Unicode carriage-return
character (U+000D) followed by Unicode line-feed character (U+000A). For the most
part this transformation will have no visible effects; however, it will affect the
interpretation of verbatim string literal tokens ( §6.4.5.6 ). The purpose of this
recommendation is to allow a verbatim string literal to produce the same character
sequence when its compilation unit is moved between systems that support6.1 Programsdiffering non-Unicode character sets, in particular, those using differing character
sequences for line-separation. end not e
This specification presents the syntax of the C# programming language using two
grammars. The lexical gr ammar  (§6.2.3 ) defines how Unicode characters are combined
to form line terminators, white space, comments, tokens, and pre-processing directives.
The syntactic gr ammar  (§6.2.4 ) defines how the tokens resulting from the lexical
grammar are combined to form C# programs.
All terminal characters are to be understood as the appropriate Unicode character from
the range U+0020 to U+007F, as opposed to any similar-looking characters from other
Unicode character ranges.
The lexical and syntactic grammars are presented in the ANTLR grammar tool’s
Extended Backus-Naur form.
While the ANTLR notation is used, this specification does not present a complete
ANTLR-ready “reference grammar” for C#; writing a lexer and parser, either by hand or
using a tool such as ANTLR, is outside the scope of a language specification. With that
qualification, this specification attempts to minimize the gap between the specified
grammar and that required to build a lexer and parser in ANTLR.
ANTLR distinguishes between lexical and syntactic, termed parser by ANTLR, grammars
in its notation by starting lexical rules with an uppercase letter and parser rules with a
lowercase letter.
Note: The C# lexical grammar ( §6.2.3 ) and syntactic grammar ( §6.2.4 ) are not in exact
correspondence with the ANTLR division into lexical and parser grammers. This
small mismatch means that some ANTLR parser rules are used when specifying the
C# lexical grammar. end not e
The lexical grammar of C# is presented in §6.3, §6.4, and §6.5. The terminal symbols of
the lexical grammar are the characters of the Unicode character set, and the lexical6.2 Grammars
6.2.1 General
6.2.2 Grammar notation
6.2.3 Lexical grammargrammar specifies how characters are combined to form tokens ( §6.4), white space
(§6.3.4 ), comments ( §6.3.3 ), and pre-processing directives ( §6.5).
Many of the terminal symbols of the syntactic grammar are not defined explicitly as
tokens in the lexical grammar. Rather, advantage is taken of the ANTLR behavior that
literal strings in the grammar are extracted as implicit lexical tokens; this allows
keywords, operators, etc. to be represented in the grammar by their literal
representation rather than a token name.
Every compilation unit in a C# program shall conform to the input  production of the
lexical grammar ( §6.3.1 ).
The syntactic grammar of C# is presented in the clauses, subclauses, and annexes that
follow this subclause. The terminal symbols of the syntactic grammar are the tokens
defined explicitly by the lexical grammar and implicitly by literal strings in the grammar
itself ( §6.2.3 ). The syntactic grammar specifies how tokens are combined to form
C# programs.
Every compilation unit in a C# program shall conform to the compilation_unit
production ( §14.2 ) of the syntactic grammar.
The productions for simple_name  (§12.8.4 ) and member_ac cess (§12.8.7 ) can give rise to
ambiguities in the grammar for expressions.
Example : The statement:
C#
could be interpreted as a call to  F with two arguments, G < A and B > (7).
Alternatively, it could be interpreted as a call to  F with one argument, which is a call
to a generic method  G with two type arguments and one regular argument.
end ex ample
If a sequence of tokens can be parsed (in context) as a simple_name  (§12.8.4 ),
member_ac cess (§12.8.7 ), or point er_member_ac cess (§23.6.3 ) ending with a6.2.4 Syntactic grammar
6.2.5 Grammar ambiguities
F(G<A, B>( 7));type_ar gument_list  (§8.4.2 ), the token immediately following the closing > token is
examined, to see if it is
One of ( ) ] } : ; , . ? == != | ^ && || & [; or
One of the relational operators < > <= >= is as; or
A contextual query keyword appearing inside a query expression; or
In certain contexts, identi fier is treated as a disambiguating token. Those contexts
are where the sequence of tokens being disambiguated is immediately preceded
by one of the keywords is, case or out, or arises while parsing the first element
of a tuple literal (in which case the tokens are preceded by ( or : and the
identifier is followed by a ,) or a subsequent element of a tuple literal.
If the following token is among this list, or an identifier in such a context, then the
type_ar gument_list  is retained as part of the simple_name , member_ac cess or
point er_member -access and any other possible parse of the sequence of tokens is
discarded. Otherwise, the type_ar gument_list  is not considered to be part of the
simple_name , member_ac cess or point er_member_ac cess, even if there is no other
possible parse of the sequence of tokens.
Note: These rules are not applied when parsing a type_ar gument_list  in a
namesp ace_or_type_name  (§7.8). end not e
Example : The statement:
C#
will, according to this rule, be interpreted as a call to  F with one argument, which is
a call to a generic method  G with two type arguments and one regular argument.
The statements
C#
will each be interpreted as a call to  F with two arguments. The statement
C#F(G<A, B>( 7));
F(G<A, B> 7);
F(G<A, B>> 7);
x = F<A> + y;will be interpreted as a less-than operator, greater-than operator and unary-plus
operator, as if the statement had been written x = (F < A) > (+y), instead of as a
simple_name  with a type_ar gument_list  followed by a binary-plus operator. In the
statement
C#
the tokens C<T> are interpreted as a namesp ace_or_type_name  with a
type_ar gument_list  due to the presence of the disambiguating token && after the
type_ar gument_list .
The expression (A < B, C > D) is a tuple with two elements, each a comparison.
The expression (A<B,C> D, E) is a tuple with two elements, the first of which is a
declaration expression.
The invocation M(A < B, C > D, E) has three arguments.
The invocation M(out A<B,C> D, E) has two arguments, the first of which is an out
declaration.
The expression e is A<B> C uses a declaration pattern.
The case label case A<B> C: uses a declaration pattern.
end ex ample
When recognising a relational_expr ession  (§12.12.1 ) if both the “ relational_expr ession  is
type” and “ relational_expr ession  is constant_p attern” alternatives are applicable, and
type resolves to an accessible type, then the “ relational_expr ession  is type” alternative
shall be chosen.
For convenience, the lexical grammar defines and references the following named lexer
tokens:
ANTLRx = y is C<T> && z;
6.3 Lexical analysis
6.3.1 GeneralAlthough these are lexer rules, these names are spelled in all-uppercase letters to
distinguish them from ordinary lexer rule names.
Note: These convenience rules are exceptions to the usual practice of not providing
explicit token names for tokens defined by literal strings. end not e
The input  production defines the lexical structure of a C# compilation unit.
ANTLR
Note: The above grammar is described by ANTLR parsing rules, it defines the lexical
structure of a C# compilation unit and not lexical tokens. end not e
Five basic elements make up the lexical structure of a C# compilation unit: Line
terminators ( §6.3.2 ), white space ( §6.3.4 ), comments ( §6.3.3 ), tokens ( §6.4), and pre-
processing directives ( §6.5). Of these basic elements, only tokens are significant in the
syntactic grammar of a C# program ( §6.2.4 ).
The lexical processing of a C# compilation unit consists of reducing the file into a
sequence of tokens that becomes the input to the syntactic analysis. Line terminators,DEFAULT  : 'default'  ;
NULL     : 'null' ;
TRUE     : 'true' ;
FALSE    : 'false' ;
ASTERISK  : '*' ;
SLASH    : '/' ;
input
    : input_section?
    ;
input_section
    : input_section_part+
    ;
input_section_part
    : input_element* New_Line
    | PP_Directive
    ;
input_element
    : Whitespace
    | Comment
    | token
    ;white space, and comments can serve to separate tokens, and pre-processing directives
can cause sections of the compilation unit to be skipped, but otherwise these lexical
elements have no impact on the syntactic structure of a C# program.
When several lexical grammar productions match a sequence of characters in a
compilation unit, the lexical processing always forms the longest possible lexical
element.
Example : The character sequence  // is processed as the beginning of a single-line
comment because that lexical element is longer than a single  / token. end ex ample
Some tokens are defined by a set of lexical rules; a main rule and one or more sub-rules.
The latter are marked in the grammar by fragment to indicate the rule defines part of
another token. Fragment rules are not considered in the top-to-bottom ordering of
lexical rules.
Note: In ANTLR fragment is a keyword which produces the same behavior defined
here. end not e
Line terminators divide the characters of a C# compilation unit into lines.
ANTLR
For compatibility with source code editing tools that add end-of-file markers, and to
enable a compilation unit to be viewed as a sequence of properly terminated lines, the
following transformations are applied, in order, to every compilation unit in a
C# program:
If the last character of the compilation unit is a Control-Z character (U+001A), this
character is deleted.
A carriage-return character (U+000D) is added to the end of the compilation unit if
that compilation unit is non-empty and if the last character of the compilation unit
is not a carriage return (U+000D), a line feed (U+000A), a next line character
(U+0085), a line separator (U+2028), or a paragraph separator (U+2029).6.3.2 Line terminators
New_Line
    : New_Line_Character
    | '\u000D\u000A'     // carriage return, line feed 
    ;Note: The additional carriage-return allows a program to end in a PP_Dir ective (§6.5)
that does not have a terminating New_Line . end not e
Two forms of comments are supported: delimited comments and single-line comments.
A delimit ed comment  begins with the characters  /* and ends with the characters  */.
Delimited comments can occupy a portion of a line, a single line, or multiple lines.
Example : The example
C#
includes a delimited comment.
end ex ample
A single-line c omment  begins with the characters  // and extends to the end of the line.
Example : The example
C#
shows several single-line comments.6.3.3 Comments
/* Hello, world program
   This program writes "hello, world" to the console
*/
class Hello
{
    static void Main()
    {
        System.Console.WriteLine( "hello, world" );
    }
}
// Hello, world program
// This program writes "hello, world" to the console
//
class Hello // any name will do for this class
{
    static void Main() // this method must be named "Main"
    {
        System.Console.WriteLine( "hello, world" );
    }
}end ex ample
ANTLR
Comments do not nest. The character sequences  /* and */ have no special meaning
within a single-line comment, and the character sequences  // and /* have no special
meaning within a delimited comment.
Comments are not processed within character and string literals.
Note: These rules must be interpreted carefully. For instance, in the example below,
the delimited comment that begins before  A ends between  B and C(). The reason
is thatComment
    : Single_Line_Comment
    | Delimited_Comment
    ;
fragment  Single_Line_Comment
    : '//' Input_Character*
    ;
fragment  Input_Character
    // anything but New_Line_Character
    : ~('\u000D'  | '\u000A'    | '\u0085'  | '\u2028'  | '\u2029' )
    ;
    
fragment  New_Line_Character
    : '\u000D'   // carriage return
    | '\u000A'   // line feed
    | '\u0085'   // next line
    | '\u2028'   // line separator
    | '\u2029'   // paragraph separator
    ;
    
fragment  Delimited_Comment
    : '/*' Delimited_Comment_Section* ASTERISK+ '/'
    ;
    
fragment  Delimited_Comment_Section
    : SLASH
    | ASTERISK* Not_Slash_Or_Asterisk
    ;
fragment  Not_Slash_Or_Asterisk
    : ~('/' | '*')    // Any except SLASH or ASTERISK
    ;C#
is not actually a single-line comment, since // has no special meaning within a
delimited comment, and so */ does have its usual special meaning in that line.
Likewise, the delimited comment starting before  D ends before  E. The reason is
that "D */ " is not actually a string literal, since the initial double quote character
appears inside a delimited comment.
A useful consequence of  /* and */ having no special meaning within a single-line
comment is that a block of source code lines can be commented out by putting //
at the beginning of each line. In general, it does not work to put /* before those
lines and */ after them, as this does not properly encapsulate delimited comments
in the block, and in general may completely change the structure of such delimited
comments.
Example code:
C#
end not e
Single_Line_C omment s and Delimit ed_C omment s having particular formats can be used
as document ation c omments , as described in §D.
White space is defined as any character with Unicode class Zs (which includes the space
character) as well as the horizontal tab character, the vertical tab character, and the form
feed character.
ANTLR// B */ C();
static void Main()
{
    /* A
    // B */ C();
    Console.WriteLine( /* "D */  "E");
}
6.3.4 White spaceThere are several kinds of tokens: identifiers, keywords, literals, operators, and
punctuators. White space and comments are not tokens, though they act as separators
for tokens.
ANTLR
Note: This is an ANTLR parser rule, it does not define a lexical token but rather the
collection of token kinds. end not e
A Unicode escape sequence represents a Unicode code point. Unicode escape
sequences are processed in identifiers ( §6.4.3 ), character literals ( §6.4.5.5 ), regular string
literals ( §6.4.5.6 ), and interpolated regular string expressions ( §12.8.3 ). A Unicode escape
sequence is not processed in any other location (for example, to form an operator,
punctuator, or keyword).
ANTLRWhitespace
    : [\p{Zs}]  // any character with Unicode class Zs
    | '\u0009'   // horizontal tab
    | '\u000B'   // vertical tab
    | '\u000C'   // form feed
    ;
6.4 Tokens
6.4.1 General
token
    : identifier
    | keyword
    | Integer_Literal
    | Real_Literal
    | Character_Literal
    | String_Literal
    | operator_or_punctuator
    ;
6.4.2 Unicode character escape sequences
fragment  Unicode_Escape_Sequence
    : '\\u' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
    | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_DigitA Unicode character escape sequence represents the single Unicode code point formed
by the hexadecimal number following the “\u” or “\U” characters. Since C# uses a 16-bit
encoding of Unicode code points in character and string values, a Unicode code point in
the range U+10000 to U+10FFFF is represented using two Unicode surrogate code units.
Unicode code points above U+FFFF are not permitted in character literals. Unicode code
points above U+10FFFF are invalid and are not supported.
Multiple translations are not performed. For instance, the string literal "\u005Cu005C" is
equivalent to "\u005C" rather than "\".
Note: The Unicode value \u005C is the character “ \”. end not e
Example : The example
C#
shows several uses of \u0066, which is the escape sequence for the letter “ f”. The
program is equivalent to
C#            Hex_Digit Hex_Digit Hex_Digit Hex_Digit
    ;
class Class1
{
    static void Test(bool \u0066)
    {
        char c = '\u0066' ;
        if (\u0066)
        {
            System.Console.WriteLine(c.ToString());
        }
    }
}
class Class1
{
    static void Test(bool f)
    {
        char c = 'f';
        if (f)
        {
            System.Console.WriteLine(c.ToString());
        }end ex ample
The rules for identifiers given in this subclause correspond exactly to those
recommended by the Unicode S tandard Annex 15 except that underscore is allowed as
an initial character (as is traditional in the C programming language), Unicode escape
sequences are permitted in identifiers, and the “ @” character is allowed as a prefix to
enable keywords to be used as identifiers.
ANTLR    }
}
6.4.3 Identifiers
identifier
    : Simple_Identifier
    | contextual_keyword
    ;
Simple_Identifier
    : Available_Identifier
    | Escaped_Identifier
    ;
fragment  Available_Identifier
    // excluding keywords or contextual keywords, see note below
    : Basic_Identifier
    ;
fragment  Escaped_Identifier
    // Includes keywords and contextual keywords prefixed by '@'.
    // See note below.
    : '@' Basic_Identifier 
    ;
fragment  Basic_Identifier
    : Identifier_Start_Character Identifier_Part_Character*
    ;
fragment  Identifier_Start_Character
    : Letter_Character
    | Underscore_Character
    ;
fragment  Underscore_Character
    : '_'           // underscore
    | '\\u005'  [fF] // Unicode_Escape_Sequence for underscore
    ;Note:
For information on the Unicode character classes mentioned above, see The
Unicode S tandar d.
The fragment Available_Identi fier requires the exclusion of keywords and
contextual keywords. If the grammar in this specification is processed with
ANTLR then this exclusion is handled automatically by the semantics of ANTLR:
Keywords and contextual keywords occur in the grammar as literal strings.fragment  Identifier_Part_Character
    : Letter_Character
    | Decimal_Digit_Character
    | Connecting_Character
    | Combining_Character
    | Formatting_Character
    ;
fragment  Letter_Character
    // Category Letter, all subcategories; category Number, subcategory  
letter.
    : [\p{L}\p{Nl}]
    // Only escapes for categories L & Nl allowed. See note below.
    | Unicode_Escape_Sequence
    ;
fragment  Combining_Character
    // Category Mark, subcategories non-spacing and spacing combining.
    : [\p{Mn}\p{Mc}]
    // Only escapes for categories Mn & Mc allowed. See note below.
    | Unicode_Escape_Sequence
    ;
fragment  Decimal_Digit_Character
    // Category Number, subcategory decimal digit.
    : [\p{Nd}]
    // Only escapes for category Nd allowed. See note below.
    | Unicode_Escape_Sequence
    ;
fragment  Connecting_Character
    // Category Punctuation, subcategory connector.
    : [\p{Pc}]
    // Only escapes for category Pc allowed. See note below.
    | Unicode_Escape_Sequence
    ;
fragment  Formatting_Character
    // Category Other, subcategory format.
    : [\p{Cf}]
    // Only escapes for category Cf allowed, see note below.
    | Unicode_Escape_Sequence
    ;ANTLR creates implicit lexical token rules are created from these literal
strings.
ANTLR considers these implicit rules before the explicit lexical rules in the
grammar.
Therefore fragment Available_Identi fier will not match keywords or
contextual keywords as the lexical rules for those precede it.
Fragment Escaped_Identi fier includes escaped keywords and contextual
keywords as they are part of the longer token starting with an @ and lexical
processing always forms the longest possible lexical element ( §6.3.1 ).
How an implementation enforces the restrictions on the allowable
Unicode_Es cape_Sequenc e values is an implementation issue.
end not e
Example : Examples of valid identifiers are identifier1, _identifier2, and @if. end
example
An identifier in a conforming program shall be in the canonical format defined by
Unicode Normalization Form C, as defined by Unicode S tandard Annex 15. The behavior
when encountering an identifier not in Normalization Form C is implementation-
defined; however, a diagnostic is not required.
The prefix “ @” enables the use of keywords as identifiers, which is useful when
interfacing with other programming languages. The character  @ is not actually part of
the identifier, so the identifier might be seen in other languages as a normal identifier,
without the prefix. An identifier with an @ prefix is called a verbatim identi fier.
Note: Use of the @ prefix for identifiers that are not keywords is permitted, but
strongly discouraged as a matter of style. end not e
Example : The example:
C#
class @class
{
    public static void @static(bool @bool)
    {
        if (@bool)
        {
            System.Console.WriteLine( "true");
        }
        elsedefines a class named “ class” with a static method named “ static” that takes a
parameter named “ bool”. Note that since Unicode escapes are not permitted in
keywords, the token “ cl\u0061ss” is an identifier, and is the same identifier as
“@class”.
end ex ample
Two identifiers are considered the same if they are identical after the following
transformations are applied, in order:
The prefix “ @”, if used, is removed.
Each Unicode_Es cape_Sequenc e is transformed into its corresponding Unicode
character.
Any Formatting_Char acters are removed.
The semantics of an identifier named _ depends on the context in which it appears:
It can denote a named program element, such as a variable, class, or method, or
It can denote a discard ( §9.2.9.1 ).
Identifiers containing two consecutive underscore characters ( U+005F) are reserved for
use by the implementation; however, no diagnostic is required if such an identifier is
defined.
Note: For example, an implementation might provide extended keywords that begin
with two underscores. end not e
A keyword is an identifier-like sequence of characters that is reserved, and cannot be
used as an identifier except when prefaced by the @ character.        {
            System.Console.WriteLine( "false");
        }
    }
}
class Class1
{
    static void M()
    {
        cl\u0061ss.st\u0061tic( true);
    }
}
6.4.4 KeywordsANTLR
A contextual k eyword is an identifier-like sequence of characters that has special
meaning in certain contexts, but is not reserved, and can be used as an identifier outside
of those contexts as well as when prefaced by the @ character.
ANTLR
Note: The rules keyword and contextual_k eyword are parser rules as they do not
introduce new token kinds. All keywords and contextual keywords are defined by
implicit lexical rules as they occur as literal strings in the grammar ( §6.2.3 ). end not e
In most cases, the syntactic location of contextual keywords is such that they can never
be confused with ordinary identifier usage. For example, within a property declaration,
the get and set identifiers have special meaning ( §15.7.3 ). An identifier other than get
or set is never permitted in these locations, so this use does not conflict with a use of
these words as identifiers.keyword
    : 'abstract'  | 'as'       | 'base'       | 'bool'      | 'break'
    | 'byte'     | 'case'     | 'catch'      | 'char'      | 'checked'
    | 'class'    | 'const'    | 'continue'    | 'decimal'    | DEFAULT
    | 'delegate'  | 'do'       | 'double'      | 'else'      | 'enum'
    | 'event'    | 'explicit'  | 'extern'      | FALSE       | 'finally'
    | 'fixed'    | 'float'    | 'for'        | 'foreach'    | 'goto'
    | 'if'       | 'implicit'  | 'in'         | 'int'       | 'interface'
    | 'internal'  | 'is'       | 'lock'       | 'long'      | 'namespace'
    | 'new'      | NULL       | 'object'      | 'operator'   | 'out'
    | 'override'  | 'params'    | 'private'     | 'protected'  | 'public'
    | 'readonly'  | 'ref'      | 'return'      | 'sbyte'     | 'sealed'
    | 'short'    | 'sizeof'    | 'stackalloc'  | 'static'     | 'string'
    | 'struct'    | 'switch'    | 'this'       | 'throw'     | TRUE
    | 'try'      | 'typeof'    | 'uint'       | 'ulong'     | 'unchecked'
    | 'unsafe'    | 'ushort'    | 'using'      | 'virtual'    | 'void'
    | 'volatile'  | 'while'
    ;
contextual_keyword
    : 'add'    | 'alias'      | 'ascending'  | 'async'     | 'await'
    | 'by'     | 'descending'  | 'dynamic'    | 'equals'     | 'from'
    | 'get'    | 'global'      | 'group'     | 'into'      | 'join'
    | 'let'    | 'nameof'      | 'on'        | 'orderby'    | 'partial'
    | 'remove'  | 'select'      | 'set'       | 'unmanaged'  | 'value'
    | 'var'    | 'when'       | 'where'     | 'yield'
    ;In certain cases the grammar is not enough to distinguish contextual keyword usage
from identifiers. In all such cases it will be specified how to disambiguate between the
two. For example, the contextual keyword var in implicitly typed local variable
declarations ( §13.6.2 ) might conflict with a declared type called var, in which case the
declared name takes precedence over the use of the identifier as a contextual keyword.
Another example such disambiguation is the contextual keyword await (§12.9.8.1 ),
which is considered a keyword only when inside a method declared async, but can be
used as an identifier elsewhere.
Just as with keywords, contextual keywords can be used as ordinary identifiers by
prefixing them with the @ character.
Note: When used as contextual keywords, these identifiers cannot contain
Unicode_Es cape_Sequenc es. end not e
A literal (§12.8.2 ) is a source-code representation of a value.
ANTLR
Note: literal is a parser rule as it groups other token kinds and does not introduce a
new token kind. end not e
There are two Boolean literal values: true and false.
ANTLR6.4.5 Literals
6.4.5.1 General
literal
    : boolean_literal
    | Integer_Literal
    | Real_Literal
    | Character_Literal
    | String_Literal
    | null_literal
    ;
6.4.5.2 Boolean literalsNote: boolean_lit eral is a parser rule as it groups other token kinds and does not
introduce a new token kind. end not e
The type of a boolean_lit eral is bool.
Integer literals are used to write values of types int, uint, long, and ulong. Integer
literals have three possible forms: decimal, hexadecimal, and binary.
ANTLRboolean_literal
    : TRUE
    | FALSE
    ;
6.4.5.3 Integer literals
Integer_Literal
    : Decimal_Integer_Literal
    | Hexadecimal_Integer_Literal
    | Binary_Integer_Literal
    ;
fragment  Decimal_Integer_Literal
    : Decimal_Digit Decorated_Decimal_Digit* Integer_Type_Suffix?
    ;
fragment  Decorated_Decimal_Digit
    : '_'* Decimal_Digit
    ;
       
fragment  Decimal_Digit
    : '0'..'9'
    ;
    
fragment  Integer_Type_Suffix
    : 'U' | 'u' | 'L' | 'l' |
      'UL' | 'Ul' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
    ;
    
fragment  Hexadecimal_Integer_Literal
    : ('0x' | '0X') Decorated_Hex_Digit+ Integer_Type_Suffix?
    ;
fragment  Decorated_Hex_Digit
    : '_'* Hex_Digit
    ;
       
fragment  Hex_DigitThe type of an integer literal is determined as follows:
If the literal has no suffix, it has the first of these types in which its value can be
represented: int, uint, long, ulong.
If the literal is suffixed by U or u, it has the first of these types in which its value
can be represented: uint, ulong.
If the literal is suffixed by L or l, it has the first of these types in which its value
can be represented: long, ulong.
If the literal is suffixed by UL, Ul, uL, ul, LU, Lu, lU, or lu, it is of type ulong.
If the value represented by an integer literal is outside the range of the ulong type, a
compile-time error occurs.
Note: As a matter of style, it is suggested that “ L” be used instead of “ l” when
writing literals of type long, since it is easy to confuse the letter “ l” with the
digit “1”. end not e
To permit the smallest possible int and long values to be written as integer literals, the
following two rules exist:
When an Integer_Lit eral representing the value 2147483648 (2³¹) and no
Integer_T ype_Suf fix appears as the token immediately following a unary minus
operator token ( §12.9.3 ), the result (of both tokens) is a constant of type int with
the value −2147483648 (−2³¹). In all other situations, such an Integer_Lit eral is of
type uint.
When an Integer_Lit eral representing the value 9223372036854775808 (2⁶³) and no
Integer_T ype_Suf fix or the Integer_T ype_Suf fix L or l appears as the token
immediately following a unary minus operator token ( §12.9.3 ), the result (of both    : '0'..'9' | 'A'..'F' | 'a'..'f'
    ;
   
fragment  Binary_Integer_Literal
    : ('0b' | '0B') Decorated_Binary_Digit+ Integer_Type_Suffix?
    ;
fragment  Decorated_Binary_Digit
    : '_'* Binary_Digit
    ;
       
fragment  Binary_Digit
    : '0' | '1'
    ;tokens) is a constant of type long with the value −9223372036854775808 (−2⁶³). In
all other situations, such an Integer_Lit eral is of type ulong.
Example :
C#
end ex ample
Real literals are used to write values of types float, double, and decimal.
ANTLR123                  // decimal, int
10_543_765Lu         // decimal, ulong
1_2__3___4____5      // decimal, int
_123                 // not a numeric literal; identifier due to leading  
_
123_                 // invalid; no trailing _allowed
0xFf                 // hex, int
0X1b_a0_44_fEL       // hex, long
0x1ade_3FE1_29AaUL   // hex, ulong
0x_abc               // hex, int
_0x123               // not a numeric literal; identifier due to leading  
_
0xabc_               // invalid; no trailing _ allowed
0b101                // binary, int
0B1001_1010u         // binary, uint
0b1111_1111_0000UL   // binary, ulong
0B__111              // binary, int
__0B111              // not a numeric literal; identifier due to leading  
_
0B111__              // invalid; no trailing _ allowed
6.4.5.4 Real literals
Real_Literal
    : Decimal_Digit Decorated_Decimal_Digit* '.'
      Decimal_Digit Decorated_Decimal_Digit* Exponent_Part?  
Real_Type_Suffix?
    | '.' Decimal_Digit Decorated_Decimal_Digit* Exponent_Part?  
Real_Type_Suffix?
    | Decimal_Digit Decorated_Decimal_Digit* Exponent_Part Real_Type_Suffix?
    | Decimal_Digit Decorated_Decimal_Digit* Real_Type_Suffix
    ;
fragment  Exponent_Part
    : ('e' | 'E') Sign? Decimal_Digit Decorated_Decimal_Digit*If no Real_T ype_Suf fix is specified, the type of the Real_Lit eral is double. Otherwise, the
Real_T ype_Suf fix determines the type of the real literal, as follows:
A real literal suffixed by  F or f is of type float.
Example : The literals  1f, 1.5f, 1e10f, and 123.456F are all of type float. end
example
A real literal suffixed by  D or d is of type double.
Example : The literals  1d, 1.5d, 1e10d, and 123.456D are all of type double. end
example
A real literal suffixed by  M or m is of type decimal.
Example : The literals  1m, 1.5m, 1e10m, and 123.456M are all of type decimal.
end ex ample
This literal is converted to a decimal value by taking the exact value, and, if
necessary, rounding to the nearest representable value using banker’s
rounding ( §8.3.8 ). Any scale apparent in the literal is preserved unless the value
is rounded. Note: Hence, the literal 2.900m will be parsed to form the decimal
with sign  0, coefficient  2900, and scale  3. end not e
If the magnitude of the specified literal is too large to be represented in the indicated
type, a compile-time error occurs.
Note: In particular, a Real_Lit eral will never produce a floating-point infinity. A non-
zero Real_Lit eral may, however, be rounded to zero. end not e
The value of a real literal of type float or double is determined by using the IEC 60559
“round to nearest” mode with ties broken to “even” (a value with the least-significant-bit
zero), and all digits considered significant.    ;
fragment  Sign
    : '+' | '-'
    ;
fragment  Real_Type_Suffix
    : 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
    ;Note: In a real literal, decimal digits are always required after the decimal point. For
example, 1.3F is a real literal but 1.F is not. end not e
Example :
C#
end ex ample
A character literal represents a single character, and consists of a character in quotes, as
in 'a'.
ANTLR1.234_567      // double
.3e5f          // float
2_345E-2_0     // double
15D            // double
19.73M         // decimal
1.F            // parsed as a member access of F due to non-digit after  
.
1_.2F          // invalid; no trailing _ allowed in integer part
1._234         // parsed as a member access of _234 due to non-digit  
after .
1.234_         // invalid; no trailing _ allowed in fraction
.3e_5F         // invalid; no leading _ allowed in exponent
.3e5_F         // invalid; no trailing _ allowed in exponent
6.4.5.5 Character literals
Character_Literal
    : '\'' Character '\''
    ;
    
fragment  Character
    : Single_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    ;
    
fragment  Single_Character
    // anything but ', \, and New_Line_Character
    : ~['\\\u000D\u000A\u0085\u2028\u2029]
    ;
    
fragment Simple_Escape_Sequence
    : '\\\'' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' |
      '\\f' | '\\n' | '\\r' | '\\t' | '\\v'
    ;Note: A character that follows a backslash character ( \) in a Char acter must be one
of the following characters: ', ", \, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a
compile-time error occurs. end not e
Note: The use of the \x Hexadecimal_Es cape_Sequenc e production can be error-
prone and hard to read due to the variable number of hexadecimal digits following
the \x. For example, in the code:
C#
it might appear at first that the leading character is the same ( U+0009, a tab
character) in both strings. In fact the second string starts with U+9BAD as all three
letters in the word “Bad” are valid hexadecimal digits. As a matter of style, it is
recommended that \x is avoided in favour of either specific escape sequences ( \t
in this example) or the fixed-length \u escape sequence.
end not e
A hexadecimal escape sequence represents a single Unicode UTF-16 code unit, with the
value formed by the hexadecimal number following “ \x”.
If the value represented by a character literal is greater than U+FFFF, a compile-time
error occurs.
A Unicode escape sequence ( §6.4.2 ) in a character literal shall be in the range U+0000 to
U+FFFF.
A simple escape sequence represents a Unicode character, as described in the table
below.
Escape sequence Charact er name Unicode code point
\' Single quote U+0027
\" Double quote U+0022    
fragment  Hexadecimal_Escape_Sequence
    : '\\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
    ;
string good = "x9Good text" ;
string bad = "x9Bad text" ;Escape sequence Charact er name Unicode code point
\\ Backslash U+005C
\0 Null U+0000
\a Alert U+0007
\b Backspace U+0008
\f Form feed U+000C
\n New line U+000A
\r Carriage return U+000D
\t Horizontal tab U+0009
\v Vertical tab U+000B
The type of a Char acter_Lit eral is char.
C# supports two forms of string literals: regular str ing lit erals and verbatim str ing
literals. A regular string literal consists of zero or more characters enclosed in double
quotes, as in "hello", and can include both simple escape sequences (such as \t for
the tab character), and hexadecimal and Unicode escape sequences.
A verbatim string literal consists of an @ character followed by a double-quote
character, zero or more characters, and a closing double-quote character.
Example : A simple example is @"hello". end ex ample
In a verbatim string literal, the characters between the delimiters are interpreted
verbatim, with the only exception being a Quot e_Escape_Sequenc e, which represents one
double-quote character. In particular, simple escape sequences, and hexadecimal and
Unicode escape sequences are not processed in verbatim string literals. A verbatim
string literal may span multiple lines.
ANTLR6.4.5.6 String literals
String_Literal
    : Regular_String_Literal
    | Verbatim_String_Literal
    ;Example : The example
C#    
fragment  Regular_String_Literal
    : '"' Regular_String_Literal_Character* '"'
    ;
    
fragment  Regular_String_Literal_Character
    : Single_Regular_String_Literal_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    ;
fragment  Single_Regular_String_Literal_Character
    // anything but ", \, and New_Line_Character
    : ~["\\\u000D\u000A\u0085\u2028\u2029]
    ;
fragment  Verbatim_String_Literal
    : '@"' Verbatim_String_Literal_Character* '"'
    ;
    
fragment  Verbatim_String_Literal_Character
    : Single_Verbatim_String_Literal_Character
    | Quote_Escape_Sequence
    ;
    
fragment  Single_Verbatim_String_Literal_Character
    : ~["]     // anything but quotation mark (U+0022)
    ;
    
fragment  Quote_Escape_Sequence
    : '""'
    ;
string a = "Happy birthday, Joel" ; // Happy birthday, Joel
string b = @"Happy birthday, Joel" ; // Happy birthday, Joel
string c = "hello \t world" ; // hello world
string d = @"hello \t world" ; // hello \t world
string e = "Joe said \"Hello\" to me" ; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me" ; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt" ; // \\server\share\file.txt
string h = @"\\server\share\file.txt" ; // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree" ;
string j = @"one
two
three";shows a variety of string literals. The last string literal, j, is a verbatim string literal
that spans multiple lines. The characters between the quotation marks, including
white space such as new line characters, are preserved verbatim, and each pair of
double-quote characters is replaced by one such character.
end ex ample
Note: Any line breaks within verbatim string literals are part of the resulting string. If
the exact characters used to form line breaks are semantically relevant to an
application, any tools that translate line breaks in source code to different formats
(between “ \n” and “\r\n”, for example) will change application behavior.
Developers should be careful in such situations. end not e
Note: Since a hexadecimal escape sequence can have a variable number of hex
digits, the string literal "\x123" contains a single character with hex value 123. To
create a string containing the character with hex value 12 followed by the
character  3, one could write "\x00123" or "\x12" + "3" instead. end not e
The type of a String_Lit eral is string.
Each string literal does not necessarily result in a new string instance. When two or more
string literals that are equivalent according to the string equality operator ( §12.12.8 ),
appear in the same assembly, these string literals refer to the same string instance.
Example : For instance, the output produced by
C#
is True because the two literals refer to the same string instance.
end ex ampleclass Test
{
    static void Main()
    {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
6.4.5.7 The null literalANTLR
Note: null_lit eral is a parser rule as it does not introduce a new token kind. end not e
A null_lit eral represents a null value. It does not have a type, but can be converted to
any reference type or nullable value type through a null literal conversion ( §10.2.7 ).
There are several kinds of operators and punctuators. Operators are used in expressions
to describe operations involving one or more operands.
Example : The expression a + b uses the + operator to add the two operands a
and b. end ex ample
Punctuators are for grouping and separating.
ANTLR
Note: right_shi ft and right_shi ft_assignment  are parser rules as they do not introduce
a new token kind but represent a sequence of two tokens. The
operator_or_punctuat or rule exists for descriptive purposes only and is not used
elsewhere in the grammar. end not enull_literal
    : NULL
    ;
6.4.6 Operators and punctuators
operator_or_punctuator
    : '{'  | '}'  | '['  | ']'  | '('   | ')'  | '.'  | ','  | ':'  | ';'
    | '+'  | '-'  | ASTERISK    | SLASH | '%'  | '&'  | '|'  | '^'  | '!' | 
'~'
    | '='  | '<'  | '>'  | '?'  | '??'  | '::' | '++' | '--' | '&&' | '||'
    | '->' | '==' | '!=' | '<=' | '>='  | '+=' | '-=' | '*=' | '/=' | '%='
    | '&=' | '|=' | '^=' | '<<' | '<<=' | '=>'
    ;
right_shift
    : '>'  '>'
    ;
right_shift_assignment
    : '>' '>='
    ;right_shi ft is made up of the two tokens > and >. Similarly, right_shi ft_assignment  is
made up of the two tokens > and >=. Unlike other productions in the syntactic
grammar, no characters of any kind (not even whitespace) are allowed between the two
tokens in each of these productions. These productions are treated specially in order to
enable the correct handling of type_p aramet er_lists  (§15.2.3 ).
Note: Prior to the addition of generics to C#, >> and >>= were both single tokens.
However, the syntax for generics uses the < and > characters to delimit type
parameters and type arguments. It is often desirable to use nested constructed
types, such as List<Dictionary<string, int>>. Rather than requiring the
programmer to separate the > and > by a space, the definition of the two
operator_or_punctuat ors was changed. end not e
The pre-processing directives provide the ability to conditionally skip sections of
compilation units, to report error and warning conditions, and to delineate distinct
regions of source code.
Note: The term “pre-processing directives” is used only for consistency with the C
and C++ programming languages. In C#, there is no separate pre-processing step;
pre-processing directives are processed as part of the lexical analysis phase. end
note
ANTLR6.5 Pre-processing directives
6.5.1 General
PP_Directive
    : PP_Start PP_Kind PP_New_Line
    ;
fragment  PP_Kind
    : PP_Declaration
    | PP_Conditional
    | PP_Line
    | PP_Diagnostic
    | PP_Region
    | PP_Pragma
    ;
// Only recognised at the beginning of a line
fragment  PP_Start
    // See note below.Note:
The pre-processor grammar defines a single lexical token PP_Directive used
for all pre-processing directives. The semantics of each of the pre-processing
directives are defined in this language specification but not how to implement
them.
The PP_Start fragment must only be recognised at the start of a line, the
getCharPositionInLine() == 0 ANTLR lexical predicate above suggests one
way in which this may be achieved and is informative only, an implementation
may use a different strategy.
end not e
The following pre-processing directives are available:
#define and #undef, which are used to define and undefine, respectively,
conditional compilation symbols ( §6.5.4 ).
#if, #elif, #else, and #endif, which are used to skip conditionally sections of
source code ( §6.5.5 ).
#line, which is used to control line numbers emitted for errors and warnings
(§6.5.8 ).
#error, which is used to issue errors ( §6.5.6 ).
#region and #endregion, which are used to explicitly mark sections of source code
(§6.5.7 ).
#pragma, which is used to specify optional contextual information to a compiler
(§6.5.9 ).
A pre-processing directive always occupies a separate line of source code and always
begins with a # character and a pre-processing directive name. White space may occur    : { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace?
    ;
fragment  PP_Whitespace
    : ( [\p{Zs}]  // any character with Unicode class Zs
      | '\u0009'   // horizontal tab
      | '\u000B'   // vertical tab
      | '\u000C'   // form feed
      )+
    ;
fragment  PP_New_Line
    : PP_Whitespace? Single_Line_Comment? New_Line
    ;before the # character and between the # character and the directive name.
A source line containing a #define, #undef, #if, #elif, #else, #endif, #line, or
#endregion directive can end with a single-line comment. Delimited comments (the /*
*/ style of comments) are not permitted on source lines containing pre-processing
directives.
Pre-processing directives are not part of the syntactic grammar of C#. However, pre-
processing directives can be used to include or exclude sequences of tokens and can in
that way affect the meaning of a C# program.
Example : When compiled, the program
C#
results in the exact same sequence of tokens as the program
C#
Thus, whereas lexically, the two programs are quite different, syntactically, they are
identical.
end ex ample#define A
#undef B
class C
{
#if A
    void F() {}
#else
    void G() {}
#endif
#if B
    void H() {}
#else    
    void I() {}
#endif
}
class C
{
    void F() {}
    void I() {}
}
6.5.2 Conditional compilation symbolsThe conditional compilation functionality provided by the #if, #elif, #else, and
#endif directives is controlled through pre-processing expressions ( §6.5.3 ) and
conditional compilation symbols.
ANTLR
Note How an implementation enforces the restriction on the allowable
Basic_Identi fier values is an implementation issue. end not e
