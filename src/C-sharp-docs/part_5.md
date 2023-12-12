/ "16.5"
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
When an expression contains multiple operat