ate types can also be generic. When the generic class is used, type
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
