    duck.             |                       |
|                       |     Articulating the  |                       |
|                       |     problem can help  |                       |
|                       |     you solve it,     |                       |
|                       |     even if the       |                       |
|                       |     rubber duck       |                       |
|                       |     doesn't know      |                       |
|                       |     Python.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1202} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1203} |                       |
|                       |                       |                       |
|                       | ## 13.12  Exercis     |                       |
|                       | es {#sec163 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 9]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1204} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1205} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1206} |                       |
|                       |                       |                       |
|                       | *The "rank" of a word |                       |
|                       | is its position in a  |                       |
|                       | list of words sorted  |                       |
|                       | by frequency: the     |                       |
|                       | most common word has  |                       |
|                       | rank 1, the second    |                       |
|                       | most common has rank  |                       |
|                       | 2, etc.*              |                       |
|                       |                       |                       |
|                       | *Zipf's law describes |                       |
|                       | a relationship        |                       |
|                       | between the ranks and |                       |
|                       | frequencies of words  |                       |
|                       | in natural languages  |                       |
|                       | (*[*[http://en.       |                       |
|                       | wikipedia.org/wiki/Zi |                       |
|                       | pf\'s_law]{.c004}*](h |                       |
|                       | ttp://en.wikipedia.or |                       |
|                       | g/wiki/Zipf's_law)*). |                       |
|                       | Specifically, it      |                       |
|                       | predicts that the     |                       |
|                       | frequency,*           |                       |
|                       | [f]{.c009}*, of the   |                       |
|                       | word with rank*       |                       |
|                       | [r]{.c009} *is:*      |                       |
|                       |                       |                       |
|                       |   --------            |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       |   [f]{.c              |                       |
|                       | 009} = [c]{.c009} [r] |                       |
|                       | {.c009}^−[s]{.c009}^  |                       |
|                       |   --------            |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       |                       |                       |
|                       | *where* [s]{.c009}    |                       |
|                       | *and* [c]{.c009} *are |                       |
|                       | parameters that       |                       |
|                       | depend on the         |                       |
|                       | language and the      |                       |
|                       | text. If you take the |                       |
|                       | logarithm of both     |                       |
|                       | sides of this         |                       |
|                       | equation, you get:*   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1207} |                       |
|                       |                       |                       |
|                       |   -----------------   |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       |   log[f]{.c009} =     |                       |
|                       |  log[c]{.c009} − [s]{ |                       |
|                       | .c009} log[r]{.c009}  |                       |
|                       |   -----------------   |                       |
|                       | --------------------- |                       |
|                       | --------------------- |                       |
|                       |                       |                       |
|                       | *So if you plot log*  |                       |
|                       | [f]{.c009} *versus    |                       |
|                       | log* [r]{.c009}*, you |                       |
|                       | should get a straight |                       |
|                       | line with slope*      |                       |
|                       | −[s]{.c009} *and      |                       |
|                       | intercept log*        |                       |
|                       | [c]{.c009}*.*         |                       |
|                       |                       |                       |
|                       | *Write a program that |                       |
|                       | reads a text from a   |                       |
|                       | file, counts word     |                       |
|                       | frequencies, and      |                       |
|                       | prints one line for   |                       |
|                       | each word, in         |                       |
|                       | descending order of   |                       |
|                       | frequency, with log*  |                       |
|                       | [f]{.c009} *and log*  |                       |
|                       | [r]{.c009}*. Use the  |                       |
|                       | graphing program of   |                       |
|                       | your choice to plot   |                       |
|                       | the results and check |                       |
|                       | whether they form a   |                       |
|                       | straight line. Can    |                       |
|                       | you estimate the      |                       |
|                       | value of*             |                       |
|                       | [s]{.c009}*?*         |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [[*ht                 |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/zipf.py*]{.c004 |                       |
|                       | }](https://thinkpytho |                       |
|                       | n.com/code/zipf.py)*. |                       |
|                       | To run my solution,   |                       |
|                       | you need the plotting |                       |
|                       | module                |                       |
|                       | [matplotlib]{.c004}.  |                       |
|                       | If you installed      |                       |
|                       | Anaconda, you already |                       |
|                       | have                  |                       |
|                       | [matplotlib]{.c004};  |                       |
|                       | otherwise you might   |                       |
|                       | have to install it.*  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1208} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2013.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2015.html)
---
generator: hevea 2.32
title: Files
---

[![Previous](back.png)](thinkpython2014.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2016.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 14  Fil     | to support my books,  |
|                       | es {#sec164 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | This chapter          | with PayPal. Thank    |
|                       | introduces the idea   | you!                  |
|                       | of "persistent"       |                       |
|                       | programs that keep    |   -----------         |
|                       | data in permanent     | --------------------- |
|                       | storage, and shows    | --------------------- |
|                       | how to use different  | --------------------- |
|                       | kinds of permanent    | --------------------- |
|                       | storage, like files   |   Pay what you want:  |
|                       | and databases.        |   Small \$1           |
|                       |                       | .00 USD Medium \$5.00 |
|                       | ## 14.1  Persisten    |  USD Large \$10.00 US |
|                       | ce {#sec165 .section} | D X-Large \$20.00 USD |
|                       |                       |  XX-Large \$50.00 USD |
|                       | [                     |   -----------         |
|                       | ]{#hevea_default1209} | --------------------- |
|                       | [                     | --------------------- |
|                       | ]{#hevea_default1210} | --------------------- |
|                       | [                     | --------------------- |
|                       | ]{#hevea_default1211} |                       |
|                       |                       | ![](                  |
|                       | Most of the programs  | https://www.paypalobj |
|                       | we have seen so far   | ects.com/en_US/i/scr/ |
|                       | are transient in the  | pixel.gif){border="0" |
|                       | sense that they run   | width="1" height="1"} |
|                       | for a short time and  |                       |
|                       | produce some output,  | ####                  |
|                       | but when they end,    | Are you using one of  |
|                       | their data            | our books in a class? |
|                       | disappears. If you    |                       |
|                       | run the program       | We\'d like to know    |
|                       | again, it starts with | about it. Please      |
|                       | a clean slate.        | consider filling out  |
|                       |                       | [this short           |
|                       | Other programs are    | survey](http://s      |
|                       | [persistent]{.c010}:  | preadsheets.google.co |
|                       | they run for a long   | m/viewform?formkey=dC |
|                       | time (or all the      | 0tNUZkMjBEdXVoRGljNm9 |
|                       | time); they keep at   | FRmlTMHc6MA){onclick= |
|                       | least some of their   | "javascript: pageTrac |
|                       | data in permanent     | ker._trackPageview('/ |
|                       | storage (a hard       | outbound/survey');"}. |
|                       | drive, for example);  |                       |
|                       | and if they shut down | \                     |
|                       | and restart, they     |                       |
|                       | pick up where they    | [Think                |
|                       | left off.             | DSP](http             |
|                       |                       | ://www.amazon.com/gp/ |
|                       | Examples of           | product/1491938455/re |
|                       | persistent programs   | f=as_li_tl?ie=UTF8&ca |
|                       | are operating         | mp=1789&creative=9325 |
|                       | systems, which run    | &creativeASIN=1491938 |
|                       | pretty much whenever  | 455&linkCode=as2&tag= |
|                       | a computer is on, and | greenteapre01-20&link |
|                       | web servers, which    | Id=2JJH4SWCAVVYSQHO){ |
|                       | run all the time,     | rel="nofollow"}![](ht |
|                       | waiting for requests  | tp://ir-na.amazon-ads |
|                       | to come in on the     | ystem.com/e/ir?t=gree |
|                       | network.              | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491938455){.c003 |
|                       | One of the simplest   | width="1" height="1"  |
|                       | ways for programs to  | border="0"}           |
|                       | maintain their data   |                       |
|                       | is by reading and     | [                     |
|                       | writing text files.   | ![](http://ws-na.amaz |
|                       | We have already seen  | on-adsystem.com/widge |
|                       | programs that read    | ts/q?_encoding=UTF8&A |
|                       | text files; in this   | SIN=1491938455&Format |
|                       | chapter we will see   | =_SL160_&ID=AsinImage |
|                       | programs that write   | &MarketPlace=US&Servi |
|                       | them.                 | ceVersion=20070822&WS |
|                       |                       | =1&tag=greenteapre01- |
|                       | An alternative is to  | 20){border="0"}](http |
|                       | store the state of    | ://www.amazon.com/gp/ |
|                       | the program in a      | product/1491938455/re |
|                       | database. In this     | f=as_li_tl?ie=UTF8&ca |
|                       | chapter I will        | mp=1789&creative=9325 |
|                       | present a simple      | &creativeASIN=1491938 |
|                       | database and a        | 455&linkCode=as2&tag= |
|                       | module,               | greenteapre01-20&link |
|                       | [pickle]{.c004}, that | Id=CTV7PDT7E5EGGJUM){ |
|                       | makes it easy to      | rel="nofollow"}![](ht |
|                       | store program data.   | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1212} | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491938455){.c003 |
|                       | ]{#hevea_default1213} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | ## 14                 |                       |
|                       | .2  Reading and writi | [Think                |
|                       | ng {#sec166 .section} | Java](http            |
|                       |                       | ://www.amazon.com/gp/ |
|                       | [                     | product/1491929561/re |
|                       | ]{#hevea_default1214} | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | A text file is a      | &creativeASIN=1491929 |
|                       | sequence of           | 561&linkCode=as2&tag= |
|                       | characters stored on  | greenteapre01-20&link |
|                       | a permanent medium    | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | like a hard drive,    | rel="nofollow"}![](ht |
|                       | flash memory, or      | tp://ir-na.amazon-ads |
|                       | CD-ROM. We saw how to | ystem.com/e/ir?t=gree |
|                       | open and read a file  | nteapre01-20&l=as2&o= |
|                       | in                    | 1&a=1491929561){.c003 |
|                       | Sec                   | width="1" height="1"  |
|                       | tion [9.1](thinkpytho | border="0"}           |
|                       | n2010.html#wordlist). |                       |
|                       | [                     | [                     |
|                       | ]{#hevea_default1215} | ![](http://ws-na.amaz |
|                       | [                     | on-adsystem.com/widge |
|                       | ]{#hevea_default1216} | ts/q?_encoding=UTF8&A |
|                       |                       | SIN=1491929561&Format |
|                       | To write a file, you  | =_SL160_&ID=AsinImage |
|                       | have to open it with  | &MarketPlace=US&Servi |
|                       | mode `'w'` as a       | ceVersion=20070822&WS |
|                       | second parameter:     | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | ``` verbatim          | ://www.amazon.com/gp/ |
|                       | >>> fout = op         | product/1491929561/re |
|                       | en('output.txt', 'w') | f=as_li_tl?ie=UTF8&ca |
|                       | ```                   | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491929 |
|                       | If the file already   | 561&linkCode=as2&tag= |
|                       | exists, opening it in | greenteapre01-20&link |
|                       | write mode clears out | Id=PT77ANWARUNNU3UK){ |
|                       | the old data and      | rel="nofollow"}![](ht |
|                       | starts fresh, so be   | tp://ir-na.amazon-ads |
|                       | careful! If the file  | ystem.com/e/ir?t=gree |
|                       | doesn't exist, a new  | nteapre01-20&l=as2&o= |
|                       | one is created.       | 1&a=1491929561){.c003 |
|                       |                       | width="1" height="1"  |
|                       | [open]{.c004} returns | border="0"}           |
|                       | a file object that    |                       |
|                       | provides methods for  | [Think                |
|                       | working with the      | Bay                   |
|                       | file. The             | es](http://www.amazon |
|                       | [write]{.c004} method | .com/gp/product/14493 |
|                       | puts data into the    | 70780/ref=as_li_qf_sp |
|                       | file.                 | _asin_tl?ie=UTF8&camp |
|                       |                       | =1789&creative=9325&c |
|                       | ``` verbatim          | reativeASIN=144937078 |
|                       | >>> line1 = "This     | 0&linkCode=as2&tag=gr |
|                       | here's the wattle,\n" | eenteapre01-20)![](ht |
|                       | >>> fout.write(line1) | tp://ir-na.amazon-ads |
|                       | 24                    | ystem.com/e/ir?t=gree |
|                       | ```                   | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1449370780){.c003 |
|                       | The return value is   | width="1" height="1"  |
|                       | the number of         | border="0"}           |
|                       | characters that were  |                       |
|                       | written. The file     | [![](http://ws        |
|                       | object keeps track of | -na.amazon-adsystem.c |
|                       | where it is, so if    | om/widgets/q?_encodin |
|                       | you call              | g=UTF8&ASIN=144937078 |
|                       | [write]{.c004} again, | 0&Format=_SL160_&ID=A |
|                       | it adds the new data  | sinImage&MarketPlace= |
|                       | to the end of the     | US&ServiceVersion=200 |
|                       | file.                 | 70822&WS=1&tag=greent |
|                       |                       | eapre01-20){border="0 |
|                       | ``` verbatim          | "}](http://www.amazon |
|                       | >>> line2 = "the e    | .com/gp/product/14493 |
|                       | mblem of our land.\n" | 70780/ref=as_li_qf_sp |
|                       | >>> fout.write(line2) | _asin_il?ie=UTF8&camp |
|                       | 24                    | =1789&creative=9325&c |
|                       | ```                   | reativeASIN=144937078 |
|                       |                       | 0&linkCode=as2&tag=gr |
|                       | When you are done     | eenteapre01-20)![](ht |
|                       | writing, you should   | tp://ir-na.amazon-ads |
|                       | close the file.       | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1449370780){.c003 |
|                       | >>> fout.close()      | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | [                     | [Think Python         |
|                       | ]{#hevea_default1217} | 2e](http              |
|                       | [                     | ://www.amazon.com/gp/ |
|                       | ]{#hevea_default1218} | product/1491939362/re |
|                       | If you don't close    | f=as_li_tl?ie=UTF8&ca |
|                       | the file, it gets     | mp=1789&creative=9325 |
|                       | closed for you when   | &creativeASIN=1491939 |
|                       | the program ends.     | 362&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | #                     | Id=FJKSQ3IHEMY2F2VA){ |
|                       | # 14.3  Format operat | rel="nofollow"}![](ht |
|                       | or {#sec167 .section} | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | [                     | nteapre01-20&l=as2&o= |
|                       | ]{#hevea_default1219} | 1&a=1491939362){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1220} | border="0"}           |
|                       |                       |                       |
|                       | The argument of       | [                     |
|                       | [write]{.c004} has to | ![](http://ws-na.amaz |
|                       | be a string, so if we | on-adsystem.com/widge |
|                       | want to put other     | ts/q?_encoding=UTF8&A |
|                       | values in a file, we  | SIN=1491939362&Format |
|                       | have to convert them  | =_SL160_&ID=AsinImage |
|                       | to strings. The       | &MarketPlace=US&Servi |
|                       | easiest way to do     | ceVersion=20070822&WS |
|                       | that is with          | =1&tag=greenteapre01- |
|                       | [str]{.c004}:         | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | ``` verbatim          | product/1491939362/re |
|                       | >>> x = 52            | f=as_li_tl?ie=UTF8&ca |
|                       | >                     | mp=1789&creative=9325 |
|                       | >> fout.write(str(x)) | &creativeASIN=1491939 |
|                       | ```                   | 362&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | An alternative is to  | Id=ZZ454DLQ3IXDHNHX){ |
|                       | use the [format       | rel="nofollow"}![](ht |
|                       | operator]{.c010},     | tp://ir-na.amazon-ads |
|                       | [%]{.c004}. When      | ystem.com/e/ir?t=gree |
|                       | applied to integers,  | nteapre01-20&l=as2&o= |
|                       | [%]{.c004} is the     | 1&a=1491939362){.c003 |
|                       | modulus operator. But | width="1" height="1"  |
|                       | when the first        | border="0"}           |
|                       | operand is a string,  |                       |
|                       | [%]{.c004} is the     | [Think Stats          |
|                       | format operator.      | 2e](http://ww         |
|                       | [                     | w.amazon.com/gp/produ |
|                       | ]{#hevea_default1221} | ct/1491907339/ref=as_ |
|                       |                       | li_tl?ie=UTF8&camp=17 |
|                       | The first operand is  | 89&creative=9325&crea |
|                       | the [format           | tiveASIN=1491907339&l |
|                       | string]{.c010}, which | inkCode=as2&tag=green |
|                       | contains one or more  | teapre01-20&linkId=O7 |
|                       | [format               | WYM6H6YBYUFNWU)![](ht |
|                       | sequences]{.c010},    | tp://ir-na.amazon-ads |
|                       | which specify how the | ystem.com/e/ir?t=gree |
|                       | second operand is     | nteapre01-20&l=as2&o= |
|                       | formatted. The result | 1&a=1491907339){.c003 |
|                       | is a string.          | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1222} |                       |
|                       |                       | [![](h                |
|                       | For example, the      | ttp://ws-na.amazon-ad |
|                       | format sequence       | system.com/widgets/q? |
|                       | `'%d'` means that the | _encoding=UTF8&ASIN=1 |
|                       | second operand should | 491907339&Format=_SL1 |
|                       | be formatted as a     | 60_&ID=AsinImage&Mark |
|                       | decimal integer:      | etPlace=US&ServiceVer |
|                       |                       | sion=20070822&WS=1&ta |
|                       | ``` verbatim          | g=greenteapre01-20){b |
|                       | >>> camels = 42       | order="0"}](http://ww |
|                       | >>> '%d' % camels     | w.amazon.com/gp/produ |
|                       | '42'                  | ct/1491907339/ref=as_ |
|                       | ```                   | li_tl?ie=UTF8&camp=17 |
|                       |                       | 89&creative=9325&crea |
|                       | The result is the     | tiveASIN=1491907339&l |
|                       | string `'42'`, which  | inkCode=as2&tag=green |
|                       | is not to be confused | teapre01-20&linkId=JV |
|                       | with the integer      | SYKQHYSUIEYRHL)![](ht |
|                       | value [42]{.c004}.    | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | A format sequence can | nteapre01-20&l=as2&o= |
|                       | appear anywhere in    | 1&a=1491907339){.c003 |
|                       | the string, so you    | width="1" height="1"  |
|                       | can embed a value in  | border="0"}           |
|                       | a sentence:           |                       |
|                       |                       | [Think                |
|                       | ``` verbatim          | Complexity](http      |
|                       | >>> 'I have spotted   | ://www.amazon.com/gp/ |
|                       |  %d camels.' % camels | product/1449314635/re |
|                       | 'I hav                | f=as_li_tf_tl?ie=UTF8 |
|                       | e spotted 42 camels.' | &tag=greenteapre01-20 |
|                       | ```                   | &linkCode=as2&camp=17 |
|                       |                       | 89&creative=9325&crea |
|                       | If there is more than | tiveASIN=1449314635)! |
|                       | one format sequence   | [](http://www.assoc-a |
|                       | in the string, the    | mazon.com/e/ir?t=gree |
|                       | second argument has   | nteapre01-20&l=as2&o= |
|                       | to be a tuple. Each   | 1&a=1449314635){.c003 |
|                       | format sequence is    | width="1" height="1"  |
|                       | matched with an       | border="0"}           |
|                       | element of the tuple, |                       |
|                       | in order.             | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | The following example | on-adsystem.com/widge |
|                       | uses `'%d'` to format | ts/q?_encoding=UTF8&A |
|                       | an integer, `'%g'` to | SIN=1449314635&Format |
|                       | format a              | =_SL160_&ID=AsinImage |
|                       | floating-point        | &MarketPlace=US&Servi |
|                       | number, and `'%s'` to | ceVersion=20070822&WS |
|                       | format a string:      | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | ``` verbatim          | ://www.amazon.com/gp/ |
|                       | >>> 'In %d years I    | product/1449314635/re |
|                       |  have spotted %g %s.' | f=as_li_tf_il?ie=UTF8 |
|                       |  % (3, 0.1, 'camels') | &camp=1789&creative=9 |
|                       | 'In 3 years I have    | 325&creativeASIN=1449 |
|                       |  spotted 0.1 camels.' | 314635&linkCode=as2&t |
|                       | ```                   | ag=greenteapre01-20)! |
|                       |                       | [](http://www.assoc-a |
|                       | The number of         | mazon.com/e/ir?t=gree |
|                       | elements in the tuple | nteapre01-20&l=as2&o= |
|                       | has to match the      | 1&a=1449314635){.c003 |
|                       | number of format      | width="1" height="1"  |
|                       | sequences in the      | border="0"}           |
|                       | string. Also, the     |                       |
|                       | types of the elements |                       |
|                       | have to match the     |                       |
|                       | format sequences:     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1223} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1224} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > '%d %d %d' % (1, 2) |                       |
|                       | TypeErr               |                       |
|                       | or: not enough argume |                       |
|                       | nts for format string |                       |
|                       | >>> '%d' % 'dollars'  |                       |
|                       | TypeError             |                       |
|                       | : %d format: a number |                       |
|                       |  is required, not str |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In the first example, |                       |
|                       | there aren't enough   |                       |
|                       | elements; in the      |                       |
|                       | second, the element   |                       |
|                       | is the wrong type.    |                       |
|                       |                       |                       |
|                       | For more information  |                       |
|                       | on the format         |                       |
|                       | operator, see         |                       |
|                       | [[                    |                       |
|                       | https://docs.python.o |                       |
|                       | rg/3/library/stdtypes |                       |
|                       | .html#printf-style-st |                       |
|                       | ring-formatting]{.c00 |                       |
|                       | 4}](https://docs.pyth |                       |
|                       | on.org/3/library/stdt |                       |
|                       | ypes.html#printf-styl |                       |
|                       | e-string-formatting). |                       |
|                       | A more powerful       |                       |
|                       | alternative is the    |                       |
|                       | string format method, |                       |
|                       | which you can read    |                       |
|                       | about at              |                       |
|                       | [[ht                  |                       |
|                       | tps://docs.python.org |                       |
|                       | /3/library/stdtypes.h |                       |
|                       | tml#str.format]{.c004 |                       |
|                       | }](https://docs.pytho |                       |
|                       | n.org/3/library/stdty |                       |
|                       | pes.html#str.format). |                       |
|                       |                       |                       |
|                       | ## 14                 |                       |
|                       | .4  Filenames and pat |                       |
|                       | hs {#sec168 .section} |                       |
|                       |                       |                       |
|                       | []{#paths}            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1225} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1226} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1227} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1228} |                       |
|                       |                       |                       |
|                       | Files are organized   |                       |
|                       | into                  |                       |
|                       | [directories]{.c010}  |                       |
|                       | (also called          |                       |
|                       | "folders"). Every     |                       |
|                       | running program has a |                       |
|                       | "current directory",  |                       |
|                       | which is the default  |                       |
|                       | directory for most    |                       |
|                       | operations. For       |                       |
|                       | example, when you     |                       |
|                       | open a file for       |                       |
|                       | reading, Python looks |                       |
|                       | for it in the current |                       |
|                       | directory.            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1229} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1230} |                       |
|                       |                       |                       |
|                       | The [os]{.c004}       |                       |
|                       | module provides       |                       |
|                       | functions for working |                       |
|                       | with files and        |                       |
|                       | directories ("os"     |                       |
|                       | stands for "operating |                       |
|                       | system").             |                       |
|                       | [os.getcwd]{.c004}    |                       |
|                       | returns the name of   |                       |
|                       | the current           |                       |
|                       | directory:            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1231} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1232} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> import os         |                       |
|                       | >>> cwd = os.getcwd() |                       |
|                       | >>> cwd               |                       |
|                       | '/home/dinsdale'      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [cwd]{.c004} stands   |                       |
|                       | for "current working  |                       |
|                       | directory". The       |                       |
|                       | result in this        |                       |
|                       | example is            |                       |
|                       | [/h                   |                       |
|                       | ome/dinsdale]{.c004}, |                       |
|                       | which is the home     |                       |
|                       | directory of a user   |                       |
|                       | named                 |                       |
|                       | [dinsdale]{.c004}.    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1233} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1234} |                       |
|                       |                       |                       |
|                       | A string like         |                       |
|                       | `'/home/dinsdale'`    |                       |
|                       | that identifies a     |                       |
|                       | file or directory is  |                       |
|                       | called a              |                       |
|                       | [path]{.c010}.        |                       |
|                       |                       |                       |
|                       | A simple filename,    |                       |
|                       | like                  |                       |
|                       | [memo.txt]{.c004} is  |                       |
|                       | also considered a     |                       |
|                       | path, but it is a     |                       |
|                       | [relative             |                       |
|                       | path]{.c010} because  |                       |
|                       | it relates to the     |                       |
|                       | current directory. If |                       |
|                       | the current directory |                       |
|                       | is                    |                       |
|                       | [/h                   |                       |
|                       | ome/dinsdale]{.c004}, |                       |
|                       | the filename          |                       |
|                       | [memo.txt]{.c004}     |                       |
|                       | would refer to        |                       |
|                       | [/home/dinsd          |                       |
|                       | ale/memo.txt]{.c004}. |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1235} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1236} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1237} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1238} |                       |
|                       |                       |                       |
|                       | A path that begins    |                       |
|                       | with [/]{.c004} does  |                       |
|                       | not depend on the     |                       |
|                       | current directory; it |                       |
|                       | is called an          |                       |
|                       | [absolute             |                       |
|                       | path]{.c010}. To find |                       |
|                       | the absolute path to  |                       |
|                       | a file, you can use   |                       |
|                       | [os.                  |                       |
|                       | path.abspath]{.c004}: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> os.pat            |                       |
|                       | h.abspath('memo.txt') |                       |
|                       | '/ho                  |                       |
|                       | me/dinsdale/memo.txt' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [os.path]{.c004}      |                       |
|                       | provides other        |                       |
|                       | functions for working |                       |
|                       | with filenames and    |                       |
|                       | paths. For example,   |                       |
|                       | [o                    |                       |
|                       | s.path.exists]{.c004} |                       |
|                       | checks whether a file |                       |
|                       | or directory exists:  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1239} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1240} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> os.pa             |                       |
|                       | th.exists('memo.txt') |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If it exists,         |                       |
|                       | [                     |                       |
|                       | os.path.isdir]{.c004} |                       |
|                       | checks whether it's a |                       |
|                       | directory:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> os.p              |                       |
|                       | ath.isdir('memo.txt') |                       |
|                       | False                 |                       |
|                       | >>> os.path.is        |                       |
|                       | dir('/home/dinsdale') |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Similarly,            |                       |
|                       | [o                    |                       |
|                       | s.path.isfile]{.c004} |                       |
|                       | checks whether it's a |                       |
|                       | file.                 |                       |
|                       |                       |                       |
|                       | [os.listdir]{.c004}   |                       |
|                       | returns a list of the |                       |
|                       | files (and other      |                       |
|                       | directories) in the   |                       |
|                       | given directory:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> os.listdir(cwd)   |                       |
|                       | ['music',             |                       |
|                       | 'photos', 'memo.txt'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | To demonstrate these  |                       |
|                       | functions, the        |                       |
|                       | following example     |                       |
|                       | "walks" through a     |                       |
|                       | directory, prints the |                       |
|                       | names of all the      |                       |
|                       | files, and calls      |                       |
|                       | itself recursively on |                       |
|                       | all the directories.  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1241} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1242} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def walk(dirname):    |                       |
|                       |     for name in       |                       |
|                       |  os.listdir(dirname): |                       |
|                       |         path = os.pat |                       |
|                       | h.join(dirname, name) |                       |
|                       |                       |                       |
|                       |         if            |                       |
|                       | os.path.isfile(path): |                       |
|                       |                       |                       |
|                       |           print(path) |                       |
|                       |         else:         |                       |
|                       |                       |                       |
|                       |            walk(path) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [os.path.join]{.c004} |                       |
|                       | takes a directory and |                       |
|                       | a file name and joins |                       |
|                       | them into a complete  |                       |
|                       | path.                 |                       |
|                       |                       |                       |
|                       | The [os]{.c004}       |                       |
|                       | module provides a     |                       |
|                       | function called       |                       |
|                       | [walk]{.c004} that is |                       |
|                       | similar to this one   |                       |
|                       | but more versatile.   |                       |
|                       | As an exercise, read  |                       |
|                       | the documentation and |                       |
|                       | use it to print the   |                       |
|                       | names of the files in |                       |
|                       | a given directory and |                       |
|                       | its subdirectories.   |                       |
|                       | You can download my   |                       |
|                       | solution from         |                       |
|                       | [[                    |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/walk.py]{.c00 |                       |
|                       | 4}](https://thinkpyth |                       |
|                       | on.com/code/walk.py). |                       |
|                       |                       |                       |
|                       | ## 14                 |                       |
|                       | .5  Catching exceptio |                       |
|                       | ns {#sec169 .section} |                       |
|                       |                       |                       |
|                       | []{#catch}            |                       |
|                       |                       |                       |
|                       | A lot of things can   |                       |
|                       | go wrong when you try |                       |
|                       | to read and write     |                       |
|                       | files. If you try to  |                       |
|                       | open a file that      |                       |
|                       | doesn't exist, you    |                       |
|                       | get an                |                       |
|                       | [FileN                |                       |
|                       | otFoundError]{.c004}: |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1243} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1244} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1245} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1246} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> f                 |                       |
|                       | in = open('bad_file') |                       |
|                       | Fil                   |                       |
|                       | eNotFoundError: [Errn |                       |
|                       | o 2] No such file or  |                       |
|                       | directory: 'bad_file' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you don't have     |                       |
|                       | permission to access  |                       |
|                       | a file:               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1247} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1248} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> fout = ope        |                       |
|                       | n('/etc/passwd', 'w') |                       |
|                       | PermissionError: [    |                       |
|                       | Errno 13] Permission  |                       |
|                       | denied: '/etc/passwd' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And if you try to     |                       |
|                       | open a directory for  |                       |
|                       | reading, you get      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > fin = open('/home') |                       |
|                       | IsADirector           |                       |
|                       | yError: [Errno 21] Is |                       |
|                       |  a directory: '/home' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | To avoid these        |                       |
|                       | errors, you could use |                       |
|                       | functions like        |                       |
|                       | [o                    |                       |
|                       | s.path.exists]{.c004} |                       |
|                       | and                   |                       |
|                       | [os                   |                       |
|                       | .path.isfile]{.c004}, |                       |
|                       | but it would take a   |                       |
|                       | lot of time and code  |                       |
|                       | to check all the      |                       |
|                       | possibilities (if     |                       |
|                       | "[Errno 21]{.c004}"   |                       |
|                       | is any indication,    |                       |
|                       | there are at least 21 |                       |
|                       | things that can go    |                       |
|                       | wrong).               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1249} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1250} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1251} |                       |
|                       |                       |                       |
|                       | It is better to go    |                       |
|                       | ahead and try---and   |                       |
|                       | deal with problems if |                       |
|                       | they happen---which   |                       |
|                       | is exactly what the   |                       |
|                       | [try]{.c004}          |                       |
|                       | statement does. The   |                       |
|                       | syntax is similar to  |                       |
|                       | an                    |                       |
|                       | [if\...else]{.c004}   |                       |
|                       | statement:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | try:                  |                       |
|                       |     f                 |                       |
|                       | in = open('bad_file') |                       |
|                       | except:               |                       |
|                       |     print('So         |                       |
|                       | mething went wrong.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Python starts by      |                       |
|                       | executing the         |                       |
|                       | [try]{.c004} clause.  |                       |
|                       | If all goes well, it  |                       |
|                       | skips the             |                       |
|                       | [except]{.c004}       |                       |
|                       | clause and proceeds.  |                       |
|                       | If an exception       |                       |
|                       | occurs, it jumps out  |                       |
|                       | of the [try]{.c004}   |                       |
|                       | clause and runs the   |                       |
|                       | [except]{.c004}       |                       |
|                       | clause.               |                       |
|                       |                       |                       |
|                       | Handling an exception |                       |
|                       | with a [try]{.c004}   |                       |
|                       | statement is called   |                       |
|                       | [catching]{.c010} an  |                       |
|                       | exception. In this    |                       |
|                       | example, the          |                       |
|                       | [except]{.c004}       |                       |
|                       | clause prints an      |                       |
|                       | error message that is |                       |
|                       | not very helpful. In  |                       |
|                       | general, catching an  |                       |
|                       | exception gives you a |                       |
|                       | chance to fix the     |                       |
|                       | problem, or try       |                       |
|                       | again, or at least    |                       |
|                       | end the program       |                       |
|                       | gracefully.           |                       |
|                       |                       |                       |
|                       | ## 14.6  Databas      |                       |
|                       | es {#sec170 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1252} |                       |
|                       |                       |                       |
|                       | A [database]{.c010}   |                       |
|                       | is a file that is     |                       |
|                       | organized for storing |                       |
|                       | data. Many databases  |                       |
|                       | are organized like a  |                       |
|                       | dictionary in the     |                       |
|                       | sense that they map   |                       |
|                       | from keys to values.  |                       |
|                       | The biggest           |                       |
|                       | difference between a  |                       |
|                       | database and a        |                       |
|                       | dictionary is that    |                       |
|                       | the database is on    |                       |
|                       | disk (or other        |                       |
|                       | permanent storage),   |                       |
|                       | so it persists after  |                       |
|                       | the program ends.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1253} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1254} |                       |
|                       |                       |                       |
|                       | The module            |                       |
|                       | [dbm]{.c004} provides |                       |
|                       | an interface for      |                       |
|                       | creating and updating |                       |
|                       | database files. As an |                       |
|                       | example, I'll create  |                       |
|                       | a database that       |                       |
|                       | contains captions for |                       |
|                       | image files.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1255} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1256} |                       |
|                       |                       |                       |
|                       | Opening a database is |                       |
|                       | similar to opening    |                       |
|                       | other files:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> import dbm        |                       |
|                       | >>> db = dbm.         |                       |
|                       | open('captions', 'c') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The mode `'c'` means  |                       |
|                       | that the database     |                       |
|                       | should be created if  |                       |
|                       | it doesn't already    |                       |
|                       | exist. The result is  |                       |
|                       | a database object     |                       |
|                       | that can be used (for |                       |
|                       | most operations) like |                       |
|                       | a dictionary.         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1257} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1258} |                       |
|                       |                       |                       |
|                       | When you create a new |                       |
|                       | item, [dbm]{.c004}    |                       |
|                       | updates the database  |                       |
|                       | file.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1259} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | db['cleese.png'] = 'P |                       |
|                       | hoto of John Cleese.' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | When you access one   |                       |
|                       | of the items,         |                       |
|                       | [dbm]{.c004} reads    |                       |
|                       | the file:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> db['cleese.png']  |                       |
|                       | b'P                   |                       |
|                       | hoto of John Cleese.' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result is a       |                       |
|                       | [bytes                |                       |
|                       | object]{.c010}, which |                       |
|                       | is why it begins with |                       |
|                       | [b]{.c004}. A bytes   |                       |
|                       | object is similar to  |                       |
|                       | a string in many      |                       |
|                       | ways. When you get    |                       |
|                       | farther into Python,  |                       |
|                       | the difference        |                       |
|                       | becomes important,    |                       |
|                       | but for now we can    |                       |
|                       | ignore it.            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1260} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1261} |                       |
|                       |                       |                       |
|                       | If you make another   |                       |
|                       | assignment to an      |                       |
|                       | existing key,         |                       |
|                       | [dbm]{.c004} replaces |                       |
|                       | the old value:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > db['cleese.png'] =  |                       |
|                       | 'Photo of John Cleese |                       |
|                       |  doing a silly walk.' |                       |
|                       | >>> db['cleese.png']  |                       |
|                       | b                     |                       |
|                       | 'Photo of John Cleese |                       |
|                       |  doing a silly walk.' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Some dictionary       |                       |
|                       | methods, like         |                       |
|                       | [keys]{.c004} and     |                       |
|                       | [items]{.c004}, don't |                       |
|                       | work with database    |                       |
|                       | objects. But          |                       |
|                       | iteration with a      |                       |
|                       | [for]{.c004} loop     |                       |
|                       | works:                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1262} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | for key in db.keys(): |                       |
|                       |                       |                       |
|                       |   print(key, db[key]) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As with other files,  |                       |
|                       | you should close the  |                       |
|                       | database when you are |                       |
|                       | done:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> db.close()        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1263} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1264} |                       |
|                       |                       |                       |
|                       | ## 14.7  Pickli       |                       |
|                       | ng {#sec171 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1265} |                       |
|                       |                       |                       |
|                       | A limitation of       |                       |
|                       | [dbm]{.c004} is that  |                       |
|                       | the keys and values   |                       |
|                       | have to be strings or |                       |
|                       | bytes. If you try to  |                       |
|                       | use any other type,   |                       |
|                       | you get an error.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1266} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1267} |                       |
|                       |                       |                       |
|                       | The [pickle]{.c004}   |                       |
|                       | module can help. It   |                       |
|                       | translates almost any |                       |
|                       | type of object into a |                       |
|                       | string suitable for   |                       |
|                       | storage in a          |                       |
|                       | database, and then    |                       |
|                       | translates strings    |                       |
|                       | back into objects.    |                       |
|                       |                       |                       |
|                       | [pickle.dumps]{.c004} |                       |
|                       | takes an object as a  |                       |
|                       | parameter and returns |                       |
|                       | a string              |                       |
|                       | representation        |                       |
|                       | ([dumps]{.c004} is    |                       |
|                       | short for "dump       |                       |
|                       | string"):             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> import pickle     |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> pickle.dumps(t)   |                       |
|                       | b'\x80\x03]q\x        |                       |
|                       | 00(K\x01K\x02K\x03e.' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The format isn't      |                       |
|                       | obvious to human      |                       |
|                       | readers; it is meant  |                       |
|                       | to be easy for        |                       |
|                       | [pickle]{.c004} to    |                       |
|                       | interpret.            |                       |
|                       | [pickle.loads]{.c004} |                       |
|                       | ("load string")       |                       |
|                       | reconstitutes the     |                       |
|                       | object:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t1 = [1, 2, 3]    |                       |
|                       | >>>                   |                       |
|                       |  s = pickle.dumps(t1) |                       |
|                       | >>>                   |                       |
|                       |  t2 = pickle.loads(s) |                       |
|                       | >>> t2                |                       |
|                       | [1, 2, 3]             |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Although the new      |                       |
|                       | object has the same   |                       |
|                       | value as the old, it  |                       |
|                       | is not (in general)   |                       |
|                       | the same object:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t1 == t2          |                       |
|                       | True                  |                       |
|                       | >>> t1 is t2          |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In other words,       |                       |
|                       | pickling and then     |                       |
|                       | unpickling has the    |                       |
|                       | same effect as        |                       |
|                       | copying the object.   |                       |
|                       |                       |                       |
|                       | You can use           |                       |
|                       | [pickle]{.c004} to    |                       |
|                       | store non-strings in  |                       |
|                       | a database. In fact,  |                       |
|                       | this combination is   |                       |
|                       | so common that it has |                       |
|                       | been encapsulated in  |                       |
|                       | a module called       |                       |
|                       | [shelve]{.c004}.      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1268} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1269} |                       |
|                       |                       |                       |
|                       | ## 14.8  Pip          |                       |
|                       | es {#sec172 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1270} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1271} |                       |
|                       |                       |                       |
|                       | Most operating        |                       |
|                       | systems provide a     |                       |
|                       | command-line          |                       |
|                       | interface, also known |                       |
|                       | as a [shell]{.c010}.  |                       |
|                       | Shells usually        |                       |
|                       | provide commands to   |                       |
|                       | navigate the file     |                       |
|                       | system and launch     |                       |
|                       | applications. For     |                       |
|                       | example, in Unix you  |                       |
|                       | can change            |                       |
|                       | directories with      |                       |
|                       | [cd]{.c004}, display  |                       |
|                       | the contents of a     |                       |
|                       | directory with        |                       |
|                       | [ls]{.c004}, and      |                       |
|                       | launch a web browser  |                       |
|                       | by typing (for        |                       |
|                       | example)              |                       |
|                       | [firefox]{.c004}.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1272} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1273} |                       |
|                       |                       |                       |
|                       | Any program that you  |                       |
|                       | can launch from the   |                       |
|                       | shell can also be     |                       |
|                       | launched from Python  |                       |
|                       | using a [pipe         |                       |
|                       | object]{.c010}, which |                       |
|                       | represents a running  |                       |
|                       | program.              |                       |
|                       |                       |                       |
|                       | For example, the Unix |                       |
|                       | command [ls           |                       |
|                       | -l]{.c004} normally   |                       |
|                       | displays the contents |                       |
|                       | of the current        |                       |
|                       | directory in long     |                       |
|                       | format. You can       |                       |
|                       | launch [ls]{.c004}    |                       |
|                       | with                  |                       |
|                       | [os.popen]{.c004}^    |                       |
|                       | [1](#note1){#text1}^: |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1274} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1275} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> cmd = 'ls -l'     |                       |
|                       | >                     |                       |
|                       | >> fp = os.popen(cmd) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The argument is a     |                       |
|                       | string that contains  |                       |
|                       | a shell command. The  |                       |
|                       | return value is an    |                       |
|                       | object that behaves   |                       |
|                       | like an open file.    |                       |
|                       | You can read the      |                       |
|                       | output from the       |                       |
|                       | [ls]{.c004} process   |                       |
|                       | one line at a time    |                       |
|                       | with                  |                       |
|                       | [readline]{.c004} or  |                       |
|                       | get the whole thing   |                       |
|                       | at once with          |                       |
|                       | [read]{.c004}:        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1276} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1277} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1278} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1279} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> res = fp.read()   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | When you are done,    |                       |
|                       | you close the pipe    |                       |
|                       | like a file:          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1280} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1281} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> stat = fp.close() |                       |
|                       | >>> print(stat)       |                       |
|                       | None                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The return value is   |                       |
|                       | the final status of   |                       |
|                       | the [ls]{.c004}       |                       |
|                       | process;              |                       |
|                       | [None]{.c004} means   |                       |
|                       | that it ended         |                       |
|                       | normally (with no     |                       |
|                       | errors).              |                       |
|                       |                       |                       |
|                       | For example, most     |                       |
|                       | Unix systems provide  |                       |
|                       | a command called      |                       |
|                       | [md5sum]{.c004} that  |                       |
|                       | reads the contents of |                       |
|                       | a file and computes a |                       |
|                       | "checksum". You can   |                       |
|                       | read about MD5 at     |                       |
|                       | [[http://en.wik       |                       |
|                       | ipedia.org/wiki/Md5]{ |                       |
|                       | .c004}](http://en.wik |                       |
|                       | ipedia.org/wiki/Md5). |                       |
|                       | This command provides |                       |
|                       | an efficient way to   |                       |
|                       | check whether two     |                       |
|                       | files have the same   |                       |
|                       | contents. The         |                       |
|                       | probability that      |                       |
|                       | different contents    |                       |
|                       | yield the same        |                       |
|                       | checksum is very      |                       |
|                       | small (that is,       |                       |
|                       | unlikely to happen    |                       |
|                       | before the universe   |                       |
|                       | collapses).           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1282} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1283} |                       |
|                       |                       |                       |
|                       | You can use a pipe to |                       |
|                       | run [md5sum]{.c004}   |                       |
|                       | from Python and get   |                       |
|                       | the result:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | filename = 'book.tex' |                       |
|                       | >>> cmd =             |                       |
|                       |  'md5sum ' + filename |                       |
|                       | >                     |                       |
|                       | >> fp = os.popen(cmd) |                       |
|                       | >>> res = fp.read()   |                       |
|                       | >>> stat = fp.close() |                       |
|                       | >>> print(res)        |                       |
|                       | 1e0033f0ed0656636de0d |                       |
|                       | 75144ba32e0  book.tex |                       |
|                       | >>> print(stat)       |                       |
|                       | None                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 14.9  Writing modul |                       |
|                       | es {#sec173 .section} |                       |
|                       |                       |                       |
|                       | []{#modules}          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1284} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1285} |                       |
|                       |                       |                       |
|                       | Any file that         |                       |
|                       | contains Python code  |                       |
|                       | can be imported as a  |                       |
|                       | module. For example,  |                       |
|                       | suppose you have a    |                       |
|                       | file named            |                       |
|                       | [wc.py]{.c004} with   |                       |
|                       | the following code:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       |  linecount(filename): |                       |
|                       |     count = 0         |                       |
|                       |     for li            |                       |
|                       | ne in open(filename): |                       |
|                       |         count += 1    |                       |
|                       |     return count      |                       |
|                       |                       |                       |
|                       | prin                  |                       |
|                       | t(linecount('wc.py')) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you run this       |                       |
|                       | program, it reads     |                       |
|                       | itself and prints the |                       |
|                       | number of lines in    |                       |
|                       | the file, which is 7. |                       |
|                       | You can also import   |                       |
|                       | it like this:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> import wc         |                       |
|                       | 7                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now you have a module |                       |
|                       | object [wc]{.c004}:   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1286} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1287} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> wc                |                       |
|                       | <modu                 |                       |
|                       | le 'wc' from 'wc.py'> |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The module object     |                       |
|                       | provides `linecount`: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | wc.linecount('wc.py') |                       |
|                       | 7                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | So that's how you     |                       |
|                       | write modules in      |                       |
|                       | Python.               |                       |
|                       |                       |                       |
|                       | The only problem with |                       |
|                       | this example is that  |                       |
|                       | when you import the   |                       |
|                       | module it runs the    |                       |
|                       | test code at the      |                       |
|                       | bottom. Normally when |                       |
|                       | you import a module,  |                       |
|                       | it defines new        |                       |
|                       | functions but it      |                       |
|                       | doesn't run them.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1288} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1289} |                       |
|                       |                       |                       |
|                       | Programs that will be |                       |
|                       | imported as modules   |                       |
|                       | often use the         |                       |
|                       | following idiom:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if __                 |                       |
|                       | name__ == '__main__': |                       |
|                       |     prin              |                       |
|                       | t(linecount('wc.py')) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | `__name__` is a       |                       |
|                       | built-in variable     |                       |
|                       | that is set when the  |                       |
|                       | program starts. If    |                       |
|                       | the program is        |                       |
|                       | running as a script,  |                       |
|                       | `__name__` has the    |                       |
|                       | value `'__main__'`;   |                       |
|                       | in that case, the     |                       |
|                       | test code runs.       |                       |
|                       | Otherwise, if the     |                       |
|                       | module is being       |                       |
|                       | imported, the test    |                       |
|                       | code is skipped.      |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1290} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1291} |                       |
|                       |                       |                       |
|                       | As an exercise, type  |                       |
|                       | this example into a   |                       |
|                       | file named            |                       |
|                       | [wc.py]{.c004} and    |                       |
|                       | run it as a script.   |                       |
|                       | Then run the Python   |                       |
|                       | interpreter and       |                       |
|                       | [import wc]{.c004}.   |                       |
|                       | What is the value of  |                       |
|                       | `__name__` when the   |                       |
|                       | module is being       |                       |
|                       | imported?             |                       |
|                       |                       |                       |
|                       | Warning: If you       |                       |
|                       | import a module that  |                       |
|                       | has already been      |                       |
|                       | imported, Python does |                       |
|                       | nothing. It does not  |                       |
|                       | re-read the file,     |                       |
|                       | even if it has        |                       |
|                       | changed.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1292} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1293} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1294} |                       |
|                       |                       |                       |
|                       | If you want to reload |                       |
|                       | a module, you can use |                       |
|                       | the built-in function |                       |
|                       | [reload]{.c004}, but  |                       |
|                       | it can be tricky, so  |                       |
|                       | the safest thing to   |                       |
|                       | do is restart the     |                       |
|                       | interpreter and then  |                       |
|                       | import the module     |                       |
|                       | again.                |                       |
|                       |                       |                       |
|                       | ## 14.10  Debuggi     |                       |
|                       | ng {#sec174 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1295} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1296} |                       |
|                       |                       |                       |
|                       | When you are reading  |                       |
|                       | and writing files,    |                       |
|                       | you might run into    |                       |
|                       | problems with         |                       |
|                       | whitespace. These     |                       |
|                       | errors can be hard to |                       |
|                       | debug because spaces, |                       |
|                       | tabs and newlines are |                       |
|                       | normally invisible:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> s = '1 2\t 3\n 4' |                       |
|                       | >>> print(s)          |                       |
|                       | 1 2  3                |                       |
|                       |  4                    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1297} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1298} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1299} |                       |
|                       |                       |                       |
|                       | The built-in function |                       |
|                       | [repr]{.c004} can     |                       |
|                       | help. It takes any    |                       |
|                       | object as an argument |                       |
|                       | and returns a string  |                       |
|                       | representation of the |                       |
|                       | object. For strings,  |                       |
|                       | it represents         |                       |
|                       | whitespace characters |                       |
|                       | with backslash        |                       |
|                       | sequences:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> print(repr(s))    |                       |
|                       | '1 2\t 3\n 4'         |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This can be helpful   |                       |
|                       | for debugging.        |                       |
|                       |                       |                       |
|                       | One other problem you |                       |
|                       | might run into is     |                       |
|                       | that different        |                       |
|                       | systems use different |                       |
|                       | characters to         |                       |
|                       | indicate the end of a |                       |
|                       | line. Some systems    |                       |
|                       | use a newline,        |                       |
|                       | represented `\n`.     |                       |
|                       | Others use a return   |                       |
|                       | character,            |                       |
|                       | represented `\r`.     |                       |
|                       | Some use both. If you |                       |
|                       | move files between    |                       |
|                       | different systems,    |                       |
|                       | these inconsistencies |                       |
|                       | can cause problems.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1300} |                       |
|                       |                       |                       |
|                       | For most systems,     |                       |
|                       | there are             |                       |
|                       | applications to       |                       |
|                       | convert from one      |                       |
|                       | format to another.    |                       |
|                       | You can find them     |                       |
|                       | (and read more about  |                       |
|                       | this issue) at        |                       |
|                       | [[                    |                       |
|                       | http://en.wikipedia.o |                       |
|                       | rg/wiki/Newline]{.c00 |                       |
|                       | 4}](http://en.wikiped |                       |
|                       | ia.org/wiki/Newline). |                       |
|                       | Or, of course, you    |                       |
|                       | could write one       |                       |
|                       | yourself.             |                       |
|                       |                       |                       |
|                       | ## 14.11  Glossa      |                       |
|                       | ry {#sec175 .section} |                       |
|                       |                       |                       |
|                       | [persistent:]{.c010}  |                       |
|                       | :   Pertaining to a   |                       |
|                       |     program that runs |                       |
|                       |     indefinitely and  |                       |
|                       |     keeps at least    |                       |
|                       |     some of its data  |                       |
|                       |     in permanent      |                       |
|                       |     storage.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1301} |                       |
|                       |                       |                       |
|                       | [for                  |                       |
|                       | mat operator:]{.c010} |                       |
|                       | :   An operator,      |                       |
|                       |     [%]{.c004}, that  |                       |
|                       |     takes a format    |                       |
|                       |     string and a      |                       |
|                       |     tuple and         |                       |
|                       |     generates a       |                       |
|                       |     string that       |                       |
|                       |     includes the      |                       |
|                       |     elements of the   |                       |
|                       |     tuple formatted   |                       |
|                       |     as specified by   |                       |
|                       |     the format        |                       |
|                       |     string.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1302} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1303} |                       |
|                       |                       |                       |
|                       | [f                    |                       |
|                       | ormat string:]{.c010} |                       |
|                       | :   A string, used    |                       |
|                       |     with the format   |                       |
|                       |     operator, that    |                       |
|                       |     contains format   |                       |
|                       |     sequences.        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1304} |                       |
|                       |                       |                       |
|                       | [for                  |                       |
|                       | mat sequence:]{.c010} |                       |
|                       | :   A sequence of     |                       |
|                       |     characters in a   |                       |
|                       |     format string,    |                       |
|                       |     like [%d]{.c004}, |                       |
|                       |     that specifies    |                       |
|                       |     how a value       |                       |
|                       |     should be         |                       |
|                       |     formatted.        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1305} |                       |
|                       |                       |                       |
|                       | [text file:]{.c010}   |                       |
|                       | :   A sequence of     |                       |
|                       |     characters stored |                       |
|                       |     in permanent      |                       |
|                       |     storage like a    |                       |
|                       |     hard drive.       |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1306} |                       |
|                       |                       |                       |
|                       | [directory:]{.c010}   |                       |
|                       | :   A named           |                       |
|                       |     collection of     |                       |
|                       |     files, also       |                       |
|                       |     called a folder.  |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1307} |                       |
|                       |                       |                       |
|                       | [path:]{.c010}        |                       |
|                       | :   A string that     |                       |
|                       |     identifies a      |                       |
|                       |     file.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1308} |                       |
|                       |                       |                       |
|                       | [r                    |                       |
|                       | elative path:]{.c010} |                       |
|                       | :   A path that       |                       |
|                       |     starts from the   |                       |
|                       |     current           |                       |
|                       |     directory.        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1309} |                       |
|                       |                       |                       |
|                       | [a                    |                       |
|                       | bsolute path:]{.c010} |                       |
|                       | :   A path that       |                       |
|                       |     starts from the   |                       |
|                       |     topmost directory |                       |
|                       |     in the file       |                       |
|                       |     system.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1310} |                       |
|                       |                       |                       |
|                       | [catch:]{.c010}       |                       |
|                       | :   To prevent an     |                       |
|                       |     exception from    |                       |
|                       |     terminating a     |                       |
|                       |     program using the |                       |
|                       |     [try]{.c004} and  |                       |
|                       |     [except]{.c004}   |                       |
|                       |     statements.       |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1311} |                       |
|                       |                       |                       |
|                       | [database:]{.c010}    |                       |
|                       | :   A file whose      |                       |
|                       |     contents are      |                       |
|                       |     organized like a  |                       |
|                       |     dictionary with   |                       |
|                       |     keys that         |                       |
|                       |     correspond to     |                       |
|                       |     values.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1312} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | bytes object:]{.c010} |                       |
|                       | :   An object similar |                       |
|                       |     to a string.      |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1313} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1314} |                       |
|                       |                       |                       |
|                       | [shell:]{.c010}       |                       |
|                       | :   A program that    |                       |
|                       |     allows users to   |                       |
|                       |     type commands and |                       |
|                       |     then executes     |                       |
|                       |     them by starting  |                       |
|                       |     other programs.   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1315} |                       |
|                       |                       |                       |
|                       | [pipe object:]{.c010} |                       |
|                       | :   An object that    |                       |
|                       |     represents a      |                       |
|                       |     running program,  |                       |
|                       |     allowing a Python |                       |
|                       |     program to run    |                       |
|                       |     commands and read |                       |
|                       |     the results.      |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1316} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1317} |                       |
|                       |                       |                       |
|                       | ## 14.12  Exercis     |                       |
|                       | es {#sec176 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called [sed]{.c004}   |                       |
|                       | that takes as         |                       |
|                       | arguments a pattern   |                       |
|                       | string, a replacement |                       |
|                       | string, and two       |                       |
|                       | filenames; it should  |                       |
|                       | read the first file   |                       |
|                       | and write the         |                       |
|                       | contents into the     |                       |
|                       | second file (creating |                       |
|                       | it if necessary). If  |                       |
|                       | the pattern string    |                       |
|                       | appears anywhere in   |                       |
|                       | the file, it should   |                       |
|                       | be replaced with the  |                       |
|                       | replacement string.*  |                       |
|                       |                       |                       |
|                       | *If an error occurs   |                       |
|                       | while opening,        |                       |
|                       | reading, writing or   |                       |
|                       | closing files, your   |                       |
|                       | program should catch  |                       |
|                       | the exception, print  |                       |
|                       | an error message, and |                       |
|                       | exit. Solution:*      |                       |
|                       | [*[h                  |                       |
|                       | ttps://thinkpython.co |                       |
|                       | m/code/sed.py]{.c004} |                       |
|                       | *](https://thinkpytho |                       |
|                       | n.com/code/sed.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1318} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1319} |                       |
|                       |                       |                       |
|                       | *If you download my   |                       |
|                       | solution to           |                       |
|                       | Exer                  |                       |
|                       | cise *[*2*](thinkpyth |                       |
|                       | on2013.html#anagrams) |                       |
|                       | *from*                |                       |
|                       | [[*https://thinkpytho |                       |
|                       | n.com/code/anagram_se |                       |
|                       | ts.py*]{.c004}](https |                       |
|                       | ://thinkpython.com/co |                       |
|                       | de/anagram_sets.py)*, |                       |
|                       | you'll see that it    |                       |
|                       | creates a dictionary  |                       |
|                       | that maps from a      |                       |
|                       | sorted string of      |                       |
|                       | letters to the list   |                       |
|                       | of words that can be  |                       |
|                       | spelled with those    |                       |
|                       | letters. For example, |                       |
|                       | `'opst'` maps to the  |                       |
|                       | list                  |                       |
|                       | `['opts',             |                       |
|                       | 'post', 'pots', 'spot |                       |
|                       | ', 'stop', 'tops']`.* |                       |
|                       |                       |                       |
|                       | *Write a module that  |                       |
|                       | imports               |                       |
|                       | `anagram_sets` and    |                       |
|                       | provides two new      |                       |
|                       | functions:            |                       |
|                       | `store_anagrams`      |                       |
|                       | should store the      |                       |
|                       | anagram dictionary in |                       |
|                       | a "shelf";            |                       |
|                       | `read_anagrams`       |                       |
|                       | should look up a word |                       |
|                       | and return a list of  |                       |
|                       | its anagrams.         |                       |
|                       | Solution:*            |                       |
|                       | [[*https://thinkpy    |                       |
|                       | thon.com/code/anagram |                       |
|                       | _db.py*]{.c004}](http |                       |
|                       | s://thinkpython.com/c |                       |
|                       | ode/anagram_db.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       | []{#checksum}         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1320} |                       |
|                       |                       |                       |
|                       | *In a large           |                       |
|                       | collection of MP3     |                       |
|                       | files, there may be   |                       |
|                       | more than one copy of |                       |
|                       | the same song, stored |                       |
|                       | in different          |                       |
|                       | directories or with   |                       |
|                       | different file names. |                       |
|                       | The goal of this      |                       |
|                       | exercise is to search |                       |
|                       | for duplicates.*      |                       |
|                       |                       |                       |
|                       | 1.  *Write a program  |                       |
|                       |     that searches a   |                       |
|                       |     directory and all |                       |
|                       |     of its            |                       |
|                       |     subdirectories,   |                       |
|                       |     recursively, and  |                       |
|                       |     returns a list of |                       |
|                       |     complete paths    |                       |
|                       |     for all files     |                       |
|                       |     with a given      |                       |
|                       |     suffix (like      |                       |
|                       |     [.mp3]{.c004}).   |                       |
|                       |     Hint:             |                       |
|                       |     [os.path]{.c004}  |                       |
|                       |     provides several  |                       |
|                       |     useful functions  |                       |
|                       |     for manipulating  |                       |
|                       |     file and path     |                       |
|                       |     names.*           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1321} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1322} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1323} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1324} |                       |
|                       | 2.  *To recognize     |                       |
|                       |     duplicates, you   |                       |
|                       |     can use           |                       |
|                       |     [md5sum]{.c004}   |                       |
|                       |     to compute a      |                       |
|                       |     "checksum" for    |                       |
|                       |     each files. If    |                       |
|                       |     two files have    |                       |
|                       |     the same          |                       |
|                       |     checksum, they    |                       |
|                       |     probably have the |                       |
|                       |     same contents.*   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1325} |                       |
|                       | 3.  *To double-check, |                       |
|                       |     you can use the   |                       |
|                       |     Unix command      |                       |
|                       |     [diff]{.c004}.*   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1326} |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[http               |                       |
|                       | s://thinkpython.com/c |                       |
|                       | ode/find_duplicates.p |                       |
|                       | y]{.c004}*](https://t |                       |
|                       | hinkpython.com/code/f |                       |
|                       | ind_duplicates.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | -------------------   |                       |
|                       |                       |                       |
|                       | [1](#text1){#note1}   |                       |
|                       |                       |                       |
|                       | :   ::: footnotetext  |                       |
|                       |     [popen]{.c004} is |                       |
|                       |     deprecated now,   |                       |
|                       |     which means we    |                       |
|                       |     are supposed to   |                       |
|                       |     stop using it and |                       |
|                       |     start using the   |                       |
|                       |                       |                       |
|                       |   [subprocess]{.c004} |                       |
|                       |     module. But for   |                       |
|                       |     simple cases, I   |                       |
|                       |     find              |                       |
|                       |                       |                       |
|                       |   [subprocess]{.c004} |                       |
|                       |     more complicated  |                       |
|                       |     than necessary.   |                       |
|                       |     So I am going to  |                       |
|                       |     keep using        |                       |
|                       |     [popen]{.c004}    |                       |
|                       |     until they take   |                       |
|                       |     it away.          |                       |
|                       |     :::               |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2014.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2016.html)
---
generator: hevea 2.32
title: Classes and objects
---

[![Previous](back.png)](thinkpython2015.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2017.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter             | to support my books,  |
|                       | 15  Classes and objec | you can use the       |
|                       | ts {#sec177 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | []{#clobjects}        | you!                  |
|                       |                       |                       |
|                       | At this point you     |   -----------         |
|                       | know how to use       | --------------------- |
|                       | functions to organize | --------------------- |
|                       | code and built-in     | --------------------- |
|                       | types to organize     | --------------------- |
|                       | data. The next step   |   Pay what you want:  |
|                       | is to learn           |   Small \$1           |
|                       | "object-oriented      | .00 USD Medium \$5.00 |
|                       | programming", which   |  USD Large \$10.00 US |
|                       | uses                  | D X-Large \$20.00 USD |
|                       | programmer-defined    |  XX-Large \$50.00 USD |
|                       | types to organize     |   -----------         |
|                       | both code and data.   | --------------------- |
|                       | Object-oriented       | --------------------- |
|                       | programming is a big  | --------------------- |
|                       | topic; it will take a | --------------------- |
|                       | few chapters to get   |                       |
|                       | there.                | ![](                  |
|                       | [                     | https://www.paypalobj |
|                       | ]{#hevea_default1327} | ects.com/en_US/i/scr/ |
|                       |                       | pixel.gif){border="0" |
|                       | Code examples from    | width="1" height="1"} |
|                       | this chapter are      |                       |
|                       | available from        | ####                  |
|                       | [[http                | Are you using one of  |
|                       | s://thinkpython.com/c | our books in a class? |
|                       | ode/Point1.py]{.c004} |                       |
|                       | ](https://thinkpython | We\'d like to know    |
|                       | .com/code/Point1.py); | about it. Please      |
|                       | solutions to the      | consider filling out  |
|                       | exercises are         | [this short           |
|                       | available from        | survey](http://s      |
|                       | [[https://thinkp      | preadsheets.google.co |
|                       | ython.com/code/Point1 | m/viewform?formkey=dC |
|                       | _soln.py]{.c004}](htt | 0tNUZkMjBEdXVoRGljNm9 |
|                       | ps://thinkpython.com/ | FRmlTMHc6MA){onclick= |
|                       | code/Point1_soln.py). | "javascript: pageTrac |
|                       |                       | ker._trackPageview('/ |
|                       | ## 15.1  P            | outbound/survey');"}. |
|                       | rogrammer-defined typ |                       |
|                       | es {#sec178 .section} | \                     |
|                       |                       |                       |
|                       | []{#point}            | [Think                |
|                       | [                     | DSP](http             |
|                       | ]{#hevea_default1328} | ://www.amazon.com/gp/ |
|                       | [                     | product/1491938455/re |
|                       | ]{#hevea_default1329} | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | We have used many of  | &creativeASIN=1491938 |
|                       | Python's built-in     | 455&linkCode=as2&tag= |
|                       | types; now we are     | greenteapre01-20&link |
|                       | going to define a new | Id=2JJH4SWCAVVYSQHO){ |
|                       | type. As an example,  | rel="nofollow"}![](ht |
|                       | we will create a type | tp://ir-na.amazon-ads |
|                       | called [Point]{.c004} | ystem.com/e/ir?t=gree |
|                       | that represents a     | nteapre01-20&l=as2&o= |
|                       | point in              | 1&a=1491938455){.c003 |
|                       | two-dimensional       | width="1" height="1"  |
|                       | space.                | border="0"}           |
|                       | [                     |                       |
|                       | ]{#hevea_default1330} | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | In mathematical       | on-adsystem.com/widge |
|                       | notation, points are  | ts/q?_encoding=UTF8&A |
|                       | often written in      | SIN=1491938455&Format |
|                       | parentheses with a    | =_SL160_&ID=AsinImage |
|                       | comma separating the  | &MarketPlace=US&Servi |
|                       | coordinates. For      | ceVersion=20070822&WS |
|                       | example, (0,0)        | =1&tag=greenteapre01- |
|                       | represents the        | 20){border="0"}](http |
|                       | origin, and           | ://www.amazon.com/gp/ |
|                       | ([                    | product/1491938455/re |
|                       | x]{.c009},[y]{.c009}) | f=as_li_tl?ie=UTF8&ca |
|                       | represents the point  | mp=1789&creative=9325 |
|                       | [x]{.c009} units to   | &creativeASIN=1491938 |
|                       | the right and         | 455&linkCode=as2&tag= |
|                       | [y]{.c009} units up   | greenteapre01-20&link |
|                       | from the origin.      | Id=CTV7PDT7E5EGGJUM){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | There are several     | tp://ir-na.amazon-ads |
|                       | ways we might         | ystem.com/e/ir?t=gree |
|                       | represent points in   | nteapre01-20&l=as2&o= |
|                       | Python:               | 1&a=1491938455){.c003 |
|                       |                       | width="1" height="1"  |
|                       | -   We could store    | border="0"}           |
|                       |     the coordinates   |                       |
|                       |     separately in two | [Think                |
|                       |     variables,        | Java](http            |
|                       |     [x]{.c004} and    | ://www.amazon.com/gp/ |
|                       |     [y]{.c004}.       | product/1491929561/re |
|                       | -   We could store    | f=as_li_tl?ie=UTF8&ca |
|                       |     the coordinates   | mp=1789&creative=9325 |
|                       |     as elements in a  | &creativeASIN=1491929 |
|                       |     list or tuple.    | 561&linkCode=as2&tag= |
|                       | -   We could create a | greenteapre01-20&link |
|                       |     new type to       | Id=ZY6MAYM33ZTNSCNZ){ |
|                       |     represent points  | rel="nofollow"}![](ht |
|                       |     as objects.       | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | [                     | nteapre01-20&l=as2&o= |
|                       | ]{#hevea_default1331} | 1&a=1491929561){.c003 |
|                       |                       | width="1" height="1"  |
|                       | Creating a new type   | border="0"}           |
|                       | is more complicated   |                       |
|                       | than the other        | [                     |
|                       | options, but it has   | ![](http://ws-na.amaz |
|                       | advantages that will  | on-adsystem.com/widge |
|                       | be apparent soon.     | ts/q?_encoding=UTF8&A |
|                       |                       | SIN=1491929561&Format |
|                       | A programmer-defined  | =_SL160_&ID=AsinImage |
|                       | type is also called a | &MarketPlace=US&Servi |
|                       | [class]{.c010}. A     | ceVersion=20070822&WS |
|                       | class definition      | =1&tag=greenteapre01- |
|                       | looks like this:      | 20){border="0"}](http |
|                       | [                     | ://www.amazon.com/gp/ |
|                       | ]{#hevea_default1332} | product/1491929561/re |
|                       | [                     | f=as_li_tl?ie=UTF8&ca |
|                       | ]{#hevea_default1333} | mp=1789&creative=9325 |
|                       | [                     | &creativeASIN=1491929 |
|                       | ]{#hevea_default1334} | 561&linkCode=as2&tag= |
|                       | [                     | greenteapre01-20&link |
|                       | ]{#hevea_default1335} | Id=PT77ANWARUNNU3UK){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | ``` verbatim          | tp://ir-na.amazon-ads |
|                       | class Point:          | ystem.com/e/ir?t=gree |
|                       |     """Represents a p | nteapre01-20&l=as2&o= |
|                       | oint in 2-D space.""" | 1&a=1491929561){.c003 |
|                       | ```                   | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The header indicates  |                       |
|                       | that the new class is | [Think                |
|                       | called                | Bay                   |
|                       | [Point]{.c004}. The   | es](http://www.amazon |
|                       | body is a docstring   | .com/gp/product/14493 |
|                       | that explains what    | 70780/ref=as_li_qf_sp |
|                       | the class is for. You | _asin_tl?ie=UTF8&camp |
|                       | can define variables  | =1789&creative=9325&c |
|                       | and methods inside a  | reativeASIN=144937078 |
|                       | class definition, but | 0&linkCode=as2&tag=gr |
|                       | we will get back to   | eenteapre01-20)![](ht |
|                       | that later.           | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1336} | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1449370780){.c003 |
|                       | ]{#hevea_default1337} | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1338} |                       |
|                       |                       | [![](http://ws        |
|                       | Defining a class      | -na.amazon-adsystem.c |
|                       | named [Point]{.c004}  | om/widgets/q?_encodin |
|                       | creates a [class      | g=UTF8&ASIN=144937078 |
|                       | object]{.c010}.       | 0&Format=_SL160_&ID=A |
|                       |                       | sinImage&MarketPlace= |
|                       | ``` verbatim          | US&ServiceVersion=200 |
|                       | >>> Point             | 70822&WS=1&tag=greent |
|                       | <cl                   | eapre01-20){border="0 |
|                       | ass '__main__.Point'> | "}](http://www.amazon |
|                       | ```                   | .com/gp/product/14493 |
|                       |                       | 70780/ref=as_li_qf_sp |
|                       | Because               | _asin_il?ie=UTF8&camp |
|                       | [Point]{.c004} is     | =1789&creative=9325&c |
|                       | defined at the top    | reativeASIN=144937078 |
|                       | level, its "full      | 0&linkCode=as2&tag=gr |
|                       | name" is              | eenteapre01-20)![](ht |
|                       | `__main__.Point`.     | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1339} | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1449370780){.c003 |
|                       | ]{#hevea_default1340} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The class object is   |                       |
|                       | like a factory for    | [Think Python         |
|                       | creating objects. To  | 2e](http              |
|                       | create a Point, you   | ://www.amazon.com/gp/ |
|                       | call [Point]{.c004}   | product/1491939362/re |
|                       | as if it were a       | f=as_li_tl?ie=UTF8&ca |
|                       | function.             | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491939 |
|                       | ``` verbatim          | 362&linkCode=as2&tag= |
|                       | >>> blank = Point()   | greenteapre01-20&link |
|                       | >>> blank             | Id=FJKSQ3IHEMY2F2VA){ |
|                       | <__main__.Point       | rel="nofollow"}![](ht |
|                       | object at 0xb7e9d3ac> | tp://ir-na.amazon-ads |
|                       | ```                   | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | The return value is a | 1&a=1491939362){.c003 |
|                       | reference to a Point  | width="1" height="1"  |
|                       | object, which we      | border="0"}           |
|                       | assign to             |                       |
|                       | [blank]{.c004}.       | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | Creating a new object | on-adsystem.com/widge |
|                       | is called             | ts/q?_encoding=UTF8&A |
|                       | [i                    | SIN=1491939362&Format |
|                       | nstantiation]{.c010}, | =_SL160_&ID=AsinImage |
|                       | and the object is an  | &MarketPlace=US&Servi |
|                       | [instance]{.c010} of  | ceVersion=20070822&WS |
|                       | the class.            | =1&tag=greenteapre01- |
|                       | [                     | 20){border="0"}](http |
|                       | ]{#hevea_default1341} | ://www.amazon.com/gp/ |
|                       | [                     | product/1491939362/re |
|                       | ]{#hevea_default1342} | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | When you print an     | &creativeASIN=1491939 |
|                       | instance, Python      | 362&linkCode=as2&tag= |
|                       | tells you what class  | greenteapre01-20&link |
|                       | it belongs to and     | Id=ZZ454DLQ3IXDHNHX){ |
|                       | where it is stored in | rel="nofollow"}![](ht |
|                       | memory (the prefix    | tp://ir-na.amazon-ads |
|                       | [0x]{.c004} means     | ystem.com/e/ir?t=gree |
|                       | that the following    | nteapre01-20&l=as2&o= |
|                       | number is in          | 1&a=1491939362){.c003 |
|                       | hexadecimal).         | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1343} |                       |
|                       |                       | [Think Stats          |
|                       | Every object is an    | 2e](http://ww         |
|                       | instance of some      | w.amazon.com/gp/produ |
|                       | class, so "object"    | ct/1491907339/ref=as_ |
|                       | and "instance" are    | li_tl?ie=UTF8&camp=17 |
|                       | interchangeable. But  | 89&creative=9325&crea |
|                       | in this chapter I use | tiveASIN=1491907339&l |
|                       | "instance" to         | inkCode=as2&tag=green |
|                       | indicate that I am    | teapre01-20&linkId=O7 |
|                       | talking about a       | WYM6H6YBYUFNWU)![](ht |
|                       | programmer-defined    | tp://ir-na.amazon-ads |
|                       | type.                 | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ## 15.2  Attribut     | 1&a=1491907339){.c003 |
|                       | es {#sec179 .section} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | []{#attributes}       |                       |
|                       | [                     | [![](h                |
|                       | ]{#hevea_default1344} | ttp://ws-na.amazon-ad |
|                       | [                     | system.com/widgets/q? |
|                       | ]{#hevea_default1345} | _encoding=UTF8&ASIN=1 |
|                       | [                     | 491907339&Format=_SL1 |
|                       | ]{#hevea_default1346} | 60_&ID=AsinImage&Mark |
|                       |                       | etPlace=US&ServiceVer |
|                       | You can assign values | sion=20070822&WS=1&ta |
|                       | to an instance using  | g=greenteapre01-20){b |
|                       | dot notation:         | order="0"}](http://ww |
|                       |                       | w.amazon.com/gp/produ |
|                       | ``` verbatim          | ct/1491907339/ref=as_ |
|                       | >>> blank.x = 3.0     | li_tl?ie=UTF8&camp=17 |
|                       | >>> blank.y = 4.0     | 89&creative=9325&crea |
|                       | ```                   | tiveASIN=1491907339&l |
|                       |                       | inkCode=as2&tag=green |
|                       | This syntax is        | teapre01-20&linkId=JV |
|                       | similar to the syntax | SYKQHYSUIEYRHL)![](ht |
|                       | for selecting a       | tp://ir-na.amazon-ads |
|                       | variable from a       | ystem.com/e/ir?t=gree |
|                       | module, such as       | nteapre01-20&l=as2&o= |
|                       | [math.pi]{.c004} or   | 1&a=1491907339){.c003 |
|                       | [strin                | width="1" height="1"  |
|                       | g.whitespace]{.c004}. | border="0"}           |
|                       | In this case, though, |                       |
|                       | we are assigning      | [Think                |
|                       | values to named       | Complexity](http      |
|                       | elements of an        | ://www.amazon.com/gp/ |
|                       | object. These         | product/1449314635/re |
|                       | elements are called   | f=as_li_tf_tl?ie=UTF8 |
|                       | [attributes]{.c010}.  | &tag=greenteapre01-20 |
|                       |                       | &linkCode=as2&camp=17 |
|                       | As a noun,            | 89&creative=9325&crea |
|                       | "AT-trib-ute" is      | tiveASIN=1449314635)! |
|                       | pronounced with       | [](http://www.assoc-a |
|                       | emphasis on the first | mazon.com/e/ir?t=gree |
|                       | syllable, as opposed  | nteapre01-20&l=as2&o= |
|                       | to "a-TRIB-ute",      | 1&a=1449314635){.c003 |
|                       | which is a verb.      | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | Figu                  |                       |
|                       | re [15.1](#fig.point) | [                     |
|                       | is a state diagram    | ![](http://ws-na.amaz |
|                       | that shows the result | on-adsystem.com/widge |
|                       | of these assignments. | ts/q?_encoding=UTF8&A |
|                       | A state diagram that  | SIN=1449314635&Format |
|                       | shows an object and   | =_SL160_&ID=AsinImage |
|                       | its attributes is     | &MarketPlace=US&Servi |
|                       | called an [object     | ceVersion=20070822&WS |
|                       | diagram]{.c010}.      | =1&tag=greenteapre01- |
|                       | [                     | 20){border="0"}](http |
|                       | ]{#hevea_default1347} | ://www.amazon.com/gp/ |
|                       | [                     | product/1449314635/re |
|                       | ]{#hevea_default1348} | f=as_li_tf_il?ie=UTF8 |
|                       | [                     | &camp=1789&creative=9 |
|                       | ]{#hevea_default1349} | 325&creativeASIN=1449 |
|                       | [                     | 314635&linkCode=as2&t |
|                       | ]{#hevea_default1350} | ag=greenteapre01-20)! |
|                       |                       | [](http://www.assoc-a |
|                       | > ::: center          | mazon.com/e/ir?t=gree |
|                       | >                     | nteapre01-20&l=as2&o= |
|                       | > ------------------- | 1&a=1449314635){.c003 |
|                       | > :::                 | width="1" height="1"  |
|                       | >                     | border="0"}           |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2020.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       | 15.1: Object diagram. |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.point}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | The variable          |                       |
|                       | [blank]{.c004} refers |                       |
|                       | to a Point object,    |                       |
|                       | which contains two    |                       |
|                       | attributes. Each      |                       |
|                       | attribute refers to a |                       |
|                       | floating-point        |                       |
|                       | number.               |                       |
|                       |                       |                       |
|                       | You can read the      |                       |
|                       | value of an attribute |                       |
|                       | using the same        |                       |
|                       | syntax:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> blank.y           |                       |
|                       | 4.0                   |                       |
|                       | >>> x = blank.x       |                       |
|                       | >>> x                 |                       |
|                       | 3.0                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The expression        |                       |
|                       | [blank.x]{.c004}      |                       |
|                       | means, "Go to the     |                       |
|                       | object [blank]{.c004} |                       |
|                       | refers to and get the |                       |
|                       | value of [x]{.c004}." |                       |
|                       | In the example, we    |                       |
|                       | assign that value to  |                       |
|                       | a variable named      |                       |
|                       | [x]{.c004}. There is  |                       |
|                       | no conflict between   |                       |
|                       | the variable          |                       |
|                       | [x]{.c004} and the    |                       |
|                       | attribute [x]{.c004}. |                       |
|                       |                       |                       |
|                       | You can use dot       |                       |
|                       | notation as part of   |                       |
|                       | any expression. For   |                       |
|                       | example:              |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> '(%g, %g)'        |                       |
|                       |  % (blank.x, blank.y) |                       |
|                       | '(3.0, 4.0)'          |                       |
|                       | >>> dis               |                       |
|                       | tance = math.sqrt(bla |                       |
|                       | nk.x**2 + blank.y**2) |                       |
|                       | >>> distance          |                       |
|                       | 5.0                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | You can pass an       |                       |
|                       | instance as an        |                       |
|                       | argument in the usual |                       |
|                       | way. For example:     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1351} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_point(p):   |                       |
|                       |     print('(%         |                       |
|                       | g, %g)' % (p.x, p.y)) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | `print_point` takes a |                       |
|                       | point as an argument  |                       |
|                       | and displays it in    |                       |
|                       | mathematical          |                       |
|                       | notation. To invoke   |                       |
|                       | it, you can pass      |                       |
|                       | [blank]{.c004} as an  |                       |
|                       | argument:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >                     |                       |
|                       | >> print_point(blank) |                       |
|                       | (3.0, 4.0)            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Inside the function,  |                       |
|                       | [p]{.c004} is an      |                       |
|                       | alias for             |                       |
|                       | [blank]{.c004}, so if |                       |
|                       | the function modifies |                       |
|                       | [p]{.c004},           |                       |
|                       | [blank]{.c004}        |                       |
|                       | changes.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1352} |                       |
|                       |                       |                       |
|                       | As an exercise, write |                       |
|                       | a function called     |                       |
|                       | `dis                  |                       |
|                       | tance_between_points` |                       |
|                       | that takes two Points |                       |
|                       | as arguments and      |                       |
|                       | returns the distance  |                       |
|                       | between them.         |                       |
|                       |                       |                       |
|                       | ## 15.3  Rectangl     |                       |
|                       | es {#sec180 .section} |                       |
|                       |                       |                       |
|                       | []{#rectangles}       |                       |
|                       |                       |                       |
|                       | Sometimes it is       |                       |
|                       | obvious what the      |                       |
|                       | attributes of an      |                       |
|                       | object should be, but |                       |
|                       | other times you have  |                       |
|                       | to make decisions.    |                       |
|                       | For example, imagine  |                       |
|                       | you are designing a   |                       |
|                       | class to represent    |                       |
|                       | rectangles. What      |                       |
|                       | attributes would you  |                       |
|                       | use to specify the    |                       |
|                       | location and size of  |                       |
|                       | a rectangle? You can  |                       |
|                       | ignore angle; to keep |                       |
|                       | things simple, assume |                       |
|                       | that the rectangle is |                       |
|                       | either vertical or    |                       |
|                       | horizontal.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1353} |                       |
|                       |                       |                       |
|                       | There are at least    |                       |
|                       | two possibilities:    |                       |
|                       |                       |                       |
|                       | -   You could specify |                       |
|                       |     one corner of the |                       |
|                       |     rectangle (or the |                       |
|                       |     center), the      |                       |
|                       |     width, and the    |                       |
|                       |     height.           |                       |
|                       | -   You could specify |                       |
|                       |     two opposing      |                       |
|                       |     corners.          |                       |
|                       |                       |                       |
|                       | At this point it is   |                       |
|                       | hard to say whether   |                       |
|                       | either is better than |                       |
|                       | the other, so we'll   |                       |
|                       | implement the first   |                       |
|                       | one, just as an       |                       |
|                       | example.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1354} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1355} |                       |
|                       |                       |                       |
|                       | Here is the class     |                       |
|                       | definition:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | class Rectangle:      |                       |
|                       |     """Rep            |                       |
|                       | resents a rectangle.  |                       |
|                       |                       |                       |
|                       |     attributes: w     |                       |
|                       | idth, height, corner. |                       |
|                       |     """               |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The docstring lists   |                       |
|                       | the attributes:       |                       |
|                       | [width]{.c004} and    |                       |
|                       | [height]{.c004} are   |                       |
|                       | numbers;              |                       |
|                       | [corner]{.c004} is a  |                       |
|                       | Point object that     |                       |
|                       | specifies the         |                       |
|                       | lower-left corner.    |                       |
|                       |                       |                       |
|                       | To represent a        |                       |
|                       | rectangle, you have   |                       |
|                       | to instantiate a      |                       |
|                       | Rectangle object and  |                       |
|                       | assign values to the  |                       |
|                       | attributes:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | box = Rectangle()     |                       |
|                       | box.width = 100.0     |                       |
|                       | box.height = 200.0    |                       |
|                       | box.corner = Point()  |                       |
|                       | box.corner.x = 0.0    |                       |
|                       | box.corner.y = 0.0    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The expression        |                       |
|                       | [box.corner.x]{.c004} |                       |
|                       | means, "Go to the     |                       |
|                       | object [box]{.c004}   |                       |
|                       | refers to and select  |                       |
|                       | the attribute named   |                       |
|                       | [corner]{.c004}; then |                       |
|                       | go to that object and |                       |
|                       | select the attribute  |                       |
|                       | named [x]{.c004}."    |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2021.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       | 15.2: Object diagram. |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.rectangle}  |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | Figure [              |                       |
|                       | 15.2](#fig.rectangle) |                       |
|                       | shows the state of    |                       |
|                       | this object. An       |                       |
|                       | object that is an     |                       |
|                       | attribute of another  |                       |
|                       | object is             |                       |
|                       | [embedded]{.c010}.    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1356} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1357} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1358} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1359} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1360} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1361} |                       |
|                       |                       |                       |
|                       | ## 15.4  Ins          |                       |
|                       | tances as return valu |                       |
|                       | es {#sec181 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1362} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1363} |                       |
|                       |                       |                       |
|                       | Functions can return  |                       |
|                       | instances. For        |                       |
|                       | example,              |                       |
|                       | `find_center` takes a |                       |
|                       | [Rectangle]{.c004} as |                       |
|                       | an argument and       |                       |
|                       | returns a             |                       |
|                       | [Point]{.c004} that   |                       |
|                       | contains the          |                       |
|                       | coordinates of the    |                       |
|                       | center of the         |                       |
|                       | [Rectangle]{.c004}:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef find_center(rect): |                       |
|                       |     p = Point()       |                       |
|                       |     p.x = rect.co     |                       |
|                       | rner.x + rect.width/2 |                       |
|                       |     p.y = rect.cor    |                       |
|                       | ner.y + rect.height/2 |                       |
|                       |     return p          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here is an example    |                       |
|                       | that passes           |                       |
|                       | [box]{.c004} as an    |                       |
|                       | argument and assigns  |                       |
|                       | the resulting Point   |                       |
|                       | to [center]{.c004}:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> cent              |                       |
|                       | er = find_center(box) |                       |
|                       | >>                    |                       |
|                       | > print_point(center) |                       |
|                       | (50, 100)             |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 15                 |                       |
|                       | .5  Objects are mutab |                       |
|                       | le {#sec182 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1364} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1365} |                       |
|                       |                       |                       |
|                       | You can change the    |                       |
|                       | state of an object by |                       |
|                       | making an assignment  |                       |
|                       | to one of its         |                       |
|                       | attributes. For       |                       |
|                       | example, to change    |                       |
|                       | the size of a         |                       |
|                       | rectangle without     |                       |
|                       | changing its          |                       |
|                       | position, you can     |                       |
|                       | modify the values of  |                       |
|                       | [width]{.c004} and    |                       |
|                       | [height]{.c004}:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | box.w                 |                       |
|                       | idth = box.width + 50 |                       |
|                       | box.heig              |                       |
|                       | ht = box.height + 100 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | You can also write    |                       |
|                       | functions that modify |                       |
|                       | objects. For example, |                       |
|                       | `grow_rectangle`      |                       |
|                       | takes a Rectangle     |                       |
|                       | object and two        |                       |
|                       | numbers,              |                       |
|                       | [dwidth]{.c004} and   |                       |
|                       | [dheight]{.c004}, and |                       |
|                       | adds the numbers to   |                       |
|                       | the width and height  |                       |
|                       | of the rectangle:     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def grow_rectangle(re |                       |
|                       | ct, dwidth, dheight): |                       |
|                       |                       |                       |
|                       |  rect.width += dwidth |                       |
|                       |     r                 |                       |
|                       | ect.height += dheight |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here is an example    |                       |
|                       | that demonstrates the |                       |
|                       | effect:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | box.width, box.height |                       |
|                       | (150.0, 300.0)        |                       |
|                       | >>> grow_re           |                       |
|                       | ctangle(box, 50, 100) |                       |
|                       | >>>                   |                       |
|                       | box.width, box.height |                       |
|                       | (200.0, 400.0)        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Inside the function,  |                       |
|                       | [rect]{.c004} is an   |                       |
|                       | alias for             |                       |
|                       | [box]{.c004}, so when |                       |
|                       | the function modifies |                       |
|                       | [rect]{.c004},        |                       |
|                       | [box]{.c004} changes. |                       |
|                       |                       |                       |
|                       | As an exercise, write |                       |
|                       | a function named      |                       |
|                       | `move_rectangle` that |                       |
|                       | takes a Rectangle and |                       |
|                       | two numbers named     |                       |
|                       | [dx]{.c004} and       |                       |
|                       | [dy]{.c004}. It       |                       |
|                       | should change the     |                       |
|                       | location of the       |                       |
|                       | rectangle by adding   |                       |
|                       | [dx]{.c004} to the    |                       |
|                       | [x]{.c004} coordinate |                       |
|                       | of [corner]{.c004}    |                       |
|                       | and adding            |                       |
|                       | [dy]{.c004} to the    |                       |
|                       | [y]{.c004} coordinate |                       |
|                       | of [corner]{.c004}.   |                       |
|                       |                       |                       |
|                       | ## 15.6  Copyi        |                       |
|                       | ng {#sec183 .section} |                       |
|                       |                       |                       |
|                       | []{#copying}          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1366} |                       |
|                       |                       |                       |
|                       | Aliasing can make a   |                       |
|                       | program difficult to  |                       |
|                       | read because changes  |                       |
|                       | in one place might    |                       |
|                       | have unexpected       |                       |
|                       | effects in another    |                       |
|                       | place. It is hard to  |                       |
|                       | keep track of all the |                       |
|                       | variables that might  |                       |
|                       | refer to a given      |                       |
|                       | object.               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1367} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1368} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1369} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1370} |                       |
|                       |                       |                       |
|                       | Copying an object is  |                       |
|                       | often an alternative  |                       |
|                       | to aliasing. The      |                       |
|                       | [copy]{.c004} module  |                       |
|                       | contains a function   |                       |
|                       | called [copy]{.c004}  |                       |
|                       | that can duplicate    |                       |
|                       | any object:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> p1 = Point()      |                       |
|                       | >>> p1.x = 3.0        |                       |
|                       | >>> p1.y = 4.0        |                       |
|                       |                       |                       |
|                       | >>> import copy       |                       |
|                       | >                     |                       |
|                       | >> p2 = copy.copy(p1) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [p1]{.c004} and       |                       |
|                       | [p2]{.c004} contain   |                       |
|                       | the same data, but    |                       |
|                       | they are not the same |                       |
|                       | Point.                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> print_point(p1)   |                       |
|                       | (3, 4)                |                       |
|                       | >>> print_point(p2)   |                       |
|                       | (3, 4)                |                       |
|                       | >>> p1 is p2          |                       |
|                       | False                 |                       |
|                       | >>> p1 == p2          |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [is]{.c004}       |                       |
|                       | operator indicates    |                       |
|                       | that [p1]{.c004} and  |                       |
|                       | [p2]{.c004} are not   |                       |
|                       | the same object,      |                       |
|                       | which is what we      |                       |
|                       | expected. But you     |                       |
|                       | might have expected   |                       |
|                       | [==]{.c004} to yield  |                       |
|                       | [True]{.c004} because |                       |
|                       | these points contain  |                       |
|                       | the same data. In     |                       |
|                       | that case, you will   |                       |
|                       | be disappointed to    |                       |
|                       | learn that for        |                       |
|                       | instances, the        |                       |
|                       | default behavior of   |                       |
|                       | the [==]{.c004}       |                       |
|                       | operator is the same  |                       |
|                       | as the [is]{.c004}    |                       |
|                       | operator; it checks   |                       |
|                       | object identity, not  |                       |
|                       | object equivalence.   |                       |
|                       | That's because for    |                       |
|                       | programmer-defined    |                       |
|                       | types, Python doesn't |                       |
|                       | know what should be   |                       |
|                       | considered            |                       |
|                       | equivalent. At least, |                       |
|                       | not yet.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1371} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1372} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1373} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1374} |                       |
|                       |                       |                       |
|                       | If you use            |                       |
|                       | [copy.copy]{.c004} to |                       |
|                       | duplicate a           |                       |
|                       | Rectangle, you will   |                       |
|                       | find that it copies   |                       |
|                       | the Rectangle object  |                       |
|                       | but not the embedded  |                       |
|                       | Point.                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1375} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | box2 = copy.copy(box) |                       |
|                       | >>> box2 is box       |                       |
|                       | False                 |                       |
|                       | >>> box2              |                       |
|                       | .corner is box.corner |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2022.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       | 15.3: Object diagram. |                       |
|                       | >   ---------         |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.rectangle2} |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | Figure [1             |                       |
|                       | 5.3](#fig.rectangle2) |                       |
|                       | shows what the object |                       |
|                       | diagram looks like.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1376} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1377} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1378} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1379} |                       |
|                       | This operation is     |                       |
|                       | called a [shallow     |                       |
|                       | copy]{.c010} because  |                       |
|                       | it copies the object  |                       |
|                       | and any references it |                       |
|                       | contains, but not the |                       |
|                       | embedded objects.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1380} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1381} |                       |
|                       |                       |                       |
|                       | For most              |                       |
|                       | applications, this is |                       |
|                       | not what you want. In |                       |
|                       | this example,         |                       |
|                       | invoking              |                       |
|                       | `grow_rectangle` on   |                       |
|                       | one of the Rectangles |                       |
|                       | would not affect the  |                       |
|                       | other, but invoking   |                       |
|                       | `move_rectangle` on   |                       |
|                       | either would affect   |                       |
|                       | both! This behavior   |                       |
|                       | is confusing and      |                       |
|                       | error-prone.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1382} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1383} |                       |
|                       |                       |                       |
|                       | Fortunately, the      |                       |
|                       | [copy]{.c004} module  |                       |
|                       | provides a method     |                       |
|                       | named                 |                       |
|                       | [deepcopy]{.c004}     |                       |
|                       | that copies not only  |                       |
|                       | the object but also   |                       |
|                       | the objects it refers |                       |
|                       | to, and the objects   |                       |
|                       | *they* refer to, and  |                       |
|                       | so on. You will not   |                       |
|                       | be surprised to learn |                       |
|                       | that this operation   |                       |
|                       | is called a [deep     |                       |
|                       | copy]{.c010}.         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1384} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1385} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> box3              |                       |
|                       |  = copy.deepcopy(box) |                       |
|                       | >>> box3 is box       |                       |
|                       | False                 |                       |
|                       | >>> box3              |                       |
|                       | .corner is box.corner |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [box3]{.c004} and     |                       |
|                       | [box]{.c004} are      |                       |
|                       | completely separate   |                       |
|                       | objects.              |                       |
|                       |                       |                       |
|                       | As an exercise, write |                       |
|                       | a version of          |                       |
|                       | `move_rectangle` that |                       |
|                       | creates and returns a |                       |
|                       | new Rectangle instead |                       |
|                       | of modifying the old  |                       |
|                       | one.                  |                       |
|                       |                       |                       |
|                       | ## 15.7  Debuggi      |                       |
|                       | ng {#sec184 .section} |                       |
|                       |                       |                       |
|                       | []{#hasattr}          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1386} |                       |
|                       |                       |                       |
|                       | When you start        |                       |
|                       | working with objects, |                       |
|                       | you are likely to     |                       |
|                       | encounter some new    |                       |
|                       | exceptions. If you    |                       |
|                       | try to access an      |                       |
|                       | attribute that        |                       |
|                       | doesn't exist, you    |                       |
|                       | get an                |                       |
|                       | [At                   |                       |
|                       | tributeError]{.c004}: |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1387} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1388} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> p = Point()       |                       |
|                       | >>> p.x = 3           |                       |
|                       | >>> p.y = 4           |                       |
|                       | >>> p.z               |                       |
|                       | Attribute             |                       |
|                       | Error: Point instance |                       |
|                       |  has no attribute 'z' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you are not sure   |                       |
|                       | what type an object   |                       |
|                       | is, you can ask:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1389} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1390} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> type(p)           |                       |
|                       | <cl                   |                       |
|                       | ass '__main__.Point'> |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | You can also use      |                       |
|                       | [isinstance]{.c004}   |                       |
|                       | to check whether an   |                       |
|                       | object is an instance |                       |
|                       | of a class:           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1391} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1392} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       |  isinstance(p, Point) |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you are not sure   |                       |
|                       | whether an object has |                       |
|                       | a particular          |                       |
|                       | attribute, you can    |                       |
|                       | use the built-in      |                       |
|                       | function              |                       |
|                       | [hasattr]{.c004}:     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1393} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1394} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> hasattr(p, 'x')   |                       |
|                       | True                  |                       |
|                       | >>> hasattr(p, 'z')   |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first argument    |                       |
|                       | can be any object;    |                       |
|                       | the second argument   |                       |
|                       | is a *string* that    |                       |
|                       | contains the name of  |                       |
|                       | the attribute.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1395} |                       |
|                       |                       |                       |
|                       | You can also use a    |                       |
|                       | [try]{.c004}          |                       |
|                       | statement to see if   |                       |
|                       | the object has the    |                       |
|                       | attributes you need:  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1396} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1397} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | try:                  |                       |
|                       |     x = p.x           |                       |
|                       | e                     |                       |
|                       | xcept AttributeError: |                       |
|                       |     x = 0             |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This approach can     |                       |
|                       | make it easier to     |                       |
|                       | write functions that  |                       |
|                       | work with different   |                       |
|                       | types; more on that   |                       |
|                       | topic is coming up in |                       |
|                       | Section               |                       |
|                       | [17.9](thinkpython201 |                       |
|                       | 8.html#polymorphism). |                       |
|                       |                       |                       |
|                       | ## 15.8  Glossa       |                       |
|                       | ry {#sec185 .section} |                       |
|                       |                       |                       |
|                       | [class:]{.c010}       |                       |
|                       | :   A                 |                       |
|                       |                       |                       |
|                       |    programmer-defined |                       |
|                       |     type. A class     |                       |
|                       |     definition        |                       |
|                       |     creates a new     |                       |
|                       |     class object.     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1398} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1399} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1400} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | class object:]{.c010} |                       |
|                       | :   An object that    |                       |
|                       |     contains          |                       |
|                       |     information about |                       |
|                       |     a                 |                       |
|                       |                       |                       |
|                       |    programmer-defined |                       |
|                       |     type. The class   |                       |
|                       |     object can be     |                       |
|                       |     used to create    |                       |
|                       |     instances of the  |                       |
|                       |     type.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1401} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1402} |                       |
|                       |                       |                       |
|                       | [instance:]{.c010}    |                       |
|                       | :   An object that    |                       |
|                       |     belongs to a      |                       |
|                       |     class.            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1403} |                       |
|                       |                       |                       |
|                       | [instantiate:]{.c010} |                       |
|                       | :   To create a new   |                       |
|                       |     object.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1404} |                       |
|                       |                       |                       |
|                       | [attribute:]{.c010}   |                       |
|                       | :   One of the named  |                       |
|                       |     values associated |                       |
|                       |     with an object.   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1405} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1406} |                       |
|                       |                       |                       |
|                       | [emb                  |                       |
|                       | edded object:]{.c010} |                       |
|                       | :   An object that is |                       |
|                       |     stored as an      |                       |
|                       |     attribute of      |                       |
|                       |     another object.   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1407} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1408} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | shallow copy:]{.c010} |                       |
|                       | :   To copy the       |                       |
|                       |     contents of an    |                       |
|                       |     object, including |                       |
|                       |     any references to |                       |
|                       |     embedded objects; |                       |
|                       |     implemented by    |                       |
|                       |     the [copy]{.c004} |                       |
|                       |     function in the   |                       |
|                       |     [copy]{.c004}     |                       |
|                       |     module.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1409} |                       |
|                       |                       |                       |
|                       | [deep copy:]{.c010}   |                       |
|                       | :   To copy the       |                       |
|                       |     contents of an    |                       |
|                       |     object as well as |                       |
|                       |     any embedded      |                       |
|                       |     objects, and any  |                       |
|                       |     objects embedded  |                       |
|                       |     in them, and so   |                       |
|                       |     on; implemented   |                       |
|                       |     by the            |                       |
|                       |     [deepcopy]{.c004} |                       |
|                       |     function in the   |                       |
|                       |     [copy]{.c004}     |                       |
|                       |     module.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1410} |                       |
|                       |                       |                       |
|                       | [ob                   |                       |
|                       | ject diagram:]{.c010} |                       |
|                       | :   A diagram that    |                       |
|                       |     shows objects,    |                       |
|                       |     their attributes, |                       |
|                       |     and the values of |                       |
|                       |     the attributes.   |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1411} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1412} |                       |
|                       |                       |                       |
|                       | ## 15.9  Exercis      |                       |
|                       | es {#sec186 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a definition   |                       |
|                       | for a class named     |                       |
|                       | [Circle]{.c004} with  |                       |
|                       | attributes            |                       |
|                       | [center]{.c004} and   |                       |
|                       | [radius]{.c004},      |                       |
|                       | where [center]{.c004} |                       |
|                       | is a Point object and |                       |
|                       | [radius]{.c004} is a  |                       |
|                       | number.*              |                       |
|                       |                       |                       |
|                       | *Instantiate a Circle |                       |
|                       | object that           |                       |
|                       | represents a circle   |                       |
|                       | with its center at*   |                       |
|                       | (150, 100) *and       |                       |
|                       | radius 75.*           |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named                 |                       |
|                       | `point_in_circle`     |                       |
|                       | that takes a Circle   |                       |
|                       | and a Point and       |                       |
|                       | returns True if the   |                       |
|                       | Point lies in or on   |                       |
|                       | the boundary of the   |                       |
|                       | circle.*              |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named                 |                       |
|                       | `rect_in_circle` that |                       |
|                       | takes a Circle and a  |                       |
|                       | Rectangle and returns |                       |
|                       | True if the Rectangle |                       |
|                       | lies entirely in or   |                       |
|                       | on the boundary of    |                       |
|                       | the circle.*          |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named                 |                       |
|                       | `rect_circle_overlap` |                       |
|                       | that takes a Circle   |                       |
|                       | and a Rectangle and   |                       |
|                       | returns True if any   |                       |
|                       | of the corners of the |                       |
|                       | Rectangle fall inside |                       |
|                       | the Circle. Or as a   |                       |
|                       | more challenging      |                       |
|                       | version, return True  |                       |
|                       | if any part of the    |                       |
|                       | Rectangle falls       |                       |
|                       | inside the Circle.*   |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[https:/            |                       |
|                       | /thinkpython.com/code |                       |
|                       | /Circle.py]{.c004}*]( |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/Circle.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `draw_rect`    |                       |
|                       | that takes a Turtle   |                       |
|                       | object and a          |                       |
|                       | Rectangle and uses    |                       |
|                       | the Turtle to draw    |                       |
|                       | the Rectangle. See    |                       |
|                       | Chapt                 |                       |
|                       | er *[*4*](thinkpython |                       |
|                       | 2005.html#turtlechap) |                       |
|                       | *for examples using   |                       |
|                       | Turtle objects.*      |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `draw_circle`  |                       |
|                       | that takes a Turtle   |                       |
|                       | and a Circle and      |                       |
|                       | draws the Circle.*    |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[htt                |                       |
|                       | ps://thinkpython.com/ |                       |
|                       | code/draw.py]{.c004}* |                       |
|                       | ](https://thinkpython |                       |
|                       | .com/code/draw.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2015.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2017.html)
---
generator: hevea 2.32
title: Classes and functions
---

[![Previous](back.png)](thinkpython2016.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2018.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 16          | to support my books,  |
|                       |   Classes and functio | you can use the       |
|                       | ns {#sec187 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | []{#time}             | you!                  |
|                       |                       |                       |
|                       | Now that we know how  |   -----------         |
|                       | to create new types,  | --------------------- |
|                       | the next step is to   | --------------------- |
|                       | write functions that  | --------------------- |
|                       | take                  | --------------------- |
|                       | programmer-defined    |   Pay what you want:  |
|                       | objects as parameters |   Small \$1           |
|                       | and return them as    | .00 USD Medium \$5.00 |
|                       | results. In this      |  USD Large \$10.00 US |
|                       | chapter I also        | D X-Large \$20.00 USD |
|                       | present "functional   |  XX-Large \$50.00 USD |
|                       | programming style"    |   -----------         |
|                       | and two new program   | --------------------- |
|                       | development plans.    | --------------------- |
|                       |                       | --------------------- |
|                       | Code examples from    | --------------------- |
|                       | this chapter are      |                       |
|                       | available from        | ![](                  |
|                       | [[ht                  | https://www.paypalobj |
|                       | tps://thinkpython.com | ects.com/en_US/i/scr/ |
|                       | /code/Time1.py]{.c004 | pixel.gif){border="0" |
|                       | }](https://thinkpytho | width="1" height="1"} |
|                       | n.com/code/Time1.py). |                       |
|                       | Solutions to the      | ####                  |
|                       | exercises are at      | Are you using one of  |
|                       | [[https://thin        | our books in a class? |
|                       | kpython.com/code/Time |                       |
|                       | 1_soln.py]{.c004}](ht | We\'d like to know    |
|                       | tps://thinkpython.com | about it. Please      |
|                       | /code/Time1_soln.py). | consider filling out  |
|                       |                       | [this short           |
|                       | ## 16.1  Ti           | survey](http://s      |
|                       | me {#sec188 .section} | preadsheets.google.co |
|                       |                       | m/viewform?formkey=dC |
|                       | []{#isafter}          | 0tNUZkMjBEdXVoRGljNm9 |
|                       |                       | FRmlTMHc6MA){onclick= |
|                       | As another example of | "javascript: pageTrac |
|                       | a programmer-defined  | ker._trackPageview('/ |
|                       | type, we'll define a  | outbound/survey');"}. |
|                       | class called          |                       |
|                       | [Time]{.c004} that    | \                     |
|                       | records the time of   |                       |
|                       | day. The class        | [Think                |
|                       | definition looks like | DSP](http             |
|                       | this:                 | ://www.amazon.com/gp/ |
|                       | [                     | product/1491938455/re |
|                       | ]{#hevea_default1413} | f=as_li_tl?ie=UTF8&ca |
|                       | [                     | mp=1789&creative=9325 |
|                       | ]{#hevea_default1414} | &creativeASIN=1491938 |
|                       | [                     | 455&linkCode=as2&tag= |
|                       | ]{#hevea_default1415} | greenteapre01-20&link |
|                       | [                     | Id=2JJH4SWCAVVYSQHO){ |
|                       | ]{#hevea_default1416} | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | ``` verbatim          | ystem.com/e/ir?t=gree |
|                       | class Time:           | nteapre01-20&l=as2&o= |
|                       |     """Repres         | 1&a=1491938455){.c003 |
|                       | ents the time of day. | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       |     attributes:       |                       |
|                       |  hour, minute, second | [                     |
|                       |     """               | ![](http://ws-na.amaz |
|                       | ```                   | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | We can create a new   | SIN=1491938455&Format |
|                       | [Time]{.c004} object  | =_SL160_&ID=AsinImage |
|                       | and assign attributes | &MarketPlace=US&Servi |
|                       | for hours, minutes,   | ceVersion=20070822&WS |
|                       | and seconds:          | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | ``` verbatim          | ://www.amazon.com/gp/ |
|                       | time = Time()         | product/1491938455/re |
|                       | time.hour = 11        | f=as_li_tl?ie=UTF8&ca |
|                       | time.minute = 59      | mp=1789&creative=9325 |
|                       | time.second = 30      | &creativeASIN=1491938 |
|                       | ```                   | 455&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | The state diagram for | Id=CTV7PDT7E5EGGJUM){ |
|                       | the [Time]{.c004}     | rel="nofollow"}![](ht |
|                       | object looks like     | tp://ir-na.amazon-ads |
|                       | Figu                  | ystem.com/e/ir?t=gree |
|                       | re [16.1](#fig.time). | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491938455){.c003 |
|                       | ]{#hevea_default1417} | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1418} |                       |
|                       | [                     | [Think                |
|                       | ]{#hevea_default1419} | Java](http            |
|                       | [                     | ://www.amazon.com/gp/ |
|                       | ]{#hevea_default1420} | product/1491929561/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | As an exercise, write | mp=1789&creative=9325 |
|                       | a function called     | &creativeASIN=1491929 |
|                       | `print_time` that     | 561&linkCode=as2&tag= |
|                       | takes a Time object   | greenteapre01-20&link |
|                       | and prints it in the  | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | form                  | rel="nofollow"}![](ht |
|                       | [hour:m               | tp://ir-na.amazon-ads |
|                       | inute:second]{.c004}. | ystem.com/e/ir?t=gree |
|                       | Hint: the format      | nteapre01-20&l=as2&o= |
|                       | sequence `'%.2d'`     | 1&a=1491929561){.c003 |
|                       | prints an integer     | width="1" height="1"  |
|                       | using at least two    | border="0"}           |
|                       | digits, including a   |                       |
|                       | leading zero if       | [                     |
|                       | necessary.            | ![](http://ws-na.amaz |
|                       |                       | on-adsystem.com/widge |
|                       | Write a boolean       | ts/q?_encoding=UTF8&A |
|                       | function called       | SIN=1491929561&Format |
|                       | `is_after` that takes | =_SL160_&ID=AsinImage |
|                       | two Time objects,     | &MarketPlace=US&Servi |
|                       | [t1]{.c004} and       | ceVersion=20070822&WS |
|                       | [t2]{.c004}, and      | =1&tag=greenteapre01- |
|                       | returns [True]{.c004} | 20){border="0"}](http |
|                       | if [t1]{.c004}        | ://www.amazon.com/gp/ |
|                       | follows [t2]{.c004}   | product/1491929561/re |
|                       | chronologically and   | f=as_li_tl?ie=UTF8&ca |
|                       | [False]{.c004}        | mp=1789&creative=9325 |
|                       | otherwise. Challenge: | &creativeASIN=1491929 |
|                       | don't use an          | 561&linkCode=as2&tag= |
|                       | [if]{.c004}           | greenteapre01-20&link |
|                       | statement.            | Id=PT77ANWARUNNU3UK){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | > ::: center          | tp://ir-na.amazon-ads |
|                       | >                     | ystem.com/e/ir?t=gree |
|                       | > ------------------- | nteapre01-20&l=as2&o= |
|                       | > :::                 | 1&a=1491929561){.c003 |
|                       | >                     | width="1" height="1"  |
|                       | > ::: center          | border="0"}           |
|                       | > ![]                 |                       |
|                       | (thinkpython2023.png) | [Think                |
|                       | > :::                 | Bay                   |
|                       | >                     | es](http://www.amazon |
|                       | > ::: caption         | .com/gp/product/14493 |
|                       | >   ---------         | 70780/ref=as_li_qf_sp |
|                       | --------------------- | _asin_tl?ie=UTF8&camp |
|                       | >   Figure            | =1789&creative=9325&c |
|                       | 16.1: Object diagram. | reativeASIN=144937078 |
|                       | >   ---------         | 0&linkCode=as2&tag=gr |
|                       | --------------------- | eenteapre01-20)![](ht |
|                       | > :::                 | tp://ir-na.amazon-ads |
|                       | >                     | ystem.com/e/ir?t=gree |
|                       | > []{#fig.time}       | nteapre01-20&l=as2&o= |
|                       | >                     | 1&a=1449370780){.c003 |
|                       | > ::: center          | width="1" height="1"  |
|                       | >                     | border="0"}           |
|                       | > ------------------- |                       |
|                       | > :::                 | [![](http://ws        |
|                       |                       | -na.amazon-adsystem.c |
|                       | ## 16.2  Pure functio | om/widgets/q?_encodin |
|                       | ns {#sec189 .section} | g=UTF8&ASIN=144937078 |
|                       |                       | 0&Format=_SL160_&ID=A |
|                       | [                     | sinImage&MarketPlace= |
|                       | ]{#hevea_default1421} | US&ServiceVersion=200 |
|                       | [                     | 70822&WS=1&tag=greent |
|                       | ]{#hevea_default1422} | eapre01-20){border="0 |
|                       |                       | "}](http://www.amazon |
|                       | In the next few       | .com/gp/product/14493 |
|                       | sections, we'll write | 70780/ref=as_li_qf_sp |
|                       | two functions that    | _asin_il?ie=UTF8&camp |
|                       | add time values. They | =1789&creative=9325&c |
|                       | demonstrate two kinds | reativeASIN=144937078 |
|                       | of functions: pure    | 0&linkCode=as2&tag=gr |
|                       | functions and         | eenteapre01-20)![](ht |
|                       | modifiers. They also  | tp://ir-na.amazon-ads |
|                       | demonstrate a         | ystem.com/e/ir?t=gree |
|                       | development plan I'll | nteapre01-20&l=as2&o= |
|                       | call [prototype and   | 1&a=1449370780){.c003 |
|                       | patch]{.c010}, which  | width="1" height="1"  |
|                       | is a way of tackling  | border="0"}           |
|                       | a complex problem by  |                       |
|                       | starting with a       | [Think Python         |
|                       | simple prototype and  | 2e](http              |
|                       | incrementally dealing | ://www.amazon.com/gp/ |
|                       | with the              | product/1491939362/re |
|                       | complications.        | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | Here is a simple      | &creativeASIN=1491939 |
|                       | prototype of          | 362&linkCode=as2&tag= |
|                       | `add_time`:           | greenteapre01-20&link |
|                       |                       | Id=FJKSQ3IHEMY2F2VA){ |
|                       | ``` verbatim          | rel="nofollow"}![](ht |
|                       | def add_time(t1, t2): | tp://ir-na.amazon-ads |
|                       |     sum = Time()      | ystem.com/e/ir?t=gree |
|                       |     sum.hou           | nteapre01-20&l=as2&o= |
|                       | r = t1.hour + t2.hour | 1&a=1491939362){.c003 |
|                       |     sum.minute =      | width="1" height="1"  |
|                       | t1.minute + t2.minute | border="0"}           |
|                       |     sum.second =      |                       |
|                       | t1.second + t2.second | [                     |
|                       |     return sum        | ![](http://ws-na.amaz |
|                       | ```                   | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | The function creates  | SIN=1491939362&Format |
|                       | a new [Time]{.c004}   | =_SL160_&ID=AsinImage |
|                       | object, initializes   | &MarketPlace=US&Servi |
|                       | its attributes, and   | ceVersion=20070822&WS |
|                       | returns a reference   | =1&tag=greenteapre01- |
|                       | to the new object.    | 20){border="0"}](http |
|                       | This is called a      | ://www.amazon.com/gp/ |
|                       | [pure                 | product/1491939362/re |
|                       | function]{.c010}      | f=as_li_tl?ie=UTF8&ca |
|                       | because it does not   | mp=1789&creative=9325 |
|                       | modify any of the     | &creativeASIN=1491939 |
|                       | objects passed to it  | 362&linkCode=as2&tag= |
|                       | as arguments and it   | greenteapre01-20&link |
|                       | has no effect, like   | Id=ZZ454DLQ3IXDHNHX){ |
|                       | displaying a value or | rel="nofollow"}![](ht |
|                       | getting user input,   | tp://ir-na.amazon-ads |
|                       | other than returning  | ystem.com/e/ir?t=gree |
|                       | a value.              | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491939362){.c003 |
|                       | ]{#hevea_default1423} | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1424} |                       |
|                       |                       | [Think Stats          |
|                       | To test this          | 2e](http://ww         |
|                       | function, I'll create | w.amazon.com/gp/produ |
|                       | two Time objects:     | ct/1491907339/ref=as_ |
|                       | [start]{.c004}        | li_tl?ie=UTF8&camp=17 |
|                       | contains the start    | 89&creative=9325&crea |
|                       | time of a movie, like | tiveASIN=1491907339&l |
|                       | *Monty Python and the | inkCode=as2&tag=green |
|                       | Holy Grail*, and      | teapre01-20&linkId=O7 |
|                       | [duration]{.c004}     | WYM6H6YBYUFNWU)![](ht |
|                       | contains the run time | tp://ir-na.amazon-ads |
|                       | of the movie, which   | ystem.com/e/ir?t=gree |
|                       | is one hour 35        | nteapre01-20&l=as2&o= |
|                       | minutes.              | 1&a=1491907339){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1425} | border="0"}           |
|                       |                       |                       |
|                       | `add_time` figures    | [![](h                |
|                       | out when the movie    | ttp://ws-na.amazon-ad |
|                       | will be done.         | system.com/widgets/q? |
|                       |                       | _encoding=UTF8&ASIN=1 |
|                       | ``` verbatim          | 491907339&Format=_SL1 |
|                       | >>> start = Time()    | 60_&ID=AsinImage&Mark |
|                       | >>> start.hour = 9    | etPlace=US&ServiceVer |
|                       | >>> start.minute = 45 | sion=20070822&WS=1&ta |
|                       | >>> start.second =  0 | g=greenteapre01-20){b |
|                       |                       | order="0"}](http://ww |
|                       | >>> duration = Time() | w.amazon.com/gp/produ |
|                       | >>> duration.hour = 1 | ct/1491907339/ref=as_ |
|                       | >>>                   | li_tl?ie=UTF8&camp=17 |
|                       |  duration.minute = 35 | 89&creative=9325&crea |
|                       | >>                    | tiveASIN=1491907339&l |
|                       | > duration.second = 0 | inkCode=as2&tag=green |
|                       |                       | teapre01-20&linkId=JV |
|                       | >>> done = add_       | SYKQHYSUIEYRHL)![](ht |
|                       | time(start, duration) | tp://ir-na.amazon-ads |
|                       | >>> print_time(done)  | ystem.com/e/ir?t=gree |
|                       | 10:80:00              | nteapre01-20&l=as2&o= |
|                       | ```                   | 1&a=1491907339){.c003 |
|                       |                       | width="1" height="1"  |
|                       | The result,           | border="0"}           |
|                       | [10:80:00]{.c004}     |                       |
|                       | might not be what you | [Think                |
|                       | were hoping for. The  | Complexity](http      |
|                       | problem is that this  | ://www.amazon.com/gp/ |
|                       | function does not     | product/1449314635/re |
|                       | deal with cases where | f=as_li_tf_tl?ie=UTF8 |
|                       | the number of seconds | &tag=greenteapre01-20 |
|                       | or minutes adds up to | &linkCode=as2&camp=17 |
|                       | more than sixty. When | 89&creative=9325&crea |
|                       | that happens, we have | tiveASIN=1449314635)! |
|                       | to "carry" the extra  | [](http://www.assoc-a |
|                       | seconds into the      | mazon.com/e/ir?t=gree |
|                       | minute column or the  | nteapre01-20&l=as2&o= |
|                       | extra minutes into    | 1&a=1449314635){.c003 |
|                       | the hour column.      | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1426} |                       |
|                       |                       | [                     |
|                       | Here's an improved    | ![](http://ws-na.amaz |
|                       | version:              | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | ``` verbatim          | SIN=1449314635&Format |
|                       | def add_time(t1, t2): | =_SL160_&ID=AsinImage |
|                       |     sum = Time()      | &MarketPlace=US&Servi |
|                       |     sum.hou           | ceVersion=20070822&WS |
|                       | r = t1.hour + t2.hour | =1&tag=greenteapre01- |
|                       |     sum.minute =      | 20){border="0"}](http |
|                       | t1.minute + t2.minute | ://www.amazon.com/gp/ |
|                       |     sum.second =      | product/1449314635/re |
|                       | t1.second + t2.second | f=as_li_tf_il?ie=UTF8 |
|                       |                       | &camp=1789&creative=9 |
|                       |                       | 325&creativeASIN=1449 |
|                       |  if sum.second >= 60: | 314635&linkCode=as2&t |
|                       |                       | ag=greenteapre01-20)! |
|                       |      sum.second -= 60 | [](http://www.assoc-a |
|                       |                       | mazon.com/e/ir?t=gree |
|                       |       sum.minute += 1 | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1449314635){.c003 |
|                       |                       | width="1" height="1"  |
|                       |  if sum.minute >= 60: | border="0"}           |
|                       |                       |                       |
|                       |      sum.minute -= 60 |                       |
|                       |         sum.hour += 1 |                       |
|                       |                       |                       |
|                       |     return sum        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Although this         |                       |
|                       | function is correct,  |                       |
|                       | it is starting to get |                       |
|                       | big. We will see a    |                       |
|                       | shorter alternative   |                       |
|                       | later.                |                       |
|                       |                       |                       |
|                       | ## 16.3  Modifie      |                       |
|                       | rs {#sec190 .section} |                       |
|                       |                       |                       |
|                       | []{#increment}        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1427} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1428} |                       |
|                       |                       |                       |
|                       | Sometimes it is       |                       |
|                       | useful for a function |                       |
|                       | to modify the objects |                       |
|                       | it gets as            |                       |
|                       | parameters. In that   |                       |
|                       | case, the changes are |                       |
|                       | visible to the        |                       |
|                       | caller. Functions     |                       |
|                       | that work this way    |                       |
|                       | are called            |                       |
|                       | [modifiers]{.c010}.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1429} |                       |
|                       |                       |                       |
|                       | [increment]{.c004},   |                       |
|                       | which adds a given    |                       |
|                       | number of seconds to  |                       |
|                       | a [Time]{.c004}       |                       |
|                       | object, can be        |                       |
|                       | written naturally as  |                       |
|                       | a modifier. Here is a |                       |
|                       | rough draft:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def incr              |                       |
|                       | ement(time, seconds): |                       |
|                       |     t                 |                       |
|                       | ime.second += seconds |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       | if time.second >= 60: |                       |
|                       |                       |                       |
|                       |     time.second -= 60 |                       |
|                       |                       |                       |
|                       |      time.minute += 1 |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       | if time.minute >= 60: |                       |
|                       |                       |                       |
|                       |     time.minute -= 60 |                       |
|                       |                       |                       |
|                       |        time.hour += 1 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first line        |                       |
|                       | performs the basic    |                       |
|                       | operation; the        |                       |
|                       | remainder deals with  |                       |
|                       | the special cases we  |                       |
|                       | saw before.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1430} |                       |
|                       |                       |                       |
|                       | Is this function      |                       |
|                       | correct? What happens |                       |
|                       | if [seconds]{.c004}   |                       |
|                       | is much greater than  |                       |
|                       | sixty?                |                       |
|                       |                       |                       |
|                       | In that case, it is   |                       |
|                       | not enough to carry   |                       |
|                       | once; we have to keep |                       |
|                       | doing it until        |                       |
|                       | [time.second]{.c004}  |                       |
|                       | is less than sixty.   |                       |
|                       | One solution is to    |                       |
|                       | replace the           |                       |
|                       | [if]{.c004}           |                       |
|                       | statements with       |                       |
|                       | [while]{.c004}        |                       |
|                       | statements. That      |                       |
|                       | would make the        |                       |
|                       | function correct, but |                       |
|                       | not very efficient.   |                       |
|                       | As an exercise, write |                       |
|                       | a correct version of  |                       |
|                       | [increment]{.c004}    |                       |
|                       | that doesn't contain  |                       |
|                       | any loops.            |                       |
|                       |                       |                       |
|                       | Anything that can be  |                       |
|                       | done with modifiers   |                       |
|                       | can also be done with |                       |
|                       | pure functions. In    |                       |
|                       | fact, some            |                       |
|                       | programming languages |                       |
|                       | only allow pure       |                       |
|                       | functions. There is   |                       |
|                       | some evidence that    |                       |
|                       | programs that use     |                       |
|                       | pure functions are    |                       |
|                       | faster to develop and |                       |
|                       | less error-prone than |                       |
|                       | programs that use     |                       |
|                       | modifiers. But        |                       |
|                       | modifiers are         |                       |
|                       | convenient at times,  |                       |
|                       | and functional        |                       |
|                       | programs tend to be   |                       |
|                       | less efficient.       |                       |
|                       |                       |                       |
|                       | In general, I         |                       |
|                       | recommend that you    |                       |
|                       | write pure functions  |                       |
|                       | whenever it is        |                       |
|                       | reasonable and resort |                       |
|                       | to modifiers only if  |                       |
|                       | there is a compelling |                       |
|                       | advantage. This       |                       |
|                       | approach might be     |                       |
|                       | called a [functional  |                       |
|                       | programming           |                       |
|                       | style]{.c010}.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1431} |                       |
|                       |                       |                       |
|                       | As an exercise, write |                       |
|                       | a "pure" version of   |                       |
|                       | [increment]{.c004}    |                       |
|                       | that creates and      |                       |
|                       | returns a new Time    |                       |
|                       | object rather than    |                       |
|                       | modifying the         |                       |
|                       | parameter.            |                       |
|                       |                       |                       |
|                       | ## 16.4  Prot         |                       |
|                       | otyping versus planni |                       |
|                       | ng {#sec191 .section} |                       |
|                       |                       |                       |
|                       | []{#prototype}        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1432} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1433} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1434} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1435} |                       |
|                       |                       |                       |
|                       | The development plan  |                       |
|                       | I am demonstrating is |                       |
|                       | called "prototype and |                       |
|                       | patch". For each      |                       |
|                       | function, I wrote a   |                       |
|                       | prototype that        |                       |
|                       | performed the basic   |                       |
|                       | calculation and then  |                       |
|                       | tested it, patching   |                       |
|                       | errors along the way. |                       |
|                       |                       |                       |
|                       | This approach can be  |                       |
|                       | effective, especially |                       |
|                       | if you don't yet have |                       |
|                       | a deep understanding  |                       |
|                       | of the problem. But   |                       |
|                       | incremental           |                       |
|                       | corrections can       |                       |
|                       | generate code that is |                       |
|                       | unnecessarily         |                       |
|                       | complicated---since   |                       |
|                       | it deals with many    |                       |
|                       | special cases---and   |                       |
|                       | unreliable---since it |                       |
|                       | is hard to know if    |                       |
|                       | you have found all    |                       |
|                       | the errors.           |                       |
|                       |                       |                       |
|                       | An alternative is     |                       |
|                       | [designed             |                       |
|                       | development]{.c010},  |                       |
|                       | in which high-level   |                       |
|                       | insight into the      |                       |
|                       | problem can make the  |                       |
|                       | programming much      |                       |
|                       | easier. In this case, |                       |
|                       | the insight is that a |                       |
|                       | Time object is really |                       |
|                       | a three-digit number  |                       |
|                       | in base 60 (see       |                       |
|                       | [[http://en           |                       |
|                       | .wikipedia.org/wiki/S |                       |
|                       | exagesimal]{.c004}](h |                       |
|                       | ttp://en.wikipedia.or |                       |
|                       | g/wiki/Sexagesimal)). |                       |
|                       | The [second]{.c004}   |                       |
|                       | attribute is the      |                       |
|                       | "ones column", the    |                       |
|                       | [minute]{.c004}       |                       |
|                       | attribute is the      |                       |
|                       | "sixties column", and |                       |
|                       | the [hour]{.c004}     |                       |
|                       | attribute is the      |                       |
|                       | "thirty-six hundreds  |                       |
|                       | column".              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1436} |                       |
|                       |                       |                       |
|                       | When we wrote         |                       |
|                       | `add_time` and        |                       |
|                       | [increment]{.c004},   |                       |
|                       | we were effectively   |                       |
|                       | doing addition in     |                       |
|                       | base 60, which is why |                       |
|                       | we had to carry from  |                       |
|                       | one column to the     |                       |
|                       | next.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1437} |                       |
|                       |                       |                       |
|                       | This observation      |                       |
|                       | suggests another      |                       |
|                       | approach to the whole |                       |
|                       | problem---we can      |                       |
|                       | convert Time objects  |                       |
|                       | to integers and take  |                       |
|                       | advantage of the fact |                       |
|                       | that the computer     |                       |
|                       | knows how to do       |                       |
|                       | integer arithmetic.   |                       |
|                       |                       |                       |
|                       | Here is a function    |                       |
|                       | that converts Times   |                       |
|                       | to integers:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef time_to_int(time): |                       |
|                       |     minutes = time.ho |                       |
|                       | ur * 60 + time.minute |                       |
|                       |     seconds = minut   |                       |
|                       | es * 60 + time.second |                       |
|                       |     return seconds    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And here is a         |                       |
|                       | function that         |                       |
|                       | converts an integer   |                       |
|                       | to a Time (recall     |                       |
|                       | that [divmod]{.c004}  |                       |
|                       | divides the first     |                       |
|                       | argument by the       |                       |
|                       | second and returns    |                       |
|                       | the quotient and      |                       |
|                       | remainder as a        |                       |
|                       | tuple).               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1438} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | int_to_time(seconds): |                       |
|                       |     time = Time()     |                       |
|                       |                       |                       |
|                       | minutes, time.second  |                       |
|                       | = divmod(seconds, 60) |                       |
|                       |     ti                |                       |
|                       | me.hour, time.minute  |                       |
|                       | = divmod(minutes, 60) |                       |
|                       |     return time       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | You might have to     |                       |
|                       | think a bit, and run  |                       |
|                       | some tests, to        |                       |
|                       | convince yourself     |                       |
|                       | that these functions  |                       |
|                       | are correct. One way  |                       |
|                       | to test them is to    |                       |
|                       | check that            |                       |
|                       | `time_to_int(         |                       |
|                       | int_to_time(x)) == x` |                       |
|                       | for many values of    |                       |
|                       | [x]{.c004}. This is   |                       |
|                       | an example of a       |                       |
|                       | consistency check.    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1439} |                       |
|                       |                       |                       |
|                       | Once you are          |                       |
|                       | convinced they are    |                       |
|                       | correct, you can use  |                       |
|                       | them to rewrite       |                       |
|                       | `add_time`:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def add_time(t1, t2): |                       |
|                       |     s                 |                       |
|                       | econds = time_to_int( |                       |
|                       | t1) + time_to_int(t2) |                       |
|                       |     return            |                       |
|                       |  int_to_time(seconds) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This version is       |                       |
|                       | shorter than the      |                       |
|                       | original, and easier  |                       |
|                       | to verify. As an      |                       |
|                       | exercise, rewrite     |                       |
|                       | [increment]{.c004}    |                       |
|                       | using `time_to_int`   |                       |
|                       | and `int_to_time`.    |                       |
|                       |                       |                       |
|                       | In some ways,         |                       |
|                       | converting from base  |                       |
|                       | 60 to base 10 and     |                       |
|                       | back is harder than   |                       |
|                       | just dealing with     |                       |
|                       | times. Base           |                       |
|                       | conversion is more    |                       |
|                       | abstract; our         |                       |
|                       | intuition for dealing |                       |
|                       | with time values is   |                       |
|                       | better.               |                       |
|                       |                       |                       |
|                       | But if we have the    |                       |
|                       | insight to treat      |                       |
|                       | times as base 60      |                       |
|                       | numbers and make the  |                       |
|                       | investment of writing |                       |
|                       | the conversion        |                       |
|                       | functions             |                       |
|                       | (`time_to_int` and    |                       |
|                       | `int_to_time`), we    |                       |
|                       | get a program that is |                       |
|                       | shorter, easier to    |                       |
|                       | read and debug, and   |                       |
|                       | more reliable.        |                       |
|                       |                       |                       |
|                       | It is also easier to  |                       |
|                       | add features later.   |                       |
|                       | For example, imagine  |                       |
|                       | subtracting two Times |                       |
|                       | to find the duration  |                       |
|                       | between them. The     |                       |
|                       | naive approach would  |                       |
|                       | be to implement       |                       |
|                       | subtraction with      |                       |
|                       | borrowing. Using the  |                       |
|                       | conversion functions  |                       |
|                       | would be easier and   |                       |
|                       | more likely to be     |                       |
|                       | correct.              |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1440} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1441} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1442} |                       |
|                       |                       |                       |
|                       | Ironically, sometimes |                       |
|                       | making a problem      |                       |
|                       | harder (or more       |                       |
|                       | general) makes it     |                       |
|                       | easier (because there |                       |
|                       | are fewer special     |                       |
|                       | cases and fewer       |                       |
|                       | opportunities for     |                       |
|                       | error).               |                       |
|                       |                       |                       |
|                       | ## 16.5  Debuggi      |                       |
|                       | ng {#sec192 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1443} |                       |
|                       |                       |                       |
|                       | A Time object is      |                       |
|                       | well-formed if the    |                       |
|                       | values of             |                       |
|                       | [minute]{.c004} and   |                       |
|                       | [second]{.c004} are   |                       |
|                       | between 0 and 60      |                       |
|                       | (including 0 but not  |                       |
|                       | 60) and if            |                       |
|                       | [hour]{.c004} is      |                       |
|                       | positive.             |                       |
|                       | [hour]{.c004} and     |                       |
|                       | [minute]{.c004}       |                       |
|                       | should be integer     |                       |
|                       | values, but we might  |                       |
|                       | allow [second]{.c004} |                       |
|                       | to have a fraction    |                       |
|                       | part.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1444} |                       |
|                       |                       |                       |
|                       | Requirements like     |                       |
|                       | these are called      |                       |
|                       | [invariants]{.c010}   |                       |
|                       | because they should   |                       |
|                       | always be true. To    |                       |
|                       | put it a different    |                       |
|                       | way, if they are not  |                       |
|                       | true, something has   |                       |
|                       | gone wrong.           |                       |
|                       |                       |                       |
|                       | Writing code to check |                       |
|                       | invariants can help   |                       |
|                       | detect errors and     |                       |
|                       | find their causes.    |                       |
|                       | For example, you      |                       |
|                       | might have a function |                       |
|                       | like `valid_time`     |                       |
|                       | that takes a Time     |                       |
|                       | object and returns    |                       |
|                       | [False]{.c004} if it  |                       |
|                       | violates an           |                       |
|                       | invariant:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def valid_time(time): |                       |
|                       |     if time.hour      |                       |
|                       | < 0 or time.minute <  |                       |
|                       | 0 or time.second < 0: |                       |
|                       |         return False  |                       |
|                       |                       |                       |
|                       | if time.minute >= 60  |                       |
|                       | or time.second >= 60: |                       |
|                       |         return False  |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | At the beginning of   |                       |
|                       | each function you     |                       |
|                       | could check the       |                       |
|                       | arguments to make     |                       |
|                       | sure they are valid:  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1445} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1446} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def add_time(t1, t2): |                       |
|                       |     if                |                       |
|                       |  not valid_time(t1) o |                       |
|                       | r not valid_time(t2): |                       |
|                       |         raise Val     |                       |
|                       | ueError('invalid Time |                       |
|                       |  object in add_time') |                       |
|                       |     s                 |                       |
|                       | econds = time_to_int( |                       |
|                       | t1) + time_to_int(t2) |                       |
|                       |     return            |                       |
|                       |  int_to_time(seconds) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Or you could use an   |                       |
|                       | [assert               |                       |
|                       | statement]{.c010},    |                       |
|                       | which checks a given  |                       |
|                       | invariant and raises  |                       |
|                       | an exception if it    |                       |
|                       | fails:                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1447} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1448} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def add_time(t1, t2): |                       |
|                       |                       |                       |
|                       |   assert valid_time(t |                       |
|                       | 1) and valid_time(t2) |                       |
|                       |     s                 |                       |
|                       | econds = time_to_int( |                       |
|                       | t1) + time_to_int(t2) |                       |
|                       |     return            |                       |
|                       |  int_to_time(seconds) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [assert]{.c004}       |                       |
|                       | statements are useful |                       |
|                       | because they          |                       |
|                       | distinguish code that |                       |
|                       | deals with normal     |                       |
|                       | conditions from code  |                       |
|                       | that checks for       |                       |
|                       | errors.               |                       |
|                       |                       |                       |
|                       | ## 16.6  Glossa       |                       |
|                       | ry {#sec193 .section} |                       |
|                       |                       |                       |
|                       | [prototy              |                       |
|                       | pe and patch:]{.c010} |                       |
|                       | :   A development     |                       |
|                       |     plan that         |                       |
|                       |     involves writing  |                       |
|                       |     a rough draft of  |                       |
|                       |     a program,        |                       |
|                       |     testing, and      |                       |
|                       |     correcting errors |                       |
|                       |     as they are       |                       |
|                       |     found.            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1449} |                       |
|                       |                       |                       |
|                       | [designed             |                       |
|                       |  development:]{.c010} |                       |
|                       | :   A development     |                       |
|                       |     plan that         |                       |
|                       |     involves          |                       |
|                       |     high-level        |                       |
|                       |     insight into the  |                       |
|                       |     problem and more  |                       |
|                       |     planning than     |                       |
|                       |     incremental       |                       |
|                       |     development or    |                       |
|                       |     prototype         |                       |
|                       |     development.      |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1450} |                       |
|                       |                       |                       |
|                       | [p                    |                       |
|                       | ure function:]{.c010} |                       |
|                       | :   A function that   |                       |
|                       |     does not modify   |                       |
|                       |     any of the        |                       |
|                       |     objects it        |                       |
|                       |     receives as       |                       |
|                       |     arguments. Most   |                       |
|                       |     pure functions    |                       |
|                       |     are fruitful.     |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1451} |                       |
|                       |                       |                       |
|                       | [modifier:]{.c010}    |                       |
|                       | :   A function that   |                       |
|                       |     changes one or    |                       |
|                       |     more of the       |                       |
|                       |     objects it        |                       |
|                       |     receives as       |                       |
|                       |     arguments. Most   |                       |
|                       |     modifiers are     |                       |
|                       |     void; that is,    |                       |
|                       |     they return       |                       |
|                       |     [None]{.c004}.    |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1452} |                       |
|                       |                       |                       |
|                       | [functional progr     |                       |
|                       | amming style:]{.c010} |                       |
|                       | :   A style of        |                       |
|                       |     program design in |                       |
|                       |     which the         |                       |
|                       |     majority of       |                       |
|                       |     functions are     |                       |
|                       |     pure.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1453} |                       |
|                       |                       |                       |
|                       | [invariant:]{.c010}   |                       |
|                       | :   A condition that  |                       |
|                       |     should always be  |                       |
|                       |     true during the   |                       |
|                       |     execution of a    |                       |
|                       |     program.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1454} |                       |
|                       |                       |                       |
|                       | [asse                 |                       |
|                       | rt statement:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     checks a          |                       |
|                       |     condition and     |                       |
|                       |     raises an         |                       |
|                       |     exception if it   |                       |
|                       |     fails.            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1455} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1456} |                       |
|                       |                       |                       |
|                       | ## 16.7  Exercis      |                       |
|                       | es {#sec194 .section} |                       |
|                       |                       |                       |
|                       | Code examples from    |                       |
|                       | this chapter are      |                       |
|                       | available from        |                       |
|                       | [[ht                  |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/Time1.py]{.c004 |                       |
|                       | }](https://thinkpytho |                       |
|                       | n.com/code/Time1.py); |                       |
|                       | solutions to the      |                       |
|                       | exercises are         |                       |
|                       | available from        |                       |
|                       | [[https://thin        |                       |
|                       | kpython.com/code/Time |                       |
|                       | 1_soln.py]{.c004}](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/Time1_soln.py). |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `mul_time`     |                       |
|                       | that takes a Time     |                       |
|                       | object and a number   |                       |
|                       | and returns a new     |                       |
|                       | Time object that      |                       |
|                       | contains the product  |                       |
|                       | of the original Time  |                       |
|                       | and the number.*      |                       |
|                       |                       |                       |
|                       | *Then use `mul_time`  |                       |
|                       | to write a function   |                       |
|                       | that takes a Time     |                       |
|                       | object that           |                       |
|                       | represents the        |                       |
|                       | finishing time in a   |                       |
|                       | race, and a number    |                       |
|                       | that represents the   |                       |
|                       | distance, and returns |                       |
|                       | a Time object that    |                       |
|                       | represents the        |                       |
|                       | average pace (time    |                       |
|                       | per mile).*           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1457} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1458} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1459} |                       |
|                       |                       |                       |
|                       | *The                  |                       |
|                       | [datetime]{.c004}     |                       |
|                       | module provides       |                       |
|                       | [time]{.c004} objects |                       |
|                       | that are similar to   |                       |
|                       | the Time objects in   |                       |
|                       | this chapter, but     |                       |
|                       | they provide a rich   |                       |
|                       | set of methods and    |                       |
|                       | operators. Read the   |                       |
|                       | documentation at*     |                       |
|                       | [[*ht                 |                       |
|                       | tp://docs.python.org/ |                       |
|                       | 3/library/datetime.ht |                       |
|                       | ml*]{.c004}](http://d |                       |
|                       | ocs.python.org/3/libr |                       |
|                       | ary/datetime.html)*.* |                       |
|                       |                       |                       |
|                       | 1.  *Use the          |                       |
|                       |     [datetime]{.c004} |                       |
|                       |     module to write a |                       |
|                       |     program that gets |                       |
|                       |     the current date  |                       |
|                       |     and prints the    |                       |
|                       |     day of the week.* |                       |
|                       | 2.  *Write a program  |                       |
|                       |     that takes a      |                       |
|                       |     birthday as input |                       |
|                       |     and prints the    |                       |
|                       |     user's age and    |                       |
|                       |     the number of     |                       |
|                       |     days, hours,      |                       |
|                       |     minutes and       |                       |
|                       |     seconds until     |                       |
|                       |     their next        |                       |
|                       |     birthday.*        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1460} |                       |
|                       | 3.  *For two people   |                       |
|                       |     born on different |                       |
|                       |     days, there is a  |                       |
|                       |     day when one is   |                       |
|                       |     twice as old as   |                       |
|                       |     the other. That's |                       |
|                       |     their Double Day. |                       |
|                       |     Write a program   |                       |
|                       |     that takes two    |                       |
|                       |     birth dates and   |                       |
|                       |     computes their    |                       |
|                       |     Double Day.*      |                       |
|                       | 4.  *For a little     |                       |
|                       |     more challenge,   |                       |
|                       |     write the more    |                       |
|                       |     general version   |                       |
|                       |     that computes the |                       |
|                       |     day when one      |                       |
|                       |     person is*        |                       |
|                       |     [n]{.c009} *times |                       |
|                       |     older than the    |                       |
|                       |     other.*           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1461} |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[http               |                       |
|                       | s://thinkpython.com/c |                       |
|                       | ode/double.py]{.c004} |                       |
|                       | *](https://thinkpytho |                       |
|                       | n.com/code/double.py) |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2016.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2018.html)
---
generator: hevea 2.32
title: Classes and methods
---

