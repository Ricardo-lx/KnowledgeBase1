r to asynchronously await for a result to finish. Control
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
If you use Vi