            |
|                       | :   A mathematical    |                       |
|                       |     entity that       |                       |
|                       |     represents a      |                       |
|                       |     mapping between   |                       |
|                       |     the elements of a |                       |
|                       |     set and the       |                       |
|                       |     number of times   |                       |
|                       |     they appear.      |                       |
|                       |                       |                       |
|                       | [factory:]{.c010}     |                       |
|                       | :   A function,       |                       |
|                       |     usually passed as |                       |
|                       |     a parameter, used |                       |
|                       |     to create         |                       |
|                       |     objects.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1729} |                       |
|                       |                       |                       |
|                       | ## 19.11  Exercis     |                       |
|                       | es {#sec233 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *The following is a   |                       |
|                       | function that         |                       |
|                       | computes the binomial |                       |
|                       | coefficient           |                       |
|                       | recursively.*         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | binomial_coeff(n, k): |                       |
|                       |     """Comp           |                       |
|                       | ute the binomial coef |                       |
|                       | ficient "n choose k". |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |   n: number of trials |                       |
|                       |     k                 |                       |
|                       | : number of successes |                       |
|                       |                       |                       |
|                       |     returns: int      |                       |
|                       |     """               |                       |
|                       |     if k == 0:        |                       |
|                       |         return 1      |                       |
|                       |     if n == 0:        |                       |
|                       |         return 0      |                       |
|                       |                       |                       |
|                       |     res = binomia     |                       |
|                       | l_coeff(n-1, k) + bin |                       |
|                       | omial_coeff(n-1, k-1) |                       |
|                       |     return res        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *Rewrite the body of  |                       |
|                       | the function using    |                       |
|                       | nested conditional    |                       |
|                       | expressions.*         |                       |
|                       |                       |                       |
|                       | *One note: this       |                       |
|                       | function is not very  |                       |
|                       | efficient because it  |                       |
|                       | ends up computing the |                       |
|                       | same values over and  |                       |
|                       | over. You could make  |                       |
|                       | it more efficient by  |                       |
|                       | memoizing (see        |                       |
|                       | Section               |                       |
|                       | *[*11.6*](thinkpython |                       |
|                       | 2012.html#memoize)*). |                       |
|                       | But you will find     |                       |
|                       | that it's harder to   |                       |
|                       | memoize if you write  |                       |
|                       | it using conditional  |                       |
|                       | expressions.*         |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2019.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2021.html)
---
generator: hevea 2.32
title: Debugging
---

[![Previous](back.png)](thinkpython2020.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2022.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Appendix A  Debuggi | to support my books,  |
|                       | ng {#sec234 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | [                     | with PayPal. Thank    |
|                       | ]{#hevea_default1730} | you!                  |
|                       |                       |                       |
|                       | When you are          |   -----------         |
|                       | debugging, you should | --------------------- |
|                       | distinguish among     | --------------------- |
|                       | different kinds of    | --------------------- |
|                       | errors in order to    | --------------------- |
|                       | track them down more  |   Pay what you want:  |
|                       | quickly:              |   Small \$1           |
|                       |                       | .00 USD Medium \$5.00 |
|                       | -   Syntax errors are |  USD Large \$10.00 US |
|                       |     discovered by the | D X-Large \$20.00 USD |
|                       |     interpreter when  |  XX-Large \$50.00 USD |
|                       |     it is translating |   -----------         |
|                       |     the source code   | --------------------- |
|                       |     into byte code.   | --------------------- |
|                       |     They indicate     | --------------------- |
|                       |     that there is     | --------------------- |
|                       |     something wrong   |                       |
|                       |     with the          | ![](                  |
|                       |     structure of the  | https://www.paypalobj |
|                       |     program. Example: | ects.com/en_US/i/scr/ |
|                       |     Omitting the      | pixel.gif){border="0" |
|                       |     colon at the end  | width="1" height="1"} |
|                       |     of a [def]{.c004} |                       |
|                       |     statement         | ####                  |
|                       |     generates the     | Are you using one of  |
|                       |     somewhat          | our books in a class? |
|                       |     redundant message |                       |
|                       |     [SyntaxError:     | We\'d like to know    |
|                       |     invalid           | about it. Please      |
|                       |     syntax]{.c004}.   | consider filling out  |
|                       |     [                 | [this short           |
|                       | ]{#hevea_default1731} | survey](http://s      |
|                       |     [                 | preadsheets.google.co |
|                       | ]{#hevea_default1732} | m/viewform?formkey=dC |
|                       | -   Runtime errors    | 0tNUZkMjBEdXVoRGljNm9 |
|                       |     are produced by   | FRmlTMHc6MA){onclick= |
|                       |     the interpreter   | "javascript: pageTrac |
|                       |     if something goes | ker._trackPageview('/ |
|                       |     wrong while the   | outbound/survey');"}. |
|                       |     program is        |                       |
|                       |     running. Most     | \                     |
|                       |     runtime error     |                       |
|                       |     messages include  | [Think                |
|                       |     information about | DSP](http             |
|                       |     where the error   | ://www.amazon.com/gp/ |
|                       |     occurred and what | product/1491938455/re |
|                       |     functions were    | f=as_li_tl?ie=UTF8&ca |
|                       |     executing.        | mp=1789&creative=9325 |
|                       |     Example: An       | &creativeASIN=1491938 |
|                       |     infinite          | 455&linkCode=as2&tag= |
|                       |     recursion         | greenteapre01-20&link |
|                       |     eventually causes | Id=2JJH4SWCAVVYSQHO){ |
|                       |     the runtime error | rel="nofollow"}![](ht |
|                       |     "maximum          | tp://ir-na.amazon-ads |
|                       |     recursion depth   | ystem.com/e/ir?t=gree |
|                       |     exceeded".        | nteapre01-20&l=as2&o= |
|                       |     [                 | 1&a=1491938455){.c003 |
|                       | ]{#hevea_default1733} | width="1" height="1"  |
|                       |     [                 | border="0"}           |
|                       | ]{#hevea_default1734} |                       |
|                       |     [                 | [                     |
|                       | ]{#hevea_default1735} | ![](http://ws-na.amaz |
|                       | -   Semantic errors   | on-adsystem.com/widge |
|                       |     are problems with | ts/q?_encoding=UTF8&A |
|                       |     a program that    | SIN=1491938455&Format |
|                       |     runs without      | =_SL160_&ID=AsinImage |
|                       |     producing error   | &MarketPlace=US&Servi |
|                       |     messages but      | ceVersion=20070822&WS |
|                       |     doesn't do the    | =1&tag=greenteapre01- |
|                       |     right thing.      | 20){border="0"}](http |
|                       |     Example: An       | ://www.amazon.com/gp/ |
|                       |     expression may    | product/1491938455/re |
|                       |     not be evaluated  | f=as_li_tl?ie=UTF8&ca |
|                       |     in the order you  | mp=1789&creative=9325 |
|                       |     expect, yielding  | &creativeASIN=1491938 |
|                       |     an incorrect      | 455&linkCode=as2&tag= |
|                       |     result.           | greenteapre01-20&link |
|                       |     [                 | Id=CTV7PDT7E5EGGJUM){ |
|                       | ]{#hevea_default1736} | rel="nofollow"}![](ht |
|                       |     [                 | tp://ir-na.amazon-ads |
|                       | ]{#hevea_default1737} | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | The first step in     | 1&a=1491938455){.c003 |
|                       | debugging is to       | width="1" height="1"  |
|                       | figure out which kind | border="0"}           |
|                       | of error you are      |                       |
|                       | dealing with.         | [Think                |
|                       | Although the          | Java](http            |
|                       | following sections    | ://www.amazon.com/gp/ |
|                       | are organized by      | product/1491929561/re |
|                       | error type, some      | f=as_li_tl?ie=UTF8&ca |
|                       | techniques are        | mp=1789&creative=9325 |
|                       | applicable in more    | &creativeASIN=1491929 |
|                       | than one situation.   | 561&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | ## A.1  Syntax erro   | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | rs {#sec235 .section} | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1738} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | Syntax errors are     | width="1" height="1"  |
|                       | usually easy to fix   | border="0"}           |
|                       | once you figure out   |                       |
|                       | what they are.        | [                     |
|                       | Unfortunately, the    | ![](http://ws-na.amaz |
|                       | error messages are    | on-adsystem.com/widge |
|                       | often not helpful.    | ts/q?_encoding=UTF8&A |
|                       | The most common       | SIN=1491929561&Format |
|                       | messages are          | =_SL160_&ID=AsinImage |
|                       | [SyntaxError: invalid | &MarketPlace=US&Servi |
|                       | syntax]{.c004} and    | ceVersion=20070822&WS |
|                       | [SyntaxError: invalid | =1&tag=greenteapre01- |
|                       | token]{.c004},        | 20){border="0"}](http |
|                       | neither of which is   | ://www.amazon.com/gp/ |
|                       | very informative.     | product/1491929561/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | On the other hand,    | mp=1789&creative=9325 |
|                       | the message does tell | &creativeASIN=1491929 |
|                       | you where in the      | 561&linkCode=as2&tag= |
|                       | program the problem   | greenteapre01-20&link |
|                       | occurred. Actually,   | Id=PT77ANWARUNNU3UK){ |
|                       | it tells you where    | rel="nofollow"}![](ht |
|                       | Python noticed a      | tp://ir-na.amazon-ads |
|                       | problem, which is not | ystem.com/e/ir?t=gree |
|                       | necessarily where the | nteapre01-20&l=as2&o= |
|                       | error is. Sometimes   | 1&a=1491929561){.c003 |
|                       | the error is prior to | width="1" height="1"  |
|                       | the location of the   | border="0"}           |
|                       | error message, often  |                       |
|                       | on the preceding      | [Think                |
|                       | line.                 | Bay                   |
|                       | [                     | es](http://www.amazon |
|                       | ]{#hevea_default1739} | .com/gp/product/14493 |
|                       | [                     | 70780/ref=as_li_qf_sp |
|                       | ]{#hevea_default1740} | _asin_tl?ie=UTF8&camp |
|                       |                       | =1789&creative=9325&c |
|                       | If you are building   | reativeASIN=144937078 |
|                       | the program           | 0&linkCode=as2&tag=gr |
|                       | incrementally, you    | eenteapre01-20)![](ht |
|                       | should have a good    | tp://ir-na.amazon-ads |
|                       | idea about where the  | ystem.com/e/ir?t=gree |
|                       | error is. It will be  | nteapre01-20&l=as2&o= |
|                       | in the last line you  | 1&a=1449370780){.c003 |
|                       | added.                | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | If you are copying    |                       |
|                       | code from a book,     | [![](http://ws        |
|                       | start by comparing    | -na.amazon-adsystem.c |
|                       | your code to the      | om/widgets/q?_encodin |
|                       | book's code very      | g=UTF8&ASIN=144937078 |
|                       | carefully. Check      | 0&Format=_SL160_&ID=A |
|                       | every character. At   | sinImage&MarketPlace= |
|                       | the same time,        | US&ServiceVersion=200 |
|                       | remember that the     | 70822&WS=1&tag=greent |
|                       | book might be wrong,  | eapre01-20){border="0 |
|                       | so if you see         | "}](http://www.amazon |
|                       | something that looks  | .com/gp/product/14493 |
|                       | like a syntax error,  | 70780/ref=as_li_qf_sp |
|                       | it might be.          | _asin_il?ie=UTF8&camp |
|                       |                       | =1789&creative=9325&c |
|                       | Here are some ways to | reativeASIN=144937078 |
|                       | avoid the most common | 0&linkCode=as2&tag=gr |
|                       | syntax errors:        | eenteapre01-20)![](ht |
|                       | [                     | tp://ir-na.amazon-ads |
|                       | ]{#hevea_default1741} | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | 1.  Make sure you are | 1&a=1449370780){.c003 |
|                       |     not using a       | width="1" height="1"  |
|                       |     Python keyword    | border="0"}           |
|                       |     for a variable    |                       |
|                       |     name.             | [Think Python         |
|                       |     [                 | 2e](http              |
|                       | ]{#hevea_default1742} | ://www.amazon.com/gp/ |
|                       | 2.  Check that you    | product/1491939362/re |
|                       |     have a colon at   | f=as_li_tl?ie=UTF8&ca |
|                       |     the end of the    | mp=1789&creative=9325 |
|                       |     header of every   | &creativeASIN=1491939 |
|                       |     compound          | 362&linkCode=as2&tag= |
|                       |     statement,        | greenteapre01-20&link |
|                       |     including         | Id=FJKSQ3IHEMY2F2VA){ |
|                       |     [for]{.c004},     | rel="nofollow"}![](ht |
|                       |     [while]{.c004},   | tp://ir-na.amazon-ads |
|                       |     [if]{.c004}, and  | ystem.com/e/ir?t=gree |
|                       |     [def]{.c004}      | nteapre01-20&l=as2&o= |
|                       |     statements.       | 1&a=1491939362){.c003 |
|                       |     [                 | width="1" height="1"  |
|                       | ]{#hevea_default1743} | border="0"}           |
|                       |     [                 |                       |
|                       | ]{#hevea_default1744} | [                     |
|                       | 3.  Make sure that    | ![](http://ws-na.amaz |
|                       |     any strings in    | on-adsystem.com/widge |
|                       |     the code have     | ts/q?_encoding=UTF8&A |
|                       |     matching          | SIN=1491939362&Format |
|                       |     quotation marks.  | =_SL160_&ID=AsinImage |
|                       |     Make sure that    | &MarketPlace=US&Servi |
|                       |     all quotation     | ceVersion=20070822&WS |
|                       |     marks are         | =1&tag=greenteapre01- |
|                       |     "straight         | 20){border="0"}](http |
|                       |     quotes", not      | ://www.amazon.com/gp/ |
|                       |     "curly quotes".   | product/1491939362/re |
|                       |     [                 | f=as_li_tl?ie=UTF8&ca |
|                       | ]{#hevea_default1745} | mp=1789&creative=9325 |
|                       | 4.  If you have       | &creativeASIN=1491939 |
|                       |     multiline strings | 362&linkCode=as2&tag= |
|                       |     with triple       | greenteapre01-20&link |
|                       |     quotes (single or | Id=ZZ454DLQ3IXDHNHX){ |
|                       |     double), make     | rel="nofollow"}![](ht |
|                       |     sure you have     | tp://ir-na.amazon-ads |
|                       |     terminated the    | ystem.com/e/ir?t=gree |
|                       |     string properly.  | nteapre01-20&l=as2&o= |
|                       |     An unterminated   | 1&a=1491939362){.c003 |
|                       |     string may cause  | width="1" height="1"  |
|                       |     an [invalid       | border="0"}           |
|                       |     token]{.c004}     |                       |
|                       |     error at the end  | [Think Stats          |
|                       |     of your program,  | 2e](http://ww         |
|                       |     or it may treat   | w.amazon.com/gp/produ |
|                       |     the following     | ct/1491907339/ref=as_ |
|                       |     part of the       | li_tl?ie=UTF8&camp=17 |
|                       |     program as a      | 89&creative=9325&crea |
|                       |     string until it   | tiveASIN=1491907339&l |
|                       |     comes to the next | inkCode=as2&tag=green |
|                       |     string. In the    | teapre01-20&linkId=O7 |
|                       |     second case, it   | WYM6H6YBYUFNWU)![](ht |
|                       |     might not produce | tp://ir-na.amazon-ads |
|                       |     an error message  | ystem.com/e/ir?t=gree |
|                       |     at all!           | nteapre01-20&l=as2&o= |
|                       |     [                 | 1&a=1491907339){.c003 |
|                       | ]{#hevea_default1746} | width="1" height="1"  |
|                       |     [                 | border="0"}           |
|                       | ]{#hevea_default1747} |                       |
|                       | 5.  An unclosed       | [![](h                |
|                       |     opening           | ttp://ws-na.amazon-ad |
|                       |     operator---`(`,   | system.com/widgets/q? |
|                       |     `{`, or           | _encoding=UTF8&ASIN=1 |
|                       |     `[`---makes       | 491907339&Format=_SL1 |
|                       |     Python continue   | 60_&ID=AsinImage&Mark |
|                       |     with the next     | etPlace=US&ServiceVer |
|                       |     line as part of   | sion=20070822&WS=1&ta |
|                       |     the current       | g=greenteapre01-20){b |
|                       |     statement.        | order="0"}](http://ww |
|                       |     Generally, an     | w.amazon.com/gp/produ |
|                       |     error occurs      | ct/1491907339/ref=as_ |
|                       |     almost            | li_tl?ie=UTF8&camp=17 |
|                       |     immediately in    | 89&creative=9325&crea |
|                       |     the next line.    | tiveASIN=1491907339&l |
|                       | 6.  Check for the     | inkCode=as2&tag=green |
|                       |     classic           | teapre01-20&linkId=JV |
|                       |     [=]{.c004}        | SYKQHYSUIEYRHL)![](ht |
|                       |     instead of        | tp://ir-na.amazon-ads |
|                       |     [==]{.c004}       | ystem.com/e/ir?t=gree |
|                       |     inside a          | nteapre01-20&l=as2&o= |
|                       |     conditional.      | 1&a=1491907339){.c003 |
|                       |     [                 | width="1" height="1"  |
|                       | ]{#hevea_default1748} | border="0"}           |
|                       | 7.  Check the         |                       |
|                       |     indentation to    | [Think                |
|                       |     make sure it      | Complexity](http      |
|                       |     lines up the way  | ://www.amazon.com/gp/ |
|                       |     it is supposed    | product/1449314635/re |
|                       |     to. Python can    | f=as_li_tf_tl?ie=UTF8 |
|                       |     handle space and  | &tag=greenteapre01-20 |
|                       |     tabs, but if you  | &linkCode=as2&camp=17 |
|                       |     mix them it can   | 89&creative=9325&crea |
|                       |     cause problems.   | tiveASIN=1449314635)! |
|                       |     The best way to   | [](http://www.assoc-a |
|                       |     avoid this        | mazon.com/e/ir?t=gree |
|                       |     problem is to use | nteapre01-20&l=as2&o= |
|                       |     a text editor     | 1&a=1449314635){.c003 |
|                       |     that knows about  | width="1" height="1"  |
|                       |     Python and        | border="0"}           |
|                       |     generates         |                       |
|                       |     consistent        | [                     |
|                       |     indentation.      | ![](http://ws-na.amaz |
|                       |     [                 | on-adsystem.com/widge |
|                       | ]{#hevea_default1749} | ts/q?_encoding=UTF8&A |
|                       |     [                 | SIN=1449314635&Format |
|                       | ]{#hevea_default1750} | =_SL160_&ID=AsinImage |
|                       | 8.  If you have       | &MarketPlace=US&Servi |
|                       |     non-ASCII         | ceVersion=20070822&WS |
|                       |     characters in the | =1&tag=greenteapre01- |
|                       |     code (including   | 20){border="0"}](http |
|                       |     strings and       | ://www.amazon.com/gp/ |
|                       |     comments), that   | product/1449314635/re |
|                       |     might cause a     | f=as_li_tf_il?ie=UTF8 |
|                       |     problem, although | &camp=1789&creative=9 |
|                       |     Python 3 usually  | 325&creativeASIN=1449 |
|                       |     handles non-ASCII | 314635&linkCode=as2&t |
|                       |     characters. Be    | ag=greenteapre01-20)! |
|                       |     careful if you    | [](http://www.assoc-a |
|                       |     paste in text     | mazon.com/e/ir?t=gree |
|                       |     from a web page   | nteapre01-20&l=as2&o= |
|                       |     or other source.  | 1&a=1449314635){.c003 |
|                       |                       | width="1" height="1"  |
|                       | If nothing works,     | border="0"}           |
|                       | move on to the next   |                       |
|                       | section\...           |                       |
|                       |                       |                       |
|                       | ### A.1.1  I keep m   |                       |
|                       | aking changes and it  |                       |
|                       | makes no difference.  |                       |
|                       | {#sec236 .subsection} |                       |
|                       |                       |                       |
|                       | If the interpreter    |                       |
|                       | says there is an      |                       |
|                       | error and you don't   |                       |
|                       | see it, that might be |                       |
|                       | because you and the   |                       |
|                       | interpreter are not   |                       |
|                       | looking at the same   |                       |
|                       | code. Check your      |                       |
|                       | programming           |                       |
|                       | environment to make   |                       |
|                       | sure that the program |                       |
|                       | you are editing is    |                       |
|                       | the one Python is     |                       |
|                       | trying to run.        |                       |
|                       |                       |                       |
|                       | If you are not sure,  |                       |
|                       | try putting an        |                       |
|                       | obvious and           |                       |
|                       | deliberate syntax     |                       |
|                       | error at the          |                       |
|                       | beginning of the      |                       |
|                       | program. Now run it   |                       |
|                       | again. If the         |                       |
|                       | interpreter doesn't   |                       |
|                       | find the new error,   |                       |
|                       | you are not running   |                       |
|                       | the new code.         |                       |
|                       |                       |                       |
|                       | There are a few       |                       |
|                       | likely culprits:      |                       |
|                       |                       |                       |
|                       | -   You edited the    |                       |
|                       |     file and forgot   |                       |
|                       |     to save the       |                       |
|                       |     changes before    |                       |
|                       |     running it again. |                       |
|                       |     Some programming  |                       |
|                       |     environments do   |                       |
|                       |     this for you, but |                       |
|                       |     some don't.       |                       |
|                       | -   You changed the   |                       |
|                       |     name of the file, |                       |
|                       |     but you are still |                       |
|                       |     running the old   |                       |
|                       |     name.             |                       |
|                       | -   Something in your |                       |
|                       |     development       |                       |
|                       |     environment is    |                       |
|                       |     configured        |                       |
|                       |     incorrectly.      |                       |
|                       | -   If you are        |                       |
|                       |     writing a module  |                       |
|                       |     and using         |                       |
|                       |     [import]{.c004},  |                       |
|                       |     make sure you     |                       |
|                       |     don't give your   |                       |
|                       |     module the same   |                       |
|                       |     name as one of    |                       |
|                       |     the standard      |                       |
|                       |     Python modules.   |                       |
|                       | -   If you are using  |                       |
|                       |     [import]{.c004}   |                       |
|                       |     to read a module, |                       |
|                       |     remember that you |                       |
|                       |     have to restart   |                       |
|                       |     the interpreter   |                       |
|                       |     or use            |                       |
|                       |     [reload]{.c004}   |                       |
|                       |     to read a         |                       |
|                       |     modified file. If |                       |
|                       |     you import the    |                       |
|                       |     module again, it  |                       |
|                       |     doesn't do        |                       |
|                       |     anything.         |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1751} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1752} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1753} |                       |
|                       |                       |                       |
|                       | If you get stuck and  |                       |
|                       | you can't figure out  |                       |
|                       | what is going on, one |                       |
|                       | approach is to start  |                       |
|                       | again with a new      |                       |
|                       | program like "Hello,  |                       |
|                       | World!", and make     |                       |
|                       | sure you can get a    |                       |
|                       | known program to run. |                       |
|                       | Then gradually add    |                       |
|                       | the pieces of the     |                       |
|                       | original program to   |                       |
|                       | the new one.          |                       |
|                       |                       |                       |
|                       | ## A.2  Runtime erro  |                       |
|                       | rs {#sec237 .section} |                       |
|                       |                       |                       |
|                       | Once your program is  |                       |
|                       | syntactically         |                       |
|                       | correct, Python can   |                       |
|                       | read it and at least  |                       |
|                       | start running it.     |                       |
|                       | What could possibly   |                       |
|                       | go wrong?             |                       |
|                       |                       |                       |
|                       | ### A                 |                       |
|                       | .2.1  My program does |                       |
|                       |  absolutely nothing.  |                       |
|                       | {#sec238 .subsection} |                       |
|                       |                       |                       |
|                       | This problem is most  |                       |
|                       | common when your file |                       |
|                       | consists of functions |                       |
|                       | and classes but does  |                       |
|                       | not actually invoke a |                       |
|                       | function to start     |                       |
|                       | execution. This may   |                       |
|                       | be intentional if you |                       |
|                       | only plan to import   |                       |
|                       | this module to supply |                       |
|                       | classes and           |                       |
|                       | functions.            |                       |
|                       |                       |                       |
|                       | If it is not          |                       |
|                       | intentional, make     |                       |
|                       | sure there is a       |                       |
|                       | function call in the  |                       |
|                       | program, and make     |                       |
|                       | sure the flow of      |                       |
|                       | execution reaches it  |                       |
|                       | (see "Flow of         |                       |
|                       | Execution" below).    |                       |
|                       |                       |                       |
|                       | ### A.2.              |                       |
|                       | 2  My program hangs.  |                       |
|                       | {#sec239 .subsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1754} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1755} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1756} |                       |
|                       |                       |                       |
|                       | If a program stops    |                       |
|                       | and seems to be doing |                       |
|                       | nothing, it is        |                       |
|                       | "hanging". Often that |                       |
|                       | means that it is      |                       |
|                       | caught in an infinite |                       |
|                       | loop or infinite      |                       |
|                       | recursion.            |                       |
|                       |                       |                       |
|                       | -   If there is a     |                       |
|                       |     particular loop   |                       |
|                       |     that you suspect  |                       |
|                       |     is the problem,   |                       |
|                       |     add a             |                       |
|                       |     [print]{.c004}    |                       |
|                       |     statement         |                       |
|                       |     immediately       |                       |
|                       |     before the loop   |                       |
|                       |     that says         |                       |
|                       |     "entering the     |                       |
|                       |     loop" and another |                       |
|                       |     immediately after |                       |
|                       |     that says         |                       |
|                       |     "exiting the      |                       |
|                       |     loop".            |                       |
|                       |                       |                       |
|                       |     Run the program.  |                       |
|                       |     If you get the    |                       |
|                       |     first message and |                       |
|                       |     not the second,   |                       |
|                       |     you've got an     |                       |
|                       |     infinite loop. Go |                       |
|                       |     to the "Infinite  |                       |
|                       |     Loop" section     |                       |
|                       |     below.            |                       |
|                       |                       |                       |
|                       | -   Most of the time, |                       |
|                       |     an infinite       |                       |
|                       |     recursion will    |                       |
|                       |     cause the program |                       |
|                       |     to run for a      |                       |
|                       |     while and then    |                       |
|                       |     produce a         |                       |
|                       |     "RuntimeError:    |                       |
|                       |     Maximum recursion |                       |
|                       |     depth exceeded"   |                       |
|                       |     error. If that    |                       |
|                       |     happens, go to    |                       |
|                       |     the "Infinite     |                       |
|                       |     Recursion"        |                       |
|                       |     section below.    |                       |
|                       |                       |                       |
|                       |     If you are not    |                       |
|                       |     getting this      |                       |
|                       |     error but you     |                       |
|                       |     suspect there is  |                       |
|                       |     a problem with a  |                       |
|                       |     recursive method  |                       |
|                       |     or function, you  |                       |
|                       |     can still use the |                       |
|                       |     techniques in the |                       |
|                       |     "Infinite         |                       |
|                       |     Recursion"        |                       |
|                       |     section.          |                       |
|                       |                       |                       |
|                       | -   If neither of     |                       |
|                       |     those steps       |                       |
|                       |     works, start      |                       |
|                       |     testing other     |                       |
|                       |     loops and other   |                       |
|                       |     recursive         |                       |
|                       |     functions and     |                       |
|                       |     methods.          |                       |
|                       |                       |                       |
|                       | -   If that doesn't   |                       |
|                       |     work, then it is  |                       |
|                       |     possible that you |                       |
|                       |     don't understand  |                       |
|                       |     the flow of       |                       |
|                       |     execution in your |                       |
|                       |     program. Go to    |                       |
|                       |     the "Flow of      |                       |
|                       |     Execution"        |                       |
|                       |     section below.    |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | ### Infinite Loop {#s |                       |
|                       | ec240 .subsubsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1757} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1758} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1759} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1760} |                       |
|                       |                       |                       |
|                       | If you think you have |                       |
|                       | an infinite loop and  |                       |
|                       | you think you know    |                       |
|                       | what loop is causing  |                       |
|                       | the problem, add a    |                       |
|                       | [print]{.c004}        |                       |
|                       | statement at the end  |                       |
|                       | of the loop that      |                       |
|                       | prints the values of  |                       |
|                       | the variables in the  |                       |
|                       | condition and the     |                       |
|                       | value of the          |                       |
|                       | condition.            |                       |
|                       |                       |                       |
|                       | For example:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | wh                    |                       |
|                       | ile x > 0 and y < 0 : |                       |
|                       |                       |                       |
|                       |   # do something to x |                       |
|                       |                       |                       |
|                       |   # do something to y |                       |
|                       |                       |                       |
|                       |     print('x: ', x)   |                       |
|                       |     print('y: ', y)   |                       |
|                       |                       |                       |
|                       |    print("condition:  |                       |
|                       | ", (x > 0 and y < 0)) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now when you run the  |                       |
|                       | program, you will see |                       |
|                       | three lines of output |                       |
|                       | for each time through |                       |
|                       | the loop. The last    |                       |
|                       | time through the      |                       |
|                       | loop, the condition   |                       |
|                       | should be             |                       |
|                       | [False]{.c004}. If    |                       |
|                       | the loop keeps going, |                       |
|                       | you will be able to   |                       |
|                       | see the values of     |                       |
|                       | [x]{.c004} and        |                       |
|                       | [y]{.c004}, and you   |                       |
|                       | might figure out why  |                       |
|                       | they are not being    |                       |
|                       | updated correctly.    |                       |
|                       |                       |                       |
|                       | #### I                |                       |
|                       | nfinite Recursion {#s |                       |
|                       | ec241 .subsubsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1761} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1762} |                       |
|                       |                       |                       |
|                       | Most of the time,     |                       |
|                       | infinite recursion    |                       |
|                       | causes the program to |                       |
|                       | run for a while and   |                       |
|                       | then produce a        |                       |
|                       | [Maximum recursion    |                       |
|                       | depth                 |                       |
|                       | exceeded]{.c004}      |                       |
|                       | error.                |                       |
|                       |                       |                       |
|                       | If you suspect that a |                       |
|                       | function is causing   |                       |
|                       | an infinite           |                       |
|                       | recursion, make sure  |                       |
|                       | that there is a base  |                       |
|                       | case. There should be |                       |
|                       | some condition that   |                       |
|                       | causes the function   |                       |
|                       | to return without     |                       |
|                       | making a recursive    |                       |
|                       | invocation. If not,   |                       |
|                       | you need to rethink   |                       |
|                       | the algorithm and     |                       |
|                       | identify a base case. |                       |
|                       |                       |                       |
|                       | If there is a base    |                       |
|                       | case but the program  |                       |
|                       | doesn't seem to be    |                       |
|                       | reaching it, add a    |                       |
|                       | [print]{.c004}        |                       |
|                       | statement at the      |                       |
|                       | beginning of the      |                       |
|                       | function that prints  |                       |
|                       | the parameters. Now   |                       |
|                       | when you run the      |                       |
|                       | program, you will see |                       |
|                       | a few lines of output |                       |
|                       | every time the        |                       |
|                       | function is invoked,  |                       |
|                       | and you will see the  |                       |
|                       | parameter values. If  |                       |
|                       | the parameters are    |                       |
|                       | not moving toward the |                       |
|                       | base case, you will   |                       |
|                       | get some ideas about  |                       |
|                       | why not.              |                       |
|                       |                       |                       |
|                       | ####                  |                       |
|                       | Flow of Execution {#s |                       |
|                       | ec242 .subsubsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1763} |                       |
|                       |                       |                       |
|                       | If you are not sure   |                       |
|                       | how the flow of       |                       |
|                       | execution is moving   |                       |
|                       | through your program, |                       |
|                       | add [print]{.c004}    |                       |
|                       | statements to the     |                       |
|                       | beginning of each     |                       |
|                       | function with a       |                       |
|                       | message like          |                       |
|                       | "entering function    |                       |
|                       | [foo]{.c004}", where  |                       |
|                       | [foo]{.c004} is the   |                       |
|                       | name of the function. |                       |
|                       |                       |                       |
|                       | Now when you run the  |                       |
|                       | program, it will      |                       |
|                       | print a trace of each |                       |
|                       | function as it is     |                       |
|                       | invoked.              |                       |
|                       |                       |                       |
|                       | ### A.2.3  W          |                       |
|                       | hen I run the program |                       |
|                       |  I get an exception.  |                       |
|                       | {#sec243 .subsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1764} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1765} |                       |
|                       |                       |                       |
|                       | If something goes     |                       |
|                       | wrong during runtime, |                       |
|                       | Python prints a       |                       |
|                       | message that includes |                       |
|                       | the name of the       |                       |
|                       | exception, the line   |                       |
|                       | of the program where  |                       |
|                       | the problem occurred, |                       |
|                       | and a traceback.      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1766} |                       |
|                       |                       |                       |
|                       | The traceback         |                       |
|                       | identifies the        |                       |
|                       | function that is      |                       |
|                       | currently running,    |                       |
|                       | and then the function |                       |
|                       | that called it, and   |                       |
|                       | then the function     |                       |
|                       | that called *that*,   |                       |
|                       | and so on. In other   |                       |
|                       | words, it traces the  |                       |
|                       | sequence of function  |                       |
|                       | calls that got you to |                       |
|                       | where you are,        |                       |
|                       | including the line    |                       |
|                       | number in your file   |                       |
|                       | where each call       |                       |
|                       | occurred.             |                       |
|                       |                       |                       |
|                       | The first step is to  |                       |
|                       | examine the place in  |                       |
|                       | the program where the |                       |
|                       | error occurred and    |                       |
|                       | see if you can figure |                       |
|                       | out what happened.    |                       |
|                       | These are some of the |                       |
|                       | most common runtime   |                       |
|                       | errors:               |                       |
|                       |                       |                       |
|                       | [NameError:]{.c010}   |                       |
|                       | :   You are trying to |                       |
|                       |     use a variable    |                       |
|                       |     that doesn't      |                       |
|                       |     exist in the      |                       |
|                       |     current           |                       |
|                       |     environment.      |                       |
|                       |     Check if the name |                       |
|                       |     is spelled right, |                       |
|                       |     or at least       |                       |
|                       |     consistently. And |                       |
|                       |     remember that     |                       |
|                       |     local variables   |                       |
|                       |     are local; you    |                       |
|                       |     cannot refer to   |                       |
|                       |     them from outside |                       |
|                       |     the function      |                       |
|                       |     where they are    |                       |
|                       |     defined.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1767} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1768} |                       |
|                       |                       |                       |
|                       | [TypeError:]{.c010}   |                       |
|                       | :   There are several |                       |
|                       |     possible causes:  |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1769} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1770} |                       |
|                       |     -   You are       |                       |
|                       |         trying to use |                       |
|                       |         a value       |                       |
|                       |         improperly.   |                       |
|                       |         Example:      |                       |
|                       |         indexing a    |                       |
|                       |         string, list, |                       |
|                       |         or tuple with |                       |
|                       |         something     |                       |
|                       |         other than an |                       |
|                       |         integer.      |                       |
|                       |         [             |                       |
|                       | ]{#hevea_default1771} |                       |
|                       |     -   There is a    |                       |
|                       |         mismatch      |                       |
|                       |         between the   |                       |
|                       |         items in a    |                       |
|                       |         format string |                       |
|                       |         and the items |                       |
|                       |         passed for    |                       |
|                       |         conversion.   |                       |
|                       |         This can      |                       |
|                       |         happen if     |                       |
|                       |         either the    |                       |
|                       |         number of     |                       |
|                       |         items does    |                       |
|                       |         not match or  |                       |
|                       |         an invalid    |                       |
|                       |         conversion is |                       |
|                       |         called for.   |                       |
|                       |         [             |                       |
|                       | ]{#hevea_default1772} |                       |
|                       |         [             |                       |
|                       | ]{#hevea_default1773} |                       |
|                       |     -   You are       |                       |
|                       |         passing the   |                       |
|                       |         wrong number  |                       |
|                       |         of arguments  |                       |
|                       |         to a          |                       |
|                       |         function. For |                       |
|                       |         methods, look |                       |
|                       |         at the method |                       |
|                       |         definition    |                       |
|                       |         and check     |                       |
|                       |         that the      |                       |
|                       |         first         |                       |
|                       |         parameter is  |                       |
|                       |                       |                       |
|                       |        [self]{.c004}. |                       |
|                       |         Then look at  |                       |
|                       |         the method    |                       |
|                       |         invocation;   |                       |
|                       |         make sure you |                       |
|                       |         are invoking  |                       |
|                       |         the method on |                       |
|                       |         an object     |                       |
|                       |         with the      |                       |
|                       |         right type    |                       |
|                       |         and providing |                       |
|                       |         the other     |                       |
|                       |         arguments     |                       |
|                       |         correctly.    |                       |
|                       |                       |                       |
|                       | [KeyError:]{.c010}    |                       |
|                       | :   You are trying to |                       |
|                       |     access an element |                       |
|                       |     of a dictionary   |                       |
|                       |     using a key that  |                       |
|                       |     the dictionary    |                       |
|                       |     does not contain. |                       |
|                       |     If the keys are   |                       |
|                       |     strings, remember |                       |
|                       |     that              |                       |
|                       |     capitalization    |                       |
|                       |     matters.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1774} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1775} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1776} |                       |
|                       |                       |                       |
|                       | [At                   |                       |
|                       | tributeError:]{.c010} |                       |
|                       |                       |                       |
|                       | :   You are trying to |                       |
|                       |     access an         |                       |
|                       |     attribute or      |                       |
|                       |     method that does  |                       |
|                       |     not exist. Check  |                       |
|                       |     the spelling! You |                       |
|                       |     can use the       |                       |
|                       |     built-in function |                       |
|                       |     [vars]{.c004} to  |                       |
|                       |     list the          |                       |
|                       |     attributes that   |                       |
|                       |     do exist.         |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1777} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1778} |                       |
|                       |                       |                       |
|                       |     If an             |                       |
|                       |     AttributeError    |                       |
|                       |     indicates that an |                       |
|                       |     object has        |                       |
|                       |                       |                       |
|                       |    [NoneType]{.c004}, |                       |
|                       |     that means that   |                       |
|                       |     it is             |                       |
|                       |     [None]{.c004}. So |                       |
|                       |     the problem is    |                       |
|                       |     not the attribute |                       |
|                       |     name, but the     |                       |
|                       |     object.           |                       |
|                       |                       |                       |
|                       |     The reason the    |                       |
|                       |     object is none    |                       |
|                       |     might be that you |                       |
|                       |     forgot to return  |                       |
|                       |     a value from a    |                       |
|                       |     function; if you  |                       |
|                       |     get to the end of |                       |
|                       |     a function        |                       |
|                       |     without hitting a |                       |
|                       |     [return]{.c004}   |                       |
|                       |     statement, it     |                       |
|                       |     returns           |                       |
|                       |     [None]{.c004}.    |                       |
|                       |     Another common    |                       |
|                       |     cause is using    |                       |
|                       |     the result from a |                       |
|                       |     list method, like |                       |
|                       |     [sort]{.c004},    |                       |
|                       |     that returns      |                       |
|                       |     [None]{.c004}.    |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1779} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1780} |                       |
|                       |                       |                       |
|                       | [IndexError:]{.c010}  |                       |
|                       | :   The index you are |                       |
|                       |     using to access a |                       |
|                       |     list, string, or  |                       |
|                       |     tuple is greater  |                       |
|                       |     than its length   |                       |
|                       |     minus one.        |                       |
|                       |     Immediately       |                       |
|                       |     before the site   |                       |
|                       |     of the error, add |                       |
|                       |     a [print]{.c004}  |                       |
|                       |     statement to      |                       |
|                       |     display the value |                       |
|                       |     of the index and  |                       |
|                       |     the length of the |                       |
|                       |     array. Is the     |                       |
|                       |     array the right   |                       |
|                       |     size? Is the      |                       |
|                       |     index the right   |                       |
|                       |     value?            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1781} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1782} |                       |
|                       |                       |                       |
|                       | The Python debugger   |                       |
|                       | ([pdb]{.c004}) is     |                       |
|                       | useful for tracking   |                       |
|                       | down exceptions       |                       |
|                       | because it allows you |                       |
|                       | to examine the state  |                       |
|                       | of the program        |                       |
|                       | immediately before    |                       |
|                       | the error. You can    |                       |
|                       | read about            |                       |
|                       | [pdb]{.c004} at       |                       |
|                       | [[https://docs        |                       |
|                       | .python.org/3/library |                       |
|                       | /pdb.html]{.c004}](ht |                       |
|                       | tps://docs.python.org |                       |
|                       | /3/library/pdb.html). |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1783} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1784} |                       |
|                       |                       |                       |
|                       | ### A.2.4  I added    |                       |
|                       | so many [print]{.c004 |                       |
|                       | } statements I get in |                       |
|                       | undated with output.  |                       |
|                       | {#sec244 .subsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1785} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1786} |                       |
|                       |                       |                       |
|                       | One of the problems   |                       |
|                       | with using            |                       |
|                       | [print]{.c004}        |                       |
|                       | statements for        |                       |
|                       | debugging is that you |                       |
|                       | can end up buried in  |                       |
|                       | output. There are two |                       |
|                       | ways to proceed:      |                       |
|                       | simplify the output   |                       |
|                       | or simplify the       |                       |
|                       | program.              |                       |
|                       |                       |                       |
|                       | To simplify the       |                       |
|                       | output, you can       |                       |
|                       | remove or comment out |                       |
|                       | [print]{.c004}        |                       |
|                       | statements that       |                       |
|                       | aren't helping, or    |                       |
|                       | combine them, or      |                       |
|                       | format the output so  |                       |
|                       | it is easier to       |                       |
|                       | understand.           |                       |
|                       |                       |                       |
|                       | To simplify the       |                       |
|                       | program, there are    |                       |
|                       | several things you    |                       |
|                       | can do. First, scale  |                       |
|                       | down the problem the  |                       |
|                       | program is working    |                       |
|                       | on. For example, if   |                       |
|                       | you are searching a   |                       |
|                       | list, search a        |                       |
|                       | *small* list. If the  |                       |
|                       | program takes input   |                       |
|                       | from the user, give   |                       |
|                       | it the simplest input |                       |
|                       | that causes the       |                       |
|                       | problem.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1787} |                       |
|                       |                       |                       |
|                       | Second, clean up the  |                       |
|                       | program. Remove dead  |                       |
|                       | code and reorganize   |                       |
|                       | the program to make   |                       |
|                       | it as easy to read as |                       |
|                       | possible. For         |                       |
|                       | example, if you       |                       |
|                       | suspect that the      |                       |
|                       | problem is in a       |                       |
|                       | deeply nested part of |                       |
|                       | the program, try      |                       |
|                       | rewriting that part   |                       |
|                       | with simpler          |                       |
|                       | structure. If you     |                       |
|                       | suspect a large       |                       |
|                       | function, try         |                       |
|                       | splitting it into     |                       |
|                       | smaller functions and |                       |
|                       | testing them          |                       |
|                       | separately.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1788} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1789} |                       |
|                       |                       |                       |
|                       | Often the process of  |                       |
|                       | finding the minimal   |                       |
|                       | test case leads you   |                       |
|                       | to the bug. If you    |                       |
|                       | find that a program   |                       |
|                       | works in one          |                       |
|                       | situation but not in  |                       |
|                       | another, that gives   |                       |
|                       | you a clue about what |                       |
|                       | is going on.          |                       |
|                       |                       |                       |
|                       | Similarly, rewriting  |                       |
|                       | a piece of code can   |                       |
|                       | help you find subtle  |                       |
|                       | bugs. If you make a   |                       |
|                       | change that you think |                       |
|                       | shouldn't affect the  |                       |
|                       | program, and it does, |                       |
|                       | that can tip you off. |                       |
|                       |                       |                       |
|                       | ## A.3  Semantic erro |                       |
|                       | rs {#sec245 .section} |                       |
|                       |                       |                       |
|                       | In some ways,         |                       |
|                       | semantic errors are   |                       |
|                       | the hardest to debug, |                       |
|                       | because the           |                       |
|                       | interpreter provides  |                       |
|                       | no information about  |                       |
|                       | what is wrong. Only   |                       |
|                       | you know what the     |                       |
|                       | program is supposed   |                       |
|                       | to do.                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1790} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1791} |                       |
|                       |                       |                       |
|                       | The first step is to  |                       |
|                       | make a connection     |                       |
|                       | between the program   |                       |
|                       | text and the behavior |                       |
|                       | you are seeing. You   |                       |
|                       | need a hypothesis     |                       |
|                       | about what the        |                       |
|                       | program is actually   |                       |
|                       | doing. One of the     |                       |
|                       | things that makes     |                       |
|                       | that hard is that     |                       |
|                       | computers run so      |                       |
|                       | fast.                 |                       |
|                       |                       |                       |
|                       | You will often wish   |                       |
|                       | that you could slow   |                       |
|                       | the program down to   |                       |
|                       | human speed, and with |                       |
|                       | some debuggers you    |                       |
|                       | can. But the time it  |                       |
|                       | takes to insert a few |                       |
|                       | well-placed           |                       |
|                       | [print]{.c004}        |                       |
|                       | statements is often   |                       |
|                       | short compared to     |                       |
|                       | setting up the        |                       |
|                       | debugger, inserting   |                       |
|                       | and removing          |                       |
|                       | breakpoints, and      |                       |
|                       | "stepping" the        |                       |
|                       | program to where the  |                       |
|                       | error is occurring.   |                       |
|                       |                       |                       |
|                       | ### A.3.1  My p       |                       |
|                       | rogram doesn't work.  |                       |
|                       | {#sec246 .subsection} |                       |
|                       |                       |                       |
|                       | You should ask        |                       |
|                       | yourself these        |                       |
|                       | questions:            |                       |
|                       |                       |                       |
|                       | -   Is there          |                       |
|                       |     something the     |                       |
|                       |     program was       |                       |
|                       |     supposed to do    |                       |
|                       |     but which doesn't |                       |
|                       |     seem to be        |                       |
|                       |     happening? Find   |                       |
|                       |     the section of    |                       |
|                       |     the code that     |                       |
|                       |     performs that     |                       |
|                       |     function and make |                       |
|                       |     sure it is        |                       |
|                       |     executing when    |                       |
|                       |     you think it      |                       |
|                       |     should.           |                       |
|                       | -   Is something      |                       |
|                       |     happening that    |                       |
|                       |     shouldn't? Find   |                       |
|                       |     code in your      |                       |
|                       |     program that      |                       |
|                       |     performs that     |                       |
|                       |     function and see  |                       |
|                       |     if it is          |                       |
|                       |     executing when it |                       |
|                       |     shouldn't.        |                       |
|                       | -   Is a section of   |                       |
|                       |     code producing an |                       |
|                       |     effect that is    |                       |
|                       |     not what you      |                       |
|                       |     expected? Make    |                       |
|                       |     sure that you     |                       |
|                       |     understand the    |                       |
|                       |     code in question, |                       |
|                       |     especially if it  |                       |
|                       |     involves          |                       |
|                       |     functions or      |                       |
|                       |     methods in other  |                       |
|                       |     Python modules.   |                       |
|                       |     Read the          |                       |
|                       |     documentation for |                       |
|                       |     the functions you |                       |
|                       |     call. Try them    |                       |
|                       |     out by writing    |                       |
|                       |     simple test cases |                       |
|                       |     and checking the  |                       |
|                       |     results.          |                       |
|                       |                       |                       |
|                       | In order to program,  |                       |
|                       | you need a mental     |                       |
|                       | model of how programs |                       |
|                       | work. If you write a  |                       |
|                       | program that doesn't  |                       |
|                       | do what you expect,   |                       |
|                       | often the problem is  |                       |
|                       | not in the program;   |                       |
|                       | it's in your mental   |                       |
|                       | model.                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1792} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1793} |                       |
|                       |                       |                       |
|                       | The best way to       |                       |
|                       | correct your mental   |                       |
|                       | model is to break the |                       |
|                       | program into its      |                       |
|                       | components (usually   |                       |
|                       | the functions and     |                       |
|                       | methods) and test     |                       |
|                       | each component        |                       |
|                       | independently. Once   |                       |
|                       | you find the          |                       |
|                       | discrepancy between   |                       |
|                       | your model and        |                       |
|                       | reality, you can      |                       |
|                       | solve the problem.    |                       |
|                       |                       |                       |
|                       | Of course, you should |                       |
|                       | be building and       |                       |
|                       | testing components as |                       |
|                       | you develop the       |                       |
|                       | program. If you       |                       |
|                       | encounter a problem,  |                       |
|                       | there should be only  |                       |
|                       | a small amount of new |                       |
|                       | code that is not      |                       |
|                       | known to be correct.  |                       |
|                       |                       |                       |
|                       | ### A.3.2  I'         |                       |
|                       | ve got a big hairy ex |                       |
|                       | pression and it doesn |                       |
|                       | 't do what I expect.  |                       |
|                       | {#sec247 .subsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1794} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1795} |                       |
|                       |                       |                       |
|                       | Writing complex       |                       |
|                       | expressions is fine   |                       |
|                       | as long as they are   |                       |
|                       | readable, but they    |                       |
|                       | can be hard to debug. |                       |
|                       | It is often a good    |                       |
|                       | idea to break a       |                       |
|                       | complex expression    |                       |
|                       | into a series of      |                       |
|                       | assignments to        |                       |
|                       | temporary variables.  |                       |
|                       |                       |                       |
|                       | For example:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | se                    |                       |
|                       | lf.hands[i].addCard(s |                       |
|                       | elf.hands[self.findNe |                       |
|                       | ighbor(i)].popCard()) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This can be rewritten |                       |
|                       | as:                   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | neighbor =            |                       |
|                       |  self.findNeighbor(i) |                       |
|                       | p                     |                       |
|                       | ickedCard = self.hand |                       |
|                       | s[neighbor].popCard() |                       |
|                       | self.hands[i          |                       |
|                       | ].addCard(pickedCard) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The explicit version  |                       |
|                       | is easier to read     |                       |
|                       | because the variable  |                       |
|                       | names provide         |                       |
|                       | additional            |                       |
|                       | documentation, and it |                       |
|                       | is easier to debug    |                       |
|                       | because you can check |                       |
|                       | the types of the      |                       |
|                       | intermediate          |                       |
|                       | variables and display |                       |
|                       | their values.         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1796} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1797} |                       |
|                       |                       |                       |
|                       | Another problem that  |                       |
|                       | can occur with big    |                       |
|                       | expressions is that   |                       |
|                       | the order of          |                       |
|                       | evaluation may not be |                       |
|                       | what you expect. For  |                       |
|                       | example, if you are   |                       |
|                       | translating the       |                       |
|                       | expression            |                       |
|                       | [x]{.c009}/2 π into   |                       |
|                       | Python, you might     |                       |
|                       | write:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | y = x / 2 * math.pi   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | That is not correct   |                       |
|                       | because               |                       |
|                       | multiplication and    |                       |
|                       | division have the     |                       |
|                       | same precedence and   |                       |
|                       | are evaluated from    |                       |
|                       | left to right. So     |                       |
|                       | this expression       |                       |
|                       | computes [x]{.c009} π |                       |
|                       | / 2.                  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1798} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1799} |                       |
|                       |                       |                       |
|                       | A good way to debug   |                       |
|                       | expressions is to add |                       |
|                       | parentheses to make   |                       |
|                       | the order of          |                       |
|                       | evaluation explicit:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |                       |                       |
|                       | y = x / (2 * math.pi) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Whenever you are not  |                       |
|                       | sure of the order of  |                       |
|                       | evaluation, use       |                       |
|                       | parentheses. Not only |                       |
|                       | will the program be   |                       |
|                       | correct (in the sense |                       |
|                       | of doing what you     |                       |
|                       | intended), it will    |                       |
|                       | also be more readable |                       |
|                       | for other people who  |                       |
|                       | haven't memorized the |                       |
|                       | order of operations.  |                       |
|                       |                       |                       |
|                       | ###                   |                       |
|                       |  A.3.3  I've got a fu |                       |
|                       | nction that doesn't r |                       |
|                       | eturn what I expect.  |                       |
|                       | {#sec248 .subsection} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1800} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1801} |                       |
|                       |                       |                       |
|                       | If you have a         |                       |
|                       | [return]{.c004}       |                       |
|                       | statement with a      |                       |
|                       | complex expression,   |                       |
|                       | you don't have a      |                       |
|                       | chance to print the   |                       |
|                       | result before         |                       |
|                       | returning. Again, you |                       |
|                       | can use a temporary   |                       |
|                       | variable. For         |                       |
|                       | example, instead of:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | return self.han       |                       |
|                       | ds[i].removeMatches() |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | you could write:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | count = self.han      |                       |
|                       | ds[i].removeMatches() |                       |
|                       | return count          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now you have the      |                       |
|                       | opportunity to        |                       |
|                       | display the value of  |                       |
|                       | [count]{.c004} before |                       |
|                       | returning.            |                       |
|                       |                       |                       |
|                       | ### A.3.4             |                       |
|                       | I'm really, really st |                       |
|                       | uck and I need help.  |                       |
|                       | {#sec249 .subsection} |                       |
|                       |                       |                       |
|                       | First, try getting    |                       |
|                       | away from the         |                       |
|                       | computer for a few    |                       |
|                       | minutes. Computers    |                       |
|                       | emit waves that       |                       |
|                       | affect the brain,     |                       |
|                       | causing these         |                       |
|                       | symptoms:             |                       |
|                       |                       |                       |
|                       | -   Frustration and   |                       |
|                       |     rage.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1802} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1803} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1804} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1805} |                       |
|                       | -   Superstitious     |                       |
|                       |     beliefs ("the     |                       |
|                       |     computer hates    |                       |
|                       |     me") and magical  |                       |
|                       |     thinking ("the    |                       |
|                       |     program only      |                       |
|                       |     works when I wear |                       |
|                       |     my hat            |                       |
|                       |     backward").       |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1806} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1807} |                       |
|                       | -   Random walk       |                       |
|                       |     programming (the  |                       |
|                       |     attempt to        |                       |
|                       |     program by        |                       |
|                       |     writing every     |                       |
|                       |     possible program  |                       |
|                       |     and choosing the  |                       |
|                       |     one that does the |                       |
|                       |     right thing).     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1808} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1809} |                       |
|                       |                       |                       |
|                       | If you find yourself  |                       |
|                       | suffering from any of |                       |
|                       | these symptoms, get   |                       |
|                       | up and go for a walk. |                       |
|                       | When you are calm,    |                       |
|                       | think about the       |                       |
|                       | program. What is it   |                       |
|                       | doing? What are some  |                       |
|                       | possible causes of    |                       |
|                       | that behavior? When   |                       |
|                       | was the last time you |                       |
|                       | had a working         |                       |
|                       | program, and what did |                       |
|                       | you do next?          |                       |
|                       |                       |                       |
|                       | Sometimes it just     |                       |
|                       | takes time to find a  |                       |
|                       | bug. I often find     |                       |
|                       | bugs when I am away   |                       |
|                       | from the computer and |                       |
|                       | let my mind wander.   |                       |
|                       | Some of the best      |                       |
|                       | places to find bugs   |                       |
|                       | are trains, showers,  |                       |
|                       | and in bed, just      |                       |
|                       | before you fall       |                       |
|                       | asleep.               |                       |
|                       |                       |                       |
|                       | ### A.3.5  No,        |                       |
|                       |  I really need help.  |                       |
|                       | {#sec250 .subsection} |                       |
|                       |                       |                       |
|                       | It happens. Even the  |                       |
|                       | best programmers      |                       |
|                       | occasionally get      |                       |
|                       | stuck. Sometimes you  |                       |
|                       | work on a program so  |                       |
|                       | long that you can't   |                       |
|                       | see the error. You    |                       |
|                       | need a fresh pair of  |                       |
|                       | eyes.                 |                       |
|                       |                       |                       |
|                       | Before you bring      |                       |
|                       | someone else in, make |                       |
|                       | sure you are          |                       |
|                       | prepared. Your        |                       |
|                       | program should be as  |                       |
|                       | simple as possible,   |                       |
|                       | and you should be     |                       |
|                       | working on the        |                       |
|                       | smallest input that   |                       |
|                       | causes the error. You |                       |
|                       | should have           |                       |
|                       | [print]{.c004}        |                       |
|                       | statements in the     |                       |
|                       | appropriate places    |                       |
|                       | (and the output they  |                       |
|                       | produce should be     |                       |
|                       | comprehensible). You  |                       |
|                       | should understand the |                       |
|                       | problem well enough   |                       |
|                       | to describe it        |                       |
|                       | concisely.            |                       |
|                       |                       |                       |
|                       | When you bring        |                       |
|                       | someone in to help,   |                       |
|                       | be sure to give them  |                       |
|                       | the information they  |                       |
|                       | need:                 |                       |
|                       |                       |                       |
|                       | -   If there is an    |                       |
|                       |     error message,    |                       |
|                       |     what is it and    |                       |
|                       |     what part of the  |                       |
|                       |     program does it   |                       |
|                       |     indicate?         |                       |
|                       | -   What was the last |                       |
|                       |     thing you did     |                       |
|                       |     before this error |                       |
|                       |     occurred? What    |                       |
|                       |     were the last     |                       |
|                       |     lines of code     |                       |
|                       |     that you wrote,   |                       |
|                       |     or what is the    |                       |
|                       |     new test case     |                       |
|                       |     that fails?       |                       |
|                       | -   What have you     |                       |
|                       |     tried so far, and |                       |
|                       |     what have you     |                       |
|                       |     learned?          |                       |
|                       |                       |                       |
|                       | When you find the     |                       |
|                       | bug, take a second to |                       |
|                       | think about what you  |                       |
|                       | could have done to    |                       |
|                       | find it faster. Next  |                       |
|                       | time you see          |                       |
|                       | something similar,    |                       |
|                       | you will be able to   |                       |
|                       | find the bug more     |                       |
|                       | quickly.              |                       |
|                       |                       |                       |
|                       | Remember, the goal is |                       |
|                       | not just to make the  |                       |
|                       | program work. The     |                       |
|                       | goal is to learn how  |                       |
|                       | to make the program   |                       |
|                       | work.                 |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2020.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2022.html)
---
generator: hevea 2.32
title: Analysis of Algorithms
---

[![Previous](back.png)](thinkpython2021.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2023.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Appendix B          | to support my books,  |
|                       |  Analysis of Algorith | you can use the       |
|                       | ms {#sec251 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | []{#algorithms}       | you!                  |
|                       |                       |                       |
|                       | > This appendix is an |   -----------         |
|                       | > edited excerpt from | --------------------- |
|                       | > [Think              | --------------------- |
|                       | > Complexity]{.c009}, | --------------------- |
|                       | > by Allen B. Downey, | --------------------- |
|                       | > also published by   |   Pay what you want:  |
|                       | > O'Reilly Media      |   Small \$1           |
|                       | > (2012). When you    | .00 USD Medium \$5.00 |
|                       | > are done with this  |  USD Large \$10.00 US |
|                       | > book, you might     | D X-Large \$20.00 USD |
|                       | > want to move on to  |  XX-Large \$50.00 USD |
|                       | > that one.           |   -----------         |
|                       |                       | --------------------- |
|                       | [Analysis of          | --------------------- |
|                       | algorithms]{.c010} is | --------------------- |
|                       | a branch of computer  | --------------------- |
|                       | science that studies  |                       |
|                       | the performance of    | ![](                  |
|                       | algorithms,           | https://www.paypalobj |
|                       | especially their run  | ects.com/en_US/i/scr/ |
|                       | time and space        | pixel.gif){border="0" |
|                       | requirements. See     | width="1" height="1"} |
|                       | [[http://en           |                       |
|                       | .wikipedia.org/wiki/A | ####                  |
|                       | nalysis_of_algorithms | Are you using one of  |
|                       | ]{.c004}](http://en.w | our books in a class? |
|                       | ikipedia.org/wiki/Ana |                       |
|                       | lysis_of_algorithms). | We\'d like to know    |
|                       | [                     | about it. Please      |
|                       | ]{#hevea_default1810} | consider filling out  |
|                       | [                     | [this short           |
|                       | ]{#hevea_default1811} | survey](http://s      |
|                       |                       | preadsheets.google.co |
|                       | The practical goal of | m/viewform?formkey=dC |
|                       | algorithm analysis is | 0tNUZkMjBEdXVoRGljNm9 |
|                       | to predict the        | FRmlTMHc6MA){onclick= |
|                       | performance of        | "javascript: pageTrac |
|                       | different algorithms  | ker._trackPageview('/ |
|                       | in order to guide     | outbound/survey');"}. |
|                       | design decisions.     |                       |
|                       |                       | \                     |
|                       | During the 2008       |                       |
|                       | United States         | [Think                |
|                       | Presidential          | DSP](http             |
|                       | Campaign, candidate   | ://www.amazon.com/gp/ |
|                       | Barack Obama was      | product/1491938455/re |
|                       | asked to perform an   | f=as_li_tl?ie=UTF8&ca |
|                       | impromptu analysis    | mp=1789&creative=9325 |
|                       | when he visited       | &creativeASIN=1491938 |
|                       | Google. Chief         | 455&linkCode=as2&tag= |
|                       | executive Eric        | greenteapre01-20&link |
|                       | Schmidt jokingly      | Id=2JJH4SWCAVVYSQHO){ |
|                       | asked him for "the    | rel="nofollow"}![](ht |
|                       | most efficient way to | tp://ir-na.amazon-ads |
|                       | sort a million 32-bit | ystem.com/e/ir?t=gree |
|                       | integers." Obama had  | nteapre01-20&l=as2&o= |
|                       | apparently been       | 1&a=1491938455){.c003 |
|                       | tipped off, because   | width="1" height="1"  |
|                       | he quickly replied,   | border="0"}           |
|                       | "I think the bubble   |                       |
|                       | sort would be the     | [                     |
|                       | wrong way to go." See | ![](http://ws-na.amaz |
|                       | [[http://www.y        | on-adsystem.com/widge |
|                       | outube.com/watch?v=k4 | ts/q?_encoding=UTF8&A |
|                       | RRi_ntQc8]{.c004}](ht | SIN=1491938455&Format |
|                       | tp://www.youtube.com/ | =_SL160_&ID=AsinImage |
|                       | watch?v=k4RRi_ntQc8). | &MarketPlace=US&Servi |
|                       | [                     | ceVersion=20070822&WS |
|                       | ]{#hevea_default1812} | =1&tag=greenteapre01- |
|                       | [                     | 20){border="0"}](http |
|                       | ]{#hevea_default1813} | ://www.amazon.com/gp/ |
|                       | [                     | product/1491938455/re |
|                       | ]{#hevea_default1814} | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | This is true: bubble  | &creativeASIN=1491938 |
|                       | sort is conceptually  | 455&linkCode=as2&tag= |
|                       | simple but slow for   | greenteapre01-20&link |
|                       | large datasets. The   | Id=CTV7PDT7E5EGGJUM){ |
|                       | answer Schmidt was    | rel="nofollow"}![](ht |
|                       | probably looking for  | tp://ir-na.amazon-ads |
|                       | is "radix sort"       | ystem.com/e/ir?t=gree |
|                       | ([[http://            | nteapre01-20&l=as2&o= |
|                       | en.wikipedia.org/wiki | 1&a=1491938455){.c003 |
|                       | /Radix_sort]{.c004}]( | width="1" height="1"  |
|                       | http://en.wikipedia.o | border="0"}           |
|                       | rg/wiki/Radix_sort))^ |                       |
|                       | [1](#note2){#text2}^. | [Think                |
|                       | [                     | Java](http            |
|                       | ]{#hevea_default1815} | ://www.amazon.com/gp/ |
|                       |                       | product/1491929561/re |
|                       | The goal of algorithm | f=as_li_tl?ie=UTF8&ca |
|                       | analysis is to make   | mp=1789&creative=9325 |
|                       | meaningful            | &creativeASIN=1491929 |
|                       | comparisons between   | 561&linkCode=as2&tag= |
|                       | algorithms, but there | greenteapre01-20&link |
|                       | are some problems:    | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | [                     | rel="nofollow"}![](ht |
|                       | ]{#hevea_default1816} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | -   The relative      | nteapre01-20&l=as2&o= |
|                       |     performance of    | 1&a=1491929561){.c003 |
|                       |     the algorithms    | width="1" height="1"  |
|                       |     might depend on   | border="0"}           |
|                       |     characteristics   |                       |
|                       |     of the hardware,  | [                     |
|                       |     so one algorithm  | ![](http://ws-na.amaz |
|                       |     might be faster   | on-adsystem.com/widge |
|                       |     on Machine A,     | ts/q?_encoding=UTF8&A |
|                       |     another on        | SIN=1491929561&Format |
|                       |     Machine B. The    | =_SL160_&ID=AsinImage |
|                       |     general solution  | &MarketPlace=US&Servi |
|                       |     to this problem   | ceVersion=20070822&WS |
|                       |     is to specify a   | =1&tag=greenteapre01- |
|                       |     [machine          | 20){border="0"}](http |
|                       |     model]{.c010} and | ://www.amazon.com/gp/ |
|                       |     analyze the       | product/1491929561/re |
|                       |     number of steps,  | f=as_li_tl?ie=UTF8&ca |
|                       |     or operations, an | mp=1789&creative=9325 |
|                       |     algorithm         | &creativeASIN=1491929 |
|                       |     requires under a  | 561&linkCode=as2&tag= |
|                       |     given model.      | greenteapre01-20&link |
|                       |     [                 | Id=PT77ANWARUNNU3UK){ |
|                       | ]{#hevea_default1817} | rel="nofollow"}![](ht |
|                       | -   Relative          | tp://ir-na.amazon-ads |
|                       |     performance might | ystem.com/e/ir?t=gree |
|                       |     depend on the     | nteapre01-20&l=as2&o= |
|                       |     details of the    | 1&a=1491929561){.c003 |
|                       |     dataset. For      | width="1" height="1"  |
|                       |     example, some     | border="0"}           |
|                       |     sorting           |                       |
|                       |     algorithms run    | [Think                |
|                       |     faster if the     | Bay                   |
|                       |     data are already  | es](http://www.amazon |
|                       |     partially sorted; | .com/gp/product/14493 |
|                       |     other algorithms  | 70780/ref=as_li_qf_sp |
|                       |     run slower in     | _asin_tl?ie=UTF8&camp |
|                       |     this case. A      | =1789&creative=9325&c |
|                       |     common way to     | reativeASIN=144937078 |
|                       |     avoid this        | 0&linkCode=as2&tag=gr |
|                       |     problem is to     | eenteapre01-20)![](ht |
|                       |     analyze the       | tp://ir-na.amazon-ads |
|                       |     [worst            | ystem.com/e/ir?t=gree |
|                       |     case]{.c010}      | nteapre01-20&l=as2&o= |
|                       |     scenario. It is   | 1&a=1449370780){.c003 |
|                       |     sometimes useful  | width="1" height="1"  |
|                       |     to analyze        | border="0"}           |
|                       |     average case      |                       |
|                       |     performance, but  | [![](http://ws        |
|                       |     that's usually    | -na.amazon-adsystem.c |
|                       |     harder, and it    | om/widgets/q?_encodin |
|                       |     might not be      | g=UTF8&ASIN=144937078 |
|                       |     obvious what set  | 0&Format=_SL160_&ID=A |
|                       |     of cases to       | sinImage&MarketPlace= |
|                       |     average over.     | US&ServiceVersion=200 |
|                       |     [                 | 70822&WS=1&tag=greent |
|                       | ]{#hevea_default1818} | eapre01-20){border="0 |
|                       |     [                 | "}](http://www.amazon |
|                       | ]{#hevea_default1819} | .com/gp/product/14493 |
|                       | -   Relative          | 70780/ref=as_li_qf_sp |
|                       |     performance also  | _asin_il?ie=UTF8&camp |
|                       |     depends on the    | =1789&creative=9325&c |
|                       |     size of the       | reativeASIN=144937078 |
|                       |     problem. A        | 0&linkCode=as2&tag=gr |
|                       |     sorting algorithm | eenteapre01-20)![](ht |
|                       |     that is fast for  | tp://ir-na.amazon-ads |
|                       |     small lists might | ystem.com/e/ir?t=gree |
|                       |     be slow for long  | nteapre01-20&l=as2&o= |
|                       |     lists. The usual  | 1&a=1449370780){.c003 |
|                       |     solution to this  | width="1" height="1"  |
|                       |     problem is to     | border="0"}           |
|                       |     express run time  |                       |
|                       |     (or number of     | [Think Python         |
|                       |     operations) as a  | 2e](http              |
|                       |     function of       | ://www.amazon.com/gp/ |
|                       |     problem size, and | product/1491939362/re |
|                       |     group functions   | f=as_li_tl?ie=UTF8&ca |
|                       |     into categories   | mp=1789&creative=9325 |
|                       |     depending on how  | &creativeASIN=1491939 |
|                       |     quickly they grow | 362&linkCode=as2&tag= |
|                       |     as problem size   | greenteapre01-20&link |
|                       |     increases.        | Id=FJKSQ3IHEMY2F2VA){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | The good thing about  | tp://ir-na.amazon-ads |
|                       | this kind of          | ystem.com/e/ir?t=gree |
|                       | comparison is that it | nteapre01-20&l=as2&o= |
|                       | lends itself to       | 1&a=1491939362){.c003 |
|                       | simple classification | width="1" height="1"  |
|                       | of algorithms. For    | border="0"}           |
|                       | example, if I know    |                       |
|                       | that the run time of  | [                     |
|                       | Algorithm A tends to  | ![](http://ws-na.amaz |
|                       | be proportional to    | on-adsystem.com/widge |
|                       | the size of the       | ts/q?_encoding=UTF8&A |
|                       | input, [n]{.c009},    | SIN=1491939362&Format |
|                       | and Algorithm B tends | =_SL160_&ID=AsinImage |
|                       | to be proportional to | &MarketPlace=US&Servi |
|                       | [n]{.c009}^2^, then I | ceVersion=20070822&WS |
|                       | expect A to be faster | =1&tag=greenteapre01- |
|                       | than B, at least for  | 20){border="0"}](http |
|                       | large values of       | ://www.amazon.com/gp/ |
|                       | [n]{.c009}.           | product/1491939362/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | This kind of analysis | mp=1789&creative=9325 |
|                       | comes with some       | &creativeASIN=1491939 |
|                       | caveats, but we'll    | 362&linkCode=as2&tag= |
|                       | get to that later.    | greenteapre01-20&link |
|                       |                       | Id=ZZ454DLQ3IXDHNHX){ |
|                       | ## B.1  Order of grow | rel="nofollow"}![](ht |
|                       | th {#sec252 .section} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | Suppose you have      | nteapre01-20&l=as2&o= |
|                       | analyzed two          | 1&a=1491939362){.c003 |
|                       | algorithms and        | width="1" height="1"  |
|                       | expressed their run   | border="0"}           |
|                       | times in terms of the |                       |
|                       | size of the input:    | [Think Stats          |
|                       | Algorithm A takes     | 2e](http://ww         |
|                       | 100[n]{.c009}+1 steps | w.amazon.com/gp/produ |
|                       | to solve a problem    | ct/1491907339/ref=as_ |
|                       | with size [n]{.c009}; | li_tl?ie=UTF8&camp=17 |
|                       | Algorithm B takes     | 89&creative=9325&crea |
|                       | [n]{.c009}^2^ +       | tiveASIN=1491907339&l |
|                       | [n]{.c009} + 1 steps. | inkCode=as2&tag=green |
|                       | [                     | teapre01-20&linkId=O7 |
|                       | ]{#hevea_default1820} | WYM6H6YBYUFNWU)![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | The following table   | ystem.com/e/ir?t=gree |
|                       | shows the run time of | nteapre01-20&l=as2&o= |
|                       | these algorithms for  | 1&a=1491907339){.c003 |
|                       | different problem     | width="1" height="1"  |
|                       | sizes:                | border="0"}           |
|                       |                       |                       |
|                       |   -------- ------     | [![](h                |
|                       | ------- ------------- | ttp://ws-na.amazon-ad |
|                       |   Input    Run        | system.com/widgets/q? |
|                       | time of   Run time of | _encoding=UTF8&ASIN=1 |
|                       |   size     Algo       | 491907339&Format=_SL1 |
|                       | rithm A   Algorithm B | 60_&ID=AsinImage&Mark |
|                       |   10                  | etPlace=US&ServiceVer |
|                       |     1 001         111 | sion=20070822&WS=1&ta |
|                       |   100                 | g=greenteapre01-20){b |
|                       |  10 001        10 101 | order="0"}](http://ww |
|                       |   1 000    10         | w.amazon.com/gp/produ |
|                       | 0 001       1 001 001 | ct/1491907339/ref=as_ |
|                       |   10 000   1 00       | li_tl?ie=UTF8&camp=17 |
|                       | 0 001     100 010 001 | 89&creative=9325&crea |
|                       |   -------- ------     | tiveASIN=1491907339&l |
|                       | ------- ------------- | inkCode=as2&tag=green |
|                       |                       | teapre01-20&linkId=JV |
|                       | At [n]{.c009}=10,     | SYKQHYSUIEYRHL)![](ht |
|                       | Algorithm A looks     | tp://ir-na.amazon-ads |
|                       | pretty bad; it takes  | ystem.com/e/ir?t=gree |
|                       | almost 10 times       | nteapre01-20&l=as2&o= |
|                       | longer than Algorithm | 1&a=1491907339){.c003 |
|                       | B. But for            | width="1" height="1"  |
|                       | [n]{.c009}=100 they   | border="0"}           |
|                       | are about the same,   |                       |
|                       | and for larger values | [Think                |
|                       | A is much better.     | Complexity](http      |
|                       |                       | ://www.amazon.com/gp/ |
|                       | The fundamental       | product/1449314635/re |
|                       | reason is that for    | f=as_li_tf_tl?ie=UTF8 |
|                       | large values of       | &tag=greenteapre01-20 |
|                       | [n]{.c009}, any       | &linkCode=as2&camp=17 |
|                       | function that         | 89&creative=9325&crea |
|                       | contains an           | tiveASIN=1449314635)! |
|                       | [n]{.c009}^2^ term    | [](http://www.assoc-a |
|                       | will grow faster than | mazon.com/e/ir?t=gree |
|                       | a function whose      | nteapre01-20&l=as2&o= |
|                       | leading term is       | 1&a=1449314635){.c003 |
|                       | [n]{.c009}. The       | width="1" height="1"  |
|                       | [leading term]{.c010} | border="0"}           |
|                       | is the term with the  |                       |
|                       | highest exponent.     | [                     |
|                       | [                     | ![](http://ws-na.amaz |
|                       | ]{#hevea_default1821} | on-adsystem.com/widge |
|                       | [                     | ts/q?_encoding=UTF8&A |
|                       | ]{#hevea_default1822} | SIN=1449314635&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | For Algorithm A, the  | &MarketPlace=US&Servi |
|                       | leading term has a    | ceVersion=20070822&WS |
|                       | large coefficient,    | =1&tag=greenteapre01- |
|                       | 100, which is why B   | 20){border="0"}](http |
|                       | does better than A    | ://www.amazon.com/gp/ |
|                       | for small [n]{.c009}. | product/1449314635/re |
|                       | But regardless of the | f=as_li_tf_il?ie=UTF8 |
|                       | coefficients, there   | &camp=1789&creative=9 |
|                       | will always be some   | 325&creativeASIN=1449 |
|                       | value of [n]{.c009}   | 314635&linkCode=as2&t |
|                       | where [a n]{.c009}^2^ | ag=greenteapre01-20)! |
|                       | \> [b n]{.c009}, for  | [](http://www.assoc-a |
|                       | any values of         | mazon.com/e/ir?t=gree |
|                       | [a]{.c009} and        | nteapre01-20&l=as2&o= |
|                       | [b]{.c009}.           | 1&a=1449314635){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1823} | border="0"}           |
|                       |                       |                       |
|                       | The same argument     |                       |
|                       | applies to the        |                       |
|                       | non-leading terms.    |                       |
|                       | Even if the run time  |                       |
|                       | of Algorithm A were   |                       |
|                       | [n]{.c009}+1000000,   |                       |
|                       | it would still be     |                       |
|                       | better than Algorithm |                       |
|                       | B for sufficiently    |                       |
|                       | large [n]{.c009}.     |                       |
|                       |                       |                       |
|                       | In general, we expect |                       |
|                       | an algorithm with a   |                       |
|                       | smaller leading term  |                       |
|                       | to be a better        |                       |
|                       | algorithm for large   |                       |
|                       | problems, but for     |                       |
|                       | smaller problems,     |                       |
|                       | there may be a        |                       |
|                       | [crossover            |                       |
|                       | point]{.c010} where   |                       |
|                       | another algorithm is  |                       |
|                       | better. The location  |                       |
|                       | of the crossover      |                       |
|                       | point depends on the  |                       |
|                       | details of the        |                       |
|                       | algorithms, the       |                       |
|                       | inputs, and the       |                       |
|                       | hardware, so it is    |                       |
|                       | usually ignored for   |                       |
|                       | purposes of           |                       |
|                       | algorithmic analysis. |                       |
|                       | But that doesn't mean |                       |
|                       | you can forget about  |                       |
|                       | it.                   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1824} |                       |
|                       |                       |                       |
|                       | If two algorithms     |                       |
|                       | have the same leading |                       |
|                       | order term, it is     |                       |
|                       | hard to say which is  |                       |
|                       | better; again, the    |                       |
|                       | answer depends on the |                       |
|                       | details. So for       |                       |
|                       | algorithmic analysis, |                       |
|                       | functions with the    |                       |
|                       | same leading term are |                       |
|                       | considered            |                       |
|                       | equivalent, even if   |                       |
|                       | they have different   |                       |
|                       | coefficients.         |                       |
|                       |                       |                       |
|                       | An [order of          |                       |
|                       | growth]{.c010} is a   |                       |
|                       | set of functions      |                       |
|                       | whose growth behavior |                       |
|                       | is considered         |                       |
|                       | equivalent. For       |                       |
|                       | example, 2[n]{.c009}, |                       |
|                       | 100[n]{.c009} and     |                       |
|                       | [n]{.c009}+1 belong   |                       |
|                       | to the same order of  |                       |
|                       | growth, which is      |                       |
|                       | written               |                       |
|                       | [                     |                       |
|                       | O]{.c009}([n]{.c009}) |                       |
|                       | in [Big-Oh            |                       |
|                       | notation]{.c010} and  |                       |
|                       | often called          |                       |
|                       | [linear]{.c010}       |                       |
|                       | because every         |                       |
|                       | function in the set   |                       |
|                       | grows linearly with   |                       |
|                       | [n]{.c009}.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1825} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1826} |                       |
|                       |                       |                       |
|                       | All functions with    |                       |
|                       | the leading term      |                       |
|                       | [n]{.c009}^2^ belong  |                       |
|                       | to                    |                       |
|                       | [O]{.                 |                       |
|                       | c009}([n]{.c009}^2^); |                       |
|                       | they are called       |                       |
|                       | [quadratic]{.c010}.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1827} |                       |
|                       |                       |                       |
|                       | The following table   |                       |
|                       | shows some of the     |                       |
|                       | orders of growth that |                       |
|                       | appear most commonly  |                       |
|                       | in algorithmic        |                       |
|                       | analysis, in          |                       |
|                       | increasing order of   |                       |
|                       | badness.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1828} |                       |
|                       |                       |                       |
|                       |   --                  |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       | ------- ------------- |                       |
|                       | --------------------- |                       |
|                       |   Order of            |                       |
|                       |                       |                       |
|                       |                  Name |                       |
|                       |   growth              |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |   [O]{.c009}(1)       |                       |
|                       |                       |                       |
|                       |              constant |                       |
|                       |                       |                       |
|                       | [O]{.c009}(log~[b]{.c |                       |
|                       | 009}~ [n]{.c009})     |                       |
|                       |           logarithmic |                       |
|                       |  (for any [b]{.c009}) |                       |
|                       |   [O]{.c009}([n]{.    |                       |
|                       | c009})                |                       |
|                       |                linear |                       |
|                       |   [                   |                       |
|                       | O]{.c009}([n]{.c009}  |                       |
|                       | log~[b]{.c009}~ [n]{. |                       |
|                       | c009})   linearithmic |                       |
|                       |   [O]{.c009}([n]{.c00 |                       |
|                       | 9}^2^)                |                       |
|                       |             quadratic |                       |
|                       |   [O]{.c009}([n]{     |                       |
|                       | .c009}^3^)            |                       |
|                       |                 cubic |                       |
|                       |                       |                       |
|                       | [O]{.c009}([c]{.c009} |                       |
|                       | ^[n]{.c009}^)         |                       |
|                       |           exponential |                       |
|                       |  (for any [c]{.c009}) |                       |
|                       |   --                  |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       | ------- ------------- |                       |
|                       | --------------------- |                       |
|                       |                       |                       |
|                       | For the logarithmic   |                       |
|                       | terms, the base of    |                       |
|                       | the logarithm doesn't |                       |
|                       | matter; changing      |                       |
|                       | bases is the          |                       |
|                       | equivalent of         |                       |
|                       | multiplying by a      |                       |
|                       | constant, which       |                       |
|                       | doesn't change the    |                       |
|                       | order of growth.      |                       |
|                       | Similarly, all        |                       |
|                       | exponential functions |                       |
|                       | belong to the same    |                       |
|                       | order of growth       |                       |
|                       | regardless of the     |                       |
|                       | base of the exponent. |                       |
|                       | Exponential functions |                       |
|                       | grow very quickly, so |                       |
|                       | exponential           |                       |
|                       | algorithms are only   |                       |
|                       | useful for small      |                       |
|                       | problems.             |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1829} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1830} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Read the Wikipedia   |                       |
|                       | page on Big-Oh        |                       |
|                       | notation at*          |                       |
|                       | [*[http://en.wiki     |                       |
|                       | pedia.org/wiki/Big_O_ |                       |
|                       | notation]{.c004}*](ht |                       |
|                       | tp://en.wikipedia.org |                       |
|                       | /wiki/Big_O_notation) |                       |
|                       | *and answer the       |                       |
|                       | following questions:* |                       |
|                       |                       |                       |
|                       | 1.  *What is the      |                       |
|                       |     order of growth   |                       |
|                       |     of*               |                       |
|                       |     [n]{.c009}^3^ +   |                       |
|                       |     [n]{.c009}^2^*?   |                       |
|                       |     What about*       |                       |
|                       |     1000000           |                       |
|                       |     [n]{.c009}^3^ +   |                       |
|                       |     [n]{.c009}^2^*?   |                       |
|                       |     What about*       |                       |
|                       |     [n]{.c009}^3^ +   |                       |
|                       |     1000000           |                       |
|                       |     [n]{.c009}^2^*?*  |                       |
|                       | 2.  *What is the      |                       |
|                       |     order of growth   |                       |
|                       |     of*               |                       |
|                       |     ([n]{.c009}^2^ +  |                       |
|                       |     [n]{.c009}) ·     |                       |
|                       |     ([n]{.c009} +     |                       |
|                       |     1)*? Before you   |                       |
|                       |     start             |                       |
|                       |     multiplying,      |                       |
|                       |     remember that you |                       |
|                       |     only need the     |                       |
|                       |     leading term.*    |                       |
|                       | 3.  *If* [f]{.c009}   |                       |
|                       |     *is in*           |                       |
|                       |     [O]               |                       |
|                       | {.c009}([g]{.c009})*, |                       |
|                       |     for some          |                       |
|                       |     unspecified       |                       |
|                       |     function*         |                       |
|                       |     [g]{.c009}*, what |                       |
|                       |     can we say about* |                       |
|                       |     [af               |                       |
|                       | ]{.c009}+[b]{.c009}*, |                       |
|                       |     where* [a]{.c009} |                       |
|                       |     *and* [b]{.c009}  |                       |
|                       |     *are constants?*  |                       |
|                       | 4.  *If*              |                       |
|                       |     [f]{.c009}~1~     |                       |
|                       |     *and*             |                       |
|                       |     [f]{.c009}~2~     |                       |
|                       |     *are in*          |                       |
|                       |     [O]               |                       |
|                       | {.c009}([g]{.c009})*, |                       |
|                       |     what can we say   |                       |
|                       |     about*            |                       |
|                       |     [f]{.c009}~1~ +   |                       |
|                       |     [f]{.c009}~2~*?*  |                       |
|                       | 5.  *If*              |                       |
|                       |     [f]{.c009}~1~ *is |                       |
|                       |     in*               |                       |
|                       |     [                 |                       |
|                       | O]{.c009}([g]{.c009}) |                       |
|                       |     *and*             |                       |
|                       |     [f]{.c009}~2~ *is |                       |
|                       |     in*               |                       |
|                       |     [O]               |                       |
|                       | {.c009}([h]{.c009})*, |                       |
|                       |     what can we say   |                       |
|                       |     about*            |                       |
|                       |     [f]{.c009}~1~ +   |                       |
|                       |     [f]{.c009}~2~*?*  |                       |
|                       | 6.  *If*              |                       |
|                       |     [f]{.c009}~1~ *is |                       |
|                       |     in*               |                       |
|                       |     [                 |                       |
|                       | O]{.c009}([g]{.c009}) |                       |
|                       |     *and*             |                       |
|                       |     [f]{.c009}~2~     |                       |
|                       |     *is*              |                       |
|                       |     [O]               |                       |
|                       | {.c009}([h]{.c009})*, |                       |
|                       |     what can we say   |                       |
|                       |     about*            |                       |
|                       |     [f]{.c009}~1~ ·   |                       |
|                       |     [f]{.c009}~2~*?*  |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | Programmers who care  |                       |
|                       | about performance     |                       |
|                       | often find this kind  |                       |
|                       | of analysis hard to   |                       |
|                       | swallow. They have a  |                       |
|                       | point: sometimes the  |                       |
|                       | coefficients and the  |                       |
|                       | non-leading terms     |                       |
|                       | make a real           |                       |
|                       | difference. Sometimes |                       |
|                       | the details of the    |                       |
|                       | hardware, the         |                       |
|                       | programming language, |                       |
|                       | and the               |                       |
|                       | characteristics of    |                       |
|                       | the input make a big  |                       |
|                       | difference. And for   |                       |
|                       | small problems, order |                       |
|                       | of growth is          |                       |
|                       | irrelevant.           |                       |
|                       |                       |                       |
|                       | But if you keep those |                       |
|                       | caveats in mind,      |                       |
|                       | algorithmic analysis  |                       |
|                       | is a useful tool. At  |                       |
|                       | least for large       |                       |
|                       | problems, the         |                       |
|                       | "better" algorithm is |                       |
|                       | usually better, and   |                       |
|                       | sometimes it is       |                       |
|                       | *much* better. The    |                       |
|                       | difference between    |                       |
|                       | two algorithms with   |                       |
|                       | the same order of     |                       |
|                       | growth is usually a   |                       |
|                       | constant factor, but  |                       |
|                       | the difference        |                       |
|                       | between a good        |                       |
|                       | algorithm and a bad   |                       |
|                       | algorithm is          |                       |
|                       | unbounded!            |                       |
|                       |                       |                       |
|                       | ## B.2  Analysis of   |                       |
|                       | basic Python operatio |                       |
|                       | ns {#sec253 .section} |                       |
|                       |                       |                       |
|                       | In Python, most       |                       |
|                       | arithmetic operations |                       |
|                       | are constant time;    |                       |
|                       | multiplication        |                       |
|                       | usually takes longer  |                       |
|                       | than addition and     |                       |
|                       | subtraction, and      |                       |
|                       | division takes even   |                       |
|                       | longer, but these run |                       |
|                       | times don't depend on |                       |
|                       | the magnitude of the  |                       |
|                       | operands. Very large  |                       |
|                       | integers are an       |                       |
|                       | exception; in that    |                       |
|                       | case the run time     |                       |
|                       | increases with the    |                       |
|                       | number of digits.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1831} |                       |
|                       |                       |                       |
|                       | Indexing              |                       |
|                       | operations---reading  |                       |
|                       | or writing elements   |                       |
|                       | in a sequence or      |                       |
|                       | dictionary---are also |                       |
|                       | constant time,        |                       |
|                       | regardless of the     |                       |
|                       | size of the data      |                       |
|                       | structure.            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1832} |                       |
|                       |                       |                       |
|                       | A [for]{.c004} loop   |                       |
|                       | that traverses a      |                       |
|                       | sequence or           |                       |
|                       | dictionary is usually |                       |
|                       | linear, as long as    |                       |
|                       | all of the operations |                       |
|                       | in the body of the    |                       |
|                       | loop are constant     |                       |
|                       | time. For example,    |                       |
|                       | adding up the         |                       |
|                       | elements of a list is |                       |
|                       | linear:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |     total = 0         |                       |
|                       |     for x in t:       |                       |
|                       |         total += x    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The built-in function |                       |
|                       | [sum]{.c004} is also  |                       |
|                       | linear because it     |                       |
|                       | does the same thing,  |                       |
|                       | but it tends to be    |                       |
|                       | faster because it is  |                       |
|                       | a more efficient      |                       |
|                       | implementation; in    |                       |
|                       | the language of       |                       |
|                       | algorithmic analysis, |                       |
|                       | it has a smaller      |                       |
|                       | leading coefficient.  |                       |
|                       |                       |                       |
|                       | As a rule of thumb,   |                       |
|                       | if the body of a loop |                       |
|                       | is in                 |                       |
|                       | [O]{.c009}([n         |                       |
|                       | ]{.c009}^[a]{.c009}^) |                       |
|                       | then the whole loop   |                       |
|                       | is in                 |                       |
|                       | [O]{.c009}([n]{.      |                       |
|                       | c009}^[a]{.c009}+1^). |                       |
|                       | The exception is if   |                       |
|                       | you can show that the |                       |
|                       | loop exits after a    |                       |
|                       | constant number of    |                       |
|                       | iterations. If a loop |                       |
|                       | runs [k]{.c009} times |                       |
|                       | regardless of         |                       |
|                       | [n]{.c009}, then the  |                       |
|                       | loop is in            |                       |
|                       | [O]{.c009}([n]        |                       |
|                       | {.c009}^[a]{.c009}^), |                       |
|                       | even for large        |                       |
|                       | [k]{.c009}.           |                       |
|                       |                       |                       |
|                       | Multiplying by        |                       |
|                       | [k]{.c009} doesn't    |                       |
|                       | change the order of   |                       |
|                       | growth, but neither   |                       |
|                       | does dividing. So if  |                       |
|                       | the body of a loop is |                       |
|                       | in                    |                       |
|                       | [O]{.c009}([n         |                       |
|                       | ]{.c009}^[a]{.c009}^) |                       |
|                       | and it runs           |                       |
|                       | [n]{.c009}/[k]{.c009} |                       |
|                       | times, the loop is in |                       |
|                       | [O]{.c009}([n]{.      |                       |
|                       | c009}^[a]{.c009}+1^), |                       |
|                       | even for large        |                       |
|                       | [k]{.c009}.           |                       |
|                       |                       |                       |
|                       | Most string and tuple |                       |
|                       | operations are        |                       |
|                       | linear, except        |                       |
|                       | indexing and          |                       |
|                       | [len]{.c004}, which   |                       |
|                       | are constant time.    |                       |
|                       | The built-in          |                       |
|                       | functions             |                       |
|                       | [min]{.c004} and      |                       |
|                       | [max]{.c004} are      |                       |
|                       | linear. The run-time  |                       |
|                       | of a slice operation  |                       |
|                       | is proportional to    |                       |
|                       | the length of the     |                       |
|                       | output, but           |                       |
|                       | independent of the    |                       |
|                       | size of the input.    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1833} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1834} |                       |
|                       |                       |                       |
|                       | String concatenation  |                       |
|                       | is linear; the run    |                       |
|                       | time depends on the   |                       |
|                       | sum of the lengths of |                       |
|                       | the operands.         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1835} |                       |
|                       |                       |                       |
|                       | All string methods    |                       |
|                       | are linear, but if    |                       |
|                       | the lengths of the    |                       |
|                       | strings are bounded   |                       |
|                       | by a constant---for   |                       |
|                       | example, operations   |                       |
|                       | on single             |                       |
|                       | characters---they are |                       |
|                       | considered constant   |                       |
|                       | time. The string      |                       |
|                       | method [join]{.c004}  |                       |
|                       | is linear; the run    |                       |
|                       | time depends on the   |                       |
|                       | total length of the   |                       |
|                       | strings.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1836} |                       |
|                       |                       |                       |
|                       | Most list methods are |                       |
|                       | linear, but there are |                       |
|                       | some exceptions:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1837} |                       |
|                       |                       |                       |
|                       | -   Adding an element |                       |
|                       |     to the end of a   |                       |
|                       |     list is constant  |                       |
|                       |     time on average;  |                       |
|                       |     when it runs out  |                       |
|                       |     of room it        |                       |
|                       |     occasionally gets |                       |
|                       |     copied to a       |                       |
|                       |     bigger location,  |                       |
|                       |     but the total     |                       |
|                       |     time for          |                       |
|                       |     [n]{.c009}        |                       |
|                       |     operations is     |                       |
|                       |     [O                |                       |
|                       | ]{.c009}([n]{.c009}), |                       |
|                       |     so the average    |                       |
|                       |     time for each     |                       |
|                       |     operation is      |                       |
|                       |     [O]{.c009}(1).    |                       |
|                       | -   Removing an       |                       |
|                       |     element from the  |                       |
|                       |     end of a list is  |                       |
|                       |     constant time.    |                       |
|                       | -   Sorting is        |                       |
|                       |                       |                       |
|                       | [O]{.c009}([n]{.c009} |                       |
|                       |     log[n]{.c009}).   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1838} |                       |
|                       |                       |                       |
|                       | Most dictionary       |                       |
|                       | operations and        |                       |
|                       | methods are constant  |                       |
|                       | time, but there are   |                       |
|                       | some exceptions:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1839} |                       |
|                       |                       |                       |
|                       | -   The run time of   |                       |
|                       |     [update]{.c004}   |                       |
|                       |     is proportional   |                       |
|                       |     to the size of    |                       |
|                       |     the dictionary    |                       |
|                       |     passed as a       |                       |
|                       |     parameter, not    |                       |
|                       |     the dictionary    |                       |
|                       |     being updated.    |                       |
|                       | -   [keys]{.c004},    |                       |
|                       |     [values]{.c004}   |                       |
|                       |     and               |                       |
|                       |     [items]{.c004}    |                       |
|                       |     are constant time |                       |
|                       |     because they      |                       |
|                       |     return iterators. |                       |
|                       |     But if you loop   |                       |
|                       |     through the       |                       |
|                       |     iterators, the    |                       |
|                       |     loop will be      |                       |
|                       |     linear.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1840} |                       |
|                       |                       |                       |
|                       | The performance of    |                       |
|                       | dictionaries is one   |                       |
|                       | of the minor miracles |                       |
|                       | of computer science.  |                       |
|                       | We will see how they  |                       |
|                       | work in               |                       |
|                       | Secti                 |                       |
|                       | on [B.4](#hashtable). |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       |                       |                       |
|                       | *Read the Wikipedia   |                       |
|                       | page on sorting       |                       |
|                       | algorithms at*        |                       |
|                       | [*                    |                       |
|                       | [http://en.wikipedia. |                       |
|                       | org/wiki/Sorting_algo |                       |
|                       | rithm]{.c004}*](http: |                       |
|                       | //en.wikipedia.org/wi |                       |
|                       | ki/Sorting_algorithm) |                       |
|                       | *and answer the       |                       |
|                       | following questions:* |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1841} |                       |
|                       |                       |                       |
|                       | 1.  *What is a        |                       |
|                       |     "comparison       |                       |
|                       |     sort?" What is    |                       |
|                       |     the best          |                       |
|                       |     worst-case order  |                       |
|                       |     of growth for a   |                       |
|                       |     comparison sort?  |                       |
|                       |     What is the best  |                       |
|                       |     worst-case order  |                       |
|                       |     of growth for any |                       |
|                       |     sort algorithm?*  |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1842} |                       |
|                       | 2.  *What is the      |                       |
|                       |     order of growth   |                       |
|                       |     of bubble sort,   |                       |
|                       |     and why does      |                       |
|                       |     Barack Obama      |                       |
|                       |     think it is "the  |                       |
|                       |     wrong way to      |                       |
|                       |     go?"*             |                       |
|                       | 3.  *What is the      |                       |
|                       |     order of growth   |                       |
|                       |     of radix sort?    |                       |
|                       |     What              |                       |
|                       |     preconditions do  |                       |
|                       |     we need to use    |                       |
|                       |     it?*              |                       |
|                       | 4.  *What is a stable |                       |
|                       |     sort and why      |                       |
|                       |     might it matter   |                       |
|                       |     in practice?*     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1843} |                       |
|                       | 5.  *What is the      |                       |
|                       |     worst sorting     |                       |
|                       |     algorithm (that   |                       |
|                       |     has a name)?*     |                       |
|                       | 6.  *What sort        |                       |
|                       |     algorithm does    |                       |
|                       |     the C library     |                       |
|                       |     use? What sort    |                       |
|                       |     algorithm does    |                       |
|                       |     Python use? Are   |                       |
|                       |     these algorithms  |                       |
|                       |     stable? You might |                       |
|                       |     have to Google    |                       |
|                       |     around to find    |                       |
|                       |     these answers.*   |                       |
|                       | 7.  *Many of the      |                       |
|                       |     non-comparison    |                       |
|                       |     sorts are linear, |                       |
|                       |     so why does       |                       |
|                       |     Python use an*    |                       |
|                       |                       |                       |
|                       | [O]{.c009}([n]{.c009} |                       |
|                       |     log[n]{.c009})    |                       |
|                       |     *comparison       |                       |
|                       |     sort?*            |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ## B.3  Analys        |                       |
|                       | is of search algorith |                       |
|                       | ms {#sec254 .section} |                       |
|                       |                       |                       |
|                       | A [search]{.c010} is  |                       |
|                       | an algorithm that     |                       |
|                       | takes a collection    |                       |
|                       | and a target item and |                       |
|                       | determines whether    |                       |
|                       | the target is in the  |                       |
|                       | collection, often     |                       |
|                       | returning the index   |                       |
|                       | of the target.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1844} |                       |
|                       |                       |                       |
|                       | The simplest search   |                       |
|                       | algorithm is a        |                       |
|                       | "linear search",      |                       |
|                       | which traverses the   |                       |
|                       | items of the          |                       |
|                       | collection in order,  |                       |
|                       | stopping if it finds  |                       |
|                       | the target. In the    |                       |
|                       | worst case it has to  |                       |
|                       | traverse the entire   |                       |
|                       | collection, so the    |                       |
|                       | run time is linear.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1845} |                       |
|                       |                       |                       |
|                       | The [in]{.c004}       |                       |
|                       | operator for          |                       |
|                       | sequences uses a      |                       |
|                       | linear search; so do  |                       |
|                       | string methods like   |                       |
|                       | [find]{.c004} and     |                       |
|                       | [count]{.c004}.       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1846} |                       |
|                       |                       |                       |
|                       | If the elements of    |                       |
|                       | the sequence are in   |                       |
|                       | order, you can use a  |                       |
|                       | [bisection            |                       |
|                       | search]{.c010}, which |                       |
|                       | is                    |                       |
|                       | [O]{.                 |                       |
|                       | c009}(log[n]{.c009}). |                       |
|                       | Bisection search is   |                       |
|                       | similar to the        |                       |
|                       | algorithm you might   |                       |
|                       | use to look a word up |                       |
|                       | in a dictionary (a    |                       |
|                       | paper dictionary, not |                       |
|                       | the data structure).  |                       |
|                       | Instead of starting   |                       |
|                       | at the beginning and  |                       |
|                       | checking each item in |                       |
|                       | order, you start with |                       |
|                       | the item in the       |                       |
|                       | middle and check      |                       |
|                       | whether the word you  |                       |
|                       | are looking for comes |                       |
|                       | before or after. If   |                       |
|                       | it comes before, then |                       |
|                       | you search the first  |                       |
|                       | half of the sequence. |                       |
|                       | Otherwise you search  |                       |
|                       | the second half.      |                       |
|                       | Either way, you cut   |                       |
|                       | the number of         |                       |
|                       | remaining items in    |                       |
|                       | half.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1847} |                       |
|                       |                       |                       |
|                       | If the sequence has   |                       |
|                       | 1,000,000 items, it   |                       |
|                       | will take about 20    |                       |
|                       | steps to find the     |                       |
|                       | word or conclude that |                       |
|                       | it's not there. So    |                       |
|                       | that's about 50,000   |                       |
|                       | times faster than a   |                       |
|                       | linear search.        |                       |
|                       |                       |                       |
|                       | Bisection search can  |                       |
|                       | be much faster than   |                       |
|                       | linear search, but it |                       |
|                       | requires the sequence |                       |
|                       | to be in order, which |                       |
|                       | might require extra   |                       |
|                       | work.                 |                       |
|                       |                       |                       |
|                       | There is another data |                       |
|                       | structure, called a   |                       |
|                       | [hashtable]{.c010}    |                       |
|                       | that is even          |                       |
|                       | faster---it can do a  |                       |
|                       | search in constant    |                       |
|                       | time---and it doesn't |                       |
|                       | require the items to  |                       |
|                       | be sorted. Python     |                       |
|                       | dictionaries are      |                       |
|                       | implemented using     |                       |
|                       | hashtables, which is  |                       |
|                       | why most dictionary   |                       |
|                       | operations, including |                       |
|                       | the [in]{.c004}       |                       |
|                       | operator, are         |                       |
|                       | constant time.        |                       |
|                       |                       |                       |
|                       | ## B.4  Hashtabl      |                       |
|                       | es {#sec255 .section} |                       |
|                       |                       |                       |
|                       | []{#hashtable}        |                       |
|                       |                       |                       |
|                       | To explain how        |                       |
|                       | hashtables work and   |                       |
|                       | why their performance |                       |
|                       | is so good, I start   |                       |
|                       | with a simple         |                       |
|                       | implementation of a   |                       |
|                       | map and gradually     |                       |
|                       | improve it until it's |                       |
|                       | a hashtable.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1848} |                       |
|                       |                       |                       |
|                       | I use Python to       |                       |
|                       | demonstrate these     |                       |
|                       | implementations, but  |                       |
|                       | in real life you      |                       |
|                       | wouldn't write code   |                       |
|                       | like this in Python;  |                       |
|                       | you would just use a  |                       |
|                       | dictionary! So for    |                       |
|                       | the rest of this      |                       |
|                       | chapter, you have to  |                       |
|                       | imagine that          |                       |
|                       | dictionaries don't    |                       |
|                       | exist and you want to |                       |
|                       | implement a data      |                       |
|                       | structure that maps   |                       |
|                       | from keys to values.  |                       |
|                       | The operations you    |                       |
|                       | have to implement     |                       |
|                       | are:                  |                       |
|                       |                       |                       |
|                       | [[add(k               |                       |
|                       | , v)]{.c004}:]{.c010} |                       |
|                       | :   Add a new item    |                       |
|                       |     that maps from    |                       |
|                       |     key [k]{.c004} to |                       |
|                       |     value [v]{.c004}. |                       |
|                       |     With a Python     |                       |
|                       |     dictionary,       |                       |
|                       |     [d]{.c004}, this  |                       |
|                       |     operation is      |                       |
|                       |     written [d\[k\] = |                       |
|                       |     v]{.c004}.        |                       |
|                       |                       |                       |
|                       | [[ge                  |                       |
|                       | t(k)]{.c004}:]{.c010} |                       |
|                       | :   Look up and       |                       |
|                       |     return the value  |                       |
|                       |     that corresponds  |                       |
|                       |     to key            |                       |
|                       |     [k]{.c004}. With  |                       |
|                       |     a Python          |                       |
|                       |     dictionary,       |                       |
|                       |     [d]{.c004}, this  |                       |
|                       |     operation is      |                       |
|                       |     written           |                       |
|                       |     [d\[k\]]{.c004}   |                       |
|                       |     or                |                       |
|                       |                       |                       |
|                       |    [d.get(k)]{.c004}. |                       |
|                       |                       |                       |
|                       | For now, I assume     |                       |
|                       | that each key only    |                       |
|                       | appears once. The     |                       |
|                       | simplest              |                       |
|                       | implementation of     |                       |
|                       | this interface uses a |                       |
|                       | list of tuples, where |                       |
|                       | each tuple is a       |                       |
|                       | key-value pair.       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1849} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | class LinearMap:      |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |   def __init__(self): |                       |
|                       |                       |                       |
|                       |       self.items = [] |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |  def add(self, k, v): |                       |
|                       |         self          |                       |
|                       | .items.append((k, v)) |                       |
|                       |                       |                       |
|                       |     def get(self, k): |                       |
|                       |         for ke        |                       |
|                       | y, val in self.items: |                       |
|                       |                       |                       |
|                       |          if key == k: |                       |
|                       |                       |                       |
|                       |            return val |                       |
|                       |                       |                       |
|                       |        raise KeyError |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [add]{.c004} appends  |                       |
|                       | a key-value tuple to  |                       |
|                       | the list of items,    |                       |
|                       | which takes constant  |                       |
|                       | time.                 |                       |
|                       |                       |                       |
|                       | [get]{.c004} uses a   |                       |
|                       | [for]{.c004} loop to  |                       |
|                       | search the list: if   |                       |
|                       | it finds the target   |                       |
|                       | key it returns the    |                       |
|                       | corresponding value;  |                       |
|                       | otherwise it raises a |                       |
|                       | [KeyError]{.c004}. So |                       |
|                       | [get]{.c004} is       |                       |
|                       | linear.               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1850} |                       |
|                       |                       |                       |
|                       | An alternative is to  |                       |
|                       | keep the list sorted  |                       |
|                       | by key. Then          |                       |
|                       | [get]{.c004} could    |                       |
|                       | use a bisection       |                       |
|                       | search, which is      |                       |
|                       | [O]{.                 |                       |
|                       | c009}(log[n]{.c009}). |                       |
|                       | But inserting a new   |                       |
|                       | item in the middle of |                       |
|                       | a list is linear, so  |                       |
|                       | this might not be the |                       |
|                       | best option. There    |                       |
|                       | are other data        |                       |
|                       | structures that can   |                       |
|                       | implement             |                       |
|                       | [add]{.c004} and      |                       |
|                       | [get]{.c004} in log   |                       |
|                       | time, but that's      |                       |
|                       | still not as good as  |                       |
|                       | constant time, so     |                       |
|                       | let's move on.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1851} |                       |
|                       |                       |                       |
|                       | One way to improve    |                       |
|                       | [LinearMap]{.c004} is |                       |
|                       | to break the list of  |                       |
|                       | key-value pairs into  |                       |
|                       | smaller lists. Here's |                       |
|                       | an implementation     |                       |
|                       | called                |                       |
|                       | [BetterMap]{.c004},   |                       |
|                       | which is a list of    |                       |
|                       | 100 LinearMaps. As    |                       |
|                       | we'll see in a        |                       |
|                       | second, the order of  |                       |
|                       | growth for            |                       |
|                       | [get]{.c004} is still |                       |
|                       | linear, but           |                       |
|                       | [BetterMap]{.c004} is |                       |
|                       | a step on the path    |                       |
|                       | toward hashtables:    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1852} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | class BetterMap:      |                       |
|                       |                       |                       |
|                       |     def _             |                       |
|                       | _init__(self, n=100): |                       |
|                       |                       |                       |
|                       |        self.maps = [] |                       |
|                       |                       |                       |
|                       |    for i in range(n): |                       |
|                       |             self.map  |                       |
|                       | s.append(LinearMap()) |                       |
|                       |                       |                       |
|                       |     d                 |                       |
|                       | ef find_map(self, k): |                       |
|                       |         index = has   |                       |
|                       | h(k) % len(self.maps) |                       |
|                       |         re            |                       |
|                       | turn self.maps[index] |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |  def add(self, k, v): |                       |
|                       |                       |                       |
|                       |  m = self.find_map(k) |                       |
|                       |         m.add(k, v)   |                       |
|                       |                       |                       |
|                       |     def get(self, k): |                       |
|                       |                       |                       |
|                       |  m = self.find_map(k) |                       |
|                       |                       |                       |
|                       |       return m.get(k) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | `__init__` makes a    |                       |
|                       | list of [n]{.c004}    |                       |
|                       | [LinearMap]{.c004}s.  |                       |
|                       |                       |                       |
|                       | `find_map` is used by |                       |
|                       | [add]{.c004} and      |                       |
|                       | [get]{.c004} to       |                       |
|                       | figure out which map  |                       |
|                       | to put the new item   |                       |
|                       | in, or which map to   |                       |
|                       | search.               |                       |
|                       |                       |                       |
|                       | `find_map` uses the   |                       |
|                       | built-in function     |                       |
|                       | [hash]{.c004}, which  |                       |
|                       | takes almost any      |                       |
|                       | Python object and     |                       |
|                       | returns an integer. A |                       |
|                       | limitation of this    |                       |
|                       | implementation is     |                       |
|                       | that it only works    |                       |
|                       | with hashable keys.   |                       |
|                       | Mutable types like    |                       |
|                       | lists and             |                       |
|                       | dictionaries are      |                       |
|                       | unhashable.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1853} |                       |
|                       |                       |                       |
|                       | Hashable objects that |                       |
|                       | are considered        |                       |
|                       | equivalent return the |                       |
|                       | same hash value, but  |                       |
|                       | the converse is not   |                       |
|                       | necessarily true: two |                       |
|                       | objects with          |                       |
|                       | different values can  |                       |
|                       | return the same hash  |                       |
|                       | value.                |                       |
|                       |                       |                       |
|                       | `find_map` uses the   |                       |
|                       | modulus operator to   |                       |
|                       | wrap the hash values  |                       |
|                       | into the range from 0 |                       |
|                       | to                    |                       |
|                       | [le                   |                       |
|                       | n(self.maps)]{.c004}, |                       |
|                       | so the result is a    |                       |
|                       | legal index into the  |                       |
|                       | list. Of course, this |                       |
|                       | means that many       |                       |
|                       | different hash values |                       |
|                       | will wrap onto the    |                       |
|                       | same index. But if    |                       |
|                       | the hash function     |                       |
|                       | spreads things out    |                       |
|                       | pretty evenly (which  |                       |
|                       | is what hash          |                       |
|                       | functions are         |                       |
|                       | designed to do), then |                       |
|                       | we expect             |                       |
|                       | [n]{.c009}/100 items  |                       |
|                       | per LinearMap.        |                       |
|                       |                       |                       |
|                       | Since the run time of |                       |
|                       | [                     |                       |
|                       | LinearMap.get]{.c004} |                       |
|                       | is proportional to    |                       |
|                       | the number of items,  |                       |
|                       | we expect BetterMap   |                       |
|                       | to be about 100 times |                       |
|                       | faster than           |                       |
|                       | LinearMap. The order  |                       |
|                       | of growth is still    |                       |
|                       | linear, but the       |                       |
|                       | leading coefficient   |                       |
|                       | is smaller. That's    |                       |
|                       | nice, but still not   |                       |
|                       | as good as a          |                       |
|                       | hashtable.            |                       |
|                       |                       |                       |
|                       | Here (finally) is the |                       |
|                       | crucial idea that     |                       |
|                       | makes hashtables      |                       |
|                       | fast: if you can keep |                       |
|                       | the maximum length of |                       |
|                       | the LinearMaps        |                       |
|                       | bounded,              |                       |
|                       | [                     |                       |
|                       | LinearMap.get]{.c004} |                       |
|                       | is constant time. All |                       |
|                       | you have to do is     |                       |
|                       | keep track of the     |                       |
|                       | number of items and   |                       |
|                       | when the number of    |                       |
|                       | items per LinearMap   |                       |
|                       | exceeds a threshold,  |                       |
|                       | resize the hashtable  |                       |
|                       | by adding more        |                       |
|                       | LinearMaps.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1854} |                       |
|                       |                       |                       |
|                       | Here is an            |                       |
|                       | implementation of a   |                       |
|                       | hashtable:            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1855} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | class HashMap:        |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |   def __init__(self): |                       |
|                       |         sel           |                       |
|                       | f.maps = BetterMap(2) |                       |
|                       |         self.num = 0  |                       |
|                       |                       |                       |
|                       |     def get(self, k): |                       |
|                       |         re            |                       |
|                       | turn self.maps.get(k) |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |  def add(self, k, v): |                       |
|                       |                       |                       |
|                       |        if self.num == |                       |
|                       |  len(self.maps.maps): |                       |
|                       |                       |                       |
|                       |         self.resize() |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |   self.maps.add(k, v) |                       |
|                       |         self.num += 1 |                       |
|                       |                       |                       |
|                       |     def resize(self): |                       |
|                       |         new_maps = Be |                       |
|                       | tterMap(self.num * 2) |                       |
|                       |                       |                       |
|                       |         for           |                       |
|                       |  m in self.maps.maps: |                       |
|                       |                       |                       |
|                       |  for k, v in m.items: |                       |
|                       |                       |                       |
|                       |    new_maps.add(k, v) |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |  self.maps = new_maps |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | `__init__` creates a  |                       |
|                       | [BetterMap]{.c004}    |                       |
|                       | and initializes       |                       |
|                       | [num]{.c004}, which   |                       |
|                       | keeps track of the    |                       |
|                       | number of items.      |                       |
|                       |                       |                       |
|                       | [get]{.c004} just     |                       |
|                       | dispatches to         |                       |
|                       | [BetterMap]{.c004}.   |                       |
|                       | The real work happens |                       |
|                       | in [add]{.c004},      |                       |
|                       | which checks the      |                       |
|                       | number of items and   |                       |
|                       | the size of the       |                       |
|                       | [BetterMap]{.c004}:   |                       |
|                       | if they are equal,    |                       |
|                       | the average number of |                       |
|                       | items per LinearMap   |                       |
|                       | is 1, so it calls     |                       |
|                       | [resize]{.c004}.      |                       |
|                       |                       |                       |
|                       | [resize]{.c004} makes |                       |
|                       | a new                 |                       |
|                       | [BetterMap]{.c004},   |                       |
|                       | twice as big as the   |                       |
|                       | previous one, and     |                       |
|                       | then "rehashes" the   |                       |
|                       | items from the old    |                       |
|                       | map to the new.       |                       |
|                       |                       |                       |
|                       | Rehashing is          |                       |
|                       | necessary because     |                       |
|                       | changing the number   |                       |
|                       | of LinearMaps changes |                       |
|                       | the denominator of    |                       |
|                       | the modulus operator  |                       |
|                       | in `find_map`. That   |                       |
|                       | means that some       |                       |
|                       | objects that used to  |                       |
|                       | hash into the same    |                       |
|                       | LinearMap will get    |                       |
|                       | split up (which is    |                       |
|                       | what we wanted,       |                       |
|                       | right?).              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1856} |                       |
|                       |                       |                       |
|                       | Rehashing is linear,  |                       |
|                       | so [resize]{.c004} is |                       |
|                       | linear, which might   |                       |
|                       | seem bad, since I     |                       |
|                       | promised that         |                       |
|                       | [add]{.c004} would be |                       |
|                       | constant time. But    |                       |
|                       | remember that we      |                       |
|                       | don't have to resize  |                       |
|                       | every time, so        |                       |
|                       | [add]{.c004} is       |                       |
|                       | usually constant time |                       |
|                       | and only occasionally |                       |
|                       | linear. The total     |                       |
|                       | amount of work to run |                       |
|                       | [add]{.c004}          |                       |
|                       | [n]{.c009} times is   |                       |
|                       | proportional to       |                       |
|                       | [n]{.c009}, so the    |                       |
|                       | average time of each  |                       |
|                       | [add]{.c004} is       |                       |
|                       | constant time!        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1857} |                       |
|                       |                       |                       |
|                       | To see how this       |                       |
|                       | works, think about    |                       |
|                       | starting with an      |                       |
|                       | empty HashTable and   |                       |
|                       | adding a sequence of  |                       |
|                       | items. We start with  |                       |
|                       | 2 LinearMaps, so the  |                       |
|                       | first 2 adds are fast |                       |
|                       | (no resizing          |                       |
|                       | required). Let's say  |                       |
|                       | that they take one    |                       |
|                       | unit of work each.    |                       |
|                       | The next add requires |                       |
|                       | a resize, so we have  |                       |
|                       | to rehash the first   |                       |
|                       | two items (let's call |                       |
|                       | that 2 more units of  |                       |
|                       | work) and then add    |                       |
|                       | the third item (one   |                       |
|                       | more unit). Adding    |                       |
|                       | the next item costs 1 |                       |
|                       | unit, so the total so |                       |
|                       | far is 6 units of     |                       |
|                       | work for 4 items.     |                       |
|                       |                       |                       |
|                       | The next [add]{.c004} |                       |
|                       | costs 5 units, but    |                       |
|                       | the next three are    |                       |
|                       | only one unit each,   |                       |
|                       | so the total is 14    |                       |
|                       | units for the first 8 |                       |
|                       | adds.                 |                       |
|                       |                       |                       |
|                       | The next [add]{.c004} |                       |
|                       | costs 9 units, but    |                       |
|                       | then we can add 7     |                       |
|                       | more before the next  |                       |
|                       | resize, so the total  |                       |
|                       | is 30 units for the   |                       |
|                       | first 16 adds.        |                       |
|                       |                       |                       |
|                       | After 32 adds, the    |                       |
|                       | total cost is 62      |                       |
|                       | units, and I hope you |                       |
|                       | are starting to see a |                       |
|                       | pattern. After        |                       |
|                       | [n]{.c009} adds,      |                       |
|                       | where [n]{.c009} is a |                       |
|                       | power of two, the     |                       |
|                       | total cost is         |                       |
|                       | 2[n]{.c009}−2 units,  |                       |
|                       | so the average work   |                       |
|                       | per add is a little   |                       |
|                       | less than 2 units.    |                       |
|                       | When [n]{.c009} is a  |                       |
|                       | power of two, that's  |                       |
|                       | the best case; for    |                       |
|                       | other values of       |                       |
|                       | [n]{.c009} the        |                       |
|                       | average work is a     |                       |
|                       | little higher, but    |                       |
|                       | that's not important. |                       |
|                       | The important thing   |                       |
|                       | is that it is         |                       |
|                       | [O]{.c009}(1).        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1858} |                       |
|                       |                       |                       |
|                       | Fi                    |                       |
|                       | gure [B.1](#fig.hash) |                       |
|                       | shows how this works  |                       |
|                       | graphically. Each     |                       |
|                       | block represents a    |                       |
|                       | unit of work. The     |                       |
|                       | columns show the      |                       |
|                       | total work for each   |                       |
|                       | add in order from     |                       |
|                       | left to right: the    |                       |
|                       | first two             |                       |
|                       | [adds]{.c004} cost 1  |                       |
|                       | unit each, the third  |                       |
|                       | costs 3 units, etc.   |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2026.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -------------     |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       | >   Figure B.1:       |                       |
|                       |  The cost of a hashta |                       |
|                       | ble add.[]{#fig.hash} |                       |
|                       | >   -------------     |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | The extra work of     |                       |
|                       | rehashing appears as  |                       |
|                       | a sequence of         |                       |
|                       | increasingly tall     |                       |
|                       | towers with           |                       |
|                       | increasing space      |                       |
|                       | between them. Now if  |                       |
|                       | you knock over the    |                       |
|                       | towers, spreading the |                       |
|                       | cost of resizing over |                       |
|                       | all adds, you can see |                       |
|                       | graphically that the  |                       |
|                       | total cost after      |                       |
|                       | [n]{.c009} adds is    |                       |
|                       | 2[n]{.c009} − 2.      |                       |
|                       |                       |                       |
|                       | An important feature  |                       |
|                       | of this algorithm is  |                       |
|                       | that when we resize   |                       |
|                       | the HashTable it      |                       |
|                       | grows geometrically;  |                       |
|                       | that is, we multiply  |                       |
|                       | the size by a         |                       |
|                       | constant. If you      |                       |
|                       | increase the size     |                       |
|                       | ar                    |                       |
|                       | ithmetically---adding |                       |
|                       | a fixed number each   |                       |
|                       | time---the average    |                       |
|                       | time per [add]{.c004} |                       |
|                       | is linear.            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1859} |                       |
|                       |                       |                       |
|                       | You can download my   |                       |
|                       | implementation of     |                       |
|                       | HashMap from          |                       |
|                       | [[https://thinkpython |                       |
|                       | .com/code/Map.py]{.c0 |                       |
|                       | 04}](https://thinkpyt |                       |
|                       | hon.com/code/Map.py), |                       |
|                       | but remember that     |                       |
|                       | there is no reason to |                       |
|                       | use it; if you want a |                       |
|                       | map, just use a       |                       |
|                       | Python dictionary.    |                       |
|                       |                       |                       |
|                       | ## B.5  Glossa        |                       |
|                       | ry {#sec256 .section} |                       |
|                       |                       |                       |
|                       | [analysis o           |                       |
|                       | f algorithms:]{.c010} |                       |
|                       | :   A way to compare  |                       |
|                       |     algorithms in     |                       |
|                       |     terms of their    |                       |
|                       |     run time and/or   |                       |
|                       |     space             |                       |
|                       |     requirements.     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1860} |                       |
|                       |                       |                       |
|                       | [m                    |                       |
|                       | achine model:]{.c010} |                       |
|                       | :   A simplified      |                       |
|                       |     representation of |                       |
|                       |     a computer used   |                       |
|                       |     to describe       |                       |
|                       |     algorithms.       |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1861} |                       |
|                       |                       |                       |
|                       | [worst case:]{.c010}  |                       |
|                       | :   The input that    |                       |
|                       |     makes a given     |                       |
|                       |     algorithm run     |                       |
|                       |     slowest (or       |                       |
|                       |     require the most  |                       |
|                       |     space).           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1862} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | leading term:]{.c010} |                       |
|                       | :   In a polynomial,  |                       |
|                       |     the term with the |                       |
|                       |     highest exponent. |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1863} |                       |
|                       |                       |                       |
|                       | [cro                  |                       |
|                       | ssover point:]{.c010} |                       |
|                       | :   The problem size  |                       |
|                       |     where two         |                       |
|                       |     algorithms        |                       |
|                       |     require the same  |                       |
|                       |     run time or       |                       |
|                       |     space.            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1864} |                       |
|                       |                       |                       |
|                       | [ord                  |                       |
|                       | er of growth:]{.c010} |                       |
|                       | :   A set of          |                       |
|                       |     functions that    |                       |
|                       |     all grow in a way |                       |
|                       |     considered        |                       |
|                       |     equivalent for    |                       |
|                       |     purposes of       |                       |
|                       |     analysis of       |                       |
|                       |     algorithms. For   |                       |
|                       |     example, all      |                       |
|                       |     functions that    |                       |
|                       |     grow linearly     |                       |
|                       |     belong to the     |                       |
|                       |     same order of     |                       |
|                       |     growth.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1865} |                       |
|                       |                       |                       |
|                       | [Big                  |                       |
|                       | -Oh notation:]{.c010} |                       |
|                       | :   Notation for      |                       |
|                       |     representing an   |                       |
|                       |     order of growth;  |                       |
|                       |     for example,      |                       |
|                       |     [                 |                       |
|                       | O]{.c009}([n]{.c009}) |                       |
|                       |     represents the    |                       |
|                       |     set of functions  |                       |
|                       |     that grow         |                       |
|                       |     linearly.         |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1866} |                       |
|                       |                       |                       |
|                       | [linear:]{.c010}      |                       |
|                       | :   An algorithm      |                       |
|                       |     whose run time is |                       |
|                       |     proportional to   |                       |
|                       |     problem size, at  |                       |
|                       |     least for large   |                       |
|                       |     problem sizes.    |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1867} |                       |
|                       |                       |                       |
|                       | [quadratic:]{.c010}   |                       |
|                       | :   An algorithm      |                       |
|                       |     whose run time is |                       |
|                       |     proportional to   |                       |
|                       |     [n]{.c009}^2^,    |                       |
|                       |     where [n]{.c009}  |                       |
|                       |     is a measure of   |                       |
|                       |     problem size.     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1868} |                       |
|                       |                       |                       |
|                       | [search:]{.c010}      |                       |
|                       | :   The problem of    |                       |
|                       |     locating an       |                       |
|                       |     element of a      |                       |
|                       |     collection (like  |                       |
|                       |     a list or         |                       |
|                       |     dictionary) or    |                       |
|                       |     determining that  |                       |
|                       |     it is not         |                       |
|                       |     present.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1869} |                       |
|                       |                       |                       |
|                       | [hashtable:]{.c010}   |                       |
|                       | :   A data structure  |                       |
|                       |     that represents a |                       |
|                       |     collection of     |                       |
|                       |     key-value pairs   |                       |
|                       |     and performs      |                       |
|                       |     search in         |                       |
|                       |     constant time.    |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1870} |                       |
|                       |                       |                       |
|                       | -------------------   |                       |
|                       |                       |                       |
|                       | [1](#text2){#note2}   |                       |
|                       |                       |                       |
|                       | :   ::: footnotetext  |                       |
|                       |     But if you get a  |                       |
|                       |     question like     |                       |
|                       |     this in an        |                       |
|                       |     interview, I      |                       |
|                       |     think a better    |                       |
|                       |     answer is, "The   |                       |
|                       |     fastest way to    |                       |
|                       |     sort a million    |                       |
|                       |     integers is to    |                       |
|                       |     use whatever sort |                       |
|                       |     function is       |                       |
|                       |     provided by the   |                       |
|                       |     language I'm      |                       |
|                       |     using. Its        |                       |
|                       |     performance is    |                       |
|                       |     good enough for   |                       |
|                       |     the vast majority |                       |
|                       |     of applications,  |                       |
|                       |     but if it turned  |                       |
|                       |     out that my       |                       |
|                       |     application was   |                       |
|                       |     too slow, I would |                       |
|                       |     use a profiler to |                       |
|                       |     see where the     |                       |
|                       |     time was being    |                       |
|                       |     spent. If it      |                       |
|                       |     looked like a     |                       |
|                       |     faster sort       |                       |
|                       |     algorithm would   |                       |
|                       |     have a            |                       |
|                       |     significant       |                       |
|                       |     effect on         |                       |
|                       |     performance, then |                       |
|                       |     I would look      |                       |
|                       |     around for a good |                       |
|                       |     implementation of |                       |
|                       |     radix sort."      |                       |
|                       |     :::               |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2021.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2023.html)
---
generator: hevea 2.32
title: Index
---

