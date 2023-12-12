   [50,51,52,53,54,55,56,57,58,59],
   [60,61,62,63,64,65,66,67,68,69],
   [70,71,72,73,74,75,76,77,78,79],
   [80,81,82,83,84,85,86,87,88,89],
   [90,91,92,93,94,95,96,97,98,99],
];
var selectedRows = jagged[ 3..^3];
foreach (var row in selectedRows)
{
    var selectedColumns = row[ 2..^2];
    foreach (var cell in selectedColumns)
    {
        Console.Write( $"{cell}, ");
    }
    Console.WriteLine();
}
Scenarios for indices and ranges
int[] sequence = Sequence( 1000);
for(int start = 0; start < sequence.Length; start += 100)
{When taking a range from an array, the result is an array that is copied from the initial
array, rather than referenced. Modifying values in the resulting array will not change
values in the initial array.
For example:
C#    Range r = start..(start+ 10);
    var (min, max, average) = MovingAverage(sequence, r);
    Console.WriteLine( $"From {r.Start}  to {r.End}:    \tMin: {min},\tMax: 
{max},\tAverage: {average} ");
}
for (int start = 0; start < sequence.Length; start += 100)
{
    Range r = ^(start + 10)..^start;
    var (min, max, average) = MovingAverage(sequence, r);
    Console.WriteLine( $"From {r.Start}  to {r.End}:  \tMin: {min},\tMax: 
{max},\tAverage: {average} ");
}
(int min, int max, double average) MovingAverage( int[] subSequence, Range  
range) =>
    (
        subSequence[range].Min(),
        subSequence[range].Max(),
        subSequence[range].Average()
    );
int[] Sequence (int count) => [..Enumerable.Range( 0, count).Select(x => ( int)
(Math.Sqrt(x) * 100))];
A Note on Range Indices and Arrays
var arrayOfFiveItems = new[] { 1, 2, 3, 4, 5 };
var firstThreeItems = arrayOfFiveItems[. .3]; // contains 1,2,3
firstThreeItems[ 0] =  11; // now contains 11,2,3
Console.WriteLine( string.Join(",", firstThreeItems));
Console.WriteLine( string.Join(",", arrayOfFiveItems));
// output:
// 11,2,3
// 1,2,3,4,5
See alsoMember access operators and expressions
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
 Provide product feedbackTutorial: Express your design intent
more clearly with nullable and non-
nullable reference types
Article •11/03/2022
Nullable reference types  complement reference types the same way nullable value types
complement value types. Y ou declare a variable to be a nullable r eference type  by
appending a ? to the type. For example, string? represents a nullable string. You can
use these new types to more clearly express your design intent: some variables must
always hav e a value, others may be missing a v alue.
In this tutorial, you'll learn how to:
You'll need to set up your machine to run .NET, including the C# compiler. The C#
compiler is available with Visual S tudio 2022 , or the .NET SDK .
This tutorial assumes you're familiar with C# and .NET, including either Visual S tudio or
the .NET CLI.
In this tutorial, you'll build a library that models running a survey. The code uses both
nullable reference types and non-nullable reference types to represent the real-world
concepts. The survey questions can never be null. A respondent might prefer not to
answer a question. The responses might be null in this case.
The code you'll write for this sample expresses that intent, and the compiler enforces
that intent.Incorporate nullable and non-nullable reference types into your designs＂
Enable nullable reference type checks throughout your code.＂
Write code where the compiler enforces those design decisions.＂
Use the nullable reference feature in your own designs＂
Prerequisites
Incorporate nulla ble reference types into your
designsCreate a new console application either in Visual S tudio or from the command line using
dotnet new console. Name the application NullableIntroduction. Once you've created
the application, you'll need to specify that the entire project compiles in an enabled
nullable annotation cont ext. Open the .csproj file and add a Nullable element to the
PropertyGroup element. Set its value to enable. You must opt into the nullable
reference types  feature in projects earlier than C# 11. That's because once the feature is
turned on, existing reference variable declarations become non-nullable r eference
types . While that decision will help find issues where existing code may not have proper
null-checks, it may not accurately reflect your original design intent:
XML
Prior to .NET 6, new projects do not include the Nullable element. Beginning with .NET
6, new projects include the <Nullable>enable</Nullable> element in the project file.
This survey application requires creating a number of classes:
A class that models the list of questions.
A class that models a list of people contacted for the survey.
A class that models the answers from a person that took the survey.
These types will make use of both nullable and non-nullable reference types to express
which members are required and which members are optional. Nullable reference types
communicate that design intent clearly:
The questions that are part of the survey can never be null: It makes no sense to
ask an empty question.
The respondents can never be null. Y ou'll want to track people you contacted, even
respondents that declined to participate.
Any response to a question may be null. R espondents can decline to answer some
or all questions.
If you've programmed in C#, you may be so accustomed to reference types that allow
null values that you may have missed other opportunities to declare non-nullableCreate the application and enable nulla ble
reference types
<Nullable >enable</Nullable >
Design the types for the applicationinstances:
The collection of questions should be non-nullable.
The collection of respondents should be non-nullable.
As you write the code, you'll see that a non-nullable reference type as the default for
references avoids common mistakes that could lead to NullR eferenceException s. One
lesson from this tutorial is that you made decisions about which variables could or could
not be null. The language didn't provide syntax to express those decisions. Now it
does.
The app you'll build does the following steps:
1. Creates a survey and adds questions to it.
2. Creates a pseudo-random set of respondents for the survey.
3. Contacts respondents until the completed survey size reaches the goal number.
4. Writes out important statistics on the survey responses.
The first code you'll write creates the survey. Y ou'll write classes to model a survey
question and a survey run. Y our survey has three types of questions, distinguished by
the format of the answer: Y es/No answers, number answers, and text answers. Create a
public SurveyQuestion class:
C#
The compiler interprets every reference type variable declaration as a non-nullable
reference type for code in an enabled nullable annotation context. Y ou can see your first
warning by adding properties for the question text and the type of question, as shown
in the following code:
C#Build the survey with nulla ble and non-nulla ble
reference types
namespace  NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
namespace  NullableIntroduction
{Because you haven't initialized QuestionText, the compiler issues a warning that a non-
nullable property hasn't been initialized. Y our design requires the question text to be
non-null, so you add a constructor to initialize it and the QuestionType value as well. The
finished class definition looks like the following code:
C#
Adding the constructor removes the warning. The constructor argument is also a non-
nullable reference type, so the compiler doesn't issue any warnings.
Next, create a public class named SurveyRun. This class contains a list of
SurveyQuestion objects and methods to add questions to the survey, as shown in the
following code:
C#    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }
    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
namespace  NullableIntroduction ;
public enum QuestionType
{
    YesNo,
    Number,
    Text
}
public class SurveyQuestion
{
    public string QuestionText { get; }
    public QuestionType TypeOfQuestion { get; }
    public SurveyQuestion (QuestionType typeOfQuestion, string text) =>
        (TypeOfQuestion, QuestionText) = (typeOfQuestion, text);
}As before, you must initialize the list object to a non-null value or the compiler issues a
warning. There are no null checks in the second overload of AddQuestion because they
aren't needed: Y ou've declared that variable to be non-nullable. Its value can't be null.
Switch to Program.cs  in your editor and replace the contents of Main with the following
lines of code:
C#
Because the entire project is in an enabled nullable annotation context, you'll get
warnings when you pass null to any method expecting a non-nullable reference type.
Try it by adding the following line to Main:
C#using System.Collections.Generic;
namespace  NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new 
List<SurveyQuestion>();
        public void AddQuestion (QuestionType type, string question ) =>
            AddQuestion( new SurveyQuestion(type, question));
        public void AddQuestion (SurveyQuestion surveyQuestion ) => 
surveyQuestions.Add(surveyQuestion);
    }
}
var surveyRun = new SurveyRun();
surveyRun.AddQuestion(QuestionType.YesNo, "Has your code ever thrown a  
NullReferenceException?" );
surveyRun.AddQuestion( new SurveyQuestion(QuestionType.Number, "How many  
times (to the nearest 100) has that happened?" ));
surveyRun.AddQuestion(QuestionType.Text, "What is your favorite color?" );
surveyRun.AddQuestion(QuestionType.Text, default);
Create respondents and get answers to the
surveyNext, write the code that generates answers to the survey. This process involves several
small tasks:
1. Build a method that generates respondent objects. These represent people asked
to fill out the survey.
2. Build logic to simulate asking the questions to a respondent and collecting
answers or noting that a respondent didn't answer.
3. Repeat until enough respondents have answered the survey.
You'll need a class to represent a survey response, so add that now. Enable nullable
support. Add an Id property and a constructor that initializes it, as shown in the
following code:
C#
Next, add a static method to create new participants by generating a random ID:
C#
The main responsibility of this class is to generate the responses for a participant to the
questions in the survey. This responsibility has a few steps:
1. Ask for participation in the survey. If the person doesn't consent, return a missing
(or null) response.
2. Ask each question and record the answer. Each answer may also be missing (or
null).
Add the following code to your SurveyResponse class:
C#namespace  NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }
        public SurveyResponse (int id) => Id = id;
    }
}
private static readonly  Random randomGenerator = new Random();
public static SurveyResponse GetRandomId () => new 
SurveyResponse(randomGenerator.Next());The storage for the survey answers is a Dictionary<int, string>?, indicating that it may
be null. Y ou're using the new language feature to declare your design intent, both to the
compiler and to anyone reading your code later. If you ever dereferenceprivate Dictionary< int, string>? surveyResponses;
public bool AnswerSurvey (IEnumerable<SurveyQuestion> questions )
{
    if (ConsentToSurvey())
    {
        surveyResponses = new Dictionary< int, string>();
        int index = 0;
        foreach (var question in questions)
        {
            var answer = GenerateAnswer(question);
            if (answer != null)
            {
                surveyResponses.Add(index, answer);
            }
            index++;
        }
    }
    return surveyResponses != null;
}
private bool ConsentToSurvey () => randomGenerator.Next( 0, 2) == 1;
private string? GenerateAnswer(SurveyQuestion question)
{
    switch (question.TypeOfQuestion)
    {
        case QuestionType.YesNo:
            int n = randomGenerator.Next( -1, 2);
            return (n == -1) ? default : (n == 0) ? "No" : "Yes";
        case QuestionType.Number:
            n = randomGenerator.Next( -30, 101);
            return (n < 0) ? default : n.ToString();
        case QuestionType.Text:
        default:
            switch (randomGenerator.Next( 0, 5))
            {
                case 0:
                    return default;
                case 1:
                    return "Red";
                case 2:
                    return "Green";
                case 3:
                    return "Blue";
            }
            return "Red. No, Green. Wait.. Blue... AAARGGGGGHHH!" ;
    }
}surveyResponses without checking for the null value first, you'll get a compiler warning.
You don't get a warning in the AnswerSurvey method because the compiler can
determine the surveyResponses variable was set to a non-null value above.
Using null for missing answers highlights a key point for working with nullable
reference types: your goal isn't to remove all null values from your program. Rather,
your goal is to ensure that the code you write expresses the intent of your design.
Missing values are a necessary concept to express in your code. The null value is a clear
way to express those missing values. T rying to remove all null values only leads to
defining some other way to express those missing values without null.
Next, you need to write the PerformSurvey method in the SurveyRun class. Add the
following code in the SurveyRun class:
C#
Here again, your choice of a nullable List<SurveyResponse>? indicates the response may
be null. That indicates the survey hasn't been given to any respondents yet. Notice that
respondents are added until enough have consented.
The last step to run the survey is to add a call to perform the survey at the end of the
Main method:
C#private List<SurveyResponse>? respondents;
public void PerformSurvey (int numberOfRespondents )
{
    int respondentsConsenting = 0;
    respondents = new List<SurveyResponse>();
    while (respondentsConsenting < numberOfRespondents)
    {
        var respondent = SurveyResponse.GetRandomId();
        if (respondent.AnswerSurvey(surveyQuestions))
            respondentsConsenting++;
        respondents.Add(respondent);
    }
}
surveyRun.PerformSurvey( 50);
Examine survey responsesThe last step is to display survey results. Y ou'll add code to many of the classes you've
written. This code demonstrates the value of distinguishing nullable and non-nullable
reference types. S tart by adding the following two expression-bodied members to the
SurveyResponse class:
C#
Because surveyResponses is a nullable reference type, null checks are necessary before
de-referencing it. The Answer method returns a non-nullable string, so we have to cover
the case of a missing answer by using the null-coalescing operator.
Next, add these three expression-bodied members to the SurveyRun class:
C#
The AllParticipants member must take into account that the respondents variable
might be null, but the return value can't be null. If you change that expression by
removing the ?? and the empty sequence that follows, the compiler warns you the
method might return null and its return signature returns a non-nullable type.
Finally, add the following loop at the bottom of the Main method:
C#public bool AnsweredSurvey => surveyResponses != null;
public string Answer(int index) => surveyResponses?.GetValueOrDefault(index)  
?? "No answer" ;
public IEnumerable<SurveyResponse> AllParticipants => (respondents ??  
Enumerable.Empty<SurveyResponse>());
public ICollection<SurveyQuestion> Questions => surveyQuestions;
public SurveyQuestion GetQuestion (int index) => surveyQuestions[index];
foreach (var participant in surveyRun.AllParticipants)
{
    Console.WriteLine( $"Participant: {participant.Id} :");
    if (participant.AnsweredSurvey)
    {
        for (int i = 0; i < surveyRun.Questions.Count; i++)
        {
            var answer = participant.Answer(i);
            Console.WriteLine( $"\t{surveyRun.GetQuestion(i).QuestionText}  : 
{answer} ");
        }
    }
    else
    {You don't need any null checks in this code because you've designed the underlying
interfaces so that they all return non-nullable reference types.
You can get the code for the finished tutorial from our samples  repository in the
csharp/NullableIntroduction  folder.
Experiment by changing the type declarations between nullable and non-nullable
reference types. See how that generates different warnings to ensure you don't
accidentally dereference a null.
Learn how to use nullable reference type when using Entity Framework:        Console.WriteLine( "\tNo responses" );
    }
}
Get the code
Next steps
Entity Framew ork Cor e Fundamentals: W orking with Nullable R eference T ypes
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
 Provide product feedbackUse string interpolation to construct
formatted strings
Article •09/15/2021
This tutorial teaches you how to use C# string interpolation  to insert values into a single
result string. Y ou write C# code and see the results of compiling and running it. The
tutorial contains a series of lessons that show you how to insert values into a string and
format those values in different ways.
This tutorial expects that you have a machine you can use for development. The .NET
tutorial Hello W orld in 10 minutes  has instructions for setting up your local
development environment on Windows, Linux, or macOS. Y ou can also complete the
interactive version  of this tutorial in your browser.
Create a directory named interpolat ed. Make it the current directory and run the
following command from a console window:
.NET CLI
This command creates a new .NET Core console application in the current directory.
Open Program.cs  in your favorite editor, and replace the line Console.WriteLine("Hello
World!"); with the following code, where you replace <name> with your name:
C#
Try this code by typing dotnet run in your console window. When you run the program,
it displays a single string that includes your name in the greeting. The string included in
the WriteLine  method call is an interpolat ed str ing expr ession . It's a kind of template that
lets you construct a single string (called the result str ing) from a string that includes
embedded code. Interpolated strings are particularly useful for inserting values into a
string or concatenating (joining together) strings.
Create an interpolated string
dotnet new console  
var name = "<name>" ; 
Console.WriteLine( $"Hello, {name}. It's a pleasure to meet you!" ); This simple example contains the two elements that every interpolated string must have:
A string literal that begins with the $ character before its opening quotation mark
character. There can't be any spaces between the $ symbol and the quotation
mark character. (If you'd like to see what happens if you include one, insert a space
after the $ character, save the file, and run the program again by typing dotnet
run in the console window. The C# compiler displays an error message, "error
CS1056: Unexpected character '$'".)
One or more interpolation expr essions . An interpolation expression is indicated by
an opening and closing brace ( { and }). You can put any C# expression that
returns a value (including null) inside the braces.
Let's try a few more string interpolation examples with some other data types.
In the previous section, you used string interpolation to insert one string inside of
another. The result of an interpolation expression can be of any data type, though. Let's
include values of various data types in an interpolated string.
In the following example, we first define a class  data type Vegetable that has a Name
property  and a ToString method , which overrides  the behavior of the Object.T oString()
method. The public  access modifier  makes that method available to any client code to
get the string representation of a Vegetable instance. In the example the
Vegetable.ToString method returns the value of the Name property that is initialized at
the Vegetable constructor :
C#
Then we create an instance of the Vegetable class named item by using the new
operator  and providing a name for the constructor Vegetable:
C#
Finally, we include the item variable into an interpolated string that also contains a
DateTime  value, a Decimal  value, and a Unit enumeration  value. R eplace all of the C#Include different data types
public Vegetable (string name) => Name = name;  
var item = new Vegetable( "eggplant" ); code in your editor with the following code, and then use the dotnet run command to
run it:
C#
Note that the interpolation expression item in the interpolated string resolves to the
text "eggplant" in the result string. That's because, when the type of the expression
result is not a string, the result is resolved to a string in the following way:
If the interpolation expression evaluates to null, an empty string ("", or
String.Empty ) is used.
If the interpolation expression doesn't evaluate to null, typically the ToString
method of the result type is called. Y ou can test this by updating the
implementation of the Vegetable.ToString method. Y ou might not even need to
implement the ToString method since every type has some implementation of this
method. T o test this, comment out the definition of the Vegetable.ToString
method in the example (to do that, put a comment symbol, //, in front of it). In
the output, the string "eggplant" is replaced by the fully qualified type name
("Vegetable" in this example), which is the default behavior of the Object.T oString()using System;  
public class Vegetable  
{ 
   public Vegetable (string name) => Name = name;  
   public string Name { get; } 
   public override  string ToString () => Name;  
} 
public class Program 
{ 
   public enum Unit { item, kilogram, gram, dozen };  
   public static void Main() 
   { 
      var item = new Vegetable( "eggplant" ); 
      var date = DateTime.Now;  
      var price = 1.99m; 
      var unit = Unit.item;  
      Console.WriteLine( $"On {date}, the price of {item} was {price} per 
{unit}."); 
   } 
} method. The default behavior of the ToString method for an enumeration value is
to return the string representation of the value.
In the output from this example, the date is too precise (the price of eggplant doesn't
change every second), and the price value doesn't indicate a unit of currency. In the next
section, you'll learn how to fix those issues by controlling the format of string
representations of the expression results.
In the previous section, two poorly formatted strings were inserted into the result string.
One was a date and time value for which only the date was appropriate. The second was
a price that didn't indicate its unit of currency. Both issues are easy to address. S tring
interpolation lets you specify format str ings that control the formatting of particular
types. Modify the call to Console.WriteLine from the previous example to include the
format strings for the date and price expressions as shown in the following line:
C#
You specify a format string by following the interpolation expression with a colon (":")
and the format string. "d" is a standard date and time format string  that represents the
short date format. "C2" is a standard numeric format string  that represents a number as
a currency value with two digits after the decimal point.
A number of types in the .NET libraries support a predefined set of format strings. These
include all the numeric types and the date and time types. For a complete list of types
that support format strings, see Format S trings and .NET Class Library T ypes in the
Formatting T ypes in .NET  article.
Try modifying the format strings in your text editor and, each time you make a change,
rerun the program to see how the changes affect the formatting of the date and time
and the numeric value. Change the "d" in {date:d} to "t" (to display the short time
format), "y" (to display the year and month), and "yyyy" (to display the year as a four-
digit number). Change the "C2" in {price:C2} to "e" (for exponential notation) and "F3"
(for a numeric value with three digits after the decimal point).
In addition to controlling formatting, you can also control the field width and alignment
of the formatted strings that are included in the result string. In the next section, you'llControl the formatting of interpolation
expressions
Console.WriteLine( $"On {date:d} , the price of {item} was {price:C2}  per 
{unit}."); learn how to do this.
Ordinarily, when the result of an interpolation expression is formatted to string, that
string is included in a result string without leading or trailing spaces. P articularly when
you work with a set of data, being able to control a field width and text alignment helps
to produce a more readable output. T o see this, replace all the code in your text editor
with the following code, then type dotnet run to execute the program:
C#
The names of authors are left-aligned, and the titles they wrote are right-aligned. Y ou
specify the alignment by adding a comma (",") after an interpolation expression and
designating the minimum  field width. If the specified value is a positive number, the
field is right-aligned. If it is a negative number, the field is left-aligned.
Try removing the negative signs from the {"Author",-25} and {title.Key,-25} code
and run the example again, as the following code does:
C#Control the field width and alignment of
interpolation expressions
using System;  
using System.Collections.Generic;
public class Example 
{ 
   public static void Main() 
   { 
      var titles = new Dictionary< string, string>() 
      { 
          [ "Doyle, Arthur Conan" ] = "Hound of the Baskervilles, The" , 
          [ "London, Jack" ] = "Call of the Wild, The" , 
          [ "Shakespeare, William" ] = "Tempest, The"  
      };  
      Console.WriteLine( "Author and Title List" ); 
      Console.WriteLine();  
      Console.WriteLine( $"|{"Author" ,-25}|{"Title",30}|"); 
      foreach (var title in titles)  
         Console.WriteLine( $"|{title.Key, -25}|{title.Value, 30}|"); 
   } 
} This time, the author information is right-aligned.
You can combine an alignment specifier and a format string for a single interpolation
expression. T o do that, specify the alignment first, followed by a colon and the format
string. R eplace all of the code inside the Main method with the following code, which
displays three formatted strings with defined field widths. Then run the program by
entering the dotnet run command.
C#
The output looks something like the following:
Console
You've completed the string interpolation tutorial.
For more information, see the String interpolation  topic and the String interpolation in
C# tutorial.Console.WriteLine( $"|{"Author" ,25}|{"Title",30}|"); 
foreach (var title in titles)  
   Console.WriteLine( $"|{title.Key, 25}|{title.Value, 30}|"); 
Console.WriteLine( $"[{DateTime.Now, -20:d}] Hour [ {DateTime.Now, -10:HH}] 
[{1063.342 ,15:N2}] feet"); 
[04/14/2018          ] Hour [16        ] [       1,063.34] feet  String interpolation in C#
Article •08/29/2023
This tutorial shows you how to use string interpolation  to format and include expression
results in a result string. The examples assume that you are familiar with basic C#
concepts and .NET type formatting. If you are new to string interpolation or .NET type
formatting, check out the interactive string interpolation tutorial  first. For more
information about formatting types in .NET, see Formatting types in .NET .
To identify a string literal as an interpolated string, prepend it with the $ symbol. Y ou
can embed any valid C# expression that returns a value in an interpolated string. In the
following example, as soon as an expression is evaluated, its result is converted into a
string and included in a result string:
C#
As the example shows, you include an expression in an interpolated string by enclosing
it with braces:
C#
Interpolated strings support all the capabilities of the string composite formatting
feature. That makes them a more readable alternative to the use of the String.Format
method.Introduction
double a = 3;
double b = 4;
Console.WriteLine( $"Area of the right triangle with legs of {a} and {b} is 
{0.5 * a * b} ");
Console.WriteLine( $"Length of the hypotenuse of the right triangle with legs  
of {a} and {b} is {CalculateHypotenuse(a, b)} ");
double CalculateHypotenuse (double leg1, double leg2) => Math.Sqrt(leg1 *  
leg1 + leg2 * leg2);
// Output:
// Area of the right triangle with legs of 3 and 4 is 6
// Length of the hypotenuse of the right triangle with legs of 3 and 4 is 5
{<interpolationExpression>}To specify a format string that is supported by the type of the expression result, follow
the interpolation expression with a colon (":") and the format string:
C#
The following example shows how to specify standard and custom format strings for
expressions that produce date and time or numeric results:
C#
For more information, see the Format string component  section of the Composite
formatting  article.
To specify the minimum field width and the alignment of the formatted expression
result, follow the interpolation expression with a comma (",") and the constant
expression:
C#
If the alignment  value is positive, the formatted expression result is right-aligned; if
negative, it's left-aligned.
If you need to specify both alignment and a format string, start with the alignment
component:How to specify a format string for an
interpolation expression
{<interpolationExpression>:<formatString>}
var date = new DateTime( 1731, 11, 25);
Console.WriteLine( $"On {date:dddd, MMMM dd, yyyy}  L. Euler introduced the  
letter e to denote {Math.E:F5} .");
// Output:
// On Sunday, November 25, 1731 L. Euler introduced the letter e to denote  
2.71828.
How to control the field width and alignment
of the formatted interpolation expression
{<interpolationExpression>,<alignment>}C#
The following example shows how to specify alignment and uses pipe characters ("|") to
delimit text fields:
C#
As the example output shows, if the length of the formatted expression result exceeds
specified field width, the alignment  value is ignored.
For more information, see the Alignment component  section of the Composite
formatting  article.
Interpolated strings support all escape sequences that can be used in ordinary string
literals. For more information, see String escape sequences .
To interpret escape sequences literally, use a verbatim  string literal. An interpolated
verbatim string starts with the both $ and @ characters. Y ou can use $ and @ in any
order: both $@"..." and @$"..." are valid interpolated verbatim strings.
To include a brace, "{" or "}", in a result string, use two braces, "{{" or "}}". For more
information, see the Escaping braces  section of the Composite formatting  article.{<interpolationExpression>,<alignment>:<formatString>}
const int NameAlignment = -9;
const int ValueAlignment = 7;
double a = 3;
double b = 4;
Console.WriteLine( $"Three classical Pythagorean means of {a} and {b}:");
Console.WriteLine( $"|{"Arithmetic" ,NameAlignment} |{0.5 * (a + 
b),ValueAlignment:F3} |");
Console.WriteLine( $"|{"Geometric" ,NameAlignment} |{Math.Sqrt(a *  
b),ValueAlignment:F3} |");
Console.WriteLine( $"|{"Harmonic" ,NameAlignment} |{2 / (1 / a + 1 / 
b),ValueAlignment:F3} |");
// Output:
// Three classical Pythagorean means of 3 and 4:
// |Arithmetic|  3.500|
// |Geometric|  3.464|
// |Harmonic |  3.429|
How to use escape sequences in an
interpolated stringThe following example shows how to include braces in a result string and construct a
verbatim interpolated string:
C#
Beginning with C# 11, you can use interpolated raw string literals .
As the colon (":") has special meaning in an item with an interpolation expression, in
order to use a conditional operator  in an expression, enclose it in parentheses, as the
following example shows:
C#
By default, an interpolated string uses the current culture defined by the
CultureInfo.CurrentCulture  property for all formatting operations.var xs = new int[] { 1, 2, 7, 9 };
var ys = new int[] { 7, 9, 12 };
Console.WriteLine( $"Find the intersection of the {{ {string.Join(", ",xs)}}} 
and {{{string.Join(", ",ys)}}} sets." );
// Output:
// Find the intersection of the {1, 2, 7, 9} and {7, 9, 12} sets.
var userName = "Jane";
var stringWithEscapes = $"C:\\Users\\ {userName} \\Documents" ;
var verbatimInterpolated = $@"C:\Users\ {userName} \Documents" ;
Console.WriteLine(stringWithEscapes);
Console.WriteLine(verbatimInterpolated);
// Output:
// C:\Users\Jane\Documents
// C:\Users\Jane\Documents
How to use a ternary conditional operator ?:
in an interpolation expression
var rand = new Random();
for (int i = 0; i < 7; i++)
{
    Console.WriteLine( $"Coin flip: {(rand.NextDouble() < 0.5 ? "heads" : 
"tails")}");
}
How to create a cultur e-specific result string
with string interpolationBeginning with .NET 6, you can use the String.Create(IFormatProvider,
DefaultInterpolatedS tringHandler)  method to resolve an interpolated string to a culture-
specific result string, as the following example shows:
C#
In earlier versions of .NET, use implicit conversion of an interpolated string to a
System.FormattableS tring  instance and call its ToString(IFormatProvider)  method to
create a culture-specific result string. The following example shows how to do that:
C#var cultures = new System.Globalization.CultureInfo[]
{
    System.Globalization.CultureInfo.GetCultureInfo( "en-US"),
    System.Globalization.CultureInfo.GetCultureInfo( "en-GB"),
    System.Globalization.CultureInfo.GetCultureInfo( "nl-NL"),
    System.Globalization.CultureInfo.InvariantCulture
};
var date = DateTime.Now;
var number = 31_415_926 .536;
foreach (var culture in cultures)
{
    var cultureSpecificMessage = string.Create(culture, $"{date,23}
{number, 20:N3}");
    Console.WriteLine( $"{culture.Name, -10}{cultureSpecificMessage} ");
}
// Output is similar to:
// en-US       8/27/2023 12:35:31 PM      31,415,926.536
// en-GB         27/08/2023 12:35:31      31,415,926.536
// nl-NL         27-08-2023 12:35:31      31.415.926,536
//               08/27/2023 12:35:31      31,415,926.536
var cultures = new System.Globalization.CultureInfo[]
{
    System.Globalization.CultureInfo.GetCultureInfo( "en-US"),
    System.Globalization.CultureInfo.GetCultureInfo( "en-GB"),
    System.Globalization.CultureInfo.GetCultureInfo( "nl-NL"),
    System.Globalization.CultureInfo.InvariantCulture
};
var date = DateTime.Now;
var number = 31_415_926 .536;
FormattableString message = $"{date,23}{number, 20:N3}";
foreach (var culture in cultures)
{
    var cultureSpecificMessage = message.ToString(culture);
    Console.WriteLine( $"{culture.Name, -10}{cultureSpecificMessage} ");
}
// Output is similar to:
// en-US       8/27/2023 12:35:31 PM      31,415,926.536
// en-GB         27/08/2023 12:35:31      31,415,926.536As the example shows, you can use one FormattableS tring  instance to generate multiple
result strings for various cultures.
Beginning with .NET 6, use the String.Create(IFormatProvider,
DefaultInterpolatedS tringHandler)  method to resolve an interpolated string to a result
string for the InvariantCulture , as the following example shows:
C#
In earlier versions of .NET, along with the FormattableS tring.T oString(IFormatProvider)
method, you can use the static FormattableS tring.Invariant  method, as the following
example shows:
C#
This tutorial describes common scenarios of string interpolation usage. For more
information about string interpolation, see String interpolation . For more information
about formatting types in .NET, see the Formatting types in .NET  and Composite
formatting  articles.// nl-NL         27-08-2023 12:35:31      31.415.926,536
//               08/27/2023 12:35:31      31,415,926.536
How to create a result string using the invariant
cultur e
string message = string.Create(CultureInfo.InvariantCulture, $"Date and time  
in invariant culture: {DateTime.Now} ");
Console.WriteLine(message);
// Output is similar to:
// Date and time in invariant culture: 05/17/2018 15:46:24
string message = FormattableString.Invariant( $"Date and time in invariant  
culture: {DateTime.Now} ");
Console.WriteLine(message);
// Output is similar to:
// Date and time in invariant culture: 05/17/2018 15:46:24
Conclusion
See alsoString.Format
System.FormattableS tring
System.IFormattable
StringsConsole app
Article •03/14/2023
This tutorial teaches you a number of features in .NET and the C# language. Y ou'll learn:
The basics of the .NET CLI
The structure of a C# Console Application
Console I/O
The basics of File I/O APIs in .NET
The basics of the T ask-based Asynchronous Programming in .NET
You'll build an application that reads a text file, and echoes the contents of that text file
to the console. The output to the console is paced to match reading it aloud. Y ou can
speed up or slow down the pace by pressing the '<' (less than) or '>' (greater than) keys.
You can run this application on Windows, Linux, macOS, or in a Docker container.
There are a lot of features in this tutorial. Let's build them one by one.
.NET 6 SDK .
A code editor.
The first step is to create a new application. Open a command prompt and create a new
directory for your application. Make that the current directory. T ype the command
dotnet new console at the command prompt. This creates the starter files for a basic
"Hello W orld" application.
Before you start making modifications, let's run the simple Hello W orld application. After
creating the application, type dotnet run at the command prompt. This command runs
the NuGet package restore process, creates the application executable, and runs the
executable.
The simple Hello W orld application code is all in Program.cs . Open that file with your
favorite text editor. R eplace the code in Program.cs  with the following code:
C#Prerequisites
Create the app
namespace  TeleprompterConsole ; At the top of the file, see a namespace statement. Like other Object Oriented languages
you may have used, C# uses namespaces to organize types. This Hello W orld program is
no different. Y ou can see that the program is in the namespace with the name
TeleprompterConsole.
The first feature to add is the ability to read a text file and display all that text to the
console. First, let's add a text file. Copy the sampleQuotes.txt  file from the GitHub
repository for this sample  into your project directory. This will serve as the script for
your application. For information on how to download the sample app for this tutorial,
see the instructions in Samples and Tutorials .
Next, add the following method in your Program class (right below the Main method):
C#
This method is a special type of C# method called an iterator method . Iterator methods
return sequences that are evaluated lazily. That means each item in the sequence is
generated as it is requested by the code consuming the sequence. Iterator methods are
methods that contain one or more yield return  statements. The object returned by the
ReadFrom method contains the code to generate each item in the sequence. In this
example, that involves reading the next line of text from the source file, and returning
that string. Each time the calling code requests the next item from the sequence, theinternal  class Program 
{ 
    static void Main(string[] args) 
    { 
        Console.WriteLine( "Hello World!" ); 
    } 
} 
Reading and Echoing the File
static IEnumerable< string> ReadFrom (string file) 
{ 
    string? line; 
    using (var reader = File.OpenText(file))  
    { 
        while ((line = reader.ReadLine()) != null) 
        {  
            yield return line; 
        }  
    } 
} code reads the next line of text from the file and returns it. When the file is completely
read, the sequence indicates that there are no more items.
There are two C# syntax elements that may be new to you. The using  statement in this
method manages resource cleanup. The variable that is initialized in the using
statement ( reader, in this example) must implement the IDisposable  interface. That
interface defines a single method, Dispose, that should be called when the resource
should be released. The compiler generates that call when execution reaches the closing
brace of the using statement. The compiler-generated code ensures that the resource is
released even if an exception is thrown from the code in the block defined by the using
statement.
The reader variable is defined using the var keyword. var defines an implicitly typed
local v ariable . That means the type of the variable is determined by the compile-time
type of the object assigned to the variable. Here, that is the return value from the
OpenT ext(S tring)  method, which is a StreamR eader  object.
Now, let's fill in the code to read the file in the Main method:
C#
Run the program (using dotnet run) and you can see every line printed out to the
console.
What you have is being displayed far too fast to read aloud. Now you need to add the
delays in the output. As you start, you'll be building some of the core code that enables
asynchronous processing. However, these first steps will follow a few anti-patterns. The
anti-patterns are pointed out in comments as you add the code, and the code will be
updated in later steps.
There are two steps to this section. First, you'll update the iterator method to return
single words instead of entire lines. That's done with these modifications. R eplace the
yield return line; statement with the following code:
C#var lines = ReadFrom( "sampleQuotes.txt" ); 
foreach (var line in lines) 
{ 
    Console.WriteLine(line);  
} 
Adding Delays and Formatting  outputNext, you need to modify how you consume the lines of the file, and add a delay after
writing each word. R eplace the Console.WriteLine(line) statement in the Main method
with the following block:
C#
Run the sample, and check the output. Now, each single word is printed, followed by a
200 ms delay. However, the displayed output shows some issues because the source
text file has several lines that have more than 80 characters without a line break. That
can be hard to read while it's scrolling by. That's easy to fix. Y ou'll just keep track of the
length of each line, and generate a new line whenever the line length reaches a certain
threshold. Declare a local variable after the declaration of words in the ReadFrom method
that holds the line length:
C#
Then, add the following code after the yield return word + " "; statement (before the
closing brace):
C#var words = line.Split( ' '); 
foreach (var word in words) 
{ 
    yield return word + " "; 
} 
yield return Environment.NewLine;  
Console.Write(line);  
if (!string.IsNullOrWhiteSpace(line))  
{ 
    var pause = Task.Delay( 200); 
    // Synchronously waiting on a task is an  
    // anti-pattern. This will get fixed in later  
    // steps.  
    pause.Wait();  
} 
var lineLength = 0; 
lineLength += word.Length + 1; 
if (lineLength > 70) 
{ 
    yield return Environment.NewLine;  
    lineLength = 0; 
} Run the sample, and you'll be able to read aloud at its pre-configured pace.
In this final step, you'll add the code to write the output asynchronously in one task,
while also running another task to read input from the user if they want to speed up or
slow down the text display, or stop the text display altogether. This has a few steps in it
and by the end, you'll have all the updates that you need. The first step is to create an
asynchronous Task returning method that represents the code you've created so far to
read and display the file.
Add this method to your Program class (it's taken from the body of your Main method):
C#
You'll notice two changes. First, in the body of the method, instead of calling Wait() to
synchronously wait for a task to finish, this version uses the await keyword. In order to
do that, you need to add the async modifier to the method signature. This method
returns a Task. Notice that there are no return statements that return a Task object.
Instead, that Task object is created by code the compiler generates when you use the
await operator. Y ou can imagine that this method returns when it reaches an await.
The returned Task indicates that the work has not completed. The method resumes
when the awaited task completes. When it has executed to completion, the returned
Task indicates that it is complete. Calling code can monitor that returned Task to
determine when it has completed.
Add an await keyword before the call to ShowTeleprompter:
C#Async Tasks
private static async Task ShowTeleprompter () 
{ 
    var words = ReadFrom( "sampleQuotes.txt" ); 
    foreach (var word in words) 
    { 
        Console.Write(word);  
        if (!string.IsNullOrWhiteSpace(word))  
        {  
            await Task.Delay( 200); 
        }  
    } 
} This requires you to change the Main method signature to:
C#
Learn more about the async Main  method  in our fundamentals section.
Next, you need to write the second asynchronous method to read from the Console and
watch for the '<' (less than), '>' (greater than) and 'X' or 'x' keys. Here's the method you
add for that task:
C#
This creates a lambda expression to represent an Action  delegate that reads a key from
the Console and modifies a local variable representing the delay when the user presses
the '<' (less than) or '>' (greater than) keys. The delegate method finishes when user
presses the 'X' or 'x' keys, which allow the user to stop the text display at any time. This
method uses ReadK ey() to block and wait for the user to press a key.await ShowTeleprompter();  
static async Task Main(string[] args) 
private static async Task GetInput () 
{ 
    var delay = 200; 
    Action work = () =>  
    { 
        do { 
            var key = Console.ReadKey( true); 
            if (key.KeyChar == '>') 
            {  
                delay -= 10; 
            }  
            else if (key.KeyChar == '<') 
            {  
                delay += 10; 
            }  
            else if (key.KeyChar == 'X' || key.KeyChar == 'x') 
            {  
                break; 
            }  
        } while (true); 
    }; 
    await Task.Run(work);  
} To finish this feature, you need to create a new async Task returning method that starts
both of these tasks ( GetInput and ShowTeleprompter), and also manages the shared data
between these two tasks.
It's time to create a class that can handle the shared data between these two tasks. This
class contains two public properties: the delay, and a flag Done to indicate that the file
has been completely read:
C#
Put that class in a new file, and include that class in the TeleprompterConsole namespace
as shown. Y ou'll also need to add a using static statement at the top of the file so that
you can reference the Min and Max methods without the enclosing class or namespace
names. A using static  statement imports the methods from one class. This is in contrast
with the using statement without static, which imports all classes from a namespace.
C#
Next, you need to update the ShowTeleprompter and GetInput methods to use the new
config object. Write one final Task returning async method to start both tasks and exit
when the first task finishes:
C#namespace  TeleprompterConsole ; 
internal  class TelePrompterConfig  
{ 
    public int DelayInMilliseconds { get; private set; } = 200; 
    public void UpdateDelay (int increment ) // negative to speed up  
    { 
        var newDelay = Min(DelayInMilliseconds + increment, 1000); 
        newDelay = Max(newDelay, 20); 
        DelayInMilliseconds = newDelay;  
    } 
    public bool Done { get; private set; } 
    public void SetDone() 
    { 
        Done = true; 
    } 
} 
using static System.Math;  
private static async Task RunTeleprompter () 
{ The one new method here is the WhenAny(T ask[])  call. That creates a Task that finishes
as soon as any of the tasks in its argument list completes.
Next, you need to update both the ShowTeleprompter and GetInput methods to use the
config object for the delay:
C#
This new version of ShowTeleprompter calls a new method in the TeleprompterConfig
class. Now, you need to update Main to call RunTeleprompter instead of
ShowTeleprompter:    var config = new TelePrompterConfig();  
    var displayTask = ShowTeleprompter(config);  
    var speedTask = GetInput(config);  
    await Task.WhenAny(displayTask, speedTask);  
} 
private static async Task ShowTeleprompter (TelePrompterConfig config ) 
{ 
    var words = ReadFrom( "sampleQuotes.txt" ); 
    foreach (var word in words) 
    { 
        Console.Write(word);  
        if (!string.IsNullOrWhiteSpace(word))  
        {  
            await Task.Delay(config.DelayInMilliseconds);  
        }  
    } 
    config.SetDone();  
} 
private static async Task GetInput (TelePrompterConfig config ) 
{ 
    Action work = () =>  
    { 
        do { 
            var key = Console.ReadKey( true); 
            if (key.KeyChar == '>') 
                config.UpdateDelay( -10); 
            else if (key.KeyChar == '<') 
                config.UpdateDelay( 10); 
            else if (key.KeyChar == 'X' || key.KeyChar == 'x') 
                config.SetDone();
        } while (!config.Done);  
    }; 
    await Task.Run(work);  
} C#
This tutorial showed you a number of the features around the C# language and the .NET
Core libraries related to working in Console applications. Y ou can build on this
knowledge to explore more about the language, and the classes introduced here. Y ou've
seen the basics of File and Console I/O, blocking and non-blocking use of the T ask-
based asynchronous programming, a tour of the C# language and how C# programs are
organized, and the .NET CLI.
For more information about File I/O, see File and S tream I/O . For more information
about asynchronous programming model used in this tutorial, see Task-based
Asynchronous Programming  and Asynchronous programming .await RunTeleprompter();  
ConclusionTutorial: Make HTTP requests in a .NET
console app using C#
Article •10/29/2022
This tutorial builds an app that issues HT TP requests to a REST service on GitHub. The
app reads information in JSON format and converts the JSON into C# objects.
Converting from JSON to C# objects is known as deserialization .
The tutorial shows how to:
If you prefer to follow along with the final sample  for this tutorial, you can download it.
For download instructions, see Samples and Tutorials .
.NET SDK 6.0 or later
A code editor such as [Visual S tudio Code  (an open-source, cross-platform
editor). Y ou can run the sample app on Windows, Linux, or macOS, or in a Docker
container.
1. Open a command prompt and create a new directory for your app. Make that the
current directory.
2. Enter the following command in a console window:
.NET CLI
This command creates the starter files for a basic "Hello W orld" app. The project
name is "W ebAPIClient".
3. Navigate into the "W ebAPIClient" directory, and run the app.
.NET CLISend HT TP requests. ＂
Deserialize JSON responses. ＂
Configure deserialization with attributes. ＂
Prerequisites
Create the client app
dotnet new console  --name WebAPIClient.NET CLI
dotnet run  automatically runs dotnet restore  to restore any dependencies that the
app needs. It also runs dotnet build  if needed. Y ou should see the app output
"Hello, World!". In your terminal, press Ctrl+C to stop the app.
This app calls the GitHub API  to get information about the projects under the .NET
Foundation  umbrella. The endpoint is https://api.github.com/orgs/dotnet/repos . To
retrieve information, it makes an HT TP GET request. Browsers also make HT TP GET
requests, so you can paste that URL into your browser address bar to see what
information you'll be receiving and processing.
Use the HttpClient  class to make HT TP requests. HttpClient  supports only async
methods for its long-running APIs. So the following steps create an async method and
call it from the Main method.
1. Open the Program.cs file in your project directory and replace its contents with the
following:
C#
This code:
Replaces the Console.WriteLine statement with a call to
ProcessRepositoriesAsync that uses the await keyword.
Defines an empty ProcessRepositoriesAsync method.
2. In the Program class, use an HttpClient  to handle requests and responses, by
replacing the content with the following C#.cd WebAPIClient
dotnet run
Make HTTP requests
await ProcessRepositoriesAsync();
static async Task ProcessRepositoriesAsync (HttpClient client )
{
}C#
This code:
Sets up HT TP headers for all requests:
An Accept  header to accept JSON responses
A User-Agent  header. These headers are checked by the GitHub server
code and are necessary to retrieve information from GitHub.
3. In the ProcessRepositoriesAsync method, call the GitHub endpoint that returns a
list of all repositories under the .NET foundation organization:
C#
This code:
Awaits the task returned from calling HttpClient.GetS tringAsync(S tring)
method. This method sends an HT TP GET request to the specified URI. The
body of the response is returned as a String , which is available when the task
completes.
The response string json is printed to the console.
4. Build the app and run it.using System.Net.Http.Headers;
using HttpClient client = new();
client.DefaultRequestHeaders.Accept.Clear();
client.DefaultRequestHeaders.Accept.Add(
    new 
MediaTypeWithQualityHeaderValue( "application/vnd.github.v3+json" ));
client.DefaultRequestHeaders.Add( "User-Agent" , ".NET Foundation  
Repository Reporter" );
await ProcessRepositoriesAsync(client);
static async Task ProcessRepositoriesAsync (HttpClient client )
{
}
 static async Task ProcessRepositoriesAsync (HttpClient client )
 {
     var json = await client.GetStringAsync(
         "https://api.github.com/orgs/dotnet/repos" );
     Console.Write(json);
 }.NET CLI
There is no build warning because the ProcessRepositoriesAsync now contains an
await operator. The output is a long display of JSON text.
The following steps convert the JSON response into C# objects. Y ou use the
System.T ext.Json.JsonSerializer  class to deserialize JSON into objects.
1. Create a file named Reposit ory.cs and add the following code:
C#
The preceding code defines a class to represent the JSON object returned from the
GitHub API. Y ou'll use this class to display a list of repository names.
The JSON for a repository object contains dozens of properties, but only the name
property will be deserialized. The serializer automatically ignores JSON properties
for which there is no match in the target class. This feature makes it easier to
create types that work with only a subset of fields in a large JSON packet.
The C# convention is to capitalize the first letter of property names , but the name
property here starts with a lowercase letter because that matches exactly what's in
the JSON. Later you'll see how to use C# property names that don't match the
JSON property names.
2. Use the serializer to convert JSON into C# objects. R eplace the call to
GetStringAsync(S tring)  in the ProcessRepositoriesAsync method with the following
lines:
C#dotnet run
Deserialize the JSON Result
public record class Repository (string name);
await using Stream stream =
    await 
client.GetStreamAsync( "https://api.github.com/orgs/dotnet/repos" );
var repositories =
    await JsonSerializer.DeserializeAsync<List<Repository>>(stream);The updated code replaces GetStringAsync(S tring)  with GetStreamAsync(S tring) .
This serializer method uses a stream instead of a string as its source.
The first argument to JsonSerializer.DeserializeAsync<T Value>(S tream,
JsonSerializerOptions, CancellationT oken)  is an await expression. await
expressions can appear almost anywhere in your code, even though up to now,
you've only seen them as part of an assignment statement. The other two
parameters, JsonSerializerOptions and CancellationToken, are optional and are
omitted in the code snippet.
The DeserializeAsync method is gener ic, which means you supply type arguments
for what kind of objects should be created from the JSON text. In this example,
you're deserializing to a List<Repository>, which is another generic object, a
System.Collections.Generic.List<T> . The List<T> class stores a collection of
objects. The type argument declares the type of objects stored in the List<T>. The
type argument is your Repository record, because the JSON text represents a
collection of repository objects.
3. Add code to display the name of each repository. R eplace the lines that read:
C#
with the following code:
C#
4. The following using directives should be present at the top of the file:
C#
5. Run the app.
.NET CLIConsole.Write(json);
foreach (var repo in repositories ?? Enumerable.Empty<Repository>())
    Console.Write(repo.name);
using System.Net.Http.Headers;
using System.Text.Json;
dotnet runThe output is a list of the names of the repositories that are part of the .NET
Foundation.
1. In Reposit ory.cs, replace the file contents with the following C#.
C#
This code:
Changes the name of the name property to Name.
Adds the JsonPropertyNameAttribute  to specify how this property appears in
the JSON.
2. In Program.cs , update the code to use the new capitalization of the Name property:
C#
3. Run the app.
The output is the same.
The ProcessRepositoriesAsync method can do the async work and return a collection of
the repositories. Change that method to return Task<List<Repository>>, and move the
code that writes to the console near its caller.
1. Change the signature of ProcessRepositoriesAsync to return a task whose result is
a list of Repository objects:
C#Configure deserialization
using System.Text.Json.Serialization;
public record class Repository (
    [property: JsonPropertyName( "name")] string Name);
foreach (var repo in repositories)
   Console.Write(repo.Name);
Refactor the code
static async Task<List<Repository>> ProcessRepositoriesAsync(HttpClient  2. Return the repositories after processing the JSON response:
C#
The compiler generates the Task<T> object for the return value because you've
marked this method as async.
3. Modify the Program.cs  file, replacing the call to ProcessRepositoriesAsync with the
following to capture the results and write each repository name to the console.
C#
4. Run the app.
The output is the same.
The following steps add code to process more of the properties in the received JSON
packet. Y ou probably won't want to process every property, but adding a few more
demonstrates other features of C#.
1. Replace the contents of Repository class, with the following record definition:
C#client)
await using Stream stream =
    await 
client.GetStreamAsync( "https://api.github.com/orgs/dotnet/repos" );
var repositories =
    await JsonSerializer.DeserializeAsync<List<Repository>>(stream);
return repositories ?? new();
var repositories = await ProcessRepositoriesAsync(client);
foreach (var repo in repositories)
    Console.Write(repo.Name);
Deserialize more properties
using System.Text.Json.Serialization;
public record class Repository (
    [property: JsonPropertyName( "name")] string Name,
    [property: JsonPropertyName ("description" )] string Description,
    [property: JsonPropertyName ("html_url" )] Uri GitHubHomeUrl,The Uri and int types have built-in functionality to convert to and from string
representation. No extra code is needed to deserialize from JSON string format to
those target types. If the JSON packet contains data that doesn't convert to a
target type, the serialization action throws an exception.
2. Update the foreach loop in the Program.cs  file to display the property values:
C#
3. Run the app.
The list now includes the additional properties.
The date of the last push operation is formatted in this fashion in the JSON response:
JSON
This format is for Coordinated Universal Time (UT C), so the result of deserialization is a
DateTime  value whose Kind property is Utc.
To get a date and time represented in your time zone, you have to write a custom
conversion method.
1. In Reposit ory.cs, add a property for the UT C representation of the date and time
and a readonly LastPush property that returns the date converted to local time,
the file should look like the following:
C#    [property: JsonPropertyName ("homepage" )] Uri Homepage,
    [property: JsonPropertyName ("watchers" )] int Watchers) ;
foreach (var repo in repositories)
{
    Console.WriteLine( $"Name: {repo.Name} ");
    Console.WriteLine( $"Homepage: {repo.Homepage} ");
    Console.WriteLine( $"GitHub: {repo.GitHubHomeUrl} ");
    Console.WriteLine( $"Description: {repo.Description} ");
    Console.WriteLine( $"Watchers: {repo.Watchers:#, 0}");
    Console.WriteLine();
}
Add a date property
2016-02-08T21:27:00ZThe LastPush property is defined using an expression-bodied member  for the get
accessor. There's no set accessor. Omitting the set accessor is one way to define
a read-only  property in C#. (Y es, you can create write-only  properties in C#, but
their value is limited.)
2. Add another output statement in Program.cs : again:
C#
3. The complete app should resemble the following Program.cs  file:
C#using System.Text.Json.Serialization;
public record class Repository (
    [property: JsonPropertyName( "name")] string Name,
    [property: JsonPropertyName ("description" )] string Description,
    [property: JsonPropertyName ("html_url" )] Uri GitHubHomeUrl,
    [property: JsonPropertyName ("homepage" )] Uri Homepage,
    [property: JsonPropertyName ("watchers" )] int Watchers,
    [property: JsonPropertyName ("pushed_at" )] DateTime LastPushUtc)
{
    public DateTime LastPush => LastPushUtc.ToLocalTime();
}
Console.WriteLine( $"Last push: {repo.LastPush} ");
using System.Net.Http.Headers;
using System.Text.Json;
using HttpClient client = new();
client.DefaultRequestHeaders.Accept.Clear();
client.DefaultRequestHeaders.Accept.Add(
    new 
MediaTypeWithQualityHeaderValue( "application/vnd.github.v3+json" ));
client.DefaultRequestHeaders.Add( "User-Agent" , ".NET Foundation  
Repository Reporter" );
var repositories = await ProcessRepositoriesAsync(client);
foreach (var repo in repositories)
{
    Console.WriteLine( $"Name: {repo.Name} ");
    Console.WriteLine( $"Homepage: {repo.Homepage} ");
    Console.WriteLine( $"GitHub: {repo.GitHubHomeUrl} ");
    Console.WriteLine( $"Description: {repo.Description} ");
    Console.WriteLine( $"Watchers: {repo.Watchers:#, 0}");
    Console.WriteLine( $"{repo.LastPush} ");4. Run the app.
The output includes the date and time of the last push to each repository.
In this tutorial, you created an app that makes web requests and parses the results. Y our
version of the app should now match the finished sample .
Learn more about how to configure JSON serialization in How to serialize and
deserialize (marshal and unmarshal) JSON in .NET .    Console.WriteLine();
}
static async Task<List<Repository>> ProcessRepositoriesAsync(HttpClient  
client)
{
    await using Stream stream =
        await 
client.GetStreamAsync( "https://api.github.com/orgs/dotnet/repos" );
    var repositories =
        await JsonSerializer.DeserializeAsync<List<Repository>>
(stream);
    return repositories ?? new();
}
Next stepsWork with Language-Integrated Query
(LINQ)
Article •09/15/2021
This tutorial teaches you features in .NET Core and the C# language. Y ou’ll learn how to:
Generate sequences with LINQ.
Write methods that can be easily used in LINQ queries.
Distinguish between eager and lazy evaluation.
You'll learn these techniques by building an application that demonstrates one of the
basic skills of any magician: the faro shuffle . Briefly, a faro shuffle is a technique where
you split a card deck exactly in half, then the shuffle interleaves each one card from each
half to rebuild the original deck.
Magicians use this technique because every card is in a known location after each
shuffle, and the order is a repeating pattern.
For your purposes, it is a light hearted look at manipulating sequences of data. The
application you'll build constructs a card deck and then performs a sequence of shuffles,
writing the sequence out each time. Y ou'll also compare the updated order to the
original order.
This tutorial has multiple steps. After each step, you can run the application and see the
progress. Y ou can also see the completed sample  in the dotnet/samples GitHub
repository. For download instructions, see Samples and Tutorials .
You’ll need to set up your machine to run .NET core. Y ou can find the installation
instructions on the .NET Core Download  page. Y ou can run this application on
Windows, Ubuntu Linux, or OS X, or in a Docker container. Y ou’ll need to install your
favorite code editor. The descriptions below use Visual S tudio Code  which is an open
source, cross-platform editor. However, you can use whatever tools you are comfortable
with.Introduction
Prerequisites
Create the ApplicationThe first step is to create a new application. Open a command prompt and create a new
directory for your application. Make that the current directory. T ype the command
dotnet new console at the command prompt. This creates the starter files for a basic
"Hello W orld" application.
If you've never used C# before, this tutorial  explains the structure of a C# program. Y ou
can read that and then return here to learn more about LINQ.
Before you begin, make sure that the following lines are at the top of the Program.cs file
generated by dotnet new console:
C#
If these three lines ( using statements) aren't at the top of the file, our program will not
compile.
Now that you have all of the references that you'll need, consider what constitutes a
deck of cards. Commonly, a deck of playing cards has four suits, and each suit has
thirteen values. Normally, you might consider creating a Card class right off the bat and
populating a collection of Card objects by hand. With LINQ, you can be more concise
than the usual way of dealing with creating a deck of cards. Instead of creating a Card
class, you can create two sequences to represent suits and ranks, respectively. Y ou'll
create a really simple pair of iterator methods  that will generate the ranks and suits as
IEnumerable<T> s of strings:
C#Create the Data Set
// Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
// Program.cs
// The Main() method
static IEnumerable< string> Suits()
{
    yield return "clubs";
    yield return "diamonds" ;
    yield return "hearts" ;
    yield return "spades" ;
}Place these underneath the Main method in your Program.cs file. These two methods
both utilize the yield return syntax to produce a sequence as they run. The compiler
builds an object that implements IEnumerable<T>  and generates the sequence of
strings as they are requested.
Now, use these iterator methods to create the deck of cards. Y ou'll place the LINQ query
in our Main method. Here's a look at it:
C#
The multiple from clauses produce a SelectMany , which creates a single sequence from
combining each element in the first sequence with each element in the second
sequence. The order is important for our purposes. The first element in the first source
sequence (Suits) is combined with every element in the second sequence (Ranks). This
produces all thirteen cards of first suit. That process is repeated with each element in thestatic IEnumerable< string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
// Program.cs
static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };
    // Display each card that we've generated and placed in startingDeck in  
the console
    foreach (var card in startingDeck)
    {
        Console.WriteLine(card);
    }
}first sequence (Suits). The end result is a deck of cards ordered by suits, followed by
values.
It's important to keep in mind that whether you choose to write your LINQ in the query
syntax used above or use method syntax instead, it's always possible to go from one
form of syntax to the other. The above query written in query syntax can be written in
method syntax as:
C#
The compiler translates LINQ statements written with query syntax into the equivalent
method call syntax. Therefore, regardless of your syntax choice, the two versions of the
query produce the same result. Choose which syntax works best for your situation: for
instance, if you're working in a team where some of the members have difficulty with
method syntax, try to prefer using query syntax.
Go ahead and run the sample you've built at this point. It will display all 52 cards in the
deck. Y ou may find it very helpful to run this sample under a debugger to observe how
the Suits() and Ranks() methods execute. Y ou can clearly see that each string in each
sequence is generated only as it is needed.
var startingDeck = Suits().SelectMany(suit => Ranks().Select(rank => new { 
Suit = suit, Rank = rank }));
Manipulate the OrderNext, focus on how you're going to shuffle the cards in the deck. The first step in any
good shuffle is to split the deck in two. The Take and Skip methods that are part of the
LINQ APIs provide that feature for you. Place them underneath the foreach loop:
C#
However, there's no shuffle method to take advantage of in the standard library, so
you'll have to write your own. The shuffle method you'll be creating illustrates several
techniques that you'll use with LINQ-based programs, so each part of this process will
be explained in steps.
In order to add some functionality to how you interact with the IEnumerable<T>  you'll
get back from LINQ queries, you'll need to write some special kinds of methods called
extension methods . Briefly, an extension method is a special purpose static method  that
adds new functionality to an already-existing type without having to modify the original
type you want to add functionality to.
Give your extension methods a new home by adding a new static class file to your
program called Extensions.cs, and then start building out the first extension method:
C#// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };
    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
    // 52 cards in a deck, so 52 / 2 = 26
    var top = startingDeck.Take( 26);
    var bottom = startingDeck.Skip( 26);
}
// Extensions.cs
using System;
using System.Collections.Generic;
using System.Linq;
namespace  LinqFaroShuffle
{
    public static class Extensions
    {Look at the method signature for a moment, specifically the parameters:
C#
You can see the addition of the this modifier on the first argument to the method. That
means you call the method as though it were a member method of the type of the first
argument. This method declaration also follows a standard idiom where the input and
output types are IEnumerable<T>. That practice enables LINQ methods to be chained
together to perform more complex queries.
Naturally, since you split the deck into halves, you'll need to join those halves together.
In code, this means you'll be enumerating both of the sequences you acquired through
Take and Skip at once, interleaving the elements, and creating one sequence: your
now-shuffled deck of cards. Writing a LINQ method that works with two sequences
requires that you understand how IEnumerable<T>  works.
The IEnumerable<T>  interface has one method: GetEnumerator . The object returned by
GetEnumerator  has a method to move to the next element, and a property that retrieves
the current element in the sequence. Y ou will use those two members to enumerate the
collection and return the elements. This Interleave method will be an iterator method, so
instead of building a collection and returning the collection, you'll use the yield return
syntax shown above.
Here's the implementation of that method:
C#        public static IEnumerable<T> InterleaveSequenceWith<T>( this 
IEnumerable<T> first, IEnumerable<T> second)
        {
            // Your implementation will go here soon enough
        }
    }
}
public static IEnumerable<T> InterleaveSequenceWith<T> ( this IEnumerable<T>  
first, IEnumerable<T> second)
public static IEnumerable<T> InterleaveSequenceWith<T>
    (this IEnumerable<T> first, IEnumerable<T> second)
{
    var firstIter = first.GetEnumerator();
    var secondIter = second.GetEnumerator();
    while (firstIter.MoveNext() && secondIter.MoveNext())
    {Now that you've written this method, go back to the Main method and shuffle the deck
once:
C#
How many shuffles it takes to set the deck back to its original order? T o find out, you'll
need to write a method that determines if two sequences are equal. After you have that
method, you'll need to place the code that shuffles the deck in a loop, and check to see
when the deck is back in order.
Writing a method to determine if the two sequences are equal should be
straightforward. It's a similar structure to the method you wrote to shuffle the deck. Only
this time, instead of yield returning each element, you'll compare the matching
elements of each sequence. When the entire sequence has been enumerated, if every
element matches, the sequences are the same:
C#        yield return firstIter.Current;
        yield return secondIter.Current;
    }
}
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };
    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
    var top = startingDeck.Take( 26);
    var bottom = startingDeck.Skip( 26);
    var shuffle = top.InterleaveSequenceWith(bottom);
    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
ComparisonsThis shows a second LINQ idiom: terminal methods. They take a sequence as input (or in
this case, two sequences), and return a single scalar value. When using terminal
methods, they are always the final method in a chain of methods for a LINQ query,
hence the name "terminal".
You can see this in action when you use it to determine when the deck is back in its
original order. Put the shuffle code inside a loop, and stop when the sequence is back in
its original order by applying the SequenceEquals() method. Y ou can see it would always
be the final method in any query, because it returns a single value instead of a
sequence:
C#public static bool SequenceEquals<T>
    (this IEnumerable<T> first, IEnumerable<T> second)
{
    var firstIter = first.GetEnumerator();
    var secondIter = second.GetEnumerator();
    while ((firstIter?.MoveNext() == true) && secondIter.MoveNext())
    {
        if ((firstIter.Current is not null) && 
!firstIter.Current.Equals(secondIter.Current))
        {
            return false;
        }
    }
    return true;
}
// Program.cs
static void Main(string[] args)
{
    // Query for building the deck
    // Shuffling using InterleaveSequenceWith<T>();
    var times = 0;
    // We can re-use the shuffle variable from earlier, or you can make a  
new one
    shuffle = startingDeck;
    do
    {
        shuffle = shuffle.Take( 26).InterleaveSequenceWith(shuffle.Skip( 26));
        foreach (var card in shuffle)
        {
            Console.WriteLine(card);
        }Run the code you've got so far and take note of how the deck rearranges on each
shuffle. After 8 shuffles (iterations of the do-while loop), the deck returns to the original
configuration it was in when you first created it from the starting LINQ query.
The sample you've built so far executes an out shuf fle, where the top and bottom cards
stay the same on each run. Let's make one change: we'll use an in shuf fle instead, where
all 52 cards change position. For an in shuffle, you interleave the deck so that the first
card in the bottom half becomes the first card in the deck. That means the last card in
the top half becomes the bottom card. This is a simple change to a singular line of code.
Update the current shuffle query by switching the positions of Take and Skip. This will
change the order of the top and bottom halves of the deck:
C#
Run the program again, and you'll see that it takes 52 iterations for the deck to reorder
itself. Y ou'll also start to notice some serious performance degradations as the program
continues to run.
There are a number of reasons for this. Y ou can tackle one of the major causes of this
performance drop: inefficient use of lazy ev aluation .
Briefly, lazy evaluation states that the evaluation of a statement is not performed until its
value is needed. LINQ queries are statements that are evaluated lazily. The sequences
are generated only as the elements are requested. Usually, that's a major benefit of
LINQ. However, in a use such as this program, this causes exponential growth in
execution time.
Remember that we generated the original deck using a LINQ query. Each shuffle is
generated by performing three LINQ queries on the previous deck. All these are
performed lazily. That also means they are performed again each time the sequence is        Console.WriteLine();
        times++;
    } while (!startingDeck.SequenceEquals(shuffle));
    Console.WriteLine(times);
}
Optimizations
shuffle = shuffle.Skip( 26).InterleaveSequenceWith(shuffle.Take( 26));requested. By the time you get to the 52nd iteration, you're regenerating the original
deck many, many times. Let's write a log to demonstrate this behavior. Then, you'll fix it.
In your Extensions.cs file, type in or copy the method below. This extension method
creates a new file called debug.log within your project directory and records what query
is currently being executed to the log file. This extension method can be appended to
any query to mark that the query executed.
C#
You will see a red squiggle under File, meaning it doesn't exist. It won't compile, since
the compiler doesn't know what File is. To solve this problem, make sure to add the
following line of code under the very first line in Extensions.cs:
C#
This should solve the issue and the red error disappears.
Next, instrument the definition of each query with a log message:
C#public static IEnumerable<T> LogQuery<T>
    (this IEnumerable<T> sequence, string tag)
{
    // File.AppendText creates a new file if the file doesn't exist.
    using (var writer = File.AppendText( "debug.log" ))
    {
        writer.WriteLine( $"Executing Query {tag}");
    }
    return sequence;
}
using System.IO;
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = ( from s in Suits().LogQuery ("Suit Generation" )
                        from r in Ranks().LogQuery ("Rank Generation" )
                        select new { Suit = s, Rank = r  
}).LogQuery( "Starting Deck" );
    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }Notice that you don't log every time you access a query. Y ou log only when you create
the original query. The program still takes a long time to run, but now you can see why.
If you run out of patience running the in shuffle with logging turned on, switch back to
the out shuffle. Y ou'll still see the lazy evaluation effects. In one run, it executes 2592
queries, including all the value and suit generation.
You can improve the performance of the code here to reduce the number of executions
you make. A simple fix you can make is to cache  the results of the original LINQ query
that constructs the deck of cards. Currently, you're executing the queries again and
again every time the do-while loop goes through an iteration, re-constructing the deck
of cards and reshuffling it every time. T o cache the deck of cards, you can leverage the
LINQ methods ToArray  and ToList ; when you append them to the queries, they'll
perform the same actions you've told them to, but now they'll store the results in an
array or a list, depending on which method you choose to call. Append the LINQ
method ToArray  to both queries and run the program again:    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;
    do
    {
        // Out shuffle
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */
        // In shuffle
        shuffle = shuffle.Skip( 26).LogQuery( "Bottom Half" )
                .InterleaveSequenceWith(shuffle.Take( 26).LogQuery( "Top 
Half"))
                .LogQuery( "Shuffle" );
        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }
        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));
    Console.WriteLine(times);
}C#
public static void Main(string[] args)
{
    IEnumerable<Suit>? suits = Suits();
    IEnumerable<Rank>? ranks = Ranks();
    if ((suits is null) || (ranks is null))
        return;
    var startingDeck = ( from s in suits.LogQuery( "Suit Generation" )
                        from r in ranks.LogQuery( "Value Generation" )
                        select new { Suit = s, Rank = r })
                        .LogQuery( "Starting Deck" )
                        .ToArray();
    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;
    do
    {
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26).LogQuery("Bottom  
Half"))
            .LogQuery("Shuffle")
            .ToArray();
        */
        shuffle = shuffle.Skip( 26)
            .LogQuery( "Bottom Half" )
            .InterleaveSequenceWith(shuffle.Take( 26).LogQuery( "Top Half" ))
            .LogQuery( "Shuffle" )
            .ToArray();
        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }
        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));Now the out shuffle is down to 30 queries. Run again with the in shuffle and you'll see
similar improvements: it now executes 162 queries.
Please note that this example is designed  to highlight the use cases where lazy
evaluation can cause performance difficulties. While it's important to see where lazy
evaluation can impact code performance, it's equally important to understand that not
all queries should run eagerly. The performance hit you incur without using ToArray  is
because each new arrangement of the deck of cards is built from the previous
arrangement. Using lazy evaluation means each new deck configuration is built from the
original deck, even executing the code that built the startingDeck. That causes a large
amount of extra work.
In practice, some algorithms run well using eager evaluation, and others run well using
lazy evaluation. For daily usage, lazy evaluation is usually a better choice when the data
source is a separate process, like a database engine. For databases, lazy evaluation
allows more complex queries to execute only one round trip to the database process
and back to the rest of your code. LINQ is flexible whether you choose to utilize lazy or
eager evaluation, so measure your processes and pick whichever kind of evaluation
gives you the best performance.
In this project, you covered:
using LINQ queries to aggregate data into a meaningful sequence
writing Extension methods to add our own custom functionality to LINQ queries
locating areas in our code where our LINQ queries might run into performance
issues like degraded speed
lazy and eager evaluation in regards to LINQ queries and the implications they
might have on query performance
Aside from LINQ, you learned a bit about a technique magicians use for card tricks.
Magicians use the F aro shuffle because they can control where every card moves in the
deck. Now that you know, don't spoil it for everyone else!
For more information on LINQ, see:
Introduction to LINQ
Basic LINQ Query Operations (C#)
Data T ransformations With LINQ (C#)    Console.WriteLine(times);
}
ConclusionQuery S yntax and Method S yntax in LINQ (C#)
C# Features That Support LINQLanguage Integrated Query (LINQ)
Article •07/18/2023
Language-Integrated Query (LINQ) is the name for a set of technologies based on the
integration of query capabilities directly into the C# language. T raditionally, queries
against data are expressed as simple strings without type checking at compile time or
IntelliSense support. Furthermore, you have to learn a different query language for each
type of data source: SQL databases, XML documents, various W eb services, and so on.
With LINQ, a query is a first-class language construct, just like classes, methods, events.
For a developer who writes queries, the most visible "language-integrated" part of LINQ
is the query expression. Query expressions are written in a declarative query syntax. By
using query syntax, you can perform filtering, ordering, and grouping operations on
data sources with a minimum of code. Y ou use the same basic query expression patterns
to query and transform data in SQL databases, ADO.NET Datasets, XML documents and
streams, and .NET collections.
The following example shows the complete query operation. The complete operation
includes creating a data source, defining the query expression, and executing the query
in a foreach statement.
C#
Query expressions can be used to query and to transform data from any LINQ-
enabled data source. For example, a single query can retrieve data from a SQL// Specify the data source.
int[] scores = { 97, 92, 81, 60 };
// Define the query expression.
IEnumerable< int> scoreQuery =
    from score in scores
    where score > 80
    select score;
// Execute the query.
foreach (int i in scoreQuery)
{
    Console.Write(i + " ");
}
// Output: 97 92 81
Query expression overviewdatabase, and produce an XML stream as output.
Query expressions are easy to grasp because they use many familiar C# language
constructs.
The variables in a query expression are all strongly typed, although in many cases
you do not have to provide the type explicitly because the compiler can infer it. For
more information, see Type relationships in LINQ query operations .
A query is not executed until you iterate over the query variable, for example, in a
foreach statement. For more information, see Introduction to LINQ queries .
At compile time, query expressions are converted to S tandard Query Operator
method calls according to the rules set forth in the C# specification. Any query that
can be expressed by using query syntax can also be expressed by using method
syntax. However, in most cases query syntax is more readable and concise. For
more information, see C# language specification  and Standard query operators
overview .
As a rule when you write LINQ queries, we recommend that you use query syntax
whenever possible and method syntax whenever necessary. There is no semantic
or performance difference between the two different forms. Query expressions are
often more readable than equivalent expressions written in method syntax.
Some query operations, such as Count  or Max, have no equivalent query
expression clause and must therefore be expressed as a method call. Method
syntax can be combined with query syntax in various ways. For more information,
see Query syntax and method syntax in LINQ .
Query expressions can be compiled to expression trees or to delegates, depending
on the type that the query is applied to. IEnumerable<T>  queries are compiled to
delegates. IQueryable  and IQueryable<T>  queries are compiled to expression
trees. For more information, see Expression trees .
There are two ways you can enable LINQ querying of in-memory data. If the data is of a
type that implements IEnumerable<T> , you can query the data by using LINQ to
Objects. If it does not make sense to enable enumeration of your type by implementingHow to enable LINQ querying of your data
source
In-memory datathe IEnumerable<T>  interface, you can define LINQ standard query operator methods in
that type or create LINQ standard query operator methods that extend the type. Custom
implementations of the standard query operators should use deferred execution to
return the results.
The best option for enabling LINQ querying of a remote data source is to implement the
IQueryable<T>  interface. However, this differs from extending a provider such as LINQ
to SQL for a data source.
LINQ providers that implement IQueryable<T>  can vary widely in their complexity.
A less complex IQueryable provider might interface with a single method of a W eb
service. This type of provider is very specific because it expects specific information in
the queries that it handles. It has a closed type system, perhaps exposing a single result
type. Most of the execution of the query occurs locally, for example by using the
Enumerable  implementations of the standard query operators. A less complex provider
might examine only one method call expression in the expression tree that represents
the query, and let the remaining logic of the query be handled elsewhere.
An IQueryable provider of medium complexity might target a data source that has a
partially expressive query language. If it targets a W eb service, it might interface with
more than one method of the W eb service and select the method to call based on the
question that the query poses. A provider of medium complexity would have a richer
type system than a simple provider, but it would still be a fixed type system. For
example, the provider might expose types that have one-to-many relationships that can
be traversed, but it would not provide mapping technology for user-defined types.
A complex IQueryable provider, such as the LINQ to SQL provider, might translate
complete LINQ queries to an expressive query language, such as SQL. A complex
provider is more general than a less complex provider, because it can handle a wider
variety of questions in the query. It also has an open type system and therefore must
contain extensive infrastructure to map user-defined types. Developing a complex
provider requires a significant amount of effort.Remote data
IQueryable LINQ providersIntroduction to LINQ Queries (C#)
Article •09/15/2021
A query is an expression that retrieves data from a data source. Queries are usually
expressed in a specialized query language. Different languages have been developed
over time for the various types of data sources, for example SQL for relational databases
and XQuery for XML. Therefore, developers have had to learn a new query language for
each type of data source or data format that they must support. LINQ simplifies this
situation by offering a consistent model for working with data across various kinds of
data sources and formats. In a LINQ query, you are always working with objects. Y ou use
the same basic coding patterns to query and transform data in XML documents, SQL
databases, ADO.NET Datasets, .NET collections, and any other format for which a LINQ
provider is available.
All LINQ query operations consist of three distinct actions:
1. Obtain the data source.
2. Create the query.
3. Execute the query.
The following example shows how the three parts of a query operation are expressed in
source code. The example uses an integer array as a data source for convenience;
however, the same concepts apply to other data sources also. This example is referred
to throughout the rest of this topic.
C#Three Parts of a Query Operation
class IntroToLINQ
{
    static void Main()
    {
        // The Three Parts of a LINQ Query:
        // 1. Data source.
        int[] numbers = new int[7] { 0, 1, 2, 3, 4, 5, 6 };
        // 2. Query creation.
        // numQuery is an IEnumerable<int>
        var numQuery =
            from num in numbers
            where (num % 2) == 0
            select num;The following illustration shows the complete query operation. In LINQ, the execution of
the query is distinct from the query itself. In other words, you have not retrieved any
data just by creating a query variable.
In the previous example, because the data source is an array, it implicitly supports the
generic IEnumerable<T>  interface. This fact means it can be queried with LINQ. A query
is executed in a foreach statement, and foreach requires IEnumerable  or
IEnumerable<T> . Types that support IEnumerable<T>  or a derived interface such as the
generic IQueryable<T>  are called queryable types .
A queryable type requires no modification or special treatment to serve as a LINQ data
source. If the source data is not already in memory as a queryable type, the LINQ
provider must represent it as such. For example, LINQ to XML loads an XML document
into a queryable XElement  type:
C#        // 3. Query execution.
        foreach (int num in numQuery)
        {
            Console.Write( "{0,1} " , num);
        }
    }
}
The Data SourceWith LINQ to SQL, you first create an object-relational mapping at design time either
manually or by using the LINQ to SQL T ools in Visual S tudio . You write your queries
against the objects, and at run-time LINQ to SQL handles the communication with the
database. In the following example, Customers represents a specific table in the
database, and the type of the query result, IQueryable<T> , derives from
IEnumerable<T> .
C#
For more information about how to create specific types of data sources, see the
documentation for the various LINQ providers. However, the basic rule is very simple: a
LINQ data source is any object that supports the generic IEnumerable<T>  interface, or
an interface that inherits from it.
The query specifies what information to retrieve from the data source or sources.
Optionally, a query also specifies how that information should be sorted, grouped, and
shaped before it is returned. A query is stored in a query variable and initialized with a
query expression. T o make it easier to write queries, C# has introduced new query
syntax.// Create a data source from an XML document.
// using System.Xml.Linq;
XElement contacts = XElement.Load( @"c:\myContactList.xml" );
Northwnd db = new Northwnd( @"c:\northwnd.mdf" );
// Query for customers in London.
IQueryable<Customer> custQuery =
    from cust in db.Customers
    where cust.City == "London"
    select cust;
７ Note
Types such as ArrayList  that support the non-generic IEnumerable  interface can
also be used as a LINQ data source. For more information, see How t o quer y an
ArrayList with LINQ (C#) .
The QueryThe query in the previous example returns all the even numbers from the integer array.
The query expression contains three clauses: from, where and select. (If you are
familiar with SQL, you will have noticed that the ordering of the clauses is reversed from
the order in SQL.) The from clause specifies the data source, the where clause applies
the filter, and the select clause specifies the type of the returned elements. These and
the other query clauses are discussed in detail in the Language Integrated Query (LINQ)
section. For now, the important point is that in LINQ, the query variable itself takes no
action and returns no data. It just stores the information that is required to produce the
results when the query is executed at some later point. For more information about how
queries are constructed behind the scenes, see Standard Query Operators Overview
(C#).
As stated previously, the query variable itself only stores the query commands. The
actual execution of the query is deferred until you iterate over the query variable in a
foreach statement. This concept is referred to as deferr ed ex ecution  and is
demonstrated in the following example:
C#
The foreach statement is also where the query results are retrieved. For example, in the
previous query, the iteration variable num holds each value (one at a time) in the
returned sequence.
Because the query variable itself never holds the query results, you can execute it as
often as you like. For example, you may have a database that is being updated７ Note
Queries can also be expressed by using method syntax. For more information, see
Quer y Syntax and Method S yntax in LINQ .
Query Execution
Deferred Execution
//  Query execution.
foreach (int num in numQuery)
{
    Console.Write( "{0,1} " , num);
}continually by a separate application. In your application, you could create one query
that retrieves the latest data, and you could execute it repeatedly at some interval to
retrieve different results every time.
Queries that perform aggregation functions over a range of source elements must first
iterate over those elements. Examples of such queries are Count, Max, Average, and
First. These execute without an explicit foreach statement because the query itself
must use foreach in order to return a result. Note also that these types of queries return
a single value, not an IEnumerable collection. The following query returns a count of the
even numbers in the source array:
C#
To force immediate execution of any query and cache its results, you can call the ToList
or ToArray  methods.
C#
You can also force execution by putting the foreach loop immediately after the query
expression. However, by calling ToList or ToArray you also cache all the data in a single
collection object.Forcing Immediate Execution
var evenNumQuery =
    from num in numbers
    where (num % 2) == 0
    select num;
int evenNumCount = evenNumQuery.Count();
List<int> numQuery2 =
    (from num in numbers
     where (num % 2) == 0
     select num).ToList();
// or like this:
// numQuery3 is still an int[]
var numQuery3 =
    (from num in numbers
     where (num % 2) == 0
     select num).ToArray();Getting S tarted with LINQ in C#
Walkthrough: Writing Queries in C#
Language Integrated Query (LINQ)
foreach, in
Query K eywords (LINQ)See alsoQuery expression basics
Article •09/21/2022
This article introduces the basic concepts related to query expressions in C#.
A query is a set of instructions that describes what data to retrieve from a given data
source (or sources) and what shape and organization the returned data should have. A
query is distinct from the results that it produces.
Generally, the source data is organized logically as a sequence of elements of the same
kind. For example, a SQL database table contains a sequence of rows. In an XML file,
there is a "sequence" of XML elements (although these are organized hierarchically in a
tree structure). An in-memory collection contains a sequence of objects.
From an application's viewpoint, the specific type and structure of the original source
data is not important. The application always sees the source data as an
IEnumerable<T>  or IQueryable<T>  collection. For example, in LINQ to XML, the source
data is made visible as an IEnumerable<XElement >.
Given this source sequence, a query may do one of three things:
Retrieve a subset of the elements to produce a new sequence without modifying
the individual elements. The query may then sort or group the returned sequence
in various ways, as shown in the following example (assume scores is an int[]):
C#
Retrieve a sequence of elements as in the previous example but transform them to
a new type of object. For example, a query may retrieve only the last names from
certain customer records in a data source. Or it may retrieve the complete record
and then use it to construct another in-memory object type or even XML data
before generating the final result sequence. The following example shows a
projection from an int to a string. Note the new type of highScoresQuery.What is a query and what does it do?
IEnumerable< int> highScoresQuery =
    from score in scores
    where score > 80
    orderby score descending
    select score;C#
Retrieve a singleton value about the source data, such as:
The number of elements that match a certain condition.
The element that has the greatest or least value.
The first element that matches a condition, or the sum of particular values in a
specified set of elements. For example, the following query returns the number
of scores greater than 80 from the scores integer array:
C#
In the previous example, note the use of parentheses around the query
expression before the call to the Count method. Y ou can also express this by
using a new variable to store the concrete result. This technique is more
readable because it keeps the variable that stores the query separate from the
query that stores a result.
C#
In the previous example, the query is executed in the call to Count, because Count must
iterate over the results in order to determine the number of elements returned by
highScoresQuery.IEnumerable< string> highScoresQuery2 =
    from score in scores
    where score > 80
    orderby score descending
    select $"The score is {score}";
int highScoreCount = (
    from score in scores
    where score > 80
    select score
).Count();
IEnumerable< int> highScoresQuery3 =
    from score in scores
    where score > 80
    select score;
int scoreCount = highScoresQuery3.Count();A query expr ession  is a query expressed in query syntax. A query expression is a first-
class language construct. It is just like any other expression and can be used in any
context in which a C# expression is valid. A query expression consists of a set of clauses
written in a declarative syntax similar to SQL or XQuery. Each clause in turn contains one
or more C# expressions, and these expressions may themselves be either a query
expression or contain a query expression.
A query expression must begin with a from  clause and must end with a select  or group
clause. Between the first from clause and the last select or group clause, it can contain
one or more of these optional clauses: where , orderby , join, let and even additional from
clauses. Y ou can also use the into keyword to enable the result of a join or group
clause to serve as the source for additional query clauses in the same query expression.
In LINQ, a query variable is any variable that stores a query instead of the results  of a
query. More specifically, a query variable is always an enumerable type that will produce
a sequence of elements when it is iterated over in a foreach statement or a direct call to
its IEnumerator.MoveNext method.
The following code example shows a simple query expression with one data source, one
filtering clause, one ordering clause, and no transformation of the source elements. The
select clause ends the query.
C#What is a query expression?
Query variable
// Data source.
int[] scores = { 90, 71, 82, 93, 75, 82 };
// Query Expression.
IEnumerable< int> scoreQuery = //query variable
    from score in scores //required
    where score > 80 // optional
    orderby score descending  // optional
    select score; //must end with select or group
// Execute the query to produce the results
foreach (int testScore in scoreQuery)
{
    Console.WriteLine(testScore);
}
// Output: 93 90 82 82In the previous example, scoreQuery is a query variable,  which is sometimes referred to
as just a query. The query variable stores no actual result data, which is produced in the
foreach loop. And when the foreach statement executes, the query results are not
returned through the query variable scoreQuery. Rather, they are returned through the
iteration variable testScore. The scoreQuery variable can be iterated in a second
foreach loop. It will produce the same results as long as neither it nor the data source
has been modified.
A query variable may store a query that is expressed in query syntax or method syntax,
or a combination of the two. In the following examples, both queryMajorCities and
queryMajorCities2 are query variables:
C#
On the other hand, the following two examples show variables that are not query
variables even though each is initialized with a query. They are not query variables
because they store results:
C#
C#//Query syntax
IEnumerable<City> queryMajorCities =
    from city in cities
    where city.Population > 100000
    select city;
// Method-based syntax
IEnumerable<City> queryMajorCities2 = cities.Where(c => c.Population > 
100000);
int highestScore = (
    from score in scores
    select score
).Max();
// or split the expression
IEnumerable< int> scoreQuery =
    from score in scores
    select score;
int highScore = scoreQuery.Max();
// the following returns the same result
highScore = scores.Max();For more information about the different ways to express queries, see Query syntax and
method syntax in LINQ .
This documentation usually provides the explicit type of the query variable in order to
show the type relationship between the query variable and the select clause . However,
you can also use the var keyword to instruct the compiler to infer the type of a query
variable (or any other local variable) at compile time. For example, the query example
that was shown previously in this topic can also be expressed by using implicit typing:
C#
In the above, the use of var is optional here and in all queries. queryCities is an
IEnumerable<City> just as when it is explicitly typed.
For more information, see Implicitly typed local variables  and Type relationships in LINQ
query operations .
A query expression must begin with a from clause. It specifies a data source together
with a range variable. The range variable represents each successive element in theList<City> largeCitiesList = (
    from country in countries
    from city in country.Cities
    where city.Population > 10000
    select city
).ToList();
// or split the expression
IEnumerable<City> largeCitiesQuery =
    from country in countries
    from city in country.Cities
    where city.Population > 10000
    select city;
List<City> largeCitiesList2 = largeCitiesQuery.ToList();
Explicit and implicit typing of query variables
var queryCities =
    from city in cities
    where city.Population > 100000
    select city;
Starting a query expressionsource sequence as the source sequence is being traversed. The range variable is
strongly typed based on the type of elements in the data source. In the following
example, because countries is an array of Country objects, the range variable is also
typed as Country. Because the range variable is strongly typed, you can use the dot
operator to access any available members of the type.
C#
The range variable is in scope until the query is exited either with a semicolon or with a
continuation  clause.
A query expression may contain multiple from clauses. Use additional from clauses
when each element in the source sequence is itself a collection or contains a collection.
For example, assume that you have a collection of Country objects, each of which
contains a collection of City objects named Cities. To query the City objects in each
Country, use two from clauses as shown here:
C#
For more information, see from clause .
A query expression must end with either a group clause or a select clause.
Use the group clause to produce a sequence of groups organized by a key that you
specify. The key can be any data type. For example, the following query creates a
sequence of groups that contains one or more Country objects and whose key is a char
type with value being the first letter of countries' names.IEnumerable<Country> countryAreaQuery =
    from country in countries
    where country.Area > 500000 //sq km
    select country;
IEnumerable<City> cityQuery =
    from country in countries
    from city in country.Cities
    where city.Population > 10000
    select city;
Ending a query expression
group clauseC#
For more information about grouping, see group clause .
Use the select clause to produce all other types of sequences. A simple select clause
just produces a sequence of the same type of objects as the objects that are contained
in the data source. In this example, the data source contains Country objects. The
orderby clause just sorts the elements into a new order and the select clause produces
a sequence of the reordered Country objects.
C#
The select clause can be used to transform source data into sequences of new types.
This transformation is also named a projection . In the following example, the select
clause projects a sequence of anonymous types which contains only a subset of the
fields in the original element. Note that the new objects are initialized by using an object
initializer.
C#
So in this example, the var is required because the query produces an anonymous type.
For more information about all the ways that a select clause can be used to transform
source data, see select clause .var queryCountryGroups =
    from country in countries
    group country by country.Name[ 0];
select clause
IEnumerable<Country> sortedQuery =
    from country in countries
    orderby country.Area
    select country;
var queryNameAndPop =
    from country in countries
    select new
    {
        Name = country.Name,
        Pop = country.Population
    };You can use the into keyword in a select or group clause to create a temporary
identifier that stores a query. Do this when you must perform additional query
operations on a query after a grouping or select operation. In the following example
countries are grouped according to population in ranges of 10 million. After these
groups are created, additional clauses filter out some groups, and then to sort the
groups in ascending order. T o perform those additional operations, the continuation
represented by countryGroup is required.
C#
For more information, see into.
Between the starting from clause, and the ending select or group clause, all other
clauses ( where, join, orderby, from, let) are optional. Any of the optional clauses may
be used zero times or multiple times in a query body.
Use the where clause to filter out elements from the source data based on one or more
predicate expressions. The where clause in the following example has one predicate with
two conditions.Continuations with i n t o
// percentileQuery is an IEnumerable<IGrouping<int, Country>>
var percentileQuery =
    from country in countries
    let percentile = ( int)country.Population / 10_000_000
    group country by percentile into countryGroup
    where countryGroup.Key >= 20
    orderby countryGroup.Key
    select countryGroup;
// grouping is an IGrouping<int, Country>
foreach (var grouping in percentileQuery)
{
    Console.WriteLine(grouping.Key);
    foreach (var country in grouping)
    {
        Console.WriteLine(country.Name + ":" + country.Population);
    }
}
Filtering, ordering, and joining
where clauseC#
For more information, see where clause .
Use the orderby clause to sort the results in either ascending or descending order. Y ou
can also specify secondary sort orders. The following example performs a primary sort
on the country objects by using the Area property. It then performs a secondary sort by
using the Population property.
C#
The ascending keyword is optional; it is the default sort order if no order is specified. For
more information, see orderby clause .
Use the join clause to associate and/or combine elements from one data source with
elements from another data source based on an equality comparison between specified
keys in each element. In LINQ, join operations are performed on sequences of objects
whose elements are different types. After you have joined two sequences, you must use
a select or group statement to specify which element to store in the output sequence.
You can also use an anonymous type to combine properties from each set of associated
elements into a new type for the output sequence. The following example associates
prod objects whose Category property matches one of the categories in the categories
string array. Products whose Category does not match any string in categories are
filtered out. The select statement projects a new type whose properties are taken from
both cat and prod.
C#IEnumerable<City> queryCityPop =
    from city in cities
    where city.Population < 200000 && city.Population > 100000
    select city;
orderby clause
IEnumerable<Country> querySortedCountries =
    from country in countries
    orderby country.Area, country.Population descending
    select country;
join clauseYou can also perform a group join by storing the results of the join operation into a
temporary variable by using the into keyword. For more information, see join clause .
Use the let clause to store the result of an expression, such as a method call, in a new
range variable. In the following example, the range variable firstName stores the first
element of the array of strings that is returned by Split.
C#
For more information, see let clause .
A query clause may itself contain a query expression, which is sometimes referred to as
a subquer y. Each subquery starts with its own from clause that does not necessarily
point to the same data source in the first from clause. For example, the following query
shows a query expression that is used in the select statement to retrieve the results of a
grouping operation.
C#var categoryQuery =
    from cat in categories
    join prod in products on cat equals prod.Category
    select new
    {
        Category = cat,
        Name = prod.Name
    };
let clause
string[] names = { "Svetlana Omelchenko" , "Claire O'Donnell" , "Sven 
Mortensen" , "Cesar Garcia"  };
IEnumerable< string> queryFirstNames =
    from name in names
    let firstName = name.Split( ' ')[0]
    select firstName;
foreach (string s in queryFirstNames)
{
    Console.Write(s + " ");
}
//Output: Svetlana Claire Sven Cesar
Subqueries in a query expressionFor more information, see Perform a subquery on a grouping operation .
C# programming guide
Language Integrated Query (LINQ)
Query keywords (LINQ)
Standard query operators overviewvar queryGroupMax =
    from student in students
    group student by student.Year into studentGroup
    select new
    {
        Level = studentGroup.Key,
        HighestScore = (
            from student2 in studentGroup
            select student2.ExamScores.Average()
        ).Max()
    };
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
 Provide product feedbackWrite LINQ queries in C#
Article •07/18/2023
Most queries in the introductory Language Integrated Query (LINQ) documentation are
written by using the LINQ declarative query syntax. However, the query syntax must be
translated into method calls for the .NET common language runtime (CLR) when the
code is compiled. These method calls invoke the standard query operators, which have
names such as Where, Select, GroupBy, Join, Max, and Average. You can call them
directly by using method syntax instead of query syntax.
Query syntax and method syntax are semantically identical, but many people find query
syntax simpler and easier to read. Some queries must be expressed as method calls. For
example, you must use a method call to express a query that retrieves the number of
elements that match a specified condition. Y ou also must use a method call for a query
that retrieves the element that has the maximum value in a source sequence. The
reference documentation for the standard query operators in the System.Linq
namespace generally uses method syntax. Therefore, even when getting started writing
LINQ queries, it is useful to be familiar with how to use method syntax in queries and in
query expressions themselves.
The following example shows a simple query expr ession  and the semantically equivalent
query written as a method-b ased quer y.
C#Standard query operator extension methods
class QueryVMethodSyntax
{
    static void Main()
    {
        int[] numbers = { 5, 10, 8, 3, 6, 12};
        //Query syntax:
        IEnumerable< int> numQuery1 =
            from num in numbers
            where num % 2 == 0
            orderby num
            select num;
        //Method syntax:
        IEnumerable< int> numQuery2 = numbers.Where(num => num % 2 == 
0).OrderBy(n => n);
        foreach (int i in numQuery1)The output from the two examples is identical. Y ou can see that the type of the query
variable is the same in both forms: IEnumerable<T> .
To understand the method-based query, let's examine it more closely. On the right side
of the expression, notice that the where clause is now expressed as an instance method
on the numbers object, which as you will recall has a type of IEnumerable<int>. If you are
familiar with the generic IEnumerable<T>  interface, you know that it does not have a
Where method. However, if you invoke the IntelliSense completion list in the Visual
Studio IDE, you will see not only a Where method, but many other methods such as
Select, SelectMany, Join, and Orderby. These are all the standard query operators.
Although it looks as if IEnumerable<T>  has been redefined to include these additional
methods, in fact this is not the case. The standard query operators are implemented as a
new kind of method called extension methods . Extensions methods "extend" an existing
type; they can be called as if they were instance methods on the type. The standard        {
            Console.Write(i + " ");
        }
        Console.WriteLine(System.Environment.NewLine);
        foreach (int i in numQuery2)
        {
            Console.Write(i + " ");
        }
        // Keep the console open in debug mode.
        Console.WriteLine(System.Environment.NewLine);
        Console.WriteLine( "Press any key to exit" );
        Console.ReadKey();
    }
}
/*
    Output:
    6 8 10 12
    6 8 10 12
 */query operators extend IEnumerable<T>  and that is why you can write
numbers.Where(...).
To get started using LINQ, all that you really have to know about extension methods is
how to bring them into scope in your application by using the correct using directives.
From your application's point of view, an extension method and a regular instance
method are the same.
For more information about extension methods, see Extension Methods . For more
information about standard query operators, see Standard Query Operators Overview
(C#). Some LINQ providers, such as LINQ to SQL and LINQ to XML, implement their own
standard query operators and additional extension methods for other types besides
IEnumerable<T> .
In the previous example, notice that the conditional expression ( num % 2 == 0) is passed
as an in-line argument to the Where method: Where(num => num % 2 == 0). This inline
expression is called a lambda expression. It is a convenient way to write code that would
otherwise have to be written in more cumbersome form as an anonymous method or a
generic delegate or an expression tree. In C# => is the lambda operator, which is read as
"goes to". The num on the left of the operator is the input variable which corresponds to
num in the query expression. The compiler can infer the type of num because it knows
that numbers is a generic IEnumerable<T>  type. The body of the lambda is just the same
as the expression in query syntax or in any other C# expression or statement; it can
include method calls and other complex logic. The "return value" is just the expression
result.
To get started using LINQ, you do not have to use lambdas extensively. However, certain
queries can only be expressed in method syntax and some of those require lambda
expressions. After you become more familiar with lambdas, you will find that they are a
powerful and flexible tool in your LINQ toolbox. For more information, see Lambda
Expressions .
In the previous code example, note that the OrderBy method is invoked by using the
dot operator on the call to Where. Where produces a filtered sequence, and then
Orderby operates on that sequence by sorting it. Because queries return an
IEnumerable, you compose them in method syntax by chaining the method callsLambda expressions
Composability of queriestogether. This is what the compiler does behind the scenes when you write queries by
using query syntax. And because a query variable does not store the results of the
query, you can modify it or use it as the basis for a new query at any time, even after it
has been executed.
The following examples demonstrate some simple LINQ queries by using each approach
listed previously. In general, the rule is to use (1) whenever possible, and use (2) and (3)
whenever necessary.
The recommended way to write most queries is to use query syntax to create query
expressions . The following example shows three query expressions. The first query
expression demonstrates how to filter or restrict results by applying conditions with a
where clause. It returns all elements in the source sequence whose values are greater
than 7 or less than 3. The second expression demonstrates how to order the returned
results. The third expression demonstrates how to group results according to a key. This
query returns two groups based on the first letter of the word.
C#７ Note
These queries operate on simple in-memory collections; however, the basic syntax
is identical to that used in LINQ to Entities and LINQ to XML.
Example - Query syntax
List<int> numbers = new() { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
// The query variables can also be implicitly typed by using var
// Query #1.
IEnumerable< int> filteringQuery =
    from num in numbers
    where num < 3 || num > 7
    select num;
// Query #2.
IEnumerable< int> orderingQuery =
    from num in numbers
    where num < 3 || num > 7
    orderby num ascending
    select num;
// Query #3.
string[] groupingQuery = { "carrots" , "cabbage" , "broccoli" , "beans", Note that the type of the queries is IEnumerable<T> . All of these queries could be
written using var as shown in the following example:
var query = from num in numbers...
In each previous example, the queries do not actually execute until you iterate over the
query variable in a foreach statement or other statement. For more information, see
Introduction to LINQ Queries .
Some query operations must be expressed as a method call. The most common such
methods are those that return singleton numeric values, such as Sum, Max, Min,
Average , and so on. These methods must always be called last in any query because
they represent only a single value and cannot serve as the source for an additional query
operation. The following example shows a method call in a query expression:
C#
If the method has Action or Func parameters, these are provided in the form of a
lambda  expression, as shown in the following example:
C#
In the previous queries, only Query #4 executes immediately. This is because it returns a
single value, and not a generic IEnumerable<T>  collection. The method itself has to use
foreach in order to compute its value."barley"  };
IEnumerable<IGrouping< char, string>> queryFoodGroups =
    from item in groupingQuery
    group item by item[0];
Example - Method syntax
List<int> numbers1 = new() { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
List<int> numbers2 = new() { 15, 14, 11, 13, 19, 18, 16, 17, 12, 10 };
// Query #4.
double average = numbers1.Average();
// Query #5.
IEnumerable< int> concatenationQuery = numbers1.Concat(numbers2);
// Query #6.
IEnumerable< int> largeNumbersQuery = numbers2.Where(c => c > 15);Each of the previous queries can be written by using implicit typing with var, as shown in
the following example:
C#
This example shows how to use method syntax on the results of a query clause. Just
enclose the query expression in parentheses, and then apply the dot operator and call
the method. In the following example, query #7 returns a count of the numbers whose
value is between 3 and 7. In general, however, it is better to use a second variable to
store the result of the method call. In this manner, the query is less likely to be confused
with the results of the query.
C#
Because Query #7 returns a single value and not a collection, the query executes
immediately.
The previous query can be written by using implicit typing with var, as follows:
C#// var is used for convenience in these queries
var average = numbers1.Average();
var concatenationQuery = numbers1.Concat(numbers2);
var largeNumbersQuery = numbers2.Where(c => c > 15);
Example - Mixed query and method syntax
// Query #7.
// Using a query expression with method syntax
int numCount1 = (
    from num in numbers1
    where num < 3 || num > 7
    select num
).Count();
// Better: Create a new variable to store
// the method call result
IEnumerable< int> numbersQuery =
    from num in numbers1
    where num < 3 || num > 7
    select num;
int numCount2 = numbersQuery.Count();It can be written in method syntax as follows:
C#
It can be written by using explicit typing, as follows:
C#
Walkthrough: Writing Queries in C#
Language Integrated Query (LINQ)
where clausevar numCount = ( from num in numbers...
var numCount = numbers.Where(n => n < 3 || n > 7).Count();
int numCount = numbers.Where(n => n < 3 || n > 7).Count();
See alsoType Relationships in LINQ Query
Operations (C#)
Article •07/18/2023
To write queries effectively, you should understand how types of the variables in a
complete query operation all relate to each other. If you understand these relationships
you will more easily comprehend the LINQ samples and code examples in the
documentation. Furthermore, you will understand what occurs behind the scenes when
variables are implicitly typed by using var.
LINQ query operations are strongly typed in the data source, in the query itself, and in
the query execution. The type of the variables in the query must be compatible with the
type of the elements in the data source and with the type of the iteration variable in the
foreach statement. This strong typing guarantees that type errors are caught at compile
time when they can be corrected before users encounter them.
In order to demonstrate these type relationships, most of the examples that follow use
explicit typing for all variables. The last example shows how the same principles apply
even when you use implicit typing by using var.
The following illustration shows a LINQ to Objects query operation that performs no
transformations on the data. The source contains a sequence of strings and the query
output is also a sequence of strings.
1. The type argument of the data source determines the type of the range variable.
2. The type of the object that is selected determines the type of the query variable.
Here name is a string. Therefore, the query variable is an IEnumerable<string>.Queries that do not Transform the Source Data3. The query variable is iterated over in the foreach statement. Because the query
variable is a sequence of strings, the iteration variable is also a string.
The following illustration shows a LINQ to SQL query operation that performs a simple
transformation on the data. The query takes a sequence of Customer objects as input,
and selects only the Name property in the result. Because Name is a string, the query
produces a sequence of strings as output.
1. The type argument of the data source determines the type of the range variable.
2. The select statement returns the Name property instead of the complete Customer
object. Because Name is a string, the type argument of custNameQuery is string,
not Customer.
3. Because custNameQuery is a sequence of strings, the foreach loop's iteration
variable must also be a string.
The following illustration shows a slightly more complex transformation. The select
statement returns an anonymous type that captures just two members of the original
Customer object.
Queries that Transform the Source Data1. The type argument of the data source is always the type of the range variable in
the query.
2. Because the select statement produces an anonymous type, the query variable
must be implicitly typed by using var.
3. Because the type of the query variable is implicit, the iteration variable in the
foreach loop must also be implicit.
Although you should understand the type relationships in a query operation, you have
the option to let the compiler do all the work for you. The keyword var can be used for
any local variable in a query operation. The following illustration is similar to example
number 2 that was discussed earlier. However, the compiler supplies the strong type for
each variable in the query operation.
For more information about var, see Implicitly T yped Local V ariables .
LINQ queries are based on generic types. Y ou do not need an in-depth knowledge of
generics before you can start writing queries. However, you may want to understand
two basic concepts:
1. When you create an instance of a generic collection class such as List<T> , you
replace the "T" with the type of objects that the list will hold. For example, a list of
strings is expressed as List<string>, and a list of Customer objects is expressed as
List<Customer>. A generic list is strongly typed and provides many benefits over
collections that store their elements as Object . If you try to add a Customer to aLetting  the compiler infer type information
LINQ and generic types (C#)List<string>, you will get an error at compile time. It is easy to use generic
collections because you do not have to perform run-time type-casting.
2. IEnumerable<T>  is the interface that enables generic collection classes to be
enumerated by using the foreach statement. Generic collection classes support
IEnumerable<T>  just as non-generic collection classes such as ArrayList  support
IEnumerable .
For more information about generics, see Generics .
LINQ query variables are typed as IEnumerable<T>  or a derived type such as
IQueryable<T> . When you see a query variable that is typed as IEnumerable<Customer>,
it just means that the query, when it is executed, will produce a sequence of zero or
more Customer objects.
C#
For more information, see Type R elationships in LINQ Query Operations .
If you prefer, you can avoid generic syntax by using the var keyword. The var keyword
instructs the compiler to infer the type of a query variable by looking at the data source
specified in the from clause. The following example produces the same compiled code
as the previous example:
C#IEnum erable<T> variables in LINQ queries
IEnumerable<Customer> customerQuery =
    from cust in customers
    where cust.City == "London"
    select cust;
foreach (Customer customer in customerQuery)
{
    Console.WriteLine(customer.LastName + ", " + customer.FirstName);
}
Letting  the compiler handle generic type
declarations
var customerQuery2 =
    from cust in customersThe var keyword is useful when the type of the variable is obvious or when it is not that
important to explicitly specify nested generic types such as those that are produced by
group queries. In general, we recommend that if you use var, realize that it can make
your code more difficult for others to read. For more information, see Implicitly T yped
Local V ariables .    where cust.City == "London"
    select cust;
foreach(var customer in customerQuery2)
{
    Console.WriteLine(customer.LastName + ", " + customer.FirstName);
}C# Features That Support LINQ
Article •03/09/2023
These new features are all used to a degree with LINQ queries, they are not limited to
LINQ and can be used in any context where you find them useful.
Query expressions use a declarative syntax similar to SQL or XQuery to query over
IEnumerable collections. At compile time query syntax is converted to method calls to a
LINQ provider's implementation of the standard query operator extension methods.
Applications control the standard query operators that are in scope by specifying the
appropriate namespace with a using directive. The following query expression takes an
array of strings, groups them according to the first character in the string, and orders
the groups.
C#
For more information, see LINQ Query Expressions .
Instead of explicitly specifying a type when you declare and initialize a variable, you can
use the var modifier to instruct the compiler to infer and assign the type, as shown here:
C#
Variables declared as var are just as strongly typed as variables whose type you specify
explicitly. The use of var makes it possible to create anonymous types, but it can be
used only for local variables. Arrays can also be declared with implicit typing.Query Expressions
var query = from str in stringArray
            group str by str[0] into stringGroup
            orderby stringGroup.Key
            select stringGroup;
Implicitly Typed Variables (var)
var number = 5;
var name = "Virginia" ;
var query = from str in stringArray
            where str[0] == 'm'
            select str;For more information, see Implicitly T yped Local V ariables .
Object and collection initializers make it possible to initialize objects without explicitly
calling a constructor for the object. Initializers are typically used in query expressions
when they project the source data into a new data type. Assuming a class named
Customer with public Name and Phone properties, the object initializer can be used as in
the following code:
C#
Continuing with our Customer class, assume that there is a data source called
IncomingOrders, and that for each order with a large OrderSize, we would like to create
a new Customer based off of that order. A LINQ query can be executed on this data
source and use object initialization to fill a collection:
C#
The data source may have more properties lying under the hood than the Customer
class such as OrderSize, but with object initialization, the data returned from the query
is molded into the desired data type; we choose the data that is relevant to our class. As
a result, we now have an IEnumerable filled with the new Customers we wanted. The
above can also be written in LINQ's method syntax:
C#
For more information, see:
Object and Collection Initializers
Query Expression S yntax for S tandard Query OperatorsObject and Collection Initializers
var cust = new Customer { Name = "Mike", Phone = "555-1212"  };
var newLargeOrderCustomers = from o in IncomingOrders
                            where o.OrderSize > 5
                            select new Customer { Name = o.Name, Phone =  
o.Phone };
var newLargeOrderCustomers = IncomingOrders.Where(x => x.OrderSize > 
5).Select(y => new Customer { Name = y.Name, Phone = y.Phone });An anonymous type is constructed by the compiler and the type name is only available
to the compiler. Anonymous types provide a convenient way to group a set of
properties temporarily in a query result without having to define a separate named type.
Anonymous types are initialized with a new expression and an object initializer, as
shown here:
C#
For more information, see Anonymous T ypes.
An extension method is a static method that can be associated with a type, so that it can
be called as if it were an instance method on the type. This feature enables you to, in
effect, "add" new methods to existing types without actually modifying them. The
standard query operators are a set of extension methods that provide LINQ query
functionality for any type that implements IEnumerable<T> .
For more information, see Extension Methods .
A lambda expression is an inline function that uses the => operator to separate input
parameters from the function body and can be converted at compile time to a delegate
or an expression tree. In LINQ programming, you encounter lambda expressions when
you make direct method calls to the standard query operators.
For more information, see:
Lambda Expressions
Expression T rees (C#)
Language-Integrated Query (LINQ) (C#)Anonymous Types
select new {name = cust.Name, phone = cust.Phone};
Extension Methods
Lambda Expressions
See alsoStandard Query Operators Overview
(C#)
Article •07/18/2023
The standar d quer y oper ators are the methods that form the LINQ pattern. Most of these
methods operate on sequences, where a sequence is an object whose type implements
the IEnumerable<T>  interface or the IQueryable<T>  interface. The standard query
operators provide query capabilities including filtering, projection, aggregation, sorting
and more.
There are two sets of LINQ standard query operators: one that operates on objects of
type IEnumerable<T> , another that operates on objects of type IQueryable<T> . The
methods that make up each set are static members of the Enumerable  and Queryable
classes, respectively. They are defined as extension methods  of the type that they
operate on. Extension methods can be called by using either static method syntax or
instance method syntax.
In addition, several standard query operator methods operate on types other than those
based on IEnumerable<T>  or IQueryable<T> . The Enumerable  type defines two such
methods that both operate on objects of type IEnumerable . These methods,
Cast<TR esult>(IEnumerable)  and OfType<TR esult>(IEnumerable) , let you enable a non-
parameterized, or non-generic, collection to be queried in the LINQ pattern. They do
this by creating a strongly typed collection of objects. The Queryable  class defines two
similar methods, Cast<TR esult>(IQueryable)  and OfType<TR esult>(IQueryable) , that
operate on objects of type IQueryable .
The standard query operators differ in the timing of their execution, depending on
whether they return a singleton value or a sequence of values. Those methods that
return a singleton value (for example, Average  and Sum) execute immediately. Methods
that return a sequence defer the query execution and return an enumerable object.
For methods that operate on in-memory collections, that is, those methods that extend
IEnumerable<T> , the returned enumerable object captures the arguments that were
passed to the method. When that object is enumerated, the logic of the query operator
is employed and the query results are returned.
In contrast, methods that extend IQueryable<T>  don't implement any querying
behavior. They build an expression tree that represents the query to be performed. The
query processing is handled by the source IQueryable<T>  object.Calls to query methods can be chained together in one query, which enables queries to
become arbitrarily complex.
The following code example demonstrates how the standard query operators can be
used to obtain information about a sequence.
C#
Some of the more frequently used standard query operators have dedicated C# and
Visual Basic language keyword syntax that enables them to be called as part of a querystring sentence = "the quick brown fox jumps over the lazy dog" ;  
// Split the string into individual words to create a collection.  
string[] words = sentence.Split( ' ');  
  
// Using query expression syntax.  
var query = from word in words  
            group word.ToUpper() by word.Length into gr  
            orderby gr.Key  
            select new { Length = gr.Key, Words = gr };  
  
// Using method-based query syntax.  
var query2 = words.  
    GroupBy(w => w.Length, w => w.ToUpper()).  
    Select(g => new { Length = g.Key, Words = g }).  
    OrderBy(o => o.Length);  
  
foreach (var obj in query)  
{  
    Console.WriteLine( "Words of length {0}:" , obj.Length);  
    foreach (string word in obj.Words)  
        Console.WriteLine(word);  
}  
  
// This code example produces the following output:  
//  
// Words of length 3:  
// THE  
// FOX  
// THE  
// DOG  
// Words of length 4:  
// OVER  
// LAZY  
// Words of length 5:  
// QUICK  
// BROWN  
// JUMPS
Query expression syntaxexpression . For more information about standard query operators that have dedicated
keywords and their corresponding syntaxes, see Query Expression S yntax for S tandard
Query Operators (C#) .
You can augment the set of standard query operators by creating domain-specific
methods that are appropriate for your target domain or technology. Y ou can also
replace the standard query operators with your own implementations that provide
additional services such as remote evaluation, query translation, and optimization. See
AsEnumerable  for an example.
In a LINQ query, the first step is to specify the data source. In C# as in most
programming languages a variable must be declared before it can be used. In a LINQ
query, the from clause comes first in order to introduce the data source ( customers) and
the range v ariable  (cust).
C#
The range variable is like the iteration variable in a foreach loop except that no actual
iteration occurs in a query expression. When the query is executed, the range variable
will serve as a reference to each successive element in customers. Because the compiler
can infer the type of cust, you do not have to specify it explicitly. Additional range
variables can be introduced by a let clause. For more information, see let clause .Extending the standard query operators
Obtain a data source
//queryAllCustomers is an IEnumerable<Customer>
var queryAllCustomers = from cust in customers
                        select cust;
７ Note
For non-generic data sources such as ArrayList , the range variable must be
explicitly typed. For more information, see How t o quer y an ArrayList with LINQ
(C#) and from clause .
FilteringProbably the most common query operation is to apply a filter in the form of a Boolean
expression. The filter causes the query to return only those elements for which the
expression is true. The result is produced by using the where clause. The filter in effect
specifies which elements to exclude from the source sequence. In the following example,
only those customers who have an address in London are returned.
C#
You can use the familiar C# logical AND and OR operators to apply as many filter
expressions as necessary in the where clause. For example, to return only customers
from "London" AND whose name is "Devon" you would write the following code:
C#
To return customers from London or P aris, you would write the following code:
C#
For more information, see where clause .
Often it is convenient to sort the returned data. The orderby clause will cause the
elements in the returned sequence to be sorted according to the default comparer for
the type being sorted. For example, the following query can be extended to sort the
results based on the Name property. Because Name is a string, the default comparer
performs an alphabetical sort from A to Z.
C#var queryLondonCustomers = from cust in customers
                           where cust.City == "London"
                           select cust;
where cust.City == "London"  && cust.Name == "Devon"
where cust.City == "London"  || cust.City == "Paris"
Ordering
var queryLondonCustomers3 =
    from cust in customers
    where cust.City == "London"To order the results in reverse order, from Z to A, use the orderby…descending clause.
For more information, see orderby clause .
The group clause enables you to group your results based on a key that you specify. For
example you could specify that the results should be grouped by the City so that all
customers from London or P aris are in individual groups. In this case, cust.City is the
key.
C#
When you end a query with a group clause, your results take the form of a list of lists.
Each element in the list is an object that has a Key member and a list of elements that
are grouped under that key. When you iterate over a query that produces a sequence of
groups, you must use a nested foreach loop. The outer loop iterates over each group,
and the inner loop iterates over each group's members.
If you must refer to the results of a group operation, you can use the into keyword to
create an identifier that can be queried further. The following query returns only those
groups that contain more than two customers:
C#    orderby cust.Name ascending
    select cust;
Grouping
// queryCustomersByCity is an IEnumerable<IGrouping<string, Customer>>
  var queryCustomersByCity =
      from cust in customers
      group cust by cust.City;
  // customerGroup is an IGrouping<string, Customer>
  foreach (var customerGroup in queryCustomersByCity)
  {
      Console.WriteLine(customerGroup.Key);
      foreach (Customer customer in customerGroup)
      {
          Console.WriteLine( "    {0}" , customer.Name);
      }
  }
// custQuery is an IEnumerable<IGrouping<string, Customer>>
var custQuery =For more information, see group clause .
Join operations create associations between sequences that are not explicitly modeled
in the data sources. For example you can perform a join to find all the customers and
distributors who have the same location. In LINQ the join clause always works against
object collections instead of database tables directly.
C#
In LINQ, you do not have to use join as often as you do in SQL, because foreign keys in
LINQ are represented in the object model as properties that hold a collection of items.
For example, a Customer object contains a collection of Order objects. Rather than
performing a join, you access the orders by using dot notation:
C#
For more information, see join clause .
The select clause produces the results of the query and specifies the "shape" or type of
each returned element. For example, you can specify whether your results will consist of
complete Customer objects, just one member, a subset of members, or some completely
different result type based on a computation or new object creation. When the select
clause produces something other than a copy of the source element, the operation is
called a projection . The use of projections to transform data is a powerful capability of    from cust in customers
    group cust by cust.City into custGroup
    where custGroup.Count() > 2
    orderby custGroup.Key
    select custGroup;
Joining
var innerJoinQuery =
    from cust in customers
    join dist in distributors on cust.City equals dist.City
    select new { CustomerName = cust.Name, DistributorName = dist.Name };
from order in Customer.Orders...  
Selecting (Projections)LINQ query expressions. For more information, see Data T ransformations with LINQ (C#)
and select clause .
The following table lists the standard query operators that have equivalent query
expression clauses.
Method C# quer y expr ession
syntax
Cast Use an explicitly
typed range variable,
for example:
from int i in
numbers
(For more
information, see from
clause .)
GroupBy group … by
-or-
group … by … into …
(For more
information, see
group clause .)
GroupJoin<T Outer,TInner,TK ey,TR esult>(IEnumerable<T Outer>,
IEnumerable<TInner>, Func<T Outer,TK ey>, Func<TInner,TK ey>,
Func<T Outer,IEnumerable<TInner>, TR esult>)join … in … on …
equals … into …
(For more
information, see join
clause .)
Join<T Outer,TInner,TK ey,TR esult>(IEnumerable<T Outer>,
IEnumerable<TInner>, Func<T Outer,TK ey>, Func<TInner,TK ey>,
Func<T Outer,TInner,TR esult>)join … in … on …
equals …
(For more
information, see join
clause .)
OrderBy<T Source,TK ey>(IEnumerable<T Source>, Func<T Source,TK ey>) orderbyQuery Expression Syntax TableMethod C# quer y expr ession
syntax
(For more
information, see
orderby clause .)
OrderByDescending<T Source,TK ey>(IEnumerable<T Source>,
Func<T Source,TK ey>)orderby …
descending
(For more
information, see
orderby clause .)
Select select
(For more
information, see
select clause .)
SelectMany Multiple from
clauses.
(For more
information, see from
clause .)
ThenBy<T Source,TK ey>(IOrderedEnumerable<T Source>,
Func<T Source,TK ey>)orderby …, …
(For more
information, see
orderby clause .)
ThenByDescending<T Source,TK ey>(IOrderedEnumerable<T Source>,
Func<T Source,TK ey>)orderby …, …
descending
(For more
information, see
orderby clause .)
Where where
(For more
information, see
where clause .)
EnumerableSee alsoQueryable
Extension Methods
Query K eywords (LINQ)
Anonymous T ypesData Transformations with LINQ (C#)
Article •09/15/2021
Language-Integrated Query (LINQ) is not only about retrieving data. It is also a powerful
tool for transforming data. By using a LINQ query, you can use a source sequence as
input and modify it in many ways to create a new output sequence. Y ou can modify the
sequence itself without modifying the elements themselves by sorting and grouping.
But perhaps the most powerful feature of LINQ queries is the ability to create new types.
This is accomplished in the select  clause. For example, you can perform the following
tasks:
Merge multiple input sequences into a single output sequence that has a new
type.
Create output sequences whose elements consist of only one or several properties
of each element in the source sequence.
Create output sequences whose elements consist of the results of operations
performed on the source data.
Create output sequences in a different format. For example, you can transform
data from SQL rows or text files into XML.
These are just several examples. Of course, these transformations can be combined in
various ways in the same query. Furthermore, the output sequence of one query can be
used as the input sequence for a new query.
You can use a LINQ query to create an output sequence that contains elements from
more than one input sequence. The following example shows how to combine two in-
memory data structures, but the same principles can be applied to combine data from
XML or SQL or DataSet sources. Assume the following two class types:
C#Joining  Multip le Inputs into One Output
Sequence
class Student
{
    public string First { get; set; }
    public string Last {get; set;}
    public int ID { get; set; }
    public string Street { get; set; }The following example shows the query:
C#    public string City { get; set; }
    public List<int> Scores;
}
class Teacher
{
    public string First { get; set; }
    public string Last { get; set; }
    public int ID { get; set; }
    public string City { get; set; }
}
class DataTransformations
{
    static void Main()
    {
        // Create the first data source.
        List<Student> students = new List<Student>()
        {
            new Student { First= "Svetlana" ,
                Last="Omelchenko" ,
                ID=111,
                Street="123 Main Street" ,
                City="Seattle" ,
                Scores= new List<int> { 97, 92, 81, 60 } },
            new Student { First= "Claire" ,
                Last="O’Donnell" ,
                ID=112,
                Street="124 Main Street" ,
                City="Redmond" ,
                Scores= new List<int> { 75, 84, 91, 39 } },
            new Student { First= "Sven",
                Last="Mortensen" ,
                ID=113,
                Street="125 Main Street" ,
                City="Lake City" ,
                Scores= new List<int> { 88, 94, 65, 91 } },
        };
        // Create the second data source.
        List<Teacher> teachers = new List<Teacher>()
        {
            new Teacher { First= "Ann", Last="Beebe", ID=945, City="Seattle"  
},
            new Teacher { First= "Alex", Last="Robinson" , ID=956, 
City="Redmond"  },
            new Teacher { First= "Michiyo" , Last="Sato", ID=972, 
City="Tacoma"  }
        };For more information, see join clause  and select clause .
There are two primary ways to select a subset of each element in the source sequence:
1. To select just one member of the source element, use the dot operation. In the
following example, assume that a Customer object contains several public
properties including a string named City. When executed, this query will produce
an output sequence of strings.
C#
2. To create elements that contain more than one property from the source element,
you can use an object initializer with either a named object or an anonymous type.
The following example shows the use of an anonymous type to encapsulate two
properties from each Customer element:        // Create the query.
        var peopleInSeattle = ( from student in students
                    where student.City == "Seattle"
                    select student.Last)
                    .Concat( from teacher in teachers
                            where teacher.City == "Seattle"
                            select teacher.Last);
        Console.WriteLine( "The following students and teachers live in  
Seattle:" );
        // Execute the query.
        foreach (var person in peopleInSeattle)
        {
            Console.WriteLine(person);
        }
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
    The following students and teachers live in Seattle:
    Omelchenko
    Beebe
 */
Selecting a Subset of each Source Element
var query = from cust in Customers  
            select cust.City;  C#
For more information, see Object and Collection Initializers  and Anonymous T ypes.
LINQ queries make it easy to transform data between in-memory data structures, SQL
databases, ADO.NET Datasets and XML streams or documents. The following example
transforms objects in an in-memory data structure into XML elements.
C#var query = from cust in Customer  
            select new {Name = cust.Name, City = cust.City};  
Transforming in-Memory Objects into XML
class XMLTransform
{
    static void Main()
    {
        // Create the data source by using a collection initializer.
        // The Student class was defined previously in this topic.
        List<Student> students = new List<Student>()
        {
            new Student {First= "Svetlana" , Last="Omelchenko" , ID=111, Scores  
= new List<int>{97, 92, 81, 60}},
            new Student {First= "Claire" , Last="O’Donnell" , ID=112, Scores = 
new List<int>{75, 84, 91, 39}},
            new Student {First= "Sven", Last="Mortensen" , ID=113, Scores = 
new List<int>{88, 94, 65, 91}},
        };
        // Create the query.
        var studentsToXML = new XElement( "Root",
            from student in students
            let scores = string.Join(",", student.Scores)
            select new XElement ("student" ,
                       new XElement( "First", student.First ),
                       new XElement ("Last", student.Last ),
                       new XElement ("Scores" , scores )
                    ) // end "student"
                ); // end "Root"
        // Execute the query.
        Console.WriteLine(studentsToXML);
        // Keep the console open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();The code produces the following XML output:
XML
For more information, see Creating XML T rees in C# (LINQ to XML) .
An output sequence might not contain any elements or element properties from the
source sequence. The output might instead be a sequence of values that is computed by
using the source elements as input arguments.
The following query will take a sequence of numbers that represent radii of circles,
calculate the area for each radius, and return an output sequence containing strings
formatted with the calculated area.
Each string for the output sequence will be formatted using string interpolation . An
interpolated string will have a $ in front of the string's opening quotation mark, and
operations can be performed within curly braces placed inside the interpolated string.
Once those operations are performed, the results will be concatenated.    }
}
<Root>  
  <student>  
    <First>Svetlana </First>  
    <Last>Omelchenko </Last>  
    <Scores>97,92,81,60 </Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell </Last>  
    <Scores>75,84,91,39 </Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen </Last>  
    <Scores>88,94,65,91 </Scores>  
  </student>  
</Root>  
Performing Operations on Source Elements
７ Note
Calling methods in query expressions is not supported if the query will be
translated into some other domain. For example, you cannot call an ordinary C#C#
Language-Integrated Query (LINQ) (C#)
LINQ to SQL
LINQ to DataSet
LINQ to XML (C#)method in LINQ to SQL because SQL Server has no context for it. However, you can
map stored procedures to methods and call those. For more information, see
Stored Pr ocedur es.
class FormatQuery
{
    static void Main()
    {
        // Data source.
        double[] radii = { 1, 2, 3 };
        // LINQ query using method syntax.
        IEnumerable< string> output = 
            radii.Select(r => $"Area for a circle with a radius of ' {r}' = 
{r * r * Math.PI:F2} ");
        /*
        // LINQ query using query syntax.
        IEnumerable<string> output =
            from rad in radii
            select $"Area for a circle with a radius of '{rad}' = {rad * rad  
* Math.PI:F2}";
        */
        foreach (string s in output)
        {
            Console.WriteLine(s);
        }
            
        // Keep the console open in debug mode.
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
    Area for a circle with a radius of '1' = 3.14
    Area for a circle with a radius of '2' = 12.57
    Area for a circle with a radius of '3' = 28.27
*/
See alsoselect clauseStore the results of a query in memory
Article •02/18/2022
A query is basically a set of instructions for how to retrieve and organize data. Queries
are executed lazily, as each subsequent item in the result is requested. When you use
foreach to iterate the results, items are returned as accessed. T o evaluate a query and
store its results without executing a foreach loop, just call one of the following methods
on the query variable:
ToList
ToArray
ToDictionary
ToLookup
We recommend that when you store the query results, you assign the returned
collection object to a new variable as shown in the following example:
C#
Language Integrated Query (LINQ)Example
List<int> numbers = new() { 1, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 }; 
IEnumerable< int> queryFactorsOfFour =  
    from num in numbers  
    where num % 4 == 0 
    select num; 
// Store the results in a new variable  
// without executing a foreach loop.  
List<int> factorsofFourList = queryFactorsOfFour.ToList();  
// Read and write from the newly created list to demonstrate that it holds  
data. 
Console.WriteLine(factorsofFourList[ 2]); 
factorsofFourList[ 2] = 0; 
Console.WriteLine(factorsofFourList[ 2]); 
See alsoFiltering Data (C#)
Article •03/15/2023
Filtering refers to the operation of restricting the result set to contain only those
elements that satisfy a specified condition. It is also known as selection.
The following illustration shows the results of filtering a sequence of characters. The
predicate for the filtering operation specifies that the character must be 'A'.
The standard query operator methods that perform selection are listed in the following
section.
Method
NameDescr iption C# Quer y
Expr ession S yntaxMore Infor mation
OfType Selects values, depending on their
ability to be cast to a specified type.Not applicable. Enumerable.OfT ype
Queryable.OfT ype
Where Selects values that are based on a
predicate function.where Enumerable.Where
Queryable.Where
The following example uses the where clause to filter from an array those strings that
have a specific length.
C#Methods
Query Expression Syntax Example
string[] words = [ "the", "quick", "brown", "fox", "jumps" ];  
  
IEnumerable< string> query = from word in words  
                            where word.Length == 3  
                            select word;  System.Linq
Standard Query Operators Overview (C#)
where clause
Dynamically specify predicate filters at run time
How to query an assembly's metadata with R eflection (LINQ) (C#)
How to query for files with a specified attribute or name (C#)
How to sort or filter text data by any word or field (LINQ) (C#)  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
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
 Provide product feedbackProjection operations (C#)
Article •10/06/2022
Projection refers to the operation of transforming an object into a new form that often
consists only of those properties that will be subsequently used. By using projection, you
can construct a new type that is built from each object. Y ou can project a property and
perform a mathematical function on it. Y ou can also project the original object without
changing it.
The standard query operator methods that perform projection are listed in the following
section.
Method
namesDescr iption C# quer y
expr ession
syntaxMore infor mation
Select Projects values that are based on a
transform function.select Enumerable.Select
Queryable.Select
SelectMany Projects sequences of values that are
based on a transform function and
then flattens them into one
sequence.Use multiple
from clausesEnumerable.SelectMany
Queryable.SelectMany
Zip Produces a sequence of tuples with
elements from 2-3 specified
sequences.Not applicable. Enumerable.Zip
Queryable.Zip
The following example uses the select clause to project the first letter from each string
in a list of strings.
C#Methods
Select
List<string> words = [ "an", "apple", "a", "day" ];
var query = from word in words
            select word.Substring( 0, 1);
foreach (string s in query)
    Console.WriteLine(s);The following example uses multiple from clauses to project each word from each string
in a list of strings.
C#
There are several overloads for the Zip projection operator. All of the Zip methods
work on sequences of two or more possibly heterogenous types. The first two overloads
return tuples, with the corresponding positional type from the given sequences.
Consider the following collections:
C#/* This code produces the following output:
    a
    a
    a
    d
*/
SelectMany
List<string> phrases = [ "an apple a day" , "the quick brown fox" ];
var query = from phrase in phrases
            from word in phrase.Split( ' ')
            select word;
foreach (string s in query)
    Console.WriteLine(s);
/* This code produces the following output:
    an
    apple
    a
    day
    the
    quick
    brown
    fox
*/
ZipTo project these sequences together, use the Enumerable.Zip<TFirst,T Second>
(IEnumerable<TFirst>, IEnumerable<T Second>)  operator:
C#
The second overload accepts a third sequence. Let's create another collection, namely
emoji:
C#// An int array with 7 elements.
IEnumerable< int> numbers =
[
    1, 2, 3, 4, 5, 6, 7
];
// A char array with 6 elements.
IEnumerable< char> letters =
[
    'A', 'B', 'C', 'D', 'E', 'F'
];
foreach ((int number, char letter) in numbers.Zip(letters))
{
    Console.WriteLine( $"Number: {number}  zipped with letter: ' {letter} '");
}
// This code produces the following output:
//     Number: 1 zipped with letter: 'A'
//     Number: 2 zipped with letter: 'B'
//     Number: 3 zipped with letter: 'C'
//     Number: 4 zipped with letter: 'D'
//     Number: 5 zipped with letter: 'E'
//     Number: 6 zipped with letter: 'F'
） Impor tant
The resulting sequence from a zip operation is never longer in length than the
shortest sequence. The numbers and letters collections differ in length, and the
resulting sequence omits the last element from the numbers collection, as it has
nothing to zip with.
// A string array with 8 elements.
IEnumerable< string> emoji = 
[
    "🤓", "🔥", "🎉", "👀", "⭐", "💜", " ✔", "💯"
];To project these sequences together, use the Enumerable.Zip<TFirst,T Second,T Third>
(IEnumerable<TFirst>, IEnumerable<T Second>, IEnumerable<T Third>)  operator:
C#
Much like the previous overload, the Zip method projects a tuple, but this time with
three elements.
The third overload accepts a Func<TFirst, TSecond, TResult> argument that acts as a
results selector. Given the two types from the sequences being zipped, you can project a
new resulting sequence.
C#
With the preceding Zip overload, the specified function is applied to the corresponding
elements numbers and letter, producing a sequence of the string results.foreach ((int number, char letter, string em) in numbers.Zip(letters,  
emoji))
{
    Console.WriteLine(
        $"Number: {number}  is zipped with letter: ' {letter} ' and emoji: 
{em}");
}
// This code produces the following output:
//     Number: 1 is zipped with letter: 'A' and emoji: 🤓
//     Number: 2 is zipped with letter: 'B' and emoji: 🔥
//     Number: 3 is zipped with letter: 'C' and emoji: 🎉
//     Number: 4 is zipped with letter: 'D' and emoji: 👀
//     Number: 5 is zipped with letter: 'E' and emoji: ⭐
//     Number: 6 is zipped with letter: 'F' and emoji: 💜
foreach (string result in
    numbers.Zip(letters, (number, letter) => $"{number}  = {letter}  
({(int)letter} )"))
{
    Console.WriteLine(result);
}
// This code produces the following output:
//     1 = A (65)
//     2 = B (66)
//     3 = C (67)
//     4 = D (68)
//     5 = E (69)
//     6 = F (70)
Select versus SelectManyThe work of both Select and SelectMany is to produce a result value (or values) from
source values. Select produces one result value for every source value. The overall
result is therefore a collection that has the same number of elements as the source
collection. In contrast, SelectMany produces a single overall result that contains
concatenated sub-collections from each source value. The transform function that is
passed as an argument to SelectMany must return an enumerable sequence of values
for each source value. These enumerable sequences are then concatenated by
SelectMany to create one large sequence.
The following two illustrations show the conceptual difference between the actions of
these two methods. In each case, assume that the selector (transform) function selects
the array of flowers from each source value.
This illustration depicts how Select returns a collection that has the same number of
elements as the source collection.
This illustration depicts how SelectMany concatenates the intermediate sequence of
arrays into one final result value that contains each value from each intermediate array.
The following example compares the behavior of Select and SelectMany. The code
creates a "bouquet" of flowers by taking the items from each list of flower names in the
source collection. In this example, the "single value" that the transform function
Select<T Source,TR esult>(IEnumerable<T Source>, Func<T Source,TR esult>)  uses is itself
a collection of values. This requires the extra foreach loop in order to enumerate each
string in each sub-sequence.
C#Code example
class Bouquet
{
    public List<string> Flowers { get; set; }
}
static void SelectVsSelectMany ()
{
    List<Bouquet> bouquets = 
    [
        new Bouquet { Flowers = new List<string> { "sunflower" , "daisy", 
"daffodil" , "larkspur"  }},
        new Bouquet { Flowers = new List<string> { "tulip", "rose", "orchid"  
}},
        new Bouquet { Flowers = new List<string> { "gladiolis" , "lily", 
"snapdragon" , "aster", "protea"  }},
        new Bouquet { Flowers = new List<string> { "larkspur" , "lilac", 
"iris", "dahlia"  }}
    ];
    IEnumerable<List< string>> query1 = bouquets.Select(bq => bq.Flowers);
    IEnumerable< string> query2 = bouquets.SelectMany(bq => bq.Flowers);
    Console.WriteLine( "Results by using Select():" );
    // Note the extra foreach loop here.
    foreach (IEnumerable<String> collection in query1)
        foreach (string item in collection)
            Console.WriteLine(item);
    Console.WriteLine( "\nResults by using SelectMany():" );
    foreach (string item in query2)
        Console.WriteLine(item);
    /* This code produces the following output:
       Results by using Select():
        sunflower
        daisy
        daffodil
        larkspurSystem.Linq
Standard Query Operators Overview (C#)
select clause
How to populate object collections from multiple sources (LINQ) (C#)
How to split a file into many files by using groups (LINQ) (C#)        tulip
        rose
        orchid
        gladiolis
        lily
        snapdragon
        aster
        protea
        larkspur
        lilac
        iris
        dahlia
       Results by using SelectMany():
        sunflower
        daisy
        daffodil
        larkspur
        tulip
        rose
        orchid
        gladiolis
        lily
        snapdragon
        aster
        protea
        larkspur
        lilac
        iris
        dahlia
    */
}
See also
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review.NET feedb ack
The .NET documentation is open
source. Provide feedback here.
 Open a documentation issueissues and pull requests. For
more information, see our
contributor guide . Provide product feedbackSet operations (C#)
Article •12/22/2021
Set operations in LINQ refer to query operations that produce a result set that is based
on the presence or absence of equivalent elements within the same or separate
collections (or sets).
The standard query operator methods that perform set operations are listed in the
following section.
Method
namesDescr iption C# quer y
expr ession
syntaxMore infor mation
Distinct or
DistinctByRemoves duplicate values from a
collection.Not
applicable.Enumerable.Distinct  
Enumerable.DistinctBy  
Queryable.Distinct  
Queryable.DistinctBy
Except or
ExceptByReturns the set difference, which means
the elements of one collection that do not
appear in a second collection.Not
applicable.Enumerable.Except  
Enumerable.ExceptBy  
Queryable.Except  
Queryable.ExceptBy
Intersect
or
IntersectByReturns the set intersection, which means
elements that appear in each of two
collections.Not
applicable.Enumerable.Intersect  
Enumerable.IntersectBy  
Queryable.Intersect  
Queryable.IntersectBy
Union or
UnionByReturns the set union, which means unique
elements that appear in either of two
collections.Not
applicable.Enumerable.Union  
Enumerable.UnionBy  
Queryable.Union  
Queryable.UnionBy
Some of the following examples rely on a record type that represents the planets in our
solar system.
C#Methods
ExamplesThe record Planet is a positional record, which requires a Name, Type, and OrderFromSun
arguments to instantiate it. There are several static readonly planet instances on the
Planet type. These are convenience-based definitions for well-known planets. The Type
member identifies the planet type.
C#namespace  SolarSystem ; 
record Planet( 
    string Name, 
    PlanetType Type,  
    int OrderFromSun ) 
{ 
    public static readonly  Planet Mercury =  
        new(nameof(Mercury), PlanetType.Rock, 1); 
    public static readonly  Planet Venus =  
        new(nameof(Venus), PlanetType.Rock, 2); 
    public static readonly  Planet Earth =  
        new(nameof(Earth), PlanetType.Rock, 3); 
    public static readonly  Planet Mars =  
        new(nameof(Mars), PlanetType.Rock, 4); 
    public static readonly  Planet Jupiter =  
        new(nameof(Jupiter), PlanetType.Gas, 5); 
    public static readonly  Planet Saturn =  
        new(nameof(Saturn), PlanetType.Gas, 6); 
    public static readonly  Planet Uranus =  
        new(nameof(Uranus), PlanetType.Liquid, 7); 
    public static readonly  Planet Neptune =  
        new(nameof(Neptune), PlanetType.Liquid, 8); 
    // Yes, I know... not technically a planet anymore  
    public static readonly  Planet Pluto =  
        new(nameof(Pluto), PlanetType.Ice, 9); 
} 
namespace  SolarSystem ; 
enum PlanetType  
{ 
    Rock,  
    Ice,  
    Gas,  The following example depicts the behavior of the Enumerable.Distinct  method on a
sequence of strings. The returned sequence contains the unique elements from the
input sequence.
C#
The DistinctBy  is an alternative approach to Distinct that takes a keySelector. The
keySelector is used as the comparative discriminator of the source type. Consider the
following planet array:
C#    Liquid  
}; 
Distinct and DistinctBy
string[] planets = { "Mercury" , "Venus", "Venus", "Earth", "Mars", "Earth" 
}; 
IEnumerable< string> query = from planet in planets.Distinct()  
                            select planet;  
foreach (var str in query) 
{ 
    Console.WriteLine(str);  
} 
/* This code produces the following output:  
 * 
 * Mercury  
 * Venus  
 * Earth  
 * Mars 
 */ 
Planet[] planets =  
{ 
    Planet.Mercury,  
    Planet.Venus,  
    Planet.Earth,  
    Planet.Mars,  
    Planet.Jupiter,  
    Planet.Saturn,  
    Planet.Uranus,  In the following code, planets are discriminated based on their PlanetType, and the first
planet of each type is displayed:
C#
In the preceding C# code:
The Planet array is filtered distinctly to the first occurrence of each unique planet
type.
The resulting planet instances are written to the console.
The following example depicts the behavior of Enumerable.Except . The returned
sequence contains only the elements from the first input sequence that are not in the
second input sequence.
C#    Planet.Neptune,  
    Planet.Pluto  
}; 
foreach (Planet planet in planets.DistinctBy(p => p.Type))  
{ 
    Console.WriteLine(planet);  
} 
// This code produces the following output:  
//     Planet { Name = Mercury, Type = Rock, OrderFromSun = 1 }  
//     Planet { Name = Jupiter, Type = Gas, OrderFromSun = 5 }  
//     Planet { Name = Uranus, Type = Liquid, OrderFromSun = 7 }  
//     Planet { Name = Pluto, Type = Ice, OrderFromSun = 9 }  
Except and ExceptBy
string[] planets1 = { "Mercury" , "Venus", "Earth", "Jupiter"  }; 
string[] planets2 = { "Mercury" , "Earth", "Mars", "Jupiter"  }; 
IEnumerable< string> query = from planet in planets1.Except(planets2)  
                            select planet;  
foreach (var str in query) 
{ The ExceptBy  method is an alternative approach to Except that takes two sequences of
possibly heterogenous types and a keySelector. The keySelector is the same type as
the second collection's type, and it is used as the comparative discriminator of the
source type. Consider the following planet arrays:
C#
To find planets in the first collection that aren't in the second collection, you can project
the planet names as the second collection and provide the same keySelector:
C#    Console.WriteLine(str);  
} 
/* This code produces the following output:  
 * 
 * Venus  
 */ 
Planet[] planets =  
{ 
    Planet.Mercury,  
    Planet.Venus,  
    Planet.Earth,  
    Planet.Jupiter  
}; 
Planet[] morePlanets =  
{ 
    Planet.Mercury,  
    Planet.Earth,  
    Planet.Mars,  
    Planet.Jupiter  
}; 
// A shared "keySelector"  
static string PlanetNameSelector (Planet planet ) => planet.Name;  
foreach (Planet planet in 
    planets.ExceptBy(  
        morePlanets.Select(PlanetNameSelector), PlanetNameSelector))  
{ 
    Console.WriteLine(planet);  
} 
// This code produces the following output:  
//     Planet { Name = Venus, Type = Rock, OrderFromSun = 2 }  In the preceding C# code:
The keySelector is defined as a static local function that discriminates on a
planet name.
The first planet array is filtered to planets that are not found in the second planet
array, based on their name.
The resulting planet instance is written to the console.
The following example depicts the behavior of Enumerable.Intersect . The returned
sequence contains the elements that are common to both of the input sequences.
C#
The IntersectBy  method is an alternative approach to Intersect that takes two
sequences of possibly heterogenous types and a keySelector. The keySelector is used
as the comparative discriminator of the second collection's type. Consider the following
planet arrays:
C#Intersect and IntersectBy
string[] planets1 = { "Mercury" , "Venus", "Earth", "Jupiter"  }; 
string[] planets2 = { "Mercury" , "Earth", "Mars", "Jupiter"  }; 
IEnumerable< string> query = from planet in planets1.Intersect(planets2)  
                            select planet;  
foreach (var str in query) 
{ 
    Console.WriteLine(str);  
} 
/* This code produces the following output:  
 * 
 * Mercury  
 * Earth  
 * Jupiter  
 */ There are two arrays of planets; one represents the first five planets from the sun and
the second represents the last five planets from the sun. Since the Planet type is a
positional record type, you can use its value comparison semantics in the form of the
keySelector:
C#
In the preceding C# code:
The two Planet arrays are intersected by their value comparison semantics.
Only planets that are found in both arrays are present in the resulting sequence.
The resulting planet instances are written to the console.
The following example depicts a union operation on two sequences of strings. The
returned sequence contains the unique elements from both input sequences.Planet[] firstFivePlanetsFromTheSun =  
{ 
    Planet.Mercury,  
    Planet.Venus,  
    Planet.Earth,  
    Planet.Mars,  
    Planet.Jupiter  
}; 
Planet[] lastFivePlanetsFromTheSun =  
{ 
    Planet.Mars,  
    Planet.Jupiter,  
    Planet.Saturn,  
    Planet.Uranus,  
    Planet.Neptune  
}; 
foreach (Planet planet in 
    firstFivePlanetsFromTheSun.IntersectBy(  
        lastFivePlanetsFromTheSun, planet => planet))  
{ 
    Console.WriteLine(planet);  
} 
// This code produces the following output:  
//     Planet { Name = Mars, Type = Rock, OrderFromSun = 4 }  
//     Planet { Name = Jupiter, Type = Gas, OrderFromSun = 5 }  
Union and UnionByC#
The UnionBy  method is an alternative approach to Union that takes two sequences of
the same type and a keySelector. The keySelector is used as the comparative
discriminator of the source type. Consider the following planet arrays:
C#string[] planets1 = { "Mercury" , "Venus", "Earth", "Jupiter"  }; 
string[] planets2 = { "Mercury" , "Earth", "Mars", "Jupiter"  }; 
IEnumerable< string> query = from planet in planets1.Union(planets2)  
                            select planet;  
foreach (var str in query) 
{ 
    Console.WriteLine(str);  
} 
/* This code produces the following output:  
 * 
 * Mercury  
 * Venus  
 * Earth  
 * Jupiter  
 * Mars 
 */ 
Planet[] firstFivePlanetsFromTheSun =  
{ 
    Planet.Mercury,  
    Planet.Venus,  
    Planet.Earth,  
    Planet.Mars,  
    Planet.Jupiter  
}; 
Planet[] lastFivePlanetsFromTheSun =  
{ 
    Planet.Mars,  
    Planet.Jupiter,  
    Planet.Saturn,  
    Planet.Uranus,  
    Planet.Neptune  
}; To union these two collections into a single sequence, you provide the keySelector:
C#
In the preceding C# code:
The two Planet arrays are weaved together using their record value comparison
semantics.
The resulting planet instances are written to the console.
System.Linq
Standard Query Operators Overview (C#)
How to combine and compare string collections (LINQ) (C#)
How to find the set difference between two lists (LINQ) (C#)foreach (Planet planet in 
    firstFivePlanetsFromTheSun.UnionBy(  
        lastFivePlanetsFromTheSun, planet => planet))  
{ 
    Console.WriteLine(planet);  
} 
// This code produces the following output:  
//     Planet { Name = Mercury, Type = Rock, OrderFromSun = 1 }  
//     Planet { Name = Venus, Type = Rock, OrderFromSun = 2 }  
//     Planet { Name = Earth, Type = Rock, OrderFromSun = 3 }  
//     Planet { Name = Mars, Type = Rock, OrderFromSun = 4 }  
//     Planet { Name = Jupiter, Type = Gas, OrderFromSun = 5 }  
//     Planet { Name = Saturn, Type = Gas, OrderFromSun = 6 }  
//     Planet { Name = Uranus, Type = Liquid, OrderFromSun = 7 }  
//     Planet { Name = Neptune, Type = Liquid, OrderFromSun = 8 }  
See alsoSorting Data (C#)
Article •09/15/2021
A sorting operation orders the elements of a sequence based on one or more attributes.
The first sort criterion performs a primary sort on the elements. By specifying a second
sort criterion, you can sort the elements within each primary sort group.
The following illustration shows the results of an alphabetical sort operation on a
sequence of characters:
The standard query operator methods that sort data are listed in the following section.
Method Name Descr iption C# Quer y
Expr ession
SyntaxMore Infor mation
OrderBy Sorts values in
ascending order.orderby Enumerable.OrderBy
Queryable.OrderBy
OrderByDescending Sorts values in
descending order.orderby …
descendingEnumerable.OrderByDescending
Queryable.OrderByDescending
ThenBy Performs a secondary
sort in ascending
order.orderby …, … Enumerable.ThenBy
Queryable.ThenBy
ThenByDescending Performs a secondary
sort in descending
order.orderby …, …
descendingEnumerable.ThenByDescending
Queryable.ThenByDescending
Reverse Reverses the order of
the elements in a
collection.Not applicable. Enumerable.R everse
Queryable.R everseMethodsThe following example demonstrates how to use the orderby clause in a LINQ query to
sort the strings in an array by string length, in ascending order.
C#
The next example demonstrates how to use the orderby descending clause in a LINQ
query to sort the strings by their first letter, in descending order.
C#Query Expression Syntax Examples
Primary Sort Examples
Primary Ascending Sort
string[] words = [ "the", "quick", "brown", "fox", "jumps"];  
  
IEnumerable< string> query = from word in words  
                            orderby word.Length  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
    quick  
    brown  
    jumps  
*/  
Primary Descending Sort
string[] words = [ "the", "quick", "brown", "fox", "jumps"];  
  
IEnumerable< string> query = from word in words  
                            orderby word.Substring( 0, 1) descending   
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  The following example demonstrates how to use the orderby clause in a LINQ query to
perform a primary and secondary sort of the strings in an array. The strings are sorted
primarily by length and secondarily by the first letter of the string, both in ascending
order.
C#
The next example demonstrates how to use the orderby descending clause in a LINQ
query to perform a primary sort, in ascending order, and a secondary sort, in descending
order. The strings are sorted primarily by length and secondarily by the first letter of the
string.
C#    the  
    quick  
    jumps  
    fox  
    brown  
*/  
Secondary Sort Examples
Secondary Ascending Sort
string[] words = [ "the", "quick", "brown", "fox", "jumps"];  
  
IEnumerable< string> query = from word in words  
                            orderby word.Length, word.Substring( 0, 1)  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    fox  
    the  
    brown  
    jumps  
    quick  
*/  
Secondary Descending SortSystem.Linq
Standard Query Operators Overview (C#)
orderby clause
Order the results of a join clause
How to sort or filter text data by any word or field (LINQ) (C#)string[] words = [ "the", "quick", "brown", "fox", "jumps"];  
  
IEnumerable< string> query = from word in words  
                            orderby word.Length, word.Substring( 0, 1) 
descending   
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
    quick  
    jumps  
    brown  
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
 Provide product feedbackQuantifier operations in LINQ (C#)
Article •06/07/2022
Quantifier operations return a Boolean  value that indicates whether some or all of the
elements in a sequence satisfy a condition.
The following illustration depicts two different quantifier operations on two different
source sequences. The first operation asks if any of the elements are the character 'A'.
The second operation asks if all the elements are the character 'A'. Both methods return
true in this example.
The standard query operator methods that perform quantifier operations are listed in
the following section.
Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
All Determines whether all the elements in a
sequence satisfy a condition.Not applicable. Enumerable.All  
Queryable.All
Any Determines whether any elements in a
sequence satisfy a condition.Not applicable. Enumerable.Any
Queryable.Any
Contains Determines whether a sequence contains
a specified element.Not applicable. Enumerable.Contains  
Queryable.Contains
The following example uses the All to check that all strings are of a specific length.Methods
Query Expression Syntax Examples
AllC#
The following example uses the Any to check that any strings are start with 'o'.
C#class Market 
{ 
    public string Name { get; set; } 
    public string[] Items { get; set; } 
} 
public static void Example() 
{ 
    List<Market> markets = new List<Market>  
    { 
        new Market { Name = "Emily's" , Items = new string[] { "kiwi", 
"cheery" , "banana"  } }, 
        new Market { Name = "Kim's", Items = new string[] { "melon", 
"mango", "olive" } }, 
        new Market { Name = "Adam's" , Items = new string[] { "kiwi", 
"apple", "orange"  } }, 
    }; 
    // Determine which market have all fruit names length equal to 5  
    IEnumerable< string> names = from market in markets  
                                where market.Items.All(item => item.Length  
== 5) 
                                select market.Name;  
    foreach (string name in names) 
    { 
        Console.WriteLine( $"{name} market" ); 
    } 
    // This code produces the following output:  
    // 
    // Kim's market  
} 
Any
class Market 
{ 
    public string Name { get; set; } 
    public string[] Items { get; set; } 
} 
public static void Example() 
{ 
    List<Market> markets = new List<Market>  The following example uses the Contains to check an array have a specific element.
C#    { 
        new Market { Name = "Emily's" , Items = new string[] { "kiwi", 
"cheery" , "banana"  } }, 
        new Market { Name = "Kim's", Items = new string[] { "melon", 
"mango", "olive" } }, 
        new Market { Name = "Adam's" , Items = new string[] { "kiwi", 
"apple", "orange"  } }, 
    }; 
    // Determine which market have any fruit names start with 'o'  
    IEnumerable< string> names = from market in markets  
                                where market.Items.Any(item =>  
item.StartsWith( "o")) 
                                select market.Name;  
    foreach (string name in names) 
    { 
        Console.WriteLine( $"{name} market" ); 
    } 
    // This code produces the following output:  
    // 
    // Kim's market  
    // Adam's market  
} 
Contains
class Market 
{ 
    public string Name { get; set; } 
    public string[] Items { get; set; } 
} 
public static void Example() 
{ 
    List<Market> markets = new List<Market>  
    { 
        new Market { Name = "Emily's" , Items = new string[] { "kiwi", 
"cheery" , "banana"  } }, 
        new Market { Name = "Kim's", Items = new string[] { "melon", 
"mango", "olive" } }, 
        new Market { Name = "Adam's" , Items = new string[] { "kiwi", 
"apple", "orange"  } }, 
    }; 
    // Determine which market contains fruit names equal 'kiwi'  
    IEnumerable< string> names = from market in markets  System.Linq
Standard Query Operators Overview (C#)
Dynamically specify predicate filters at run time
How to query for sentences that contain a specified set of words (LINQ) (C#)                                where market.Items.Contains( "kiwi") 
                                select market.Name;  
    foreach (string name in names) 
    { 
        Console.WriteLine( $"{name} market" ); 
    } 
    // This code produces the following output:  
    // 
    // Emily's market  
    // Adam's market  
} 
See alsoPartitioning data (C#)
Article •12/22/2021
Partitioning in LINQ refers to the operation of dividing an input sequence into two
sections, without rearranging the elements, and then returning one of the sections.
The following illustration shows the results of three different partitioning operations on
a sequence of characters. The first operation returns the first three elements in the
sequence. The second operation skips the first three elements and returns the remaining
elements. The third operation skips the first two elements in the sequence and returns
the next three elements.
The standard query operator methods that partition sequences are listed in the
following section.
Method
namesDescr iption C# quer y
expr ession
syntaxMore infor mation
Skip Skips elements up to a specified position
in a sequence.Not
applicable.Enumerable.Skip  
Queryable.Skip
SkipWhile Skips elements based on a predicate
function until an element does not satisfy
the condition.Not
applicable.Enumerable.SkipWhile  
Queryable.SkipWhile
Take Takes elements up to a specified position
in a sequence.Not
applicable.Enumerable.T ake 
Queryable.T ake
TakeWhile Takes elements based on a predicate
function until an element does not satisfy
the condition.Not
applicable.Enumerable.T akeWhile  
Queryable.T akeWhileOperatorsMethod
namesDescr iption C# quer y
expr ession
syntaxMore infor mation
Chunk Splits the elements of a sequence into
chunks of a specified maximum size.Not
applicable.Enumerable.Chunk  
Queryable.Chunk
The Chunk operator is used to split elements of a sequence based on a given size.
C#
The preceding C# code:
Relies on Enumerable.Range(Int32, Int32)  to generate a sequence of numbers.
Applies the Chunk operator, splitting the sequence into chunks with a max size of
three.Example
int chunkNumber = 1; 
foreach (int[] chunk in Enumerable.Range( 0, 8).Chunk( 3)) 
{ 
    Console.WriteLine( $"Chunk {chunkNumber++} :"); 
    foreach (int item in chunk) 
    { 
        Console.WriteLine( $"    {item}"); 
    } 
    Console.WriteLine();  
} 
// This code produces the following output:  
// Chunk 1:  
//    0 
//    1 
//    2 
// 
//Chunk 2:  
//    3 
//    4 
//    5 
// 
//Chunk 3:  
//    6 
//    7 
See alsoSystem.Linq
Standard Query Operators Overview (C#)Generation Operations (C#)
Article •09/15/2021
Generation refers to creating a new sequence of values.
The standard query operator methods that perform generation are listed in the
following section.
Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
DefaultIfEmpty Replaces an empty collection
with a default valued singleton
collection.Not applicable. Enumerable.DefaultIfEmpty  
Queryable.DefaultIfEmpty
Empty Returns an empty collection. Not applicable. Enumerable.Empty
Range Generates a collection that
contains a sequence of numbers.Not applicable. Enumerable.Range
Repeat Generates a collection that
contains one repeated value.Not applicable. Enumerable.R epeat
System.Linq
Standard Query Operators Overview (C#)Methods
See alsoEquality Operations (C#)
Article •09/15/2021
Two sequences whose corresponding elements are equal and which have the same
number of elements are considered equal.
Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
SequenceEqual Determines whether two
sequences are equal by
comparing elements in a pair-
wise manner.Not
applicable.Enumerable.SequenceEqual  
Queryable.SequenceEqual
System.Linq
Standard Query Operators Overview (C#)
How to compare the contents of two folders (LINQ) (C#)Methods
See alsoElemen t operations (C#)
Article •09/15/2021
Element operations return a single, specific element from a sequence.
The standard query operator methods that perform element operations are listed in the
following section.
Method name Descr iption C# quer y
expr ession
syntaxMore infor mation
ElementAt Returns the element at a
specified index in a
collection.Not
applicable.Enumerable.ElementAt  
Queryable.ElementAt
ElementAtOrDefault Returns the element at a
specified index in a
collection or a default
value if the index is out of
range.Not
applicable.Enumerable.ElementAtOrDefault
Queryable.ElementAtOrDefault
First Returns the first element
of a collection, or the first
element that satisfies a
condition.Not
applicable.Enumerable.First  
Queryable.First
FirstOrDefault Returns the first element
of a collection, or the first
element that satisfies a
condition. R eturns a
default value if no such
element exists.Not
applicable.Enumerable.FirstOrDefault  
Queryable.FirstOrDefault  
Queryable.FirstOrDefault<T Source>
(IQueryable<T Source>)
Last Returns the last element
of a collection, or the last
element that satisfies a
condition.Not
applicable.Enumerable.Last  
Queryable.LastMethodsMethod name Descr iption C# quer y
expr ession
syntaxMore infor mation
LastOrDefault Returns the last element
of a collection, or the last
element that satisfies a
condition. R eturns a
default value if no such
element exists.Not
applicable.Enumerable.LastOrDefault  
Queryable.LastOrDefault
Single Returns the only element
of a collection or the only
element that satisfies a
condition. Throws an
InvalidOperationException
if there is no element or
more than one element to
return.Not
applicable.Enumerable.Single  
Queryable.Single
SingleOrDefault Returns the only element
of a collection or the only
element that satisfies a
condition. R eturns a
default value if there is no
element to return. Throws
an
InvalidOperationException
if there is more than one
element to return.Not
applicable.Enumerable.SingleOrDefault  
Queryable.SingleOrDefault
System.Linq
Standard Query Operators Overview (C#)
How to query for the largest file or files in a directory tree (LINQ) (C#)See alsoConverting Data Types (C#)
Article •09/15/2021
Conversion methods change the type of input objects.
Conversion operations in LINQ queries are useful in a variety of applications. Following
are some examples:
The Enumerable.AsEnumerable  method can be used to hide a type's custom
implementation of a standard query operator.
The Enumerable.OfT ype method can be used to enable non-parameterized
collections for LINQ querying.
The Enumerable.T oArray , Enumerable.T oDictionary , Enumerable.T oList , and
Enumerable.T oLookup  methods can be used to force immediate query execution
instead of deferring it until the query is enumerated.
The following table lists the standard query operator methods that perform data-type
conversions.
The conversion methods in this table whose names start with "As" change the static type
of the source collection but do not enumerate it. The methods whose names start with
"To" enumerate the source collection and put the items into the corresponding
collection type.
Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
AsEnumerable Returns the input typed as
IEnumerable<T> .Not
applicable.Enumerable.AsEnumerable
AsQueryable Converts a (generic) IEnumerable
to a (generic) IQueryable .Not
applicable.Queryable.AsQueryable
Cast Casts the elements of a collection
to a specified type.Use an
explicitly
typed range
variable. For
example:Enumerable.Cast
Queryable.CastMethodsMethod
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
from string
str in words
OfType Filters values, depending on their
ability to be cast to a specified
type.Not
applicable.Enumerable.OfT ype
Queryable.OfT ype
ToArray Converts a collection to an array.
This method forces query
execution.Not
applicable.Enumerable.T oArray
ToDictionary Puts elements into a
Dictionary<TK ey,TValue>  based
on a key selector function. This
method forces query execution.Not
applicable.Enumerable.T oDictionary
ToList Converts a collection to a List<T> .
This method forces query
execution.Not
applicable.Enumerable.T oList
ToLookup Puts elements into a
Lookup<TK ey,TElement>  (a one-
to-many dictionary) based on a
key selector function. This method
forces query execution.Not
applicable.Enumerable.T oLookup
The following code example uses an explicitly typed range variable to cast a type to a
subtype before accessing a member that is available only on the subtype.
C#Query Expression Syntax Example
class Plant
{
    public string Name { get; set; }
}
class CarnivorousPlant  : Plant
{
    public string TrapType { get; set; }
}
static void Cast()
{
    Plant[] plants = System.Linq
Standard Query Operators Overview (C#)
from clause
LINQ Query Expressions
How to query an ArrayList with LINQ (C#)    [
        new CarnivorousPlant { Name = "Venus Fly Trap" , TrapType = "Snap 
Trap" },
        new CarnivorousPlant { Name = "Pitcher Plant" , TrapType = "Pitfall  
Trap" },
        new CarnivorousPlant { Name = "Sundew" , TrapType = "Flypaper Trap"  
},
        new CarnivorousPlant { Name = "Waterwheel Plant" , TrapType = "Snap 
Trap" }
    ];
    var query = from CarnivorousPlant cPlant in plants
                where cPlant.TrapType == "Snap Trap"
                select cPlant;
    foreach (Plant plant in query)
        Console.WriteLine(plant.Name);
    /* This code produces the following output:
        Venus Fly Trap
        Waterwheel Plant
    */
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
 Provide product feedbackConcatenation Operations (C#)
Article •09/15/2021
Concatenation refers to the operation of appending one sequence to another.
The following illustration depicts a concatenation operation on two sequences of
characters.
The standard query operator methods that perform concatenation are listed in the
following section.
Method
NameDescr iption C# Quer y
Expr ession S yntaxMore Infor mation
Concat Concatenates two sequences to form
one sequence.Not applicable. Enumerable.Concat  
Queryable.Concat
System.Linq
Standard Query Operators Overview (C#)
How to combine and compare string collections (LINQ) (C#)Methods
See alsoAggregation operations (C#)
Article •09/15/2021
An aggregation operation computes a single value from a collection of values. An
example of an aggregation operation is calculating the average daily temperature from
a month's worth of daily temperature values.
The following illustration shows the results of two different aggregation operations on a
sequence of numbers. The first operation sums the numbers. The second operation
returns the maximum value in the sequence.
The standard query operator methods that perform aggregation operations are listed in
the following section.
Method
namedescr iption C# quer y
expr ession
syntaxMore infor mation
Aggregate Performs a custom aggregation operation
on the values of a collection.Not
applicable.Enumerable.Aggregate  
Queryable.Aggregate
Average Calculates the average value of a
collection of values.Not
applicable.Enumerable.A verage  
Queryable.A verage
Count Counts the elements in a collection,
optionally only those elements that satisfy
a predicate function.Not
applicable.Enumerable.Count  
Queryable.Count
LongCount Counts the elements in a large collection,
optionally only those elements that satisfy
a predicate function.Not
applicable.Enumerable.LongCount  
Queryable.LongCountMethodsMethod
namedescr iption C# quer y
expr ession
syntaxMore infor mation
Max or
MaxByDetermines the maximum value in a
collection.Not
applicable.Enumerable.Max  
Enumerable.MaxBy  
Queryable.Max  
Queryable.MaxBy
Min or
MinByDetermines the minimum value in a
collection.Not
applicable.Enumerable.Min  
Enumerable.MinBy  
Queryable.Min  
Queryable.MinBy
Sum Calculates the sum of the values in a
collection.Not
applicable.Enumerable.Sum  
Queryable.Sum
System.Linq
Standard Query Operators Overview (C#)
How to compute column values in a CSV text file (LINQ) (C#)
How to query for the largest file or files in a directory tree (LINQ) (C#)
How to query for the total number of bytes in a set of folders (LINQ) (C#)See alsoJoin Operations (C#)
Article •09/15/2021
A join of two data sources is the association of objects in one data source with objects
that share a common attribute in another data source.
Joining is an important operation in queries that target data sources whose relationships
to each other cannot be followed directly. In object-oriented programming, this could
mean a correlation between objects that is not modeled, such as the backwards
direction of a one-way relationship. An example of a one-way relationship is a Customer
class that has a property of type City, but the City class does not have a property that is
a collection of Customer objects. If you have a list of City objects and you want to find
all the customers in each city, you could use a join operation to find them.
The join methods provided in the LINQ framework are Join and GroupJoin . These
methods perform equijoins, or joins that match two data sources based on equality of
their keys. (For comparison, T ransact-SQL supports join operators other than 'equals', for
example the 'less than' operator.) In relational database terms, Join implements an inner
join, a type of join in which only those objects that have a match in the other data set
are returned. The GroupJoin  method has no direct equivalent in relational database
terms, but it implements a superset of inner joins and left outer joins. A left outer join is
a join that returns each element of the first (left) data source, even if it has no correlated
elements in the other data source.
The following illustration shows a conceptual view of two sets and the elements within
those sets that are included in either an inner join or a left outer join.
MethodsMethod
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
Join Joins two sequences based on key
selector functions and extracts pairs of
values.join … in … on
… equals …Enumerable.Join  
Queryable.Join
GroupJoin Joins two sequences based on key
selector functions and groups the
resulting matches for each element.join … in … on
… equals …
into …Enumerable.GroupJoin  
Queryable.GroupJoin
The following example uses the join … in … on … equals … clause to join two
sequences based on specific value:
C#Query expression syntax examples
Join
class Product 
{ 
    public string? Name { get; set; } 
    public int CategoryId { get; set; } 
} 
class Category  
{ 
    public int Id { get; set; } 
    public string? CategoryName { get; set; } 
} 
public static void Example() 
{ 
    List<Product> products = new List<Product>  
    { 
        new Product { Name = "Cola", CategoryId = 0 }, 
        new Product { Name = "Tea", CategoryId = 0 }, 
        new Product { Name = "Apple", CategoryId = 1 }, 
        new Product { Name = "Kiwi", CategoryId = 1 }, 
        new Product { Name = "Carrot" , CategoryId = 2 },
    }; 
    List<Category> categories = new List<Category>  
    { 
        new Category { Id = 0, CategoryName = "Beverage"  }, 
        new Category { Id = 1, CategoryName = "Fruit" }, 
        new Category { Id = 2, CategoryName = "Vegetable"  } The following example uses the join … in … on … equals … into … clause to join two
sequences based on specific value and groups the resulting matches for each element:
C#    }; 
    // Join products and categories based on CategoryId  
    var query = from product in products  
                join category in categories on product.CategoryId equals 
category.Id  
                select new { product.Name, category.CategoryName };  
    foreach (var item in query) 
    { 
        Console.WriteLine( $"{item.Name}  - {item.CategoryName} "); 
    } 
    // This code produces the following output:  
    // 
    // Cola - Beverage  
    // Tea - Beverage  
    // Apple - Fruit  
    // Kiwi - Fruit  
    // Carrot - Vegetable  
} 
GroupJoin
class Product 
{ 
    public string? Name { get; set; } 
    public int CategoryId { get; set; } 
} 
class Category  
{ 
    public int Id { get; set; } 
    public string? CategoryName { get; set; } 
} 
public static void Example() 
{ 
    List<Product> products = new List<Product>  
    { 
        new Product { Name = "Cola", CategoryId = 0 }, 
        new Product { Name = "Tea", CategoryId = 0 }, 
        new Product { Name = "Apple", CategoryId = 1 }, 
        new Product { Name = "Kiwi", CategoryId = 1 }, 
        new Product { Name = "Carrot" , CategoryId = 2 },
    }; System.Linq
Standard Query Operators Overview (C#)
Anonymous T ypes
Formulate Joins and Cross-Product Queries
join clause
Join by using composite keys
How to join content from dissimilar files (LINQ) (C#)
Order the results of a join clause
Perform custom join operations
Perform grouped joins
Perform inner joins    List<Category> categories = new List<Category>  
    { 
        new Category { Id = 0, CategoryName = "Beverage"  }, 
        new Category { Id = 1, CategoryName = "Fruit" }, 
        new Category { Id = 2, CategoryName = "Vegetable"  } 
    }; 
    // Join categories and product based on CategoryId and grouping result  
    var productGroups = from category in categories  
                        join product in products on category.Id equals 
product.CategoryId into productGroup  
                        select productGroup;  
    foreach (IEnumerable<Product> productGroup in productGroups)  
    { 
        Console.WriteLine( "Group"); 
        foreach (Product product in productGroup)  
        {  
            Console.WriteLine( $"{product.Name, 8}"); 
        }  
    } 
    // This code produces the following output:  
    // 
    // Group  
    //     Cola  
    //      Tea  
    // Group  
    //    Apple  
    //     Kiwi  
    // Group  
    //   Carrot  
} 
See alsoPerform left outer joins
How to populate object collections from multiple sources (LINQ) (C#)Perform inner joins
Article •07/27/2023
In relational database terms, an inner join  produces a result set in which each element of
the first collection appears one time for every matching element in the second
collection. If an element in the first collection has no matching elements, it doesn't
appear in the result set. The Join method, which is called by the join clause in C#,
implements an inner join.
This article shows you how to perform four variations of an inner join:
A simple inner join that correlates elements from two data sources based on a
simple key.
An inner join that correlates elements from two data sources based on a composit e
key. A composite key, which is a key that consists of more than one value, enables
you to correlate elements based on more than one property.
A multiple join  in which successive join operations are appended to each other.
An inner join that is implemented by using a group join.
The following example creates two collections that contain objects of two user-defined
types, Person and Pet. The query uses the join clause in C# to match Person objects
with Pet objects whose Owner is that Person. The select clause in C# defines how the７ Note
The examples in this topic use the following data classes:
C#
as well as the Student class from Quer y a collection o f objects .record Person(string FirstName, string LastName );
record Pet(string Name, Person Owner );
record Employee (string FirstName, string LastName, int EmployeeID );
record Cat(string Name, Person Owner ) : Pet(Name, Owner );
record Dog(string Name, Person Owner ) : Pet(Name, Owner );
Example - Simple key joinresulting objects will look. In this example, the resulting objects are anonymous types
that consist of the owner's first name and the pet's name.
C#
You achieve the same results using the Join method syntax:Person magnus = new(FirstName: "Magnus" , LastName: "Hedlund" );
Person terry = new("Terry", "Adams");
Person charlotte = new("Charlotte" , "Weiss");
Person arlene = new("Arlene" , "Huff");
Person rui = new("Rui", "Raposo" );
List<Person> people = new() { magnus, terry, charlotte, arlene, rui };
List<Pet> pets = new()
{
    new(Name: "Barley" , Owner: terry),
    new("Boots", terry),
    new("Whiskers" , charlotte),
    new("Blue Moon" , rui),
    new("Daisy", magnus),
};
// Create a collection of person-pet pairs. Each element in the collection
// is an anonymous type containing both the person's name and their pet's  
name.
var query =
    from person in people
    join pet in pets on person equals pet.Owner
    select new
    {
        OwnerName = person.FirstName,
        PetName = pet.Name
    };
string result = "";
foreach (var ownerAndPet in query)
{
    result += $"\"{ownerAndPet.PetName} \" is owned by 
{ownerAndPet.OwnerName} \r\n";
}
Console.Write(result);
return result;
/* Output:
     "Daisy" is owned by Magnus
     "Barley" is owned by Terry
     "Boots" is owned by Terry
     "Whiskers" is owned by Charlotte
     "Blue Moon" is owned by Rui
*/C#
The Person object whose LastName is "Huff" doesn't appear in the result set because
there's no Pet object that has Pet.Owner equal to that Person.
Instead of correlating elements based on just one property, you can use a composite
key to compare elements based on multiple properties. T o do this, specify the key
selector function for each collection to return an anonymous type that consists of the
properties you want to compare. If you label the properties, they must have the same
label in each key's anonymous type. The properties must also appear in the same order.
The following example uses a list of Employee objects and a list of Student objects to
determine which employees are also students. Both of these types have a FirstName
and a LastName property of type String . The functions that create the join keys from
each list's elements return an anonymous type that consists of the FirstName and
LastName properties of each element. The join operation compares these composite
keys for equality and returns pairs of objects from each list where both the first name
and the last name match.
C#var query =
    people.Join(pets,
                person => person,
                pet => pet.Owner,
                (person, pet) =>
                    new { OwnerName = person.FirstName, PetName = pet.Name  
});
Example - Composite key join
List<Employee> employees = new()
{
    new(FirstName: "Terry", LastName: "Adams", EmployeeID: 522459),
    new("Charlotte" , "Weiss", 204467),
    new("Magnus" , "Hedland" , 866200),
    new("Vernette" , "Price", 437139)
};
List<Student> students = new()
{
    new(FirstName: "Vernette" , LastName: "Price", StudentID: 9562),
    new("Terry", "Earls", 9870),
    new("Terry", "Adams", 9913)
};You can use the Join method, as shown in the following example:
C#
Any number of join operations can be appended to each other to perform a multiple
join. Each join clause in C# correlates a specified data source with the results of the
previous join.// Join the two data sources based on a composite key consisting of first  
and last name,
// to determine which employees are also students.
var query =
    from employee in employees
    join student in students on new
    {
        employee.FirstName,
        employee.LastName
    } equals new
    {
        student.FirstName,
        student.LastName
    }
    select employee.FirstName + " " + employee.LastName;
string result = "";
result += "The following people are both employees and students:\r\n" ;
foreach (string name in query)
{
    result += $"{name}\r\n";
}
Console.Write(result);
return result;
/* Output:
    The following people are both employees and students:
    Terry Adams
    Vernette Price
 */
var query = employees.Join(
     students,
     employee => new {FirstName = employee.FirstName, LastName =  
employee.LastName },
     student => new { FirstName = student.FirstName, student.LastName },
     (employee, student) => $"{employee.FirstName}  {employee.LastName} "
 );
Example - Multip le joinThe following example creates three collections: a list of Person objects, a list of Cat
objects, and a list of Dog objects.
The first join clause in C# matches people and cats based on a Person object matching
Cat.Owner. It returns a sequence of anonymous types that contain the Person object
and Cat.Name.
The second join clause in C# correlates the anonymous types returned by the first join
with Dog objects in the supplied list of dogs, based on a composite key that consists of
the Owner property of type Person, and the first letter of the animal's name. It returns a
sequence of anonymous types that contain the Cat.Name and Dog.Name properties from
each matching pair. Because this is an inner join, only those objects from the first data
source that have a match in the second data source are returned.
C#
Person magnus = new(FirstName: "Magnus" , LastName: "Hedlund" );
Person terry = new("Terry", "Adams");
Person charlotte = new("Charlotte" , "Weiss");
Person arlene = new("Arlene" , "Huff");
Person rui = new("Rui", "Raposo" );
Person phyllis = new("Phyllis" , "Harris" );
List<Person> people = new() { magnus, terry, charlotte, arlene, rui, phyllis  
};
List<Cat> cats = new()
{
    new(Name: "Barley" , Owner: terry),
    new("Boots", terry),
    new("Whiskers" , charlotte),
    new("Blue Moon" , rui),
    new("Daisy", magnus),
};
List<Dog> dogs = new()
{
    new(Name: "Four Wheel Drive" , Owner: phyllis),
    new("Duke", magnus),
    new("Denim", terry),
    new("Wiley", charlotte),
    new("Snoopy" , rui),
    new("Snickers" , arlene),
};
// The first join matches Person and Cat.Owner from the list of people and
// cats, based on a common Person. The second join matches dogs whose names  
start
// with the same letter as the cats that have the same owner.
var query =The equivalent using multiple Join method uses the same approach with the anonymous
type (in the example below it's named commonOwner):
C#    from person in people
    join cat in cats on person equals cat.Owner
    join dog in dogs on new
    {
        Owner = person,
        Letter = cat.Name.Substring( 0, 1)
    } equals new
    {
        dog.Owner,
        Letter = dog.Name.Substring( 0, 1)
    }
    select new
    {
        CatName = cat.Name,
        DogName = dog.Name
    };
string result = "";
foreach (var obj in query)
{
    result += $"The cat \" {obj.CatName} \" shares a house, and the first  
letter of their name, with \" {obj.DogName} \".\r\n" ;
}
Console.Write(result);
return result;
/* Output:
     The cat "Daisy" shares a house, and the first letter of their name,  
with "Duke".
     The cat "Whiskers" shares a house, and the first letter of their name,  
with "Wiley".
 */
var query = people.Join(cats,
        person => person,
        cat => cat.Owner,
        (person, cat) => new { person, cat })
    .Join(dogs,
        commonOwner => new { Owner = commonOwner.person, Letter =  
commonOwner.cat.Name.Substring( 0, 1) },
        dog => new { dog.Owner, Letter = dog.Name.Substring( 0, 1) },
        (commonOwner, dog) => new { CatName = commonOwner.cat.Name, DogName  
= dog.Name });
Example - Inner join by using grouped joinThe following example shows you how to implement an inner join by using a group join.
In query1, the list of Person objects is group-joined to the list of Pet objects based on
the Person matching the Pet.Owner property. The group join creates a collection of
intermediate groups, where each group consists of a Person object and a sequence of
matching Pet objects.
By adding a second from clause to the query, this sequence of sequences is combined
(or flattened) into one longer sequence. The type of the elements of the final sequence
is specified by the select clause. In this example, that type is an anonymous type that
consists of the Person.FirstName and Pet.Name properties for each matching pair.
The result of query1 is equivalent to the result set that would have been obtained by
using the join clause without the into clause to perform an inner join. The query2
variable demonstrates this equivalent query.
C#
Person magnus = new(FirstName: "Magnus" , LastName: "Hedlund" );
Person terry = new("Terry", "Adams");
Person charlotte = new("Charlotte" , "Weiss");
Person arlene = new("Arlene" , "Huff");
List<Person> people = new() { magnus, terry, charlotte, arlene };
List<Pet> pets = new()
{
    new(Name: "Barley" , Owner: terry),
    new("Boots", terry),
    new("Whiskers" , charlotte),
    new("Blue Moon" , terry),
    new("Daisy", magnus),
};
var query1 =
    from person in people
    join pet in pets on person equals pet.Owner into gj
    from subpet in gj
    select new
    {
        OwnerName = person.FirstName,
        PetName = subpet.Name
    };
string result = "";
result += "Inner join using GroupJoin():\r\n" ;
foreach (var v in query1)
{
    result += $"{v.OwnerName}  - {v.PetName} \r\n";
}The same results can be achieved using GroupJoin  method, as follows:
C#
This approach requires chaining the query results with SelectMany  to create the final list
of Owner - P et relation based on the results of group join. T o avoid chaining, the single
Join method can be used as presented here:
C#var query2 =
    from person in people
    join pet in pets on person equals pet.Owner
    select new
    {
        OwnerName = person.FirstName,
        PetName = pet.Name
    };
result += "\r\nThe equivalent operation using Join():\r\n" ;
foreach (var v in query2)
{
    result += $"{v.OwnerName}  - {v.PetName} \r\n";
}
Console.Write(result);
return result;
/* Output:
    Inner join using GroupJoin():
    Magnus - Daisy
    Terry - Barley
    Terry - Boots
    Terry - Blue Moon
    Charlotte - Whiskers
    The equivalent operation using Join():
    Magnus - Daisy
    Terry - Barley
    Terry - Boots
    Terry - Blue Moon
    Charlotte - Whiskers
*/
var query1 = people.GroupJoin(pets,
        person => person,
        pet => pet.Owner,
        (person, gj) => new { person, gj })
    .SelectMany(pet => pet.gj,
        (groupJoinPet, subpet) => new { OwnerName =  
groupJoinPet.person.FirstName, PetName = subpet.Name });Join
GroupJoin
Perform grouped joins
Perform left outer joins
Anonymous typesvar query2 = people.Join(pets,
    person => person,
    pet => pet.Owner,
    (person, pet) => new { OwnerName = person.FirstName, PetName = pet.Name  
});
See alsoPerform grouped joins
Article •11/14/2023
The group join is useful for producing hierarchical data structures. It pairs each element
from the first collection with a set of correlated elements from the second collection.
For example, a class or a relational database table named Student might contain two
fields: Id and Name. A second class or relational database table named Course might
contain two fields: StudentId and CourseTitle. A group join of these two data sources,
based on matching Student.Id and Course.StudentId, would group each Student with
a collection of Course objects (which might be empty).
The first example in this article shows you how to perform a group join. The second
example shows you how to use a group join to create XML elements.７ Note
Each element of the first collection appears in the result set of a group join
regardless of whether correlated elements are found in the second collection. In the
case where no correlated elements are found, the sequence of correlated elements
for that element is empty. The result selector therefore has access to every element
of the first collection. This differs from the result selector in a non-group join, which
cannot access elements from the first collection that have no match in the second
collection.
２ Warning
Enumerable.Gr oupJoin  has no direct equivalent in traditional relational database
terms. However, this method does implement a superset of inner joins and left
outer joins. Both of these operations can be written in terms of a grouped join. For
more information, see Join Operations  and Entity Framew ork Cor e, Gr oupJoin .
７ Note
The examples in this topic use the Person and Pet data classes from Perform inner
joins .The following example performs a group join of objects of type Person and Pet based
on the Person matching the Pet.Owner property. Unlike a non-group join, which would
produce a pair of elements for each match, the group join produces only one resulting
object for each element of the first collection, which in this example is a Person object.
The corresponding elements from the second collection, which in this example are Pet
objects, are grouped into a collection. Finally, the result selector function creates an
anonymous type for each match that consists of Person.FirstName and a collection of
Pet objects.
C#Example - Group join
Person magnus = new(FirstName: "Magnus" , LastName: "Hedlund" );
Person terry = new("Terry", "Adams");
Person charlotte = new("Charlotte" , "Weiss");
Person arlene = new("Arlene" , "Huff");
List<Person> people = new() { magnus, terry, charlotte, arlene };
List<Pet> pets = new()
{
    new(Name: "Barley" , Owner: terry),
    new("Boots", terry),
    new("Whiskers" , charlotte),
    new("Blue Moon" , terry),
    new("Daisy", magnus),
};
var query =
    from person in people
    join pet in pets on person equals pet.Owner into gj
    select new
    {
        OwnerName = person.FirstName,
        Pets = gj
    };
foreach (var v in query)
{
    // Output the owner's name.
    Console.WriteLine( $"{v.OwnerName} :");
    // Output each of the owner's pet's names.
    foreach (var pet in v.Pets)
    {
        Console.WriteLine( $"  {pet.Name} ");
    }
}In the above example, query variable contains the query that creates a list where each
element is an anonymous type that contains the person's first name and a collection of
pets that are owned by them.
Group joins are ideal for creating XML by using LINQ to XML. The following example is
similar to the previous example except that instead of creating anonymous types, the
result selector function creates XML elements that represent the joined objects.
C#/* Output:
     Magnus:
       Daisy
     Terry:
       Barley
       Boots
       Blue Moon
     Charlotte:
       Whiskers
     Arlene:
 */
Example - Group join to create XML
// using System.Xml.Linq;
Person magnus = new(FirstName: "Magnus" , LastName: "Hedlund" );
Person terry = new("Terry", "Adams");
Person charlotte = new("Charlotte" , "Weiss");
Person arlene = new("Arlene" , "Huff");
List<Person> people = new() { magnus, terry, charlotte, arlene };
List<Pet> pets = new()
{
    new(Name: "Barley" , Owner: terry),
    new("Boots", terry),
    new("Whiskers" , charlotte),
    new("Blue Moon" , terry),
    new("Daisy", magnus),
};
XElement ownersAndPets = new("PetOwners" ,
    from person in people
    join pet in pets on person equals pet.Owner into gj
    select new XElement ("Person" ,
        new XAttribute( "FirstName" , person.FirstName ),
        new XAttribute ("LastName" , person.LastName ),
        from subpet in gj
        select new XElement ("Pet", subpet.Name )Join
GroupJoin
Perform inner joins
Perform left outer joins
Anonymous types    )
);
Console.WriteLine(ownersAndPets);
/* Output:
     <PetOwners>
       <Person FirstName="Magnus" LastName="Hedlund">
         <Pet>Daisy</Pet>
       </Person>
       <Person FirstName="Terry" LastName="Adams">
         <Pet>Barley</Pet>
         <Pet>Boots</Pet>
         <Pet>Blue Moon</Pet>
       </Person>
       <Person FirstName="Charlotte" LastName="Weiss">
         <Pet>Whiskers</Pet>
       </Person>
       <Person FirstName="Arlene" LastName="Huff" />
     </PetOwners>
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
 Provide product feedbackPerform left outer joins
Article •03/11/2022
A left outer join is a join in which each element of the first collection is returned,
regardless of whether it has any correlated elements in the second collection. Y ou can
use LINQ to perform a left outer join by calling the DefaultIfEmpty  method on the
results of a group join.
The following example demonstrates how to use the DefaultIfEmpty  method on the
results of a group join to perform a left outer join.
The first step in producing a left outer join of two collections is to perform an inner join
by using a group join. (See Perform inner joins  for an explanation of this process.) In this
example, the list of Person objects is inner-joined to the list of Pet objects based on a
Person object that matches Pet.Owner.
The second step is to include each element of the first (left) collection in the result set
even if that element has no matches in the right collection. This is accomplished by
calling DefaultIfEmpty  on each sequence of matching elements from the group join. In
this example, DefaultIfEmpty  is called on each sequence of matching Pet objects. The
method returns a collection that contains a single, default value if the sequence of
matching Pet objects is empty for any Person object, thereby ensuring that each
Person object is represented in the result collection.
C#７ Note
The example in this topic uses the Pet and Person data classes from Perform inner
joins .
Example
７ Note
The default value for a reference type is null; therefore, the example checks for a
null reference before accessing each element of each Pet collection.Join
GroupJoin
Perform inner joins
Perform grouped joins
Anonymous typesPerson magnus = new("Magnus" , "Hedlund" ); 
Person terry = new("Terry", "Adams"); 
Person charlotte = new("Charlotte" , "Weiss"); 
Person arlene = new("Arlene" , "Huff"); 
Pet barley = new("Barley" , terry);  
Pet boots = new("Boots", terry);  
Pet whiskers = new("Whiskers" , charlotte);  
Pet bluemoon = new("Blue Moon" , terry);  
Pet daisy = new("Daisy", magnus);  
// Create two lists.  
List<Person> people = new() { magnus, terry, charlotte, arlene };  
List<Pet> pets = new() { barley, boots, whiskers, bluemoon, daisy };  
var query =  
    from person in people 
    join pet in pets on person equals pet.Owner into gj 
    from subpet in gj.DefaultIfEmpty()  
    select new 
    { 
        person.FirstName,  
        PetName = subpet?.Name ?? string.Empty 
    }; 
foreach (var v in query) 
{ 
    Console.WriteLine( $"{v.FirstName + ":",-15}{v.PetName} "); 
} 
record class Person(string FirstName, string LastName ); 
record class Pet(string Name, Person Owner ); 
// This code produces the following output:  
// 
// Magnus:        Daisy  
// Terry:         Barley  
// Terry:         Boots  
// Terry:         Blue Moon  
// Charlotte:     Whiskers  
// Arlene:  
See alsoOrder the results of a join clause
Article •02/18/2022
This example shows how to order the results of a join operation. Note that the ordering
is performed after the join. Although you can use an orderby clause with one or more of
the source sequences before the join, generally we do not recommend it. Some LINQ
providers might not preserve that ordering after the join.
This query creates a group join, and then sorts the groups based on the category
element, which is still in scope. Inside the anonymous type initializer, a sub-query orders
all the matching elements from the products sequence.
C#７ Note
The example in this topic uses the following data classes:
C#
record Product(string Name, int CategoryID ); 
record Category (string Name, int ID); 
Example
List<Category> categories = new() 
{ 
    new(Name: "Beverages" , ID: 001), 
    new("Condiments" , 002), 
    new("Vegetables" , 003), 
    new("Grains" , 004), 
    new("Fruit", 005) 
}; 
List<Product> products = new() 
{ 
    new(Name: "Cola", CategoryID: 001), 
    new("Tea", 001), 
    new("Mustard" , 002), 
    new("Pickles" , 002), 
    new("Carrots" , 003), 
    new("Bok Choy" , 003), 
    new("Peaches" , 005), 
    new("Melons" , 005), Language Integrated Query (LINQ)
orderby clause
join clause}; 
var groupJoinQuery2 =  
    from category in categories  
    join prod in products on category.ID equals prod.CategoryID into 
prodGroup  
    orderby category.Name  
    select new 
    { 
        Category = category.Name,
        Products =  
            from prod2 in prodGroup  
            orderby prod2.Name  
            select prod2 
    }; 
foreach (var productGroup in groupJoinQuery2)  
{ 
    Console.WriteLine(productGroup.Category);  
    foreach (var prodItem in productGroup.Products)  
    { 
        Console.WriteLine( $"  {prodItem.Name, -10} {prodItem.CategoryID} "); 
    } 
} 
/* Output:  
    Beverages  
      Cola       1  
      Tea        1  
    Condiments  
      Mustard    2  
      Pickles    2  
    Fruit  
      Melons     5  
      Peaches    5  
    Grains  
    Vegetables  
      Bok Choy   3  
      Carrots    3  
 */ 
See alsoJoin by using composite keys
Article •09/15/2021
This example shows how to perform join operations in which you want to use more than
one key to define a match. This is accomplished by using a composite key. Y ou create a
composite key as an anonymous type or named typed with the values that you want to
compare. If the query variable will be passed across method boundaries, use a named
type that overrides Equals  and GetHashCode  for the key. The names of the properties,
and the order in which they occur, must be identical in each key.
The following example demonstrates how to use a composite key to join data from
three tables:
C#
Type inference on composite keys depends on the names of the properties in the keys,
and the order in which they occur. If the properties in the source sequences don't have
the same names, you must assign new names in the keys. For example, if the Orders
table and OrderDetails table each used different names for their columns, you could
create composite keys by assigning identical names in the anonymous types:
C#
Composite keys can be also used in a group clause.
Language Integrated Query (LINQ)Example
var query = from o in db.Orders  
    from p in db.Products  
    join d in db.OrderDetails  
        on new {o.OrderID, p.ProductID} equals new {d.OrderID, d.ProductID}  
into details  
        from d in details  
        select new {o.OrderID, p.ProductID, d.UnitPrice};  
join...on new {Name = o.CustomerName, ID = o.CustID} equals 
    new {Name = d.CustName, ID = d.CustID }  
See alsojoin clause
group clausePerform cu stom join operations
Article •11/14/2023
This example shows how to perform join operations that aren't possible with the join
clause. In a query expression, the join clause is limited to, and optimized for, equijoins,
which are by far the most common type of join operation. When performing an equijoin,
you will probably always get the best performance by using the join clause.
However, the join clause cannot be used in the following cases:
When the join is predicated on an expression of inequality (a non-equijoin).
When the join is predicated on more than one expression of equality or inequality.
When you have to introduce a temporary range variable for the right side (inner)
sequence before the join operation.
To perform joins that aren't equijoins, you can use multiple from clauses to introduce
each data source independently. Y ou then apply a predicate expression in a where
clause to the range variable for each source. The expression also can take the form of a
method call.
This query shows a simple cross join. Cross joins must be used with caution because
they can produce very large result sets. However, they can be useful in some scenarios
for creating source sequences against which additional queries are run.
C#７ Note
Don't confuse this kind of custom join operation with the use of multiple from
clauses to access inner collections. For more information, see join clause .
Cross-join
７ Note
This example and the one after use the Product and Category definitions from
Order the r esults o f a join clause .List<Category> categories = new()
{
    new(Name: "Beverages" , ID: 001),
    new("Condiments" , 002),
    new("Vegetables" , 003)
};
List<Product> products = new()
{
    new(Name: "Tea", CategoryID: 001),
    new("Mustard" , 002),
    new("Pickles" , 002),
    new("Carrots" , 003),
    new("Bok Choy" , 003),
    new("Peaches" , 005),
    new("Melons" , 005),
    new("Ice Cream" , 007),
    new("Mackerel" , 012)
};
var crossJoinQuery =
    from c in categories
    from p in products
    select new
    {
        c.ID,
        p.Name
    };
Console.WriteLine( "Cross Join Query:" );
foreach (var v in crossJoinQuery)
{
    Console.WriteLine( $"{v.ID,-5}{v.Name} ");
}
/* Output:
    Cross Join Query:
    1    Tea
    1    Mustard
    1    Pickles
    1    Carrots
    1    Bok Choy
    1    Peaches
    1    Melons
    1    Ice Cream
    1    Mackerel
    2    Tea
    2    Mustard
    2    Pickles
    2    Carrots
    2    Bok Choy
    2    Peaches
    2    Melons
    2    Ice Cream
    2    MackerelThis query produces a sequence of all the products whose category ID is listed in the
category list on the left side. Note the use of the let clause and the Contains method
to create a temporary array. It also is possible to create the array before the query and
eliminate the first from clause.
C#    3    Tea
    3    Mustard
    3    Pickles
    3    Carrots
    3    Bok Choy
    3    Peaches
    3    Melons
    3    Ice Cream
    3    Mackerel
*/
Non-equijoin
var nonEquijoinQuery =
    from p in products
    let catIds =
        from c in categories
        select c.ID
    where catIds.Contains(p.CategoryID) == true
    select new
    {
        Product = p.Name,
        p.CategoryID
    };
Console.WriteLine( "Non-equijoin query:" );
foreach (var v in nonEquijoinQuery)
{
    Console.WriteLine( $"{v.CategoryID, -5}{v.Product} ");
}
/* Output:
    Non-equijoin query:
    1    Tea
    2    Mustard
    2    Pickles
    3    Carrots
    3    Bok Choy
*/
Merge CSV filesIn the following example, the query must join two sequences based on matching keys
that, in the case of the inner (right side) sequence, cannot be obtained prior to the join
clause itself. If this join were performed with a join clause, then the Split method
would have to be called for each element. The use of multiple from clauses enables the
query to avoid the overhead of the repeated method call. However, since join is
optimized, in this particular case it might still be faster than using multiple from clauses.
The results will vary depending primarily on how expensive the method call is.
C#
string[] names = File.ReadAllLines( @"csv/names.csv" );
string[] scores = File.ReadAllLines( @"csv/scores.csv" );
IEnumerable<Student> queryNamesScores =
    // Split each line in the data files into an array of strings.
    from name in names
    let x = name.Split( ',')
    from score in scores
    let s = score.Split( ',')
    // Look for matching IDs from the two data files.
    where x[2] == s[0]
    // If the IDs match, build a Student object.
    select new Student(
        FirstName: x[ 0],
        LastName: x[ 1],
        StudentID: int.Parse(x[ 2]),
        ExamScores: (
            from scoreAsText in s.Skip( 1)
            select int.Parse(scoreAsText )
        ).ToList()
    );
List<Student> students = queryNamesScores.ToList();
foreach (var student in students)
{
    Console.WriteLine( $"The average score of {student.FirstName}  
{student.LastName}  is {student.ExamScores.Average()} .");
}
/* Output:
    The average score of Omelchenko Svetlana is 82.5.
    The average score of O'Donnell Claire is 72.25.
    The average score of Mortensen Sven is 84.5.
    The average score of Garcia Cesar is 88.25.
    The average score of Garcia Debra is 67.
    The average score of Fakhouri Fadi is 92.25.
    The average score of Feng Hanying is 88.
    The average score of Garcia Hugo is 85.75.
    The average score of Tucker Lance is 81.75.
    The average score of Adams Terry is 85.25.Note that queryNamesScores, containing the merged data sources, in the above example
is using a named type. Y ou could use var instead of an explicit type for the query.
Also, the students variable is optional to create. This good practice of storing the newly
created Student objects in memory allows for faster access in future queries.
Language Integrated Query (LINQ)
join clause
Order the results of a join clause    The average score of Zabokritski Eugene is 83.
    The average score of Tucker Michael is 92.
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
 Provide product feedbackGrouping Data (C#)
Article •09/15/2021
Grouping refers to the operation of putting data into groups so that the elements in
each group share a common attribute.
The following illustration shows the results of grouping a sequence of characters. The
key for each group is the character.
The standard query operator methods that group data elements are listed in the
following section.
Method
NameDescr iption C# Quer y
Expr ession
SyntaxMore Infor mation
GroupBy Groups elements that share a common
attribute. Each group is represented by an
IGrouping<TK ey,TElement>  object.group … by
-or-
group … by …
into …Enumerable.GroupBy
Queryable.GroupBy
ToLookup Inserts elements into a
Lookup<TK ey,TElement>  (a one-to-many
dictionary) based on a key selector
function.Not
applicable.Enumerable.T oLookupMethods
Query Expression Syntax ExampleThe following code example uses the group by clause to group integers in a list
according to whether they are even or odd.
C#
System.Linq
Standard Query Operators Overview (C#)
group clause
Create a nested group
How to group files by extension (LINQ) (C#)
Group query results
Perform a subquery on a grouping operation
How to split a file into many files by using groups (LINQ) (C#)List<int> numbers = [ 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208];  
  
IEnumerable<IGrouping< int, int>> query = from number in numbers  
                                         group number by number % 2;  
  
foreach (var group in query)  
{  
    Console.WriteLine( group.Key == 0 ? "\nEven numbers:"  : "\nOdd 
numbers:" );  
    foreach (int i in group)  
        Console.WriteLine(i);  
}  
  
/* This code produces the following output:  
  
    Odd numbers:  
    35  
    3987  
    199  
    329  
  
    Even numbers:  
    44  
    200  
    84  
    4  
    446  
    208  
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
 Provide product feedbackGroup query results
Article •11/14/2023
Grouping is one of the most powerful capabilities of LINQ. The following examples show
how to group data in various ways:
By a single property.
By the first letter of a string property.
By a computed numeric range.
By Boolean predicate or other expression.
By a compound key.
In addition, the last two queries project their results into a new anonymous type that
contains only the student's first and last name. For more information, see the group
clause .
The following example shows how to group source elements by using a single property
of the element as the group key. In this case the key is a string, the student's last name.
It is also possible to use a substring for the key; see the next example . The grouping
operation uses the default equality comparer for the type.
C#７ Note
The examples in this topic use the Student class and students list from the sample
code in Quer y a collection o f objects .
Group by single property example
// Variable groupByLastNamesQuery is an IEnumerable<IGrouping<string,
// DataClass.Student>>.
var groupByLastNamesQuery =
    from student in students
    group student by student.LastName into newGroup
    orderby newGroup.Key
    select newGroup;
foreach (var nameGroup in groupByLastNamesQuery)
{The following example shows how to group source elements by using something other
than a property of the object for the group key. In this example, the key is the first letter
of the student's last name.
C#    Console.WriteLine( $"Key: {nameGroup.Key} ");
    foreach (var student in nameGroup)
    {
        Console.WriteLine( $"\t{student.LastName} , {student.FirstName} ");
    }
}
/* Output:
    Key: Adams
            Adams, Terry
    Key: Fakhouri
            Fakhouri, Fadi
    Key: Feng
            Feng, Hanying
    Key: Garcia
            Garcia, Cesar
            Garcia, Debra
            Garcia, Hugo
    Key: Mortensen
            Mortensen, Sven
    Key: O'Donnell
            O'Donnell, Claire
    Key: Omelchenko
            Omelchenko, Svetlana
    Key: Tucker
            Tucker, Lance
            Tucker, Michael
    Key: Zabokritski
            Zabokritski, Eugene
*/
Group by value example
var groupByFirstLetterQuery =
    from student in students
    group student by student.LastName[ 0];
foreach (var studentGroup in groupByFirstLetterQuery)
{
    Console.WriteLine( $"Key: {studentGroup.Key} ");
    foreach (var student in studentGroup)
    {
        Console.WriteLine( $"\t{student.LastName} , {student.FirstName} ");
    }
}Note that nested foreach is required to access group items.
The following example shows how to group source elements by using a numeric range
as a group key. The query then projects the results into an anonymous type that
contains only the first and last name and the percentile range to which the student
belongs. An anonymous type is used because it is not necessary to use the complete
Student object to display the results. GetPercentile is a helper function that calculates a
percentile based on the student's average score. The method returns an integer
between 0 and 10.
C#/* Output:
    Key: A
            Adams, Terry
    Key: F
            Fakhouri, Fadi
            Feng, Hanying
    Key: G
            Garcia, Cesar
            Garcia, Debra
            Garcia, Hugo
    Key: M
            Mortensen, Sven
    Key: O
            O'Donnell, Claire
            Omelchenko, Svetlana
    Key: T
            Tucker, Lance
            Tucker, Michael
    Key: Z
            Zabokritski, Eugene
*/
Group by a range example
int GetPercentile (Student s )
{
    double avg = s.ExamScores.Average();
    return avg > 0 ? (int)avg / 10 : 0;
}
var groupByPercentileQuery =
    from student in students
    let percentile = GetPercentile(student)
    group new
    {
        student.FirstName,Note that nested foreach required to iterate over groups and group items.
The following example shows how to group source elements by using a Boolean
comparison expression. In this example, the Boolean expression tests whether a
student's average exam score is greater than 75. As in previous examples, the results are
projected into an anonymous type because the complete source element is not needed.
Note that the properties in the anonymous type become properties on the Key member
and can be accessed by name when the query is executed.
C#        student.LastName
    } by percentile into percentGroup
    orderby percentGroup.Key
    select percentGroup;
foreach (var studentGroup in groupByPercentileQuery)
{
    Console.WriteLine( $"Key: {studentGroup.Key * 10}");
    foreach (var item in studentGroup)
    {
        Console.WriteLine( $"\t{item.LastName} , {item.FirstName} ");
    }
}
/* Output:
    Key: 60
            Garcia, Debra
    Key: 70
            O'Donnell, Claire
    Key: 80
            Adams, Terry
            Feng, Hanying
            Garcia, Cesar
            Garcia, Hugo
            Mortensen, Sven
            Omelchenko, Svetlana
            Tucker, Lance
            Zabokritski, Eugene
    Key: 90
            Fakhouri, Fadi
            Tucker, Michael
*/
Group by comparison example
var groupByHighAverageQuery =
    from student in students
    group newThe following example shows how to use an anonymous type to encapsulate a key that
contains multiple values. In this example, the first key value is the first letter of the
student's last name. The second key value is a Boolean that specifies whether the
student scored over 85 on the first exam. Y ou can order the groups by any property in
the key.
C#    {
        student.FirstName,
        student.LastName
    } by student.ExamScores.Average() > 75 into studentGroup
    select studentGroup;
foreach (var studentGroup in groupByHighAverageQuery)
{
    Console.WriteLine( $"Key: {studentGroup.Key} ");
    foreach (var student in studentGroup)
    {
        Console.WriteLine( $"\t{student.FirstName}  {student.LastName} ");
    }
}
/* Output:
    Key: True
            Terry Adams
            Fadi Fakhouri
            Hanying Feng
            Cesar Garcia
            Hugo Garcia
            Sven Mortensen
            Svetlana Omelchenko
            Lance Tucker
            Michael Tucker
            Eugene Zabokritski
    Key: False
            Debra Garcia
            Claire O'Donnell
*/
Group by anonymous type
var groupByCompoundKey =
    from student in students
    group student by new
    {
        FirstLetterOfLastName = student.LastName[ 0],
        IsScoreOver85 = student.ExamScores[ 0] > 85
    } into studentGroup
    orderby studentGroup.Key.FirstLetterOfLastNameGroupBy
IGrouping<TK ey,TElement>
Language Integrated Query (LINQ)
group clause
Anonymous T ypes
Perform a Subquery on a Grouping Operation
Create a Nested Group
Grouping Data    select studentGroup;
foreach (var scoreGroup in groupByCompoundKey)
{
    string s = scoreGroup.Key.IsScoreOver85 == true ? "more than 85"  : "less 
than 85" ;
    Console.WriteLine( $"Name starts with 
{scoreGroup.Key.FirstLetterOfLastName}  who scored {s}");
    foreach (var item in scoreGroup)
    {
        Console.WriteLine( $"\t{item.FirstName}  {item.LastName} ");
    }
}
/* Output:
    Name starts with A who scored more than 85
            Terry Adams
    Name starts with F who scored more than 85
            Fadi Fakhouri
            Hanying Feng
    Name starts with G who scored more than 85
            Cesar Garcia
            Hugo Garcia
    Name starts with G who scored less than 85
            Debra Garcia
    Name starts with M who scored more than 85
            Sven Mortensen
    Name starts with O who scored less than 85
            Claire O'Donnell
    Name starts with O who scored more than 85
            Svetlana Omelchenko
    Name starts with T who scored less than 85
            Lance Tucker
    Name starts with T who scored more than 85
            Michael Tucker
    Name starts with Z who scored more than 85
            Eugene Zabokritski
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
 Provide product feedbackCreate a nested group
Article •11/14/2023
The following example shows how to create nested groups in a LINQ query expression.
Each group that is created according to student year or grade level is then further
subdivided into groups based on the individuals' names.
C#Example
７ Note
The example in this topic uses the Student class and students list from the sample
code in Quer y a collection o f objects .
var nestedGroupsQuery =
    from student in students
    group student by student. Year into newGroup1
    from newGroup2 in (
        from student in newGroup1
        group student by student.LastName
    )
    group newGroup2 by newGroup1.Key ;
foreach (var outerGroup in nestedGroupsQuery)
{
    Console.WriteLine( $"DataClass.Student Level = {outerGroup.Key} ");
    foreach (var innerGroup in outerGroup)
    {
        Console.WriteLine( $"\tNames that begin with: {innerGroup.Key} ");
        foreach (var innerGroupElement in innerGroup)
        {
            Console.WriteLine( $"\t\t{innerGroupElement.LastName}  
{innerGroupElement.FirstName} ");
        }
    }
}
/* Output:
    DataClass.Student Level = SecondYear
            Names that begin with: Adams
                    Adams Terry
            Names that begin with: Garcia
                    Garcia Hugo
            Names that begin with: Omelchenko
                    Omelchenko SvetlanaNote that three nested foreach loops are required to iterate over the inner elements of
a nested group.
(Hover the mouse cursor over the iteration variables, outerGroup, innerGroup and
innerGroupElement to see their actual type.)
Language Integrated Query (LINQ)    DataClass.Student Level = ThirdYear
            Names that begin with: Fakhouri
                    Fakhouri Fadi
            Names that begin with: Garcia
                    Garcia Debra
            Names that begin with: Tucker
                    Tucker Lance
    DataClass.Student Level = FirstYear
            Names that begin with: Feng
                    Feng Hanying
            Names that begin with: Mortensen
                    Mortensen Sven
            Names that begin with: Tucker
                    Tucker Michael
    DataClass.Student Level = FourthYear
            Names that begin with: Garcia
                    Garcia Cesar
            Names that begin with: O'Donnell
                    O'Donnell Claire
            Names that begin with: Zabokritski
                    Zabokritski Eugene
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
 Provide product feedbackPerform a subquery on a grouping
operation
Article •02/18/2022
This article shows two different ways to create a query that orders the source data into
groups, and then performs a subquery over each group individually. The basic technique
in each example is to group the source elements by using a continuation  named
newGroup, and then generating a new subquery against newGroup. This subquery is run
against each new group that is created by the outer query. Note that in this particular
example the final output is not a group, but a flat sequence of anonymous types.
For more information about how to group, see group clause .
For more information about continuations, see into. The following example uses an in-
memory data structure as the data source, but the same principles apply for any kind of
LINQ data source.
C#Example
７ Note
The examples in this topic use the Student class and students list from the sample
code in Quer y a collection o f objects .
var queryGroupMax =  
    from student in students  
    group student by student.Year into studentGroup  
    select new 
    { 
        Level = studentGroup.Key,
        HighestScore = (  
            from student2 in studentGroup  
            select student2.ExamScores.Average()  
        ).Max()  
    }; 
int count = queryGroupMax.Count();  
Console.WriteLine( $"Number of groups = {count}"); 
foreach (var item in queryGroupMax)  
{ The query in the snippet above can also be written using method syntax. The following
code snippet has a semantically equivalent query written using method syntax.
C#
Language Integrated Query (LINQ)    Console.WriteLine( $"  {item.Level}  Highest Score= {item.HighestScore} "); 
} 
var queryGroupMax =  
    students  
        .GroupBy(student => student.Year)  
        .Select(studentGroup => new 
        {  
            Level = studentGroup.Key,  
            HighestScore = studentGroup.Select(student2 =>  
student2.ExamScores.Average()).Max()  
        });  
int count = queryGroupMax.Count();  
Console.WriteLine( $"Number of groups = {count}"); 
foreach (var item in queryGroupMax)  
{ 
    Console.WriteLine( $"  {item.Level}  Highest Score= {item.HighestScore} "); 
} 
See alsoGroup results by contiguous keys
Article •11/14/2023
The following example shows how to group elements into chunks that represent
subsequences of contiguous keys. For example, assume that you are given the following
sequence of key-value pairs:
Key Value
A We
A think
A that
B Linq
C is
A really
B cool
B !
The following groups will be created in this order:
1. We, think, that
2. Linq
3. is
4. really
5. cool, !
The solution is implemented as an extension method that is thread-safe and that returns
its results in a streaming manner. In other words, it produces its groups as it moves
through the source sequence. Unlike the group or orderby operators, it can begin
returning groups to the caller before all of the sequence has been read.
Thread-safety is accomplished by making a copy of each group or chunk as the source
sequence is iterated, as explained in the source code comments. If the source sequence
has a large sequence of contiguous items, the common language runtime may throw an
OutOfMemoryException .
ExampleThe following example shows both the extension method and the client code that uses
it:
C#
C#public static class ChunkExtensions
{
    public static IEnumerable<IGrouping<TKey, TSource>> ChunkBy<TSource,  
TKey>(
            this IEnumerable<TSource> source,
            Func<TSource, TKey> keySelector) =>
                source.ChunkBy(keySelector, EqualityComparer<TKey>.Default);
    public static IEnumerable<IGrouping<TKey, TSource>> ChunkBy<TSource,  
TKey>(
            this IEnumerable<TSource> source,
            Func<TSource, TKey> keySelector,
            IEqualityComparer<TKey> comparer)
    {
        // Flag to signal end of source sequence.
        const bool noMoreSourceElements = true;
        // Auto-generated iterator for the source array.
        IEnumerator<TSource>? enumerator = source.GetEnumerator();
        // Move to the first element in the source sequence.
        if (!enumerator.MoveNext())
        {
            yield break;        // source collection is empty
        }
        while (true)
        {
            var key = keySelector(enumerator.Current);
            Chunk<TKey, TSource> current = new(key, enumerator, value => 
comparer.Equals(key, keySelector( value)));
            yield return current;
            if (current.CopyAllChunkElements() == noMoreSourceElements)
            {
                yield break;
            }
        }
    }
}
public static class GroupByContiguousKeys
{In the presented code, of ChunkExtensions class implementation, the while(true), loop
in the ChunkBy method, iterates through source sequence and create a copy of each
Chunk. On each pass, the iterator advances to the first element of the next "Chunk"
(The chunk is represented by Chunk  class.)
in the source sequence. This loop corresponds to the outer foreach loop that executes
the query. What happens in that loop is:
1. Get the key for the current Chunk, by assigning it to key variable: var key =
keySelector(enumerator.Current);. The source iterator will churn through the
source sequence until it finds an element with a key that doesn't match.
2. Make a new Chunk (group) object, and store it in current variable, that initially has
one GroupItem, which is a copy of the current source element.    // The source sequence.
    static readonly  KeyValuePair< string, string>[] list = [
        new("A", "We"),
        new("A", "think"),
        new("A", "that"),
        new("B", "LINQ"),
        new("C", "is"),
        new("A", "really" ),
        new("B", "cool"),
        new("B", "!")
    ];
    // Query variable declared as class member to be available
    // on different threads.
    static readonly  IEnumerable<IGrouping< string, KeyValuePair< string, 
string>>> query =
        list.ChunkBy(p => p.Key);
    public static void GroupByContiguousKeys1 ()
    {
        // ChunkBy returns IGrouping objects, therefore a nested
        // foreach loop is required to access the elements in each "chunk".
        foreach (var item in query)
        {
            Console.WriteLine( $"Group key = {item.Key} ");
            foreach (var inner in item)
            {
                Console.WriteLine( $"\t{inner.Value} ");
            }
        }
    }
}
ChunkExtensions class3. Return that Chunk. A Chunk is an IGrouping<TKey,TSource>, which is the return
value of the ChunkBy  method. At this point the Chunk only has the first element in
its source sequence. The remaining elements will be returned only when the client
code foreach's over this chunk. See Chunk.GetEnumerator for more info.
4. Check to see whether
(a) the chunk has made a copy of all its source elements or
(b) the iterator has reached the end of the source sequence.
If the caller uses an inner foreach loop to iterate the chunk items, and that loop ran
to completion, then the Chunk.GetEnumerator method will already have made
copies of all chunk items before we get here. If the Chunk.GetEnumerator loop did
not enumerate all elements in the chunk, we need to do it here to avoid corrupting
the iterator for clients that may be calling us on a separate thread.
The Chunk class is a contiguous group of one or more source elements that have the
same key. A Chunk has a key and a list of ChunkItem objects, which are copies of the
elements in the source sequence:
C#Chunk class
class Chunk<TKey, TSource> : IGrouping <TKey, TSource>
{
    // INVARIANT: DoneCopyingChunk == true ||
    //   (predicate != null && predicate(enumerator.Current) &&  
current.Value == enumerator.Current)
    // A Chunk has a linked list of ChunkItems, which represent the elements  
in the current chunk. Each ChunkItem
    // has a reference to the next ChunkItem in the list.
    class ChunkItem
    {
        public ChunkItem (TSource value) => Value = value;
        public readonly  TSource Value;
        public ChunkItem? Next;
    }
    public TKey Key { get; }
    // Stores a reference to the enumerator for the source sequence
    private IEnumerator<TSource> enumerator;
    // A reference to the predicate that is used to compare keys.
    private Func<TSource, bool> predicate;
    // Stores the contents of the first source element that
    // belongs with this chunk.    private readonly  ChunkItem head;
    // End of the list. It is repositioned each time a new
    // ChunkItem is added.
    private ChunkItem? tail;
    // Flag to indicate the source iterator has reached the end of the  
source sequence.
    internal  bool isLastSourceElement;
    // Private object for thread synchronization
    private readonly  object m_Lock;
    // REQUIRES: enumerator != null && predicate != null
    public Chunk(TKey key, [DisallowNull] IEnumerator<TSource> enumerator,  
[DisallowNull] Func<TSource, bool> predicate )
    {
        Key = key;
        this.enumerator = enumerator;
        this.predicate = predicate;
        // A Chunk always contains at least one element.
        head = new ChunkItem(enumerator.Current);
        // The end and beginning are the same until the list contains > 1  
elements.
        tail = head;
        m_Lock = new object();
    }
    // Indicates that all chunk elements have been copied to the list of  
ChunkItems.
    private bool DoneCopyingChunk => tail == null;
    // Adds one ChunkItem to the current group
    // REQUIRES: !DoneCopyingChunk && lock(this)
    private void CopyNextChunkElement ()
    {
        // Try to advance the iterator on the source sequence.
        isLastSourceElement = !enumerator.MoveNext();
        // If we are (a) at the end of the source, or (b) at the end of the  
current chunk
        // then null out the enumerator and predicate for reuse with the  
next chunk.
        if (isLastSourceElement || !predicate(enumerator.Current))
        {
            enumerator = default!;
            predicate = default!;
        }
        else
        {
            tail!.Next = new ChunkItem(enumerator.Current);
        }        // tail will be null if we are at the end of the chunk elements
        // This check is made in DoneCopyingChunk.
        tail = tail!.Next!;
    }
    // Called after the end of the last chunk was reached.
    internal  bool CopyAllChunkElements ()
    {
        while (true)
        {
            lock (m_Lock)
            {
                if (DoneCopyingChunk)
                {
                    return isLastSourceElement;
                }
                else
                {
                    CopyNextChunkElement();
                }
            }
        }
    }
    // Stays just one step ahead of the client requests.
    public IEnumerator<TSource> GetEnumerator ()
    {
        // Specify the initial element to enumerate.
        ChunkItem? current = head;
        // There should always be at least one ChunkItem in a Chunk.
        while (current != null)
        {
            // Yield the current item in the list.
            yield return current.Value;
            // Copy the next item from the source sequence,
            // if we are at the end of our local list.
            lock (m_Lock)
            {
                if (current == tail)
                {
                    CopyNextChunkElement();
                }
            }
            // Move to the next ChunkItem in the list.
            current = current.Next;
        }
    }
    System.Collections.IEnumerator  
System.Collections.IEnumerable.GetEnumerator() => GetEnumerator();
}A Chunk has a linked list of ChunkItems, which represent the elements in the current
chunk. Each ChunkItem (represented by ChunkItem class) has a reference to the next
ChunkItem in the list. The list consists of it's head - which stores the contents of the first
source element that belongs with this chunk, and it's tail - which is an end of the list. It
is repositioned each time a new ChunkItem is added.
The Chunk class contains the private boolean field: DoneCopyingChunk, which indicates
that all chunk elements have been copied to the list of ChunkItems, and the source
enumerator is either at the end, or else on an element with a new key. The tail of the
linked list is set to null in the CopyNextChunkElement method if the key of the next
element does not match the current chunk's key, or there are no more elements in the
source.
The CopyNextChunkElement method of the Chunk class adds one ChunkItem to the current
group of items.
By using enumerator.MoveNext() method, it tries to advance the iterator on the source
sequence. If MoveNext() method returns false it means that iteration is at the end, and
isLastSourceElement is set to true. Then, if iteration is at the end of the source, or at
the end of the current chunk then the enumerator and predicate is null out for reuse
with the next chunk.
The CopyAllChunkElements method is called after the end of the last chunk was reached.
It first checks whether there are more elements in the source sequence. If there are, it
returns true if enumerator for this chunk was exhausted. In this method, when private
DoneCopyingChunk field is checked for true, if isLastSourceElement is false, it signals to
the outer iterator to continue iterating.
The GetEnumerator method of the Chunk class is invoked by the inner foreach loop. This
method stays just one step ahead of the client requests. It adds the next element of the
chunk only after the clients requests the last element in the list so far.
Language Integrated Query (LINQ)See also
６ Collaborat e with us on
GitHub.NET feedb ackThe source for this content can
be found on GitHub, where you
can also create and review
issues and pull requests. For
more information, see our
contributor guide ..NET is an open source project.
Select a link to provide feedback:
 Open a documentation issue
 Provide product feedbackQuery a collection of objects
Article •07/18/2023
The term "LINQ to Objects" refers to the use of LINQ queries with any IEnumerable  or
IEnumerable<T>  collection directly, without the use of an intermediate LINQ provider or
API such as LINQ to SQL  or LINQ to XML . You can use LINQ to query any enumerable
collections such as List<T> , Array , or Dictionary<TK ey,TValue> . The collection may be
user-defined or may be returned by a .NET API. In the LINQ approach, you write
declarative code that describes what you want to retrieve.
In addition, LINQ queries offer three main advantages over traditional foreach loops:
They are more concise and readable, especially when filtering multiple conditions.
They provide powerful filtering, ordering, and grouping capabilities with a
minimum of application code.
They can be ported to other data sources with little or no modification.
In general, the more complex the operation you want to perform on the data, the more
benefit you'll realize by using LINQ instead of traditional iteration techniques.
This example shows how to perform a simple query over a list of Student objects. Each
Student object contains some basic information about the student, and a list that
represents the student's scores on four examinations.
C#７ Note
Many other examples in this section use the same Student class and students
collection.
class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int ID { get; set; }
    public GradeLevel? Year { get; set; }
    public List<int> ExamScores { get; set; }
    public Student(string FirstName, string LastName, int ID, GradeLevel  
Year, List< int> ExamScores )
    {        this.FirstName = FirstName;
        this.LastName = LastName;
        this.ID = ID;
        this.Year = Year;
        this.ExamScores = ExamScores;
    }
    public Student(string FirstName, string LastName, int StudentID,  
List<int>? ExamScores = null)
    {
        this.FirstName = FirstName;
        this.LastName = LastName;
        ID = StudentID;
        this.ExamScores = ExamScores ?? Enumerable.Empty< int>().ToList();
    }
    public static List<Student> students = new()
    {
        new(
            FirstName: "Terry", LastName: "Adams", ID: 120,
            Year: GradeLevel.SecondYear,
            ExamScores: new() { 99, 82, 81, 79 }
        ),
        new(
            "Fadi", "Fakhouri" , 116,
            GradeLevel.ThirdYear,
            new() { 99, 86, 90, 94 }
        ),
        new(
            "Hanying" , "Feng", 117,
            GradeLevel.FirstYear,
            new() { 93, 92, 80, 87 }
        ),
        new(
            "Cesar", "Garcia" , 114,
            GradeLevel.FourthYear,
            new() { 97, 89, 85, 82 }
        ),
        new(
            "Debra", "Garcia" , 115,
            GradeLevel.ThirdYear,
            new() { 35, 72, 91, 70 }
        ),
        new(
            "Hugo", "Garcia" , 118,
            GradeLevel.SecondYear,
            new() { 92, 90, 83, 78 }
        ),
        new(
            "Sven", "Mortensen" , 113,
            GradeLevel.FirstYear,
            new() { 88, 94, 65, 91 }
        ),
        new(
            "Claire" , "O'Donnell" , 112,The following query returns the students who received a score of 90 or greater on their
first exam.
C#            GradeLevel.FourthYear,
            new() { 75, 84, 91, 39 }
        ),
        new(
            "Svetlana" , "Omelchenko" , 111,
            GradeLevel.SecondYear,
            new() { 97, 92, 81, 60 }
        ),
        new(
            "Lance", "Tucker" , 119,
            GradeLevel.ThirdYear,
            new() { 68, 79, 88, 92 }
        ),
        new(
            "Michael" , "Tucker" , 122,
            GradeLevel.FirstYear,
            new() { 94, 92, 91, 91 }
        ),
        new(
            "Eugene" , "Zabokritski" , 121,
            GradeLevel.FourthYear,
            new() { 96, 85, 91, 60 }
        )
    };
}
enum GradeLevel
{
    FirstYear = 1,
    SecondYear,
    ThirdYear,
    FourthYear
};
Example
void QueryHighScores (int exam, int score)
{
    var highScores =
        from student in students
        where student.ExamScores[exam] > score
        select new
        {
            Name = student.FirstName,
            Score = student.ExamScores[exam]
        };This query is intentionally simple to enable you to experiment. For example, you can try
more conditions in the where clause, or use an orderby clause to sort the results.
The LINQ to Objects implementations of the standard query operator methods execute
in one of two main ways: immediate or deferred. The query operators that use deferred
execution can be additionally divided into two categories: streaming and non-streaming.
If you know how the different query operators execute, it may help you understand the
results that you get from a given query. This is especially true if the data source is
changing or if you are building a query on top of another query. This topic classifies the
standard query operators according to their manner of execution.
Immediate execution means that the data source is read and the operation is performed
once. All the standard query operators that return a scalar result execute immediately.
You can force a query to execute immediately using the Enumerable.T oList  or
Enumerable.T oArray  methods. Immediate execution provides reuse of query results, not
query declaration. The results are retrieved once, then stored for future use.
Deferred execution means that the operation is not performed at the point in the code
where the query is declared. The operation is performed only when the query variable is
enumerated, for example by using a foreach statement. This means that the results of
executing the query depend on the contents of the data source when the query is
executed rather than when the query is defined. If the query variable is enumerated
multiple times, the results might differ every time. Almost all the standard query
operators whose return type is IEnumerable<T>  or IOrderedEnumerable<TElement>
execute in a deferred manner. Deferred execution provides the facility of query reuse    foreach (var item in highScores)
    {
        Console.WriteLine( $"{item.Name, -15}{item.Score} ");
    }
}
QueryHighScores( 1, 90);
Classification of standard query operators by
manner of execution
Immediate
Deferredsince the query fetches the updated data from the data source each time query results
are iterated.
Query operators that use deferred execution can be additionally classified as streaming
or non-streaming.
Streaming operators do not have to read all the source data before they yield elements.
At the time of execution, a streaming operator performs its operation on each source
element as it is read and yields the element if appropriate. A streaming operator
continues to read source elements until a result element can be produced. This means
that more than one source element might be read to produce one result element.
Non-streaming operators must read all the source data before they can yield a result
element. Operations such as sorting or grouping fall into this category. At the time of
execution, non-streaming query operators read all the source data, put it into a data
structure, perform the operation, and yield the resulting elements.
The following table classifies each standard query operator method according to its
method of execution.
Standar d quer y
operat orReturn type Immediat e
executionDeferr ed
streaming
executionDeferr ed
Non-
streaming
execution
Aggregate TSource X
All Boolean XStreaming
Non-streaming
Classification table
７ Note
If an operator is marked in two columns, two input sequences are involved in the
operation, and each sequence is evaluated differently. In these cases, it is always
the first sequence in the parameter list that is evaluated in a deferred, streaming
manner.Standar d quer y
operat orReturn type Immediat e
executionDeferr ed
streaming
executionDeferr ed
Non-
streaming
execution
Any Boolean X
AsEnumerable IEnumerable<T> X
Average Single numeric value X
Cast IEnumerable<T> X
Concat IEnumerable<T> X
Contains Boolean X
Count Int32 X
DefaultIfEmpty IEnumerable<T> X
Distinct IEnumerable<T> X
ElementAt TSource X
ElementAtOrDefault TSource? X
Empty IEnumerable<T> X
Except IEnumerable<T> X X
First TSource X
FirstOrDefault TSource? X
GroupBy IEnumerable<T> X
GroupJoin IEnumerable<T> X X
Intersect IEnumerable<T> X X
Join IEnumerable<T> X X
Last TSource X
LastOrDefault TSource? X
LongCount Int64 X
Max Single numeric value, TSource, or
TResult?XStandar d quer y
operat orReturn type Immediat e
executionDeferr ed
streaming
executionDeferr ed
Non-
streaming
execution
Min Single numeric value, TSource, or
TResult?X
OfType IEnumerable<T> X
OrderBy IOrderedEnumerable<TElement> X
OrderByDescending IOrderedEnumerable<TElement> X
Range IEnumerable<T> X
Repeat IEnumerable<T> X
Reverse IEnumerable<T> X
Select IEnumerable<T> X
SelectMany IEnumerable<T> X
SequenceEqual Boolean X
Single TSource X
SingleOrDefault TSource? X
Skip IEnumerable<T> X
SkipWhile IEnumerable<T> X
Sum Single numeric value X
Take IEnumerable<T> X
TakeWhile IEnumerable<T> X
ThenBy IOrderedEnumerable<TElement> X
ThenByDescending IOrderedEnumerable<TElement> X
ToArray TSource[] array X
ToDictionary Dictionary<TK ey,TValue> X
ToList IList<T> X
ToLookup ILookup<TK ey,TElement> X
Union IEnumerable<T> XStandar d quer y
operat orReturn type Immediat e
executionDeferr ed
streaming
executionDeferr ed
Non-
streaming
execution
Where IEnumerable<T> X
Language Integrated Query (LINQ)
String interpolationSee alsoWalkthrough: Writing Queries in C#
(LINQ)
Article •09/21/2022
This walkthrough demonstrates the C# language features that are used to write LINQ
query expressions.
1. Start Visual S tudio.
2. On the menu bar, choose File, New , Project .
The New Pr oject  dialog box opens.
3. Expand Installed , expand Templat es, expand Visual C# , and then choose Console
Application .
4. In the Name  text box, enter a different name or accept the default name, and then
choose the OK button.
The new project appears in Solution Explor er.
5. Notice that your project has a reference to S ystem.Core.dll and a using directive
for the System.Linq  namespace.
The data source for the queries is a simple list of Student objects. Each Student record
has a first name, last name, and an array of integers that represents their test scores in
the class. Copy this code into your project. Note the following characteristics:Create a C# Project
７ Note
The following instructions are for Visual S tudio. If you are using a different
development environment, create a console project with a reference to
System.Core.dll and a using directive for the System.Linq  namespace.
To create a project in Visual Studio
Create an in-Memory Data SourceThe Student class consists of auto-implemented properties.
Each student in the list is initialized with an object initializer.
The list itself is initialized with a collection initializer.
This whole data structure will be initialized and instantiated without explicit calls to any
constructor or explicit member access. For more information about these new features,
see Auto-Implemented Properties  and Object and Collection Initializers .
Add the Student class and the initialized list of students to the Program class in
your project.
C#To add the data source
public class Student
{
    public string First { get; set; }
    public string Last { get; set; }
    public int ID { get; set; }
    public List<int> Scores;
}
// Create a data source by using a collection initializer.
static List<Student> students = new List<Student>
{
    new Student {First= "Svetlana" , Last="Omelchenko" , ID=111, Scores= 
new List<int> {97, 92, 81, 60}},
    new Student {First= "Claire" , Last="O'Donnell" , ID=112, Scores= new 
List<int> {75, 84, 91, 39}},
    new Student {First= "Sven", Last="Mortensen" , ID=113, Scores= new 
List<int> {88, 94, 65, 91}},
    new Student {First= "Cesar", Last="Garcia" , ID=114, Scores= new 
List<int> {97, 89, 85, 82}},
    new Student {First= "Debra", Last="Garcia" , ID=115, Scores= new 
List<int> {35, 72, 91, 70}},
    new Student {First= "Fadi", Last="Fakhouri" , ID=116, Scores= new 
List<int> {99, 86, 90, 94}},
    new Student {First= "Hanying" , Last="Feng", ID=117, Scores= new 
List<int> {93, 92, 80, 87}},
    new Student {First= "Hugo", Last="Garcia" , ID=118, Scores= new 
List<int> {92, 90, 83, 78}},
    new Student {First= "Lance", Last="Tucker" , ID=119, Scores= new 
List<int> {68, 79, 88, 92}},
    new Student {First= "Terry", Last="Adams", ID=120, Scores= new 
List<int> {99, 82, 81, 79}},
    new Student {First= "Eugene" , Last="Zabokritski" , ID=121, Scores= 
new List<int> {96, 85, 91, 60}},
    new Student {First= "Michael" , Last="Tucker" , ID=122, Scores= new 1. Add a new Student to the Students list and use a name and test scores of your
choice. T ry typing all the new student information in order to better learn the
syntax for the object initializer.
In the application's Main method, create a simple query that, when it is executed,
will produce a list of all students whose score on the first test was greater than 90.
Note that because the whole Student object is selected, the type of the query is
IEnumerable<Student>. Although the code could also use implicit typing by using
the var keyword, explicit typing is used to clearly illustrate results. (For more
information about var, see Implicitly T yped Local V ariables .)
Note also that the query's range variable, student, serves as a reference to each
Student in the source, providing member access for each object.
C#
1. Now write the foreach loop that will cause the query to execute. Note the
following about the code:List<int> {94, 92, 91, 91}}
};
To add a new Student to the Students list
Create the Query
To create a simple query
// Create the query.
// The first line could also be written as "var studentQuery ="
IEnumerable<Student> studentQuery =
    from student in students
    where student.Scores[ 0] > 90
    select student;
Execute the Query
To execute the queryEach element in the returned sequence is accessed through the iteration
variable in the foreach loop.
The type of this variable is Student, and the type of the query variable is
compatible, IEnumerable<Student>.
2. After you have added this code, build and run the application to see the results in
the Console  window.
C#
1. You can combine multiple Boolean conditions in the where clause in order to
further refine a query. The following code adds a condition so that the query
returns those students whose first score was over 90 and whose last score was less
than 80. The where clause should resemble the following code.
C#
For more information, see where clause .// Execute the query.
// var could be used here also.
foreach (Student student in studentQuery)
{
    Console.WriteLine( "{0}, {1}" , student.Last, student.First);
}
// Output:
// Omelchenko, Svetlana
// Garcia, Cesar
// Fakhouri, Fadi
// Feng, Hanying
// Garcia, Hugo
// Adams, Terry
// Zabokritski, Eugene
// Tucker, Michael
To add another filter condition
where student.Scores[ 0] > 90 && student.Scores[ 3] < 80  
Modify the Query
To order the results1. It will be easier to scan the results if they are in some kind of order. Y ou can order
the returned sequence by any accessible field in the source elements. For example,
the following orderby clause orders the results in alphabetical order from A to Z
according to the last name of each student. Add the following orderby clause to
your query, right after the where statement and before the select statement:
C#
2. Now change the orderby clause so that it orders the results in reverse order
according to the score on the first test, from the highest score to the lowest score.
C#
3. Change the WriteLine format string so that you can see the scores:
C#
For more information, see orderby clause .
1. Grouping is a powerful capability in query expressions. A query with a group clause
produces a sequence of groups, and each group itself contains a Key and a
sequence that consists of all the members of that group. The following new query
groups the students by using the first letter of their last name as the key.
C#
2. Note that the type of the query has now changed. It now produces a sequence of
groups that have a char type as a key, and a sequence of Student objects.orderby student.Last ascending   
orderby student.Scores[ 0] descending   
Console.WriteLine( "{0}, {1} {2}" , student.Last, student.First,  
student.Scores[ 0]);  
To group the results
IEnumerable<IGrouping< char, Student>> studentQuery2 =
    from student in students
    group student by student.Last[ 0];Because the type of the query has changed, the following code changes the
foreach execution loop also:
C#
3. Run the application and view the results in the Console  window.
For more information, see group clause .
1. Explicitly coding IEnumerables of IGroupings can quickly become tedious. Y ou can
write the same query and foreach loop much more conveniently by using var.
The var keyword does not change the types of your objects; it just instructs the
compiler to infer the types. Change the type of studentQuery and the iteration
variable group to var and rerun the query. Note that in the inner foreach loop,
the iteration variable is still typed as Student, and the query works just as before.foreach (IGrouping< char, Student> studentGroup in studentQuery2)
{
    Console.WriteLine(studentGroup.Key);
    foreach (Student student in studentGroup)
    {
        Console.WriteLine( "   {0}, {1}" ,
                  student.Last, student.First);
    }
}
// Output:
// O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
// M
//   Mortensen, Sven
// G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
// F
//   Fakhouri, Fadi
//   Feng, Hanying
// T
//   Tucker, Lance
//   Tucker, Michael
// A
//   Adams, Terry
// Z
//   Zabokritski, Eugene
To make the variables implicitly typedChange the student iteration variable to var and run the query again. Y ou see that
you get exactly the same results.
C#
For more information about var, see Implicitly T yped Local V ariables .
1. When you run the previous query, you notice that the groups are not in
alphabetical order. T o change this, you must provide an orderby clause after the
group clause. But to use an orderby clause, you first need an identifier that serves
as a reference to the groups created by the group clause. Y ou provide the identifier
by using the into keyword, as follows:var studentQuery3 =
    from student in students
    group student by student.Last[ 0];
foreach (var groupOfStudents in studentQuery3)
{
    Console.WriteLine(groupOfStudents.Key);
    foreach (var student in groupOfStudents)
    {
        Console.WriteLine( "   {0}, {1}" ,
            student.Last, student.First);
    }
}
// Output:
// O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
// M
//   Mortensen, Sven
// G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
// F
//   Fakhouri, Fadi
//   Feng, Hanying
// T
//   Tucker, Lance
//   Tucker, Michael
// A
//   Adams, Terry
// Z
//   Zabokritski, Eugene
To order the groups by their key valueC#
When you run this query, you will see the groups are now sorted in alphabetical
order.
1. You can use the let keyword to introduce an identifier for any expression result in
the query expression. This identifier can be a convenience, as in the following
example, or it can enhance performance by storing the results of an expression so
that it does not have to be calculated multiple times.
C#var studentQuery4 =
    from student in students
    group student by student.Last[ 0] into studentGroup
    orderby studentGroup.Key
    select studentGroup;
foreach (var groupOfStudents in studentQuery4)
{
    Console.WriteLine(groupOfStudents.Key);
    foreach (var student in groupOfStudents)
    {
        Console.WriteLine( "   {0}, {1}" ,
            student.Last, student.First);
    }
}
// Output:
//A
//   Adams, Terry
//F
//   Fakhouri, Fadi
//   Feng, Hanying
//G
//   Garcia, Cesar
//   Garcia, Debra
//   Garcia, Hugo
//M
//   Mortensen, Sven
//O
//   Omelchenko, Svetlana
//   O'Donnell, Claire
//T
//   Tucker, Lance
//   Tucker, Michael
//Z
//   Zabokritski, Eugene
To introduce an identifier by using letFor more information, see let clause .
1. As described in Query S yntax and Method S yntax in LINQ , some query operations
can only be expressed by using method syntax. The following code calculates the
total score for each Student in the source sequence, and then calls the Average()
method on the results of that query to calculate the average score of the class.
C#// studentQuery5 is an IEnumerable<string>
// This query returns those students whose
// first test score was higher than their
// average score.
var studentQuery5 =
    from student in students
    let totalScore = student.Scores[ 0] + student.Scores[ 1] +
        student.Scores[ 2] + student.Scores[ 3]
    where totalScore / 4 < student.Scores[ 0]
    select student.Last + " " + student.First;
foreach (string s in studentQuery5)
{
    Console.WriteLine(s);
}
// Output:
// Omelchenko Svetlana
// O'Donnell Claire
// Mortensen Sven
// Garcia Cesar
// Fakhouri Fadi
// Feng Hanying
// Garcia Hugo
// Adams Terry
// Zabokritski Eugene
// Tucker Michael
To use method syntax in a query expression
var studentQuery6 =
    from student in students
    let totalScore = student.Scores[ 0] + student.Scores[ 1] +
        student.Scores[ 2] + student.Scores[ 3]
    select totalScore;
double averageScore = studentQuery6.Average();
Console.WriteLine( "Class average score = {0}" , averageScore);1. It is very common for a query to produce a sequence whose elements differ from
the elements in the source sequences. Delete or comment out your previous query
and execution loop, and replace it with the following code. Note that the query
returns a sequence of strings (not Students), and this fact is reflected in the
foreach loop.
C#
2. Code earlier in this walkthrough indicated that the average class score is
approximately 334. T o produce a sequence of Students whose total score is
greater than the class average, together with their Student ID, you can use an
anonymous type in the select statement:
C#// Output:
// Class average score = 334.166666666667
To transform or project in the select clause
IEnumerable< string> studentQuery7 =
    from student in students
    where student.Last == "Garcia"
    select student.First;
Console.WriteLine( "The Garcias in the class are:" );
foreach (string s in studentQuery7)
{
    Console.WriteLine(s);
}
// Output:
// The Garcias in the class are:
// Cesar
// Debra
// Hugo
var studentQuery8 =
    from student in students
    let x = student.Scores[ 0] + student.Scores[ 1] +
        student.Scores[ 2] + student.Scores[ 3]
    where x > averageScore
    select new { id = student.ID, score = x };
foreach (var item in studentQuery8)
{
    Console.WriteLine( "Student ID: {0}, Score: {1}" , item.id,  After you are familiar with the basic aspects of working with queries in C#, you are ready
to read the documentation and samples for the specific type of LINQ provider you are
interested in:
LINQ to SQL
LINQ to DataSet
LINQ to XML (C#)
LINQ to Objects (C#)
Language-Integrated Query (LINQ) (C#)
LINQ Query Expressionsitem.score);
}
// Output:
// Student ID: 113, Score: 338
// Student ID: 114, Score: 353
// Student ID: 116, Score: 369
// Student ID: 117, Score: 352
// Student ID: 118, Score: 343
// Student ID: 120, Score: 341
// Student ID: 122, Score: 368
Next Steps
See alsoLINQ and file directories (C#)
Article •09/15/2021
Many file system operations are essentially queries and are therefore well suited to the
LINQ approach.
The queries in this section are non-destructive. They are not used to change the
contents of the original files or folders. This follows the rule that queries should not
cause any side-effects. In general, any code (including queries that perform create /
update / delete operators) that modifies source data should be kept separate from the
code that just queries the data.
This section contains the following topics:
How to query for files with a specified attribute or name (C#)
Shows how to search for files by examining one or more properties of its FileInfo  object.
How to group files by extension (LINQ) (C#)
Shows how to return groups of FileInfo  object based on their file name extension.
How to query for the total number of bytes in a set of folders (LINQ) (C#)
Shows how to return the total number of bytes in all the files in a specified directory
tree.
How to compare the contents of two folders (LINQ) (C#) s
Shows how to return all the files that are present in two specified folders, and also all
the files that are present in one folder but not the other.
How to query for the largest file or files in a directory tree (LINQ) (C#)
Shows how to return the largest or smallest file, or a specified number of files, in a
directory tree.
How to query for duplicate files in a directory tree (LINQ) (C#)
Shows how to group for all file names that occur in more than one location in a
specified directory tree. Also shows how to perform more complex comparisons based
on a custom comparer.
How to query the contents of files in a folder (LINQ) (C#)
Shows how to iterate through folders in a tree, open each file, and query the file's
contents.
CommentsThere is some complexity involved in creating a data source that accurately represents
the contents of the file system and handles exceptions gracefully. The examples in this
section create a snapshot collection of FileInfo  objects that represents all the files under
a specified root folder and all its subfolders. The actual state of each FileInfo  may
change in the time between when you begin and end executing a query. For example,
you can create a list of FileInfo  objects to use as a data source. If you try to access the
Length property in a query, the FileInfo  object will try to access the file system to update
the value of Length. If the file no longer exists, you will get a FileNotFoundException  in
your query, even though you are not querying the file system directly. Some queries in
this section use a separate method that consumes these particular exceptions in certain
cases. Another option is to keep your data source updated dynamically by using the
FileSystemW atcher .How to query for files with a specified
attribute or name (C#)
Article •07/18/2023
This example shows how to find all files that have a specified file name extension (for
example ".txt") in a specified directory tree. It also shows how to return either the newest
or oldest file in the tree based on the creation time.
C#Example
class FindFileByExtension   
{  
    // This query will produce the full path for all .txt files  
    // under the specified folder including subfolders.  
    // It orders the list according to the file name.  
    static void Main()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery  
permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        //Create the query  
        IEnumerable<System.IO.FileInfo> fileQuery =  
            from file in fileList  
            where file.Extension == ".txt"  
            orderby file.Name  
            select file;  
  
        //Execute the query. This might write out a lot of files!  
        foreach (System.IO.FileInfo fi in fileQuery)  
        {  
            Console.WriteLine(fi.FullName);  
        }  
  
        // Create and execute a new query by using the previous
        // query as a starting point. fileQuery is not
        // executed again until the call to Last()  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.        var newestFile =  
            (from file in fileQuery  
             orderby file.CreationTime  
             select new { file.FullName, file.CreationTime })  
            .Last();  
  
        Console.WriteLine( "\r\nThe newest .txt file is {0}. Creation time:  
{1}",  
            newestFile.FullName, newestFile.CreationTime);  
    }  
}  
Compiling the Code
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
 Provide product feedbackHow to group files by extension (LINQ)
(C#)
Article •07/18/2023
This example shows how LINQ can be used to perform advanced grouping and sorting
operations on lists of files or folders. It also shows how to page output in the console
window by using the Skip and Take methods.
The following query shows how to group the contents of a specified directory tree by
the file name extension.
C#Example
class GroupByExtension   
{  
    // This query will sort all the files under the specified folder  
    //  and subfolder into groups keyed by the file extension.  
    private static void Main()  
    {  
        // Take a snapshot of the file system.  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\Common7" ;  
  
        // Used in WriteLine to trim output lines.  
        int trimLength = startFolder.Length;  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery  
permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        // Create the query.  
        var queryGroupByExt =  
            from file in fileList  
            group file by file.Extension.ToLower() into fileGroup  
            orderby fileGroup.Key  
            select fileGroup;  
  
        // Display one group at a time. If the number of
        // entries is greater than the number of lines          // in the console window, then page the output.  
        PageOutput(trimLength, queryGroupByExt);  
    }  
  
    // This method specifically handles group queries of FileInfo objects  
with string keys.  
    // It can be modified to work for any long listings of data. Note that  
explicit typing  
    // must be used in method signatures. The groupbyExtList parameter is a  
query that produces  
    // groups of FileInfo objects with string keys.  
    private static void PageOutput (int rootLength,  
                                    
IEnumerable<System.Linq.IGrouping< string, System.IO.FileInfo>>  
groupByExtList )  
    {  
        // Flag to break out of paging loop.  
        bool goAgain = true;  
  
        // "3" = 1 line for extension + 1 for "Press any key" + 1 for input  
cursor.  
        int numLines = Console.WindowHeight - 3;  
  
        // Iterate through the outer collection of groups.  
        foreach (var filegroup in groupByExtList)  
        {  
            // Start a new extension at the top of a page.  
            int currentLine = 0;  
  
            // Output only as many lines of the current group as will fit in  
the window.  
            do  
            {  
                Console.Clear();  
                Console.WriteLine(filegroup.Key == String.Empty ? "[none]"  : 
filegroup.Key);  
  
                // Get 'numLines' number of items starting at number  
'currentLine'.  
                var resultPage = filegroup.Skip(currentLine).Take(numLines);   
  
                //Execute the resultPage query  
                foreach (var f in resultPage)  
                {  
                    Console.WriteLine( "\t{0}", 
f.FullName.Substring(rootLength));  
                }  
  
                // Increment the line counter.  
                currentLine += numLines;  
  
                // Give the user a chance to escape.  
                Console.WriteLine( "Press any key to continue or the 'End'  
key to break..." );  
                ConsoleKey key = Console.ReadKey().Key;  The output from this program can be long, depending on the details of the local file
system and what the startFolder is set to. T o enable viewing of all results, this example
shows how to page through results. The same techniques can be applied to Windows
and W eb applications. Notice that because the code pages the items in a group, a
nested foreach loop is required. There is also some additional logic to compute the
current position in the list, and to enable the user to stop paging and exit the program.
In this particular case, the paging query is run against the cached results from the
original query. In other contexts, such as LINQ to SQL, such caching is not required.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.                if (key == ConsoleKey.End)  
                {  
                    goAgain = false;  
                    break;  
                }  
            } while (currentLine < filegroup.Count());  
  
            if (goAgain == false)  
                break;  
        }  
    }  
}  
Compiling the CodeHow to query for the total number of
bytes in a set of folders (LINQ) (C#)
Article •07/18/2023
This example shows how to retrieve the total number of bytes used by all the files in a
specified folder and all its subfolders.
The Sum method adds the values of all the items selected in the select clause. Y ou can
easily modify this query to retrieve the biggest or smallest file in the specified directory
tree by calling the Min or Max method instead of Sum.
C#Example
class QuerySize   
{  
    public static void Main()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\VC#" ;  
  
        // Take a snapshot of the file system.  
        // This method assumes that the application has discovery  
permissions  
        // for all folders under the specified path.  
        IEnumerable< string> fileList =  
System.IO.Directory.GetFiles(startFolder, "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        var fileQuery = from file in fileList  
                        select GetFileLength (file);  
  
        // Cache the results to avoid multiple trips to the file system.  
        long[] fileLengths = fileQuery.ToArray();  
  
        // Return the size of the largest file  
        long largestFile = fileLengths.Max();  
  
        // Return the total number of bytes in all the files under the  
specified folder.  
        long totalBytes = fileLengths.Sum();  
  
        Console.WriteLine( "There are {0} bytes in {1} files under {2}" ,  
            totalBytes, fileList.Count(), startFolder);  
        Console.WriteLine( "The largest files is {0} bytes." , largestFile);  
    }  If you only have to count the number of bytes in a specified directory tree, you can do
this more efficiently without creating a LINQ query, which incurs the overhead of
creating the list collection as a data source. The usefulness of the LINQ approach
increases as the query becomes more complex, or when you have to run multiple
queries against the same data source.
The query calls out to a separate method to obtain the file length. It does this in order
to consume the possible exception that will be raised if the file was deleted on another
thread after the FileInfo  object was created in the call to GetFiles. Even though the
FileInfo  object has already been created, the exception can occur because a FileInfo
object will try to refresh its Length  property with the most current length the first time
the property is accessed. By putting this operation in a try-catch block outside the
query, the code follows the rule of avoiding operations in queries that can cause side-
effects. In general, great care must be taken when you consume exceptions to make
sure that an application is not left in an unknown state.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the System.IO.FileInfo.Length  
property.  
    static long GetFileLength (string filename )  
    {  
        long retval;  
        try  
        {  
            System.IO.FileInfo fi = new System.IO.FileInfo(filename);  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
}  
Compiling the Code６ Collaborat e with us on
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
 Provide product feedbackHow to compare the contents of two
folders (LINQ) (C#)
Article •07/18/2023
This example demonstrates three ways to compare two file listings:
By querying for a Boolean value that specifies whether the two file lists are
identical.
By querying for the intersection to retrieve the files that are in both folders.
By querying for the set difference to retrieve the files that are in one folder but not
the other.
The FileComparer class shown here demonstrates how to use a custom comparer class
together with the S tandard Query Operators. The class is not intended for use in real-
world scenarios. It just uses the name and length in bytes of each file to determine
whether the contents of each folder are identical or not. In a real-world scenario, you
should modify this comparer to perform a more rigorous equality check.
C#７ Note
The techniques shown here can be adapted to compare sequences of objects
of any type.
Example
namespace  QueryCompareTwoDirs   
{  
    class CompareDirs   
    {  
  
        static void Main(string[] args)  
        {  
  
            // Create two identical or different temporary folders
            // on a local drive and change these file paths.  
            string pathA = @"C:\TestDir" ;  
            string pathB = @"C:\TestDir2" ;  
  
            System.IO.DirectoryInfo dir1 = new System.IO.DirectoryInfo(pathA);  
            System.IO.DirectoryInfo dir2 = new 
System.IO.DirectoryInfo(pathB);  
  
            // Take a snapshot of the file system.  
            IEnumerable<System.IO.FileInfo> list1 = dir1.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
            IEnumerable<System.IO.FileInfo> list2 = dir2.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
            //A custom file comparer defined below  
            FileCompare myFileCompare = new FileCompare();  
  
            // This query determines whether the two folders contain  
            // identical file lists, based on the custom file comparer  
            // that is defined in the FileCompare class.  
            // The query executes immediately because it returns a bool.  
            bool areIdentical = list1.SequenceEqual(list2, myFileCompare);  
  
            if (areIdentical == true)  
            {  
                Console.WriteLine( "the two folders are the same" );  
            }  
            else  
            {  
                Console.WriteLine( "The two folders are not the same" );  
            }  
  
            // Find the common files. It produces a sequence and doesn't
            // execute until the foreach statement.  
            var queryCommonFiles = list1.Intersect(list2, myFileCompare);  
  
            if (queryCommonFiles.Any())  
            {  
                Console.WriteLine( "The following files are in both  
folders:" );  
                foreach (var v in queryCommonFiles)  
                {  
                    Console.WriteLine(v.FullName); //shows which items end  
up in result list  
                }  
            }  
            else  
            {  
                Console.WriteLine( "There are no common files in the two  
folders." );  
            }  
  
            // Find the set difference between the two folders.  
            // For this example we only check one way.  
            var queryList1Only = ( from file in list1  
                                  select file).Except(list2, myFileCompare);   
  
            Console.WriteLine( "The following files are in list1 but not  
list2:");  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.            foreach (var v in queryList1Only)  
            {  
                Console.WriteLine(v.FullName);  
            }  
        }  
    }  
  
    // This implementation defines a very simple comparison  
    // between two FileInfo objects. It only compares the name  
    // of the files being compared and their length in bytes.  
    class FileCompare  : 
System.Collections .Generic.IEqualityComparer <System.IO.FileInfo >  
    {  
        public FileCompare () { }  
  
        public bool Equals(System.IO.FileInfo f1, System.IO.FileInfo f2 )  
        {  
            return (f1.Name == f2.Name &&  
                    f1.Length == f2.Length);  
        }  
  
        // Return a hash that reflects the comparison criteria. According to  
the
        // rules for IEqualityComparer<T>, if Equals is true, then the hash  
codes must  
        // also be equal. Because equality as defined here is a simple value  
equality, not  
        // reference identity, it is possible that two or more objects will  
produce the same  
        // hash code.  
        public int GetHashCode (System.IO.FileInfo fi )  
        {  
            string s = $"{fi.Name} {fi.Length} ";
            return s.GetHashCode();  
        }  
    }  
}  
Compiling the Code
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you.NET feedb ack
The .NET documentation is open
source. Provide feedback here.can also create and review
issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackHow to query for the largest file or files
in a directory tree (LINQ) (C#)
Article •07/18/2023
This example shows five queries related to file size in bytes:
How to retrieve the size in bytes of the largest file.
How to retrieve the size in bytes of the smallest file.
How to retrieve the FileInfo  object largest or smallest file from one or more folders
under a specified root folder.
How to retrieve a sequence such as the 10 largest files.
How to order files into groups based on their file size in bytes, ignoring files that
are less than a specified size.
The following example contains five separate queries that show how to query and group
files, depending on their file size in bytes. Y ou can easily modify these examples to base
the query on some other property of the FileInfo  object.
C#Example
class QueryBySize   
{  
    static void Main(string[] args)  
    {  
        QueryFilesBySize();  
        Console.WriteLine( "Press any key to exit" );  
        Console.ReadKey();  
    }  
  
    private static void QueryFilesBySize ()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery  
permissions          // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        //Return the size of the largest file  
        long maxSize =  
            (from file in fileList  
             let len = GetFileLength(file)  
             select len)  
             .Max();  
  
        Console.WriteLine( "The length of the largest file under {0} is {1}" ,  
            startFolder, maxSize);  
  
        // Return the FileInfo object for the largest file  
        // by sorting and selecting from beginning of list  
        System.IO.FileInfo longestFile =  
            (from file in fileList  
             let len = GetFileLength(file)  
             where len > 0  
             orderby len descending   
             select file)  
            .First();  
  
        Console.WriteLine( "The largest file under {0} is {1} with a length  
of {2} bytes" ,  
                            startFolder, longestFile.FullName,  
longestFile.Length);  
  
        //Return the FileInfo of the smallest file  
        System.IO.FileInfo smallestFile =  
            (from file in fileList  
             let len = GetFileLength(file)  
             where len > 0  
             orderby len ascending   
             select file).First();  
  
        Console.WriteLine( "The smallest file under {0} is {1} with a length  
of {2} bytes" ,  
                            startFolder, smallestFile.FullName,  
smallestFile.Length);  
  
        //Return the FileInfos for the 10 largest files  
        // queryTenLargest is an IEnumerable<System.IO.FileInfo>  
        var queryTenLargest =  
            (from file in fileList  
             let len = GetFileLength(file)  
             orderby len descending   
             select file).Take( 10);  
  
        Console.WriteLine( "The 10 largest files under {0} are:" , 
startFolder);  
  
        foreach (var v in queryTenLargest)  
        {  To return one or more complete FileInfo  objects, the query first must examine each one
in the data source, and then sort them by the value of their Length property. Then it can
return the single one or the sequence with the greatest lengths. Use First to return the
first element in a list. Use Take to return the first n number of elements. Specify a
descending sort order to put the smallest elements at the start of the list.            Console.WriteLine( "{0}: {1} bytes" , v.FullName, v.Length);  
        }  
  
        // Group the files according to their size, leaving out  
        // files that are less than 200000 bytes.
        var querySizeGroups =  
            from file in fileList  
            let len = GetFileLength(file)  
            where len > 0  
            group file by (len / 100000) into fileGroup  
            where fileGroup.Key > = 2  
            orderby fileGroup.Key descending   
            select fileGroup;  
  
        foreach (var filegroup in querySizeGroups)  
        {  
            Console.WriteLine(filegroup.Key.ToString() + "00000");  
            foreach (var item in filegroup)  
            {  
                Console.WriteLine( "\t{0}: {1}" , item.Name, item.Length);  
            }  
        }  
    }  
  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the FileInfo.Length property.  
    // In this particular case, it is safe to swallow the exception.  
    static long GetFileLength (System.IO.FileInfo fi )  
    {  
        long retval;  
        try  
        {  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
  
}  The query calls out to a separate method to obtain the file size in bytes in order to
consume the possible exception that will be raised in the case where a file was deleted
on another thread in the time period since the FileInfo  object was created in the call to
GetFiles. Even through the FileInfo  object has already been created, the exception can
occur because a FileInfo  object will try to refresh its Length  property by using the most
current size in bytes the first time the property is accessed. By putting this operation in a
try-catch block outside the query, we follow the rule of avoiding operations in queries
that can cause side-effects. In general, great care must be taken when consuming
exceptions, to make sure that an application is not left in an unknown state.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.Compiling the CodeHow to query for duplicate files in a
directory tree (LINQ) (C#)
Article •07/18/2023
Sometimes files that have the same name may be located in more than one folder. For
example, under the Visual S tudio installation folder, several folders have a readme.htm
file. This example shows how to query for such duplicate file names under a specified
root folder. The second example shows how to query for files whose size and LastWrite
times also match.
C#Example
class QueryDuplicateFileNames   
{  
    static void Main(string[] args)  
    {  
        // Uncomment QueryDuplicates2 to run that query.  
        QueryDuplicates();  
        // QueryDuplicates2();  
    }  
  
    static void QueryDuplicates ()  
    {  
        // Change the root drive or folder if necessary  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery  
permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        // used in WriteLine to keep the lines shorter  
        int charsToSkip = startFolder.Length;  
  
        // var can be used for convenience with groups.  
        var queryDupNames =  
            from file in fileList  
            group file.FullName.Substring(charsToSkip) by file.Name into 
fileGroup              where fileGroup.Count() > 1  
            select fileGroup;  
  
        // Pass the query to a method that will  
        // output one page at a time.  
        PageOutput< string, string>(queryDupNames);  
    }  
  
    // A Group key that can be passed to a separate method.  
    // Override Equals and GetHashCode to define equality for the key.  
    // Override ToString to provide a friendly name for Key.ToString()  
    class PortableKey   
    {  
        public string Name { get; set; }  
        public DateTime LastWriteTime { get; set; }  
        public long Length { get; set; }  
  
        public override  bool Equals(object obj)  
        {  
            PortableKey other = (PortableKey)obj;  
            return other.LastWriteTime == this.LastWriteTime &&  
                   other.Length == this.Length &&  
                   other.Name == this.Name;  
        }  
  
        public override  int GetHashCode ()  
        {  
            string str = $"{this.LastWriteTime} {this.Length} {this.Name}";
            return str.GetHashCode();  
        }  
        public override  string ToString ()  
        {  
            return $"{this.Name} {this.Length}  {this.LastWriteTime} ";
        }  
    }  
    static void QueryDuplicates2 ()  
    {  
        // Change the root drive or folder if necessary.  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\Common7" ;  
  
        // Make the lines shorter for the console display  
        int charsToSkip = startFolder.Length;  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        // Note the use of a compound key. Files that match  
        // all three properties belong to the same group.  
        // A named type is used to enable the query to be  
        // passed to another method. Anonymous types can also be used  
        // for composite keys but cannot be passed across method boundaries           //
        var queryDupFiles =  
            from file in fileList  
            group file.FullName.Substring(charsToSkip) by  
                new PortableKey { Name = file.Name, LastWriteTime =  
file.LastWriteTime, Length = file.Length } into fileGroup  
            where fileGroup.Count() > 1  
            select fileGroup;  
  
        var list = queryDupFiles.ToList();  
  
        int i = queryDupFiles.Count();  
  
        PageOutput<PortableKey, string>(queryDupFiles);  
    }  
  
    // A generic method to page the output of the QueryDuplications methods   
    // Here the type of the group must be specified explicitly. "var" cannot   
    // be used in method signatures. This method does not display more than  
one  
    // group per page.  
    private static void PageOutput<K, V>
(IEnumerable<System.Linq.IGrouping<K, V>> groupByExtList)  
    {  
        // Flag to break out of paging loop.  
        bool goAgain = true;  
  
        // "3" = 1 line for extension + 1 for "Press any key" + 1 for input  
cursor.  
        int numLines = Console.WindowHeight - 3;  
  
        // Iterate through the outer collection of groups.  
        foreach (var filegroup in groupByExtList)  
        {  
            // Start a new extension at the top of a page.  
            int currentLine = 0;  
  
            // Output only as many lines of the current group as will fit in  
the window.  
            do  
            {  
                Console.Clear();  
                Console.WriteLine( "Filename = {0}" , filegroup.Key.ToString()  
== String.Empty ? "[none]"  : filegroup.Key.ToString());  
  
                // Get 'numLines' number of items starting at number  
'currentLine'.  
                var resultPage = filegroup.Skip(currentLine).Take(numLines);   
  
                //Execute the resultPage query  
                foreach (var fileName in resultPage)  
                {  
                    Console.WriteLine( "\t{0}", fileName);  
                }  
  The first query uses a simple key to determine a match; this finds files that have the
same name but whose contents might be different. The second query uses a compound
key to match against three properties of the FileInfo  object. This query is much more
likely to find files that have the same name and similar or identical content.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.                // Increment the line counter.  
                currentLine += numLines;  
  
                // Give the user a chance to escape.  
                Console.WriteLine( "Press any key to continue or the 'End'  
key to break..." );  
                ConsoleKey key = Console.ReadKey().Key;  
                if (key == ConsoleKey.End)  
                {  
                    goAgain = false;  
                    break;  
                }  
            } while (currentLine < filegroup.Count());  
  
            if (goAgain == false)  
                break;  
        }  
    }  
}  
Compiling the Code
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
 Provide product feedbackHow to query the contents of text files
in a folder (LINQ) (C#)
Article •07/18/2023
This example shows how to query over all the files in a specified directory tree, open
each file, and inspect its contents. This type of technique could be used to create
indexes or reverse indexes of the contents of a directory tree. A simple string search is
performed in this example. However, more complex types of pattern matching can be
performed with a regular expression. For more information, see How to combine LINQ
queries with regular expressions (C#) .
C#Example
class QueryContents   
{  
    public static void Main()  
    {  
        // Modify this path as necessary.  
        string startFolder = @"c:\program files\Microsoft Visual Studio  
9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new 
System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery  
permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles( "*.*", 
System.IO.SearchOption.AllDirectories);  
  
        string searchTerm = @"Visual Studio" ;  
  
        // Search the contents of each file.  
        // A regular expression created with the RegEx class  
        // could be used instead of the Contains method.  
        // queryMatchingFiles is an IEnumerable<string>.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = GetFileText(file.FullName)  
            where fileText.Contains(searchTerm)  
            select file.FullName;  
  
        // Execute the query.  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.        Console.WriteLine( "The term \"{0}\" was found in:" , searchTerm);  
        foreach (string filename in queryMatchingFiles)  
        {  
            Console.WriteLine(filename);  
        }  
    }  
  
    // Read the contents of the file.  
    static string GetFileText (string name)  
    {  
        string fileContents = String.Empty;  
  
        // If the file has been deleted since we took
        // the snapshot, ignore it and return the empty string.  
        if (System.IO.File.Exists(name))  
        {  
            fileContents = System.IO.File.ReadAllText(name);  
        }  
        return fileContents;  
    }  
}  
Compiling the Code
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
 Provide product feedbackHow to return a query from a method
Article •11/14/2023
This example shows how to return a query from a method as the return value and as an
out parameter.
Query objects are composable, meaning that you can return a query from a method.
Objects that represent queries do not store the resulting collection, but rather the steps
to produce the results when needed. The advantage of returning query objects from
methods is that they can be further composed or modified. Therefore any return value
or out parameter of a method that returns a query must also have that type. If a
method materializes a query into a concrete List<T>  or Array  type, it is considered to be
returning the query results instead of the query itself. A query variable that is returned
from a method can still be composed or modified.
In the following example, the first method QueryMethod1 returns a query as a return
value, and the second method QueryMethod2 returns a query as an out parameter
(returnQ in the example). Note that in both cases it is a query that is returned, not query
results.
C#
Query myQuery1 is executed in the following foreach loop.
C#Example
IEnumerable< string> QueryMethod1 (int[] ints) =>
    from i in ints
    where i > 4
    select i.ToString();
void QueryMethod2 (int[] ints, out IEnumerable< string> returnQ ) =>
    returnQ =
        from i in ints
        where i < 4
        select i.ToString();
int[] nums = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
var myQuery1 = QueryMethod1(nums);Rest the mouse pointer over myQuery1 to see its type.
You also can execute the query returned from QueryMethod1 directly, without using
myQuery1.
C#
Rest the mouse pointer over the call to QueryMethod1 to see its return type.
QueryMethod2 returns a query as the value of its out parameter:
C#
You can modify a query by using query composition. In this case, the previous query
object is used to create a new query object. This new object will return different results
than the original query object.
C#foreach (var s in myQuery1)
{
    Console.WriteLine(s);
}
foreach (var s in QueryMethod1 (nums))
{
    Console.WriteLine(s);
}
QueryMethod2(nums, out IEnumerable< string> myQuery2);
// Execute the returned query.
foreach (var s in myQuery2)
{
    Console.WriteLine(s);
}
myQuery1 =
    from item in myQuery1
    orderby item descending
    select item;
// Execute the modified query.
Console.WriteLine( "\nResults of executing modified myQuery1:" );
foreach (var s in myQuery1)
{Language Integrated Query (LINQ)    Console.WriteLine(s);
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
 Provide product feedbackDynamically specify predicate filters at
run time
Article •03/09/2023
In some cases, you don't know until run time how many predicates you have to apply to
source elements in the where clause. One way to dynamically specify multiple predicate
filters is to use the Contains  method, as shown in the following example. The query will
return different results based on the value of id when the query is executed.
C#
int[] ids = { 111, 114, 112 }; 
var queryNames =  
    from student in students  
    where ids.Contains(student.ID)  
    select new 
    { 
        student.LastName,  
        student.ID  
    }; 
foreach (var name in queryNames)  
{ 
    Console.WriteLine( $"{name.LastName} : {name.ID} "); 
} 
/* Output:  
    Garcia: 114  
    O'Donnell: 112  
    Omelchenko: 111  
 */ 
// Change the ids.  
ids = new[] { 122, 117, 120, 115 }; 
// The query will now return different results  
foreach (var name in queryNames)  
{ 
    Console.WriteLine( $"{name.LastName} : {name.ID} "); 
} 
/* Output:  
    Adams: 120  
    Feng: 117  
    Garcia: 115  
    Tucker: 122  
 */ You can use control flow statements, such as if... else or switch, to select among
predetermined alternative queries. In the following example, studentQuery uses a
different where clause if the runtime value of oddYear is true or false.
C#Using different queries at runtim e
void FilterByYearType (bool oddYear ) 
{ 
    IEnumerable<Student> studentQuery;  
    if (oddYear)  
    { 
        studentQuery =  
            from student in students  
            where student.Year == GradeLevel.FirstYear || student.Year ==  
GradeLevel.ThirdYear  
            select student;  
    } 
    else 
    { 
        studentQuery =  
            from student in students  
            where student.Year == GradeLevel.SecondYear || student.Year ==  
GradeLevel.FourthYear  
            select student;  
    } 
    string descr = oddYear ? "odd" : "even"; 
    Console.WriteLine( $"The following students are at an {descr} year 
level:"); 
    foreach (Student name in studentQuery)  
    { 
        Console.WriteLine( $"{name.LastName} : {name.ID} "); 
    } 
} 
FilterByYearType( true); 
/* Output:  
    The following students are at an odd year level:  
    Fakhouri: 116  
    Feng: 117  
    Garcia: 115  
    Mortensen: 113  
    Tucker: 119  
    Tucker: 122  
 */ 
FilterByYearType( false); 
/* Output:  Language Integrated Query (LINQ)
where clause
Querying based on runtime state    The following students are at an even year level:  
    Adams: 120  
    Garcia: 114  
    Garcia: 118  
    O'Donnell: 112  
    Omelchenko: 111  
    Zabokritski: 121  
 */ 
See alsoHandle null values in query expressions
Article •02/18/2022
This example shows how to handle possible null values in source collections. An object
collection such as an IEnumerable<T>  can contain elements whose value is null. If a
source collection is null or contains an element whose value is null, and your query
doesn't handle null values, a NullR eferenceException  will be thrown when you execute
the query.
You can code defensively to avoid a null reference exception as shown in the following
example:
C#
In the previous example, the where clause filters out all null elements in the categories
sequence. This technique is independent of the null check in the join clause. The
conditional expression with null in this example works because Products.CategoryID is
of type int?, which is shorthand for Nullable<int>.
In a join clause, if only one of the comparison keys is a nullable value type, you can cast
the other to a nullable value type in the query expression. In the following example,
assume that EmployeeID is a column that contains values of type int?:
C#var query1 =
    from c in categories
    where c != null
    join p in products on c.ID equals p?.CategoryID
    select new
    {
        Category = c.Name,
        Name = p.Name
    };
void TestMethod (Northwind db )
{
    var query =
        from o in db.Orders
        join e in db.Employees
            on o.EmployeeID equals (int?)e.EmployeeID
        select new { o.OrderID, e.FirstName };
}In each of the examples, the equals query keyword is used. Y ou can also use pattern
matching , which includes patterns for is null and is not null. These patterns aren't
recommended in LINQ queries because query providers may not interpret the new C#
syntax correctly. A query provider is a library that translates C# query expressions into a
native data format, such as Entity Framework Core. Query providers implement the
System.Linq.IQueryProvider  interface to create data sources that implement the
System.Linq.IQueryable<T>  interface.
Nullable<T>
Language Integrated Query (LINQ)
Nullable value typesSee also
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
 Provide product feedbackHandle exceptions in query expressions
Article •11/14/2023
It's possible to call any method in the context of a query expression. However, we
recommend that you avoid calling any method in a query expression that can create a
side effect such as modifying the contents of the data source or throwing an exception.
This example shows how to avoid raising exceptions when you call methods in a query
expression without violating the general .NET guidelines on exception handling. Those
guidelines state that it's acceptable to catch a specific exception when you understand
why it's thrown in a given context. For more information, see Best Practices for
Exceptions .
The final example shows how to handle those cases when you must throw an exception
during execution of a query.
The following example shows how to move exception handling code outside a query
expression. This is only possible when the method does not depend on any variables
local to the query. It is easier to deal with exceptions outside of the query expression.
C#Example 1
// A data source that is very likely to throw an exception!
IEnumerable< int> GetData() => throw new InvalidOperationException();
// DO THIS with a datasource that might
// throw an exception.
IEnumerable< int>? dataSource = null;
try
{
    dataSource = GetData();
}
catch (InvalidOperationException)
{
    Console.WriteLine( "Invalid operation" );
}
if (dataSource is not null)
{
    // If we get here, it is safe to proceed.
    var query =
        from i in dataSource
        select i * i;
    foreach (var i in query)Note that in the catch (InvalidOperationException) in the example above, handle (or
don't handle) the exception in the way that is appropriate for your application.
In some cases, the best response to an exception that is thrown from within a query
might be to stop the query execution immediately. The following example shows how to
handle exceptions that might be thrown from inside a query body. Assume that
SomeMethodThatMightThrow can potentially cause an exception that requires the query
execution to stop.
Note that the try block encloses the foreach loop, and not the query itself. This is
because the foreach loop is the point at which the query is actually executed. For more
information, see Introduction to LINQ queries . The runtime exception will only be
thrown when the query is executed. Therefore they must be handled in the foreach
loop.
C#    {
        Console.WriteLine(i.ToString());
    }
}
Example 2
// Not very useful as a general purpose method.
string SomeMethodThatMightThrow (string s) =>
    s[4] == 'C' ?
        throw new InvalidOperationException() :
        @"C:\newFolder\"  + s;
// Data source.
string[] files = { "fileA.txt" , "fileB.txt" , "fileC.txt"  };
// Demonstration query that throws.
var exceptionDemoQuery =
    from file in files
    let n = SomeMethodThatMightThrow(file)
    select n;
try
{
    foreach (var item in exceptionDemoQuery)
    {
        Console.WriteLine( $"Processing {item}");
    }
}Remember to catch whatever exception you expect to raise and/or do any necessary
cleanup in a finally block.
Language Integrated Query (LINQ)catch (InvalidOperationException e)
{
    Console.WriteLine(e.Message);
}
/* Output:
    Processing C:\newFolder\fileA.txt
    Processing C:\newFolder\fileB.txt
    Operation is not valid due to the current state of the object.
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
 Provide product feedbackHow to count occurrences of a word in a
string (LINQ) (C#)
Article •07/18/2023
This example shows how to use a LINQ query to count the occurrences of a specified
word in a string. Note that to perform the count, first the Split method is called to create
an array of words. There is a performance cost to the Split method. If the only operation
on the string is to count the words, you should consider using the Matches  or IndexOf
methods instead. However, if performance is not a critical issue, or you have already
split the sentence in order to perform other types of queries over it, then it makes sense
to use LINQ to count the words or phrases as well.
C#Example
class CountWords   
{  
    static void Main()  
    {  
        string text = @"Historically, the world of data and the world of  
objects"  +  
          @" have not been well integrated. Programmers work in C# or Visual  
Basic" +  
          @" and also in SQL or XQuery. On the one side are concepts such as  
classes,"  +  
          @" objects, fields, inheritance, and .NET APIs. On the other side"  
+  
          @" are tables, columns, rows, nodes, and separate languages for  
dealing with"  +  
          @" them. Data types often require translation between the two  
worlds; there are"  +  
          @" different standard functions. Because the object world has no  
notion of query, a"  +  
          @" query can only be represented as a string without compile-time  
type checking or"  +  
          @" IntelliSense support in the IDE. Transferring data from SQL  
tables or XML trees to"  +  
          @" objects in memory is often tedious and error-prone." ;  
  
        string searchTerm = "data";  
  
        //Convert the string into an array of words  
        string[] source = text.Split(
            ['.', '?', '!', ' ', ';', ':', ','],
            StringSplitOptions.RemoveEmptyEntries);  
  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.        // Create the query.  Use the InvariantCultureIgnoreCase comparison  
to match "data" and "Data"
        var matchQuery = from word in source  
                         where word.Equals(searchTerm,  
StringComparison.InvariantCultureIgnoreCase)  
                         select word;  
  
        // Count the matches, which executes the query.  
        int wordCount = matchQuery.Count();  
        Console.WriteLine( "{0} occurrences(s) of the search term \"{1}\"  
were found." , wordCount, searchTerm);  
    }  
}  
/* Output:  
   3 occurrences(s) of the search term "data" were found.  
*/  
Compiling the Code
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
 Provide product feedbackHow to query for sentences that contain
a specified set of words (LINQ) (C#)
Article •07/18/2023
This example shows how to find sentences in a text file that contain matches for each of
a specified set of words. Although the array of search terms is hard-coded in this
example, it could also be populated dynamically at run time. In this example, the query
returns the sentences that contain the words "Historically," "data," and "integrated."
C#Example
class FindSentences   
{  
    static void Main()  
    {  
        string text = @"Historically, the world of data and the world of  
objects "  +  
        @"have not been well integrated. Programmers work in C# or Visual  
Basic " +  
        @"and also in SQL or XQuery. On the one side are concepts such as  
classes, "  +  
        @"objects, fields, inheritance, and .NET APIs. On the other side "  +  
        @"are tables, columns, rows, nodes, and separate languages for  
dealing with "  +  
        @"them. Data types often require translation between the two worlds;  
there are "  +  
        @"different standard functions. Because the object world has no  
notion of query, a "  +  
        @"query can only be represented as a string without compile-time  
type checking or "  +  
        @"IntelliSense support in the IDE. Transferring data from SQL tables  
or XML trees to "  +  
        @"objects in memory is often tedious and error-prone." ;  
  
        // Split the text block into an array of sentences.  
        string[] sentences = text.Split([ '.', '?', '!' ]);  
  
        // Define the search terms. This list could also be dynamically  
populated at run time.  
        string[] wordsToMatch = { "Historically" , "data", "integrated"  };  
  
        // Find sentences that contain all the terms in the wordsToMatch  
array.  
        // Note that the number of terms to match is not specified at  
compile time.  
        var sentenceQuery = from sentence in sentences  The query works by first splitting the text into sentences, and then splitting the
sentences into an array of strings that hold each word. For each of these arrays, the
Distinct  method removes all duplicate words, and then the query performs an Intersect
operation on the word array and the wordsToMatch array. If the count of the intersection
is the same as the count of the wordsToMatch array, all words were found in the words
and the original sentence is returned.
In the call to Split, the punctuation marks are used as separators in order to remove
them from the string. If you did not do this, for example you could have a string
"Historically," that would not match "Historically" in the wordsToMatch array. Y ou may
have to use additional separators, depending on the types of punctuation found in the
source text.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.                            let w = sentence.Split([ '.', '?', '!', ' ', ';', 
':', ','],  
                                                    
StringSplitOptions.RemoveEmptyEntries)  
                            where 
w.Distinct().Intersect(wordsToMatch).Count() == wordsToMatch.Count()  
                            select sentence;  
  
        // Execute the query. Note that you can explicitly type  
        // the iteration variable here even though sentenceQuery  
        // was implicitly typed.
        foreach (string str in sentenceQuery)  
        {  
            Console.WriteLine(str);  
        }  
    }  
}  
/* Output:  
Historically, the world of data and the world of objects have not been well  
integrated  
*/  
Compiling the Code
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you.NET feedb ack
The .NET documentation is open
source. Provide feedback here.can also create and review
issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackHow to query for characters in a string
(LINQ) (C#)
Article •07/18/2023
Because the String  class implements the generic IEnumerable<T>  interface, any string
can be queried as a sequence of characters. However, this is not a common use of LINQ.
For complex pattern matching operations, use the Regex  class.
The following example queries a string to determine the number of numeric digits it
contains. Note that the query is "reused" after it is executed the first time. This is
possible because the query itself does not store any actual results.
C#Example
class QueryAString   
{  
    static void Main()  
    {  
        string aString = "ABCDE99F-J74-12-89A" ;  
  
        // Select only those characters that are numbers  
        IEnumerable< char> stringQuery =  
          from ch in aString  
          where Char.IsDigit(ch)  
          select ch;  
  
        // Execute the query  
        foreach (char c in stringQuery)  
            Console.Write(c + " ");  
  
        // Call the Count method on the existing query.  
        int count = stringQuery.Count();  
        Console.WriteLine( "Count = {0}" , count);  
  
        // Select all characters before the first '-'  
        IEnumerable< char> stringQuery2 = aString.TakeWhile(c => c != '-');  
  
        // Execute the second query  
        foreach (char c in stringQuery2)  
            Console.Write(c);  
  
        Console.WriteLine(System.Environment.NewLine + "Press any key to  
exit");  
        Console.ReadKey();  
    }  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.
How to combine LINQ queries with regular expressions (C#)}  
/* Output:  
  Output: 9 9 7 4 1 2 8 9  
  Count = 8  
  ABCDE99F  
*/  
Compiling the Code
See alsoHow to combine LINQ queries with
regular expressions (C#)
Article •07/18/2023
This example shows how to use the Regex  class to create a regular expression for more
complex matching in text strings. The LINQ query makes it easy to filter on exactly the
files that you want to search with the regular expression, and to shape the results.
C#Example
class QueryWithRegEx   
{  
    public static void Main()  
    {  
        // Modify this path as necessary so that it accesses your version of  
Visual Studio.  
        string startFolder = @"C:\Program Files (x86)\Microsoft Visual  
Studio 14.0\" ;  
        // One of the following paths may be more appropriate on your  
computer.  
        //string startFolder = @"C:\Program Files (x86)\Microsoft Visual  
Studio\2017\";  
  
        // Take a snapshot of the file system.  
        IEnumerable<System.IO.FileInfo> fileList = GetFiles(startFolder);  
  
        // Create the regular expression to find all things "Visual".  
        System.Text.RegularExpressions.Regex searchTerm =  
            new System.Text.RegularExpressions.Regex( @"Visual  
(Basic|C#|C\+\+|Studio)" );  
  
        // Search the contents of each .htm file.  
        // Remove the where clause to find even more matchedValues!  
        // This query produces a list of files where a match  
        // was found, and a list of the matchedValues in that file.  
        // Note: Explicit typing of "Match" in select clause.  
        // This is required because MatchCollection is not a
        // generic IEnumerable collection.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = System.IO.File.ReadAllText(file.FullName)  
            let matches = searchTerm.Matches(fileText)  
            where matches.Count > 0  
            select new  
            {  Note that you can also query the MatchCollection  object that is returned by a RegEx
search. In this example only the value of each match is produced in the results. However,
it is also possible to use LINQ to perform all kinds of filtering, sorting, and grouping on
that collection. Because MatchCollection  is a non-generic IEnumerable  collection, you
have to explicitly state the type of the range variable in the query.                name = file.FullName,  
                matchedValues = from System.Text.RegularExpressions.Match  
match in matches  
                                select match.Value  
            };  
  
        // Execute the query.  
        Console.WriteLine( "The term \"{0}\" was found in:" , 
searchTerm.ToString());  
  
        foreach (var v in queryMatchingFiles)  
        {  
            // Trim the path a bit, then write
            // the file name in which a match was found.  
            string s = v.name.Substring(startFolder.Length - 1);  
            Console.WriteLine(s);  
  
            // For this file, write out all the matching strings  
            foreach (var v2 in v.matchedValues)  
            {  
                Console.WriteLine( "  " + v2);  
            }  
        }  
   }  
  
    // This method assumes that the application has discovery
    // permissions for all folders under the specified path.  
    static IEnumerable<System.IO.FileInfo> GetFiles( string path)  
    {  
        if (!System.IO.Directory.Exists(path))  
            throw new System.IO.DirectoryNotFoundException();  
  
        string[] fileNames = null;  
        List<System.IO.FileInfo> files = new List<System.IO.FileInfo>();  
  
        fileNames = System.IO.Directory.GetFiles(path, "*.*", 
System.IO.SearchOption.AllDirectories);  
        foreach (string name in fileNames)  
        {  
            files.Add( new System.IO.FileInfo(name));  
        }  
        return files;  
    }  
}  Create a C# console application project with using directives for the S ystem.Linq and
System.IO namespaces.Compiling the Code
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
 Provide product feedbackHow to find the set difference between
two lists (LINQ) (C#)
Article •07/18/2023
This example shows how to use LINQ to compare two lists of strings and output those
lines that are in names1.txt but not in names2.txt.
1. Copy names1.txt and names2.txt to your solution folder as shown in How to
combine and compare string collections (LINQ) (C#) .
C#To create the data files
Example
class CompareLists   
{
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 =  
System.IO.File.ReadAllLines( @"../../../names1.txt" );  
        string[] names2 =  
System.IO.File.ReadAllLines( @"../../../names2.txt" );  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable< string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine( "The following lines are in names1.txt but not  
names2.txt" );  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open until the user presses a key.
        Console.WriteLine( "Press any key to exit" );  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  Some types of query operations in C#, such as Except , Distinct , Union , and Concat , can
only be expressed in method-based syntax.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
Compiling the CodeHow to sort or filter text data by any
word or field (LINQ) (C#)
Article •07/18/2023
The following example shows how to sort lines of structured text, such as comma-
separated values, by any field in the line. The field may be dynamically specified at run
time. Assume that the fields in scores.csv represent a student's ID number, followed by a
series of four test scores.
1. Copy the scores.csv data from the topic How to join content from dissimilar files
(LINQ) (C#)  and save it to your solution folder.
C#To create a file that contains data
Example
public class SortLines   
{  
    static void Main()  
    {  
        // Create an IEnumerable data source  
        string[] scores =  
System.IO.File.ReadAllLines( @"../../../scores.csv" );  
  
        // Change this to any value from 0 to 4.  
        int sortField = 1;  
  
        Console.WriteLine( "Sorted highest to lowest by field [{0}]:" , 
sortField);  
  
        // Demonstrates how to return query from a method.  
        // The query is executed here.  
        foreach (string str in RunQuery (scores, sortField ))  
        {  
            Console.WriteLine(str);  
        }  
    }  
  
    // Returns the query variable, not query results!  
    static IEnumerable< string> RunQuery (IEnumerable< string> source, int num)  
    {  
        // Split the string and sort on field[num]  
        var scoreQuery = from line in source  
                         let fields = line.Split( ',')  This example also demonstrates how to return a query variable from a method.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.                         orderby fields[num] descending   
                         select line;  
  
        return scoreQuery;  
    }  
}  
/* Output (if sortField == 1):  
   Sorted highest to lowest by field [1]:  
    116, 99, 86, 90, 94  
    120, 99, 82, 81, 79  
    111, 97, 92, 81, 60  
    114, 97, 89, 85, 82  
    121, 96, 85, 91, 60  
    122, 94, 92, 91, 91  
    117, 93, 92, 80, 87  
    118, 92, 90, 83, 78  
    113, 88, 94, 65, 91  
    112, 75, 84, 91, 39  
    119, 68, 79, 88, 92  
    115, 35, 72, 91, 70  
 */  
Compiling the Code
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
 Provide product feedbackHow to reorder the fields of a delimited
file (LINQ) (C#)
Article •07/18/2023
A comma-separated value (CSV) file is a text file that is often used to store spreadsheet
data or other tabular data that is represented by rows and columns. By using the Split
method to separate the fields, it is very easy to query and manipulate CSV files by using
LINQ. In fact, the same technique can be used to reorder the parts of any structured line
of text; it is not limited to CSV files.
In the following example, assume that the three columns represent students' "last
name," "first name", and "ID." The fields are in alphabetical order based on the students'
last names. The query produces a new sequence in which the ID column appears first,
followed by a second column that combines the student's first name and last name. The
lines are reordered according to the ID field. The results are saved into a new file and
the original data is not modified.
1. Copy the following lines into a plain text file that is named spreadsheet1.csv. Save
the file in your project folder.
csv
C#To create the data file
Adams,Terry,120  
Fakhouri,Fadi,116  
Feng,Hanying,117  
Garcia,Cesar,114  
Garcia,Debra,115  
Garcia,Hugo,118  
Mortensen,Sven,113  
O'Donnell,Claire,112  
Omelchenko,Svetlana,111  
Tucker,Lance,119  
Tucker,Michael,122  
Zabokritski,Eugene,121  
ExampleCreate a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.class CSVFiles   
{  
    static void Main(string[] args)  
    {  
        // Create the IEnumerable data source  
        string[] lines =  
System.IO.File.ReadAllLines( @"../../../spreadsheet1.csv" );  
  
        // Create the query. Put field 2 first, then  
        // reverse and combine fields 0 and 1 from the old field  
        IEnumerable< string> query =  
            from line in lines  
            let x = line.Split( ',')  
            orderby x[2]  
            select x[2] + ", " + (x[1] + " " + x[0]);  
  
        // Execute the query and write out the new file. Note that  
WriteAllLines  
        // takes a string[], so ToArray is called on the query.  
        System.IO.File.WriteAllLines( @"../../../spreadsheet2.csv" , 
query.ToArray());  
  
        Console.WriteLine( "Spreadsheet2.csv written to disk. Press any key  
to exit" );  
        Console.ReadKey();  
    }  
}  
/* Output to spreadsheet2.csv:  
111, Svetlana Omelchenko  
112, Claire O'Donnell  
113, Sven Mortensen  
114, Cesar Garcia  
115, Debra Garcia  
116, Fadi Fakhouri  
117, Hanying Feng  
118, Hugo Garcia  
119, Lance Tucker  
120, Terry Adams  
121, Eugene Zabokritski  
122, Michael Tucker  
 */  
Compiling the CodeHow to combine and compare string
collections (LINQ) (C#)
Article •07/18/2023
This example shows how to merge files that contain lines of text and then sort the
results. Specifically, it shows how to perform a simple concatenation, a union, and an
intersection on the two sets of text lines.
1. Copy these names into a text file that is named names1.txt and save it in your
project folder:
text
2. Copy these names into a text file that is named names2.txt and save it in your
project folder. Note that the two files have some names in common.
textTo set up the project and the text files
Bankov, Peter  
Holm, Michael  
Garcia, Hugo  
Potra, Cristina  
Noriega, Fabricio  
Aw, Kam Foo  
Beebe, Ann  
Toyoshima, Tim  
Guy, Wey Yuan  
Garcia, Debra  
Liu, Jinghao  
Bankov, Peter  
Holm, Michael  
Garcia, Hugo  
Beebe, Ann  
Gilchrist, Beth  
Myrcha, Jacek  
Giakoumakis, Leo  
McLin, Nkenge  
El Yassir, Mehdi  
ExampleC#
class MergeStrings   
    {  
        static void Main(string[] args)  
        {  
            //Put text files in your solution folder  
            string[] fileA =  
System.IO.File.ReadAllLines( @"../../../names1.txt" );  
            string[] fileB =  
System.IO.File.ReadAllLines( @"../../../names2.txt" );  
  
            //Simple concatenation and sort. Duplicates are preserved.  
            IEnumerable< string> concatQuery =  
                fileA.Concat(fileB).OrderBy(s => s);  
  
            // Pass the query variable to another function for execution.  
            OutputQueryResults(concatQuery, "Simple concatenate and sort.  
Duplicates are preserved:" );  
  
            // Concatenate and remove duplicate names based on  
            // default string comparer.  
            IEnumerable< string> uniqueNamesQuery =  
                fileA.Union(fileB).OrderBy(s => s);  
            OutputQueryResults(uniqueNamesQuery, "Union removes duplicate  
names:");  
  
            // Find the names that occur in both files (based on  
            // default string comparer).  
            IEnumerable< string> commonNamesQuery =  
                fileA.Intersect(fileB);  
            OutputQueryResults(commonNamesQuery, "Merge based on  
intersect:" );  
  
            // Find the matching fields in each list. Merge the two
            // results by using Concat, and then  
            // sort using the default string comparer.  
            string nameMatch = "Garcia" ;  
  
            IEnumerable<String> tempQuery1 =  
                from name in fileA  
                let n = name.Split( ',')  
                where n[0] == nameMatch  
                select name;  
  
            IEnumerable< string> tempQuery2 =  
                from name2 in fileB  
                let n2 = name2.Split( ',')  
                where n2[0] == nameMatch  
                select name2;  
  
            IEnumerable< string> nameMatchQuery =  
                tempQuery1.Concat(tempQuery2).OrderBy(s => s);  
            OutputQueryResults(nameMatchQuery, $"Concat based on partial  name match \" {nameMatch} \":");
        }  
  
        static void OutputQueryResults (IEnumerable< string> query, string 
message)  
        {  
            Console.WriteLine(System.Environment.NewLine + message);  
            foreach (string item in query)  
            {  
                Console.WriteLine(item);  
            }  
            Console.WriteLine( "{0} total names in list" , query.Count());  
        }  
    }  
    /* Output:  
        Simple concatenate and sort. Duplicates are preserved:  
        Aw, Kam Foo  
        Bankov, Peter  
        Bankov, Peter  
        Beebe, Ann  
        Beebe, Ann  
        El Yassir, Mehdi  
        Garcia, Debra  
        Garcia, Hugo  
        Garcia, Hugo  
        Giakoumakis, Leo  
        Gilchrist, Beth  
        Guy, Wey Yuan  
        Holm, Michael  
        Holm, Michael  
        Liu, Jinghao  
        McLin, Nkenge  
        Myrcha, Jacek  
        Noriega, Fabricio  
        Potra, Cristina  
        Toyoshima, Tim  
        20 total names in list  
  
        Union removes duplicate names:  
        Aw, Kam Foo  
        Bankov, Peter  
        Beebe, Ann  
        El Yassir, Mehdi  
        Garcia, Debra  
        Garcia, Hugo  
        Giakoumakis, Leo  
        Gilchrist, Beth  
        Guy, Wey Yuan  
        Holm, Michael  
        Liu, Jinghao  
        McLin, Nkenge  
        Myrcha, Jacek  
        Noriega, Fabricio  
        Potra, Cristina  
        Toyoshima, Tim  Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.        16 total names in list  
  
        Merge based on intersect:  
        Bankov, Peter  
        Holm, Michael  
        Garcia, Hugo  
        Beebe, Ann  
        4 total names in list  
  
        Concat based on partial name match "Garcia":  
        Garcia, Debra  
        Garcia, Hugo  
        Garcia, Hugo  
        3 total names in list  
*/  
Compiling the Code
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
 Provide product feedbackHow to populate object collections from
multiple sources (LINQ) (C#)
Article •07/18/2023
This example shows how to merge data from different sources into a sequence of new
types.
Copy the names.csv and scores.csv files into your project folder, as described in How to
join content from dissimilar files (LINQ) (C#) .
The following example shows how to use a named type Student to store merged data
from two in-memory collections of strings that simulate spreadsheet data in .csv format.
The first collection of strings represents the student names and IDs, and the second
collection represents the student ID (in the first column) and four exam scores. The ID is
used as the foreign key.
C#７ Note
Don't try to join in-memory data or data in the file system with data that is still in a
database. Such cross-domain joins can yield undefined results because of different
ways in which join operations might be defined for database queries and other
types of sources. Additionally, there is a risk that such an operation could cause an
out-of-memory exception if the amount of data in the database is large enough. T o
join data from a database to in-memory data, first call ToList or ToArray on the
database query, and then perform the join on the returned collection.
To create the data file
Example
using System;
using System.Collections.Generic;
using System.Linq;
class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }    public int ID { get; set; }
    public List<int> ExamScores { get; set; }
}
class PopulateCollection
{
    static void Main()
    {
        // These data files are defined in How to join content from
        // dissimilar files (LINQ).
        // Each line of names.csv consists of a last name, a first name, and  
an
        // ID number, separated by commas. For example,  
Omelchenko,Svetlana,111
        string[] names = System.IO.File.ReadAllLines( @"../../../names.csv" );
        // Each line of scores.csv consists of an ID number and four test
        // scores, separated by commas. For example, 111, 97, 92, 81, 60
        string[] scores =  
System.IO.File.ReadAllLines( @"../../../scores.csv" );
        // Merge the data sources using a named type.
        // var could be used instead of an explicit type. Note the dynamic
        // creation of a list of ints for the ExamScores member. The first  
item
        // is skipped in the split string because it is the student ID,
        // not an exam score.
        IEnumerable<Student> queryNamesScores =
            from nameLine in names
            let splitName = nameLine.Split( ',')
            from scoreLine in scores
            let splitScoreLine = scoreLine.Split( ',')
            where Convert.ToInt32(splitName[ 2]) == 
Convert.ToInt32(splitScoreLine[ 0])
            select new Student()
            {
                FirstName = splitName[ 0],
                LastName = splitName[ 1],
                ID = Convert.ToInt32(splitName[ 2]),
                ExamScores = ( from scoreAsText in splitScoreLine.Skip( 1)
                              select Convert.ToInt32(scoreAsText)).
                              ToList()
            };
        // Optional. Store the newly created student objects in memory
        // for faster access in future queries. This could be useful with
        // very large data files.
        List<Student> students = queryNamesScores.ToList();
        // Display each student's name and exam score average.
        foreach (var student in students)
        {
            Console.WriteLine( "The average score of {0} {1} is {2}." ,
                student.FirstName, student.LastName,In the select  clause, an object initializer is used to instantiate each new Student object
by using the data from the two sources.
If you don't have to store the results of a query, anonymous types can be more
convenient than named types. Named types are required if you pass the query results
outside the method in which the query is executed. The following example executes the
same task as the previous example, but uses anonymous types instead of named types:
C#                student.ExamScores.Average());
        }
        //Keep console window open in debug mode
        Console.WriteLine( "Press any key to exit." );
        Console.ReadKey();
    }
}
/* Output:
    The average score of Omelchenko Svetlana is 82.5.
    The average score of O'Donnell Claire is 72.25.
    The average score of Mortensen Sven is 84.5.
    The average score of Garcia Cesar is 88.25.
    The average score of Garcia Debra is 67.
    The average score of Fakhouri Fadi is 92.25.
    The average score of Feng Hanying is 88.
    The average score of Garcia Hugo is 85.75.
    The average score of Tucker Lance is 81.75.
    The average score of Adams Terry is 85.25.
    The average score of Zabokritski Eugene is 83.
    The average score of Tucker Michael is 92.
 */
// Merge the data sources by using an anonymous type.
// Note the dynamic creation of a list of ints for the
// ExamScores member. We skip 1 because the first string
// in the array is the student ID, not an exam score.
var queryNamesScores2 =
    from nameLine in names
    let splitName = nameLine.Split( ',')
    from scoreLine in scores
    let splitScoreLine = scoreLine.Split( ',')
    where Convert.ToInt32(splitName[ 2]) == 
Convert.ToInt32(splitScoreLine[ 0])
    select new
    {
        First = splitName[ 0],
        Last = splitName[ 1],
        ExamScores = ( from scoreAsText in splitScoreLine.Skip( 1)
                      select Convert.ToInt32(scoreAsText))
                      .ToList()
    };Object and Collection Initializers
Anonymous T ypes// Display each student's name and exam score average.
foreach (var student in queryNamesScores2)
{
    Console.WriteLine( "The average score of {0} {1} is {2}." ,
        student.First, student.Last, student.ExamScores.Average());
}
See alsoHow to split a file into many files by
using groups (LINQ) (C#)
Article •07/18/2023
This example shows one way to merge the contents of two files and then create a set of
new files that organize the data in a new way.
1. Copy these names into a text file that is named names1.txt and save it in your
project folder:
text
2. Copy these names into a text file that is named names2.txt and save it in your
project folder: Note that the two files have some names in common.
textTo create the data files
Bankov, Peter  
Holm, Michael  
Garcia, Hugo  
Potra, Cristina  
Noriega, Fabricio  
Aw, Kam Foo  
Beebe, Ann  
Toyoshima, Tim  
Guy, Wey Yuan  
Garcia, Debra  
Liu, Jinghao  
Bankov, Peter  
Holm, Michael  
Garcia, Hugo  
Beebe, Ann  
Gilchrist, Beth  
Myrcha, Jacek  
Giakoumakis, Leo  
McLin, Nkenge  
El Yassir, Mehdi  
ExampleC#
class SplitWithGroups   
{  
    static void Main()  
    {  
        string[] fileA =  
System.IO.File.ReadAllLines( @"../../../names1.txt" );  
        string[] fileB =  
System.IO.File.ReadAllLines( @"../../../names2.txt" );  
  
        // Concatenate and remove duplicate names based on  
        // default string comparer  
        var mergeQuery = fileA.Union(fileB);  
  
        // Group the names by the first letter in the last name.  
        var groupQuery = from name in mergeQuery  
                         let n = name.Split( ',')  
                         group name by n[0][0] into g  
                         orderby g.Key  
                         select g;  
  
        // Create a new file for each group that was created  
        // Note that nested foreach loops are required to access  
        // individual items with each group.  
        foreach (var g in groupQuery)  
        {  
            // Create the new file name.  
            string fileName = @"../../../testFile_"  + g.Key + ".txt";  
  
            // Output to display.  
            Console.WriteLine(g.Key);  
  
            // Write file.  
            using (System.IO.StreamWriter sw = new 
System.IO.StreamWriter(fileName))  
            {  
                foreach (var item in g)  
                {  
                    sw.WriteLine(item);  
                    // Output to console for example purposes.  
                    Console.WriteLine( "   {0}" , item);  
                }  
            }  
        }  
        // Keep console window open in debug mode.  
        Console.WriteLine( "Files have been written. Press any key to exit" );  
        Console.ReadKey();  
    }  
}  
/* Output:
    A  
       Aw, Kam Foo  
    B  The program writes a separate file for each group in the same folder as the data files.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.       Bankov, Peter  
       Beebe, Ann  
    E  
       El Yassir, Mehdi  
    G  
       Garcia, Hugo  
       Guy, Wey Yuan  
       Garcia, Debra  
       Gilchrist, Beth  
       Giakoumakis, Leo  
    H  
       Holm, Michael  
    L  
       Liu, Jinghao  
    M  
       Myrcha, Jacek  
       McLin, Nkenge  
    N  
       Noriega, Fabricio  
    P  
       Potra, Cristina  
    T  
       Toyoshima, Tim  
 */  
Compiling the CodeHow to join content from dissimilar files
(LINQ) (C#)
Article •07/18/2023
This example shows how to join data from two comma-delimited files that share a
common value that is used as a matching key. This technique can be useful if you have
to combine data from two spreadsheets, or from a spreadsheet and from a file that has
another format, into a new file. Y ou can modify the example to work with any kind of
structured text.
1. Copy the following lines into a file that is named scores.csv and save it to your
project folder. The file represents spreadsheet data. Column 1 is the student's ID,
and columns 2 through 5 are test scores.
csv
2. Copy the following lines into a file that is named names.cs v and save it to your
project folder. The file represents a spreadsheet that contains the student's last
name, first name, and student ID.
csvTo create the data files
111, 97, 92, 81, 60  
112, 75, 84, 91, 39  
113, 88, 94, 65, 91  
114, 97, 89, 85, 82  
115, 35, 72, 91, 70  
116, 99, 86, 90, 94  
117, 93, 92, 80, 87  
118, 92, 90, 83, 78  
119, 68, 79, 88, 92  
120, 99, 82, 81, 79  
121, 96, 85, 91, 60  
122, 94, 92, 91, 91  
Omelchenko,Svetlana,111  
O'Donnell,Claire,112  
Mortensen,Sven,113  
Garcia,Cesar,114  
Garcia,Debra,115  
Fakhouri,Fadi,116  
Feng,Hanying,117  C#Garcia,Hugo,118  
Tucker,Lance,119  
Adams,Terry,120  
Zabokritski,Eugene,121  
Tucker,Michael,122  
Example
using System;
using System.Collections.Generic;
using System.Linq;
class JoinStrings   
{  
    static void Main()  
    {  
        // Join content from dissimilar files that contain  
        // related information. File names.csv contains the student  
        // name plus an ID number. File scores.csv contains the ID
        // and a set of four test scores. The following query joins  
        // the scores to the student names by using ID as a  
        // matching key.  
  
        string[] names = System.IO.File.ReadAllLines( @"../../../names.csv" );  
        string[] scores =  
System.IO.File.ReadAllLines( @"../../../scores.csv" );  
  
        // Name:    Last[0],       First[1],  ID[2]  
        //          Omelchenko,    Svetlana,  11  
        // Score:   StudentID[0],  Exam1[1]   Exam2[2],  Exam3[3],  Exam4[4]   
        //          111,           97,        92,        81,        60  
  
        // This query joins two dissimilar spreadsheets based on common ID  
value.  
        // Multiple from clauses are used instead of a join clause  
        // in order to store results of id.Split.  
        IEnumerable< string> scoreQuery1 =  
            from name in names  
            let nameFields = name.Split( ',')  
            from id in scores  
            let scoreFields = id.Split( ',')  
            where Convert.ToInt32(nameFields[ 2]) == 
Convert.ToInt32(scoreFields[ 0])
            select nameFields[ 0] + "," + scoreFields[ 1] + "," + 
scoreFields[ 2]
                   + "," + scoreFields[ 3] + "," + scoreFields[ 4];  
  
        // Pass a query variable to a method and execute it  
        // in the method. The query itself is unchanged.  
        OutputQueryResults(scoreQuery1, "Merge two spreadsheets:" );    
        // Keep console window open in debug mode.  
        Console.WriteLine( "Press any key to exit" );  
        Console.ReadKey();  
    }  
  
    static void OutputQueryResults (IEnumerable< string> query, string 
message)  
    {  
        Console.WriteLine(System.Environment.NewLine + message);  
        foreach (string item in query)  
        {  
            Console.WriteLine(item);  
        }  
        Console.WriteLine( "{0} total names in list" , query.Count());  
    }  
}  
/* Output:  
Merge two spreadsheets:
Omelchenko, 97, 92, 81, 60
O'Donnell, 75, 84, 91, 39
Mortensen, 88, 94, 65, 91
Garcia, 97, 89, 85, 82
Garcia, 35, 72, 91, 70
Fakhouri, 99, 86, 90, 94
Feng, 93, 92, 80, 87
Garcia, 92, 90, 83, 78
Tucker, 68, 79, 88, 92
Adams, 99, 82, 81, 79
Zabokritski, 96, 85, 91, 60
Tucker, 94, 92, 91, 91
12 total names in list
 */  How to compute column values in a CSV
text file (LINQ) (C#)
Article •07/18/2023
This example shows how to perform aggregate computations such as Sum, A verage,
Min, and Max on the columns of a .csv file. The example principles that are shown here
can be applied to other types of structured text.
1. Copy the following lines into a file that is named scores.csv and save it in your
project folder. Assume that the first column represents a student ID, and
subsequent columns represent scores from four exams.
csv
C#To create the source file
111, 97, 92, 81, 60  
112, 75, 84, 91, 39  
113, 88, 94, 65, 91  
114, 97, 89, 85, 82  
115, 35, 72, 91, 70  
116, 99, 86, 90, 94  
117, 93, 92, 80, 87  
118, 92, 90, 83, 78  
119, 68, 79, 88, 92  
120, 99, 82, 81, 79  
121, 96, 85, 91, 60  
122, 94, 92, 91, 91  
Example
class SumColumns   
{  
    static void Main(string[] args)  
    {  
        string[] lines =  
System.IO.File.ReadAllLines( @"../../../scores.csv" );  
  
        // Specifies the column to compute.  
        int exam = 3;  
  
        // Spreadsheet format:          // Student ID    Exam#1  Exam#2  Exam#3  Exam#4  
        // 111,          97,     92,     81,     60  
  
        // Add one to exam to skip over the first column,  
        // which holds the student ID.  
        SingleColumn(lines, exam + 1);  
        Console.WriteLine();  
        MultiColumns(lines);  
  
        Console.WriteLine( "Press any key to exit" );  
        Console.ReadKey();  
    }  
  
    static void SingleColumn (IEnumerable< string> strs, int examNum )  
    {  
        Console.WriteLine( "Single Column Query:" );  
  
        // Parameter examNum specifies the column to
        // run the calculations on. This value could be  
        // passed in dynamically at run time.
  
        // Variable columnQuery is an IEnumerable<int>.  
        // The following query performs two steps:  
        // 1) use Split to break each row (a string) into an array
        //    of strings,
        // 2) convert the element at position examNum to an int  
        //    and select it.  
        var columnQuery =  
            from line in strs  
            let elements = line.Split( ',')  
            select Convert.ToInt32(elements[examNum]);  
  
        // Execute the query and cache the results to improve  
        // performance. This is helpful only with very large files.  
        var results = columnQuery.ToList();  
  
        // Perform aggregate calculations Average, Max, and  
        // Min on the column specified by examNum.  
        double average = results.Average();  
        int max = results.Max();  
        int min = results.Min();  
  
        Console.WriteLine( "Exam #{0}: Average:{1:##.##} High Score:{2} Low  
Score:{3}" ,  
                 examNum, average, max, min);  
    }  
  
    static void MultiColumns (IEnumerable< string> strs)  
    {  
        Console.WriteLine( "Multi Column Query:" );  
  
        // Create a query, multiColQuery. Explicit typing is used  
        // to make clear that, when executed, multiColQuery produces
        // nested sequences. However, you get the same results by  
        // using 'var'.    
        // The multiColQuery query performs the following steps:  
        // 1) use Split to break each row (a string) into an array
        //    of strings,
        // 2) use Skip to skip the "Student ID" column, and store the
        //    rest of the row in scores.  
        // 3) convert each score in the current row from a string to  
        //    an int, and select that entire sequence as one row
        //    in the results.  
        IEnumerable<IEnumerable< int>> multiColQuery =  
            from line in strs  
            let elements = line.Split( ',')  
            let scores = elements.Skip( 1)  
            select (from str in scores  
                    select Convert.ToInt32(str));  
  
        // Execute the query and cache the results to improve  
        // performance.
        // ToArray could be used instead of ToList.  
        var results = multiColQuery.ToList();  
  
        // Find out how many columns you have in results.  
        int columnCount = results[ 0].Count();  
  
        // Perform aggregate calculations Average, Max, and  
        // Min on each column.
        // Perform one iteration of the loop for each column
        // of scores.  
        // You can use a for loop instead of a foreach loop
        // because you already executed the multiColQuery
        // query by calling ToList.  
        for (int column = 0; column < columnCount; column++)  
        {  
            var results2 = from row in results  
                           select row.ElementAt(column);  
            double average = results2.Average();  
            int max = results2.Max();  
            int min = results2.Min();  
  
            // Add one to column because the first exam is Exam #1,  
            // not Exam #0.  
            Console.WriteLine( "Exam #{0} Average: {1:##.##} High Score: {2}  
Low Score: {3}" ,  
                          column + 1, average, max, min);  
        }  
    }  
}  
/* Output:  
    Single Column Query:  
    Exam #4: Average:76.92 High Score:94 Low Score:39  
  
    Multi Column Query:  
    Exam #1 Average: 86.08 High Score: 99 Low Score: 35  
    Exam #2 Average: 86.42 High Score: 94 Low Score: 72  
    Exam #3 Average: 84.75 High Score: 91 Low Score: 65  The query works by using the Split method to convert each line of text into an array.
Each array element represents a column. Finally, the text in each column is converted to
its numeric representation. If your file is a tab-separated file, just update the argument
in the Split method to \t.
Create a C# console application project, with using directives for the S ystem.Linq and
System.IO namespaces.    Exam #4 Average: 76.92 High Score: 94 Low Score: 39  
 */  
Compiling the CodeQuerying based on runtime state (C#)
Article •03/09/2023
Consider code that defines an IQueryable  or an IQueryable<T>  against a data source:
C#
Every time you run this code, the same exact query will be executed. This is frequently
not very useful, as you may want your code to execute different queries depending on
conditions at run time. This article describes how you can execute a different query
based on runtime state.
Fundamentally, an IQueryable  has two components:
Expression —a language- and datasource-agnostic representation of the current
query's components, in the form of an expression tree.
Provider —an instance of a LINQ provider, which knows how to materialize the
current query into a value or set of values.７ Note
Make sure you add using System.Linq.Expressions; and using static
System.Linq.Expressions.Expression; at the top of your .cs file.
var companyNames = new[] {
    "Consolidated Messenger" , "Alpine Ski House" , "Southridge Video" ,
    "City Power & Light" , "Coho Winery" , "Wide World Importers" ,
    "Graphic Design Institute" , "Adventure Works" , "Humongous Insurance" ,
    "Woodgrove Bank" , "Margie's Travel" , "Northwind Traders" ,
    "Blue Yonder Airlines" , "Trey Research" , "The Phone Company" ,
    "Wingtip Toys" , "Lucerne Publishing" , "Fourth Coffee"
};
// We're using an in-memory array as the data source, but the IQueryable  
could have come
// from anywhere -- an ORM backed by a database, a web request, or any other  
LINQ provider.
IQueryable< string> companyNamesSource = companyNames.AsQueryable();
var fixedQry = companyNames.OrderBy(x => x);
IQueryable / IQueryable<T> and expression
treesIn the context of dynamic querying, the provider will usually remain the same; the
expression tree of the query will differ from query to query.
Expression trees are immutable; if you want a different expression tree—and thus a
different query—you'll need to translate the existing expression tree to a new one, and
thus to a new IQueryable .
The following sections describe specific techniques for querying differently in response
to runtime state:
Use runtime state from within the expression tree
Call additional LINQ methods
Vary the expression tree passed into the LINQ methods
Construct an Expression<TDelegate>  expression tree using the factory methods at
Expression
Add method call nodes to an IQueryable 's expression tree
Construct strings, and use the Dynamic LINQ library
Assuming the LINQ provider supports it, the simplest way to query dynamically is to
reference the runtime state directly in the query via a closed-over variable, such as
length in the following code example:
C#
The internal expression tree—and thus the query—haven't been modified; the query
returns different values only because the value of length has been changed.
Use runtim e state from within the expression
tree
var length = 1;
var qry = companyNamesSource
    .Select(x => x.Substring( 0, length))
    .Distinct();
Console.WriteLine( string.Join(",", qry));
// prints: C, A, S, W, G, H, M, N, B, T, L, F
length = 2;
Console.WriteLine( string.Join(",", qry));
// prints: Co, Al, So, Ci, Wi, Gr, Ad, Hu, Wo, Ma, No, Bl, Tr, Th, Lu, Fo
Call additional LINQ methodsGenerally, the built-in LINQ methods  at Queryable  perform two steps:
Wrap the current expression tree in a MethodCallExpression  representing the
method call.
Pass the wrapped expression tree back to the provider, either to return a value via
the provider's IQueryProvider.Execute  method; or to return a translated query
object via the IQueryProvider.CreateQuery  method.
You can replace the original query with the result of an IQueryable<T> -returning
method, to get a new query. Y ou can do this conditionally based on runtime state, as in
the following example:
C#
You can pass in different expressions to the LINQ methods, depending on runtime state:
C#
You might also want to compose the various subexpressions using a third-party library
such as LinqKit 's PredicateBuilder :
// bool sortByLength = /* ... */;
var qry = companyNamesSource;
if (sortByLength)
{
    qry = qry.OrderBy(x => x.Length);
}
Vary the expression tree passed into the LINQ
methods
// string? startsWith = /* ... */;
// string? endsWith = /* ... */;
Expression<Func< string, bool>> expr = (startsWith, endsWith) switch
{
    ("" or null, "" or null) => x => true,
    (_, "" or null) => x => x.StartsWith(startsWith),
    ("" or null, _) => x => x.EndsWith(endsWith),
    (_, _) => x => x.StartsWith(startsWith) || x.EndsWith(endsWith)
};
var qry = companyNamesSource.Where(expr);
C#
In all the examples up to this point, we've known the element type at compile time—
string—and thus the type of the query— IQueryable<string>. You may need to add
components to a query of any element type, or to add different components, depending
on the element type. Y ou can create expression trees from the ground up, using the
factory methods at System.Linq.Expressions.Expression , and thus tailor the expression at
run time to a specific element type.
When you construct an expression to pass into one of the LINQ methods, you're actually
constructing an instance of Expression<TDelegate> , where TDelegate is some delegate
type such as Func<string, bool>, Action, or a custom delegate type.
Expression<TDelegate>  inherits from LambdaExpression , which represents a complete
lambda expression like the following:
C#// This is functionally equivalent to the previous example.
// using LinqKit;
// string? startsWith = /* ... */;
// string? endsWith = /* ... */;
Expression<Func< string, bool>>? expr = PredicateBuilder.New< string>(false);
var original = expr;
if (!string.IsNullOrEmpty(startsWith))
{
    expr = expr.Or(x => x.StartsWith(startsWith));
}
if (!string.IsNullOrEmpty(endsWith))
{
    expr = expr.Or(x => x.EndsWith(endsWith));
}
if (expr == original)
{
    expr = x => true;
}
var qry = companyNamesSource.Where(expr);
Construct expression trees and queries using
factory methods
Constructing an Expression<TDelegate>A LambdaExpression  has two components:
A parameter list— (string x)—represented by the Parameters  property.
A body— x.StartsWith("a")—represented by the Body  property.
The basic steps in constructing an Expression<TDelegate>  are as follows:
Define ParameterExpression  objects for each of the parameters (if any) in the
lambda expression, using the Parameter  factory method.
C#
Construct the body of your LambdaExpression , using the ParameterExpression (s)
you've defined, and the factory methods at Expression . For instance, an expression
representing x.StartsWith("a") could be constructed like this:
C#
Wrap the parameters and body in a compile-time-typed Expression<TDelegate> ,
using the appropriate Lambda  factory method overload:
C#
The following sections describe a scenario in which you might want to construct an
Expression<TDelegate>  to pass into a LINQ method, and provide a complete example
of how to do so using the factory methods.
Let's say you have multiple entity types:Expression<Func< string, bool>> expr = x => x.StartsWith( "a");
ParameterExpression x = Expression.Parameter( typeof(string), "x");
Expression body = Call(
    x,
    typeof(string).GetMethod( "StartsWith" , new[] { typeof(string) })!,
    Constant( "a")
);
Expression<Func< string, bool>> expr = Lambda<Func< string, bool>>(body,  
x);
ScenarioC#
For any of these entity types, you want to filter and return only those entities that have a
given text inside one of their string fields. For Person, you'd want to search the
FirstName and LastName properties:
C#
But for Car, you'd want to search only the Model property:
C#
While you could write one custom function for IQueryable<Person> and another for
IQueryable<Car>, the following function adds this filtering to any existing query,
irrespective of the specific element type.
C#record Person(string LastName, string FirstName, DateTime DateOfBirth );
record Car(string Model, int Year);
string term = /* ... */ ;
var personsQry = new List<Person>()
    .AsQueryable()
    .Where(x => x.FirstName.Contains(term) || x.LastName.Contains(term));
string term = /* ... */ ;
var carsQry = new List<Car>()
    .AsQueryable()
    .Where(x => x.Model.Contains(term));
Example
// using static System.Linq.Expressions.Expression;
IQueryable<T> TextFilter<T>(IQueryable<T> source, string term)
{
    if (string.IsNullOrEmpty(term)) { return source; }
    // T is a compile-time placeholder for the element type of the query.
    Type elementType = typeof(T);
    // Get all the string properties on this specific type.
    PropertyInfo[] stringProperties =
        elementType.GetProperties()
            .Where(x => x.PropertyType == typeof(string))Because the TextFilter function takes and returns an IQueryable<T>  (and not just an
IQueryable ), you can add further compile-time-typed query elements after the text filter.
C#            .ToArray();
    if (!stringProperties.Any()) { return source; }
    // Get the right overload of String.Contains
    MethodInfo containsMethod = typeof(string).GetMethod( "Contains" , new[] { 
typeof(string) })!;
    // Create a parameter for the expression tree:
    // the 'x' in 'x => x.PropertyName.Contains("term")'
    // The type of this parameter is the query's element type
    ParameterExpression prm = Parameter(elementType);
    // Map each property to an expression tree node
    IEnumerable<Expression> expressions = stringProperties
        .Select(prp =>
            // For each property, we have to construct an expression tree  
node like x.PropertyName.Contains("term")
            Call(                  // .Contains(...) 
                Property(          // .PropertyName
                    prm,           // x 
                    prp
                ),
                containsMethod,
                Constant(term)     // "term" 
            )
        );
    // Combine all the resultant expression nodes using ||
    Expression body = expressions
        .Aggregate(
            (prev, current) => Or(prev, current)
        );
    // Wrap the expression body in a compile-time-typed lambda expression
    Expression<Func<T, bool>> lambda = Lambda<Func<T, bool>>(body, prm);
    // Because the lambda is compile-time-typed (albeit with a generic  
parameter), we can use it with the Where method
    return source.Where(lambda);
}
var qry = TextFilter(
        new List<Person>().AsQueryable(), 
        "abcd"
    )
    .Where(x => x.DateOfBirth < new DateTime( 2001, 1, 1));
var qry1 = TextFilter(If you have an IQueryable  instead of an IQueryable<T> , you can't directly call the
generic LINQ methods. One alternative is to build the inner expression tree as above,
and use reflection to invoke the appropriate LINQ method while passing in the
expression tree.
You could also duplicate the LINQ method's functionality, by wrapping the entire tree in
a MethodCallExpression  that represents a call to the LINQ method:
C#
In this case, you don't have a compile-time T generic placeholder, so you'll use the
Lambda  overload that doesn't require compile-time type information, and which
produces a LambdaExpression  instead of an Expression<TDelegate> .        new List<Car>().AsQueryable(), 
        "abcd"
    )
    .Where(x => x.Year == 2010);
Add method call nodes to the IQueryable's
expression tree
IQueryable TextFilter_Untyped (IQueryable source, string term)
{
    if (string.IsNullOrEmpty(term)) { return source; }
    Type elementType = source.ElementType;
    // The logic for building the ParameterExpression and the  
LambdaExpression's body is the same as in the previous example,
    // but has been refactored into the constructBody function.
    (Expression? body, ParameterExpression? prm) =  
constructBody(elementType, term);
    if (body is null) {return source;}
    Expression filteredTree = Call(
        typeof(Queryable),
        "Where",
        new[] { elementType},
        source.Expression,
        Lambda(body, prm!)
    );
    return source.Provider.CreateQuery(filteredTree);
}Constructing expression trees using factory methods is relatively complex; it is easier to
compose strings. The Dynamic LINQ library  exposes a set of extension methods on
IQueryable  corresponding to the standard LINQ methods at Queryable , and which
accept strings in a special syntax  instead of expression trees. The library generates the
appropriate expression tree from the string, and can return the resultant translated
IQueryable .
For instance, the previous example could be rewritten as follows:
C#
Execute expression trees
Dynamically specify predicate filters at run timeThe Dynamic LINQ library
// using System.Linq.Dynamic.Core
IQueryable TextFilter_Strings (IQueryable source, string term) {
    if (string.IsNullOrEmpty(term)) { return source; }
    var elementType = source.ElementType;
    // Get all the string property names on this specific type.
    var stringProperties = 
        elementType.GetProperties()
            .Where(x => x.PropertyType == typeof(string))
            .ToArray();
    if (!stringProperties.Any()) { return source; }
    // Build the string expression
    string filterExpr = string.Join(
        " || ",
        stringProperties.Select(prp => $"{prp.Name} .Contains(@0)" )
    );
    return source.Where(filterExpr, term);
}
See alsoHow to query an ArrayList with LINQ
(C#)
Article •07/18/2023
When using LINQ to query non-generic IEnumerable  collections such as ArrayList , you
must explicitly declare the type of the range variable to reflect the specific type of the
objects in the collection. For example, if you have an ArrayList  of Student objects, your
from clause  should look like this:
C#
By specifying the type of the range variable, you are casting each item in the ArrayList  to
a Student.
The use of an explicitly typed range variable in a query expression is equivalent to
calling the Cast method. Cast throws an exception if the specified cast cannot be
performed. Cast and OfType are the two S tandard Query Operator methods that operate
on non-generic IEnumerable  types. For more information, see Type R elationships in
LINQ Query Operations .
The following example shows a simple query over an ArrayList . Note that this example
uses object initializers when the code calls the Add method, but this is not a
requirement.
C#var query = from Student s in arrList  
//...
Example
using System;  
using System.Collections;  
using System.Linq;  
  
namespace  NonGenericLINQ   
{  
    public class Student  
    {  
        public string FirstName { get; set; }  
        public string LastName { get; set; }  
        public int[] Scores { get; set; }  
    }    
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ArrayList arrList = new ArrayList();  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Svetlana" , LastName = "Omelchenko" , 
Scores = new int[] { 98, 92, 81, 60 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Claire" , LastName = "O’Donnell" , Scores  
= new int[] { 75, 84, 91, 39 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Sven", LastName = "Mortensen" , Scores =  
new int[] { 88, 94, 65, 91 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Cesar", LastName = "Garcia" , Scores = 
new int[] { 97, 89, 85, 82 }  
                    });  
  
            var query = from Student student in arrList  
                        where student.Scores[ 0] > 95  
                        select student;  
  
            foreach (Student s in query)  
                Console.WriteLine(s.LastName + ": " + s.Scores[ 0]);  
        }  
    }  
}  
/* Output:
    Omelchenko: 98  
    Garcia: 97  
*/  
６ Collaborat e with us on
GitHub
The source for this content can
be found on GitHub, where you
can also create and review.NET feedb ack
The .NET documentation is open
source. Provide feedback here.issues and pull requests. For
more information, see our
contributor guide . Open a documentation issue
 Provide product feedbackHow to add custom methods for LINQ
queries (C#)
Article •09/15/2021
You extend the set of methods that you use for LINQ queries by adding extension
methods to the IEnumerable<T>  interface. For example, in addition to the standard
average or maximum operations, you create a custom aggregate method to compute a
single value from a sequence of values. Y ou also create a method that works as a
custom filter or a specific data transform for a sequence of values and returns a new
sequence. Examples of such methods are Distinct , Skip, and Reverse .
When you extend the IEnumerable<T>  interface, you can apply your custom methods to
any enumerable collection. For more information, see Extension Methods .
An aggregate method computes a single value from a set of values. LINQ provides
several aggregate methods, including Average , Min, and Max. You can create your own
aggregate method by adding an extension method to the IEnumerable<T>  interface.
The following code example shows how to create an extension method called Median to
compute a median for a sequence of numbers of type double.
C#Add an aggregate method
public static class EnumerableExtension  
{ 
    public static double Median(this IEnumerable< double>? source ) 
    { 
        if (source is null || !source.Any())  
        {  
            throw new InvalidOperationException( "Cannot compute median for a  
null or empty set." ); 
        }  
        var sortedList =  
            source.OrderBy(number => number).ToList();  
        int itemIndex = sortedList.Count / 2; 
        if (sortedList.Count % 2 == 0) 
        {  
            // Even number of items.  
            return (sortedList[itemIndex] + sortedList[itemIndex - 1]) / 2; 
        }  You call this extension method for any enumerable collection in the same way you call
other aggregate methods from the IEnumerable<T>  interface.
The following code example shows how to use the Median method for an array of type
double.
C#
You can overload your aggregate method so that it accepts sequences of various types.
The standard approach is to create an overload for each type. Another approach is to
create an overload that will take a generic type and convert it to a specific type by using
a delegate. Y ou can also combine both approaches.
You can create a specific overload for each type that you want to support. The following
code example shows an overload of the Median method for the int type.
C#
You can now call the Median overloads for both integer and double types, as shown in
the following code:        else 
        {  
            // Odd number of items.  
            return sortedList[itemIndex];  
        }  
    } 
} 
double[] numbers = { 1.9, 2, 8, 4, 5.7, 6, 7.2, 0 }; 
var query = numbers.Median();  
Console.WriteLine( $"double: Median = {query}"); 
// This code produces the following output:  
//     double: Median = 4.85  
Overload an aggregate method to accept various types
Create an overload for each type
// int overload  
public static double Median(this IEnumerable< int> source ) => 
    (from number in source select (double)number). Median(); C#
You can also create an overload that accepts a sequence of generic objects. This
overload takes a delegate as a parameter and uses it to convert a sequence of objects of
a generic type to a specific type.
The following code shows an overload of the Median method that takes the
Func<T,TR esult>  delegate as a parameter. This delegate takes an object of generic type
T and returns an object of type double.
C#
You can now call the Median method for a sequence of objects of any type. If the type
doesn't have its own method overload, you have to pass a delegate parameter. In C#,
you can use a lambda expression for this purpose. Also, in Visual Basic only, if you use
the Aggregate or Group By clause instead of the method call, you can pass any value or
expression that is in the scope this clause.
The following example code shows how to call the Median method for an array of
integers and an array of strings. For strings, the median for the lengths of strings in the
array is calculated. The example shows how to pass the Func<T,TR esult>  delegate
parameter to the Median method for each case.
C#double[] numbers1 = { 1.9, 2, 8, 4, 5.7, 6, 7.2, 0 }; 
var query1 = numbers1.Median();  
Console.WriteLine( $"double: Median = {query1} "); 
int[] numbers2 = { 1, 2, 3, 4, 5 }; 
var query2 = numbers2.Median();  
Console.WriteLine( $"int: Median = {query2} "); 
// This code produces the following output:  
//     double: Median = 4.85  
//     int: Median = 3  
Create a generic overload
// generic overload  
public static double Median<T>(  
    this IEnumerable<T> numbers, Func<T, double> selector) =>  
    (from num in numbers select selector (num)).Median(); You can extend the IEnumerable<T>  interface with a custom query method that returns
a sequence of values. In this case, the method must return a collection of type
IEnumerable<T> . Such methods can be used to apply filters or data transforms to a
sequence of values.
The following example shows how to create an extension method named
AlternateElements that returns every other element in a collection, starting from the
first element.
C#int[] numbers3 = { 1, 2, 3, 4, 5 }; 
/* 
    You can use the num => num lambda expression as a parameter for the  
Median method  
    so that the compiler will implicitly convert its value to double.  
    If there is no implicit conversion, the compiler will display an error  
message.  
*/ 
var query3 = numbers3.Median(num => num);  
Console.WriteLine( $"int: Median = {query3} "); 
string[] numbers4 = { "one", "two", "three", "four", "five" }; 
// With the generic overload, you can also use numeric properties of  
objects.  
var query4 = numbers4.Median(str => str.Length);  
Console.WriteLine( $"string: Median = {query4} "); 
// This code produces the following output:  
//     int: Median = 3  
//     string: Median = 4  
Add a method that returns a sequence
// Extension method for the IEnumerable<T> interface.  
// The method returns every other element of a sequence.  
public static IEnumerable<T> AlternateElements<T>( this IEnumerable<T>  
source) 
{ 
    int index = 0; 
    foreach (T element in source)  
    { 
        if (index % 2 == 0) 
        {  
            yield return element;  
        }  You can call this extension method for any enumerable collection just as you would call
other methods from the IEnumerable<T>  interface, as shown in the following code:
C#
IEnumerable<T>
Extension Methods        index++;  
    } 
} 
string[] strings = { "a", "b", "c", "d", "e" }; 
var query5 = strings.AlternateElements();  
foreach (var element in query5)  
{ 
    Console.WriteLine(element);  
} 
// This code produces the following output:  
//     a  
//     c  
//     e  
See alsoAsynchronous programming with async
and await
Article •09/28/2023
The Task asynchronous programming model (T AP) provides an abstraction over
asynchronous code. Y ou write code as a sequence of statements, just like always. Y ou
can read that code as though each statement completes before the next begins. The
compiler performs many transformations because some of those statements may start
work and return a Task that represents the ongoing work.
That's the goal of this syntax: enable code that reads like a sequence of statements, but
executes in a much more complicated order based on external resource allocation and
when tasks are complete. It's analogous to how people give instructions for processes
that include asynchronous tasks. Throughout this article, you'll use an example of
instructions for making breakfast to see how the async and await keywords make it
easier to reason about code that includes a series of asynchronous instructions. Y ou'd
write the instructions something like the following list to explain how to make a
breakfast:
1. Pour a cup of coffee.
2. Heat a pan, then fry two eggs.
3. Fry three slices of bacon.
4. Toast two pieces of bread.
5. Add butter and jam to the toast.
6. Pour a glass of orange juice.
If you have experience with cooking, you'd execute those instructions asynchr onously .
You'd start warming the pan for eggs, then start the bacon. Y ou'd put the bread in the
toaster, then start the eggs. At each step of the process, you'd start a task, then turn
your attention to tasks that are ready for your attention.
Cooking breakfast is a good example of asynchronous work that isn't parallel. One
person (or thread) can handle all these tasks. Continuing the breakfast analogy, one
person can make breakfast asynchronously by starting the next task before the first task
completes. The cooking progresses whether or not someone is watching it. As soon as
you start warming the pan for the eggs, you can begin frying the bacon. Once the bacon
starts, you can put the bread into the toaster.
For a parallel algorithm, you'd need multiple cooks (or threads). One would make the
eggs, one the bacon, and so on. Each one would be focused on just that one task. Eachcook (or thread) would be blocked synchronously waiting for the bacon to be ready to
flip, or the toast to pop.
Now, consider those same instructions written as C# statements:
C#
using System;
using System.Threading.Tasks;
namespace  AsyncBreakfast
{
    // These classes are intentionally empty for the purpose of this  
example. They are simply marker classes for the purpose of demonstration,  
contain no properties, and serve no other purpose.
    internal  class Bacon { }
    internal  class Coffee { }
    internal  class Egg { }
    internal  class Juice { }
    internal  class Toast { }
    class Program
    {
        static void Main(string[] args)
        {
            Coffee cup = PourCoffee();
            Console.WriteLine( "coffee is ready" );
            Egg eggs = FryEggs( 2);
            Console.WriteLine( "eggs are ready" );
            Bacon bacon = FryBacon( 3);
            Console.WriteLine( "bacon is ready" );
            Toast toast = ToastBread( 2);
            ApplyButter(toast);
            ApplyJam(toast);
            Console.WriteLine( "toast is ready" );
            Juice oj = PourOJ();
            Console.WriteLine( "oj is ready" );
            Console.WriteLine( "Breakfast is ready!" );
        }
        private static Juice PourOJ()
        {
            Console.WriteLine( "Pouring orange juice" );
            return new Juice();
        }
        private static void ApplyJam (Toast toast ) =>
            Console.WriteLine( "Putting jam on the toast" );        private static void ApplyButter (Toast toast ) =>
            Console.WriteLine( "Putting butter on the toast" );
        private static Toast ToastBread (int slices)
        {
            for (int slice = 0; slice < slices; slice++)
            {
                Console.WriteLine( "Putting a slice of bread in the  
toaster" );
            }
            Console.WriteLine( "Start toasting..." );
            Task.Delay( 3000).Wait();
            Console.WriteLine( "Remove toast from toaster" );
            return new Toast();
        }
        private static Bacon FryBacon (int slices)
        {
            Console.WriteLine( $"putting {slices}  slices of bacon in the  
pan");
            Console.WriteLine( "cooking first side of bacon..." );
            Task.Delay( 3000).Wait();
            for (int slice = 0; slice < slices; slice++)
            {
                Console.WriteLine( "flipping a slice of bacon" );
            }
            Console.WriteLine( "cooking the second side of bacon..." );
            Task.Delay( 3000).Wait();
            Console.WriteLine( "Put bacon on plate" );
            return new Bacon();
        }
        private static Egg FryEggs(int howMany )
        {
            Console.WriteLine( "Warming the egg pan..." );
            Task.Delay( 3000).Wait();
            Console.WriteLine( $"cracking {howMany}  eggs");
            Console.WriteLine( "cooking the eggs ..." );
            Task.Delay( 3000).Wait();
            Console.WriteLine( "Put eggs on plate" );
            return new Egg();
        }
        private static Coffee PourCoffee ()
        {
            Console.WriteLine( "Pouring coffee" );
            return new Coffee();
        }
    }
}The synchronously prepared breakfast took roughly 30 minutes because the total is the
sum of each task.
Computers don't interpret those instructions the same way people do. The computer
will block on each statement until the work is complete before moving on to the next
statement. That creates an unsatisfying breakfast. The later tasks wouldn't be started
until the earlier tasks had been completed. It would take much longer to create the
breakfast, and some items would have gotten cold before being served.
If you want the computer to execute the above instructions asynchronously, you must
write asynchronous code.
These concerns are important for the programs you write today. When you write client
programs, you want the UI to be responsive to user input. Y our application shouldn't
make a phone appear frozen while it's downloading data from the web. When you write
server programs, you don't want threads blocked. Those threads could be serving other
requests. Using synchronous code when asynchronous alternatives exist hurts your
ability to scale out less expensively. Y ou pay for those blocked threads.
Successful modern applications require asynchronous code. Without language support,
writing asynchronous code required callbacks, completion events, or other means that
obscured the original intent of the code. The advantage of the synchronous code is thatits step-by-step actions make it easy to scan and understand. T raditional asynchronous
models forced you to focus on the asynchronous nature of the code, not on the
fundamental actions of the code.
The preceding code demonstrates a bad practice: constructing synchronous code to
perform asynchronous operations. As written, this code blocks the thread executing it
from doing any other work. It won't be interrupted while any of the tasks are in
progress. It would be as though you stared at the toaster after putting the bread in.
You'd ignore anyone talking to you until the toast popped.
Let's start by updating this code so that the thread doesn't block while tasks are
running. The await keyword provides a non-blocking way to start a task, then continue
execution when that task completes. A simple asynchronous version of the make a
breakfast code would look like the following snippet:
C#Don't block, await instead
static async Task Main(string[] args)
{
    Coffee cup = PourCoffee();
    Console.WriteLine( "coffee is ready" );
    Egg eggs = await FryEggsAsync( 2);
    Console.WriteLine( "eggs are ready" );
    Bacon bacon = await FryBaconAsync( 3);
    Console.WriteLine( "bacon is ready" );
    Toast toast = await ToastBreadAsync( 2);
    ApplyButter(toast);
    ApplyJam(toast);
    Console.WriteLine( "toast is ready" );
    Juice oj = PourOJ();
    Console.WriteLine( "oj is ready" );
    Console.WriteLine( "Breakfast is ready!" );
}
） Impor tant
The total elapsed time is roughly the same as the initial synchronous version. The
code has yet to take advantage of some of the key features of asynchronous
programming.This code doesn't block while the eggs or the bacon are cooking. This code won't start
any other tasks though. Y ou'd still put the toast in the toaster and stare at it until it pops.
But at least, you'd respond to anyone that wanted your attention. In a restaurant where
multiple orders are placed, the cook could start another breakfast while the first is
cooking.
Now, the thread working on the breakfast isn't blocked while awaiting any started task
that hasn't yet finished. For some applications, this change is all that's needed. A GUI
application still responds to the user with just this change. However, for this scenario,
you want more. Y ou don't want each of the component tasks to be executed
sequentially. It's better to start each of the component tasks before awaiting the
previous task's completion.
In many scenarios, you want to start several independent tasks immediately. Then, as
each task finishes, you can continue other work that's ready. In the breakfast analogy,
that's how you get breakfast done more quickly. Y ou also get everything done close to
the same time. Y ou'll get a hot breakfast.
The System.Threading.T asks.T ask and related types are classes you can use to reason
about tasks that are in progress. That enables you to write code that more closely
resembles the way you'd create breakfast. Y ou'd start cooking the eggs, bacon, and
toast at the same time. As each requires action, you'd turn your attention to that task,
take care of the next action, then wait for something else that requires your attention.
You start a task and hold on to the Task object that represents the work. Y ou'll await
each task before working with its result. Tip
The method bodies of the FryEggsAsync, FryBaconAsync, and ToastBreadAsync have
all been updated to return Task<Egg>, Task<Bacon>, and Task<Toast> respectively.
The methods are renamed from their original version to include the "Async" suffix.
Their implementations are shown as part of the final v ersion later in this article.
７ Note
The Main method returns Task, despite not having a return expression—this is by
design. For more information, see Evaluation o f a void-r eturning async function .
Start tasks concurrentlyLet's make these changes to the breakfast code. The first step is to store the tasks for
operations when they start, rather than awaiting them:
C#
The preceding code won't get your breakfast ready any faster. The tasks are all awaited
as soon as they are started. Next, you can move the await statements for the bacon and
eggs to the end of the method, before serving breakfast:
C#Coffee cup = PourCoffee();
Console.WriteLine( "Coffee is ready" );
Task<Egg> eggsTask = FryEggsAsync( 2);
Egg eggs = await eggsTask;
Console.WriteLine( "Eggs are ready" );
Task<Bacon> baconTask = FryBaconAsync( 3);
Bacon bacon = await baconTask;
Console.WriteLine( "Bacon is ready" );
Task<Toast> toastTask = ToastBreadAsync( 2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine( "Toast is ready" );
Juice oj = PourOJ();
Console.WriteLine( "Oj is ready" );
Console.WriteLine( "Breakfast is ready!" );
Coffee cup = PourCoffee();
Console.WriteLine( "Coffee is ready" );
Task<Egg> eggsTask = FryEggsAsync( 2);
Task<Bacon> baconTask = FryBaconAsync( 3);
Task<Toast> toastTask = ToastBreadAsync( 2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine( "Toast is ready" );
Juice oj = PourOJ();
Console.WriteLine( "Oj is ready" );
Egg eggs = await eggsTask;
Console.WriteLine( "Eggs are ready" );
Bacon bacon = await baconTask;
Console.WriteLine( "Bacon is ready" );The asynchronously prepared breakfast took roughly 20 minutes, this time savings is
because some tasks ran concurrently.
The preceding code works better. Y ou start all the asynchronous tasks at once. Y ou await
each task only when you need the results. The preceding code may be similar to code in
a web application that makes requests to different microservices, then combines the
results into a single page. Y ou'll make all the requests immediately, then await all those
tasks and compose the web page.
You have everything ready for breakfast at the same time except the toast. Making the
toast is the composition of an asynchronous operation (toasting the bread), and
synchronous operations (adding the butter and the jam). Updating this code illustrates
an important concept:Console.WriteLine( "Breakfast is ready!" );
Composition with tasks
） Impor tant
The composition of an asynchronous operation followed by synchronous work is an
asynchronous operation. S tated another way, if any portion of an operation is
asynchronous, the entire operation is asynchronous.The preceding code showed you that you can use Task or Task<TR esult>  objects to hold
running tasks. Y ou await each task before using its result. The next step is to create
methods that represent the combination of other work. Before serving breakfast, you
want to await the task that represents toasting the bread before adding butter and jam.
You can represent that work with the following code:
C#
The preceding method has the async modifier in its signature. That signals to the
compiler that this method contains an await statement; it contains asynchronous
operations. This method represents the task that toasts the bread, then adds butter and
jam. This method returns a Task<TR esult>  that represents the composition of those
three operations. The main block of code now becomes:
C#static async Task<Toast> MakeToastWithButterAndJamAsync (int number)
{
    var toast = await ToastBreadAsync(number);
    ApplyButter(toast);
    ApplyJam(toast);
    return toast;
}
static async Task Main(string[] args)
{
    Coffee cup = PourCoffee();
    Console.WriteLine( "coffee is ready" );
    var eggsTask = FryEggsAsync( 2);
    var baconTask = FryBaconAsync( 3);
    var toastTask = MakeToastWithButterAndJamAsync( 2);
    var eggs = await eggsTask;
    Console.WriteLine( "eggs are ready" );
    var bacon = await baconTask;
    Console.WriteLine( "bacon is ready" );
    var toast = await toastTask;
    Console.WriteLine( "toast is ready" );
    Juice oj = PourOJ();
    Console.WriteLine( "oj is ready" );
    Console.WriteLine( "Breakfast is ready!" );
}The previous change illustrated an important technique for working with asynchronous
code. Y ou compose tasks by separating the operations into a new method that returns a
task. Y ou can choose when to await that task. Y ou can start other tasks concurrently.
Up to this point, you've implicitly assumed that all these tasks complete successfully.
Asynchronous methods throw exceptions, just like their synchronous counterparts.
Asynchronous support for exceptions and error handling strives for the same goals as
asynchronous support in general: Y ou should write code that reads like a series of
synchronous statements. T asks throw exceptions when they can't complete successfully.
The client code can catch those exceptions when a started task is awaited. For example,
let's assume that the toaster catches fire while making the toast. Y ou can simulate that
by modifying the ToastBreadAsync method to match the following code:
C#
Run the application after making these changes, and you'll output similar to the
following text:
ConsoleAsynchronous exceptions
private static async Task<Toast> ToastBreadAsync (int slices)
{
    for (int slice = 0; slice < slices; slice++)
    {
        Console.WriteLine( "Putting a slice of bread in the toaster" );
    }
    Console.WriteLine( "Start toasting..." );
    await Task.Delay( 2000);
    Console.WriteLine( "Fire! Toast is ruined!" );
    throw new InvalidOperationException( "The toaster is on fire" );
    await Task.Delay( 1000);
    Console.WriteLine( "Remove toast from toaster" );
    return new Toast();
}
７ Note
You'll get a warning when you compile the preceding code regarding unreachable
code. That's intentional, because once the toaster catches fire, operations won't
proceed normally.You'll notice quite a few tasks are completed between when the toaster catches fire and
the exception is observed. When a task that runs asynchronously throws an exception,
that T ask is fault ed. The T ask object holds the exception thrown in the Task.Exception
property. F aulted tasks throw an exception when they're awaited.
There are two important mechanisms to understand: how an exception is stored in a
faulted task, and how an exception is unpackaged and rethrown when code awaits a
faulted task.
When code running asynchronously throws an exception, that exception is stored in the
Task. The Task.Exception  property is a System.AggregateException  because more than
one exception may be thrown during asynchronous work. Any exception thrown is
added to the AggregateException.InnerExceptions  collection. If that Exception property
is null, a new AggregateException is created and the thrown exception is the first item in
the collection.
The most common scenario for a faulted task is that the Exception property contains
exactly one exception. When code awaits a faulted task, the first exception in the
AggregateException.InnerExceptions  collection is rethrown. That's why the output fromPouring coffee
Coffee is ready
Warming the egg pan...
putting 3 slices of bacon in the pan
Cooking first side of bacon...
Putting a slice of bread in the toaster
Putting a slice of bread in the toaster
Start toasting...
Fire! Toast is ruined!
Flipping a slice of bacon
Flipping a slice of bacon
Flipping a slice of bacon
Cooking the second side of bacon...
Cracking 2 eggs
Cooking the eggs ...
Put bacon on plate
Put eggs on plate
Eggs are ready
Bacon is ready
Unhandled exception. System.InvalidOperationException: The toaster is on  
fire
   at AsyncBreakfast.Program.ToastBreadAsync(Int32 slices) in  
Program.cs:line 65
   at AsyncBreakfast.Program.MakeToastWithButterAndJamAsync(Int32 number) in  
Program.cs:line 36
   at AsyncBreakfast.Program.Main(String[] args) in Program.cs:line 24
   at AsyncBreakfast.Program.<Main>(String[] args)this example shows an InvalidOperationException instead of an AggregateException.
Extracting the first inner exception makes working with asynchronous methods as
similar as possible to working with their synchronous counterparts. Y ou can examine the
Exception property in your code when your scenario may generate multiple exceptions.
Before going on, comment out these two lines in your ToastBreadAsync method. Y ou
don't want to start another fire:
C#
The series of await statements at the end of the preceding code can be improved by
using methods of the Task class. One of those APIs is WhenAll , which returns a Task that
completes when all the tasks in its argument list have completed, as shown in the
following code:
C#
Another option is to use WhenAny , which returns a Task<Task> that completes when
any of its arguments complete. Y ou can await the returned task, knowing that it has
already finished. The following code shows how you could use WhenAny  to await the
first task to finish and then process its result. After processing the result from the
completed task, you remove that completed task from the list of tasks passed to
WhenAny. Tip
We recommend that any argument validation exceptions emerge synchr onously
from task-returning methods. For more information and an example of how to do
it, see Exceptions in task -returning methods .
Console.WriteLine( "Fire! Toast is ruined!" );
throw new InvalidOperationException( "The toaster is on fire" );
Await tasks efficiently
await Task.WhenAll(eggsTask, baconTask, toastTask);
Console.WriteLine( "Eggs are ready" );
Console.WriteLine( "Bacon is ready" );
Console.WriteLine( "Toast is ready" );
Console.WriteLine( "Breakfast is ready!" );C#
Near the end, you see the line await finishedTask;. The line await Task.WhenAny
doesn't await the finished task. It awaits the Task returned by Task.WhenAny. The result
of Task.WhenAny is the task that has completed (or faulted). Y ou should await that task
again, even though you know it's finished running. That's how you retrieve its result, or
ensure that the exception causing it to fault gets thrown.
After all those changes, the final version of the code looks like this:
C#var breakfastTasks = new List<Task> { eggsTask, baconTask, toastTask };
while (breakfastTasks.Count > 0)
{
    Task finishedTask = await Task.WhenAny(breakfastTasks);
    if (finishedTask == eggsTask)
    {
        Console.WriteLine( "Eggs are ready" );
    }
    else if (finishedTask == baconTask)
    {
        Console.WriteLine( "Bacon is ready" );
    }
    else if (finishedTask == toastTask)
    {
        Console.WriteLine( "Toast is ready" );
    }
    await finishedTask;
    breakfastTasks.Remove(finishedTask);
}
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
namespace  AsyncBreakfast
{
    // These classes are intentionally empty for the purpose of this  
example. They are simply marker classes for the purpose of demonstration,  
contain no properties, and serve no other purpose.
    internal  class Bacon { }
    internal  class Coffee { }
    internal  class Egg { }
    internal  class Juice { }
    internal  class Toast { }
    class Program
    {        static async Task Main(string[] args)
        {
            Coffee cup = PourCoffee();
            Console.WriteLine( "coffee is ready" );
            var eggsTask = FryEggsAsync( 2);
            var baconTask = FryBaconAsync( 3);
            var toastTask = MakeToastWithButterAndJamAsync( 2);
            var breakfastTasks = new List<Task> { eggsTask, baconTask,  
toastTask };
            while (breakfastTasks.Count > 0)
            {
                Task finishedTask = await Task.WhenAny(breakfastTasks);
                if (finishedTask == eggsTask)
                {
                    Console.WriteLine( "eggs are ready" );
                }
                else if (finishedTask == baconTask)
                {
                    Console.WriteLine( "bacon is ready" );
                }
                else if (finishedTask == toastTask)
                {
                    Console.WriteLine( "toast is ready" );
                }
                await finishedTask;
                breakfastTasks.Remove(finishedTask);
            }
            Juice oj = PourOJ();
            Console.WriteLine( "oj is ready" );
            Console.WriteLine( "Breakfast is ready!" );
        }
        static async Task<Toast> MakeToastWithButterAndJamAsync (int number)
        {
            var toast = await ToastBreadAsync(number);
            ApplyButter(toast);
            ApplyJam(toast);
            return toast;
        }
        private static Juice PourOJ()
        {
            Console.WriteLine( "Pouring orange juice" );
            return new Juice();
        }
        private static void ApplyJam (Toast toast ) =>
            Console.WriteLine( "Putting jam on the toast" );
        private static void ApplyButter (Toast toast ) =>
            Console.WriteLine( "Putting butter on the toast" );        private static async Task<Toast> ToastBreadAsync (int slices)
        {
            for (int slice = 0; slice < slices; slice++)
            {
                Console.WriteLine( "Putting a slice of bread in the  
toaster" );
            }
            Console.WriteLine( "Start toasting..." );
            await Task.Delay( 3000);
            Console.WriteLine( "Remove toast from toaster" );
            return new Toast();
        }
        private static async Task<Bacon> FryBaconAsync (int slices)
        {
            Console.WriteLine( $"putting {slices}  slices of bacon in the  
pan");
            Console.WriteLine( "cooking first side of bacon..." );
            await Task.Delay( 3000);
            for (int slice = 0; slice < slices; slice++)
            {
                Console.WriteLine( "flipping a slice of bacon" );
            }
            Console.WriteLine( "cooking the second side of bacon..." );
            await Task.Delay( 3000);
            Console.WriteLine( "Put bacon on plate" );
            return new Bacon();
        }
        private static async Task<Egg> FryEggsAsync (int howMany )
        {
            Console.WriteLine( "Warming the egg pan..." );
            await Task.Delay( 3000);
            Console.WriteLine( $"cracking {howMany}  eggs");
            Console.WriteLine( "cooking the eggs ..." );
            await Task.Delay( 3000);
            Console.WriteLine( "Put eggs on plate" );
            return new Egg();
        }
        private static Coffee PourCoffee ()
        {
            Console.WriteLine( "Pouring coffee" );
            return new Coffee();
        }
    }
}The final version of the asynchronously prepared breakfast took roughly 6 minutes
because some tasks ran concurrently, and the code monitored multiple tasks at once
and only took action when it was needed.
This final code is asynchronous. It more accurately reflects how a person would cook a
breakfast. Compare the preceding code with the first code sample in this article. The
core actions are still clear from reading the code. Y ou can read this code the same way
you'd read those instructions for making a breakfast at the beginning of this article. The
language features for async and await provide the translation every person makes to
follow those written instructions: start tasks as you can and don't block waiting for tasks
to complete.
Next steps
Explor e real w orld scenarios for asynchr onous pr ograms
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
 Provide product feedbackAsynchronous programming scenarios
Article •10/12/2023
If you have any I/O-bound needs (such as requesting data from a network, accessing a
database, or reading and writing to a file system), you'll want to utilize asynchronous
programming. Y ou could also have CPU-bound code, such as performing an expensive
calculation, which is also a good scenario for writing async code.
C# has a language-level asynchronous programming model, which allows for easily
writing asynchronous code without having to juggle callbacks or conform to a library
that supports asynchrony. It follows what is known as the Task-based Asynchronous
Pattern (T AP).
The core of async programming is the Task and Task<T> objects, which model
asynchronous operations. They are supported by the async and await keywords. The
model is fairly simple in most cases:
For I/O-bound code, you await an operation that returns a Task or Task<T> inside
of an async method.
For CPU-bound code, you await an operation that is started on a background
thread with the Task.Run  method.
The await keyword is where the magic happens. It yields control to the caller of the
method that performed await, and it ultimately allows a UI to be responsive or a service
to be elastic. While there are ways  to approach async code other than async and await,
this article focuses on the language-level constructs.Overview of the asynchronous model
７ Note
In some of following examples System.Net.Http.HttpClient  class is used to
download some data from a web service. The s_httpClient object used in these
examples is a static field of Program class (please check the complete example):
private static readonly HttpClient s_httpClient = new();
I/O-bound example: Download data from a web serviceYou may need to download some data from a web service when a button is pressed but
don't want to block the UI thread. It can be accomplished like this:
C#
The code expresses the intent (downloading data asynchronously) without getting
bogged down in interacting with Task objects.
Say you're writing a mobile game where pressing a button can inflict damage on many
enemies on the screen. P erforming the damage calculation can be expensive, and doing
it on the UI thread would make the game appear to pause as the calculation is
performed!
The best way to handle this is to start a background thread, which does the work using
Task.Run, and await its result using await. This allows the UI to feel smooth as the work
is being done.
C#s_downloadButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI as the request
    // from the web service is happening.
    //
    // The UI thread is now free to perform other work.
    var stringData = await s_httpClient.GetStringAsync(URL);
    DoSomethingWithData(stringData);
};
CPU-bound example: Perform a calculation for a game
static DamageResult CalculateDamageDone ()
{
    return new DamageResult()
    {
        // Code omitted:
        //
        // Does an expensive calculation and returns
        // the result of that calculation.
    };
}
s_calculateButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI while CalculateDamageDone()
    // performs its work. The UI thread is free to perform other work.
    var damageResult = await Task.Run(() => CalculateDamageDone());This code clearly expresses the intent of the button's click event, it doesn't require
managing a background thread manually, and it does so in a non-blocking way.
On the C# side of things, the compiler transforms your code into a state machine that
keeps track of things like yielding execution when an await is reached and resuming
execution when a background job has finished.
For the theoretically inclined, this is an implementation of the Promise Model of
asynchrony .
Async code can be used for both I/O-bound and CPU-bound code, but differently
for each scenario.
Async code uses Task<T> and Task, which are constructs used to model work
being done in the background.
The async keyword turns a method into an async method, which allows you to use
the await keyword in its body.
When the await keyword is applied, it suspends the calling method and yields
control back to its caller until the awaited task is complete.
await can only be used inside an async method.
The first two examples of this guide showed how you could use async and await for
I/O-bound and CPU-bound work. It's key that you can identify when a job you need to
do is I/O-bound or CPU-bound because it can greatly affect the performance of your
code and could potentially lead to misusing certain constructs.
Here are two questions you should ask before you write any code:
1. Will your code be "waiting" for something, such as data from a database?
If your answer is "yes", then your work is I/O-bound .
2. Will your code be performing an expensive computation?    DisplayDamage(damageResult);
};
What happens under the covers
Key pieces to understand
Recognize CPU-bound and I/O-bound workIf you answered "yes", then your work is CPU-bound .
If the work you have is I/O-bound , use async and await without  Task.Run. You should
not use the T ask P arallel Library.
If the work you have is CPU-bound  and you care about responsiveness, use async and
await, but spawn off the work on another thread with Task.Run. If the work is
appropriate for concurrency and parallelism, also consider using the Task P arallel Library .
Additionally, you should always measure the execution of your code. For example, you
may find yourself in a situation where your CPU-bound work is not costly enough
compared with the overhead of context switches when multithreading. Every choice has
its tradeoff, and you should pick the correct tradeoff for your situation.
The following examples demonstrate various ways you can write async code in C#. They
cover a few different scenarios you may come across.
This snippet downloads the HTML from the given URL and counts the number of times
the string ".NET" occurs in the HTML. It uses ASP.NET to define a W eb API controller
method, which performs this task and returns the number.
C#
Here's the same scenario written for a Universal Windows App, which performs the same
task when a Button is pressed:More examples
Extract data from a network
７ Note
If you plan on doing HTML parsing in production code, don't use regular
expressions. Use a parsing library instead.
[HttpGet, Route( "DotNetCount" )]
static public async Task<int> GetDotNetCount (string URL)
{
    // Suspends GetDotNetCount() to allow the caller (the web server)
    // to accept another request, rather than blocking on this one.
    var html = await s_httpClient.GetStringAsync(URL);
    return Regex.Matches(html, @"\.NET" ).Count;
}C#
You may find yourself in a situation where you need to retrieve multiple pieces of data
concurrently. The Task API contains two methods, Task.WhenAll  and Task.WhenAny , that
allow you to write asynchronous code that performs a non-blocking wait on multiple
background jobs.
This example shows how you might grab User data for a set of userIds.
C#private readonly  HttpClient _httpClient = new HttpClient();
private async void OnSeeTheDotNetsButtonClick (object sender, RoutedEventArgs  
e)
{
    // Capture the task handle here so we can await the background task  
later.
    var getDotNetFoundationHtmlTask =  
_httpClient.GetStringAsync( "https://dotnetfoundation.org" );
    // Any other work on the UI thread can be done here, such as enabling a  
Progress Bar.
    // This is important to do here, before the "await" call, so that the  
user
    // sees the progress bar before execution of this method is yielded.
    NetworkProgressBar.IsEnabled = true;
    NetworkProgressBar.Visibility = Visibility.Visible;
    // The await operator suspends OnSeeTheDotNetsButtonClick(), returning  
control to its caller.
    // This is what allows the app to be responsive and not block the UI  
thread.
    var html = await getDotNetFoundationHtmlTask;
    int count = Regex.Matches(html, @"\.NET" ).Count;
    DotNetCountLabel.Text = $"Number of .NETs on dotnetfoundation.org: 
{count}";
    NetworkProgressBar.IsEnabled = false;
    NetworkProgressBar.Visibility = Visibility.Collapsed;
}
Wait for multiple tasks to complete
private static async Task<User> GetUserAsync (int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object correspondingHere's another way to write this more succinctly, using LINQ:
C#
Although it's less code, use caution when mixing LINQ with asynchronous code. Because
LINQ uses deferred (lazy) execution, async calls won't happen immediately as they do in
a foreach loop unless you force the generated sequence to iterate with a call to
.ToList() or .ToArray(). The above example uses Enumerable.T oArray  to perform the
query eagerly and store the results in an array. That forces the code id =>
GetUserAsync(id) to run and start the task.
With async programming, there are some details to keep in mind that can prevent
unexpected behavior.
async methods need t o hav e an await keyword in their body or they will nev er
yield!
This is important to keep in mind. If await is not used in the body of an async
method, the C# compiler generates a warning, but the code compiles and runs as    // to the entry in the database with {userId} as its Id.
    return await Task.FromResult( new User() { id = userId });
}
private static async Task<IEnumerable<User>> GetUsersAsync(IEnumerable< int> 
userIds)
{
    var getUserTasks = new List<Task<User>>();
    foreach (int userId in userIds)
    {
        getUserTasks.Add(GetUserAsync(userId));
    }
    return await Task.WhenAll(getUserTasks);
}
private static async Task<User[]> GetUsersAsyncByLINQ(IEnumerable< int> 
userIds)
{
    var getUserTasks = userIds.Select(id => GetUserAsync(id)).ToArray();
    return await Task.WhenAll(getUserTasks);
}
Important info and adviceif it were a normal method. This is incredibly inefficient, as the state machine
generated by the C# compiler for the async method is not accomplishing anything.
Add "Async" as the suffix o f every async method name y ou writ e.
This is the convention used in .NET to more easily differentiate synchronous and
asynchronous methods. Certain methods that aren't explicitly called by your code
(such as event handlers or web controller methods) don't necessarily apply.
Because they are not explicitly called by your code, being explicit about their
naming isn't as important.
async void should only be used for ev ent handler s.
async void is the only way to allow asynchronous event handlers to work because
events do not have return types (thus cannot make use of Task and Task<T>). Any
other use of async void does not follow the T AP model and can be challenging to
use, such as:
Exceptions thrown in an async void method can't be caught outside of that
method.
async void methods are difficult to test.
async void methods can cause bad side effects if the caller isn't expecting them
to be async.
Tread car efully when using async lambdas in LINQ expr essions
Lambda expressions in LINQ use deferred execution, meaning code could end up
executing at a time when you're not expecting it to. The introduction of blocking
tasks into this can easily result in a deadlock if not written correctly. Additionally,
the nesting of asynchronous code like this can also make it more difficult to reason
about the execution of the code. Async and LINQ are powerful but should be used
together as carefully and clearly as possible.
Write code that awaits T asks in a non-blocking manner
Blocking the current thread as a means to wait for a Task to complete can result in
deadlocks and blocked context threads and can require more complex error-
handling. The following table provides guidance on how to deal with waiting for
tasks in a non-blocking way:
Use this... Instead o f this... When wishing t o do this...
await Task.Wait or
Task.ResultRetrieving the result of a background
taskUse this... Instead o f this... When wishing t o do this...
await
Task.WhenAnyTask.WaitAny Waiting for any task to complete
await
Task.WhenAllTask.WaitAll Waiting for all tasks to complete
await Task.DelayThread.Sleep Waiting for a period of time
Consider using  ValueTask wher e possible
Returning a Task object from async methods can introduce performance
bottlenecks in certain paths. Task is a reference type, so using it means allocating
an object. In cases where a method declared with the async modifier returns a
cached result or completes synchronously, the extra allocations can become a
significant time cost in performance critical sections of code. It can become costly
if those allocations occur in tight loops. For more information, see generalized
async return types .
Consider using  ConfigureAwait(false)
A common question is, "when should I use the Task.ConfigureA wait(Boolean)
method?". The method allows for a Task instance to configure its awaiter. This is
an important consideration and setting it incorrectly could potentially have
performance implications and even deadlocks. For more information on
ConfigureAwait, see the ConfigureA wait F AQ .
Write less stat eful code
Don't depend on the state of global objects or the execution of certain methods.
Instead, depend only on the return values of methods. Why?
Code will be easier to reason about.
Code will be easier to test.
Mixing async and synchronous code is far simpler.
Race conditions can typically be avoided altogether.
Depending on return values makes coordinating async code simple.
(Bonus) it works really well with dependency injection.
A recommended goal is to achieve complete or near-complete Referential
Transparency  in your code. Doing so will result in a predictable, testable, and
maintainable codebase.
The following code is the complete text of the Program.cs  file for the example.
C#Complete example
using System.Text.RegularExpressions;
using System.Windows;
using Microsoft.AspNetCore.Mvc;
class Button
{
    public Func<object, object, Task>? Clicked
    {
        get;
        internal  set;
    }
}
class DamageResult
{
    public int Damage
    {
        get { return 0; }
    }
}
class User
{
    public bool isEnabled
    {
        get;
        set;
    }
    public int id
    {
        get;
        set;
    }
}
public class Program
{
    private static readonly  Button s_downloadButton = new();
    private static readonly  Button s_calculateButton = new();
    private static readonly  HttpClient s_httpClient = new();
    private static readonly  IEnumerable< string> s_urlList = new string[]
    {
            "https://learn.microsoft.com" ,
            "https://learn.microsoft.com/aspnet/core" ,            "https://learn.microsoft.com/azure" ,
            "https://learn.microsoft.com/azure/devops" ,
            "https://learn.microsoft.com/dotnet" ,
            "https://learn.microsoft.com/dotnet/desktop/wpf/get-
started/create-app-visual-studio" ,
            "https://learn.microsoft.com/education" ,
            "https://learn.microsoft.com/shows/net-core-101/what-is-net" ,
            "https://learn.microsoft.com/enterprise-mobility-security" ,
            "https://learn.microsoft.com/gaming" ,
            "https://learn.microsoft.com/graph" ,
            "https://learn.microsoft.com/microsoft-365" ,
            "https://learn.microsoft.com/office" ,
            "https://learn.microsoft.com/powershell" ,
            "https://learn.microsoft.com/sql" ,
            "https://learn.microsoft.com/surface" ,
            "https://dotnetfoundation.org" ,
            "https://learn.microsoft.com/visualstudio" ,
            "https://learn.microsoft.com/windows" ,
            "https://learn.microsoft.com/xamarin"
    };
    private static void Calculate ()
    {
        // <PerformGameCalculation>
        static DamageResult CalculateDamageDone ()
        {
            return new DamageResult()
            {
                // Code omitted:
                //
                // Does an expensive calculation and returns
                // the result of that calculation.
            };
        }
        s_calculateButton.Clicked += async (o, e) =>
        {
            // This line will yield control to the UI while  
CalculateDamageDone()
            // performs its work. The UI thread is free to perform other  
work.
            var damageResult = await Task.Run(() => CalculateDamageDone());
            DisplayDamage(damageResult);
        };
        // </PerformGameCalculation>
    }
    private static void DisplayDamage (DamageResult damage )
    {
        Console.WriteLine(damage.Damage);
    }
    private static void Download (string URL)
    {
        // <UnblockingDownload>        s_downloadButton.Clicked += async (o, e) =>
        {
            // This line will yield control to the UI as the request
            // from the web service is happening.
            //
            // The UI thread is now free to perform other work.
            var stringData = await s_httpClient.GetStringAsync(URL);
            DoSomethingWithData(stringData);
        };
        // </UnblockingDownload>
    }
    private static void DoSomethingWithData (object stringData )
    {
        Console.WriteLine( "Displaying data: " , stringData);
    }
    // <GetUsersForDataset>
    private static async Task<User> GetUserAsync (int userId)
    {
        // Code omitted:
        //
        // Given a user Id {userId}, retrieves a User object corresponding
        // to the entry in the database with {userId} as its Id.
        return await Task.FromResult( new User() { id = userId });
    }
    private static async Task<IEnumerable<User>>  
GetUsersAsync(IEnumerable< int> userIds)
    {
        var getUserTasks = new List<Task<User>>();
        foreach (int userId in userIds)
        {
            getUserTasks.Add(GetUserAsync(userId));
        }
        return await Task.WhenAll(getUserTasks);
    }
    // </GetUsersForDataset>
    // <GetUsersForDatasetByLINQ>
    private static async Task<User[]> GetUsersAsyncByLINQ(IEnumerable< int> 
userIds)
    {
        var getUserTasks = userIds.Select(id => GetUserAsync(id)).ToArray();
        return await Task.WhenAll(getUserTasks);
    }
    // </GetUsersForDatasetByLINQ>
    // <ExtractDataFromNetwork>
    [HttpGet, Route( "DotNetCount" )]
    static public async Task<int> GetDotNetCount (string URL)
    {
        // Suspends GetDotNetCount() to allow the caller (the web server)        // to accept another request, rather than blocking on this one.
        var html = await s_httpClient.GetStringAsync(URL);
        return Regex.Matches(html, @"\.NET" ).Count;
    }
    // </ExtractDataFromNetwork>
    static async Task Main()
    {
        Console.WriteLine( "Application started." );
        Console.WriteLine( "Counting '.NET' phrase in websites..." );
        int total = 0;
        foreach (string url in s_urlList)
        {
            var result = await GetDotNetCount(url);
            Console.WriteLine( $"{url}: {result} ");
            total += result;
        }
        Console.WriteLine( "Total: "  + total);
        Console.WriteLine( "Retrieving User objects with list of IDs..." );
        IEnumerable< int> ids = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 0 };
        var users = await GetUsersAsync(ids);
        foreach (User? user in users)
        {
            Console.WriteLine( $"{user.id} : isEnabled= {user.isEnabled} ");
        }
        Console.WriteLine( "Application ending." );
    }
}
// Example output:
//
// Application started.
// Counting '.NET' phrase in websites...
// https://learn.microsoft.com: 0
// https://learn.microsoft.com/aspnet/core: 57
// https://learn.microsoft.com/azure: 1
// https://learn.microsoft.com/azure/devops: 2
// https://learn.microsoft.com/dotnet: 83
// https://learn.microsoft.com/dotnet/desktop/wpf/get-started/create-app-
visual-studio: 31
// https://learn.microsoft.com/education: 0
// https://learn.microsoft.com/shows/net-core-101/what-is-net: 42
// https://learn.microsoft.com/enterprise-mobility-security: 0
// https://learn.microsoft.com/gaming: 0
// https://learn.microsoft.com/graph: 0
// https://learn.microsoft.com/microsoft-365: 0
// https://learn.microsoft.com/office: 0
// https://learn.microsoft.com/powershell: 0
// https://learn.microsoft.com/sql: 0
// https://learn.microsoft.com/surface: 0
// https://dotnetfoundation.org: 16
// https://learn.microsoft.com/visualstudio: 0The T ask asynchronous programming model (C#) .// https://learn.microsoft.com/windows: 0
// https://learn.microsoft.com/xamarin: 6
// Total: 238
// Retrieving User objects with list of IDs...
// 1: isEnabled= False
// 2: isEnabled= False
// 3: isEnabled= False
// 4: isEnabled= False
// 5: isEnabled= False
// 6: isEnabled= False
// 7: isEnabled= False
// 8: isEnabled= False
// 9: isEnabled= False
// 0: isEnabled= False
// Application ending.
Other resources
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
 Provide product feedbackTask asynchronous programming model
Article •02/13/2023
You can avoid performance bottlenecks and enhance the overall responsiveness of your
application by using asynchronous programming. However, traditional techniques for
writing asynchronous applications can be complicated, making them difficult to write,
debug, and maintain.
C# supports simplified approach, async programming, that leverages asynchronous
support in the .NET runtime. The compiler does the difficult work that the developer
used to do, and your application retains a logical structure that resembles synchronous
code. As a result, you get all the advantages of asynchronous programming with a
fraction of the effort.
This topic provides an overview of when and how to use async programming and
includes links to support topics that contain details and examples.
Asynchrony is essential for activities that are potentially blocking, such as web access.
Access to a web resource sometimes is slow or delayed. If such an activity is blocked in a
synchronous process, the entire application must wait. In an asynchronous process, the
application can continue with other work that doesn't depend on the web resource until
the potentially blocking task finishes.
The following table shows typical areas where asynchronous programming improves
responsiveness. The listed APIs from .NET and the Windows Runtime contain methods
that support async programming.
Application ar ea .NET types with async
methodsWindows Runtime types with async
methods
Web access HttpClient Windows.W eb.Http.HttpClient
SyndicationClient
Working with files JsonSerializer
StreamR eader
StreamWriter
XmlR eader
XmlWriterStorageFile
Working with
imagesMediaCapture
BitmapEncoderAsync improves responsivenessApplication ar ea .NET types with async
methodsWindows Runtime types with async
methods
BitmapDecoder
WCF
programmingSynchronous and Asynchronous
Operations
Asynchrony proves especially valuable for applications that access the UI thread because
all UI-related activity usually shares one thread. If any process is blocked in a
synchronous application, all are blocked. Y our application stops responding, and you
might conclude that it has failed when instead it's just waiting.
When you use asynchronous methods, the application continues to respond to the UI.
You can resize or minimize a window, for example, or you can close the application if
you don't want to wait for it to finish.
The async-based approach adds the equivalent of an automatic transmission to the list
of options that you can choose from when designing asynchronous operations. That is,
you get all the benefits of traditional asynchronous programming but with much less
effort from the developer.
The async  and await  keywords in C# are the heart of async programming. By using those
two keywords, you can use resources in .NET Framework, .NET Core, or the Windows
Runtime to create an asynchronous method almost as easily as you create a
synchronous method. Asynchronous methods that you define by using the async
keyword are referred to as async methods .
The following example shows an async method. Almost everything in the code should
look familiar to you.
You can find a complete Windows Presentation Foundation (WPF) example available for
download from Asynchronous programming with async and await in C# .
C#Async methods are easy to write
public async Task<int> GetUrlContentLengthAsync ()
{
    var client = new HttpClient();
    Task<string> getStringTask =
        client.GetStringAsync( "https://learn.microsoft.com/dotnet" );
    DoIndependentWork();You can learn several practices from the preceding sample. S tart with the method
signature. It includes the async modifier. The return type is Task<int> (See "R eturn
Types" section for more options). The method name ends in Async. In the body of the
method, GetStringAsync returns a Task<string>. That means that when you await the
task you'll get a string (contents). Before awaiting the task, you can do work that
doesn't rely on the string from GetStringAsync.
Pay close attention to the await operator. It suspends GetUrlContentLengthAsync:
GetUrlContentLengthAsync can't continue until getStringTask is complete.
Meanwhile, control returns to the caller of GetUrlContentLengthAsync.
Control resumes here when getStringTask is complete.
The await operator then retrieves the string result from getStringTask.
The return statement specifies an integer result. Any methods that are awaiting
GetUrlContentLengthAsync retrieve the length value.
If GetUrlContentLengthAsync doesn't have any work that it can do between calling
GetStringAsync and awaiting its completion, you can simplify your code by calling and
awaiting in the following single statement.
C#
The following characteristics summarize what makes the previous example an async
method:
The method signature includes an async modifier.
The name of an async method, by convention, ends with an "Async" suffix.
The return type is one of the following types:    string contents = await getStringTask;
    return contents.Length;
}
void DoIndependentWork ()
{
    Console.WriteLine( "Working..." );
}
string contents = await 
client.GetStringAsync( "https://learn.microsoft.com/dotnet" );Task<TR esult>  if your method has a return statement in which the operand has
type TResult.
Task if your method has no return statement or has a return statement with no
operand.
void if you're writing an async event handler.
Any other type that has a GetAwaiter method.
For more information, see the Return types and parameters  section.
The method usually includes at least one await expression, which marks a point
where the method can't continue until the awaited asynchronous operation is
complete. In the meantime, the method is suspended, and control returns to the
method's caller. The next section of this topic illustrates what happens at the
suspension point.
In async methods, you use the provided keywords and types to indicate what you want
to do, and the compiler does the rest, including keeping track of what must happen
when control returns to an await point in a suspended method. Some routine processes,
such as loops and exception handling, can be difficult to handle in traditional
asynchronous code. In an async method, you write these elements much as you would
in a synchronous solution, and the problem is solved.
For more information about asynchrony in previous versions of .NET Framework, see TPL
and traditional .NET Framework asynchronous programming .
The most important thing to understand in asynchronous programming is how the
control flow moves from method to method. The following diagram leads you through
the process:What happens in an async methodThe numbers in the diagram correspond to the following steps, initiated when a calling
method calls the async method.
1. A calling method calls and awaits the GetUrlContentLengthAsync async method.
2. GetUrlContentLengthAsync creates an HttpClient  instance and calls the
GetStringAsync  asynchronous method to download the contents of a website as a
string.
3. Something happens in GetStringAsync that suspends its progress. P erhaps it must
wait for a website to download or some other blocking activity. T o avoid blocking
resources, GetStringAsync yields control to its caller, GetUrlContentLengthAsync.
GetStringAsync returns a Task<TR esult> , where TResult is a string, and
GetUrlContentLengthAsync assigns the task to the getStringTask variable. The task
represents the ongoing process for the call to GetStringAsync, with a commitment
to produce an actual string value when the work is complete.
4. Because getStringTask hasn't been awaited yet, GetUrlContentLengthAsync can
continue with other work that doesn't depend on the final result from
GetStringAsync. That work is represented by a call to the synchronous method
DoIndependentWork.
5. DoIndependentWork is a synchronous method that does its work and returns to its
caller.
6. GetUrlContentLengthAsync has run out of work that it can do without a result from
getStringTask. GetUrlContentLengthAsync next wants to calculate and return the
length of the downloaded string, but the method can't calculate that value until
the method has the string.
Therefore, GetUrlContentLengthAsync uses an await operator to suspend its
progress and to yield control to the method that called GetUrlContentLengthAsync.
GetUrlContentLengthAsync returns a Task<int> to the caller. The task represents a
promise to produce an integer result that's the length of the downloaded string.
Inside the calling method the processing pattern continues. The caller might do
other work that doesn't depend on the result from GetUrlContentLengthAsync
before awaiting that result, or the caller might await immediately. The calling
method is waiting for GetUrlContentLengthAsync, and GetUrlContentLengthAsync is
waiting for GetStringAsync.
7. GetStringAsync completes and produces a string result. The string result isn't
returned by the call to GetStringAsync in the way that you might expect.
(Remember that the method already returned a task in step 3.) Instead, the string
result is stored in the task that represents the completion of the method,
getStringTask. The await operator retrieves the result from getStringTask. The
assignment statement assigns the retrieved result to contents.
8. When GetUrlContentLengthAsync has the string result, the method can calculate
the length of the string. Then the work of GetUrlContentLengthAsync is also
complete, and the waiting event handler can resume. In the full example at the end
of the topic, you can confirm that the event handler retrieves and prints the value
of the length result. If you are new to asynchronous programming, take a minute
to consider the difference between synchronous and asynchronous behavior. A
synchronous method returns when its work is complete (step 5), but an async
method returns a task value when its work is suspended (steps 3 and 6). When the７ Note
If GetStringAsync (and therefore getStringTask) completes before
GetUrlContentLengthAsync awaits it, control remains in
GetUrlContentLengthAsync. The expense of suspending and then returning to
GetUrlContentLengthAsync would be wasted if the called asynchronous
process getStringTask has already completed and GetUrlContentLengthAsync
doesn't have to wait for the final result.async method eventually completes its work, the task is marked as completed and
the result, if any, is stored in the task.
You might be wondering where to find methods such as GetStringAsync that support
async programming. .NET Framework 4.5 or higher and .NET Core contain many
members that work with async and await. You can recognize them by the "Async" suffix
that's appended to the member name, and by their return type of Task or
Task<TR esult> . For example, the System.IO.Stream class contains methods such as
CopyT oAsync , ReadAsync , and WriteAsync  alongside the synchronous methods CopyT o,
Read, and Write .
The Windows Runtime also contains many methods that you can use with async and
await in Windows apps. For more information, see Threading and async programming
for UWP development, and Asynchronous programming (Windows S tore apps)  and
Quickstart: Calling asynchronous APIs in C# or Visual Basic  if you use earlier versions of
the Windows Runtime.
Async methods are intended to be non-blocking operations. An await expression in an
async method doesn't block the current thread while the awaited task is running.
Instead, the expression signs up the rest of the method as a continuation and returns
control to the caller of the async method.
The async and await keywords don't cause additional threads to be created. Async
methods don't require multithreading because an async method doesn't run on its own
thread. The method runs on the current synchronization context and uses time on the
thread only when the method is active. Y ou can use Task.Run  to move CPU-bound work
to a background thread, but a background thread doesn't help with a process that's just
waiting for results to become available.
The async-based approach to asynchronous programming is preferable to existing
approaches in almost every case. In particular, this approach is better than the
BackgroundW orker  class for I/O-bound operations because the code is simpler and you
don't have to guard against race conditions. In combination with the Task.Run  method,
async programming is better than BackgroundW orker  for CPU-bound operations
because async programming separates the coordination details of running your code
from the work that Task.Run transfers to the thread pool.API async methods
ThreadsIf you specify that a method is an async method by using the async  modifier, you enable
the following two capabilities.
The marked async method can use await  to designate suspension points. The
await operator tells the compiler that the async method can't continue past that
point until the awaited asynchronous process is complete. In the meantime,
control returns to the caller of the async method.
The suspension of an async method at an await expression doesn't constitute an
exit from the method, and finally blocks don't run.
The marked async method can itself be awaited by methods that call it.
An async method typically contains one or more occurrences of an await operator, but
the absence of await expressions doesn't cause a compiler error. If an async method
doesn't use an await operator to mark a suspension point, the method executes as a
synchronous method does, despite the async modifier. The compiler issues a warning
for such methods.
async and await are contextual keywords. For more information and examples, see the
following topics:
async
await
An async method typically returns a Task or a Task<TR esult> . Inside an async method, an
await operator is applied to a task that's returned from a call to another async method.
You specify Task<TR esult>  as the return type if the method contains a return  statement
that specifies an operand of type TResult.
You use Task as the return type if the method has no return statement or has a return
statement that doesn't return an operand.
You can also specify any other return type, provided that the type includes a GetAwaiter
method. ValueT ask<TR esult>  is an example of such a type. It is available in the
System.Threading.T asks.Extension  NuGet package.async and await
Return types and parameters
The following example shows how you declare and call a method that returns a
Task<TR esult>  or a Task:
C#
Each returned task represents ongoing work. A task encapsulates information about the
state of the asynchronous process and, eventually, either the final result from the
process or the exception that the process raises if it doesn't succeed.
An async method can also have a void return type. This return type is used primarily to
define event handlers, where a void return type is required. Async event handlers often
serve as the starting point for async programs.
An async method that has a void return type can't be awaited, and the caller of a void-
returning method can't catch any exceptions that the method throws.
An async method can't declare in, ref or out parameters, but the method can call
methods that have such parameters. Similarly, an async method can't return a value by
reference, although it can call methods with ref return values.
For more information and examples, see Async return types (C#) .async Task<int> GetTaskOfTResultAsync ()
{
    int hours = 0;
    await Task.Delay( 0);
    return hours;
}
Task<int> returnedTaskTResult = GetTaskOfTResultAsync();
int intResult = await returnedTaskTResult;
// Single line
// int intResult = await GetTaskOfTResultAsync();
async Task GetTaskAsync ()
{
    await Task.Delay( 0);
    // No return statement needed
}
Task returnedTask = GetTaskAsync();
await returnedTask;
// Single line
await GetTaskAsync();Asynchronous APIs in Windows Runtime programming have one of the following return
types, which are similar to tasks:
IAsyncOperation<TR esult> , which corresponds to Task<TR esult>
IAsyncAction , which corresponds to Task
IAsyncActionWithProgress<TProgress>
IAsyncOperationWithProgress<TR esult,TProgress>
By convention, methods that return commonly awaitable types (for example, Task,
Task<T>, ValueTask, ValueTask<T>) should have names that end with "Async". Methods
that start an asynchronous operation but do not return an awaitable type should not
have names that end with "Async", but may start with "Begin", "S tart", or some other
verb to suggest this method does not return or throw the result of the operation.
You can ignore the convention where an event, base class, or interface contract suggests
a different name. For example, you shouldn't rename common event handlers, such as
OnButtonClick.
Title Descr iption
How to make multiple web requests in
parallel by using async and await (C#)Demonstrates how to start several tasks at the same
time.
Async return types (C#) Illustrates the types that async methods can return,
and explains when each type is appropriate.
Cancel tasks with a cancellation token as a
signaling mechanism.Shows how to add the following functionality to
your async solution:
- Cancel a list of tasks (C#)
- Cancel tasks after a period of time (C#)
- Process asynchronous task as they complete (C#)
Using async for file access (C#) Lists and demonstrates the benefits of using async
and await to access files.
Task-based asynchronous pattern (T AP) Describes an asynchronous pattern, the pattern is
based on the Task and Task<TR esult>  types.
Async Videos on Channel 9 Provides links to a variety of videos about async
programming.Naming convention
Related articles (Visual Studio)Asynchronous programming with async and await
async
awaitSee also
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
 Provide product feedbackAsync return types (C#)
Article •04/08/2023
Async methods can have the following return types:
Task, for an async method that performs an operation but returns no value.
Task<TR esult> , for an async method that returns a value.
void, for an event handler.
Any type that has an accessible GetAwaiter method. The object returned by the
GetAwaiter method must implement the
System.Runtime.CompilerServices.ICriticalNotifyCompletion  interface.
IAsyncEnumerable<T> , for an async method that returns an async str eam.
For more information about async methods, see Asynchronous programming with async
and await (C#) .
Several other types also exist that are specific to Windows workloads:
DispatcherOperation , for async operations limited to Windows.
IAsyncAction , for async actions in UWP that don't return a value.
IAsyncActionWithProgress<TProgress> , for async actions in UWP that report
progress but don't return a value.
IAsyncOperation<TR esult> , for async operations in UWP that return a value.
IAsyncOperationWithProgress<TR esult,TProgress> , for async operations in UWP
that report progress and return a value.
Async methods that don't contain a return statement or that contain a return
statement that doesn't return an operand usually have a return type of Task. Such
methods return void if they run synchronously. If you use a Task return type for an
async method, a calling method can use an await operator to suspend the caller's
completion until the called async method has finished.
In the following example, the WaitAndApologizeAsync method doesn't contain a return
statement, so the method returns a Task object. R eturning a Task enables
WaitAndApologizeAsync to be awaited. The Task type doesn't include a Result property
because it has no return value.
C#Task return typeWaitAndApologizeAsync is awaited by using an await statement instead of an await
expression, similar to the calling statement for a synchronous void-returning method.
The application of an await operator in this case doesn't produce a value. When the
right operand of an await is a Task<TR esult> , the await expression produces a result of
T. When the right operand of an await is a Task, the await and its operand are a
statement.
You can separate the call to WaitAndApologizeAsync from the application of an await
operator, as the following code shows. However, remember that a Task doesn't have a
Result property, and that no value is produced when an await operator is applied to a
Task.
The following code separates calling the WaitAndApologizeAsync method from awaiting
the task that the method returns.
C#public static async Task DisplayCurrentInfoAsync () 
{ 
    await WaitAndApologizeAsync();  
    Console.WriteLine( $"Today is {DateTime.Now:D} "); 
    Console.WriteLine( $"The current time is {DateTime.Now.TimeOfDay:t} "); 
    Console.WriteLine( "The current temperature is 76 degrees." ); 
} 
static async Task WaitAndApologizeAsync () 
{ 
    await Task.Delay( 2000); 
    Console.WriteLine( "Sorry for the delay...\n" ); 
} 
// Example output:  
//    Sorry for the delay...  
// 
// Today is Monday, August 17, 2020  
// The current time is 12:59:24.2183304  
// The current temperature is 76 degrees.  
Task waitAndApologizeTask = WaitAndApologizeAsync();  
string output =  
    $"Today is {DateTime.Now:D} \n" + 
    $"The current time is {DateTime.Now.TimeOfDay:t} \n" + 
    "The current temperature is 76 degrees.\n" ; 
await waitAndApologizeTask;  
Console.WriteLine(output);  The Task<TR esult>  return type is used for an async method that contains a return
statement in which the operand is TResult.
In the following example, the GetLeisureHoursAsync method contains a return
statement that returns an integer. The method declaration must specify a return type of
Task<int>. The FromR esult  async method is a placeholder for an operation that returns
a DayOfW eek.
C#
When GetLeisureHoursAsync is called from within an await expression in the
ShowTodaysInfo method, the await expression retrieves the integer value (the value of
leisureHours) that's stored in the task returned by the GetLeisureHours method. For
more information about await expressions, see await .
You can better understand how await retrieves the result from a Task<T> by separating
the call to GetLeisureHoursAsync from the application of await, as the following code
shows. A call to method GetLeisureHoursAsync that isn't immediately awaited returns a
Task<int>, as you would expect from the declaration of the method. The task isTask<TResult> return type
public static async Task ShowTodaysInfoAsync () 
{ 
    string message =  
        $"Today is {DateTime.Today:D} \n" + 
        "Today's hours of leisure: "  + 
        $"{await GetLeisureHoursAsync()} "; 
    Console.WriteLine(message);  
} 
static async Task<int> GetLeisureHoursAsync () 
{ 
    DayOfWeek today = await Task.FromResult(DateTime.Now.DayOfWeek);  
    int leisureHours =  
        today is DayOfWeek.Saturday || today is DayOfWeek.Sunday  
        ? 16 : 5; 
    return leisureHours;  
} 
// Example output:  
//    Today is Wednesday, May 24, 2017  
//    Today's hours of leisure: 5assigned to the getLeisureHoursTask variable in the example. Because
getLeisureHoursTask is a Task<TR esult> , it contains a Result  property of type TResult.
In this case, TResult represents an integer type. When await is applied to
getLeisureHoursTask, the await expression evaluates to the contents of the Result
property of getLeisureHoursTask. The value is assigned to the ret variable.
C#
You use the void return type in asynchronous event handlers, which require a void
return type. For methods other than event handlers that don't return a value, you should
return a Task instead, because an async method that returns void can't be awaited. Any
caller of such a method must continue to completion without waiting for the called
async method to finish. The caller must be independent of any values or exceptions that
the async method generates.
The caller of a void-returning async method can't catch exceptions thrown from the
method. Such unhandled exceptions are likely to cause your application to fail. If a
method that returns a Task or Task<TR esult>  throws an exception, the exception is
stored in the returned task. The exception is rethrown when the task is awaited. Make） Impor tant
The Result  property is a blocking property. If you try to access it before its task is
finished, the thread that's currently active is blocked until the task completes and
the value is available. In most cases, you should access the value by using await
instead of accessing the property directly.
The previous example retrieved the value of the Result  property to block the main
thread so that the Main method could print the message to the console before the
application ended.
var getLeisureHoursTask = GetLeisureHoursAsync();  
string message =  
    $"Today is {DateTime.Today:D} \n" + 
    "Today's hours of leisure: "  + 
    $"{await getLeisureHoursTask} "; 
Console.WriteLine(message);  
Void return typesure that any async method that can produce an exception has a return type of Task or
Task<TR esult>  and that calls to the method are awaited.
The following example shows the behavior of an async event handler. In the example
code, an async event handler must let the main thread know when it finishes. Then the
main thread can wait for an async event handler to complete before exiting the
program.
C#
public class NaiveButton  
{ 
    public event EventHandler? Clicked;  
    public void Click() 
    { 
        Console.WriteLine( "Somebody has clicked a button. Let's raise the  
event..." ); 
        Clicked?.Invoke( this, EventArgs.Empty);  
        Console.WriteLine( "All listeners are notified." ); 
    } 
} 
public class AsyncVoidExample  
{ 
    static readonly  TaskCompletionSource< bool> s_tcs = new 
TaskCompletionSource< bool>(); 
    public static async Task MultipleEventHandlersAsync () 
    { 
        Task< bool> secondHandlerFinished = s_tcs.Task;  
        var button = new NaiveButton();  
        button.Clicked += OnButtonClicked1;  
        button.Clicked += OnButtonClicked2Async;  
        button.Clicked += OnButtonClicked3;  
        Console.WriteLine( "Before button.Click() is called..." ); 
        button.Click();  
        Console.WriteLine( "After button.Click() is called..." ); 
        await secondHandlerFinished;  
    } 
    private static void OnButtonClicked1 (object? sender, EventArgs e ) 
    { 
        Console.WriteLine( "   Handler 1 is starting..." ); 
        Task.Delay( 100).Wait();  
        Console.WriteLine( "   Handler 1 is done." ); 
    } An async method can return any type that has an accessible GetAwaiter method that
returns an instance of an await er type . In addition, the type returned from the
GetAwaiter method must have the
System.Runtime.CompilerServices.AsyncMethodBuilderAttribute  attribute. Y ou can learn
more in the article on Attributes read by the compiler  or the C# spec for the Task type
builder pattern .
This feature is the complement to awaitable expressions , which describes the
requirements for the operand of await. Generalized async return types enable the
compiler to generate async methods that return different types. Generalized async
return types enabled performance improvements in the .NET libraries. Because Task and
Task<TR esult>  are reference types, memory allocation in performance-critical paths,    private static async void OnButtonClicked2Async (object? sender,  
EventArgs e ) 
    { 
        Console.WriteLine( "   Handler 2 is starting..." ); 
        Task.Delay( 100).Wait();  
        Console.WriteLine( "   Handler 2 is about to go async..." );
        await Task.Delay( 500); 
        Console.WriteLine( "   Handler 2 is done." ); 
        s_tcs.SetResult( true); 
    } 
    private static void OnButtonClicked3 (object? sender, EventArgs e ) 
    { 
        Console.WriteLine( "   Handler 3 is starting..." ); 
        Task.Delay( 100).Wait();  
        Console.WriteLine( "   Handler 3 is done." ); 
    } 
} 
// Example output:  
// 
// Before button.Click() is called...  
// Somebody has clicked a button. Let's raise the event...  
//    Handler 1 is starting...  
//    Handler 1 is done.  
//    Handler 2 is starting...  
//    Handler 2 is about to go async...  
//    Handler 3 is starting...  
//    Handler 3 is done.  
// All listeners are notified.  
// After button.Click() is called...  
//    Handler 2 is done.  
Generalized async return types and
ValueTask<TResult>particularly when allocations occur in tight loops, can adversely affect performance.
Support for generalized return types means that you can return a lightweight value type
instead of a reference type to avoid additional memory allocations.
.NET provides the System.Threading.T asks.V alueT ask<TR esult>  structure as a lightweight
implementation of a generalized task-returning value. The following example uses the
ValueT ask<TR esult>  structure to retrieve the value of two dice rolls.
C#
Writing a generalized async return type is an advanced scenario, and is targeted for use
in specialized environments. Consider using the Task, Task<T>, and ValueTask<T> types
instead, which cover most scenarios for asynchronous code.
In C# 10 and later, you can apply the AsyncMethodBuilder attribute to an async method
(instead of the async return type declaration) to override the builder for that type.
Typically you'd apply this attribute to use a different builder provided in the .NET
runtime.class Program 
{ 
    static readonly  Random s_rnd = new Random();  
    static async Task Main() => 
        Console.WriteLine( $"You rolled {await GetDiceRollAsync()} "); 
    static async ValueTask< int> GetDiceRollAsync () 
    { 
        Console.WriteLine( "Shaking dice..." ); 
        int roll1 = await RollAsync();  
        int roll2 = await RollAsync();  
        return roll1 + roll2;  
    } 
    static async ValueTask< int> RollAsync () 
    { 
        await Task.Delay( 500); 
        int diceRoll = s_rnd.Next( 1, 7); 
        return diceRoll;  
    } 
} 
// Example output:  
//    Shaking dice...  
//    You rolled 8  An async method may return an async str eam, represented by IAsyncEnumerable<T> .
An async stream provides a way to enumerate items read from a stream when elements
are generated in chunks with repeated asynchronous calls. The following example shows
an async method that generates an async stream:
C#
The preceding example reads lines from a string asynchronously. Once each line is read,
the code enumerates each word in the string. Callers would enumerate each word using
the await foreach statement. The method awaits when it needs to asynchronously read
the next line from the source string.
FromR esult
Process asynchronous tasks as they complete
Asynchronous programming with async and await (C#)
async
awaitAsync streams with IAsyncEnum erable<T>
static async IAsyncEnumerable< string> ReadWordsFromStreamAsync () 
{ 
    string data = 
        @"This is a line of text.
              Here is the second line of text.  
              And there is one more for good measure.  
              Wait, that was the penultimate line." ; 
    using var readStream = new StringReader(data);  
    string? line = await readStream.ReadLineAsync();  
    while (line != null) 
    { 
        foreach (string word in line.Split( ' ', 
StringSplitOptions.RemoveEmptyEntries))  
        {  
            yield return word; 
        }  
        line = await readStream.ReadLineAsync();  
    } 
} 
See alsoProcess asynchronous tasks as they
complete (C#)
Article •05/23/2023
By using Task.WhenAny , you can start multiple tasks at the same time and process them
one by one as they're completed rather than process them in the order in which they're
started.
The following example uses a query to create a collection of tasks. Each task downloads
the contents of a specified website. In each iteration of a while loop, an awaited call to
WhenAny  returns the task in the collection of tasks that finishes its download first. That
task is removed from the collection and processed. The loop repeats until the collection
contains no more tasks.
You can follow this tutorial by using one of the following options:
Visual S tudio 2022  with the .NET desk top dev elopment  workload installed. The
.NET SDK is automatically installed when you select this workload.
The .NET SDK  with a code editor of your choice, such as Visual S tudio Code .
Create a new .NET Core console application. Y ou can create one by using the dotnet
new console  command or from Visual S tudio.
Open the Program.cs  file in your code editor, and replace the existing code with this
code:
C#Prerequisites
Create example application
using System.Diagnostics;  
namespace  ProcessTasksAsTheyFinish ; 
class Program 
{ 
    static void Main(string[] args) 
    { 
        Console.WriteLine( "Hello World!" ); 
    } 
} In the Program class definition, add the following two fields:
C#
The HttpClient exposes the ability to send HT TP requests and receive HT TP responses.
The s_urlList holds all of the URLs that the application plans to process.
The main entry point into the console application is the Main method. R eplace the
existing method with the following:
C#Add fields
static readonly  HttpClient s_client = new HttpClient  
{ 
    MaxResponseContentBufferSize = 1_000_000  
}; 
static readonly  IEnumerable< string> s_urlList = new string[] 
{ 
    "https://learn.microsoft.com" , 
    "https://learn.microsoft.com/aspnet/core" , 
    "https://learn.microsoft.com/azure" , 
    "https://learn.microsoft.com/azure/devops" , 
    "https://learn.microsoft.com/dotnet" , 
    "https://learn.microsoft.com/dynamics365" , 
    "https://learn.microsoft.com/education" , 
    "https://learn.microsoft.com/enterprise-mobility-security" , 
    "https://learn.microsoft.com/gaming" , 
    "https://learn.microsoft.com/graph" , 
    "https://learn.microsoft.com/microsoft-365" , 
    "https://learn.microsoft.com/office" , 
    "https://learn.microsoft.com/powershell" , 
    "https://learn.microsoft.com/sql" , 
    "https://learn.microsoft.com/surface" , 
    "https://learn.microsoft.com/system-center" , 
    "https://learn.microsoft.com/visualstudio" , 
    "https://learn.microsoft.com/windows" , 
    "https://learn.microsoft.com/xamarin"  
}; 
Update application entry point
static Task Main() => SumPageSizesAsync();  The updated Main method is now considered an Async main , which allows for an
asynchronous entry point into the executable. It is expressed as a call to
SumPageSizesAsync.
Below the Main method, add the SumPageSizesAsync method:
C#
The while loop removes one of the tasks in each iteration. After every task has
completed, the loop ends. The method starts by instantiating and starting a Stopwatch .
It then includes a query that, when executed, creates a collection of tasks. Each call to
ProcessUrlAsync in the following code returns a Task<TR esult> , where TResult is an
integer:
C#Create the asynchronous sum page sizes
method
static async Task SumPageSizesAsync () 
{ 
    var stopwatch = Stopwatch.StartNew();  
    IEnumerable<Task< int>> downloadTasksQuery =  
        from url in s_urlList  
        select ProcessUrlAsync (url, s_client ); 
    List<Task< int>> downloadTasks = downloadTasksQuery.ToList();  
    int total = 0; 
    while (downloadTasks.Any())  
    { 
        Task< int> finishedTask = await Task.WhenAny(downloadTasks);  
        downloadTasks.Remove(finishedTask);  
        total += await finishedTask;  
    } 
    stopwatch.Stop();  
    Console.WriteLine( $"\nTotal bytes returned:  {total:#,#} "); 
    Console.WriteLine( $"Elapsed time:          {stopwatch.Elapsed} \n"); 
} 
IEnumerable<Task< int>> downloadTasksQuery =  
    from url in s_urlList  
    select ProcessUrlAsync (url, s_client ); Due to deferred execution  with the LINQ, you call Enumerable.T oList  to start each task.
C#
The while loop performs the following steps for each task in the collection:
1. Awaits a call to WhenAny to identify the first task in the collection that has finished
its download.
C#
2. Removes that task from the collection.
C#
3. Awaits finishedTask, which is returned by a call to ProcessUrlAsync. The
finishedTask variable is a Task<TR esult>  where TResult is an integer. The task is
already complete, but you await it to retrieve the length of the downloaded
website, as the following example shows. If the task is faulted, await will throw the
first child exception stored in the AggregateException, unlike reading the
Task<TR esult>.R esult  property, which would throw the AggregateException.
C#
Add the following ProcessUrlAsync method below the SumPageSizesAsync method:
C#List<Task< int>> downloadTasks = downloadTasksQuery.ToList();  
Task<int> finishedTask = await Task.WhenAny(downloadTasks);  
downloadTasks.Remove(finishedTask);  
total += await finishedTask;  
Add process method
static async Task<int> ProcessUrlAsync (string url, HttpClient client ) 
{ 
    byte[] content = await client.GetByteArrayAsync(url);  
    Console.WriteLine( $"{url,-60} {content.Length, 10:#,#}"); For any given URL, the method will use the client instance provided to get the
response as a byte[]. The length is returned after the URL and length is written to the
console.
Run the program several times to verify that the downloaded lengths don't always
appear in the same order.
The following code is the complete text of the Program.cs  file for the example.
C#    return content.Length;  
} 
Ｕ Caution
You can use WhenAny in a loop, as described in the example, to solve problems that
involve a small number of tasks. However, other approaches are more efficient if
you have a large number of tasks to process. For more information and examples,
see Processing tasks as they complet e.
Complete example
using System.Diagnostics;  
HttpClient s_client = new() 
{ 
    MaxResponseContentBufferSize = 1_000_000  
}; 
IEnumerable< string> s_urlList = new string[] 
{ 
    "https://learn.microsoft.com" , 
    "https://learn.microsoft.com/aspnet/core" , 
    "https://learn.microsoft.com/azure" , 
    "https://learn.microsoft.com/azure/devops" , 
    "https://learn.microsoft.com/dotnet" , 
    "https://learn.microsoft.com/dynamics365" , 
    "https://learn.microsoft.com/education" , 
    "https://learn.microsoft.com/enterprise-mobility-security" , 
    "https://learn.microsoft.com/gaming" , 
    "https://learn.microsoft.com/graph" , 
    "https://learn.microsoft.com/microsoft-365" , 
    "https://learn.microsoft.com/office" , 
    "https://learn.microsoft.com/powershell" , 
    "https://learn.microsoft.com/sql" , 
    "https://learn.microsoft.com/surface" ,     "https://learn.microsoft.com/system-center" , 
    "https://learn.microsoft.com/visualstudio" , 
    "https://learn.microsoft.com/windows" , 
    "https://learn.microsoft.com/xamarin"  
}; 
await SumPageSizesAsync();  
async Task SumPageSizesAsync () 
{ 
    var stopwatch = Stopwatch.StartNew();  
    IEnumerable<Task< int>> downloadTasksQuery =  
        from url in s_urlList  
        select ProcessUrlAsync (url, s_client ); 
    List<Task< int>> downloadTasks = downloadTasksQuery.ToList();  
    int total = 0; 
    while (downloadTasks.Any())  
    { 
        Task< int> finishedTask = await Task.WhenAny(downloadTasks);  
        downloadTasks.Remove(finishedTask);  
        total += await finishedTask;  
    } 
    stopwatch.Stop();  
    Console.WriteLine( $"\nTotal bytes returned:    {total:#,#} "); 
    Console.WriteLine( $"Elapsed time:              {stopwatch.Elapsed} \n"); 
} 
static async Task<int> ProcessUrlAsync (string url, HttpClient client ) 
{ 
    byte[] content = await client.GetByteArrayAsync(url);  
    Console.WriteLine( $"{url,-60} {content.Length, 10:#,#}"); 
    return content.Length;  
} 
// Example output:  
// https://learn.microsoft.com                                      132,517  
// https://learn.microsoft.com/powershell                            57,375  
// https://learn.microsoft.com/gaming                                33,549  
// https://learn.microsoft.com/aspnet/core                           88,714  
// https://learn.microsoft.com/surface                               39,840  
// https://learn.microsoft.com/enterprise-mobility-security          30,903  
// https://learn.microsoft.com/microsoft-365                         67,867  
// https://learn.microsoft.com/windows                               26,816  
// https://learn.microsoft.com/xamarin                               57,958  
// https://learn.microsoft.com/dotnet                                78,706  
// https://learn.microsoft.com/graph                                 48,277  
// https://learn.microsoft.com/dynamics365                           49,042  
// https://learn.microsoft.com/office                                67,867  
// https://learn.microsoft.com/system-center                         42,887  WhenAny
Asynchronous programming with async and await (C#)// https://learn.microsoft.com/education                             38,636  
// https://learn.microsoft.com/azure                                421,663  
// https://learn.microsoft.com/visualstudio                          30,925  
// https://learn.microsoft.com/sql                                   54,608  
// https://learn.microsoft.com/azure/devops                          86,034  
// Total bytes returned:    1,454,184  
// Elapsed time:            00:00:01.1290403  
See alsoAsynchronous file access (C#)
Article •02/13/2023
You can use the async feature to access files. By using the async feature, you can call
into asynchronous methods without using callbacks or splitting your code across
multiple methods or lambda expressions. T o make synchronous code asynchronous, you
just call an asynchronous method instead of a synchronous method and add a few
keywords to the code.
You might consider the following reasons for adding asynchrony to file access calls:
The simple examples in this topic demonstrate File.WriteAllT extAsync  and
File.R eadAllT extAsync . For fine control over the file I/O operations, use the FileStream
class, which has an option that causes asynchronous I/O to occur at the operating
system level. By using this option, you can avoid blocking a thread pool thread in many
cases. T o enable this option, you specify the useAsync=true or
options=FileOptions.Asynchronous argument in the constructor call.
You can't use this option with StreamR eader  and StreamWriter  if you open them directly
by specifying a file path. However, you can use this option if you provide them a Stream
that the FileStream  class opened. Asynchronous calls are faster in UI apps even if a
thread pool thread is blocked, because the UI thread isn't blocked during the wait.Asynchrony makes UI applications more responsive because the UI thread that
launches the operation can perform other work. If the UI thread must execute code
that takes a long time (for example, more than 50 milliseconds), the UI may freeze
until the I/O is complete and the UI thread can again process keyboard and mouse
input and other events.＂
Asynchrony improves the scalability of ASP.NET and other server-based applications
by reducing the need for threads. If the application uses a dedicated thread per
response and a thousand requests are being handled simultaneously, a thousand
threads are needed. Asynchronous operations often don't need to use a thread
during the wait. They use the existing I/O completion thread briefly at the end.＂
The latency of a file access operation might be very low under current conditions,
but the latency may greatly increase in the future. For example, a file may be moved
to a server that's across the world.＂
The added overhead of using the Async feature is small. ＂
Asynchronous tasks can easily be run in parallel. ＂
Use appropriate classesThe following examples write text to a file. At each await statement, the method
immediately exits. When the file I/O is complete, the method resumes at the statement
that follows the await statement. The async modifier is in the definition of methods that
use the await statement.
C#
C#
The original example has the statement await sourceStream.WriteAsync(encodedText, 0,
encodedText.Length);, which is a contraction of the following two statements:Write text
Simple example
public async Task SimpleWriteAsync () 
{ 
    string filePath = "simple.txt" ; 
    string text = $"Hello World" ; 
    await File.WriteAllTextAsync(filePath, text);  
} 
Finite control example
public async Task ProcessWriteAsync () 
{ 
    string filePath = "temp.txt" ; 
    string text = $"Hello World {Environment.NewLine} "; 
    await WriteTextAsync(filePath, text);  
} 
async Task WriteTextAsync (string filePath, string text) 
{ 
    byte[] encodedText = Encoding.Unicode.GetBytes(text);  
    using var sourceStream =  
        new FileStream(  
            filePath,  
            FileMode.Create, FileAccess.Write, FileShare.None,  
            bufferSize: 4096, useAsync: true); 
    await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
} C#
The first statement returns a task and causes file processing to start. The second
statement with the await causes the method to immediately exit and return a different
task. When the file processing later completes, execution returns to the statement that
follows the await.
The following examples read text from a file.
C#
The text is buffered and, in this case, placed into a StringBuilder . Unlike in the previous
example, the evaluation of the await produces a value. The ReadAsync  method returns a
Task<Int32 >, so the evaluation of the await produces an Int32 value numRead after the
operation completes. For more information, see Async R eturn T ypes (C#) .
C#Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
await theTask;  
Read text
Simple example
public async Task SimpleReadAsync () 
{ 
    string filePath = "simple.txt" ; 
    string text = await File.ReadAllTextAsync(filePath);  
    Console.WriteLine(text);  
} 
Finite control example
public async Task ProcessReadAsync () 
{ 
    try 
    { 
        string filePath = "temp.txt" ; 
        if (File.Exists(filePath) != false) 
        {  
            string text = await ReadTextAsync(filePath);  
            Console.WriteLine(text);  The following examples demonstrate parallel processing by writing 10 text files.
C#        }  
        else 
        {  
            Console.WriteLine( $"file not found: {filePath} "); 
        }  
    } 
    catch (Exception ex)  
    { 
        Console.WriteLine(ex.Message);  
    } 
} 
async Task<string> ReadTextAsync (string filePath ) 
{ 
    using var sourceStream =  
        new FileStream(  
            filePath,  
            FileMode.Open, FileAccess.Read, FileShare.Read,  
            bufferSize: 4096, useAsync: true); 
    var sb = new StringBuilder();  
    byte[] buffer = new byte[0x1000]; 
    int numRead;  
    while ((numRead = await sourceStream.ReadAsync(buffer, 0, 
buffer.Length)) != 0) 
    { 
        string text = Encoding.Unicode.GetString(buffer, 0, numRead);  
        sb.Append(text);  
    } 
    return sb.ToString();  
} 
Parallel asynchronous I/O
Simple example
public async Task SimpleParallelWriteAsync () 
{ 
    string folder = Directory.CreateDirectory( "tempfolder" ).Name; 
    IList<Task> writeTaskList = new List<Task>();  
    for (int index = 11; index <= 20; ++ index)  
    { 
        string fileName = $"file-{index:00}.txt"; For each file, the WriteAsync  method returns a task that is then added to a list of tasks.
The await Task.WhenAll(tasks); statement exits the method and resumes within the
method when file processing is complete for all of the tasks.
The example closes all FileStream  instances in a finally block after the tasks are
complete. If each FileStream was instead created in a using statement, the FileStream
might be disposed of before the task was complete.
Any performance boost is almost entirely from the parallel processing and not the
asynchronous processing. The advantages of asynchrony are that it doesn't tie up
multiple threads, and that it doesn't tie up the user interface thread.
C#        string filePath = $"{folder} /{fileName} "; 
        string text = $"In file {index}{Environment.NewLine} "; 
        writeTaskList.Add(File.WriteAllTextAsync(filePath, text));  
    } 
    await Task.WhenAll(writeTaskList);  
} 
Finite control example
public async Task ProcessMultipleWritesAsync () 
{ 
    IList<FileStream> sourceStreams = new List<FileStream>();  
    try 
    { 
        string folder = Directory.CreateDirectory( "tempfolder" ).Name; 
        IList<Task> writeTaskList = new List<Task>();  
        for (int index = 1; index <= 10; ++ index)  
        {  
            string fileName = $"file-{index:00}.txt"; 
            string filePath = $"{folder} /{fileName} "; 
            string text = $"In file {index}{Environment.NewLine} "; 
            byte[] encodedText = Encoding.Unicode.GetBytes(text);  
            var sourceStream =  
                new FileStream(  
                    filePath,  
                    FileMode.Create, FileAccess.Write, FileShare.None,  
                    bufferSize: 4096, useAsync: true); 
            Task writeTask = sourceStream.WriteAsync(encodedText, 0, When using the WriteAsync  and ReadAsync  methods, you can specify a
CancellationT oken , which you can use to cancel the operation mid-stream. For more
information, see Cancellation in managed threads .
Asynchronous programming with async and await (C#)
Async return types (C#)encodedText.Length);  
            sourceStreams.Add(sourceStream);  
            writeTaskList.Add(writeTask);  
        }  
        await Task.WhenAll(writeTaskList);  
    } 
    finally 
    { 
        foreach (FileStream sourceStream in sourceStreams)  
        {  
            sourceStream.Close();
        }  
    } 
} 
See alsoCancel a list of tasks
Article •02/13/2023
You can cancel an async console application if you don't want to wait for it to finish. By
following the example in this topic, you can add a cancellation to an application that
downloads the contents of a list of websites. Y ou can cancel many tasks by associating
the CancellationT okenSource  instance with each task. If you select the Enter  key, you
cancel all tasks that aren't yet complete.
This tutorial covers:
This tutorial requires the following:
.NET 5 or later SDK
Integrated development environment (IDE)
We recommend Visual S tudio or Visual S tudio Code
Create a new .NET Core console application. Y ou can create one by using the dotnet
new console  command or from Visual S tudio . Open the Program.cs  file in your favorite
code editor.
Replace the existing using statements with these declarations:
C#Creating a .NET console application ＂
Writing an async application that supports cancellation ＂
Demonstrating signaling cancellation ＂
Prerequisites
Create example application
Replace using statements
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;In the Program class definition, add these three fields:
C#
The CancellationT okenSource  is used to signal a requested cancellation to a
CancellationT oken . The HttpClient exposes the ability to send HT TP requests and
receive HT TP responses. The s_urlList holds all of the URLs that the application plans
to process.
The main entry point into the console application is the Main method. R eplace the
existing method with the following:
C#Add fields
static readonly  CancellationTokenSource s_cts = new 
CancellationTokenSource();
static readonly  HttpClient s_client = new HttpClient
{
    MaxResponseContentBufferSize = 1_000_000
};
static readonly  IEnumerable< string> s_urlList = new string[]
{
    "https://learn.microsoft.com" ,
    "https://learn.microsoft.com/aspnet/core" ,
    "https://learn.microsoft.com/azure" ,
    "https://learn.microsoft.com/azure/devops" ,
    "https://learn.microsoft.com/dotnet" ,
    "https://learn.microsoft.com/dynamics365" ,
    "https://learn.microsoft.com/education" ,
    "https://learn.microsoft.com/enterprise-mobility-security" ,
    "https://learn.microsoft.com/gaming" ,
    "https://learn.microsoft.com/graph" ,
    "https://learn.microsoft.com/microsoft-365" ,
    "https://learn.microsoft.com/office" ,
    "https://learn.microsoft.com/powershell" ,
    "https://learn.microsoft.com/sql" ,
    "https://learn.microsoft.com/surface" ,
    "https://learn.microsoft.com/system-center" ,
    "https://learn.microsoft.com/visualstudio" ,
    "https://learn.microsoft.com/windows" ,
    "https://learn.microsoft.com/xamarin"
};
Update application entry pointThe updated Main method is now considered an Async main , which allows for an
asynchronous entry point into the executable. It writes a few instructional messages to
the console, then declares a Task instance named cancelTask, which will read console
key strokes. If the Enter  key is pressed, a call to CancellationT okenSource.Cancel()  is
made. This will signal cancellation. Next, the sumPageSizesTask variable is assigned from
the SumPageSizesAsync method. Both tasks are then passed to Task.WhenAny(T ask[]) ,
which will continue when any of the two tasks have completed.
The next block of code ensures that the application doesn't exit until the cancellation
has been processed. If the first task to complete is the cancelTask, the sumPageSizeTask
is awaited. If it was cancelled, when awaited it throws astatic async Task Main()
{
    Console.WriteLine( "Application started." );
    Console.WriteLine( "Press the ENTER key to cancel...\n" );
    Task cancelTask = Task.Run(() =>
    {
        while (Console.ReadKey().Key != ConsoleKey.Enter)
        {
            Console.WriteLine( "Press the ENTER key to cancel..." );
        }
        Console.WriteLine( "\nENTER key pressed: cancelling downloads.\n" );
        s_cts.Cancel();
    });
    
    Task sumPageSizesTask = SumPageSizesAsync();
    Task finishedTask = await Task.WhenAny( new[] { cancelTask,  
sumPageSizesTask });
    if (finishedTask == cancelTask)
    {
        // wait for the cancellation to take place:
        try
        {
            await sumPageSizesTask;
            Console.WriteLine( "Download task completed before cancel request  
was processed." );
        }
        catch (TaskCanceledException)
        {
            Console.WriteLine( "Download task has been cancelled." );
        }
    }
        
    Console.WriteLine( "Application ending." );
}System.Threading.T asks.T askCanceledException . The block catches that exception, and
prints a message.
Below the Main method, add the SumPageSizesAsync method:
C#
The method starts by instantiating and starting a Stopwatch . It then loops through each
URL in the s_urlList and calls ProcessUrlAsync. With each iteration, the s_cts.Token is
passed into the ProcessUrlAsync method and the code returns a Task<TR esult> , where
TResult is an integer:
C#
Add the following ProcessUrlAsync method below the SumPageSizesAsync method:Create the asynchronous sum page sizes
method
static async Task SumPageSizesAsync ()
{
    var stopwatch = Stopwatch.StartNew();
    int total = 0;
    foreach (string url in s_urlList)
    {
        int contentLength = await ProcessUrlAsync(url, s_client,  
s_cts.Token);
        total += contentLength;
    }
    stopwatch.Stop();
    Console.WriteLine( $"\nTotal bytes returned:  {total:#,#} ");
    Console.WriteLine( $"Elapsed time:          {stopwatch.Elapsed} \n");
}
int total = 0;
foreach (string url in s_urlList)
{
    int contentLength = await ProcessUrlAsync(url, s_client, s_cts.Token);
    total += contentLength;
}
Add process methodC#
For any given URL, the method will use the client instance provided to get the
response as a byte[]. The CancellationT oken  instance is passed into the
HttpClient.GetAsync(S tring, CancellationT oken)  and
HttpContent.R eadAsByteArrayAsync()  methods. The token is used to register for
requested cancellation. The length is returned after the URL and length is written to the
console.
Console
The following code is the complete text of the Program.cs  file for the example.
C#static async Task<int> ProcessUrlAsync (string url, HttpClient client,  
CancellationToken token )
{
    HttpResponseMessage response = await client.GetAsync(url, token);
    byte[] content = await response.Content.ReadAsByteArrayAsync(token);
    Console.WriteLine( $"{url,-60} {content.Length, 10:#,#}");
    return content.Length;
}
Example application output
Application started.
Press the ENTER key to cancel...
https://learn.microsoft.com                                       37,357
https://learn.microsoft.com/aspnet/core                           85,589
https://learn.microsoft.com/azure                                398,939
https://learn.microsoft.com/azure/devops                          73,663
https://learn.microsoft.com/dotnet                                67,452
https://learn.microsoft.com/dynamics365                           48,582
https://learn.microsoft.com/education                             22,924
ENTER key pressed: cancelling downloads.
Application ending.
Complete example
using System.Diagnostics;class Program
{
    static readonly  CancellationTokenSource s_cts = new 
CancellationTokenSource();
    static readonly  HttpClient s_client = new HttpClient
    {
        MaxResponseContentBufferSize = 1_000_000
    };
    static readonly  IEnumerable< string> s_urlList = new string[]
    {
            "https://learn.microsoft.com" ,
            "https://learn.microsoft.com/aspnet/core" ,
            "https://learn.microsoft.com/azure" ,
            "https://learn.microsoft.com/azure/devops" ,
            "https://learn.microsoft.com/dotnet" ,
            "https://learn.microsoft.com/dynamics365" ,
            "https://learn.microsoft.com/education" ,
            "https://learn.microsoft.com/enterprise-mobility-security" ,
            "https://learn.microsoft.com/gaming" ,
            "https://learn.microsoft.com/graph" ,
            "https://learn.microsoft.com/microsoft-365" ,
            "https://learn.microsoft.com/office" ,
            "https://learn.microsoft.com/powershell" ,
            "https://learn.microsoft.com/sql" ,
            "https://learn.microsoft.com/surface" ,
            "https://learn.microsoft.com/system-center" ,
            "https://learn.microsoft.com/visualstudio" ,
            "https://learn.microsoft.com/windows" ,
            "https://learn.microsoft.com/xamarin"
    };
    static async Task Main()
    {
        Console.WriteLine( "Application started." );
        Console.WriteLine( "Press the ENTER key to cancel...\n" );
        Task cancelTask = Task.Run(() =>
        {
            while (Console.ReadKey().Key != ConsoleKey.Enter)
            {
                Console.WriteLine( "Press the ENTER key to cancel..." );
            }
            Console.WriteLine( "\nENTER key pressed: cancelling  
downloads.\n" );
            s_cts.Cancel();
        });
        Task sumPageSizesTask = SumPageSizesAsync();
        Task finishedTask = await Task.WhenAny( new[] { cancelTask,  
sumPageSizesTask });
        if (finishedTask == cancelTask)CancellationT oken
CancellationT okenSource
Asynchronous programming with async and await (C#)        {
            // wait for the cancellation to take place:
            try
            {
                await sumPageSizesTask;
                Console.WriteLine( "Download task completed before cancel  
request was processed." );
            }
            catch (TaskCanceledException)
            {
                Console.WriteLine( "Download task has been cancelled." );
            }
        }
        Console.WriteLine( "Application ending." );
    }
    static async Task SumPageSizesAsync ()
    {
        var stopwatch = Stopwatch.StartNew();
        int total = 0;
        foreach (string url in s_urlList)
        {
            int contentLength = await ProcessUrlAsync(url, s_client,  
s_cts.Token);
            total += contentLength;
        }
        stopwatch.Stop();
        Console.WriteLine( $"\nTotal bytes returned:  {total:#,#} ");
        Console.WriteLine( $"Elapsed time:          {stopwatch.Elapsed} \n");
    }
    static async Task<int> ProcessUrlAsync (string url, HttpClient client,  
CancellationToken token )
    {
        HttpResponseMessage response = await client.GetAsync(url, token);
        byte[] content = await response.Content.ReadAsByteArrayAsync(token);
        Console.WriteLine( $"{url,-60} {content.Length, 10:#,#}");
        return content.Length;
    }
}
See alsoNext steps
Cancel async tasks af ter a period o f time (C#)Cancel async tasks after a period of time
Article •09/08/2023
You can cancel an asynchronous operation after a period of time by using the
CancellationT okenSource.CancelAfter  method if you don't want to wait for the operation
to finish. This method schedules the cancellation of any associated tasks that aren't
complete within the period of time that's designated by the CancelAfter expression.
This example adds to the code that's developed in Cancel a list of tasks (C#)  to
download a list of websites and to display the length of the contents of each one.
This tutorial covers:
This tutorial requires the following:
You're expected to have created an application in the Cancel a list of tasks (C#)
