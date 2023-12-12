        if (type.Name != "var") 
        {  
            // Create a new TypeSyntax for the inferred type. Be careful  
            // to keep any leading and trailing trivia from the var keyword.  
            TypeSyntax typeName =  
SyntaxFactory.ParseTypeName(type.ToDisplayString())  
                .WithLeadingTrivia(variableTypeName.GetLeadingTrivia())  
                .WithTrailingTrivia(variableTypeName.GetTrailingTrivia());  
            // Add an annotation to simplify the type name.  
            TypeSyntax simplifiedTypeName =  You'll need to add one using directive to use the Simplifier  type:
C#
Run your tests, and they should all pass. Congratulate yourself by running your finished
analyzer. Press Ctrl+F5 to run the analyzer project in a second instance of Visual
Studio with the R oslyn Preview extension loaded.
In the second Visual S tudio instance, create a new C# Console Application project
and add int x = "abc"; to the Main method. Thanks to the first bug fix, no
warning should be reported for this local variable declaration (though there's a
compiler error as expected).
Next, add object s = "abc"; to the Main method. Because of the second bug fix,
no warning should be reported.
Finally, add another local variable that uses the var keyword. Y ou'll see that a
warning is reported and a suggestion appears beneath to the left.
Move the editor caret over the squiggly underline and press Ctrl+.. to display
the suggested code fix. Upon selecting your code fix, note that the var keyword is
now handled correctly.
Finally, add the following code:
C#
After these changes, you get red squiggles only on the first two variables. Add const to
both i and j, and you get a new warning on k because it can now be const.typeName.WithAdditionalAnnotations(Simplifier.Annotation);  
            // Replace the type in the variable declaration.  
            variableDeclaration =  
variableDeclaration.WithType(simplifiedTypeName);  
        }  
    } 
} 
// Produce the new local declaration.  
LocalDeclarationStatementSyntax newLocal =  
trimmedLocal.WithModifiers(newModifiers)  
                           .WithDeclaration(variableDeclaration);  
using Microsoft.CodeAnalysis.Simplification;  
int i = 2; 
int j = 32; 
int k = i + j;  Congratulations! Y ou've created your first .NET Compiler Platform extension that
performs on-the-fly code analysis to detect an issue and provides a quick fix to correct
it. Along the way, you've learned many of the code APIs that are part of the .NET
Compiler Platform SDK (R oslyn APIs). Y ou can check your work against the completed
sample  in our samples GitHub repository.
Get started with syntax analysis
Get started with semantic analysis
Other resourcesC# programming guide
Article •09/01/2023
This section provides detailed information on key C# language features and features
accessible to C# through .NET.
Most of this section assumes that you already know something about C# and general
programming concepts. If you are a complete beginner with programming or with C#,
you might want to visit the Introduction to C# Tutorials  or .NET In-Browser Tutorial ,
where no prior programming knowledge is required.
For information about specific keywords, operators, and preprocessor directives, see C#
Reference . For information about the C# Language Specification, see C# Language
Specification .
Programming concepts
Statements
Expression-bodied members
Equality Comparisons
Types
Classes, structs, and records
Interfaces
Delegates
Strings
Properties
Indexers
Events
Generics
Iterators
Language SectionsApplication Domains
Assemblies in .NET
Exceptions and Exception Handling
C# ReferencePlatform Sections
See alsoProgramming Concepts (C#)
Article •09/01/2023
This section explains programming concepts in the C# language.
Title Descr iption
methods, and properties
by using attributes.
Covariance and
Contravariance (C#)Shows how to enable implicit conversion of generic type parameters
in interfaces and delegates.
Iterators (C#) Describes iterators, which are used to step through collections and
return elements one at a time.
Language-Integrated
Query (LINQ) (C#)Discusses the powerful query capabilities in the language syntax of
C#, and the model for querying relational databases, XML documents,
datasets, and in-memory collections.
Performance Tips
Discusses several basic rules that may help you increase the performance of your
application.In This Section
Related SectionsCovariance and Contravariance (C#)
Article •07/30/2022
In C#, covariance and contravariance enable implicit reference conversion for array
types, delegate types, and generic type arguments. Covariance preserves assignment
compatibility and contravariance reverses it.
The following code demonstrates the difference between assignment compatibility,
covariance, and contravariance.
C#
Covariance for arrays enables implicit conversion of an array of a more derived type to
an array of a less derived type. But this operation is not type safe, as shown in the
following code example.
C#
Covariance and contravariance support for method groups allows for matching method
signatures with delegate types. This enables you to assign to delegates not only// Assignment compatibility.  
string str = "test";   
// An object of a more derived type is assigned to an object of a less  
derived type.  
object obj = str;   
   
// Covariance.  
IEnumerable< string> strings = new List<string>();   
// An object that is instantiated with a more derived type argument  
// is assigned to an object instantiated with a less derived type argument.  
// Assignment compatibility is preserved.  
IEnumerable< object> objects = strings;   
   
// Contravariance.  
// Assume that the following method is in the class:  
static void SetObject (object o) { } 
Action<object> actObject = SetObject;   
// An object that is instantiated with a less derived type argument  
// is assigned to an object instantiated with a more derived type argument.  
// Assignment compatibility is reversed.  
Action<string> actString = actObject;   
object[] array = new String[ 10];   
// The following statement produces a run-time exception.   
// array[0] = 10;   methods that have matching signatures, but also methods that return more derived
types (covariance) or that accept parameters that have less derived types
(contravariance) than that specified by the delegate type. For more information, see
Variance in Delegates (C#)  and Using V ariance in Delegates (C#) .
The following code example shows covariance and contravariance support for method
groups.
C#
In .NET Framework 4 and later versions, C# supports covariance and contravariance in
generic interfaces and delegates and allows for implicit conversion of generic type
parameters. For more information, see Variance in Generic Interfaces (C#)  and Variance
in Delegates (C#) .
The following code example shows implicit reference conversion for generic interfaces.
C#
A generic interface or delegate is called variant if its generic parameters are declared
covariant or contravariant. C# enables you to create your own variant interfaces and
delegates. For more information, see Creating V ariant Generic Interfaces (C#)  and
Variance in Delegates (C#) .static object GetObject () { return null; }   
static void SetObject (object obj) { }   
   
static string GetString () { return ""; }   
static void SetString (string str) { }   
   
static void Test()   
{   
    // Covariance. A delegate specifies a return type as object,  
    // but you can assign a method that returns a string.   
    Func< object> del = GetString;   
   
    // Contravariance. A delegate specifies a parameter type as string,   
    // but you can assign a method that takes an object.   
    Action< string> del2 = SetObject;   
}   
IEnumerable<String> strings = new List<String>();   
IEnumerable<Object> objects = strings;   
Related TopicsTitle Descr iption Title Descr iption
Variance in Generic
Interfaces (C#)Discusses covariance and contravariance in generic interfaces and
provides a list of variant generic interfaces in .NET.
Creating V ariant Generic
Interfaces (C#)Shows how to create custom variant interfaces.
Using V ariance in Interfaces
for Generic Collections (C#)Shows how covariance and contravariance support in the
IEnumerable<T>  and IComparable<T>  interfaces can help you
reuse code.
Variance in Delegates (C#) Discusses covariance and contravariance in generic and non-
generic delegates and provides a list of variant generic delegates
in .NET.
Using V ariance in Delegates
(C#)Shows how to use covariance and contravariance support in non-
generic delegates to match method signatures with delegate
types.
Using V ariance for Func and
Action Generic Delegates
(C#)Shows how covariance and contravariance support in the Func and
Action delegates can help you reuse code.Variance in Gen eric Interfaces (C#)
Article •09/15/2021
.NET Framework 4 introduced variance support for several existing generic interfaces.
Variance support enables implicit conversion of classes that implement these interfaces.
Starting with .NET Framework 4, the following interfaces are variant:
IEnumerable<T>  (T is covariant)
IEnumerator<T>  (T is covariant)
IQueryable<T>  (T is covariant)
IGrouping<TK ey,TElement>  (TKey and TElement are covariant)
IComparer<T>  (T is contravariant)
IEqualityComparer<T>  (T is contravariant)
IComparable<T>  (T is contravariant)
Starting with .NET Framework 4.5, the following interfaces are variant:
IReadOnlyList<T>  (T is covariant)
IReadOnlyCollection<T>  (T is covariant)
Covariance permits a method to have a more derived return type than that defined by
the generic type parameter of the interface. T o illustrate the covariance feature, consider
these generic interfaces: IEnumerable<Object> and IEnumerable<String>. The
IEnumerable<String> interface does not inherit the IEnumerable<Object> interface.
However, the String type does inherit the Object type, and in some cases you may
want to assign objects of these interfaces to each other. This is shown in the following
code example.
C#
In earlier versions of .NET Framework, this code causes a compilation error in C# and, if
Option Strict is on, in Visual Basic. But now you can use strings instead of objects, as
shown in the previous example, because the IEnumerable<T>  interface is covariant.IEnumerable<String> strings = new List<String>();  
IEnumerable<Object> objects = strings;  Contravariance permits a method to have argument types that are less derived than that
specified by the generic parameter of the interface. T o illustrate contravariance, assume
that you have created a BaseComparer class to compare instances of the BaseClass class.
The BaseComparer class implements the IEqualityComparer<BaseClass> interface.
Because the IEqualityComparer<T>  interface is now contravariant, you can use
BaseComparer to compare instances of classes that inherit the BaseClass class. This is
shown in the following code example.
C#
For more examples, see Using V ariance in Interfaces for Generic Collections (C#) .
Variance in generic interfaces is supported for reference types only. V alue types do not
support variance. For example, IEnumerable<int> cannot be implicitly converted to
IEnumerable<object>, because integers are represented by a value type.
C#// Simple hierarchy of classes.  
class BaseClass  { } 
class DerivedClass  : BaseClass  { } 
// Comparer class.  
class BaseComparer  : IEqualityComparer <BaseClass > 
{ 
    public int GetHashCode (BaseClass baseInstance ) 
    { 
        return baseInstance.GetHashCode();  
    } 
    public bool Equals(BaseClass x, BaseClass y ) 
    { 
        return x == y;  
    } 
} 
class Program 
{ 
    static void Test() 
    { 
        IEqualityComparer<BaseClass> baseComparer = new BaseComparer();  
        // Implicit conversion of IEqualityComparer<BaseClass> to  
        // IEqualityComparer<DerivedClass>.  
        IEqualityComparer<DerivedClass> childComparer = baseComparer;  
    } 
} 
IEnumerable< int> integers = new List<int>(); 
// The following statement generates a compiler error,  It is also important to remember that classes that implement variant interfaces are still
invariant. For example, although List<T>  implements the covariant interface
IEnumerable<T> , you cannot implicitly convert List<String> to List<Object>. This is
illustrated in the following code example.
C#
Using V ariance in Interfaces for Generic Collections (C#)
Creating V ariant Generic Interfaces (C#)
Generic Interfaces
Variance in Delegates (C#)// because int is a value type.  
// IEnumerable<Object> objects = integers;  
// The following line generates a compiler error  
// because classes are invariant.
// List<Object> list = new List<String>();  
// You can use the interface object instead.  
IEnumerable<Object> listObjects = new List<String>();  
See alsoCreating Variant Generic Interfaces (C#)
Article •09/15/2021
You can declare generic type parameters in interfaces as covariant or contravariant.
Covariance allows interface methods to have more derived return types than that
defined by the generic type parameters. Contravariance allows interface methods to
have argument types that are less derived than that specified by the generic parameters.
A generic interface that has covariant or contravariant generic type parameters is called
variant.
You can declare variant generic interfaces by using the in and out keywords for generic
type parameters.
You can declare a generic type parameter covariant by using the out keyword. The
covariant type must satisfy the following conditions:
The type is used only as a return type of interface methods and not used as a type
of method arguments. This is illustrated in the following example, in which the type
R is declared covariant.
C#７ Note
.NET Framework 4 introduced variance support for several existing generic
interfaces. For the list of the variant interfaces in .NET, see Variance in Generic
Interfaces (C#) .
Declaring Variant Generic Interfaces
） Impor tant
ref, in, and out parameters in C# cannot be variant. V alue types also do not
support variance.
interface  ICovariant <out R> 
{ 
    R GetSomething (); 
    // The following statement generates a compiler error.  
    // void SetSomething(R sampleArg);  There is one exception to this rule. If you have a contravariant generic delegate as
a method parameter, you can use the type as a generic type parameter for the
delegate. This is illustrated by the type R in the following example. For more
information, see Variance in Delegates (C#)  and Using V ariance for Func and Action
Generic Delegates (C#) .
C#
The type is not used as a generic constraint for the interface methods. This is
illustrated in the following code.
C#
You can declare a generic type parameter contravariant by using the in keyword. The
contravariant type can be used only as a type of method arguments and not as a return
type of interface methods. The contravariant type can also be used for generic
constraints. The following code shows how to declare a contravariant interface and use a
generic constraint for one of its methods.
C#} 
interface  ICovariant <out R> 
{ 
    void DoSomething (Action<R> callback ); 
} 
interface  ICovariant <out R> 
{ 
    // The following statement generates a compiler error  
    // because you can use only contravariant or invariant types  
    // in generic constraints.  
    // void DoSomething<T>() where T : R;  
} 
interface  IContravariant <in A> 
{ 
    void SetSomething (A sampleArg ); 
    void DoSomething<T>() where T : A; 
    // The following statement generates a compiler error.  
    // A GetSomething();  
} It is also possible to support both covariance and contravariance in the same interface,
but for different type parameters, as shown in the following code example.
C#
You implement variant generic interfaces in classes by using the same syntax that is
used for invariant interfaces. The following code example shows how to implement a
covariant interface in a generic class.
C#
Classes that implement variant interfaces are invariant. For example, consider the
following code.
C#interface  IVariant <out R, in A> 
{ 
    R GetSomething (); 
    void SetSomething (A sampleArg ); 
    R GetSetSomethings (A sampleArg ); 
} 
Implementing  Variant Generic Interfaces
interface  ICovariant <out R> 
{ 
    R GetSomething (); 
} 
class SampleImplementation <R> : ICovariant <R> 
{ 
    public R GetSomething () 
    { 
        // Some code.  
        return default(R); 
    } 
} 
// The interface is covariant.  
ICovariant<Button> ibutton = new SampleImplementation<Button>();  
ICovariant<Object> iobj = ibutton;  
// The class is invariant.  
SampleImplementation<Button> button = new SampleImplementation<Button>();  
// The following statement generates a compiler error  
// because classes are invariant.
// SampleImplementation<Object> obj = button;  When you extend a variant generic interface, you have to use the in and out keywords
to explicitly specify whether the derived interface supports variance. The compiler does
not infer the variance from the interface that is being extended. For example, consider
the following interfaces.
C#
In the IInvariant<T> interface, the generic type parameter T is invariant, whereas in
IExtCovariant<out T> the type parameter is covariant, although both interfaces extend
the same interface. The same rule is applied to contravariant generic type parameters.
You can create an interface that extends both the interface where the generic type
parameter T is covariant and the interface where it is contravariant if in the extending
interface the generic type parameter T is invariant. This is illustrated in the following
code example.
C#
However, if a generic type parameter T is declared covariant in one interface, you
cannot declare it contravariant in the extending interface, or vice versa. This is illustrated
in the following code example.
C#
When you implement variant generic interfaces, variance can sometimes lead to
ambiguity. Such ambiguity should be avoided.Extending Variant Generic Interfaces
interface  ICovariant <out T> { } 
interface  IInvariant <T> : ICovariant <T> { } 
interface  IExtCovariant <out T> : ICovariant <T> { } 
interface  ICovariant <out T> { } 
interface  IContravariant <in T> { } 
interface  IInvariant <T> : ICovariant <T>, IContravariant <T> { } 
interface  ICovariant <out T> { } 
// The following statement generates a compiler error.  
// interface ICoContraVariant<in T> : ICovariant<T> { }  
Avoiding AmbiguityFor example, if you explicitly implement the same variant generic interface with different
generic type parameters in one class, it can create ambiguity. The compiler does not
produce an error in this case, but it's not specified which interface implementation will
be chosen at run time. This ambiguity could lead to subtle bugs in your code. Consider
the following code example.
C#
In this example, it is unspecified how the pets.GetEnumerator method chooses between
Cat and Dog. This could cause problems in your code.// Simple class hierarchy.  
class Animal { } 
class Cat : Animal { } 
class Dog : Animal { } 
// This class introduces ambiguity  
// because IEnumerable<out T> is covariant.  
class Pets : IEnumerable <Cat>, IEnumerable <Dog> 
{ 
    IEnumerator<Cat> IEnumerable<Cat>.GetEnumerator()  
    { 
        Console.WriteLine( "Cat");
        // Some code.  
        return null; 
    } 
    IEnumerator IEnumerable.GetEnumerator()  
    { 
        // Some code.  
        return null; 
    } 
    IEnumerator<Dog> IEnumerable<Dog>.GetEnumerator()  
    { 
        Console.WriteLine( "Dog");
        // Some code.  
        return null; 
    } 
} 
class Program 
{ 
    public static void Test() 
    { 
        IEnumerable<Animal> pets = new Pets();  
        pets.GetEnumerator();  
    } 
} Variance in Generic Interfaces (C#)
Using V ariance for Func and Action Generic Delegates (C#)See alsoUsing Variance in Interfaces for Generic
Collections (C#)
Article •09/15/2021
A covariant interface allows its methods to return more derived types than those
specified in the interface. A contravariant interface allows its methods to accept
parameters of less derived types than those specified in the interface.
In .NET Framework 4, several existing interfaces became covariant and contravariant.
These include IEnumerable<T>  and IComparable<T> . This enables you to reuse
methods that operate with generic collections of base types for collections of derived
types.
For a list of variant interfaces in .NET, see Variance in Generic Interfaces (C#) .
The following example illustrates the benefits of covariance support in the
IEnumerable<T>  interface. The PrintFullName method accepts a collection of the
IEnumerable<Person> type as a parameter. However, you can reuse it for a collection of
the IEnumerable<Employee> type because Employee inherits Person.
C#Converting Generic Collections
// Simple hierarchy of classes.  
public class Person   
{   
    public string FirstName { get; set; }   
    public string LastName { get; set; }   
}   
   
public class Employee  : Person { }   
   
class Program   
{   
    // The method has a parameter of the IEnumerable<Person> type.   
    public static void PrintFullName (IEnumerable<Person> persons )   
    {   
        foreach (Person person in persons)   
        {   
            Console.WriteLine( "Name: {0} {1}" ,   
            person.FirstName, person.LastName);   
        }   
    }   
   The following example illustrates the benefits of contravariance support in the
IEqualityComparer<T>  interface. The PersonComparer class implements the
IEqualityComparer<Person> interface. However, you can reuse this class to compare a
sequence of objects of the Employee type because Employee inherits Person.
C#    public static void Test()   
    {   
        IEnumerable<Employee> employees = new List<Employee>();   
   
        // You can pass IEnumerable<Employee>,  
        // although the method expects IEnumerable<Person>.   
   
        PrintFullName(employees);   
   
    }   
}   
Comparing Generic Collections
// Simple hierarchy of classes.  
public class Person   
{   
    public string FirstName { get; set; }   
    public string LastName { get; set; }   
}   
   
public class Employee  : Person { }   
   
// The custom comparer for the Person type   
// with standard implementations of Equals()   
// and GetHashCode() methods.   
class PersonComparer  : IEqualityComparer <Person>   
{   
    public bool Equals(Person x, Person y )   
    { 
        if (Object.ReferenceEquals(x, y)) return true;  
        if (Object.ReferenceEquals(x, null) ||   
            Object.ReferenceEquals(y, null))   
            return false; 
        return x.FirstName == y.FirstName && x.LastName == y.LastName;   
    }   
    public int GetHashCode (Person person )   
    {   
        if (Object.ReferenceEquals(person, null)) return 0;   
        int hashFirstName = person.FirstName == null   
            ? 0 : person.FirstName.GetHashCode();   
        int hashLastName = person.LastName.GetHashCode();   
        return hashFirstName ^ hashLastName;   Variance in Generic Interfaces (C#)    }   
}   
   
class Program   
{   
   
    public static void Test()   
    {   
        List<Employee> employees = new List<Employee> {   
               new Employee() {FirstName = "Michael" , LastName =  
"Alexander" },   
               new Employee() {FirstName = "Jeff", LastName = "Price"}   
            };   
   
        // You can pass PersonComparer,  
        // which implements IEqualityComparer<Person>,   
        // although the method expects IEqualityComparer<Employee>.   
   
        IEnumerable<Employee> noduplicates =   
            employees.Distinct<Employee>( new PersonComparer());   
   
        foreach (var employee in noduplicates)   
            Console.WriteLine(employee.FirstName + " " + employee.LastName);    
    }   
}   
See alsoVariance in Delegates (C#)
Article •09/15/2021
.NET Framework 3.5 introduced variance support for matching method signatures with
delegate types in all delegates in C#. This means that you can assign to delegates not
only methods that have matching signatures, but also methods that return more derived
types (covariance) or that accept parameters that have less derived types
(contravariance) than that specified by the delegate type. This includes both generic and
non-generic delegates.
For example, consider the following code, which has two classes and two delegates:
generic and non-generic.
C#
When you create delegates of the SampleDelegate or SampleGenericDelegate<A, R>
types, you can assign any one of the following methods to those delegates.
C#
The following code example illustrates the implicit conversion between the method
signature and the delegate type.public class First { }   
public class Second : First { }   
public delegate  First SampleDelegate (Second a );   
public delegate  R SampleGenericDelegate<A, R>(A a);   
// Matching signature.   
public static First ASecondRFirst (Second second )   
{ return new First(); }   
   
// The return type is more derived.   
public static Second ASecondRSecond (Second second )   
{ return new Second(); }   
   
// The argument type is less derived.   
public static First AFirstRFirst (First first )   
{ return new First(); }   
   
// The return type is more derived  
// and the argument type is less derived.   
public static Second AFirstRSecond (First first )   
{ return new Second(); }   C#
For more examples, see Using V ariance in Delegates (C#)  and Using V ariance for Func
and Action Generic Delegates (C#) .
In .NET Framework 4 or later you can enable implicit conversion between delegates, so
that generic delegates that have different types specified by generic type parameters
can be assigned to each other, if the types are inherited from each other as required by
variance.
To enable implicit conversion, you must explicitly declare generic parameters in a
delegate as covariant or contravariant by using the in or out keyword.
The following code example shows how you can create a delegate that has a covariant
generic type parameter.
C#// Assigning a method with a matching signature  
// to a non-generic delegate. No conversion is necessary.   
SampleDelegate dNonGeneric = ASecondRFirst;   
// Assigning a method with a more derived return type  
// and less derived argument type to a non-generic delegate.   
// The implicit conversion is used.   
SampleDelegate dNonGenericConversion = AFirstRSecond;   
   
// Assigning a method with a matching signature to a generic delegate.   
// No conversion is necessary.   
SampleGenericDelegate<Second, First> dGeneric = ASecondRFirst;   
// Assigning a method with a more derived return type  
// and less derived argument type to a generic delegate.   
// The implicit conversion is used.   
SampleGenericDelegate<Second, First> dGenericConversion = AFirstRSecond;   
Variance in Generic Type Parameters
// Type T is declared covariant by using the out keyword.   
public delegate  T SampleGenericDelegate < out T>();   
   
public static void Test()   
{   
    SampleGenericDelegate <String> dString = () => " ";   
   
    // You can assign delegates to each other,   
    // because the type T is declared covariant.   
    SampleGenericDelegate <Object> dObject = dString;  
}   If you use only variance support to match method signatures with delegate types and
do not use the in and out keywords, you may find that sometimes you can instantiate
delegates with identical lambda expressions or methods, but you cannot assign one
delegate to another.
In the following code example, SampleGenericDelegate<String> cannot be explicitly
converted to SampleGenericDelegate<Object>, although String inherits Object. You can
fix this problem by marking the generic parameter T with the out keyword.
C#
.NET Framework 4 introduced variance support for generic type parameters in several
existing generic delegates:
Action delegates from the System  namespace, for example, Action<T>  and
Action<T1,T2>
Func delegates from the System  namespace, for example, Func<TR esult>  and
Func<T,TR esult>
The Predicate<T>  delegate
The Comparison<T>  delegate
The Converter<TInput,T Output>  delegatepublic delegate  T SampleGenericDelegate<T>();   
   
public static void Test()   
{   
    SampleGenericDelegate<String> dString = () => " ";   
   
    // You can assign the dObject delegate   
    // to the same lambda expression as dString delegate   
    // because of the variance support for  
    // matching method signatures with delegate types.   
    SampleGenericDelegate<Object> dObject = () => " ";   
   
    // The following statement generates a compiler error   
    // because the generic type T is not marked as covariant.   
    // SampleGenericDelegate <Object> dObject = dString;   
   
}   
Generic Delegates That Have Variant Type Parameters in
.NETFor more information and examples, see Using V ariance for Func and Action Generic
Delegates (C#) .
If a generic delegate has covariant or contravariant generic type parameters, it can be
referred to as a variant gener ic delegat e.
You can declare a generic type parameter covariant in a generic delegate by using the
out keyword. The covariant type can be used only as a method return type and not as a
type of method arguments. The following code example shows how to declare a
covariant generic delegate.
C#
You can declare a generic type parameter contravariant in a generic delegate by using
the in keyword. The contravariant type can be used only as a type of method
arguments and not as a method return type. The following code example shows how to
declare a contravariant generic delegate.
C#
It is also possible to support both variance and covariance in the same delegate, but for
different type parameters. This is shown in the following example.
C#
You can instantiate and invoke variant delegates just as you instantiate and invoke
invariant delegates. In the following example, the delegate is instantiated by a lambdaDeclaring Variant Type Parameters in Generic Delegates
public delegate  R DCovariant< out R>();   
public delegate  void DContravariant< in A>(A a);   
） Impor tant
ref, in, and out parameters in C# can't be marked as variant.
public delegate  R DVariant< in A, out R>(A a);   
Instantiating and Invoking Variant Generic Delegatesexpression.
C#
Don't combine variant delegates. The Combine  method does not support variant
delegate conversion and expects delegates to be of exactly the same type. This can lead
to a run-time exception when you combine delegates either by using the Combine
method or by using the + operator, as shown in the following code example.
C#
Variance for generic type parameters is supported for reference types only. For example,
DVariant<int> can't be implicitly converted to DVariant<Object> or DVariant<long>,
because integer is a value type.
The following example demonstrates that variance in generic type parameters is not
supported for value types.
C#DVariant<String, String> dvariant = (String str) => str + " ";   
dvariant( "test");   
Combining Variant Generic Delegates
Action<object> actObj = x => Console.WriteLine( "object: {0}" , x);   
Action<string> actStr = x => Console.WriteLine( "string: {0}" , x);   
// All of the following statements throw exceptions at run time.   
// Action<string> actCombine = actStr + actObj;   
// actStr += actObj;   
// Delegate.Combine(actStr, actObj);   
Variance in Generic Type Parameters for Value
and Reference Types
// The type T is covariant.   
public delegate  T DVariant< out T>();   
   
// The type T is invariant.   
public delegate  T DInvariant<T>();   
   
public static void Test()   
{   
    int i = 0;   Generics
Using V ariance for Func and Action Generic Delegates (C#)
How to combine delegates (Multicast Delegates)    DInvariant< int> dInt = () => i;   
    DVariant< int> dVariantInt = () => i;   
   
    // All of the following statements generate a compiler error  
    // because type variance in generic parameters is not supported   
    // for value types, even if generic type parameters are declared  
variant.   
    // DInvariant<Object> dObject = dInt;   
    // DInvariant<long> dLong = dInt;   
    // DVariant<Object> dVariantObject = dVariantInt;   
    // DVariant<long> dVariantLong = dVariantInt;  
}   
See alsoUsing Variance in Delegates (C#)
Article •09/15/2021
When you assign a method to a delegate, covariance and contravariance provide
flexibility for matching a delegate type with a method signature. Covariance permits a
method to have return type that is more derived than that defined in the delegate.
Contravariance permits a method that has parameter types that are less derived than
those in the delegate type.
This example demonstrates how delegates can be used with methods that have return
types that are derived from the return type in the delegate signature. The data type
returned by DogsHandler is of type Dogs, which derives from the Mammals type that is
defined in the delegate.
C#Example 1: Covariance
Description
Code
class Mammals {}   
class Dogs : Mammals {}   
   
class Program   
{   
    // Define the delegate.   
    public delegate  Mammals HandlerMethod ();  
   
    public static Mammals MammalsHandler ()   
    {   
        return null;   
    }   
   
    public static Dogs DogsHandler ()   
    {   
        return null;   
    }   
   
    static void Test()   
    {   
        HandlerMethod handlerMammals = MammalsHandler;   
   
        // Covariance enables this assignment.   This example demonstrates how delegates can be used with methods that have
parameters whose types are base types of the delegate signature parameter type. With
contravariance, you can use one event handler instead of separate handlers. The
following example makes use of two delegates:
A KeyEventHandler  delegate that defines the signature of the Button.K eyDown
event. Its signature is:
C#
A MouseEventHandler  delegate that defines the signature of the
Button.MouseClick  event. Its signature is:
C#
The example defines an event handler with an EventArgs  parameter and uses it to
handle both the Button.KeyDown and Button.MouseClick events. It can do this because
EventArgs  is a base type of both KeyEventArgs  and MouseEventArgs .
C#        HandlerMethod handlerDogs = DogsHandler;   
    }   
}   
Example 2: Contravariance
Description
public delegate  void KeyEventHandler (object sender, KeyEventArgs e ) 
public delegate  void MouseEventHandler (object sender, MouseEventArgs e ) 
Code
// Event handler that accepts a parameter of the EventArgs type.   
private void MultiHandler (object sender, System.EventArgs e )   
{   
    label1.Text = System.DateTime.Now.ToString();   
}   
   
public Form1()   
{   Variance in Delegates (C#)
Using V ariance for Func and Action Generic Delegates (C#)    InitializeComponent();   
   
    // You can use a method that has an EventArgs parameter,   
    // although the event expects the KeyEventArgs parameter.   
    this.button1.KeyDown += this.MultiHandler;   
   
    // You can use the same method  
    // for an event that expects the MouseEventArgs parameter.   
    this.button1.MouseClick += this.MultiHandler;   
   
}   
See alsoUsing Variance for Func and Action
Generic Delegates (C#)
Article •09/15/2021
These examples demonstrate how to use covariance and contravariance in the Func and
Action generic delegates to enable reuse of methods and provide more flexibility in
your code.
For more information about covariance and contravariance, see Variance in Delegates
(C#).
The following example illustrates the benefits of covariance support in the generic Func
delegates. The FindByTitle method takes a parameter of the String type and returns
an object of the Employee type. However, you can assign this method to the
Func<String, Person> delegate because Employee inherits Person.
C#Using Delegates with Covariant Type
Parameters
// Simple hierarchy of classes.  
public class Person { }   
public class Employee  : Person { }   
class Program   
{   
    static Employee FindByTitle (String title )   
    {   
        // This is a stub for a method that returns   
        // an employee that has the specified title.   
        return new Employee();   
    }   
   
    static void Test()   
    {   
        // Create an instance of the delegate without using variance.   
        Func<String, Employee> findEmployee = FindByTitle;   
   
        // The delegate expects a method to return Person,   
        // but you can assign it a method that returns Employee.   
        Func<String, Person> findPerson = FindByTitle;   
   
        // You can also assign a delegate  
        // that returns a more derived type  
        // to a delegate that returns a less derived type.   The following example illustrates the benefits of contravariance support in the generic
Action delegates. The AddToContacts method takes a parameter of the Person type.
However, you can assign this method to the Action<Employee> delegate because
Employee inherits Person.
C#
Covariance and Contravariance (C#)        findPerson = findEmployee;   
   
    }   
}   
Using Delegates with Contravariant Type
Parameters
public class Person { }   
public class Employee  : Person { }   
class Program   
{   
    static void AddToContacts (Person person )  
    {   
        // This method adds a Person object   
        // to a contact list.   
    }   
   
    static void Test()   
    {   
        // Create an instance of the delegate without using variance.   
        Action<Person> addPersonToContacts = AddToContacts;   
   
        // The Action delegate expects  
        // a method that has an Employee parameter,   
        // but you can assign it a method that has a Person parameter   
        // because Employee derives from Person.   
        Action<Employee> addEmployeeToContacts = AddToContacts;   
   
        // You can also assign a delegate  
        // that accepts a less derived parameter to a delegate  
        // that accepts a more derived parameter.   
        addEmployeeToContacts = addPersonToContacts;   
    }   
}   
See alsoGenericsIterators (C#)
Article •04/12/2023
An iterator can be used to step through collections such as lists and arrays.
An iterator method or get accessor performs a custom iteration over a collection. An
iterator method uses the yield return  statement to return each element one at a time.
When a yield return statement is reached, the current location in code is remembered.
Execution is restarted from that location the next time the iterator function is called.
You consume an iterator from client code by using a foreach  statement or by using a
LINQ query.
In the following example, the first iteration of the foreach loop causes execution to
proceed in the SomeNumbers iterator method until the first yield return statement is
reached. This iteration returns a value of 3, and the current location in the iterator
method is retained. On the next iteration of the loop, execution in the iterator method
continues from where it left off, again stopping when it reaches a yield return
statement. This iteration returns a value of 5, and the current location in the iterator
method is again retained. The loop completes when the end of the iterator method is
reached.
C#
The return type of an iterator method or get accessor can be IEnumerable ,
IEnumerable<T> , IEnumerator , or IEnumerator<T> .
You can use a yield break statement to end the iteration.static void Main()
{
    foreach (int number in SomeNumbers ())
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 3 5 8
    Console.ReadKey();
}
public static System.Collections. IEnumerable SomeNumbers ()
{
    yield return 3;
    yield return 5;
    yield return 8;
}The following example has a single yield return statement that is inside a for loop. In
Main, each iteration of the foreach statement body creates a call to the iterator
function, which proceeds to the next yield return statement.
C#
In the following example, the DaysOfTheWeek class implements the IEnumerable
interface, which requires a GetEnumerator  method. The compiler implicitly calls the
GetEnumerator method, which returns an IEnumerator .７ Note
For all examples in this topic except the Simple Iterator example, include using
directives for the System.Collections and System.Collections.Generic
namespaces.
Simple Iterator
static void Main()
{
    foreach (int number in EvenSequence (5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    // Output: 6 8 10 12 14 16 18
    Console.ReadKey();
}
public static System.Collections.Generic. IEnumerable< int>
    EvenSequence (int firstNumber, int lastNumber )
{
    // Yield even numbers in the range.
    for (int number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
Creating a Collection ClassThe GetEnumerator method returns each string one at a time by using the yield return
statement.
C#
The following example creates a Zoo class that contains a collection of animals.
The foreach statement that refers to the class instance ( theZoo) implicitly calls the
GetEnumerator method. The foreach statements that refer to the Birds and Mammals
properties use the AnimalsForType named iterator method.
C#static void Main()
{
    DaysOfTheWeek days = new DaysOfTheWeek();
    foreach (string day in days)
    {
        Console.Write(day + " ");
    }
    // Output: Sun Mon Tue Wed Thu Fri Sat
    Console.ReadKey();
}
public class DaysOfTheWeek  : IEnumerable
{
    private string[] days = [ "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", 
"Sat"];
    public IEnumerator GetEnumerator ()
    {
        for (int index = 0; index < days.Length; index++)
        {
            // Yield each day of the week.
            yield return days[index];
        }
    }
}
static void Main()
{
    Zoo theZoo = new Zoo();
    theZoo.AddMammal( "Whale");
    theZoo.AddMammal( "Rhinoceros" );
    theZoo.AddBird( "Penguin" );
    theZoo.AddBird( "Warbler" );
    foreach (string name in theZoo)
    {        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros Penguin Warbler
    foreach (string name in theZoo.Birds)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Penguin Warbler
    foreach (string name in theZoo.Mammals)
    {
        Console.Write(name + " ");
    }
    Console.WriteLine();
    // Output: Whale Rhinoceros
    Console.ReadKey();
}
public class Zoo : IEnumerable
{
    // Private members.
    private List<Animal> animals = new List<Animal>();
    // Public methods.
    public void AddMammal (string name)
    {
        animals.Add( new Animal { Name = name, Type = Animal.TypeEnum.Mammal  
});
    }
    public void AddBird(string name)
    {
        animals.Add( new Animal { Name = name, Type = Animal.TypeEnum.Bird  
});
    }
    public IEnumerator GetEnumerator ()
    {
        foreach (Animal theAnimal in animals)
        {
            yield return theAnimal.Name;
        }
    }
    // Public members.
    public IEnumerable Mammals
    {
        get { return AnimalsForType(Animal.TypeEnum.Mammal); }
    }
    public IEnumerable BirdsIn the following example, the Stack<T>  generic class implements the IEnumerable<T>
generic interface. The Push  method assigns values to an array of type T. The
GetEnumerator  method returns the array values by using the yield return statement.
In addition to the generic GetEnumerator  method, the non-generic GetEnumerator
method must also be implemented. This is because IEnumerable<T>  inherits from
IEnumerable . The non-generic implementation defers to the generic implementation.
The example uses named iterators to support various ways of iterating through the
same collection of data. These named iterators are the TopToBottom and BottomToTop
properties, and the TopN method.
The BottomToTop property uses an iterator in a get accessor.
C#    {
        get { return AnimalsForType(Animal.TypeEnum.Bird); }
    }
    // Private methods.
    private IEnumerable AnimalsForType (Animal.TypeEnum type )
    {
        foreach (Animal theAnimal in animals)
        {
            if (theAnimal.Type == type)
            {
                yield return theAnimal.Name;
            }
        }
    }
    // Private class.
    private class Animal
    {
        public enum TypeEnum { Bird, Mammal }
        public string Name { get; set; }
        public TypeEnum Type { get; set; }
    }
}
Using Iterators with a Generic List
static void Main()
{
    Stack<int> theStack = new Stack<int>();    //  Add items to the stack.
    for (int number = 0; number <= 9; number++)
    {
        theStack.Push(number);
    }
    // Retrieve items from the stack.
    // foreach is allowed because theStack implements IEnumerable<int>.
    foreach (int number in theStack)
    {
        Console.Write( "{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0
    // foreach is allowed, because theStack.TopToBottom returns  
IEnumerable(Of Integer).
    foreach (int number in theStack.TopToBottom)
    {
        Console.Write( "{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3 2 1 0
    foreach (int number in theStack.BottomToTop)
    {
        Console.Write( "{0} ", number);
    }
    Console.WriteLine();
    // Output: 0 1 2 3 4 5 6 7 8 9
    foreach (int number in theStack.TopN( 7))
    {
        Console.Write( "{0} ", number);
    }
    Console.WriteLine();
    // Output: 9 8 7 6 5 4 3
    Console.ReadKey();
}
public class Stack<T> : IEnumerable <T>
{
    private T[] values = new T[100];
    private int top = 0;
    public void Push(T t)
    {
        values[top] = t;
        top++;
    }
    public T Pop()
    {
        top--;
        return values[top];An iterator can occur as a method or get accessor. An iterator cannot occur in an event,
instance constructor, static constructor, or static finalizer.    }
    // This method implements the GetEnumerator method. It allows
    // an instance of the class to be used in a foreach statement.
    public IEnumerator<T> GetEnumerator ()
    {
        for (int index = top - 1; index >= 0; index--)
        {
            yield return values[index];
        }
    }
    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
    public IEnumerable<T> TopToBottom
    {
        get { return this; }
    }
    public IEnumerable<T> BottomToTop
    {
        get
        {
            for (int index = 0; index <= top - 1; index++)
            {
                yield return values[index];
            }
        }
    }
    public IEnumerable<T> TopN(int itemsFromTop )
    {
        // Return less than itemsFromTop if necessary.
        int startIndex = itemsFromTop >= top ? 0 : top - itemsFromTop;
        for (int index = top - 1; index >= startIndex; index--)
        {
            yield return values[index];
        }
    }
}
Syntax InformationAn implicit conversion must exist from the expression type in the yield return
statement to the type argument for the IEnumerable<T> returned by the iterator.
In C#, an iterator method cannot have any in, ref, or out parameters.
In C#, yield is not a reserved word and has special meaning only when it is used before
a return or break keyword.
Although you write an iterator as a method, the compiler translates it into a nested class
that is, in effect, a state machine. This class keeps track of the position of the iterator as
long the foreach loop in the client code continues.
To see what the compiler does, you can use the Ildasm.exe tool to view the Microsoft
intermediate language code that's generated for an iterator method.
When you create an iterator for a class  or struct , you don't have to implement the whole
IEnumerator  interface. When the compiler detects the iterator, it automatically generates
the Current, MoveNext, and Dispose methods of the IEnumerator  or IEnumerator<T>
interface.
On each successive iteration of the foreach loop (or the direct call to
IEnumerator.MoveNext), the next iterator code body resumes after the previous yield
return statement. It then continues to the next yield return statement until the end of
the iterator body is reached, or until a yield break statement is encountered.
Iterators don't support the IEnumerator.R eset method. T o reiterate from the start, you
must obtain a new iterator. Calling Reset on the iterator returned by an iterator method
throws a NotSupportedException .
For additional information, see the C# Language Specification .
Iterators enable you to maintain the simplicity of a foreach loop when you need to use
complex code to populate a list sequence. This can be useful when you want to do the
following:
Modify the list sequence after the first foreach loop iteration.Technical Implementation
Use of IteratorsAvoid fully loading a large list before the first iteration of a foreach loop. An
example is a paged fetch to load a batch of table rows. Another example is the
EnumerateFiles  method, which implements iterators in .NET.
Encapsulate building the list in the iterator. In the iterator method, you can build
the list and then yield each result in a loop.
System.Collections.Generic
IEnumerable<T>
foreach, in
GenericsSee also
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
 Provide product feedbackStatemen ts (C# Programming Guide)
Article •04/22/2023
The actions that a program takes are expressed in statements. Common actions include
declaring variables, assigning values, calling methods, looping through collections, and
branching to one or another block of code, depending on a given condition. The order
in which statements are executed in a program is called the flow of control or flow of
execution. The flow of control may vary every time that a program is run, depending on
how the program reacts to input that it receives at run time.
A statement can consist of a single line of code that ends in a semicolon, or a series of
single-line statements in a block. A statement block is enclosed in {} brackets and can
contain nested blocks. The following code shows two examples of single-line
statements, and a multi-line statement block:
C#
    static void Main() 
    { 
        // Declaration statement.
        int counter;  
        // Assignment statement.  
        counter = 1; 
        // Error! This is an expression, not an expression statement.  
        // counter + 1;  
        // Declaration statements with initializers are functionally  
        // equivalent to  declaration statement followed by assignment  
statement:  
        int[] radii = { 15, 32, 108, 74, 9 }; // Declare and initialize an  
array. 
        const double pi = 3.14159; // Declare and initialize  constant.  
        // foreach statement block that contains multiple statements.  
        foreach (int radius in radii) 
        {  
            // Declaration statement with initializer.  
            double circumference = pi * ( 2 * radius);  
            // Expression statement (method invocation). A single-line  
            // statement can span multiple text lines because line breaks  
            // are treated as white space, which is ignored by the compiler.  
            System.Console.WriteLine( "Radius of circle #{0} is {1}.  
Circumference = {2:N2}" , 
                                    counter, radius, circumference);  
            // Expression statement (postfix increment).  The following table lists the various types of statements in C# and their associated
keywords, with links to topics that include more information:
Categor y C# keywords / not es
Declaration
statementsA declaration statement introduces a new variable or constant. A variable
declaration can optionally assign a value to the variable. In a constant declaration,
the assignment is required.
Expression
statementsExpression statements that calculate a value must store the value in a variable.
Selection
statementsSelection statements enable you to branch to different sections of code, depending
on one or more specified conditions. For more information, see the following topics:
if
switch
Iteration
statementsIteration statements enable you to loop through collections like arrays, or perform
the same set of statements repeatedly until a specified condition is met. For more
information, see the following topics:
do
for
foreach
while            counter++;  
        } // End of foreach statement block  
    } // End of Main method body.  
} // End of SimpleStatements class.  
/* 
   Output:  
    Radius of circle #1 = 15. Circumference = 94.25  
    Radius of circle #2 = 32. Circumference = 201.06  
    Radius of circle #3 = 108. Circumference = 678.58  
    Radius of circle #4 = 74. Circumference = 464.96  
    Radius of circle #5 = 9. Circumference = 56.55  
*/ 
Types of statementsCategor y C# keywords / not es
Jump
statementsJump statements transfer control to another section of code. For more information,
see the following topics:
break
continue
goto
return
yield
Exception-
handling
statementsException-handling statements enable you to gracefully recover from exceptional
conditions that occur at run time. For more information, see the following topics:
throw
try-catch
try-finally
try-catch-finally
checked
and
uncheckedThe checked and unchecked statements enable you to specify whether integral-type
numerical operations are allowed to cause an overflow when the result is stored in a
variable that is too small to hold the resulting value.
The await
statementIf you mark a method with the async  modifier, you can use the await  operator in the
method. When control reaches an await expression in the async method, control
returns to the caller, and progress in the method is suspended until the awaited
task completes. When the task is complete, execution can resume in the method.  
For a simple example, see the "Async Methods" section of Methods . For more
information, see Asynchronous Programming with async and await .
The yield
return
statementAn iterator performs a custom iteration over a collection, such as a list or an array.
An iterator uses the yield return  statement to return each element one at a time.
When a yield return statement is reached, the current location in code is
remembered. Execution is restarted from that location when the iterator is called
the next time.  
For more information, see Iterators .
The fixed
statementThe fixed statement prevents the garbage collector from relocating a movable
variable. For more information, see fixed .
The lock
statementThe lock statement enables you to limit access to blocks of code to only one thread
at a time. For more information, see lock.
Labeled
statementsYou can give a statement a label and then use the goto  keyword to jump to the
labeled statement. (See the example in the following row.)
The empty
statementThe empty statement consists of a single semicolon. It does nothing and can be
used in places where a statement is required but no action needs to be performed.The following code shows examples of variable declarations with and without an initial
assignment, and a constant declaration with the necessary initialization.
C#
The following code shows examples of expression statements, including assignment,
object creation with assignment, and method invocation.
C#
The following examples show two uses for an empty statement:
C#Declaration statements
// Variable declaration statements.  
double area; 
double radius = 2; 
// Constant declaration statement.  
const double pi = 3.14159; 
Expression statements
// Expression statement (assignment).  
area = 3.14 * (radius * radius);  
// Error. Not  statement because no assignment:  
//circ * 2;  
// Expression statement (method invocation).  
System.Console.WriteLine();  
// Expression statement (new object creation).  
System.Collections.Generic.List< string> strings =  
    new System.Collections.Generic.List< string>(); 
The empty statement
void ProcessMessages () 
{ 
    while (ProcessMessage())  
        ; // Statement needed here.  
} Some statements, for example, iteration statements , always have an embedded
statement that follows them. This embedded statement may be either a single
statement or multiple statements enclosed by {} brackets in a statement block. Even
single-line embedded statements can be enclosed in {} brackets, as shown in the
following example:
C#
An embedded statement that is not enclosed in {} brackets cannot be a declaration
statement or a labeled statement. This is shown in the following example:
C#
Put the embedded statement in a block to fix the error:
C#void F() 
{ 
    //... 
    if (done) goto exit; 
//... 
exit: 
    ; // Statement needed here.  
} 
Embedded statements
// Recommended style. Embedded statement in  block.  
foreach (string s in System.IO.Directory.GetDirectories(
                        System.Environment.CurrentDirectory))  
{ 
    System.Console.WriteLine(s);  
} 
// Not recommended.  
foreach (string s in System.IO.Directory.GetDirectories(
                        System.Environment.CurrentDirectory))  
    System.Console.WriteLine(s);  
if(pointB == true) 
    //Error CS1023:  
    int radius = 5; 
if (b == true) 
{ 
    // OK: Statement blocks can be nested, as shown in the following code:
C#
If the compiler determines that the flow of control can never reach a particular
statement under any circumstances, it will produce warning CS0162, as shown in the
following example:
C#
For more information, see the Statements  section of the C# language specification .    System.DateTime d = System.DateTime.Now;  
    System.Console.WriteLine(d.ToLongDateString());  
} 
Nested statement blocks
foreach (string s in System.IO.Directory.GetDirectories(
    System.Environment.CurrentDirectory))  
{ 
    if (s.StartsWith( "CSharp" )) 
    { 
        if (s.EndsWith( "TempFolder" )) 
        {  
            return s; 
        }  
    } 
} 
return "Not found." ; 
Unreachable statements
// An over-simplified example of unreachable code.  
const int val = 5; 
if (val < 4) 
{ 
    System.Console.WriteLine( "I'll never write anything." ); //CS0162  
} 
C# language specification
See alsoC# Programming Guide
Statement keywords
C# operators and expressionsExpression-bodied members (C#
programming guide)
Article •09/29/2022
Expression body definitions let you provide a member's implementation in a concise,
readable form. Y ou can use an expression body definition whenever the logic for any
supported member, such as a method or property, consists of a single expression. An
expression body definition has the following general syntax:
C#
where expression  is a valid expression.
Expression body definitions can be used with the following type members:
Method
Read-only property
Property
Constructor
Finalizer
Indexer
An expression-bodied method consists of a single expression that returns a value whose
type matches the method's return type, or, for methods that return void, that performs
some operation. For example, types that override the ToString  method typically include
a single expression that returns the string representation of the current object.
The following example defines a Person class that overrides the ToString  method with
an expression body definition. It also defines a DisplayName method that displays a
name to the console. The return keyword is not used in the ToString expression body
definition.
C#member => expression;
Methods
using System;
namespace  ExpressionBodiedMembers ;For more information, see Methods (C# Programming Guide) .
You can use expression body definition to implement a read-only property. T o do that,
use the following syntax:
C#
The following example defines a Location class whose read-only Name property is
implemented as an expression body definition that returns the value of the private
locationName field:
C#public class Person
{
   public Person(string firstName, string lastName )
   {
      fname = firstName;
      lname = lastName;
   }
   private string fname;
   private string lname;
   public override  string ToString () => $"{fname} {lname}".Trim();
   public void DisplayName () => Console.WriteLine(ToString());
}
class Example
{
   static void Main()
   {
      Person p = new Person( "Mandy", "Dejesus" );
      Console.WriteLine(p);
      p.DisplayName();
   }
}
Read-only properties
PropertyType PropertyName => expression;
public class Location
{
   private string locationName;
   public Location (string name)
   {For more information about properties, see Properties (C# Programming Guide) .
You can use expression body definitions to implement property get and set accessors.
The following example demonstrates how to do that:
C#
For more information about properties, see Properties (C# Programming Guide) .
An expression body definition for a constructor typically consists of a single assignment
expression or a method call that handles the constructor's arguments or initializes
instance state.
The following example defines a Location class whose constructor has a single string
parameter named name . The expression body definition assigns the argument to the
Name property.
C#      locationName = name;
   }
   public string Name => locationName;
}
Properties
public class Location
{
   private string locationName;
   public Location (string name) => Name = name;
   public string Name
   {
      get => locationName;
      set => locationName = value;
   }
}
Constructors
public class Location
{
   private string locationName;For more information, see Constructors (C# Programming Guide) .
An expression body definition for a finalizer typically contains cleanup statements, such
as statements that release unmanaged resources.
The following example defines a finalizer that uses an expression body definition to
indicate that the finalizer has been called.
C#
For more information, see Finalizers (C# Programming Guide) .
Like with properties, indexer get and set accessors consist of expression body
definitions if the get accessor consists of a single expression that returns a value or the
set accessor performs a simple assignment.
The following example defines a class named Sports that includes an internal String
array that contains the names of some sports. Both the indexer get and set accessors
are implemented as expression body definitions.
C#   public Location (string name) => Name = name;
   public string Name
   {
      get => locationName;
      set => locationName = value;
   }
}
Finalizers
public class Destroyer
{
   public override  string ToString () => GetType().Name;
   ~Destroyer() => Console.WriteLine( $"The {ToString()}  finalizer is  
executing." );
}
Indexers
using System;
using System.Collections.Generic;For more information, see Indexers (C# Programming Guide) .
.NET code style rules for expression-bodied-membersnamespace  SportsExample ;
public class Sports
{
   private string[] types = [ "Baseball" , "Basketball" , "Football" ,
                              "Hockey" , "Soccer" , "Tennis" ,
                              "Volleyball"  ];
   public string this[int i]
   {
      get => types[i];
      set => types[i] = value;
   }
}
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
 Provide product feedbackEquality comparisons (C# Programming
Guide)
Article •09/23/2021
It is sometimes necessary to compare two values for equality. In some cases, you are
testing for value equality , also known as equiv alenc e, which means that the values that
are contained by the two variables are equal. In other cases, you have to determine
whether two variables refer to the same underlying object in memory. This type of
equality is called reference equality , or identity . This topic describes these two kinds of
equality and provides links to other topics for more information.
Reference equality means that two object references refer to the same underlying
object. This can occur through simple assignment, as shown in the following example.
C#Reference equality
using System;  
class Test 
{ 
    public int Num { get; set; } 
    public string Str { get; set; } 
    static void Main() 
    { 
        Test a = new Test() { Num = 1, Str = "Hi" }; 
        Test b = new Test() { Num = 1, Str = "Hi" }; 
        bool areEqual = System.Object.ReferenceEquals(a, b);  
        // False:  
        System.Console.WriteLine( "ReferenceEquals(a, b) = {0}" , areEqual);  
        // Assign b to a.  
        b = a;  
        // Repeat calls with different results.  
        areEqual = System.Object.ReferenceEquals(a, b);  
        // True:  
        System.Console.WriteLine( "ReferenceEquals(a, b) = {0}" , areEqual);  
        // Keep the console open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} In this code, two objects are created, but after the assignment statement, both
references refer to the same object. Therefore they have reference equality. Use the
ReferenceEquals  method to determine whether two references refer to the same object.
The concept of reference equality applies only to reference types. V alue type objects
cannot have reference equality because when an instance of a value type is assigned to
a variable, a copy of the value is made. Therefore you can never have two unboxed
structs that refer to the same location in memory. Furthermore, if you use
ReferenceEquals  to compare two value types, the result will always be false, even if the
values that are contained in the objects are all identical. This is because each variable is
boxed into a separate object instance. For more information, see How to test for
reference equality (Identity) .
Value equality means that two objects contain the same value or values. For primitive
value types such as int or bool, tests for value equality are straightforward. Y ou can use
the == operator, as shown in the following example.
C#
For most other types, testing for value equality is more complex because it requires that
you understand how the type defines it. For classes and structs that have multiple fields
or properties, value equality is often defined to mean that all fields or properties have
the same value. For example, two Point objects might be defined to be equivalent if
pointA.X is equal to pointB.X and pointA.Y is equal to pointB.Y. For records, value
equality means that two variables of a record type are equal if the types match and all
property and field values match.
However, there is no requirement that equivalence be based on all the fields in a type. It
can be based on a subset. When you compare types that you do not own, you should
make sure to understand specifically how equivalence is defined for that type. For moreValue equality
int a = GetOriginalValue();   
int b = GetCurrentValue();   
   
// Test for value equality.  
if (b == a)  
{   
    // The two integers are equal.   
}   information about how to define value equality in your own classes and structs, see How
to define value equality for a type .
Equality comparisons of floating-point values ( double  and float) are problematic
because of the imprecision of floating-point arithmetic on binary computers. For more
information, see the remarks in the topic System.Double .
Title Descr iption
How to test for
reference equality
(Identity)Describes how to determine whether two variables have reference
equality.
How to define value
equality for a typeDescribes how to provide a custom definition of value equality for a
type.
C# Programming
GuideProvides links to detailed information about important C# language
features and features that are available to C# through .NET.
Types Provides information about the C# type system and links to additional
information.
Records Provides information about record types, which test for value equality
by default.
C# Programming GuideValue equality for floating-point values
Related topics
See alsoHow to define value equality for a class
or struct (C# Programming Guide)
Article •06/21/2022
Records  automatically implement value equality. Consider defining a record instead of a
class when your type models data and should implement value equality.
When you define a class or struct, you decide whether it makes sense to create a custom
definition of value equality (or equivalence) for the type. T ypically, you implement value
equality when you expect to add objects of the type to a collection, or when their
primary purpose is to store a set of fields or properties. Y ou can base your definition of
value equality on a comparison of all the fields and properties in the type, or you can
base the definition on a subset.
In either case, and in both classes and structs, your implementation should follow the
five guarantees of equivalence (for the following rules, assume that x, y and z are not
null):
1. The reflexive property: x.Equals(x) returns true.
2. The symmetric property: x.Equals(y) returns the same value as y.Equals(x).
3. The transitive property: if (x.Equals(y) && y.Equals(z)) returns true, then
x.Equals(z) returns true.
4. Successive invocations of x.Equals(y) return the same value as long as the objects
referenced by x and y aren't modified.
5. Any non-null value isn't equal to null. However, x.Equals(y) throws an exception
when x is null. That breaks rules 1 or 2, depending on the argument to Equals.
Any struct that you define already has a default implementation of value equality that it
inherits from the System.V alueT ype override of the Object.Equals(Object)  method. This
implementation uses reflection to examine all the fields and properties in the type.
Although this implementation produces correct results, it is relatively slow compared to
a custom implementation that you write specifically for the type.
The implementation details for value equality are different for classes and structs.
However, both classes and structs require the same basic steps for implementing
equality:1. Override the virtual  Object.Equals(Object)  method. In most cases, your
implementation of bool Equals( object obj ) should just call into the type-
specific Equals method that is the implementation of the System.IEquatable<T>
interface. (See step 2.)
2. Implement the System.IEquatable<T>  interface by providing a type-specific
Equals method. This is where the actual equivalence comparison is performed. For
example, you might decide to define equality by comparing only one or two fields
in your type. Don't throw exceptions from Equals. For classes that are related by
inheritance:
This method should examine only fields that are declared in the class. It
should call base.Equals to examine fields that are in the base class. (Don't
call base.Equals if the type inherits directly from Object , because the Object
implementation of Object.Equals(Object)  performs a reference equality
check.)
Two variables should be deemed equal only if the run-time types of the
variables being compared are the same. Also, make sure that the IEquatable
implementation of the Equals method for the run-time type is used if the
run-time and compile-time types of a variable are different. One strategy for
making sure run-time types are always compared correctly is to implement
IEquatable only in sealed classes. For more information, see the class
example  later in this article.
3. Optional but recommended: Overload the == and != operators.
4. Override Object.GetHashCode  so that two objects that have value equality produce
the same hash code.
5. Optional: T o support definitions for "greater than" or "less than," implement the
IComparable<T>  interface for your type, and also overload the <= and >=
operators.
７ Note
You can use records to get value equality semantics without any unnecessary
boilerplate code.
Class exampleThe following example shows how to implement value equality in a class (reference
type).
C#
namespace  ValueEqualityClass ;
class TwoDPoint  : IEquatable <TwoDPoint >
{
    public int X { get; private set; }
    public int Y { get; private set; }
    public TwoDPoint (int x, int y)
    {
        if (x is (< 1 or > 2000) || y is (< 1 or > 2000))
        {
            throw new ArgumentException( "Point must be in range 1 - 2000" );
        }
        this.X = x;
        this.Y = y;
    }
    public override  bool Equals(object obj) => this.Equals(obj as 
TwoDPoint);
    public bool Equals(TwoDPoint p )
    {
        if (p is null)
        {
            return false;
        }
        // Optimization for a common success case.
        if (Object.ReferenceEquals( this, p))
        {
            return true;
        }
        // If run-time types are not exactly the same, return false.
        if (this.GetType() != p.GetType())
        {
            return false;
        }
        // Return true if the fields match.
        // Note that the base class is not invoked because it is
        // System.Object, which defines Equals as reference equality.
        return (X == p.X) && (Y == p.Y);
    }
    public override  int GetHashCode () => (X, Y).GetHashCode();
    public static bool operator  ==(TwoDPoint lhs, TwoDPoint rhs)
    {        if (lhs is null)
        {
            if (rhs is null)
            {
                return true;
            }
            // Only the left side is null.
            return false;
        }
        // Equals handles case of null on right side.
        return lhs.Equals(rhs);
    }
    public static bool operator  !=(TwoDPoint lhs, TwoDPoint rhs) => !(lhs ==  
rhs);
}
// For the sake of simplicity, assume a ThreeDPoint IS a TwoDPoint.
class ThreeDPoint  : TwoDPoint , IEquatable <ThreeDPoint >
{
    public int Z { get; private set; }
    public ThreeDPoint (int x, int y, int z)
        : base(x, y)
    {
        if ((z < 1) || (z > 2000))
        {
            throw new ArgumentException( "Point must be in range 1 - 2000" );
        }
        this.Z = z;
    }
    public override  bool Equals(object obj) => this.Equals(obj as 
ThreeDPoint);
    public bool Equals(ThreeDPoint p )
    {
        if (p is null)
        {
            return false;
        }
        // Optimization for a common success case.
        if (Object.ReferenceEquals( this, p))
        {
            return true;
        }
        // Check properties that this class declares.
        if (Z == p.Z)
        {
            // Let base class check its own fields
            // and do the run-time type comparison.
            return base.Equals((TwoDPoint)p);        }
        else
        {
            return false;
        }
    }
    public override  int GetHashCode () => (X, Y, Z).GetHashCode();
    public static bool operator  ==(ThreeDPoint lhs, ThreeDPoint rhs)
    {
        if (lhs is null)
        {
            if (rhs is null)
            {
                // null == null = true.
                return true;
            }
            // Only the left side is null.
            return false;
        }
        // Equals handles the case of null on right side.
        return lhs.Equals(rhs);
    }
    public static bool operator  !=(ThreeDPoint lhs, ThreeDPoint rhs) => !
(lhs == rhs);
}
class Program
{
    static void Main(string[] args)
    {
        ThreeDPoint pointA = new ThreeDPoint( 3, 4, 5);
        ThreeDPoint pointB = new ThreeDPoint( 3, 4, 5);
        ThreeDPoint pointC = null;
        int i = 5;
        Console.WriteLine( "pointA.Equals(pointB) = {0}" , 
pointA.Equals(pointB));
        Console.WriteLine( "pointA == pointB = {0}" , pointA == pointB);
        Console.WriteLine( "null comparison = {0}" , pointA.Equals(pointC));
        Console.WriteLine( "Compare to some other type = {0}" , 
pointA.Equals(i));
        TwoDPoint pointD = null;
        TwoDPoint pointE = null;
        Console.WriteLine( "Two null TwoDPoints are equal: {0}" , pointD ==  
pointE);
        pointE = new TwoDPoint( 3, 4);
        Console.WriteLine( "(pointE == pointA) = {0}" , pointE == pointA);
        Console.WriteLine( "(pointA == pointE) = {0}" , pointA == pointE);On classes (reference types), the default implementation of both Object.Equals(Object)
methods performs a reference equality comparison, not a value equality check. When an
implementer overrides the virtual method, the purpose is to give it value equality
semantics.
The == and != operators can be used with classes even if the class does not overload
them. However, the default behavior is to perform a reference equality check. In a class,
if you overload the Equals method, you should overload the == and != operators, but
it is not required.        Console.WriteLine( "(pointA != pointE) = {0}" , pointA != pointE);
        System.Collections.ArrayList list = new 
System.Collections.ArrayList();
        list.Add( new ThreeDPoint( 3, 4, 5));
        Console.WriteLine( "pointE.Equals(list[0]): {0}" , 
pointE.Equals(list[ 0]));
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
    pointA.Equals(pointB) = True
    pointA == pointB = True
    null comparison = False
    Compare to some other type = False
    Two null TwoDPoints are equal: True
    (pointE == pointA) = False
    (pointA == pointE) = False
    (pointA != pointE) = True
    pointE.Equals(list[0]): False
*/
） Impor tant
The preceding example code may not handle every inheritance scenario the way
you expect. Consider the following code:
C#
TwoDPoint p1 = new ThreeDPoint( 1, 2, 3);
TwoDPoint p2 = new ThreeDPoint( 1, 2, 4);
Console.WriteLine(p1.Equals(p2)); // output: TrueThe following example shows how to implement value equality in a struct (value type):
C#This code reports that p1 equals p2 despite the difference in z values. The
difference is ignored because the compiler picks the TwoDPoint implementation of
IEquatable based on the compile-time type.
The built-in value equality of record types handles scenarios like this correctly. If
TwoDPoint and ThreeDPoint were record types, the result of p1.Equals(p2) would
be False. For more information, see Equality in record type inheritance
hierar chies .
Struct example
namespace  ValueEqualityStruct
{
    struct TwoDPoint : IEquatable<TwoDPoint>
    {
        public int X { get; private set; }
        public int Y { get; private set; }
        public TwoDPoint (int x, int y)
            : this()
        {
            if (x is (< 1 or > 2000) || y is (< 1 or > 2000))
            {
                throw new ArgumentException( "Point must be in range 1 -  
2000");
            }
            X = x;
            Y = y;
        }
        public override  bool Equals(object? obj) => obj is TwoDPoint other  
&& this.Equals(other);
        public bool Equals(TwoDPoint p ) => X == p.X && Y == p.Y;
        public override  int GetHashCode () => (X, Y).GetHashCode();
        public static bool operator  ==(TwoDPoint lhs, TwoDPoint rhs) =>  
lhs.Equals(rhs);
        public static bool operator  !=(TwoDPoint lhs, TwoDPoint rhs) => !
(lhs == rhs);
    }
    class Program    {
        static void Main(string[] args)
        {
            TwoDPoint pointA = new TwoDPoint( 3, 4);
            TwoDPoint pointB = new TwoDPoint( 3, 4);
            int i = 5;
            // True:
            Console.WriteLine( "pointA.Equals(pointB) = {0}" , 
pointA.Equals(pointB));
            // True:
            Console.WriteLine( "pointA == pointB = {0}" , pointA == pointB);
            // True:
            Console.WriteLine( "object.Equals(pointA, pointB) = {0}" , 
object.Equals(pointA, pointB));
            // False:
            Console.WriteLine( "pointA.Equals(null) = {0}" , 
pointA.Equals( null));
            // False:
            Console.WriteLine( "(pointA == null) = {0}" , pointA == null);
            // True:
            Console.WriteLine( "(pointA != null) = {0}" , pointA != null);
            // False:
            Console.WriteLine( "pointA.Equals(i) = {0}" , pointA.Equals(i));
            // CS0019:
            // Console.WriteLine("pointA == i = {0}", pointA == i);
            // Compare unboxed to boxed.
            System.Collections.ArrayList list = new 
System.Collections.ArrayList();
            list.Add( new TwoDPoint( 3, 4));
            // True:
            Console.WriteLine( "pointA.Equals(list[0]): {0}" , 
pointA.Equals(list[ 0]));
            // Compare nullable to nullable and to non-nullable.
            TwoDPoint? pointC = null;
            TwoDPoint? pointD = null;
            // False:
            Console.WriteLine( "pointA == (pointC = null) = {0}" , pointA ==  
pointC);
            // True:
            Console.WriteLine( "pointC == pointD = {0}" , pointC == pointD);
            TwoDPoint temp = new TwoDPoint( 3, 4);
            pointC = temp;
            // True:
            Console.WriteLine( "pointA == (pointC = 3,4) = {0}" , pointA ==  
pointC);
            pointD = temp;
            // True:
            Console.WriteLine( "pointD == (pointC = 3,4) = {0}" , pointD ==  
pointC);For structs, the default implementation of Object.Equals(Object)  (which is the overridden
version in System.V alueT ype) performs a value equality check by using reflection to
compare the values of every field in the type. When an implementer overrides the virtual
Equals method in a struct, the purpose is to provide a more efficient means of
performing the value equality check and optionally to base the comparison on some
subset of the struct's fields or properties.
The == and != operators can't operate on a struct unless the struct explicitly overloads
them.
Equality comparisons
C# programming guide            Console.WriteLine( "Press any key to exit." );
            Console.ReadKey();
        }
    }
    /* Output:
        pointA.Equals(pointB) = True
        pointA == pointB = True
        Object.Equals(pointA, pointB) = True
        pointA.Equals(null) = False
        (pointA == null) = False
        (pointA != null) = True
        pointA.Equals(i) = False
        pointE.Equals(list[0]): True
        pointA == (pointC = null) = False
        pointC == pointD = True
        pointA == (pointC = 3,4) = True
        pointD == (pointC = 3,4) = True
    */
}
See also
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
contributor guide .How to test for reference equality
(Identity) (C# Programming Guide)
Article •11/05/2021
You do not have to implement any custom logic to support reference equality
comparisons in your types. This functionality is provided for all types by the static
Object.R eferenceEquals  method.
The following example shows how to determine whether two variables have reference
equality , which means that they refer to the same object in memory.
The example also shows why Object.R eferenceEquals  always returns false for value
types and why you should not use ReferenceEquals  to determine string equality.
C#Example
using System.Text;  
namespace  TestReferenceEquality  
{ 
    struct TestStruct  
    { 
        public int Num { get; private set; } 
        public string Name { get; private set; } 
        public TestStruct (int i, string s) : this() 
        {  
            Num = i;  
            Name = s;  
        }  
    } 
    class TestClass  
    { 
        public int Num { get; set; } 
        public string? Name { get; set; } 
    } 
    class Program 
    { 
        static void Main() 
        {  
            // Demonstrate reference equality with reference types.  
            #region ReferenceTypes              // Create two reference type instances that have identical  
values. 
            TestClass tcA = new TestClass() { Num = 1, Name = "New 
TestClass"  }; 
            TestClass tcB = new TestClass() { Num = 1, Name = "New 
TestClass"  }; 
            Console.WriteLine( "ReferenceEquals(tcA, tcB) = {0}" , 
                                Object.ReferenceEquals(tcA, tcB)); // false  
            // After assignment, tcB and tcA refer to the same object.  
            // They now have reference equality.  
            tcB = tcA;  
            Console.WriteLine( "After assignment: ReferenceEquals(tcA, tcB) =  
{0}", 
                                Object.ReferenceEquals(tcA, tcB)); // true 
            // Changes made to tcA are reflected in tcB. Therefore, objects  
            // that have reference equality also have value equality.  
            tcA.Num = 42; 
            tcA.Name = "TestClass 42" ; 
            Console.WriteLine( "tcB.Name = {0} tcB.Num: {1}" , tcB.Name,  
tcB.Num);  
            #endregion  
            // Demonstrate that two value type instances never have  
reference equality.  
            #region ValueTypes  
            TestStruct tsC = new TestStruct( 1, "TestStruct 1" ); 
            // Value types are copied on assignment. tsD and tsC have  
            // the same values but are not the same object.  
            TestStruct tsD = tsC;
            Console.WriteLine( "After assignment: ReferenceEquals(tsC, tsD) =  
{0}", 
                                Object.ReferenceEquals(tsC, tsD)); // false  
            #endregion  
            #region stringRefEquality  
            // Constant strings within the same assembly are always interned  
by the runtime.  
            // This means they are stored in the same location in memory.  
Therefore,  
            // the two strings have reference equality although no  
assignment takes place.  
            string strA = "Hello world!" ; 
            string strB = "Hello world!" ; 
            Console.WriteLine( "ReferenceEquals(strA, strB) = {0}" , 
                             Object.ReferenceEquals(strA, strB)); // true 
            // After a new string is assigned to strA, strA and strB  
            // are no longer interned and no longer have reference equality.  
            strA = "Goodbye world!" ; 
            Console.WriteLine( "strA = \"{0}\" strB = \"{1}\"" , strA, strB);  The implementation of Equals in the System.Object  universal base class also performs a
reference equality check, but it is best not to use this because, if a class happens to
override the method, the results might not be what you expect. The same is true for the
== and != operators. When they are operating on reference types, the default behavior
of == and != is to perform a reference equality check. However, derived classes can
overload the operator to perform a value equality check. T o minimize the potential for
error, it is best to always use ReferenceEquals  when you have to determine whether two
objects have reference equality.
Constant strings within the same assembly are always interned by the runtime. That is,
only one instance of each unique literal string is maintained. However, the runtime does            Console.WriteLine( "After strA changes, ReferenceEquals(strA,  
strB) = {0}" , 
                            Object.ReferenceEquals(strA, strB)); // false  
            // A string that is created at runtime cannot be interned.  
            StringBuilder sb = new StringBuilder( "Hello world!" ); 
            string stringC = sb.ToString();  
            // False:  
            Console.WriteLine( "ReferenceEquals(stringC, strB) = {0}" , 
                            Object.ReferenceEquals(stringC, strB));  
            // The string class overloads the == operator to perform an  
equality comparison.  
            Console.WriteLine( "stringC == strB = {0}" , stringC == strB); // 
true 
            #endregion  
            // Keep the console open in debug mode.  
            Console.WriteLine( "Press any key to exit." ); 
            Console.ReadKey();  
        }  
    } 
} 
/* Output:  
    ReferenceEquals(tcA, tcB) = False  
    After assignment: ReferenceEquals(tcA, tcB) = True  
    tcB.Name = TestClass 42 tcB.Num: 42  
    After assignment: ReferenceEquals(tsC, tsD) = False  
    ReferenceEquals(strA, strB) = True  
    strA = "Goodbye world!" strB = "Hello world!"  
    After strA changes, ReferenceEquals(strA, strB) = False  
    ReferenceEquals(stringC, strB) = False  
    stringC == strB = True  
*/ not guarantee that strings created at run time are interned, nor does it guarantee that
two equal constant strings in different assemblies are interned.
Equality ComparisonsSee alsoCasting and type conversions (C#
Programming Guide)
Article •01/12/2022
Because C# is statically-typed at compile time, after a variable is declared, it cannot be
declared again or assigned a value of another type unless that type is implicitly
convertible to the variable's type. For example, the string cannot be implicitly
converted to int. Therefore, after you declare i as an int, you cannot assign the string
"Hello" to it, as the following code shows:
C#
However, you might sometimes need to copy a value into a variable or method
parameter of another type. For example, you might have an integer variable that you
need to pass to a method whose parameter is typed as double. Or you might need to
assign a class variable to a variable of an interface type. These kinds of operations are
called type c onversions . In C#, you can perform the following kinds of conversions:
Implicit conv ersions : No special syntax is required because the conversion always
succeeds and no data will be lost. Examples include conversions from smaller to
larger integral types, and conversions from derived classes to base classes.
Explicit conv ersions (casts) : Explicit conversions require a cast expression . Casting
is required when information might be lost in the conversion, or when the
conversion might not succeed for other reasons. T ypical examples include numeric
conversion to a type that has less precision or a smaller range, and conversion of a
base-class instance to a derived class.
User-defined conv ersions : User-defined conversions are performed by special
methods that you can define to enable explicit and implicit conversions between
custom types that do not have a base class–derived class relationship. For more
information, see User-defined conversion operators .
Conv ersions with helper classes : To convert between non-compatible types, such
as integers and System.DateTime  objects, or hexadecimal strings and byte arrays,
you can use the System.BitConverter  class, the System.Convert  class, and the Parseint i; 
// error CS0029: Cannot implicitly convert type 'string' to 'int'  
i = "Hello"; methods of the built-in numeric types, such as Int32.P arse. For more information,
see How to convert a byte array to an int , How to convert a string to a number ,
and How to convert between hexadecimal strings and numeric types .
For built-in numeric types, an implicit conversion can be made when the value to be
stored can fit into the variable without being truncated or rounded off. For integral
types, this means the range of the source type is a proper subset of the range for the
target type. For example, a variable of type long (64-bit integer) can store any value that
an int (32-bit integer) can store. In the following example, the compiler implicitly
converts the value of num on the right to a type long before assigning it to bigNum.
C#
For a complete list of all implicit numeric conversions, see the Implicit numeric
conversions  section of the Built-in numeric conversions  article.
For reference types, an implicit conversion always exists from a class to any one of its
direct or indirect base classes or interfaces. No special syntax is necessary because a
derived class always contains all the members of a base class.
C#
However, if a conversion cannot be made without a risk of losing information, the
compiler requires that you perform an explicit conversion, which is called a cast. A cast is
a way of explicitly informing the compiler that you intend to make the conversion and
that you are aware that data loss might occur, or the cast may fail at run time. T o
perform a cast, specify the type that you are casting to in parentheses in front of theImplicit conversions
// Implicit conversion. A long can  
// hold any value an int can hold, and more!  
int num = 2147483647 ; 
long bigNum = num;  
Derived d = new Derived();  
// Always OK.  
Base b = d;  
Explicit conversionsvalue or variable to be converted. The following program casts a double  to an int. The
program will not compile without the cast.
C#
For a complete list of supported explicit numeric conversions, see the Explicit numeric
conversions  section of the Built-in numeric conversions  article.
For reference types, an explicit cast is required if you need to convert from a base type
to a derived type:
C#
A cast operation between reference types does not change the run-time type of the
underlying object; it only changes the type of the value that is being used as a reference
to that object. For more information, see Polymorphism .
In some reference type conversions, the compiler cannot determine whether a cast will
be valid. It is possible for a cast operation that compiles correctly to fail at run time. Asclass Test 
{ 
    static void Main() 
    { 
        double x = 1234.7; 
        int a; 
        // Cast double to int.  
        a = ( int)x; 
        System.Console.WriteLine(a);  
    } 
} 
// Output: 1234  
// Create a new derived type.  
Giraffe g = new Giraffe();  
// Implicit conversion to base type is safe.  
Animal a = g;  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe)a;  
Type conversion exceptions at run timeshown in the following example, a type cast that fails at run time will cause an
InvalidCastException  to be thrown.
C#
The Test method has an Animal parameter, thus explicitly casting the argument a to a
Reptile makes a dangerous assumption. It is safer to not make assumptions, but rather
check the type. C# provides the is operator to enable you to test for compatibility
before actually performing a cast. For more information, see How to safely cast using
pattern matching and the as and is operators .
For more information, see the Conversions  section of the C# language specification .
C# Programming Guideclass Animal 
{ 
    public void Eat() => System.Console.WriteLine( "Eating." ); 
    public override  string ToString () => "I am an animal." ; 
} 
class Reptile : Animal { } 
class Mammal : Animal { } 
class UnSafeCast  
{ 
    static void Main() 
    { 
        Test( new Mammal());  
        // Keep the console window open in debug mode.  
        System.Console.WriteLine( "Press any key to exit." ); 
        System.Console.ReadKey();
    } 
    static void Test(Animal a ) 
    { 
        // System.InvalidCastException at run time  
        // Unable to cast object of type 'Mammal' to type 'Reptile'  
        Reptile r = (Reptile)a;  
    } 
} 
C# language specification
See alsoTypes
Cast expression
User-defined conversion operators
Generalized T ype Conversion
How to convert a string to a numberBoxing and Unboxing (C# Programming
Guide)
Article •09/15/2021
Boxing is the process of converting a value type  to the type object or to any interface
type implemented by this value type. When the common language runtime (CLR) boxes
a value type, it wraps the value inside a System.Object  instance and stores it on the
managed heap. Unboxing extracts the value type from the object. Boxing is implicit;
unboxing is explicit. The concept of boxing and unboxing underlies the C# unified view
of the type system in which a value of any type can be treated as an object.
In the following example, the integer variable i is boxed and assigned to object o.
C#
The object o can then be unboxed and assigned to integer variable i:
C#
The following examples illustrate how boxing is used in C#.
C#int i = 123; 
// The following line boxes i.  
object o = i; 
o = 123; 
i = (int)o;  // unboxing  
// String.Concat example.  
// String.Concat has many versions. Rest the mouse pointer on  
// Concat in the following statement to verify that the version  
// that is used here takes three object arguments. Both 42 and  
// true must be boxed.  
Console.WriteLine(String.Concat( "Answer" , 42, true)); 
// List example.  
// Create a list of objects to hold a heterogeneous collection  
// of elements.  
List<object> mixedList = new List<object>(); 
// Add a string element to the list.  
mixedList.Add( "First Group:" ); // Add some integers to the list.
for (int j = 1; j < 5; j++) 
{ 
    // Rest the mouse pointer over j to verify that you are adding
    // an int to a list of objects. Each element j is boxed when  
    // you add j to mixedList.  
    mixedList.Add(j);  
} 
// Add another string and more integers.  
mixedList.Add( "Second Group:" ); 
for (int j = 5; j < 10; j++) 
{ 
    mixedList.Add(j);  
} 
// Display the elements in the list. Declare the loop variable by  
// using var, so that the compiler assigns its type.  
foreach (var item in mixedList)  
{ 
    // Rest the mouse pointer over item to verify that the elements  
    // of mixedList are objects.  
    Console.WriteLine(item);  
} 
// The following loop sums the squares of the first group of boxed  
// integers in mixedList. The list elements are objects, and cannot  
// be multiplied or added to the sum until they are unboxed. The  
// unboxing must be done explicitly.  
var sum = 0; 
for (var j = 1; j < 5; j++) 
{ 
    // The following statement causes a compiler error: Operator  
    // '*' cannot be applied to operands of type 'object' and  
    // 'object'.  
    //sum += mixedList[j] * mixedList[j]);  
    // After the list elements are unboxed, the computation does  
    // not cause a compiler error.  
    sum += ( int)mixedList[j] * ( int)mixedList[j];  
} 
// The sum displayed is 30, the sum of 1 + 4 + 9 + 16.  
Console.WriteLine( "Sum: " + sum);
// Output:  
// Answer42True  
// First Group:  
// 1 
// 2 
// 3 
// 4 
// Second Group:  
// 5 
// 6 In relation to simple assignments, boxing and unboxing are computationally expensive
processes. When a value type is boxed, a new object must be allocated and constructed.
To a lesser degree, the cast required for unboxing is also expensive computationally. For
more information, see Performance .
Boxing is used to store value types in the garbage-collected heap. Boxing is an implicit
conversion of a value type  to the type object or to any interface type implemented by
this value type. Boxing a value type allocates an object instance on the heap and copies
the value into the new object.
Consider the following declaration of a value-type variable:
C#
The following statement implicitly applies the boxing operation on the variable i:
C#
The result of this statement is creating an object reference o, on the stack, that
references a value of the type int, on the heap. This value is a copy of the value-type
value assigned to the variable i. The difference between the two variables, i and o, is
illustrated in the following image of boxing conversion:// 7 
// 8 
// 9 
// Sum: 30  
Performance
Boxing
int i = 123; 
// Boxing copies the value of i into object o.  
object o = i; It is also possible to perform the boxing explicitly as in the following example, but
explicit boxing is never required:
C#
This example converts an integer variable i to an object o by using boxing. Then, the
value stored in the variable i is changed from 123 to 456. The example shows that the
original value type and the boxed object use separate memory locations, and therefore
can store different values.
C#int i = 123; 
object o = (object)i;  // explicit boxing  
Example
class TestBoxing  
{ 
    static void Main() 
    { 
        int i = 123; 
        // Boxing copies the value of i into object o.  
        object o = i; 
        // Change the value of i.
        i = 456; 
        // The change in i doesn't affect the value stored in o.  
        System.Console.WriteLine( "The value-type value = {0}" , i);
        System.Console.WriteLine( "The object-type value = {0}" , o); 
    } 
} 
/* Output:  
    The value-type value = 456  
    The object-type value = 123  
*/ Unboxing is an explicit conversion from the type object to a value type  or from an
interface type to a value type that implements the interface. An unboxing operation
consists of:
Checking the object instance to make sure that it is a boxed value of the given
value type.
Copying the value from the instance into the value-type variable.
The following statements demonstrate both boxing and unboxing operations:
C#
The following figure demonstrates the result of the previous statements:
For the unboxing of value types to succeed at run time, the item being unboxed must
be a reference to an object that was previously created by boxing an instance of that
value type. Attempting to unbox null causes a NullR eferenceException . Attempting to
unbox a reference to an incompatible value type causes an InvalidCastException .
The following example demonstrates a case of invalid unboxing and the resulting
InvalidCastException. Using try and catch, an error message is displayed when the
error occurs.
C#Unboxing
int i = 123;      // a value type  
object o = i;     // boxing  
int j = (int)o;   // unboxing  
ExampleThis program outputs:
Specified cast is not valid. Error: Incorrect unboxing.
If you change the statement:
C#
to:
C#
the conversion will be performed, and you will get the output:
Unboxing OK.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.class TestUnboxing  
{ 
    static void Main() 
    { 
        int i = 123; 
        object o = i;  // implicit boxing  
        try 
        {  
            int j = (short)o;  // attempt to unbox  
            System.Console.WriteLine( "Unboxing OK." ); 
        }  
        catch (System.InvalidCastException e)  
        {  
            System.Console.WriteLine( "{0} Error: Incorrect unboxing." , 
e.Message);  
        }  
    } 
} 
int j = (short)o; 
int j = (int)o; 
C# language specificationC# programming guide
Reference types
Value typesSee alsoHow to convert a byte array to an int
(C# Programming Guide)
Article •09/23/2021
This example shows you how to use the BitConverter  class to convert an array of bytes
to an int and back to an array of bytes. Y ou may have to convert from bytes to a built-in
data type after you read bytes off the network, for example. In addition to the
ToInt32(Byte[], Int32)  method in the example, the following table lists methods in the
BitConverter  class that convert bytes (from an array of bytes) to other built-in types.
Type r eturned Method
bool ToBoolean(Byte[], Int32)
char ToChar(Byte[], Int32)
double ToDouble(Byte[], Int32)
short ToInt16(Byte[], Int32)
int ToInt32(Byte[], Int32)
long ToInt64(Byte[], Int32)
float ToSingle(Byte[], Int32)
ushort ToUInt16(Byte[], Int32)
uint ToUInt32(Byte[], Int32)
ulong ToUInt64(Byte[], Int32)
This example initializes an array of bytes, reverses the array if the computer architecture
is little-endian (that is, the least significant byte is stored first), and then calls the
ToInt32(Byte[], Int32)  method to convert four bytes in the array to an int. The second
argument to ToInt32(Byte[], Int32)  specifies the start index of the array of bytes.Examples
７ Note
The output may differ depending on the endianness of your computer's
architecture.C#
In this example, the GetBytes(Int32)  method of the BitConverter  class is called to convert
an int to an array of bytes.
C#
BitConverter
IsLittleEndian
Typesbyte[] bytes = { 0, 0, 0, 25 }; 
// If the system architecture is little-endian (that is, little end first),  
// reverse the byte array.  
if (BitConverter.IsLittleEndian)  
    Array.Reverse(bytes);  
int i = BitConverter.ToInt32(bytes, 0); 
Console.WriteLine( "int: {0}" , i);
// Output: int: 25  
７ Note
The output may differ depending on the endianness of your computer's
architecture.
byte[] bytes = BitConverter.GetBytes( 201805978 ); 
Console.WriteLine( "byte array: "  + BitConverter.ToString(bytes));  
// Output: byte array: 9A-50-07-0C  
See alsoHow to convert a string to a number
(C# Programming Guide)
Article •05/27/2022
You convert a string to a number by calling the Parse or TryParse method found on
numeric types ( int, long, double, and so on), or by using methods in the
System.Convert  class.
It's slightly more efficient and straightforward to call a TryParse method (for example,
int.TryParse("11", out number) ) or Parse method (for example, var number =
int.Parse("11") ). Using a Convert  method is more useful for general objects that
implement IConvertible .
You use Parse or TryParse methods on the numeric type you expect the string contains,
such as the System.Int32  type. The Convert.T oInt32  method uses Parse internally. The
Parse method returns the converted number; the TryParse method returns a boolean
value that indicates whether the conversion succeeded, and returns the converted
number in an out parameter. If the string isn't in a valid format, Parse throws an
exception, but TryParse returns false. When calling a Parse method, you should
always use exception handling to catch a FormatException  when the parse operation
fails.
The Parse and TryParse methods ignore white space at the beginning and at the end
of the string, but all other characters must be characters that form the appropriate
numeric type ( int, long, ulong, float, decimal, and so on). Any white space within the
string that forms the number causes an error. For example, you can use
decimal.TryParse to parse "10", "10.3", or " 10 ", but you can't use this method to parse
10 from "10X", "1 0" (note the embedded space), "10 .3" (note the embedded space),
"10e1" ( float.TryParse works here), and so on. A string whose value is null or
String.Empty  fails to parse successfully. Y ou can check for a null or empty string before
attempting to parse it by calling the String.IsNullOrEmpty  method.
The following example demonstrates both successful and unsuccessful calls to Parse
and TryParse.
C#Call Parse or TryParse methodsusing System;  
public static class StringConversion  
{ 
    public static void Main() 
    { 
        string input = String.Empty;  
        try 
        {  
            int result = Int32.Parse(input);  
            Console.WriteLine(result);  
        }  
        catch (FormatException)  
        {  
            Console.WriteLine( $"Unable to parse ' {input}'"); 
        }  
        // Output: Unable to parse ''  
        try 
        {  
            int numVal = Int32.Parse( "-105"); 
            Console.WriteLine(numVal);  
        }  
        catch (FormatException e)
        {  
            Console.WriteLine(e.Message);  
        }  
        // Output: -105  
        if (Int32.TryParse( "-105", out int j))
        {  
            Console.WriteLine(j);
        }  
        else 
        {  
            Console.WriteLine( "String could not be parsed." ); 
        }  
        // Output: -105  
        try 
        {  
            int m = Int32.Parse( "abc"); 
        }  
        catch (FormatException e)
        {  
            Console.WriteLine(e.Message);  
        }  
        // Output: Input string was not in a correct format.  
        const string inputString = "abc"; 
        if (Int32.TryParse(inputString, out int numValue))  
        {  
            Console.WriteLine(numValue);  
        }  The following example illustrates one approach to parsing a string expected to include
leading numeric characters (including hexadecimal characters) and trailing non-numeric
characters. It assigns valid characters from the beginning of a string to a new string
before calling the TryParse method. Because the strings to be parsed contain a few
characters, the example calls the String.Concat  method to assign valid characters to a
new string. For a larger string, the StringBuilder  class can be used instead.
C#        else 
        {  
            Console.WriteLine( $"Int32.TryParse could not parse  
'{inputString} ' to an int." ); 
        }  
        // Output: Int32.TryParse could not parse 'abc' to an int.  
    } 
} 
using System;  
public static class StringConversion  
{ 
    public static void Main() 
    { 
        var str = "  10FFxxx" ; 
        string numericString = string.Empty; 
        foreach (var c in str) 
        {  
            // Check for numeric characters (hex in this case) or leading or  
trailing spaces.  
            if ((c >= '0' && c <= '9') || (char.ToUpperInvariant(c) >= 'A' 
&& char.ToUpperInvariant(c) <= 'F') || c == ' ') 
            {  
                numericString = string.Concat(numericString, c.ToString());  
            }  
            else 
            {  
                break; 
            }  
        }  
        if (int.TryParse(numericString,  
System.Globalization.NumberStyles.HexNumber, null, out int i)) 
        {  
            Console.WriteLine( $"'{str}' --> '{numericString} ' --> {i}"); 
        }  
        // Output: '  10FFxxx' --> '  10FF' --> 4351  
        str = "   -10FFXXX" ; 
        numericString = ""; 
        foreach (char c in str) The following table lists some of the methods from the Convert  class that you can use to
convert a string to a number.
Numer ic type Method
decimal ToDecimal(S tring)
float ToSingle(S tring)
double ToDouble(S tring)
short ToInt16(S tring)
int ToInt32(S tring)
long ToInt64(S tring)
ushort ToUInt16(S tring)
uint ToUInt32(S tring)
ulong ToUInt64(S tring)
The following example calls the Convert.T oInt32(S tring)  method to convert an input
string to an int. The example catches the two most common exceptions that can be
thrown by this method, FormatException  and OverflowException . If the resulting        {  
            // Check for numeric characters (0-9), a negative sign, or  
leading or trailing spaces.  
            if ((c >= '0' && c <= '9') || c == ' ' || c == '-') 
            {  
                numericString = string.Concat(numericString, c);  
            }  
            else 
            {  
                break; 
            }  
        }  
        if (int.TryParse(numericString, out int j)) 
        {  
            Console.WriteLine( $"'{str}' --> '{numericString} ' --> {j}"); 
        }  
        // Output: '   -10FFXXX' --> '   -10' --> -10  
    } 
} 
Call Convert methodsnumber can be incremented without exceeding Int32.MaxV alue, the example adds 1 to
the result and displays the output.
C#
using System;  
public class ConvertStringExample1  
{ 
    static void Main(string[] args) 
    { 
        int numVal = -1; 
        bool repeat = true; 
        while (repeat)  
        {  
            Console.Write( "Enter a number between −2,147,483,648 and  
+2,147,483,647 (inclusive): " ); 
            string? input = Console.ReadLine();  
            // ToInt32 can throw FormatException or OverflowException.  
            try 
            {  
                numVal = Convert.ToInt32(input);  
                if (numVal < Int32.MaxValue)  
                {  
                    Console.WriteLine( "The new value is {0}" , ++numVal);  
                }  
                else 
                {  
                    Console.WriteLine( "numVal cannot be incremented beyond  
its current value" ); 
                }  
           }  
            catch (FormatException)  
            {  
                Console.WriteLine( "Input string is not a sequence of  
digits." ); 
            }  
            catch (OverflowException)  
            {  
                Console.WriteLine( "The number cannot fit in an Int32." ); 
            }  
            Console.Write( "Go again? Y/N: " ); 
            string? go = Console.ReadLine();  
            if (go?.ToUpper() != "Y") 
            {  
                repeat = false; 
            }  
        }  
    } 
} // Sample Output:  
//   Enter a number between -2,147,483,648 and +2,147,483,647 (inclusive):  
473 
//   The new value is 474  
//   Go again? Y/N: y  
//   Enter a number between -2,147,483,648 and +2,147,483,647 (inclusive):  
2147483647  
//   numVal cannot be incremented beyond its current value  
//   Go again? Y/N: y  
//   Enter a number between -2,147,483,648 and +2,147,483,647 (inclusive):  
-1000 
//   The new value is -999  
//   Go again? Y/N: n  How to convert between hexadecimal
strings and numeric types (C#
Programming Guide)
Article •10/12/2021
These examples show you how to perform the following tasks:
Obtain the hexadecimal value of each character in a string .
Obtain the char that corresponds to each value in a hexadecimal string.
Convert a hexadecimal string to an int.
Convert a hexadecimal string to a float.
Convert a byte array to a hexadecimal string.
This example outputs the hexadecimal value of each character in a string. First it parses
the string to an array of characters. Then it calls ToInt32(Char)  on each character to
obtain its numeric value. Finally, it formats the number as its hexadecimal representation
in a string.
C#Examples
string input = "Hello World!" ;
char[] values = input.ToCharArray();
foreach (char letter in values)
{
    // Get the integral value of the character.
    int value = Convert.ToInt32(letter);
    // Convert the integer value to a hexadecimal value in string form.
    Console.WriteLine( $"Hexadecimal value of {letter}  is {value:X}");
}
/* Output:
    Hexadecimal value of H is 48
    Hexadecimal value of e is 65
    Hexadecimal value of l is 6C
    Hexadecimal value of l is 6C
    Hexadecimal value of o is 6F
    Hexadecimal value of   is 20
    Hexadecimal value of W is 57
    Hexadecimal value of o is 6FThis example parses a string of hexadecimal values and outputs the character
corresponding to each hexadecimal value. First it calls the Split(Char[])  method to obtain
each hexadecimal value as an individual string in an array. Then it calls ToInt32(S tring,
Int32)  to convert the hexadecimal value to a decimal value represented as an int. It
shows two different ways to obtain the character corresponding to that character code.
The first technique uses ConvertFromUtf32(Int32) , which returns the character
corresponding to the integer argument as a string. The second technique explicitly
casts the int to a char.
C#
This example shows another way to convert a hexadecimal string to an integer, by
calling the Parse(S tring, NumberS tyles)  method.    Hexadecimal value of r is 72
    Hexadecimal value of l is 6C
    Hexadecimal value of d is 64
    Hexadecimal value of ! is 21
 */
string hexValues = "48 65 6C 6C 6F 20 57 6F 72 6C 64 21" ;
string[] hexValuesSplit = hexValues.Split( ' ');
foreach (string hex in hexValuesSplit)
{
    // Convert the number expressed in base-16 to an integer.
    int value = Convert.ToInt32(hex, 16);
    // Get the character corresponding to the integral value.
    string stringValue = Char.ConvertFromUtf32( value);
    char charValue = ( char)value;
    Console.WriteLine( "hexadecimal value = {0}, int value = {1}, char value  
= {2} or {3}" ,
                        hex, value, stringValue, charValue);
}
/* Output:
    hexadecimal value = 48, int value = 72, char value = H or H
    hexadecimal value = 65, int value = 101, char value = e or e
    hexadecimal value = 6C, int value = 108, char value = l or l
    hexadecimal value = 6C, int value = 108, char value = l or l
    hexadecimal value = 6F, int value = 111, char value = o or o
    hexadecimal value = 20, int value = 32, char value =   or
    hexadecimal value = 57, int value = 87, char value = W or W
    hexadecimal value = 6F, int value = 111, char value = o or o
    hexadecimal value = 72, int value = 114, char value = r or r
    hexadecimal value = 6C, int value = 108, char value = l or l
    hexadecimal value = 64, int value = 100, char value = d or d
    hexadecimal value = 21, int value = 33, char value = ! or !
*/C#
The following example shows how to convert a hexadecimal string to a float by using
the System.BitConverter  class and the UInt32.P arse method.
C#
The following example shows how to convert a byte array to a hexadecimal string by
using the System.BitConverter  class.
C#
The following example shows how to convert a byte array to a hexadecimal string by
calling the Convert.T oHexS tring  method introduced in .NET 5.0.
C#string hexString = "8E2";
int num = Int32.Parse(hexString,  
System.Globalization.NumberStyles.HexNumber);
Console.WriteLine(num);
//Output: 2274
string hexString = "43480170" ;
uint num = uint.Parse(hexString,  
System.Globalization.NumberStyles.AllowHexSpecifier);
byte[] floatVals = BitConverter.GetBytes(num);
float f = BitConverter.ToSingle(floatVals, 0);
Console.WriteLine( "float convert = {0}" , f);
// Output: 200.0056
byte[] vals = { 0x01, 0xAA, 0xB1, 0xDC, 0x10, 0xDD };
string str = BitConverter.ToString(vals);
Console.WriteLine(str);
str = BitConverter.ToString(vals).Replace( "-", "");
Console.WriteLine(str);
/*Output:
  01-AA-B1-DC-10-DD
  01AAB1DC10DD
 */Standard Numeric Format S trings
Types
How to determine whether a string represents a numeric valuebyte[] array = { 0x64, 0x6f, 0x74, 0x63, 0x65, 0x74 };
string hexValue = Convert.ToHexString(array);
Console.WriteLine(hexValue);
/*Output:
  646F74636574
 */
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
 Provide product feedbackVersioning with the Override and New
Keywords (C# Programming Guide)
Article •10/27/2021
The C# language is designed so that versioning between base and derived classes in
different libraries can evolve and maintain backward compatibility. This means, for
example, that the introduction of a new member in a base class  with the same name as
a member in a derived class is completely supported by C# and does not lead to
unexpected behavior. It also means that a class must explicitly state whether a method is
intended to override an inherited method, or whether a method is a new method that
hides a similarly named inherited method.
In C#, derived classes can contain methods with the same name as base class methods.
If the method in the derived class is not preceded by new or override  keywords,
the compiler will issue a warning and the method will behave as if the new
keyword were present.
If the method in the derived class is preceded with the new keyword, the method is
defined as being independent of the method in the base class.
If the method in the derived class is preceded with the override keyword, objects
of the derived class will call that method instead of the base class method.
In order to apply the override keyword to the method in the derived class, the
base class method must be defined virtual .
The base class method can be called from within the derived class using the base
keyword.
The override, virtual, and new keywords can also be applied to properties,
indexers, and events.
By default, C# methods are not virtual. If a method is declared as virtual, any class
inheriting the method can implement its own version. T o make a method virtual, the
virtual modifier is used in the method declaration of the base class. The derived class
can then override the base virtual method by using the override keyword or hide the
virtual method in the base class by using the new keyword. If neither the override
keyword nor the new keyword is specified, the compiler will issue a warning and the
method in the derived class will hide the method in the base class.To demonstrate this in practice, assume for a moment that Company A has created a
class named GraphicsClass, which your program uses. The following is GraphicsClass:
C#
Your company uses this class, and you use it to derive your own class, adding a new
method:
C#
Your application is used without problems, until Company A releases a new version of
GraphicsClass, which resembles the following code:
C#
The new version of GraphicsClass now contains a method named DrawRectangle.
Initially, nothing occurs. The new version is still binary compatible with the old version.
Any software that you have deployed will continue to work, even if the new class is
installed on those computer systems. Any existing calls to the method DrawRectangle
will continue to reference your version, in your derived class.
However, as soon as you recompile your application by using the new version of
GraphicsClass, you will receive a warning from the compiler, CS0108. This warning
informs you that you have to consider how you want your DrawRectangle method to
behave in your application.class GraphicsClass  
{ 
    public virtual void DrawLine () { } 
    public virtual void DrawPoint () { } 
} 
class YourDerivedGraphicsClass  : GraphicsClass  
{ 
    public void DrawRectangle () { } 
} 
class GraphicsClass  
{ 
    public virtual void DrawLine () { } 
    public virtual void DrawPoint () { } 
    public virtual void DrawRectangle () { } 
} If you want your method to override the new base class method, use the override
keyword:
C#
The override keyword makes sure that any objects derived from
YourDerivedGraphicsClass will use the derived class version of DrawRectangle. Objects
derived from YourDerivedGraphicsClass can still access the base class version of
DrawRectangle by using the base keyword:
C#
If you do not want your method to override the new base class method, the following
considerations apply. T o avoid confusion between the two methods, you can rename
your method. This can be time-consuming and error-prone, and just not practical in
some cases. However, if your project is relatively small, you can use Visual S tudio's
Refactoring options to rename the method. For more information, see Refactoring
Classes and T ypes (Class Designer) .
Alternatively, you can prevent the warning by using the keyword new in your derived
class definition:
C#
Using the new keyword tells the compiler that your definition hides the definition that is
contained in the base class. This is the default behavior.
When a method is named on a class, the C# compiler selects the best method to call if
more than one method is compatible with the call, such as when there are two methodsclass YourDerivedGraphicsClass  : GraphicsClass  
{ 
    public override  void DrawRectangle () { } 
} 
base.DrawRectangle();  
class YourDerivedGraphicsClass  : GraphicsClass  
{ 
    public new void DrawRectangle () { } 
} 
Override and Method Selectionwith the same name, and parameters that are compatible with the parameter passed.
The following methods would be compatible:
C#
When DoWork is called on an instance of Derived, the C# compiler will first try to make
the call compatible with the versions of DoWork declared originally on Derived. Override
methods are not considered as declared on a class, they are new implementations of a
method declared on a base class. Only if the C# compiler cannot match the method call
to an original method on Derived, it will try to match the call to an overridden method
with the same name and compatible parameters. For example:
C#
Because the variable val can be converted to a double implicitly, the C# compiler calls
DoWork(double) instead of DoWork(int). There are two ways to avoid this. First, avoid
declaring new methods with the same name as virtual methods. Second, you can
instruct the C# compiler to call the virtual method by making it search the base class
method list by casting the instance of Derived to Base. Because the method is virtual,
the implementation of DoWork(int) on Derived will be called. For example:
C#
For more examples of new and override, see Knowing When to Use Override and New
Keywords .
C# Programming Guide
The C# type systempublic class Derived : Base 
{ 
    public override  void DoWork(int param) { } 
    public void DoWork(double param) { } 
} 
int val = 5; 
Derived d = new Derived();  
d.DoWork(val);  // Calls DoWork(double).  
((Base)d).DoWork(val);  // Calls DoWork(int) on Derived.  
See alsoMethods
InheritanceKnowing When to Use Override and
New Keywords (C# Programming Guide)
Article •10/27/2021
In C#, a method in a derived class can have the same name as a method in the base
class. Y ou can specify how the methods interact by using the new and override
keywords. The override modifier extends the base class virtual method, and the new
modifier hides  an accessible base class method. The difference is illustrated in the
examples in this topic.
In a console application, declare the following two classes, BaseClass and DerivedClass.
DerivedClass inherits from BaseClass.
C#
In the Main method, declare variables bc, dc, and bcdc.
bc is of type BaseClass, and its value is of type BaseClass.
dc is of type DerivedClass, and its value is of type DerivedClass.
bcdc is of type BaseClass, and its value is of type DerivedClass. This is the variable
to pay attention to.
Because bc and bcdc have type BaseClass, they can only directly access Method1, unless
you use casting. V ariable dc can access both Method1 and Method2. These relationships
are shown in the following code.class BaseClass    
{   
    public void Method1()   
    {   
        Console.WriteLine( "Base - Method1" );   
    }   
}   
   
class DerivedClass  : BaseClass    
{   
    public void Method2()   
    {   
        Console.WriteLine( "Derived - Method2" );   
    }   
}   C#
Next, add the following Method2 method to BaseClass. The signature of this method
matches the signature of the Method2 method in DerivedClass.
C#
Because BaseClass now has a Method2 method, a second calling statement can be
added for BaseClass variables bc and bcdc, as shown in the following code.
C#
When you build the project, you see that the addition of the Method2 method in
BaseClass causes a warning. The warning says that the Method2 method in
DerivedClass hides the Method2 method in BaseClass. You are advised to use the new
keyword in the Method2 definition if you intend to cause that result. Alternatively, youclass Program   
{   
    static void Main(string[] args)   
    {   
        BaseClass bc = new BaseClass();   
        DerivedClass dc = new DerivedClass();   
        BaseClass bcdc = new DerivedClass();   
   
        bc.Method1();   
        dc.Method1();   
        dc.Method2();   
        bcdc.Method1();   
    }   
    // Output:   
    // Base - Method1   
    // Base - Method1   
    // Derived - Method2   
    // Base - Method1   
}   
public void Method2()   
{   
    Console.WriteLine( "Base - Method2" );   
}   
bc.Method1();   
bc.Method2();   
dc.Method1();   
dc.Method2();   
bcdc.Method1();   
bcdc.Method2();   could rename one of the Method2 methods to resolve the warning, but that is not always
practical.
Before adding new, run the program to see the output produced by the additional
calling statements. The following results are displayed.
C#
The new keyword preserves the relationships that produce that output, but it suppresses
the warning. The variables that have type BaseClass continue to access the members of
BaseClass, and the variable that has type DerivedClass continues to access members in
DerivedClass first, and then to consider members inherited from BaseClass.
To suppress the warning, add the new modifier to the definition of Method2 in
DerivedClass, as shown in the following code. The modifier can be added before or
after public.
C#
Run the program again to verify that the output has not changed. Also verify that the
warning no longer appears. By using new, you are asserting that you are aware that the
member that it modifies hides a member that is inherited from the base class. For more
information about name hiding through inheritance, see new Modifier .
To contrast this behavior to the effects of using override, add the following method to
DerivedClass. The override modifier can be added before or after public.
C#// Output:   
// Base - Method1   
// Base - Method2   
// Base - Method1   
// Derived - Method2   
// Base - Method1   
// Base - Method2   
public new void Method2()   
{   
    Console.WriteLine( "Derived - Method2" );   
}   
public override  void Method1()   
{   Add the virtual modifier to the definition of Method1 in BaseClass. The virtual
modifier can be added before or after public.
C#
Run the project again. Notice especially the last two lines of the following output.
C#
The use of the override modifier enables bcdc to access the Method1 method that is
defined in DerivedClass. Typically, that is the desired behavior in inheritance hierarchies.
You want objects that have values that are created from the derived class to use the
methods that are defined in the derived class. Y ou achieve that behavior by using
override to extend the base class method.
The following code contains the full example.
C#    Console.WriteLine( "Derived - Method1" );   
}   
public virtual void Method1()   
{   
    Console.WriteLine( "Base - Method1" );   
}   
// Output:   
// Base - Method1   
// Base - Method2   
// Derived - Method1   
// Derived - Method2   
// Derived - Method1   
// Base - Method2   
using System;   
using System.Text;   
   
namespace  OverrideAndNew    
{   
    class Program   
    {   
        static void Main(string[] args)   
        {   
            BaseClass bc = new BaseClass();   
            DerivedClass dc = new DerivedClass();   
            BaseClass bcdc = new DerivedClass();   
               // The following two calls do what you would expect. They call   
            // the methods that are defined in BaseClass.   
            bc.Method1();   
            bc.Method2();   
            // Output:   
            // Base - Method1   
            // Base - Method2   
   
            // The following two calls do what you would expect. They call   
            // the methods that are defined in DerivedClass.   
            dc.Method1();   
            dc.Method2();   
            // Output:   
            // Derived - Method1   
            // Derived - Method2   
   
            // The following two calls produce different results, depending  
            // on whether override (Method1) or new (Method2) is used.   
            bcdc.Method1();   
            bcdc.Method2();   
            // Output:   
            // Derived - Method1   
            // Base - Method2   
        }   
    }   
   
    class BaseClass    
    {   
        public virtual void Method1()   
        {   
            Console.WriteLine( "Base - Method1" );   
        }   
   
        public virtual void Method2()   
        {   
            Console.WriteLine( "Base - Method2" );   
        }   
    }   
   
    class DerivedClass  : BaseClass    
    {   
        public override  void Method1()   
        {   
            Console.WriteLine( "Derived - Method1" );   
        }   
   
        public new void Method2()   
        {   
            Console.WriteLine( "Derived - Method2" );   
        }   
    }   
}   The following example illustrates similar behavior in a different context. The example
defines three classes: a base class named Car and two classes that are derived from it,
ConvertibleCar and Minivan. The base class contains a DescribeCar method. The
method displays a basic description of a car, and then calls ShowDetails to provide
additional information. Each of the three classes defines a ShowDetails method. The new
modifier is used to define ShowDetails in the ConvertibleCar class. The override
modifier is used to define ShowDetails in the Minivan class.
C#
// Define the base class, Car. The class defines two methods,   
// DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each  
derived   
// class also defines a ShowDetails method. The example tests which version  
of   
// ShowDetails is selected, the base class method or the derived class  
method.   
class Car   
{   
    public void DescribeCar ()   
    {   
        System.Console.WriteLine( "Four wheels and an engine." );   
        ShowDetails();   
    }   
   
    public virtual void ShowDetails ()   
    {   
        System.Console.WriteLine( "Standard transportation." );   
    }   
}   
   
// Define the derived classes.   
   
// Class ConvertibleCar uses the new modifier to acknowledge that  
ShowDetails   
// hides the base class method.  
class ConvertibleCar  : Car   
{   
    public new void ShowDetails ()   
    {   
        System.Console.WriteLine( "A roof that opens up." );   
    }   
}   
   
// Class Minivan uses the override modifier to specify that ShowDetails   
// extends the base class method.   
class Minivan : Car   
{   
    public override  void ShowDetails ()   
    {   
        System.Console.WriteLine( "Carries seven people." );   The example tests which version of ShowDetails is called. The following method,
TestCars1, declares an instance of each class, and then calls DescribeCar on each
instance.
C#
TestCars1 produces the following output. Notice especially the results for car2, which
probably are not what you expected. The type of the object is ConvertibleCar, but
DescribeCar does not access the version of ShowDetails that is defined in the
ConvertibleCar class because that method is declared with the new modifier, not the
override modifier. As a result, a ConvertibleCar object displays the same description as
a Car object. Contrast the results for car3, which is a Minivan object. In this case, the
ShowDetails method that is declared in the Minivan class overrides the ShowDetails
method that is declared in the Car class, and the description that is displayed describes
a minivan.
C#    }   
}   
public static void TestCars1 ()   
{   
    System.Console.WriteLine( "\nTestCars1" );   
    System.Console.WriteLine( "----------" );   
   
    Car car1 = new Car();   
    car1.DescribeCar();   
    System.Console.WriteLine( "----------" );   
   
    // Notice the output from this test case. The new modifier is   
    // used in the definition of ShowDetails in the ConvertibleCar   
    // class.  
   
    ConvertibleCar car2 = new ConvertibleCar();   
    car2.DescribeCar();   
    System.Console.WriteLine( "----------" );   
   
    Minivan car3 = new Minivan();   
    car3.DescribeCar();   
    System.Console.WriteLine( "----------" );   
}   
// TestCars1   
// ----------   
// Four wheels and an engine.   
// Standard transportation.   TestCars2 creates a list of objects that have type Car. The values of the objects are
instantiated from the Car, ConvertibleCar, and Minivan classes. DescribeCar is called
on each element of the list. The following code shows the definition of TestCars2.
C#
The following output is displayed. Notice that it is the same as the output that is
displayed by TestCars1. The ShowDetails method of the ConvertibleCar class is not
called, regardless of whether the type of the object is ConvertibleCar, as in TestCars1,
or Car, as in TestCars2. Conversely, car3 calls the ShowDetails method from the
Minivan class in both cases, whether it has type Minivan or type Car.
C#// ----------   
// Four wheels and an engine.   
// Standard transportation.   
// ----------   
// Four wheels and an engine.   
// Carries seven people.   
// ----------   
public static void TestCars2 ()   
{   
    System.Console.WriteLine( "\nTestCars2" );   
    System.Console.WriteLine( "----------" );   
   
    var cars = new List<Car> { new Car(), new ConvertibleCar(),  
        new Minivan() };   
   
    foreach (var car in cars)   
    {   
        car.DescribeCar();   
        System.Console.WriteLine( "----------" );   
    }   
}   
// TestCars2   
// ----------   
// Four wheels and an engine.   
// Standard transportation.   
// ----------   
// Four wheels and an engine.   
// Standard transportation.   
// ----------   
// Four wheels and an engine.   
// Carries seven people.   
// ----------   Methods TestCars3 and TestCars4 complete the example. These methods call
ShowDetails directly, first from objects declared to have type ConvertibleCar and
Minivan (TestCars3), then from objects declared to have type Car (TestCars4). The
following code defines these two methods.
C#
The methods produce the following output, which corresponds to the results from the
first example in this topic.
C#
The following code shows the complete project and its output.
C#public static void TestCars3 ()   
{   
    System.Console.WriteLine( "\nTestCars3" );   
    System.Console.WriteLine( "----------" );   
    ConvertibleCar car2 = new ConvertibleCar();   
    Minivan car3 = new Minivan();   
    car2.ShowDetails();   
    car3.ShowDetails();   
}   
   
public static void TestCars4 ()   
{   
    System.Console.WriteLine( "\nTestCars4" );   
    System.Console.WriteLine( "----------" );   
    Car car2 = new ConvertibleCar();   
    Car car3 = new Minivan();   
    car2.ShowDetails();   
    car3.ShowDetails();   
}   
// TestCars3   
// ----------   
// A roof that opens up.   
// Carries seven people.   
   
// TestCars4   
// ----------   
// Standard transportation.   
// Carries seven people.   
using System;   
using System.Collections.Generic;   
using System.Linq;   using System.Text;   
   
namespace  OverrideAndNew2    
{   
    class Program   
    {   
        static void Main(string[] args)   
        {   
            // Declare objects of the derived classes and test which version    
            // of ShowDetails is run, base or derived.   
            TestCars1();   
   
            // Declare objects of the base class, instantiated with the   
            // derived classes, and repeat the tests.   
            TestCars2();   
   
            // Declare objects of the derived classes and call ShowDetails   
            // directly.   
            TestCars3();   
   
            // Declare objects of the base class, instantiated with the   
            // derived classes, and repeat the tests.   
            TestCars4();   
        }   
   
        public static void TestCars1 ()   
        {   
            System.Console.WriteLine( "\nTestCars1" );   
            System.Console.WriteLine( "----------" );   
   
            Car car1 = new Car();   
            car1.DescribeCar();  
            System.Console.WriteLine( "----------" );   
   
            // Notice the output from this test case. The new modifier is   
            // used in the definition of ShowDetails in the ConvertibleCar   
            // class.  
            ConvertibleCar car2 = new ConvertibleCar();   
            car2.DescribeCar();  
            System.Console.WriteLine( "----------" );   
   
            Minivan car3 = new Minivan();   
            car3.DescribeCar();  
            System.Console.WriteLine( "----------" );   
        }   
        // Output:   
        // TestCars1   
        // ----------   
        // Four wheels and an engine.   
        // Standard transportation.   
        // ----------   
        // Four wheels and an engine.   
        // Standard transportation.   
        // ----------   
        // Four wheels and an engine.           // Carries seven people.   
        // ----------   
   
        public static void TestCars2 ()   
        {   
            System.Console.WriteLine( "\nTestCars2" );   
            System.Console.WriteLine( "----------" );   
   
            var cars = new List<Car> { new Car(), new ConvertibleCar(),  
                new Minivan() };   
   
            foreach (var car in cars)   
            {   
                car.DescribeCar();   
                System.Console.WriteLine( "----------" );   
            }   
        }   
        // Output:   
        // TestCars2   
        // ----------   
        // Four wheels and an engine.   
        // Standard transportation.   
        // ----------   
        // Four wheels and an engine.   
        // Standard transportation.   
        // ----------   
        // Four wheels and an engine.   
        // Carries seven people.   
        // ----------   
   
        public static void TestCars3 ()   
        {   
            System.Console.WriteLine( "\nTestCars3" );   
            System.Console.WriteLine( "----------" );   
            ConvertibleCar car2 = new ConvertibleCar();   
            Minivan car3 = new Minivan();   
            car2.ShowDetails();  
            car3.ShowDetails();  
        }   
        // Output:   
        // TestCars3   
        // ----------   
        // A roof that opens up.   
        // Carries seven people.   
   
        public static void TestCars4 ()   
        {   
            System.Console.WriteLine( "\nTestCars4" );   
            System.Console.WriteLine( "----------" );   
            Car car2 = new ConvertibleCar();   
            Car car3 = new Minivan();   
            car2.ShowDetails();  
            car3.ShowDetails();  
        }   
        // Output:           // TestCars4   
        // ----------   
        // Standard transportation.   
        // Carries seven people.   
    }   
   
    // Define the base class, Car. The class defines two virtual methods,   
    // DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each  
derived   
    // class also defines a ShowDetails method. The example tests which  
version of   
    // ShowDetails is used, the base class method or the derived class  
method.   
    class Car   
    {   
        public virtual void DescribeCar ()   
        {   
            System.Console.WriteLine( "Four wheels and an engine." );   
            ShowDetails();   
        }   
   
        public virtual void ShowDetails ()   
        {   
            System.Console.WriteLine( "Standard transportation." );   
        }   
    }   
   
    // Define the derived classes.   
   
    // Class ConvertibleCar uses the new modifier to acknowledge that  
ShowDetails   
    // hides the base class method.   
    class ConvertibleCar  : Car   
    {   
        public new void ShowDetails ()   
        {   
            System.Console.WriteLine( "A roof that opens up." );   
        }   
    }   
   
    // Class Minivan uses the override modifier to specify that ShowDetails   
    // extends the base class method.   
    class Minivan : Car   
    {   
        public override  void ShowDetails ()   
        {   
            System.Console.WriteLine( "Carries seven people." );   
        }   
    }   
   
}   C# Programming Guide
The C# type system
Versioning with the Override and New K eywords
base
abstractSee alsoHow to override the ToString method
(C# Programming Guide)
Article •10/27/2021
Every class or struct in C# implicitly inherits the Object  class. Therefore, every object in
C# gets the ToString  method, which returns a string representation of that object. For
example, all variables of type int have a ToString method, which enables them to
return their contents as a string:
C#
When you create a custom class or struct, you should override the ToString  method in
order to provide information about your type to client code.
For information about how to use format strings and other types of custom formatting
with the ToString method, see Formatting T ypes.
To override the ToString method in your class or struct:
1. Declare a ToString method with the following modifiers and return type:
C#
2. Implement the method so that it returns a string.int x = 42; 
string strx = x.ToString();  
Console.WriteLine(strx);  
// Output:  
// 42 
） Impor tant
When you decide what information to provide through this method, consider
whether your class or struct will ever be used by untrusted code. Be careful to
ensure that you do not provide any information that could be exploited by
malicious code.
public override  string ToString (){}   The following example returns the name of the class in addition to the data
specific to a particular instance of the class.
C#
You can test the ToString method as shown in the following code example:
C#
IFormattable
C# Programming Guide
The C# type system
Strings
string
override
virtual
Formatting T ypesclass Person 
{ 
    public string Name { get; set; } 
    public int Age { get; set; } 
    public override  string ToString () 
    { 
        return "Person: "  + Name + " " + Age; 
    } 
} 
Person person = new Person { Name = "John", Age = 12 }; 
Console.WriteLine(person);  
// Output:  
// Person: John 12  
See alsoMembers (C# Programming Guide)
Article •09/17/2021
Classes and structs have members that represent their data and behavior. A class's
members include all the members declared in the class, along with all members (except
constructors and finalizers) declared in all classes in its inheritance hierarchy. Private
members in base classes are inherited but are not accessible from derived classes.
The following table lists the kinds of members a class or struct may contain:
Member Descr iption
Fields Fields are variables declared at class scope. A field may be a built-in numeric type
or an instance of another class. For example, a calendar class may have a field that
contains the current date.
Constants Constants are fields whose value is set at compile time and cannot be changed.
Properties Properties are methods on a class that are accessed as if they were fields on that
class. A property can provide protection for a class field to keep it from being
changed without the knowledge of the object.
Methods Methods define the actions that a class can perform. Methods can take parameters
that provide input data, and can return output data through parameters. Methods
can also return a value directly, without using a parameter.
Events Events provide notifications about occurrences, such as button clicks or the
successful completion of a method, to other objects. Events are defined and
triggered by using delegates.
Operators Overloaded operators are considered type members. When you overload an
operator, you define it as a public static method in a type. For more information,
see Operator overloading .
Indexers Indexers enable an object to be indexed in a manner similar to arrays.
Constructors Constructors are methods that are called when the object is first created. They are
often used to initialize the data of an object.
Finalizers Finalizers are used very rarely in C#. They are methods that are called by the
runtime execution engine when the object is about to be removed from memory.
They are generally used to make sure that any resources which must be released
are handled appropriately.
Nested
TypesNested types are types declared within another type. Nested types are often used
to describe objects that are used only by the types that contain them.C# Programming Guide
ClassesSee alsoAbstract and Sealed Classes and Class
Members (C# Programming Guide)
Article •10/27/2021
The abstract  keyword enables you to create classes and class  members that are
incomplete and must be implemented in a derived class.
The sealed  keyword enables you to prevent the inheritance of a class or certain class
members that were previously marked virtual .
Classes can be declared as abstract by putting the keyword abstract before the class
definition. For example:
C#
An abstract class cannot be instantiated. The purpose of an abstract class is to provide a
common definition of a base class that multiple derived classes can share. For example,
a class library may define an abstract class that is used as a parameter to many of its
functions, and require programmers using that library to provide their own
implementation of the class by creating a derived class.
Abstract classes may also define abstract methods. This is accomplished by adding the
keyword abstract before the return type of the method. For example:
C#
Abstract methods have no implementation, so the method definition is followed by a
semicolon instead of a normal method block. Derived classes of the abstract class must
implement all abstract methods. When an abstract class inherits a virtual method from aAbstract Classes and Class Members
public abstract  class A 
{ 
    // Class members here.  
} 
public abstract  class A 
{ 
    public abstract  void DoWork(int i); 
} base class, the abstract class can override the virtual method with an abstract method.
For example:
C#
If a virtual method is declared abstract, it is still virtual to any class inheriting from
the abstract class. A class inheriting an abstract method cannot access the original
implementation of the method—in the previous example, DoWork on class F cannot call
DoWork on class D. In this way, an abstract class can force derived classes to provide new
method implementations for virtual methods.
Classes can be declared as sealed  by putting the keyword sealed before the class
definition. For example:
C#
A sealed class cannot be used as a base class. For this reason, it cannot also be an
abstract class. Sealed classes prevent derivation. Because they can never be used as a// compile with: -target:library  
public class D 
{ 
    public virtual void DoWork(int i) 
    { 
        // Original implementation.  
    } 
} 
public abstract  class E : D 
{ 
    public abstract  override  void DoWork(int i); 
} 
public class F : E 
{ 
    public override  void DoWork(int i) 
    { 
        // New implementation.  
    } 
} 
Sealed Classes and Class Members
public sealed class D 
{ 
    // Class members here.  
} base class, some run-time optimizations can make calling sealed class members slightly
faster.
A method, indexer, property, or event, on a derived class that is overriding a virtual
member of the base class can declare that member as sealed. This negates the virtual
aspect of the member for any further derived class. This is accomplished by putting the
sealed keyword before the override  keyword in the class member declaration. For
example:
C#
C# Programming Guide
The C# type system
Inheritance
Methods
Fields
How to define abstract propertiespublic class D : C 
{ 
    public sealed override  void DoWork() { } 
} 
See alsoStatic Classes and Static Class Members
(C# Programming Guide)
Article •03/10/2023
A static  class is basically the same as a non-static class, but there is one difference: a
static class cannot be instantiated. In other words, you cannot use the new operator to
create a variable of the class type. Because there is no instance variable, you access the
members of a static class by using the class name itself. For example, if you have a static
class that is named UtilityClass that has a public static method named MethodA, you
call the method as shown in the following example:
C#
A static class can be used as a convenient container for sets of methods that just
operate on input parameters and do not have to get or set any internal instance fields.
For example, in the .NET Class Library, the static System.Math  class contains methods
that perform mathematical operations, without any requirement to store or retrieve data
that is unique to a particular instance of the Math  class. That is, you apply the members
of the class by specifying the class name and the method name, as shown in the
following example.
C#
As is the case with all class types, the type information for a static class is loaded by the
.NET runtime when the program that references the class is loaded. The program cannot
specify exactly when the class is loaded. However, it is guaranteed to be loaded and to
have its fields initialized and its static constructor called before the class is referenced
for the first time in your program. A static constructor is only called one time, and a
static class remains in memory for the lifetime of the application domain in which your
program resides.UtilityClass.MethodA();   
double dub = -3.14;   
Console.WriteLine(Math.Abs(dub));   
Console.WriteLine(Math.Floor(dub));   
Console.WriteLine(Math.Round(Math.Abs(dub)));   
   
// Output:   
// 3.14   
// -4   
// 3   The following list provides the main features of a static class:
Contains only static members.
Cannot be instantiated.
Is sealed.
Cannot contain Instance Constructors .
Creating a static class is therefore basically the same as creating a class that contains
only static members and a private constructor. A private constructor prevents the class
from being instantiated. The advantage of using a static class is that the compiler can
check to make sure that no instance members are accidentally added. The compiler will
guarantee that instances of this class cannot be created.
Static classes are sealed and therefore cannot be inherited. They cannot inherit from any
class or interface except Object . Static classes cannot contain an instance constructor.
However, they can contain a static constructor. Non-static classes should also define a
static constructor if the class contains static members that require non-trivial
initialization. For more information, see Static Constructors .
Here is an example of a static class that contains two methods that convert temperature
from Celsius to F ahrenheit and from F ahrenheit to Celsius:
C#７ Note
To create a non-static class that allows only one instance of itself to be created, see
Implementing Singlet on in C# .
Example
public static class TemperatureConverter  
{ 
    public static double CelsiusToFahrenheit (string temperatureCelsius ) 
    { 
        // Convert argument to double for calculations.  
        double celsius = Double.Parse(temperatureCelsius);  
        // Convert Celsius to Fahrenheit.  
        double fahrenheit = (celsius * 9 / 5) + 32; 
        return fahrenheit;      } 
    public static double FahrenheitToCelsius (string temperatureFahrenheit ) 
    { 
        // Convert argument to double for calculations.  
        double fahrenheit = Double.Parse(temperatureFahrenheit);  
        // Convert Fahrenheit to Celsius.  
        double celsius = (fahrenheit - 32) * 5 / 9; 
        return celsius;  
    } 
} 
class TestTemperatureConverter  
{ 
    static void Main() 
    { 
        Console.WriteLine( "Please select the convertor direction" ); 
        Console.WriteLine( "1. From Celsius to Fahrenheit." ); 
        Console.WriteLine( "2. From Fahrenheit to Celsius." ); 
        Console.Write( ":"); 
        string? selection = Console.ReadLine();  
        double F, C = 0; 
        switch (selection)  
        {  
            case "1": 
                Console.Write( "Please enter the Celsius temperature: " ); 
                F =  
TemperatureConverter.CelsiusToFahrenheit(Console.ReadLine() ?? "0"); 
                Console.WriteLine( "Temperature in Fahrenheit: {0:F2}" , F); 
                break; 
            case "2": 
                Console.Write( "Please enter the Fahrenheit temperature: " ); 
                C =  
TemperatureConverter.FahrenheitToCelsius(Console.ReadLine() ?? "0"); 
                Console.WriteLine( "Temperature in Celsius: {0:F2}" , C); 
                break; 
            default: 
                Console.WriteLine( "Please select a convertor." ); 
                break; 
        }  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Example Output:  
    Please select the convertor direction  
    1. From Celsius to Fahrenheit.  A non-static class can contain static methods, fields, properties, or events. The static
member is callable on a class even when no instance of the class has been created. The
static member is always accessed by the class name, not the instance name. Only one
copy of a static member exists, regardless of how many instances of the class are
created. S tatic methods and properties cannot access non-static fields and events in
their containing type, and they cannot access an instance variable of any object unless
it's explicitly passed in a method parameter.
It is more typical to declare a non-static class with some static members, than to declare
an entire class as static. T wo common uses of static fields are to keep a count of the
number of objects that have been instantiated, or to store a value that must be shared
among all instances.
Static methods can be overloaded but not overridden, because they belong to the class,
and not to any instance of the class.
Although a field cannot be declared as static const, a const  field is essentially static in
its behavior. It belongs to the type, not to instances of the type. Therefore, const fields
can be accessed by using the same ClassName.MemberName notation that's used for static
fields. No object instance is required.
C# does not support static local variables (that is, variables that are declared in method
scope).
You declare static class members by using the static keyword before the return type of
the member, as shown in the following example:
C#    2. From Fahrenheit to Celsius.  
    :2 
    Please enter the Fahrenheit temperature: 20  
    Temperature in Celsius: -6.67
    Press any key to exit.  
 */ 
Static Members
public class Automobile
{ 
    public static int NumberOfWheels = 4; 
    public static int SizeOfGasTank  
    { 
        get Static members are initialized before the static member is accessed for the first time and
before the static constructor, if there is one, is called. T o access a static class member,
use the name of the class instead of a variable name to specify the location of the
member, as shown in the following example:
C#
If your class contains static fields, provide a static constructor that initializes them when
the class is loaded.
A call to a static method generates a call instruction in Microsoft intermediate language
(MSIL), whereas a call to an instance method generates a callvirt instruction, which
also checks for null object references. However, most of the time the performance
difference between the two is not significant.
For more information, see Static classes , Static and instance members  and Static
constructors  in the C# Language Specification . The language specification is the
definitive source for C# syntax and usage.
C# Programming Guide
static
Classes
class
Static Constructors        {  
            return 15; 
        }  
    } 
    public static void Drive() { } 
    public static event EventType? RunOutOfGas;  
    // Other non-static fields and properties...  
} 
Automobile.Drive();  
int i = Automobile.NumberOfWheels;  
C# Language Specification
See alsoInstance ConstructorsAcces s Modifiers (C# Programming
Guide)
Article •11/10/2023
All types and type members have an accessibility level. The accessibility level controls
whether they can be used from other code in your assembly or other assemblies. An
assembly  is a .dll or .exe created by compiling one or more .cs files in a single
compilation. Use the following access modifiers to specify the accessibility of a type or
member when you declare it:
public : The type or member can be accessed by any other code in the same
assembly or another assembly that references it. The accessibility level of public
members of a type is controlled by the accessibility level of the type itself.
private : The type or member can be accessed only by code in the same class or
struct.
protected : The type or member can be accessed only by code in the same class,
or in a class that is derived from that class.
internal : The type or member can be accessed by any code in the same assembly,
but not from another assembly. In other words, internal types or members can be
accessed from code that is part of the same compilation.
protected internal : The type or member can be accessed by any code in the
assembly in which it's declared, or from within a derived class in another
assembly.
private protected : The type or member can be accessed by types derived from the
class that are declared within its containing assembly.
Caller' s location publicprotected
internalprotectedinternalprivate
protectedprivate
Within the class ✔  ✔ ✔ ✔ ✔ ✔ 
Derived class (same
assembly)✔ ✔ ✔ ✔ ✔ ❌
Non-derived class
(same assembly)✔ ✔ ❌✔ ❌❌
Derived class ✔ ✔ ✔ ❌❌❌Summary tableCaller' s location publicprotected
internalprotectedinternalprivate
protectedprivate
(different assembly)
Non-derived class
(different assembly)✔ ❌❌❌❌❌
The following examples demonstrate how to specify access modifiers on a type and
member:
C#
Not all access modifiers are valid for all types or members in all contexts. In some cases,
the accessibility of a type member is constrained by the accessibility of its containing
type.
Classes, records, and structs declared directly within a namespace (in other words, that
aren't nested within other classes or structs) can be either public or internal. internal
is the default if no access modifier is specified.
Struct members, including nested classes and structs, can be declared public, internal,
or private. Class members, including nested classes and structs, can be public,
protected internal, protected, internal, private protected, or private. Class and
struct members, including nested classes and structs, have private access by default.
Private nested types aren't accessible from outside the containing type.
Derived classes and derived records can't have greater accessibility than their base
types. Y ou can't declare a public class B that derives from an internal class A. If allowed,
it would have the effect of making A public, because all protected or internal
members of A are accessible from the derived class.
You can enable specific other assemblies to access your internal types by using the
InternalsVisibleToAttribute. For more information, see Friend Assemblies .public class Bicycle
{
    public void Pedal() { }
}
Class, record, and struct accessibility
Class, record, and struct member accessibilityClass and record members (including nested classes, records and structs) can be
declared with any of the six types of access. S truct members can't be declared as
protected, protected internal, or private protected because structs don't support
inheritance.
Normally, the accessibility of a member isn't greater than the accessibility of the type
that contains it. However, a public member of an internal class might be accessible
from outside the assembly if the member implements interface methods or overrides
virtual methods that are defined in a public base class.
The type of any member field, property, or event must be at least as accessible as the
member itself. Similarly, the return type and the parameter types of any method,
indexer, or delegate must be at least as accessible as the member itself. For example,
you can't have a public method M that returns a class C unless C is also public.
Likewise, you can't have a protected property of type A if A is declared as private.
User-defined operators must always be declared as public and static. For more
information, see Operator overloading .
Finalizers can't have accessibility modifiers.
To set the access level for a class, record, or struct member, add the appropriate
keyword to the member declaration, as shown in the following example.
C#
// public class:
public class Tricycle
{
    // protected method:
    protected  void Pedal() { }
    // private field:
    private int _wheels = 3;
    // protected internal property:
    protected  internal  int Wheels
    {
        get { return _wheels; }
    }
}
Other typesInterfaces declared directly within a namespace can be public or internal and, just like
classes and structs, interfaces default to internal access. Interface members are public
by default because the purpose of an interface is to enable other types to access a class
or struct. Interface member declarations may include any access modifier. This is most
useful for static methods to provide common implementations needed by all
implementors of a class.
Enumeration members are always public, and no access modifiers can be applied.
Delegates behave like classes and structs. By default, they have internal access when
declared directly within a namespace, and private access when nested.
Type Default access
class internal
struct internal
interface internal
record internal
enum internal
interface members public
Anonymous types internal
class, record, and struct members private
For more details see the Accessibility Levels  page.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
Specify modifier order (style rule IDE0036)
C# Programming Guide
The C# type systemDefault access summary table
C# language specification
See alsoInterfaces
Accessibility Levels
private
public
internal
protected
protected internal
private protected
sealed
class
struct
interface
Anonymous types
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
 Provide product feedbackFields (C# Programming Guide)
Article •05/26/2023
A field is a variable of any type that is declared directly in a class  or struct . Fields are
member s of their containing type.
A class or struct may have instance fields, static fields, or both. Instance fields are
specific to an instance of a type. If you have a class T, with an instance field F, you can
create two objects of type T, and modify the value of F in each object without affecting
the value in the other object. By contrast, a static field belongs to the type itself, and is
shared among all instances of that type. Y ou can access the static field only by using the
type name. If you access the static field by an instance name, you get CS0176  compile-
time error.
Generally, you should declare private or protected accessibility for fields. Data that
your type exposes to client code should be provided through methods , properties , and
indexers . By using these constructs for indirect access to internal fields, you can guard
against invalid input values. A private field that stores the data exposed by a public
property is called a backing st ore or backing f ield. You can declare public fields, but
then you can't prevent code that uses your type from setting that field to an invalid
value or otherwise changing an object's data.
Fields typically store the data that must be accessible to more than one type method
and must be stored for longer than the lifetime of any single method. For example, a
type that represents a calendar date might have three integer fields: one for the month,
one for the day, and one for the year. V ariables that aren't used outside the scope of a
single method should be declared as local v ariables  within the method body itself.
Fields are declared in the class or struct block by specifying the access level, followed by
the type, followed by the name of the field. For example:
C#
public class CalendarEntry  
{ 
    // private field (Located near wrapping "Date" property).  
    private DateTime _date;  
    // Public property exposes _date field safely.  
    public DateTime Date  
    { 
        get 
        {  To access a field in an instance, add a period after the instance name, followed by the
name of the field, as in instancename._fieldName. For example:            return _date; 
        }  
        set 
        {  
            // Set some reasonable boundaries for likely birth dates.  
            if (value.Year > 1900 && value.Year <= DateTime.Today.Year)  
            {  
                _date = value; 
            }  
            else 
            {  
                throw new ArgumentOutOfRangeException( "Date"); 
            }  
        }  
    } 
    // public field (Generally not recommended).  
    public string? Day; 
    // Public method also exposes _date field safely.  
    // Example call: birthday.SetDate("1975, 6, 30");  
    public void SetDate(string dateString ) 
    { 
        DateTime dt = Convert.ToDateTime(dateString);  
        // Set some reasonable boundaries for likely birth dates.  
        if (dt.Year > 1900 && dt.Year <= DateTime.Today.Year)  
        {  
            _date = dt;  
        }  
        else 
        {  
            throw new ArgumentOutOfRangeException( "dateString" ); 
        }  
    } 
    public TimeSpan GetTimeSpan (string dateString ) 
    { 
        DateTime dt = Convert.ToDateTime(dateString);  
        if (dt.Ticks < _date.Ticks)  
        {  
            return _date - dt;  
        }  
        else 
        {  
            throw new ArgumentOutOfRangeException( "dateString" ); 
        }  
    } 
} C#
A field can be given an initial value by using the assignment operator when the field is
declared. T o automatically assign the Day field to "Monday", for example, you would
declare Day as in the following example:
C#
Fields are initialized immediately before the constructor for the object instance is called.
If the constructor assigns the value of a field, it overwrites any value given during field
declaration. For more information, see Using Constructors .
Fields can be marked as public , private , protected , internal , protected internal , or private
protected . These access modifiers define how users of the type can access the fields. For
more information, see Access Modifiers .
A field can optionally be declared static . Static fields are available to callers at any time,
even if no instance of the type exists. For more information, see Static Classes and S tatic
Class Members .
A field can be declared readonly . A read-only field can only be assigned a value during
initialization or in a constructor. A static readonly field is similar to a constant, except
that the C# compiler doesn't have access to the value of a static read-only field at
compile time, only at run time. For more information, see Constants .
A field can be declared required . A required field must be initialized by the constructor,
or by an object initializers  when an object is created. Y ou add the
System.Diagnostics.CodeAnalysis.SetsR equiredMembersAttribute  attribute to any
constructor declaration that initializes all required members.CalendarEntry birthday = new CalendarEntry();  
birthday.Day = "Saturday" ; 
public class CalendarDateWithInitialization  
{ 
    public string Day = "Monday" ; 
    //... 
} 
７ Note
A field initializer cannot refer to other instance fields.The required modifier can't be combined with the readonly modifier on the same field.
However, property  can be required and init only.
Beginning with C# 12, Primary constructor  parameters are an alternative to declaring
fields. When your type has dependencies that must be provided at initialization, you can
create a primary constructor that provides those dependencies. These parameters may
be captured and used in place of declared fields in your types. In the case of record
types, primary constructor parameters are surfaced as public properties.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Programming Guide
The C# type system
Using Constructors
Inheritance
Access Modifiers
Abstract and Sealed Classes and Class MembersC# language specification
See alsoConstants (C# Programming Guide)
Article •11/14/2023
Constants are immutable values which are known at compile time and do not change
for the life of the program. Constants are declared with the const  modifier. Only the C#
built-in types  may be declared as const. Reference type constants other than String  can
only be initialized with a null value. User-defined types, including classes, structs, and
arrays, cannot be const. Use the readonly  modifier to create a class, struct, or array that
is initialized one time at run time (for example in a constructor) and thereafter cannot be
changed.
C# does not support const methods, properties, or events.
The enum type enables you to define named constants for integral built-in types (for
example int, uint, long, and so on). For more information, see enum .
Constants must be initialized as they are declared. For example:
C#
In this example, the constant Months is always 12, and it cannot be changed even by the
class itself. In fact, when the compiler encounters a constant identifier in C# source code
(for example, Months), it substitutes the literal value directly into the intermediate
language (IL) code that it produces. Because there is no variable address associated with
a constant at run time, const fields cannot be passed by reference and cannot appear
as an l-value in an expression.
Multiple constants of the same type can be declared at the same time, for example:
C#class Calendar1
{
    public const int Months = 12;
}
７ Note
Use caution when you refer to constant values defined in other code such as DLLs.
If a new version of the DLL defines a new value for the constant, your program will
still hold the old literal value until it is recompiled against the new version.The expression that is used to initialize a constant can refer to another constant if it
does not create a circular reference. For example:
C#
Constants can be marked as public , private , protected , internal , protected internal  or
private protected . These access modifiers define how users of the class can access the
constant. For more information, see Access Modifiers .
Constants are accessed as if they were static  fields because the value of the constant is
the same for all instances of the type. Y ou do not use the static keyword to declare
them. Expressions that are not in the class that defines the constant must use the class
name, a period, and the name of the constant to access the constant. For example:
C#
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Programming Guide
Properties
Typesclass Calendar2
{
    public const int Months = 12, Weeks = 52, Days = 365;
}
class Calendar3
{
    public const int Months = 12;
    public const int Weeks = 52;
    public const int Days = 365;
    public const double DaysPerWeek = ( double) Days / ( double) Weeks;
    public const double DaysPerMonth = ( double) Days / ( double) Months;
}
int birthstones = Calendar.Months;
C# Language Specification
See alsoreadonly
Immutability in C# P art One: Kinds of Immutability
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
 Provide product feedbackHow to define abstract properties (C#
Programming Guide)
Article •10/27/2021
The following example shows how to define abstract  properties. An abstract property
declaration does not provide an implementation of the property accessors -- it declares
that the class supports properties, but leaves the accessor implementation to derived
classes. The following example demonstrates how to implement the abstract properties
inherited from a base class.
This sample consists of three files, each of which is compiled individually and its
resulting assembly is referenced by the next compilation:
abstractshape.cs: the Shape class that contains an abstract Area property.
shapes.cs: The subclasses of the Shape class.
shapetest.cs: A test program to display the areas of some Shape-derived objects.
To compile the example, use the following command:
csc abstractshape.cs shapes.cs shapetest.cs
This will create the executable file shapetest.exe.
This file declares the Shape class that contains the Area property of the type double.
C#Examples
// compile with: csc -target:library abstractshape.cs  
public abstract  class Shape 
{ 
    private string name; 
    public Shape(string s) 
    { 
        // calling the set accessor of the Id property.  
        Id = s;  
    } 
    public string Id 
    { 
        get Modifiers on the property are placed on the property declaration itself. For
example:
C#
When declaring an abstract property (such as Area in this example), you simply
indicate what property accessors are available, but do not implement them. In this
example, only a get accessor is available, so the property is read-only.
The following code shows three subclasses of Shape and how they override the Area
property to provide their own implementation.
C#        {  
            return name; 
        }  
        set 
        {  
            name = value; 
        }  
    } 
    // Area is a read-only property - only a get accessor is needed:  
    public abstract  double Area 
    { 
        get; 
    } 
    public override  string ToString () 
    { 
        return $"{Id} Area = {Area:F2} "; 
    } 
} 
public abstract  double Area   
// compile with: csc -target:library -reference:abstractshape.dll shapes.cs  
public class Square : Shape 
{ 
    private int side; 
    public Square(int side, string id) 
        : base(id) 
    { 
        this.side = side;  
    } 
    public override  double Area The following code shows a test program that creates a number of Shape-derived
objects and prints out their areas.    { 
        get 
        {  
            // Given the side, return the area of a square:  
            return side * side;  
        }  
    } 
} 
public class Circle : Shape 
{ 
    private int radius;
    public Circle(int radius, string id) 
        : base(id) 
    { 
        this.radius = radius;  
    } 
    public override  double Area 
    { 
        get 
        {  
            // Given the radius, return the area of a circle:  
            return radius * radius * System.Math.PI;  
        }  
    } 
} 
public class Rectangle  : Shape 
{ 
    private int width; 
    private int height;
    public Rectangle (int width, int height, string id) 
        : base(id) 
    { 
        this.width = width;  
        this.height = height;  
    } 
    public override  double Area 
    { 
        get 
        {  
            // Given the width and height, return the area of a rectangle:  
            return width * height;  
        }  
    } 
} C#
C# Programming Guide
The C# type system
Abstract and Sealed Classes and Class Members
Properties// compile with: csc -reference:abstractshape.dll;shapes.dll shapetest.cs  
class TestClass  
{ 
    static void Main() 
    { 
        Shape[] shapes =  
        {  
            new Square( 5, "Square #1" ), 
            new Circle( 3, "Circle #1" ), 
            new Rectangle( 4, 5, "Rectangle #1" ) 
        };  
        System.Console.WriteLine( "Shapes Collection" ); 
        foreach (Shape s in shapes)  
        {  
            System.Console.WriteLine(s);  
        }  
    } 
} 
/* Output:  
    Shapes Collection  
    Square #1 Area = 25.00  
    Circle #1 Area = 28.27  
    Rectangle #1 Area = 20.00  
*/ 
See alsoHow to define constants in C#
Article •10/27/2021
Constants are fields whose values are set at compile time and can never be changed.
Use constants to provide meaningful names instead of numeric literals ("magic
numbers") for special values.
To define constant values of integral types ( int, byte, and so on) use an enumerated
type. For more information, see enum .
To define non-integral constants, one approach is to group them in a single static class
named Constants. This will require that all references to the constants be prefaced with
the class name, as shown in the following example.
C#
The use of the class name qualifier helps ensure that you and others who use the
constant understand that it is constant and cannot be modified.７ Note
In C# the #define  preprocessor directive cannot be used to define constants in the
way that is typically used in C and C++.
Example
static class Constants  
{ 
    public const double Pi = 3.14159; 
    public const int SpeedOfLight = 300000; // km per sec.  
} 
class Program 
{ 
    static void Main() 
    { 
        double radius = 5.3; 
        double area = Constants.Pi * (radius * radius);  
        int secsFromSun = 149476000  / Constants.SpeedOfLight; // in km  
        Console.WriteLine(secsFromSun);  
    } 
} The C# type systemSee alsoProperties (C# Programming Guide)
Article •04/12/2023
A property is a member that provides a flexible mechanism to read, write, or compute
the value of a private field. Properties can be used as if they're public data members, but
they're special methods called accessors. This feature enables data to be accessed easily
and still helps promote the safety and flexibility of methods.
Properties enable a class to expose a public way of getting and setting values,
while hiding implementation or verification code.
A get property accessor is used to return the property value, and a set property
accessor is used to assign a new value. An init property accessor is used to assign a
new value only during object construction. These accessors can have different
access levels. For more information, see Restricting Accessor Accessibility .
The value  keyword is used to define the value being assigned by the set or init
accessor.
Properties can be read-wr ite (they have both a get and a set accessor), read-only
(they have a get accessor but no set accessor), or write-only  (they have a set
accessor, but no get accessor). Write-only properties are rare and are most
commonly used to restrict access to sensitive data.
Simple properties that require no custom accessor code can be implemented
either as expression body definitions or as auto-implemented properties .
One basic pattern for implementing a property involves using a private backing field for
setting and retrieving the property value. The get accessor returns the value of the
private field, and the set accessor may perform some data validation before assigning a
value to the private field. Both accessors may also perform some conversion or
computation on the data before it's stored or returned.
The following example illustrates this pattern. In this example, the TimePeriod class
represents an interval of time. Internally, the class stores the time interval in seconds in a
private field named _seconds. A read-write property named Hours allows the customer
to specify the time interval in hours. Both the get and the set accessors perform the
necessary conversion between hours and seconds. In addition, the set accessorProperties overview
Properties with backing fieldsvalidates the data and throws an ArgumentOutOfRangeException  if the number of
hours is invalid.
C#
You could access properties to get and set the value as shown in the following example:
C#
Property accessors often consist of single-line statements that just assign or return the
result of an expression. Y ou can implement these properties as expression-bodied
members. Expression body definitions consist of the => symbol followed by the
expression to assign to or retrieve from the property.
Read-only properties can implement the get accessor as an expression-bodied
member. In this case, neither the get accessor keyword nor the return keyword is used.
The following example implements the read-only Name property as an expression-
bodied member.public class TimePeriod
{
    private double _seconds;
    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
                throw new ArgumentOutOfRangeException( nameof(value),
                      "The valid range is between 0 and 24." );
            _seconds = value * 3600;
        }
    }
}
TimePeriod t = new TimePeriod();
// The property assignment causes the 'set' accessor to be called.
t.Hours = 24;
// Retrieving the property causes the 'get' accessor to be called.
Console.WriteLine( $"Time in hours: {t.Hours} ");
// The example displays the following output:
//    Time in hours: 24
Expression body definitio nsC#
Both the get and the set accessor can be implemented as expression-bodied
members. In this case, the get and set keywords must be present. The following
example illustrates the use of expression body definitions for both accessors. The
return keyword isn't used with the get accessor.
C#public class Person
{
    private string _firstName;
    private string _lastName;
    public Person(string first, string last)
    {
        _firstName = first;
        _lastName = last;
    }
    public string Name => $"{_firstName}  {_lastName} ";
}
public class SaleItem
{
    string _name;
    decimal _cost;
    public SaleItem (string name, decimal cost)
    {
        _name = name;
        _cost = cost;
    }
    public string Name
    {
        get => _name;
        set => _name = value;
    }
    public decimal Price
    {
        get => _cost;
        set => _cost = value;
    }
}
Auto-implemented propertiesIn some cases, property get and set accessors just assign a value to or retrieve a value
from a backing field without including any extra logic. By using auto-implemented
properties, you can simplify your code while having the C# compiler transparently
provide the backing field for you.
If a property has both a get and a set (or a get and an init) accessor, both must be
auto-implemented. Y ou define an auto-implemented property by using the get and
set keywords without providing any implementation. The following example repeats
the previous one, except that Name and Price are auto-implemented properties. The
example also removes the parameterized constructor, so that SaleItem objects are now
initialized with a call to the parameterless constructor and an object initializer .
C#
Auto-implemented properties can declare different accessibilities for the get and set
accessors. Y ou commonly declare a public get accessor and a private set accessor. Y ou
can learn more in the article on restricting accessor accessibility .
Beginning with C# 11, you can add the required member to force client code to
initialize any property or field:
C#public class SaleItem
{
    public string Name
    { get; set; }
    public decimal Price
    { get; set; }
}
Required properties
public class SaleItem
{
    public required string Name
    { get; set; }
    public required decimal Price
    { get; set; }
}To create a SaleItem, you must set both the Name and Price properties using object
initializers , as shown in the following code:
C#
Using Properties
Interface Properties
Comparison Between Properties and Indexers
Restricting Accessor Accessibility
Auto-Implemented Properties
For more information, see Properties  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
Indexers
get keyword
set keywordvar item = new SaleItem { Name = "Shoes", Price = 19.95m };
Console.WriteLine( $"{item.Name} : sells for {item.Price:C2} ");
Related sections
C# Language Specification
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
 Provide product feedbackUsing Properties (C# Programming
Guide)
Article •04/22/2023
Properties combine aspects of both fields and methods. T o the user of an object, a
property appears to be a field; accessing the property requires the same syntax. T o the
implementer of a class, a property is one or two code blocks, representing a get
accessor and/or a set accessor. The code block for the get accessor is executed when
the property is read; the code block for the set accessor is executed when the property
is assigned a value. A property without a set accessor is considered read-only. A
property without a get accessor is considered write-only. A property that has both
accessors is read-write. Y ou can use an init accessor instead of a set accessor to make
the property read-only.
Unlike fields, properties aren't classified as variables. Therefore, you can't pass a
property as a ref or out parameter.
Properties have many uses: they can validate data before allowing a change; they can
transparently expose data on a class where that data is retrieved from some other
source, such as a database; they can take an action when data is changed, such as
raising an event, or changing the value of other fields.
Properties are declared in the class block by specifying the access level of the field,
followed by the type of the property, followed by the name of the property, and
followed by a code block that declares a get-accessor and/or a set accessor. For
example:
C#
public class Date
{
    private int _month = 7;  // Backing store
    public int Month
    {
        get => _month;
        set
        {
            if ((value > 0) && (value < 13))
            {
                _month = value;
            }
        }In this example, Month is declared as a property so that the set accessor can make sure
that the Month value is set between 1 and 12. The Month property uses a private field to
track the actual value. The real location of a property's data is often referred to as the
property's "backing store." It's common for properties to use private fields as a backing
store. The field is marked private in order to make sure that it can only be changed by
calling the property. For more information about public and private access restrictions,
see Access Modifiers .
Auto-implemented properties provide simplified syntax for simple property declarations.
For more information, see Auto-Implemented Properties .
The body of the get accessor resembles that of a method. It must return a value of the
property type. The execution of the get accessor is equivalent to reading the value of
the field. For example, when you're returning the private variable from the get accessor
and optimizations are enabled, the call to the get accessor method is inlined by the
compiler so there's no method-call overhead. However, a virtual get accessor method
can't be inlined because the compiler doesn't know at compile-time which method may
actually be called at run time. The following example shows a get accessor that returns
the value of a private field _name:
C#
When you reference the property, except as the target of an assignment, the get
accessor is invoked to read the value of the property. For example:
C#    }
}
The get accessor
class Employee
{
    private string _name;  // the name field
    public string Name => _name;     // the Name property
}
var employee= new Employee();
//...
System.Console.Write(employee.Name);  // the get accessor is invoked hereThe get accessor must end in a return  or throw  statement, and control can't flow off the
accessor body.
The get accessor can be used to return the field value or to compute it and return it. For
example:
C#
In the previous code segment, if you don't assign a value to the Name property, it will
return the value NA.
The set accessor resembles a method whose return type is void. It uses an implicit
parameter called value, whose type is the type of the property. In the following
example, a set accessor is added to the Name property:
C#
When you assign a value to the property, the set accessor is invoked by using an
argument that provides the new value. For example:２ Warning
It's a bad programming style to change the state of the object by using the get
accessor.
class Manager
{
    private string _name;
    public string Name => _name != null ? _name : "NA";
}
The set accessor
class Student
{
    private string _name;  // the name field
    public string Name    // the Name property
    {
        get => _name;
        set => _name = value;
    }
}C#
It's an error to use the implicit parameter name, value, for a local variable declaration in
a set accessor.
The code to create an init accessor is the same as the code to create a set accessor
except that you use the init keyword instead of set. The difference is that the init
accessor can only be used in the constructor or by using an object-initializer .
Properties can be marked as public, private, protected, internal, protected
internal, or private protected. These access modifiers define how users of the class
can access the property. The get and set accessors for the same property may have
different access modifiers. For example, the get may be public to allow read-only
access from outside the type, and the set may be private or protected. For more
information, see Access Modifiers .
A property may be declared as a static property by using the static keyword. S tatic
properties are available to callers at any time, even if no instance of the class exists. For
more information, see Static Classes and S tatic Class Members .
A property may be marked as a virtual property by using the virtual  keyword. Virtual
properties enable derived classes to override the property behavior by using the
override  keyword. For more information about these options, see Inheritance .
A property overriding a virtual property can also be sealed , specifying that for derived
classes it's no longer virtual. Lastly, a property can be declared abstract . Abstract
properties don't define an implementation in the class, and derived classes must write
their own implementation. For more information about these options, see Abstract and
Sealed Classes and Class Members .var student = new Student();
student.Name = "Joe";  // the set accessor is invoked here
System.Console.Write(student.Name);  // the get accessor is invoked here
The init accessor
Remarks
７ NoteThis example demonstrates instance, static, and read-only properties. It accepts the
name of the employee from the keyboard, increments NumberOfEmployees by 1, and
displays the Employee name and number.
C#
This example demonstrates how to access a property in a base class that is hidden by
another property that has the same name in a derived class:
C#It is an error to use a virtual, abstract , or override  modifier on an accessor of a
static  property.
Examples
public class Employee
{
    public static int NumberOfEmployees;
    private static int _counter;
    private string _name;
    // A read-write instance property:
    public string Name
    {
        get => _name;
        set => _name = value;
    }
    // A read-only static property:
    public static int Counter => _counter;
    // A Constructor:
    public Employee () => _counter = ++NumberOfEmployees; // Calculate the  
employee's number:
}
Hidden property example
public class Employee
{
    private string _name;
    public string Name
    {
        get => _name;
        set => _name = value;
    }The following are important points in the previous example:
The property Name in the derived class hides the property Name in the base class. In
such a case, the new modifier is used in the declaration of the property in the
derived class:
C#
The cast (Employee) is used to access the hidden property in the base class:
C#}
public class Manager : Employee
{
    private string _name;
    // Notice the use of the new modifier:
    public new string Name
    {
        get => _name;
        set => _name = value + ", Manager" ;
    }
}
class TestHiding
{
    public static void Test()
    {
        Manager m1 = new Manager();
        // Derived class property.
        m1.Name = "John";
        // Base class property.
        ((Employee)m1).Name = "Mary";
        System.Console.WriteLine( "Name in the derived class is: {0}" , 
m1.Name);
        System.Console.WriteLine( "Name in the base class is: {0}" , 
((Employee)m1).Name);
    }
}
/* Output:
    Name in the derived class is: John, Manager
    Name in the base class is: Mary
*/
public new string NameFor more information about hiding members, see the new Modifier .
In this example, two classes, Cube and Square, implement an abstract class, Shape, and
override its abstract Area property. Note the use of the override  modifier on the
properties. The program accepts the side as an input and calculates the areas for the
square and cube. It also accepts the area as an input and calculates the corresponding
side for the square and cube.
C#((Employee)m1).Name = "Mary";
Override property example
abstract  class Shape
{
    public abstract  double Area
    {
        get;
        set;
    }
}
class Square : Shape
{
    public double side;
    //constructor
    public Square(double s) => side = s;
    public override  double Area
    {
        get => side * side;
        set => side = System.Math.Sqrt( value);
    }
}
class Cube : Shape
{
    public double side;
    //constructor
    public Cube(double s) => side = s;
    public override  double Area
    {
        get => 6 * side * side;
        set => side = System.Math.Sqrt( value / 6);
    }Properties
Interface Properties
Auto-Implemented Properties}
class TestShapes
{
    static void Main()
    {
        // Input the side:
        System.Console.Write( "Enter the side: " );
        double side = double.Parse(System.Console.ReadLine());
        // Compute the areas:
        Square s = new Square(side);
        Cube c = new Cube(side);
        // Display the results:
        System.Console.WriteLine( "Area of the square = {0:F2}" , s.Area);
        System.Console.WriteLine( "Area of the cube = {0:F2}" , c.Area);
        System.Console.WriteLine();
        // Input the area:
        System.Console.Write( "Enter the area: " );
        double area = double.Parse(System.Console.ReadLine());
        // Compute the sides:
        s.Area = area;
        c.Area = area;
        // Display the results:
        System.Console.WriteLine( "Side of the square = {0:F2}" , s.side);
        System.Console.WriteLine( "Side of the cube = {0:F2}" , c.side);
    }
}
/* Example Output:
    Enter the side: 4
    Area of the square = 16.00
    Area of the cube = 96.00
    Enter the area: 24
    Side of the square = 4.90
    Side of the cube = 2.00
*/
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
 Provide product feedbackInterface Properties (C# Programming
Guide)
Article •09/29/2022
Properties can be declared on an interface . The following example declares an interface
property accessor:
C#
Interface properties typically don't have a body. The accessors indicate whether the
property is read-write, read-only, or write-only. Unlike in classes and structs, declaring
the accessors without a body doesn't declare an auto-implemented property . An
interface may define a default implementation for members, including properties.
Defining a default implementation for a property in an interface is rare because
interfaces may not define instance data fields.
In this example, the interface IEmployee has a read-write property, Name, and a read-
only property, Counter. The class Employee implements the IEmployee interface and
uses these two properties. The program reads the name of a new employee and the
current number of employees and displays the employee name and the computed
employee number.
You could use the fully qualified name of the property, which references the interface in
which the member is declared. For example:
C#public interface  ISampleInterface  
{ 
    // Property declaration:  
    string Name 
    { 
        get; 
        set; 
    } 
} 
Example
string IEmployee.Name  
{ 
    get { return "Employee Name" ; } The preceding example demonstrates Explicit Interface Implementation . For example, if
the class Employee is implementing two interfaces ICitizen and IEmployee and both
interfaces have the Name property, the explicit interface member implementation will be
necessary. That is, the following property declaration:
C#
implements the Name property on the IEmployee interface, while the following
declaration:
C#
implements the Name property on the ICitizen interface.
C#    set { } 
} 
string IEmployee.Name  
{ 
    get { return "Employee Name" ; } 
    set { } 
} 
string ICitizen.Name  
{ 
    get { return "Citizen Name" ; } 
    set { } 
} 
interface  IEmployee  
{ 
    string Name 
    { 
        get; 
        set; 
    } 
    int Counter  
    { 
        get; 
    } 
} 
public class Employee  : IEmployee  
{ 
    public static int numberOfEmployees;  C#
Console
C# Programming Guide
Properties
Using Properties
Comparison Between Properties and Indexers    private string _name; 
    public string Name  // read-write instance property  
    { 
        get => _name;  
        set => _name = value; 
    } 
    private int _counter;  
    public int Counter  // read-only instance property  
    { 
        get => _counter;  
    } 
    // constructor  
    public Employee () => _counter = ++numberOfEmployees;  
} 
System.Console.Write( "Enter number of employees: " ); 
Employee.numberOfEmployees = int.Parse(System.Console.ReadLine());
Employee e1 = new Employee();  
System.Console.Write( "Enter the name of the new employee: " ); 
e1.Name = System.Console.ReadLine();  
System.Console.WriteLine( "The employee information:" ); 
System.Console.WriteLine( "Employee number: {0}" , e1.Counter);  
System.Console.WriteLine( "Employee name: {0}" , e1.Name);  
Sample output
Enter number of employees: 210  
Enter the name of the new employee: Hazem Abolrous  
The employee information:  
Employee number: 211  
Employee name: Hazem Abolrous  
See alsoIndexers
InterfacesRestricting Acces sor Accessibility (C#
Programming Guide)
Article •07/30/2022
The get and set portions of a property or indexer are called accessors. By default these
accessors have the same visibility or access level of the property or indexer to which
they belong. For more information, see accessibility levels . However, it's sometimes
useful to restrict access to one of these accessors. T ypically, you restrict the accessibility
of the set accessor, while keeping the get accessor publicly accessible. For example:
C#
In this example, a property called Name defines a get and set accessor. The get
accessor receives the accessibility level of the property itself, public in this case, while
the set accessor is explicitly restricted by applying the protected  access modifier to the
accessor itself.
Using the accessor modifiers on properties or indexers is subject to these conditions:private string _name = "Hello"; 
public string Name 
{ 
    get 
    { 
        return _name; 
    } 
    protected  set 
    { 
        _name = value; 
    } 
} 
７ Note
The examples in this article don't use auto-implement ed pr oper ties. Auto-
implement ed pr operties provide a concise syntax for declaring properties when a
custom backing field isn't required.
Restrictions on Access Modifiers on AccessorsYou can't use accessor modifiers on an interface or an explicit interface  member
implementation.
You can use accessor modifiers only if the property or indexer has both set and
get accessors. In this case, the modifier is permitted on only one of the two
accessors.
If the property or indexer has an override  modifier, the accessor modifier must
match the accessor of the overridden accessor, if any.
The accessibility level on the accessor must be more restrictive than the
accessibility level on the property or indexer itself.
When you override a property or indexer, the overridden accessors must be accessible
to the overriding code. Also, the accessibility of both the property/indexer and its
accessors must match the corresponding overridden property/indexer and its accessors.
For example:
C#Access Modifiers on Overriding Accessors
public class Parent 
{ 
    public virtual int TestProperty  
    { 
        // Notice the accessor accessibility level.  
        protected  set { } 
        // No access modifier is used here.  
        get { return 0; } 
    } 
} 
public class Kid : Parent 
{ 
    public override  int TestProperty  
    { 
        // Use the same accessibility level as in the overridden accessor.  
        protected  set { } 
        // Cannot use access modifier here.  
        get { return 0; } 
    } 
} 
Implementing  InterfacesWhen you use an accessor to implement an interface, the accessor may not have an
access modifier. However, if you implement the interface using one accessor, such as
get, the other accessor can have an access modifier, as in the following example:
C#
If you use an access modifier on the accessor, the accessibility domain  of the accessor is
determined by this modifier.
If you didn't use an access modifier on the accessor, the accessibility domain of the
accessor is determined by the accessibility level of the property or indexer.
The following example contains three classes, BaseClass, DerivedClass, and MainClass.
There are two properties on the BaseClass, Name and Id on both classes. The example
demonstrates how the property Id on DerivedClass can be hidden by the property Id
on BaseClass when you use a restrictive access modifier such as protected  or private .
Therefore, when you assign values to this property, the property on the BaseClass classpublic interface  ISomeInterface  
{ 
    int TestProperty  
    { 
        // No access modifier allowed here  
        // because this is an interface.  
        get; 
    } 
} 
public class TestClass  : ISomeInterface  
{ 
    public int TestProperty  
    { 
        // Cannot use access modifier here because  
        // this is an interface implementation.  
        get { return 10; } 
        // Interface property does not have set accessor,  
        // so access modifier is allowed.  
        protected  set { } 
    } 
} 
Accessor Accessibility Domain
Exampleis called instead. R eplacing the access modifier by public  will make the property
accessible.
The example also demonstrates that a restrictive access modifier, such as private or
protected, on the set accessor of the Name property in DerivedClass prevents access to
the accessor in the derived class. It generates an error when you assign to it, or accesses
the base class property of the same name, if it's accessible.
C#
public class BaseClass  
{ 
    private string _name = "Name-BaseClass" ; 
    private string _id = "ID-BaseClass" ; 
    public string Name 
    { 
        get { return _name; }  
        set { } 
    } 
    public string Id 
    { 
        get { return _id; } 
        set { } 
    } 
} 
public class DerivedClass  : BaseClass  
{ 
    private string _name = "Name-DerivedClass" ; 
    private string _id = "ID-DerivedClass" ; 
    new public string Name 
    { 
        get 
        {  
            return _name; 
        }  
        // Using "protected" would make the set accessor not accessible.  
        set 
        {  
            _name = value; 
        }  
    } 
    // Using private on the following property hides it in the Main Class.  
    // Any assignment to the property will use Id in BaseClass.  
    new private string Id 
    { 
        get Notice that if you replace the declaration new private string Id by new public string
Id, you get the output:
Name and ID in the base class: Name-BaseClass, ID-BaseClass Name and ID in the
derived class: John, John123
Properties
Indexers        {  
            return _id; 
        }  
        set 
        {  
            _id = value; 
        }  
    } 
} 
class MainClass  
{ 
    static void Main() 
    { 
        BaseClass b1 = new BaseClass();  
        DerivedClass d1 = new DerivedClass();  
        b1.Name = "Mary"; 
        d1.Name = "John"; 
        b1.Id = "Mary123" ; 
        d1.Id = "John123" ;  // The BaseClass.Id property is called.  
        System.Console.WriteLine( "Base: {0}, {1}" , b1.Name, b1.Id);  
        System.Console.WriteLine( "Derived: {0}, {1}" , d1.Name, d1.Id);  
        // Keep the console window open in debug mode.  
        System.Console.WriteLine( "Press any key to exit." ); 
        System.Console.ReadKey();
    } 
} 
/* Output:  
    Base: Name-BaseClass, ID-BaseClass  
    Derived: John, ID-BaseClass  
*/ 
Comments
See alsoAccess Modifiers
Init only properties
Required propertiesHow to declare and use read write
properties (C# Programming Guide)
Article •07/30/2022
Properties provide the convenience of public data members without the risks that come
with unprotected, uncontrolled, and unverified access to an object's data. Properties
declare accessors: special methods that assign and retrieve values from the underlying
data member. The set accessor enables data members to be assigned, and the get
accessor retrieves data member values.
This sample shows a Person class that has two properties: Name (string) and Age (int).
Both properties provide get and set accessors, so they're considered read/write
properties.
C#Example
class Person 
{ 
    private string _name = "N/A"; 
    private int _age = 0; 
    // Declare a Name property of type string:  
    public string Name 
    { 
        get 
        {  
            return _name; 
        }  
        set 
        {  
            _name = value; 
        }  
    } 
    // Declare an Age property of type int:  
    public int Age 
    { 
        get 
        {  
            return _age; 
        }  
        set 
        {              _age = value; 
        }  
    } 
    public override  string ToString () 
    { 
        return "Name = "  + Name + ", Age = "  + Age; 
    } 
} 
public class Wrapper 
{ 
    private string _name = "N/A"; 
    public string Name 
    { 
        get 
        {  
            return _name; 
        }  
        private set 
        {  
            _name = value; 
        }  
    } 
} 
class TestPerson  
{ 
    static void Main() 
    { 
        // Create a new Person object:  
        Person person = new Person();  
        // Print out the name and the age associated with the person:  
        Console.WriteLine( "Person details - {0}" , person);  
        // Set some values on the person object:  
        person.Name = "Joe"; 
        person.Age = 99; 
        Console.WriteLine( "Person details - {0}" , person);  
        // Increment the Age property:  
        person.Age += 1; 
        Console.WriteLine( "Person details - {0}" , person);  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
/* Output:  
    Person details - Name = N/A, Age = 0  
    Person details - Name = Joe, Age = 99  In the previous example, the Name and Age properties are public  and include both a get
and a set accessor. Public accessors allow any object to read and write these properties.
It's sometimes desirable, however, to exclude one of the accessors. Y ou can omit the
set accessor to make the property read-only:
C#
Alternatively, you can expose one accessor publicly but make the other private or
protected. For more information, see Asymmetric Accessor Accessibility .
Once the properties are declared, they can be used as fields of the class. Properties
allow for a natural syntax when both getting and setting the value of a property, as in
the following statements:
C#
In a property set method a special value variable is available. This variable contains the
value that the user specified, for example:
C#
Notice the clean syntax for incrementing the Age property on a Person object:    Person details - Name = Joe, Age = 100  
*/ 
Robust Programming
public string Name 
{ 
    get 
    { 
        return _name; 
    } 
    private set 
    { 
        _name = value; 
    } 
} 
person.Name = "Joe"; 
person.Age = 99; 
_name = value; C#
If separate set and get methods were used to model properties, the equivalent code
might look like this:
C#
The ToString method is overridden in this example:
C#
Notice that ToString isn't explicitly used in the program. It's invoked by default by the
WriteLine calls.
Properties
The C# type systemperson.Age += 1; 
person.SetAge(person.GetAge() + 1); 
public override  string ToString () 
{ 
    return "Name = "  + Name + ", Age = "  + Age; 
} 
See alsoAuto-Implemen ted Properties (C#
Programming Guide)
Article •09/29/2022
Auto-implemented properties make property-declaration more concise when no
additional logic is required in the property accessors. They also enable client code to
create objects. When you declare a property as shown in the following example, the
compiler creates a private, anonymous backing field that can only be accessed through
the property's get and set accessors. init accessors can also be declared as auto-
implemented properties.
The following example shows a simple class that has some auto-implemented
properties:
C#Example
// This class is mutable. Its data can be modified from
// outside the class.
public class Customer
{
    // Auto-implemented properties for trivial get and set
    public double TotalPurchases { get; set; }
    public string Name { get; set; }
    public int CustomerId { get; set; }
    // Constructor
    public Customer (double purchases, string name, int id)
    {
        TotalPurchases = purchases;
        Name = name;
        CustomerId = id;
    }
    // Methods
    public string GetContactInfo () { return "ContactInfo" ; }
    public string GetTransactionHistory () { return "History" ; }
    // .. Additional methods, events, etc.
}
class Program
{
    static void Main()
    {You can't declare auto-implemented properties in interfaces. Auto-implemented
properties declare a private instance backing field, and interfaces may not declare
instance fields. Declaring a property in an interface without defining a body declares a
property with accessors that must be implemented by each type that implements that
interface.
You can initialize auto-implemented properties similarly to fields:
C#
The class that is shown in the previous example is mutable. Client code can change the
values in objects after creation. In complex classes that contain significant behavior
(methods) as well as data, it's often necessary to have public properties. However, for
small classes or structs that just encapsulate a set of values (data) and have little or no
behaviors, you should use one of the following options for making the objects
immutable:
Declare only a get accessor (immutable everywhere except the constructor).
Declare a get accessor and an init accessor (immutable everywhere except
during object construction).
Declare the set accessor as private  (immutable to consumers).
For more information, see How to implement a lightweight class with auto-implemented
properties .
Use auto-implemented properties (style rule IDE0032)
Properties
Modifiers        // Initialize a new object.
        Customer cust1 = new Customer( 4987.63, "Northwind" , 90108);
        // Modify a property.
        cust1.TotalPurchases += 499.99;
    }
}
public string FirstName { get; set; } = "Jane";
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
 Provide product feedbackHow to implement a lightweight class
with auto-implemented properties (C#
Programming Guide)
Article •07/30/2022
This example shows how to create an immutable lightweight class that serves only to
encapsulate a set of auto-implemented properties. Use this kind of construct instead of
a struct when you must use reference type semantics.
You can make an immutable property in the following ways:
Declare only the get accessor, which makes the property immutable everywhere
except in the type's constructor.
Declare an init accessor instead of a set accessor, which makes the property
settable only in the constructor or by using an object initializer .
Declare the set accessor to be private . The property is settable within the type, but
it's immutable to consumers.
You can add the required  modifier to the property declaration to force callers to set the
property as part of initializing a new object.
The following example shows how a property with only get accessor differs than one
with get and private set.
C#
class Contact
{
    public string Name { get; }
    public string Address { get; private set; }
    public Contact(string contactName, string contactAddress )
    {
        // Both properties are accessible in the constructor.
        Name = contactName;
        Address = contactAddress;
    }
    // Name isn't assignable here. This will generate a compile error.
    //public void ChangeName(string newName) => Name = newName;
    // Address is assignable here.
    public void ChangeAddress (string newAddress ) => Address = newAddress;
}The following example shows two ways to implement an immutable class that has auto-
implemented properties. Each way declares one of the properties with a private set and
one of the properties with a get only. The first class uses a constructor only to initialize
the properties, and the second class uses a static factory method that calls a constructor.
C#Example
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// constructor to initialize its properties.
class Contact
{
    // Read-only property.
    public string Name { get; }
    // Read-write property with a private set accessor.
    public string Address { get; private set; }
    // Public constructor.
    public Contact(string contactName, string contactAddress )
    {
        Name = contactName;
        Address = contactAddress;
    }
}
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// static method and private constructor to initialize its properties.
public class Contact2
{
    // Read-write property with a private set accessor.
    public string Name { get; private set; }
    // Read-only property.
    public string Address { get; }
    // Private constructor.
    private Contact2 (string contactName, string contactAddress )
    {
        Name = contactName;
        Address = contactAddress;
    }
    // Public factory method.
    public static Contact2 CreateContact (string name, string address )
    {
        return new Contact2(name, address);
    }
}The compiler creates backing fields for each auto-implemented property. The fields
aren't accessible directly from source code.public class Program
{
    static void Main()
    {
        // Some simple data sources.
        string[] names = [ "Terry Adams" ,"Fadi Fakhouri" , "Hanying Feng" ,
                            "Cesar Garcia" , "Debra Garcia" ];
        string[] addresses = [ "123 Main St." , "345 Cypress Ave." , "678 1st  
Ave",
                                "12 108th St." , "89 E. 42nd St." ];
        // Simple query to demonstrate object creation in select clause.
        // Create Contact objects by using a constructor.
        var query1 = from i in Enumerable.Range( 0, 5)
                    select new Contact(names[i], addresses[i] );
        // List elements cannot be modified by client code.
        var list = query1.ToList();
        foreach (var contact in list)
        {
            Console.WriteLine( "{0}, {1}" , contact.Name, contact.Address);
        }
        // Create Contact2 objects by using a static factory method.
        var query2 = from i in Enumerable.Range( 0, 5)
                        select Contact2.CreateContact(names[i],  
addresses[i]);
        // Console output is identical to query1.
        var list2 = query2.ToList();
        // List elements cannot be modified by client code.
        // CS0272:
        // list2[0].Name = "Eugene Zabokritski";
    }
}
/* Output:
    Terry Adams, 123 Main St.
    Fadi Fakhouri, 345 Cypress Ave.
    Hanying Feng, 678 1st Ave
    Cesar Garcia, 12 108th St.
    Debra Garcia, 89 E. 42nd St.
*/
See alsoProperties
struct
Object and Collection Initializers
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
 Provide product feedbackMethods (C# Programming Guide)
Article •06/20/2023
A method is a code block that contains a series of statements. A program causes the
statements to be executed by calling the method and specifying any required method
arguments. In C#, every executed instruction is performed in the context of a method.
The Main method is the entry point for every C# application and it's called by the
common language runtime (CLR) when the program is started. In an application that
uses top-level statements , the Main method is generated by the compiler and contains
all top-level statements.
Methods are declared in a class , struct , or interface  by specifying the access level such as
public or private, optional modifiers such as abstract or sealed, the return value, the
name of the method, and any method parameters. These parts together are the
signature of the method.
Method parameters are enclosed in parentheses and are separated by commas. Empty
parentheses indicate that the method requires no parameters. This class contains four
methods:
C#７ Note
This article discusses named methods. For information about anonymous functions,
see Lambda expr essions .
Method signatures
） Impor tant
A return type of a method is not part of the signature of the method for the
purposes of method overloading. However, it is part of the signature of the method
when determining the compatibility between a delegate and the method that it
points to.
abstract  class Motorcycle
{
    // Anyone can call this.Calling a method on an object is like accessing a field. After the object name, add a
period, the name of the method, and parentheses. Arguments are listed within the
parentheses, and are separated by commas. The methods of the Motorcycle class can
therefore be called as in the following example:
C#
The method definition specifies the names and types of any parameters that are
required. When calling code calls the method, it provides concrete values called
arguments for each parameter. The arguments must be compatible with the parameter    public void StartEngine () {/* Method statements here */  }
    // Only derived classes can call this.
    protected  void AddGas(int gallons ) { /* Method statements here */  }
    // Derived classes can override the base class implementation.
    public virtual int Drive(int miles, int speed) { /* Method statements  
here */ return 1; }
    // Derived classes must implement this.
    public abstract  double GetTopSpeed ();
}
Method access
class TestMotorcycle  : Motorcycle
{
    public override  double GetTopSpeed ()
    {
        return 108.4;
    }
    static void Main()
    {
        TestMotorcycle moto = new TestMotorcycle();
        moto.StartEngine();
        moto.AddGas( 15);
        moto.Drive( 5, 20);
        double speed = moto.GetTopSpeed();
        Console.WriteLine( "My top speed is {0}" , speed);
    }
}
Method parameters vs. argumentstype but the argument name (if any) used in the calling code doesn't have to be the
same as the parameter named defined in the method. For example:
C#
By default, when an instance of a value type  is passed to a method, its copy is passed
instead of the instance itself. Therefore, changes to the argument have no effect on the
original instance in the calling method. T o pass a value-type instance by reference, use
the ref keyword. For more information, see Passing V alue-T ype P arameters .
When an object of a reference type is passed to a method, a reference to the object is
passed. That is, the method receives not the object itself but an argument that indicates
the location of the object. If you change a member of the object by using this reference,
the change is reflected in the argument in the calling method, even if you pass the
object by value.
You create a reference type by using the class keyword, as the following example
shows:
C#public void Caller()
{
    int numA = 4;
    // Call with an int variable.
    int productA = Square(numA);
    int numB = 32;
    // Call with another int variable.
    int productB = Square(numB);
    // Call with an integer literal.
    int productC = Square( 12);
    // Call with an expression that evaluates to int.
    productC = Square(productA * 3);
}
int Square(int i)
{
    // Store input argument in a local variable.
    int input = i;
    return input * input;
}
Passing by reference vs. passing by valueNow, if you pass an object that is based on this type to a method, a reference to the
object is passed. The following example passes an object of type SampleRefType to
method ModifyObject:
C#
The example does essentially the same thing as the previous example in that it passes
an argument by value to a method. But, because a reference type is used, the result is
different. The modification that is made in ModifyObject to the value field of the
parameter, obj, also changes the value field of the argument, rt, in the TestRefType
method. The TestRefType method displays 33 as the output.
For more information about how to pass reference types by reference and by value, see
Passing R eference-T ype P arameters  and Reference T ypes.
Methods can return a value to the caller. If the return type (the type listed before the
method name) is not void, the method can return the value by using the return
statement . A statement with the return keyword followed by a value that matches the
return type will return that value to the method caller.
The value can be returned to the caller by value or by reference . Values are returned to
the caller by reference if the ref keyword is used in the method signature and it follows
each return keyword. For example, the following method signature and returnpublic class SampleRefType
{
    public int value;
}
public static void TestRefType ()
{
    SampleRefType rt = new SampleRefType();
    rt.value = 44;
    ModifyObject(rt);
    Console.WriteLine(rt. value);
}
static void ModifyObject (SampleRefType obj )
{
    obj.value = 33;
}
Return valuesstatement indicate that the method returns a variable named estDistance by reference
to the caller.
C#
The return keyword also stops the execution of the method. If the return type is void, a
return statement without a value is still useful to stop the execution of the method.
Without the return keyword, the method will stop executing when it reaches the end of
the code block. Methods with a non-void return type are required to use the return
keyword to return a value. For example, these two methods use the return keyword to
return integers:
C#
To use a value returned from a method, the calling method can use the method call
itself anywhere a value of the same type would be sufficient. Y ou can also assign the
return value to a variable. For example, the following two code examples accomplish the
same goal:
C#
C#public ref double GetEstimatedDistance ()
{
    return ref estDistance;
}
class SimpleMath
{
    public int AddTwoNumbers (int number1, int number2 )
    {
        return number1 + number2;
    }
    public int SquareANumber (int number)
    {
        return number * number;
    }
}
int result = obj.AddTwoNumbers( 1, 2);
result = obj.SquareANumber(result);
// The result is 9.
Console.WriteLine(result);Using a local variable, in this case, result, to store a value is optional. It may help the
readability of the code, or it may be necessary if you need to store the original value of
the argument for the entire scope of the method.
To use a value returned by reference from a method, you must declare a ref local
variable if you intend to modify its value. For example, if the
Planet.GetEstimatedDistance method returns a Double  value by reference, you can
define it as a ref local variable with code like the following:
C#
Returning a multi-dimensional array from a method, M, that modifies the array's
contents is not necessary if the calling function passed the array into M. You may return
the resulting array from M for good style or functional flow of values, but it is not
necessary because C# passes all reference types by value, and the value of an array
reference is the pointer to the array. In the method M, any changes to the array's
contents are observable by any code that has a reference to the array, as shown in the
following example:
C#result = obj.SquareANumber(obj.AddTwoNumbers( 1, 2));
// The result is 9.
Console.WriteLine(result);
ref double distance = ref Planet.GetEstimatedDistance();
static void Main(string[] args)
{
    int[,] matrix = new int[2, 2];
    FillMatrix(matrix);
    // matrix is now full of -1
}
public static void FillMatrix (int[,] matrix )
{
    for (int i = 0; i < matrix.GetLength( 0); i++)
    {
        for (int j = 0; j < matrix.GetLength( 1); j++)
        {
            matrix[i, j] = -1;
        }
    }
}By using the async feature, you can invoke asynchronous methods without using explicit
callbacks or manually splitting your code across multiple methods or lambda
expressions.
If you mark a method with the async  modifier, you can use the await  operator in the
method. When control reaches an await expression in the async method, control returns
to the caller, and progress in the method is suspended until the awaited task completes.
When the task is complete, execution can resume in the method.
An async method typically has a return type of Task<TR esult> , Task,
IAsyncEnumerable<T> or void. The void return type is used primarily to define event
handlers, where a void return type is required. An async method that returns void can't
be awaited, and the caller of a void-returning method can't catch exceptions that the
method throws. An async method can have any task-like return type .
In the following example, DelayAsync is an async method that has a return type of
Task<TR esult> . DelayAsync has a return statement that returns an integer. Therefore
the method declaration of DelayAsync must have a return type of Task<int>. Because
the return type is Task<int>, the evaluation of the await expression in
DoSomethingAsync produces an integer as the following statement demonstrates: int
result = await delayTask.
The Main method is an example of an async method that has a return type of Task. It
goes to the DoSomethingAsync method, and because it is expressed with a single line, it
can omit the async and await keywords. Because DoSomethingAsync is an async method,
the task for the call to DoSomethingAsync must be awaited, as the following statement
shows: await DoSomethingAsync();.
C#Async methods
７ Note
An async method returns to the caller when either it encounters the first awaited
object that's not yet complete or it gets to the end of the async method, whichever
occurs first.
class Program
{
    static Task Main() => DoSomethingAsync();An async method can't declare any ref or out parameters, but it can call methods that
have such parameters.
For more information about async methods, see Asynchronous programming with async
and await  and Async return types .
It is common to have method definitions that simply return immediately with the result
of an expression, or that have a single statement as the body of the method. There is a
syntax shortcut for defining such methods using =>:
C#
If the method returns void or is an async method, then the body of the method must
be a statement expression (same as with lambdas). For properties and indexers, they
must be read only, and you don't use the get accessor keyword.    static async Task DoSomethingAsync ()
    {
        Task<int> delayTask = DelayAsync();
        int result = await delayTask;
        // The previous two statements may be combined into
        // the following statement.
        //int result = await DelayAsync();
        Console.WriteLine( $"Result: {result} ");
    }
    static async Task<int> DelayAsync ()
    {
        await Task.Delay( 100);
        return 5;
    }
}
// Example output:
//   Result: 5
Expression body definitio ns
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator  +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);An iterator performs a custom iteration over a collection, such as a list or an array. An
iterator uses the yield return  statement to return each element one at a time. When a
yield return statement is reached, the current location in code is remembered.
Execution is restarted from that location when the iterator is called the next time.
You call an iterator from client code by using a foreach  statement.
The return type of an iterator can be IEnumerable , IEnumerable<T> ,
IAsyncEnumerable<T> , IEnumerator , or IEnumerator<T> .
For more information, see Iterators .
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.
C# Programming Guide
The C# type system
Access Modifiers
Static Classes and S tatic Class Members
Inheritance
Abstract and Sealed Classes and Class Members
params
out
ref
Method P arametersIterators
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
 Open a documentation issue
 Provide product feedbackmore information, see our
contributor guide .Local functions (C# Programming
Guide)
Article •05/27/2023
Local f unctions  are methods of a type that are nested in another member. They can only
be called from their containing member. Local functions can be declared in and called
from:
Methods, especially iterator methods and async methods
Constructors
Property accessors
Event accessors
Anonymous methods
Lambda expressions
Finalizers
Other local functions
However, local functions can't be declared inside an expression-bodied member.
Local functions make the intent of your code clear. Anyone reading your code can see
that the method is not callable except by the containing method. For team projects, they
also make it impossible for another developer to mistakenly call the method directly
from elsewhere in the class or struct.
A local function is defined as a nested method inside a containing member. Its definition
has the following syntax:
C#７ Note
In some cases, you can use a lambda expression to implement functionality also
supported by a local function. For a comparison, see Local functions vs. lambda
expressions .
Local function syntax
<modifiers> < return-type> <method-name> <parameter-list>You can use the following modifiers with a local function:
async
unsafe
static  A static local function can't capture local variables or instance state.
extern  An external local function must be static.
All local variables that are defined in the containing member, including its method
parameters, are accessible in a non-static local function.
Unlike a method definition, a local function definition cannot include the member access
modifier. Because all local functions are private, including an access modifier, such as
the private keyword, generates compiler error CS0106, "The modifier 'private' is not
valid for this item."
The following example defines a local function named AppendPathSeparator that is
private to a method named GetText:
C#
You can apply attributes to a local function, its parameters and type parameters, as the
following example shows:
C#７ Note
The <parameter-list> shouldn't contain the parameters named with contextual
keyword value. The compiler creates the temporary variable "value", which
contains the referenced outer variables, which later causes ambiguity and may also
cause an unexpected behaviour.
private static string GetText(string path, string filename )
{
     var reader = File.OpenText( $"{AppendPathSeparator(path)} {filename} ");
     var text = reader.ReadToEnd();
     return text;
     string AppendPathSeparator (string filepath )
     {
        return filepath.EndsWith( @"\") ? filepath : filepath + @"\";
     }
}The preceding example uses a special attribute  to assist the compiler in static analysis in
a nullable context.
One of the useful features of local functions is that they can allow exceptions to surface
immediately. For iterator methods, exceptions are surfaced only when the returned
sequence is enumerated, and not when the iterator is retrieved. For async methods, any
exceptions thrown in an async method are observed when the returned task is awaited.
The following example defines an OddSequence method that enumerates odd numbers
in a specified range. Because it passes a number greater than 100 to the OddSequence
enumerator method, the method throws an ArgumentOutOfRangeException . As the
output from the example shows, the exception surfaces only when you iterate the
numbers, and not when you retrieve the enumerator.
C##nullable enable
private static void Process(string?[] lines, string mark)
{
    foreach (var line in lines)
    {
        if (IsValid(line))
        {
            // Processing logic...
        }
    }
    bool IsValid([NotNullWhen( true)] string? line)
    {
        return !string.IsNullOrEmpty(line) && line.Length >= mark.Length;
    }
}
Local functions and exceptions
public class IteratorWithoutLocalExample
{
   public static void Main()
   {
      IEnumerable< int> xs = OddSequence( 50, 110);
      Console.WriteLine( "Retrieved enumerator..." );
      foreach (var x in xs)  // line 11
      {
         Console.Write( $"{x} ");
      }
   }If you put iterator logic into a local function, argument validation exceptions are thrown
when you retrieve the enumerator, as the following example shows:
C#   public static IEnumerable< int> OddSequence (int start, int end)
   {
      if (start < 0 || start > 99)
         throw new ArgumentOutOfRangeException( nameof(start), "start must be  
between 0 and 99." );
      if (end > 100)
         throw new ArgumentOutOfRangeException( nameof(end), "end must be  
less than or equal to 100." );
      if (start >= end)
         throw new ArgumentException( "start must be less than end." );
      for (int i = start; i <= end; i++)
      {
         if (i % 2 == 1)
            yield return i;
      }
   }
}
// The example displays the output like this:
//
//    Retrieved enumerator...
//    Unhandled exception. System.ArgumentOutOfRangeException: end must be  
less than or equal to 100. (Parameter 'end')
//    at IteratorWithoutLocalExample.OddSequence(Int32 start, Int32  
end)+MoveNext() in IteratorWithoutLocal.cs:line 22
//    at IteratorWithoutLocalExample.Main() in IteratorWithoutLocal.cs:line  
11
public class IteratorWithLocalExample
{
   public static void Main()
   {
      IEnumerable< int> xs = OddSequence( 50, 110);  // line 8
      Console.WriteLine( "Retrieved enumerator..." );
      foreach (var x in xs)
      {
         Console.Write( $"{x} ");
      }
   }
   public static IEnumerable< int> OddSequence (int start, int end)
   {
      if (start < 0 || start > 99)
         throw new ArgumentOutOfRangeException( nameof(start), "start must be  
between 0 and 99." );
      if (end > 100)At first glance, local functions and lambda expressions  are very similar. In many cases,
the choice between using lambda expressions and local functions is a matter of style
and personal preference . However, there are real differences in where you can use one
or the other that you should be aware of.
Let's examine the differences between the local function and lambda expression
implementations of the factorial algorithm. Here's the version using a local function:
C#
This version uses lambda expressions:         throw new ArgumentOutOfRangeException( nameof(end), "end must be  
less than or equal to 100." );
      if (start >= end)
         throw new ArgumentException( "start must be less than end." );
      return GetOddSequenceEnumerator();
      IEnumerable< int> GetOddSequenceEnumerator ()
      {
         for (int i = start; i <= end; i++)
         {
            if (i % 2 == 1)
               yield return i;
         }
      }
   }
}
// The example displays the output like this:
//
//    Unhandled exception. System.ArgumentOutOfRangeException: end must be  
less than or equal to 100. (Parameter 'end')
//    at IteratorWithLocalExample.OddSequence(Int32 start, Int32 end) in  
IteratorWithLocal.cs:line 22
//    at IteratorWithLocalExample.Main() in IteratorWithLocal.cs:line 8
Local functions vs. lambda expressions
public static int LocalFunctionFactorial (int n)
{
    return nthFactorial(n);
    int nthFactorial (int number) => number < 2 
        ? 1 
        : number * nthFactorial(number - 1);
}C#
Local functions are explicitly named like methods. Lambda expressions are anonymous
methods and need to be assigned to variables of a delegate type, typically either
Action or Func types. When you declare a local function, the process is like writing a
normal method; you declare a return type and a function signature.
Lambda expressions rely on the type of the Action/Func variable that they're assigned
to determine the argument and return types. In local functions, since the syntax is much
like writing a normal method, argument types and return type are already part of the
function declaration.
Beginning with C# 10, some lambda expressions have a natur al type , which enables the
compiler to infer the return type and parameter types of the lambda expression.
Lambda expressions are objects that are declared and assigned at run time. In order for
a lambda expression to be used, it needs to be definitely assigned: the Action/Func
variable that it will be assigned to must be declared and the lambda expression assigned
to it. Notice that LambdaFactorial must declare and initialize the lambda expression
nthFactorial before defining it. Not doing so results in a compile time error for
referencing nthFactorial before assigning it.
Local functions are defined at compile time. As they're not assigned to variables, they
can be referenced from any code location wher e it is in scope ; in our first examplepublic static int LambdaFactorial (int n)
{
    Func<int, int> nthFactorial = default(Func<int, int>);
    nthFactorial = number => number < 2
        ? 1
        : number * nthFactorial(number - 1);
    return nthFactorial(n);
}
Naming
Function signatures and lambda expression types
Definite assignmentLocalFunctionFactorial, we could declare our local function either above or below the
return statement and not trigger any compiler errors.
These differences mean that recursive algorithms are easier to create using local
functions. Y ou can declare and define a local function that calls itself. Lambda
expressions must be declared, and assigned a default value before they can be re-
assigned to a body that references the same lambda expression.
Lambda expressions are converted to delegates when they're declared. Local functions
are more flexible in that they can be written like a traditional method or as a delegate.
Local functions are only converted to delegates when us ed as a delegate.
If you declare a local function and only reference it by calling it like a method, it will not
be converted to a delegate.
The rules of definite assignment  also affect any variables that are captured by the local
function or lambda expression. The compiler can perform static analysis that enables
local functions to definitely assign captured variables in the enclosing scope. Consider
this example:
C#
The compiler can determine that LocalFunction definitely assigns y when called.
Because LocalFunction is called before the return statement, y is definitely assigned at
the return statement.
Note that when a local function captures variables in the enclosing scope, the local
function is implemented as a delegate type.Implementation as a delegate
Variable capture
int M()
{
    int y;
    LocalFunction();
    return y;
    void LocalFunction () => y = 0;
}
Heap allocationsDepending on their use, local functions can avoid heap allocations that are always
necessary for lambda expressions. If a local function is never converted to a delegate,
and none of the variables captured by the local function are captured by other lambdas
or local functions that are converted to delegates, the compiler can avoid heap
allocations.
Consider this async example:
C#
The closure for this lambda expression contains the address, index and name variables.
In the case of local functions, the object that implements the closure may be a struct
type. That struct type would be passed by reference to the local function. This difference
in implementation would save on an allocation.
The instantiation necessary for lambda expressions means extra memory allocations,
which may be a performance factor in time-critical code paths. Local functions do not
incur this overhead. In the example above, the local functions version has two fewer
allocations than the lambda expression version.
If you know that your local function won't be converted to a delegate and none of the
variables captured by it are captured by other lambdas or local functions that arepublic async Task<string> PerformLongRunningWorkLambda (string address, int 
index, string name)
{
    if (string.IsNullOrWhiteSpace(address))
        throw new ArgumentException(message: "An address is required" , 
paramName: nameof(address));
    if (index < 0)
        throw new ArgumentOutOfRangeException(paramName: nameof(index),  
message: "The index must be non-negative" );
    if (string.IsNullOrWhiteSpace(name))
        throw new ArgumentException(message: "You must supply a name" , 
paramName: nameof(name));
    Func<Task< string>> longRunningWorkImplementation = async () =>
    {
        var interimResult = await FirstWork(address);
        var secondResult = await SecondStep(index, name);
        return $"The results are {interimResult}  and {secondResult} . 
Enjoy.";
    };
    return await longRunningWorkImplementation();
}converted to delegates, you can guarantee that your local function avoids being
allocated on the heap by declaring it as a static local function.
C# Tip
Enable .NET code style rule IDE0062  to ensure that local functions are always
marked static.
７ Note
The local function equivalent of this method also uses a class for the closure.
Whether the closure for a local function is implemented as a class or a struct is
an implementation detail. A local function may use a struct whereas a lambda will
always use a class.
public async Task<string> PerformLongRunningWork (string address, int index, 
string name)
{
    if (string.IsNullOrWhiteSpace(address))
        throw new ArgumentException(message: "An address is required" , 
paramName: nameof(address));
    if (index < 0)
        throw new ArgumentOutOfRangeException(paramName: nameof(index),  
message: "The index must be non-negative" );
    if (string.IsNullOrWhiteSpace(name))
        throw new ArgumentException(message: "You must supply a name" , 
paramName: nameof(name));
    return await longRunningWorkImplementation();
    async Task<string> longRunningWorkImplementation ()
    {
        var interimResult = await FirstWork(address);
        var secondResult = await SecondStep(index, name);
        return $"The results are {interimResult}  and {secondResult} . 
Enjoy.";
    }
}
Usage of the yield keywordOne final advantage not demonstrated in this sample is that local functions can be
implemented as iterators, using the yield return syntax to produce a sequence of
values.
C#
The yield return statement is not allowed in lambda expressions. For more
information, see compiler error CS1621 .
While local functions may seem redundant to lambda expressions, they actually serve
different purposes and have different uses. Local functions are more efficient for the
case when you want to write a function that is called only from the context of another
method.
For more information, see the Local function declarations  section of the C# language
specification .
Use local function instead of lambda (style rule IDE0039)
Methodspublic IEnumerable< string> SequenceToLowercase (IEnumerable< string> input)
{
    if (!input.Any())
    {
        throw new ArgumentException( "There are no items to convert to  
lowercase." );
    }
    
    return LowercaseIterator();
    
    IEnumerable< string> LowercaseIterator ()
    {
        foreach (var output in input.Select(item => item.ToLower()))
        {
            yield return output;
        }
    }
}
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
 Provide product feedbackImplicitly typed local variables (C#
Programming Guide)
Article •03/14/2023
Local variables can be declared without giving an explicit type. The var keyword
instructs the compiler to infer the type of the variable from the expression on the right
side of the initialization statement. The inferred type may be a built-in type, an
anonymous type, a user-defined type, or a type defined in the .NET class library. For
more information about how to initialize arrays with var, see Implicitly T yped Arrays .
The following examples show various ways in which local variables can be declared with
var:
C#
It is important to understand that the var keyword does not mean "variant" and does
not indicate that the variable is loosely typed, or late-bound. It just means that the
compiler determines and assigns the most appropriate type.
The var keyword may be used in the following contexts:
On local variables (variables declared at method scope) as shown in the previous
example.// i is compiled as an int
var i = 5;
// s is compiled as a string
var s = "Hello";
// a is compiled as int[]
var a = new[] { 0, 1, 2 };
// expr is compiled as IEnumerable<Customer>
// or perhaps IQueryable<Customer>
var expr =
    from c in customers
    where c.City == "London"
    select c;
// anon is compiled as an anonymous type
var anon = new { Name = "Terry", Age = 34 };
// list is compiled as List<int>
var list = new List<int>();In a for initialization statement.
C#
In a foreach  initialization statement.
C#
In a using  statement.
C#
For more information, see How to use implicitly typed local variables and arrays in a
query expression .
In many cases the use of var is optional and is just a syntactic convenience. However,
when a variable is initialized with an anonymous type you must declare the variable as
var if you need to access the properties of the object at a later point. This is a common
scenario in LINQ query expressions. For more information, see Anonymous T ypes.
From the perspective of your source code, an anonymous type has no name. Therefore,
if a query variable has been initialized with var, then the only way to access the
properties in the returned sequence of objects is to use var as the type of the iteration
variable in the foreach statement.
C#for (var x = 1; x < 10; x++)
foreach (var item in list) {...}
using (var file = new StreamReader( "C:\\myfile.txt" )) {...}
var and anonymous types
class ImplicitlyTypedLocals2
{
    static void Main()
    {
        string[] words = { "aPPLE", "BlUeBeRrY" , "cHeRry"  };
        // If a query produces a sequence of anonymous types,
        // then use var in the foreach statement to access the properties.
        var upperLowerWords =The following restrictions apply to implicitly-typed variable declarations:
var can only be used when a local variable is declared and initialized in the same
statement; the variable cannot be initialized to null, or to a method group or an
anonymous function.
var cannot be used on fields at class scope.
Variables declared by using var cannot be used in the initialization expression. In
other words, this expression is legal: int i = (i = 20); but this expression
produces a compile-time error: var i = (i = 20);
Multiple implicitly-typed variables cannot be initialized in the same statement.
If a type named var is in scope, then the var keyword will resolve to that type
name and will not be treated as part of an implicitly typed local variable
declaration.
Implicit typing with the var keyword can only be applied to variables at local method
scope. Implicit typing is not available for class fields as the C# compiler would encounter
a logical paradox as it processed the code: the compiler needs to know the type of the
field, but it cannot determine the type until the assignment expression is analyzed, and
the expression cannot be evaluated without knowing the type. Consider the following
code:
C#             from w in words
             select new { Upper = w.ToUpper(), Lower = w.ToLower() };
        // Execute the query
        foreach (var ul in upperLowerWords)
        {
            Console.WriteLine( "Uppercase: {0}, Lowercase: {1}" , ul.Upper,  
ul.Lower);
        }
    }
}
/* Outputs:
    Uppercase: APPLE, Lowercase: apple
    Uppercase: BLUEBERRY, Lowercase: blueberry
    Uppercase: CHERRY, Lowercase: cherry
 */
RemarksbookTitles is a class field given the type var. As the field has no expression to evaluate,
it is impossible for the compiler to infer what type bookTitles is supposed to be. In
addition, adding an expression to the field (like you would for a local variable) is also
insufficient:
C#
When the compiler encounters fields during code compilation, it records each field's
type before processing any expressions associated with it. The compiler encounters the
same paradox trying to parse bookTitles: it needs to know the type of the field, but the
compiler would normally determine var's type by analyzing the expression, which isn't
possible without knowing the type beforehand.
You may find that var can also be useful with query expressions in which the exact
constructed type of the query variable is difficult to determine. This can occur with
grouping and ordering operations.
The var keyword can also be useful when the specific type of the variable is tedious to
type on the keyboard, or is obvious, or does not add to the readability of the code. One
example where var is helpful in this manner is with nested generic types such as those
used with group operations. In the following query, the type of the query variable is
IEnumerable<IGrouping<string, Student>>. As long as you and others who must
maintain your code understand this, there is no problem with using implicit typing for
convenience and brevity.
C#
The use of var helps simplify your code, but its use should be restricted to cases where
it is required, or when it makes your code easier to read. For more information about
when to use var properly, see the Implicitly typed local variables  section on the C#
Coding Guidelines article.private var bookTitles;
private var bookTitles = new List<string>();
// Same as previous example except we use the entire last name as a key.
// Query variable is an IEnumerable<IGrouping<string, Student>>
var studentQuery3 =
    from student in students
    group student by student.Last;C# Reference
Implicitly T yped Arrays
How to use implicitly typed local variables and arrays in a query expression
Anonymous T ypes
Object and Collection Initializers
var
LINQ in C#
LINQ (Language-Integrated Query)
Iteration statements
using statementSee alsoHow to use implicitly typed local
variables and arrays in a query
expression (C# Programming Guide)
Article •09/21/2022
You can use implicitly typed local variables whenever you want the compiler to
determine the type of a local variable. Y ou must use implicitly typed local variables to
store anonymous types, which are often used in query expressions. The following
examples illustrate both optional and required uses of implicitly typed local variables in
queries.
Implicitly typed local variables are declared by using the var contextual keyword. For
more information, see Implicitly T yped Local V ariables  and Implicitly T yped Arrays .
The following example shows a common scenario in which the var keyword is required:
a query expression that produces a sequence of anonymous types. In this scenario, both
the query variable and the iteration variable in the foreach statement must be implicitly
typed by using var because you do not have access to a type name for the anonymous
type. For more information about anonymous types, see Anonymous T ypes.
C#Examples
private static void QueryNames (char firstLetter )
{
    // Create the query. Use of var is required because
    // the query produces a sequence of anonymous types:
    // System.Collections.Generic.IEnumerable<????>.
    var studentQuery =
        from student in students
        where student.FirstName[ 0] == firstLetter
        select new { student.FirstName, student.LastName };
    // Execute the query and display the results.
    foreach (var anonType in studentQuery)
    {
        Console.WriteLine( "First = {0}, Last = {1}" , anonType.FirstName,  
anonType.LastName);
    }
}The following example uses the var keyword in a situation that is similar, but in which
the use of var is optional. Because student.LastName is a string, execution of the query
returns a sequence of strings. Therefore, the type of queryId could be declared as
System.Collections.Generic.IEnumerable<string> instead of var. Keyword var is used
for convenience. In the example, the iteration variable in the foreach statement is
explicitly typed as a string, but it could instead be declared by using var. Because the
type of the iteration variable is not an anonymous type, the use of var is an option, not
a requirement. R emember, var itself is not a type, but an instruction to the compiler to
infer and assign the type.
C#
C# Programming Guide
Extension Methods
LINQ (Language-Integrated Query)
LINQ in C#// Variable queryId could be declared by using
// System.Collections.Generic.IEnumerable<string>
// instead of var.
var queryId =
    from student in students
    where student.Id > 111
    select student.LastName;
// Variable str could be declared by using var instead of string.
foreach (string str in queryId)
{
    Console.WriteLine( "Last name: {0}" , str);
}
See alsoExtension Methods (C# Programming
Guide)
Article •09/29/2022
Extension methods enable you to "add" methods to existing types without creating a
new derived type, recompiling, or otherwise modifying the original type. Extension
methods are static methods, but they're called as if they were instance methods on the
extended type. For client code written in C#, F# and Visual Basic, there's no apparent
difference between calling an extension method and the methods defined in a type.
The most common extension methods are the LINQ standard query operators that add
query functionality to the existing System.Collections.IEnumerable  and
System.Collections.Generic.IEnumerable<T>  types. T o use the standard query operators,
first bring them into scope with a using System.Linq directive. Then any type that
implements IEnumerable<T>  appears to have instance methods such as GroupBy ,
OrderBy , Average , and so on. Y ou can see these additional methods in IntelliSense
statement completion when you type "dot" after an instance of an IEnumerable<T>  type
such as List<T>  or Array .
The following example shows how to call the standard query operator OrderBy method
on an array of integers. The expression in parentheses is a lambda expression. Many
standard query operators take lambda expressions as parameters, but this isn't a
requirement for extension methods. For more information, see Lambda Expressions .
C#OrderBy Example
class ExtensionMethods2
{
    static void Main()
    {
        int[] ints = { 10, 45, 15, 39, 21, 26 };
        var result = ints.OrderBy(g => g);
        foreach (var i in result)
        {
            System.Console.Write(i + " ");
        }
    }
}
//Output: 10 15 21 26 39 45Extension methods are defined as static methods but are called by using instance
method syntax. Their first parameter specifies which type the method operates on. The
parameter is preceded by the this modifier. Extension methods are only in scope when
you explicitly import the namespace into your source code with a using directive.
The following example shows an extension method defined for the System.S tring  class.
It's defined inside a non-nested, non-generic static class:
C#
The WordCount extension method can be brought into scope with this using directive:
C#
And it can be called from an application by using this syntax:
C#
You invoke the extension method in your code with instance method syntax. The
intermediate language (IL) generated by the compiler translates your code into a call on
the static method. The principle of encapsulation is not really being violated. Extension
methods cannot access private variables in the type they are extending.
Both the MyExtensions class and the WordCount method are static, and it can be
accessed like all other static members. The WordCount method can be invoked like
other static methods as follows:
C#namespace  ExtensionMethods
{
    public static class MyExtensions
    {
        public static int WordCount (this string str)
        {
            return str.Split( new char[] { ' ', '.', '?' },
                             StringSplitOptions.RemoveEmptyEntries).Length;
        }
    }
}
using ExtensionMethods;
string s = "Hello Extension Methods" ;
int i = s.WordCount();The preceding C# code:
Declares and assigns a new string named s with a value of "Hello Extension
Methods".
Calls MyExtensions.WordCount given argument s
For more information, see How to implement and call a custom extension method .
In general, you'll probably be calling extension methods far more often than
implementing your own. Because extension methods are called by using instance
method syntax, no special knowledge is required to use them from client code. T o
enable extension methods for a particular type, just add a using directive for the
namespace in which the methods are defined. For example, to use the standard query
operators, add this using directive to your code:
C#
(You may also have to add a reference to S ystem.Core.dll.) Y ou'll notice that the standard
query operators now appear in IntelliSense as additional methods available for most
IEnumerable<T>  types.
You can use extension methods to extend a class or interface, but not to override them.
An extension method with the same name and signature as an interface or class method
will never be called. At compile time, extension methods always have lower priority than
instance methods defined in the type itself. In other words, if a type has a method
named Process(int i), and you have an extension method with the same signature, the
compiler will always bind to the instance method. When the compiler encounters a
method invocation, it first looks for a match in the type's instance methods. If no match
is found, it will search for any extension methods that are defined for the type, and bind
to the first extension method that it finds.string s = "Hello Extension Methods" ;
int i = MyExtensions.WordCount(s);
using System.Linq;
Binding Extension Methods at Compile Time
ExampleThe following example demonstrates the rules that the C# compiler follows in
determining whether to bind a method call to an instance method on the type, or to an
extension method. The static class Extensions contains extension methods defined for
any type that implements IMyInterface. Classes A, B, and C all implement the
interface.
The MethodB extension method is never called because its name and signature exactly
match methods already implemented by the classes.
When the compiler can't find an instance method with a matching signature, it will bind
to a matching extension method if one exists.
C#
// Define an interface named IMyInterface.
namespace  DefineIMyInterface
{
    using System;
    public interface  IMyInterface
    {
        // Any class that implements IMyInterface must define a method
        // that matches the following signature.
        void MethodB();
    }
}
// Define extension methods for IMyInterface.
namespace  Extensions
{
    using System;
    using DefineIMyInterface;
    // The following extension methods can be accessed by instances of any
    // class that implements IMyInterface.
    public static class Extension
    {
        public static void MethodA(this IMyInterface myInterface, int i)
        {
            Console.WriteLine
                ("Extension.MethodA(this IMyInterface myInterface, int i)" );
        }
        public static void MethodA(this IMyInterface myInterface, string s)
        {
            Console.WriteLine
                ("Extension.MethodA(this IMyInterface myInterface, string  
s)");
        }
        // This method is never called in ExtensionMethodsDemo1, because  each
        // of the three classes A, B, and C implements a method named  
MethodB
        // that has a matching signature.
        public static void MethodB(this IMyInterface myInterface )
        {
            Console.WriteLine
                ("Extension.MethodB(this IMyInterface myInterface)" );
        }
    }
}
// Define three classes that implement IMyInterface, and then use them to  
test
// the extension methods.
namespace  ExtensionMethodsDemo1
{
    using System;
    using Extensions;
    using DefineIMyInterface;
    class A : IMyInterface
    {
        public void MethodB() { Console.WriteLine( "A.MethodB()" ); }
    }
    class B : IMyInterface
    {
        public void MethodB() { Console.WriteLine( "B.MethodB()" ); }
        public void MethodA(int i) { Console.WriteLine( "B.MethodA(int i)" ); 
}
    }
    class C : IMyInterface
    {
        public void MethodB() { Console.WriteLine( "C.MethodB()" ); }
        public void MethodA(object obj)
        {
            Console.WriteLine( "C.MethodA(object obj)" );
        }
    }
    class ExtMethodDemo
    {
        static void Main(string[] args)
        {
            // Declare an instance of class A, class B, and class C.
            A a = new A();
            B b = new B();
            C c = new C();
            // For a, b, and c, call the following methods:
            //      -- MethodA with an int argument
            //      -- MethodA with a string argument
            //      -- MethodB with no argument.In the past, it was common to create "Collection Classes" that implemented the
System.Collections.Generic.IEnumerable<T>  interface for a given type and contained
functionality that acted on collections of that type. While there's nothing wrong with            // A contains no MethodA, so each call to MethodA resolves to
            // the extension method that has a matching signature.
            a.MethodA( 1);           // Extension.MethodA(IMyInterface, int)
            a.MethodA( "hello");     // Extension.MethodA(IMyInterface,  
string)
            // A has a method that matches the signature of the following  
call
            // to MethodB.
            a.MethodB();            // A.MethodB()
            // B has methods that match the signatures of the following
            // method calls.
            b.MethodA( 1);           // B.MethodA(int)
            b.MethodB();            // B.MethodB()
            // B has no matching method for the following call, but
            // class Extension does.
            b.MethodA( "hello");     // Extension.MethodA(IMyInterface,  
string)
            // C contains an instance method that matches each of the  
following
            // method calls.
            c.MethodA( 1);           // C.MethodA(object)
            c.MethodA( "hello");     // C.MethodA(object)
            c.MethodB();            // C.MethodB()
        }
    }
}
/* Output:
    Extension.MethodA(this IMyInterface myInterface, int i)
    Extension.MethodA(this IMyInterface myInterface, string s)
    A.MethodB()
    B.MethodA(int i)
    B.MethodB()
    Extension.MethodA(this IMyInterface myInterface, string s)
    C.MethodA(object obj)
    C.MethodA(object obj)
    C.MethodB()
 */
Common Usage Patterns
Collection Functionalitycreating this type of collection object, the same functionality can be achieved by using
an extension on the System.Collections.Generic.IEnumerable<T> . Extensions have the
advantage of allowing the functionality to be called from any collection such as an
System.Array  or System.Collections.Generic.List<T>  that implements
System.Collections.Generic.IEnumerable<T>  on that type. An example of this using an
Array of Int32 can be found earlier in this article .
When using an Onion Architecture or other layered application design, it's common to
have a set of Domain Entities or Data T ransfer Objects that can be used to communicate
across application boundaries. These objects generally contain no functionality, or only
minimal functionality that applies to all layers of the application. Extension methods can
be used to add functionality that is specific to each application layer without loading the
object down with methods not needed or wanted in other layers.
C#
Rather than creating new objects when reusable functionality needs to be created, we
can often extend an existing type, such as a .NET or CLR type. As an example, if we don't
use extension methods, we might create an Engine or Query class to do the work of
executing a query on a SQL Server that may be called from multiple places in our code.
However we can instead extend the System.Data.SqlClient.SqlConnection  class using
extension methods to perform that query from anywhere we have a connection to a SQL
Server. Other examples might be to add common functionality to the System.S tring
class, extend the data processing capabilities of the System.IO.File  and System.IO.S tream
objects, and System.Exception  objects for specific error handling functionality. These
types of use-cases are limited only by your imagination and good sense.Layer-Specific Functionality
public class DomainEntity
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
static class DomainEntityExtensions
{
    static string FullName (this DomainEntity value)
        => $"{value.FirstName}  {value.LastName} ";
}
Extending Predefined TypesExtending predefined types can be difficult with struct types because they're passed by
value to methods. That means any changes to the struct are made to a copy of the
struct. Those changes aren't visible once the extension method exits. Y ou can add the
ref modifier to the first argument making it a ref extension method. The ref keyword
can appear before or after the this keyword without any semantic differences. Adding
the ref modifier indicates that the first argument is passed by reference. This enables
you to write extension methods that change the state of the struct being extended (note
that private members are not accessible). Only value types or generic types constrained
to struct (see struct  constraint  for more information) are allowed as the first parameter
of a ref extension method. The following example shows how to use a ref extension
method to directly modify a built-in type without the need to reassign the result or pass
it through a function with the ref keyword:
C#
This next example demonstrates ref extension methods for user-defined struct types:
C#public static class IntExtensions
{
    public static void Increment (this int number)
        => number++;
    // Take note of the extra ref keyword here
    public static void RefIncrement (this ref int number)
        => number++;
}
public static class IntProgram
{
    public static void Test()
    {
        int x = 1;
        // Takes x by value leading to the extension method
        // Increment modifying its own copy, leaving x unchanged
        x.Increment();
        Console.WriteLine( $"x is now {x}"); // x is now 1
        // Takes x by reference leading to the extension method
        // RefIncrement changing the value of x directly
        x.RefIncrement();
        Console.WriteLine( $"x is now {x}"); // x is now 2
    }
}While it's still considered preferable to add functionality by modifying an object's code
or deriving a new type whenever it's reasonable and possible to do so, extension
methods have become a crucial option for creating reusable functionality throughout
the .NET ecosystem. For those occasions when the original source isn't under your
control, when a derived object is inappropriate or impossible, or when the functionality
shouldn't be exposed beyond its applicable scope, Extension methods are an excellent
choice.
For more information on derived types, see Inheritance .public struct Account
{
    public uint id;
    public float balance;
    private int secret;
}
public static class AccountExtensions
{
    // ref keyword can also appear before the this keyword
    public static void Deposit(ref this Account account, float amount)
    {
        account.balance += amount;
        // The following line results in an error as an extension
        // method is not allowed to access private members
        // account.secret = 1; // CS0122
    }
}
public static class AccountProgram
{
    public static void Test()
    {
        Account account = new()
        {
            id = 1,
            balance = 100f
        };
        Console.WriteLine( $"I have $ {account.balance} "); // I have $100
        account.Deposit( 50f);
        Console.WriteLine( $"I have $ {account.balance} "); // I have $150
    }
}
General GuidelinesWhen using an extension method to extend a type whose source code you aren't in
control of, you run the risk that a change in the implementation of the type will cause
your extension method to break.
If you do implement extension methods for a given type, remember the following
points:
An extension method will never be called if it has the same signature as a method
defined in the type.
Extension methods are brought into scope at the namespace level. For example, if
you have multiple static classes that contain extension methods in a single
namespace named Extensions, they'll all be brought into scope by the using
Extensions; directive.
For a class library that you implemented, you shouldn't use extension methods to avoid
incrementing the version number of an assembly. If you want to add significant
functionality to a library for which you own the source code, follow the .NET guidelines
for assembly versioning. For more information, see Assembly V ersioning .
C# Programming Guide
Parallel Programming Samples (these include many example extension methods)
Lambda Expressions
Standard Query Operators Overview
Conversion rules for Instance parameters and their impact
Extension methods Interoperability between languages
Extension methods and Curried Delegates
Extension method Binding and Error reportingSee also
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
 Provide product feedbackHow to implement and call a custom
extension method  (C# Programming
Guide)
Article •09/15/2021
This topic shows how to implement your own extension methods for any .NET type.
Client code can use your extension methods by adding a reference to the DLL that
contains them, and adding a using  directive that specifies the namespace in which the
extension methods are defined.
1. Define a static class  to contain the extension method.
The class must be visible to client code. For more information about accessibility
rules, see Access Modifiers .
2. Implement the extension method as a static method with at least the same
visibility as the containing class.
3. The first parameter of the method specifies the type that the method operates on;
it must be preceded with the this modifier.
4. In the calling code, add a using directive to specify the namespace  that contains
the extension method class.
5. Call the methods as if they were instance methods on the type.
Note that the first parameter is not specified by calling code because it represents
the type on which the operator is being applied, and the compiler already knows
the type of your object. Y ou only have to provide arguments for parameters 2
through n.
The following example implements an extension method named WordCount in the
CustomExtensions.StringExtension class. The method operates on the String  class, which
is specified as the first method parameter. The CustomExtensions namespace is imported
into the application namespace, and the method is called inside the Main method.To define and call the extension method
ExampleC#
Extension methods present no specific security vulnerabilities. They can never be used to
impersonate existing methods on a type, because all name collisions are resolved in
favor of the instance or static method defined by the type itself. Extension methods
cannot access any private data in the extended class.using System.Linq;
using System.Text;
using System;
namespace  CustomExtensions
{
    // Extension methods must be defined in a static class.
    public static class StringExtension
    {
        // This is the extension method.
        // The first parameter takes the "this" modifier
        // and specifies the type for which the method is defined.
        public static int WordCount (this string str)
        {
            return str.Split( new char[] {' ', '.','?'}, 
StringSplitOptions.RemoveEmptyEntries).Length;
        }
    }
}
namespace  Extension_Methods_Simple
{
    // Import the extension method namespace.
    using CustomExtensions;
    class Program
    {
        static void Main(string[] args)
        {
            string s = "The quick brown fox jumped over the lazy dog." ;
            // Call the method as if it were an
            // instance method on the type. Note that the first
            // parameter is not specified by the calling code.
            int i = s.WordCount();
            System.Console.WriteLine( "Word count of s is {0}" , i);
        }
    }
}
.NET Security
See alsoC# Programming Guide
Extension Methods
LINQ (Language-Integrated Query)
Static Classes and S tatic Class Members
protected
internal
public
this
namespaceHow to create a new method for an
enumeration (C# Programming Guide)
Article •09/15/2021
You can use extension methods to add functionality specific to a particular enum type.
In the following example, the Grades enumeration represents the possible letter grades
that a student may receive in a class. An extension method named Passing is added to
the Grades type so that each instance of that type now "knows" whether it represents a
passing grade or not.
C#Example
using System;  
using System.Collections.Generic;
using System.Text;  
using System.Linq;  
namespace  EnumExtension  
{ 
    // Define an extension method in a non-nested static class.  
    public static class Extensions  
    { 
        public static Grades minPassing = Grades.D;  
        public static bool Passing(this Grades grade ) 
        {  
            return grade >= minPassing;  
        }  
    } 
    public enum Grades { F = 0, D=1, C=2, B=3, A=4 }; 
    class Program 
    { 
        static void Main(string[] args) 
        {  
            Grades g1 = Grades.D;
            Grades g2 = Grades.F;
            Console.WriteLine( "First {0} a passing grade." , g1.Passing() ?  
"is" : "is not" ); 
            Console.WriteLine( "Second {0} a passing grade." , g2.Passing() ?  
"is" : "is not" ); 
            Extensions.minPassing = Grades.C;  
            Console.WriteLine( "\r\nRaising the bar!\r\n" ); 
            Console.WriteLine( "First {0} a passing grade." , g1.Passing() ?  Note that the Extensions class also contains a static variable that is updated
dynamically and that the return value of the extension method reflects the current value
of that variable. This demonstrates that, behind the scenes, extension methods are
invoked directly on the static class in which they are defined.
C# Programming Guide
Extension Methods"is" : "is not" ); 
            Console.WriteLine( "Second {0} a passing grade." , g2.Passing() ?  
"is" : "is not" ); 
        }  
    } 
  } 
/* Output:  
    First is a passing grade.  
    Second is not a passing grade.  
    Raising the bar!  
    First is not a passing grade.
    Second is not a passing grade.  
 */ 
See alsoNamed and Optional Arguments (C#
Programming Guide)
Article •02/25/2023
Named ar guments  enable you to specify an argument for a parameter by matching the
argument with its name rather than with its position in the parameter list. Optional
arguments  enable you to omit arguments for some parameters. Both techniques can be
used with methods, indexers, constructors, and delegates.
When you use named and optional arguments, the arguments are evaluated in the
order in which they appear in the argument list, not the parameter list.
Named and optional parameters enable you to supply arguments for selected
parameters. This capability greatly eases calls to C OM interfaces such as the Microsoft
Office Automation APIs.
Named arguments free you from matching the order of arguments to the order of
parameters in the parameter lists of called methods. The argument for each parameter
can be specified by parameter name. For example, a function that prints order details
(such as, seller name, order number & product name) can be called by sending
arguments by position, in the order defined by the function.
C#
If you don't remember the order of the parameters but know their names, you can send
the arguments in any order.
C#
Named arguments also improve the readability of your code by identifying what each
argument represents. In the example method below, the sellerName can't be null or
white space. As both sellerName and productName are string types, instead of sendingNamed arguments
PrintOrderDetails( "Gift Shop" , 31, "Red Mug" );
PrintOrderDetails(orderNum: 31, productName: "Red Mug" , sellerName: "Gift 
Shop");
PrintOrderDetails(productName: "Red Mug" , sellerName: "Gift Shop" , orderNum:  
31);arguments by position, it makes sense to use named arguments to disambiguate the
two and reduce confusion for anyone reading the code.
Named arguments, when used with positional arguments, are valid as long as
they're not followed by any positional arguments, or
C#
they're used in the correct position. In the example below, the parameter orderNum
is in the correct position but isn't explicitly named.
C#
Positional arguments that follow any out-of-order named arguments are invalid.
C#
The following code implements the examples from this section along with some
additional ones.
C#PrintOrderDetails( "Gift Shop" , 31, productName: "Red Mug" );
PrintOrderDetails(sellerName: "Gift Shop" , 31, productName: "Red Mug" );
// This generates CS1738: Named argument specifications must appear after  
all fixed arguments have been specified.
PrintOrderDetails(productName: "Red Mug" , 31, "Gift Shop" );
Example
class NamedExample
{
    static void Main(string[] args)
    {
        // The method can be called in the normal way, by using positional  
arguments.
        PrintOrderDetails( "Gift Shop" , 31, "Red Mug" );
        // Named arguments can be supplied for the parameters in any order.
        PrintOrderDetails(orderNum: 31, productName: "Red Mug" , sellerName: 
"Gift Shop" );
        PrintOrderDetails(productName: "Red Mug" , sellerName: "Gift Shop" , 
orderNum: 31);The definition of a method, constructor, indexer, or delegate can specify its parameters
are required or optional. Any call must provide arguments for all required parameters,
but can omit arguments for optional parameters.
Each optional parameter has a default value as part of its definition. If no argument is
sent for that parameter, the default value is used. A default value must be one of the
following types of expressions:
a constant expression;
an expression of the form new ValType(), where ValType is a value type, such as an
enum  or a struct ;
an expression of the form default(V alType), where ValType is a value type.
Optional parameters are defined at the end of the parameter list, after any required
parameters. If the caller provides an argument for any one of a succession of optional
parameters, it must provide arguments for all preceding optional parameters. Comma-
separated gaps in the argument list aren't supported. For example, in the following        // Named arguments mixed with positional arguments are valid
        // as long as they are used in their correct position.
        PrintOrderDetails( "Gift Shop" , 31, productName: "Red Mug" );
        PrintOrderDetails(sellerName: "Gift Shop" , 31, productName: "Red 
Mug"); 
        PrintOrderDetails( "Gift Shop" , orderNum: 31, "Red Mug" );
        // However, mixed arguments are invalid if used out-of-order.
        // The following statements will cause a compiler error.
        // PrintOrderDetails(productName: "Red Mug", 31, "Gift Shop");
        // PrintOrderDetails(31, sellerName: "Gift Shop", "Red Mug");
        // PrintOrderDetails(31, "Red Mug", sellerName: "Gift Shop");
    }
    static void PrintOrderDetails (string sellerName, int orderNum, string 
productName )
    {
        if (string.IsNullOrWhiteSpace(sellerName))
        {
            throw new ArgumentException(message: "Seller name cannot be null  
or empty." , paramName: nameof(sellerName));
        }
        Console.WriteLine( $"Seller: {sellerName} , Order #: {orderNum} , 
Product: {productName} ");
    }
}
Optional argumentscode, instance method ExampleMethod is defined with one required and two optional
parameters.
C#
The following call to ExampleMethod causes a compiler error, because an argument is
provided for the third parameter but not for the second.
C#
However, if you know the name of the third parameter, you can use a named argument
to accomplish the task.
C#
IntelliSense uses brackets to indicate optional parameters, as shown in the following
illustration:
In the following example, the constructor for ExampleClass has one parameter, which is
optional. Instance method ExampleMethod has one required parameter, required, andpublic void ExampleMethod (int required, string optionalstr = "default  
string",
    int optionalint = 10)
//anExample.ExampleMethod(3, ,4);
anExample.ExampleMethod( 3, optionalint: 4);
７ Note
You can also declare optional parameters by using the .NET OptionalA ttribut e
class. OptionalAttribute parameters do not require a default value. However, if a
default value is desired, take a look at DefaultP aramet erValueA ttribut e class.
Exampletwo optional parameters, optionalstr and optionalint. The code in Main shows the
different ways in which the constructor and method can be invoked.
C#
namespace  OptionalNamespace
{
    class OptionalExample
    {
        static void Main(string[] args)
        {
            // Instance anExample does not send an argument for the  
constructor's
            // optional parameter.
            ExampleClass anExample = new ExampleClass();
            anExample.ExampleMethod( 1, "One", 1);
            anExample.ExampleMethod( 2, "Two");
            anExample.ExampleMethod( 3);
            // Instance anotherExample sends an argument for the  
constructor's
            // optional parameter.
            ExampleClass anotherExample = new ExampleClass( "Provided name" );
            anotherExample.ExampleMethod( 1, "One", 1);
            anotherExample.ExampleMethod( 2, "Two");
            anotherExample.ExampleMethod( 3);
            // The following statements produce compiler errors.
            // An argument must be supplied for the first parameter, and it
            // must be an integer.
            //anExample.ExampleMethod("One", 1);
            //anExample.ExampleMethod();
            // You cannot leave a gap in the provided arguments.
            //anExample.ExampleMethod(3, ,4);
            //anExample.ExampleMethod(3, 4);
            // You can use a named parameter to make the previous
            // statement work.
            anExample.ExampleMethod( 3, optionalint: 4);
        }
    }
    class ExampleClass
    {
        private string _name;
        // Because the parameter for the constructor, name, has a default
        // value assigned to it, it is optional.
        public ExampleClass (string name = "Default name" )
        {
            _name = name;
        }The preceding code shows a number of examples where optional parameters aren't
applied correctly. The first illustrates that an argument must be supplied for the first
parameter, which is required.
Named and optional arguments, along with support for dynamic objects, greatly
improve interoperability with C OM APIs, such as Office Automation APIs.
For example, the AutoFormat  method in the Microsoft Office Excel Range  interface has
seven parameters, all of which are optional. These parameters are shown in the
following illustration:
However, you can greatly simplify the call to AutoFormat by using named and optional
arguments. Named and optional arguments enable you to omit the argument for an
optional parameter if you don't want to change the parameter's default value. In the
following call, a value is specified for only one of the seven parameters.        // The first parameter, required, has no default value assigned
        // to it. Therefore, it is not optional. Both optionalstr and
        // optionalint have default values assigned to them. They are  
optional.
        public void ExampleMethod (int required, string optionalstr = 
"default string" ,
            int optionalint = 10)
        {
            Console.WriteLine(
                $"{_name}: {required} , {optionalstr} , and {optionalint} .");
        }
    }
    // The output from this example is the following:
    // Default name: 1, One, and 1.
    // Default name: 2, Two, and 10.
    // Default name: 3, default string, and 10.
    // Provided name: 1, One, and 1.
    // Provided name: 2, Two, and 10.
    // Provided name: 3, default string, and 10.
    // Default name: 3, default string, and 4.
}
COM interfacesC#
For more information and examples, see How to use named and optional arguments in
Office programming  and How to access Office interop objects by using C# features .
Use of named and optional arguments affects overload resolution in the following ways:
A method, indexer, or constructor is a candidate for execution if each of its
parameters either is optional or corresponds, by name or by position, to a single
argument in the calling statement, and that argument can be converted to the
type of the parameter.
If more than one candidate is found, overload resolution rules for preferred
conversions are applied to the arguments that are explicitly specified. Omitted
arguments for optional parameters are ignored.
If two candidates are judged to be equally good, preference goes to a candidate
that doesn't have optional parameters for which arguments were omitted in the
call. Overload resolution generally prefers candidates that have fewer parameters.
For more information, see the C# Language Specification . The language specification is
the definitive source for C# syntax and usage.var excelApp = new Microsoft.Office.Interop.Excel.Application();
excelApp.Workbooks.Add();
excelApp.Visible = true;
var myFormat =
    
Microsoft.Office.Interop.Excel.XlRangeAutoFormat.xlRangeAutoFormatAccounting
1;
excelApp.Range[ "A1", "B4"].AutoFormat( Format: myFormat );
Overload resolutio n
C# language specification
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review.NET feedb ack
The .NET documentation is open
source. Provide feedback here.issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackConstructors (C# programming guide)
Article •04/10/2023
Whenever an instance of a class  or a struct  is created, its constructor is called. A class or
struct may have multiple constructors that take different arguments. Constructors
enable the programmer to set default values, limit instantiation, and write code that is
flexible and easy to read. For more information and examples, see Instance constructors
and Using constructors .
There are several actions that are part of initializing a new instance. Those actions take
place in the following order:
1. Instance fields ar e set to 0. This is typically done by the runtime.
2. Field initializer s run. The field initializers in the most derived type run.
3. Base type f ield initializer s run. Field initializers starting with the direct base through
each base type to System.Object .
4. Base inst ance constr uctors run. Any instance constructors, starting with
Object.Object  through each base class to the direct base class.
5. The inst ance constr uctor runs. The instance constructor for the type runs.
6. Object initializer s run. If the expression includes any object initializers, those run
after the instance constructor runs. Object initializers run in the textual order.
The preceding actions take place when a new instance is initialized. If a new instance of
a struct is set to its default value, all instance fields are set to 0.
If the static constructor  hasn't run, the static constructor runs before any of the instance
constructor actions take place.
A constructor is a method whose name is the same as the name of its type. Its method
signature includes only an optional access modifier , the method name and its parameter
list; it does not include a return type. The following example shows the constructor for a
class named Person.
C#Constructor syntax
public class Person 
{ 
   private string last; 
   private string first; 
   public Person(string lastName, string firstName ) If a constructor can be implemented as a single statement, you can use an expression
body definition . The following example defines a Location class whose constructor has
a single string parameter named name . The expression body definition assigns the
argument to the locationName field.
C#
The previous examples have all shown instance constructors, which create a new object.
A class or struct can also have a static constructor, which initializes static members of
the type. Static constructors are parameterless. If you don't provide a static constructor
to initialize static fields, the C# compiler initializes static fields to their default value as
listed in the Default values of C# types  article.
The following example uses a static constructor to initialize a static field.
C#   { 
      last = lastName;  
      first = firstName;  
   } 
   // Remaining implementation of Person class.  
} 
public class Location  
{ 
   private string locationName;  
   public Location (string name) => Name = name;  
   public string Name 
   { 
      get => locationName;  
      set => locationName = value; 
   } 
} 
Static constructors
public class Child : Person 
{ 
   private static int maximumAge;  
   public Child(string lastName, string firstName ) : base(lastName,  
firstName ) 
   { } You can also define a static constructor with an expression body definition, as the
following example shows.
C#
For more information and examples, see Static Constructors .
Using constructors
Instance constructors
Private constructors
Static constructors
How to write a copy constructor
C# Programming Guide
The C# type system
Finalizers
static
Why Do Initializers Run In The Opposite Order As Constructors? P art One   static Child() => maximumAge = 18; 
   // Remaining implementation of Child class.  
} 
public class Child : Person 
{ 
   private static int maximumAge;  
   public Child(string lastName, string firstName ) : base(lastName,  
firstName ) 
   { } 
   static Child() => maximumAge = 18; 
   // Remaining implementation of Child class.  
} 
In This Section
See alsoUsing Constructors (C# Programming
Guide)
Article •05/26/2023
When a class  or struct  is instantiated, its constructor is called. Constructors have the
same name as the class or struct, and they usually initialize the data members of the
new object.
In the following example, a class named Taxi is defined by using a simple constructor.
This class is then instantiated with the new operator. The Taxi constructor is invoked by
the new operator immediately after memory is allocated for the new object.
C#
A constructor that takes no parameters is called a paramet erless c onstr uctor.
Parameterless constructors are invoked whenever an object is instantiated by using the
new operator and no arguments are provided to new. C# 12 introduces primary
constr uctors. A primary constructor specifies parameters that must be provided to
initialize a new object. For more information, see Instance Constructors .
Unless the class is static , classes without constructors are given a public parameterless
constructor by the C# compiler in order to enable class instantiation. For more
information, see Static Classes and S tatic Class Members .public class Taxi 
{ 
    public bool IsInitialized;  
    public Taxi() 
    { 
        IsInitialized = true; 
    } 
} 
class TestTaxi  
{ 
    static void Main() 
    { 
        Taxi t = new Taxi();  
        Console.WriteLine(t.IsInitialized);  
    } 
} You can prevent a class from being instantiated by making the constructor private, as
follows:
C#
For more information, see Private Constructors .
Constructors for struct  types resemble class constructors. When a struct type is
instantiated with new, a constructor is invoked. When a struct is set to its default
value, the runtime initializes all memory in the struct to 0. Prior to C# 10, structs can't
contain an explicit parameterless constructor because one is provided automatically by
the compiler. For more information, see the Struct initialization and default values
section of the Structure types  article.
The following code uses the parameterless constructor for Int32 , so that you're assured
that the integer is initialized:
C#
The following code, however, causes a compiler error because it doesn't use new, and
because it tries to use an object that hasn't been initialized:
C#
Alternatively, objects based on structs (including all built-in numeric types) can be
initialized or assigned and then used as in the following example:
C#class NLog 
{ 
    // Private Constructor:  
    private NLog() { } 
    public static double e = Math.E;  //2.71828...  
} 
int i = new int(); 
Console.WriteLine(i);  
int i; 
Console.WriteLine(i);  
int a = 44;  // Initialize the value type...  
int b; Both classes and structs can define constructors that take parameters, including primary
constructors . Constructors that take parameters must be called through a new statement
or a base statement. Classes and structs can also define multiple constructors, and
neither is required to define a parameterless constructor. For example:
C#
This class can be created by using either of the following statements:
C#
A constructor can use the base keyword to call the constructor of a base class. For
example:
C#b = 33;      // Or assign it before using it.  
Console.WriteLine( "{0}, {1}" , a, b);  
public class Employee  
{ 
    public int Salary;  
    public Employee () { } 
    public Employee (int annualSalary ) 
    { 
        Salary = annualSalary;  
    } 
    public Employee (int weeklySalary, int numberOfWeeks ) 
    { 
        Salary = weeklySalary * numberOfWeeks;  
    } 
} 
Employee e1 = new Employee( 30000); 
Employee e2 = new Employee( 500, 52); 
public class Manager : Employee  
{ 
    public Manager(int annualSalary ) 
        : base(annualSalary ) 
    { 
        //Add further instructions here.  
    } 
} In this example, the constructor for the base class is called before the block for the
constructor is executed. The base keyword can be used with or without parameters. Any
parameters to the constructor can be used as parameters to base, or as part of an
expression. For more information, see base.
In a derived class, if a base-class constructor isn't called explicitly by using the base
keyword, the parameterless constructor, if there's one, is called implicitly. The following
constructor declarations are effectively the same:
C#
C#
If a base class doesn't offer a parameterless constructor, the derived class must make an
explicit call to a base constructor by using base.
A constructor can invoke another constructor in the same object by using the this
keyword. Like base, this can be used with or without parameters, and any parameters
in the constructor are available as parameters to this, or as part of an expression. For
example, the second constructor in the previous example can be rewritten using this:
C#
The use of the this keyword in the previous example causes this constructor to be
called:
C#public Manager(int initialData ) 
{ 
    //Add further instructions here.  
} 
public Manager(int initialData ) 
    : base() 
{ 
    //Add further instructions here.  
} 
public Employee (int weeklySalary, int numberOfWeeks ) 
    : this(weeklySalary * numberOfWeeks ) 
{ 
} Constructors can be marked as public , private , protected , internal , protected internal  or
private protected . These access modifiers define how users of the class can construct the
class. For more information, see Access Modifiers .
A constructor can be declared static by using the static  keyword. S tatic constructors are
called automatically, immediately before any static fields are accessed, and are used to
initialize static class members. For more information, see Static Constructors .
For more information, see Instance constructors  and Static constructors  in the C#
Language Specification . The language specification is the definitive source for C# syntax
and usage.
C# Programming Guide
The C# type system
Constructors
Finalizerspublic Employee (int annualSalary ) 
{ 
    Salary = annualSalary;  
} 
C# Language Specification
See alsoInstance co nstructors (C# programming
guide)
Article •11/14/2023
You declare an instance constructor to specify the code that is executed when you
create a new instance of a type with the new expression . To initialize a static  class or
static variables in a nonstatic class, you can define a static constructor .
As the following example shows, you can declare several instance constructors in one
type:
C#
In the preceding example, the first, parameterless, constructor calls the second
constructor with both arguments equal 0. To do that, use the this keyword.class Coords
{
    public Coords()
        : this(0, 0)
    {  }
    public Coords(int x, int y)
    {
        X = x;
        Y = y;
    }
    public int X { get; set; }
    public int Y { get; set; }
    public override  string ToString () => $"({X},{Y})";
}
class Example
{
    static void Main()
    {
        var p1 = new Coords();
        Console.WriteLine( $"Coords #1 at {p1}");
        // Output: Coords #1 at (0,0)
        var p2 = new Coords( 5, 3);
        Console.WriteLine( $"Coords #2 at {p2}");
        // Output: Coords #2 at (5,3)
    }
}When you declare an instance constructor in a derived class, you can call a constructor
of a base class. T o do that, use the base keyword, as the following example shows:
C#
abstract  class Shape
{
    public const double pi = Math.PI;
    protected  double x, y;
    public Shape(double x, double y)
    {
        this.x = x;
        this.y = y;
    }
    public abstract  double Area();
}
class Circle : Shape
{
    public Circle(double radius)
        : base(radius, 0)
    {  }
    public override  double Area() => pi * x * x;
}
class Cylinder  : Circle
{
    public Cylinder (double radius, double height)
        : base(radius)
    {
        y = height;
    }
    public override  double Area() => (2 * base.Area()) + ( 2 * pi * x * y);
}
class Example
{
    static void Main()
    {
        double radius = 2.5;
        double height = 3.0;
        var ring = new Circle(radius);
        Console.WriteLine( $"Area of the circle = {ring.Area():F2} ");
        // Output: Area of the circle = 19.63
        
        var tube = new Cylinder(radius, height);
        Console.WriteLine( $"Area of the cylinder = {tube.Area():F2} ");
        // Output: Area of the cylinder = 86.39If a class has no explicit instance constructors, C# provides a parameterless constructor
that you can use to instantiate an instance of that class, as the following example shows:
C#
That constructor initializes instance fields and properties according to the corresponding
initializers. If a field or property has no initializer, its value is set to the default value  of
the field's or property's type. If you declare at least one instance constructor in a class,
C# doesn't provide a parameterless constructor.
A structur e type always provides a parameterless constructor. The parameterless
constructor is either an implicit parameterless constructor that produces the default
value of a type or an explicitly declared parameterless constructor. For more
information, see the Struct initialization and default values  section of the Structure types
article.
Beginning in C# 12, you can declare a primary constr uctor in classes and structs. Y ou
place any parameters in parentheses following the type name:
C#    }
}
Parameterless constructors
public class Person
{
    public int age;
    public string name = "unknown" ;
}
class Example
{
    static void Main()
    {
        var person = new Person();
        Console.WriteLine( $"Name: {person.name} , Age: {person.age} ");
        // Output:  Name: unknown, Age: 0
    }
}
Primary constructorsThe parameters to a primary constructor are in scope in the entire body of the declaring
type. They can initialize properties or fields. They can be used as variables in methods or
local functions. They can be passed to a base constructor.
A primary constructor indicates that these parameters are necessary for any instance of
the type. Any explicitly written constructor must use the this(...) initializer syntax to
invoke the primary constructor. That ensures that the primary constructor parameters
are definitely assigned by all constructors. For any class type, including record class
types, the implicit parameterless constructor isn't emitted when a primary constructor is
present. For any struct type, including record struct types, the implicit parameterless
constructor is always emitted, and always initializes all fields, including primary
constructor parameters, to the 0-bit pattern. If you write an explicit parameterless
constructor, it must invoke the primary constructor. In that case, you can specify a
different value for the primary constructor parameters. The following code shows
examples of primary constructors.
C#
You can add attributes to the synthesized primary constructor method by specifying the
method: target on the attribute:
C#public class NamedItem (string name)
{
    public string Name => name;
}
// name isn't captured in Widget.
// width, height, and depth are captured as private fields
public class Widget(string name, int width, int height, int depth) : 
NamedItem (name)
{
    public Widget() : this("N/A", 1,1,1) {} // unnamed unit cube
    public int WidthInCM => width;
    public int HeightInCM => height;
    public int DepthInCM => depth;
    public int Volume => width * height * depth;
}
[method: MyAttribute ]
public class TaggedWidget (string name)
{If you don't specify the method target, the attribute is placed on the class rather than the
method.
In class and struct types, primary constructor parameters are available anywhere in
the body of the type. They can be used as member fields. When a primary constructor
parameter is used, the compiler captures the constructor parameter in a private field
with a compiler-generated name. If a primary constructor parameter isn't used in the
body of the type, no private field is captured. That rule prevents accidentally allocating
two copies of a primary constructor parameter that's passed to a base constructor.
If the type includes the record modifier, the compiler instead synthesizes a public
property with the same name as the primary constructor parameter. For record class
types, if a primary constructor parameter uses the same name as a base primary
constructor, that property is a public property of the base record class type. It isn't
duplicated in the derived record class type. These properties aren't generated for non-
record types.
C# programming guide
Classes, structs, and records
Constructors
Finalizers
base
this
Primary constructors feature spec   // details elided
}
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
 Provide product feedbackPrivate Constructors (C# Programming
Guide)
Article •01/12/2022
A private constructor is a special instance constructor. It is generally used in classes that
contain static members only. If a class has one or more private constructors and no
public constructors, other classes (except nested classes) cannot create instances of this
class. For example:
C#
The declaration of the empty constructor prevents the automatic generation of a
parameterless constructor. Note that if you do not use an access modifier with the
constructor it will still be private by default. However, the private  modifier is usually used
explicitly to make it clear that the class cannot be instantiated.
Private constructors are used to prevent creating instances of a class when there are no
instance fields or methods, such as the Math  class, or when a method is called to obtain
an instance of a class. If all the methods in the class are static, consider making the
complete class static. For more information see Static Classes and S tatic Class Members .
The following is an example of a class using a private constructor.
C#class NLog 
{ 
    // Private Constructor:  
    private NLog() { } 
    public static double e = Math.E;  //2.71828...  
} 
Example
public class Counter 
{ 
    private Counter() { } 
    public static int currentCount;  
    public static int IncrementCount () 
    { 
        return ++currentCount;  Notice that if you uncomment the following statement from the example, it will
generate an error because the constructor is inaccessible because of its protection level:
C#
C# Programming Guide
The C# type system
Constructors
Finalizers
private
public    } 
} 
class TestCounter  
{ 
    static void Main() 
    { 
        // If you uncomment the following statement, it will generate  
        // an error because the constructor is inaccessible:  
        // Counter aCounter = new Counter();   // Error  
        Counter.currentCount = 100; 
        Counter.IncrementCount();
        Console.WriteLine( "New count: {0}" , Counter.currentCount);  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
// Output: New count: 101  
// Counter aCounter = new Counter();   // Error  
See alsoStatic Constructors (C# Programming
Guide)
Article •10/24/2023
A static constructor is used to initialize any static  data, or to perform a particular action
that needs to be performed only once. It is called automatically before the first instance
is created or any static members are referenced. A static constructor will be called at
most once.
C#
There are several actions that are part of static initialization. Those actions take place in
the following order:
1. Static f ields ar e set to 0. This is typically done by the runtime.
2. Static f ield initializer s run. The static field initializers in the most derived type run.
3. Base type st atic f ield initializer s run. Static field initializers starting with the direct
base through each base type to System.Object .
4. Base static c onstr uctors run. Any static constructors, starting with Object.Object
through each base class to the direct base class.
5. The st atic c onstr uctor runs. The static constructor for the type runs.
A module initializer  can be an alternative to a static constructor. For more information,
see the specification for module initializers .
Static constructors have the following properties:
A static constructor doesn't take access modifiers or have parameters.class SimpleClass
{
    // Static variable that must be initialized at run time.
    static readonly  long baseline;
    // Static constructor is called at most one time, before any
    // instance constructor is invoked or member is accessed.
    static SimpleClass ()
    {
        baseline = DateTime.Now.Ticks;
    }
}
RemarksA class or struct can only have one static constructor.
Static constructors cannot be inherited or overloaded.
A static constructor cannot be called directly and is only meant to be called by the
common language runtime (CLR). It is invoked automatically.
The user has no control on when the static constructor is executed in the program.
A static constructor is called automatically. It initializes the class  before the first
instance is created or any static members declared in that class (not its base
classes) are referenced. A static constructor runs before an instance constructor. If
static field variable initializers are present in the class of the static constructor,
they're executed in the textual order in which they appear in the class declaration.
The initializers run immediately prior to the execution of the static constructor.
If you don't provide a static constructor to initialize static fields, all static fields are
initialized to their default value as listed in Default values of C# types .
If a static constructor throws an exception, the runtime doesn't invoke it a second
time, and the type will remain uninitialized for the lifetime of the application
domain. Most commonly, a TypeInitializationException  exception is thrown when a
static constructor is unable to instantiate a type or for an unhandled exception
occurring within a static constructor. For static constructors that aren't explicitly
defined in source code, troubleshooting may require inspection of the
intermediate language (IL) code.
The presence of a static constructor prevents the addition of the BeforeFieldInit
type attribute. This limits runtime optimization.
A field declared as static readonly may only be assigned as part of its declaration
or in a static constructor. When an explicit static constructor isn't required, initialize
static fields at declaration rather than through a static constructor for better
runtime optimization.
The runtime calls a static constructor no more than once in a single application
domain. That call is made in a locked region based on the specific type of the class.
No additional locking mechanisms are needed in the body of a static constructor.
To avoid the risk of deadlocks, don't block the current thread in static constructors
and initializers. For example, don't wait on tasks, threads, wait handles or events,
don't acquire locks, and don't execute blocking parallel operations such as parallel
loops, Parallel.Invoke and P arallel LINQ queries.
７ Note
Though not directly accessible, the presence of an explicit static constructor should
be documented to assist with troubleshooting initialization exceptions.A typical use of static constructors is when the class is using a log file and the
constructor is used to write entries to this file.
Static constructors are also useful when creating wrapper classes for unmanaged
code, when the constructor can call the LoadLibrary method.
Static constructors are also a convenient place to enforce run-time checks on the
type parameter that cannot be checked at compile time via type-parameter
constraints.
In this example, class Bus has a static constructor. When the first instance of Bus is
created ( bus1), the static constructor is invoked to initialize the class. The sample output
verifies that the static constructor runs only one time, even though two instances of Bus
are created, and that it runs before the instance constructor runs.
C#Usage
Example
public class Bus
{
    // Static variable used by all Bus instances.
    // Represents the time the first bus of the day starts its route.
    protected  static readonly  DateTime globalStartTime;
    // Property for the number of each bus.
    protected  int RouteNumber { get; set; }
    // Static constructor to initialize the static variable.
    // It is invoked before the first instance constructor is run.
    static Bus()
    {
        globalStartTime = DateTime.Now;
        // The following statement produces the first line of output,
        // and the line occurs only once.
        Console.WriteLine( "Static constructor sets global start time to  
{0}",
            globalStartTime.ToLongTimeString());
    }
    // Instance constructor.
    public Bus(int routeNum )
    {
        RouteNumber = routeNum;
        Console.WriteLine( "Bus #{0} is created." , RouteNumber);
    }    // Instance method.
    public void Drive()
    {
        TimeSpan elapsedTime = DateTime.Now - globalStartTime;
        // For demonstration purposes we treat milliseconds as minutes to  
simulate
        // actual bus times. Do not do this in your actual bus schedule  
program!
        Console.WriteLine( "{0} is starting its route {1:N2} minutes after  
global start time {2}." ,
                                this.RouteNumber,
                                elapsedTime.Milliseconds,
                                globalStartTime.ToShortTimeString());
    }
}
class TestBus
{
    static void Main()
    {
        // The creation of this instance activates the static constructor.
        Bus bus1 = new Bus(71);
        // Create a second bus.
        Bus bus2 = new Bus(72);
        // Send bus1 on its way.
        bus1.Drive();
        // Wait for bus2 to warm up.
        System.Threading.Thread.Sleep( 25);
        // Send bus2 on its way.
        bus2.Drive();
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Sample output:
    Static constructor sets global start time to 3:57:08 PM.
    Bus #71 is created.
    Bus #72 is created.
    71 is starting its route 6.00 minutes after global start time 3:57 PM.
    72 is starting its route 31.00 minutes after global start time 3:57 PM.
*/
C# language specificationFor more information, see the Static constructors  section of the C# language
specification .
C# Programming Guide
The C# type system
Constructors
Static Classes and S tatic Class Members
Finalizers
Constructor Design Guidelines
Security W arning - CA2121: S tatic constructors should be private
Module initializersSee also
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
 Provide product feedbackHow to write a copy constructor (C#
Programming Guide)
Article •05/26/2023
C# records  provide a copy constructor for objects, but for classes you have to write one
yourself.
In the following example, the Person class  defines a copy constructor that takes, as its
argument, an instance of Person. The values of the properties of the argument are
assigned to the properties of the new instance of Person. The code contains an
alternative copy constructor that sends the Name and Age properties of the instance that
you want to copy to the instance constructor of the class. The Person class is sealed, so
no derived types can be declared that could introduce errors by copying only the base
class.
C#） Impor tant
Writing copy constructors that work for all derived types in a class hierarchy can be
difficult. If your class isn't sealed, you should strongly consider creating a hierarchy
of record class types to use the compiler-synthesized copy constructor.
Example
public sealed class Person 
{ 
    // Copy constructor.  
    public Person(Person previousPerson ) 
    { 
        Name = previousPerson.Name;  
        Age = previousPerson.Age;
    } 
    //// Alternate copy constructor calls the instance constructor.  
    //public Person(Person previousPerson)  
    //    : this(previousPerson.Name, previousPerson.Age)  
    //{ 
    //} 
    // Instance constructor.  
    public Person(string name, int age) ICloneable
Records
C# Programming Guide
The C# type system    { 
        Name = name;  
        Age = age;  
    } 
    public int Age { get; set; } 
    public string Name { get; set; } 
    public string Details() 
    { 
        return Name + " is " + Age.ToString();  
    } 
} 
class TestPerson  
{ 
    static void Main() 
    { 
        // Create a Person object by using the instance constructor.  
        Person person1 = new Person( "George" , 40); 
        // Create another Person object, copying person1.  
        Person person2 = new Person(person1);  
        // Change each person's age.  
        person1.Age = 39; 
        person2.Age = 41; 
        // Change person2's name.
        person2.Name = "Charles" ; 
        // Show details to verify that the name and age fields are distinct.  
        Console.WriteLine(person1.Details());  
        Console.WriteLine(person2.Details());  
        // Keep the console window open in debug mode.  
        Console.WriteLine( "Press any key to exit." ); 
        Console.ReadKey();  
    } 
} 
// Output:  
// George is 39  
// Charles is 41  
See alsoConstructors
FinalizersFinalizers (C# Programming Guide)
Article •03/14/2023
Finalizers (historically referred to as destruct ors) are used to perform any necessary final
clean-up when a class instance is being collected by the garbage collector. In most
cases, you can avoid writing a finalizer by using the
System.Runtime.InteropServices.SafeHandle  or derived classes to wrap any unmanaged
handle.
Finalizers cannot be defined in structs. They are only used with classes.
A class can only have one finalizer.
Finalizers cannot be inherited or overloaded.
Finalizers cannot be called. They are invoked automatically.
A finalizer does not take modifiers or have parameters.
For example, the following is a declaration of a finalizer for the Car class.
C#
A finalizer can also be implemented as an expression body definition, as the following
example shows.
C#Remarks
class Car 
{ 
    ~Car()  // finalizer  
    { 
        // cleanup statements...  
    } 
} 
public class Destroyer  
{ 
   public override  string ToString () => GetType().Name;  
   ~Destroyer() => Console.WriteLine( $"The {ToString()}  finalizer is  
executing." ); 
} The finalizer implicitly calls Finalize  on the base class of the object. Therefore, a call to a
finalizer is implicitly translated to the following code:
C#
This design means that the Finalize method is called recursively for all instances in the
inheritance chain, from the most-derived to the least-derived.
The programmer has no control over when the finalizer is called; the garbage collector
decides when to call it. The garbage collector checks for objects that are no longer
being used by the application. If it considers an object eligible for finalization, it calls the
finalizer (if any) and reclaims the memory used to store the object. It's possible to force
garbage collection by calling Collect , but most of the time, this call should be avoided
because it may create performance issues.protected  override  void Finalize () 
{ 
    try 
    { 
        // Cleanup statements...  
    } 
    finally 
    { 
        base.Finalize();  
    } 
} 
７ Note
Empty finalizers should not be used. When a class contains a finalizer, an entry is
created in the Finalize queue. This queue is processed by the garbage collector.
When the GC processes the queue, it calls each finalizer. Unnecessary finalizers,
including empty finalizers, finalizers that only call the base class finalizer, or
finalizers that only call conditionally emitted methods, cause a needless loss of
performance.
７ Note
Whether or not finalizers are run as part of application termination is specific to
each implementation o f .NE T. When an application terminates, .NET Framework
makes every reasonable effort to call finalizers for objects that haven't yet been
garbage collected, unless such cleanup has been suppressed (by a call to the library
method GC.SuppressFinalize, for example). .NET 5 (including .NET Core) and laterIf you need to perform cleanup reliably when an application exits, register a handler for
the System.AppDomain.ProcessExit  event. That handler would ensure
IDisposable.Dispose()  (or, IAsyncDisposable.DisposeAsync() ) has been called for all
objects that require cleanup before application exit. Because you can't call Finalize
directly, and you can't guarantee the garbage collector calls all finalizers before exit, you
must use Dispose or DisposeAsync to ensure resources are freed.
In general, C# does not require as much memory management on the part of the
developer as languages that don't target a runtime with garbage collection. This is
because the .NET garbage collector implicitly manages the allocation and release of
memory for your objects. However, when your application encapsulates unmanaged
resources, such as windows, files, and network connections, you should use finalizers to
free those resources. When the object is eligible for finalization, the garbage collector
runs the Finalize method of the object.
If your application is using an expensive external resource, we also recommend that you
provide a way to explicitly release the resource before the garbage collector frees the
object. T o release the resource, implement a Dispose method from the IDisposable
interface that performs the necessary cleanup for the object. This can considerably
improve the performance of the application. Even with this explicit control over
resources, the finalizer becomes a safeguard to clean up resources if the call to the
Dispose method fails.
For more information about cleaning up resources, see the following articles:
Cleaning Up Unmanaged R esources
Implementing a Dispose Method
Implementing a DisposeAsync Method
using statementversions don't call finalizers as part of application termination. For more
information, see GitHub issue dotnet/csharpstandar d #291 .
Using finalizers to release resources
Explicit release of resources
ExampleThe following example creates three classes that make a chain of inheritance. The class
First is the base class, Second is derived from First, and Third is derived from
Second. All three have finalizers. In Main, an instance of the most-derived class is
created. The output from this code depends on which implementation of .NET the
application targets:
.NET Framework: The output shows that the finalizers for the three classes are
called automatically when the application terminates, in order from the most-
derived to the least-derived.
.NET 5 (including .NET Core) or a later version: There's no output, because this
implementation of .NET doesn't call finalizers when the application terminates.
C#
class First 
{ 
    ~First()  
    { 
        System.Diagnostics.Trace.WriteLine( "First's finalizer is called." ); 
    } 
} 
class Second : First 
{ 
    ~Second()  
    { 
        System.Diagnostics.Trace.WriteLine( "Second's finalizer is called." ); 
    } 
} 
class Third : Second 
{ 
    ~Third()  
    { 
        System.Diagnostics.Trace.WriteLine( "Third's finalizer is called." ); 
    } 
} 
/*  
Test with code like the following:  
    Third t = new Third();  
    t = null;  
When objects are finalized, the output would be:  
Third's finalizer is called.  
Second's finalizer is called.  
First's finalizer is called.  
*/ For more information, see the Finalizers  section of the C# Language Specification .
IDisposable
C# Programming Guide
Constructors
Garbage CollectionC# language specification
See alsoObject and Collection Initializers (C#
Programming Guide)
Article •07/14/2023
C# lets you instantiate an object or collection and perform member assignments in a
single statement.
Object initializers let you assign values to any accessible fields or properties of an object
at creation time without having to invoke a constructor followed by lines of assignment
statements. The object initializer syntax enables you to specify arguments for a
constructor or omit the arguments (and parentheses syntax). The following example
shows how to use an object initializer with a named type, Cat and how to invoke the
parameterless constructor. Note the use of auto-implemented properties in the Cat
class. For more information, see Auto-Implemented Properties .
C#
C#
The object initializers syntax allows you to create an instance, and after that it assigns
the newly created object, with its assigned properties, to the variable in the assignment.Object initia lizers
public class Cat
{
    // Auto-implemented properties.
    public int Age { get; set; }
    public string? Name { get; set; }
    public Cat()
    {
    }
    public Cat(string name)
    {
        this.Name = name;
    }
}
Cat cat = new Cat { Age = 10, Name = "Fluffy"  };
Cat sameCat = new Cat("Fluffy" ){ Age = 10 };Object initializers can set indexers, in addition to assigning fields and properties.
Consider this basic Matrix class:
C#
You could initialize the identity matrix with the following code:
C#
Any accessible indexer that contains an accessible setter can be used as one of the
expressions in an object initializer, regardless of the number or types of arguments. The
index arguments form the left side of the assignment, and the value is the right side of
the expression. For example, these are all valid if IndexersExample has the appropriate
indexers:
C#public class Matrix
{
    private double[,] storage = new double[3, 3];
    public double this[int row, int column]
    {
        // The embedded array will throw out of range exceptions as  
appropriate.
        get { return storage[row, column]; }
        set { storage[row, column] = value; }
    }
}
var identity = new Matrix
{
    [0, 0] = 1.0,
    [0, 1] = 0.0,
    [0, 2] = 0.0,
    [1, 0] = 0.0,
    [1, 1] = 1.0,
    [1, 2] = 0.0,
    [2, 0] = 0.0,
    [2, 1] = 0.0,
    [2, 2] = 1.0,
};
var thing = new IndexersExample
{
    name = "object one" ,
    [1] = '1',For the preceding code to compile, the IndexersExample type must have the following
members:
C#
Although object initializers can be used in any context, they are especially useful in LINQ
query expressions. Query expressions make frequent use of anonymous types , which
can only be initialized by using an object initializer, as shown in the following
declaration.
C#
Anonymous types enable the select clause in a LINQ query expression to transform
objects of the original sequence into objects whose value and shape may differ from the
original. This is useful if you want to store only a part of the information from each
object in a sequence. In the following example, assume that a product object ( p)
contains many fields and methods, and that you are only interested in creating a
sequence of objects that contain the product name and the unit price.
C#
When this query is executed, the productInfos variable will contain a sequence of
objects that can be accessed in a foreach statement as shown in this example:    [2] = '4',
    [3] = '9',
    Size = Math.PI,
    ['C',4] = "Middle C"
}
public string name;
public double Size { set { ... }; }
public char this[int i] { set { ... }; }
public string this[char c, int i] {  set { ... }; }
Object Initializers with anonymous types
var pet = new { Age = 10, Name = "Fluffy"  };  
var productInfos =
    from p in products
    select new { p.ProductName, p.UnitPrice };C#
Each object in the new anonymous type has two public properties that receive the same
names as the properties or fields in the original object. Y ou can also rename a field when
you are creating an anonymous type; the following example renames the UnitPrice
field to Price.
C#
You use the required keyword to force callers to set the value of a property or field
using an object initializer. R equired properties don't need to be set as constructor
parameters. The compiler ensures all callers initialize those values.
C#
It's a typical practice to guarantee that your object is properly initialized, especially when
you have multiple fields or properties to manage and don't want to include them all in
the constructor.foreach(var p in productInfos){...}  
select new {p.ProductName, Price = p.UnitPrice};  
Object Initializers with the required modifier
public class Pet
{
    public required int Age;
    public string Name;
}
// `Age` field is necessary to be initialized.
// You don't need to initialize `Name` property
var pet = new Pet() { Age = 10};
// Compiler error:
// Error CS9035 Required member 'Pet.Age' must be set in the object  
initializer or attribute constructor.
// var pet = new Pet();
Object Initializers with the init accessorMaking sure no one changes the designed object could be limited by using an init
accessor. It helps to restrict the setting of the property value.
C#
Required init-only properties support immutable structures while allowing natural syntax
for users of the type.
Collection initializers let you specify one or more element initializers when you initialize
a collection type that implements IEnumerable  and has Add with the appropriate
signature as an instance method or an extension method. The element initializers can be
a simple value, an expression, or an object initializer. By using a collection initializer, you
do not have to specify multiple calls; the compiler adds the calls automatically.
The following example shows two simple collection initializers:
C#
The following collection initializer uses object initializers to initialize objects of the Cat
class defined in a previous example. Note that the individual object initializers arepublic class Person
{
    public string FirstName { get; set; }
    public string LastName { get; init; }
}
// The `LastName` property can be set only during initialization. It CAN'T  
be modified afterwards.
// The `FirstName` property can be modified after initialization.
var pet = new Person() { FirstName = "Joe", LastName = "Doe"};
// You can assign the FirstName property to a different value.
pet.FirstName = "Jane";
// Compiler error:
// Error CS8852  Init - only property or indexer 'Person.LastName' can only  
be assigned in an object initializer,
//               or on 'this' or 'base' in an instance constructor or an  
'init' accessor.
// pet.LastName = "Kowalski";
Collection initia lizers
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };  enclosed in braces and separated by commas.
C#
You can specify null as an element in a collection initializer if the collection's Add
method allows it.
C#
You can specify indexed elements if the collection supports read / write indexing.
C#
The preceding sample generates code that calls the Item[TK ey] to set the values. Y ou
could also initialize dictionaries and other associative containers using the following
syntax. Notice that instead of indexer syntax, with parentheses and an assignment, it
uses an object with multiple values:
C#List<Cat> cats = new List<Cat>
{
    new Cat{ Name = "Sylvester" , Age=8 },
    new Cat{ Name = "Whiskers" , Age=2 },
    new Cat{ Name = "Sasha", Age=14 }
};
List<Cat?> moreCats = new List<Cat?>
{
    new Cat{ Name = "Furrytail" , Age=5 },
    new Cat{ Name = "Peaches" , Age=4 },
    null
};
var numbers = new Dictionary< int, string>
{
    [7] = "seven",
    [9] = "nine",
    [13] = "thirteen"
};
var moreNumbers = new Dictionary< int, string>
{
    {19, "nineteen"  },
    {23, "twenty-three"  },
    {42, "forty-two"  }
};This initializer example calls Add(TK ey, TValue)  to add the three items into the dictionary.
These two different ways to initialize associative collections have slightly different
behavior because of the method calls the compiler generates. Both variants work with
the Dictionary class. Other types may only support one or the other based on their
public API.
Some classes may have collection properties where the property is read-only, like the
Cats property of CatOwner in the following case:
C#
You will not be able to use collection initializer syntax discussed so far since the property
cannot be assigned a new list:
C#
However, new entries can be added to Cats nonetheless using the initialization syntax
by omitting the list creation ( new List<Cat>), as shown next:
C#Object Initializers with collection read-only
property initia lization
public class CatOwner
{
    public IList<Cat> Cats { get; } = new List<Cat>();
}
CatOwner owner = new CatOwner
{
    Cats = new List<Cat>
    {
        new Cat{ Name = "Sylvester" , Age=8 },
        new Cat{ Name = "Whiskers" , Age=2 },
        new Cat{ Name = "Sasha", Age=14 }
    }
};
CatOwner owner = new CatOwner
{
    Cats =
    {
        new Cat{ Name = "Sylvester" , Age=8 },
        new Cat{ Name = "Whiskers" , Age=2 },The set of entries to be added simply appear surrounded by braces. The above is
identical to writing:
C#
The following example combines the concepts of object and collection initializers.
C#        new Cat{ Name = "Sasha", Age=14 }
    }
};
CatOwner owner = new CatOwner();
owner.Cats.Add( new Cat{ Name = "Sylvester" , Age=8 });
owner.Cats.Add( new Cat{ Name = "Whiskers" , Age=2 });
owner.Cats.Add( new Cat{ Name = "Sasha", Age=14 });
Examples
public class InitializationSample
{
    public class Cat
    {
        // Auto-implemented properties.
        public int Age { get; set; }
        public string? Name { get; set; }
        public Cat() { }
        public Cat(string name)
        {
            Name = name;
        }
    }
    public static void Main()
    {
        Cat cat = new Cat { Age = 10, Name = "Fluffy"  };
        Cat sameCat = new Cat("Fluffy" ){ Age = 10 };
        List<Cat> cats = new List<Cat>
        {
            new Cat { Name = "Sylvester" , Age = 8 },
            new Cat { Name = "Whiskers" , Age = 2 },
            new Cat { Name = "Sasha", Age = 14 }
        };
        List<Cat?> moreCats = new List<Cat?>
        {The following example shows an object that implements IEnumerable  and contains an
Add method with multiple parameters, It uses a collection initializer with multiple
elements per item in the list that correspond to the signature of the Add method.
C#            new Cat { Name = "Furrytail" , Age = 5 },
            new Cat { Name = "Peaches" , Age = 4 },
            null
        };
        // Display results.
        System.Console.WriteLine(cat.Name);
        foreach (Cat c in cats)
            System.Console.WriteLine(c.Name);
        foreach (Cat? c in moreCats)
            if (c != null)
                System.Console.WriteLine(c.Name);
            else
                System.Console.WriteLine( "List element has null value." );
    }
    // Output:
    //Fluffy
    //Sylvester
    //Whiskers
    //Sasha
    //Furrytail
    //Peaches
    //List element has null value.
}
    public class FullExample
    {
        class FormattedAddresses  : IEnumerable <string>
        {
            private List<string> internalList = new List<string>();
            public IEnumerator< string> GetEnumerator () => 
internalList.GetEnumerator();
            System.Collections.IEnumerator  
System.Collections.IEnumerable.GetEnumerator() =>  
internalList.GetEnumerator();
            public void Add(string firstname, string lastname,
                string street, string city,
                string state, string zipcode ) => internalList.Add(
                $@"{firstname}  {lastname}
{street}
{city}, {state} {zipcode} "
                );Add methods can use the params keyword to take a variable number of arguments, as
shown in the following example. This example also demonstrates the custom
implementation of an indexer to initialize a collection using indexes.
C#        }
        public static void Main()
        {
            FormattedAddresses addresses = new FormattedAddresses()
            {
                {"John", "Doe", "123 Street" , "Topeka" , "KS", "00000" },
                {"Jane", "Smith", "456 Street" , "Topeka" , "KS", "00000" }
            };
            Console.WriteLine( "Address Entries:" );
            foreach (string addressEntry in addresses)
            {
                Console.WriteLine( "\r\n" + addressEntry);
            }
        }
        /*
         * Prints:
            Address Entries:
            John Doe
            123 Street
            Topeka, KS 00000
            Jane Smith
            456 Street
            Topeka, KS 00000
         */
    }
public class DictionaryExample
{
    class RudimentaryMultiValuedDictionary <TKey, TValue> : 
IEnumerable <KeyValuePair <TKey, List<TValue>>> where TKey : notnull
    {
        private Dictionary<TKey, List<TValue>> internalDictionary = new 
Dictionary<TKey, List<TValue>>();
        public IEnumerator<KeyValuePair<TKey, List<TValue>>> GetEnumerator()  
=> internalDictionary.GetEnumerator();
        System.Collections.IEnumerator  
System.Collections.IEnumerable.GetEnumerator() =>  internalDictionary.GetEnumerator();
        public List<TValue> this[TKey key]
        {
            get => internalDictionary[key];
            set => Add(key, value);
        }
        public void Add(TKey key, params TValue[] values ) => Add(key,  
(IEnumerable<TValue>)values);
        public void Add(TKey key, IEnumerable<TValue> values )
        {
            if (!internalDictionary.TryGetValue(key, out List<TValue>?  
storedValues))
                internalDictionary.Add(key, storedValues = new List<TValue>
());
            storedValues.AddRange(values);
        }
    }
    public static void Main()
    {
        RudimentaryMultiValuedDictionary< string, string> 
rudimentaryMultiValuedDictionary1
            = new RudimentaryMultiValuedDictionary< string, string>()
            {
                {"Group1" , "Bob", "John", "Mary" },
                {"Group2" , "Eric", "Emily", "Debbie" , "Jesse" }
            };
        RudimentaryMultiValuedDictionary< string, string> 
rudimentaryMultiValuedDictionary2
            = new RudimentaryMultiValuedDictionary< string, string>()
            {
                ["Group1" ] = new List<string>() { "Bob", "John", "Mary" },
                ["Group2" ] = new List<string>() { "Eric", "Emily", "Debbie" , 
"Jesse" }
            };
        RudimentaryMultiValuedDictionary< string, string> 
rudimentaryMultiValuedDictionary3
            = new RudimentaryMultiValuedDictionary< string, string>()
            {
                {"Group1" , new string []{ "Bob", "John", "Mary" } },
                { "Group2" , new string[]{ "Eric", "Emily", "Debbie" , "Jesse" 
} }
            };
        Console.WriteLine( "Using first multi-valued dictionary created with  
a collection initializer:" );
        foreach (KeyValuePair< string, List<string>> group in 
rudimentaryMultiValuedDictionary1)
        {
            Console.WriteLine( $"\r\nMembers of group {group.Key}: ");            foreach (string member in group.Value)
            {
                Console.WriteLine(member);
            }
        }
        Console.WriteLine( "\r\nUsing second multi-valued dictionary created  
with a collection initializer using indexing:" );
        foreach (KeyValuePair< string, List<string>> group in 
rudimentaryMultiValuedDictionary2)
        {
            Console.WriteLine( $"\r\nMembers of group {group.Key}: ");
            foreach (string member in group.Value)
            {
                Console.WriteLine(member);
            }
        }
        Console.WriteLine( "\r\nUsing third multi-valued dictionary created  
with a collection initializer using indexing:" );
        foreach (KeyValuePair< string, List<string>> group in 
rudimentaryMultiValuedDictionary3)
        {
            Console.WriteLine( $"\r\nMembers of group {group.Key}: ");
            foreach (string member in group.Value)
            {
                Console.WriteLine(member);
            }
        }
    }
    /*
     * Prints:
        Using first multi-valued dictionary created with a collection  
initializer:
        Members of group Group1:
        Bob
        John
        Mary
        Members of group Group2:
        Eric
        Emily
        Debbie
        Jesse
        Using second multi-valued dictionary created with a collection  
initializer using indexing:Use object initializers (style rule IDE0017)
Use collection initializers (style rule IDE0028)
C# Programming Guide
LINQ in C#
Anonymous T ypes        Members of group Group1:
        Bob
        John
        Mary
        Members of group Group2:
        Eric
        Emily
        Debbie
        Jesse
        Using third multi-valued dictionary created with a collection  
initializer using indexing:
        Members of group Group1:
        Bob
        John
        Mary
        Members of group Group2:
        Eric
        Emily
        Debbie
        Jesse
     */
}
See alsoHow to initialize objects by using an
object initializer (C# Programming
Guide)
Article •09/15/2021
You can use object initializers to initialize type objects in a declarative manner without
explicitly invoking a constructor for the type.
The following examples show how to use object initializers with named objects. The
compiler processes object initializers by first accessing the parameterless instance
constructor and then processing the member initializations. Therefore, if the
parameterless constructor is declared as private in the class, object initializers that
require public access will fail.
You must use an object initializer if you're defining an anonymous type. For more
information, see How to return subsets of element properties in a query .
The following example shows how to initialize a new StudentName type by using object
initializers. This example sets properties in the StudentName type:
C#Example
public class HowToObjectInitializers  
{ 
    public static void Main() 
    { 
        // Declare a StudentName by using the constructor that has two  
parameters.  
        StudentName student1 = new StudentName( "Craig", "Playstead" ); 
        // Make the same declaration by using an object initializer and  
sending 
        // arguments for the first and last names. The parameterless  
constructor is  
        // invoked in processing this declaration, not the constructor that  
has 
        // two parameters.  
        StudentName student2 = new StudentName  
        {  
            FirstName = "Craig", 
            LastName = "Playstead"  
        };          // Declare a StudentName by using an object initializer and sending  
        // an argument for only the ID property. No corresponding  
constructor is  
        // necessary. Only the parameterless constructor is used to process  
object 
        // initializers.  
        StudentName student3 = new StudentName  
        {  
            ID = 183 
        };  
        // Declare a StudentName by using an object initializer and sending  
        // arguments for all three properties. No corresponding constructor  
is 
        // defined in the class.  
        StudentName student4 = new StudentName  
        {  
            FirstName = "Craig", 
            LastName = "Playstead" , 
            ID = 116 
        };  
        Console.WriteLine(student1.ToString());  
        Console.WriteLine(student2.ToString());  
        Console.WriteLine(student3.ToString());  
        Console.WriteLine(student4.ToString());  
    } 
    // Output:  
    // Craig  0  
    // Craig  0  
    //   183  
    // Craig  116  
    public class StudentName  
    { 
        // This constructor has no parameters. The parameterless constructor  
        // is invoked in the processing of object initializers.  
        // You can test this by changing the access modifier from public to  
        // private. The declarations in Main that use object initializers  
will 
        // fail.  
        public StudentName () { } 
        // The following constructor has parameters for two of the three  
        // properties.  
        public StudentName (string first, string last) 
        {  
            FirstName = first;  
            LastName = last;  
        }  
        // Properties.  
        public string? FirstName { get; set; } 
        public string? LastName { get; set; } Object initializers can be used to set indexers in an object. The following example
defines a BaseballTeam class that uses an indexer to get and set players at different
positions. The initializer can assign players, based on the abbreviation for the position,
or the number used for each position baseball scorecards:
C#        public int ID { get; set; } 
        public override  string ToString () => FirstName + "  " + ID; 
    } 
} 
public class HowToIndexInitializer  
{ 
    public class BaseballTeam  
    { 
        private string[] players = new string[9]; 
        private readonly  List<string> positionAbbreviations = new 
List<string> 
        {  
            "P", "C", "1B", "2B", "3B", "SS", "LF", "CF", "RF" 
        };  
        public string this[int position]  
        {  
            // Baseball positions are 1 - 9.  
            get { return players[position -1]; } 
            set { players[position -1] = value; } 
        }  
        public string this[string position]  
        {  
            get { return players[positionAbbreviations.IndexOf(position)]; }  
            set { players[positionAbbreviations.IndexOf(position)] = value; 
} 
        }  
    } 
    public static void Main() 
    { 
        var team = new BaseballTeam  
        {  
            [ "RF"] = "Mookie Betts" , 
            [ 4] = "Jose Altuve" , 
            [ "CF"] = "Mike Trout"  
        };  
        Console.WriteLine(team[ "2B"]); 
    } 
} C# Programming Guide
Object and Collection InitializersSee alsoHow to initialize a dictionary with a
collection initializer (C# Programming
Guide)
Article •06/27/2023
A Dictionary<TK ey,TValue>  contains a collection of key/value pairs. Its Add method
takes two parameters, one for the key and one for the value. One way to initialize a
Dictionary<TK ey,TValue> , or any collection whose Add method takes multiple
parameters, is to enclose each set of parameters in braces as shown in the following
example. Another option is to use an index initializer, also shown in the following
example.
In the following code example, a Dictionary<TK ey,TValue>  is initialized with instances of
type StudentName. The first initialization uses the Add method with two arguments. The
compiler generates a call to Add for each of the pairs of int keys and StudentName
values. The second uses a public read / write indexer method of the Dictionary class:
C#７ Note
The major difference between these two ways of initializing the collection is that in
case of having duplicated keys, for example:
C#
Add method will throw ArgumentEx ception : 'An item with the same key has
already been added. Key: 111', while the second part of example, the public read /
write indexer method, will quietly overwrite the already existing entry with the same
key.{ 111, new StudentName { FirstName= "Sachin" , LastName= "Karnik" , ID=211 
} }, 
{ 111, new StudentName { FirstName= "Dina", LastName= "Salimzianova" , 
ID=317 } },  
ExampleNote the two pairs of braces in each element of the collection in the first declaration.
The innermost braces enclose the object initializer for the StudentName, and the
outermost braces enclose the initializer for the key/value pair that will be added to the
students Dictionary<TK ey,TValue> . Finally, the whole collection initializer for the
dictionary is enclosed in braces. In the second initialization, the left side of thepublic class HowToDictionaryInitializer  
{ 
    class StudentName  
    { 
        public string? FirstName { get; set; } 
        public string? LastName { get; set; } 
        public int ID { get; set; } 
    } 
    public static void Main() 
    { 
        var students = new Dictionary< int, StudentName>()  
        {  
            { 111, new StudentName { FirstName= "Sachin" , LastName= "Karnik" , 
ID=211 } }, 
            { 112, new StudentName { FirstName= "Dina", 
LastName= "Salimzianova" , ID=317 } }, 
            { 113, new StudentName { FirstName= "Andy", LastName= "Ruth", 
ID=198 } } 
        };  
        foreach(var index in Enumerable.Range( 111, 3)) 
        {  
            Console.WriteLine( $"Student {index} is 
{students[index].FirstName}  {students[index].LastName} "); 
        }  
        Console.WriteLine();   
        var students2 = new Dictionary< int, StudentName>()  
        {  
            [ 111] = new StudentName { FirstName= "Sachin" , LastName= "Karnik" , 
ID=211 }, 
            [ 112] = new StudentName { FirstName= "Dina", 
LastName= "Salimzianova" , ID=317 } , 
            [ 113] = new StudentName { FirstName= "Andy", LastName= "Ruth", 
ID=198 } 
        };  
        foreach (var index in Enumerable.Range( 111, 3)) 
        {  
            Console.WriteLine( $"Student {index} is 
{students2[index].FirstName}  {students2[index].LastName} "); 
        }  
    } 
} assignment is the key and the right side is the value, using an object initializer for
StudentName.
C# Programming Guide
Object and Collection InitializersSee alsoNested Types (C# Programming Guide)
Article •10/27/2021
A type defined within a class , struct , or interface  is called a nested type. For example
C#
Regardless of whether the outer type is a class, interface, or struct, nested types default
to private ; they are accessible only from their containing type. In the previous example,
the Nested class is inaccessible to external types.
You can also specify an access modifier  to define the accessibility of a nested type, as
follows:
Nested types of a class  can be public , protected , internal , protected internal ,
private  or private protected .
However, defining a protected, protected internal or private protected nested
class inside a sealed class  generates compiler warning CS0628 , "new protected
member declared in sealed class."
Also be aware that making a nested type externally visible violates the code quality
rule CA1034  "Nested types should not be visible".
Nested types of a struct  can be public , internal , or private .
The following example makes the Nested class public:
C#public class Container  
{ 
    class Nested 
    { 
        Nested() { }  
    } 
} 
public class Container  
{ 
    public class Nested 
    { 
        Nested() { }  
    } 
} The nested, or inner, type can access the containing, or outer, type. T o access the
containing type, pass it as an argument to the constructor of the nested type. For
example:
C#
A nested type has access to all of the members that are accessible to its containing type.
It can access private and protected members of the containing type, including any
inherited protected members.
In the previous declaration, the full name of class Nested is Container.Nested. This is the
name used to create a new instance of the nested class, as follows:
C#
C# Programming Guide
The C# type system
Access Modifiers
Constructors
CA1034 rulepublic class Container  
{ 
    public class Nested 
    { 
        private Container? parent;  
        public Nested() 
        {  
        }  
        public Nested(Container parent ) 
        {  
            this.parent = parent;  
        }  
    } 
} 
Container.Nested nest = new Container.Nested();  
See alsoPartial Classes and Methods (C#
Programming Guide)
Article •04/12/2023
It is possible to split the definition of a class , a struct , an interface  or a method over two
or more source files. Each source file contains a section of the type or method definition,
and all parts are combined when the application is compiled.
There are several situations when splitting a class definition is desirable:
When working on large projects, spreading a class over separate files enables
multiple programmers to work on it at the same time.
When working with automatically generated source, code can be added to the
class without having to recreate the source file. Visual S tudio uses this approach
when it creates Windows Forms, W eb service wrapper code, and so on. Y ou can
create code that uses these classes without having to modify the file created by
Visual S tudio.
When using source generators  to generate additional functionality in a class.
To split a class definition, use the partial  keyword modifier, as shown here:
C#
The partial keyword indicates that other parts of the class, struct, or interface can be
defined in the namespace. All the parts must use the partial keyword. All the partsPartial Classes
public partial class Employee
{
    public void DoWork()
    {
    }
}
public partial class Employee
{
    public void GoToLunch ()
    {
    }
}must be available at compile time to form the final type. All the parts must have the
same accessibility, such as public, private, and so on.
If any part is declared abstract, then the whole type is considered abstract. If any part is
declared sealed, then the whole type is considered sealed. If any part declares a base
type, then the whole type inherits that class.
All the parts that specify a base class must agree, but parts that omit a base class still
inherit the base type. P arts can specify different base interfaces, and the final type
implements all the interfaces listed by all the partial declarations. Any class, struct, or
interface members declared in a partial definition are available to all the other parts. The
final type is the combination of all the parts at compile time.
The following example shows that nested types can be partial, even if the type they are
nested within is not partial itself.
C#
At compile time, attributes of partial-type definitions are merged. For example, consider
the following declarations:
C#７ Note
The partial modifier is not available on delegate or enumeration declarations.
class Container
{
    partial class Nested
    {
        void Test() { }
    }
    partial class Nested
    {
        void Test2() { }
    }
}
[SerializableAttribute ]
partial class Moon { }
[ObsoleteAttribute ]
partial class Moon { }They are equivalent to the following declarations:
C#
The following are merged from all the partial-type definitions:
XML comments
interfaces
generic-type parameter attributes
class attributes
members
For example, consider the following declarations:
C#
They are equivalent to the following declarations:
C#
There are several rules to follow when you are working with partial class definitions:
All partial-type definitions meant to be parts of the same type must be modified
with partial. For example, the following class declarations generate an error:
C#
The partial modifier can only appear immediately before the keywords class,
struct, or interface.[SerializableAttribute ]
[ObsoleteAttribute ]
class Moon { }
partial class Earth : Planet, IRotate { }
partial class Earth : IRevolve  { }
class Earth : Planet, IRotate, IRevolve  { }
Restrictions
public partial class A { }
//public class A { }  // Error, must also be marked partialNested partial types are allowed in partial-type definitions as illustrated in the
following example:
C#
All partial-type definitions meant to be parts of the same type must be defined in
the same assembly and the same module (.exe or .dll file). P artial definitions cannot
span multiple modules.
The class name and generic-type parameters must match on all partial-type
definitions. Generic types can be partial. Each partial declaration must use the
same parameter names in the same order.
The following keywords on a partial-type definition are optional, but if present on
one partial-type definition, cannot conflict with the keywords specified on another
partial definition for the same type:
public
private
protected
internal
abstract
sealed
base class
new modifier (nested parts)
generic constraints
For more information, see Constraints on T ype P arameters .
In the following example, the fields and the constructor of the class, Coords, are
declared in one partial class definition, and the member, PrintCoords, is declared in
another partial class definition.
C#partial class ClassWithNestedClass
{
    partial class NestedClass  { }
}
partial class ClassWithNestedClass
{
    partial class NestedClass  { }
}
ExamplesThe following example shows that you can also develop partial structs and interfaces.
C#public partial class Coords
{
    private int x;
    private int y;
    public Coords(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
public partial class Coords
{
    public void PrintCoords ()
    {
        Console.WriteLine( "Coords: {0},{1}" , x, y);
    }
}
class TestCoords
{
    static void Main()
    {
        Coords myCoords = new Coords( 10, 15);
        myCoords.PrintCoords();
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
// Output: Coords: 10,15
partial interface  ITest
{
    void Interface_Test ();
}
partial interface  ITest
{
    void Interface_Test2 ();
}
partial struct S1
{
    void Struct_Test () { }
}A partial class or struct may contain a partial method. One part of the class contains the
signature of the method. An implementation can be defined in the same part or another
part. If the implementation is not supplied, then the method and all calls to the method
are removed at compile time. Implementation may be required depending on method
signature. A partial method isn't required to have an implementation in the following
cases:
It doesn't have any accessibility modifiers (including the default private ).
It returns void.
It doesn't have any out parameters.
It doesn't have any of the following modifiers virtual , override , sealed , new, or
extern .
Any method that doesn't conform to all those restrictions (for example, public virtual
partial void method), must provide an implementation. That implementation may be
supplied by a source gener ator.
Partial methods enable the implementer of one part of a class to declare a method. The
implementer of another part of the class can define that method. There are two
scenarios where this is useful: templates that generate boilerplate code, and source
generators.
Templat e code : The template reserves a method name and signature so that
generated code can call the method. These methods follow the restrictions that
enable a developer to decide whether to implement the method. If the method is
not implemented, then the compiler removes the method signature and all calls to
the method. The calls to the method, including any results that would occur from
evaluation of arguments in the calls, have no effect at run time. Therefore, any
code in the partial class can freely use a partial method, even if the implementation
is not supplied. No compile-time or run-time errors will result if the method is
called but not implemented.
Sour ce generat ors: Source generators provide an implementation for methods.
The human developer can add the method declaration (often with attributes read
by the source generator). The developer can write code that calls these methods.partial struct S1
{
    void Struct_Test2 () { }
}
Partial MethodsThe source generator runs during compilation and provides the implementation. In
this scenario, the restrictions for partial methods that may not be implemented
often aren't followed.
C#
Partial method declarations must begin with the contextual keyword partial .
Partial method signatures in both parts of the partial type must match.
Partial methods can have static  and unsafe  modifiers.
Partial methods can be generic. Constraints are put on the defining partial method
declaration, and may optionally be repeated on the implementing one. P arameter
and type parameter names do not have to be the same in the implementing
declaration as in the defining one.
You can make a delegate  to a partial method that has been defined and
implemented, but not to a partial method that has only been defined.
For more information, see Partial types  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
C# Programming Guide
Classes
Structure types
Interfaces
partial (T ype)// Definition in file1.cs
partial void OnNameChanged ();
// Implementation in file2.cs
partial void OnNameChanged ()
{
  // method body
}
C# Language Specification
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
 Provide product feedbackHow to return subsets of element
properties in a query (C# Programming
Guide)
Article •09/15/2021
Use an anonymous type in a query expression when both of these conditions apply:
You want to return only some of the properties of each source element.
You do not have to store the query results outside the scope of the method in
which the query is executed.
If you only want to return one property or field from each source element, then you can
just use the dot operator in the select clause. For example, to return only the ID of
each student, write the select clause as follows:
C#
The following example shows how to use an anonymous type to return only a subset of
the properties of each source element that matches the specified condition.
C#select student.ID;   
Example
private static void QueryByScore () 
{ 
    // Create the query. var is required because  
    // the query produces a sequence of anonymous types.  
    var queryHighScores =  
        from student in students  
        where student.ExamScores[ 0] > 95 
        select new { student.FirstName, student.LastName };  
    // Execute the query.  
    foreach (var obj in queryHighScores)  
    { 
        // The anonymous type's properties were not named. Therefore  
        // they have the same names as the Student properties.  
        Console.WriteLine(obj.FirstName + ", " + obj.LastName);  
    } 
} Note that the anonymous type uses the source element's names for its properties if no
names are specified. T o give new names to the properties in the anonymous type, write
the select statement as follows:
C#
If you try this in the previous example, then the Console.WriteLine statement must also
change:
C#
To run this code, copy and paste the class into a C# console application with a using
directive for S ystem.Linq.
C# Programming Guide
Anonymous T ypes
LINQ in C#/* Output:  
Adams, Terry  
Fakhouri, Fadi  
Garcia, Cesar  
Omelchenko, Svetlana  
Zabokritski, Eugene  
*/ 
select new { First = student.FirstName, Last = student.LastName };   
Console.WriteLine(student.First + " " + student.Last);   
Compiling the Code
See alsoExplicit Interface Implementation (C#
Programming Guide)
Article •09/29/2022
If a class  implements two interfaces that contain a member with the same signature,
then implementing that member on the class will cause both interfaces to use that
member as their implementation. In the following example, all the calls to Paint invoke
the same method. This first sample defines the types:
C#
The following sample calls the methods:
C#public interface  IControl  
{ 
    void Paint(); 
} 
public interface  ISurface  
{ 
    void Paint(); 
} 
public class SampleClass  : IControl , ISurface  
{ 
    // Both ISurface.Paint and IControl.Paint call this method.  
    public void Paint() 
    { 
        Console.WriteLine( "Paint method in SampleClass" ); 
    } 
} 
SampleClass sample = new SampleClass();  
IControl control = sample;  
ISurface surface = sample;  
// The following lines all call the same method.  
sample.Paint();  
control.Paint();  
surface.Paint();  
// Output:  
// Paint method in SampleClass  
// Paint method in SampleClass  
// Paint method in SampleClass  But you might not want the same implementation to be called for both interfaces. T o
call a different implementation depending on which interface is in use, you can
implement an interface member explicitly. An explicit interface implementation is a class
member that is only called through the specified interface. Name the class member by
prefixing it with the name of the interface and a period. For example:
C#
The class member IControl.Paint is only available through the IControl interface, and
ISurface.Paint is only available through ISurface. Both method implementations are
separate, and neither are available directly on the class. For example:
C#
Explicit implementation is also used to resolve cases where two interfaces each declare
different members of the same name such as a property and a method. T o implement
both interfaces, a class has to use explicit implementation either for the property P, or
the method P, or both, to avoid a compiler error. For example:
C#public class SampleClass  : IControl , ISurface  
{ 
    void IControl.Paint()  
    { 
        System.Console.WriteLine( "IControl.Paint" ); 
    } 
    void ISurface.Paint()  
    { 
        System.Console.WriteLine( "ISurface.Paint" ); 
    } 
} 
SampleClass sample = new SampleClass();  
IControl control = sample;  
ISurface surface = sample;  
// The following lines all call the same method.  
//sample.Paint(); // Compiler error.  
control.Paint();  // Calls IControl.Paint on SampleClass.  
surface.Paint();  // Calls ISurface.Paint on SampleClass.  
// Output:  
// IControl.Paint  
// ISurface.Paint  An explicit interface implementation doesn't have an access modifier since it isn't
accessible as a member of the type it's defined in. Instead, it's only accessible when
called through an instance of the interface. If you specify an access modifier for an
explicit interface implementation, you get compiler error CS0106 . For more information,
see interface  (C# R eference) .
You can define an implementation for members declared in an interface. If a class
inherits a method implementation from an interface, that method is only accessible
through a reference of the interface type. The inherited member doesn't appear as part
of the public interface. The following sample defines a default implementation for an
interface method:
C#
The following sample invokes the default implementation:
C#interface  ILeft 
{ 
    int P { get;} 
} 
interface  IRight 
{ 
    int P(); 
} 
class Middle : ILeft, IRight 
{ 
    public int P() { return 0; } 
    int ILeft.P { get { return 0; } } 
} 
public interface  IControl  
{ 
    void Paint() => Console.WriteLine( "Default Paint method" ); 
} 
public class SampleClass  : IControl  
{ 
    // Paint() is inherited from IControl.  
} 
var sample = new SampleClass();  
//sample.Paint();// "Paint" isn't accessible.  
var control = sample as IControl;  
control.Paint();  Any class that implements the IControl interface can override the default Paint
method, either as a public method, or as an explicit interface implementation.
C# Programming Guide
Object oriented programming
Interfaces
InheritanceSee alsoHow to explicitly implement interface
memb ers (C# Programming Guide)
Article •09/23/2021
This example declares an interface , IDimensions, and a class, Box, which explicitly
implements the interface members GetLength and GetWidth. The members are accessed
through the interface instance dimensions.
C#Example
interface  IDimensions  
{ 
    float GetLength (); 
    float GetWidth (); 
} 
class Box : IDimensions  
{ 
    float lengthInches;  
    float widthInches;  
    Box( float length, float width) 
    { 
        lengthInches = length;  
        widthInches = width;  
    } 
    // Explicit interface member implementation:  
    float IDimensions.GetLength()
    { 
        return lengthInches;  
    } 
    // Explicit interface member implementation:  
    float IDimensions.GetWidth()  
    { 
        return widthInches;  
    } 
    static void Main() 
    { 
        // Declare a class instance box1:  
        Box box1 = new Box(30.0f, 20.0f); 
        // Declare an interface instance dimensions:  
        IDimensions dimensions = box1;  
        // The following commented lines would produce compilation  Notice that the following lines, in the Main method, are commented out because
they would produce compilation errors. An interface member that is explicitly
implemented cannot be accessed from a class  instance:
C#
Notice also that the following lines, in the Main method, successfully print out the
dimensions of the box because the methods are being called from an instance of
the interface:
C#
C# Programming Guide
Object oriented programming
Interfaces
How to explicitly implement members of two interfaces        // errors because they try to access an explicitly implemented  
        // interface member from a class instance:  
        //System.Console.WriteLine("Length: {0}", box1.GetLength());  
        //System.Console.WriteLine("Width: {0}", box1.GetWidth());  
        // Print out the dimensions of the box by calling the methods  
        // from an instance of the interface:  
        System.Console.WriteLine( "Length: {0}" , dimensions.GetLength());  
        System.Console.WriteLine( "Width: {0}" , dimensions.GetWidth());  
    } 
} 
/* Output:  
    Length: 30  
    Width: 20  
*/ 
Robust Programming
//System.Console.WriteLine("Length: {0}", box1.GetLength());  
//System.Console.WriteLine("Width: {0}", box1.GetWidth());  
System.Console.WriteLine( "Length: {0}" , dimensions.GetLength());  
System.Console.WriteLine( "Width: {0}" , dimensions.GetWidth());  
See alsoHow to explicitly implement members
of two interfaces (C# Programming
Guide)
Article •09/23/2021
Explicit interface  implementation also allows the programmer to implement two
interfaces that have the same member names and give each interface member a
separate implementation. This example displays the dimensions of a box in both metric
and English units. The Box class  implements two interfaces IEnglishDimensions and
IMetricDimensions, which represent the different measurement systems. Both interfaces
have identical member names, Length and Width.
C#Example
// Declare the English units interface:  
interface  IEnglishDimensions  
{ 
    float Length(); 
    float Width(); 
} 
// Declare the metric units interface:  
interface  IMetricDimensions  
{ 
    float Length(); 
    float Width(); 
} 
// Declare the Box class that implements the two interfaces:  
// IEnglishDimensions and IMetricDimensions:  
class Box : IEnglishDimensions , IMetricDimensions  
{ 
    float lengthInches;  
    float widthInches;  
    public Box(float lengthInches, float widthInches ) 
    { 
        this.lengthInches = lengthInches;  
        this.widthInches = widthInches;  
    } 
    // Explicitly implement the members of IEnglishDimensions:  
    float IEnglishDimensions.Length() => lengthInches;  If you want to make the default measurements in English units, implement the methods
Length and Width normally, and explicitly implement the Length and Width methods
from the IMetricDimensions interface:
C#    float IEnglishDimensions.Width() => widthInches;  
    // Explicitly implement the members of IMetricDimensions:  
    float IMetricDimensions.Length() => lengthInches * 2.54f; 
    float IMetricDimensions.Width() => widthInches * 2.54f; 
    static void Main() 
    { 
        // Declare a class instance box1:  
        Box box1 = new Box(30.0f, 20.0f); 
        // Declare an instance of the English units interface:  
        IEnglishDimensions eDimensions = box1;  
        // Declare an instance of the metric units interface:  
        IMetricDimensions mDimensions = box1;  
        // Print dimensions in English units:  
        System.Console.WriteLine( "Length(in): {0}" , eDimensions.Length());  
        System.Console.WriteLine( "Width (in): {0}" , eDimensions.Width());  
        // Print dimensions in metric units:  
        System.Console.WriteLine( "Length(cm): {0}" , mDimensions.Length());  
        System.Console.WriteLine( "Width (cm): {0}" , mDimensions.Width());  
    } 
} 
/* Output:  
    Length(in): 30  
    Width (in): 20  
    Length(cm): 76.2  
    Width (cm): 50.8  
*/ 
Robust Programming
// Normal implementation:  
public float Length() => lengthInches;  
public float Width() => widthInches;  
// Explicit implementation:  
float IMetricDimensions.Length() => lengthInches * 2.54f; 
float IMetricDimensions.Width() => widthInches * 2.54f; In this case, you can access the English units from the class instance and access the
metric units from the interface instance:
C#
C# Programming Guide
Object oriented programming
Interfaces
How to explicitly implement interface memberspublic static void Test() 
{ 
    Box box1 = new Box(30.0f, 20.0f); 
    IMetricDimensions mDimensions = box1;  
    System.Console.WriteLine( "Length(in): {0}" , box1.Length());  
    System.Console.WriteLine( "Width (in): {0}" , box1.Width());  
    System.Console.WriteLine( "Length(cm): {0}" , mDimensions.Length());  
    System.Console.WriteLine( "Width (cm): {0}" , mDimensions.Width());  
} 
See alsoDelegates (C# Programming Guide)
Article •09/29/2022
A delegate  is a type that represents references to methods with a particular parameter
list and return type. When you instantiate a delegate, you can associate its instance with
any method with a compatible signature and return type. Y ou can invoke (or call) the
method through the delegate instance.
Delegates are used to pass methods as arguments to other methods. Event handlers are
nothing more than methods that are invoked through delegates. Y ou create a custom
method, and a class such as a windows control can call your method when a certain
event occurs. The following example shows a delegate declaration:
C#
Any method from any accessible class or struct that matches the delegate type can be
assigned to the delegate. The method can be either static or an instance method. This
flexibility means you can programmatically change method calls, or plug new code into
existing classes.
This ability to refer to a method as a parameter makes delegates ideal for defining
callback methods. Y ou can write a method that compares two objects in your
application. That method can be used in a delegate for a sort algorithm. Because the
comparison code is separate from the library, the sort method can be more general.
Function pointers  support similar scenarios, where you need more control over the
calling convention. The code associated with a delegate is invoked using a virtual
method added to a delegate type. Using function pointers, you can specify different
conventions.public delegate  int PerformCalculation (int x, int y);
７ Note
In the context of method overloading, the signature of a method does not include
the return value. But in the context of delegates, the signature does include the
return value. In other words, a method must have the same return type as the
delegate.
Delegates OverviewDelegates have the following properties:
Delegates are similar to C++ function pointers, but delegates are fully object-
oriented, and unlike C++ pointers to member functions, delegates encapsulate
both an object instance and a method.
Delegates allow methods to be passed as parameters.
Delegates can be used to define callback methods.
Delegates can be chained together; for example, multiple methods can be called
on a single event.
Methods don't have to match the delegate type exactly. For more information, see
Using V ariance in Delegates .
Lambda expressions are a more concise way of writing inline code blocks. Lambda
expressions (in certain contexts) are compiled to delegate types. For more
information about lambda expressions, see Lambda expressions .
Using Delegates
When to Use Delegates Instead of Interfaces (C# Programming Guide)
Delegates with Named vs. Anonymous Methods
Using V ariance in Delegates
How to combine delegates (Multicast Delegates)
How to declare, instantiate, and use a delegate
For more information, see Delegates  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
Delegate
C# Programming Guide
EventsIn This Section
C# Language Specification
See also
６ Collaborat e with us on
GitHub .NET feedb ackThe source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .The .NET documentation is open
source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackUsing Delegates (C# Programming
Guide)
Article •07/31/2023
A delegate  is a type that safely encapsulates a method, similar to a function pointer in C
and C++. Unlike C function pointers, delegates are object-oriented, type safe, and
secure. The type of a delegate is defined by the name of the delegate. The following
example declares a delegate named Callback that can encapsulate a method that takes
a string  as an argument and returns void:
C#
A delegate object is normally constructed by providing the name of the method the
delegate will wrap, or with a lambda expression . Once a delegate is instantiated in this
manner it can be invoked. Invoking a delegate calls the method attached to the
delegate instance. The parameters passed to the delegate by the caller are passed to the
method, and the return value, if any, from the method is returned to the caller by the
delegate. For example:
C#
C#
Delegate types are derived from the Delegate  class in .NET. Delegate types are sealed —
they cannot be derived from— and it is not possible to derive custom classes from
Delegate . Because the instantiated delegate is an object, it can be passed as an
argument, or assigned to a property. This allows a method to accept a delegate as a
parameter, and call the delegate at some later time. This is known as an asynchronouspublic delegate  void Callback (string message );
// Create a method for a delegate.
public static void DelegateMethod (string message )
{
    Console.WriteLine(message);
}
// Instantiate the delegate.
Callback handler = DelegateMethod;
// Call the delegate.
handler( "Hello World" );callback, and is a common method of notifying a caller when a long process has
completed. When a delegate is used in this fashion, the code using the delegate does
not need any knowledge of the implementation of the method being used. The
functionality is similar to the encapsulation interfaces provide.
Another common use of callbacks is defining a custom comparison method and passing
that delegate to a sort method. It allows the caller's code to become part of the sort
algorithm. The following example method uses the Del type as a parameter:
C#
You can then pass the delegate created above to that method:
C#
and receive the following output to the console:
Console
Using the delegate as an abstraction, MethodWithCallback does not need to call the
console directly—it does not have to be designed with a console in mind. What
MethodWithCallback does is simply prepare a string and pass the string to another
method. This is especially powerful since a delegated method can use any number of
parameters.
When a delegate is constructed to wrap an instance method, the delegate references
both the instance and the method. A delegate has no knowledge of the instance type
aside from the method it wraps, so a delegate can refer to any type of object as long as
there is a method on that object that matches the delegate signature. When a delegate
is constructed to wrap a static method, it only references the method. Consider the
following declarations:
C#public static void MethodWithCallback (int param1, int param2, Callback  
callback )
{
    callback( "The number is: "  + (param1 + param2).ToString());
}
MethodWithCallback( 1, 2, handler);
The number is: 3Along with the static DelegateMethod shown previously, we now have three methods
that can be wrapped by a Del instance.
A delegate can call more than one method when invoked. This is referred to as
multicasting. T o add an extra method to the delegate's list of methods—the invocation
list—simply requires adding two delegates using the addition or addition assignment
operators ('+' or '+='). For example:
C#
At this point allMethodsDelegate contains three methods in its invocation list— Method1,
Method2, and DelegateMethod. The original three delegates, d1, d2, and d3, remain
unchanged. When allMethodsDelegate is invoked, all three methods are called in order.
If the delegate uses reference parameters, the reference is passed sequentially to each
of the three methods in turn, and any changes by one method are visible to the next
method. When any of the methods throws an exception that is not caught within the
method, that exception is passed to the caller of the delegate and no subsequent
methods in the invocation list are called. If the delegate has a return value and/or out
parameters, it returns the return value and parameters of the last method invoked. T o
remove a method from the invocation list, use the subtraction or subtraction
assignment operators  (- or -=). For example:
C#public class MethodClass
{
    public void Method1(string message ) { }
    public void Method2(string message ) { }
}
var obj = new MethodClass();
Callback d1 = obj.Method1;
Callback d2 = obj.Method2;
Callback d3 = DelegateMethod;
//Both types of assignment are valid.
Callback allMethodsDelegate = d1 + d2;
allMethodsDelegate += d3;
//remove Method1
allMethodsDelegate -= d1;
// copy AllMethodsDelegate while removing d2
Callback oneMethodDelegate = allMethodsDelegate - d2;Because delegate types are derived from System.Delegate, the methods and properties
defined by that class can be called on the delegate. For example, to find the number of
methods in a delegate's invocation list, you may write:
C#
Delegates with more than one method in their invocation list derive from
MulticastDelegate , which is a subclass of System.Delegate. The above code works in
either case because both classes support GetInvocationList.
Multicast delegates are used extensively in event handling. Event source objects send
event notifications to recipient objects that have registered to receive that event. T o
register for an event, the recipient creates a method designed to handle the event, then
creates a delegate for that method and passes the delegate to the event source. The
source calls the delegate when the event occurs. The delegate then calls the event
handling method on the recipient, delivering the event data. The delegate type for a
given event is defined by the event source. For more, see Events .
Comparing delegates of two different types assigned at compile-time will result in a
compilation error. If the delegate instances are statically of the type System.Delegate,
then the comparison is allowed, but will return false at run time. For example:
C#
C# Programming Guide
Delegates
Using V ariance in Delegatesint invocationCount = d1.GetInvocationList().GetLength( 0);
delegate  void Callback1 ();
delegate  void Callback2 ();
static void method(Callback1 d, Callback2 e, System.Delegate f )
{
    // Compile-time error.
    //Console.WriteLine(d == e);
    // OK at compile-time. False if the run-time type of f
    // is not the same as that of d.
    Console.WriteLine(d == f);
}
See alsoVariance in Delegates
Using V ariance for Func and Action Generic Delegates
Events
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
 Provide product feedbackDelegates with Named vs. Anonymous
Methods (C# Programming Guide)
Article •11/08/2021
A delegate  can be associated with a named method. When you instantiate a delegate by
using a named method, the method is passed as a parameter, for example:
C#
This is called using a named method. Delegates constructed with a named method can
encapsulate either a static  method or an instance method. Named methods are the only
way to instantiate a delegate in earlier versions of C#. However, in a situation where
creating a new method is unwanted overhead, C# enables you to instantiate a delegate
and immediately specify a code block that the delegate will process when it is called.
The block can contain either a lambda expression  or an anonymous method .
The method that you pass as a delegate parameter must have the same signature as the
delegate declaration. A delegate instance may encapsulate either static or instance
method.
Beginning with C# 10, method groups with a single overload have a natur al type . This
means the compiler can infer the return type and parameter types for the delegate type:
C#// Declare a delegate.
delegate  void WorkCallback (int x);
// Define a named method.
void DoWork(int k) { /* ... */  }
// Instantiate the delegate using the method as a parameter.
WorkCallback d = obj.DoWork;
７ Note
Although the delegate can use an out parameter, we do not recommend its use
with multicast event delegates because you cannot know which delegate will be
called.
var read = Console.Read; // Just one overload; Func<int> inferredThe following is a simple example of declaring and using a delegate. Notice that both
the delegate, Del, and the associated method, MultiplyNumbers, have the same
signature
C#
In the following example, one delegate is mapped to both static and instance methods
and returns specific information from each.
C#var write = Console.Write; // ERROR: Multiple overloads, can't choose
Examples
// Declare a delegate
delegate  void MultiplyCallback (int i, double j);
class MathClass
{
    static void Main()
    {
        MathClass m = new MathClass();
        // Delegate instantiation using "MultiplyNumbers"
        MultiplyCallback d = m.MultiplyNumbers;
        // Invoke the delegate object.
        Console.WriteLine( "Invoking the delegate using 'MultiplyNumbers':" );
        for (int i = 1; i <= 5; i++)
        {
            d(i, 2);
        }
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
    // Declare the associated method.
    void MultiplyNumbers (int m, double n)
    {
        Console.Write(m * n + " ");
    }
}
/* Output:
    Invoking the delegate using 'MultiplyNumbers':
    2 4 6 8 10
*/C# Programming Guide
Delegates
How to combine delegates (Multicast Delegates)
Events// Declare a delegate
delegate  void Callback ();
class SampleClass
{
    public void InstanceMethod ()
    {
        Console.WriteLine( "A message from the instance method." );
    }
    static public void StaticMethod ()
    {
        Console.WriteLine( "A message from the static method." );
    }
}
class TestSampleClass
{
    static void Main()
    {
        var sc = new SampleClass();
        // Map the delegate to the instance method:
        Callback d = sc.InstanceMethod;
        d();
        // Map to the static method:
        d = SampleClass.StaticMethod;
        d();
    }
}
/* Output:
    A message from the instance method.
    A message from the static method.
*/
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
 Provide product feedbackHow to combine delegates (Multicast
Delegates) (C# Programming Guide)
Article •09/15/2021
This example demonstrates how to create multicast delegates. A useful property of
delegate  objects is that multiple objects can be assigned to one delegate instance by
using the + operator. The multicast delegate contains a list of the assigned delegates.
When the multicast delegate is called, it invokes the delegates in the list, in order. Only
delegates of the same type can be combined.
The - operator can be used to remove a component delegate from a multicast
delegate.
C#Example
using System;  
// Define a custom delegate that has a string parameter and returns void.  
delegate  void CustomDel (string s); 
class TestClass  
{ 
    // Define two methods that have the same signature as CustomDel.  
    static void Hello(string s) 
    { 
        Console.WriteLine( $"  Hello, {s}!"); 
    } 
    static void Goodbye(string s) 
    { 
        Console.WriteLine( $"  Goodbye, {s}!"); 
    } 
    static void Main() 
    { 
        // Declare instances of the custom delegate.  
        CustomDel hiDel, byeDel, multiDel, multiMinusHiDel;  
        // In this example, you can omit the custom delegate if you  
        // want to and use Action<string> instead.  
        //Action<string> hiDel, byeDel, multiDel, multiMinusHiDel;  
        // Initialize the delegate object hiDel that references the  
        // method Hello.  
        hiDel = Hello;  MulticastDelegate
C# Programming Guide
Events        // Initialize the delegate object byeDel that references the  
        // method Goodbye.  
        byeDel = Goodbye;  
        // The two delegates, hiDel and byeDel, are combined to  
        // form multiDel.  
        multiDel = hiDel + byeDel;  
        // Remove hiDel from the multicast delegate, leaving byeDel,  
        // which calls only the method Goodbye.  
        multiMinusHiDel = multiDel - hiDel;  
        Console.WriteLine( "Invoking delegate hiDel:" ); 
        hiDel( "A"); 
        Console.WriteLine( "Invoking delegate byeDel:" ); 
        byeDel( "B"); 
        Console.WriteLine( "Invoking delegate multiDel:" ); 
        multiDel( "C"); 
        Console.WriteLine( "Invoking delegate multiMinusHiDel:" ); 
        multiMinusHiDel( "D"); 
    } 
} 
/* Output:  
Invoking delegate hiDel:  
  Hello, A!  
Invoking delegate byeDel:  
  Goodbye, B!  
Invoking delegate multiDel:  
  Hello, C!  
  Goodbye, C!  
Invoking delegate multiMinusHiDel:  
  Goodbye, D!  
*/ 
See alsoHow to declare, instantiate, and use a
Delegate (C# Programming Guide)
Article •09/29/2022
You can declare delegates using any of the following methods:
Declare a delegate type and declare a method with a matching signature:
C#
C#
Assign a method group to a delegate type:
C#
Declare an anonymous method:
C#
Use a lambda expression:
C#// Declare a delegate.  
delegate  void Del(string str); 
// Declare a method with the same signature as the delegate.  
static void Notify(string name) 
{ 
    Console.WriteLine( $"Notification received for: {name}"); 
} 
// Create an instance of the delegate.  
Del del1 = new Del(Notify);  
// C# 2.0 provides a simpler way to declare an instance of Del.  
Del del2 = Notify;  
// Instantiate Del by using an anonymous method.  
Del del3 = delegate (string name) 
    { Console.WriteLine( $"Notification received for: {name}"); }; For more information, see Lambda Expressions .
The following example illustrates declaring, instantiating, and using a delegate. The
BookDB class encapsulates a bookstore database that maintains a database of books. It
exposes a method, ProcessPaperbackBooks, which finds all paperback books in the
database and calls a delegate for each one. The delegate type that is used is named
ProcessBookCallback. The Test class uses this class to print the titles and average price
of the paperback books.
The use of delegates promotes good separation of functionality between the bookstore
database and the client code. The client code has no knowledge of how the books are
stored or how the bookstore code finds paperback books. The bookstore code has no
knowledge of what processing is performed on the paperback books after it finds them.
C#// Instantiate Del by using a lambda expression.  
Del del4 = name =>  { Console.WriteLine( $"Notification received for:  
{name}"); }; 
Example
// A set of classes for handling a bookstore:  
namespace  Bookstore  
{ 
    using System.Collections;  
    // Describes a book in the book list:  
    public struct Book 
    { 
        public string Title;        // Title of the book.  
        public string Author;       // Author of the book.  
        public decimal Price;       // Price of the book.  
        public bool Paperback;      // Is it paperback?  
        public Book(string title, string author, decimal price, bool 
paperBack ) 
        {  
            Title = title;  
            Author = author;  
            Price = price;  
            Paperback = paperBack;  
        }  
    } 
    // Declare a delegate type for processing a book:  
    public delegate  void ProcessBookCallback (Book book );     // Maintains a book database.
    public class BookDB 
    { 
        // List of all books in the database:  
        ArrayList list = new ArrayList();  
        // Add a book to the database:  
        public void AddBook(string title, string author, decimal price, bool 
paperBack ) 
        {  
            list.Add( new Book(title, author, price, paperBack));  
        }  
        // Call a passed-in delegate on each paperback book to process it:  
        public void ProcessPaperbackBooks (ProcessBookCallback processBook ) 
        {  
            foreach (Book b in list) 
            {  
                if (b.Paperback)  
                    // Calling the delegate:  
                    processBook(b);  
            }  
        }  
    } 
} 
// Using the Bookstore classes:  
namespace  BookTestClient  
{ 
    using Bookstore;  
    // Class to total and average prices of books:  
    class PriceTotaller  
    { 
        int countBooks = 0; 
        decimal priceBooks = 0.0m; 
        internal  void AddBookToTotal (Book book ) 
        {  
            countBooks += 1; 
            priceBooks += book.Price;  
        }  
        internal  decimal AveragePrice () 
        {  
            return priceBooks / countBooks;  
        }  
    } 
    // Class to test the book database:  
    class Test 
    { 
        // Print the title of the book.  
        static void PrintTitle (Book b)         {  
            Console.WriteLine( $"   {b.Title} "); 
        }  
        // Execution starts here.
        static void Main() 
        {  
            BookDB bookDB = new BookDB();  
            // Initialize the database with some books:  
            AddBooks(bookDB);  
            // Print all the titles of paperbacks:  
            Console.WriteLine( "Paperback Book Titles:" ); 
            // Create a new delegate object associated with the static  
            // method Test.PrintTitle:  
            bookDB.ProcessPaperbackBooks(PrintTitle);  
            // Get the average price of a paperback by using  
            // a PriceTotaller object:  
            PriceTotaller totaller = new PriceTotaller();  
            // Create a new delegate object associated with the nonstatic  
            // method AddBookToTotal on the object totaller:  
            bookDB.ProcessPaperbackBooks(totaller.AddBookToTotal);  
            Console.WriteLine( "Average Paperback Book Price: ${0:#.##}" , 
                    totaller.AveragePrice());  
        }  
        // Initialize the book database with some test books:  
        static void AddBooks (BookDB bookDB ) 
        {  
            bookDB.AddBook( "The C Programming Language" , "Brian W. Kernighan  
and Dennis M. Ritchie" , 19.95m, true); 
            bookDB.AddBook( "The Unicode Standard 2.0" , "The Unicode  
Consortium" , 39.95m, true); 
            bookDB.AddBook( "The MS-DOS Encyclopedia" , "Ray Duncan" , 129.95m, 
false); 
            bookDB.AddBook( "Dogbert's Clues for the Clueless" , "Scott 
Adams", 12.00m, true); 
        }  
    } 
} 
/* Output:  
Paperback Book Titles:  
   The C Programming Language  
   The Unicode Standard 2.0  
   Dogbert's Clues for the Clueless  
Average Paperback Book Price: $23.97  
*/ Declaring a delegate.
The following statement declares a new delegate type.
C#
Each delegate type describes the number and types of the arguments, and the
type of the return value of methods that it can encapsulate. Whenever a new set of
argument types or return value type is needed, a new delegate type must be
declared.
Instantiating a delegate.
After a delegate type has been declared, a delegate object must be created and
associated with a particular method. In the previous example, you do this by
passing the PrintTitle method to the ProcessPaperbackBooks method as in the
following example:
C#
This creates a new delegate object associated with the static  method
Test.PrintTitle. Similarly, the non-static method AddBookToTotal on the object
totaller is passed as in the following example:
C#
In both cases a new delegate object is passed to the ProcessPaperbackBooks
method.
After a delegate is created, the method it is associated with never changes;
delegate objects are immutable.
Calling a delegate.
After a delegate object is created, the delegate object is typically passed to other
code that will call the delegate. A delegate object is called by using the name ofRobust Programming
public delegate  void ProcessBookCallback (Book book ); 
bookDB.ProcessPaperbackBooks(PrintTitle);  
bookDB.ProcessPaperbackBooks(totaller.AddBookToTotal);  the delegate object, followed by the parenthesized arguments to be passed to the
delegate. Following is an example of a delegate call:
C#
A delegate can be either called synchronously, as in this example, or
asynchronously by using BeginInvoke and EndInvoke methods.
C# Programming Guide
Events
DelegatesprocessBook(b);  
See alsoStrings and string literals
Article •05/27/2023
A string is an object of type String  whose value is text. Internally, the text is stored as a
sequential read-only collection of Char objects. There's no null-terminating character at
the end of a C# string; therefore a C# string can contain any number of embedded null
characters ('\0'). The Length  property of a string represents the number of Char objects
it contains, not the number of Unicode characters. T o access the individual Unicode
code points in a string, use the StringInfo  object.
In C#, the string keyword is an alias for String ; therefore, String and string are
equivalent. It's recommended to use the provided alias string as it works even without
using System;. The String class provides many methods for safely creating,
manipulating, and comparing strings. In addition, the C# language overloads some
operators to simplify common string operations. For more information about the
keyword, see string . For more information about the type and its methods, see String .
You can declare and initialize strings in various ways, as shown in the following example:
C#string vs. System.String
Declaring and initia lizing strings
// Declare without initializing.
string message1;
// Initialize to null.
string message2 = null;
// Initialize as an empty string.
// Use the Empty constant instead of the literal "".
string message3 = System.String.Empty;
// Initialize with a regular string literal.
string oldPath = "c:\\Program Files\\Microsoft Visual Studio 8.0" ;
// Initialize with a verbatim string literal.
string newPath = @"c:\Program Files\Microsoft Visual Studio 9.0" ;
// Use System.String if you prefer.
System.String greeting = "Hello World!" ;You don't use the new operator to create a string object except when initializing the
string with an array of chars.
Initialize a string with the Empty  constant value to create a new String  object whose
string is of zero length. The string literal representation of a zero-length string is "". By
initializing strings with the Empty  value instead of null, you can reduce the chances of a
NullR eferenceException  occurring. Use the static IsNullOrEmpty(S tring)  method to verify
the value of a string before you try to access it.
String objects are immut able: they can't be changed after they've been created. All of
the String  methods and C# operators that appear to modify a string actually return the
results in a new string object. In the following example, when the contents of s1 and s2
are concatenated to form a single string, the two original strings are unmodified. The +=
operator creates a new string that contains the combined contents. That new object is
assigned to the variable s1, and the original object that was assigned to s1 is released
for garbage collection because no other variable holds a reference to it.
C#// In local variables (i.e. within a method body)
// you can use implicit typing.
var temp = "I'm still a strongly-typed System.String!" ;
// Use a const string to prevent 'message4' from
// being used to store another string value.
const string message4 = "You can't get rid of me!" ;
// Use the String constructor only when creating
// a string from a char*, char[], or sbyte*. See
// System.String documentation for details.
char[] letters = { 'A', 'B', 'C' };
string alphabet = new string(letters);
Immutability of strings
string s1 = "A string is more " ;
string s2 = "than the sum of its chars." ;
// Concatenate s1 and s2. This actually creates a new
// string object and stores it in s1, releasing the
// reference to the original object.
s1 += s2;
System.Console.WriteLine(s1);
// Output: A string is more than the sum of its chars.Because a string "modification" is actually a new string creation, you must use caution
when you create references to strings. If you create a reference to a string, and then
"modify" the original string, the reference will continue to point to the original object
instead of the new object that was created when the string was modified. The following
code illustrates this behavior:
C#
For more information about how to create new strings that are based on modifications
such as search and replace operations on the original string, see How to modify string
contents .
Quot ed str ing lit erals start and end with a single double quote character ( ") on the same
line. Quoted string literals are best suited for strings that fit on a single line and don't
include any escape sequences . A quoted string literal must embed escape characters, as
shown in the following example:
C#string str1 = "Hello " ;
string str2 = str1;
str1 += "World";
System.Console.WriteLine(str2);
//Output: Hello
Quoted string literals
string columns = "Column 1\tColumn 2\tColumn 3" ;
//Output: Column 1        Column 2        Column 3
string rows = "Row 1\r\nRow 2\r\nRow 3" ;
/* Output:
    Row 1
    Row 2
    Row 3
*/
string title = "\"The \u00C6olean Harp\", by Samuel Taylor Coleridge" ;
//Output: "The Æolean Harp", by Samuel Taylor Coleridge
Verbatim string literalsVerbatim str ing lit erals are more convenient for multi-line strings, strings that contain
backslash characters, or embedded double quotes. V erbatim strings preserve new line
characters as part of the string text. Use double quotation marks to embed a quotation
mark inside a verbatim string. The following example shows some common uses for
verbatim strings:
C#
Beginning with C# 11, you can use raw str ing lit erals to more easily create strings that
are multi-line, or use any characters requiring escape sequences. Raw str ing lit erals
remove the need to ever use escape sequences. Y ou can write the string, including
whitespace formatting, how you want it to appear in output. A raw str ing lit eral:
Starts and ends with a sequence of at least three double quote characters ( """).
You're allowed more than three consecutive characters to start and end the
sequence in order to support string literals that contain three (or more) repeated
quote characters.
Single line raw string literals require the opening and closing quote characters on
the same line.
Multi-line raw string literals require both opening and closing quote characters on
their own line.
In multi-line raw string literals, any whitespace to the left of the closing quotes is
removed from all lines of the raw string literal.
In multi-line raw string literals, whitespace following the opening quote on the
same line is ignored.string title = "\"The \u00C6olean Harp\", by Samuel Taylor Coleridge" ;
//Output: "The Æolean Harp", by Samuel Taylor Coleridge
string filePath = @"C:\Users\scoleridge\Documents\" ;
//Output: C:\Users\scoleridge\Documents\
string text = @"My pensive SARA ! thy soft cheek reclined
    Thus on mine arm, most soothing sweet it is
    To sit beside our Cot,..." ;
/* Output:
My pensive SARA ! thy soft cheek reclined
    Thus on mine arm, most soothing sweet it is
    To sit beside our Cot,...
*/
string quote = @"Her name was ""Sara.""" ;
//Output: Her name was "Sara."
Raw string literalsIn multi-line raw string literals, whitespace only lines following the opening quote
are included in the string literal.
The following examples demonstrate these rules:
C#
The following examples demonstrate the compiler errors reported based on these rules:
C#string singleLine = """Friends say " hello" as they pass by." "";
string multiLine = """
    "Hello World! " is typically the first program someone writes.
    """;
string embeddedXML = """
       <element attr = " content">
           <body style=" normal">
               Here is the main text
           </body>
           <footer>
               Excerpts from " An amazing story "
           </footer>
       </element >
       """;
// The line "<element attr = "content">" starts in the first column.
// All whitespace left of that column is removed from the string.
string rawStringLiteralDelimiter = """"
    Raw string literals are delimited 
    by a string of at least three double quotes,
    like this: """
    """";
// CS8997: Unterminated raw string literal.
var multiLineStart = """This
    is the beginning of a string 
    """;
// CS9000: Raw string literal delimiter must be on its own line.
var multiLineEnd = """
    This is the beginning of a string " "";
// CS8999: Line does not start with the same whitespace as the closing line
// of the raw string literal
var noOutdenting = """
    A line of text.
Trying to outdent the second line.
    """;The first two examples are invalid because multiline raw string literals require the
opening and closing quote sequence on its own line. The third example is invalid
because the text is outdented from the closing quote sequence.
You should consider raw string literals when you're generating text that includes
characters that require escape sequences  when using quoted string literals or verbatim
string literals. Raw string literals will be easier for you and others to read because it will
more closely resemble the output text. For example, consider the following code that
includes a string of formatted JSON:
C#
Compare that text with the equivalent text in the sample on JSON deserialization , which
doesn't make use of this new feature.
Escape
sequenceCharact er name Unicode encoding
\' Single quote 0x0027string jsonString = """
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius ": 25,
  "Summary": "Hot",
  "DatesAvailable ": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "TemperatureRanges ": {
    "Cold": {
      "High": 20,
      "Low": -10
    },
    "Hot": {
      "High": 60,
      "Low": 20
    }
            },
  "SummaryWords ": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
""";
String escape sequencesEscape
sequenceCharact er name Unicode encoding
\" Double quote 0x0022
\ Backslash 0x005C
\0 Null 0x0000
\a Alert 0x0007
\b Backspace 0x0008
\f Form feed 0x000C
\n New line 0x000A
\r Carriage return 0x000D
\t Horizontal tab 0x0009
\v Vertical tab 0x000B
\u Unicode escape sequence (UTF-16) \uHHHH (range: 0000 - FFFF; example:
\u00E7 = "ç")
\U Unicode escape sequence (UTF-32) \U00HHHHHH (range: 000000 - 10FFFF;
example: \U0001F47D = "👽 ")
\x Unicode escape sequence similar to
"\u" except with variable length\xH[H][H][H] (range: 0 - FFFF; example:
\x00E7 or \x0E7 or \xE7 = "ç")
２ Warning
When using the \x escape sequence and specifying less than 4 hex digits, if the
characters that immediately follow the escape sequence are valid hex digits (i.e. 0-
9, A-F, and a-f), they will be interpreted as being part of the escape sequence. For
example, \xA1 produces "¡", which is code point U+00A1. However, if the next
character is "A" or "a", then the escape sequence will instead be interpreted as
being \xA1A and produce " ਚ ", which is code point U+0A1A. In such cases,
specifying all 4 hex digits (for example, \x00A1) prevents any possible
misinterpretation.
７ NoteA format string is a string whose contents are determined dynamically at run time.
Format strings are created by embedding interpolat ed expr essions  or placeholders inside
of braces within a string. Everything inside the braces ( {...}) will be resolved to a value
and output as a formatted string at run time. There are two methods to create format
strings: string interpolation and composite formatting.
Interpolat ed str ings are identified by the $ special character and include interpolated
expressions in braces. If you're new to string interpolation, see the String interpolation -
C# interactive tutorial  for a quick overview.
Use string interpolation to improve the readability and maintainability of your code.
String interpolation achieves the same results as the String.Format method, but
improves ease of use and inline clarity.
C#
Beginning with C# 10, you can use string interpolation to initialize a constant string
when all the expressions used for placeholders are also constant strings.At compile time, verbatim and raw strings are converted to ordinary strings with all
the same escape sequences. Therefore, if you view a verbatim or raw string in the
debugger watch window, you will see the escape characters that were added by the
compiler, not the verbatim or raw version from your source code. For example, the
verbatim string @"C:\files.txt" will appear in the watch window as "C: \files.txt".
Format strings
String interpolation
var jh = (firstName: "Jupiter" , lastName: "Hammon" , born: 1711, published: 
1761);
Console.WriteLine( $"{jh.firstName}  {jh.lastName}  was an African American  
poet born in {jh.born} .");
Console.WriteLine( $"He was first published in {jh.published}  at the age of 
{jh.published - jh.born} .");
Console.WriteLine( $"He'd be over {Math.Round(( 2018d - jh.born) / 100d) * 
100d} years old today." );
// Output:
// Jupiter Hammon was an African American poet born in 1711.
// He was first published in 1761 at the age of 50.
// He'd be over 300 years old today.Beginning with C# 11, you can combine raw str ing lit erals with string interpolations. Y ou
start and end the format string with three or more successive double quotes. If your
output string should contain the { or } character, you can use extra $ characters to
specify how many { and } characters start and end an interpolation. Any sequence of
fewer { or } characters is included in the output. The following example shows how
you can use that feature to display the distance of a point from the origin, and place the
point inside braces:
C#
C# also allows verbatim string interpolation, for example across multiple lines, using the
$@ or @$ syntax.
To interpret escape sequences literally, use a verbatim  string literal. An interpolated
verbatim string starts with the $ character followed by the @ character. Y ou can use the
$ and @ tokens in any order: both $@"..." and @$"..." are valid interpolated verbatim
strings.
C#int X = 2;
int Y = 3;
var pointMessage = $ $"""The point {{{X}}, {{Y}}} is {{Math.Sqrt(X * X + Y *  
Y)}} from the origin." "";
Console.WriteLine(pointMessage);
// Output:
// The point {2, 3} is 3.605551275463989 from the origin.
Verbatim string interpolation
var jh = (firstName: "Jupiter" , lastName: "Hammon" , born: 1711, published: 
1761);
Console.WriteLine( $@"{jh.firstName}  {jh.lastName}
    was an African American poet born in {jh.born} .");
Console.WriteLine(@ $"He was first published in {jh.published}
at the age of {jh.published - jh.born} .");
// Output:
// Jupiter Hammon
//     was an African American poet born in 1711.
// He was first published in 1761
// at the age of 50.The String.Format  utilizes placeholders in braces to create a format string. This example
results in similar output to the string interpolation method used above.
C#
For more information on formatting .NET types, see Formatting T ypes in .NET .
A substring is any sequence of characters that is contained in a string. Use the Substring
method to create a new string from a part of the original string. Y ou can search for one
or more occurrences of a substring by using the IndexOf  method. Use the Replace
method to replace all occurrences of a specified substring with a new string. Like the
Substring  method, Replace  actually returns a new string and doesn't modify the original
string. For more information, see How to search strings  and How to modify string
contents .
C#Composite formatting
var pw = (firstName: "Phillis" , lastName: "Wheatley" , born: 1753, published:  
1773);
Console.WriteLine( "{0} {1} was an African American poet born in {2}." , 
pw.firstName, pw.lastName, pw.born);
Console.WriteLine( "She was first published in {0} at the age of {1}." , 
pw.published, pw.published - pw.born);
Console.WriteLine( "She'd be over {0} years old today." , Math.Round(( 2018d - 
pw.born) / 100d) * 100d);
// Output:
// Phillis Wheatley was an African American poet born in 1753.
// She was first published in 1773 at the age of 20.
// She'd be over 300 years old today.
Substrings
string s3 = "Visual C# Express" ;
System.Console.WriteLine(s3.Substring( 7, 2));
// Output: "C#"
System.Console.WriteLine(s3.Replace( "C#", "Basic"));
// Output: "Visual Basic Express"
// Index values are zero-based
int index = s3.IndexOf( "C");
// index = 7You can use array notation with an index value to acquire read-only access to individual
characters, as in the following example:
C#
If the String  methods don't provide the functionality that you must have to modify
individual characters in a string, you can use a StringBuilder  object to modify the
individual chars "in-place", and then create a new string to store the results by using the
StringBuilder  methods. In the following example, assume that you must modify the
original string in a particular way and then store the results for future use:
C#
An empty string is an instance of a System.S tring  object that contains zero characters.
Empty strings are used often in various programming scenarios to represent a blank text
field. Y ou can call methods on empty strings because they're valid System.S tring  objects.
Empty strings are initialized as follows:
C#Accessing individual characters
string s5 = "Printing backwards" ;
for (int i = 0; i < s5.Length; i++)
{
    System.Console.Write(s5[s5.Length - i - 1]);
}
// Output: "sdrawkcab gnitnirP"
string question = "hOW DOES mICROSOFT wORD DEAL WITH THE cAPS lOCK KEY?" ;
System.Text.StringBuilder sb = new System.Text.StringBuilder(question);
for (int j = 0; j < sb.Length; j++)
{
    if (System.Char.IsLower(sb[j]) == true)
        sb[j] = System.Char.ToUpper(sb[j]);
    else if (System.Char.IsUpper(sb[j]) == true)
        sb[j] = System.Char.ToLower(sb[j]);
}
// Store the new string.
string corrected = sb.ToString();
System.Console.WriteLine(corrected);
// Output: How does Microsoft Word deal with the Caps Lock key?
Null strings and empty stringsBy contrast, a null string doesn't refer to an instance of a System.S tring  object and any
attempt to call a method on a null string causes a NullR eferenceException . However, you
can use null strings in concatenation and comparison operations with other strings. The
following examples illustrate some cases in which a reference to a null string does and
doesn't cause an exception to be thrown:
C#
String operations in .NET are highly optimized and in most cases don't significantly
impact performance. However, in some scenarios such as tight loops that are executing
many hundreds or thousands of times, string operations can affect performance. Thestring s = String.Empty;
string str = "hello";
string nullStr = null;
string emptyStr = String.Empty;
string tempStr = str + nullStr;
// Output of the following line: hello
Console.WriteLine(tempStr);
bool b = (emptyStr == nullStr);
// Output of the following line: False
Console.WriteLine(b);
// The following line creates a new empty string.
string newStr = emptyStr + nullStr;
// Null strings and empty strings behave differently. The following
// two lines display 0.
Console.WriteLine(emptyStr.Length);
Console.WriteLine(newStr.Length);
// The following line raises a NullReferenceException.
//Console.WriteLine(nullStr.Length);
// The null character can be displayed and counted, like other chars.
string s1 = "\x0" + "abc";
string s2 = "abc" + "\x0";
// Output of the following line: * abc*
Console.WriteLine( "*" + s1 + "*");
// Output of the following line: *abc *
Console.WriteLine( "*" + s2 + "*");
// Output of the following line: 4
Console.WriteLine(s2.Length);
Using StringBuilder for fast string creationStringBuilder  class creates a string buffer that offers better performance if your program
performs many string manipulations. The StringBuilder  string also enables you to
reassign individual characters, something the built-in string data type doesn't support.
This code, for example, changes the content of a string without creating a new string:
C#
In this example, a StringBuilder  object is used to create a string from a set of numeric
types:
C#
Because the String  type implements IEnumerable<T> , you can use the extension
methods defined in the Enumerable  class on strings. T o avoid visual clutter, these
methods are excluded from IntelliSense for the String  type, but they're available
nevertheless. Y ou can also use LINQ query expressions on strings. For more information,
see LINQ and S trings .
How to modify string contents : Illustrates techniques to transform strings and
modify the contents of strings.System.Text.StringBuilder sb = new System.Text.StringBuilder( "Rat: the ideal  
pet");
sb[0] = 'C';
System.Console.WriteLine(sb.ToString());
//Outputs Cat: the ideal pet
var sb = new StringBuilder();
// Create a string composed of numbers 0 - 9
for (int i = 0; i < 10; i++)
{
    sb.Append(i.ToString());
}
Console.WriteLine(sb);  // displays 0123456789
// Copy one character of the string (not possible with a System.String)
sb[0] = sb[9];
Console.WriteLine(sb);  // displays 9123456789
Strings, extension methods and LINQ
Related articlesHow to compare strings : Shows how to perform ordinal and culture specific
comparisons of strings.
How to concatenate multiple strings : Demonstrates various ways to join multiple
strings into one.
How to parse strings using S tring.Split : Contains code examples that illustrate how
to use the String.Split  method to parse strings.
How to search strings : Explains how to use search for specific text or patterns in
strings.
How to determine whether a string represents a numeric value : Shows how to
safely parse a string to see whether it has a valid numeric value.
String interpolation : Describes the string interpolation feature that provides a
convenient syntax to format strings.
Basic S tring Operations : Provides links to articles that use System.S tring  and
System.T ext.StringBuilder  methods to perform basic string operations.
Parsing S trings : Describes how to convert string representations of .NET base types
to instances of the corresponding types.
Parsing Date and Time S trings in .NET : Shows how to convert a string such as
"01/24/2008" to a System.DateTime  object.
Comparing S trings : Includes information about how to compare strings and
provides examples in C# and Visual Basic.
Using the S tringBuilder Class : Describes how to create and modify dynamic string
objects by using the StringBuilder  class.
LINQ and S trings : Provides information about how to perform various string
operations by using LINQ queries.
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
 Provide product feedbackHow to determine whether a string
represents a numeric value (C#
Programming Guide)
Article •04/16/2022
To determine whether a string is a valid representation of a specified numeric type, use
the static TryParse method that is implemented by all primitive numeric types and also
by types such as DateTime  and IPAddress . The following example shows how to
determine whether "108" is a valid int.
C#
If the string contains nonnumeric characters or the numeric value is too large or too
small for the particular type you have specified, TryParse returns false and sets the out
parameter to zero. Otherwise, it returns true and sets the out parameter to the numeric
value of the string.
The following examples show how to use TryParse with string representations of long,
byte, and decimal values.
C#int i = 0; 
string s = "108";   
bool result = int.TryParse(s, out i); //i now = 108   
７ Note
A string may contain only numeric characters and still not be valid for the type
whose TryParse method that you use. For example, "256" is not a valid value for
byte but it is valid for int. "98.6" is not a valid value for int but it is a valid
decimal.
Example
string numString = "1287543" ; //"1287543.0" will return false for a long  
long number1 = 0; 
bool canConvert = long.TryParse(numString, out number1);Primitive numeric types also implement the Parse static method, which throws an
exception if the string is not a valid number. TryParse is generally more efficient
because it just returns false if the number is not valid.
Always use the TryParse or Parse methods to validate user input from controls such as
text boxes and combo boxes.
How to convert a byte array to an int
How to convert a string to a number
How to convert between hexadecimal strings and numeric types
Parsing Numeric S trings
Formatting T ypesif (canConvert == true) 
Console.WriteLine( "number1 now = {0}" , number1);  
else 
Console.WriteLine( "numString is not a valid long" ); 
byte number2 = 0; 
numString = "255"; // A value of 256 will return false  
canConvert = byte.TryParse(numString, out number2);  
if (canConvert == true) 
Console.WriteLine( "number2 now = {0}" , number2);  
else 
Console.WriteLine( "numString is not a valid byte" ); 
decimal number3 = 0; 
numString = "27.3"; //"27" is also a valid decimal  
canConvert = decimal.TryParse(numString, out number3);  
if (canConvert == true) 
Console.WriteLine( "number3 now = {0}" , number3);  
else 
Console.WriteLine( "number3 is not a valid decimal" ); 
Robust Programming
.NET Security
See alsoIndexers (C# Programming Guide)
Article •04/12/2023
Indexers allow instances of a class or struct to be indexed just like arrays. The indexed
value can be set or retrieved without explicitly specifying a type or instance member.
Indexers resemble properties  except that their accessors take parameters.
The following example defines a generic class with simple get and set accessor methods
to assign and retrieve values. The Program class creates an instance of this class for
storing strings.
C#
using System;  
class SampleCollection <T> 
{ 
   // Declare an array to store the data elements.  
   private T[] arr = new T[100]; 
   // Define the indexer to allow client code to use [] notation.  
   public T this[int i] 
   { 
      get { return arr[i]; }  
      set { arr[i] = value; } 
   } 
} 
class Program 
{ 
   static void Main() 
   { 
      var stringCollection = new SampleCollection< string>(); 
      stringCollection[ 0] = "Hello, World" ; 
      Console.WriteLine(stringCollection[ 0]); 
   } 
} 
// The example displays the following output:  
//       Hello, World.  
７ Note
For more examples, see Related Sections .
Expression Body Definitio nsIt is common for an indexer's get or set accessor to consist of a single statement that
either returns or sets a value. Expression-bodied members provide a simplified syntax to
support this scenario. A read-only indexer can be implemented as an expression-bodied
member, as the following example shows.
C#
Note that => introduces the expression body, and that the get keyword is not used.
Both the get and set accessor can be implemented as expression-bodied members. In
this case, both get and set keywords must be used. For example:
C#using System;  
class SampleCollection <T> 
{ 
   // Declare an array to store the data elements.  
   private T[] arr = new T[100]; 
   int nextIndex = 0; 
   // Define the indexer to allow client code to use [] notation.  
   public T this[int i] => arr[i];  
   public void Add(T value) 
   { 
      if (nextIndex >= arr.Length)  
         throw new IndexOutOfRangeException( $"The collection can hold only  
{arr.Length}  elements." ); 
      arr[nextIndex++] = value; 
   } 
} 
class Program 
{ 
   static void Main() 
   { 
      var stringCollection = new SampleCollection< string>(); 
      stringCollection.Add( "Hello, World" ); 
      System.Console.WriteLine(stringCollection[ 0]); 
   } 
} 
// The example displays the following output:  
//       Hello, World.  
using System;  
class SampleCollection <T> 
{ 
   // Declare an array to store the data elements.  Indexers enable objects to be indexed in a similar manner to arrays.
A get accessor returns a value. A set accessor assigns a value.
The this keyword is used to define the indexer.
The value  keyword is used to define the value being assigned by the set accessor.
Indexers do not have to be indexed by an integer value; it is up to you how to
define the specific look-up mechanism.
Indexers can be overloaded.
Indexers can have more than one formal parameter, for example, when accessing a
two-dimensional array.
Using Indexers
Indexers in Interfaces
Comparison Between Properties and Indexers   private T[] arr = new T[100]; 
   // Define the indexer to allow client code to use [] notation.  
   public T this[int i] 
   { 
      get => arr[i];  
      set => arr[i] = value; 
   } 
} 
class Program 
{ 
   static void Main() 
   { 
      var stringCollection = new SampleCollection< string>(); 
      stringCollection[ 0] = "Hello, World." ; 
      Console.WriteLine(stringCollection[ 0]); 
   } 
} 
// The example displays the following output:  
//       Hello, World.  
Indexers Overview
Related SectionsRestricting Accessor Accessibility
For more information, see Indexers  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
C# Programming Guide
PropertiesC# Language Specification
See alsoUsing indexers (C# Programming Guide)
Article •09/24/2022
Indexers are a syntactic convenience that enable you to create a class , struct , or interface
that client applications can access as an array. The compiler will generate an Item
property (or an alternatively named property if IndexerNameAttribute  is present), and
the appropriate accessor methods. Indexers are most frequently implemented in types
whose primary purpose is to encapsulate an internal collection or array. For example,
suppose you have a class TempRecord that represents the temperature in F ahrenheit as
recorded at 10 different times during a 24-hour period. The class contains a temps array
of type float[] to store the temperature values. By implementing an indexer in this
class, clients can access the temperatures in a TempRecord instance as float temp =
tempRecord[4] instead of as float temp = tempRecord.temps[4]. The indexer notation
not only simplifies the syntax for client applications; it also makes the class, and its
purpose more intuitive for other developers to understand.
To declare an indexer on a class or struct, use the this keyword, as the following example
shows:
C#
The type of an indexer and the type of its parameters must be at least as accessible as
the indexer itself. For more information about accessibility levels, see Access Modifiers .// Indexer declaration
public int this[int index]
{
    // get and set accessors
}
） Impor tant
Declaring an indexer will automatically generate a property named Item on the
object. The Item property is not directly accessible from the instance member
access expr ession . Additionally, if you add your own Item property to an object
with an indexer, you'll get a CS0102 compiler err or. To avoid this error, use the
Index erNameA ttribut e rename the indexer as detailed below.
RemarksFor more information about how to use indexers with an interface, see Interface
Indexers .
The signature of an indexer consists of the number and types of its formal parameters. It
doesn't include the indexer type or the names of the formal parameters. If you declare
more than one indexer in the same class, they must have different signatures.
An indexer is not classified as a variable; therefore, an indexer value cannot be passed by
reference (as a ref or out parameter) unless its value is a reference (i.e., it returns by
reference.)
To provide the indexer with a name that other languages can use, use
System.Runtime.CompilerServices.IndexerNameAttribute , as the following example
shows:
C#
This indexer will have the name TheItem, as it is overridden by the indexer name
attribute. By default, the indexer name is Item.
The following example shows how to declare a private array field, temps, and an indexer.
The indexer enables direct access to the instance tempRecord[i]. The alternative to using
the indexer is to declare the array as a public  member and access its members,
tempRecord.temps[i], directly.
C#// Indexer declaration
[System.Runtime.CompilerServices.IndexerName( "TheItem" )]
public int this[int index]
{
    // get and set accessors
}
Example 1
public class TempRecord
{
    // Array of temperature values
    float[] temps = new float[10]
    {
        56.2F, 56.7F, 56.5F, 56.9F, 58.8F,
        61.3F, 65.9F, 62.1F, 59.2F, 57.5F
    };
    // To enable client code to validate inputNotice that when an indexer's access is evaluated, for example, in a Console.Write
statement, the get accessor is invoked. Therefore, if no get accessor exists, a compile-
time error occurs.
C#    // when accessing your indexer.
    public int Length => temps.Length;
    
    // Indexer declaration.
    // If index is out of range, the temps array will throw the exception.
    public float this[int index]
    {
        get => temps[index];
        set => temps[index] = value;
    }
}
class Program
{
    static void Main()
    {
        var tempRecord = new TempRecord();
        // Use the indexer's set accessor
        tempRecord[ 3] = 58.3F;
        tempRecord[ 5] = 60.1F;
        // Use the indexer's get accessor
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine( $"Element # {i} = {tempRecord[i]} ");
        }
        // Keep the console window open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
    /* Output:
        Element #0 = 56.2
        Element #1 = 56.7
        Element #2 = 56.5
        Element #3 = 58.3
        Element #4 = 58.8
        Element #5 = 60.1
        Element #6 = 65.9
        Element #7 = 62.1
        Element #8 = 59.2
        Element #9 = 57.5
    */
}C# doesn't limit the indexer parameter type to integer. For example, it may be useful to
use a string with an indexer. Such an indexer might be implemented by searching for
the string in the collection, and returning the appropriate value. As accessors can be
overloaded, the string and integer versions can coexist.
The following example declares a class that stores the days of the week. A get accessor
takes a string, the name of a day, and returns the corresponding integer. For example,
"Sunday" returns 0, "Monday" returns 1, and so on.
C#
C#Indexing using other values
Example 2
// Using a string as an indexer value
class DayCollection
{
    string[] days = { "Sun", "Mon", "Tues", "Wed", "Thurs", "Fri", "Sat" };
    // Indexer with only a get accessor with the expression-bodied  
definition:
    public int this[string day] => FindDayIndex(day);
    private int FindDayIndex (string day)
    {
        for (int j = 0; j < days.Length; j++)
        {
            if (days[j] == day)
            {
                return j;
            }
        }
        throw new ArgumentOutOfRangeException(
            nameof(day),
            $"Day {day} is not supported.\nDay input must be in the form  
\"Sun\", \"Mon\", etc" );
    }
}
Consuming example 2
class Program
{The following example declares a class that stores the days of the week using the
System.DayOfW eek enum. A get accessor takes a DayOfWeek, the value of a day, and
returns the corresponding integer. For example, DayOfWeek.Sunday returns 0,
DayOfWeek.Monday returns 1, and so on.
C#    static void Main(string[] args)
    {
        var week = new DayCollection();
        Console.WriteLine(week[ "Fri"]);
        try
        {
            Console.WriteLine(week[ "Made-up day" ]);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine( $"Not supported input: {e.Message} ");
        }
    }
    // Output:
    // 5
    // Not supported input: Day Made-up day is not supported.
    // Day input must be in the form "Sun", "Mon", etc (Parameter 'day')
}
Example 3
using Day = System.DayOfWeek;
class DayOfWeekCollection
{
    Day[] days =
    {
        Day.Sunday, Day.Monday, Day.Tuesday, Day.Wednesday,
        Day.Thursday, Day.Friday, Day.Saturday
    };
    // Indexer with only a get accessor with the expression-bodied  
definition:
    public int this[Day day] => FindDayIndex(day);
    private int FindDayIndex (Day day)
    {
        for (int j = 0; j < days.Length; j++)
        {
            if (days[j] == day)
            {
                return j;C#
There are two main ways in which the security and reliability of indexers can be
improved:
Be sure to incorporate some type of error-handling strategy to handle the chance
of client code passing in an invalid index value. In the first example earlier in this
topic, the T empR ecord class provides a Length property that enables the client
code to verify the input before passing it to the indexer. Y ou can also put the error
handling code inside the indexer itself. Be sure to document for users any
exceptions that you throw inside an indexer accessor.            }
        }
        throw new ArgumentOutOfRangeException(
            nameof(day),
            $"Day {day} is not supported.\nDay input must be a defined  
System.DayOfWeek value." );
    }
}
Consuming example 3
class Program
{
    static void Main()
    {
        var week = new DayOfWeekCollection();
        Console.WriteLine(week[DayOfWeek.Friday]);
        try
        {
            Console.WriteLine(week[(DayOfWeek) 43]);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine( $"Not supported input: {e.Message} ");
        }
    }
    // Output:
    // 5
    // Not supported input: Day 43 is not supported.
    // Day input must be a defined System.DayOfWeek value. (Parameter 'day')
}
Robust programmingSet the accessibility of the get and set accessors to be as restrictive as is
reasonable. This is important for the set accessor in particular. For more
information, see Restricting Accessor Accessibility .
C# Programming Guide
Indexers
PropertiesSee also
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
 Provide product feedbackIndexers in Interfaces (C# Programming
Guide)
Article •09/15/2021
Indexers can be declared on an interface . Accessors of interface indexers differ from the
accessors of class  indexers in the following ways:
Interface accessors do not use modifiers.
An interface accessor typically does not have a body.
The purpose of the accessor is to indicate whether the indexer is read-write, read-only,
or write-only. Y ou may provide an implementation for an indexer defined in an interface,
but this is rare. Indexers typically define an API to access data fields, and data fields
cannot be defined in an interface.
The following is an example of an interface indexer accessor:
C#
The signature of an indexer must differ from the signatures of all other indexers
declared in the same interface.
The following example shows how to implement interface indexers.
C#public interface  ISomeInterface  
{ 
    //... 
    // Indexer declaration:  
    string this[int index] 
    { 
        get; 
        set; 
    } 
} 
Example
// Indexer on an interface:  
public interface  IIndexInterface  
{ 
    // Indexer declaration:  C#
In the preceding example, you could use the explicit interface member implementation
by using the fully qualified name of the interface member. For example
C#    int this[int index] 
    { 
        get; 
        set; 
    } 
} 
// Implementing the interface.  
class IndexerClass  : IIndexInterface  
{ 
    private int[] arr = new int[100]; 
    public int this[int index]   // indexer declaration  
    { 
        // The arr object will throw IndexOutOfRange exception.  
        get => arr[index];  
        set => arr[index] = value; 
    } 
} 
IndexerClass test = new IndexerClass();  
System.Random rand = System.Random.Shared;  
// Call the indexer to initialize its elements.  
for (int i = 0; i < 10; i++) 
{ 
    test[i] = rand.Next();  
} 
for (int i = 0; i < 10; i++) 
{ 
    System.Console.WriteLine( $"Element # {i} = {test[i]} "); 
} 
/* Sample output:  
    Element #0 = 360877544  
    Element #1 = 327058047  
    Element #2 = 1913480832  
    Element #3 = 1519039937  
    Element #4 = 601472233  
    Element #5 = 323352310  
    Element #6 = 1422639981  
    Element #7 = 1797892494  
    Element #8 = 875761049  
    Element #9 = 393083859  
*/ However, the fully qualified name is only needed to avoid ambiguity when the class is
implementing more than one interface with the same indexer signature. For example, if
an Employee class is implementing two interfaces, ICitizen and IEmployee, and both
interfaces have the same indexer signature, the explicit interface member
implementation is necessary. That is, the following indexer declaration:
C#
implements the indexer on the IEmployee interface, while the following declaration:
C#
implements the indexer on the ICitizen interface.
C# Programming Guide
Indexers
Properties
Interfacesstring IIndexInterface. this[int index] 
{ 
} 
string IEmployee. this[int index] 
{ 
} 
string ICitizen. this[int index] 
{ 
} 
See alsoComparison Between Properties and
Indexers (C# Programming Guide)
Article •09/15/2021
Indexers are like properties. Except for the differences shown in the following table, all
the rules that are defined for property accessors apply to indexer accessors also.
Proper ty Index er
Allows methods to be called as if
they were public data members.Allows elements of an internal collection of an object to be
accessed by using array notation on the object itself.
Accessed through a simple name. Accessed through an index.
Can be a static or an instance
member.Must be an instance member.
A get accessor of a property has
no parameters.A get accessor of an indexer has the same formal
parameter list as the indexer.
A set accessor of a property
contains the implicit value
parameter.A set accessor of an indexer has the same formal
parameter list as the indexer, and also to the value
parameter.
Supports shortened syntax with
Auto-Implemented Properties .Supports expression bodied members for get only indexers.
C# Programming Guide
Indexers
PropertiesSee alsoEvents (C# Programming Guide)
Article •04/12/2023
Events enable a class  or object to notify other classes or objects when something of
interest occurs. The class that sends (or raises) the event is called the publisher  and the
classes that receive (or handle ) the event are called subscribers.
In a typical C# Windows Forms or W eb application, you subscribe to events raised by
controls such as buttons and list boxes. Y ou can use the Visual C# integrated
development environment (IDE) to browse the events that a control publishes and select
the ones that you want to handle. The IDE provides an easy way to automatically add an
empty event handler method and the code to subscribe to the event. For more
information, see How to subscribe to and unsubscribe from events .
Events have the following properties:
The publisher determines when an event is raised; the subscribers determine what
action is taken in response to the event.
An event can have multiple subscribers. A subscriber can handle multiple events
from multiple publishers.
Events that have no subscribers are never raised.
Events are typically used to signal user actions such as button clicks or menu
selections in graphical user interfaces.
When an event has multiple subscribers, the event handlers are invoked
synchronously when an event is raised. T o invoke events asynchronously, see
Calling S ynchronous Methods Asynchronously .
In the .NET class library, events are based on the EventHandler  delegate and the
EventArgs  base class.
For more information, see:
How to subscribe to and unsubscribe from eventsEvents Overview
Related SectionsHow to publish events that conform to .NET Guidelines
How to raise base class events in derived classes
How to implement interface events
How to implement custom event accessors
For more information, see Events  in the C# Language Specification . The language
specification is the definitive source for C# syntax and usage.
EventHandler
C# Programming Guide
Delegates
Creating Event Handlers in Windows FormsC# Language Specification
See alsoHow to subscribe to and unsubscribe
from ev ents (C# Programming Guide)
Article •10/12/2021
You subscribe to an event that is published by another class when you want to write
custom code that is called when that event is raised. For example, you might subscribe
to a button's click event in order to make your application do something useful when
the user clicks the button.
1. If you cannot see the Proper ties window, in Design  view, right-click the form or
control for which you want to create an event handler, and select Proper ties.
2. On top of the Proper ties window, click the Events icon.
3. Double-click the event that you want to create, for example the Load event.
Visual C# creates an empty event handler method and adds it to your code.
Alternatively you can add the code manually in Code  view. For example, the
following lines of code declare an event handler method that will be called when
the Form class raises the Load event.
C#
The line of code that is required to subscribe to the event is also automatically
generated in the InitializeComponent method in the Form1.Designer.cs file in your
project. It resembles this:
C#To subscribe to events by using the Visual Studio IDE
private void Form1_Load (object sender, System.EventArgs e ) 
{ 
    // Add your form load event handling code here.  
} 
this.Load += new System.EventHandler( this.Form1_Load);  
To subscribe to events programmatically1. Define an event handler method whose signature matches the delegate signature
for the event. For example, if the event is based on the EventHandler  delegate
type, the following code represents the method stub:
C#
2. Use the addition assignment operator ( +=) to attach an event handler to the event.
In the following example, assume that an object named publisher has an event
named RaiseCustomEvent. Note that the subscriber class needs a reference to the
publisher class in order to subscribe to its events.
C#
You can also use a lambda expression  to specify an event handler:
C#
If you don't have to unsubscribe from an event later, you can use the addition
assignment operator ( +=) to attach an anonymous function as an event handler. In the
following example, assume that an object named publisher has an event named
RaiseCustomEvent and that a CustomEventArgs class has also been defined to carry some
kind of specialized event information. Note that the subscriber class needs a reference
to publisher in order to subscribe to its events.
C#void HandleCustomEvent (object sender, CustomEventArgs a )   
{   
   // Do something useful here.   
}   
publisher.RaiseCustomEvent += HandleCustomEvent;   
public Form1()   
{   
    InitializeComponent();   
    this.Click += (s,e) =>  
        {  
            MessageBox.Show(((MouseEventArgs)e).Location.ToString());  
        };  
}   
To subscribe to events by using an anonymous functionYou cannot easily unsubscribe from an event if you used an anonymous function to
subscribe to it. T o unsubscribe in this scenario, go back to the code where you subscribe
to the event, store the anonymous function in a delegate variable, and then add the
delegate to the event. W e recommend that you don't use anonymous functions to
subscribe to events if you have to unsubscribe from the event at some later point in
your code. For more information about anonymous functions, see Lambda expressions .
To prevent your event handler from being invoked when the event is raised, unsubscribe
from the event. In order to prevent resource leaks, you should unsubscribe from events
before you dispose of a subscriber object. Until you unsubscribe from an event, the
multicast delegate that underlies the event in the publishing object has a reference to
the delegate that encapsulates the subscriber's event handler. As long as the publishing
object holds that reference, garbage collection will not delete your subscriber object.
Use the subtraction assignment operator ( -=) to unsubscribe from an event:
C#
When all subscribers have unsubscribed from an event, the event instance in the
publisher class is set to null.
Events
event
How to publish events that conform to .NET Guidelines
- and -= operators
+ and += operatorspublisher.RaiseCustomEvent += ( object o, CustomEventArgs e) =>  
{   
  string s = o.ToString() + " " + e.ToString();   
  Console.WriteLine(s);   
};   
Unsubscribing
To unsubscribe from an event
publisher.RaiseCustomEvent -= HandleCustomEvent;   
See alsoHow to publish events that conform to
.NET Guidelines (C# Programming
Guide)
Article •09/15/2021
The following procedure demonstrates how to add events that follow the standard .NET
pattern to your classes and structs. All events in the .NET class library are based on the
EventHandler  delegate, which is defined as follows:
C#
Although events in classes that you define can be based on any valid delegate type,
even delegates that return a value, it is generally recommended that you base your
events on the .NET pattern by using EventHandler , as shown in the following example.
The name EventHandler can lead to a bit of confusion as it doesn't actually handle the
event. The EventHandler , and generic EventHandler<TEventArgs>  are delegate types. A
method or lambda expression whose signature matches the delegate definition is the
event handler  and will be invoked when the event is raised.
1. (Skip this step and go to S tep 3a if you do not have to send custom data with your
event.) Declare the class for your custom data at a scope that is visible to both
your publisher and subscriber classes. Then add the required members to hold
your custom event data. In this example, a simple string is returned.
C#public delegate  void EventHandler (object sender, EventArgs e ); 
７ Note
.NET Framework 2.0 introduces a generic version of this delegate,
EventHandler<TEv entAr gs>. The following examples show how to use both
versions.
Publish events based on the EventHandler
pattern2. (Skip this step if you are using the generic version of EventHandler<TEventArgs> .)
Declare a delegate in your publishing class. Give it a name that ends with
EventHandler. The second parameter specifies your custom EventArgs type.
C#
3. Declare the event in your publishing class by using one of the following steps.
a. If you have no custom EventArgs class, your Event type will be the non-generic
EventHandler delegate. Y ou do not have to declare the delegate because it is
already declared in the System  namespace that is included when you create
your C# project. Add the following code to your publisher class.
C#
b. If you are using the non-generic version of EventHandler  and you have a
custom class derived from EventArgs , declare your event inside your publishing
class and use your delegate from step 2 as the type.
C#
c. If you are using the generic version, you do not need a custom delegate.
Instead, in your publishing class, you specify your event type as
EventHandler<CustomEventArgs>, substituting the name of your own class
between the angle brackets.
C#public class CustomEventArgs  : EventArgs  
{ 
    public CustomEventArgs (string message ) 
    { 
        Message = message;  
    } 
    public string Message { get; set; } 
} 
public delegate  void CustomEventHandler (object sender, CustomEventArgs  
args); 
public event EventHandler RaiseCustomEvent;  
public event CustomEventHandler RaiseCustomEvent;  The following example demonstrates the previous steps by using a custom EventArgs
class and EventHandler<TEventArgs>  as the event type.
C#public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
Example
using System;  
namespace  DotNetEvents  
{ 
    // Define a class to hold custom event info  
    public class CustomEventArgs  : EventArgs  
    { 
        public CustomEventArgs (string message ) 
        {  
            Message = message;  
        }  
        public string Message { get; set; } 
    } 
    // Class that publishes an event  
    class Publisher  
    { 
        // Declare the event using EventHandler<T>  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        public void DoSomething () 
        {  
            // Write some code that does something useful here  
            // then raise the event. You can also raise an event  
            // before you execute a block of code.  
            OnRaiseCustomEvent( new CustomEventArgs( "Event triggered" )); 
        }  
        // Wrap event invocations inside a protected virtual method  
        // to allow derived classes to override the event invocation  
behavior  
        protected  virtual void OnRaiseCustomEvent (CustomEventArgs e ) 
        {  
            // Make a temporary copy of the event to avoid possibility of  
            // a race condition if the last subscriber unsubscribes  
            // immediately after the null check and before the event is  
raised. 
            EventHandler<CustomEventArgs> raiseEvent = RaiseCustomEvent;  
            // Event will be null if there are no subscribers              if (raiseEvent != null) 
            {  
                // Format the string to send inside the CustomEventArgs  
parameter  
                e.Message += $" at {DateTime.Now} "; 
                // Call to raise the event.  
                raiseEvent( this, e); 
            }  
        }  
    } 
    //Class that subscribes to an event  
    class Subscriber  
    { 
        private readonly  string _id; 
        public Subscriber (string id, Publisher pub ) 
        {  
            _id = id;  
            // Subscribe to the event  
            pub.RaiseCustomEvent += HandleCustomEvent;  
        }  
        // Define what actions to take when the event is raised.  
        void HandleCustomEvent (object sender, CustomEventArgs e ) 
        {  
            Console.WriteLine( $"{_id} received this message: {e.Message} "); 
        }  
    } 
    class Program 
    { 
        static void Main() 
        {  
            var pub = new Publisher();  
            var sub1 = new Subscriber( "sub1", pub); 
            var sub2 = new Subscriber( "sub2", pub); 
            // Call the method that raises the event.  
            pub.DoSomething();  
            // Keep the console window open  
            Console.WriteLine( "Press any key to continue..." ); 
            Console.ReadLine();  
        }  
    } 
} 
See alsoDelegate
C# Programming Guide
Events
DelegatesHow to raise base class events in
derived classes (C# Programming Guide)
Article •09/15/2021
The following simple example shows the standard way to declare events in a base class
so that they can also be raised from derived classes. This pattern is used extensively in
Windows Forms classes in the .NET class libraries.
When you create a class that can be used as a base class for other classes, you should
consider the fact that events are a special type of delegate that can only be invoked
from within the class that declared them. Derived classes cannot directly invoke events
that are declared within the base class. Although sometimes you may want an event that
can only be raised by the base class, most of the time, you should enable the derived
class to invoke base class events. T o do this, you can create a protected invoking
method in the base class that wraps the event. By calling or overriding this invoking
method, derived classes can invoke the event indirectly.
C#７ Note
Do not declare virtual events in a base class and override them in a derived class.
The C# compiler does not handle these correctly and it is unpredictable whether a
subscriber to the derived event will actually be subscribing to the base class event.
Example
namespace  BaseClassEvents  
{ 
    // Special EventArgs class to hold info about Shapes.  
    public class ShapeEventArgs  : EventArgs  
    { 
        public ShapeEventArgs (double area) 
        {  
            NewArea = area;  
        }  
        public double NewArea { get; } 
    } 
    // Base class event publisher    public abstract  class Shape 
    { 
        protected  double _area; 
        public double Area 
        {  
            get => _area;  
            set => _area = value; 
        }  
        // The event. Note that by using the generic EventHandler<T> event  
type 
        // we do not need to declare a separate delegate type.  
        public event EventHandler<ShapeEventArgs> ShapeChanged;  
        public abstract  void Draw(); 
        //The event-invoking method that derived classes can override.  
        protected  virtual void OnShapeChanged (ShapeEventArgs e ) 
        {  
            // Safely raise the event for all subscribers  
            ShapeChanged?.Invoke( this, e); 
        }  
    } 
    public class Circle : Shape 
    { 
        private double _radius;  
        public Circle(double radius) 
        {  
            _radius = radius;  
            _area = 3.14 * _radius * _radius;  
        }  
        public void Update(double d) 
        {  
            _radius = d;  
            _area = 3.14 * _radius * _radius;  
            OnShapeChanged( new ShapeEventArgs(_area));  
        }  
        protected  override  void OnShapeChanged (ShapeEventArgs e ) 
        {  
            // Do any circle-specific processing here.  
            // Call the base class event invocation method.  
            base.OnShapeChanged(e);  
        }  
        public override  void Draw() 
        {  
            Console.WriteLine( "Drawing a circle" ); 
        }  
    }     public class Rectangle  : Shape 
    { 
        private double _length;  
        private double _width;  
        public Rectangle (double length, double width) 
        {  
            _length = length;  
            _width = width;  
            _area = _length * _width;  
        }  
        public void Update(double length, double width) 
        {  
            _length = length;  
            _width = width;  
            _area = _length * _width;  
            OnShapeChanged( new ShapeEventArgs(_area));  
        }  
        protected  override  void OnShapeChanged (ShapeEventArgs e ) 
        {  
            // Do any rectangle-specific processing here.  
            // Call the base class event invocation method.  
            base.OnShapeChanged(e);  
        }  
        public override  void Draw() 
        {  
            Console.WriteLine( "Drawing a rectangle" ); 
        }  
    } 
    // Represents the surface on which the shapes are drawn  
    // Subscribes to shape events so that it knows  
    // when to redraw a shape.  
    public class ShapeContainer  
    { 
        private readonly  List<Shape> _list;  
        public ShapeContainer () 
        {  
            _list = new List<Shape>();  
        }  
        public void AddShape (Shape shape ) 
        {  
            _list.Add(shape);  
            // Subscribe to the base class event.  
            shape.ShapeChanged += HandleShapeChanged;  
        }  C# Programming Guide
Events
Delegates        // ...Other methods to draw, resize, etc.  
        private void HandleShapeChanged (object sender, ShapeEventArgs e ) 
        {  
            if (sender is Shape shape)  
            {  
                // Diagnostic message for demonstration purposes.  
                Console.WriteLine( $"Received event. Shape area is now  
{e.NewArea} "); 
                // Redraw the shape here.  
                shape.Draw();  
            }  
        }  
    } 
    class Test 
    { 
        static void Main() 
        {  
            //Create the event publishers and subscriber  
            var circle = new Circle( 54); 
            var rectangle = new Rectangle( 12, 9); 
            var container = new ShapeContainer();  
            // Add the shapes to the container.  
            container.AddShape(circle);  
            container.AddShape(rectangle);  
            // Cause some events to be raised.  
            circle.Update( 57); 
            rectangle.Update( 7, 7); 
            // Keep the console window open in debug mode.  
            Console.WriteLine( "Press any key to continue..." ); 
            Console.ReadKey();  
        }  
    } 
} 
/* Output:  
        Received event. Shape area is now 10201.86  
        Drawing a circle  
        Received event. Shape area is now 49  
        Drawing a rectangle  
 */ 
See alsoAccess Modifiers
Creating Event Handlers in Windows FormsHow to implement interface events (C#
Programming Guide)
Article •09/15/2021
An interface  can declare an event . The following example shows how to implement
interface events in a class. Basically the rules are the same as when you implement any
interface method or property.
Declare the event in your class and then invoke it in the appropriate areas.
C#To implement interface events in a class
namespace  ImplementInterfaceEvents    
{   
    public interface  IDrawingObject    
    {   
        event EventHandler ShapeChanged;   
    }   
    public class MyEventArgs  : EventArgs  
    {   
        // class members   
    }   
    public class Shape : IDrawingObject    
    {   
        public event EventHandler ShapeChanged;   
        void ChangeShape ()   
        {   
            // Do something here before the event…   
            OnShapeChanged( new MyEventArgs( /*arguments*/ ));   
            // or do something here after the event.  
        }   
        protected  virtual void OnShapeChanged (MyEventArgs e )   
        {   
            ShapeChanged?.Invoke( this, e);   
        }   
    }   
}   
ExampleThe following example shows how to handle the less-common situation in which your
class inherits from two or more interfaces and each interface has an event with the same
name. In this situation, you must provide an explicit interface implementation for at least
one of the events. When you write an explicit interface implementation for an event, you
must also write the add and remove event accessors. Normally these are provided by the
compiler, but in this case the compiler cannot provide them.
By providing your own accessors, you can specify whether the two events are
represented by the same event in your class, or by different events. For example, if the
events should be raised at different times according to the interface specifications, you
can associate each event with a separate implementation in your class. In the following
example, subscribers determine which OnDraw event they will receive by casting the
shape reference to either an IShape or an IDrawingObject.
C#
namespace  WrapTwoInterfaceEvents  
{ 
    using System;  
    public interface  IDrawingObject  
    { 
        // Raise this event before drawing  
        // the object.  
        event EventHandler OnDraw;  
    } 
    public interface  IShape 
    { 
        // Raise this event after drawing  
        // the shape.  
        event EventHandler OnDraw;  
    } 
    // Base class event publisher inherits two  
    // interfaces, each with an OnDraw event  
    public class Shape : IDrawingObject , IShape 
    { 
        // Create an event for each interface event  
        event EventHandler PreDrawEvent;  
        event EventHandler PostDrawEvent;  
        object objectLock = new Object();  
        // Explicit interface implementation required.  
        // Associate IDrawingObject's event with  
        // PreDrawEvent  
        #region IDrawingObjectOnDraw  
        event EventHandler IDrawingObject.OnDraw  
        {  
            add             {  
                lock (objectLock)
                {  
                    PreDrawEvent += value; 
                }  
            }  
            remove 
            {  
                lock (objectLock)
                {  
                    PreDrawEvent -= value; 
                }  
            }  
        }  
        #endregion  
        // Explicit interface implementation required.  
        // Associate IShape's event with  
        // PostDrawEvent  
        event EventHandler IShape.OnDraw  
        {  
            add 
            {  
                lock (objectLock)
                {  
                    PostDrawEvent += value; 
                }  
            }  
            remove 
            {  
                lock (objectLock)
                {  
                    PostDrawEvent -= value; 
                }  
            }  
        }  
        // For the sake of simplicity this one method  
        // implements both interfaces.  
        public void Draw() 
        {  
            // Raise IDrawingObject's event before the object is drawn.  
            PreDrawEvent?.Invoke( this, EventArgs.Empty);  
            Console.WriteLine( "Drawing a shape." ); 
            // Raise IShape's event after the object is drawn.  
            PostDrawEvent?.Invoke( this, EventArgs.Empty);  
        }  
    } 
    public class Subscriber1  
    { 
        // References the shape object as an IDrawingObject  
        public Subscriber1 (Shape shape ) 
        {  
            IDrawingObject d = (IDrawingObject)shape;  C# Programming Guide
Events
Delegates
Explicit Interface Implementation
How to raise base class events in derived classes            d.OnDraw += d_OnDraw;
        }  
        void d_OnDraw (object sender, EventArgs e ) 
        {  
            Console.WriteLine( "Sub1 receives the IDrawingObject event." ); 
        }  
    } 
    // References the shape object as an IShape  
    public class Subscriber2  
    { 
        public Subscriber2 (Shape shape ) 
        {  
            IShape d = (IShape)shape;  
            d.OnDraw += d_OnDraw;
        }  
        void d_OnDraw (object sender, EventArgs e ) 
        {  
            Console.WriteLine( "Sub2 receives the IShape event." ); 
        }  
    } 
    public class Program 
    { 
        static void Main(string[] args) 
        {  
            Shape shape = new Shape();  
            Subscriber1 sub = new Subscriber1(shape);  
            Subscriber2 sub2 = new Subscriber2(shape);  
            shape.Draw();  
            // Keep the console window open in debug mode.  
            System.Console.WriteLine( "Press any key to exit." ); 
            System.Console.ReadKey();  
        }  
    } 
} 
/* Output:  
    Sub1 receives the IDrawingObject event.  
    Drawing a shape.  
    Sub2 receives the IShape event.  
*/ 
See alsoHow to implement custom event
accessors (C# Programming Guide)
Article •09/15/2021
An event is a special kind of multicast delegate that can only be invoked from within the
class that it is declared in. Client code subscribes to the event by providing a reference
to a method that should be invoked when the event is fired. These methods are added
to the delegate's invocation list through event accessors, which resemble property
accessors, except that event accessors are named add and remove. In most cases, you
do not have to supply custom event accessors. When no custom event accessors are
supplied in your code, the compiler will add them automatically. However, in some cases
you may have to provide custom behavior. One such case is shown in the topic How to
implement interface events .
The following example shows how to implement custom add and remove event
accessors. Although you can substitute any code inside the accessors, we recommend
that you lock the event before you add or remove a new event handler method.
C#Example
event EventHandler IDrawingObject.OnDraw  
{ 
    add 
    { 
        lock (objectLock)  
        {  
            PreDrawEvent += value; 
        }  
    } 
    remove 
    { 
        lock (objectLock)  
        {  
            PreDrawEvent -= value; 
        }  
    } 
} 
See alsoEvents
eventGeneric type parameters (C#
Programming Guide)
Article •08/01/2023
In a generic type or method definition, a type parameter is a placeholder for a specific
type that a client specifies when they create an instance of the generic type. A generic
class, such as GenericList<T> listed in Introduction to Generics , cannot be used as-is
because it is not really a type; it is more like a blueprint for a type. T o use
GenericList<T>, client code must declare and instantiate a constructed type by
specifying a type argument inside the angle brackets. The type argument for this
particular class can be any type recognized by the compiler. Any number of constructed
type instances can be created, each one using a different type argument, as follows:
C#
In each of these instances of GenericList<T>, every occurrence of T in the class is
substituted at run time with the type argument. By means of this substitution, we have
created three separate type-safe and efficient objects using a single class definition. For
more information on how this substitution is performed by the CLR, see Generics in the
Runtime .
You can learn the naming conventions for generic type parameters in the article on
naming conventions .
System.Collections.Generic
C# Programming Guide
Generics
Differences Between C++ T emplates and C# GenericsGenericList< float> list1 = new GenericList< float>();
GenericList<ExampleClass> list2 = new GenericList<ExampleClass>();
GenericList<ExampleStruct> list3 = new GenericList<ExampleStruct>();
See alsoConstraints on type parameters (C#
Programming Guide)
Article •11/15/2022
Constraints inform the compiler about the capabilities a type argument must have.
Without any constraints, the type argument could be any type. The compiler can only
assume the members of System.Object , which is the ultimate base class for any .NET
type. For more information, see Why use constraints . If client code uses a type that
doesn't satisfy a constraint, the compiler issues an error. Constraints are specified by
using the where contextual keyword. The following table lists the various types of
constraints:
Constraint Descr iption
where T :
structThe type argument must be a non-nullable value type . For information about
nullable value types, see Nullable value types . Because all value types have an
accessible parameterless constructor, the struct constraint implies the new()
constraint and can't be combined with the new() constraint. Y ou can't combine
the struct constraint with the unmanaged constraint.
where T :
classThe type argument must be a reference type. This constraint applies also to any
class, interface, delegate, or array type. In a nullable context, T must be a non-
nullable reference type.
where T :
class?The type argument must be a reference type, either nullable or non-nullable.
This constraint applies also to any class, interface, delegate, or array type.
where T :
notnullThe type argument must be a non-nullable type. The argument can be a non-
nullable reference type or a non-nullable value type.
where T :
defaultThis constraint resolves the ambiguity when you need to specify an
unconstrained type parameter when you override a method or provide an
explicit interface implementation. The default constraint implies the base
method without either the class or struct constraint. For more information,
see the default  constraint  spec proposal.
where T :
unmanagedThe type argument must be a non-nullable unmanaged type . The unmanaged
constraint implies the struct constraint and can't be combined with either the
struct or new() constraints.
where T :
new()The type argument must have a public parameterless constructor. When used
together with other constraints, the new() constraint must be specified last. The
new() constraint can't be combined with the struct and unmanaged constraints.
where T :
<base classThe type argument must be or derive from the specified base class. In a nullable
context, T must be a non-nullable reference type derived from the specifiedConstraint Descr iption
name> base class.
where T :
<base class
name>?The type argument must be or derive from the specified base class. In a nullable
context, T may be either a nullable or non-nullable type derived from the
specified base class.
where T :
<interface
name>The type argument must be or implement the specified interface. Multiple
interface constraints can be specified. The constraining interface can also be
generic. In a nullable context, T must be a non-nullable type that implements
the specified interface.
where T :
<interface
name>?The type argument must be or implement the specified interface. Multiple
interface constraints can be specified. The constraining interface can also be
generic. In a nullable context, T may be a nullable reference type, a non-nullable
reference type, or a value type. T may not be a nullable value type.
where T : U The type argument supplied for T must be or derive from the argument
supplied for U. In a nullable context, if U is a non-nullable reference type, T
must be non-nullable reference type. If U is a nullable reference type, T may be
either nullable or non-nullable.
Constraints specify the capabilities and expectations of a type parameter. Declaring
those constraints means you can use the operations and method calls of the
constraining type. If your generic class or method uses any operation on the generic
members beyond simple assignment or calling any methods not supported by
System.Object , you'll apply constraints to the type parameter. For example, the base
class constraint tells the compiler that only objects of this type or derived from this type
will be used as type arguments. Once the compiler has this guarantee, it can allow
methods of that type to be called in the generic class. The following code example
demonstrates the functionality you can add to the GenericList<T> class (in Introduction
to Generics ) by applying a base class constraint.
C#Why use constraints
public class Employee
{
    public Employee (string name, int id) => (Name, ID) = (name, id);
    public string Name { get; set; }
    public int ID { get; set; }
}
public class GenericList <T> where T : Employee
{The constraint enables the generic class to use the Employee.Name property. The
constraint specifies that all items of type T are guaranteed to be either an Employee
object or an object that inherits from Employee.    private class Node
    {
        public Node(T t) => (Next, Data) = ( null, t);
        public Node? Next { get; set; }
        public T Data { get; set; }
    }
    private Node? head;
    public void AddHead(T t)
    {
        Node n = new Node(t) { Next = head };
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
    public T? FindFirstOccurrence( string s)
    {
        Node? current = head;
        T? t = null;
        while (current != null)
        {
            //The constraint enables access to the Name property.
            if (current.Data.Name == s)
            {
                t = current.Data;
                break;
            }
            else
            {
                current = current.Next;
            }
        }
        return t;
    }
}Multiple constraints can be applied to the same type parameter, and the constraints
themselves can be generic types, as follows:
C#
When applying the where T : class constraint, avoid the == and != operators on the
type parameter because these operators will test for reference identity only, not for
value equality. This behavior occurs even if these operators are overloaded in a type that
is used as an argument. The following code illustrates this point; the output is false even
though the String  class overloads the == operator.
C#
The compiler only knows that T is a reference type at compile time and must use the
default operators that are valid for all reference types. If you must test for value equality,
the recommended way is to also apply the where T : IEquatable<T> or where T :
IComparable<T> constraint and implement the interface in any class that will be used to
construct the generic class.
You can apply constraints to multiple parameters, and multiple constraints to a single
parameter, as shown in the following example:
C#class EmployeeList <T> where T : Employee , IEmployee , System.IComparable <T>, 
new()
{
    // ...
}
public static void OpEqualsTest<T>(T s, T t) where T : class
{
    System.Console.WriteLine(s == t);
}
private static void TestStringEquality ()
{
    string s1 = "target" ;
    System.Text.StringBuilder sb = new System.Text.StringBuilder( "target" );
    string s2 = sb.ToString();
    OpEqualsTest< string>(s1, s2);
}
Constraining  multip le parametersType parameters that have no constraints, such as T in public class SampleClass<T>{},
are called unbounded type parameters. Unbounded type parameters have the following
rules:
The != and == operators can't be used because there's no guarantee that the
concrete type argument will support these operators.
They can be converted to and from System.Object or explicitly converted to any
interface type.
You can compare them to null. If an unbounded parameter is compared to null,
the comparison will always return false if the type argument is a value type.
The use of a generic type parameter as a constraint is useful when a member function
with its own type parameter has to constrain that parameter to the type parameter of
the containing type, as shown in the following example:
C#
In the previous example, T is a type constraint in the context of the Add method, and an
unbounded type parameter in the context of the List class.
Type parameters can also be used as constraints in generic class definitions. The type
parameter must be declared within the angle brackets together with any other type
parameters:
C#class Base { }
class Test<T, U>
    where U : struct
    where T : Base, new()
{ }
Unbounded type parameters
Type parameters as constraints
public class List<T>
{
    public void Add<U>(List<U> items) where U : T { /*...*/}
}The usefulness of type parameters as constraints with generic classes is limited because
the compiler can assume nothing about the type parameter except that it derives from
System.Object. Use type parameters as constraints on generic classes in scenarios in
which you want to enforce an inheritance relationship between two type parameters.
You can use the notnull constraint to specify that the type argument must be a non-
nullable value type or non-nullable reference type. Unlike most other constraints, if a
type argument violates the notnull constraint, the compiler generates a warning
instead of an error.
The notnull constraint has an effect only when used in a nullable context. If you add
the notnull constraint in a nullable oblivious context, the compiler doesn't generate any
warnings or errors for violations of the constraint.
The class constraint in a nullable context specifies that the type argument must be a
non-nullable reference type. In a nullable context, when a type argument is a nullable
reference type, the compiler generates a warning.
The addition of nullable reference types complicates the use of T? in a generic type or
method. T? can be used with either the struct or class constraint, but one of them
must be present. When the class constraint was used, T? referred to the nullable
reference type for T. T? can be used when neither constraint is applied. In that case, T?
is interpreted as T? for value types and reference types. However, if T is an instance of
Nullable<T> , T? is the same as T. In other words, it doesn't become T??.
Because T? can now be used without either the class or struct constraint, ambiguities
can arise in overrides or explicit interface implementations. In both those cases, the
override doesn't include the constraints, but inherits them from the base class. When the
base class doesn't apply either the class or struct constraint, derived classes need to
somehow specify an override applies to the base method without either constraint.//Type parameter V is used as a type constraint.
public class SampleClass <T, U, V> where T : V { }
notnull constraint
class constraint
default constraintThat's when the derived method applies the default constraint. The default constraint
clarifies neither  the class nor struct constraint.
You can use the unmanaged constraint to specify that the type parameter must be a non-
nullable unmanaged type . The unmanaged constraint enables you to write reusable
routines to work with types that can be manipulated as blocks of memory, as shown in
the following example:
C#
The preceding method must be compiled in an unsafe context because it uses the
sizeof operator on a type not known to be a built-in type. Without the unmanaged
constraint, the sizeof operator is unavailable.
The unmanaged constraint implies the struct constraint and can't be combined with it.
Because the struct constraint implies the new() constraint, the unmanaged constraint
can't be combined with the new() constraint as well.
You can use System.Delegate  or System.MulticastDelegate  as a base class constraint. The
CLR always allowed this constraint, but the C# language disallowed it. The
System.Delegate constraint enables you to write code that works with delegates in a
type-safe manner. The following code defines an extension method that combines two
delegates provided they're the same type:
C#Unm anaged constraint
unsafe public static byte[] ToByteArray<T>( this T argument) where T : 
unmanaged
{
    var size = sizeof(T);
    var result = new Byte[size];
    Byte* p = ( byte*)&argument;
    for (var i = 0; i < size; i++)
        result[i] = *p++;
    return result;
}
Delegate constraints
public static TDelegate? TypeSafeCombine<TDelegate>( this TDelegate source,  
TDelegate target)You can use the above method to combine delegates that are the same type:
C#
If you uncomment the last line, it won't compile. Both first and test are delegate
types, but they're different delegate types.
You can also specify the System.Enum  type as a base class constraint. The CLR always
allowed this constraint, but the C# language disallowed it. Generics using System.Enum
provide type-safe programming to cache results from using the static methods in
System.Enum. The following sample finds all the valid values for an enum type, and then
builds a dictionary that maps those values to its string representation.
C#
Enum.GetValues and Enum.GetName use reflection, which has performance implications.
You can call EnumNamedValues to build a collection that is cached and reused rather than
repeating the calls that require reflection.    where TDelegate : System.Delegate
    => Delegate.Combine(source, target) as TDelegate;
Action first = () => Console.WriteLine( "this");
Action second = () => Console.WriteLine( "that");
var combined = first.TypeSafeCombine(second);
combined!();
Func<bool> test = () => true;
// Combine signature ensures combined delegates must
// have the same type.
//var badCombined = first.TypeSafeCombine(test);
Enum  constraints
public static Dictionary< int, string> EnumNamedValues<T>() where T : 
System.Enum
{
    var result = new Dictionary< int, string>();
    var values = Enum.GetValues( typeof(T));
    foreach (int item in values)
        result.Add(item, Enum.GetName( typeof(T), item)!);
    return result;
}You could use it as shown in the following sample to create an enum and build a
dictionary of its values and names:
C#
C#
Some scenarios require that an argument supplied for a type parameter implement that
interface. For example:
C#
This pattern enables the C# compiler to determine the containing type for the
overloaded operators, or any static virtual or static abstract method. It provides
the syntax so that the addition and subtraction operators can be defined on a
containing type. Without this constraint, the parameters and arguments would be
required to be declared as the interface, rather than the type parameter:
C#enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Green,
    Blue,
    Indigo,
    Violet
}
var map = EnumNamedValues<Rainbow>();
foreach (var pair in map)
    Console.WriteLine( $"{pair.Key} :\t{pair.Value} ");
Type arguments implement declared interface
public interface  IAdditionSubtraction <T> where T : IAdditionSubtraction <T>
{
    public abstract  static T operator  +(T left, T right);
    public abstract  static T operator  -(T left, T right);
}
public interface  IAdditionSubtraction <T> where T : IAdditionSubtraction <T>
{The preceding syntax would require implementers to use explicit interface
implementation  for those methods. Providing the extra constraint enables the interface
to define the operators in terms of the type parameters. T ypes that implement the
interface can implicitly implement the interface methods.
System.Collections.Generic
C# Programming Guide
Introduction to Generics
Generic Classes
new Constraint    public abstract  static IAdditionSubtraction<T> operator  +(
        IAdditionSubtraction<T> left,
        IAdditionSubtraction<T> right);
    public abstract  static IAdditionSubtraction<T> operator  -(
        IAdditionSubtraction<T> left,
        IAdditionSubtraction<T> right);
}
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
 Provide product feedbackGeneric Classes (C# Programming
Guide)
Article •07/09/2022
Generic classes encapsulate operations that are not specific to a particular data type.
The most common use for generic classes is with collections like linked lists, hash tables,
stacks, queues, trees, and so on. Operations such as adding and removing items from
the collection are performed in basically the same way regardless of the type of data
being stored.
For most scenarios that require collection classes, the recommended approach is to use
the ones provided in the .NET class library. For more information about using these
classes, see Generic Collections in .NET .
Typically, you create generic classes by starting with an existing concrete class, and
changing types into type parameters one at a time until you reach the optimal balance
of generalization and usability. When creating your own generic classes, important
considerations include the following:
Which types to generalize into type parameters.
As a rule, the more types you can parameterize, the more flexible and reusable
your code becomes. However, too much generalization can create code that is
difficult for other developers to read or understand.
What constraints, if any, to apply to the type parameters (See Constraints on T ype
Parameters ).
A good rule is to apply the maximum constraints possible that will still let you
handle the types you must handle. For example, if you know that your generic class
is intended for use only with reference types, apply the class constraint. That will
prevent unintended use of your class with value types, and will enable you to use
the as operator on T, and check for null values.
Whether to factor generic behavior into base classes and subclasses.
Because generic classes can serve as base classes, the same design considerations
apply here as with non-generic classes. See the rules about inheriting from generic
base classes later in this topic.
Whether to implement one or more generic interfaces.For example, if you are designing a class that will be used to create items in a
generics-based collection, you may have to implement an interface such as
IComparable<T>  where T is the type of your class.
For an example of a simple generic class, see Introduction to Generics .
The rules for type parameters and constraints have several implications for generic class
behavior, especially regarding inheritance and member accessibility. Before proceeding,
you should understand some terms. For a generic class Node<T>, client code can
reference the class either by specifying a type argument - to create a closed constructed
type (Node<int>); or by leaving the type parameter unspecified - for example when you
specify a generic base class, to create an open constructed type ( Node<T>). Generic
classes can inherit from concrete, closed constructed, or open constructed base classes:
C#
Non-generic, in other words, concrete, classes can inherit from closed constructed base
classes, but not from open constructed classes or from type parameters because there is
no way at run time for client code to supply the type argument required to instantiate
the base class.
C#
Generic classes that inherit from open constructed types must supply type arguments
for any base class type parameters that are not shared by the inheriting class, asclass BaseNode  { } 
class BaseNodeGeneric <T> { } 
// concrete type  
class NodeConcrete <T> : BaseNode  { } 
//closed constructed type  
class NodeClosed <T> : BaseNodeGeneric <int> { }
//open constructed type  
class NodeOpen <T> : BaseNodeGeneric <T> { } 
//No error  
class Node1 : BaseNodeGeneric <int> { } 
//Generates an error  
//class Node2 : BaseNodeGeneric<T> {}  
//Generates an error  
//class Node3 : T {}  demonstrated in the following code:
C#
Generic classes that inherit from open constructed types must specify constraints that
are a superset of, or imply, the constraints on the base type:
C#
Generic types can use multiple type parameters and constraints, as follows:
C#
Open constructed and closed constructed types can be used as method parameters:
C#class BaseNodeMultiple <T, U> { } 
//No error  
class Node4<T> : BaseNodeMultiple <T, int> { } 
//No error  
class Node5<T, U> : BaseNodeMultiple <T, U> { } 
//Generates an error  
//class Node6<T> : BaseNodeMultiple<T, U> {}  
class NodeItem <T> where T : System.IComparable <T>, new() { } 
class SpecialNodeItem <T> : NodeItem <T> where T : System.IComparable <T>, 
new() { } 
class SuperKeyType <K, V, U> 
    where U : System.IComparable <U> 
    where V : new() 
{ } 
void Swap<T>(List<T> list1, List<T> list2)  
{ 
    //code to swap items  
} 
void Swap(List<int> list1, List< int> list2) 
{ 
    //code to swap items  
} If a generic class implements an interface, all instances of that class can be cast to that
interface.
Generic classes are invariant. In other words, if an input parameter specifies a
List<BaseClass>, you will get a compile-time error if you try to provide a
List<DerivedClass>.
System.Collections.Generic
C# Programming Guide
Generics
Saving the S tate of Enumerators
An Inheritance Puzzle, P art OneSee alsoGeneric Interfaces (C# Programming
Guide)
Article •07/09/2022
It's often useful to define interfaces either for generic collection classes, or for the
generic classes that represent items in the collection. T o avoid boxing and unboxing
operations on value types, it's better to use generic interfaces , such as IComparable<T> ,
on generic classes. The .NET class library defines several generic interfaces for use with
the collection classes in the System.Collections.Generic  namespace. For more
information about these interfaces, see Generic interfaces .
When an interface is specified as a constraint on a type parameter, only types that
implement the interface can be used. The following code example shows a
SortedList<T> class that derives from the GenericList<T> class. For more information,
see Introduction to Generics . SortedList<T> adds the constraint where T :
IComparable<T>. This constraint enables the BubbleSort method in SortedList<T> to use
the generic CompareT o method on list elements. In this example, list elements are a
simple class, Person that implements IComparable<Person>.
C#
//Type parameter T in angle brackets.  
public class GenericList <T> : System.Collections .Generic.IEnumerable <T> 
{ 
    protected  Node head;  
    protected  Node current = null; 
    // Nested class is also generic on T  
    protected  class Node 
    { 
        public Node next;  
        private T data;  //T as private member datatype  
        public Node(T t)  //T used in non-generic constructor  
        {  
            next = null; 
            data = t;  
        }  
        public Node Next  
        {  
            get { return next; }  
            set { next = value; } 
        }  
        public T Data  //T as return type of property          {  
            get { return data; }  
            set { data = value; } 
        }  
    } 
    public GenericList ()  //constructor  
    { 
        head = null; 
    } 
    public void AddHead(T t)  //T as method parameter type  
    { 
        Node n = new Node(t);  
        n.Next = head;  
        head = n;  
    } 
    // Implementation of the iterator  
    public System.Collections.Generic. IEnumerator<T> GetEnumerator () 
    { 
        Node current = head;  
        while (current != null) 
        {  
            yield return current.Data;  
            current = current.Next;  
        }  
    } 
    // IEnumerable<T> inherits from IEnumerable, therefore this class  
    // must implement both the generic and non-generic versions of
    // GetEnumerator. In most cases, the non-generic method can  
    // simply call the generic method.  
    System.Collections.IEnumerator  
System.Collections.IEnumerable.GetEnumerator()  
    { 
        return GetEnumerator();  
    } 
} 
public class SortedList <T> : GenericList <T> where T : System.IComparable <T> 
{ 
    // A simple, unoptimized sort algorithm that  
    // orders list elements from lowest to highest:  
    public void BubbleSort () 
    { 
        if (null == head || null == head.Next)  
        {  
            return; 
        }  
        bool swapped;  
        do 
        {              Node previous = null; 
            Node current = head;  
            swapped = false; 
            while (current.next != null) 
            {  
                //  Because we need to call this method, the SortedList  
                //  class is constrained on IComparable<T>  
                if (current.Data.CompareTo(current.next.Data) > 0) 
                {  
                    Node tmp = current.next;  
                    current.next = current.next.next;  
                    tmp.next = current;  
                    if (previous == null) 
                    {  
                        head = tmp;  
                    }  
                    else 
                    {  
                        previous.next = tmp;  
                    }  
                    previous = tmp;  
                    swapped = true; 
                }  
                else 
                {  
                    previous = current;  
                    current = current.next;  
                }  
            }  
        } while (swapped);  
    } 
} 
// A simple class that implements IComparable<T> using itself as the  
// type argument. This is a common design pattern in objects that  
// are stored in generic lists.  
public class Person : System.IComparable <Person> 
{ 
    string name; 
    int age; 
    public Person(string s, int i) 
    { 
        name = s;  
        age = i;  
    } 
    // This will cause list elements to be sorted on age values.  
    public int CompareTo (Person p ) 
    { 
        return age - p.age;  
    }     public override  string ToString () 
    { 
        return name + ":" + age; 
    } 
    // Must implement Equals.  
    public bool Equals(Person p ) 
    { 
        return (this.age == p.age);  
    } 
} 
public class Program 
{ 
    public static void Main() 
    { 
        //Declare and instantiate a new generic SortedList class.  
        //Person is the type argument.  
        SortedList<Person> list = new SortedList<Person>();  
        //Create name and age values to initialize Person objects.  
        string[] names = new string[] 
        {  
            "Franscoise" , 
            "Bill", 
            "Li", 
            "Sandra" , 
            "Gunnar" , 
            "Alok", 
            "Hiroyuki" , 
            "Maria", 
            "Alessandro" , 
            "Raul" 
        };  
        int[] ages = new int[] { 45, 19, 28, 23, 18, 9, 108, 72, 30, 35 }; 
        //Populate the list.  
        for (int x = 0; x < 10; x++) 
        {  
            list.AddHead( new Person(names[x], ages[x]));  
        }  
        //Print out unsorted list.  
        foreach (Person p in list) 
        {  
            System.Console.WriteLine(p.ToString());  
        }  
        System.Console.WriteLine( "Done with unsorted list" ); 
        //Sort the list.  
        list.BubbleSort();  
        //Print out sorted list.  
        foreach (Person p in list) Multiple interfaces can be specified as constraints on a single type, as follows:
C#
An interface can define more than one type parameter, as follows:
C#
The rules of inheritance that apply to classes also apply to interfaces:
C#
Generic interfaces can inherit from non-generic interfaces if the generic interface is
covariant, which means it only uses its type parameter as a return value. In the .NET class
library, IEnumerable<T>  inherits from IEnumerable  because IEnumerable<T>  only uses
T in the return value of GetEnumerator  and in the Current  property getter.
Concrete classes can implement closed constructed interfaces, as follows:
C#        {  
            System.Console.WriteLine(p.ToString());  
        }  
        System.Console.WriteLine( "Done with sorted list" ); 
    } 
} 
class Stack<T> where T : System.IComparable <T>, IEnumerable <T> 
{ 
} 
interface  IDictionary <K, V> 
{ 
} 
interface  IMonth<T> { } 
interface  IJanuary  : IMonth<int> { }  //No error  
interface  IFebruary <T> : IMonth<int> { }  //No error  
interface  IMarch<T> : IMonth<T> { }    //No error  
                                       //interface IApril<T>  : IMonth<T, U>  
{}  //Error  
interface  IBaseInterface <T> { } 
class SampleClass  : IBaseInterface <string> { }Generic classes can implement generic interfaces or closed constructed interfaces as
long as the class parameter list supplies all arguments required by the interface, as
follows:
C#
The rules that control method overloading are the same for methods within generic
classes, generic structs, or generic interfaces. For more information, see Generic
Methods .
Beginning with C# 11, interfaces may declare static abstract or static virtual
members. Interfaces that declare either static abstract or static virtual members
are almost always generic interfaces. The compiler must resolve calls to static virtual
and static abstract methods at compile time. static virtual and static abstract
methods declared in interfaces don't have a runtime dispatch mechanism analogous to
virtual or abstract methods declared in classes. Instead, the compiler uses type
information available at compile time. These members are typically declared in generic
interfaces. Furthermore, most interfaces that declare static virtual or static abstract
methods declare that one of the type parameters must implement the declared
interface . The compiler then uses the supplied type arguments to resolve the type of the
