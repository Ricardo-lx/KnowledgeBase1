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
and specialize base classes