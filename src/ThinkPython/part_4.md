           | 2                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | By default,           |                       |
|                       | [find]{.c004} starts  |                       |
|                       | at the beginning of   |                       |
|                       | the string, but it    |                       |
|                       | can take a second     |                       |
|                       | argument, the index   |                       |
|                       | where it should       |                       |
|                       | start:                |                       |
|                       | []{#hevea_default603} |                       |
|                       | []{#hevea_default604} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >                     |                       |
|                       | >> word.find('na', 3) |                       |
|                       | 4                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This is an example of |                       |
|                       | an [optional          |                       |
|                       | argument]{.c010};     |                       |
|                       | [find]{.c004} can     |                       |
|                       | also take a third     |                       |
|                       | argument, the index   |                       |
|                       | where it should stop: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> name = 'bob'      |                       |
|                       | >>>                   |                       |
|                       |  name.find('b', 1, 2) |                       |
|                       | -1                    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This search fails     |                       |
|                       | because [b]{.c004}    |                       |
|                       | does not appear in    |                       |
|                       | the index range from  |                       |
|                       | [1]{.c004} to         |                       |
|                       | [2]{.c004}, not       |                       |
|                       | including [2]{.c004}. |                       |
|                       | Searching up to, but  |                       |
|                       | not including, the    |                       |
|                       | second index makes    |                       |
|                       | [find]{.c004}         |                       |
|                       | consistent with the   |                       |
|                       | slice operator.       |                       |
|                       |                       |                       |
|                       | ## 8.9  T             |                       |
|                       | he [in]{.c004} operat |                       |
|                       | or {#sec100 .section} |                       |
|                       |                       |                       |
|                       | []{#inboth}           |                       |
|                       | []{#hevea_default605} |                       |
|                       | []{#hevea_default606} |                       |
|                       | []{#hevea_default607} |                       |
|                       | []{#hevea_default608} |                       |
|                       |                       |                       |
|                       | The word [in]{.c004}  |                       |
|                       | is a boolean operator |                       |
|                       | that takes two        |                       |
|                       | strings and returns   |                       |
|                       | [True]{.c004} if the  |                       |
|                       | first appears as a    |                       |
|                       | substring in the      |                       |
|                       | second:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> 'a' in 'banana'   |                       |
|                       | True                  |                       |
|                       | >                     |                       |
|                       | >> 'seed' in 'banana' |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | For example, the      |                       |
|                       | following function    |                       |
|                       | prints all the        |                       |
|                       | letters from          |                       |
|                       | [word1]{.c004} that   |                       |
|                       | also appear in        |                       |
|                       | [word2]{.c004}:       |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def i                 |                       |
|                       | n_both(word1, word2): |                       |
|                       |                       |                       |
|                       |  for letter in word1: |                       |
|                       |                       |                       |
|                       |   if letter in word2: |                       |
|                       |                       |                       |
|                       |         print(letter) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | With well-chosen      |                       |
|                       | variable names,       |                       |
|                       | Python sometimes      |                       |
|                       | reads like English.   |                       |
|                       | You could read this   |                       |
|                       | loop, "for (each)     |                       |
|                       | letter in (the first) |                       |
|                       | word, if (the) letter |                       |
|                       | (appears) in (the     |                       |
|                       | second) word, print   |                       |
|                       | (the) letter."        |                       |
|                       |                       |                       |
|                       | Here's what you get   |                       |
|                       | if you compare apples |                       |
|                       | and oranges:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> in_both           |                       |
|                       | ('apples', 'oranges') |                       |
|                       | a                     |                       |
|                       | e                     |                       |
|                       | s                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 8.10  String comparis |                       |
|                       | on {#sec101 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default609} |                       |
|                       | []{#hevea_default610} |                       |
|                       |                       |                       |
|                       | The relational        |                       |
|                       | operators work on     |                       |
|                       | strings. To see if    |                       |
|                       | two strings are       |                       |
|                       | equal:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if word == 'banana':  |                       |
|                       |     print('           |                       |
|                       | All right, bananas.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Other relational      |                       |
|                       | operations are useful |                       |
|                       | for putting words in  |                       |
|                       | alphabetical order:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | if word < 'banana':   |                       |
|                       |     print('Your       |                       |
|                       | word, ' + word + ', c |                       |
|                       | omes before banana.') |                       |
|                       | elif word > 'banana': |                       |
|                       |     print('Your       |                       |
|                       |  word, ' + word + ',  |                       |
|                       | comes after banana.') |                       |
|                       | else:                 |                       |
|                       |     print('           |                       |
|                       | All right, bananas.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Python does not       |                       |
|                       | handle uppercase and  |                       |
|                       | lowercase letters the |                       |
|                       | same way people do.   |                       |
|                       | All the uppercase     |                       |
|                       | letters come before   |                       |
|                       | all the lowercase     |                       |
|                       | letters, so:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Your word, Pineapple, |                       |
|                       |  comes before banana. |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A common way to       |                       |
|                       | address this problem  |                       |
|                       | is to convert strings |                       |
|                       | to a standard format, |                       |
|                       | such as all           |                       |
|                       | lowercase, before     |                       |
|                       | performing the        |                       |
|                       | comparison. Keep that |                       |
|                       | in mind in case you   |                       |
|                       | have to defend        |                       |
|                       | yourself against a    |                       |
|                       | man armed with a      |                       |
|                       | Pineapple.            |                       |
|                       |                       |                       |
|                       | ## 8.11  Debuggi      |                       |
|                       | ng {#sec102 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default611} |                       |
|                       | []{#hevea_default612} |                       |
|                       |                       |                       |
|                       | When you use indices  |                       |
|                       | to traverse the       |                       |
|                       | values in a sequence, |                       |
|                       | it is tricky to get   |                       |
|                       | the beginning and end |                       |
|                       | of the traversal      |                       |
|                       | right. Here is a      |                       |
|                       | function that is      |                       |
|                       | supposed to compare   |                       |
|                       | two words and return  |                       |
|                       | [True]{.c004} if one  |                       |
|                       | of the words is the   |                       |
|                       | reverse of the other, |                       |
|                       | but it contains two   |                       |
|                       | errors:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def is_r              |                       |
|                       | everse(word1, word2): |                       |
|                       |     if len(           |                       |
|                       | word1) != len(word2): |                       |
|                       |         return False  |                       |
|                       |                       |                       |
|                       |     i = 0             |                       |
|                       |     j = len(word2)    |                       |
|                       |                       |                       |
|                       |     while j > 0:      |                       |
|                       |         if            |                       |
|                       | word1[i] != word2[j]: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |         i = i+1       |                       |
|                       |         j = j-1       |                       |
|                       |                       |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first [if]{.c004} |                       |
|                       | statement checks      |                       |
|                       | whether the words are |                       |
|                       | the same length. If   |                       |
|                       | not, we can return    |                       |
|                       | [False]{.c004}        |                       |
|                       | immediately.          |                       |
|                       | Otherwise, for the    |                       |
|                       | rest of the function, |                       |
|                       | we can assume that    |                       |
|                       | the words are the     |                       |
|                       | same length. This is  |                       |
|                       | an example of the     |                       |
|                       | guardian pattern in   |                       |
|                       | Sec                   |                       |
|                       | tion [6.8](thinkpytho |                       |
|                       | n2007.html#guardian). |                       |
|                       | []{#hevea_default613} |                       |
|                       | []{#hevea_default614} |                       |
|                       | []{#hevea_default615} |                       |
|                       |                       |                       |
|                       | [i]{.c004} and        |                       |
|                       | [j]{.c004} are        |                       |
|                       | indices: [i]{.c004}   |                       |
|                       | traverses             |                       |
|                       | [word1]{.c004}        |                       |
|                       | forward while         |                       |
|                       | [j]{.c004} traverses  |                       |
|                       | [word2]{.c004}        |                       |
|                       | backward. If we find  |                       |
|                       | two letters that      |                       |
|                       | don't match, we can   |                       |
|                       | return [False]{.c004} |                       |
|                       | immediately. If we    |                       |
|                       | get through the whole |                       |
|                       | loop and all the      |                       |
|                       | letters match, we     |                       |
|                       | return [True]{.c004}. |                       |
|                       |                       |                       |
|                       | If we test this       |                       |
|                       | function with the     |                       |
|                       | words "pots" and      |                       |
|                       | "stop", we expect the |                       |
|                       | return value          |                       |
|                       | [True]{.c004}, but we |                       |
|                       | get an IndexError:    |                       |
|                       | []{#hevea_default616} |                       |
|                       | []{#hevea_default617} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> is_re             |                       |
|                       | verse('pots', 'stop') |                       |
|                       | ...                   |                       |
|                       |                       |                       |
|                       |  File "reverse.py", l |                       |
|                       | ine 15, in is_reverse |                       |
|                       |     if                |                       |
|                       | word1[i] != word2[j]: |                       |
|                       | IndexError: stri      |                       |
|                       | ng index out of range |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | For debugging this    |                       |
|                       | kind of error, my     |                       |
|                       | first move is to      |                       |
|                       | print the values of   |                       |
|                       | the indices           |                       |
|                       | immediately before    |                       |
|                       | the line where the    |                       |
|                       | error appears.        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |     while j > 0:      |                       |
|                       |         print(i, j    |                       |
|                       | )        # print here |                       |
|                       |                       |                       |
|                       |         if            |                       |
|                       | word1[i] != word2[j]: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |         i = i+1       |                       |
|                       |         j = j-1       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Now when I run the    |                       |
|                       | program again, I get  |                       |
|                       | more information:     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> is_re             |                       |
|                       | verse('pots', 'stop') |                       |
|                       | 0 4                   |                       |
|                       | ...                   |                       |
|                       | IndexError: stri      |                       |
|                       | ng index out of range |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first time        |                       |
|                       | through the loop, the |                       |
|                       | value of [j]{.c004}   |                       |
|                       | is 4, which is out of |                       |
|                       | range for the string  |                       |
|                       | `'pots'`. The index   |                       |
|                       | of the last character |                       |
|                       | is 3, so the initial  |                       |
|                       | value for [j]{.c004}  |                       |
|                       | should be             |                       |
|                       | [                     |                       |
|                       | len(word2)-1]{.c004}. |                       |
|                       |                       |                       |
|                       | If I fix that error   |                       |
|                       | and run the program   |                       |
|                       | again, I get:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> is_re             |                       |
|                       | verse('pots', 'stop') |                       |
|                       | 0 3                   |                       |
|                       | 1 2                   |                       |
|                       | 2 1                   |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This time we get the  |                       |
|                       | right answer, but it  |                       |
|                       | looks like the loop   |                       |
|                       | only ran three times, |                       |
|                       | which is suspicious.  |                       |
|                       | To get a better idea  |                       |
|                       | of what is happening, |                       |
|                       | it is useful to draw  |                       |
|                       | a state diagram.      |                       |
|                       | During the first      |                       |
|                       | iteration, the frame  |                       |
|                       | for `is_reverse` is   |                       |
|                       | shown in              |                       |
|                       | Figur                 |                       |
|                       | e [8.2](#fig.state4). |                       |
|                       | []{#hevea_default618} |                       |
|                       | []{#hevea_default619} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2010.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | >   Figur             |                       |
|                       | e 8.2: State diagram. |                       |
|                       | >   -------           |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.state4}     |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | I took some license   |                       |
|                       | by arranging the      |                       |
|                       | variables in the      |                       |
|                       | frame and adding      |                       |
|                       | dotted lines to show  |                       |
|                       | that the values of    |                       |
|                       | [i]{.c004} and        |                       |
|                       | [j]{.c004} indicate   |                       |
|                       | characters in         |                       |
|                       | [word1]{.c004} and    |                       |
|                       | [word2]{.c004}.       |                       |
|                       |                       |                       |
|                       | Starting with this    |                       |
|                       | diagram, run the      |                       |
|                       | program on paper,     |                       |
|                       | changing the values   |                       |
|                       | of [i]{.c004} and     |                       |
|                       | [j]{.c004} during     |                       |
|                       | each iteration. Find  |                       |
|                       | and fix the second    |                       |
|                       | error in this         |                       |
|                       | function.             |                       |
|                       | []{#isreverse}        |                       |
|                       |                       |                       |
|                       | ## 8.12  Glossa       |                       |
|                       | ry {#sec103 .section} |                       |
|                       |                       |                       |
|                       | [object:]{.c010}      |                       |
|                       | :   Something a       |                       |
|                       |     variable can      |                       |
|                       |     refer to. For     |                       |
|                       |     now, you can use  |                       |
|                       |     "object" and      |                       |
|                       |     "value"           |                       |
|                       |     interchangeably.  |                       |
|                       |                       |                       |
|                       | []{#hevea_default620} |                       |
|                       |                       |                       |
|                       | [sequence:]{.c010}    |                       |
|                       | :   An ordered        |                       |
|                       |     collection of     |                       |
|                       |     values where each |                       |
|                       |     value is          |                       |
|                       |     identified by an  |                       |
|                       |     integer index.    |                       |
|                       |                       |                       |
|                       | []{#hevea_default621} |                       |
|                       |                       |                       |
|                       | [item:]{.c010}        |                       |
|                       | :   One of the values |                       |
|                       |     in a sequence.    |                       |
|                       |                       |                       |
|                       | []{#hevea_default622} |                       |
|                       |                       |                       |
|                       | [index:]{.c010}       |                       |
|                       | :   An integer value  |                       |
|                       |     used to select an |                       |
|                       |     item in a         |                       |
|                       |     sequence, such as |                       |
|                       |     a character in a  |                       |
|                       |     string. In Python |                       |
|                       |     indices start     |                       |
|                       |     from 0.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default623} |                       |
|                       |                       |                       |
|                       | [slice:]{.c010}       |                       |
|                       | :   A part of a       |                       |
|                       |     string specified  |                       |
|                       |     by a range of     |                       |
|                       |     indices.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default624} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | empty string:]{.c010} |                       |
|                       | :   A string with no  |                       |
|                       |     characters and    |                       |
|                       |     length 0,         |                       |
|                       |     represented by    |                       |
|                       |     two quotation     |                       |
|                       |     marks.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default625} |                       |
|                       |                       |                       |
|                       | [immutable:]{.c010}   |                       |
|                       | :   The property of a |                       |
|                       |     sequence whose    |                       |
|                       |     items cannot be   |                       |
|                       |     changed.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default626} |                       |
|                       |                       |                       |
|                       | [traverse:]{.c010}    |                       |
|                       | :   To iterate        |                       |
|                       |     through the items |                       |
|                       |     in a sequence,    |                       |
|                       |     performing a      |                       |
|                       |     similar operation |                       |
|                       |     on each.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default627} |                       |
|                       |                       |                       |
|                       | [search:]{.c010}      |                       |
|                       | :   A pattern of      |                       |
|                       |     traversal that    |                       |
|                       |     stops when it     |                       |
|                       |     finds what it is  |                       |
|                       |     looking for.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default628} |                       |
|                       |                       |                       |
|                       | []{#hevea_default629} |                       |
|                       |                       |                       |
|                       | [counter:]{.c010}     |                       |
|                       | :   A variable used   |                       |
|                       |     to count          |                       |
|                       |     something,        |                       |
|                       |     usually           |                       |
|                       |     initialized to    |                       |
|                       |     zero and then     |                       |
|                       |     incremented.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default630} |                       |
|                       |                       |                       |
|                       | [invocation:]{.c010}  |                       |
|                       | :   A statement that  |                       |
|                       |     calls a method.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default631} |                       |
|                       |                       |                       |
|                       | [optio                |                       |
|                       | nal argument:]{.c010} |                       |
|                       | :   A function or     |                       |
|                       |     method argument   |                       |
|                       |     that is not       |                       |
|                       |     required.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default632} |                       |
|                       |                       |                       |
|                       | []{#hevea_default633} |                       |
|                       |                       |                       |
|                       | ## 8.13  Exercis      |                       |
|                       | es {#sec104 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       | []{#hevea_default634} |                       |
|                       | []{#hevea_default635} |                       |
|                       |                       |                       |
|                       | *Read the             |                       |
|                       | documentation of the  |                       |
|                       | string methods at*    |                       |
|                       | [[*http://doc         |                       |
|                       | s.python.org/3/librar |                       |
|                       | y/stdtypes.html#strin |                       |
|                       | g-methods*]{.c004}](h |                       |
|                       | ttp://docs.python.org |                       |
|                       | /3/library/stdtypes.h |                       |
|                       | tml#string-methods)*. |                       |
|                       | You might want to     |                       |
|                       | experiment with some  |                       |
|                       | of them to make sure  |                       |
|                       | you understand how    |                       |
|                       | they work.            |                       |
|                       | [strip]{.c004} and    |                       |
|                       | [replace]{.c004} are  |                       |
|                       | particularly useful.* |                       |
|                       |                       |                       |
|                       | *The documentation    |                       |
|                       | uses a syntax that    |                       |
|                       | might be confusing.   |                       |
|                       | For example, in       |                       |
|                       | `find(s               |                       |
|                       | ub[, start[, end]])`, |                       |
|                       | the brackets indicate |                       |
|                       | optional arguments.   |                       |
|                       | So [sub]{.c004} is    |                       |
|                       | required, but         |                       |
|                       | [start]{.c004} is     |                       |
|                       | optional, and if you  |                       |
|                       | include               |                       |
|                       | [start]{.c004}, then  |                       |
|                       | [end]{.c004} is       |                       |
|                       | optional.*            |                       |
|                       | []{#hevea_default636} |                       |
|                       | []{#hevea_default637} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#hevea_default638} |                       |
|                       | []{#hevea_default639} |                       |
|                       |                       |                       |
|                       | *There is a string    |                       |
|                       | method called         |                       |
|                       | [count]{.c004} that   |                       |
|                       | is similar to the     |                       |
|                       | function in           |                       |
|                       | Section               |                       |
|                       |  *[*8.7*](#counter)*. |                       |
|                       | Read the              |                       |
|                       | documentation of this |                       |
|                       | method and write an   |                       |
|                       | invocation that       |                       |
|                       | counts the number of  |                       |
|                       | [a]{.c004}'s in       |                       |
|                       | `'banana'`.*          |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       | []{#hevea_default640} |                       |
|                       | []{#hevea_default641} |                       |
|                       | []{#hevea_default642} |                       |
|                       |                       |                       |
|                       | *A string slice can   |                       |
|                       | take a third index    |                       |
|                       | that specifies the    |                       |
|                       | "step size"; that is, |                       |
|                       | the number of spaces  |                       |
|                       | between successive    |                       |
|                       | characters. A step    |                       |
|                       | size of 2 means every |                       |
|                       | other character; 3    |                       |
|                       | means every third,    |                       |
|                       | etc.*                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> fruit = 'banana'  |                       |
|                       | >>> fruit[0:5:2]      |                       |
|                       | 'bnn'                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *A step size of -1    |                       |
|                       | goes through the word |                       |
|                       | backwards, so the     |                       |
|                       | slice `[::-1]`        |                       |
|                       | generates a reversed  |                       |
|                       | string.*              |                       |
|                       | []{#hevea_default643} |                       |
|                       |                       |                       |
|                       | *Use this idiom to    |                       |
|                       | write a one-line      |                       |
|                       | version of            |                       |
|                       | `is_palindrome` from  |                       |
|                       | Exercise              |                       |
|                       | *[*3*](thinkpython200 |                       |
|                       | 7.html#palindrome)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 4]{.c010}   |                       |
|                       |                       |                       |
|                       | *The following        |                       |
|                       | functions are all*    |                       |
|                       | intended *to check    |                       |
|                       | whether a string      |                       |
|                       | contains any          |                       |
|                       | lowercase letters,    |                       |
|                       | but at least some of  |                       |
|                       | them are wrong. For   |                       |
|                       | each function,        |                       |
|                       | describe what the     |                       |
|                       | function actually     |                       |
|                       | does (assuming that   |                       |
|                       | the parameter is a    |                       |
|                       | string).*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef any_lowercase1(s): |                       |
|                       |     for c in s:       |                       |
|                       |                       |                       |
|                       |       if c.islower(): |                       |
|                       |                       |                       |
|                       |           return True |                       |
|                       |         else:         |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |                       |                       |
|                       | d                     |                       |
|                       | ef any_lowercase2(s): |                       |
|                       |     for c in s:       |                       |
|                       |                       |                       |
|                       |     if 'c'.islower(): |                       |
|                       |                       |                       |
|                       |         return 'True' |                       |
|                       |         else:         |                       |
|                       |                       |                       |
|                       |        return 'False' |                       |
|                       |                       |                       |
|                       | d                     |                       |
|                       | ef any_lowercase3(s): |                       |
|                       |     for c in s:       |                       |
|                       |                       |                       |
|                       |    flag = c.islower() |                       |
|                       |     return flag       |                       |
|                       |                       |                       |
|                       | d                     |                       |
|                       | ef any_lowercase4(s): |                       |
|                       |     flag = False      |                       |
|                       |     for c in s:       |                       |
|                       |         flag          |                       |
|                       | = flag or c.islower() |                       |
|                       |     return flag       |                       |
|                       |                       |                       |
|                       | d                     |                       |
|                       | ef any_lowercase5(s): |                       |
|                       |     for c in s:       |                       |
|                       |                       |                       |
|                       |   if not c.islower(): |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       | []{#hevea_default644} |                       |
|                       | []{#hevea_default645} |                       |
|                       |                       |                       |
|                       | []{#exrotate} *A      |                       |
|                       | Caesar cypher is a    |                       |
|                       | weak form of          |                       |
|                       | encryption that       |                       |
|                       | involves "rotating"   |                       |
|                       | each letter by a      |                       |
|                       | fixed number of       |                       |
|                       | places. To rotate a   |                       |
|                       | letter means to shift |                       |
|                       | it through the        |                       |
|                       | alphabet, wrapping    |                       |
|                       | around to the         |                       |
|                       | beginning if          |                       |
|                       | necessary, so 'A'     |                       |
|                       | rotated by 3 is 'D'   |                       |
|                       | and 'Z' rotated by 1  |                       |
|                       | is 'A'.*              |                       |
|                       |                       |                       |
|                       | *To rotate a word,    |                       |
|                       | rotate each letter by |                       |
|                       | the same amount. For  |                       |
|                       | example, "cheer"      |                       |
|                       | rotated by 7 is       |                       |
|                       | "jolly" and "melon"   |                       |
|                       | rotated by -10 is     |                       |
|                       | "cubed". In the       |                       |
|                       | movie* 2001: A Space  |                       |
|                       | Odyssey*, the ship    |                       |
|                       | computer is called    |                       |
|                       | HAL, which is IBM     |                       |
|                       | rotated by -1.*       |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `rotate_word`  |                       |
|                       | that takes a string   |                       |
|                       | and an integer as     |                       |
|                       | parameters, and       |                       |
|                       | returns a new string  |                       |
|                       | that contains the     |                       |
|                       | letters from the      |                       |
|                       | original string       |                       |
|                       | rotated by the given  |                       |
|                       | amount.*              |                       |
|                       |                       |                       |
|                       | *You might want to    |                       |
|                       | use the built-in      |                       |
|                       | function              |                       |
|                       | [ord]{.c004}, which   |                       |
|                       | converts a character  |                       |
|                       | to a numeric code,    |                       |
|                       | and [chr]{.c004},     |                       |
|                       | which converts        |                       |
|                       | numeric codes to      |                       |
|                       | characters. Letters   |                       |
|                       | of the alphabet are   |                       |
|                       | encoded in            |                       |
|                       | alphabetical order,   |                       |
|                       | so for example:*      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > ord('c') - ord('a') |                       |
|                       | 2                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *Because `'c'` is the |                       |
|                       | two-eth letter of the |                       |
|                       | alphabet. But beware: |                       |
|                       | the numeric codes for |                       |
|                       | upper case letters    |                       |
|                       | are different.*       |                       |
|                       |                       |                       |
|                       | *Potentially          |                       |
|                       | offensive jokes on    |                       |
|                       | the Internet are      |                       |
|                       | sometimes encoded in  |                       |
|                       | ROT13, which is a     |                       |
|                       | Caesar cypher with    |                       |
|                       | rotation 13. If you   |                       |
|                       | are not easily        |                       |
|                       | offended, find and    |                       |
|                       | decode some of them.  |                       |
|                       | Solution:*            |                       |
|                       | [*[https:/            |                       |
|                       | /thinkpython.com/code |                       |
|                       | /rotate.py]{.c004}*]( |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/rotate.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2008.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2010.html)
---
generator: hevea 2.32
title: "Case study: word play"
---

[![Previous](back.png)](thinkpython2009.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2011.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 9           | to support my books,  |
|                       |   Case study: word pl | you can use the       |
|                       | ay {#sec105 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | []{#wordplay}         | you!                  |
|                       |                       |                       |
|                       | This chapter presents |   -----------         |
|                       | the second case       | --------------------- |
|                       | study, which involves | --------------------- |
|                       | solving word puzzles  | --------------------- |
|                       | by searching for      | --------------------- |
|                       | words that have       |   Pay what you want:  |
|                       | certain properties.   |   Small \$1           |
|                       | For example, we'll    | .00 USD Medium \$5.00 |
|                       | find the longest      |  USD Large \$10.00 US |
|                       | palindromes in        | D X-Large \$20.00 USD |
|                       | English and search    |  XX-Large \$50.00 USD |
|                       | for words whose       |   -----------         |
|                       | letters appear in     | --------------------- |
|                       | alphabetical order.   | --------------------- |
|                       | And I will present    | --------------------- |
|                       | another program       | --------------------- |
|                       | development plan:     |                       |
|                       | reduction to a        | ![](                  |
|                       | previously solved     | https://www.paypalobj |
|                       | problem.              | ects.com/en_US/i/scr/ |
|                       |                       | pixel.gif){border="0" |
|                       | ##                    | width="1" height="1"} |
|                       | 9.1  Reading word lis |                       |
|                       | ts {#sec106 .section} | ####                  |
|                       |                       | Are you using one of  |
|                       | []{#wordlist}         | our books in a class? |
|                       |                       |                       |
|                       | For the exercises in  | We\'d like to know    |
|                       | this chapter we need  | about it. Please      |
|                       | a list of English     | consider filling out  |
|                       | words. There are lots | [this short           |
|                       | of word lists         | survey](http://s      |
|                       | available on the Web, | preadsheets.google.co |
|                       | but the one most      | m/viewform?formkey=dC |
|                       | suitable for our      | 0tNUZkMjBEdXVoRGljNm9 |
|                       | purpose is one of the | FRmlTMHc6MA){onclick= |
|                       | word lists collected  | "javascript: pageTrac |
|                       | and contributed to    | ker._trackPageview('/ |
|                       | the public domain by  | outbound/survey');"}. |
|                       | Grady Ward as part of |                       |
|                       | the Moby lexicon      | \                     |
|                       | project (see          |                       |
|                       | [[http:               | [Think                |
|                       | //wikipedia.org/wiki/ | DSP](http             |
|                       | Moby_Project]{.c004}] | ://www.amazon.com/gp/ |
|                       | (http://wikipedia.org | product/1491938455/re |
|                       | /wiki/Moby_Project)). | f=as_li_tl?ie=UTF8&ca |
|                       | It is a list of       | mp=1789&creative=9325 |
|                       | 113,809 official      | &creativeASIN=1491938 |
|                       | crosswords; that is,  | 455&linkCode=as2&tag= |
|                       | words that are        | greenteapre01-20&link |
|                       | considered valid in   | Id=2JJH4SWCAVVYSQHO){ |
|                       | crossword puzzles and | rel="nofollow"}![](ht |
|                       | other word games. In  | tp://ir-na.amazon-ads |
|                       | the Moby collection,  | ystem.com/e/ir?t=gree |
|                       | the filename is       | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491938455){.c003 |
|                       | 113809of.fic]{.c004}; | width="1" height="1"  |
|                       | you can download a    | border="0"}           |
|                       | copy, with the        |                       |
|                       | simpler name          | [                     |
|                       | [words.txt]{.c004},   | ![](http://ws-na.amaz |
|                       | from                  | on-adsystem.com/widge |
|                       | [[http                | ts/q?_encoding=UTF8&A |
|                       | s://thinkpython.com/c | SIN=1491938455&Format |
|                       | ode/words.txt]{.c004} | =_SL160_&ID=AsinImage |
|                       | ](https://thinkpython | &MarketPlace=US&Servi |
|                       | .com/code/words.txt). | ceVersion=20070822&WS |
|                       | []{#hevea_default646} | =1&tag=greenteapre01- |
|                       | []{#hevea_default647} | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | This file is in plain | product/1491938455/re |
|                       | text, so you can open | f=as_li_tl?ie=UTF8&ca |
|                       | it with a text        | mp=1789&creative=9325 |
|                       | editor, but you can   | &creativeASIN=1491938 |
|                       | also read it from     | 455&linkCode=as2&tag= |
|                       | Python. The built-in  | greenteapre01-20&link |
|                       | function              | Id=CTV7PDT7E5EGGJUM){ |
|                       | [open]{.c004} takes   | rel="nofollow"}![](ht |
|                       | the name of the file  | tp://ir-na.amazon-ads |
|                       | as a parameter and    | ystem.com/e/ir?t=gree |
|                       | returns a [file       | nteapre01-20&l=as2&o= |
|                       | object]{.c010} you    | 1&a=1491938455){.c003 |
|                       | can use to read the   | width="1" height="1"  |
|                       | file.                 | border="0"}           |
|                       | []{#hevea_default648} |                       |
|                       | []{#hevea_default649} | [Think                |
|                       | []{#hevea_default650} | Java](http            |
|                       | []{#hevea_default651} | ://www.amazon.com/gp/ |
|                       | []{#hevea_default652} | product/1491929561/re |
|                       | []{#hevea_default653} | f=as_li_tl?ie=UTF8&ca |
|                       |                       | mp=1789&creative=9325 |
|                       | ``` verbatim          | &creativeASIN=1491929 |
|                       | >>> fi                | 561&linkCode=as2&tag= |
|                       | n = open('words.txt') | greenteapre01-20&link |
|                       | ```                   | Id=ZY6MAYM33ZTNSCNZ){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | [fin]{.c004} is a     | tp://ir-na.amazon-ads |
|                       | common name for a     | ystem.com/e/ir?t=gree |
|                       | file object used for  | nteapre01-20&l=as2&o= |
|                       | input. The file       | 1&a=1491929561){.c003 |
|                       | object provides       | width="1" height="1"  |
|                       | several methods for   | border="0"}           |
|                       | reading, including    |                       |
|                       | [readline]{.c004},    | [                     |
|                       | which reads           | ![](http://ws-na.amaz |
|                       | characters from the   | on-adsystem.com/widge |
|                       | file until it gets to | ts/q?_encoding=UTF8&A |
|                       | a newline and returns | SIN=1491929561&Format |
|                       | the result as a       | =_SL160_&ID=AsinImage |
|                       | string:               | &MarketPlace=US&Servi |
|                       | []{#hevea_default654} | ceVersion=20070822&WS |
|                       | []{#hevea_default655} | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | ``` verbatim          | ://www.amazon.com/gp/ |
|                       | >>> fin.readline()    | product/1491929561/re |
|                       | 'aa\n'                | f=as_li_tl?ie=UTF8&ca |
|                       | ```                   | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491929 |
|                       | The first word in     | 561&linkCode=as2&tag= |
|                       | this particular list  | greenteapre01-20&link |
|                       | is "aa", which is a   | Id=PT77ANWARUNNU3UK){ |
|                       | kind of lava. The     | rel="nofollow"}![](ht |
|                       | sequence `\n`         | tp://ir-na.amazon-ads |
|                       | represents the        | ystem.com/e/ir?t=gree |
|                       | newline character     | nteapre01-20&l=as2&o= |
|                       | that separates this   | 1&a=1491929561){.c003 |
|                       | word from the next.   | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The file object keeps |                       |
|                       | track of where it is  | [Think                |
|                       | in the file, so if    | Bay                   |
|                       | you call              | es](http://www.amazon |
|                       | [readline]{.c004}     | .com/gp/product/14493 |
|                       | again, you get the    | 70780/ref=as_li_qf_sp |
|                       | next word:            | _asin_tl?ie=UTF8&camp |
|                       |                       | =1789&creative=9325&c |
|                       | ``` verbatim          | reativeASIN=144937078 |
|                       | >>> fin.readline()    | 0&linkCode=as2&tag=gr |
|                       | 'aah\n'               | eenteapre01-20)![](ht |
|                       | ```                   | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | The next word is      | nteapre01-20&l=as2&o= |
|                       | "aah", which is a     | 1&a=1449370780){.c003 |
|                       | perfectly legitimate  | width="1" height="1"  |
|                       | word, so stop looking | border="0"}           |
|                       | at me like that. Or,  |                       |
|                       | if it's the newline   | [![](http://ws        |
|                       | character that's      | -na.amazon-adsystem.c |
|                       | bothering you, we can | om/widgets/q?_encodin |
|                       | get rid of it with    | g=UTF8&ASIN=144937078 |
|                       | the string method     | 0&Format=_SL160_&ID=A |
|                       | [strip]{.c004}:       | sinImage&MarketPlace= |
|                       | []{#hevea_default656} | US&ServiceVersion=200 |
|                       | []{#hevea_default657} | 70822&WS=1&tag=greent |
|                       |                       | eapre01-20){border="0 |
|                       | ``` verbatim          | "}](http://www.amazon |
|                       | >>>                   | .com/gp/product/14493 |
|                       | line = fin.readline() | 70780/ref=as_li_qf_sp |
|                       | >>                    | _asin_il?ie=UTF8&camp |
|                       | > word = line.strip() | =1789&creative=9325&c |
|                       | >>> word              | reativeASIN=144937078 |
|                       | 'aahed'               | 0&linkCode=as2&tag=gr |
|                       | ```                   | eenteapre01-20)![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | You can also use a    | ystem.com/e/ir?t=gree |
|                       | file object as part   | nteapre01-20&l=as2&o= |
|                       | of a [for]{.c004}     | 1&a=1449370780){.c003 |
|                       | loop. This program    | width="1" height="1"  |
|                       | reads                 | border="0"}           |
|                       | [words.txt]{.c004}    |                       |
|                       | and prints each word, | [Think Python         |
|                       | one per line:         | 2e](http              |
|                       | []{#hevea_default658} | ://www.amazon.com/gp/ |
|                       | []{#hevea_default659} | product/1491939362/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | ``` verbatim          | mp=1789&creative=9325 |
|                       | fi                    | &creativeASIN=1491939 |
|                       | n = open('words.txt') | 362&linkCode=as2&tag= |
|                       | for line in fin:      | greenteapre01-20&link |
|                       |                       | Id=FJKSQ3IHEMY2F2VA){ |
|                       |   word = line.strip() | rel="nofollow"}![](ht |
|                       |     print(word)       | tp://ir-na.amazon-ads |
|                       | ```                   | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ## 9.2  Exercis       | 1&a=1491939362){.c003 |
|                       | es {#sec107 .section} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | There are solutions   |                       |
|                       | to these exercises in | [                     |
|                       | the next section. You | ![](http://ws-na.amaz |
|                       | should at least       | on-adsystem.com/widge |
|                       | attempt each one      | ts/q?_encoding=UTF8&A |
|                       | before you read the   | SIN=1491939362&Format |
|                       | solutions.            | =_SL160_&ID=AsinImage |
|                       |                       | &MarketPlace=US&Servi |
|                       | ::: theorem           | ceVersion=20070822&WS |
|                       | [Exercise 1]{.c010}   | =1&tag=greenteapre01- |
|                       | *Write a program that | 20){border="0"}](http |
|                       | reads                 | ://www.amazon.com/gp/ |
|                       | [words.txt]{.c004}    | product/1491939362/re |
|                       | and prints only the   | f=as_li_tl?ie=UTF8&ca |
|                       | words with more than  | mp=1789&creative=9325 |
|                       | 20 characters (not    | &creativeASIN=1491939 |
|                       | counting              | 362&linkCode=as2&tag= |
|                       | whitespace).*         | greenteapre01-20&link |
|                       | []{#hevea_default660} | Id=ZZ454DLQ3IXDHNHX){ |
|                       | :::                   | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | ::: theorem           | ystem.com/e/ir?t=gree |
|                       | [Exercise 2]{.c010}   | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | *In 1939 Ernest       | width="1" height="1"  |
|                       | Vincent Wright        | border="0"}           |
|                       | published a 50,000    |                       |
|                       | word novel called*    | [Think Stats          |
|                       | Gadsby *that does not | 2e](http://ww         |
|                       | contain the letter    | w.amazon.com/gp/produ |
|                       | "e". Since "e" is the | ct/1491907339/ref=as_ |
|                       | most common letter in | li_tl?ie=UTF8&camp=17 |
|                       | English, that's not   | 89&creative=9325&crea |
|                       | easy to do.*          | tiveASIN=1491907339&l |
|                       |                       | inkCode=as2&tag=green |
|                       | *In fact, it is       | teapre01-20&linkId=O7 |
|                       | difficult to          | WYM6H6YBYUFNWU)![](ht |
|                       | construct a solitary  | tp://ir-na.amazon-ads |
|                       | thought without using | ystem.com/e/ir?t=gree |
|                       | that most common      | nteapre01-20&l=as2&o= |
|                       | symbol. It is slow    | 1&a=1491907339){.c003 |
|                       | going at first, but   | width="1" height="1"  |
|                       | with caution and      | border="0"}           |
|                       | hours of training you |                       |
|                       | can gradually gain    | [![](h                |
|                       | facility.*            | ttp://ws-na.amazon-ad |
|                       |                       | system.com/widgets/q? |
|                       | *All right, I'll stop | _encoding=UTF8&ASIN=1 |
|                       | now.*                 | 491907339&Format=_SL1 |
|                       |                       | 60_&ID=AsinImage&Mark |
|                       | *Write a function     | etPlace=US&ServiceVer |
|                       | called `has_no_e`     | sion=20070822&WS=1&ta |
|                       | that returns          | g=greenteapre01-20){b |
|                       | [True]{.c004} if the  | order="0"}](http://ww |
|                       | given word doesn't    | w.amazon.com/gp/produ |
|                       | have the letter "e"   | ct/1491907339/ref=as_ |
|                       | in it.*               | li_tl?ie=UTF8&camp=17 |
|                       |                       | 89&creative=9325&crea |
|                       | *Write a program that | tiveASIN=1491907339&l |
|                       | reads                 | inkCode=as2&tag=green |
|                       | [words.txt]{.c004}    | teapre01-20&linkId=JV |
|                       | and prints only the   | SYKQHYSUIEYRHL)![](ht |
|                       | words that have no    | tp://ir-na.amazon-ads |
|                       | "e". Compute the      | ystem.com/e/ir?t=gree |
|                       | percentage of words   | nteapre01-20&l=as2&o= |
|                       | in the list that have | 1&a=1491907339){.c003 |
|                       | no "e".*              | width="1" height="1"  |
|                       | []{#hevea_default661} | border="0"}           |
|                       | :::                   |                       |
|                       |                       | [Think                |
|                       | ::: theorem           | Complexity](http      |
|                       | [Exercise 3]{.c010}   | ://www.amazon.com/gp/ |
|                       |                       | product/1449314635/re |
|                       | *Write a function     | f=as_li_tf_tl?ie=UTF8 |
|                       | named [avoids]{.c004} | &tag=greenteapre01-20 |
|                       | that takes a word and | &linkCode=as2&camp=17 |
|                       | a string of forbidden | 89&creative=9325&crea |
|                       | letters, and that     | tiveASIN=1449314635)! |
|                       | returns [True]{.c004} | [](http://www.assoc-a |
|                       | if the word doesn't   | mazon.com/e/ir?t=gree |
|                       | use any of the        | nteapre01-20&l=as2&o= |
|                       | forbidden letters.*   | 1&a=1449314635){.c003 |
|                       |                       | width="1" height="1"  |
|                       | *Write a program that | border="0"}           |
|                       | prompts the user to   |                       |
|                       | enter a string of     | [                     |
|                       | forbidden letters and | ![](http://ws-na.amaz |
|                       | then prints the       | on-adsystem.com/widge |
|                       | number of words that  | ts/q?_encoding=UTF8&A |
|                       | don't contain any of  | SIN=1449314635&Format |
|                       | them. Can you find a  | =_SL160_&ID=AsinImage |
|                       | combination of 5      | &MarketPlace=US&Servi |
|                       | forbidden letters     | ceVersion=20070822&WS |
|                       | that excludes the     | =1&tag=greenteapre01- |
|                       | smallest number of    | 20){border="0"}](http |
|                       | words?*               | ://www.amazon.com/gp/ |
|                       | :::                   | product/1449314635/re |
|                       |                       | f=as_li_tf_il?ie=UTF8 |
|                       | ::: theorem           | &camp=1789&creative=9 |
|                       | [Exercise 4]{.c010}   | 325&creativeASIN=1449 |
|                       |                       | 314635&linkCode=as2&t |
|                       | *Write a function     | ag=greenteapre01-20)! |
|                       | named `uses_only`     | [](http://www.assoc-a |
|                       | that takes a word and | mazon.com/e/ir?t=gree |
|                       | a string of letters,  | nteapre01-20&l=as2&o= |
|                       | and that returns      | 1&a=1449314635){.c003 |
|                       | [True]{.c004} if the  | width="1" height="1"  |
|                       | word contains only    | border="0"}           |
|                       | letters in the list.  |                       |
|                       | Can you make a        |                       |
|                       | sentence using only   |                       |
|                       | the letters           |                       |
|                       | [acefhlo]{.c004}?     |                       |
|                       | Other than "Hoe       |                       |
|                       | alfalfa"?*            |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named `uses_all` that |                       |
|                       | takes a word and a    |                       |
|                       | string of required    |                       |
|                       | letters, and that     |                       |
|                       | returns [True]{.c004} |                       |
|                       | if the word uses all  |                       |
|                       | the required letters  |                       |
|                       | at least once. How    |                       |
|                       | many words are there  |                       |
|                       | that use all the      |                       |
|                       | vowels                |                       |
|                       | [aeiou]{.c004}? How   |                       |
|                       | about                 |                       |
|                       | [aeiouy]{.c004}?*     |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 6]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called                |                       |
|                       | `is_abecedarian` that |                       |
|                       | returns [True]{.c004} |                       |
|                       | if the letters in a   |                       |
|                       | word appear in        |                       |
|                       | alphabetical order    |                       |
|                       | (double letters are   |                       |
|                       | ok). How many         |                       |
|                       | abecedarian words are |                       |
|                       | there?*               |                       |
|                       |                       |                       |
|                       | []{#hevea_default662} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ## 9.3  Sear          |                       |
|                       | ch {#sec108 .section} |                       |
|                       |                       |                       |
|                       | []{#search}           |                       |
|                       | []{#hevea_default663} |                       |
|                       | []{#hevea_default664} |                       |
|                       |                       |                       |
|                       | All of the exercises  |                       |
|                       | in the previous       |                       |
|                       | section have          |                       |
|                       | something in common;  |                       |
|                       | they can be solved    |                       |
|                       | with the search       |                       |
|                       | pattern we saw in     |                       |
|                       | Section [8.6](thinkp  |                       |
|                       | ython2009.html#find). |                       |
|                       | The simplest example  |                       |
|                       | is:                   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def has_no_e(word):   |                       |
|                       |                       |                       |
|                       |   for letter in word: |                       |
|                       |                       |                       |
|                       |     if letter == 'e': |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [for]{.c004} loop |                       |
|                       | traverses the         |                       |
|                       | characters in         |                       |
|                       | [word]{.c004}. If we  |                       |
|                       | find the letter "e",  |                       |
|                       | we can immediately    |                       |
|                       | return                |                       |
|                       | [False]{.c004};       |                       |
|                       | otherwise we have to  |                       |
|                       | go to the next        |                       |
|                       | letter. If we exit    |                       |
|                       | the loop normally,    |                       |
|                       | that means we didn't  |                       |
|                       | find an "e", so we    |                       |
|                       | return [True]{.c004}. |                       |
|                       | []{#hevea_default665} |                       |
|                       |                       |                       |
|                       | []{#hevea_default666} |                       |
|                       | []{#hevea_default667} |                       |
|                       | You could write this  |                       |
|                       | function more         |                       |
|                       | concisely using the   |                       |
|                       | [in]{.c004} operator, |                       |
|                       | but I started with    |                       |
|                       | this version because  |                       |
|                       | it demonstrates the   |                       |
|                       | logic of the search   |                       |
|                       | pattern.              |                       |
|                       |                       |                       |
|                       | []{#hevea_default668} |                       |
|                       | [avoids]{.c004} is a  |                       |
|                       | more general version  |                       |
|                       | of `has_no_e` but it  |                       |
|                       | has the same          |                       |
|                       | structure:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def avo               |                       |
|                       | ids(word, forbidden): |                       |
|                       |                       |                       |
|                       |   for letter in word: |                       |
|                       |         if            |                       |
|                       |  letter in forbidden: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | We can return         |                       |
|                       | [False]{.c004} as     |                       |
|                       | soon as we find a     |                       |
|                       | forbidden letter; if  |                       |
|                       | we get to the end of  |                       |
|                       | the loop, we return   |                       |
|                       | [True]{.c004}.        |                       |
|                       |                       |                       |
|                       | `uses_only` is        |                       |
|                       | similar except that   |                       |
|                       | the sense of the      |                       |
|                       | condition is          |                       |
|                       | reversed:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def uses_o            |                       |
|                       | nly(word, available): |                       |
|                       |                       |                       |
|                       |  for letter in word:  |                       |
|                       |         if let        |                       |
|                       | ter not in available: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Instead of a list of  |                       |
|                       | forbidden letters, we |                       |
|                       | have a list of        |                       |
|                       | available letters. If |                       |
|                       | we find a letter in   |                       |
|                       | [word]{.c004} that is |                       |
|                       | not in                |                       |
|                       | [available]{.c004},   |                       |
|                       | we can return         |                       |
|                       | [False]{.c004}.       |                       |
|                       |                       |                       |
|                       | `uses_all` is similar |                       |
|                       | except that we        |                       |
|                       | reverse the role of   |                       |
|                       | the word and the      |                       |
|                       | string of letters:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def uses              |                       |
|                       | _all(word, required): |                       |
|                       |     for               |                       |
|                       |  letter in required:  |                       |
|                       |         i             |                       |
|                       | f letter not in word: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Instead of traversing |                       |
|                       | the letters in        |                       |
|                       | [word]{.c004}, the    |                       |
|                       | loop traverses the    |                       |
|                       | required letters. If  |                       |
|                       | any of the required   |                       |
|                       | letters do not appear |                       |
|                       | in the word, we can   |                       |
|                       | return                |                       |
|                       | [False]{.c004}.       |                       |
|                       | []{#hevea_default669} |                       |
|                       |                       |                       |
|                       | If you were really    |                       |
|                       | thinking like a       |                       |
|                       | computer scientist,   |                       |
|                       | you would have        |                       |
|                       | recognized that       |                       |
|                       | `uses_all` was an     |                       |
|                       | instance of a         |                       |
|                       | previously solved     |                       |
|                       | problem, and you      |                       |
|                       | would have written:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def uses              |                       |
|                       | _all(word, required): |                       |
|                       |     return uses       |                       |
|                       | _only(required, word) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This is an example of |                       |
|                       | a program development |                       |
|                       | plan called           |                       |
|                       | [reduction to a       |                       |
|                       | previously solved     |                       |
|                       | problem]{.c010},      |                       |
|                       | which means that you  |                       |
|                       | recognize the problem |                       |
|                       | you are working on as |                       |
|                       | an instance of a      |                       |
|                       | solved problem and    |                       |
|                       | apply an existing     |                       |
|                       | solution.             |                       |
|                       | []{#hevea_default670} |                       |
|                       | []{#hevea_default671} |                       |
|                       |                       |                       |
|                       | ## 9.                 |                       |
|                       | 4  Looping with indic |                       |
|                       | es {#sec109 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default672} |                       |
|                       | []{#hevea_default673} |                       |
|                       |                       |                       |
|                       | I wrote the functions |                       |
|                       | in the previous       |                       |
|                       | section with          |                       |
|                       | [for]{.c004} loops    |                       |
|                       | because I only needed |                       |
|                       | the characters in the |                       |
|                       | strings; I didn't     |                       |
|                       | have to do anything   |                       |
|                       | with the indices.     |                       |
|                       |                       |                       |
|                       | For `is_abecedarian`  |                       |
|                       | we have to compare    |                       |
|                       | adjacent letters,     |                       |
|                       | which is a little     |                       |
|                       | tricky with a         |                       |
|                       | [for]{.c004} loop:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | is_abecedarian(word): |                       |
|                       |                       |                       |
|                       |    previous = word[0] |                       |
|                       |     for c in word:    |                       |
|                       |                       |                       |
|                       |      if c < previous: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |         previous = c  |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | An alternative is to  |                       |
|                       | use recursion:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | is_abecedarian(word): |                       |
|                       |                       |                       |
|                       |    if len(word) <= 1: |                       |
|                       |         return True   |                       |
|                       |                       |                       |
|                       | if word[0] > word[1]: |                       |
|                       |         return False  |                       |
|                       |     return is_        |                       |
|                       | abecedarian(word[1:]) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Another option is to  |                       |
|                       | use a [while]{.c004}  |                       |
|                       | loop:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | is_abecedarian(word): |                       |
|                       |     i = 0             |                       |
|                       |     w                 |                       |
|                       | hile i < len(word)-1: |                       |
|                       |         if            |                       |
|                       |  word[i+1] < word[i]: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |         i = i+1       |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The loop starts at    |                       |
|                       | [i=0]{.c004} and ends |                       |
|                       | when                  |                       |
|                       | [i                    |                       |
|                       | =len(word)-1]{.c004}. |                       |
|                       | Each time through the |                       |
|                       | loop, it compares the |                       |
|                       | [i]{.c009}th          |                       |
|                       | character (which you  |                       |
|                       | can think of as the   |                       |
|                       | current character) to |                       |
|                       | the [i]{.c009}+1th    |                       |
|                       | character (which you  |                       |
|                       | can think of as the   |                       |
|                       | next).                |                       |
|                       |                       |                       |
|                       | If the next character |                       |
|                       | is less than          |                       |
|                       | (alphabetically       |                       |
|                       | before) the current   |                       |
|                       | one, then we have     |                       |
|                       | discovered a break in |                       |
|                       | the abecedarian       |                       |
|                       | trend, and we return  |                       |
|                       | [False]{.c004}.       |                       |
|                       |                       |                       |
|                       | If we get to the end  |                       |
|                       | of the loop without   |                       |
|                       | finding a fault, then |                       |
|                       | the word passes the   |                       |
|                       | test. To convince     |                       |
|                       | yourself that the     |                       |
|                       | loop ends correctly,  |                       |
|                       | consider an example   |                       |
|                       | like `'flossy'`. The  |                       |
|                       | length of the word is |                       |
|                       | 6, so the last time   |                       |
|                       | the loop runs is when |                       |
|                       | [i]{.c004} is 4,      |                       |
|                       | which is the index of |                       |
|                       | the second-to-last    |                       |
|                       | character. On the     |                       |
|                       | last iteration, it    |                       |
|                       | compares the          |                       |
|                       | second-to-last        |                       |
|                       | character to the      |                       |
|                       | last, which is what   |                       |
|                       | we want.              |                       |
|                       | []{#hevea_default674} |                       |
|                       |                       |                       |
|                       | Here is a version of  |                       |
|                       | `is_palindrome` (see  |                       |
|                       | Exer                  |                       |
|                       | cise [3](thinkpython2 |                       |
|                       | 007.html#palindrome)) |                       |
|                       | that uses two         |                       |
|                       | indices; one starts   |                       |
|                       | at the beginning and  |                       |
|                       | goes up; the other    |                       |
|                       | starts at the end and |                       |
|                       | goes down.            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       |  is_palindrome(word): |                       |
|                       |     i = 0             |                       |
|                       |     j = len(word)-1   |                       |
|                       |                       |                       |
|                       |     while i<j:        |                       |
|                       |         i             |                       |
|                       | f word[i] != word[j]: |                       |
|                       |                       |                       |
|                       |          return False |                       |
|                       |         i = i+1       |                       |
|                       |         j = j-1       |                       |
|                       |                       |                       |
|                       |     return True       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Or we could reduce to |                       |
|                       | a previously solved   |                       |
|                       | problem and write:    |                       |
|                       | []{#hevea_default675} |                       |
|                       | []{#hevea_default676} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       |  is_palindrome(word): |                       |
|                       |     return i          |                       |
|                       | s_reverse(word, word) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Using `is_reverse`    |                       |
|                       | from                  |                       |
|                       | Secti                 |                       |
|                       | on [8.11](thinkpython |                       |
|                       | 2009.html#isreverse). |                       |
|                       |                       |                       |
|                       | ## 9.5  Debuggi       |                       |
|                       | ng {#sec110 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default677} |                       |
|                       | []{#hevea_default678} |                       |
|                       | []{#hevea_default679} |                       |
|                       |                       |                       |
|                       | Testing programs is   |                       |
|                       | hard. The functions   |                       |
|                       | in this chapter are   |                       |
|                       | relatively easy to    |                       |
|                       | test because you can  |                       |
|                       | check the results by  |                       |
|                       | hand. Even so, it is  |                       |
|                       | somewhere between     |                       |
|                       | difficult and         |                       |
|                       | impossible to choose  |                       |
|                       | a set of words that   |                       |
|                       | test for all possible |                       |
|                       | errors.               |                       |
|                       |                       |                       |
|                       | Taking `has_no_e` as  |                       |
|                       | an example, there are |                       |
|                       | two obvious cases to  |                       |
|                       | check: words that     |                       |
|                       | have an 'e' should    |                       |
|                       | return                |                       |
|                       | [False]{.c004}, and   |                       |
|                       | words that don't      |                       |
|                       | should return         |                       |
|                       | [True]{.c004}. You    |                       |
|                       | should have no        |                       |
|                       | trouble coming up     |                       |
|                       | with one of each.     |                       |
|                       |                       |                       |
|                       | Within each case,     |                       |
|                       | there are some less   |                       |
|                       | obvious subcases.     |                       |
|                       | Among the words that  |                       |
|                       | have an "e", you      |                       |
|                       | should test words     |                       |
|                       | with an "e" at the    |                       |
|                       | beginning, the end,   |                       |
|                       | and somewhere in the  |                       |
|                       | middle. You should    |                       |
|                       | test long words,      |                       |
|                       | short words, and very |                       |
|                       | short words, like the |                       |
|                       | empty string. The     |                       |
|                       | empty string is an    |                       |
|                       | example of a [special |                       |
|                       | case]{.c010}, which   |                       |
|                       | is one of the         |                       |
|                       | non-obvious cases     |                       |
|                       | where errors often    |                       |
|                       | lurk.                 |                       |
|                       | []{#hevea_default680} |                       |
|                       |                       |                       |
|                       | In addition to the    |                       |
|                       | test cases you        |                       |
|                       | generate, you can     |                       |
|                       | also test your        |                       |
|                       | program with a word   |                       |
|                       | list like             |                       |
|                       | [words.txt]{.c004}.   |                       |
|                       | By scanning the       |                       |
|                       | output, you might be  |                       |
|                       | able to catch errors, |                       |
|                       | but be careful: you   |                       |
|                       | might catch one kind  |                       |
|                       | of error (words that  |                       |
|                       | should not be         |                       |
|                       | included, but are)    |                       |
|                       | and not another       |                       |
|                       | (words that should be |                       |
|                       | included, but         |                       |
|                       | aren't).              |                       |
|                       |                       |                       |
|                       | In general, testing   |                       |
|                       | can help you find     |                       |
|                       | bugs, but it is not   |                       |
|                       | easy to generate a    |                       |
|                       | good set of test      |                       |
|                       | cases, and even if    |                       |
|                       | you do, you can't be  |                       |
|                       | sure your program is  |                       |
|                       | correct. According to |                       |
|                       | a legendary computer  |                       |
|                       | scientist:            |                       |
|                       | []{#hevea_default681} |                       |
|                       |                       |                       |
|                       | > Program testing can |                       |
|                       | > be used to show the |                       |
|                       | > presence of bugs,   |                       |
|                       | > but never to show   |                       |
|                       | > their absence!      |                       |
|                       | >                     |                       |
|                       | > --- Edsger W.       |                       |
|                       | > Dijkstra            |                       |
|                       |                       |                       |
|                       | []{#hevea_default682} |                       |
|                       |                       |                       |
|                       | ## 9.6  Glossa        |                       |
|                       | ry {#sec111 .section} |                       |
|                       |                       |                       |
|                       | [file object:]{.c010} |                       |
|                       | :   A value that      |                       |
|                       |     represents an     |                       |
|                       |     open file.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default683} |                       |
|                       |                       |                       |
|                       | []{#hevea_default684} |                       |
|                       |                       |                       |
|                       | [reducti              |                       |
|                       | on to a previously so |                       |
|                       | lved problem:]{.c010} |                       |
|                       | :   A way of solving  |                       |
|                       |     a problem by      |                       |
|                       |     expressing it as  |                       |
|                       |     an instance of a  |                       |
|                       |     previously solved |                       |
|                       |     problem.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default685} |                       |
|                       |                       |                       |
|                       | []{#hevea_default686} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | special case:]{.c010} |                       |
|                       | :   A test case that  |                       |
|                       |     is atypical or    |                       |
|                       |     non-obvious (and  |                       |
|                       |     less likely to be |                       |
|                       |     handled           |                       |
|                       |     correctly).       |                       |
|                       |                       |                       |
|                       | []{#hevea_default687} |                       |
|                       |                       |                       |
|                       | ## 9.7  Exercis       |                       |
|                       | es {#sec112 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 7]{.c010}   |                       |
|                       | []{#hevea_default688} |                       |
|                       | []{#hevea_default689} |                       |
|                       | []{#hevea_default690} |                       |
|                       |                       |                       |
|                       | *This question is     |                       |
|                       | based on a Puzzler    |                       |
|                       | that was broadcast on |                       |
|                       | the radio program*    |                       |
|                       | Car Talk              |                       |
|                       | *(*[*[http://www      |                       |
|                       | .cartalk.com/content/ |                       |
|                       | puzzlers]{.c004}*](ht |                       |
|                       | tp://www.cartalk.com/ |                       |
|                       | content/puzzlers)*):* |                       |
|                       |                       |                       |
|                       | > *Give me a word     |                       |
|                       | > with three          |                       |
|                       | > consecutive double  |                       |
|                       | > letters. I'll give  |                       |
|                       | > you a couple of     |                       |
|                       | > words that almost   |                       |
|                       | > qualify, but don't. |                       |
|                       | > For example, the    |                       |
|                       | > word committee,     |                       |
|                       | > c-o-m-m-i-t-t-e-e.  |                       |
|                       | > It would be great   |                       |
|                       | > except for the 'i'  |                       |
|                       | > that sneaks in      |                       |
|                       | > there. Or           |                       |
|                       | > Mississippi:        |                       |
|                       | > M                   |                       |
|                       | -i-s-s-i-s-s-i-p-p-i. |                       |
|                       | > If you could take   |                       |
|                       | > out those i's it    |                       |
|                       | > would work. But     |                       |
|                       | > there is a word     |                       |
|                       | > that has three      |                       |
|                       | > consecutive pairs   |                       |
|                       | > of letters and to   |                       |
|                       | > the best of my      |                       |
|                       | > knowledge this may  |                       |
|                       | > be the only word.   |                       |
|                       | > Of course there are |                       |
|                       | > probably 500 more   |                       |
|                       | > but I can only      |                       |
|                       | > think of one. What  |                       |
|                       | > is the word?*       |                       |
|                       |                       |                       |
|                       | *Write a program to   |                       |
|                       | find it. Solution:*   |                       |
|                       | [*[https://thi        |                       |
|                       | nkpython.com/code/car |                       |
|                       | talk1.py]{.c004}*](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/cartalk1.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 8]{.c010}   |                       |
|                       | *Here's another* Car  |                       |
|                       | Talk *Puzzler         |                       |
|                       | (*[[*http://www       |                       |
|                       | .cartalk.com/content/ |                       |
|                       | puzzlers*]{.c004}](ht |                       |
|                       | tp://www.cartalk.com/ |                       |
|                       | content/puzzlers)*):* |                       |
|                       | []{#hevea_default691} |                       |
|                       | []{#hevea_default692} |                       |
|                       | []{#hevea_default693} |                       |
|                       | []{#hevea_default694} |                       |
|                       |                       |                       |
|                       | > *"I was driving on  |                       |
|                       | > the highway the     |                       |
|                       | > other day and I     |                       |
|                       | > happened to notice  |                       |
|                       | > my odometer. Like   |                       |
|                       | > most odometers, it  |                       |
|                       | > shows six digits,   |                       |
|                       | > in whole miles      |                       |
|                       | > only. So, if my car |                       |
|                       | > had 300,000 miles,  |                       |
|                       | > for example, I'd    |                       |
|                       | > see 3-0-0-0-0-0.*   |                       |
|                       | >                     |                       |
|                       | > *"Now, what I saw   |                       |
|                       | > that day was very   |                       |
|                       | > interesting. I      |                       |
|                       | > noticed that the    |                       |
|                       | > last 4 digits were  |                       |
|                       | > palindromic; that   |                       |
|                       | > is, they read the   |                       |
|                       | > same forward as     |                       |
|                       | > backward. For       |                       |
|                       | > example, 5-4-4-5 is |                       |
|                       | > a palindrome, so my |                       |
|                       | > odometer could have |                       |
|                       | > read 3-1-5-4-4-5.*  |                       |
|                       | >                     |                       |
|                       | > *"One mile later,   |                       |
|                       | > the last 5 numbers  |                       |
|                       | > were palindromic.   |                       |
|                       | > For example, it     |                       |
|                       | > could have read     |                       |
|                       | > 3-6-5-4-5-6. One    |                       |
|                       | > mile after that,    |                       |
|                       | > the middle 4 out of |                       |
|                       | > 6 numbers were      |                       |
|                       | > palindromic. And    |                       |
|                       | > you ready for this? |                       |
|                       | > One mile later, all |                       |
|                       | > 6 were              |                       |
|                       | > palindromic!*       |                       |
|                       | >                     |                       |
|                       | > *"The question is,  |                       |
|                       | > what was on the     |                       |
|                       | > odometer when I     |                       |
|                       | > first looked?"*     |                       |
|                       |                       |                       |
|                       | *Write a Python       |                       |
|                       | program that tests    |                       |
|                       | all the six-digit     |                       |
|                       | numbers and prints    |                       |
|                       | any numbers that      |                       |
|                       | satisfy these         |                       |
|                       | requirements.         |                       |
|                       | Solution:*            |                       |
|                       | [*[https://thi        |                       |
|                       | nkpython.com/code/car |                       |
|                       | talk2.py]{.c004}*](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/cartalk2.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 9]{.c010}   |                       |
|                       | *Here's another* Car  |                       |
|                       | Talk *Puzzler you can |                       |
|                       | solve with a search   |                       |
|                       | (*[[*http://www       |                       |
|                       | .cartalk.com/content/ |                       |
|                       | puzzlers*]{.c004}](ht |                       |
|                       | tp://www.cartalk.com/ |                       |
|                       | content/puzzlers)*):* |                       |
|                       | []{#hevea_default695} |                       |
|                       | []{#hevea_default696} |                       |
|                       | []{#hevea_default697} |                       |
|                       |                       |                       |
|                       | > *"Recently I had a  |                       |
|                       | > visit with my mom   |                       |
|                       | > and we realized     |                       |
|                       | > that the two digits |                       |
|                       | > that make up my age |                       |
|                       | > when reversed       |                       |
|                       | > resulted in her     |                       |
|                       | > age. For example,   |                       |
|                       | > if she's 73, I'm    |                       |
|                       | > 37. We wondered how |                       |
|                       | > often this has      |                       |
|                       | > happened over the   |                       |
|                       | > years but we got    |                       |
|                       | > sidetracked with    |                       |
|                       | > other topics and we |                       |
|                       | > never came up with  |                       |
|                       | > an answer.*         |                       |
|                       | >                     |                       |
|                       | > *"When I got home I |                       |
|                       | > figured out that    |                       |
|                       | > the digits of our   |                       |
|                       | > ages have been      |                       |
|                       | > reversible six      |                       |
|                       | > times so far. I     |                       |
|                       | > also figured out    |                       |
|                       | > that if we're lucky |                       |
|                       | > it would happen     |                       |
|                       | > again in a few      |                       |
|                       | > years, and if we're |                       |
|                       | > really lucky it     |                       |
|                       | > would happen one    |                       |
|                       | > more time after     |                       |
|                       | > that. In other      |                       |
|                       | > words, it would     |                       |
|                       | > have happened 8     |                       |
|                       | > times over all. So  |                       |
|                       | > the question is,    |                       |
|                       | > how old am I now?"* |                       |
|                       |                       |                       |
|                       | *Write a Python       |                       |
|                       | program that searches |                       |
|                       | for solutions to this |                       |
|                       | Puzzler. Hint: you    |                       |
|                       | might find the string |                       |
|                       | method [zfill]{.c004} |                       |
|                       | useful.*              |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[https://thi        |                       |
|                       | nkpython.com/code/car |                       |
|                       | talk3.py]{.c004}*](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/cartalk3.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2009.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2011.html)
---
generator: hevea 2.32
title: Lists
---

[![Previous](back.png)](thinkpython2010.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2012.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 10  Lis     | to support my books,  |
|                       | ts {#sec113 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | This chapter presents | with PayPal. Thank    |
|                       | one of Python's most  | you!                  |
|                       | useful built-in       |                       |
|                       | types, lists. You     |   -----------         |
|                       | will also learn more  | --------------------- |
|                       | about objects and     | --------------------- |
|                       | what can happen when  | --------------------- |
|                       | you have more than    | --------------------- |
|                       | one name for the same |   Pay what you want:  |
|                       | object.               |   Small \$1           |
|                       |                       | .00 USD Medium \$5.00 |
|                       | ## 10.                |  USD Large \$10.00 US |
|                       | 1  A list is a sequen | D X-Large \$20.00 USD |
|                       | ce {#sec114 .section} |  XX-Large \$50.00 USD |
|                       |                       |   -----------         |
|                       | []{#sequence}         | --------------------- |
|                       |                       | --------------------- |
|                       | Like a string, a      | --------------------- |
|                       | [list]{.c010} is a    | --------------------- |
|                       | sequence of values.   |                       |
|                       | In a string, the      | ![](                  |
|                       | values are            | https://www.paypalobj |
|                       | characters; in a      | ects.com/en_US/i/scr/ |
|                       | list, they can be any | pixel.gif){border="0" |
|                       | type. The values in a | width="1" height="1"} |
|                       | list are called       |                       |
|                       | [elements]{.c010} or  | ####                  |
|                       | sometimes             | Are you using one of  |
|                       | [items]{.c010}.       | our books in a class? |
|                       | []{#hevea_default698} |                       |
|                       | []{#hevea_default699} | We\'d like to know    |
|                       | []{#hevea_default700} | about it. Please      |
|                       | []{#hevea_default701} | consider filling out  |
|                       | []{#hevea_default702} | [this short           |
|                       |                       | survey](http://s      |
|                       | There are several     | preadsheets.google.co |
|                       | ways to create a new  | m/viewform?formkey=dC |
|                       | list; the simplest is | 0tNUZkMjBEdXVoRGljNm9 |
|                       | to enclose the        | FRmlTMHc6MA){onclick= |
|                       | elements in square    | "javascript: pageTrac |
|                       | brackets (`[` and     | ker._trackPageview('/ |
|                       | `]`):                 | outbound/survey');"}. |
|                       |                       |                       |
|                       | ``` verbatim          | \                     |
|                       | [10, 20, 30, 40]      |                       |
|                       | ['c                   | [Think                |
|                       | runchy frog', 'ram bl | DSP](http             |
|                       | adder', 'lark vomit'] | ://www.amazon.com/gp/ |
|                       | ```                   | product/1491938455/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | The first example is  | mp=1789&creative=9325 |
|                       | a list of four        | &creativeASIN=1491938 |
|                       | integers. The second  | 455&linkCode=as2&tag= |
|                       | is a list of three    | greenteapre01-20&link |
|                       | strings. The elements | Id=2JJH4SWCAVVYSQHO){ |
|                       | of a list don't have  | rel="nofollow"}![](ht |
|                       | to be the same type.  | tp://ir-na.amazon-ads |
|                       | The following list    | ystem.com/e/ir?t=gree |
|                       | contains a string, a  | nteapre01-20&l=as2&o= |
|                       | float, an integer,    | 1&a=1491938455){.c003 |
|                       | and (lo!) another     | width="1" height="1"  |
|                       | list:                 | border="0"}           |
|                       |                       |                       |
|                       | ``` verbatim          | [                     |
|                       | ['spa                 | ![](http://ws-na.amaz |
|                       | m', 2.0, 5, [10, 20]] | on-adsystem.com/widge |
|                       | ```                   | ts/q?_encoding=UTF8&A |
|                       |                       | SIN=1491938455&Format |
|                       | A list within another | =_SL160_&ID=AsinImage |
|                       | list is               | &MarketPlace=US&Servi |
|                       | [nested]{.c010}.      | ceVersion=20070822&WS |
|                       | []{#hevea_default703} | =1&tag=greenteapre01- |
|                       | []{#hevea_default704} | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | A list that contains  | product/1491938455/re |
|                       | no elements is called | f=as_li_tl?ie=UTF8&ca |
|                       | an empty list; you    | mp=1789&creative=9325 |
|                       | can create one with   | &creativeASIN=1491938 |
|                       | empty brackets, `[]`. | 455&linkCode=as2&tag= |
|                       | []{#hevea_default705} | greenteapre01-20&link |
|                       | []{#hevea_default706} | Id=CTV7PDT7E5EGGJUM){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | As you might expect,  | tp://ir-na.amazon-ads |
|                       | you can assign list   | ystem.com/e/ir?t=gree |
|                       | values to variables:  | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491938455){.c003 |
|                       | ``` verbatim          | width="1" height="1"  |
|                       | >>> cheeses = ['Chedd | border="0"}           |
|                       | ar', 'Edam', 'Gouda'] |                       |
|                       | >>                    | [Think                |
|                       | > numbers = [42, 123] | Java](http            |
|                       | >>> empty = []        | ://www.amazon.com/gp/ |
|                       | >>> print(che         | product/1491929561/re |
|                       | eses, numbers, empty) | f=as_li_tl?ie=UTF8&ca |
|                       | ['Cheddar', 'Edam',   | mp=1789&creative=9325 |
|                       | 'Gouda'] [42, 123] [] | &creativeASIN=1491929 |
|                       | ```                   | 561&linkCode=as2&tag= |
|                       |                       | greenteapre01-20&link |
|                       | []{#hevea_default707} | Id=ZY6MAYM33ZTNSCNZ){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | ##                    | tp://ir-na.amazon-ads |
|                       | 10.2  Lists are mutab | ystem.com/e/ir?t=gree |
|                       | le {#sec115 .section} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | []{#mutable}          | width="1" height="1"  |
|                       | []{#hevea_default708} | border="0"}           |
|                       | []{#hevea_default709} |                       |
|                       | []{#hevea_default710} | [                     |
|                       | []{#hevea_default711} | ![](http://ws-na.amaz |
|                       | []{#hevea_default712} | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | The syntax for        | SIN=1491929561&Format |
|                       | accessing the         | =_SL160_&ID=AsinImage |
|                       | elements of a list is | &MarketPlace=US&Servi |
|                       | the same as for       | ceVersion=20070822&WS |
|                       | accessing the         | =1&tag=greenteapre01- |
|                       | characters of a       | 20){border="0"}](http |
|                       | string---the bracket  | ://www.amazon.com/gp/ |
|                       | operator. The         | product/1491929561/re |
|                       | expression inside the | f=as_li_tl?ie=UTF8&ca |
|                       | brackets specifies    | mp=1789&creative=9325 |
|                       | the index. Remember   | &creativeASIN=1491929 |
|                       | that the indices      | 561&linkCode=as2&tag= |
|                       | start at 0:           | greenteapre01-20&link |
|                       |                       | Id=PT77ANWARUNNU3UK){ |
|                       | ``` verbatim          | rel="nofollow"}![](ht |
|                       | >>> cheeses[0]        | tp://ir-na.amazon-ads |
|                       | 'Cheddar'             | ystem.com/e/ir?t=gree |
|                       | ```                   | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | Unlike strings, lists | width="1" height="1"  |
|                       | are mutable. When the | border="0"}           |
|                       | bracket operator      |                       |
|                       | appears on the left   | [Think                |
|                       | side of an            | Bay                   |
|                       | assignment, it        | es](http://www.amazon |
|                       | identifies the        | .com/gp/product/14493 |
|                       | element of the list   | 70780/ref=as_li_qf_sp |
|                       | that will be          | _asin_tl?ie=UTF8&camp |
|                       | assigned.             | =1789&creative=9325&c |
|                       | []{#hevea_default713} | reativeASIN=144937078 |
|                       |                       | 0&linkCode=as2&tag=gr |
|                       | ``` verbatim          | eenteapre01-20)![](ht |
|                       | >>                    | tp://ir-na.amazon-ads |
|                       | > numbers = [42, 123] | ystem.com/e/ir?t=gree |
|                       | >>> numbers[1] = 5    | nteapre01-20&l=as2&o= |
|                       | >>> numbers           | 1&a=1449370780){.c003 |
|                       | [42, 5]               | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | The one-eth element   | [![](http://ws        |
|                       | of [numbers]{.c004},  | -na.amazon-adsystem.c |
|                       | which used to be 123, | om/widgets/q?_encodin |
|                       | is now 5.             | g=UTF8&ASIN=144937078 |
|                       | []{#hevea_default714} | 0&Format=_SL160_&ID=A |
|                       | []{#hevea_default715} | sinImage&MarketPlace= |
|                       |                       | US&ServiceVersion=200 |
|                       | Figure [              | 70822&WS=1&tag=greent |
|                       | 10.1](#fig.liststate) | eapre01-20){border="0 |
|                       | shows the state       | "}](http://www.amazon |
|                       | diagram for           | .com/gp/product/14493 |
|                       | [cheeses]{.c004},     | 70780/ref=as_li_qf_sp |
|                       | [numbers]{.c004} and  | _asin_il?ie=UTF8&camp |
|                       | [empty]{.c004}.       | =1789&creative=9325&c |
|                       | []{#hevea_default716} | reativeASIN=144937078 |
|                       | []{#hevea_default717} | 0&linkCode=as2&tag=gr |
|                       |                       | eenteapre01-20)![](ht |
|                       | > ::: center          | tp://ir-na.amazon-ads |
|                       | >                     | ystem.com/e/ir?t=gree |
|                       | > ------------------- | nteapre01-20&l=as2&o= |
|                       | > :::                 | 1&a=1449370780){.c003 |
|                       | >                     | width="1" height="1"  |
|                       | > ::: center          | border="0"}           |
|                       | > ![]                 |                       |
|                       | (thinkpython2011.png) | [Think Python         |
|                       | > :::                 | 2e](http              |
|                       | >                     | ://www.amazon.com/gp/ |
|                       | > ::: caption         | product/1491939362/re |
|                       | >   --------          | f=as_li_tl?ie=UTF8&ca |
|                       | --------------------- | mp=1789&creative=9325 |
|                       | >   Figure            | &creativeASIN=1491939 |
|                       |  10.1: State diagram. | 362&linkCode=as2&tag= |
|                       | >   --------          | greenteapre01-20&link |
|                       | --------------------- | Id=FJKSQ3IHEMY2F2VA){ |
|                       | > :::                 | rel="nofollow"}![](ht |
|                       | >                     | tp://ir-na.amazon-ads |
|                       | > []{#fig.liststate}  | ystem.com/e/ir?t=gree |
|                       | >                     | nteapre01-20&l=as2&o= |
|                       | > ::: center          | 1&a=1491939362){.c003 |
|                       | >                     | width="1" height="1"  |
|                       | > ------------------- | border="0"}           |
|                       | > :::                 |                       |
|                       |                       | [                     |
|                       | Lists are represented | ![](http://ws-na.amaz |
|                       | by boxes with the     | on-adsystem.com/widge |
|                       | word "list" outside   | ts/q?_encoding=UTF8&A |
|                       | and the elements of   | SIN=1491939362&Format |
|                       | the list inside.      | =_SL160_&ID=AsinImage |
|                       | [cheeses]{.c004}      | &MarketPlace=US&Servi |
|                       | refers to a list with | ceVersion=20070822&WS |
|                       | three elements        | =1&tag=greenteapre01- |
|                       | indexed 0, 1 and 2.   | 20){border="0"}](http |
|                       | [numbers]{.c004}      | ://www.amazon.com/gp/ |
|                       | contains two          | product/1491939362/re |
|                       | elements; the diagram | f=as_li_tl?ie=UTF8&ca |
|                       | shows that the value  | mp=1789&creative=9325 |
|                       | of the second element | &creativeASIN=1491939 |
|                       | has been reassigned   | 362&linkCode=as2&tag= |
|                       | from 123 to 5.        | greenteapre01-20&link |
|                       | [empty]{.c004} refers | Id=ZZ454DLQ3IXDHNHX){ |
|                       | to a list with no     | rel="nofollow"}![](ht |
|                       | elements.             | tp://ir-na.amazon-ads |
|                       | []{#hevea_default718} | ystem.com/e/ir?t=gree |
|                       | []{#hevea_default719} | nteapre01-20&l=as2&o= |
|                       | []{#hevea_default720} | 1&a=1491939362){.c003 |
|                       |                       | width="1" height="1"  |
|                       | List indices work the | border="0"}           |
|                       | same way as string    |                       |
|                       | indices:              | [Think Stats          |
|                       |                       | 2e](http://ww         |
|                       | -   Any integer       | w.amazon.com/gp/produ |
|                       |     expression can be | ct/1491907339/ref=as_ |
|                       |     used as an index. | li_tl?ie=UTF8&camp=17 |
|                       | -   If you try to     | 89&creative=9325&crea |
|                       |     read or write an  | tiveASIN=1491907339&l |
|                       |     element that does | inkCode=as2&tag=green |
|                       |     not exist, you    | teapre01-20&linkId=O7 |
|                       |     get an            | WYM6H6YBYUFNWU)![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       |  [IndexError]{.c004}. | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | []{#hevea_default721} | 1&a=1491907339){.c003 |
|                       |                       | width="1" height="1"  |
|                       | []{#hevea_default722} | border="0"}           |
|                       | -   If an index has a |                       |
|                       |     negative value,   | [![](h                |
|                       |     it counts         | ttp://ws-na.amazon-ad |
|                       |     backward from the | system.com/widgets/q? |
|                       |     end of the list.  | _encoding=UTF8&ASIN=1 |
|                       |                       | 491907339&Format=_SL1 |
|                       | []{#hevea_default723} | 60_&ID=AsinImage&Mark |
|                       |                       | etPlace=US&ServiceVer |
|                       | []{#hevea_default724} | sion=20070822&WS=1&ta |
|                       | []{#hevea_default725} | g=greenteapre01-20){b |
|                       | []{#hevea_default726} | order="0"}](http://ww |
|                       | []{#hevea_default727} | w.amazon.com/gp/produ |
|                       |                       | ct/1491907339/ref=as_ |
|                       | The [in]{.c004}       | li_tl?ie=UTF8&camp=17 |
|                       | operator also works   | 89&creative=9325&crea |
|                       | on lists.             | tiveASIN=1491907339&l |
|                       |                       | inkCode=as2&tag=green |
|                       | ``` verbatim          | teapre01-20&linkId=JV |
|                       | >>> cheeses = ['Chedd | SYKQHYSUIEYRHL)![](ht |
|                       | ar', 'Edam', 'Gouda'] | tp://ir-na.amazon-ads |
|                       | >>> 'Edam' in cheeses | ystem.com/e/ir?t=gree |
|                       | True                  | nteapre01-20&l=as2&o= |
|                       | >>> 'Brie' in cheeses | 1&a=1491907339){.c003 |
|                       | False                 | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | ##                    | [Think                |
|                       | 10.3  Traversing a li | Complexity](http      |
|                       | st {#sec116 .section} | ://www.amazon.com/gp/ |
|                       |                       | product/1449314635/re |
|                       | []{#hevea_default728} | f=as_li_tf_tl?ie=UTF8 |
|                       | []{#hevea_default729} | &tag=greenteapre01-20 |
|                       | []{#hevea_default730} | &linkCode=as2&camp=17 |
|                       | []{#hevea_default731} | 89&creative=9325&crea |
|                       | []{#hevea_default732} | tiveASIN=1449314635)! |
|                       |                       | [](http://www.assoc-a |
|                       | The most common way   | mazon.com/e/ir?t=gree |
|                       | to traverse the       | nteapre01-20&l=as2&o= |
|                       | elements of a list is | 1&a=1449314635){.c003 |
|                       | with a [for]{.c004}   | width="1" height="1"  |
|                       | loop. The syntax is   | border="0"}           |
|                       | the same as for       |                       |
|                       | strings:              | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | ``` verbatim          | on-adsystem.com/widge |
|                       | f                     | ts/q?_encoding=UTF8&A |
|                       | or cheese in cheeses: | SIN=1449314635&Format |
|                       |     print(cheese)     | =_SL160_&ID=AsinImage |
|                       | ```                   | &MarketPlace=US&Servi |
|                       |                       | ceVersion=20070822&WS |
|                       | This works well if    | =1&tag=greenteapre01- |
|                       | you only need to read | 20){border="0"}](http |
|                       | the elements of the   | ://www.amazon.com/gp/ |
|                       | list. But if you want | product/1449314635/re |
|                       | to write or update    | f=as_li_tf_il?ie=UTF8 |
|                       | the elements, you     | &camp=1789&creative=9 |
|                       | need the indices. A   | 325&creativeASIN=1449 |
|                       | common way to do that | 314635&linkCode=as2&t |
|                       | is to combine the     | ag=greenteapre01-20)! |
|                       | built-in functions    | [](http://www.assoc-a |
|                       | [range]{.c004} and    | mazon.com/e/ir?t=gree |
|                       | [len]{.c004}:         | nteapre01-20&l=as2&o= |
|                       | []{#hevea_default733} | 1&a=1449314635){.c003 |
|                       | []{#hevea_default734} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | ``` verbatim          |                       |
|                       | for i in              |                       |
|                       |  range(len(numbers)): |                       |
|                       |     number            |                       |
|                       | s[i] = numbers[i] * 2 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This loop traverses   |                       |
|                       | the list and updates  |                       |
|                       | each element.         |                       |
|                       | [len]{.c004} returns  |                       |
|                       | the number of         |                       |
|                       | elements in the list. |                       |
|                       | [range]{.c004}        |                       |
|                       | returns a list of     |                       |
|                       | indices from 0 to     |                       |
|                       | [n]{.c009}−1, where   |                       |
|                       | [n]{.c009} is the     |                       |
|                       | length of the list.   |                       |
|                       | Each time through the |                       |
|                       | loop [i]{.c004} gets  |                       |
|                       | the index of the next |                       |
|                       | element. The          |                       |
|                       | assignment statement  |                       |
|                       | in the body uses      |                       |
|                       | [i]{.c004} to read    |                       |
|                       | the old value of the  |                       |
|                       | element and to assign |                       |
|                       | the new value.        |                       |
|                       | []{#hevea_default735} |                       |
|                       | []{#hevea_default736} |                       |
|                       |                       |                       |
|                       | A [for]{.c004} loop   |                       |
|                       | over an empty list    |                       |
|                       | never runs the body:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | for x in []:          |                       |
|                       |     print('           |                       |
|                       | This never happens.') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Although a list can   |                       |
|                       | contain another list, |                       |
|                       | the nested list still |                       |
|                       | counts as a single    |                       |
|                       | element. The length   |                       |
|                       | of this list is four: |                       |
|                       | []{#hevea_default737} |                       |
|                       | []{#hevea_default738} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | ['spam', 1, ['Bri     |                       |
|                       | e', 'Roquefort', 'Pol |                       |
|                       |  le Veq'], [1, 2, 3]] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 10.4  List operatio |                       |
|                       | ns {#sec117 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default739} |                       |
|                       |                       |                       |
|                       | The [+]{.c004}        |                       |
|                       | operator concatenates |                       |
|                       | lists:                |                       |
|                       | []{#hevea_default740} |                       |
|                       | []{#hevea_default741} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> a = [1, 2, 3]     |                       |
|                       | >>> b = [4, 5, 6]     |                       |
|                       | >>> c = a + b         |                       |
|                       | >>> c                 |                       |
|                       | [1, 2, 3, 4, 5, 6]    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [\*]{.c004}       |                       |
|                       | operator repeats a    |                       |
|                       | list a given number   |                       |
|                       | of times:             |                       |
|                       | []{#hevea_default742} |                       |
|                       | []{#hevea_default743} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> [0] * 4           |                       |
|                       | [0, 0, 0, 0]          |                       |
|                       | >>> [1, 2, 3] * 3     |                       |
|                       | [1, 2,                |                       |
|                       |  3, 1, 2, 3, 1, 2, 3] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first example     |                       |
|                       | repeats               |                       |
|                       | [\[0\]]{.c004} four   |                       |
|                       | times. The second     |                       |
|                       | example repeats the   |                       |
|                       | list [\[1, 2,         |                       |
|                       | 3\]]{.c004} three     |                       |
|                       | times.                |                       |
|                       |                       |                       |
|                       | ## 10.5  List slic    |                       |
|                       | es {#sec118 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default744} |                       |
|                       | []{#hevea_default745} |                       |
|                       | []{#hevea_default746} |                       |
|                       | []{#hevea_default747} |                       |
|                       | []{#hevea_default748} |                       |
|                       |                       |                       |
|                       | The slice operator    |                       |
|                       | also works on lists:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = ['a', 'b'     |                       |
|                       | , 'c', 'd', 'e', 'f'] |                       |
|                       | >>> t[1:3]            |                       |
|                       | ['b', 'c']            |                       |
|                       | >>> t[:4]             |                       |
|                       | ['a', 'b', 'c', 'd']  |                       |
|                       | >>> t[3:]             |                       |
|                       | ['d', 'e', 'f']       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you omit the first |                       |
|                       | index, the slice      |                       |
|                       | starts at the         |                       |
|                       | beginning. If you     |                       |
|                       | omit the second, the  |                       |
|                       | slice goes to the     |                       |
|                       | end. So if you omit   |                       |
|                       | both, the slice is a  |                       |
|                       | copy of the whole     |                       |
|                       | list.                 |                       |
|                       | []{#hevea_default749} |                       |
|                       | []{#hevea_default750} |                       |
|                       | []{#hevea_default751} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t[:]              |                       |
|                       | ['a', 'b'             |                       |
|                       | , 'c', 'd', 'e', 'f'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Since lists are       |                       |
|                       | mutable, it is often  |                       |
|                       | useful to make a copy |                       |
|                       | before performing     |                       |
|                       | operations that       |                       |
|                       | modify lists.         |                       |
|                       | []{#hevea_default752} |                       |
|                       |                       |                       |
|                       | A slice operator on   |                       |
|                       | the left side of an   |                       |
|                       | assignment can update |                       |
|                       | multiple elements:    |                       |
|                       | []{#hevea_default753} |                       |
|                       | []{#hevea_default754} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = ['a', 'b'     |                       |
|                       | , 'c', 'd', 'e', 'f'] |                       |
|                       | >>                    |                       |
|                       | > t[1:3] = ['x', 'y'] |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'x'             |                       |
|                       | , 'y', 'd', 'e', 'f'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 10.6  List metho   |                       |
|                       | ds {#sec119 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default755} |                       |
|                       | []{#hevea_default756} |                       |
|                       |                       |                       |
|                       | Python provides       |                       |
|                       | methods that operate  |                       |
|                       | on lists. For         |                       |
|                       | example,              |                       |
|                       | [append]{.c004} adds  |                       |
|                       | a new element to the  |                       |
|                       | end of a list:        |                       |
|                       | []{#hevea_default757} |                       |
|                       | []{#hevea_default758} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > t = ['a', 'b', 'c'] |                       |
|                       | >>> t.append('d')     |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'b', 'c', 'd']  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [extend]{.c004} takes |                       |
|                       | a list as an argument |                       |
|                       | and appends all of    |                       |
|                       | the elements:         |                       |
|                       | []{#hevea_default759} |                       |
|                       | []{#hevea_default760} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       |  t1 = ['a', 'b', 'c'] |                       |
|                       | >>> t2 = ['d', 'e']   |                       |
|                       | >>> t1.extend(t2)     |                       |
|                       | >>> t1                |                       |
|                       | ['a'                  |                       |
|                       | , 'b', 'c', 'd', 'e'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This example leaves   |                       |
|                       | [t2]{.c004}           |                       |
|                       | unmodified.           |                       |
|                       |                       |                       |
|                       | [sort]{.c004}         |                       |
|                       | arranges the elements |                       |
|                       | of the list from low  |                       |
|                       | to high:              |                       |
|                       | []{#hevea_default761} |                       |
|                       | []{#hevea_default762} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = ['d'          |                       |
|                       | , 'c', 'e', 'b', 'a'] |                       |
|                       | >>> t.sort()          |                       |
|                       | >>> t                 |                       |
|                       | ['a'                  |                       |
|                       | , 'b', 'c', 'd', 'e'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Most list methods are |                       |
|                       | void; they modify the |                       |
|                       | list and return       |                       |
|                       | [None]{.c004}. If you |                       |
|                       | accidentally write [t |                       |
|                       | = t.sort()]{.c004},   |                       |
|                       | you will be           |                       |
|                       | disappointed with the |                       |
|                       | result.               |                       |
|                       | []{#hevea_default763} |                       |
|                       | []{#hevea_default764} |                       |
|                       | []{#hevea_default765} |                       |
|                       | []{#hevea_default766} |                       |
|                       |                       |                       |
|                       | ## 10.7               |                       |
|                       |  Map, filter and redu |                       |
|                       | ce {#sec120 .section} |                       |
|                       |                       |                       |
|                       | []{#filter}           |                       |
|                       |                       |                       |
|                       | To add up all the     |                       |
|                       | numbers in a list,    |                       |
|                       | you can use a loop    |                       |
|                       | like this:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def add_all(t):       |                       |
|                       |     total = 0         |                       |
|                       |     for x in t:       |                       |
|                       |         total += x    |                       |
|                       |     return total      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [total]{.c004} is     |                       |
|                       | initialized to 0.     |                       |
|                       | Each time through the |                       |
|                       | loop, [x]{.c004} gets |                       |
|                       | one element from the  |                       |
|                       | list. The [+=]{.c004} |                       |
|                       | operator provides a   |                       |
|                       | short way to update a |                       |
|                       | variable. This        |                       |
|                       | [augmented assignment |                       |
|                       | statement]{.c010},    |                       |
|                       | []{#hevea_default767} |                       |
|                       | []{#hevea_default768} |                       |
|                       | []{#hevea_default769} |                       |
|                       | []{#hevea_default770} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |     total += x        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | is equivalent to      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       |     total = total + x |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As the loop runs,     |                       |
|                       | [total]{.c004}        |                       |
|                       | accumulates the sum   |                       |
|                       | of the elements; a    |                       |
|                       | variable used this    |                       |
|                       | way is sometimes      |                       |
|                       | called an             |                       |
|                       | [accumulator]{.c010}. |                       |
|                       | []{#hevea_default771} |                       |
|                       |                       |                       |
|                       | Adding up the         |                       |
|                       | elements of a list is |                       |
|                       | such a common         |                       |
|                       | operation that Python |                       |
|                       | provides it as a      |                       |
|                       | built-in function,    |                       |
|                       | [sum]{.c004}:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> sum(t)            |                       |
|                       | 6                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | An operation like     |                       |
|                       | this that combines a  |                       |
|                       | sequence of elements  |                       |
|                       | into a single value   |                       |
|                       | is sometimes called   |                       |
|                       | [reduce]{.c010}.      |                       |
|                       | []{#hevea_default772} |                       |
|                       | []{#hevea_default773} |                       |
|                       | []{#hevea_default774} |                       |
|                       |                       |                       |
|                       | Sometimes you want to |                       |
|                       | traverse one list     |                       |
|                       | while building        |                       |
|                       | another. For example, |                       |
|                       | the following         |                       |
|                       | function takes a list |                       |
|                       | of strings and        |                       |
|                       | returns a new list    |                       |
|                       | that contains         |                       |
|                       | capitalized strings:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef capitalize_all(t): |                       |
|                       |     res = []          |                       |
|                       |     for s in t:       |                       |
|                       |         res.a         |                       |
|                       | ppend(s.capitalize()) |                       |
|                       |     return res        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [res]{.c004} is       |                       |
|                       | initialized with an   |                       |
|                       | empty list; each time |                       |
|                       | through the loop, we  |                       |
|                       | append the next       |                       |
|                       | element. So           |                       |
|                       | [res]{.c004} is       |                       |
|                       | another kind of       |                       |
|                       | accumulator.          |                       |
|                       | []{#hevea_default775} |                       |
|                       |                       |                       |
|                       | An operation like     |                       |
|                       | `capitalize_all` is   |                       |
|                       | sometimes called a    |                       |
|                       | [map]{.c010} because  |                       |
|                       | it "maps" a function  |                       |
|                       | (in this case the     |                       |
|                       | method                |                       |
|                       | [capitalize]{.c004})  |                       |
|                       | onto each of the      |                       |
|                       | elements in a         |                       |
|                       | sequence.             |                       |
|                       | []{#hevea_default776} |                       |
|                       | []{#hevea_default777} |                       |
|                       | []{#hevea_default778} |                       |
|                       | []{#hevea_default779} |                       |
|                       |                       |                       |
|                       | Another common        |                       |
|                       | operation is to       |                       |
|                       | select some of the    |                       |
|                       | elements from a list  |                       |
|                       | and return a sublist. |                       |
|                       | For example, the      |                       |
|                       | following function    |                       |
|                       | takes a list of       |                       |
|                       | strings and returns a |                       |
|                       | list that contains    |                       |
|                       | only the uppercase    |                       |
|                       | strings:              |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def only_upper(t):    |                       |
|                       |     res = []          |                       |
|                       |     for s in t:       |                       |
|                       |                       |                       |
|                       |       if s.isupper(): |                       |
|                       |                       |                       |
|                       |         res.append(s) |                       |
|                       |     return res        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [isupper]{.c004} is a |                       |
|                       | string method that    |                       |
|                       | returns [True]{.c004} |                       |
|                       | if the string         |                       |
|                       | contains only upper   |                       |
|                       | case letters.         |                       |
|                       |                       |                       |
|                       | An operation like     |                       |
|                       | `only_upper` is       |                       |
|                       | called a              |                       |
|                       | [filter]{.c010}       |                       |
|                       | because it selects    |                       |
|                       | some of the elements  |                       |
|                       | and filters out the   |                       |
|                       | others.               |                       |
|                       |                       |                       |
|                       | Most common list      |                       |
|                       | operations can be     |                       |
|                       | expressed as a        |                       |
|                       | combination of map,   |                       |
|                       | filter and reduce.    |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 10.8  Deleting elemen |                       |
|                       | ts {#sec121 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default780} |                       |
|                       | []{#hevea_default781} |                       |
|                       |                       |                       |
|                       | There are several     |                       |
|                       | ways to delete        |                       |
|                       | elements from a list. |                       |
|                       | If you know the index |                       |
|                       | of the element you    |                       |
|                       | want, you can use     |                       |
|                       | [pop]{.c004}:         |                       |
|                       | []{#hevea_default782} |                       |
|                       | []{#hevea_default783} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > t = ['a', 'b', 'c'] |                       |
|                       | >>> x = t.pop(1)      |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'c']            |                       |
|                       | >>> x                 |                       |
|                       | 'b'                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [pop]{.c004} modifies |                       |
|                       | the list and returns  |                       |
|                       | the element that was  |                       |
|                       | removed. If you don't |                       |
|                       | provide an index, it  |                       |
|                       | deletes and returns   |                       |
|                       | the last element.     |                       |
|                       |                       |                       |
|                       | If you don't need the |                       |
|                       | removed value, you    |                       |
|                       | can use the           |                       |
|                       | [del]{.c004}          |                       |
|                       | operator:             |                       |
|                       | []{#hevea_default784} |                       |
|                       | []{#hevea_default785} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > t = ['a', 'b', 'c'] |                       |
|                       | >>> del t[1]          |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'c']            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you know the       |                       |
|                       | element you want to   |                       |
|                       | remove (but not the   |                       |
|                       | index), you can use   |                       |
|                       | [remove]{.c004}:      |                       |
|                       | []{#hevea_default786} |                       |
|                       | []{#hevea_default787} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > t = ['a', 'b', 'c'] |                       |
|                       | >>> t.remove('b')     |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'c']            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The return value from |                       |
|                       | [remove]{.c004} is    |                       |
|                       | [None]{.c004}.        |                       |
|                       | []{#hevea_default788} |                       |
|                       | []{#hevea_default789} |                       |
|                       |                       |                       |
|                       | To remove more than   |                       |
|                       | one element, you can  |                       |
|                       | use [del]{.c004} with |                       |
|                       | a slice index:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = ['a', 'b'     |                       |
|                       | , 'c', 'd', 'e', 'f'] |                       |
|                       | >>> del t[1:5]        |                       |
|                       | >>> t                 |                       |
|                       | ['a', 'f']            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As usual, the slice   |                       |
|                       | selects all the       |                       |
|                       | elements up to but    |                       |
|                       | not including the     |                       |
|                       | second index.         |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 10.9  Lists and strin |                       |
|                       | gs {#sec122 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default790} |                       |
|                       | []{#hevea_default791} |                       |
|                       | []{#hevea_default792} |                       |
|                       |                       |                       |
|                       | A string is a         |                       |
|                       | sequence of           |                       |
|                       | characters and a list |                       |
|                       | is a sequence of      |                       |
|                       | values, but a list of |                       |
|                       | characters is not the |                       |
|                       | same as a string. To  |                       |
|                       | convert from a string |                       |
|                       | to a list of          |                       |
|                       | characters, you can   |                       |
|                       | use [list]{.c004}:    |                       |
|                       | []{#hevea_default793} |                       |
|                       | []{#hevea_default794} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> s = 'spam'        |                       |
|                       | >>> t = list(s)       |                       |
|                       | >>> t                 |                       |
|                       | ['s', 'p', 'a', 'm']  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Because [list]{.c004} |                       |
|                       | is the name of a      |                       |
|                       | built-in function,    |                       |
|                       | you should avoid      |                       |
|                       | using it as a         |                       |
|                       | variable name. I also |                       |
|                       | avoid [l]{.c004}      |                       |
|                       | because it looks too  |                       |
|                       | much like [1]{.c004}. |                       |
|                       | So that's why I use   |                       |
|                       | [t]{.c004}.           |                       |
|                       |                       |                       |
|                       | The [list]{.c004}     |                       |
|                       | function breaks a     |                       |
|                       | string into           |                       |
|                       | individual letters.   |                       |
|                       | If you want to break  |                       |
|                       | a string into words,  |                       |
|                       | you can use the       |                       |
|                       | [split]{.c004}        |                       |
|                       | method:               |                       |
|                       | []{#hevea_default795} |                       |
|                       | []{#hevea_default796} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> s = 'p            |                       |
|                       | ining for the fjords' |                       |
|                       | >>> t = s.split()     |                       |
|                       | >>> t                 |                       |
|                       | ['pining', 'f         |                       |
|                       | or', 'the', 'fjords'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | An optional argument  |                       |
|                       | called a              |                       |
|                       | [delimiter]{.c010}    |                       |
|                       | specifies which       |                       |
|                       | characters to use as  |                       |
|                       | word boundaries. The  |                       |
|                       | following example     |                       |
|                       | uses a hyphen as a    |                       |
|                       | delimiter:            |                       |
|                       | []{#hevea_default797} |                       |
|                       | []{#hevea_default798} |                       |
|                       | []{#hevea_default799} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       |  s = 'spam-spam-spam' |                       |
|                       | >>> delimiter = '-'   |                       |
|                       | >>> t                 |                       |
|                       |  = s.split(delimiter) |                       |
|                       | >>> t                 |                       |
|                       | ['s                   |                       |
|                       | pam', 'spam', 'spam'] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [join]{.c004} is the  |                       |
|                       | inverse of            |                       |
|                       | [split]{.c004}. It    |                       |
|                       | takes a list of       |                       |
|                       | strings and           |                       |
|                       | concatenates the      |                       |
|                       | elements.             |                       |
|                       | [join]{.c004} is a    |                       |
|                       | string method, so you |                       |
|                       | have to invoke it on  |                       |
|                       | the delimiter and     |                       |
|                       | pass the list as a    |                       |
|                       | parameter:            |                       |
|                       | []{#hevea_default800} |                       |
|                       | []{#hevea_default801} |                       |
|                       | []{#hevea_default802} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = ['pining', 'f |                       |
|                       | or', 'the', 'fjords'] |                       |
|                       | >>> delimiter = ' '   |                       |
|                       | >>>                   |                       |
|                       | s = delimiter.join(t) |                       |
|                       | >>> s                 |                       |
|                       | 'p                    |                       |
|                       | ining for the fjords' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In this case the      |                       |
|                       | delimiter is a space  |                       |
|                       | character, so         |                       |
|                       | [join]{.c004} puts a  |                       |
|                       | space between words.  |                       |
|                       | To concatenate        |                       |
|                       | strings without       |                       |
|                       | spaces, you can use   |                       |
|                       | the empty string,     |                       |
|                       | `''`, as a delimiter. |                       |
|                       | []{#hevea_default803} |                       |
|                       | []{#hevea_default804} |                       |
|                       |                       |                       |
|                       | ## 10                 |                       |
|                       | .10  Objects and valu |                       |
|                       | es {#sec123 .section} |                       |
|                       |                       |                       |
|                       | []{#equivalence}      |                       |
|                       | []{#hevea_default805} |                       |
|                       | []{#hevea_default806} |                       |
|                       |                       |                       |
|                       | If we run these       |                       |
|                       | assignment            |                       |
|                       | statements:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | a = 'banana'          |                       |
|                       | b = 'banana'          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | We know that          |                       |
|                       | [a]{.c004} and        |                       |
|                       | [b]{.c004} both refer |                       |
|                       | to a string, but we   |                       |
|                       | don't know whether    |                       |
|                       | they refer to the     |                       |
|                       | *same* string. There  |                       |
|                       | are two possible      |                       |
|                       | states, shown in      |                       |
|                       | Figur                 |                       |
|                       | e [10.2](#fig.list1). |                       |
|                       | []{#hevea_default807} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2012.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  10.2: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.list1}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | In one case,          |                       |
|                       | [a]{.c004} and        |                       |
|                       | [b]{.c004} refer to   |                       |
|                       | two different objects |                       |
|                       | that have the same    |                       |
|                       | value. In the second  |                       |
|                       | case, they refer to   |                       |
|                       | the same object.      |                       |
|                       | []{#hevea_default808} |                       |
|                       | []{#hevea_default809} |                       |
|                       |                       |                       |
|                       | To check whether two  |                       |
|                       | variables refer to    |                       |
|                       | the same object, you  |                       |
|                       | can use the           |                       |
|                       | [is]{.c004} operator. |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> a = 'banana'      |                       |
|                       | >>> b = 'banana'      |                       |
|                       | >>> a is b            |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In this example,      |                       |
|                       | Python only created   |                       |
|                       | one string object,    |                       |
|                       | and both [a]{.c004}   |                       |
|                       | and [b]{.c004} refer  |                       |
|                       | to it. But when you   |                       |
|                       | create two lists, you |                       |
|                       | get two objects:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> a = [1, 2, 3]     |                       |
|                       | >>> b = [1, 2, 3]     |                       |
|                       | >>> a is b            |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | So the state diagram  |                       |
|                       | looks like            |                       |
|                       | Figur                 |                       |
|                       | e [10.3](#fig.list2). |                       |
|                       | []{#hevea_default810} |                       |
|                       | []{#hevea_default811} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2013.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  10.3: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.list2}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | In this case we would |                       |
|                       | say that the two      |                       |
|                       | lists are             |                       |
|                       | [equivalent]{.c010},  |                       |
|                       | because they have the |                       |
|                       | same elements, but    |                       |
|                       | not                   |                       |
|                       | [identical]{.c010},   |                       |
|                       | because they are not  |                       |
|                       | the same object. If   |                       |
|                       | two objects are       |                       |
|                       | identical, they are   |                       |
|                       | also equivalent, but  |                       |
|                       | if they are           |                       |
|                       | equivalent, they are  |                       |
|                       | not necessarily       |                       |
|                       | identical.            |                       |
|                       | []{#hevea_default812} |                       |
|                       | []{#hevea_default813} |                       |
|                       |                       |                       |
|                       | Until now, we have    |                       |
|                       | been using "object"   |                       |
|                       | and "value"           |                       |
|                       | interchangeably, but  |                       |
|                       | it is more precise to |                       |
|                       | say that an object    |                       |
|                       | has a value. If you   |                       |
|                       | evaluate [\[1, 2,     |                       |
|                       | 3\]]{.c004}, you get  |                       |
|                       | a list object whose   |                       |
|                       | value is a sequence   |                       |
|                       | of integers. If       |                       |
|                       | another list has the  |                       |
|                       | same elements, we say |                       |
|                       | it has the same       |                       |
|                       | value, but it is not  |                       |
|                       | the same object.      |                       |
|                       | []{#hevea_default814} |                       |
|                       | []{#hevea_default815} |                       |
|                       |                       |                       |
|                       | ## 10.11  Aliasi      |                       |
|                       | ng {#sec124 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default816} |                       |
|                       | []{#hevea_default817} |                       |
|                       |                       |                       |
|                       | If [a]{.c004} refers  |                       |
|                       | to an object and you  |                       |
|                       | assign [b =           |                       |
|                       | a]{.c004}, then both  |                       |
|                       | variables refer to    |                       |
|                       | the same object:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> a = [1, 2, 3]     |                       |
|                       | >>> b = a             |                       |
|                       | >>> b is a            |                       |
|                       | True                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The state diagram     |                       |
|                       | looks like            |                       |
|                       | Figur                 |                       |
|                       | e [10.4](#fig.list3). |                       |
|                       | []{#hevea_default818} |                       |
|                       | []{#hevea_default819} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2014.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  10.4: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.list3}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | The association of a  |                       |
|                       | variable with an      |                       |
|                       | object is called a    |                       |
|                       | [reference]{.c010}.   |                       |
|                       | In this example,      |                       |
|                       | there are two         |                       |
|                       | references to the     |                       |
|                       | same object.          |                       |
|                       | []{#hevea_default820} |                       |
|                       |                       |                       |
|                       | An object with more   |                       |
|                       | than one reference    |                       |
|                       | has more than one     |                       |
|                       | name, so we say that  |                       |
|                       | the object is         |                       |
|                       | [aliased]{.c010}.     |                       |
|                       | []{#hevea_default821} |                       |
|                       |                       |                       |
|                       | If the aliased object |                       |
|                       | is mutable, changes   |                       |
|                       | made with one alias   |                       |
|                       | affect the other:     |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> b[0] = 42         |                       |
|                       | >>> a                 |                       |
|                       | [42, 2, 3]            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Although this         |                       |
|                       | behavior can be       |                       |
|                       | useful, it is         |                       |
|                       | error-prone. In       |                       |
|                       | general, it is safer  |                       |
|                       | to avoid aliasing     |                       |
|                       | when you are working  |                       |
|                       | with mutable objects. |                       |
|                       | []{#hevea_default822} |                       |
|                       |                       |                       |
|                       | For immutable objects |                       |
|                       | like strings,         |                       |
|                       | aliasing is not as    |                       |
|                       | much of a problem. In |                       |
|                       | this example:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | a = 'banana'          |                       |
|                       | b = 'banana'          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | It almost never makes |                       |
|                       | a difference whether  |                       |
|                       | [a]{.c004} and        |                       |
|                       | [b]{.c004} refer to   |                       |
|                       | the same string or    |                       |
|                       | not.                  |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 10.12  List argumen |                       |
|                       | ts {#sec125 .section} |                       |
|                       |                       |                       |
|                       | []{#list.arguments}   |                       |
|                       | []{#hevea_default823} |                       |
|                       | []{#hevea_default824} |                       |
|                       | []{#hevea_default825} |                       |
|                       | []{#hevea_default826} |                       |
|                       | []{#hevea_default827} |                       |
|                       |                       |                       |
|                       | When you pass a list  |                       |
|                       | to a function, the    |                       |
|                       | function gets a       |                       |
|                       | reference to the      |                       |
|                       | list. If the function |                       |
|                       | modifies the list,    |                       |
|                       | the caller sees the   |                       |
|                       | change. For example,  |                       |
|                       | `delete_head` removes |                       |
|                       | the first element     |                       |
|                       | from a list:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def delete_head(t):   |                       |
|                       |     del t[0]          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here's how it is      |                       |
|                       | used:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> lett              |                       |
|                       | ers = ['a', 'b', 'c'] |                       |
|                       | >>>                   |                       |
|                       |  delete_head(letters) |                       |
|                       | >>> letters           |                       |
|                       | ['b', 'c']            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The parameter         |                       |
|                       | [t]{.c004} and the    |                       |
|                       | variable              |                       |
|                       | [letters]{.c004} are  |                       |
|                       | aliases for the same  |                       |
|                       | object. The stack     |                       |
|                       | diagram looks like    |                       |
|                       | Figure                |                       |
|                       |  [10.5](#fig.stack5). |                       |
|                       | []{#hevea_default828} |                       |
|                       | []{#hevea_default829} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2015.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  10.5: Stack diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.stack5}     |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | Since the list is     |                       |
|                       | shared by two frames, |                       |
|                       | I drew it between     |                       |
|                       | them.                 |                       |
|                       |                       |                       |
|                       | It is important to    |                       |
|                       | distinguish between   |                       |
|                       | operations that       |                       |
|                       | modify lists and      |                       |
|                       | operations that       |                       |
|                       | create new lists. For |                       |
|                       | example, the          |                       |
|                       | [append]{.c004}       |                       |
|                       | method modifies a     |                       |
|                       | list, but the         |                       |
|                       | [+]{.c004} operator   |                       |
|                       | creates a new list.   |                       |
|                       | []{#hevea_default830} |                       |
|                       | []{#hevea_default831} |                       |
|                       | []{#hevea_default832} |                       |
|                       | []{#hevea_default833} |                       |
|                       |                       |                       |
|                       | Here's an example     |                       |
|                       | using                 |                       |
|                       | [append]{.c004}:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t1 = [1, 2]       |                       |
|                       | >>> t2 = t1.append(3) |                       |
|                       | >>> t1                |                       |
|                       | [1, 2, 3]             |                       |
|                       | >>> t2                |                       |
|                       | None                  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The return value from |                       |
|                       | [append]{.c004} is    |                       |
|                       | [None]{.c004}.        |                       |
|                       |                       |                       |
|                       | Here's an example     |                       |
|                       | using the [+]{.c004}  |                       |
|                       | operator:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t3 = t1 + [4]     |                       |
|                       | >>> t1                |                       |
|                       | [1, 2, 3]             |                       |
|                       | >>> t3                |                       |
|                       | [1, 2, 3, 4]          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result of the     |                       |
|                       | operator is a new     |                       |
|                       | list, and the         |                       |
|                       | original list is      |                       |
|                       | unchanged.            |                       |
|                       |                       |                       |
|                       | This difference is    |                       |
|                       | important when you    |                       |
|                       | write functions that  |                       |
|                       | are supposed to       |                       |
|                       | modify lists. For     |                       |
|                       | example, this         |                       |
|                       | function *does not*   |                       |
|                       | delete the head of a  |                       |
|                       | list:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | de                    |                       |
|                       | f bad_delete_head(t): |                       |
|                       |     t = t[1:]         |                       |
|                       |              # WRONG! |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The slice operator    |                       |
|                       | creates a new list    |                       |
|                       | and the assignment    |                       |
|                       | makes [t]{.c004}      |                       |
|                       | refer to it, but that |                       |
|                       | doesn't affect the    |                       |
|                       | caller.               |                       |
|                       | []{#hevea_default834} |                       |
|                       | []{#hevea_default835} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t4 = [1, 2, 3]    |                       |
|                       | >>                    |                       |
|                       | > bad_delete_head(t4) |                       |
|                       | >>> t4                |                       |
|                       | [1, 2, 3]             |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | At the beginning of   |                       |
|                       | `bad_delete_head`,    |                       |
|                       | [t]{.c004} and        |                       |
|                       | [t4]{.c004} refer to  |                       |
|                       | the same list. At the |                       |
|                       | end, [t]{.c004}       |                       |
|                       | refers to a new list, |                       |
|                       | but [t4]{.c004} still |                       |
|                       | refers to the         |                       |
|                       | original, unmodified  |                       |
|                       | list.                 |                       |
|                       |                       |                       |
|                       | An alternative is to  |                       |
|                       | write a function that |                       |
|                       | creates and returns a |                       |
|                       | new list. For         |                       |
|                       | example,              |                       |
|                       | [tail]{.c004} returns |                       |
|                       | all but the first     |                       |
|                       | element of a list:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def tail(t):          |                       |
|                       |     return t[1:]      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This function leaves  |                       |
|                       | the original list     |                       |
|                       | unmodified. Here's    |                       |
|                       | how it is used:       |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> lett              |                       |
|                       | ers = ['a', 'b', 'c'] |                       |
|                       | >>>                   |                       |
|                       |  rest = tail(letters) |                       |
|                       | >>> rest              |                       |
|                       | ['b', 'c']            |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 10.13  Debuggi     |                       |
|                       | ng {#sec126 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default836} |                       |
|                       |                       |                       |
|                       | Careless use of lists |                       |
|                       | (and other mutable    |                       |
|                       | objects) can lead to  |                       |
|                       | long hours of         |                       |
|                       | debugging. Here are   |                       |
|                       | some common pitfalls  |                       |
|                       | and ways to avoid     |                       |
|                       | them:                 |                       |
|                       |                       |                       |
|                       | 1.  Most list methods |                       |
|                       |     modify the        |                       |
|                       |     argument and      |                       |
|                       |     return            |                       |
|                       |     [None]{.c004}.    |                       |
|                       |     This is the       |                       |
|                       |     opposite of the   |                       |
|                       |     string methods,   |                       |
|                       |     which return a    |                       |
|                       |     new string and    |                       |
|                       |     leave the         |                       |
|                       |     original alone.   |                       |
|                       |                       |                       |
|                       |     If you are used   |                       |
|                       |     to writing string |                       |
|                       |     code like this:   |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |                       |                       |
|                       |   word = word.strip() |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     It is tempting to |                       |
|                       |     write list code   |                       |
|                       |     like this:        |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |     t = t.sort        |                       |
|                       | ()           # WRONG! |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       | []{#hevea_default837} |                       |
|                       |                       |                       |
|                       | []{#hevea_default838} |                       |
|                       |                       |                       |
|                       |     Because           |                       |
|                       |     [sort]{.c004}     |                       |
|                       |     returns           |                       |
|                       |     [None]{.c004},    |                       |
|                       |     the next          |                       |
|                       |     operation you     |                       |
|                       |     perform with      |                       |
|                       |     [t]{.c004} is     |                       |
|                       |     likely to fail.   |                       |
|                       |                       |                       |
|                       |     Before using list |                       |
|                       |     methods and       |                       |
|                       |     operators, you    |                       |
|                       |     should read the   |                       |
|                       |     documentation     |                       |
|                       |     carefully and     |                       |
|                       |     then test them in |                       |
|                       |     interactive mode. |                       |
|                       |                       |                       |
|                       | 2.  Pick an idiom and |                       |
|                       |     stick with it.    |                       |
|                       |                       |                       |
|                       |     Part of the       |                       |
|                       |     problem with      |                       |
|                       |     lists is that     |                       |
|                       |     there are too     |                       |
|                       |     many ways to do   |                       |
|                       |     things. For       |                       |
|                       |     example, to       |                       |
|                       |     remove an element |                       |
|                       |     from a list, you  |                       |
|                       |     can use           |                       |
|                       |     [pop]{.c004},     |                       |
|                       |     [remove]{.c004},  |                       |
|                       |     [del]{.c004}, or  |                       |
|                       |     even a slice      |                       |
|                       |     assignment.       |                       |
|                       |                       |                       |
|                       |     To add an         |                       |
|                       |     element, you can  |                       |
|                       |     use the           |                       |
|                       |     [append]{.c004}   |                       |
|                       |     method or the     |                       |
|                       |     [+]{.c004}        |                       |
|                       |     operator.         |                       |
|                       |     Assuming that     |                       |
|                       |     [t]{.c004} is a   |                       |
|                       |     list and          |                       |
|                       |     [x]{.c004} is a   |                       |
|                       |     list element,     |                       |
|                       |     these are         |                       |
|                       |     correct:          |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |     t.append(x)       |                       |
|                       |     t = t + [x]       |                       |
|                       |     t += [x]          |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     And these are     |                       |
|                       |     wrong:            |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |     t.append([        |                       |
|                       | x])          # WRONG! |                       |
|                       |     t = t.appe        |                       |
|                       | nd(x)        # WRONG! |                       |
|                       |     t + [x]           |                       |
|                       |              # WRONG! |                       |
|                       |     t = t + x         |                       |
|                       |              # WRONG! |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     Try out each of   |                       |
|                       |     these examples in |                       |
|                       |     interactive mode  |                       |
|                       |     to make sure you  |                       |
|                       |     understand what   |                       |
|                       |     they do. Notice   |                       |
|                       |     that only the     |                       |
|                       |     last one causes a |                       |
|                       |     runtime error;    |                       |
|                       |     the other three   |                       |
|                       |     are legal, but    |                       |
|                       |     they do the wrong |                       |
|                       |     thing.            |                       |
|                       |                       |                       |
|                       | 3.  Make copies to    |                       |
|                       |     avoid aliasing.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default839} |                       |
|                       |                       |                       |
|                       | []{#hevea_default840} |                       |
|                       |                       |                       |
|                       |     If you want to    |                       |
|                       |     use a method like |                       |
|                       |     [sort]{.c004}     |                       |
|                       |     that modifies the |                       |
|                       |     argument, but you |                       |
|                       |     need to keep the  |                       |
|                       |     original list as  |                       |
|                       |     well, you can     |                       |
|                       |     make a copy.      |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |     >>> t = [3, 1, 2] |                       |
|                       |     >>> t2 = t[:]     |                       |
|                       |     >>> t2.sort()     |                       |
|                       |     >>> t             |                       |
|                       |     [3, 1, 2]         |                       |
|                       |     >>> t2            |                       |
|                       |     [1, 2, 3]         |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     In this example   |                       |
|                       |     you could also    |                       |
|                       |     use the built-in  |                       |
|                       |     function          |                       |
|                       |     [sorted]{.c004},  |                       |
|                       |     which returns a   |                       |
|                       |     new, sorted list  |                       |
|                       |     and leaves the    |                       |
|                       |     original alone.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default841} |                       |
|                       |                       |                       |
|                       | []{#hevea_default842} |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |                       |                       |
|                       |    >>> t2 = sorted(t) |                       |
|                       |     >>> t             |                       |
|                       |     [3, 1, 2]         |                       |
|                       |     >>> t2            |                       |
|                       |     [1, 2, 3]         |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       | ## 10.14  Glossa      |                       |
|                       | ry {#sec127 .section} |                       |
|                       |                       |                       |
|                       | [list:]{.c010}        |                       |
|                       | :   A sequence of     |                       |
|                       |     values.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default843} |                       |
|                       |                       |                       |
|                       | [element:]{.c010}     |                       |
|                       | :   One of the values |                       |
|                       |     in a list (or     |                       |
|                       |     other sequence),  |                       |
|                       |     also called       |                       |
|                       |     items.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default844} |                       |
|                       |                       |                       |
|                       | [nested list:]{.c010} |                       |
|                       | :   A list that is an |                       |
|                       |     element of        |                       |
|                       |     another list.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default845} |                       |
|                       |                       |                       |
|                       | [accumulator:]{.c010} |                       |
|                       | :   A variable used   |                       |
|                       |     in a loop to add  |                       |
|                       |     up or accumulate  |                       |
|                       |     a result.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default846} |                       |
|                       |                       |                       |
|                       | [augmente             |                       |
|                       | d assignment:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     updates the value |                       |
|                       |     of a variable     |                       |
|                       |     using an operator |                       |
|                       |     like `+=`.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default847} |                       |
|                       |                       |                       |
|                       | []{#hevea_default848} |                       |
|                       |                       |                       |
|                       | []{#hevea_default849} |                       |
|                       |                       |                       |
|                       | [reduce:]{.c010}      |                       |
|                       | :   A processing      |                       |
|                       |     pattern that      |                       |
|                       |     traverses a       |                       |
|                       |     sequence and      |                       |
|                       |     accumulates the   |                       |
|                       |     elements into a   |                       |
|                       |     single result.    |                       |
|                       |                       |                       |
|                       | []{#hevea_default850} |                       |
|                       |                       |                       |
|                       | []{#hevea_default851} |                       |
|                       |                       |                       |
|                       | [map:]{.c010}         |                       |
|                       | :   A processing      |                       |
|                       |     pattern that      |                       |
|                       |     traverses a       |                       |
|                       |     sequence and      |                       |
|                       |     performs an       |                       |
|                       |     operation on each |                       |
|                       |     element.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default852} |                       |
|                       |                       |                       |
|                       | []{#hevea_default853} |                       |
|                       |                       |                       |
|                       | [filter:]{.c010}      |                       |
|                       | :   A processing      |                       |
|                       |     pattern that      |                       |
|                       |     traverses a list  |                       |
|                       |     and selects the   |                       |
|                       |     elements that     |                       |
|                       |     satisfy some      |                       |
|                       |     criterion.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default854} |                       |
|                       |                       |                       |
|                       | []{#hevea_default855} |                       |
|                       |                       |                       |
|                       | [object:]{.c010}      |                       |
|                       | :   Something a       |                       |
|                       |     variable can      |                       |
|                       |     refer to. An      |                       |
|                       |     object has a type |                       |
|                       |     and a value.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default856} |                       |
|                       |                       |                       |
|                       | [equivalent:]{.c010}  |                       |
|                       | :   Having the same   |                       |
|                       |     value.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default857} |                       |
|                       |                       |                       |
|                       | [identical:]{.c010}   |                       |
|                       | :   Being the same    |                       |
|                       |     object (which     |                       |
|                       |     implies           |                       |
|                       |     equivalence).     |                       |
|                       |                       |                       |
|                       | []{#hevea_default858} |                       |
|                       |                       |                       |
|                       | [reference:]{.c010}   |                       |
|                       | :   The association   |                       |
|                       |     between a         |                       |
|                       |     variable and its  |                       |
|                       |     value.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default859} |                       |
|                       |                       |                       |
|                       | [aliasing:]{.c010}    |                       |
|                       | :   A circumstance    |                       |
|                       |     where two or more |                       |
|                       |     variables refer   |                       |
|                       |     to the same       |                       |
|                       |     object.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default860} |                       |
|                       |                       |                       |
|                       | [delimiter:]{.c010}   |                       |
|                       | :   A character or    |                       |
|                       |     string used to    |                       |
|                       |     indicate where a  |                       |
|                       |     string should be  |                       |
|                       |     split.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default861} |                       |
|                       |                       |                       |
|                       | ## 10.15  Exercis     |                       |
|                       | es {#sec128 .section} |                       |
|                       |                       |                       |
|                       | You can download      |                       |
|                       | solutions to these    |                       |
|                       | exercises from        |                       |
|                       | [                     |                       |
|                       | [https://thinkpython. |                       |
|                       | com/code/list_exercis |                       |
|                       | es.py]{.c004}](https: |                       |
|                       | //thinkpython.com/cod |                       |
|                       | e/list_exercises.py). |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `nested_sum`   |                       |
|                       | that takes a list of  |                       |
|                       | lists of integers and |                       |
|                       | adds up the elements  |                       |
|                       | from all of the       |                       |
|                       | nested lists. For     |                       |
|                       | example:*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [[1           |                       |
|                       | , 2], [3], [4, 5, 6]] |                       |
|                       | >>> nested_sum(t)     |                       |
|                       | 21                    |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#cumulative}       |                       |
|                       | []{#hevea_default862} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called                |                       |
|                       | [cumsum]{.c004} that  |                       |
|                       | takes a list of       |                       |
|                       | numbers and returns   |                       |
|                       | the cumulative sum;   |                       |
|                       | that is, a new list   |                       |
|                       | where the*            |                       |
|                       | [i]{.c009}*th element |                       |
|                       | is the sum of the     |                       |
|                       | first* [i]{.c009}+1   |                       |
|                       | *elements from the    |                       |
|                       | original list. For    |                       |
|                       | example:*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> cumsum(t)         |                       |
|                       | [1, 3, 6]             |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `middle` that  |                       |
|                       | takes a list and      |                       |
|                       | returns a new list    |                       |
|                       | that contains all but |                       |
|                       | the first and last    |                       |
|                       | elements. For         |                       |
|                       | example:*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3, 4]  |                       |
|                       | >>> middle(t)         |                       |
|                       | [2, 3]                |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 4]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `chop` that    |                       |
|                       | takes a list,         |                       |
|                       | modifies it by        |                       |
|                       | removing the first    |                       |
|                       | and last elements,    |                       |
|                       | and returns           |                       |
|                       | [None]{.c004}. For    |                       |
|                       | example:*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3, 4]  |                       |
|                       | >>> chop(t)           |                       |
|                       | >>> t                 |                       |
|                       | [2, 3]                |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       | *Write a function     |                       |
|                       | called `is_sorted`    |                       |
|                       | that takes a list as  |                       |
|                       | a parameter and       |                       |
|                       | returns [True]{.c004} |                       |
|                       | if the list is sorted |                       |
|                       | in ascending order    |                       |
|                       | and [False]{.c004}    |                       |
|                       | otherwise. For        |                       |
|                       | example:*             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       |  is_sorted([1, 2, 2]) |                       |
|                       | True                  |                       |
|                       | >>>                   |                       |
|                       | is_sorted(['b', 'a']) |                       |
|                       | False                 |                       |
|                       | ```                   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 6]{.c010}   |                       |
|                       | []{#anagram}          |                       |
|                       | []{#hevea_default863} |                       |
|                       |                       |                       |
|                       | *Two words are        |                       |
|                       | anagrams if you can   |                       |
|                       | rearrange the letters |                       |
|                       | from one to spell the |                       |
|                       | other. Write a        |                       |
|                       | function called       |                       |
|                       | `is_anagram` that     |                       |
|                       | takes two strings and |                       |
|                       | returns [True]{.c004} |                       |
|                       | if they are           |                       |
|                       | anagrams.*            |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 7]{.c010}   |                       |
|                       | []{#duplicate}        |                       |
|                       | []{#hevea_default864} |                       |
|                       | []{#hevea_default865} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called                |                       |
|                       | `has_duplicates` that |                       |
|                       | takes a list and      |                       |
|                       | returns [True]{.c004} |                       |
|                       | if there is any       |                       |
|                       | element that appears  |                       |
|                       | more than once. It    |                       |
|                       | should not modify the |                       |
|                       | original list.*       |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 8]{.c010}   |                       |
|                       |                       |                       |
|                       | *This exercise        |                       |
|                       | pertains to the       |                       |
|                       | so-called Birthday    |                       |
|                       | Paradox, which you    |                       |
|                       | can read about at*    |                       |
|                       | [*[                   |                       |
|                       | http://en.wikipedia.o |                       |
|                       | rg/wiki/Birthday_para |                       |
|                       | dox]{.c004}*](http:// |                       |
|                       | en.wikipedia.org/wiki |                       |
|                       | /Birthday_paradox)*.* |                       |
|                       | []{#hevea_default866} |                       |
|                       |                       |                       |
|                       | *If there are 23      |                       |
|                       | students in your      |                       |
|                       | class, what are the   |                       |
|                       | chances that two of   |                       |
|                       | them have the same    |                       |
|                       | birthday? You can     |                       |
|                       | estimate this         |                       |
|                       | probability by        |                       |
|                       | generating random     |                       |
|                       | samples of 23         |                       |
|                       | birthdays and         |                       |
|                       | checking for matches. |                       |
|                       | Hint: you can         |                       |
|                       | generate random       |                       |
|                       | birthdays with the    |                       |
|                       | [randint]{.c004}      |                       |
|                       | function in the       |                       |
|                       | [random]{.c004}       |                       |
|                       | module.*              |                       |
|                       | []{#hevea_default867} |                       |
|                       | []{#hevea_default868} |                       |
|                       | []{#hevea_default869} |                       |
|                       | []{#hevea_default870} |                       |
|                       |                       |                       |
|                       | *You can download my  |                       |
|                       | solution from*        |                       |
|                       | [*[https://thi        |                       |
|                       | nkpython.com/code/bir |                       |
|                       | thday.py]{.c004}*](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/birthday.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 9]{.c010}   |                       |
|                       | []{#hevea_default871} |                       |
|                       | []{#hevea_default872} |                       |
|                       | []{#hevea_default873} |                       |
|                       | []{#hevea_default874} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | that reads the file   |                       |
|                       | [words.txt]{.c004}    |                       |
|                       | and builds a list     |                       |
|                       | with one element per  |                       |
|                       | word. Write two       |                       |
|                       | versions of this      |                       |
|                       | function, one using   |                       |
|                       | the [append]{.c004}   |                       |
|                       | method and the other  |                       |
|                       | using the idiom [t =  |                       |
|                       | t + \[x\]]{.c004}.    |                       |
|                       | Which one takes       |                       |
|                       | longer to run? Why?*  |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [[*https://thi        |                       |
|                       | nkpython.com/code/wor |                       |
|                       | dlist.py*]{.c004}](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/wordlist.py)*.* |                       |
|                       | []{#hevea_default875} |                       |
|                       | []{#hevea_default876} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [                     |                       |
|                       | Exercise 10]{.c010}   |                       |
|                       | []{#wordlist1}        |                       |
|                       | []{#bisection}        |                       |
|                       | []{#hevea_default877} |                       |
|                       | []{#hevea_default878} |                       |
|                       | []{#hevea_default879} |                       |
|                       | []{#hevea_default880} |                       |
|                       | []{#hevea_default881} |                       |
|                       | []{#hevea_default882} |                       |
|                       |                       |                       |
|                       | *To check whether a   |                       |
|                       | word is in the word   |                       |
|                       | list, you could use   |                       |
|                       | the [in]{.c004}       |                       |
|                       | operator, but it      |                       |
|                       | would be slow because |                       |
|                       | it searches through   |                       |
|                       | the words in order.*  |                       |
|                       |                       |                       |
|                       | *Because the words    |                       |
|                       | are in alphabetical   |                       |
|                       | order, we can speed   |                       |
|                       | things up with a      |                       |
|                       | bisection search      |                       |
|                       | (also known as binary |                       |
|                       | search), which is     |                       |
|                       | similar to what you   |                       |
|                       | do when you look a    |                       |
|                       | word up in the        |                       |
|                       | dictionary (the book, |                       |
|                       | not the data          |                       |
|                       | structure). You start |                       |
|                       | in the middle and     |                       |
|                       | check to see whether  |                       |
|                       | the word you are      |                       |
|                       | looking for comes     |                       |
|                       | before the word in    |                       |
|                       | the middle of the     |                       |
|                       | list. If so, you      |                       |
|                       | search the first half |                       |
|                       | of the list the same  |                       |
|                       | way. Otherwise you    |                       |
|                       | search the second     |                       |
|                       | half.*                |                       |
|                       |                       |                       |
|                       | *Either way, you cut  |                       |
|                       | the remaining search  |                       |
|                       | space in half. If the |                       |
|                       | word list has 113,809 |                       |
|                       | words, it will take   |                       |
|                       | about 17 steps to     |                       |
|                       | find the word or      |                       |
|                       | conclude that it's    |                       |
|                       | not there.*           |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called `in_bisect`    |                       |
|                       | that takes a sorted   |                       |
|                       | list and a target     |                       |
|                       | value and returns     |                       |
|                       | [True]{.c004} if the  |                       |
|                       | word is in the list   |                       |
|                       | and [False]{.c004} if |                       |
|                       | it's not.*            |                       |
|                       | []{#hevea_default883} |                       |
|                       | []{#hevea_default884} |                       |
|                       |                       |                       |
|                       | *Or you could read    |                       |
|                       | the documentation of  |                       |
|                       | the [bisect]{.c004}   |                       |
|                       | module and use that!  |                       |
|                       | Solution:*            |                       |
|                       | [[*https:/            |                       |
|                       | /thinkpython.com/code |                       |
|                       | /inlist.py*]{.c004}]( |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/inlist.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [                     |                       |
|                       | Exercise 11]{.c010}   |                       |
|                       | []{#hevea_default885} |                       |
|                       |                       |                       |
|                       | *Two words are a      |                       |
|                       | "reverse pair" if     |                       |
|                       | each is the reverse   |                       |
|                       | of the other. Write a |                       |
|                       | program that finds    |                       |
|                       | all the reverse pairs |                       |
|                       | in the word list.     |                       |
|                       | Solution:*            |                       |
|                       | [                     |                       |
|                       | *[https://thinkpython |                       |
|                       | .com/code/reverse_pai |                       |
|                       | r.py]{.c004}*](https: |                       |
|                       | //thinkpython.com/cod |                       |
|                       | e/reverse_pair.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [                     |                       |
|                       | Exercise 12]{.c010}   |                       |
|                       | []{#hevea_default886} |                       |
|                       |                       |                       |
|                       | *Two words            |                       |
|                       | "interlock" if taking |                       |
|                       | alternating letters   |                       |
|                       | from each forms a new |                       |
|                       | word. For example,    |                       |
|                       | "shoe" and "cold"     |                       |
|                       | interlock to form     |                       |
|                       | "schooled".           |                       |
|                       | Solution:*            |                       |
|                       | [*[https://thin       |                       |
|                       | kpython.com/code/inte |                       |
|                       | rlock.py]{.c004}*](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/interlock.py)*. |                       |
|                       | Credit: This exercise |                       |
|                       | is inspired by an     |                       |
|                       | example at*           |                       |
|                       | [*[http://puzz        |                       |
|                       | lers.org]{.c004}*](ht |                       |
|                       | tp://puzzlers.org)*.* |                       |
|                       |                       |                       |
|                       | 1.  *Write a program  |                       |
|                       |     that finds all    |                       |
|                       |     pairs of words    |                       |
|                       |     that interlock.   |                       |
|                       |     Hint: don't       |                       |
|                       |     enumerate all     |                       |
|                       |     pairs!*           |                       |
|                       | 2.  *Can you find any |                       |
|                       |     words that are    |                       |
|                       |     three-way         |                       |
|                       |     interlocked; that |                       |
|                       |     is, every third   |                       |
|                       |     letter forms a    |                       |
|                       |     word, starting    |                       |
|                       |     from the first,   |                       |
|                       |     second or third?* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2010.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2012.html)
---
generator: hevea 2.32
title: Dictionaries
---

[![Previous](back.png)](thinkpython2011.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2013.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # C                   | to support my books,  |
|                       | hapter 11  Dictionari | you can use the       |
|                       | es {#sec129 .chapter} | button below and pay  |
|                       |                       | with PayPal. Thank    |
|                       | This chapter presents | you!                  |
|                       | another built-in type |                       |
|                       | called a dictionary.  |   -----------         |
|                       | Dictionaries are one  | --------------------- |
|                       | of Python's best      | --------------------- |
|                       | features; they are    | --------------------- |
|                       | the building blocks   | --------------------- |
|                       | of many efficient and |   Pay what you want:  |
|                       | elegant algorithms.   |   Small \$1           |
|                       |                       | .00 USD Medium \$5.00 |
|                       | ## 11.1  A            |  USD Large \$10.00 US |
|                       | dictionary is a mappi | D X-Large \$20.00 USD |
|                       | ng {#sec130 .section} |  XX-Large \$50.00 USD |
|                       |                       |   -----------         |
|                       | []{#hevea_default887} | --------------------- |
|                       | []{#hevea_default888} | --------------------- |
|                       | []{#hevea_default889} | --------------------- |
|                       | []{#hevea_default890} | --------------------- |
|                       | []{#hevea_default891} |                       |
|                       | []{#hevea_default892} | ![](                  |
|                       | A [dictionary]{.c010} | https://www.paypalobj |
|                       | is like a list, but   | ects.com/en_US/i/scr/ |
|                       | more general. In a    | pixel.gif){border="0" |
|                       | list, the indices     | width="1" height="1"} |
|                       | have to be integers;  |                       |
|                       | in a dictionary they  | ####                  |
|                       | can be (almost) any   | Are you using one of  |
|                       | type.                 | our books in a class? |
|                       |                       |                       |
|                       | A dictionary contains | We\'d like to know    |
|                       | a collection of       | about it. Please      |
|                       | indices, which are    | consider filling out  |
|                       | called [keys]{.c010}, | [this short           |
|                       | and a collection of   | survey](http://s      |
|                       | values. Each key is   | preadsheets.google.co |
|                       | associated with a     | m/viewform?formkey=dC |
|                       | single value. The     | 0tNUZkMjBEdXVoRGljNm9 |
|                       | association of a key  | FRmlTMHc6MA){onclick= |
|                       | and a value is called | "javascript: pageTrac |
|                       | a [key-value          | ker._trackPageview('/ |
|                       | pair]{.c010} or       | outbound/survey');"}. |
|                       | sometimes an          |                       |
|                       | [item]{.c010}.        | \                     |
|                       | []{#hevea_default893} |                       |
|                       |                       | [Think                |
|                       | In mathematical       | DSP](http             |
|                       | language, a           | ://www.amazon.com/gp/ |
|                       | dictionary represents | product/1491938455/re |
|                       | a [mapping]{.c010}    | f=as_li_tl?ie=UTF8&ca |
|                       | from keys to values,  | mp=1789&creative=9325 |
|                       | so you can also say   | &creativeASIN=1491938 |
|                       | that each key "maps   | 455&linkCode=as2&tag= |
|                       | to" a value. As an    | greenteapre01-20&link |
|                       | example, we'll build  | Id=2JJH4SWCAVVYSQHO){ |
|                       | a dictionary that     | rel="nofollow"}![](ht |
|                       | maps from English to  | tp://ir-na.amazon-ads |
|                       | Spanish words, so the | ystem.com/e/ir?t=gree |
|                       | keys and the values   | nteapre01-20&l=as2&o= |
|                       | are all strings.      | 1&a=1491938455){.c003 |
|                       |                       | width="1" height="1"  |
|                       | The function          | border="0"}           |
|                       | [dict]{.c004} creates |                       |
|                       | a new dictionary with | [                     |
|                       | no items. Because     | ![](http://ws-na.amaz |
|                       | [dict]{.c004} is the  | on-adsystem.com/widge |
|                       | name of a built-in    | ts/q?_encoding=UTF8&A |
|                       | function, you should  | SIN=1491938455&Format |
|                       | avoid using it as a   | =_SL160_&ID=AsinImage |
|                       | variable name.        | &MarketPlace=US&Servi |
|                       | []{#hevea_default894} | ceVersion=20070822&WS |
|                       | []{#hevea_default895} | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | ``` verbatim          | ://www.amazon.com/gp/ |
|                       | >>> eng2sp = dict()   | product/1491938455/re |
|                       | >>> eng2sp            | f=as_li_tl?ie=UTF8&ca |
|                       | {}                    | mp=1789&creative=9325 |
|                       | ```                   | &creativeASIN=1491938 |
|                       |                       | 455&linkCode=as2&tag= |
|                       | The                   | greenteapre01-20&link |
|                       | squiggly-brackets,    | Id=CTV7PDT7E5EGGJUM){ |
|                       | `{}`, represent an    | rel="nofollow"}![](ht |
|                       | empty dictionary. To  | tp://ir-na.amazon-ads |
|                       | add items to the      | ystem.com/e/ir?t=gree |
|                       | dictionary, you can   | nteapre01-20&l=as2&o= |
|                       | use square brackets:  | 1&a=1491938455){.c003 |
|                       | []{#hevea_default896} | width="1" height="1"  |
|                       | []{#hevea_default897} | border="0"}           |
|                       |                       |                       |
|                       | ``` verbatim          | [Think                |
|                       | >>>                   | Java](http            |
|                       | eng2sp['one'] = 'uno' | ://www.amazon.com/gp/ |
|                       | ```                   | product/1491929561/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | This line creates an  | mp=1789&creative=9325 |
|                       | item that maps from   | &creativeASIN=1491929 |
|                       | the key `'one'` to    | 561&linkCode=as2&tag= |
|                       | the value `'uno'`. If | greenteapre01-20&link |
|                       | we print the          | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | dictionary again, we  | rel="nofollow"}![](ht |
|                       | see a key-value pair  | tp://ir-na.amazon-ads |
|                       | with a colon between  | ystem.com/e/ir?t=gree |
|                       | the key and value:    | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | ``` verbatim          | width="1" height="1"  |
|                       | >>> eng2sp            | border="0"}           |
|                       | {'one': 'uno'}        |                       |
|                       | ```                   | [                     |
|                       |                       | ![](http://ws-na.amaz |
|                       | This output format is | on-adsystem.com/widge |
|                       | also an input format. | ts/q?_encoding=UTF8&A |
|                       | For example, you can  | SIN=1491929561&Format |
|                       | create a new          | =_SL160_&ID=AsinImage |
|                       | dictionary with three | &MarketPlace=US&Servi |
|                       | items:                | ceVersion=20070822&WS |
|                       |                       | =1&tag=greenteapre01- |
|                       | ``` verbatim          | 20){border="0"}](http |
|                       | >>> eng2sp = {'o      | ://www.amazon.com/gp/ |
|                       | ne': 'uno', 'two': 'd | product/1491929561/re |
|                       | os', 'three': 'tres'} | f=as_li_tl?ie=UTF8&ca |
|                       | ```                   | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491929 |
|                       | But if you print      | 561&linkCode=as2&tag= |
|                       | [eng2sp]{.c004}, you  | greenteapre01-20&link |
|                       | might be surprised:   | Id=PT77ANWARUNNU3UK){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | ``` verbatim          | tp://ir-na.amazon-ads |
|                       | >>> eng2sp            | ystem.com/e/ir?t=gree |
|                       | {'o                   | nteapre01-20&l=as2&o= |
|                       | ne': 'uno', 'three':  | 1&a=1491929561){.c003 |
|                       | 'tres', 'two': 'dos'} | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | The order of the      | [Think                |
|                       | key-value pairs might | Bay                   |
|                       | not be the same. If   | es](http://www.amazon |
|                       | you type the same     | .com/gp/product/14493 |
|                       | example on your       | 70780/ref=as_li_qf_sp |
|                       | computer, you might   | _asin_tl?ie=UTF8&camp |
|                       | get a different       | =1789&creative=9325&c |
|                       | result. In general,   | reativeASIN=144937078 |
|                       | the order of items in | 0&linkCode=as2&tag=gr |
|                       | a dictionary is       | eenteapre01-20)![](ht |
|                       | unpredictable.        | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | But that's not a      | nteapre01-20&l=as2&o= |
|                       | problem because the   | 1&a=1449370780){.c003 |
|                       | elements of a         | width="1" height="1"  |
|                       | dictionary are never  | border="0"}           |
|                       | indexed with integer  |                       |
|                       | indices. Instead, you | [![](http://ws        |
|                       | use the keys to look  | -na.amazon-adsystem.c |
|                       | up the corresponding  | om/widgets/q?_encodin |
|                       | values:               | g=UTF8&ASIN=144937078 |
|                       |                       | 0&Format=_SL160_&ID=A |
|                       | ``` verbatim          | sinImage&MarketPlace= |
|                       | >>> eng2sp['two']     | US&ServiceVersion=200 |
|                       | 'dos'                 | 70822&WS=1&tag=greent |
|                       | ```                   | eapre01-20){border="0 |
|                       |                       | "}](http://www.amazon |
|                       | The key `'two'`       | .com/gp/product/14493 |
|                       | always maps to the    | 70780/ref=as_li_qf_sp |
|                       | value `'dos'` so the  | _asin_il?ie=UTF8&camp |
|                       | order of the items    | =1789&creative=9325&c |
|                       | doesn't matter.       | reativeASIN=144937078 |
|                       |                       | 0&linkCode=as2&tag=gr |
|                       | If the key isn't in   | eenteapre01-20)![](ht |
|                       | the dictionary, you   | tp://ir-na.amazon-ads |
|                       | get an exception:     | ystem.com/e/ir?t=gree |
|                       | []{#hevea_default898} | nteapre01-20&l=as2&o= |
|                       | []{#hevea_default899} | 1&a=1449370780){.c003 |
|                       |                       | width="1" height="1"  |
|                       | ``` verbatim          | border="0"}           |
|                       | >>> eng2sp['four']    |                       |
|                       | KeyError: 'four'      | [Think Python         |
|                       | ```                   | 2e](http              |
|                       |                       | ://www.amazon.com/gp/ |
|                       | The [len]{.c004}      | product/1491939362/re |
|                       | function works on     | f=as_li_tl?ie=UTF8&ca |
|                       | dictionaries; it      | mp=1789&creative=9325 |
|                       | returns the number of | &creativeASIN=1491939 |
|                       | key-value pairs:      | 362&linkCode=as2&tag= |
|                       | []{#hevea_default900} | greenteapre01-20&link |
|                       | []{#hevea_default901} | Id=FJKSQ3IHEMY2F2VA){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | ``` verbatim          | tp://ir-na.amazon-ads |
|                       | >>> len(eng2sp)       | ystem.com/e/ir?t=gree |
|                       | 3                     | nteapre01-20&l=as2&o= |
|                       | ```                   | 1&a=1491939362){.c003 |
|                       |                       | width="1" height="1"  |
|                       | The [in]{.c004}       | border="0"}           |
|                       | operator works on     |                       |
|                       | dictionaries, too; it | [                     |
|                       | tells you whether     | ![](http://ws-na.amaz |
|                       | something appears as  | on-adsystem.com/widge |
|                       | a *key* in the        | ts/q?_encoding=UTF8&A |
|                       | dictionary (appearing | SIN=1491939362&Format |
|                       | as a value is not     | =_SL160_&ID=AsinImage |
|                       | good enough).         | &MarketPlace=US&Servi |
|                       | []{#hevea_default902} | ceVersion=20070822&WS |
|                       | []{#hevea_default903} | =1&tag=greenteapre01- |
|                       | []{#hevea_default904} | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | ``` verbatim          | product/1491939362/re |
|                       | >>> 'one' in eng2sp   | f=as_li_tl?ie=UTF8&ca |
|                       | True                  | mp=1789&creative=9325 |
|                       | >>> 'uno' in eng2sp   | &creativeASIN=1491939 |
|                       | False                 | 362&linkCode=as2&tag= |
|                       | ```                   | greenteapre01-20&link |
|                       |                       | Id=ZZ454DLQ3IXDHNHX){ |
|                       | To see whether        | rel="nofollow"}![](ht |
|                       | something appears as  | tp://ir-na.amazon-ads |
|                       | a value in a          | ystem.com/e/ir?t=gree |
|                       | dictionary, you can   | nteapre01-20&l=as2&o= |
|                       | use the method        | 1&a=1491939362){.c003 |
|                       | [values]{.c004},      | width="1" height="1"  |
|                       | which returns a       | border="0"}           |
|                       | collection of values, |                       |
|                       | and then use the      | [Think Stats          |
|                       | [in]{.c004} operator: | 2e](http://ww         |
|                       | []{#hevea_default905} | w.amazon.com/gp/produ |
|                       | []{#hevea_default906} | ct/1491907339/ref=as_ |
|                       |                       | li_tl?ie=UTF8&camp=17 |
|                       | ``` verbatim          | 89&creative=9325&crea |
|                       | >>> v                 | tiveASIN=1491907339&l |
|                       | als = eng2sp.values() | inkCode=as2&tag=green |
|                       | >>> 'uno' in vals     | teapre01-20&linkId=O7 |
|                       | True                  | WYM6H6YBYUFNWU)![](ht |
|                       | ```                   | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | The [in]{.c004}       | nteapre01-20&l=as2&o= |
|                       | operator uses         | 1&a=1491907339){.c003 |
|                       | different algorithms  | width="1" height="1"  |
|                       | for lists and         | border="0"}           |
|                       | dictionaries. For     |                       |
|                       | lists, it searches    | [![](h                |
|                       | the elements of the   | ttp://ws-na.amazon-ad |
|                       | list in order, as in  | system.com/widgets/q? |
|                       | Section [8.6](thinkp  | _encoding=UTF8&ASIN=1 |
|                       | ython2009.html#find). | 491907339&Format=_SL1 |
|                       | As the list gets      | 60_&ID=AsinImage&Mark |
|                       | longer, the search    | etPlace=US&ServiceVer |
|                       | time gets longer in   | sion=20070822&WS=1&ta |
|                       | direct proportion.    | g=greenteapre01-20){b |
|                       |                       | order="0"}](http://ww |
|                       | Python dictionaries   | w.amazon.com/gp/produ |
|                       | use a data structure  | ct/1491907339/ref=as_ |
|                       | called a              | li_tl?ie=UTF8&camp=17 |
|                       | [hashtable]{.c010}    | 89&creative=9325&crea |
|                       | that has a remarkable | tiveASIN=1491907339&l |
|                       | property: the         | inkCode=as2&tag=green |
|                       | [in]{.c004} operator  | teapre01-20&linkId=JV |
|                       | takes about the same  | SYKQHYSUIEYRHL)![](ht |
|                       | amount of time no     | tp://ir-na.amazon-ads |
|                       | matter how many items | ystem.com/e/ir?t=gree |
|                       | are in the            | nteapre01-20&l=as2&o= |
|                       | dictionary. I explain | 1&a=1491907339){.c003 |
|                       | how that's possible   | width="1" height="1"  |
|                       | in                    | border="0"}           |
|                       | Sect                  |                       |
|                       | ion [B.4](thinkpython | [Think                |
|                       | 2022.html#hashtable), | Complexity](http      |
|                       | but the explanation   | ://www.amazon.com/gp/ |
|                       | might not make sense  | product/1449314635/re |
|                       | until you've read a   | f=as_li_tf_tl?ie=UTF8 |
|                       | few more chapters.    | &tag=greenteapre01-20 |
|                       |                       | &linkCode=as2&camp=17 |
|                       | ##                    | 89&creative=9325&crea |
|                       | 11.2  Dictionary as a | tiveASIN=1449314635)! |
|                       |  collection of counte | [](http://www.assoc-a |
|                       | rs {#sec131 .section} | mazon.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | []{#histogram}        | 1&a=1449314635){.c003 |
|                       | []{#hevea_default907} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | Suppose you are given |                       |
|                       | a string and you want | [                     |
|                       | to count how many     | ![](http://ws-na.amaz |
|                       | times each letter     | on-adsystem.com/widge |
|                       | appears. There are    | ts/q?_encoding=UTF8&A |
|                       | several ways you      | SIN=1449314635&Format |
|                       | could do it:          | =_SL160_&ID=AsinImage |
|                       |                       | &MarketPlace=US&Servi |
|                       | 1.  You could create  | ceVersion=20070822&WS |
|                       |     26 variables, one | =1&tag=greenteapre01- |
|                       |     for each letter   | 20){border="0"}](http |
|                       |     of the alphabet.  | ://www.amazon.com/gp/ |
|                       |     Then you could    | product/1449314635/re |
|                       |     traverse the      | f=as_li_tf_il?ie=UTF8 |
|                       |     string and, for   | &camp=1789&creative=9 |
|                       |     each character,   | 325&creativeASIN=1449 |
|                       |     increment the     | 314635&linkCode=as2&t |
|                       |     corresponding     | ag=greenteapre01-20)! |
|                       |     counter, probably | [](http://www.assoc-a |
|                       |     using a chained   | mazon.com/e/ir?t=gree |
|                       |     conditional.      | nteapre01-20&l=as2&o= |
|                       | 2.  You could create  | 1&a=1449314635){.c003 |
|                       |     a list with 26    | width="1" height="1"  |
|                       |     elements. Then    | border="0"}           |
|                       |     you could convert |                       |
|                       |     each character to |                       |
|                       |     a number (using   |                       |
|                       |     the built-in      |                       |
|                       |     function          |                       |
|                       |     [ord]{.c004}),    |                       |
|                       |     use the number as |                       |
|                       |     an index into the |                       |
|                       |     list, and         |                       |
|                       |     increment the     |                       |
|                       |     appropriate       |                       |
|                       |     counter.          |                       |
|                       | 3.  You could create  |                       |
|                       |     a dictionary with |                       |
|                       |     characters as     |                       |
|                       |     keys and counters |                       |
|                       |     as the            |                       |
|                       |     corresponding     |                       |
|                       |     values. The first |                       |
|                       |     time you see a    |                       |
|                       |     character, you    |                       |
|                       |     would add an item |                       |
|                       |     to the            |                       |
|                       |     dictionary. After |                       |
|                       |     that you would    |                       |
|                       |     increment the     |                       |
|                       |     value of an       |                       |
|                       |     existing item.    |                       |
|                       |                       |                       |
|                       | Each of these options |                       |
|                       | performs the same     |                       |
|                       | computation, but each |                       |
|                       | of them implements    |                       |
|                       | that computation in a |                       |
|                       | different way.        |                       |
|                       | []{#hevea_default908} |                       |
|                       |                       |                       |
|                       | An                    |                       |
|                       | [i                    |                       |
|                       | mplementation]{.c010} |                       |
|                       | is a way of           |                       |
|                       | performing a          |                       |
|                       | computation; some     |                       |
|                       | implementations are   |                       |
|                       | better than others.   |                       |
|                       | For example, an       |                       |
|                       | advantage of the      |                       |
|                       | dictionary            |                       |
|                       | implementation is     |                       |
|                       | that we don't have to |                       |
|                       | know ahead of time    |                       |
|                       | which letters appear  |                       |
|                       | in the string and we  |                       |
|                       | only have to make     |                       |
|                       | room for the letters  |                       |
|                       | that do appear.       |                       |
|                       |                       |                       |
|                       | Here is what the code |                       |
|                       | might look like:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def histogram(s):     |                       |
|                       |     d = dict()        |                       |
|                       |     for c in s:       |                       |
|                       |                       |                       |
|                       |        if c not in d: |                       |
|                       |             d[c] = 1  |                       |
|                       |         else:         |                       |
|                       |             d[c] += 1 |                       |
|                       |     return d          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The name of the       |                       |
|                       | function is           |                       |
|                       | [histogram]{.c004},   |                       |
|                       | which is a            |                       |
|                       | statistical term for  |                       |
|                       | a collection of       |                       |
|                       | counters (or          |                       |
|                       | frequencies).         |                       |
|                       | []{#hevea_default909} |                       |
|                       | []{#hevea_default910} |                       |
|                       | []{#hevea_default911} |                       |
|                       |                       |                       |
|                       | The first line of the |                       |
|                       | function creates an   |                       |
|                       | empty dictionary. The |                       |
|                       | [for]{.c004} loop     |                       |
|                       | traverses the string. |                       |
|                       | Each time through the |                       |
|                       | loop, if the          |                       |
|                       | character [c]{.c004}  |                       |
|                       | is not in the         |                       |
|                       | dictionary, we create |                       |
|                       | a new item with key   |                       |
|                       | [c]{.c004} and the    |                       |
|                       | initial value 1       |                       |
|                       | (since we have seen   |                       |
|                       | this letter once). If |                       |
|                       | [c]{.c004} is already |                       |
|                       | in the dictionary we  |                       |
|                       | increment             |                       |
|                       | [d\[c\]]{.c004}.      |                       |
|                       | []{#hevea_default912} |                       |
|                       |                       |                       |
|                       | Here's how it works:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> h = hist          |                       |
|                       | ogram('brontosaurus') |                       |
|                       | >>> h                 |                       |
|                       | {                     |                       |
|                       | 'a': 1, 'b': 1, 'o':  |                       |
|                       | 2, 'n': 1, 's': 2, 'r |                       |
|                       | ': 2, 'u': 2, 't': 1} |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The histogram         |                       |
|                       | indicates that the    |                       |
|                       | letters `'a'` and     |                       |
|                       | `'b'` appear once;    |                       |
|                       | `'o'` appears twice,  |                       |
|                       | and so on.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default913} |                       |
|                       | []{#hevea_default914} |                       |
|                       | Dictionaries have a   |                       |
|                       | method called         |                       |
|                       | [get]{.c004} that     |                       |
|                       | takes a key and a     |                       |
|                       | default value. If the |                       |
|                       | key appears in the    |                       |
|                       | dictionary,           |                       |
|                       | [get]{.c004} returns  |                       |
|                       | the corresponding     |                       |
|                       | value; otherwise it   |                       |
|                       | returns the default   |                       |
|                       | value. For example:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >                     |                       |
|                       | >> h = histogram('a') |                       |
|                       | >>> h                 |                       |
|                       | {'a': 1}              |                       |
|                       | >>> h.get('a', 0)     |                       |
|                       | 1                     |                       |
|                       | >>> h.get('c', 0)     |                       |
|                       | 0                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As an exercise, use   |                       |
|                       | [get]{.c004} to write |                       |
|                       | [histogram]{.c004}    |                       |
|                       | more concisely. You   |                       |
|                       | should be able to     |                       |
|                       | eliminate the         |                       |
|                       | [if]{.c004}           |                       |
|                       | statement.            |                       |
|                       |                       |                       |
|                       | ## 11.3  L            |                       |
|                       | ooping and dictionari |                       |
|                       | es {#sec132 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default915} |                       |
|                       | []{#hevea_default916} |                       |
|                       | []{#hevea_default917} |                       |
|                       |                       |                       |
|                       | If you use a          |                       |
|                       | dictionary in a       |                       |
|                       | [for]{.c004}          |                       |
|                       | statement, it         |                       |
|                       | traverses the keys of |                       |
|                       | the dictionary. For   |                       |
|                       | example, `print_hist` |                       |
|                       | prints each key and   |                       |
|                       | the corresponding     |                       |
|                       | value:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_hist(h):    |                       |
|                       |     for c in h:       |                       |
|                       |                       |                       |
|                       |        print(c, h[c]) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here's what the       |                       |
|                       | output looks like:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> h                 |                       |
|                       | = histogram('parrot') |                       |
|                       | >>> print_hist(h)     |                       |
|                       | a 1                   |                       |
|                       | p 1                   |                       |
|                       | r 2                   |                       |
|                       | t 1                   |                       |
|                       | o 1                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Again, the keys are   |                       |
|                       | in no particular      |                       |
|                       | order. To traverse    |                       |
|                       | the keys in sorted    |                       |
|                       | order, you can use    |                       |
|                       | the built-in function |                       |
|                       | [sorted]{.c004}:      |                       |
|                       | []{#hevea_default918} |                       |
|                       | []{#hevea_default919} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | for key in sorted(h): |                       |
|                       | ...                   |                       |
|                       |    print(key, h[key]) |                       |
|                       | a 1                   |                       |
|                       | o 1                   |                       |
|                       | p 1                   |                       |
|                       | r 2                   |                       |
|                       | t 1                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 11.4  Reverse look |                       |
|                       | up {#sec133 .section} |                       |
|                       |                       |                       |
|                       | []{#raise}            |                       |
|                       | []{#hevea_default920} |                       |
|                       | []{#hevea_default921} |                       |
|                       | []{#hevea_default922} |                       |
|                       | []{#hevea_default923} |                       |
|                       |                       |                       |
|                       | Given a dictionary    |                       |
|                       | [d]{.c004} and a key  |                       |
|                       | [k]{.c004}, it is     |                       |
|                       | easy to find the      |                       |
|                       | corresponding value   |                       |
|                       | [v = d\[k\]]{.c004}.  |                       |
|                       | This operation is     |                       |
|                       | called a              |                       |
|                       | [lookup]{.c010}.      |                       |
|                       |                       |                       |
|                       | But what if you have  |                       |
|                       | [v]{.c004} and you    |                       |
|                       | want to find          |                       |
|                       | [k]{.c004}? You have  |                       |
|                       | two problems: first,  |                       |
|                       | there might be more   |                       |
|                       | than one key that     |                       |
|                       | maps to the value     |                       |
|                       | [v]{.c004}. Depending |                       |
|                       | on the application,   |                       |
|                       | you might be able to  |                       |
|                       | pick one, or you      |                       |
|                       | might have to make a  |                       |
|                       | list that contains    |                       |
|                       | all of them. Second,  |                       |
|                       | there is no simple    |                       |
|                       | syntax to do a        |                       |
|                       | [reverse              |                       |
|                       | lookup]{.c010}; you   |                       |
|                       | have to search.       |                       |
|                       |                       |                       |
|                       | Here is a function    |                       |
|                       | that takes a value    |                       |
|                       | and returns the first |                       |
|                       | key that maps to that |                       |
|                       | value:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       | reverse_lookup(d, v): |                       |
|                       |     for k in d:       |                       |
|                       |         if d[k] == v: |                       |
|                       |             return k  |                       |
|                       |                       |                       |
|                       |   raise LookupError() |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This function is yet  |                       |
|                       | another example of    |                       |
|                       | the search pattern,   |                       |
|                       | but it uses a feature |                       |
|                       | we haven't seen       |                       |
|                       | before,               |                       |
|                       | [raise]{.c004}. The   |                       |
|                       | [raise                |                       |
|                       | statement]{.c010}     |                       |
|                       | causes an exception;  |                       |
|                       | in this case it       |                       |
|                       | causes a              |                       |
|                       | [LookupError]{.c004}, |                       |
|                       | which is a built-in   |                       |
|                       | exception used to     |                       |
|                       | indicate that a       |                       |
|                       | lookup operation      |                       |
|                       | failed.               |                       |
|                       | []{#hevea_default924} |                       |
|                       | []{#hevea_default925} |                       |
|                       | []{#hevea_default926} |                       |
|                       | []{#hevea_default927} |                       |
|                       | []{#hevea_default928} |                       |
|                       | []{#hevea_default929} |                       |
|                       |                       |                       |
|                       | If we get to the end  |                       |
|                       | of the loop, that     |                       |
|                       | means [v]{.c004}      |                       |
|                       | doesn't appear in the |                       |
|                       | dictionary as a       |                       |
|                       | value, so we raise an |                       |
|                       | exception.            |                       |
|                       |                       |                       |
|                       | Here is an example of |                       |
|                       | a successful reverse  |                       |
|                       | lookup:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> h                 |                       |
|                       | = histogram('parrot') |                       |
|                       | >>> key =             |                       |
|                       |  reverse_lookup(h, 2) |                       |
|                       | >>> key               |                       |
|                       | 'r'                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And an unsuccessful   |                       |
|                       | one:                  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> key =             |                       |
|                       |  reverse_lookup(h, 3) |                       |
|                       | Traceback (mo         |                       |
|                       | st recent call last): |                       |
|                       |   File "<stdin>"      |                       |
|                       | , line 1, in <module> |                       |
|                       |                       |                       |
|                       |  File "<stdin>", line |                       |
|                       |  5, in reverse_lookup |                       |
|                       | LookupError           |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The effect when you   |                       |
|                       | raise an exception is |                       |
|                       | the same as when      |                       |
|                       | Python raises one: it |                       |
|                       | prints a traceback    |                       |
|                       | and an error message. |                       |
|                       | []{#hevea_default930} |                       |
|                       | []{#hevea_default931} |                       |
|                       | []{#hevea_default932} |                       |
|                       |                       |                       |
|                       | When you raise an     |                       |
|                       | exception, you can    |                       |
|                       | provide a detailed    |                       |
|                       | error message as an   |                       |
|                       | optional argument.    |                       |
|                       | For example:          |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >                     |                       |
|                       | >> raise LookupError( |                       |
|                       | 'value does not appea |                       |
|                       | r in the dictionary') |                       |
|                       | Traceback (mo         |                       |
|                       | st recent call last): |                       |
|                       |   File "<             |                       |
|                       | stdin>", line 1, in ? |                       |
|                       | LookupErro            |                       |
|                       | r: value does not app |                       |
|                       | ear in the dictionary |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A reverse lookup is   |                       |
|                       | much slower than a    |                     