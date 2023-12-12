.
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
interface, and deleg