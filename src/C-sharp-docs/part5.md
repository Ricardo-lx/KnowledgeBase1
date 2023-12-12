declared member.
C# Programming Guide
Introduction to Generics
interface
Genericsinterface  IBaseInterface1 <T> { } 
interface  IBaseInterface2 <T, U> { } 
class SampleClass1 <T> : IBaseInterface1 <T> { }          //No error  
class SampleClass2 <T> : IBaseInterface2 <T, string> { }  //No error  
See alsoGeneric metho ds (C# programming
guide)
Article •04/12/2023
A generic method is a method that is declared with type parameters, as follows:
C#
The following code example shows one way to call the method by using int for the
type argument:
C#
You can also omit the type argument and the compiler will infer it. The following call to
Swap is equivalent to the previous call:
C#
The same rules for type inference apply to static methods and instance methods. The
compiler can infer the type parameters based on the method arguments you pass in; it
cannot infer the type parameters only from a constraint or return value. Therefore type
inference does not work with methods that have no parameters. T ype inference occurs
at compile time before the compiler tries to resolve overloaded method signatures. The
compiler applies type inference logic to all generic methods that share the same name.static void Swap<T>( ref T lhs, ref T rhs) 
{ 
    T temp;  
    temp = lhs;  
    lhs = rhs;  
    rhs = temp;  
} 
public static void TestSwap () 
{ 
    int a = 1; 
    int b = 2; 
    Swap< int>(ref a, ref b); 
    System.Console.WriteLine(a + " " + b); 
} 
Swap(ref a, ref b); In the overload resolution step, the compiler includes only those generic methods on
which type inference succeeded.
Within a generic class, non-generic methods can access the class-level type parameters,
as follows:
C#
If you define a generic method that takes the same type parameters as the containing
class, the compiler generates warning CS0693  because within the method scope, the
argument supplied for the inner T hides the argument supplied for the outer T. If you
require the flexibility of calling a generic class method with type arguments other than
the ones provided when the class was instantiated, consider providing another identifier
for the type parameter of the method, as shown in GenericList2<T> in the following
example.
C#
Use constraints to enable more specialized operations on type parameters in methods.
This version of Swap<T>, now named SwapIfGreater<T>, can only be used with type
arguments that implement IComparable<T> .
C#class SampleClass <T> 
{ 
    void Swap(ref T lhs, ref T rhs) { } 
} 
class GenericList <T> 
{ 
    // CS0693.  
    void SampleMethod<T>() { }  
} 
class GenericList2 <T> 
{ 
    // No warning.  
    void SampleMethod<U>() { }  
} 
void SwapIfGreater<T>( ref T lhs, ref T rhs) where T : System.IComparable<T>  
{ 
    T temp;  
    if (lhs.CompareTo(rhs) > 0) 
    { 
        temp = lhs;  Generic methods can be overloaded on several type parameters. For example, the
following methods can all be located in the same class:
C#
For more information, see the C# Language Specification .
System.Collections.Generic
C# Programming Guide
Introduction to Generics
Methods        lhs = rhs;  
        rhs = temp;  
    } 
} 
void DoWork() { } 
void DoWork<T>() { }  
void DoWork<T, U>() { }  
C# Language Specification
See alsoGenerics and Arrays (C# Programming
Guide)
Article •09/29/2022
Single-dimensional arrays that have a lower bound of zero automatically implement
IList<T> . This enables you to create generic methods that can use the same code to
iterate through arrays and other collection types. This technique is primarily useful for
reading data in collections. The IList<T>  interface cannot be used to add or remove
elements from an array. An exception will be thrown if you try to call an IList<T>
method such as RemoveAt  on an array in this context.
The following code example demonstrates how a single generic method that takes an
IList<T>  input parameter can iterate through both a list and an array, in this case an
array of integers.
C#
class Program
{
    static void Main()
    {
        int[] arr = { 0, 1, 2, 3, 4 };
        List<int> list = new List<int>();
        for (int x = 5; x < 10; x++)
        {
            list.Add(x);
        }
        ProcessItems< int>(arr);
        ProcessItems< int>(list);
    }
    static void ProcessItems<T>(IList<T> coll)
    {
        // IsReadOnly returns True for the array and False for the List.
        System.Console.WriteLine
            ("IsReadOnly returns {0} for this collection." ,
            coll.IsReadOnly);
        // The following statement causes a run-time exception for the
        // array, but not for the List.
        //coll.RemoveAt(4);
        foreach (T item in coll)
        {
            System.Console.Write(item?.ToString() + " ");
        }System.Collections.Generic
C# Programming Guide
Generics
Arrays
Generics        System.Console.WriteLine();
    }
}
See alsoGeneric Delegates (C# Programming
Guide)
Article •09/15/2021
A delegate  can define its own type parameters. Code that references the generic
delegate can specify the type argument to create a closed constructed type, just like
when instantiating a generic class or calling a generic method, as shown in the following
example:
C#
C# version 2.0 has a new feature called method group conversion, which applies to
concrete as well as generic delegate types, and enables you to write the previous line
with this simplified syntax:
C#
Delegates defined within a generic class can use the generic class type parameters in the
same way that class methods do.
C#
Code that references the delegate must specify the type argument of the containing
class, as follows:
C#public delegate  void Del<T>(T item);  
public static void Notify(int i) { } 
Del<int> m1 = new Del<int>(Notify);  
Del<int> m2 = Notify;  
class Stack<T> 
{ 
    public delegate  void StackDelegate (T[] items ); 
} 
private static void DoWork(float[] items ) { } 
public static void TestStack () 
{ Generic delegates are especially useful in defining events based on the typical design
pattern because the sender argument can be strongly typed and no longer has to be
cast to and from Object .
C#
System.Collections.Generic
C# Programming Guide
Introduction to Generics
Generic Methods
Generic Classes
Generic Interfaces
Delegates
Generics    Stack< float> s = new Stack<float>(); 
    Stack< float>.StackDelegate d = DoWork;  
} 
delegate  void StackEventHandler<T, U>(T sender, U eventArgs);  
class Stack<T> 
{ 
    public class StackEventArgs  : System.EventArgs  { } 
    public event StackEventHandler<Stack<T>, StackEventArgs>? StackEvent;  
    protected  virtual void OnStackChanged (StackEventArgs a ) 
    { 
        if (StackEvent is not null) 
            StackEvent( this, a); 
    } 
} 
class SampleClass  
{ 
    public void HandleStackChange<T>(Stack<T> stack, Stack<T>.StackEventArgs  
args) { }  
} 
public static void Test() 
{ 
    Stack< double> s = new Stack<double>(); 
    SampleClass o = new SampleClass();  
    s.StackEvent += o.HandleStackChange;  
} 
See alsoDifferences Between C++ Templates
and C# Gen erics (C# Programming
Guide)
Article •05/04/2023
C# Generics and C++ templates are both language features that provide support for
parameterized types. However, there are many differences between the two. At the
syntax level, C# generics are a simpler approach to parameterized types without the
complexity of C++ templates. In addition, C# does not attempt to provide all of the
functionality that C++ templates provide. At the implementation level, the primary
difference is that C# generic type substitutions are performed at run time and generic
type information is thereby preserved for instantiated objects. For more information, see
Generics in the Runtime .
The following are the key differences between C# Generics and C++ templates:
C# generics do not provide the same amount of flexibility as C++ templates. For
example, it is not possible to call arithmetic operators in a C# generic class,
although it is possible to call user defined operators.
C# does not allow non-type template parameters, such as template C<int i> {}.
C# does not support explicit specialization; that is, a custom implementation of a
template for a specific type.
C# does not support partial specialization: a custom implementation for a subset
of the type arguments.
C# does not allow the type parameter to be used as the base class for the generic
type.
C# does not allow type parameters to have default types.
In C#, a generic type parameter cannot itself be a generic, although constructed
types can be used as generics. C++ does allow template parameters.
C++ allows code that might not be valid for all type parameters in the template,
which is then checked for the specific type used as the type parameter. C# requires
code in a class to be written in such a way that it will work with any type that
satisfies the constraints. For example, in C++ it is possible to write a function that
uses the arithmetic operators + and - on objects of the type parameter, which willproduce an error at the time of instantiation of the template with a type that does
not support these operators. C# disallows this; the only language constructs
allowed are those that can be deduced from the constraints.
C# Programming Guide
Introduction to Generics
TemplatesSee alsoGenerics in the runtime (C#
programming guide)
Article •04/28/2023
When a generic type or method is compiled into Microsoft intermediate language
(MSIL), it contains metadata that identifies it as having type parameters. How the MSIL
for a generic type is used differs based on whether the supplied type parameter is a
value type or reference type.
When a generic type is first constructed with a value type as a parameter, the runtime
creates a specialized generic type with the supplied parameter or parameters
substituted in the appropriate locations in the MSIL. Specialized generic types are
created one time for each unique value type that is used as a parameter.
For example, suppose your program code declared a stack that's constructed of
integers:
C#
At this point, the runtime generates a specialized version of the Stack<T>  class that has
the integer substituted appropriately for its parameter. Now, whenever your program
code uses a stack of integers, the runtime reuses the generated specialized Stack<T>
class. In the following example, two instances of a stack of integers are created, and they
share a single instance of the Stack<int> code:
C#
However, suppose that another Stack<T>  class with a different value type such as a
long or a user-defined structure as its parameter is created at another point in your
code. As a result, the runtime generates another version of the generic type and
substitutes a long in the appropriate locations in MSIL. Conversions are no longer
necessary because each specialized generic class natively contains the value type.
Generics work somewhat differently for reference types. The first time a generic type is
constructed with any reference type, the runtime creates a specialized generic type with
object references substituted for the parameters in the MSIL. Then, every time that aStack<int>? stack;  
Stack<int> stackOne = new Stack<int>(); 
Stack<int> stackTwo = new Stack<int>(); constructed type is instantiated with a reference type as its parameter, regardless of
what type it is, the runtime reuses the previously created specialized version of the
generic type. This is possible because all references are the same size.
For example, suppose you had two reference types, a Customer class and an Order class,
and also suppose that you created a stack of Customer types:
C#
C#
At this point, the runtime generates a specialized version of the Stack<T>  class that
stores object references that will be filled in later instead of storing data. Suppose the
next line of code creates a stack of another reference type, which is named Order:
C#
Unlike with value types, another specialized version of the Stack<T>  class is not created
for the Order type. Instead, an instance of the specialized version of the Stack<T>  class
is created and the orders variable is set to reference it. Suppose that you then
encountered a line of code to create a stack of a Customer type:
C#
As with the previous use of the Stack<T>  class created by using the Order type, another
instance of the specialized Stack<T>  class is created. The pointers that are contained
therein are set to reference an area of memory the size of a Customer type. Because the
number of reference types can vary wildly from program to program, the C#
implementation of generics greatly reduces the amount of code by reducing to one the
number of specialized classes created by the compiler for generic classes of reference
types.class Customer  { } 
class Order { } 
Stack<Customer> customers;  
Stack<Order> orders = new Stack<Order>();  
customers = new Stack<Customer>();  Moreover, when a generic C# class is instantiated by using a value type or reference
type parameter, reflection can query it at run time and both its actual type and its type
parameter can be ascertained.
System.Collections.Generic
C# Programming Guide
Introduction to Generics
GenericsSee alsoC# reference
Article •06/21/2023
This section provides reference material about C# keywords, operators, special
characters, preprocessor directives, compiler options, and compiler errors and warnings.
C# types
C# keywords  
Provides links to information about C# keywords and syntax.
C# operators  
Provides links to information about C# operators and syntax.
C# statements
C# special characters  
Provides links to information about special contextual characters in C# and their usage.
C# attributes
C# preprocessor directives  
Provides links to information about compiler commands for embedding in C# source
code.
C# compiler options  
Includes information about compiler options and how to use them.
XML documentation comments
C# compiler errors  
Includes code snippets that demonstrate the cause and correction of C# compiler errors
and warnings.
C# standard specification  The latest C# standard draft, as created by the ECMA
committee. The feature specifications for those features implemented in newer
language versions.In this section
Related sectionsUsing the Visual S tudio development environment for C#  
Provides links to conceptual and task topics that describe the IDE and editor.
C# programming guide  
Includes information about how to use the C# programming language.C# language versioning
Article •11/01/2023
The latest C# compiler determines a default language version based on your project's
target framework or frameworks. Visual S tudio doesn't provide a UI to change the value,
but you can change it by editing the csproj file. The choice of default ensures that you
use the latest language version compatible with your target framework. Y ou benefit
from access to the latest language features compatible with your project's target. This
default choice also ensures you don't use a language that requires types or runtime
behavior not available in your target framework. Choosing a language version newer
than the default can cause hard to diagnose compile-time and runtime errors.
C# 12  is supported only on .NET 8 and newer versions. C# 11  is supported only on .NET
7 and newer versions. C# 10  is supported only on .NET 6 and newer versions.
Check the Visual S tudio platform compatibility  page for details on which .NET versions
are supported by versions of Visual S tudio. Check the Visual S tudio for Mac platform
compatibility  page for details on which .NET versions are supported by versions of
Visual S tudio for Mac. Check the Mono page for C#  for Mono compatibility with C#
versions.
The compiler determines a default based on these rules:
Target Version C# language v ersion default
.NET 7.x C# 11
.NET 6.x C# 10
.NET 5.x C# 9.0
.NET Core 3.x C# 8.0
.NET Core 2.x C# 7.3
.NET S tandard 2.1 C# 8.0
.NET S tandard 2.0 C# 7.3
.NET S tandard 1.x C# 7.3
.NET Framework all C# 7.3
DefaultsIf your project targets a preview framework that has a corresponding preview language
version, the language version used is the preview language version. Y ou use the latest
features with that preview in any environment, without affecting projects that target a
released .NET Core version.
If you must specify your C# version explicitly, you can do so in several ways:
Manually edit your project file .
Set the language version for multiple projects in a subdirectory .
Configure the LangV ersion compiler option .
You can set the language version in your project file. For example, if you explicitly want
access to preview features, add an element like this:
XML） Impor tant
The new project template for Visual S tudio 2017 added a
<LangVersion>latest</LangVersion> entry to new project files. If you upgrade the
target framework for these projects, the <LangVersion> setting can override the
default  for the new target framework. Be sure to remove the
<LangVersion>latest</LangVersion> from your project file to ensure your project
uses the recommended compiler version for your target framework. Y ou can
update the target framework to access newer language features.
Override the default
 Tip
You can see the language version in Visual S tudio in the project properties page.
Under the Build  tab, the Advanced pane displays the version selected.
To know what language version you're currently using, put #error version (case
sensitive) in your code. This makes the compiler report a compiler error, CS8304,
with a message containing the compiler version being used and the current
selected language version. See #error (C# R eference)  for more information.
Edit the project fileThe value preview uses the latest available preview C# language version that your
compiler supports.
To configure multiple projects, you can create a Directory.Build.pr ops file, typically in
your solution directory, that contains the <LangVersion> element. Add the following
setting to the Directory.Build.pr ops file:
XML
Builds in all subdirectories of the directory containing that file now use the preview C#
version. For more information, see Customize your build .
The following table shows all current C# language versions. Older compilers might not
understand every value. If you install the latest .NET SDK, you have access to everything
listed.
Value Meaning
preview The compiler accepts all valid language syntax from the latest preview version.
latest The compiler accepts syntax from the latest released version of the compiler
(including minor version).
latestMajor
or defaultThe compiler accepts syntax from the latest released major version of the compiler.
12.0 The compiler accepts only syntax that is included in C# 12 or lower.
11.0 The compiler accepts only syntax that is included in C# 11 or lower.
10.0 The compiler accepts only syntax that is included in C# 10 or lower.<PropertyGroup >
   <LangVersion >preview</LangVersion >
</PropertyGroup >
Configure multiple projects
<Project>
 <PropertyGroup >
   <LangVersion >preview</LangVersion >
 </PropertyGroup >
</Project>
C# language version referenceValue Meaning
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
(1.0/1.2).
７ Note
Specifying LangV ersion with the default value is different from omitting the
LangV ersion option. Specifying default uses the latest version of the language
that the compiler supports, without taking into account the target framework. For
example, building a project that targets .NET 6 from the current version of Visual
Studio 2022 uses C# 10 if LangV ersion isn't specified, but uses C# 11 if
LangV ersion is set to default.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For.NET feedb ack
The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackmore information, see our
contributor guide .Value types (C# reference)
Article •09/29/2022
Value types  and reference types  are the two main categories of C# types. A variable of a
value type contains an instance of the type. This differs from a variable of a reference
type, which contains a reference to an instance of the type. By default, on assignment ,
passing an argument to a method, and returning a method result, variable values are
copied. In the case of value-type variables, the corresponding type instances are copied.
The following example demonstrates that behavior:
C#
using System;  
public struct MutablePoint  
{ 
    public int X; 
    public int Y; 
    public MutablePoint (int x, int y) => (X, Y) = (x, y);  
    public override  string ToString () => $"({X}, {Y})"; 
} 
public class Program 
{ 
    public static void Main() 
    { 
        var p1 = new MutablePoint( 1, 2); 
        var p2 = p1;  
        p2.Y = 200; 
        Console.WriteLine( $"{nameof(p1)} after {nameof(p2)} is modified:  
{p1}"); 
        Console.WriteLine( $"{nameof(p2)}: {p2}"); 
        MutateAndDisplay(p2);  
        Console.WriteLine( $"{nameof(p2)} after passing to a method: {p2}"); 
    } 
    private static void MutateAndDisplay (MutablePoint p ) 
    { 
        p.X = 100; 
        Console.WriteLine( $"Point mutated in a method: {p}"); 
    } 
} 
// Expected output:  
// p1 after p2 is modified: (1, 2)  
// p2: (1, 200)  
// Point mutated in a method: (100, 200)  
// p2 after passing to a method: (1, 200)  As the preceding example shows, operations on a value-type variable affect only that
instance of the value type, stored in the variable.
If a value type contains a data member of a reference type, only the reference to the
instance of the reference type is copied when a value-type instance is copied. Both the
copy and original value-type instance have access to the same reference-type instance.
The following example demonstrates that behavior:
C#
using System;  
using System.Collections.Generic;
public struct TaggedInteger  
{ 
    public int Number;  
    private List<string> tags; 
    public TaggedInteger (int n) 
    { 
        Number = n;  
        tags = new List<string>(); 
    } 
    public void AddTag(string tag) => tags.Add(tag);  
    public override  string ToString () => $"{Number}  [{string.Join(", ", 
tags)}]"; 
} 
public class Program 
{ 
    public static void Main() 
    { 
        var n1 = new TaggedInteger( 0); 
        n1.AddTag( "A"); 
        Console.WriteLine(n1);  // output: 0 [A]  
        var n2 = n1;  
        n2.Number = 7; 
        n2.AddTag( "B"); 
        Console.WriteLine(n1);  // output: 0 [A, B]  
        Console.WriteLine(n2);  // output: 7 [A, B]  
    } 
} 
７ NoteA value type can be one of the two following kinds:
a structure type , which encapsulates data and related functionality
an enumeration type , which is defined by a set of named constants and represents
a choice or a combination of choices
A nullable value type  T? represents all values of its underlying value type T and an
additional null value. Y ou cannot assign null to a variable of a value type, unless it's a
nullable value type.
You can use the struct  constraint  to specify that a type parameter is a non-nullable value
type. Both structure and enumeration types satisfy the struct constraint. Y ou can use
System.Enum in a base class constraint (that is known as the enum constraint ) to specify
that a type parameter is an enumeration type.
C# provides the following built-in value types, also known as simple types :
Integral numeric types
Floating-point numeric types
bool that represents a Boolean value
char that represents a Unicode UTF-16 character
All simple types are structure types and differ from other structure types in that they
permit certain additional operations:
You can use literals to provide a value of a simple type. For example, 'A' is a literal
of the type char and 2001 is a literal of the type int.
You can declare constants of the simple types with the const  keyword. It's not
possible to have constants of other structure types.
Constant expressions, whose operands are all constants of the simple types, are
evaluated at compile time.
A value tuple  is a value type, but not a simple type.To make your code less error-prone and more robust, define and use immutable
value types. This article uses mutable value types only for demonstration purposes.
Kinds of value types and type constraints
Built-in value typesFor more information, see the following sections of the C# language specification :
Value types
Simple types
Variables
C# reference
System.V alueT ype
Reference typesC# language specification
See alsoIntegral numeric types (C# reference)
Article •09/29/2022
The integral numer ic types  represent integer numbers. All integral numeric types are
value types . They're also simple types  and can be initialized with literals . All integral
numeric types support arithmetic , bitwise logical , comparison , and equality  operators.
C# supports the following predefined integral types:
C#
type/k eywordRange Size .NET type
sbyte -128 to 127 Signed 8-bit
integerSystem.SByte
byte 0 to 255 Unsigned 8-bit
integerSystem.Byte
short -32,768 to 32,767 Signed 16-bit
integerSystem.Int16
ushort 0 to 65,535 Unsigned 16-bit
integerSystem.UInt16
int -2,147,483,648 to 2,147,483,647 Signed 32-bit
integerSystem.Int32
uint 0 to 4,294,967,295 Unsigned 32-bit
integerSystem.UInt32
long -9,223,372,036,854,775,808 to
9,223,372,036,854,775,807Signed 64-bit
integerSystem.Int64
ulong 0 to 18,446,744,073,709,551,615 Unsigned 64-bit
integerSystem.UInt64
nint Depends on platform (computed at
runtime)Signed 32-bit or
64-bit integerSystem.IntPtr
nuint Depends on platform (computed at
runtime)Unsigned 32-bit or
64-bit integerSystem.UIntPtr
In all of the table rows except the last two, each C# type keyword from the leftmost
column is an alias for the corresponding .NET type. The keyword and .NET type nameCharacteristics of the integral typesare interchangeable. For example, the following declarations declare variables of the
same type:
C#
The nint and nuint types in the last two rows of the table are native-sized integers. Y ou
can use the nint and nuint keywords to define nativ e-sized int egers. These are 32-bit
integers when running in a 32-bit process, or 64-bit integers when running in a 64-bit
process. They can be used for interop scenarios, low-level libraries, and to optimize
performance in scenarios where integer math is used extensively.
The native-sized integer types are represented internally as the .NET types System.IntPtr
and System.UIntPtr . Starting in C# 11, the nint and nuint types are aliases for the
underlying types.
The default value of each integral type is zero, 0.
Each of the integral types has MinValue and MaxValue properties that provide the
minimum and maximum value of that type. These properties are compile-time constants
except for the case of the native-sized types ( nint and nuint). The MinValue and
MaxValue properties are calculated at runtime for native-sized types. The sizes of those
types depend on the process settings.
Use the System.Numerics.BigInteger  structure to represent a signed integer with no
upper or lower bounds.
Integer literals can be
decimal : without any prefix
hexadecimal : with the 0x or 0X prefix
binar y: with the 0b or 0B prefix
The following code demonstrates an example of each:
C#int a = 123;
System.Int32 b = 123;
Integer literals
var decimalLiteral = 42;
var hexLiteral = 0x2A;The preceding example also shows the use of _ as a digit s eparator. You can use the
digit separator with all kinds of numeric literals.
The type of an integer literal is determined by its suffix as follows:
If the literal has no suffix, its type is the first of the following types in which its
value can be represented: int, uint, long, ulong.
If the literal is suffixed by U or u, its type is the first of the following types in which
its value can be represented: uint, ulong.
If the literal is suffixed by L or l, its type is the first of the following types in which
its value can be represented: long, ulong.
If the literal is suffixed by UL, Ul, uL, ul, LU, Lu, lU, or lu, its type is ulong.
If the value represented by an integer literal exceeds UInt64.MaxV alue, a compiler error
CS1021  occurs.
If the determined type of an integer literal is int and the value represented by the
literal is within the range of the destination type, the value can be implicitly converted to
sbyte, byte, short, ushort, uint, ulong, nint or nuint:
C#var binaryLiteral = 0b_0010_1010;
７ Note
Literals are interpreted as positive values. For example, the literal
0xFF_FF_FF_FF represents the number 4294967295 of the uint type, though it
has the same bit representation as the number -1 of the int type. If you
need a value of a certain type, cast a literal to that type. Use the unchecked
operator, if a literal value cannot be represented in the target type. For
example, unchecked((int)0xFF_FF_FF_FF) produces -1.
７ Note
You can use the lowercase letter l as a suffix. However, this generates a
compiler warning because the letter l can be confused with the digit 1. Use
L for clarity.As the preceding example shows, if the literal's value isn't within the range of the
destination type, a compiler error CS0031  occurs.
You can also use a cast to convert the value represented by an integer literal to the type
other than the determined type of the literal:
C#
You can convert any integral numeric type to any other integral numeric type. If the
destination type can store all values of the source type, the conversion is implicit.
Otherwise, you need to use a cast expression  to perform an explicit conversion. For
more information, see Built-in numeric conversions .
Native sized integer types have special behavior because the storage is determined by
the natural integer size on the target machine.
To get the size of a native-sized integer at run time, you can use sizeof().
However, the code must be compiled in an unsafe context. For example:
C#byte a = 17;
byte b = 300;   // CS0031: Constant value '300' cannot be converted to a  
'byte'
var signedByte = ( sbyte)42;
var longVariable = ( long)42;
Conversions
Native sized integers
Console.WriteLine( $"size of nint = {sizeof(nint)}");
Console.WriteLine( $"size of nuint = {sizeof(nuint)}");
// output when run in a 64-bit process
//size of nint = 8
//size of nuint = 8
// output when run in a 32-bit process
//size of nint = 4
//size of nuint = 4You can also get the equivalent value from the static IntPtr.Size  and UIntPtr.Size
properties.
To get the minimum and maximum values of native-sized integers at run time, use
MinValue and MaxValue as static properties with the nint and nuint keywords, as
in the following example:
C#
You can use constant values in the following ranges:
For nint: Int32.MinV alue to Int32.MaxV alue.
For nuint: UInt32.MinV alue to UInt32.MaxV alue.
The compiler provides implicit and explicit conversions to other numeric types. For
more information, see Built-in numeric conversions .
There's no direct syntax for native-sized integer literals. There's no suffix to indicate
that a literal is a native-sized integer, such as L to indicate a long. You can use
implicit or explicit casts of other integer values instead. For example:
C#
For more information, see the following sections of the C# language specification :Console.WriteLine( $"nint.MinValue = {nint.MinValue} ");
Console.WriteLine( $"nint.MaxValue = {nint.MaxValue} ");
Console.WriteLine( $"nuint.MinValue = {nuint.MinValue} ");
Console.WriteLine( $"nuint.MaxValue = {nuint.MaxValue} ");
// output when run in a 64-bit process
//nint.MinValue = -9223372036854775808
//nint.MaxValue = 9223372036854775807
//nuint.MinValue = 0
//nuint.MaxValue = 18446744073709551615
// output when run in a 32-bit process
//nint.MinValue = -2147483648
//nint.MaxValue = 2147483647
//nuint.MinValue = 0
//nuint.MaxValue = 4294967295
nint a = 42
nint a = (nint)42;
C# language specificationIntegral types
Integer literals
Native sized integral types
C# 11 - Numeric IntPtr  and `UIntPtr
C# reference
Value types
Floating-point types
Standard numeric format strings
Numerics in .NETSee also
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
 Provide product feedbackFloating-point numeric types (C#
reference)
Article •09/29/2022
The floating-point numer ic types  represent real numbers. All floating-point numeric
types are value types . They are also simple types  and can be initialized with literals . All
floating-point numeric types support arithmetic , comparison , and equality  operators.
C# supports the following predefined floating-point types:
C# type/k eywordAppr oximat e range Precision Size .NET type
float ±1.5 x 10  to ±3.4 x 10 ~6-9 digits 4 bytes System.Single
double ±5.0 × 10  to ±1.7 × 10 ~15-17 digits 8 bytes System.Double
decimal ±1.0 x 10  to ±7.9228 x 10 28-29 digits 16 bytes System.Decimal
In the preceding table, each C# type keyword from the leftmost column is an alias for
the corresponding .NET type. They are interchangeable. For example, the following
declarations declare variables of the same type:
C#
The default value of each floating-point type is zero, 0. Each of the floating-point types
has the MinValue and MaxValue constants that provide the minimum and maximum
finite value of that type. The float and double types also provide constants that
represent not-a-number and infinity values. For example, the double type provides the
following constants: Double.NaN , Double.NegativeInfinity , and Double.P ositiveInfinity .
The decimal type is appropriate when the required degree of precision is determined by
the number of digits to the right of the decimal point. Such numbers are commonly
used in financial applications, for currency amounts (for example, $1.00), interest rates
(for example, 2.625%), and so forth. Even numbers that are precise to only one decimal
digit are handled more accurately by the decimal type: 0.1, for example, can be exactly
represented by a decimal instance, while there's no double or float instance thatCharacteristics of the floating-point types
−45 38
−324 308
-28 28
double a = 12.3; 
System.Double b = 12.3; exactly represents 0.1. Because of this difference in numeric types, unexpected rounding
errors can occur in arithmetic calculations when you use double or float for decimal
data. Y ou can use double instead of decimal when optimizing performance is more
important than ensuring accuracy. However, any difference in performance would go
unnoticed by all but the most calculation-intensive applications. Another possible
reason to avoid decimal is to minimize storage requirements. For example, ML.NET  uses
float because the difference between 4 bytes and 16 bytes adds up for very large data
sets. For more information, see System.Decimal .
You can mix integral  types and the float and double types in an expression. In this
case, integral types are implicitly converted to one of the floating-point types and, if
necessary, the float type is implicitly converted to double. The expression is evaluated
as follows:
If there is double type in the expression, the expression evaluates to double, or to
bool in relational and equality comparisons.
If there is no double type in the expression, the expression evaluates to float, or
to bool in relational and equality comparisons.
You can also mix integral types and the decimal type in an expression. In this case,
integral types are implicitly converted to the decimal type and the expression evaluates
to decimal, or to bool in relational and equality comparisons.
You cannot mix the decimal type with the float and double types in an expression. In
this case, if you want to perform arithmetic, comparison, or equality operations, you
must explicitly convert the operands either from or to the decimal type, as the following
example shows:
C#
You can use either standard numeric format strings  or custom numeric format strings  to
format a floating-point value.
The type of a real literal is determined by its suffix as follows:double a = 1.0; 
decimal b = 2.1m; 
Console.WriteLine(a + ( double)b); 
Console.WriteLine(( decimal)a + b);  
Real literalsThe literal without suffix or with the d or D suffix is of type double
The literal with the f or F suffix is of type float
The literal with the m or M suffix is of type decimal
The following code demonstrates an example of each:
C#
The preceding example also shows the use of _ as a digit s eparator. You can use the
digit separator with all kinds of numeric literals.
You can also use scientific notation, that is, specify an exponent part of a real literal, as
the following example shows:
C#
There is only one implicit conversion between floating-point numeric types: from float
to double. However, you can convert any floating-point type to any other floating-point
type with the explicit cast . For more information, see Built-in numeric conversions .
For more information, see the following sections of the C# language specification :double d = 3D; 
d = 4d; 
d = 3.934_001; 
float f = 3_000.5F; 
f = 5.4f; 
decimal myMoney = 3_000.5m; 
myMoney = 400.75M; 
double d = 0.42e2; 
Console.WriteLine(d);  // output 42  
float f = 134.45E-2 f; 
Console.WriteLine(f);  // output: 1.3445  
decimal m = 1.5E6m; 
Console.WriteLine(m);  // output: 1500000  
Conversions
C# language specificationFloating-point types
The decimal type
Real literals
C# reference
Value types
Integral types
Standard numeric format strings
Numerics in .NET
System.Numerics.ComplexSee alsoBuilt-in numeric conversions (C#
reference)
Article •01/31/2023
C# provides a set of integral  and floating-point  numeric types. There exists a conversion
between any two numeric types, either implicit or explicit. Y ou must use a cast
expression  to perform an explicit conversion.
The following table shows the predefined implicit conversions between the built-in
numeric types:
From To
sbyte short, int, long, float, double, decimal, or nint
byte short, ushort, int, uint, long, ulong, float, double, decimal, nint, or nuint
short int, long, float, double, or decimal, or nint
ushort int, uint, long, ulong, float, double, or decimal, nint, or nuint
int long, float, double, or decimal, nint
uint long, ulong, float, double, or decimal, or nuint
long float, double, or decimal
ulong float, double, or decimal
float double
nint long, float, double, or decimal
nuint ulong, float, double, or decimalImplicit numeric conversions
７ Note
The implicit conversions from int, uint, long, ulong, nint, or nuint to float and
from long, ulong, nint, or nuint to double may cause a loss of precision, but
never a loss of an order of magnitude. The other implicit numeric conversions never
lose any information.Also note that
Any integral numeric type  is implicitly convertible to any floating-point numeric
type.
There are no implicit conversions to the byte and sbyte types. There are no
implicit conversions from the double and decimal types.
There are no implicit conversions between the decimal type and the float or
double types.
A value of a constant expression of type int (for example, a value represented by
an integer literal) can be implicitly converted to sbyte, byte, short, ushort, uint,
ulong, nint, or nuint, if it's within the range of the destination type:
C#
As the preceding example shows, if the constant value is not within the range of
the destination type, a compiler error CS0031  occurs.
The following table shows the predefined explicit conversions between the built-in
numeric types for which there is no implicit conversion :
From To
sbyte byte, ushort, uint, ulong, or nuint
byte sbyte
short sbyte, byte, ushort, uint, ulong, or nuint
ushort sbyte, byte, or short
int sbyte, byte, short, ushort, uint, ulong, or nuint
uint sbyte, byte, short, ushort, int, or nint
long sbyte, byte, short, ushort, int, uint, ulong, nint, or nuint
ulong sbyte, byte, short, ushort, int, uint, long, nint, or nuintbyte a = 13; 
byte b = 300;  // CS0031: Constant value '300' cannot be converted to a  
'byte' 
Explicit numeric conversionsFrom To
float sbyte, byte, short, ushort, int, uint, long, ulong, decimal, nint, or nuint
double sbyte, byte, short, ushort, int, uint, long, ulong, float, decimal, nint, or nuint
decimal sbyte, byte, short, ushort, int, uint, long, ulong, float, double, nint, or nuint
nint sbyte, byte, short, ushort, int, uint, ulong, or nuint
nuint sbyte, byte, short, ushort, int, uint, long, or nint
Also note that:
When you convert a value of an integral type to another integral type, the result
depends on the overflow-checking context . In a checked context, the conversion
succeeds if the source value is within the range of the destination type. Otherwise,
an OverflowException  is thrown. In an unchecked context, the conversion always
succeeds, and proceeds as follows:
If the source type is larger than the destination type, then the source value is
truncated by discarding its "extra" most significant bits. The result is then
treated as a value of the destination type.
If the source type is smaller than the destination type, then the source value is
either sign-extended or zero-extended so that it's of the same size as the
destination type. Sign-extension is used if the source type is signed; zero-
extension is used if the source type is unsigned. The result is then treated as a
value of the destination type.
If the source type is the same size as the destination type, then the source value
is treated as a value of the destination type.
When you convert a decimal value to an integral type, this value is rounded
towards zero to the nearest integral value. If the resulting integral value is outside
the range of the destination type, an OverflowException  is thrown.
When you convert a double or float value to an integral type, this value is
rounded towards zero to the nearest integral value. If the resulting integral value is７ Note
An explicit numeric conversion might result in data loss or throw an exception,
typically an OverflowEx ception .outside the range of the destination type, the result depends on the overflow-
checking context . In a checked context, an OverflowException  is thrown, while in
an unchecked context, the result is an unspecified value of the destination type.
When you convert double to float, the double value is rounded to the nearest
float value. If the double value is too small or too large to fit into the float type,
the result is zero or infinity.
When you convert float or double to decimal, the source value is converted to
decimal representation and rounded to the nearest number after the 28th decimal
place if necessary. Depending on the value of the source value, one of the
following results may occur:
If the source value is too small to be represented as a decimal, the result
becomes zero.
If the source value is NaN (not a number), infinity, or too large to be
represented as a decimal, an OverflowException  is thrown.
When you convert decimal to float or double, the source value is rounded to the
nearest float or double value, respectively.
For more information, see the following sections of the C# language specification :
Implicit numeric conversions
Explicit numeric conversions
C# reference
Casting and type conversionsC# language specification
See alsobool (C# reference)
Article •01/25/2022
The bool type keyword is an alias for the .NET System.Boolean  structure type that
represents a Boolean value, which can be either true or false.
To perform logical operations with values of the bool type, use Boolean logical
operators. The bool type is the result type of comparison  and equality  operators. A
bool expression can be a controlling conditional expression in the if, do, while , and for
statements and in the conditional operator ?:.
The default value of the bool type is false.
You can use the true and false literals to initialize a bool variable or to pass a bool
value:
C#
Use the nullable bool? type, if you need to support the three-valued logic, for example,
when you work with databases that support a three-valued Boolean type. For the bool?
operands, the predefined & and | operators support the three-valued logic. For more
information, see the Nullable Boolean logical operators  section of the Boolean logical
operators  article.
For more information about nullable value types, see Nullable value types .
C# provides only two conversions that involve the bool type. Those are an implicit
conversion to the corresponding nullable bool? type and an explicit conversion fromLiterals
bool check = true; 
Console.WriteLine(check ? "Checked"  : "Not checked" );  // output: Checked  
Console.WriteLine( false ? "Checked"  : "Not checked" );  // output: Not  
checked 
Three-valued Boolean logic
Conversionsthe bool? type. However, .NET provides additional methods that you can use to convert
to or from the bool type. For more information, see the Converting to and from
Boolean values  section of the System.Boolean  API reference page.
For more information, see The bool type  section of the C# language specification .
C# reference
Value types
true and false operatorsC# language specification
See alsochar (C# reference)
Article •01/25/2022
The char type keyword is an alias for the .NET System.Char  structure type that
represents a Unicode UTF-16 character.
Type Range Size .NET type
char U+0000 to U+FFFF 16 bit System.Char
The default value of the char type is \0, that is, U+0000.
The char type supports comparison , equality , increment , and decrement  operators.
Moreover, for char operands, arithmetic  and bitwise logical  operators perform an
operation on the corresponding character codes and produce the result of the int type.
The string  type represents text as a sequence of char values.
You can specify a char value with:
a character literal.
a Unicode escape sequence, which is \u followed by the four-symbol hexadecimal
representation of a character code.
a hexadecimal escape sequence, which is \x followed by the hexadecimal
representation of a character code.
C#
As the preceding example shows, you can also cast the value of a character code into
the corresponding char value.Literals
var chars = new[] 
{ 
    'j', 
    '\u006A' , 
    '\x006A' , 
    (char)106, 
}; 
Console.WriteLine( string.Join(" ", chars));  // output: j j j j  The char type is implicitly convertible to the following integral  types: ushort, int, uint,
long, and ulong. It's also implicitly convertible to the built-in floating-point  numeric
types: float, double, and decimal. It's explicitly convertible to sbyte, byte, and short
integral types.
There are no implicit conversions from other types to the char type. However, any
integral  or floating-point  numeric type is explicitly convertible to char.
For more information, see the Integral types  section of the C# language specification .
C# reference
Value types
Strings
System.T ext.Rune
Character encoding in .NET７ Note
In the case of a Unicode escape sequence, you must specify all four hexadecimal
digits. That is, \u006A is a valid escape sequence, while \u06A and \u6A are not
valid.
In the case of a hexadecimal escape sequence, you can omit the leading zeros. That
is, the \x006A, \x06A, and \x6A escape sequences are valid and correspond to the
same character.
Conversions
C# language specification
See alsoEnumeration types (C# reference)
Article •04/08/2023
An enumer ation type  (or enum type ) is a value type  defined by a set of named constants
of the underlying integral numeric  type. T o define an enumeration type, use the enum
keyword and specify the names of enum member s:
C#
By default, the associated constant values of enum members are of type int; they start
with zero and increase by one following the definition text order. Y ou can explicitly
specify any other integral numeric  type as an underlying type of an enumeration type.
You can also explicitly specify the associated constant values, as the following example
shows:
C#
You cannot define a method inside the definition of an enumeration type. T o add
functionality to an enumeration type, create an extension method .
The default value of an enumeration type E is the value produced by expression (E)0,
even if zero doesn't have the corresponding enum member.
You use an enumeration type to represent a choice from a set of mutually exclusive
values or a combination of choices. T o represent a combination of choices, define an
enumeration type as bit flags.enum Season 
{ 
    Spring,  
    Summer,  
    Autumn,  
    Winter  
} 
enum ErrorCode : ushort 
{ 
    None = 0, 
    Unknown = 1, 
    ConnectionLost = 100, 
    OutlierReading = 200 
} If you want an enumeration type to represent a combination of choices, define enum
members for those choices such that an individual choice is a bit field. That is, the
associated values of those enum members should be the powers of two. Then, you can
use the bitwise logical operators | or & to combine choices or intersect combinations of
choices, respectively. T o indicate that an enumeration type declares bit fields, apply the
Flags  attribute to it. As the following example shows, you can also include some typical
combinations in the definition of an enumeration type.
C#Enum eration types as bit flags
[Flags] 
public enum Days 
{ 
    None      = 0b_0000_0000,  // 0 
    Monday    = 0b_0000_0001,  // 1 
    Tuesday   = 0b_0000_0010,  // 2 
    Wednesday = 0b_0000_0100,  // 4 
    Thursday  = 0b_0000_1000,  // 8 
    Friday    = 0b_0001_0000,  // 16 
    Saturday  = 0b_0010_0000,  // 32 
    Sunday    = 0b_0100_0000,  // 64 
    Weekend   = Saturday | Sunday
} 
public class FlagsEnumExample  
{ 
    public static void Main() 
    { 
        Days meetingDays = Days.Monday | Days.Wednesday | Days.Friday;  
        Console.WriteLine(meetingDays);  
        // Output:  
        // Monday, Wednesday, Friday  
        Days workingFromHomeDays = Days.Thursday | Days.Friday;  
        Console.WriteLine( $"Join a meeting by phone on {meetingDays &  
workingFromHomeDays} "); 
        // Output:  
        // Join a meeting by phone on Friday  
        bool isMeetingOnTuesday = (meetingDays & Days.Tuesday) ==  
Days.Tuesday;  
        Console.WriteLine( $"Is there a meeting on Tuesday:  
{isMeetingOnTuesday} "); 
        // Output:  
        // Is there a meeting on Tuesday: False  
        var a = (Days) 37; 
        Console.WriteLine(a);  
        // Output:  For more information and examples, see the System.FlagsAttribute  API reference page
and the Non-exclusive members and the Flags attribute  section of the System.Enum  API
reference page.
The System.Enum  type is the abstract base class of all enumeration types. It provides a
number of methods to get information about an enumeration type and its values. For
more information and examples, see the System.Enum  API reference page.
You can use System.Enum in a base class constraint (that is known as the enum
constraint ) to specify that a type parameter is an enumeration type. Any enumeration
type also satisfies the struct constraint, which is used to specify that a type parameter
is a non-nullable value type.
For any enumeration type, there exist explicit conversions between the enumeration
type and its underlying integral type. If you cast an enum value to its underlying type,
the result is the associated integral value of an enum member.
C#        // Monday, Wednesday, Saturday  
    } 
} 
The System.Enum  type and enum constraint
Conversions
public enum Season 
{ 
    Spring,  
    Summer,  
    Autumn,  
    Winter  
} 
public class EnumConversionExample  
{ 
    public static void Main() 
    { 
        Season a = Season.Autumn;
        Console.WriteLine( $"Integral value of {a} is {(int)a}");  // output:  
Integral value of Autumn is 2  
        var b = (Season) 1; 
        Console.WriteLine(b);  // output: Summer  Use the Enum.IsDefined  method to determine whether an enumeration type contains an
enum member with the certain associated value.
For any enumeration type, there exist boxing and unboxing  conversions to and from the
System.Enum  type, respectively.
For more information, see the following sections of the C# language specification :
Enums
Enum values and operations
Enumeration logical operators
Enumeration comparison operators
Explicit enumeration conversions
Implicit enumeration conversions
C# reference
Enumeration format strings
Design guidelines - Enum design
Design guidelines - Enum naming conventions
switch  expression
switch  statement        var c = (Season) 4; 
        Console.WriteLine(c);  // output: 4  
    } 
} 
C# language specification
See alsoStructure types (C# reference)
Article •10/26/2023
A structur e type  (or struct type ) is a value type  that can encapsulate data and related
functionality. Y ou use the struct keyword to define a structure type:
C#
For information about ref struct and readonly ref struct types, see the ref structure
types  article.
Structure types have value s emantics . That is, a variable of a structure type contains an
instance of the type. By default, variable values are copied on assignment, passing an
argument to a method, and returning a method result. For structure-type variables, an
instance of the type is copied. For more information, see Value types .
Typically, you use structure types to design small data-centric types that provide little or
no behavior. For example, .NET uses structure types to represent a number (both integer
and real), a Boolean value , a Unicode character , a time instance . If you're focused on the
behavior of a type, consider defining a class . Class types have reference semantics . That
is, a variable of a class type contains a reference to an instance of the type, not the
instance itself.
Because structure types have value semantics, we recommend you define immut able
structure types.public struct Coords
{
    public Coords(double x, double y)
    {
        X = x;
        Y = y;
    }
    public double X { get; }
    public double Y { get; }
    public override  string ToString () => $"({X}, {Y})";
}
readonly structYou use the readonly modifier to declare that a structure type is immutable. All data
members of a readonly struct must be read-only as follows:
Any field declaration must have the readonly  modifier
Any property, including auto-implemented ones, must be read-only or init only .
That guarantees that no member of a readonly struct modifies the state of the struct.
That means that other instance members except constructors are implicitly readonly .
The following code defines a readonly struct with init-only property setters:
C#
You can also use the readonly modifier to declare that an instance member doesn't
modify the state of a struct. If you can't declare the whole structure type as readonly,
use the readonly modifier to mark the instance members that don't modify the state of
the struct.
Within a readonly instance member, you can't assign to structure's instance fields.
However, a readonly member can call a non- readonly member. In that case, the７ Note
In a readonly struct, a data member of a mutable reference type still can mutate its
own state. For example, you can't replace a List<T>  instance, but you can add new
elements to it.
public readonly  struct Coords
{
    public Coords(double x, double y)
    {
        X = x;
        Y = y;
    }
    public double X { get; init; }
    public double Y { get; init; }
    public override  string ToString () => $"({X}, {Y})";
}
readonly instance memberscompiler creates a copy of the structure instance and calls the non- readonly member
on that copy. As a result, the original structure instance isn't modified.
Typically, you apply the readonly modifier to the following kinds of instance members:
methods:
C#
You can also apply the readonly modifier to methods that override methods
declared in System.Object :
C#
properties and indexers:
C#
If you need to apply the readonly modifier to both accessors of a property or
indexer, apply it in the declaration of the property or indexer.
You may apply the readonly modifier to a property or indexer with an init
accessor:public readonly  double Sum()
{
    return X + Y;
}
public readonly  override  string ToString () => $"({X}, {Y})";
private int counter;
public int Counter
{
    readonly  get => counter;
    set => counter = value;
}
７ Note
The compiler declares a get accessor of an auto-implement ed pr oper ty as
readonly, regardless of presence of the readonly modifier in a property
declaration.C#
You can apply the readonly modifier to static fields of a structure type, but not any
other static members, such as properties or methods.
The compiler may make use of the readonly modifier for performance optimizations.
For more information, see Avoiding allocations .
Beginning with C# 10, you can use the with expression  to produce a copy of a structure-
type instance with the specified properties and fields modified. Y ou use object initializer
syntax to specify what members to modify and their new values, as the following
example shows:
C#public readonly  double X { get; init; }
Nondestructive mutation
public readonly  struct Coords
{
    public Coords(double x, double y)
    {
        X = x;
        Y = y;
    }
    public double X { get; init; }
    public double Y { get; init; }
    public override  string ToString () => $"({X}, {Y})";
}
public static void Main()
{
    var p1 = new Coords( 0, 0);
    Console.WriteLine(p1);  // output: (0, 0)
    var p2 = p1 with { X = 3 };
    Console.WriteLine(p2);  // output: (3, 0)
    var p3 = p1 with { X = 1, Y = 4 };
    Console.WriteLine(p3);  // output: (1, 4)
}
record structBeginning with C# 10, you can define record structure types. R ecord types provide built-
in functionality for encapsulating data. Y ou can define both record struct and readonly
record struct types. A record struct can't be a ref struct . For more information and
examples, see Records .
Beginning with C# 12, you can declare inline arr ays as a struct type:
C#
An inline array is a structure that contains a contiguous block of N elements of the same
type. It's a safe-code equivalent of the fixed buffer  declaration available only in unsafe
code. An inline array is a struct with the following characteristics:
It contains a single field.
The struct doesn't specify an explicit layout.
In addition, the compiler validates the
System.Runtime.CompilerServices.InlineArrayAttribute  attribute:
The length must be greater than zero ( > 0).
The target type must be a struct.
In most cases, an inline array can be accessed like an array, both to read and write
values. In addition, you can use the range  and index  operators.
There are minimal restrictions on the type of the single field. It can't be a pointer type,
but it can be any reference type, or any value type. Y ou can use inline arrays with almost
any C# data structure.
Inline arrays are an advanced language feature. They're intended for high-performance
scenarios where an inline, contiguous block of elements is faster than other alternative
data structures. Y ou can learn more about inline arrays from the feature specletInline  arrays
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct CharBuffer
{
    private char _firstElement;
}
Struct initia lization and default valuesA variable of a struct type directly contains the data for that struct. That creates a
distinction between an uninitialized struct, which has its default value and an initialized
struct, which stores values set by constructing it. For example consider the following
code:
C#
As the preceding example shows, the default value expression  ignores a parameterless
constructor and produces the default value  of the structure type. S tructure-type array
instantiation also ignores a parameterless constructor and produces an array populated
with the default values of a structure type.
The most common situation where you see default values is in arrays or in other
collections where internal storage includes blocks of variables. The following example
creates an array of 30 TemperatureRange structures, each of which has the default value:
C#public readonly  struct Measurement
{
    public Measurement ()
    {
        Value = double.NaN;
        Description = "Undefined" ;
    }
    public Measurement (double value, string description )
    {
        Value = value;
        Description = description;
    }
    public double Value { get; init; }
    public string Description { get; init; }
    public override  string ToString () => $"{Value} ({Description} )";
}
public static void Main()
{
    var m1 = new Measurement();
    Console.WriteLine(m1);  // output: NaN (Undefined)
    var m2 = default(Measurement);
    Console.WriteLine(m2);  // output: 0 ()
    var ms = new Measurement[ 2];
    Console.WriteLine( string.Join(", ", ms));  // output: 0 (), 0 ()
}All of a struct's member fields must be definitely assigned  when it's created because
struct types directly store their data. The default value of a struct has definitely
assigned  all fields to 0. All fields must be definitely assigned when a constructor is
invoked. Y ou initialize fields using the following mechanisms:
You can add field initializer s to any field or auto implemented property.
You can initialize any fields, or auto properties, in the body of the constructor.
Beginning with C# 11, if you don't initialize all fields in a struct, the compiler adds code
to the constructor that initializes those fields to the default value. The compiler performs
its usual definite assignment analysis. Any fields that are accessed before being
assigned, or not definitely assigned when the constructor finishes executing are
assigned their default values before the constructor body executes. If this is accessed
before all fields are assigned, the struct is initialized to the default value before the
constructor body executes.
C#// All elements have default values of 0:
TemperatureRange[] lastMonth = new TemperatureRange[ 30];
public readonly  struct Measurement
{
    public Measurement (double value)
    {
        Value = value;
    }
    public Measurement (double value, string description )
    {
        Value = value;
        Description = description;
    }
    public Measurement (string description )
    {
        Description = description;
    }
    public double Value { get; init; }
    public string Description { get; init; } = "Ordinary measurement" ;
    public override  string ToString () => $"{Value} ({Description} )";
}
public static void Main()
{
    var m1 = new Measurement( 5);Every struct has a public parameterless constructor. If you write a parameterless
constructor, it must be public. If a struct declares any field initializers, it must explicitly
declare a constructor. That constructor need not be parameterless. If a struct declares a
field initializer but no constructors, the compiler reports an error. Any explicitly declared
constructor (with parameters, or parameterless) executes all field initializers for that
struct. All fields without a field initializer or an assignment in a constructor are set to the
default value . For more information, see the Parameterless struct constructors  feature
proposal note.
Beginning with C# 12, struct types can define a primary constructor  as part of its
declaration. Primary constructors provides a concise syntax for constructor parameters
that can be used throughout the struct body, in any member declaration for that
struct.
If all instance fields of a structure type are accessible, you can also instantiate it without
the new operator. In that case you must initialize all instance fields before the first use of
the instance. The following example shows how to do that:
C#    Console.WriteLine(m1);  // output: 5 (Ordinary measurement)
    var m2 = new Measurement();
    Console.WriteLine(m2);  // output: 0 ()
    var m3 = default(Measurement);
    Console.WriteLine(m3);  // output: 0 ()
}
public static class StructWithoutNew
{
    public struct Coords
    {
        public double x;
        public double y;
    }
    public static void Main()
    {
        Coords p;
        p.x = 3;
        p.y = 4;
        Console.WriteLine( $"({p.x}, {p.y})");  // output: (3, 4)
    }
}In the case of the built-in value types , use the corresponding literals to specify a value of
the type.
Structs have most of the capabilities of a class  type. There are some exceptions, and
some exceptions that have been removed in more recent versions:
A structure type can't inherit from other class or structure type and it can't be the
base of a class. However, a structure type can implement interfaces .
You can't declare a finalizer  within a structure type.
Prior to C# 11, a constructor of a structure type must initialize all instance fields of
the type.
When you pass a structure-type variable to a method as an argument or return a
structure-type value from a method, the whole instance of a structure type is copied.
Pass by value can affect the performance of your code in high-performance scenarios
that involve large structure types. Y ou can avoid value copying by passing a structure-
type variable by reference. Use the ref, out, in, or ref readonly method parameter
modifiers to indicate that an argument must be passed by reference . Use ref returns  to
return a method result by reference. For more information, see Avoid allocations .
You also use the struct keyword in the struct  constraint  to specify that a type
parameter is a non-nullable value type. Both structure and enumeration  types satisfy the
struct constraint.
For any structure type (except ref struct  types), there exist boxing and unboxing
conversions to and from the System.V alueT ype and System.Object  types. There exist also
boxing and unboxing conversions between a structure type and any interface that it
implements.Limitations with the design of a structure type
Passing structure-type variables by reference
struct constraint
Conversions
C# language specificationFor more information, see the Structs  section of the C# language specification .
For more information about struct features, see the following feature proposal notes:
Readonly structs
Readonly instance members
C# 10 - P arameterless struct constructors
C# 10 - Allow with expression on structs
C# 10 - R ecord structs
C# 11 - Auto default structs
C# reference
The C# type system
Design guidelines - Choosing between class and struct
Design guidelines - S truct designSee also
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
 Provide product feedbackref structure types (C# reference)
Article •06/23/2023
You can use the ref modifier in the declaration of a structure type . Instances of a ref
struct type are allocated on the stack and can't escape to the managed heap. T o ensure
that, the compiler limits the usage of ref struct types as follows:
A ref struct can't be the element type of an array.
A ref struct can't be a declared type of a field of a class or a non- ref struct.
A ref struct can't implement interfaces.
A ref struct can't be boxed to System.V alueT ype or System.Object .
A ref struct can't be a type argument.
A ref struct variable can't be captured by a lambda expression  or a local
function .
A ref struct variable can't be used in an async  method. However, you can use
ref struct variables in synchronous methods, for example, in methods that return
Task or Task<TR esult> .
A ref struct variable can't be used in iterators .
You can define a disposable ref struct. To do that, ensure that a ref struct fits the
disposable pattern . That is, it has an instance Dispose method, which is accessible,
parameterless and has a void return type. Y ou can use the using statement or
declaration  with an instance of a disposable ref struct.
Typically, you define a ref struct type when you need a type that also includes data
members of ref struct types:
C#
To declare a ref struct as readonly, combine the readonly and ref modifiers in the
type declaration (the readonly modifier must come before the ref modifier):
C#public ref struct CustomRef
{
    public bool IsValid;
    public Span<int> Inputs;
    public Span<int> Outputs;
}In .NET, examples of a ref struct are System.Span<T>  and System.R eadOnlySpan<T> .
Beginning with C# 11, you can declare a ref field in a ref struct, as the following
example shows:
C#
A ref field may have the null value. Use the Unsafe.IsNullR ef<T>(T)  method to
determine if a ref field is null.
You can apply the readonly modifier to a ref field in the following ways:
readonly ref: You can ref reassign  such a field with the = ref operator only inside
a constructor or an init accessor . You can assign a value with the = operator at any
point allowed by the field access modifier.public readonly  ref struct ConversionRequest
{
    public ConversionRequest (double rate, ReadOnlySpan< double> values )
    {
        Rate = rate;
        Values = values;
    }
    public double Rate { get; }
    public ReadOnlySpan< double> Values { get; }
}
ref fields
public ref struct RefFieldExample
{
    private ref int number;
    public int GetNumber ()
    {
        if (System.Runtime.CompilerServices.Unsafe.IsNullRef( ref number))
        {
            throw new InvalidOperationException( "The number ref field is not  
initialized." );
        }
        return number;
    }
}ref readonly: At any point, you cannot assign a value with the = operator to such
a field. However, you can ref reassign a field with the = ref operator.
readonly ref readonly: You can only ref reassign such a field in a constructor or an
init accessor. At any point, you cannot assign a value to the field.
The compiler ensures that a reference stored in a ref field doesn't outlive its referent.
The ref fields feature enables a safe implementation of types like System.Span<T> :
C#
The Span<T> type stores a reference through which it accesses the contiguous elements
in memory. The use of a reference enables a Span<T> instance to avoid copying the
storage it refers to.
For more information, see the following sections of the C# language specification :
Structs: R ef modifier
Safe context constraint for ref struct types
For more information about ref fields, see the Low-level struct improvements  proposal
note.
C# reference
The C# type systempublic readonly  ref struct Span<T>
{
    internal  readonly  ref T _reference;
    private readonly  int _length;
    // Omitted for brevity...
}
C# language specification
See alsoTuple types (C# reference)
Article •05/17/2023
The tuples  feature provides concise syntax to group multiple data elements in a
lightweight data structure. The following example shows how you can declare a tuple
variable, initialize it, and access its data members:
C#
As the preceding example shows, to define a tuple type, you specify types of all its data
members and, optionally, the field names . You can't define methods in a tuple type, but
you can use the methods provided by .NET, as the following example shows:
C#
Tuple types support equality operators  == and !=. For more information, see the Tuple
equality  section.
Tuple types are value types ; tuple elements are public fields. That makes tuples mutable
value types.
You can define tuples with an arbitrary large number of elements:
C#(double, int) t1 = ( 4.5, 3);
Console.WriteLine( $"Tuple with elements {t1.Item1}  and {t1.Item2} .");
// Output:
// Tuple with elements 4.5 and 3.
(double Sum, int Count) t2 = ( 4.5, 3);
Console.WriteLine( $"Sum of {t2.Count}  elements is {t2.Sum} .");
// Output:
// Sum of 3 elements is 4.5.
(double, int) t = (4.5, 3);
Console.WriteLine(t.ToString());
Console.WriteLine( $"Hash code of {t} is {t.GetHashCode()} .");
// Output:
// (4.5, 3)
// Hash code of (4.5, 3) is 718460086.
var t =
(1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
11, 12, 13, 14, 15, 16, 17, 18,One of the most common use cases of tuples is as a method return type. That is, instead
of defining out method parameters , you can group method results in a tuple return
type, as the following example shows:
C#19, 20, 21, 22, 23, 24, 25, 26);
Console.WriteLine(t.Item26);  // output: 26
Use cases of tuples
var xs = new[] { 4, 7, 9 };
var limits = FindMinMax(xs);
Console.WriteLine( $"Limits of [ {string.Join(" ", xs)}] are {limits.min}  and 
{limits.max} ");
// Output:
// Limits of [4 7 9] are 4 and 9
var ys = new[] { -9, 0, 67, 100 };
var (minimum, maximum) = FindMinMax(ys);
Console.WriteLine( $"Limits of [ {string.Join(" ", ys)}] are {minimum}  and 
{maximum} ");
// Output:
// Limits of [-9 0 67 100] are -9 and 100
(int min, int max) FindMinMax( int[] input)
{
    if (input is null || input.Length == 0)
    {
        throw new ArgumentException( "Cannot find minimum and maximum of a  
null or empty array." );
    }
    // Initialize min to MaxValue so every value in the input
    // is less than this initial value.
    var min = int.MaxValue;
    // Initialize max to MinValue so every value in the input
    // is greater than this initial value.
    var max = int.MinValue;
    foreach (var i in input)
    {
        if (i < min)
        {
            min = i;
        }
        if (i > max)
        {
            max = i;
        }
    }As the preceding example shows, you can work with the returned tuple instance directly
or deconstruct  it in separate variables.
You can also use tuple types instead of anonymous types ; for example, in LINQ queries.
For more information, see Choosing between anonymous and tuple types .
Typically, you use tuples to group loosely related data elements. In public APIs, consider
defining a class  or a structure  type.
You explicitly specify tuple fields names in a tuple initialization expression or in the
definition of a tuple type, as the following example shows:
C#
If you don't specify a field name, it may be inferred from the name of the corresponding
variable in a tuple initialization expression, as the following example shows:
C#
That's called tuple projection initializers. The name of a variable isn't projected onto a
tuple field name in the following cases:
The candidate name is a member name of a tuple type, for example, Item3,
ToString, or Rest.
The candidate name is a duplicate of another tuple field name, either explicit or
implicit.    return (min, max);
}
Tuple field names
var t = (Sum: 4.5, Count: 3);
Console.WriteLine( $"Sum of {t.Count}  elements is {t.Sum}.");
(double Sum, int Count) d = ( 4.5, 3);
Console.WriteLine( $"Sum of {d.Count}  elements is {d.Sum}.");
var sum = 4.5;
var count = 3;
var t = (sum, count);
Console.WriteLine( $"Sum of {t.count}  elements is {t.sum}.");In the preceding cases, you either explicitly specify the name of a field or access a field
by its default name.
The default names of tuple fields are Item1, Item2, Item3 and so on. Y ou can always use
the default name of a field, even when a field name is specified explicitly or inferred, as
the following example shows:
C#
Tuple assignment  and tuple equality comparisons  don't take field names into account.
At compile time, the compiler replaces non-default field names with the corresponding
default names. As a result, explicitly specified or inferred field names aren't available at
run time.
Beginning with C# 12, you can specify an alias for a tuple type with a using  directive . The
following example adds a global using alias for a tuple type with two integer values for
an allowed Min and Max value:
C#
After declaring the alias, you can use the BandPass name as an alias for that tuple type:
C#var a = 1;
var t = (a, b: 2, 3);
Console.WriteLine( $"The 1st element is {t.Item1}  (same as {t.a}).");
Console.WriteLine( $"The 2nd element is {t.Item2}  (same as {t.b}).");
Console.WriteLine( $"The 3rd element is {t.Item3} .");
// Output:
// The 1st element is 1 (same as 1).
// The 2nd element is 2 (same as 2).
// The 3rd element is 3.
 Tip
Enable .NET code style rule IDE0037  to set a preference on inferred or explicit tuple
field names.
global using BandPass = ( int Min, int Max);
BandPass bracket = ( 40, 100);
Console.WriteLine( $"The bandpass filter is {bracket.Min}  to {bracket.Max} ");An alias doesn't introduce a new type, but only creates a synonym for an existing type.
You can deconstruct a tuple declared with the BandPass alias the same as you can with
its underlying tuple type:
C#
As with tuple assignment or deconstruction, the tuple member names don't need to
match; the types do.
Similarly, a second alias with the same arity and member types can be used
interchangeably with the original alias. Y ou could declare a second alias:
C#
You can assign a Range tuple to a BandPass tuple. As with all tuple assignment, the field
names need not match, only the types and the arity.
C#
An alias for a tuple type provides more semantic information when you use tuples. It
doesn't introduce a new type. T o provide type safety, you should declare a positional
record  instead.
C# supports assignment between tuple types that satisfy both of the following
conditions:
both tuple types have the same number of elements
for each tuple position, the type of the right-hand tuple element is the same as or
implicitly convertible to the type of the corresponding left-hand tuple element
Tuple element values are assigned following the order of tuple elements. The names of
tuple fields are ignored and not assigned, as the following example shows:(int a , int b) = bracket;
Console.WriteLine( $"The bracket is {a} to {b}");
using Range = ( int Minimum, int Maximum);
Range r = bracket;
Console.WriteLine( $"The range is {r.Minimum}  to {r.Maximum} ");
Tuple assignment and deconstructionC#
You can also use the assignment operator = to deconstr uct a tuple instance in separate
variables. Y ou can do that in many ways:
Use the var keyword outside the parentheses to declare implicitly typed variables
and let the compiler infer their types:
C#
Explicitly declare the type of each variable inside parentheses:
C#
Declare some types explicitly and other types implicitly (with var) inside the
parentheses:
C#(int, double) t1 = ( 17, 3.14);
(double First, double Second) t2 = ( 0.0, 1.0);
t2 = t1;
Console.WriteLine( $"{nameof(t2)}: {t2.First}  and {t2.Second} ");
// Output:
// t2: 17 and 3.14
(double A, double B) t3 = ( 2.0, 3.0);
t3 = t2;
Console.WriteLine( $"{nameof(t3)}: {t3.A} and {t3.B}");
// Output:
// t3: 17 and 3.14
var t = ("post office" , 3.6);
var (destination, distance) = t;
Console.WriteLine( $"Distance to {destination}  is {distance}  
kilometers." );
// Output:
// Distance to post office is 3.6 kilometers.
var t = ("post office" , 3.6);
(string destination, double distance) = t;
Console.WriteLine( $"Distance to {destination}  is {distance}  
kilometers." );
// Output:
// Distance to post office is 3.6 kilometers.
var t = ("post office" , 3.6);
(var destination, double distance) = t;Use existing variables:
C#
The destination of a deconstruct expression can include both existing variables and
variables declared in the deconstruction declaration.
You can also combine deconstruction with pattern matching  to inspect the
characteristics of fields in a tuple. The following example loops through several integers
and prints those that are divisible by 3. It deconstructs the tuple result of Int32.DivR em
and matches against a Remainder of 0:
C#
For more information about deconstruction of tuples and other types, see
Deconstructing tuples and other types .
Tuple types support the == and != operators. These operators compare members of
the left-hand operand with the corresponding members of the right-hand operand
following the order of tuple elements.Console.WriteLine( $"Distance to {destination}  is {distance}  
kilometers." );
// Output:
// Distance to post office is 3.6 kilometers.
var destination = string.Empty;
var distance = 0.0;
var t = ("post office" , 3.6);
(destination, distance) = t;
Console.WriteLine( $"Distance to {destination}  is {distance}  
kilometers." );
// Output:
// Distance to post office is 3.6 kilometers.
for (int i = 4; i < 20;  i++)
{
    if (Math.DivRem(i, 3) is ( Quotient: var q, Remainder: 0 ))
    {
        Console.WriteLine( $"{i} is divisible by 3, with quotient {q}");
    }
}
Tuple equalityC#
As the preceding example shows, the == and != operations don't take into account
tuple field names.
Two tuples are comparable when both of the following conditions are satisfied:
Both tuples have the same number of elements. For example, t1 != t2 doesn't
compile if t1 and t2 have different numbers of elements.
For each tuple position, the corresponding elements from the left-hand and right-
hand tuple operands are comparable with the == and != operators. For example,
(1, (2, 3)) == ((1, 2), 3) doesn't compile because 1 isn't comparable with (1,
2).
The == and != operators compare tuples in short-circuiting way. That is, an operation
stops as soon as it meets a pair of non equal elements or reaches the ends of tuples.
However, before any comparison, all tuple elements are evaluated, as the following
example shows:
C#(int a, byte b) left = ( 5, 10);
(long a, int b) right = ( 5, 10);
Console.WriteLine(left == right);  // output: True
Console.WriteLine(left != right);  // output: False
var t1 = (A: 5, B: 10);
var t2 = (B: 5, A: 10);
Console.WriteLine(t1 == t2);  // output: True
Console.WriteLine(t1 != t2);  // output: False
Console.WriteLine((Display( 1), Display( 2)) == (Display( 3), Display( 4)));
int Display(int s)
{
    Console.WriteLine(s);
    return s;
}
// Output:
// 1
// 2
// 3
// 4
// False
Tuples as out parametersTypically, you refactor a method that has out parameters  into a method that returns a
tuple. However, there are cases in which an out parameter can be of a tuple type. The
following example shows how to work with tuples as out parameters:
C#
C# tuples, which are backed by System.V alueTuple  types, are different from tuples that
are represented by System.Tuple  types. The main differences are as follows:
System.ValueTuple types are value types . System.Tuple types are reference types .
System.ValueTuple types are mutable. System.Tuple types are immutable.
Data members of System.ValueTuple types are fields. Data members of
System.Tuple types are properties.
For more information, see:
Tuple types
Tuple equality operators
C# reference
Value types
Choosing between anonymous and tuple typesvar limitsLookup = new Dictionary< int, (int Min, int Max)>()
{
    [2] = (4, 10),
    [4] = (10, 20),
    [6] = (0, 23)
};
if (limitsLookup.TryGetValue( 4, out (int Min, int Max) limits))
{
    Console.WriteLine( $"Found limits: min is {limits.Min} , max is 
{limits.Max} ");
}
// Output:
// Found limits: min is 10, max is 20
Tuples vs System.Tuple
C# language specification
See alsoSystem.V alueTuple
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
 Provide product feedbackNullable value types (C# reference)
Article •04/08/2023
A nullable v alue type  T? represents all values of its underlying value type  T and an
additional null value. For example, you can assign any of the following three values to a
bool? variable: true, false, or null. An underlying value type T cannot be a nullable
value type itself.
Any nullable value type is an instance of the generic System.Nullable<T>  structure. Y ou
can refer to a nullable value type with an underlying type T in any of the following
interchangeable forms: Nullable<T> or T?.
You typically use a nullable value type when you need to represent the undefined value
of an underlying value type. For example, a Boolean, or bool, variable can only be either
true or false. However, in some applications a variable value can be undefined or
missing. For example, a database field may contain true or false, or it may contain no
value at all, that is, NULL. You can use the bool? type in that scenario.
As a value type is implicitly convertible to the corresponding nullable value type, you
can assign a value to a variable of a nullable value type as you would do that for its
underlying value type. Y ou can also assign the null value. For example:
C#
The default value of a nullable value type represents null, that is, it's an instance whose
Nullable<T>.HasV alue property returns false.Declaration and assignment
double? pi = 3.14; 
char? letter = 'a'; 
int m2 = 10; 
int? m = m2;  
bool? flag = null; 
// An array of a nullable value type:  
int?[] arr = new int?[10]; You can use the is operator with a type pattern  to both examine an instance of a
nullable value type for null and retrieve a value of an underlying type:
C#
You always can use the following read-only properties to examine and get a value of a
nullable value type variable:
Nullable<T>.HasV alue indicates whether an instance of a nullable value type has a
value of its underlying type.
Nullable<T>.V alue gets the value of an underlying type if HasV alue is true. If
HasV alue is false, the Value property throws an InvalidOperationException .
The following example uses the HasValue property to test whether the variable contains
a value before displaying it:
C#Examination of an instance of a nulla ble value
type
int? a = 42; 
if (a is int valueOfA)  
{ 
    Console.WriteLine( $"a is {valueOfA} "); 
} 
else 
{ 
    Console.WriteLine( "a does not have a value" ); 
} 
// Output:  
// a is 42  
int? b = 10; 
if (b.HasValue)  
{ 
    Console.WriteLine( $"b is {b.Value} "); 
} 
else 
{ 
    Console.WriteLine( "b does not have a value" ); 
} 
// Output:  
// b is 10  You can also compare a variable of a nullable value type with null instead of using the
HasValue property, as the following example shows:
C#
If you want to assign a value of a nullable value type to a non-nullable value type
variable, you might need to specify the value to be assigned in place of null. Use the
null-coalescing operator ?? to do that (you can also use the
Nullable<T>.GetV alueOrDefault(T)  method for the same purpose):
C#
If you want to use the default  value of the underlying value type in place of null, use
the Nullable<T>.GetV alueOrDefault()  method.
You can also explicitly cast a nullable value type to a non-nullable type, as the following
example shows:
C#int? c = 7; 
if (c != null) 
{ 
    Console.WriteLine( $"c is {c.Value} "); 
} 
else 
{ 
    Console.WriteLine( "c does not have a value" ); 
} 
// Output:  
// c is 7  
Conversion from a nulla ble value type to an
underlying type
int? a = 28; 
int b = a ?? -1; 
Console.WriteLine( $"b is {b}");  // output: b is 28  
int? c = null; 
int d = c ?? -1; 
Console.WriteLine( $"d is {d}");  // output: d is -1  
int? n = null; At run time, if the value of a nullable value type is null, the explicit cast throws an
InvalidOperationException .
A non-nullable value type T is implicitly convertible to the corresponding nullable value
type T?.
The predefined unary and binary operators  or any overloaded operators that are
supported by a value type T are also supported by the corresponding nullable value
type T?. These operators, also known as lifted oper ators, produce null if one or both
operands are null; otherwise, the operator uses the contained values of its operands to
calculate the result. For example:
C#
For the comparison operators  <, >, <=, and >=, if one or both operands are null, the
result is false; otherwise, the contained values of operands are compared. Do not
assume that because a particular comparison (for example, <=) returns false, the
opposite comparison ( >) returns true. The following example shows that 10 is
neither greater than or equal to null
nor less than null//int m1 = n;    // Doesn't compile  
int n2 = (int)n; // Compiles, but throws an exception if n is null  
Lifted operators
int? a = 10; 
int? b = null; 
int? c = 10; 
a++;        // a is 11  
a = a * c;  // a is 110  
a = a + b;  // a is null  
７ Note
For the bool? type, the predefined & and | operators don't follow the rules
described in this section: the result of an operator evaluation can be non-null even
if one of the operands is null. For more information, see the Nullable Boolean
logical operat ors section of the Boolean logical operat ors article.C#
For the equality operator  ==, if both operands are null, the result is true, if only one of
the operands is null, the result is false; otherwise, the contained values of operands
are compared.
For the inequality operator  !=, if both operands are null, the result is false, if only one
of the operands is null, the result is true; otherwise, the contained values of operands
are compared.
If there exists a user-defined conversion  between two value types, the same conversion
can also be used between the corresponding nullable value types.
An instance of a nullable value type T? is boxed  as follows:
If HasV alue returns false, the null reference is produced.
If HasV alue returns true, the corresponding value of the underlying value type T
is boxed, not the instance of Nullable<T> .
You can unbox a boxed value of a value type T to the corresponding nullable value type
T?, as the following example shows:
C#int? a = 10; 
Console.WriteLine( $"{a} >= null is {a >= null}"); 
Console.WriteLine( $"{a} < null is {a < null}"); 
Console.WriteLine( $"{a} == null is {a == null}"); 
// Output:  
// 10 >= null is False  
// 10 < null is False  
// 10 == null is False  
int? b = null; 
int? c = null; 
Console.WriteLine( $"null >= null is {b >= c} "); 
Console.WriteLine( $"null == null is {b == c} "); 
// Output:  
// null >= null is False  
// null == null is True  
Boxing and unboxing
int a = 41; 
object aBoxed = a;  
int? aNullable = ( int?)aBoxed;  The following example shows how to determine whether a System.T ype instance
represents a constructed nullable value type, that is, the System.Nullable<T>  type with a
specified type parameter T:
C#
As the example shows, you use the typeof  operator to create a System.T ype instance.
If you want to determine whether an instance is of a nullable value type, don't use the
Object.GetT ype method to get a Type instance to be tested with the preceding code.
When you call the Object.GetT ype method on an instance of a nullable value type, the
instance is boxed  to Object . As boxing of a non-null instance of a nullable value type is
equivalent to boxing of a value of the underlying type, GetType returns a Type instance
that represents the underlying type of a nullable value type:
C#Console.WriteLine( $"Value of aNullable: {aNullable} "); 
object aNullableBoxed = aNullable;  
if (aNullableBoxed is int valueOfA)  
{ 
    Console.WriteLine( $"aNullableBoxed is boxed int: {valueOfA} "); 
} 
// Output:  
// Value of aNullable: 41  
// aNullableBoxed is boxed int: 41  
How to identify a nulla ble value type
Console.WriteLine( $"int? is {(IsNullable( typeof(int?)) ? "nullable"  : "non 
nullable" )} value type" ); 
Console.WriteLine( $"int is {(IsNullable( typeof(int)) ? "nullable"  : "non-
nullable" )} value type" ); 
bool IsNullable (Type type ) => Nullable.GetUnderlyingType(type) != null; 
// Output:  
// int? is nullable value type  
// int is non-nullable value type
int? a = 17; 
Type typeOfA = a.GetType();  
Console.WriteLine(typeOfA.FullName);  
// Output:  
// System.Int32  Also, don't use the is operator to determine whether an instance is of a nullable value
type. As the following example shows, you cannot distinguish types of a nullable value
type instance and its underlying type instance with the is operator:
C#
Instead use the Nullable.GetUnderlyingT ype from the first example and typeof  operator
to check if an instance is of a nullable value type.
For more information, see the following sections of the C# language specification :
Nullable types
Lifted operators
Implicit nullable conversions
Explicit nullable conversions
Lifted conversion operators
C# reference
What exactly does 'lifted' mean?int? a = 14; 
if (a is int) 
{ 
    Console.WriteLine( "int? instance is compatible with int" ); 
} 
int b = 17; 
if (b is int?) 
{ 
    Console.WriteLine( "int instance is compatible with int?" ); 
} 
// Output:  
// int? instance is compatible with int  
// int instance is compatible with int?  
７ Note
The methods described in this section are not applicable in the case of nullable
reference types .
C# language specification
See alsoSystem.Nullable<T>
System.Nullable
Nullable.GetUnderlyingT ype
Nullable reference typesReference types (C# reference)
Article •01/06/2023
There are two kinds of types in C#: reference types and value types. V ariables of
reference types store references to their data (objects), while variables of value types
directly contain their data. With reference types, two variables can reference the same
object; therefore, operations on one variable can affect the object referenced by the
other variable. With value types, each variable has its own copy of the data, and it's not
possible for operations on one variable to affect the other (except in the case of in,
ref, and out parameter variables; see in, ref, and out parameter modifier).
The following keywords are used to declare reference types:
class
interface
delegate
record
C# also provides the following built-in reference types:
dynamic
object
string
C# reference
C# keywords
Pointer types
Value typesSee also６ Collaborat e with us on
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
 Provide product feedbackBuilt-in reference types (C# reference)
Article •02/25/2023
C# has many built-in reference types. They have keywords or operators that are
synonyms for a type in the .NET library.
The object type is an alias for System.Object  in .NET. In the unified type system of C#,
all types, predefined and user-defined, reference types and value types, inherit directly
or indirectly from System.Object . You can assign values of any type to variables of type
object. Any object variable can be assigned to its default value using the literal null.
When a variable of a value type is converted to object, it's said to be boxed. When a
variable of type object is converted to a value type, it's said to be unbo xed. For more
information, see Boxing and Unboxing .
The string type represents a sequence of zero or more Unicode characters. string is
an alias for System.S tring  in .NET.
Although string is a reference type, the equality operators == and != are defined to
compare the values of string objects, not references. V alue based equality makes
testing for string equality more intuitive. For example:
C#
The previous example displays "T rue" and then "F alse" because the content of the
strings is equivalent, but a and b don't refer to the same string instance.
The + operator  concatenates strings:
C#The object type
The string type
string a = "hello";
string b = "h";
// Append to contents of 'b'
b += "ello";
Console.WriteLine(a == b);
Console.WriteLine( object.ReferenceEquals(a, b));The preceding code creates a string object that contains "good morning".
Strings are immut able--the contents of a string object can't be changed after the object
is created. For example, when you write this code, the compiler actually creates a new
string object to hold the new sequence of characters, and that new object is assigned to
b. The memory that had been allocated for b (when it contained the string "h") is then
eligible for garbage collection.
C#
The [] operator  can be used for readonly access to individual characters of a string.
Valid index values start at 0 and must be less than the length of the string:
C#
In similar fashion, the [] operator can also be used for iterating over each character in a
string:
C#
String literals are of type string and can be written in three forms, raw, quoted, and
verbatim.
Raw str ing lit erals are available beginning in C# 11. Raw string literals can contain
arbitrary text without requiring escape sequences. Raw string literals can includestring a = "good " + "morning" ;
string b = "h";
b += "ello";
string str = "test";
char x = str[ 2];  // x = 's';
string str = "test";
for (int i = 0; i < str.Length; i++)
{
  Console.Write(str[i] + " ");
}
// Output: t e s t
String literalswhitespace and new lines, embedded quotes, and other special characters. Raw string
literals are enclosed in a minimum of three double quotation marks ("""):
C#
You can even include a sequence of three (or more) double quote characters. If your text
requires an embedded sequence of quotes, you start and end the raw string literal with
more quote marks, as needed:
C#
Raw string literals typically have the starting and ending quote sequences on separate
lines from the embedded text. Multiline raw string literals support strings that are
themselves quoted strings:
C#
When the starting and ending quotes are on separate lines, the newlines following the
opening quote and preceding the ending quote aren't included in the final content. The
closing quote sequence dictates the leftmost column for the string literal. Y ou can
indent a raw string literal to match the overall code format:
C#"""
This is a multi-line
    string literal with the second line indented.
"""
"""""
This raw string literal has four " """, count them: " """ four!
embedded quote characters in a sequence. That's why it starts and ends
with five double quotes.
You could extend this example with as many embedded quotes as needed for  
your text.
"""""
var message = """
"This is a very important message. "
""";
Console.WriteLine(message);
// output: "This is a very important message."
var message = """
    "This is a very important message. "
    """;Columns to the right of the ending quote sequence are preserved. This behavior enables
raw strings for data formats such as JSON, Y AML, or XML, as shown in the following
example:
C#
The compiler issues an error if any of the text lines extend to the left of the closing
quote sequence. The opening and closing quote sequences can be on the same line,
providing the string literal neither starts nor ends with a quote character:
C#
You can combine raw string literals with string interpolation  to include quote characters
and braces in the output string.
Quoted string literals are enclosed in double quotation marks ("):
C#
String literals can contain any character literal. Escape sequences are included. The
following example uses escape sequence \\ for backslash, \u0066 for the letter f, and
\n for newline.
C#Console.WriteLine(message);
// output: "This is a very important message."
// The leftmost whitespace is not part of the raw string literal
var json= """
    {
        "prop": 0
    }
    """;
var shortText = """He said " hello!" this morning." "";
"good morning"   // a string literal
string a = "\\\u0066\n F" ;
Console.WriteLine(a);
// Output:
// \f
//  FVerbatim string literals  start with @ and are also enclosed in double quotation marks.
For example:
C#
The advantage of verbatim strings is that escape sequences aren't processed, which
makes it easy to write. For example, the following text matches a fully qualified Windows
file name:
C#
To include a double quotation mark in an @-quoted string, double it:
C#
Strings in .NET are stored using UTF-16 encoding. UTF-8 is the standard for W eb
protocols and other important libraries. Beginning in C# 11, you can add the u8 suffix to
a string literal to specify UTF-8 encoding. UTF-8 literals are stored as
ReadOnlySpan<byte> objects. The natural type of a UTF-8 string literal is
ReadOnlySpan<byte>. Using a UTF-8 string literal creates a more clear declaration than
declaring the equivalent System.R eadOnlySpan<T> , as shown in the following code:
C#７ Note
The escape code \udddd (where dddd is a four-digit number) represents the
Unicode character U+ dddd. Eight-digit Unicode escape codes are also recognized:
\Udddddddd.
@"good morning"   // a string literal
@"c:\Docs\Source\a.txt"   // rather than "c:\\Docs\\Source\\a.txt"
@"""Ahoy!"" cried the captain."  // "Ahoy!" cried the captain.
UTF-8 string literals
ReadOnlySpan< byte> AuthWithTrailingSpace = new byte[] { 0x41, 0x55, 0x54, 
0x48, 0x20 };
ReadOnlySpan< byte> AuthStringLiteral = "AUTH "u8;To store a UTF-8 string literal as an array requires the use of ReadOnlySpan<T>.T oArray()
to copy the bytes containing the literal to the mutable array:
C#
UTF-8 string literals aren't compile time constants; they're runtime constants. Therefore,
they can't be used as the default value for an optional parameter. UTF-8 string literals
can't be combined with string interpolation. Y ou can't use the $ token and the u8 suffix
on the same string expression.
The declaration of a delegate type is similar to a method signature. It has a return value
and any number of parameters of any type:
C#
In .NET, System.Action and System.Func types provide generic definitions for many
common delegates. Y ou likely don't need to define new custom delegate types. Instead,
you can create instantiations of the provided generic types.
A delegate is a reference type that can be used to encapsulate a named or an
anonymous method. Delegates are similar to function pointers in C++; however,
delegates are type-safe and secure. For applications of delegates, see Delegates  and
Generic Delegates . Delegates are the basis for Events . A delegate can be instantiated by
associating it either with a named or anonymous method.
The delegate must be instantiated with a method or lambda expression that has a
compatible return type and input parameters. For more information on the degree of
variance that is allowed in the method signature, see Variance in Delegates . For use with
anonymous methods, the delegate and the code to be associated with it are declared
together.
Delegate combination or removal fails with a runtime exception when the delegate
types involved at run time are different due to variant conversion. The following
example demonstrates a situation that fails:byte[] AuthStringLiteral = "AUTH "u8.ToArray();
The delegate type
public delegate  void MessageDelegate (string message );
public delegate  int AnotherDelegate (MyType m, long num);C#
You can create a delegate with the correct runtime type by creating a new delegate
object. The following example demonstrates how this workaround may be applied to
the preceding example.
C#
You can declare function point ers, which use similar syntax. A function pointer uses the
calli instruction instead of instantiating a delegate type and calling the virtual Invoke
method.
The dynamic type indicates that use of the variable and references to its members
bypass compile-time type checking. Instead, these operations are resolved at run time.
The dynamic type simplifies access to C OM APIs such as the Office Automation APIs, to
dynamic APIs such as IronPython libraries, and to the HTML Document Object Model
(DOM).
Type dynamic behaves like type object in most circumstances. In particular, any non-
null expression can be converted to the dynamic type. The dynamic type differs from
object in that operations that contain expressions of type dynamic aren't resolved or
type checked by the compiler. The compiler packages together information about the
operation, and that information is later used to evaluate the operation at run time. As
part of the process, variables of type dynamic are compiled into variables of type
object. Therefore, type dynamic exists only at compile time, not at run time.Action<string> stringAction = str => {};
Action<object> objectAction = obj => {};
  
// Valid due to implicit reference conversion of
// objectAction to Action<string>, but may fail
// at run time.
Action<string> combination = stringAction + objectAction;
Action<string> stringAction = str => {};
Action<object> objectAction = obj => {};
  
// Creates a new delegate instance with a runtime type of Action<string>.
Action<string> wrappedObjectAction = new Action< string>(objectAction);
// The two Action<string> delegate instances can now be combined.
Action<string> combination = stringAction + wrappedObjectAction;
The dynamic typeThe following example contrasts a variable of type dynamic to a variable of type object.
To verify the type of each variable at compile time, place the mouse pointer over dyn or
obj in the WriteLine statements. Copy the following code into an editor where
IntelliSense is available. IntelliSense shows dynamic  for dyn and object  for obj.
C#
The WriteLine  statements display the run-time types of dyn and obj. At that point, both
have the same type, integer. The following output is produced:
Console
To see the difference between dyn and obj at compile time, add the following two lines
between the declarations and the WriteLine statements in the previous example.
C#
A compiler error is reported for the attempted addition of an integer and an object in
expression obj + 3. However, no error is reported for dyn + 3. The expression that
contains dyn isn't checked at compile time because the type of dyn is dynamic.
The following example uses dynamic in several declarations. The Main method also
contrasts compile-time type checking with run-time type checking.
C#class Program
{
    static void Main(string[] args)
    {
        dynamic dyn = 1;
        object obj = 1;
        // Rest the mouse pointer over dyn and obj to see their
        // types at compile time.
        System.Console.WriteLine(dyn.GetType());
        System.Console.WriteLine(obj.GetType());
    }
}
System.Int32
System.Int32
dyn = dyn + 3;
obj = obj + 3;using System;
namespace  DynamicExamples
{
    class Program
    {
        static void Main(string[] args)
        {
            ExampleClass ec = new ExampleClass();
            Console.WriteLine(ec.ExampleMethod( 10));
            Console.WriteLine(ec.ExampleMethod( "value"));
            // The following line causes a compiler error because  
ExampleMethod
            // takes only one argument.
            //Console.WriteLine(ec.ExampleMethod(10, 4));
            dynamic dynamic_ec = new ExampleClass();
            Console.WriteLine(dynamic_ec.ExampleMethod( 10));
            // Because dynamic_ec is dynamic, the following call to  
ExampleMethod
            // with two arguments does not produce an error at compile time.
            // However, it does cause a run-time error.
            //Console.WriteLine(dynamic_ec.ExampleMethod(10, 4));
        }
    }
    class ExampleClass
    {
        static dynamic _field;
        dynamic Prop { get; set; }
        public dynamic ExampleMethod (dynamic d)
        {
            dynamic local = "Local variable" ;
            int two = 2;
            if (d is int)
            {
                return local;
            }
            else
            {
                return two;
            }
        }
    }
}
// Results:
// Local variable
// 2
// Local variableFor more information, see the following sections of the C# language specification :
§8.2.3 The object type
§8.2.4 The dynamic type
§8.2.5 The string type
§8.2.8 Delegate types
C# 11 - Raw string literals
C# 11 - Raw string literals
C# Reference
C# Keywords
Events
Using T ype dynamic
Best Practices for Using S trings
Basic S tring Operations
Creating New S trings
Type-testing and cast operators
How to safely cast using pattern matching and the as and is operators
Walkthrough: creating and using dynamic objects
System.Object
System.S tring
System.Dynamic.DynamicObjectC# language specification
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
 Provide product feedbackRecords (C# reference)
Article •05/25/2023
You use the record modifier to define a reference type  that provides built-in
functionality for encapsulating data. C# 10 allows the record class syntax as a synonym
to clarify a reference type, and record struct to define a value type  with similar
functionality.
When you declare a primary constructor  on a record, the compiler generates public
properties for the primary constructor parameters. The primary constructor parameters
to a record are referred to as positional p aramet ers. The compiler creates positional
properties that mirror the primary constructor or positional parameters. The compiler
doesn't synthesize properties for primary constructor parameters on types that don't
have the record modifier.
The following two examples demonstrate record (or record class) reference types:
C#
C#
The following two examples demonstrate record struct value types:
C#
C#public record Person(string FirstName, string LastName );
public record Person
{
    public required string FirstName { get; init; }
    public required string LastName { get; init; }
};
public readonly  record struct Point(double X, double Y, double Z);
public record struct Point
{
    public double X { get; init; }
    public double Y { get; init; }
    public double Z { get; init; }
}You can also create records with mutable properties and fields:
C#
Record structs can be mutable as well, both positional record structs and record structs
with no positional parameters:
C#
C#
While records can be mutable, they're primarily intended for supporting immutable data
models. The record type offers the following features:
Concise syntax for creating a reference type with immutable properties
Built-in behavior useful for a data-centric reference type:
Value equality
Concise syntax for nondestructive mutation
Built-in formatting for display
Support for inheritance hierarchies
The preceding examples show some distinctions between records that are reference
types and records that are value types:
A record or a record class declares a reference type. The class keyword is
optional, but can add clarity for readers. A record struct declares a value type.
Positional properties are immut able in a record class and a readonly record
struct. They're mutable in a record struct.public record Person
{
    public required string FirstName { get; set; }
    public required string LastName { get; set; }
};
public record struct DataMeasurement (DateTime TakenAt, double Measurement );
public record struct Point
{
    public double X { get; set; }
    public double Y { get; set; }
    public double Z { get; set; }
}The remainder of this article discusses both record class and record struct types. The
differences are detailed in each section. Y ou should decide between a record class and
a record struct similar to deciding between a class and a struct. The term record is
used to describe behavior that applies to all record types. Either record struct or
record class is used to describe behavior that applies to only struct or class types,
respectively. The record struct type was introduced in C# 10.
You can use positional parameters to declare properties of a record and to initialize the
property values when you create an instance:
C#
When you use the positional syntax for property definition, the compiler creates:
A public autoimplemented property for each positional parameter provided in the
record declaration.
For record types and readonly record struct types: An init-only  property.
For record struct types: A read-write property.
A primary constructor whose parameters match the positional parameters on the
record declaration.
For record struct types, a parameterless constructor that sets each field to its
default value.
A Deconstruct method with an out parameter for each positional parameter
provided in the record declaration. The method deconstructs properties defined by
using positional syntax; it ignores properties that are defined by using standard
property syntax.
You may want to add attributes to any of these elements the compiler creates from the
record definition. Y ou can add a target to any attribute you apply to the positional
record's properties. The following example applies the
System.T ext.Json.Serialization.JsonPropertyNameAttribute  to each property of thePositional syntax for property definitio n
public record Person(string FirstName, string LastName );
public static void Main()
{
    Person person = new("Nancy", "Davolio" );
    Console.WriteLine(person);
    // output: Person { FirstName = Nancy, LastName = Davolio }
}Person record. The property: target indicates that the attribute is applied to the
compiler-generated property. Other values are field: to apply the attribute to the field,
and param: to apply the attribute to the parameter.
C#
The preceding example also shows how to create XML documentation comments for
the record. Y ou can add the <param> tag to add documentation for the primary
constructor's parameters.
If the generated autoimplemented property definition isn't what you want, you can
define your own property of the same name. For example, you may want to change
accessibility or mutability, or provide an implementation for either the get or set
accessor. If you declare the property in your source, you must initialize it from the
positional parameter of the record. If your property is an autoimplemented property,
you must initialize the property. If you add a backing field in your source, you must
initialize the backing field. The generated deconstructor uses your property definition.
For instance, the following example declares the FirstName and LastName properties of
a positional record public, but restricts the Id positional parameter to internal. You
can use this syntax for records and record struct types.
C#/// <summary>
/// Person record type
/// </summary>
/// <param name="FirstName"> First Name </param>
/// <param name="LastName"> Last Name </param>
/// <remarks>
/// The person type is a positional record containing the
/// properties for the first and last name. Those properties
/// map to the JSON elements "firstName" and "lastName" when
/// serialized or deserialized.
/// </remarks>
public record Person([property: JsonPropertyName( "firstName" )] string 
FirstName, 
    [property: JsonPropertyName ("lastName" )] string LastName) ;
public record Person(string FirstName, string LastName, string Id)
{
    internal  string Id { get; init; } = Id;
}
public static void Main()
{
    Person person = new("Nancy", "Davolio" , "12345");
    Console.WriteLine(person.FirstName); //output: NancyA record type doesn't have to declare any positional properties. Y ou can declare a
record without any positional properties, and you can declare other fields and
properties, as in the following example:
C#
If you define properties by using standard property syntax but omit the access modifier,
the properties are implicitly private.
A positional r ecord and a positional r eadonly r ecord struct declare init-only properties. A
positional r ecord struct declares read-write properties. Y ou can override either of those
defaults, as shown in the previous section.
Immutability can be useful when you need a data-centric type to be thread-safe or
you're depending on a hash code remaining the same in a hash table. Immutability isn't
appropriate for all data scenarios, however. Entity Framework Core , for example, doesn't
support updating with immutable entity types.
Init-only properties, whether created from positional parameters ( record class, and
readonly record struct) or by specifying init accessors, have shallo w immut ability .
After initialization, you can't change the value of value-type properties or the reference
of reference-type properties. However, the data that a reference-type property refers to
can be changed. The following example shows that the content of a reference-type
immutable property (an array in this case) is mutable:
C#}
public record Person(string FirstName, string LastName )
{
    public string[] PhoneNumbers { get; init; } = Array.Empty< string>();
};
Immutability
public record Person(string FirstName, string LastName, string[] 
PhoneNumbers );
public static void Main()
{
    Person person = new("Nancy", "Davolio" , new string[1] { "555-1234"  });
    Console.WriteLine(person.PhoneNumbers[ 0]); // output: 555-1234The features unique to record types are implemented by compiler-synthesized methods,
and none of these methods compromises immutability by modifying object state.
Unless specified, the synthesized methods are generated for record, record struct, and
readonly record struct declarations.
If you don't override or replace equality methods, the type you declare governs how
equality is defined:
For class types, two objects are equal if they refer to the same object in memory.
For struct types, two objects are equal if they are of the same type and store the
same values.
For types with the record modifier ( record class, record struct, and readonly
record struct), two objects are equal if they are of the same type and store the
same values.
The definition of equality for a record struct is the same as for a struct. The difference
is that for a struct, the implementation is in ValueT ype.Equals(Object)  and relies on
reflection. For records, the implementation is compiler synthesized and uses the
declared data members.
Reference equality is required for some data models. For example, Entity Framework
Core  depends on reference equality to ensure that it uses only one instance of an entity
type for what is conceptually one entity. For this reason, records and record structs
aren't appropriate for use as entity types in Entity Framework Core.
The following example illustrates value equality of record types:
C#    person.PhoneNumbers[ 0] = "555-6789" ;
    Console.WriteLine(person.PhoneNumbers[ 0]); // output: 555-6789
}
Value equality
public record Person(string FirstName, string LastName, string[] 
PhoneNumbers );
public static void Main()
{
    var phoneNumbers = new string[2];
    Person person1 = new("Nancy", "Davolio" , phoneNumbers);
    Person person2 = new("Nancy", "Davolio" , phoneNumbers);
    Console.WriteLine(person1 == person2); // output: TrueTo implement value equality, the compiler synthesizes several methods, including:
An override of Object.Equals(Object) . It's an error if the override is declared
explicitly.
This method is used as the basis for the Object.Equals(Object, Object)  static
method when both parameters are non-null.
A virtual, or sealed, Equals(R? other) where R is the record type. This method
implements IEquatable<T> . This method can be declared explicitly.
If the record type is derived from a base record type Base, Equals(Base? other).
It's an error if the override is declared explicitly. If you provide your own
implementation of Equals(R? other), provide an implementation of GetHashCode
also.
An override of Object.GetHashCode() . This method can be declared explicitly.
Overrides of operators == and !=. It's an error if the operators are declared
explicitly.
If the record type is derived from a base record type, protected override Type
EqualityContract { get; };. This property can be declared explicitly. For more
information, see Equality in inheritance hierarchies .
The compiler doesn't synthesize a method when a record type has a method that
matches the signature of a synthesized method allowed to be declared explicitly.
If you need to copy an instance with some modifications, you can use a with expression
to achieve nondestr uctive mut ation . A with expression makes a new record instance that
is a copy of an existing record instance, with specified properties and fields modified.
You use object initializer  syntax to specify the values to be changed, as shown in the
following example:
C#    person1.PhoneNumbers[ 0] = "555-1234" ;
    Console.WriteLine(person1 == person2); // output: True
    Console.WriteLine(ReferenceEquals(person1, person2)); // output: False
}
Nondestructive mutationThe with expression can set positional properties or properties created by using
standard property syntax. Explicitly declared properties must have an init or set
accessor to be changed in a with expression.
The result of a with expression is a shallo w copy, which means that for a reference
property, only the reference to an instance is copied. Both the original record and the
copy end up with a reference to the same instance.
To implement this feature for record class types, the compiler synthesizes a clone
method and a copy constructor. The virtual clone method returns a new record
initialized by the copy constructor. When you use a with expression, the compiler
creates code that calls the clone method and then sets the properties that are specified
in the with expression.
If you need different copying behavior, you can write your own copy constructor in a
record class. If you do that, the compiler doesn't synthesize one. Make your
constructor private if the record is sealed, otherwise make it protected. The compiler
doesn't synthesize a copy constructor for record struct types. Y ou can write one, butpublic record Person(string FirstName, string LastName )
{
    public string[] PhoneNumbers { get; init; }
}
public static void Main()
{
    Person person1 = new("Nancy", "Davolio" ) { PhoneNumbers = new string[1] 
};
    Console.WriteLine(person1);
    // output: Person { FirstName = Nancy, LastName = Davolio, PhoneNumbers  
= System.String[] }
    Person person2 = person1 with { FirstName = "John" };
    Console.WriteLine(person2);
    // output: Person { FirstName = John, LastName = Davolio, PhoneNumbers =  
System.String[] }
    Console.WriteLine(person1 == person2); // output: False
    person2 = person1 with { PhoneNumbers = new string[1] };
    Console.WriteLine(person2);
    // output: Person { FirstName = Nancy, LastName = Davolio, PhoneNumbers  
= System.String[] }
    Console.WriteLine(person1 == person2); // output: False
    person2 = person1 with { };
    Console.WriteLine(person1 == person2); // output: True
}the compiler doesn't generate calls to it for with expressions. The values of the record
struct are copied on assignment.
You can't override the clone method, and you can't create a member named Clone in
any record type. The actual name of the clone method is compiler-generated.
Record types have a compiler-generated ToString  method that displays the names and
values of public properties and fields. The ToString method returns a string of the
following format:
<record type name> { <property name> = <value>, <property name> = <value>,
...}
The string printed for <value> is the string returned by the ToString()  for the type of the
property. In the following example, ChildNames is a System.Array , where ToString
returns System.String[]:
To implement this feature, in record class types, the compiler synthesizes a virtual
PrintMembers method and a ToString  override. In record struct types, this member is
private. The ToString override creates a StringBuilder  object with the type name
followed by an opening bracket. It calls PrintMembers to add property names and
values, then adds the closing bracket. The following example shows code similar to what
the synthesized override contains:
C#Built-in formatting  for display
Person { FirstName = Nancy, LastName = Davolio, ChildNames = System.String[]  
}
public override  string ToString ()
{
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.Append( "Teacher" ); // type name
    stringBuilder.Append( " { ");
    if (PrintMembers(stringBuilder))
    {
        stringBuilder.Append( " ");
    }
    stringBuilder.Append( "}");You can provide your own implementation of PrintMembers or the ToString override.
Examples are provided in the PrintMembers  formatting in derived records  section later
in this article. In C# 10 and later, your implementation of ToString may include the
sealed modifier, which prevents the compiler from synthesizing a ToString
implementation for any derived records. Y ou can create a consistent string
representation throughout a hierarchy of record types. (Derived records still have a
PrintMembers method generated for all derived properties.)
This section only applies to record class types.
A record can inherit from another record. However, a record can't inherit from a class,
and a class can't inherit from a record.
The derived record declares positional parameters for all the parameters in the base
record primary constructor. The base record declares and initializes those properties.
The derived record doesn't hide them, but only creates and initializes properties for
parameters that aren't declared in its base record.
The following example illustrates inheritance with positional property syntax:
C#    return stringBuilder.ToString();
}
Inheritance
Positional parameters in derived record types
public abstract  record Person(string FirstName, string LastName );
public record Teacher(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public static void Main()
{
    Person teacher = new Teacher( "Nancy", "Davolio" , 3);
    Console.WriteLine(teacher);
    // output: Teacher { FirstName = Nancy, LastName = Davolio, Grade = 3 }
}
Equality in inheritance hierarchiesThis section applies to record class types, but not record struct types. For two record
variables to be equal, the run-time type must be equal. The types of the containing
variables might be different. Inherited equality comparison is illustrated in the following
code example:
C#
In the example, all variables are declared as Person, even when the instance is a derived
type of either Student or Teacher. The instances have the same properties and the same
property values. But student == teacher returns False although both are Person-type
variables, and student == student2 returns True although one is a Person variable and
one is a Student variable. The equality test depends on the runtime type of the actual
object, not the declared type of the variable.
To implement this behavior, the compiler synthesizes an EqualityContract property that
returns a Type object that matches the type of the record. The EqualityContract enables
the equality methods to compare the runtime type of objects when they're checking for
equality. If the base type of a record is object, this property is virtual. If the base type
is another record type, this property is an override. If the record type is sealed, this
property is effectively sealed because the type is sealed.
When code compares two instances of a derived type, the synthesized equality methods
check all data members of the base and derived types for equality. The synthesized
GetHashCode method uses the GetHashCode method from all data members declared in
the base type and the derived record type. The data members of a record include all
declared fields and the compiler-synthesized backing field for any autoimplemented
properties.public abstract  record Person(string FirstName, string LastName );
public record Teacher(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public record Student(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public static void Main()
{
    Person teacher = new Teacher( "Nancy", "Davolio" , 3);
    Person student = new Student( "Nancy", "Davolio" , 3);
    Console.WriteLine(teacher == student); // output: False
    Student student2 = new Student( "Nancy", "Davolio" , 3);
    Console.WriteLine(student2 == student); // output: True
}
with expressions in derived recordsThe result of a with expression has the same run-time type as the expression's operand.
All properties of the run-time type get copied, but you can only set properties of the
compile-time type, as the following example shows:
C#
The synthesized PrintMembers method of a derived record type calls the base
implementation. The result is that all public properties and fields of both derived and
base types are included in the ToString output, as shown in the following example:
C#public record Point(int X, int Y)
{
    public int Zbase { get; set; }
};
public record NamedPoint (string Name, int X, int Y) : Point(X, Y)
{
    public int Zderived { get; set; }
};
public static void Main()
{
    Point p1 = new NamedPoint( "A", 1, 2) { Zbase = 3, Zderived = 4 };
    Point p2 = p1 with { X = 5, Y = 6, Zbase = 7 }; // Can't set Name or  
Zderived
    Console.WriteLine(p2 is NamedPoint);  // output: True
    Console.WriteLine(p2);
    // output: NamedPoint { X = 5, Y = 6, Zbase = 7, Name = A, Zderived = 4  
}
    Point p3 = (NamedPoint)p1 with { Name = "B", X = 5, Y = 6, Zbase = 7, 
Zderived = 8 };
    Console.WriteLine(p3);
    // output: NamedPoint { X = 5, Y = 6, Zbase = 7, Name = B, Zderived = 8  
}
}
PrintMembers formatting in derived records
public abstract  record Person(string FirstName, string LastName );
public record Teacher(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public record Student(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public static void Main()
{You can provide your own implementation of the PrintMembers method. If you do that,
use the following signature:
For a sealed record that derives from object (doesn't declare a base record):
private bool PrintMembers(StringBuilder builder);
For a sealed record that derives from another record (note that the enclosing type
is sealed, so the method is effectively sealed): protected override bool
PrintMembers(StringBuilder builder);
For a record that isn't sealed and derives from object: protected virtual bool
PrintMembers(StringBuilder builder);
For a record that isn't sealed and derives from another record: protected override
bool PrintMembers(StringBuilder builder);
Here's an example of code that replaces the synthesized PrintMembers methods, one for
a record type that derives from object, and one for a record type that derives from
another record:
C#    Person teacher = new Teacher( "Nancy", "Davolio" , 3);
    Console.WriteLine(teacher);
    // output: Teacher { FirstName = Nancy, LastName = Davolio, Grade = 3 }
}
public abstract  record Person(string FirstName, string LastName, string[] 
PhoneNumbers )
{
    protected  virtual bool PrintMembers (StringBuilder stringBuilder )
    {
        stringBuilder.Append( $"FirstName = {FirstName} , LastName = 
{LastName} , ");
        stringBuilder.Append( $"PhoneNumber1 = {PhoneNumbers[ 0]}, 
PhoneNumber2 = {PhoneNumbers[ 1]}");
        return true;
    }
}
public record Teacher(string FirstName, string LastName, string[] 
PhoneNumbers, int Grade)
    : Person(FirstName, LastName, PhoneNumbers )
{
    protected  override  bool PrintMembers (StringBuilder stringBuilder )
    {
        if (base.PrintMembers(stringBuilder))
        {
            stringBuilder.Append( ", ");
        };
        stringBuilder.Append( $"Grade = {Grade}");The Deconstruct method of a derived record returns the values of all positional
properties of the compile-time type. If the variable type is a base record, only the base
record properties are deconstructed unless the object is cast to the derived type. The
following example demonstrates calling a deconstructor on a derived record.
C#        return true;
    }
};
public static void Main()
{
    Person teacher = new Teacher( "Nancy", "Davolio" , new string[2] { "555-
1234", "555-6789"  }, 3);
    Console.WriteLine(teacher);
    // output: Teacher { FirstName = Nancy, LastName = Davolio, PhoneNumber1  
= 555-1234, PhoneNumber2 = 555-6789, Grade = 3 }
}
７ Note
In C# 10 and later, the compiler will synthesize PrintMembers in derived records
even when a base record has sealed the ToString method. Y ou can also create your
own implementation of PrintMembers.
Deconstructor behavior in derived records
public abstract  record Person(string FirstName, string LastName );
public record Teacher(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public record Student(string FirstName, string LastName, int Grade)
    : Person(FirstName, LastName );
public static void Main()
{
    Person teacher = new Teacher( "Nancy", "Davolio" , 3);
    var (firstName, lastName) = teacher; // Doesn't deconstruct Grade
    Console.WriteLine( $"{firstName} , {lastName} ");// output: Nancy, Davolio
    var (fName, lName, grade) = (Teacher)teacher;
    Console.WriteLine( $"{fName}, {lName}, {grade}");// output: Nancy,  
Davolio, 3
}The record keyword is a modifier for either a class or struct type. Adding the record
modifier includes the behavior described earlier in this article. There's no generic
constraint that requires a type to be a record. A record class satisfies the class
constraint. A record struct satisfies the struct constraint. For more information, see
Constraints on type parameters .
For more information, see the Classes  section of the C# language specification .
For more information about these features, see the following feature proposal notes:
Records
Init-only setters
Covariant returns
C# reference
Design guidelines - Choosing between class and struct
Design guidelines - S truct design
The C# type system
with expressionGeneric constraints
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
 Provide product feedbackclass (C# Reference)
Article •09/17/2021
Classes are declared using the keyword class, as shown in the following example:
C#
Only single inheritance is allowed in C#. In other words, a class can inherit
implementation from one base class only. However, a class can implement more than
one interface. The following table shows examples of class inheritance and interface
implementation:
Inher itance Example
None class ClassA { }
Single class DerivedClass : BaseClass { }
None, implements two interfaces class ImplClass : IFace1, IFace2 { }
Single, implements one interface class ImplDerivedClass : BaseClass, IFace1 { }
Classes that you declare directly within a namespace, not nested within other classes,
can be either public  or internal . Classes are internal by default.
Class members, including nested classes, can be public , protected internal , protected ,
internal , private , or private protected . Members are private by default.
For more information, see Access Modifiers .
You can declare generic classes that have type parameters. For more information, see
Generic Classes .
A class can contain declarations of the following members:
Constructorsclass TestClass  
{ 
    // Methods, properties, fields, events, delegates  
    // and nested classes go here.  
} 
RemarksConstants
Fields
Finalizers
Methods
Properties
Indexers
Operators
Events
Delegates
Classes
Interfaces
Structure types
Enumeration types
The following example demonstrates declaring class fields, constructors, and methods. It
also demonstrates object instantiation and printing instance data. In this example, two
classes are declared. The first class, Child, contains two private fields ( name and age),
two public constructors and one public method. The second class, StringTest, is used
to contain Main.
C#Example
class Child 
{ 
    private int age; 
    private string name; 
    // Default constructor:  
    public Child() 
    { 
        name = "N/A"; 
    } 
    // Constructor:  Notice that in the previous example the private fields ( name and age) can only be
accessed through the public method of the Child class. For example, you cannot print
the child's name, from the Main method, using a statement like this:
C#    public Child(string name, int age) 
    { 
        this.name = name;  
        this.age = age;  
    } 
    // Printing method:  
    public void PrintChild () 
    { 
        Console.WriteLine( "{0}, {1} years old." , name, age);  
    } 
} 
class StringTest  
{ 
    static void Main() 
    { 
        // Create objects by using the new operator:  
        Child child1 = new Child("Craig", 11); 
        Child child2 = new Child("Sally", 10); 
        // Create an object using the default constructor:  
        Child child3 = new Child();  
        // Display results:  
        Console.Write( "Child #1: " ); 
        child1.PrintChild();  
        Console.Write( "Child #2: " ); 
        child2.PrintChild();  
        Console.Write( "Child #3: " ); 
        child3.PrintChild();  
    } 
} 
/* Output:  
    Child #1: Craig, 11 years old.  
    Child #2: Sally, 10 years old.  
    Child #3: N/A, 0 years old.  
*/ 
Comments
Console.Write(child1.name);   // Error  Accessing private members of Child from Main would only be possible if Main were a
member of the class.
Types declared inside a class without an access modifier default to private, so the data
members in this example would still be private if the keyword were removed.
Finally, notice that for the object created using the parameterless constructor ( child3),
the age field was initialized to zero by default.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Reference T ypesC# language specification
See alsointerface (C# Reference)
Article •12/08/2022
An interface defines a contract. Any class  or struct  that implements that contract must
provide an implementation of the members defined in the interface. An interface may
define a default implementation for members. It may also define static  members in
order to provide a single implementation for common functionality. Beginning with C#
11, an interface may define static abstract or static virtual members to declare that
an implementing type must provide the declared members. T ypically, static virtual
methods declare that an implementation must define a set of overloaded operators .
In the following example, class ImplementationClass must implement a method named
SampleMethod that has no parameters and returns void.
For more information and examples, see Interfaces .
C#
An interface can be a member of a namespace or a class. An interface declaration can
contain declarations (signatures without any implementation) of the following members:Example interface
interface  ISampleInterface  
{ 
    void SampleMethod (); 
} 
class ImplementationClass  : ISampleInterface  
{ 
    // Explicit interface member implementation:  
    void ISampleInterface.SampleMethod()  
    { 
        // Method implementation.
    } 
    static void Main() 
    { 
        // Declare an interface instance.  
        ISampleInterface obj = new ImplementationClass();  
        // Call the member.  
        obj.SampleMethod();  
    } 
} Methods
Properties
Indexers
Events
These preceding member declarations typically don't contain a body. An interface
member may declare a body. Member bodies in an interface are the default
implement ation . Members with bodies permit the interface to provide a "default"
implementation for classes and structs that don't provide an overriding implementation.
An interface may include:
Constants
Operators
Static constructor .
Nested types
Static fields, methods, properties, indexers, and events
Member declarations using the explicit interface implementation syntax .
Explicit access modifiers (the default access is public ).
Beginning with C# 11, an interface may declare static abstract and static virtual
members for all member types except fields. Interfaces can declare that implementing
types must define operators or other static members. This feature enables generic
algorithms to specify number-like behavior. Y ou can see examples in the numeric types
in the .NET runtime, such as System.Numerics.INumber<T Self> . These interfaces define
common mathematical operators that are implemented by many numeric types. The
compiler must resolve calls to static virtual and static abstract methods at compile
time. The static virtual and static abstract methods declared in interfaces don't
have a runtime dispatch mechanism analogous to virtual or abstract methods
declared in classes. Instead, the compiler uses type information available at compile
time. Therefore, static virtual methods are almost exclusively declared in generic
interfaces . Furthermore, most interfaces that declare static virtual or static abstract
methods declare that one of the type parameters must implement the declared
interface . For example, the INumber<T> interface declares that T must implement
INumber<T>. The compiler uses the type argument to resolve calls to the methods and
operators declared in the interface declaration. For example, the int type implementsDefault interface members
Static abstract and virtual membersINumber<int>. When the type parameter T denotes the type argument int, the static
members declared on int are invoked. Alternatively, when double is the type argument,
the static members declared on the double type are invoked.
You can try this feature by working with the tutorial on static abstract members in
interfaces .
Interfaces may not contain instance state. While static fields are now permitted, instance
fields aren't permitted in interfaces. Instance auto-properties  aren't supported in
interfaces, as they would implicitly declare a hidden field. This rule has a subtle effect on
property declarations. In an interface declaration, the following code doesn't declare an
auto-implemented property as it does in a class or struct. Instead, it declares a
property that doesn't have a default implementation but must be implemented in any
type that implements the interface:
C#
An interface can inherit from one or more base interfaces. When an interface overrides a
method  implemented in a base interface, it must use the explicit interface
implementation  syntax.
When a base type list contains a base class and interfaces, the base class must come first
in the list.
A class that implements an interface can explicitly implement members of that interface.
An explicitly implemented member can't be accessed through a class instance, but only） Impor tant
Method dispatch for static abstract and static virtual methods declared in
interfaces is resolved using the compile time type of an expression. If the runtime
type of an expression is derived from a different compile time type, the static
methods on the base (compile time) type will be called.
Interface inheritance
public interface  INamed 
{ 
  public string Name {get; set;} 
} through an instance of the interface. In addition, default interface members can only be
accessed through an instance of the interface.
For more information about explicit interface implementation, see Explicit Interface
Implementation .
The following example demonstrates interface implementation. In this example, the
interface contains the property declaration and the class contains the implementation.
Any instance of a class that implements IPoint has integer properties x and y.
C#Example interface implementation
interface  IPoint 
{ 
    // Property signatures:  
    int X { get; set; } 
    int Y { get; set; } 
    double Distance { get; } 
} 
class Point : IPoint 
{ 
    // Constructor:  
    public Point(int x, int y) 
    { 
        X = x;  
        Y = y;  
    } 
    // Property implementation:  
    public int X { get; set; } 
    public int Y { get; set; } 
    // Property implementation  
    public double Distance =>  
       Math.Sqrt(X * X + Y * Y);  
} 
class MainClass  
{ 
    static void PrintPoint (IPoint p ) 
    { 
        Console.WriteLine( "x={0}, y={1}" , p.X, p.Y);  
    } For more information, see the Interfaces  section of the C# language specification , the
feature specification for C# 8 - Default interface members , and the feature spec for C#
11 - static abstract members in interfaces
C# Reference
C# Programming Guide
C# Keywords
Reference T ypes
Interfaces
Using Properties
Using Indexers    static void Main() 
    { 
        IPoint p = new Point(2, 3); 
        Console.Write( "My Point: " ); 
        PrintPoint(p);  
    } 
} 
// Output: My Point: x=2, y=3  
C# language specification
See alsoNullable reference types (C# reference)
Article •10/07/2022
Nullable reference types are available in code that has opted in to a nullable awar e
context. Nullable reference types, the null static analysis warnings, and the null-forgiving
operator  are optional language features. All are turned off by default. A nullable c ontext
is controlled at the project level using build settings, or in code using pragmas.
In a nullable aware context:
A variable of a reference type T must be initialized with non-null, and may never
be assigned a value that may be null.
A variable of a reference type T? may be initialized with null or assigned null,
but is required to be checked against null before de-referencing.
A variable m of type T? is considered to be non-null when you apply the null-
forgiving operator, as in m!.
The distinctions between a non-nullable reference type T and a nullable reference type
T? are enforced by the compiler's interpretation of the preceding rules. A variable of
type T and a variable of type T? are represented by the same .NET type. The following
example declares a non-nullable string and a nullable string, and then uses the null-
forgiving operator to assign a value to a non-nullable string:
C#７ Note
This article covers nullable reference types. Y ou can also declare nullable v alue
types .
） Impor tant
All project templates starting with .NET 6 (C# 10) enable the nullable c ontext for the
project. Projects created with earlier templates don't include this element, and
these features are off unless you enable them in the project file or use pragmas.
string notNull = "Hello"; 
string? nullable = default; 
notNull = nullable!; // null forgiveness  The variables notNull and nullable are both represented by the String  type. Because
the non-nullable and nullable types are both stored as the same type, there are several
locations where using a nullable reference type isn't allowed. In general, a nullable
reference type can't be used as a base class or implemented interface. A nullable
reference type can't be used in any object creation or type testing expression. A nullable
reference type can't be the type of a member access expression. The following examples
show these constructs:
C#
The examples in the previous section illustrate the nature of nullable reference types.
Nullable reference types aren't new class types, but rather annotations on existing
reference types. The compiler uses those annotations to help you find potential null
reference errors in your code. There's no runtime difference between a non-nullable
reference type and a nullable reference type. The compiler doesn't add any runtime
checking for non-nullable reference types. The benefits are in the compile-time analysis.
The compiler generates warnings that help you find and fix potential null errors in your
code. Y ou declare your intent, and the compiler warns you when your code violates that
intent.
In a nullable enabled context, the compiler performs static analysis on variables of any
reference type, both nullable and non-nullable. The compiler tracks the null-st ate of
each reference variable as either not-null or maybe-null . The default state of a non-
nullable reference is not-null. The default state of a nullable reference is maybe-null .
Non-nullable reference types should always be safe to dereference because their null-
state is not-null. To enforce that rule, the compiler issues warnings if a non-nullablepublic MyClass : System.Object? // not allowed  
{ 
} 
var nullEmpty = System.String?.Empty; // Not allowed  
var maybeObject = new object?(); // Not allowed  
try 
{ 
    if (thing is string? nullableString) // not allowed  
        Console.WriteLine(nullableString);  
} catch (Exception? e) // Not Allowed  
{ 
    Console.WriteLine( "error"); 
} 
Nullable references and static analysisreference type isn't initialized to a non-null value. Local variables must be assigned
where they're declared. Every field must be assigned a not-null value, in a field initializer
or every constructor. The compiler issues warnings when a non-nullable reference is
assigned to a reference whose state is maybe-null . Generally, a non-nullable reference is
not-null and no warnings are issued when those variables are dereferenced.
Nullable reference types may be initialized or assigned to null. Therefore, static analysis
must determine that a variable is not-null before it's dereferenced. If a nullable reference
is determined to be maybe-null , assigning to a non-nullable reference variable
generates a compiler warning. The following class shows examples of these warnings:
C#７ Note
If you assign a maybe-null  expression to a non-nullable reference type, the
compiler generates a warning. The compiler then generates warnings for that
variable until it's assigned to a not-null expression.
public class ProductDescription  
{ 
    private string shortDescription;  
    private string? detailedDescription;  
    public ProductDescription () // Warning! shortDescription not  
initialized.  
    { 
    } 
    public ProductDescription (string productDescription ) => 
        this.shortDescription = productDescription;  
    public void SetDescriptions (string productDescription, string? 
details= null) 
    { 
        shortDescription = productDescription;  
        detailedDescription = details;  
    } 
    public string GetDescription () 
    { 
        if (detailedDescription.Length == 0) // Warning! dereference  
possible null  
        {  
            return shortDescription;  
        }  
        else 
        {  The following snippet shows where the compiler emits warnings when using this class:
C#
The preceding examples demonstrate how compiler's static analysis determines the
null-st ate of reference variables. The compiler applies language rules for null checks and
assignments to inform its analysis. The compiler can't make assumptions about the
semantics of methods or properties. If you call methods that perform null checks, the
compiler can't know those methods affect a variable's null-st ate. There are attributes
you can add to your APIs to inform the compiler about the semantics of arguments and
return values. These attributes have been applied to many common APIs in the .NET
Core libraries. For example, IsNullOrEmpty  has been updated, and the compiler correctly
interprets that method as a null check. For more information about the attributes that
apply to null-st ate static analysis, see the article on Nullable attributes .
There are two ways to control the nullable context. At the project level, you can add the
<Nullable>enable</Nullable> project setting. In a single C# source file, you can add the            return $"{shortDescription} \n{detailedDescription} "; 
        }  
    } 
    public string FullDescription () 
    { 
        if (detailedDescription == null) 
        {  
            return shortDescription;  
        }  
        else if (detailedDescription.Length > 0) // OK, detailedDescription  
can't be null.  
        {  
            return $"{shortDescription} \n{detailedDescription} "; 
        }  
        return shortDescription;  
    } 
} 
string shortDescription = default; // Warning! non-nullable set to null;  
var product = new ProductDescription(shortDescription); // Warning! static  
analysis knows shortDescription maybe null.  
string description = "widget" ; 
var item = new ProductDescription(description);  
item.SetDescriptions(description, "These widgets will do everything." ); 
Setting  the nulla ble context#nullable enable pragma to enable the nullable context. See the article on setting a
nullable strategy . Prior to .NET 6, new projects use the default,
<Nullable>disable</Nullable>. Beginning with .NET 6, new projects include the
<Nullable>enable</Nullable> element in the project file.
For more information, see the following proposals for the C# language specification :
Nullable reference types
Draft nullable reference types specification
C# reference
Nullable value typesC# language specification
See alsoCollections
Article •09/01/2023
The .NET runtime provides many collection types that store and manage groups of
related objects. Some of the collection types, such as System.Array , System.Span<T> ,
and System.Memory<T>  are recognized in the C# language. In addition, interfaces like
System.Collections.Generic.IEnumerable<T>  are recognized in the language for
enumerating the elements of a collection.
Collections provide a flexible way to work with groups of objects. Y ou can classify
different collections by these characteristics:
Element access : Every collection can be enumerated to access each element in
order. Some collections access elements by index , the element's position in an
ordered collection. The most common example is
System.Collections.Generic.List<T> . Other collections access elements by key,
where a value is associated with a single key. The most common example is
System.Collections.Generic.Dictionary<TK ey,TValue> . You choose between these
collection types based on how your app accesses elements.
Performance pr ofile: Every collection has different performance profiles for actions
like adding an element, finding an element, or removing an element. Y ou can pick
a collection type based on the operations used most in your app.
Grow and shrink dynamically : Most collections supporting adding or removing
elements dynamically. Notably, Array , System.Span<T> , and System.Memory<T>
don't.
In addition to those characteristics, the runtime provides specialized collections that
prevent adding or removing elements or modifying the elements of the collection.
Other specialized collections provide safety for concurrent access in multi-threaded
apps.
You can find all the collection types in the .NET API reference . For more information, see
Commonly Used Collection T ypes and Selecting a Collection Class .
Arrays  are represented by System.Array  and have syntax support in the C# language.
This syntax provides more concise declarations for array variables.７ Note
For the examples in this article, you might need to add using dir ectiv es for the
System.Collections.Generic and System.Linq namespaces.System.Span<T>  is a ref struct  type that provides a snapshot over a sequence of
elements without copying those elements. The compiler enforces safety rules to ensure
the Span can't be accessed after the sequence it references is no longer in scope. It's
used in many .NET APIs to improve performance. Memory<T>  provides similar behavior
when you can't use a ref struct type.
Beginning with C# 12, all of the collection types can be initialized using a Collection
expression .
An index able c ollection  is one where you can access each element using its index. Its
index  is the number of elements before it in the sequence. Therefore, the element
reference by index 0 is the first element, index 1 is the second, and so on. These
examples use the List<T>  class. It's the most common indexable collection.
The following example creates and initializes a list of strings, removes an element, and
adds an element to the end of the list. After each modification, it iterates through the
strings by using a foreach  statement or a for loop:
C#Indexable collections
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook" , "coho", "pink", "sockeye"  };
// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
// Remove an element from the list by specifying
// the object.
salmons.Remove( "coho");
// Iterate using the index:
for (var index = 0; index < salmons.Count; index++)
{
    Console.Write(salmons[index] + " ");
}
// Output: chinook pink sockeye
// Add the removed element
salmons.Add( "coho");
// Iterate through the list.The following example removes elements from a list by index. Instead of a foreach
statement, it uses a for statement that iterates in descending order. The RemoveAt
method causes elements after a removed element to have a lower index value.
C#
For the type of elements in the List<T> , you can also define your own class. In the
following example, the Galaxy class that is used by the List<T>  is defined in the code.
C#foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook pink sockeye coho
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
// Remove odd numbers.
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        // Remove the element by specifying
        // the zero-based index in the list.
        numbers.RemoveAt(index);
    }
}
// Iterate through the list.
// A lambda expression is placed in the ForEach method
// of the List(T) object.
numbers.ForEach(
    number => Console.Write(number + " "));
// Output: 0 2 4 6 8
private static void IterateThroughList ()
{
    var theGalaxies = new List<Galaxy>
    {
        new (){ Name= "Tadpole" , MegaLightYears= 400},
        new (){ Name= "Pinwheel" , MegaLightYears= 25},
        new (){ Name= "Milky Way" , MegaLightYears= 0},
        new (){ Name= "Andromeda" , MegaLightYears= 3}
    };
    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);These examples use the Dictionary<TK ey,TValue>  class. It's the most common dictionary
collection. A dictionary collection enables you to access elements in the collection by
using the key of each element. Each addition to the dictionary consists of a value and its
associated key.
The following example creates a Dictionary collection and iterates through the
dictionary by using a foreach statement.
C#    }
    // Output:
    //  Tadpole  400
    //  Pinwheel  25
    //  Milky Way  0
    //  Andromeda  3
}
public class Galaxy
{
    public string Name { get; set; }
    public int MegaLightYears { get; set; }
}
Key/value pair collections
private static void IterateThruDictionary ()
{
    Dictionary< string, Element> elements = BuildDictionary();
    foreach (KeyValuePair< string, Element> kvp in elements)
    {
        Element theElement = kvp.Value;
        Console.WriteLine( "key: " + kvp.Key);
        Console.WriteLine( "values: "  + theElement.Symbol + " " +
            theElement.Name + " " + theElement.AtomicNumber);
    }
}
public class Element
{
    public required string Symbol { get; init; }
    public required string Name { get; init; }
    public required int AtomicNumber { get; init; }
}
private static Dictionary< string, Element> BuildDictionary () =>
    new ()The following example uses the ContainsK ey method and the Item[]  property of
Dictionary to quickly find an item by key. The Item property enables you to access an
item in the elements collection by using the elements[symbol] in C#.
C#
The following example instead uses the TryGetV alue method to quickly find an item by
key.
C#
An iterator is used to perform a custom iteration over a collection. An iterator can be a
method or a get accessor. An iterator uses a yield return  statement to return each
element of the collection one at a time.
You call an iterator by using a foreach  statement. Each iteration of the foreach loop calls
the iterator. When a yield return statement is reached in the iterator, an expression is    {
        {"K",
            new (){ Symbol= "K", Name="Potassium" , AtomicNumber= 19}},
        {"Ca",
            new (){ Symbol= "Ca", Name="Calcium" , AtomicNumber= 20}},
        {"Sc",
            new (){ Symbol= "Sc", Name="Scandium" , AtomicNumber= 21}},
        {"Ti",
            new (){ Symbol= "Ti", Name="Titanium" , AtomicNumber= 22}}
    };
if (elements.ContainsKey(symbol) == false)
{
    Console.WriteLine(symbol + " not found" );
}
else
{
    Element theElement = elements[symbol];
    Console.WriteLine( "found: "  + theElement.Name);
}
if (elements.TryGetValue(symbol, out Element? theElement) == false)
    Console.WriteLine(symbol + " not found" );
else
    Console.WriteLine( "found: "  + theElement.Name);
Iteratorsreturned, and the current location in code is retained. Execution is restarted from that
location the next time that the iterator is called.
For more information, see Iterators (C#) .
The following example uses an iterator method. The iterator method has a yield return
statement that is inside a for loop. In the ListEvenNumbers method, each iteration of
the foreach statement body creates a call to the iterator method, which proceeds to the
next yield return statement.
C#
Language-integrated query (LINQ) can be used to access collections. LINQ queries
provide filtering, ordering, and grouping capabilities. For more information, see Getting
Started with LINQ in C# .
The following example runs a LINQ query against a generic List. The LINQ query
returns a different collection that contains the results.
C#private static void ListEvenNumbers ()
{
    foreach (int number in EvenSequence (5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    Console.WriteLine();
    // Output: 6 8 10 12 14 16 18
}
private static IEnumerable< int> EvenSequence (
    int firstNumber, int lastNumber )
{
    // Yield even numbers in the range.
    for (var number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
LINQ and collectionsprivate static void ShowLINQ ()
{
    List<Element> elements = BuildList();
    // LINQ Query.
    var subset = from theElement in elements
                 where theElement.AtomicNumber < 22
                 orderby theElement.Name
                 select theElement;
    foreach (Element theElement in subset)
    {
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
    }
    // Output:
    //  Calcium 20
    //  Potassium 19
    //  Scandium 21
}
private static List<Element> BuildList () => new()
    {
        { new(){ Symbol= "K", Name="Potassium" , AtomicNumber= 19}},
        { new(){ Symbol= "Ca", Name="Calcium" , AtomicNumber= 20}},
        { new(){ Symbol= "Sc", Name="Scandium" , AtomicNumber= 21}},
        { new(){ Symbol= "Ti", Name="Titanium" , AtomicNumber= 22}}
    };Arrays
Article •09/01/2023
You can store multiple variables of the same type in an array data structure. Y ou declare
an array by specifying the type of its elements. If you want the array to store elements of
any type, you can specify object as its type. In the unified type system of C#, all types,
predefined and user-defined, reference types and value types, inherit directly or
indirectly from Object .
C#
An array has the following properties:
An array can be single-dimensional , multidimensional , or jagged .
The number of dimensions are set when an array variable is declared. The length of
each dimension is established when the array instance is created. These values
can't be changed during the lifetime of the instance.
A jagged array is an array of arrays, and each member array has the default value
of null.
Arrays are zero indexed: an array with n elements is indexed from 0 to n-1.
Array elements can be of any type, including an array type.
Array types are reference types  derived from the abstract base type Array . All
arrays implement IList and IEnumerable . You can use the foreach  statement to
iterate through an array. Single-dimensional arrays also implement IList<T>  and
IEnumerable<T> .
The elements of an array can be initialized to known values when the array is created.
Beginning with C# 12, all of the collection types can be initialized using a Collection
expression . Elements that aren't initialized are set to the default value . The default value
is the 0-bit pattern. All reference types (including non-nullable  types), have the values
null. All value types have the 0-bit patterns. That means the Nullable<T>.HasV alue
property is false and the Nullable<T>.V alue property is undefined. In the .NET
implementation, the Value property throws an exception.
The following example creates single-dimensional, multidimensional, and jagged arrays:
C#type[] arrayName;
// Declare a single-dimensional array of 5 integers.
int[] array1 = new int[5];A single-dimensional arr ay is a sequence of like elements. Y ou access an element via its
index . The index  is its ordinal position in the sequence. The first element in the array is at
index 0. You create a single-dimensional array using the new operator specifying the
array element type and the number of elements. The following example declares and
initializes single-dimensional arrays:
C#// Declare and set array element values.
int[] array2 = { 1, 2, 3, 4, 5, 6 };
// Declare a two dimensional array.
int[,] multiDimensionalArray1 = new int[2, 3];
// Declare and set array element values.
int[,] multiDimensionalArray2 = { { 1, 2, 3 }, { 4, 5, 6 } };
// Declare a jagged array.
int[][] jaggedArray = new int[6][];
// Set the values of the first array in the jagged array structure.
jaggedArray[ 0] = new int[4] { 1, 2, 3, 4 };
Single-dimensional arrays
int[] array = new int[5];
string[] weekDays = { "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" };
Console.WriteLine(weekDays[ 0]);
Console.WriteLine(weekDays[ 1]);
Console.WriteLine(weekDays[ 2]);
Console.WriteLine(weekDays[ 3]);
Console.WriteLine(weekDays[ 4]);
Console.WriteLine(weekDays[ 5]);
Console.WriteLine(weekDays[ 6]);
/*Output:
Sun
Mon
Tue
Wed
Thu
Fri
Sat
*/The first declaration declares an uninitialized array of five integers, from array[0] to
array[4]. The elements of the array are initialized to the default value  of the element
type, 0 for integers. The second declaration declares an array of strings and initializes all
seven values of that array. A foreach statement  iterates the elements of the weekday
array and prints all the values. For single-dimensional arrays, the foreach statement
processes elements in increasing index order, starting with index 0 and ending with
index Length - 1.
You can pass an initialized single-dimensional array to a method. In the following
example, an array of strings is initialized and passed as an argument to a DisplayArray
method for strings. The method displays the elements of the array. Next, the
ChangeArray method reverses the array elements, and then the ChangeArrayElements
method modifies the first three elements of the array. After each method returns, the
DisplayArray method shows that passing an array by value doesn't prevent changes to
the array elements.
C#Pass single-dimensional arrays as arguments
class ArrayExample
{
    static void DisplayArray (string[] arr) => 
Console.WriteLine( string.Join(" ", arr));
    // Change the array by reversing its elements.
    static void ChangeArray (string[] arr) => Array.Reverse(arr);
    static void ChangeArrayElements (string[] arr)
    {
        // Change the value of the first three array elements.
        arr[0] = "Mon";
        arr[1] = "Wed";
        arr[2] = "Fri";
    }
    static void Main()
    {
        // Declare and initialize an array.
        string[] weekDays = { "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", 
"Sat" };
        // Display the array elements.
        DisplayArray(weekDays);
        Console.WriteLine();
        // Reverse the array.
        ChangeArray(weekDays);Arrays can have more than one dimension. For example, the following declarations
create four arrays: two have two dimensions, two have three dimensions. The first two
declarations declare the length of each dimension, but don't initialize the values of the
array. The second two declarations use an initializer to set the values of each element in
the multidimensional array.
C#        // Display the array again to verify that it stays reversed.
        Console.WriteLine( "Array weekDays after the call to ChangeArray:" );
        DisplayArray(weekDays);
        Console.WriteLine();
        // Assign new values to individual array elements.
        ChangeArrayElements(weekDays);
        // Display the array again to verify that it has changed.
        Console.WriteLine( "Array weekDays after the call to  
ChangeArrayElements:" );
        DisplayArray(weekDays);
    }
}
// The example displays the following output:
//         Sun Mon Tue Wed Thu Fri Sat
//
//        Array weekDays after the call to ChangeArray:
//        Sat Fri Thu Wed Tue Mon Sun
//
//        Array weekDays after the call to ChangeArrayElements:
//        Mon Wed Fri Wed Tue Mon Sun
Multid imensional arrays
int[,] array2DDeclaration = new int[4, 2];
int[,,] array3DDeclaration = new int[4, 2, 3];
// Two-dimensional array.
int[,] array2DInitialization =  { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } };
// Three-dimensional array.
int[,,] array3D = new int[,,] { { { 1, 2, 3 }, { 4,   5,  6 } },
                                { { 7, 8, 9 }, { 10, 11, 12 } } };
// Accessing array elements.
System.Console.WriteLine(array2DInitialization[ 0, 0]);
System.Console.WriteLine(array2DInitialization[ 0, 1]);
System.Console.WriteLine(array2DInitialization[ 1, 0]);
System.Console.WriteLine(array2DInitialization[ 1, 1]);
System.Console.WriteLine(array2DInitialization[ 3, 0]);
System.Console.WriteLine(array2DInitialization[ 3, 1]);For multi-dimensional arrays, elements are traversed such that the indices of the
rightmost dimension are incremented first, then the next left dimension, and so on, to
the leftmost index. The following example enumerates both a 2D and a 3D array:
C#
In a 2D array, you can think of the left index as the row and the right index as the
column .// Output:
// 1
// 2
// 3
// 4
// 7
// 8
System.Console.WriteLine(array3D[ 1, 0, 1]);
System.Console.WriteLine(array3D[ 1, 1, 2]);
// Output:
// 8
// 12
// Getting the total count of elements or the length of a given dimension.
var allLength = array3D.Length;
var total = 1;
for (int i = 0; i < array3D.Rank; i++)
{
    total *= array3D.GetLength(i);
}
System.Console.WriteLine( $"{allLength}  equals {total}");
// Output:
// 12 equals 12
int[,] numbers2D = { { 9, 99 }, { 3, 33 }, { 5, 55 } };
foreach (int i in numbers2D)
{
    System.Console.Write( $"{i} ");
}
// Output: 9 99 3 33 5 55
int[,,] array3D = new int[,,] { { { 1, 2, 3 }, { 4,   5,  6 } },
                        { { 7, 8, 9 }, { 10, 11, 12 } } };
foreach (int i in array3D)
{
    System.Console.Write( $"{i} ");
}
// Output: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12However, with multidimensional arrays, using a nested for loop gives you more control
over the order in which to process the array elements:
C#
You pass an initialized multidimensional array to a method in the same way that you
pass a one-dimensional array. The following code shows a partial declaration of a print
method that accepts a two-dimensional array as its argument. Y ou can initialize and
pass a new array in one step, as is shown in the following example. In the following
example, a two-dimensional array of integers is initialized and passed to the
Print2DArray method. The method displays the elements of the array.
C#int[,,] array3D = new int[,,] { { { 1, 2, 3 }, { 4,   5,  6 } },
                        { { 7, 8, 9 }, { 10, 11, 12 } } };
for (int i = 0; i < array3D.GetLength( 0); i++)
{
    for (int j = 0; j < array3D.GetLength( 1); j++)
    {
        for (int k = 0; k < array3D.GetLength( 2); k++)
        {
            System.Console.Write( $"{array3D[i, j, k]}  ");
        }
        System.Console.WriteLine();
    }
    System.Console.WriteLine();
}
// Output (including blank lines): 
// 1 2 3
// 4 5 6
// 
// 7 8 9
// 10 11 12
//
Pass multidimensional arrays as arguments
static void Print2DArray (int[,] arr)
{
    // Display the array elements.
    for (int i = 0; i < arr.GetLength( 0); i++)
    {
        for (int j = 0; j < arr.GetLength( 1); j++)
        {
            System.Console.WriteLine( "Element({0},{1})={2}" , i, j, arr[i,  
j]);
        }A jagged array is an array whose elements are arrays, possibly of different sizes. A
jagged array is sometimes called an "array of arrays." Its elements are reference types
and are initialized to null. The following examples show how to declare, initialize, and
access jagged arrays. The first example, jaggedArray, is declared in one statement. Each
contained array is created in subsequent statements. The second example, jaggedArray2
is declared and initialized in one statement. It's possible to mix jagged and
multidimensional arrays. The final example, jaggedArray3, is a declaration and
initialization of a single-dimensional jagged array that contains three two-dimensional
array elements of different sizes.
C#    }
}
static void ExampleUsage ()
{
    // Pass the array as an argument.
    Print2DArray( new int[,] { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } });
}
/* Output:
    Element(0,0)=1
    Element(0,1)=2
    Element(1,0)=3
    Element(1,1)=4
    Element(2,0)=5
    Element(2,1)=6
    Element(3,0)=7
    Element(3,1)=8
*/
Jagged arrays
int[][] jaggedArray = new int[3][];
jaggedArray[ 0] = new int[] { 1, 3, 5, 7, 9 };
jaggedArray[ 1] = new int[] { 0, 2, 4, 6 };
jaggedArray[ 2] = new int[] { 11, 22 };
int[][] jaggedArray2 = 
{
    new int[] { 1, 3, 5, 7, 9 },
    new int[] { 0, 2, 4, 6 },
    new int[] { 11, 22 }
};
// Assign 77 to the second element ([1]) of the first array ([0]):
jaggedArray2[ 0][1] = 77;A jagged array's elements must be initialized before you can use them. Each of the
elements is itself an array. It's also possible to use initializers to fill the array elements
with values. When you use initializers, you don't need the array size.
This example builds an array whose elements are themselves arrays. Each one of the
array elements has a different size.
C#// Assign 88 to the second element ([1]) of the third array ([2]):
jaggedArray2[ 2][1] = 88;
int[][,] jaggedArray3 = new int[3][,]
{
    new int[,] { {1,3}, {5,7} },
    new int[,] { {0,2}, {4,6}, {8,10} },
    new int[,] { {11,22}, {99,88}, {0,9} }
};
Console.Write( "{0}", jaggedArray3[ 0][1, 0]);
Console.WriteLine(jaggedArray3.Length);
// Declare the array of two elements.
int[][] arr = new int[2][];
// Initialize the elements.
arr[0] = new int[5] { 1, 3, 5, 7, 9 };
arr[1] = new int[4] { 2, 4, 6, 8 };
// Display the array elements.
for (int i = 0; i < arr.Length; i++)
{
    System.Console.Write( "Element({0}): " , i);
    for (int j = 0; j < arr[i].Length; j++)
    {
        System.Console.Write( "{0}{1}" , arr[i][j], j == (arr[i].Length - 1) ? 
"" : " ");
    }
    System.Console.WriteLine();
}
/* Output:
    Element(0): 1 3 5 7 9
    Element(1): 2 4 6 8
*/
Implicitly typed arraysYou can create an implicitly typed array in which the type of the array instance is inferred
from the elements specified in the array initializer. The rules for any implicitly typed
variable also apply to implicitly typed arrays. For more information, see Implicitly T yped
Local V ariables .
The following examples show how to create an implicitly typed array:
C#
var a = new[] { 1, 10, 100, 1000 }; // int[]
// Accessing array
Console.WriteLine( "First element: "  + a[0]);
Console.WriteLine( "Second element: "  + a[1]);
Console.WriteLine( "Third element: "  + a[2]);
Console.WriteLine( "Fourth element: "  + a[3]);
/* Outputs
First element: 1
Second element: 10
Third element: 100
Fourth element: 1000
*/
var b = new[] { "hello", null, "world" }; // string[]
// Accessing elements of an array using 'string.Join' method
Console.WriteLine( string.Join(" ", b));
/* Output
hello  world
*/
// single-dimension jagged array
var c = new[]
{
                                    new[]{1,2,3,4},
                                    new[]{5,6,7,8}
            };
// Looping through the outer array
for (int k = 0; k < c.Length; k++)
{
    // Looping through each inner array
    for (int j = 0; j < c[k].Length; j++)
    {
        // Accessing each element and printing it to the console
        Console.WriteLine( $"Element at c[ {k}][{j}] is: {c[k][j]} ");
    }
}
/* Outputs
Element at c[0][0] is: 1
Element at c[0][1] is: 2
Element at c[0][2] is: 3
Element at c[0][3] is: 4
Element at c[1][0] is: 5In the previous example, notice that with implicitly typed arrays, no square brackets are
used on the left side of the initialization statement. Also, jagged arrays are initialized by
using new [] just like single-dimensional arrays.
When you create an anonymous type that contains an array, the array must be implicitly
typed in the type's object initializer. In the following example, contacts is an implicitly
typed array of anonymous types, each of which contains an array named PhoneNumbers.
The var keyword isn't used inside the object initializers.
C#Element at c[1][1] is: 6
Element at c[1][2] is: 7
Element at c[1][3] is: 8
*/
// jagged array of strings
var d = new[]
{
                new[]{"Luca", "Mads", "Luke", "Dinesh" },
                new[]{"Karen", "Suma", "Frances" }
            };
// Looping through the outer array
int i = 0;
foreach (var subArray in d)
{
    // Looping through each inner array
    int j = 0;
    foreach (var element in subArray)
    {
        // Accessing each element and printing it to the console
        Console.WriteLine( $"Element at d[ {i}][{j}] is: {element} ");
        j++;
    }
    i++;
}
/* Outputs
Element at d[0][0] is: Luca
Element at d[0][1] is: Mads
Element at d[0][2] is: Luke
Element at d[0][3] is: Dinesh
Element at d[1][0] is: Karen
Element at d[1][1] is: Suma
Element at d[1][2] is: Frances
*/
var contacts = new[]
{
        new {
            Name = " Eugene Zabokritski" ,            PhoneNumbers = new[] { "206-555-0108" , "425-555-0001"  }
        },
        new {
            Name = " Hanying Feng" ,
            PhoneNumbers = new[] { "650-555-0199"  }
        }
    };void (C# reference)
Article •09/15/2021
You use void as the return type of a method  (or a local function ) to specify that the
method doesn't return a value.
C#
You can also use void as a referent type to declare a pointer to an unknown type. For
more information, see Pointer types .
You cannot use void as the type of a variable.
C# reference
System.V oidpublic static void Display(IEnumerable< int> numbers ) 
{ 
    if (numbers is null) 
    { 
        return; 
    } 
    Console.WriteLine( string.Join(" ", numbers));  
} 
See alsoBuilt-in types (C# reference)
Article •06/18/2022
The following table lists the C# built-in value  types:
C# type k eyword .NET type
bool System.Boolean
byte System.Byte
sbyte System.SByte
char System.Char
decimal System.Decimal
double System.Double
float System.Single
int System.Int32
uint System.UInt32
nint System.IntPtr
nuint System.UIntPtr
long System.Int64
ulong System.UInt64
short System.Int16
ushort System.UInt16
The following table lists the C# built-in reference  types:
C# type k eyword .NET type
object System.Object
string System.S tring
dynamic System.Object
In the preceding tables, each C# type keyword from the left column (except dynamic ) is
an alias for the corresponding .NET type. They are interchangeable. For example, thefollowing declarations declare variables of the same type:
C#
The void keyword represents the absence of a type. Y ou use it as the return type of a
method that doesn't return a value.
Use language keywords instead of framework type names (style rule IDE0049)
C# reference
Default values of C# typesint a = 123; 
System.Int32 b = 123; 
See alsoUnmanaged types (C# reference)
Article •04/12/2023
A type is an unmanaged type  if it's any of the following types:
sbyte, byte, short, ushort, int, uint, long, ulong, nint, nuint, char, float,
double, decimal, or bool
Any enum  type
Any pointer  type
Any user-defined struct  type that contains fields of unmanaged types only.
You can use the unmanaged  constraint  to specify that a type parameter is a non-pointer,
non-nullable unmanaged type.
A constr ucted struct type that contains fields of unmanaged types only is also
unmanaged, as the following example shows:
C#
A generic struct may be the source of both unmanaged and managed constructed
types. The preceding example defines a generic struct Coords<T> and presents theusing System;  
public struct Coords<T>
{ 
    public T X; 
    public T Y; 
} 
public class UnmanagedTypes  
{ 
    public static void Main() 
    { 
        DisplaySize<Coords< int>>(); 
        DisplaySize<Coords< double>>(); 
    } 
    private unsafe static void DisplaySize<T>() where T : unmanaged  
    { 
        Console.WriteLine( $"{typeof(T)} is unmanaged and its size is  
{sizeof(T)} bytes"); 
    } 
} 
// Output:  
// Coords`1[System.Int32] is unmanaged and its size is 8 bytes  
// Coords`1[System.Double] is unmanaged and its size is 16 bytes  examples of unmanaged constructed types. The example of a managed type is
Coords<object>. It's managed because it has the fields of the object type, which is
managed. If you want all constructed types to be unmanaged types, use the unmanaged
constraint in the definition of a generic struct:
C#
For more information, see the Pointer types  section of the C# language specification .
C# reference
Pointer types
Memory and span-related types
sizeof operator
stackallocpublic struct Coords<T> where T : unmanaged  
{ 
    public T X; 
    public T Y; 
} 
C# language specification
See alsoDefault values of C# types (C#
reference)
Article •02/21/2023
The following table shows the default values of C# types:
Type Default v alue
Any reference
typenull
Any built-in
integral numeric
type0 (zero)
Any built-in
floating-point
numeric type0 (zero)
bool false
char '\0' (U+0000)
enum The value produced by the expression (E)0, where E is the enum identifier.
struct The value produced by setting all value-type fields to their default values and
all reference-type fields to null.
Any nullable
value typeAn instance for which the HasV alue property is false and the Value property
is undefined. That default value is also known as the null value of a nullable
value type.
Use the default  operator  to produce the default value of a type, as the following
example shows:
C#
You can use the default  literal  to initialize a variable with the default value of its type:
C#Default value expressions
int a = default(int); For a value type, the implicit  parameterless constructor also produces the default value
of the type, as the following example shows:
C#
At run time, if the System.T ype instance represents a value type, you can use the
Activator.CreateInstance(T ype) method to invoke the parameterless constructor to
obtain the default value of the type.
For more information, see the following sections of the C# language specification :
Default values
Default constructors
C# 10 - P arameterless struct constructors
C# 11 - Auto default structs
C# reference
Constructorsint a = default; 
Parameterless constructor of a value type
var n = new System.Numerics.Complex();  
Console.WriteLine(n);  // output: (0, 0)  
７ Note
In C# 10 and later, a structur e type  (which is a value type) may have an explicit
paramet erless construct or that may produce a non-default value of the type. Thus,
we recommend using the default operator or the default literal to produce the
default value of a type.
C# language specification
See alsoC# Keywords
Article •04/22/2023
Keywords are predefined, reserved identifiers that have special meanings to the
compiler. They can't be used as identifiers in your program unless they include @ as a
prefix. For example, @if is a valid identifier, but if isn't because if is a keyword.
The first table in this article lists keywords that are reserved identifiers in any part of a
C# program. The second table in this article lists the contextual keywords in C#.
Contextual keywords have special meaning only in a limited program context and can
be used as identifiers outside that context. Generally, as new keywords are added to the
C# language, they're added as contextual keywords in order to avoid breaking programs
written in earlier versions.
abstract
as
base
bool
break
byte
case
catch
char
checked
class
const
continue
decimal
default
delegate
do
double
else
enum
event
explicit
extern
false
finallyfixed
float
for
foreach
goto
if
implicit
in
int
interface
internal
is
lock
long
namespace
new
null
object
operator
out
override
params
private
protected
public
readonly
ref
return
sbyte
sealed
short
sizeof
stackalloc
static
string
struct
switch
this
throwtrue
try
typeof
uint
ulong
unchecked
unsafe
ushort
using
virtual
void
volatile
while
A contextual keyword is used to provide a specific meaning in the code, but it isn't a
reserved word in C#. Some contextual keywords, such as partial and where, have
special meanings in two or more contexts.
add
and
alias
ascending
args
async
await
by
descending
dynamic
equals
file
from
get
global
group
init
into
joinContextual keywordslet
managed  (function pointer calling convention)
nameof
nint
not
notnull
nuint
on
or
orderby
partial  (type)
partial  (method)
record
remove
required
scoped
select
set
unmanaged  (function pointer calling convention)
unmanaged  (generic type constraint)
value
var
when  (filter condition)
where  (generic type constraint)
where  (query clause)
with
yield
C# referenceSee also
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review.NET feedb ack
The .NET documentation is open
source. Provide feedback here.
 Open a documentation issueissues and pull requests. For
more information, see our
contributor guide . Provide product feedbackAcces s Modifiers (C# Reference)
Article •09/27/2022
Access modifiers are keywords used to specify the declared accessibility of a member or
a type. This section introduces the five access modifiers:
public
protected
internal
private
file
The following seven accessibility levels can be specified using the access modifiers:
public : Access isn't restricted.
protected : Access is limited to the containing class or types derived from the
containing class.
internal : Access is limited to the current assembly.
protected internal : Access is limited to the current assembly or types derived from
the containing class.
private : Access is limited to the containing type.
private protected : Access is limited to the containing class or types derived from
the containing class within the current assembly.
file: The declared type is only visible in the current source file. File scoped types are
generally used for source generators.
This section also introduces the following concepts:
Accessibility Levels : Using the four access modifiers to declare six levels of
accessibility.
Accessibility Domain : Specifies where, in the program sections, a member can be
referenced.
Restrictions on Using Accessibility Levels : A summary of the restrictions on using
declared accessibility levels.
Add accessibility modifiers (style rule IDE0040)
C# Reference
C# Programming Guide
C# KeywordsSee alsoAccess Modifiers
Access K eywords
ModifiersAcces sibility Levels (C# Reference)
Article •08/16/2023
Use the access modifiers, public, protected, internal, or private, to specify one of the
following declared accessibility levels for members.
Declar ed
accessibilityMeaning
public Access is not restricted.
protected Access is limited to the containing class or types derived from the
containing class.
internal Access is limited to the current assembly.
protected internal Access is limited to the current assembly or types derived from the
containing class.
private Access is limited to the containing type.
private protected Access is limited to the containing class or types derived from the
containing class within the current assembly.
Only one access modifier is allowed for a member or type, except when you use the
protected internal or private protected combinations.
Access modifiers are not allowed on namespaces. Namespaces have no access
restrictions.
Depending on the context in which a member declaration occurs, only certain declared
accessibilities are permitted. If no access modifier is specified in a member declaration, a
default accessibility is used.
Top-level types, which are not nested in other types, can only have internal or public
accessibility. The default accessibility for these types is internal.
Nested types, which are members of other types, can have declared accessibilities as
indicated in the following table.
Member s ofDefault member accessibility Allow ed declar ed accessibility o f the member
enum public None
class private publicMember s ofDefault member accessibility Allow ed declar ed accessibility o f the member
protected
internal
private
protected internal
private protected
interfacepublic public
protected
internal
private*
protected internal
private protected
struct private public
internal
private
* An interface member with private accessibility must have a default implementation.
The accessibility of a nested type depends on its accessibility domain , which is
determined by both the declared accessibility of the member and the accessibility
domain of the immediately containing type. However, the accessibility domain of a
nested type cannot exceed that of the containing type.７ Note
If a class or struct is modified with the record keyword modifier, then the same
access modifiers are allowed.
Also, with the record modifier the default member accessibility is still private both
for class and the struct.
C# Language SpecificationFor more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Domain
Restrictions on Using Accessibility Levels
Access Modifiers
public
private
protected
internalSee alsoAcces sibility Domain (C# Reference)
Article •09/15/2021
The accessibility domain of a member specifies in which program sections a member
can be referenced. If the member is nested within another type, its accessibility domain
is determined by both the accessibility level  of the member and the accessibility domain
of the immediately containing type.
The accessibility domain of a top-level type is at least the program text of the project
that it is declared in. That is, the domain includes all of the source files of this project.
The accessibility domain of a nested type is at least the program text of the type in
which it is declared. That is, the domain is the type body, which includes all nested types.
The accessibility domain of a nested type never exceeds that of the containing type.
These concepts are demonstrated in the following example.
This example contains a top-level type, T1, and two nested classes, M1 and M2. The
classes contain fields that have different declared accessibilities. In the Main method, a
comment follows each statement to indicate the accessibility domain of each member.
Notice that the statements that try to reference the inaccessible members are
commented out. If you want to see the compiler errors caused by referencing an
inaccessible member, remove the comments one at a time.
C#Example
public class T1 
{ 
    public static int publicInt;  
    internal  static int internalInt;  
    private static int privateInt = 0; 
    static T1() 
    { 
        // T1 can access public or internal members  
        // in a public or private (or internal) nested class.  
        M1.publicInt = 1; 
        M1.internalInt = 2; 
        M2.publicInt = 3; 
        M2.internalInt = 4; 
        // Cannot access the private member privateInt  
        // in either class:  
        // M1.privateInt = 2; //CS0122  
    }     public class M1 
    { 
        public static int publicInt;  
        internal  static int internalInt;  
        private static int privateInt = 0; 
    } 
    private class M2 
    { 
        public static int publicInt = 0; 
        internal  static int internalInt = 0; 
        private static int privateInt = 0; 
    } 
} 
class MainClass  
{ 
    static void Main() 
    { 
        // Access is unlimited.  
        T1.publicInt = 1; 
        // Accessible only in current assembly.  
        T1.internalInt = 2; 
        // Error CS0122: inaccessible outside T1.  
        // T1.privateInt = 3;  
        // Access is unlimited.  
        T1.M1.publicInt = 1; 
        // Accessible only in current assembly.  
        T1.M1.internalInt = 2; 
        // Error CS0122: inaccessible outside M1.  
        //    T1.M1.privateInt = 3;  
        // Error CS0122: inaccessible outside T1.  
        //    T1.M2.publicInt = 1;  
        // Error CS0122: inaccessible outside T1.  
        //    T1.M2.internalInt = 2;  
        // Error CS0122: inaccessible outside M2.  
        //    T1.M2.privateInt = 3;  
        // Keep the console open in debug mode.  
        System.Console.WriteLine( "Press any key to exit." ); 
        System.Console.ReadKey();
    } 
} For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Restrictions on Using Accessibility Levels
Access Modifiers
public
private
protected
internalC# Language Specification
See alsoRestrictions on using accessibility levels
(C# Reference)
Article •09/15/2021
When you specify a type in a declaration, check whether the accessibility level of the
type is dependent on the accessibility level of a member or of another type. For
example, the direct base class must be at least as accessible as the derived class. The
following declarations cause a compiler error because the base class BaseClass is less
accessible than MyClass:
C#
The following table summarizes the restrictions on declared accessibility levels.
Cont ext Remarks
Classes The direct base class of a class type must be at least as accessible as the class type
itself.
Interfaces The explicit base interfaces of an interface type must be at least as accessible as
the interface type itself.
Delegates The return type and parameter types of a delegate type must be at least as
accessible as the delegate type itself.
Constants The type of a constant must be at least as accessible as the constant itself.
Fields The type of a field must be at least as accessible as the field itself.
Methods The return type and parameter types of a method must be at least as accessible as
the method itself.
Properties The type of a property must be at least as accessible as the property itself.
Events The type of an event must be at least as accessible as the event itself.
Indexers The type and parameter types of an indexer must be at least as accessible as the
indexer itself.
Operators The return type and parameter types of an operator must be at least as accessible
as the operator itself.class BaseClass  {...} 
public class MyClass: BaseClass  {...} // Error  Cont ext Remarks
Constructors The parameter types of a constructor must be at least as accessible as the
constructor itself.
The following example contains erroneous declarations of different types. The comment
following each declaration indicates the expected compiler error.
C#Example
// Restrictions on Using Accessibility Levels  
// CS0052 expected as well as CS0053, CS0056, and CS0057  
// To make the program work, change access level of both class B  
// and MyPrivateMethod() to public.  
using System;  
// A delegate:  
delegate  int MyDelegate (); 
class B 
{ 
    // A private method:  
    static int MyPrivateMethod () 
    { 
        return 0; 
    } 
} 
public class A 
{ 
    // Error: The type B is less accessible than the field A.myField.  
    public B myField = new B(); 
    // Error: The type B is less accessible  
    // than the constant A.myConst.  
    public readonly  B myConst = new B(); 
    public B MyMethod () 
    { 
        // Error: The type B is less accessible  
        // than the method A.MyMethod.  
        return new B();
    } 
    // Error: The type B is less accessible than the property A.MyProp  
    public B MyProp  
    { 
        set For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Domain
Accessibility Levels
Access Modifiers
public
private
protected
internal        {  
        }  
    } 
    MyDelegate d = new MyDelegate(B.MyPrivateMethod);  
    // Even when B is declared public, you still get the error:  
    // "The parameter B.MyPrivateMethod is not accessible due to  
    // protection level."  
    public static B operator  +(A m1, B m2)  
    { 
        // Error: The type B is less accessible  
        // than the operator A.operator +(A,B)  
        return new B();
    } 
    static void Main() 
    { 
        Console.Write( "Compiled successfully" ); 
    } 
} 
C# language specification
See alsointernal (C# Reference)
Article •01/25/2022
The internal keyword is an access modifier  for types and type members.
This page covers internal access. The internal keyword is also part of the
protected internal  access modifier.
Internal types or members are accessible only within files in the same assembly, as in
this example:
C#
For a comparison of internal with the other access modifiers, see Accessibility Levels
and Access Modifiers .
For more information about assemblies, see Assemblies in .NET .
A common use of internal access is in component-based development because it
enables a group of components to cooperate in a private manner without being
exposed to the rest of the application code. For example, a framework for building
graphical user interfaces could provide Control and Form classes that cooperate by
using members with internal access. Since these members are internal, they are not
exposed to code that is using the framework.
It is an error to reference a type or a member with internal access outside the assembly
within which it was defined.
This example contains two files, Assembly1.cs and Assembly1_a.cs. The first file contains
an internal base class, BaseClass. In the second file, an attempt to instantiate BaseClass
will produce an error.
C#public class BaseClass  
{   
    // Only accessible within the same assembly.  
    internal  static int x = 0; 
}   
Example 1C#
In this example, use the same files you used in example 1, and change the accessibility
level of BaseClass to public. Also change the accessibility level of the member intM to
internal. In this case, you can instantiate the class, but you cannot access the internal
member.
C#
C#// Assembly1.cs   
// Compile with: /target:library   
internal  class BaseClass  
{   
   public static int intM = 0;   
}   
// Assembly1_a.cs   
// Compile with: /reference:Assembly1.dll   
class TestAccess  
{   
   static void Main() 
   {   
      var myBase = new BaseClass();   // CS0122   
   }   
}   
Example 2
// Assembly2.cs   
// Compile with: /target:library   
public class BaseClass  
{   
   internal  static int intM = 0;   
}   
// Assembly2_a.cs   
// Compile with: /reference:Assembly2.dll   
public class TestAccess
{   
   static void Main() 
   {   
      var myBase = new BaseClass();   // Ok.   
      BaseClass.intM = 444;    // CS0117   
   }   
}   For more information, see Declared accessibility  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
public
private
protectedC# Language Specification
See alsoprivate (C# Reference)
Article •10/27/2022
The private keyword is a member access modifier.
This page covers private access. The private keyword is also part of the private
protected  access modifier.
Private access is the least permissive access level. Private members are accessible only
within the body of the class or the struct in which they are declared, as in this example:
C#
Nested types in the same body can also access those private members.
It is a compile-time error to reference a private member outside the class or the struct in
which it is declared.
For a comparison of private with the other access modifiers, see Accessibility Levels
and Access Modifiers .
In this example, the Employee class contains two private data members, _name and
_salary. As private members, they cannot be accessed except by member methods.
Public methods named GetName and Salary are added to allow controlled access to the
private members. The _name member is accessed by way of a public method, and the
_salary member is accessed by way of a public read-only property. For more
information, see Properties .
C#class Employee  
{ 
    private int _i; 
    double _d;   // private access by default  
} 
Example
class Employee2  
{ 
    private readonly  string _name = "FirstName, LastName" ; 
    private readonly  double _salary = 100.0; For more information, see Declared accessibility  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
public
protected
internal    public string GetName() 
    { 
        return _name; 
    } 
    public double Salary 
    { 
        get { return _salary; }  
    } 
} 
class PrivateTest  
{ 
    static void Main() 
    { 
        var e = new Employee2();  
        // The data members are inaccessible (private), so  
        // they can't be accessed like this:  
        //    string n = e._name;
        //    double s = e._salary;  
        // '_name' is indirectly accessed via method:  
        string n = e.GetName();  
        // '_salary' is indirectly accessed via property  
        double s = e.Salary;  
    } 
} 
C# language specification
See alsoprotected (C# Reference)
Article •01/25/2022
The protected keyword is a member access modifier.
A protected member is accessible within its class and by derived class instances.
For a comparison of protected with the other access modifiers, see Accessibility Levels .
A protected member of a base class is accessible in a derived class only if the access
occurs through the derived class type. For example, consider the following code
segment:
C#７ Note
This page covers protected access. The protected keyword is also part of the
protected int ernal  and private protected access modifiers.
Example 1
class A 
{ 
    protected  int x = 123; 
} 
class B : A 
{ 
    static void Main() 
    { 
        var a = new A(); 
        var b = new B(); 
        // Error CS1540, because x can only be accessed by  
        // classes derived from A.  
        // a.x = 10;  
        // OK, because this class derives from A.  
        b.x = 10; 
    } 
} The statement a.x = 10 generates an error because it is made within the static method
Main, and not an instance of class B.
Struct members cannot be protected because the struct cannot be inherited.
In this example, the class DerivedPoint is derived from Point. Therefore, you can access
the protected members of the base class directly from the derived class.
C#
If you change the access levels of x and y to private , the compiler will issue the error
messages:
'Point.y' is inaccessible due to its protection level.
'Point.x' is inaccessible due to its protection level.
For more information, see Declared accessibility  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.Example 2
class Point 
{ 
    protected  int x; 
    protected  int y; 
} 
class DerivedPoint : Point 
{ 
    static void Main() 
    { 
        var dpoint = new DerivedPoint();  
        // Direct access to protected members.  
        dpoint.x = 10; 
        dpoint.y = 15; 
        Console.WriteLine( $"x = {dpoint.x} , y = {dpoint.y} "); 
    } 
} 
// Output: x = 10, y = 15  
C# language specification
See alsoC# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
public
private
internal
Security concerns for internal virtual keywordspublic (C# Reference)
Article •01/25/2022
The public keyword is an access modifier for types and type members. Public access is
the most permissive access level. There are no restrictions on accessing public members,
as in this example:
C#
See Access Modifiers  and Accessibility Levels  for more information.
In the following example, two classes are declared, PointTest and Program. The public
members x and y of PointTest are accessed directly from Program.
C#
If you change the public access level to private  or protected , you will get the error
message:class SampleClass  
{ 
    public int x; // No access restrictions.  
} 
Example
class PointTest  
{ 
    public int x; 
    public int y; 
} 
class Program 
{ 
    static void Main() 
    { 
        var p = new PointTest();  
        // Direct access to public members.  
        p.x = 10; 
        p.y = 15; 
        Console.WriteLine( $"x = {p.x}, y = {p.y}"); 
    } 
} 
// Output: x = 10, y = 15  'PointT est.y' is inaccessible due to its protection level.
For more information, see Declared accessibility  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
Access Modifiers
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
private
protected
internalC# language specification
See alsoprotected internal (C# Reference)
Article •09/15/2021
The protected internal keyword combination is a member access modifier. A protected
internal member is accessible from the current assembly or from types that are derived
from the containing class. For a comparison of protected internal with the other access
modifiers, see Accessibility Levels .
A protected internal member of a base class is accessible from any type within its
containing assembly. It is also accessible in a derived class located in another assembly
only if the access occurs through a variable of the derived class type. For example,
consider the following code segment:
C#
C#Example
// Assembly1.cs  
// Compile with: /target:library  
public class BaseClass  
{ 
   protected  internal  int myValue = 0; 
} 
class TestAccess  
{ 
    void Access() 
    { 
        var baseObject = new BaseClass();  
        baseObject.myValue = 5; 
    } 
} 
// Assembly2.cs  
// Compile with: /reference:Assembly1.dll  
class DerivedClass  : BaseClass  
{ 
    static void Main() 
    { 
        var baseObject = new BaseClass();  
        var derivedObject = new DerivedClass();  
        // Error CS1540, because myValue can only be accessed by  
        // classes derived from BaseClass.  This example contains two files, Assembly1.cs and Assembly2.cs. The first file contains a
public base class, BaseClass, and another class, TestAccess. BaseClass owns a
protected internal member, myValue, which is accessed by the TestAccess type. In the
second file, an attempt to access myValue through an instance of BaseClass will produce
an error, while an access to this member through an instance of a derived class,
DerivedClass will succeed.
Struct members cannot be protected internal because the struct cannot be inherited.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
public
private
internal
Security concerns for internal virtual keywords        // baseObject.myValue = 10;  
        // OK, because this class derives from BaseClass.  
        derivedObject.myValue = 10; 
    } 
} 
C# language specification
See alsoprivate protected (C# Reference)
Article •09/15/2021
The private protected keyword combination is a member access modifier. A private
protected member is accessible by types derived from the containing class, but only
within its containing assembly. For a comparison of private protected with the other
access modifiers, see Accessibility Levels .
A private protected member of a base class is accessible from derived types in its
containing assembly only if the static type of the variable is the derived class type. For
example, consider the following code segment:
C#
C#７ Note
The private protected access modifier is valid in C# version 7.2 and later.
Example
public class BaseClass  
{ 
    private protected  int myValue = 0; 
} 
public class DerivedClass1  : BaseClass  
{ 
    void Access() 
    { 
        var baseObject = new BaseClass();  
        // Error CS1540, because myValue can only be accessed by  
        // classes derived from BaseClass.  
        // baseObject.myValue = 5;  
        // OK, accessed through the current derived class instance  
        myValue = 5; 
    } 
} 
// Assembly2.cs  
// Compile with: /reference:Assembly1.dll  This example contains two files, Assembly1.cs and Assembly2.cs. The first file contains a
public base class, BaseClass, and a type derived from it, DerivedClass1. BaseClass owns
a private protected member, myValue, which DerivedClass1 tries to access in two ways.
The first attempt to access myValue through an instance of BaseClass will produce an
error. However, the attempt to use it as an inherited member in DerivedClass1 will
succeed.
In the second file, an attempt to access myValue as an inherited member of
DerivedClass2 will produce an error, as it is only accessible by derived types in
Assembly1.
If Assembly1.cs contains an InternalsVisibleT oAttribute  that names Assembly2, the
derived class DerivedClass2 will have access to private protected members declared in
BaseClass. InternalsVisibleTo makes private protected members visible to derived
classes in other assemblies.
Struct members cannot be private protected because the struct cannot be inherited.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
publicclass DerivedClass2  : BaseClass  
{ 
    void Access() 
    { 
        // Error CS0122, because myValue can only be  
        // accessed by types in Assembly1  
        // myValue = 10;  
    } 
} 
C# language specification
See alsoprivate
internal
Security concerns for internal virtual keywordsfile (C# Reference)
Article •11/18/2022
Beginning with C# 11, the file contextual keyword is a type modifier.
The file modifier restricts a top-level type's scope and visibility to the file in which it's
declared. The file modifier will generally be applied to types written by a source
generator. File-local types provide source generators with a convenient way to avoid
name collisions among generated types. The file modifier declares a file-local type, as
in this example:
C#
Any types nested within a file-local type are also only visible within the file in which it's
declared. Other types in an assembly may use the same name as a file-local type.
Because the file-local type is visible only in the file where it's declared, these types don't
create a naming collision.
A file-local type can't be the return type or parameter type of any member that is more
visible than file scope. A file-local type can't be a field member of a type that has
greater visibility than file scope. However, a more visible type may implicitly
implement a file-local interface type. The type can also explicitly implement  a file-local
interface but explicit implementations can only be used within the file scope.
The following example shows a public type that uses a file-local type to provide a
worker method. In addition, the public type implements a file-local interface implicitly:
C#file class HiddenWidget  
{ 
    // implementation  
} 
Example
// In File1.cs:  
file interface  IWidget 
{ 
    int ProvideAnswer (); 
} 
file class HiddenWidget  In another source file, you can declare types that have the same names as the file-local
types. The file-local types aren't visible:
C#
For more information, see Declared accessibility  in the C# Language Specification , and
the C# 11 - File local types  feature specification.
C# Reference
C# Programming Guide
C# Keywords
Access Modifiers
Accessibility Levels
Modifiers
public
protected
internal{ 
    public int Work() => 42; 
} 
public class Widget : IWidget 
{ 
    public int ProvideAnswer () 
    { 
        var worker = new HiddenWidget();  
        return worker.Work();  
    } 
} 
// In File2.cs:  
// Doesn't conflict with HiddenWidget  
// declared in File1.cs  
public class HiddenWidget  
{ 
    public void RunTask() 
    { 
        // omitted  
    } 
} 
C# language specification
See alsoabstract (C# Reference)
Article •09/15/2021
The abstract modifier indicates that the thing being modified has a missing or
incomplete implementation. The abstract modifier can be used with classes, methods,
properties, indexers, and events. Use the abstract modifier in a class declaration to
indicate that a class is intended only to be a base class of other classes, not instantiated
on its own. Members marked as abstract must be implemented by non-abstract classes
that derive from the abstract class.
In this example, the class Square must provide an implementation of GetArea because it
derives from Shape:
C#
Abstract classes have the following features:
An abstract class cannot be instantiated.
An abstract class may contain abstract methods and accessors.Example 1
abstract  class Shape 
{ 
    public abstract  int GetArea(); 
} 
class Square : Shape 
{ 
    private int _side; 
    public Square(int n) => _side = n;  
    // GetArea method is required to avoid a compile-time error.  
    public override  int GetArea() => _side * _side;  
    static void Main() 
    { 
        var sq = new Square( 12); 
        Console.WriteLine( $"Area of the square = {sq.GetArea()} "); 
    } 
} 
// Output: Area of the square = 144  It is not possible to modify an abstract class with the sealed  modifier because the
two modifiers have opposite meanings. The sealed modifier prevents a class from
being inherited and the abstract modifier requires a class to be inherited.
A non-abstract class derived from an abstract class must include actual
implementations of all inherited abstract methods and accessors.
Use the abstract modifier in a method or property declaration to indicate that the
method or property does not contain implementation.
Abstract methods have the following features:
An abstract method is implicitly a virtual method.
Abstract method declarations are only permitted in abstract classes.
Because an abstract method declaration provides no actual implementation, there
is no method body; the method declaration simply ends with a semicolon and
there are no curly braces ({ }) following the signature. For example:
C#
The implementation is provided by a method override , which is a member of a
non-abstract class.
It is an error to use the static  or virtual  modifiers in an abstract method declaration.
Abstract properties behave like abstract methods, except for the differences in
declaration and invocation syntax.
It is an error to use the abstract modifier on a static property.
An abstract inherited property can be overridden in a derived class by including a
property declaration that uses the override  modifier.
For more information about abstract classes, see Abstract and Sealed Classes and Class
Members .
An abstract class must provide implementation for all interface members.
An abstract class that implements an interface might map the interface methods onto
abstract methods. For example:
C#public abstract  void MyMethod ();   In this example, the class DerivedClass is derived from an abstract class BaseClass. The
abstract class contains an abstract method, AbstractMethod, and two abstract properties,
X and Y.
C#interface  I 
{ 
    void M();
} 
abstract  class C : I 
{ 
    public abstract  void M(); 
} 
Example 2
// Abstract class  
abstract  class BaseClass  
{ 
    protected  int _x = 100; 
    protected  int _y = 150; 
    // Abstract method  
    public abstract  void AbstractMethod (); 
    // Abstract properties  
    public abstract  int X { get; } 
    public abstract  int Y { get; } 
} 
class DerivedClass  : BaseClass  
{ 
    public override  void AbstractMethod () 
    { 
        _x++;  
        _y++;  
    } 
    public override  int X   // overriding property  
    { 
        get 
        {  
            return _x + 10; 
        }  
    } 
    public override  int Y   // overriding property  
    { In the preceding example, if you attempt to instantiate the abstract class by using a
statement like this:
C#
You will get an error saying that the compiler cannot create an instance of the abstract
class 'BaseClass'.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
Modifiers
virtual
override
C# Keywords        get 
        {  
            return _y + 10; 
        }  
    } 
    static void Main() 
    { 
        var o = new DerivedClass();  
        o.AbstractMethod();  
        Console.WriteLine( $"x = {o.X}, y = {o.Y}"); 
    } 
} 
// Output: x = 111, y = 161  
BaseClass bc = new BaseClass();   // Error   
C# Language Specification
See alsoasync (C# Reference)
Article •03/22/2023
Use the async modifier to specify that a method, lambda expression , or anonymous
method  is asynchronous. If you use this modifier on a method or expression, it's referred
to as an async method . The following example defines an async method named
ExampleMethodAsync:
C#
If you're new to asynchronous programming or do not understand how an async
method uses the await  operator  to do potentially long-running work without blocking
the caller's thread, read the introduction in Asynchronous programming with async and
await . The following code is found inside an async method and calls the
HttpClient.GetS tringAsync  method:
C#
An async method runs synchronously until it reaches its first await expression, at which
point the method is suspended until the awaited task is complete. In the meantime,
control returns to the caller of the method, as the example in the next section shows.
If the method that the async keyword modifies doesn't contain an await expression or
statement, the method executes synchronously. A compiler warning alerts you to any
async methods that don't contain await statements, because that situation might
indicate an error. See Compiler W arning (level 1) CS4014 .
The async keyword is contextual in that it's a keyword only when it modifies a method,
a lambda expression, or an anonymous method. In all other contexts, it's interpreted as
an identifier.public async Task<int> ExampleMethodAsync ()
{
    //...
}
string contents = await httpClient.GetStringAsync(requestUrl);
ExampleThe following example shows the structure and flow of control between an async event
handler, StartButton_Click, and an async method, ExampleMethodAsync. The result from
the async method is the number of characters of a web page. The code is suitable for a
Windows Presentation Foundation (WPF) app or Windows S tore app that you create in
Visual S tudio; see the code comments for setting up the app.
You can run this code in Visual S tudio as a Windows Presentation Foundation (WPF) app
or a Windows S tore app. Y ou need a Button control named StartButton and a T extbox
control named ResultsTextBox. Remember to set the names and handler so that you
have something like this:
XAML
To run the code as a WPF app:
Paste this code into the MainWindow class in MainWindow.xaml.cs.
Add a reference to S ystem.Net.Http.
Add a using directive for S ystem.Net.Http.
To run the code as a Windows S tore app:
Paste this code into the MainPage class in MainP age.xaml.cs.
Add using directives for S ystem.Net.Http and S ystem.Threading.T asks.
C#<Button Content="Button"  HorizontalAlignment ="Left" Margin="88,77,0,0"  
VerticalAlignment ="Top" Width="75"
        Click="StartButton_Click"  Name="StartButton" />
<TextBox HorizontalAlignment ="Left" Height="137" Margin="88,140,0,0"  
TextWrapping ="Wrap"
         Text="&lt;Enter a URL&gt;"  VerticalAlignment ="Top" Width="310" 
Name="ResultsTextBox" />
private async void StartButton_Click (object sender, RoutedEventArgs e )
{
    // ExampleMethodAsync returns a Task<int>, which means that the method
    // eventually produces an int result. However, ExampleMethodAsync  
returns
    // the Task<int> value as soon as it reaches an await.
    ResultsTextBox.Text += "\n";
    try
    {
        int length = await ExampleMethodAsync();
        // Note that you could put "await ExampleMethodAsync()" in the next  
line where
        // "length" is, but due to when '+=' fetches the value of  An async method can have the following return types:
Task
Task<TR esult>
void. async void methods are generally discouraged for code other than event
handlers because callers cannot await those methods and must implement a
different mechanism to report successful completion or error conditions.
Any type that has an accessible GetAwaiter method. The
System.Threading.Tasks.ValueTask<TResult> type is one such implementation. It is
available by adding the NuGet package System.Threading.Tasks.Extensions.ResultsTextBox, you
        // would not see the global side effect of ExampleMethodAsync  
setting the text.
        ResultsTextBox.Text += String.Format( "Length: {0:N0}\n" , length);
    }
    catch (Exception)
    {
        // Process the exception if one occurs.
    }
}
public async Task<int> ExampleMethodAsync ()
{
    var httpClient = new HttpClient();
    int exampleInt = ( await 
httpClient.GetStringAsync( "http://msdn.microsoft.com" )).Length;
    ResultsTextBox.Text += "Preparing to finish ExampleMethodAsync.\n" ;
    // After the following return statement, any method that's awaiting
    // ExampleMethodAsync (in this case, StartButton_Click) can get the
    // integer result.
    return exampleInt;
}
// The example displays the following output:
// Preparing to finish ExampleMethodAsync.
// Length: 53292
） Impor tant
For more information about tasks and the code that executes while waiting for a
task, see Asynchr onous pr ogramming with async and await . For a full console
example that uses similar elements, see Process asynchr onous tasks as they
complet e (C#) .
Return TypesThe async method can't declare any in, ref or out parameters, nor can it have a reference
return value , but it can call methods that have such parameters.
You specify Task<TResult> as the return type of an async method if the return  statement
of the method specifies an operand of type TResult. You use Task if no meaningful
value is returned when the method is completed. That is, a call to the method returns a
Task, but when the Task is completed, any await expression that's awaiting the Task
evaluates to void.
You use the void return type primarily to define event handlers, which require that
return type. The caller of a void-returning async method can't await it and can't catch
exceptions that the method throws.
You return another type, typically a value type, that has a GetAwaiter method to
minimize memory allocations in performance-critical sections of code.
For more information and examples, see Async R eturn T ypes.
AsyncS tateMachineAttribute
await
Asynchronous programming with async and await
Process asynchronous tasks as they complete
.NET blog: How async/await really works in C#See also
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
 Provide product feedbackconst (C# Reference)
Article •05/10/2023
You use the const keyword to declare a constant field or a local constant. Constant
fields and locals aren't variables and may not be modified. Constants can be numbers,
Boolean values, strings, or a null reference. Don’t create a constant to represent
information that you expect to change at any time. For example, don’t use a constant
field to store the price of a service, a product version number, or the brand name of a
company. These values can change over time, and because compilers propagate
constants, other code compiled with your libraries will have to be recompiled to see the
changes. See also the readonly  keyword. For example:
C#
Beginning with C# 10, interpolated strings  may be constants, if all expressions used are
also constant strings. This feature can improve the code that builds constant strings:
C#
The type of a constant declaration specifies the type of the members that the
declaration introduces. The initializer of a local constant or a constant field must be a
constant expression that can be implicitly converted to the target type.
A constant expression is an expression that can be fully evaluated at compile time.
Therefore, the only possible values for constants of reference types are strings and a null
reference.
The constant declaration can declare multiple constants, such as:
C#const int X = 0; 
public const double GravitationalConstant = 6.673e-11 ; 
private const string ProductName = "Visual C#" ; 
const string Language = "C#"; 
const string Platform = ".NET"; 
const string Version = "10.0"; 
const string FullProductName = $"{Platform}  - Language: {Language}  Version:  
{Version} "; 
RemarksThe static modifier is not allowed in a constant declaration.
A constant can participate in a constant expression, as follows:
C#
C#public const double X = 1.0, Y = 2.0, Z = 3.0; 
public const int C1 = 5; 
public const int C2 = C1 + 100; 
７ Note
The readonly  keyword differs from the const keyword. A const field can only be
initialized at the declaration of the field. A readonly field can be initialized either at
the declaration or in a constructor. Therefore, readonly fields can have different
values depending on the constructor used. Also, although a const field is a
compile-time constant, the readonly field can be used for run-time constants, as in
this line: public static readonly uint l1 = (uint)DateTime.Now.Ticks;
Examples
public class ConstTest  
{ 
    class SampleClass  
    { 
        public int x; 
        public int y; 
        public const int C1 = 5; 
        public const int C2 = C1 + 5; 
        public SampleClass (int p1, int p2) 
        {  
            x = p1;  
            y = p2;  
        }  
    } 
    static void Main() 
    { 
        var mC = new SampleClass( 11, 22); 
        Console.WriteLine( $"x = {mC.x}, y = {mC.y}"); 
        Console.WriteLine( $"C1 = {SampleClass.C1} , C2 = {SampleClass.C2} "); The following example demonstrates how to declare a local constant:
C#
For more information, see the following sections of the C# language specification :
Constants
Constant expressions
C# reference
C# keywords
readonly    } 
} 
/* Output  
    x = 11, y = 22  
    C1 = 5, C2 = 10  
*/ 
public class SealedTest
{ 
    static void Main() 
    { 
        const int C = 707; 
        Console.WriteLine( $"My local constant = {C}"); 
    } 
} 
// Output: My local constant = 707  
C# language specification
See alsoevent (C# reference)
Article •05/03/2022
The event keyword is used to declare an event in a publisher class.
The following example shows how to declare and raise an event that uses EventHandler
as the underlying delegate type. For the complete code example that also shows how to
use the generic EventHandler<TEventArgs>  delegate type and how to subscribe to an
event and create an event handler method, see How to publish events that conform to
.NET Guidelines .
C#
Events are a special kind of multicast delegate that can only be invoked from within the
class (or derived classes) or struct where they are declared (the publisher class). If other
classes or structs subscribe to the event, their event handler methods will be called
when the publisher class raises the event. For more information and code examples, see
Events  and Delegates .Example
public class SampleEventArgs  
{ 
    public SampleEventArgs (string text) { Text = text; }  
    public string Text { get; } // readonly  
} 
public class Publisher  
{ 
    // Declare the delegate (if using non-generic pattern).  
    public delegate  void SampleEventHandler (object sender, SampleEventArgs  
e); 
    // Declare the event.  
    public event SampleEventHandler SampleEvent;  
    // Wrap the event in a protected virtual method  
    // to enable derived classes to raise the event.  
    protected  virtual void RaiseSampleEvent () 
    { 
        // Raise the event in a thread-safe manner using the ?. operator.  
        SampleEvent?.Invoke( this, new SampleEventArgs( "Hello")); 
    } 
} Events can be marked as public , private , protected , internal , protected internal , or
private protected . These access modifiers define how users of the class can access the
event. For more information, see Access Modifiers .
The following keywords apply to events.
KeywordDescr iption For mor e
infor mation
static Makes the event available to callers at any time, even if no
instance of the class exists.Static Classes
and S tatic Class
Members
virtual Allows derived classes to override the event behavior by using the
override  keyword.Inheritance
sealed Specifies that for derived classes it is no longer virtual.
abstract The compiler will not generate the add and remove event accessor
blocks and therefore derived classes must provide their own
implementation.
An event may be declared as a static event by using the static  keyword. This makes the
event available to callers at any time, even if no instance of the class exists. For more
information, see Static Classes and S tatic Class Members .
An event can be marked as a virtual event by using the virtual  keyword. This enables
derived classes to override the event behavior by using the override  keyword. For more
information, see Inheritance . An event overriding a virtual event can also be sealed ,
which specifies that for derived classes it is no longer virtual. Lastly, an event can be
declared abstract , which means that the compiler will not generate the add and remove
event accessor blocks. Therefore derived classes must provide their own
implementation.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.Keywords and events
C# language specification
See alsoC# Reference
C# Programming Guide
C# Keywords
add
remove
Modifiers
How to combine delegates (Multicast Delegates)extern (C# Reference)
Article •09/15/2021
The extern modifier is used to declare a method that is implemented externally. A
common use of the extern modifier is with the DllImport attribute when you are using
Interop services to call into unmanaged code. In this case, the method must also be
declared as static, as shown in the following example:
C#
The extern keyword can also define an external assembly alias, which makes it possible
to reference different versions of the same component from within a single assembly.
For more information, see extern alias .
It is an error to use the abstract  and extern modifiers together to modify the same
member. Using the extern modifier means that the method is implemented outside the
C# code, whereas using the abstract modifier means that the method implementation
is not provided in the class.
The extern keyword has more limited uses in C# than in C++. T o compare the C#
keyword with the C++ keyword, see Using extern to Specify Linkage in the C++
Language R eference.
In this example, the program receives a string from the user and displays it inside a
message box. The program uses the MessageBox method imported from the User32.dll
library.
C#[DllImport( "avifil32.dll" )] 
private static extern void AVIFileInit (); 
Example 1
//using System.Runtime.InteropServices;  
class ExternTest  
{ 
    [DllImport( "User32.dll" , CharSet=CharSet.Unicode) ] 
    public static extern int MessageBox (IntPtr h, string m, string c, int 
type); 
    static int Main() 
    { This example illustrates a C# program that calls into a C library (a native DLL).
1. Create the following C file and name it cmdll.c:
C
2. Open a Visual S tudio x64 (or x32) Native T ools Command Prompt window from the
Visual S tudio installation directory and compile the cmdll.c file by typing cl -LD
cmdll.c  at the command prompt.
3. In the same directory, create the following C# file and name it cm.cs:
C#
4. Open a Visual S tudio x64 (or x32) Native T ools Command Prompt window from the
Visual S tudio installation directory and compile the cm.cs file by typing:        string myString;  
        Console.Write( "Enter your message: " ); 
        myString = Console.ReadLine();  
        return MessageBox((IntPtr) 0, myString, "My Message Box" , 0); 
    } 
} 
Example 2
// cmdll.c  
// Compile with: -LD  
int __declspec(dllexport) SampleMethod( int i) 
{ 
  return i*10; 
} 
// cm.cs  
using System;  
using System.Runtime.InteropServices;  
public class MainClass  
{ 
    [DllImport( "Cmdll.dll" )] 
      public static extern int SampleMethod (int x); 
    static void Main() 
    { 
        Console.WriteLine( "SampleMethod() returns {0}." , 
SampleMethod( 5)); 
    } 
} csc cm.cs  (for the x64 command prompt) —or— csc -platform:x86 cm.cs  (for
the x32 command prompt)
This will create the executable file cm.exe.
5. Run cm.exe. The SampleMethod method passes the value 5 to the DLL file, which
returns the value multiplied by 10. The program produces the following output:
Output
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
System.Runtime.InteropServices.DllImportAttribute
C# Reference
C# Programming Guide
C# Keywords
ModifiersSampleMethod() returns 50.  
C# language specification
See alsoin (Generic Modifier) (C# Reference)
Article •02/25/2022
For generic type parameters, the in keyword specifies that the type parameter is
contravariant. Y ou can use the in keyword in generic interfaces and delegates.
Contravariance enables you to use a less derived type than that specified by the generic
parameter. This allows for implicit conversion of classes that implement contravariant
interfaces and implicit conversion of delegate types. Covariance and contravariance in
generic type parameters are supported for reference types, but they are not supported
for value types.
A type can be declared contravariant in a generic interface or delegate only if it defines
the type of a method's parameters and not of a method's return type. In, ref, and out
parameters must be invariant, meaning they are neither covariant nor contravariant.
An interface that has a contravariant type parameter allows its methods to accept
arguments of less derived types than those specified by the interface type parameter.
For example, in the IComparer<T>  interface, type T is contravariant, you can assign an
object of the IComparer<Person> type to an object of the IComparer<Employee> type
without using any special conversion methods if Employee inherits Person.
A contravariant delegate can be assigned another delegate of the same type, but with a
less derived generic type parameter.
For more information, see Covariance and Contravariance .
The following example shows how to declare, extend, and implement a contravariant
generic interface. It also shows how you can use implicit conversion for classes that
implement this interface.
C#Contravariant generic interface
// Contravariant interface.  
interface  IContravariant <in A> { } 
// Extending contravariant interface.  
interface  IExtContravariant <in A> : IContravariant <A> { } 
// Implementing contravariant interface.  
class Sample<A> : IContravariant <A> { } The following example shows how to declare, instantiate, and invoke a contravariant
generic delegate. It also shows how you can implicitly convert a delegate type.
C#class Program 
{ 
    static void Test() 
    { 
        IContravariant<Object> iobj = new Sample<Object>();  
        IContravariant<String> istr = new Sample<String>();  
        // You can assign iobj to istr because  
        // the IContravariant interface is contravariant.  
        istr = iobj;  
    } 
} 
Contravariant generic delegate
// Contravariant delegate.  
public delegate  void DContravariant< in A>(A argument);  
// Methods that match the delegate signature.  
public static void SampleControl (Control control ) 
{ } 
public static void SampleButton (Button button ) 
{ } 
public void Test() 
{ 
    // Instantiating the delegates with the methods.  
    DContravariant<Control> dControl = SampleControl;  
    DContravariant<Button> dButton = SampleButton;  
    // You can assign dControl to dButton  
    // because the DContravariant delegate is contravariant.  
    dButton = dControl;  
    // Invoke the delegate.  
    dButton( new Button());  
} 
C# language specificationFor more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
out
Covariance and Contravariance
ModifiersSee alsonew modifier (C# Reference)
Article •04/12/2023
When used as a declaration modifier, the new keyword explicitly hides a member that is
inherited from a base class. When you hide an inherited member, the derived version of
the member replaces the base class version. This assumes that the base class version of
the member is visible, as it would already be hidden if it were marked as private or, in
some cases, internal. Although you can hide public or protected members without
using the new modifier, you get a compiler warning. If you use new to explicitly hide a
member, it suppresses this warning.
You can also use the new keyword to create an instance of a type  or as a generic type
constraint .
To hide an inherited member, declare it in the derived class by using the same member
name, and modify it with the new keyword. For example:
C#
In this example, BaseC.Invoke is hidden by DerivedC.Invoke. The field x is not affected
because it is not hidden by a similar name.
Name hiding through inheritance takes one of the following forms:
Generally, a constant, field, property, or type that is introduced in a class or struct
hides all base class members that share its name. There are special cases. For
example, if you declare a new field with name N to have a type that is not
invocable, and a base type declares N to be a method, the new field does not hide
the base declaration in invocation syntax. For more information, see the Member
lookup  section of the C# language specification .
A method introduced in a class or struct hides properties, fields, and types that
share that name in the base class. It also hides all base class methods that have thepublic class BaseC 
{ 
    public int x; 
    public void Invoke() { } 
} 
public class DerivedC  : BaseC 
{ 
    new public void Invoke() { } 
} same signature.
An indexer introduced in a class or struct hides all base class indexers that have the
same signature.
It is an error to use both new and override  on the same member, because the two
modifiers have mutually exclusive meanings. The new modifier creates a new member
with the same name and causes the original member to become hidden. The override
modifier extends the implementation for an inherited member.
Using the new modifier in a declaration that does not hide an inherited member
generates a warning.
In this example, a base class, BaseC, and a derived class, DerivedC, use the same field
name x, which hides the value of the inherited field. The example demonstrates the use
of the new modifier. It also demonstrates how to access the hidden members of the
base class by using their fully qualified names.
C#Examples
public class BaseC 
{ 
    public static int x = 55; 
    public static int y = 22; 
} 
public class DerivedC  : BaseC 
{ 
    // Hide field 'x'.  
    new public static int x = 100; 
    static void Main() 
    { 
        // Display the new value of x:  
        Console.WriteLine(x);  
        // Display the hidden value of x:  
        Console.WriteLine(BaseC.x);  
        // Display the unhidden member y:  
        Console.WriteLine(y);  
    } 
} 
/* 
Output: 
100 In this example, a nested class hides a class that has the same name in the base class.
The example demonstrates how to use the new modifier to eliminate the warning
message and how to access the hidden class members by using their fully qualified
names.
C#
If you remove the new modifier, the program will still compile and run, but you will get
the following warning:55 
22 
*/ 
public class BaseC 
{ 
    public class NestedC 
    { 
        public int x = 200; 
        public int y; 
    } 
} 
public class DerivedC  : BaseC 
{ 
    // Nested type hiding the base type members.  
    new public class NestedC 
    { 
        public int x = 100; 
        public int y; 
        public int z; 
    } 
    static void Main() 
    { 
        // Creating an object from the overlapping class:  
        NestedC c1  = new NestedC();  
        // Creating an object from the hidden class:  
        BaseC.NestedC c2 = new BaseC.NestedC();  
        Console.WriteLine(c1.x);  
        Console.WriteLine(c2.x);  
    } 
} 
/* 
Output: 
100 
200 
*/ text
For more information, see The new modifier  section of the C# language specification .
C# Reference
C# Programming Guide
C# Keywords
Modifiers
Versioning with the Override and New K eywords
Knowing When to Use Override and New K eywordsThe keyword new is required on 'MyDerivedC.x' because it hides inherited  
member 'MyBaseC.x'.  
C# language specification
See alsoout (generic mo difier) (C# Reference)
Article •09/15/2021
For generic type parameters, the out keyword specifies that the type parameter is
covariant. Y ou can use the out keyword in generic interfaces and delegates.
Covariance enables you to use a more derived type than that specified by the generic
parameter. This allows for implicit conversion of classes that implement covariant
interfaces and implicit conversion of delegate types. Covariance and contravariance are
supported for reference types, but they are not supported for value types.
An interface that has a covariant type parameter enables its methods to return more
derived types than those specified by the type parameter. For example, because in .NET
Framework 4, in IEnumerable<T> , type T is covariant, you can assign an object of the
IEnumerable(Of String) type to an object of the IEnumerable(Of Object) type without
using any special conversion methods.
A covariant delegate can be assigned another delegate of the same type, but with a
more derived generic type parameter.
For more information, see Covariance and Contravariance .
The following example shows how to declare, extend, and implement a covariant
generic interface. It also shows how to use implicit conversion for classes that
implement a covariant interface.
C#Example - covariant generic interface
// Covariant interface.  
interface  ICovariant <out R> { } 
// Extending covariant interface.
interface  IExtCovariant <out R> : ICovariant <R> { } 
// Implementing covariant interface.  
class Sample<R> : ICovariant <R> { } 
class Program 
{ 
    static void Test() 
    { 
        ICovariant<Object> iobj = new Sample<Object>();  
        ICovariant<String> istr = new Sample<String>();  In a generic interface, a type parameter can be declared covariant if it satisfies the
following conditions:
The type parameter is used only as a return type of interface methods and not
used as a type of method arguments.
The type parameter is not used as a generic constraint for the interface methods.
The following example shows how to declare, instantiate, and invoke a covariant generic
delegate. It also shows how to implicitly convert delegate types.
C#        // You can assign istr to iobj because  
        // the ICovariant interface is covariant.  
        iobj = istr;  
    } 
} 
７ Note
There is one exception to this rule. If in a covariant interface you have a
contravariant generic delegate as a method parameter, you can use the
covariant type as a generic type parameter for this delegate. For more
information about covariant and contravariant generic delegates, see Variance
in Delegat es and Using V ariance for Func and Action Generic Delegat es.
Example - covariant generic delegate
// Covariant delegate.  
public delegate  R DCovariant< out R>(); 
// Methods that match the delegate signature.  
public static Control SampleControl () 
{ return new Control(); }  
public static Button SampleButton () 
{ return new Button(); }  
public void Test() 
{ 
    // Instantiate the delegates with the methods.  
    DCovariant<Control> dControl = SampleControl;  
    DCovariant<Button> dButton = SampleButton;  In a generic delegate, a type can be declared covariant if it is used only as a method
return type and not used for method arguments.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
Variance in Generic Interfaces
in
Modifiers    // You can assign dButton to dControl  
    // because the DCovariant delegate is covariant.  
    dControl = dButton;  
    // Invoke the delegate.  
    dControl();  
} 
C# language specification
See alsooverride (C# reference)
Article •04/12/2023
The override modifier is required to extend or modify the abstract or virtual
implementation of an inherited method, property, indexer, or event.
In the following example, the Square class must provide an overridden implementation
of GetArea because GetArea is inherited from the abstract Shape class:
C#
An override method provides a new implementation of the method inherited from a
base class. The method that is overridden by an override declaration is known as the
overridden base method. An override method must have the same signature as the
overridden base method. override methods support covariant return types. In
particular, the return type of an override method can derive from the return type of the
corresponding base method.
You cannot override a non-virtual or static method. The overridden base method must
be virtual, abstract, or override.
An override declaration cannot change the accessibility of the virtual method. Both
the override method and the virtual method must have the same access levelabstract  class Shape
{
    public abstract  int GetArea();
}
class Square : Shape
{
    private int _side;
    public Square(int n) => _side = n;
    // GetArea method is required to avoid a compile-time error.
    public override  int GetArea() => _side * _side;
    static void Main()
    {
        var sq = new Square( 12);
        Console.WriteLine( $"Area of the square = {sq.GetArea()} ");
    }
}
// Output: Area of the square = 144modifier .
You cannot use the new, static, or virtual modifiers to modify an override method.
An overriding property declaration must specify exactly the same access modifier, type,
and name as the inherited property. R ead-only overriding properties support covariant
return types. The overridden property must be virtual, abstract, or override.
For more information about how to use the override keyword, see Versioning with the
Override and New K eywords  and Knowing when to use Override and New K eywords . For
information about inheritance, see Inheritance .
This example defines a base class named Employee, and a derived class named
SalesEmployee. The SalesEmployee class includes an extra field, salesbonus, and
overrides the method CalculatePay in order to take it into account.
C#Example
class TestOverride
{
    public class Employee
    {
        public string Name { get; }
        // Basepay is defined as protected, so that it may be
        // accessed only by this class and derived classes.
        protected  decimal _basepay;
        // Constructor to set the name and basepay values.
        public Employee (string name, decimal basepay )
        {
            Name = name;
            _basepay = basepay;
        }
        // Declared virtual so it can be overridden.
        public virtual decimal CalculatePay ()
        {
            return _basepay;
        }
    }
    // Derive a new class from Employee.
    public class SalesEmployee  : Employee
    {
        // New field that will affect the base pay.
        private decimal _salesbonus;For more information, see the Override methods  section of the C# language
specification .
For more information about covariant return types, see the feature proposal note .
C# reference
Inheritance
C# keywords
Modifiers        // The constructor calls the base-class version, and
        // initializes the salesbonus field.
        public SalesEmployee (string name, decimal basepay, decimal 
salesbonus )
            : base(name, basepay )
        {
            _salesbonus = salesbonus;
        }
        // Override the CalculatePay method
        // to take bonus into account.
        public override  decimal CalculatePay ()
        {
            return _basepay + _salesbonus;
        }
    }
    static void Main()
    {
        // Create some new employees.
        var employee1 = new SalesEmployee( "Alice", 1000, 500);
        var employee2 = new Employee( "Bob", 1200);
        Console.WriteLine( $"Employee1 {employee1.Name}  earned: 
{employee1.CalculatePay()} ");
        Console.WriteLine( $"Employee2 {employee2.Name}  earned: 
{employee2.CalculatePay()} ");
    }
}
/*
    Output:
    Employee1 Alice earned: 1500
    Employee2 Bob earned: 1200
*/
C# language specification
See alsoabstract
virtual
new (modifier)
Polymorphism
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
 Provide product feedbackreadonly (C# Reference)
Article •09/28/2023
The readonly keyword is a modifier that can be used in five contexts:
In a field declaration , readonly indicates that assignment to the field can only
occur as part of the declaration or in a constructor in the same class. A readonly
field can be assigned and reassigned multiple times within the field declaration
and constructor.
A readonly field can't be assigned after the constructor exits. This rule has
different implications for value types and reference types:
Because value types directly contain their data, a field that is a readonly value
type is immutable.
Because reference types contain a reference to their data, a field that is a
readonly reference type must always refer to the same object. That object isn't
immutable. The readonly modifier prevents the field from being replaced by a
different instance of the reference type. However, the modifier doesn't prevent
the instance data of the field from being modified through the read-only field.
In a readonly struct type definition, readonly indicates that the structure type is
immutable. For more information, see the readonly  struct  section of the Structure
types  article.
In an instance member declaration within a structure type, readonly indicates that
an instance member doesn't modify the state of the structure. For more
information, see the readonly  instance members  section of the Structure types
article.
In a ref readonly  method return , the readonly modifier indicates that method
returns a reference and writes aren't allowed to that reference.
To declare a ref readonly  parameter  to a method.２ Warning
An externally visible type that contains an externally visible read-only field
that is a mutable reference type may be a security vulnerability and may
trigger warning CA2104  : "Do not declare read only mutable reference types."In this example, the value of the field year can't be changed in the method ChangeYear,
even though it's assigned a value in the class constructor:
C#
You can assign a value to a readonly field only in the following contexts:
When the variable is initialized in the declaration, for example:
C#
In an instance constructor of the class that contains the instance field declaration.
In the static constructor of the class that contains the static field declaration.
These constructor contexts are also the only contexts in which it's valid to pass a
readonly field as an out or ref parameter.Readonly field example
class Age
{
    private readonly  int _year;
    Age(int year)
    {
        _year = year;
    }
    void ChangeYear ()
    {
        //_year = 1967; // Compile error if uncommented.
    }
}
public readonly  int y = 5;
７ Note
The readonly keyword is different from the const  keyword. A const field can only
be initialized at the declaration of the field. A readonly field can be assigned
multiple times in the field declaration and in any constructor. Therefore, readonly
fields can have different values depending on the constructor used. Also, while a
const field is a compile-time constant, the readonly field can be used for run-time
constants as in the following example:
C#C#
In the preceding example, if you use a statement like the following example:
C#
you'll get the compiler error message:public static readonly  uint timeStamp = (uint)DateTime.Now.Ticks;
public class SamplePoint
{
    public int x;
    // Initialize a readonly field
    public readonly  int y = 25;
    public readonly  int z;
    public SamplePoint ()
    {
        // Initialize a readonly instance field
        z = 24;
    }
    public SamplePoint (int p1, int p2, int p3)
    {
        x = p1;
        y = p2;
        z = p3;
    }
    public static void Main()
    {
        SamplePoint p1 = new SamplePoint( 11, 21, 32);   // OK
        Console.WriteLine( $"p1: x= {p1.x}, y={p1.y}, z={p1.z}");
        SamplePoint p2 = new SamplePoint();
        p2.x = 55;   // OK
        Console.WriteLine( $"p2: x= {p2.x}, y={p2.y}, z={p2.z}");
    }
    /*
     Output:
        p1: x=11, y=21, z=32
        p2: x=55, y=25, z=24
    */
}
p2.y = 66;        // ErrorA readonly field cannot be assigned t o (ex cept in a construct or or a v ariable
initializer)
You can also use the readonly modifier to declare that an instance member doesn't
modify the state of a struct.
C#
The readonly modifier on a ref return indicates that the returned reference can't be
modified. The following example returns a reference to the origin. It uses the readonly
modifier to indicate that callers can't modify the origin:
C#
The type returned doesn't need to be a readonly struct. Any type that can be returned
by ref can be returned by ref readonly.
Ref readonly return can also be used in conjunction with readonly instance members on
struct types:
C#Readonly instance members
public readonly  double Sum()
{
    return X + Y;
}
Ref readonly return example
private static readonly  SamplePoint s_origin = new SamplePoint( 0, 0, 0);
public static ref readonly  SamplePoint Origin => ref s_origin;
Readonly ref readonly return example
public struct ReadonlyRefReadonlyExample
{
    private int _data;
    public readonly  ref readonly  int ReadonlyRefReadonly (ref int reference )
    {
        // _data = 1; // Compile error if uncommented.The method essentially returns a readonly reference together with the instance member
(in this case a method) being readonly (not able to modify any instance fields).
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
You can also see the language specification proposals:
readonly ref and readonly struct
readonly struct members
Add readonly modifier (style rule IDE0044)
C# Reference
C# Programming Guide
C# Keywords
Modifiers
const
Fields        return ref reference;
    }
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
 Provide product feedbacksealed (C# Reference)
Article •09/15/2021
When applied to a class, the sealed modifier prevents other classes from inheriting
from it. In the following example, class B inherits from class A, but no class can inherit
from class B.
C#
You can also use the sealed modifier on a method or property that overrides a virtual
method or property in a base class. This enables you to allow classes to derive from your
class and prevent them from overriding specific virtual methods or properties.
In the following example, Z inherits from Y but Z cannot override the virtual function F
that is declared in X and sealed in Y.
C#class A {} 
sealed class B : A {} 
Example
class X 
{ 
    protected  virtual void F() { Console.WriteLine( "X.F"); } 
    protected  virtual void F2() { Console.WriteLine( "X.F2"); } 
} 
class Y : X 
{ 
    sealed protected  override  void F() { Console.WriteLine( "Y.F"); } 
    protected  override  void F2() { Console.WriteLine( "Y.F2"); } 
} 
class Z : Y 
{ 
    // Attempting to override F causes compiler error CS0239.  
    // protected override void F() { Console.WriteLine("Z.F"); }  
    // Overriding F2 is allowed.  
    protected  override  void F2() { Console.WriteLine( "Z.F2"); } 
} When you define new methods or properties in a class, you can prevent deriving classes
from overriding them by not declaring them as virtual .
It is an error to use the abstract  modifier with a sealed class, because an abstract class
must be inherited by a class that provides an implementation of the abstract methods or
properties.
When applied to a method or property, the sealed modifier must always be used with
override .
Because structs are implicitly sealed, they cannot be inherited.
For more information, see Inheritance .
For more examples, see Abstract and Sealed Classes and Class Members .
C#
In the previous example, you might try to inherit from the sealed class by using the
following statement:
class MyDerivedC: SealedClass {} // Error
The result is an error message:
'MyDerivedC': cannot derive from sealed type 'SealedClass'sealed class SealedClass  
{ 
    public int x; 
    public int y; 
} 
class SealedTest2  
{ 
    static void Main() 
    { 
        var sc = new SealedClass();  
        sc.x = 110; 
        sc.y = 150; 
        Console.WriteLine( $"x = {sc.x}, y = {sc.y}"); 
    } 
} 
// Output: x = 110, y = 150  
RemarksTo determine whether to seal a class, method, or property, you should generally
consider the following two points:
The potential benefits that deriving classes might gain through the ability to
customize your class.
The potential that deriving classes could modify your classes in such a way that
they would no longer work correctly or as expected.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Static Classes and S tatic Class Members
Abstract and Sealed Classes and Class Members
Access Modifiers
Modifiers
override
virtualC# language specification
See alsostatic (C# Reference)
Article •09/29/2022
This page covers the static modifier keyword. The static keyword is also part of the
using static  directive.
Use the static modifier to declare a static member, which belongs to the type itself
rather than to a specific object. The static modifier can be used to declare static
classes. In classes, interfaces, and structs, you may add the static modifier to fields,
methods, properties, operators, events, and constructors. The static modifier can't be
used with indexers or finalizers. For more information, see Static Classes and S tatic Class
Members .
You can add the static modifier to a local function . A static local function can't capture
local variables or instance state.
You can add the static modifier to a lambda expression  or anonymous method . A
static lambda or anonymous method can't capture local variables or instance state.
The following class is declared as static and contains only static methods:
C#
A constant or type declaration is implicitly a static member. A static member can't be
referenced through an instance. Instead, it's referenced through the type name. For
example, consider the following class:
C#Example - static class
static class CompanyEmployee
{
    public static void DoSomething () { /*...*/ }
    public static void DoSomethingElse () { /*...*/  }
}
public class MyBaseC
{
    public struct MyStruct
    {
        public static int x = 100;To refer to the static member x, use the fully qualified name, MyBaseC.MyStruct.x,
unless the member is accessible from the same scope:
C#
While an instance of a class contains a separate copy of all instance fields of the class,
there's only one copy of each static field.
It isn't possible to use this to reference static methods or property accessors.
If the static keyword is applied to a class, all the members of the class must be static.
Classes, interfaces, and static classes may have static constructors. A static
constructor is called at some point between when the program starts and the class is
instantiated.
To demonstrate static members, consider a class that represents a company employee.
Assume that the class contains a method to count employees and a field to store the
number of employees. Both the method and the field don't belong to any one
employee instance. Instead, they belong to the class of employees as a whole. They
should be declared as static members of the class.
This example reads the name and ID of a new employee, increments the employee
counter by one, and displays the information for the new employee and the new
number of employees. This program reads the current number of employees from the
keyboard.
C#    }
}
Console.WriteLine(MyBaseC.MyStruct.x);
７ Note
The static keyword has more limited uses than in C++. T o compare with the C++
keyword, see Storage classes (C++) .
Example - static field and methodpublic class Employee4
{
    public string id;
    public string name;
    public Employee4 ()
    {
    }
    public Employee4 (string name, string id)
    {
        this.name = name;
        this.id = id;
    }
    public static int employeeCounter;
    public static int AddEmployee ()
    {
        return ++employeeCounter;
    }
}
class MainClass  : Employee4
{
    static void Main()
    {
        Console.Write( "Enter the employee's name: " );
        string name = Console.ReadLine();
        Console.Write( "Enter the employee's ID: " );
        string id = Console.ReadLine();
        // Create and configure the employee object.
        Employee4 e = new Employee4(name, id);
        Console.Write( "Enter the current number of employees: " );
        string n = Console.ReadLine();
        Employee4.employeeCounter = Int32.Parse(n);
        Employee4.AddEmployee();
        // Display the new information.
        Console.WriteLine( $"Name: {e.name} ");
        Console.WriteLine( $"ID:   {e.id}");
        Console.WriteLine( $"New Number of Employees: 
{Employee4.employeeCounter} ");
    }
}
/*
Input:
Matthias Berndt
AF643G
15
 *
Sample Output:
Enter the employee's name: Matthias BerndtThis example shows that you can initialize a static field by using another static field
that is not yet declared. The results will be undefined until you explicitly assign a value
to the static field.
C#
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming GuideEnter the employee's ID: AF643G
Enter the current number of employees: 15
Name: Matthias Berndt
ID:   AF643G
New Number of Employees: 16
*/
Example - static initia lization
class Test
{
    static int x = y;
    static int y = 5;
    static void Main()
    {
        Console.WriteLine(Test.x);
        Console.WriteLine(Test.y);
        Test.x = 99;
        Console.WriteLine(Test.x);
    }
}
/*
Output:
    0
    5
    99
*/
C# language specification
See alsoC# Keywords
Modifiers
using static directive
Static Classes and S tatic Class Members
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
 Provide product feedbackunsafe (C# Reference)
Article •09/10/2022
The unsafe keyword denotes an unsafe context, which is required for any operation
involving pointers. For more information, see Unsafe Code and P ointers .
You can use the unsafe modifier in the declaration of a type or a member. The entire
textual extent of the type or member is therefore considered an unsafe context. For
example, the following is a method declared with the unsafe modifier:
C#
The scope of the unsafe context extends from the parameter list to the end of the
method, so pointers can also be used in the parameter list:
C#
You can also use an unsafe block to enable the use of an unsafe code inside this block.
For example:
C#
To compile unsafe code, you must specify the AllowUnsafeBlocks  compiler option.
Unsafe code is not verifiable by the common language runtime.
C#unsafe static void FastCopy (byte[] src, byte[] dst, int count) 
{ 
    // Unsafe context: can use pointers here.  
} 
unsafe static void FastCopy  ( byte* ps, byte* pd, int count ) {...} 
unsafe 
{ 
    // Unsafe context: can use pointers here.  
} 
Example
// compile with: -unsafe  
class UnsafeTest  For more information, see Unsafe code  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
C# reference
C# keywords
fixed  statement
Unsafe code, pointer types, and function pointers
Pointer related operators{ 
    // Unsafe method: takes pointer to int.  
    unsafe static void SquarePtrParam (int* p) 
    { 
        *p *= *p;  
    } 
    unsafe static void Main() 
    { 
        int i = 5; 
        // Unsafe method: uses address-of operator (&).  
        SquarePtrParam(&i);  
        Console.WriteLine(i);  
    } 
} 
// Output: 25  
C# language specification
See alsovirtual (C# Reference)
Article •09/15/2021
The virtual keyword is used to modify a method, property, indexer, or event
declaration and allow for it to be overridden in a derived class. For example, this method
can be overridden by any class that inherits it:
C#
The implementation of a virtual member can be changed by an overriding member  in a
derived class. For more information about how to use the virtual keyword, see
Versioning with the Override and New K eywords  and Knowing When to Use Override
and New K eywords .
When a virtual method is invoked, the run-time type of the object is checked for an
overriding member. The overriding member in the most derived class is called, which
might be the original member, if no derived class has overridden the member.
By default, methods are non-virtual. Y ou cannot override a non-virtual method.
You cannot use the virtual modifier with the static, abstract, private, or override
modifiers. The following example shows a virtual property:
C#public virtual double Area() 
{ 
    return x * y; 
} 
Remarks
class MyBaseClass  
{ 
    // virtual auto-implemented property. Overrides can only  
    // provide specialized behavior if they implement get and set accessors.  
    public virtual string Name { get; set; } 
    // ordinary virtual property with backing field  
    private int _num; 
    public virtual int Number 
    { 
        get { return _num; }  
        set { _num = value; } 
    } Virtual properties behave like virtual methods, except for the differences in declaration
and invocation syntax.
It is an error to use the virtual modifier on a static property.
A virtual inherited property can be overridden in a derived class by including a
property declaration that uses the override modifier.
In this example, the Shape class contains the two coordinates x, y, and the Area()
virtual method. Different shape classes such as Circle, Cylinder, and Sphere inherit the
Shape class, and the surface area is calculated for each figure. Each derived class has its
own override implementation of Area().
Notice that the inherited classes Circle, Sphere, and Cylinder all use constructors that
initialize the base class, as shown in the following declaration.
C#} 
class MyDerivedClass  : MyBaseClass  
{ 
    private string _name; 
    // Override auto-implemented property with ordinary property  
    // to provide specialized accessor behavior.  
    public override  string Name 
    { 
        get 
        {  
            return _name; 
        }  
        set 
        {  
            if (!string.IsNullOrEmpty( value)) 
            {  
                _name = value; 
            }  
            else 
            {  
                _name = "Unknown" ; 
            }  
        }  
    } 
} 
ExampleThe following program calculates and displays the appropriate area for each figure by
invoking the appropriate implementation of the Area() method, according to the object
that is associated with the method.
C#public Cylinder (double r, double h): base(r, h) {} 
class TestClass  
{ 
    public class Shape 
    { 
        public const double PI = Math.PI;  
        protected  double _x, _y;  
        public Shape() 
        {  
        }  
        public Shape(double x, double y) 
        {  
            _x = x;  
            _y = y;  
        }  
        public virtual double Area() 
        {  
            return _x * _y;  
        }  
    } 
    public class Circle : Shape 
    { 
        public Circle(double r) : base(r, 0) 
        {  
        }  
        public override  double Area() 
        {  
            return PI * _x * _x;  
        }  
    } 
    public class Sphere : Shape 
    { 
        public Sphere(double r) : base(r, 0) 
        {  
        }  
        public override  double Area() 
        {  For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
Polymorphism
abstract
override
new (modifier)            return 4 * PI * _x * _x;  
        }  
    } 
    public class Cylinder  : Shape 
    { 
        public Cylinder (double r, double h) : base(r, h) 
        {  
        }  
        public override  double Area() 
        {  
            return 2 * PI * _x * _x + 2 * PI * _x * _y;  
        }  
    } 
    static void Main() 
    { 
        double r = 3.0, h = 5.0; 
        Shape c = new Circle(r);  
        Shape s = new Sphere(r);  
        Shape l = new Cylinder(r, h);  
        // Display results.  
        Console.WriteLine( "Area of Circle   = {0:F2}" , c.Area());  
        Console.WriteLine( "Area of Sphere   = {0:F2}" , s.Area());  
        Console.WriteLine( "Area of Cylinder = {0:F2}" , l.Area());  
    } 
} 
/* 
Output: 
Area of Circle   = 28.27  
Area of Sphere   = 113.10  
Area of Cylinder = 150.80  
*/ 
C# language specification
See alsovolatile (C# Reference)
Article •04/12/2023
The volatile keyword indicates that a field might be modified by multiple threads that
are executing at the same time. The compiler, the runtime system, and even hardware
may rearrange reads and writes to memory locations for performance reasons. Fields
that are declared volatile are excluded from certain kinds of optimizations. There is no
guarantee of a single total ordering of volatile writes as seen from all threads of
execution. For more information, see the Volatile  class.
The volatile keyword can be applied to fields of these types:
Reference types.
Pointer types (in an unsafe context). Note that although the pointer itself can be
volatile, the object that it points to cannot. In other words, you cannot declare a
"pointer to volatile."
Simple types such as sbyte, byte, short, ushort, int, uint, char, float, and
bool.
An enum type with one of the following base types: byte, sbyte, short, ushort,
int, or uint.
Generic type parameters known to be reference types.
IntPtr  and UIntPtr .
Other types, including double and long, cannot be marked volatile because reads and
writes to fields of those types cannot be guaranteed to be atomic. T o protect multi-
threaded access to those types of fields, use the Interlocked  class members or protect
access using the lock statement.
The volatile keyword can only be applied to fields of a class or struct. Local
variables cannot be declared volatile.７ Note
On a multiprocessor system, a volatile read operation does not guarantee to obtain
the latest value written to that memory location by any processor. Similarly, a
volatile write operation does not guarantee that the value written would be
immediately visible to other processors.
ExampleThe following example shows how to declare a public field variable as volatile.
C#
The following example demonstrates how an auxiliary or worker thread can be created
and used to perform processing in parallel with that of the primary thread. For more
information about multithreading, see Managed Threading .
C#class VolatileTest  
{ 
    public volatile  int sharedStorage;  
    public void Test(int i) 
    { 
        sharedStorage = i;  
    } 
} 
public class Worker 
{ 
    // This method is called when the thread is started.  
    public void DoWork() 
    { 
        bool work = false; 
        while (!_shouldStop)  
        {  
            work = !work; // simulate some work  
        }  
        Console.WriteLine( "Worker thread: terminating gracefully." ); 
    } 
    public void RequestStop () 
    { 
        _shouldStop = true; 
    } 
    // Keyword volatile is used as a hint to the compiler that this data  
    // member is accessed by multiple threads.  
    private volatile  bool _shouldStop;  
} 
public class WorkerThreadExample  
{ 
    public static void Main() 
    { 
        // Create the worker thread object. This does not start the thread.  
        Worker workerObject = new Worker();  
        Thread workerThread = new Thread(workerObject.DoWork);  
        // Start the worker thread.  
        workerThread.Start();  
        Console.WriteLine( "Main thread: starting worker thread..." ); With the volatile modifier added to the declaration of _shouldStop in place, you'll
always get the same results (similar to the excerpt shown in the preceding code).
However, without that modifier on the _shouldStop member, the behavior is
unpredictable. The DoWork method may optimize the member access, resulting in
reading stale data. Because of the nature of multi-threaded programming, the number
of stale reads is unpredictable. Different runs of the program will produce somewhat
different results.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# language specification: volatile keyword
C# Reference
C# Programming Guide
C# Keywords
Modifiers
lock statement
Interlocked        // Loop until the worker thread activates.  
        while (!workerThread.IsAlive)  
            ;  
        // Put the main thread to sleep for 500 milliseconds to  
        // allow the worker thread to do some work.  
        Thread.Sleep( 500); 
        // Request that the worker thread stop itself.  
        workerObject.RequestStop();  
        // Use the Thread.Join method to block the current thread  
        // until the object's thread terminates.  
        workerThread.Join();  
        Console.WriteLine( "Main thread: worker thread has terminated." ); 
    } 
    // Sample output:  
    // Main thread: starting worker thread...  
    // Worker thread: terminating gracefully.  
    // Main thread: worker thread has terminated.  
} 
C# language specification
See alsoStatemen t keywords (C# Reference)
Article •04/22/2023
Statements are program instructions. Except as described in the topics referenced in the
following table, statements are executed in sequence. The following table lists the C#
statement keywords. For more information about statements that are not expressed
with any keyword, see Statements .
Categor y C# keywords
Selection statements if, switch
Iteration statements do, for, foreach, while
Jump statements break, continue, goto, return
Exception-handling statements throw, try-catch, try-finally, try-catch-finally
checked and unchecked statements checked, unchecked
fixed statement fixed
lock statement lock
yield statement yield
C# Reference
Statements
C# KeywordsSee alsoMethod Parameters
Article •10/26/2023
By default, arguments in C# are passed to functions by value. That means a copy of the
variable is passed to the method. For value ( struct) types, a copy of the value is passed
to the method. For reference ( class) types, a copy of the reference is passed to the
method. P arameter modifiers enable you to pass arguments by reference. The following
concepts help you understand these distinctions and how to use the parameter
modifiers:
Pass b y value means passing a copy o f the v ariable  to the method.
Pass b y reference means passing access t o the v ariable  to the method.
A variable of a reference type  contains a reference to its data.
A variable of a value type  contains its data directly.
Because a struct is a value type , the method receives and operates on a copy of the
struct argument when you pass a struct by value to a method. The method has no
access to the original struct in the calling method and therefore can't change it in any
way. The method can change only the copy.
A class instance is a reference type  not a value type. When a reference type is passed by
value to a method, the method receives a copy of the reference to the class instance.
Both variables refer to the same object. The parameter is a copy of the reference. The
called method can't reassign the instance in the calling method. However, the called
method can use the copy of the reference to access the instance members. If the called
method changes an instance member, the calling method also sees those changes since
it references the same instance.
The output of the following example illustrates the difference. The method ClassTaker
changes the value of the willIChange field because the method uses the address in the
parameter to find the specified field of the class instance. The willIChange field of the
struct in the calling method doesn't change from calling StructTaker because the value
of the argument is a copy of the struct itself, not a copy of its address. StructTaker
changes the copy, and the copy is lost when the call to StructTaker is completed.
C#
class TheClass
{
    public string? willIChange;
}How an argument is passed, and whether it's a reference type or value type controls
what modifications made to the argument are visible from the caller:
When you pass a value type by value:
If the method assigns the parameter to refer to a different object, those
changes aren't visible from the caller.
If the method modifies the state of the object referred to by the parameter,
those changes aren't visible from the caller.
When you pass a reference type by value:
If the method assigns the parameter to refer to a different object, those
changes aren't visible from the caller.
If the method modifies the state of the object referred to by the parameter,
those changes are visible from the caller.struct TheStruct
{
    public string willIChange;
}
class TestClassAndStruct
{
    static void ClassTaker (TheClass c )
    {
        c.willIChange = "Changed" ;
    }
    static void StructTaker (TheStruct s )
    {
        s.willIChange = "Changed" ;
    }
    public static void Main()
    {
        TheClass testClass = new TheClass();
        TheStruct testStruct = new TheStruct();
        testClass.willIChange = "Not Changed" ;
        testStruct.willIChange = "Not Changed" ;
        ClassTaker(testClass);
        StructTaker(testStruct);
        Console.WriteLine( "Class field = {0}" , testClass.willIChange);
        Console.WriteLine( "Struct field = {0}" , testStruct.willIChange);
    }
}
/* Output:
    Class field = Changed
    Struct field = Not Changed
*/When you pass a value type by reference:
If the method assigns the parameter to refer to a different object, those
changes aren't visible from the caller.
If the method modifies the state of the object referred to by the parameter,
those changes are visible from the caller.
When you pass a reference type by reference:
If the method assigns the parameter to refer to a different object, those
changes are visible from the caller.
If the method modifies the state of the object referred to by the parameter,
those changes are visible from the caller.
Passing a reference type by reference enables the called method to replace the object to
which the reference parameter refers in the caller. The storage location of the object is
passed to the method as the value of the reference parameter. If you change the value
in the storage location of the parameter (to point to a new object), you also change the
storage location to which the caller refers. The following example passes an instance of
a reference type as a ref parameter.
C#
class Product
{
    public Product(string name, int newID)
    {
        ItemName = name;
        ItemID = newID;
    }
    public string ItemName { get; set; }
    public int ItemID { get; set; }
}
private static void ChangeByReference (ref Product itemRef )
{
    // Change the address that is stored in the itemRef parameter.
    itemRef = new Product( "Stapler" , 12345);
}
private static void ModifyProductsByReference ()
{
    // Declare an instance of Product and display its initial values.
    Product item = new Product( "Fasteners" , 54321);
    System.Console.WriteLine( "Original values in Main.  Name: {0}, ID:  
{1}\n",
        item.ItemName, item.ItemID);
    // Pass the product instance to ChangeByReference.
    ChangeByReference( ref item);
    System.Console.WriteLine( "Calling method.  Name: {0}, ID: {1}\n" ,Methods can store the values of parameters in fields. When parameters are passed by
value, that's usually safe. V alues are copied, and reference types are reachable when
stored in a field. P assing parameters by reference safely requires the compiler to define
when it's safe to assign a reference to a new variable. For every expression, the compiler
defines a safe context that bounds access to an expression or variable. The compiler uses
two scopes: safe-c ontext and ref-safe-c ontext.
The safe-c ontext defines the scope where any expression can be safely accessed.
The ref-safe-c ontext defines the scope where a reference to any expression can be
safely accessed or modified.
Informally, you can think of these scopes as the mechanism to ensure your code never
accesses or modifies a reference that's no longer valid. A reference is valid as long as it
refers to a valid object or struct. The safe-c ontext defines when a variable can be
assigned or reassigned. The ref-safe-c ontext defines when a variable can be ref assigned
or ref reassigned . Assignment assigns a variable to a new value; ref assignment  assigns
the variable to refer t o a different storage location.
You apply one of the following modifiers to a parameter declaration to pass arguments
by reference instead of by value:
ref: The argument must be initialized before calling the method. The method can
assign a new value to the parameter, but isn't required to do so.
out: The calling method isn't required to initialize the argument before calling the
method. The method must assign a value to the parameter.
readonly ref : The argument must be initialized before calling the method. The
method can't assign a new value to the parameter.
in: The argument must be initialized before calling the method. The method can't
assign a new value to the parameter. The compiler might create a temporary
variable to hold a copy of the argument to in parameters.        item.ItemName, item.ItemID);
}
// This method displays the following output:
// Original values in Main.  Name: Fasteners, ID: 54321
// Calling method.  Name: Stapler, ID: 12345
Safe context of references and values
Reference parametersMembers of a class can't have signatures that differ only by ref, ref readonly, in, or
out. A compiler error occurs if the only difference between two members of a type is
that one of them has a ref parameter and the other has an out, ref readonly, or in
parameter. However, methods can be overloaded when one method has a ref, ref
readonly, in, or out parameter and the other has a parameter that is passed by value,
as shown in the following example. In other situations that require signature matching,
such as hiding or overriding, in, ref, ref readonly, and out are part of the signature
and don't match each other.
When a parameter has one of the preceding modifiers, the corresponding argument can
have a compatible modifier:
An argument for a ref parameter must include the ref modifier.
An argument for an out parameter must include the out modifier.
An argument for an in parameter can optionally include the in modifier. If the
ref modifier is used on the argument instead, the compiler issues a warning.
An argument for a ref readonly parameter should include either the in or ref
modifiers, but not both. If neither modifier is included, the compiler issues a
warning.
When you use these modifiers, they describe how the argument is used:
ref means the method can read or write the value of the argument.
out means the method sets the value of the argument.
ref readonly means the method reads, but can't write the value of the argument.
The argument should  be passed by reference.
in means the method reads, but can't write the value of the argument. The
argument will be passed by reference or through a temporary variable.
Properties aren't variables. They're methods, and can't be passed to ref parameters.
You can't use the previous parameter modifiers in the following kinds of methods:
Async methods, which you define by using the async  modifier.
Iterator methods, which include a yield return  or yield break statement.
Extension methods  also have restrictions on the use of these argument keywords:
The out keyword can't be used on the first argument of an extension method.
The ref keyword can't be used on the first argument of an extension method
when the argument isn't a struct, or a generic type not constrained to be a struct.
The ref readonly and in keywords can't be used unless the first argument is a
struct.The ref readonly and in keywords can't be used on any generic type, even when
constrained to be a struct.
To use a ref parameter, both the method definition and the calling method must
explicitly use the ref keyword, as shown in the following example. (Except that the
calling method can omit ref when making a C OM call.)
C#
An argument that is passed to a ref parameter must be initialized before it's passed.
To use an out parameter, both the method definition and the calling method must
explicitly use the out keyword. For example:
C#
Variables passed as out arguments don't have to be initialized before being passed in a
method call. However, the called method is required to assign a value before the
method returns.
Deconstruct methods  declare their parameters with the out modifier to return multiple
values. Other methods can return value tuples  for multiple return values.ref parameter modifier
void Method(ref int refArgument )
{
    refArgument = refArgument + 44;
}
int number = 1;
Method(ref number);
Console.WriteLine(number);
// Output: 45
out parameter modifier
int initializeInMethod;
OutArgExample( out initializeInMethod);
Console.WriteLine(initializeInMethod);     // value is now 44
void OutArgExample (out int number)
{
    number = 44;
}You can declare a variable in a separate statement before you pass it as an out
argument. Y ou can also declare the out variable in the argument list of the method call,
rather than in a separate variable declaration. out variable declarations produce more
compact, readable code, and also prevent you from inadvertently assigning a value to
the variable before the method call. The following example defines the number variable
in the call to the Int32.T ryParse method.
C#
You can also declare an implicitly typed local variable.
The ref readonly modifier must be present in the method declaration. A modifier at the
call site is optional. Either the in or ref modifier can be used. The ref readonly
modifier isn't valid at the call site. Which modifier you use at the call site can help
describe characteristics of the argument. Y ou can only use ref if the argument is a
variable, and is writable. Y ou can only use in when the argument is a variable. It might
be writable, or readonly. Y ou can't add either modifier if the argument isn't a variable,
but is an expression. The following examples show these conditions. The following
method uses the ref readonly modifier to indicate that a large struct should be passed
by reference for performance reasons:
C#
You can call the method using the ref or in modifier. If you omit the modifier, the
compiler issues a warning. When the argument is an expression, not a variable, you can't
add the in or ref modifiers, so you should suppress the warning:string numberAsString = "1640";
if (Int32.TryParse(numberAsString, out int number))
    Console.WriteLine( $"Converted ' {numberAsString} ' to {number} ");
else
    Console.WriteLine( $"Unable to convert ' {numberAsString} '");
// The example displays the following output:
//       Converted '1640' to 1640
ref readonly modifier
public static void ForceByRef (ref readonly  OptionStruct thing )
{
    // elided
}C#
If the variable is a readonly variable, you must use the in modifier. The compiler issues
an error if you use the ref modifier instead.
The ref readonly modifier indicates that the method expects the argument to be a
variable rather than an expression that isn't a variable. Examples of expressions that
aren't variables are constants, method return values, and properties. If the argument
isn't a variable, the compiler issues a warning.
The in modifier is required in the method declaration but unnecessary at the call site.
C#
The in modifier allows the compiler to create a temporary variable for the argument
and pass a readonly reference to that argument. The compiler always creates a
temporary variable when the argument must be converted, when there's an implicit
conversion  from the argument type, or when the argument is a value that isn't a
variable. For example, when the argument is a literal value, or the value returned from a
property accessor. When your API requires that the argument be passed by reference,
choose the ref readonly modifier instead of the in modifier.
Methods that are defined using in parameters potentially gain performance
optimization. Some struct type arguments might be large in size, and when methods
are called in tight loops or critical code paths, the cost of copying those structures isForceByRef( in options);
ForceByRef( ref options);
ForceByRef(options); // Warning! variable should be passed with `ref` or  
`in`
ForceByRef( new OptionStruct()); // Warning, but an expression, so no  
variable to reference
in parameter modifier
int readonlyArgument = 44;
InArgExample(readonlyArgument);
Console.WriteLine(readonlyArgument);     // value is still 44
void InArgExample (in int number)
{
    // Uncomment the following line to see error CS8331
    //number = 19;
}substantial. Methods declare in parameters to specify that arguments can be passed by
reference safely because the called method doesn't modify the state of that argument.
Passing those arguments by reference avoids the (potentially) expensive copy. Y ou
explicitly add the in modifier at the call site to ensure the argument is passed by
reference, not by value. Explicitly using in has the following two effects:
Specifying in at the call site forces the compiler to select a method defined with a
matching in parameter. Otherwise, when two methods differ only in the presence
of in, the by value overload is a better match.
By specifying in, you declare your intent to pass an argument by reference. The
argument used with in must represent a location that can be directly referred to.
The same general rules for out and ref arguments apply: Y ou can't use constants,
ordinary properties, or other expressions that produce values. Otherwise, omitting
in at the call site informs the compiler that it's fine to create a temporary variable
to pass by read-only reference to the method. The compiler creates a temporary
variable to overcome several restrictions with in arguments:
A temporary variable allows compile-time constants as in parameters.
A temporary variable allows properties, or other expressions for in parameters.
A temporary variable allows arguments where there's an implicit conversion
from the argument type to the parameter type.
In all the preceding instances, the compiler creates a temporary variable that stores the
value of the constant, property, or other expression.
The following code illustrates these rules:
C#
Now, suppose another method using by-value arguments was available. The results
change as shown in the following code:static void Method(in int argument )
{
    // implementation removed
}
Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`C#
The only method call where the argument is passed by reference is the final one.
No other parameters are permitted after the params keyword in a method declaration,
and only one params keyword is permitted in a method declaration.
If the declared type of the params parameter isn't a single-dimensional array, compiler
error CS0225  occurs.
When you call a method with a params parameter, you can pass in:
A comma-separated list of arguments of the type of the array elements.
An array of arguments of the specified type.
No arguments. If you send no arguments, the length of the params list is zero.
The following example demonstrates various ways in which arguments can be sent to a
params parameter.static void Method(int argument )
{
    // implementation removed
}
static void Method(in int argument )
{
    // implementation removed
}
Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
７ Note
The preceding code uses int as the argument type for simplicity. Because int is
no larger than a reference in most modern machines, there is no benefit to passing
a single int as a readonly reference.
params modifierC#
public class MyClass
{
    public static void UseParams (params int[] list)
    {
        for (int i = 0; i < list.Length; i++)
        {
            Console.Write(list[i] + " ");
        }
        Console.WriteLine();
    }
    public static void UseParams2 (params object[] list)
    {
        for (int i = 0; i < list.Length; i++)
        {
            Console.Write(list[i] + " ");
        }
        Console.WriteLine();
    }
    static void Main()
    {
        // You can send a comma-separated list of arguments of the
        // specified type.
        UseParams( 1, 2, 3, 4);
        UseParams2( 1, 'a', "test");
        // A params parameter accepts zero or more arguments.
        // The following calling statement displays only a blank line.
        UseParams2();
        // An array argument can be passed, as long as the array
        // type matches the parameter type of the method being called.
        int[] myIntArray = { 5, 6, 7, 8, 9 };
        UseParams(myIntArray);
        object[] myObjArray = { 2, 'b', "test", "again" };
        UseParams2(myObjArray);
        // The following call causes a compiler error because the object
        // array cannot be converted into an integer array.
        //UseParams(myObjArray);
        // The following call does not cause an error, but the entire
        // integer array becomes the first element of the params array.
        UseParams2(myIntArray);
    }
}
/*
Output:
    1 2 3 4
    1 a testArgument lists  in the C# Language Specification . The language specification is the
definitive source for C# syntax and usage.    5 6 7 8 9
    2 b test again
    System.Int32[]
*/
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
 Provide product feedbacknamespace
Article •07/09/2022
The namespace keyword is used to declare a scope that contains a set of related objects.
You can use a namespace to organize code elements and to create globally unique
types.
C#
File s coped namesp ace declar ations  enable you to declare that all types in a file are in a
single namespace. File scoped namespace declarations are available with C# 10. The
following example is similar to the previous example, but uses a file scoped namespace
declaration:
C#namespace  SampleNamespace  
{ 
    class SampleClass  { } 
    interface  ISampleInterface  { } 
    struct SampleStruct { }  
    enum SampleEnum { a, b }  
    delegate  void SampleDelegate (int i); 
    namespace  Nested 
    { 
        class SampleClass2  { } 
    } 
} 
using System;  
namespace  SampleFileScopedNamespace ; 
class SampleClass  { } 
interface  ISampleInterface  { } 
struct SampleStruct { }  
enum SampleEnum { a, b }  
delegate  void SampleDelegate (int i); The preceding example doesn't include a nested namespace. File scoped namespaces
can't include additional namespace declarations. Y ou cannot declare a nested
namespace or a second file-scoped namespace:
C#
Within a namespace, you can declare zero or more of the following types:
class
interface
struct
enum
delegate
nested namespaces can be declared except in file scoped namespace declarations
The compiler adds a default namespace. This unnamed namespace, sometimes referred
to as the global namespace, is present in every file. It contains declarations not included
in a declared namespace. Any identifier in the global namespace is available for use in a
named namespace.
Namespaces implicitly have public access. For a discussion of the access modifiers you
can assign to elements in a namespace, see Access Modifiers .
It's possible to define a namespace in two or more declarations. For example, the
following example defines two classes as part of the MyCompany namespace:
C#namespace  SampleNamespace ; 
class AnotherSampleClass  
{ 
    public void AnotherSampleMethod () 
    { 
        System.Console.WriteLine(
            "SampleMethod inside SampleNamespace" ); 
    } 
} 
namespace  AnotherNamespace ; // Not allowed!  
namespace  ANestedNamespace  // Not allowed!  
{ 
   // declarations...  
} The following example shows how to call a static method in a nested namespace.
C#
For more information, see the Namespaces  section of the C# language specification . For
more information on file scoped namespace declarations, see the feature specification .namespace  MyCompany.Proj1  
{ 
    class MyClass 
    { 
    } 
} 
namespace  MyCompany.Proj1  
{ 
    class MyClass1  
    { 
    } 
} 
namespace  SomeNameSpace  
{ 
    public class MyClass 
    { 
        static void Main() 
        {  
            Nested.NestedNameSpaceClass.SayHello();  
        }  
    } 
    // a nested namespace  
    namespace  Nested 
    { 
        public class NestedNameSpaceClass  
        {  
            public static void SayHello () 
            {  
                Console.WriteLine( "Hello"); 
            }  
        }  
    } 
} 
// Output: Hello  
C# language specificationNamespace declaration preferences (IDE0160 and IDE0161)
C# reference
C# keywords
using
using static
Namespace alias qualifier ::
NamespacesSee alsousing directive
Article •03/14/2023
The using directive allows you to use types defined in a namespace without specifying
the fully qualified namespace of that type. In its basic form, the using directive imports
all the types from a single namespace, as shown in the following example:
C#
You can apply two modifiers to a using directive:
The global modifier has the same effect as adding the same using directive to
every source file in your project. This modifier was introduced in C# 10.
The static modifier imports the static members and nested types from a single
type rather than importing all the types in a namespace.
You can combine both modifiers to import the static members from a type in all source
files in your project.
You can also create an alias for a namespace or a type with a using alias dir ective.
C#
You can use the global modifier on a using alias dir ective.
The scope of a using directive without the global modifier is the file in which it
appears.
The using directive can appear:
At the beginning of a source code file, before any namespace or type declarations.using System.Text;
using Project = PC.MyCompany.Project;
７ Note
The using keyword is also used to create using st atements , which help ensure that
IDisposable  objects such as files and fonts are handled correctly. For more
information about the using st atement , see using stat ement .In any namespace, but before any namespaces or types declared in that
namespace, unless the global modifier is used, in which case the directive must
appear before all namespace and type declarations.
Otherwise, compiler error CS1529  is generated.
Create a using directive to use the types in a namespace without having to specify the
namespace. A using directive doesn't give you access to any namespaces that are
nested in the namespace you specify. Namespaces come in two categories: user-defined
and system-defined. User-defined namespaces are namespaces defined in your code.
For a list of the system-defined namespaces, see .NET API Browser .
Adding the global modifier to a using directive means that using is applied to all files
in the compilation (typically a project). The global using directive was added in C# 10.
Its syntax is:
C#
where fully-quali fied-namesp ace is the fully qualified name of the namespace whose
types can be referenced without specifying the namespace.
A global using  directive can appear at the beginning of any source code file. All global
using directives in a single file must appear before:
All using directives without the global modifier.
All namespace and type declarations in the file.
You may add global using directives to any source file. T ypically, you'll want to keep
them in a single location. The order of global using directives doesn't matter, either in
a single file, or between files.
The global modifier may be combined with the static modifier. The global modifier
may be applied to a using alias dir ective. In both cases, the directive's scope is all files in
the current compilation. The following example enables using all the methods declared
in the System.Math  in all files in your project:
C#global modifier
global using <fully-qualified- namespace >;You can also globally include a namespace by adding a <Using> item to your project file,
for example, <Using Include="My.Awesome.Namespace" />. For more information, see
<Using>  item .
The using static directive names a type whose static members and nested types you
can access without specifying a type name. Its syntax is:
C#
The <fully-qualified-type-name> is the name of the type whose static members and
nested types can be referenced without specifying a type name. If you don't provide a
fully qualified type name (the full namespace name along with the type name), C#
generates compiler error CS0246 : "The type or namespace name 'type/namespace'
couldn't be found (are you missing a using directive or an assembly reference?)".global using static System.Math;
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
For more information, see the article on Implicit using dir ectiv es
static modifier
using static <fully-qualified-type-name>;The using static directive applies to any type that has static members (or nested
types), even if it also has instance members. However, instance members can only be
invoked through the type instance.
You can access static members of a type without having to qualify the access with the
type name:
C#
Ordinarily, when you call a static member, you provide the type name along with the
member name. R epeatedly entering the same type name to invoke members of the type
can result in verbose, obscure code. For example, the following definition of a Circle
class references many members of the Math  class.
C#using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt( 3*3 + 4*4));
    }
}
using System;
public class Circle
{
   public Circle(double radius)
   {
      Radius = radius;
   }
   public double Radius { get; set; }
   public double Diameter
   {
      get { return 2 * Radius; }
   }
   public double Circumference
   {
      get { return 2 * Radius * Math.PI; }
   }
   public double Area
   {
      get { return Math.PI * Math.Pow(Radius, 2); }By eliminating the need to explicitly reference the Math  class each time a member is
referenced, the using static directive produces cleaner code:
C#
using static imports only accessible static members and nested types declared in the
specified type. Inherited members aren't imported. Y ou can import from any named
type with a using static directive, including Visual Basic modules. If F# top-level
functions appear in metadata as static members of a named type whose name is a valid
C# identifier, then the F# functions can be imported.
using static makes extension methods declared in the specified type available for
extension method lookup. However, the names of the extension methods aren't
imported into scope for unqualified reference in code.
Methods with the same name imported from different types by different using static
directives in the same compilation unit or namespace form a method group. Overload   }
}
using System;
using static System.Math;
public class Circle
{
   public Circle(double radius)
   {
      Radius = radius;
   }
   public double Radius { get; set; }
   public double Diameter
   {
      get { return 2 * Radius; }
   }
   public double Circumference
   {
      get { return 2 * Radius * PI; }
   }
   public double Area
   {
      get { return PI * Pow(Radius, 2); }
   }
}resolution within these method groups follows normal C# rules.
The following example uses the using static directive to make the static members of
the Console , Math , and String  classes available without having to specify their type
name.
C#
using System;
using static System.Console;
using static System.Math;
using static System.String;
class Program
{
   static void Main()
   {
      Write("Enter a circle's radius: " );
      var input = ReadLine();
      if (!IsNullOrEmpty(input) && double.TryParse(input, out var radius)) {
         var c = new Circle(radius);
         string s = "\nInformation about the circle:\n" ;
         s = s + Format( "   Radius: {0:N2}\n" , c.Radius);
         s = s + Format( "   Diameter: {0:N2}\n" , c.Diameter);
         s = s + Format( "   Circumference: {0:N2}\n" , c.Circumference);
         s = s + Format( "   Area: {0:N2}\n" , c.Area);
         WriteLine(s);
      }
      else {
         WriteLine( "Invalid input..." );
      }
   }
}
public class Circle
{
   public Circle(double radius)
   {
      Radius = radius;
   }
   public double Radius { get; set; }
   public double Diameter
   {
      get { return 2 * Radius; }
   }
   public double Circumference
   {
      get { return 2 * Radius * PI; }
   }In the example, the using static directive could also have been applied to the Double
type. Adding that directive would make it possible to call the TryParse(S tring, Double)
method without specifying a type name. However, using TryParse without a type name
creates less readable code, since it becomes necessary to check the using static
directives to determine which numeric type's TryParse method is called.
using static also applies to enum types. By adding using static with the enum, the
type is no longer required to use the enum members.
C#
Create a using alias directive to make it easier to qualify an identifier to a namespace or
type. In any using directive, the fully qualified namespace or type must be used   public double Area
   {
      get { return PI * Pow(Radius, 2); }
   }
}
// The example displays the following output:
//       Enter a circle's radius: 12.45
//
//       Information about the circle:
//          Radius: 12.45
//          Diameter: 24.90
//          Circumference: 78.23
//          Area: 486.95
using static Color;
enum Color
{
    Red,
    Green,
    Blue
}
class Program
{
    public static void Main()
    {
        Color color = Green;
    }
}
using aliasregardless of the using directives that come before it. No using alias can be used in the
declaration of a using directive. For example, the following example generates a
compiler error:
C#
The following example shows how to define and use a using alias for a namespace:
C#
A using alias directive can't have an open generic type on the right-hand side. For
example, you can't create a using alias for a List<T>, but you can create one for a
List<int>.
The following example shows how to define a using directive and a using alias for a
class:
C#using s = System.Text;
using s.RegularExpressions; // Generates a compiler error.
namespace  PC
{
    // Define an alias for the nested namespace.
    using Project = PC.MyCompany.Project;
    class A
    {
        void M()
        {
            // Use the alias
            var mc = new Project.MyClass();
        }
    }
    namespace  MyCompany
    {
        namespace  Project
        {
            public class MyClass { }
        }
    }
}
using System;
// Using alias directive for a class.
using AliasToMyClass = NameSpace1.MyClass;Beginning with C# 12, you can create aliases for types that were previously restricted,
including tuple types , pointer types, and other unsafe types. For more information on
the updated rules, see the feature spec .
The Microsoft.VisualBasic.MyServices  namespace ( My in Visual Basic) provides easy and
intuitive access to a number of .NET classes, enabling you to write code that interacts// Using alias directive for a generic class.
using UsingAlias = NameSpace2.MyClass< int>;
namespace  NameSpace1
{
    public class MyClass
    {
        public override  string ToString ()
        {
            return "You are in NameSpace1.MyClass." ;
        }
    }
}
namespace  NameSpace2
{
    class MyClass<T>
    {
        public override  string ToString ()
        {
            return "You are in NameSpace2.MyClass." ;
        }
    }
}
namespace  NameSpace3
{
    class MainClass
    {
        static void Main()
        {
            var instance1 = new AliasToMyClass();
            Console.WriteLine(instance1);
            var instance2 = new UsingAlias();
            Console.WriteLine(instance2);
        }
    }
}
// Output:
//    You are in NameSpace1.MyClass.
//    You are in NameSpace2.MyClass.
How to use the Visual Basic My namespacewith the computer, application, settings, resources, and so on. Although originally
designed for use with Visual Basic, the MyServices namespace can be used in C#
applications.
For more information about using the MyServices namespace from Visual Basic, see
Development with My .
You need to add a reference to the Microsoft.VisualB asic.dll  assembly in your project.
Not all the classes in the MyServices namespace can be called from a C# application: for
example, the FileSystemProxy  class is not compatible. In this particular case, the static
methods that are part of FileSystem , which are also contained in VisualBasic.dll, can be
used instead. For example, here is how to use one such method to duplicate a directory:
C#
For more information, see Using directives  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.
For more information on the global using  modifier, see the global usings feature
specification - C# 10 .
C# reference
C# keywords
Namespaces
Style rule IDE0005 - R emove unnecessary 'using' directives
Style rule IDE0065 - 'using' directive placement
using  statement// Duplicate a directory
Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory(
    @"C:\original_directory" ,
    @"C:\copy_of_original_directory" );
C# language specification
See alsoextern alias (C# Reference)
Article •09/15/2021
You might have to reference two versions of assemblies that have the same fully-
qualified type names. For example, you might have to use two or more versions of an
assembly in the same application. By using an external assembly alias, the namespaces
from each assembly can be wrapped inside root-level namespaces named by the alias,
which enables them to be used in the same file.
To reference two assemblies with the same fully-qualified type names, an alias must be
specified at a command prompt, as follows:
/r:GridV1=grid.dll
/r:GridV2=grid20.dll
This creates the external aliases GridV1 and GridV2. To use these aliases from within a
program, reference them by using the extern keyword. For example:
extern alias GridV1;
extern alias GridV2;
Each extern alias declaration introduces an additional root-level namespace that
parallels (but does not lie within) the global namespace. Thus types from each assembly
can be referred to without ambiguity by using their fully qualified name, rooted in the
appropriate namespace-alias.
In the previous example, GridV1::Grid would be the grid control from grid.dll, and
GridV2::Grid would be the grid control from grid20.dll.
If you are using Visual S tudio, aliases can be provided in similar way.７ Note
The extern keyword is also used as a method modifier, declaring a method written
in unmanaged code.
Using Visual StudioAdd reference of grid.dll  and grid20.dll  to your project in Visual S tudio. Open a property
tab and change the Aliases from global to GridV1 and GridV2 respectively.
Use these aliases the same way above
C#
Now you can create alias for a namespace or a type by using alias dir ective. For more
information, see using directive .
C#
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
:: Operator
References  (C# Compiler Options) extern alias GridV1;  
   
 extern alias GridV2;  
using Class1V1 = GridV1::Namespace.Class1;  
using Class1V2 = GridV2::Namespace.Class1;  
C# Language Specification
See alsonew constraint (C# Reference)
Article •04/12/2023
The new constraint specifies that a type argument in a generic class or method
declaration must have a public parameterless constructor. T o use the new constraint, the
type cannot be abstract.
Apply the new constraint to a type parameter when a generic class creates new
instances of the type, as shown in the following example:
C#
When you use the new() constraint with other constraints, it must be specified last:
C#
For more information, see Constraints on T ype P arameters .
You can also use the new keyword to create an instance of a type  or as a member
declaration modifier .
For more information, see the Type parameter constraints  section of the C# language
specification .
C# Reference
C# Programming Guideclass ItemFactory <T> where T : new()
{ 
    public T GetNewItem () 
    { 
        return new T();
    } 
} 
public class ItemFactory2 <T> 
    where T : IComparable , new() 
{  } 
C# language specification
See alsoC# Keywords
Genericswhere (generic type constraint) (C#
Reference)
Article •09/29/2022
The where clause in a generic definition specifies constraints on the types that are used
as arguments for type parameters in a generic type, method, delegate, or local function.
Constraints can specify interfaces, base classes, or require a generic type to be a
reference, value, or unmanaged type. They declare capabilities that the type argument
must have, and must be placed after any declared base class or implemented interfaces.
For example, you can declare a generic class, AGenericClass, such that the type
parameter T implements the IComparable<T>  interface:
C#
The where clause can also include a base class constraint. The base class constraint
states that a type to be used as a type argument for that generic type has the specified
class as a base class, or is that base class. If the base class constraint is used, it must
appear before any other constraints on that type parameter. Some types are disallowed
as a base class constraint: Object , Array , and ValueT ype. The following example shows
the types that can now be specified as a base class:
C#
In a nullable context, the nullability of the base class type is enforced. If the base class is
non-nullable (for example Base), the type argument must be non-nullable. If the base
class is nullable (for example Base?), the type argument may be either a nullable or non-public class AGenericClass <T> where T : IComparable <T> { } 
７ Note
For more information on the where clause in a query expression, see wher e clause .
public class UsingEnum <T> where T : System.Enum { } 
public class UsingDelegate <T> where T : System.Delegate  { } 
public class Multicaster <T> where T : System.MulticastDelegate  { } nullable reference type. The compiler issues a warning if the type argument is a nullable
reference type when the base class is non-nullable.
The where clause can specify that the type is a class or a struct. The struct constraint
removes the need to specify a base class constraint of System.ValueType. The
System.ValueType type may not be used as a base class constraint. The following
example shows both the class and struct constraints:
C#
In a nullable context, the class constraint requires a type to be a non-nullable reference
type. T o allow nullable reference types, use the class? constraint, which allows both
nullable and non-nullable reference types.
The where clause may include the notnull constraint. The notnull constraint limits the
type parameter to non-nullable types. The type may be a value type  or a non-nullable
reference type. The notnull constraint is available for code compiled in a nullable
enable  context . Unlike other constraints, if a type argument violates the notnull
constraint, the compiler generates a warning instead of an error. W arnings are only
generated in a nullable enable context.
The addition of nullable reference types introduces a potential ambiguity in the
meaning of T? in generic methods. If T is a struct, T? is the same as
System.Nullable<T> . However, if T is a reference type, T? means that null is a valid
value. The ambiguity arises because overriding methods can't include constraints. The
new default constraint resolves this ambiguity. Y ou'll add it when a base class or
interface declares two overloads of a method, one that specifies the struct constraint,
and one that doesn't have either the struct or class constraint applied:
C#class MyClass<T, U> 
    where T : class 
    where U : struct 
{ } 
public abstract  class B 
{ 
    public void M<T>(T? item) where T : struct { } 
    public abstract  void M<T>(T? item);  
} You use the default constraint to specify that your derived class overrides the method
without the constraint in your derived class, or explicit interface implementation. It's
only valid on methods that override base methods, or explicit interface
implementations:
C#
C#
The where clause may also include an unmanaged constraint. The unmanaged constraint
limits the type parameter to types known as unmanaged types . The unmanaged
constraint makes it easier to write low-level interop code in C#. This constraint enables
reusable routines across all unmanaged types. The unmanaged constraint can't be
combined with the class or struct constraint. The unmanaged constraint enforces that
the type must be a struct:
C#
The where clause may also include a constructor constraint, new(). That constraint
makes it possible to create an instance of a type parameter using the new operator. Thepublic class D : B 
{ 
    // Without the "default" constraint, the compiler tries to override the  
first method in B  
    public override  void M<T>(T? item) where T : default { } 
} 
） Impor tant
Generic declarations that include the notnull constraint can be used in a nullable
oblivious context, but compiler does not enforce the constraint.
#nullable enable  
    class NotNullContainer <T> 
        where T : notnull 
    { 
    } 
#nullable restore  
class UnManagedWrapper <T> 
    where T : unmanaged  
{ } new() Constraint  lets the compiler know that any type argument supplied must have an
accessible parameterless constructor. For example:
C#
The new() constraint appears last in the where clause. The new() constraint can't be
combined with the struct or unmanaged constraints. All types satisfying those
constraints must have an accessible parameterless constructor, making the new()
constraint redundant.
With multiple type parameters, use one where clause for each type parameter, for
example:
C#
You can also attach constraints to type parameters of generic methods, as shown in the
following example:
C#
Notice that the syntax to describe type parameter constraints on delegates is the same
as that of methods:
C#public class MyGenericClass <T> where T : IComparable <T>, new() 
{ 
    // The following line is not possible without new() constraint:  
    T item = new T(); 
} 
public interface  IMyInterface  { } 
namespace  CodeExample  
{ 
    class Dictionary <TKey, TVal> 
        where TKey : IComparable <TKey> 
        where TVal : IMyInterface  
    { 
        public void Add(TKey key, TVal val ) { } 
    } 
} 
public void MyMethod<T>(T t) where T : IMyInterface { }  
delegate  T MyDelegate<T>() where T : new(); For information on generic delegates, see Generic Delegates .
For details on the syntax and use of constraints, see Constraints on T ype P arameters .
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
Introduction to Generics
new Constraint
Constraints on T ype P arametersC# language specification
See alsobase (C# Reference)
Article •03/23/2023
The base keyword is used to access members of the base class from within a derived
class. Use it if you want to:
Call a method on the base class that has been overridden by another method.
Specify which base-class constructor should be called when creating instances of
the derived class.
The base class access is permitted only in a constructor, in an instance method, and in
an instance property accessor.
Using the base keyword from within a static method will give an error.
The base class that is accessed is the base class specified in the class declaration. For
example, if you specify class ClassB : ClassA, the members of ClassA are accessed
from ClassB, regardless of the base class of ClassA.
In this example, both the base class Person and the derived class Employee have a
method named GetInfo. By using the base keyword, it is possible to call the GetInfo
method of the base class from within the derived class.
C#Example 1
public class Person 
{ 
    protected  string ssn = "444-55-6666" ; 
    protected  string name = "John L. Malgraine" ; 
    public virtual void GetInfo() 
    { 
        Console.WriteLine( "Name: {0}" , name);  
        Console.WriteLine( "SSN: {0}" , ssn); 
    } 
} 
class Employee  : Person
{ 
    public string id = "ABC567EFG" ; 
    public override  void GetInfo() 
    { 
        // Calling the base class GetInfo method:  
        base.GetInfo();  For additional examples, see new, virtual , and override .
This example shows how to specify the base-class constructor called when creating
instances of a derived class.
C#        Console.WriteLine( "Employee ID: {0}" , id); 
    } 
} 
class TestClass  
{ 
    static void Main() 
    { 
        Employee E = new Employee();  
        E.GetInfo();  
    } 
} 
/* 
Output 
Name: John L. Malgraine  
SSN: 444-55-6666  
Employee ID: ABC567EFG  
*/ 
Example 2
public class BaseClass  
{ 
    int num; 
    public BaseClass () 
    { 
        Console.WriteLine( "in BaseClass()" ); 
    } 
    public BaseClass (int i) 
    { 
        num = i;  
        Console.WriteLine( "in BaseClass(int i)" ); 
    } 
    public int GetNum() 
    { 
        return num; 
    } 
} 
public class DerivedClass  : BaseClass  For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
this{ 
    // This constructor will call BaseClass.BaseClass()  
    public DerivedClass () : base() 
    { 
    } 
    // This constructor will call BaseClass.BaseClass(int i)  
    public DerivedClass (int i) : base(i) 
    { 
    } 
    static void Main() 
    { 
        DerivedClass md = new DerivedClass();  
        DerivedClass md1 = new DerivedClass( 1); 
    } 
} 
/* 
Output: 
in BaseClass()  
in BaseClass(int i)  
*/ 
C# language specification
See alsothis (C# Reference)
Article •01/14/2023
The this keyword refers to the current instance of the class and is also used as a
modifier of the first parameter of an extension method.
The following are common uses of this:
To qualify members hidden by similar names, for example:
C#
To pass an object as a parameter to other methods, for example:
C#
To declare indexers , for example:
C#７ Note
This article discusses the use of this with class instances. For more information
about its use in extension methods, see Extension Methods .
public class Employee  
{ 
    private string alias; 
    private string name; 
    public Employee (string name, string alias) 
    { 
        // Use this to qualify the members of the class  
        // instead of the constructor parameters.  
        this.name = name;  
        this.alias = alias; 
    } 
} 
CalcTax( this); 
public int this[int param] 
{ 
    get { return array[param]; }  Static member functions, because they exist at the class level and not as part of an
object, do not have a this pointer. It is an error to refer to this in a static method.
In this example, this is used to qualify the Employee class members, name and alias,
which are hidden by similar names. It is also used to pass an object to the method
CalcTax, which belongs to another class.
C#    set { array[param] = value; } 
} 
Example
class Employee  
{ 
    private string name; 
    private string alias; 
    private decimal salary = 3000.00m; 
    // Constructor:  
    public Employee (string name, string alias) 
    { 
        // Use this to qualify the fields, name and alias:  
        this.name = name;  
        this.alias = alias; 
    } 
    // Printing method:  
    public void printEmployee () 
    { 
        Console.WriteLine( "Name: {0}\nAlias: {1}" , name, alias); 
        // Passing the object to the CalcTax method by using this:  
        Console.WriteLine( "Taxes: {0:C}" , Tax.CalcTax( this)); 
    } 
    public decimal Salary 
    { 
        get { return salary; }  
    } 
} 
class Tax 
{ 
    public static decimal CalcTax(Employee E ) 
    { 
        return 0.08m * E.Salary;  
    } 
} For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
this code-style preferences (IDE0003 and IDE0009)
C# Reference
C# Programming Guide
C# Keywords
base
Methodsclass MainClass  
{ 
    static void Main() 
    { 
        // Create objects:  
        Employee E1 = new Employee( "Mingda Pan" , "mpan"); 
        // Display results:  
        E1.printEmployee();  
    } 
} 
/* 
Output: 
    Name: Mingda Pan  
    Alias: mpan  
    Taxes: $240.00  
 */ 
C# language specification
See alsonull (C# Reference)
Article •09/15/2021
The null keyword is a literal that represents a null reference, one that does not refer to
any object. null is the default value of reference-type variables. Ordinary value types
cannot be null, except for nullable value types .
The following example demonstrates some behaviors of the null keyword:
C#
class Program 
{ 
    class MyClass 
    { 
        public void MyMethod () { } 
    } 
    static void Main(string[] args) 
    { 
        // Set a breakpoint here to see that mc = null.  
        // However, the compiler considers it "unassigned."  
        // and generates a compiler error if you try to  
        // use the variable.  
        MyClass mc;  
        // Now the variable can be used, but...  
        mc = null; 
        // ... a method call on a null object raises  
        // a run-time NullReferenceException.  
        // Uncomment the following line to see for yourself.  
        // mc.MyMethod();  
        // Now mc has a value.  
        mc = new MyClass();  
        // You can call its method.  
        mc.MyMethod();  
        // Set mc to null again. The object it referenced  
        // is no longer accessible and can now be garbage-collected.  
        mc = null; 
        // A null string is not the same as an empty string.  
        string s = null; 
        string t = String.Empty; // Logically the same as ""  
        // Equals applied to any null object returns false.  For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# reference
C# keywords
Default values of C# types
Nothing (Visual Basic)        bool b = (t.Equals(s));  
        Console.WriteLine(b);  
        // Equality operator also returns false when one  
        // operand is null.  
        Console.WriteLine( "Empty string {0} null string" , s == t ? "equals" : 
"does not equal" ); 
        // Returns true.  
        Console.WriteLine( "null == null is {0}" , null == null); 
        // A value type cannot be null  
        // int i = null; // Compiler error!  
        // Use a nullable value type instead:  
        int? i = null; 
        // Keep the console window open in debug mode.  
        System.Console.WriteLine( "Press any key to exit." ); 
        System.Console.ReadKey();
    } 
} 
C# language specification
See alsobool (C# reference)
Article •01/25/2022
The bool type keyword is an alias for the .NET System.Boolean  structure type that
represents a Boolean value, which can be either true or false.
To perform logical operations with values of the bool type, use Boolean logical
operators. The bool type is the result type of comparison  and equality  operators. A
bool expression can be a controlling conditional expression in the if, do, while , and for
statements and in the conditional operator ?:.
The default value of the bool type is false.
You can use the true and false literals to initialize a bool variable or to pass a bool
value:
C#
Use the nullable bool? type, if you need to support the three-valued logic, for example,
when you work with databases that support a three-valued Boolean type. For the bool?
operands, the predefined & and | operators support the three-valued logic. For more
information, see the Nullable Boolean logical operators  section of the Boolean logical
operators  article.
For more information about nullable value types, see Nullable value types .
C# provides only two conversions that involve the bool type. Those are an implicit
conversion to the corresponding nullable bool? type and an explicit conversion fromLiterals
bool check = true; 
Console.WriteLine(check ? "Checked"  : "Not checked" );  // output: Checked  
Console.WriteLine( false ? "Checked"  : "Not checked" );  // output: Not  
checked 
Three-valued Boolean logic
Conversionsthe bool? type. However, .NET provides additional methods that you can use to convert
to or from the bool type. For more information, see the Converting to and from
Boolean values  section of the System.Boolean  API reference page.
For more information, see The bool type  section of the C# language specification .
C# reference
Value types
true and false operatorsC# language specification
See alsodefault (C# reference)
Article •09/15/2021
You can use the default keyword in the following contexts:
To specify the default case in the switch  statement .
As the default operator or literal  to produce the default value of a type.
As the default  type constraint  on a generic method override or explicit interface
implementation.
C# reference
C# keywordsSee alsoadd (C# Reference)
Article •09/15/2021
The add contextual keyword is used to define a custom event accessor that is invoked
when client code subscribes to your event . If you supply a custom add accessor, you
must also supply a remove  accessor.
The following example shows an event that has custom add and remove  accessors. For
the full example, see How to implement interface events .
C#
You do not typically need to provide your own custom event accessors. The accessors
that are automatically generated by the compiler when you declare an event are
sufficient for most scenarios.
EventsExample
class Events : IDrawingObject  
{ 
    event EventHandler PreDrawEvent;  
    event EventHandler IDrawingObject.OnDraw  
    { 
        add => PreDrawEvent += value; 
        remove => PreDrawEvent -= value; 
    } 
} 
See alsoget (C# Reference)
Article •09/29/2022
The get keyword defines an accessor method in a property or indexer that returns the
property value or the indexer element. For more information, see Properties , Auto-
Implemented Properties  and Indexers .
The following example defines both a get and a set accessor for a property named
Seconds. It uses a private field named _seconds to back the property value.
C#
Often, the get accessor consists of a single statement that returns a value, as it did in
the previous example. Y ou can implement the get accessor as an expression-bodied
member. The following example implements both the get and the set accessor as
expression-bodied members.
C#
For simple cases in which a property's get and set accessors perform no other
operation than setting or retrieving a value in a private backing field, you can takeclass TimePeriod  
{ 
     private double _seconds;  
     public double Seconds  
     { 
         get { return _seconds; }  
         set { _seconds = value; } 
     } 
} 
class TimePeriod  
{ 
    private double _seconds;  
    public double Seconds  
    { 
        get => _seconds;  
        set => _seconds = value; 
    } 
} advantage of the C# compiler's support for auto-implemented properties. The following
example implements Hours as an auto-implemented property.
C#
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Propertiesclass TimePeriod2  
{ 
    public double Hours { get; set; } 
} 
C# Language Specification
See alsoinit (C# Reference)
Article •12/06/2023
The init keyword defines an accessor method in a property or indexer. An init-only
setter assigns a value to the property or the indexer element only during object
construction. An init enforces immutability, so that once the object is initialized, it can't
be changed. An init accessor enables calling code to use an object initializer  to set the
initial value. As a contrast, an auto-implemented property  with only a get setter must
be initialized by calling a constructor. A property with a private set accessor can be
modified after construction, but only in the class.
The following example defines both a get and an init accessor for a property named
YearOfBirth. It uses a private field named _yearOfBirth to back the property value.
C#
Often, the init accessor consists of a single statement that assigns a value, as it did in
the previous example. Because of init, the following doesn 't work:
C#
An init accessor doesn't force callers to set the property. Instead, it allows callers to
use an object initializer while prohibiting later modification. Y ou can add the required
modifier to force callers to set a property. The following example shows an init onlyclass Person_InitExample
{
     private int _yearOfBirth;
     public int YearOfBirth
     {
         get { return _yearOfBirth; }
         init { _yearOfBirth = value; }
     }
}
var john = new Person_InitExample
{
    YearOfBirth = 1984
};
john.YearOfBirth = 1926; //Not allowed, as its value can only be set once in  
the constructorproperty with a nullable value type as its backing field. If a caller doesn't initialize the
YearOfBirth property, that property will have the default null value:
C#
To force callers to set an initial non-null value, you add the required modifier, as shown
in the following example:
C#
The init accessor can be used as an expression-bodied member. Example:
C#class Person_InitExampleNullability
{
    private int? _yearOfBirth;
    public int? YearOfBirth
    {
        get => _yearOfBirth;
        init => _yearOfBirth = value;
    }
}
class Person_InitExampleNonNull
{
    private int _yearOfBirth;
    public required int YearOfBirth
    {
        get => _yearOfBirth;
        init => _yearOfBirth = value;
    }
}
class Person_InitExampleExpressionBodied
{
    private int _yearOfBirth;
    public int YearOfBirth
    {
        get => _yearOfBirth;
        init => _yearOfBirth = value;
    }
}The init accessor can also be used in autoimplemented properties, as the following
example code demonstrates:
C#
The following example shows the distinction between a private set, read only, and
init properties. Both the private set version and the read only version require callers to
use the added constructor to set the name property. The private set version allows a
person to change their name after the instance is constructed. The init version doesn't
require a constructor. Callers can initialize the properties using an object initializer:
C#
C#class Person_InitExampleAutoProperty
{
    public int YearOfBirth { get; init; }
}
class PersonPrivateSet
{
    public string FirstName { get; private set; }
    public string LastName { get; private set; }
    public PersonPrivateSet (string first, string last) => (FirstName,  
LastName) = (first, last);
    public void ChangeName (string first, string last) => (FirstName,  
LastName) = (first, last);
}
class PersonReadOnly
{
    public string FirstName { get; }
    public string LastName { get; }
    public PersonReadOnly (string first, string last) => (FirstName,  
LastName) = (first, last);
}
class PersonInit
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}
PersonPrivateSet personPrivateSet = new("Bill", "Gates");
PersonReadOnly personReadOnly = new("Bill", "Gates");
PersonInit personInit = new() { FirstName = "Bill", LastName = "Gates" };For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
PropertiesC# language specification
See also
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
 Provide product feedbackpartial type (C# Reference)
Article •09/15/2021
Partial type definitions allow for the definition of a class, struct, interface, or record to be
split into multiple files.
In File1.cs :
C#
In File2.cs  the declaration:
C#
Splitting a class, struct or interface type over several files can be useful when you are
working with large projects, or with automatically generated code such as that provided
by the Windows Forms Designer . A partial type may contain a partial method . For more
information, see Partial Classes and Methods .namespace  PC 
{ 
    partial class A 
    { 
        int num = 0; 
        void MethodA() { } 
        partial void MethodC(); 
    } 
} 
namespace  PC 
{ 
    partial class A 
    { 
        void MethodB() { } 
        partial void MethodC() { } 
    } 
} 
Remarks
C# language specificationFor more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
Modifiers
Introduction to GenericsSee alsopartial metho d (C# Reference)
Article •01/05/2023
A partial method has its signature defined in one part of a partial type, and its
implementation defined in another part of the type. P artial methods enable class
designers to provide method hooks, similar to event handlers, that developers may
decide to implement or not. If the developer does not supply an implementation, the
compiler removes the signature at compile time. The following conditions apply to
partial methods:
Declarations must begin with the contextual keyword partial .
Signatures in both parts of the partial type must match.
The partial keyword isn't allowed on constructors, finalizers, overloaded operators,
property declarations, or event declarations.
A partial method isn't required to have an implementation in the following cases:
It doesn't have any accessibility modifiers (including the default private ).
It returns void.
It doesn't have any out parameters.
It doesn't have any of the following modifiers virtual , override , sealed , new, or
extern .
Any method that doesn't conform to all those restrictions (for example, public virtual
partial void method), must provide an implementation.
The following example shows a partial method defined in two parts of a partial class:
C#
namespace  PM
{
    partial class A
    {
        partial void OnSomethingHappened (string s);
    }
    // This part can be in a separate file.
    partial class A
    {
        // Comment out this method and the program
        // will still compile.Partial methods can also be useful in combination with source generators. For example a
regex could be defined using the following pattern:
C#
For more information, see Partial Classes and Methods .
C# Reference
partial type        partial void OnSomethingHappened (String s )
        {
            Console.WriteLine( "Something happened: {0}" , s);
        }
    }
}
[GeneratedRegex( "(dog|cat|fish)" )]
partial bool IsPetMatch (string input);
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
 Provide product feedbackremove (C# Reference)
Article •09/15/2021
The remove contextual keyword is used to define a custom event accessor that is
invoked when client code unsubscribes from your event . If you supply a custom remove
accessor, you must also supply an add accessor.
The following example shows an event with custom add and remove accessors. For the
full example, see How to implement interface events .
C#
You do not typically need to provide your own custom event accessors. The accessors
that are automatically generated by the compiler when you declare an event are
sufficient for most scenarios.
EventsExample
class Events : IDrawingObject  
{ 
    event EventHandler PreDrawEvent;  
    event EventHandler IDrawingObject.OnDraw  
    { 
        add => PreDrawEvent += value; 
        remove => PreDrawEvent -= value; 
    } 
} 
See alsorequired modifier (C# Reference)
Article •01/31/2023
The required modifier indicates that the field or property it's applied to must be
initialized by an object initializer . Any expression that initializes a new instance of the
type must initialize all requir ed member s. The required modifier is available beginning
with C# 11. The required modifier enables developers to create types where properties
or fields must be properly initialized, yet still allow initialization using object initializers.
Several rules ensure this behavior:
The required modifier can be applied to fields and properties declared in struct,
and class types, including record and record struct types. The required
modifier can't be applied to members of an interface.
Explicit interface implementations can't be marked as required. They can't be set
in object initializers.
Required members must be initialized, but they may be initialized to null. If the
type is a non-nullable reference type, the compiler issues a warning if you initialize
the member to null. The compiler issues an error if the member isn't initialized at
all.
Required members must be at least as visible as their containing type. For example,
a public class can't contain a required field that's protected. Furthermore,
required properties must have setters ( set or init accessors) that are at least as
visible as their containing types. Members that aren't accessible can't be set by
code that creates an instance.
Derived classes can't hide a required member declared in the base class. Hiding a
required member prevents callers from using object initializers for it. Furthermore,
derived types that override a required property must include the required
modifier. The derived type can't remove the required state. Derived types can add
the required modifier when overriding a property.
A type with any required members may not be used as a type argument when the
type parameter includes the new() constraint. The compiler can't enforce that all
required members are initialized in the generic code.
The required modifier isn't allowed on the declaration for positional parameters
on a record. Y ou can add an explicit declaration for a positional property that does
include the required modifier.
Some types, such as positional records , use a primary constructor to initialize positional
properties. If any of those properties include the required modifier, the primary
constructor adds the SetsR equiredMembers  attribute. This indicates that the primaryconstructor initializes all required members. Y ou can write your own constructor with the
System.Diagnostics.CodeAnalysis.SetsR equiredMembersAttribute  attribute. However, the
compiler doesn't verify that these constructors do initialize all required members.
Rather, the attribute asserts to the compiler that the constructor does initialize all
required members. The SetsRequiredMembers attribute adds these rules to constructors:
A constructor that chains to another constructor annotated with the
SetsRequiredMembers attribute, either this(), or base(), must also include the
SetsRequiredMembers attribute. That ensures that callers can correctly use all
appropriate constructors.
Copy constructors generated for record types have the SetsRequiredMembers
attribute applied if any of the members are required.
The following code shows a class hierarchy that uses the required modifier for the
FirstName and LastName properties:
C#２ Warning
The SetsRequiredMembers disables the compiler's checks that all required members
are initialized when an object is created. Use it with caution.
public class Person 
{ 
    public Person() { } 
    [SetsRequiredMembers ] 
    public Person(string firstName, string lastName ) => 
        (FirstName, LastName) = (firstName, lastName);  
    public required string FirstName { get; init; } 
    public required string LastName { get; init; } 
    public int? Age { get; set; } 
} 
public class Student : Person 
{ 
    public Student() : base() 
    { 
    } 
    [SetsRequiredMembers ] 
    public Student(string firstName, string lastName ) : 
        base(firstName, lastName ) 
    { For more information on required members, see the C#11 - R equired members  feature
specification.    } 
    public double GPA { get; set; } 
} set (C# Reference)
Article •09/29/2022
The set keyword defines an accessor method in a property or indexer that assigns a
value to the property or the indexer element. For more information and examples, see
Properties , Auto-Implemented Properties , and Indexers .
The following example defines both a get and a set accessor for a property named
Seconds. It uses a private field named _seconds to back the property value.
C#
Often, the set accessor consists of a single statement that assigns a value, as it did in
the previous example. Y ou can implement the set accessor as an expression-bodied
member. The following example implements both the get and the set accessors as
expression-bodied members.
C#
For simple cases in which a property's get and set accessors perform no other
operation than setting or retrieving a value in a private backing field, you can takeclass TimePeriod  
{ 
     private double _seconds;  
     public double Seconds  
     { 
         get { return _seconds; }  
         set { _seconds = value; } 
     } 
} 
class TimePeriod  
{ 
    private double _seconds;  
    public double Seconds  
    { 
        get => _seconds;  
        set => _seconds = value; 
    } 
} advantage of the C# compiler's support for auto-implemented properties. The following
example implements Hours as an auto-implemented property.
C#
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords
Propertiesclass TimePeriod2  
{ 
    public double Hours { get; set; } 
} 
C# language specification
See alsowhen (C# reference)
Article •04/22/2023
You use the when contextual keyword to specify a filter condition in the following
contexts:
In a catch clause of a try-catch  or try-catch-finally  statement.
As a case guard  in the switch  statement .
As a case guard  in the switch  expression .
The when keyword can be used in a catch clause to specify a condition that must be true
for the handler for a specific exception to execute. Its syntax is:
C#
where expr is an expression that evaluates to a Boolean value. If it returns true, the
exception handler executes; if false, it does not.
The following example uses the when keyword to conditionally execute handlers for an
HttpR equestException  depending on the text of the exception message.
C#when in a catch clause
catch (ExceptionType [e]) when (expr) 
using System;  
using System.Net.Http;  
using System.Threading.Tasks;  
class Program 
{ 
    static void Main() 
    { 
        Console.WriteLine(MakeRequest().Result);  
    } 
    public static async Task<string> MakeRequest () 
    { 
        var client = new HttpClient();  
        var streamTask = client.GetStringAsync( "https://localHost:10000" ); 
        try 
        {  
            var responseText = await streamTask;  C# reference
C# keywords            return responseText;  
        }  
        catch (HttpRequestException e) when (e.Message.Contains( "301")) 
        {  
            return "Site Moved" ; 
        }  
        catch (HttpRequestException e) when (e.Message.Contains( "404")) 
        {  
            return "Page Not Found" ; 
        }  
        catch (HttpRequestException e)  
        {  
            return e.Message;  
        }  
    } 
} 
See alsovalue (C# Reference)
Article •09/15/2021
The contextual keyword value is used in the set accessor in property  and indexer
declarations. It is similar to an input parameter of a method. The word value references
the value that client code is attempting to assign to the property or indexer. In the
following example, MyDerivedClass has a property called Name that uses the value
parameter to assign a new string to the backing field name. From the point of view of
client code, the operation is written as a simple assignment.
C#
class MyBaseClass  
{ 
    // virtual auto-implemented property. Overrides can only  
    // provide specialized behavior if they implement get and set accessors.  
    public virtual string Name { get; set; } 
    // ordinary virtual property with backing field  
    private int _num; 
    public virtual int Number 
    { 
        get { return _num; }  
        set { _num = value; } 
    } 
} 
class MyDerivedClass  : MyBaseClass  
{ 
    private string _name; 
    // Override auto-implemented property with ordinary property  
    // to provide specialized accessor behavior.  
    public override  string Name 
    { 
        get 
        {  
            return _name; 
        }  
        set 
        {  
            if (!string.IsNullOrEmpty( value)) 
            {  
                _name = value; 
            }  
            else 
            {  
                _name = "Unknown" ; 
            }  For more information, see the Properties  and Indexers  articles.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Reference
C# Programming Guide
C# Keywords        }  
    } 
} 
C# language specification
See alsoQuery keywords (C# Reference)
Article •08/05/2023
This section contains the contextual keywords used in query expressions.
Clause Descr iption
from Specifies a data source and a range variable (similar to an iteration variable).
where Filters source elements based on one or more Boolean expressions separated by
logical AND and OR operators ( && or || ).
select Specifies the type and shape that the elements in the returned sequence will have
when the query is executed.
group Groups query results according to a specified key value.
into Provides an identifier that can serve as a reference to the results of a join, group or
select clause.
orderby Sorts query results in ascending or descending order based on the default
comparer for the element type.
join Joins two data sources based on an equality comparison between two specified
matching criteria.
let Introduces a range variable to store subexpression results in a query expression.
in Contextual keyword in a join clause.
on Contextual keyword in a join clause.
equals Contextual keyword in a join clause.
by Contextual keyword in a group  clause.
ascending Contextual keyword in an orderby  clause.
descending Contextual keyword in an orderby  clause.
C# Keywords
LINQ in C#In this section
See alsofrom clause (C# Reference)
Article •09/21/2022
A query expression must begin with a from clause. Additionally, a query expression can
contain sub-queries, which also begin with a from clause. The from clause specifies the
following:
The data source on which the query or sub-query will be run.
A local range v ariable  that represents each element in the source sequence.
Both the range variable and the data source are strongly typed. The data source
referenced in the from clause must have a type of IEnumerable , IEnumerable<T> , or a
derived type such as IQueryable<T> .
In the following example, numbers is the data source and num is the range variable. Note
that both variables are strongly typed even though the var keyword is used.
C#
class LowNums 
{ 
    static void Main() 
    { 
        // A simple data source.  
        int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 }; 
        // Create the query.  
        // lowNums is an IEnumerable<int>  
        var lowNums = from num in numbers  
            where num < 5 
            select num; 
        // Execute the query.  
        foreach (int i in lowNums)  
        {  
            Console.Write(i + " "); 
        }  
    } 
} 
// Output: 4 1 3 2 0  
The range variableThe compiler infers the type of the range variable when the data source implements
IEnumerable<T> . For example, if the source has a type of IEnumerable<Customer>, then
the range variable is inferred to be Customer. The only time that you must specify the
type explicitly is when the source is a non-generic IEnumerable type such as ArrayList .
For more information, see How to query an ArrayList with LINQ .
In the previous example num is inferred to be of type int. Because the range variable is
strongly typed, you can call methods on it or use it in other operations. For example,
instead of writing select num, you could write select num.ToString() to cause the
query expression to return a sequence of strings instead of integers. Or you could write
select num + 10 to cause the expression to return the sequence 14, 11, 13, 12, 10. For
more information, see select clause .
The range variable is like an iteration variable in a foreach  statement except for one very
important difference: a range variable never actually stores data from the source. It's just
a syntactic convenience that enables the query to describe what will occur when the
query is executed. For more information, see Introduction to LINQ Queries (C#) .
In some cases, each element in the source sequence may itself be either a sequence or
contain a sequence. For example, your data source may be an IEnumerable<Student>
where each student object in the sequence contains a list of test scores. T o access the
inner list within each Student element, you can use compound from clauses. The
technique is like using nested foreach  statements. Y ou can add where  or orderby  clauses
to either from clause to filter the results. The following example shows a sequence of
Student objects, each of which contains an inner List of integers representing test
scores. T o access the inner list, use a compound from clause. Y ou can insert clauses
between the two from clauses if necessary.
C#Compound from clauses
class CompoundFrom  
{ 
    // The element type of the data source.  
    public class Student 
    { 
        public string LastName { get; set; } 
        public List<int> Scores { get; set;} 
    } 
    static void Main() 
    {         // Use a collection initializer to create the data source. Note that  
        // each element in the list contains an inner sequence of scores.  
        List<Student> students = new List<Student>  
        {  
           new Student {LastName= "Omelchenko" , Scores= new List<int> {97, 
72, 81, 60}}, 
           new Student {LastName= "O'Donnell" , Scores= new List<int> {75, 84, 
91, 39}}, 
           new Student {LastName= "Mortensen" , Scores= new List<int> {88, 94, 
65, 85}}, 
           new Student {LastName= "Garcia" , Scores= new List<int> {97, 89, 
85, 82}}, 
           new Student {LastName= "Beebe", Scores= new List<int> {35, 72, 91, 
70}} 
        };  
        // Use a compound from to access the inner sequence within each  
element.  
        // Note the similarity to a nested foreach statement.  
        var scoreQuery = from student in students  
                         from score in student.Scores  
                            where score > 90 
                            select new { Last = student.LastName, score };  
        // Execute the queries.  
        Console.WriteLine( "scoreQuery:" ); 
        // Rest the mouse pointer on scoreQuery in the following line to  
        // see its type. The type is IEnumerable<'a>, where 'a is an  
        // anonymous type defined as new {string Last, int score}. That is,  
        // each instance of this anonymous type has two members, a string  
        // (Last) and an int (score).  
        foreach (var student in scoreQuery)  
        {  
            Console.WriteLine( "{0} Score: {1}" , student.Last,  
student.score);  
        }  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* 
scoreQuery:  
Omelchenko Score: 97  
O'Donnell Score: 91  
Mortensen Score: 94  
Garcia Score: 97  
Beebe Score: 91  
*/ 
Using Multip le from Clauses to Perform JoinsA compound from clause is used to access inner collections in a single data source.
However, a query can also contain multiple from clauses that generate supplemental
queries from independent data sources. This technique enables you to perform certain
types of join operations that are not possible by using the join clause .
The following example shows how two from clauses can be used to form a complete
cross join of two data sources.
C#
class CompoundFrom2  
{ 
    static void Main() 
    { 
        char[] upperCase = { 'A', 'B', 'C' }; 
        char[] lowerCase = { 'x', 'y', 'z' }; 
        // The type of joinQuery1 is IEnumerable<'a>, where 'a  
        // indicates an anonymous type. This anonymous type has two  
        // members, upper and lower, both of type char.  
        var joinQuery1 =  
            from upper in upperCase  
            from lower in lowerCase  
            select new { upper, lower };  
        // The type of joinQuery2 is IEnumerable<'a>, where 'a  
        // indicates an anonymous type. This anonymous type has two  
        // members, upper and lower, both of type char.  
        var joinQuery2 =  
            from lower in lowerCase  
            where lower != 'x' 
            from upper in upperCase  
            select new { lower, upper };  
        // Execute the queries.  
        Console.WriteLine( "Cross join:" ); 
        // Rest the mouse pointer on joinQuery1 to verify its type.  
        foreach (var pair in joinQuery1)  
        {  
            Console.WriteLine( "{0} is matched to {1}" , pair.upper,  
pair.lower);  
        }  
        Console.WriteLine( "Filtered non-equijoin:" ); 
        // Rest the mouse pointer over joinQuery2 to verify its type.  
        foreach (var pair in joinQuery2)  
        {  
            Console.WriteLine( "{0} is matched to {1}" , pair.lower,  
pair.upper);  
        }  
        // Keep the console window open in debug mode.  For more information about join operations that use multiple from clauses, see Perform
left outer joins .
Query K eywords (LINQ)
Language Integrated Query (LINQ)        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
        Cross join:  
        A is matched to x  
        A is matched to y  
        A is matched to z  
        B is matched to x  
        B is matched to y  
        B is matched to z  
        C is matched to x  
        C is matched to y  
        C is matched to z  
        Filtered non-equijoin:  
        y is matched to A  
        y is matched to B  
        y is matched to C  
        z is matched to A  
        z is matched to B  
        z is matched to C  
        */  
See alsowhere clause (C# Reference)
Article •09/15/2021
The where clause is used in a query expression to specify which elements from the data
source will be returned in the query expression. It applies a Boolean condition
(predicat e) to each source element (referenced by the range variable) and returns those
for which the specified condition is true. A single query expression may contain multiple
where clauses and a single clause may contain multiple predicate subexpressions.
In the following example, the where clause filters out all numbers except those that are
less than five. If you remove the where clause, all numbers from the data source would
be returned. The expression num < 5 is the predicate that is applied to each element.
C#
Within a single where clause, you can specify as many predicates as necessary by using
the && and || operators. In the following example, the query specifies two predicates in
order to select only the even numbers that are less than five.Example 1
class WhereSample
{
    static void Main()
    {
        // Simple data source. Arrays support IEnumerable<T>.
        int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
        // Simple query with one predicate in where clause.
        var queryLowNums =
            from num in numbers
            where num < 5
            select num;
        // Execute the query.
        foreach (var s in queryLowNums)
        {
            Console.Write(s.ToString() + " ");
        }
    }
}
//Output: 4 1 3 2 0
Example 2C#
A where clause may contain one or more methods that return Boolean values. In the
following example, the where clause uses a method to determine whether the current
value of the range variable is even or odd.
C#class WhereSample2
{
    static void Main()
    {
        // Data source.
        int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
        // Create the query with two predicates in where clause.
        var queryLowNums2 =
            from num in numbers
            where num < 5 && num % 2 == 0
            select num;
        // Execute the query
        foreach (var s in queryLowNums2)
        {
            Console.Write(s.ToString() + " ");
        }
        Console.WriteLine();
        // Create the query with two where clause.
        var queryLowNums3 =
            from num in numbers
            where num < 5
            where num % 2 == 0
            select num;
        // Execute the query
        foreach (var s in queryLowNums3)
        {
            Console.Write(s.ToString() + " ");
        }
    }
}
// Output:
// 4 2 0
// 4 2 0
Example 3
class WhereSample3
{The where clause is a filtering mechanism. It can be positioned almost anywhere in a
query expression, except it cannot be the first or last clause. A where clause may appear
either before or after a group  clause depending on whether you have to filter the source
elements before or after they are grouped.
If a specified predicate is not valid for the elements in the data source, a compile-time
error will result. This is one benefit of the strong type-checking provided by LINQ.
At compile time the where keyword is converted into a call to the Where  Standard
Query Operator method.
Query K eywords (LINQ)
from clause
select clause
Filtering Data    static void Main()
    {
        // Data source
        int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
        // Create the query with a method call in the where clause.
        // Note: This won't work in LINQ to SQL unless you have a
        // stored procedure that is mapped to a method by this name.
        var queryEvenNums =
            from num in numbers
            where IsEven(num)
            select num;
         // Execute the query.
        foreach (var s in queryEvenNums)
        {
            Console.Write(s.ToString() + " ");
        }
    }
    // Method may be instance method or static method.
    static bool IsEven(int i)
    {
        return i % 2 == 0;
    }
}
//Output: 4 8 6 2 0
Remarks
See alsoLINQ in C#select clause (C# Reference)
Article •09/15/2021
In a query expression, the select clause specifies the type of values that will be
produced when the query is executed. The result is based on the evaluation of all the
previous clauses and on any expressions in the select clause itself. A query expression
must terminate with either a select clause or a group  clause.
The following example shows a simple select clause in a query expression.
C#
The type of the sequence produced by the select clause determines the type of the
query variable queryHighScores. In the simplest case, the select clause just specifies the
range variable. This causes the returned sequence to contain elements of the same type
as the data source. For more information, see Type R elationships in LINQ Query
Operations . However, the select clause also provides a powerful mechanism for
transforming (or projecting ) source data into new types. For more information, see Data
Transformations with LINQ (C#) .class SelectSample1
{
    static void Main()
    {
        //Create the data source
        List<int> Scores = new List<int>() { 97, 92, 81, 60 };
        // Create the query.
        IEnumerable< int> queryHighScores =
            from score in Scores
            where score > 80
            select score;
        // Execute the query.
        foreach (int i in queryHighScores)
        {
            Console.Write(i + " ");
        }
    }
}
//Output: 97 92 81
ExampleThe following example shows all the different forms that a select clause may take. In
each query, note the relationship between the select clause and the type of the query
variable  (studentQuery1, studentQuery2, and so on).
C#
    class SelectSample2
    {
        // Define some classes
        public class Student
        {
            public string First { get; set; }
            public string Last { get; set; }
            public int ID { get; set; }
            public List<int> Scores;
            public ContactInfo GetContactInfo (SelectSample2 app, int id)
            {
                ContactInfo cInfo =
                    (from ci in app.contactList
                    where ci.ID == id
                    select ci)
                    .FirstOrDefault();
                return cInfo;
            }
            public override  string ToString ()
            {
                return First + " " + Last + ":" + ID;
            }
        }
        public class ContactInfo
        {
            public int ID { get; set; }
            public string Email { get; set; }
            public string Phone { get; set; }
            public override  string ToString () { return Email + "," + Phone;  
}
        }
        public class ScoreInfo
        {
            public double Average { get; set; }
            public int ID { get; set; }
        }
        // The primary data source
        List<Student> students = new List<Student>()
        {
             new Student {First= "Svetlana" , Last="Omelchenko" , ID=111, 
Scores= new List<int>() {97, 92, 81, 60}},
             new Student {First= "Claire" , Last="O'Donnell" , ID=112, Scores= new List<int>() {75, 84, 91, 39}},
             new Student {First= "Sven", Last="Mortensen" , ID=113, Scores= 
new List<int>() {88, 94, 65, 91}},
             new Student {First= "Cesar", Last="Garcia" , ID=114, Scores= new 
List<int>() {97, 89, 85, 82}},
        };
        // Separate data source for contact info.
        List<ContactInfo> contactList = new List<ContactInfo>()
        {
            new ContactInfo {ID= 111, Email= "SvetlanO@Contoso.com" , 
Phone="206-555-0108" },
            new ContactInfo {ID= 112, Email= "ClaireO@Contoso.com" , 
Phone="206-555-0298" },
            new ContactInfo {ID= 113, Email= "SvenMort@Contoso.com" , 
Phone="206-555-1130" },
            new ContactInfo {ID= 114, Email= "CesarGar@Contoso.com" , 
Phone="206-555-0521" }
        };
        static void Main(string[] args)
        {
            SelectSample2 app = new SelectSample2();
            // Produce a filtered sequence of unmodified Students.
            IEnumerable<Student> studentQuery1 =
                from student in app.students
                where student.ID > 111
                select student;
            Console.WriteLine( "Query1: select range_variable" );
            foreach (Student s in studentQuery1)
            {
                Console.WriteLine(s.ToString());
            }
            // Produce a filtered sequence of elements that contain
            // only one property of each Student.
            IEnumerable<String> studentQuery2 =
                from student in app.students
                where student.ID > 111
                select student.Last;
            Console.WriteLine( "\r\n studentQuery2: select  
range_variable.Property" );
            foreach (string s in studentQuery2)
            {
                Console.WriteLine(s);
            }
            // Produce a filtered sequence of objects created by
            // a method call on each Student.
            IEnumerable<ContactInfo> studentQuery3 =
                from student in app.students
                where student.ID > 111                select student.GetContactInfo(app, student.ID);
            Console.WriteLine( "\r\n studentQuery3: select  
range_variable.Method" );
            foreach (ContactInfo ci in studentQuery3)
            {
                Console.WriteLine(ci.ToString());
            }
            // Produce a filtered sequence of ints from
            // the internal array inside each Student.
            IEnumerable< int> studentQuery4 =
                from student in app.students
                where student.ID > 111
                select student.Scores[ 0];
            Console.WriteLine( "\r\n studentQuery4: select  
range_variable[index]" );
            foreach (int i in studentQuery4)
            {
                Console.WriteLine( "First score = {0}" , i);
            }
            // Produce a filtered sequence of doubles
            // that are the result of an expression.
            IEnumerable< double> studentQuery5 =
                from student in app.students
                where student.ID > 111
                select student.Scores[ 0] * 1.1;
            Console.WriteLine( "\r\n studentQuery5: select expression" );
            foreach (double d in studentQuery5)
            {
                Console.WriteLine( "Adjusted first score = {0}" , d);
            }
            // Produce a filtered sequence of doubles that are
            // the result of a method call.
            IEnumerable< double> studentQuery6 =
                from student in app.students
                where student.ID > 111
                select student.Scores.Average();
            Console.WriteLine( "\r\n studentQuery6: select expression2" );
            foreach (double d in studentQuery6)
            {
                Console.WriteLine( "Average = {0}" , d);
            }
            // Produce a filtered sequence of anonymous types
            // that contain only two properties from each Student.
            var studentQuery7 =
                from student in app.students
                where student.ID > 111
                select new { student.First, student.Last };            Console.WriteLine( "\r\n studentQuery7: select new anonymous  
type");
            foreach (var item in studentQuery7)
            {
                Console.WriteLine( "{0}, {1}" , item.Last, item.First);
            }
            // Produce a filtered sequence of named objects that contain
            // a method return value and a property from each Student.
            // Use named types if you need to pass the query variable
            // across a method boundary.
            IEnumerable<ScoreInfo> studentQuery8 =
                from student in app.students
                where student.ID > 111
                select new ScoreInfo
                {
                    Average = student.Scores.Average(),
                    ID = student.ID
                };
            Console.WriteLine( "\r\n studentQuery8: select new named type" );
            foreach (ScoreInfo si in studentQuery8)
            {
                Console.WriteLine( "ID = {0}, Average = {1}" , si.ID,  
si.Average);
            }
            // Produce a filtered sequence of students who appear on a  
contact list
            // and whose average is greater than 85.
            IEnumerable<ContactInfo> studentQuery9 =
                from student in app.students
                where student.Scores.Average() > 85
                join ci in app.contactList on student.ID equals ci.ID
                select ci;
            Console.WriteLine( "\r\n studentQuery9: select result of join  
clause");
            foreach (ContactInfo ci in studentQuery9)
            {
                Console.WriteLine( "ID = {0}, Email = {1}" , ci.ID, ci.Email);
            }
            // Keep the console window open in debug mode
            Console.WriteLine( "Press any key to exit." );
            Console.ReadKey();
            }
        }
    /* Output
        Query1: select range_variable
        Claire O'Donnell:112
        Sven Mortensen:113
        Cesar Garcia:114As shown in studentQuery8 in the previous example, sometimes you might want the
elements of the returned sequence to contain only a subset of the properties of the
source elements. By keeping the returned sequence as small as possible you can reduce
the memory requirements and increase the speed of the execution of the query. Y ou can
accomplish this by creating an anonymous type in the select clause and using an
object initializer to initialize it with the appropriate properties from the source element.
For an example of how to do this, see Object and Collection Initializers .        studentQuery2: select range_variable.Property
        O'Donnell
        Mortensen
        Garcia
        studentQuery3: select range_variable.Method
        ClaireO@Contoso.com,206-555-0298
        SvenMort@Contoso.com,206-555-1130
        CesarGar@Contoso.com,206-555-0521
        studentQuery4: select range_variable[index]
        First score = 75
        First score = 88
        First score = 97
        studentQuery5: select expression
        Adjusted first score = 82.5
        Adjusted first score = 96.8
        Adjusted first score = 106.7
        studentQuery6: select expression2
        Average = 72.25
        Average = 84.5
        Average = 88.25
        studentQuery7: select new anonymous type
        O'Donnell, Claire
        Mortensen, Sven
        Garcia, Cesar
        studentQuery8: select new named type
        ID = 112, Average = 72.25
        ID = 113, Average = 84.5
        ID = 114, Average = 88.25
        studentQuery9: select result of join clause
        ID = 114, Email = CesarGar@Contoso.com
*/
RemarksAt compile time, the select clause is translated to a method call to the Select  standard
query operator.
C# Reference
Query K eywords (LINQ)
from clause
partial (Method) (C# R eference)
Anonymous T ypes
LINQ in C#See alsogroup clause (C# Reference)
Article •09/15/2021
The group clause returns a sequence of IGrouping<TK ey,TElement>  objects that contain
zero or more items that match the key value for the group. For example, you can group
a sequence of strings according to the first letter in each string. In this case, the first
letter is the key and has a type char, and is stored in the Key property of each
IGrouping<TK ey,TElement>  object. The compiler infers the type of the key.
You can end a query expression with a group clause, as shown in the following example:
C#
If you want to perform additional query operations on each group, you can specify a
temporary identifier by using the into contextual keyword. When you use into, you
must continue with the query, and eventually end it with either a select statement or
another group clause, as shown in the following excerpt:
C#
More complete examples of the use of group with and without into are provided in the
Example section of this article.
Because the IGrouping<TK ey,TElement>  objects produced by a group query are
essentially a list of lists, you must use a nested foreach  loop to access the items in each
group. The outer loop iterates over the group keys, and the inner loop iterates over each// Query variable is an IEnumerable<IGrouping<char, Student>>  
var studentQuery1 =  
    from student in students  
    group student by student.Last[ 0]; 
// Group students by the first letter of their last name  
// Query variable is an IEnumerable<IGrouping<char, Student>>  
var studentQuery2 =  
    from student in students  
    group student by student.Last[ 0] into g 
    orderby g.Key 
    select g; 
Enum erating the results of a group queryitem in the group itself. A group may have a key but no elements. The following is the
foreach loop that executes the query in the previous code examples:
C#
Group keys can be any type, such as a string, a built-in numeric type, or a user-defined
named type or anonymous type.
The previous code examples used a char. A string key could easily have been specified
instead, for example the complete last name:
C#
The following example shows the use of a bool value for a key to divide the results into
two groups. Note that the value is produced by a sub-expression in the group clause.
C#// Iterate group items with a nested foreach. This IGrouping encapsulates  
// a sequence of Student objects, and a Key of type char.  
// For convenience, var can also be used in the foreach statement.  
foreach (IGrouping< char, Student> studentGroup in studentQuery2)  
{ 
     Console.WriteLine(studentGroup.Key);  
     // Explicit type for student could also be used here.  
     foreach (var student in studentGroup)  
     { 
         Console.WriteLine( "   {0}, {1}" , student.Last, student.First);  
     } 
 } 
Key types
Grouping by string
// Same as previous example except we use the entire last name as a key.  
// Query variable is an IEnumerable<IGrouping<string, Student>>  
var studentQuery3 =  
    from student in students  
    group student by student.Last;  
Grouping by bool
class GroupSample1  
{     // The element type of the data source.  
    public class Student 
    { 
        public string First { get; set; } 
        public string Last { get; set; } 
        public int ID { get; set; } 
        public List<int> Scores;  
    } 
    public static List<Student> GetStudents () 
    { 
        // Use a collection initializer to create the data source. Note that  
each element  
        //  in the list contains an inner sequence of scores.  
        List<Student> students = new List<Student>  
        {  
           new Student {First= "Svetlana" , Last="Omelchenko" , ID=111, Scores=  
new List<int> {97, 72, 81, 60}}, 
           new Student {First= "Claire" , Last="O'Donnell" , ID=112, Scores=  
new List<int> {75, 84, 91, 39}}, 
           new Student {First= "Sven", Last="Mortensen" , ID=113, Scores= new 
List<int> {99, 89, 91, 95}}, 
           new Student {First= "Cesar", Last="Garcia" , ID=114, Scores= new 
List<int> {72, 81, 65, 84}}, 
           new Student {First= "Debra", Last="Garcia" , ID=115, Scores= new 
List<int> {97, 89, 85, 82}} 
        };  
        return students;  
    } 
    static void Main() 
    { 
        // Obtain the data source.  
        List<Student> students = GetStudents();  
        // Group by true or false.  
        // Query variable is an IEnumerable<IGrouping<bool, Student>>  
        var booleanGroupQuery =  
            from student in students  
            group student by student.Scores.Average() >= 80; //pass or fail!  
        // Execute the query and access items in each group  
        foreach (var studentGroup in booleanGroupQuery)  
        {  
            Console.WriteLine(studentGroup.Key == true ? "High averages"  : 
"Low averages" ); 
            foreach (var student in studentGroup)  
            {  
                Console.WriteLine( "   {0}, {1}:{2}" , student.Last,  
student.First, student.Scores.Average());  
            }  
        }  
        // Keep the console window open in debug mode.  The next example uses an expression to create numeric group keys that represent a
percentile range. Note the use of let as a convenient location to store a method call
result, so that you don't have to call the method two times in the group clause. For
more information about how to safely use methods in query expressions, see Handle
exceptions in query expressions .
C#        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
  Low averages  
   Omelchenko, Svetlana:77.5  
   O'Donnell, Claire:72.25  
   Garcia, Cesar:75.5  
  High averages  
   Mortensen, Sven:93.5  
   Garcia, Debra:88.25  
*/ 
Grouping by numeric range
class GroupSample2  
{ 
    // The element type of the data source.  
    public class Student 
    { 
        public string First { get; set; } 
        public string Last { get; set; } 
        public int ID { get; set; } 
        public List<int> Scores;  
    } 
    public static List<Student> GetStudents () 
    { 
        // Use a collection initializer to create the data source. Note that  
each element  
        //  in the list contains an inner sequence of scores.  
        List<Student> students = new List<Student>  
        {  
           new Student {First= "Svetlana" , Last="Omelchenko" , ID=111, Scores=  
new List<int> {97, 72, 81, 60}}, 
           new Student {First= "Claire" , Last="O'Donnell" , ID=112, Scores=  
new List<int> {75, 84, 91, 39}}, 
           new Student {First= "Sven", Last="Mortensen" , ID=113, Scores= new 
List<int> {99, 89, 91, 95}}, 
           new Student {First= "Cesar", Last="Garcia" , ID=114, Scores= new 
List<int> {72, 81, 65, 84}},            new Student {First= "Debra", Last="Garcia" , ID=115, Scores= new 
List<int> {97, 89, 85, 82}} 
        };  
        return students;  
    } 
    // This method groups students into percentile ranges based on their  
    // grade average. The Average method returns a double, so to produce a  
whole 
    // number it is necessary to cast to int before dividing by 10.  
    static void Main() 
    { 
        // Obtain the data source.  
        List<Student> students = GetStudents();  
        // Write the query.  
        var studentQuery =  
            from student in students  
            let avg = ( int)student.Scores.Average()  
            group student by (avg / 10) into g 
            orderby g.Key 
            select g; 
        // Execute the query.  
        foreach (var studentGroup in studentQuery)  
        {  
            int temp = studentGroup.Key * 10; 
            Console.WriteLine( "Students with an average between {0} and  
{1}", temp, temp + 10); 
            foreach (var student in studentGroup)  
            {  
                Console.WriteLine( "   {0}, {1}:{2}" , student.Last,  
student.First, student.Scores.Average());  
            }  
        }  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
     Students with an average between 70 and 80  
       Omelchenko, Svetlana:77.5  
       O'Donnell, Claire:72.25  
       Garcia, Cesar:75.5  
     Students with an average between 80 and 90  
       Garcia, Debra:88.25  
     Students with an average between 90 and 100  
       Mortensen, Sven:93.5  
 */ Use a composite key when you want to group elements according to more than one
key. Y ou create a composite key by using an anonymous type or a named type to hold
the key element. In the following example, assume that a class Person has been
declared with members named surname and city. The group clause causes a separate
group to be created for each set of persons with the same last name and the same city.
C#
Use a named type if you must pass the query variable to another method. Create a
special class using auto-implemented properties for the keys, and then override the
Equals  and GetHashCode  methods. Y ou can also use a struct, in which case you do not
strictly have to override those methods. For more information see How to implement a
lightweight class with auto-implemented properties  and How to query for duplicate files
in a directory tree . The latter article has a code example that demonstrates how to use a
composite key with a named type.
The following example shows the standard pattern for ordering source data into groups
when no additional query logic is applied to the groups. This is called a grouping
without a continuation. The elements in an array of strings are grouped according to
their first letter. The result of the query is an IGrouping<TK ey,TElement>  type that
contains a public Key property of type char and an IEnumerable<T>  collection that
contains each item in the grouping.
The result of a group clause is a sequence of sequences. Therefore, to access the
individual elements within each returned group, use a nested foreach loop inside the
loop that iterates the group keys, as shown in the following example.
C#Grouping by composite keys
group person by new {name = person.surname, city = person.city};  
Example 1
class GroupExample1  
{ 
    static void Main() 
    { 
        // Create a data source.  
        string[] words = { "blueberry" , "chimpanzee" , "abacus" , "banana" , 
"apple", "cheese"  }; This example shows how to perform additional logic on the groups after you have
created them, by using a continuation  with into. For more information, see into. The
following example queries each group to select only those whose key value is a vowel.
C#        // Create the query.  
        var wordGroups =  
            from w in words 
            group w by w[0]; 
        // Execute the query.  
        foreach (var wordGroup in wordGroups)  
        {  
            Console.WriteLine( "Words that start with the letter '{0}':" , 
wordGroup.Key);  
            foreach (var word in wordGroup)  
            {  
                Console.WriteLine(word);  
            }  
        }  
        // Keep the console window open in debug mode  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
      Words that start with the letter 'b':  
        blueberry  
        banana  
      Words that start with the letter 'c':  
        chimpanzee  
        cheese  
      Words that start with the letter 'a':  
        abacus  
        apple  
     */ 
Example 2
class GroupClauseExample2  
{ 
    static void Main() 
    { 
        // Create the data source.  
        string[] words2 = { "blueberry" , "chimpanzee" , "abacus" , "banana" , 
"apple", "cheese" , "elephant" , "umbrella" , "anteater"  };
        // Create the query.  
        var wordGroups2 =  At compile time, group clauses are translated into calls to the GroupBy  method.
IGrouping<TK ey,TElement>
GroupBy
ThenBy
ThenByDescending
Query K eywords
Language Integrated Query (LINQ)
Create a nested group
Group query results            from w in words2 
            group w by w[0] into grps 
            where (grps.Key == 'a' || grps.Key == 'e' || grps.Key == 'i' 
                   || grps.Key == 'o' || grps.Key == 'u') 
            select grps; 
        // Execute the query.  
        foreach (var wordGroup in wordGroups2)  
        {  
            Console.WriteLine( "Groups that start with a vowel: {0}" , 
wordGroup.Key);  
            foreach (var word in wordGroup)  
            {  
                Console.WriteLine( "   {0}" , word);  
            }  
        }  
        // Keep the console window open in debug mode  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
    Groups that start with a vowel: a  
        abacus  
        apple  
        anteater  
    Groups that start with a vowel: e  
        elephant  
    Groups that start with a vowel: u  
        umbrella  
*/ 
Remarks
See alsoPerform a subquery on a grouping operationinto (C# Reference)
Article •09/15/2021
The into contextual keyword can be used to create a temporary identifier to store the
results of a group , join or select  clause into a new identifier. This identifier can itself be a
generator for additional query commands. When used in a group or select clause, the
use of the new identifier is sometimes referred to as a continuation .
The following example shows the use of the into keyword to enable a temporary
identifier fruitGroup which has an inferred type of IGrouping. By using the identifier,
you can invoke the Count  method on each group and select only those groups that
contain two or more words.
C#Example
class IntoSample1  
{ 
    static void Main() 
    { 
        // Create a data source.  
        string[] words = { "apples" , "blueberries" , "oranges" , "bananas" , 
"apricots" }; 
        // Create the query.  
        var wordGroups1 =  
            from w in words 
            group w by w[0] into fruitGroup  
            where fruitGroup.Count() >= 2 
            select new { FirstLetter = fruitGroup.Key, Words =  
fruitGroup.Count() };  
        // Execute the query. Note that we only iterate over the groups,  
        // not the items in each group  
        foreach (var item in wordGroups1)  
        {  
            Console.WriteLine( " {0} has {1} elements." , item.FirstLetter,  
item.Words);  
        }  
        // Keep the console window open in debug mode  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} The use of into in a group clause is only necessary when you want to perform
additional query operations on each group. For more information, see group clause .
For an example of the use of into in a join clause, see join clause .
Query K eywords (LINQ)
LINQ in C#
group clause/* Output:  
   a has 2 elements.  
   b has 2 elements.  
*/ 
See alsoorderby clause (C# Reference)
Article •09/15/2021
In a query expression, the orderby clause causes the returned sequence or subsequence
(group) to be sorted in either ascending or descending order. Multiple keys can be
specified in order to perform one or more secondary sort operations. The sorting is
performed by the default comparer for the type of the element. The default sort order is
ascending. Y ou can also specify a custom comparer. However, it is only available by
using method-based syntax. For more information, see Sorting Data .
In the following example, the first query sorts the words in alphabetical order starting
from A, and second query sorts the same words in descending order. (The ascending
keyword is the default sort value and can be omitted.)
C#Example 1
class OrderbySample1
{
    static void Main()
    {
        // Create a delicious data source.
        string[] fruits = { "cherry" , "apple", "blueberry"  };
        // Query for ascending sort.
        IEnumerable< string> sortAscendingQuery =
            from fruit in fruits
            orderby fruit //"ascending" is default
            select fruit;
        // Query for descending sort.
        IEnumerable< string> sortDescendingQuery =
            from w in fruits
            orderby w descending
            select w;
        // Execute the query.
        Console.WriteLine( "Ascending:" );
        foreach (string s in sortAscendingQuery)
        {
            Console.WriteLine(s);
        }
        // Execute the query.
        Console.WriteLine(Environment.NewLine + "Descending:" );
        foreach (string s in sortDescendingQuery)The following example performs a primary sort on the students' last names, and then a
secondary sort on their first names.
C#        {
            Console.WriteLine(s);
        }
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
Ascending:
apple
blueberry
cherry
Descending:
cherry
blueberry
apple
*/
Example 2
class OrderbySample2
{
    // The element type of the data source.
    public class Student
    {
        public string First { get; set; }
        public string Last { get; set; }
        public int ID { get; set; }
    }
    public static List<Student> GetStudents ()
    {
        // Use a collection initializer to create the data source. Note that  
each element
        //  in the list contains an inner sequence of scores.
        List<Student> students = new List<Student>
        {
           new Student {First= "Svetlana" , Last="Omelchenko" , ID=111},
           new Student {First= "Claire" , Last="O'Donnell" , ID=112},
           new Student {First= "Sven", Last="Mortensen" , ID=113},
           new Student {First= "Cesar", Last="Garcia" , ID=114},
           new Student {First= "Debra", Last="Garcia" , ID=115}
        };        return students;
    }
    static void Main(string[] args)
    {
        // Create the data source.
        List<Student> students = GetStudents();
        // Create the query.
        IEnumerable<Student> sortedStudents =
            from student in students
            orderby student.Last ascending , student.First ascending
            select student;
        // Execute the query.
        Console.WriteLine( "sortedStudents:" );
        foreach (Student student in sortedStudents)
            Console.WriteLine(student.Last + " " + student.First);
        // Now create groups and sort the groups. The query first sorts the  
names
        // of all students so that they will be in alphabetical order after  
they are
        // grouped. The second orderby sorts the group keys in alpha order.
        var sortedGroups =
            from student in students
            orderby student.Last, student.First
            group student by student.Last[ 0] into newGroup
            orderby newGroup.Key
            select newGroup;
        // Execute the query.
        Console.WriteLine(Environment.NewLine + "sortedGroups:" );
        foreach (var studentGroup in sortedGroups)
        {
            Console.WriteLine(studentGroup.Key);
            foreach (var student in studentGroup)
            {
                Console.WriteLine( "   {0}, {1}" , student.Last,  
student.First);
            }
        }
        // Keep the console window open in debug mode
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
sortedStudents:
Garcia Cesar
Garcia Debra
Mortensen Sven
O'Donnell Claire
Omelchenko SvetlanaAt compile time, the orderby clause is translated to a call to the OrderBy  method.
Multiple keys in the orderby clause translate to ThenBy  method calls.
C# Reference
Query K eywords (LINQ)
LINQ in C#
group clause
Language Integrated Query (LINQ)sortedGroups:
G
   Garcia, Cesar
   Garcia, Debra
M
   Mortensen, Sven
O
   O'Donnell, Claire
   Omelchenko, Svetlana
*/
Remarks
See alsojoin clause (C# Reference)
Article •04/28/2023
The join clause is useful for associating elements from different source sequences that
have no direct relationship in the object model. The only requirement is that the
elements in each source share some value that can be compared for equality. For
example, a food distributor might have a list of suppliers of a certain product, and a list
of buyers. A join clause can be used, for example, to create a list of the suppliers and
buyers of that product who are all in the same specified region.
A join clause takes two source sequences as input. The elements in each sequence
must either be or contain a property that can be compared to a corresponding property
in the other sequence. The join clause compares the specified keys for equality by
using the special equals keyword. All joins performed by the join clause are equijoins.
The shape of the output of a join clause depends on the specific type of join you are
performing. The following are three most common join types:
Inner join
Group join
Left outer join
The following example shows a simple inner equijoin. This query produces a flat
sequence of "product name / category" pairs. The same category string will appear in
multiple elements. If an element from categories has no matching products, that
category will not appear in the results.
C#
For more information, see Perform inner joins .Inner join
var innerJoinQuery =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID  
    select new { ProductName = prod.Name, Category = category.Name };  
//produces flat sequence  
Group joinA join clause with an into expression is called a group join.
C#
A group join produces a hierarchical result sequence, which associates elements in the
left source sequence with one or more matching elements in the right side source
sequence. A group join has no equivalent in relational terms; it is essentially a sequence
of object arrays.
If no elements from the right source sequence are found to match an element in the left
source, the join clause will produce an empty array for that item. Therefore, the group
join is still basically an inner-equijoin except that the result sequence is organized into
groups.
If you just select the results of a group join, you can access the items, but you cannot
identify the key that they match on. Therefore, it is generally more useful to select the
results of the group join into a new type that also has the key name, as shown in the
previous example.
You can also, of course, use the result of a group join as the generator of another
subquery:
C#
For more information, see Perform grouped joins .
In a left outer join, all the elements in the left source sequence are returned, even if no
matching elements are in the right sequence. T o perform a left outer join in LINQ, usevar innerGroupJoinQuery =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
    select new { CategoryName = category.Name, Products = prodGroup };  
var innerGroupJoinQuery2 =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
    from prod2 in prodGroup  
    where prod2.UnitPrice > 2.50M 
    select prod2; 
Left outer jointhe DefaultIfEmpty method in combination with a group join to specify a default right-
side element to produce if a left-side element has no matches. Y ou can use null as the
default value for any reference type, or you can specify a user-defined default type. In
the following example, a user-defined default type is shown:
C#
For more information, see Perform left outer joins .
A join clause performs an equijoin. In other words, you can only base matches on the
equality of two keys. Other types of comparisons such as "greater than" or "not equals"
are not supported. T o make clear that all joins are equijoins, the join clause uses the
equals keyword instead of the == operator. The equals keyword can only be used in a
join clause and it differs from the == operator in some important ways. When
comparing strings, equals has an overload to compare by value and the operator ==
uses reference equality. When both sides of comparison have identical string variables,
equals and == reach the same result: true. That's because, when a program declares
two or more equivalent string variables, the compiler stores all of them in the same
location. This is known as interning. Another important difference is the null comparison:
null equals null is evaluated as false with equals operator, instead of == operator that
evaluates it as true. Lastly, the scoping behavior is different: with equals, the left key
consumes the outer source sequence, and the right key consumes the inner source. The
outer source is only in scope on the left side of equals and the inner source sequence is
only in scope on the right side.
You can perform non-equijoins, cross joins, and other custom join operations by using
multiple from clauses to introduce new sequences independently into a query. For more
information, see Perform custom join operations .var leftOuterJoinQuery =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
    from item in prodGroup.DefaultIfEmpty( new Product { Name = String.Empty,  
CategoryID = 0 }) 
    select new { CatName = category.Name, ProdName = item.Name };  
The equals operator
Non-equijoinsIn a LINQ query expression, join operations are performed on object collections. Object
collections cannot be "joined" in exactly the same way as two relational tables. In LINQ,
explicit join clauses are only required when two source sequences are not tied by any
relationship. When working with LINQ to SQL, foreign key tables are represented in the
object model as properties of the primary table. For example, in the Northwind
database, the Customer table has a foreign key relationship with the Orders table. When
you map the tables to the object model, the Customer class has an Orders property that
contains the collection of Orders associated with that Customer. In effect, the join has
already been done for you.
For more information about querying across related tables in the context of LINQ to
SQL, see How to: Map Database R elationships .
You can test for equality of multiple values by using a composite key. For more
information, see Join by using composite keys . Composite keys can be also used in a
group clause.
The following example compares the results of an inner join, a group join, and a left
outer join on the same data sources by using the same matching keys. Some extra code
is added to these examples to clarify the results in the console display.
C#Joins on object collections vs. relational tables
Composite keys
Example
class JoinDemonstration  
{ 
    #region Data 
    class Product 
    { 
        public string Name { get; set; } 
        public int CategoryID { get; set; } 
    } 
    class Category  
    { 
        public string Name { get; set; } 
        public int ID { get; set; } 
    }     // Specify the first data source.  
    List<Category> categories = new List<Category>()  
    { 
        new Category {Name= "Beverages" , ID=001}, 
        new Category {Name= "Condiments" , ID=002}, 
        new Category {Name= "Vegetables" , ID=003}, 
        new Category {Name= "Grains" , ID=004}, 
        new Category {Name= "Fruit", ID=005} 
    }; 
    // Specify the second data source.  
    List<Product> products = new List<Product>()  
   { 
      new Product {Name= "Cola",  CategoryID= 001}, 
      new Product {Name= "Tea",  CategoryID= 001}, 
      new Product {Name= "Mustard" , CategoryID= 002}, 
      new Product {Name= "Pickles" , CategoryID= 002}, 
      new Product {Name= "Carrots" , CategoryID= 003}, 
      new Product {Name= "Bok Choy" , CategoryID= 003}, 
      new Product {Name= "Peaches" , CategoryID= 005}, 
      new Product {Name= "Melons" , CategoryID= 005}, 
    }; 
    #endregion  
    static void Main(string[] args) 
    { 
        JoinDemonstration app = new JoinDemonstration();  
        app.InnerJoin();  
        app.GroupJoin();  
        app.GroupInnerJoin();  
        app.GroupJoin3();  
        app.LeftOuterJoin();  
        app.LeftOuterJoin2();  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
    void InnerJoin () 
    { 
        // Create the query that selects  
        // a property from each element.  
        var innerJoinQuery =  
           from category in categories  
           join prod in products on category.ID equals prod.CategoryID  
           select new { Category = category.ID, Product = prod.Name };  
        Console.WriteLine( "InnerJoin:" ); 
        // Execute the query. Access results  
        // with a simple foreach statement.  
        foreach (var item in innerJoinQuery)  
        {  
            Console.WriteLine( "{0,-10}{1}" , item.Product, item.Category);          }  
        Console.WriteLine( "InnerJoin: {0} items in 1 group." , 
innerJoinQuery.Count());  
        Console.WriteLine(System.Environment.NewLine);  
    } 
    void GroupJoin () 
    { 
        // This is a demonstration query to show the output  
        // of a "raw" group join. A more typical group join  
        // is shown in the GroupInnerJoin method.  
        var groupJoinQuery =  
           from category in categories  
           join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
           select prodGroup;  
        // Store the count of total items (for demonstration only).  
        int totalItems = 0; 
        Console.WriteLine( "Simple GroupJoin:" ); 
        // A nested foreach statement is required to access group items.  
        foreach (var prodGrouping in groupJoinQuery)  
        {  
            Console.WriteLine( "Group:" ); 
            foreach (var item in prodGrouping)  
            {  
                totalItems++;  
                Console.WriteLine( "   {0,-10}{1}" , item.Name,  
item.CategoryID);  
            }  
        }  
        Console.WriteLine( "Unshaped GroupJoin: {0} items in {1} unnamed  
groups", totalItems, groupJoinQuery.Count());  
        Console.WriteLine(System.Environment.NewLine);  
    } 
    void GroupInnerJoin () 
    { 
        var groupJoinQuery2 =  
            from category in categories  
            orderby category.ID  
            join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
            select new 
            {  
                Category = category.Name,  
                Products = from prod2 in prodGroup  
                           orderby prod2.Name  
                           select prod2 
            };  
        //Console.WriteLine("GroupInnerJoin:");  
        int totalItems = 0;         Console.WriteLine( "GroupInnerJoin:" ); 
        foreach (var productGroup in groupJoinQuery2)  
        {  
            Console.WriteLine(productGroup.Category);  
            foreach (var prodItem in productGroup.Products)  
            {  
                totalItems++;  
                Console.WriteLine( "  {0,-10} {1}" , prodItem.Name,  
prodItem.CategoryID);  
            }  
        }  
        Console.WriteLine( "GroupInnerJoin: {0} items in {1} named groups" , 
totalItems, groupJoinQuery2.Count());  
        Console.WriteLine(System.Environment.NewLine);  
    } 
    void GroupJoin3 () 
    { 
        var groupJoinQuery3 =  
            from category in categories  
            join product in products on category.ID equals 
product.CategoryID into prodGroup  
            from prod in prodGroup  
            orderby prod.CategoryID  
            select new { Category = prod.CategoryID, ProductName = prod.Name  
}; 
        //Console.WriteLine("GroupInnerJoin:");  
        int totalItems = 0; 
        Console.WriteLine( "GroupJoin3:" ); 
        foreach (var item in groupJoinQuery3)  
        {  
            totalItems++;  
            Console.WriteLine( "   {0}:{1}" , item.ProductName,  
item.Category);  
        }  
        Console.WriteLine( "GroupJoin3: {0} items in 1 group" , totalItems);  
        Console.WriteLine(System.Environment.NewLine);  
    } 
    void LeftOuterJoin () 
    { 
        // Create the query.  
        var leftOuterQuery =  
           from category in categories  
           join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
           select prodGroup.DefaultIfEmpty( new Product() { Name =  
"Nothing!" , CategoryID = category.ID });  
        // Store the count of total items (for demonstration only).          int totalItems = 0; 
        Console.WriteLine( "Left Outer Join:" ); 
        // A nested foreach statement  is required to access group items  
        foreach (var prodGrouping in leftOuterQuery)  
        {  
            Console.WriteLine( "Group:" ); 
            foreach (var item in prodGrouping)  
            {  
                totalItems++;  
                Console.WriteLine( "  {0,-10}{1}" , item.Name,  
item.CategoryID);  
            }  
        }  
        Console.WriteLine( "LeftOuterJoin: {0} items in {1} groups" , 
totalItems, leftOuterQuery.Count());  
        Console.WriteLine(System.Environment.NewLine);  
    } 
    void LeftOuterJoin2 () 
    { 
        // Create the query.  
        var leftOuterQuery2 =  
           from category in categories  
           join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
           from item in prodGroup.DefaultIfEmpty()  
           select new { Name = item == null ? "Nothing!"  : item.Name,  
CategoryID = category.ID };  
        Console.WriteLine( "LeftOuterJoin2: {0} items in 1 group" , 
leftOuterQuery2.Count());  
        // Store the count of total items  
        int totalItems = 0; 
        Console.WriteLine( "Left Outer Join 2:" ); 
        // Groups have been flattened.  
        foreach (var item in leftOuterQuery2)  
        {  
            totalItems++;  
            Console.WriteLine( "{0,-10}{1}" , item.Name, item.CategoryID);  
        }  
        Console.WriteLine( "LeftOuterJoin2: {0} items in 1 group" , 
totalItems);  
    } 
} 
/*Output:  
InnerJoin:  
Cola      1  
Tea       1  
Mustard   2  
Pickles   2  Carrots   3  
Bok Choy  3  
Peaches   5  
Melons    5  
InnerJoin: 8 items in 1 group.  
Unshaped GroupJoin:  
Group: 
    Cola      1  
    Tea       1  
Group: 
    Mustard   2  
    Pickles   2  
Group: 
    Carrots   3  
    Bok Choy  3  
Group: 
Group: 
    Peaches   5  
    Melons    5  
Unshaped GroupJoin: 8 items in 5 unnamed groups  
GroupInnerJoin:  
Beverages  
    Cola       1  
    Tea        1  
Condiments  
    Mustard    2  
    Pickles    2  
Vegetables  
    Bok Choy   3  
    Carrots    3  
Grains 
Fruit 
    Melons     5  
    Peaches    5  
GroupInnerJoin: 8 items in 5 named groups  
GroupJoin3:  
    Cola:1  
    Tea:1  
    Mustard:2  
    Pickles:2  
    Carrots:3  
    Bok Choy:3  
    Peaches:5  
    Melons:5  
GroupJoin3: 8 items in 1 group  
Left Outer Join:  
Group: A join clause that is not followed by into is translated into a Join method call. A join
clause that is followed by into is translated to a GroupJoin  method call.
Query K eywords (LINQ)
Language Integrated Query (LINQ)
Join Operations
group clause
Perform left outer joins
Perform inner joins
Perform grouped joins
Order the results of a join clause
Join by using composite keys    Cola      1  
    Tea       1  
Group: 
    Mustard   2  
    Pickles   2  
Group: 
    Carrots   3  
    Bok Choy  3  
Group: 
    Nothing!  4  
Group: 
    Peaches   5  
    Melons    5  
LeftOuterJoin: 9 items in 5 groups  
LeftOuterJoin2: 9 items in 1 group  
Left Outer Join 2:  
Cola      1  
Tea       1  
Mustard   2  
Pickles   2  
Carrots   3  
Bok Choy  3  
Nothing!  4  
Peaches   5  
Melons    5  
LeftOuterJoin2: 9 items in 1 group  
Press any key to exit.  
*/ 
Remarks
See alsoCompatible database systems for Visual S tudiolet clause (C# Reference)
Article •09/15/2021
In a query expression, it's sometimes useful to store the result of a subexpression in
order to use it in subsequent clauses. Y ou can do this with the let keyword, which
creates a new range variable and initializes it with the result of the expression you
supply. Once initialized with a value, the range variable can't be used to store another
value. However, if the range variable holds a queryable type, it can be queried.
In the following example let is used in two ways:
1. To create an enumerable type that can itself be queried.
2. To enable the query to call ToLower only one time on the range variable word.
Without using let, you would have to call ToLower in each predicate in the where
clause.
C#Example
class LetSample1
{
    static void Main()
    {
        string[] strings =
        {
            "A penny saved is a penny earned." ,
            "The early bird catches the worm." ,
            "The pen is mightier than the sword."
        };
        // Split the sentence into an array of words
        // and select those whose first letter is a vowel.
        var earlyBirdQuery =
            from sentence in strings
            let words = sentence.Split( ' ')
            from word in words
            let w = word.ToLower()
            where w[0] == 'a' || w[0] == 'e'
                || w[0] == 'i' || w[0] == 'o'
                || w[0] == 'u'
            select word;
        // Execute the query.
        foreach (var v in earlyBirdQuery)
        {C# Reference
Query K eywords (LINQ)
LINQ in C#
Language Integrated Query (LINQ)
Handle exceptions in query expressions            Console.WriteLine( "\"{0}\" starts with a vowel" , v);
        }
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
    "A" starts with a vowel
    "is" starts with a vowel
    "a" starts with a vowel
    "earned." starts with a vowel
    "early" starts with a vowel
    "is" starts with a vowel
*/
See alsoascending (C# Reference)
Article •09/15/2021
The ascending contextual keyword is used in the orderby clause  in query expressions to
specify that the sort order is from smallest to largest. Because ascending is the default
sort order, you do not have to specify it.
The following example shows the use of ascending in an orderby clause .
C#
C# Reference
LINQ in C#
descendingExample
IEnumerable< string> sortAscendingQuery =  
    from vegetable in vegetables  
    orderby vegetable ascending  
    select vegetable;  
See alsodescending (C# Reference)
Article •09/15/2021
The descending contextual keyword is used in the orderby clause  in query expressions
to specify that the sort order is from largest to smallest.
The following example shows the use of descending in an orderby clause .
C#
C# Reference
LINQ in C#
ascendingExample
IEnumerable< string> sortDescendingQuery =  
    from vegetable in vegetables  
    orderby vegetable descending  
    select vegetable;  
See alsoon (C# Reference)
Article •09/15/2021
The on contextual keyword is used in the join clause  of a query expression to specify the
join condition.
The following example shows the use of on in a join clause.
C#
C# Reference
Language Integrated Query (LINQ)Example
var innerJoinQuery =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID  
    select new { ProductName = prod.Name, Category = category.Name };  
See alsoequals (C# Reference)
Article •09/15/2021
The equals contextual keyword is used in a join clause in a query expression to
compare the elements of two sequences. For more information, see join clause .
The following example shows the use of the equals keyword in a join clause.
C#
Language Integrated Query (LINQ)Example
var innerJoinQuery =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID  
    select new { ProductName = prod.Name, Category = category.Name };  
See alsoby (C# Reference)
Article •09/15/2021
The by contextual keyword is used in the group clause in a query expression to specify
how the returned items should be grouped. For more information, see group clause .
The following example shows the use of the by contextual keyword in a group clause to
specify that the students should be grouped according to the first letter of the last name
of each student.
C#
LINQ in C#Example
var query = from student in students  
            group student by student.LastName[ 0]; 
See alsoin (C# Reference)
Article •09/15/2021
The in keyword is used in the following contexts:
generic type parameters  in generic interfaces and delegates.
As a parameter modifier , which lets you pass an argument to a method by
reference rather than by value.
foreach  statements.
from clauses  in LINQ query expressions.
join clauses  in LINQ query expressions.
C# Keywords
C# ReferenceSee also
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
 Provide product feedbackC# operators and expressions
Article •03/09/2023
C# provides a number of operators. Many of them are supported by the built-in types
and allow you to perform basic operations with values of those types. Those operators
include the following groups:
Arithmetic operators  that perform arithmetic operations with numeric operands
Comparison operators  that compare numeric operands
Boolean logical operators  that perform logical operations with bool operands
Bitwise and shift operators  that perform bitwise or shift operations with operands
of the integral types
Equality operators  that check if their operands are equal or not
Typically, you can overload  those operators, that is, specify the operator behavior for the
operands of a user-defined type.
The simplest C# expressions are literals (for example, integer  and real numbers) and
names of variables. Y ou can combine them into complex expressions by using operators.
Operator precedence  and associativity  determine the order in which the operations in
an expression are performed. Y ou can use parentheses to change the order of
evaluation imposed by operator precedence and associativity.
In the following code, examples of expressions are at the right-hand side of
assignments:
C#
Typically, an expression produces a result and can be included in another expression. A
void method call is an example of an expression that doesn't produce a result. It can be
used only as a statement , as the following example shows:int a, b, c;
a = 7;
b = a;
c = b++;
b = a + b * c;
c = a >= 100 ? b : c / 10;
a = (int)Math.Sqrt(b * b + c * c);
string s = "String literal" ;
char l = s[s.Length - 1];
var numbers = new List<int>(new[] { 1, 2, 3 });
b = numbers.FindLast(n => n > 1);C#
Here are some other kinds of expressions that C# provides:
Interpolated string expressions  that provide convenient syntax to create formatted
strings:
C#
Lambda expressions  that allow you to create anonymous functions:
C#
Query expressions  that allow you to use query capabilities directly in C#:
C#
You can use an expression body definition  to provide a concise definition for a method,
constructor, property, indexer, or finalizer.Console.WriteLine( "Hello, world!" );
var r = 2.3;
var message = $"The area of a circle with radius {r} is {Math.PI * r *  
r:F3}.";
Console.WriteLine(message);
// Output:
// The area of a circle with radius 2.3 is 16.619.
int[] numbers = { 2, 3, 4, 5 };
var maximumSquare = numbers.Max(x => x * x);
Console.WriteLine(maximumSquare);
// Output:
// 25
var scores = new[] { 90, 97, 78, 68, 85 };
IEnumerable< int> highScoresQuery =
    from score in scores
    where score > 80
    orderby score descending
    select score;
Console.WriteLine( string.Join(" ", highScoresQuery));
// Output:
// 97 90 85
Operator precedenceIn an expression with multiple operators, the operators with higher precedence are
evaluated before the operators with lower precedence. In the following example, the
multiplication is performed first because it has higher precedence than addition:
C#
Use parentheses to change the order of evaluation imposed by operator precedence:
C#
The following table lists the C# operators starting with the highest precedence to the
lowest. The operators within each row have the same precedence.
Operat ors Categor y or name
x.y, f(x), a[i], x?.y, x?[y], x++, x--, x!, new, typeof , checked ,
unchecked , default , nameof , delegate , sizeof , stackalloc , x->yPrimary
+x, -x, !x, ~x, ++x, --x, ^x, (T)x, await , &x, *x, true and false Unary
x..y Range
switch , with switch and with
expressions
x * y, x / y, x % y Multiplicative
x + y , x – y Additive
x << y , x >> y , x >>> y Shift
x < y , x > y , x <= y , x >= y , is, as Relational and type-testing
x == y , x != y Equality
x & y Boolean logical AND  or
bitwise logical AND
x ^ y Boolean logical X OR or
bitwise logical X OR
x | y Boolean logical OR  or
bitwise logical ORvar a = 2 + 2 * 2;
Console.WriteLine(a); //  output: 6
var a = (2 + 2) * 2;
Console.WriteLine(a); //  output: 8Operat ors Categor y or name
x && y Conditional AND
x || y Conditional OR
x ?? y Null-coalescing operator
c ? t : f Conditional operator
x = y , x += y , x -= y , x *= y , x /= y , x %= y , x &= y , x |= y , x ^= y , x
<<= y , x >>= y , x >>>= y , x ??= y , =>Assignment and lambda
declaration
For information about the precedence of logical pattern combinators , see the
Precedence and order of checking of logical patterns  section of the Patterns  article.
When operators have the same precedence, associativity of the operators determines
the order in which the operations are performed:
Left-associativ e operators are evaluated in order from left to right. Except for the
assignment operators  and the null-coalescing operators , all binary operators are
left-associative. For example, a + b - c is evaluated as (a + b) - c.
Right -associativ e operators are evaluated in order from right to left. The
assignment operators, the null-coalescing operators, lambdas, and the conditional
operator ?: are right-associative. For example, x = y = z is evaluated as x = (y =
z).
Use parentheses to change the order of evaluation imposed by operator associativity:
C#Operator associativity
） Impor tant
In an expression of the form P?.A0?.A1, if P is null, neither A0 nor A1 are
evaluated. Similarly, in an expression of the form P?.A0.A1, because A0 isn't
evaluated when P is null, neither is A0.A1. See the C# language specification  for
more details.
int a = 13 / 5 / 2;
int b = 13 / (5 / 2);
Console.WriteLine( $"a = {a}, b = {b}");  // output: a = 1, b = 6Unrelated to operator precedence and associativity, operands in an expression are
evaluated from left to right. The following examples demonstrate the order in which
operators and operands are evaluated:
Expr ession Order o f evaluation
a + b a, b, +
a + b * c a, b, c, *, +
a / b + c * d a, b, /, c, d, *, +
a / (b + c) * d a, b, c, +, /, d, *
Typically, all operator operands are evaluated. However, some operators evaluate
operands conditionally. That is, the value of the leftmost operand of such an operator
defines if (or which) other operands should be evaluated. These operators are the
conditional logical AND ( &&) and OR (||) operators, the null-coalescing operators ?? and
??=, the null-conditional operators ?. and ?[], and the conditional operator ?:. For more
information, see the description of each operator.
For more information, see the following sections of the C# language specification :
Expressions
Operators
C# reference
Operator overloading
Expression treesOperand evaluation
C# language specification
See alsoArithmetic operators (C# reference)
Article •04/08/2023
The following operators perform arithmetic operations with operands of numeric types:
Unary ++ (increment) , -- (decrement) , + (plus) , and - (minus)  operators
Binary * (multiplication) , / (division) , % (remainder) , + (addition) , and - (subtraction)
operators
Those operators are supported by all integral  and floating-point  numeric types.
In the case of integral types, those operators (except the ++ and -- operators) are
defined for the int, uint, long, and ulong types. When operands are of other integral
types (sbyte, byte, short, ushort, or char), their values are converted to the int type,
which is also the result type of an operation. When operands are of different integral or
floating-point types, their values are converted to the closest containing type, if such a
type exists. For more information, see the Numeric promotions  section of the C#
language specification . The ++ and -- operators are defined for all integral and
floating-point numeric types and the char type. The result type of a compound
assignment expression  is the type of the left-hand operand.
The unary increment operator ++ increments its operand by 1. The operand must be a
variable, a property  access, or an indexer  access.
The increment operator is supported in two forms: the postfix increment operator, x++,
and the prefix increment operator, ++x.
The result of x++ is the value of x befor e the operation, as the following example shows:
C#Increment operator ++
Postfix increment operator
int i = 3; 
Console.WriteLine(i);   // output: 3  
Console.WriteLine(i++); // output: 3  
Console.WriteLine(i);   // output: 4  The result of ++x is the value of x after the operation, as the following example shows:
C#
The unary decrement operator -- decrements its operand by 1. The operand must be a
variable, a property  access, or an indexer  access.
The decrement operator is supported in two forms: the postfix decrement operator, x--,
and the prefix decrement operator, --x.
The result of x-- is the value of x befor e the operation, as the following example shows:
C#
The result of --x is the value of x after the operation, as the following example shows:
C#Prefix increment operator
double a = 1.5; 
Console.WriteLine(a);   // output: 1.5  
Console.WriteLine(++a); // output: 2.5  
Console.WriteLine(a);   // output: 2.5  
Decrement operator --
Postfix decrement operator
int i = 3; 
Console.WriteLine(i);   // output: 3  
Console.WriteLine(i--); // output: 3  
Console.WriteLine(i);   // output: 2  
Prefix decrement operator
double a = 1.5; 
Console.WriteLine(a);   // output: 1.5  
Console.WriteLine(--a); // output: 0.5  
Console.WriteLine(a);   // output: 0.5  
Unary plus and minus operatorsThe unary + operator returns the value of its operand. The unary - operator computes
the numeric negation of its operand.
C#
The ulong  type doesn't support the unary - operator.
The multiplication operator * computes the product of its operands:
C#
The unary * operator is the pointer indirection operator .
The division operator / divides its left-hand operand by its right-hand operand.
For the operands of integer types, the result of the / operator is of an integer type and
equals the quotient of the two operands rounded towards zero:
C#Console.WriteLine(+ 4);     // output: 4  
Console.WriteLine( -4);     // output: -4  
Console.WriteLine(-( -4));  // output: 4  
uint a = 5; 
var b = -a;  
Console.WriteLine(b);            // output: -5  
Console.WriteLine(b.GetType());  // output: System.Int64  
Console.WriteLine(- double.NaN);  // output: NaN  
Multip lication operator *
Console.WriteLine( 5 * 2);         // output: 10  
Console.WriteLine( 0.5 * 2.5);     // output: 1.25  
Console.WriteLine( 0.1m * 23.4m);  // output: 2.34  
Division operator /
Integer division
Console.WriteLine( 13 / 5);    // output: 2  
Console.WriteLine( -13 / 5);   // output: -2  To obtain the quotient of the two operands as a floating-point number, use the float,
double, or decimal type:
C#
For the float, double, and decimal types, the result of the / operator is the quotient of
the two operands:
C#
If one of the operands is decimal, another operand can be neither float nor double,
because neither float nor double is implicitly convertible to decimal. You must
explicitly convert the float or double operand to the decimal type. For more
information about conversions between numeric types, see Built-in numeric conversions .
The remainder operator % computes the remainder after dividing its left-hand operand
by its right-hand operand.
For the operands of integer types, the result of a % b is the value produced by a - (a /
b) * b. The sign of the non-zero remainder is the same as the sign of the left-hand
operand, as the following example shows:
C#Console.WriteLine( 13 / -5);   // output: -2  
Console.WriteLine( -13 / -5);  // output: 2  
Console.WriteLine( 13 / 5.0);       // output: 2.6  
int a = 13; 
int b = 5; 
Console.WriteLine(( double)a / b);  // output: 2.6  
Floating-point division
Console.WriteLine( 16.8f / 4.1f);   // output: 4.097561  
Console.WriteLine( 16.8d / 4.1d);   // output: 4.09756097560976  
Console.WriteLine( 16.8m / 4.1m);   // output: 4.0975609756097560975609756098  
Remainder operator %
Integer remainderUse the Math.DivR em method to compute both integer division and remainder results.
For the float and double operands, the result of x % y for the finite x and y is the
value z such that
The sign of z, if non-zero, is the same as the sign of x.
The absolute value of z is the value produced by |x| - n * |y| where n is the
largest possible integer that is less than or equal to |x| / |y| and |x| and |y|
are the absolute values of x and y, respectively.
For information about the behavior of the % operator with non-finite operands, see the
Remainder operator  section of the C# language specification .
For the decimal operands, the remainder operator % is equivalent to the remainder
operator  of the System.Decimal  type.
The following example demonstrates the behavior of the remainder operator with
floating-point operands:
C#Console.WriteLine( 5 % 4);   // output: 1  
Console.WriteLine( 5 % -4);  // output: 1  
Console.WriteLine( -5 % 4);  // output: -1  
Console.WriteLine( -5 % -4); // output: -1  
Floating-point remainder
７ Note
This method of computing the remainder is analogous to that used for integer
operands, but different from the IEEE 754 specification. If you need the remainder
operation that complies with the IEEE 754 specification, use the
Math.IEEER emainder  method.
Console.WriteLine( -5.2f % 2.0f); // output: -1.2  
Console.WriteLine( 5.9 % 3.1);    // output: 2.8  
Console.WriteLine( 5.9m % 3.1m);  // output: 2.8  
Addition operator +The addition operator + computes the sum of its operands:
C#
You can also use the + operator for string concatenation and delegate combination. For
more information, see the + and += operators  article.
The subtraction operator - subtracts its right-hand operand from its left-hand operand:
C#
You can also use the - operator for delegate removal. For more information, see the -
and -= operators  article.
For a binary operator op, a compound assignment expression of the form
C#
is equivalent to
C#
except that x is only evaluated once.
The following example demonstrates the usage of compound assignment with
arithmetic operators:Console.WriteLine( 5 + 4);       // output: 9  
Console.WriteLine( 5 + 4.3);     // output: 9.3  
Console.WriteLine( 5.1m + 4.2m); // output: 9.3  
Subtraction operator -
Console.WriteLine( 47 - 3);      // output: 44  
Console.WriteLine( 5 - 4.3);     // output: 0.7  
Console.WriteLine( 7.5m - 2.3m); // output: 5.2  
Compound assignment
x op= y 
x = x op y  C#
Because of numeric promotions , the result of the op operation might be not implicitly
convertible to the type T of x. In such a case, if op is a predefined operator and the
result of the operation is explicitly convertible to the type T of x, a compound
assignment expression of the form x op= y is equivalent to x = (T)(x op y), except
that x is only evaluated once. The following example demonstrates that behavior:
C#
In the preceding example, value 44 is the result of converting value 300 to the byte
type.int a = 5; 
a += 9; 
Console.WriteLine(a);  // output: 14  
a -= 4; 
Console.WriteLine(a);  // output: 10  
a *= 2; 
Console.WriteLine(a);  // output: 20  
a /= 4; 
Console.WriteLine(a);  // output: 5  
a %= 3; 
Console.WriteLine(a);  // output: 2  
byte a = 200; 
byte b = 100; 
var c = a + b;  
Console.WriteLine(c.GetType());  // output: System.Int32  
Console.WriteLine(c);  // output: 300  
a += b; 
Console.WriteLine(a);  // output: 44  
７ Note
In the check ed ov erflow-checking cont ext, the preceding example throws an
OverflowEx ception . For more information, see the Integer arithmetic ov erflow
section.You also use the += and -= operators to subscribe to and unsubscribe from an event ,
respectively. For more information, see How to subscribe to and unsubscribe from
events .
The following list orders arithmetic operators starting from the highest precedence to
the lowest:
Postfix increment x++ and decrement x-- operators
Prefix increment ++x and decrement --x and unary + and - operators
Multiplicative *, /, and % operators
Additive + and - operators
Binary arithmetic operators are left-associative. That is, operators with the same
precedence level are evaluated from left to right.
Use parentheses, (), to change the order of evaluation imposed by operator
precedence and associativity.
C#
For the complete list of C# operators ordered by precedence level, see the Operator
precedence  section of the C# operators  article.
When the result of an arithmetic operation is outside the range of possible finite values
of the involved numeric type, the behavior of an arithmetic operator depends on the
type of its operands.
Integer division by zero always throws a DivideByZeroException .Operator precedence and associativity
Console.WriteLine( 2 + 2 * 2);   // output: 6  
Console.WriteLine(( 2 + 2) * 2); // output: 8  
Console.WriteLine( 9 / 5 / 2);   // output: 0  
Console.WriteLine( 9 / (5 / 2)); // output: 4  
Arithmetic overflow and division by zero
Integer arithmetic overflowIf integer arithmetic overflow occurs, the overflow-checking context, which can be
checked or unchecked , controls the resulting behavior:
In a checked context, if overflow happens in a constant expression, a compile-time
error occurs. Otherwise, when the operation is performed at run time, an
OverflowException  is thrown.
In an unchecked context, the result is truncated by discarding any high-order bits
that don't fit in the destination type.
Along with the checked and unchecked  statements, you can use the checked and
unchecked operators to control the overflow-checking context, in which an expression is
evaluated:
C#
By default, arithmetic operations occur in an uncheck ed context.
Arithmetic operations with the float and double types never throw an exception. The
result of arithmetic operations with those types can be one of special values that
represent infinity and not-a-number:
C#int a = int.MaxValue;  
int b = 3; 
Console.WriteLine( unchecked (a + b));  // output: -2147483646  
try 
{ 
    int d = checked(a + b);  
} 
catch(OverflowException)  
{ 
    Console.WriteLine( $"Overflow occurred when adding {a} to {b}."); 
} 
Floating-point arithmetic overflow
double a = 1.0 / 0.0; 
Console.WriteLine(a);                    // output: Infinity  
Console.WriteLine( double.IsInfinity(a)); // output: True  
Console.WriteLine( double.MaxValue + double.MaxValue); // output: Infinity  
double b = 0.0 / 0.0; 
Console.WriteLine(b);                // output: NaN  
Console.WriteLine( double.IsNaN(b));  // output: True  For the operands of the decimal type, arithmetic overflow always throws an
OverflowException . Division by zero always throws a DivideByZeroException .
Because of general limitations of the floating-point representation of real numbers and
floating-point arithmetic, round-off errors might occur in calculations with floating-
point types. That is, the produced result of an expression might differ from the expected
mathematical result. The following example demonstrates several such cases:
C#
For more information, see remarks at the System.Double , System.Single , or
System.Decimal  reference pages.
A user-defined type can overload  the unary ( ++, --, +, and -) and binary ( *, /, %, +,
and -) arithmetic operators. When a binary operator is overloaded, the corresponding
compound assignment operator is also implicitly overloaded. A user-defined type can't
explicitly overload a compound assignment operator.
Beginning with C# 11, when you overload an arithmetic operator, you can use the
checked keyword to define the check ed version of that operator. The following example
shows how to do that:
C#Round-off errors
Console.WriteLine( .41f % .2f); // output: 0.00999999  
double a = 0.1; 
double b = 3 * a; 
Console.WriteLine(b == 0.3);   // output: False  
Console.WriteLine(b - 0.3);    // output: 5.55111512312578E-17  
decimal c = 1 / 3.0m; 
decimal d = 3 * c; 
Console.WriteLine(d == 1.0m);  // output: False  
Console.WriteLine(d);          // output: 0.9999999999999999999999999999  
Operator overloadability
User-defined checked operatorsWhen you define a checked operator, you must also define the corresponding operator
without the checked modifier. The checked operator is called in a checked context ; the
operator without the checked modifier is called in an unchecked context . If you only
provide the operator without the checked modifier, it's called in both a checked and
unchecked context.
When you define both versions of an operator, it's expected that their behavior differs
only when the result of an operation is too large to represent in the result type as
follows:
A checked operator throws an OverflowException .
An operator without the checked modifier returns an instance representing a
truncat ed result.
For information about the difference in behavior of the built-in arithmetic operators, see
the Arithmetic overflow and division by zero  section.
You can use the checked modifier only when you overload any of the following
operators:
Unary ++, --, and - operators
Binary *, /, +, and - operators
Explicit conversion operatorspublic record struct Point(int X, int Y) 
{ 
    public static Point operator  checked +(Point left, Point right)  
    { 
        checked  
        {  
            return new Point(left.X + right.X, left.Y + right.Y);  
        }  
    } 
     
    public static Point operator  +(Point left, Point right)  
    { 
        return new Point(left.X + right.X, left.Y + right.Y);  
    } 
} 
７ Note
The overflow-checking context within the body of a checked operator is not
affected by the presence of the checked modifier. The default context is defined by
the value of the CheckForOv erflowUnder flow compiler option. Use the check edFor more information, see the following sections of the C# language specification :
Postfix increment and decrement operators
Prefix increment and decrement operators
Unary plus operator
Unary minus operator
Multiplication operator
Division operator
Remainder operator
Addition operator
Subtraction operator
Compound assignment
The checked and unchecked operators
Numeric promotions
C# reference
C# operators and expressions
System.Math
System.MathF
Numerics in .NETand uncheck ed statements  to explicitly specify the overflow-checking context, as
the example at the beginning of this section demonstrates.
C# language specification
See alsoBoolean logical operators - AND, OR,
NOT, XOR
Article •11/29/2023
The logical Boolean operators perform logical operations with bool operands. The
operators include the unary logical negation ( !), binary logical AND ( &), OR (|), and
exclusive OR ( ^), and the binary conditional logical AND ( &&) and OR ( ||).
Unary ! (logical negation)  operator.
Binary & (logical AND) , | (logical OR) , and ^ (logical exclusive OR)  operators. Those
operators always evaluate both operands.
Binary && (conditional logical AND)  and || (conditional logical OR)  operators.
Those operators evaluate the right-hand operand only if it's necessary.
For operands of the integral numeric types , the &, |, and ^ operators perform bitwise
logical operations. For more information, see Bitwise and shift operators .
The unary prefix ! operator computes logical negation of its operand. That is, it
produces true, if the operand evaluates to false, and false, if the operand evaluates
to true:
C#
The unary postfix ! operator is the null-forgiving operator .
The & operator computes the logical AND of its operands. The result of x & y is true if
both x and y evaluate to true. Otherwise, the result is false.
The & operator always evaluates both operands. When the left-hand operand evaluates
to false, the operation result is false regardless of the value of the right-hand
operand. However, even then, the right-hand operand is evaluated.Logical negation operator !
bool passed = false;
Console.WriteLine(!passed);  // output: True
Console.WriteLine(! true);    // output: False
Logical AND operator &In the following example, the right-hand operand of the & operator is a method call,
which is performed regardless of the value of the left-hand operand:
C#
The conditional logical AND operator  && also computes the logical AND of its operands,
but doesn't evaluate the right-hand operand if the left-hand operand evaluates to
false.
For operands of the integral numeric types , the & operator computes the bitwise logical
AND  of its operands. The unary & operator is the address-of operator .
The ^ operator computes the logical exclusive OR, also known as the logical X OR, of its
operands. The result of x ^ y is true if x evaluates to true and y evaluates to false,
or x evaluates to false and y evaluates to true. Otherwise, the result is false. That is,
for the bool operands, the ^ operator computes the same result as the inequality
operator  !=.
C#bool SecondOperand ()
{
    Console.WriteLine( "Second operand is evaluated." );
    return true;
}
bool a = false & SecondOperand();
Console.WriteLine(a);
// Output:
// Second operand is evaluated.
// False
bool b = true & SecondOperand();
Console.WriteLine(b);
// Output:
// Second operand is evaluated.
// True
Logical exclusive OR operator ^
Console.WriteLine( true ^ true);    // output: False
Console.WriteLine( true ^ false);   // output: True
Console.WriteLine( false ^ true);   // output: True
Console.WriteLine( false ^ false);  // output: FalseFor operands of the integral numeric types , the ^ operator computes the bitwise logical
exclusive OR  of its operands.
The | operator computes the logical OR of its operands. The result of x | y is true if
either x or y evaluates to true. Otherwise, the result is false.
The | operator always evaluates both operands. When the left-hand operand evaluates
to true, the operation result is true regardless of the value of the right-hand operand.
However, even then, the right-hand operand is evaluated.
In the following example, the right-hand operand of the | operator is a method call,
which is performed regardless of the value of the left-hand operand:
C#
The conditional logical OR operator  || also computes the logical OR of its operands,
but doesn't evaluate the right-hand operand if the left-hand operand evaluates to true.
For operands of the integral numeric types , the | operator computes the bitwise logical
OR of its operands.
The conditional logical AND operator &&, also known as the "short-circuiting" logical
AND operator, computes the logical AND of its operands. The result of x && y is true ifLogical OR operator |
bool SecondOperand ()
{
    Console.WriteLine( "Second operand is evaluated." );
    return true;
}
bool a = true | SecondOperand();
Console.WriteLine(a);
// Output:
// Second operand is evaluated.
// True
bool b = false | SecondOperand();
Console.WriteLine(b);
// Output:
// Second operand is evaluated.
// True
Conditional logical AND operator &&both x and y evaluate to true. Otherwise, the result is false. If x evaluates to false,
y isn't evaluated.
In the following example, the right-hand operand of the && operator is a method call,
which isn't performed if the left-hand operand evaluates to false:
C#
The logical AND operator  & also computes the logical AND of its operands, but always
evaluates both operands.
The conditional logical OR operator ||, also known as the "short-circuiting" logical OR
operator, computes the logical OR of its operands. The result of x || y is true if either
x or y evaluates to true. Otherwise, the result is false. If x evaluates to true, y isn't
evaluated.
In the following example, the right-hand operand of the || operator is a method call,
which isn't performed if the left-hand operand evaluates to true:
C#bool SecondOperand ()
{
    Console.WriteLine( "Second operand is evaluated." );
    return true;
}
bool a = false && SecondOperand();
Console.WriteLine(a);
// Output:
// False
bool b = true && SecondOperand();
Console.WriteLine(b);
// Output:
// Second operand is evaluated.
// True
Conditional logical OR operator ||
bool SecondOperand ()
{
    Console.WriteLine( "Second operand is evaluated." );
    return true;
}
bool a = true || SecondOperand();The logical OR operator  | also computes the logical OR of its operands, but always
evaluates both operands.
For bool? operands, the & (logical AND)  and | (logical OR)  operators support the three-
valued logic as follows:
The & operator produces true only if both its operands evaluate to true. If either
x or y evaluates to false, x & y produces false (even if another operand
evaluates to null). Otherwise, the result of x & y is null.
The | operator produces false only if both its operands evaluate to false. If
either x or y evaluates to true, x | y produces true (even if another operand
evaluates to null). Otherwise, the result of x | y is null.
The following table presents that semantics:
x y x&y x|y
true true true true
true false false true
true null null true
false true false true
false false false false
false null false null
null true null true
null false false null
null null null nullConsole.WriteLine(a);
// Output:
// True
bool b = false || SecondOperand();
Console.WriteLine(b);
// Output:
// Second operand is evaluated.
// True
Nullable Boolean logical operatorsThe behavior of those operators differs from the typical operator behavior with nullable
value types. T ypically, an operator that is defined for operands of a value type can be
also used with operands of the corresponding nullable value type. Such an operator
produces null if any of its operands evaluates to null. However, the & and |
operators can produce non-null even if one of the operands evaluates to null. For
more information about the operator behavior with nullable value types, see the Lifted
operators  section of the Nullable value types  article.
You can also use the ! and ^ operators with bool? operands, as the following example
shows:
C#
The conditional logical operators && and || don't support bool? operands.
For a binary operator op, a compound assignment expression of the form
C#
is equivalent to
C#
except that x is only evaluated once.
The &, |, and ^ operators support compound assignment, as the following example
shows:
C#bool? test = null;
Display(!test);         // output: null
Display(test ^ false);  // output: null
Display(test ^ null);   // output: null
Display( true ^ null);   // output: null
void Display(bool? b) => Console.WriteLine(b is null ? "null" : 
b.Value.ToString());
Compound assignment
x op= y
x = x op yThe following list orders logical operators starting from the highest precedence to the
lowest:
Logical negation operator !
Logical AND operator &
Logical exclusive OR operator ^
Logical OR operator |
Conditional logical AND operator &&
Conditional logical OR operator ||
Use parentheses, (), to change the order of evaluation imposed by operator
precedence:
C#bool test = true;
test &= false;
Console.WriteLine(test);  // output: False
test |= true;
Console.WriteLine(test);  // output: True
test ^= false;
Console.WriteLine(test);  // output: True
７ Note
The conditional logical operators && and || don't support compound assignment.
Operator precedence
Console.WriteLine( true | true & false);   // output: True
Console.WriteLine(( true | true) & false); // output: False
bool Operand(string name, bool value)
{
    Console.WriteLine( $"Operand {name} is evaluated." );
    return value;
}
var byDefaultPrecedence = Operand( "A", true) || Operand( "B", true) && 
Operand( "C", false);
Console.WriteLine(byDefaultPrecedence);
// Output:
// Operand A is evaluated.For the complete list of C# operators ordered by precedence level, see the Operator
precedence  section of the C# operators  article.
A user-defined type can overload  the !, &, |, and ^ operators. When a binary operator
is overloaded, the corresponding compound assignment operator is also implicitly
overloaded. A user-defined type can't explicitly overload a compound assignment
operator.
A user-defined type can't overload the conditional logical operators && and ||.
However, if a user-defined type overloads the true and false operators  and the & or |
operator in a certain way, the && or || operation, respectively, can be evaluated for the
operands of that type. For more information, see the User-defined conditional logical
operators  section of the C# language specification .
For more information, see the following sections of the C# language specification :
Logical negation operator
Logical operators
Conditional logical operators
Compound assignment
C# reference
C# operators and expressions
Bitwise and shift operators// True
var changedOrder = (Operand( "A", true) || Operand( "B", true)) && 
Operand( "C", false);
Console.WriteLine(changedOrder);
// Output:
// Operand A is evaluated.
// Operand C is evaluated.
// False
Operator overloadability
C# language specification
See also６ Collaborat e with us on
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
 Provide product feedbackBitwise and shift operators (C#
reference)
Article •02/08/2023
The bitwise and shift operators include unary bitwise complement, binary left and right
shift, unsigned right shift, and the binary logical AND, OR, and exclusive OR operators.
These operands take operands of the integral numeric types  or the char type.
Unary ~ (bitwise complement)  operator
Binary << (left shift) , >> (right shift) , and >>> (unsigned right shift)  operators
Binary & (logical AND) , | (logical OR) , and ^ (logical exclusive OR)  operators
Those operators are defined for the int, uint, long, and ulong types. When both
operands are of other integral types ( sbyte, byte, short, ushort, or char), their values
are converted to the int type, which is also the result type of an operation. When
operands are of different integral types, their values are converted to the closest
containing integral type. For more information, see the Numeric promotions  section of
the C# language specification . The compound operators (such as >>=) don't convert
their arguments to int or have the result type as int.
The &, |, and ^ operators are also defined for operands of the bool type. For more
information, see Boolean logical operators .
Bitwise and shift operations never cause overflow and produce the same results in
checked and unchecked  contexts.
The ~ operator produces a bitwise complement of its operand by reversing each bit:
C#
You can also use the ~ symbol to declare finalizers. For more information, see Finalizers .Bitwise complement operator ~
uint a = 0b_0000_1111_0000_1111_0000_1111_0000_1100;  
uint b = ~a;  
Console.WriteLine(Convert.ToString(b, toBase: 2)); 
// Output:  
// 11110000111100001111000011110011  The << operator shifts its left-hand operand left by the number of bits defined by its
right-hand operand. For information about how the right-hand operand defines the
shift count, see the Shift count of the shift operators  section.
The left-shift operation discards the high-order bits that are outside the range of the
result type and sets the low-order empty bit positions to zero, as the following example
shows:
C#
Because the shift operators are defined only for the int, uint, long, and ulong types,
the result of an operation always contains at least 32 bits. If the left-hand operand is of
another integral type ( sbyte, byte, short, ushort, or char), its value is converted to the
int type, as the following example shows:
C#
The >> operator shifts its left-hand operand right by the number of bits defined by its
right-hand operand. For information about how the right-hand operand defines the
shift count, see the Shift count of the shift operators  section.
The right-shift operation discards the low-order bits, as the following example shows:Left-shift operator <<
uint x = 0b_1100_1001_0000_0000_0000_0000_0001_0001;  
Console.WriteLine( $"Before: {Convert.ToString(x, toBase: 2)}"); 
uint y = x << 4; 
Console.WriteLine( $"After:  {Convert.ToString(y, toBase: 2)}"); 
// Output:  
// Before: 11001001000000000000000000010001  
// After:  10010000000000000000000100010000  
byte a = 0b_1111_0001;  
var b = a << 8; 
Console.WriteLine(b.GetType());  
Console.WriteLine( $"Shifted byte: {Convert.ToString(b, toBase: 2)}"); 
// Output:  
// System.Int32  
// Shifted byte: 1111000100000000
Right-shift operator >>C#
The high-order empty bit positions are set based on the type of the left-hand operand
as follows:
If the left-hand operand is of type int or long, the right-shift operator performs
an arithmetic  shift: the value of the most significant bit (the sign bit) of the left-
hand operand is propagated to the high-order empty bit positions. That is, the
high-order empty bit positions are set to zero if the left-hand operand is non-
negative and set to one if it's negative.
C#
If the left-hand operand is of type uint or ulong, the right-shift operator performs
a logical  shift: the high-order empty bit positions are always set to zero.
C#uint x = 0b_1001; 
Console.WriteLine( $"Before: {Convert.ToString(x, toBase: 2), 4}"); 
uint y = x >> 2; 
Console.WriteLine( $"After:  {Convert.ToString(y, toBase: 2).PadLeft( 4, '0'), 
4}"); 
// Output:  
// Before: 1001  
// After:  0010  
int a = int.MinValue;  
Console.WriteLine( $"Before: {Convert.ToString(a, toBase: 2)}"); 
int b = a >> 3; 
Console.WriteLine( $"After:  {Convert.ToString(b, toBase: 2)}"); 
// Output:  
// Before: 10000000000000000000000000000000  
// After:  11110000000000000000000000000000  
uint c = 0b_1000_0000_0000_0000_0000_0000_0000_0000;  
Console.WriteLine( $"Before: {Convert.ToString(c, toBase: 2), 32}"); 
uint d = c >> 3; 
Console.WriteLine( $"After:  {Convert.ToString(d, toBase: 2).PadLeft( 32, 
'0'), 32}"); 
// Output:  
// Before: 10000000000000000000000000000000  
// After:  00010000000000000000000000000000  Available in C# 11 and later, the >>> operator shifts its left-hand operand right by the
number of bits defined by its right-hand operand. For information about how the right-
hand operand defines the shift count, see the Shift count of the shift operators  section.
The >>> operator always performs a logical  shift. That is, the high-order empty bit
positions are always set to zero, regardless of the type of the left-hand operand. The >>
operator  performs an arithmetic  shift (that is, the value of the most significant bit is
propagated to the high-order empty bit positions) if the left-hand operand is of a
signed type. The following example demonstrates the difference between >> and >>>
operators for a negative left-hand operand:
C#７ Note
Use the unsigned right -shift operat or to perform a logical  shift on operands of
signed integer types. This is preferred to casting a left-hand operand to an
unsigned type and then casting the result of a shift operation back to a signed
type.
Unsigned right-shift operator >>>
int x = -8; 
Console.WriteLine( $"Before:    {x,11}, hex: {x,8:x}, binary:  
{Convert.ToString(x, toBase: 2), 32}"); 
int y = x >> 2; 
Console.WriteLine( $"After  >>: {y,11}, hex: {y,8:x}, binary:  
{Convert.ToString(y, toBase: 2), 32}"); 
int z = x >>> 2; 
Console.WriteLine( $"After >>>: {z,11}, hex: {z,8:x}, binary:  
{Convert.ToString(z, toBase: 2).PadLeft( 32, '0'), 32}"); 
// Output:  
// Before:             -8, hex: fffffff8, binary:  
11111111111111111111111111111000  
// After  >>:          -2, hex: fffffffe, binary:  
11111111111111111111111111111110  
// After >>>:  1073741822, hex: 3ffffffe, binary:  
00111111111111111111111111111110  
Logical AND operator &The & operator computes the bitwise logical AND of its integral operands:
C#
For bool operands, the & operator computes the logical AND  of its operands. The unary
& operator is the address-of operator .
The ^ operator computes the bitwise logical exclusive OR, also known as the bitwise
logical X OR, of its integral operands:
C#
For bool operands, the ^ operator computes the logical exclusive OR  of its operands.
The | operator computes the bitwise logical OR of its integral operands:
C#
For bool operands, the | operator computes the logical OR  of its operands.uint a = 0b_1111_1000;  
uint b = 0b_1001_1101;  
uint c = a & b;  
Console.WriteLine(Convert.ToString(c, toBase: 2)); 
// Output:  
// 10011000  
Logical exclusive OR operator ^
uint a = 0b_1111_1000;  
uint b = 0b_0001_1100;  
uint c = a ^ b;  
Console.WriteLine(Convert.ToString(c, toBase: 2)); 
// Output:  
// 11100100  
Logical OR operator |
uint a = 0b_1010_0000;  
uint b = 0b_1001_0001;  
uint c = a | b;  
Console.WriteLine(Convert.ToString(c, toBase: 2)); 
// Output:  
// 10110001  For a binary operator op, a compound assignment expression of the form
C#
is equivalent to
C#
except that x is only evaluated once.
The following example demonstrates the usage of compound assignment with bitwise
and shift operators:
C#Compound assignment
x op= y 
x = x op y  
uint INITIAL_VALUE = 0b_1111_1000;  
uint a = INITIAL_VALUE;  
a &= 0b_1001_1101;  
Display(a);  // output: 10011000  
a = INITIAL_VALUE;  
a |= 0b_0011_0001;  
Display(a);  // output: 11111001  
a = INITIAL_VALUE;  
a ^= 0b_1000_0000;  
Display(a);  // output: 01111000  
a = INITIAL_VALUE;  
a <<= 2; 
Display(a);  // output: 1111100000  
a = INITIAL_VALUE;  
a >>= 4; 
Display(a);  // output: 00001111  
a = INITIAL_VALUE;  
a >>>= 4; 
Display(a);  // output: 00001111  
void Display(uint x) => Console.WriteLine( $"{Convert.ToString(x, toBase:  
2).PadLeft( 8, '0'), 8}"); Because of numeric promotions , the result of the op operation might be not implicitly
convertible to the type T of x. In such a case, if op is a predefined operator and the
result of the operation is explicitly convertible to the type T of x, a compound
assignment expression of the form x op= y is equivalent to x = (T)(x op y), except
that x is only evaluated once. The following example demonstrates that behavior:
C#
The following list orders bitwise and shift operators starting from the highest
precedence to the lowest:
Bitwise complement operator ~
Shift operators <<, >>, and >>>
Logical AND operator &
Logical exclusive OR operator ^
Logical OR operator |
Use parentheses, (), to change the order of evaluation imposed by operator
precedence:
C#byte x = 0b_1111_0001;  
int b = x << 8; 
Console.WriteLine( $"{Convert.ToString(b, toBase: 2)}");  // output:  
1111000100000000  
x <<= 8; 
Console.WriteLine(x);  // output: 0  
Operator precedence
uint a = 0b_1101; 
uint b = 0b_1001; 
uint c = 0b_1010; 
uint d1 = a | b & c;  
Display(d1);  // output: 1101  
uint d2 = (a | b) & c;  
Display(d2);  // output: 1000  
void Display(uint x) => Console.WriteLine( $"{Convert.ToString(x, toBase: 2), 
4}"); For the complete list of C# operators ordered by precedence level, see the Operator
precedence  section of the C# operators  article.
For the built-in shift operators <<, >>, and >>>, the type of the right-hand operand
must be int or a type that has a predefined implicit numeric conversion  to int.
For the x << count, x >> count, and x >>> count expressions, the actual shift count
depends on the type of x as follows:
If the type of x is int or uint, the shift count is defined by the low-order five bits
of the right-hand operand. That is, the shift count is computed from count & 0x1F
(or count & 0b_1_1111).
If the type of x is long or ulong, the shift count is defined by the low-order six
bits of the right-hand operand. That is, the shift count is computed from count &
0x3F (or count & 0b_11_1111).
The following example demonstrates that behavior:
C#Shift count of the shift operators
int count1 = 0b_0000_0001;  
int count2 = 0b_1110_0001;  
int a = 0b_0001; 
Console.WriteLine( $"{a} << {count1}  is {a << count1} ; {a} << {count2}  is {a 
<< count2} "); 
// Output:  
// 1 << 1 is 2; 1 << 225 is 2  
int b = 0b_0100; 
Console.WriteLine( $"{b} >> {count1}  is {b >> count1} ; {b} >> {count2}  is {b 
>> count2} "); 
// Output:  
// 4 >> 1 is 2; 4 >> 225 is 2  
int count = -31; 
int c = 0b_0001; 
Console.WriteLine( $"{c} << {count} is {c << count} "); 
// Output:  
// 1 << -31 is 2  The ~, &, |, and ^ operators are also supported by any enumeration  type. For
operands of the same enumeration type, a logical operation is performed on the
corresponding values of the underlying integral type. For example, for any x and y of
an enumeration type T with an underlying type U, the x & y expression produces the
same result as the (T)((U)x & (U)y) expression.
You typically use bitwise logical operators with an enumeration type that is defined with
the Flags  attribute. For more information, see the Enumeration types as bit flags  section
of the Enumeration types  article.
A user-defined type can overload  the ~, <<, >>, >>>, &, |, and ^ operators. When a
binary operator is overloaded, the corresponding compound assignment operator is
also implicitly overloaded. A user-defined type can't explicitly overload a compound
assignment operator.
If a user-defined type T overloads the <<, >>, or >>> operator, the type of the left-hand
operand must be T. In C# 10 and earlier, the type of the right-hand operand must be
int; beginning with C# 11, the type of the right-hand operand of an overloaded shift
operator can be any.
For more information, see the following sections of the C# language specification :
Bitwise complement operator
Shift operators
Logical operators
Compound assignment
Numeric promotions７ Note
As the preceding example shows, the result of a shift operation can be non-zero
even if the value of the right-hand operand is greater than the number of bits in
the left-hand operand.
Enum eration logical operators
Operator overloadability
C# language specificationC# 11 - R elaxed shift requirements
C# 11 - Logical right-shift operator
C# reference
C# operators and expressions
Boolean logical operatorsSee alsoCollection expressions - C# language
reference
Article •09/01/2023
You can use a collection expr ession  to create common collection values. A collection
expression  is a terse syntax that, when evaluated, can be assigned to many different
collection types. A collection expression contains a sequence of elements between [
and ] brackets. The following example declares a System.Span<T>  of string elements
and initializes them to the days of the week:
C#
A collection expr ession  can be converted to many different collection types. The first
example demonstrated how to initialize a variable using a collection expression. The
following code shows many of the other locations where you can use a collection
expression:
C#
You can't use a collection expression where a compile-time constant is expected, such as
initializing a constant, or as the default value for a method argument.Span<string> weekDays = [ "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" ];
foreach (var day in weekDays)
{
    Console.WriteLine(day);
}
// Initialize private field:
private static readonly  ImmutableArray< string> _months = [ "Jan", "Feb", 
"Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec" ];
// property with expression body:
public IEnumerable< int> MaxDays =>
    [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 ];
public int Sum(IEnumerable< int> values ) =>
    values.Sum();
public void Example()
{
    // As a parameter:
    int sum = Sum([ 1, 2, 3, 4, 5]);
}Both of the previous examples used constants as the elements of a collection
expression. Y ou can also use variables for the elements as shown in the following
example:
C#
You use a spread element  .. to inline collection values in a collection expression. The
following example creates a collection for the full alphabet by combining a collection of
the vowels, a collection of the consonants, and the letter "y", which can be either:
C#
The spread element ..vowels, when evaluated, produces five elements: "a", "e", "i",
"o", and "u". The spread element ..consonants produces 20 elements, the number in
the consonants array. The variable in a spread element must be enumerable using a
foreach  statement. As shown in the previous example, you can combine spread
elements with individual elements in a collection expression.
A collection expr ession  can be converted to different collection types, including:string hydrogen = "H";
string helium = "He";
string lithium = "Li";
string beryllium = "Be";
string boron = "B";
string carbon = "C";
string nitrogen = "N";
string oxygen = "O";
string fluorine = "F";
string neon = "Ne";
string[] elements = [ hydrogen, helium, lithium, beryllium, boron, carbon,  
nitrogen, oxygen, fluorine, neon ];
foreach (var element in elements)
{
    Console.WriteLine(element);
}
Spread element
string[] vowels = [ "a", "e", "i", "o", "u" ];
string[] consonants = [ "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
                        "n", "p", "q", "r", "s", "t", "v", "w", "x", "z" ];
string[] alphabet = [ ..vowels, ..consonants, "y" ];
ConversionsSystem.Span<T>  and System.R eadOnlySpan<T>
Inline arrays
Arrays
Any type with a create method whose parameter type is ReadOnlySpan<T> where
there's an implicit conversion from the collection expression type to T.
Any type that supports a collection initializer , such as
System.Collections.Generic.List<T> . Usually, this requirement means the type
supports System.Collections.Generic.IEnumerable<T>  and there's an accessible
Add method to add items to the collection. There must be an implicit conversion
from the collection expression elements' type to the collection's element type. For
spread elements, there must be an implicit conversion from the spread element's
type to the collection's element type.
Many APIs are overloaded with multiple collection types as parameters. Because a
collection expression can be converted to many different expression types, these APIs
may require casts on the collection expression to specify the correct conversion. The
following conversion rules resolve some of the ambiguities:
Conversion to Span<T> , ReadOnlySpan<T> , or another ref struct  type is better
than a conversion to a non-ref struct type.
Conversion to a noninterface type is better than a conversion to an interface type.
When a collection expression is converted to a Span or ReadOnlySpan, the span object's
safe context is taken from the safe context of all elements included in the span. For
detailed rules, see the Collection expression specification .
A type opts in to collection expression support by writing a Create() method and
applying the System.Runtime.CompilerServices.CollectionBuilderAttribute  on the
collection type to indicate the builder method. For example, consider an application that
uses fixed length buffers of 80 characters. That class might look something like the
following code:
C#Collection builder
public class LineBuffer  : IEnumerable <char>
{
    private readonly  char[] _buffer = new char[80];
    public LineBuffer (ReadOnlySpan< char> buffer )
    {
        int number = (_buffer.Length < buffer.Length) ? _buffer.Length :  You'd like to use it with collection expressions as shown in the following sample:
C#
The LineBuffer type implements IEnumerable<char>, so the compiler recognizes it as a
collection of char items. The type parameter of the implemented
System.Collections.Generic.IEnumerable<T>  interface indicates the element type. Y ou
need to make two additions to your application to be able to assign collection
expressions to a LineBuffer object. First, you need to create a class that contains a
Create method:
C#
The Create method must return a LineBuffer object, and it must take a single
parameter of the type ReadOnlySpan<char>. The type parameter of the ReadOnlySpan
must match the element type of the collection. A builder method that returns a generic
collection would have the generic ReadOnlySpan<T> as its parameter. The method must
be accessible and static.
Finally, you must add the CollectionBuilderAttribute  to the LineBuffer class declaration:
C#buffer.Length;
        for (int i = 0; i < number; i++)
        {
            _buffer[i] = buffer[i];
        }
    }
    public IEnumerator< char> GetEnumerator () => _buffer.AsEnumerable< char>
().GetEnumerator();
    IEnumerator IEnumerable.GetEnumerator() => _buffer.GetEnumerator();
    // etc
}
LineBuffer line = [ 'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', 
'!' ];
internal  static class LineBufferBuilder
{
    internal  static LineBuffer Create(ReadOnlySpan< char> values ) => new 
LineBuffer(values);
}The first parameter provides the name of the Builder  class. The second attribute
provides the name of the builder method.[CollectionBuilder(typeof(LineBufferBuilder), "Create" )]Equality operators - test if two objects
are equal or not
Article •04/08/2023
The == (equality)  and != (inequality)  operators check if their operands are equal or not.
Value types are equal when their contents are equal. R eference types are equal when the
two variables refer to the same storage.
The equality operator == returns true if its operands are equal, false otherwise.
Operands of the built-in value types  are equal if their values are equal:
C#
Two operands of the same enum  type are equal if the corresponding values of the
underlying integral type are equal.
User-defined struct  types don't support the == operator by default. T o support the ==
operator, a user-defined struct must overload  it.Equality operator ==
Value types equality
int a = 1 + 2 + 3;
int b = 6;
Console.WriteLine(a == b);  // output: True
char c1 = 'a';
char c2 = 'A';
Console.WriteLine(c1 == c2);  // output: False
Console.WriteLine(c1 == char.ToLower(c2));  // output: True
７ Note
For the ==, <, >, <=, and >= operators, if any of the operands is not a number
(Double.NaN  or Single.NaN ), the result of operation is false. That means that the
NaN value is neither greater than, less than, nor equal to any other double (or
float) value, including NaN. For more information and examples, see the
Double.NaN  or Single.NaN  reference article.The == and != operators are supported by C# tuples . For more information, see the
Tuple equality  section of the Tuple types  article.
By default, two non-record reference-type operands are equal if they refer to the same
object:
C#
As the example shows, user-defined reference types support the == operator by default.
However, a reference type can overload the == operator. If a reference type overloads
the == operator, use the Object.R eferenceEquals  method to check if two references of
that type refer to the same object.
Record types  support the == and != operators that by default provide value equality
semantics. That is, two record operands are equal when both of them are null or
corresponding values of all fields and auto-implemented properties are equal.
C#Reference types equality
public class ReferenceTypesEquality
{
    public class MyClass
    {
        private int id;
        public MyClass(int id) => this.id = id;
    }
    public static void Main()
    {
        var a = new MyClass( 1);
        var b = new MyClass( 1);
        var c = a;
        Console.WriteLine(a == b);  // output: False
        Console.WriteLine(a == c);  // output: True
    }
}
Record types equality
public class RecordTypesEquality
{
    public record Point(int X, int Y, string Name);
    public record TaggedNumber (int Number, List< string> Tags);As the preceding example shows, for non-record reference-type members their
reference values are compared, not the referenced instances.
Two string  operands are equal when both of them are null or both string instances are
of the same length and have identical characters in each character position:
C#
String equality comparisons are case-sensitive ordinal comparisons. For more
information about string comparison, see How to compare strings in C# .
Two delegate  operands of the same run-time type are equal when both of them are
null or their invocation lists are of the same length and have equal entries in each
position:
C#    public static void Main()
    {
        var p1 = new Point(2, 3, "A");
        var p2 = new Point(1, 3, "B");
        var p3 = new Point(2, 3, "A");
        Console.WriteLine(p1 == p2);  // output: False
        Console.WriteLine(p1 == p3);  // output: True
        var n1 = new TaggedNumber( 2, new List<string>() { "A" });
        var n2 = new TaggedNumber( 2, new List<string>() { "A" });
        Console.WriteLine(n1 == n2);  // output: False
    }
}
String equality
string s1 = "hello!" ;
string s2 = "HeLLo!" ;
Console.WriteLine(s1 == s2.ToLower());  // output: True
string s3 = "Hello!" ;
Console.WriteLine(s1 == s3);  // output: False
Delegate equality
Action a = () => Console.WriteLine( "a");
Action b = a + a;For more information, see the Delegate equality operators  section of the C# language
specification .
Delegates that are produced from evaluation of semantically identical lambda
expressions  aren't equal, as the following example shows:
C#
The inequality operator != returns true if its operands aren't equal, false otherwise.
For the operands of the built-in types , the expression x != y produces the same result
as the expression !(x == y). For more information about type equality, see the Equality
operator  section.
The following example demonstrates the usage of the != operator:
C#Action c = a + a;
Console.WriteLine( object.ReferenceEquals(b, c));  // output: False
Console.WriteLine(b == c);  // output: True
Action a = () => Console.WriteLine( "a");
Action b = () => Console.WriteLine( "a");
Console.WriteLine(a == b);  // output: False
Console.WriteLine(a + b == a + b);  // output: True
Console.WriteLine(b + a == a + b);  // output: False
Inequality operator !=
int a = 1 + 1 + 2 + 3;
int b = 6;
Console.WriteLine(a != b);  // output: True
string s1 = "Hello";
string s2 = "Hello";
Console.WriteLine(s1 != s2);  // output: False
object o1 = 1;
object o2 = 1;
Console.WriteLine(o1 != o2);  // output: True
Operator overloadabilityA user-defined type can overload  the == and != operators. If a type overloads one of
the two operators, it must also overload the other one.
A record type can't explicitly overload the == and != operators. If you need to change
the behavior of the == and != operators for record type T, implement the
IEquatable<T>.Equals  method with the following signature:
C#
For more information, see the Relational and type-testing operators  section of the C#
language specification .
For more information about equality of record types, see the Equality members  section
of the records feature proposal note .
C# reference
C# operators and expressions
System.IEquatable<T>
Object.Equals
Object.R eferenceEquals
Equality comparisons
Comparison operatorspublic virtual bool Equals(T? other );
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
 Provide product feedbackComparison operators (C# reference)
Article •04/08/2023
The < (less than) , > (greater than) , <= (less than or equal) , and >= (greater than or
equal)  comparison, also known as relational, operators compare their operands. Those
operators are supported by all integral  and floating-point  numeric types.
The char type also supports comparison operators. In the case of char operands, the
corresponding character codes are compared.
Enumeration types also support comparison operators. For operands of the same enum
type, the corresponding values of the underlying integral type are compared.
The == and != operators  check if their operands are equal or not.
The < operator returns true if its left-hand operand is less than its right-hand operand,
false otherwise:
C#７ Note
For the ==, <, >, <=, and >= operators, if any of the operands is not a number
(Double.NaN  or Single.NaN ), the result of operation is false. That means that the
NaN value is neither greater than, less than, nor equal to any other double (or
float) value, including NaN. For more information and examples, see the
Double.NaN  or Single.NaN  reference article.
Less than operator <
Console.WriteLine( 7.0 < 5.1);   // output: False  
Console.WriteLine( 5.1 < 5.1);   // output: False  
Console.WriteLine( 0.0 < 5.1);   // output: True  
Console.WriteLine( double.NaN < 5.1);   // output: False  
Console.WriteLine( double.NaN >= 5.1);  // output: False  
Greater than operator >The > operator returns true if its left-hand operand is greater than its right-hand
operand, false otherwise:
C#
The <= operator returns true if its left-hand operand is less than or equal to its right-
hand operand, false otherwise:
C#
The >= operator returns true if its left-hand operand is greater than or equal to its
right-hand operand, false otherwise:
C#
A user-defined type can overload  the <, >, <=, and >= operators.Console.WriteLine( 7.0 > 5.1);   // output: True  
Console.WriteLine( 5.1 > 5.1);   // output: False  
Console.WriteLine( 0.0 > 5.1);   // output: False  
Console.WriteLine( double.NaN > 5.1);   // output: False  
Console.WriteLine( double.NaN <= 5.1);  // output: False  
Less than or equal operator <=
Console.WriteLine( 7.0 <= 5.1);   // output: False  
Console.WriteLine( 5.1 <= 5.1);   // output: True  
Console.WriteLine( 0.0 <= 5.1);   // output: True  
Console.WriteLine( double.NaN > 5.1);   // output: False  
Console.WriteLine( double.NaN <= 5.1);  // output: False  
Greater than or equal operator >=
Console.WriteLine( 7.0 >= 5.1);   // output: True  
Console.WriteLine( 5.1 >= 5.1);   // output: True  
Console.WriteLine( 0.0 >= 5.1);   // output: False  
Console.WriteLine( double.NaN < 5.1);   // output: False  
Console.WriteLine( double.NaN >= 5.1);  // output: False  
Operator overloadabilityIf a type overloads one of the < or > operators, it must overload both < and >. If a
type overloads one of the <= or >= operators, it must overload both <= and >=.
For more information, see the Relational and type-testing operators  section of the C#
language specification .
C# reference
C# operators and expressions
System.IComparable<T>
Equality operatorsC# language specification
See alsoMember access operators and
expressions - the dot, indexer, and
invocation operators.
Article •03/15/2023
You use several operators and expressions to access a type member. These operators
include member access ( .), array element or indexer access ( []), index-from-end ( ^),
range (..), null-conditional operators ( ?. and ?[]), and method invocation ( ()). These
include the null-c onditional  member access ( ?.), and indexer access ( ?[]) operators.
. (member access) : to access a member of a namespace or a type
[] (array element or indexer access) : to access an array element or a type indexer
?. and ?[] (null-conditional operators) : to perform a member or element access
operation only if an operand is non-null
() (invocation) : to call an accessed method or invoke a delegate
^ (index from end) : to indicate that the element position is from the end of a
sequence
.. (range) : to specify a range of indices that you can use to obtain a range of
sequence elements
You use the . token to access a member of a namespace or a type, as the following
examples demonstrate:
Use . to access a nested namespace within a namespace, as the following
example of a using  directive  shows:
C#
Use . to form a quali fied name  to access a type within a namespace, as the
following code shows:
C#Member access expression .
using System.Collections.Generic;
System.Collections.Generic.IEnumerable< int> numbers = new int[] { 1, 2, 3 };Use a using  directive  to make the use of qualified names optional.
Use . to access type members , static and non-static, as the following code shows:
C#
You can also use . to access an extension method .
Square brackets, [], are typically used for array, indexer, or pointer element access.
The following example demonstrates how to access array elements:
C#
If an array index is outside the bounds of the corresponding dimension of an array, an
IndexOutOfRangeException  is thrown.
As the preceding example shows, you also use square brackets when you declare an
array type or instantiate an array instance.var constants = new List<double>();
constants.Add(Math.PI);
constants.Add(Math.E);
Console.WriteLine( $"{constants.Count}  values to show:" );
Console.WriteLine( string.Join(", ", constants));
// Output:
// 2 values to show:
// 3.14159265358979, 2.71828182845905
Indexer operator []
Array access
int[] fib = new int[10];
fib[0] = fib[ 1] = 1;
for (int i = 2; i < fib.Length; i++)
{
    fib[i] = fib[i - 1] + fib[i - 2];
}
Console.WriteLine(fib[fib.Length - 1]);  // output: 55
double[,] matrix = new double[2,2];
matrix[0,0] = 1.0;
matrix[0,1] = 2.0;
matrix[1,0] = matrix[ 1,1] = 3.0;
var determinant = matrix[ 0,0] * matrix[ 1,1] - matrix[ 1,0] * matrix[ 0,1];
Console.WriteLine(determinant);  // output: -3For more information about arrays, see Arrays .
The following example uses the .NET Dictionary<TK ey,TValue>  type to demonstrate
indexer access:
C#
Indexers allow you to index instances of a user-defined type in the similar way as array
indexing. Unlike array indices, which must be integer, the indexer parameters can be
declared to be of any type.
For more information about indexers, see Indexers .
For information about pointer element access, see the Pointer element access operator
[] section of the Pointer related operators  article.
You also use square brackets to specify attributes :
C#
A null-conditional operator applies a member access  (?.) or element access  (?[])
operation to its operand only if that operand evaluates to non-null; otherwise, it returns
null. That is:
If a evaluates to null, the result of a?.x or a?[x] is null.
If a evaluates to non-null, the result of a?.x or a?[x] is the same as the result of
a.x or a[x], respectively.Indexer access
var dict = new Dictionary< string, double>();
dict["one"] = 1;
dict["pi"] = Math.PI;
Console.WriteLine(dict[ "one"] + dict[ "pi"]);  // output: 4.14159265358979
Other usages of []
[System.Diagnostics.Conditional( "DEBUG")]
void TraceMethod () {}
Null-conditional operators ?. and ?[]The null-conditional operators are short-circuiting. That is, if one operation in a chain of
conditional member or element access operations returns null, the rest of the chain
doesn't execute. In the following example, B isn't evaluated if A evaluates to null and
C isn't evaluated if A or B evaluates to null:
C#
If A might be null but B and C wouldn't be null if A isn't null, you only need to apply
the null-conditional operator to A:
C#
In the preceding example, B isn't evaluated and C() isn't called if A is null. However, if
the chained member access is interrupted, for example by parentheses as in (A?.B).C(),
short-circuiting doesn't happen.
The following examples demonstrate the usage of the ?. and ?[] operators:
C#７ Note
If a.x or a[x] throws an exception, a?.x or a?[x] would throw the same
exception for non-null a. For example, if a is a non-null array instance and x
is outside the bounds of a, a?[x] would throw an
IndexOutOfRangeEx ception .
A?.B?.Do(C);
A?.B?[C];
A?.B.C();
double SumNumbers (List<double[]> setsOfNumbers, int indexOfSetToSum )
{
    return setsOfNumbers?[indexOfSetToSum]?.Sum() ?? double.NaN;
}
var sum1 = SumNumbers( null, 0);
Console.WriteLine(sum1);  // output: NaN
var numberSets = new List<double[]>
{
    new[] { 1.0, 2.0, 3.0 },
    nullC#
The first of the preceding two examples also uses the null-coalescing operator ?? to
specify an alternative expression to evaluate in case the result of a null-conditional
operation is null.
If a.x or a[x] is of a non-nullable value type T, a?.x or a?[x] is of the corresponding
nullable value type  T?. If you need an expression of type T, apply the null-coalescing};
var sum2 = SumNumbers(numberSets, 0);
Console.WriteLine(sum2);  // output: 6
var sum3 = SumNumbers(numberSets, 1);
Console.WriteLine(sum3);  // output: NaN
namespace  MemberAccessOperators2 ;
public static class NullConditionalShortCircuiting
{
    public static void Main()
    {
        Person person = null;
        person?.Name.Write(); // no output: Write() is not called due to  
short-circuit.
        try
        {
            (person?.Name).Write();
        }
        catch (NullReferenceException)
        {
            Console.WriteLine( "NullReferenceException" );
        }; // output: NullReferenceException
    }
}
public class Person
{
    public FullName Name { get; set; }
}
public class FullName
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public void Write()
    {
        Console.WriteLine( $"{FirstName}  {LastName} ");
    }
}operator ?? to a null-conditional expression, as the following example shows:
C#
In the preceding example, if you don't use the ?? operator, numbers?.Length < 2
evaluates to false when numbers is null.
The null-conditional member access operator ?. is also known as the Elvis operator.
Use the ?. operator to check if a delegate is non-null and invoke it in a thread-safe way
(for example, when you raise an event ), as the following code shows:
C#
That code is equivalent to the following code:
C#int GetSumOfFirstTwoOrDefault (int[] numbers )
{
    if ((numbers?.Length ?? 0) < 2)
    {
        return 0;
    }
    return numbers[ 0] + numbers[ 1];
}
Console.WriteLine(GetSumOfFirstTwoOrDefault( null));  // output: 0
Console.WriteLine(GetSumOfFirstTwoOrDefault( new int[0]));  // output: 0
Console.WriteLine(GetSumOfFirstTwoOrDefault( new[] { 3, 4, 5 }));  // output:  
7
７ Note
The ?. operator evaluates its left-hand operand no more than once, guaranteeing
that it cannot be changed to null after being verified as non-null.
Thread-safe delegate invocation
PropertyChanged?.Invoke(…)
var handler = this.PropertyChanged;
if (handler != null)
{The preceding example is a thread-safe way to ensure that only a non-null handler is
invoked. Because delegate instances are immutable, no thread can change the object
referenced by the handler local variable. In particular, if the code executed by another
thread unsubscribes from the PropertyChanged event and PropertyChanged becomes
null before handler is invoked, the object referenced by handler remains unaffected.
Use parentheses, (), to call a method  or invoke a delegate .
The following example demonstrates how to call a method, with or without arguments,
and invoke a delegate:
C#
You also use parentheses when you invoke a constructor  with the new operator.
You also use parentheses to adjust the order in which to evaluate operations in an
expression. For more information, see C# operators .
Cast expressions , which perform explicit type conversions, also use parentheses.
The ^ operator indicates the element position from the end of a sequence. For a
sequence of length length, ^n points to the element with offset length - n from the    handler(…);
}
Invocation expression ()
Action<int> display = s => Console.WriteLine(s);
var numbers = new List<int>();
numbers.Add( 10);
numbers.Add( 17);
display(numbers.Count);   // output: 2
numbers.Clear();
display(numbers.Count);   // output: 0
Other usages of ()
Index from end operator ^start of a sequence. For example, ^1 points to the last element of a sequence and
^length points to the first element of a sequence.
C#
As the preceding example shows, expression ^e is of the System.Index  type. In
expression ^e, the result of e must be implicitly convertible to int.
You can also use the ^ operator with the range operator  to create a range of indices.
For more information, see Indices and ranges .
The .. operator specifies the start and end of a range of indices as its operands. The
left-hand operand is an inclusiv e start of a range. The right-hand operand is an exclusiv e
end of a range. Either of the operands can be an index from the start or from the end of
a sequence, as the following example shows:
C#int[] xs = new[] { 0, 10, 20, 30, 40 };
int last = xs[^ 1];
Console.WriteLine(last);  // output: 40
var lines = new List<string> { "one", "two", "three", "four" };
string prelast = lines[^ 2];
Console.WriteLine(prelast);  // output: three
string word = "Twenty" ;
Index toFirst = ^word.Length;
char first = word[toFirst];
Console.WriteLine(first);  // output: T
Range operator ..
int[] numbers = new[] { 0, 10, 20, 30, 40, 50 };
int start = 1;
int amountToTake = 3;
int[] subset = numbers[start..(start + amountToTake)];
Display(subset);  // output: 10 20 30
int margin = 1;
int[] inner = numbers[margin..^margin];
Display(inner);  // output: 10 20 30 40
string line = "one two three" ;
int amountToTakeFromEnd = 5;
Range endIndices = ^amountToTakeFromEnd..^ 0;
string end = line[endIndices];
Console.WriteLine(end);  // output: threeAs the preceding example shows, expression a..b is of the System.Range  type. In
expression a..b, the results of a and b must be implicitly convertible to Int32  or Index .
You can omit any of the operands of the .. operator to obtain an open-ended range:
a.. is equivalent to a..^0
..b is equivalent to 0..b
.. is equivalent to 0..^0
C#
The following table shows various ways to express collection ranges:
Range operat or
expr essionDescr iption
.. All values in the collection.
..end Values from the start to the end exclusively.
start.. Values from the start inclusively to the end.void Display<T>(IEnumerable<T> xs) => Console.WriteLine( string.Join(" ", 
xs));
） Impor tant
Implicit conversions from int to Index throw an ArgumentOutOfRangeEx ception
when the value is negative.
int[] numbers = new[] { 0, 10, 20, 30, 40, 50 };
int amountToDrop = numbers.Length / 2;
int[] rightHalf = numbers[amountToDrop..];
Display(rightHalf);  // output: 30 40 50
int[] leftHalf = numbers[..^amountToDrop];
Display(leftHalf);  // output: 0 10 20
int[] all = numbers[..];
Display(all);  // output: 0 10 20 30 40 50
void Display<T>(IEnumerable<T> xs) => Console.WriteLine( string.Join(" ", 
xs));Range operat or
expr essionDescr iption
start..end Values from the start inclusively to the end exclusively.
^start.. Values from the start inclusively to the end counting from the end.
..^end Values from the start to the end exclusively counting from the end.
start..^end Values from start inclusively to end exclusively counting from the
end.
^start..^end Values from start inclusively to end exclusively both counting from
the end.
The following example demonstrates the effect of using all the ranges presented in the
preceding table:
C#
For more information, see Indices and ranges .
The .. token is also used as the spread operator  in a collection expression.int[] oneThroughTen =
{
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10
};
Write(oneThroughTen, ..);
Write(oneThroughTen, . .3);
Write(oneThroughTen, 2..);
Write(oneThroughTen, 3..5);
Write(oneThroughTen, ^ 2..);
Write(oneThroughTen, ..^ 3);
Write(oneThroughTen, 3..^4);
Write(oneThroughTen, ^ 4..^2);
static void Write(int[] values, Range range ) =>
    Console.WriteLine( $"{range}:\t{string.Join(", ", values[range])} ");
// Sample output:
//      0..^0:      1, 2, 3, 4, 5, 6, 7, 8, 9, 10
//      0..3:       1, 2, 3
//      2..^0:      3, 4, 5, 6, 7, 8, 9, 10
//      3..5:       4, 5
//      ^2..^0:     9, 10
//      0..^3:      1, 2, 3, 4, 5, 6, 7
//      3..^4:      4, 5, 6
//      ^4..^2:     7, 8The ., (), ^, and .. operators can't be overloaded. The [] operator is also considered
a non-overloadable operator. Use indexers  to support indexing with user-defined types.
For more information, see the following sections of the C# language specification :
Member access
Element access
Null-conditional member access
Invocation expressions
For more information about indices and ranges, see the feature proposal note .
Use index operator (style rule IDE0056)
Use range operator (style rule IDE0057)
Use conditional delegate call (style rule IDE1005)
C# reference
C# operators and expressions
?? (null-coalescing operator)
:: operatorOperator overloadability
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
 Provide product feedbackType-testing operators and cast
expressions - is, as, typeof and casts
Article •04/08/2023
These operators and expressions perform type checking or type conversion. The is
operator  checks if the run-time type of an expression is compatible with a given type.
The as operator  explicitly converts an expression to a given type if its run-time type is
compatible with that type. Cast expressions  perform an explicit conversion to a target
type. The typeof operator  obtains the System.T ype instance for a type.
The is operator checks if the run-time type of an expression result is compatible with a
given type. The is operator also tests an expression result against a pattern.
The expression with the type-testing is operator has the following form
C#
where E is an expression that returns a value and T is the name of a type or a type
parameter. E can't be an anonymous method or a lambda expression.
The is operator returns true when an expression result is non-null and any of the
following conditions are true:
The run-time type of an expression result is T.
The run-time type of an expression result derives from type T, implements
interface T, or another implicit reference conversion  exists from it to T.
The run-time type of an expression result is a nullable value type  with the
underlying type T and the Nullable<T>.HasV alue is true.
A boxing  or unboxing  conversion exists from the run-time type of an expression
result to type T.
The is operator doesn't consider user-defined conversions.is operator
E is T The following example demonstrates that the is operator returns true if the run-time
type of an expression result derives from a given type, that is, there exists a reference
conversion between types:
C#
The next example shows that the is operator takes into account boxing and unboxing
conversions but doesn't consider numeric conversions :
C#
For information about C# conversions, see the Conversions  chapter of the C# language
specification .
The is operator also tests an expression result against a pattern. The following example
shows how to use a declaration pattern  to check the run-time type of an expression:
C#public class Base { } 
public class Derived : Base { } 
public static class IsOperatorExample  
{ 
    public static void Main() 
    { 
        object b = new Base();  
        Console.WriteLine(b is Base);  // output: True  
        Console.WriteLine(b is Derived);  // output: False  
        object d = new Derived();  
        Console.WriteLine(d is Base);  // output: True  
        Console.WriteLine(d is Derived); // output: True  
    } 
} 
int i = 27; 
Console.WriteLine(i is System.IFormattable);  // output: True  
object iBoxed = i;  
Console.WriteLine(iBoxed is int);  // output: True  
Console.WriteLine(iBoxed is long);  // output: False  
Type testing with pattern matchingFor information about the supported patterns, see Patterns .
The as operator explicitly converts the result of an expression to a given reference or
nullable value type. If the conversion isn't possible, the as operator returns null. Unlike
a cast expression , the as operator never throws an exception.
The expression of the form
C#
where E is an expression that returns a value and T is the name of a type or a type
parameter, produces the same result as
C#
except that E is only evaluated once.
The as operator considers only reference, nullable, boxing, and unboxing conversions.
You can't use the as operator to perform a user-defined conversion. T o do that, use a
cast expression .
The following example demonstrates the usage of the as operator:
C#int i = 23; 
object iBoxed = i;  
int? jNullable = 7; 
if (iBoxed is int a && jNullable is int b) 
{ 
    Console.WriteLine(a + b);  // output 30  
} 
as operator
E as T 
E is T ? (T)(E) : (T) null 
IEnumerable< int> numbers = new[] { 10, 20, 30 }; 
IList<int> indexable = numbers as IList<int>; 
if (indexable != null) 
{ 
    Console.WriteLine(indexable[ 0] + indexable[indexable.Count - 1]);  // A cast expression of the form (T)E performs an explicit conversion of the result of
expression E to type T. If no explicit conversion exists from the type of E to type T, a
compile-time error occurs. At run time, an explicit conversion might not succeed and a
cast expression might throw an exception.
The following example demonstrates explicit numeric and reference conversions:
C#
For information about supported explicit conversions, see the Explicit conversions
section of the C# language specification . For information about how to define a custom
explicit or implicit type conversion, see User-defined conversion operators .
You also use parentheses to call a method or invoke a delegate .
Other use of parentheses is to adjust the order in which to evaluate operations in an
expression. For more information, see C# operators .output: 40  
} 
７ Note
As the preceding example shows, you need to compare the result of the as
expression with null to check if the conversion is successful. Y ou can use the is
operat or both to test if the conversion succeeds and, if it succeeds, assign its result
to a new variable.
Cast expression
double x = 1234.7; 
int a = (int)x; 
Console.WriteLine(a);   // output: 1234  
IEnumerable< int> numbers = new int[] { 10, 20, 30 }; 
IList<int> list = (IList< int>)numbers;  
Console.WriteLine(list.Count);  // output: 3  
Console.WriteLine(list[ 1]);  // output: 20  
Other usages of ()The typeof operator obtains the System.T ype instance for a type. The argument to the
typeof operator must be the name of a type or a type parameter, as the following
example shows:
C#
The argument mustn't be a type that requires metadata annotations. Examples include
the following types:
dynamic
string? (or any nullable reference type)
These types aren't directly represented in metadata. The types include attributes that
describe the underlying type. In both cases, you can use the underlying type. Instead of
dynamic, you can use object. Instead of string?, you can use string.
You can also use the typeof operator with unbound generic types. The name of an
unbound generic type must contain the appropriate number of commas, which is one
less than the number of type parameters. The following example shows the usage of the
typeof operator with an unbound generic type:
C#
An expression can't be an argument of the typeof operator. T o get the System.T ype
instance for the run-time type of an expression result, use the Object.GetT ype method.typeof operator
void PrintType<T>() => Console.WriteLine( typeof(T)); 
Console.WriteLine( typeof(List<string>)); 
PrintType< int>(); 
PrintType<System.Int32>();  
PrintType<Dictionary< int, char>>(); 
// Output:  
// System.Collections.Generic.List`1[System.String]  
// System.Int32  
// System.Int32  
// System.Collections.Generic.Dictionary`2[System.Int32,System.Char]  
Console.WriteLine( typeof(Dictionary<,>));  
// Output:  
// System.Collections.Generic.Dictionary`2[TKey,TValue]  Use the typeof operator to check if the run-time type of the expression result exactly
matches a given type. The following example demonstrates the difference between type
checking done with the typeof operator and the is operator :
C#
The is, as, and typeof operators can't be overloaded.
A user-defined type can't overload the () operator, but can define custom type
conversions that can be performed by a cast expression. For more information, see
User-defined conversion operators .
For more information, see the following sections of the C# language specification :
The is operator
The as operator
Cast expressions
The typeof operatorType testing with the typeof operator
public class Animal { } 
public class Giraffe : Animal { } 
public static class TypeOfExample  
{ 
    public static void Main() 
    { 
        object b = new Giraffe();  
        Console.WriteLine(b is Animal);  // output: True  
        Console.WriteLine(b.GetType() == typeof(Animal));  // output: False  
        Console.WriteLine(b is Giraffe);  // output: True  
        Console.WriteLine(b.GetType() == typeof(Giraffe));  // output: True  
    } 
} 
Operator overloadability
C# language specification
See alsoC# reference
C# operators and expressions
How to safely cast by using pattern matching and the is and as operators
Generics in .NETUser-defined explicit and implicit
conversion operators
Article •04/12/2023
A user-defined type can define a custom implicit or explicit conversion from or to
another type. Implicit conversions don't require special syntax to be invoked and can
occur in various situations, for example, in assignments and methods invocations.
Predefined C# implicit conversions always succeed and never throw an exception. User-
defined implicit conversions should behave in that way as well. If a custom conversion
can throw an exception or lose information, define it as an explicit conversion.
User-defined conversions aren't considered by the is and as operators. Use a cast
expression  to invoke a user-defined explicit conversion.
Use the operator and implicit or explicit keywords to define an implicit or explicit
conversion, respectively. The type that defines a conversion must be either a source type
or a target type of that conversion. A conversion between two user-defined types can be
defined in either of the two types.
The following example demonstrates how to define an implicit and explicit conversion:
C#
using System;  
public readonly  struct Digit 
{ 
    private readonly  byte digit; 
    public Digit(byte digit) 
    { 
        if (digit > 9) 
        {  
            throw new ArgumentOutOfRangeException( nameof(digit), "Digit 
cannot be greater than nine." ); 
        }  
        this.digit = digit;  
    } 
    public static implicit  operator  byte(Digit d) => d.digit;  
    public static explicit  operator  Digit(byte b) => new Digit(b);  
    public override  string ToString () => $"{digit}"; 
} 
public static class UserDefinedConversions  Beginning with C# 11, you can define check ed explicit conversion operators. For more
information, see the User-defined checked operators  section of the Arithmetic operators
article.
You also use the operator keyword to overload a predefined C# operator. For more
information, see Operator overloading .
For more information, see the following sections of the C# language specification :
Conversion operators
User-defined conversions
Implicit conversions
Explicit conversions
C# reference
C# operators and expressions
Operator overloading
Type-testing and cast operators
Casting and type conversion
Design guidelines - Conversion operators
Chained user-defined explicit conversions in C#{ 
    public static void Main() 
    { 
        var d = new Digit(7); 
        byte number = d;  
        Console.WriteLine(number);  // output: 7  
        Digit digit = (Digit)number;  
        Console.WriteLine(digit);  // output: 7  
    } 
} 
C# language specification
See alsoPointer related operators - take the
address of variables, dereference
storage locations, and access memory
locations
Article •04/12/2023
The pointer operators enable you to take the address of a variable ( &), dereference a
pointer ( *), compare pointer values, and add or subtract pointers and integers.
You use the following operators to work with pointers:
Unary & (address-of)  operator: to get the address of a variable
Unary * (pointer indirection)  operator: to obtain the variable pointed by a pointer
The -> (member access)  and [] (element access)  operators
Arithmetic operators +, -, ++, and --
