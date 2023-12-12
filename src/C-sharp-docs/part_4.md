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
Console.WriteLine(e.Evaluate(vars)); /