[![Previous](back.png)](thinkpython2022.html)
[![Up](up.png)](index.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Ind                 | to support my books,  |
|                       | ex {#sec257 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | +--------+--------+   | with PayPal. Thank    |
|                       | | -      | -      |   | you!                  |
|                       | |    Ack |   list |   |                       |
|                       | | ermann |     co |   |   -----------         |
|                       | |        | mprehe |   | --------------------- |
|                       | |    fun | nsion, |   | --------------------- |
|                       | | ction, |        |   | --------------------- |
|                       | |        |  [19.2 |   | --------------------- |
|                       | |   [6.1 | ](thin |   |   Pay what you want:  |
|                       | | 1](thi | kpytho |   |   Small \$1           |
|                       | | nkpyth | n2020. |   | .00 USD Medium \$5.00 |
|                       | | on2007 | html#h |   |  USD Large \$10.00 US |
|                       | | .html# | evea_d |   | D X-Large \$20.00 USD |
|                       | | hevea_ | efault |   |  XX-Large \$50.00 USD |
|                       | | defaul | 1670), |   |   -----------         |
|                       | | t488), |        |   | --------------------- |
|                       | |        |  [19.1 |   | --------------------- |
|                       | |   [11. | 0](thi |   | --------------------- |
|                       | | 10](th | nkpyth |   | --------------------- |
|                       | | inkpyt | on2020 |   |                       |
|                       | | hon201 | .html# |   | ![](                  |
|                       | | 2.html | hevea_ |   | https://www.paypalobj |
|                       | | #hevea | defaul |   | ects.com/en_US/i/scr/ |
|                       | | _defau | t1726) |   | pixel.gif){border="0" |
|                       | | lt997) | -      |   | width="1" height="1"} |
|                       | | -      |   list |   |                       |
|                       | |  Archi |     me |   | ####                  |
|                       | | median | thods, |   | Are you using one of  |
|                       | |     s  |        |   | our books in a class? |
|                       | | piral, |    [B. |   |                       |
|                       | |        | 2](thi |   | We\'d like to know    |
|                       | |    [4. | nkpyth |   | about it. Please      |
|                       | | 12](th | on2022 |   | consider filling out  |
|                       | | inkpyt | .html# |   | [this short           |
|                       | | hon200 | hevea_ |   | survey](http://s      |
|                       | | 5.html | defaul |   | preadsheets.google.co |
|                       | | #hevea | t1837) |   | m/viewform?formkey=dC |
|                       | | _defau | -      |   | 0tNUZkMjBEdXVoRGljNm9 |
|                       | | lt311) | litera |   | FRmlTMHc6MA){onclick= |
|                       | | -      | lness, |   | "javascript: pageTrac |
|                       | |    Att |     [  |   | ker._trackPageview('/ |
|                       | | ribute | 1.6](t |   | outbound/survey');"}. |
|                       | | Error, | hinkpy |   |                       |
|                       | |        | thon20 |   | \                     |
|                       | |  [15.7 | 02.htm |   |                       |
|                       | | ](thin | l#heve |   | [Think                |
|                       | | kpytho | a_defa |   | DSP](http             |
|                       | | n2016. | ult55) |   | ://www.amazon.com/gp/ |
|                       | | html#h | -      |   | product/1491938455/re |
|                       | | evea_d |  local |   | f=as_li_tl?ie=UTF8&ca |
|                       | | efault |        |   | mp=1789&creative=9325 |
|                       | | 1388), |    var |   | &creativeASIN=1491938 |
|                       | |        | iable, |   | 455&linkCode=as2&tag= |
|                       | |  [A.2. |        |   | greenteapre01-20&link |
|                       | | 3](thi |    [3. |   | Id=2JJH4SWCAVVYSQHO){ |
|                       | | nkpyth | 8](thi |   | rel="nofollow"}![](ht |
|                       | | on2021 | nkpyth |   | tp://ir-na.amazon-ads |
|                       | | .html# | on2004 |   | ystem.com/e/ir?t=gree |
|                       | | hevea_ | .html# |   | nteapre01-20&l=as2&o= |
|                       | | defaul | hevea_ |   | 1&a=1491938455){.c003 |
|                       | | t1779) | defaul |   | width="1" height="1"  |
|                       | | -   A  | t202), |   | border="0"}           |
|                       | | usten, |        |   |                       |
|                       | |        |    [3. |   | [                     |
|                       | |  Jane, | 13](th |   | ![](http://ws-na.amaz |
|                       | |        | inkpyt |   | on-adsystem.com/widge |
|                       | |   [13. | hon200 |   | ts/q?_encoding=UTF8&A |
|                       | | 3](thi | 4.html |   | SIN=1491938455&Format |
|                       | | nkpyth | #hevea |   | =_SL160_&ID=AsinImage |
|                       | | on2014 | _defau |   | &MarketPlace=US&Servi |
|                       | | .html# | lt240) |   | ceVersion=20070822&WS |
|                       | | hevea_ | -      |   | =1&tag=greenteapre01- |
|                       | | defaul |    log |   | 20){border="0"}](http |
|                       | | t1162) |        |   | ://www.amazon.com/gp/ |
|                       | | -      |    fun |   | product/1491938455/re |
|                       | | abeced | ction, |   | f=as_li_tl?ie=UTF8&ca |
|                       | | arian, |     [3 |   | mp=1789&creative=9325 |
|                       | |        | .2](th |   | &creativeASIN=1491938 |
|                       | |    [8. | inkpyt |   | 455&linkCode=as2&tag= |
|                       | | 3](thi | hon200 |   | greenteapre01-20&link |
|                       | | nkpyth | 4.html |   | Id=CTV7PDT7E5EGGJUM){ |
|                       | | on2009 | #hevea |   | rel="nofollow"}![](ht |
|                       | | .html# | _defau |   | tp://ir-na.amazon-ads |
|                       | | hevea_ | lt164) |   | ystem.com/e/ir?t=gree |
|                       | | defaul | -      |   | nteapre01-20&l=as2&o= |
|                       | | t567), |   loga |   | 1&a=1491938455){.c003 |
|                       | |     [9 | rithm, |   | width="1" height="1"  |
|                       | | .2](th |        |   | border="0"}           |
|                       | | inkpyt |  [13.1 |   |                       |
|                       | | hon201 | 2](thi |   | [Think                |
|                       | | 0.html | nkpyth |   | Java](http            |
|                       | | #hevea | on2014 |   | ://www.amazon.com/gp/ |
|                       | | _defau | .html# |   | product/1491929561/re |
|                       | | lt662) | hevea_ |   | f=as_li_tl?ie=UTF8&ca |
|                       | | -      | defaul |   | mp=1789&creative=9325 |
|                       | |    abs | t1207) |   | &creativeASIN=1491929 |
|                       | |        | -      |   | 561&linkCode=as2&tag= |
|                       | |    fun |  logar |   | greenteapre01-20&link |
|                       | | ction, | ithmic |   | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | |     [6 |     g  |   | rel="nofollow"}![](ht |
|                       | | .1](th | rowth, |   | tp://ir-na.amazon-ads |
|                       | | inkpyt |        |   | ystem.com/e/ir?t=gree |
|                       | | hon200 |    [B. |   | nteapre01-20&l=as2&o= |
|                       | | 7.html | 1](thi |   | 1&a=1491929561){.c003 |
|                       | | #hevea | nkpyth |   | width="1" height="1"  |
|                       | | _defau | on2022 |   | border="0"}           |
|                       | | lt427) | .html# |   |                       |
|                       | | -   ab | hevea_ |   | [                     |
|                       | | solute | defaul |   | ![](http://ws-na.amaz |
|                       | |        | t1829) |   | on-adsystem.com/widge |
|                       | |  path, | -   l  |   | ts/q?_encoding=UTF8&A |
|                       | |        | ogical |   | SIN=1491929561&Format |
|                       | |  [14.4 |        |   | =_SL160_&ID=AsinImage |
|                       | | ](thin |    ope |   | &MarketPlace=US&Servi |
|                       | | kpytho | rator, |   | ceVersion=20070822&WS |
|                       | | n2015. |        |   | =1&tag=greenteapre01- |
|                       | | html#h |    [5. |   | 20){border="0"}](http |
|                       | | evea_d | 2](thi |   | ://www.amazon.com/gp/ |
|                       | | efault | nkpyth |   | product/1491929561/re |
|                       | | 1237), | on2006 |   | f=as_li_tl?ie=UTF8&ca |
|                       | |        | .html# |   | mp=1789&creative=9325 |
|                       | |  [14.1 | hevea_ |   | &creativeASIN=1491929 |
|                       | | 1](thi | defaul |   | 561&linkCode=as2&tag= |
|                       | | nkpyth | t322), |   | greenteapre01-20&link |
|                       | | on2015 |     [5 |   | Id=PT77ANWARUNNU3UK){ |
|                       | | .html# | .3](th |   | rel="nofollow"}![](ht |
|                       | | hevea_ | inkpyt |   | tp://ir-na.amazon-ads |
|                       | | defaul | hon200 |   | ystem.com/e/ir?t=gree |
|                       | | t1310) | 6.html |   | nteapre01-20&l=as2&o= |
|                       | | -   a  | #hevea |   | 1&a=1491929561){.c003 |
|                       | | ccess, | _defau |   | width="1" height="1"  |
|                       | |        | lt332) |   | border="0"}           |
|                       | |    [10 | -   l  |   |                       |
|                       | | .2](th | ookup, |   | [Think                |
|                       | | inkpyt |        |   | Bay                   |
|                       | | hon201 |    [11 |   | es](http://www.amazon |
|                       | | 1.html | .9](th |   | .com/gp/product/14493 |
|                       | | #hevea | inkpyt |   | 70780/ref=as_li_qf_sp |
|                       | | _defau | hon201 |   | _asin_tl?ie=UTF8&camp |
|                       | | lt709) | 2.html |   | =1789&creative=9325&c |
|                       | | -      | #hevea |   | reativeASIN=144937078 |
|                       | | accumu | _defau |   | 0&linkCode=as2&tag=gr |
|                       | | lator, | lt980) |   | eenteapre01-20)![](ht |
|                       | |        | -   l  |   | tp://ir-na.amazon-ads |
|                       | |   [10. | ookup, |   | ystem.com/e/ir?t=gree |
|                       | | 14](th |        |   | nteapre01-20&l=as2&o= |
|                       | | inkpyt |  dicti |   | 1&a=1449370780){.c003 |
|                       | | hon201 | onary, |   | width="1" height="1"  |
|                       | | 1.html |        |   | border="0"}           |
|                       | | #hevea |    [11 |   |                       |
|                       | | _defau | .4](th |   | [![](http://ws        |
|                       | | lt846) | inkpyt |   | -na.amazon-adsystem.c |
|                       | |     -  | hon201 |   | om/widgets/q?_encodin |
|                       | |   hist | 2.html |   | g=UTF8&ASIN=144937078 |
|                       | | ogram, | #hevea |   | 0&Format=_SL160_&ID=A |
|                       | |        | _defau |   | sinImage&MarketPlace= |
|                       | |   [13. | lt922) |   | US&ServiceVersion=200 |
|                       | | 3](thi | -      |   | 70822&WS=1&tag=greent |
|                       | | nkpyth |  loop, |   | eapre01-20){border="0 |
|                       | | on2014 |        |   | "}](http://www.amazon |
|                       | | .html# |    [4. |   | .com/gp/product/14493 |
|                       | | hevea_ | 2](thi |   | 70780/ref=as_li_qf_sp |
|                       | | defaul | nkpyth |   | _asin_il?ie=UTF8&camp |
|                       | | t1163) | on2005 |   | =1789&creative=9325&c |
|                       | |        | .html# |   | reativeASIN=144937078 |
|                       | |    -   | hevea_ |   | 0&linkCode=as2&tag=gr |
|                       | |  list, | defaul |   | eenteapre01-20)![](ht |
|                       | |        | t266), |   | tp://ir-na.amazon-ads |
|                       | |    [10 |        |   | ystem.com/e/ir?t=gree |
|                       | | .7](th |   [4.1 |   | nteapre01-20&l=as2&o= |
|                       | | inkpyt | 1](thi |   | 1&a=1449370780){.c003 |
|                       | | hon201 | nkpyth |   | width="1" height="1"  |
|                       | | 1.html | on2005 |   | border="0"}           |
|                       | | #hevea | .html# |   |                       |
|                       | | _defau | hevea_ |   | [Think Python         |
|                       | | lt775) | defaul |   | 2e](http              |
|                       | |        | t293), |   | ://www.amazon.com/gp/ |
|                       | |  -   s |        |   | product/1491939362/re |
|                       | | tring, |    [7. |   | f=as_li_tl?ie=UTF8&ca |
|                       | |        | 3](thi |   | mp=1789&creative=9325 |
|                       | |   [18. | nkpyth |   | &creativeASIN=1491939 |
|                       | | 5](thi | on2008 |   | 362&linkCode=as2&tag= |
|                       | | nkpyth | .html# |   | greenteapre01-20&link |
|                       | | on2019 | hevea_ |   | Id=FJKSQ3IHEMY2F2VA){ |
|                       | | .html# | defaul |   | rel="nofollow"}![](ht |
|                       | | hevea_ | t510), |   | tp://ir-na.amazon-ads |
|                       | | defaul |        |   | ystem.com/e/ir?t=gree |
|                       | | t1592) |   [12. |   | nteapre01-20&l=as2&o= |
|                       | |     -  | 5](thi |   | 1&a=1491939362){.c003 |
|                       | |   sum, | nkpyth |   | width="1" height="1"  |
|                       | |        | on2013 |   | border="0"}           |
|                       | |    [10 | .html# |   |                       |
|                       | | .7](th | hevea_ |   | [                     |
|                       | | inkpyt | defaul |   | ![](http://ws-na.amaz |
|                       | | hon201 | t1071) |   | on-adsystem.com/widge |
|                       | | 1.html |     -  |   | ts/q?_encoding=UTF8&A |
|                       | | #hevea |   cond |   | SIN=1491939362&Format |
|                       | | _defau | ition, |   | =_SL160_&ID=AsinImage |
|                       | | lt771) |        |   | &MarketPlace=US&Servi |
|                       | | -      |        |   | ceVersion=20070822&WS |
|                       | |    add |  [A.2. |   | =1&tag=greenteapre01- |
|                       | |     m  | 2](thi |   | 20){border="0"}](http |
|                       | | ethod, | nkpyth |   | ://www.amazon.com/gp/ |
|                       | |        | on2021 |   | product/1491939362/re |
|                       | |   [17. | .html# |   | f=as_li_tl?ie=UTF8&ca |
|                       | | 7](thi | hevea_ |   | mp=1789&creative=9325 |
|                       | | nkpyth | defaul |   | &creativeASIN=1491939 |
|                       | | on2018 | t1760) |   | 362&linkCode=as2&tag= |
|                       | | .html# |     -  |   | greenteapre01-20&link |
|                       | | hevea_ |   for, |   | Id=ZZ454DLQ3IXDHNHX){ |
|                       | | defaul |        |   | rel="nofollow"}![](ht |
|                       | | t1500) |    [4. |   | tp://ir-na.amazon-ads |
|                       | | -   ad | 2](thi |   | ystem.com/e/ir?t=gree |
|                       | | dition | nkpyth |   | nteapre01-20&l=as2&o= |
|                       | |        | on2005 |   | 1&a=1491939362){.c003 |
|                       | |   with | .html# |   | width="1" height="1"  |
|                       | |        | hevea_ |   | border="0"}           |
|                       | |    car | defaul |   |                       |
|                       | | rying, | t264), |   | [Think Stats          |
|                       | |     [7 |        |   | 2e](http://ww         |
|                       | | .6](th |    [5. |   | w.amazon.com/gp/produ |
|                       | | inkpyt | 8](thi |   | ct/1491907339/ref=as_ |
|                       | | hon200 | nkpyth |   | li_tl?ie=UTF8&camp=17 |
|                       | | 8.html | on2006 |   | 89&creative=9325&crea |
|                       | | #hevea | .html# |   | tiveASIN=1491907339&l |
|                       | | _defau | hevea_ |   | inkCode=as2&tag=green |
|                       | | lt523) | defaul |   | teapre01-20&linkId=O7 |
|                       | | -      | t367), |   | WYM6H6YBYUFNWU)![](ht |
|                       | |   algo |        |   | tp://ir-na.amazon-ads |
|                       | | rithm, |    [8. |   | ystem.com/e/ir?t=gree |
|                       | |        | 3](thi |   | nteapre01-20&l=as2&o= |
|                       | |    [7. | nkpyth |   | 1&a=1491907339){.c003 |
|                       | | 6](thi | on2009 |   | width="1" height="1"  |
|                       | | nkpyth | .html# |   | border="0"}           |
|                       | | on2008 | hevea_ |   |                       |
|                       | | .html# | defaul |   | [![](h                |
|                       | | hevea_ | t563), |   | ttp://ws-na.amazon-ad |
|                       | | defaul |        |   | system.com/widgets/q? |
|                       | | t522), |    [10 |   | _encoding=UTF8&ASIN=1 |
|                       | |        | .3](th |   | 491907339&Format=_SL1 |
|                       | |    [7. | inkpyt |   | 60_&ID=AsinImage&Mark |
|                       | | 8](thi | hon201 |   | etPlace=US&ServiceVer |
|                       | | nkpyth | 1.html |   | sion=20070822&WS=1&ta |
|                       | | on2008 | #hevea |   | g=greenteapre01-20){b |
|                       | | .html# | _defau |   | order="0"}](http://ww |
|                       | | hevea_ | lt731) |   | w.amazon.com/gp/produ |
|                       | | defaul |     -  |   | ct/1491907339/ref=as_ |
|                       | | t536), |    inf |   | li_tl?ie=UTF8&camp=17 |
|                       | |        | inite, |   | 89&creative=9325&crea |
|                       | |  [13.7 |        |   | tiveASIN=1491907339&l |
|                       | | ](thin |    [7. |   | inkCode=as2&tag=green |
|                       | | kpytho | 3](thi |   | teapre01-20&linkId=JV |
|                       | | n2014. | nkpyth |   | SYKQHYSUIEYRHL)![](ht |
|                       | | html#h | on2008 |   | tp://ir-na.amazon-ads |
|                       | | evea_d | .html# |   | ystem.com/e/ir?t=gree |
|                       | | efault | hevea_ |   | nteapre01-20&l=as2&o= |
|                       | | 1178), | defaul |   | 1&a=1491907339){.c003 |
|                       | |     [  | t513), |   | width="1" height="1"  |
|                       | | B](thi |        |   | border="0"}           |
|                       | | nkpyth |        |   |                       |
|                       | | on2022 |  [A.2. |   | [Think                |
|                       | | .html# | 2](thi |   | Complexity](http      |
|                       | | hevea_ | nkpyth |   | ://www.amazon.com/gp/ |
|                       | | defaul | on2021 |   | product/1449314635/re |
|                       | | t1810) | .html# |   | f=as_li_tf_tl?ie=UTF8 |
|                       | |     -  | hevea_ |   | &tag=greenteapre01-20 |
|                       | |   MD5, | defaul |   | &linkCode=as2&camp=17 |
|                       | |        | t1758) |   | 89&creative=9325&crea |
|                       | |        |        |   | tiveASIN=1449314635)! |
|                       | |  [14.1 |  -   n |   | [](http://www.assoc-a |
|                       | | 2](thi | ested, |   | mazon.com/e/ir?t=gree |
|                       | | nkpyth |        |   | nteapre01-20&l=as2&o= |
|                       | | on2015 |   [18. |   | 1&a=1449314635){.c003 |
|                       | | .html# | 4](thi |   | width="1" height="1"  |
|                       | | hevea_ | nkpyth |   | border="0"}           |
|                       | | defaul | on2019 |   |                       |
|                       | | t1323) | .html# |   | [                     |
|                       | |        | hevea_ |   | ![](http://ws-na.amaz |
|                       | |   -    | defaul |   | on-adsystem.com/widge |
|                       | | square | t1585) |   | ts/q?_encoding=UTF8&A |
|                       | |        |     -  |   | SIN=1449314635&Format |
|                       | |        |   trav |   | =_SL160_&ID=AsinImage |
|                       | |  root, | ersal, |   | &MarketPlace=US&Servi |
|                       | |        |        |   | ceVersion=20070822&WS |
|                       | |     [7 |     [8 |   | =1&tag=greenteapre01- |
|                       | | .9](th | .3](th |   | 20){border="0"}](http |
|                       | | inkpyt | inkpyt |   | ://www.amazon.com/gp/ |
|                       | | hon200 | hon200 |   | product/1449314635/re |
|                       | | 8.html | 9.html |   | f=as_li_tf_il?ie=UTF8 |
|                       | | #hevea | #hevea |   | &camp=1789&creative=9 |
|                       | | _defau | _defau |   | 325&creativeASIN=1449 |
|                       | | lt537) | lt561) |   | 314635&linkCode=as2&t |
|                       | | -      |        |   | ag=greenteapre01-20)! |
|                       | |    ali |   -    |   | [](http://www.assoc-a |
|                       | | asing, | while, |   | mazon.com/e/ir?t=gree |
|                       | |        |        |   | nteapre01-20&l=as2&o= |
|                       | |  [10.1 |     [7 |   | 1&a=1449314635){.c003 |
|                       | | 0](thi | .3](th |   | width="1" height="1"  |
|                       | | nkpyth | inkpyt |   | border="0"}           |
|                       | | on2011 | hon200 |   |                       |
|                       | | .html# | 8.html |   |                       |
|                       | | hevea_ | #hevea |   |                       |
|                       | | defaul | _defau |   |                       |
|                       | | t807), | lt506) |   |                       |
|                       | |        | -      |   |                       |
|                       | |  [10.1 |   loop |   |                       |
|                       | | 1](thi |        |   |                       |
|                       | | nkpyth |    var |   |                       |
|                       | | on2011 | iable, |   |                       |
|                       | | .html# |        |   |                       |
|                       | | hevea_ |   [19. |   |                       |
|                       | | defaul | 2](thi |   |                       |
|                       | | t816), | nkpyth |   |                       |
|                       | |        | on2020 |   |                       |
|                       | |  [10.1 | .html# |   |                       |
|                       | | 4](thi | hevea_ |   |                       |
|                       | | nkpyth | defaul |   |                       |
|                       | | on2011 | t1673) |   |                       |
|                       | | .html# | -   l  |   |                       |
|                       | | hevea_ | ooping |   |                       |
|                       | | defaul |     -  |   |                       |
|                       | | t860), |   with |   |                       |
|                       | |        |        |   |                       |
|                       | |  [15.2 |      d |   |                       |
|                       | | ](thin | iction |   |                       |
|                       | | kpytho | aries, |   |                       |
|                       | | n2016. |        |   |                       |
|                       | | html#h |    [11 |   |                       |
|                       | | evea_d | .3](th |   |                       |
|                       | | efault | inkpyt |   |                       |
|                       | | 1352), | hon201 |   |                       |
|                       | |        | 2.html |   |                       |
|                       | |  [15.6 | #hevea |   |                       |
|                       | | ](thin | _defau |   |                       |
|                       | | kpytho | lt916) |   |                       |
|                       | | n2016. |     -  |   |                       |
|                       | | html#h |   with |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault |     in |   |                       |
|                       | | 1366), | dices, |   |                       |
|                       | |        |        |   |                       |
|                       | |  [17.1 |    [9. |   |                       |
|                       | | 3](thi | 4](thi |   |                       |
|                       | | nkpyth | nkpyth |   |                       |
|                       | | on2018 | on2010 |   |                       |
|                       | | .html# | .html# |   |                       |
|                       | | hevea_ | hevea_ |   |                       |
|                       | | defaul | defaul |   |                       |
|                       | | t1545) | t672), |   |                       |
|                       | |        |        |   |                       |
|                       | |  -   c |    [10 |   |                       |
|                       | | opying | .3](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |     to | hon201 |   |                       |
|                       | |        | 1.html |   |                       |
|                       | |        | #hevea |   |                       |
|                       | | avoid, | _defau |   |                       |
|                       | |        | lt733) |   |                       |
|                       | |   [10. |     -  |   |                       |
|                       | | 13](th |   with |   |                       |
|                       | | inkpyt |        |   |                       |
|                       | | hon201 |     st |   |                       |
|                       | | 1.html | rings, |   |                       |
|                       | | #hevea |        |   |                       |
|                       | | _defau |     [8 |   |                       |
|                       | | lt839) | .7](th |   |                       |
|                       | | -      | inkpyt |   |                       |
|                       | |   all, | hon200 |   |                       |
|                       | |        | 9.html |   |                       |
|                       | |   [19. | #hevea |   |                       |
|                       | | 4](thi | _defau |   |                       |
|                       | | nkpyth | lt596) |   |                       |
|                       | | on2020 | -   l  |   |                       |
|                       | | .html# | ooping |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |    and |   |                       |
|                       | | t1691) |        |   |                       |
|                       | | -      |    cou |   |                       |
|                       | |    alp | nting, |   |                       |
|                       | | habet, |     [8 |   |                       |
|                       | |        | .7](th |   |                       |
|                       | |    [4. | inkpyt |   |                       |
|                       | | 12](th | hon200 |   |                       |
|                       | | inkpyt | 9.html |   |                       |
|                       | | hon200 | #hevea |   |                       |
|                       | | 5.html | _defau |   |                       |
|                       | | #hevea | lt595) |   |                       |
|                       | | _defau | -      |   |                       |
|                       | | lt307) |    low |   |                       |
|                       | | -      | -level |   |                       |
|                       | |  alter |        |   |                       |
|                       | | native |    lan |   |                       |
|                       | |        | guage, |   |                       |
|                       | |   exec |     [  |   |                       |
|                       | | ution, | 1.8](t |   |                       |
|                       | |     [5 | hinkpy |   |                       |
|                       | | .5](th | thon20 |   |                       |
|                       | | inkpyt | 02.htm |   |                       |
|                       | | hon200 | l#heve |   |                       |
|                       | | 6.html | a_defa |   |                       |
|                       | | #hevea | ult65) |   |                       |
|                       | | _defau | -   ls |   |                       |
|                       | | lt350) |        |   |                       |
|                       | | -      |  (Unix |   |                       |
|                       | |   ambi |        |   |                       |
|                       | | guity, |    com |   |                       |
|                       | |     [  | mand), |   |                       |
|                       | | 1.6](t |        |   |                       |
|                       | | hinkpy |  [14.8 |   |                       |
|                       | | thon20 | ](thin |   |                       |
|                       | | 02.htm | kpytho |   |                       |
|                       | | l#heve | n2015. |   |                       |
|                       | | a_defa | html#h |   |                       |
|                       | | ult53) | evea_d |   |                       |
|                       | | -   an | efault |   |                       |
|                       | | agram, | 1272)\ |   |                       |
|                       | |        |     \  |   |                       |
|                       | |   [10. | -      |   |                       |
|                       | | 15](th | Markov |   |                       |
|                       | | inkpyt |        |   |                       |
|                       | | hon201 |    ana |   |                       |
|                       | | 1.html | lysis, |   |                       |
|                       | | #hevea |        |   |                       |
|                       | | _defau |   [13. |   |                       |
|                       | | lt863) | 8](thi |   |                       |
|                       | | -   a  | nkpyth |   |                       |
|                       | | nagram | on2014 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |   set, | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | | [12.10 | t1179) |   |                       |
|                       | | ](thin | -      |   |                       |
|                       | | kpytho |   McCl |   |                       |
|                       | | n2013. | oskey, |   |                       |
|                       | | html#h |     R  |   |                       |
|                       | | evea_d | obert, |   |                       |
|                       | | efault |     [8 |   |                       |
|                       | | 1124), | .3](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |  [14.1 | hon200 |   |                       |
|                       | | 2](thi | 9.html |   |                       |
|                       | | nkpyth | #hevea |   |                       |
|                       | | on2015 | _defau |   |                       |
|                       | | .html# | lt568) |   |                       |
|                       | | hevea_ | -      |   |                       |
|                       | | defaul |    MD5 |   |                       |
|                       | | t1318) |        |   |                       |
|                       | | -   an |   algo |   |                       |
|                       | | alysis | rithm, |   |                       |
|                       | |     of |        |   |                       |
|                       | |        |  [14.1 |   |                       |
|                       | |  algor | 2](thi |   |                       |
|                       | | ithms, | nkpyth |   |                       |
|                       | |     [B | on2015 |   |                       |
|                       | | ](thin | .html# |   |                       |
|                       | | kpytho | hevea_ |   |                       |
|                       | | n2022. | defaul |   |                       |
|                       | | html#h | t1322) |   |                       |
|                       | | evea_d | -   M  |   |                       |
|                       | | efault | eyers, |   |                       |
|                       | | 1811), |        |   |                       |
|                       | |        | Chris, |   |                       |
|                       | |    [B. |        |   |                       |
|                       | | 5](thi |   [0]( |   |                       |
|                       | | nkpyth | thinkp |   |                       |
|                       | | on2022 | ython2 |   |                       |
|                       | | .html# | 001.ht |   |                       |
|                       | | hevea_ | ml#hev |   |                       |
|                       | | defaul | ea_def |   |                       |
|                       | | t1860) | ault5) |   |                       |
|                       | | -   an | -      |   |                       |
|                       | | alysis |   Moby |   |                       |
|                       | |     of |     Pr |   |                       |
|                       | |        | oject, |   |                       |
|                       | |  primi |     [9 |   |                       |
|                       | | tives, | .1](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |    [B. | hon201 |   |                       |
|                       | | 2](thi | 0.html |   |                       |
|                       | | nkpyth | #hevea |   |                       |
|                       | | on2022 | _defau |   |                       |
|                       | | .html# | lt646) |   |                       |
|                       | | hevea_ | -      |   |                       |
|                       | | defaul |  Monty |   |                       |
|                       | | t1831) |        |   |                       |
|                       | | -      | Python |   |                       |
|                       | |    and |        |   |                       |
|                       | |        |    and |   |                       |
|                       | |    ope |        |   |                       |
|                       | | rator, |    the |   |                       |
|                       | |     [5 |        |   |                       |
|                       | | .3](th |   Holy |   |                       |
|                       | | inkpyt |        |   |                       |
|                       | | hon200 | Grail, |   |                       |
|                       | | 6.html |        |   |                       |
|                       | | #hevea |   [16. |   |                       |
|                       | | _defau | 2](thi |   |                       |
|                       | | lt334) | nkpyth |   |                       |
|                       | | -      | on2017 |   |                       |
|                       | |   any, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |   [19. | defaul |   |                       |
|                       | | 4](thi | t1425) |   |                       |
|                       | | nkpyth | -      |   |                       |
|                       | | on2020 |   MP3, |   |                       |
|                       | | .html# |        |   |                       |
|                       | | hevea_ |  [14.1 |   |                       |
|                       | | defaul | 2](thi |   |                       |
|                       | | t1685) | nkpyth |   |                       |
|                       | | -      | on2015 |   |                       |
|                       | | append | .html# |   |                       |
|                       | |     m  | hevea_ |   |                       |
|                       | | ethod, | defaul |   |                       |
|                       | |        | t1320) |   |                       |
|                       | |   [10. | -   m  |   |                       |
|                       | | 6](thi | achine |   |                       |
|                       | | nkpyth |        |   |                       |
|                       | | on2011 | model, |   |                       |
|                       | | .html# |     [B |   |                       |
|                       | | hevea_ | ](thin |   |                       |
|                       | | defaul | kpytho |   |                       |
|                       | | t757), | n2022. |   |                       |
|                       | |        | html#h |   |                       |
|                       | |  [10.1 | evea_d |   |                       |
|                       | | 2](thi | efault |   |                       |
|                       | | nkpyth | 1817), |   |                       |
|                       | | on2011 |        |   |                       |
|                       | | .html# |    [B. |   |                       |
|                       | | hevea_ | 5](thi |   |                       |
|                       | | defaul | nkpyth |   |                       |
|                       | | t830), | on2022 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |  [10.1 | hevea_ |   |                       |
|                       | | 5](thi | defaul |   |                       |
|                       | | nkpyth | t1861) |   |                       |
|                       | | on2011 | -      |   |                       |
|                       | | .html# |  main, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |    [3. |   |                       |
|                       | | t871), | 9](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |  [18.4 | on2004 |   |                       |
|                       | | ](thin | .html# |   |                       |
|                       | | kpytho | hevea_ |   |                       |
|                       | | n2019. | defaul |   |                       |
|                       | | html#h | t214), |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault |    [5. |   |                       |
|                       | | 1588), | 8](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |   [18. | on2006 |   |                       |
|                       | | 6](thi | .html# |   |                       |
|                       | | nkpyth | hevea_ |   |                       |
|                       | | on2019 | defaul |   |                       |
|                       | | .html# | t361), |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |   [11. |   |                       |
|                       | | t1599) | 7](thi |   |                       |
|                       | | -      | nkpyth |   |                       |
|                       | |    arc | on2012 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |    fun | hevea_ |   |                       |
|                       | | ction, | defaul |   |                       |
|                       | |     [4 | t952), |   |                       |
|                       | | .3](th |        |   |                       |
|                       | | inkpyt |   [14. |   |                       |
|                       | | hon200 | 9](thi |   |                       |
|                       | | 5.html | nkpyth |   |                       |
|                       | | #hevea | on2015 |   |                       |
|                       | | _defau | .html# |   |                       |
|                       | | lt271) | hevea_ |   |                       |
|                       | | -      | defaul |   |                       |
|                       | |    arg | t1291) |   |                       |
|                       | | ument, | -   m  |   |                       |
|                       | |        | aintai |   |                       |
|                       | |    [3. | nable, |   |                       |
|                       | | 1](thi |        |   |                       |
|                       | | nkpyth |  [17.1 |   |                       |
|                       | | on2004 | 1](thi |   |                       |
|                       | | .html# | nkpyth |   |                       |
|                       | | hevea_ | on2018 |   |                       |
|                       | | defaul | .html# |   |                       |
|                       | | t149), | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | |    [3. | t1526) |   |                       |
|                       | | 4](thi | -      |   |                       |
|                       | | nkpyth |    map |   |                       |
|                       | | on2004 |     pa |   |                       |
|                       | | .html# | ttern, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |   [10. |   |                       |
|                       | | t181), | 7](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |    [3. | on2011 |   |                       |
|                       | | 7](thi | .html# |   |                       |
|                       | | nkpyth | hevea_ |   |                       |
|                       | | on2004 | defaul |   |                       |
|                       | | .html# | t776), |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |   [10. |   |                       |
|                       | | t195), | 14](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |    [3. | hon201 |   |                       |
|                       | | 7](thi | 1.html |   |                       |
|                       | | nkpyth | #hevea |   |                       |
|                       | | on2004 | _defau |   |                       |
|                       | | .html# | lt852) |   |                       |
|                       | | hevea_ | -      |   |                       |
|                       | | defaul |    map |   |                       |
|                       | | t201), |        |   |                       |
|                       | |        |    to, |   |                       |
|                       | |   [3.1 |        |   |                       |
|                       | | 3](thi |   [18. |   |                       |
|                       | | nkpyth | 1](thi |   |                       |
|                       | | on2004 | nkpyth |   |                       |
|                       | | .html# | on2019 |   |                       |
|                       | | hevea_ | .html# |   |                       |
|                       | | defaul | hevea_ |   |                       |
|                       | | t239), | defaul |   |                       |
|                       | |        | t1555) |   |                       |
|                       | |   [10. | -   ma |   |                       |
|                       | | 12](th | pping, |   |                       |
|                       | | inkpyt |        |   |                       |
|                       | | hon201 |   [11. |   |                       |
|                       | | 1.html | 9](thi |   |                       |
|                       | | #hevea | nkpyth |   |                       |
|                       | | _defau | on2012 |   |                       |
|                       | | lt824) | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |  -   g | defaul |   |                       |
|                       | | ather, | t970), |   |                       |
|                       | |        |        |   |                       |
|                       | |   [12. |   [13. |   |                       |
|                       | | 4](thi | 8](thi |   |                       |
|                       | | nkpyth | nkpyth |   |                       |
|                       | | on2013 | on2014 |   |                       |
|                       | | .html# | .html# |   |                       |
|                       | | hevea_ | hevea_ |   |                       |
|                       | | defaul | defaul |   |                       |
|                       | | t1053) | t1182) |   |                       |
|                       | |        | -   ma |   |                       |
|                       | | -   ke | sh-up, |   |                       |
|                       | | yword, |        |   |                       |
|                       | |        |   [13. |   |                       |
|                       | |    [4. | 8](thi |   |                       |
|                       | | 5](thi | nkpyth |   |                       |
|                       | | nkpyth | on2014 |   |                       |
|                       | | on2005 | .html# |   |                       |
|                       | | .html# | hevea_ |   |                       |
|                       | | hevea_ | defaul |   |                       |
|                       | | defaul | t1185) |   |                       |
|                       | | t277), | -      |   |                       |
|                       | |        |   math |   |                       |
|                       | |   [4.1 |        |   |                       |
|                       | | 1](thi |    fun |   |                       |
|                       | | nkpyth | ction, |   |                       |
|                       | | on2005 |     [3 |   |                       |
|                       | | .html# | .2](th |   |                       |
|                       | | hevea_ | inkpyt |   |                       |
|                       | | defaul | hon200 |   |                       |
|                       | | t297), | 4.html |   |                       |
|                       | |        | #hevea |   |                       |
|                       | |   [19. | _defau |   |                       |
|                       | | 9](thi | lt159) |   |                       |
|                       | | nkpyth | -      |   |                       |
|                       | | on2020 |  matpl |   |                       |
|                       | | .html# | otlib, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |  [13.1 |   |                       |
|                       | | t1722) | 2](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |    -   | on2014 |   |                       |
|                       | |  list, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |   [10. | defaul |   |                       |
|                       | | 12](th | t1208) |   |                       |
|                       | | inkpyt | -      |   |                       |
|                       | | hon201 |    max |   |                       |
|                       | | 1.html |        |   |                       |
|                       | | #hevea |    fun |   |                       |
|                       | | _defau | ction, |   |                       |
|                       | | lt825) |        |   |                       |
|                       | |     -  |  [12.3 |   |                       |
|                       | |    opt | ](thin |   |                       |
|                       | | ional, | kpytho |   |                       |
|                       | |        | n2013. |   |                       |
|                       | |    [8. | html#h |   |                       |
|                       | | 8](thi | evea_d |   |                       |
|                       | | nkpyth | efault |   |                       |
|                       | | on2009 | 1045), |   |                       |
|                       | | .html# |        |   |                       |
|                       | | hevea_ |   [12. |   |                       |
|                       | | defaul | 4](thi |   |                       |
|                       | | t604), | nkpyth |   |                       |
|                       | |        | on2013 |   |                       |
|                       | |   [8.1 | .html# |   |                       |
|                       | | 2](thi | hevea_ |   |                       |
|                       | | nkpyth | defaul |   |                       |
|                       | | on2009 | t1058) |   |                       |
|                       | | .html# | -      |   |                       |
|                       | | hevea_ |   md5, |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t633), |   [14. |   |                       |
|                       | |        | 8](thi |   |                       |
|                       | |   [8.1 | nkpyth |   |                       |
|                       | | 3](thi | on2015 |   |                       |
|                       | | nkpyth | .html# |   |                       |
|                       | | on2009 | hevea_ |   |                       |
|                       | | .html# | defaul |   |                       |
|                       | | hevea_ | t1282) |   |                       |
|                       | | defaul | -   m  |   |                       |
|                       | | t637), | d5sum, |   |                       |
|                       | |        |        |   |                       |
|                       | |   [10. |  [14.1 |   |                       |
|                       | | 9](thi | 2](thi |   |                       |
|                       | | nkpyth | nkpyth |   |                       |
|                       | | on2011 | on2015 |   |                       |
|                       | | .html# | .html# |   |                       |
|                       | | hevea_ | hevea_ |   |                       |
|                       | | defaul | defaul |   |                       |
|                       | | t798), | t1325) |   |                       |
|                       | |        | -      |   |                       |
|                       | |   [11. |   memb |   |                       |
|                       | | 4](thi | ership |   |                       |
|                       | | nkpyth |        |   |                       |
|                       | | on2012 |   -    |   |                       |
|                       | | .html# | binary |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |      s |   |                       |
|                       | | t932), | earch, |   |                       |
|                       | |        |        |   |                       |
|                       | |   [19. |   [10. |   |                       |
|                       | | 1](thi | 15](th |   |                       |
|                       | | nkpyth | inkpyt |   |                       |
|                       | | on2020 | hon201 |   |                       |
|                       | | .html# | 1.html |   |                       |
|                       | | hevea_ | #hevea |   |                       |
|                       | | defaul | _defau |   |                       |
|                       | | t1667) | lt880) |   |                       |
|                       | |        |     -  |   |                       |
|                       | |    -   |    bis |   |                       |
|                       | |  posit | ection |   |                       |
|                       | | ional, |        |   |                       |
|                       | |        |      s |   |                       |
|                       | |        | earch, |   |                       |
|                       | |  [17.3 |        |   |                       |
|                       | | ](thin |   [10. |   |                       |
|                       | | kpytho | 15](th |   |                       |
|                       | | n2018. | inkpyt |   |                       |
|                       | | html#h | hon201 |   |                       |
|                       | | evea_d | 1.html |   |                       |
|                       | | efault | #hevea |   |                       |
|                       | | 1482), | _defau |   |                       |
|                       | |        | lt877) |   |                       |
|                       | |        |        |   |                       |
|                       | | [17.12 |    -   |   |                       |
|                       | | ](thin |  dicti |   |                       |
|                       | | kpytho | onary, |   |                       |
|                       | | n2018. |        |   |                       |
|                       | | html#h |    [11 |   |                       |
|                       | | evea_d | .1](th |   |                       |
|                       | | efault | inkpyt |   |                       |
|                       | | 1534), | hon201 |   |                       |
|                       | |        | 2.html |   |                       |
|                       | |   [19. | #hevea |   |                       |
|                       | | 9](thi | _defau |   |                       |
|                       | | nkpyth | lt902) |   |                       |
|                       | | on2020 |        |   |                       |
|                       | | .html# |    -   |   |                       |
|                       | | hevea_ |  list, |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t1720) |    [10 |   |                       |
|                       | |     -  | .2](th |   |                       |
|                       | |    var | inkpyt |   |                       |
|                       | | iable- | hon201 |   |                       |
|                       | | length | 1.html |   |                       |
|                       | |        | #hevea |   |                       |
|                       | |        | _defau |   |                       |
|                       | | tuple, | lt725) |   |                       |
|                       | |        |     -  |   |                       |
|                       | |   [12. |   set, |   |                       |
|                       | | 4](thi |        |   |                       |
|                       | | nkpyth |   [11. |   |                       |
|                       | | on2013 | 10](th |   |                       |
|                       | | .html# | inkpyt |   |                       |
|                       | | hevea_ | hon201 |   |                       |
|                       | | defaul | 2.html |   |                       |
|                       | | t1050) | #hevea |   |                       |
|                       | | -   ar | _defau |   |                       |
|                       | | gument | lt994) |   |                       |
|                       | |     sc | -      |   |                       |
|                       | | atter, |  memo, |   |                       |
|                       | |        |        |   |                       |
|                       | |   [12. |   [11. |   |                       |
|                       | | 4](thi | 6](thi |   |                       |
|                       | | nkpyth | nkpyth |   |                       |
|                       | | on2013 | on2012 |   |                       |
|                       | | .html# | .html# |   |                       |
|                       | | hevea_ | hevea_ |   |                       |
|                       | | defaul | defaul |   |                       |
|                       | | t1055) | t948), |   |                       |
|                       | | -      |        |   |                       |
|                       | |   arit |    [11 |   |                       |
|                       | | hmetic | .9](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |    ope | hon201 |   |                       |
|                       | | rator, | 2.html |   |                       |
|                       | |     [  | #hevea |   |                       |
|                       | | 1.4](t | _defau |   |                       |
|                       | | hinkpy | lt987) |   |                       |
|                       | | thon20 | -      |   |                       |
|                       | | 02.htm | mental |   |                       |
|                       | | l#heve |        |   |                       |
|                       | | a_defa | model, |   |                       |
|                       | | ult27) |        |   |                       |
|                       | | -      |  [A.3. |   |                       |
|                       | | assert | 1](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |   stat | on2021 |   |                       |
|                       | | ement, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |  [16.5 | defaul |   |                       |
|                       | | ](thin | t1793) |   |                       |
|                       | | kpytho | -      |   |                       |
|                       | | n2017. |    met |   |                       |
|                       | | html#h | aphor, |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault | method |   |                       |
|                       | | 1447), |        |   |                       |
|                       | |        |  invoc |   |                       |
|                       | |   [16. | ation, |   |                       |
|                       | | 6](thi |        |   |                       |
|                       | | nkpyth |   [17. |   |                       |
|                       | | on2017 | 2](thi |   |                       |
|                       | | .html# | nkpyth |   |                       |
|                       | | hevea_ | on2018 |   |                       |
|                       | | defaul | .html# |   |                       |
|                       | | t1455) | hevea_ |   |                       |
|                       | | -      | defaul |   |                       |
|                       | |  assig | t1477) |   |                       |
|                       | | nment, | -      |   |                       |
|                       | |        |  metat |   |                       |
|                       | |    [2. | hesis, |   |                       |
|                       | | 9](thi |        |   |                       |
|                       | | nkpyth |  [12.1 |   |                       |
|                       | | on2003 | 0](thi |   |                       |
|                       | | .html# | nkpyth |   |                       |
|                       | | hevea_ | on2013 |   |                       |
|                       | | defaul | .html# |   |                       |
|                       | | t127), | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | |    [7. | t1128) |   |                       |
|                       | | 1](thi | -   m  |   |                       |
|                       | | nkpyth | ethod, |   |                       |
|                       | | on2008 |        |   |                       |
|                       | | .html# |   [4.1 |   |                       |
|                       | | hevea_ | 1](thi |   |                       |
|                       | | defaul | nkpyth |   |                       |
|                       | | t493), | on2005 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |    [10 | hevea_ |   |                       |
|                       | | .1](th | defaul |   |                       |
|                       | | inkpyt | t292), |   |                       |
|                       | | hon201 |        |   |                       |
|                       | | 1.html |    [8. |   |                       |
|                       | | #hevea | 8](thi |   |                       |
|                       | | _defau | nkpyth |   |                       |
|                       | | lt707) | on2009 |   |                       |
|                       | |     -  | .html# |   |                       |
|                       | |   augm | hevea_ |   |                       |
|                       | | ented, | defaul |   |                       |
|                       | |        | t598), |   |                       |
|                       | |   [10. |        |   |                       |
|                       | | 7](thi |  [17.1 |   |                       |
|                       | | nkpyth | ](thin |   |                       |
|                       | | on2011 | kpytho |   |                       |
|                       | | .html# | n2018. |   |                       |
|                       | | hevea_ | html#h |   |                       |
|                       | | defaul | evea_d |   |                       |
|                       | | t769), | efault |   |                       |
|                       | |        | 1463), |   |                       |
|                       | |   [10. |        |   |                       |
|                       | | 14](th |  [17.1 |   |                       |
|                       | | inkpyt | 2](thi |   |                       |
|                       | | hon201 | nkpyth |   |                       |
|                       | | 1.html | on2018 |   |                       |
|                       | | #hevea | .html# |   |                       |
|                       | | _defau | hevea_ |   |                       |
|                       | | lt847) | defaul |   |                       |
|                       | |        | t1531) |   |                       |
|                       | |    -   |        |   |                       |
|                       | |  item, |   -    |   |                       |
|                       | |        | \_\_cm |   |                       |
|                       | |    [8. | p\_\_, |   |                       |
|                       | | 5](thi |        |   |                       |
|                       | | nkpyth |   [18. |   |                       |
|                       | | on2009 | 3](thi |   |                       |
|                       | | .html# | nkpyth |   |                       |
|                       | | hevea_ | on2019 |   |                       |
|                       | | defaul | .html# |   |                       |
|                       | | t585), | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | |   [10. | t1577) |   |                       |
|                       | | 2](thi |        |   |                       |
|                       | | nkpyth |   -    |   |                       |
|                       | | on2011 | \_\_st |   |                       |
|                       | | .html# | r\_\_, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t719), |  [17.6 |   |                       |
|                       | |        | ](thin |   |                       |
|                       | |   [12. | kpytho |   |                       |
|                       | | 1](thi | n2018. |   |                       |
|                       | | nkpyth | html#h |   |                       |
|                       | | on2013 | evea_d |   |                       |
|                       | | .html# | efault |   |                       |
|                       | | hevea_ | 1494), |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t1026) |   [18. |   |                       |
|                       | |        | 5](thi |   |                       |
|                       | |   -    | nkpyth |   |                       |
|                       | | tuple, | on2019 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |  [12.2 | defaul |   |                       |
|                       | | ](thin | t1591) |   |                       |
|                       | | kpytho |     -  |   |                       |
|                       | | n2013. |   add, |   |                       |
|                       | | html#h |        |   |                       |
|                       | | evea_d |   [17. |   |                       |
|                       | | efault | 7](thi |   |                       |
|                       | | 1030), | nkpyth |   |                       |
|                       | |        | on2018 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |  [12.3 | hevea_ |   |                       |
|                       | | ](thin | defaul |   |                       |
|                       | | kpytho | t1501) |   |                       |
|                       | | n2013. |        |   |                       |
|                       | | html#h |  -   a |   |                       |
|                       | | evea_d | ppend, |   |                       |
|                       | | efault |        |   |                       |
|                       | | 1044), |   [10. |   |                       |
|                       | |        | 6](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |  [12.5 | on2011 |   |                       |
|                       | | ](thin | .html# |   |                       |
|                       | | kpytho | hevea_ |   |                       |
|                       | | n2013. | defaul |   |                       |
|                       | | html#h | t758), |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault |        |   |                       |
|                       | | 1070), |  [10.1 |   |                       |
|                       | |        | 2](thi |   |                       |
|                       | |   [12. | nkpyth |   |                       |
|                       | | 9](thi | on2011 |   |                       |
|                       | | nkpyth | .html# |   |                       |
|                       | | on2013 | hevea_ |   |                       |
|                       | | .html# | defaul |   |                       |
|                       | | hevea_ | t831), |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t1114) |        |   |                       |
|                       | | -      |  [10.1 |   |                       |
|                       | |   assi | 5](thi |   |                       |
|                       | | gnment | nkpyth |   |                       |
|                       | |        | on2011 |   |                       |
|                       | |   stat | .html# |   |                       |
|                       | | ement, | hevea_ |   |                       |
|                       | |     [  | defaul |   |                       |
|                       | | 2.1](t | t872), |   |                       |
|                       | | hinkpy |        |   |                       |
|                       | | thon20 |        |   |                       |
|                       | | 03.htm |  [18.4 |   |                       |
|                       | | l#heve | ](thin |   |                       |
|                       | | a_defa | kpytho |   |                       |
|                       | | ult89) | n2019. |   |                       |
|                       | | -      | html#h |   |                       |
|                       | |   attr | evea_d |   |                       |
|                       | | ibute, | efault |   |                       |
|                       | |        | 1589), |   |                       |
|                       | |  [15.7 |        |   |                       |
|                       | | ](thin |   [18. |   |                       |
|                       | | kpytho | 6](thi |   |                       |
|                       | | n2016. | nkpyth |   |                       |
|                       | | html#h | on2019 |   |                       |
|                       | | evea_d | .html# |   |                       |
|                       | | efault | hevea_ |   |                       |
|                       | | 1395), | defaul |   |                       |
|                       | |        | t1600) |   |                       |
|                       | |  [17.1 |        |   |                       |
|                       | | 1](thi |   -    |   |                       |
|                       | | nkpyth | close, |   |                       |
|                       | | on2018 |        |   |                       |
|                       | | .html# |        |   |                       |
|                       | | hevea_ |  [14.2 |   |                       |
|                       | | defaul | ](thin |   |                       |
|                       | | t1528) | kpytho |   |                       |
|                       | |        | n2015. |   |                       |
|                       | |  -   \ | html#h |   |                       |
|                       | | _\_dic | evea_d |   |                       |
|                       | | t\_\_, | efault |   |                       |
|                       | |        | 1218), |   |                       |
|                       | |        |        |   |                       |
|                       | |  [17.1 |        |   |                       |
|                       | | 0](thi |  [14.6 |   |                       |
|                       | | nkpyth | ](thin |   |                       |
|                       | | on2018 | kpytho |   |                       |
|                       | | .html# | n2015. |   |                       |
|                       | | hevea_ | html#h |   |                       |
|                       | | defaul | evea_d |   |                       |
|                       | | t1519) | efault |   |                       |
|                       | |        | 1264), |   |                       |
|                       | |   -    |        |   |                       |
|                       | | class, |   [14. |   |                       |
|                       | |        | 8](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |  [18.2 | on2015 |   |                       |
|                       | | ](thin | .html# |   |                       |
|                       | | kpytho | hevea_ |   |                       |
|                       | | n2019. | defaul |   |                       |
|                       | | html#h | t1281) |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault |   -    |   |                       |
|                       | | 1562), | count, |   |                       |
|                       | |        |        |   |                       |
|                       | |        |    [8. |   |                       |
|                       | |  [18.1 | 13](th |   |                       |
|                       | | 1](thi | inkpyt |   |                       |
|                       | | nkpyth | hon200 |   |                       |
|                       | | on2019 | 9.html |   |                       |
|                       | | .html# | #hevea |   |                       |
|                       | | hevea_ | _defau |   |                       |
|                       | | defaul | lt639) |   |                       |
|                       | | t1643) |        |   |                       |
|                       | |        |  -   e |   |                       |
|                       | |  -   i | xtend, |   |                       |
|                       | | nitial |        |   |                       |
|                       | | izing, |    [10 |   |                       |
|                       | |        | .6](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |  [17.1 | hon201 |   |                       |
|                       | | 0](thi | 1.html |   |                       |
|                       | | nkpyth | #hevea |   |                       |
|                       | | on2018 | _defau |   |                       |
|                       | | .html# | lt760) |   |                       |
|                       | | hevea_ |     -  |   |                       |
|                       | | defaul |   get, |   |                       |
|                       | | t1515) |        |   |                       |
|                       | |     -  |    [11 |   |                       |
|                       | |    ins | .2](th |   |                       |
|                       | | tance, | inkpyt |   |                       |
|                       | |        | hon201 |   |                       |
|                       | |        | 2.html |   |                       |
|                       | |  [15.2 | #hevea |   |                       |
|                       | | ](thin | _defau |   |                       |
|                       | | kpytho | lt914) |   |                       |
|                       | | n2016. |        |   |                       |
|                       | | html#h |    -   |   |                       |
|                       | | evea_d |  init, |   |                       |
|                       | | efault |        |   |                       |
|                       | | 1345), |        |   |                       |
|                       | |        |  [17.5 |   |                       |
|                       | |        | ](thin |   |                       |
|                       | |  [15.8 | kpytho |   |                       |
|                       | | ](thin | n2018. |   |                       |
|                       | | kpytho | html#h |   |                       |
|                       | | n2016. | evea_d |   |                       |
|                       | | html#h | efault |   |                       |
|                       | | evea_d | 1486), |   |                       |
|                       | | efault |        |   |                       |
|                       | | 1405), |        |   |                       |
|                       | |        |  [18.1 |   |                       |
|                       | |        | ](thin |   |                       |
|                       | |  [18.2 | kpytho |   |                       |
|                       | | ](thin | n2019. |   |                       |
|                       | | kpytho | html#h |   |                       |
|                       | | n2019. | evea_d |   |                       |
|                       | | html#h | efault |   |                       |
|                       | | evea_d | 1560), |   |                       |
|                       | | efault |        |   |                       |
|                       | | 1564), |        |   |                       |
|                       | |        |  [18.4 |   |                       |
|                       | |        | ](thin |   |                       |
|                       | |  [18.1 | kpytho |   |                       |
|                       | | 1](thi | n2019. |   |                       |
|                       | | nkpyth | html#h |   |                       |
|                       | | on2019 | evea_d |   |                       |
|                       | | .html# | efault |   |                       |
|                       | | hevea_ | 1583), |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t1645) |   [18. |   |                       |
|                       | | -      | 7](thi |   |                       |
|                       | |    aug | nkpyth |   |                       |
|                       | | mented | on2019 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |  assig | hevea_ |   |                       |
|                       | | nment, | defaul |   |                       |
|                       | |        | t1620) |   |                       |
|                       | |   [10. |        |   |                       |
|                       | | 7](thi |   -    |   |                       |
|                       | | nkpyth | items, |   |                       |
|                       | | on2011 |        |   |                       |
|                       | | .html# |   [12. |   |                       |
|                       | | hevea_ | 6](thi |   |                       |
|                       | | defaul | nkpyth |   |                       |
|                       | | t770), | on2013 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |   [10. | hevea_ |   |                       |
|                       | | 14](th | defaul |   |                       |
|                       | | inkpyt | t1081) |   |                       |
|                       | | hon201 |        |   |                       |
|                       | | 1.html |    -   |   |                       |
|                       | | #hevea |  join, |   |                       |
|                       | | _defau |        |   |                       |
|                       | | lt848) |   [10. |   |                       |
|                       | | -   a  | 9](thi |   |                       |
|                       | | verage | nkpyth |   |                       |
|                       | |        | on2011 |   |                       |
|                       | |  case, | .html# |   |                       |
|                       | |     [  | hevea_ |   |                       |
|                       | | B](thi | defaul |   |                       |
|                       | | nkpyth | t801), |   |                       |
|                       | | on2022 |        |   |                       |
|                       | | .html# |   [18. |   |                       |
|                       | | hevea_ | 5](thi |   |                       |
|                       | | defaul | nkpyth |   |                       |
|                       | | t1819) | on2019 |   |                       |
|                       | | -   a  | .html# |   |                       |
|                       | | verage | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | |  cost, | t1595) |   |                       |
|                       | |        |     -  |   |                       |
|                       | |   [B.4 |   mro, |   |                       |
|                       | | ](thin |        |   |                       |
|                       | | kpytho |   [18. |   |                       |
|                       | | n2022. | 9](thi |   |                       |
|                       | | html#h | nkpyth |   |                       |
|                       | | evea_d | on2019 |   |                       |
|                       | | efault | .html# |   |                       |
|                       | | 1858)\ | hevea_ |   |                       |
|                       | |     \  | defaul |   |                       |
|                       | | -   [  | t1631) |   |                       |
|                       | | Better |     -  |   |                       |
|                       | | Map]{. |   pop, |   |                       |
|                       | | c004}, |        |   |                       |
|                       | |        |   [10. |   |                       |
|                       | |    [B. | 8](thi |   |                       |
|                       | | 4](thi | nkpyth |   |                       |
|                       | | nkpyth | on2011 |   |                       |
|                       | | on2022 | .html# |   |                       |
|                       | | .html# | hevea_ |   |                       |
|                       | | hevea_ | defaul |   |                       |
|                       | | defaul | t783), |   |                       |
|                       | | t1852) |        |   |                       |
|                       | | -      |   [18. |   |                       |
|                       | | Big-Oh | 6](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |    not | on2019 |   |                       |
|                       | | ation, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |    [B. | defaul |   |                       |
|                       | | 5](thi | t1598) |   |                       |
|                       | | nkpyth |        |   |                       |
|                       | | on2022 |    -   |   |                       |
|                       | | .html# |  radd, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |   [17. |   |                       |
|                       | | t1866) | 8](thi |   |                       |
|                       | | -   ba | nkpyth |   |                       |
|                       | | dness, | on2018 |   |                       |
|                       | |        | .html# |   |                       |
|                       | |    [B. | hevea_ |   |                       |
|                       | | 1](thi | defaul |   |                       |
|                       | | nkpyth | t1509) |   |                       |
|                       | | on2022 |        |   |                       |
|                       | | .html# |    -   |   |                       |
|                       | | hevea_ |  read, |   |                       |
|                       | | defaul |        |   |                       |
|                       | | t1828) |   [14. |   |                       |
|                       | | -      | 8](thi |   |                       |
|                       | |   base | nkpyth |   |                       |
|                       | |        | on2015 |   |                       |
|                       | |  case, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |    [5. | defaul |   |                       |
|                       | | 9](thi | t1279) |   |                       |
|                       | | nkpyth |     -  |   |                       |
|                       | | on2006 |    rea |   |                       |
|                       | | .html# | dline, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |    [9. |   |                       |
|                       | | t371), | 1](thi |   |                       |
|                       | |        | nkpyth |   |                       |
|                       | |    [5. | on2010 |   |                       |
|                       | | 13](th | .html# |   |                       |
|                       | | inkpyt | hevea_ |   |                       |
|                       | | hon200 | defaul |   |                       |
|                       | | 6.html | t655), |   |                       |
|                       | | #hevea |        |   |                       |
|                       | | _defau |   [14. |   |                       |
|                       | | lt413) | 8](thi |   |                       |
|                       | | -   b  | nkpyth |   |                       |
|                       | | enchma | on2015 |   |                       |
|                       | | rking, | .html# |   |                       |
|                       | |        | hevea_ |   |                       |
|                       | |  [13.9 | defaul |   |                       |
|                       | | ](thin | t1277) |   |                       |
|                       | | kpytho |        |   |                       |
|                       | | n2014. |  -   r |   |                       |
|                       | | html#h | emove, |   |                       |
|                       | | evea_d |        |   |                       |
|                       | | efault |    [10 |   |                       |
|                       | | 1189), | .8](th |   |                       |
|                       | |        | inkpyt |   |                       |
|                       | |  [13.1 | hon201 |   |                       |
|                       | | 1](thi | 1.html |   |                       |
|                       | | nkpyth | #hevea |   |                       |
|                       | | on2014 | _defau |   |                       |
|                       | | .html# | lt787) |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul | -   re |   |                       |
|                       | | t1201) | place, |   |                       |
|                       | | -      |        |   |                       |
|                       | |   big, |   [13. |   |                       |
|                       | |        | 1](thi |   |                       |
|                       | |  hairy | nkpyth |   |                       |
|                       | |        | on2014 |   |                       |
|                       | |  expre | .html# |   |                       |
|                       | | ssion, | hevea_ |   |                       |
|                       | |        | defaul |   |                       |
|                       | |  [A.3. | t1140) |   |                       |
|                       | | 2](thi |        |   |                       |
|                       | | nkpyth |    -   |   |                       |
|                       | | on2021 |  setde |   |                       |
|                       | | .html# | fault, |   |                       |
|                       | | hevea_ |        |   |                       |
|                       | | defaul |   [11. |   |                       |
|                       | | t1795) | 10](th |   |                       |
|                       | | -      | inkpyt |   |                       |
|                       | | big-oh | hon201 |   |                       |
|                       | |        | 2.html |   |                       |
|                       | |    not | #hevea |   |                       |
|                       | | ation, | _defau |   |                       |
|                       | |        | lt996) |   |                       |
|                       | |    [B. |        |   |                       |
|                       | | 1](thi |    -   |   |                       |
|                       | | nkpyth |  sort, |   |                       |
|                       | | on2022 |        |   |                       |
|                       | | .html# |   [10. |   |                       |
|                       | | hevea_ | 6](thi |   |                       |
|                       | | defaul | nkpyth |   |                       |
|                       | | t1825) | on2011 |   |                       |
|                       | | -      | .html# |   |                       |
|                       | | binary | hevea_ |   |                       |
|                       | |     s  | defaul |   |                       |
|                       | | earch, | t762), |   |                       |
|                       | |        |        |   |                       |
|                       | |   [10. |        |   |                       |
|                       | | 15](th |  [10.1 |   |                       |
|                       | | inkpyt | 3](thi |   |                       |
|                       | | hon201 | nkpyth |   |                       |
|                       | | 1.html | on2011 |   |                       |
|                       | | #hevea | .html# |   |                       |
|                       | | _defau | hevea_ |   |                       |
|                       | | lt881) | defaul |   |                       |
|                       | | -      | t838), |   |                       |
|                       | | bingo, |        |   |                       |
|                       | |        |   [18. |   |                       |
|                       | |  [12.1 | 6](thi |   |                       |
|                       | | 0](thi | nkpyth |   |                       |
|                       | | nkpyth | on2019 |   |                       |
|                       | | on2013 | .html# |   |                       |
|                       | | .html# | hevea_ |   |                       |
|                       | | hevea_ | defaul |   |                       |
|              