[![Previous](back.png)](thinkpython2017.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2019.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter             | to support my books,  |
|                       | 17  Classes and metho | you can use the       |
|                       | ds {#sec195 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | Although we are using | you!                  |
|                       | some of Python's      |                       |
|                       | object-oriented       |   -----------         |
|                       | features, the         | --------------------- |
|                       | programs from the     | --------------------- |
|                       | last two chapters are | --------------------- |
|                       | not really            | --------------------- |
|                       | object-oriented       |   Pay what you want:  |
|                       | because they don't    |   Small \$1           |
|                       | represent the         | .00 USD Medium \$5.00 |
|                       | relationships between |  USD Large \$10.00 US |
|                       | programmer-defined    | D X-Large \$20.00 USD |
|                       | types and the         |  XX-Large \$50.00 USD |
|                       | functions that        |   -----------         |
|                       | operate on them. The  | --------------------- |
|                       | next step is to       | --------------------- |
|                       | transform those       | --------------------- |
|                       | functions into        | --------------------- |
|                       | methods that make the |                       |
|                       | relationships         | ![](                  |
|                       | explicit.             | https://www.paypalobj |
|                       |                       | ects.com/en_US/i/scr/ |
|                       | Code examples from    | pixel.gif){border="0" |
|                       | this chapter are      | width="1" height="1"} |
|                       | available from        |                       |
|                       | [[ht                  | ####                  |
|                       | tps://thinkpython.com | Are you using one of  |
|                       | /code/Time2.py]{.c004 | our books in a class? |
|                       | }](https://thinkpytho |                       |
|                       | n.com/code/Time2.py), | We\'d like to know    |
|                       | and solutions to the  | about it. Please      |
|                       | exercises are in      | consider filling out  |
|                       | [[https://thinkp      | [this short           |
|                       | ython.com/code/Point2 | survey](http://s      |
|                       | _soln.py]{.c004}](htt | preadsheets.google.co |
|                       | ps://thinkpython.com/ | m/viewform?formkey=dC |
|                       | code/Point2_soln.py). | 0tNUZkMjBEdXVoRGljNm9 |
|                       |                       | FRmlTMHc6MA){onclick= |
|                       | ## 17.1  O            | "javascript: pageTrac |
|                       | bject-oriented featur | ker._trackPageview('/ |
|                       | es {#sec196 .section} | outbound/survey');"}. |
|                       |                       |                       |
|                       | [                     | \                     |
|                       | ]{#hevea_default1462} |                       |
|                       |                       | [Think                |
|                       | Python is an          | DSP](http             |
|                       | [object-oriented      | ://www.amazon.com/gp/ |
|                       | programming           | product/1491938455/re |
|                       | language]{.c010},     | f=as_li_tl?ie=UTF8&ca |
|                       | which means that it   | mp=1789&creative=9325 |
|                       | provides features     | &creativeASIN=1491938 |
|                       | that support          | 455&linkCode=as2&tag= |
|                       | object-oriented       | greenteapre01-20&link |
|                       | programming, which    | Id=2JJH4SWCAVVYSQHO){ |
|                       | has these defining    | rel="nofollow"}![](ht |
|                       | characteristics:      | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | -   Programs include  | nteapre01-20&l=as2&o= |
|                       |     class and method  | 1&a=1491938455){.c003 |
|                       |     definitions.      | width="1" height="1"  |
|                       | -   Most of the       | border="0"}           |
|                       |     computation is    |                       |
|                       |     expressed in      | [                     |
|                       |     terms of          | ![](http://ws-na.amaz |
|                       |     operations on     | on-adsystem.com/widge |
|                       |     objects.          | ts/q?_encoding=UTF8&A |
|                       | -   Objects often     | SIN=1491938455&Format |
|                       |     represent things  | =_SL160_&ID=AsinImage |
|                       |     in the real       | &MarketPlace=US&Servi |
|                       |     world, and        | ceVersion=20070822&WS |
|                       |     methods often     | =1&tag=greenteapre01- |
|                       |     correspond to the | 20){border="0"}](http |
|                       |     ways things in    | ://www.amazon.com/gp/ |
|                       |     the real world    | product/1491938455/re |
|                       |     interact.         | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | For example, the      | &creativeASIN=1491938 |
|                       | [Time]{.c004} class   | 455&linkCode=as2&tag= |
|                       | defined in            | greenteapre01-20&link |
|                       | Chapter [16](think    | Id=CTV7PDT7E5EGGJUM){ |
|                       | python2017.html#time) | rel="nofollow"}![](ht |
|                       | corresponds to the    | tp://ir-na.amazon-ads |
|                       | way people record the | ystem.com/e/ir?t=gree |
|                       | time of day, and the  | nteapre01-20&l=as2&o= |
|                       | functions we defined  | 1&a=1491938455){.c003 |
|                       | correspond to the     | width="1" height="1"  |
|                       | kinds of things       | border="0"}           |
|                       | people do with times. |                       |
|                       | Similarly, the        | [Think                |
|                       | [Point]{.c004} and    | Java](http            |
|                       | [Rectangle]{.c004}    | ://www.amazon.com/gp/ |
|                       | classes in            | product/1491929561/re |
|                       | Ch                    | f=as_li_tl?ie=UTF8&ca |
|                       | apter [15](thinkpytho | mp=1789&creative=9325 |
|                       | n2016.html#clobjects) | &creativeASIN=1491929 |
|                       | correspond to the     | 561&linkCode=as2&tag= |
|                       | mathematical concepts | greenteapre01-20&link |
|                       | of a point and a      | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | rectangle.            | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | So far, we have not   | ystem.com/e/ir?t=gree |
|                       | taken advantage of    | nteapre01-20&l=as2&o= |
|                       | the features Python   | 1&a=1491929561){.c003 |
|                       | provides to support   | width="1" height="1"  |
|                       | object-oriented       | border="0"}           |
|                       | programming. These    |                       |
|                       | features are not      | [                     |
|                       | strictly necessary;   | ![](http://ws-na.amaz |
|                       | most of them provide  | on-adsystem.com/widge |
|                       | alternative syntax    | ts/q?_encoding=UTF8&A |
|                       | for things we have    | SIN=1491929561&Format |
|                       | already done. But in  | =_SL160_&ID=AsinImage |
|                       | many cases, the       | &MarketPlace=US&Servi |
|                       | alternative is more   | ceVersion=20070822&WS |
|                       | concise and more      | =1&tag=greenteapre01- |
|                       | accurately conveys    | 20){border="0"}](http |
|                       | the structure of the  | ://www.amazon.com/gp/ |
|                       | program.              | product/1491929561/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | For example, in       | mp=1789&creative=9325 |
|                       | [Time1.py]{.c004}     | &creativeASIN=1491929 |
|                       | there is no obvious   | 561&linkCode=as2&tag= |
|                       | connection between    | greenteapre01-20&link |
|                       | the class definition  | Id=PT77ANWARUNNU3UK){ |
|                       | and the function      | rel="nofollow"}![](ht |
|                       | definitions that      | tp://ir-na.amazon-ads |
|                       | follow. With some     | ystem.com/e/ir?t=gree |
|                       | examination, it is    | nteapre01-20&l=as2&o= |
|                       | apparent that every   | 1&a=1491929561){.c003 |
|                       | function takes at     | width="1" height="1"  |
|                       | least one             | border="0"}           |
|                       | [Time]{.c004} object  |                       |
|                       | as an argument.       | [Think                |
|                       | [                     | Bay                   |
|                       | ]{#hevea_default1463} | es](http://www.amazon |
|                       | [                     | .com/gp/product/14493 |
|                       | ]{#hevea_default1464} | 70780/ref=as_li_qf_sp |
|                       |                       | _asin_tl?ie=UTF8&camp |
|                       | This observation is   | =1789&creative=9325&c |
|                       | the motivation for    | reativeASIN=144937078 |
|                       | [methods]{.c010}; a   | 0&linkCode=as2&tag=gr |
|                       | method is a function  | eenteapre01-20)![](ht |
|                       | that is associated    | tp://ir-na.amazon-ads |
|                       | with a particular     | ystem.com/e/ir?t=gree |
|                       | class. We have seen   | nteapre01-20&l=as2&o= |
|                       | methods for strings,  | 1&a=1449370780){.c003 |
|                       | lists, dictionaries   | width="1" height="1"  |
|                       | and tuples. In this   | border="0"}           |
|                       | chapter, we will      |                       |
|                       | define methods for    | [![](http://ws        |
|                       | programmer-defined    | -na.amazon-adsystem.c |
|                       | types.                | om/widgets/q?_encodin |
|                       | [                     | g=UTF8&ASIN=144937078 |
|                       | ]{#hevea_default1465} | 0&Format=_SL160_&ID=A |
|                       | [                     | sinImage&MarketPlace= |
|                       | ]{#hevea_default1466} | US&ServiceVersion=200 |
|                       | [                     | 70822&WS=1&tag=greent |
|                       | ]{#hevea_default1467} | eapre01-20){border="0 |
|                       | [                     | "}](http://www.amazon |
|                       | ]{#hevea_default1468} | .com/gp/product/14493 |
|                       |                       | 70780/ref=as_li_qf_sp |
|                       | Methods are           | _asin_il?ie=UTF8&camp |
|                       | semantically the same | =1789&creative=9325&c |
|                       | as functions, but     | reativeASIN=144937078 |
|                       | there are two         | 0&linkCode=as2&tag=gr |
|                       | syntactic             | eenteapre01-20)![](ht |
|                       | differences:          | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | -   Methods are       | nteapre01-20&l=as2&o= |
|                       |     defined inside a  | 1&a=1449370780){.c003 |
|                       |     class definition  | width="1" height="1"  |
|                       |     in order to make  | border="0"}           |
|                       |     the relationship  |                       |
|                       |     between the class | [Think Python         |
|                       |     and the method    | 2e](http              |
|                       |     explicit.         | ://www.amazon.com/gp/ |
|                       | -   The syntax for    | product/1491939362/re |
|                       |     invoking a method | f=as_li_tl?ie=UTF8&ca |
|                       |     is different from | mp=1789&creative=9325 |
|                       |     the syntax for    | &creativeASIN=1491939 |
|                       |     calling a         | 362&linkCode=as2&tag= |
|                       |     function.         | greenteapre01-20&link |
|                       |                       | Id=FJKSQ3IHEMY2F2VA){ |
|                       | In the next few       | rel="nofollow"}![](ht |
|                       | sections, we will     | tp://ir-na.amazon-ads |
|                       | take the functions    | ystem.com/e/ir?t=gree |
|                       | from the previous two | nteapre01-20&l=as2&o= |
|                       | chapters and          | 1&a=1491939362){.c003 |
|                       | transform them into   | width="1" height="1"  |
|                       | methods. This         | border="0"}           |
|                       | transformation is     |                       |
|                       | purely mechanical;    | [                     |
|                       | you can do it by      | ![](http://ws-na.amaz |
|                       | following a sequence  | on-adsystem.com/widge |
|                       | of steps. If you are  | ts/q?_encoding=UTF8&A |
|                       | comfortable           | SIN=1491939362&Format |
|                       | converting from one   | =_SL160_&ID=AsinImage |
|                       | form to another, you  | &MarketPlace=US&Servi |
|                       | will be able to       | ceVersion=20070822&WS |
|                       | choose the best form  | =1&tag=greenteapre01- |
|                       | for whatever you are  | 20){border="0"}](http |
|                       | doing.                | ://www.amazon.com/gp/ |
|                       |                       | product/1491939362/re |
|                       | ##                    | f=as_li_tl?ie=UTF8&ca |
|                       |  17.2  Printing objec | mp=1789&creative=9325 |
|                       | ts {#sec197 .section} | &creativeASIN=1491939 |
|                       |                       | 362&linkCode=as2&tag= |
|                       | [                     | greenteapre01-20&link |
|                       | ]{#hevea_default1469} | Id=ZZ454DLQ3IXDHNHX){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | In                    | tp://ir-na.amazon-ads |
|                       | Chapter [16](thinkp   | ystem.com/e/ir?t=gree |
|                       | ython2017.html#time), | nteapre01-20&l=as2&o= |
|                       | we defined a class    | 1&a=1491939362){.c003 |
|                       | named [Time]{.c004}   | width="1" height="1"  |
|                       | and in                | border="0"}           |
|                       | Sec                   |                       |
|                       | tion [16.1](thinkpyth | [Think Stats          |
|                       | on2017.html#isafter), | 2e](http://ww         |
|                       | you wrote a function  | w.amazon.com/gp/produ |
|                       | named `print_time`:   | ct/1491907339/ref=as_ |
|                       |                       | li_tl?ie=UTF8&camp=17 |
|                       | ``` verbatim          | 89&creative=9325&crea |
|                       | class Time:           | tiveASIN=1491907339&l |
|                       |     """Represent      | inkCode=as2&tag=green |
|                       | s the time of day.""" | teapre01-20&linkId=O7 |
|                       |                       | WYM6H6YBYUFNWU)![](ht |
|                       | def print_time(time): | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | print('%.2d:%.2d:%.2d | nteapre01-20&l=as2&o= |
|                       | ' % (time.hour, time. | 1&a=1491907339){.c003 |
|                       | minute, time.second)) | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | To call this          | [![](h                |
|                       | function, you have to | ttp://ws-na.amazon-ad |
|                       | pass a [Time]{.c004}  | system.com/widgets/q? |
|                       | object as an          | _encoding=UTF8&ASIN=1 |
|                       | argument:             | 491907339&Format=_SL1 |
|                       |                       | 60_&ID=AsinImage&Mark |
|                       | ``` verbatim          | etPlace=US&ServiceVer |
|                       | >>> start = Time()    | sion=20070822&WS=1&ta |
|                       | >>> start.hour = 9    | g=greenteapre01-20){b |
|                       | >>> start.minute = 45 | order="0"}](http://ww |
|                       | >>> start.second = 00 | w.amazon.com/gp/produ |
|                       | >>> print_time(start) | ct/1491907339/ref=as_ |
|                       | 09:45:00              | li_tl?ie=UTF8&camp=17 |
|                       | ```                   | 89&creative=9325&crea |
|                       |                       | tiveASIN=1491907339&l |
|                       | To make `print_time`  | inkCode=as2&tag=green |
|                       | a method, all we have | teapre01-20&linkId=JV |
|                       | to do is move the     | SYKQHYSUIEYRHL)![](ht |
|                       | function definition   | tp://ir-na.amazon-ads |
|                       | inside the class      | ystem.com/e/ir?t=gree |
|                       | definition. Notice    | nteapre01-20&l=as2&o= |
|                       | the change in         | 1&a=1491907339){.c003 |
|                       | indentation.          | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1470} |                       |
|                       |                       | [Think                |
|                       | ``` verbatim          | Complexity](http      |
|                       | class Time:           | ://www.amazon.com/gp/ |
|                       |                       | product/1449314635/re |
|                       | def print_time(time): | f=as_li_tf_tl?ie=UTF8 |
|                       |                       | &tag=greenteapre01-20 |
|                       | print('%.2d:%.2d:%.2d | &linkCode=as2&camp=17 |
|                       | ' % (time.hour, time. | 89&creative=9325&crea |
|                       | minute, time.second)) | tiveASIN=1449314635)! |
|                       | ```                   | [](http://www.assoc-a |
|                       |                       | mazon.com/e/ir?t=gree |
|                       | Now there are two     | nteapre01-20&l=as2&o= |
|                       | ways to call          | 1&a=1449314635){.c003 |
|                       | `print_time`. The     | width="1" height="1"  |
|                       | first (and less       | border="0"}           |
|                       | common) way is to use |                       |
|                       | function syntax:      | [                     |
|                       | [                     | ![](http://ws-na.amaz |
|                       | ]{#hevea_default1471} | on-adsystem.com/widge |
|                       | [                     | ts/q?_encoding=UTF8&A |
|                       | ]{#hevea_default1472} | SIN=1449314635&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | ``` verbatim          | &MarketPlace=US&Servi |
|                       | >>> T                 | ceVersion=20070822&WS |
|                       | ime.print_time(start) | =1&tag=greenteapre01- |
|                       | 09:45:00              | 20){border="0"}](http |
|                       | ```                   | ://www.amazon.com/gp/ |
|                       |                       | product/1449314635/re |
|                       | In this use of dot    | f=as_li_tf_il?ie=UTF8 |
|                       | notation,             | &camp=1789&creative=9 |
|                       | [Time]{.c004} is the  | 325&creativeASIN=1449 |
|                       | name of the class,    | 314635&linkCode=as2&t |
|                       | and `print_time` is   | ag=greenteapre01-20)! |
|                       | the name of the       | [](http://www.assoc-a |
|                       | method.               | mazon.com/e/ir?t=gree |
|                       | [start]{.c004} is     | nteapre01-20&l=as2&o= |
|                       | passed as a           | 1&a=1449314635){.c003 |
|                       | parameter.            | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The second (and more  |                       |
|                       | concise) way is to    |                       |
|                       | use method syntax:    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1473} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >                     |                       |
|                       | >> start.print_time() |                       |
|                       | 09:45:00              |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In this use of dot    |                       |
|                       | notation,             |                       |
|                       | `print_time` is the   |                       |
|                       | name of the method    |                       |
|                       | (again), and          |                       |
|                       | [start]{.c004} is the |                       |
|                       | object the method is  |                       |
|                       | invoked on, which is  |                       |
|                       | called the            |                       |
|                       | [subject]{.c010}.     |                       |
|                       | Just as the subject   |                       |
|                       | of a sentence is what |                       |
|                       | the sentence is       |                       |
|                       | about, the subject of |                       |
|                       | a method invocation   |                       |
|                       | is what the method is |                       |
|                       | about.                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1474} |                       |
|                       |                       |                       |
|                       | Inside the method,    |                       |
|                       | the subject is        |                       |
|                       | assigned to the first |                       |
|                       | parameter, so in this |                       |
|                       | case [start]{.c004}   |                       |
|                       | is assigned to        |                       |
|                       | [time]{.c004}.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1475} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1476} |                       |
|                       |                       |                       |
|                       | By convention, the    |                       |
|                       | first parameter of a  |                       |
|                       | method is called      |                       |
|                       | [self]{.c004}, so it  |                       |
|                       | would be more common  |                       |
|                       | to write `print_time` |                       |
|                       | like this:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | class Time:           |                       |
|                       |                       |                       |
|                       | def print_time(self): |                       |
|                       |                       |                       |
|                       | print('%.2d:%.2d:%.2d |                       |
|                       | ' % (self.hour, self. |                       |
|                       | minute, self.second)) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The reason for this   |                       |
|                       | convention is an      |                       |
|                       | implicit metaphor:    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1477} |                       |
|                       |                       |                       |
|                       | -   The syntax for a  |                       |
|                       |     function call,    |                       |
|                       |                       |                       |
|                       |  `print_time(start)`, |                       |
|                       |     suggests that the |                       |
|                       |     function is the   |                       |
|                       |     active agent. It  |                       |
|                       |     says something    |                       |
|                       |     like, "Hey        |                       |
|                       |     `print_time`!     |                       |
|                       |     Here's an object  |                       |
|                       |     for you to        |                       |
|                       |     print."           |                       |
|                       | -   In                |                       |
|                       |     object-oriented   |                       |
|                       |     programming, the  |                       |
|                       |     objects are the   |                       |
|                       |     active agents. A  |                       |
|                       |     method invocation |                       |
|                       |     like              |                       |
|                       |                       |                       |
|                       |  `start.print_time()` |                       |
|                       |     says "Hey         |                       |
|                       |     [start]{.c004}!   |                       |
|                       |     Please print      |                       |
|                       |     yourself."        |                       |
|                       |                       |                       |
|                       | This change in        |                       |
|                       | perspective might be  |                       |
|                       | more polite, but it   |                       |
|                       | is not obvious that   |                       |
|                       | it is useful. In the  |                       |
|                       | examples we have seen |                       |
|                       | so far, it may not    |                       |
|                       | be. But sometimes     |                       |
|                       | shifting              |                       |
|                       | responsibility from   |                       |
|                       | the functions onto    |                       |
|                       | the objects makes it  |                       |
|                       | possible to write     |                       |
|                       | more versatile        |                       |
|                       | functions (or         |                       |
|                       | methods), and makes   |                       |
|                       | it easier to maintain |                       |
|                       | and reuse code.       |                       |
|                       |                       |                       |
|                       | As an exercise,       |                       |
|                       | rewrite `time_to_int` |                       |
|                       | (from                 |                       |
|                       | Secti                 |                       |
|                       | on [16.4](thinkpython |                       |
|                       | 2017.html#prototype)) |                       |
|                       | as a method. You      |                       |
|                       | might be tempted to   |                       |
|                       | rewrite `int_to_time` |                       |
|                       | as a method, too, but |                       |
|                       | that doesn't really   |                       |
|                       | make sense because    |                       |
|                       | there would be no     |                       |
|                       | object to invoke it   |                       |
|                       | on.                   |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 17.3  Another examp |                       |
|                       | le {#sec198 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1478} |                       |
|                       |                       |                       |
|                       | Here's a version of   |                       |
|                       | [increment]{.c004}    |                       |
|                       | (from                 |                       |
|                       | Secti                 |                       |
|                       | on [16.3](thinkpython |                       |
|                       | 2017.html#increment)) |                       |
|                       | rewritten as a        |                       |
|                       | method:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | # inside class Time:  |                       |
|                       |                       |                       |
|                       |     def incr          |                       |
|                       | ement(self, seconds): |                       |
|                       |         seconds       |                       |
|                       | += self.time_to_int() |                       |
|                       |         return        |                       |
|                       |  int_to_time(seconds) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This version assumes  |                       |
|                       | that `time_to_int` is |                       |
|                       | written as a method.  |                       |
|                       | Also, note that it is |                       |
|                       | a pure function, not  |                       |
|                       | a modifier.           |                       |
|                       |                       |                       |
|                       | Here's how you would  |                       |
|                       | invoke                |                       |
|       