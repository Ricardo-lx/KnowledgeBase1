the accessible nested types and static members (except extension methods) contained
directly in the declaration of the given type can be referenced directly.
A global_using_st atic_dir ective specifically does not import extension methods directly as
static methods, but makes them available for extension method invocation.
A global_using_st atic_dir ective only imports members and types declared directly in the
given type, not members and types declared in base classes.
Ambiguities between multiple global_using_namesp ace_directives and
global_using_st atic_dir ectives are discussed in the section for
global_using_namesp ace_directives (above).Global Using static directives
global_using_static_directive  
    : 'global'  'using' 'static'  type_name ';' 
    ; 
Changes are made to the algorithm determining the meaning of a
quali fied_alias_member  as follows.
This is the relevant bullet point with proposed additions (which are in bold ):
Otherwise, starting with the namespace declaration ( §13.3 ) immediately
containing the quali fied_alias_member  (if any), continuing with each enclosing
namespace declaration (if any), and ending with the compilation unit containing
the quali fied_alias_member , the following steps are evaluated until an entity is
located:
If the namespace declaration or compilation unit contains a using_alias_dir ective
that associates N with a type, or, when a compilation unit is r eached, the
program contains a glob al_using_alias_dir ectiv e that associat es N with a type,
then the quali fied_alias_member  is undefined and a compile-time error occurs.
Otherwise, if the namespace declaration or compilation unit contains an
extern_alias_dir ective or using_alias_dir ective that associates N with a
namespace, * or, when a compilation unit is r eached, the pr ogram contains a
glob al_using_alias_dir ectiv e that associat es N with a namesp ace, then:
If the namespace associated with N contains a namespace named I and K is
zero, then the quali fied_alias_member  refers to that namespace.
Otherwise, if the namespace associated with N contains a non-generic type
named I and K is zero, then the quali fied_alias_member  refers to that type.
Otherwise, if the namespace associated with N contains a type named I that
has K type parameters, then the quali fied_alias_member  refers to that type
constructed with the given type arguments.
Otherwise, the quali fied_alias_member  is undefined and a compile-time error
occurs.Qualified alias member §13.8
File Sco ped Namespaces
Article •06/23/2023
File scoped namespaces use a less verbose format for the typical case of files containing
only one namespace. The file scoped namespace format is namespace X.Y.Z; (note the
semicolon and lack of braces). This allows for files like the following:
c#
The semantics are that using the namespace X.Y.Z; form is equivalent to writing
namespace X.Y.Z { ... } where the remainder of the file following the file-scoped
namespace is in the ... section of a standard namespace declaration.
Analysis of the C# ecosystem shows that approximately 99.7% files are all of either one
of these forms:
c#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
namespace  X.Y.Z; 
using System;  
class X 
{ 
} 
Motivationor
c#
However, both these forms force the user to indent the majority of their code and add a
fair amount of ceremony for what is effectively a very basic concept. This affects clarity,
uses horizontal and vertical space, and is often unsatisfying for users both used to C#
and coming from other languages (which commonly have less ceremony here).
The primary goal of the feature therefore is to meet the needs of the majority of the
ecosystem with less unnecessary boilerplate.
This proposal takes the form of a diff to the existing compilation units ( §13.2 ) section
of the specification.
A compilation_unit  defines the overall structure of a source file. A compilation unit
consists of zero or more using_dir ectives followed by zero or more global_attr ibutes
followed by zero or more namesp ace_member_declar ation s.
A compilation_unit  defines the overall structure of a source file. A compilation unit
consists of zero or more using_dir ectives followed by zero or more global_attr ibutes
followed by a compilation_unit_body . A compilation_unit_body  can either be a
file_scoped_namesp ace_declar ation  or zero or more statement s and
namesp ace_member_declar ation s.namespace  X.Y.Z 
{ 
    // usings  
    // types  
} 
// usings  
namespace  X.Y.Z 
{ 
    // types  
} 
Detailed design
Diffantlr
... unchanged ...
A file_scoped_namesp ace_declar ation  will contribute members corresponding to the
namesp ace_declar ation  it is semantically equivalent to. See ( Namespace Declarations ) for
more details.
A namesp ace_declar ation  consists of the keyword namespace, followed by a namespace
name and body, optionally followed by a semicolon. A
file_scoped_namesp ace_declar ation  consists of the keyword namespace, followed by a
namespace name, a semicolon and an optional list of extern_alias_dir ectives,
using_dir ectives and type_declar ation s.
antlr
... unchanged ...
the two namespace declarations above contribute to the same declaration space, in this
case declaring two classes with the fully qualified names N1.N2.A and N1.N2.B. Becausecompilation_unit  
~~    : extern_alias_directive* using_directive* global_attributes?  
namespace_member_declaration*~~  
    : extern_alias_directive* using_directive* global_attributes?  
compilation_unit_body  
    ; 
compilation_unit_body  
    : statement* namespace_member_declaration*  
    | file_scoped_namespace_declaration  
    ; 
Namespace declarations
namespace_declaration  
    : 'namespace'  qualified_identifier namespace_body ';'? 
    ; 
     
file_scoped_namespace_declaration
    : 'namespace'  qualified_identifier ';' extern_alias_directive*  
using_directive* type_declaration*  
    ; 
... unchanged ...  the two declarations contribute to the same declaration space, it would have been an
error if each contained a declaration of a member with the same name.
A file_scoped_namesp ace_declar ation  permits a namespace declaration to be written
without the { ... } block. For example:
C#
is semantically equivalent to
C#
Specifically, a file_scoped_namesp ace_declar ation  is treated the same as a
namesp ace_declar ation  at the same location in the compilation_unit  with the same
quali fied_identi fier. The extern_alias_dir ectives, using_dir ectives and type_declar ation s of
that file_scoped_namesp ace_declar ation  act as if they were declared in the same order
inside the namesp ace_body  of that namesp ace_declar ation .
A source file cannot contain both a file_scoped_namesp ace_declar ation  and a
namesp ace_declar ation . A source file cannot contain multiple
file_scoped_namesp ace_declar ation s. A compilation_unit  cannot contain both a
file_scoped_namesp ace_declar ation  and any top level statement s. type_declar ation s
cannot precede a file_scoped_namesp ace_declar ation .
... unchanged ...extern alias A; 
namespace  Name; 
using B; 
class C 
{ 
} 
extern alias A; 
namespace  Name 
{ 
    using B; 
    class C 
    { 
    } 
} 
Extern aliasesExtended property patterns
Article •06/23/2023
Allow property subpatterns to reference nested members, for instance:
C#
Instead of:
C#
When you want to match a child property, nesting another recursive pattern adds too
much noise which will hurt readability with no real advantage.
The property_pattern syntax is modified as follow:
diff７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
if (e is MethodCallExpression { Method.Name: "MethodName"  }) 
if (e is MethodCallExpression { Method: { Name: "MethodName"  } }) 
Motivation
Detailed design
The receiver for each name lookup is the type of the previous member T0, starting from
the input type  of the property_pattern. if T is a nullable type, T0 is its underlying type,
otherwise T0 is equal to T.
For example, a pattern of the form { Prop1.Prop2: pattern } is exactly equivalent to {
Prop1: { Prop2: pattern } }.
Note that this will include the null check when T is a nullable value type or a reference
type. This null check means that the nested properties available will be the properties of
T0, not of T.
Repeated member paths are allowed. The compilation of pattern matching can take
advantage of common parts of patterns.property_pattern  
  : type? property_pattern_clause simple_designation?  
  ; 
property_pattern_clause  
  : '{' (subpattern (',' subpattern)* ','?)? '}'  
  ; 
subpattern  
- : identifier ':' pattern  
+ : subpattern_name ':' pattern  
  ; 
+subpattern_name  
+ : identifier  
+ | subpattern_name '.' identifier  
+ ; Improved Interpolated Strings
Article •03/21/2022
We introduce a new pattern for creating and using interpolated string expressions to
allow for efficient formatting and use in both general string scenarios and more
specialized scenarios such as logging frameworks, without incurring unnecessary
allocations from formatting the string in the framework.
Today, string interpolation mainly lowers down to a call to string.Format. This, while
general purpose, can be inefficient for a number of reasons:
1. It boxes any struct arguments, unless the runtime has happened to introduce an
overload of string.Format that takes exactly the correct types of arguments in
exactly the correct order.
This ordering is why the runtime is hesitant to introduce generic versions of
the method, as it would lead to combinatoric explosion of generic
instantiations of a very common method.
2. It has to allocate an array for the arguments in most cases.
3. There is no opportunity to avoid instantiating the instance if it's not needed.
Logging frameworks, for example, will recommend avoiding string interpolation
because it will cause a string to be realized that may not be needed, depending on
the current log-level of the application.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation4. It can never use Span or other ref struct types today, because ref structs are not
allowed as generic type parameters, meaning that if a user wants to avoid copying
to intermediate locations they have to manually format strings.
Internally, the runtime has a type called ValueStringBuilder to help deal with the first 2
of these scenarios. They pass a stackalloc'd buffer to the builder, repeatedly call
AppendFormat with every part, and then get a final string out. If the resulting string goes
past the bounds of the stack buffer, they can then move to an array on the heap.
However, this type is dangerous to expose directly, as incorrect usage could lead to a
rented array to be double-disposed, which then will cause all sorts of undefined
behavior in the program as two locations think they have sole access to the rented array.
This proposal creates a way to use this type safely from native C# code by just writing an
interpolated string literal, leaving written code unchanged while improving every
interpolated string that a user writes. It also extends this pattern to allow for
interpolated strings passed as arguments to other methods to use a handler pattern,
defined by receiver of the method, that will allow things like logging frameworks to
avoid allocating strings that will never be needed, and giving C# users familiar,
convenient interpolation syntax.
We introduce a new handler pattern that can represent an interpolated string passed as
an argument to a method. The simple English of the pattern is as follows:
When an interpolat ed_str ing_expr ession  is passed as an argument to a method, we look
at the type of the parameter. If the parameter type has a constructor that can be
invoked with 2 int parameters, literalLength and formattedCount, optionally takes
additional parameters specified by an attribute on the original parameter, optionally has
an out boolean trailing parameter, and the type of the original parameter has instance
AppendLiteral and AppendFormatted methods that can be invoked for every part of the
interpolated string, then we lower the interpolation using that, instead of into a
traditional call to string.Format(formatStr, args). A more concrete example is helpful
for picturing this:
C#Detailed Design
The handler pattern
// The handler that will actually "build" the interpolated string"  
[InterpolatedStringHandler ] 
public ref struct TraceLoggerParamsInterpolatedStringHandler  { 
    // Storage for the built-up string  
    private bool _logLevelEnabled;  
    public TraceLoggerParamsInterpolatedStringHandler (int literalLength, int 
formattedCount, Logger logger, out bool handlerIsValid ) 
    { 
        if (!logger._logLevelEnabled)  
        {  
            handlerIsValid = false; 
            return; 
        }  
        handlerIsValid = true; 
        _logLevelEnabled = logger.EnabledLevel;  
    } 
    public void AppendLiteral (string s) 
    { 
        // Store and format part as required  
    } 
    public void AppendFormatted<T>(T t)  
    { 
        // Store and format part as required  
    } 
} 
// The logger class. The user has an instance of this, accesses it via  
static state, or some other access  
// mechanism  
public class Logger 
{ 
    // Initialization code omitted  
    public LogLevel EnabledLevel;  
    public void 
LogTrace ([InterpolatedStringHandlerArguments( "")]TraceLoggerParamsInterpolat
edStringHandler handler)  
    { 
        // Impl of logging  
    } 
} 
Logger logger = GetLogger(LogLevel.Info);  
// Given the above definitions, usage looks like this:  
var name = "Fred Silberberg" ; 
logger.LogTrace( $"{name} will never be printed because info is < trace!" ); 
// This is converted to:  
var name = "Fred Silberberg" ; 
var receiverTemp = logger;  
var handler = new TraceLoggerParamsInterpolatedStringHandler(literalLength:  Here, because TraceLoggerParamsInterpolatedStringHandler has a constructor with the
correct parameters, we say that the interpolated string has an implicit handler
conversion to that parameter, and it lowers to the pattern shown above. The specese
needed for this is a bit complicated, and is expanded below.
The rest of this proposal will use Append... to refer to either of AppendLiteral or
AppendFormatted in cases when both are applicable.
The compiler recognizes the
System.Runtime.CompilerServices.InterpolatedStringHandlerAttribute:
C#
This attribute is used by the compiler to determine if a type is a valid interpolated string
handler type.
The compiler also recognizes the
System.Runtime.CompilerServices.InterpolatedStringHandlerArgumentAttribute:
C#47, formattedCount: 1, receiverTemp, out var handlerIsValid);  
if (handlerIsValid)  
{ 
    handler.AppendFormatted(name);  
    handler.AppendLiteral( " will never be printed because info is <  
trace!"); 
} 
receiverTemp.LogTrace(handler);  
New attributes
using System;  
namespace  System.Runtime.CompilerServices  
{ 
    [AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct,  
AllowMultiple = false, Inherited = false) ] 
    public sealed class InterpolatedStringHandlerAttribute  : Attribute  
    { 
        public InterpolatedStringHandlerAttribute () 
        {  
        }  
    } 
} 
namespace  System.Runtime.CompilerServices  
{ This attribute is used on parameters, to inform the compiler how to lower an
interpolated string handler pattern used in a parameter position.
Type T is said to be an applicable_int erpolat ed_str ing_handler_type  if it is attributed with
System.Runtime.CompilerServices.InterpolatedStringHandlerAttribute. There exists an
implicit interpolat ed_str ing_handler_c onversion to T from an
interpolat ed_str ing_expr ession , or an additiv e_expr ession  composed entirely of
_interpolated_string_expression_s and using only + operators.
For simplicity in the rest of this speclet, interpolat ed_str ing_expr ession  refers to both a
simple interpolat ed_str ing_expr ession , and to an additiv e_expr ession  composed entirely
of _interpolated_string_expression_s and using only + operators.
Note that this conversion always exists, regardless of whether there will be later errors
when actually attempting to lower the interpolation using the handler pattern. This is
done to help ensure that there are predictable and useful errors and that runtime
behavior doesn't change based on the content of an interpolated string.
We adjust the wording of the applicable function member algorithm ( §11.6.4.2 ) as
follows (a new sub-bullet is added to each section, in bold):
A function member is said to be an applicable f unction member  with respect to an
argument list A when all of the following are true:
Each argument in A corresponds to a parameter in the function member
declaration as described in Corresponding parameters ( §11.6.2.2 ), and any
parameter to which no argument corresponds is an optional parameter.    [AttributeUsage(AttributeTargets.Parameter, AllowMultiple = false,  
Inherited = false) ] 
    public sealed class InterpolatedStringHandlerArgumentAttribute  : 
Attribute  
    { 
        public InterpolatedHandlerArgumentAttribute (string argument ); 
        public InterpolatedHandlerArgumentAttribute (params string[] 
arguments ); 
        public string[] Arguments { get; } 
    } 
} 
Interpolated string handler conversion
Applicable function member adjustments
For each argument in A, the parameter passing mode of the argument (i.e., value,
ref, or out) is identical to the parameter passing mode of the corresponding
parameter, and
for a value parameter or a parameter array, an implicit conversion ( §10.2 )
exists from the argument to the type of the corresponding parameter, or
for a ref paramet er whose type is a struct type, an implicit
interpolat ed_str ing_handler_c onversion exists fr om the ar gument t o the type
of the corr esponding p aramet er, or
for a ref or out parameter, the type of the argument is identical to the type of
the corresponding parameter. After all, a ref or out parameter is an alias for
the argument passed.
For a function member that includes a parameter array, if the function member is
applicable by the above rules, it is said to be applicable in its normal for m. If a function
member that includes a parameter array is not applicable in its normal form, the
function member may instead be applicable in its expanded for m:
The expanded form is constructed by replacing the parameter array in the function
member declaration with zero or more value parameters of the element type of
the parameter array such that the number of arguments in the argument list A
matches the total number of parameters. If A has fewer arguments than the
number of fixed parameters in the function member declaration, the expanded
form of the function member cannot be constructed and is thus not applicable.
Otherwise, the expanded form is applicable if for each argument in A the
parameter passing mode of the argument is identical to the parameter passing
mode of the corresponding parameter, and
for a fixed value parameter or a value parameter created by the expansion, an
implicit conversion ( §10.2 ) exists from the type of the argument to the type of
the corresponding parameter, or
for a ref paramet er whose type is a struct type, an implicit
interpolat ed_str ing_handler_c onversion exists fr om the ar gument t o the type
of the corr esponding p aramet er, or
for a ref or out parameter, the type of the argument is identical to the type of
the corresponding parameter.
Important note: this means that if there are 2 otherwise equivalent overloads, that only
differ by the type of the applicable_int erpolat ed_str ing_handler_type , these overloads will
be considered ambiguous. Further, because we do not see through explicit casts, it is
possible that there could arise an unresolvable scenario where both applicable
overloads use InterpolatedStringHandlerArguments and are totally uncallable without
manually performing the handler lowering pattern. W e could potentially make changes
to the better function member algorithm to resolve this if we so choose, but this
scenario unlikely to occur and isn't a priority to address.
We change the better conversion from expression ( §11.6.4.4 ) section to the following:
Given an implicit conversion C1 that converts from an expression E to a type T1, and an
implicit conversion C2 that converts from an expression E to a type T2, C1 is a better
conversion than C2 if:
1. E is a non-constant interpolat ed_str ing_expr ession , C1 is an
implicit_str ing_handler_c onversion, T1 is an
applicable_int erpolat ed_str ing_handler_type , and C2 is not an
implicit_str ing_handler_c onversion, or
2. E does not exactly match T2 and at least one of the following holds:
E exactly matches T1 (§11.6.4.4 )
T1 is a better conversion target than T2 (§11.6.4.6 )
This does mean that there are some potentially non-obvious overload resolution rules,
depending on whether the interpolated string in question is a constant-expression or
not. For example:
C#
This is introduced so that things that can simply be emitted as constants do so, and
don't incur any overhead, while things that cannot be constant use the handler pattern.
We introduce a new type in System.Runtime.CompilerServices:
DefaultInterpolatedStringHandler. This is a ref struct with many of the same semanticsBetter conversion from expression adjustments
void Log(string s) { ... }  
void Log(TraceLoggerParamsInterpolatedStringHandler p ) { ... }  
Log($""); // Calls Log(string s), because $"" is a constant expression  
Log($"{"test"}"); // Calls Log(string s), because $"{"test"}" is a constant  
expression  
Log($"{1}"); // Calls Log(TraceLoggerParamsInterpolatedStringHandler p),  
because $"{1}" is not a constant expression  
InterpolatedStringHandler and Usageas ValueStringBuilder, intended for direct use by the C# compiler. This struct would
look approximately like this:
C#
We make a slight change to the rules for the meaning of an
interpolat ed_str ing_expr ession  (§11.7.3 ):
If the type o f an int erpolat ed string is string and the type
System.Runtime.CompilerServices.DefaultInterpolatedStringHandler exists, and the
current cont ext suppor ts using that type, the string  is low ered using the handler
pattern. The final string value is then obtained by calling ToStringAndClear() on the
handler type.  Other wise, if  the type of an interpolated string is System.IFormattable or
System.FormattableString [the rest is unchanged]
The "and the current context supports using that type" rule is intentionally vague to give
the compiler leeway in optimizing usage of this pattern. The handler type is likely to be
a ref struct type, and ref struct types are normally not permitted in async methods. For// API Proposal issue: https://github.com/dotnet/runtime/issues/50601  
namespace  System.Runtime.CompilerServices  
{ 
    [InterpolatedStringHandler ] 
    public ref struct DefaultInterpolatedStringHandler  
    { 
        public DefaultInterpolatedStringHandler (int literalLength, int 
formattedCount ); 
        public string ToStringAndClear (); 
        public void AppendLiteral (string value); 
        public void AppendFormatted<T>(T value); 
        public void AppendFormatted<T>(T value, string? format);  
        public void AppendFormatted<T>(T value, int alignment);  
        public void AppendFormatted<T>(T value, int alignment, string? 
format);  
        public void AppendFormatted (ReadOnlySpan< char> value); 
        public void AppendFormatted (ReadOnlySpan< char> value, int alignment  
= 0, string? format = null); 
        public void AppendFormatted (string? value); 
        public void AppendFormatted (string? value, int alignment = 0, 
string? format = null); 
        public void AppendFormatted (object? value, int alignment = 0, 
string? format = null); 
    } 
} 
this particular case, the compiler would be allowed to make use the handler if none of
the interpolation holes contain an await expression, as we can statically determine that
the handler type is safely used without additional complicated analysis because the
handler will be dropped after the interpolated string expression is evaluated.
Open  Question :
Do we want to instead just make the compiler know about
DefaultInterpolatedStringHandler and skip the string.Format call entirely? It would
allow us to hide a method that we don't necessarily want to put in people's faces when
they manually call string.Format.
Answer: Yes.
Open  Question :
Do we want to have handlers for System.IFormattable and System.FormattableString as
well?
Answer: No.
In this section, method invocation resolution refers to the steps listed in §11.7.8.2 .
Given an applicable_int erpolat ed_str ing_handler_type  T and an
interpolat ed_str ing_expr ession  i, method invocation resolution and validation for a valid
constructor on T is performed as follows:
1. Member lookup for instance constructors is performed on T. The resulting method
group is called M.
2. The argument list A is constructed as follows:
a. The first two arguments are integer constants, representing the literal length of
i, and the number of interpolation  components in i, respectively.
b. If i is used as an argument to some parameter pi in method M1, and
parameter pi is attributed with
System.Runtime.CompilerServices.InterpolatedStringHandlerArgumentAttribute,
then for every name Argx in the Arguments array of that attribute the compiler
matches it to a parameter px that has the same name. The empty string is
matched to the receiver of M1.Handler pattern codegen
Constructor resolutionIf any Argx is not able to be matched to a parameter of M1, or an Argx
requests the receiver of M1 and M1 is a static method, an error is produced
and no further steps are taken.
Otherwise, the type of every resolved px is added to the argument list, in
the order specified by the Arguments array. Each px is passed with the
same ref semantics as is specified in M1.
c. The final argument is a bool, passed as an out parameter.
3. Traditional method invocation resolution is performed with method group M and
argument list A. For the purposes of method invocation final validation, the
context of M is treated as a member_ac cess through type T.
If a single-best constructor F was found, the result of overload resolution is
F.
If no applicable constructors were found, step 3 is retried, removing the final
bool parameter from A. If this retry also finds no applicable members, an
error is produced and no further steps are taken.
If no single-best method was found, the result of overload resolution is
ambiguous, an error is produced, and no further steps are taken.
4. Final validation on F is performed.
If any element of A occurred lexically after i, an error is produced and no
further steps are taken.
If any A requests the receiver of F, and F is an indexer being used as an
initializer_t arget in a member_initializer , then an error is reported and no
further steps are taken.
Note: the resolution here intentionally do not use the actual expressions passed as other
arguments for Argx elements. W e only consider the types post-conversion. This makes
sure that we don't have double-conversion issues, or unexpected cases where a lambda
is bound to one delegate type when passed to M1 and bound to a different delegate
type when passed to M.
Note: W e report an error for indexers uses as member initializers because of the order of
evaluation for nested member initializers. Consider this code snippet:
C#
var x1 = new C1 { C2 = { [GetString()] = { A = 2, B = 4 } } }; 
/* Lowering:  The arguments to __c1.C2[] are evaluated befor e the receiver of the indexer. While we
could come up with a lowering that works for this scenario (either by creating a temp for
__c1.C2 and sharing it across both indexer invocations, or only using it for the first
indexer invocation and sharing the argument across both invocations) we think that any
lowering would be confusing for what we believe is a pathological scenario. Therefore,
we forbid the scenario entirely.__c1 = new C1();  
string argTemp = GetString();  
__c1.C2[argTemp][1] = 2;  
__c1.C2[argTemp][3] = 4;  
Prints: 
GetString  
get_C2 
get_C2 
*/ 
string GetString () 
{ 
    Console.WriteLine( "GetString" ); 
    return ""; 
} 
class C1 
{ 
    private C2 c2 = new C2(); 
    public C2 C2 { get { Console.WriteLine( "get_C2" ); return c2; } set { } } 
} 
class C2 
{ 
    public C3 this[string s] 
    { 
        get => new C3(); 
        set { } 
    } 
} 
class C3 
{ 
    public int A 
    { 
        get => 0; 
        set { } 
    } 
    public int B 
    { 
        get => 0; 
        set { } 
    } 
} Open Question :
If we use a constructor instead of Create, we'd improve runtime codegen, at the
expense of narrowing the pattern a bit.
Answer: We will restrict to constructors for now. W e can revisit adding a general Create
method later if the scenario arises.
Given an applicable_int erpolat ed_str ing_handler_type  T and an
interpolat ed_str ing_expr ession  i, overload resolution for a set of valid Append...
methods on T is performed as follows:
1. If there are any interpolat ed_regular_str ing_char acter components in i:
a. Member lookup on T with the name AppendLiteral is performed. The resulting
method group is called Ml.
b. The argument list Al is constructed with one value parameter of type string.
c. Traditional method invocation resolution is performed with method group Ml
and argument list Al. For the purposes of method invocation final validation,
the context of Ml is treated as a member_ac cess through an instance of T.
If a single-best method Fi is found and no errors were produced, the
result of method invocation resolution is Fi.
Otherwise, an error is reported.
2. For every interpolation  ix component of i:
a. Member lookup on T with the name AppendFormatted is performed. The
resulting method group is called Mf.
b. The argument list Af is constructed:
i. The first parameter is the expression of ix, passed by value.
ii. If ix directly contains a constant_expr ession  component, then an integer
value parameter is added, with the name alignment specified.
iii. If ix is directly followed by an interpolation_for mat, then a string value
parameter is added, with the name format specified.
c. Traditional method invocation resolution is performed with method group Mf
and argument list Af. For the purposes of method invocation final validation,
the context of Mf is treated as a member_ac cess through an instance of T.Append... method overload resolutionIf a single-best method Fi is found, the result of method invocation
resolution is Fi.
Otherwise, an error is reported.
3. Finally, for every Fi discovered in steps 1 and 2, final validation is performed:
If any Fi does not return bool by value or void, an error is reported.
If all Fi do not return the same type, an error is reported.
Note that these rules do not permit extension methods for the Append... calls. W e
could consider enabling that if we choose, but this is analogous to the enumerator
pattern, where we allow GetEnumerator to be an extension method, but not Current or
MoveNext().
These rules do permit default parameters for the Append... calls, which will work with
things like CallerLineNumber or CallerArgumentExpression (when supported by the
language).
We have separate overload lookup rules for base elements vs interpolation holes
because some handlers will want to be able to understand the difference between the
components that were interpolated and the components that were part of the base
string.
Open  Question
Some scenarios, like structured logging, want to be able to provide names for
interpolation elements. For example, today a logging call might look like Log("{name}
bought {itemCount} items", name, items.Count);. The names inside the {} provide
important structure information for loggers that help with ensuring output is consistent
and uniform. Some cases might be able to reuse the :format component of an
interpolation hole for this, but many loggers already understand format specifiers and
have existing behavior for output formatting based on this info. Is there some syntax we
can use to enable putting these named specifiers in?
Some cases may be able to get away with CallerArgumentExpression, provided that
support does land in C# 10. But for cases that invoke a method/property, that may not
be sufficient.
Answer:
While there are some interesting parts to templated strings we could explore in an
orthogonal language feature, we don't think a specific syntax here has much benefit
over solutions such as using a tuple: $"{("StructuredCategory", myExpression)}".Given an applicable_int erpolat ed_str ing_handler_type  T and an
interpolat ed_str ing_expr ession  i that had a valid constructor Fc and Append... methods
Fa resolved, lowering for i is performed as follows:
1. Any arguments to Fc that occur lexically before i are evaluated and stored into
temporary variables in lexical order. In order to preserve lexical ordering, if i
occurred as part of a larger expression e, any components of e that occurred
before i will be evaluated as well, again in lexical order.
2. Fc is called with the length of the interpolated string literal components, the
number of interpolation  holes, any previously evaluated arguments, and a bool out
argument (if Fc was resolved with one as the last parameter). The result is stored
into a temporary value ib.
a. The length of the literal components is calculated after replacing any
open_br ace_escape_s equenc e with a single {, and any
close_brace_escape_s equenc e with a single }.
3. If Fc ended with a bool out argument, a check on that bool value is generated. If
true, the methods in Fa will be called. Otherwise, they will not be called.
4. For every Fax in Fa, Fax is called on ib with either the current literal component
or interpolation  expression, as appropriate. If Fax returns a bool, the result is
logically anded with all preceding Fax calls.
a. If Fax is a call to AppendLiteral, the literal component is unescaped by
replacing any open_br ace_escape_s equenc e with a single {, and any
close_brace_escape_s equenc e with a single }.
5. The result of the conversion is ib.
Again, note that arguments passed to Fc and arguments passed to e are the same
temp. Conversions may occur on top of the temp to convert to a form that Fc requires,
but for example lambdas cannot be bound to a different delegate type between Fc and
e.
Open  Question
This lowering means that subsequent parts of the interpolated string after a false-
returning Append... call don't get evaluated. This could potentially be very confusing,
particularly if the format hole is side-effecting. W e could instead evaluate all format
holes first, then repeatedly call Append... with the results, stopping if it returns false.
This would ensure that all expressions get evaluated as one might expect, but we call asPerforming the conversionfew methods as we need to. While the partial evaluation might be desirable for some
more advanced cases, it is perhaps non-intuitive for the general case.
Another alternative, if we want to always evaluate all format holes, is to remove the
Append... version of the API and just do repeated Format calls. The handler can track
whether it should just be dropping the argument and immediately returning for this
version.
Answer: We will have conditional evaluation of the holes.
Open  Question
Do we need to dispose of disposable handler types, and wrap calls with try/finally to
ensure that Dispose is called? For example, the interpolated string handler in the bcl
might have a rented array inside it, and if one of the interpolation holes throws an
exception during evaluation, that rented array could be leaked if it wasn't disposed.
Answer: No. handlers can be assigned to locals (such as MyHandler handler = $"
{MyCode()};), and the lifetime of such handlers is unclear. Unlike foreach enumerators,
where the lifetime is obvious and no user-defined local is created for the enumerator.
To minimize complexity of the implementation, we have a few limitations on how we
perform nullable analysis on interpolated string handler constructors used as arguments
to a method or indexer. In particular, we do not flow information from the constructor
back through to the original slots of parameters or arguments from the original context,
and we do not use constructor parameter types to inform generic type inference for
type parameters in the containing method. An example of where this can have an
impact is:
C#Impact on nullable reference types
string s = ""; 
C c = new C(); 
c.M(s, $"", c.ToString(), s.ToString()); // No warnings on c.ToString() or  
s.ToString(), as the `MaybeNull` does not flow back.  
public class C 
{ 
    public void M(string s1, [InterpolatedStringHandlerArgument( "", "s1")] 
CustomHandler c1, string s2, string s3) { } 
} 
[InterpolatedStringHandler ] 
public partial struct CustomHandler  C#
For type author simplicity, we could consider allowing expressions of type string to be
implicitly-convertible to applicable_int erpolat ed_str ing_handler_types . As proposed
today, authors will likely need to overload on both that handler type and regular string
types, so their users don't have to understand the difference. This may be an annoying
and non-obvious overhead, as a string expression can be viewed as an interpolation
with expression.Length prefilled length and 0 holes to be filled.
This would allow new APIs to only expose a handler, without also having to expose a
string-accepting overload. However, it won't get around the need for changes to
better conversion from expression, so while it would work it may be unnecessary
overhead.
Answer:{ 
    public CustomHandler (int literalLength, int formattedCount, [MaybeNull]  
C c, [MaybeNull] string s) : this() 
    { 
    } 
} 
string? s = null; 
M(s, $""); // Infers `string` for `T` because of the `T?` parameter, not  
`string?`, as flow analysis does not consider the unannotated `T` parameter  
of the constructor  
void M<T>(T? t, [InterpolatedStringHandlerArgument( "s1")] CustomHandler<T>  
c) { } 
[InterpolatedStringHandler ] 
public partial struct CustomHandler<T>  
{ 
    public CustomHandler (int literalLength, int formattedCount, T t ) : 
this() 
    { 
    } 
} 
Other considerations
Allow string types to be convertible to handlers as wellWe think that this could end up being confusing, and there's an easy workaround for
custom handler types: add a user-defined conversion from string.
ValueStringBuilder as it exists today has 2 constructors: one that takes a count, and
allocates on the heap eagerly, and one that takes a Span<char>. That Span<char> is
usually a fixed size in the runtime codebase, around 250 elements on average. T o truly
replace that type, we should consider an extension to this where we also recognize
GetInterpolatedString methods that take a Span<char>, instead of just the count
version. However, we see a few potential thorny cases to resolve here:
We don't want to stackalloc repeatedly in a hot loop. If we were to do this
extension to the feature, we'd likely want to share the stackalloc'd span between
loop iterations. W e know this is safe, as Span<T> is a ref struct that can't be stored
on the heap, and users would have to be pretty devious to manage to extract a
reference to that Span (such as creating a method that accepts such a handler then
deliberately retrieving the Span from the handler and returning it to the caller).
However, allocating ahead of time produces other questions:
Should we eagerly stackalloc? What if the loop is never entered, or exits before
it needs the space?
If we don't eagerly stackalloc, does that mean we introduce a hidden branch on
every loop? Most loops likely won't care about this, but it could affect some
tight loops that don't want to pay the cost.
Some strings can be quite big, and the appropriate amount to stackalloc is
dependent on a number of factors, including runtime factors. W e don't really want
the C# compiler and specification to have to determine this ahead of time, so we'd
want to resolve https://github.com/dotnet/runtime/issues/25423  and add an API
for the compiler to call in these cases. It also adds more pros and cons to the
points from the previous loop, where we don't want to potentially allocate large
arrays on the heap many times or before one is needed.
Answer:
This is out of scope for C# 10. W e can look at this in general when we look at the more
general params Span<T> feature.
For simplicity, this spec currently just proposes recognizing a Append... method, and
things that always succeed (like InterpolatedStringHandler) would always return trueIncorporating spans for heap-less strings
Non-try version of the APIfrom the method. This was done to support partial formatting scenarios where the user
wants to stop formatting if an error occurs or if it's unnecessary, such as the logging
case, but could potentially introduce a bunch of unnecessary branches in standard
interpolated string usage. W e could consider an addendum where we use just FormatX
methods if no Append... method is present, but it does present questions about what
we do if there's a mix of both Append... and FormatX calls.
Answer:
We want the non-try version of the API. The proposal has been updated to reflect this.
There is unfortunate lack of symmetry in the proposal at it currently exists: invoking an
extension method in reduced form produces different semantics than invoking the
extension method in normal form. This is different from most other locations in the
language, where reduced form is just a sugar. W e propose adding an attribute to the
framework that we will recognize when binding a method, that informs the compiler
that certain parameters should be passed to the constructor on the handler. Usage looks
like this:
C#
Usage of this is then:
C#Passing previous arguments to the handler
namespace  System.Runtime.CompilerServices  
{ 
    [AttributeUsage(AttributeTargets.Parameter, AllowMultiple = false,  
Inherited = false) ] 
    public sealed class InterpolatedStringHandlerArgumentAttribute  : 
Attribute  
    { 
        public InterpolatedStringHandlerArgumentAttribute (string argument ); 
        public InterpolatedStringHandlerArgumentAttribute (params string[] 
arguments ); 
        public string[] Arguments { get; } 
    } 
} 
namespace  System 
{ 
    public sealed class String 
    { The questions we need to answer:
1. Do we like this pattern in general?
2. Do we want to allow these arguments to come from after the handler parameter?
Some existing patterns in the BCL, such as Utf8Formatter, put the value to be
formatted befor e the thing needed to format into. T o fit in best with these patterns,
we'd likely want to allow this, but we need to decide if this out-of-order evaluate is
ok.
Answer:
We want to support this. The spec has been updated to reflect this. Arguments will be
required to be specified in lexical order at the call site, and if a needed argument to the
create method is specified after the interpolated string literal, an error is produced.
Because $"{await A()}" is a valid expression today, we need to rationalize how
interpolation holes with await. W e could solve this with a few rules:        public static string Format(IFormatProvider? provider,  
[InterpolatedStringHandlerArgument( "provider" )] ref 
DefaultInterpolatedStringHandler handler) ; 
        …  
    } 
} 
namespace  System.Runtime.CompilerServices  
{ 
    public ref struct DefaultInterpolatedStringHandler  
    { 
        public DefaultInterpolatedStringHandler (int baseLength, int 
holeCount, IFormatProvider? provider ); // additional factory  
        …  
    } 
} 
var formatted = string.Format(CultureInfo.InvariantCulture, $"{X} = {Y}"); 
// Is lowered to  
var tmp1 = CultureInfo.InvariantCulture;  
var handler = new DefaultInterpolatedStringHandler( 3, 2, tmp1);  
handler.AppendFormatted(X);  
handler.AppendLiteral( " = "); 
handler.AppendFormatted(Y);  
var formatted = string.Format(tmp1, handler);  
await usage in interpolation holes1. If an interpolated string used as a string, IFormattable, or FormattableString has
an await in an interpolation hole, fall back to old-style formatter.
2. If an interpolated string is subject to an implicit_str ing_handler_c onversion and
applicable_int erpolat ed_str ing_handler_type  is a ref struct, await is not allowed
to be used in the format holes.
Fundamentally, this desugaring could use a ref struct in an async method as long as we
guarantee that the ref struct will not need to be saved to the heap, which should be
possible if we forbid awaits in the interpolation holes.
Alternatively, we could simply make all handler types non-ref structs, including the
framework handler for interpolated strings. This would, however, preclude us from
someday recognizing a Span version that does not need to allocate any scratch space at
all.
Answer:
We will treat interpolated string handlers the same as any other type: this means that if
the handler type is a ref struct and the current context doesn't allow the usage of ref
structs, it is illegal to use handler here. The spec around lowering of string literals used
as strings is intentionally vague to allow the compiler to decide on what rules it deems
appropriate, but for custom handler types they will have to follow the same rules as the
rest of the language.
Some handlers might want to be passed as ref parameters (either in or ref). Should we
allow either? And if so, what will a ref handler look like? ref $"" is confusing, as you're
not actually passing the string by ref, you're passing the handler that is created from the
ref by ref, and has similar potential issues with async methods.
Answer:
We want to support this. The spec has been updated to reflect this. The rules should
reflect the same rules that apply to extension methods on value types.
Because this proposal makes interpolated strings context sensitive, we would like to
allow the compiler to treat a binary expression composed entirely of interpolatedHandlers as ref parameters
Interpolated strings through binary expressions and
conversionsstrings, or an interpolated string subjected to a cast, as an interpolated string literal for
the purposes of overload resolution. For example, take the following scenario:
C#
This would be ambiguous, necessitating a cast to either Handler1 or Handler2 in order
to resolve. However, in making that cast, we would potentially throw away the
information that there is context from the method receiver, meaning that the cast would
fail because there is nothing to fill in the information of c. A similar issue arises with
binary concatenation of strings: the user could want to format the literal across several
lines to avoid line wrapping, but would not be able to because that would no longer be
an interpolated string literal convertible to the handler type.
To resolve these cases, we make the following changes:
An additiv e_expr ession  composed entirely of interpolat ed_str ing_expr essions  and
using only + operators is considered to be an interpolat ed_str ing_lit eral for the
purposes of conversions and overload resolution. The final interpolated string is
created by logically concatinating all individual interpolat ed_str ing_expr ession
components, from left to right.
A cast_expr ession  or a relational_expr ession  with operator as whose operand is an
interpolat ed_str ing_expr essions  is considered an interpolat ed_str ing_expr essions  for
the purposes of conversions and overload resolution.
Open Questions :struct Handler1  
{ 
    public Handler1 (int literalLength, int formattedCount, C c ) => ...;  
    // AppendX... methods as necessary  
} 
struct Handler2  
{ 
    public Handler2 (int literalLength, int formattedCount, C c ) => ...;  
    // AppendX... methods as necessary  
} 
class C 
{ 
    void M(Handler1 handler ) => ...;  
    void M(Handler2 handler ) => ...;  
} 
c.M($"{X}"); // Ambiguous between the M overloads  Do we want to do this? W e don't do this for System.FormattableString, for example, but
that can be broken out onto a different line, whereas this can be context-dependent and
therefore not able to be broken out into a different line. There are also no overload
resolution concerns with FormattableString and IFormattable.
Answer:
We think that this is a valid use case for additive expressions, but that the cast version is
not compelling enough at this time. W e can add it later if necessary. The spec has been
updated to reflect this decision.
See https://github.com/dotnet/runtime/issues/50635  for examples of proposed
handler APIs using this pattern.Other use cases
Constant Interpolated Strings
Article •06/23/2023
Enables constants to be generated from interpolated strings of type string constant.
The following code is already legal:
However, there have been many community requests to make the following also legal:７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
public class C  
{ 
    const string S1 = "Hello world";  
    const string S2 = "Hello" + " " + "World";  
    const string S3 = S1 + " Kevin, welcome to the team!";  
} 
public class C  
{ 
    const string S1 = $"Hello world";  
    const string S2 = $"Hello{" "}World";  
    const string S3 = $"{S1} Kevin, welcome to the team!";  
} This proposal represents the next logical step for constant string generation, where
existing string syntax that works in other situations is made to work for constants.
The following represent the updated specifications for constant expressions under this
new proposal. Current specifications from which this was directly based on can be found
in §11.20 .
A constant_expr ession  is an expression that can be fully evaluated at compile-time.
antlr
A constant expression must be the null literal or a value with one of the following
types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double,
decimal, bool, object, string, or any enumeration type. Only the following constructs
are permitted in constant expressions:
Literals (including the null literal).
References to const members of class and struct types.
References to members of enumeration types.
References to const parameters or local variables
Parenthesized sub-expressions, which are themselves constant expressions.
Cast expressions, provided the target type is one of the types listed above.
checked and unchecked expressions
Default value expressions
Nameof expressions
The predefined +, -, !, and ~ unary operators.
The predefined +, -, *, /, %, <<, >>, &, |, ^, &&, ||, ==, !=, <, >, <=, and >=
binary operators, provided each operand is of a type listed above.
The ?: conditional operator.
Interpolat ed str ings ${}, provided that all c omponents ar e constant expr essions o f
type string and all int erpolat ed components lack alignment and for mat speci fiers.
The following conversions are permitted in constant expressions:Detailed design
Constant Expressions
constant_expression  
    : expression  
    ; Identity conversions
Numeric conversions
Enumeration conversions
Constant expression conversions
Implicit and explicit reference conversions, provided that the source of the
conversions is a constant expression that evaluates to the null value.
Other conversions including boxing, unboxing and implicit reference conversions of
non-null values are not permitted in constant expressions. For example:
C#
the initialization of i is an error because a boxing conversion is required. The
initialization of str is an error because an implicit reference conversion from a non-null
value is required.
Whenever an expression fulfills the requirements listed above, the expression is
evaluated at compile-time. This is true even if the expression is a sub-expression of a
larger expression that contains non-constant constructs.
The compile-time evaluation of constant expressions uses the same rules as run-time
evaluation of non-constant expressions, except that where run-time evaluation would
have thrown an exception, compile-time evaluation causes a compile-time error to
occur.
Unless a constant expression is explicitly placed in an unchecked context, overflows that
occur in integral-type arithmetic operations and conversions during the compile-time
evaluation of the expression always cause compile-time errors ( §11.20 ).
Constant expressions occur in the contexts listed below. In these contexts, a compile-
time error occurs if an expression cannot be fully evaluated at compile-time.
Constant declarations ( §14.4 ).
Enumeration member declarations ( §18.4 ).
Default arguments of formal parameter lists ( §14.6.2 )
case labels of a switch statement ( §12.8.3 ).
goto case statements ( §12.10.4 ).class C  
{ 
    const object i = 5;         // error: boxing conversion not permitted  
    const object str = "hello"; // error: implicit reference conversion  
} 
Dimension lengths in an array creation expression ( §11.7.15.5 ) that includes an
initializer.
Attributes ( §21 ).
An implicit constant expression conversion ( §10.2.11 ) permits a constant expression of
type int to be converted to sbyte, byte, short, ushort, uint, or ulong, provided the
value of the constant expression is within the range of the destination type.
This proposal adds additional complexity to the compiler in exchange for broader
applicability of interpolated strings. As these strings are fully evaluated at compile time,
the valuable automatic formatting features of interpolated strings are less neccesary.
Most use cases can be largely replicated through the alternatives below.
The current + operator for string concatenation can combine strings in a similar manner
to the current proposal.
What parts of the design are still undecided?
Link to design notes that affect this proposal, and describe in one sentence for each
what changes they led to.
Drawbacks
Alternatives
Unresolved questions
Design meetingsLambda improvements
Article •06/23/2023
Proposed changes:
1. Allow lambdas with attributes
2. Allow lambdas with explicit return type
3. Infer a natural delegate type for lambdas and method groups
Support for attributes on lambdas would provide parity with methods and local
functions.
Support for explicit return types would provide symmetry with lambda parameters
where explicit types can be specified. Allowing explicit return types would also provide
control over compiler performance in nested lambdas where overload resolution must
bind the lambda body currently to determine the signature.
A natural type for lambda expressions and method groups will allow more scenarios
where lambdas and method groups may be used without an explicit delegate type,
including as initializers in var declarations.
Requiring explicit delegate types for lambdas and method groups has been a friction
point for customers, and has become an impediment to progress in ASP.NET with recent
work on MapAction .７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
ASP.NET MapAction  without proposed changes ( MapAction() takes a System.Delegate
argument):
C#
ASP.NET MapAction  with natural types for method groups:
C#
ASP.NET MapAction  with attributes and natural types for lambda expressions:
C#
Attributes may be added to lambda expressions and lambda parameters. T o avoid
ambiguity between method attributes and parameter attributes, a lambda expression
with attributes must use a parenthesized parameter list. P arameter types are not
required.
C#
[HttpGet( "/")] Todo GetTodo() => new(Id: 0, Name: "Name"); 
app.MapAction((Func<Todo>)GetTodo);  
[HttpPost( "/")] Todo PostTodo ([FromBody] Todo todo ) => todo;  
app.MapAction((Func<Todo, Todo>)PostTodo);  
[HttpGet( "/")] Todo GetTodo() => new(Id: 0, Name: "Name"); 
app.MapAction(GetTodo);  
[HttpPost( "/")] Todo PostTodo ([FromBody] Todo todo ) => todo;  
app.MapAction(PostTodo);  
app.MapAction([HttpGet( "/")] () => new Todo(Id: 0, Name: "Name")); 
app.MapAction([HttpPost( "/")] ([FromBody] Todo todo) => todo);  
Attributes
f = [A] () => { };        // [A] lambda  
f = [return:A] x => x;    // syntax error at '=>'  
f = [return:A] (x) => x;  // [A] lambda  
f = [A] static x => x;    // syntax error at '=>'  
f = ([A] x) => x;         // [A] x  
f = ([A] ref int x) => x; // [A] x  Multiple attributes may be specified, either comma-separated within the same attribute
list or as separate attribute lists.
C#
Attributes are not supported for anon ymous methods  declared with delegate { }
syntax.
C#
The parser will look ahead to differentiate a collection initializer with an element
assignment from a collection initializer with a lambda expression.
C#
The parser will treat ?[ as the start of a conditional element access.
C#
Attributes on the lambda expression or lambda parameters will be emitted to metadata
on the method that maps to the lambda.
In general, customers should not depend on how lambda expressions and local
functions map from source to metadata. How lambdas and local functions are emitted
can, and has, changed between compiler versions.
The changes proposed here are targeted at the Delegate driven scenario. It should be
valid to inspect the MethodInfo associated with a Delegate instance to determine the
signature of the lambda expression or local function including any explicit attributes and
additional metadata emitted by the compiler such as default parameters. This allows
teams such as ASP.NET to make available the same behaviors for lambdas and local
functions as ordinary methods.var f = [A1, A2][A3] () => { };    // ok 
var g = ([A1][A2, A3] int x) => x; // ok 
f = [A] delegate  { return 1; };         // syntax error at 'delegate'  
f = delegate  ([A] int x) { return x; }; // syntax error at '['  
var y = new C { [A] = x };    // ok: y[A] = x  
var z = new C { [A] x => x }; // ok: z[0] = [A] x => x  
x = b ? [A];               // ok 
y = b ? [A] () => { } : z; // syntax error at '('  An explicit return type may be specified before the parenthesized parameter list.
C#
The parser will look ahead to differentiate a method call T() from a lambda expression
T () => e.
Explicit return types are not supported for anonymous methods declared with delegate
{ } syntax.
C#
Method type inference should make an exact inference from an explicit lambda return
type.
C#
Variance conversions are not allowed from lambda return type to delegate return type
(matching similar behavior for parameter types).
C#
The parser allows lambda expressions with ref return types within expressions without
additional parentheses.
C#Explicit return type
f = T () => default;                    // ok 
f = short x => 1;                       // syntax error at '=>'  
f = ref int (ref int x) => ref x;       // ok 
f = static void (_) => { };             // ok 
f = async async (async async) => async; // ok?
f = delegate  int { return 1; };         // syntax error  
f = delegate  int (int x) { return x; }; // syntax error  
static void F<T>(Func<T, T> f) { ... }  
F(int (i) => i); // Func<int, int>  
Func<object> f1 = string () => null; // error  
Func<object?> f2 = object () => x;   // warning  var cannot be used as an explicit return type for lambda expressions.
C#
An anon ymous f unction  expression ( §11.16 ) (a lambda expr ession  or an anon ymous
method ) has a natural type if the parameters types are explicit and the return type is
either explicit or can be inferred (see §11.6.3.13 ).
A method gr oup has a natural type if all candidate methods in the method group have a
common signature. (If the method group may include extension methods, the
candidates include the containing type and all extension method scopes.)
The natural type of an anonymous function expression or method group is a
function_type . A function_type  represents a method signature: the parameter types and
ref kinds, and return type and ref kind. Anonymous function expressions or method
groups with the same signature have the same function_type .
Function_types  are used in a few specific contexts only:
implicit and explicit conversions
method type inference ( §11.6.3 ) and best common type ( §11.6.3.15 )
var initializers
A function_type  exists at compile time only: function_types  do not appear in source or
metadata.
From a function_type  F there are implicit function_type  conversions:d = ref int () => x; // d = (ref int () => x)  
F(ref int () => x);  // F((ref int () => x))  
class var { } 
d = var (var v) => v;              // error: contextual keyword 'var' cannot  
be used as explicit lambda return type  
d = @var (var v) => v;             // ok 
d = ref var (ref var v) => ref v;  // error: contextual keyword 'var' cannot  
be used as explicit lambda return type  
d = ref @var (ref var v) => ref v; // ok 
Natural (function) type
ConversionsTo a function_type  G if the parameters and return types of F are variance-
convertible to the parameters and return type of G
To System.MulticastDelegate or base classes or interfaces of
System.MulticastDelegate
To System.Linq.Expressions.Expression or
System.Linq.Expressions.LambdaExpression
Anonymous function expressions and method groups already have conversions fr om
expression  to delegate types and expression tree types (see anonymous function
conversions §10.7  and method group conversions §10.8 ). Those conversions are
sufficient for converting to strongly-typed delegate types and expression tree types. The
function_type  conversions above add conversions fr om type  to the base types only:
System.MulticastDelegate, System.Linq.Expressions.Expression, etc.
There are no conversions to a function_type  from a type other than a function_type .
There are no explicit conversions for function_types  since function_types  cannot be
referenced in source.
A conversion to System.MulticastDelegate or base type or interface realizes the
anonymous function or method group as an instance of an appropriate delegate type. A
conversion to System.Linq.Expressions.Expression<TDelegate> or base type realizes the
lambda expression as an expression tree with an appropriate delegate type.
C#
Function_type  conversions are not implicit or explicit standard conversions §10.4  and
are not considered when determining whether a user-defined conversion operator is
applicable to an anonymous function or method group. From evaluation of user defined
conversions §10.5.3 :
For a conversion operator to be applicable, it must be possible to perform a
standard conversion ( §10.4 ) from the source type to the operand type of the
operator, and it must be possible to perform a standard conversion from the result
type of the operator to the target type.
C#
Delegate d = delegate  (object obj) { }; // Action<object>  
Expression e = () => "";                // Expression<Func<string>>  
object o = "".Clone;                    // Func<object>  
A warning is reported for an implicit conversion of a method group to object, since the
conversion is valid but perhaps unintentional.
C#
The existing rules for type inference are mostly unchanged (see §11.6.3 ). There are
however a couple o f changes  below to specific phases of type inference.
The first phase ( §11.6.3.2 ) allows an anonymous function to bind to Ti even if Ti is
not a delegate or expression tree type (perhaps a type parameter constrained to
System.Delegate for instance).
For each of the method arguments Ei:
If Ei is an anonymous function and Ti is a delegat e type or expr ession tr ee
type, an explicit p aramet er type infer ence is made from Ei to Ti and an
explicit r eturn type infer ence is made fr om Ei to Ti.
Otherwise, if Ei has a type U and xi is a value parameter then a lower-bound
inference is made from U to Ti.
Otherwise, if Ei has a type U and xi is a ref or out parameter then an exact
inference is made from U to Ti.
Otherwise, no inference is made for this argument.class C 
{ 
    public static implicit  operator  C(Delegate d ) { ... }  
} 
C c; 
c = () => 1;      // error: cannot convert lambda expression to type 'C'  
c = (C)(() => 2); // error: cannot convert lambda expression to type 'C'  
Random r = new Random();  
object obj; 
obj = r.NextDouble;         // warning: Converting method group to 'object'.  
Did you intend to invoke the method?  
obj = (object)r.NextDouble; // ok 
Type inference
First phase
Explicit return type inference
An explicit r eturn type infer ence is made from an expr ession E to a type T in the
following way:
If E is an anonymous function with explicit r eturn type Ur and T is a
delegat e type or expr ession tr ee type with r eturn type Vr then an exact
infer ence (§11.6.3.9 ) is made from Ur to Vr.
Fixing ( §11.6.3.12 ) ensures other conversions are preferred over function_type
conversions. (Lambda expressions and method group expressions only contribute to
lower bounds so handling of function_types  is needed for lower bounds only.)
An unfixed type variable Xi with a set of bounds is fixed as follows:
The set of candidat e types  Uj starts out as the set of all types in the set of
bounds for Xi wher e function types ar e ignor ed in low er bounds if ther e any
types that ar e not function types .
We then examine each bound for Xi in turn: For each exact bound U of Xi all
types Uj which are not identical to U are removed from the candidate set. For
each lower bound U of Xi all types Uj to which there is not an implicit
conversion from U are removed from the candidate set. For each upper bound
U of Xi all types Uj from which there is not an implicit conversion to U are
removed from the candidate set.
If among the remaining candidate types Uj there is a unique type V from
which there is an implicit conversion to all the other candidate types, then Xi
is fixed to V.
Otherwise, type inference fails.
Best common type ( §11.6.3.15 ) is defined in terms of type inference so the type
inference changes above apply to best common type as well.
C#
Fixing
Best common type
var fs = new[] { (string s) => s.Length; ( string s) => int.Parse(s) } // 
Func<string, int>[]  Anonymous functions and method groups with function types can be used as initializers
in var declarations.
C#
Function types are not used in assignments to discards.
C#
The delegate type for the anonymous function or method group with parameter types
P1, ..., Pn and return type R is:
if any parameter or return value is not by value, or there are more than 16
parameters, or any of the parameter types or return are not valid type arguments
(say, (int* p) => { }), then the delegate is a synthesized internal anonymous
delegate type with signature that matches the anonymous function or method
group, and with parameter names arg1, ..., argn or arg if a single parameter;
if R is void, then the delegate type is System.Action<P1, ..., Pn>;
otherwise the delegate type is System.Func<P1, ..., Pn, R>.
The compiler may allow more signatures to bind to System.Action<> and System.Func<>
types in the future (if ref struct types are allowed type arguments for instance).var
var f1 = () => default;           // error: cannot infer type  
var f2 = x => x;                  // error: cannot infer type  
var f3 = () => 1;                 // System.Func<int>  
var f4 = string () => null;       // System.Func<string>  
var f5 = delegate  (object o) { }; // System.Action<object>  
static void F1() { } 
static void F1<T>(this T t) { }  
static void F2(this string s) { } 
var f6 = F1;    // error: multiple methods  
var f7 = "".F1; // System.Action  
var f8 = F2;    // System.Action<string>  
d = () => 0; // ok 
_ = () => 1; // error  
Delegate typesmodopt() or modreq() in the method group signature are ignored in the corresponding
delegate type.
If two anonymous functions or method groups in the same compilation require
synthesized delegate types with the same parameter types and modifiers and the same
return type and modifiers, the compiler will use the same synthesized delegate type.
Better function member ( §11.6.4.3 ) is updated to prefer members where none of the
conversions and none of the type arguments involved inferred types from lambda
expressions or method groups.
Better function member
... Given an argument list A with a set of argument expressions {E1, E2, ..., En}
and two applicable function members Mp and Mq with parameter types {P1, P2,
..., Pn} and {Q1, Q2, ..., Qn}, Mp is defined to be a better function member
than Mq if
1. for each ar gument, the implicit conv ersion fr om Ex to Px is not a
function_type_c onversion, and
Mp is a non-generic method or Mp is a generic method with type
paramet ers {X1, X2, ..., Xp} and for each type p aramet er Xi the type
argument is inferr ed fr om an expr ession or fr om a type other than a
function_type , and
for at least one ar gument, the implicit conv ersion fr om Ex to Qx is a
function_type_c onversion, or Mq is a generic method with type
paramet ers {Y1, Y2, ..., Yq} and for at least one type p aramet er Yi
the type ar gument is inferr ed fr om a function_type , or
2. for each argument, the implicit conversion from Ex to Qx is not better than
the implicit conversion from Ex to Px, and for at least one argument, the
conversion from Ex to Px is better than the conversion from Ex to Qx.
Better conversion from expression ( §11.6.4.4 ) is updated to prefer conversions that did
not involve inferred types from lambda expressions or method groups.
Better conversion from expressionOverload resolution
Given an implicit conversion C1 that converts from an expression E to a type T1,
and an implicit conversion C2 that converts from an expression E to a type T2, C1
is a better conversion than C2 if:
1. C1 is not a function_type_c onversion and C2 is a function_type_c onversion, or
2. E is a non-constant interpolat ed_str ing_expr ession , C1 is an
implicit_str ing_handler_c onversion, T1 is an
applicable_int erpolat ed_str ing_handler_type , and C2 is not an
implicit_str ing_handler_c onversion, or
3. E does not exactly match T2 and at least one of the following holds:
E exactly matches T1 (§11.6.4.4 )
T1 is a better conversion target than T2 (§11.6.4.6 )
antlr
Should default values be supported for lambda expression parameters for
completeness?
Should System.Diagnostics.ConditionalAttribute be disallowed on lambda expressions
since there are few scenarios where a lambda expression could be used conditionally?
C#
Syntax
lambda_expression  
  : modifier* identifier '=>' (block | expression)  
  | attribute_list* modifier* type? lambda_parameters '=>' (block |  
expression)  
  ; 
lambda_parameters  
  : lambda_parameter  
  | '(' (lambda_parameter ( ',' lambda_parameter)*)? ')' 
  ; 
lambda_parameter  
  : identifier  
  | attribute_list* modifier* type? identifier equals_value_clause?  
  ; 
Open issuesShould the function_type  be available from the compiler API, in addition to the resulting
delegate type?
Currently, the inferred delegate type uses System.Action<> or System.Func<> when
parameter and return types are valid type arguments and there are no more than 16
parameters, and if the expected Action<> or Func<> type is missing, an error is reported.
Instead, should the compiler use System.Action<> or System.Func<> regardless of arity?
And if the expected type is missing, synthesize a delegate type otherwise?([Conditional( "DEBUG")] static (x, y) => Assert(x == y))(a, b); // ok? CallerArgumentExpression
Article •06/23/2023
Allow developers to capture the expressions passed to a method, to enable better error
messages in diagnostic/testing APIs and reduce keystrokes.
When an assertion or argument validation fails, the developer wants to know as much as
possible about where and why it failed. However, today's diagnostic APIs do not fully
facilitate this. Consider the following method:
C#
When one of the asserts fail, only the filename, line number, and method name will be
provided in the stack trace. The developer will not be able to tell which assert failed
from this information-- they will have to open the file and navigate to the provided line
number to see what went wrong.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
T Single<T>( this T[] array)  
{ 
    Debug.Assert(array != null); 
    Debug.Assert(array.Length == 1); 
    return array[0]; 
} This is also the reason testing frameworks have to provide a variety of assert methods.
With xUnit, Assert.True and Assert.False are not frequently used because they do not
provide enough context about what failed.
While the situation is a bit better for argument validation because the names of invalid
arguments are shown to the developer, the developer must pass these names to
exceptions manually. If the above example were rewritten to use traditional argument
validation instead of Debug.Assert, it would look like
C#
Notice that nameof(array) must be passed to each exception, although it's already clear
from context which argument is invalid.
In the above examples, including the string "array != null" or "array.Length == 1" in
the assert message would help the developer determine what failed. Enter
CallerArgumentExpression: it's an attribute the framework can use to obtain the string
associated with a particular method argument. W e would add it to Debug.Assert like so
C#T Single<T>( this T[] array)  
{ 
    if (array == null) 
    { 
        throw new ArgumentNullException( nameof(array));  
    } 
    if (array.Length != 1) 
    { 
        throw new ArgumentException( "Array must contain a single element." , 
nameof(array));  
    } 
    return array[0]; 
} 
Detailed design
public static class Debug 
{ 
    public static void Assert(bool condition,  
[CallerArgumentExpression( "condition" )] string message  = null); 
} The source code in the above example would stay the same. However, the code the
compiler actually emits would correspond to
C#
The compiler specially recognizes the attribute on Debug.Assert. It passes the string
associated with the argument referred to in the attribute's constructor (in this case,
condition) at the call site. When either assert fails, the developer will be shown the
condition that was false and will know which one failed.
For argument validation, the attribute cannot be used directly, but can be made use of
through a helper class:
C#T Single<T>( this T[] array)  
{ 
    Debug.Assert(array != null, "array != null" ); 
    Debug.Assert(array.Length == 1, "array.Length == 1" ); 
    return array[0]; 
} 
public static class Verify 
{ 
    public static void Argument (bool condition, string message,  
[CallerArgumentExpression( "condition" )] string conditionExpression  = null) 
    { 
        if (!condition) throw new ArgumentException(message: message,  
paramName: conditionExpression);  
    } 
    public static void InRange(int argument, int low, int high, 
        [CallerArgumentExpression( "argument" )] string argumentExpression  = 
null, 
        [ CallerArgumentExpression( "low")] string lowExpression = null, 
        [ CallerArgumentExpression( "high")] string highExpression = null) 
    { 
        if (argument < low)  
        {  
            throw new ArgumentOutOfRangeException(paramName:  
argumentExpression,  
                message: $"{argumentExpression}  ({argument} ) cannot be less  
than {lowExpression}  ({low})."); 
        }  
        if (argument > high)  
        {  
            throw new ArgumentOutOfRangeException(paramName:  
argumentExpression,  A proposal to add such a helper class to the framework is underway at
https://github.com/dotnet/corefx/issues/17068 . If this language feature was
implemented, the proposal could be updated to take advantage of this feature.
The this parameter in an extension method may be referenced by
CallerArgumentExpression. For example:
C#                message: $"{argumentExpression}  ({argument} ) cannot be  
greater than {highExpression}  ({high})."); 
        }  
    } 
    public static void NotNull<T>(T argument,  
[CallerArgumentExpression( "argument" )] string argumentExpression = null) 
        where T : class 
    { 
        if (argument == null) throw new ArgumentNullException(paramName:  
argumentExpression);  
    } 
} 
T Single<T>( this T[] array)  
{ 
    Verify.NotNull(array); // paramName: "array"  
    Verify.Argument(array.Length == 1, "Array must contain a single  
element." ); // paramName: "array.Length == 1"  
    return array[0]; 
} 
T ElementAt (this T[] array, int index) 
{ 
    Verify.NotNull(array); // paramName: "array"  
    // paramName: "index"  
    // message: "index (-1) cannot be less than 0 (0).", or  
    //          "index (6) cannot be greater than array.Length - 1 (5)."  
    Verify.InRange(index, 0, array.Length - 1); 
    return array[index];  
} 
Extension methods
public static void ShouldBe<T>( this T @this, T expected,  
[CallerArgumentExpression( "this")] string thisExpression = null) {} 
contestant.Points.ShouldBe( 1337); // thisExpression: "contestant.Points"  thisExpression will receive the expression corresponding to the object before the dot. If
it's called with static method syntax, e.g. Ext.ShouldBe(contestant.Points, 1337), it will
behave as if first parameter wasn't marked this.
There should always be an expression corresponding to the this parameter. Even if an
instance of a class calls an extension method on itself, e.g. this.Single() from inside a
collection type, the this is mandated by the compiler so "this" will get passed. If this
rule is changed in the future, we can consider passing null or the empty string.
Like the other Caller* attributes, such as CallerMemberName, this attribute may
only be used on parameters with default values.
Multiple parameters marked with CallerArgumentExpression are permitted, as
shown above.
The attribute's namespace will be System.Runtime.CompilerServices.
If null or a string that is not a parameter name (e.g. "notAParameterName") is
provided, the compiler will pass in an empty string.
The type of the parameter CallerArgumentExpressionAttribute is applied to must
have a standard conversion from string. This means no user-defined conversions
from string are allowed, and in practice means the type of such a parameter must
be string, object, or an interface implemented by string.
People who know how to use decompilers will be able to see some of the source
code at call sites for methods marked with this attribute. This may be
undesirable/unexpected for closed-source software.
Although this is not a flaw in the feature itself, a source of concern may be that
there exists a Debug.Assert API today that only takes a bool. Even if the overload
taking a message had its second parameter marked with this attribute and made
optional, the compiler would still pick the no-message one in overload resolution.
Therefore, the no-message overload would have to be removed to take advantage
of this feature, which would be a binary (although not source) breaking change.Extra details
Drawbacks
AlternativesIf being able to see source code at call sites for methods that use this attribute
proves to be a problem, we can make the attribute's effects opt-in. Developers will
enable it through an assembly-wide [assembly: EnableCallerArgumentExpression]
attribute they put in AssemblyInfo.cs.
In the case the attribute's effects are not enabled, calling methods marked with
the attribute would not be an error, to allow existing methods to use the
attribute and maintain source compatibility. However, the attribute would be
ignored and the method would be called with whatever default value was
provided.
C#
To prevent the binary compatibility problem  from occurring every time we want to
add new caller info to Debug.Assert, an alternative solution would be to add a
CallerInfo struct to the framework that contains all the necessary information
about the caller.
C#// Assembly1  
void Foo(string bar); // V1 
void Foo(string bar, string barExpression = "not provided" ); // V2 
void Foo(string bar, [CallerArgumentExpression( "bar")] string barExpression  
= "not provided" ); // V3 
// Assembly2  
Foo(a); // V1: Compiles to Foo(a), V2, V3: Compiles to Foo(a, "not  
provided")  
Foo(a, "provided" ); // V2, V3: Compiles to Foo(a, "provided")  
// Assembly3  
[assembly: EnableCallerArgumentExpression ] 
Foo(a); // V1: Compiles to Foo(a), V2: Compiles to Foo(a, "not provided"),  
V3: Compiles to Foo(a, "a")  
Foo(a, "provided" ); // V2, V3: Compiles to Foo(a, "provided")  
struct CallerInfo  
{ 
    public string MemberName { get; set; } 
    public string TypeName { get; set; } 
    public string Namespace { get; set; } 
    public string FullTypeName { get; set; } 
    public string FilePath { get; set; } 
    public int LineNumber { get; set; } This was originally proposed at https://github.com/dotnet/csharplang/issues/87 .
There are a few disadvantages of this approach:
Despite being pay-for-play friendly by allowing you to specify which properties
you need, it could still hurt perf significantly by allocating an array for the
expressions/calling MethodBase.GetCurrentMethod even when the assert passes.    public int ColumnNumber { get; set; } 
    public Type Type { get; set; } 
    public MethodBase Method { get; set; } 
    public string[] ArgumentExpressions { get; set; } 
} 
[Flags] 
enum CallerInfoOptions  
{ 
    MemberName = 1, TypeName = 2, ... 
} 
public static class Debug 
{ 
    public static void Assert(bool condition,  
        // If a flag is not set here, the corresponding CallerInfo member is 
not populated by the caller, so it 's 
        // pay-for-play friendly.
        [CallerInfo(CallerInfoOptions.FilePath | CallerInfoOptions.Method |  
CallerInfoOptions.ArgumentExpressions)] CallerInfo callerInfo =  
default(CallerInfo))  
    { 
        string filePath = callerInfo.FilePath;  
        MethodBase method = callerInfo.Method;  
        string conditionExpression = callerInfo.ArgumentExpressions[0];  
        //...  
    } 
} 
class Bar  
{ 
    void Foo()  
    { 
        Debug.Assert(false);  
        // Translates to:  
        var callerInfo = new CallerInfo();  
        callerInfo.FilePath = @"C:\Bar.cs";  
        callerInfo.Method = MethodBase.GetCurrentMethod();  
        callerInfo.ArgumentExpressions = new string[] { "false" };  
        Debug.Assert(false, callerInfo);  
    } 
} 
Additionally, while passing a new flag to the CallerInfo attribute won't be a
breaking change, Debug.Assert won't be guaranteed to actually receive that new
parameter from call sites that compiled against an old version of the method.
TBD
N/AUnresolved questions
Design meetingsEnhanced #line directives
Article •01/24/2023
The compiler applies the mapping defined by #line directives to diagnostic locations
and sequence points emitted to the PDB.
Currently only the line number and file path can be mapped while the starting character
is inferred from the source code. The proposal is to allow specifying full span mapping.
DSLs that generate C# source code (such as ASP.NET Razor) can't currently produce
precise source mapping using #line directives. This results in degraded debugging
experience in some cases as the sequence points emitted to the PDB can't map to the
precise location in the original source code.
For example, the following Razor code
generates code like so (simplified):
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
@page "/"  
Time: @DateTime.Now  The above directive would map the sequence point emitted by the compiler for the
_builder.Add(DateTime.Now); statement to the line 2, but the column would be off (16
instead of 7).
The Razor source generator actually incorrectly generates the following code:
C#
The intent was to preserve the starting character and it works for diagnostic location
mapping. However, this does not work for sequence points since #line directive only
applies to the sequence points that follow it. There is no sequence point in the middle of
the _builder.Add(DateTime.Now); statement (sequence points can only be emitted at IL
instructions with empty evaluation stack). The #line 2 directive in above code thus has
no effect on the generated PDB and the debugger won't place a breakpoint or stop on
the @DateTime.Now snippet in the Razor page.
Issues addressed by this proposal: https://github.com/dotnet/roslyn/issues/43432
https://github.com/dotnet/roslyn/issues/46526
We amend the syntax of line_indicator used in pp_line directive like so:
Current:#line hidden 
void Render() 
{ 
   _builder.Add( "Time:"); 
#line 2 "page.razor"  
   _builder.Add(DateTime.Now);  
#line hidden 
} 
#line hidden 
void Render() 
{ 
   _builder.Add( "Time:"); 
   _builder.Add(  
#line 2 "page.razor"  
      DateTime.Now  
#line hidden 
); 
} 
Detailed designProposed:
That is, the #line directive would accept either 5 decimal numbers ( start line , start
character, end line , end char acter, character offset), 4 decimal numbers ( start line , start
character, end line , end char acter), or a single one ( line).
If character offset is not specified its default value is 0, otherwise it specifies the number
of UTF-16 characters. The number must be non-negative and less then length of the line
following the #line directive in the unmapped file.
(start line , start char acter)-(end line , end char acter) specifies a span in the mapped file.
start line  and end line  are positive integers that specify line numbers. start char acter, end
character are positive integers that specify UTF-16 character numbers. start line , start
character, end line , end char acter are 1-based, meaning that the first line of the file and
the first UTF-16 character on each line is assigned number 1.
The implementation would constraint these numbers so that they specify a valid
sequence point source span :
start line  - 1 is within range [0, 0x20000000) and not equal to 0xfeefee.
end line  - 1 is within range [0, 0x20000000) and not equal to 0xfeefee.
start char acter - 1 is within range [0, 0x10000)
end char acter - 1 is within range [0, 0x10000)
end line  is greater or equal to start line .line_indicator  
    : decimal_digit+ whitespace file_name  
    | decimal_digit+  
    | 'default'  
    | 'hidden'  
    ; 
line_indicator  
    : '(' decimal_digit+ ',' decimal_digit+ ')' '-' '(' decimal_digit+ ','  
decimal_digit+ ')' whitespace decimal_digit+ whitespace file_name  
    | '(' decimal_digit+ ',' decimal_digit+ ')' '-' '(' decimal_digit+ ','  
decimal_digit+ ')' whitespace file_name  
    | decimal_digit+ whitespace file_name  
    | decimal_digit+  
    | 'default'  
    | 'hidden'  
    ; 
start line  is equal to end line  then end char acter is greater than start char acter.
Note that the numbers specified in the directive syntax are 1-based numbers but
the actual spans in the PDB are zero-based. Hence the -1 adjustments above.
The mapped spans of sequence points and the locations of diagnostics that #line
directive applies to are calculated as follows.
Let d be the zero-based number of the unmapped line containing the #line directive.
Let span L = (start: ( start line  - 1, start char acter - 1), end: ( end line  - 1, end char acter - 1))
be zero-based span specified by the directive.
Function M that maps a position (line, character) within the scope of the #line directive
in the source file containing the #line directive to a mapped position (mapped line,
mapped character) is defined as follows:
M(l, c) =
l == d + 1 => ( L.start.line  + l – d – 1, L.start.char acter + max( c – character offset, 0))
l > d + 1 => ( L.start.line  + l – d – 1, c)
The syntax constructs that sequence points are associated with are determined by the
compiler implementation and not covered by this specification. The compiler also
decides for each sequence point its unmapped span. This span may partially or fully
cover the associated syntax construct.
Once the unmapped spans are determined by the compiler the function M defined
above is applied to their starting and ending positions, with the exception of the ending
position of all sequence points within the scope of the #line directive whose unmapped
location is at line d + 1 and character less than character offset. The end position of all
these sequence points is L.end .
Example [5.i] demonstrates why it is necessary to provide the ability to specify the
end position of the first sequence point span.
The above definition allows the generator of the unmapped source code to avoid
intimate knowledge of which exact source constructs of the C# language produce
sequence points. The mapped spans of the sequence points in the scope of the
#line directive are derived from the relative position of the corresponding
unmapped spans to the first unmapped span.Specifying the character offset allows the generator to insert any single-line prefix on
the first line. This prefix is generated code that is not present in the mapped file.
Such inserted prefix affects the value of the first unmapped sequence point span.
Therefore the starting character of subsequent sequence point spans need to be
offset by the length of the prefix ( character offset). See example [2].
For clarity the examples use spanof('...') and lineof('...') pseudo-syntax to
express the mapped span start position and line number, respectively, of the specified
code snippet.
Consider the following code with unmapped zero-based line numbers listed on the
right:
d = 3 L = (0, 9)..(0, 14)Examples
1. First and subsequent spans
#line (1,10)-(1,15) "a" // 3  
  A();B(                // 4  
);C();                  // 5  
    D();                // 6  There are 4 sequence point spans the directive applies to with following unmapped and
mapped spans: (4, 2)..(4, 5) => (0, 9)..(0, 14) (4, 6)..(5, 1) => (0, 15)..(1, 1) (5, 2)..(5, 5) =>
(1, 2)..(1, 5) (6, 4)..(6, 7) => (2, 4)..(2, 7)
Razor generates _builder.Add( prefix of length 15 (including two leading spaces).
Razor:
Generated C#:
C#
d = 4 L = (1, 1)..(3,0) character offset = 15
Spans:
_builder.Add(F(…)); => F(…): (5, 2)..(7, 2) => (1, 1)..(3, 0)
1+1 => 1+1: (5, 23)..(5, 25) => (1, 9)..(1, 11)
2+2 => 2+2: (6, 7)..(6, 9) => (2, 7)..(2, 9)
Razor:2. Character offset
@page "/"                                   
@F(() => 1+1,  
   () => 2+2  
)  
#line hidden 
void Render()             
{  
#line spanof('F(...)') 15 "page.razor"  // 4  
  _builder.Add(F(() => 1+1,            // 5 
  () => 2+2                            // 6 
));                                    // 7 
#line hidden 
} 
); 
} 
3. Razor: Single-line spanGenerated C#:
C#
Razor:
Generated C#:
C#@page "/"  
Time: @DateTime.Now  
#line hidden 
void Render() 
{ 
  _builder.Add( "Time:"); 
#line spanof('DateTime.Now') 15 "page.razor"  
  _builder.Add(DateTime.Now);  
#line hidden 
); 
} 
4. Razor: Multi-line span
@page "/"                                   
@JsonToHtml(@"  
{ 
  ""key1"": "value1",  
  ""key2"": "value2"  
}")  
#line hidden 
void Render() 
{ 
  _builder.Add( "Time:"); 
#line spanof('JsonToHtml(@"...")') 15 "page.razor"  
  _builder.Add(JsonToHtml( @" 
{ 
  ""key1"": " value1", 
  ""key2"": "value2" 
}")); 
#line hidden 
} 
); 
} In this example, the mapped span of the first sequence point that is associated with the
IL instruction that is emitted for the _builder.Add(Html.Helper(() => statement needs
to cover the whole expression of Html.Helper(...) in the generated file a.razor. This is
achieved by application of rule [1] to the end position of the sequence point.
C#
Uses existing #line line file form since
a) Razor does not add any prefix, b) { is not present in the generated file and there
can't be a sequence point placed on it, therefore the span of the first unmapped
sequence point is unknown to Razor.
The starting character of Console in the generated file must be aligned with the Razor
file.5. Razor: block constructs
i. block containing expressions
@Html.Helper(() =>  
{ 
    <p>Hello World</p>  
    @DateTime.Now  
}) 
#line spanof('Html.Helper(() => { ... })') 13 "a.razor"  
_builder.Add(Html.Helper(() =>  
#line lineof('{') "a.razor"  
{ 
#line spanof('DateTime.Now') 13 "a.razor"  
_builder.Add(DateTime.Now);  
#line lineof('}') "a.razor"  
} 
#line hidden 
) 
ii. block containing statementsC#
Uses existing #line line file form since
a) Razor does not add any prefix, b) { is not present in the generated file and there
can't be a sequence point placed on it, therefore the span of the first unmapped
sequence point is unknown to Razor.
The starting character of [Parameter] in the generated file must be aligned with the
Razor file.
C#
Uses existing #line line file form since a) Razor does not add any prefix. b) the span
of the first unmapped sequence point may not be known to Razor (or shouldn't need to
know).
The starting character of the keyword in the generated file must be aligned with the
Razor file.@{Console.WriteLine(1);Console.WriteLine(2);}  
#line lineof('@{') "a.razor"  
  Console.WriteLine( 1);Console.WriteLine( 2); 
#line hidden 
iii. block containing top-level code (@code, @functions)
@code { 
    [Parameter]  
    public int IncrementAmount { get; set; }  
} 
#line lineof('[') "a.razor"  
    [Parameter ] 
    public int IncrementAmount { get; set; } 
#line hidden 
6. Razor: @for, @foreach, @while, @do, @if, @switch, @using, @try,
@lockC#@for (var i = 0; i < 10; i++)  
{ 
} 
@if (condition)  
{ 
} 
else 
{ 
} 
#line lineof('for') "a.razor"  
 for (var i = 0; i < 10; i++) 
{ 
} 
#line lineof(' if') "a.razor"  
 if (condition)  
{ 
} 
else 
{ 
} 
#line hidden Improved Definite Assignment Analysis
Article •05/29/2022
Definite assignment §9.4  as specified has a few gaps which have caused users
inconvenience. In particular, scenarios involving comparison to boolean constants,
conditional-access, and null coalescing.
csharplang discussion of this proposal:
https://github.com/dotnet/csharplang/discussions/4240
Probably a dozen or so user reports can be found via this or similar queries (i.e. search
for "definite assignment" instead of "CS0165", or search in csharplang).
https://github.com/dotnet/roslyn/issues?
q=is%3Aclosed+is%3Aissue+label%3A%22R esolution-By+Design%22+cs0165
I have included related issues in the scenarios below to give a sense of the relative
impact of each scenario.
As a point of reference, let's start with a well-known "happy case" that does work in
definite assignment and in nullable.
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Related discussions and issues
Scenarioshttps://github.com/dotnet/csharplang/discussions/801
https://github.com/dotnet/roslyn/issues/45582
Links to 4 other issues where people were affected by this.
C#
https://github.com/dotnet/roslyn/issues/33559
https://github.com/dotnet/csharplang/discussions/4214
https://github.com/dotnet/csharplang/issues/3659
https://github.com/dotnet/csharplang/issues/3485
https://github.com/dotnet/csharplang/issues/3659#nullable enable  
C c = new C(); 
if (c != null && c.M( out object obj0)) 
{ 
    obj0.ToString(); // ok 
} 
public class C 
{ 
    public bool M(out object obj) 
    { 
        obj = new object(); 
        return true; 
    } 
} 
Comparison to bool constant
if ((c != null && c.M( out object obj1)) == true) 
{ 
    obj1.ToString(); // undesired error  
} 
if ((c != null && c.M( out object obj2)) is true) 
{ 
    obj2.ToString(); // undesired error  
} 
Comparison between a conditional access and a constant
value
This scenario is probably the biggest one. W e do support this in nullable but not in
definite assignment.
C#
https://github.com/dotnet/csharplang/discussions/916
https://github.com/dotnet/csharplang/issues/3365
This scenario is very similar to the previous one. This is also supported in nullable but
not in definite assignment.
C#
https://github.com/dotnet/roslyn/issues/4272
It's worth pointing out that we already have special behavior for when the condition
expression is constant (i.e. true ? a : b). We just unconditionally visit the arm indicated
by the constant condition and ignore the other arm.
Also note that we haven't handled this scenario in nullable.
C#if (c?.M(out object obj3) == true) 
{ 
    obj3.ToString(); // undesired error  
} 
Conditional access coalesced to a bool constant
if (c?.M(out object obj4) ?? false) 
{ 
    obj4.ToString(); // undesired error  
} 
Conditional expressions where one arm is a bool constant
if (c != null ? c.M(out object obj4) : false) 
{ 
    obj4.ToString(); // undesired error  
} 
SpecificationWe introduce a new section ?. (null-conditional operat or) expr essions . See the null-
conditional operator specification ( §11.7.7 )and Precise rules for determining definite
assignment §9.4.4  for context.
As in the definite assignment rules linked above, we refer to a given initially unassigned
variable as v.
We introduce the concept of "directly contains". An expression E is said to "directly
contain" a subexpression E if it is not subject to a user-defined conversion §10.5
whose parameter is not of a non-nullable value type, and one of the following
conditions holds:
E is E. For example, a?.b() directly contains the expression a?.b().
If E is a parenthesized expression (E2), and E directly contains E.
If E is a null-forgiving operator expression E2!, and E directly contains E.
If E is a cast expression (T)E2, and the cast does not subject E to a non-lifted
user-defined conversion whose parameter is not of a non-nullable value type, and
E directly contains E.
For an expression E of the form primary_expression null_conditional_operations, let E
be the expression obtained by textually removing the leading ? from each of the
null_c onditional_oper ations  of E that have one, as in the linked specification above.
In subsequent sections we will refer to E as the non-c onditional c ounterpart to the null-
conditional expression. Note that some expressions in subsequent sections are subject
to additional rules that only apply when one of the operands directly contains a null-
conditional expression.
The definite assignment state of v at any point within E is the same as the definite
assignment state at the corresponding point within E0.
The definite assignment state of v after E is the same as the definite assignment
state of v after primary_expr ession .
We use the concept of "directly contains" to allow us to skip over relatively simple
"wrapper" expressions when analyzing conditional accesses that are compared to other
values. For example, ((a?.b(out x))!) == true is expected to result in the same flow
state as a?.b == true in general.?. (null-conditional operator) expressions
1
1
2 1
2 1
2
2 1
0
0
RemarksWe also want to allow analysis to function in the presence of a number of possible
conversions on a conditional access. Propagating out "state when not null" is not
possible when the conversion is user-defined, though, since we can't count on user-
defined conversions to honor the constraint that the output is non-null only if the input
is non-null. The only exception to this is when the user-defined conversion's input is a
non-nullable value type. For example:
C#
This also includes lifted conversions like the following:
C#
When we consider whether a variable is assigned at a given point within a null-
conditional expression, we simply assume that any preceding null-conditional
operations within the same null-conditional expression succeeded.
For example, given a conditional expression a?.b(out x)?.c(x), the non-conditional
counterpart is a.b(out x).c(x). If we want to know the definite assignment state of x
before ?.c(x), for example, then we perform a "hypothetical" analysis of a.b(out x)
and use the resulting state as an input to ?.c(x).
We introduce a new section "Boolean constant expressions":public struct S1 { } 
public struct S2 { public static implicit  operator  S2?(S1 s1) => null; } 
string x; 
S1? s1 = null; 
_ = s1?.M1(x = "a") ?? s1.Value.M2(x = "a"); 
x.ToString(); // ok 
public struct S1 
{ 
    public S1 M1(object obj) => this; 
    public S2 M2(object obj) => new S2(); 
} 
public struct S2 
{ 
    public static implicit  operator  S2(S1 s1) => null; 
} 
Boolean constant expressionsFor an expression expr where expr is a constant expression with a bool value:
The definite assignment state of v after expr is determined by:
If expr is a constant expression with value true, and the state of v before expr is
"not definitely assigned", then the state of v after expr is "definitely assigned
when false".
If expr is a constant expression with value false, and the state of v before expr is
"not definitely assigned", then the state of v after expr is "definitely assigned
when true".
We assume that if an expression has a constant value bool false, for example, it's
impossible to reach any branch that requires the expression to return true. Therefore
variables are assumed to be definitely assigned in such branches. This ends up
combining nicely with the spec changes for expressions like ?? and ?: and enabling a
lot of useful scenarios.
It's also worth noting that we never expect to be in a conditional state befor e visiting a
constant expression. That's why we do not account for scenarios such as " expr is a
constant expression with value true, and the state of v before expr is "definitely assigned
when true".
We augment section §9.4.4.29  as follows:
For an expression expr of the form expr_first ?? expr_second:
...
The definite assignment state of v after expr is determined by:
...
If expr_f irst directly contains a null-conditional expression E, and v is definitely
assigned after the non-conditional counterpart E, then the definite assignment
state of v after expr is the same as the definite assignment state of v after
expr_s econd.
The above rule formalizes that for an expression like a?.M(out x) ?? (x = false), either
the a?.M(out x) was fully evaluated and produced a non-null value, in which case x wasRemarks
?? (null-coalescing expressions) augment
0
Remarksassigned, or the x = false was evaluated, in which case x was also assigned. Therefore
x is always assigned after this expression.
This also handles the dict?.TryGetValue(key, out var value) ?? false scenario, by
observing that v is definitely assigned after dict.TryGetValue(key, out var value), and
v is "definitely assigned when true" after false, and concluding that v must be
"definitely assigned when true".
The more general formulation also allows us to handle some more unusual scenarios,
such as:
if (x?.M(out y) ?? (b && z.M(out y))) y.ToString();
if (x?.M(out y) ?? z?.M(out y) ?? false) y.ToString();
We augment section §9.4.4.30  as follows:
For an expression expr of the form expr_cond ? expr_true : expr_false:
...
The definite assignment state of v after expr is determined by:
...
If the state of v after expr_tr ue is "definitely assigned when true", and the state
of v after expr_fals e is "definitely assigned when true", then the state of v after
expr is "definitely assigned when true".
If the state of v after expr_tr ue is "definitely assigned when false", and the state
of v after expr_fals e is "definitely assigned when false", then the state of v after
expr is "definitely assigned when false".
This makes it so when both arms of a conditional expression result in a conditional state,
we join the corresponding conditional states and propagate it out instead of unsplitting
the state and allowing the final state to be non-conditional. This enables scenarios like
the following:
C#?: (conditional) expressions
Remarks
bool b = true; 
object x = null; 
int y; 
if (b ? x != null && Set( out y) : x != null && Set( out y)) This is an admittedly niche scenario, that compiles without error in the native compiler,
but was broken in R oslyn in order to match the specification at the time. See internal
issue .
We introduce a new section ==/!= (r elational equality operat or) expr essions .
The general rules for expressions with embedded expressions §9.4.4.23  apply, except
for the scenarios described below.
For an expression expr of the form expr_first == expr_second, where == is a[predefined
comparison operator ( §11.11 ) or a lifted operator ( §11.4.8 ), the definite assignment
state of v after expr is determined by:
If expr_f irst directly contains a null-conditional expression E and expr_s econd is a
constant expression with value null, and the state of v after the non-conditional
counterpart E is "definitely assigned", then the state of v after expr is "definitely
assigned when false".
If expr_f irst directly contains a null-conditional expression E and expr_s econd is an
expression of a non-nullable value type, or a constant expression with a non-null
value, and the state of v after the non-conditional counterpart E is "definitely
assigned", then the state of v after expr is "definitely assigned when true".
If expr_f irst is of type boolean , and expr_s econd is a constant expression with value
true, then the definite assignment state after expr is the same as the definite
assignment state after expr_f irst.
If expr_f irst is of type boolean , and expr_s econd is a constant expression with value
false, then the definite assignment state after expr is the same as the definite
assignment state of v after the logical negation expression !expr_first.
For an expression expr of the form expr_first != expr_second, where != is a predefined
comparison operator ( §11.11 ) or a lifted operator (( §11.4.8 )), the definite assignment
state of v after expr is determined by:
If expr_f irst directly contains a null-conditional expression E and expr_s econd is a
constant expression with value null, and the state of v after the non-conditional{ 
  y.ToString();  
} 
bool Set(out int x) { x = 0; return true; } 
==/!= ( relational equality operator) expressions
0
0
counterpart E is "definitely assigned", then the state of v after expr is "definitely
assigned when true".
If expr_f irst directly contains a null-conditional expression E and expr_s econd is an
expression of a non-nullable value type, or a constant expression with a non-null
value, and the state of v after the non-conditional counterpart E is "definitely
assigned", then the state of v after expr is "definitely assigned when false".
If expr_f irst is of type boolean , and expr_s econd is a constant expression with value
true, then the definite assignment state after expr is the same as the definite
assignment state of v after the logical negation expression !expr_first.
If expr_f irst is of type boolean , and expr_s econd is a constant expression with value
false, then the definite assignment state after expr is the same as the definite
assignment state after expr_f irst.
All of the above rules in this section are commutative, meaning that if a rule applies
when evaluated in the form expr_second op expr_first, it also applies in the form
expr_first op expr_second.
The general idea expressed by these rules is:
if a conditional access is compared to null, then we know the operations
definitely occurred if the result of the comparison is false
if a conditional access is compared to a non-nullable value type or a non-null
constant, then we know the operations definitely occurred if the result of the
comparison is true.
since we can't trust user-defined operators to provide reliable answers where
initialization safety is concerned, the new rules only apply when a predefined
==/!= operator is in use.
We may eventually want to refine these rules to thread through conditional state which
is present at the end of a member access or call. Such scenarios don't really happen in
definite assignment, but they do happen in nullable in the presence of
[NotNullWhen(true)] and similar attributes. This would require special handling for bool
constants in addition to just handling for null/non-null constants.
Some consequences of these rules:
if (a?.b(out var x) == true)) x() else x(); will error in the 'else' branch
if (a?.b(out var x) == 42)) x() else x(); will error in the 'else' branch
if (a?.b(out var x) == false)) x() else x(); will error in the 'else' branch0
0
Remarksif (a?.b(out var x) == null)) x() else x(); will error in the 'then' branch
if (a?.b(out var x) != true)) x() else x(); will error in the 'then' branch
if (a?.b(out var x) != 42)) x() else x(); will error in the 'then' branch
if (a?.b(out var x) != false)) x() else x(); will error in the 'then' branch
if (a?.b(out var x) != null)) x() else x(); will error in the 'else' branch
We introduce a new section is operat or and is pattern expr essions .
For an expression expr of the form E is T, where T is any type or pattern
The definite assignment state of v before E is the same as the definite assignment
state of v before expr.
The definite assignment state of v after expr is determined by:
If E directly contains a null-conditional expression, and the state of v after the
non-conditional counterpart E is "definitely assigned", and T is any type or a
pattern that does not match a null input, then the state of v after expr is
"definitely assigned when true".
If E directly contains a null-conditional expression, and the state of v after the
non-conditional counterpart E is "definitely assigned", and T is a pattern that
matches a null input, then the state of v after expr is "definitely assigned when
false".
If E is of type boolean and T is a pattern which only matches a true input, then
the definite assignment state of v after expr is the same as the definite
assignment state of v after E.
If E is of type boolean and T is a pattern which only matches a false input,
then the definite assignment state of v after expr is the same as the definite
assignment state of v after the logical negation expression !expr.
Otherwise, if the definite assignment state of v after E is "definitely assigned",
then the definite assignment state of v after expr is "definitely assigned".
This section is meant to address similar scenarios as in the ==/!= section above. This
specification does not address recursive patterns, e.g. (a?.b(out x), c?.d(out y)) is
(object, object). Such support may come later if time permits.is operator and is pattern expressions
0
0
Remarks
Additional scenariosThis specification doesn't currently address scenarios involving pattern switch
expressions and switch statements. For example:
C#
It seems like support for this could come later if time permits.
There have been several categories of bugs filed for nullable which require we
essentially increase the sophistication of pattern analysis. It is likely that any ruling we
make which improves definite assignment would also be carried over to nullable.
https://github.com/dotnet/roslyn/issues/49353  
https://github.com/dotnet/roslyn/issues/46819  
https://github.com/dotnet/roslyn/issues/44127
It feels odd to have the analysis "reach down" and have special recognition of
conditional accesses, when typically flow analysis state is supposed to propagate
upward. W e are concerned about how a solution like this could intersect painfully with
possible future language features that do null checks.
Two alternatives to this proposal:
1. Introduce "state when null" and "state when not null" to the language and
compiler. This has been judged to be too much effort for the scenarios we are
trying to solve, but that we could potentially implement the above proposal and
then move to a "state when null/not null" model later on without breaking people.
2. Do nothing.
There are impacts on switch expressions that should be specified:
https://github.com/dotnet/csharplang/discussions/4240#discussioncomment-343395_ = c?.M( out object obj4) switch 
{ 
    not null => obj4.ToString() // undesired error  
}; 
Drawbacks
Alternatives
Unresolved questions
https://github.com/dotnet/csharplang/discussions/4243Design meetings
AsyncMethodBuilder override
Article •09/21/2021
Allow per-method override of the async method builder to use. For some async
methods we want to customize the invocation of Builder.Create() to use a different
builder type .
C#
Today, async method builders are tied to a given type used as a return type of an async
method. For example, any method that's declared as async Task uses
AsyncTaskMethodBuilder, and any method that's declared as async ValueTask<T> uses
AsyncValueTaskMethodBuilder<T>. This is due to the [AsyncMethodBuilder(Type)]
attribute on the type used as a return type, e.g. ValueTask<T> is attributed as
[AsyncMethodBuilder(typeof(AsyncValueTaskMethodBuilder<>))]. This addresses the
majority common case, but it leaves a few notable holes for advanced scenarios.
In .NET 5, an experimental feature was shipped that provides two modes in which
AsyncValueTaskMethodBuilder and AsyncValueTaskMethodBuilder<T> operate. The on-by-
default mode is the same as has been there since the functionality was introduced: when７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
[AsyncMethodBuilderAttribute(typeof(PoolingAsyncValueTaskMethodBuilder<>)) ] 
// new usage of AsyncMethodBuilderAttribute type  
static async ValueTask< int> ExampleAsync () { ... }  
Motivationthe state machine needs to be lifted to the heap, an object is allocated to store the
state, and the async method returns a ValueTask{<T>} backed by a Task{<T>}. However,
if an environment variable is set, all builders in the process switch to a mode where,
instead, the ValueTask{<T>} instances are backed by reusable IValueTaskSource{<T>}
implementations that are pooled. Each async method has its own pool with a fixed
maximum number of instances allowed to be pooled, and as long as no more than that
number are ever returned to the pool to be pooled at the same time, async
ValueTask<{T}> methods effectively become free of any GC allocation overhead.
There are several problems with this experimental mode, however, which is both why a)
it's off by default and b) we're likely to remove it in a future release unless very
compelling new information emerges
(https://github.com/dotnet/runtime/issues/13633 ).
It introduces a behavioral difference for consumers of the returned ValueTask{<T>}
if that ValueTask isn't being consumed according to spec. When it's backed by a
Task, you can do with the ValueTask things you can do with a Task, like await it
multiple times, await it concurrently, block waiting for it to complete, etc. But when
it's backed by an arbitrary IValueTaskSource, such operations are prohibited, and
automatically switching from the former to the latter can lead to bugs. With the
switch at the process level and affecting all async ValueTask methods in the
process, whether you control them or not, it's too big a hammer.
It's not necessarily a performance win, and could represent a regression in some
situations. The implementation is trading the cost of pooling (accessing a pool isn't
free) with the cost of GC, and in various situations the GC can win. Again, applying
the pooling to all async ValueTask methods in the process rather than being
selective about the ones it would most benefit is too big a hammer.
It adds to the IL size of a trimmed application, even if the flag isn't set, and then to
the resulting asm size. It's possible that can be worked around with improvements
to the implementation to teach it that for a given deployment the environment
variable will always be false, but as it stands today, every async ValueTask method
saw for example an ~2K binary footprint increase in aot images due to this option,
and, again, that applies to all async ValueTask methods in the whole application
closure.
Different methods may benefit from differing levels of control, e.g. the size of the
pool employed because of knowledge of the method and how it's used, but the
same setting is applied to all uses of the builder. One could imagine working
around that by having the builder code use reflection at runtime to look for some
attribute, but that adds significant run-time expense, and likely on the startup path.
On top of all of these issues with the existing pooling, it's also the case that developers
are prevented from writing their own customized builders for types they don't own. If,
for example, a developer wants to implement their own pooling support, they also have
to introduce a brand new task-like type, rather than just being able to use
{Value}Task{<T>}, because the attribute specifying the builder is only specifiable on the
type declaration of the return type.
We need a way to have an individual async method opt-in to a specific builder.
In dotnet/runtime, add AttributeTargets.Method to the targets for
System.Runtime.CompilerServices.AsyncMethodBuilderAttribute:
C#
This allows the attribute to be applied on methods or local functions or lambdas.Detailed design
Using AsyncMethodBuilderAttribute on methods
namespace  System.Runtime.CompilerServices  
{ 
    /// <summary>  
    /// Indicates the type of the async method builder that should be used  
by a language compiler:  
    /// - to build the return type of an async method that is attributed,  
    /// - to build the attributed type when used as the return type of an  
async method.  
    /// </summary>  
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class |  
AttributeTargets.Struct | AttributeTargets.Interface |  
AttributeTargets.Delegate | AttributeTargets.Enum, Inherited = false,  
AllowMultiple = false) ] 
    public sealed class AsyncMethodBuilderAttribute  : Attribute  
    { 
        /// <summary> Initializes the <see 
cref="AsyncMethodBuilderAttribute"/> .</summary>  
        /// <param name="builderType"> The <see cref="Type"/>  of the 
associated builder. </param>  
        public AsyncMethodBuilderAttribute (Type builderType ) => BuilderType  
= builderType;  
        /// <summary> Gets the <see cref="Type"/>  of the associated builder.
</summary>  
        public Type BuilderType { get; } 
    } 
} Example of usage on a method:
C#
It is an error to apply the attribute multiple times on a given method.  
It is an error to apply the attribute to a lambda with an implicit return type.
A developer who wants to use a specific custom builder for all of their methods can do
so by putting the relevant attribute on each method.
When compiling an async method, the builder type is determined by:
1. using the builder type from the AsyncMethodBuilder attribute if one is present,
2. otherwise, falling back to the builder type determined by previous approach. (see
spec for task-like types ).
If an AsyncMethodBuilder attribute is present, we take the builder type specified by the
attribute and construct it if necessary.  
If the override type is an open generic type, take the single type argument of the async
method's return type and substitute it into the override type.  
If the override type is a bound generic type, then we produce an error.  
If the async method's return type does not have a single type argument, then we
produce an error.
We verify that the builder type is compatible with the return type of the async method:
1. look for the public Create method with no type parameters and no parameters on
the constructed builder type.  
It is an error if the method is not found. It is an error if the method returns a type
other than the constructed builder type.
2. look for the public Task property.  
It is an error if the property is not found.
3. consider the type of that Task property (a task-like type):  
It is an error if the task-like type does not matches the return type of the async
method.
Note that it is not necessary for the return type of the method to be a task-like type.[AsyncMethodBuilder(typeof(PoolingAsyncValueTaskMethodBuilder<>)) ] // new 
usage, referring to some custom builder type  
static async ValueTask< int> ExampleAsync () { ... }  
Determining the builder type for an async method
The builder type determined above is used as part of the existing async method design.
For example, today if a method is defined as:
C#
the compiler will generate code akin to:
C#
With this change, if the developer wrote:
C#
it would instead be compiled to:
C#Execution
public async ValueTask<T> ExampleAsync () { ... }  
[AsyncStateMachine(typeof(<ExampleAsync>d__29)) ] 
[CompilerGenerated ] 
static ValueTask< int> ExampleAsync () 
{ 
    <ExampleAsync>d__29 stateMachine;  
    stateMachine.<>t__builder = AsyncValueTaskMethodBuilder< int>.Create();  
    stateMachine.<> 1__state = -1; 
    stateMachine.<>t__builder.Start( ref stateMachine);  
    return stateMachine.<>t__builder.Task;  
} 
[AsyncMethodBuilder(typeof(PoolingAsyncValueTaskMethodBuilder<>)) ] // new 
usage, referring to some custom builder type  
static async ValueTask< int> ExampleAsync () { ... }  
[AsyncStateMachine(typeof(<ExampleAsync>d__29)) ] 
[CompilerGenerated ] 
[AsyncMethodBuilder(typeof(PoolingAsyncValueTaskMethodBuilder<>)) ] // 
retained but not necessary anymore  
static ValueTask< int> ExampleAsync () 
{ 
    <ExampleAsync>d__29 stateMachine;  
    stateMachine.<>t__builder =  
PoolingAsyncValueTaskMethodBuilder< int>.Create(); // <>t__builder now a  
different type  
    stateMachine.<> 1__state = -1; 
    stateMachine.<>t__builder.Start( ref stateMachine);  Just those small additions enable:
Anyone to write their own builder that can be applied to async methods that
return Task<T> and ValueTask<T>
As "anyone", the runtime to ship the experimental builder support as new public
builder types that can be opted into on a method-by-method basis; the existing
support would be removed from the existing builders. Methods (including some
we care about in the core libraries) can then be attributed on a case-by-case basis
to use the pooling support, without impacting any other unattributed methods.
and with minimal surface area changes or feature work in the compiler.
Note that we need the emitted code to allow a different type being returned from
Create method:
Note that this mechanism to change the the builder type cannot be used when the
synthesized entry-point for top-level statements is async. An explicit entry-point should
be used instead.
The syntax for applying such an attribute to a method is verbose. The impact of
this is lessened if a developer can apply it to multiple methods en mass, e.g. at the
type or module level.
Implement a different task-like type and expose that difference to consumers.
ValueTask was made extensible via the IValueTaskSource interface to avoid that
need, however.
Address just the V alueT ask pooling part of the issue by enabling the experiment as
the on-by-default-and-only implementation. That doesn't address other aspects,
such as configuring the pooling, or enabling someone else to provide their own
builder.    return stateMachine.<>t__builder.Task;  
} 
AsyncPooledBuilder _builder = AsyncPooledBuilderWithSize4.Create();  
Drawbacks
AlternativesEarlier versions of this document allowed for scoped override of builder types.
1. Replace or also cr eate. All of the examples in this proposal are about replacing a
buildable task-like's builder. Should the feature be scoped to just that? Or should
you be able to use this attribute on a method with a return type that doesn't
already have a builder (e.g. some common interface)? That could impact overload
resolution.
2. Private Builder s. Should the compiler support non-public async method builders?
This is not spec'd today, but experimentally we only support public ones. That
makes some sense when the attribute is applied to a type to control what builder
is used with that type, since anyone writing an async method with that type as the
return type would need access to the builder. However, with this new feature,
when that attribute is applied to a method, it only impacts the implementation of
that method, and thus could reasonably reference a non-public builder. Likely we
will want to support library authors who have non-public ones they want to use.Unresolved questionsStatic abstract members in interfaces
Article •03/28/2023
An interface is allowed to specify abstract static members that implementing classes and
structs are then required to provide an explicit or implicit implementation of. The
members can be accessed off of type parameters that are constrained by the interface.
There is currently no way to abstract over static members and write generalized code
that applies across types that define those static members. This is particularly
problematic for member kinds that only exist in a static form, notably operators.
This feature allows generic algorithms over numeric types, represented by interface
constraints that specify the presence of given operators. The algorithms can therefore
be expressed in terms of such operators:
c#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
// Interface specifies static properties and operators  
interface  IAddable <T> where T : IAddable <T> 
{ 
    static abstract  T Zero { get; } 
    static abstract  T operator  +(T t1, T t2);  
} 
// Classes and structs (including built-ins) can implement interface  
struct Int32 : …, IAddable<Int32>  
{ 
    static Int32 I. operator  +(Int32 x, Int32 y) => x + y; // Explicit  The feature would allow static interface members to be declared virtual.
Today, instance members in interfaces are implicitly abstract (or virtual if they have a
default implementation), but can optionally have an abstract (or virtual) modifier.
Non-virtual instance members must be explicitly marked as sealed.
Static interface members today are implicitly non-virtual, and do not allow abstract,
virtual or sealed modifiers.
Static interface members other than fields are allowed to also have the abstract
modifier. Abstract static members are not allowed to have a body (or in the case of
properties, the accessors are not allowed to have a body).
c#    public static int Zero => 0;                          // Implicit
} 
// Generic algorithms can use static members on T  
public static T AddAll<T>(T[] ts) where T : IAddable<T>  
{ 
    T result = T.Zero;                   // Call static operator  
    foreach (T t in ts) { result += t; } // Use `+`  
    return result;  
} 
// Generic method can be applied to built-in and user-defined types  
int sixtyThree = AddAll( new [] { 1, 2, 4, 8, 16, 32 }); 
Syntax
Interface members
Today's rules
Proposal
Abstract static members
interface  I<T> where T : I<T> 
{ 
    static abstract  void M(); 
    static abstract  T P { get; set; } 
    static abstract  event Action E;  Static interface members other than fields are allowed to also have the virtual
modifier. Virtual static members are required to have a body.
c#
For symmetry with non-virtual instance members, static members should be allowed an
optional sealed modifier, even though they are non-virtual by default:
c#    static abstract  T operator  +(T l, T r);  
    static abstract  bool operator  ==(T l, T r);  
    static abstract  bool operator  !=(T l, T r);  
    static abstract  implicit  operator  T(string s); 
    static abstract  explicit  operator  string(T t); 
} 
Virtual static members
interface  I<T> where T : I<T> 
{ 
    static virtual void M() {} 
    static virtual T P { get; set; } 
    static virtual event Action E;  
    static virtual T operator  +(T l, T r) { throw new 
NotImplementedException(); }  
} 
Explicitly non-virtual static members
interface  I0 
{ 
    static sealed void M() => Console.WriteLine( "Default behavior" ); 
     
    static sealed int f = 0; 
     
    static sealed int P1 { get; set; } 
    static sealed int P2 { get => f; set => f = value; } 
     
    static sealed event Action E1;  
    static sealed event Action E2 { add => E1 += value; remove => E1 -=  
value; } 
     
    static sealed I0 operator  +(I0 l, I0 r) => l;  
} Classes and structs can implement abstract instance members of interfaces either
implicitly or explicitly. An implicitly implemented interface member is a normal (virtual or
non-virtual) member declaration of the class or struct that just "happens" to also
implement the interface member. The member can even be inherited from a base class
and thus not even be present in the class declaration.
An explicitly implemented interface member uses a qualified name to identify the
interface member in question. The implementation is not directly accessible as a
member on the class or struct, but only through the interface.
No new syntax is needed in classes and structs to facilitate implicit implementation of
static abstract interface members. Existing static member declarations serve that
purpose.
Explicit implementations of static abstract interface members use a qualified name along
with the static modifier.
c#Implementation of interface members
Today's rules
Proposal
class C : I<C> 
{ 
    string _s; 
    public C(string s) => _s = s;  
    static void I<C>.M() => Console.WriteLine( "Implementation" ); 
    static C I<C>.P { get; set; } 
    static event Action I<C>.E;  
    static C I<C>. operator  +(C l, C r) => new C($"{l._s} {r._s}"); 
    static bool I<C>.operator  ==(C l, C r) => l._s == r._s;  
    static bool I<C>.operator  !=(C l, C r) => l._s != r._s;  
    static implicit  I<C>.operator  C(string s) => new C(s); 
    static explicit  I<C>.operator  string(C c) => c._s;  
} 
Semantics
Operator restrictionsToday all unary and binary operator declarations have some requirement involving at
least one of their operands to be of type T or T?, where T is the instance type of the
enclosing type.
These requirements need to be relaxed so that a restricted operand is allowed to be of a
type parameter that counts as "the instance type of the enclosing type".
In order for a type parameter T to count as " the instance type of the enclosing type", it
must meet the following requirements:
T is a direct type parameter on the interface in which the operator declaration
occurs, and
T is directly constrained by what the spec calls the "instance type" - i.e. the
surrounding interface with its own type parameters used as type arguments.
Abstract/virtual declarations of == and != operators, as well as abstract/virtual
declarations of implicit and explicit conversion operators will be allowed in interfaces.
Derived interfaces will be allowed to implement them too.
For == and != operators, at least one parameter type must be a type parameter that
counts as "the instance type of the enclosing type", as defined in the previous section.
The rules for when a static member declaration in a class or struct is considered to
implement a static abstract interface member, and for what requirements apply when it
does, are the same as for instance members.
TBD:  Ther e may be additional or di fferent rules nec essary her e that w e hav en't yet
thought o f.
We discussed the issue raised by https://github.com/dotnet/csharplang/issues/5955
and decided to add a restriction around usage of an interface as a type argument
(https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-03-
28.md#type-hole-in-static-abstracts ). Here is the restriction as it was proposed by
https://github.com/dotnet/csharplang/issues/5955  and approved by the LDM.Equality operators and conversions
Implementing static abstract members
Interfaces as type arguments
An interface containing or inheriting a static abstract/virtual member that does not have
most specific implementation in the interface cannot be used as a type argument. If all
static abstract/virtual members have most specific implementation, the interface can be
used as a type argument.
A static abstract interface member M may be accessed on a type parameter T using the
expression T.M when T is constrained by an interface I and M is an accessible static
abstract member of I.
c#
At runtime, the actual member implementation used is the one that exists on the actual
type provided as a type argument.
c#
Since query expressions are spec'ed as a syntactic rewrite, C# actually lets you use a type
as the query source, as long as it has static members for the query operators you use! In
other words, if the syntax fits, we allow it! W e think this behavior was not intentional or
important in the original LINQ, and we don't want to do the work to support it on type
parameters. If there are scenarios out there we will hear about them, and can choose to
embrace this later.
Variance safety rules should apply to signatures of static abstract members. The addition
proposed in https://github.com/dotnet/csharplang/blob/main/proposals/variance-
safety-for-static-interface-members.md#variance-safety  should be adjusted from
These restrictions do not apply t o occurrences of types within declar ations o f static
member s.Accessing static abstract interface members
T M<T>() where T : I<T>  
{ 
    T.M();  
    T t = T.P;  
    T.E += () => { };  
    return t + T.P;  
} 
C c = M<C>(); // The static members of C get called  
Variance safety §17.2.3.2
to
These restrictions do not apply t o occurrences of types within declar ations o f non-vir tual,
non-abstr act static member s.
The following bullet points
Determine the types S, S₀ and T₀.
If E has a type, let S be that type.
If S or T are nullable value types, let Sᵢ and Tᵢ be their underlying types,
otherwise let Sᵢ and Tᵢ be S and T, respectively.
If Sᵢ or Tᵢ are type parameters, let S₀ and T₀ be their effective base classes,
otherwise let S₀ and T₀ be Sₓ and Tᵢ, respectively.
Find the set of types, D, from which user-defined conversion operators will be
considered. This set consists of S0 (if S0 is a class or struct), the base classes of S0
(if S0 is a class), and T0 (if T0 is a class or struct).
Find the set of applicable user-defined and lifted conversion operators, U. This set
consists of the user-defined and lifted implicit conversion operators declared by
the classes or structs in D that convert from a type encompassing S to a type
encompassed by T. If U is empty, the conversion is undefined and a compile-time
error occurs.
are adjusted as follows:
Determine the types S, S₀ and T₀.
If E has a type, let S be that type.
If S or T are nullable value types, let Sᵢ and Tᵢ be their underlying types,
otherwise let Sᵢ and Tᵢ be S and T, respectively.
If Sᵢ or Tᵢ are type parameters, let S₀ and T₀ be their effective base classes,
otherwise let S₀ and T₀ be Sₓ and Tᵢ, respectively.
Find the set of applicable user-defined and lifted conversion operators, U.
Find the set of types, D1, from which user-defined conversion operators will be
considered. This set consists of S0 (if S0 is a class or struct), the base classes of
S0 (if S0 is a class), and T0 (if T0 is a class or struct).
Find the set of applicable user-defined and lifted conversion operators, U1. This
set consists of the user-defined and lifted implicit conversion operators declared
by the classes or structs in D1 that convert from a type encompassing S to a
type encompassed by T.§10.5.4 User defined implicit conversions
If U1 is not empty, then U is U1. Otherwise,
Find the set of types, D2, from which user-defined conversion operators will
be considered. This set consists of Sᵢ effectiv e interface set and their base
interfaces (if Sᵢ is a type parameter), and Tᵢ effectiv e interface set (if Tᵢ is a
type parameter).
Find the set of applicable user-defined and lifted conversion operators, U2.
This set consists of the user-defined and lifted implicit conversion operators
declared by the interfaces in D2 that convert from a type encompassing S to
a type encompassed by T.
If U2 is not empty, then U is U2
If U is empty, the conversion is undefined and a compile-time error occurs.
The following bullet points
Determine the types S, S₀ and T₀.
If E has a type, let S be that type.
If S or T are nullable value types, let Sᵢ and Tᵢ be their underlying types,
otherwise let Sᵢ and Tᵢ be S and T, respectively.
If Sᵢ or Tᵢ are type parameters, let S₀ and T₀ be their effective base classes,
otherwise let S₀ and T₀ be Sᵢ and Tᵢ, respectively.
Find the set of types, D, from which user-defined conversion operators will be
considered. This set consists of S0 (if S0 is a class or struct), the base classes of S0
(if S0 is a class), T0 (if T0 is a class or struct), and the base classes of T0 (if T0 is a
class).
Find the set of applicable user-defined and lifted conversion operators, U. This set
consists of the user-defined and lifted implicit or explicit conversion operators
declared by the classes or structs in D that convert from a type encompassing or
encompassed by S to a type encompassing or encompassed by T. If U is empty,
the conversion is undefined and a compile-time error occurs.
are adjusted as follows:
Determine the types S, S₀ and T₀.
If E has a type, let S be that type.
If S or T are nullable value types, let Sᵢ and Tᵢ be their underlying types,
otherwise let Sᵢ and Tᵢ be S and T, respectively.§10.5.5 User-defined explicit conversions
If Sᵢ or Tᵢ are type parameters, let S₀ and T₀ be their effective base classes,
otherwise let S₀ and T₀ be Sᵢ and Tᵢ, respectively.
Find the set of applicable user-defined and lifted conversion operators, U.
Find the set of types, D1, from which user-defined conversion operators will be
considered. This set consists of S0 (if S0 is a class or struct), the base classes of
S0 (if S0 is a class), T0 (if T0 is a class or struct), and the base classes of T0 (if
T0 is a class).
Find the set of applicable user-defined and lifted conversion operators, U1. This
set consists of the user-defined and lifted implicit or explicit conversion
operators declared by the classes or structs in D1 that convert from a type
encompassing or encompassed by S to a type encompassing or encompassed
by T.
If U1 is not empty, then U is U1. Otherwise,
Find the set of types, D2, from which user-defined conversion operators will
be considered. This set consists of Sᵢ effectiv e interface set and their base
interfaces (if Sᵢ is a type parameter), and Tᵢ effectiv e interface set and their
base interfaces (if Tᵢ is a type parameter).
Find the set of applicable user-defined and lifted conversion operators, U2.
This set consists of the user-defined and lifted implicit or explicit conversion
operators declared by the interfaces in D2 that convert from a type
encompassing or encompassed by S to a type encompassing or
encompassed by T.
If U2 is not empty, then U is U2
If U is empty, the conversion is undefined and a compile-time error occurs.
An additional  feature to this proposal is to allow static virtual members in interfaces to
have default implementations, just as instance virtual/abstract members do.
One complication here is that default implementations would want to call other static
virtual members "virtually". Allowing static virtual members to be called directly on the
interface would require flowing a hidden type parameter representing the "self" type
that the current static method really got invoked on. This seems complicated, expensive
and potentially confusing.
We discussed a simpler version which maintains the limitations of the current proposal
that static virtual members can only be invoked on type parameters. Since interfaces
with static virtual members will often have an explicit type parameter representing aDefault implementations"self" type, this wouldn't be a big loss: other static virtual members could just be called
on that self type. This version is a lot simpler, and seems quite doable.
At https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
24.md#default-implementations-of-abstract-statics  we decided to support Default
Implementations of static members following/expanding the rules established in
https://github.com/dotnet/csharplang/blob/main/proposals/csharp-8.0/default-
interface-methods.md  accordingly.
Given the following code, a user might reasonably expect it to print T rue (as it would if
the constant pattern was written inline):
C#
However, because the input type of the pattern is not double, the constant 1 pattern
will first type check the incoming T against int. This is unintuitive, so we will block it
until a future C# version adds better handling for numeric matching against types
derived from INumberBase<T>. To do so, we will say that, we will explicitly recognize
INumberBase<T> as the type that all "numbers" will derive from, and block the pattern if
we're trying to match a numeric constant pattern against a number type that we can't
represent the pattern in (ie, a type parameter constrained to INumberBase<T>, or a user-
defined number type that inherits from INumberBase<T>).
Formally, we add an exception to the definition of pattern-compatible  for constant
patterns:
A constant pattern tests the value of an expression against a constant value. The
constant may be any constant expression, such as a literal, the name of a declared
const variable, or an enumeration constant. When the input value is not an open
type, the constant expression is implicitly converted to the type of the matched
expression; if the type of the input value is not pattern-compatible  with the type of
the constant expression, the pattern-matching operation is an error. If the constant
expression being mat ched against is a numeric v alue, the input v alue is a type
Pattern matching
M(1.0); 
static void M<T>(T t) where T : INumberBase<T>  
{ 
    Console.WriteLine(t is 1); 
} that inherits fr om System.Numerics.INumberBase<T>, and ther e is no constant
conv ersion fr om the constant expr ession t o the type o f the input v alue, the
pattern-mat ching operation is an err or.
We also add a similar exception for relational patterns:
When the input is a type for which a suitable built-in binary relational operator is
defined that is applicable with the input as its left operand and the given constant
as its right operand, the evaluation of that operator is taken as the meaning of the
relational pattern. Otherwise we convert the input to the type of the expression
using an explicit nullable or unboxing conversion. It is a compile-time error if no
such conversion exists. It is a compile-time err or if the input type is a type
paramet er constrained t o or a type inheriting fr om
System.Numerics.INumberBase<T> and the input type has no suitable built -in binar y
relational operat or defined.  The pattern is considered not to match if the
conversion fails. If the conversion succeeds then the result of the pattern-matching
operation is the result of evaluating the expression e OP v where e is the converted
input, OP is the relational operator, and v is the constant expression.
"static abstract" is a new concept and will meaningfully add to the conceptual load
of C#.
It's not a cheap feature to build. W e should make sure it's worth it.
An alternative approach would be to have "structural constraints" directly and explicitly
requiring the presence of specific operators on a type parameter. The drawbacks of that
are: - This would have to be written out every time. Having a named constraint seems
better. - This is a whole new kind of constraint, whereas the proposed feature utilizes
the existing concept of interface constraints. - It would only work for operators, not
(easily) other kinds of static members.Drawbacks
Alternatives
Structural constraints
Unresolved questionsSee https://github.com/dotnet/csharplang/issues/5783  and
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
16.md#static-abstract-interfaces-and-static-classes  for more information.
https://github.com/dotnet/csharplang/blob/master/meetings/2021/LDM-2021-02-
08.md
https://github.com/dotnet/csharplang/blob/main/meetings/2021/LDM-2021-04-
05.md
https://github.com/dotnet/csharplang/blob/master/meetings/2020/LDM-2020-06-
29.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
24.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
16.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-03-
28.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-04-
06.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-06-
06.mdStatic abstract interfaces and static classes
Design meetings
Checked user-defined operators
Article •09/30/2022
C# should support defining checked variants of the following user-defined operators so
that users can opt into or out of overflow behavior as appropriate:
The ++ and -- unary operators §11.7.14  and §11.8.6 .
The - unary operator §11.8.3 .
The +, -, *, and / binary operators §11.9 .
Explicit conversion operators.
There is no way for a user to declare a type and support both checked and unchecked
versions of an operator. This will make it hard to port various algorithms to use the
proposed generic math interfaces exposed by the libraries team. Likewise, this makes it
impossible to expose a type such as Int128 or UInt128 without the language
simultaneously shipping its own support to avoid breaking changes.
Grammar at operators ( §14.10 ) will be adjusted to allow checked keyword after the
operator keyword right before the operator token:７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Detailed design
Syntax
antlr
For example:
C#
C#
For brevity below, an operator with the checked keyword is referred to as a checked
operator and an operator without it is referred to as a regular operator. These terms
are not applicable to operators that don't have a checked form.overloadable_unary_operator  
    : '+' | 'checked' ? '-' | '!' | '~' | 'checked' ? '++' | 'checked' ? '--' | 
'true' | 'false' 
    ; 
overloadable_binary_operator  
    : 'checked' ? '+'   | 'checked' ? '-'   | 'checked' ? '*'   | 'checked' ? 
'/'   | '%'   | '&'   | '|'   | '^'   | '<<' 
    | right_shift | '=='  | '!='  | '>'   | '<'   | '>='  | '<=' 
    ; 
     
conversion_operator_declarator  
    : 'implicit'  'operator'  type '(' type identifier ')' 
    | 'explicit'  'operator'  'checked' ? type '(' type identifier ')' 
    ;     
public static T operator  checked ++(T x) {...}  
public static T operator  checked --(T x) {...}  
public static T operator  checked -(T x) {...}  
public static T operator  checked +(T lhs, T rhs) {...}  
public static T operator  checked -(T lhs, T rhs) {...}  
public static T operator  checked *(T lhs, T rhs) {...}  
public static T operator  checked /(T lhs, T rhs) {...}  
public static explicit  operator  checked U(T x) {...} 
public static T I1.operator  checked ++(T x) {...}  
public static T I1.operator  checked --(T x) {...}  
public static T I1.operator  checked -(T x) {...}  
public static T I1.operator  checked +(T lhs, T rhs) {...}  
public static T I1.operator  checked -(T lhs, T rhs) {...}  
public static T I1.operator  checked *(T lhs, T rhs) {...}  
public static T I1.operator  checked /(T lhs, T rhs) {...}  
public static explicit  I1.operator  checked U(T x) {...} 
SemanticsA user-defined checked operator is expected to throw an exception when the result of
an operation is too large to represent in the destination type. What does it mean to be
too large actually depends on the nature of the destination type and is not prescribed
by the language. T ypically the exception thrown is a System.OverflowException, but the
language doesn't have any specific requirements regarding this.
A user-defined regular operator is expected to not throw an exception when the result
of an operation is too large to represent in the destination type. Instead, it is expected
to return an instance representing a truncated result. What does it mean to be too large
and to be truncated actually depends on the nature of the destination type and is not
prescribed by the language.
All existing user-defined operators out there that will have checked form supported fall
into the category of regular operators. It is understood that many of them are likely to
not follow the semantics specified above, but for the purpose of semantic analysis,
compiler will assume that they are.
Checked/unchecked context within the body of a checked operator is not affected by
the presence of the checked keyword. In other words, the context is the same as
immediately at the beginning of the operator declaration. The developer would need to
explicitly switch the context if part of their algorithm cannot rely on default context.
Section "I.10.3.1 Unary operators" of ECMA-335 will be adjusted to include
op_Check edIncr ement , op_Check edDecr ement , op_Check edUnar yNegation  as the names
for methods implementing checked ++, -- and - unary operators.
Section "I.10.3.2 Binary operators" of ECMA-335 will be adjusted to include
op_Check edAddition , op_Check edSubtr action , op_Check edMultiply , op_Check edDivision  as
the names for methods implementing checked +, -, *, and / binary operators.
Section "I.10.3.3 Conversion operators" of ECMA-335 will be adjusted to include
op_Check edExplicit  as the name for a method implementing checked explicit conversion
operator.
Unary checked operators follow the rules from §14.10.2 .Checked vs. unchecked context within a checked operator
Names in metadata
Unary operators
Also, a checked operator declaration requires a pair-wise declaration of a regular
operator (the return type should match as well). A compile-time error occurs otherwise.
C#
Binary checked operators follow the rules from §14.10.3 .
Also, a checked operator declaration requires a pair-wise declaration of a regular
operator (the return type should match as well). A compile-time error occurs otherwise.
C#
The https://github.com/dotnet/csharplang/blob/main/spec/expressions.md#candidate-
user-defined-operators  section will be adjusted as follows (additions/changes are in
bold).public struct Int128 
{ 
    // This is fine, both a checked and regular operator are defined  
    public static Int128 operator  checked -(Int128 lhs);
    public static Int128 operator  -(Int128 lhs);  
    // This is fine, only a regular operator is defined  
    public static Int128 operator  --(Int128 lhs);  
    // This should error, a regular operator must also be defined  
    public static Int128 operator  checked ++(Int128 lhs);  
} 
Binary operators
public struct Int128 
{ 
    // This is fine, both a checked and regular operator are defined  
    public static Int128 operator  checked +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  +(Int128 lhs, Int128 rhs);  
    // This is fine, only a regular operator is defined  
    public static Int128 operator  -(Int128 lhs, Int128 rhs);  
    // This should error, a regular operator must also be defined  
    public static Int128 operator  checked *(Int128 lhs, Int128 rhs);  
} 
Candidate user-defined operators
Given a type T and an operation operator op(A), where op is an overloadable operator
and A is an argument list, the set of candidate user-defined operators provided by T for
operator op(A) is determined as follows:
Determine the type T0. If T is a nullable type, T0 is its underlying type, otherwise
T0 is equal to T.
Find the set o f user -defined operat ors, U. This set consists o f:
In unchecked evaluation cont ext, all r egular operator op declarations in T0.
In checked evaluation cont ext, all check ed and r egular operator op
declarations in T0 except r egular declarations that hav e pair-wise mat ching
checked operator declaration.
For all operator op declarations in U and all lifted forms of such operators, if at
least one operator is applicable ( Applicable function member ) with respect to
the argument list A, then the set of candidate operators consists of all such
applicable operators in T0.
Otherwise, if T0 is object, the set of candidate operators is empty.
Otherwise, the set of candidate operators provided by T0 is the set of candidate
operators provided by the direct base class of T0, or the effective base class of T0
if T0 is a type parameter.
Similar rules will be applied while determining the set of candidate operators in
interfaces https://github.com/dotnet/csharplang/blob/main/meetings/2017/LDM-2017-
06-27.md#shadowing-within-interfaces .
The section §11.7.18  will be adjusted to reflect the effect that the checked/unchecked
context has on unary and binary operator overload resolution.
C#
Example #1:
public class MyClass 
{ 
    public static void Add(Int128 lhs, Int128 rhs ) 
    { 
        // Resolves to `op_CheckedAddition`  
        Int128 r1 = checked(lhs + rhs);  
        // Resolves to `op_Addition`  
        Int128 r2 = unchecked (lhs + rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r3 = checked(lhs - rhs);  C#        // Resolve to `op_Subtraction`  
        Int128 r4 = unchecked (lhs - rhs);  
        // Resolves to `op_CheckedMultiply`  
        Int128 r5 = checked(lhs * rhs);  
        // Error: Operator '*' cannot be applied to operands of type  
'Int128' and 'Int128'  
        Int128 r6 = unchecked (lhs * rhs);  
    } 
    public static void Divide(Int128 lhs, byte rhs) 
    { 
        // Resolves to `op_Division` - it is a better match than  
`op_CheckedDivision`  
        Int128 r4 = checked(lhs / rhs);  
    } 
} 
public struct Int128 
{ 
    public static Int128 operator  checked +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  -(Int128 lhs, Int128 rhs);  
    // Cannot be declared in C#, but could be declared by some other  
language  
    public static Int128 operator  checked *(Int128 lhs, Int128 rhs);  
    // Cannot be declared in C#, but could be declared by some other  
language  
    public static Int128 operator  checked /(Int128 lhs, int rhs); 
    public static Int128 operator  /(Int128 lhs, byte rhs); 
} 
Example #2:
class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // error CS0034: Operator '+' is ambiguous on operands of type 'C2'  
and 'C3'  
        o = checked(x + y);  
         
        // C2.op_Addition  C#        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    // Cannot be declared in C#, but could be declared by some other  
language  
    public static C1 operator  checked + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    public static C2 operator  + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 
{ 
} 
Example #3:
class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // error CS0034: Operator '+' is ambiguous on operands of type 'C2'  
and 'C3'  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    // Cannot be declared in C#, but could be declared by some other  
language  
    public static C2 operator  checked + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 Conversion checked operators follow the rules from §14.10.4 .
However, a checked operator declaration requires a pair-wise declaration of a regular
operator. A compile-time error occurs otherwise.
The following paragraph
The signature of a conversion operator consists of the source type and the target
type. (This is the only form of member for which the return type participates in the
signature.) The implicit or explicit classification of a conversion operator is not part
of the operator's signature. Thus, a class or struct cannot declare both an implicit
and an explicit conversion operator with the same source and target types.
will be adjusted to allow a type to declare checked and regular forms of explicit
conversions with the same source and target types. A type will not be allowed to declare
both an implicit and a checked explicit conversion operator with the same source and
target types.
The third bullet in §10.5.5 :
Find the set of applicable user-defined and lifted conversion operators, U. This
set consists of the user-defined and lifted implicit or explicit conversion
operators declared by the classes or structs in D that convert from a type
encompassing or encompassed by S to a type encompassing or encompassed
by T. If U is empty, the conversion is undefined and a compile-time error
occurs.
will be replaced with the following bullet points:
Find the set o f conv ersion operat ors, U0. This set consists o f:
In unchecked evaluation cont ext, the user -defined implicit or r egular explicit
conv ersion operat ors declar ed by the classes or structs in D.{ 
} 
Conversion operators
Processing of user-defined explicit conversions
In checked evaluation cont ext, the user -defined implicit or r egular/check ed
explicit conv ersion operat ors declar ed by the classes or structs in D except
regular explicit conv ersion operat ors that hav e pair-wise mat ching checked
operator declaration within the same declaring type.
Find the set of applicable user-defined and lifted conversion operators, U. This set
consists of the user-defined and lifted implicit or explicit conversion operators in
U0 that convert from a type encompassing or encompassed by S to a type
encompassing or encompassed by T. If U is empty, the conversion is undefined
and a compile-time error occurs.
The Checked and unchecked operators §11.7.18  section will be adjusted to reflect the
effect that the checked/unchecked context has on processing of user-defined explicit
conversions.
A checked operator does not implement a regular operator and vice versa.
Checked operators will be supported in Linq Expression T rees. A
UnaryExpression/BinaryExpression node will be created with corresponding MethodInfo.
The following factory methods will be used:
C#
Note, that C# doesn't support assignments in expression trees, therefore checked
increment/decrement will not be supported as well.
There is no factory method for checked divide. There is an open question regarding this
- Checked division in Linq Expression T rees.
Implementing operators
Linq Expression Trees
public static UnaryExpression NegateChecked  (Expression expression,  
MethodInfo? method ); 
public static BinaryExpression AddChecked  (Expression left, Expression  
right, MethodInfo? method ); 
public static BinaryExpression SubtractChecked  (Expression left, Expression  
right, MethodInfo? method ); 
public static BinaryExpression MultiplyChecked  (Expression left, Expression  
right, MethodInfo? method ); 
public static UnaryExpression ConvertChecked  (Expression expression, Type  
type, MethodInfo? method ); We will investigate the cost of adding support for checked operators in dynamic
invocation in CoreCLR and pursue an implementation if the cost is not too high. This is a
quote from https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-
2022-02-09.md .
This adds additional complexity to the language and allows users to introduce more
kinds of breaking changes to their types.
The generic math interfaces that the libraries plans to expose could expose named
methods (such as AddChecked). The primary drawback is that this is less
readable/maintainable and doesn't get the benefit of the language precedence rules
around operators.
Alternatively the checked keyword could be moved to the place right before the
operator keyword:
C#
C#Dynamic
Drawbacks
Alternatives
Placement of the checked keyword
public static T checked operator  ++(T x) {...}  
public static T checked operator  --(T x) {...}  
public static T checked operator  -(T x) {...}  
public static T checked operator  +(T lhs, T rhs) {...}  
public static T checked operator  -(T lhs, T rhs) {...}  
public static T checked operator  *(T lhs, T rhs) {...}  
public static T checked operator  /(T lhs, T rhs) {...}  
public static explicit  checked operator  U(T x) {...} 
public static T checked I1. operator  ++(T x) {...}  
public static T checked I1. operator  --(T x) {...}  
public static T checked I1. operator  -(T x) {...}  
public static T checked I1. operator  +(T lhs, T rhs) {...}  
public static T checked I1. operator  -(T lhs, T rhs) {...}  
public static T checked I1. operator  *(T lhs, T rhs) {...}  Or it could be moved into the set of operator modifiers:
antlr
C#
C#
There were suggestions to support unchecked keyword at the same position as the
checked keyword with the following possible meanings:
Simply to explicitly reflect the regular nature of the operator, or
Perhaps to designate a distinct flavor of an operator that is supposed to be used in
an unchecked context. The language could support op_Addition,
op_CheckedAddition, and op_UncheckedAddition to help limit the number ofpublic static T checked I1. operator  /(T lhs, T rhs) {...}  
public static explicit  checked I1. operator  U(T x) {...} 
operator_modifier  
    : 'public'  
    | 'static'  
    | 'extern'  
    | 'checked'  
    | operator_modifier_unsafe  
    ; 
public static checked T operator  ++(T x) {...}  
public static checked T operator  --(T x) {...}  
public static checked T operator  -(T x) {...}  
public static checked T operator  +(T lhs, T rhs) {...}  
public static checked T operator  -(T lhs, T rhs) {...}  
public static checked T operator  *(T lhs, T rhs) {...}  
public static checked T operator  /(T lhs, T rhs) {...}  
public static checked explicit  operator  U(T x) {...} 
public static checked T I1. operator  ++(T x) {...}  
public static checked T I1. operator  --(T x) {...}  
public static checked T I1. operator  -(T x) {...}  
public static checked T I1. operator  +(T lhs, T rhs) {...}  
public static checked T I1. operator  -(T lhs, T rhs) {...}  
public static checked T I1. operator  *(T lhs, T rhs) {...}  
public static checked T I1. operator  /(T lhs, T rhs) {...}  
public static checked explicit  I1.operator  U(T x) {...} 
unchecked keywordbreaking changes. This adds another layer of complexity that is likely not necessary
in most code.
Alternatively the operator names could be op_Unar yNegationCheck ed,
op_AdditionCheck ed, op_Subtr actionCheck ed, op_MultiplyCheck ed, op_DivisionCheck ed,
with Check ed at the end. However, it looks like there is already a pattern established to
end the names with the operator word. For example, there is a op_UnsignedRightShi ft
operator rather than op_RightShi ftUnsigned  operator.
The compiler, when performing member lookup to find candidate user-defined
operators within an unchecked context, could ignore checked operators. If metadata is
encountered that only defines a checked operator, then a compilation error will occur.
C#
The compiler, when performing member lookup to find candidate user-defined
operators within a checked context will also consider applicable operators ending with
Checked. That is, if the compiler was attempting to find applicable function members forOperator names in ECMA-335
Checked operators are inapplicable in an unchecked
context
public class MyClass 
{ 
    public static void Add(Int128 lhs, Int128 rhs ) 
    { 
        // Resolves to `op_CheckedMultiply`  
        Int128 r5 = checked(lhs * rhs);  
        // Error: Operator '*' cannot be applied to operands of type  
'Int128' and 'Int128'  
        Int128 r5 = unchecked (lhs * rhs);  
    } 
} 
public struct Int128 
{ 
    public static Int128 operator  checked *(Int128 lhs, Int128 rhs);  
} 
More complicated operator lookup and overload
resolution rules in a checked contextthe binary addition operator, it would look for both op_Addition and
op_AdditionChecked. If the only applicable function member is a checked operator, it will
be used. If both a regular operator and checked operator exist and are equally
applicable the checked operator will be preferred. If both a regular operator and a
checked operator exist but the regular operator is an exact match while the checked
operator is not, the compiler will prefer the regular operator.
C#
public class MyClass 
{ 
    public static void Add(Int128 lhs, Int128 rhs ) 
    { 
        // Resolves to `op_CheckedAddition`  
        Int128 r1 = checked(lhs + rhs);  
        // Resolves to `op_Addition`  
        Int128 r2 = unchecked (lhs + rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r3 = checked(lhs - rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r4 = unchecked (lhs - rhs);  
    } 
    public static void Multiply (Int128 lhs, byte rhs) 
    { 
        // Resolves to `op_Multiply` even though `op_CheckedMultiply` is  
also applicable  
        Int128 r4 = checked(lhs * rhs);  
    } 
} 
public struct Int128 
{ 
    public static Int128 operator  checked +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  -(Int128 lhs, Int128 rhs);  
    public static Int128 operator  checked *(Int128 lhs, int rhs); 
    public static Int128 operator  *(Int128 lhs, byte rhs); 
} 
Yet another way to build the set of candidate user-
defined operatorsAssuming that regular operator matches unchecked evaluation context, checked
operator matches checked evaluation context and an operator that doesn't have
checked form (for example, +) matches either context, the first bullet in
https://github.com/dotnet/csharplang/blob/main/spec/expressions.md#unary-operator-
overload-resolution :
The set of candidate user-defined operators provided by X for the operation
operator op(x) is determined using the rules of Candidate user-defined
operators .
will be replaced with the following two bullet points:
The set of candidate user-defined operators provided by X for the operation
operator op(x) matching the curr ent check ed/uncheck ed cont ext is determined
using the rules of Candidate user-defined operators .
If the set of candidate user-defined operators is not empty, then this becomes the
set of candidate operators for the operation. Otherwise, the set of candidate user-
defined operators provided by X for the operation operator op(x) matching the
opposit e check ed/uncheck ed cont ext is determined using the rules of Candidate
user-defined operators .
Assuming that regular operator matches unchecked evaluation context, checked
operator matches checked evaluation context and an operator that doesn't have a
checked form (for example, %) matches either context, the first bullet in
https://github.com/dotnet/csharplang/blob/main/spec/expressions.md#binary-
operator-overload-resolution :
The set of candidate user-defined operators provided by X and Y for the
operation operator op(x,y) is determined. The set consists of the union of the
candidate operators provided by X and the candidate operators provided by
Y, each determined using the rules of Candidate user-defined operators . If
X and Y are the same type, or if X and Y are derived from a common base
type, then shared candidate operators only occur in the combined set once.
will be replaced with the following two bullet points:Unary operator overload resolution
Binary operator overload resolution
The set of candidate user-defined operators provided by X and Y for the
operation operator op(x,y) matching the curr ent check ed/uncheck ed cont ext is
determined. The set consists of the union of the candidate operators provided by
X and the candidate operators provided by Y, each determined using the rules of
Candidate user-defined operators . If X and Y are the same type, or if X and Y
are derived from a common base type, then shared candidate operators only occur
in the combined set once.
If the set of candidate user-defined operators is not empty, then this becomes the
set of candidate operators for the operation. Otherwise, the set of candidate user-
defined operators provided by X and Y for the operation operator op(x,y)
matching the opposit e check ed/uncheck ed cont ext is determined. The set
consists of the union of the candidate operators provided by X and the candidate
operators provided by Y, each determined using the rules of Candidate user-
defined operators . If X and Y are the same type, or if X and Y are derived from
a common base type, then shared candidate operators only occur in the combined
set once.
C#
Example #1:
public class MyClass 
{ 
    public static void Add(Int128 lhs, Int128 rhs ) 
    { 
        // Resolves to `op_CheckedAddition`  
        Int128 r1 = checked(lhs + rhs);  
        // Resolves to `op_Addition`  
        Int128 r2 = unchecked (lhs + rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r3 = checked(lhs - rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r4 = unchecked (lhs - rhs);  
        // Resolves to `op_CheckedMultiply`  
        Int128 r5 = checked(lhs * rhs);  
        // Resolves to `op_CheckedMultiply`  
        Int128 r5 = unchecked (lhs * rhs);  
    } 
    public static void Divide(Int128 lhs, byte rhs) 
    { 
        // Resolves to `op_CheckedDivision`  C#        Int128 r4 = checked(lhs / rhs);  
    } 
} 
public struct Int128 
{ 
    public static Int128 operator  checked +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  -(Int128 lhs, Int128 rhs);  
    public static Int128 operator  checked *(Int128 lhs, Int128 rhs);  
    public static Int128 operator  checked /(Int128 lhs, int rhs); 
    public static Int128 operator  /(Int128 lhs, byte rhs); 
} 
Example #2:
class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // C1.op_CheckedAddition  
        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  checked + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    public static C2 operator  + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 
{ 
} 
Example #3:C#
C#class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // C2.op_CheckedAddition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    public static C2 operator  checked + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 
{ 
} 
Example #4:
class C 
{ 
    static void Add(C2 x, byte y) 
    { 
        object o; 
         
        // C1.op_CheckedAddition  
        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  
    } 
    static void Add2(C2 x, int y) 
    { 
        object o; 
         
        // C2.op_Addition  C#        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  checked + (C1 x, byte y) => new C1(); 
} 
class C2 : C1 
{ 
    public static C2 operator  + (C2 x, int y) => new C2(); 
} 
Example #5:
class C 
{ 
    static void Add(C2 x, byte y) 
    { 
        object o; 
         
        // C2.op_CheckedAddition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
    static void Add2(C2 x, int y) 
    { 
        object o; 
         
        // C1.op_Addition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  + (C1 x, int y) => new C1(); 
} 
class C2 : C1 Assuming that regular operator matches unchecked evaluation context and checked
operator matches checked evaluation context, the third bullet in
https://github.com/dotnet/csharplang/blob/main/spec/conversions.md#processing-of-
user-defined-explicit-conversions :
Find the set of applicable user-defined and lifted conversion operators, U. This
set consists of the user-defined and lifted implicit or explicit conversion
operators declared by the classes or structs in D that convert from a type
encompassing or encompassed by S to a type encompassing or encompassed
by T. If U is empty, the conversion is undefined and a compile-time error
occurs.
will be replaced with the following bullet points:
Find the set of applicable user-defined and lifted explicit conversion operators
matching the curr ent check ed/uncheck ed cont ext, U0. This set consists of the
user-defined and lifted explicit conversion operators declared by the classes or
structs in D that match the curr ent check ed/uncheck ed cont ext and convert from
a type encompassing or encompassed by S to a type encompassing or
encompassed by T.
Find the set of applicable user-defined and lifted explicit conversion operators
matching the opposit e check ed/uncheck ed cont ext, U1. If U0 is not empty, U1 is
empty. Otherwise, this set consists of the user-defined and lifted explicit
conversion operators declared by the classes or structs in D that match the
opposit e check ed/uncheck ed cont ext and convert from a type encompassing or
encompassed by S to a type encompassing or encompassed by T.
Find the set of applicable user-defined and lifted conversion operators, U. This set
consists of operators from U0, U1, and the user-defined and lifted implicit
conversion operators declared by the classes or structs in D that convert from a
type encompassing or encompassed by S to a type encompassing or
encompassed by T. If U is empty, the conversion is undefined and a compile-time
error occurs.{ 
    public static C2 operator  checked + (C2 x, byte y) => new C2(); 
} 
Processing of user-defined explicit conversions
The first bullet in section §11.4.4  will be adjusted as follows (additions are in bold).
The set of candidate user-defined operators provided by X for the operation
operator op(x) is determined using the rules of "Candidate user-defined
operators" section below. If the set contains at least one operat or in check ed
form, all operat ors in r egular form ar e remov ed fr om the set.
The section §11.7.18  will be adjusted to reflect the effect that the checked/unchecked
context has on unary operator overload resolution.
The first bullet in section §11.4.5  will be adjusted as follows (additions are in bold).
The set of candidate user-defined operators provided by X and Y for the
operation operator op(x,y) is determined. The set consists of the union of the
candidate operators provided by X and the candidate operators provided by Y,
each determined using the rules of "Candidate user-defined operators" section
below. If X and Y are the same type, or if X and Y are derived from a common
base type, then shared candidate operators only occur in the combined set once. If
the set contains at least one operat or in check ed form, all operat ors in r egular
form ar e remov ed fr om the set.
The Checked and unchecked operators §11.7.18  section will be adjusted to reflect the
effect that the checked/unchecked context has on binary operator overload resolution.
The https://github.com/dotnet/csharplang/blob/main/spec/expressions.md#candidate-
user-defined-operators  section will be adjusted as follows (additions are in bold).
Given a type T and an operation operator op(A), where op is an overloadable operator
and A is an argument list, the set of candidate user-defined operators provided by T for
operator op(A) is determined as follows:Yet another another way to build the set of candidate
user-defined operators
Unary operator overload resolution
Binary operator overload resolution
Candidate user-defined operators
Determine the type T0. If T is a nullable type, T0 is its underlying type, otherwise
T0 is equal to T.
For all operator op declarations in their check ed and r egular forms in checked
evaluation cont ext and only in their r egular form in unchecked evaluation
context in T0 and all lifted forms of such operators, if at least one operator is
applicable ( Applicable function member ) with respect to the argument list A,
then the set of candidate operators consists of all such applicable operators in T0.
Otherwise, if T0 is object, the set of candidate operators is empty.
Otherwise, the set of candidate operators provided by T0 is the set of candidate
operators provided by the direct base class of T0, or the effective base class of T0
if T0 is a type parameter.
Similar filtering will be applied while determining the set of candidate operators in
interfaces https://github.com/dotnet/csharplang/blob/main/meetings/2017/LDM-2017-
06-27.md#shadowing-within-interfaces .
The https://github.com/dotnet/csharplang/blob/main/spec/expressions.md#the-
checked-and-unchecked-operators  section will be adjusted to reflect the effect that
the checked/unchecked context has on unary and binary operator overload resolution.
C#
Example #1:
public class MyClass 
{ 
    public static void Add(Int128 lhs, Int128 rhs ) 
    { 
        // Resolves to `op_CheckedAddition`  
        Int128 r1 = checked(lhs + rhs);  
        // Resolves to `op_Addition`  
        Int128 r2 = unchecked (lhs + rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r3 = checked(lhs - rhs);  
        // Resolve to `op_Subtraction`  
        Int128 r4 = unchecked (lhs - rhs);  
        // Resolves to `op_CheckedMultiply`  
        Int128 r5 = checked(lhs * rhs);  
        // Error: Operator '*' cannot be applied to operands of type  
'Int128' and 'Int128'  
        Int128 r5 = unchecked (lhs * rhs);  C#    } 
    public static void Divide(Int128 lhs, byte rhs) 
    { 
        // Resolves to `op_CheckedDivision`  
        Int128 r4 = checked(lhs / rhs);  
    } 
} 
public struct Int128 
{ 
    public static Int128 operator  checked +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  +(Int128 lhs, Int128 rhs);  
    public static Int128 operator  -(Int128 lhs, Int128 rhs);  
    public static Int128 operator  checked *(Int128 lhs, Int128 rhs);  
    public static Int128 operator  checked /(Int128 lhs, int rhs); 
    public static Int128 operator  /(Int128 lhs, byte rhs); 
} 
Example #2:
class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // C1.op_CheckedAddition  
        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  checked + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    public static C2 operator  + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 C#
C#{ 
} 
Example #3:
class C 
{ 
    static void Add(C2 x, C3 y ) 
    { 
        object o; 
         
        // C2.op_CheckedAddition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  + (C1 x, C3 y) => new C3(); 
} 
class C2 : C1 
{ 
    public static C2 operator  checked + (C2 x, C1 y) => new C2(); 
} 
class C3 : C1 
{ 
} 
Example #4:
class C 
{ 
    static void Add(C2 x, byte y) 
    { 
        object o; 
         
        // C2.op_Addition  
        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  C#    } 
    static void Add2(C2 x, int y) 
    { 
        object o; 
         
        // C2.op_Addition  
        o = checked(x + y);  
         
        // C2.op_Addition  
        o = unchecked (x + y);  
    } 
} 
class C1 
{ 
    public static C1 operator  checked + (C1 x, byte y) => new C1(); 
} 
class C2 : C1 
{ 
    public static C2 operator  + (C2 x, int y) => new C2(); 
} 
Example #5:
class C 
{ 
    static void Add(C2 x, byte y) 
    { 
        object o; 
         
        // C2.op_CheckedAddition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
    static void Add2(C2 x, int y) 
    { 
        object o; 
         
        // C1.op_Addition  
        o = checked(x + y);  
         
        // C1.op_Addition  
        o = unchecked (x + y);  
    } 
} The third bullet in §10.5.5 :
Find the set of applicable user-defined and lifted conversion operators, U. This
set consists of the user-defined and lifted implicit or explicit conversion
operators declared by the classes or structs in D that convert from a type
encompassing or encompassed by S to a type encompassing or encompassed
by T. If U is empty, the conversion is undefined and a compile-time error
occurs.
will be replaced with the following bullet points:
Find the set of applicable user-defined and lifted explicit conversion operators, U0.
This set consists of the user-defined and lifted explicit conversion operators
declared by the classes or structs in D in their check ed and r egular forms in
checked evaluation cont ext and only in their r egular form in unchecked
evaluation cont ext and convert from a type encompassing or encompassed by S
to a type encompassing or encompassed by T.
If U0 contains at least one operator in checked form, all operators in regular form
are removed from the set.
Find the set of applicable user-defined and lifted conversion operators, U. This set
consists of operators from U0, and the user-defined and lifted implicit conversion
operators declared by the classes or structs in D that convert from a type
encompassing or encompassed by S to a type encompassing or encompassed by
T. If U is empty, the conversion is undefined and a compile-time error occurs.
The Checked and unchecked operators §11.7.18  section will be adjusted to reflect the
effect that the checked/unchecked context has on processing of user-defined explicit
conversions.class C1 
{ 
    public static C1 operator  + (C1 x, int y) => new C1(); 
} 
class C2 : C1 
{ 
    public static C2 operator  checked + (C2 x, byte y) => new C2(); 
} 
Processing of user-defined explicit conversions
The compiler could treat the default context of a checked operator as checked. The
developer would need to explicitly use unchecked if part of their algorithm should not
participate in the checked context. However, this might not work well in the future if we
start allowing checked/unchecked tokens as modifiers on operators to set the context
within the body. The modifier and the keyword could contradict each other. Also, we
wouldn't be able to do the same (treat default context as unchecked) for a regular
operator because that would be a breaking change.
Should the language allow checked and unchecked modifiers on methods (e.g. static
checked void M())? This would allow removing nesting levels for methods that require it.
There is no factory method to create a checked division node and there is no
ExpressionType.DivideChecked member. W e could still use the following factory method
to create regular divide node with MethodInfo pointing to the op_CheckedDivision
method. Consumers will have to check the name to infer the context.
C#
Note, even though §11.7.18  section lists / operator as one of the operators affected
by checked/unchecked evaluation context, IL doesn't have a special op code to perform
checked division. Compiler always uses the factory method reardless of the context
today.
Proposal: Checked user-defined devision will not be supported in Linq Expression T rees.
In general, implicit conversion operators are not supposed to throw.
Proposal: No.Checked vs. unchecked context within a checked operator
Unresolved questions
Checked division in Linq Expression Trees
public static BinaryExpression Divide (Expression left, Expression right,  
MethodInfo? method ); 
(Resolved) Should we support implicit checked
conversion operators?Resolution:  Approved -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
07.md#checked-implicit-conversions
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
07.md  https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-
02-09.md  https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-
2022-02-14.md
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
23.md
Design meetings
Unsigned right shift operator
Article •06/23/2023
An unsigned right shift operator will be supported by C# as a built-in operator (for
primitive integral types) and as a user-defined operator.
When working with signed integral value, it is not uncommon that you need to shift bits
right without replicating the high order bit on each shift. While this can be achieved for
primitive integral types with a regular shift operator, a cast to an unsigned type before
the shift operation and a cast back after it is required. Within the context of the generic
math interfaces the libraries are planning to expose, this is potentially more problematic
as the type might not necessary have an unsigned counterpart defined or known
upfront by the generic math code, yet an algorithm might rely on ability to perform an
unsigned right shift operation.
Section §6.4.6  will be adjusted to include >>> operator - the unsigned right shift
operator:
antlr７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Detailed design
Operators and punctuators
No characters of any kind (not even whitespace) are allowed between the tokens in
unsigned_r ight_shi ft and unsigned_r ight_shi ft_assignment  productions. These productions
are treated specially in order to enable the correct handling of type_p aramet er_list s.
Section §11.10  will be adjusted to include >>> operator - the unsigned right shift
operator:
The <<, >> and >>> operators are used to perform bit shifting operations.
antlr
For an operation of the form x << count or x >> count or x >>> count, binary operator
overload resolution ( §11.4.5 ) is applied to select a specific operator implementation.
The operands are converted to the parameter types of the selected operator, and the
type of the result is the return type of the operator.
The predefined unsigned shift operators will support the same set of signatures that
predefined signed shift operators support today in the current implementation.
Shift right:
C#unsigned_right_shift  
    : '>>>' 
    ; 
unsigned_right_shift_assignment  
    : '>>>=' 
    ; 
Shift operators
shift_expression  
    : additive_expression  
    | shift_expression '<<' additive_expression  
    | shift_expression right_shift additive_expression  
    | shift_expression unsigned_right_shift additive_expression  
    ; 
int operator  >>>(int x, int count);  
uint operator  >>>(uint x, int count);  
long operator  >>>(long x, int count);  
ulong operator  >>>(ulong x, int count);  
nint operator  >>>(nint x, int count);  
nuint operator  >>>(nuint x, int count);  The >>> operator shifts x right by a number of bits computed as described below.
The low-order bits of x are discarded, the remaining bits are shifted right, and the
high-order empty bit positions are set to zero.
For the predefined operators, the number of bits to shift is computed as follows:
When the type of x is int or uint, the shift count is given by the low-order five
bits of count. In other words, the shift count is computed from count & 0x1F.
When the type of x is long or ulong, the shift count is given by the low-order six
bits of count. In other words, the shift count is computed from count & 0x3F.
If the resulting shift count is zero, the shift operators simply return the value of x.
Shift operations never cause overflows and produce the same results in checked and
unchecked contexts.
Section §11.18  will be adjusted to include unsigned_r ight_shi ft_assignment  as follows:
antlr
The Integral types §8.3.6  section will be adjusted to include information about >>>
operator. The relevant bullet point is the following:
For the binary <<, >> and >>> operators, the left operand is converted to type T,
where T is the first of int, uint, long, and ulong that can fully represent allAssignment operators
assignment_operator  
    : '=' 
    | '+=' 
    | '-=' 
    | '*=' 
    | '/=' 
    | '%=' 
    | '&=' 
    | '|=' 
    | '^=' 
    | '<<=' 
    | right_shift_assignment  
    | unsigned_right_shift_assignment  
    ; 
Integral types
possible values of the operand. The operation is then performed using the
precision of type T, and the type of the result is T.
Operator >>> will be added to the set of constructs permitted in constant expressions at
§11.20 .
Operator >>> will be added to the set of overloadable binary operators at §11.4.3 .
Operator >>> will be added to the set of binary operators permitting a lifted form at
§11.4.8 .
Section §11.4.2  will be adjusted to add >>> operator to the "Shift" category and >>>=
operator to the "Assignment and lambda expression" category.
The >>> operator is subject to the same grammar ambiguities described at §6.2.5  as a
regular >> operator.
The §14.10  section will be adjusted to include >>> operator.
antlrConstant expressions
Operator overloading
Lifted operators
Operator precedence and associativity
Grammar ambiguities
Operators
overloadable_binary_operator  
    : '+'   | '-'   | '*'   | '/'   | '%'   | '&'   | '|'   | '^'   | '<<' 
    | right_shift | unsigned_right_shift | '=='  | '!='  | '>'   | '<'   | 
'>='  | '<=' 
    ; 
Binary operatorsThe signature of a >>> operator is subject to the same rules as those at §14.10.3  for
the signature of a >> operator.
Section "I.10.3.2 Binary operators" of ECMA-335 already reserved the name for an
unsigned right shift operator - op_UnsignedRightShift.
The >>> operator will not be supported in Linq Expression T rees because semantics of
predefined >>> operators on signed types cannot be accurately represented without
adding conversions to an unsigned type and back. See
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
09.md#unsigned-right-shift-operator  for more information.
It looks like dynamic binding uses values of S ystem.Linq.Expressions.ExpressionT ype
enum to communicate binary operator kind to the runtime binder. Since we don't have
a member specifically representing an unsigned right shift operator, dynamic binding
for >>> operator will not be supported and the static and dynamic binding ( §11.3 )
section will be adjusted to reflect that.
The >>> operator will be supported in Linq Expressioin T rees.
For a user-defined operator, a BinaryExpression node pointing to the operator
method will be created.
For predefined operators
when the first operand is an ansigned type, a BinaryExpression node will be
created.
when the first operand is a signed type, a conversion for the first operand to an
unsigned type will be added, a BinaryExpression node will be created and
Metadata name
Linq Expression Trees
Dynamic Binding
Drawbacks
Alternatives
Linq Expression Treesconversion for the result back to the signed type will be added.
For example:
C#
Resolution:
Rejected, see https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-
2022-02-09.md#unsigned-right-shift-operator  for more information.
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
09.mdExpression<System.Func< int, int, int>> z = (x, y) => x >>> y; // (x, y) =>  
Convert((Convert(x, UInt32) >> y), Int32)  
Unresolved questions
Design meetings
Relaxing shift operator requirements
Article •06/23/2023
The shift operator requirements will be relaxed so that the right-hand side operand is no
longer restricted to only be int.
When working with types other than int, it is not uncommon that you shift using the
result of another computation, such as shifting based on the leading zero count. The
natural type of something like a leading zero count is the same as the input type
(TSelf) and so in many cases, this requires you to convert that result to int before
shifting, even if that result is already within range.
Within the context of the generic math interfaces the libraries are planning to expose,
this is potentially problematic as the type is not well known and so the conversion to
int may not be possible or even well-defined.
§11.10  should be reworded as follows:
diff７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Detailed design
Shift operators
That is, the restriction that the first operand be the class or struct containing the
operator declaration remains. While the restriction that the second operand must be
int is removed.
§14.10.3  should be reworded as follows:
diff
That is, the restriction that the first parameter be T or T? remains. While the restriction
that the second operand must be int or int? is removed.
The first bullet point at §11.4.5  should be reworded as follows:
The set of candidate user-defined operators provided by X and Y for the
operation operator op(x,y) is determined. The set consists of the union of the
candidate operators provided by X and , unless the operat or is a shif t operat or,
the candidate operators provided by Y, each determined using the rules of
Candidate user-defined operators §11.4.6 . If X and Y are the same type, or if X
and Y are derived from a common base type, then shared candidate operators
only occur in the combined set once.
That is, for shift operators, candidate operators are only those provided by type X.- When declaring an overloaded shift operator, the type of the first operand  
must always be the class or struct containing the operator declaration,  
and the type of the second operand must always be int.  
+ When declaring an overloaded shift operator, the type of the first operand  
must always be the class or struct containing the operator declaration.  
Binary operators
-*  A binary `<<` or `>>` operator must take two parameters, the first of  
which must have type `T` or `T?` and the second of which must have type  
`int` or `int?`, and can return any type.  
+*  A binary `<<` or `>>` operator must take two parameters, the first of  
which must have type `T` or `T?`, and can return any type.  
Binary operator overload resolution
DrawbacksUsers will be able to define operators that do not follow the recommended guidelines,
such as implementing cout << "string" in C#.
The generic math interfaces being exposed by the libraries could expose explicitly
named methods instead. This may make code more difficult to read/maintain.
The generic math interfaces could require the shift take int and that a conversion be
performed. This conversion may be expensive or may be not possible depending on the
type in question.
Is there concern around preserving the "intent" around why the second operand was
restricted to int?
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
09.mdAlternatives
Unresolved questions
Design meetings
Numeric IntPtr
Article •09/30/2022
This is a revision on the initial native integers feature ( spec ), where the nint/nuint
types were distinct from the underlying types System.IntPtr/System.UIntPtr. In short,
we now treat nint/nuint as simple types aliasing System.IntPtr/System.UIntPtr, like
we do for int in relation to System.Int32. The
System.Runtime.CompilerServices.RuntimeFeature.NumericIntPtr runtime feature flag
triggers this new behavior.
C# provides a set of predefined struct types called the simple types. The simple types
are identified through keywords, but these keywords are simply aliases for predefined
struct types in the System namespace, as described in the table below.
Keyword Aliased type
sbyte System.SByte
byte System.Byte
short System.Int16
ushort System.UInt16７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Design
8.3.5 Simple typesKeyword Aliased type
int System.Int32
uint System.UInt32
nint System.IntPtr
nuint System.UIntPtr
long System.Int64
ulong System.UInt64
char System.Char
float System.Single
double System.Double
bool System.Boolean
decimal System.Decimal
[...]
C# supports eleven integral types: sbyte, byte, short, ushort, int, uint, nint, nuint,
long, ulong, and char. [...]
In other words, an unmanaged_type  is one of the following:
sbyte, byte, short, ushort, int, uint, nint, nuint, long, ulong, char, float,
double, decimal, or bool.
Any enum_type .
Any user-defined struct_type  that is not a constructed type and contains fields of
unmanaged_type s only.
In unsafe code, any point er_type .
The implicit numeric conversions are:8.3.6 Integral types
8.8 Unm anaged types
10.2.3 Implicit numeric conversionsFrom sbyte to short, int, nint, long, float, double, or decimal.
From byte to short, ushort, int, uint, nint, nuint, long, ulong, float, double,
or decimal.
From short to int, nint, long, float, double, or decimal.
From ushort to int, uint, nint, nuint, long, ulong, float, double, or decimal.
From int to nint, long, float, double, or decimal.
From uint to nuint, long, ulong, float, double, or decimal.
From nint to long, float, double, or decimal.
From nuint to ulong, float, double, or decimal.
From long to float, double, or decimal.
From ulong to float, double, or decimal.
From char to ushort, int, uint, nint, nuint, long, ulong, float, double, or
decimal.
From float to double.
[...]
An implicit constant expression conversion permits the following conversions:
A constant_expr ession  of type int can be converted to type sbyte, byte, short,
ushort, uint, nint, nuint, or ulong, provided the value of the constant_expr ession
is within the range of the destination type. [...]
The explicit numeric conversions are the conversions from a numer ic_type  to another
numer ic_type  for which an implicit numeric conversion does not already exist:
From sbyte to byte, ushort, uint, nuint, ulong, or char.
From byte to sbyte or char.
From short to sbyte, byte, ushort, uint, nuint, ulong, or char.
From ushort to sbyte, byte, short, or char.
From int to sbyte, byte, short, ushort, uint, nuint, ulong, or char.
From uint to sbyte, byte, short, ushort, int, nint, or char.
From long to sbyte, byte, short, ushort, int, uint, nint, nuint, ulong, or char.
From nint to sbyte, byte, short, ushort, int, uint, nuint, ulong, or char.
From nuint to sbyte, byte, short, ushort, int, uint, nint, long, or char.10.2.11 Implicit constant expression conversions
10.3.2 Explicit numeric conversionsFrom ulong to sbyte, byte, short, ushort, int, uint, nint, nuint, long, or char.
From char to sbyte, byte, or short.
From float to sbyte, byte, short, ushort, int, uint, nint, nuint, long, ulong,
char, or decimal.
From double to sbyte, byte, short, ushort, int, uint, nint, nuint, long, ulong,
char, float, or decimal.
From decimal to sbyte, byte, short, ushort, int, uint, nint, nuint, long,
ulong, char, float, or double.
[...]
The explicit enumeration conversions are:
From sbyte, byte, short, ushort, int, uint, nint, nuint, long, ulong, char,
float, double, or decimal to any enum_type .
From any enum_type  to sbyte, byte, short, ushort, int, uint, nint, nuint, long,
ulong, char, float, double, or decimal.
From any enum_type  to any other enum_type .
Given two types T₁ and T₂, T₁ is a better conversion t arget than T₂ if one of the
following holds:
An implicit conversion from T₁ to T₂ exists and no implicit conversion from T₂ to
T₁ exists
T₁ is Task<S₁>, T₂ is Task<S₂>, and S₁ is a better conversion target than S₂
T₁ is S₁ or S₁? where S₁ is a signed integral type, and T₂ is S₂ or S₂? where S₂
is an unsigned integral type. Specifically: [...]
[...] The number of expressions in the argument_list  shall be the same as the rank of the
array_type , and each expression shall be of type int, uint, nint, nuint, long, or
ulong, or shall be implicitly convertible to one or more of these types.10.3.3 Explicit enumeration conversions
11.6.4.6 Better conversion target
11.7.10 Element access
11.7.10.2 Array access[...] The number of expressions in the argument_list  shall be the same as the rank of the
array_type , and each expression shall be of type int, uint, nint, nuint, long, or
ulong, or shall be implicitly convertible to one or more of these types.
[...] The run-time processing of an array access of the form P[A], where P is a
primary_no_arr ay_cr eation_expr ession  of an array_type  and A is an argument_list ,
consists of the following steps: [...]
The index expressions of the argument_list  are evaluated in order, from left to
right. Following evaluation of each index expression, an implicit conversion to one
of the following types is performed: int, uint, nint, nuint, long, ulong. The first
type in this list for which an implicit conversion exists is chosen. [...]
Unary operator overload resolution is applied to select a specific operator
implementation. Predefined ++ and -- operators exist for the following types: sbyte,
byte, short, ushort, int, uint, nint, nuint, long, ulong, char, float, double,
decimal, and any enum type.
The predefined unary plus operators are:
C#
The predefined unary minus operators are:
Integer negation:
C#11.7.14 Postfix increment and decrement operators
11.8.2 Unary plus operator
... 
nint operator  +(nint x); 
nuint operator  +(nuint x); 
11.8.3 Unary minus operator
... 
nint operator  –(nint x); Predefined ++ and -- operators exist for the following types: sbyte, byte, short,
ushort, int, uint, nint, nuint, long, ulong, char, float, double, decimal, and any
enum type.
In addition, a default_v alue_expr ession  is a constant expression if the type is one of the
following value types: sbyte, byte, short, ushort, int, uint, nint, nuint, long, ulong,
char, float, double, decimal, bool, or any enumeration type.
The predefined bitwise complement operators are:
C#
Predefined ++ and -- operators exist for the following types: sbyte, byte, short,
ushort, int, uint, nint, nuint, long, ulong, char, float, double, decimal, and any
enum type.
The predefined multiplication operators are listed below. The operators all compute the
product of  x and y.
Integer multiplication:
C#11.7.14 Postfix increment and decrement operators
11.7.19 Default value expressions
11.8.5 Bitwise complement operator
... 
nint operator  ~(nint x); 
nuint operator  ~(nuint x); 
11.8.6 Prefix increment and decrement operators
11.9 Arithmetic operators
11.9.2 Multiplication operator
... 
nint operator  *(nint x, nint y); The predefined division operators are listed below. The operators all compute the
quotient of x and y.
Integer division:
C#
The predefined remainder operators are listed below. The operators all compute the
remainder of the division between x and y.
Integer remainder:
C#
Integer addition:
C#
Integer subtraction:nuint operator  *(nuint x, nuint y); 
11.9.3 Division operator
... 
nint operator  /(nint x, nint y); 
nuint operator  /(nuint x, nuint y); 
11.9.4 Remainder operator
... 
nint operator  %(nint x, nint y); 
nuint operator  %(nuint x, nuint y); 
11.9.5 Addition operator
... 
nint operator  +(nint x, nint y); 
nuint operator  +(nuint x, nuint y); 
11.9.6 Subtraction operatorC#
The predefined shift operators are listed below.
Shift left:
C#
Shift right:
C#
The >> operator shifts x right by a number of bits computed as described below.
When x is of type int, nint or long, the low-order bits of  x are discarded, the
remaining bits are shifted right, and the high-order empty bit positions are set to
zero if x is non-negative and set to one if x is negative.
When x is of type uint, nuint or ulong, the low-order bits of  x are discarded, the
remaining bits are shifted right, and the high-order empty bit positions are set to
zero.
Unsigned shift right:
C#... 
nint operator  –(nint x, nint y); 
nuint operator  –(nuint x, nuint y); 
11.10 Shift operators
... 
nint operator  <<(nint x, int count);  
nuint operator  <<(nuint x, int count);  
... 
nint operator  >>(nint x, int count);  
nuint operator  >>(nuint x, int count);  
... 
nint operator  >>>(nint x, int count);  
nuint operator  >>>(nuint x, int count);  For the predefined operators, the number of bits to shift is computed as follows: [...]
When the type of  x is nint or nuint, the shift count is given by the low-order five
bits of count on a 32 bit platform, or the lower-order six bits of count on a 64 bit
platform.
The predefined integer comparison operators are:
C#
The predefined integer logical operators are:
C#11.11 Relational and type-testing operators
11.11.2 Integer comparison operators
... 
bool operator  ==(nint x, nint y); 
bool operator  ==(nuint x, nuint y); 
bool operator  !=(nint x, nint y); 
bool operator  !=(nuint x, nuint y); 
bool operator  <(nint x, nint y); 
bool operator  <(nuint x, nuint y); 
bool operator  >(nint x, nint y); 
bool operator  >(nuint x, nuint y); 
bool operator  <=(nint x, nint y); 
bool operator  <=(nuint x, nuint y); 
bool operator  >=(nint x, nint y); 
bool operator  >=(nuint x, nuint y); 
11.12 Logical operators
11.12.2 Integer logical operators
... 
nint operator  &(nint x, nint y); 
nuint operator  &(nuint x, nuint y); A constant expression may be either a value type or a reference type. If a constant
expression is a value type, it must be one of the following types: sbyte, byte, short,
ushort, int, uint, nint, nuint, long, ulong, char, float, double, decimal, bool, or
any enumeration type.
[...]
An implicit constant expression conversion permits a constant expression of type int to
be converted to sbyte, byte, short, ushort, uint, nint, nuint, or ulong, provided the
value of the constant expression is within the range of the destination type.
Array elements are accessed using element_ac cess expressions of the form A[I₁, I₂,
..., Iₓ], where A is an expression of an array type and each Iₑ is an expression of
type int, uint, nint, nuint, long, ulong, or can be implicitly converted to one or more
of these types. The result of an array element access is a variable, namely the array
element selected by the indices.
[...]
Additionally, in an unsafe context, the set of available explicit conversions is extended to
include the following explicit pointer conversions:
From any point er_type  to any other point er_type .
From sbyte, byte, short, ushort, int, uint, nint, nuint, long, or ulong to any
point er_type .nint operator  |(nint x, nint y); 
nuint operator  |(nuint x, nuint y); 
nint operator  ^(nint x, nint y); 
nuint operator  ^(nuint x, nuint y); 
11.20 Constant expressions
16.4 Array element access
22.5 Pointer conversions
22.5.1 GeneralFrom any point er_type  to sbyte, byte, short, ushort, int, uint, nint, nuint,
long, or ulong.
[...] In a pointer element access of the form P[E], P shall be an expression of a pointer
type other than void*, and E shall be an expression that can be implicitly converted to
int, uint, nint, nuint, long, or ulong.
In an unsafe context, the + operator and – operator can be applied to values of all
pointer types except void*. Thus, for every pointer type T*, the following operators are
implicitly defined:
C#
Given an expression P of a pointer type T* and an expression N of type int, uint,
nint, nuint, long, or ulong, the expressions P + N and N + P compute the pointer
value of type T* that results from adding N * sizeof(T) to the address given by P.
Likewise, the expression P – N computes the pointer value of type T* that results from
subtracting N * sizeof(T) from the address given by P.
One of the main impacts of this design is that System.IntPtr and System.UIntPtr gain
some built-in operators (conversions, unary and binary).  
Those include checked operators, which means that the following operators on those
types will now throw when overflowing:
IntPtr + int22.6.4 Pointer element access
22.6.7 Pointer arithmetic
[...] 
T* operator  +(T* x, nint y); 
T* operator  +(T* x, nuint y); 
T* operator  +(nint x, T* y);  
T* operator  +(nuint x, T* y);  
T* operator  -(T* x, nint y); 
T* operator  -(T* x, nuint y); 
Various considerations
Breaking changesIntPtr - int
IntPtr -> int
long -> IntPtr
void* -> IntPtr
This design means that nint and nuint can simply be emitted as System.IntPtr and
System.UIntPtr, without the use of
System.Runtime.CompilerServices.NativeIntegerAttribute. 
Similarly, when loading metadata NativeIntegerAttribute can be ignored.Metadata encodingRaw string literal
Article •01/10/2023
Allow a new form of string literal that starts with a minimum of three """ characters
(but no maximum), optionally followed by a new_line, the content of the string, and
then ends with the same number of quotes that the literal started with. For example:
Because the nested contents might itself want to use """ then the starting/ending
delimiters can be longer like so:
To make the text easy to read and allow for indentation that developers like in code,
these string literals will naturally remove the indentation specified on the last line when
producing the final literal value. For example, a literal of the form:７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
var xml = """  
          <element attr="content"/>  
          """;  
var xml = """"  
          Ok to use """ here  
          """";  Will have the contents:
This allows code to look natural, while still producing literals that are desired, and
avoiding runtime costs if this required the use of specialized string manipulation
routines.
If the indentation behavior is not desired, it is also trivial to disable like so:
A single line form is also supported. It starts with a minimum of three """ characters
(but no maximum), the content of the string (which cannot contain any new_line
characters), and then ends with the same number of quotes that the literal started with.
For example:
Interpolated raw strings are also supported. In this case, the string specifies the number
of braces needed to start an interpolation (determined by the number of dollar signs
present at the start of the literal). Any brace sequence with fewer braces than that is just
treated as content. For example:var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
          """;  
<element attr="content">  
  <body>  
  </body>  
</element>  
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
"""; 
var xml = """<summary><element attr="content"/></summary>""";  C# lacks a general way to create simple string literals that can contain effectively any
arbitrary text. All C# string literal forms today need some form of escaping in case the
contents use some special character (always if a delimiter is used). This prevents easily
having literals containing other languages in them (for example, an XML, HTML or JSON
literal).
All current approaches to form these literals in C# today always force the user to
manually escape the contents. Editing at that point can be highly annoying as the
escaping cannot be avoided and must be dealt with whenever it arises in the contents.
This is particularly painful for regexes, especially when they contain quotes or
backslashes. Even with a @"" string, quotes themselves must be escaped leading to a
mix of C# and regex interspersed. { and } are similarly frustrating in $"" strings.
The crux of the problem is that all our strings have a fixed start/end delimiter. As long as
that is the case, we will always have to have an escaping mechanism as the string
contents may need to specify that end delimiter in their contents. This is particularly
problematic as that delimiter " is exceedingly common in many languages.
To address this, this proposal allows for flexible start and end delimiters so that they can
always be made in a way that will not conflict with the content of the string.
1. Provide a mechanism that will allow all string values to be provided by the user
without the need for any escape-sequences whatsoever. Because all strings must
be representable without escape-sequences, it must always be possible for the
user to specify delimiters that will be guaranteed to not collide with any text
contents.
2. Support interpolations in the same fashion. As above, because all strings must be
representable without escapes, it must always be possible for the user to specify an
interpolation delimiter that will be guaranteed to not collide with any textvar json = $$"""  
             {  
                "summary": "text",  
                "length" : {{value.Length}},  
             };  
             """  
Motivation
Goalscontents. Importantly, languages that use our interpolation delimiter characters
({ and }) should feel first-class and not painful to use.
3. Multiline string literals should look pleasant in code and should not make
indentation within the compilation unit look strange. Importantly, literal values that
themselves have no indentation should not be forced to occupy the first column of
the file as that can break up the flow of code and will look unaligned with the rest
of the code that surrounds it.
This behavior should be easy to override while keeping literals clear and easy
to read.
4. For all strings that do not themselves contain a new_line or start or end with a
quote (") character, it should be possible to represent the string literal itself on a
single line.
Optionally, with extra complexity, we could refine this to state that: For all
strings that do not themselves contain a new_line (but can start or end with a
quote " character), it should be possible to represent the string literal itself
on a single line. For more details see the expanded proposal in the Drawbacks
section.
We will add a new string_literal production with the following form:Detailed design (non-interpolation case)
string_literal  
    : regular_string_literal  
    | verbatim_string_literal  
    | raw_string_literal  
    ; 
raw_string_literal  
    : single_line_raw_string_literal  
    | multi_line_raw_string_literal  
    ; 
raw_string_literal_delimiter  
    : """  
    | """"  
    | """""  
    | etc.  
    ; 
raw_content  The ending delimiter to a raw_string_literal must match the starting delimiter. So if
the starting delimiter is """"" the ending delimiter must be that as well.
The above grammar for a raw_string_literal should be interpreted as:
1. It starts with at least three quotes (but no upper bound on quotes).
2. It then continues with contents on the same line as the starting quotes. These
contents on the same line can be blank, or non-blank. 'blank' is synonymous with
'entirely whitespace'.
3. If the contents on that same line is non-blank no further content can follow. In
other words the literal is required to end with the same number of quotes on that
same line.
4. If the contents on the same line is blank, then the literal can continue with a
new_line and some number of subsequent content lines and new_lines.
A content line is any text except a new_line.
It then ends with a new_line some number (possibly zero) of whitespace and
the same number of quotes that the literal started with.
The portions between the starting and ending raw_string_literal_delimiter are used
to form the value of the raw_string_literal in the following fashion:
In the case of single_line_raw_string_literal the value of the literal will exactly
be the contents between the starting and ending raw_string_literal_delimiter.
In the case of multi_line_raw_string_literal the initial whitespace* new_line and
the final new_line whitespace* is not part of the value of the string. However, the    : not_new_line+  
    ; 
single_line_raw_string_literal  
    : raw_string_literal_delimiter raw_content raw_string_literal_delimiter  
    ; 
multi_line_raw_string_literal  
    : raw_string_literal_delimiter whitespace* new_line (raw_content |  
new_line)* new_line whitespace* raw_string_literal_delimiter  
    ; 
not_new_line  
    : <any unicode character that is not new_line>  
    ; 
Raw string literal valuefinal whitespace* portion preceding the raw_string_literal_delimiter terminal is
considered the 'indentation whitespace' and will affect how the other lines are
interpreted.
To get the final value the sequence of (raw_content | new_line)* is walked and
the following is performed:
If it a new_line the content of the new_line is added to the final string value.
If it is not a 'blank' raw_content (i.e. not_new_line+ contains a non- whitespace
character):
the 'indentation whitespace' must be a prefix of the raw_content. It is an
error otherwise.
the 'indentation whitespace' is stripped from the start of raw_content and
the remainder is added to the final string value.
If it is a 'blank' raw_content (i.e. not_new_line+ is entirely whitespace):
the 'indentation whitespace' must be a prefix of the raw_content or the
raw_content must be a prefix of of the 'indentation whitespace'. It is an error
otherwise.
as much of the 'indentation whitespace' is stripped from the start of
raw_content and any remainder is added to the final string value.
1. A single_line_raw_string_literal is not capable of representing a string with a
new_line value in it. A single_line_raw_string_literal does not participate in the
'indentation whitespace' trimming. Its value is always the exact characters between
the starting and ending delimiters.
2. Because a multi_line_raw_string_literal ignores the final new_line of the last
content line, the following represents a string with no starting new_line and no
terminating new_line
This maintains symmetry with how the starting new_line is ignored, and it also provides
a uniform way to ensure the 'indentation whitespace' can always be adjusted. T o
represent a string with a terminal new_line an extra line must be provided like so:Clarifications:
var v1 = """  
         This is the entire content of the string.  
         """  3. A single_line_raw_string_literal cannot represent a string value that starts or
ends with a quote ( ") though an augmentation to this proposal is provided in the
Drawbacks section that shows how that could be supported.
4. A multi_line_raw_string_literal starts with whitespace* new_line following the
initial raw_string_literal_delimiter. This content after the delimiter is entirely
ignored and is not used in any way when determining the value of the string. This
allows for a mechanism to specify a raw_string_literal whose content starts with
a " character itself. For example:
5. A raw_string_literal can also represent content that end with a quote ( "). This is
supported as the terminating delimiter must be on its own line. For example:
5. The requirement that a 'blank' raw_content be either a prefix of the 'indentation
whitespace' or the 'indentation whitespace' must be a prefix of it helps ensure
confusing scenarios with mixed whitespace do not occur, especially as it would be
unclear what should happen with that line. For example, the following case is
illegal:var v1 = """  
         This string ends with a new line.  
         """  
var v1 = """  
         "The content of this string starts with a quote  
         """  
var v1 = """  
         "The content of this string starts and ends with a quote"  
         """  
var v1 = """  
         ""The content of this string starts and ends with two quotes""  
         """  6. Here the 'indentation whitespace' is nine space characters, but the 'blank'
raw_content does not start with a prefix of that. There is no clear answer as to how
that <tab> line should be treated at all. Should it be ignored? Should it be the
same as .........<tab>? As such, making it illegal seems the clearest for avoiding
confusion.
7. The following cases are legal though and represent the same string:
In both these cases, the 'indentation whitespace' will be nine spaces. And in both cases,
we will remove as much of that prefix as possible, leading the 'blank' raw_content in
each case to be empty (not counting every new_line). This allows users to not have to
see and potentially fret about whitespace on these lines when they copy/paste or edit
these lines.
8. In the case though of:var v1 = """  
         Start  
<tab> 
         End  
         """  
var v1 = """  
         Start  
<four spaces>  
         End  
         """  
var v1 = """  
         Start  
<nine spaces>  
         End  
         """  
var v1 = """  
         Start  
<ten spaces>  
         End  
         """  The 'indentation whitespace' will still be nine spaces. Here though, we will remove as
much of the 'indentation whitespace' as possible, and the 'blank' raw_content will
contribute a single space to the final content. This allows for cases where the content
does need whitespace on these lines that should be preserved.
9. The following is technically not legal:
This is because the start of the raw string must have a new_line (which it does) but the
end must have a new_line as well (which it does not). The minimal legal
raw_string_literal is:
However, this string is decidedly uninteresting as it is equivalent to "".
The 'indentation whitespace' algorithm can be visualized on several inputs like so:
is interpreted asvar v1 = """  
         """  
var v1 = """  
         """  
Indentation examples
Example 1 - Standard case
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
          """;  This is illegal. The last content line must end with a new_line.
is interpreted asvar xml = """  
          |<element attr="content">  
          |  <body>  
          |  </body>  
          |</element>  
           """;  
Example 2 - End delimiter on same line as content.
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>""";  
Example 3 - End delimiter before start delimiter
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
"""; 
var xml = """  
|          <element attr="content">  
|            <body>  
|            </body>  
|          </element>  
"""; 
Example 4 - End delimiter after start delimiterThis is illegal. The lines of content must start with the 'indentation whitespace'
is interpreted asvar xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
              """;  
Example 5 - Empty blank line
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
          </element>  
          """;  
var xml = """  
          |<element attr="content">  
          |  <body>  
          |  </body>  
          |  
          |</element>  
           """;  
Example 5 - Blank line with less whitespace than prefix
(dots represent spaces)
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
.... 
          </element>  
          """;  is interpreted as
is interpreted as
Interpolations in normal interpolated strings (e.g. $"...") are supported today through
the use of the { character to start an interpolation and the use of an {{ escape-
sequence to insert an actual open brace character. Using this same mechanism would
violate goals '1' and '2' of this proposal. Languages that have { as a core charactervar xml = """  
          |<element attr="content">  
          |  <body>  
          |  </body>  
          |  
          |</element>  
           """;  
Example 5 - Blank line with more whitespace than prefix
(dots represent spaces)
var xml = """  
          <element attr="content">  
            <body>  
            </body>  
..............  
          </element>  
          """;  
var xml = """  
          |<element attr="content">  
          |  <body>  
          |  </body>  
          |....  
          |</element>  
           """;  
Detailed design (interpolation case)(examples being JavaScript, JSON, R egex, and even embedded C#) would now need
escaping, undoing the purpose of raw string literals.
To support interpolations we introduce them in a different fashion than normal $"
interpolated strings. Specifically, an interpolated_raw_string_literal will start with
some number of $ characters. The count of these indicates how many { (and })
characters are needed in the content of the literal to delimit the interpolation.
Importantly, there continues to be no escaping mechanism for curly braces. Rather, just
as with quotes ( ") the literal itself can always ensure it specifies delimiters for the
interpolations that are certain to not collide with any of the rest of the content of the
string. For example a JSON literal containing interpolation holes can be written like so:
c#
Here, the {{...}} matches the requisite count of two braces specified by the $$
delimiter prefix. In the case of a single $ that means the interpolation is specified just as
{...} as in normal interpolated string literals. Importantly, this means that an
interpolated literal with N $ characters can have a sequence of 2*N-1 braces (of the
same type in a row). The last N braces will start (or end) an interpolation, and the
remaining N-1 braces will just be content. For example:
c#
In this case the inner two {{ and }} braces belong to the interpolation, and the outer
singular braces are just content. So the above string is equivalent to the content X{2}Z.
Having 2*N (or more) braces is always an error. To have longer sequences of braces as
content, the number of $ characters must be increased accordingly.
Interpolated raw string literals are defined as:var v1 = $$""" 
         {  
            " orders":  
            [  
                { " number": {{order_number}} }  
            ]  
         }  
         " "" 
var v1 = $$"""X{{{1+1}}}Z" ""; The above is similar to the definition of raw_string_literal but with some important
differences. A interpolated_raw_string_literal should be interpreted as:interpolated_raw_string_literal  
    : single_line_interpolated_raw_string_literal  
    | multi_line_interpolated_raw_string_literal  
    ; 
interpolated_raw_string_start  
    : $ 
    | $$  
    | $$$  
    | etc.  
    ; 
interpolated_raw_string_literal_delimiter  
    : interpolated_raw_string_start raw_string_literal_delimiter  
    ; 
single_line_interpolated_raw_string_literal  
    : interpolated_raw_string_literal_delimiter interpolated_raw_content  
raw_string_literal_delimiter  
    ; 
multi_line_interpolated_raw_string_literal  
    : interpolated_raw_string_literal_delimiter whitespace* new_line  
(interpolated_raw_content | new_line)* new_line whitespace*  
raw_string_literal_delimiter  
    ; 
interpolated_raw_content  
    : (not_new_line | raw_interpolation)+  
    ; 
raw_interpolation  
    : raw_interpolation_start interpolation raw_interpolation_end  
    ; 
raw_interpolation_start  
    : { 
    | {{  
    | {{{  
    | etc.  
    ; 
raw_interpolation_end  
    : } 
    | }}  
    | }}}  
    | etc.  
    ; 1. It starts with at least one dollar sign (but no upper bound) and then three quotes
(also with no upper bound).
2. It then continues with content on the same line as the starting quotes. This content
on the same line can be blank, or non-blank. 'blank' is synonymous with 'entirely
whitespace'.
3. If the content on that same line is non-blank no further content can follow. In
other words the literal is required to end with the same number of quotes on that
same line.
4. If the contents on the same line is blank, then the literal can continue with a
new_line and some number of subsequent content lines and new_lines.
A content line is any text except a new_line.
A content line can contain multiple raw_interpolation occurrences at any
position. The raw_interpolation must start with an equal number of open
braces ( {) as the number of dollar signs at the start of the literal.
If 'indentation whitespace' is not-empty, a raw_interpolation cannot
immediately follow a new_line.
The raw_interpolation will following the normal rules specified at §11.7.3 .
Any raw_interpolation must end with the same number of close braces ( })
as dollar signs and open braces.
Any interpolation can itself contain new-lines within in the same manner as
an interpolation in a normal verbatim_string_literal (@"").
It then ends with a new_line some number (possibly zero) of whitespace and
the same number of quotes that the literal started with.
Computation of the interpolated string value follows the same rules as a normal
raw_string_literal except updated to handle lines containing raw_interpolations.
Building the string value happens in the same fashion, just with the interpolation holes
replaced with whatever values those expressions produce at runtime. If the
interpolated_raw_string_literal is converted to a FormattableString then the values
of the interpolations are passed in their respective order to the arguments array to
FormattableString.Create. The rest of the content of the
interpolated_raw_string_literal after the 'indentation whitespace' has been stripped
from all lines will be used to generate format string passed to
FormattableString.Create, except with appropriately numbered {N} contents in each
location where a raw_interpolation occurred (or {N,constant} in the case if its
interpolation is of the form expression ',' constant_expression).
There is an ambiguity in the above specification. Specifically when a section of { in text
and { of an interpolation abut. For example:
This could be interpreted as: {{ {order_number } }} or { {{order_number}} }. However,
as the former is illegal (no C# expression could start with {) it would be pointless to
interpret that way. So we interpret in the latter fashion, where the innermost { and }
braces form the interpolation, and any outermost ones form the text. In the future this
might be an issue if the language ever supports any expressions that are surrounded by
braces. However, in that case, the recommendation would be to write such a case like
so: {{({some_new_expression_form})}}. Here, parentheses would help designate the
expression portion from the rest of the literal/interpolation. This has precedence already
with how ternary conditional expressions need to be wrapped to not conflict with the
formatting/alignment specifier of an interpolation (e.g. {(x ? y : z)}).
Examples: (upcoming)
Raw string literals add more complexity to the language. We already have many string
literal forms already for numerous purposes. "" strings, @"" strings, and $"" strings
already have a lot of power and flexibility. But they all lack a way to provide raw
contents that never need escaping.
The above rules do not support the case of 4.a:
4. ...
Optionally, with extra complexity, we could refine this to state that: For all
strings that do not themselves contain a new_line (but can start or end with a
quote " character), it should be possible to represent the string literal itself
on a single line.
That's because we have no means to know that a starting or ending quote ( ") should
belong to the contents and not the delimiter itself. If this is an important scenario we
want to support though, we can add a parallel ''' construct to go along with the """
form. With that parallel construct, a single line string that start and ends with " can be
written easily as '''"This string starts and ends with quotes"''' along with the
parallel construct """'This string starts and ends with apostrophes'""". This may also
be desirable to support to help visually separate out quote characters, which may helpvar v1 = $$"""  
         {{{order_number}}}  
         """  
Drawbackswhen embedding languages that primarily use one quote character much more than
then other.
https://github.com/dotnet/csharplang/discussions/89  covers many options here.
Alternatives are numerous, but i feel stray too far into complexity and poor ergonomics.
This approach opts for simplicity where you just keep increasing the start/end quote
length until there is no concern about a conflict with the string contents. It also allows
the code you write to look well indented, while still producing a dedented literal that is
what most code wants.
One of the most interesting potential variations though is the use of ` (or ```) fences
for these raw string literals. This would have several benefits:
1. It would avoid all the issues with strings starting er ending with quotes.
2. It would look familiar to markdown. Though that in itself is potentially not a good
thing as users might expect markdown interpretation.
3. A raw string literal would only have to start and end with a single character in most
cases, and would only need multiple in the much rarer case of contents that
contain back-ticks themselves.
4. It would feel natural to extend this in the future with ```xml, again akin to
markdown. Though, of course, that is also true of the """ form.
Overall though, the net benefit here seems small. In keeping with C# history, i think "
should continue to be the string literal delimiter, just as it is for @"" and $"".
[x] should we have a single line form? We technically could do without it. But it
would mean simple strings not containing a newline would always take at least
three lines. I think we should It's very heavyweight to force single line constructs to
be three lines just to avoid escaping.
Design decision: Y es, we will have a single line form.
[x] should we require that multiline must  start with a newline? I think we should. It
also gives us the ability to support things like """xml in the future.Alternatives
Design meetings
Open issues to discuss Resolved issues:Design decision: Y es, we will require that multiline must start with a newline
[x] should the automatic dedenting be done at all? I think we should. It makes
code look so much more pleasant.
Design decision: Y es, automatic dedenting will be done.
[x] should we restrict common-whitespace from mixing whitespace types? I don't
think we should. Indeed, there is a common indentation strategy called "tab for
indentation, space for alignment". It would be very natural to use this to align the
end delimiter with the start delimiter in a case where the start delimiter doesn't
start on a tab stop.
Design decision: W e will not have any restrictions on mixing whitespace.
[x] should we use something else for the fences? ` would match markdown syntax,
and would mean we didn't need to always start these strings with three quotes.
Just one would suffice for the common case.
Design decision: W e will use """
[x] should we have a requirement that the delimiter have more quotes than the
longest sequence of quotes in the string value? Technically it's not required. for
example:
This is a string with """ as the delimiter. Several community members have stated this is
confusing and we should require in a case like this that the delimiter always have more
characters. That would then be:
Design decision: Y es, the delimiter must be longer than any sequence of quotes in the
string itself.var v = """  
        contents"""""  
        """  
var v = """"""  
        contents"""""  
        """"""  Allow new-lines in all interpolations
Article •06/23/2023
[x] Proposed
[x] Implementation: https://github.com/dotnet/roslyn/pull/56853
[x] Specification: this file.
The language today non-verbatim and verbatim interpolated strings ( $"" and $@""
respectively). The primary sensible  difference for these is that a non-verbatim
interpolated string works like a normal string and cannot contain newlines in its text
segments, and must instead use escapes (like \r\n). Conversely, a verbatim interpolated
string can contain newlines in its text segments (like a verbatim string), and doesn't
escape newlines or other character (except for "" to escape a quote itself).
This is all reasonable and will not change with this proposal.
What is unreasonable today is that we extend the restriction on 'no newlines' in a non-
verbatim interpolated string beyond its text segments into the interpolations  themselves.
This means, for example, that you cannot write the following:
c#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
var v = $"Count is\t: { this.Is.A.Really( long(expr)) 
                            .That.I.Should(  
                                be + able)[  
                                    to.Wrap()] } ."; Ultimately, the 'interpolation must be on a single line itself' rule is just a restriction of
the current implementation. That restriction really isn't necessary, and can be annoying,
and would be fairly trivial to remove (see work
https://github.com/dotnet/roslyn/pull/54875  to show how). In the end, all it does is
force the dev to place things on a single line, or force them into a verbatim interpolated
string (both of which may be unpalatable).
The interpolation expressions themselves are not text, and shouldn't be beholden to any
escaping/newline rules therin.
diff
https://github.com/dotnet/csharplang/blob/main/meetings/2021/LDM-2021-09-
20.md
Specification change
single_regular_balanced_text_character  
-    : '<Any character except / (U+002F), @ (U+0040), \" (U+0022), $  
(U+0024), ( (U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B), }  
(U+007D) and new_line_character>'
-    | '</ (U+002F), if not directly followed by / (U+002F) or * (U+002A)>'  
+    : <Any character except @ (U+0040), \" (U+0022), $ (U+0024), (  
(U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B), } (U+007D)>  
+    | comment  
    ; 
LDM Discussions
Utf8 Strings Literals
Article •09/30/2022
This proposal adds the ability to write UTF8 string literals in C# and have them
automatically encoded into their UTF-8 byte representation.
UTF8 is the language of the web and its use is necessary in significant portions of the
.NET stack. While much of data comes in the form of byte[] off the network stack there
is still significant uses of constants in the code. For example networking stack has to
commonly write constants like "HTTP/1.0\r\n", " AUTH" or . "Content-Length: ".
Today there is no efficient syntax for doing this as C# represents all strings using UTF16
encoding. That means developers have to choose between the convenience of encoding
at runtime which incurs overhead, including the time spent at startup actually
performing the encoding operation (and allocations if targeting a type that doesn't
actually require them), or manually translating the bytes and storing in a byte[].
c#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
// Efficient but verbose and error prone
static ReadOnlySpan< byte> AuthWithTrailingSpace => new byte[] { 0x41, 0x55, 
0x54, 0x48, 0x20 };
WriteBytes(AuthWithTrailingSpace);
// Incurs allocation and startup costs performing an encoding that could  
have been done at compile-timeThis trade off is a pain point that comes up frequently for our partners in the runtime,
ASP.NET and Azure. Often times it causes them to leave performance on the table
because they don't want to go through the hassle of writing out the byte[] encoding
by hand.
To fix this we will allow for UTF8 literals in the language and encode them into the UTF8
byte[] at compile time.
The language will provide the u8 suffix on string literals to force the type to be UTF8.
The suffix is case-insensitive, U8 suffix will be supported and will have the same
meaning as u8 suffix.
When the u8 suffix is used, the value of the literal is a ReadOnlySpan<byte> containing a
UTF-8 byte representation of the string. A null terminator is placed beyond the last byte
in memory (and outside the length of the ReadOnlySpan<byte>) in order to handle some
interop scenarios where the call expects null terminated strings.
c#
Since the literals would be allocated as global constants, the lifetime of the resulting
ReadOnlySpan<byte> would not prevent it from being returned or passed around to
elsewhere. However, certain contexts, most notably within async functions, do not allowstatic readonly  byte[] s_authWithTrailingSpace =  
Encoding.UTF8.GetBytes( "AUTH ");
WriteBytes(s_authWithTrailingSpace);
// Simplest / most convenient but terribly inefficient
WriteBytes(Encoding.UTF8.GetBytes( "AUTH "));
Detailed design
u8 suffix on string literals
string s1 = "hello"u8;             // Error
var s2 = "hello"u8;                // Okay and type is ReadOnlySpan<byte>
ReadOnlySpan< byte> s3 = "hello"u8; // Okay.
byte[] s4 = "hello"u8;             // Error - Cannot implicitly convert type  
'System.ReadOnlySpan<byte>' to 'byte[]'.
byte[] s5 = "hello"u8.ToArray();   // Okay.
Span<byte> s6 = "hello"u8;         // Error - Cannot implicitly convert type  
'System.ReadOnlySpan<byte>' to 'System.Span<byte>'.locals of ref struct types, so there would be a usage penalty in those situations, with a
ToArray() call or similar being required.
A u8 literal doesn't have a constant value. That is because ReadOnlySpan<byte> cannot
be type of a constant today. If the definition of const is expanded in the future to
consider ReadOnlySpan<byte>, then this value should also be considered a constant.
Practically though this means a u8 literal cannot be used as the default value of an
optional parameter.
c#
When the input text for the literal is a malformed UTF16 string, then the language will
emit an error:
c#
A new bullet point will be added to §11.9.5 Addition operator  as follows.
UTF8 byte representation concatenation:
C#
This binary + operator performs byte sequences concatenation and is applicable if
and only if both operands are semantically UTF8 byte representations. An operand
is semantically a UTF8 byte representation when it is eiher a value of a u8 literal, or
a value produced by the UTF8 byte representation concatenation operator.
The result of the UTF8 byte representation concatenation is a ReadOnlySpan<byte>
that consists of the bytes of the left operand followed by the bytes of the right
operand. A null terminator is placed beyond the last byte in memory (and outside// Error: The argument is not constant
void Write(ReadOnlySpan< byte> message = "missing" u8) { ... } 
var bytes = "hello \uD801\uD802" u8; // Error: the input string is not valid  
UTF16
Addition operator
ReadOnlySpan< byte> operator  +(ReadOnlySpan< byte> x, ReadOnlySpan< byte> 
y);the length of the ReadOnlySpan<byte>) in order to handle some interop scenarios
where the call expects null terminated strings.
The language will lower the UTF8 encoded strings exactly as if the developer had typed
the resulting byte[] literal in code. For example:
c#
That means all optimizations that apply to the new byte[] { ... } form will apply to
utf8 literals as well. This means the call site will be allocation free as C# will optimize this
be stored in the .data section of the PE file.
Multiple consecutive applications of UTF8 byte representation concatenation operators
are collapsed into a single creation of ReadOnlySpan<byte> with byte array containing the
final byte sequence.
c#Lowering
ReadOnlySpan< byte> span = "hello"u8;
// Equivalent to
ReadOnlySpan< byte> span = new ReadOnlySpan< byte>(new byte[] { 0x68, 0x65, 
0x6c, 0x6c, 0x6f, 0x00 }).
                               Slice(0,5); // The `Slice` call will be  
optimized away by the compiler.
ReadOnlySpan< byte> span = "h"u8 + "el"u8 + "lo"u8;
// Equivalent to
ReadOnlySpan< byte> span = new ReadOnlySpan< byte>(new byte[] { 0x68, 0x65, 
0x6c, 0x6c, 0x6f, 0x00 }).
                               Slice(0,5); // The `Slice` call will be  
optimized away by the compiler.
Drawbacks
Relying on core APIsThe compiler implementation will use UTF8Encoding for both invalid string detection as
well as translation to byte[]. The exact APIs will possibly depend on which target
framework the compiler is using. But UTF8Encoding will be the workhorse of the
implementation.
Historically the compiler has avoided using runtime APIs for literal processing. That is
because it takes control of how constants are processed away from the language and
into the runtime. Concretely it means items like bug fixes can change constant encoding
and mean that the outcome of C# compilation depends on which runtime the compiler
is executing on.
This is not a hypothetical problem. Early versions of R oslyn used double.Parse to handle
floating point constant parsing. That caused a number of problems. First it meant that
some floating point values had different representations between the native compiler
and R oslyn. Second as .NET core envolved and fixed long standing bugs in the
double.Parse code it meant that the meaning of those constants changed in the
language depending on what runtime the compiler executed on. As a result the
compiler ended up writing it's own version of floating point parsing code and removing
the dependency on double.Parse.
This scenario was discussed with the runtime team and we do not feel it has the same
problems we've hit before. The UTF8 parsing is stable across runtimes and there are no
known issues in this area that are areas for future compat concerns. If one does come up
we can re-evaluate the strategy.
The design could rely on target typing only and remove the u8 suffix on string literals.
In the majority of cases today the string literal is being assigned directly to a
ReadOnlySpan<byte> hence it's unnecessary.
c#
The u8 suffix exists primarily to support two scenarios: var and overload resolution. For
the latter consider the following use case:
c#Alternatives
Target type only
ReadOnlySpan< byte> span = "Hello World;"  Given the implementation it is better to call Write(ReadOnlySpan<byte>) and the u8
suffix makes this convenient: Write("hello"u8). Lacking that developers need to resort
to awkward casting Write((ReadOnlySpan<byte>)"hello").
Still this is a convenience item, the feature can exist without it and it is non-breaking to
add it at a later time.
While the .NET ecosystem is standardizing on ReadOnlySpan<byte> as the defacto Utf8
string type today it's possible the runtime will introduce an actual Utf8String type is the
future.
We should evaluate our design here in the face of this possible change and reflect on
whether we'd regret the decisions we've made. This should be weighed though against
the realistic probability we'll introduce Utf8String, a probability which seems to
decrease every day we find ReadOnlySpan<byte> as an acceptable alternative.
It seems unlikely that we would regret the target type conversion between string literals
and ReadOnlySpan<byte>. The use of ReadOnlySpan<byte> as utf8 is embedded in our
APIs now and hence there is still value in the conversion even if Utf8String comes along
and is a "better" type. The language could simply prefer conversions to Utf8String over
ReadOnlySpan<byte>.
It seems more likely that we'd regret the u8 suffix pointing to ReadOnlySpan<byte>
instead of Utf8String. It would be similar to how we regret that stackalloc int[] has a
natural type of int* instead of Span<int>. This is not a deal breaker though, just an
inconvenience.
The language will allow conversions between string constants and byte sequences
where the text is converted into the equivalent UTF8 byte representation. Specifically the
compiler will allow string_c onstant_t o_UTF8_b yte_representation_c onversion - implicitvoid Write(ReadOnlySpan< byte> span) { ... } 
void Write(string s) {
    var bytes = Encoding.Utf8.GetBytes(s);
    Write(bytes.AsSpan());
}
Wait for Utf8String type
Conversions between string constants and byte
sequencesconversions from string constants to byte[], Span<byte>, and ReadOnlySpan<byte>. A
new bullet point will be added to the implicit conversions §10.2  section. This
conversion is not a standard conversion §10.4 .
c#
When the input text for the conversion is a malformed UTF16 string then the language
will emit an error:
c#
The predominant usage of this feature is expected to be with literals but it will work with
any string constant value. A conversion from a string constant with null value will be
supprted as well. The result of the conversion will be default value of the target type.
c#
In the case of any constant operation on strings, such as +, the encoding to UTF8 will
occur on the final string vs. happening for the individual parts and then concatenating
the results. This ordering is important to consider because it can impact whether or not
the conversion succeeds.
c#
The two parts here are invalid on their own as they are incomplete portions of a
surrogate pair. Individually there is no correct translation to UTF8 but together they
form a complete surrogate pair that can be successfully translated to UTF8.
byte[] array = "hello";             // new byte[] { 0x68, 0x65, 0x6c, 0x6c,  
0x6f }
Span<byte> span = "dog";            // new byte[] { 0x64, 0x6f, 0x67 }
ReadOnlySpan< byte> span = "cat";    // new byte[] { 0x63, 0x61, 0x74 }
const string text = "hello \uD801\uD802" ;
byte[] bytes = text; // Error: the input string is not valid UTF16
const string data = "dog"
ReadOnlySpan< byte> span = data;     // new byte[] { 0x64, 0x6f, 0x67 }
const string first = "\uD83D" ;  // high surrogate
const string second = "\uDE00" ; // low surrogate
ReadOnlySpan< byte> span = first + second;The string_c onstant_t o_UTF8_b yte_representation_c onversion is not allowed in Linq
Expression T rees.
While the inputs to these conversions are constants and the data is fully encoded at
compile time, the conversion is not considered constant by the language. That is
because arrays are not constant today. If the definition of const is expanded in the
future to consider arrays then these conversions should also be considered. Practically
though this means a result of these conversions cannot be used as the default value of
an optional parameter.
c#
Once implemented string literals will have the same problem that other literals have in
the language: what type they represent depends on how they are used. C# provides a
literal suffix to disambiguate the meaning for other literals. For example developers can
write 3.14f to force the value to be a float or 1l to force the value to be a long.
Whether this conversion is supported and, if so, how it is performed is not specified.
Proposal:
Allow implicit conversions from a string constant with null value to byte[],
Span<byte>, and ReadOnlySpan<byte>. The result of the conversion is default value of
the target type.
Resolution:
The proposal is approved -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md#conversions-from-null-literals .// Error: The argument is not constant
void Write(ReadOnlySpan< byte> message = "missing" ) { ... } 
Unresolved questions
(Resolved) Conversions between a string constant with
null value and byte sequences
(Resolved) Where does
string_constant_to_UTF8_byte_representation_conversionIs string_c onstant_t o_UTF8_b yte_representation_c onversion a bullet point in the implicit
conversions §10.2  section on its own, or is it part of §10.2.11 , or does it belong to
some other existing implicit conversions group?
Proposal:
It is a new bullet point in implicit conversions §10.2 , similar to "Implicit interpolated
string conversions" or "Method group conversions". It doesn't feel like it belongs to
"Implicit constant expression conversions" because, even though the source is a
constant expression, the result is never a constant expression. Also, "Implicit constant
expression conversions" are considered to be "S tandard implicit conversions" §10.4.2 ,
which is likely to lead to non-trivial behavior changes involving user-defined
conversions.
Resolution:
We will introduce a new conversion kind for string constant to UTF-8 bytes -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md#conversion-kinds
In addition to "pure" S tandard Conversions (the standard conversions are those pre-
defined conversions that can occur as part of a user-defined conversion), compiler also
treats some predefined conversions as "somewhat" standard. For example, an implicit
interpolated string conversion can occur as part of a user-defined conversion if there is
an explicit cast to the target type in code. As if it is a S tandard Explicit Conversion, even
though it is an implicit conversion not explicitly included into the set of standard implicit
or explicit conversions. For example:
C#belong?
(Resolved) Is
string_constant_to_UTF8_byte_representation_conversion a
standard conversion
class C
{
    static void Main()
    {
        C1 x = $"hello" ; // error CS0266: Cannot implicitly convert type  
'string' to 'C1'. An explicit conversion exists (are you missing a cast?)
        var y = (C1) $"dog"; // works
    }Proposal:
The new conversion is not a standard conversion. This will avoid non-trivial behavior
changes involving user-defined conversions. For example, we won't need to worry about
user-defined cinversions under implicit tuple literal conversions, etc.
Resolution:
Not a standard conversion, for now -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md#implicit-standard-conversion .
Should string_c onstant_t o_UTF8_b yte_representation_c onversion be allowed in context of
a Linq Expression T ree conversion? W e can disallow it for now, or we could simply
include the "lowered" form into the tree. For example:
C#
What about string literals with u8 suffix? W e could surface those as byte array creations:
C#
Resolution:
Disallow in Linq Expression T rees -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-}
class C1
{
    public static implicit  operator  C1(System.FormattableString x ) => new 
C1();
}
(Resolved) Linq Expression Tree conversion
Expression<Func< byte[]>> x = () => "hello";           // () => new [] {104,  
101, 108, 108, 111}
Expression<FuncSpanOfByte> y = () => "dog";           // () => new  
Span`1(new [] {100, 111, 103}) 
Expression<FuncReadOnlySpanOfByte> z = () => "cat";   // () => new  
ReadOnlySpan`1(new [] {99, 97, 116})
Expression<Func< byte[]>> x = () => "hello"u8;           // () => new []  
{104, 101, 108, 108, 111}26.md#expression-tree-representation .
The "Detailed design" section says: "The natural type though will be
ReadOnlySpan<byte>." At the same time: "When the u8 suffix is used the literal can still
be converted to any of the allowed types: byte[], Span<byte> or ReadOnlySpan<byte>."
There are several disadvantages with this approach:
ReadOnlySpan<byte> is not available on desktop framework;
There are no existing conversions from ReadOnlySpan<byte> to byte[] or
Span<byte>. In order to support them we will likely need to treat the literals as
target typed. Both the language rules and implementation will become more
complicated.
Proposal:
The natural type will be byte[]. It is readily available on all frameworks. B TW, at runtime
we will always be starting with creating a byte array, even with the original proposal. W e
also don't need any special conversion rules to support conversions to Span<byte> and
ReadOnlySpan<byte>. There are already implicit user-defined conversions from byte[] to
Span<byte> and ReadOnlySpan<byte>. There is even implicit user-defined conversion to
ReadOnlyMemory<byte> (see the "Depth of the conversion" question below). There is a
disadvantage, language doesn't allow chaining user-defined conversions. So, the
following code will not compile:
C#
(Resolved) The natural type of a string literal with u8
suffix
using System;
class C
{
    static void Main()
    {
        var y = (C2) "dog"u8; // error CS0030: Cannot convert type 'byte[]'  
to 'C2'
        var z = (C3) "cat"u8; // error CS0030: Cannot convert type 'byte[]'  
to 'C3'
    }
}
class C2
{
    public static implicit  operator  C2(Span<byte> x) => new C2();However, as with any user-defined conversion, an explicit cast can be used to make one
user-defined conversion a part of another user-defined conversion.
It feels like all motivating scenarios are going to be addressed with byte[] as the
natural type, but the language rules and implementation will be significantly simpler.
Resolution:
The proposal is approved -
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md#natural-type-of-u8-literals . We will likely want to have a deeper debate about
whether u8 string literals should have a type of a mutable array, but we don't think that
debate is necessary for now.
Will it also work anywhere that a byte[] could work? Consider:
c#
The first example likely should work because of the natural type that comes from u8.
The second example is hard to make work because it requires conversions in both
directions. That is unless we add ReadOnlyMemory<byte> as one of the allowed conversion
types.
Proposal:
Don't do anything special.
Resolution:
No new conversion targets added for now
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md#conversion-depth .}
class C3
{
    public static explicit  operator  C3(ReadOnlySpan< byte> x) => new C3();
}
(Resolved) Depth of the conversion
static readonly  ReadOnlyMemory< byte> s_data1 = "Data"u8;
static readonly  ReadOnlyMemory< byte> s_data2 = "Data";
The following API would become ambiguous:
c#
What should we do to address this?
Proposal:
Similar to https://github.com/dotnet/csharplang/blob/main/proposals/csharp-
10.0/lambda-improvements.md#overload-resolution , Better function member
(§11.6.4.3 ) is updated to prefer members where none of the conversions involved
require converting string constants to UTF8 byte sequences.
Better function member
... Given an argument list A with a set of argument expressions {E1, E2, ..., En}
and two applicable function members Mp and Mq with parameter types {P1, P2,
..., Pn} and {Q1, Q2, ..., Qn}, Mp is defined to be a better function member
than Mq if
1. for each ar gument, the implicit conv ersion fr om Ex to Px is not a
string_c onstant_t o_UTF8_b yte_representation_c onversion, and for at least one
argument, the implicit conv ersion fr om Ex to Qx is a
string_c onstant_t o_UTF8_b yte_representation_c onversion, or
2. for each argument, the implicit conversion from Ex to Px is not a
function_type_c onversion, and
Mp is a non-generic method or Mp is a generic method with type
parameters {X1, X2, ..., Xp} and for each type parameter Xi the type
argument is inferred from an expression or from a type other than a
function_type , and
for at least one argument, the implicit conversion from Ex to Qx is a
function_type_c onversion, or Mq is a generic method with type parameters
{Y1, Y2, ..., Yq} and for at least one type parameter Yi the type
argument is inferred from a function_type , or(Resolved) Overload resolution breaks
M("");
static void M1(ReadOnlySpan< char> charArray ) => ...;
static void M1(byte[] byteArray ) => ...;
3. for each argument, the implicit conversion from Ex to Qx is not better than
the implicit conversion from Ex to Px, and for at least one argument, the
conversion from Ex to Px is better than the conversion from Ex to Qx.
Note that the addition of this rule is not going to cover scenarios with instance methods
becoming applicable and "shadowing" extension methods. For example:
C#
Behavior of this code will silently change from printing "string" to printing "byte[]".
Are we Ok with this behavior change? Should it be documented as a breaking change?
Note that there is no proposal to make
string_c onstant_t o_UTF8_b yte_representation_c onversion unavailable when C#10
language version is targeted. In that case, the example above becomes an error rather
than returns to C#10 behavior. This follows a general principle that target language
version doesn't affect semantics of the language.
Are we Ok with this behavior? Should it be documented as a breaking change?
The new rule also is not going to prevent breaks involving tuple litearal conversions. For
example,
C#using System;
class Program
{
    static void Main()
    {
        var p = new Program();
        Console.WriteLine(p.M( ""));
    }
    public string M(byte[] b) => "byte[]" ;
}
static class E
{
    public static string M(this object o, string s) => "string" ;
}
class C
{
    static void Main()
    {is going to silently print "array" instead of "object".
Are we Ok with this behavior? Should it be documented as a breaking change? P erhaps
we could complicate the new rule to dig into the tuple literal conversions.
Resolution:
The prototype will not adjust any rules here, so we can hopefully see what breaks in
practice - https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-
01-26.md#breaking-changes .
Proposal:
Support U8 suffix as well for consistency with numeric suffixes.
Resolution:
Approved - https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-
2022-01-26.md#suffix-case-sensitivity .
Examples of where runtime has manually encoded the UTF8 bytes today
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/Common/src/S ystem/Net/Http/aspnetcore/Http2/Hpack/S tat
usCodes.cs#L13-L78
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Memory/src/S ystem/Buffers/T ext/Base64Encoder.cs#L
581-L591
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.HttpListener/src/S ystem/Net/Windows/HttpR espo
nseStream.Windows.cs#L284
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Http/src/S ystem/Net/Http/SocketsHttpHandler/Ht        System.Console.Write(Test(( "s", 1)));
    }
    static string Test((object, int) a) => "object" ;
    static string Test((byte[], int) a) => "array";
}
(Resolved) Should u8 suffix be case-insensitive?
Examples today
tp2Stream.cs#L30
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Http/src/S ystem/Net/Http/SocketsHttpHandler/Ht
tp3RequestS tream.cs#L852
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.T ext.Json/src/S ystem/T ext/Json/JsonConstants.cs#L35-
L42
Examples where we leave perf on the table
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Security/src/S ystem/Net/Security/P al.Managed/Sa
feChannelBindingHandle.cs#L16-L17
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Http/src/S ystem/Net/Http/SocketsHttpHandler/Ht
tpConnection.cs#L37-L43
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Http/src/S ystem/Net/Http/SocketsHttpHandler/Ht
tp2Connection.cs#L78
https://github.com/dotnet/runtime/blob/e095fde94baa480a6d65dfdee43d9cc0ad
0d0b38/src/libraries/S ystem.Net.Mail/src/S ystem/Net/Mail/SmtpCommands.cs#L6
69-L687
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-01-
26.md  https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-
04-18.md  https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-
2022-06-06.md
Design meetings
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackPattern match Span<char> on a constant
string
Article •06/23/2023
Permit pattern matching a Span<char> and a ReadOnlySpan<char> on a constant string.
For perfomance, usage of Span<char> and ReadOnlySpan<char> is preferred over string in
many scenarios. The framework has added many new APIs to allow you to use
ReadOnlySpan<char> in place of a string.
A common operation on strings is to use a switch to test if it is a particular value, and
the compiler optimizes such a switch. However there is currently no way to do the same
on a ReadOnlySpan<char> efficiently, other than implementing the switch and the
optimization manually.
In order to encourage adoption of ReadOnlySpan<char> we allow pattern matching a
ReadOnlySpan<char>, on a constant string, thus also allowing it to be used in a switch.
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
static bool Is123(ReadOnlySpan< char> s) 
{ 
    return s is "123"; 
} We alter the spec for constant patterns as follows (the proposed addition is shown in
bold):
A constant pattern tests the value of an expression against a constant value. The
constant may be any constant expression, such as a literal, the name of a declared
const variable, or an enumeration constant, or a typeof expression etc.
If both e and c are of integral types, the pattern is considered matched if the result
of the expression e == c is true.
If e is of type System.Span<char> or System.ReadOnlySpan<char>, and c is a constant
string, and c does not hav e a constant v alue o f null, then the p attern is
consider ed mat ching if System.MemoryExtensions.SequenceEqual<char>(e,
System.MemoryExtensions.AsSpan(c)) returns true.
Otherwise the pattern is considered matching if object.Equals(e, c) returns true.
In this case it is a compile-time error if the static type of e is not pattern compatible
with the type of the constant.
System.Span<T> and System.ReadOnlySpan<T> are matched by name, must be ref
structs, and can be defined outside corlib.
System.MemoryExtensions is matched by name and can be defined outside corlib.
The signature of System.MemoryExtensions.SequenceEqual overloads must match:
public static bool SequenceEqual<T>(System.Span<T>, System.ReadOnlySpan<T>)
public static bool SequenceEqual<T>(System.ReadOnlySpan<T>,
System.ReadOnlySpan<T>)
The signature of System.MemoryExtensions.AsSpan must match:
public static System.ReadOnlySpan<char> AsSpan(string)static bool IsABC(Span<char> s) 
{ 
    return s switch { "ABC" => true, _ => false }; 
} 
Detailed design
Well-known membersMethods with optional parameters are excluded from consideration.
None
None
1. Should matching be defined independently from
MemoryExtensions.SequenceEqual() etc.?
... the pattern is considered matching if e.Length == c.Length and e[i] ==
c[i] for all characters in e.
Recommendation: Def ine in t erms of MemoryExtensions.SequenceEqual() for
performanc e. If MemoryExtensions is missing, r eport compile err or.
2. Should matching against (string)null be allowed?
If so, should (string)null subsume "" since MemoryExtensions.AsSpan(null) ==
MemoryExtensions.AsSpan("")?
C#
Recommendation: C onstant p attern (string)null should be r eported as an err or.
3. Should the constant pattern match include a runtime type test of the expression
value for Span<char> or ReadOnlySpan<char>?Drawbacks
Alternatives
Unresolved questions
static bool IsEmpty(ReadOnlySpan< char> span) 
{ 
    return span switch 
    { 
        ( string)null => true, // ok? 
        "" => true,           // error: unreachable?  
        _ => false, 
    }; 
} C#
Recommendation: No implicit r untime type t est for c onstant p attern. (IsABC<T>()
example is allo wed becaus e the type t est is explicit.)
4. Should subsumption consider constant string patterns, list patterns, and Length
property pattern?
C#
Recommendation: Same subsumption behavior as us ed when the expr ession v alue is
string. (Does that mean no subsumption betw een c onstant str ings, list p atterns, and
Length, other than tr eating [..] as mat ching an y?)
https://github.com/dotnet/csharplang/blob/master/meetings/2020/LDM-2020-10-
07.md#readonlyspanchar-patternsstatic bool Is123<T>(Span<T> s)  
{ 
    return s is "123"; // test for Span<char>?  
} 
static bool IsABC<T>(Span<T> s)  
{ 
    return s is Span<char> and "ABC"; // ok? 
} 
static bool IsEmptyString<T>(T t) where T : ref struct 
{ 
    return t is ""; // test for ReadOnlySpan<char>, Span<char>, string?  
} 
static int ToNum(ReadOnlySpan< char> s) 
{ 
    return s switch 
    { 
        { Length: 0 } => 0, 
        "" => 1,        // error: unreachable?  
        [ 'A',..] => 2, 
        "ABC" => 3,     // error: unreachable?  
        _ => 4, 
    }; 
} 
Design meetings
List patterns
Article •06/23/2023
Lets you to match an array or a list with a sequence of patterns e.g. array is [1, 2, 3]
will match an integer array of the length three with 1, 2, 3 as its elements, respectively.
The pattern syntax is modified as follow:
antlr７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Detailed design
list_pattern_clause  
  : '[' (pattern ( ',' pattern)* ','?)? ']' 
  ; 
list_pattern  
  : list_pattern_clause simple_designation?  
  ; 
slice_pattern  
  : '..' pattern?  
  ; 
primary_pattern  
  : list_pattern  
  | slice_pattern  
  | // all of the pattern forms previously defined  
  ; There are two new patterns:
The list_p attern is used to match elements.
A slice_pattern is only permitted once and only directly in a list_p attern_claus e and
discards zero or mor e elements.
A list_p attern is compatible with any type that is countable as well as index able — it has
an accessible indexer that takes an Index as an argument or otherwise an accessible
indexer with a single int parameter. If both indexers are present, the former is
preferred.
A slice_pattern with a subpattern is compatible with any type that is countable as well as
sliceable  — it has an accessible indexer that takes a Range as an argument or otherwise
an accessible Slice method with two int parameters. If both are present, the former is
preferred.
A slice_pattern without a subpattern is compatible with any type that is compatible with
a list_p attern.
This set of rules is derived from the range index er pattern.
Subsumption checking works just like positional patterns with ITuple  - corresponding
subpatterns are matched by position plus an additional node for testing length.
For example, the following code produces an error because both patterns yield the
same D AG:
C#
Unlike:
C#Pattern compatibility
Subsumption checking
case [_, .., 1]: // expr.Length is >= 2 && expr[^1] is 1
case [.., _, 1]: // expr.Length is >= 2 && expr[^1] is 1
case [_, 1, ..]: // expr.Length is >= 2 && expr[1] is 1  
case [.., 1, _]: // expr.Length is >= 2 && expr[^2] is 1The order in which subpatterns are matched at runtime is unspecified, and a failed
match may not attempt to match all subpatterns.
Given a specific length, it's possible that two subpatterns refer to the same element, in
which case a test for this value is inserted into the decision D AG.
For instance, [_, >0, ..] or [.., <=0, _] becomes length >= 2 && ([1] > 0 ||
length == 3 || [^2] <= 0) where the length value of 3 implies the other test.
Conversely, [_, >0, ..] and [.., <=0, _] becomes length >= 2 && [1] > 0 &&
length != 3 && [^2] <= 0 where the length value of 3 disallows the other test.
As a result, an error is produced for something like case [.., p]: case [p]: because at
runtime, we're matching the same element in the second case.
If a slice subpattern matches a list or a length value, subpatterns are treated as if they
were a direct subpattern of the containing list. For instance, [..[1, 2, 3]] subsumes a
pattern of the form [1, 2, 3].
The following assumptions are made on the members being used:
The property that makes the type countable is assumed to always return a non-
negative value, if and only if the type is index able. For instance, the pattern {
Length: -1 } can never match an array.
The member that makes the type sliceable  is assumed to be well-behaved, that is,
the return value is never null and that it is a proper subslice of the containing list.
The behavior of a pattern-matching operation is undefined if any of the above
assumptions doesn't hold.
A pattern of the form expr is [1, 2, 3] is equivalent to the following code:
C#
A slice_pattern acts like a proper discard i.e. no tests will be emitted for such pattern,
rather it only affects other nodes, namely the length and indexer. For instance, a patternLowering
expr.Length is 3 
&& expr[ new Index(0, fromEnd: false)] is 1 
&& expr[ new Index(1, fromEnd: false)] is 2 
&& expr[ new Index(2, fromEnd: false)] is 3 of the form expr is [1, .. var s, 3] is equivalent to the following code (if compatible
via explicit Index and Range support):
C#
The input type  for the slice_pattern is the return type of the underlying this[Range] or
Slice method with two exceptions: For string and arrays, string.Substring and
RuntimeHelpers.GetSubArray will be used, respectively.
1. Should we support multi-dimensional arrays? (answer [LDM 2021-05-26]: Not
supported. If we want to make a general MD-array focused release, we would want
to revisit all the areas they're currently lacking, not just list patterns.)
2. Should we accept a general pattern following .. in a slice_pattern? (answer [LDM
2021-05-26]: Y es, any pattern is allowed after a slice.)
3. By this definition, the pattern [..] tests for expr.Length >= 0. Should we omit
such test, assuming Length is always non-negative? (answer [LDM 2021-05-26]:
[..] will not emit a Length check)expr.Length is >= 2 
&& expr[ new Index(0, fromEnd: false)] is 1 
&& expr[ new Range(new Index(1, fromEnd: false), new Index(1, fromEnd:  
true))] is var s 
&& expr[ new Index(1, fromEnd: true)] is 3 
Unresolved questionsRequired Members
Article •03/17/2023
This proposal adds a way of specifying that a property or field is required to be set
during object initialization, forcing the instance creator to provide an initial value for the
member in an object initializer at the creation site.
Object hierarchies today require a lot of boilerplate to carry data across all levels of the
hierarchy. Let's look at a simple hierarchy involving a Person as might be defined in C#
8:
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
class Person 
{ 
    public string FirstName { get; } 
    public string MiddleName { get; } 
    public string LastName { get; } 
    public Person(string firstName, string lastName, string? middleName =  
null) 
    { 
        FirstName = firstName;  
        LastName = lastName;  
        MiddleName = middleName ?? string.Empty; 
    } 
} There's lots of repetition going on here:
1. At the root of the hierarchy, the type of each property had to be repeated twice,
and the name had to be repeated four times.
2. At the derived level, the type of each inherited property had to be repeated once,
and the name had to be repeated twice.
This is a simple hierarchy with 3 properties and 1 level of inheritance, but many real-
world examples of these types of hierarchies go many levels deeper, accumulating larger
and larger numbers of properties to pass along as they do so. R oslyn is one such
codebase, for example, in the various tree types that make our CST s and AST s. This
nesting is tedious enough that we have code generators to generate the constructors
and definitions of these types, and many customers take similar approaches to the
problem. C# 9 introduces records, which for some scenarios can make this better:
C#
records eliminate the first source of duplication, but the second source of duplication
remains unchanged: unfortunately, this is the source of duplication that grows as the
hierarchy grows, and is the most painful part of the duplication to fix up after making a
change in the hierarchy as it required chasing the hierarchy through all of its locations,
possibly even across projects and potentially breaking consumers.
As a workaround to avoid this duplication, we have long seen consumers embracing
object initializers as a way of avoiding writing constructors. Prior to C# 9, however, this
had 2 major downsides:
1. The object hierarchy has to be fully mutable, with set accessors on every property.
2. There is no way to ensure that every instantation of an object from the graph sets
every member.class Student : Person 
{ 
    public int ID { get; } 
    public Student(int id, string firstName, string lastName, string? 
middleName = null) 
        : base(firstName, lastName, middleName ) 
    { 
        ID = id;  
    } 
} 
record Person(string FirstName, string LastName, string MiddleName = ""); 
record Student(int ID, string FirstName, string LastName, string MiddleName  
= "") : Person(FirstName, LastName, MiddleName ); C# 9 again addressed the first issue here, by introducing the init accessor: with it,
these properties can be set on object creation/initialization, but not subsequently.
However, we again still have the second issue: properties in C# have been optional since
C# 1.0. Nullable reference types, introduced in C# 8.0, addressed part of this issue: if a
constructor does not initialize a non-nullable reference-type property, then the user is
warned about it. However, this doesn't solve the problem: the user here wants to not
repeat large parts of their type in the constructor, they want to pass the requir ement  to
set properties on to their consumers. It also doesn't provide any warnings about ID
from Student, as that is a value type. These scenarios are extremely common in
database model ORMs, such as EF Core, which need to have a public parameterless
constructor but then drive nullability of the rows based on the nullability of the
properties.
This proposal seeks to address these concerns by introducing a new feature to C#:
required members. R equired members will be required to be initialized by consumers,
rather than by the type author, with various customizations to allow flexibility for
multiple constructors and other scenarios.
class, struct, and record types gain the ability to declare a requir ed_member_list . This
list is the list of all the properties and fields of a type that are considered requir ed, and
must be initialized during the construction and initialization of an instance of the type.
Types inherit these lists from their base types automatically, providing a seamless
experience that removes boilerplate and repetitive code.
We add 'required' to the list of modifiers in field_modi fier and property_modi fier. The
requir ed_member_list  of a type is composed of all the members that have had required
applied to them. Thus, the Person type from earlier now looks like this:
C#Detailed Design
required modifier
public class Person 
{ 
    // The default constructor requires that FirstName and LastName be set  
at construction time  
    public required string FirstName { get; init; } 
    public string MiddleName { get; init; } = ""; 
    public required string LastName { get; init; } 
} All constructors on a type that has a requir ed_member_list  automatically advertise a
contract that consumers of the type must initialize all of the properties in the list. It is an
error for a constructor to advertise a contract that requires a member that is not at least
as accessible as the constructor itself. For example:
C#
required is only valid in class, struct, and record types. It is not valid in interface
types. required cannot be combined with the following modifiers:
fixed
ref readonly
ref
const
static
required is not allowed to be applied to indexers.
The compiler will issue a warning when Obsolete is applied to a required member of a
type and:
1. The type is not marked Obsolete, or
2. Any constructor not attributed with SetsRequiredMembersAttribute is not marked
Obsolete.
All constructors in a type with required members, or whose base type specifies required
members, must have those members set by a consumer when that constructor is called.
In order to exempt constructors from this requirement, a constructor can be attributedpublic class C 
{ 
    public required int Prop { get; protected  init; } 
    // Advertises that Prop is required. This is fine, because the  
constructor is just as accessible as the property initer.  
    protected  C() {} 
    // Error: ctor C(object) is more accessible than required property  
Prop.init.  
    public C(object otherArg ) {} 
} 
SetsRequiredMembersAttributewith SetsRequiredMembersAttribute, which removes these requirements. The constructor
body is not validated to ensure that it definitely sets the required members of the type.
SetsRequiredMembersAttribute removes all requirements from a constructor, and those
requirements are not checked for validity in any way. NB: this is the escape hatch if
inheriting from a type with an invalid required members list is necessary: mark the
constructor of that type with SetsRequiredMembersAttribute, and no errors will be
reported.
If a constructor C chains to a base or this constructor that is attributed with
SetsRequiredMembersAttribute, C must also be attributed with
SetsRequiredMembersAttribute.
For record types, we will emit SetsRequiredMembersAttribute on the synthesized copy
constructor of a record if the record type or any of its base types have required
members.
NB: An earlier version of this proposal had a larger metalanguage around initialization,
allowing adding and removing individual required members from a constructor, as well
as validation that the constructor was setting all required members. This was deemed
too complex for the initial release, and removed. W e can look at adding more complex
contracts and modifications as a later feature.
For every constructor Ci in type T with required members R, consumers calling Ci
must do one of:
Set all members of R in an object_initializer  on the object_cr eation_expr ession ,
Or set all members of R via the named_ar gument_list  section of an attribute_target.
unless Ci is attributed with SetsRequiredMembers.
If the current context does not permit an object_initializer  or is not an attribute_target,
and Ci is not attributed with SetsRequiredMembers, then it is an error to call Ci.
A type with a parameterless constructor that advertises a contract is not allowed to be
substituted for a type parameter constrained to new(), as there is no way for the generic
instantiation to ensure that the requirements are satisfied.Enforcement
new() constraintRequired members are not enforced on instances of struct types created with default
or default(StructType). They are enforced for struct instances created with new
StructType(), even when StructType has no parameterless constructor and the default
struct constructor is used.
It is an error to mark a member required if the member cannot be set in any context
where the containing type is visible.
If the member is a field, it cannot be readonly.
If the member is a property, it must have a setter or initer at least as accessible as
the member's containing type.
This means the following cases are not allowed:
C#struct defaults
Accessibility
interface  I 
{ 
    int Prop1 { get; } 
} 
public class Base 
{ 
    public virtual int Prop2 { get; set; } 
    protected  required int _field; // Error: _field is not at least as  
visible as Base. Open question below about the protected constructor  
scenario  
    public required readonly  int _field2; // Error: required fields cannot  
be readonly  
    protected  Base() { } 
    protected  class Inner 
    { 
        protected  required int PropInner { get; set; } // Error: PropInner  
cannot be set inside Base or Derived  
    } 
} 
public class Derived : Base, I 
{ 
    required int I.Prop1 { get; } // Error: explicit interface implementions  
cannot be required as they cannot be set in an object initializer  
    public required override  int Prop2 { get; set; } // Error: this property  
is hidden by Derived.Prop2 and cannot be set in an object initializer  It is an error to hide a required member, as that member can no longer be set by a
consumer.
When overriding a required member, the required keyword must be included on the
method signature. This is done so that if we ever want to allow unrequiring a property
with an override in the future, we have design space to do so.
Overrides are allowed to mark a member required where it was not required in the
base type. A member so-marked is added to the required members list of the derived
type.
Types are allowed to override required virtual properties. This means that if the base
virtual property has storage, and the derived type tries to access the base
implementation of that property, they could observe uninitialized storage. NB: This is a
general C# anti-pattern, and we don't think that this proposal should attempt to address
it.
Members that are marked required are not required to be initialized to a valid nullable
state at the end of a constructor. All required members from this type and any base
types are considered by nullable analysis to be default at the beginning of any
constructor in that type, unless chaining to a this or base constructor that is attributed
with SetsRequiredMembersAttribute.
Nullable analysis will warn about all required members from the current and base types
that do not have a valid nullable state at the end of a constructor attributed with
SetsRequiredMembersAttribute.
C#    public new int Prop2 { get; } 
    public required int Prop3 { get; } // Error: Required member must have a  
setter or initer  
    public required int Prop4 { get; internal  set; } // Error: Required  
member setter must be at least as visible as the constructor of Derived  
} 
Effect on nullable analysis
#nullable enable  
public class Base 
{ 
    public required string Prop1 { get; set; } The following 2 attributes are known to the C# compiler and required for this feature to
function:
C#    public Base() {} 
    [SetsRequiredMembers ] 
    public Base(int unused) { Prop1 = ""; } 
} 
public class Derived : Base 
{ 
    public required string Prop2 { get; set; } 
    [SetsRequiredMembers ] 
    public Derived() : base() 
    { 
    } // Warning: Prop1 and Prop2 are possibly null.  
    [SetsRequiredMembers ] 
    public Derived(int unused) : base() 
    { 
        Prop1.ToString(); // Warning: possibly null dereference  
        Prop2.ToString(); // Warning: possibly null dereference  
    } 
    [SetsRequiredMembers ] 
    public Derived(int unused, int unused2 ) : this() 
    { 
        Prop1.ToString(); // Ok 
        Prop2.ToString(); // Ok 
    } 
    [SetsRequiredMembers ] 
    public Derived(int unused1, int unused2, int unused3 ) : base(unused1) 
    { 
        Prop1.ToString(); // Ok 
        Prop2.ToString(); // Warning: possibly null dereference  
    } 
} 
Metadata Representation
namespace  System.Runtime.CompilerServices  
{ 
    [AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct |  
AttributeTargets.Field | AttributeTargets.Property, AllowMultiple = false,  
Inherited = false) ] 
    public sealed class RequiredMemberAttribute  : Attribute  
    { 
        public RequiredMemberAttribute () {} 
    } It is an error to manually apply RequiredMemberAttribute to a type.
Any member that is marked required has a RequiredMemberAttribute applied to it. In
addition, any type that defines such members is marked with RequiredMemberAttribute,
as a marker to indicate that there are required members in this type. Note that if type B
derives from A, and A defines required members but B does not add any new or
override any existing required members, B will not be marked with a
RequiredMemberAttribute. To fully determine whether there are any required members in
B, checking the full inheritance hierarchy is necessary.
Any constructor in a type with required members that does not have
SetsRequiredMembersAttribute applied to it is marked with two attributes:
1. System.Runtime.CompilerServices.CompilerFeatureRequiredAttribute with the
feature name "RequiredMembers".
2. System.ObsoleteAttribute with the string "Types with required members are not
supported in this version of your compiler", and the attribute is marked as an
error, to prevent any older compilers from using these constructors.
We don't use a modreq here because it is a goal to maintain binary compat: if the last
required property was removed from a type, the compiler would no longer synthesize
this modreq, which is a binary-breaking change and all consumers would need to be
recompiled. A compiler that understands required members will ignore this obsolete
attribute. Note that members can come from base types as well: even if there are no
new required members in the current type, if any base type has required members, this
Obsolete attribute will be generated. If the constructor already has an Obsolete
attribute, no additional Obsolete attribute will be generated.
We use both ObsoleteAttribute and CompilerFeatureRequiredAttribute because the
latter is new this release, and older compilers don't understand it. In the future, we may} 
namespace  System.Diagnostics.CodeAnalysis  
{ 
    [AttributeUsage(AttributeTargets.Constructor, AllowMultiple = false,  
Inherited = false) ] 
    public sealed class SetsRequiredMembersAttribute  : Attribute  
    { 
        public SetsRequiredMembersAttribute () {} 
    } 
} be able to drop the ObsoleteAttribute and/or not use it to protect new features, but for
now we need both for full protection.
To build the full list of required members R for a given type T, including all base types,
the following algorithm is run:
1. For every Tb, starting with T and working through the base type chain until
object is reached.
2. If Tb is marked with RequiredMemberAttribute, then all members of Tb marked
with RequiredMemberAttribute are gathered into Rb
a. For every Ri in Rb, if Ri is overridden by any member of R, it is skipped.
b. Otherwise, if any Ri is hidden by a member of R, then the lookup of required
members fails and no further steps are taken. Calling any constructor of T not
attributed with SetsRequiredMembers issues an error.
c. Otherwise, Ri is added to R.
What will the enforcement mechanisms for nested member initializers be? Will they be
disallowed entirely?
C#Open Questions
Nested member initializers
class Range 
{ 
    public required Location Start { get; init; } 
    public required Location End { get; init; } 
} 
class Location  
{ 
    public required int Column { get; init; } 
    public required int Line { get; init; } 
} 
_ = new Range { Start = { Column = 0, Line = 0 }, End = { Column = 1, Line =  
0 } } // Would this be allowed if Location is a struct type?  
_ = new Range { Start = new Location { Column = 0, Line = 0 }, End = new 
Location { Column = 1, Line = 0 } } // Or would this form be necessary  
instead?  Do we strictly enforce that members specified in a init clause without an initializer
must initialize all members? It seems likely that we do, otherwise we create an easy pit-
of-failure. However, we also run the risk of reintroducing the same problems we solved
with MemberNotNull in C# 9. If we want to strictly enforce this, we will likely need a way
for a helper method to indicate that it sets a member. Some possible syntaxes we've
discussed for this:
Allow init methods. These methods are only allowed to be called from a
constructor or from another init method, and can access this as if it's in the
constructor (ie, set readonly and init fields/properties). This can be combined
with init clauses on such methods. A init clause would be considered satisfied if
the member in the clause is definitely assigned in the body of the
method/constructor. Calling a method with a init clause that includes a member
counts as assigning to that member. If we do decided that this is a route we want
to pursue, now or in the future, it seems likely that we should not use init as the
keyword for the init clause on a constructor, as that would be confusing.
Allow the ! operator to suppress the warning/error explicitly. If initializing a
member in a complicated way (such as in a shared method), the user can add a !
to the init clause to indicate the compiler should not check for initialization.
Conclusion : After discussion we like the idea of the ! operator. It allows the user to be
intentional about more complicated scenarios while also not creating a large design
hole around init methods and annotating every method as setting members X or Y. !
was chosen because we already use it for suppressing nullable warnings, and using it to
tell the compiler "I'm smarter than you" in another place is a natural extension of the
syntax form.
This proposal does not allow interfaces to mark members as required. This protects us
from having to figure out complex scenarios around new() and interface constraints in
generics right now, and is directly related to both factories and generic construction. In
order to ensure that we have design space in this area, we forbid required in interfaces,
and forbid types with requir ed_member_lists  from being substituted for type parametersDiscussed Questions
Level of enforcement for init clauses
Required interface membersconstrained to new(). When we want to take a broader look at generic construction
scenarios with factories, we can revisit this issue.
Is init the right word? init as a postfix modifier on the constructor might
interfere if we ever want to reuse it for factories and also enable init methods
with a prefix modifier. Other possibilities:
set
Is required the right modifier for specifying that all members are initialized?
Others suggested:
default
all
With a ! to indicate complex logic
Should we require a separator between the base/this and the init?
: separator
',' separator
Is required the right modifier? Other alternatives that have been suggested:
req
require
mustinit
must
explicit
Conclusion : We have removed the init constructor clause for now, and are proceeding
with required as the property modifier.
Should we allow access to this in the init clause? If we want the assignment in init to
be a shorthand for assigning the member in the constructor itself, it seems like we
should.
Additionally, does it create a new scope, like base() does, or does it share the same
scope as the method body? This is particularly important for things like local functions,
which the init clause may want to access, or for name shadowing, if an init expression
introduces a variable via out parameter.
Conclusion : init clause has been removed.Syntax questions
Init clause restrictionsIn versions of this proposal with the init clause, we talked about being able to have the
following scenario:
C#
However, we have removed the init clause from the proposal at this point, so we need
to decide whether to allow this scenario in a limited fashion. The options we have are:
1. Disallow the scenario. This is the most conservative approach, and the rules in the
Accessibility  are currently written with this assumption in mind. The rule is that any
member that is required must be at least as visible as its containing type.
2. Require that all constructors are either:
a. No more visible than the least-visible required member.
b. Have the SetsRequiredMembersAttribute applied to the constructor. These
would ensure that anyone who can see a constructor can either set all the
things it exports, or there is nothing to set. This could be useful for types that
are only ever created via static Create methods or similar builders, but the
utility seems overall limited.
3. Readd a way to remove specific parts of the contract to the proposal, as discussed
in LDM  previously.
Conclusion : Option 1, all required members must be at least as visible as their
containing type.
The current spec says that the required keyword needs to be copied over and that
overrides can make a member more required, but not less. Is that what we want to do?Accessibility requirements and init
public class Base 
{ 
    protected  required int _field;  
    protected  Base() {} // Contract required that _field is set  
} 
public class Derived : Base 
{ 
    public Derived() : init(_field = 1) // Contract is fulfilled and _field  
is removed from the required members list  
    { 
    } 
} 
Override rulesAllowing removal of requirements needs more contract modification abilities than we
are currently proposing.
Conclusion : Adding required on override is allowed. If the overridden member is
required, the overridding member must also be required.
We could also take a different approach to metadata representation, taking a page from
extension methods. W e could put a RequiredMemberAttribute on the type to indicate
that the type contains required members, and then put a RequiredMemberAttribute on
each member that is required. This would simplify the lookup sequence (no need to do
member lookup, just look for members with the attribute).
Conclusion : Alternative approved.
The Metadata R epresentation  needs to be approved. W e additionally need to decide
whether these attributes should be included in the BCL.
1. For RequiredMemberAttribute, this attribute is more akin to the general embedded
attributes we use for nullable/nint/tuple member names, and will not be manually
applied by the user in C#. It's possible that other languages might want to
manually apply this attribute, however.
2. SetsRequiredMembersAttribute, on the other hand, is directly used by consumers,
and thus should likely be in the BCL.
If we go with the alternative representation in the previous section, that might change
the calculus on RequiredMemberAttribute: instead of being similar to the general
embedded attributes for nint/nullable/tuple member names, it's closer to
System.Runtime.CompilerServices.ExtensionAttribute, which has been in the framework
since extension methods shipped.
Conclusion : We will put both attributes in the BCL.
Should not setting a required member be a warning or an error? It is certainly possible
to trick the system, via Activator.CreateInstance(typeof(C)) or similar, which means we
may not be able to fully guarantee all properties are always set. W e also allowAlternative metadata representation
Metadata Representation
Warning vs Errorsuppression of the diagnostics at the constructor-site by using the !, which we
generally do not allow for errors. However, the feature is similar to readonly fields or init
properties, in that we hard error if users attempt to set such a member after
initialization, but they can be circumvented by reflection.
Conclusion : Errors.Auto-default structs
Article •06/23/2023
https://github.com/dotnet/csharplang/issues/5737
This feature makes it so that in struct constructors, we identify fields which were not
explicitly assigned by the user before returning or before use, and initialize them
implicitly to default instead of giving definite assignment errors.
This proposal is raised as a possible mitigation for usability issues found in
dotnet/csharplang#5552 and dotnet/csharplang#5635, as well as addressing #5563 (all
fields must be definitely assigned, but field is not accessible within the constructor).
Since C# 1.0, struct constructors have been required to definitely assign this as if it
were an out parameter.
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
public struct S 
{ 
    public int x, y; 
    public S() // error: Fields 'S.x' and 'S.y' must be fully assigned  
before control is returned to the caller  
    { 
    } 
} This presents issues when setters are manually defined on semi-auto properties, since
the compiler can't treat assignment of the property as equivalent to assignment of the
backing field.
C#
We assume that introducing finer-grained restrictions for setters, such as a scheme
where the setter doesn't take ref this but rather takes out field as a parameter, is
going to be too niche and incomplete for some use cases.
One fundamental tension we are struggling with is that when struct properties have
manually implemented setters, users often have to do some form of "repetition" of
either repeatedly assigning or repeating their logic:
C#public struct S 
{ 
    public int X { get => field; set => field = value; } 
    public S() // error: struct fields aren't fully assigned. But caller can  
only assign 'this.field' by assigning 'this'.  
    { 
    } 
} 
struct S 
{ 
    private int _x; 
    public int X 
    { 
        get => _x; 
        set => _x = value >= 0 ? value : throw new 
ArgumentOutOfRangeException();  
    } 
    // Solution 1: assign some value in the constructor before "really"  
assigning through the property setter.  
    public S(int x) 
    { 
        _x = default; 
        X = x;  
    } 
    // Solution 2: assign the field once in the constructor, repeating the  
implementation of the setter.  
    public S(int x) 
    { 
        _x = x >= 0 ? x : throw new ArgumentOutOfRangeException();  
    } 
} A small group has looked at this issue and considered a few possible solutions:
1. Require users to assign this = default when semi-auto properties have manually
implemented setters. W e agree this is the wrong solution since it blows away
values set in field initializers.
2. Implicitly initialize all backing fields of auto/semi-auto properties.
This solves the "semi-auto property setters" problem, and it squarely places
explicitly declared fields under different rules: "don't implicitly initialize my
fields, but do implicitly initialize my auto-properties."
3. Provide a way to assign the backing field of a semi-auto property and require users
to assign it.
This could be cumbersome compared to (2). An auto property is supposed to
be "automatic", and perhaps that includes "automatic" initialization of the
field. It could introduce confusion as to when the underlying field is being
assigned by an assignment to the property, and when the property setter is
being called.
We've also received feedback  from users who want to, for example, include a few field
initializers in structs without having to explicitly assign everything. W e can solve this
issue as well as the "semi-auto property with manually implemented setter" issue at the
same time.
C#Previous discussion
struct MagnitudeVector3d  
{ 
    double X, Y, Z;  
    double Magnitude = 1; 
    public MagnitudeVector3d () // error: must assign 'X', 'Y', 'Z' before  
returning  
    { 
    } 
} 
Adjusting definite assignmentInstead of performing a definite assignment analysis to give errors for unassigned fields
on this, we do it to determine which f ields need t o be initialized implicitly . Such
initialization is inserted at the beginning o f the c onstr uctor.
C#
struct S 
{ 
    int x, y; 
    // Example 1  
    public S() 
    { 
        // ok. Compiler inserts an assignment of `this = default`.  
    } 
    // Example 2  
    public S() 
    { 
        // ok. Compiler inserts an assignment of `y = default`.  
        x = 1; 
    } 
    // Example 3  
    public S() 
    { 
        // valid since C# 1.0. Compiler inserts no implicit assignments.  
        x = 1; 
        y = 2; 
    } 
    // Example 4  
    public S(bool b) 
    { 
        // ok. Compiler inserts assignment of `this = default`.  
        if (b) 
            x = 1; 
        else 
            y = 2; 
    } 
    // Example 5  
    void M() { } 
    public S(bool b) 
    { 
        // ok. Compiler inserts assignment of `y = default`.  
        x = 1; 
        if (b) 
            M();  
        y = 2; 
    } 
} In examples (4) and (5), the resulting codegen sometimes has "double assignments" of
fields. This is generally fine, but for users who are concerned with such double
assignments, we can emit what used to be definite assignment error diagnostics as
disabled-b y-default  warning diagnostics.
C#
Users who set the severity of this diagnostic to "error" will opt in to the pre-C# 11
behavior. Such users are essentially "shut out" of semi-auto properties with manually
implemented setters.
C#
At first glance, this feels like a "hole" in the feature, but it's actually the right thing t o
do. By enabling the diagnostic, the user is telling us that they don't want the compiler to
implicitly initialize their fields in the constructor. There's no way to avoid the implicit
initialization here, so the solution for them is to use a different way of initializing the
field than a manually implemented setter, such as manually declaring the field and
assigning it, or by including a field initializer.
Currently, the JIT does not eliminate dead stores through refs, which means that these
implicit initializations do have a real cost. But that might be fixable.
https://github.com/dotnet/runtime/issues/13727struct S 
{ 
    int x; 
    public S() // warning: 'S.x' is implicitly initialized to 'default'.  
    { 
    } 
} 
struct S 
{ 
    public int X 
    { 
        get => field;  
        set => field = field < value ? value : field;  
    } 
    public S() // error: backing field of 'S.X' is implicitly initialized to  
'default'.  
    { 
        X = 1; 
    } 
} 
It's worth noting that initializing individual fields instead of the entire instance is really
just an optimization. The compiler should probably be free to implement whatever
heuristic it wants, as long as it meets the invariant that fields which are not definitely
assigned at all return points or before any non-field member access of this are
implicitly initialized.
For example, if a struct has 100 fields, and just one of them is explicitly initialized, it
might make more sense to do an initobj on the entire thing, than to implicitly emit
initobj for the 99 other fields. However, an implementation which implicitly emits
initobj for the 99 other fields would still be valid.
We adjust the following section of the standard:
https://github.com/dotnet/csharpstandard/blob/draft-
v6/standard/expressions.md#11712-this-access
If the constructor declaration has no constructor initializer, the this variable
behaves exactly the same as an out parameter of the struct type. In particular, this
means that the variable shall be definitely assigned in every execution path of the
instance constructor.
We adjust this language to read:
If the constructor declaration has no constructor initializer, the this variable behaves
similarly to an out parameter of the struct type, except that it is not an error when the
definite assignment requirements ( §9.4.1 ) are not met. Instead, we introduce the
following behaviors:
1. When the this variable itself does not meet the requirements, then all unassigned
instance variables within this at all points where requirements are violated are
implicitly initialized to the default value ( §9.3 ) in an initialization  phase before
any other code in the constructor runs.
2. When an instance variable v within this does not meet the requirements, or any
instance variable at any level of nesting within v does not meet the requirements,
then v is implicitly initialized to the default value in an initialization  phase before
any other code in the constructor runs.Changes to language specification
Design meetingshttps://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-02-
14.md#definite-assignment-in-structs
Low Level Struct Improvements
Article •10/24/2023
This proposal is an aggregation of several different proposals for struct performance
improvements: ref fields and the ability to override lifetime defaults. The goal being a
design which takes into account the various proposals to create a single overarching
feature set for low level struct improvements.
Note: Previous versions of this spec used the terms "ref-safe-to-escape" and "safe-
to-escape", which were introduced in the Span safety  feature specification. The
ECMA standard committee  changed the names to "ref-safe-context"  and "safe-
context" , respectively. The values of the safe context have been refined to use
"declaration-block", "function-member", and "caller-context" consistently. The
speclets had used different phrasing for these terms, and also used "safe-to-return"
as a synonym for "caller-context". This speclet has been updated to use the terms in
the C# 7.3 standard.
Earlier versions of C# added a number of low level performance features to the
language: ref returns, ref struct, function pointers, etc. ... These enabled .NET
developers to write highly performant code while continuing to leverage the C#
language rules for type and memory safety. It also allowed the creation of fundamental
performance types in the .NET libraries like Span<T>.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
MotivationAs these features have gained traction in the .NET ecosystem developers, both internal
and external, have been providing us with information on remaining friction points in
the ecosystem. Places where they still need to drop to unsafe code to get their work
done, or require the runtime to special case types like Span<T>.
Today Span<T> is accomplished by using the internal type ByReference<T> which the
runtime effectively treats as a ref field. This provides the benefit of ref fields but with
the downside that the language provides no safety verification for it, as it does for other
uses of ref. Further only dotnet/runtime can use this type as it's internal, so 3rd
parties can not design their own primitives based on ref fields. P art of the motivation
for this work  is to remove ByReference<T> and use proper ref fields in all code bases.
This proposal plans to address these issues by building on top of our existing low level
features. Specifically it aims to:
Allow ref struct types to declare ref fields.
Allow the runtime to fully define Span<T> using the C# type system and remove
special case type like ByReference<T>
Allow struct types to return ref to their fields.
Allow runtime to remove unsafe uses caused by limitations of lifetime defaults
Allow the declaration of safe fixed buffers for managed and unmanaged types in
struct
The rules for ref struct safety are defined in the span safety document  using the
previous terms. Those rules have been incorporated into the C# 7 standard in §9.7.2
and §16.4.12 . This document will describe the required changes to this document as a
result of this proposal. Once accepted as an approved feature these changes will be
incorporated into that document.
Once this design is complete our Span<T> definition will be as follows:
c#
Detailed Design
readonly  ref struct Span<T>
{
    readonly  ref T _field;
    readonly  int _length;
    // This constructor does not exist today but will be added as a part 
    // of changing Span<T> to have ref fields. It is a convenient, and
    // safe, way to create a length one span over a stack value that today The language will allow developers to declare ref fields inside of a ref struct. This can
be useful for example when encapsulating large mutable struct instances or defining
high performance types like Span<T> in libraries besides the runtime.
C#
A ref field will be emitted into metadata using the ELEMENT_TYPE_BYREF signature. This
is no different than how we emit ref locals or ref arguments. For example ref int
_field will be emitted as ELEMENT_TYPE_BYREF ELEMENT_TYPE_I4. This will require us to
update ECMA335 to allow this entry but this should be rather straight forward.
Developers can continue to initialize a ref struct with a ref field using the default
expression in which case all declared ref fields will have the value null. Any attempt to
use such fields will result in a NullReferenceException being thrown.
c#
While the C# language pretends that a ref cannot be null this is legal at the runtime
level and has well defined semantics. Developers who introduce ref fields into their
types need to be aware of this possibility and should be strongly  discouraged from
leaking this detail into consuming code. Instead ref fields should be validated as non-    // requires unsafe code.
    public Span(ref T value)
    {
        _field = ref value;
        _length = 1;
    }
}
Provide ref fields and scoped
ref struct S 
{
    public ref int Value;
}
ref struct S 
{
    public ref int Value;
}
S local = default;
local.Value.ToString(); // throws NullReferenceExceptionnull using the runtime helpers  and throwing when an uninitialized struct is used
incorrectly.
c#
A ref field can be combined with readonly modifiers in the following ways:
readonly ref: this is a field that cannot be ref reassigned outside a constructor or
init methods. It can be value assigned though outside those contexts
ref readonly: this is a field that can be ref reassigned but cannot be value
assigned at any point. This how an in parameter could be ref reassigned to a ref
field.
readonly ref readonly: a combination of ref readonly and readonly ref.
c#
ref struct S1 
{
    private ref int Value;
    public int GetValue ()
    {
        if (System.Runtime.CompilerServices.Unsafe.IsNullRef( ref Value))
        {
            throw new InvalidOperationException(...);
        }
        return Value;
    }
}
ref struct ReadOnlyExample
{
    ref readonly  int Field1;
    readonly  ref int Field2;
    readonly  ref readonly  int Field3;
    void Uses(int[] array )
    {
        Field1 = ref array[0];  // Okay
        Field1 = array[ 0];      // Error: can't assign ref readonly value  
(value is readonly)
        Field2 = ref array[0];  // Error: can't repoint readonly ref
        Field2 = array[ 0];      // Okay
        Field3 = ref array[0];  // Error: can't repoint readonly ref
        Field3 = array[ 0];      // Error: can't assign ref readonly value  
(value is readonly)A readonly ref struct will require that ref fields are declared readonly ref. There is
no requirement that they are declared readonly ref readonly. This does allow a
readonly struct to have indirect mutations via such a field but that is no different than
a readonly field that pointed to a reference type today ( more details )
A readonly ref will be emitted to metadata using the initonly flag, same as any other
field. A ref readonly field will be attributed with
System.Runtime.CompilerServices.IsReadOnlyAttribute. A readonly ref readonly will be
emitted with both items.
This feature requires runtime support and changes to the ECMA spec. As such these will
only be enabled when the corresponding feature flag is set in corelib. The issue tracking
the exact API is tracked here https://github.com/dotnet/runtime/issues/64165
The set of changes to our safe context rules necessary to allow ref fields is small and
targeted. The rules already account for ref fields existing and being consumed from
APIs. The changes need to focus on only two aspects: how they are created and how
they are ref reassigned.
First the rules establishing ref-safe-c ontext values for fields need to be updated for ref
fields as follows:
An expression in the form ref e.F ref-safe-c ontext as follows:
1. If F is a ref field its ref-safe-c ontext is the safe-c ontext of e.
2. Else if e is of a reference type, it has ref-safe-c ontext of caller -context
3. Else its ref-safe-c ontext is taken from the ref-safe-c ontext of e.
This does not represent a rule change though as the rules have always accounted for
ref state to exist inside a ref struct. This is in fact how the ref state in Span<T> has
always worked and the consumption rules correctly account for this. The change here is
just accounting for developers to be able to access ref fields directly and ensure they
do so by the existing rules implicitly applied to Span<T>.
This does mean though that ref fields can be returned as ref from a ref struct but
normal fields cannot.
c#    }
}
This may seem like an error at first glance but this is a deliberate design point. Again
though, this is not a new rule being created by this proposal, it is instead acknowledging
the existing rules Span<T> behaved by now that developers can declare their own ref
state.
Next the rules for ref reassignment need to be adjusted for the presence of ref fields.
The primary scenario for ref reassignment is ref struct constructors storing ref
parameters into ref fields. The support will be more general but this is the core
scenario. T o support this the rules for ref reassignment will be adjusted to account for
ref fields as follows:
The left operand of the = ref operator must be an expression that binds to a ref local
variable, a ref parameter (other than this), an out parameter, or a r ef field .
For a ref reassignment in the form e1 = ref e2 both of the following must be true:
1. e2 must have ref-safe-c ontext at least as large as the ref-safe-c ontext of e1
2. e1 must have the same safe-c ontext as e2 Note
That means the desired Span<T> constructor works without any extra annotation:
c#ref struct RS
{
    ref int _refField;
    int _field;
    // Okay: this falls into bullet one above. 
    public ref int Prop1 => ref _refField;
    // Error: This is bullet four above and the ref-safe-context of `this`
    // in a `struct` is function-member.
    public ref int Prop2 => ref _field;
}
Ref reassignment rules
readonly  ref struct Span<T>
{
    readonly  ref T _field;
    readonly  int _length;
    public Span(ref T value)
    {The change to ref reassignment rules means ref parameters can now escape from a
method as a ref field in a ref struct value. As discussed in the compat considerations
section  this can change the rules for existing APIs that never intended for ref
parameters to escape as a ref field. The lifetime rules for parameters are based solely
on their declaration not on their usage. All ref and in parameters have ref-safe-c ontext
of caller -context and hence can now be returned by ref or a ref field. In order to
support APIs having ref parameters that can be escaping or non-escaping, and thus
restore C# 10 call site semantics, the language will introduce limited lifetime
annotations.
The keyword scoped will be used to restrict the lifetime of a value. It can be applied to a
ref or a value that is a ref struct and has the impact of restricting the ref-safe-c ontext
or safe-c ontext lifetime, respectively, to the function-member . For example:
Paramet er or Local ref-safe-cont ext safe-cont ext
Span<int> s function-member caller -context
scoped Span<int> s function-member function-member
ref Span<int> s caller -context caller -context
scoped ref Span<int> s function-member caller -context
In this relationship the ref-safe-c ontext of a value can never be wider the safe-c ontext.
This allows for APIs in C# 11 to be annotated such that they have the same rules as C#
10:
c#        // Falls into the `x.e1 = ref e2` case, where `x` is the implicit  
`this`. The 
        // safe-context of `this` is *return-only* and ref-safe-context of  
`value` is 
        // *caller-context* hence this is legal.
        _field = ref value;
        _length = 1;
    }
}
scoped modifier
Span<int> CreateSpan (scoped ref int parameter )
{The scoped annotation also means that the this parameter of a struct can now be
defined as scoped ref T. Previously it had to be special cased in the rules as ref
parameter that had different ref-safe-c ontext rules than other ref parameters (see all
the references to including or excluding the receiver in the safe context rules). Now it
can be expressed as a general concept throughout the rules which further simplifies
them.
The scoped annotation can also be applied to the following locations:
locals: This annotation sets the lifetime as safe-c ontext, or ref-safe-c ontext in case
of a ref local, to of function-member  irrespective of the initializer lifetime.
c#    // Just as with C# 10, the implementation of this method isn't relevant  
to callers.
}
Span<int> BadUseExamples (int parameter )
{
    // Legal in C# 10 and legal in C# 11 due to scoped ref
    return CreateSpan( ref parameter);
    // Legal in C# 10 and legal in C# 11 due to scoped ref
    int local = 42;
    return CreateSpan( ref local);
    // Legal in C# 10 and legal in C# 11 due to scoped ref
    Span<int> span = stackalloc  int[42];
    return CreateSpan( ref span[0]);
}
Span<int> ScopedLocalExamples ()
{
    // Error: `span` has a safe-context of *function-member*. That is true  
even though the 
    // initializer has a safe-context of *caller-context*. The annotation  
overrides the 
    // initializer
    scoped Span< int> span = default;
    return span;
    // Okay: the initializer has safe-context of *caller-context* hence so  
does `span2` 
    // and the return is legal.
    Span<int> span2 = default;
    return span2;
    // The declarations of `span3` and `span4` are functionally identical  
because the Other uses for scoped on locals are discussed below .
The scoped annotation cannot be applied to any other location including returns, fields,
array elements, etc ... Further while scoped has impact when applied to any ref, in or
out it only has impact when applied to values which are ref struct. Having
declarations like scoped int has no impact because a non ref struct is always safe to
return. The compiler will create a diagnostic for such cases to avoid developer
confusion.
To further limit the impact of the compat change of making ref and in parameters
returnable as ref fields, the language will change the default ref-safe-c ontext value for
out parameters to be function-member . Effectively out parameters are implicitly scoped
out going forward. From a compat perspective this means they cannot be returned by
ref:
c#
This will increase the flexibility of APIs that return ref struct values and have out
parameters because it does not have to consider the parameter being captured by
reference anymore. This is important because it's a common pattern in reader style APIs:
c#    // initializer has a safe-context of *function-member* meaning the  
`scoped` annotation
    // is effectively implied on `span3`
    Span<int> span3 = stackalloc  int[42];
    scoped Span< int> span4 = stackalloc  int[42];
}
Change the behavior of out parameters
ref int Sneaky(out int i) 
{
    i = 42;
    // Error: ref-safe-context of out is now function-member
    return ref i;
}
Span<byte> Read(Span<byte> buffer, out int read)
{
    // .. 
}The language will also no longer consider arguments passed to an out parameter to be
returnable. T reating the input to an out parameter as returnable was extremely
confusing to developers. It essentially subverts the intent of out by forcing developers
to consider the value passed by the caller which is never used except in languages that
don't respect out. Going forward languages that support ref struct must ensure the
original value passed to an out parameter is never read.
C# achieves this via it's definite assignment rules. That both achieves our ref safe context
rules as well as allowing for existing code which assigns and then returns out
parameters values.
c#
Together these changes mean the argument to an out parameter does not contribute
safe-c ontext or ref-safe-c ontext values to method invocations. This significantly reduces
the overall compat impact of ref fields as well as simplifies how developers think about
out. An argument to an out parameter does not contribute to the return, it is simply an
output.
The safe-c ontext of a declaration variable from an out argument ( M(x, out var y)) or
deconstruction ( (var x, var y) = M()) is the narrowest of the following:Span<byte> Use()
{
    var buffer = new byte[256];
    // If we keep current `out` ref-safe-context this is an error. The  
language must consider
    // the `read` parameter as returnable as a `ref` field
    //
    // If we change `out` ref-safe-context this is legal. The language does  
not consider the 
    // `read` parameter to be returnable hence this is safe
    int read;
    return Read(buffer, out read);
}
Span<int> StrangeButLegal (out Span<int> span)
{
    span = default;
    return span;
}
Infer s a f e -c o n t e x t of declaration expressionscaller-context
if out variable is marked scoped, then declar ation-block  (i.e. function-member or
narrower).
if out variable's type is ref struct, consider all arguments to the containing
invocation, including the receiver:
safe-c ontext of any argument where its corresponding parameter is not out and
has safe-c ontext of return-only  or wider
ref-safe-c ontext of any argument where its corresponding parameter has ref-
safe-c ontext of return-only  or wider
See also Examples of inferred safe-c ontext of declaration expressions .
Overall there are two ref location which are implicitly declared as scoped:
this on a struct instance method
out parameters
The ref safe context rules will be written in terms of scoped ref and ref. For ref safe
context purposes an in parameter is equivalent to ref and out is equivalent to scoped
ref. Both in and out will only be specifically called out when it is important to the
semantic of the rule. Otherwise they are just considered ref and scoped ref
respectively.
When discussing the ref-safe-c ontext of arguments that correspond to in parameters
they will be generalized as ref arguments in the spec. In the case the argument is an
lvalue then the ref-safe-c ontext is that of the lvalue, otherwise it is function-member .
Again in will only be called out here when it is important to the semantic of the current
rule.
The design also requires that the introduction of a new safe-context: return-only . This is
similar to caller -context in that it can be returned but it can only be returned through a
return statement.
The details of return-only  is that it's a context which is greater than function-member  but
smaller than caller -context. An expression provided to a return statement must be at
least return-only . As such most existing rules fall out. For example assignment into a ref
parameter from an expression with a safe-c ontext of return-only  will fail because it'sImplicitly scoped parameters
Return-only safe contextsmaller than the ref parameter's safe-c ontext which is caller -context. The need for this
new escape context will be discussed below .
There are three locations which default to return-only :
A ref or in parameter with have a ref-safe-c ontext of return-only . This is done in
part for ref struct to prevent silly cyclic assignment  issues. It is done uniformly
though to simplify the model as well as minimize compat changes.
A out parameter for a ref struct will have safe-c ontext of return-only . This allows
for return and out to be equally expressive. This does not have the silly cyclic
assignment problem because out is implicitly scoped so the ref-safe-c ontext is still
smaller than the safe-c ontext.
A this parameter for a struct constructor will have a safe-c ontext of return-only .
This falls out due to being modeled as out parameters.
Any expression or statement which explicitly returns a value from a method or lambda
must have a safe-c ontext, and if applicable a ref-safe-c ontext, of at least return-only . That
includes return statements, expression bodied members and lambda expressions.
Likewise any assignment to an out must have a safe-c ontext of at least return-only . This
is not a special case though, this just follows from the existing assignment rules.
Note: An expression whose type is not a ref struct type always has a safe-c ontext of
caller -context.
The ref safe context rules for method invocation will be updated in several ways. The
first is by recognizing the impact that scoped has on arguments. For a given argument
expr that is passed to parameter p:
1. If p is scoped ref then expr does not contribute ref-safe-c ontext when
considering arguments.
2. If p is scoped then expr does not contribute safe-c ontext when considering
arguments.
3. If p is out then expr does not contribute ref-safe-c ontext or safe-c ontext more
details
The language "does not contribute" means the arguments are simply not considered
when calculating the ref-safe-c ontext or safe-c ontext value of the method returnRules for method invocationrespectively. That is because the values can't contribute to that lifetime as the scoped
annotation prevents it.
The method invocation rules can now be simplified. The receiver no longer needs to be
special cased, in the case of struct it is now simply a scoped ref T. The value rules
need to change to account for ref field returns:
A value resulting from a method invocation e1.M(e2, ...), where M() does not
return ref-to-ref-struct, has a safe-c ontext taken from the narrowest of the following:
1. The caller -context
2. When the return is a ref struct the safe-c ontext contributed by all argument
expressions
3. When the return is a ref struct the ref-safe-c ontext contributed by all ref
arguments
If M() does return ref-to-ref-struct, the safe-c ontext is the same as the safe-c ontext
of all arguments which are ref-to-ref-struct. It is an error if there are multiple
arguments with different safe-c ontext because of method arguments must match .
The ref calling rules can be simplified to:
A value resulting from a method invocation ref e1.M(e2, ...), where M() does not
return ref-to-ref-struct, is ref-safe-c ontext the narrowest of the following contexts:
1. The caller -context
2. The safe-c ontext contributed by all argument expressions
3. The ref-safe-c ontext contributed by all ref arguments
If M() does return ref-to-ref-struct, the ref-safe-c ontext is the narrowest ref-safe-
context contributed by all arguments which are ref-to-ref-struct.
This rule now lets us define the two variants of desired methods:
c#
Span<int> CreateWithoutCapture (scoped ref int value)
{
    // Error: value Rule 3 specifies that the safe-context be limited to the  
ref-safe-context
    // of the ref argument. That is the *function-member* for value hence  
this is not allowed.
    return new Span<int>(ref value);
}The presence of ref fields means the rules around method arguments must match need
to be updated as a ref parameter can now be stored as a field in a ref struct
argument to the method. Previously the rule only had to consider another ref struct
being stored as a field. The impact of this is discussed in the compat considerations . The
new rule is ...
For any method invocation e.M(a1, a2, ... aN)
1. Calculate the narrowest safe-c ontext from:
caller -context
The safe-c ontext of all argumentsSpan<int> CreateAndCapture (ref int value)
{
    // Okay: value Rule 3 specifies that the safe-context be limited to the  
ref-safe-context
    // of the ref argument. That is the *caller-context* for value hence  
this is not allowed.
    return new Span<int>(ref value);
}
Span<int> ComplexScopedRefExample (scoped ref Span<int> span)
{
    // Okay: the safe-context of `span` is *caller-context* hence this is  
legal.
    return span;
    // Okay: the local `refLocal` has a ref-safe-context of *function-
member* and a 
    // safe-context of *caller-context*. In the call below it is passed to a  
    // parameter that is `scoped ref` which means it does not contribute 
    // ref-safe-context. It only contributes its safe-context hence the  
returned
    // rvalue ends up as safe-context of *caller-context*
    Span<int> local = default;
    ref Span<int> refLocal = ref local;
    return ComplexScopedRefExample( ref refLocal);
    // Error: similar analysis as above but the safe-context of `stackLocal`  
is 
    // *function-member* hence this is illegal
    Span<int> stackLocal = stackalloc  int[42];
    return ComplexScopedRefExample( ref stackLocal);
}
Method arguments must matchThe ref-safe-c ontext of all ref arguments whose corresponding
parameters have a ref-safe-c ontext of caller -context
2. All ref arguments of ref struct types must be assignable by a value with
that safe-cpmt ext. This is a case where ref does not generalize to include in
and out
For any method invocation e.M(a1, a2, ... aN)
1. Calculate the narrowest safe-c ontext from:
caller -context
The safe-c ontext of all arguments
The ref-safe-c ontext of all ref arguments whose corresponding
parameters are not scoped
2. All out arguments of ref struct types must be assignable by a value with
that safe-c ontext.
The presence of scoped allows developers to reduce the friction this rule creates by
marking parameters which are not returned as scoped. This removes their arguments
from (1) in both cases above and provides greater flexibility to callers.
Impact of this change is discussed more deeply below . Overall this will allow developers
to make call sites more flexible by annotating non-escaping ref-like values with scoped.
The scoped modifier and [UnscopedRef] attribute (see below ) on parameters also
impacts our object overriding, interface implementation and delegate conversion rules.
The signature for an override, interface implementation or delegate conversion can:
Add scoped to a ref or in parameter
Add scoped to a ref struct parameter
Remove [UnscopedRef] from an out parameter
Remove [UnscopedRef] from a ref parameter of a ref struct type
Any other difference with respect to scoped or [UnscopedRef] is considered a mismatch.
The compiler will report a diagnostic for unsafe scoped mismat ches across overrides,
interface implementations, and delegate conversions when:Parameter scope varianceThe method returns a ref struct or returns a ref or ref readonly, or the method
has a ref or out parameter of ref struct type, and
The method has at least one additional ref, in, or out parameter, or a parameter
of ref struct type.
The rules above ignore this parameters because ref struct instance methods cannot
be used for overrides, interface implementations, or delegate conversions.
The diagnostic is reported as an error if the mismatched signatures are both using C#11
ref safe context rules; otherwise, the diagnostic is a warning.
The scoped mismatch warning may be reported on a module compiled with C#7.2 ref
safe context rules where scoped is not available. In some such cases, it may be necessary
to suppress the warning if the other mismatched signature cannot be modified.
The scoped modifier and [UnscopedRef] attribute also have the following effects on
method signatures:
The scoped modifier and [UnscopedRef] attribute do not affect hiding
Overloads cannot differ only on scoped or [UnscopedRef]
The section on ref field and scoped is long so wanted to close with a brief summary of
the proposed breaking changes:
A value that has ref-safe-c ontext to the caller -context is returnable by ref or ref
field.
A out parameter would have a safe-c ontext of function-member .
Detailed Notes:
A ref field can only be declared inside of a ref struct
A ref field cannot be declared static, volatile or const
A ref field cannot have a type that is ref struct
The reference assembly generation process must preserve the presence of a ref
field inside a ref struct
A readonly ref struct must declare its ref fields as readonly ref
For by-ref values the scoped modifier must appear before in, out, or ref
The span safety rules document will be updated as outlined in this document
The new ref safe context rules will be in effect when either
The core library contains the feature flag indicating support for ref fields
The langversion value is 11 or higher12.6.2 Local variable declarations : added 'scoped'?.
antlr
12.9.4 The for statement : added 'scoped'? indirectly from
local_variable_declaration.
12.9.5 The foreach  statement : added 'scoped'?.
antlr
11.6.2 Argument lists : added 'scoped'? for out declaration variable.
antlr
--.-.- Deconstruction expressions :
antlr
14.6.2 Method parameters : added 'scoped'? to parameter_modifier.Syntax
local_variable_declaration
    : 'scoped' ? local_variable_mode_modifier? local_variable_type  
local_variable_declarators
    ;
local_variable_mode_modifier
    : 'ref' 'readonly' ?
    ;
foreach_statement
    : 'foreach'  '(' 'scoped' ? local_variable_type identifier 'in' expression  
')'
      embedded_statement
    ;
argument_value
    : expression
    | 'in' variable_reference
    | 'ref' variable_reference
    | 'out' ('scoped' ? local_variable_type)? identifier
    ;
[TBD]
antlr
19.2 Delegate declarations : added 'scoped'? indirectly from fixed_parameter.
11.16 Anonymous function expressions : added 'scoped'?.
antlr
The compiler has a concept of a set of "restricted types" which is largely undocumented.
These types were given a special status because in C# 1.0 there was no general purpose
way to express their behavior. Most notably the fact that the types can contain
references to the execution stack. Instead the compiler had special knowledge of them
and restricted their use to ways that would always be safe: disallowed returns, cannot
use as array elements, cannot use in generics, etc ...
Once ref fields are available and extended to support ref struct these types can be
correctly defined in C# using a combination of ref struct and ref fields. Thereforefixed_parameter
    : attributes? parameter_modifier? type identifier default_argument?
    ;
parameter_modifier
    | 'this' 'scoped' ? parameter_mode_modifier?
    | 'scoped'  parameter_mode_modifier?
    | parameter_mode_modifier
    ;
parameter_mode_modifier
    : 'in'
    | 'ref'
    | 'out'
    ;
explicit_anonymous_function_parameter
    : 'scoped' ? anonymous_function_parameter_modifier? type identifier
    ;
anonymous_function_parameter_modifier
    : 'in'
    | 'ref'
    | 'out'
    ;
Sunset restricted typeswhen the compiler detects that a runtime supports ref fields it will no longer have a
notion of restricted types. It will instead use the types as they are defined in the code.
To support this our ref safe context rules will be updated as follows:
__makeref will be treated as a method with the signature static TypedReference
__makeref<T>(ref T value)
__refvalue will be treated as a method with the signature static ref T
__refvalue<T>(TypedReference tr). The expression __refvalue(tr, int) will
effectively use the second argument as the type parameter.
__arglist as a parameter will have a ref-safe-c ontext and safe-c ontext of function-
member .
__arglist(...) as an expression will have a ref-safe-c ontext and safe-c ontext of
function-member .
Conforming runtimes will ensure that TypedReference, RuntimeArgumentHandle and
ArgIterator are defined as ref struct. Further TypedReference must be viewed as
having a ref field to a ref struct for any possible type (it can store any value). That
combined with the above rules will ensure references to the stack do not escape beyond
their lifetime.
Note: strictly speaking this is a compiler implementation detail vs. part of the language.
But given the relationship with ref fields it is being included in the language proposal
for simplicity.
One of the most notable friction points is the inability to return fields by ref in instance
members of a struct. This means developers can't create ref returning methods /
properties and have to resort to exposing fields directly. This reduces the usefulness of
ref returns in struct where it is often the most desired.
c#Provide unscoped
struct S
{
    int _field;
    // Error: this, and hence _field, can't return by ref
    public ref int Prop => ref _field;
}The rationale  for this default is reasonable but there is nothing inherently wrong with
a struct escaping this by reference, it is simply the default chosen by the ref safe
context rules.
To fix this the language will provide the opposite of the scoped lifetime annotation by
supporting an UnscopedRefAttribute. This can be applied to any ref and it will change
the ref-safe-c ontext to be one level wider than its default. For example:
if applied to a struct instance method it will become return only  where previously
it was containing method .
if applied to a ref parameter it will become caller -context where previously it was
return only
When applying [UnscopedRef] to an instance method of a struct it has the impact of
modifying the implicit this parameter. This means this acts as an unannotated ref of
the same type.
c#
The annotation can also be placed on out parameters to restore them to C# 10
behavior.
c#
struct S
{
    int field; 
    // Error: `field` has the ref-safe-context of `this` which is *function-
member* because 
    // it is a `scoped ref`
    ref int Prop1 => ref field;
    // Okay: `field` has the ref-safe-context of `this` which is *caller-
context* because 
    // it is a `ref`
    [UnscopedRef ] ref int Prop1 => ref field;
}
ref int SneakyOut ([UnscopedRef] out int i)
{
    i = 42;
    return ref i;
}For the purposes of ref safe cotnext rules, such an [UnscopedRef] out is considered
simply a ref. Similar to how in is considered ref for lifetime purposes.
The [UnscopedRef] annotation will be disallowed on init members and constructors
inside struct. Those members are already special with respect to ref semantics as they
view readonly members as mutable. This means taking ref to those members appears
as a simple ref, not ref readonly. This is allowed within the boundary of constructors
and init. Allowing [UnscopedRef] would permit such a ref to incorrectly escape
outside the constructor and permit mutation after readonly semantics had taken place.
The attribute type will have the following definition:
c#
Detailed Notes:
An instance method or property annotated with [UnscopedRef] has ref-safe-c ontext
of this set to the caller -context.
A member annotated with [UnscopedRef] cannot implement an interface.
It is an error to use [UnscopedRef] on
A member that is not declared on a struct
A static member, init member or constructor on a struct
A parameter marked scoped
A parameter passed by value
A parameter passed by reference that is not implicitly scoped
The scoped annotations will be emitted into metadata via the type
System.Runtime.CompilerServices.ScopedRefAttribute attribute. The attribute will benamespace  System.Diagnostics.CodeAnalysis
{
    [AttributeUsage(
        AttributeTargets.Method | AttributeTargets.Property |  
AttributeTargets.Parameter,
        AllowMultiple = false,
        Inherited = false) ]
    public sealed class UnscopedRefAttribute  : Attribute
    {
    }
}
ScopedRefAttributematched by namespace-qualified name so the definition does not need to appear in any
specific assembly.
The ScopedRefAttribute type is for compiler use only - it is not permitted in source. The
type declaration is synthesized by the compiler if not already included in the
compilation.
The type will have the following definition:
c#
The compiler will emit this attribute on the parameter with scoped syntax. This will only
be emitted when the syntax causes the value to differ from its default state. For example
scoped out will cause no attribute to be emitted.
There are several differences in the ref safe context rules between C#7.2 and C#11. Any
of these differences could result in breaking changes when recompiling with C#11
against references compiled with C#10 or earlier.
1. unscoped ref/in/out parameters may escape a method invocation as a ref field
of a ref struct in C#11, not in C#7.2
2. out parameters are implicitly scoped in C#11, and unscoped in C#7.2
3. ref/in parameters to ref struct types are implicitly scoped in C#11, and
unscoped in C#7.2
To reduce the chance of breaking changes when recompiling with C#11, we will update
the C#11 compiler to use the ref safe context rules for method in vocation  that match the
rules that w ere used to analyze the method declar ation . Essentially, when analyzing a call
to a method compiled with an older compiler, the C#11 compiler will use C#7.2 ref safe
context rules.
To enable this, the compiler will emit a new [module: RefSafetyRules(11)] attribute
when the module is compiled with -langversion:11 or higher or compiled with a corlibnamespace  System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Parameter, AllowMultiple = false,  
Inherited = false) ]
    internal  sealed class ScopedRefAttribute  : Attribute
    {
    }
}
RefSafetyRulesAttributecontaining the feature flag for ref fields.
The argument to the attribute indicates the language version of the ref safe context rules
used when the module was compiled. The version is currently fixed at 11 regardless of
the actual language version passed to the compiler.
The expectation is that future versions of the compiler will update the ref safe context
rules and emit attributes with distinct versions.
If the compiler loads a module that includes a [module: RefSafetyRules(version)] with
a version other than 11, the compiler will report a warning for the unrecognized
version if there are any calls to methods declared in that module.
When the C#11 compiler analyzes a method call :
If the module containing the method declaration includes [module:
RefSafetyRules(version)], regardless of version, the method call is analyzed with
C#11 rules.
If the module containing the method declaration is from source, and compiled
with -langversion:11 or with a corlib containing the feature flag for ref fields, the
method call is analyzed with C#11 rules.
If the module c ontaining the method declar ation r eferences System.Runtime { ver:
7.0 }, the method call is analyzed with C#11 r ules. This r ule is a t empor ary
mitigation for modules c ompiled with earlier pr eviews o f C#11 / .NE T 7 and will be
removed lat er.
Otherwise, the method call is analyzed with C#7.2 rules.
A pre-C#11 compiler will ignore any RefSafetyRulesAttribute and analyze method calls
with C#7.2 rules only.
The RefSafetyRulesAttribute will be matched by namespace-qualified name so the
definition does not need to appear in any specific assembly.
The RefSafetyRulesAttribute type is for compiler use only - it is not permitted in
source. The type declaration is synthesized by the compiler if not already included in the
compilation.
C#
namespace  System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Module, AllowMultiple = false,  
Inherited = false) ]
    internal  sealed class RefSafetyRulesAttribute  : Attribute
    {Safe fixed size buffers was not delivered in C# 11. This feature may be implemented in a
future version of C#.
The language will relax the restrictions on fixed sized arrays such that they can be
declared in safe code and the element type can be managed or unmanaged. This will
make types like the following legal:
c#
These declarations, much like their unsafe counter parts, will define a sequence of N
elements in the containing type. These members can be accessed with an indexer and
can also be converted to Span<T> and ReadOnlySpan<T> instances.
When indexing into a fixed buffer of type T the readonly state of the container must
be taken into account. If the container is readonly then the indexer returns ref readonly
T else it returns ref T.
Accessing a fixed buffer without an indexer has no natural type however it is
convertible to Span<T> types. In the case the container is readonly the buffer is
implicitly convertible to ReadOnlySpan<T>, else it can implicitly convert to Span<T> or
ReadOnlySpan<T> (the Span<T> conversion is considered better).
The resulting Span<T> instance will have a length equal to the size declared on the
fixed buffer. The safe-c ontext of the returned value will be equal to the safe-c ontext of
the container, just as it would if the backing data was accessed as a field.
For each fixed declaration in a type where the element type is T the language will
generate a corresponding get only indexer method whose return type is ref T. The
indexer will be annotated with the [UnscopedRef] attribute as the implementation will
be returning fields of the declaring type. The accessibility of the member will match the
accessibility on the fixed field.        public RefSafetyRulesAttribute (int version ) { Version = version; }
        public readonly  int Version;
    }
}
Safe fixed size buffers
internal  struct CharBuffer
{
    internal  char Data[128];
}For example, the signature of the indexer for CharBuffer.Data will be the following:
c#
If the provided index is outside the declared bounds of the fixed array then an
IndexOutOfRangeException will be thrown. In the case a constant value is provided then
it will be replaced with a direct reference to the appropriate element. Unless the
constant is outside the declared bounds in which case a compile time error would occur.
There will also be a named accessor generated for each fixed buffer that provides by
value get and set operations. Having this means that fixed buffers will more closely
resemble existing array semantics by having a ref accessor as well as byval get and
set operations. This means compilers will have the same flexibility when emitting code
consuming fixed buffers as they do when consuming arrays. This should make
operations like await over fixed buffers easier to emit.
This also has the added benefit that it will make fixed buffers easier to consume from
other languages. Named indexers is a feature that has existed since the 1.0 release of
.NET. Even languages which cannot directly emit a named indexer can generally
consume them (C# is actually a good example of this).
The backing storage for the buffer will be generated using the [InlineArray] attribute.
This is a mechanism discussed in issue 12320  which allows specifically for the case of
efficiently declaring sequence of fields of the same type. This particular issue is still
under active discussion and the expectation is that the implementation of this feature
will follow however that discussion goes.
In section 11.7.15.3 Object initializers , we update the grammar to:
antlr
In the section for with expression , we update the grammar to:[UnscopedRef ] internal  ref char DataIndexer (int index) => ...;
Initializers with ref values in new and with expressions
initializer_value
    : 'ref' expression // added
    | expression
    | object_or_collection_initializer
    ;
antlr
The left operand of the assignment must be an expression that binds to a ref field.
The right operand must be an expression that yields an lvalue designating a value of the
same type as the left operand.
We add a similar rule to ref local reassignment :
If the left operand is a writeable ref (i.e. it designates anything other than a ref
readonly field), then the right operand must be a writeable lvalue.
The escape rules for constructor invocations  remain:
A new expression that invokes a constructor obeys the same rules as a method
invocation that is considered to return the type being constructed.
Namely the rules of method invocation  updated above:
An rvalue resulting from a method invocation e1.M(e2, ...) has safe-c ontext from
the smallest of the following contexts:
1. The caller -context
2. The safe-c ontext contributed by all argument expressions
3. When the return is a ref struct then ref-safe-c ontext contributed by all ref
arguments
For a new expression with initializers, the initializer expressions count as arguments (they
contribute their safe-c ontext) and the ref initializer expressions count as ref arguments
(they contribute their ref-safe-c ontext), recursively.
Pointer types ( section 22.3 ) are extended to allow managed types as referent type.
Such pointer types are written as a managed type followed by a * token. They produce
a warning.
The address-of operator ( section 22.6.5 ) is relaxed to accept a variable with a
managed type as its operand.member_initializer
    : identifier '=' 'ref' expression // added
    | identifier '=' expression
    ;
Changes in unsafe context
The fixed statement ( section 22.7 ) is relaxed to accept fixed_point er_initializer  that is
the address of a variable of managed type T or that is an expression of an array_type
with elements of a managed type T.
The stack allocation initializer ( section 22.9 ) is similarly relaxed.
There are considerations other parts of the development stack should consider when
evaluating this feature.
The challenge in this proposal is the compatibility implications this design has to our
existing span safety rules , or §9.7.2 . While those rules fully support the concept of a
ref struct having ref fields they do not allow for APIs, other than stackalloc, to
capture ref state that refers to the stack. The ref safe cpmtext rules have a hard
assumption , or §16.4.12.8  that a constructor of the form Span(ref T value) does
not exist. That means the safety rules do not account for a ref parameter being able to
escape as a ref field hence it allows for code like the following.
c#
Effectively there are three ways for a ref parameter to escape from a method
invocation:
1. By value return
2. By ref return
3. By ref field in ref struct that is returned or passed as ref / out parameter
The existing rules only account for (1) and (2). They do not account for (3) hence gaps
like returning locals as ref fields are not accounted for. This design must change the
Considerations
Compat Considerations
Span<int> CreateSpanOfInt ()
{
    // This is legal according to the 7.2 span rules because they do not  
account
    // for a constructor in the form Span(ref T value) existing. 
    int local = 42;
    return new Span<int>(ref local);
}rules to account for (3). This will have a small impact to compatibility for existing APIs.
Specifically it will impact APIs that have the following properties.
Have a ref struct in the signature
Where the ref struct is a return type, ref or out parameter
Has an additional in or ref parameter excluding the receiver
In C# 10 callers of such APIs never had to consider that ref state input to the API could
be captured as a ref field. That allowed for several patterns to exist, safely in C# 10, that
will be unsafe in C# 11 due to the ability for ref state to escape as a ref field. For
example:
c#
The impact of this compatibility break is expected to be very small. The impacted API
shape made little sense in the absence of ref fields hence it is unlikely customers
created many of these. Experiments running tools to spot this API shape over existing
repositories back up that assertion. The only repository with any significant counts of
this shape is dotnet/runtime  and that is because that repo can create ref fields via
the ByReference<T> intrinsic type.Span<int> CreateSpan (ref int parameter )
{
    // The implementation of this method is irrelevant when considering the  
lifetime of the 
    // returned Span<T>. The ref safe context rules only look at the method  
signature, not the 
    // implementation. In C# 10 ref fields didn't exist hence there was no  
way for `parameter`
    // to escape by ref in this method
}
Span<int> BadUseExamples (int parameter )
{
    // Legal in C# 10 but would be illegal with ref fields
    return CreateSpan( ref parameter);
    // Legal in C# 10 but would be illegal with ref fields
    int local = 42;
    return CreateSpan( ref local);
    // Legal in C# 10 but would be illegal with ref fields
    Span<int> span = stackalloc  int[42];
    return CreateSpan( ref span[0]);
}
Even so the design must account for such APIs existing because it expresses a valid
pattern, just not a common one. Hence the design must give developers the tools to
restore the existing lifetime rules when upgrading to C# 10. Specifically it must provide
mechanisms that allow developers to annotate ref parameters as unable to escape by
ref or ref field. That allows customers to define APIs in C# 11 that have the same C#
10 callsite rules.
A reference assembly for a compilation using features described in this proposal must
maintain the elements that convey ref safe context information. That means all lifetime
annotation attributes must be preserved in their original position. Any attempt to
replace or omit them can lead to invalid reference assemblies.
Representing ref fields is more nuanced. Ideally a ref field would appear in a reference
assembly as would any other field. However a ref field represents a change to the
metadata format and that can cause issues with tool chains that are not updated to
understand this metadata change. A concrete example is C++/CLI which will likely error
if it consumes a ref field. Hence it's advantageous if ref fields can be omitted from
reference assemblies in our core libraries.
A ref field by itself has no impact on ref safe context rules. As a concrete example
consider that flipping the existing Span<T> definition to use a ref field has no impact
on consumption. Hence the ref itself can be omitted safely. However a ref field does
have other impacts to consumption that must be preserved:
A ref struct which has a ref field is never considered unmanaged
The type of the ref field impacts infinite generic expansion rules. Hence if the type
of a ref field contains a type parameter that must be preserved
Given those rules here is a valid reference assembly transformation for a ref struct:
c#Reference Assemblies
// Impl assembly 
ref struct S<T>
{
    ref T _field;
}
// Ref assembly 
ref struct S<T>
{
    object _o; // force managed Lifetimes are most naturally expressed using types. A given program's lifetimes are safe
when the lifetime types type check. While the syntax of C# implicitly adds lifetimes to
values, there is an underlying type system that describes the fundamental rules here. It's
often easier to discuss the implication of changes to the design in terms of these rules
so they are included here for discussion sake.
Note that this is not meant to be a 100% complete documentation. Documenting every
single behavior isn't a goal here. Instead it's meant to establish a general understanding
and common verbiage by which the model, and potential changes to it, can be
discussed.
Usually it's not necessary to directly talk about lifetime types. The exceptions are places
where lifetimes can vary based on particular "instantiation" sites. This is a kind of
polymorphism and we call these varying lifetimes "generic lifetimes", represented as
generic parameters. C# does not provide syntax for expressing lifetime generics, so we
define an implicit "translation" from C# to an expanded lowered language that contains
explicit generic parameters.
The below examples make use of named lifetimes. The syntax $a refers to a lifetime
named a. It is a lifetime that has no meaning by itself but can be given a relationship to
other lifetimes via the where $a : $b syntax. This establishes that $a is convertible to
$b. It may help to think of this as establishing that $a is a lifetime at least as long as $b.
There are a few predefined lifetimes for convenience and brevity below:
$heap: this is the lifetime of any value that exists on the heap. It is available in all
contexts and method signatures.
$local: this is the lifetime of any value that exists on the method stack. It's
effectively a name place holder for function-member . It is implicitly defined in
methods and can appear in method signatures except for any output position.
$ro: name place holder for return only
$cm: name place holder for caller -context
There are a few predefined relationships between lifetimes:
where $heap : $a for all lifetimes $a
where $cm : $ro    T _f; // maintain generic expansion protections
}
Annotationswhere $x : $local for all predefined lifetimes. User defined lifetimes have no
relationship to local unless explicitly defined.
Lifetime variables when defined on types can be invariant or covariant. These are
expressed using the same syntax as generic parameters:
C#
The lifetime parameter $this on type definitions is not predefined but it does have a
few rules associated with it when it is defined:
It must be the first lifetime parameter.
It must be covariant: out $this.
The lifetime of ref fields must be convertible to $this
The $this lifetime of all non-ref fields must be $heap or $this.
The lifetime of a ref is expressed by providing a lifetime argument to the ref. For
example a ref that refers to the heap is expressed as ref<$heap>.
When defining a constructor in the model the name new will be used for the method. It
is necessary to have a parameter list for the returned value as well as the constructor
arguments. This is necessary to express the relationship between constructor inputs and
the constructed value. Rather than having Span<$a><$ro> the model will use Span<$a>
new<$ro> instead. The type of this in the constructor, including lifetimes, will be the
defined return value.
The basic rules for the lifetime are defined as:
All lifetimes are expressed syntactically as generic arguments, coming before type
arguments. This is true for predefined lifetimes except $heap and $local.
All types T that are not a ref struct implicitly have lifetime of T<$heap>. This is
implicit, there is no need to write int<$heap> in every sample.
For a ref field defined as ref<$l0> T<$l1, $l2, ... $ln>:
All lifetimes $l1 through $ln must be invariant.
The lifetime of $l0 must be convertible to $this
For a ref defined as ref<$a> T<$b, ...>, $b must be convertible to $a
The ref of a variable has a lifetime defined by:
For a ref local, parameter, field or return of type ref<$a> T the lifetime is $a// $this is covariant
// $a is invariant
ref struct S<out $this, $a> $heap for all reference types and fields of reference types
$local for everything else
An assignment or return is legal when the underlying type conversion is legal
Lifetimes of expressions can be made explicit by using cast annotations:
(T<$a> expr) the value lifetime is explicitly $a for T<...>
ref<$a> (T<$b>)expr the value lifetime is $b for T<...> and the ref lifetime is
$a.
For the purpose of lifetime rules a ref is considered part of the type of the expression
for purposes of conversions. It is logically represented by converting ref<$a> T<...> to
ref<$a, T<...>> where $a is covariant and T is invariant.
Next let's define the rules that allow us to map C# syntax to the underlying model.
For brevity sake a type which has no explicit lifetime parameters treated as if there is out
$this defined and applied to all fields of the type. A type with a ref field must define
explicit lifetime parameters.
These rules exists to support our existing invariant that T can be assigned to scoped T
for all types. That maps down to T<$a, ...> being assignable to T<$local, ...> for all
lifetimes known to be convertible to $local. Further this supports other items like being
able to assign Span<T> from the heap to those on the stack. This does exclude types
where fields have differing lifetimes for non-ref values but that is the reality of C# today.
Changing that would require a significant change of C# rules that would need to be
mapped out.
The type of this for a type S<out $this, ...> inside an instance method is implicitly
defined as the following:
For normal instance method: ref<$local> S<$cm, ...>
For instance method annotated with [UnscopedRef]: ref<$ro> S<$cm, ...>
The lack of an explicit this parameter forces the implicit rules here. For complex
samples and discussions consider writing as a static method and making this an
explicit parameter.
C#
ref struct S<out $this>
{
    // Implicit this can make discussion confusing 
    void M<$ro, $cm>( ref<$ro> S<$cm> s) {  }
    // Rewrite as explicit this to simplify discussionThe C# method syntax maps to the model in the following ways:
ref parameters have a ref lifetime of $ro
parameters of type ref struct have a this lifetime of $cm
ref returns have a ref lifetime of $ro
returns of type ref struct have a value lifetime of $ro
scoped on a parameter or ref changes the ref lifetime to be $local
Given that let's explore a simple example that demonstrates the model here:
C#
Now let's explore the same example using a ref struct:
C#    static void M<$ro, $cm>( ref<$local> S<$cm> this, ref<$ro> S<$cm> s) { }
}
ref int M1(ref int i) => ...
// Maps to the following. 
ref<$ro> int Identity<$ro>( ref<$ro> int i)
{
    // okay: has ref lifetime $ro which is equal to $ro
    return ref i;
    // okay: has ref lifetime $heap which convertible $ro
    int[] array = new int[42];
    return ref array[0];
    // error: has ref lifetime $local which has no conversion to $a hence 
    // it's illegal
    int local = 42;
    return ref local;
}
ref struct S
{
    ref int Field;
    S(ref int f)
    {
        Field = ref f;
    }
}
S M2(ref int i, S span1, scoped S span2 ) => ...Next let's see how this helps with the cyclic self assignment problem:
C#// Maps to 
ref struct S<out $this>
{
    // Implicitly 
    ref<$this> int Field;
    S<$ro> new<$ro>(ref<$ro> int f)
    {
        Field = ref f;
    }
}
S<$ro> M2<$ro>(
    ref<$ro> int i,
    S<$ro> span1)
    S<$local> span2)
{
    // okay: types match exactly
    return span1;
    // error: has lifetime $local which has no conversion to $ro
    return span2;
    // okay: type S<$heap> has a conversion to S<$ro> because $heap has a
    // conversion to $ro and the first lifetime parameter of S<> is  
covariant
    return default(S<$heap>)
    // okay: the ref lifetime of ref $i is $ro so this is just an 
    // identity conversion
    S<$ro> local = new S<$ro>( ref $i);
    return local;
    int[] array = new int[42];
    // okay: S<$heap> is convertible to S<$ro>
    return new S<$heap>( ref<$heap> array[ 0]);
    // okay: the parameter of the ctor is $ro ref int and the argument is  
$heap ref int. These 
    // are convertible.
    return new S<$ro>( ref<$heap> array[ 0]);
    // error: has ref lifetime $local which has no conversion to $a hence 
    // it's illegal
    int local = 42;
    return ref local;
}Next let's see how this helps with the silly capture parameter problem:
C#ref struct S
{
    int field;
    ref int refField;
    static void SelfAssign (ref S s)
    {
        s.refField = ref s.field;
    }
}
// Maps to 
ref struct S<out $this>
{
    int field;
    ref<$this> int refField;
    static void SelfAssign<$ro, $cm>( ref<$ro> S<$cm> s)
    {
        // error: the types work out here to ref<$cm> int = ref<$ro> int and  
that is 
        // illegal as $ro has no conversion to $cm (the relationship is the  
other direction)
        s.refField = ref<$ro> s.field;
    }
}
ref struct S
{
    ref int refField;
    void Use(ref int parameter )
    {
        // error: this needs to be an error else every call to this.Use(ref  
local) would fail 
        // because compiler would assume the `ref` was captured by ref.
        this.refField = ref parameter;
    }
}
// Maps to 
ref struct S<out $this>
{
    ref<$this> int refField;
    
    // Using static form of this method signature so the type of this is  This design proposes several compatibility breaks with our existing ref-safe-context
rules. Even though the breaks are believed to be minimally impactful significant
consideration was given to a design which had no breaking changes.
The compat preserving design though was significantly more complex than this one. In
order to preserve compat ref fields need distinct lifetimes for the ability to return by
ref and return by ref field. Essentially it requires us to provide ref-field-s afe-c ontext
tracking for all parameters to a method. This needs to be calculated for all expressions
and tracked in all values virtually everywhere that ref-safe-c ontext is tracked today.
Further this value has relationships with ref-safe-c ontext. For example it's non-sensical to
have a value can be returned as a ref field but not directly as ref. That is because ref
fields can be trivially returned by ref already ( ref state in a ref struct can be returned
by ref even when the containing value cannot). Hence the rules further need constant
adjustment to ensure these values are sensible with respect to each other.
Also it means the language needs syntax to represent ref parameters that can be
returned in three different ways: by ref field, by ref and by value. The default being
returnable by ref. Going forward though the more natural return, particularly when ref
struct are involved is expected to be by ref field or ref. That means new APIs require
an extra syntax annotation to be correct by default. This is undesirable.
These compat changes though will impact methods that have the following properties:
Have a Span<T> or ref structexplicit. 
    static void Use<$ro, $cm>( ref<$local> S<$cm> @ this, ref<$ro> int 
parameter)
    {
        // error: the types here are:
        //  - refField is ref<$cm> int
        //  - ref parameter is ref<$ro> int
        // That means the RHS is not convertible to the LHS ($ro is not  
covertible to $cm) and 
        // hence this reassignment is illegal
        @this.refField = ref<$ro> parameter;
    }
}
Open Issues
Change the design to avoid compat breaksWhere the ref struct is a return type, ref or out parameter
Has an additional in or ref parameter (excluding the receiver)
To understand the impact it's helpful to break APIs into categories:
1. Want consumers to account for ref being captured as a ref field. Prime example
is the Span(ref T value) constructors
2. Do not want consumers to account for ref being captured as a ref field. These
though break into two categories
a. Unsafe APIs. These are APIS inside the Unsafe and MemoryMarshal types, of
which MemoryMarshal.CreateSpan is the most prominent. These APIs do capture
the ref unsafely but they are also known to be unsafe APIs.
b. Safe APIs. These are APIs which take ref parameters for efficiency but it is not
actually captured anywhere. Examples are small but one is
AsnDecoder.ReadEnumeratedBytes
This change primarily benefits (1) above. These are expected to make up the majority of
APIs that take a ref and return a ref struct going forward. The changes negatively
impact (2.1) and (2.2) as it breaks the existing calling semantics because the lifetime
rules change.
The APIs in category (2.1) though are largely authored by Microsoft or by developers
who stand the most to benefit from ref fields (the T anner's of the world). It is
reasonable to assume this class of developers would be amenable to a compatibility tax
on upgrade to C# 11 in the form of a few annotations to retain the existing semantics if
ref fields were provided in return.
The APIs in category (2.2) are the biggest issue. It is unknown how many such APIs exist
and it's unclear if these would be more / less frequent in 3rd party code. The
expectation is there is a very small number of them, particularly if we take the compat
break on out. Searches so far have revealed a very small number of these existing in
public surface area. This is a hard pattern to search for though as it requires semantic
analysis. Before taking this change a tool based approach would be needed to verify the
assumptions around this impacting a small number of known cases.
For both cases in category (2) though the fix is straight forward. The ref parameters
that do not want to be considered capturable must add scoped to the ref. In (2.1) this
will likely also force the developer to use Unsafe or MemoryMarshal but that is expected
for unsafe style APIs.
Ideally the language could reduce the impact of silent breaking changes by issuing a
warning when an API silently falls into the troublesome behavior. That would be amethod that both takes a ref, returns ref struct but does not actually capture the ref
in the ref struct. The compiler could issue a diagnostic in that case informing
developers such ref should be annotated as scoped ref instead.
Decision  This design can be achieved but the resulting feature is more difficult to use to
the point the decision was made to take the compat break.
Decision  The compiler will provide a warning when a method meets the criteria but
does not capture the ref parameter as a ref field. This should suitably warn customers
on upgrade about the potential issues they are creating
This design calls for using attributes to annotate the new lifetime rules. This also
could've been done just as easily with contextual keywords. For instance
[DoesNotEscape] could map to scoped. However keywords, even the contextual ones,
generally must meet a very high bar for inclusion. They take up valuable language real
estate and are more prominent parts of the language. This feature, while valuable, is
going to serve a minority of C# developers.
On the surface that would seem to favor not using keywords but there are two
important points to consider:
1. The annotations will effect program semantics. Having attributes impact program
semantics is a line C# is reluctant to cross and it's unclear if this is the feature that
should justify the language taking that step.
2. The developers most likely to use this feature intersect strongly with the set of
developers that use function pointers. That feature, while also used by a minority
of developers, did warrant a new syntax and that decision is still seen as sound.
Taken together this means syntax should be considered.
A rough sketch of the syntax would be:
[RefDoesNotEscape] maps to scoped ref
[DoesNotEscape] maps to scoped
[RefDoesEscape] maps to unscoped
Decision  Use syntax for scoped and scoped ref; use attribute for unscoped.Keywords vs. attributes
Allow fixed buffer localsThis design allows for safe fixed buffers that can support any type. One possible
extension here is allowing such fixed buffers to be declared as local variables. This
would allow a number of existing stackalloc operations to be replaced with a fixed
buffer. It would also expand the set of scenarios we could have stack style allocations as
stackalloc is limited to unmanaged element types while fixed buffers are not.
c#
This holds together but does require us to extend the syntax for locals a bit. Unclear if
this is or isn't worth the extra complexity. P ossible we could decide no for now and bring
back later if sufficient need is demonstrated.
Example of where this would be beneficial:
https://github.com/dotnet/runtime/pull/34149
Decision  hold off on this for now
A decision needs to be made if methods marked with new lifetime attributes should or
should not translate to modreq in emit. There would be effectively a 1:1 mapping
between annotations and modreq if this approach was taken.
The rationale for adding a modreq is the attributes change the semantics of ref safe
context rules. Only languages which understand these semantics should be calling the
methods in question. Further when applied to OHI scenarios, the lifetimes become a
contract that all derived methods must implement. Having the annotations exist without
modreq can lead to situations where virtual method chains with conflicting lifetime
annotations are loaded (can happen if only one part of virtual chain is compiled and
other is not).
The initial ref safe context work did not use modreq but instead relied on languages and
the framework to understand. At the same time though all of the elements that
contribute to the ref safe context rules are a strong part of the method signature: ref,class FixedBufferLocals
{
    void Example()
    {
        Span<int> span = stackalloc  int[42];
        int buffer[ 42];
    }
}
To use modreqs or notin, ref struct, etc ... Hence any change to the existing rules of a method already
results in a binary change to the signature. T o give the new lifetime annotations the
same impact they will need modreq enforcement.
The concern is whether or not this is overkill. It does have the negative impact that
making signatures more flexible, by say adding [DoesNotEscape] to a parameter, will
result in a binary compat change. That trade off means that over time frameworks like
BCL likely won't be able to relax such signatures. It could be mitigated to a degree by
taking some approach the language does with in parameters and only apply modreq in
virtual positions.
Decision  Do not use modreq in metadata. The difference between out and ref is not
modreq but they now have different ref safe context values. There is no real benefit to
only half enforcing the rules with modreq here.
Should the design for fixed buffers be extended to include multi-dimensional style
arrays? Essentially allowing for declarations like the following:
c#
Decision  Do not allow for now
The runtime repository has several non-public APIs that capture ref parameters as ref
fields. These are unsafe because the lifetime of the resulting value is not tracked. For
example the Span<T>(ref T value, int length) constructor.
The majority of these APIs will likely choose to have proper lifetime tracking on the
return which will be achieved simply by updating to C# 11. A few though will want to
keep their current semantics of not tracking the return value because their entire intent
is to be unsafe. The most notable examples are MemoryMarshal.CreateSpan and
MemoryMarshal.CreateReadOnlySpan. This will be achieved by marking the parameters as
scoped.Allow multi-dimensional fixed buffers
struct Dimensions
{
    int array[42, 13];
}
Violating scopedThat means the runtime needs an established pattern for unsafely removing scoped
from a parameter:
1. Unsafe.AsRef<T>(in T value) could expand its existing purpose by changing to
scoped in T value. This would allow it to both remove in and scoped from
parameters. It then becomes the universal "remove ref safety" method
2. Introduce a new method whose entire purpose is to remove scoped: ref T
Unsafe.AsUnscoped<T>(scoped in T value). This removes in as well because if it
did not then callers still need a combination of method calls to "remove ref safety"
at which point the existing solution is likely sufficient.
The design only has two locations which are scoped by default:
this is scoped ref
out is scoped ref
The decision on out is to significantly reduce the compat burden of ref fields and at
the same time is a more natural default. It lets developers actually think of out as data
flowing outward only where as if it's ref then the rules must consider data flowing in
both directions. This leads to significant developer confusion.
The decision on this is undesirable because it means a struct cannot return a field by
ref. This is an important scenario to high perf developers and the [UnscopedRef]
attribute was added essentially for this one scenario.
Keywords have a high bar and adding it for a single scenario is suspect. As such thought
was given to whether we could avoid this keyword at all by making this simply ref by
default and not scoped ref. All members that need this to be scoped ref could do so
by marking the method scoped (as a method can be marked readonly to create a
readonly ref today).
On a normal struct this is mostly a positive change as it only introduces compat issues
when a member has a ref return. There are very few of these methods and a tool could
spot these and convert them to scoped members quickly.
On a ref struct this change introduces significantly bigger compat issues. Consider the
following:
c#Unscoped this by default?Essentially it would mean all instance method invocations on mutable ref struct locals
would be illegal unless the local was further marked as scoped. The rules have to
consider the case where fields were ref reassigned to other fields in this. A readonly
ref struct doesn't have this problem because the readonly nature prevents ref
reassignment. S till this would be a significant back compat breaking change as it would
impact virtually every existing mutable ref struct.
A readonly ref struct though is still problematic once we expand to having ref fields
to ref struct. It allows for the same basic problem by just moving the capture into the
value of the ref field:
c#ref struct Sneaky
{
    int Field;
    ref int RefField;
    public void SelfAssign ()
    {
        // This pattern of ref reassign to fields on this inside instance  
methods is now
        // completely legal.
        RefField = ref Field;
    }
    static Sneaky UseExample ()
    {
        Sneaky local = default;
        // Error: this is illegal, and must be illegal, by our existing  
rules as the 
        // ref-safe-context of local is now an input into method arguments  
must match. 
        local.SelfAssign();
        // This would be dangerous as local now has a dangerous `ref` but  
the above 
        // prevents us from getting here.
        return local;
    }
}
readonly  ref struct ReadOnlySneaky
{
    readonly  int Field;
    readonly  ref ReadOnlySpan< int> Span;
    public void SelfAssign ()Some thought was given to the idea of having this have different defaults based on
the type of struct or member. For example:
this as ref: struct, readonly ref struct or readonly member
this as scoped ref: ref struct or readonly ref struct with ref field to ref
struct
This minimizes compat breaks and maximizes flexibility but at the cost of complicating
the story for customers. It also doesn't fully solve the problem because future features,
like safe fixed buffers, require that a mutable ref struct have ref returns for fields
which don't work by this design alone as it would fall into the scoped ref category.
Decision  Keep this as scoped ref
This feature opens up a new set of ref safe context rules because it allows for a ref field
to refer to a ref struct. This generic nature of ByReference<T> meant that up until now
the runtime could not have such a construct. As a result all of our rules are written under
the assumption this is not possible. The ref field feature is largely not about making
new rules but codifying the existing rules in our system. Allowing ref fields to ref
struct requires us to codify new rules because there are several new scenarios to
consider.
The first is that a readonly ref is now capable of storing ref state. For example:
c#    {
        // Instance method captures a ref to itself
        Span = new ReadOnlySpan< int>(ref Field, 1);
    }
}
ref fields to ref struct
readonly  ref struct Container
{
    readonly  ref Span<int> Span;
    void Store(Span<int> span)
    {
        Span = span;
    }
}This means when thinking about method arguments must match rules we must consider
readonly ref T is potential method output when T potentially has a ref field to a ref
struct.
The second issue is language must consider a new type of safe context: ref-field-s afe-
context. All ref struct which transitively contain a ref field have another escape scope
representing the value(s) in the ref field(s). In the case of multiple ref fields they can
be collectively tracked as a single value. The default value for this for parameters is
caller -context.
c#
This value is not related to the safe-c ontext of the container; that is as the container
context gets smaller it has no impact on the ref-field-s afe-c ontext of the ref field values.
Further the ref-field-s afe-c ontext can never be smaller than the safe-c ontext of the
container.
c#ref struct Nested
{
    ref Span<int> Span;
}
Span<int> M(ref Nested nested ) => nested.Span;
ref struct Nested
{
    ref Span<int> Span;
}
void M(ref Nested nested )
{
    scoped ref Nested refLocal = ref nested;
    // the ref-field-safe-context of local is still *caller-context* which  
means the following
    // is illegal
    refLocal.Span = stackalloc  int[42];
    scoped Nested valLocal = nested;
    // the ref-field-safe-context of local is still *caller-context* which  
means the following
    // is still illegal
    valLocal.Span = stackalloc  int[42];
}This ref-field-s afe-c ontext has essentially always existed. Up until now ref fields could
only point to normal struct hence it was trivially collapsed to caller -context. To support
ref fields to ref struct our existing rules need to be updated to take into account this
new ref-safe-c ontext.
Third the rules for ref reassignment need to be updated to ensure that we don't violate
ref-field-c ontext for the values. Essentially for x.e1 = ref e2 where the type of e1 is a
ref struct the ref-field-s afe-c ontext must be equal.
These problems are very solvable. The compiler team has sketched out a few versions of
these rules and they largely fall out from our existing analysis. The problem is there is no
consuming code for such rules that helps prove out there correctness and usability. This
makes us very hesitant to add support because of the fear we'll pick wrong defaults and
back the runtime into usability corner when it does take advantage of this. This concern
is particularly strong because .NET 8 likely pushes us in this direction with allow T: ref
struct and Span<Span<T>>. The rules would be better written if it's done in conjunction
with consumption code.
Decision  Delay allowing ref field to ref struct until .NET 8 where we have scenarios
that will help drive the rules around these scenarios.
The features outlined in this document don't need to be implemented in a single pass.
Instead they can be implemented in phases across several language releases in the
following buckets:
1. ref fields and scoped
2. [UnscopedRef]
3. ref fields to ref struct
4. Sunset restricted types
5. fixed sized buffers
What gets implemented in which release is merely a scoping exercise.
Decision  Only (1) and (2) made C# 11.0. The rest will be considered in future versions of
C#.What will make C# 11.0?
Future Considerations
Advanced lifetime annotationsThe lifetime annotations in this proposal are limited in that they allow developers to
change the default escape / don't escape behavior of values. This does add powerful
flexibility to our model but it does not radically change the set of relationships that can
be expressed. At the core the C# model is still effectively binary: can a value be returned
or not?
That allows limited lifetime relationships to be understood. For example a value that
can't be returned from a method has a smaller lifetime than one that can be returned
from a method. There is no way to describe the lifetime relationship between values that
can be returned from a method though. Specifically there is no way to say that one
value has a larger lifetime than the other once it's established both can be returned
from a method. The next step in our lifetime evolution would be allowing such
relationships to be described.
Other methods such as Rust allow this type of relationship to be expressed and hence
can implement handle more complex scoped style operations. Our language could
similarly benefit if such a feature were included. At the moment there is no motivating
pressure to do this but if there is in the future our scoped model could be expanded to
included it in a fairly straight forward fashion.
Every scoped could be assigned a named lifetime by adding a generic style argument to
the syntax. For example scoped<'a> is a value that has lifetime 'a. Constraints like
where could then be used to describe the relationships between these lifetimes.
c#
This method defines two lifetimes 'a and 'b and there relationship, specifically that 'b
is greater than 'a. This allows for the callsite to have more granular rules for how values
can be safely passed into methods vs. the more coarse grained rules present today.
The following issues are all related to this proposal:void M(scoped<'a> ref MyStruct s, scoped<' b> Span< int> span)
  where 'b >= 'a
{
    s.Span = span;
}
Related Information
Issueshttps://github.com/dotnet/csharplang/issues/1130
https://github.com/dotnet/csharplang/issues/1147
https://github.com/dotnet/csharplang/issues/992
https://github.com/dotnet/csharplang/issues/1314
https://github.com/dotnet/csharplang/issues/2208
https://github.com/dotnet/runtime/issues/32060
https://github.com/dotnet/runtime/issues/61135
https://github.com/dotnet/csharplang/discussions/78
The following proposals are related to this proposal:
https://github.com/dotnet/csharplang/blob/725763343ad44a9251b03814e6897d8
7fe553769/proposals/fixed-sized-buffers.md
Utf8JsonR eader
This particular snippet requires unsafe because it runs into issues with passing around a
Span<T> which can be stack allocated to an instance method on a ref struct. Even
though this parameter is not captured the language must assume it is and hence
needlessly causes friction here.
Utf8JsonWriter
This snippet wants to mutate a parameter by escaping elements of the data. The
escaped data can be stack allocated for efficiency. Even though the parameter is not
escaped the compiler assigns it a safe-c ontext of outside the enclosing method because
it is a parameter. This means in order to use stack allocation the implementation must
use unsafe in order to assign back to the parameter after escaping the data.
c#
Proposals
Existing samples
Fun Samples
ReadOnlySpan<T>
public readonly  ref struct ReadOnlySpan<T>
{
    readonly  ref readonly  T _value;c#
Below are a set of examples demonstrating how and why the rules work the way they
do. Included are several examples showing dangerous behaviors and how the rules
prevent them from happening. It's important to keep these in mind when making
adjustments to the proposal.    readonly  int _length;
    public ReadOnlySpan (in T value)
    {
        _value = ref value;
        _length = 1;
    }
}
Frugal list
struct FrugalList<T>
{
    private T _item0;
    private T _item1;
    private T _item2;
    public int Count = 3;
    public FrugalList (){}
    public ref T this[int index]
    {
        [UnscopedRef ] get
        {
            switch (index)
            {
                case 0: return ref _item0;
                case 1: return ref _item1;
                case 2: return ref _item2;
                default: throw null;
            }
        }
    }
}
Examples and Notes
Ref reassignment and call sitesDemonstrating how ref reassignment  and method invocation  work together.
c#
ref struct RS
{
    ref int _refField;
    public ref int Prop => ref _refField;
    public RS(int[] array )
    {
        _refField = ref array[0];
    }
    public RS(ref int i)
    {
        _refField = ref i;
    }
    public RS CreateRS () => ...;
    public ref int M1(RS rs)
    {
        // The call site arguments for Prop contribute here:
        //   - `rs` contributes no ref-safe-context as the corresponding  
parameter, 
        //      which is `this`, is `scoped ref`
        //   - `rs` contribute safe-context of *caller-context*
        // 
        // This is an lvalue invocation and the arguments contribute only  
safe-context 
        // values of *caller-context*. That means `local1` has ref-safe-
context of 
        // *caller-context*
        ref int local1 = ref rs.Prop;
        // Okay: this is legal because `local` has ref-safe-context of  
*caller-context*
        return ref local1;
        // The arguments contribute here:
        //   - `this` contributes no ref-safe-context as the corresponding  
parameter
        //     is `scoped ref`
        //   - `this` contributes safe-context of *caller-context*
        //
        // This is an rvalue invocation and following those rules the safe-
context of 
        // `local2` will be *caller-context*
        RS local2 = CreateRS();
        // Okay: this follows the same analysis as `ref rs.Prop` above
        return ref local2.Prop;The reason for the following line in the ref reassignment rules  may not be obvious at
first glance:
e1 must have the same safe-c ontext as e2
This is because the lifetime of the values pointed to by ref locations are invariant. The
indirection prevents us from allowing any kind of variance here, even to narrower
lifetimes. If narrowing is allowed then it opens up the following unsafe code:
C#        // The arguments contribute here:
        //   - `local3` contributes ref-safe-context of *function-member*
        //   - `local3` contributes safe-context of *caller-context*
        // 
        // This is an rvalue invocation which returns a `ref struct` and  
following those 
        // rules the safe-context of `local4` will be *function-member*
        int local3 = 42;
        var local4 = new RS(ref local3);
        // Error: 
        // The arguments contribute here:
        //   - `local4` contributes no ref-safe-context as the corresponding  
parameter
        //     is `scoped ref`
        //   - `local4` contributes safe-context of *function-member*
        // 
        // This is an lvalue invocation and following those rules the ref-
safe-context 
        // of the return is *function-member*
        return ref local4.Prop;
    }
}
Ref reassignment and unsafe escapes
void Example(ref Span<int> p)
{
    Span<int> local = stackalloc  int[42];
    ref Span<int> refLocal = ref local;
    // The safe-context of refLocal is narrower than p. For a non-ref  
reassignment 
    // this would be allowed as its safe to assign wider lifetimes to  
narrower ones.
    // In the case of ref reassignment though this rule prevents it as the 
    // safe-context values are different.For a ref to non ref struct this rule is trivially satisfied as the values all have the same
safe-c ontext. This rule really only comes into play when the value is a ref struct.
This behavior of ref will also be important in a future where we allow ref fields to ref
struct.
The use of scoped on locals will be particularly helpful to code patterns which
conditionally assign values with different safe-c ontext to locals. It means code no longer
needs to rely on initialization tricks like = stackalloc byte[0] to define a local safe-
context but now can simply use scoped.
c#
This pattern comes up frequently in low level code. When the ref struct involved is
Span<T> the above trick can be used. It is not applicable to other ref struct types
though and can result in low level code needing to resort to unsafe to work around the
inability to properly specify the lifetime.    refLocal = ref p;
    // If it were allowed this would be legal as the safe-context of  
refLocal
    // is *caller-context* and that is satisfied by stackalloc. At the same  
time
    // it would be assigning through p and escaping the stackalloc to the  
calling
    // method
    // 
    // This is equivalent of saying p = stackalloc int[13]!!! 
    refLocal = stackalloc  int[13];
}
scoped locals
// Old way 
// Span<byte> span = stackalloc byte[0];
// New way 
scoped Span< byte> span;
int len = ...;
if (len < MaxStackLen)
{
    span = stackalloc  byte[len];
}
else
{
    span = new byte[len];
}One source of repeated friction in low level code is the default escape for parameters is
permissive. They are safe-c ontext to the caller -context. This is a sensible default because
it lines up with the coding patterns of .NET as a whole. In low level code though there is
a larger use of ref struct and this default can cause friction with other parts of the ref
safe context rules.
The main friction point occurs because of the method arguments must match  rule.
This rule most commonly comes into play with instance methods on ref struct where
at least one parameter is also a ref struct. This is a common pattern in low level code
where ref struct types commonly leverage Span<T> parameters in their methods. For
example it will occur on any writer style ref struct that uses Span<T> to pass around
buffers.
This rule exists to prevent scenarios like the following:
c#
Essentially this rule exists because the language must assume that all inputs to a method
escape to their maximum allowed safe-c ontext. When there are ref or out parameters,
including the receivers, it's possible for the inputs to escape as fields of those ref values
(as happens in RS.Set above).
In practice though there are many such methods which pass ref struct as parameters
that never intend to capture them in output. It is just a value that is used within the
current method. For example:scoped parameter values
ref struct RS
{
    Span<int> _field;
    void Set(Span<int> p)
    {
        _field = p;
    }
    static void DangerousCode (ref RS p)
    {
        Span<int> span = stackalloc  int[] { 42 };
        // Error: if allowed this would let the method return a reference to  
        // the stack
        p.Set(span);
    }
}c#
In order to work around this low level code will resort to unsafe tricks to lie to the
compiler about the lifetime of their ref struct. This significantly reduces the value
proposition of ref struct as they are meant to be a means to avoid unsafe while
continuing to write high performance code.
This is where scoped is an effective tool on ref struct parameters because it removes
them from consideration as being returned from the method according to the updated
method arguments must match rule . A ref struct parameter which is consumed, but
never returned, can be labeled as scoped to make call sites more flexible.
c#ref struct JsonReader
{
    Span<char> _buffer;
    int _position;
    internal  bool TextEquals (ReadOnlySpan< char> text)
    {
        var current = _buffer.Slice(_position, text.Length);
        return current == text;
    }
}
class C
{
    static void M(ref JsonReader reader )
    {
        Span<char> span = stackalloc  char[4];
        span[0] = 'd';
        span[1] = 'o';
        span[2] = 'g';
        // Error: The safe-context of `span` is function-member 
        // while `reader` is outside function-member hence this fails
        // by the above rule.
        if (reader.TextEquals(span))
        {
            ...
        }
    }
}
ref struct JsonReader
{
    Span<char> _buffer;
    int _position;When a ref is taken to a readonly field in a constructor or init member the type is
ref not ref readonly. This is a long standing behavior that allows for code like the
following:
c#
That does pose a potential problem though if such a ref were able to be stored into a
ref field on the same type. It would allow for direct mutation of a readonly struct
from an instance member:    internal  bool TextEquals (scoped ReadOnlySpan< char> text)
    {
        var current = _buffer.Slice(_position, text.Length);
        return current == text;
    }
}
class C
{
    static void M(ref JsonReader reader )
    {
        Span<char> span = stackalloc  char[4];
        span[0] = 'd';
        span[1] = 'o';
        span[2] = 'g';
        // Okay: the compiler never considers `span` as capturable here  
hence it doesn't
        // contribute to the method arguments must match rule
        if (reader.TextEquals(span))
        {
            ...
        }
    }
}
Preventing tricky ref assignment from readonly mutation
struct S
{
    readonly  int i; 
    public S(string s)
    {
        M(ref i);
    }
    static void M(ref int i) { }
}c#
The proposal prevents this though because it violates the ref safe context rules.
Consider the following:
The ref-safe-c ontext of this is function-member  and safe-c ontext is caller -context.
These are both standard for this in a struct member.
The ref-safe-c ontext of i is function-member . This falls out from the field lifetimes
rules . Specifically rule 4.
At that point the line r = ref i is illegal by ref reassignment rules .
These rules were not intended to prevent this behavior but do so as a side effect. It's
important to keep this in mind for any future rule update to evaluate the impact to
scenarios like this.
One aspect this design struggled with is how freely a ref can be returned from a
method. Allowing all ref to be returned as freely as normal values is likely what most
developers intuitively expect. However it allows for pathological scenarios that the
compiler must consider when calculating ref safety. Consider the following:
c#readonly  ref struct S
{ 
    readonly  int i; 
    readonly  ref int r; 
    public S()
    {
        i = 0;
        r = ref i;
    }
    public void Oops()
    {
        r++;
    }
Silly cyclic assignment
ref struct S
{
    int field;
    ref int refField;
    static void SelfAssign (ref S s)
    {This is not a code pattern that we expect any developers to use. Y et when a ref can be
returned with the same lifetime as a value it is legal under the rules. The compiler must
consider all legal cases when evaluating a method call and this leads to such APIs being
effectively unusable.
c#
To make these APIs usable the compiler ensures that the ref lifetime for a ref
parameter is smaller than lifetime of any references in the associated parameter value.
This is the rationale for having ref-safe-c ontext for ref to ref struct be return-only  and
out be caller -context. That prevents cyclic assignment because of the difference in
lifetimes.
It is also why [UnscopedRef] only promotes the ref-safe-c ontext of any ref to ref
struct values to return-only  and not caller -context. Consider that using caller -context
allows for cyclic assignment and would force a viral use of [UnscopedRef] for a ref
struct:
c#        s.refField = ref s.field;
    }
}
void M(ref S s)
{
    ...
}
void Usage()
{
    // safe-context to caller-context
    S local = default; 
    // Error: compiler is forced to assume the worst and concludes a self  
assignment
    // is possible here and must issue an error.
    M(ref local);
}
ref struct S
{
    byte Field;
    [UnscopedRef ]
    public Span<byte> Data => new Span<byte>(ref Field, 1);
}This is correctly illegal in that case because the compiler has to consider the
pathological case that S.Data could cyclic assign via this. That forces methods all
methods that call S.Data to further mark their ref parameters as [UnscopedRef]. This is
viral until the method which creates the value as a local. This is why return-only  exists as
a safe-c ontext. It does complicate the spec / implementation but it serves to make the
feature significantly more usable.
Note: this cyclic assignment problem does continue to exist for [UnscopedRef] out to
ref struct because that causes the safe-c ontext and ref-safe-c ontext to be equivalent.
c#
In terms of advanced annotations the [UnscopedRef] design creates the following:void M(ref S s)
{
    // Error: passing a scoped ref to [UnscopedRef] ref 
    Span<byte> span = s.Data;
}
ref struct RS
{
    int field;
    ref int refField;
}
void M1(out RS p)
{
    // Error: from method arguments must match:
    // Step 1 would calculate the narrowest escape as *caller-context*
    // Step 2 would fail the assignment check because p has safe-context of  
*return-only*
    M2(out p);
}
void M2([UnscopedRef] out RS p)
{
    // The lifetimes of LHS and RHS are equivalent here and hence this is  
legal
    p.refField = ref p.Field;
}
ref struct S { }
// C# code
S Create1(ref S p)Consider the below code sample:
c#
When designing the rules for ref fields on readonly instances in a vacuum the rules can
be validly designed such that the above is legal or illegal. Essentially readonly can
validly be deep through a ref field or it can apply only to the ref. Applying only to the
ref prevents ref reassignment but allows normal assignment which changes the
referred to value.
This design does not exist in a vacuum though, it is designing rules for types that
already effectively have ref fields. The most prominent of which, Span<T>, already has a
strong dependency on readonly not being deep here. Its primary scenario is the ability
to assign to the ref field through a readonly instance.
c#S Create2([UnscopedRef] ref S p)
// Annotation equivalent
scoped<'b> S Create1(scoped<'a> ref scoped<'b> S)
scoped<'a> S Create2(scoped<'a> ref scoped<'b> S)
  where 'b >= 'a
readonly cannot be deep through ref fields
ref struct S
{
    ref int Field;
    readonly  void Method()
    {
        // Legal or illegal?
        Field = 42;
    }
}
readonly  ref struct SpanOfOne
{
    readonly  ref int Field;
    public ref int this[int index]
    {
        get
        {
            if (index != 1)
                throw new Exception();This means we must choose the shallow interpretation of readonly.
One subtle design question is: How are constructors bodies modeled for ref safety?
Essentially how is the following constructor analyzed?
c#
There are roughly two approaches:
1. Model as a static method where this is a local where its safe-c ontext is caller -
context
2. Model as a static method where this is an out parameter.
Further a constructor must meet the following invariants:
1. Ensure that ref parameters can be captured as ref fields.
2. Ensure that ref to fields of this cannot be escaped through ref parameters. That
would violate tricky ref assignment .
The intent is to pick the form that satisfies our invariants without introduction of any
special rules for constructors. Given that the best model for constructors is viewing this
as an out parameter. The return only  nature of the out allows us to satisfy all the
invariants above without any special casing:
c#            return ref Field;
        }
    }
}
Modeling constructors
ref struct S
{
    int field;
    public S(ref int f)
    {
        field = ref f;
    }
}
public static void ctor(out S @this, ref int f)
{
    // The ref-safe-context of `ref f` is *return-only* which is also the The method arguments must match rule is a common source of confusion for
developers. It's a rule which has a number of special cases that are hard to understand
unless you are familiar with the reasoning behind the rule. For the sake of better
understanding the reasons for the rule we will simplify ref-safe-c ontext and safe-c ontext
to simply context.
Methods can pretty liberally return state passed to them as parameters. Essentially any
reachable state which is unscoped can be returned (including returning by ref). This
can be returned directly through a return statement or indirectly by assigning into a
ref value.
Direct returns don't pose much problems for ref safety. The compiler simply needs to
look at all the returnable inputs to a method and then it effectively restricts the return
value to be the minimum context of the input. That return value then goes through
normal processing.
Indirect returns pose a significant problem because all ref are both an input and output
to the method. These outputs already have a known context. The compiler can't infer
new ones, it has to consider them at their current level. That means the compiler has to
look at every single ref which is assignable in the called method, evaluate it's context,
and then verify no returnable input to the method has a smaller context than that ref. If
any such case exists then the method call must be illegal because it could violate ref
safety.
Method arguments must match is the process by which the compiler asserts this safety
check.
A different way to evaluate this which is often easier for developers to consider is to do
the following exercise:
1. Look at the method definition identify all places where state can be indirectly
returned: a. Mutable ref parameters pointing to ref struct b. Mutable ref
parameters with ref assignable ref fields c. Assignable ref params or ref fields
pointing to ref struct (consider recursively)
2. Look at the call site a. Identify the contexts that line up with the locations identified
above b. Identify the contexts of all inputs to the method that are returnable (don't    // safe-context of `this.field` hence this assignment is allowed
    @this.field = ref f;
}
Method arguments must matchline up with scoped parameters)
If any value in 2.b is smaller than 2.a then the method call must be illegal. Let's look at a
few examples to illustrate the rules:
c#
Looking at the call to F0 lets go through (1) and (2). The parameters with potential for
indirect return are a and b as both can be directly assigned. The arguments which line
up to those parameters are:
a which maps to x that has context of caller -context
b which maps to y that has with context of function-member
The set of returnable input to the method are
x with escape-s cope of caller -context
ref x with escape-s cope of caller -context
y with escape-s cope of function-member
The value ref y is not returnable since it maps to a scoped ref hence it is not
considered an input. But given that there is at least one input with a smaller escape
scope (y argument) than one of the outputs ( x argument) the method call is illegal.
A different variation is the following:
c#ref struct R { }
class Program
{
    static void F0(ref R a, scoped ref R b) => throw null;
    static void F1(ref R x, scoped R y )
    {
        F0(ref x, ref y);
    }
}
ref struct R { }
class Program
{
    static void F0(ref R a, ref int b) => throw null;
    static void F1(ref R x)Again the parameters with potential for indirect return are a and b as both can be
directly assigned. But b can be excluded because it does not point to a ref struct
hence cannot be used to store ref state. Thus we have:
a which maps to x that has context of caller -context
The set of returnable input to the method are:
x with context of caller -context
ref x with context of caller -context
ref y with context of function-member
Given that there is at least one input with a smaller escape s cope (ref y argument) than
one of the outputs ( x argument) the method call is illegal.
This is the logic that the method arguments must match rule is trying to encompass. It
goes further as it considers both scoped as a way to remove inputs from consideration
and readonly as a way to remove ref as an output (can't assign into a readonly ref so
it can't be a source of output). These special cases do add complexity to the rules but it's
done so for the benefit of the developer. The compiler seeks to remove all inputs and
outputs it knows can't contribute to the result to give developers maximum flexibility
when calling a member. Much like overload resolution it's worth the effort to make our
rules more complex when it creates more flexibility for consumers.
Related to Infer safe-c ontext of declaration expressions .
C#    {
        int y = 42;
        F0(ref x, ref y);
    }
}
Examples of inferred s a f e -c o n t e x t of declaration expressions
ref struct RS
{
    public RS(ref int x) { } // assumed to be able to capture 'x'
    static void M0(RS input, out RS output ) => output = input;
    static void M1()
    {
        var i = 0;Note that the local context which results from the scoped modifier is the narrowest
which could possibly be used for the variable--to be any narrower would mean the
expression refers to variables which are only declared in a narrower context than the
expression.        var rs1 = new RS(ref i); // safe-context of 'rs1' is function-member
        M0(rs1, out var rs2); // safe-context of 'rs2' is function-member
    }
    static void M2(RS rs1)
    {
        M0(rs1, out var rs2); // safe-context of 'rs2' is function-member
    }
    static void M3(RS rs1)
    {
        M0(rs1, out scoped var rs2); // 'scoped' modifier forces safe-
context of 'rs2' to the current local context (function-member or narrower).
    }
}
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackExtended nameof scope
Article •06/23/2023
Allow nameof(parameter) inside an attribute on a method or parameter. For example:
[MyAttribute(nameof(parameter))] void M(int parameter) { }
[MyAttribute(nameof(TParameter))] void M<TParameter>() { }
void M(int parameter, [MyAttribute(nameof(parameter))] int other) { }
Attributes like NotNullWhen or CallerExpression need to refer to parameters, but those
parameters are currently not in scope.
Methods
The method's type_p aramet ers are in scope throughout the method_declar ation , and can
be used to form types throughout that scope in return_type , method_body , and
type_p aramet er_constr aints_claus es but not in attributes, except within a nameof
expression in attr ibut es.
Method parameters
A method declaration creates a separate declaration space for parameters, type
parameters and local variables. Names are introduced into this declaration space by the７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Detailed design
type parameter list and the formal parameter list of the method and by local variable
declarations in the block of the method. Names ar e intr oduced int o this declaration
space by the type p aramet er list and the formal p aramet er list o f the method in
nameof expr essions in attribut es placed on the method or its p aramet ers.
[...] 
Within the block of a method, formal parameters can be referenced by their identifiers
in simple_name expressions (Simple names). Within a nameof expr ession in attribut es
placed on the method or its p aramet ers, formal p aramet ers can be r eferenced by
their identifier s in simple_name  expr essions.
Anonymous function signatures
The scope of the parameters of the anonymous function is the
anonymous_function_body (§7.7) and nameof expr essions in attribut es placed on the
anonymous function or its p aramet ers.
Delegate declarations
The scope o f the p aramet ers of the delegat e is nameof expr essions in attribut es
placed on the declaration, its type p aramet ers or its p aramet ers.
Simple names
A simple_name  is either of the form I or of the form I<A1,...,Ak>, where I is a single
identifier and <A1,...,Ak> is an optional type_ar gument_list . When no
type_ar gument_list  is specified, consider K to be zero. The simple_name  is evaluated and
classified as follows:
If K is zero and the simple_name  appears within a block and if the block's (or an
enclosing block's) local variable declaration space (Declarations) contains a local
variable, parameter or constant with name I, then the simple_name  refers to that
local variable, parameter or constant and is classified as a variable or value.
If K is zero and the simple_name  appears within the body of a generic method
declaration and if that declaration includes a type parameter with name I, then
the simple_name  refers to that type parameter.
If K is zer o and the simple_name  appear s within a nameof expr ession in an
attribut e on the method declaration or its p aramet ers and if that declaration
includes a p aramet er or type p aramet er with name I, then the simple_name
refers to that p aramet er or type p aramet er.
Otherwise, for each instance type T (The instance type), starting with the instance
type of the immediately enclosing type declaration and continuing with the
instance type of each enclosing class or struct declaration (if any):  
[...]
Otherwise, for each namespace N, starting with the namespace in which the
simple_name  occurs, continuing with each enclosing namespace (if any), and
ending with the global namespace, the following steps are evaluated until an entity
is located:  
[...]
Otherwise, the simple_name is undefined and a compile-time error occurs.
Scopes
The scope of a type parameter declared by a type_parameter_list on a
method_declaration is [...] and nameof expr essions in an attribut e on the method
declaration or its p aramet ers.
The scope of a parameter declared in a method_declaration (Methods) is the
method_body  of that method_declaration and nameof expr essions in an attribut e
on the method declaration or its p aramet ers.
Declarations
Related spec sections
File-local types
Article •06/23/2023
Permit a file modifier on top-level type declarations. The type only exists in the file
where it is declared.
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
// File1.cs
namespace  NS;
file class Widget
{
}
// File2.cs
namespace  NS;
file class Widget // different symbol than the Widget in File1
{
}
// File3.cs
using NS;
var widget = new Widget(); // error: The type or namespace name 'Widget'  
could not be found.
MotivationOur primary motivation is from source generators. Source generators work by adding
files to the user's compilation.
1. Those files should be able to contain implementation details which are hidden
from the rest of the compilation, yet are usable throughout the file they are
declared in.
2. We want to reduce the need for generators to "search" for type names which won't
collide with declarations in user code or code from other generators.
We add the file modifier to the following modifier sets:
class
struct
interface
enum
delegate
record
record struct.
The file modifier can only be used on a top-level type.
When a type has the file modifier, it is said to be a file-local  type.
No accessibility modifiers can be used in combination with file on a type. file is
treated as an independent concept from accessibility. Since file-local types can't be
nested, only the default accessibility internal is usable with file types.
C#
The implementation guarantees that file-local types in different files with the same
name will be distinct to the runtime. The type's accessibility and name in metadata is
implementation-defined. The intention is to permit the compiler to adopt any future
access-limitation features in the runtime which are suited to the feature. It's expectedDetailed design
Accessibility
public file class C1 { } // error
internal  file class C2 { } // error
file class C3 { } // ok
Namingthat in the initial implementation, an internal accessibility would be used and an
unspeakable generated name will be used which depends on the file the type is
declared in.
We amend the member lookup  section as follows (new text in bold ):
Next, if K is zero, all nested types whose declarations include type parameters
are removed. If K is not zero, all members with a different number of type
parameters are removed. When K is zero, methods having type parameters are
not removed, since the type inference process ( §11.6.3 ) might be able to
infer the type arguments.
Next, let F be the compilation unit which contains the expr ession wher e
member lookup is occurring. All member s which ar e file-local types and ar e
not declar ed in F are remov ed fr om the set.
Next, if the set o f accessible member s contains file-local types, all member s
which ar e not file-local types ar e remov ed fr om the set.
These rules disallow usage of file-local types outside the file in which they are declared.
These rules also permit a file-local type to shado w a namespace or a non-file-local type:
C#
C#Lookup
Remarks
// File1.cs
class C
{
    public static void M() { }
}
// File2.cs
file class C
{
    public static void M() { }
}
class Program
{
    static void Main()
    {Note that we don't update the scopes  section of the spec. This is because, as the spec
states:
The s c ope of a name is the region of program text within which it is possible to refer
to the entity declared by the name without qualification of the name.
In effect, scope only impacts the lookup of non-qualified names. This isn't quite the right
concept for us to leverage because we need to also impact the lookup of qualified
names:
C#
C#        C.M(); // refers to the 'C' in File2.cs
    }
}
// File1.cs
namespace  NS1
{
    file class C
    {
        public static void M() { }
    }
}
namespace  NS2
{
    class Program
    {
        public static void M()
        {
            C.M(); // error: C is not in scope
            NS1.C.M(); // ok: C can be accessed through NS1.
        }
    }
}
// File2.cs
namespace  NS1
{
    class Program
    {
        C.M(); // error
        NS1.C.M(); // error
    }
}Therefore, we don't specify the feature in terms of which scope the type is contained in,
but rather as additional "filtering rules" in member lookup.
File-local classes are permitted to be attribute types, and can be used as attributes
within both file-local types and non-file-local types, just as if the attribute type were a
non-file-local type. The metadata name of the file-local attribute type still goes through
the same name generation strategy as other file-local types. This means detecting the
presence of a file-local type by a hard-coded string name is likely to be impractical,
because it requires depending on the internal name generation strategy of the compiler,
which may change over time. However, detecting via typeof(MyFileLocalAttribute)
works.
C#
There is a general need to prevent file-local types from appearing in member
parameters, returns, and type parameter constraints where the file-local type might not
be in scope at the point of usage of the member.
Note that non-file-local types are permitted to implement file-local interfaces, similar to
how types can implement less-accessible interfaces. Depending on the types present in
the interface members, it could result in a violation of the rules in the following section.Attributes
using System;
using System.Linq;
file class MyFileLocalAttribute  : Attribute  { }
[MyFileLocalAttribute ]
public class C
{
    public static void Main()
    {
        var attribute = typeof(C).CustomAttributes.Where(attr =>  
attr.AttributeType == typeof(MyFileLocalAttribute)).First();
        Console.Write(attribute); // outputs the generated name of the file-
local attribute type
    }
}
Usage in signatures
Only allow signature usage in members of file-local typesPerhaps the simplest way to ensure this is to enforce that file-local types can only
appear in signatures or as base types of other file-local types:
C#
Note that this does restrict usage in explicit implementations, even though such usages
are safe. W e do this in order to simplify the rules for the initial iteration of the feature.
C#
It is a compile-time error to use a file-local type in a global using static directive, i.e.
C#file class FileBase
{
}
public class Derived : FileBase  // error
{
    private FileBase M2() => new FileBase() // error
}
file class FileDerived  : FileBase  // ok
{
    private FileBase M2() => new FileBase() // ok
}
file interface  I
{
    void M(I i);
}
class C : I
{
    void I.M(I i) { } // error
}
global using static
global using static C; // error
file class C
{
    public static void M() { }
}file-local type declarations can implement interfaces, override virtual methods, etc. just
like regular type declarations.
C#Implementation/overrides
file struct Widget : IEquatable<Widget>
{
    public bool Equals(Widget other ) => true;
}Generic Attributes
Article •06/23/2023
When generics were introduced in C# 2.0, attribute classes were not allowed to
participate. W e can make the language more composable by removing (rather,
loosening) this restriction. The .NET Core runtime has added support for generic
attributes. Now, all that's missing is support for generic attributes in the compiler.
Currently attribute authors can take a System.Type as a parameter and have users pass a
typeof expression to provide the attribute with types that it needs. However, outside of
analyzers, there's no way for an attribute author to constrain what types are allowed to
be passed to an attribute via typeof. If attributes could be generic, then attribute
authors could use the existing system of type parameter constraints to express the
requirements for the types they take as input.
The following section is amended: §14.2.4.2
The direct base class of a class type must not be any of the following types:
System.Array, S ystem.Delegate, S ystem.MulticastDelegate, S ystem.Enum, or
System.V alueT ype. Furthermore, a generic class declaration cannot use
System.Attribute as a direct or indirect base class.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Detailed design
One important note is that the following section of the spec is unaffected when
referencing the point of usage of an attribute, i.e. within an attribute list: T ype
parameters - §8.5 .
A type parameter cannot be used anywhere within an attribute.
This means that when a generic attribute is used, its construction needs to be fully
"closed", i.e. not containing any type parameters, which means the following is still
disallowed:
C#
When a generic attribute is used in an attribute list, its type arguments have the same
restrictions that typeof has on its argument. For example, [Attr<dynamic>] is an error.
This is because "attribute-dependent" types like dynamic, List<string?>, nint, and so
on can't be fully represented in the final IL for an attribute type argument, because there
isn't a symbol to "attach" the DynamicAttribute or other well-known attribute to.
Removing the restriction, reasoning out the implications, and adding the appropriate
tests is work.
Attribute authors who want users to be able to discover the requirements for the types
they provide to attributes need to write analyzers and guide their users to use those
analyzers in their builds.
using System;  
using System.Collections.Generic;
public class Attr<T1> : Attribute  { } 
public class Program<T2> 
{ 
    [Attr<T2> ] // error  
    [Attr<List<T2>> ] // error  
    void M() { } 
} 
Drawbacks
Alternatives
Unresolved questions[x] What does AllowMultiple = false mean on a generic attribute? If we have
[Attr<string>] and [Attr<object>] both used on a symbol, does that mean
"multiple" of the attribute are in use?
For now we are inclined to take the more restrictive route here and consider the
attribute class's original definition when deciding whether multiple of it have
been applied. In other words, [Attr<string>] and [Attr<object>] applied
together is incompatible with AllowMultiple = false.
https://github.com/dotnet/csharplang/blob/main/meetings/2017/LDM-2017-02-
21.md#generic-attributes
At the time there was a concern that we would have to gate the feature on
whether the target runtime supports it. (However, we now only support C# 10
on .NET 6. It would be nice to for the implementation to be aware of what
minimum target framework supports the feature, but seems less essential
today.)Design meetings
Primary constructors
Article •08/16/2023
Classes and structs can have a parameter list, and their base class specification can have
an argument list. Primary constructor parameters are in scope throughout the class or
struct declaration, and if they are captured by a function member or anonymous
function, they are appropriately stored (e.g. as unspeakable private fields of the declared
class or struct).
The proposal "retcons" the primary constructors already available on records in terms of
this more general feature with some additional members synthesized.
The ability of a class or struct in C# to have more than one constructor provides for
generality, but at the expense of some tedium in the declaration syntax, because the
constructor input and the class state need to be cleanly separated.
Primary constructors put the parameters of one constructor in scope for the whole class
or struct to be used for initialization or directly as object state. The trade-off is that any
other constructors must call through the primary constructor.
c#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
public class C(bool b, int i, string s) : B(b) // b passed to base  
constructor
{
    public int I { get; set; } = i; // i used for initializationThis describes the generalized design across records and non-records, and then details
how the existing primary constructors for records are specified by adding a set of
synthesized members in the presence of a primary constructor.
Class and struct declarations are augmented to allow a parameter list on the type name,
an argument list on the base class, and a body consisting of just a ;:
antlr    public string S // s used directly in function members
    {
        get => s;
        set => s = value ?? throw new ArgumentNullException( nameof(S));
    }
    public C(string s) : this(true, 0, s) { } // must call this(...)
}
Detailed design
Syntax
class_declaration
  : attributes? class_modifier* 'partial' ? class_designator identifier  
type_parameter_list?
  parameter_list? class_base? type_parameter_constraints_clause* class_body
  ;
  
class_designator
  : 'record'  'class'?
  | 'class'
  
class_base
  : ':' class_type argument_list?
  | ':' interface_type_list
  | ':' class_type  argument_list? ',' interface_type_list
  ;  
  
class_body
  : '{' class_member_declaration* '}' ';'?
  | ';'
  ;
  
struct_declaration
  : attributes? struct_modifier* 'partial' ? 'record' ? 'struct'  identifier  
type_parameter_list?
    parameter_list? struct_interfaces? type_parameter_constraints_clause*  
struct_body
  ;Note: These productions replace record_declaration in Records  and
record_struct_declaration in Record structs , which both become obsolete.
It is an error for a class_base to have an argument_list if the enclosing
class_declaration does not contain a parameter_list. At most one partial type
declaration of a partial class or struct may provide a parameter_list. The parameters in
the parameter_list of a record declaration must all be value parameters.
Note, according to this proposal class_body, struct_body, interface_body and
enum_body are allowed to consist of just a ;.
A class or struct with a parameter_list has an implicit public constructor whose
signature corresponds to the value parameters of the type declaration. This is called the
primar y constr uctor for the type, and causes the implicitly declared parameterless
constructor, if present, to be suppressed. It is an error to have a primary constructor and
a constructor with the same signature already present in the type declaration.
The lookup of simple names  is augmented to handle primary constructor parameters.
The changes are highlighted in bold  in the following excerpt:struct_body
  : '{' struct_member_declaration* '}' ';'?
  | ';'
  ;
  
interface_declaration
  : attributes? interface_modifier* 'partial' ? 'interface'
    identifier variant_type_parameter_list? interface_base?
    type_parameter_constraints_clause* interface_body
  ;  
    
interface_body
  : '{' interface_member_declaration* '}' ';'?
  | ';'
  ;
enum_declaration
  : attributes? enum_modifier* 'enum' identifier enum_base? enum_body
  ;
enum_body
  : '{' enum_member_declarations? '}' ';'?
  | '{' enum_member_declarations ',' '}' ';'?
  | ';'
  ;
Lookup
Otherwise, for each instance type T (§14.3.2 ), starting with the instance type
of the immediately enclosing type declaration and continuing with the
instance type of each enclosing class or struct declaration (if any):
If the declaration o f T includes a primar y construct or paramet er I and
the r eference occur s within the argument_list of T's class_base or within
an initializer o f a field, pr oper ty or ev ent o f T, the r esult is the primar y
construct or paramet er I
Other wise,  if e is zero and the declaration of T includes a type parameter
with name I, then the simple_name  refers to that type parameter.
Otherwise, if a member lookup ( §11.5 ) of I in T with e type arguments
produces a match:
If T is the instance type of the immediately enclosing class or struct type
and the lookup identifies one or more methods, the result is a method
group with an associated instance expression of this. If a type argument
list was specified, it is used in calling a generic method ( §11.7.8.2 ).
Otherwise, if T is the instance type of the immediately enclosing class or
struct type, if the lookup identifies an instance member, and if the
reference occurs within the block  of an instance constructor, an instance
method, or an instance accessor ( §11.2.1 ), the result is the same as a
member access ( §11.7.6 ) of the form this.I. This can only happen
when e is zero.
Otherwise, the result is the same as a member access ( §11.7.6 ) of the
form T.I or T.I<A₁, ..., Aₑ>.
Other wise, if the declaration o f T includes a primar y construct or
paramet er I, the r esult is the primar y construct or paramet er I.
The first addition corresponds to the change incurred by primary constructors on
records , and ensures that primary constructor parameters are found before any
corresponding fields within initializers and base class arguments. It extends this rule to
static initializers as well. However, since records always have an instance member with
the same name as the parameter, the extension can only lead to a change in an error
message. Illegal access to a parameter vs. illegal access to an instance member.
The second addition allows primary constructor parameters to be found elsewhere
within the type body, but only if not shadowed by members.
It is an error to reference a primary constructor parameter if the reference does not
occur within one of the following:
a nameof argument
an initializer of an instance field, property or event of the declaring type (type
declaring primary constructor with the parameter).
the argument_list of class_base of the declaring type.
the body of an instance method (note that instance constructors are excluded) of
the declaring type.
the body of an instance accessor of the declaring type.
In other words, primary constructor parameters are in scope throughout the declaring
type body. They shadow members of the declaring type within an initializer of a field,
property or event of the declaring type, or within the argument_list of class_base of
the declaring type. They are shadowed by members of the declaring type everywhere
else.
Thus, in the following declaration:
c#
The initializer for the field i references the parameter i, whereas the body of the
property I references the field i.
Compiler will produce a warning on usage of an identifier when a base member
shadows a primary constructor parameter if that primary constructor parameter was not
passed to the base type via its constructor.
A primary constructor parameter is considered to be passed to the base type via its
constructor when all the following conditions are true for an argument in class_b ase:
The argument represents an implicit or explicit identity conversion of a primary
constructor parameter;
The argument is not part of an expanded params argument;
A primary constructor leads to the generation of an instance constructor on the
enclosing type with the given parameters. If the class_base has an argument list, theclass C(int i)
{
    protected  int i = i; // references parameter
    public int I => i; // references field
}
Warn on shadowing by a member from base
Semanticsgenerated instance constructor will have a base initializer with the same argument list.
Primary constructor parameters in class/struct declarations can be declared ref, in or
out. Declaring ref or out parameters remains illegal in primary constructors of record
declaration.
All instance member initializers in the class body will become assignments in the
generated constructor.
If a primary constructor parameter is referenced from within an instance member, and
the reference is not inside of a nameof argument, it is captured into the state of the
enclosing type, so that it remains accessible after the termination of the constructor. A
likely implementation strategy is via a private field using a mangled name. In a readonly
struct the capture fields will be readonly. Therefore, access to captured parameters of a
readonly struct will have similar restrictions as access to readonly fields. Access to
captured parameters within a readonly member will have similar restrictions as access to
instance fields in the same context.
Capturing is not allowed for parameters that have ref-like type, and capturing is not
allowed for ref, in or out parameters. This is similar to a limitation for capturing in
lambdas.
If a primary constructor parameter is only referenced from within instance member
initializers, those can directly reference the parameter of the generated constructor, as
they are executed as part of it.
Primary Constructor will do the following sequence of operations:
1. Parameter values are stored in capture fields, if any.
2. Instance initializers are executed
3. Base constructor initializer is called
Parameter references in any user code are replaced with corresponding capture field
references.
For instance this declaration:
c#
public class C(bool b, int i, string s) : B(b) // b passed to base  
constructor
{
    public int I { get; set; } = i; // i used for initialization
    public string S // s used directly in function members
    {
        get => s;Generates code similar to the following:
c#
It is an error for a non-primary constructor declaration to have the same parameter list
as the primary constructor. All non-primary constructor declarations must use a this
initializer, so that the primary constructor is ultimately called.
Records produce a warning if a primary constructor parameter isn't read within the
(possibly generated) instance initializers or base initializer. Similar warnings will be
reported for primary constructor parameters in classes and structures:
for a by-value parameter, if the parameter is not captured and is not read within
any instance initializers or base initializer.
for an in parameter, if the parameter is not read within any instance initializers or
base initializer.
for a ref parameter, if the parameter is not read or written to within any instance
initializers or base initializer.        set => s = value ?? throw new NullArgumentException( nameof(X));
    }
    public C(string s) : this(true, 0, s) { } // must call this(...)
}
public class C : B
{
    public int I { get; set; }
    public string S
    {
        get => __s;
        set => __s = value ?? throw new NullArgumentException( nameof(X));
    }
    public C(string s) : this(0, s) { ... } // must call this(...)
    
    // generated members
    private string __s; // for capture of s
    public C(bool b, int i, string s)
    {
        __s = s; // capture s
        I = i; // run I's initializer
        B(b) // run B's constructor
    }
}
Identical simple names and type namesThere is a special language rule for scenarios often referred to as "Color Color" scenarios
- Identical simple names and type names .
In a member access of the form E.I, if E is a single identifier, and if the meaning of
E as a simple_name  (§11.7.4 ) is a constant, field, property, local variable, or
parameter with the same type as the meaning of E as a type_name  (§7.8.1 ), then
both possible meanings of E are permitted. The member lookup of E.I is never
ambiguous, since I shall necessarily be a member of the type E in both cases. In
other words, the rule simply permits access to the static members and nested types
of E where a compile-time error would otherwise have occurred.
With respect to primary constructors, the rule affects whether an identifier within an
instance member should be treated as a type reference, or as a primary constructor
parameter reference, which, in turn, captures the parameter into the the state of the
enclosing type. Even though "the member lookup of E.I is never ambiguous", when
lookup yields a member group, in some cases it is impossible to determine whether a
member access refers to a static member or an instance member without fully resolving
(binding) the member access. At the same time, capturing a primary constructor
parameter changes properties of enclosing type in a way that affects semantic analysis.
For example, the type might become unmanaged and fail certain constraints because of
that. There are even scenarios for which binding can succeed either way, depending on
whether the parameter is considered captured or not. For example:
C#
struct S1(Color Color )
{
    public void Test()
    {
        Color.M1( this);
    }
}
class Color
{
    public void M1<T>(T x, int y = 0)
    {
        System.Console.WriteLine( "instance" );
    }
    
    public static void M1<T>(T x) where T : unmanaged
    {
        System.Console.WriteLine( "static" );
    }
}If we treat receiver Color as a value, we capture the parameter and 'S1' becomes
managed. Then the static method becomes inapplicable due to the constraint and we
would call instance method. However, if we treat the receiver as a type, we don't capture
the parameter and 'S1' remains unmanaged, then both methods are applicable, but the
static method is "better" because it doesn't have an optional parameter. Neither choice
leads to an error, but each would result in distinct behavior.
Given this, compiler will produce an ambiguity error for a member access E.I when all
the following conditions are met:
Member lookup of E.I yields a member group containing instance and static
members at the same time. Extension methods applicable to the receiver type are
treated as instance methods for the purpose of this check.
If E is treated as a simple name, rather than a type name, it would refer to a
primary constructor parameter and would capture the parameter into the state of
the enclosing type.
If a primary constructor parameter is passed to the base and also captured, there's a
high risk that it is inadvertently stored twice in the object.
Compiler will produce a warning for in or by value argument in a class_base
argument_list when all the following conditions are true:
The argument represents an implicit or explicit identity conversion of a primary
constructor parameter;
The argument is not part of an expanded params argument;
The primary constructor parameter is captured into the state of the enclosing type.
Compiler will produce a warning for a variable_initializer when all the following
conditions are true:
The variable initializer represents an implicit or explicit identity conversion of a
primary constructor parameter;
The primary constructor parameter is captured into the state of the enclosing type.
For example:
c#Double storage warnings
public class Person(string name)
{
    public string Name { get; set; } = name;   // initializationAt https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-03-
13.md  we decided to embrace the
https://github.com/dotnet/csharplang/issues/7047  proposal.
The "method" attribute target is allowed on a class_declar ation /struct_declar ation  with
paramet er_list  and results in the corresponding primary constructor having that
attribute. Attributes with the method target on a class_declar ation /struct_declar ation
without paramet er_list  are are ignored with a warning.
C#
With this proposal, records no longer need to separately specify a primary constructor
mechanism. Instead, record (class and struct) declarations that have primary
constructors would follow the general rules, with these simple additions:    public override  string ToString () => name; // capture
}
Attributes targeting primary constructors
[method: FooAttr ] // Good
public partial record Rec(
    [property: Foo] int X,
    [field: NonSerialized] int Y
);
[method: BarAttr ] // warning CS0657: 'method' is not a valid attribute  
location for this declaration. Valid attribute locations for this  
declaration are 'type'. All attributes in this block will be ignored.
public partial record Rec
{
    public void Frobnicate ()
    {
        ...
    }
}
[method: Attr ] // Good
public record MyUnit1();
[method: Attr ] // warning CS0657: 'method' is not a valid attribute location  
for this declaration. Valid attribute locations for this declaration are  
'type'. All attributes in this block will be ignored.
public record MyUnit2;
Primary constructors on recordsFor each primary constructor parameter, if a member with the same name already
exists, it must be an instance property or field. If not, a public init-only auto-
property of the same name is synthesized with a property initializer assigning from
the parameter.
A deconstructor is synthesized with out parameters to match the primary
constructor parameters.
If an explicit constructor declaration is a "copy constructor" - a constructor that
takes a single parameter of the enclosing type - it is not required to call a this
initializer, and will not execute the member initializers present in the record
declaration.
The allocation size of constructed objects is less obvious, as the compiler
determines whether to allocate a field for a primary constructor parameter based
on the full text of the class. This risk is similar to the implicit capture of variables by
lambda expressions.
A common temptation (or accidental pattern) might be to capture the "same"
parameter at multiple levels of inheritance as it is passed up the constructor chain
instead of explicitly allotting it a protected field at the base class, leading to
duplicated allocations for the same data in objects. This is very similar to today's
risk of overriding auto-properties with auto-properties.
As proposed here, there is no place for additional logic that might usually be
expressed in constructor bodies. The "primary constructor bodies" extension below
addresses that.
As proposed, execution order semantics are subtly different from within ordinary
constructors, delaying member initializers to after the base calls. This could
probably be remedied, but at the cost of some of the extension proposals (notably
"primary constructor bodies").
The proposal only works for scenarios where a single constructor can be
designated primary.
There is no way to express separate accessibility of the class and the primary
constructor. An example is when public constructors all delegate to one private
"build-it-all" constructor. If necessary, syntax could be proposed for that later.Drawbacks
Alternatives
No captureA much simpler version of the feature would prohibit primary constructor parameters
from occurring in member bodies. R eferencing them would be an error. Fields would
have to be explicitly declared if storage is desired beyond the initialization code.
c#
This could still be evolved to the full proposal at a later time, and would avoid a number
of decisions and complexities, at the cost of removing less boilerplate initially, and
probably also seeming unintuitive.
An alternative approach is for primary constructor parameters to always and visibly
generate a field of the same name. Instead of closing over the parameters in the same
manner as local and anonymous functions, there would explicitly be a generated
member declaration, similar to the public properties generated for primary construcor
parameters in records. Just like for records, if a suitable member already exists, one
would not be generated.
If the generated field is private it could still be elided when it is not used as a field in
member bodies. In classes, however, a private field would often not be the right choice,
because of the state duplication it could cause in derived classes. An option here would
be to instead generating a protected field in classes, encouraging reuse of storage
across inheritance layers. However, then we would not be able to elide the declaration,
and would incur allocation cost for every primary constructor parameter.
This would align non-record primary constructors more closely with record ones, in that
members are always (at least conceptually) generated, albeit different kinds of members
with different accessibilities. But it would also lead to surprising differences from how
parameters and locals are captured elsewhere in C#. If we were ever to allow local
classes, for example, they would capture enclosing parameters and locals implicitly.
Visibly generating shadowing fields for them would not seem to be a reasonable
behavior.
Another problem often raised with this approach is that many developers have different
naming conventions for parameters and fields. Which should be used for the primarypublic class C(string s)
{
    public S1 => s; // Nope!
    public S2 { get; } = s; // Still allowed
}
Explicit generated fieldsconstructor parameter? Either choice would lead to inconsistency with the rest of the
code.
Finally, visibly generating member declarations is really the name of the game for
records, but much more surprising and "out of character" for non-record classes and
structs. All in all, those are the reasons why the main proposal opts for implicit capture,
with sensible behavior (consistent with records) for explicit member declarations when
they are desired.
The lookup rules above are intended to allow for the current behavior of primary
constructor parameters in records when a corresponding member is manually declared,
and to explain the behavior of the generated member when it is not. This requires
lookup to differ between "initialization scope" (this/base initializers, member initializers)
and "body scope" (member bodies), which the above proposal achieves by changing
when  primary constructor parameters are looked for, depending on where the reference
occurs.
An observation is that referencing an instance member with a simple name in initializer
scope always leads to an error. Instead of merely shadowing instance members in those
places, could we simply take them out of scope? That way, there wouldn't be this weird
conditional ordering of scopes.
This alternative is probably possible, but it would have some consequences that are
somewhat far-reaching and potentially undesirable. First of all, if we remove instance
members from initializer scope then a simple name that does correspond to an instance
member and not to a primary constructor parameter could accidentally bind to
something outside of the type declaration! This seems like it would rarely be intentional,
and an error would be better.
Furthermore, static members are fine to reference in initialization scope. So we would
have to distinguish between static and instance members in lookup, something we don't
do today. (W e do distinguish in overload resolution but that is not in play here). So that
would have to also be changed, leading to yet more situations where e.g. in static
contexts something would bind "further out" rather than error because it found an
instance member.
All in all this "simplification" would lead to quite a downstream complication that no-
one asked for.Remove instance members from initializer scope
Possible extensionsThese are variations or additions to the core proposal that may be considered in
conjunction with it, or at a later stage if deemed useful.
The rules above make it an error to reference a primary constructor parameter within
another constructor. This could be allowed within the body  of other constructors,
though, since the primary constructor runs first. However it would need to remain
disallowed within the argument list of the this initializer.
c#
Such access would still incur capture, as that would be the only way the constructor
body could get at the variable after the primary constructor has already run.
The prohibition on primary constructor parameters in the this-initializer's arguments
could be weakened to allow them, but make them not definitely assigned, but that does
not seem useful.
Constructors without a this initializer (i.e. with an implicit or explicit base initializer)
could be allowed. Such a constructor would not run instance field, property and event
initializers, as those would be considered to be part of the primary constructor only.
In the presence of such base-calling constructors, there are a couple of options for how
primary constructor parameter capture is handled. The simplest is to completely
disallow capture in this situation. Primary constructor parameters would be for
initialization only when such constructors exist.
Alternatively, if combined with the previously described option to allow access to
primary constructor parameters within constructors, the parameters could enter the
constructor body as not definitely assigned, and ones that are captured would need to
be definitely assigned by the end of the constructor body. They would essentially be
implicit out parameters. That way, captured primary constructor parameters wouldPrimary constructor parameter access within constructors
public class C(bool b, int i, string s) : B(b)
{
    public C(string s) : this(b, s) // b still disallowed
    { 
        i++; // could be allowed
    }
}
Allow constructors without a this initializeralways have a sensible (i.e. explicitly assigned) value by the time they are consumed by
other function members.
An attraction of this extension (in either form) is that it fully generalizes the current
exemption for "copy constructors" in records, without leading to situations where
uninitialized primary constructor parameters are observed. Essentially, constructors that
initialize the object in alternative ways are fine. The capture-related restrictions would
not be a breaking change for existing manually defined copy constructors in records,
because records never capture their primary constructor parameters (they generate
fields instead).
c#
Constructors themselves often contain parameter validation logic or other nontrivial
initialization code that cannot be expressed as initializers.
Primary constructors could be extended to allow statement blocks to appear directly in
the class body. Those statements would be inserted in the generated constructor at the
point where they appear between initializing assignments, and would thus be executed
interspersed with initializers. For instance:
c#public class C(bool b, int i, string s) : B(b)
{
    public int I { get; set; } = i; // i used for initialization
    public string S // s used directly in function members
    {
        get => s;
        set => s = value ?? throw new NullArgumentException( nameof(X));
    }
    public C(string s2) : base(true) // cannot use `string s` because it  
would shadow
    { 
        s = s2; // must initialize s because it is captured by S
    }
    protected  C(C original ) : base(original ) // copy constructor
    {
        this.s = original.s; // assignment to b and i not required because  
not captured
    }
}
Primary constructor bodies
public class C(int i, string s) : B(s)
{A lot of this scenario might be adequately be covered if we were to introduce "final
initializers" which run after the constructors and any object/collection initializers have
completed. However, argument validation is one thing that would ideally happen as
early as possible.
Primary constructor bodies could also provide a place for allowing an access modifier
for the primary constructor, allowing it to deviate from the accessibility of the enclosing
type.
A possible and often mentioned addition could be to allow primary constructor
parameters to be annotated so that they would also declare a member on the type.
Most commonly it is proposed to allow an access specifier on the parameters to trigger
the member generation:
c#
There are some problems:
What if a property is desired, not a field? Having { get; set; } syntax inline in a
parameter list does not seem appetizing.
What if different naming conventions are used for parameters and fields? Then this
feature would be useless.
This is a potential future addition that can be adopted or not. The current proposal
leaves the possibility open.    {
        if (i < 0) throw new ArgumentOutOfRangeException( nameof(i));
    }
int[] a = new int[i];
    public int S => s;
}
Combined parameter and member declarations
public class C(bool b, protected  int i, string s) : B(b) // i is a field as  
well as a parameter
{
    void M()
    {
        ... i ... // refers to the field i
        ... s ... // closes over the parameter s
    }
}The https://github.com/dotnet/csharplang/blob/main/proposals/csharp-12.0/primary-
constructors.md#lookup  section specifies that type parameters of declaring type
should come before type's primary constructor parameters in every context where those
parameters are in scope. However, we already have existing behavior with records -
primary constructor parameters come before type parameters in base initializer and field
initializers.
What should we do about this discrepancy?
Adjust the rules to match the behavior.
Adjust the behavior (a possible breaking change).
Disallow a primiry constructor parameter to use type parameter's name (a possible
breaking change).
Do nothing, accept the inconsistency between the spec and implementation.
Adjust the rules to match the behavior
(https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-09-
25.md#primary-constructors ).
Should we allow field targeting attributes for captured primary constructor parameters?
C#Open questions
Lookup order for type parameters
Conclusion:
Field targeting attributes for captured primary
constructor parameters
class C1([field: Test] int x) // Parameter is captured, the attribute goes  
to the capture field
{
    public int X => x;
}
class C2([field: Test] int x) // Parameter is not captured, the attribute is  
ignored with a warning CS0657: 'field' is not a valid attribute location for  
this declaration. Valid attribute locations for this declaration are  
'param'. All attributes in this block will be ignored.
{Right now the attributes are ignored with the warning regardless of whether the
parameter is captured.
Note that for records, field targeted attributes are allowed when a property is
synthesized for it. The attributes go on the backing field then.
C#
Not allowed ( https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-
2023-05-03.md#attributes-on-captured-parameters ).
Should we report a warning when a member from base is shadowing a primary
constructor parameter inside a member (see
https://github.com/dotnet/csharplang/discussions/7109#discussioncomment-
5666621 )?
An alternative design is approved -
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
08.md#primary-constructors
When a parameter captured into the state of the enclosing type is also referenced in a
lambda inside an instance initializer or a base initializer, the lambda and the state of the
enclosing type should refer to the same location for the parameter. For example:    public int X = x;
}
record R1([field: Test] int X); // Ok, the attribute goes on the backing  
field
record R2([field: Test] int X) // warning CS0657: 'field' is not a valid  
attribute location for this declaration. Valid attribute locations for this  
declaration are 'param'. All attributes in this block will be ignored.
{
    public int X = X;
}
Conclusion:
Warn on shadowing by a member from base
Conclusion:
Capturing instance of the enclosing type in a closureC#
Since naive implementation of capturing a parameter into the state of the type simply
captures the parameter in a private instance field, the lambda needs to refer to the same
field. As a result, it needs to be able to access the instance of the type. This requires
capturing this into a closure before the base constructor is invoked. That, in turn,
results in safe, but an unverifiable IL. Is this acceptable?
Alternatively we could:
Disallow lambdas like that;
Or, instead, capture parameters like that in an instance of a separate class (yet
another closure), and share that instance between the closure and the instance of
the enclosing type. Thus eliminating the need to capture this in a closure.
We are comfortable with capturing this into a closure before the base constructor is
invoked ( https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-
02-15.md ). The runtime team didn't find the IL pattern problematic as well.
C# allows to assign to this within a struct. If the struct captures a primary constructor
parameter, the assignment is going to overwrite its value, which might be not obvious
to the user. Do we want to report a warning for assignments like this?
C#partial class C1
{
    public System.Func< int> F1 = Execute1(() => p1++);
}
partial class C1 (int p1)
{
    public int M1() { return p1++; }
    static System. Func<int> Execute1 (System.Func< int> f)
    {
        _ = f();
        return f;
    }
}
Conclusion:
Assigning to this within a structAllowed, no warning
(https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-02-
15.md ).
We have a warning if a primary constructor parameter is passed to the base and also
captured, because there's a high risk that it is inadvertently stored twice in the object.
It seems that there's a similar risk if a parameter is used to initialize a member, and is
also captured. Here's a small example:
c#
For a given instance of Person, changes to Name would not be reflected in the output of
ToString, which is probably unintended on the developer's part.
Should we introduce a double storage warning for this situation?
This is how it would work:
The compiler will produce a warning for a variable_initializer when all the following
conditions are true:
The variable initializer represents an implicit or explicit identity conversion of a
primary constructor parameter;struct S(int x)
{
    int X => x;
    
    void M(S s)
    {
        this = s; // 'x' is overwritten
    }
}
Conclusion:
Double storage warning for initialization plus capture
public class Person(string name)
{
    public string Name { get; set; } = name;   // initialization
    public override  string ToString () => name; // capture
}The primary constructor parameter is captured into the state of the enclosing type.
Approved, see https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-
2023-05-15.md#primary-constructors
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-10-
17.md
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-01-
18.md
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-02-
15.md
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-02-
22.md
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-03-
13.md
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
03.md#primary-constructors
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
08.md#primary-constructors
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
15.md#primary-constructors
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-09-
25.md#primary-constructorsConclusion:
LDM meetings
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackCollection expressions
Article •09/27/2023
Collection expressions introduce a new terse syntax, [e1, e2, e3, etc], to create
common collection values. Inlining other collections into these values is possible using a
spread operator .. like so: [e1, ..c2, e2, ..c2].
Several collection-like types can be created without requiring external BCL support.
These types are:
Array types , such as int[].
Span<T>  and ReadOnlySpan<T> .
Types that support collection initializers , such as List<T> .
Further support is present for collection-like types not covered under the above through
a new attribute and API pattern that can be adopted directly on the type itself.
Collection-like values are hugely present in programming, algorithms, and
especially in the C#/.NET ecosystem. Nearly all programs will utilize these values to
store data and send or receive data from other components. Currently, almost all
C# programs must use many different and unfortunately verbose approaches to
create instances of such values. Some approaches also have performance
drawbacks. Here are some common examples:
Arrays, which require either new Type[] or new[] before the { ... } values.
Spans, which may use stackalloc and other cumbersome constructs.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
MotivationCollection initializers, which require syntax like new List<T> (lacking inference of
a possibly verbose T) prior to their values, and which can cause multiple
reallocations of memory because they use N .Add invocations without
supplying an initial capacity.
Immutable collections, which require syntax like ImmutableArray.Create(...) to
initialize the values, and which can cause intermediary allocations and data
copying. More efficient construction forms (like ImmutableArray.CreateBuilder)
are unwieldy and still produce unavoidable garbage.
Looking at the surrounding ecosystem, we also find examples everywhere of list
creation being more convenient and pleasant to use. T ypeScript, Dart, S wift, Elm,
Python, and more opt for a succinct syntax for this purpose, with widespread
usage, and to great effect. Cursory investigations have revealed no substantive
problems arising in those ecosystems with having these literals built in.
C# has also added list patterns  in C# 11. This pattern allows matching and
deconstruction of list-like values using a clean and intuitive syntax. However, unlike
almost all other pattern constructs, this matching/deconstruction syntax lacks the
corresponding construction syntax.
Getting the best performance for constructing each collection type can be tricky.
Simple solutions often waste both CPU and memory. Having a literal form allows
for maximum flexibility from the compiler implementation to optimize the literal to
produce at least as good a result as a user could provide, but with simple code.
Very often the compiler will be able to do better, and the specification aims to
allow the implementation large amounts of leeway in terms of implementation
strategy to ensure this.
An inclusive solution is needed for C#. It should meet the vast majority of casse for
customers in terms of the collection-like types and values they already have. It should
also feel natural in the language and mirror the work done in pattern matching.
This leads to a natural conclusion that the syntax should be like [e1, e2, e3, e-etc] or
[e1, ..c2, e2], which correspond to the pattern equivalents of [p1, p2, p3, p-etc]
and [p1, ..p2, p3].
The following grammar  productions are added:
diff
Detailed design
Collection literals are target-typed .
For brevity, collection_expression will be referred to as "literal" in the following
sections.
expression_element instances will commonly be referred to as e1, e_n, etc.
spread_element instances will commonly be referred to as ..s1, ..s_n, etc.
span type  means either Span<T> or ReadOnlySpan<T>.
Literals will commonly be shown as [e1, ..s1, e2, ..s2, etc] to convey any
number of elements in any order. Importantly, this form will be used to represent
all cases such as:
Empty literals []
Literals with no expression_element in them.
Literals with no spread_element in them.
Literals with arbitrary ordering of any element type.
The iteration type  of ..s_n is the type of the iteration v ariable  determined as if s_n
were used as the expression being iterated over in a foreach_statement .primary_no_array_creation_expression
  ...
+ | collection_expression
  ;
+ collection_expression
  : '[' ']'
  | '[' collection_element ( ',' collection_element )* ']'
  ;
+ collection_element
  : expression_element
  | spread_element
  ;
+ expression_element
  : expression
  ;
+ spread_element
  : '..' expression
  ;
Spec clarifications
Variables starting with __name are used to represent the results of the evaluation of
name, stored in a location so that it is only evaluated once. For example __e1 is the
evaluation of e1.
List<T>, IEnumerable<T>, etc. refer to the respective types in the
System.Collections.Generic namespace.
The specification defines a translation  of the literal to existing C# constructs.
Similar to the query expr ession tr anslation , the literal is itself only legal if the
translation would result in legal code. The purpose of this rule is to avoid having to
repeat other rules of the language that are implied (for example, about
convertibility of expressions when assigned to storage locations).
An implementation is not required to translate literals exactly as specified below.
Any translation is legal if the same result is produced and there are no observable
differences in the production of the result.
For example, an implementation could translate literals like [1, 2, 3] directly
to a new int[] { 1, 2, 3 } expression that itself bakes the raw data into the
assembly, eliding the need for __index or a sequence of instructions to assign
each value. Importantly, this does mean if any step of the translation might
cause an exception at runtime that the program state is still left in the state
indicated by the translation.
References to 'stack allocation' refer to any strategy to allocate on the stack and
not the heap. Importantly, it does not imply or require that that strategy be
through the actual stackalloc mechanism. For example, the use of inline arrays
is also an allowed and desirable approach to accomplish stack allocation where
available.
Collections are assumed to be well-behaved. For example:
It is assumed that the value of Count on a collection will produce that same
value as the number of elements when enumerated.
The types used in this spec defined in the System.Collections.Generic
namespace are presumed to be side-effect free. As such, the compiler can
optimize scenarios where such types might be used as intermediary values, but
otherwise not be exposed.
It is assumed that a call to some applicable .AddRange(x) member on a
collection will result in the same final value as iterating over x and adding all of
its enumerated values individually to the collection with .Add.
The behavior of collection literals with collections that are not well-behaved is
undefined.
A collection expr ession c onversion allows a collection expression to be converted to a
type.
The following implicit collection expr ession c onversions  exist from a collection expression:
To a single dimensional array type  T[] where:
For each element  Ei there is an implicit c onversion to T.
To a span type  System.Span<T> or System.ReadOnlySpan<T> where:
For each element  Ei there is an implicit c onversion to T.
To a type with a create method  with paramet er type  System.ReadOnlySpan<T> where:
For each element  Ei there is an implicit c onversion to T.
To a struct or class type  that implements
System.Collections.Generic.IEnumerable<T> where:
For each element  Ei there is an implicit c onversion to T.
To a struct or class type  that implements System.Collections.IEnumerable and does
not implement  System.Collections.Generic.IEnumerable<T>.
To an interface type  System.Collections.Generic.IEnumerable<T>,
System.Collections.Generic.IReadOnlyCollection<T>,
System.Collections.Generic.IReadOnlyList<T>,
System.Collections.Generic.ICollection<T>, or
System.Collections.Generic.IList<T> where:
For each element  Ei there is an implicit c onversion to T.
There is no collection expr ession c onversion from a collection expression to a multi
dimensional array type .
In the cases above, a collection expression element  Ei is considered to have an implicit
conversion to type T if:
Ei is an expression element  and there is an implicit conversion from Ei to T.
Ei is a spread element  Si and there is an implicit conversion from the iteration
type of Si to T.
Types for which there is an implicit collection expression conversion from a collection
expression are the valid target types  for that collection expression.ConversionsThe following additional implicit conversions exist from a collection expr ession :
To a nullable v alue type  T? where there is a collection expr ession c onversion from
the collection expression to a value type T. The conversion is a collection
expression c onversion to T followed by an implicit nullable c onversion from T to
T?.
To a reference type T where there is a create method  associated with T that
returns a type U and an implicit r eference conversion from U to T. The conversion
is a collection expr ession c onversion to U followed by an implicit r eference
conversion from U to T.
To an interface type I where there is a create method  associated with I that
returns a type V and an implicit bo xing c onversion from V to I. The conversion is a
collection expr ession c onversion to V followed by an implicit bo xing c onversion from
V to I.
A create method  is indicated with a [CollectionBuilder(...)] attribute on the collection
type. The attribute specifies the builder type  and method name  of a method to be
invoked to construct an instance of the collection type.
c#
The attribute can be applied to a class, struct, ref struct, or interface. The attribute
is not inherited although the attribute can be applied to a base class or an abstract
class.Create methods
namespace  System.Runtime.CompilerServices
{
    [AttributeUsage(
        AttributeTargets.Class | AttributeTargets.Struct |  
AttributeTargets.Interface,
        Inherited = false,
        AllowMultiple = false) ]
    public sealed class CollectionBuilderAttribute  : System.Attribute
    {
        public CollectionBuilderAttribute (Type builderType, string 
methodName );
        public Type BuilderType { get; }
        public string MethodName { get; }
    }
}The collection type must have an iteration type .
For the create method :
The builder type  must be a non-generic class or struct.
The method must be defined on the builder type  directly.
The method must be static.
The method must be accessible where the collection expression is used.
The arity of the method must match the arity of the collection type.
The method must have a single parameter of type System.ReadOnlySpan<E>, passed
by value, and there is an identity c onversion  from E to the iteration type  of the
collection type .
There is an identity c onversion , implicit r eference conversion , or boxing
conversion  from the method return type to the collection type .
An error is reported if the [CollectionBuilder] attribute does not refer to an invocable
method with the expected signature.
Method overloads on the builder type  with distinct signatures are ignored. Methods
declared on base types or interfaces are ignored.
For a collection expr ession  with a target type C<S, S, …> where the type declar ation
C<T, T, …> has an associated builder method  B.M<U, U, …>(), the gener ic type
arguments  from the target type are applied in order — and from outermost containing
type to innermost — to the builder method .
The span parameter for the create method  can be explicitly marked scoped or
[UnscopedRef]. If the parameter is implicitly or explicitly scoped, the compiler may
allocate the storage for the span on the stack rather than the heap.
For example, a possible create method  for ImmutableArray<T>:
C#
With the create method  above, ImmutableArray<int> ia = [1, 2, 3]; could be emitted
as:
01
01 01
[CollectionBuilder(typeof(ImmutableArray), "Create" )]
public struct ImmutableArray<T> { ... }
public static class ImmutableArray
{
    public static ImmutableArray<T> Create<T>(ReadOnlySpan<T> items) { ... }
}C#
The elements of a collection expression are evaluat ed in order, left to right. Each
element is evaluated exactly once, and any further references to the elements refer to
the results of this initial evaluation.
A spread element may be iterated before or after the subsequent elements in the
collection expression are evaluat ed.
An unhandled exception thrown from any of the methods used during construction will
be uncaught and will prevent further steps in the construction.
Length, Count, and GetEnumerator are assumed to have no side effects.
If the target type is a struct or class type  that implements
System.Collections.IEnumerable, and the target type does not have a create method ,
the construction of the collection instance is as follows:
The elements are evaluated in order. Some or all elements may be evaluated
during the steps below rather than before.
The compiler may determine the known length  of the collection expression by
invoking countable  properties — or equivalent properties from well-known
interfaces or types — on each spread element expr ession .
The constructor that is applicable with no arguments is invoked.
For each element in order:
If the element is an expression element , the applicable Add instance or extension
method is invoked with the element expression  as the argument. (Unlike classic
collection initializer behavior , element evaluation and Add calls are not
necessarily interleaved.)
If the element is a spread element  then one of the following is used:[InlineArray( 3)] struct __InlineArray3<T> { private T _element0; }
Span<int> __tmp = new __InlineArray3< int>();
__tmp[0] = 1;
__tmp[1] = 2;
__tmp[2] = 3;
ImmutableArray< int> ia =
    ImmutableArray.Create((ReadOnlySpan< int>)__tmp);
Construction
An applicable GetEnumerator instance or extension method is invoked on the
spread element expr ession  and for each item from the enumerator the
applicable Add instance or extension method is invoked on the collection
instance with the item as the argument. If the enumerator implements
IDisposable, then Dispose will be called after enumeration, regardless of
exceptions.
An applicable AddRange instance or extension method is invoked on the
collection inst ance with the spread element expression  as the argument.
An applicable CopyTo instance or extension method is invoked on the spread
element expr ession  with the collection instance and int index as arguments.
During the construction steps above, an applicable EnsureCapacity instance or
extension method may be invoked one or more times on the collection inst ance
with an int capacity argument.
If the target type is an array, a span, a type with a create method , or an interface, the
construction of the collection instance is as follows:
The elements are evaluated in order. Some or all elements may be evaluated
during the steps below rather than before.
The compiler may determine the known length  of the collection expression by
invoking countable  properties — or equivalent properties from well-known
interfaces or types — on each spread element expr ession .
An initialization inst ance is created as follows:
If the target type is an array and the collection expression has a known length ,
an array is allocated with the expected length.
If the target type is a span or a type with a create method , and the collection has
a known length , a span with the expected length is created referring to
contiguous storage.
Otherwise intermediate storage is allocated.
For each element in order:
If the element is an expression element , the initialization instance index er is
invoked to add the evaluated expression at the current index.
If the element is a spread element  then one of the following is used:
A member of a well-known interface or type is invoked to copy items from
the spread element expression to the initialization instance.
An applicable GetEnumerator instance or extension method is invoked on the
spread element expr ession  and for each item from the enumerator, the
initialization instance index er is invoked to add the item at the current index.
If the enumerator implements IDisposable, then Dispose will be called after
enumeration, regardless of exceptions.
An applicable CopyTo instance or extension method is invoked on the spread
element expr ession  with the initialization instance and int index as
arguments.
If intermediate storage was allocated for the collection, a collection instance is
allocated with the actual collection length and the values from the initialization
instance are copied to the collection instance, or if a span is required the compiler
may use a span of the actual collection length from the intermediate storage.
Otherwise the initialization instance is the collection instance.
If the target type has a create method , the create method is invoked with the span
instance.
Note: The compiler may delay  adding elements to the collection — or delay  iterating
through spread elements — until after evaluating subsequent elements. (When
subsequent spread elements have countable properties that would allow calculating
the expected length of the collection before allocating the collection.) Conversely,
the compiler may eagerly  add elements to the collection — and eagerly  iterate
through spread elements — when there is no advantage to delaying.
Consider the following collection expression:
c#
If spread elements b and c are countable, the compiler could delay adding items
from a and b until after c is evaluated, to allow allocating the resulting array at the
expected length. After that, the compiler could eagerly add items from c, before
evaluating d.
c#int[] x = [a, ..b, ..c, d];
var __tmp1 = a;
var __tmp2 = b;
var __tmp3 = c;
var __result = new int[2 + __tmp2.Length + __tmp3.Length];
int __index = 0;
__result[__index++] = __tmp1;
foreach (var __i in __tmp2) __result[__index++] = __i;
foreach (var __i in __tmp3) __result[__index++] = __i;The empty literal [] has no type. However, similar to the null-lit eral, this literal
can be implicitly converted to any constr uctible  collection type.
For example, the following is not legal as there is no target type  and there are no
other conversions involved:
c#
Spreading an empty literal is permitted to be elided. For example:
c#
Here, if b is false, it is not required that any value actually be constructed for the
empty collection expression since it would immediately be spread into zero values
in the final literal.
The empty collection expression is permitted to be a singleton if used to construct
a final collection value that is known to not be mutable. For example:
c#__result[__index++] = d;
x = __result;
Empty collection literal
var v = []; // illegal
bool b = ...
List<int> l = [x, y, .. b ? [ 1, 2, 3] : []];
// Can be a singleton, like Array.Empty<int>()
int[] x = []; 
// Can be a singleton. Allowed to use Array.Empty<int>(),  
Enumerable.Empty<int>(),
// or any other implementation that can not be mutated.
IEnumerable< int> y = [];
// Must not be a singleton.  Value must be allowed to mutate, and  
should not mutate
// other references elsewhere.
List<int> z = [];See safe context constr aint  for definitions of the safe-c ontext values: declar ation-block ,
function-member , and caller -context.
The safe-c ontext of a collection expression is:
The safe-context of an empty collection expression [] is the caller -context.
If the target type is a span type  System.ReadOnlySpan<T>, and T is one of the
primitiv e types  bool, sbyte, byte, short, ushort, char, int, uint, long, ulong,
float, or double, and the collection expression contains constant v alues only , the
safe-context of the collection expression is the caller -context.
If the target type is a span type  System.Span<T> or System.ReadOnlySpan<T>, the
safe-context of the collection expression is the declar ation-block .
If the target type is a ref str uct type  with a create method , the safe-context of the
collection expression is the safe-c ontext of an in vocation  of the create method
where the collection expression is the span argument to the method.
Otherwise the safe-context of the collection expression is the caller -context.
A collection expression with a safe-context of declar ation-block  cannot escape the
enclosing scope, and the compiler may store the collection on the stack rather than the
heap.
To allow a collection expression for a ref struct type to escape the declar ation-block , it
may be necessary to cast the expression to another type.
C#Ref safety
static ReadOnlySpan< int> AsSpanConstants ()
{
    return [1, 2, 3]; // ok: span refers to assembly data section
}
static ReadOnlySpan<T> AsSpan2<T>(T x, T y)
{
    return [x, y];    // error: span may refer to stack data
}
static ReadOnlySpan<T> AsSpan3<T>(T x, T y, T z)
{
    return (T[])[x, y, z]; // ok: span refers to T[] on heap
}c#
The type infer ence rules are updated as follows.
The existing rules for the first phas e are extracted to a new input type infer ence
section, and a rule is added to input type infer ence and output type infer ence for
collection expression expressions.
11.6.3.2 The first phase
For each of the method arguments Eᵢ:
An input type infer ence is made from Eᵢ to the corresponding paramet er type
Tᵢ.
An input type infer ence is made from an expression E to a type T in the following
way:
If E is a collection expr ession  with elements Eᵢ, and T is a type with an
iteration type  Tₑ or T is a nullable v alue type  T0? and T0 has an iteration
type  Tₑ, then for each Eᵢ:
If Eᵢ is an expression element , then an input type infer ence is made from Eᵢ
to Tₑ.
If Eᵢ is an spread element  with an iteration type  Sᵢ, then a lower-bound
inference is made from Sᵢ to Tₑ.
[existing r ules fr om first phas e] ...
11.6.3.7 Output type inferences
An output type infer ence is made from an expression E to a type T in the following
way:
If E is a collection expr ession  with elements Eᵢ, and T is a type with an
iteration type  Tₑ or T is a nullable v alue type  T0? and T0 has an iteration
type  Tₑ, then for each Eᵢ:Type inference
var a = AsArray([ 1, 2, 3]);          // AsArray<int>(int[])
var b = AsListOfArray([[ 4, 5], []]); // AsListOfArray<int>(List<int[]>)
static T[] AsArray<T>(T[] arg) => arg;
static List<T[]> AsListOfArray<T>(List<T[]> arg) => arg;
If Eᵢ is an expression element , then an output type infer ence is made from
Eᵢ to Tₑ.
If Eᵢ is an spread element , no inference is made from Eᵢ.
[existing r ules fr om output type infer ences] ...
No changes to extension method in vocation  rules.
11.7.8.3 Extension method invocations
An extension method Cᵢ.Mₑ is eligible  if:
...
An implicit identity, reference, or boxing conversion exists from expr to the
type of the first parameter of  Mₑ.
A collection expression does not have a natural type so the existing conversions from
type are not applicable. As a result, a collection expression cannot be used directly as
the first parameter for an extension method invocation.
c#
Better conversion fr om expr ession  is updated to prefer certain target types in collection
expression conversions.
In the updated rules:
A span_type  is one of:
System.Span<T>Extension methods
static class Extensions
{
    public static ImmutableArray<T> AsImmutableArray<T>( this 
ImmutableArray<T> arg) => arg;
}
var x = [1].AsImmutableArray();           // error: collection expression  
has no target type
var y = [2].AsImmutableArray< int>();      // error: ...
var z = Extensions.AsImmutableArray([ 3]); // ok
Overload resolutio n
System.ReadOnlySpan<T>.
An array_or_arr ay_int erface_or_str ing_type  is one of:
an array type
System.String
one of the following interface types  implemented by an array type :
System.Collections.Generic.IEnumerable<T>
System.Collections.Generic.IReadOnlyCollection<T>
System.Collections.Generic.IReadOnlyList<T>
System.Collections.Generic.ICollection<T>
System.Collections.Generic.IList<T>
Given an implicit conversion C₁ that converts from an expression E to a type T₁,
and an implicit conversion C₂ that converts from an expression E to a type T₂, C₁
is a better conversion than C₂ if one of the following holds:
E is a collection expr ession  and one o f the following holds:
T₁ is System.ReadOnlySpan<E₁>, and T₂ is System.Span<E₂>, and an implicit
conv ersion exists fr om E₁ to E₂
T₁ is System.ReadOnlySpan<E₁> or System.Span<E₁>, and T₂ is an
array_or_arr ay_int erface_or_str ing_type  with iteration type  E₂, and an
implicit conv ersion exists fr om E₁ to E₂
T₁ is not a span_type , and T₂ is not a span_type , and an implicit
conv ersion exists fr om T₁ to T₂
E is not a collection expr ession  and one o f the following holds:
E exactly matches T₁ and E does not exactly match T₂
E exactly matches both or neither of T₁ and T₂, and T₁ is a better
conversion t arget  than T₂
E is a method group, ...
Examples of differences with overload resolution between array initializers and collection
expressions:
c#
static void Generic<T>(Span<T> value) { }
static void Generic<T>(T[] value) { }
static void SpanDerived (Span<string> value) { }
static void SpanDerived (object[] value) { }
static void ArrayDerived (Span<object> value) { }
static void ArrayDerived (string[] value) { }The span types ReadOnlySpan<T> and Span<T> are both constr uctible c ollection types .
Support for them follows the design for params Span<T> . Specifically, constructing
either of those spans will result in an array T[] created on the stack  if the params array
is within limits (if any) set by the compiler. Otherwise the array will be allocated on the
heap.
If the compiler chooses to allocate on the stack, it is not required to translate a literal
directly to a stackalloc at that specific point. For example, given:
c#
The compiler is allowed to translate that using stackalloc as long as the Span meaning
stays the same and span-safety  is maintained. For example, it can translate the above
to:
c#// Array initializers
Generic( new[] { "" });      // string[]
SpanDerived( new[] { "" });  // ambiguous
ArrayDerived( new[] { "" }); // string[]
// Collection expressions
Generic([ ""]);              // Span<string>
SpanDerived([ ""]);          // Span<string>
ArrayDerived([ ""]);         // ambiguous
Span types
foreach (var x in y)
{
    Span<int> span = [a, b, c];
    // do things with span
}
Span<int> __buffer = stackalloc  int[3];
foreach (var x in y)
{
    __buffer[ 0] = a
    __buffer[ 1] = b
    __buffer[ 2] = c;
    Span<int> span = __buffer;
    // do things with span
}The compiler can also inline arrays , if available, when choosing to allocate on the
stack.
If the compiler decides to allocate on the heap, the translation for Span<T> is simply:
c#
A collection expression has a known length  if the compile-time type of each spread
element  in the collection expression is countable .
Given a target type IEnumerable<T>, IReadOnlyCollection<T>, IReadOnlyList<T>,
ICollection<T>, or IList<T>a compliant implementation is only required to produce a
value that implements that interface. A compliant implementation is free to:
1. Use an existing type that implements that interface.
2. Synthesize a type that implements the interface.
In either case, the type used is allowed to implement a larger set of interfaces than
those strictly required.
Synthesized types are free to employ any strategy they want to implement the required
interfaces properly. For example, a synthesized type might inline the elements directly
within itself, avoiding the need for additional internal collection allocations. A
synthesized type could also not use any storage whatsoever, opting to compute the
values directly. For example, using Enumerable.Range(1, 10) for [1, 2, 3, 4, 5, 6, 7,
8, 9, 10].
Given a target type or IEnumerable<T>, IReadOnlyCollection<T>, IReadOnlyList<T>, the
value generated is allowed to implement more interfaces than required. For example,
implementing the mutable interfaces as well (specifically, implementing ICollection<T>
or IList<T>). However, in that case:
T[] __array = [...]; // using existing rules
Span<T> __result = __array;
Collection literal translation
Interface translation
Non-mutable interface translation1. The value must return true when queried for ICollection<T>.IsReadOnly. This
ensures consumers can appropriately tell that the collection is non-mutable,
despite implementing the mutable views.
2. The value must throw on any call to a mutation method (like IList<T>.Add). This
ensures safety, preventing a non-mutable collection from being accidentally
mutated.
It is recommended that any type that is synthesized implement all these interfaces. This
ensures that maximal compatibility with existing libraries, including those that introspect
the interfaces implemented by a value in order to light up performance optimizations.
Given a target type or ICollection<T> or IList<T>:
1. The value must return false when queried for ICollection<T>.IsReadOnly.
The value generated is allowed to implement more interfaces than required. Specifically,
implementing IList<T> even when only targeting ICollection<T>. However, in that
case:
1. The value must support all mutation methods (like IList<T>.RemoveAt).
Having a known length  allows for efficient construction of a result with the potential for
no copying of data and no unnecessary slack space in a result.
Not having a known length  does not prevent any result from being created. However, it
may result in extra CPU and memory costs producing the data, then moving to the final
destination.
For a known length  literal [e1, ..s1, etc], the translation first starts with the
following:
c#
Given a target type T for that literal:Mutable interface translation
Known length translation
int __len = count_of_expression_elements +
            __s1.Count;
            ...
            __s_n.Count;If T is some T1[], then the literal is translated as:
c#
The implementation is allowed to utilize other means to populate the array. For
example, utilizing efficient bulk-copy methods like .CopyTo().
If T is some Span<T1>, then the literal is translated as the same as above, except
that the __result initialization is translated as:
c#
The translation may use stackalloc T1[] or an inline arr ay rather than new
T1[] if span-safety  is maintained.
If T is some ReadOnlySpan<T1>, then the literal is translated the same as for the
Span<T1> case except that the final result will be that Span<T1> implicitly
converted  to a ReadOnlySpan<T1>.
A ReadOnlySpan<T1> where T1 is some primitive type, and all collection
elements are constant does not need its data to be on the heap, or on the stack.
For example, an implementation could construct this span directly as a
reference to portion of the data segment of the program.
The above forms (for arrays and spans) are the base representations of the
collection expression and are used for the following translation rules:
If T is some C<S0, S1, …> which has a corresponding create-method
B.M<U0, U1, …>(), then the literal is translated as:
c#T1[] __result = new T1[__len];
int __index = 0;
__result[__index++] = __e1;
foreach (T1 __t in __s1)
    __result[__index++] = __t;
// further assignments of the remaining elements
Span<T1> __result = new T1[__len];
// same assignments as the array translation
As the create method  must have an argument type of some instantiated
ReadOnlySpan<T>, the translation rule for spans applies when passing the
collection expression to the create method.
If T supports collection initializers , then:
if the type T contains an accessible constructor with a single parameter
int capacity, then the literal is translated as:
c#
Note: the name of the parameter is required to be capacity.
This form allows for a literal to inform the newly constructed type of the
count of elements to allow for efficient allocation of internal storage. This
avoids wasteful reallocations as the elements are added.
otherwise, the literal is translated as:
c#
This allows creating the target type, albeit with no capacity optimization to
prevent internal reallocation of storage.// Collection literal is passed as is as the single B.M<...>(...)  
argument
C<S0, S1, …> __result = B.M<S0, S1, …>([...])
T __result = new T(capacity: __len);
__result.Add(__e1);
foreach (var __t in __s1)
    __result.Add(__t);
// further additions of the remaining elements
T __result = new T();
__result.Add(__e1);
foreach (var __t in __s1)
    __result.Add(__t);
// further additions of the remaining elements
Unknown length translationGiven a target type T for an unkno wn length  literal:
If T supports collection initializers , then the literal is translated as:
c#
This allows spreading of any iterable type, albeit with the least amount of
optimization possible.
If T is some T1[], then the literal has the same semantics as:
c#
The above is inefficient though; it creates the intermediary list, and then creates
a copy of the final array from it. Implementations are free to optimize this away,
for example producing code like so:
c#
This allows for minimal waste and copying, without additional overhead that
library collections might incur.
The counts passed to CreateArray are used to provide a starting size hint to
prevent wasteful resizes.
T __result = new T();
__result.Add(__e1);
foreach (var __t in __s1)
    __result.Add(__t);
// further additions of the remaining elements
List<T1> __list = [...]; /* initialized using predefined rules */
T1[] __result = __list.ToArray();
T1[] __result = <private_details>.CreateArray<T1>(
    count_of_expression_elements);
int __index = 0;
<private_details>.Add( ref __result, __index++, __e1);
foreach (var __t in __s1)
    <private_details>.Add( ref __result, __index++, __t);
// further additions of the remaining elements
<private_details>.Resize( ref __result, __index);If T is some span type , an implementation may follow the above T[] strategy,
or any other strategy with the same semantics, but better performance. For
example, instead of allocating the array as a copy of the list elements,
CollectionsMarshal.AsSpan(__list) could be used to obtain a span value
directly.
While collection literals can be used for many scenarios, there are a few that they are
not capable of replacing. These include:
Multi-dimensional arrays (e.g. new int[5, 10] { ... }). There is no facility to
include the dimensions, and all collection literals are either linear or map structures
only.
Collections which pass special values to their constructors. There is no facility to
access the constructor being used.
Nested collection initializers, e.g. new Widget { Children = { w1, w2, w3 } }. This
form needs to stay since it has very different semantics from Children = [w1, w2,
w3]. The former calls .Add repeatedly on .Children while the latter would assign a
new collection over .Children. We could consider having the latter form fall back
to adding to an existing collection if .Children can't be assigned, but that seems
like it could be extremely confusing.
There are two "true" syntactic ambiguities where there are multiple legal syntactic
interpretations of code that uses a collection_literal_expression.
The spread_element is ambiguous with a range_expression . One could
technically have:
c#
To resolve this, we can either:
Require users to parenthesize (..e) or include a start index 0..e if they
want a range.
Choose a different syntax (like ...) for spread. This would be unfortunate for
the lack of consistency with slice patterns.Unsupported scenarios
Syntax ambiguities
Range[] ranges = [range1, ..e, range2];There are two cases where there isn't a true ambiguity but where the syntax greatly
increases parsing complexity. While not a problem given engineering time, this
does still increase cognitive overhead for users when looking at code.
Ambiguity between collection_literal_expression and attributes on
statements or local functions. Consider:
c#
This could be one of:
c#
Without complex lookahead, it would be impossible to tell without consuming
the entirety of the literal.
Options to address this include:
Allow this, doing the parsing work to determine which of these cases this is.
Disallow this, and require the user wrap the literal in parentheses like ([X(),
Y, Z()]).ForEach(...).
Ambiguity between a collection_literal_expression in a
conditional_expression and a null_conditional_operations. Consider:
c#
This could be one of:
c#[X(), Y, Z() ]
// A list literal inside some expression statement
[X(), Y, Z() ].ForEach(() => ...);
// The attributes for a statement or local function
[X(), Y, Z() ] void LocalFunc () { }
M(x ? [a, b, c]
// A ternary conditional picking between two collections
M(x ? [a, b, c] : [d, e, f]);
// A null conditional safely indexing into 'x':
M(x ? [a, b, c]);Without complex lookahead, it would be impossible to tell without consuming
the entirety of the literal.
Note: this is a problem even without a natur al type  because target typing
applies through conditional_expressions.
As with the others, we could require parentheses to disambiguate. In other
words, presume the null_conditional_operation interpretation unless written
like so: x ? ([1, 2, 3]) :. However, that seems rather unfortunate. This sort of
code does not seem unreasonable to write and will likely trip people up.
This introduces yet another form  for collection expressions on top of the myriad
ways we already have. This is extra complexity for the language. That said, this also
makes it possible to unify on one ring syntax to rule them all, which means existing
codebases can be simplified and moved to a uniform look everywhere.
Using [...] instead of {...} moves away from the syntax we've generally used for
arrays and collection initializers already. Specifically that it uses [...] instead of
{...}. However, this was already settled on by the language team when we did list
patterns. W e attempted to make {...} work with list patterns and ran into
insurmountable issues. Because of this, we moved to [...] which, while new for C#,
feels natural in many programming languages and allowed us to start fresh with
no ambiguity. Using [...] as the corresponding literal form is complementary with
our latest decisions, and gives us a clean place to work without problem.
This does introduce warts into the language. For example, the following are both legal
and (fortunately) mean the exact same thing:
c#
However, given the breadth and consistency brought by the new literal syntax, we
should consider recommending that people move to the new form. IDE suggestions and
fixes could help in that regard.
What other designs have been considered? What is the impact of not doing this?Drawbacks
int[] x = { 1, 2, 3 };
int[] x = [ 1, 2, 3 ];
AlternativesShould the compiler use stackalloc for stack allocation when inline arr ays are not
available and the iteration type  is a primitive type?
Resolution: No. Managing a stackalloc buffer requires additional effort over an
inline arr ay to ensure the buffer is not allocated repeatedly when the collection
expression is within a loop. The additional complexity in the compiler and in the
generated code outweighs the benefit of stack allocation on older platforms.
In what order should we evaluate literal elements compared with Length/Count
property evaluation? Should we evaluate all elements first, then all lengths? Or
should we evaluate an element, then its length, then the next element, and so on?
Resolution: W e evaluate all elements first, then everything else follows that.
Can an unkno wn length  literal create a collection type that needs a known length ,
like an array, span, or Construct(array/span) collection? This would be harder to do
efficiently, but it might be possible through clever use of pooled arrays and/or
builders.
Resolution: Y es, we allow creating a fixes-length collection from an unkno wn length
literal. The compiler is permitted to implement this in as efficient a manner as
possible.
The following text exists to record the original discussion of this topic.
Details
Users could always make an unkno wn length  literal into a known length  one with
code like this:
c#
However, this is unfortunate due to the need to force allocations of temporary
storage. W e could potentially be more efficient if we controlled how this was
emitted.
Can a collection_expression be target-typed to an IEnumerable<T> or other
collection interfaces?
For example:Resolved questions
ImmutableArray< int> x = [a, ..unknownLength.ToArray(), b];c#
Resolution: Y es, a literal can be target-typed to any interface type I<T> that
List<T> implements. For example, IEnumerable<long>. This is the same as target-
typing to List<long> and then assigning that result to the specified interface type.
The following text exists to record the original discussion of this topic.
Details
The open question here is determining what underlying type to actually create.
One option is to look at the proposal for params IEnumerable<T> . There, we
would generate an array to pass the values along, similar to what happens with
params T[].
Can/should the compiler emit Array.Empty<T>() for []? Should we mandate that
it does this, to avoid allocations whenever possible?
Yes. The compiler should emit Array.Empty<T>() for any case where this is legal
and the final result is non-mutable. For example, targeting T[], IEnumerable<T>,
IReadOnlyCollection<T> or IReadOnlyList<T>. It should not use Array.Empty<T>
when the target is mutable ( ICollection<T> or IList<T>).
Should we expand on collection initializers to look for the very common AddRange
method? It could be used by the underlying constructed type to perform adding of
spread elements potentially more efficiently. W e might also want to look for things
like .CopyTo as well. There may be drawbacks here as those methods might end up
causing excess allocations/dispatches versus directly enumerating in the translated
code.
Yes. An implementation is allowed to utilize other methods to initialize a collection
value, under the presumption that these methods have well-defined semantics,
and that collection types should be "well behaved". In practice though, an
implementation should be cautious as benefits in one way (bulk copying) may
come with negative consequences as well (for example, boxing a struct collection).
An implementation should take advantage in the cases where there are no
downsides. For example, with an .AddRange(ReadOnlySpan<T>) method.void DoWork(IEnumerable< long> values ) { ... }
// Needs to produce `longs` not `ints` for this to work.
DoWork([ 1, 2, 3]);
Unresolved questionsShould it be legal to create and immediately index into a collection literal? Note:
this requires an answer to the unresolved question below of whether collection
literals have a natur al type .
Stack allocations for huge collections might blow the stack. Should the compiler
have a heuristic for placing this data on the heap? Should the language be
unspecified to allow for this flexibility? W e should follow the spec for params
Span<T> .
Do we need to target-type spread_element? Consider, for example:
c#
Note: this may commonly come up in the following form to allow conditional
inclusion of some set of elements, or nothing if the condition is false:
c#
In order to evaluate this full literal, we need to evaluate the element expressions
within. That means being able to evaluate b ? [c] : [d, e]. However, absent a
target type to evaluate this expression in the context of, and absent any sort of
natur al type , this would we would be unable to determine what to do with either
[c] or [d, e] here.
To resolve this, we could say that when evaluating a literal's spread_element
expression, there was an implicit target type equivalent to the target type of the
literal itself. So, in the above, that would be rewritten as:
c#
Span<int> span = [a, ..b ? [c] : [d, e], f];
Span<int> span = [a, ..b ? [c, d, e] : [], f];
int __e1 = a;
Span<int> __s1 = b ? [c] : [d, e];
int __e2 = f;
Span<int> __result = stackalloc  int[2 + __s1.Length];
int __index = 0;
__result[__index++] = a;
foreach (int __t in __s1)
  __result[index++] = __t;
__result[__index++] = f;https://github.com/dotnet/csharplang/blob/main/meetings/2021/LDM-2021-11-
01.md#collection-literals
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-03-
09.md#ambiguity-of--in-collection-expressions
https://github.com/dotnet/csharplang/blob/main/meetings/2022/LDM-2022-09-
28.md#collection-literals
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2022-10-06.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2022-10-14.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2022-10-21.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-04-05.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-04-28.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-05-26.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-06-12.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-06-26.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-08-03.md
https://github.com/dotnet/csharplang/blob/main/meetings/working-groups/collection-
literals/CL-2023-08-10.md
Stack allocations for huge collections might blow the stack. Should the compiler
have a heuristic for placing this data on the heap? Should the language beSpan<int> span = __result;
Design meetings
Working group meetings
Upcoming agenda itemsunspecified to allow for this flexibility? W e should follow what the spec/impl does
for params Span<T> . Options are:
Always stackalloc. T each people to be careful with Span. This allows things like
Span<T> span = [1, 2, ..s] to work, and be fine as long as s is small. If this
could blow the stack, users could always create an array instead, and then get a
span around this. This seems like the most in line with what people might want,
but with extreme danger.
Only stackalloc when the literal has a fixed number of elements (i.e. no spread
elements). This then likely makes things always safe, with fixed stack usage, and
the compiler (hopefully) able to reuse that fixed buffer. However, it means
things like [1, 2, ..s] would never be possible, even if the user knows it is
completely safe at runtime.
How does overload resolution work? If an API has:
C#
What happens with M([1, 2, 3])? We likely need to define 'betterness' for these
conversions.
Should we expand on collection initializers to look for the very common AddRange
method? It could be used by the underlying constructed type to perform adding of
spread elements potentially more efficiently. W e might also want to look for things
like .CopyTo as well. There may be drawbacks here as those methods might end up
causing excess allocations/dispatches versus directly enumerating in the translated
code.
Generic type inference should be updated to flow type information to/from
collection literals. For example:
C#
It seems natural that this should be something the inference algorithm can be
made aware of. Once this is supported for the 'base' constructible collection type
cases (T[], I<T>, Span<T> new T()), then it should also fall out of the
Collect(constructible_type) case. For example:
public void M(T[] values );
public void M(List<T> values );
void M<T>(T[] values);
M([1, 2, 3]);C#
Here, Immutable<T> is constructible through an init void Construct(T[] values)
method. So the T[] values type would be used with inference against [1, 2, 3]
leading to an inference of int for T.
Cast/Index ambiguity.
Today the following is an expression that is indexed into
c#
But it would be nice to be able to do things like:
c#
Can/should we take a break here?
Syntactic ambiguities with ?[.
It might be worthwhile to change the rules for nullable index access to state that
no space can occur between ? and [. That would be a breaking change (but likely
minor as VS already forces those together if you type them with a space). If we do
this, then we can have x?[y] be parsed differently than x ? [y].
A similar thing occurs if we want to go with
https://github.com/dotnet/csharplang/issues/2926 . In that world x?.y is
ambiguous with x ? .y. If we require the ?. to abut, we can syntactically
distinguish the two cases trivially.void M<T>(ImmutableArray<T> values);
M([1, 2, 3]);
var v = (Expr)[ 1, 2, 3];
var v = (ImmutableArray< int>)[1, 2, 3];
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where youC# featur e specification
feedb ack
C# feature specification is an open
source project. Select a link tocan also create and review
issues and pull requests. For
more information, see our
contributor guide .provide feedback:
 Open a documentation issue
 Provide product feedbackAllow using alias directive to reference
any kind of Type
Article •08/16/2023
Relax the using_alias_directive ( §13.5.2 ) to allow it to point at any sort of type, not just
named types. This would support types not allowed today, like: tuple types, pointer
types, array types, etc. For example, this would now be allowed:
c#
For ages, C# has had the ability to introduce aliases for namespaces and named types
(classes, delegated, interfaces, records and structs). This worked acceptably well as it
provided a means to introduce non-conflicting names in cases where a normal named
pulled in from using_directives might be ambiguous, and it allowed a way to provide a
simpler name when dealing with complex generic types. However, the rise of additional
complex type symbols in the language has caused more use to arise where aliases
would be valuable but are currently not allowed. For example, both tuples and function-
pointers often can have large and complex regular textual forms that can be painful to
continually write out, and a burden to try to read. Aliases would help in these cases by
giving a short, developer-provided, name that can then be used in place of those full
structural forms.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
using Point = ( int x, int y);
MotivationWe will change the grammar of using_alias_directive thusly:
Top-level reference type nullability annotations are disallowed.
Interestingly, most of the spec language in §13.5.2  does not need to change. Most
language in it already refers to 'namespace or type', for example:
A using_alias_directive introduces an identifier that serves as an alias for a
namespace or type within the immediately enclosing compilation unit or namespace
body.
This remains true, just that the grammar now allows the 'type' to be any arbitrary type,
not the limited set allowed for by namespace_or_type_name previously.
The sections that do need updating are:
diffDetailed design
using_alias_directive
-    : 'using' identifier '=' namespace_or_type_name ';'
+    : 'using' identifier '=' (namespace_name | type) ';'
    ;
- The order in which using_alias_directives are written has no significance,  
and resolution of the namespace_or_type_name referenced by a  
using_alias_directive is not affected by the using_alias_directive itself or  
by other using_directives in the immediately containing compilation unit or  
namespace body. In other words, the namespace_or_type_name of a  
using_alias_directive is resolved as if the immediately containing  
compilation unit or namespace body had no using_directives. A  
using_alias_directive may however be affected by extern_alias_directives in  
the immediately containing compilation unit or namespace body. In the  
example
+ The order in which using_alias_directives are written has no significance,  
and resolution of the `(namespace_name | type)` referenced by a  
using_alias_directive is not affected by the using_alias_directive itself or  
by other using_directives in the immediately containing compilation unit or  
namespace body. In other words, the `(namespace_name | type)` of a  
using_alias_directive is resolved as if the immediately containing  
compilation unit or namespace body had no using_directives. A  
using_alias_directive may however be affected by extern_alias_directives in  
the immediately containing compilation unit or namespace body. In the  
examplediff
diff
A new unsafe context  is added through an optional 'unsafe' keyword in the
using_alias_directive production:
diff- The namespace_name referenced by a using_namespace_directive is resolved  
in the same way as the namespace_or_type_name referenced by a  
using_alias_directive. Thus, using_namespace_directives in the same  
compilation unit or namespace body do not affect each other and can be  
written in any order.
+ The namespace_name referenced by a using_namespace_directive is resolved  
in the same way as the namespace_or_type_name referenced by a  
using_alias_directive. Thus, using_namespace_directives in the same  
compilation unit or namespace body do not affect each other and can be  
written in any order.
+ It is illegal for a using alias type to be a nullable reference type.
    1. `using X = string?;` is not legal.
    2. `using X = List<string?>;` is legal.  The alias is to `List<...>`  
which is itself not a nullable reference type itself, even though it  
contains one as a type argument.
    3. `using X = int?;` is legal.  This is a nullable *value* type, not a  
nullable *reference* type.
Supporting aliases to types containing
pointers.
using_alias_directive
+    : 'using' 'unsafe'? identifier '=' (namespace_name | type) ';'
    ;
    
using_static_directive
+    : 'using' 'static' 'unsafe'? type_name ';'
    ;
+ 'unsafe' can only be used with an using_alias_directive or  
using_static_directive, not a using_directive.
+ The 'unsafe' keyword present in a 'using_alias_directive' causes the  
entire textual extent of the 'type' portion (not the 'namespace_name'  
portion) to become an unsafe context. 
+ The 'unsafe' keyword present in a 'using_static_directive' causes the  entire textual extent of the 'type_name' portion to become an unsafe  
context. 
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackOptional and parameter array
parameters for lambdas and method
groups
Article •08/16/2023
To build on top of the lambda improvements introduced in C# 10 (see relevant
background ), we propose adding support for default parameter values and params
arrays in lambdas. This would enable users to implement the following lambdas:
C#
Similarly, we will allow the same kind of behavior for method groups:
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
var addWithDefault = ( int addTo = 2) => addTo + 1;
addWithDefault(); // 3
addWithDefault( 5); // 6
var counter = ( params int[] xs) => xs.Length;
counter(); // 0
counter( 1, 2, 3); // 3
var addWithDefault = AddWithDefaultMethod;
addWithDefault(); // 3
addWithDefault( 5) // 6
var counter = CountMethod;
counter(); // 0Lambda Improvements in C# 10
Method group conversion specification §10.8
App frameworks in the .NET ecosystem leverage lambdas heavily to allow users to
quickly write business logic associated with an endpoint.
C#
Lambdas don't currently support setting default values on parameters, so if a developer
wanted to build an application that was resilient to scenarios where users didn't provide
data, they're left to either use local functions or set the default values within the lambda
body, as opposed to the more succinct proposed syntax.
C#counter( 1, 2); // 2
int AddWithDefaultMethod (int addTo = 2) {
  return addTo + 1;
}
int CountMethod (params int[] xs) {
  return xs.Length;
}
Relevant background
Motivation
var app = WebApplication.Create(args);
app.MapPost( "/todos/{id}" , (TodoService todoService, int id, string task) =>  
{
  var todo = todoService.Create(id, task);
  return Results.Created(todo);
});
var app = WebApplication.Create(args);
app.MapPost( "/todos/{id}" , (TodoService todoService, int id, string task = 
"foo") => {
  var todo = todoService.Create(id, task);
  return Results.Created(todo);
});The proposed syntax also has the benefit of reducing confusing differences between
lambdas and local functions, making it easier to reason about constructs and "grow up"
lambdas to functions without compromising features, particularly in other scenarios
where lambdas are used in APIs where method groups can also be provided as
references. This is also the main motivation for supporting the params array which is not
covered by the aforementioned use-case scenario.
For example:
C#
Currently, when a user implements a lambda with an optional or params parameter, the
compiler raises an error.
C#
When a user attempts to use a method group where the underlying method has an
optional or params parameter, this information isn't propagated, so the call to the
method doesn't typecheck due to a mismatch in the number of expected arguments.
C#var app = WebApplication.Create(args);
Result TodoHandler (TodoService todoService, int id, string task = "foo") {
  var todo = todoService.Create(id, task);
  return Results.Created(todo);
}
app.MapPost( "/todos/{id}" , TodoHandler);
Current behavior
var addWithDefault = ( int addTo = 2) => addTo + 1; // error CS1065: Default  
values are not valid in this context.
var counter = ( params int[] xs) => xs.Length; // error CS1670: params is not  
valid in this context
void M1(int i = 1) { }
var m1 = M1; // Infers Action<int>
m1(); // error CS7036: There is no argument given that corresponds to the  
required parameter 'obj' of 'Action<int>'
void M2(params int[] xs) { }
var m2 = M2; // Infers Action<int[]>Following this proposal, default values and params can be applied to lambda parameters
with the following behavior:
C#
Default values and params can be applied to method group parameters by specifically
defining such method group:
C#
Currently, the inferred type of a method group is Action or Func so the following code
compiles:
C#m2(); // error CS7036: There is no argument given that corresponds to the  
required parameter 'obj' of 'Action<int[]>'
New behavior
var addWithDefault = ( int addTo = 2) => addTo + 1;
addWithDefault(); // 3
addWithDefault( 5); // 6
var counter = ( params int[] xs) => xs.Length;
counter(); // 0
counter( 1, 2, 3); // 3
int AddWithDefault (int addTo = 2) {
  return addTo + 1;
}
var add1 = AddWithDefault; 
add1(); // ok, default parameter value will be used
int Counter(params int[] xs) {
  return xs.Length;
}
var counter1 = Counter;
counter1( 1, 2, 3); // ok, `params` will be used
Breaking changeFollowing this change, code of this nature would cease to compile in .NET SDK 7.0.200
or later.
C#void WriteInt (int i = 0) {
  Console.Write(i);
}
var writeInt = WriteInt; // Inferred as Action<int>
DoAction(writeInt, 3); // Ok, writeInt is an Action<int>
void DoAction (Action<int> a, int p) {
  a(p);
}
int Count(params int[] xs) {
  return xs.Length;
}
var counter = Count; // Inferred as Func<int[], int>
DoFunction(counter, 3); // Ok, counter is a Func<int[], int>
int DoFunction (Func<int[], int> f, int p) {
  return f(new[] { p });
}
void WriteInt (int i = 0) {
  Console.Write(i);
}
var writeInt = WriteInt; // Inferred as anonymous delegate type
DoAction(writeInt, 3); // Error, cannot convert from anonymous delegate type  
to Action
void DoAction (Action<int> a, int p) {
  a(p);
}
int Count(params int[] xs) {
  return xs.Length;
}
var counter = Count; // Inferred as anonymous delegate type
DoFunction(counter, 3); // Error, cannot convert from anonymous delegate  
type to Func
int DoFunction (Func<int[], int> f, int p) {
  return f(new[] { p });
}The impact of this breaking change needs to be considered. Fortunately, the use of var
to infer the type of a method group has only been supported since C# 10, so only code
which has been written since then which explicitly relies on this behavior would break.
This enhancement requires the following changes to the grammar for lambda
expressions.
diff
Note that this allows default parameter values and params arrays only for lambdas, not
for anonymous methods declared with delegate { } syntax.
Same rules as for method parameters ( §14.6.2 ) apply for lambda parameters:
A parameter with a ref, out or this modifier cannot have a default_ar gument .
A paramet er_arr ay may occur after an optional parameter, but cannot have a
default value – the omission of arguments for a paramet er_arr ay would instead
result in the creation of an empty array.
No changes to the grammar are necessary for method groups since this proposal would
only change their semantics.Detailed design
Grammar and parser changes
 lambda_expression
   : modifier* identifier '=>' (block | expression)
-  | attribute_list* modifier* type? lambda_parameters '=>' (block |  
expression)
+  | attribute_list* modifier* type? lambda_parameter_list '=>' (block |  
expression)
   ;
+lambda_parameter_list
+  : lambda_parameters (',' parameter_array)?
+  | parameter_array
+  ;
 lambda_parameter
   : identifier
-  | attribute_list* modifier* type? identifier
+  | attribute_list* modifier* type? identifier default_argument?
   ;
The following addition (in bold) is required to anonymous function conversions
(§10.7 ):
Specifically, an anonymous function F is compatible with a delegate type D
provided:
[...]
If F has an explicitly typed parameter list, each parameter in D has the same
type and modifiers as the corresponding parameter in F ignoring params
modifier s and default v alues .
The following addition (in bold) is required to the function types  specification in a
prior proposal:
The natural type of an anonymous function expression or method group is a
function_type . A function_type  represents a method signature: the parameter types,
default v alues, r ef kinds, params modifier s, and return type and ref kind.
Anonymous function expressions or method groups with the same signature have
the same function_type .
The following addition (in bold) is required to the delegate types  specification in a
prior proposal:
The delegate type for the anonymous function or method group with parameter
types P1, ..., Pn and return type R is:
if any parameter or return value is not by value, or any p aramet er is optional
or params, or there are more than 16 parameters, or any of the parameter
types or return are not valid type arguments (say, (int* p) => { }), then the
delegate is a synthesized internal anonymous delegate type with signature
that matches the anonymous function or method group, and with parameter
names arg1, ..., argn or arg if a single parameter; [...]
Updates of prior proposals
Binder changes
Synthesizing new delegate typesAs with the behavior for delegates with ref or out parameters, delegate types are
synthesized for lambdas or method groups defined with optional or params parameters.
Note that in the below examples, the notation a', b', etc. is used to represent these
anonymous delegate types.
C#
Anonymous delegates with optional parameters will be unified when the same
parameter (based on position) has the same default value, regardless of parameter
name.
C#var addWithDefault = ( int addTo = 2) => addTo + 1;
// internal delegate int a'(int arg = 2);
var printString = ( string toPrint = "defaultString" ) => 
Console.WriteLine(toPrint);
// internal delegate void b'(string arg = "defaultString");
var counter = ( params int[] xs) => xs.Length;
// internal delegate int c'(params int[] arg);
string PathJoin (string s1, string s2, string sep = "/") { return $"{s1}{sep}
{s2}"; }
var joinFunc = pathJoin;
// internal delegate string d'(string arg1, string arg2, string arg3 = " ");
Conversion and unification behavior
int E(int j = 13) {
  return 11;
}
int F(int k = 0) {
  return 3;
}
int G(int x = 13) {
  return 4;
}
var a = (int i = 13) => 1;
// internal delegate int b'(int arg = 13);
var b = (int i = 0) => 2;
// internal delegate int c'(int arg = 0);
var c = (int i = 13) => 3;
// internal delegate int b'(int arg = 13);
var d = (int c = 13) => 1;
// internal delegate int b'(int arg = 13);
var e = E;Anonymous delegates with an array as the last parameter will be unified when the last
parameter has the same params modifier and array type, regardless of parameter name.
C#// internal delegate int b'(int arg = 13);
var f = F;
// internal delegate int c'(int arg = 0);
var g = G;
// internal delegate int b'(int arg = 13);
a = b; // Not allowed
a = c; // Allowed
a = d; // Allowed
c = e; // Allowed
e = f; // Not Allowed
b = f; // Allowed
e = g; // Allowed
d = (int c = 10) => 2; // Error: default parameter value is different  
between new lambda
                       // and synthesized delegate b'. We won't do implicit  
conversion
int C(int[] xs) {
  return xs.Length;
}
int D(params int[] xs) {
  return xs.Length;
}
var a = (int[] xs) => xs.Length;
// internal delegate int a'(int[] xs);
var b = (params int[] xs) => xs.Length;
// internal delegate int b'(params int[] xs);
var c = C;
// internal delegate int a'(int[] xs);
var d = D;
// internal delegate int b'(params int[] xs);
a = b; // Not allowed
a = c; // Allowed
b = c; // Not allowed
b = d; // Allowed
c = (params int[] xs) => xs.Length; // Error: different delegate types; no  
implicit conversion
d = (int[] xs) => xs.Length; // Error: different delegate types; no implicit  
conversionSimilarly, there is of course compatibility with named delegates that already support
optional and params parameters. When default values or params modifiers differ in a
conversion, the source one will be unused if it's in a lambda expression, since the
lambda cannot be called in any other way. That might seem counter-intuitive to users,
hence a warning will be emitted when the source default value or params modifier is
present and different from the target one. If the source is a method group, it can be
called on its own, hence no warning will be emitted.
C#
The default parameter values will be emitted to metadata. The IL for this feature will be
very similar in nature to the IL emitted for lambdas with ref and out parameters. A
class which inherits from System.Delegate or similar will be generated, and the Invoke
method will include .param directives to set default parameter values ordelegate  int DelegateNoDefault (int x);
delegate  int DelegateWithDefault (int x = 1);
int MethodNoDefault (int x) => x;
int MethodWithDefault (int x = 2) => x;
DelegateNoDefault d1 = MethodWithDefault; // no warning: source is a method  
group
DelegateWithDefault d2 = MethodWithDefault; // no warning: source is a  
method group
DelegateWithDefault d3 = MethodNoDefault; // no warning: source is a method  
group
DelegateNoDefault d4 = ( int x = 1) => x; // warning: source present, target  
missing
DelegateWithDefault d5 = ( int x = 2) => x; // warning: source present,  
target different
DelegateWithDefault d6 = ( int x) => x; // no warning: source missing, target  
present
delegate  int DelegateNoParams (int[] xs);
delegate  int DelegateWithParams (params int[] xs);
int MethodNoParams (int[] xs) => xs.Length;
int MethodWithParams (params int[] xs) => xs.Length;
DelegateNoParams d7 = MethodWithParams; // no warning: source is a method  
group
DelegateWithParams d8 = MethodNoParams; // no warning: source is a method  
group
DelegateNoParams d9 = ( params int[] xs) => xs.Length; // warning: source  
present, target missing
DelegateWithParams d10 = ( int[] xs) => xs.Length; // no warning: source  
missing, target present
IL/runtime behaviorSystem.ParamArrayAttribute – just as would be the case for a standard named delegate
with optional or params parameters.
These delegate types can be inspected at runtime, as normal. In code, users can
introspect the DefaultValue in the ParameterInfo associated with the lambda or
method group by using the associated MethodInfo.
C#
Open question:  how does this interact with the existing DefaultParameterValue
attribute?
Proposed answ er: For parity, permit the DefaultParameterValue attribute on lambdas
and ensure that the delegate generation behavior matches for default parameter values
supported via the syntax.
C#
Open question:  First, note that this is outside the scope of the current proposal but it
might be worth discussing in the future. Do we want to support defaults with implicitly
typed lambda parameters? I.e.,
C#var addWithDefault = ( int addTo = 2) => addTo + 1;
void AddWithDefaultMethod (int addTo = 2) {
  return addTo + 1;
}
addWithDefault.Method.GetParameters()[ 0].DefaultValue; // 2
var add1 = AddWithDefaultMethod;
add1.Method.GetParameters()[ 0].DefaultValue; // 2
Open questions
var a = (int i = 13) => 1;
// same as
var b = ([DefaultParameterValue( 13)] int i) => 1;
b = a; // Allowed
delegate  void M1(int i = 3);
M1 m = (x = 3) => x + x; // Ok
delegate  void M2(long i = 2);This inference leads to some tricky conversion issues which would require more
discussion.
There are also parsing performance considerations here. For instance, today the term (x
= could never be the start of a lambda expression. If this syntax was allowed for lambda
defaults, then the parser would need a larger lookahead (scanning all the way until a =>
token) in order to determine whether a term is a lambda or not.
LDM 2022-10-10 : decision to add support for params in the same way as default
parameter values.M2 m = (x = 3.0) => ...; //Error: cannot convert implicitly from long to  
double
Design meetings
Inline Arrays
Article •08/16/2023
Provide a general-purpose and safe mechanism for consuming struct types utilizing
InlineArrayAttribute  feature. Provide a general-purpose and safe mechanism for
declaring inline arrays within C# classes, structs, and interfaces.
Note: Previous versions of this spec used the terms "ref-safe-to-escape" and "safe-
to-escape", which were introduced in the Span safety  feature specification. The
ECMA standard committee  changed the names to "ref-safe-context"  and "safe-
context" , respectively. The values of the safe context have been refined to use
"declaration-block", "function-member", and "caller-context" consistently. The
speclets had used different phrasing for these terms, and also used "safe-to-return"
as a synonym for "caller-context". This speclet has been updated to use the terms in
the C# 7.3 standard.
This proposal plans to address the many limitations of
https://github.com/dotnet/csharpstandard/blob/draft-v8/standard/unsafe-
code.md#228-fixed-size-buffers . Specifically it aims to allow:
accessing elements of struct types utilizing InlineArrayAttribute  feature;
the declaration of inline arrays for managed and unmanaged types in a struct,
class, or interface.
And provide language safety verification for them.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
Summary
Motivation
Recently runtime added InlineArrayAttribute  feature. In short, a user can declare a
structure type like the following:
C#
Runtime provides a special type layout for the Buffer type:
The size of the type is extended to fit 10 (the number comes from the InlineArray
attribute) elements of object type (the type comes from the type of the only
instance field in the struct, _element0 in this example).
The first element is aligned with the instance field and with the beginning of the
struct
The elements are laid out sequentially in memory as though they are elements of
an array.
Runtime provides regular GC tracking for all elements in the struct.
This proposal will refer to types like this as "inline array types".
Elements of an inline array type can be accessed through pointers or through span
instances returned by
System.Runtime.InteropServices.MemoryMarshal.CreateSpan /System.Runtime.InteropSer
vices.MemoryMarshal.CreateR eadOnlySpan  APIs. However, neither the pointer
approach, nor the APIs provide type and bounds checking out of the box.
Language will provide a type-safe/ref-safe way for accessing elements of inline array
types. The access will be span based. This limits support to inline array types with
element types that can be used as a type argument. For example, a pointer type cannot
be used as an element type. Other examples the span types.
Since there is a guarantee that the first element in an inline array type is aligned at the
beginning of the type (no gap), compiler will use the following code to get a Span value:
C#Detailed Design
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct Buffer
{
    private object _element0;
}
Obtaining instances of span types for an inline array typeAnd the following code to get a ReadOnlySpan value:
C#
In order to reduce IL size at use sites compiler should be able to add two generic
reusable helpers into private implementation detail type and use them across all use
sites in the same program.
C#
The Element access  will be extended to support inline array element access.
An element_ac cess consists of a primary_no_arr ay_cr eation_expr ession , followed by a “ [”
token, followed by an argument_list , followed by a “ ]” token. The argument_list  consists
of one or more argument s, separated by commas.
ANTLR
The argument_list  of an element_ac cess is not allowed to contain ref or out arguments.MemoryMarshal.CreateSpan( ref Unsafe.As<TBuffer, TElement>( ref buffer), size)
MemoryMarshal.CreateReadOnlySpan( ref Unsafe.As<TBuffer, TElement>( ref 
Unsafe.AsRef( in buffer)), size)
public static System.Span<TElement> InlineArrayAsSpan<TBuffer, TElement>( ref 
TBuffer buffer, int size) where TBuffer : struct
{
    return MemoryMarshal.CreateSpan( ref Unsafe.As<TBuffer, TElement>( ref 
buffer), size);
}
public static System.ReadOnlySpan<TElement>  
InlineArrayAsReadOnlySpan<TBuffer, TElement>( in TBuffer buffer, int size) 
where TBuffer : struct
{
    return MemoryMarshal.CreateReadOnlySpan( ref Unsafe.As<TBuffer, TElement>
(ref Unsafe.AsRef( in buffer)), size);
}
Element access
element_access
    : primary_no_array_creation_expression '[' argument_list ']'
    ;An element_ac cess is dynamically bound ( §11.3.3 ) if at least one of the following holds:
The primary_no_arr ay_cr eation_expr ession  has compile-time type dynamic.
At least one expression of the argument_list  has compile-time type dynamic and
the primary_no_arr ay_cr eation_expr ession  does not have an array type, and the
primar y_no_arr ay_cr eation_expr ession  does not hav e an inline array type or
there is mor e than one it em in the ar gument list .
In this case, the compiler classifies the element_ac cess as a value of type dynamic. The
rules below to determine the meaning of the element_ac cess are then applied at run-
time, using the run-time type instead of the compile-time type of those of the
primary_no_arr ay_cr eation_expr ession  and argument_list  expressions which have the
compile-time type dynamic. If the primary_no_arr ay_cr eation_expr ession  does not have
compile-time type dynamic, then the element access undergoes a limited compile-time
check as described in §11.6.5 .
If the primary_no_arr ay_cr eation_expr ession  of an element_ac cess is a value of an
array_type , the element_ac cess is an array access ( §11.7.10.2 ). If the
primar y_no_arr ay_cr eation_expr ession  of an element_ac cess is a v ariable or v alue o f an
inline array type and the argument_list  consists o f a single ar gument, the
element_ac cess is an inline array element access.  Otherwise, the
primary_no_arr ay_cr eation_expr ession  shall be a variable or value of a class, struct, or
interface type that has one or more indexer members, in which case the element_ac cess
is an indexer access ( §11.7.10.3 ).
For an inline array element access, the primary_no_arr ay_cr eation_expr ession  of the
element_ac cess must be a variable or value of an inline array type. Furthermore, the
argument_list  of an inline array element access is not allowed to contain named
arguments. The argument_list  must contain a single expression, and the expression must
be
of type int, or
implicitly convertible to int, or
implicitly convertible to System.Index, or
implicitly convertible to System.Range.
Inline array element access
When the expression type is intIf primary_no_arr ay_cr eation_expr ession  is a writable variable, the result of evaluating an
inline array element access is a writable variable equivalent to invoking public ref T
this[int index] { get; }  with that integer value on an instance of System.Span<T> returned
by System.Span<T> InlineArrayAsSpan method on primary_no_arr ay_cr eation_expr ession .
For the purpose of ref-safety analysis the ref-safe-c ontext/safe-c ontext of the access are
equivalent to the same for an invocation of a method with the signature static ref T
GetItem(ref InlineArrayType array). The resulting variable is considered movable if and
only if primary_no_arr ay_cr eation_expr ession  is movable.
If primary_no_arr ay_cr eation_expr ession  is a readonly variable, the result of evaluating an
inline array element access is a readonly variable equivalent to invoking public ref
readonly T this[int index] { get; }  with that integer value on an instance of
System.ReadOnlySpan<T> returned by System.ReadOnlySpan<T>
InlineArrayAsReadOnlySpan method on primary_no_arr ay_cr eation_expr ession . For the
purpose of ref-safety analysis the ref-safe-c ontext/safe-c ontext of the access are
equivalent to the same for an invocation of a method with the signature static ref
readonly T GetItem(in InlineArrayType array). The resulting variable is considered
movable if and only if primary_no_arr ay_cr eation_expr ession  is movable.
If primary_no_arr ay_cr eation_expr ession  is a value, the result of evaluating an inline array
element access is a value equivalent to invoking public ref readonly T this[int index] {
get; }  with that integer value on an instance of System.ReadOnlySpan<T> returned by
System.ReadOnlySpan<T> InlineArrayAsReadOnlySpan method on
primary_no_arr ay_cr eation_expr ession . For the purpose of ref-safety analysis the ref-safe-
context/safe-c ontext of the access are equivalent to the same for an invocation of a
method with the signature static T GetItem(InlineArrayType array).
For example:
C#
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct Buffer10<T>
{
    private T _element0;
}
void M1(Buffer10< int> x)
{
    ref int a = ref x[0]; // Ok, equivalent to `ref int a = ref  
InlineArrayAsSpan<Buffer10<int>, int>(ref x, 10)[0]`
}
void M2(in Buffer10< int> x)
{Indexing into an inline array with a constant expression outside of the declared inline
array bounds is a compile time error.
The expression is converted to int and then the element access is interpreted as
described in When the expr ession type is int  section.
The expression is converted to System.Index, which is then transformed to an int-based
index value as described at
https://github.com/dotnet/csharplang/blob/main/proposals/csharp-
8.0/ranges.md#implicit-index-support , assuming that the length of the collection is
known at compile time and is equal to the amount of elements in the inline array type of
the primary_no_arr ay_cr eation_expr ession . Then the element access is interpreted as
described in When the expr ession type is int  section.
If primary_no_arr ay_cr eation_expr ession  is a writable variable, the result of evaluating an
inline array element access is a value equivalent to invoking public Span<T> Slice (int
start, int length)  on an instance of System.Span<T> returned by System.Span<T>
InlineArrayAsSpan method on primary_no_arr ay_cr eation_expr ession . For the purpose of
ref-safety analysis the ref-safe-c ontext/safe-c ontext of the access are equivalent to the
same for an invocation of a method with the signature static System.Span<T>
GetSlice(ref InlineArrayType array).    ref readonly  int a = ref x[0]; // Ok, equivalent to `ref readonly int a  
= ref InlineArrayAsReadOnlySpan<Buffer10<int>, int>(in x, 10)[0]`
    ref int b = ref x[0]; // An error, `x` is a readonly variable => `x[0]`  
is a readonly variable
}
Buffer10< int> GetBuffer () => default;
void M3()
{
    int a = GetBuffer()[ 0]; // Ok, equivalent to `int a =  
InlineArrayAsReadOnlySpan<Buffer10<int>, int>(GetBuffer(), 10)[0]` 
    ref readonly  int b = ref GetBuffer ()[0]; // An error, `GetBuffer()[0]`  
is a value
    ref int c = ref GetBuffer ()[0]; // An error, `GetBuffer()[0]` is a value
}
When the expression is implicitly convertible to int
When the expression implicitly convertible to System.Index
When the expression implicitly convertible to System.RangeIf primary_no_arr ay_cr eation_expr ession  is a readonly variable, the result of evaluating an
inline array element access is a value equivalent to invoking public R eadOnlySpan<T>
Slice (int start, int length)  on an instance of System.ReadOnlySpan<T> returned by
System.ReadOnlySpan<T> InlineArrayAsReadOnlySpan method on
primary_no_arr ay_cr eation_expr ession . For the purpose of ref-safety analysis the ref-safe-
context/safe-c ontext of the access are equivalent to the same for an invocation of a
method with the signature static System.ReadOnlySpan<T> GetSlice(in InlineArrayType
array).
If primary_no_arr ay_cr eation_expr ession  is a value, an error is reported.
The arguments for the Slice method invocation are calculated from the index
expression converted to System.Range as described at
https://github.com/dotnet/csharplang/blob/main/proposals/csharp-
8.0/ranges.md#implicit-range-support , assuming that the length of the collection is
known at compile time and is equal to the amount of elements in the inline array type of
the primary_no_arr ay_cr eation_expr ession .
Compiler can omit the Slice call if it is known at compile time that start is 0 and
length is less or equal to the amount of elements in the inline array type. Compiler can
also report an error if it is known at compile time that slicing goes out of inline array
bounds.
For example:
C#
void M1(Buffer10< int> x)
{
    System.Span< int> a = x[..]; // Ok, equivalent to `System.Span<int> a =  
InlineArrayAsSpan<Buffer10<int>, int>(ref x, 10).Slice(0, 10)`
}
void M2(in Buffer10< int> x)
{
    System.ReadOnlySpan< int> a = x[..]; // Ok, equivalent to  
`System.ReadOnlySpan<int> a = InlineArrayAsReadOnlySpan<Buffer10<int>, int>
(in x, 10).Slice(0, 10)`
    System.Span< int> b = x[..]; // An error, System.ReadOnlySpan<int> cannot  
be converted to System.Span<int>
}
Buffer10< int> GetBuffer () => default;
void M3()
{A new conversion, an inline array conversion, from expression will be added. The inline
array conversion is a standard conversion .
There is an implicit conversion from expression of an inline array type to the following
types:
System.Span<T>
System.ReadOnlySpan<T>
However, converting a readonly variable to System.Span<T> or converting a value to
either type is an error.
For example:
C#
For the purpose of ref-safety analysis the safe-c ontext of the conversion is equivalent to
safe-c ontext for an invocation of a method with the signature static System.Span<T>    _ = GetBuffer()[..]; // An error, `GetBuffer()` is a value
}
Conversions
void M1(Buffer10< int> x)
{
    System.ReadOnlySpan< int> a = x; // Ok, equivalent to  
`System.ReadOnlySpan<int> a = InlineArrayAsReadOnlySpan<Buffer10<int>, int>
(in x, 10)`
    System.Span< int> b = x; // Ok, equivalent to `System.Span<int> b =  
InlineArrayAsSpan<Buffer10<int>, int>(ref x, 10)`
}
void M2(in Buffer10< int> x)
{
    System.ReadOnlySpan< int> a = x; // Ok, equivalent to  
`System.ReadOnlySpan<int> a = InlineArrayAsReadOnlySpan<Buffer10<int>, int>
(in x, 10)`
    System.Span< int> b = x; // An error, readonly mismatch
}
Buffer10< int> GetBuffer () => default;
void M3()
{
    System.ReadOnlySpan< int> a = GetBuffer(); // An error, ref-safety
    System.Span< int> b = GetBuffer(); // An error, ref-safety
}Convert(ref InlineArrayType array), or static System.ReadOnlySpan<T> Convert(in
InlineArrayType array).
List patterns  will not be supported for instances of inline array types.
Regular definite assignment rules are applicable to variables that have an inline array
type.
An inline array type is a valid constr uctible c ollection  target type for a collection literal .
For example:
C#
The length of the collection literal must match the length of the target inline array type.
If the length of the literal is known at compile time and it doesn't match the target
length, an error is reported. Otherwise, an exception is going to be thrown at runtime
once the mismatch is encountered. The exact exception type is TBD. Some candidates
are: S ystem.NotSupportedException, S ystem.InvalidOperationException.
An instance of an inline array type is a valid expression in a spread_element .
Compiler will validate the following aspects of the InlineArrayAttribute applications:
The target type is a struct
The target type has only one field
Specified length > 0List patterns
Definite assignment checking
Collection literals
int[5] a = [1, 2, 3, 4, 5]; // initializes anonymous inline array of length  
5
Buffer10< int> b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; // initializes user-
defined inline array
var d = new int[][2] {[11, 12], [21, 22], [31, 32]}; // regular array with  
an element type of an anonymous inline array type with element type int and  
length 2
Validation of the InlineArrayAttribute applicationsThe target struct doesn't have an explicit layout specified
By default, element initialization will not be supported via initializer_t arget of form '['
argument_list ']' (see https://github.com/dotnet/csharpstandard/blob/draft-
v8/standard/expressions.md#128163-object-initializers ):
C#
However, if the inline array type explicitly defines suitable indexer, object initializer will
use it:
C#
The foreach statement  will be adjusted to allow usage of an inline array type as a
collection in a foreach statement.Inline Array elements in an object initializer
static C M2() => new C() { F = {[ 0] = 111} }; // error CS1913: Member '[0]'  
cannot be initialized. It is not a field or property.
class C
{
    public Buffer10< int> F;
}
static C M2() => new C() { F = {[ 0] = 111} }; // Ok, indexer is invoked
class C
{
    public Buffer10< int> F;
}
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct Buffer10<T>
{
    private T _element0;
    public T this[int i]
    {
        get => this[i];
        set => this[i] = value;
    }
}
The foreach statement
For example:
C#
is equivalent to:
C#
We will support foreach over inline arrays, even if it starts as restricted in async
methods due to involvement of the span types into the translation.foreach (var a in getBufferAsValue ())
{
    WriteLine(a);
}
foreach (var b in getBufferAsWritableVariable ())
{
    WriteLine(b);
}
foreach (var c in getBufferAsReadonlyVariable ())
{
    WriteLine(c);
}
Buffer10< int> getBufferAsValue () => default;
ref Buffer10< int> getBufferAsWritableVariable () => default;
ref readonly  Buffer10< int> getBufferAsReadonlyVariable () => default;
Buffer10< int> temp = getBufferAsValue();
foreach (var a in (System.ReadOnlySpan< int>)temp)
{
    WriteLine(a);
}
foreach (var b in (System.Span< int>)getBufferAsWritableVariable ())
{
    WriteLine(b);
}
foreach (var c in (System.ReadOnlySpan< int>)getBufferAsReadonlyVariable ())
{
    WriteLine(c);
}
Open design questionsThe grammar at https://github.com/dotnet/csharpstandard/blob/draft-
v8/standard/types.md#821-general  will be adjusted as follows:
diff
The type of the constant_expr ession  must be implicitly convertible to type int, and the
value must be a non-zero positive integer.
The relevant part of the https://github.com/dotnet/csharpstandard/blob/draft-
v8/standard/arrays.md#1621-general  section will be adjusted as follows.
The grammar productions for array types are provided in
https://github.com/dotnet/csharpstandard/blob/draft-v8/standard/types.md#821-
general .
An array type is written as a non_arr ay_type  followed by one or more rank_speci fiers.
A non_arr ay_type  is any type that is not itself an array_type .
The rank of an array type is given by the leftmost rank_speci fier in the array_type : A
rank_speci fier indicates that the array is an array with a rank of one plus the number of
“,” tokens in the rank_speci fier.
The element type of an array type is the type that results from deleting the leftmost
rank_speci fier:
An array type of the form T[ constant_expression ] is an anonymous inline array
type with length denoted by constant_expr ession  and a non-array element type T.
An array type of the form T[ constant_expression ][R₁]...[Rₓ] is an anonymous
inline array type with length denoted by constant_expr ession  and an element type
T[R₁]...[Rₓ].Alternatives
Inline array type syntax
array_type
    : non_array_type rank_specifier+
    ;
rank_specifier
    : '[' ','* ']'
+   | '[' constant_expression ']' 
    ;
An array type of the form T[R] (where R is not a constant_expr ession ) is a regular
array type with rank R and a non-array element type T.
An array type of the form T[R][R₁]...[Rₓ] (where R is not a constant_expr ession ) is
a regular array type with rank R and an element type T[R₁]...[Rₓ].
In effect, the rank_speci fiers are read from left to right befor e the final non-array element
type.
Example : The type in int[][,,][,] is a single-dimensional array of three-
dimensional arrays of two-dimensional arrays of int. end ex ample
At run-time, a value of a regular array type can be null or a reference to an instance of
that array type.
Note: Following the rules of https://github.com/dotnet/csharpstandard/blob/draft-
v8/standard/arrays.md#166-array-covariance , the value may also be a reference
to a covariant array type. end not e
An anonymous inline array type is a compiler synthesized inline array type with internal
accessibility. The element type must be a type that can be used as a type argument.
Unlike an explicitly declared inline array type, an anonymous inline array type cannot be
referenced by name, it can be referenced only by array_type  syntax. In context of the
same program, any two array_type s denoting inline array types of the same element
type and of the same length, refer to the same anonymous inline array type.
Besides internal accessibility, compiler will prevent consumption of APIs utilizing
anonymous inline array types across assembly boundaries by using a required custom
modifier (exact type TBD) applied to an anonymous inline array type reference in the
signature.
Array creation expressions
ANTLR
Array creation expressions
array_creation_expression
    : 'new' non_array_type '[' expression_list ']' rank_specifier*
      array_initializer?
    | 'new' array_type array_initializer
    | 'new' rank_specifier array_initializer
    ;Given the current grammar, use of a constant_expr ession  in place of the expression_list
already has meaning of allocating a regular single-dimensional array type of the
specified length. Therefore, array_cr eation_expr ession  will continue to represent an
allocation of a regular array.
However, the new form of the rank_speci fier could be used to incorporate an
anonymous inline array type into the element type of the allocated array.
For example, the following expressions create a regular array of length 2 with an
element type of an anonymous inline array type with element type int and length 5:
C#
The Array initializers  section will be adjusted to allow use of array_initializer  to
initialize inline array types (no changes to the grammar necessary).
ANTLR
The length of the inline array must be explicitly provided by the target type.
For example:
C#new int[2][5];
new int[][5] {default, default};
new [] {default(int[5]), default(int[5])};
Array initializers
array_initializer
    : '{' variable_initializer_list? '}'
    | '{' variable_initializer_list ',' '}'
    ;
variable_initializer_list
    : variable_initializer ( ',' variable_initializer)*
    ;
    
variable_initializer
    : expression
    | array_initializer
    ;
int[5] a = {1, 2, 3, 4, 5}; // initializes anonymous inline array of length  
5
Buffer10< int> b = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; // initializes user-Note, that for the purpose of this proposal a term "fixed-size buffer" refers to a the
proposed "safe fixed-size buffer" feature rather than to a buffer described at
https://github.com/dotnet/csharpstandard/blob/draft-v8/standard/unsafe-
code.md#228-fixed-size-buffers .
In this design, fixed-size buffer types do not get general special treatment by the
language. There is a special syntax to declare members that represent fixed-size buffers
and new rules around consuming those members. They are not fields from the language
point of view.
The grammar for variable_declar ator in
https://github.com/dotnet/csharpstandard/blob/draft-v8/standard/classes.md#145-
fields  will be extended to allow specifying the size of the buffer:
diffdefined inline array
var c = new int[][] {{11, 12}, {21, 22}, {31, 32}}; // An error for the  
nested array initializer
var d = new int[][2] {{11, 12}, {21, 22}, {31, 32}}; // An error for the  
nested array initializer
Detailed Design (Option 2)
field_declaration
    : attributes? field_modifier* type variable_declarators ';'
    ;
field_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'readonly'
    | 'volatile'
    | unsafe_modifier   // unsafe code support
    ;
variable_declarators
    : variable_declarator (',' variable_declarator)*
    ;
    
variable_declarator
    : identifier ('=' variable_initializer)?
+   | fixed_size_buffer_declarator
    ;
    A fixed_size_buf fer_declar ator introduces a fixed-size buffer of a given element type.
The buffer element type is the type specified in field_declaration. A fixed-size buffer
declarator introduces a new member and consists of an identifier that names the
member, followed by a constant expression enclosed in [ and ] tokens. The constant
expression denotes the number of elements in the member introduced by that fixed-
size buffer declarator. The type of the constant expression must be implicitly convertible
to type int, and the value must be a non-zero positive integer.
The elements of a fixed-size buffer shall be laid out sequentially in memory as though
they are elements of an array.
A field_declar ation  with a fixed_size_buf fer_declar ator in an interface must have static
modifier.
Depending on the situation (details are specified below), an access to a fixed-size buffer
member is classified as a value (never a variable) of either System.ReadOnlySpan<S> or
System.Span<S>, where S is the element type of the fixed-size buffer. Both types provide
indexers returning a reference to a specific element with appropriate "readonly-ness",
which prevents direct assignment to the elements when language rules don't permit
that.
This limits the set of types that can be used as a fixed-size buffer element type to types
that can be used as type arguments. For example, a pointer type cannot be used as an
element type.
The resulting span instance will have a length equal to the size declared on the fixed-
size buffer. Indexing into the span with a constant expression outside of the declared
fixed-size buffer bounds is a compile time error.
The safe-c ontext of the value will be equal to the safe-c ontext of the container, just as it
would if the backing data was accessed as a field.
Member lookup of a fixed-size buffer member proceeds exactly like member lookup of
a field.fixed_size_buffer_declarator
    : identifier '[' constant_expression ']'
    ;    
Fixed-size buffers in expressionsA fixed-size buffer can be referenced in an expression using a simple_name  or a
member_ac cess .
When an instance fixed-size buffer member is referenced as a simple name, the effect is
the same as a member access of the form this.I, where I is the fixed-size buffer
member. When a static fixed-size buffer member is referenced as a simple name, the
effect is the same as a member access of the form E.I, where I is the fixed-size buffer
member and E is the declaring type.
In a member access of the form E.I, if E is of a struct type and a member lookup of I
in that struct type identifies a non-readonly instance fixed-size member, then E.I is
evaluated and classified as follows:
If E is classified as a value, then E.I can be used only as a
primary_no_arr ay_cr eation_expr ession  of an element access  with index of
System.Index type, or of a type implicitly convertible to int. R esult of the element
access is a fixed-size member's element at the specified position, classified as a
value.
Otherwise, if E is classified as a readonly variable and the result of the expression
is classified as a value of type System.ReadOnlySpan<S>, where S is the element type
of I. The value can be used to access member's elements.
Otherwise, E is classified as a writable variable and the result of the expression is
classified as a value of type System.Span<S>, where S is the element type of I. The
value can be used to access member's elements.
In a member access of the form E.I, if E is of a class type and a member lookup of I in
that class type identifies a non-readonly instance fixed-size member, then E.I is
evaluated and classified as a value of type System.Span<S>, where S is the element type
of I.
In a member access of the form E.I, if member lookup of I identifies a non-readonly
static fixed-size member, then E.I is evaluated and classified as a value of type
System.Span<S>, where S is the element type of I.
When a field_declar ation  includes a readonly modifier, the member introduced by the
fixed_size_buffer_declarator is a readonly f ixed-size buf fer. Direct assignments toNon-readonly fixed-size buffers
Readonly fixed-size bufferselements of a readonly fixed-size buffer can only occur in an instance constructor, init
member or static constructor in the same type. Specifically, direct assignments to an
element of readonly fixed-size buffer are permitted only in the following contexts:
For an instance member, in the instance constructors or init member of the type
that contains the member declaration; for a static member, in the static constructor
of the type that contains the member declaration. These are also the only contexts
in which it is valid to pass an element of readonly fixed-size buffer as an out or
ref parameter.
Attempting to assign to an element of a readonly fixed-size buffer or pass it as an out
or ref parameter in any other context is a compile-time error. This is achieved by the
following.
A member access for a readonly fixed-size buffer is evaluated and classified as follows:
In a member access of the form E.I, if E is of a struct type and E is classified as a
value, then E.I can be used only as a primary_no_arr ay_cr eation_expr ession  of an
element access  with index of System.Index type, or of a type implicitly
convertible to int. R esult of the element access is a fixed-size member's element at
the specified position, classified as a value.
If access occurs in a context where direct assignments to an element of readonly
fixed-size buffer are permitted, the result of the expression is classified as a value
of type System.Span<S>, where S is the element type of the fixed-size buffer. The
value can be used to access member's elements.
Otherwise, the expression is classified as a value of type System.ReadOnlySpan<S>,
where S is the element type of the fixed-size buffer. The value can be used to
access member's elements.
Fixed-size buffers are not subject to definite assignment-checking, and fixed-size buffer
members are ignored for purposes of definite-assignment checking of struct type
variables.
When a fixed-size buffer member is static or the outermost containing struct variable of
a fixed-size buffer member is a static variable, an instance variable of a class instance, or
an array element, the elements of the fixed-size buffer are automatically initialized to
their default values. In all other cases, the initial content of a fixed-size buffer is
undefined.
Definite assignment checkingFor metadata encoding compiler will rely on recently added
System.Runtime.CompilerServices.InlineArrayAttribute .
Fixed-size buffers like:
C#
will be emitted as fields of a specially decorated struct type.
Equivalent C# code will be:
C#Metadata
Metadata emit and code generation
public partial class C
{
    public int buffer1[ 10];
    public readonly  int buffer2[ 10];
}
public partial class C
{
    public Buffer10< int> buffer1;
    public readonly  Buffer10< int> buffer2;
}
[System.Runtime.CompilerServices.InlineArray( 10)]
public struct Buffer10<T>
{
    private T _element0;
    [UnscopedRef ]
    public System. Span<T> AsSpan()
    {
        return System.Runtime.InteropServices.MemoryMarshal.CreateSpan( ref 
_element0, 10);
    }
    [UnscopedRef ]
    public readonly  System. ReadOnlySpan<T> AsReadOnlySpan ()
    {
        return 
System.Runtime.InteropServices.MemoryMarshal.CreateReadOnlySpan(
                    ref System.Runtime.CompilerServices.Unsafe.AsRef( in 
_element0), 10);The actual naming conventions for the type and its members are TBD. The framework
will likely include a set of predefined "buffer" types that cover a limited set of buffer
sizes. When a predefined type doesn't exist, compiler will synthesize it in the module
being built. Names of the generated types will be "speakable" in order to support
consumption from other languages.
A code generated for an access like:
C#
will be equivalent to:
C#
When compiler imports a field declaration of type T and the following conditions are all
met:    }
}
public partial class C
{
    void M1(int val)
    {
        buffer1[ 1] = val;
    }
    int M2()
    {
        return buffer2[ 1];
    }
}
public partial class C
{
    void M1(int val)
    {
        buffer.AsSpan()[ 1] = val;
    }
    int M2()
    {
        return buffer2.AsReadOnlySpan()[ 1];
    }
}
Metadata importT is a struct type decorated with the InlineArray attribute, and
The first instance field declared within T has type F, and
There is a public System.Span<F> AsSpan() within T, and
There is a public readonly System.ReadOnlySpan<T> AsReadOnlySpan() or public
System.ReadOnlySpan<T> AsReadOnlySpan() within T.
the field will be treated as C# fixed-size buffer with element type F. Otherwise, the field
will be treated as a regular field of type T.
One thought is to treat these members more like method groups, in that they aren't
automatically a value in and of themselves, but can be made into one if necessary.
Here’s how that would work:
Safe fixed-size buffer accesses have their own classification (just like e.g. method
groups and lambdas)
They can be indexed directly as a language operation (not via span types) to
produce a variable (which is readonly if the buffer is in a readonly context, just the
same as fields of a struct)
They have implicit conversions-from-expression to Span<T> and ReadOnlySpan<T>,
but use of the former is an error if they are in a readonly context
Their natural type is ReadOnlySpan<T>, so that’s what they contribute if they
participate in type inference (e.g., var, best-common-type or generic)
C/C++ has a different notion of fixed-size buffers. For example, there is a notion of
"zero-length fixed sized buffers", which is often used as a way to indicate that the data is
"variable length". It is not a goal of this proposal to be able to interop with that.
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-04-
03.md#fixed-size-buffers
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-04-
10.md#fixed-size-buffers
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
01.md#fixed-size-buffersMethod or property group like approach in the language
C/C++ fixed-size buffers
LDM meetings
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
03.md#inline-arrays
https://github.com/dotnet/csharplang/blob/main/meetings/2023/LDM-2023-05-
17.md#inline-arrays
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackref readonly parameters
Article •08/16/2023
Allow parameter declaration-site modifier ref readonly and change callsite rules as
follows:
Callsit e
annotationref
paramet erref readonly
paramet erin
paramet erout
paramet er
ref Allowed Allow ed Warning Error
in Error Allow ed Allowed Error
out Error Error Error Allowed
No annotation Error Warning Allowed Error
(Note that there is one change to the existing rules: in parameter with ref callsite
annotation produces a warning instead of an error.)
Change argument value rules as follows:
Value kind ref paramet erref readonly paramet erin paramet erout paramet er
rvalue Error Warning Allowed Error
lvalue Allowed Allow ed Allowed Allowed
Where lvalue means a variable (i.e., a value with a location; does not have to be
writable/assignable) and rvalue means any kind of value.７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
SummaryC# 7.2 introduced in parameters  as a way to pass readonly references. in parameters
allow both lvalues and rvalues and can be used without any annotation at the callsite.
However, APIs which capture or return references from their parameters would like to
disallow rvalues and also enforce some indication at the callsite that a reference is being
captured. ref readonly parameters are ideal in such cases as they warn if used with
rvalues or without any annotation at the callsite.
Furthermore, there are APIs that need only read-only references but use
ref parameters since they were introduced before in became available and
changing to in would be a source and binary breaking change, e.g.,
QueryInterface, or
in parameters to accept readonly references even though passing rvalues to them
doesn't really make sense, e.g., ReadOnlySpan<T>..ctor(in T value), or
ref parameters to disallow rvalues even though they don't mutate the passed
reference, e.g., Unsafe.IsNullRef.
These APIs could migrate to ref readonly parameters without breaking users. For
details on binary compatibility, see the proposed metadata encoding . Specifically,
changing
ref → ref readonly would only be a binary breaking change for virtual methods,
ref → in would also be a binary breaking change for virtual methods, but not a
source breaking change (because the rules change to only warn for ref arguments
passed to in parameters),
in → ref readonly would not be a breaking change (but no callsite annotation or
rvalue would result in a warning),
note that this would be a source breaking change for users using older compiler
versions (as they interpret ref readonly parameters as ref parameters,
disallowing in or no annotation at the callsite) and new compiler versions with
LangVersion <= 11 (for consistency with older compiler versions, an error will be
emitted that ref readonly parameters are not supported unless the
corresponding arguments are passed with the ref modifier).
In the opposite direction, changing
ref readonly → ref would be potentially a source breaking change (unless only
ref callsite annotation was used and only readonly references used as arguments),
and a binary breaking change for virtual methods,Motivation
ref readonly → in would not be a breaking change (but ref callsite annotation
would result in a warning).
In general, rules for ref readonly parameters are the same as specified for in
parameters in their proposal , except where explicitly changed in this proposal.
No changes in grammar are necessary. The modifier ref readonly will be allowed for
parameters. Apart from normal methods, ref readonly will be allowed for indexer
parameters (like in but unlike ref), but disallowed for operator parameters (like ref
but unlike in).
Default parameter values will be allowed for ref readonly parameters with a warning
since they are equivalent to passing rvalues. This allows API authors to change in
parameters with default values to ref readonly parameters without introducing a
source breaking change.
Note that even though ref argument modifier is allowed for ref readonly parameters,
nothing changes w.r.t. value kind checks, i.e.,
ref can only be used with assignable values;
to pass readonly references, one has to use the in argument modifier instead;
to pass rvalues, one has to use no modifier (which results in a warning for ref
readonly parameters as described in the summary of this proposal ).
Overload resolution will allow mixing ref/ref readonly/in/no callsite annotations and
parameter modifiers as denoted by the table in the summary of this proposal , i.e., all
allowed and warning cases will be considered as possible candidates during overload
resolution. Specifically, there's a change in existing behavior where methods with in
parameter will match calls with the corresponding argument marked as ref—this
change will be gated on LangV ersion.Detailed design
Parameter declarations
Value kind checks
Overload resolutionHowever, the warning for passing an argument with no callsite modifier to a ref
readonly parameter will be suppressed if the parameter is
the receiver in an extension method invocation,
used implicitly as part of custom collection initializer or interpolated string handler.
By-value overloads will be preferred over ref readonly overloads in case there is no
argument modifier ( in parameters have the same behavior).
Similarly, for the purpose of anonymous function [ §10.7 ] and method group [ §10.8 ]
conversions, these modifiers are considered compatible (but the conversion results in a
warning):
ref readonly can be interchanged with in or ref modifier,
in can be interchanged with ref modifier (this change will be gated on
LangV ersion).
Note that there is no change in behavior of function pointer conversions . As a
reminder, implicit function pointer conversions are disallowed if there is a mismatch
between reference kind modifiers, and explicit casts are always allowed without any
warnings.
Members declared in a single type cannot differ in signature solely by ref/out/in/ref
readonly. For other purposes of signature matching (e.g., hiding or overriding), ref
readonly can be interchanged with in modifier, but that results in a warning at the
declaration site [ §7.6 ]. This doesn't apply when matching partial declaration with its
implementation and when matching interceptor signature with intercepted signature.
Note that there is no change in overriding for ref/in and ref readonly/ref modifier
pairs, they cannot be interchanged, because the signatures aren't binary compatible. For
consistency, the same is true for other signature matching purposes (e.g., hiding).
As a reminder,
ref parameters are emitted as plain byref types ( T& in IL),Method conversions
Signature matching
Metadata encodingin parameters are like ref plus they are annotated with
System.Runtime.CompilerServices.IsReadOnlyAttribute. In C# 7.3 and later, they
are also emitted with [in] and if virtual,
modreq(System.Runtime.InteropServices.InAttribute).
ref readonly parameters will be emitted as [in] T&, plus annotated with the following
attribute:
C#
Furthermore, if virtual, they will be emitted with
modreq(System.Runtime.InteropServices.InAttribute) to ensure binary compatibility
with in parameters. Note that unlike in parameters, no [IsReadOnly] will be emitted
for ref readonly parameters to avoid increasing metadata size and also to make older
compiler versions interpret ref readonly parameters as ref parameters (and hence ref
→ ref readonly won't be a source breaking change even between different compiler
versions).
The RequiresLocationAttribute will be matched by namespace-qualified name and
synthesized by the compiler if not already included in the compilation.
Specifying the attribute in source will be an error if it's applied to a parameter, similarly
to ParamArrayAttribute.
In function pointers, in parameters are emitted with
modreq(System.Runtime.InteropServices.InAttribute) (see function pointers
proposal ). ref readonly parameters will be emitted without that modreq, but instead
with modopt(System.Runtime.CompilerServices.RequiresLocationAttribute). Older
compiler versions will ignore the modopt and hence interpret ref readonly parameters
as ref parameters (consistent with older compiler behavior for normal methods with
ref readonly parameters as described above) and new compiler versions aware of thenamespace  System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Parameter, AllowMultiple = false,  
Inherited = false) ]
    public sealed class RequiresLocationAttribute  : Attribute
    {
    }
}
Function pointers
modopt will use it to recognize ref readonly parameters to emit warnings during
conversions  and invocations . For consistency with older compiler versions, new compiler
versions with LangVersion <= 11 will report errors that ref readonly parameters are not
supported unless the corresponding arguments are passed with the ref modifier.
Note that it is a binary break to change modifiers in function pointer signatures if they
are part of public APIs, hence it will be a binary break when changing ref or in to ref
readonly. However, a source break will only occur for callers with LangVersion <= 11
when changing in → ref readonly (if invoking the pointer with in callsite modifier),
consistent with normal methods.
The ref/in mismatch relaxation in overload resolution introduces a behavior breaking
change demonstrated in the following example:
C#
In C# 11, the call binds to E.M, hence "E" is printed. In C# 12, C.M is allowed to bind
(with a warning) and no extension scopes are searched since we have an applicable
candidate, hence "C" is printed.
There is also a source breaking change due to the same reason. The example below
prints "1" in C# 11, but fails to compile with an ambiguity error in C# 12:
C#Breaking changes
class C
{
    string M(in int i) => "C";
    static void Main()
    {
        int i = 5;
        System.Console.Write( new C().M(ref i));
    }
}
static class E
{
    public static string M(this C c, ref int i) => "E";
}
var i = 5;
System.Console.Write(C.M( null, ref i));
interface  I1 { }The examples above demonstrate the breaks for method invocations, but since they are
caused by overload resolution changes, they can be similarly triggered for method
conversions.
API authors could annotate in parameters designed to accept only lvalues with a
custom attribute and provide an analyzer to flag incorrect usages. This would not allow
API authors to change signatures of existing APIs that opted to use ref parameters to
disallow rvalues. Callers of such APIs would still need to perform extra work to get a ref
if they have access only to a ref readonly variable. Changing these APIs from ref to
[RequiresLocation] in would be a source breaking change (and in case of virtual
methods, also a binary breaking change).
Instead of allowing the modifier ref readonly, the compiler could recognize when a
special attribute (like [RequiresLocation]) is applied to a parameter. This was discussed
in LDM 2022-04-25 , deciding this is a language feature, not an analyzer, so it should
look like one.
Passing lvalues without any modifiers to ref readonly parameters could be permitted
without any warnings, similarly to C++'s implicit byref parameters. This was discussed in
LDM 2022-05-11 , noting that the primary motivation for ref readonly parameters are
APIs which capture or return references from these parameters, so marker of some kind
is a good thing.
Passing rvalue to a ref readonly could be an error, not a warning. That was initially
accepted in LDM 2022-04-25 , but later e-mail discussions relaxed this because we
would lose the ability to change existing APIs without breaking users.interface  I2 { }
static class C
{
    public static string M(I1 o, ref int x) => "1";
    public static string M(I2 o, in int x) => "2";
}
Alternatives
Parameter declarations
Value kind checks
in could be the "natural" callsite modifier for ref readonly parameters and using ref
could result in warnings. This would ensure a consistent code style and make it obvious
at the callsite that the reference is readonly (unlike ref). It was initially accepted in LDM
2022-04-25 . However, warnings could be a friction point for API authors to move from
ref to ref readonly. Also, in has been redefined as ref readonly + convenience
features, hence this was rejected in LDM 2022-05-11 .
Inverse ordering of modifiers ( readonly ref instead of ref readonly) could be allowed.
This would be inconsistent with how readonly ref returns and fields behave (inverse
ordering is disallowed or means something different, respectively) and could clash with
readonly parameters if implemented in the future.
Default parameter values could be an error for ref readonly parameters.
Errors could be emitted instead of warnings when passing rvalues to ref readonly
parameters or mismatching callsite annotations and parameter modifiers. Similarly,
special modreq could be used instead of an attribute to ensure ref readonly parameters
are distinct from in parameters on the binary level. This would provide stronger
guarantees, so it would be good for new APIs, but prevent adoption in existing runtime
APIs which cannot introduce breaking changes.
Value kind checks could be relaxed to allow passing readonly references via ref into
in/ref readonly parameters. That would be similar to how ref assignments and ref
returns work today—they also allow passing references as readonly via the ref modifier
on the source expression. However, the ref there is usually close to the place where the
target is declared as ref readonly, so it is clear we are passing a reference as readonly,
unlike invocations whose argument and parameter modifiers are usually far apart.
Furthermore, they allow only the ref modifier unlike arguments which allow also in,
hence in and ref would become interchangeable for arguments, or in would become
practically obsolete if users wanted to make their code consistent (they would probably
use ref everywhere since it's the only modifier allowed for ref assignments and ref
returns).
Pending LDM review
Parameter declarations
Value kind checksOverload resolution, overriding, and conversion could disallow interchangeability of ref
readonly and in modifiers.
The overload resolution change for existing in parameters could be taken
unconditionally (not considering LangV ersion), but that would be a breaking change.
Invoking an extension method with ref readonly receiver could result in warning
"Argument 1 should be passed with ref or in keyword" as would happen for non-
extension invocations with no callsite modifiers (user could fix such warning by turning
the extension method invocation into static method invocation). The same warning
could be reported when using custom collection initializer or interpolated string handler
with ref readonly parameter, although user could not work around it.
ref readonly overloads could be preferred over by-value overloads when there is no
callsite modifier or there could be an ambiguity error.
Function pointer conversions could warn on ref readonly/ref/in mismatch, but if we
wanted to gate that on LangV ersion, a significant implementation investment would be
required as today type conversions do not need access to compilation. Furthermore,
even though mismatch is currently an error, it is easy for users to add a cast to allow the
mismatch if they want.
Specifying the RequiresLocationAttribute in source could be allowed, similarly to In
and Out attributes. Alternatively, it could be an error when applied in other contexts
than just parameters, similarly to IsReadOnly attribute; to preserve further design space.
Function pointer ref readonly parameters could be emitted with different
modopt/modreq combinations (note that "source break" in this table means for callers
with LangVersion <= 11):
Modifier s Can be r ecognized
across
compilationsOld compiler s
see them asref → ref
readonlyin → ref
readonly
modreq(In)
modopt(RequiresLocation)yes in binary,
sourcebinary
breakOverload resolution
Method conversions
Metadata encodingModifier s Can be r ecognized
across
compilationsOld compiler s
see them asref → ref
readonlyin → ref
readonly
break
modreq(In) no in binary,
source
breakok
modreq(RequiresLocation) yes unsupported binary,
source
breakbinary,
source
break
modopt(RequiresLocation) yes ref binary
breakbinary,
source
break
We could emit both [RequiresLocation] and [IsReadOnly] attributes for ref readonly
parameters. Then in → ref readonly would not be a breaking change even for older
compiler versions, but ref → ref readonly would become a source breaking change for
older compiler versions (as they would interpret ref readonly as in, disallowing ref
modifiers) and new compiler versions with LangVersion <= 11 (for consistency).
We could make the behavior for LangVersion <= 11 different from the behavior for
older compiler versions. For example, it could be an error whenever a ref readonly
parameter is called (even when using the ref modifier at the callsite), or it could be
always allowed without any errors.
This proposal suggests accepting a behavior breaking change because it should be rare
to hit, is gated by LangV ersion, and users can work around it by calling the extension
method explicitly. Instead, we could mitigate it by
disallowing the ref/in mismatch (that would only prevent migration to in for old
APIs that used ref because in wasn't available yet),
modifying the overload resolution rules to continue looking for a better match
(determined by betterness rules specified below) when there's a ref kind mismatch
introduced in this proposal,
or alternatively continue only for ref vs. in mismatch, not the others ( ref
readonly vs. ref/in/by-value).Breaking changes
Betterness rulesThe following example currently results in three ambiguity errors for the three
invocations of M. We could add new betterness rules to resolve the ambiguities. This
would also resolve the source breaking change described earlier. One way would be to
make the example print 221 (where ref readonly parameter is matched with in
argument since it would be a warning to call it with no modifier whereas for in
parameter that's allowed).
C#
New betterness rules could mark as worse the parameter whose argument could have
been passed with a different argument modifier to make it better. In other words, user
should be always able to turn a worse parameter into a better parameter by changing its
corresponding argument modifier. For example, when an argument is passed by in, a
ref readonly parameter is preferred over an in parameter because user could pass the
argument by-value to choose the in parameter. This rule is just an extension of by-
value/in preference rule that is in effect today (it's the last overload resolution rule and
the whole overload is better if any of its parameter is better and none is worse than the
corresponding parameter of another overload).
argument better paramet er worse paramet er
ref/in ref readonly in
ref ref ref readonly/in
by-value by-value/ in ref readonly
in in ref
We should handle method conversions similarly. The following example currently results
in two ambiguity errors for the two delegate assignments. New betterness rules couldinterface  I1 { }
interface  I2 { }
class C
{
    static string M(I1 o, in int i) => "1";
    static string M(I2 o, ref readonly  int i) => "2";
    static void Main()
    {
        int i = 5;
        System.Console.Write(M( null, ref i));
        System.Console.Write(M( null, in i));
        System.Console.Write(M( null, i));
    }
}prefer a method parameter whose refness modifier matches the corresponding target
delegate parameter refness modifier over one that has a mismatch. Hence, the following
example would print 12.
C#
LDM 2022-04-25 : feature accepted
LDM 2022-05-09 : discussion split into three parts
LDM 2022-05-11 : allowed ref and no callsite annotation for ref readonly
parametersclass C
{
    void M(I1 o, ref readonly  int x) => System.Console.Write( "1");
    void M(I2 o, ref int x) => System.Console.Write( "2");
    void Run()
    {
        D1 m1 = this.M;
        D2 m2 = this.M;
        var i = 5;
        m1(null, in i);
        m2(null, ref i);
    }
    static void Main() => new C().Run();
}
interface  I1 { }
interface  I2 { }
class X : I1, I2 { }
delegate  void D1(X s, ref readonly  int x);
delegate  void D2(X s, ref int x);
Design meetings
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedbackExperimentalAttribute
Article •10/31/2023
Report warnings for references to types and members marked with
System.Diagnostics.CodeAnalysis.ExperimentalAttribute.
C#７ Note
This article is a feature specification. The specification represents the proposed
feature specification. There may be some discrepancies between the feature
specification and the completed implementation. Those differences are captured in
the pertinent language design meeting (LDM) not es. Links to pertinent
meetings are included at the bottom of the spec. Y ou can learn more about the
process for merging feature speclets into the C# language standard in the article
on the specifications .
namespace  System.Diagnostics.CodeAnalysis
{
    [AttributeUsage(AttributeTargets.Assembly |
                    AttributeTargets.Module |
                    AttributeTargets.Class |
                    AttributeTargets.Struct |
                    AttributeTargets.Enum |
                    AttributeTargets.Constructor |
                    AttributeTargets.Method |
                    AttributeTargets.Property |
                    AttributeTargets.Field |
                    AttributeTargets.Event |
                    AttributeTargets.Interface |
                    AttributeTargets.Delegate, Inherited = false) ]
    public sealed class ExperimentalAttribute  : Attribute
    {
        public ExperimentalAttribute (string diagnosticId )
        {
            DiagnosticId = diagnosticId;
        }
        public string DiagnosticId { get; }
        public string? UrlFormat { get; set; }
    }
}Although the diagnostic is technically a warning (so that the compiler allows
suppressing it), it is treated as an error for purpose of reporting. This causes the build to
fail if the diagnostic is not suppressed.
The diagnostic is reported for any reference to a type or member that is either:
marked with the attribute,
in an assembly or module marked with the attribute,
except when the reference occurs within [Experimental] members (automatic
suppression).
It is also possible to suppress the diagnostic by usual means, such as an explicit compiler
option or #pragma.
For example, if the API is marked with [Experimental("DiagID")] or
[Experimental("DiagID", UrlFormat = "https://example.org/{0}")], the diagnostic can
be suppressed with #pragma warning disable DiagID.
An error is produced if the diagnostic ID given to the experimental attribute is not a
valid C# identifier .
The diagnostic message is a specific message, where '{0}' is the fully-qualified type or
member name.
The attribute is not inherited from base types or overridden members.
Warnings for [Experimental] are reported within [Obsolete] or [Deprecated] members.
Warnings and errors for [Obsolete] and [Deprecated] are reported inside
[Experimental] members.
But warnings and errors for [Obsolete] and [Deprecated] are reported instead of
[Experimental] if there are multiple attributes.Reported diagnostic
'{0}' is for evaluation purposes only and is subject to change or removal in  
future updates.
ObsoleteAttribute and DeprecatedAttribute６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide .C# featur e specification
feedb ack
The C# feature specifications are
open source. Provide feedback here.
 Open a documentation issue
 Provide product feedback