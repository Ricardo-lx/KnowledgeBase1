Tell us about y our PDF experience.
C# documentation
Learn how to write any application using the C# programming language on the .NET
platform.
Learn t o program in C#
ｂGET STARTED
Learn C# | Tutorials, courses, videos, and more
ｑVIDEO
C# beginner video series
C# beginner stream
C# intermediate video series
ｇTUTORIAL
Self-guided tutorials
In-browser tutorial
ｉREFERENCE
C# on Q&A
Languages on .NET tech community forums
C# on S tack Overflow
C# on Discord
C# fundamentals
ｅOVERVIE W
A tour of C#
Inside a C# program
C# highlights video series
ｐCONCEPT
Type system
Object oriented programming
Functional techniques
Exceptions
Coding style
ｇTUTORIAL
Display command-line
Intro to classes
Object oriented C#
Converting types
Pattern matching
Use LINQ to query data
Key concepts
ｅOVERVIE W
C# language strategy
Programming concepts
ｆQUICKST ART
Methods
Properties
Indexers
Iterators
Delegates
Events
ｐCONCEPTNullable reference types
Nullable reference migrations
Language Integrated Query (LINQ)
Versioning
What' s new
ｈWHA T'S NE W
What's new in C# 12
What's new in C# 11
What's new in C# 10
ｇTUTORIAL
Explore record types
Explore top level statements
Explore new patterns
Write a custom string interpolation handler
ｉREFERENCE
Breaking changes in the C# compiler
Version compatibility
C# language r eference
ｉREFERENCE
Language reference
C# keywords
C# operators and expressions
Configure language versionC# language specification - C# 7 draft in progress
Stay in t ouch
ｉREFERENCE
.NET developer community
YouTube
Twitter
A tour of the C# language
Article •05/04/2023
C# (pronounced "See Sharp") is a modern, object-oriented, and type-safe programming
language. C# enables developers to build many types of secure and robust applications
that run in .NET. C# has its roots in the C family of languages and will be immediately
familiar to C, C++, Java, and JavaScript programmers. This tour provides an overview of
the major components of the language in C# 11 and earlier. If you want to explore the
language through interactive examples, try the introduction to C#  tutorials.
C# is an object-oriented, component -oriented programming language. C# provides
language constructs to directly support these concepts, making C# a natural language in
which to create and use software components. Since its origin, C# has added features to
support new workloads and emerging software design practices. At its core, C# is an
object -oriented language. Y ou define types and their behavior.
Several C# features help create robust and durable applications. Garb age c ollection
automatically reclaims memory occupied by unreachable unused objects. Nullable types
guard against variables that don't refer to allocated objects. Exception handling
provides a structured and extensible approach to error detection and recovery. Lambda
expressions  support functional programming techniques. Language Int egrated Quer y
(LINQ)  syntax creates a common pattern for working with data from any source.
Language support for asynchr onous oper ations  provides syntax for building distributed
systems. C# has a unified type s ystem. All C# types, including primitive types such as
int and double, inherit from a single root object type. All types share a set of common
operations. V alues of any type can be stored, transported, and operated upon in a
consistent manner. Furthermore, C# supports both user-defined reference types  and
value types . C# allows dynamic allocation of objects and in-line storage of lightweight
structures. C# supports generic methods and types, which provide increased type safety
and performance. C# provides iterators, which enable implementers of collection classes
to define custom behaviors for client code.
C# emphasizes versioning  to ensure programs and libraries can evolve over time in a
compatible manner. Aspects of C#'s design that were directly influenced by versioning
considerations include the separate virtual and override modifiers, the rules for
method overload resolution, and support for explicit interface member declarations.
.NET architectureC# programs run on .NET, a virtual execution system called the common language
runtime (CLR) and a set of class libraries. The CLR is the implementation by Microsoft of
the common language infrastructure (CLI), an international standard. The CLI is the basis
for creating execution and development environments in which languages and libraries
work together seamlessly.
Source code written in C# is compiled into an intermediate language (IL)  that conforms
to the CLI specification. The IL code and resources, such as bitmaps and strings, are
stored in an assembly, typically with an extension of .dll. An assembly contains a
manifest that provides information about the assembly's types, version, and culture.
When the C# program is executed, the assembly is loaded into the CLR. The CLR
performs Just-In-Time (JIT) compilation to convert the IL code to native machine
instructions. The CLR provides other services related to automatic garbage collection,
exception handling, and resource management. Code that's executed by the CLR is
sometimes referred to as "managed code." "Unmanaged code," is compiled into native
machine language that targets a specific platform.
Language interoperability is a key feature of .NET. IL code produced by the C# compiler
conforms to the Common T ype Specification (CT S). IL code generated from C# can
interact with code that was generated from the .NET versions of F#, Visual Basic, C++.
There are more than 20 other CT S-compliant languages. A single assembly may contain
multiple modules written in different .NET languages. The types can reference each
other as if they were written in the same language.
In addition to the runtime services, .NET also includes extensive libraries. These libraries
support many different workloads. They're organized into namespaces that provide a
wide variety of useful functionality. The libraries include everything from file input and
output to string manipulation to XML parsing, to web application frameworks to
Windows Forms controls. The typical C# application uses the .NET class library
extensively to handle common "plumbing" chores.
For more information about .NET, see Overview of .NET .
The "Hello, W orld" program is traditionally used to introduce a programming language.
Here it is in C#:
C#Hello world
using System;The "Hello, W orld" program starts with a using directive that references the System
namespace. Namespaces provide a hierarchical means of organizing C# programs and
libraries. Namespaces contain types and other namespaces—for example, the System
namespace contains a number of types, such as the Console class referenced in the
program, and many other namespaces, such as IO and Collections. A using directive
that references a given namespace enables unqualified use of the types that are
members of that namespace. Because of the using directive, the program can use
Console.WriteLine as shorthand for System.Console.WriteLine.
The Hello class declared by the "Hello, W orld" program has a single member, the
method named Main. The Main method is declared with the static modifier. While
instance methods can reference a particular enclosing object instance using the keyword
this, static methods operate without reference to a particular object. By convention, a
static method named Main serves as the entry point of a C# program.
The line starting with // is a single line c omment . C# single line comments start with //
continue to the end of the current line. C# also supports multi-line c omments . Multi-line
comments start with /* and end with */. The output of the program is produced by the
WriteLine method of the Console class in the System namespace. This class is provided
by the standard class libraries, which, by default, are automatically referenced by the
compiler.
You use the .NET SDK  to build your own "Hello, W orld" program. Once you install the
SDK, you run dotnet new console to create a basic "Hello, W orld" program that you can
modify. For more information, see the Hello, W orld tutorial  in the .NET Get started
section.
A type defines the structure and behavior of any data in C#. The declaration of a type
may include its members, base type, interfaces it implements, and operations permitted
for that type. A variable  is a label that refers to an instance of a specific type.class Hello
{
    static void Main()
    {
        // This line prints "Hello, World" 
        Console.WriteLine( "Hello, World" );
    }
}
Types and variablesThere are two kinds of types in C#: value types  and reference types . Variables of value
types directly contain their data. V ariables of reference types store references to their
data, the latter being known as objects. With reference types, it's possible for two
variables to reference the same object and possible for operations on one variable to
affect the object referenced by the other variable. With value types, the variables each
have their own copy of the data, and it isn't possible for operations on one to affect the
other (except for ref and out parameter variables).
An identi fier is a variable name. An identifier is a sequence of unicode characters
without any whitespace. An identifier may be a C# reserved word, if it's prefixed by @.
Using a reserved word as an identifier can be useful when interacting with other
languages.
C#'s value types are further divided into simple types , enum types , struct types , nullable
value types , and tuple v alue types . C#'s reference types are further divided into class
types , interface types , array types , and delegat e types .
The following outline provides an overview of C#'s type system.
Value types
Simple types
Signed integral : sbyte, short, int, long
Unsigned integral : byte, ushort, uint, ulong
Unicode characters : char, which represents a UTF-16 code unit
IEEE binary floating-point : float, double
High-precision decimal floating-point : decimal
Boolean: bool, which represents Boolean values—values that are either true
or false
Enum types
User-defined types of the form enum E {...}. An enum type is a distinct type
with named constants. Every enum type has an underlying type, which must
be one of the eight integral types. The set of values of an enum type is the
same as the set of values of the underlying type.
Struct types
User-defined types of the form struct S {...}
Nullable value types
Extensions of all other value types with a null value
Tuple value types
User-defined types of the form (T1, T2, ...)
Reference types
Class typesUltimate base class of all other types: object
Unicode strings : string, which represents a sequence of UTF-16 code units
User-defined types of the form class C {...}
Interface types
User-defined types of the form interface I {...}
Array types
Single-dimensional, multi-dimensional, and jagged. For example: int[],
int[,], and int[][]
Delegate types
User-defined types of the form delegate int D(...)
C# programs use type declar ations  to create new types. A type declaration specifies the
name and the members of the new type. Six of C#'s categories of types are user-
definable: class types, struct types, interface types, enum types, delegate types, and
tuple value types. Y ou can also declare record types, either record struct, or record
class. Record types have compiler-synthesized members. Y ou use records primarily for
storing values, with minimal associated behavior.
A class type defines a data structure that contains data members (fields) and
function members (methods, properties, and others). Class types support single
inheritance and polymorphism, mechanisms whereby derived classes can extend
and specialize base classes.
A struct type is similar to a class type in that it represents a structure with data
members and function members. However, unlike classes, structs are value types
and don't typically require heap allocation. S truct types don't support user-
specified inheritance, and all struct types implicitly inherit from type object.
An interface type defines a contract as a named set of public members. A class
or struct that implements an interface must provide implementations of the
interface's members. An interface may inherit from multiple base interfaces, and
a class or struct may implement multiple interfaces.
A delegate type represents references to methods with a particular parameter list
and return type. Delegates make it possible to treat methods as entities that can
be assigned to variables and passed as parameters. Delegates are analogous to
function types provided by functional languages. They're also similar to the
concept of function pointers found in some other languages. Unlike function
pointers, delegates are object-oriented and type-safe.
The class, struct, interface, and delegate types all support generics, whereby they
can be parameterized with other types.C# supports single-dimensional and multi-dimensional arrays of any type. Unlike the
types listed above, array types don't have to be declared before they can be used.
Instead, array types are constructed by following a type name with square brackets. For
example, int[] is a single-dimensional array of int, int[,] is a two-dimensional array
of int, and int[][] is a single-dimensional array of single-dimensional arrays, or a
"jagged" array, of int.
Nullable types don't require a separate definition. For each non-nullable type T, there's
a corresponding nullable type T?, which can hold an additional value, null. For
instance, int? is a type that can hold any 32-bit integer or the value null, and string?
is a type that can hold any string or the value null.
C#'s type system is unified such that a value of any type can be treated as an object.
Every type in C# directly or indirectly derives from the object class type, and object is
the ultimate base class of all types. V alues of reference types are treated as objects
simply by viewing the values as type object. Values of value types are treated as objects
by performing boxing and unbo xing oper ations . In the following example, an int value is
converted to object and back again to int.
C#
When a value of a value type is assigned to an object reference, a "box" is allocated to
hold the value. That box is an instance of a reference type, and the value is copied into
that box. Conversely, when an object reference is cast to a value type, a check is made
that the referenced object is a box of the correct value type. If the check succeeds, the
value in the box is copied to the value type.
C#'s unified type system effectively means that value types are treated as object
references "on demand." Because of the unification, general-purpose libraries that use
type object can be used with all types that derive from object, including both
reference types and value types.
There are several kinds of variables  in C#, including fields, array elements, local variables,
and parameters. V ariables represent storage locations. Every variable has a type that
determines what values can be stored in the variable, as shown below.
Non-nullable value type
A value of that exact typeint i = 123;
object o = i;    // Boxing
int j = (int)o;  // UnboxingNullable value type
A null value or a value of that exact type
object
A null reference, a reference to an object of any reference type, or a reference
to a boxed value of any value type
Class type
A null reference, a reference to an instance of that class type, or a reference to
an instance of a class derived from that class type
Interface type
A null reference, a reference to an instance of a class type that implements
that interface type, or a reference to a boxed value of a value type that
implements that interface type
Array type
A null reference, a reference to an instance of that array type, or a reference to
an instance of a compatible array type
Delegate type
A null reference or a reference to an instance of a compatible delegate type
The key organizational concepts in C# are programs, namesp aces, types , member s, and
assemblies . Programs declare types, which contain members and can be organized into
namespaces. Classes, structs, and interfaces are examples of types. Fields, methods,
properties, and events are examples of members. When C# programs are compiled,
they're physically packaged into assemblies. Assemblies typically have the file extension
.exe or .dll, depending on whether they implement applications  or libraries,
respectively.
As a small example, consider the below C# code:
C#Program structure
namespace  Acme.Collections ;
public class Stack<T>
{
    Entry _top;
    public void Push(T data)
    {
        _top = new Entry(_top, data);
    }
    public T Pop()The fully qualified name of this class is Acme.Collections.Stack. The class contains
several members: a field named _top, two methods named Push and Pop, and a nested
class named Entry. The Entry class further contains three members: a property named
Next, a property named Data, and a constructor. The Stack is a gener ic class. It has one
type parameter, T that is replaced with a concrete type when it's used.
A stack is a "first in - last out" (FIL O) collection. New elements are added to the top of
the stack. When an element is removed, it's removed from the top of the stack. The
previous example declares the Stack type that defines the storage and behavior for a
stack. Y ou can declare a variable that refers to an instance of the Stack type to use that
functionality.
Assemblies contain executable code in the form of Intermediate Language (IL)
instructions, and symbolic information in the form of metadata. Before it's executed, the
Just-In-Time (JIT) compiler of .NET Common Language Runtime converts the IL code in
an assembly to processor-specific code.
Because an assembly is a self-describing unit of functionality containing both code and
metadata, there's no need for #include directives and header files in C#. The public
types and members contained in a particular assembly are made available in a C#
program simply by referencing that assembly when compiling the program. For
example, this program uses the Acme.Collections.Stack class from the acme.dll
assembly:    {
        if (_top == null)
        {
            throw new InvalidOperationException();
        }
        T result = _top.Data;
        _top = _top.Next;
        return result;
    }
    class Entry
    {
        public Entry Next { get; set; }
        public T Data { get; set; }
        public Entry(Entry next, T data )
        {
            Next = next;
            Data = data;
        }
    }
}C#
To compile this program, you would need to reference the assembly containing the stack
class defined in the earlier example.
C# programs can be stored in several source files. When a C# program is compiled, all
of the source files are processed together, and the source files can freely reference each
other. Conceptually, it's as if all the source files were concatenated into one large file
before being processed. Forward declarations are never needed in C# because, with few
exceptions, declaration order is insignificant. C# doesn't limit a source file to declaring
only one public type nor does it require the name of the source file to match a type
declared in the source file.
Further articles in this tour explain these organizational blocks.class Example
{
    public static void Main()
    {
        var s = new Acme.Collections.Stack< int>();
        s.Push(1); // stack contains 1
        s.Push(10); // stack contains 1, 10
        s.Push(100); // stack contains 1, 10, 100
        Console.WriteLine(s.Pop()); // stack contains 1, 10
        Console.WriteLine(s.Pop()); // stack contains 1
        Console.WriteLine(s.Pop()); // stack is empty
    }
}
NextC# types and members
Article •05/26/2023
As an object-oriented language, C# supports the concepts of encapsulation, inheritance,
and polymorphism. A class may inherit directly from one parent class, and it may
implement any number of interfaces. Methods that override virtual methods in a parent
class require the override keyword as a way to avoid accidental redefinition. In C#, a
struct is like a lightweight class; it's a stack-allocated type that can implement interfaces
but doesn't support inheritance. C# provides record class and record struct types,
which are types whose purpose is primarily storing data values.
All types are initialized through a constr uctor, a method responsible for initializing an
instance. T wo constructor declarations have unique behavior:
A paramet erless c onstr uctor, which initializes all fields to their default value.
A primary constr uctor, which declares the required parameters for an instance of
that type.
Class es are the most fundamental of C#'s types. A class is a data structure that combines
state (fields) and actions (methods and other function members) in a single unit. A class
provides a definition for instances of the class, also known as objects . Classes support
inher itance and polymorphism , mechanisms whereby derived class es can extend and
specialize base class es.
New classes are created using class declarations. A class declaration starts with a header.
The header specifies:
The attributes and modifiers of the class
The name of the class
The base class (when inheriting from a base class )
The interfaces implemented by the class.
The header is followed by the class body, which consists of a list of member declarations
written between the delimiters { and }.
The following code shows a declaration of a simple class named Point:
C#Classes and objectsInstances of classes are created using the new operator, which allocates memory for a
new instance, invokes a constructor to initialize the instance, and returns a reference to
the instance. The following statements create two Point objects and store references to
those objects in two variables:
C#
The memory occupied by an object is automatically reclaimed when the object is no
longer reachable. It's not necessary or possible to explicitly deallocate objects in C#.
C#
Applications or tests for algorithms might need to create multiple Point objects. The
following class generates a sequence of random points. The number of points is set by
the primary constr uctor parameter. The primary constructor parameter numberOfPoints is
in scope for all members of the class:
C#public class Point
{
    public int X { get; }
    public int Y { get; }
    
    public Point(int x, int y) => (X, Y) = (x, y);
}
var p1 = new Point(0, 0);
var p2 = new Point(10, 20);
var p1 = new Point(0, 0);
var p2 = new Point(10, 20);
public class PointFactory (int numberOfPoints )
{
    public IEnumerable<Point> CreatePoints ()
    {
        var generator = new Random();
        for (int i = 0; i < numberOfPoints; i++)
        {
            yield return new Point(generator.Next( ), generator. Next());
        }
    }
}You can use the class as shown in the following code:
C#
Generic classes define type p aramet ers. Type parameters are a list of type parameter
names enclosed in angle brackets. T ype parameters follow the class name. The type
parameters can then be used in the body of the class declarations to define the
members of the class. In the following example, the type parameters of Pair are TFirst
and TSecond:
C#
A class type that is declared to take type parameters is called a gener ic class type . Struct,
interface, and delegate types can also be generic. When the generic class is used, type
arguments must be provided for each of the type parameters:
C#
A generic type with type arguments provided, like Pair<int,string> above, is called a
constr ucted type .var factory = new PointFactory( 10);
foreach (var point in factory.CreatePoints())
{
    Console.WriteLine( $"({point.X} , {point.Y} )");
}
Type parameters
public class Pair<TFirst, TSecond>
{
    public TFirst First { get; }
    public TSecond Second { get; }
    
    public Pair(TFirst first, TSecond second ) => 
        (First, Second) = (first, second);
}
var pair = new Pair<int, string>(1, "two");
int i = pair.First;     //TFirst int
string s = pair.Second; //TSecond string
Base classesA class declaration may specify a base class. Follow the class name and type parameters
with a colon and the name of the base class. Omitting a base class specification is the
same as deriving from type object. In the following example, the base class of Point3D
is Point. From the first example, the base class of Point is object:
C#
A class inherits the members of its base class. Inheritance means that a class implicitly
contains almost all members of its base class. A class doesn't inherit the instance and
static constructors, and the finalizer. A derived class can add new members to those
members it inherits, but it can't remove the definition of an inherited member. In the
previous example, Point3D inherits the X and Y members from Point, and every
Point3D instance contains three properties, X, Y, and Z.
An implicit conversion exists from a class type to any of its base class types. A variable of
a class type can reference an instance of that class or an instance of any derived class.
For example, given the previous class declarations, a variable of type Point can
reference either a Point or a Point3D:
C#
Classes define types that support inheritance and polymorphism. They enable you to
create sophisticated behaviors based on hierarchies of derived classes. By contrast,
struct types are simpler types whose primary purpose is to store data values. S tructs
can't declare a base type; they implicitly derive from System.V alueT ype. You can't derive
other struct types from a struct type. They're implicitly sealed.
C#public class Point3D : Point
{
    public int Z { get; set; }
    
    public Point3D(int x, int y, int z) : base(x, y)
    {
        Z = z;
    }
}
Point a = new(10, 20);
Point b = new Point3D( 10, 20, 30);
StructsAn interface defines a contract that can be implemented by classes and structs. Y ou
define an interface to declare capabilities that are shared among distinct types. For
example, the System.Collections.Generic.IEnumerable<T>  interface defines a consistent
way to traverse all the items in a collection, such as an array. An interface can contain
methods, properties, events, and indexers. An interface typically doesn't provide
implementations of the members it defines—it merely specifies the members that must
be supplied by classes or structs that implement the interface.
Interfaces may employ multiple inher itance. In the following example, the interface
IComboBox inherits from both ITextBox and IListBox.
C#
Classes and structs can implement multiple interfaces. In the following example, the
class EditBox implements both IControl and IDataBound.
C#public struct Point
{
    public double X { get; }
    public double Y { get; }
    
    public Point(double x, double y) => (X, Y) = (x, y);
}
Interfaces
interface  IControl
{
    void Paint();
}
interface  ITextBox  : IControl
{
    void SetText(string text);
}
interface  IListBox  : IControl
{
    void SetItems (string[] items );
}
interface  IComboBox  : ITextBox , IListBox  { }When a class or struct implements a particular interface, instances of that class or struct
can be implicitly converted to that interface type. For example
C#
An Enum  type defines a set of constant values. The following enum declares constants
that define different root vegetables:
C#
You can also define an enum to be used in combination as flags. The following
declaration declares a set of flags for the four seasons. Any combination of the seasons
may be applied, including an All value that includes all seasons:
C#interface  IDataBound
{
    void Bind(Binder b );
}
public class EditBox : IControl , IDataBound
{
    public void Paint() { }
    public void Bind(Binder b ) { }
}
EditBox editBox = new();
IControl control = editBox;
IDataBound dataBound = editBox;
Enum s
public enum SomeRootVegetable
{
    HorseRadish,
    Radish,
    Turnip
}
[Flags]
public enum Seasons
{
    None = 0,
    Summer = 1,
    Autumn = 2,The following example shows declarations of both the preceding enums:
C#
Variables of any type may be declared as non-nullable  or nullable . A nullable variable
can hold an additional null value, indicating no value. Nullable V alue types (structs or
enums) are represented by System.Nullable<T> . Non-nullable and Nullable R eference
types are both represented by the underlying reference type. The distinction is
represented by metadata read by the compiler and some libraries. The compiler
provides warnings when nullable references are dereferenced without first checking
their value against null. The compiler also provides warnings when non-nullable
references are assigned a value that may be null. The following example declares a
nullable int , initializing it to null. Then, it sets the value to 5. It demonstrates the same
concept with a nullable str ing. For more information, see nullable value types  and
nullable reference types .
C#
C# supports tuples , which provides concise syntax to group multiple data elements in a
lightweight data structure. Y ou instantiate a tuple by declaring the types and names of
the members between ( and ), as shown in the following example:    Winter = 4,
    Spring = 8,
    All = Summer | Autumn | Winter | Spring
}
var turnip = SomeRootVegetable.Turnip;
var spring = Seasons.Spring;
var startingOnEquinox = Seasons.Spring | Seasons.Autumn;
var theYear = Seasons.All;
Nullable types
int? optionalInt = default; 
optionalInt = 5;
string? optionalText = default;
optionalText = "Hello World." ;
TuplesC#
Tuples provide an alternative for data structure with multiple members, without using
the building blocks described in the next article.
 (double Sum, int Count) t2 = ( 4.5, 3);
Console.WriteLine( $"Sum of {t2.Count}  elements is {t2.Sum} .");
//Output:
//Sum of 3 elements is 4.5.
Previous NextC# program building blocks
Article •01/10/2023
The types described in the previous article in this T our of C# series  are built by using
these building blocks:
Members , such as properties, fields, methods, and events.
Expressions
Statements
The members of a class are either static member s or instance member s. Static
members belong to classes, and instance members belong to objects (instances of
classes).
The following list provides an overview of the kinds of members a class can contain.
Constants : Constant values associated with the class
Fields : Variables that are associated with the class
Methods : Actions that can be performed by the class
Proper ties: Actions associated with reading and writing named properties of the
class
Index ers: Actions associated with indexing instances of the class like an array
Events: Notifications that can be generated by the class
Operat ors: Conversions and expression operators supported by the class
Construct ors: Actions required to initialize instances of the class or the class itself
Finalizer s: Actions done before instances of the class are permanently discarded
Types : Nested types declared by the class
Each member of a class has an associated accessibility, which controls the regions of
program text that can access the member. There are six possible forms of accessibility.
The access modifiers are summarized below.
public: Access isn't limited.
private: Access is limited to this class.
protected: Access is limited to this class or classes derived from this class.
internal: Access is limited to the current assembly ( .exe or .dll).Members
Accessibilityprotected internal: Access is limited to this class, classes derived from this class,
or classes within the same assembly.
private protected: Access is limited to this class or classes derived from this type
within the same assembly.
A field is a variable that is associated with a class or with an instance of a class.
A field declared with the static modifier defines a static field. A static field identifies
exactly one storage location. No matter how many instances of a class are created,
there's only ever one copy of a static field.
A field declared without the static modifier defines an instance field. Every instance of a
class contains a separate copy of all the instance fields of that class.
In the following example, each instance of the Color class has a separate copy of the R,
G, and B instance fields, but there's only one copy of the Black, White, Red, Green, and
Blue static fields:
C#
As shown in the previous example, read-only f ields may be declared with a readonly
modifier. Assignment to a read-only field can only occur as part of the field's declaration
or in a constructor in the same class.Fields
public class Color
{
    public static readonly  Color Black = new(0, 0, 0);
    public static readonly  Color White = new(255, 255, 255);
    public static readonly  Color Red = new(255, 0, 0);
    public static readonly  Color Green = new(0, 255, 0);
    public static readonly  Color Blue = new(0, 0, 255);
    
    public byte R;
    public byte G;
    public byte B;
    public Color(byte r, byte g, byte b)
    {
        R = r;
        G = g;
        B = b;
    }
}A method  is a member that implements a computation or action that can be performed
by an object or class. Static methods  are accessed through the class. Instance methods
are accessed through instances of the class.
Methods may have a list of paramet ers, which represent values or variable references
passed to the method. Methods have a return type , which specifies the type of the value
computed and returned by the method. A method's return type is void if it doesn't
return a value.
Like types, methods may also have a set of type parameters, for which type arguments
must be specified when the method is called. Unlike types, the type arguments can
often be inferred from the arguments of a method call and need not be explicitly given.
The signatur e of a method must be unique in the class in which the method is declared.
The signature of a method consists of the following:
The name of the method
The number, modifiers, and types of its parameters
The number of type parameters in generic methods.
The signature of a method doesn't include the return type.
When a method body is a single expression, the method can be defined using a
compact expression format, as shown in the following example:
C#
Parameters are used to pass values or variable references to methods. The parameters
of a method get their actual values from the arguments  that are specified when the
method is invoked. There are four kinds of parameters: value parameters, reference
parameters, output parameters, and parameter arrays.
A value p aramet er is used for passing input arguments. A value parameter corresponds
to a local variable that gets its initial value from the argument that was passed for the
parameter. Modifications to a value parameter don't affect the argument that was
passed for the parameter.Methods
public override  string ToString () => "This is an object" ;
ParametersValue parameters can be optional, by specifying a default value so that corresponding
arguments can be omitted.
A reference paramet er is used for passing arguments by reference. The argument passed
for a reference parameter must be a variable with a definite value. During execution of
the method, the reference parameter represents the same storage location as the
argument variable. A reference parameter is declared with the ref modifier. The
following example shows the use of ref parameters.
C#
An output p aramet er is used for passing arguments by reference. It's similar to a
reference parameter, except that it doesn't require that you explicitly assign a value to
the caller-provided argument. An output parameter is declared with the out modifier.
The following example shows the use of out parameters.
C#
A paramet er arr ay permits a variable number of arguments to be passed to a method. A
parameter array is declared with the params modifier. Only the last parameter of a
method can be a parameter array, and the type of a parameter array must be a single-static void Swap(ref int x, ref int y)
{
    int temp = x;
    x = y;
    y = temp;
}
public static void SwapExample ()
{
    int i = 1, j = 2;
    Swap(ref i, ref j);
    Console.WriteLine( $"{i} {j}");    // "2 1"
}
static void Divide(int x, int y, out int quotient, out int remainder )
{
    quotient = x / y;
    remainder = x % y;
}
public static void OutUsage ()
{
    Divide(10, 3, out int quo, out int rem);
    Console.WriteLine( $"{quo} {rem}");// "3 1"
}dimensional array type. The Write and WriteLine methods of the System.Console  class
are good examples of parameter array usage. They're declared as follows.
C#
Within a method that uses a parameter array, the parameter array behaves exactly like a
regular parameter of an array type. However, in an invocation of a method with a
parameter array, it's possible to pass either a single argument of the parameter array
type or any number of arguments of the element type of the parameter array. In the
latter case, an array instance is automatically created and initialized with the given
arguments. This example
C#
is equivalent to writing the following.
C#
A method's body specifies the statements to execute when the method is invoked.
A method body can declare variables that are specific to the invocation of the method.
Such variables are called local v ariables . A local variable declaration specifies a typepublic class Console
{
    public static void Write(string fmt, params object[] args) { }
    public static void WriteLine (string fmt, params object[] args) { }
    // ...
}
int x, y, z;
x = 3;
y = 4;
z = 5;
Console.WriteLine( "x={0} y={1} z={2}" , x, y, z);
int x = 3, y = 4, z = 5;
string s = "x={0} y={1} z={2}" ;
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
Method body and local variablesname, a variable name, and possibly an initial value. The following example declares a
local variable i with an initial value of zero and a local variable j with no initial value.
C#
C# requires a local variable to be definitely assigned  before its value can be obtained.
For example, if the declaration of the previous i didn't include an initial value, the
compiler would report an error for the later usages of i because i wouldn't be
definitely assigned at those points in the program.
A method can use return statements to return control to its caller. In a method
returning void, return statements can't specify an expression. In a method returning
non-void, return statements must include an expression that computes the return
value.
A method declared with a static modifier is a static method . A static method doesn't
operate on a specific instance and can only directly access static members.
A method declared without a static modifier is an instance method . An instance
method operates on a specific instance and can access both static and instance
members. The instance on which an instance method was invoked can be explicitly
accessed as this. It's an error to refer to this in a static method.
The following Entity class has both static and instance members.
C#class Squares
{
    public static void WriteSquares ()
    {
        int i = 0;
        int j;
        while (i < 10)
        {
            j = i * i;
            Console.WriteLine( $"{i} x {i} = {j}");
            i++;
        }
    }
}
Static and instance methodsEach Entity instance contains a serial number (and presumably some other information
that isn't shown here). The Entity constructor (which is like an instance method)
initializes the new instance with the next available serial number. Because the
constructor is an instance member, it's permitted to access both the _serialNo instance
field and the s_nextSerialNo static field.
The GetNextSerialNo and SetNextSerialNo static methods can access the
s_nextSerialNo static field, but it would be an error for them to directly access the
_serialNo instance field.
The following example shows the use of the Entity class.
C#class Entity
{
    static int s_nextSerialNo;
    int _serialNo;
    
    public Entity()
    {
        _serialNo = s_nextSerialNo++;
    }
    
    public int GetSerialNo ()
    {
        return _serialNo;
    }
    
    public static int GetNextSerialNo ()
    {
        return s_nextSerialNo;
    }
    
    public static void SetNextSerialNo (int value)
    {
        s_nextSerialNo = value;
    }
}
Entity.SetNextSerialNo( 1000);
Entity e1 = new();
Entity e2 = new();
Console.WriteLine(e1.GetSerialNo());          // Outputs "1000"
Console.WriteLine(e2.GetSerialNo());          // Outputs "1001"
Console.WriteLine(Entity.GetNextSerialNo());  // Outputs "1002"The SetNextSerialNo and GetNextSerialNo static methods are invoked on the class
whereas the GetSerialNo instance method is invoked on instances of the class.
You use virtual, override, and abstract methods to define the behavior for a hierarchy of
class types. Because a class can derive from a base class, those derived classes may need
to modify the behavior implemented in the base class. A virtual method is one declared
and implemented in a base class where any derived class may provide a more specific
implementation. An override method is a method implemented in a derived class that
modifies the behavior of the base class' implementation. An abstr act method is a
method declared in a base class that must  be overridden in all derived classes. In fact,
abstract methods don't define an implementation in the base class.
Method calls to instance methods may resolve to either base class or derived class
implementations. The type of a variable determines its compile-time type . The compile-
time type  is the type the compiler uses to determine its members. However, a variable
may be assigned to an instance of any type derived from its compile-time type . The run-
time type  is the type of the actual instance a variable refers to.
When a virtual method is invoked, the run-time type  of the instance for which that
invocation takes place determines the actual method implementation to invoke. In a
nonvirtual method invocation, the compile-time type  of the instance is the determining
factor.
A virtual method can be overridden  in a derived class. When an instance method
declaration includes an override modifier, the method overrides an inherited virtual
method with the same signature. A virtual method declaration introduces a new
method. An override method declaration specializes an existing inherited virtual method
by providing a new implementation of that method.
An abstr act method  is a virtual method with no implementation. An abstract method is
declared with the abstract modifier and is permitted only in an abstract class. An
abstract method must be overridden in every non-abstract derived class.
The following example declares an abstract class, Expression, which represents an
expression tree node, and three derived classes, Constant, VariableReference, and
Operation, which implement expression tree nodes for constants, variable references,
and arithmetic operations. (This example is similar to, but not related to the expression
tree types).
C#Virtual, override, and abstract methodspublic abstract  class Expression
{
    public abstract  double Evaluate (Dictionary< string, object> vars);
}
public class Constant  : Expression
{
    double _value;
    
    public Constant (double value)
    {
        _value = value;
    }
    
    public override  double Evaluate (Dictionary< string, object> vars)
    {
        return _value;
    }
}
public class VariableReference  : Expression
{
    string _name;
    
    public VariableReference (string name)
    {
        _name = name;
    }
    
    public override  double Evaluate (Dictionary< string, object> vars)
    {
        object value = vars[_name] ?? throw new Exception( $"Unknown  
variable: {_name}");
        return Convert.ToDouble( value);
    }
}
public class Operation  : Expression
{
    Expression _left;
    char _op;
    Expression _right;
    
    public Operation (Expression left, char op, Expression right )
    {
        _left = left;
        _op = op;
        _right = right;
    }
    
    public override  double Evaluate (Dictionary< string, object> vars)
    {
        double x = _left.Evaluate(vars);
        double y = _right.Evaluate(vars);The previous four classes can be used to model arithmetic expressions. For example,
using instances of these classes, the expression x + 3 can be represented as follows.
C#
The Evaluate method of an Expression instance is invoked to evaluate the given
expression and produce a double value. The method takes a Dictionary argument that
contains variable names (as keys of the entries) and values (as values of the entries).
Because Evaluate is an abstract method, non-abstract classes derived from Expression
must override Evaluate.
A Constant's implementation of Evaluate simply returns the stored constant. A
VariableReference's implementation looks up the variable name in the dictionary and
returns the resulting value. An Operation's implementation first evaluates the left and
right operands (by recursively invoking their Evaluate methods) and then performs the
given arithmetic operation.
The following program uses the Expression classes to evaluate the expression x * (y +
2) for different values of x and y.
C#        switch (_op)
        {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
            
            default: throw new Exception( "Unknown operator" );
        }
    }
}
Expression e = new Operation(
    new VariableReference( "x"),
    '+',
    new Constant( 3));
Expression e = new Operation(
    new VariableReference( "x"),
    '*',
    new Operation(
        new VariableReference( "y"),
        '+',
        new Constant( 2)
    )Method overloading  permits multiple methods in the same class to have the same name
as long as they have unique signatures. When compiling an invocation of an overloaded
method, the compiler uses overload resolution  to determine the specific method to
invoke. Overload resolution finds the one method that best matches the arguments. If
no single best match can be found, an error is reported. The following example shows
overload resolution in effect. The comment for each invocation in the UsageExample
method shows which method is invoked.
C#
As shown by the example, a particular method can always be selected by explicitly
casting the arguments to the exact parameter types and type arguments.);
Dictionary< string, object> vars = new();
vars["x"] = 3;
vars["y"] = 5;
Console.WriteLine(e.Evaluate(vars)); // "21"
vars["x"] = 1.5;
vars["y"] = 9;
Console.WriteLine(e.Evaluate(vars)); // "16.5"
Method overloading
class OverloadingExample
{
    static void F() => Console.WriteLine( "F()");
    static void F(object x) => Console.WriteLine( "F(object)" );
    static void F(int x) => Console.WriteLine( "F(int)" );
    static void F(double x) => Console.WriteLine( "F(double)" );
    static void F<T>(T x) => Console.WriteLine( $"F<T>(T), T is 
{typeof(T)}");            
    static void F(double x, double y) => Console.WriteLine( "F(double,  
double)" );
    
    public static void UsageExample ()
    {
        F();            // Invokes F()
        F(1);           // Invokes F(int)
        F(1.0);         // Invokes F(double)
        F("abc");       // Invokes F<T>(T), T is System.String
        F((double)1);   // Invokes F(double)
        F((object)1);   // Invokes F(object)
        F<int>(1);      // Invokes F<T>(T), T is System.Int32
        F(1, 1);        // Invokes F(double, double)
    }
}Members that contain executable code are collectively known as the function member s
of a class. The preceding section describes methods, which are the primary types of
function members. This section describes the other kinds of function members
supported by C#: constructors, properties, indexers, events, operators, and finalizers.
The following example shows a generic class called MyList<T>, which implements a
growable list of objects. The class contains several examples of the most common kinds
of function members.
C#Other function members
public class MyList<T>
{
    const int DefaultCapacity = 4;
    T[] _items;
    int _count;
    public MyList(int capacity = DefaultCapacity )
    {
        _items = new T[capacity];
    }
    public int Count => _count;
    public int Capacity
    {
        get =>  _items.Length;
        set
        {
            if (value < _count) value = _count;
            if (value != _items.Length)
            {
                T[] newItems = new T[value];
                Array.Copy(_items, 0, newItems, 0, _count);
                _items = newItems;
            }
        }
    }
    public T this[int index]
    {
        get => _items[index];
        set
        {
            if (!object.Equals(_items[index], value)) {
                _items[index] = value;
                OnChanged();
            }C# supports both instance and static constructors. An instance constr uctor is a member
that implements the actions required to initialize an instance of a class. A static
constr uctor is a member that implements the actions required to initialize a class itself
when it's first loaded.
A constructor is declared like a method with no return type and the same name as the
containing class. If a constructor declaration includes a static modifier, it declares a        }
    }
    public void Add(T item)
    {
        if (_count == Capacity) Capacity = _count * 2;
        _items[_count] = item;
        _count++;
        OnChanged();
    }
    protected  virtual void OnChanged () =>
        Changed?.Invoke( this, EventArgs.Empty);
    public override  bool Equals(object other) =>
        Equals(this, other as MyList<T>);
    static bool Equals(MyList<T> a, MyList<T> b )
    {
        if (Object.ReferenceEquals(a, null)) return 
Object.ReferenceEquals(b, null);
        if (Object.ReferenceEquals(b, null) || a._count != b._count)
            return false;
        for (int i = 0; i < a._count; i++)
        {
            if (!object.Equals(a._items[i], b._items[i]))
            {
                return false;
            }
        }
        return true;
    }
    public event EventHandler Changed;
    public static bool operator  ==(MyList<T> a, MyList<T> b) =>
        Equals(a, b);
    public static bool operator  !=(MyList<T> a, MyList<T> b) =>
        !Equals(a, b);
}
Constructorsstatic constructor. Otherwise, it declares an instance constructor.
Instance constructors can be overloaded and can have optional parameters. For
example, the MyList<T> class declares one instance constructor with a single optional
int parameter. Instance constructors are invoked using the new operator. The following
statements allocate two MyList<string> instances using the constructor of the MyList
class with and without the optional argument.
C#
Unlike other members, instance constructors aren't inherited. A class has no instance
constructors other than those constructors actually declared in the class. If no instance
constructor is supplied for a class, then an empty one with no parameters is
automatically provided.
Properties are a natural extension of fields. Both are named members with associated
types, and the syntax for accessing fields and properties is the same. However, unlike
fields, properties don't denote storage locations. Instead, properties have accessors that
specify the statements executed when their values are read or written. A get ac cessor
reads the value. A set accessor writes the value.
A property is declared like a field, except that the declaration ends with a get accessor
or a set accessor written between the delimiters { and } instead of ending in a
semicolon. A property that has both a get accessor and a set accessor is a read-wr ite
property. A property that has only a get accessor is a read-only pr operty. A property that
has only a set accessor is a write-only pr operty.
A get accessor corresponds to a parameterless method with a return value of the
property type. A set accessor corresponds to a method with a single parameter named
value and no return type. The get accessor computes the value of the property. The set
accessor provides a new value for the property. When the property is the target of an
assignment, or the operand of ++ or --, the set accessor is invoked. In other cases
where the property is referenced, the get accessor is invoked.
The MyList<T> class declares two properties, Count and Capacity, which are read-only
and read-write, respectively. The following code is an example of use of these
properties:MyList<string> list1 = new();
MyList<string> list2 = new(10);
PropertiesC#
Similar to fields and methods, C# supports both instance properties and static
properties. S tatic properties are declared with the static modifier, and instance
properties are declared without it.
The accessor(s) of a property can be virtual. When a property declaration includes a
virtual, abstract, or override modifier, it applies to the accessor(s) of the property.
An index er is a member that enables objects to be indexed in the same way as an array.
An indexer is declared like a property except that the name of the member is this
followed by a parameter list written between the delimiters [ and ]. The parameters
are available in the accessor(s) of the indexer. Similar to properties, indexers can be
read-write, read-only, and write-only, and the accessor(s) of an indexer can be virtual.
The MyList<T> class declares a single read-write indexer that takes an int parameter.
The indexer makes it possible to index MyList<T> instances with int values. For
example:
C#
Indexers can be overloaded. A class can declare multiple indexers as long as the number
or types of their parameters differ.MyList<string> names = new();
names.Capacity = 100;   // Invokes set accessor
int i = names.Count;    // Invokes get accessor
int j = names.Capacity; // Invokes get accessor
Indexers
MyList<string> names = new();
names.Add( "Liz");
names.Add( "Martha" );
names.Add( "Beth");
for (int i = 0; i < names.Count; i++)
{
    string s = names[i];
    names[i] = s.ToUpper();
}
EventsAn event is a member that enables a class or object to provide notifications. An event is
declared like a field except that the declaration includes an event keyword and the type
must be a delegate type.
Within a class that declares an event member, the event behaves just like a field of a
delegate type (provided the event isn't abstract and doesn't declare accessors). The field
stores a reference to a delegate that represents the event handlers that have been
added to the event. If no event handlers are present, the field is null.
The MyList<T> class declares a single event member called Changed, which indicates that
a new item has been added to the list or a list item has been changed using the indexer
set accessor. The Changed event is raised by the OnChanged virtual method, which first
checks whether the event is null (meaning that no handlers are present). The notion of
raising an event is precisely equivalent to invoking the delegate represented by the
event. There are no special language constructs for raising events.
Clients react to events through event handler s. Event handlers are attached using the +=
operator and removed using the -= operator. The following example attaches an event
handler to the Changed event of a MyList<string>.
C#
For advanced scenarios where control of the underlying storage of an event is desired,
an event declaration can explicitly provide add and remove accessors, which are similar
to the set accessor of a property.class EventExample
{
    static int s_changeCount;
    
    static void ListChanged (object sender, EventArgs e )
    {
        s_changeCount++;
    }
    
    public static void Usage()
    {
        var names = new MyList< string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add( "Liz");
        names.Add( "Martha" );
        names.Add( "Beth");
        Console.WriteLine(s_changeCount); // "3"
    }
}An operator is a member that defines the meaning of applying a particular expression
operator to instances of a class. Three kinds of operators can be defined: unary
operators, binary operators, and conversion operators. All operators must be declared as
public and static.
The MyList<T> class declares two operators, operator == and operator !=. These
overridden operators give new meaning to expressions that apply those operators to
MyList instances. Specifically, the operators define equality of two MyList<T> instances
as comparing each of the contained objects using their Equals methods. The following
example uses the == operator to compare two MyList<int> instances.
C#
The first Console.WriteLine outputs True because the two lists contain the same
number of objects with the same values in the same order. Had MyList<T> not defined
operator ==, the first Console.WriteLine would have output False because a and b
reference different MyList<int> instances.
A finalizer  is a member that implements the actions required to finalize an instance of a
class. T ypically, a finalizer is needed to release unmanaged resources. Finalizers can't
have parameters, they can't have accessibility modifiers, and they can't be invoked
explicitly. The finalizer for an instance is invoked automatically during garbage
collection. For more information, see the article on finalizers .
The garbage collector is allowed wide latitude in deciding when to collect objects and
run finalizers. Specifically, the timing of finalizer invocations isn't deterministic, and
finalizers may be executed on any thread. For these and other reasons, classes should
implement finalizers only when no other solutions are feasible.Operators
MyList<int> a = new();
a.Add(1);
a.Add(2);
MyList<int> b = new();
b.Add(1);
b.Add(2);
Console.WriteLine(a == b);  // Outputs "True"
b.Add(3);
Console.WriteLine(a == b);  // Outputs "False"
FinalizersThe using statement provides a better approach to object destruction.
Expressions  are constructed from operands and operators. The operators of an
expression indicate which operations to apply to the operands. Examples of operators
include +, -, *, /, and new. Examples of operands include literals, fields, local variables,
and expressions.
When an expression contains multiple operators, the precedenc e of the operators
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
await operator tells the compiler to asynchronously await for a result to finish. Control
is returned to the caller, and the method returns a structure that manages the state of
the asynchronous work. The structure is typically a
System.Threading.T asks.T ask<TR esult> , but can be any type that supports the awaiter
pattern. These features enable you to write code that reads as its synchronous
counterpart, but executes asynchronously. For example, the following code downloads
the home page for Microsoft docs :
C#
This small sample shows the major features for asynchronous programming:
The method declaration includes the async modifier.double[] doubles = Apply(a, ( double x) => x * 2.0);
async / await
public async Task<int> RetrieveDocsHomePage ()
{
    var client = new HttpClient();
    byte[] content = await 
client.GetByteArrayAsync( "https://learn.microsoft.com/" );
    Console.WriteLine( $"{nameof(RetrieveDocsHomePage)} : Finished  
downloading." );
    return content.Length;
}The body of the method awaits the return of the GetByteArrayAsync method.
The type specified in the return statement matches the type argument in the
Task<T> declaration for the method. (A method that returns a Task would use
return statements without any argument).
Types, members, and other entities in a C# program support modifiers that control
certain aspects of their behavior. For example, the accessibility of a method is controlled
using the public, protected, internal, and private modifiers. C# generalizes this
capability such that user-defined types of declarative information can be attached to
program entities and retrieved at run-time. Programs specify this declarative
information by defining and using attributes.
The following example declares a HelpAttribute attribute that can be placed on
program entities to provide links to their associated documentation.
C#
All attribute classes derive from the Attribute  base class provided by the .NET library.
Attributes can be applied by giving their name, along with any arguments, inside square
brackets just before the associated declaration. If an attribute's name ends in Attribute,
that part of the name can be omitted when the attribute is referenced. For example, the
HelpAttribute can be used as follows.
C#Attributes
public class HelpAttribute  : Attribute
{
    string _url;
    string _topic;
    public HelpAttribute (string url) => _url = url;
    public string Url => _url;
    public string Topic
    {
        get => _topic;
        set => _topic = value;
    }
}
[Help("https://learn.microsoft.com/dotnet/csharp/tour-of-csharp/features" )]
public class WidgetThis example attaches a HelpAttribute to the Widget class. It adds another
HelpAttribute to the Display method in the class. The public constructors of an
attribute class control the information that must be provided when the attribute is
attached to a program entity. Additional information can be provided by referencing
public read-write properties of the attribute class (such as the reference to the Topic
property previously).
The metadata defined by attributes can be read and manipulated at run time using
reflection. When a particular attribute is requested using this technique, the constructor
for the attribute class is invoked with the information provided in the program source.
The resulting attribute instance is returned. If additional information was provided
through properties, those properties are set to the given values before the attribute
instance is returned.
The following code sample demonstrates how to get the HelpAttribute instances
associated to the Widget class and its Display method.
C#{
    [Help("https://learn.microsoft.com/dotnet/csharp/tour-of-
csharp/features" ,
    Topic = "Display" )]
    public void Display(string text) { }
}
Type widgetType = typeof(Widget);
object[] widgetClassAttributes =  
widgetType.GetCustomAttributes( typeof(HelpAttribute), false);
if (widgetClassAttributes.Length > 0)
{
    HelpAttribute attr = (HelpAttribute)widgetClassAttributes[ 0];
    Console.WriteLine( $"Widget class help URL : {attr.Url}  - Related topic :  
{attr.Topic} ");
}
System.Reflection.MethodInfo displayMethod =  
widgetType.GetMethod( nameof(Widget.Display));
object[] displayMethodAttributes =  
displayMethod.GetCustomAttributes( typeof(HelpAttribute), false);
if (displayMethodAttributes.Length > 0)
{
    HelpAttribute attr = (HelpAttribute)displayMethodAttributes[ 0];
    Console.WriteLine( $"Display method help URL : {attr.Url}  - Related topic  You can explore more about C# by trying one of our tutorials .: {attr.Topic} ");
}
Learn more
Previous
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
 Provide product feedbackAnnotated C# strategy
Article •02/21/2023
We will keep evolving C# to meet the changing needs of developers and remain a state-
of-the-art programming language. W e will innovate eagerly and broadly in collaboration
with the teams responsible for .NET libraries, developer tools, and workload support,
while being careful to stay within the spirit of the language. R ecognizing the diversity of
domains where C# is being used, we will prefer language and performance
improvements that benefit all or most developers and maintain a high commitment to
backwards compatibility. W e will continue to empower the broader .NET ecosystem and
grow its role in C#’s future, while maintaining stewardship of design decisions.
The C# strategy guides our decisions about C# evolution, and these annotations provide
insight into how we think about key statements.
"we will innovate eagerly and broadly"
The C# community continues to grow, and the C# language continues to evolve to meet
the community's needs and expectations. W e draw inspiration from a variety of sources
to select features that benefit a large segment of C# developers, and that provide
consistent improvements in productivity, readability, and performance.
"being careful to stay within the spirit of the language"
We evaluate new ideas in the spirit and history of the C# language. W e prioritize
innovations that make sense to the majority of existing C# developers.
"improvements that benefit all or most developers"
Developers use C# in all .NET workloads, such as web front and back ends, cloud native
development, desktop development and building cross platform applications. W e focus
on new features that have the most impact either directly, or by empowering
improvements to common libraries. Language feature development includes integration
into our developer tools and learning resources.
"high commitment to backwards compatibility"How strategy guides C#We respect that there is a massive amount of C# code in use today. Any potential
breaking change is carefully considered against the scale and impact of disruption to
the C# community.
"maintaining stewardship"
C# language design  takes place in the open with community participation. Anyone
can propose new C# features in our GitHub repos . The Language Design T eam
makes the final decisions after weighing community input.
Introduction to C#
Article •12/10/2022
Welcome to the introduction to C# tutorials. These lessons start with interactive code
that you can run in your browser. Y ou can learn the basics of C# from the C# 101 video
series  before starting these interactive lessons.
The first lessons explain C# concepts using small snippets of code. Y ou'll learn the basics
of C# syntax and how to work with data types like strings, numbers, and booleans. It's all
interactive, and you'll be writing and running code within minutes. These first lessons
assume no prior knowledge of programming or the C# language.
You can try these tutorials in different environments. The concepts you'll learn are the
same. The difference is which experience you prefer:
In your browser, on the docs platform : This experience embeds a runnable C# code
window in docs pages. Y ou write and execute C# code in the browser.
In the Microsoft Learn training experience . This learning path contains several
modules that teach the basics of C#.
In Jupyter on Binder . You can experiment with C# code in a Jupyter notebook on
binder.
On your local machine . After you've explored online, you can download  the .NET
SDK and build programs on your machine.
All the introductory tutorials following the Hello W orld lesson are available using the
online browser experience or in your own local development environment . At the end of
each tutorial, you decide if you want to continue with the next lesson online or on your
own machine. There are links to help you set up your environment and continue with
the next tutorial on your machine.
In the Hello world  tutorial, you'll create the most basic C# program. Y ou'll explore the
string type and how to work with text. Y ou can also use the path on Microsoft Learn
training  or Jupyter on Binder .
https://learn-video.azurefd.net/vod/player?show=csharp-101&ep=what-is-
c&locale=en-us&embedUrl=%2Fdotnet%2Fcsharp%2Ftour-of-csharp%2Ftutorials%2F
Hello world
Numbers in C#In the Numbers in C#  tutorial, you'll learn how computers store numbers and how to
perform calculations with different numeric types. Y ou'll learn the basics of rounding,
and how to perform mathematical calculations using C#. This tutorial is also available to
run locally on your machine .
This tutorial assumes that you've finished the Hello world  lesson.
The Branches and loops  tutorial teaches the basics of selecting different paths of code
execution based on the values stored in variables. Y ou'll learn the basics of control flow,
which is the basis of how programs make decisions and choose different actions. This
tutorial is also available to run locally on your machine .
This tutorial assumes that you've finished the Hello world  and Numbers in C#  lessons.
The List collection  lesson gives you a tour of the List collection type that stores
sequences of data. Y ou'll learn how to add and remove items, search for items, and sort
the lists. Y ou'll explore different kinds of lists. This tutorial is also available to run locally
on your machine .
This tutorial assumes that you've finished the lessons listed above.
This sample requires the dotnet-try  global tool. Once you install the tool, and clone
the try-samples  repo, you can learn Language Integrated Query (LINQ) through a set
of 101 samples you can run interactively. Y ou can explore different ways to query,
explore, and transform data sequences.Branches and loops
List collection
101 Linq Samples
Set up your local environment
Article •04/28/2022
The first step in running a tutorial on your machine is to set up a development
environment.
We recommend Visual S tudio  for Windows or Mac. Y ou can download a free
version from the Visual S tudio downloads page . Visual S tudio includes the .NET
SDK.
You can also use the Visual S tudio Code  editor. Y ou'll need to install the latest
.NET SDK  separately.
If you prefer a different editor, you need to install the latest .NET SDK .
The instructions in these tutorials assume that you're using the .NET CLI to create, build,
and run applications. Y ou'll use the following commands:
dotnet new  creates an application. This command generates the files and assets
necessary for your application. The introduction to C# tutorials all use the console
application type. Once you've got the basics, you can expand to other application
types.
dotnet build  builds the executable.
dotnet run  runs the executable.
If you use Visual S tudio 2019 for these tutorials, you'll choose a Visual S tudio menu
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
decimal max = decimal.MaxValue;  Notice that the range is smaller than the double type. Y ou can see the greater precision
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
When you're done, let's move on to write some code yourself to use what you've
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
You learn about these program elements in the types  section of the fundamentals guide:
Classes
Structs
Namespaces
Interfaces
Enums// A skeleton of a C# program
using System;
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
    class Program
    {
        static void Main(string[] args)
        {
            //Your program starts here...
            Console.WriteLine( "Hello world!" );
        }
    }
}
Related SectionsDelegates
For more information, see Basic concepts  in the C# Language Specification . The
language specification is the definitive source for C# syntax and usage.C# Language Specification
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
 Provide product feedbackMain() and command-line arguments
Article •09/29/2022
The Main method is the entry point of a C# application. (Libraries and services do not
require a Main method as an entry point.) When the application is started, the Main
method is the first method that is invoked.
There can only be one entry point in a C# program. If you have more than one class that
has a Main method, you must compile your program with the StartupObject  compiler
option to specify which Main method to use as the entry point. For more information,
see StartupObject  (C# Compiler Options) .
C#
You can also use Top-level statements  in one file as the entry point for your application:
C#
The Main method is the entry point of an executable program; it is where the
program control starts and ends.
Main is declared inside a class or struct. Main must be static  and it need not be
public . (In the earlier example, it receives the default access of private .) The
enclosing class or struct is not required to be static.class TestClass
{
    static void Main(string[] args)
    {
        // Display the number of command line arguments.
        Console.WriteLine(args.Length);
    }
}
using System.Text;
StringBuilder builder = new();
builder.AppendLine( "Hello");
builder.AppendLine( "World!" );
Console.WriteLine(builder.ToString());
OverviewMain can either have a void, int, Task, or Task<int> return type.
If and only if Main returns a Task or Task<int>, the declaration of Main may
include the async  modifier. This specifically excludes an async void Main method.
The Main method can be declared with or without a string[] parameter that
contains command-line arguments. When using Visual S tudio to create Windows
applications, you can add the parameter manually or else use the
GetCommandLineArgs()  method to obtain the command-line arguments.
Parameters are read as zero-indexed command-line arguments. Unlike C and C++,
the name of the program is not treated as the first command-line argument in the
args array, but it is the first element of the GetCommandLineArgs()  method.
The following list shows valid Main signatures:
C#
The preceding examples all use the public accessor modifier. That's typical, but not
required.
The addition of async and Task, Task<int> return types simplifies program code when
console applications need to start and await asynchronous operations in Main.
You can return an int from the Main method by defining the method in one of the
following ways:
Main method code Main signatur e
No use of args or await static int Main()
Uses args, no use of await static int Main(string[] args)
No use of args, uses await static async Task<int> Main()
Uses args and await static async Task<int> Main(string[] args)public static void Main() { }
public static int Main() { }
public static void Main(string[] args) { }
public static int Main(string[] args) { }
public static async Task Main() { }
public static async Task<int> Main() { }
public static async Task Main(string[] args) { }
public static async Task<int> Main(string[] args) { }
Main() return valuesIf the return value from Main is not used, returning void or Task allows for slightly
simpler code.
Main method code Main signatur e
No use of args or await static void Main()
Uses args, no use of await static void Main(string[] args)
No use of args, uses await static async Task Main()
Uses args and await static async Task Main(string[] args)
However, returning int or Task<int> enables the program to communicate status
information to other programs or scripts that invoke the executable file.
The following example shows how the exit code for the process can be accessed.
This example uses .NET Core  command-line tools. If you are unfamiliar with .NET Core
command-line tools, you can learn about them in this get-started article .
Create a new application by running dotnet new console. Modify the Main method in
Program.cs  as follows:
C#
When a program is executed in Windows, any value returned from the Main function is
stored in an environment variable. This environment variable can be retrieved using
ERRORLEVEL from a batch file, or $LastExitCode from P owerShell.
You can build the application using the dotnet CLI  dotnet build command.
Next, create a P owerShell script to run the application and display the result. P aste the
following code into a text file and save it as test.ps1 in the folder that contains the
project. Run the P owerShell script by typing test.ps1 at the P owerShell prompt.// Save this program as MainReturnValTest.cs.
class MainReturnValTest
{
    static int Main()
    {
        //...
        return 0;
    }
}Because the code returns zero, the batch file will report success. However, if you change
MainR eturnV alTest.cs to return a non-zero value and then recompile the program,
subsequent execution of the P owerShell script will report failure.
PowerShell
Output
When you declare an async return value for Main, the compiler generates the
boilerplate code for calling asynchronous methods in Main. If you don't specify the
async keyword, you need to write that code yourself, as shown in the following
example. The code in the example ensures that your program runs until the
asynchronous operation is completed:
C#
This boilerplate code can be replaced by:dotnet run
if ($LastExitCode  -eq 0) {
    Write-Host  "Execution succeeded"
} else
{
    Write-Host  "Execution Failed"
}
Write-Host  "Return value = "  $LastExitCode
Execution succeeded
Return value = 0
Async Main return values
class AsyncMainReturnValTest
{
    public static void Main()
    {
        AsyncConsoleWork().GetAwaiter().GetResult();
    }
    private static async Task<int> AsyncConsoleWork ()
    {
        // Main body here
        return 0;
    }
}C#
An advantage of declaring Main as async is that the compiler always generates the
correct code.
When the application entry point returns a Task or Task<int>, the compiler generates a
new entry point that calls the entry point method declared in the application code.
Assuming that this entry point is called $GeneratedMain, the compiler generates the
following code for these entry points:
static Task Main() results in the compiler emitting the equivalent of private
static void $GeneratedMain() => Main().GetAwaiter().GetResult();
static Task Main(string[]) results in the compiler emitting the equivalent of
private static void $GeneratedMain(string[] args) =>
Main(args).GetAwaiter().GetResult();
static Task<int> Main() results in the compiler emitting the equivalent of private
static int $GeneratedMain() => Main().GetAwaiter().GetResult();
static Task<int> Main(string[]) results in the compiler emitting the equivalent of
private static int $GeneratedMain(string[] args) =>
Main(args).GetAwaiter().GetResult();class Program
{
    static async Task<int> Main(string[] args)
    {
        return await AsyncConsoleWork();
    }
    private static async Task<int> AsyncConsoleWork ()
    {
        // main body here 
        return 0;
    }
}
７ Note
If the examples used async modifier on the Main method, the compiler would
generate the same code.
Command-Line ArgumentsYou can send arguments to the Main method by defining the method in one of the
following ways:
Main method code Main signatur e
No return value, no use of await static void Main(string[] args)
Return value, no use of await static int Main(string[] args)
No return value, uses await static async Task Main(string[] args)
Return value, uses await static async Task<int> Main(string[] args)
If the arguments are not used, you can omit args from the method signature for slightly
simpler code:
Main method code Main signatur e
No return value, no use of await static void Main()
Return value, no use of await static int Main()
No return value, uses await static async Task Main()
Return value, uses await static async Task<int> Main()
The parameter of the Main method is a String  array that represents the command-line
arguments. Usually you determine whether arguments exist by testing the Length
property, for example:
C#７ Note
You can also use Envir onment.CommandLine  or
Envir onment.GetCommandLineAr gs to access the command-line arguments from
any point in a console or Windows Forms application. T o enable command-line
arguments in the Main method signature in a Windows Forms application, you
must manually modify the signature of Main. The code generated by the Windows
Forms designer creates Main without an input parameter.
if (args.Length == 0)
{
    System.Console.WriteLine( "Please enter a numeric argument." );You can also convert the string arguments to numeric types by using the Convert  class
or the Parse method. For example, the following statement converts the string to a
long number by using the Parse method:
C#
It is also possible to use the C# type long, which aliases Int64:
C#
You can also use the Convert class method ToInt64 to do the same thing:
C#
For more information, see Parse and Convert .
The following example shows how to use command-line arguments in a console
application. The application takes one argument at run time, converts the argument to
an integer, and calculates the factorial of the number. If no arguments are supplied, the
application issues a message that explains the correct usage of the program.
To compile and run the application from a command prompt, follow these steps:
1. Paste the following code into any text editor, and then save the file as a text file
with the name Factorial.cs .
C#    return 1;
}
 Tip
The args array can't be null. So, it's safe to access the Length property without null
checking.
long num = Int64.Parse(args[ 0]);
long num = long.Parse(args[ 0]);
long num = Convert.ToInt64(s);public class Functions
{
    public static long Factorial (int n)
    {
        // Test for invalid input.
        if ((n < 0) || (n > 20))
        {
            return -1;
        }
        // Calculate the factorial iteratively rather than recursively.
        long tempResult = 1;
        for (int i = 1; i <= n; i++)
        {
            tempResult *= i;
        }
        return tempResult;
    }
}
class MainClass
{
    static int Main(string[] args)
    {
        // Test if input arguments were supplied.
        if (args.Length == 0)
        {
            Console.WriteLine( "Please enter a numeric argument." );
            Console.WriteLine( "Usage: Factorial <num>" );
            return 1;
        }
        // Try to convert the input arguments to numbers. This will  
throw
        // an exception if the argument is not a number.
        // num = int.Parse(args[0]);
        int num;
        bool test = int.TryParse(args[ 0], out num);
        if (!test)
        {
            Console.WriteLine( "Please enter a numeric argument." );
            Console.WriteLine( "Usage: Factorial <num>" );
            return 1;
        }
        // Calculate factorial.
        long result = Functions.Factorial(num);
        // Print result.
        if (result == -1)
            Console.WriteLine( "Input must be >= 0 and <= 20." );
        else
            Console.WriteLine( $"The Factorial of {num} is {result} .");2. From the Start screen or Start menu, open a Visual S tudio Developer Command
Prompt  window, and then navigate to the folder that contains the file that you
created.
3. Enter the following command to compile the application.
dotnet build
If your application has no compilation errors, an executable file that's named
Factorial.ex e is created.
4. Enter the following command to calculate the factorial of 3:
dotnet run -- 3
5. The command produces this output: The factorial of 3 is 6.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
System.Environment
How to display command line arguments        return 0;
    }
}
// If 3 is entered on command line, the
// output reads: The factorial of 3 is 6.
７ Note
When running an application in Visual S tudio, you can specify command-line
arguments in the Debug P age, Pr oject Designer .
C# language specification
See also
６ Collaborat e with us on
GitHub.NET feedb ackThe source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackTop-level statemen ts - programs
without Main metho ds
Article •01/12/2022
You don't have to explicitly include a Main method in a console application project.
Instead, you can use the top-lev el statements  feature to minimize the code you have to
write. In this case, the compiler generates a class and Main method entry point for the
application.
Here's a Program.cs  file that is a complete C# program in C# 10:
C#
Top-level statements let you write simple programs for small utilities such as Azure
Functions and GitHub Actions. They also make it simpler for new C# programmers to
get started learning and writing code.
The following sections explain the rules on what you can and can't do with top-level
statements.
An application must have only one entry point. A project can have only one file with
top-level statements. Putting top-level statements in more than one file in a project
results in the following compiler error:
CS8802 Only one compilation unit can have top-level statements.
A project can have any number of additional source code files that don't have top-level
statements.
You can write a Main method explicitly, but it can't function as an entry point. The
compiler issues the following warning:
CS7022 The entry point of the program is global code; ignoring 'Main()' entry point.Console.WriteLine( "Hello World!" );
Only one top-level file
No other entry pointsIn a project with top-level statements, you can't use the -main  compiler option to select
the entry point, even if the project has one or more Main methods.
If you include using directives, they must come first in the file, as in this example:
C#
Top-level statements are implicitly in the global namespace.
A file with top-level statements can also contain namespaces and type definitions, but
they must come after the top-level statements. For example:
C#using directives
using System.Text;
StringBuilder builder = new();
builder.AppendLine( "Hello");
builder.AppendLine( "World!" );
Console.WriteLine(builder.ToString());
Global namespace
Namespaces and type definitio ns
MyClass.TestMethod();
MyNamespace.MyClass.MyMethod();
public class MyClass
{
    public static void TestMethod ()
    {
        Console.WriteLine( "Hello World!" );
    }
}
namespace  MyNamespace
{
    class MyClass
    {
        public static void MyMethod ()Top-level statements can reference the args variable to access any command-line
arguments that were entered. The args variable is never null but its Length is zero if no
command-line arguments were provided. For example:
C#
You can call an async method by using await. For example:
C#
To return an int value when the application ends, use the return statement as you
would in a Main method that returns an int. For example:
C#        {
            Console.WriteLine( "Hello World from  
MyNamespace.MyClass.MyMethod!" );
        }
    }
}
args
if (args.Length > 0)
{
    foreach (var arg in args)
    {
        Console.WriteLine( $"Argument= {arg}");
    }
}
else
{
    Console.WriteLine( "No arguments" );
}
await
Console.Write( "Hello " );
await Task.Delay( 5000);
Console.WriteLine( "World!" );
Exit code for the processThe compiler generates a method to serve as the program entry point for a project with
top-level statements. The name of this method isn't actually Main, it's an
implementation detail that your code can't reference directly. The signature of the
method depends on whether the top-level statements contain the await keyword or the
return statement. The following table shows what the method signature would look
like, using the method name Main in the table for convenience.
Top-lev el code contains Implicit Main signatur e
await and return static async Task<int> Main(string[] args)
await static async Task Main(string[] args)
return static int Main(string[] args)
No await or return static void Main(string[] args)
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
Feature specification - T op-level statementsstring? s = Console.ReadLine();
int returnValue = int.Parse(s ?? "-1");
return returnValue;
Implicit entry point method
C# language specification
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
 Provide product feedbackThe C# type system
Article •11/14/2023
C# is a strongly typed language. Every variable and constant has a type, as does every
expression that evaluates to a value. Every method declaration specifies a name, the
type and kind (value, reference, or output) for each input parameter and for the return
value. The .NET class library defines built-in numeric types and complex types that
represent a wide variety of constructs. These include the file system, network
connections, collections and arrays of objects, and dates. A typical C# program uses
types from the class library and user-defined types that model the concepts that are
specific to the program's problem domain.
The information stored in a type can include the following items:
The storage space that a variable of the type requires.
The maximum and minimum values that it can represent.
The members (methods, fields, events, and so on) that it contains.
The base type it inherits from.
The interface(s) it implements.
The kinds of operations that are permitted.
The compiler uses type information to make sure all operations that are performed in
your code are type s afe. For example, if you declare a variable of type int, the compiler
allows you to use the variable in addition and subtraction operations. If you try to
perform those same operations on a variable of type bool, the compiler generates an
error, as shown in the following example:
C#
int a = 5;
int b = a + 2; //OK
bool test = true;
// Error. Operator '+' cannot be applied to operands of type 'int' and  
'bool'.
int c = a + test;
７ Note
C and C++ developers, notice that in C#, bool is not convertible to int.The compiler embeds the type information into the executable file as metadata. The
common language runtime (CLR) uses that metadata at run time to further guarantee
type safety when it allocates and reclaims memory.
When you declare a variable or constant in a program, you must either specify its type
or use the var keyword to let the compiler infer the type. The following example shows
some variable declarations that use both built-in numeric types and complex user-
defined types:
C#
The types of method parameters and return values are specified in the method
declaration. The following signature shows a method that requires an int as an input
argument and returns a string:
C#
After you declare a variable, you can't redeclare it with a new type, and you can't assign
a value not compatible with its declared type. For example, you can't declare an int and
then assign it a Boolean value of true. However, values can be converted to other types,
for example when they're assigned to new variables or passed as method arguments. ASpecifying types in variable declarations
// Declaration only:
float temperature;
string name;
MyClass myClass;
// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3;
int[] source = [ 0, 1, 2, 3, 4, 5];
var query = from item in source
            where item <= limit
            select item;
public string GetName(int ID)
{
    if (ID < names.Length)
        return names[ID];
    else
        return String.Empty;
}
private string[] names = [ "Spencer" , "Sally", "Doug"];type c onversion that doesn't cause data loss is performed automatically by the compiler.
A conversion that might cause data loss requires a cast in the source code.
For more information, see Casting and T ype Conversions .
C# provides a standard set of built-in types. These represent integers, floating point
values, Boolean expressions, text characters, decimal values, and other types of data.
There are also built-in string and object types. These types are available for you to use
in any C# program. For the complete list of the built-in types, see Built-in types .
You use the struct , class , interface , enum , and record  constructs to create your own
custom types. The .NET class library itself is a collection of custom types that you can
use in your own applications. By default, the most frequently used types in the class
library are available in any C# program. Others become available only when you
explicitly add a project reference to the assembly that defines them. After the compiler
has a reference to the assembly, you can declare variables (and constants) of the types
declared in that assembly in source code. For more information, see .NET Class Library .
It's important to understand two fundamental points about the type system in .NET:
It supports the principle of inheritance. T ypes can derive from other types, called
base types . The derived type inherits (with some restrictions) the methods,
properties, and other members of the base type. The base type can in turn derive
from some other type, in which case the derived type inherits the members of both
base types in its inheritance hierarchy. All types, including built-in numeric types
such as System.Int32  (C# keyword: int), derive ultimately from a single base type,
which is System.Object  (C# keyword: object ). This unified type hierarchy is called
the Common T ype S ystem  (CTS). For more information about inheritance in C#, see
Inheritance .
Each type in the CT S is defined as either a value type  or a reference type . These
types include all custom types in the .NET class library and also your own user-
defined types. T ypes that you define by using the struct keyword are value types;
all the built-in numeric types are structs. Types that you define by using theBuilt-in types
Custom types
The common type systemclass or record keyword are reference types. R eference types and value types
have different compile-time rules, and different run-time behavior.
The following illustration shows the relationship between value types and reference
types in the CT S.
Classes and structs are two of the basic constructs of the common type system in .NET.
Each is essentially a data structure that encapsulates a set of data and behaviors that
belong together as a logical unit. The data and behaviors are the member s of the class,
struct, or record. The members include its methods, properties, events, and so on, as
listed later in this article.
A class, struct, or record declaration is like a blueprint that is used to create instances or
objects at run time. If you define a class, struct, or record named Person, Person is the
name of the type. If you declare and initialize a variable p of type Person, p is said to
be an object or instance of Person. Multiple instances of the same Person type can be
created, and each instance can have different values in its properties and fields.７ Note
You can see that the most commonly used types are all organized in the System
namespace. However, the namespace in which a type is contained has no relation
to whether it is a value type or reference type.A class is a reference type. When an object of the type is created, the variable to which
the object is assigned holds only a reference to that memory. When the object reference
is assigned to a new variable, the new variable refers to the original object. Changes
made through one variable are reflected in the other variable because they both refer to
the same data.
A struct is a value type. When a struct is created, the variable to which the struct is
assigned holds the struct's actual data. When the struct is assigned to a new variable, it's
copied. The new variable and the original variable therefore contain two separate copies
of the same data. Changes made to one copy don't affect the other copy.
Record types may be either reference types ( record class) or value types ( record
struct). Record types contain methods that support value-equality.
In general, classes are used to model more complex behavior. Classes typically store
data that is intended to be modified after a class object is created. S tructs are best
suited for small data structures. S tructs typically store data that isn't intended to be
modified after the struct is created. R ecord types are data structures with additional
compiler synthesized members. R ecords typically store data that isn't intended to be
modified after the object is created.
Value types derive from System.V alueT ype, which derives from System.Object . Types that
derive from System.V alueT ype have special behavior in the CLR. V alue type variables
directly contain their values. The memory for a struct is allocated inline in whatever
context the variable is declared. There's no separate heap allocation or garbage
collection overhead for value-type variables. Y ou can declare record struct types that
are value types and include the synthesized members for records .
There are two categories of value types: struct and enum.
The built-in numeric types are structs, and they have fields and methods that you can
access:
C#
But you declare and assign values to them as if they're simple non-aggregate types:
C#Value types
// constant field on type byte.
byte b = byte.MaxValue;Value types are sealed . You can't derive a type from any value type, for example
System.Int32 . You can't define a struct to inherit from any user-defined class or struct
because a struct can only inherit from System.V alueT ype. However, a struct can
implement one or more interfaces. Y ou can cast a struct type to any interface type that it
implements. This cast causes a boxing operation to wrap the struct inside a reference
type object on the managed heap. Boxing operations occur when you pass a value type
to a method that takes a System.Object  or any interface type as an input parameter. For
more information, see Boxing and Unboxing .
You use the struct  keyword to create your own custom value types. T ypically, a struct is
used as a container for a small set of related variables, as shown in the following
example:
C#
For more information about structs, see Structure types . For more information about
value types, see Value types .
The other category of value types is enum. An enum defines a set of named integral
constants. For example, the System.IO.FileMode  enumeration in the .NET class library
contains a set of named constant integers that specify how a file should be opened. It's
defined as shown in the following example:
C#byte num = 0xA;
int i = 5;
char c = 'Z';
public struct Coords
{
    public int x, y;
    public Coords(int p1, int p2)
    {
        x = p1;
        y = p2;
    }
}
public enum FileMode
{
    CreateNew = 1,
    Create = 2,
    Open = 3,
    OpenOrCreate = 4,The System.IO.FileMode.Create  constant has a value of 2. However, the name is much
more meaningful for humans reading the source code, and for that reason it's better to
use enumerations instead of constant literal numbers. For more information, see
System.IO.FileMode .
All enums inherit from System.Enum , which inherits from System.V alueT ype. All the rules
that apply to structs also apply to enums. For more information about enums, see
Enumeration types .
A type that is defined as a class, record, delegate , array, or interface  is a reference
type.
When declaring a variable of a reference type , it contains the value null until you assign
it with an instance of that type or create one using the new operator. Creation and
assignment of a class are demonstrated in the following example:
C#
An interface  cannot be directly instantiated using the new operator. Instead, create and
assign an instance of a class that implements the interface. Consider the following
example:
C#
When the object is created, the memory is allocated on the managed heap. The variable
holds only a reference to the location of the object. T ypes on the managed heap require
overhead both when they're allocated and when they're reclaimed. Garb age c ollection  is    Truncate = 5,
    Append = 6,
}
Reference types
MyClass myClass = new MyClass();
MyClass myClass2 = myClass;
MyClass myClass = new MyClass();
// Declare and assign using an existing value.
IMyInterface myInterface = myClass;
// Or create and assign a value in a single statement.
IMyInterface myInterface2 = new MyClass();the automatic memory management functionality of the CLR, which performs the
reclamation. However, garbage collection is also highly optimized, and in most scenarios
it doesn't create a performance issue. For more information about garbage collection,
see Automatic Memory Management .
All arrays are reference types, even if their elements are value types. Arrays implicitly
derive from the System.Array  class. Y ou declare and use them with the simplified syntax
that is provided by C#, as shown in the following example:
C#
Reference types fully support inheritance. When you create a class, you can inherit from
any other interface or class that isn't defined as sealed . Other classes can inherit from
your class and override your virtual methods. For more information about how to create
your own classes, see Classes, structs, and records . For more information about
inheritance and virtual methods, see Inheritance .
In C#, literal values receive a type from the compiler. Y ou can specify how a numeric
literal should be typed by appending a letter to the end of the number. For example, to
specify that the value 4.56 should be treated as a float, append an "f" or "F" after the
number: 4.56f. If no letter is appended, the compiler will infer a type for the literal. For
more information about which types can be specified with letter suffixes, see Integral
numeric types  and Floating-point numeric types .
Because literals are typed, and all types derive ultimately from System.Object , you can
write and compile code such as the following code:
C#// Declare and initialize an array of integers.
int[] nums = [ 1, 2, 3, 4, 5];
// Access an instance property of System.Array.
int len = nums.Length;
Types of literal values
string s = "The answer is "  + 5.ToString();
// Outputs: "The answer is 5"
Console.WriteLine(s);
Type type = 12345.GetType();
// Outputs: "System.Int32"
Console.WriteLine(type);A type can be declared with one or more type p aramet ers that serve as a placeholder for
the actual type (the concrete type ). Client code provides the concrete type when it
creates an instance of the type. Such types are called gener ic types . For example, the
.NET type System.Collections.Generic.List<T>  has one type parameter that by
convention is given the name T. When you create an instance of the type, you specify
the type of the objects that the list will contain, for example, string:
C#
The use of the type parameter makes it possible to reuse the same class to hold any
type of element, without having to convert each element to object . Generic collection
classes are called strongly typed c ollections  because the compiler knows the specific type
of the collection's elements and can raise an error at compile time if, for example, you
try to add an integer to the stringList object in the previous example. For more
information, see Generics .
You can implicitly type a local variable (but not class members) by using the var
keyword. The variable still receives a type at compile time, but the type is provided by
the compiler. For more information, see Implicitly T yped Local V ariables .
It can be inconvenient to create a named type for simple sets of related values that you
don't intend to store or pass outside method boundaries. Y ou can create anon ymous
types  for this purpose. For more information, see Anonymous T ypes.
Ordinary value types can't have a value of null. However, you can create nullable v alue
types  by appending a ? after the type. For example, int? is an int type that can also
have the value null. Nullable value types are instances of the generic struct type
System.Nullable<T> . Nullable value types are especially useful when you're passing data
to and from databases in which numeric values might be null. For more information,
see Nullable value types .Generic types
List<string> stringList = new List<string>();
stringList.Add( "String example" );
// compile time error adding a type other than a string:
stringList.Add( 4);
Implicit types, anonymous types, and nulla ble
value typesA variable can have different compile-time and run-time types. The compile-time type  is
the declared or inferred type of the variable in the source code. The run-time type  is the
type of the instance referred to by that variable. Often those two types are the same, as
in the following example:
C#
In other cases, the compile-time type is different, as shown in the following two
examples:
C#
In both of the preceding examples, the run-time type is a string. The compile-time
type is object in the first line, and IEnumerable<char> in the second.
If the two types are different for a variable, it's important to understand when the
compile-time type and the run-time type apply. The compile-time type determines all
the actions taken by the compiler. These compiler actions include method call
resolution, overload resolution, and available implicit and explicit casts. The run-time
type determines all actions that are resolved at run time. These run-time actions include
dispatching virtual method calls, evaluating is and switch expressions, and other type
testing APIs. T o better understand how your code interacts with types, recognize which
action applies to which type.
For more information, see the following articles:
Builtin types
Value T ypes
Reference T ypesCompile-time type and run-time type
string message = "This is a string of characters" ;
object anotherMessage = "This is another string of characters" ;
IEnumerable< char> someCharacters = "abcdefghijklmnopqrstuvwxyz" ;
Related sections
C# language specificationFor more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
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
 Provide product feedbackDeclare namespaces to organize types
Article •01/12/2022
Namespaces are heavily used in C# programming in two ways. First, .NET uses
namespaces to organize its many classes, as follows:
C#
System  is a namespace and Console  is a class in that namespace. The using keyword
can be used so that the complete name isn't required, as in the following example:
C#
C#
For more information, see the using Directive .
Second, declaring your own namespaces can help you control the scope of class and
method names in larger programming projects. Use the namespace  keyword to declareSystem.Console.WriteLine( "Hello World!" ); 
using System;  
Console.WriteLine( "Hello World!" ); 
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
the project type.a namespace, as in the following example:
C#
The name of the namespace must be a valid C# identifier name .
Beginning with C# 10, you can declare a namespace for all types defined in that file, as
shown in the following example:
C#
The advantage of this new syntax is that it's simpler, saving horizontal space and braces.
That makes your code easier to read.
Namespaces have the following properties:
They organize large code projects.
They're delimited by using the . operator.
The using directive obviates the requirement to specify the name of the
namespace for every class.namespace  SampleNamespace  
{ 
    class SampleClass  
    { 
        public void SampleMethod () 
        {  
            System.Console.WriteLine(  
                "SampleMethod inside SampleNamespace" ); 
        }  
    } 
} 
namespace  SampleNamespace ; 
class AnotherSampleClass  
{ 
    public void AnotherSampleMethod () 
    { 
        System.Console.WriteLine(
            "SampleMethod inside SampleNamespace" ); 
    } 
} 
Namespaces overviewThe global namespace is the "root" namespace: global::System will always refer
to the .NET System  namespace.
For more information, see the Namespaces  section of the C# language specification .C# language specificationIntroduction to classes
Article •05/26/2023
A type that is defined as a class  is a reference type . At run time, when you declare a
variable of a reference type, the variable contains the value null until you explicitly
create an instance of the class by using the new operator, or assign it an object of a
compatible type that may have been created elsewhere, as shown in the following
example:
C#
When the object is created, enough memory is allocated on the managed heap for that
specific object, and the variable holds only a reference to the location of said object. The
memory used by an object is reclaimed by the automatic memory management
functionality of the CLR, which is known as garbage c ollection . For more information
about garbage collection, see Automatic memory management and garbage collection .
Classes are declared by using the class keyword followed by a unique identifier, as
shown in the following example:
C#
An optional access modifier precedes the class keyword. Because public  is used in this
case, anyone can create instances of this class. The name of the class follows the classReference types
//Declaring an object of type MyClass.  
MyClass mc = new MyClass();  
//Declaring another object of the same type, assigning it the value of the  
first object.  
MyClass mc2 = mc;  
Declaring classes
//[access modifier] - [class] - [identifier]  
public class Customer  
{ 
   // Fields, properties, methods and events go here...  
} keyword. The name of the class must be a valid C# identifier name . The remainder of the
definition is the class body, where the behavior and data are defined. Fields, properties,
methods, and events on a class are collectively referred to as class member s.
Although they're sometimes used interchangeably, a class and an object are different
things. A class defines a type of object, but it isn't an object itself. An object is a concrete
entity based on a class, and is sometimes referred to as an instance of a class.
Objects can be created by using the new keyword followed by the name of the class, like
this:
C#
When an instance of a class is created, a reference to the object is passed back to the
programmer. In the previous example, object1 is a reference to an object that is based
on Customer. This reference refers to the new object but doesn't contain the object data
itself. In fact, you can create an object reference without creating an object at all:
C#
We don't recommend creating object references that don't refer to an object because
trying to access an object through such a reference fails at run time. A reference can be
made to refer to an object, either by creating a new object, or by assigning it an existing
object, such as this:
C#
This code creates two object references that both refer to the same object. Therefore,
any changes to the object made through object3 are reflected in subsequent uses of
object4. Because objects that are based on classes are referred to by reference, classes
are known as reference types.Creating objects
Customer object1 = new Customer();  
Customer object2;  
Customer object3 = new Customer();  
Customer object4 = object3;  The preceding sections introduced the syntax to declare a class type and create an
instance of that type. When you create an instance of a type, you want to ensure that its
fields and properties are initialized to useful values. There are several ways to initialize
values:
Accept default values
Field initializers
Constructor parameters
Object initializers
Every .NET type has a default value. T ypically, that value is 0 for number types, and null
for all reference types. Y ou can rely on that default value when it's reasonable in your
app.
When the .NET default isn't the right value, you can set an initial value using a field
initializer :
C#
You can require callers to provide an initial value by defining a constr uctor that's
responsible for setting that initial value:
C#
Beginning with C# 12, you can define a primary constr uctor as part of the class
declaration:
C#Constructors and initialization
public class Container  
{ 
    // Initialize capacity field to a default value of 10:  
    private int _capacity = 10; 
} 
public class Container  
{ 
    private int _capacity;  
    public Container (int capacity ) => _capacity = capacity;  
} 
public class Container (int capacity ) 
{ Adding parameters to the class name defines the primary constr uctor. Those parameters
are available in the class body, which includes its members. Y ou can use them to
initialize fields or anywhere else where they're needed.
You can also use the required modifier on a property and allow callers to use an object
initializer  to set the initial value of the property:
C#
The addition of the required keyword mandates that callers must set those properties
as part of a new expression:
C#
Classes fully support inher itance, a fundamental characteristic of object-oriented
programming. When you create a class, you can inherit from any other class that isn't
defined as sealed . Other classes can inherit from your class and override class virtual
methods. Furthermore, you can implement one or more interfaces.
Inheritance is accomplished by using a derivation , which means a class is declared by
using a base class  from which it inherits data and behavior. A base class is specified by
appending a colon and the name of the base class following the derived class name, like
this:
C#    private int _capacity = capacity;  
} 
public class Person 
{ 
    public required string LastName { get; set; } 
    public required string FirstName { get; set; } 
} 
var p1 = new Person(); // Error! Required properties not set  
var p2 = new Person() { FirstName = "Grace", LastName = "Hopper"  }; 
Class inheritance
public class Manager : Employee  
{ 
    // Employee fields, properties, methods and events are inherited  When a class declaration includes a base class, it inherits all the members of the base
class except the constructors. For more information, see Inheritance .
A class in C# can only directly inherit from one base class. However, because a base class
may itself inherit from another class, a class might indirectly inherit multiple base
classes. Furthermore, a class can directly implement one or more interfaces. For more
information, see Interfaces .
A class can be declared as abstract . An abstract class contains abstract methods that
have a signature definition but no implementation. Abstract classes can't be
instantiated. They can only be used through derived classes that implement the abstract
methods. By contrast, a sealed  class doesn't allow other classes to derive from it. For
more information, see Abstract and Sealed Classes and Class Members .
Class definitions can be split between different source files. For more information, see
Partial Classes and Methods .
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.    // New Manager fields, properties, methods and events go here...  
} 
C# Language SpecificationIntroduction to record types in C#
Article •05/26/2023
A record  in C# is a class  or struct  that provides special syntax and behavior for working
with data models. The record modifier instructs the compiler to synthesize members
that are useful for types whose primary role is storing data. These members include an
overload of ToString()  and members that support value equality.
Consider using a record in place of a class or struct in the following scenarios:
You want to define a data model that depends on value equality .
You want to define a type for which objects are immutable.
For records, value equality means that two variables of a record type are equal if the
types match and all property and field values match. For other reference types such as
classes, equality means reference equality . That is, two variables of a class type are equal
if they refer to the same object. Methods and operators that determine equality of two
record instances use value equality.
Not all data models work well with value equality. For example, Entity Framework Core
depends on reference equality to ensure that it uses only one instance of an entity type
for what is conceptually one entity. For this reason, record types aren't appropriate for
use as entity types in Entity Framework Core.
An immutable type is one that prevents you from changing any property or field values
of an object after it's instantiated. Immutability can be useful when you need a type to
be thread-safe or you're depending on a hash code remaining the same in a hash table.
Records provide concise syntax for creating and working with immutable types.
Immutability isn't appropriate for all data scenarios. Entity Framework Core , for example,
doesn't support updating with immutable entity types.When to use records
Value equality
Immutability
How records differ from classes and structsThe same syntax that declares  and instantiates  classes or structs can be used with
records. Just substitute the class keyword with the record, or use record struct
instead of struct. Likewise, the same syntax for expressing inheritance relationships is
supported by record classes. R ecords differ from classes in the following ways:
You can use positional parameters  in a primary constructor  to create and
instantiate a type with immutable properties.
The same methods and operators that indicate reference equality or inequality in
classes (such as Object.Equals(Object)  and ==), indicate value equality or inequality
in records.
You can use a with expression  to create a copy of an immutable object with new
values in selected properties.
A record's ToString method creates a formatted string that shows an object's type
name and the names and values of all its public properties.
A record can inherit from another record . A record can't inherit from a class, and a
class can't inherit from a record.
Record structs differ from structs in that the compiler synthesizes the methods for
equality, and ToString. The compiler synthesizes a Deconstruct method for positional
record structs.
The compiler synthesizes a public init-only property for each primary constructor
parameter in a record class. In a record struct, the compiler synthesizes a public
read-write property. The compiler doesn't create properties for primary constructor
parameters in class and struct types that don't include record modifier.
The following example defines a public record that uses positional parameters to
declare and instantiate a record. It then prints the type name and property values:
C#Examples
public record Person(string FirstName, string LastName );
public static class Program
{
    public static void Main()
    {
        Person person = new("Nancy", "Davolio" );
        Console.WriteLine(person);
        // output: Person { FirstName = Nancy, LastName = Davolio }
    }The following example demonstrates value equality in records:
C#
The following example demonstrates use of a with expression to copy an immutable
object and change one of the properties:
C#}
public record Person(string FirstName, string LastName, string[] 
PhoneNumbers );
public static class Program
{
    public static void Main()
    {
        var phoneNumbers = new string[2];
        Person person1 = new("Nancy", "Davolio" , phoneNumbers);
        Person person2 = new("Nancy", "Davolio" , phoneNumbers);
        Console.WriteLine(person1 == person2); // output: True
        person1.PhoneNumbers[ 0] = "555-1234" ;
        Console.WriteLine(person1 == person2); // output: True
        Console.WriteLine(ReferenceEquals(person1, person2)); // output:  
False
    }
}
public record Person(string FirstName, string LastName )
{
    public required string[] PhoneNumbers { get; init; }
}
public class Program
{
    public static void Main()
    {
        Person person1 = new("Nancy", "Davolio" ) { PhoneNumbers = new 
string[1] };
        Console.WriteLine(person1);
        // output: Person { FirstName = Nancy, LastName = Davolio,  
PhoneNumbers = System.String[] }
        Person person2 = person1 with { FirstName = "John" };
        Console.WriteLine(person2);
        // output: Person { FirstName = John, LastName = Davolio,  
PhoneNumbers = System.String[] }
        Console.WriteLine(person1 == person2); // output: FalseFor more information, see Records (C# reference) .
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.        person2 = person1 with { PhoneNumbers = new string[1] };
        Console.WriteLine(person2);
        // output: Person { FirstName = Nancy, LastName = Davolio,  
PhoneNumbers = System.String[] }
        Console.WriteLine(person1 == person2); // output: False
        person2 = person1 with { };
        Console.WriteLine(person1 == person2); // output: True
    }
}
C# Language Specification
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
 Provide product feedbackInterfaces - define behavior for multiple
types
Article •03/18/2023
An interface contains definitions for a group of related functionalities that a non-
abstract class  or a struct  must implement. An interface may define static methods,
which must have an implementation. An interface may define a default implementation
for members. An interface may not declare instance data such as fields, auto-
implemented properties, or property-like events.
By using interfaces, you can, for example, include behavior from multiple sources in a
class. That capability is important in C# because the language doesn't support multiple
inheritance of classes. In addition, you must use an interface if you want to simulate
inheritance for structs, because they can't actually inherit from another struct or class.
You define an interface by using the interface  keyword as the following example shows.
C#
The name of an interface must be a valid C# identifier name . By convention, interface
names begin with a capital I.
Any class or struct that implements the IEquatable<T>  interface must contain a
definition for an Equals  method that matches the signature that the interface specifies.
As a result, you can count on a class that implements IEquatable<T> to contain an
Equals method with which an instance of the class can determine whether it's equal to
another instance of the same class.
The definition of IEquatable<T> doesn't provide an implementation for Equals. A class
or struct can implement multiple interfaces, but a class can only inherit from a single
class.
For more information about abstract classes, see Abstract and Sealed Classes and Class
Members .
Interfaces can contain instance methods, properties, events, indexers, or any
combination of those four member types. Interfaces may contain static constructors,interface  IEquatable <T> 
{ 
    bool Equals(T obj); 
} fields, constants, or operators. Beginning with C# 11, interface members that aren't
fields may be static abstract. An interface can't contain instance fields, instance
constructors, or finalizers. Interface members are public by default, and you can
explicitly specify accessibility modifiers, such as public, protected, internal, private,
protected internal, or private protected. A private member must have a default
implementation.
To implement an interface member, the corresponding member of the implementing
class must be public, non-static, and have the same name and signature as the interface
member.
A class or struct that implements an interface must provide an implementation for all
declared members without a default implementation provided by the interface.
However, if a base class implements an interface, any class that's derived from the base
class inherits that implementation.
The following example shows an implementation of the IEquatable<T>  interface. The
implementing class, Car, must provide an implementation of the Equals  method.
C#
Properties and indexers of a class can define extra accessors for a property or indexer
that's defined in an interface. For example, an interface might declare a property that７ Note
When an interface declares static members, a type implementing that interface may
also declare static members with the same signature. Those are distinct and
uniquely identified by the type declaring the member. The static member declared
in a type doesn 't override the static member declared in the interface.
public class Car : IEquatable <Car> 
{ 
    public string? Make { get; set; } 
    public string? Model { get; set; } 
    public string? Year { get; set; } 
    // Implementation of IEquatable<T> interface  
    public bool Equals(Car? car ) 
    { 
        return (this.Make, this.Model, this.Year) ==  
            (car?.Make, car?.Model, car?.Year);  
    } 
} has a get accessor. The class that implements the interface can declare the same
property with both a get and set accessor. However, if the property or indexer uses
explicit implementation, the accessors must match. For more information about explicit
implementation, see Explicit Interface Implementation  and Interface Properties .
Interfaces can inherit from one or more interfaces. The derived interface inherits the
members from its base interfaces. A class that implements a derived interface must
implement all members in the derived interface, including all members of the derived
interface's base interfaces. That class may be implicitly converted to the derived
interface or any of its base interfaces. A class might include an interface multiple times
through base classes that it inherits or through interfaces that other interfaces inherit.
However, the class can provide an implementation of an interface only one time and
only if the class declares the interface as part of the definition of the class ( class
ClassName : InterfaceName). If the interface is inherited because you inherited a base
class that implements the interface, the base class provides the implementation of the
members of the interface. However, the derived class can reimplement any virtual
interface members instead of using the inherited implementation. When interfaces
declare a default implementation of a method, any class implementing that interface
inherits that implementation (Y ou need to cast the class instance to the interface type to
access the default implementation on the Interface member).
A base class can also implement interface members by using virtual members. In that
case, a derived class can change the interface behavior by overriding the virtual
members. For more information about virtual members, see Polymorphism .
An interface has the following properties:
In C# versions earlier than 8.0, an interface is like an abstract base class with only
abstract members. A class or struct that implements the interface must implement
all its members.
Beginning with C# 8.0, an interface may define default implementations for some
or all of its members. A class or struct that implements the interface doesn't have
to implement members that have default implementations. For more information,
see default interface methods .
An interface can't be instantiated directly. Its members are implemented by any
class or struct that implements the interface.
A class or struct can implement multiple interfaces. A class can inherit a base class
and also implement one or more interfaces.Interfaces summaryGeneric classes and methods
Article •07/11/2023
Generics introduces the concept of type parameters to .NET, which make it possible to
design classes and methods that defer the specification of one or more types until the
class or method is declared and instantiated by client code. For example, by using a
generic type parameter T, you can write a single class that other client code can use
without incurring the cost or risk of runtime casts or boxing operations, as shown here:
C#
Generic classes and methods combine reusability, type safety, and efficiency in a way
that their non-generic counterparts cannot. Generics are most frequently used with
collections and the methods that operate on them. The System.Collections.Generic
namespace contains several generic-based collection classes. The non-generic
collections, such as ArrayList  are not recommended and are maintained for compatibility
purposes. For more information, see Generics in .NET .
You can also create custom generic types and methods to provide your own generalized
solutions and design patterns that are type-safe and efficient. The following code
example shows a simple generic linked-list class for demonstration purposes. (In most
cases, you should use the List<T>  class provided by .NET instead of creating your own.)// Declare the generic class.
public class GenericList <T>
{
    public void Add(T input) { }
}
class TestGenericList
{
    private class ExampleClass  { }
    static void Main()
    {
        // Declare a list of type int.
        GenericList< int> list1 = new GenericList< int>();
        list1.Add( 1);
        // Declare a list of type string.
        GenericList< string> list2 = new GenericList< string>();
        list2.Add( "");
        // Declare a list of type ExampleClass.
        GenericList<ExampleClass> list3 = new GenericList<ExampleClass>();
        list3.Add( new ExampleClass());
    }
}The type parameter T is used in several locations where a concrete type would
ordinarily be used to indicate the type of the item stored in the list. It is used in the
following ways:
As the type of a method parameter in the AddHead method.
As the return type of the Data property in the nested Node class.
As the type of the private member data in the nested class.
T is available to the nested Node class. When GenericList<T> is instantiated with a
concrete type, for example as a GenericList<int>, each occurrence of T will be replaced
with int.
C#
// type parameter T in angle brackets
public class GenericList <T>
{
    // The nested class is also generic on T.
    private class Node
    {
        // T used in non-generic constructor.
        public Node(T t)
        {
            next = null;
            data = t;
        }
        private Node? next;
        public Node? Next
        {
            get { return next; }
            set { next = value; }
        }
        // T as private member data type.
        private T data;
        // T as return type of property.
        public T Data
        {
            get { return data; }
            set { data = value; }
        }
    }
    private Node? head;
    // constructor
    public GenericList ()
    {
        head = null;The following code example shows how client code uses the generic GenericList<T>
class to create a list of integers. Simply by changing the type argument, the following
code could easily be modified to create lists of strings or any other custom type:
C#    }
    // T as method parameter type:
    public void AddHead(T t)
    {
        Node n = new Node(t);
        n.Next = head;
        head = n;
    }
    public IEnumerator<T> GetEnumerator ()
    {
        Node? current = head;
        while (current != null)
        {
            yield return current.Data;
            current = current.Next;
        }
    }
}
class TestGenericList
{
    static void Main()
    {
        // int is the type argument
        GenericList< int> list = new GenericList< int>();
        for (int x = 0; x < 10; x++)
        {
            list.AddHead(x);
        }
        foreach (int i in list)
        {
            System.Console.Write(i + " ");
        }
        System.Console.WriteLine( "\nDone" );
    }
}
７ NoteUse generic types to maximize code reuse, type safety, and performance.
The most common use of generics is to create collection classes.
The .NET class library contains several generic collection classes in the
System.Collections.Generic  namespace. The generic collections should be used
whenever possible instead of classes such as ArrayList  in the System.Collections
namespace.
You can create your own generic interfaces, classes, methods, events, and
delegates.
Generic classes may be constrained to enable access to methods on particular data
types.
Information on the types that are used in a generic data type may be obtained at
run-time by using reflection.
For more information, see the C# Language Specification .
System.Collections.Generic
Generics in .NETFollowing examples applies not only to class types, but also interface and
struct types
Generics overview
C# language specification
See alsoAnonymous types
Article •11/29/2023
Anonymous types provide a convenient way to encapsulate a set of read-only properties
into a single object without having to explicitly define a type first. The type name is
generated by the compiler and is not available at the source code level. The type of each
property is inferred by the compiler.
You create anonymous types by using the new operator together with an object
initializer. For more information about object initializers, see Object and Collection
Initializers .
The following example shows an anonymous type that is initialized with two properties
named Amount and Message.
C#
Anonymous types typically are used in the select  clause of a query expression to return
a subset of the properties from each object in the source sequence. For more
information about queries, see LINQ in C# .
Anonymous types contain one or more public read-only properties. No other kinds of
class members, such as methods or events, are valid. The expression that is used to
initialize a property cannot be null, an anonymous function, or a pointer type.
The most common scenario is to initialize an anonymous type with properties from
another type. In the following example, assume that a class exists that is named
Product. Class Product includes Color and Price properties, together with other
properties that you are not interested in. V ariable products is a collection of Product
objects. The anonymous type declaration starts with the new keyword. The declaration
initializes a new type that uses only two properties from Product. Using anonymous
types causes a smaller amount of data to be returned in the query.
If you don't specify member names in the anonymous type, the compiler gives the
anonymous type members the same name as the property being used to initialize them.
You provide a name for a property that's being initialized with an expression, as shownvar v = new { Amount = 108, Message = "Hello" };
// Rest the mouse pointer over v.Amount and v.Message in the following
// statement to verify that their inferred types are int and string.
Console.WriteLine(v.Amount + v.Message);in the previous example. In the following example, the names of the properties of the
anonymous type are Color and Price.
C#
It is also possible to define a field by object of another type: class, struct or even another
anonymous type. It is done by using the variable holding this object just like in the
following example, where two anonymous types are created using already instantiated
user-defined types. In both cases the product field in the anonymous type shipment
and shipmentWithBonus will be of type Product containing it's default values of each
field. And the bonus field will be of anonymous type created by the compiler.
C#
Typically, when you use an anonymous type to initialize a variable, you declare the
variable as an implicitly typed local variable by using var. The type name cannot be
specified in the variable declaration because only the compiler has access to the
underlying name of the anonymous type. For more information about var, see Implicitly
Typed Local V ariables .
You can create an array of anonymously typed elements by combining an implicitly
typed local variable and an implicitly typed array, as shown in the following example.
C#var productQuery =
    from prod in products
    select new { prod.Color, prod.Price };
foreach (var v in productQuery)
{
    Console.WriteLine( "Color={0}, Price={1}" , v.Color, v.Price);
}
 Tip
You can use .NET style rule IDE0037  to enforce whether inferred or explicit member
names are preferred.
var product = new Product();
var bonus = new { note = "You won!"  };
var shipment = new { address = "Nowhere St." , product };
var shipmentWithBonus = new { address = "Somewhere St." , product, bonus };Anonymous types are class  types that derive directly from object , and that cannot be
cast to any type except object . The compiler provides a name for each anonymous type,
although your application cannot access it. From the perspective of the common
language runtime, an anonymous type is no different from any other reference type.
If two or more anonymous object initializers in an assembly specify a sequence of
properties that are in the same order and that have the same names and types, the
compiler treats the objects as instances of the same type. They share the same
compiler-generated type information.
Anonymous types support non-destructive mutation in the form of with expressions .
This enables you to create a new instance of an anonymous type where one or more
properties have new values:
C#
You cannot declare a field, a property, an event, or the return type of a method as
having an anonymous type. Similarly, you cannot declare a formal parameter of a
method, property, constructor, or indexer as having an anonymous type. T o pass an
anonymous type, or a collection that contains anonymous types, as an argument to a
method, you can declare the parameter as type object. However, using object for
anonymous types defeats the purpose of strong typing. If you must store query results
or pass them outside the method boundary, consider using an ordinary named struct or
class instead of an anonymous type.
Because the Equals  and GetHashCode  methods on anonymous types are defined in
terms of the Equals and GetHashCode methods of the properties, two instances of the
same anonymous type are equal only if all their properties are equal.var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = 
"grape", diam = 1 }};
var apple = new { Item = "apples" , Price = 1.35 };
var onSale = apple with { Price = 0.79 };
Console.WriteLine(apple);
Console.WriteLine(onSale);
７ Note
The accessibility lev el of an anonymous type is internal, hence two anonymous
types defined in different assemblies are not of the same type. Therefore instancesAnonymous types do override the ToString  method, concatenating the name and
ToString output of every property surrounded by curly braces.of anonymous types can't be equal to each other when defined in different
assemblies, even when having all their properties equal.
var v = new { Title = "Hello", Age = 24 };
Console.WriteLine(v.ToString()); // "{ Title = Hello, Age = 24 }"
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
 Provide product feedbackOverview of classes, structs, and records
in C#
Article •09/21/2022
In C#, the definition of a type—a class, struct, or record—is like a blueprint that specifies
what the type can do. An object is basically a block of memory that has been allocated
and configured according to the blueprint. This article provides an overview of these
blueprints and their features. The next article in this series  introduces objects.
Encapsulation  is sometimes referred to as the first pillar or principle of object-oriented
programming. A class or struct can specify how accessible each of its members is to
code outside of the class or struct. Methods and variables that aren't intended to be
used from outside of the class or assembly can be hidden to limit the potential for
coding errors or malicious exploits. For more information, see the Object-oriented
programming  tutorial.
The member s of a type include all methods, fields, constants, properties, and events. In
C#, there are no global variables or methods as there are in some other languages. Even
a program's entry point, the Main method, must be declared within a class or struct
(implicitly when you use top-level statements ).
The following list includes all the various kinds of members that may be declared in a
class, struct, or record.
Fields
Constants
Properties
Methods
Constructors
Events
Finalizers
Indexers
Operators
Nested T ypesEncapsulation
MembersFor more information, see Members .
Some methods and properties are meant to be called or accessed from code outside a
class or struct, known as client c ode. Other methods and properties might be only for
use in the class or struct itself. It's important to limit the accessibility of your code so
that only the intended client code can reach it. Y ou specify how accessible your types
and their members are to client code by using the following access modifiers:
public
protected
internal
protected internal
private
private protected .
The default accessibility is private.
Classes (but not structs) support the concept of inheritance. A class that derives from
another class, called the base class , automatically contains all the public, protected, and
internal members of the base class except its constructors and finalizers.
Classes may be declared as abstract , which means that one or more of their methods
have no implementation. Although abstract classes cannot be instantiated directly, they
can serve as base classes for other classes that provide the missing implementation.
Classes can also be declared as sealed  to prevent other classes from inheriting from
them.
For more information, see Inheritance  and Polymorphism .
Classes, structs, and records can implement multiple interfaces. T o implement from an
interface means that the type implements all the methods defined in the interface. For
more information, see Interfaces .Accessibility
Inheritance
Interfaces
Generic TypesClasses, structs, and records can be defined with one or more type parameters. Client
code supplies the type when it creates an instance of the type. For example, the List<T>
class in the System.Collections.Generic  namespace is defined with one type parameter.
Client code creates an instance of a List<string> or List<int> to specify the type that
the list will hold. For more information, see Generics .
Classes (but not structs or records) can be declared as static. A static class can contain
only static members and can't be instantiated with the new keyword. One copy of the
class is loaded into memory when the program loads, and its members are accessed
through the class name. Classes, structs, and records can contain static members. For
more information, see Static classes and static class members .
A class, struct, or record can be nested within another class, struct, or record. For more
information, see Nested T ypes.
You can define part of a class, struct, or method in one code file and another part in a
separate code file. For more information, see Partial Classes and Methods .
You can instantiate and initialize class or struct objects, and collections of objects, by
assigning values to its properties. For more information, see How to initialize objects by
using an object initializer .
In situations where it isn't convenient or necessary to create a named class you use
anonymous types. Anonymous types are defined by their named data members. For
more information, see Anonymous types .Static Types
Nested Types
Partial Types
Object Initializers
Anonymous Types
Extension MethodsYou can "extend" a class without creating a derived class by creating a separate type.
That type contains methods that can be called as if they belonged to the original type.
For more information, see Extension methods .
Within a class or struct method, you can use implicit typing to instruct the compiler to
determine a variable's type at compile time. For more information, see var (C#
reference) .
You can add the record modifier to a class or a struct. R ecords are types with built-in
behavior for value-based equality. A record (either record class or record struct)
provides the following features:
Concise syntax for creating a reference type with immutable properties.
Value equality. T wo variables of a record type are equal if they have the same type,
and if, for every field, the values in both records are equal. Classes use reference
equality: two variables of a class type are equal if they refer to the same object.
Concise syntax for nondestructive mutation. A with expression lets you create a
new record instance that is a copy of an existing instance but with specified
property values changed.
Built-in formatting for display. The ToString method prints the record type name
and the names and values of public properties.
Support for inheritance hierarchies in record classes. R ecord classes support
inheritance. R ecord structs don't support inheritance.
For more information, see Records .
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.Implicitly Typed Local Variables
Records
C# Language Specification
６ Collaborat e with us on
GitHub.NET feedb ackThe source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackObjects - create instances of types
Article •09/17/2021
A class or struct definition is like a blueprint that specifies what the type can do. An
object is basically a block of memory that has been allocated and configured according
to the blueprint. A program may create many objects of the same class. Objects are also
called instances, and they can be stored in either a named variable or in an array or
collection. Client code is the code that uses these variables to call the methods and
access the public properties of the object. In an object-oriented language such as C#, a
typical program consists of multiple objects interacting dynamically.
Because classes are reference types, a variable of a class object holds a reference to the
address of the object on the managed heap. If a second variable of the same type is
assigned to the first variable, then both variables refer to the object at that address. This
point is discussed in more detail later in this article.
Instances of classes are created by using the new operator . In the following example,
Person is the type and person1 and person2 are instances, or objects, of that type.
C#７ Note
Static types behave differently than what is described here. For more information,
see Static Classes and S tatic Class Member s.
Struct Instances vs. Class Instances
public class Person 
{ 
    public string Name { get; set; } 
    public int Age { get; set; } 
    public Person(string name, int age) 
    { 
        Name = name;  
        Age = age;  
    } 
    // Other properties, methods, events...  
} 
class Program 
{ 
    static void Main() Because structs are value types, a variable of a struct object holds a copy of the entire
object. Instances of structs can also be created by using the new operator, but this isn't
required, as shown in the following example:
C#    { 
        Person person1 = new Person( "Leopold" , 6); 
        Console.WriteLine( "person1 Name = {0} Age = {1}" , person1.Name,  
person1.Age);  
        // Declare new person, assign person1 to it.  
        Person person2 = person1;
        // Change the name of person2, and person1 also changes.  
        person2.Name = "Molly"; 
        person2.Age = 16; 
        Console.WriteLine( "person2 Name = {0} Age = {1}" , person2.Name,  
person2.Age);  
        Console.WriteLine( "person1 Name = {0} Age = {1}" , person1.Name,  
person1.Age);  
    } 
} 
/* 
    Output:  
    person1 Name = Leopold Age = 6  
    person2 Name = Molly Age = 16
    person1 Name = Molly Age = 16
*/ 
namespace  Example; 
public struct Person 
{ 
    public string Name; 
    public int Age; 
    public Person(string name, int age) 
    { 
        Name = name;  
        Age = age;  
    } 
} 
public class Application  
{ 
    static void Main() 
    { 
        // Create  struct instance and initialize by using "new".  
        // Memory is allocated on thread stack.  
        Person p1 = new Person( "Alex", 9); 
        Console.WriteLine( "p1 Name = {0} Age = {1}" , p1.Name, p1.Age);  The memory for both p1 and p2 is allocated on the thread stack. That memory is
reclaimed along with the type or method in which it's declared. This is one reason why
structs are copied on assignment. By contrast, the memory that is allocated for a class
instance is automatically reclaimed (garbage collected) by the common language
runtime when all references to the object have gone out of scope. It isn't possible to
deterministically destroy a class object like you can in C++. For more information about
garbage collection in .NET, see Garbage Collection .
When you compare two objects for equality, you must first distinguish whether you
want to know whether the two variables represent the same object in memory, or
whether the values of one or more of their fields are equivalent. If you're intending to
compare values, you must consider whether the objects are instances of value types
(structs) or reference types (classes, delegates, arrays).        // Create  new struct object. Note that  struct can be initialized  
        // without using "new".  
        Person p2 = p1;  
        // Assign values to p2 members.  
        p2.Name = "Spencer" ; 
        p2.Age = 7; 
        Console.WriteLine( "p2 Name = {0} Age = {1}" , p2.Name, p2.Age);  
        // p1 values remain unchanged because p2 is  copy.  
        Console.WriteLine( "p1 Name = {0} Age = {1}" , p1.Name, p1.Age);  
    } 
} 
/* 
    Output:  
    p1 Name = Alex Age = 9  
    p2 Name = Spencer Age = 7  
    p1 Name = Alex Age = 9  
*/ 
７ Note
The allocation and deallocation of memory on the managed heap is highly
optimized in the common language runtime. In most cases there is no significant
difference in the performance cost of allocating a class instance on the heap versus
allocating a struct instance on the stack.
Object Identity  vs. Value EqualityTo determine whether two class instances refer to the same location in memory
(which means that they have the same identity ), use the static Object.Equals
method. ( System.Object  is the implicit base class for all value types and reference
types, including user-defined structs and classes.)
To determine whether the instance fields in two struct instances have the same
values, use the ValueT ype.Equals  method. Because all structs implicitly inherit from
System.V alueT ype, you call the method directly on your object as shown in the
following example:
C#
The System.V alueT ype implementation of Equals uses boxing and reflection in
some cases. For information about how to provide an efficient equality algorithm
that is specific to your type, see How to define value equality for a type . Records
are reference types that use value semantics for equality.
To determine whether the values of the fields in two class instances are equal, you
might be able to use the Equals  method or the == operator . However, only use
them if the class has overridden or overloaded them to provide a custom definition
of what "equality" means for objects of that type. The class might also implement
the IEquatable<T>  interface or the IEqualityComparer<T>  interface. Both
interfaces provide methods that can be used to test value equality. When
designing your own classes that override Equals, make sure to follow the// Person is defined in the previous example.  
//public struct Person  
//{ 
//    public string Name;  
//    public int Age;  
//    public Person(string name, int age)  
//    { 
//        Name = name;  
//        Age = age;  
//    } 
//} 
Person p1 = new Person( "Wallace" , 75); 
Person p2 = new Person( "", 42); 
p2.Name = "Wallace" ; 
p2.Age = 75; 
if (p2.Equals(p1))  
    Console.WriteLine( "p2 and p1 have the same values." ); 
// Output: p2 and p1 have the same values.  guidelines stated in How to define value equality for a type  and
Object.Equals(Object) .
For more information:
Classes
Constructors
Finalizers
Events
object
Inheritance
class
Structure types
new Operator
Common T ype S ystemRelated SectionsInheritance - derive types to create
more specialized behavior
Article •02/16/2022
Inheritance, together with encapsulation and polymorphism, is one of the three primary
characteristics of object-oriented programming. Inheritance enables you to create new
classes that reuse, extend, and modify the behavior defined in other classes. The class
whose members are inherited is called the base class , and the class that inherits those
members is called the derived class . A derived class can have only one direct base class.
However, inheritance is transitive. If ClassC is derived from ClassB, and ClassB is
derived from ClassA, ClassC inherits the members declared in ClassB and ClassA.
Conceptually, a derived class is a specialization of the base class. For example, if you
have a base class Animal, you might have one derived class that is named Mammal and
another derived class that is named Reptile. A Mammal is an Animal, and a Reptile is an
Animal, but each derived class represents different specializations of the base class.
Interface declarations may define a default implementation for its members. These
implementations are inherited by derived interfaces, and by classes that implement
those interfaces. For more information on default interface methods, see the article on
interfaces .
When you define a class to derive from another class, the derived class implicitly gains
all the members of the base class, except for its constructors and finalizers. The derived
class reuses the code in the base class without having to reimplement it. Y ou can add
more members in the derived class. The derived class extends the functionality of the
base class.
The following illustration shows a class WorkItem that represents an item of work in
some business process. Like all classes, it derives from System.Object  and inherits all its
methods. WorkItem adds six members of its own. These members include a constructor,
because constructors aren't inherited. Class ChangeRequest inherits from WorkItem and
represents a particular kind of work item. ChangeRequest adds two more members to the
members that it inherits from WorkItem and from Object . It must add its own
constructor, and it also adds originalItemID. Property originalItemID enables the７ Note
Structs do not support inheritance, but they can implement interfaces.ChangeRequest instance to be associated with the original WorkItem to which the change
request applies.
The following example shows how the class relationships demonstrated in the previous
illustration are expressed in C#. The example also shows how WorkItem overrides the
virtual method Object.T oString , and how the ChangeRequest class inherits the WorkItem
implementation of the method. The first block defines the classes:
C#
// WorkItem implicitly inherits from the Object class.  
public class WorkItem  
{ 
    // Static field currentID stores the job ID of the last WorkItem that  
    // has been created.  
    private static int currentID;  
    //Properties.  
    protected  int ID { get; set; } 
    protected  string Title { get; set; } 
    protected  string Description { get; set; } 
    protected  TimeSpan jobLength { get; set; }
    // Default constructor. If a derived class does not invoke a base-  
    // class constructor explicitly, the default constructor is called  
    // implicitly.  
    public WorkItem () 
    { 
        ID = 0; 
        Title = "Default title" ; 
        Description = "Default description." ; 
        jobLength = new TimeSpan();  
    }     // Instance constructor that has three parameters.  
    public WorkItem (string title, string desc, TimeSpan joblen ) 
    { 
        this.ID = GetNextID();  
        this.Title = title;  
        this.Description = desc;  
        this.jobLength = joblen;  
    } 
    // Static constructor to initialize the static member, currentID. This  
    // constructor is called one time, automatically, before any instance  
    // of WorkItem or ChangeRequest is created, or currentID is referenced.  
    static WorkItem () => currentID = 0; 
    // currentID is a static field. It is incremented each time a new  
    // instance of WorkItem is created.  
    protected  int GetNextID () => ++currentID;  
    // Method Update enables you to update the title and job length of an  
    // existing WorkItem object.  
    public void Update(string title, TimeSpan joblen ) 
    { 
        this.Title = title;  
        this.jobLength = joblen;  
    } 
    // Virtual method override of the ToString method that is inherited  
    // from System.Object.  
    public override  string ToString () => 
        $"{this.ID} - {this.Title}"; 
} 
// ChangeRequest derives from WorkItem and adds a property (originalItemID)  
// and two constructors.  
public class ChangeRequest  : WorkItem  
{ 
    protected  int originalItemID { get; set; } 
    // Constructors. Because neither constructor calls a base-class  
    // constructor explicitly, the default constructor in the base class  
    // is called implicitly. The base class must contain a default
    // constructor.  
    // Default constructor for the derived class.  
    public ChangeRequest () { } 
    // Instance constructor that has four parameters.  
    public ChangeRequest (string title, string desc, TimeSpan jobLen,  
                         int originalID ) 
    { 
        // The following properties and the GetNexID method are inherited  
        // from WorkItem.  
        this.ID = GetNextID();  
        this.Title = title;  
        this.Description = desc;  This next block shows how to use the base and derived classes:
C#
When a base class declares a method as virtual , a derived class can override  the method
with its own implementation. If a base class declares a member as abstract , that method
must be overridden in any non-abstract class that directly inherits from that class. If a
derived class is itself abstract, it inherits abstract members without implementing them.
Abstract and virtual members are the basis for polymorphism, which is the second        this.jobLength = jobLen;  
        // Property originalItemID is a member of ChangeRequest, but not  
        // of WorkItem.  
        this.originalItemID = originalID;  
    } 
} 
// Create an instance of WorkItem by using the constructor in the  
// base class that takes three arguments.  
WorkItem item = new WorkItem( "Fix Bugs" , 
                            "Fix all bugs in my code branch" , 
                            new TimeSpan( 3, 4, 0, 0)); 
// Create an instance of ChangeRequest by using the constructor in  
// the derived class that takes four arguments.  
ChangeRequest change = new ChangeRequest( "Change Base Class Design" , 
                                        "Add members to the class" , 
                                        new TimeSpan( 4, 0, 0), 
                                        1); 
// Use the ToString method defined in WorkItem.  
Console.WriteLine(item.ToString());  
// Use the inherited Update method to change the title of the  
// ChangeRequest object.  
change.Update( "Change the Design of the Base Class" , 
    new TimeSpan( 4, 0, 0)); 
// ChangeRequest inherits WorkItem's override of ToString.  
Console.WriteLine(change.ToString());  
/* Output:  
    1 - Fix Bugs  
    2 - Change the Design of the Base Class  
*/ 
Abstract and virtual methodsprimary characteristic of object-oriented programming. For more information, see
Polymorphism .
You can declare a class as abstract  if you want to prevent direct instantiation by using
the new operator. An abstract class can be used only if a new class is derived from it. An
abstract class can contain one or more method signatures that themselves are declared
as abstract. These signatures specify the parameters and return value but have no
implementation (method body). An abstract class doesn't have to contain abstract
members; however, if a class does contain an abstract member, the class itself must be
declared as abstract. Derived classes that aren't abstract themselves must provide the
implementation for any abstract methods from an abstract base class.
An interface is a reference type that defines a set of members. All classes and structs
that implement that interface must implement that set of members. An interface may
define a default implementation for any or all of these members. A class can implement
multiple interfaces even though it can derive from only a single direct base class.
Interfaces are used to define specific capabilities for classes that don't necessarily have
an "is a" relationship. For example, the System.IEquatable<T>  interface can be
implemented by any class or struct to determine whether two objects of the type are
equivalent (however the type defines equivalence). IEquatable<T>  doesn't imply the
same kind of "is a" relationship that exists between a base class and a derived class (for
example, a Mammal is an Animal). For more information, see Interfaces .
A class can prevent other classes from inheriting from it, or from any of its members, by
declaring itself or the member as sealed .
A derived class can hide base class members by declaring members with the same name
and signature. The new modifier can be used to explicitly indicate that the member isn't
intended to be an override of the base member. The use of new isn't required, but a
compiler warning will be generated if new isn't used. For more information, seeAbstract base classes
Interfaces
Preventing  further derivation
Derived class hiding of base class membersVersioning with the Override and New K eywords  and Knowing When to Use Override
and New K eywords .Polymorphism
Article •01/31/2023
Polymorphism is often referred to as the third pillar of object-oriented programming,
after encapsulation and inheritance. P olymorphism is a Greek word that means "many-
shaped" and it has two distinct aspects:
At run time, objects of a derived class may be treated as objects of a base class in
places such as method parameters and collections or arrays. When this
polymorphism occurs, the object's declared type is no longer identical to its run-
time type.
Base classes may define and implement virtual  methods , and derived classes can
override  them, which means they provide their own definition and implementation.
At run-time, when client code calls the method, the CLR looks up the run-time type
of the object, and invokes that override of the virtual method. In your source code
you can call a method on a base class, and cause a derived class's version of the
method to be executed.
Virtual methods enable you to work with groups of related objects in a uniform way. For
example, suppose you have a drawing application that enables a user to create various
kinds of shapes on a drawing surface. Y ou don't know at compile time which specific
types of shapes the user will create. However, the application has to keep track of all the
various types of shapes that are created, and it has to update them in response to user
mouse actions. Y ou can use polymorphism to solve this problem in two basic steps:
1. Create a class hierarchy in which each specific shape class derives from a common
base class.
2. Use a virtual method to invoke the appropriate method on any derived class
through a single call to the base class method.
First, create a base class called Shape, and derived classes such as Rectangle, Circle,
and Triangle. Give the Shape class a virtual method called Draw, and override it in each
derived class to draw the particular shape that the class represents. Create a
List<Shape> object and add a Circle, Triangle, and Rectangle to it.
C#
public class Shape 
{ 
    // A few example members  
    public int X { get; private set; } 
    public int Y { get; private set; } 
    public int Height { get; set; } To update the drawing surface, use a foreach  loop to iterate through the list and call the
Draw method on each Shape object in the list. Even though each object in the list has a
declared type of Shape, it's the run-time type (the overridden version of the method in
each derived class) that will be invoked.
C#    public int Width { get; set; } 
    // Virtual method  
    public virtual void Draw() 
    { 
        Console.WriteLine( "Performing base class drawing tasks" ); 
    } 
} 
public class Circle : Shape 
{ 
    public override  void Draw() 
    { 
        // Code to draw a circle...  
        Console.WriteLine( "Drawing a circle" ); 
        base.Draw();  
    } 
} 
public class Rectangle  : Shape 
{ 
    public override  void Draw() 
    { 
        // Code to draw a rectangle...  
        Console.WriteLine( "Drawing a rectangle" ); 
        base.Draw();  
    } 
} 
public class Triangle  : Shape 
{ 
    public override  void Draw() 
    { 
        // Code to draw a triangle...  
        Console.WriteLine( "Drawing a triangle" ); 
        base.Draw();  
    } 
} 
// Polymorphism at work #1: a Rectangle, Triangle and Circle  
// can all be used wherever a Shape is expected. No cast is  
// required because an implicit conversion exists from a derived  
// class to its base class.  
var shapes = new List<Shape>  
{ 
    new Rectangle(),  
    new Triangle(),  In C#, every type is polymorphic because all types, including user-defined types, inherit
from Object .
When a derived class inherits from a base class, it includes all the members of the base
class. All the behavior declared in the base class is part of the derived class. That enables
objects of the derived class to be treated as objects of the base class. Access modifiers
(public, protected, private and so on) determine if those members are accessible from
the derived class implementation. Virtual methods gives the designer different choices
for the behavior of the derived class:
The derived class may override virtual members in the base class, defining new
behavior.
The derived class may inherit the closest base class method without overriding it,
preserving the existing behavior but enabling further derived classes to override
the method.
The derived class may define new non-virtual implementation of those members
that hide the base class implementations.
A derived class can override a base class member only if the base class member is
declared as virtual  or abstract . The derived member must use the override  keyword to
explicitly indicate that the method is intended to participate in virtual invocation. The
following code provides an example:    new Circle()  
}; 
// Polymorphism at work #2: the virtual method Draw is  
// invoked on each of the derived classes, not the base class.  
foreach (var shape in shapes)  
{ 
    shape.Draw();  
} 
/* Output:  
    Drawing a rectangle  
    Performing base class drawing tasks  
    Drawing a triangle  
    Performing base class drawing tasks  
    Drawing a circle  
    Performing base class drawing tasks  
*/ 
Polymorphism overview
Virtual membersC#
Fields can't be virtual; only methods, properties, events, and indexers can be virtual.
When a derived class overrides a virtual member, that member is called even when an
instance of that class is being accessed as an instance of the base class. The following
code provides an example:
C#
Virtual methods and properties enable derived classes to extend a base class without
needing to use the base class implementation of a method. For more information, see
Versioning with the Override and New K eywords . An interface provides another way to
define a method or set of methods whose implementation is left to derived classes.
If you want your derived class to have a member with the same name as a member in a
base class, you can use the new keyword to hide the base class member. The new
keyword is put before the return type of a class member that is being replaced. The
following code provides an example:
C#public class BaseClass  
{ 
    public virtual void DoWork() { }
    public virtual int WorkProperty  
    { 
        get { return 0; } 
    } 
} 
public class DerivedClass  : BaseClass  
{ 
    public override  void DoWork() { } 
    public override  int WorkProperty  
    { 
        get { return 0; } 
    } 
} 
DerivedClass B = new DerivedClass();  
B.DoWork();  // Calls the new method.  
BaseClass A = B;  
A.DoWork();  // Also calls the new method.  
Hide base class members with new membersHidden base class members may be accessed from client code by casting the instance of
the derived class to an instance of the base class. For example:
C#
Virtual members remain virtual, regardless of how many classes have been declared
between the virtual member and the class that originally declared it. If class A declares a
virtual member, and class B derives from A, and class C derives from B, class C inherits
the virtual member, and may override it, regardless of whether class B declared an
override for that member. The following code provides an example:
C#public class BaseClass  
{ 
    public void DoWork() { WorkField++; }  
    public int WorkField;  
    public int WorkProperty  
    { 
        get { return 0; } 
    } 
} 
public class DerivedClass  : BaseClass  
{ 
    public new void DoWork() { WorkField++; }  
    public new int WorkField;  
    public new int WorkProperty  
    { 
        get { return 0; } 
    } 
} 
DerivedClass B = new DerivedClass();  
B.DoWork();  // Calls the new method.  
BaseClass A = (BaseClass)B;  
A.DoWork();  // Calls the old method.  
Prevent derived classes from overriding virtual members
public class A 
{ 
    public virtual void DoWork() { }
} 
public class B : A 
{ A derived class can stop virtual inheritance by declaring an override as sealed . Stopping
inheritance requires putting the sealed keyword before the override keyword in the
class member declaration. The following code provides an example:
C#
In the previous example, the method DoWork is no longer virtual to any class derived
from C. It's still virtual for instances of C, even if they're cast to type B or type A. Sealed
methods can be replaced by derived classes by using the new keyword, as the following
example shows:
C#
In this case, if DoWork is called on D using a variable of type D, the new DoWork is called.
If a variable of type C, B, or A is used to access an instance of D, a call to DoWork will
follow the rules of virtual inheritance, routing those calls to the implementation of
DoWork on class C.
A derived class that has replaced or overridden a method or property can still access the
method or property on the base class using the base keyword. The following code
provides an example:
C#    public override  void DoWork() { } 
} 
public class C : B 
{ 
    public sealed override  void DoWork() { } 
} 
public class D : C 
{ 
    public new void DoWork() { } 
} 
Access base class virtual members from derived classes
public class Base 
{ 
    public virtual void DoWork() {/*...*/ } 
} 
public class Derived : Base For more information, see base.{ 
    public override  void DoWork() 
    { 
        //Perform Derived's work here  
        //... 
        // Call DoWork on base class  
        base.DoWork();  
    } 
} 
７ Note
It is recommended that virtual members use base to call the base class
implementation of that member in their own implementation. Letting the base class
behavior occur enables the derived class to concentrate on implementing behavior
specific to the derived class. If the base class implementation is not called, it is up
to the derived class to make their behavior compatible with the behavior of the
base class.Pattern matching overview
Article •12/04/2022
Pattern mat ching  is a technique where you test an expression to determine if it has
certain characteristics. C# pattern matching provides more concise syntax for testing
expressions and taking action when an expression matches. The " is expression" supports
pattern matching to test an expression and conditionally declare a new variable to the
result of that expression. The " switch  expression" enables you to perform actions based
on the first matching pattern for an expression. These two expressions support a rich
vocabulary of patterns.
This article provides an overview of scenarios where you can use pattern matching.
These techniques can improve the readability and correctness of your code. For a full
discussion of all the patterns you can apply, see the article on patterns  in the language
reference.
One of the most common scenarios for pattern matching is to ensure values aren't
null. You can test and convert a nullable value type to its underlying type while testing
for null using the following example:
C#
The preceding code is a declar ation p attern to test the type of the variable, and assign it
to a new variable. The language rules make this technique safer than many others. The
variable number is only accessible and assigned in the true portion of the if clause. If
you try to access it elsewhere, either in the else clause, or after the if block, the
compiler issues an error. Secondly, because you're not using the == operator, this
pattern works when a type overloads the == operator. That makes it an ideal way to
check null reference values, adding the not pattern:Null checks
int? maybe = 12; 
if (maybe is int number)  
{ 
    Console.WriteLine( $"The nullable int 'maybe' has the value {number} "); 
} 
else 
{ 
    Console.WriteLine( "The nullable int 'maybe' doesn't hold a value" ); 
} C#
The preceding example used a constant p attern to compare the variable to null. The
not is a logical p attern that matches when the negated pattern doesn't match.
Another common use for pattern matching is to test a variable to see if it matches a
given type. For example, the following code tests if a variable is non-null and
implements the System.Collections.Generic.IList<T>  interface. If it does, it uses the
ICollection<T>.Count  property on that list to find the middle index. The declaration
pattern doesn't match a null value, regardless of the compile-time type of the variable.
The code below guards against null, in addition to guarding against a type that doesn't
implement IList.
C#
The same tests can be applied in a switch expression to test a variable against multiple
different types. Y ou can use that information to create better algorithms based on the
specific run-time type.string? message = "This is not the null string" ; 
if (message is not null) 
{ 
    Console.WriteLine(message);  
} 
Type tests
public static T MidPoint<T>(IEnumerable<T> sequence)  
{ 
    if (sequence is IList<T> list)  
    { 
        return list[list.Count / 2]; 
    } 
    else if (sequence is null) 
    { 
        throw new ArgumentNullException( nameof(sequence), "Sequence can't be  
null."); 
    } 
    else 
    { 
        int halfLength = sequence.Count() / 2 - 1; 
        if (halfLength < 0) halfLength = 0; 
        return sequence.Skip(halfLength).First();  
    } 
} You can also test a variable to find a match on specific values. The following code shows
one example where you test a value against all possible values declared in an
enumeration:
C#
The previous example demonstrates a method dispatch based on the value of an
enumeration. The final _ case is a discard pattern that matches all values. It handles any
error conditions where the value doesn't match one of the defined enum values. If you
omit that switch arm, the compiler warns that you haven't handled all possible input
values. At run time, the switch expression throws an exception if the object being
examined doesn't match any of the switch arms. Y ou could use numeric constants
instead of a set of enum values. Y ou can also use this similar technique for constant
string values that represent the commands:
C#
The preceding example shows the same algorithm, but uses string values instead of an
enum. Y ou would use this scenario if your application responds to text commands
instead of a regular data format. S tarting with C# 11, you can also use a Span<char> or a
ReadOnlySpan<char>to test for constant string values, as shown in the following sample:Compare discrete values
public State PerformOperation (Operation command ) => 
   command switch 
   { 
       Operation.SystemTest => RunDiagnostics(),  
       Operation.Start => StartSystem(),  
       Operation.Stop => StopSystem(),  
       Operation.Reset => ResetToReady(),  
       _ => throw new ArgumentException( "Invalid enum value for command" , 
nameof(command)),  
   }; 
public State PerformOperation (string command ) => 
   command switch 
   { 
       "SystemTest"  => RunDiagnostics(),  
       "Start" => StartSystem(),  
       "Stop" => StopSystem(),  
       "Reset" => ResetToReady(),  
       _ => throw new ArgumentException( "Invalid string value for command" , 
nameof(command)),  
   }; C#
In all these examples, the discard pattern ensures that you handle every input. The
compiler helps you by making sure every possible input value is handled.
You can use relational p atterns to test how a value compares to constants. For example,
the following code returns the state of water based on the temperature in F ahrenheit:
C#
The preceding code also demonstrates the conjunctive and logical p attern to check that
both relational patterns match. Y ou can also use a disjunctive or pattern to check that
either pattern matches. The two relational patterns are surrounded by parentheses,
which you can use around any pattern for clarity. The final two switch arms handle the
cases for the melting point and the boiling point. Without those two arms, the compiler
warns you that your logic doesn't cover every possible input.
The preceding code also demonstrates another important feature the compiler provides
for pattern matching expressions: The compiler warns you if you don't handle every
input value. The compiler also issues a warning if a switch arm is already handled by a
previous switch arm. That gives you freedom to refactor and reorder switch expressions.
Another way to write the same expression could be:public State PerformOperation (ReadOnlySpan< char> command ) => 
   command switch 
   { 
       "SystemTest"  => RunDiagnostics(),  
       "Start" => StartSystem(),  
       "Stop" => StopSystem(),  
       "Reset" => ResetToReady(),  
       _ => throw new ArgumentException( "Invalid string value for command" , 
nameof(command)),  
   }; 
Relational patterns
string WaterState (int tempInFahrenheit ) => 
    tempInFahrenheit switch 
    { 
        (> 32) and (< 212) => "liquid" , 
        < 32 => "solid", 
        > 212 => "gas",
        32 => "solid/liquid transition" , 
        212 => "liquid / gas transition" , 
    }; C#
The key lesson in this, and any other refactoring or reordering, is that the compiler
validates that you've covered all inputs.
All the patterns you've seen so far have been checking one input. Y ou can write patterns
that examine multiple properties of an object. Consider the following Order record:
C#
The preceding positional record type declares two members at explicit positions.
Appearing first is the Items, then the order's Cost. For more information, see Records .
The following code examines the number of items and the value of an order to calculate
a discounted price:
C#
The first two arms examine two properties of the Order. The third examines only the
cost. The next checks against null, and the final matches any other value. If the Orderstring WaterState2 (int tempInFahrenheit ) => 
    tempInFahrenheit switch 
    { 
        < 32 => "solid", 
        32 => "solid/liquid transition" , 
        < 212 => "liquid" , 
        212 => "liquid / gas transition" , 
        _ => "gas", 
}; 
Multip le inputs
public record Order(int Items, decimal Cost); 
public decimal CalculateDiscount (Order order ) => 
    order switch 
    { 
        { Items: > 10, Cost: > 1000.00m } => 0.10m, 
        { Items: > 5, Cost: > 500.00m } => 0.05m, 
        { Cost: > 250.00m } => 0.02m, 
        null => throw new ArgumentNullException( nameof(order), "Can't 
calculate discount on null order" ), 
        var someObject => 0m, 
    }; type defines a suitable Deconstruct  method, you can omit the property names from the
pattern and use deconstruction to examine properties:
C#
The preceding code demonstrates the positional p attern where the properties are
deconstructed for the expression.
You can check elements in a list or an array using a list pattern. A list pattern  provides a
means to apply a pattern to any element of a sequence. In addition, you can apply the
discard pattern (_) to match any element, or apply a slice pattern to match zero or more
elements.
List patterns are a valuable tool when data doesn't follow a regular structure. Y ou can
use pattern matching to test the shape and values of the data instead of transforming it
into a set of objects.
Consider the following excerpt from a text file containing bank transactions:
Output
It's a CSV format, but some of the rows have more columns than others. Even worse for
processing, one column in the WITHDRAWAL type has user-generated text and can containpublic decimal CalculateDiscount (Order order ) => 
    order switch 
    { 
        ( > 10,  > 1000.00m) => 0.10m, 
        ( > 5, > 50.00m) => 0.05m, 
        { Cost: > 250.00m } => 0.02m, 
        null => throw new ArgumentNullException( nameof(order), "Can't 
calculate discount on null order" ), 
        var someObject => 0m, 
    }; 
List patterns
04-01-2020, DEPOSIT,    Initial deposit,            2250.00  
04-15-2020, DEPOSIT,    Refund,                      125.65  
04-18-2020, DEPOSIT,    Paycheck,                    825.65  
04-22-2020, WITHDRAWAL, Debit,           Groceries,  255.73  
05-01-2020, WITHDRAWAL, #1102,           Rent, apt, 2100.00  
05-02-2020, INTEREST,                                  0.65  
05-07-2020, WITHDRAWAL, Debit,           Movies,      12.57  
04-15-2020, FEE,                                       5.55  a comma in the text. A list pattern that includes the discard pattern, constant pattern and
var pattern to capture the value processes data in this format:
C#
The preceding example takes a string array, where each element is one field in the row.
The switch expression keys on the second field, which determines the kind of
transaction, and the number of remaining columns. Each row ensures the data is in the
correct format. The discard pattern ( _) skips the first field, with the date of the
transaction. The second field matches the type of transaction. R emaining element
matches skip to the field with the amount. The final match uses the var pattern to
capture the string representation of the amount. The expression calculates the amount
to add or subtract from the balance.
List p atterns enable you to match on the shape of a sequence of data elements. Y ou use
the discard and slice patterns to match the location of elements. Y ou use other patterns
to match characteristics about individual elements.
This article provided a tour of the kinds of code you can write with pattern matching in
C#. The following articles show more examples of using patterns in scenarios, and the
full vocabulary of patterns available to use.
Use pattern matching to avoid 'is' check followed by a cast (style rules IDE0020 and
IDE0038)
Exploration: Use pattern matching to build your class behavior for better code
Tutorial: Use pattern matching to build type-driven and data-driven algorithmsdecimal balance = 0m; 
foreach (string[] transaction in ReadRecords ()) 
{ 
    balance += transaction switch 
    { 
        [ _, "DEPOSIT" , _, var amount ]     => decimal.Parse(amount),  
        [ _, "WITHDRAWAL" , .., var amount ] => -decimal.Parse(amount),  
        [ _, "INTEREST" , var amount ]       => decimal.Parse(amount),  
        [ _, "FEE", var fee ]               => - decimal.Parse(fee),  
        _                                 => throw new 
InvalidOperationException( $"Record {string.Join(", ", transaction)}  is not 
in the expected format!" ), 
    }; 
    Console.WriteLine( $"Record: {string.Join(", ", transaction)} , New 
balance: {balance:C} ");
} 
See alsoReference: P attern matchingDiscards - C# Fundamentals
Article •11/14/2023
Discards are placeholder variables that are intentionally unused in application code.
Discards are equivalent to unassigned variables; they don't have a value. A discard
communicates intent to the compiler and others that read your code: Y ou intended to
ignore the result of an expression. Y ou may want to ignore the result of an expression,
one or more members of a tuple expression, an out parameter to a method, or the
target of a pattern matching expression.
Discards make the intent of your code clear. A discard indicates that our code never
uses the variable. They enhance its readability and maintainability.
You indicate that a variable is a discard by assigning it the underscore ( _) as its name.
For example, the following method call returns a tuple in which the first and second
values are discards. area is a previously declared variable set to the third component
returned by GetCityInformation:
C#
You can use discards to specify unused input parameters of a lambda expression. For
more information, see the Input parameters of a lambda expression  section of the
Lambda expressions  article.
When _ is a valid discard, attempting to retrieve its value or use it in an assignment
operation generates compiler error CS0103, "The name '_' doesn't exist in the current
context". This error is because _ isn't assigned a value, and may not even be assigned a
storage location. If it were an actual variable, you couldn't discard more than one value,
as the previous example did.
Discards are useful in working with tuples when your application code uses some tuple
elements but ignores others. For example, the following QueryCityDataForYears method
returns a tuple with the name of a city, its area, a year, the city's population for that year,
a second year, and the city's population for that second year. The example shows the
change in population between those two years. Of the data available from the tuple,
we're unconcerned with the city area, and we know the city name and the two dates at(_, _, area) = city.GetCityInformation(cityName);
Tuple and object deconstructiondesign-time. As a result, we're only interested in the two population values stored in the
tuple, and can handle its remaining values as discards.
C#
For more information on deconstructing tuples with discards, see Deconstructing tuples
and other types .
The Deconstruct method of a class, structure, or interface also allows you to retrieve
and deconstruct a specific set of data from an object. Y ou can use discards when you're
interested in working with only a subset of the deconstructed values. The following
example deconstructs a Person object into four strings (the first and last names, the city,
and the state), but discards the last name and the state.
C#var (_, _, _, pop1, _, pop2) = QueryCityDataForYears( "New York City" , 1960, 
2010);
Console.WriteLine( $"Population change, 1960 to 2010: {pop2 - pop1:N0} ");
static (string, double, int, int, int, int) QueryCityDataForYears( string 
name, int year1, int year2)
{
    int population1 = 0, population2 = 0;
    double area = 0;
    if (name == "New York City" )
    {
        area = 468.48;
        if (year1 == 1960)
        {
            population1 = 7781984;
        }
        if (year2 == 2010)
        {
            population2 = 8175133;
        }
        return (name, area, year1, population1, year2, population2);
    }
    return ("", 0, 0, 0, 0, 0);
}
// The example displays the following output:
//      Population change, 1960 to 2010: 393,149
using System;
namespace  Discards
{    public class Person
    {
        public string FirstName { get; set; }
        public string MiddleName { get; set; }
        public string LastName { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public Person(string fname, string mname, string lname,
                      string cityName, string stateName )
        {
            FirstName = fname;
            MiddleName = mname;
            LastName = lname;
            City = cityName;
            State = stateName;
        }
        // Return the first and last name.
        public void Deconstruct (out string fname, out string lname)
        {
            fname = FirstName;
            lname = LastName;
        }
        public void Deconstruct (out string fname, out string mname, out 
string lname)
        {
            fname = FirstName;
            mname = MiddleName;
            lname = LastName;
        }
        public void Deconstruct (out string fname, out string lname,
                                out string city, out string state)
        {
            fname = FirstName;
            lname = LastName;
            city = City;
            state = State;
        }
    }
    class Example
    {
        public static void Main()
        {
            var p = new Person( "John", "Quincy" , "Adams", "Boston" , "MA");
            // Deconstruct the person object.
            var (fName, _, city, _) = p;
            Console.WriteLine( $"Hello {fName} of {city}!");
            // The example displays the following output:
            //      Hello John of Boston!
        }For more information on deconstructing user-defined types with discards, see
Deconstructing tuples and other types .
The discard pattern can be used in pattern matching with the switch expression . Every
expression, including null, always matches the discard pattern.
The following example defines a ProvidesFormatInfo method that uses a switch
expression to determine whether an object provides an IFormatProvider  implementation
and tests whether the object is null. It also uses the discard pattern to handle non-null
objects of any other type.
C#
When calling the Deconstruct method to deconstruct a user-defined type (an instance
of a class, structure, or interface), you can discard the values of individual out    }
}
Pattern matching with switch
object?[] objects = [CultureInfo.CurrentCulture,
                   CultureInfo.CurrentCulture.DateTimeFormat,
                   CultureInfo.CurrentCulture.NumberFormat,
                   new ArgumentException(), null];
foreach (var obj in objects)
    ProvidesFormatInfo(obj);
static void ProvidesFormatInfo (object? obj) =>
    Console.WriteLine(obj switch
    {
        IFormatProvider fmt => $"{fmt.GetType()}  object" ,
        null => "A null object reference: Its use could result in a  
NullReferenceException" ,
        _ => "Some object type without format information"
    });
// The example displays the following output:
//    System.Globalization.CultureInfo object
//    System.Globalization.DateTimeFormatInfo object
//    System.Globalization.NumberFormatInfo object
//    Some object type without format information
//    A null object reference: Its use could result in a  
NullReferenceException
Calls to methods with out parametersarguments. But you can also discard the value of out arguments when calling any
method with an out parameter.
The following example calls the DateTime.T ryParse(S tring, out DateTime)  method to
determine whether the string representation of a date is valid in the current culture.
Because the example is concerned only with validating the date string and not with
parsing it to extract the date, the out argument to the method is a discard.
C#
You can use a standalone discard to indicate any variable that you choose to ignore.
One typical use is to use an assignment to ensure that an argument isn't null. The
following code uses a discard to force an assignment. The right side of the assignment
uses the null coalescing operator  to throw an System.ArgumentNullException  when the
argument is null. The code doesn't need the result of the assignment, so it's discarded.
The expression forces a null check. The discard clarifies your intent: the result of the
assignment isn't needed or used.
C#string[] dateStrings = [ "05/01/2018 14:57:32.8" , "2018-05-01 14:57:32.8" ,
                      "2018-05-01T14:57:32.8375298-04:00" , "5/01/2018" ,
                      "5/01/2018 14:57:32.80 -07:00" ,
                      "1 May 2018 2:57:32.8 PM" , "16-05-2018 1:00:32 PM" ,
                      "Fri, 15 May 2018 20:10:57 GMT" ];
foreach (string dateString in dateStrings)
{
    if (DateTime.TryParse(dateString, out _))
        Console.WriteLine( $"'{dateString} ': valid" );
    else
        Console.WriteLine( $"'{dateString} ': invalid" );
}
// The example displays output like the following:
//       '05/01/2018 14:57:32.8': valid
//       '2018-05-01 14:57:32.8': valid
//       '2018-05-01T14:57:32.8375298-04:00': valid
//       '5/01/2018': valid
//       '5/01/2018 14:57:32.80 -07:00': valid
//       '1 May 2018 2:57:32.8 PM': valid
//       '16-05-2018 1:00:32 PM': invalid
//       'Fri, 15 May 2018 20:10:57 GMT': invalid
A standalone discard
public static void Method(string arg)
{
    _ = arg ?? throw new ArgumentNullException(paramName: nameof(arg), The following example uses a standalone discard to ignore the Task object returned by
an asynchronous operation. Assigning the task has the effect of suppressing the
exception that the operation throws as it is about to complete. It makes your intent
clear: Y ou want to discard the Task, and ignore any errors generated from that
asynchronous operation.
C#
Without assigning the task to a discard, the following code generates a compiler
warning:
C#message: "arg can't be null" );
    // Do work with arg.
}
private static async Task ExecuteAsyncMethods ()
{
    Console.WriteLine( "About to launch a task..." );
    _ = Task.Run(() =>
    {
        var iterations = 0;
        for (int ctr = 0; ctr < int.MaxValue; ctr++)
            iterations++;
        Console.WriteLine( "Completed looping operation..." );
        throw new InvalidOperationException();
    });
    await Task.Delay( 5000);
    Console.WriteLine( "Exiting after 5 second delay" );
}
// The example displays output like the following:
//       About to launch a task...
//       Completed looping operation...
//       Exiting after 5 second delay
private static async Task ExecuteAsyncMethods ()
{
    Console.WriteLine( "About to launch a task..." );
    // CS4014: Because this call is not awaited, execution of the current  
method continues before the call is completed.
    // Consider applying the 'await' operator to the result of the call.
    Task.Run(() =>
    {
        var iterations = 0;
        for (int ctr = 0; ctr < int.MaxValue; ctr++)
            iterations++;
        Console.WriteLine( "Completed looping operation..." );
        throw new InvalidOperationException();_ is also a valid identifier. When used outside of a supported context, _ is treated not
as a discard but as a valid variable. If an identifier named _ is already in scope, the use
of _ as a standalone discard can result in:
Accidental modification of the value of the in-scope _ variable by assigning it the
value of the intended discard. For example:
C#
A compiler error for violating type safety. For example:
C#
Compiler error CS0136, "A local or parameter named '_' cannot be declared in this
scope because that name is used in an enclosing local scope to define a local or
parameter." For example:
C#    });
    await Task.Delay( 5000);
    Console.WriteLine( "Exiting after 5 second delay" );
７ Note
If you run either of the preceding two samples using a debugger, the debugger will
stop the program when the exception is thrown. Without a debugger attached, the
exception is silently ignored in both cases.
private static void ShowValue (int _)
{
   byte[] arr = [ 0, 0, 1, 2];
   _ = BitConverter.ToInt32(arr, 0);
   Console.WriteLine(_);
}
 // The example displays the following output:
 //       33619968
private static bool RoundTrips (int _)
{
   string value = _.ToString();
   int newValue = 0;
   _ = Int32.TryParse( value, out newValue);
   return _ == newValue;
}
// The example displays the following compiler error:
//      error CS0029: Cannot implicitly convert type 'bool' to 'int'Remove unnecessary expression value (style rule IDE0058)
Remove unnecessary value assignment (style rule IDE0059)
Remove unused parameter (style rule IDE0060)
Deconstructing tuples and other types
is operator
switch  expression public void DoSomething (int _)
{
 var _ = GetValue(); // Error: cannot declare local _ when one is  
already in scope
}
// The example displays the following compiler error:
// error CS0136:
//       A local or parameter named '_' cannot be declared in this  
scope
//       because that name is used in an enclosing local scope
//       to define a local or parameter
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
 Provide product feedbackDeconstructing tuples and other types
Article •09/29/2022
A tuple provides a lightweight way to retrieve multiple values from a method call. But
once you retrieve the tuple, you have to handle its individual elements. W orking on an
element-by-element basis is cumbersome, as the following example shows. The
QueryCityData method returns a three-tuple, and each of its elements is assigned to a
variable in a separate operation.
C#
Retrieving multiple field and property values from an object can be equally
cumbersome: you must assign a field or property value to a variable on a member-by-
member basis.
You can retrieve multiple elements from a tuple or retrieve multiple field, property, and
computed values from an object in a single deconstr uct operation. T o deconstruct a
tuple, you assign its elements to individual variables. When you deconstruct an object,
you assign selected values to individual variables.public class Example
{
    public static void Main()
    {
        var result = QueryCityData( "New York City" );
        var city = result.Item1;
        var pop = result.Item2;
        var size = result.Item3;
         // Do something with the data.
    }
    private static (string, int, double) QueryCityData (string name)
    {
        if (name == "New York City" )
            return (name, 8175133, 468.48);
        return ("", 0, 0);
    }
}
TuplesC# features built-in support for deconstructing tuples, which lets you unpackage all the
items in a tuple in a single operation. The general syntax for deconstructing a tuple is
similar to the syntax for defining one: you enclose the variables to which each element is
to be assigned in parentheses in the left side of an assignment statement. For example,
the following statement assigns the elements of a four-tuple to four separate variables:
C#
There are three ways to deconstruct a tuple:
You can explicitly declare the type of each field inside parentheses. The following
example uses this approach to deconstruct the three-tuple returned by the
QueryCityData method.
C#
You can use the var keyword so that C# infers the type of each variable. Y ou place
the var keyword outside of the parentheses. The following example uses type
inference when deconstructing the three-tuple returned by the QueryCityData
method.
C#
You can also use the var keyword individually with any or all of the variable
declarations inside the parentheses.
C#var (name, address, city, zip) = contact.GetAddressInfo();
public static void Main()
{
    (string city, int population, double area) = QueryCityData( "New 
York City" );
    // Do something with the data.
}
public static void Main()
{
    var (city, population, area) = QueryCityData( "New York City" );
    // Do something with the data.
}This is cumbersome and isn't recommended.
Lastly, you may deconstruct the tuple into variables that have already been
declared.
C#
Beginning in C# 10, you can mix variable declaration and assignment in a
deconstruction.
C#
You can't specify a specific type outside the parentheses even if every field in the tuple
has the same type. Doing so generates compiler error CS8136, "Deconstruction 'var (...)'
form disallows a specific type for 'var'.".
You must assign each element of the tuple to a variable. If you omit any elements, the
compiler generates error CS8132, "Can't deconstruct a tuple of 'x' elements into 'y'public static void Main()
{
    (string city, var population, var area) = QueryCityData( "New York  
City");
    // Do something with the data.
}
public static void Main()
{
    string city = "Raleigh" ;
    int population = 458880;
    double area = 144.8;
    (city, population, area) = QueryCityData( "New York City" );
    // Do something with the data.
}
public static void Main()
{
    string city = "Raleigh" ;
    int population = 458880;
    (city, population, double area) = QueryCityData( "New York City" );
    // Do something with the data.
}variables."
Often when deconstructing a tuple, you're interested in the values of only some
elements. Y ou can take advantage of C#'s support for discards, which are write-only
variables whose values you've chosen to ignore. A discard is chosen by an underscore
character ("_") in an assignment. Y ou can discard as many values as you like; all are
represented by the single discard, _.
The following example illustrates the use of tuples with discards. The
QueryCityDataForYears method returns a six-tuple with the name of a city, its area, a
year, the city's population for that year, a second year, and the city's population for that
second year. The example shows the change in population between those two years. Of
the data available from the tuple, we're unconcerned with the city area, and we know
the city name and the two dates at design-time. As a result, we're only interested in the
two population values stored in the tuple, and can handle its remaining values as
discards.
C#Tuple elements with discards
using System;
public class ExampleDiscard
{
    public static void Main()
    {
        var (_, _, _, pop1, _, pop2) = QueryCityDataForYears( "New York  
City", 1960, 2010);
        Console.WriteLine( $"Population change, 1960 to 2010: {pop2 - 
pop1:N0} ");
    }
    private static (string, double, int, int, int, int) 
QueryCityDataForYears (string name, int year1, int year2)
    {
        int population1 = 0, population2 = 0;
        double area = 0;
        if (name == "New York City" )
        {
            area = 468.48;
            if (year1 == 1960)
            {
                population1 = 7781984;
            }
            if (year2 == 2010)C# doesn't offer built-in support for deconstructing non-tuple types other than the
record  and DictionaryEntry  types. However, as the author of a class, a struct, or an
interface, you can allow instances of the type to be deconstructed by implementing one
or more Deconstruct methods. The method returns void, and each value to be
deconstructed is indicated by an out parameter in the method signature. For example,
the following Deconstruct method of a Person class returns the first, middle, and last
name:
C#
You can then deconstruct an instance of the Person class named p with an assignment
like the following code:
C#
The following example overloads the Deconstruct method to return various
combinations of properties of a Person object. Individual overloads return:
A first and last name.
A first, middle, and last name.
A first name, a last name, a city name, and a state name.
C#            {
                population2 = 8175133;
            }
            return (name, area, year1, population1, year2, population2);
        }
        return ("", 0, 0, 0, 0, 0);
    }
}
// The example displays the following output:
//      Population change, 1960 to 2010: 393,149
User-defined types
public void Deconstruct (out string fname, out string mname, out string 
lname)
var (fName, mName, lName) = p;using System;
public class Person
{
    public string FirstName { get; set; }
    public string MiddleName { get; set; }
    public string LastName { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public Person(string fname, string mname, string lname,
                  string cityName, string stateName )
    {
        FirstName = fname;
        MiddleName = mname;
        LastName = lname;
        City = cityName;
        State = stateName;
    }
    // Return the first and last name.
    public void Deconstruct (out string fname, out string lname)
    {
        fname = FirstName;
        lname = LastName;
    }
    public void Deconstruct (out string fname, out string mname, out string 
lname)
    {
        fname = FirstName;
        mname = MiddleName;
        lname = LastName;
    }
    public void Deconstruct (out string fname, out string lname,
                            out string city, out string state)
    {
        fname = FirstName;
        lname = LastName;
        city = City;
        state = State;
    }
}
public class ExampleClassDeconstruction
{
    public static void Main()
    {
        var p = new Person( "John", "Quincy" , "Adams", "Boston" , "MA");
        // Deconstruct the person object.
        var (fName, lName, city, state) = p;
        Console.WriteLine( $"Hello {fName} {lName} of {city}, {state}!");Multiple Deconstruct methods having the same number of parameters are ambiguous.
You must be careful to define Deconstruct methods with different numbers of
parameters, or "arity". Deconstruct methods with the same number of parameters
cannot be distinguished during overload resolution.
Just as you do with tuples , you can use discards to ignore selected items returned by a
Deconstruct method. Each discard is defined by a variable named "_", and a single
deconstruction operation can include multiple discards.
The following example deconstructs a Person object into four strings (the first and last
names, the city, and the state) but discards the last name and the state.
C#
If you didn't author a class, struct, or interface, you can still deconstruct objects of that
type by implementing one or more Deconstruct extension methods  to return the values
in which you're interested.
The following example defines two Deconstruct extension methods for the
System.R eflection.PropertyInfo  class. The first returns a set of values that indicate the
characteristics of the property, including its type, whether it's static or instance, whether
it's read-only, and whether it's indexed. The second indicates the property's accessibility.
Because the accessibility of get and set accessors can differ, Boolean values indicate
whether the property has separate get and set accessors and, if it does, whether they
have the same accessibility. If there's only one accessor or both the get and the set
accessor have the same accessibility, the access variable indicates the accessibility of    }
}
// The example displays the following output:
//    Hello John Adams of Boston, MA!
User-defined type with discards
// Deconstruct the person object.
var (fName, _, city, _) = p;
Console.WriteLine( $"Hello {fName} of {city}!");
// The example displays the following output:
//      Hello John of Boston!
Extension methods for user-defined typesthe property as a whole. Otherwise, the accessibility of the get and set accessors are
indicated by the getAccess and setAccess variables.
C#
using System;
using System.Collections.Generic;
using System.Reflection;
public static class ReflectionExtensions
{
    public static void Deconstruct (this PropertyInfo p, out bool isStatic,
                                   out bool isReadOnly, out bool isIndexed,
                                   out Type propertyType )
    {
        var getter = p.GetMethod;
        // Is the property read-only?
        isReadOnly = ! p.CanWrite;
        // Is the property instance or static?
        isStatic = getter.IsStatic;
        // Is the property indexed?
        isIndexed = p.GetIndexParameters().Length > 0;
        // Get the property type.
        propertyType = p.PropertyType;
    }
    public static void Deconstruct (this PropertyInfo p, out bool 
hasGetAndSet,
                                   out bool sameAccess, out string access,
                                   out string getAccess, out string 
setAccess )
    {
        hasGetAndSet = sameAccess = false;
        string getAccessTemp = null;
        string setAccessTemp = null;
        MethodInfo getter = null;
        if (p.CanRead)
            getter = p.GetMethod;
        MethodInfo setter = null;
        if (p.CanWrite)
            setter = p.SetMethod;
        if (setter != null && getter != null)
            hasGetAndSet = true;
        if (getter != null)
        {
            if (getter.IsPublic)                getAccessTemp = "public" ;
            else if (getter.IsPrivate)
                getAccessTemp = "private" ;
            else if (getter.IsAssembly)
                getAccessTemp = "internal" ;
            else if (getter.IsFamily)
                getAccessTemp = "protected" ;
            else if (getter.IsFamilyOrAssembly)
                getAccessTemp = "protected internal" ;
        }
        if (setter != null)
        {
            if (setter.IsPublic)
                setAccessTemp = "public" ;
            else if (setter.IsPrivate)
                setAccessTemp = "private" ;
            else if (setter.IsAssembly)
                setAccessTemp = "internal" ;
            else if (setter.IsFamily)
                setAccessTemp = "protected" ;
            else if (setter.IsFamilyOrAssembly)
                setAccessTemp = "protected internal" ;
        }
        // Are the accessibility of the getter and setter the same?
        if (setAccessTemp == getAccessTemp)
        {
            sameAccess = true;
            access = getAccessTemp;
            getAccess = setAccess = String.Empty;
        }
        else
        {
            access = null;
            getAccess = getAccessTemp;
            setAccess = setAccessTemp;
        }
    }
}
public class ExampleExtension
{
    public static void Main()
    {
        Type dateType = typeof(DateTime);
        PropertyInfo prop = dateType.GetProperty( "Now");
        var (isStatic, isRO, isIndexed, propType) = prop;
        Console.WriteLine( $"\nThe {dateType.FullName} .{prop.Name}  
property:" );
        Console.WriteLine( $"   PropertyType: {propType.Name} ");
        Console.WriteLine( $"   Static:       {isStatic} ");
        Console.WriteLine( $"   Read-only:    {isRO}");
        Console.WriteLine( $"   Indexed:      {isIndexed} ");Some system types provide the Deconstruct method as a convenience. For example, the
System.Collections.Generic.K eyValueP air<TK ey,TValue>  type provides this functionality.
When you're iterating over a System.Collections.Generic.Dictionary<TK ey,TValue>  each
element is a KeyValuePair<TKey, TValue> and can be deconstructed. Consider the
following example:
C#        Type listType = typeof(List<>);
        prop = listType.GetProperty( "Item",
                                    BindingFlags.Public |  
BindingFlags.NonPublic | BindingFlags.Instance | BindingFlags.Static);
        var (hasGetAndSet, sameAccess, accessibility, getAccessibility,  
setAccessibility) = prop;
        Console.Write( $"\nAccessibility of the {listType.FullName} .
{prop.Name}  property: " );
        if (!hasGetAndSet | sameAccess)
        {
            Console.WriteLine(accessibility);
        }
        else
        {
            Console.WriteLine( $"\n   The get accessor: {getAccessibility} ");
            Console.WriteLine( $"   The set accessor: {setAccessibility} ");
        }
    }
}
// The example displays the following output:
//       The System.DateTime.Now property:
//          PropertyType: DateTime
//          Static:       True
//          Read-only:    True
//          Indexed:      False
//
//       Accessibility of the System.Collections.Generic.List`1.Item  
property: public
Extension method for system types
Dictionary< string, int> snapshotCommitMap = 
new(StringComparer.OrdinalIgnoreCase)
{
    ["https://github.com/dotnet/docs" ] = 16_465,
    ["https://github.com/dotnet/runtime" ] = 114_223,
    ["https://github.com/dotnet/installer" ] = 22_436,
    ["https://github.com/dotnet/roslyn" ] = 79_484,
    ["https://github.com/dotnet/aspnetcore" ] = 48_386
};You can add a Deconstruct method to system types that don't have one. Consider the
following extension method:
C#
This extension method allows all Nullable<T>  types to be deconstructed into a tuple of
(bool hasValue, T value). The following example shows code that uses this extension
method:
C#foreach (var (repo, commitCount) in snapshotCommitMap)
{
    Console.WriteLine(
        $"The {repo} repository had {commitCount:N0}  commits as of November  
10th, 2021." );
}
public static class NullableExtensions
{
    public static void Deconstruct<T>(
        this T? nullable,
        out bool hasValue,
        out T value) where T : struct
    {
        hasValue = nullable.HasValue;
        value = nullable.GetValueOrDefault();
    }
}
DateTime? questionableDateTime = default;
var (hasValue, value) = questionableDateTime;
Console.WriteLine(
    $"{{ HasValue = {hasValue} , Value = {value} }}");
questionableDateTime = DateTime.Now;
(hasValue, value) = questionableDateTime;
Console.WriteLine(
    $"{{ HasValue = {hasValue} , Value = {value} }}");
// Example outputs:
// { HasValue = False, Value = 1/1/0001 12:00:00 AM }
// { HasValue = True, Value = 11/10/2021 6:11:45 PM }
record typesWhen you declare a record  type by using two or more positional parameters, the
compiler creates a Deconstruct method with an out parameter for each positional
parameter in the record declaration. For more information, see Positional syntax for
property definition  and Deconstructor behavior in derived records .
Deconstruct variable declaration (style rule IDE0042)
Discards
Tuple typesSee also
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
 Provide product feedbackExceptions and Exception Handling
Article •04/22/2023
The C# language's exception handling features help you deal with any unexpected or
exceptional situations that occur when a program is running. Exception handling uses
the try, catch, and finally keywords to try actions that may not succeed, to handle
failures when you decide that it's reasonable to do so, and to clean up resources
afterward. Exceptions can be generated by the common language runtime (CLR), by
.NET or third-party libraries, or by application code. Exceptions are created by using the
throw keyword.
In many cases, an exception may be thrown not by a method that your code has called
directly, but by another method further down in the call stack. When an exception is
thrown, the CLR will unwind the stack, looking for a method with a catch block for the
specific exception type, and it will execute the first such catch block that it finds. If it
finds no appropriate catch block anywhere in the call stack, it will terminate the process
and display a message to the user.
In this example, a method tests for division by zero and catches the error. Without the
exception handling, this program would terminate with a DivideByZer oException was
unhandled  error.
C#
public class ExceptionTest  
{ 
    static double SafeDivision (double x, double y) 
    { 
        if (y == 0) 
            throw new DivideByZeroException();  
        return x / y; 
    } 
    public static void Main() 
    { 
        // Input for test purposes. Change the values to see  
        // exception handling behavior.  
        double a = 98, b = 0; 
        double result;  
        try 
        {  
            result = SafeDivision(a, b);  
            Console.WriteLine( "{0} divided by {1} = {2}" , a, b, result);  
        }  
        catch (DivideByZeroException)  Exceptions have the following properties:
Exceptions are types that all ultimately derive from System.Exception.
Use a try block around the statements that might throw exceptions.
Once an exception occurs in the try block, the flow of control jumps to the first
associated exception handler that is present anywhere in the call stack. In C#, the
catch keyword is used to define an exception handler.
If no exception handler for a given exception is present, the program stops
executing with an error message.
Don't catch an exception unless you can handle it and leave the application in a
known state. If you catch System.Exception, rethrow it using the throw keyword at
the end of the catch block.
If a catch block defines an exception variable, you can use it to obtain more
information about the type of exception that occurred.
Exceptions can be explicitly generated by a program by using the throw keyword.
Exception objects contain detailed information about the error, such as the state of
the call stack and a text description of the error.
Code in a finally block is executed regardless of if an exception is thrown. Use a
finally block to release resources, for example to close any streams or files that
were opened in the try block.
Managed exceptions in .NET are implemented on top of the Win32 structured
exception handling mechanism. For more information, see Structured Exception
Handling (C/C++)  and A Crash Course on the Depths of Win32 S tructured
Exception Handling .
For more information, see Exceptions  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.        {  
            Console.WriteLine( "Attempted divide by zero." ); 
        }  
    } 
} 
Exceptions Overview
C# Language Specification
See alsoSystem.Exception
Exception-handling statements
ExceptionsUse exceptions
Article •09/15/2021
In C#, errors in the program at run time are propagated through the program by using a
mechanism called exceptions. Exceptions are thrown by code that encounters an error
and caught by code that can correct the error. Exceptions can be thrown by the .NET
runtime or by code in a program. Once an exception is thrown, it propagates up the call
stack until a catch statement for the exception is found. Uncaught exceptions are
handled by a generic exception handler provided by the system that displays a dialog
box.
Exceptions are represented by classes derived from Exception . This class identifies the
type of exception and contains properties that have details about the exception.
Throwing an exception involves creating an instance of an exception-derived class,
optionally configuring properties of the exception, and then throwing the object by
using the throw keyword. For example:
C#
After an exception is thrown, the runtime checks the current statement to see whether it
is within a try block. If it is, any catch blocks associated with the try block are checked
to see whether they can catch the exception. Catch blocks typically specify exception
types; if the type of the catch block is the same type as the exception, or a base class of
the exception, the catch block can handle the method. For example:
C#class CustomException  : Exception
{
    public CustomException (string message )
    {
    }
}
private static void TestThrow ()
{
    throw new CustomException( "Custom exception in TestThrow()" );
}
try
{
    TestThrow();
}
catch (CustomException ex)
{If the statement that throws an exception isn't within a try block or if the try block
that encloses it has no matching catch block, the runtime checks the calling method for
a try statement and catch blocks. The runtime continues up the calling stack,
searching for a compatible catch block. After the catch block is found and executed,
control is passed to the next statement after that catch block.
A try statement can contain more than one catch block. The first catch statement that
can handle the exception is executed; any following catch statements, even if they're
compatible, are ignored. Order catch blocks from most specific (or most-derived) to
least specific. For example:
C#    System.Console.WriteLine(ex.ToString());
}
using System;
using System.IO;
namespace  Exceptions
{
    public class CatchOrder
    {
        public static void Main()
        {
            try
            {
                using (var sw = new StreamWriter( "./test.txt" ))
                {
                    sw.WriteLine( "Hello");
                }
            }
            // Put the more specific exceptions first.
            catch (DirectoryNotFoundException ex)
            {
                Console.WriteLine(ex);
            }
            catch (FileNotFoundException ex)
            {
                Console.WriteLine(ex);
            }
            // Put the least specific exception last.
            catch (IOException ex)
            {
                Console.WriteLine(ex);
            }
            Console.WriteLine( "Done");
        }Before the catch block is executed, the runtime checks for finally blocks. Finally
blocks enable the programmer to clean up any ambiguous state that could be left over
from an aborted try block, or to release any external resources (such as graphics
handles, database connections, or file streams) without waiting for the garbage collector
in the runtime to finalize the objects. For example:
C#
If WriteByte() threw an exception, the code in the second try block that tries to
reopen the file would fail if file.Close() isn't called, and the file would remain locked.
Because finally blocks are executed even if an exception is thrown, the finally block
in the previous example allows for the file to be closed correctly and helps avoid an
error.
If no compatible catch block is found on the call stack after an exception is thrown, one
of three things occurs:    }
}
static void TestFinally ()
{
    FileStream? file = null;
    //Change the path to something that works on your machine.
    FileInfo fileInfo = new System.IO.FileInfo( "./file.txt" );
    try
    {
        file = fileInfo.OpenWrite();
        file.WriteByte( 0xF);
    }
    finally
    {
        // Closing the file allows you to reopen it immediately - otherwise  
IOException is thrown.
        file?.Close();
    }
    try
    {
        file = fileInfo.OpenWrite();
        Console.WriteLine( "OpenWrite() succeeded" );
    }
    catch (IOException)
    {
        Console.WriteLine( "OpenWrite() failed" );
    }
}If the exception is within a finalizer , the finalizer is aborted and the base finalizer, if
any, is called.
If the call stack contains a static constructor, or a static field initializer, a
TypeInitializationException  is thrown, with the original exception assigned to the
InnerException  property of the new exception.
If the start of the thread is reached, the thread is terminated.Exception Handling (C# Programming
Guide)
Article •03/14/2023
A try block is used by C# programmers to partition code that might be affected by an
exception. Associated catch  blocks are used to handle any resulting exceptions. A finally
block contains code that is run whether or not an exception is thrown in the try block,
such as releasing resources that are allocated in the try block. A try block requires one
or more associated catch blocks, or a finally block, or both.
The following examples show a try-catch statement, a try-finally statement, and a
try-catch-finally statement.
C#
C#
C#try 
{ 
    // Code to try goes here.  
} 
catch (SomeSpecificException ex)  
{ 
    // Code to handle the exception goes here.  
    // Only catch exceptions that you know how to handle.  
    // Never catch base class System.Exception without  
    // rethrowing it at the end of the catch block.  
} 
try 
{ 
    // Code to try goes here.  
} 
finally 
{ 
    // Code to execute after the try block goes here.  
} 
try 
{ 
    // Code to try goes here.  
} 
catch (SomeSpecificException ex)  A try block without a catch or finally block causes a compiler error.
A catch block can specify the type of exception to catch. The type specification is called
an exception f ilter. The exception type should be derived from Exception . In general,
don't specify Exception  as the exception filter unless either you know how to handle all
exceptions that might be thrown in the try block, or you've included a throw  statement
at the end of your catch block.
Multiple catch blocks with different exception classes can be chained together. The
catch blocks are evaluated from top to bottom in your code, but only one catch block
is executed for each exception that is thrown. The first catch block that specifies the
exact type or a base class of the thrown exception is executed. If no catch block
specifies a matching exception class, a catch block that doesn't have any type is
selected, if one is present in the statement. It's important to position catch blocks with
the most specific (that is, the most derived) exception classes first.
Catch exceptions when the following conditions are true:
You have a good understanding of why the exception might be thrown, and you
can implement a specific recovery, such as prompting the user to enter a new file
name when you catch a FileNotFoundException  object.
You can create and throw a new, more specific exception.
C#{ 
    // Code to handle the exception goes here.  
} 
finally 
{ 
    // Code to execute after the try (and possibly catch) blocks  
    // goes here.  
} 
Catch Blocks
int GetInt(int[] array, int index) 
{ 
    try 
    { 
        return array[index];  
    } 
    catch (IndexOutOfRangeException e)  
    { 
        throw new ArgumentOutOfRangeException(  You want to partially handle an exception before passing it on for more handling.
In the following example, a catch block is used to add an entry to an error log
before rethrowing the exception.
C#
You can also specify exception f ilters to add a boolean expression to a catch clause.
Exception filters indicate that a specific catch clause matches only when that condition is
true. In the following example, both catch clauses use the same exception class, but an
extra condition is checked to create a different error message:
C#
An exception filter that always returns false can be used to examine all exceptions but
not process them. A typical use is to log exceptions:            "Parameter index is out of range." , e); 
    } 
} 
try 
{ 
    // Try to access a resource.  
} 
catch (UnauthorizedAccessException e)  
{ 
    // Call a custom error logging procedure.  
    LogError(e);  
    // Re-throw the error.  
    throw; 
} 
int GetInt(int[] array, int index) 
{ 
    try 
    { 
        return array[index];  
    } 
    catch (IndexOutOfRangeException e) when (index < 0)  
    { 
        throw new ArgumentOutOfRangeException(  
            "Parameter index cannot be negative." , e); 
    } 
    catch (IndexOutOfRangeException e)  
    { 
        throw new ArgumentOutOfRangeException(  
            "Parameter index cannot be greater than the array size." , e); 
    } 
} C#
The LogException method always returns false, no catch clause using this exception
filter matches. The catch clause can be general, using System.Exception , and later
clauses can process more specific exception classes.
A finally block enables you to clean up actions that are performed in a try block. If
present, the finally block executes last, after the try block and any matched catch
block. A finally block always runs, whether an exception is thrown or a catch block
matching the exception type is found.
The finally block can be used to release resources such as file streams, database
connections, and graphics handles without waiting for the garbage collector in the
runtime to finalize the objects.
In the following example, the finally block is used to close a file that is opened in the
try block. Notice that the state of the file handle is checked before the file is closed. If
the try block can't open the file, the file handle still has the value null and the finally
block doesn't try to close it. Instead, if the file is opened successfully in the try block,
the finally block closes the open file.
C#public static void Main() 
{ 
    try 
    { 
        string? s = null; 
        Console.WriteLine(s.Length);  
    } 
    catch (Exception e) when (LogException(e))  
    { 
    } 
    Console.WriteLine( "Exception must have been handled" ); 
} 
private static bool LogException (Exception e ) 
{ 
    Console.WriteLine( $"\tIn the log routine. Caught {e.GetType()} "); 
    Console.WriteLine( $"\tMessage: {e.Message} "); 
    return false; 
} 
Finally BlocksFor more information, see Exceptions  and The try statement  in the C# Language
Specification . The language specification is the definitive source for C# syntax and
usage.
C# reference
Exception-handling statements
using statementFileStream? file = null; 
FileInfo fileinfo = new System.IO.FileInfo( "./file.txt" ); 
try 
{ 
    file = fileinfo.OpenWrite();  
    file.WriteByte( 0xF); 
} 
finally 
{ 
    // Check for null because OpenWrite might have failed.  
    file?.Close();  
} 
C# Language Specification
See alsoCreate and throw exceptions
Article •11/03/2023
Exceptions are used to indicate that an error has occurred while running the program.
Exception objects that describe an error are created and then thrown with the throw
statement or expression . The runtime then searches for the most compatible exception
handler.
Programmers should throw exceptions when one or more of the following conditions
are true:
The method can't complete its defined functionality. For example, if a parameter to
a method has an invalid value:
C#
An inappropriate call to an object is made, based on the object state. One example
might be trying to write to a read-only file. In cases where an object state doesn't
allow an operation, throw an instance of InvalidOperationException  or an object
based on a derivation of this class. The following code is an example of a method
that throws an InvalidOperationException  object:
C#static void CopyObject (SampleClass original )
{
    _ = original ?? throw new ArgumentException( "Parameter cannot be  
null", nameof(original));
}
public class ProgramLog
{
    FileStream logFile = null!;
    public void OpenLog(FileInfo fileName, FileMode mode ) { }
    public void WriteLog ()
    {
        if (!logFile.CanWrite)
        {
            throw new InvalidOperationException( "Logfile cannot be  
read-only" );
        }
        // Else write data to the log and return.
    }
}When an argument to a method causes an exception. In this case, the original
exception should be caught and an ArgumentException  instance should be
created. The original exception should be passed to the constructor of the
ArgumentException  as the InnerException  parameter:
C#
Exceptions contain a property named StackT race. This string contains the name of the
methods on the current call stack, together with the file name and line number where
the exception was thrown for each method. A StackT race object is created automatically
by the common language runtime (CLR) from the point of the throw statement, so that
exceptions must be thrown from the point where the stack trace should begin.
All exceptions contain a property named Message . This string should be set to explain
the reason for the exception. Information that is sensitive to security shouldn't be put in
the message text. In addition to Message , ArgumentException  contains a property
named ParamName  that should be set to the name of the argument that caused the
exception to be thrown. In a property setter, ParamName  should be set to value.
Public and protected methods throw exceptions whenever they can't complete their
intended functions. The exception class thrown is the most specific exception available
that fits the error conditions. These exceptions should be documented as part of thestatic int GetValueFromArray (int[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (IndexOutOfRangeException e)
    {
        throw new ArgumentOutOfRangeException(
            "Parameter index is out of range." , e);
    }
}
７ Note
The preceding example shows how to use the InnerException property. It's
intentionally simplified. In practice, you should check that an index is in range
before using it. Y ou could use this technique of wrapping an exception when a
member of a parameter throws an exception you couldn't anticipate before
calling the member.class functionality, and derived classes or updates to the original class should retain the
same behavior for backward compatibility.
The following list identifies practices to avoid when throwing exceptions:
Don't use exceptions to change the flow of a program as part of ordinary
execution. Use exceptions to report and handle error conditions.
Exceptions shouldn't be returned as a return value or parameter instead of being
thrown.
Don't throw System.Exception , System.S ystemException ,
System.NullR eferenceException , or System.IndexOutOfRangeException
intentionally from your own source code.
Don't create exceptions that can be thrown in debug mode but not release mode.
To identify run-time errors during the development phase, use Debug Assert
instead.
Methods declared with the async modifier have some special considerations when it
comes to exceptions. Exceptions thrown in an async method are stored in the returned
task and don't emerge until, for example, the task is awaited. For more information
about stored exceptions, see Asynchronous exceptions .
We recommend that you validate arguments and throw any corresponding exceptions,
such as ArgumentException  and ArgumentNullException , before entering the
asynchronous parts of your methods. That is, these validation exceptions should emerge
synchronously before the work starts. The following code snippet shows an example
where, if the exceptions are thrown, the ArgumentException  exceptions would emerge
synchronously, whereas the InvalidOperationException  would be stored in the returned
task.
C#Things to avoid when throwing exceptions
Exceptions in task-returning methods
// Non-async, task-returning method.
// Within this method (but outside of the local function),
// any thrown exceptions emerge synchronously.
public static Task<Toast> ToastBreadAsync (int slices, int toastTime )
{
    if (slices is < 1 or > 4)
    {
        throw new ArgumentException(Programs can throw a predefined exception class in the System  namespace (except
where previously noted), or create their own exception classes by deriving from
Exception . The derived classes should define at least three constructors: one
parameterless constructor, one that sets the message property, and one that sets both
the Message  and InnerException  properties. For example:
C#            "You must specify between 1 and 4 slices of bread." ,
            nameof(slices));
    }
    if (toastTime < 1)
    {
        throw new ArgumentException(
            "Toast time is too short." , nameof(toastTime));
    }
    return ToastBreadAsyncCore(slices, toastTime);
    // Local async function.
    // Within this function, any thrown exceptions are stored in the task.
    static async Task<Toast> ToastBreadAsyncCore (int slices, int time)
    {
        for (int slice = 0; slice < slices; slice++)
        {
            Console.WriteLine( "Putting a slice of bread in the toaster" );
        }
        // Start toasting.
        await Task.Delay(time);
        if (time > 2_000)
        {
            throw new InvalidOperationException( "The toaster is on fire!" );
        }
        Console.WriteLine( "Toast is ready!" );
        return new Toast();
    }
}
Define exception classes
[Serializable ]
public class InvalidDepartmentException  : Exception
{
    public InvalidDepartmentException () : base() { }
    public InvalidDepartmentException (string message ) : base(message) { }
    public InvalidDepartmentException (string message, Exception inner ) : Add new properties to the exception class when the data they provide is useful to
resolving the exception. If new properties are added to the derived exception class,
ToString() should be overridden to return the added information.
For more information, see Exceptions  and The throw statement  in the C# Language
Specification . The language specification is the definitive source for C# syntax and
usage.
Exception Hierarchybase(message, inner ) { }
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
 Provide product feedbackCompiler-generated exceptions
Article •04/22/2023
Some exceptions are thrown automatically by the .NET runtime when basic operations
fail. These exceptions and their error conditions are listed in the following table.
Exception Descr iption
ArithmeticException A base class for exceptions that occur during arithmetic
operations, such as DivideByZeroException  and
OverflowException .
ArrayT ypeMismatchException Thrown when an array can't store a given element because the
actual type of the element is incompatible with the actual type of
the array.
DivideByZeroException Thrown when an attempt is made to divide an integral value by
zero.
IndexOutOfRangeException Thrown when an attempt is made to index an array when the
index is less than zero or outside the bounds of the array.
InvalidCastException Thrown when an explicit conversion from a base type to an
interface or to a derived type fails at run time.
NullR eferenceException Thrown when an attempt is made to reference an object whose
value is null.
OutOfMemoryException Thrown when an attempt to allocate memory using the new
operator fails. This exception indicates that the memory available
to the common language runtime has been exhausted.
OverflowException Thrown when an arithmetic operation in a checked context
overflows.
StackOverflowException Thrown when the execution stack is exhausted by having too
many pending method calls; usually indicates a very deep or
infinite recursion.
TypeInitializationException Thrown when a static constructor throws an exception and no
compatible catch clause exists to catch it.
Exception-handling statementsSee alsoC# identifier naming rules and
conventions
Article •11/29/2023
An identifier  is the name you assign to a type (class, interface, struct, delegate, or
enum), member, variable, or namespace.
Valid identifiers must follow these rules. The C# compiler produces an error for any
identifier that doesn't follow these rules:
Identifiers must start with a letter or underscore ( _).
Identifiers can contain Unicode letter characters, decimal digit characters, Unicode
connecting characters, Unicode combining characters, or Unicode formatting
characters. For more information on Unicode categories, see the Unicode Category
Database .
You can declare identifiers that match C# keywords by using the @ prefix on the
identifier. The @ isn't part of the identifier name. For example, @if declares an identifier
named if. These verbatim identifiers  are primarily for interoperability with identifiers
declared in other languages.
For a complete definition of valid identifiers, see the Identifiers article in the C#
Language Specification .
In addition to the rules, conventions for identifier names are used throughout the .NET
APIs. These conventions provide consistency for names, but the compiler doesn't
enforce them. Y ou're free to use different conventions in your projects.
By convention, C# programs use PascalCase for type names, namespaces, and all public
members. In addition, the dotnet/docs team uses the following conventions, adopted
from the .NET Runtime team's coding style :
Interface names start with a capital I.
Attribute types end with the word Attribute.Naming rules
Naming conventions
Enum types use a singular noun for nonflags, and a plural noun for flags.
Identifiers shouldn't contain two consecutive underscore ( _) characters. Those
names are reserved for compiler-generated identifiers.
Use meaningful and descriptive names for variables, methods, and classes.
Prefer clarity over brevity.
Use P ascalCase for class names and method names.
Use camelCase for method arguments, local variables, and private fields.
Use P ascalCase for constant names, both fields and local constants.
Private instance fields start with an underscore ( _).
Static fields start with s_. This convention isn't the default Visual S tudio behavior,
nor part of the Framework design guidelines , but is configurable in editorconfig .
Avoid using abbreviations or acronyms in names, except for widely known and
accepted abbreviations.
Use meaningful and descriptive namespaces that follow the reverse domain name
notation.
Choose assembly names that represent the primary purpose of the assembly.
Avoid using single-letter names, except for simple loop counters. Also, syntax
examples that describe the syntax of C# constructs often use the following single-
letter names that match the convention used in the C# language specification .
Syntax examples are an exception to the rule.
Use S for structs, C for classes.
Use M for methods.
Use v for variables, p for parameters.
Use r for ref parameters.
In the following examples, guidance pertaining to elements marked public is also
applicable when working with protected and protected internal elements, all of which Tip
You can enforce naming conventions that concern capitalization, prefixes, suffixes,
and word separators by using code-style naming rules .are intended to be visible to external callers.
Use pascal casing ("P ascalCasing") when naming a class, Interface, struct, or
delegate type.
C#
C#
C#
C#
When naming an interface, use pascal casing in addition to prefixing the name with an
I. This prefix clearly indicates to consumers that it's an interface.
C#
When naming public members of types, such as fields, properties, events, use pascal
casing. Also, use pascal casing for all methods and local functions.
C#Pascal case
public class DataService
{
}
public record PhysicalAddress (
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode );
public struct ValueCoordinate
{
}
public delegate  void DelegateType (string message );
public interface  IWorkerQueue
{
}When writing positional records, use pascal casing for parameters as they're the public
properties of the record.
C#
For more information on positional records, see Positional syntax for property definition .
Use camel casing ("camelCasing") when naming private or internal fields and prefix
them with _. Use camel casing when naming local variables, including instances of a
delegate type.
C#public class ExampleEvents
{
    // A public field, these should be used sparingly
    public bool IsValid;
    // An init-only property
    public IWorkerQueue WorkerQueue { get; init; }
    // An event
    public event Action EventProcessing;
    // Method
    public void StartEventProcessing ()
    {
        // Local function
        static int CountQueueItems () => WorkerQueue.Count;
        // ...
    }
}
public record PhysicalAddress (
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode );
Camel case
public class DataService
{
    private IWorkerQueue _workerQueue;
}When working with static fields that are private or internal, use the s_ prefix and
for thread static use t_.
C#
When writing method parameters, use camel casing.
C#
For more information on C# naming conventions, see the .NET Runtime team's coding
style .
The following guidelines apply to type parameters on generic type parameters. T ype
parameters are the placeholders for arguments in a generic type or a generic method.
You can read more about generic type parameters  in the C# programming guide.
Do name generic type parameters with descriptive names, unless a single letter
name is completely self explanatory and a descriptive name wouldn't add value.
./snippets/coding-conventions Tip
When editing C# code that follows these naming conventions in an IDE that
supports statement completion, typing _ will show all of the object-scoped
members.
public class DataService
{
    private static IWorkerQueue s_workerQueue;
    [ThreadStatic ]
    private static TimeSpan t_timeSpan;
}
public T SomeMethod<T>( int someNumber, bool isValid)
{
}
Type parameter naming guidelines
public interface ISessionChannel<TSession> { /*...*/ }
public delegate TOutput Converter<TInput, TOutput>(TInput from);Consider  using T as the type parameter name for types with one single letter type
parameter.
./snippets/coding-conventions
Do prefix descriptive type parameter names with "T".
./snippets/coding-conventions
Consider  indicating constraints placed on a type parameter in the name of
parameter. For example, a parameter constrained to ISession might be called
TSession.
The code analysis rule CA1715  can be used to ensure that type parameters are named
appropriately.
Examples that don't include using directives , use namespace qualifications. If you
know that a namespace is imported by default in a project, you don't have to fully
qualify the names from that namespace. Qualified names can be broken after a dot
(.) if they're too long for a single line, as shown in the following example.
C#
You don't have to change the names of objects that were created by using the
Visual S tudio designer tools to make them fit other guidelines.public class List<T> { /*...*/ }
public int IComparer<T>() { return 0; }
public delegate bool Predicate<T>(T item);
public struct Nullable<T> where T : struct { /*...*/ }
public interface ISessionChannel<TSession>
{
    TSession Session { get; }
}
Extra naming conventions
var currentPerformanceCounterCategory = new System.Diagnostics.
    PerformanceCounterCategory();６ Collaborat e with us on
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
 Provide product feedbackCommo n C# code conventions
Article •08/01/2023
A code standard is essential for maintaining code readability, consistency, and
collaboration within a development team. Code that follows industry practices and
established guidelines is easier to understand, maintain, and extend. Most projects
enforce a consistent style through code conventions. The dotnet/docs  and
dotnet/samples  projects are no exception. In this series of articles, you learn our
coding conventions and the tools we use to enforce them. Y ou can take our conventions
as-is, or modify them to suit your team's needs.
We chose our conventions based on the following goals:
1. Correctness : Our samples are copied and pasted into your applications. W e expect
that, so we need to make code that's resilient and correct, even after multiple edits.
2. Teaching : The purpose of our samples is to teach all of .NET and C#. For that
reason, we don't place restrictions on any language feature or API. Instead, those
samples teach when a feature is a good choice.
3. Consist ency: Readers expect a consistent experience across our content. All
samples should conform to the same style.
4. Adoption : We aggressively update our samples to use new language features. That
practice raises awareness of new features, and makes them more familiar to all C#
developers.
） Impor tant
These guidelines are used by Microsoft to develop samples and documentation.
They were adopted from the .NET Runtime, C# Coding S tyle  and C# compiler
(roslyn)  guidelines. W e chose those guidelines because they have been tested
over several years of Open Source development. They've helped community
members participate in the runtime and compiler projects. They are meant to be an
example of common C# conventions, and not an authoritative list (see Framew ork
Design Guidelines  for that).
The teaching  and adoption  goals are why the docs coding convention differs from
the runtime and compiler conventions. Both the runtime and compiler have strict
performance metrics for hot paths. Many other applications don't. Our teaching
goal mandates that we don't prohibit any construct. Instead, samples show when
constructs should be used. W e update samples more aggressively than most
This article explains our guidelines. The guidelines have evolved over time, and you'll
find samples that don't follow our guidelines. W e welcome PRs that bring those samples
into compliance, or issues that draw our attention to samples we should update. Our
guidelines are Open Source and we welcome PRs and issues. However, if your
submission would change these recommendations, open an issue for discussion first.
You're welcome to use our guidelines, or adapt them to your needs.
Tools can help your team enforce your standards. Y ou can enable code analysis  to
enforce the rules you prefer. Y ou can also create an editorconfig  so that Visual S tudio
automatically enforces your style guidelines. As a starting point, you can copy the
dotnet/docs repo's file  to use our style.
These tools make it easier for your team to adopt your preferred guidelines. Visual
Studio applies the rules in all .editorconfig files in scope to format your code. Y ou can
use multiple configurations to enforce corporate-wide standards, team standards, and
even granular project standards.
Code analysis produces warnings and diagnostics when the enabled rules are violated.
You configure the rules you want applied to your project. Then, each CI build notifies
developers when they violate any of the rules.
Choose appropriate diagnostic IDs  when building your own analyzers
The following sections describe practices that the .NET docs team follows to prepare
code examples and samples. In general, follow these practices:
Utilize modern language features and C# versions whenever possible.
Avoid obsolete or outdated language constructs.
Only catch exceptions that can be properly handled; avoid catching generic
exceptions.
Use specific exception types to provide meaningful error messages.production applications do. Our adoption  goal mandates that we show code you
should write today, even when code written last year doesn't need changes.
Tools and analyzers
Diagnostic IDs
Language guidelinesUse LINQ queries and methods for collection manipulation to improve code
readability.
Use asynchronous programming with async and await for I/O-bound operations.
Be cautious of deadlocks and use Task.ConfigureA wait when appropriate.
Use the language keywords for data types instead of the runtime types. For
example, use string instead of System.S tring , or int instead of System.Int32 .
Use int rather than unsigned types. The use of int is common throughout C#,
and it's easier to interact with other libraries when you use int. Exceptions are for
documentation specific to unsigned data types.
Use var only when a reader can infer the type from the expression. R eaders view
our samples on the docs platform. They don't have hover or tool tips that display
the type of variables.
Write code with clarity and simplicity in mind.
Avoid overly complex and convoluted code logic.
More specific guidelines follow.
Use string interpolation  to concatenate short strings, as shown in the following
code.
C#
To append strings in loops, especially when you're working with large amounts of
text, use a System.T ext.StringBuilder  object.
C#String data
string displayName = $"{nameList[n].LastName} , 
{nameList[n].FirstName} ";
var phrase = 
"lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala" ;
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);
ArraysUse the concise syntax when you initialize arrays on the declaration line. In the
following example, you can't use var instead of string[].
C#
If you use explicit instantiation, you can use var.
C#
Use Func<>  and Action<>  instead of defining delegate types. In a class, define the
delegate method.
C#
Call the method using the signature defined by the Func<> or Action<> delegate.
C#
If you create instances of a delegate type, use the concise syntax. In a class, define
the delegate type and a method that has a matching signature.
C#string[] vowels1 = { "a", "e", "i", "o", "u" };
var vowels2 = new string[] { "a", "e", "i", "o", "u" };
Delegates
Action<string> actionExample1 = x => Console.WriteLine( $"x is: {x}");
Action<string, string> actionExample2 = (x, y) =>
    Console.WriteLine( $"x is: {x}, y is {y}");
Func<string, int> funcExample1 = x => Convert.ToInt32(x);
Func<int, int, int> funcExample2 = (x, y) => x + y;
actionExample1( "string for x" );
actionExample2( "string for x" , "string for y" );
Console.WriteLine( $"The value is {funcExample1( "1")}");
Console.WriteLine( $"The sum is {funcExample2( 1, 2)}");Create an instance of the delegate type and call it. The following declaration shows
the condensed syntax.
C#
The following declaration uses the full syntax.
C#
Use a try-catch  statement for most exception handling.
C#
Simplify your code by using the C# using statement . If you have a try-finally
statement in which the only code in the finally block is a call to the Disposepublic delegate  void Del(string message );
public static void DelMethod (string str)
{
    Console.WriteLine( "DelMethod argument: {0}" , str);
}
Del exampleDel2 = DelMethod;
exampleDel2( "Hey");
Del exampleDel1 = new Del(DelMethod);
exampleDel1( "Hey");
try-catch and using statements in exception handling
static double ComputeDistance (double x1, double y1, double x2, double 
y2)
{
    try
    {
        return Math.Sqrt((x1 - x2) * (x1 - x2) + (y1 - y2) * (y1 -  
y2));
    }
    catch (System.ArithmeticException ex)
    {
        Console.WriteLine( $"Arithmetic overflow or underflow: {ex}");
        throw;
    }
}method, use a using statement instead.
In the following example, the try-finally statement only calls Dispose in the
finally block.
C#
You can do the same thing with a using statement.
C#
Use the new using  syntax  that doesn't require braces:
C#
Use && instead of & and || instead of | when you perform comparisons, as shown
in the following example.
C#Font bodyStyle = new Font("Arial", 10.0f);
try
{
    byte charset = bodyStyle.GdiCharSet;
}
finally
{
    if (bodyStyle != null)
    {
        ((IDisposable)bodyStyle).Dispose();
    }
}
using (Font arial = new Font("Arial", 10.0f))
{
    byte charset2 = arial.GdiCharSet;
}
using Font normalStyle = new Font("Arial", 10.0f);
byte charset3 = normalStyle.GdiCharSet;
&& and || operators
Console.Write( "Enter a dividend: " );
int dividend = Convert.ToInt32(Console.ReadLine());
Console.Write( "Enter a divisor: " );If the divisor is 0, the second clause in the if statement would cause a run-time error.
But the && operator short-circuits when the first expression is false. That is, it doesn't
evaluate the second expression. The & operator would evaluate both, resulting in a run-
time error when divisor is 0.
Use one of the concise forms of object instantiation, as shown in the following
declarations.
C#
C#
The preceding declarations are equivalent to the following declaration.
C#
Use object initializers to simplify object creation, as shown in the following
example.
C#int divisor = Convert.ToInt32(Console.ReadLine());
if ((divisor != 0) && (dividend / divisor) is var result)
{
    Console.WriteLine( "Quotient: {0}" , result);
}
else
{
    Console.WriteLine( "Attempted division by 0 ends up here." );
}
new operator
var firstExample = new ExampleClass();
ExampleClass instance2 = new();
ExampleClass secondExample = new ExampleClass();
var thirdExample = new ExampleClass { Name = "Desktop" , ID = 37414,
    Location = "Redmond" , Age = 2.3 };The following example sets the same properties as the preceding example but
doesn't use initializers.
C#
Use a lambda expression to define an event handler that you don't need to
remove later:
C#
The lambda expression shortens the following traditional definition.
C#
Call static  members by using the class name: ClassName.S taticMember . This practice
makes code more readable by making static access clear. Don't qualify a static member
defined in a base class with the name of a derived class. While that code compiles, thevar fourthExample = new ExampleClass();
fourthExample.Name = "Desktop" ;
fourthExample.ID = 37414;
fourthExample.Location = "Redmond" ;
fourthExample.Age = 2.3;
Event handling
public Form2()
{
    this.Click += (s, e) =>
        {
            MessageBox.Show(
                ((MouseEventArgs)e).Location.ToString());
        };
}
public Form1()
{
    this.Click += new EventHandler(Form1_Click);
}
void Form1_Click (object? sender, EventArgs e )
{
    MessageBox.Show(((MouseEventArgs)e).Location.ToString());
}
Static memberscode readability is misleading, and the code may break in the future if you add a static
member with the same name to the derived class.
Use meaningful names for query variables. The following example uses
seattleCustomers for customers who are located in Seattle.
C#
Use aliases to make sure that property names of anonymous types are correctly
capitalized, using P ascal casing.
C#
Rename properties when the property names in the result would be ambiguous.
For example, if your query returns a customer name and a distributor ID, instead of
leaving them as Name and ID in the result, rename them to clarify that Name is the
name of a customer, and ID is the ID of a distributor.
C#
Use implicit typing in the declaration of query variables and range variables. This
guidance on implicit typing in LINQ queries overrides the general rules for
implicitly typed local variables . LINQ queries often use projections that create
anonymous types. Other query expressions create results with nested generic
types. Implicit typed variables are often more readable.LINQ queries
var seattleCustomers = from customer in customers
                       where customer.City == "Seattle"
                       select customer.Name;
var localDistributors =
    from customer in customers
    join distributor in distributors on customer.City equals 
distributor.City
    select new { Customer = customer, Distributor = distributor };
var localDistributors2 =
    from customer in customers
    join distributor in distributors on customer.City equals 
distributor.City
    select new { CustomerName = customer.Name, DistributorID =  
distributor.ID };C#
Align query clauses under the from  clause, as shown in the previous examples.
Use where  clauses before other query clauses to ensure that later query clauses
operate on the reduced, filtered set of data.
C#
Use multiple from clauses instead of a join clause to access inner collections. For
example, a collection of Student objects might each contain a collection of test
scores. When the following query is executed, it returns each score that is over 90,
along with the last name of the student who received the score.
C#
Use implicit typing  for local variables when the type of the variable is obvious from
the right side of the assignment.
C#
Don't use var when the type isn't apparent from the right side of the assignment.
Don't assume the type is clear from a method name. A variable type is considered
clear if it's a new operator, an explicit cast or assignment to a literal value.var seattleCustomers = from customer in customers
                       where customer.City == "Seattle"
                       select customer.Name;
var seattleCustomers2 = from customer in customers
                        where customer.City == "Seattle"
                        orderby customer.Name
                        select customer;
var scoreQuery = from student in students
                 from score in student.Scores!
                 where score > 90
                 select new { Last = student.LastName, score };
Implicitly typed local variables
var message = "This is clearly a string." ;
var currentTemperature = 27;C#
Don't use variable names to specify the type of the variable. It might not be
correct. Instead, use the type to specify the type, and use the variable name to
indicate the semantic information of the variable. The following example should
use string for the type and something like iterations to indicate the meaning of
the information read from the console.
C#
Avoid the use of var in place of dynamic . Use dynamic when you want run-time
type inference. For more information, see Using type dynamic (C# Programming
Guide) .
Use implicit typing for the loop variable in for loops.
The following example uses implicit typing in a for statement.
C#
Don't use implicit typing to determine the type of the loop variable in foreach
loops. In most cases, the type of elements in the collection isn't immediately
obvious. The collection's name shouldn't be solely relied upon for inferring the
type of its elements.
The following example uses explicit typing in a foreach statement.
C#int numberOfIterations = Convert.ToInt32(Console.ReadLine());
int currentMaximum = ExampleClass.ResultSoFar();
var inputInt = Console.ReadLine();
Console.WriteLine(inputInt);
var phrase = 
"lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala" ;
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);use implicit type for the result sequences in LINQ queries. The section on LINQ
explains that many LINQ queries result in anonymous types where implicit types
must be used. Other queries result in nested generic types where var is more
readable.
Some of our samples explain the natur al type  of an expression. Those samples must use
var so that the compiler picks the natural type. Even though those examples are less
obvious, the use of var is required for the sample. The text should explain the behavior.
When a using directive is outside a namespace declaration, that imported namespace is
its fully qualified name. The fully qualified name is clearer. When the using directive is
inside the namespace, it could be either relative to that namespace, or its fully qualified
name.
C#foreach (char ch in laugh)
{
    if (ch == 'h')
        Console.Write( "H");
    else
        Console.Write(ch);
}
Console.WriteLine();
７ Note
Be careful not to accidentally change a type of an element of the iterable
collection. For example, it is easy to switch from System.Linq.IQuer yable  to
System.Collections.IEnumerable  in a foreach statement, which changes the
execution of a query.
Place the using directives outside the namespace
declaration
using Azure;
namespace  CoolStuff.AwesomeFeature
{
    public class Awesome
    {
        public void Stuff()
        {Assuming there's a reference (direct, or indirect) to the WaitUntil  class.
Now, let's change it slightly:
C#
And it compiles today. And tomorrow. But then sometime next week the preceding
(untouched) code fails with two errors:
Console
One of the dependencies has introduced this class in a namespace then ends with
.Azure:
C#            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
namespace  CoolStuff.AwesomeFeature
{
    using Azure;
    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
- error CS0246: The type or namespace name 'WaitUntil' could not be found  
(are you missing a using directive or an assembly reference?)
- error CS0103: The name 'WaitUntil' does not exist in the current context
namespace  CoolStuff.Azure
{
    public class SecretsManagement
    {
        public string FetchFromKeyVault (string vaultId, string secretId ) { 
return null; }
    }
}A using directive placed inside a namespace is context-sensitive and complicates name
resolution. In this example, it's the first namespace that it finds.
CoolStuff.AwesomeFeature.Azure
CoolStuff.Azure
Azure
Adding a new namespace that matches either CoolStuff.Azure or
CoolStuff.AwesomeFeature.Azure would match before the global Azure namespace. Y ou
could resolve it by adding the global:: modifier to the using declaration. However, it's
easier to place using declarations outside the namespace instead.
C#
In general, use the following format for code samples:
Use four spaces for indentation. Don't use tabs.
Align code consistently to improve readability.
Limit lines to 65 characters to enhance code readability on docs, especially on
mobile screens.
Break long statements into multiple lines to improve clarity.
Use the "Allman" style for braces: open and closing brace its own new line. Braces
line up with current indentation level.
Line breaks should occur before binary operators, if necessary.
Use single-line comments ( //) for brief explanations.namespace  CoolStuff.AwesomeFeature
{
    using global::Azure;
    public class Awesome
    {
        public void Stuff()
        {
            WaitUntil wait = WaitUntil.Completed;
            // ...
        }
    }
}
Style guidelines
Comment styleAvoid multi-line comments ( /* */) for longer explanations. Comments aren't
localized. Instead, longer explanations are in the companion article.
For describing methods, classes, fields, and all public members use XML
comments .
Place the comment on a separate line, not at the end of a line of code.
Begin comment text with an uppercase letter.
End comment text with a period.
Insert one space between the comment delimiter ( //) and the comment text, as
shown in the following example.
C#
Good layout uses formatting to emphasize the structure of your code and to make the
code easier to read. Microsoft examples and samples conform to the following
conventions:
Use the default Code Editor settings (smart indenting, four-character indents, tabs
saved as spaces). For more information, see Options, T ext Editor, C#, Formatting .
Write only one statement per line.
Write only one declaration per line.
If continuation lines aren't indented automatically, indent them one tab stop (four
spaces).
Add at least one blank line between method definitions and property definitions.
Use parentheses to make clauses in an expression apparent, as shown in the
following code.
C#// The following declaration creates a query. It does not run
// the query.
Layout conventions
if ((startX > endX) && (startX > previousX))
{Exceptions are when the sample explains operator or expression precedence.
Follow the guidelines in Secure Coding Guidelines .    // Take appropriate action.
}
Security
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
 Provide product feedbackHow to display command-line
arguments
Article •03/11/2022
Arguments provided to an executable on the command line are accessible in top-level
statements  or through an optional parameter to Main. The arguments are provided in
the form of an array of strings. Each element of the array contains one argument. White-
space between arguments is removed. For example, consider these command-line
invocations of a fictitious executable:
Input on command line Array o f strings p assed t o Main
executable.ex e a b c "a" 
"b" 
"c"
executable.ex e one tw o "one"  
"two"
executable.ex e "one tw o" three "one two"  
"three"
This example displays the command-line arguments passed to a command-line
application. The output shown is for the first entry in the table above.
C#７ Note
When you are running an application in Visual S tudio, you can specify command-
line arguments in the Debug P age, Pr oject Designer .
Example
// The Length property provides the number of array elements.  
Console.WriteLine( $"parameter count = {args.Length} "); 
for (int i = 0; i < args.Length; i++)  System.CommandLine overview
Tutorial: Get started with S ystem.CommandLine{ 
    Console.WriteLine( $"Arg[{i}] = [{args[i]} ]"); 
} 
/* Output (assumes 3 cmd line args):  
    parameter count = 3  
    Arg[0] = [a]  
    Arg[1] = [b]  
    Arg[2] = [c]  
*/ 
See alsoExplore object oriented programming
with classes and objects
Article •04/22/2023
In this tutorial, you'll build a console application and see the basic object-oriented
features that are part of the C# language.
We recommend Visual S tudio  for Windows or Mac. Y ou can download a free
version from the Visual S tudio downloads page . Visual S tudio includes the .NET
SDK.
You can also use the Visual S tudio Code  editor. Y ou'll need to install the latest
.NET SDK  separately.
If you prefer a different editor, you need to install the latest .NET SDK .
Using a terminal window, create a directory named classes. You'll build your application
there. Change to that directory and type dotnet new console in the console window.
This command creates your application. Open Program.cs . It should look like this:
C#
In this tutorial, you're going to create new types that represent a bank account. T ypically
developers define each class in a different text file. That makes it easier to manage as a
program grows in size. Create a new file named BankAc count.cs  in the Class es directory.
This file will contain the definition of a bank ac count . Object Oriented programming
organizes code by creating types in the form of class es. These classes contain the code
that represents a specific entity. The BankAccount class represents a bank account. The
code implements specific operations through methods and properties. In this tutorial,
the bank account supports this behavior:
1. It has a 10-digit number that uniquely identifies the bank account.
2. It has a string that stores the name or names of the owners.Prerequisites
Create your application
// See https://aka.ms/new-console-template for more information
Console.WriteLine( "Hello, World!" );3. The balance can be retrieved.
4. It accepts deposits.
5. It accepts withdrawals.
6. The initial balance must be positive.
7. Withdrawals can't result in a negative balance.
You can start by creating the basics of a class that defines that behavior. Create a new
file using the File:New  command. Name it BankAc count.cs . Add the following code to
your BankAc count.cs  file:
C#
Before going on, let's take a look at what you've built. The namespace declaration
provides a way to logically organize your code. This tutorial is relatively small, so you'll
put all the code in one namespace.
public class BankAccount defines the class, or type, you're creating. Everything inside
the { and } that follows the class declaration defines the state and behavior of the
class. There are five member s of the BankAccount class. The first three are properties.
Properties are data elements and can have code that enforces validation or other rules.
The last two are methods . Methods are blocks of code that perform a single function.
Reading the names of each of the members should provide enough information for you
or another developer to understand what the class does.Define the bank account type
namespace  Classes;
public class BankAccount
{
    public string Number { get; }
    public string Owner { get; set; }
    public decimal Balance { get; }
    public void MakeDeposit (decimal amount, DateTime date, string note)
    {
    }
    public void MakeWithdrawal (decimal amount, DateTime date, string note)
    {
    }
}
Open a new accountThe first feature to implement is to open a bank account. When a customer opens an
account, they must supply an initial balance, and information about the owner or
owners of that account.
Creating a new object of the BankAccount type means defining a constr uctor that
assigns those values. A constr uctor is a member that has the same name as the class. It's
used to initialize objects of that class type. Add the following constructor to the
BankAccount type. Place the following code above the declaration of MakeDeposit:
C#
The preceding code identifies the properties of the object being constructed by
including the this qualifier. That qualifier is usually optional and omitted. Y ou could
also have written:
C#
The this qualifier is only required when a local variable or parameter has the same
name as that field or property. The this qualifier is omitted throughout the remainder
of this article unless it's necessary.
Constructors are called when you create an object using new. Replace the line
Console.WriteLine("Hello World!"); in Program.cs  with the following code (replace
<name> with your name):
C#public BankAccount (string name, decimal initialBalance )
{
    this.Owner = name;
    this.Balance = initialBalance;
}
public BankAccount (string name, decimal initialBalance )
{
    Owner = name;
    Balance = initialBalance;
}
using Classes;
var account = new BankAccount( "<name>" , 1000);
Console.WriteLine( $"Account {account.Number}  was created for {account.Owner}  
with {account.Balance}  initial balance." );Let's run what you've built so far. If you're using Visual S tudio, Select Start without
debugging  from the Debug  menu. If you're using a command line, type dotnet run in
the directory where you've created your project.
Did you notice that the account number is blank? It's time to fix that. The account
number should be assigned when the object is constructed. But it shouldn't be the
responsibility of the caller to create it. The BankAccount class code should know how to
assign new account numbers. A simple way is to start with a 10-digit number. Increment
it when each new account is created. Finally, store the current account number when an
object is constructed.
Add a member declaration to the BankAccount class. Place the following line of code
after the opening brace { at the beginning of the BankAccount class:
C#
The accountNumberSeed is a data member. It's private, which means it can only be
accessed by code inside the BankAccount class. It's a way of separating the public
responsibilities (like having an account number) from the private implementation (how
account numbers are generated). It's also static, which means it's shared by all of the
BankAccount objects. The value of a non-static variable is unique to each instance of the
BankAccount object. The accountNumberSeed is a private static field and thus has the
s_ prefix as per C# naming conventions. The s denoting static and _ denoting
private field. Add the following two lines to the constructor to assign the account
number. Place them after the line that says this.Balance = initialBalance:
C#
Type dotnet run to see the results.
Your bank account class needs to accept deposits and withdrawals to work correctly.
Let's implement deposits and withdrawals by creating a journal of every transaction for
the account. T racking every transaction has a few advantages over simply updating the
balance on each transaction. The history can be used to audit all transactions andprivate static int s_accountNumberSeed = 1234567890 ;
Number = s_accountNumberSeed.ToString();
s_accountNumberSeed++;
Create deposits and withdrawalsmanage daily balances. Computing the balance from the history of all transactions when
needed ensures any errors in a single transaction that are fixed will be correctly reflected
in the balance on the next computation.
Let's start by creating a new type to represent a transaction. The transaction is a simple
type that doesn't have any responsibilities. It needs a few properties. Create a new file
named Transaction.cs . Add the following code to it:
C#
Now, let's add a List<T>  of Transaction objects to the BankAccount class. Add the
following declaration after the constructor in your BankAc count.cs  file:
C#
Now, let's correctly compute the Balance. The current balance can be found by
summing the values of all transactions. As the code is currently, you can only get the
initial balance of the account, so you'll have to update the Balance property. R eplace
the line public decimal Balance { get; } in BankAc count.cs  with the following code:
C#namespace  Classes;
public class Transaction
{
    public decimal Amount { get; }
    public DateTime Date { get; }
    public string Notes { get; }
    public Transaction (decimal amount, DateTime date, string note)
    {
        Amount = amount;
        Date = date;
        Notes = note;
    }
}
private List<Transaction> _allTransactions = new List<Transaction>();
public decimal Balance
{
    get
    {
        decimal balance = 0;
        foreach (var item in _allTransactions)
        {This example shows an important aspect of properties. You're now computing the
balance when another programmer asks for the value. Y our computation enumerates all
transactions, and provides the sum as the current balance.
Next, implement the MakeDeposit and MakeWithdrawal methods. These methods will
enforce the final two rules: the initial balance must be positive, and any withdrawal must
not create a negative balance.
These rules introduce the concept of exceptions . The standard way of indicating that a
method can't complete its work successfully is to throw an exception. The type of
exception and the message associated with it describe the error. Here, the MakeDeposit
method throws an exception if the amount of the deposit isn't greater than 0. The
MakeWithdrawal method throws an exception if the withdrawal amount isn't greater than
0, or if applying the withdrawal results in a negative balance. Add the following code
after the declaration of the _allTransactions list:
C#            balance += item.Amount;
        }
        return balance;
    }
}
public void MakeDeposit (decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException( nameof(amount), "Amount of  
deposit must be positive" );
    }
    var deposit = new Transaction(amount, date, note);
    _allTransactions.Add(deposit);
}
public void MakeWithdrawal (decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException( nameof(amount), "Amount of  
withdrawal must be positive" );
    }
    if (Balance - amount < 0)
    {
        throw new InvalidOperationException( "Not sufficient funds for this  
withdrawal" );
    }
    var withdrawal = new Transaction(-amount, date, note);The throw  statement  throws an exception. Execution of the current block ends, and
control transfers to the first matching catch block found in the call stack. Y ou'll add a
catch block to test this code a little later on.
The constructor should get one change so that it adds an initial transaction, rather than
updating the balance directly. Since you already wrote the MakeDeposit method, call it
from your constructor. The finished constructor should look like this:
C#
DateTime.Now  is a property that returns the current date and time. T est this code by
adding a few deposits and withdrawals in your Main method, following the code that
creates a new BankAccount:
C#
Next, test that you're catching error conditions by trying to create an account with a
negative balance. Add the following code after the preceding code you just added:
C#    _allTransactions.Add(withdrawal);
}
public BankAccount (string name, decimal initialBalance )
{
    Number = s_accountNumberSeed.ToString();
    s_accountNumberSeed++;
    Owner = name;
    MakeDeposit(initialBalance, DateTime.Now, "Initial balance" );
}
account.MakeWithdrawal( 500, DateTime.Now, "Rent payment" );
Console.WriteLine(account.Balance);
account.MakeDeposit( 100, DateTime.Now, "Friend paid me back" );
Console.WriteLine(account.Balance);
// Test that the initial balances must be positive.
BankAccount invalidAccount;
try
{
    invalidAccount = new BankAccount( "invalid" , -55);
}
catch (ArgumentOutOfRangeException e)
{
    Console.WriteLine( "Exception caught creating account with negative  You use the try-catch  statement  to mark a block of code that may throw exceptions and
to catch those errors that you expect. Y ou can use the same technique to test the code
that throws an exception for a negative balance. Add the following code before the
declaration of invalidAccount in your Main method:
C#
Save the file and type dotnet run to try it.
To finish this tutorial, you can write the GetAccountHistory method that creates a string
for the transaction history. Add this method to the BankAccount type:
C#balance" );
    Console.WriteLine(e.ToString());
    return;
}
// Test for a negative balance.
try
{
    account.MakeWithdrawal( 750, DateTime.Now, "Attempt to overdraw" );
}
catch (InvalidOperationException e)
{
    Console.WriteLine( "Exception caught trying to overdraw" );
    Console.WriteLine(e.ToString());
}
Challenge - log all transactions
public string GetAccountHistory ()
{
    var report = new System.Text.StringBuilder();
    decimal balance = 0;
    report.AppendLine( "Date\t\tAmount\tBalance\tNote" );
    foreach (var item in _allTransactions)
    {
        balance += item.Amount;
        report.AppendLine( $"
{item.Date.ToShortDateString()} \t{item.Amount} \t{balance} \t{item.Notes} ");
    }
    return report.ToString();
}The history uses the StringBuilder  class to format a string that contains one line for each
transaction. Y ou've seen the string formatting code earlier in these tutorials. One new
character is \t. That inserts a tab to format the output.
Add this line to test it in Program.cs :
C#
Run your program to see the results.
If you got stuck, you can see the source for this tutorial in our GitHub repo .
You can continue with the object oriented programming  tutorial.
You can learn more about these concepts in these articles:
Selection statements
Iteration statementsConsole.WriteLine(account.GetAccountHistory());
Next steps
Object-Oriented programming (C#)
Article •07/11/2023
C# is an object-oriented programming language. The four basic principles of object-
oriented programming are:
Abstr action  Modeling the relevant attributes and interactions of entities as classes
to define an abstract representation of a system.
Encapsulation  Hiding the internal state and functionality of an object and only
allowing access through a public set of functions.
Inher itance Ability to create new abstractions based on existing abstractions.
Polymorphism  Ability to implement inherited properties or methods in different
ways across multiple abstractions.
In the preceding tutorial, introduction to classes  you saw both abstr action  and
encapsulation . The BankAccount class provided an abstraction for the concept of a bank
account. Y ou could modify its implementation without affecting any of the code that
used the BankAccount class. Both the BankAccount and Transaction classes provide
encapsulation of the components needed to describe those concepts in code.
In this tutorial, you'll extend that application to make use of inher itance and
polymorphism  to add new features. Y ou'll also add features to the BankAccount class,
taking advantage of the abstr action  and encapsulation  techniques you learned in the
preceding tutorial.
After building this program, you get requests to add features to it. It works great in the
situation where there is only one bank account type. Over time, needs change, and
related account types are requested:
An interest earning account that accrues interest at the end of each month.
A line of credit that can have a negative balance, but when there's a balance,
there's an interest charge each month.
A pre-paid gift card account that starts with a single deposit, and only can be paid
off. It can be refilled once at the start of each month.
All of these different accounts are similar to BankAccount class defined in the earlier
tutorial. Y ou could copy that code, rename the classes, and make modifications. That
technique would work in the short term, but it would be more work over time. Any
changes would be copied across all the affected classes.Create different types of accountsInstead, you can create new bank account types that inherit methods and data from the
BankAccount class created in the preceding tutorial. These new classes can extend the
BankAccount class with the specific behavior needed for each type:
C#
Each of these classes inher its the shared behavior from their shared base class , the
BankAccount class. Write the implementations for new and different functionality in each
of the derived class es. These derived classes already have all the behavior defined in the
BankAccount class.
It's a good practice to create each new class in a different source file. In Visual S tudio ,
you can right-click on the project, and select add class  to add a new class in a new file. In
Visual S tudio Code , select File then New to create a new source file. In either tool,
name the file to match the class: InterestEar ningAc count.cs , LineOfCr editAc count.cs , and
GiftCardAccount.cs .
When you create the classes as shown in the preceding sample, you'll find that none of
your derived classes compile. A constructor is responsible for initializing an object. A
derived class constructor must initialize the derived class, and provide instructions on
how to initialize the base class object included in the derived class. The proper
initialization normally happens without any extra code. The BankAccount class declares
one public constructor with the following signature:
C#
The compiler doesn't generate a default constructor when you define a constructor
yourself. That means each derived class must explicitly call this constructor. Y ou declare
a constructor that can pass arguments to the base class constructor. The following code
shows the constructor for the InterestEarningAccount:public class InterestEarningAccount  : BankAccount
{
}
public class LineOfCreditAccount  : BankAccount
{
}
public class GiftCardAccount  : BankAccount
{
}
public BankAccount (string name, decimal initialBalance )C#
The parameters to this new constructor match the parameter type and names of the
base class constructor. Y ou use the : base() syntax to indicate a call to a base class
constructor. Some classes define multiple constructors, and this syntax enables you to
pick which base class constructor you call. Once you've updated the constructors, you
can develop the code for each of the derived classes. The requirements for the new
classes can be stated as follows:
An interest earning account:
Will get a credit of 2% of the month-ending-balance.
A line of credit:
Can have a negative balance, but not be greater in absolute value than the
credit limit.
Will incur an interest charge each month where the end of month balance isn't
0.
Will incur a fee on each withdrawal that goes over the credit limit.
A gift card account:
Can be refilled with a specified amount once each month, on the last day of the
month.
You can see that all three of these account types have an action that takes places at the
end of each month. However, each account type does different tasks. Y ou use
polymorphism  to implement this code. Create a single virtual method in the
BankAccount class:
C#
The preceding code shows how you use the virtual keyword to declare a method in
the base class that a derived class may provide a different implementation for. A
virtual method is a method where any derived class may choose to reimplement. The
derived classes use the override keyword to define the new implementation. T ypically
you refer to this as "overriding the base class implementation". The virtual keyword
specifies that derived classes may override the behavior. Y ou can also declare abstract
methods where derived classes must override the behavior. The base class does notpublic InterestEarningAccount (string name, decimal initialBalance ) : 
base(name, initialBalance )
{
}
public virtual void PerformMonthEndTransactions () { }provide an implementation for an abstract method. Next, you need to define the
implementation for two of the new classes you've created. S tart with the
InterestEarningAccount:
C#
Add the following code to the LineOfCreditAccount. The code negates the balance to
compute a positive interest charge that is withdrawn from the account:
C#
The GiftCardAccount class needs two changes to implement its month-end
functionality. First, modify the constructor to include an optional amount to add each
month:
C#
The constructor provides a default value for the monthlyDeposit value so callers can
omit a 0 for no monthly deposit. Next, override the PerformMonthEndTransactions
method to add the monthly deposit, if it was set to a non-zero value in the constructor:public override  void PerformMonthEndTransactions ()
{
    if (Balance > 500m)
    {
        decimal interest = Balance * 0.05m;
        MakeDeposit(interest, DateTime.Now, "apply monthly interest" );
    }
}
public override  void PerformMonthEndTransactions ()
{
    if (Balance < 0)
    {
        // Negate the balance to get a positive interest charge:
        decimal interest = -Balance * 0.07m;
        MakeWithdrawal(interest, DateTime.Now, "Charge monthly interest" );
    }
}
private readonly  decimal _monthlyDeposit = 0m;
public GiftCardAccount (string name, decimal initialBalance, decimal 
monthlyDeposit = 0) : base(name, initialBalance )
    => _monthlyDeposit = monthlyDeposit;C#
The override applies the monthly deposit set in the constructor. Add the following code
to the Main method to test these changes for the GiftCardAccount and the
InterestEarningAccount:
C#
Verify the results. Now, add a similar set of test code for the LineOfCreditAccount:
C#public override  void PerformMonthEndTransactions ()
{
    if (_monthlyDeposit != 0)
    {
        MakeDeposit(_monthlyDeposit, DateTime.Now, "Add monthly deposit" );
    }
}
var giftCard = new GiftCardAccount( "gift card" , 100, 50);
giftCard.MakeWithdrawal( 20, DateTime.Now, "get expensive coffee" );
giftCard.MakeWithdrawal( 50, DateTime.Now, "buy groceries" );
giftCard.PerformMonthEndTransactions();
// can make additional deposits:
giftCard.MakeDeposit( 27.50m, DateTime.Now, "add some additional spending  
money");
Console.WriteLine(giftCard.GetAccountHistory());
var savings = new InterestEarningAccount( "savings account" , 10000);
savings.MakeDeposit( 750, DateTime.Now, "save some money" );
savings.MakeDeposit( 1250, DateTime.Now, "Add more savings" );
savings.MakeWithdrawal( 250, DateTime.Now, "Needed to pay monthly bills" );
savings.PerformMonthEndTransactions();
Console.WriteLine(savings.GetAccountHistory());
var lineOfCredit = new LineOfCreditAccount( "line of credit" , 0);
// How much is too much to borrow?
lineOfCredit.MakeWithdrawal( 1000m, DateTime.Now, "Take out monthly  
advance" );
lineOfCredit.MakeDeposit( 50m, DateTime.Now, "Pay back small amount" );
lineOfCredit.MakeWithdrawal( 5000m, DateTime.Now, "Emergency funds for  
repairs" );
lineOfCredit.MakeDeposit( 150m, DateTime.Now, "Partial restoration on  
repairs" );
lineOfCredit.PerformMonthEndTransactions();
Console.WriteLine(lineOfCredit.GetAccountHistory());When you add the preceding code and run the program, you'll see something like the
following error:
Console
This code fails because the BankAccount assumes that the initial balance must be greater
than 0. Another assumption baked into the BankAccount class is that the balance can't
go negative. Instead, any withdrawal that overdraws the account is rejected. Both of
those assumptions need to change. The line of credit account starts at 0, and generally
will have a negative balance. Also, if a customer borrows too much money, they incur a
fee. The transaction is accepted, it just costs more. The first rule can be implemented by
adding an optional argument to the BankAccount constructor that specifies the
minimum balance. The default is 0. The second rule requires a mechanism that enables
derived classes to modify the default algorithm. In a sense, the base class "asks" the
derived type what should happen when there's an overdraft. The default behavior is to
reject the transaction by throwing an exception.
Let's start by adding a second constructor that includes an optional minimumBalance
parameter. This new constructor does all the actions done by the existing constructor.
Also, it sets the minimum balance property. Y ou could copy the body of the existing
constructor, but that means two locations to change in the future. Instead, you can use
constr uctor chaining  to have one constructor call another. The following code shows the
two constructors and the new additional field:
C#Unhandled exception. System.ArgumentOutOfRangeException: Amount of deposit  
must be positive (Parameter 'amount')
   at OOProgramming.BankAccount.MakeDeposit(Decimal amount, DateTime date,  
String note) in BankAccount.cs:line 42
   at OOProgramming.BankAccount..ctor(String name, Decimal initialBalance)  
in BankAccount.cs:line 31
   at OOProgramming.LineOfCreditAccount..ctor(String name, Decimal  
initialBalance) in LineOfCreditAccount.cs:line 9
   at OOProgramming.Program.Main(String[] args) in Program.cs:line 29
７ Note
The actual output includes the full path to the folder with the project. The folder
names were omitted for brevity. Also, depending on your code format, the line
numbers may be slightly different.The preceding code shows two new techniques. First, the minimumBalance field is marked
as readonly. That means the value cannot be changed after the object is constructed.
Once a BankAccount is created, the minimumBalance can't change. Second, the
constructor that takes two parameters uses : this(name, initialBalance, 0) { } as its
implementation. The : this() expression calls the other constructor, the one with three
parameters. This technique allows you to have a single implementation for initializing an
object even though client code can choose one of many constructors.
This implementation calls MakeDeposit only if the initial balance is greater than 0. That
preserves the rule that deposits must be positive, yet lets the credit account open with a
0 balance.
Now that the BankAccount class has a read-only field for the minimum balance, the final
change is to change the hard code 0 to minimumBalance in the MakeWithdrawal method:
C#
After extending the BankAccount class, you can modify the LineOfCreditAccount
constructor to call the new base constructor, as shown in the following code:
C#private readonly  decimal _minimumBalance;
public BankAccount (string name, decimal initialBalance ) : this(name, 
initialBalance, 0) { }
public BankAccount (string name, decimal initialBalance, decimal 
minimumBalance )
{
    Number = s_accountNumberSeed.ToString();
    s_accountNumberSeed++;
    Owner = name;
    _minimumBalance = minimumBalance;
    if (initialBalance > 0)
        MakeDeposit(initialBalance, DateTime.Now, "Initial balance" );
}
if (Balance - amount < _minimumBalance)
public LineOfCreditAccount (string name, decimal initialBalance, decimal 
creditLimit ) : base(name, initialBalance, -creditLimit )
{
}Notice that the LineOfCreditAccount constructor changes the sign of the creditLimit
parameter so it matches the meaning of the minimumBalance parameter.
The last feature to add enables the LineOfCreditAccount to charge a fee for going over
the credit limit instead of refusing the transaction.
One technique is to define a virtual function where you implement the required
behavior. The BankAccount class refactors the MakeWithdrawal method into two
methods. The new method does the specified action when the withdrawal takes the
balance below the minimum. The existing MakeWithdrawal method has the following
code:
C#
Replace it with the following code:
C#Different overdraft rules
public void MakeWithdrawal (decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException( nameof(amount), "Amount of  
withdrawal must be positive" );
    }
    if (Balance - amount < _minimumBalance)
    {
        throw new InvalidOperationException( "Not sufficient funds for this  
withdrawal" );
    }
    var withdrawal = new Transaction(-amount, date, note);
    _allTransactions.Add(withdrawal);
}
public void MakeWithdrawal (decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException( nameof(amount), "Amount of  
withdrawal must be positive" );
    }
    Transaction? overdraftTransaction = CheckWithdrawalLimit(Balance -  
amount < _minimumBalance);
    Transaction? withdrawal = new(-amount, date, note);
    _allTransactions.Add(withdrawal);
    if (overdraftTransaction != null)The added method is protected, which means that it can be called only from derived
classes. That declaration prevents other clients from calling the method. It's also
virtual so that derived classes can change the behavior. The return type is a
Transaction?. The ? annotation indicates that the method may return null. Add the
following implementation in the LineOfCreditAccount to charge a fee when the
withdrawal limit is exceeded:
C#
The override returns a fee transaction when the account is overdrawn. If the withdrawal
doesn't go over the limit, the method returns a null transaction. That indicates there's
no fee. T est these changes by adding the following code to your Main method in the
Program class:
C#        _allTransactions.Add(overdraftTransaction);
}
protected  virtual Transaction? CheckWithdrawalLimit( bool isOverdrawn)
{
    if (isOverdrawn)
    {
        throw new InvalidOperationException( "Not sufficient funds for this  
withdrawal" );
    }
    else
    {
        return default;
    }
}
protected  override  Transaction? CheckWithdrawalLimit( bool isOverdrawn) =>
    isOverdrawn
    ? new Transaction( -20, DateTime.Now, "Apply overdraft fee" )
    : default;
var lineOfCredit = new LineOfCreditAccount( "line of credit" , 0, 2000);
// How much is too much to borrow?
lineOfCredit.MakeWithdrawal( 1000m, DateTime.Now, "Take out monthly  
advance" );
lineOfCredit.MakeDeposit( 50m, DateTime.Now, "Pay back small amount" );
lineOfCredit.MakeWithdrawal( 5000m, DateTime.Now, "Emergency funds for  
repairs" );
lineOfCredit.MakeDeposit( 150m, DateTime.Now, "Partial restoration on  
repairs" );Run the program, and check the results.
If you got stuck, you can see the source for this tutorial in our GitHub repo .
This tutorial demonstrated many of the techniques used in Object-Oriented
programming:
You used Abstr action  when you defined classes for each of the different account
types. Those classes described the behavior for that type of account.
You used Encapsulation  when you kept many details private in each class.
You used Inher itance when you leveraged the implementation already created in
the BankAccount class to save code.
You used Polymorphism  when you created virtual methods that derived classes
could override to create specific behavior for that account type.lineOfCredit.PerformMonthEndTransactions();
Console.WriteLine(lineOfCredit.GetAccountHistory());
Summary
Inheritance in C# and .NET
Article •02/03/2023
This tutorial introduces you to inheritance in C#. Inheritance is a feature of object-
oriented programming languages that allows you to define a base class that provides
specific functionality (data and behavior) and to define derived classes that either inherit
or override that functionality.
We recommend Visual S tudio  for Windows or Mac. Y ou can download a free
version from the Visual S tudio downloads page . Visual S tudio includes the .NET
SDK.
You can also use the Visual S tudio Code  editor. Y ou'll need to install the latest
.NET SDK  separately.
If you prefer a different editor, you need to install the latest .NET SDK .
To create and run the examples in this tutorial, you use the dotnet  utility from the
command line. Follow these steps for each example:
1. Create a directory to store the example.
2. Enter the dotnet new console  command at a command prompt to create a new
.NET Core project.
3. Copy and paste the code from the example into your code editor.
4. Enter the dotnet restore  command from the command line to load or restore the
project's dependencies.
You don't have to run dotnet restore  because it's run implicitly by all commands
that require a restore to occur, such as dotnet new, dotnet build, dotnet run,
dotnet test, dotnet publish, and dotnet pack. To disable implicit restore, use the
--no-restore option.
The dotnet restore command is still useful in certain scenarios where explicitly
restoring makes sense, such as continuous integration builds in Azure DevOps
Services  or in build systems that need to explicitly control when the restore occurs.Prerequisites
Running  the examplesFor information about how to manage NuGet feeds, see the dotnet restore
documentation .
5. Enter the dotnet run  command to compile and execute the example.
Inher itance is one of the fundamental attributes of object-oriented programming. It
allows you to define a child class that reuses (inherits), extends, or modifies the behavior
of a parent class. The class whose members are inherited is called the base class . The
class that inherits the members of the base class is called the derived class .
C# and .NET support single inher itance only. That is, a class can only inherit from a single
class. However, inheritance is transitive, which allows you to define an inheritance
hierarchy for a set of types. In other words, type D can inherit from type C, which
inherits from type B, which inherits from the base class type A. Because inheritance is
transitive, the members of type A are available to type D.
Not all members of a base class are inherited by derived classes. The following members
are not inherited:
Static constructors , which initialize the static data of a class.
Instance constructors , which you call to create a new instance of the class. Each
class must define its own constructors.
Finalizers , which are called by the runtime's garbage collector to destroy instances
of a class.
While all other members of a base class are inherited by derived classes, whether they
are visible or not depends on their accessibility. A member's accessibility affects its
visibility for derived classes as follows:
Private  members are visible only in derived classes that are nested in their base
class. Otherwise, they are not visible in derived classes. In the following example,
A.B is a nested class that derives from A, and C derives from A. The private
A._value field is visible in A.B. However, if you remove the comments from the
C.GetValue method and attempt to compile the example, it produces compiler
error CS0122: "'A._value' is inaccessible due to its protection level."
C#Background: What is inheritance?
public class A 
{ Protected  members are visible only in derived classes.
Internal  members are visible only in derived classes that are located in the same
assembly as the base class. They are not visible in derived classes located in a
different assembly from the base class.
Public  members are visible in derived classes and are part of the derived class'
public interface. Public inherited members can be called just as if they are defined
in the derived class. In the following example, class A defines a method named
Method1, and class B inherits from class A. The example then calls Method1 as if it
were an instance method on B.
C#    private int _value = 10; 
    public class B : A 
    { 
        public int GetValue () 
        {  
            return _value;  
        }  
    } 
} 
public class C : A 
{ 
    //    public int GetValue()  
    //    { 
    //        return _value;  
    //    } 
} 
public class AccessExample  
{ 
    public static void Main(string[] args) 
    { 
        var b = new A.B(); 
        Console.WriteLine(b.GetValue());  
    } 
} 
// The example displays the following output:  
//       10  
public class A 
{ 
    public void Method1() 
    { 
        // Method implementation.
    } Derived classes can also override inherited members by providing an alternate
implementation. In order to be able to override a member, the member in the base class
must be marked with the virtual  keyword. By default, base class members are not
marked as virtual and cannot be overridden. Attempting to override a non-virtual
member, as the following example does, generates compiler error CS0506: "<member>
cannot override inherited member <member> because it is not marked virtual, abstract,
or override."
C#
In some cases, a derived class must  override the base class implementation. Base class
members marked with the abstract  keyword require that derived classes override them.
Attempting to compile the following example generates compiler error CS0534, "
<class> does not implement inherited abstract member <member>", because class B
provides no implementation for A.Method1.
C#} 
public class B : A 
{ } 
public class Example 
{ 
    public static void Main() 
    { 
        B b = new (); 
        b.Method1();  
    } 
} 
public class A 
{ 
    public void Method1() 
    { 
        // Do something.  
    } 
} 
public class B : A 
{ 
    public override  void Method1() // Generates CS0506.  
    { 
        // Do something else.  
    } 
} Inheritance applies only to classes and interfaces. Other type categories (structs,
delegates, and enums) do not support inheritance. Because of these rules, attempting to
compile code like the following example produces compiler error CS0527: "T ype
'ValueT ype' in interface list is not an interface." The error message indicates that,
although you can define the interfaces that a struct implements, inheritance is not
supported.
C#
Besides any types that they may inherit from through single inheritance, all types in the
.NET type system implicitly inherit from Object  or a type derived from it. The common
functionality of Object  is available to any type.
To see what implicit inheritance means, let's define a new class, SimpleClass, that is
simply an empty class definition:
C#
You can then use reflection (which lets you inspect a type's metadata to get information
about that type) to get a list of the members that belong to the SimpleClass type.
Although you haven't defined any members in your SimpleClass class, output from the
example indicates that it actually has nine members. One of these members is apublic abstract  class A 
{ 
    public abstract  void Method1(); 
} 
public class B : A // Generates CS0534.  
{ 
    public void Method3() 
    { 
        // Do something.  
    } 
} 
public struct ValueStructure : ValueType // Generates CS0527.  
{ 
} 
Implicit inheritance
public class SimpleClass  
{ } parameterless (or default) constructor that is automatically supplied for the SimpleClass
type by the C# compiler. The remaining eight are members of Object , the type from
which all classes and interfaces in the .NET type system ultimately implicitly inherit.
C#
using System.Reflection;  
public class SimpleClassExample  
{ 
    public static void Main() 
    { 
        Type t = typeof(SimpleClass);  
        BindingFlags flags = BindingFlags.Instance | BindingFlags.Static |  
BindingFlags.Public |  
                             BindingFlags.NonPublic |  
BindingFlags.FlattenHierarchy;  
        MemberInfo[] members = t.GetMembers(flags);  
        Console.WriteLine( $"Type {t.Name}  has {members.Length}  members: " ); 
        foreach (MemberInfo member in members)  
        {  
            string access = ""; 
            string stat = ""; 
            var method = member as MethodBase;  
            if (method != null) 
            {  
                if (method.IsPublic)  
                    access = " Public" ; 
                else if (method.IsPrivate)  
                    access = " Private" ; 
                else if (method.IsFamily)  
                    access = " Protected" ; 
                else if (method.IsAssembly)  
                    access = " Internal" ; 
                else if (method.IsFamilyOrAssembly)  
                    access = " Protected Internal " ; 
                if (method.IsStatic)  
                    stat = " Static" ; 
            }  
            string output = $"{member.Name}  ({member.MemberType} ): {access}
{stat}, Declared by {member.DeclaringType} "; 
            Console.WriteLine(output);  
        }  
    } 
} 
// The example displays the following output:  
// Type SimpleClass has 9 members:  
// ToString (Method):  Public, Declared by System.Object  
// Equals (Method):  Public, Declared by System.Object  
// Equals (Method):  Public Static, Declared by System.Object  
// ReferenceEquals (Method):  Public Static, Declared by System.Object  
// GetHashCode (Method):  Public, Declared by System.Object  
// GetType (Method):  Public, Declared by System.Object  Implicit inheritance from the Object  class makes these methods available to the
SimpleClass class:
The public ToString method, which converts a SimpleClass object to its string
representation, returns the fully qualified type name. In this case, the ToString
method returns the string "SimpleClass".
Three methods that test for equality of two objects: the public instance
Equals(Object) method, the public static Equals(Object, Object) method, and the
public static ReferenceEquals(Object, Object) method. By default, these methods
test for reference equality; that is, to be equal, two object variables must refer to
the same object.
The public GetHashCode method, which computes a value that allows an instance of
the type to be used in hashed collections.
The public GetType method, which returns a Type object that represents the
SimpleClass type.
The protected Finalize  method, which is designed to release unmanaged resources
before an object's memory is reclaimed by the garbage collector.
The protected MemberwiseClone  method, which creates a shallow clone of the
current object.
Because of implicit inheritance, you can call any inherited member from a SimpleClass
object just as if it was actually a member defined in the SimpleClass class. For instance,
the following example calls the SimpleClass.ToString method, which SimpleClass
inherits from Object .
C#// Finalize (Method):  Internal, Declared by System.Object  
// MemberwiseClone (Method):  Internal, Declared by System.Object  
// .ctor (Constructor):  Public, Declared by SimpleClass  
public class EmptyClass
{ } 
public class ClassNameExample  
{ 
    public static void Main() 
    { 
        EmptyClass sc = new(); 
        Console.WriteLine(sc.ToString());  
    } The following table lists the categories of types that you can create in C# and the types
from which they implicitly inherit. Each base type makes a different set of members
available through inheritance to implicitly derived types.
Type cat egor y Implicitly inher its fr om
class Object
struct ValueT ype, Object
enum Enum , ValueT ype, Object
delegate MulticastDelegate , Delegate , Object
Ordinarily, inheritance is used to express an "is a" relationship between a base class and
one or more derived classes, where the derived classes are specialized versions of the
base class; the derived class is a type of the base class. For example, the Publication
class represents a publication of any kind, and the Book and Magazine classes represent
specific types of publications.
Note that "is a" also expresses the relationship between a type and a specific
instantiation of that type. In the following example, Automobile is a class that has three
unique read-only properties: Make, the manufacturer of the automobile; Model, the kind
of automobile; and Year, its year of manufacture. Y our Automobile class also has a
constructor whose arguments are assigned to the property values, and it overrides the} 
// The example displays the following output:  
//        EmptyClass  
Inheritance and an "is a" relationship
７ Note
A class or struct can implement one or more interfaces. While interface
implementation is often presented as a workaround for single inheritance or as a
way of using inheritance with structs, it is intended to express a different
relationship (a "can do" relationship) between an interface and its implementing
type than inheritance. An interface defines a subset of functionality (such as the
ability to test for equality, to compare or sort objects, or to support culture-
sensitive parsing and formatting) that the interface makes available to its
implementing types.Object.T oString  method to produce a string that uniquely identifies the Automobile
instance rather than the Automobile class.
C#
In this case, you shouldn't rely on inheritance to represent specific car makes and
models. For example, you don't need to define a Packard type to represent automobiles
manufactured by the P ackard Motor Car Company. Instead, you can represent them by
creating an Automobile object with the appropriate values passed to its class
constructor, as the following example does.
C#public class Automobile
{ 
    public Automobile (string make, string model, int year) 
    { 
        if (make == null) 
            throw new ArgumentNullException( nameof(make), "The make cannot  
be null." ); 
        else if (string.IsNullOrWhiteSpace(make))  
            throw new ArgumentException( "make cannot be an empty string or  
have space characters only." ); 
        Make = make;  
        if (model == null) 
            throw new ArgumentNullException( nameof(model), "The model cannot  
be null." ); 
        else if (string.IsNullOrWhiteSpace(model))  
            throw new ArgumentException( "model cannot be an empty string or  
have space characters only." ); 
        Model = model;  
        if (year < 1857 || year > DateTime.Now.Year + 2)
            throw new ArgumentException( "The year is out of range." ); 
        Year = year;  
    } 
    public string Make { get; } 
    public string Model { get; } 
    public int Year { get; } 
    public override  string ToString () => $"{Year} {Make} {Model}"; 
} 
using System;  
public class Example An is-a relationship based on inheritance is best applied to a base class and to derived
classes that add additional members to the base class or that require additional
functionality not present in the base class.
Let's look at the process of designing a base class and its derived classes. In this section,
you'll define a base class, Publication, which represents a publication of any kind, such
as a book, a magazine, a newspaper, a journal, an article, etc. Y ou'll also define a Book
class that derives from Publication. You could easily extend the example to define other
derived classes, such as Magazine, Journal, Newspaper, and Article.
In designing your Publication class, you need to make several design decisions:
What members to include in your base Publication class, and whether the
Publication members provide method implementations or whether Publication
is an abstract base class that serves as a template for its derived classes.
In this case, the Publication class will provide method implementations. The
Designing abstract base classes and their derived classes  section contains an
example that uses an abstract base class to define the methods that derived
classes must override. Derived classes are free to provide any implementation that
is suitable for the derived type.
The ability to reuse code (that is, multiple derived classes share the declaration and
implementation of base class methods and do not need to override them) is an
advantage of non-abstract base classes. Therefore, you should add members to
Publication if their code is likely to be shared by some or most specialized
Publication types. If you fail to provide base class implementations efficiently,
you'll end up having to provide largely identical member implementations in{ 
    public static void Main() 
    { 
        var packard = new Automobile( "Packard" , "Custom Eight" , 1948); 
        Console.WriteLine(packard);  
    } 
} 
// The example displays the following output:  
//        1948 Packard Custom Eight  
Designing the base class and derived classes
The base Publication classderived classes rather a single implementation in the base class. The need to
maintain duplicated code in multiple locations is a potential source of bugs.
Both to maximize code reuse and to create a logical and intuitive inheritance
hierarchy, you want to be sure that you include in the Publication class only the
data and functionality that is common to all or to most publications. Derived
classes then implement members that are unique to the particular kinds of
publication that they represent.
How far to extend your class hierarchy. Do you want to develop a hierarchy of
three or more classes, rather than simply a base class and one or more derived
classes? For example, Publication could be a base class of Periodical, which in
turn is a base class of Magazine, Journal and Newspaper.
For your example, you'll use the small hierarchy of a Publication class and a single
derived class, Book. You could easily extend the example to create a number of
additional classes that derive from Publication, such as Magazine and Article.
Whether it makes sense to instantiate the base class. If it does not, you should
apply the abstract  keyword to the class. Otherwise, your Publication class can be
instantiated by calling its class constructor. If an attempt is made to instantiate a
class marked with the abstract keyword by a direct call to its class constructor, the
C# compiler generates error CS0144, "Cannot create an instance of the abstract
class or interface." If an attempt is made to instantiate the class by using reflection,
the reflection method throws a MemberAccessException .
By default, a base class can be instantiated by calling its class constructor. Y ou do
not have to explicitly define a class constructor. If one is not present in the base
class' source code, the C# compiler automatically provides a default
(parameterless) constructor.
For your example, you'll mark the Publication class as abstract  so that it cannot
be instantiated. An abstract class without any abstract methods indicates that
this class represents an abstract concept that is shared among several concrete
classes (like a Book, Journal).
Whether derived classes must inherit the base class implementation of particular
members, whether they have the option to override the base class implementation,
or whether they must provide an implementation. Y ou use the abstract  keyword to
force derived classes to provide an implementation. Y ou use the virtual  keyword to
allow derived classes to override a base class method. By default, methods defined
in the base class are not overridable.The Publication class does not have any abstract methods, but the class itself is
abstract.
Whether a derived class represents the final class in the inheritance hierarchy and
cannot itself be used as a base class for additional derived classes. By default, any
class can serve as a base class. Y ou can apply the sealed  keyword to indicate that a
class cannot serve as a base class for any additional classes. Attempting to derive
from a sealed class generated compiler error CS0509, "cannot derive from sealed
type <typeName>."
For your example, you'll mark your derived class as sealed.
The following example shows the source code for the Publication class, as well as a
PublicationType enumeration that is returned by the Publication.PublicationType
property. In addition to the members that it inherits from Object , the Publication class
defines the following unique members and member overrides:
C#
public enum PublicationType { Misc, Book, Magazine, Article };  
public abstract  class Publication  
{ 
    private bool _published = false; 
    private DateTime _datePublished;  
    private int _totalPages;  
    public Publication (string title, string publisher, PublicationType type ) 
    { 
        if (string.IsNullOrWhiteSpace(publisher))  
            throw new ArgumentException( "The publisher is required." ); 
        Publisher = publisher;  
        if (string.IsNullOrWhiteSpace(title))  
            throw new ArgumentException( "The title is required." ); 
        Title = title;  
        Type = type;  
    } 
    public string Publisher { get; } 
    public string Title { get; } 
    public PublicationType Type { get; } 
    public string? CopyrightName { get; private set; } 
    public int CopyrightDate { get; private set; } A constructor
Because the Publication class is abstract, it cannot be instantiated directly from
code like the following example:
C#    public int Pages 
    { 
        get { return _totalPages; }  
        set 
        {  
            if (value <= 0) 
                throw new ArgumentOutOfRangeException( nameof(value), "The 
number of pages cannot be zero or negative." ); 
            _totalPages = value; 
        }  
    } 
    public string GetPublicationDate () 
    { 
        if (!_published)  
            return "NYP"; 
        else 
            return _datePublished.ToString( "d"); 
    } 
    public void Publish(DateTime datePublished ) 
    { 
        _published = true; 
        _datePublished = datePublished;  
    } 
    public void Copyright (string copyrightName, int copyrightDate ) 
    { 
        if (string.IsNullOrWhiteSpace(copyrightName))  
            throw new ArgumentException( "The name of the copyright holder is  
required." ); 
        CopyrightName = copyrightName;  
        int currentYear = DateTime.Now.Year;  
        if (copyrightDate < currentYear - 10 || copyrightDate > currentYear  
+ 2) 
            throw new ArgumentOutOfRangeException( $"The copyright year must  
be between {currentYear - 10} and {currentYear + 1}"); 
        CopyrightDate = copyrightDate;  
    } 
    public override  string ToString () => Title;  
} However, its instance constructor can be called directly from derived class
constructors, as the source code for the Book class shows.
Two publication-related properties
Title is a read-only String  property whose value is supplied by calling the
Publication constructor.
Pages is a read-write Int32  property that indicates how many total pages the
publication has. The value is stored in a private field named totalPages. It must be
a positive number or an ArgumentOutOfRangeException  is thrown.
Publisher-related members
Two read-only properties, Publisher and Type. The values are originally supplied
by the call to the Publication class constructor.
Publishing-related members
Two methods, Publish and GetPublicationDate, set and return the publication
date. The Publish method sets a private published flag to true when it is called
and assigns the date passed to it as an argument to the private datePublished
field. The GetPublicationDate method returns the string "NYP" if the published
flag is false, and the value of the datePublished field if it is true.
Copyright-related members
The Copyright method takes the name of the copyright holder and the year of the
copyright as arguments and assigns them to the CopyrightName and CopyrightDate
properties.
An override of the ToString method
If a type does not override the Object.T oString  method, it returns the fully qualified
name of the type, which is of little use in differentiating one instance from another.
The Publication class overrides Object.T oString  to return the value of the Title
property.var publication = new Publication( "Tiddlywinks for Experts" , "Fun and  
Games", 
                                  PublicationType.Book);  The following figure illustrates the relationship between your base Publication class
and its implicitly inherited Object  class.
The Book class represents a book as a specialized type of publication. The following
example shows the source code for the Book class.
C#The Book class
using System;  
public sealed class Book : Publication  
{ 
    public Book(string title, string author, string publisher ) : 
           this(title, string.Empty, author, publisher ) 
    { } 
    public Book(string title, string isbn, string author, string publisher ) 
: base(title, publisher, PublicationType.Book ) 
    { 
        // isbn argument must be a 10- or 13-character numeric string  without "-" characters.  
        // We could also determine whether the ISBN is valid by comparing  
its checksum digit  
        // with a computed checksum.  
        // 
        if (!string.IsNullOrEmpty(isbn))  
        {  
            // Determine if ISBN length is correct.  
            if (!(isbn.Length == 10 | isbn.Length == 13)) 
                throw new ArgumentException( "The ISBN must be a 10- or 13-
character numeric string." ); 
            if (!ulong.TryParse(isbn, out _)) 
                throw new ArgumentException( "The ISBN can consist of numeric  
characters only." ); 
        }  
        ISBN = isbn;  
        Author = author;  
    } 
    public string ISBN { get; } 
    public string Author { get; } 
    public decimal Price { get; private set; } 
    // A three-digit ISO currency symbol.  
    public string? Currency { get; private set; } 
    // Returns the old price, and sets a new price.  
    public decimal SetPrice (decimal price, string currency ) 
    { 
        if (price < 0) 
            throw new ArgumentOutOfRangeException( nameof(price), "The price  
cannot be negative." ); 
        decimal oldValue = Price;
        Price = price;  
        if (currency.Length != 3) 
            throw new ArgumentException( "The ISO currency symbol is a 3-
character string." ); 
        Currency = currency;  
        return oldValue;  
    } 
    public override  bool Equals(object? obj) 
    { 
        if (obj is not Book book)  
            return false; 
        else 
            return ISBN == book.ISBN;  
    } 
    public override  int GetHashCode () => ISBN.GetHashCode();  In addition to the members that it inherits from Publication, the Book class defines the
following unique members and member overrides:
Two constructors
The two Book constructors share three common parameters. T wo, title and
publisher , correspond to parameters of the Publication constructor. The third is
author , which is stored to a public immutable Author property. One constructor
includes an isbn parameter, which is stored in the ISBN auto-property.
The first constructor uses the this keyword to call the other constructor.
Constructor chaining is a common pattern in defining constructors. Constructors
with fewer parameters provide default values when calling the constructor with the
greatest number of parameters.
The second constructor uses the base keyword to pass the title and publisher
name to the base class constructor. If you don't make an explicit call to a base class
constructor in your source code, the C# compiler automatically supplies a call to
the base class' default or parameterless constructor.
A read-only ISBN property, which returns the Book object's International S tandard
Book Number, a unique 10- or 13-digit number. The ISBN is supplied as an
argument to one of the Book constructors. The ISBN is stored in a private backing
field, which is auto-generated by the compiler.
A read-only Author property. The author name is supplied as an argument to both
Book constructors and is stored in the property.
Two read-only price-related properties, Price and Currency. Their values are
provided as arguments in a SetPrice method call. The Currency property is the
three-digit ISO currency symbol (for example, USD for the U.S. dollar). ISO currency
symbols can be retrieved from the ISOCurrencyS ymbol  property. Both of these
properties are externally read-only, but both can be set by code in the Book class.
A SetPrice method, which sets the values of the Price and Currency properties.
Those values are returned by those same properties.    public override  string ToString () => $"{(string.IsNullOrEmpty(Author) ?  
"" : Author + ", ")}{Title}"; 
} Overrides to the ToString method (inherited from Publication) and the
Object.Equals(Object)  and GetHashCode  methods (inherited from Object ).
Unless it is overridden, the Object.Equals(Object)  method tests for reference
equality. That is, two object variables are considered to be equal if they refer to the
same object. In the Book class, on the other hand, two Book objects should be
equal if they have the same ISBN.
When you override the Object.Equals(Object)  method, you must also override the
GetHashCode  method, which returns a value that the runtime uses to store items
in hashed collections for efficient retrieval. The hash code should return a value
that's consistent with the test for equality. Since you've overridden
Object.Equals(Object)  to return true if the ISBN properties of two Book objects are
equal, you return the hash code computed by calling the GetHashCode  method of
the string returned by the ISBN property.
The following figure illustrates the relationship between the Book class and Publication,
its base class.You can now instantiate a Book object, invoke both its unique and inherited members,
and pass it as an argument to a method that expects a parameter of type Publication
or of type Book, as the following example shows.
C#
public class ClassExample  
{ 
    public static void Main() 
    { 
        var book = new Book("The Tempest" , "0971655819" , "Shakespeare,  
William" , In the previous example, you defined a base class that provided an implementation for a
number of methods to allow derived classes to share code. In many cases, however, the
base class is not expected to provide an implementation. Instead, the base class is an
abstr act class  that declares abstr act methods ; it serves as a template that defines the
members that each derived class must implement. T ypically in an abstract base class, the
implementation of each derived type is unique to that type. Y ou marked the class with
the abstract keyword because it made no sense to instantiate a Publication object,
although the class did provide implementations of functionality common to
publications.
For example, each closed two-dimensional geometric shape includes two properties:
area, the inner extent of the shape; and perimeter, or the distance along the edges of
the shape. The way in which these properties are calculated, however, depends
completely on the specific shape. The formula for calculating the perimeter (or
circumference) of a circle, for example, is different from that of a square. The Shape class
is an abstract class with abstract methods. That indicates derived classes share the
same functionality, but those derived classes implement that functionality differently.                            "Public Domain Press" ); 
        ShowPublicationInfo(book);  
        book.Publish( new DateTime( 2016, 8, 18)); 
        ShowPublicationInfo(book);  
        var book2 = new Book("The Tempest" , "Classic Works Press" , 
"Shakespeare, William" ); 
        Console.Write( $"{book.Title}  and {book2.Title}  are the same  
publication: "  + 
              $"{((Publication)book).Equals(book2)} "); 
    } 
    public static void ShowPublicationInfo (Publication pub ) 
    { 
        string pubDate = pub.GetPublicationDate();  
        Console.WriteLine( $"{pub.Title} , " + 
                  $"{(pubDate == "NYP" ? "Not Yet Published"  : "published on  
" + pubDate):d}  by {pub.Publisher} "); 
    } 
} 
// The example displays the following output:  
//        The Tempest, Not Yet Published by Public Domain Press  
//        The Tempest, published on 8/18/2016 by Public Domain Press  
//        The Tempest and The Tempest are the same publication: False  
Designing abstract base classes and their
derived classesThe following example defines an abstract base class named Shape that defines two
properties: Area and Perimeter. In addition to marking the class with the abstract
keyword, each instance member is also marked with the abstract  keyword. In this case,
Shape also overrides the Object.T oString  method to return the name of the type, rather
than its fully qualified name. And it defines two static members, GetArea and
GetPerimeter, that allow callers to easily retrieve the area and perimeter of an instance
of any derived class. When you pass an instance of a derived class to either of these
methods, the runtime calls the method override of the derived class.
C#
You can then derive some classes from Shape that represent specific shapes. The
following example defines three classes, Square, Rectangle, and Circle. Each uses a
formula unique for that particular shape to compute the area and perimeter. Some of
the derived classes also define properties, such as Rectangle.Diagonal and
Circle.Diameter, that are unique to the shape that they represent.
C#public abstract  class Shape 
{ 
    public abstract  double Area { get; } 
    public abstract  double Perimeter { get; } 
    public override  string ToString () => GetType().Name;  
    public static double GetArea(Shape shape ) => shape.Area;  
    public static double GetPerimeter (Shape shape ) => shape.Perimeter;  
} 
using System;  
public class Square : Shape 
{ 
    public Square(double length) 
    { 
        Side = length;  
    } 
    public double Side { get; } 
    public override  double Area => Math.Pow(Side, 2); 
    public override  double Perimeter => Side * 4; 
    public double Diagonal => Math.Round(Math.Sqrt( 2) * Side, 2); The following example uses objects derived from Shape. It instantiates an array of
objects derived from Shape and calls the static methods of the Shape class, which wraps
return Shape property values. The runtime retrieves values from the overridden
properties of the derived types. The example also casts each Shape object in the array to
its derived type and, if the cast succeeds, retrieves properties of that particular subclass
of Shape.} 
public class Rectangle  : Shape 
{ 
    public Rectangle (double length, double width) 
    { 
        Length = length;  
        Width = width;  
    } 
    public double Length { get; } 
    public double Width { get; } 
    public override  double Area => Length * Width;  
    public override  double Perimeter => 2 * Length + 2 * Width;  
    public bool IsSquare () => Length == Width;
    public double Diagonal => Math.Round(Math.Sqrt(Math.Pow(Length, 2) + 
Math.Pow(Width, 2)), 2); 
} 
public class Circle : Shape 
{ 
    public Circle(double radius) 
    { 
        Radius = radius;  
    } 
    public override  double Area => Math.Round(Math.PI * Math.Pow(Radius, 2), 
2); 
    public override  double Perimeter => Math.Round(Math.PI * 2 * Radius, 2); 
    // Define a circumference, since it's the more familiar term.  
    public double Circumference => Perimeter;  
    public double Radius { get; } 
    public double Diameter => Radius * 2; 
} C#
using System;  
public class Example 
{ 
    public static void Main() 
    { 
        Shape[] shapes = { new Rectangle( 10, 12), new Square( 5), 
                    new Circle( 3) }; 
        foreach (Shape shape in shapes)  
        {  
            Console.WriteLine( $"{shape}: area, {Shape.GetArea(shape)} ; " + 
                              $"perimeter, {Shape.GetPerimeter(shape)} "); 
            if (shape is Rectangle rect)  
            {  
                Console.WriteLine( $"   Is Square: {rect.IsSquare()} , 
Diagonal: {rect.Diagonal} "); 
                continue ; 
            }  
            if (shape is Square sq)  
            {  
                Console.WriteLine( $"   Diagonal: {sq.Diagonal} "); 
                continue ; 
            }  
        }  
    } 
} 
// The example displays the following output:  
//         Rectangle: area, 120; perimeter, 44  
//            Is Square: False, Diagonal: 15.62  
//         Square: area, 25; perimeter, 20  
//            Diagonal: 7.07  
//         Circle: area, 28.27; perimeter, 18.85  How to safely cast by using pattern
matching and the is and as operators
Article •03/11/2022
Because objects are polymorphic, it's possible for a variable of a base class type to hold
a derived type. To access the derived type's instance members, it's necessary to cast the
value back to the derived type. However, a cast creates the risk of throwing an
InvalidCastException . C# provides pattern matching  statements that perform a cast
conditionally only when it will succeed. C# also provides the is and as operators to test if
a value is of a certain type.
The following example shows how to use the pattern matching is statement:
C#
var g = new Giraffe();  
var a = new Animal();  
FeedMammals(g);  
FeedMammals(a);  
// Output:  
// Eating.  
// Animal is not a Mammal  
SuperNova sn = new SuperNova();  
TestForMammals(g);  
TestForMammals(sn);  
static void FeedMammals (Animal a ) 
{ 
    if (a is Mammal m)  
    { 
        m.Eat();  
    } 
    else 
    { 
        // variable 'm' is not in scope here, and can't be used.  
        Console.WriteLine( $"{a.GetType().Name}  is not a Mammal" ); 
    } 
} 
static void TestForMammals (object o) 
{ 
    // You also can use the as operator and test for null  
    // before referencing the variable.  
    var m = o as Mammal;  
    if (m != null) 
    { 
        Console.WriteLine(m.ToString());  The preceding sample demonstrates a few features of pattern matching syntax. The if
(a is Mammal m) statement combines the test with an initialization assignment. The
assignment occurs only when the test succeeds. The variable m is only in scope in the
embedded if statement where it has been assigned. Y ou can't access m later in the
same method. The preceding example also shows how to use the as operator  to convert
an object to a specified type.
You can also use the same syntax for testing if a nullable value type  has a value, as
shown in the following example:
C#    } 
    else 
    { 
        Console.WriteLine( $"{o.GetType().Name}  is not a Mammal" ); 
    } 
} 
// Output:  
// I am an animal.  
// SuperNova is not a Mammal  
class Animal 
{ 
    public void Eat() { Console.WriteLine( "Eating." ); } 
    public override  string ToString () 
    { 
        return "I am an animal." ; 
    } 
} 
class Mammal : Animal { } 
class Giraffe : Mammal { } 
class SuperNova  { } 
int i = 5; 
PatternMatchingNullable(i);  
int? j = null; 
PatternMatchingNullable(j);  
double d = 9.78654; 
PatternMatchingNullable(d);  
PatternMatchingSwitch(i);  
PatternMatchingSwitch(j);  
PatternMatchingSwitch(d);  
static void PatternMatchingNullable (ValueType? val ) 
{ The preceding sample demonstrates other features of pattern matching to use with
conversions. Y ou can test a variable for the null pattern by checking specifically for the
null value. When the runtime value of the variable is null, an is statement checking
for a type always returns false. The pattern matching is statement doesn't allow a
nullable value type, such as int? or Nullable<int>, but you can test for any other value
type. The is patterns from the preceding example aren't limited to the nullable value
types. Y ou can also use those patterns to test if a variable of a reference type has a value
or it's null.    if (val is int j) // Nullable types are not allowed in patterns  
    { 
        Console.WriteLine(j);  
    } 
    else if (val is null) // If val is a nullable type with no value, this  
expression is true  
    { 
        Console.WriteLine( "val is a nullable type with the null value" ); 
    } 
    else 
    { 
        Console.WriteLine( "Could not convert "  + val.ToString());  
    } 
} 
static void PatternMatchingSwitch (ValueType? val ) 
{ 
    switch (val) 
    { 
        case int number:  
            Console.WriteLine(number);  
            break; 
        case long number:  
            Console.WriteLine(number);  
            break; 
        case decimal number:  
            Console.WriteLine(number);  
            break; 
        case float number:  
            Console.WriteLine(number);  
            break; 
        case double number:  
            Console.WriteLine(number);  
            break; 
        case null: 
            Console.WriteLine( "val is a nullable type with the null value" ); 
            break; 
        default: 
            Console.WriteLine( "Could not convert "  + val.ToString());  
            break; 
    } 
} The preceding sample also shows how you use the type pattern in a switch statement
where the variable may be one of many different types.
If you want to test if a variable is a given type, but not assign it to a new variable, you
can use the is and as operators for reference types and nullable value types. The
following code shows how to use the is and as statements that were part of the C#
language before pattern matching was introduced to test if a variable is of a given type:
C#
// Use the is operator to verify the type.  
// before performing a cast.  
Giraffe g = new(); 
UseIsOperator(g);  
// Use the as operator and test for null  
// before referencing the variable.  
UseAsOperator(g);  
// Use pattern matching to test for null  
// before referencing the variable  
UsePatternMatchingIs(g);  
// Use the as operator to test  
// an incompatible type.  
SuperNova sn = new(); 
UseAsOperator(sn);  
// Use the as operator with a value type.  
// Note the implicit conversion to int? in  
// the method body.  
int i = 5; 
UseAsWithNullable(i);  
double d = 9.78654; 
UseAsWithNullable(d);  
static void UseIsOperator (Animal a ) 
{ 
    if (a is Mammal)  
    { 
        Mammal m = (Mammal)a;  
        m.Eat();  
    } 
} 
static void UsePatternMatchingIs (Animal a ) 
{ 
    if (a is Mammal m)  
    { 
        m.Eat();  
    } As you can see by comparing this code with the pattern matching code, the pattern
matching syntax provides more robust features by combining the test and the
assignment in a single statement. Use the pattern matching syntax whenever possible.} 
static void UseAsOperator (object o) 
{ 
    Mammal? m = o as Mammal;  
    if (m is not null) 
    { 
        Console.WriteLine(m.ToString());  
    } 
    else 
    { 
        Console.WriteLine( $"{o.GetType().Name}  is not a Mammal" ); 
    } 
} 
static void UseAsWithNullable (System.ValueType val ) 
{ 
    int? j = val as int?; 
    if (j is not null) 
    { 
        Console.WriteLine(j);  
    } 
    else 
    { 
        Console.WriteLine( "Could not convert "  + val.ToString());  
    } 
} 
class Animal 
{ 
    public void Eat() => Console.WriteLine( "Eating." ); 
    public override  string ToString () => "I am an animal." ; 
} 
class Mammal : Animal { } 
class Giraffe : Mammal { } 
class SuperNova  { } Tutorial: Use pattern matching to build
type-driven and data-driven algorithms
Article •02/15/2023
You can write functionality that behaves as though you extended types that may be in
other libraries. Another use for patterns is to create functionality your application
requires that isn't a fundamental feature of the type being extended.
In this tutorial, you'll learn how to:
We recommend Visual S tudio  for Windows or Mac. Y ou can download a free
version from the Visual S tudio downloads page . Visual S tudio includes the .NET
SDK.
You can also use the Visual S tudio Code  editor. Y ou'll need to install the latest
.NET SDK  separately.
If you prefer a different editor, you need to install the latest .NET SDK .
This tutorial assumes you're familiar with C# and .NET, including either Visual S tudio or
the .NET CLI.
Modern development often includes integrating data from multiple sources and
presenting information and insights from that data in a single cohesive application. Y ou
and your team won't have control or access for all the types that represent the incoming
data.
The classic object-oriented design would call for creating types in your application that
represent each data type from those multiple data sources. Then, your application
would work with those new types, build inheritance hierarchies, create virtual methods,
and implement abstractions. Those techniques work, and sometimes they're the best
tools. Other times you can write less code. Y ou can write more clear code using
techniques that separate the data from the operations that manipulate that data.Recognize situations where pattern matching should be used.＂
Use pattern matching expressions to implement behavior based on types and
property values.＂
Combine pattern matching with other techniques to create complete algorithms.＂
Prerequisites
Scenarios for pattern matchingIn this tutorial, you'll create and explore an application that takes incoming data from
several external sources for a single scenario. Y ou'll see how pattern mat ching  provides
an efficient way to consume and process that data in ways that weren't part of the
original system.
Consider a major metropolitan area that is using tolls and peak time pricing to manage
traffic. Y ou write an application that calculates tolls for a vehicle based on its type. Later
enhancements incorporate pricing based on the number of occupants in the vehicle.
Further enhancements add pricing based on the time and the day of the week.
From that brief description, you may have quickly sketched out an object hierarchy to
model this system. However, your data is coming from multiple sources like other
vehicle registration management systems. These systems provide different classes to
model that data and you don't have a single object model you can use. In this tutorial,
you'll use these simplified classes to model for the vehicle data from these external
systems, as shown in the following code:
C#
namespace  ConsumerVehicleRegistration
{
    public class Car
    {
        public int Passengers { get; set; }
    }
}
namespace  CommercialRegistration
{
    public class DeliveryTruck
    {
        public int GrossWeightClass { get; set; }
    }
}
namespace  LiveryRegistration
{
    public class Taxi
    {
        public int Fares { get; set; }
    }
    public class Bus
    {
        public int Capacity { get; set; }
        public int Riders { get; set; }
    }
}You can download the starter code from the dotnet/samples  GitHub repository. Y ou
can see that the vehicle classes are from different systems, and are in different
namespaces. No common base class, other than System.Object can be used.
The scenario used in this tutorial highlights the kinds of problems that pattern matching
is well suited to solve:
The objects you need to work with aren't in an object hierarchy that matches your
goals. Y ou may be working with classes that are part of unrelated systems.
The functionality you're adding isn't part of the core abstraction for these classes.
The toll paid by a vehicle changes  for different types of vehicles, but the toll isn't a
core function of the vehicle.
When the shape  of the data and the operations  on that data aren't described together,
the pattern matching features in C# make it easier to work with.
The most basic toll calculation relies only on the vehicle type:
A Car is $2.00.
A Taxi is $3.50.
A Bus is $5.00.
A DeliveryTruck is $10.00
Create a new TollCalculator class, and implement pattern matching on the vehicle type
to get the toll amount. The following code shows the initial implementation of the
TollCalculator.
C#
Pattern matching designs
Implement the basic toll calculations
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;
namespace  Calculators ;
public class TollCalculator
{
    public decimal CalculateToll (object vehicle ) =>
        vehicle switchThe preceding code uses a switch  expression  (not the same as a switch  statement ) that
tests the declaration pattern . A switch expr ession  begins with the variable, vehicle in
the preceding code, followed by the switch keyword. Next comes all the switch arms
inside curly braces. The switch expression makes other refinements to the syntax that
surrounds the switch statement. The case keyword is omitted, and the result of each
arm is an expression. The last two arms show a new language feature. The { } case
matches any non-null object that didn't match an earlier arm. This arm catches any
incorrect types passed to this method. The { } case must follow the cases for each
vehicle type. If the order were reversed, the { } case would take precedence. Finally, the
null constant pattern  detects when null is passed to this method. The null pattern
can be last because the other patterns match only a non-null object of the correct type.
You can test this code using the following code in Program.cs:
C#    {
        Car c           => 2.00m,
        Taxi t          => 3.50m,
        Bus b           => 5.00m,
        DeliveryTruck t => 10.00m,
        { }             => throw new ArgumentException(message: "Not a known  
vehicle type" , paramName: nameof(vehicle)),
        null            => throw new ArgumentNullException( nameof(vehicle))
    };
}
using System;
using CommercialRegistration;
using ConsumerVehicleRegistration;
using LiveryRegistration;
using toll_calculator;
var tollCalc = new TollCalculator();
var car = new Car();
var taxi = new Taxi();
var bus = new Bus();
var truck = new DeliveryTruck();
Console.WriteLine( $"The toll for a car is {tollCalc.CalculateToll(car)} ");
Console.WriteLine( $"The toll for a taxi is {tollCalc.CalculateToll(taxi)} ");
Console.WriteLine( $"The toll for a bus is {tollCalc.CalculateToll(bus)} ");
Console.WriteLine( $"The toll for a truck is 
{tollCalc.CalculateToll(truck)} ");
try
{That code is included in the starter project, but is commented out. R emove the
comments, and you can test what you've written.
You're starting to see how patterns can help you create algorithms where the code and
the data are separate. The switch expression tests the type and produces different
values based on the results. That's only the beginning.
The toll authority wants to encourage vehicles to travel at maximum capacity. They've
decided to charge more when vehicles have fewer passengers, and encourage full
vehicles by offering lower pricing:
Cars and taxis with no passengers pay an extra $0.50.
Cars and taxis with two passengers get a $0.50 discount.
Cars and taxis with three or more passengers get a $1.00 discount.
Buses that are less than 50% full pay an extra $2.00.
Buses that are more than 90% full get a $1.00 discount.
These rules can be implemented using a property pattern  in the same switch expression.
A property pattern compares a property value to a constant value. The property pattern
examines properties of the object once the type has been determined. The single case
for a Car expands to four different cases:
C#    tollCalc.CalculateToll( "this will fail" );
}
catch (ArgumentException e)
{
    Console.WriteLine( "Caught an argument exception when using the wrong  
type");
}
try
{
    tollCalc.CalculateToll( null!);
}
catch (ArgumentNullException e)
{
    Console.WriteLine( "Caught an argument exception when using null" );
}
Add occupancy pricing
vehicle switch
{
    Car {Passengers: 0} => 2.00m + 0.50m,
    Car {Passengers: 1} => 2.0m,The first three cases test the type as a Car, then check the value of the Passengers
property. If both match, that expression is evaluated and returned.
You would also expand the cases for taxis in a similar manner:
C#
Next, implement the occupancy rules by expanding the cases for buses, as shown in the
following example:
C#
The toll authority isn't concerned with the number of passengers in the delivery trucks.
Instead, they adjust the toll amount based on the weight class of the trucks as follows:
Trucks over 5000 lbs are charged an extra $5.00.
Light trucks under 3000 lbs are given a $2.00 discount.    Car {Passengers: 2} => 2.0m - 0.50m,
    Car                 => 2.00m - 1.0m,
    // ...
};
vehicle switch
{
    // ...
    Taxi {Fares: 0}  => 3.50m + 1.00m,
    Taxi {Fares: 1}  => 3.50m,
    Taxi {Fares: 2}  => 3.50m - 0.50m,
    Taxi             => 3.50m - 1.00m,
    // ...
};
vehicle switch
{
    // ...
    Bus b when ((double)b.Riders / ( double)b.Capacity) < 0.50  => 5.00m + 
2.00m,
    Bus b when ((double)b.Riders / ( double)b.Capacity) > 0.90  => 5.00m - 
1.00m,
    Bus => 5.00m,
    // ...
};That rule is implemented with the following code:
C#
The preceding code shows the when clause of a switch arm. Y ou use the when clause to
test conditions other than equality on a property. When you've finished, you'll have a
method that looks much like the following code:
C#
Many of these switch arms are examples of recursive patterns. For example, Car {
Passengers: 1} shows a constant pattern inside a property pattern.vehicle switch
{
    // ...
    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck => 10.00m,
};
vehicle switch
{
    Car {Passengers: 0}        => 2.00m + 0.50m,
    Car {Passengers: 1}        => 2.0m,
    Car {Passengers: 2}        => 2.0m - 0.50m,
    Car                        => 2.00m - 1.0m,
    Taxi {Fares: 0}  => 3.50m + 1.00m,
    Taxi {Fares: 1}  => 3.50m,
    Taxi {Fares: 2}  => 3.50m - 0.50m,
    Taxi             => 3.50m - 1.00m,
    Bus b when ((double)b.Riders / ( double)b.Capacity) < 0.50  => 5.00m + 
2.00m,
    Bus b when ((double)b.Riders / ( double)b.Capacity) > 0.90  => 5.00m - 
1.00m,
    Bus => 5.00m,
    DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
    DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
    DeliveryTruck => 10.00m,
    { }     => throw new ArgumentException(message: "Not a known vehicle  
type", paramName: nameof(vehicle)),
    null    => throw new ArgumentNullException( nameof(vehicle))
};You can make this code less repetitive by using nested switches. The Car and Taxi both
have four different arms in the preceding examples. In both cases, you can create a
declaration pattern that feeds into a constant pattern. This technique is shown in the
following code:
C#
In the preceding sample, using a recursive expression means you don't repeat the Car
and Taxi arms containing child arms that test the property value. This technique isn't
used for the Bus and DeliveryTruck arms because those arms are testing ranges for the
property, not discrete values.public decimal CalculateToll (object vehicle ) =>
    vehicle switch
    {
        Car c => c.Passengers switch
        {
            0 => 2.00m + 0.5m,
            1 => 2.0m,
            2 => 2.0m - 0.5m,
            _ => 2.00m - 1.0m
        },
        Taxi t => t.Fares switch
        {
            0 => 3.50m + 1.00m,
            1 => 3.50m,
            2 => 3.50m - 0.50m,
            _ => 3.50m - 1.00m
        },
        Bus b when ((double)b.Riders / ( double)b.Capacity) < 0.50  => 5.00m + 
2.00m,
        Bus b when ((double)b.Riders / ( double)b.Capacity) > 0.90  => 5.00m - 
1.00m,
        Bus b => 5.00m,
        DeliveryTruck t when (t.GrossWeightClass > 5000) => 10.00m + 5.00m,
        DeliveryTruck t when (t.GrossWeightClass < 3000) => 10.00m - 2.00m,
        DeliveryTruck t => 10.00m,
        { }  => throw new ArgumentException(message: "Not a known vehicle  
type", paramName: nameof(vehicle)),
        null => throw new ArgumentNullException( nameof(vehicle))
    };
Add peak pricingFor the final feature, the toll authority wants to add time sensitive peak pricing. During
the morning and evening rush hours, the tolls are doubled. That rule only affects traffic
in one direction: inbound to the city in the morning, and outbound in the evening rush
hour. During other times during the workday, tolls increase by 50%. Late night and early
morning, tolls are reduced by 25%. During the weekend, it's the normal rate, regardless
of the time. Y ou could use a series of if and else statements to express this using the
following code:
C#
public decimal PeakTimePremiumIfElse (DateTime timeOfToll, bool inbound )
{
    if ((timeOfToll.DayOfWeek == DayOfWeek.Saturday) ||
        (timeOfToll.DayOfWeek == DayOfWeek.Sunday))
    {
        return 1.0m;
    }
    else
    {
        int hour = timeOfToll.Hour;
        if (hour < 6)
        {
            return 0.75m;
        }
        else if (hour < 10)
        {
            if (inbound)
            {
                return 2.0m;
            }
            else
            {
                return 1.0m;
            }
        }
        else if (hour < 16)
        {
            return 1.5m;
        }
        else if (hour < 20)
        {
            if (inbound)
            {
                return 1.0m;
            }
            else
            {
                return 2.0m;
            }
        }
        else // Overnight
        {The preceding code does work correctly, but isn't readable. Y ou have to chain through
all the input cases and the nested if statements to reason about the code. Instead,
you'll use pattern matching for this feature, but you'll integrate it with other techniques.
You could build a single pattern match expression that would account for all the
combinations of direction, day of the week, and time. The result would be a complicated
expression. It would be hard to read and difficult to understand. That makes it hard to
ensure correctness. Instead, combine those methods to build a tuple of values that
concisely describes all those states. Then use pattern matching to calculate a multiplier
for the toll. The tuple contains three discrete conditions:
The day is either a weekday or a weekend.
The band of time when the toll is collected.
The direction is into the city or out of the city
The following table shows the combinations of input values and the peak pricing
multiplier:
Day Time Direction Premium
Weekday morning rush inbound x 2.00
Weekday morning rush outbound x 1.00
Weekday daytime inbound x 1.50
Weekday daytime outbound x 1.50
Weekday evening rush inbound x 1.00
Weekday evening rush outbound x 2.00
Weekday overnight inbound x 0.75
Weekday overnight outbound x 0.75
Weekend morning rush inbound x 1.00
Weekend morning rush outbound x 1.00
Weekend daytime inbound x 1.00
Weekend daytime outbound x 1.00            return 0.75m;
        }
    }
}Day Time Direction Premium
Weekend evening rush inbound x 1.00
Weekend evening rush outbound x 1.00
Weekend overnight inbound x 1.00
Weekend overnight outbound x 1.00
There are 16 different combinations of the three variables. By combining some of the
conditions, you'll simplify the final switch expression.
The system that collects the tolls uses a DateTime  structure for the time when the toll
was collected. Build member methods that create the variables from the preceding
table. The following function uses a pattern matching switch expression to express
whether a DateTime  represents a weekend or a weekday:
C#
That method is correct, but it's repetitious. Y ou can simplify it, as shown in the following
code:
C#
Next, add a similar function to categorize the time into the blocks:
C#private static bool IsWeekDay (DateTime timeOfToll ) =>
    timeOfToll.DayOfWeek switch
    {
        DayOfWeek.Monday    => true,
        DayOfWeek.Tuesday   => true,
        DayOfWeek.Wednesday => true,
        DayOfWeek.Thursday  => true,
        DayOfWeek.Friday    => true,
        DayOfWeek.Saturday  => false,
        DayOfWeek.Sunday    => false
    };
private static bool IsWeekDay (DateTime timeOfToll ) =>
    timeOfToll.DayOfWeek switch
    {
        DayOfWeek.Saturday => false,
        DayOfWeek.Sunday => false,
        _ => true
    };You add a private enum to convert each range of time to a discrete value. Then, the
GetTimeBand method uses relational patterns , and conjunctive or patterns . A relational
pattern lets you test a numeric value using <, >, <=, or >=. The or pattern tests if an
expression matches one or more patterns. Y ou can also use an and pattern to ensure
that an expression matches two distinct patterns, and a not pattern to test that an
expression doesn't match a pattern.
After you create those methods, you can use another switch expression with the tuple
pattern to calculate the pricing premium. Y ou could build a switch expression with all
16 arms:
C#private enum TimeBand
{
    MorningRush,
    Daytime,
    EveningRush,
    Overnight
}
private static TimeBand GetTimeBand (DateTime timeOfToll ) =>
    timeOfToll.Hour switch
    {
        < 6 or > 19 => TimeBand.Overnight,
        < 10 => TimeBand.MorningRush,
        < 16 => TimeBand.Daytime,
        _ => TimeBand.EveningRush,
    };
public decimal PeakTimePremiumFull (DateTime timeOfToll, bool inbound ) =>
    (IsWeekDay(timeOfToll), GetTimeBand(timeOfToll), inbound) switch
    {
        (true, TimeBand.MorningRush, true) => 2.00m,
        (true, TimeBand.MorningRush, false) => 1.00m,
        (true, TimeBand.Daytime, true) => 1.50m,
        (true, TimeBand.Daytime, false) => 1.50m,
        (true, TimeBand.EveningRush, true) => 1.00m,
        (true, TimeBand.EveningRush, false) => 2.00m,
        (true, TimeBand.Overnight, true) => 0.75m,
        (true, TimeBand.Overnight, false) => 0.75m,
        (false, TimeBand.MorningRush, true) => 1.00m,
        (false, TimeBand.MorningRush, false) => 1.00m,
        (false, TimeBand.Daytime, true) => 1.00m,
        (false, TimeBand.Daytime, false) => 1.00m,
        (false, TimeBand.EveningRush, true) => 1.00m,
        (false, TimeBand.EveningRush, false) => 1.00m,
        (false, TimeBand.Overnight, true) => 1.00m,The above code works, but it can be simplified. All eight combinations for the weekend
have the same toll. Y ou can replace all eight with the following line:
C#
Both inbound and outbound traffic have the same multiplier during the weekday
daytime and overnight hours. Those four switch arms can be replaced with the following
two lines:
C#
The code should look like the following code after those two changes:
C#
Finally, you can remove the two rush hour times that pay the regular price. Once you
remove those arms, you can replace the false with a discard ( _) in the final switch arm.
You'll have the following finished method:
C#        (false, TimeBand.Overnight, false) => 1.00m,
    };
(false, _, _) => 1.0m,
(true, TimeBand.Overnight, _) => 0.75m,
(true, TimeBand.Daytime, _)   => 1.5m,
public decimal PeakTimePremium (DateTime timeOfToll, bool inbound ) =>
    (IsWeekDay(timeOfToll), GetTimeBand(timeOfToll), inbound) switch
    {
        (true, TimeBand.MorningRush, true)  => 2.00m,
        (true, TimeBand.MorningRush, false) => 1.00m,
        (true, TimeBand.Daytime,     _)     => 1.50m,
        (true, TimeBand.EveningRush, true)  => 1.00m,
        (true, TimeBand.EveningRush, false) => 2.00m,
        (true, TimeBand.Overnight,   _)     => 0.75m,
        (false, _,                   _)     => 1.00m,
    };
public decimal PeakTimePremium (DateTime timeOfToll, bool inbound ) =>
    (IsWeekDay(timeOfToll), GetTimeBand(timeOfToll), inbound) switch
    {
        (true, TimeBand.Overnight, _) => 0.75m,
        (true, TimeBand.Daytime, _) => 1.5m,
        (true, TimeBand.MorningRush, true) => 2.0m,This example highlights one of the advantages of pattern matching: the pattern
branches are evaluated in order. If you rearrange them so that an earlier branch handles
one of your later cases, the compiler warns you about the unreachable code. Those
language rules made it easier to do the preceding simplifications with confidence that
the code didn't change.
Pattern matching makes some types of code more readable and offers an alternative to
object-oriented techniques when you can't add code to your classes. The cloud is
causing data and functionality to live apart. The shape  of the data and the operations  on
it aren't necessarily described together. In this tutorial, you consumed existing data in
entirely different ways from its original function. P attern matching gave you the ability
to write functionality that overrode those types, even though you couldn't extend them.
You can download the finished code from the dotnet/samples  GitHub repository.
Explore patterns on your own and add this technique into your regular coding activities.
Learning these techniques gives you another way to approach problems and create new
functionality.
Patterns
switch  expression        (true, TimeBand.EveningRush, false) => 2.0m,
        _ => 1.0m,
    };
Next steps
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
 Provide product feedbackHow to handle an exception using
try/catch
Article •04/22/2023
The purpose of a try-catch  block is to catch and handle an exception generated by
working code. Some exceptions can be handled in a catch block and the problem
solved without the exception being rethrown; however, more often the only thing that
you can do is make sure that the appropriate exception is thrown.
In this example, IndexOutOfRangeException  isn't the most appropriate exception:
ArgumentOutOfRangeException  makes more sense for the method because the error is
caused by the index argument passed in by the caller.
C#
The code that causes an exception is enclosed in the try block. A catch statement is
added immediately after it to handle IndexOutOfRangeException, if it occurs. The catch
block handles the IndexOutOfRangeException and throws the more appropriate
ArgumentOutOfRangeException instead. In order to provide the caller with as much
information as possible, consider specifying the original exception as the InnerExceptionExample
static int GetInt(int[] array, int index) 
{ 
    try 
    { 
        return array[index];  
    } 
    catch (IndexOutOfRangeException e)  // CS0168  
    { 
        Console.WriteLine(e.Message);  
        // Set IndexOutOfRangeException to the new exception's  
InnerException.  
        throw new ArgumentOutOfRangeException( "index parameter is out of  
range.", e); 
    } 
} 
Commentsof the new exception. Because the InnerException  property is read-only , you must assign
it in the constructor of the new exception.How to execute cleanup code using
finally
Article •04/22/2023
The purpose of a finally statement is to ensure that the necessary cleanup of objects,
usually objects that are holding external resources, occurs immediately, even if an
exception is thrown. One example of such cleanup is calling Close  on a FileStream
immediately after use instead of waiting for the object to be garbage collected by the
common language runtime, as follows:
C#
To turn the previous code into a try-catch-finally statement, the cleanup code is
separated from the working code, as follows.
C#static void CodeWithoutCleanup () 
{ 
    FileStream? file = null; 
    FileInfo fileInfo = new FileInfo( "./file.txt" ); 
    file = fileInfo.OpenWrite();  
    file.WriteByte( 0xF); 
    file.Close();  
} 
Example
static void CodeWithCleanup () 
{ 
    FileStream? file = null; 
    FileInfo? fileInfo = null; 
    try 
    { 
        fileInfo = new FileInfo( "./file.txt" ); 
        file = fileInfo.OpenWrite();  
        file.WriteByte( 0xF); 
    } 
    catch (UnauthorizedAccessException e)  
    { 
        Console.WriteLine(e.Message);  Because an exception can occur at any time within the try block before the
OpenWrite() call, or the OpenWrite() call itself could fail, we aren't guaranteed that the
file is open when we try to close it. The finally block adds a check to make sure that
the FileStream  object isn't null before you call the Close  method. Without the null
check, the finally block could throw its own NullR eferenceException , but throwing
exceptions in finally blocks should be avoided if it's possible.
A database connection is another good candidate for being closed in a finally block.
Because the number of connections allowed to a database server is sometimes limited,
you should close database connections as quickly as possible. If an exception is thrown
before you can close your connection, using the finally block is better than waiting for
garbage collection.
using statement
Exception-handling statements    } 
    finally 
    { 
        file?.Close();  
    } 
} 
See alsoWhat's new in C# 12
Article •11/14/2023
C# 12 includes the following new features. Y ou can try these features using the latest
Visual S tudio 2022  version or the .NET 8 SDK .
Primary constructors  - Introduced in Visual S tudio 2022 version 17.6 Preview 2.
Collection expressions  - Introduced in Visual S tudio 2022 version 17.7 Preview 5.
Inline arrays  - Introduced in Visual S tudio 2022 version 17.7 Preview 3.
Optional parameters in lambda expressions  - Introduced in Visual S tudio 2022
version 17.5 Preview 2.
ref readonly  parameters  - Introduced in Visual S tudio 2022 version 17.8 Preview 2.
Alias any type  - Introduced in Visual S tudio 2022 version 17.6 Preview 3.
Experimental attribute  - Introduced in Visual S tudio 2022 version 17.7 Preview 3.
Interceptors  - Preview featur e Introduced in Visual S tudio 2022 version 17.7
Preview 3.
You can now create primary constructors in any class and struct. Primary constructors
are no longer restricted to record types. Primary constructor parameters are in scope
for the entire body of the class. T o ensure that all primary constructor parameters are
definitely assigned, all explicitly declared constructors must call the primary constructor
using this() syntax. Adding a primary constructor to a class prevents the compiler
from declaring an implicit parameterless constructor. In a struct, the implicit
parameterless constructor initializes all fields, including primary constructor parameters
to the 0-bit pattern.
The compiler generates public properties for primary constructor parameters only in
record types, either record class or record struct types. Nonrecord classes and
structs might not always want this behavior for primary constructor parameters.
You can learn more about primary constructors in the tutorial for exploring primary
constructors  and in the article on instance constructors .
Primary constructorsCollection expressions introduce a new terse syntax to create common collection values.
Inlining other collections into these values is possible using a spread operator ...
Several collection-like types can be created without requiring external BCL support.
These types are:
Array types, such as int[].
System.Span<T>  and System.R eadOnlySpan<T> .
Types that support collection initializers, such as
System.Collections.Generic.List<T> .
The following examples show uses of collection expressions:
C#
The spread oper ator, .. in a collection expression replaces its argument with the
elements from that collection. The argument must be a collection type. The following
examples show how the spread operator works:
C#Collection expressions
// Create an array:
int[] a = [ 1, 2, 3, 4, 5, 6, 7, 8];
// Create a list:
List<string> b = ["one", "two", "three"];
// Create a span
Span<char> c  = [ 'a', 'b', 'c', 'd', 'e', 'f', 'h', 'i'];
// Create a jagged 2D array:
int[][] twoD = [[ 1, 2, 3], [4, 5, 6], [7, 8, 9]];
// Create a jagged 2D array from variables:
int[] row0 = [ 1, 2, 3];
int[] row1 = [ 4, 5, 6];
int[] row2 = [ 7, 8, 9];
int[][] twoDFromVariables = [row0, row1, row2];
int[] row0 = [ 1, 2, 3];
int[] row1 = [ 4, 5, 6];
int[] row2 = [ 7, 8, 9];
int[] single = [..row0, ..row1, ..row2];
foreach (var element in single)
{
    Console.Write( $"{element} , ");The operand of a spread operator is an expression that can be enumerated. The spread
operator evaluates each element of the enumerations expression.
You can use collection expressions anywhere you need a collection of elements. They
can specify the initial value for a collection or be passed as arguments to methods that
take collection types. Y ou can learn more about collection expressions in the language
reference article on collection expressions  or the feature specification .
C# added in parameters as a way to pass readonly references. in parameters allow
both variables and values, and can be used without any annotation on arguments.
The addition of ref readonly parameters enables more clarity for APIs that might be
using ref parameters or in parameters:
APIs created before in was introduced might use ref even though the argument
isn't modified. Those APIs can be updated with ref readonly. It won't be a
breaking change for callers, as would be if the ref parameter was changed to in.
An example is System.Runtime.InteropServices.Marshal.QueryInterface .
APIs that take an in parameter, but logically require a variable. A value expression
doesn't work. An example is System.R eadOnlySpan<T>.R eadOnlySpan<T>(T) .
APIs that use ref because they require a variable, but don't mutate that variable.
An example is System.Runtime.CompilerServices.Unsafe.IsNullR ef.
To learn more about ref readonly parameters, see the article on parameter modifiers  in
the language reference, or the ref readonly parameters  feature specification.
You can now define default values for parameters on lambda expressions. The syntax
and rules are the same as adding default values for arguments to any method or local
function.
You can learn more about default parameters on lambda expressions in the article on
lambda expressions .}
// output:
// 1, 2, 3, 4, 5, 6, 7, 8, 9,
ref readonly parameters
Default lambda parametersYou can use the using alias directive to alias any type, not just named types. That means
you can create semantic aliases for tuple types, array types, pointer types, or other
unsafe types. For more information, see the feature specification .
Inline arrays are used by the runtime team and other library authors to improve
performance in your apps. Inline arrays enable a developer to create an array of fixed
size in a struct type. A struct with an inline buffer should provide performance
characteristics similar to an unsafe fixed size buffer. Y ou likely won't declare your own
inline arrays, but you use them transparently when they're exposed as System.Span<T>
or System.R eadOnlySpan<T>  objects from runtime APIs.
An inline arr ay is declared similar to the following struct:
C#
You use them like any other array:
C#
The difference is that the compiler can take advantage of known information about an
inline array. Y ou likely consume inline arrays as you would any other array. For more
information on how to declare inline arrays, see the language reference on struct  types .Alias any type
Inline  arrays
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct Buffer
{
    private int _element0;
}
var buffer = new Buffer();
for (int i = 0; i < 10; i++)
{
    buffer[i] = i;
}
foreach (var i in buffer)
{
    Console.WriteLine(i);
}Types, methods, or assemblies can be marked with the
System.Diagnostics.CodeAnalysis.ExperimentalAttribute  to indicate an experimental
feature. The compiler issues a warning if you access a method or type annotated with
the ExperimentalAttribute . All types included in an assembly marked with the
Experimental attribute are experimental. Y ou can read more in the article on General
attributes read by the compiler , or the feature specification .
An interceptor is a method that can declaratively substitute a call to an interceptable
method with a call to itself at compile time. This substitution occurs by having the
interceptor declare the source locations of the calls that it intercepts. Interceptors
provide a limited facility to change the semantics of existing code by adding new code
to a compilation, for example in a source generator.
You use an interceptor as part of a source generator to modify, rather than add code to
an existing source compilation. The source generator substitutes calls to an
interceptable method with a call to the interceptor method.
If you're interested in experimenting with interceptors, you can learn more by reading
the feature specification . If you use the feature, make sure to stay current with any
changes in the feature specification for this experimental feature. If the feature is
finalized, we'll add more guidance on this site.Experimental attribute
Interceptors
２ Warning
Interceptors are an experimental feature, available in preview mode with C# 12. The
feature may be subject to breaking changes or removal in a future release.
Therefore, it is not recommended for production or released applications.
In order to use interceptors, the user project must specify the property
<InterceptorsPreviewNamespaces>. This is a list of namespaces which are allowed to
contain interceptors.
For example:
<InterceptorsPreviewNamespaces>$(InterceptorsPreviewNamespaces);Microsoft.AspN
etCore.Http.Generated;MyLibrary.Generated</InterceptorsPreviewNamespaces>
What's new in .NET 8See also
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
 Provide product feedbackWhat's new in C# 11
Article •03/15/2023
The following features were added in C# 11:
Raw string literals
Generic math support
Generic attributes
UTF-8 string literals
Newlines in string interpolation expressions
List patterns
File-local types
Required members
Auto-default structs
Pattern match Span<char>  on a constant string
Extended nameof  scope
Numeric IntPtr
ref fields and scoped ref
Improved method group conversion to delegate
Warning wave 7
C# 11 is supported on .NET 7. For more information, see C# language versioning .
You can download the latest .NET 7 SDK from the .NET downloads page . You can also
download Visual S tudio 2022 , which includes the .NET 7 SDK.
You can declare a generic class  whose base class is System.Attribute . This feature
provides a more convenient syntax for attributes that require a System.T ype parameter.
Previously, you'd need to create an attribute that takes a Type as its constructor
parameter:
C#
７ Note
We're interested in your feedback on these features. If you find issues with any of
these new features, create a new issue  in the dotnet/r oslyn  repository.
Generic attributesAnd to apply the attribute, you use the typeof  operator:
C#
Using this new feature, you can create a generic attribute instead:
C#
Then, specify the type parameter to use the attribute:
C#
You must supply all type parameters when you apply the attribute. In other words, the
generic type must be fully constructed . In the example above, the empty parentheses ( (
and )) can be omitted as the attribute does not have any arguments.
C#
The type arguments must satisfy the same restrictions as the typeof  operator. T ypes that
require metadata annotations aren't allowed. For example, the following types aren't
allowed as the type parameter:// Before C# 11:
public class TypeAttribute  : Attribute
{
   public TypeAttribute (Type t) => ParamType = t;
   public Type ParamType { get; }
}
[TypeAttribute(typeof(string)) ]
public string Method() => default;
// C# 11 feature:
public class GenericAttribute <T> : Attribute  { }
[GenericAttribute<string>() ]
public string Method() => default;
public class GenericType <T>
{
   [GenericAttribute<T>() ] // Not allowed! generic attributes must be fully  
constructed types.
   public string Method() => default;
}dynamic
string? (or any nullable reference type)
(int X, int Y) (or any other tuple types using C# tuple syntax).
These types aren't directly represented in metadata. They include annotations that
describe the type. In all cases, you can use the underlying type instead:
object for dynamic.
string instead of string?.
ValueTuple<int, int> instead of (int X, int Y).
There are several language features that enable generic math support:
static virtual members in interfaces
checked user defined operators
relaxed shift operators
unsigned right-shift operator
You can add static abstract or static virtual members in interfaces to define
interfaces that include overloadable operators, other static members, and static
properties. The primary scenario for this feature is to use mathematical operators in
generic types. For example, you can implement the System.IAdditionOperators<TSelf,
TOther, TResult> interface in a type that implements operator +. Other interfaces
define other mathematical operations or well-defined values. Y ou can learn about the
new syntax in the article on interfaces . Interfaces that include static virtual methods
are typically generic interfaces . Furthermore, most will declare a constraint that the type
parameter implements the declared interface .
You can learn more and try the feature yourself in the tutorial Explore static abstract
interface members , or the Preview features in .NET 6 – generic math  blog post.
Generic math created other requirements on the language.
unsigned r ight shi ft oper ator: Before C# 11, to force an unsigned right-shift, you
would need to cast any signed integer type to an unsigned type, perform the shift,
then cast the result back to a signed type. Beginning in C# 11, you can use the
>>>, the unsigned shi ft oper ator.
relaxed shi ft oper ator requir ements : C# 11 removes the requirement that the
second operand must be an int or implicitly convertible to int. This change
allows types that implement generic math interfaces to be used in these locations.Generic math support
check ed and uncheck ed us er def ined oper ators: Developers can now define checked
and unchecked arithmetic operators. The compiler generates calls to the correct
variant based on the current context. Y ou can read more about checked operators
in the article on Arithmetic operators .
The nint and nuint types now alias System.IntPtr  and System.UIntPtr , respectively.
The text inside the { and } characters for a string interpolation can now span multiple
lines. The text between the { and } markers is parsed as C#. Any legal C#, including
newlines, is allowed. This feature makes it easier to read string interpolations that use
longer C# expressions, like pattern matching switch expressions, or LINQ queries.
You can learn more about the newlines feature in the string interpolations  article in the
language reference.
List p atterns extend pattern matching to match sequences of elements in a list or an
array. For example, sequence is [1, 2, 3] is true when the sequence is an array or a
list of three integers (1, 2, and 3). Y ou can match elements using any pattern, including
constant, type, property and relational patterns. The discard pattern ( _) matches any
single element, and the new range p attern (..) matches any sequence of zero or more
elements.
You can learn more details about list patterns in the pattern matching  article in the
language reference.
The C# standard on Method group conversions  now includes the following item:
The conversion is permitted (but not required) to use an existing delegate
instance that already contains these references.Numeric IntPtr and UIntPtr
Newlines in string interpolations
List patterns
Improved method group conversion to
delegatePrevious versions of the standard prohibited the compiler from reusing the delegate
object created for a method group conversion. The C# 11 compiler caches the delegate
object created from a method group conversion and reuses that single delegate object.
This feature was first available in Visual S tudio 2022 version 17.2 as a preview feature,
and in .NET 7 Preview 2.
Raw str ing lit erals are a new format for string literals. Raw string literals can contain
arbitrary text, including whitespace, new lines, embedded quotes, and other special
characters without requiring escape sequences. A raw string literal starts with at least
three double-quote (""") characters. It ends with the same number of double-quote
characters. T ypically, a raw string literal uses three double quotes on a single line to start
the string, and three double quotes on a separate line to end the string. The newlines
following the opening quote and preceding the closing quote aren't included in the final
content:
C#
Any whitespace to the left of the closing double quotes will be removed from the string
literal. Raw string literals can be combined with string interpolation to include braces in
the output text. Multiple $ characters denote how many consecutive braces start and
end the interpolation:
C#
The preceding example specifies that two braces start and end an interpolation. The
third repeated opening and closing brace are included in the output string.
You can learn more about raw string literals in the article on strings in the programming
guide , and the language reference articles on string literals  and interpolated strings .Raw string literals
string longMessage = """
    This is a long message.
    It has several lines.
        Some are indented
                more than others.
    Some should start at the first column.
    Some have " quoted text " in them.
    """;
var location = $ $"""
   You are at {{{Longitude}}, {{Latitude}}}
   """;The C# 11 compiler ensures that all fields of a struct type are initialized to their default
value as part of executing a constructor. This change means any field or auto property
not initialized by a constructor is automatically initialized by the compiler. S tructs where
the constructor doesn't definitely assign all fields now compile, and any fields not
explicitly initialized are set to their default value. Y ou can read more about how this
change affects struct initialization in the article on structs .
You've been able to test if a string had a specific constant value using pattern
matching for several releases. Now, you can use the same pattern matching logic with
variables that are Span<char> or ReadOnlySpan<char>.
Type parameter names and parameter names are now in scope when used in a nameof
expression in an attribute declaration  on that method. This feature means you can use
the nameof operator to specify the name of a method parameter in an attribute on the
method or parameter declaration. This feature is most often useful to add attributes for
nullable analysis .
You can specify the u8 suffix on a string literal to specify UTF-8 character encoding. If
your application needs UTF-8 strings, for HT TP string constants or similar text protocols,
you can use this feature to simplify the creation of UTF-8 strings.
You can learn more about UTF-8 string literals in the string literal section of the article
on builtin reference types .
You can add the required  modifier  to properties and fields to enforce constructors and
callers to initialize those values. TheAuto-default struct
Pattern match Span<char> or
ReadOnlySpan<char> on a constant string
Extended nameof scope
UTF-8 string literals
Required membersSystem.Diagnostics.CodeAnalysis.SetsR equiredMembersAttribute  can be added to
constructors to inform the compiler that a constructor initializes all required members.
For more information on required members, See the init-only  section of the properties
article.
You can declare ref fields inside a ref struct . This supports types such as
System.Span<T>  without special attributes or hidden internal types.
You can add the scoped  modifier to any ref declaration. This limits the scope  where the
reference can escape to.
Beginning in C# 11, you can use the file access modifier to create a type whose
visibility is scoped to the source file in which it is declared. This feature helps source
generator authors avoid naming collisions. Y ou can learn more about this feature in the
article on file-scoped types  in the language reference.
What's new in .NET 7ref fields and ref scoped variables
File local types
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
 Provide product feedbackWhat's new in C# 10
Article •02/21/2023
C# 10 adds the following features and enhancements to the C# language:
Record structs
Improvements of structure types
Interpolated string handlers
global using  directives
File-scoped namespace declaration
Extended property patterns
Improvements on lambda expressions
Allow const  interpolated strings
Record types can seal ToString()
Improved definite assignment
Allow both assignment and declaration in the same deconstruction
Allow AsyncMethodBuilder  attribute on methods
CallerArgumentExpression attribute
Enhanced #line  pragma
Warning wave 6
C# 10 is supported on .NET 6. For more information, see C# language versioning .
You can download the latest .NET 6 SDK from the .NET downloads page . You can also
download Visual S tudio 2022 , which includes the .NET 6 SDK.
You can declare value type records using the record struct  or readonly record struct
declarations . You can now clarify that a record is a reference type with the record class
declaration.
７ Note
We're interested in your feedback on these features. If you find issues with any of
these new features, create a new issue  in the dotnet/r oslyn  repository.
Record structs
Improvements of structure typesC# 10 introduces the following improvements related to structure types:
You can declare an instance parameterless constructor in a structure type and
initialize an instance field or property at its declaration. For more information, see
the Struct initialization and default values  section of the Structure types  article.
A left-hand operand of the with expression  can be of any structure type or an
anonymous (reference) type.
You can create a type that builds the resulting string from an interpolated string
expression . The .NET libraries use this feature in many APIs. Y ou can build one by
following this tutorial .
You can add the global modifier to any using directive  to instruct the compiler that the
directive applies to all source files in the compilation. This is typically all source files in a
project.
You can use a new form of the namespace  declaration  to declare that all declarations
that follow are members of the declared namespace:
C#
This new syntax saves both horizontal and vertical space for namespace declarations.
Beginning with C# 10, you can reference nested properties or fields within a property
pattern. For example, a pattern of the form
C#Interpolated string handler
Global using directives
File-scoped namespace declaration
namespace  MyNamespace ; 
Extended property patterns
{ Prop1.Prop2: pattern }  is valid in C# 10 and later and equivalent to
C#
valid in C# 8.0 and later.
For more information, see the Extended property patterns  feature proposal note. For
more information about a property pattern, see the Property pattern  section of the
Patterns  article.
C# 10 includes many improvements to how lambda expressions are handled:
Lambda expressions may have a natural type , where the compiler can infer a
delegate type from the lambda expression or method group.
Lambda expressions may declare a return type  when the compiler can't infer it.
Attributes  can be applied to lambda expressions.
These features make lambda expressions more similar to methods and local functions.
They make it easier to use lambda expressions without declaring a variable of a delegate
type, and they work more seamlessly with the new ASP.NET Core Minimal APIs.
In C# 10, const strings may be initialized using string interpolation  if all the
placeholders are themselves constant strings. S tring interpolation can create more
readable constant strings as you build constant strings used in your application. The
placeholder expressions can't be numeric constants because those constants are
converted to strings at run time. The current culture may affect their string
representation. Learn more in the language reference on const  expressions .
In C# 10, you can add the sealed modifier when you override ToString in a record type.
Sealing the ToString method prevents the compiler from synthesizing a ToString
method for any derived record types. A sealed ToString ensures all derived record
types use the ToString method defined in a common base record type. Y ou can learn
more about this feature in the article on records .{ Prop1: { Prop2: pattern } }  
Lambda expression improvements
Constant interpolated strings
Record types can seal ToStringThis change removes a restriction from earlier versions of C#. Previously, a
deconstruction could assign all values to existing variables, or initialize newly declared
variables:
C#
C# 10 removes this restriction:
C#
Prior to C# 10, there were many scenarios where definite assignment and null-state
analysis produced warnings that were false positives. These generally involved
comparisons to boolean constants, accessing a variable only in the true or false
statements in an if statement, and null coalescing expressions. These examples
generated warnings in previous versions of C#, but don't in C# 10:
C#Assignment and declaration in same
deconstruction
// Initialization:  
(int x, int y) = point;  
// assignment:  
int x1 = 0; 
int y1 = 0; 
(x1, y1) = point;  
int x = 0; 
(x, int y) = point;  
Improved definite assignment
string representation = "N/A"; 
if ((c != null && c.GetDependentValue( out object obj)) == true) 
{ 
   representation = obj.ToString(); // undesired error  
} 
// Or, using ?.  
if (c?.GetDependentValue( out object obj) == true) 
{ 
   representation = obj.ToString(); // undesired error  
} The main impact of this improvement is that the warnings for definite assignment and
null-state analysis are more accurate.
In C# 10 and later, you can specify a different async method builder for a single method,
in addition to specifying the method builder type for all methods that return a given
task-like type. A custom async method builder enables advanced performance tuning
scenarios where a given method may benefit from a custom builder.
To learn more, see the section on AsyncMethodBuilder  in the article on attributes read
by the compiler.
You can use the System.Runtime.CompilerServices.CallerArgumentExpressionAttribute  to
specify a parameter that the compiler replaces with the text representation of another
argument. This feature enables libraries to create more specific diagnostics. The
following code tests a condition. If the condition is false, the exception message
contains the text representation of the argument passed to condition:
C#
You can learn more about this feature in the article on Caller information attributes  in
the language reference section.// Or, using ??  
if (c?.GetDependentValue( out object obj) ?? false) 
{ 
   representation = obj.ToString(); // undesired error  
} 
Allow AsyncMethodBuilder attribute on
methods
CallerArgumentExpression attribute diagnostics
public static void Validate (bool condition,  
[CallerArgumentExpression( "condition" )] string? message =null) 
{ 
    if (!condition)  
    { 
        throw new InvalidOperationException( $"Argument failed validation:  
<{message} >"); 
    } 
} C# 10 supports a new format for the #line pragma. Y ou likely won't use the new format,
but you'll see its effects. The enhancements enable more fine-grained output in domain-
specific languages (DSLs) like Razor. The Razor engine uses these enhancements to
improve the debugging experience. Y ou'll find debuggers can highlight your Razor
source more accurately. T o learn more about the new syntax, see the article on
Preprocessor directives  in the language reference. Y ou can also read the feature
specification  for Razor based examples.Enhanced #line pragmaLearn about any breaking changes in
the C# compiler
Article •11/18/2022
You can find breaking changes since the C# 10 release here.
The Roslyn  team maintains a list of breaking changes in the C# and Visual Basic
compilers. Y ou can find information on those changes at these links on their GitHub
repository:
Breaking changes in R oslyn in C# 10.0/.NET 6
Breaking changes in R oslyn after .NET 5
Breaking changes in VS2019 version 16.8 introduced with .NET 5 and C# 9.0
Breaking changes in VS2019 Update 1 and beyond compared to VS2019
Breaking changes since VS2017 (C# 7)
Breaking changes in R oslyn 3.0 (VS2019) from R oslyn 2.* (VS2017)
Breaking changes in R oslyn 2.0 (VS2017) from R oslyn 1.* (VS2015) and native C#
compiler (VS2013 and previous).
Breaking changes in R oslyn 1.0 (VS2015) from the native C# compiler (VS2013 and
previous).
Unicode version change in C# 6
The history of C#
Article •11/14/2023
This article provides a history of each major release of the C# language. The C# team is
continuing to innovate and add new features. Detailed language feature status,
including features considered for upcoming releases can be found on the dotnet/roslyn
repository  on GitHub.
Releas ed No vember , 2022
The following features were added in C# 11:
Raw string literals
Generic math support
Generic attributes
UTF-8 string literals
Newlines in string interpolation expressions
List patterns
File-local types
Required members
Auto-default structs
Pattern match Span<char>  on a constant string
Extended nameof  scope
Numeric IntPtr
） Impor tant
The C# language relies on types and methods in what the C# specification defines
as a standar d libr ary for some of the features. The .NET platform delivers those
types and methods in a number of packages. One example is exception processing.
Every throw statement or expression is checked to ensure the object being thrown
is derived from Exception . Similarly, every catch is checked to ensure that the type
being caught is derived from Exception . Each version may add new requirements.
To use the latest language features in older environments, you may need to install
specific libraries. These dependencies are documented in the page for each specific
version. Y ou can learn more about the relationships betw een language and librar y
for background on this dependency.
C# version 11ref fields and scoped ref
Improved method group conversion to delegate
Warning wave 7
C# 11 introduces gener ic math  and several features that support that goal. Y ou can write
numeric algorithms once for all number types. There's more features to make working
with struct types easier, like required members and auto-default structs. W orking with
strings gets easier with Raw string literals, newline in string interpolations, and UTF-8
string literals. Features like file local types enable source generators to be simpler.
Finally, list patterns add more support for pattern matching.
Releas ed No vember , 2021
C# 10 adds the following features and enhancements to the C# language:
Record structs
Improvements of structure types
Interpolated string handlers
global using  directives
File-scoped namespace declaration
Extended property patterns
Improvements on lambda expressions
Allow const  interpolated strings
Record types can seal ToString()
Improved definite assignment
Allow both assignment and declaration in the same deconstruction
Allow AsyncMethodBuilder  attribute on methods
CallerArgumentExpression attribute
Enhanced #line  pragma
More features were available in preview  mode. In order to use these features, you must
set <LangV ersion>  to Preview  in your project:
Generic attributes  later in this article.
static abstract members in interfaces
C# 10 continues work on themes of removing ceremony, separating data from
algorithms, and improved performance for the .NET Runtime.
Many of the features mean you'll type less code to express the same concepts. Record
structs synthesize many of the same methods that record class es do. S tructs andC# version 10anonymous types support with expr essions . Global using dir ectives and file scoped
namesp ace declar ations  mean you express dependencies and namespace organization
more clearly. Lambda impr ovements  makes it easier to declare lambda expressions
where they're used. New property patterns and deconstruction improvements create
more concise code.
The new interpolated string handlers and AsyncMethodBuilder behavior can improve
performance. These language features were applied in the .NET Runtime to achieve
performance improvements in .NET 6.
C# 10 also marks more of a shift to the yearly cadence for .NET releases. Because not
every feature can be completed in a yearly timeframe, you can try a couple of "preview"
features in C# 10. Both gener ic attr ibutes and static abstr act member s in int erfaces can be
used, but these preview features may change before their final release.
Releas ed No vember , 2020
C# 9 was released with .NET 5. It's the default language version for any assembly that
targets the .NET 5 release. It contains the following new and enhanced features:
Records
Init only setters
Top-level statements
Pattern matching enhancements: relational patterns  and logical patterns
Performance and interop
Native sized integers
Function pointers
Suppress emitting localsinit flag
Module initializers
New features for partial methods
Fit and finish features
Target-typed new expressions
static  anonymous functions
Target-typed conditional expressions
Covariant return types
Extension GetEnumerator  support for foreach  loops
Lambda discard parameters
Attributes on local functionsC# version 9C# 9 continues three of the themes from previous releases: removing ceremony,
separating data from algorithms, and providing more patterns in more places.
Top level statements  means your main program is simpler to read. There's less need for
ceremony: a namespace, a Program class, and static void Main() are all unnecessary.
The introduction of records  provides a concise syntax for reference types that follow
value semantics for equality. Y ou'll use these types to define data containers that
typically define minimal behavior. Init-only setters  provide the capability for non-
destructive mutation ( with expressions) in records. C# 9 also adds covariant return
types  so that derived records can override virtual methods and return a type derived
from the base method's return type.
The pattern matching  capabilities have been expanded in several ways. Numeric types
now support range p atterns. Patterns can be combined using and, or, and not patterns.
Parentheses can be added to clarify more complex patterns:
C# 9 includes new pattern matching improvements:
Type p atterns match an object matches a particular type
Parenthesized p atterns enforce or emphasize the precedence of pattern
combinations
Conjunctiv e and patterns require both patterns to match
Disjunctiv e or patterns require either pattern to match
Negat ed not patterns require that a pattern doesn't match
Relational p atterns require the input be less than, greater than, less than or equal,
or greater than or equal to a given constant.
These patterns enrich the syntax for patterns. Consider these examples:
C#
With optional parentheses to make it clear that and has higher precedence than or:
C#
One of the most common uses is a new syntax for a null check:public static bool IsLetter (this char c) =>
    c is >= 'a' and <= 'z' or >= 'A' and <= 'Z';
public static bool IsLetterOrSeparator (this char c) =>
    c is (>= 'a' and <= 'z') or (>= 'A' and <= 'Z') or '.' or ',';C#
Any of these patterns can be used in any context where patterns are allowed: is pattern
expressions, switch expressions, nested patterns, and the pattern of a switch
statement's case label.
Another set of features supports high-performance computing in C#:
The nint and nuint types model the native-size integer types on the target CPU.
Function pointers  provide delegate-like functionality while avoiding the allocations
necessary to create a delegate object.
The localsinit instruction can be omitted to save instructions.
Another set of improvements supports scenarios where code gener ators add
functionality:
Module initializers  are methods that the runtime calls when an assembly loads.
Partial methods  support new accessibly modifiers and non-void return types. In
those cases, an implementation must be provided.
C# 9 adds many other small features that improve developer productivity, both writing
and reading code:
Target-type new expressions
static anonymous functions
Target-type conditional expressions
Extension GetEnumerator() support for foreach loops
Lambda expressions can declare discard parameters
Attributes can be applied to local functions
The C# 9 release continues the work to keep C# a modern, general-purpose
programming language. Features continue to support modern workloads and
application types.if (e is not null)
{
    // ...
}
Performance and interop
Fit and finish featuresReleas ed Sept ember , 2019
C# 8.0 is the first major C# release that specifically targets .NET Core. Some features rely
on new CLR capabilities, others on library types added only in .NET Core. C# 8.0 adds
the following features and enhancements to the C# language:
Readonly members
Default interface methods
Pattern matching enhancements :
Switch expressions
Property patterns
Tuple patterns
Positional patterns
Using declarations
Static local functions
Disposable ref structs
Nullable reference types
Asynchronous streams
Indices and ranges
Null-coalescing assignment
Unmanaged constructed types
Stackalloc in nested expressions
Enhancement of interpolated verbatim strings
Default interface members require enhancements in the CLR. Those features were added
in the CLR for .NET Core 3.0. Ranges and indexes, and asynchronous streams require
new types in the .NET Core 3.0 libraries. Nullable reference types, while implemented in
the compiler, is much more useful when libraries are annotated to provide semantic
information regarding the null state of arguments and return values. Those annotations
are being added in the .NET Core libraries.
Releas ed May , 2018
There are two main themes to the C# 7.3 release. One theme provides features that
enable safe code to be as performant as unsafe code. The second theme provides
incremental improvements to existing features. New compiler options were also added
in this release.C# version 8.0
C# version 7.3The following new features support the theme of better performance for safe code:
You can access fixed fields without pinning.
You can reassign ref local variables.
You can use initializers on stackalloc arrays.
You can use fixed statements with any type that supports a pattern.
You can use more generic constraints.
The following enhancements were made to existing features:
You can test == and != with tuple types.
You can use expression variables in more locations.
You may attach attributes to the backing field of auto-implemented properties.
Method resolution when arguments differ by in has been improved.
Overload resolution now has fewer ambiguous cases.
The new compiler options are:
-publicsign  to enable Open Source Software (OSS) signing of assemblies.
-pathmap  to provide a mapping for source directories.
Releas ed No vember , 2017
C# 7.2 added several small language features:
Initializers on stackalloc arrays.
Use fixed statements with any type that supports a pattern.
Access fixed fields without pinning.
Reassign ref local variables.
Declare readonly struct types, to indicate that a struct is immutable and should
be passed as an in parameter to its member methods.
Add the in modifier on parameters, to specify that an argument is passed by
reference but not modified by the called method.
Use the ref readonly modifier on method returns, to indicate that a method
returns its value by reference but doesn't allow writes to that object.
Declare ref struct types, to indicate that a struct type accesses managed memory
directly and must always be stack allocated.
Use additional generic constraints.
Non-trailing named arguments
Named arguments can be followed by positional arguments.C# version 7.2Leading underscores in numeric literals
Numeric literals can now have leading underscores before any printed digits.
private protected  access modifier
The private protected access modifier enables access for derived classes in the
same assembly.
Conditional ref expressions
The result of a conditional expression ( ?:) can now be a reference.
Releas ed August, 2017
C# started releasing point r eleas es with C# 7.1. This version added the language version
selection  configuration element, three new language features, and new compiler
behavior.
The new language features in this release are:
async  Main  method
The entry point for an application can have the async modifier.
default  literal expressions
You can use default literal expressions in default value expressions when the
target type can be inferred.
Inferred tuple element names
The names of tuple elements can be inferred from tuple initialization in many
cases.
Pattern matching on generic type parameters
You can use pattern match expressions on variables whose type is a generic
type parameter.
Finally, the compiler has two options -refout  and -refonly  that control reference
assembly generation
Releas ed Mar ch, 2017
C# version 7.0 was released with Visual S tudio 2017. This version has some evolutionary
and cool stuff in the vein of C# 6.0. Here are some of the new features:
Out variables
Tuples and deconstructionC# version 7.1
C# version 7.0Pattern matching
Local functions
Expanded expression bodied members
Ref locals
Ref returns
Other features included:
Discards
Binary Literals and Digit Separators
Throw expressions
All of these features offer new capabilities for developers and the opportunity to write
cleaner code than ever. A highlight is condensing the declaration of variables to use
with the out keyword and by allowing multiple return values via tuple. .NET Core now
targets any operating system and has its eyes firmly on the cloud and on portability.
These new capabilities certainly occupy the language designers' thoughts and time, in
addition to coming up with new features.
Releas ed July , 2015
Version 6.0, released with Visual S tudio 2015, released many smaller features that made
C# programming more productive. Here are some of them:
Static imports
Exception filters
Auto-property initializers
Expression bodied members
Null propagator
String interpolation
nameof operator
Other new features include:
Index initializers
Await in catch/finally blocks
Default values for getter-only properties
Each of these features is interesting in its own right. But if you look at them altogether,
you see an interesting pattern. In this version, C# started to eliminate languageC# version 6.0boilerplate to make code more terse and readable. So for fans of clean, simple code, this
language version was a huge win.
They did one other thing along with this version, though it's not a traditional language
feature in itself. They released Roslyn the compiler as a service . The C# compiler is
now written in C#, and you can use the compiler as part of your programming efforts.
Releas ed August, 2012
C# version 5.0, released with Visual S tudio 2012, was a focused version of the language.
Nearly all of the effort for that version went into another groundbreaking language
concept: the async and await model for asynchronous programming. Here's the major
features list:
Asynchronous members
Caller info attributes
Code Project: Caller Info Attributes in C# 5.0
The caller info attribute lets you easily retrieve information about the context in which
you're running without resorting to a ton of boilerplate reflection code. It has many uses
in diagnostics and logging tasks.
But async and await are the real stars of this release. When these features came out in
2012, C# changed the game again by baking asynchrony into the language as a first-
class participant. If you've ever dealt with long running operations and the
implementation of webs of callbacks, you probably loved this language feature.
Releas ed Apr il, 2010
C# version 4.0, released with Visual S tudio 2010, would have had a difficult time living
up to the groundbreaking status of version 3.0. This version introduced some interesting
new features:
Dynamic binding
Named/optional arguments
Generic covariant and contravariant
Embedded interop types
C# version 5.0
C# version 4.0Embedded interop types eased the deployment pain of creating C OM interop
assemblies for your application. Generic covariance and contravariance give you more
power to use generics, but they're a bit academic and probably most appreciated by
framework and library authors. Named and optional parameters let you eliminate many
method overloads and provide convenience. But none of those features are exactly
paradigm altering.
The major feature was the introduction of the dynamic keyword. The dynamic keyword
introduced into C# version 4.0 the ability to override the compiler on compile-time
typing. By using the dynamic keyword, you can create constructs similar to dynamically
typed languages like JavaScript. Y ou can create a dynamic x = "a string" and then add
six to it, leaving it up to the runtime to sort out what should happen next.
Dynamic binding gives you the potential for errors but also great power within the
language.
Releas ed No vember , 2007
C# version 3.0 came in late 2007, along with Visual S tudio 2008, though the full boat of
language features would actually come with .NET Framework version 3.5. This version
marked a major change in the growth of C#. It established C# as a truly formidable
programming language. Let's take a look at some major features in this version:
Auto-implemented properties
Anonymous types
Query expressions
Lambda expressions
Expression trees
Extension methods
Implicitly typed local variables
Partial methods
Object and collection initializers
In retrospect, many of these features seem both inevitable and inseparable. They all fit
together strategically. It's thought that C# version's killer feature was the query
expression, also known as Language-Integrated Query (LINQ).
A more nuanced view examines expression trees, lambda expressions, and anonymous
types as the foundation upon which LINQ is constructed. But, in either case, C# 3.0C# version 3.0presented a revolutionary concept. C# 3.0 had begun to lay the groundwork for turning
C# into a hybrid Object-Oriented / Functional language.
Specifically, you could now write SQL-style, declarative queries to perform operations on
collections, among other things. Instead of writing a for loop to compute the average
of a list of integers, you could now do that as simply as list.Average(). The
combination of query expressions and extension methods made a list of integers a
whole lot smarter.
Releas ed No vember , 2005
Let's take a look at some major features of C# 2.0, released in 2005, along with Visual
Studio 2005:
Generics
Partial types
Anonymous methods
Nullable value types
Iterators
Covariance and contravariance
Other C# 2.0 features added capabilities to existing features:
Getter/setter separate accessibility
Method group conversions (delegates)
Static classes
Delegate inference
While C# may have started as a generic Object-Oriented (OO) language, C# version 2.0
changed that in a hurry. With generics, types and methods can operate on an arbitrary
type while still retaining type safety. For instance, having a List<T>  lets you have
List<string> or List<int> and perform type-safe operations on those strings or
integers while you iterate through them. Using generics is better than creating a
ListInt type that derives from ArrayList or casting from Object for every operation.
C# version 2.0 brought iterators. T o put it succinctly, iterators let you examine all the
items in a List (or other Enumerable types) with a foreach loop. Having iterators as a
first-class part of the language dramatically enhanced readability of the language and
people's ability to reason about the code.C# version 2.0And yet, C# continued to play a bit of catch-up with Java. Java had already released
versions that included generics and iterators. But that would soon change as the
languages continued to evolve apart.
Releas ed Apr il, 2003
C# version 1.2 shipped with Visual S tudio .NET 2003. It contained a few small
enhancements to the language. Most notable is that starting with this version, the code
generated in a foreach loop called Dispose  on an IEnumerator  when that IEnumerator
implemented IDisposable .
Releas ed Januar y, 2002
When you go back and look, C# version 1.0, released with Visual S tudio .NET 2002,
looked a lot like Java. As part of its stated design goals for ECMA , it sought to be a
"simple, modern, general-purpose object-oriented language." At the time, looking like
Java meant it achieved those early design goals.
But if you look back on C# 1.0 now, you'd find yourself a little dizzy. It lacked the built-in
async capabilities and some of the slick functionality around generics you take for
granted. As a matter of fact, it lacked generics altogether. And LINQ ? Not available yet.
Those additions would take some years to come out.
C# version 1.0 looked stripped of features, compared to today. Y ou'd find yourself
writing some verbose code. But yet, you have to start somewhere. C# version 1.0 was a
viable alternative to Java on the Windows platform.
The major features of C# 1.0 included:
Classes
Structs
Interfaces
Events
Properties
Delegates
Operators and expressions
Statements
AttributesC# version 1.2
C# version 1.0
Article originally published on the NDepend blog , courtesy of Erik Dietr ich and P atrick
Smac chia.
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
 Provide product feedbackRelationships between language
features and library types
Article •10/26/2023
The C# language definition requires a standard library to have certain types and certain
accessible members on those types. The compiler generates code that uses these
required types and members for many different language features. For this reason, C#
versions are supported only for the corresponding .NET version and newer. That ensures
the correct run-time behavior and the availability of all required types and members.
This dependency on standard library functionality has been part of the C# language
since its first version. In that version, examples included:
Exception  - used for all compiler-generated exceptions.
String  - synonym of string.
Int32  - synonym of int.
That first version was simple: the compiler and the standard library shipped together,
and there was only one version of each.
Subsequent versions of C# have occasionally added new types or members to the
dependencies. Examples include: INotifyCompletion , CallerFileP athAttribute , and
CallerMemberNameAttribute . C# 7.0 added a dependency on ValueTuple  to implement
the tuples  language feature. C# 8 requires System.Index  and System.Range  for ranges
and indexes , among other features. Each new version might add additional
requirements.
The language design team works to minimize the surface area of the types and
members required in a compliant standard library. That goal is balanced against a clean
design where new library features are incorporated seamlessly into the language. There
will be new features in future versions of C# that require new types and members in a
standard library. C# compiler tools are now decoupled from the release cycle of the .NET
libraries on supported platforms.
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review.NET feedb ack
The .NET documentation is open
source. Provide feedback here.issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackVersion and update considerations for
C# developers
Article •06/29/2023
Compatibility is an important goal as new features are added to the C# language. In
almost all cases, existing code can be recompiled with a new compiler version without
any issue. The .NET runtime team also has a goal to ensure compatibility for updated
libraries. In almost all cases, when your app is launched from an updated runtime with
updated libraries, the behavior is exactly the same as with previous versions.
The language version used to compile your app typically matches the runtime target
framework moniker (TFM) referenced in your project. For more information on changing
the default language version, see the article titled configure your language version . This
default behavior ensures maximum compatibility.
When breaking changes  are introduced, they're classified as:
Binar y breaking change : A binary breaking change causes different behavior,
including possibly crashing, in your application or library when launched using a
new runtime. Y ou must recompile your app to incorporate these changes. The
existing binary won't function correctly.
Source breaking change : A source breaking change changes the meaning of your
source code. Y ou need to make source code edits before compiling your
application with the latest language version. Y our existing binary will run correctly
with the newer host and runtime. Note that for language syntax, a source breaking
change  is also a behavior al change , as defined in the runtime breaking changes .
When a binary breaking change affects your app, you must recompile your app, but you
don't need to edit any source code. When a source breaking change affects your app,
the existing binary still runs correctly in environments with the updated runtime and
libraries. However, you must make source changes to recompile with the new language
version and runtime. If a change is both source breaking and binary breaking, you must
recompile your application with the latest version and make source updates.
Because of the goal to avoid breaking changes by the C# language team and runtime
team, updating your application is typically a matter of updating the TFM and rebuilding
the app. However, for libraries that are distributed publicly, you should carefully evaluate
your policy for supported TFMs and supported language versions. Y ou may be creating
a new library with features found in the latest version and need to ensure apps built
using previous versions of the compiler can use it. Or you may be upgrading an existing
library and many of your users might not have upgraded versions yet.When you adopt new language features in your library's public API, you should evaluate
if adopting the feature introduces either a binary or source breaking change for the
users of your library. Any changes to your internal implementation that don't appear in
the public or protected interfaces are compatible.
A binar y breaking change  requires your users to recompile their code in order to use the
new version. For example, consider this public method:
C#
If you add the in modifier to the method, that's a binary breaking change:
C#
Users must recompile any application that uses the CalculateSquare method for the
new library to work correctly.
A source breaking change  requires your users to change their code before they
recompile. For example, consider this type:
C#Introducing breaking changes in your libraries
７ Note
If you use the System.Runtime.CompilerSer vices.Int ernalsVisibleT oAttribut e to
enable types to see internal members, the internal members can introduce
breaking changes.
public double CalculateSquare (double value) => value * value; 
public double CalculateSquare (in double value) => value * value; 
public class Person 
{ 
    public string FirstName { get; } 
    public string LastName { get; } 
    public Person(string firstName, string lastName ) => (FirstName,  
LastName) = (firstName, lastName);  
    // other details omitted  
} In a newer version, you'd like to take advantage of the synthesized members generated
for record types. Y ou make the following change:
C#
The previous change requires changes for any type derived from Person. All those
declarations must add the record modifier to their declarations.
When you add a binar y breaking change  to your library, you force all projects that use
your library to recompile. However, none of the source code in those projects needs to
change. As a result, the impact of the breaking change is reasonably small for each
project.
When you make a source breaking change  to your library, you require all projects to
make source changes in order to use your new library. If the necessary change requires
new language features, you force those projects to upgrade to the same language
version and TFM you're now using. Y ou've required more work for your users, and
possibly forced them to upgrade as well.
The impact of any breaking change you make depends on the number of projects that
have a dependency on your library. If your library is used internally by a few
applications, you can react to any breaking changes in all impacted projects. However, if
your library is publicly downloaded, you should evaluate the potential impact and
consider alternatives:
You might add new APIs that parallel existing APIs.
You might consider parallel builds for different TFMs.
You might consider multi-targeting.public record class Person(string FirstName, string LastName ); 
Impact of breaking changesTutorial: Explore primary constructors
Article •06/23/2023
C# 12 introduces primary constr uctors, a concise syntax to declare constructors whose
parameters are available anywhere in the body of the type.
In this tutorial, you will learn:
You need to set up your machine to run .NET 8 or later, including the C# 12 or later
compiler. The C# 12 compiler is available starting with Visual S tudio 2022 version 17.7
or the .NET 8 SDK .
You can add parameters to a struct or class declaration to create a primary
constr uctor. Primary constructor parameters are in scope throughout the class definition.
It's important to view primary constructor parameters as paramet ers even though they
are in scope throughout the class definition. Several rules clarify that they're parameters:
1. Primary constructor parameters may not be stored if they aren't needed.
2. Primary constructor parameters aren't members of the class. For example, a
primary constructor parameter named param can't be accessed as this.param.
3. Primary constructor parameters can be assigned to.
4. Primary constructor parameters don't become properties, except in record  types.
These rules are the same as parameters to any method, including other constructor
declarations.
The most common uses for a primary constructor parameter are:
1. As an argument to a base() constructor invocation.
2. To initialize a member field or property.
3. Referencing the constructor parameter in an instance member.When to declare a primary constructor on your type＂
How to call primary constructors from other constructors＂
How to use primary constructor parameters in members of the type＂
Where primary constructor parameters are stored＂
Prerequisites
Primary constructorsEvery other constructor for a class must  call the primary constructor, directly or
indirectly, through a this() constructor invocation. That rule ensures that primary
constructor parameters are assigned anywhere in the body of the type.
The following code initializes two readonly properties that are computed from primary
constructor parameters:
C#
The preceding code demonstrates a primary constructor used to initialize calculated
readonly properties. The field initializers for Magnitude and Direction use the primary
constructor parameters. The primary constructor parameters aren't used anywhere else
in the struct. The preceding struct is as though you'd written the following code:
C#
The new feature makes it easier to use field initializers when you need arguments to
initialize a field or property.
The preceding examples use primary constructor parameters to initialize readonly
properties. Y ou can also use primary constructors when the properties aren't readonly.Initialize property
public readonly  struct Distance (double dx, double dy)
{
    public readonly  double Magnitude { get; } = Math.Sqrt(dx * dx + dy *  
dy);
    public readonly  double Direction { get; } = Math.Atan2(dy, dx);
}
public readonly  struct Distance
{
    public readonly  double Magnitude { get; }
    public readonly  double Direction { get; }
    public Distance (double dx, double dy)
    {
        Magnitude = Math.Sqrt(dx * dx + dy * dy);
        Direction = Math.Atan2(dy, dx);
    }
}
Create mutable stateConsider the following code:
C#
In the preceding example, the Translate method changes the dx and dy components.
That requires the Magnitude and Direction properties be computed when accessed. The
=> operator designates an expression-bodied get accessor, whereas the = operator
designates an initializer. This version adds a parameterless constructor to the struct. The
parameterless constructor must invoke the primary constructor, so that all the primary
constructor parameters are initialized.
In the previous example, the primary constructor properties are accessed in a method.
Therefore the compiler creates hidden fields to represent each parameter. The following
code shows approximately what the compiler generates. The actual field names are valid
CIL identifiers, but not valid C# identifiers.
C#public struct Distance (double dx, double dy)
{
    public readonly  double Magnitude => Math.Sqrt(dx * dx + dy * dy);
    public readonly  double Direction => Math.Atan2(dy, dx);
    public void Translate (double deltaX, double deltaY)
    {
        dx += deltaX;
        dy += deltaY;
    }
    public Distance () : this(0,0) { }
}
public struct Distance
{
    private double __unspeakable_dx;
    private double __unspeakable_dy;
    public readonly  double Magnitude => Math.Sqrt(__unspeakable_dx *  
__unspeakable_dx + __unspeakable_dy * __unspeakable_dy);
    public readonly  double Direction => Math.Atan2(__unspeakable_dy,  
__unspeakable_dx);
    public void Translate (double deltaX, double deltaY)
    {
        __unspeakable_dx += deltaX;
        __unspeakable_dy += deltaY;
    }
    public Distance (double dx, double dy)It's important to understand that the first example didn't require the compiler to create
a field to store the value of the primary constructor parameters. The second example
used the primary constructor parameter inside a method, and therefore required the
compiler to create storage for them. The compiler creates storage for any primary
constructors only when that parameter is accessed in the body of a member of your
type. Otherwise, the primary constructor parameters aren't stored in the object.
Another common use for primary constructors is to specify parameters for dependency
injection. The following code creates a simple controller that requires a service interface
for its use:
C#
The primary constructor clearly indicates the parameters needed in the class. Y ou use
the primary constructor parameters as you would any other variable in the class.
You can invoke a base class' primary constructor from the derived class' primary
constructor. It's the easiest way for you to write a derived class that must invoke a
primary constructor in the base class. For example, consider a hierarchy of classes that    {
        __unspeakable_dx = dx;
        __unspeakable_dy = dy;
    }
    public Distance () : this(0, 0) { }
}
Dependency injection
public interface  IService
{
    Distance GetDistance ();
}
public class ExampleController (IService service ) : ControllerBase
{
    [HttpGet]
    public ActionResult<Distance> Get()
    {
        return service.GetDistance();
    }
}
Initialize base classrepresent different account types as a bank. The base class would look something like
the following code:
C#
All bank accounts, regardless of the type, have properties for the account number and
an owner. In the completed application, other common functionality would be added to
the base class.
Many types require more specific validation on constructor parameters. For example, the
BankAccount has specific requirements for the owner and accountID parameters: The
owner must not be null or whitespace, and the accountID must be a string containing
10 digits. Y ou can add this validation when you assign the corresponding properties:
C#
The previous example shows how you can validate the constructor parameters before
assigning them to the properties. Y ou can use builtin methods, like
String.IsNullOrWhiteSpace(S tring) , or your own validation method, like
ValidAccountNumber. In the previous example, any exceptions are thrown from thepublic class BankAccount (string accountID, string owner)
{
    public string AccountID { get; } = accountID;
    public string Owner { get; } = owner;
    public override  string ToString () => $"Account ID: {AccountID} , Owner: 
{Owner}";
}
public class BankAccount (string accountID, string owner)
{
    public string AccountID { get; } = ValidAccountNumber(accountID) 
        ? accountID 
        : throw new ArgumentException( "Invalid account number" , 
nameof(accountID));
    public string Owner { get; } = string.IsNullOrWhiteSpace(owner) 
        ? throw new ArgumentException( "Owner name cannot be empty" , 
nameof(owner)) 
        : owner;
    public override  string ToString () => $"Account ID: {AccountID} , Owner: 
{Owner}";
    public static bool ValidAccountNumber (string accountID ) => 
    accountID?.Length == 10 && accountID.All(c => char.IsDigit(c));
}constructor, when it invokes the initializers. If a constructor parameter isn't used to
assign a field, any exceptions are thrown when the constructor parameter is first
accessed.
One derived class would present a checking account:
C#
The derived CheckingAccount class has a primary constructor that takes all the
parameters needed in the base class, and another parameter with a default value. The
primary constructor calls the base constructor using the : BankAccount(accountID,
owner) syntax. This expression specifies both the type for the base class, and the
arguments for the primary constructor.
Your derived class isn't required to use a primary constructor. Y ou can create a
constructor in the derived class that invokes the base class' primary constructor, aspublic class CheckingAccount (string accountID, string owner, decimal 
overdraftLimit = 0) : BankAccount (accountID, owner )
{
    public decimal CurrentBalance { get; private set; } = 0;
    public void Deposit(decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), "Deposit  
amount must be positive" );
        }
        CurrentBalance += amount;
    }
    public void Withdrawal (decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), 
"Withdrawal amount must be positive" );
        }
        if (CurrentBalance - amount < -overdraftLimit)
        {
            throw new InvalidOperationException( "Insufficient funds for  
withdrawal" );
        }
        CurrentBalance -= amount;
    }
    
    public override  string ToString () => $"Account ID: {AccountID} , Owner: 
{Owner}, Balance: {CurrentBalance} ";
}shown in the following example:
C#
There's one potential concern with class hierarchies and primary constructors: it's
possible to create multiple copies of a primary constructor parameter as it's used in
both derived and base classes. The following code example creates two copies each of
the owner and accountID field:
C#public class LineOfCreditAccount  : BankAccount
{
    private readonly  decimal _creditLimit;
    public LineOfCreditAccount (string accountID, string owner, decimal 
creditLimit ) : base(accountID, owner )
    {
        _creditLimit = creditLimit;
    }
    public decimal CurrentBalance { get; private set; } = 0;
    public void Deposit(decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), "Deposit  
amount must be positive" );
        }
        CurrentBalance += amount;
    }
    public void Withdrawal (decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), 
"Withdrawal amount must be positive" );
        }
        if (CurrentBalance - amount < -_creditLimit)
        {
            throw new InvalidOperationException( "Insufficient funds for  
withdrawal" );
        }
        CurrentBalance -= amount;
    }
    public override  string ToString () => $"{base.ToString()} , Balance: 
{CurrentBalance} ";
}The highlighted line shows that the ToString method uses the primary constr uctor
paramet ers (owner and accountID) rather than the base class pr operties (Owner and
AccountID). The result is that the derived class, SavingsAccount creates storage for those
copies. The copy in the derived class is different than the property in the base class. If
the base class property could be modified, the instance of the derived class won't see
that modification. The compiler issues a warning for primary constructor parameters
that are used in a derived class and passed to a base class constructor. In this instance,
the fix is to use the properties in the base class interface.public class SavingsAccount (string accountID, string owner, decimal 
interestRate ) : BankAccount (accountID, owner )
{
    public SavingsAccount () : this("default" , "default" , 0.01m) { }
    public decimal CurrentBalance { get; private set; } = 0;
    public void Deposit(decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), "Deposit  
amount must be positive" );
        }
        CurrentBalance += amount;
    }
    public void Withdrawal (decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException( nameof(amount), 
"Withdrawal amount must be positive" );
        }
        if (CurrentBalance - amount < 0)
        {
            throw new InvalidOperationException( "Insufficient funds for  
withdrawal" );
        }
        CurrentBalance -= amount;
    }
    public void ApplyInterest ()
    {
        CurrentBalance *= 1 + interestRate;
    }
    public override  string ToString () => $"Account ID: {accountID} , Owner: 
{owner}, Balance: {CurrentBalance} ";
}You can use the primary constructors as best suits your design. For classes and structs,
primary constructor parameters are parameters to a constructor that must be invoked.
You can use them to initialize properties. Y ou can initialize fields. Those properties or
fields can be immutable, or mutable. Y ou can use them in methods. They're parameters,
and you use them in what manner suits your design best. Y ou can learn more about
primary constructors in the C# programming guide article on instance constructors  and
the proposed primary constructor specification .Summary
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
 Provide product feedbackTutorial: Explore C# 11 feature - static
virtual memb ers in interfaces
Article •08/03/2022
C# 11 and .NET 7 include static vir tual member s in int erfaces. This feature enables you to
define interfaces that include overloaded operators  or other static members. Once
you've defined interfaces with static members, you can use those interfaces as
constraints  to create generic types that use operators or other static methods. Even if
you don't create interfaces with overloaded operators, you'll likely benefit from this
feature and the generic math classes enabled by the language update.
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET 7, which supports C# 11. The C# 11
compiler is available starting with Visual S tudio 2022, version 17.3  or the .NET 7
SDK .
Let's start with an example. The following method returns the midpoint of two double
numbers:
C#
The same logic would work for any numeric type: int, short, long, float decimal, or
any type that represents a number. Y ou need to have a way to use the + and /
operators, and to define a value for 2. You can use the
System.Numerics.INumber<T Self>  interface to write the preceding method as the
following generic method:Define interfaces with static members.＂
Use interfaces to define classes that implement interfaces with operators defined.＂
Create generic algorithms that rely on static interface methods.＂
Prerequisites
Static abstract interface methods
public static double MidPoint (double left, double right) =>
    (left + right) / ( 2.0);C#
Any type that implements the INumber<T Self>  interface must include a definition for
operator +, and for operator /. The denominator is defined by T.CreateChecked(2) to
create the value 2 for any numeric type, which forces the denominator to be the same
type as the two parameters. INumberBase<T Self>.CreateChecked<T Other>(T Other)
creates an instance of the type from the specified value and throws an
OverflowException  if the value falls outside the representable range. (This
implementation has the potential for overflow if left and right are both large enough
values. There are alternative algorithms that can avoid this potential issue.)
You define static abstract members in an interface using familiar syntax: Y ou add the
static and abstract modifiers to any static member that doesn't provide an
implementation. The following example defines an IGetNext<T> interface that can be
applied to any type that overrides operator ++:
C#
The constraint that the type argument, T, implements IGetNext<T> ensures that the
signature for the operator includes the containing type, or its type argument. Many
operators enforce that its parameters must match the type, or be the type parameter
constrained to implement the containing type. Without this constraint, the ++ operator
couldn't be defined in the IGetNext<T> interface.
You can create a structure that creates a string of 'A' characters where each increment
adds another character to the string using the following code:
C#public static T MidPoint<T>(T left, T right)
    where T : INumber<T> => (left + right) / T.CreateChecked( 2);  // note:  
the addition of left and right may overflow here; it's just for  
demonstration purposes
public interface  IGetNext <T> where T : IGetNext <T>
{
    static abstract  T operator  ++(T other);
}
public struct RepeatSequence : IGetNext<RepeatSequence>
{
    private const char Ch = 'A';
    public string Text = new string(Ch, 1);More generally, you can build any algorithm where you might want to define ++ to
mean "produce the next value of this type". Using this interface produces clear code and
results:
C#
The preceding example produces the following output:
PowerShell
This small example demonstrates the motivation for this feature. Y ou can use natural
syntax for operators, constant values, and other static operations. Y ou can explore these
techniques when you create multiple types that rely on static members, including
overloaded operators. Define the interfaces that match your types' capabilities and then
declare those types' support for the new interface.
The motivating scenario for allowing static methods, including operators, in interfaces is
to support generic math  algorithms. The .NET 7 base class library contains interface
definitions for many arithmetic operators, and derived interfaces that combine many    public RepeatSequence () {}
    public static RepeatSequence operator  ++(RepeatSequence other)
        => other with { Text = other.Text + Ch };
    public override  string ToString () => Text;
}
var str = new RepeatSequence();
for (int i = 0; i < 10; i++)
    Console.WriteLine(str++);
A
AA
AAA
AAAA
AAAAA
AAAAAA
AAAAAAA
AAAAAAAA
AAAAAAAAA
AAAAAAAAAA
Generic matharithmetic operators in an INumber<T> interface. Let's apply those types to build a
Point<T> record that can use any numeric type for T. The point can be moved by some
XOffset and YOffset using the + operator.
Start by creating a new Console application, either by using dotnet new or Visual S tudio.
The public interface for the Translation<T> and Point<T> should look like the following
code:
C#
You use the record type for both the Translation<T> and Point<T> types: Both store
two values, and they represent data storage rather than sophisticated behavior. The
implementation of operator + would look like the following code:
C#
For the previous code to compile, you'll need to declare that T supports the
IAdditionOperators<TSelf, TOther, TResult> interface. That interface includes the
operator + static method. It declares three type parameters: One for the left operand,
one for the right operand, and one for the result. Some types implement + for different
operand and result types. Add a declaration that the type argument, T implements
IAdditionOperators<T, T, T>:
C#
After you add that constraint, your Point<T> class can use the + for its addition
operator. Add the same constraint on the Translation<T> declaration:
C#// Note: Not complete. This won't compile yet.
public record Translation<T>(T XOffset, T YOffset);
public record Point<T>(T X, T Y)
{
    public static Point<T> operator  +(Point<T> left, Translation<T> right);
}
public static Point<T> operator  +(Point<T> left, Translation<T> right) =>
    left with { X = left.X + right.XOffset, Y = left.Y + right.YOffset };
public record Point<T>(T X, T Y) where T : IAdditionOperators<T, T, T>The IAdditionOperators<T, T, T> constraint prevents a developer using your class from
creating a Translation using a type that doesn't meet the constraint for the addition to
a point. Y ou've added the necessary constraints to the type parameter for
Translation<T> and Point<T> so this code works. Y ou can test by adding code like the
following above the declarations of Translation and Point in your Program.cs  file:
C#
You can make this code more reusable by declaring that these types implement the
appropriate arithmetic interfaces. The first change to make is to declare that Point<T,
T> implements the IAdditionOperators<Point<T>, Translation<T>, Point<T>> interface.
The Point type makes use of different types for operands and the result. The Point
type already implements an operator + with that signature, so adding the interface to
the declaration is all you need:
C#
Finally, when you're performing addition, it's useful to have a property that defines the
additive identity value for that type. There's a new interface for that feature:
IAdditiveIdentity<T Self,TR esult> . A translation of {0, 0} is the additive identity: The
resulting point is the same as the left operand. The IAdditiveIdentity<TSelf, TResult>
interface defines one readonly property, AdditiveIdentity, that returns the identity
value. The Translation<T> needs a few changes to implement this interface:
C#public record Translation<T>(T XOffset, T YOffset) where T : 
IAdditionOperators<T, T, T>;
var pt = new Point<int>(3, 4);
var translate = new Translation< int>(5, 10);
var final = pt + translate;
Console.WriteLine(pt);
Console.WriteLine(translate);
Console.WriteLine(final);
public record Point<T>(T X, T Y) : IAdditionOperators<Point<T>,  
Translation<T>, Point<T>>
    where T : IAdditionOperators<T, T, T>There are a few changes here, so let's walk through them one by one. First, you declare
that the Translation type implements the IAdditiveIdentity interface:
C#
You next might try implementing the interface member as shown in the following code:
C#
The preceding code won't compile, because 0 depends on the type. The answer: Use
IAdditiveIdentity<T>.AdditiveIdentity for 0. That change means that your constraints
must now include that T implements IAdditiveIdentity<T>. That results in the
following implementation:
C#
Now that you've added that constraint on Translation<T>, you need to add the same
constraint to Point<T>:
C#using System.Numerics;
public record Translation<T>(T XOffset, T YOffset) :  
IAdditiveIdentity<Translation<T>, Translation<T>>
    where T : IAdditionOperators<T, T, T>, IAdditiveIdentity<T, T>
{
    public static Translation<T> AdditiveIdentity =>
        new Translation<T>(XOffset: T.AdditiveIdentity, YOffset:  
T.AdditiveIdentity);
}
public record Translation<T>(T XOffset, T YOffset) :  
IAdditiveIdentity<Translation<T>, Translation<T>>
public static Translation<T> AdditiveIdentity =>
    new Translation<T>(XOffset: 0, YOffset: 0);
public static Translation<T> AdditiveIdentity =>
    new Translation<T>(XOffset: T.AdditiveIdentity, YOffset:  
T.AdditiveIdentity);
using System.Numerics;
public record Point<T>(T X, T Y) : IAdditionOperators<Point<T>,  This sample has given you a look at how the interfaces for generic math compose. Y ou
learned how to:
Experiment with these features and register feedback. Y ou can use the Send Feedb ack
menu item in Visual S tudio, or create a new issue  in the roslyn repository on GitHub.
Build generic algorithms that work with any numeric type. Build algorithms using these
interfaces where the type argument may only implement a subset of number-like
capabilities. Even if you don't build new interfaces that use these capabilities, you can
experiment with using them in your algorithms.
Generic mathTranslation<T>, Point<T>>
    where T : IAdditionOperators<T, T, T>, IAdditiveIdentity<T, T>
{
    public static Point<T> operator  +(Point<T> left, Translation<T> right)  
=>
        left with { X = left.X + right.XOffset, Y = left.Y + right.YOffset  
};
}
Write a method that relied on the INumber<T> interface so that method could be
used with any numeric type.＂
Build a type that relies on the addition interfaces to implement a type that only
supports one mathematical operation. That type declares its support for those same
interfaces so it can be composed in other ways. The algorithms are written using
the most natural syntax of mathematical operators.＂
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
 Provide product feedbackUse pattern matching to build your class
behavior for better code
Article •12/06/2022
The pattern matching features in C# provide syntax to express your algorithms. Y ou can
use these techniques to implement the behavior in your classes. Y ou can combine
object-oriented class design with a data-oriented implementation to provide concise
code while modeling real-world objects.
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET. Download Visual S tudio 2022  or the
.NET SDK .
In this tutorial, you'll build a C# class that simulates a canal lock . Briefly, a canal lock is
a device that raises and lowers boats as they travel between two stretches of water at
different levels. A lock has two gates and some mechanism to change the water level.
In its normal operation, a boat enters one of the gates while the water level in the lock
matches the water level on the side the boat enters. Once in the lock, the water level is
changed to match the water level where the boat will leave the lock. Once the water
level matches that side, the gate on the exit side opens. Safety measures make sure an
operator can't create a dangerous situation in the canal. The water level can be changed
only when both gates are closed. At most one gate can be open. T o open a gate, the
water level in the lock must match the water level outside the gate being opened.
You can build a C# class to model this behavior. A CanalLock class would support
commands to open or close either gate. It would have other commands to raise or lower
the water. The class should also support properties to read the current state of both
gates and the water level. Y our methods implement the safety measures.Express your object oriented classes using data patterns.＂
Implement those patterns using C#'s pattern matching features.＂
Leverage compiler diagnostics to validate your implementation.＂
Prerequisites
Build a simulation of a canal lock
You'll build a console application to test your CanalLock class. Create a new console
project for .NET 5 using either Visual S tudio or the .NET CLI. Then, add a new class and
name it CanalLock. Next, design your public API, but leave the methods not
implemented:
C#
The preceding code initializes the object so both gates are closed, and the water level is
low. Next, write the following test code in your Main method to guide you as you create
a first implementation of the class:Define a class
public enum WaterLevel
{
    Low,
    High
}
public class CanalLock
{
    // Query canal lock state:
    public WaterLevel CanalLockWaterLevel { get; private set; } = 
WaterLevel.Low;
    public bool HighWaterGateOpen { get; private set; } = false;
    public bool LowWaterGateOpen { get; private set; } = false;
    // Change the upper gate.
    public void SetHighGate (bool open)
    {
        throw new NotImplementedException();
    }
    // Change the lower gate.
    public void SetLowGate (bool open)
    {
        throw new NotImplementedException();
    }
    // Change water level.
    public void SetWaterLevel (WaterLevel newLevel )
    {
        throw new NotImplementedException();
    }
    public override  string ToString () =>
        $"The lower gate is {(LowWaterGateOpen ? "Open" : "Closed" )}. " +
        $"The upper gate is {(HighWaterGateOpen ? "Open" : "Closed" )}. " +
        $"The water level is {CanalLockWaterLevel} .";
}C#
Next, add a first implementation of each method in the CanalLock class. The following
code implements the methods of the class without concern to the safety rules. Y ou'll
add safety tests later:
C#// Create a new canal lock:
var canalGate = new CanalLock();
// State should be doors closed, water level low:
Console.WriteLine(canalGate);
canalGate.SetLowGate(open: true);
Console.WriteLine( $"Open the lower gate:  {canalGate} ");
Console.WriteLine( "Boat enters lock from lower gate" );
canalGate.SetLowGate(open: false);
Console.WriteLine( $"Close the lower gate:  {canalGate} ");
canalGate.SetWaterLevel(WaterLevel.High);
Console.WriteLine( $"Raise the water level: {canalGate} ");
canalGate.SetHighGate(open: true);
Console.WriteLine( $"Open the higher gate:  {canalGate} ");
Console.WriteLine( "Boat exits lock at upper gate" );
Console.WriteLine( "Boat enters lock from upper gate" );
canalGate.SetHighGate(open: false);
Console.WriteLine( $"Close the higher gate: {canalGate} ");
canalGate.SetWaterLevel(WaterLevel.Low);
Console.WriteLine( $"Lower the water level: {canalGate} ");
canalGate.SetLowGate(open: true);
Console.WriteLine( $"Open the lower gate:  {canalGate} ");
Console.WriteLine( "Boat exits lock at upper gate" );
canalGate.SetLowGate(open: false);
Console.WriteLine( $"Close the lower gate:  {canalGate} ");
// Change the upper gate.
public void SetHighGate (bool open)
{
    HighWaterGateOpen = open;
}
// Change the lower gate.The tests you've written so far pass. Y ou've implemented the basics. Now, write a test for
the first failure condition. At the end of the previous tests, both gates are closed, and
the water level is set to low. Add a test to try opening the upper gate:
C#
This test fails because the gate opens. As a first implementation, you could fix it with the
following code:
C#
Your tests pass. But, as you add more tests, you'll add more and more if clauses and
test different properties. Soon, these methods will get too complicated as you add morepublic void SetLowGate (bool open)
{
    LowWaterGateOpen = open;
}
// Change water level.
public void SetWaterLevel (WaterLevel newLevel )
{
    CanalLockWaterLevel = newLevel;
}
Console.WriteLine( "=============================================" );
Console.WriteLine( "     Test invalid commands" );
// Open "wrong" gate (2 tests)
try
{
    canalGate = new CanalLock();
    canalGate.SetHighGate(open: true);
}
catch (InvalidOperationException)
{
    Console.WriteLine( "Invalid operation: Can't open the high gate. Water is  
low.");
}
Console.WriteLine( $"Try to open upper gate: {canalGate} ");
// Change the upper gate.
public void SetHighGate (bool open)
{
    if (open && (CanalLockWaterLevel == WaterLevel.High))
        HighWaterGateOpen = true;
    else if (open && (CanalLockWaterLevel == WaterLevel.Low))
        throw new InvalidOperationException( "Cannot open high gate when the  
water is low" );
}conditionals.
A better way is to use patterns to determine if the object is in a valid state to execute a
command. Y ou can express if a command is allowed as a function of three variables: the
state of the gate, the level of the water, and the new setting:
New setting Gate stat e Water Lev el Result
Closed Closed High Closed
Closed Closed Low Closed
Closed Open High Closed
Closed Open Low Closed
Open Closed High Open
Open Closed Low Closed (Error)
Open Open High Open
Open Open Low Closed (Error)
The fourth and last rows in the table have strike through text because they're invalid.
The code you're adding now should make sure the high water gate is never opened
when the water is low. Those states can be coded as a single switch expression
(remember that false indicates "Closed"):
C#
Try this version. Y our tests pass, validating the code. The full table shows the possible
combinations of inputs and results. That means you and other developers can quicklyImplement the commands with patterns
HighWaterGateOpen = (open, HighWaterGateOpen, CanalLockWaterLevel) switch
{
    (false, false, WaterLevel.High) => false,
    (false, false, WaterLevel.Low) => false,
    (false, true, WaterLevel.High) => false,
    (false, true, WaterLevel.Low) => false, // should never happen
    (true, false, WaterLevel.High) => true,
    (true, false, WaterLevel.Low) => throw new 
InvalidOperationException( "Cannot open high gate when the water is low" ),
    (true, true, WaterLevel.High) => true,
    (true, true, WaterLevel.Low) => false, // should never happen
};look at the table and see that you've covered all the possible inputs. Even easier, the
compiler can help as well. After you add the previous code, you can see that the
compiler generates a warning: CS8524  indicates the switch expression doesn't cover all
possible inputs. The reason for that warning is that one of the inputs is an enum type.
The compiler interprets "all possible inputs" as all inputs from the underlying type,
typically an int. This switch expression only checks the values declared in the enum. To
remove the warning, you can add a catch-all discard pattern for the last arm of the
expression. This condition throws an exception, because it indicates invalid input:
C#
The preceding switch arm must be last in your switch expression because it matches all
inputs. Experiment by moving it earlier in the order. That causes a compiler error CS8510
for unreachable code in a pattern. The natural structure of switch expressions enables
the compiler to generate errors and warnings for possible mistakes. The compiler "safety
net" makes it easier for you to create correct code in fewer iterations, and the freedom
to combine switch arms with wildcards. The compiler will issue errors if your
combination results in unreachable arms you didn't expect, and warnings if you remove
an arm that's needed.
The first change is to combine all the arms where the command is to close the gate;
that's always allowed. Add the following code as the first arm in your switch expression:
C#
After you add the previous switch arm, you'll get four compiler errors, one on each of
the arms where the command is false. Those arms are already covered by the newly
added arm. Y ou can safely remove those four lines. Y ou intended this new switch arm to
replace those conditions.
Next, you can simplify the four arms where the command is to open the gate. In both
cases where the water level is high, the gate can be opened. (In one, it's already open.)
One case where the water level is low throws an exception, and the other shouldn't
happen. It should be safe to throw the same exception if the water lock is already in an
invalid state. Y ou can make the following simplifications for those arms:
C#_  => throw new InvalidOperationException( "Invalid internal state" ),
(false, _, _) => false,Run your tests again, and they pass. Here's the final version of the SetHighGate method:
C#
Now that you've seen the technique, fill in the SetLowGate and SetWaterLevel methods
yourself. S tart by adding the following code to test invalid operations on those methods:
C#(true, _, WaterLevel.High) => true,
(true, false, WaterLevel.Low) => throw new InvalidOperationException( "Cannot 
open high gate when the water is low" ),
_ => throw new InvalidOperationException( "Invalid internal state" ),
// Change the upper gate.
public void SetHighGate (bool open)
{
    HighWaterGateOpen = (open, HighWaterGateOpen, CanalLockWaterLevel) 
switch
    {
        (false, _,    _)               => false,
        (true, _,     WaterLevel.High) => true,
        (true, false, WaterLevel.Low)  => throw new 
InvalidOperationException( "Cannot open high gate when the water is low" ),
        _                              => throw new 
InvalidOperationException( "Invalid internal state" ),
    };
}
Implement patterns yourself
Console.WriteLine();
Console.WriteLine();
try
{
    canalGate = new CanalLock();
    canalGate.SetWaterLevel(WaterLevel.High);
    canalGate.SetLowGate(open: true);
}
catch (InvalidOperationException)
{
    Console.WriteLine( "invalid operation: Can't open the lower gate. Water  
is high." );
}
Console.WriteLine( $"Try to open lower gate: {canalGate} ");
// change water level with gate open (2 tests)
Console.WriteLine();
Console.WriteLine();Run your application again. Y ou can see the new tests fail, and the canal lock gets into
an invalid state. T ry to implement the remaining methods yourself. The method to set
the lower gate should be similar to the method to set the upper gate. The method that
changes the water level has different checks, but should follow a similar structure. Y ou
may find it helpful to use the same process for the method that sets the water level.
Start with all four inputs: The state of both gates, the current state of the water level,
and the requested new water level. The switch expression should start with:
C#
You'll have 16 total switch arms to fill in. Then, test and simplify.
Did you make methods something like this?
C#try
{
    canalGate = new CanalLock();
    canalGate.SetLowGate(open: true);
    canalGate.SetWaterLevel(WaterLevel.High);
}
catch (InvalidOperationException)
{
    Console.WriteLine( "invalid operation: Can't raise water when the lower  
gate is open." );
}
Console.WriteLine( $"Try to raise water with lower gate open: {canalGate} ");
Console.WriteLine();
Console.WriteLine();
try
{
    canalGate = new CanalLock();
    canalGate.SetWaterLevel(WaterLevel.High);
    canalGate.SetHighGate(open: true);
    canalGate.SetWaterLevel(WaterLevel.Low);
}
catch (InvalidOperationException)
{
    Console.WriteLine( "invalid operation: Can't lower water when the high  
gate is open." );
}
Console.WriteLine( $"Try to lower water with high gate open: {canalGate} ");
CanalLockWaterLevel = (newLevel, CanalLockWaterLevel, LowWaterGateOpen,  
HighWaterGateOpen) switch
{
    // elided
};Your tests should pass, and the canal lock should operate safely.
In this tutorial, you learned to use pattern matching to check the internal state of an
object before applying any changes to that state. Y ou can check combinations of
properties. Once you've built tables for any of those transitions, you test your code, then
simplify for readability and maintainability. These initial refactorings may suggest further
refactorings that validate internal state or manage other API changes. This tutorial
combined classes and objects with a more data-oriented, pattern-based approach to
implement those classes.// Change the lower gate.
public void SetLowGate (bool open)
{
    LowWaterGateOpen = (open, LowWaterGateOpen, CanalLockWaterLevel) switch
    {
        (false, _, _) => false,
        (true, _, WaterLevel.Low) => true,
        (true, false, WaterLevel.High) => throw new 
InvalidOperationException( "Cannot open high gate when the water is low" ),
        _ => throw new InvalidOperationException( "Invalid internal state" ),
    };
}
// Change water level.
public void SetWaterLevel (WaterLevel newLevel )
{
    CanalLockWaterLevel = (newLevel, CanalLockWaterLevel, LowWaterGateOpen,  
HighWaterGateOpen) switch
    {
        (WaterLevel.Low, WaterLevel.Low, true, false) => WaterLevel.Low,
        (WaterLevel.High, WaterLevel.High, false, true) => WaterLevel.High,
        (WaterLevel.Low, _, false, false) => WaterLevel.Low,
        (WaterLevel.High, _, false, false) => WaterLevel.High,
        (WaterLevel.Low, WaterLevel.High, false, true) => throw new 
InvalidOperationException( "Cannot lower water when the high gate is open" ),
        (WaterLevel.High, WaterLevel.Low, true, false) => throw new 
InvalidOperationException( "Cannot raise water when the low gate is open" ),
        _ => throw new InvalidOperationException( "Invalid internal state" ),
    };
}
Summary
６ Collaborat e with us on
GitHub.NET feedb ackThe source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackTutorial: Write a custom string
interpolation handler
Article •04/06/2023
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET 6, including the C# 10 compiler. The C#
10 compiler is available starting with Visual S tudio 2022  or .NET 6 SDK .
This tutorial assumes you're familiar with C# and .NET, including either Visual S tudio or
the .NET CLI.
C# 10 adds support for a custom interpolat ed str ing handler . An interpolated string
handler is a type that processes the placeholder expression in an interpolated string.
Without a custom handler, placeholders are processed similar to String.Format . Each
placeholder is formatted as text, and then the components are concatenated to form
the resulting string.
You can write a handler for any scenario where you use information about the resulting
string. Will it be used? What constraints are on the format? Some examples include:
You may require none of the resulting strings are greater than some limit, such as
80 characters. Y ou can process the interpolated strings to fill a fixed-length buffer,
and stop processing once that buffer length is reached.
You may have a tabular format, and each placeholder must have a fixed length. A
custom handler can enforce that, rather than forcing all client code to conform.
In this tutorial, you'll create a string interpolation handler for one of the core
performance scenarios: logging libraries. Depending on the configured log level, the
work to construct a log message isn't needed. If logging is off, the work to construct a
string from an interpolated string expression isn't needed. The message is never printed,Implement the string interpolation handler pattern ＂
Interact with the receiver in a string interpolation operation. ＂
Add arguments to the string interpolation handler ＂
Understand the new library features for string interpolation ＂
Prerequisites
New outlineso any string concatenation can be skipped. In addition, any expressions used in the
placeholders, including generating stack traces, doesn't need to be done.
An interpolated string handler can determine if the formatted string will be used, and
only perform the necessary work if needed.
Let's start from a basic Logger class that supports different levels:
C#
This Logger supports six different levels. When a message won't pass the log level filter,
there's no output. The public API for the logger accepts a (fully formatted) string as the
message. All the work to create the string has already been done.
This step is to build an interpolat ed str ing handler  that recreates the current behavior. An
interpolated string handler is a type that must have the following characteristics:
The System.Runtime.CompilerServices.InterpolatedS tringHandlerAttribute  applied
to the type.
A constructor that has two int parameters, literalLength and formattedCount.
(More parameters are allowed).Initial implementation
public enum LogLevel
{
    Off,
    Critical,
    Error,
    Warning,
    Information,
    Trace
}
public class Logger
{
    public LogLevel EnabledLevel { get; init; } = LogLevel.Error;
    public void LogMessage (LogLevel level, string msg)
    {
        if (EnabledLevel < level) return;
        Console.WriteLine(msg);
    }
}
Implement the handler patternA public AppendLiteral method with the signature: public void
AppendLiteral(string s).
A generic public AppendFormatted method with the signature: public void
AppendFormatted<T>(T t).
Internally, the builder creates the formatted string, and provides a member for a client
to retrieve that string. The following code shows a LogInterpolatedStringHandler type
that meets these requirements:
C#
You can now add an overload to LogMessage in the Logger class to try your new
interpolated string handler:
C#[InterpolatedStringHandler ]
public ref struct LogInterpolatedStringHandler
{
    // Storage for the built-up string
    StringBuilder builder;
    public LogInterpolatedStringHandler (int literalLength, int 
formattedCount )
    {
        builder = new StringBuilder(literalLength);
        Console.WriteLine( $"\tliteral length: {literalLength} , 
formattedCount: {formattedCount} ");
    }
    public void AppendLiteral (string s)
    {
        Console.WriteLine( $"\tAppendLiteral called: {{ {s}}}");
        
        builder.Append(s);
        Console.WriteLine( $"\tAppended the literal string" );
    }
    public void AppendFormatted<T>(T t)
    {
        Console.WriteLine( $"\tAppendFormatted called: {{ {t}}} is of type 
{typeof(T)}");
        builder.Append(t?.ToString());
        Console.WriteLine( $"\tAppended the formatted object" );
    }
    internal  string GetFormattedText () => builder.ToString();
}You don't need to remove the original LogMessage method, the compiler will prefer a
method with an interpolated handler parameter over a method with a string parameter
when the argument is an interpolated string expression.
You can verify that the new handler is invoked using the following code as the main
program:
C#
Running the application produces output similar to the following text:
PowerShellpublic void LogMessage (LogLevel level, LogInterpolatedStringHandler builder )
{
    if (EnabledLevel < level) return;
    Console.WriteLine(builder.GetFormattedText());
}
var logger = new Logger() { EnabledLevel = LogLevel.Warning };
var time = DateTime.Now;
logger.LogMessage(LogLevel.Error, $"Error Level. CurrentTime: {time}. This 
is an error. It will be printed." );
logger.LogMessage(LogLevel.Trace, $"Trace Level. CurrentTime: {time}. This 
won't be printed." );
logger.LogMessage(LogLevel.Warning, "Warning Level. This warning is a  
string, not an interpolated string expression." );
        literal length: 65, formattedCount: 1
        AppendLiteral called: {Error Level. CurrentTime: }
        Appended the literal string
        AppendFormatted called: { 10/20/2021 12:19:10 PM} is of type  
System.DateTime
        Appended the formatted object
        AppendLiteral called: {. This is an error. It will be printed.}
        Appended the literal string
Error Level. CurrentTime: 10/20/2021 12:19:10 PM. This is an error. It will  
be printed.
        literal length: 50, formattedCount: 1
        AppendLiteral called: {Trace Level. CurrentTime: }
        Appended the literal string
        AppendFormatted called: { 10/20/2021 12:19:10 PM} is of type  
System.DateTime
        Appended the formatted object
        AppendLiteral called: {. This won 't be printed.}
        Appended the literal stringTracing through the output, you can see how the compiler adds code to call the handler
and build the string:
The compiler adds a call to construct the handler, passing the total length of the
literal text in the format string, and the number of placeholders.
The compiler adds calls to AppendLiteral and AppendFormatted for each section of
the literal string and for each placeholder.
The compiler invokes the LogMessage method using the
CoreInterpolatedStringHandler as the argument.
Finally, notice that the last warning doesn't invoke the interpolated string handler. The
argument is a string, so that call invokes the other overload with a string parameter.
The preceding version of the interpolated string handler implements the pattern. T o
avoid processing every placeholder expression, you'll need more information in the
handler. In this section, you'll improve your handler so that it does less work when the
constructed string won't be written to the log. Y ou use
System.Runtime.CompilerServices.InterpolatedS tringHandlerArgumentAttribute  to
specify a mapping between parameters to a public API and parameters to a handler's
constructor. That provides the handler with the information needed to determine if the
interpolated string should be evaluated.
Let's start with changes to the Handler. First, add a field to track if the handler is
enabled. Add two parameters to the constructor: one to specify the log level for this
message, and the other a reference to the log object:
C#Warning Level. This warning is a string, not an interpolated string  
expression.
Add more capabilities to the handler
private readonly  bool enabled;
public LogInterpolatedStringHandler (int literalLength, int formattedCount,  
Logger logger, LogLevel logLevel )
{
    enabled = logger.EnabledLevel >= logLevel;
    builder = new StringBuilder(literalLength);
    Console.WriteLine( $"\tliteral length: {literalLength} , formattedCount: 
{formattedCount} ");
}Next, use the field so that your handler only appends literals or formatted objects when
the final string will be used:
C#
Next, you'll need to update the LogMessage declaration so that the compiler passes the
additional parameters to the handler's constructor. That's handled using the
System.Runtime.CompilerServices.InterpolatedS tringHandlerArgumentAttribute  on the
handler argument:
C#
This attribute specifies the list of arguments to LogMessage that map to the parameters
that follow the required literalLength and formattedCount parameters. The empty
string (""), specifies the receiver. The compiler substitutes the value of the Logger object
represented by this for the next argument to the handler's constructor. The compiler
substitutes the value of level for the following argument. Y ou can provide any number
of arguments for any handler you write. The arguments that you add are string
arguments.public void AppendLiteral (string s)
{
    Console.WriteLine( $"\tAppendLiteral called: {{ {s}}}");
    if (!enabled) return;
    builder.Append(s);
    Console.WriteLine( $"\tAppended the literal string" );
}
public void AppendFormatted<T>(T t)
{
    Console.WriteLine( $"\tAppendFormatted called: {{ {t}}} is of type 
{typeof(T)}");
    if (!enabled) return;
    builder.Append(t?.ToString());
    Console.WriteLine( $"\tAppended the formatted object" );
}
public void LogMessage (LogLevel level,  
[InterpolatedStringHandlerArgument( "", "level")] 
LogInterpolatedStringHandler builder)
{
    if (EnabledLevel < level) return;
    Console.WriteLine(builder.GetFormattedText());
}You can run this version using the same test code. This time, you'll see the following
results:
PowerShell
You can see that the AppendLiteral and AppendFormat methods are being called, but
they aren't doing any work. The handler has determined that the final string won't be
needed, so the handler doesn't build it. There are still a couple of improvements to
make.
First, you can add an overload of AppendFormatted that constrains the argument to a
type that implements System.IFormattable . This overload enables callers to add format
strings in the placeholders. While making this change, let's also change the return type
of the other AppendFormatted and AppendLiteral methods, from void to bool (if any of
these methods have different return types, then you'll get a compilation error). That
change enables short circuiting . The methods return false to indicate that processing of
the interpolated string expression should be stopped. R eturning true indicates that it
should continue. In this example, you're using it to stop processing when the resulting
string isn't needed. Short circuiting supports more fine-grained actions. Y ou could stop
processing the expression once it reaches a certain length, to support fixed-length
buffers. Or some condition could indicate remaining elements aren't needed.
C#        literal length: 65, formattedCount: 1
        AppendLiteral called: {Error Level. CurrentTime: }
        Appended the literal string
        AppendFormatted called: { 10/20/2021 12:19:10 PM} is of type  
System.DateTime
        Appended the formatted object
        AppendLiteral called: {. This is an error. It will be printed.}
        Appended the literal string
Error Level. CurrentTime: 10/20/2021 12:19:10 PM. This is an error. It will  
be printed.
        literal length: 50, formattedCount: 1
        AppendLiteral called: {Trace Level. CurrentTime: }
        AppendFormatted called: { 10/20/2021 12:19:10 PM} is of type  
System.DateTime
        AppendLiteral called: {. This won 't be printed.}
Warning Level. This warning is a string, not an interpolated string  
expression.
public void AppendFormatted<T>(T t, string format) where T : IFormattable
{
    Console.WriteLine( $"\tAppendFormatted (IFormattable version) called: {t} 
with format {{ {format} }} is of type {typeof(T)},");With that addition, you can specify format strings in your interpolated string expression:
C#
The :t on the first message specifies the "short time format" for the current time. The
previous example showed one of the overloads to the AppendFormatted method that you
can create for your handler. Y ou don't need to specify a generic argument for the object
being formatted. Y ou may have more efficient ways to convert types you create to
string. Y ou can write overloads of AppendFormatted that takes those types instead of a
generic argument. The compiler will pick the best overload. The runtime uses this
technique to convert System.Span<T>  to string output. Y ou can add an integer
parameter to specify the alignment  of the output, with or without an IFormattable . The
System.Runtime.CompilerServices.DefaultInterpolatedS tringHandler  that ships with .NET
6 contains nine overloads of AppendFormatted  for different uses. Y ou can use it as a
reference while building a handler for your purposes.
Run the sample now, and you'll see that for the Trace message, only the first
AppendLiteral is called:
PowerShell    builder.Append(t?.ToString(format, null));
    Console.WriteLine( $"\tAppended the formatted object" );
}
var time = DateTime.Now;
logger.LogMessage(LogLevel.Error, $"Error Level. CurrentTime: {time}. The 
time doesn't use formatting." );
logger.LogMessage(LogLevel.Error, $"Error Level. CurrentTime: {time:t} . This 
is an error. It will be printed." );
logger.LogMessage(LogLevel.Trace, $"Trace Level. CurrentTime: {time:t} . This 
won't be printed." );
        literal length: 60, formattedCount: 1
        AppendLiteral called: Error Level. CurrentTime:
        Appended the literal string
        AppendFormatted called: 10/20/2021 12:18:29 PM is of type  
System.DateTime
        Appended the formatted object
        AppendLiteral called: . The time doesn 't use formatting.
        Appended the literal string
Error Level. CurrentTime: 10/20/2021 12:18:29 PM. The time doesn' t use 
formatting.
        literal length: 65, formattedCount: 1
        AppendLiteral called: Error Level. CurrentTime:
        Appended the literal stringYou can make one final update to the handler's constructor that improves efficiency. The
handler can add a final out bool parameter. Setting that parameter to false indicates
that the handler shouldn't be called at all to process the interpolated string expression:
C#
That change means you can remove the enabled field. Then, you can change the return
type of AppendLiteral and AppendFormatted to void. Now, when you run the sample,
you'll see the following output:
PowerShell        AppendFormatted (IFormattable version) called: 10/20/2021 12:18:29 
PM with format {t} is of type System.DateTime,
        Appended the formatted object
        AppendLiteral called: . This is an error. It will be printed.
        Appended the literal string
Error Level. CurrentTime: 12:18 PM. This is an error. It will be printed.
        literal length: 50, formattedCount: 1
        AppendLiteral called: Trace Level. CurrentTime:
Warning Level. This warning is a string, not an interpolated string  
expression.
public LogInterpolatedStringHandler (int literalLength, int formattedCount,  
Logger logger, LogLevel level, out bool isEnabled )
{
    isEnabled = logger.EnabledLevel >= level;
    Console.WriteLine( $"\tliteral length: {literalLength} , formattedCount: 
{formattedCount} ");
    builder = isEnabled ? new StringBuilder(literalLength) : default!;
}
        literal length: 60, formattedCount: 1
        AppendLiteral called: Error Level. CurrentTime:
        Appended the literal string
        AppendFormatted called: 10/20/2021 12:19:10 PM is of type  
System.DateTime
        Appended the formatted object
        AppendLiteral called: . The time doesn 't use formatting.
        Appended the literal string
Error Level. CurrentTime: 10/20/2021 12:19:10 PM. The time doesn' t use 
formatting.
        literal length: 65, formattedCount: 1
        AppendLiteral called: Error Level. CurrentTime:
        Appended the literal string
        AppendFormatted (IFormattable version) called: 10/20/2021 12:19:10 
PM with format {t} is of type System.DateTime,
        Appended the formatted object
        AppendLiteral called: . This is an error. It will be printed.
        Appended the literal stringThe only output when LogLevel.Trace was specified is the output from the constructor.
The handler indicated that it's not enabled, so none of the Append methods were
invoked.
This example illustrates an important point for interpolated string handlers, especially
when logging libraries are used. Any side-effects in the placeholders may not occur. Add
the following code to your main program and see this behavior in action:
C#
You can see the index variable is incremented five times each iteration of the loop.
Because the placeholders are evaluated only for Critical, Error and Warning levels,
not for Information and Trace, the final value of index doesn't match the expectation:
PowerShell
Interpolated string handlers provide greater control over how an interpolated string
expression is converted to a string. The .NET runtime team has already used this feature
to improve performance in several areas. Y ou can make use of the same capability in
your own libraries. T o explore further, look at theError Level. CurrentTime: 12:19 PM. This is an error. It will be printed.
        literal length: 50, formattedCount: 1
Warning Level. This warning is a string, not an interpolated string  
expression.
int index = 0;
int numberOfIncrements = 0;
for (var level = LogLevel.Critical; level <= LogLevel.Trace; level++)
{
    Console.WriteLine(level);
    logger.LogMessage(level, $"{level}: Increment index a few times 
{index++} , {index++} , {index++} , {index++} , {index++} ");
    numberOfIncrements += 5;
}
Console.WriteLine( $"Value of index {index}, value of numberOfIncrements: 
{numberOfIncrements} ");
Critical
Critical: Increment index a few times 0, 1, 2, 3, 4
Error
Error: Increment index a few times 5, 6, 7, 8, 9
Warning
Warning: Increment index a few times 10, 11, 12, 13, 14
Information
Trace
Value of index 15, value of numberOfIncrements: 25System.Runtime.CompilerServices.DefaultInterpolatedS tringHandler . It provides a more
complete implementation than you built here. Y ou'll see many more overloads that are
possible for the Append methods.Create record types
Article •11/14/2023
Records are types that use value-b ased equality . C# 10 adds record structs so that you
can define records as value types. T wo variables of a record type are equal if the record
type definitions are identical, and if for every field, the values in both records are equal.
Two variables of a class type are equal if the objects referred to are the same class type
and the variables refer to the same object. V alue-based equality implies other
capabilities you'll probably want in record types. The compiler generates many of those
members when you declare a record instead of a class. The compiler generates those
same methods for record struct types.
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET 6 or later, including the C# 10 or later
compiler. The C# 10 compiler is available starting with Visual S tudio 2022  or the .NET
6 SDK .
You define a record by declaring a type with the record keyword, modifying a class or
struct declaration. Optionally, you can omit the class keyword to create a record
class. A record follows value-based equality semantics. T o enforce value semantics, the
compiler generates several methods for your record type (both for record class types
and record struct types):
An override of Object.Equals(Object) .
A virtual Equals method whose parameter is the record type.
An override of Object.GetHashCode() .
Methods for operator == and operator !=.
Record types implement System.IEquatable<T> .
Records also provide an override of Object.T oString() . The compiler synthesizes methods
for displaying records using Object.T oString() . You'll explore those members as you writeDecide if you add the record modifier to a class type. ＂
Declare record types and positional record types.＂
Substitute your methods for compiler generated methods in records.＂
Prerequisites
Characteristics of recordsthe code for this tutorial. R ecords support with expressions to enable non-destructive
mutation of records.
You can also declare positional r ecords using a more concise syntax. The compiler
synthesizes more methods for you when you declare positional records:
A primary constructor whose parameters match the positional parameters on the
record declaration.
Public properties for each parameter of a primary constructor. These properties are
init-only  for record class types and readonly record struct types. For record
struct types, they're read-wr ite.
A Deconstruct method to extract properties from the record.
Data and statistics are among the scenarios where you'll want to use records. For this
tutorial, you'll build an application that computes degree days  for different uses. Degr ee
days are a measure of heat (or lack of heat) over a period of days, weeks, or months.
Degree days track and predict energy usage. More hotter days means more air
conditioning, and more colder days means more furnace usage. Degree days help
manage plant populations and correlate to plant growth as the seasons change. Degree
days help track animal migrations for species that travel to match climate.
The formula is based on the mean temperature on a given day and a baseline
temperature. T o compute degree days over time, you'll need the high and low
temperature each day for a period of time. Let's start by creating a new application.
Make a new console application. Create a new record type in a new file named
"DailyT emperature.cs":
C#
The preceding code defines a positional r ecord. The DailyTemperature record is a
readonly record struct, because you don't intend to inherit from it, and it should be
immutable. The HighTemp and LowTemp properties are init only pr operties, meaning they
can be set in the constructor or using a property initializer. If you wanted the positional
parameters to be read-write, you declare a record struct instead of a readonly record
struct. The DailyTemperature type also has a primary constr uctor that has two
parameters that match the two properties. Y ou use the primary constructor to initialize aBuild temperature data
public readonly  record struct DailyTemperature (double HighTemp, double 
LowTemp);DailyTemperature record. The following code creates and initializes several
DailyTemperature records. The first uses named parameters to clarify the HighTemp and
LowTemp. The remaining initializers use positional parameters to initialize the HighTemp
and LowTemp:
C#
You can add your own properties or methods to records, including positional records.
You'll need to compute the mean temperature for each day. Y ou can add that property
to the DailyTemperature record:
C#
Let's make sure you can use this data. Add the following code to your Main method:
C#private static DailyTemperature[] data = [
    new DailyTemperature(HighTemp: 57, LowTemp: 30), 
    new DailyTemperature( 60, 35),
    new DailyTemperature( 63, 33),
    new DailyTemperature( 68, 29),
    new DailyTemperature( 72, 47),
    new DailyTemperature( 75, 55),
    new DailyTemperature( 77, 55),
    new DailyTemperature( 72, 58),
    new DailyTemperature( 70, 47),
    new DailyTemperature( 77, 59),
    new DailyTemperature( 85, 65),
    new DailyTemperature( 87, 65),
    new DailyTemperature( 85, 72),
    new DailyTemperature( 83, 68),
    new DailyTemperature( 77, 65),
    new DailyTemperature( 72, 58),
    new DailyTemperature( 77, 55),
    new DailyTemperature( 76, 53),
    new DailyTemperature( 80, 60),
    new DailyTemperature( 85, 66) 
];
public readonly  record struct DailyTemperature (double HighTemp, double 
LowTemp)
{
    public double Mean => (HighTemp + LowTemp) / 2.0;
}
foreach (var item in data)
    Console.WriteLine(item);Run your application, and you'll see output that looks similar to the following display
(several rows removed for space):
.NET CLI
The preceding code shows the output from the override of ToString synthesized by the
compiler. If you prefer different text, you can write your own version of ToString that
prevents the compiler from synthesizing a version for you.
To compute degree days, you take the difference from a baseline temperature and the
mean temperature on a given day. T o measure heat over time, you discard any days
where the mean temperature is below the baseline. T o measure cold over time, you
discard any days where the mean temperature is above the baseline. For example, the
U.S. uses 65F as the base for both heating and cooling degree days. That's the
temperature where no heating or cooling is needed. If a day has a mean temperature of
70F, that day is five cooling degree days and zero heating degree days. Conversely, if
the mean temperature is 55F, that day is 10 heating degree days and 0 cooling degree
days.
You can express these formulas as a small hierarchy of record types: an abstract degree
day type and two concrete types for heating degree days and cooling degree days.
These types can also be positional records. They take a baseline temperature and a
sequence of daily temperature records as arguments to the primary constructor:
C#DailyTemperature { HighTemp = 57, LowTemp = 30, Mean = 43.5 }
DailyTemperature { HighTemp = 60, LowTemp = 35, Mean = 47.5 }
DailyTemperature { HighTemp = 80, LowTemp = 60, Mean = 70 }
DailyTemperature { HighTemp = 85, LowTemp = 66, Mean = 75.5 }
Compute degree days
public abstract  record DegreeDays (double BaseTemperature,  
IEnumerable<DailyTemperature> TempRecords );
public sealed record HeatingDegreeDays (double BaseTemperature,  
IEnumerable<DailyTemperature> TempRecords )
    : DegreeDays (BaseTemperature, TempRecords )
{
    public double DegreeDays => TempRecords.Where(s => s.Mean <  
BaseTemperature).Sum(s => BaseTemperature - s.Mean);
}The abstract DegreeDays record is the shared base class for both the HeatingDegreeDays
and CoolingDegreeDays records. The primary constructor declarations on the derived
records show how to manage base record initialization. Y our derived record declares
parameters for all the parameters in the base record primary constructor. The base
record declares and initializes those properties. The derived record doesn't hide them,
but only creates and initializes properties for parameters that aren't declared in its base
record. In this example, the derived records don't add new primary constructor
parameters. T est your code by adding the following code to your Main method:
C#
You'll get output like the following display:
.NET CLI
Your code calculates the correct number of heating and cooling degree days over that
period of time. But this example shows why you may want to replace some of the
synthesized methods for records. Y ou can declare your own version of any of the
compiler-synthesized methods in a record type except the clone method. The clone
method has a compiler-generated name and you can't provide a different
implementation. These synthesized methods include a copy constructor, the members
of the System.IEquatable<T>  interface, equality and inequality tests, and GetHashCode() .public sealed record CoolingDegreeDays (double BaseTemperature,  
IEnumerable<DailyTemperature> TempRecords )
    : DegreeDays (BaseTemperature, TempRecords )
{
    public double DegreeDays => TempRecords.Where(s => s.Mean >  
BaseTemperature).Sum(s => s.Mean - BaseTemperature);
}
var heatingDegreeDays = new HeatingDegreeDays( 65, data);
Console.WriteLine(heatingDegreeDays);
var coolingDegreeDays = new CoolingDegreeDays( 65, data);
Console.WriteLine(coolingDegreeDays);
HeatingDegreeDays { BaseTemperature = 65, TempRecords =  
record_types.DailyTemperature[] , DegreeDays = 85 }
CoolingDegreeDays { BaseTemperature = 65, TempRecords =  
record_types.DailyTemperature[] , DegreeDays = 71.5 }
Define compiler-synthesized methodsFor this purpose, you'll synthesize PrintMembers. You could also declare your own
ToString, but PrintMembers provides a better option for inheritance scenarios. T o
provide your own version of a synthesized method, the signature must match the
synthesized method.
The TempRecords element in the console output isn't useful. It displays the type, but
nothing else. Y ou can change this behavior by providing your own implementation of
the synthesized PrintMembers method. The signature depends on modifiers applied to
the record declaration:
If a record type is sealed, or a record struct, the signature is private bool
PrintMembers(StringBuilder builder);
If a record type isn't sealed and derives from object (that is, it doesn't declare a
base record), the signature is protected virtual bool PrintMembers(StringBuilder
builder);
If a record type isn't sealed and derives from another record, the signature is
protected override bool PrintMembers(StringBuilder builder);
These rules are easiest to comprehend through understanding the purpose of
PrintMembers. PrintMembers adds information about each property in a record type to a
string. The contract requires base records to add their members to the display and
assumes derived members will add their members. Each record type synthesizes a
ToString override that looks similar to the following example for HeatingDegreeDays:
C#
You declare a PrintMembers method in the DegreeDays record that doesn't print the type
of the collection:
C#public override  string ToString ()
{
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.Append( "HeatingDegreeDays" );
    stringBuilder.Append( " { ");
    if (PrintMembers(stringBuilder))
    {
        stringBuilder.Append( " ");
    }
    stringBuilder.Append( "}");
    return stringBuilder.ToString();
}The signature declares a virtual protected method to match the compiler's version.
Don't worry if you get the accessors wrong; the language enforces the correct signature.
If you forget the correct modifiers for any synthesized method, the compiler issues
warnings or errors that help you get the right signature.
In C# 10 and later, you can declare the ToString method as sealed in a record type.
That prevents derived records from providing a new implementation. Derived records
will still contain the PrintMembers override. Y ou would seal ToString if you didn't want it
to display the runtime type of the record. In the preceding example, you'd lose the
information on where the record was measuring heating or cooling degree days.
The synthesized members in a positional record class don't modify the state of the
record. The goal is that you can more easily create immutable records. R emember that
you declare a readonly record struct to create an immutable record struct. Look again
at the preceding declarations for HeatingDegreeDays and CoolingDegreeDays. The
members added perform computations on the values for the record, but don't mutate
state. P ositional records make it easier for you to create immutable reference types.
Creating immutable reference types means you'll want to use non-destructive mutation.
You create new record instances that are similar to existing record instances using with
expressions . These expressions are a copy construction with additional assignments that
modify the copy. The result is a new record instance where each property has been
copied from the existing record and optionally modified. The original record is
unchanged.
Let's add a couple features to your program that demonstrate with expressions. First,
let's create a new record to compute growing degree days using the same data.
Growing degr ee days  typically uses 41F as the baseline and measures temperatures
above the baseline. T o use the same data, you can create a new record that is similar to
the coolingDegreeDays, but with a different base temperature:
C#protected  virtual bool PrintMembers (StringBuilder stringBuilder )
{
    stringBuilder.Append( $"BaseTemperature = {BaseTemperature} ");
    return true;
}
Non-destructive mutationYou can compare the number of degrees computed to the numbers generated with a
higher baseline temperature. R emember that records are reference types  and these
copies are shallow copies. The array for the data isn't copied, but both records refer to
the same data. That fact is an advantage in one other scenario. For growing degree
days, it's useful to keep track of the total for the previous five days. Y ou can create new
records with different source data using with expressions. The following code builds a
collection of these accumulations, then displays the values:
C#
You can also use with expressions to create copies of records. Don't specify any
properties between the braces for the with expression. That means create a copy, and
don't change any properties:
C#
Run the finished application to see the results.
This tutorial showed several aspects of records. R ecords provide concise syntax for types
where the fundamental use is storing data. For object-oriented classes, the fundamental// Growing degree days measure warming to determine plant growing rates
var growingDegreeDays = coolingDegreeDays with { BaseTemperature = 41 };
Console.WriteLine(growingDegreeDays);
// showing moving accumulation of 5 days using range syntax
List<CoolingDegreeDays> movingAccumulation = new();
int rangeSize = (data.Length > 5) ? 5 : data.Length;
for (int start = 0; start < data.Length - rangeSize; start++)
{
    var fiveDayTotal = growingDegreeDays with { TempRecords = data[start..
(start + rangeSize)] };
    movingAccumulation.Add(fiveDayTotal);
}
Console.WriteLine();
Console.WriteLine( "Total degree days in the last five days" );
foreach(var item in movingAccumulation)
{
    Console.WriteLine(item);
}
var growingDegreeDaysCopy = growingDegreeDays with { };
Summaryuse is defining responsibilities. This tutorial focused on positional r ecords, where you can
use a concise syntax to declare the properties for a record. The compiler synthesizes
several members of the record for copying and comparing records. Y ou can add any
other members you need for your record types. Y ou can create immutable record types
knowing that none of the compiler-generated members would mutate state. And with
expressions make it easy to support non-destructive mutation.
Records add another way to define types. Y ou use class definitions to create object-
oriented hierarchies that focus on the responsibilities and behavior of objects. Y ou
create struct types for data structures that store data and are small enough to copy
efficiently. Y ou create record types when you want value-based equality and
comparison, don't want to copy values, and want to use reference variables. Y ou create
record struct types when you want the features of records for a type that is small
enough to copy efficiently.
You can learn more about records in the C# language reference article for the record
type and the proposed record type specification  and record struct specification .
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
 Provide product feedbackTutorial: Explore ideas using top-level
statemen ts to build code as you learn
Article •11/14/2023
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET 6, which includes the C# 10 compiler. The
C# 10 compiler is available starting with Visual S tudio 2022  or .NET 6 SDK .
This tutorial assumes you're familiar with C# and .NET, including either Visual S tudio or
the .NET CLI.
Top-level statements enable you to avoid the extra ceremony required by placing your
program's entry point in a static method in a class. The typical starting point for a new
console application looks like the following code:
C#
The preceding code is the result of running the dotnet new console command and
creating a new console application. Those 11 lines contain only one line of executableLearn the rules governing your use of top-level statements.＂
Use top-level statements to explore algorithms.＂
Refactor explorations into reusable components.＂
Prerequisites
Start exploring
using System;
namespace  Application
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine( "Hello World!" );
        }
    }
}code. Y ou can simplify that program with the new top-level statements feature. That
enables you to remove all but two of the lines in this program:
C#
This feature simplifies what's needed to begin exploring new ideas. Y ou can use top-
level statements for scripting scenarios, or to explore. Once you've got the basics
working, you can start refactoring the code and create methods, classes, or other
assemblies for reusable components you've built. T op-level statements do enable quick
experimentation and beginner tutorials. They also provide a smooth path from
experimentation to full programs.
Top-level statements are executed in the order they appear in the file. T op-level
statements can only be used in one source file in your application. The compiler
generates an error if you use them in more than one file.
For this tutorial, let's build a console application that answers a "yes" or "no" question
with a random answer. Y ou'll build out the functionality step by step. Y ou can focus on// See https://aka.ms/new-console-template for more information
Console.WriteLine( "Hello, World!" );
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
Build a magic .NET answer machineyour task rather than ceremony needed for the structure of a typical program. Then,
once you're happy with the functionality, you can refactor the application as you see fit.
A good starting point is to write the question back to the console. Y ou can start by
writing the following code:
C#
You don't declare an args variable. For the single source file that contains your top-level
statements, the compiler recognizes args to mean the command-line arguments. The
type of args is a string[], as in all C# programs.
You can test your code by running the following dotnet run command:
.NET CLI
The arguments after the -- on the command line are passed to the program. Y ou can
see the type of the args variable, because that's what's printed to the console:
Console
To write the question to the console, you'll need to enumerate the arguments and
separate them with a space. R eplace the WriteLine call with the following code:
C#
Now, when you run the program, it will correctly display the question as a string of
arguments.Console.WriteLine(args);
dotnet run -- Should I use top level statements in all my programs?
System.String[]
Console.WriteLine();
foreach(var s in args)
{
    Console.Write(s);
    Console.Write( ' ');
}
Console.WriteLine();After echoing the question, you can add the code to generate the random answer. S tart
by adding an array of possible answers:
C#
This array has ten answers that are affirmative, five that are non-committal, and five that
are negative. Next, add the following code to generate and display a random answer
from the array:
C#
You can run the application again to see the results. Y ou should see something like the
following output:
.NET CLI
This code answers the questions, but let's add one more feature. Y ou'd like your
question app to simulate thinking about the answer. Y ou can do that by adding a bit ofRespond with a random answer
string[] answers =
[
    "It is certain." ,       "Reply hazy, try again." ,     "Don’t count on  
it.",
    "It is decidedly so." ,  "Ask again later." ,           "My reply is no." ,
    "Without a doubt." ,     "Better not tell you now." ,   "My sources say  
no.",
    "Yes – definitely." ,    "Cannot predict now." ,        "Outlook not so  
good.",
    "You may rely on it." ,  "Concentrate and ask again." , "Very doubtful." ,
    "As I see it, yes." ,
    "Most likely." ,
    "Outlook good." ,
    "Yes.",
    "Signs point to yes." ,
];
var index = new Random().Next(answers.Length - 1);
Console.WriteLine(answers[index]);
dotnet run -- Should I use top level statements in all my programs?
Should I use top level statements in all my programs?
Better not tell you now.ASCII animation, and pausing while working. Add the following code after the line that
echoes the question:
C#
You'll also need to add a using statement to the top of the source file:
C#
The using statements must be before any other statements in the file. Otherwise, it's a
compiler error. Y ou can run the program again and see the animation. That makes a
better experience. Experiment with the length of the delay to match your taste.
The preceding code creates a set of spinning lines separated by a space. Adding the
await keyword instructs the compiler to generate the program entry point as a method
that has the async modifier, and returns a System.Threading.T asks.T ask. This program
doesn't return a value, so the program entry point returns a Task. If your program
returns an integer value, you would add a return statement to the end of your top-level
statements. That return statement would specify the integer value to return. If your top-
level statements include an await expression, the return type becomes
System.Threading.T asks.T ask<TR esult> .
Your program should look like the following code:for (int i = 0; i < 20; i++)
{
    Console.Write( "| -");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "/ \\");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "- |");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "\\ /");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
}
Console.WriteLine();
using System.Threading.Tasks;
Refactoring for the futureC#
The preceding code is reasonable. It works. But it isn't reusable. Now that you have the
application working, it's time to pull out reusable parts.
One candidate is the code that displays the waiting animation. That snippet can become
a method:Console.WriteLine();
foreach(var s in args)
{
    Console.Write(s);
    Console.Write( ' ');
}
Console.WriteLine();
for (int i = 0; i < 20; i++)
{
    Console.Write( "| -");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "/ \\");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "- |");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
    Console.Write( "\\ /");
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
}
Console.WriteLine();
string[] answers =
[
    "It is certain." ,       "Reply hazy, try again." ,     "Don't count on  
it.",
    "It is decidedly so." ,  "Ask again later." ,           "My reply is no." ,
    "Without a doubt." ,     "Better not tell you now." ,   "My sources say  
no.",
    "Yes – definitely." ,    "Cannot predict now." ,        "Outlook not so  
good.",
    "You may rely on it." ,  "Concentrate and ask again." , "Very doubtful." ,
    "As I see it, yes." ,
    "Most likely." ,
    "Outlook good." ,
    "Yes.",
    "Signs point to yes." ,
];
var index = new Random().Next(answers.Length - 1);
Console.WriteLine(answers[index]);You can start by creating a local function in your file. R eplace the current animation with
the following code:
C#
The preceding code creates a local function inside your main method. That's still not
reusable. So, extract that code into a class. Create a new file named utilities.cs  and add
the following code:
C#await ShowConsoleAnimation();
static async Task ShowConsoleAnimation ()
{
    for (int i = 0; i < 20; i++)
    {
        Console.Write( "| -");
        await Task.Delay( 50);
        Console.Write( "\b\b\b" );
        Console.Write( "/ \\");
        await Task.Delay( 50);
        Console.Write( "\b\b\b" );
        Console.Write( "- |");
        await Task.Delay( 50);
        Console.Write( "\b\b\b" );
        Console.Write( "\\ /");
        await Task.Delay( 50);
        Console.Write( "\b\b\b" );
    }
    Console.WriteLine();
}
namespace  MyNamespace
{
    public static class Utilities
    {
        public static async Task ShowConsoleAnimation ()
        {
            for (int i = 0; i < 20; i++)
            {
                Console.Write( "| -");
                await Task.Delay( 50);
                Console.Write( "\b\b\b" );
                Console.Write( "/ \\");
                await Task.Delay( 50);
                Console.Write( "\b\b\b" );
                Console.Write( "- |");
                await Task.Delay( 50);
                Console.Write( "\b\b\b" );
                Console.Write( "\\ /");A file that has top-level statements can also contain namespaces and types at the end of
the file, after the top-level statements. But for this tutorial you put the animation
method in a separate file to make it more readily reusable.
Finally, you can clean the animation code to remove some duplication:
C#
Now you have a complete application, and you've refactored the reusable parts for later
use. Y ou can call the new utility method from your top-level statements, as shown below
in the finished version of the main program:
C#                await Task.Delay( 50);
                Console.Write( "\b\b\b" );
            }
            Console.WriteLine();
        }
    }
}
foreach (string s in animations)
{
    Console.Write(s);
    await Task.Delay( 50);
    Console.Write( "\b\b\b" );
}
using MyNamespace;
Console.WriteLine();
foreach(var s in args)
{
    Console.Write(s);
    Console.Write( ' ');
}
Console.WriteLine();
await Utilities.ShowConsoleAnimation();
string[] answers =
[
    "It is certain." ,       "Reply hazy, try again." ,     "Don’t count on  
it.",
    "It is decidedly so." ,  "Ask again later." ,           "My reply is no." ,
    "Without a doubt." ,     "Better not tell you now." ,   "My sources say  
no.",
    "Yes – definitely." ,    "Cannot predict now." ,        "Outlook not so  
good.",The preceding example adds the call to Utilities.ShowConsoleAnimation, and adds an
additional using statement.
Top-level statements make it easier to create simple programs for use to explore new
algorithms. Y ou can experiment with algorithms by trying different snippets of code.
Once you've learned what works, you can refactor the code to be more maintainable.
Top-level statements simplify programs that are based on console applications. These
include Azure functions, GitHub actions, and other small utilities. For more information,
see Top-level statements (C# Programming Guide) .    "You may rely on it." ,  "Concentrate and ask again." , "Very doubtful." ,
    "As I see it, yes." ,
    "Most likely." ,
    "Outlook good." ,
    "Yes.",
    "Signs point to yes." ,
];
var index = new Random().Next(answers.Length - 1);
Console.WriteLine(answers[index]);
Summary
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
 Provide product feedbackIndices and ranges
Article •11/14/2023
Ranges and indices provide a succinct syntax for accessing single elements or ranges in
a sequence.
In this tutorial, you'll learn how to:
Indices and ranges provide a succinct syntax for accessing single elements or ranges in a
sequence.
This language support relies on two new types and two new operators:
System.Index  represents an index into a sequence.
The index from end operator ^, which specifies that an index is relative to the end
of a sequence.
System.Range  represents a sub range of a sequence.
The range operator .., which specifies the start and end of a range as its operands.
Let's start with the rules for indices. Consider an array sequence. The 0 index is the same
as sequence[0]. The ^0 index is the same as sequence[sequence.Length]. The expression
sequence[^0] does throw an exception, just as sequence[sequence.Length] does. For any
number n, the index ^n is the same as sequence.Length - n.
C#Use the syntax for ranges in a sequence.＂
Implicitly define a Range . ＂
Understand the design decisions for the start and end of each sequence.＂
Learn scenarios for the Index  and Range  types. ＂
Language support for indices and ranges
string[] words = [
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumps",    // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2You can retrieve the last word with the ^1 index. Add the following code below the
initialization:
C#
A range specifies the start and end of a range. The start of the range is inclusive, but the
end of the range is exclusive, meaning the start is included in the range but the end isn't
included in the range. The range [0..^0] represents the entire range, just as
[0..sequence.Length] represents the entire range.
The following code creates a subrange with the words "quick", "brown", and "fox". It
includes words[1] through words[3]. The element words[4] isn't in the range.
C#
The following code returns the range with "lazy" and "dog". It includes words[^2] and
words[^1]. The end index words[^0] isn't included. Add the following code as well:
C#
The following examples create ranges that are open ended for the start, end, or both:
C#    "dog"       // 8                   ^1
];              // 9 (or words.Length) ^0
Console.WriteLine( $"The last word is {words[^ 1]}");
string[] quickBrownFox = words[ 1..4];
foreach (var word in quickBrownFox)
    Console.Write( $"< {word} >");
Console.WriteLine();
string[] lazyDog = words[^ 2..^0];
foreach (var word in lazyDog)
    Console.Write( $"< {word} >");
Console.WriteLine();
string[] allWords = words[..]; // contains "The" through "dog".
string[] firstPhrase = words[. .4]; // contains "The" through "fox"
string[] lastPhrase = words[ 6..]; // contains "the", "lazy" and "dog"
foreach (var word in allWords)
    Console.Write( $"< {word} >");
Console.WriteLine();
foreach (var word in firstPhrase)You can also declare ranges or indices as variables. The variable can then be used inside
the [ and ] characters:
C#
The following sample shows many of the reasons for those choices. Modify x, y, and z
to try different combinations. When you experiment, use values where x is less than y,
and y is less than z for valid combinations. Add the following code in a new method.
Try different combinations:
C#    Console.Write( $"< {word} >");
Console.WriteLine();
foreach (var word in lastPhrase)
    Console.Write( $"< {word} >");
Console.WriteLine();
Index the = ^ 3;
Console.WriteLine(words[the]);
Range phrase = 1..4;
string[] text = words[phrase];
foreach (var word in text)
    Console.Write( $"< {word} >");
Console.WriteLine();
int[] numbers = [..Enumerable.Range( 0, 100)];
int x = 12;
int y = 25;
int z = 36;
Console.WriteLine( $"{numbers[^x]}  is the same as {numbers[numbers.Length -  
x]}");
Console.WriteLine( $"{numbers[x..y].Length}  is the same as {y - x}");
Console.WriteLine( "numbers[x..y] and numbers[y..z] are consecutive and  
disjoint:" );
Span<int> x_y = numbers[x..y];
Span<int> y_z = numbers[y..z];
Console.WriteLine( $"\tnumbers[x..y] is {x_y[0]} through {x_y[^1]}, 
numbers[y..z] is {y_z[0]} through {y_z[^1]}");
Console.WriteLine( "numbers[x..^x] removes x elements at each end:" );
Span<int> x_x = numbers[x..^x];
Console.WriteLine( $"\tnumbers[x..^x] starts with {x_x[0]} and ends with 
{x_x[^1]}");
Console.WriteLine( "numbers[..x] means numbers[0..x] and numbers[x..] means  
numbers[x..^0]" );
Span<int> start_x = numbers[..x];Not only arrays support indices and ranges. Y ou can also use indices and ranges with
string , Span<T> , or ReadOnlySpan<T> .
When using the range operator expression syntax, the compiler implicitly converts the
start and end values to an Index  and from them, creates a new Range  instance. The
following code shows an example implicit conversion from the range operator
expression syntax, and its corresponding explicit alternative:
C#Span<int> zero_x = numbers[ 0..x];
Console.WriteLine( $"\t{start_x[ 0]}..{start_x[^ 1]} is the same as 
{zero_x[ 0]}..{zero_x[^ 1]}");
Span<int> z_end = numbers[z..];
Span<int> z_zero = numbers[z..^ 0];
Console.WriteLine( $"\t{z_end[0]}..{z_end[^ 1]} is the same as {z_zero[ 0]}..
{z_zero[^ 1]}");
Implicit range operator expression conversions
Range implicitRange = 3..^5;
Range explicitRange = new(
    start: new Index(value: 3, fromEnd: false),
    end: new Index(value: 5, fromEnd: true));
if (implicitRange.Equals(explicitRange))
{
    Console.WriteLine(
        $"The implicit range ' {implicitRange} ' equals the explicit range  
'{explicitRange} '");
}
// Sample output:
//     The implicit range '3..^5' equals the explicit range '3..^5'
） Impor tant
Implicit conversions from Int32  to Index  throw an ArgumentOutOfRangeEx ception
when the value is negative. Likewise, the Index constructor throws an
ArgumentOutOfRangeException when the value parameter is negative.
Type support for indic es and rangesIndexes and ranges provide clear, concise syntax to access a single element or a range
of elements in a sequence. An index expression typically returns the type of the
elements of a sequence. A range expression typically returns the same sequence type as
the source sequence.
Any type that provides an indexer  with an Index  or Range  parameter explicitly supports
indices or ranges respectively. An indexer that takes a single Range  parameter may
return a different sequence type, such as System.Span<T> .
A type is countable  if it has a property named Length or Count with an accessible getter
and a return type of int. A countable type that doesn't explicitly support indices or
ranges may provide an implicit support for them. For more information, see the Implicit
Index support  and Implicit Range support  sections of the feature proposal note . Ranges
using implicit range support return the same sequence type as the source sequence.
For example, the following .NET types support both indices and ranges: String ,
Span<T> , and ReadOnlySpan<T> . The List<T>  supports indices but doesn't support
ranges.
Array  has more nuanced behavior. Single dimension arrays support both indices and
ranges. Multi-dimensional arrays don't support indexers or ranges. The indexer for a
multi-dimensional array has multiple parameters, not a single parameter. Jagged arrays,
also referred to as an array of arrays, support both ranges and indexers. The following
example shows how to iterate a rectangular subsection of a jagged array. It iterates the） Impor tant
The performance of code using the range operator depends on the type of the
sequence operand.
The time complexity of the range operator depends on the sequence type. For
example, if the sequence is a string or an array, then the result is a copy of the
specified section of the input, so the time complexity is O(N)  (where N is the length
of the range). On the other hand, if it's a System.Sp an<T>  or a
System.Memor y<T> , the result references the same backing store, which means
there is no copy and the operation is O(1).
In addition to the time complexity, this causes extra allocations and copies,
impacting performance. In performance sensitive code, consider using Span<T> or
Memory<T> as the sequence type, since the range operator does not allocate for
them.section in the center, excluding the first and last three rows, and the first and last two
columns from each selected row:
C#
In all cases, the range operator for Array  allocates an array to store the elements
returned.
You'll often use ranges and indices when you want to analyze a portion of a larger
sequence. The new syntax is clearer in reading exactly what portion of the sequence is
involved. The local function MovingAverage takes a Range  as its argument. The method
then enumerates just that range when calculating the min, max, and average. T ry the
following code in your project:
C#int[][] jagged = 
[
   [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
   [10,11,12,13,14,15,16,17,18,19],
   [20,21,22,23,24,25,26,27,28,29],
   [30,31,32,33,34,35,36,37,38,39],
   [40,41,42,43,44,45,46,47,48,49],
