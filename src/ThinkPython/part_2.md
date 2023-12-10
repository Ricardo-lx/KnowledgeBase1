      |
|                       |     sphere with       |                       |
|                       |     radius 5?*        |                       |
|                       | 2.  *Suppose the      |                       |
|                       |     cover price of a  |                       |
|                       |     book is \$24.95,  |                       |
|                       |     but bookstores    |                       |
|                       |     get a 40%         |                       |
|                       |     discount.         |                       |
|                       |     Shipping costs    |                       |
|                       |     \$3 for the first |                       |
|                       |     copy and 75 cents |                       |
|                       |     for each          |                       |
|                       |     additional copy.  |                       |
|                       |     What is the total |                       |
|                       |     wholesale cost    |                       |
|                       |     for 60 copies?*   |                       |
|                       | 3.  *If I leave my    |                       |
|                       |     house at 6:52 am  |                       |
|                       |     and run 1 mile at |                       |
|                       |     an easy pace      |                       |
|                       |     (8:15 per mile),  |                       |
|                       |     then 3 miles at   |                       |
|                       |     tempo (7:12 per   |                       |
|                       |     mile) and 1 mile  |                       |
|                       |     at easy pace      |                       |
|                       |     again, what time  |                       |
|                       |     do I get home for |                       |
|                       |     breakfast?*       |                       |
|                       |                       |                       |
|                       | []{#hevea_default145} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2002.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2004.html)
---
generator: hevea 2.32
title: Functions
---

[![Previous](back.png)](thinkpython2003.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2005.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 3  Functi   | to support my books,  |
|                       | ons {#sec26 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | []{#funcchap}         | with PayPal. Thank    |
|                       |                       | you!                  |
|                       | In the context of     |                       |
|                       | programming, a        |   -----------         |
|                       | [function]{.c010} is  | --------------------- |
|                       | a named sequence of   | --------------------- |
|                       | statements that       | --------------------- |
|                       | performs a            | --------------------- |
|                       | computation. When you |   Pay what you want:  |
|                       | define a function,    |   Small \$1           |
|                       | you specify the name  | .00 USD Medium \$5.00 |
|                       | and the sequence of   |  USD Large \$10.00 US |
|                       | statements. Later,    | D X-Large \$20.00 USD |
|                       | you can "call" the    |  XX-Large \$50.00 USD |
|                       | function by name.     |   -----------         |
|                       | []{#hevea_default146} | --------------------- |
|                       |                       | --------------------- |
|                       | ## 3.1  Function ca   | --------------------- |
|                       | lls {#sec27 .section} | --------------------- |
|                       |                       |                       |
|                       | []{#functionchap}     | ![](                  |
|                       | []{#hevea_default147} | https://www.paypalobj |
|                       |                       | ects.com/en_US/i/scr/ |
|                       | We have already seen  | pixel.gif){border="0" |
|                       | one example of a      | width="1" height="1"} |
|                       | [function             |                       |
|                       | call]{.c010}:         | ####                  |
|                       |                       | Are you using one of  |
|                       | ``` verbatim          | our books in a class? |
|                       | >>> type(42)          |                       |
|                       | <class 'int'>         | We\'d like to know    |
|                       | ```                   | about it. Please      |
|                       |                       | consider filling out  |
|                       | The name of the       | [this short           |
|                       | function is           | survey](http://s      |
|                       | [type]{.c004}. The    | preadsheets.google.co |
|                       | expression in         | m/viewform?formkey=dC |
|                       | parentheses is called | 0tNUZkMjBEdXVoRGljNm9 |
|                       | the [argument]{.c010} | FRmlTMHc6MA){onclick= |
|                       | of the function. The  | "javascript: pageTrac |
|                       | result, for this      | ker._trackPageview('/ |
|                       | function, is the type | outbound/survey');"}. |
|                       | of the argument.      |                       |
|                       | []{#hevea_default148} | \                     |
|                       |                       |                       |
|                       | It is common to say   | [Think                |
|                       | that a function       | DSP](http             |
|                       | "takes" an argument   | ://www.amazon.com/gp/ |
|                       | and "returns" a       | product/1491938455/re |
|                       | result. The result is | f=as_li_tl?ie=UTF8&ca |
|                       | also called the       | mp=1789&creative=9325 |
|                       | [return               | &creativeASIN=1491938 |
|                       | value]{.c010}.        | 455&linkCode=as2&tag= |
|                       | []{#hevea_default149} | greenteapre01-20&link |
|                       | []{#hevea_default150} | Id=2JJH4SWCAVVYSQHO){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | Python provides       | tp://ir-na.amazon-ads |
|                       | functions that        | ystem.com/e/ir?t=gree |
|                       | convert values from   | nteapre01-20&l=as2&o= |
|                       | one type to another.  | 1&a=1491938455){.c003 |
|                       | The [int]{.c004}      | width="1" height="1"  |
|                       | function takes any    | border="0"}           |
|                       | value and converts it |                       |
|                       | to an integer, if it  | [                     |
|                       | can, or complains     | ![](http://ws-na.amaz |
|                       | otherwise:            | on-adsystem.com/widge |
|                       | []{#hevea_default151} | ts/q?_encoding=UTF8&A |
|                       | []{#hevea_default152} | SIN=1491938455&Format |
|                       | []{#hevea_default153} | =_SL160_&ID=AsinImage |
|                       | []{#hevea_default154} | &MarketPlace=US&Servi |
|                       |                       | ceVersion=20070822&WS |
|                       | ``` verbatim          | =1&tag=greenteapre01- |
|                       | >>> int('32')         | 20){border="0"}](http |
|                       | 32                    | ://www.amazon.com/gp/ |
|                       | >>> int('Hello')      | product/1491938455/re |
|                       | Va                    | f=as_li_tl?ie=UTF8&ca |
|                       | lueError: invalid lit | mp=1789&creative=9325 |
|                       | eral for int(): Hello | &creativeASIN=1491938 |
|                       | ```                   | 455&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | [int]{.c004} can      | Id=CTV7PDT7E5EGGJUM){ |
|                       | convert               | rel="nofollow"}![](ht |
|                       | floating-point values | tp://ir-na.amazon-ads |
|                       | to integers, but it   | ystem.com/e/ir?t=gree |
|                       | doesn't round off; it | nteapre01-20&l=as2&o= |
|                       | chops off the         | 1&a=1491938455){.c003 |
|                       | fraction part:        | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | ``` verbatim          |                       |
|                       | >>> int(3.99999)      | [Think                |
|                       | 3                     | Java](http            |
|                       | >>> int(-2.3)         | ://www.amazon.com/gp/ |
|                       | -2                    | product/1491929561/re |
|                       | ```                   | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | [float]{.c004}        | &creativeASIN=1491929 |
|                       | converts integers and | 561&linkCode=as2&tag= |
|                       | strings to            | greenteapre01-20&link |
|                       | floating-point        | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | numbers:              | rel="nofollow"}![](ht |
|                       | []{#hevea_default155} | tp://ir-na.amazon-ads |
|                       | []{#hevea_default156} | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1491929561){.c003 |
|                       | >>> float(32)         | width="1" height="1"  |
|                       | 32.0                  | border="0"}           |
|                       | >>> float('3.14159')  |                       |
|                       | 3.14159               | [                     |
|                       | ```                   | ![](http://ws-na.amaz |
|                       |                       | on-adsystem.com/widge |
|                       | Finally, [str]{.c004} | ts/q?_encoding=UTF8&A |
|                       | converts its argument | SIN=1491929561&Format |
|                       | to a string:          | =_SL160_&ID=AsinImage |
|                       | []{#hevea_default157} | &MarketPlace=US&Servi |
|                       | []{#hevea_default158} | ceVersion=20070822&WS |
|                       |                       | =1&tag=greenteapre01- |
|                       | ``` verbatim          | 20){border="0"}](http |
|                       | >>> str(32)           | ://www.amazon.com/gp/ |
|                       | '32'                  | product/1491929561/re |
|                       | >>> str(3.14159)      | f=as_li_tl?ie=UTF8&ca |
|                       | '3.14159'             | mp=1789&creative=9325 |
|                       | ```                   | &creativeASIN=1491929 |
|                       |                       | 561&linkCode=as2&tag= |
|                       | ## 3.2  Math functi   | greenteapre01-20&link |
|                       | ons {#sec28 .section} | Id=PT77ANWARUNNU3UK){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | []{#hevea_default159} | tp://ir-na.amazon-ads |
|                       | []{#hevea_default160} | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | Python has a math     | 1&a=1491929561){.c003 |
|                       | module that provides  | width="1" height="1"  |
|                       | most of the familiar  | border="0"}           |
|                       | mathematical          |                       |
|                       | functions. A          | [Think                |
|                       | [module]{.c010} is a  | Bay                   |
|                       | file that contains a  | es](http://www.amazon |
|                       | collection of related | .com/gp/product/14493 |
|                       | functions.            | 70780/ref=as_li_qf_sp |
|                       | []{#hevea_default161} | _asin_tl?ie=UTF8&camp |
|                       | []{#hevea_default162} | =1789&creative=9325&c |
|                       |                       | reativeASIN=144937078 |
|                       | Before we can use the | 0&linkCode=as2&tag=gr |
|                       | functions in a        | eenteapre01-20)![](ht |
|                       | module, we have to    | tp://ir-na.amazon-ads |
|                       | import it with an     | ystem.com/e/ir?t=gree |
|                       | [import               | nteapre01-20&l=as2&o= |
|                       | statement]{.c010}:    | 1&a=1449370780){.c003 |
|                       |                       | width="1" height="1"  |
|                       | ``` verbatim          | border="0"}           |
|                       | >>> import math       |                       |
|                       | ```                   | [![](http://ws        |
|                       |                       | -na.amazon-adsystem.c |
|                       | This statement        | om/widgets/q?_encodin |
|                       | creates a [module     | g=UTF8&ASIN=144937078 |
|                       | object]{.c010} named  | 0&Format=_SL160_&ID=A |
|                       | math. If you display  | sinImage&MarketPlace= |
|                       | the module object,    | US&ServiceVersion=200 |
|                       | you get some          | 70822&WS=1&tag=greent |
|                       | information about it: | eapre01-20){border="0 |
|                       |                       | "}](http://www.amazon |
|                       | ``` verbatim          | .com/gp/product/14493 |
|                       | >>> math              | 70780/ref=as_li_qf_sp |
|                       | <modu                 | _asin_il?ie=UTF8&camp |
|                       | le 'math' (built-in)> | =1789&creative=9325&c |
|                       | ```                   | reativeASIN=144937078 |
|                       |                       | 0&linkCode=as2&tag=gr |
|                       | The module object     | eenteapre01-20)![](ht |
|                       | contains the          | tp://ir-na.amazon-ads |
|                       | functions and         | ystem.com/e/ir?t=gree |
|                       | variables defined in  | nteapre01-20&l=as2&o= |
|                       | the module. To access | 1&a=1449370780){.c003 |
|                       | one of the functions, | width="1" height="1"  |
|                       | you have to specify   | border="0"}           |
|                       | the name of the       |                       |
|                       | module and the name   | [Think Python         |
|                       | of the function,      | 2e](http              |
|                       | separated by a dot    | ://www.amazon.com/gp/ |
|                       | (also known as a      | product/1491939362/re |
|                       | period). This format  | f=as_li_tl?ie=UTF8&ca |
|                       | is called [dot        | mp=1789&creative=9325 |
|                       | notation]{.c010}.     | &creativeASIN=1491939 |
|                       | []{#hevea_default163} | 362&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | ``` verbatim          | Id=FJKSQ3IHEMY2F2VA){ |
|                       | >>> ratio = signa     | rel="nofollow"}![](ht |
|                       | l_power / noise_power | tp://ir-na.amazon-ads |
|                       | >>> decibels = 1      | ystem.com/e/ir?t=gree |
|                       | 0 * math.log10(ratio) | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | >>> radians = 0.7     | width="1" height="1"  |
|                       | >>> heigh             | border="0"}           |
|                       | t = math.sin(radians) |                       |
|                       | ```                   | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | The first example     | on-adsystem.com/widge |
|                       | uses `math.log10` to  | ts/q?_encoding=UTF8&A |
|                       | compute a             | SIN=1491939362&Format |
|                       | signal-to-noise ratio | =_SL160_&ID=AsinImage |
|                       | in decibels (assuming | &MarketPlace=US&Servi |
|                       | that `signal_power`   | ceVersion=20070822&WS |
|                       | and `noise_power` are | =1&tag=greenteapre01- |
|                       | defined). The math    | 20){border="0"}](http |
|                       | module also provides  | ://www.amazon.com/gp/ |
|                       | [log]{.c004}, which   | product/1491939362/re |
|                       | computes logarithms   | f=as_li_tl?ie=UTF8&ca |
|                       | base [e]{.c004}.      | mp=1789&creative=9325 |
|                       | []{#hevea_default164} | &creativeASIN=1491939 |
|                       | []{#hevea_default165} | 362&linkCode=as2&tag= |
|                       | []{#hevea_default166} | greenteapre01-20&link |
|                       | []{#hevea_default167} | Id=ZZ454DLQ3IXDHNHX){ |
|                       | []{#hevea_default168} | rel="nofollow"}![](ht |
|                       | []{#hevea_default169} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | The second example    | nteapre01-20&l=as2&o= |
|                       | finds the sine of     | 1&a=1491939362){.c003 |
|                       | [radians]{.c004}. The | width="1" height="1"  |
|                       | variable name         | border="0"}           |
|                       | [radians]{.c004} is a |                       |
|                       | hint that             | [Think Stats          |
|                       | [sin]{.c004} and the  | 2e](http://ww         |
|                       | other trigonometric   | w.amazon.com/gp/produ |
|                       | functions             | ct/1491907339/ref=as_ |
|                       | ([cos]{.c004},        | li_tl?ie=UTF8&camp=17 |
|                       | [tan]{.c004}, etc.)   | 89&creative=9325&crea |
|                       | take arguments in     | tiveASIN=1491907339&l |
|                       | radians. To convert   | inkCode=as2&tag=green |
|                       | from degrees to       | teapre01-20&linkId=O7 |
|                       | radians, divide by    | WYM6H6YBYUFNWU)![](ht |
|                       | 180 and multiply by   | tp://ir-na.amazon-ads |
|                       | π:                    | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1491907339){.c003 |
|                       | >>> degrees = 45      | width="1" height="1"  |
|                       | >>> radians = degr    | border="0"}           |
|                       | ees / 180.0 * math.pi |                       |
|                       | >>> math.sin(radians) | [![](h                |
|                       | 0.707106781187        | ttp://ws-na.amazon-ad |
|                       | ```                   | system.com/widgets/q? |
|                       |                       | _encoding=UTF8&ASIN=1 |
|                       | The expression        | 491907339&Format=_SL1 |
|                       | [math.pi]{.c004} gets | 60_&ID=AsinImage&Mark |
|                       | the variable          | etPlace=US&ServiceVer |
|                       | [pi]{.c004} from the  | sion=20070822&WS=1&ta |
|                       | math module. Its      | g=greenteapre01-20){b |
|                       | value is a            | order="0"}](http://ww |
|                       | floating-point        | w.amazon.com/gp/produ |
|                       | approximation of π,   | ct/1491907339/ref=as_ |
|                       | accurate to about 15  | li_tl?ie=UTF8&camp=17 |
|                       | digits.               | 89&creative=9325&crea |
|                       | []{#hevea_default170} | tiveASIN=1491907339&l |
|                       |                       | inkCode=as2&tag=green |
|                       | If you know           | teapre01-20&linkId=JV |
|                       | trigonometry, you can | SYKQHYSUIEYRHL)![](ht |
|                       | check the previous    | tp://ir-na.amazon-ads |
|                       | result by comparing   | ystem.com/e/ir?t=gree |
|                       | it to the square root | nteapre01-20&l=as2&o= |
|                       | of two, divided by    | 1&a=1491907339){.c003 |
|                       | two:                  | width="1" height="1"  |
|                       | []{#hevea_default171} | border="0"}           |
|                       | []{#hevea_default172} |                       |
|                       |                       | [Think                |
|                       | ``` verbatim          | Complexity](http      |
|                       | >                     | ://www.amazon.com/gp/ |
|                       | >> math.sqrt(2) / 2.0 | product/1449314635/re |
|                       | 0.707106781187        | f=as_li_tf_tl?ie=UTF8 |
|                       | ```                   | &tag=greenteapre01-20 |
|                       |                       | &linkCode=as2&camp=17 |
|                       | ## 3.3  Composit      | 89&creative=9325&crea |
|                       | ion {#sec29 .section} | tiveASIN=1449314635)! |
|                       |                       | [](http://www.assoc-a |
|                       | []{#hevea_default173} | mazon.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | So far, we have       | 1&a=1449314635){.c003 |
|                       | looked at the         | width="1" height="1"  |
|                       | elements of a         | border="0"}           |
|                       | program---variables,  |                       |
|                       | expressions, and      | [                     |
|                       | statements---in       | ![](http://ws-na.amaz |
|                       | isolation, without    | on-adsystem.com/widge |
|                       | talking about how to  | ts/q?_encoding=UTF8&A |
|                       | combine them.         | SIN=1449314635&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | One of the most       | &MarketPlace=US&Servi |
|                       | useful features of    | ceVersion=20070822&WS |
|                       | programming languages | =1&tag=greenteapre01- |
|                       | is their ability to   | 20){border="0"}](http |
|                       | take small building   | ://www.amazon.com/gp/ |
|                       | blocks and            | product/1449314635/re |
|                       | [compose]{.c010}      | f=as_li_tf_il?ie=UTF8 |
|                       | them. For example,    | &camp=1789&creative=9 |
|                       | the argument of a     | 325&creativeASIN=1449 |
|                       | function can be any   | 314635&linkCode=as2&t |
|                       | kind of expression,   | ag=greenteapre01-20)! |
|                       | including arithmetic  | [](http://www.assoc-a |
|                       | operators:            | mazon.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1449314635){.c003 |
|                       | x                     | width="1" height="1"  |
|                       |  = math.sin(degrees / | border="0"}           |
|                       |  360.0 * 2 * math.pi) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And even function     |                       |
|                       | calls:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | x = ma                |                       |
|                       | th.exp(math.log(x+1)) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Almost anywhere you   |                       |
|                       | can put a value, you  |                       |
|                       | can put an arbitrary  |                       |
|                       | expression, with one  |                       |
|                       | exception: the left   |                       |
|                       | side of an assignment |                       |
|                       | statement has to be a |                       |
|                       | variable name. Any    |                       |
|                       | other expression on   |                       |
|                       | the left side is a    |                       |
|                       | syntax error (we will |                       |
|                       | see exceptions to     |                       |
|                       | this rule later).     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> mi                |                       |
|                       | nutes = hours * 60    |                       |
|                       |               # right |                       |
|                       | >>> hou               |                       |
|                       | rs * 60 = minutes     |                       |
|                       |              # wrong! |                       |
|                       | SyntaxError: can      |                       |
|                       | 't assign to operator |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | []{#hevea_default174} |                       |
|                       | []{#hevea_default175} |                       |
|                       |                       |                       |
|                       | ## 3                  |                       |
|                       | .4  Adding new functi |                       |
|                       | ons {#sec30 .section} |                       |
|                       |                       |                       |
|                       | So far, we have only  |                       |
|                       | been using the        |                       |
|                       | functions that come   |                       |
|                       | with Python, but it   |                       |
|                       | is also possible to   |                       |
|                       | add new functions. A  |                       |
|                       | [function             |                       |
|                       | definition]{.c010}    |                       |
|                       | specifies the name of |                       |
|                       | a new function and    |                       |
|                       | the sequence of       |                       |
|                       | statements that run   |                       |
|                       | when the function is  |                       |
|                       | called.               |                       |
|                       | []{#hevea_default176} |                       |
|                       | []{#hevea_default177} |                       |
|                       | []{#hevea_default178} |                       |
|                       |                       |                       |
|                       | Here is an example:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_lyrics():   |                       |
|                       |                       |                       |
|                       |   print("I'm a lumber |                       |
|                       | jack, and I'm okay.") |                       |
|                       |     prin              |                       |
|                       | t("I sleep all night  |                       |
|                       | and I work all day.") |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [def]{.c004} is a     |                       |
|                       | keyword that          |                       |
|                       | indicates that this   |                       |
|                       | is a function         |                       |
|                       | definition. The name  |                       |
|                       | of the function is    |                       |
|                       | `print_lyrics`. The   |                       |
|                       | rules for function    |                       |
|                       | names are the same as |                       |
|                       | for variable names:   |                       |
|                       | letters, numbers and  |                       |
|                       | underscore are legal, |                       |
|                       | but the first         |                       |
|                       | character can't be a  |                       |
|                       | number. You can't use |                       |
|                       | a keyword as the name |                       |
|                       | of a function, and    |                       |
|                       | you should avoid      |                       |
|                       | having a variable and |                       |
|                       | a function with the   |                       |
|                       | same name.            |                       |
|                       | []{#hevea_default179} |                       |
|                       | []{#hevea_default180} |                       |
|                       | []{#hevea_default181} |                       |
|                       |                       |                       |
|                       | The empty parentheses |                       |
|                       | after the name        |                       |
|                       | indicate that this    |                       |
|                       | function doesn't take |                       |
|                       | any arguments.        |                       |
|                       | []{#hevea_default182} |                       |
|                       | []{#hevea_default183} |                       |
|                       | []{#hevea_default184} |                       |
|                       | []{#hevea_default185} |                       |
|                       | []{#hevea_default186} |                       |
|                       |                       |                       |
|                       | The first line of the |                       |
|                       | function definition   |                       |
|                       | is called the         |                       |
|                       | [header]{.c010}; the  |                       |
|                       | rest is called the    |                       |
|                       | [body]{.c010}. The    |                       |
|                       | header has to end     |                       |
|                       | with a colon and the  |                       |
|                       | body has to be        |                       |
|                       | indented. By          |                       |
|                       | convention,           |                       |
|                       | indentation is always |                       |
|                       | four spaces. The body |                       |
|                       | can contain any       |                       |
|                       | number of statements. |                       |
|                       |                       |                       |
|                       | The strings in the    |                       |
|                       | print statements are  |                       |
|                       | enclosed in double    |                       |
|                       | quotes. Single quotes |                       |
|                       | and double quotes do  |                       |
|                       | the same thing; most  |                       |
|                       | people use single     |                       |
|                       | quotes except in      |                       |
|                       | cases like this where |                       |
|                       | a single quote (which |                       |
|                       | is also an            |                       |
|                       | apostrophe) appears   |                       |
|                       | in the string.        |                       |
|                       |                       |                       |
|                       | All quotation marks   |                       |
|                       | (single and double)   |                       |
|                       | must be "straight     |                       |
|                       | quotes", usually      |                       |
|                       | located next to Enter |                       |
|                       | on the keyboard.      |                       |
|                       | "Curly quotes", like  |                       |
|                       | the ones in this      |                       |
|                       | sentence, are not     |                       |
|                       | legal in Python.      |                       |
|                       |                       |                       |
|                       | If you type a         |                       |
|                       | function definition   |                       |
|                       | in interactive mode,  |                       |
|                       | the interpreter       |                       |
|                       | prints dots           |                       |
|                       | ([\...]{.c004}) to    |                       |
|                       | let you know that the |                       |
|                       | definition isn't      |                       |
|                       | complete:             |                       |
|                       | []{#hevea_default187} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > def print_lyrics(): |                       |
|                       | ...                   |                       |
|                       |   print("I'm a lumber |                       |
|                       | jack, and I'm okay.") |                       |
|                       | ...     prin          |                       |
|                       | t("I sleep all night  |                       |
|                       | and I work all day.") |                       |
|                       | ...                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | To end the function,  |                       |
|                       | you have to enter an  |                       |
|                       | empty line.           |                       |
|                       |                       |                       |
|                       | Defining a function   |                       |
|                       | creates a [function   |                       |
|                       | object]{.c010}, which |                       |
|                       | has type `function`:  |                       |
|                       | []{#hevea_default188} |                       |
|                       | []{#hevea_default189} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > print(print_lyrics) |                       |
|                       | <function print_      |                       |
|                       | lyrics at 0xb7e99e9c> |                       |
|                       | >                     |                       |
|                       | >> type(print_lyrics) |                       |
|                       | <class 'function'>    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The syntax for        |                       |
|                       | calling the new       |                       |
|                       | function is the same  |                       |
|                       | as for built-in       |                       |
|                       | functions:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> print_lyrics()    |                       |
|                       | I'm a lumb            |                       |
|                       | erjack, and I'm okay. |                       |
|                       | I sleep all nigh      |                       |
|                       | t and I work all day. |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Once you have defined |                       |
|                       | a function, you can   |                       |
|                       | use it inside another |                       |
|                       | function. For         |                       |
|                       | example, to repeat    |                       |
|                       | the previous refrain, |                       |
|                       | we could write a      |                       |
|                       | function called       |                       |
|                       | `repeat_lyrics`:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def repeat_lyrics():  |                       |
|                       |     print_lyrics()    |                       |
|                       |     print_lyrics()    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And then call         |                       |
|                       | `repeat_lyrics`:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> repeat_lyrics()   |                       |
|                       | I'm a lumb            |                       |
|                       | erjack, and I'm okay. |                       |
|                       | I sleep all nigh      |                       |
|                       | t and I work all day. |                       |
|                       | I'm a lumb            |                       |
|                       | erjack, and I'm okay. |                       |
|                       | I sleep all nigh      |                       |
|                       | t and I work all day. |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But that's not really |                       |
|                       | how the song goes.    |                       |
|                       |                       |                       |
|                       | ## 3                  |                       |
|                       | .5  Definitions and u |                       |
|                       | ses {#sec31 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default190} |                       |
|                       |                       |                       |
|                       | Pulling together the  |                       |
|                       | code fragments from   |                       |
|                       | the previous section, |                       |
|                       | the whole program     |                       |
|                       | looks like this:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_lyrics():   |                       |
|                       |                       |                       |
|                       |   print("I'm a lumber |                       |
|                       | jack, and I'm okay.") |                       |
|                       |     prin              |                       |
|                       | t("I sleep all night  |                       |
|                       | and I work all day.") |                       |
|                       |                       |                       |
|                       | def repeat_lyrics():  |                       |
|                       |     print_lyrics()    |                       |
|                       |     print_lyrics()    |                       |
|                       |                       |                       |
|                       | repeat_lyrics()       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This program contains |                       |
|                       | two function          |                       |
|                       | definitions:          |                       |
|                       | `print_lyrics` and    |                       |
|                       | `repeat_lyrics`.      |                       |
|                       | Function definitions  |                       |
|                       | get executed just     |                       |
|                       | like other            |                       |
|                       | statements, but the   |                       |
|                       | effect is to create   |                       |
|                       | function objects. The |                       |
|                       | statements inside the |                       |
|                       | function do not run   |                       |
|                       | until the function is |                       |
|                       | called, and the       |                       |
|                       | function definition   |                       |
|                       | generates no output.  |                       |
|                       | []{#hevea_default191} |                       |
|                       |                       |                       |
|                       | As you might expect,  |                       |
|                       | you have to create a  |                       |
|                       | function before you   |                       |
|                       | can run it. In other  |                       |
|                       | words, the function   |                       |
|                       | definition has to run |                       |
|                       | before the function   |                       |
|                       | gets called.          |                       |
|                       |                       |                       |
|                       | As an exercise, move  |                       |
|                       | the last line of this |                       |
|                       | program to the top,   |                       |
|                       | so the function call  |                       |
|                       | appears before the    |                       |
|                       | definitions. Run the  |                       |
|                       | program and see what  |                       |
|                       | error message you     |                       |
|                       | get.                  |                       |
|                       |                       |                       |
|                       | Now move the function |                       |
|                       | call back to the      |                       |
|                       | bottom and move the   |                       |
|                       | definition of         |                       |
|                       | `print_lyrics` after  |                       |
|                       | the definition of     |                       |
|                       | `repeat_lyrics`. What |                       |
|                       | happens when you run  |                       |
|                       | this program?         |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 3.6  Flow of execut |                       |
|                       | ion {#sec32 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default192} |                       |
|                       |                       |                       |
|                       | To ensure that a      |                       |
|                       | function is defined   |                       |
|                       | before its first use, |                       |
|                       | you have to know the  |                       |
|                       | order statements run  |                       |
|                       | in, which is called   |                       |
|                       | the [flow of          |                       |
|                       | execution]{.c010}.    |                       |
|                       |                       |                       |
|                       | Execution always      |                       |
|                       | begins at the first   |                       |
|                       | statement of the      |                       |
|                       | program. Statements   |                       |
|                       | are run one at a      |                       |
|                       | time, in order from   |                       |
|                       | top to bottom.        |                       |
|                       |                       |                       |
|                       | Function definitions  |                       |
|                       | do not alter the flow |                       |
|                       | of execution of the   |                       |
|                       | program, but remember |                       |
|                       | that statements       |                       |
|                       | inside the function   |                       |
|                       | don't run until the   |                       |
|                       | function is called.   |                       |
|                       |                       |                       |
|                       | A function call is    |                       |
|                       | like a detour in the  |                       |
|                       | flow of execution.    |                       |
|                       | Instead of going to   |                       |
|                       | the next statement,   |                       |
|                       | the flow jumps to the |                       |
|                       | body of the function, |                       |
|                       | runs the statements   |                       |
|                       | there, and then comes |                       |
|                       | back to pick up where |                       |
|                       | it left off.          |                       |
|                       |                       |                       |
|                       | That sounds simple    |                       |
|                       | enough, until you     |                       |
|                       | remember that one     |                       |
|                       | function can call     |                       |
|                       | another. While in the |                       |
|                       | middle of one         |                       |
|                       | function, the program |                       |
|                       | might have to run the |                       |
|                       | statements in another |                       |
|                       | function. Then, while |                       |
|                       | running that new      |                       |
|                       | function, the program |                       |
|                       | might have to run yet |                       |
|                       | another function!     |                       |
|                       |                       |                       |
|                       | Fortunately, Python   |                       |
|                       | is good at keeping    |                       |
|                       | track of where it is, |                       |
|                       | so each time a        |                       |
|                       | function completes,   |                       |
|                       | the program picks up  |                       |
|                       | where it left off in  |                       |
|                       | the function that     |                       |
|                       | called it. When it    |                       |
|                       | gets to the end of    |                       |
|                       | the program, it       |                       |
|                       | terminates.           |                       |
|                       |                       |                       |
|                       | In summary, when you  |                       |
|                       | read a program, you   |                       |
|                       | don't always want to  |                       |
|                       | read from top to      |                       |
|                       | bottom. Sometimes it  |                       |
|                       | makes more sense if   |                       |
|                       | you follow the flow   |                       |
|                       | of execution.         |                       |
|                       |                       |                       |
|                       | ## 3.7                |                       |
|                       | Parameters and argume |                       |
|                       | nts {#sec33 .section} |                       |
|                       |                       |                       |
|                       | []{#parameters}       |                       |
|                       | []{#hevea_default193} |                       |
|                       | []{#hevea_default194} |                       |
|                       | []{#hevea_default195} |                       |
|                       | []{#hevea_default196} |                       |
|                       |                       |                       |
|                       | Some of the functions |                       |
|                       | we have seen require  |                       |
|                       | arguments. For        |                       |
|                       | example, when you     |                       |
|                       | call                  |                       |
|                       | [math.sin]{.c004} you |                       |
|                       | pass a number as an   |                       |
|                       | argument. Some        |                       |
|                       | functions take more   |                       |
|                       | than one argument:    |                       |
|                       | [math.pow]{.c004}     |                       |
|                       | takes two, the base   |                       |
|                       | and the exponent.     |                       |
|                       |                       |                       |
|                       | Inside the function,  |                       |
|                       | the arguments are     |                       |
|                       | assigned to variables |                       |
|                       | called                |                       |
|                       | [parameters]{.c010}.  |                       |
|                       | Here is a definition  |                       |
|                       | for a function that   |                       |
|                       | takes an argument:    |                       |
|                       | []{#hevea_default197} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | de                    |                       |
|                       | f print_twice(bruce): |                       |
|                       |     print(bruce)      |                       |
|                       |     print(bruce)      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This function assigns |                       |
|                       | the argument to a     |                       |
|                       | parameter named       |                       |
|                       | [bruce]{.c004}. When  |                       |
|                       | the function is       |                       |
|                       | called, it prints the |                       |
|                       | value of the          |                       |
|                       | parameter (whatever   |                       |
|                       | it is) twice.         |                       |
|                       |                       |                       |
|                       | This function works   |                       |
|                       | with any value that   |                       |
|                       | can be printed.       |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > print_twice('Spam') |                       |
|                       | Spam                  |                       |
|                       | Spam                  |                       |
|                       | >>> print_twice(42)   |                       |
|                       | 42                    |                       |
|                       | 42                    |                       |
|                       | >>>                   |                       |
|                       |  print_twice(math.pi) |                       |
|                       | 3.14159265359         |                       |
|                       | 3.14159265359         |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The same rules of     |                       |
|                       | composition that      |                       |
|                       | apply to built-in     |                       |
|                       | functions also apply  |                       |
|                       | to programmer-defined |                       |
|                       | functions, so we can  |                       |
|                       | use any kind of       |                       |
|                       | expression as an      |                       |
|                       | argument for          |                       |
|                       | `print_twice`:        |                       |
|                       | []{#hevea_default198} |                       |
|                       | []{#hevea_default199} |                       |
|                       | []{#hevea_default200} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> p                 |                       |
|                       | rint_twice('Spam '*4) |                       |
|                       | Spam Spam Spam Spam   |                       |
|                       | Spam Spam Spam Spam   |                       |
|                       | >>> print_twi         |                       |
|                       | ce(math.cos(math.pi)) |                       |
|                       | -1.0                  |                       |
|                       | -1.0                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The argument is       |                       |
|                       | evaluated before the  |                       |
|                       | function is called,   |                       |
|                       | so in the examples    |                       |
|                       | the expressions       |                       |
|                       | `'Spam '*4` and       |                       |
|                       | [math                 |                       |
|                       | .cos(math.pi)]{.c004} |                       |
|                       | are only evaluated    |                       |
|                       | once.                 |                       |
|                       | []{#hevea_default201} |                       |
|                       |                       |                       |
|                       | You can also use a    |                       |
|                       | variable as an        |                       |
|                       | argument:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> michael = 'E      |                       |
|                       | ric, the half a bee.' |                       |
|                       | >>>                   |                       |
|                       |  print_twice(michael) |                       |
|                       | Eric, the half a bee. |                       |
|                       | Eric, the half a bee. |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The name of the       |                       |
|                       | variable we pass as   |                       |
|                       | an argument           |                       |
|                       | ([michael]{.c004})    |                       |
|                       | has nothing to do     |                       |
|                       | with the name of the  |                       |
|                       | parameter             |                       |
|                       | ([bruce]{.c004}). It  |                       |
|                       | doesn't matter what   |                       |
|                       | the value was called  |                       |
|                       | back home (in the     |                       |
|                       | caller); here in      |                       |
|                       | `print_twice`, we     |                       |
|                       | call everybody        |                       |
|                       | [bruce]{.c004}.       |                       |
|                       |                       |                       |
|                       | ## 3.8  Variables     |                       |
|                       | and parameters are lo |                       |
|                       | cal {#sec34 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default202} |                       |
|                       | []{#hevea_default203} |                       |
|                       |                       |                       |
|                       | When you create a     |                       |
|                       | variable inside a     |                       |
|                       | function, it is       |                       |
|                       | [local]{.c010}, which |                       |
|                       | means that it only    |                       |
|                       | exists inside the     |                       |
|                       | function. For         |                       |
|                       | example:              |                       |
|                       | []{#hevea_default204} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def cat               |                       |
|                       | _twice(part1, part2): |                       |
|                       |                       |                       |
|                       |   cat = part1 + part2 |                       |
|                       |     print_twice(cat)  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This function takes   |                       |
|                       | two arguments,        |                       |
|                       | concatenates them,    |                       |
|                       | and prints the result |                       |
|                       | twice. Here is an     |                       |
|                       | example that uses it: |                       |
|                       | []{#hevea_default205} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> l                 |                       |
|                       | ine1 = 'Bing tiddle ' |                       |
|                       | >>> l                 |                       |
|                       | ine2 = 'tiddle bang.' |                       |
|                       | >>> ca                |                       |
|                       | t_twice(line1, line2) |                       |
|                       | Bin                   |                       |
|                       | g tiddle tiddle bang. |                       |
|                       | Bin                   |                       |
|                       | g tiddle tiddle bang. |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | When `cat_twice`      |                       |
|                       | terminates, the       |                       |
|                       | variable [cat]{.c004} |                       |
|                       | is destroyed. If we   |                       |
|                       | try to print it, we   |                       |
|                       | get an exception:     |                       |
|                       | []{#hevea_default206} |                       |
|                       | []{#hevea_default207} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> print(cat)        |                       |
|                       | NameError: name       |                       |
|                       |  'cat' is not defined |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Parameters are also   |                       |
|                       | local. For example,   |                       |
|                       | outside               |                       |
|                       | `print_twice`, there  |                       |
|                       | is no such thing as   |                       |
|                       | [bruce]{.c004}.       |                       |
|                       | []{#hevea_default208} |                       |
|                       |                       |                       |
|                       | ## 3.9  Stack diagr   |                       |
|                       | ams {#sec35 .section} |                       |
|                       |                       |                       |
|                       | []{#stackdiagram}     |                       |
|                       | []{#hevea_default209} |                       |
|                       | []{#hevea_default210} |                       |
|                       | []{#hevea_default211} |                       |
|                       |                       |                       |
|                       | To keep track of      |                       |
|                       | which variables can   |                       |
|                       | be used where, it is  |                       |
|                       | sometimes useful to   |                       |
|                       | draw a [stack         |                       |
|                       | diagram]{.c010}. Like |                       |
|                       | state diagrams, stack |                       |
|                       | diagrams show the     |                       |
|                       | value of each         |                       |
|                       | variable, but they    |                       |
|                       | also show the         |                       |
|                       | function each         |                       |
|                       | variable belongs to.  |                       |
|                       | []{#hevea_default212} |                       |
|                       | []{#hevea_default213} |                       |
|                       |                       |                       |
|                       | Each function is      |                       |
|                       | represented by a      |                       |
|                       | [frame]{.c010}. A     |                       |
|                       | frame is a box with   |                       |
|                       | the name of a         |                       |
|                       | function beside it    |                       |
|                       | and the parameters    |                       |
|                       | and variables of the  |                       |
|                       | function inside it.   |                       |
|                       | The stack diagram for |                       |
|                       | the previous example  |                       |
|                       | is shown in           |                       |
|                       | Figu                  |                       |
|                       | re [3.1](#fig.stack). |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2002.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | >   Figur             |                       |
|                       | e 3.1: Stack diagram. |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.stack}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | The frames are        |                       |
|                       | arranged in a stack   |                       |
|                       | that indicates which  |                       |
|                       | function called       |                       |
|                       | which, and so on. In  |                       |
|                       | this example,         |                       |
|                       | `print_twice` was     |                       |
|                       | called by             |                       |
|                       | `cat_twice`, and      |                       |
|                       | `cat_twice` was       |                       |
|                       | called by `__main__`, |                       |
|                       | which is a special    |                       |
|                       | name for the topmost  |                       |
|                       | frame. When you       |                       |
|                       | create a variable     |                       |
|                       | outside of any        |                       |
|                       | function, it belongs  |                       |
|                       | to `__main__`.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default214} |                       |
|                       |                       |                       |
|                       | Each parameter refers |                       |
|                       | to the same value as  |                       |
|                       | its corresponding     |                       |
|                       | argument. So,         |                       |
|                       | [part1]{.c004} has    |                       |
|                       | the same value as     |                       |
|                       | [line1]{.c004},       |                       |
|                       | [part2]{.c004} has    |                       |
|                       | the same value as     |                       |
|                       | [line2]{.c004}, and   |                       |
|                       | [bruce]{.c004} has    |                       |
|                       | the same value as     |                       |
|                       | [cat]{.c004}.         |                       |
|                       |                       |                       |
|                       | If an error occurs    |                       |
|                       | during a function     |                       |
|                       | call, Python prints   |                       |
|                       | the name of the       |                       |
|                       | function, the name of |                       |
|                       | the function that     |                       |
|                       | called it, and the    |                       |
|                       | name of the function  |                       |
|                       | that called *that*,   |                       |
|                       | all the way back to   |                       |
|                       | `__main__`.           |                       |
|                       |                       |                       |
|                       | For example, if you   |                       |
|                       | try to access         |                       |
|                       | [cat]{.c004} from     |                       |
|                       | within `print_twice`, |                       |
|                       | you get a             |                       |
|                       | [NameError]{.c004}:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Traceb                |                       |
|                       | ack (innermost last): |                       |
|                       |   File "test.py",     |                       |
|                       |  line 13, in __main__ |                       |
|                       |     ca                |                       |
|                       | t_twice(line1, line2) |                       |
|                       |   File "test.py",     |                       |
|                       |  line 5, in cat_twice |                       |
|                       |     print_twice(cat)  |                       |
|                       |   File "test.py", l   |                       |
|                       | ine 9, in print_twice |                       |
|                       |     print(cat)        |                       |
|                       | NameError: name       |                       |
|                       |  'cat' is not defined |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This list of          |                       |
|                       | functions is called a |                       |
|                       | [traceback]{.c010}.   |                       |
|                       | It tells you what     |                       |
|                       | program file the      |                       |
|                       | error occurred in,    |                       |
|                       | and what line, and    |                       |
|                       | what functions were   |                       |
|                       | executing at the      |                       |
|                       | time. It also shows   |                       |
|                       | the line of code that |                       |
|                       | caused the error.     |                       |
|                       | []{#hevea_default215} |                       |
|                       |                       |                       |
|                       | The order of the      |                       |
|                       | functions in the      |                       |
|                       | traceback is the same |                       |
|                       | as the order of the   |                       |
|                       | frames in the stack   |                       |
|                       | diagram. The function |                       |
|                       | that is currently     |                       |
|                       | running is at the     |                       |
|                       | bottom.               |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 3.10  Fruitful func |                       |
|                       | tions and void functi |                       |
|                       | ons {#sec36 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default216} |                       |
|                       | []{#hevea_default217} |                       |
|                       | []{#hevea_default218} |                       |
|                       | []{#hevea_default219} |                       |
|                       |                       |                       |
|                       | Some of the functions |                       |
|                       | we have used, such as |                       |
|                       | the math functions,   |                       |
|                       | return results; for   |                       |
|                       | lack of a better      |                       |
|                       | name, I call them     |                       |
|                       | [fruitful             |                       |
|                       | functions]{.c010}.    |                       |
|                       | Other functions, like |                       |
|                       | `print_twice`,        |                       |
|                       | perform an action but |                       |
|                       | don't return a value. |                       |
|                       | They are called [void |                       |
|                       | functions]{.c010}.    |                       |
|                       |                       |                       |
|                       | When you call a       |                       |
|                       | fruitful function,    |                       |
|                       | you almost always     |                       |
|                       | want to do something  |                       |
|                       | with the result; for  |                       |
|                       | example, you might    |                       |
|                       | assign it to a        |                       |
|                       | variable or use it as |                       |
|                       | part of an            |                       |
|                       | expression:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | x = math.cos(radians) |                       |
|                       | golden = (            |                       |
|                       | math.sqrt(5) + 1) / 2 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | When you call a       |                       |
|                       | function in           |                       |
|                       | interactive mode,     |                       |
|                       | Python displays the   |                       |
|                       | result:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> math.sqrt(5)      |                       |
|                       | 2.2360679774997898    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But in a script, if   |                       |
|                       | you call a fruitful   |                       |
|                       | function all by       |                       |
|                       | itself, the return    |                       |
|                       | value is lost         |                       |
|                       | forever!              |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | math.sqrt(5)          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This script computes  |                       |
|                       | the square root of 5, |                       |
|                       | but since it doesn't  |                       |
|                       | store or display the  |                       |
|                       | result, it is not     |                       |
|                       | very useful.          |                       |
|                       | []{#hevea_default220} |                       |
|                       | []{#hevea_default221} |                       |
|                       |                       |                       |
|                       | Void functions might  |                       |
|                       | display something on  |                       |
|                       | the screen or have    |                       |
|                       | some other effect,    |                       |
|                       | but they don't have a |                       |
|                       | return value. If you  |                       |
|                       | assign the result to  |                       |
|                       | a variable, you get a |                       |
|                       | special value called  |                       |
|                       | [None]{.c004}.        |                       |
|                       | []{#hevea_default222} |                       |
|                       | []{#hevea_default223} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> result            |                       |
|                       | = print_twice('Bing') |                       |
|                       | Bing                  |                       |
|                       | Bing                  |                       |
|                       | >>> print(result)     |                       |
|                       | None                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The value             |                       |
|                       | [None]{.c004} is not  |                       |
|                       | the same as the       |                       |
|                       | string `'None'`. It   |                       |
|                       | is a special value    |                       |
|                       | that has its own      |                       |
|                       | type:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> type(None)        |                       |
|                       | <class 'NoneType'>    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The functions we have |                       |
|                       | written so far are    |                       |
|                       | all void. We will     |                       |
|                       | start writing         |                       |
|                       | fruitful functions in |                       |
|                       | a few chapters.       |                       |
|                       | []{#hevea_default224} |                       |
|                       | []{#hevea_default225} |                       |
|                       |                       |                       |
|                       | ## 3.11  Why functio  |                       |
|                       | ns? {#sec37 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default226} |                       |
|                       |                       |                       |
|                       | It may not be clear   |                       |
|                       | why it is worth the   |                       |
|                       | trouble to divide a   |                       |
|                       | program into          |                       |
|                       | functions. There are  |                       |
|                       | several reasons:      |                       |
|                       |                       |                       |
|                       | -   Creating a new    |                       |
|                       |     function gives    |                       |
|                       |     you an            |                       |
|                       |     opportunity to    |                       |
|                       |     name a group of   |                       |
|                       |     statements, which |                       |
|                       |     makes your        |                       |
|                       |     program easier to |                       |
|                       |     read and debug.   |                       |
|                       | -   Functions can     |                       |
|                       |     make a program    |                       |
|                       |     smaller by        |                       |
|                       |     eliminating       |                       |
|                       |     repetitive code.  |                       |
|                       |     Later, if you     |                       |
|                       |     make a change,    |                       |
|                       |     you only have to  |                       |
|                       |     make it in one    |                       |
|                       |     place.            |                       |
|                       | -   Dividing a long   |                       |
|                       |     program into      |                       |
|                       |     functions allows  |                       |
|                       |     you to debug the  |                       |
|                       |     parts one at a    |                       |
|                       |     time and then     |                       |
|                       |     assemble them     |                       |
|                       |     into a working    |                       |
|                       |     whole.            |                       |
|                       | -   Well-designed     |                       |
|                       |     functions are     |                       |
|                       |     often useful for  |                       |
|                       |     many programs.    |                       |
|                       |     Once you write    |                       |
|                       |     and debug one,    |                       |
|                       |     you can reuse it. |                       |
|                       |                       |                       |
|                       | ## 3.12  Debugg       |                       |
|                       | ing {#sec38 .section} |                       |
|                       |                       |                       |
|                       | One of the most       |                       |
|                       | important skills you  |                       |
|                       | will acquire is       |                       |
|                       | debugging. Although   |                       |
|                       | it can be             |                       |
|                       | frustrating,          |                       |
|                       | debugging is one of   |                       |
|                       | the most              |                       |
|                       | intellectually rich,  |                       |
|                       | challenging, and      |                       |
|                       | interesting parts of  |                       |
|                       | programming.          |                       |
|                       | []{#hevea_default227} |                       |
|                       | []{#hevea_default228} |                       |
|                       |                       |                       |
|                       | In some ways          |                       |
|                       | debugging is like     |                       |
|                       | detective work. You   |                       |
|                       | are confronted with   |                       |
|                       | clues and you have to |                       |
|                       | infer the processes   |                       |
|                       | and events that led   |                       |
|                       | to the results you    |                       |
|                       | see.                  |                       |
|                       |                       |                       |
|                       | Debugging is also     |                       |
|                       | like an experimental  |                       |
|                       | science. Once you     |                       |
|                       | have an idea about    |                       |
|                       | what is going wrong,  |                       |
|                       | you modify your       |                       |
|                       | program and try       |                       |
|                       | again. If your        |                       |
|                       | hypothesis was        |                       |
|                       | correct, you can      |                       |
|                       | predict the result of |                       |
|                       | the modification, and |                       |
|                       | you take a step       |                       |
|                       | closer to a working   |                       |
|                       | program. If your      |                       |
|                       | hypothesis was wrong, |                       |
|                       | you have to come up   |                       |
|                       | with a new one. As    |                       |
|                       | Sherlock Holmes       |                       |
|                       | pointed out, "When    |                       |
|                       | you have eliminated   |                       |
|                       | the impossible,       |                       |
|                       | whatever remains,     |                       |
|                       | however improbable,   |                       |
|                       | must be the truth."   |                       |
|                       | (A. Conan Doyle, *The |                       |
|                       | Sign of Four*)        |                       |
|                       | []{#hevea_default229} |                       |
|                       | []{#hevea_default230} |                       |
|                       |                       |                       |
|                       | For some people,      |                       |
|                       | programming and       |                       |
|                       | debugging are the     |                       |
|                       | same thing. That is,  |                       |
|                       | programming is the    |                       |
|                       | process of gradually  |                       |
|                       | debugging a program   |                       |
|                       | until it does what    |                       |
|                       | you want. The idea is |                       |
|                       | that you should start |                       |
|                       | with a working        |                       |
|                       | program and make      |                       |
|                       | small modifications,  |                       |
|                       | debugging them as you |                       |
|                       | go.                   |                       |
|                       |                       |                       |
|                       | For example, Linux is |                       |
|                       | an operating system   |                       |
|                       | that contains         |                       |
|                       | millions of lines of  |                       |
|                       | code, but it started  |                       |
|                       | out as a simple       |                       |
|                       | program Linus         |                       |
|                       | Torvalds used to      |                       |
|                       | explore the Intel     |                       |
|                       | 80386 chip. According |                       |
|                       | to Larry Greenfield,  |                       |
|                       | "One of Linus's       |                       |
|                       | earlier projects was  |                       |
|                       | a program that would  |                       |
|                       | switch between        |                       |
|                       | printing AAAA and     |                       |
|                       | BBBB. This later      |                       |
|                       | evolved to Linux."    |                       |
|                       | (*The Linux Users'    |                       |
|                       | Guide* Beta Version   |                       |
|                       | 1).                   |                       |
|                       | []{#hevea_default231} |                       |
|                       |                       |                       |
|                       | ## 3.13  Gloss        |                       |
|                       | ary {#sec39 .section} |                       |
|                       |                       |                       |
|                       | [function:]{.c010}    |                       |
|                       | :   A named sequence  |                       |
|                       |     of statements     |                       |
|                       |     that performs     |                       |
|                       |     some useful       |                       |
|                       |     operation.        |                       |
|                       |     Functions may or  |                       |
|                       |     may not take      |                       |
|                       |     arguments and may |                       |
|                       |     or may not        |                       |
|                       |     produce a result. |                       |
|                       |                       |                       |
|                       | []{#hevea_default232} |                       |
|                       |                       |                       |
|                       | [functio              |                       |
|                       | n definition:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     creates a new     |                       |
|                       |     function,         |                       |
|                       |     specifying its    |                       |
|                       |     name, parameters, |                       |
|                       |     and the           |                       |
|                       |     statements it     |                       |
|                       |     contains.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default233} |                       |
|                       |                       |                       |
|                       | [fun                  |                       |
|                       | ction object:]{.c010} |                       |
|                       | :   A value created   |                       |
|                       |     by a function     |                       |
|                       |     definition. The   |                       |
|                       |     name of the       |                       |
|                       |     function is a     |                       |
|                       |     variable that     |                       |
|                       |     refers to a       |                       |
|                       |     function object.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default234} |                       |
|                       |                       |                       |
|                       | [header:]{.c010}      |                       |
|                       | :   The first line of |                       |
|                       |     a function        |                       |
|                       |     definition.       |                       |
|                       |                       |                       |
|                       | []{#hevea_default235} |                       |
|                       |                       |                       |
|                       | [body:]{.c010}        |                       |
|                       | :   The sequence of   |                       |
|                       |     statements inside |                       |
|                       |     a function        |                       |
|                       |     definition.       |                       |
|                       |                       |                       |
|                       | []{#hevea_default236} |                       |
|                       |                       |                       |
|                       | [parameter:]{.c010}   |                       |
|                       | :   A name used       |                       |
|                       |     inside a function |                       |
|                       |     to refer to the   |                       |
|                       |     value passed as   |                       |
|                       |     an argument.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default237} |                       |
|                       |                       |                       |
|                       | [f                    |                       |
|                       | unction call:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     runs a function.  |                       |
|                       |     It consists of    |                       |
|                       |     the function name |                       |
|                       |     followed by an    |                       |
|                       |     argument list in  |                       |
|                       |     parentheses.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default238} |                       |
|                       |                       |                       |
|                       | [argument:]{.c010}    |                       |
|                       | :   A value provided  |                       |
|                       |     to a function     |                       |
|                       |     when the function |                       |
|                       |     is called. This   |                       |
|                       |     value is assigned |                       |
|                       |     to the            |                       |
|                       |     corresponding     |                       |
|                       |     parameter in the  |                       |
|                       |     function.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default239} |                       |
|                       |                       |                       |
|                       | [lo                   |                       |
|                       | cal variable:]{.c010} |                       |
|                       | :   A variable        |                       |
|                       |     defined inside a  |                       |
|                       |     function. A local |                       |
|                       |     variable can only |                       |
|                       |     be used inside    |                       |
|                       |     its function.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default240} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | return value:]{.c010} |                       |
|                       | :   The result of a   |                       |
|                       |     function. If a    |                       |
|                       |     function call is  |                       |
|                       |     used as an        |                       |
|                       |     expression, the   |                       |
|                       |     return value is   |                       |
|                       |     the value of the  |                       |
|                       |     expression.       |                       |
|                       |                       |                       |
|                       | []{#hevea_default241} |                       |
|                       |                       |                       |
|                       | [fruit                |                       |
|                       | ful function:]{.c010} |                       |
|                       | :   A function that   |                       |
|                       |     returns a value.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default242} |                       |
|                       |                       |                       |
|                       | [v                    |                       |
|                       | oid function:]{.c010} |                       |
|                       | :   A function that   |                       |
|                       |     always returns    |                       |
|                       |     [None]{.c004}.    |                       |
|                       |                       |                       |
|                       | []{#hevea_default243} |                       |
|                       |                       |                       |
|                       | [[                    |                       |
|                       | None]{.c004}:]{.c010} |                       |
|                       | :   A special value   |                       |
|                       |     returned by void  |                       |
|                       |     functions.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default244} |                       |
|                       |                       |                       |
|                       | []{#hevea_default245} |                       |
|                       |                       |                       |
|                       | [module:]{.c010}      |                       |
|                       | :   A file that       |                       |
|                       |     contains a        |                       |
|                       |     collection of     |                       |
|                       |     related functions |                       |
|                       |     and other         |                       |
|                       |     definitions.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default246} |                       |
|                       |                       |                       |
|                       | [impo                 |                       |
|                       | rt statement:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     reads a module    |                       |
|                       |     file and creates  |                       |
|                       |     a module object.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default247} |                       |
|                       |                       |                       |
|                       | []{#hevea_default248} |                       |
|                       |                       |                       |
|                       | [m                    |                       |
|                       | odule object:]{.c010} |                       |
|                       | :   A value created   |                       |
|                       |     by an             |                       |
|                       |     [import]{.c004}   |                       |
|                       |     statement that    |                       |
|                       |     provides access   |                       |
|                       |     to the values     |                       |
|                       |     defined in a      |                       |
|                       |     module.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default249} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | dot notation:]{.c010} |                       |
|                       | :   The syntax for    |                       |
|                       |     calling a         |                       |
|                       |     function in       |                       |
|                       |     another module by |                       |
|                       |     specifying the    |                       |
|                       |     module name       |                       |
|                       |     followed by a dot |                       |
|                       |     (period) and the  |                       |
|                       |     function name.    |                       |
|                       |                       |                       |
|                       | []{#hevea_default250} |                       |
|                       |                       |                       |
|                       | [composition:]{.c010} |                       |
|                       | :   Using an          |                       |
|                       |     expression as     |                       |
|                       |     part of a larger  |                       |
|                       |     expression, or a  |                       |
|                       |     statement as part |                       |
|                       |     of a larger       |                       |
|                       |     statement.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default251} |                       |
|                       |                       |                       |
|                       | [flow                 |                       |
|                       | of execution:]{.c010} |                       |
|                       | :   The order         |                       |
|                       |     statements run    |                       |
|                       |     in.               |                       |
|                       |                       |                       |
|                       | []{#hevea_default252} |                       |
|                       |                       |                       |
|                       | [s                    |                       |
|                       | tack diagram:]{.c010} |                       |
|                       | :   A graphical       |                       |
|                       |     representation of |                       |
|                       |     a stack of        |                       |
|                       |     functions, their  |                       |
|                       |     variables, and    |                       |
|                       |     the values they   |                       |
|                       |     refer to.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default253} |                       |
|                       |                       |                       |
|                       | [frame:]{.c010}       |                       |
|                       | :   A box in a stack  |                       |
|                       |     diagram that      |                       |
|                       |     represents a      |                       |
|                       |     function call. It |                       |
|                       |     contains the      |                       |
|                       |     local variables   |                       |
|                       |     and parameters of |                       |
|                       |     the function.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default254} |                       |
|                       |                       |                       |
|                       | []{#hevea_default255} |                       |
|                       |                       |                       |
|                       | [traceback:]{.c010}   |                       |
|                       | :   A list of the     |                       |
|                       |     functions that    |                       |
|                       |     are executing,    |                       |
|                       |     printed when an   |                       |
|                       |     exception occurs. |                       |
|                       |                       |                       |
|                       | []{#hevea_default256} |                       |
|                       |                       |                       |
|                       | ## 3.14  Exerci       |                       |
|                       | ses {#sec40 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       | []{#hevea_default257} |                       |
|                       | []{#hevea_default258} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named `right_justify` |                       |
|                       | that takes a string   |                       |
|                       | named [s]{.c004} as a |                       |
|                       | parameter and prints  |                       |
|                       | the string with       |                       |
|                       | enough leading spaces |                       |
|                       | so that the last      |                       |
|                       | letter of the string  |                       |
|                       | is in column 70 of    |                       |
|                       | the display.*         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> r                 |                       |
|                       | ight_justify('monty') |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |                 monty |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *Hint: Use string     |                       |
|                       | concatenation and     |                       |
|                       | repetition. Also,     |                       |
|                       | Python provides a     |                       |
|                       | built-in function     |                       |
|                       | called [len]{.c004}   |                       |
|                       | that returns the      |                       |
|                       | length of a string,   |                       |
|                       | so the value of       |                       |
|                       | `len('monty')` is 5.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#hevea_default259} |                       |
|                       | []{#hevea_default260} |                       |
|                       |                       |                       |
|                       | *A function object is |                       |
|                       | a value you can       |                       |
|                       | assign to a variable  |                       |
|                       | or pass as an         |                       |
|                       | argument. For         |                       |
|                       | example, `do_twice`   |                       |
|                       | is a function that    |                       |
|                       | takes a function      |                       |
|                       | object as an argument |                       |
|                       | and calls it twice:*  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def do_twice(f):      |                       |
|                       |     f()               |                       |
|                       |     f()               |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *Here's an example    |                       |
|                       | that uses `do_twice`  |                       |
|                       | to call a function    |                       |
|                       | named `print_spam`    |                       |
|                       | twice.*               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_spam():     |                       |
|                       |     print('spam')     |                       |
|                       |                       |                       |
|                       | do_twice(print_spam)  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | 1.  *Type this        |                       |
|                       |     example into a    |                       |
|                       |     script and test   |                       |
|                       |     it.*              |                       |
|                       | 2.  *Modify           |                       |
|                       |     `do_twice` so     |                       |
|                       |     that it takes two |                       |
|                       |     arguments, a      |                       |
|                       |     function object   |                       |
|                       |     and a value, and  |                       |
|                       |     calls the         |                       |
|                       |     function twice,   |                       |
|                       |     passing the value |                       |
|                       |     as an argument.*  |                       |
|                       | 3.  *Copy the         |                       |
|                       |     definition of     |                       |
|                       |     `print_twice`     |                       |
|                       |     from earlier in   |                       |
|                       |     this chapter to   |                       |
|                       |     your script.*     |                       |
|                       | 4.  *Use the modified |                       |
|                       |     version of        |                       |
|                       |     `do_twice` to     |                       |
|                       |     call              |                       |
|                       |     `print_twice`     |                       |
|                       |     twice, passing    |                       |
|                       |     `'spam'` as an    |                       |
|                       |     argument.*        |                       |
|                       | 5.  *Define a new     |                       |
|                       |     function called   |                       |
|                       |     `do_four` that    |                       |
|                       |     takes a function  |                       |
|                       |     object and a      |                       |
|                       |     value and calls   |                       |
|                       |     the function four |                       |
|                       |     times, passing    |                       |
|                       |     the value as a    |                       |
|                       |     parameter. There  |                       |
|                       |     should be only    |                       |
|                       |     two statements in |                       |
|                       |     the body of this  |                       |
|                       |     function, not     |                       |
|                       |     four.*            |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[https://t          |                       |
|                       | hinkpython.com/code/d |                       |
|                       | o_four.py]{.c004}*](h |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/do_four.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       |                       |                       |
|                       | *Note: This exercise  |                       |
|                       | should be done using  |                       |
|                       | only the statements   |                       |
|                       | and other features we |                       |
|                       | have learned so far.* |                       |
|                       |                       |                       |
|                       | 1.  *Write a function |                       |
|                       |     that draws a grid |                       |
|                       |     like the          |                       |
|                       |     following:*       |                       |
|                       |                       |                       |
|                       | []{#hevea_default261} |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |                       |                       |
|                       | + - - - - + - - - - + |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | + - - - - + - - - - + |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | |         |         | |                       |
|                       |                       |                       |
|                       | + - - - - + - - - - + |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     *Hint: to print   |                       |
|                       |     more than one     |                       |
|                       |     value on a line,  |                       |
|                       |     you can print a   |                       |
|                       |     comma-separated   |                       |
|                       |     sequence of       |                       |
|                       |     values:*          |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |     print('+', '-')   |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     *By default,      |                       |
|                       |     [print]{.c004}    |                       |
|                       |     advances to the   |                       |
|                       |     next line, but    |                       |
|                       |     you can override  |                       |
|                       |     that behavior and |                       |
|                       |     put a space at    |                       |
|                       |     the end, like     |                       |
|                       |     this:*            |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |                       |                       |
|                       |   print('+', end=' ') |                       |
|                       |     print('-')        |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     *The output of    |                       |
|                       |     these statements  |                       |
|                       |     is `'+ -'` on the |                       |
|                       |     same line. The    |                       |
|                       |     output from the   |                       |
|                       |     next print        |                       |
|                       |     statement would   |                       |
|                       |     begin on the next |                       |
|                       |     line.*            |                       |
|                       |                       |                       |
|                       | 2.  *Write a function |                       |
|                       |     that draws a      |                       |
|                       |     similar grid with |                       |
|                       |     four rows and     |                       |
|                       |     four columns.*    |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[ht                 |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/grid.py]{.c004} |                       |
|                       | *](https://thinkpytho |                       |
|                       | n.com/code/grid.py)*. |                       |
|                       | Credit: This exercise |                       |
|                       | is based on an        |                       |
|                       | exercise in           |                       |
|                       | Oualline,* Practical  |                       |
|                       | C Programming, Third  |                       |
|                       | Edition*, O'Reilly    |                       |
|                       | Media, 1997.*         |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2003.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2005.html)
---
generator: hevea 2.32
title: "Case study: interface design"
---

[![Previous](back.png)](thinkpython2004.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2006.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 4  Case     | to support my books,  |
|                       |  study: interface des | you can use the       |
|                       | ign {#sec41 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | []{#turtlechap}       | you!                  |
|                       |                       |                       |
|                       | This chapter presents |   -----------         |
|                       | a case study that     | --------------------- |
|                       | demonstrates a        | --------------------- |
|                       | process for designing | --------------------- |
|                       | functions that work   | --------------------- |
|                       | together.             |   Pay what you want:  |
|                       |                       |   Small \$1           |
|                       | It introduces the     | .00 USD Medium \$5.00 |
|                       | [turtle]{.c004}       |  USD Large \$10.00 US |
|                       | module, which allows  | D X-Large \$20.00 USD |
|                       | you to create images  |  XX-Large \$50.00 USD |
|                       | using turtle          |   -----------         |
|                       | graphics. The         | --------------------- |
|                       | [turtle]{.c004}       | --------------------- |
|                       | module is included in | --------------------- |
|                       | most Python           | --------------------- |
|                       | installations, but if |                       |
|                       | you are running       | ![](                  |
|                       | Python using          | https://www.paypalobj |
|                       | PythonAnywhere, you   | ects.com/en_US/i/scr/ |
|                       | won't be able to run  | pixel.gif){border="0" |
|                       | the turtle examples   | width="1" height="1"} |
|                       | (at least you         |                       |
|                       | couldn't when I wrote | ####                  |
|                       | this).                | Are you using one of  |
|                       |                       | our books in a class? |
|                       | If you have already   |                       |
|                       | installed Python on   | We\'d like to know    |
|                       | your computer, you    | about it. Please      |
|                       | should be able to run | consider filling out  |
|                       | the examples.         | [this short           |
|                       | Otherwise, now is a   | survey](http://s      |
|                       | good time to install. | preadsheets.google.co |
|                       | I have posted         | m/viewform?formkey=dC |
|                       | instructions at       | 0tNUZkMjBEdXVoRGljNm9 |
|                       | [[http://tinyur       | FRmlTMHc6MA){onclick= |
|                       | l.com/thinkpython2e]{ | "javascript: pageTrac |
|                       | .c004}](http://tinyur | ker._trackPageview('/ |
|                       | l.com/thinkpython2e). | outbound/survey');"}. |
|                       |                       |                       |
|                       | Code examples from    | \                     |
|                       | this chapter are      |                       |
|                       | available from        | [Think                |
|                       | [[https:              | DSP](http             |
|                       | //thinkpython.com/cod | ://www.amazon.com/gp/ |
|                       | e/polygon.py]{.c004}] | product/1491938455/re |
|                       | (https://thinkpython. | f=as_li_tl?ie=UTF8&ca |
|                       | com/code/polygon.py). | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491938 |
|                       | #                     | 455&linkCode=as2&tag= |
|                       | # 4.1  The turtle mod | greenteapre01-20&link |
|                       | ule {#sec42 .section} | Id=2JJH4SWCAVVYSQHO){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | []{#turtle}           | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | To check whether you  | nteapre01-20&l=as2&o= |
|                       | have the              | 1&a=1491938455){.c003 |
|                       | [turtle]{.c004}       | width="1" height="1"  |
|                       | module, open the      | border="0"}           |
|                       | Python interpreter    |                       |
|                       | and type              | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | ``` verbatim          | on-adsystem.com/widge |
|                       | >>> import turtle     | ts/q?_encoding=UTF8&A |
|                       | >>>                   | SIN=1491938455&Format |
|                       | bob = turtle.Turtle() | =_SL160_&ID=AsinImage |
|                       | ```                   | &MarketPlace=US&Servi |
|                       |                       | ceVersion=20070822&WS |
|                       | When you run this     | =1&tag=greenteapre01- |
|                       | code, it should       | 20){border="0"}](http |
|                       | create a new window   | ://www.amazon.com/gp/ |
|                       | with small arrow that | product/1491938455/re |
|                       | represents the        | f=as_li_tl?ie=UTF8&ca |
|                       | turtle. Close the     | mp=1789&creative=9325 |
|                       | window.               | &creativeASIN=1491938 |
|                       |                       | 455&linkCode=as2&tag= |
|                       | Create a file named   | greenteapre01-20&link |
|                       | [mypolygon.py]{.c004} | Id=CTV7PDT7E5EGGJUM){ |
|                       | and type in the       | rel="nofollow"}![](ht |
|                       | following code:       | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | ``` verbatim          | nteapre01-20&l=as2&o= |
|                       | import turtle         | 1&a=1491938455){.c003 |
|                       | bob = turtle.Turtle() | width="1" height="1"  |
|                       | print(bob)            | border="0"}           |
|                       | turtle.mainloop()     |                       |
|                       | ```                   | [Think                |
|                       |                       | Java](http            |
|                       | The [turtle]{.c004}   | ://www.amazon.com/gp/ |
|                       | module (with a        | product/1491929561/re |
|                       | lowercase 't')        | f=as_li_tl?ie=UTF8&ca |
|                       | provides a function   | mp=1789&creative=9325 |
|                       | called                | &creativeASIN=1491929 |
|                       | [Turtle]{.c004} (with | 561&linkCode=as2&tag= |
|                       | an uppercase 'T')     | greenteapre01-20&link |
|                       | that creates a Turtle | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | object, which we      | rel="nofollow"}![](ht |
|                       | assign to a variable  | tp://ir-na.amazon-ads |
|                       | named [bob]{.c004}.   | ystem.com/e/ir?t=gree |
|                       | Printing [bob]{.c004} | nteapre01-20&l=as2&o= |
|                       | displays something    | 1&a=1491929561){.c003 |
|                       | like:                 | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | ``` verbatim          |                       |
|                       | <turtle.Turtle        | [                     |
|                       | object at 0xb7bfbf4c> | ![](http://ws-na.amaz |
|                       | ```                   | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | This means that       | SIN=1491929561&Format |
|                       | [bob]{.c004} refers   | =_SL160_&ID=AsinImage |
|                       | to an object with     | &MarketPlace=US&Servi |
|                       | type [Turtle]{.c004}  | ceVersion=20070822&WS |
|                       | as defined in module  | =1&tag=greenteapre01- |
|                       | [turtle]{.c004}.      | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | `mainloop` tells the  | product/1491929561/re |
|                       | window to wait for    | f=as_li_tl?ie=UTF8&ca |
|                       | the user to do        | mp=1789&creative=9325 |
|                       | something, although   | &creativeASIN=1491929 |
|                       | in this case there's  | 561&linkCode=as2&tag= |
|                       | not much for the user | greenteapre01-20&link |
|                       | to do except close    | Id=PT77ANWARUNNU3UK){ |
|                       | the window.           | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | Once you create a     | ystem.com/e/ir?t=gree |
|                       | Turtle, you can call  | nteapre01-20&l=as2&o= |
|                       | a [method]{.c010} to  | 1&a=1491929561){.c003 |
|                       | move it around the    | width="1" height="1"  |
|                       | window. A method is   | border="0"}           |
|                       | similar to a          |                       |
|                       | function, but it uses | [Think                |
|                       | slightly different    | Bay                   |
|                       | syntax. For example,  | es](http://www.amazon |
|                       | to move the turtle    | .com/gp/product/14493 |
|                       | forward:              | 70780/ref=as_li_qf_sp |
|                       |                       | _asin_tl?ie=UTF8&camp |
|                       | ``` verbatim          | =1789&creative=9325&c |
|                       | bob.fd(100)           | reativeASIN=144937078 |
|                       | ```                   | 0&linkCode=as2&tag=gr |
|                       |                       | eenteapre01-20)![](ht |
|                       | The method,           | tp://ir-na.amazon-ads |
|                       | [fd]{.c004}, is       | ystem.com/e/ir?t=gree |
|                       | associated with the   | nteapre01-20&l=as2&o= |
|                       | turtle object we're   | 1&a=1449370780){.c003 |
|                       | calling [bob]{.c004}. | width="1" height="1"  |
|                       | Calling a method is   | border="0"}           |
|                       | like making a         |                       |
|                       | request: you are      | [![](http://ws        |
|                       | asking [bob]{.c004}   | -na.amazon-adsystem.c |
|                       | to move forward.      | om/widgets/q?_encodin |
|                       |                       | g=UTF8&ASIN=144937078 |
|                       | The argument of       | 0&Format=_SL160_&ID=A |
|                       | [fd]{.c004} is a      | sinImage&MarketPlace= |
|                       | distance in pixels,   | US&ServiceVersion=200 |
|                       | so the actual size    | 70822&WS=1&tag=greent |
|                       | depends on your       | eapre01-20){border="0 |
|                       | display.              | "}](http://www.amazon |
|                       |                       | .com/gp/product/14493 |
|                       | Other methods you can | 70780/ref=as_li_qf_sp |
|                       | call on a Turtle are  | _asin_il?ie=UTF8&camp |
|                       | [bk]{.c004} to move   | =1789&creative=9325&c |
|                       | backward, [lt]{.c004} | reativeASIN=144937078 |
|                       | for left turn, and    | 0&linkCode=as2&tag=gr |
|                       | [rt]{.c004} right     | eenteapre01-20)![](ht |
|                       | turn. The argument    | tp://ir-na.amazon-ads |
|                       | for [lt]{.c004} and   | ystem.com/e/ir?t=gree |
|                       | [rt]{.c004} is an     | nteapre01-20&l=as2&o= |
|                       | angle in degrees.     | 1&a=1449370780){.c003 |
|                       |                       | width="1" height="1"  |
|                       | Also, each Turtle is  | border="0"}           |
|                       | holding a pen, which  |                       |
|                       | is either down or up; | [Think Python         |
|                       | if the pen is down,   | 2e](http              |
|                       | the Turtle leaves a   | ://www.amazon.com/gp/ |
|                       | trail when it moves.  | product/1491939362/re |
|                       | The methods           | f=as_li_tl?ie=UTF8&ca |
|                       | [pu]{.c004} and       | mp=1789&creative=9325 |
|                       | [pd]{.c004} stand for | &creativeASIN=1491939 |
|                       | "pen up" and "pen     | 362&linkCode=as2&tag= |
|                       | down".                | greenteapre01-20&link |
|                       |                       | Id=FJKSQ3IHEMY2F2VA){ |
|                       | To draw a right       | rel="nofollow"}![](ht |
|                       | angle, add these      | tp://ir-na.amazon-ads |
|                       | lines to the program  | ystem.com/e/ir?t=gree |
|                       | (after creating       | nteapre01-20&l=as2&o= |
|                       | [bob]{.c004} and      | 1&a=1491939362){.c003 |
|                       | before calling        | width="1" height="1"  |
|                       | `mainloop`):          | border="0"}           |
|                       |                       |                       |
|                       | ``` verbatim          | [                     |
|                       | bob.fd(100)           | ![](http://ws-na.amaz |
|                       | bob.lt(90)            | on-adsystem.com/widge |
|                       | bob.fd(100)           | ts/q?_encoding=UTF8&A |
|                       | ```                   | SIN=1491939362&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | When you run this     | &MarketPlace=US&Servi |
|                       | program, you should   | ceVersion=20070822&WS |
|                       | see [bob]{.c004} move | =1&tag=greenteapre01- |
|                       | east and then north,  | 20){border="0"}](http |
|                       | leaving two line      | ://www.amazon.com/gp/ |
|                       | segments behind.      | product/1491939362/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | Now modify the        | mp=1789&creative=9325 |
|                       | program to draw a     | &creativeASIN=1491939 |
|                       | square. Don't go on   | 362&linkCode=as2&tag= |
|                       | until you've got it   | greenteapre01-20&link |
|                       | working!              | Id=ZZ454DLQ3IXDHNHX){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | #                     | tp://ir-na.amazon-ads |
|                       | # 4.2  Simple repetit | ystem.com/e/ir?t=gree |
|                       | ion {#sec43 .section} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | []{#repetition}       | width="1" height="1"  |
|                       | []{#hevea_default262} | border="0"}           |
|                       |                       |                       |
|                       | Chances are you wrote | [Think Stats          |
|                       | something like this:  | 2e](http://ww         |
|                       |                       | w.amazon.com/gp/produ |
|                       | ``` verbatim          | ct/1491907339/ref=as_ |
|                       | bob.fd(100)           | li_tl?ie=UTF8&camp=17 |
|                       | bob.lt(90)            | 89&creative=9325&crea |
|                       |                       | tiveASIN=1491907339&l |
|                       | bob.fd(100)           | inkCode=as2&tag=green |
|                       | bob.lt(90)            | teapre01-20&linkId=O7 |
|                       |                       | WYM6H6YBYUFNWU)![](ht |
|                       | bob.fd(100)           | tp://ir-na.amazon-ads |
|                       | bob.lt(90)            | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | bob.fd(100)           | 1&a=1491907339){.c003 |
|                       | ```                   | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | We can do the same    |                       |
|                       | thing more concisely  | [![](h                |
|                       | with a [for]{.c004}   | ttp://ws-na.amazon-ad |
|                       | statement. Add this   | system.com/widgets/q? |
|                       | example to            | _encoding=UTF8&ASIN=1 |
|                       | [mypolygon.py]{.c004} | 491907339&Format=_SL1 |
|                       | and run it again:     | 60_&ID=AsinImage&Mark |
|                       | []{#hevea_default263} | etPlace=US&ServiceVer |
|                       | []{#hevea_default264} | sion=20070822&WS=1&ta |
|                       | []{#hevea_default265} | g=greenteapre01-20){b |
|                       |                       | order="0"}](http://ww |
|                       | ``` verbatim          | w.amazon.com/gp/produ |
|                       | for i in range(4):    | ct/1491907339/ref=as_ |
|                       |     print('Hello!')   | li_tl?ie=UTF8&camp=17 |
|                       | ```                   | 89&creative=9325&crea |
|                       |                       | tiveASIN=1491907339&l |
|                       | You should see        | inkCode=as2&tag=green |
|                       | something like this:  | teapre01-20&linkId=JV |
|                       |                       | SYKQHYSUIEYRHL)![](ht |
|                       | ``` verbatim          | tp://ir-na.amazon-ads |
|                       | Hello!                | ystem.com/e/ir?t=gree |
|                       | Hello!                | nteapre01-20&l=as2&o= |
|                       | Hello!                | 1&a=1491907339){.c003 |
|                       | Hello!                | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | This is the simplest  | [Think                |
|                       | use of the            | Complexity](http      |
|                       | [for]{.c004}          | ://www.amazon.com/gp/ |
|                       | statement; we will    | product/1449314635/re |
|                       | see more later. But   | f=as_li_tf_tl?ie=UTF8 |
|                       | that should be enough | &tag=greenteapre01-20 |
|                       | to let you rewrite    | &linkCode=as2&camp=17 |
|                       | your square-drawing   | 89&creative=9325&crea |
|                       | program. Don't go on  | tiveASIN=1449314635)! |
|                       | until you do.         | [](http://www.assoc-a |
|                       |                       | mazon.com/e/ir?t=gree |
|                       | Here is a             | nteapre01-20&l=as2&o= |
|                       | [for]{.c004}          | 1&a=1449314635){.c003 |
|                       | statement that draws  | width="1" height="1"  |
|                       | a square:             | border="0"}           |
|                       |                       |                       |
|                       | ``` verbatim          | [                     |
|                       | for i in range(4):    | ![](http://ws-na.amaz |
|                       |     bob.fd(100)       | on-adsystem.com/widge |
|                       |     bob.lt(90)        | ts/q?_encoding=UTF8&A |
|                       | ```                   | SIN=1449314635&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | The syntax of a       | &MarketPlace=US&Servi |
|                       | [for]{.c004}          | ceVersion=20070822&WS |
|                       | statement is similar  | =1&tag=greenteapre01- |
|                       | to a function         | 20){border="0"}](http |
|                       | definition. It has a  | ://www.amazon.com/gp/ |
|                       | header that ends with | product/1449314635/re |
|                       | a colon and an        | f=as_li_tf_il?ie=UTF8 |
|                       | indented body. The    | &camp=1789&creative=9 |
|                       | body can contain any  | 325&creativeASIN=1449 |
|                       | number of statements. | 314635&linkCode=as2&t |
|                       |                       | ag=greenteapre01-20)! |
|                       | A [for]{.c004}        | [](http://www.assoc-a |
|                       | statement is also     | mazon.com/e/ir?t=gree |
|                       | called a              | nteapre01-20&l=as2&o= |
|                       | [loop]{.c010} because | 1&a=1449314635){.c003 |
|                       | the flow of execution | width="1" height="1"  |
|                       | runs through the body | border="0"}           |
|                       | and then loops back   |                       |
|                       | to the top. In this   |                       |
|                       | case, it runs the     |                       |
|                       | body four times.      |                       |
|                       | []{#hevea_default266} |                       |
|                       |                       |                       |
|                       | This version is       |                       |
|                       | actually a little     |                       |
|                       | different from the    |                       |
|                       | previous              |                       |
|                       | square-drawing code   |                       |
|                       | because it makes      |                       |
|                       | another turn after    |                       |
|                       | drawing the last side |                       |
|                       | of the square. The    |                       |
|                       | extra turn takes more |                       |
|                       | time, but it          |                       |
|                       | simplifies the code   |                       |
|                       | if we do the same     |                       |
|                       | thing every time      |                       |
|                       | through the loop.     |                       |
|                       | This version also has |                       |
|                       | the effect of leaving |                       |
|                       | the turtle back in    |                       |
|                       | the starting          |                       |
|                       | position, facing in   |                       |
|                       | the starting          |                       |
|                       | direction.            |                       |
|                       |                       |                       |
|                       | ## 4.3  Exerci        |                       |
|                       | ses {#sec44 .section} |                       |
|                       |                       |                       |
|                       | The following is a    |                       |
|                       | series of exercises   |                       |
|                       | using the             |                       |
|                       | [turtle]{.c004}       |                       |
|                       | module. They are      |                       |
|                       | meant to be fun, but  |                       |
|                       | they have a point,    |                       |
|                       | too. While you are    |                       |
|                       | working on them,      |                       |
|                       | think about what the  |                       |
|                       | point is.             |                       |
|                       |                       |                       |
|                       | The following         |                       |
|                       | sections have         |                       |
|                       | solutions to the      |                       |
|                       | exercises, so don't   |                       |
|                       | look until you have   |                       |
|                       | finished (or at least |                       |
|                       | tried).               |                       |
|                       |                       |                       |
|                       | 1.  Write a function  |                       |
|                       |     called            |                       |
|                       |     [square]{.c004}   |                       |
|                       |     that takes a      |                       |
|                       |     parameter named   |                       |
|                       |     [t]{.c004}, which |                       |
|                       |     is a turtle. It   |                       |
|                       |     should use the    |                       |
|                       |     turtle to draw a  |                       |
|                       |     square.           |                       |
|                       |                       |                       |
|                       |     Write a function  |                       |
|                       |     call that passes  |                       |
|                       |     [bob]{.c004} as   |                       |
|                       |     an argument to    |                       |
|                       |     [square]{.c004},  |                       |
|                       |     and then run the  |                       |
|                       |     program again.    |                       |
|                       |                       |                       |
|                       | 2.  Add another       |                       |
|                       |     parameter, named  |                       |
|                       |     [length]{.c004},  |                       |
|                       |     to                |                       |
|                       |     [square]{.c004}.  |                       |
|                       |     Modify the body   |                       |
|                       |     so length of the  |                       |
|                       |     sides is          |                       |
|                       |     [length]{.c004},  |                       |
|                       |     and then modify   |                       |
|                       |     the function call |                       |
|                       |     to provide a      |                       |
|                       |     second argument.  |                       |
|                       |     Run the program   |                       |
|                       |     again. Test your  |                       |
|                       |     program with a    |                       |
|                       |     range of values   |                       |
|                       |     for               |                       |
|                       |     [length]{.c004}.  |                       |
|                       |                       |                       |
|                       | 3.  Make a copy of    |                       |
|                       |     [square]{.c004}   |                       |
|                       |     and change the    |                       |
|                       |     name to           |                       |
|                       |     [polygon]{.c004}. |                       |
|                       |     Add another       |                       |
|                       |     parameter named   |                       |
|                       |     [n]{.c004} and    |                       |
|                       |     modify the body   |                       |
|                       |     so it draws an    |                       |
|                       |     n-sided regular   |                       |
|                       |     polygon. Hint:    |                       |
|                       |     The exterior      |                       |
|                       |     angles of an      |                       |
|                       |     n-sided regular   |                       |
|                       |     polygon are       |                       |
|                       |     360/[n]{.c009}    |                       |
|                       |     degrees.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default267} |                       |
|                       |                       |                       |
|                       | []{#hevea_default268} |                       |
|                       |                       |                       |
|                       | 4.  Write a function  |                       |
|                       |     called            |                       |
|                       |     [circle]{.c004}   |                       |
|                       |     that takes a      |                       |
|                       |     turtle,           |                       |
|                       |     [t]{.c004}, and   |                       |
|                       |     radius,           |                       |
|                       |     [r]{.c004}, as    |                       |
|                       |     parameters and    |                       |
|                       |     that draws an     |                       |
|                       |     approximate       |                       |
|                       |     circle by calling |                       |
|                       |     [polygon]{.c004}  |                       |
|                       |     with an           |                       |
|                       |     appropriate       |                       |
|                       |     length and number |                       |
|                       |     of sides. Test    |                       |
|                       |     your function     |                       |
|                       |     with a range of   |                       |
|                       |     values of         |                       |
|                       |     [r]{.c004}.       |                       |
|                       |                       |                       |
|                       | []{#hevea_default269} |                       |
|                       |                       |                       |
|                       | []{#hevea_default270} |                       |
|                       |                       |                       |
|                       |     Hint: figure out  |                       |
|                       |     the circumference |                       |
|                       |     of the circle and |                       |
|                       |     make sure that    |                       |
|                       |     [length \* n =    |                       |
|                       |     c                 |                       |
|                       | ircumference]{.c004}. |                       |
|                       |                       |                       |
|                       | 5.  Make a more       |                       |
|                       |     general version   |                       |
|                       |     of                |                       |
|                       |     [circle]{.c004}   |                       |
|                       |     called            |                       |
|                       |     [arc]{.c004} that |                       |
|                       |     takes an          |                       |
|                       |     additional        |                       |
|                       |     parameter         |                       |
|                       |     [angle]{.c004},   |                       |
|                       |     which determines  |                       |
|                       |     what fraction of  |                       |
|                       |     a circle to draw. |                       |
|                       |     [angle]{.c004} is |                       |
|                       |     in units of       |                       |
|                       |     degrees, so when  |                       |
|                       |                       |                       |
|                       |   [angle=360]{.c004}, |                       |
|                       |     [arc]{.c004}      |                       |
|                       |     should draw a     |                       |
|                       |     complete circle.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default271} |                       |
|                       |                       |                       |
|                       | []{#hevea_default272} |                       |
|                       |                       |                       |
|                       | ## 4.4  Encapsulat    |                       |
|                       | ion {#sec45 .section} |                       |
|                       |                       |                       |
|                       | The first exercise    |                       |
|                       | asks you to put your  |                       |
|                       | square-drawing code   |                       |
|                       | into a function       |                       |
|                       | definition and then   |                       |
|                       | call the function,    |                       |
|                       | passing the turtle as |                       |
|                       | a parameter. Here is  |                       |
|                       | a solution:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def square(t):        |                       |
|                       |                       |                       |
|                       |    for i in range(4): |                       |
|                       |         t.fd(100)     |                       |
|                       |         t.lt(90)      |                       |
|                       |                       |                       |
|                       | square(bob)           |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The innermost         |                       |
|                       | statements,           |                       |
|                       | [fd]{.c004} and       |                       |
|                       | [lt]{.c004} are       |                       |
|                       | indented twice to     |                       |
|                       | show that they are    |                       |
|                       | inside the            |                       |
|                       | [for]{.c004} loop,    |                       |
|                       | which is inside the   |                       |
|                       | function definition.  |                       |
|                       | The next line,        |                       |
|                       | [square(bob)]{.c004}, |                       |
|                       | is flush with the     |                       |
|                       | left margin, which    |                       |
|                       | indicates the end of  |                       |
|                       | both the [for]{.c004} |                       |
|                       | loop and the function |                       |
|                       | definition.           |                       |
|                       |                       |                       |
|                       | Inside the function,  |                       |
|                       | [t]{.c004} refers to  |                       |
|                       | the same turtle       |                       |
|                       | [bob]{.c004}, so      |                       |
|                       | [t.lt(90)]{.c004} has |                       |
|                       | the same effect as    |                       |
|                       | [bob.lt(90)]{.c004}.  |                       |
|                       | In that case, why not |                       |
|                       | call the parameter    |                       |
|                       | [bob]{.c004}? The     |                       |
|                       | idea is that          |                       |
|                       | [t]{.c004} can be any |                       |
|                       | turtle, not just      |                       |
|                       | [bob]{.c004}, so you  |                       |
|                       | could create a second |                       |
|                       | turtle and pass it as |                       |
|                       | an argument to        |                       |
|                       | [square]{.c004}:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | al                    |                       |
|                       | ice = turtle.Turtle() |                       |
|                       | square(alice)         |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Wrapping a piece of   |                       |
|                       | code up in a function |                       |
|                       | is called             |                       |
|                       | [e                    |                       |
|                       | ncapsulation]{.c010}. |                       |
|                       | One of the benefits   |                       |
|                       | of encapsulation is   |                       |
|                       | that it attaches a    |                       |
|                       | name to the code,     |                       |
|                       | which serves as a     |                       |
|                       | kind of               |                       |
|                       | documentation.        |                       |
|                       | Another advantage is  |                       |
|                       | that if you re-use    |                       |
|                       | the code, it is more  |                       |
|                       | concise to call a     |                       |
|                       | function twice than   |                       |
|                       | to copy and paste the |                       |
|                       | body!                 |                       |
|                       | []{#hevea_default273} |                       |
|                       |                       |                       |
|                       | ## 4.5  Generalizat   |                       |
|                       | ion {#sec46 .section} |                       |
|                       |                       |                       |
|                       | The next step is to   |                       |
|                       | add a [length]{.c004} |                       |
|                       | parameter to          |                       |
|                       | [square]{.c004}. Here |                       |
|                       | is a solution:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef square(t, length): |                       |
|                       |                       |                       |
|                       |    for i in range(4): |                       |
|                       |         t.fd(length)  |                       |
|                       |         t.lt(90)      |                       |
|                       |                       |                       |
|                       | square(bob, 100)      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Adding a parameter to |                       |
|                       | a function is called  |                       |
|                       | [g                    |                       |
|                       | eneralization]{.c010} |                       |
|                       | because it makes the  |                       |
|                       | function more         |                       |
|                       | general: in the       |                       |
|                       | previous version, the |                       |
|                       | square is always the  |                       |
|                       | same size; in this    |                       |
|                       | version it can be any |                       |
|                       | size.                 |                       |
|                       | []{#hevea_default274} |                       |
|                       |                       |                       |
|                       | The next step is also |                       |
|                       | a generalization.     |                       |
|                       | Instead of drawing    |                       |
|                       | squares,              |                       |
|                       | [polygon]{.c004}      |                       |
|                       | draws regular         |                       |
|                       | polygons with any     |                       |
|                       | number of sides. Here |                       |
|                       | is a solution:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def p                 |                       |
|                       | olygon(t, n, length): |                       |
|                       |     angle = 360 / n   |                       |
|                       |                       |                       |
|                       |    for i in range(n): |                       |
|                       |         t.fd(length)  |                       |
|                       |         t.lt(angle)   |                       |
|                       |                       |                       |
|                       | polygon(bob, 7, 70)   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This example draws a  |                       |
|                       | 7-sided polygon with  |                       |
|                       | side length 70.       |                       |
|                       |                       |                       |
|                       | If you are using      |                       |
|                       | Python 2, the value   |                       |
|                       | of [angle]{.c004}     |                       |
|                       | might be off because  |                       |
|                       | of integer division.  |                       |
|                       | A simple solution is  |                       |
|                       | to compute [angle =   |                       |
|                       | 360.0 / n]{.c004}.    |                       |
|                       | Because the numerator |                       |
|                       | is a floating-point   |                       |
|                       | number, the result is |                       |
|                       | floating point.       |                       |
|                       | []{#hevea_default275} |                       |
|                       |                       |                       |
|                       | When a function has   |                       |
|                       | more than a few       |                       |
|                       | numeric arguments, it |                       |
|                       | is easy to forget     |                       |
|                       | what they are, or     |                       |
|                       | what order they       |                       |
|                       | should be in. In that |                       |
|                       | case it is often a    |                       |
|                       | good idea to include  |                       |
|                       | the names of the      |                       |
|                       | parameters in the     |                       |
|                       | argument list:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | polygon               |                       |
|                       | (bob, n=7, length=70) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | These are called      |                       |
|                       | [keyword              |                       |
|                       | arguments]{.c010}     |                       |
|                       | because they include  |                       |
|                       | the parameter names   |                       |
|                       | as "keywords" (not to |                       |
|                       | be confused with      |                       |
|                       | Python keywords like  |                       |
|                       | [while]{.c004} and    |                       |
|                       | [def]{.c004}).        |                       |
|                       | []{#hevea_default276} |                       |
|                       | []{#hevea_default277} |                       |
|                       |                       |                       |
|                       | This syntax makes the |                       |
|                       | program more          |                       |
|                       | readable. It is also  |                       |
|                       | a reminder about how  |                       |
|                       | arguments and         |                       |
|                       | parameters work: when |                       |
|                       | you call a function,  |                       |
|                       | the arguments are     |                       |
|                       | assigned to the       |                       |
|                       | parameters.           |                       |
|                       |                       |                       |
|                       | ## 4.6  Interface des |                       |
|                       | ign {#sec47 .section} |                       |
|                       |                       |                       |
|                       | The next step is to   |                       |
|                       | write                 |                       |
|                       | [circle]{.c004},      |                       |
|                       | which takes a radius, |                       |
|                       | [r]{.c004}, as a      |                       |
|                       | parameter. Here is a  |                       |
|                       | simple solution that  |                       |
|                       | uses [polygon]{.c004} |                       |
|                       | to draw a 50-sided    |                       |
|                       | polygon:              |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | import math           |                       |
|                       |                       |                       |
|                       | def circle(t, r):     |                       |
|                       |     circumfere        |                       |
|                       | nce = 2 * math.pi * r |                       |
|                       |     n = 50            |                       |
|                       |     lengt             |                       |
|                       | h = circumference / n |                       |
|                       |                       |                       |
|                       | polygon(t, n, length) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first line        |                       |
|                       | computes the          |                       |
|                       | circumference of a    |                       |
|                       | circle with radius    |                       |
|                       | [r]{.c004} using the  |                       |
|                       | formula 2 π           |                       |
|                       | [r]{.c009}. Since we  |                       |
|                       | use [math.pi]{.c004}, |                       |
|                       | we have to import     |                       |
|                       | [math]{.c004}. By     |                       |
|                       | convention,           |                       |
|                       | [import]{.c004}       |                       |
|                       | statements are        |                       |
|                       | usually at the        |                       |
|                       | beginning of the      |                       |
|                       | script.               |                       |
|                       |                       |                       |
|                       | [n]{.c004} is the     |                       |
|                       | number of line        |                       |
|                       | segments in our       |                       |
|                       | approximation of a    |                       |
|                       | circle, so            |                       |
|                       | [length]{.c004} is    |                       |
|                       | the length of each    |                       |
|                       | segment. Thus,        |                       |
|                       | [polygon]{.c004}      |                       |
|                       | draws a 50-sided      |                       |
|                       | polygon that          |                       |
|                       | approximates a circle |                       |
|                       | with radius           |                       |
|                       | [r]{.c004}.           |                       |
|                       |                       |                       |
|                       | One limitation of     |                       |
|                       | this solution is that |                       |
|                       | [n]{.c004} is a       |                       |
|                       | constant, which means |                       |
|                       | that for very big     |                       |
|                       | circles, the line     |                       |
|                       | segments are too      |                       |
|                       | long, and for small   |                       |
|                       | circles, we waste     |                       |
|                       | time drawing very     |                       |
|                       | small segments. One   |                       |
|                       | solution would be to  |                       |
|                       | generalize the        |                       |
|                       | function by taking    |                       |
|                       | [n]{.c004} as a       |                       |
|                       | parameter. This would |                       |
|                       | give the user         |                       |
|                       | (whoever calls        |                       |
|                       | [circle]{.c004}) more |                       |
|                       | control, but the      |                       |
|                       | interface would be    |                       |
|                       | less clean.           |                       |
|                       | []{#hevea_default278} |                       |
|                       |                       |                       |
|                       | The                   |                       |
|                       | [interface]{.c010} of |                       |
|                       | a function is a       |                       |
|                       | summary of how it is  |                       |
|                       | used: what are the    |                       |
|                       | parameters? What does |                       |
|                       | the function do? And  |                       |
|                       | what is the return    |                       |
|                       | value? An interface   |                       |
|                       | is "clean" if it      |                       |
|                       | allows the caller to  |                       |
|                       | do what they want     |                       |
|                       | without dealing with  |                       |
|                       | unnecessary details.  |                       |
|                       |                       |                       |
|                       | In this example,      |                       |
|                       | [r]{.c004} belongs in |                       |
|                       | the interface because |                       |
|                       | it specifies the      |                       |
|                       | circle to be drawn.   |                       |
|                       | [n]{.c004} is less    |                       |
|                       | appropriate because   |                       |
|                       | it pertains to the    |                       |
|                       | details of *how* the  |                       |
|                       | circle should be      |                       |
|                       | rendered.             |                       |
|                       |                       |                       |
|                       | Rather than clutter   |                       |
|                       | up the interface, it  |                       |
|                       | is better to choose   |                       |
|                       | an appropriate value  |                       |
|                       | of [n]{.c004}         |                       |
|                       | depending on          |                       |
|                       | [c                    |                       |
|                       | ircumference]{.c004}: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def circle(t, r):     |                       |
|                       |     circumfere        |                       |
|                       | nce = 2 * math.pi * r |                       |
|                       |     n = int(c         |                       |
|                       | ircumference / 3) + 3 |                       |
|                       |     lengt             |                       |
|                       | h = circumference / n |                       |
|                       |                       |                       |
|                       | polygon(t, n, length) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now the number of     |                       |
|                       | segments is an        |                       |
|                       | integer near          |                       |
|                       | [cir                  |                       |
|                       | cumference/3]{.c004}, |                       |
|                       | so the length of each |                       |
|                       | segment is            |                       |
|                       | approximately 3,      |                       |
|                       | which is small enough |                       |
|                       | that the circles look |                       |
|                       | good, but big enough  |                       |
|                       | to be efficient, and  |                       |
|                       | acceptable for any    |                       |
|                       | size circle.          |                       |
|                       |                       |                       |
|                       | Adding 3 to           |                       |
|                       | [n]{.c004} guarantees |                       |
|                       | that the polygon has  |                       |
|                       | at least 3 sides.     |                       |
|                       |                       |                       |
|                       | ## 4.7  Refactor      |                       |
|                       | ing {#sec48 .section} |                       |
|                       |                       |                       |
|                       | []{#refactoring}      |                       |
|                       | []{#hevea_default279} |                       |
|                       |                       |                       |
|                       | When I wrote          |                       |
|                       | [circle]{.c004}, I    |                       |
|                       | was able to re-use    |                       |
|                       | [polygon]{.c004}      |                       |
|                       | because a many-sided  |                       |
|                       | polygon is a good     |                       |
|                       | approximation of a    |                       |
|                       | circle. But           |                       |
|                       | [arc]{.c004} is not   |                       |
|                       | as cooperative; we    |                       |
|                       | can't use             |                       |
|                       | [polygon]{.c004} or   |                       |
|                       | [circle]{.c004} to    |                       |
|                       | draw an arc.          |                       |
|                       |                       |                       |
|                       | One alternative is to |                       |
|                       | start with a copy of  |                       |
|                       | [polygon]{.c004} and  |                       |
|                       | transform it into     |                       |
|                       | [arc]{.c004}. The     |                       |
|                       | result might look     |                       |
|                       | like this:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def arc(t, r, angle): |                       |
|                       |                       |                       |
|                       | arc_length = 2 * math |                       |
|                       | .pi * r * angle / 360 |                       |
|                       |     n = in            |                       |
|                       | t(arc_length / 3) + 1 |                       |
|                       |     step_le           |                       |
|                       | ngth = arc_length / n |                       |
|                       |     s                 |                       |
|                       | tep_angle = angle / n |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |    for i in range(n): |                       |
|                       |                       |                       |
|                       |     t.fd(step_length) |                       |
|                       |                       |                       |
|                       |      t.lt(step_angle) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The second half of    |                       |
|                       | this function looks   |                       |
|                       | like                  |                       |
|                       | [polygon]{.c004}, but |                       |
|                       | we can't re-use       |                       |
|                       | [polygon]{.c004}      |                       |
|                       | without changing the  |                       |
|                       | interface. We could   |                       |
|                       | generalize            |                       |
|                       | [polygon]{.c004} to   |                       |
|                       | take an angle as a    |                       |
|                       | third argument, but   |                       |
|                       | then [polygon]{.c004} |                       |
|                       | would no longer be an |                       |
|                       | appropriate name!     |                       |
|                       | Instead, let's call   |                       |
|                       | the more general      |                       |
|                       | function              |                       |
|                       | [polyline]{.c004}:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def polyline(         |                       |
|                       | t, n, length, angle): |                       |
|                       |                       |                       |
|                       |    for i in range(n): |                       |
|                       |         t.fd(length)  |                       |
|                       |         t.lt(angle)   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now we can rewrite    |                       |
|                       | [polygon]{.c004} and  |                       |
|                       | [arc]{.c004} to use   |                       |
|                       | [polyline]{.c004}:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def p                 |                       |
|                       | olygon(t, n, length): |                       |
|                       |     angle = 360.0 / n |                       |
|                       |     polyline          |                       |
|                       | (t, n, length, angle) |                       |
|                       |                       |                       |
|                       | def arc(t, r, angle): |                       |
|                       |                       |                       |
|                       | arc_length = 2 * math |                       |
|                       | .pi * r * angle / 360 |                       |
|                       |     n = in            |                       |
|                       | t(arc_length / 3) + 1 |                       |
|                       |     step_le           |                       |
|                       | ngth = arc_length / n |                       |
|                       |     step_ang          |                       |
|                       | le = float(angle) / n |                       |
|                       |                       |                       |
|                       |    polyline(t, n, ste |                       |
|                       | p_length, step_angle) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Finally, we can       |                       |
|                       | rewrite               |                       |
|                       | [circle]{.c004} to    |                       |
|                       | use [arc]{.c004}:     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def circle(t, r):     |                       |
|                       |     arc(t, r, 360)    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This                  |                       |
|                       | process---rearranging |                       |
|                       | a program to improve  |                       |
|                       | interfaces and        |                       |
|                       | facilitate code       |                       |
|                       | re-use---is called    |                       |
|                       | [refactoring]{.c010}. |                       |
|                       | In this case, we      |                       |
|                       | noticed that there    |                       |
|                       | was similar code in   |                       |
|                       | [arc]{.c004} and      |                       |
|                       | [polygon]{.c004}, so  |                       |
|                       | we "factored it out"  |                       |
|                       | into                  |                       |
|                       | [polyline]{.c004}.    |                       |
|                       | []{#hevea_default280} |                       |
|                       |                       |                       |
|                       | If we had planned     |                       |
|                       | ahead, we might have  |                       |
|                       | written               |                       |
|                       | [polyline]{.c004}     |                       |
|                       | first and avoided     |                       |
|                       | refactoring, but      |                       |
|                       | often you don't know  |                       |
|                       | enough at the         |                       |
|                       | beginning of a        |                       |
|                       | project to design all |                       |
|                       | the interfaces. Once  |                       |
|                       | you start coding, you |                       |
|                       | understand the        |                       |
|                       | problem better.       |                       |
|                       | Sometimes refactoring |                       |
|                       | is a sign that you    |                       |
|                       | have learned          |                       |
|                       | something.            |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       |  4.8  A development p |                       |
|                       | lan {#sec49 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default281} |                       |
|                       |                       |                       |
|                       | A [development        |                       |
|                       | plan]{.c010} is a     |                       |
|                       | process for writing   |                       |
|                       | programs. The process |                       |
|                       | we used in this case  |                       |
|                       | study is              |                       |
|                       | "encapsulation and    |                       |
|                       | generalization". The  |                       |
|                       | steps of this process |                       |
|                       | are:                  |                       |
|                       |                       |                       |
|                       | 1.  Start by writing  |                       |
|                       |     a small program   |                       |
|                       |     with no function  |                       |
|                       |     definitions.      |                       |
|                       | 2.  Once you get the  |                       |
|                       |     program working,  |                       |
|                       |     identify a        |                       |
|                       |     coherent piece of |                       |
|                       |     it, encapsulate   |                       |
|                       |     the piece in a    |                       |
|                       |     function and give |                       |
|                       |     it a name.        |                       |
|                       | 3.  Generalize the    |                       |
|                       |     function by       |                       |
|                       |     adding            |                       |
|                       |     appropriate       |                       |
|                       |     parameters.       |                       |
|                       | 4.  Repeat steps 1--3 |                       |
|                       |     until you have a  |                       |
|                       |     set of working    |                       |
|                       |     functions. Copy   |                       |
|                       |     and paste working |                       |
|                       |     code to avoid     |                       |
|                       |     retyping (and     |                       |
|                       |     re-debugging).    |                       |
|                       | 5.  Look for          |                       |
|                       |     opportunities to  |                       |
|                       |     improve the       |                       |
|                       |     program by        |                       |
|                       |     refactoring. For  |                       |
|                       |     example, if you   |                       |
|                       |     have similar code |                       |
|                       |     in several        |                       |
|                       |     places, consider  |                       |
|                       |     factoring it into |                       |
|                       |     an appropriately  |                       |
|                       |     general function. |                       |
|                       |                       |                       |
|                       | This process has some |                       |
|                       | drawbacks---we will   |                       |
|                       | see alternatives      |                       |
|                       | later---but it can be |                       |
|                       | useful if you don't   |                       |
|                       | know ahead of time    |                       |
|                       | how to divide the     |                       |
|                       | program into          |                       |
|                       | functions. This       |                       |
|                       | approach lets you     |                       |
|                       | design as you go      |                       |
|                       | along.                |                       |
|                       |                       |                       |
|                       | ## 4.9  docstr        |                       |
|                       | ing {#sec50 .section} |                       |
|                       |                       |                       |
|                       | []{#docstring}        |                       |
|                       | []{#hevea_default282} |                       |
|                       |                       |                       |
|                       | A [docstring]{.c010}  |                       |
|                       | is a string at the    |                       |
|                       | beginning of a        |                       |
|                       | function that         |                       |
|                       | explains the          |                       |
|                       | interface ("doc" is   |                       |
|                       | short for             |                       |
|                       | "documentation").     |                       |
|                       | Here is an example:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def polyline(         |                       |
|                       | t, n, length, angle): |                       |
|                       |     """Draws          |                       |
|                       |  n line segments with |                       |
|                       |  the given length and |                       |
|                       |     angle             |                       |
|                       | (in degrees) between  |                       |
|                       | them.  t is a turtle. |                       |
|                       |     """               |                       |
|                       |                       |                       |
|                       |    for i in range(n): |                       |
|                       |         t.fd(length)  |                       |
|                       |         t.lt(angle)   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | By convention, all    |                       |
|                       | docstrings are        |                       |
|                       | triple-quoted         |                       |
|                       | strings, also known   |                       |
|                       | as multiline strings  |                       |
|                       | because the triple    |                       |
|                       | quotes allow the      |                       |
|                       | string to span more   |                       |
|                       | than one line.        |                       |
|                       | []{#hevea_default283} |                       |
|                       | []{#hevea_default284} |                       |
|                       | []{#hevea_default285} |                       |
|                       | []{#hevea_default286} |                       |
|                       | []{#hevea_default287} |                       |
|                       |                       |                       |
|                       | It is terse, but it   |                       |
|                       | contains the          |                       |
|                       | essential information |                       |
|                       | someone would need to |                       |
|                       | use this function. It |                       |
|                       | explains concisely    |                       |
|                       | what the function     |                       |
|                       | does (without getting |                       |
|                       | into the details of   |                       |
|                       | how it does it). It   |                       |
|                       | explains what effect  |                       |
|                       | each parameter has on |                       |
|                       | the behavior of the   |                       |
|                       | function and what     |                       |
|                       | type each parameter   |                       |
|                       | should be (if it is   |                       |
|                       | not obvious).         |                       |
|                       |                       |                       |
|                       | Writing this kind of  |                       |
|                       | documentation is an   |                       |
|                       | important part of     |                       |
|                       | interface design. A   |                       |
|                       | well-designed         |                       |
|                       | interface should be   |                       |
|                       | simple to explain; if |                       |
|                       | you have a hard time  |                       |
|                       | explaining one of     |                       |
|                       | your functions, maybe |                       |
|                       | the interface could   |                       |
|                       | be improved.          |                       |
|                       |                       |                       |
|                       | ## 4.10  Debugg       |                       |
|                       | ing {#sec51 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default288} |                       |
|                       | []{#hevea_default289} |                       |
|                       |                       |                       |
|                       | An interface is like  |                       |
|                       | a contract between a  |                       |
|                       | function and a        |                       |
|                       | caller. The caller    |                       |
|                       | agrees to provide     |                       |
|                       | certain parameters    |                       |
|                       | and the function      |                       |
|                       | agrees to do certain  |                       |
|                       | work.                 |                       |
|                       |                       |                       |
|                       | For example,          |                       |
|                       | [polyline]{.c004}     |                       |
|                       | requires four         |                       |
|                       | arguments: [t]{.c004} |                       |
|                       | has to be a Turtle;   |                       |
|                       | [n]{.c004} has to be  |                       |
|                       | an integer;           |                       |
|                       | [length]{.c004}       |                       |
|                       | should be a positive  |                       |
|                       | number; and           |                       |
|                       | [angle]{.c004} has to |                       |
|                       | be a number, which is |                       |
|                       | understood to be in   |                       |
|                       | degrees.              |                       |
|                       |                       |                       |
|                       | These requirements    |                       |
|                       | are called            |                       |
|                       | [                     |                       |
|                       | preconditions]{.c010} |                       |
|                       | because they are      |                       |
|                       | supposed to be true   |                       |
|                       | before the function   |                       |
|                       | starts executing.     |                       |
|                       | Conversely,           |                       |
|                       | conditions at the end |                       |
|                       | of the function are   |                       |
|                       | [po                   |                       |
|                       | stconditions]{.c010}. |                       |
|                       | Postconditions        |                       |
|                       | include the intended  |                       |
|                       | effect of the         |                       |
|                       | function (like        |                       |
|                       | drawing line          |                       |
|                       | segments) and any     |                       |
|                       | side effects (like    |                       |
|                       | moving the Turtle or  |                       |
|                       | making other          |                       |
|                       | changes).             |                       |
|                       | []{#hevea_default290} |                       |
|                       | []{#hevea_default291} |                       |
|                       |                       |                       |
|                       | Preconditions are the |                       |
|                       | responsibility of the |                       |
|                       | caller. If the caller |                       |
|                       | violates a (properly  |                       |
|                       | documented!)          |                       |
|                       | precondition and the  |                       |
|                       | function doesn't work |                       |
|                       | correctly, the bug is |                       |
|                       | in the caller, not    |                       |
|                       | the function.         |                       |
|                       |                       |                       |
|                       | If the preconditions  |                       |
|                       | are satisfied and the |                       |
|                       | postconditions are    |                       |
|                       | not, the bug is in    |                       |
|                       | the function. If your |                       |
|                       | pre- and              |                       |
|                       | postconditions are    |                       |
|                       | clear, they can help  |                       |
|                       | with debugging.       |                       |
|                       |                       |                       |
|                       | ## 4.11  Gloss        |                       |
|                       | ary {#sec52 .section} |                       |
|                       |                       |                       |
|                       | [method:]{.c010}      |                       |
|                       | :   A function that   |                       |
|                       |     is associated     |                       |
|                       |     with an object    |                       |
|                       |     and called using  |                       |
|                       |     dot notation.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default292} |                       |
|                       |                       |                       |
|                       | [loop:]{.c010}        |                       |
|                       | :   A part of a       |                       |
|                       |     program that can  |                       |
|                       |     run repeatedly.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default293} |                       |
|                       |                       |                       |
|                       | [e                    |                       |
|                       | ncapsulation:]{.c010} |                       |
|                       | :   The process of    |                       |
|                       |     transforming a    |                       |
|                       |     sequence of       |                       |
|                       |     statements into a |                       |
|                       |     function          |                       |
|                       |     definition.       |                       |
|                       |                       |                       |
|                       | []{#hevea_default294} |                       |
|                       |                       |                       |
|                       | [ge                   |                       |
|                       | neralization:]{.c010} |                       |
|                       | :   The process of    |                       |
|                       |     replacing         |                       |
|                       |     something         |                       |
|                       |     unnecessarily     |                       |
|                       |     specific (like a  |                       |
|                       |     number) with      |                       |
|                       |     something         |                       |
|                       |     appropriately     |                       |
|                       |     general (like a   |                       |
|                       |     variable or       |                       |
|                       |     parameter).       |                       |
|                       |                       |                       |
|                       | []{#hevea_default295} |                       |
|                       |                       |                       |
|                       | [keyw                 |                       |
|                       | ord argument:]{.c010} |                       |
|                       | :   An argument that  |                       |
|                       |     includes the name |                       |
|                       |     of the parameter  |                       |
|                       |     as a "keyword".   |                       |
|                       |                       |                       |
|                       | []{#hevea_default296} |                       |
|                       |                       |                       |
|                       | []{#hevea_default297} |                       |
|                       |                       |                       |
|                       | [interface:]{.c010}   |                       |
|                       | :   A description of  |                       |
|                       |     how to use a      |                       |
|                       |     function,         |                       |
|                       |     including the     |                       |
|                       |     name and          |                       |
|                       |     descriptions of   |                       |
|                       |     the arguments and |                       |
|                       |     return value.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default298} |                       |
|                       |                       |                       |
|                       | [refactoring:]{.c010} |                       |
|                       | :   The process of    |                       |
|                       |     modifying a       |                       |
|                       |     working program   |                       |
|                       |     to improve        |                       |
|                       |     function          |                       |
|                       |     interfaces and    |                       |
|                       |     other qualities   |                       |
|                       |     of the code.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default299} |                       |
|                       |                       |                       |
|                       | [deve                 |                       |
|                       | lopment plan:]{.c010} |                       |
|                       | :   A process for     |                       |
|                       |     writing programs. |                       |
|                       |                       |                       |
|                       | []{#hevea_default300} |                       |
|                       |                       |                       |
|                       | [docstring:]{.c010}   |                       |
|                       | :   A string that     |                       |
|                       |     appears at the    |                       |
|                       |     top of a function |                       |
|                       |     definition to     |                       |
|                       |     document the      |                       |
|                       |     function's        |                       |
|                       |     interface.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default301} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | precondition:]{.c010} |                       |
|                       | :   A requirement     |                       |
|                       |     that should be    |                       |
|                       |     satisfied by the  |                       |
|                       |     caller before a   |                       |
|                       |     function starts.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default302} |                       |
|                       |                       |                       |
|                       | [p                    |                       |
|                       | ostcondition:]{.c010} |                       |
|                       | :   A requirement     |                       |
|                       |     that should be    |                       |
|                       |     satisfied by the  |                       |
|                       |     function before   |                       |
|                       |     it ends.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default303} |                       |
|                       |                       |                       |
|                       | ## 4.12  Exerci       |                       |
|                       | ses {#sec53 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Download the code in |                       |
|                       | this chapter from*    |                       |
|                       | [*[https://t          |                       |
|                       | hinkpython.com/code/p |                       |
|                       | olygon.py]{.c004}*](h |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/polygon.py)*.* |                       |
|                       |                       |                       |
|                       | 1.  *Draw a stack     |                       |
|                       |     diagram that      |                       |
|                       |     shows the state   |                       |
|                       |     of the program    |                       |
|                       |     while executing   |                       |
|                       |     [circle(bob,      |                       |
|                       |     radius)]{.c004}.  |                       |
|                       |     You can do the    |                       |
|                       |     arithmetic by     |                       |
|                       |     hand or add       |                       |
|                       |     [print]{.c004}    |                       |
|                       |     statements to the |                       |
|                       |     code.*            |                       |
|                       |                       |                       |
|                       | []{#hevea_default304} |                       |
|                       | 2.  *The version of   |                       |
|                       |     [arc]{.c004} in   |                       |
|                       |     Section *         |                       |
|                       | [*4.7*](#refactoring) |                       |
|                       |     *is not very      |                       |
|                       |     accurate because  |                       |
|                       |     the linear        |                       |
|                       |     approximation of  |                       |
|                       |     the circle is     |                       |
|                       |     always outside    |                       |
|                       |     the true circle.  |                       |
|                       |     As a result, the  |                       |
|                       |     Turtle ends up a  |                       |
|                       |     few pixels away   |                       |
|                       |     from the correct  |                       |
|                       |     destination. My   |                       |
|                       |     solution shows a  |                       |
|                       |     way to reduce the |                       |
|                       |     effect of this    |                       |
|                       |     error. Read the   |                       |
|                       |     code and see if   |                       |
|                       |     it makes sense to |                       |
|                       |     you. If you draw  |                       |
|                       |     a diagram, you    |                       |
|                       |     might see how it  |                       |
|                       |     works.*           |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2003.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  4.1: Turtle flowers. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.flowers}    |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#hevea_default305} |                       |
|                       |                       |                       |
|                       | *Write an             |                       |
|                       | appropriately general |                       |
|                       | set of functions that |                       |
|                       | can draw flowers as   |                       |
|                       | in                    |                       |
|                       | Figure *[*4           |                       |
|                       | .1*](#fig.flowers)*.* |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[https:             |                       |
|                       | //thinkpython.com/cod |                       |
|                       | e/flower.py]{.c004}*] |                       |
|                       | (https://thinkpython. |                       |
|                       | com/code/flower.py)*, |                       |
|                       | also requires*        |                       |
|                       | [*[https://t          |                       |
|                       | hinkpython.com/code/p |                       |
|                       | olygon.py]{.c004}*](h |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/polygon.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2004.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -----             |                       |
|                       | --------------------- |                       |
|                       | >   Fig               |                       |
|                       | ure 4.2: Turtle pies. |                       |
|                       | >   -----             |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.pies}       |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       | []{#hevea_default306} |                       |
|                       |                       |                       |
|                       | *Write an             |                       |
|                       | appropriately general |                       |
|                       | set of functions that |                       |
|                       | can draw shapes as in |                       |
|                       | Figure *              |                       |
|                       | [*4.2*](#fig.pies)*.* |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[h                  |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/pie.py]{.c004} |                       |
|                       | *](https://thinkpytho |                       |
|                       | n.com/code/pie.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 4]{.c010}   |                       |
|                       | []{#hevea_default307} |                       |
|                       | []{#hevea_default308} |                       |
|                       | []{#hevea_default309} |                       |
|                       |                       |                       |
|                       | *The letters of the   |                       |
|                       | alphabet can be       |                       |
|                       | constructed from a    |                       |
|                       | moderate number of    |                       |
|                       | basic elements, like  |                       |
|                       | vertical and          |                       |
|                       | horizontal lines and  |                       |
|                       | a few curves. Design  |                       |
|                       | an alphabet that can  |                       |
|                       | be drawn with a       |                       |
|                       | minimal number of     |                       |
|                       | basic elements and    |                       |
|                       | then write functions  |                       |
|                       | that draw the         |                       |
|                       | letters.*             |                       |
|                       |                       |                       |
|                       | *You should write one |                       |
|                       | function for each     |                       |
|                       | letter, with names    |                       |
|                       | `draw_a`, `draw_b`,   |                       |
|                       | etc., and put your    |                       |
|                       | functions in a file   |                       |
|                       | named                 |                       |
|                       | [letters.py]{.c004}.  |                       |
|                       | You can download a    |                       |
|                       | "turtle typewriter"   |                       |
|                       | from*                 |                       |
|                       | [[*https://thin       |                       |
|                       | kpython.com/code/type |                       |
|                       | writer.py*]{.c004}](h |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/typewriter.py) |                       |
|                       | *to help you test     |                       |
|                       | your code.*           |                       |
|                       |                       |                       |
|                       | *You can get a        |                       |
|                       | solution from*        |                       |
|                       | [*[https://           |                       |
|                       | thinkpython.com/code/ |                       |
|                       | letters.py]{.c004}*]( |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/letters.py)*; |                       |
|                       | it also requires*     |                       |
|                       | [*[https://t          |                       |
|                       | hinkpython.com/code/p |                       |
|                       | olygon.py]{.c004}*](h |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/polygon.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       |                       |                       |
|                       | *Read about spirals   |                       |
|                       | at*                   |                       |
|                       | [[*                   |                       |
|                       | http://en.wikipedia.o |                       |
|                       | rg/wiki/Spiral*]{.c00 |                       |
|                       | 4}](http://en.wikiped |                       |
|                       | ia.org/wiki/Spiral)*; |                       |
|                       | then write a program  |                       |
|                       | that draws an         |                       |
|                       | Archimedian spiral    |                       |
|                       | (or one of the other  |                       |
|                       | kinds). Solution:*    |                       |
|                       | [[*https:/            |                       |
|                       | /thinkpython.com/code |                       |
|                       | /spiral.py*]{.c004}]( |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/spiral.py)*.* |                       |
|                       | []{#hevea_default310} |                       |
|                       | []{#hevea_default311} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2004.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2006.html)
---
generator: hevea 2.32
title: Conditionals and recursion
---

[![Previous](back.png)](thinkpython2005.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2007.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 5  Co       | to support my books,  |
|                       | nditionals and recurs | you can use the       |
|                       | ion {#sec54 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | The main topic of     | you!                  |
|                       | this chapter is the   |                       |
|                       | [if]{.c004}           |   -----------         |
|                       | statement, which      | --------------------- |
|                       | executes different    | --------------------- |
|                       | code depending on the | --------------------- |
|                       | state of the program. | --------------------- |
|                       | But first I want to   |   Pay what you want:  |
|                       | introduce two new     |   Small \$1           |
|                       | operators: floor      | .00 USD Medium \$5.00 |
|                       | division and modulus. |  USD Large \$10.00 US |
|                       |                       | D X-Large \$20.00 USD |
|                       | ## 5.1  Fl            |  XX-Large \$50.00 USD |
|                       | oor division and modu |   -----------         |
|                       | lus {#sec55 .section} | --------------------- |
|                       |                       | --------------------- |
|                       | The [floor            | --------------------- |
|                       | division]{.c010}      | --------------------- |
|                       | operator, `//`,       |                       |
|                       | divides two numbers   | ![](                  |
|                       | and rounds down to an | https://www.paypalobj |
|                       | integer. For example, | ects.com/en_US/i/scr/ |
|                       | suppose the run time  | pixel.gif){border="0" |
|                       | of a movie is 105     | width="1" height="1"} |
|                       | minutes. You might    |                       |
|                       | want to know how long | ####                  |
|                       | that is in hours.     | Are you using one of  |
|                       | Conventional division | our books in a class? |
|                       | returns a             |                       |
|                       | floating-point        | We\'d like to know    |
|                       | number:               | about it. Please      |
|                       |                       | consider filling out  |
|                       | ``` verbatim          | [this short           |
|                       | >>> minutes = 105     | survey](http://s      |
|                       | >>> minutes / 60      | preadsheets.google.co |
|                       | 1.75                  | m/viewform?formkey=dC |
|                       | ```                   | 0tNUZkMjBEdXVoRGljNm9 |
|                       |                       | FRmlTMHc6MA){onclick= |
|                       | But we don't normally | "javascript: pageTrac |
|                       | write hours with      | ker._trackPageview('/ |
|                       | decimal points. Floor | outbound/survey');"}. |
|                       | division returns the  |                       |
|                       | integer number of     | \                     |
|                       | hours, rounding down: |                       |
|                       |                       | [Think                |
|                       | ``` verbatim          | DSP](http             |
|                       | >>> minutes = 105     | ://www.amazon.com/gp/ |
|                       | >>>                   | product/1491938455/re |
|                       | hours = minutes // 60 | f=as_li_tl?ie=UTF8&ca |
|                       | >>> hours             | mp=1789&creative=9325 |
|                       | 1                     | &creativeASIN=1491938 |
|                       | ```                   | 455&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | To get the remainder, | Id=2JJH4SWCAVVYSQHO){ |
|                       | you could subtract    | rel="nofollow"}![](ht |
|                       | off one hour in       | tp://ir-na.amazon-ads |
|                       | minutes:              | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1491938455){.c003 |
|                       | >>> remainder =       | width="1" height="1"  |
|                       |  minutes - hours * 60 | border="0"}           |
|                       | >>> remainder         |                       |
|                       | 45                    | [                     |
|                       | ```                   | ![](http://ws-na.amaz |
|                       |                       | on-adsystem.com/widge |
|                       | []{#hevea_default312} | ts/q?_encoding=UTF8&A |
|                       | []{#hevea_default313} | SIN=1491938455&Format |
|                       | []{#hevea_default314} | =_SL160_&ID=AsinImage |
|                       | []{#hevea_default315} | &MarketPlace=US&Servi |
|                       | []{#hevea_default316} | ceVersion=20070822&WS |
|                       | []{#hevea_default317} | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | An alternative is to  | ://www.amazon.com/gp/ |
|                       | use the [modulus      | product/1491938455/re |
|                       | operator]{.c010},     | f=as_li_tl?ie=UTF8&ca |
|                       | `%`, which divides    | mp=1789&creative=9325 |
|                       | two numbers and       | &creativeASIN=1491938 |
|                       | returns the           | 455&linkCode=as2&tag= |
|                       | remainder.            | greenteapre01-20&link |
|                       |                       | Id=CTV7PDT7E5EGGJUM){ |
|                       | ``` verbatim          | rel="nofollow"}![](ht |
|                       | >>> rem               | tp://ir-na.amazon-ads |
|                       | ainder = minutes % 60 | ystem.com/e/ir?t=gree |
|                       | >>> remainder         | nteapre01-20&l=as2&o= |
|                       | 45                    | 1&a=1491938455){.c003 |
|                       | ```                   | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The modulus operator  |                       |
|                       | is more useful than   | [Think                |
|                       | it seems. For         | Java](http            |
|                       | example, you can      | ://www.amazon.com/gp/ |
|                       | check whether one     | product/1491929561/re |
|                       | number is divisible   | f=as_li_tl?ie=UTF8&ca |
|                       | by another---if [x %  | mp=1789&creative=9325 |
|                       | y]{.c004} is zero,    | &creativeASIN=1491929 |
|                       | then [x]{.c004} is    | 561&linkCode=as2&tag= |
|                       | divisible by          | greenteapre01-20&link |
|                       | [y]{.c004}.           | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | []{#hevea_default318} | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | Also, you can extract | ystem.com/e/ir?t=gree |
|                       | the right-most digit  | nteapre01-20&l=as2&o= |
|                       | or digits from a      | 1&a=1491929561){.c003 |
|                       | number. For example,  | width="1" height="1"  |
|                       | [x % 10]{.c004}       | border="0"}           |
|                       | yields the right-most |                       |
|                       | digit of [x]{.c004}   | [                     |
|                       | (in base 10).         | ![](http://ws-na.amaz |
|                       | Similarly [x %        | on-adsystem.com/widge |
|                       | 100]{.c004} yields    | ts/q?_encoding=UTF8&A |
|                       | the last two digits.  | SIN=1491929561&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | If you are using      | &MarketPlace=US&Servi |
|                       | Python 2, division    | ceVersion=20070822&WS |
|                       | works differently.    | =1&tag=greenteapre01- |
|                       | The division          | 20){border="0"}](http |
|                       | operator, `/`,        | ://www.amazon.com/gp/ |
|                       | performs floor        | product/1491929561/re |
|                       | division if both      | f=as_li_tl?ie=UTF8&ca |
|                       | operands are          | mp=1789&creative=9325 |
|                       | integers, and         | &creativeASIN=1491929 |
|                       | floating-point        | 561&linkCode=as2&tag= |
|                       | division if either    | greenteapre01-20&link |
|                       | operand is a          | Id=PT77ANWARUNNU3UK){ |
|                       | [float]{.c004}.       | rel="nofollow"}![](ht |
|                       | []{#hevea_default319} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | ##                    | nteapre01-20&l=as2&o= |
|                       | 5.2  Boolean expressi | 1&a=1491929561){.c003 |
|                       | ons {#sec56 .section} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | []{#hevea_default320} |                       |
|                       | []{#hevea_default321} | [Think                |
|                       | []{#hevea_default322} | Bay                   |
|                       | []{#hevea_default323} | es](http://www.amazon |
|                       |                       | .com/gp/product/14493 |
|                       | A [boolean            | 70780/ref=as_li_qf_sp |
|                       | expression]{.c010} is | _asin_tl?ie=UTF8&camp |
|                       | an expression that is | =1789&creative=9325&c |
|                       | either true or false. | reativeASIN=144937078 |
|                       | The following         | 0&linkCode=as2&tag=gr |
|                       | examples use the      | eenteapre01-20)![](ht |
|                       | operator [==]{.c004}, | tp://ir-na.amazon-ads |
|                       | which compares two    | ystem.com/e/ir?t=gree |
|                       | operands and produces | nteapre01-20&l=as2&o= |
|                       | [True]{.c004} if they | 1&a=1449370780){.c003 |
|                       | are equal and         | width="1" height="1"  |
|                       | [False]{.c004}        | border="0"}           |
|                       | otherwise:            |                       |
|                       |                       | [![](http://ws        |
|                       | ``` verbatim          | -na.amazon-adsystem.c |
|                       | >>> 5 == 5            | om/widgets/q?_encodin |
|                       | True                  | g=UTF8&ASIN=144937078 |
|                       | >>> 5 == 6            | 0&Format=_SL160_&ID=A |
|                       | False                 | sinImage&MarketPlace= |
|                       | ```                   | US&ServiceVersion=200 |
|                       |                       | 70822&WS=1&tag=greent |
|                       | [True]{.c004} and     | eapre01-20){border="0 |
|                       | [False]{.c004} are    | "}](http://www.amazon |
|                       | special values that   | .com/gp/product/14493 |
|                       | belong to the type    | 70780/ref=as_li_qf_sp |
|                       | [bool]{.c004}; they   | _asin_il?ie=UTF8&camp |
|                       | are not strings:      | =1789&creative=9325&c |
|                       | []{#hevea_default324} | reativeASIN=144937078 |
|                       | []{#hevea_default325} | 0&linkCode=as2&tag=gr |
|                       | []{#hevea_default326} | eenteapre01-20)![](ht |
|                       | []{#hevea_default327} | tp://ir-na.amazon-ads |
|                       | []{#hevea_default328} | ystem.com/e/ir?t=gree |
|                       | []{#hevea_default329} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1449370780){.c003 |
|                       | ``` verbatim          | width="1" height="1"  |
|                       | >>> type(True)        | border="0"}           |
|                       | <class 'bool'>        |                       |
|                       | >>> type(False)       | [Think Python         |
|                       | <class 'bool'>        | 2e](http              |
|                       | ```                   | ://www.amazon.com/gp/ |
|                       |                       | product/1491939362/re |
|                       | The [==]{.c004}       | f=as_li_tl?ie=UTF8&ca |
|                       | operator is one of    | mp=1789&creative=9325 |
|                       | the [relational       | &creativeASIN=1491939 |
|                       | operators]{.c010};    | 362&linkCode=as2&tag= |
|                       | the others are:       | greenteapre01-20&link |
|                       |                       | Id=FJKSQ3IHEMY2F2VA){ |
|                       | ``` verbatim          | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | x != y                | ystem.com/e/ir?t=gree |
|                       | # x is not equal to y | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | x > y                 | width="1" height="1"  |
|                       | # x is greater than y | border="0"}           |
|                       |                       |                       |
|                       |    x < y              | [                     |
|                       |    # x is less than y | ![](http://ws-na.amaz |
|                       |       x >= y          | on-adsystem.com/widge |
|                       |          # x is great | ts/q?_encoding=UTF8&A |
|                       | er than or equal to y | SIN=1491939362&Format |
|                       |       x <= y          | =_SL160_&ID=AsinImage |
|                       |             # x is le | &MarketPlace=US&Servi |
|                       | ss than or equal to y | ceVersion=20070822&WS |
|                       | ```                   | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | Although these        | ://www.amazon.com/gp/ |
|                       | operations are        | product/1491939362/re |
|                       | probably familiar to  | f=as_li_tl?ie=UTF8&ca |
|                       | you, the Python       | mp=1789&creative=9325 |
|                       | symbols are different | &creativeASIN=1491939 |
|                       | from the mathematical | 362&linkCode=as2&tag= |
|                       | symbols. A common     | greenteapre01-20&link |
|                       | error is to use a     | Id=ZZ454DLQ3IXDHNHX){ |
|                       | single equal sign     | rel="nofollow"}![](ht |
|                       | ([=]{.c004}) instead  | tp://ir-na.amazon-ads |
|                       | of a double equal     | ystem.com/e/ir?t=gree |
|                       | sign ([==]{.c004}).   | nteapre01-20&l=as2&o= |
|                       | Remember that         | 1&a=1491939362){.c003 |
|                       | [=]{.c004} is an      | width="1" height="1"  |
|                       | assignment operator   | border="0"}           |
|                       | and [==]{.c004} is a  |                       |
|                       | relational operator.  | [Think Stats          |
|                       | There is no such      | 2e](http://ww         |
|                       | thing as [=\<]{.c004} | w.amazon.com/gp/produ |
|                       | or [=\>]{.c004}.      | ct/1491907339/ref=as_ |
|                       | []{#hevea_default330} | li_tl?ie=UTF8&camp=17 |
|                       | []{#hevea_default331} | 89&creative=9325&crea |
|                       |                       | tiveASIN=1491907339&l |
|                       | #                     | inkCode=as2&tag=green |
|                       | # 5.3  Logical operat | teapre01-20&linkId=O7 |
|                       | ors {#sec57 .section} | WYM6H6YBYUFNWU)![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | []{#hevea_default332} | ystem.com/e/ir?t=gree |
|                       | []{#hevea_default333} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491907339){.c003 |
|                       | There are three       | width="1" height="1"  |
|                       | [logical              | border="0"}           |
|                       | operators]{.c010}:    |                       |
|                       | [and]{.c004},         | [![](h                |
|                       | [or]{.c004}, and      | ttp://ws-na.amazon-ad |
|                       | [not]{.c004}. The     | system.com/widgets/q? |
|                       | semantics (meaning)   | _encoding=UTF8&ASIN=1 |
|                       | of these operators is | 491907339&Format=_SL1 |
|                       | similar to their      | 60_&ID=AsinImage&Mark |
|                       | meaning in English.   | etPlace=US&ServiceVer |
|                       | For example, [x \> 0  | sion=20070822&WS=1&ta |
|                       | and x \< 10]{.c004}   | g=greenteapre01-20){b |
|                       | is true only if       | order="0"}](http://ww |
|                       | [x]{.c004} is greater | w.amazon.com/gp/produ |
|                       | than 0 *and* less     | ct/1491907339/ref=as_ |
|                       | than 10.              | li_tl?ie=UTF8&camp=17 |
|                       | []{#hevea_default334} | 89&creative=9325&crea |
|                       | []{#hevea_default335} | tiveASIN=1491907339&l |
|                       | []{#hevea_default336} | inkCode=as2&tag=green |
|                       | []{#hevea_default337} | teapre01-20&linkId=JV |
|                       | []{#hevea_default338} | SYKQHYSUIEYRHL)![](ht |
|                       | []{#hevea_default339} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | [n%2 == 0 or n%3 ==   | nteapre01-20&l=as2&o= |
|                       | 0]{.c004} is true if  | 1&a=1491907339){.c003 |
|                       | *either or both* of   | width="1" height="1"  |
|                       | the conditions is     | border="0"}           |
|                       | true, that is, if the |                       |
|                       | number is divisible   | [Think                |
|                       | by 2 *or* 3.          | Complexity](http      |
|                       |                       | ://www.amazon.com/gp/ |
|                       | Finally, the          | product/1449314635/re |
|                       | [not]{.c004} operator | f=as_li_tf_tl?ie=UTF8 |
|                       | negates a boolean     | &tag=greenteapre01-20 |
|                       | expression, so [not   | &linkCode=as2&camp=17 |
|                       | (x \> y)]{.c004} is   | 89&creative=9325&crea |
|                       | true if [x \>         | tiveASIN=1449314635)! |
|                       | y]{.c004} is false,   | [](http://www.assoc-a |
|                       | that is, if           | mazon.com/e/ir?t=gree |
|                       | [x]{.c004} is less    | nteapre01-20&l=as2&o= |
|                       | than or equal to      | 1&a=1449314635){.c003 |
|                       | [y]{.c004}.           | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | Strictly speaking,    |                       |
|                       | the operands of the   | [                     |
|                       | logical operators     | ![](http://ws-na.amaz |
|                       | should be boolean     | on-adsystem.com/widge |
|                       | expressions, but      | ts/q?_encoding=UTF8&A |
|                       | Python is not very    | SIN=1449314635&Format |
|                       | strict. Any nonzero   | =_SL160_&ID=AsinImage |
|                       | number is interpreted | &MarketPlace=US&Servi |
|                       | as [True]{.c004}:     | ceVersion=20070822&WS |
|                       |                       | =1&tag=greenteapre01- |
|                       | ``` verbatim          | 20){border="0"}](http |
|                       | >>> 42 and True       | ://www.amazon.com/gp/ |
|                       | True                  | product/1449314635/re |
|                       | ```                   | f=as_li_tf_il?ie=UTF8 |
|                       |                       | &camp=1789&creative=9 |
|                       | This flexibility can  | 325&creativeASIN=1449 |
|                       | be useful, but there  | 314635&linkCode=as2&t |
|                       | are some subtleties   | ag=greenteapre01-20)! |
|                       | to it that might be   | [](http://www.assoc-a |
|                       | confusing. You might  | mazon.com/e/ir?t=gree |
|                       | want to avoid it      | nteapre01-20&l=as2&o= |
|                       | (unless you know what | 1&a=1449314635){.c003 |
|                       | you are doing).       | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | ## 5.                 |                       |
|                       | 4  Conditional execut |                       |
|                       | ion {#sec58 .section} |                       |
|                       |                       |                       |
|                       | []{#c                 |                       |
|                       | onditional.execution} |                       |
|                       |                       |                       |
|                       | []{#hevea_default340} |                       |
|                       | []{#hevea_default341} |                       |
|                       | []{#hevea_default342} |                       |
|                       | []{#hevea_default343} |                       |
|                       | []{#hevea_default344} |                       |
|                       | In order to write     |                       |
|                       | useful programs, we   |                       |
|                       | almost always need    |                       |
|                       | the ability to check  |                       |
|                       | conditions and change |                       |
|                       | the behavior of the   |                       |
|                       | program accordingly.  |                       |
|                       | [Conditional          |                       |
|                       | statements]{.c010}    |                       |
|                       | give us this ability. |                       |
|                       | The simplest form is  |                       |
|                       | the [if]{.c004}       |                       |
|                       | statement:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if x > 0:             |                       |
|                       |     p                 |                       |
|                       | rint('x is positive') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The boolean           |                       |
|                       | expression after      |                       |
|                       | [if]{.c004} is called |                       |
|                       | the                   |                       |
|                       | [condition]{.c010}.   |                       |
|                       | If it is true, the    |                       |
|                       | indented statement    |                       |
|                       | runs. If not, nothing |                       |
|                       | happens.              |                       |
|                       | []{#hevea_default345} |                       |
|                       | []{#hevea_default346} |                       |
|                       | []{#hevea_default347} |                       |
|                       |                       |                       |
|                       | [if]{.c004}           |                       |
|                       | statements have the   |                       |
|                       | same structure as     |                       |
|                       | function definitions: |                       |
|                       | a header followed by  |                       |
|                       | an indented body.     |                       |
|                       | Statements like this  |                       |
|                       | are called [compound  |                       |
|                       | statements]{.c010}.   |                       |
|                       |                       |                       |
|                       | There is no limit on  |                       |
|                       | the number of         |                       |
|                       | statements that can   |                       |
|                       | appear in the body,   |                       |
|                       | but there has to be   |                       |
|                       | at least one.         |                       |
|                       | Occasionally, it is   |                       |
|                       | useful to have a body |                       |
|                       | with no statements    |                       |
|                       | (usually as a place   |                       |
|                       | keeper for code you   |                       |
|                       | haven't written yet). |                       |
|                       | In that case, you can |                       |
|                       | use the [pass]{.c004} |                       |
|                       | statement, which does |                       |
|                       | nothing.              |                       |
|                       | []{#hevea_default348} |                       |
|                       | []{#hevea_default349} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if x < 0:             |                       |
|                       |     pass              |                       |
|                       |    # TODO: need to ha |                       |
|                       | ndle negative values! |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 5.                 |                       |
|                       | 5  Alternative execut |                       |
|                       | ion {#sec59 .section} |                       |
|                       |                       |                       |
|                       | []{#a                 |                       |
|                       | lternative.execution} |                       |
|                       | []{#hevea_default350} |                       |
|                       | []{#hevea_default351} |                       |
|                       | []{#hevea_default352} |                       |
|                       |                       |                       |
|                       | A second form of the  |                       |
|                       | [if]{.c004} statement |                       |
|                       | is "alternative       |                       |
|                       | execution", in which  |                       |
|                       | there are two         |                       |
|                       | possibilities and the |                       |
|                       | condition determines  |                       |
|                       | which one runs. The   |                       |
|                       | syntax looks like     |                       |
|                       | this:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if x % 2 == 0:        |                       |
|                       |                       |                       |
|                       |    print('x is even') |                       |
|                       | else:                 |                       |
|                       |     print('x is odd') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If the remainder when |                       |
|                       | [x]{.c004} is divided |                       |
|                       | by 2 is 0, then we    |                       |
|                       | know that [x]{.c004}  |                       |
|                       | is even, and the      |                       |
|                       | program displays an   |                       |
|                       | appropriate message.  |                       |
|                       | If the condition is   |                       |
|                       | false, the second set |                       |
|                       | of statements runs.   |                       |
|                       | Since the condition   |                       |
|                       | must be true or       |                       |
|                       | false, exactly one of |                       |
|                       | the alternatives will |                       |
|                       | run. The alternatives |                       |
|                       | are called            |                       |
|                       | [branches]{.c010},    |                       |
|                       | because they are      |                       |
|                       | branches in the flow  |                       |
|                       | of execution.         |                       |
|                       | []{#hevea_default353} |                       |
|                       |                       |                       |
|                       | ## 5                  |                       |
|                       | .6  Chained condition |                       |
|                       | als {#sec60 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default354} |                       |
|                       | []{#hevea_default355} |                       |
|                       |                       |                       |
|                       | Sometimes there are   |                       |
|                       | more than two         |                       |
|                       | possibilities and we  |                       |
|                       | need more than two    |                       |
|                       | branches. One way to  |                       |
|                       | express a computation |                       |
|                       | like that is a        |                       |
|                       | [chained              |                       |
|                       | conditional]{.c010}:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if x < y:             |                       |
|                       |     prin              |                       |
|                       | t('x is less than y') |                       |
|                       | elif x > y:           |                       |
|                       |     print('           |                       |
|                       | x is greater than y') |                       |
|                       | else:                 |                       |
|                       |     print             |                       |
|                       | ('x and y are equal') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [elif]{.c004} is an   |                       |
|                       | abbreviation of "else |                       |
|                       | if". Again, exactly   |                       |
|                       | one branch will run.  |                       |
|                       | There is no limit on  |                       |
|                       | the number of         |                       |
|                       | [elif]{.c004}         |                       |
|                       | statements. If there  |                       |
|                       | is an [else]{.c004}   |                       |
|                       | clause, it has to be  |                       |
|                       | at the end, but there |                       |
|                       | doesn't have to be    |                       |
|                       | one.                  |                       |
|                       | []{#hevea_default356} |                       |
|                       | []{#hevea_default357} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if choice == 'a':     |                       |
|                       |     draw_a()          |                       |
|                       | elif choice == 'b':   |                       |
|                       |     draw_b()          |                       |
|                       | elif choice == 'c':   |                       |
|                       |     draw_c()          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Each condition is     |                       |
|                       | checked in order. If  |                       |
|                       | the first is false,   |                       |
|                       | the next is checked,  |                       |
|                       | and so on. If one of  |                       |
|                       | them is true, the     |                       |
|                       | corresponding branch  |                       |
|                       | runs and the          |                       |
|                       | statement ends. Even  |                       |
|                       | if more than one      |                       |
|                       | condition is true,    |                       |
|                       | only the first true   |                       |
|                       | branch runs.          |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 5.7  Nested condition |                       |
|                       | als {#sec61 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default358} |                       |
|                       | []{#hevea_default359} |                       |
|                       |                       |                       |
|                       | One conditional can   |                       |
|                       | also be nested within |                       |
|                       | another. We could     |                       |
|                       | have written the      |                       |
|                       | example in the        |                       |
|                       | previous section like |                       |
|                       | this:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if x == y:            |                       |
|                       |     print             |                       |
|                       | ('x and y are equal') |                       |
|                       | else:                 |                       |
|                       |     if x < y:         |                       |
|                       |         prin          |                       |
|                       | t('x is less than y') |                       |
|                       |     else:             |                       |
|                       |         print('       |                       |
|                       | x is greater than y') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The outer conditional |                       |
|                       | contains two          |                       |
|                       | branches. The first   |                       |
|                       | branch contains a     |                       |
|                       | simple statement. The |                       |
|                       | second branch         |                       |
|                       | contains another      |                       |
|                       | [if]{.c004}           |                       |
|                       | statement, which has  |                       |
|                       | two branches of its   |                       |
|                       | own. Those two        |                       |
|                       | branches are both     |                       |
|                       | simple statements,    |                       |
|                       | although they could   |                       |
|                       | have been conditional |                       |
|                       | statements as well.   |                       |
|                       |                       |                       |
|                       | Although the          |                       |
|                       | indentation of the    |                       |
|                       | statements makes the  |                       |
|                       | structure apparent,   |                       |
|                       | [nested               |                       |
|                       | conditionals]{.c010}  |                       |
|                       | become difficult to   |                       |
|                       | read very quickly. It |                       |
|                       | is a good idea to     |                       |
|                       | avoid them when you   |                       |
|                       | can.                  |                       |
|                       |                       |                       |
|                       | Logical operators     |                       |
|                       | often provide a way   |                       |
|                       | to simplify nested    |                       |
|                       | conditional           |                       |
|                       | statements. For       |                       |
|                       | example, we can       |                       |
|                       | rewrite the following |                       |
|                       | code using a single   |                       |
|                       | conditional:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if 0 < x:             |                       |
|                       |     if x < 10:        |                       |
|                       |         pri           |                       |
|                       | nt('x is a positive s |                       |
|                       | ingle-digit number.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [print]{.c004}    |                       |
|                       | statement runs only   |                       |
|                       | if we make it past    |                       |
|                       | both conditionals, so |                       |
|                       | we can get the same   |                       |
|                       | effect with the       |                       |
|                       | [and]{.c004}          |                       |
|                       | operator:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if 0 < x and x < 10:  |                       |
|                       |     pri               |                       |
|                       | nt('x is a positive s |                       |
|                       | ingle-digit number.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | For this kind of      |                       |
|                       | condition, Python     |                       |
|                       | provides a more       |                       |
|                       | concise option:       |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if 0 < x < 10:        |                       |
|                       |     pri               |                       |
|                       | nt('x is a positive s |                       |
|                       | ingle-digit number.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 5.8  Recurs        |                       |
|                       | ion {#sec62 .section} |                       |
|                       |                       |                       |
|                       | []{#recursion}        |                       |
|                       | []{#hevea_default360} |                       |
|                       |                       |                       |
|                       | It is legal for one   |                       |
|                       | function to call      |                       |
|                       | another; it is also   |                       |
|                       | legal for a function  |                       |
|                       | to call itself. It    |                       |
|                       | may not be obvious    |                       |
|                       | why that is a good    |                       |
|                       | thing, but it turns   |                       |
|                       | out to be one of the  |                       |
|                       | most magical things a |                       |
|                       | program can do. For   |                       |
|                       | example, look at the  |                       |
|                       | following function:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def countdown(n):     |                       |
|                       |     if n <= 0:        |                       |
|                       |                       |                       |
|                       |    print('Blastoff!') |                       |
|                       |     else:             |                       |
|                       |         print(n)      |                       |
|                       |                       |                       |
|                       |        countdown(n-1) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If [n]{.c004} is 0 or |                       |
|                       | negative, it outputs  |                       |
|                       | the word, "Blastoff!" |                       |
|                       | Otherwise, it outputs |                       |
|                       | [n]{.c004} and then   |                       |
|                       | calls a function      |                       |
|                       | named                 |                       |
|                       | [countdown]{.c00      |                       |
|                       | 4}---itself---passing |                       |
|                       | [n-1]{.c004} as an    |                       |
|                       | argument.             |                       |
|                       |                       |                       |
|                       | What happens if we    |                       |
|                       | call this function    |                       |
|                       | like this?            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> countdown(3)      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The execution of      |                       |
|                       | [countdown]{.c004}    |                       |
|                       | begins with           |                       |
|                       | [n=3]{.c004}, and     |                       |
|                       | since [n]{.c004} is   |                       |
|                       | greater than 0, it    |                       |
|                       | outputs the value 3,  |                       |
|                       | and then calls        |                       |
|                       | itself\...            |                       |
|                       |                       |                       |
|                       | > The execution of    |                       |
|                       | > [countdown]{.c004}  |                       |
|                       | > begins with         |                       |
|                       | > [n=2]{.c004}, and   |                       |
|                       | > since [n]{.c004} is |                       |
|                       | > greater than 0, it  |                       |
|                       | > outputs the value   |                       |
|                       | > 2, and then calls   |                       |
|                       | > itself\...          |                       |
|                       | >                     |                       |
|                       | > > The execution of  |                       |
|                       | >                     |                       |
|                       |  > [countdown]{.c004} |                       |
|                       | > > begins with       |                       |
|                       | > > [n=1]{.c004}, and |                       |
|                       | > > since [n]{.c004}  |                       |
|                       | > > is greater than   |                       |
|                       | > > 0, it outputs the |                       |
|                       | > > value 1, and then |                       |
|                       | > > calls itself\...  |                       |
|                       | > >                   |                       |
|                       | > > > The execution   |                       |
|                       | > > > of              |                       |
|                       | > >                   |                       |
|                       |  > [countdown]{.c004} |                       |
|                       | > > > begins with     |                       |
|                       | > > > [n=0]{.c004},   |                       |
|                       | > > > and since       |                       |
|                       | > > > [n]{.c004} is   |                       |
|                       | > > > not greater     |                       |
|                       | > > > than 0, it      |                       |
|                       | > > > outputs the     |                       |
|                       | > > > word,           |                       |
|                       | > > > "Blastoff!" and |                       |
|                       | > > > then returns.   |                       |
|                       | > >                   |                       |
|                       | > > The               |                       |
|                       | >                     |                       |
|                       |  > [countdown]{.c004} |                       |
|                       | > > that got          |                       |
|                       | > > [n=1]{.c004}      |                       |
|                       | > > returns.          |                       |
|                       | >                     |                       |
|                       | > The                 |                       |
|                       | > [countdown]{.c004}  |                       |
|                       | > that got            |                       |
|                       | > [n=2]{.c004}        |                       |
|                       | > returns.            |                       |
|                       |                       |                       |
|                       | The                   |                       |
|                       | [countdown]{.c004}    |                       |
|                       | that got [n=3]{.c004} |                       |
|                       | returns.              |                       |
|                       |                       |                       |
|                       | And then you're back  |                       |
|                       | in `__main__`. So,    |                       |
|                       | the total output      |                       |
|                       | looks like this:      |                       |
|                       | []{#hevea_default361} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | 3                     |                       |
|                       | 2                     |                       |
|                       | 1                     |                       |
|                       | Blastoff!             |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A function that calls |                       |
|                       | itself is             |                       |
|                       | [recursive]{.c010};   |                       |
|                       | the process of        |                       |
|                       | executing it is       |                       |
|                       | called                |                       |
|                       | [recursion]{.c010}.   |                       |
|                       | []{#hevea_default362} |                       |
|                       | []{#hevea_default363} |                       |
|                       |                       |                       |
|                       | As another example,   |                       |
|                       | we can write a        |                       |
|                       | function that prints  |                       |
|                       | a string [n]{.c004}   |                       |
|                       | times.                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_n(s, n):    |                       |
|                       |     if n <= 0:        |                       |
|                       |         return        |                       |
|                       |     print(s)          |                       |
|                       |     print_n(s, n-1)   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If [n \<= 0]{.c004}   |                       |
|                       | the [return           |                       |
|                       | statement]{.c010}     |                       |
|                       | exits the function.   |                       |
|                       | The flow of execution |                       |
|                       | immediately returns   |                       |
|                       | to the caller, and    |                       |
|                       | the remaining lines   |                       |
|                       | of the function don't |                       |
|                       | run.                  |                       |
|                       | []{#hevea_default364} |                       |
|                       | []{#hevea_default365} |                       |
|                       |                       |                       |
|                       | The rest of the       |                       |
|                       | function is similar   |                       |
|                       | to                    |                       |
|                       | [countdown]{.c004}:   |                       |
|                       | it displays           |                       |
|                       | [s]{.c004} and then   |                       |
|                       | calls itself to       |                       |
|                       | display [s]{.c004}    |                       |
|                       | [n]{.c009}−1          |                       |
|                       | additional times. So  |                       |
|                       | the number of lines   |                       |
|                       | of output is [1 +     |                       |
|                       | (n - 1)]{.c004},      |                       |
|                       | which adds up to      |                       |
|                       | [n]{.c004}.           |                       |
|                       |                       |                       |
|                       | For simple examples   |                       |
|                       | like this, it is      |                       |
|                       | probably easier to    |                       |
|                       | use a [for]{.c004}    |                       |
|                       | loop. But we will see |                       |
|                       | examples later that   |                       |
|                       | are hard to write     |                       |
|                       | with a [for]{.c004}   |                       |
|                       | loop and easy to      |                       |
|                       | write with recursion, |                       |
|                       | so it is good to      |                       |
|                       | start early.          |                       |
|                       | []{#hevea_default366} |                       |
|                       | []{#hevea_default367} |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 5.9  Stack diagrams |                       |
|                       |  for recursive functi |                       |
|                       | ons {#sec63 .section} |                       |
|                       |                       |                       |
|                       | []{#recursive.stack}  |                       |
|                       | []{#hevea_default368} |                       |
|                       | []{#hevea_default369} |                       |
|                       | []{#hevea_default370} |                       |
|                       |                       |                       |
|                       | In                    |                       |
|                       | Section               |                       |
|                       |  [3.9](thinkpython200 |                       |
|                       | 4.html#stackdiagram), |                       |
|                       | we used a stack       |                       |
|                       | diagram to represent  |                       |
|                       | the state of a        |                       |
|                       | program during a      |                       |
|                       | function call. The    |                       |
|                       | same kind of diagram  |                       |
|                       | can help interpret a  |                       |
|                       | recursive function.   |                       |
|                       |                       |                       |
|                       | Every time a function |                       |
|                       | gets called, Python   |                       |
|                       | creates a frame to    |                       |
|                       | contain the           |                       |
|                       | function's local      |                       |
|                       | variables and         |                       |
|                       | parameters. For a     |                       |
|                       | recursive function,   |                       |
|                       | there might be more   |                       |
|                       | than one frame on the |                       |
|                       | stack at the same     |                       |
|                       | time.                 |                       |
|                       |                       |                       |
|                       | Figu                  |                       |
|                       | re [5.1](#fig.stack2) |                       |
|                       | shows a stack diagram |                       |
|                       | for                   |                       |
|                       | [countdown]{.c004}    |                       |
|                       | called with [n =      |                       |
|                       | 3]{.c004}.            |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2005.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | >   Figur             |                       |
|                       | e 5.1: Stack diagram. |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.stack2}     |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | As usual, the top of  |                       |
|                       | the stack is the      |                       |
|                       | frame for `__main__`. |                       |
|                       | It is empty because   |                       |
|                       | we did not create any |                       |
|                       | variables in          |                       |
|                       | `__main__` or pass    |                       |
|                       | any arguments to it.  |                       |
|                       | []{#hevea_default371} |                       |
|                       | []{#hevea_default372} |                       |
|                       |                       |                       |
|                       | The four              |                       |
|                       | [countdown]{.c004}    |                       |
|                       | frames have different |                       |
|                       | values for the        |                       |
|                       | parameter [n]{.c004}. |                       |
|                       | The bottom of the     |                       |
|                       | stack, where          |                       |
|                       | [n=0]{.c004}, is      |                       |
|                       | called the [base      |                       |
|                       | case]{.c010}. It does |                       |
|                       | not make a recursive  |                       |
|                       | call, so there are no |                       |
|                       | more frames.          |                       |
|                       |                       |                       |
|                       | As an exercise, draw  |                       |
|                       | a stack diagram for   |                       |
|                       | `print_n` called with |                       |
|                       | `s = 'Hello'` and     |                       |
|                       | [n=2]{.c004}. Then    |                       |
|                       | write a function      |                       |
|                       | called `do_n` that    |                       |
|                       | takes a function      |                       |
|                       | object and a number,  |                       |
|                       | [n]{.c004}, as        |                       |
|                       | arguments, and that   |                       |
|                       | calls the given       |                       |
|                       | function [n]{.c004}   |                       |
|                       | times.                |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 5.10  Infinite recurs |                       |
|                       | ion {#sec64 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default373} |                       |
|                       | []{#hevea_default374} |                       |
|                       | []{#hevea_default375} |                       |
|                       | []{#hevea_default376} |                       |
|                       | []{#hevea_default377} |                       |
|                       |                       |                       |
|                       | If a recursion never  |                       |
|                       | reaches a base case,  |                       |
|                       | it goes on making     |                       |
|                       | recursive calls       |                       |
|                       | forever, and the      |                       |
|                       | program never         |                       |
|                       | terminates. This is   |                       |
|                       | known as [infinite    |                       |
|                       | recursion]{.c010},    |                       |
|                       | and it is generally   |                       |
|                       | not a good idea. Here |                       |
|                       | is a minimal program  |                       |
|                       | with an infinite      |                       |
|                       | recursion:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def recurse():        |                       |
|                       |     recurse()         |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In most programming   |                       |
|                       | environments, a       |                       |
|                       | program with infinite |                       |
|                       | recursion does not    |                       |
|                       | really run forever.   |                       |
|                       | Python reports an     |                       |
|                       | error message when    |                       |
|                       | the maximum recursion |                       |
|                       | depth is reached:     |                       |
|                       | []{#hevea_default378} |                       |
|                       | []{#hevea_default379} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |   File "<stdin>       |                       |
|                       | ", line 2, in recurse |                       |
|                       |   File "<stdin>       |                       |
|                       | ", line 2, in recurse |                       |
|                       |   File "<stdin>       |                       |
|                       | ", line 2, in recurse |                       |
|                       |                       |                       |
|                       |                  .    |                       |
|                       |                   .   |                       |
|                       |                   .   |                       |
|                       |   File "<stdin>       |                       |
|                       | ", line 2, in recurse |                       |
|                       | Runt                  |                       |
|                       | imeError: Maximum rec |                       |
|                       | ursion depth exceeded |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This traceback is a   |                       |
|                       | little bigger than    |                       |
|                       | the one we saw in the |                       |
|                       | previous chapter.     |                       |
|                       | When the error        |                       |
|                       | occurs, there are     |                       |
|                       | 1000 [recurse]{.c004} |                       |
|                       | frames on the stack!  |                       |
|                       |                       |                       |
|                       | If you encounter an   |                       |
|                       | infinite recursion by |                       |
|                       | accident, review your |                       |
|                       | function to confirm   |                       |
|                       | that there is a base  |                       |
|                       | case that does not    |                       |
|                       | make a recursive      |                       |
|                       | call. And if there is |                       |
|                       | a base case, check    |                       |
|                       | whether you are       |                       |
|                       | guaranteed to reach   |                       |
|                       | it.                   |                       |
|                       |                       |                       |
|                       | ## 5.11  Keyboard in  |                       |
|                       | put {#sec65 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default380} |                       |
|                       |                       |                       |
|                       | The programs we have  |                       |
|                       | written so far accept |                       |
|                       | no input from the     |                       |
|                       | user. They just do    |                       |
|                       | the same thing every  |                       |
|                       | time.                 |                       |
|                       |                       |                       |
|                       | Python provides a     |                       |
|                       | built-in function     |                       |
|                       | called [input]{.c004} |                       |
|                       | that stops the        |                       |
|                       | program and waits for |                       |
|                       | the user to type      |                       |
|                       | something. When the   |                       |
|                       | user presses          |                       |
|                       | [Return]{.c006} or    |                       |
|                       | [Enter]{.c006}, the   |                       |
|                       | program resumes and   |                       |
|                       | `input` returns what  |                       |
|                       | the user typed as a   |                       |
|                       | string. In Python 2,  |                       |
|                       | the same function is  |                       |
|                       | called `raw_input`.   |                       |
|                       | []{#hevea_default381} |                       |
|                       | []{#hevea_default382} |                       |
|                       | []{#hevea_default383} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> text = input()    |                       |
|                       | What                  |                       |
|                       |  are you waiting for? |                       |
|                       | >>> text              |                       |
|                       | 'What                 |                       |
|                       | are you waiting for?' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Before getting input  |                       |
|                       | from the user, it is  |                       |
|                       | a good idea to print  |                       |
|                       | a prompt telling the  |                       |
|                       | user what to type.    |                       |
|                       | `input` can take a    |                       |
|                       | prompt as an          |                       |
|                       | argument:             |                       |
|                       | []{#hevea_default384} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> name = input('Wha |                       |
|                       | t...is your name?\n') |                       |
|                       | What...is your name?  |                       |
|                       | Arthur,               |                       |
|                       |  King of the Britons! |                       |
|                       | >>> name              |                       |
|                       | 'Arthur,              |                       |
|                       | King of the Britons!' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The sequence `\n` at  |                       |
|                       | the end of the prompt |                       |
|                       | represents a          |                       |
|                       | [newline]{.c010},     |                       |
|                       | which is a special    |                       |
|                       | character that causes |                       |
|                       | a line break. That's  |                       |
|                       | why the user's input  |                       |
|                       | appears below the     |                       |
|                       | prompt.               |                       |
|                       | []{#hevea_default385} |                       |
|                       |                       |                       |
|                       | If you expect the     |                       |
|                       | user to type an       |                       |
|                       | integer, you can try  |                       |
|                       | to convert the return |                       |
|                       | value to              |                       |
|                       | [int]{.c004}:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> prom              |                       |
|                       | pt = 'What...is the a |                       |
|                       | irspeed velocity of a |                       |
|                       | n unladen swallow?\n' |                       |
|                       | >>>                   |                       |
|                       | speed = input(prompt) |                       |
|                       | What...is th          |                       |
|                       | e airspeed velocity o |                       |
|                       | f an unladen swallow? |                       |
|                       | 42                    |                       |
|                       | >>> int(speed)        |                       |
|                       | 42                    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But if the user types |                       |
|                       | something other than  |                       |
|                       | a string of digits,   |                       |
|                       | you get an error:     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | speed = input(prompt) |                       |
|                       | What...is th          |                       |
|                       | e airspeed velocity o |                       |
|                       | f an unladen swallow? |                       |
|                       | What do y             |                       |
|                       | ou mean, an African o |                       |
|                       | r a European swallow? |                       |
|                       | >>> int(speed)        |                       |
|                       | ValueErr              |                       |
|                       | or: invalid literal f |                       |
|                       | or int() with base 10 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | We will see how to    |                       |
|                       | handle this kind of   |                       |
|                       | error later.          |                       |
|                       | []{#hevea_default386} |                       |
|                       | []{#hevea_default387} |                       |
|                       |                       |                       |
|                       | ## 5.12  Debugg       |                       |
|                       | ing {#sec66 .section} |                       |
|                       |                       |                       |
|                       | []{#whitespace}       |                       |
|                       | []{#hevea_default388} |                       |
|                       | []{#hevea_default389} |                       |
|                       |                       |                       |
|                       | When a syntax or      |                       |
|                       | runtime error occurs, |                       |
|                       | the error message     |                       |
|                       | contains a lot of     |                       |
|                       | information, but it   |                       |
|                       | can be overwhelming.  |                       |
|                       | The most useful parts |                       |
|                       | are usually:          |                       |
|                       |                       |                       |
|                       | -   What kind of      |                       |
|                       |     error it was, and |                       |
|                       | -   Where it          |                       |
|                       |     occurred.         |                       |
|                       |                       |                       |
|                       | Syntax errors are     |                       |
|                       | usually easy to find, |                       |
|                       | but there are a few   |                       |
|                       | gotchas. Whitespace   |                       |
|                       | errors can be tricky  |                       |
|                       | because spaces and    |                       |
|                       | tabs are invisible    |                       |
|                       | and we are used to    |                       |
|                       | ignoring them.        |                       |
|                       | []{#hevea_default390} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> x = 5             |                       |
|                       | >>>  y = 6            |                       |
|                       |   F                   |                       |
|                       | ile "<stdin>", line 1 |                       |
|                       |     y = 6             |                       |
|                       |     ^                 |                       |
|                       | IndentationErr        |                       |
|                       | or: unexpected indent |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In this example, the  |                       |
|                       | problem is that the   |                       |
|                       | second line is        |                       |
|                       | indented by one       |                       |
|                       | space. But the error  |                       |
|                       | message points to     |                       |
|                       | [y]{.c004}, which is  |                       |
|                       | misleading. In        |                       |
|                       | general, error        |                       |
|                       | messages indicate     |                       |
|                       | where the problem was |                       |
|                       | discovered, but the   |                       |
|                       | actual error might be |                       |
|                       | earlier in the code,  |                       |
|                       | sometimes on a        |                       |
|                       | previous line.        |                       |
|                       | []{#hevea_default391} |                       |
|                       | []{#hevea_default392} |                       |
|                       |                       |                       |
|                       | The same is true of   |                       |
|                       | runtime errors.       |                       |
|                       | Suppose you are       |                       |
|                       | trying to compute a   |                       |
|                       | signal-to-noise ratio |                       |
|                       | in decibels. The      |                       |
|                       | formula is            |                       |
|                       | [SNR                  |                       |
|                       | ]{.c009}~[db]{.c009}~ |                       |
|                       | = 10 log~10~          |                       |
|                       | ([P]{.c               |                       |
|                       | 009}~[signal]{.c009}~ |                       |
|                       | /                     |                       |
|                       | [P]{.c0               |                       |
|                       | 09}~[noise]{.c009}~). |                       |
|                       | In Python, you might  |                       |
|                       | write something like  |                       |
|                       | this:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | import math           |                       |
|                       | signal_power = 9      |                       |
|                       | noise_power = 10      |                       |
|                       | ratio = signal        |                       |
|                       | _power // noise_power |                       |
|                       | decibels = 1          |                       |
|                       | 0 * math.log10(ratio) |                       |
|                       | print(decibels)       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | When you run this     |                       |
|                       | program, you get an   |                       |
|                       | exception:            |                       |
|                       | []{#hevea_default393} |                       |
|                       | []{#hevea_default394} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Traceback (mo         |                       |
|                       | st recent call last): |                       |
|                       |   File "              |                       |
|                       | snr.py", line 5, in ? |                       |
|                       |     decibels = 1      |                       |
|                       | 0 * math.log10(ratio) |                       |
|                       | ValueErr              |                       |
|                       | or: math domain error |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The error message     |                       |
|                       | indicates line 5, but |                       |
|                       | there is nothing      |                       |
|                       | wrong with that line. |                       |
|                       | To find the real      |                       |
|                       | error, it might be    |                       |
|                       | useful to print the   |                       |
|                       | value of              |                       |
|                       | [ratio]{.c004}, which |                       |
|                       | turns out to be 0.    |                       |
|                       | The problem is in     |                       |
|                       | line 4, which uses    |                       |
|                       | floor division        |                       |
|                       | instead of            |                       |
|                       | floating-point        |                       |
|                       | division.             |                       |
|                       | []{#hevea_default395} |                       |
|                       | []{#hevea_default396} |                       |
|                       |                       |                       |
|                       | You should take the   |                       |
|                       | time to read error    |                       |
|                       | messages carefully,   |                       |
|                       | but don't assume that |                       |
|                       | everything they say   |                       |
|                       | is correct.           |                       |
|                       |                       |                       |
|                       | ## 5.13  Gloss        |                       |
|                       | ary {#sec67 .section} |                       |
|                       |                       |                       |
|                       | [fl                   |                       |
|                       | oor division:]{.c010} |                       |
|                       | :   An operator,      |                       |
|                       |     denoted           |                       |
|                       |     [//]{.c004}, that |                       |
|                       |     divides two       |                       |
|                       |     numbers and       |                       |
|                       |     rounds down       |                       |
|                       |     (toward negative  |                       |
|                       |     infinity) to an   |                       |
|                       |     integer.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default397} |                       |
|                       |                       |                       |
|                       | []{#hevea_default398} |                       |
|                       |                       |                       |
|                       | [modu                 |                       |
|                       | lus operator:]{.c010} |                       |
|                       