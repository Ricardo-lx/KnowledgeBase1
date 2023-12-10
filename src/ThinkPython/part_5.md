  |
|                       | forward lookup; if    |                       |
|                       | you have to do it     |                       |
|                       | often, or if the      |                       |
|                       | dictionary gets big,  |                       |
|                       | the performance of    |                       |
|                       | your program will     |                       |
|                       | suffer.               |                       |
|                       |                       |                       |
|                       | ## 11.5               |                       |
|                       |  Dictionaries and lis |                       |
|                       | ts {#sec134 .section} |                       |
|                       |                       |                       |
|                       | []{#invert}           |                       |
|                       |                       |                       |
|                       | Lists can appear as   |                       |
|                       | values in a           |                       |
|                       | dictionary. For       |                       |
|                       | example, if you are   |                       |
|                       | given a dictionary    |                       |
|                       | that maps from        |                       |
|                       | letters to            |                       |
|                       | frequencies, you      |                       |
|                       | might want to invert  |                       |
|                       | it; that is, create a |                       |
|                       | dictionary that maps  |                       |
|                       | from frequencies to   |                       |
|                       | letters. Since there  |                       |
|                       | might be several      |                       |
|                       | letters with the same |                       |
|                       | frequency, each value |                       |
|                       | in the inverted       |                       |
|                       | dictionary should be  |                       |
|                       | a list of letters.    |                       |
|                       | []{#hevea_default933} |                       |
|                       | []{#hevea_default934} |                       |
|                       |                       |                       |
|                       | Here is a function    |                       |
|                       | that inverts a        |                       |
|                       | dictionary:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def invert_dict(d):   |                       |
|                       |     inverse = dict()  |                       |
|                       |     for key in d:     |                       |
|                       |         val = d[key]  |                       |
|                       |         i             |                       |
|                       | f val not in inverse: |                       |
|                       |                       |                       |
|                       |  inverse[val] = [key] |                       |
|                       |         else:         |                       |
|                       |             inv       |                       |
|                       | erse[val].append(key) |                       |
|                       |     return inverse    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Each time through the |                       |
|                       | loop, [key]{.c004}    |                       |
|                       | gets a key from       |                       |
|                       | [d]{.c004} and        |                       |
|                       | [val]{.c004} gets the |                       |
|                       | corresponding value.  |                       |
|                       | If [val]{.c004} is    |                       |
|                       | not in                |                       |
|                       | [inverse]{.c004},     |                       |
|                       | that means we haven't |                       |
|                       | seen it before, so we |                       |
|                       | create a new item and |                       |
|                       | initialize it with a  |                       |
|                       | [singleton]{.c010} (a |                       |
|                       | list that contains a  |                       |
|                       | single element).      |                       |
|                       | Otherwise we have     |                       |
|                       | seen this value       |                       |
|                       | before, so we append  |                       |
|                       | the corresponding key |                       |
|                       | to the list.          |                       |
|                       | []{#hevea_default935} |                       |
|                       |                       |                       |
|                       | Here is an example:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> hist              |                       |
|                       | = histogram('parrot') |                       |
|                       | >>> hist              |                       |
|                       | {'a': 1, 'p': 1, 'r   |                       |
|                       | ': 2, 't': 1, 'o': 1} |                       |
|                       | >>> invers            |                       |
|                       | e = invert_dict(hist) |                       |
|                       | >>> inverse           |                       |
|                       | {1: ['a', 'p',        |                       |
|                       |  't', 'o'], 2: ['r']} |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2016.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  11.1: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.dict1}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | Figu                  |                       |
|                       | re [11.1](#fig.dict1) |                       |
|                       | is a state diagram    |                       |
|                       | showing [hist]{.c004} |                       |
|                       | and [inverse]{.c004}. |                       |
|                       | A dictionary is       |                       |
|                       | represented as a box  |                       |
|                       | with the type         |                       |
|                       | [dict]{.c004} above   |                       |
|                       | it and the key-value  |                       |
|                       | pairs inside. If the  |                       |
|                       | values are integers,  |                       |
|                       | floats or strings, I  |                       |
|                       | draw them inside the  |                       |
|                       | box, but I usually    |                       |
|                       | draw lists outside    |                       |
|                       | the box, just to keep |                       |
|                       | the diagram simple.   |                       |
|                       | []{#hevea_default936} |                       |
|                       | []{#hevea_default937} |                       |
|                       |                       |                       |
|                       | Lists can be values   |                       |
|                       | in a dictionary, as   |                       |
|                       | this example shows,   |                       |
|                       | but they cannot be    |                       |
|                       | keys. Here's what     |                       |
|                       | happens if you try:   |                       |
|                       | []{#hevea_default938} |                       |
|                       | []{#hevea_default939} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> d = dict()        |                       |
|                       | >>> d[t] = 'oops'     |                       |
|                       | Traceback (mo         |                       |
|                       | st recent call last): |                       |
|                       |   File "<             |                       |
|                       | stdin>", line 1, in ? |                       |
|                       | TypeError: list o     |                       |
|                       | bjects are unhashable |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | I mentioned earlier   |                       |
|                       | that a dictionary is  |                       |
|                       | implemented using a   |                       |
|                       | hashtable and that    |                       |
|                       | means that the keys   |                       |
|                       | have to be            |                       |
|                       | [hashable]{.c010}.    |                       |
|                       | []{#hevea_default940} |                       |
|                       | []{#hevea_default941} |                       |
|                       |                       |                       |
|                       | A [hash]{.c010} is a  |                       |
|                       | function that takes a |                       |
|                       | value (of any kind)   |                       |
|                       | and returns an        |                       |
|                       | integer. Dictionaries |                       |
|                       | use these integers,   |                       |
|                       | called hash values,   |                       |
|                       | to store and look up  |                       |
|                       | key-value pairs.      |                       |
|                       | []{#hevea_default942} |                       |
|                       |                       |                       |
|                       | This system works     |                       |
|                       | fine if the keys are  |                       |
|                       | immutable. But if the |                       |
|                       | keys are mutable,     |                       |
|                       | like lists, bad       |                       |
|                       | things happen. For    |                       |
|                       | example, when you     |                       |
|                       | create a key-value    |                       |
|                       | pair, Python hashes   |                       |
|                       | the key and stores it |                       |
|                       | in the corresponding  |                       |
|                       | location. If you      |                       |
|                       | modify the key and    |                       |
|                       | then hash it again,   |                       |
|                       | it would go to a      |                       |
|                       | different location.   |                       |
|                       | In that case you      |                       |
|                       | might have two        |                       |
|                       | entries for the same  |                       |
|                       | key, or you might not |                       |
|                       | be able to find a     |                       |
|                       | key. Either way, the  |                       |
|                       | dictionary wouldn't   |                       |
|                       | work correctly.       |                       |
|                       |                       |                       |
|                       | That's why keys have  |                       |
|                       | to be hashable, and   |                       |
|                       | why mutable types     |                       |
|                       | like lists aren't.    |                       |
|                       | The simplest way to   |                       |
|                       | get around this       |                       |
|                       | limitation is to use  |                       |
|                       | tuples, which we will |                       |
|                       | see in the next       |                       |
|                       | chapter.              |                       |
|                       |                       |                       |
|                       | Since dictionaries    |                       |
|                       | are mutable, they     |                       |
|                       | can't be used as      |                       |
|                       | keys, but they *can*  |                       |
|                       | be used as values.    |                       |
|                       |                       |                       |
|                       | ## 11.6  Mem          |                       |
|                       | os {#sec135 .section} |                       |
|                       |                       |                       |
|                       | []{#memoize}          |                       |
|                       |                       |                       |
|                       | If you played with    |                       |
|                       | the                   |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | function from         |                       |
|                       | Section [6.           |                       |
|                       | 7](thinkpython2007.ht |                       |
|                       | ml#one.more.example), |                       |
|                       | you might have        |                       |
|                       | noticed that the      |                       |
|                       | bigger the argument   |                       |
|                       | you provide, the      |                       |
|                       | longer the function   |                       |
|                       | takes to run.         |                       |
|                       | Furthermore, the run  |                       |
|                       | time increases        |                       |
|                       | quickly.              |                       |
|                       | []{#hevea_default943} |                       |
|                       | []{#hevea_default944} |                       |
|                       |                       |                       |
|                       | To understand why,    |                       |
|                       | consider              |                       |
|                       | Figure [1             |                       |
|                       | 1.2](#fig.fibonacci), |                       |
|                       | which shows the [call |                       |
|                       | graph]{.c010} for     |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | with [n=4]{.c004}:    |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2017.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   -----             |                       |
|                       | --------------------- |                       |
|                       | >   Fig               |                       |
|                       | ure 11.2: Call graph. |                       |
|                       | >   -----             |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.fibonacci}  |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | A call graph shows a  |                       |
|                       | set of function       |                       |
|                       | frames, with lines    |                       |
|                       | connecting each frame |                       |
|                       | to the frames of the  |                       |
|                       | functions it calls.   |                       |
|                       | At the top of the     |                       |
|                       | graph,                |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | with [n=4]{.c004}     |                       |
|                       | calls                 |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | with [n=3]{.c004} and |                       |
|                       | [n=2]{.c004}. In      |                       |
|                       | turn,                 |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | with [n=3]{.c004}     |                       |
|                       | calls                 |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | with [n=2]{.c004} and |                       |
|                       | [n=1]{.c004}. And so  |                       |
|                       | on.                   |                       |
|                       | []{#hevea_default945} |                       |
|                       | []{#hevea_default946} |                       |
|                       | []{#hevea_default947} |                       |
|                       |                       |                       |
|                       | Count how many times  |                       |
|                       | [fibonacci(0)]{.c004} |                       |
|                       | and                   |                       |
|                       | [fibonacci(1)]{.c004} |                       |
|                       | are called. This is   |                       |
|                       | an inefficient        |                       |
|                       | solution to the       |                       |
|                       | problem, and it gets  |                       |
|                       | worse as the argument |                       |
|                       | gets bigger.          |                       |
|                       | []{#hevea_default948} |                       |
|                       |                       |                       |
|                       | One solution is to    |                       |
|                       | keep track of values  |                       |
|                       | that have already     |                       |
|                       | been computed by      |                       |
|                       | storing them in a     |                       |
|                       | dictionary. A         |                       |
|                       | previously computed   |                       |
|                       | value that is stored  |                       |
|                       | for later use is      |                       |
|                       | called a              |                       |
|                       | [memo]{.c010}. Here   |                       |
|                       | is a "memoized"       |                       |
|                       | version of            |                       |
|                       | [fibonacci]{.c004}:   |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | known = {0:0, 1:1}    |                       |
|                       |                       |                       |
|                       | def fibonacci(n):     |                       |
|                       |     if n in known:    |                       |
|                       |                       |                       |
|                       |       return known[n] |                       |
|                       |                       |                       |
|                       |     res = fibonacci(  |                       |
|                       | n-1) + fibonacci(n-2) |                       |
|                       |     known[n] = res    |                       |
|                       |     return res        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [known]{.c004} is a   |                       |
|                       | dictionary that keeps |                       |
|                       | track of the          |                       |
|                       | Fibonacci numbers we  |                       |
|                       | already know. It      |                       |
|                       | starts with two       |                       |
|                       | items: 0 maps to 0    |                       |
|                       | and 1 maps to 1.      |                       |
|                       |                       |                       |
|                       | Whenever              |                       |
|                       | [fibonacci]{.c004} is |                       |
|                       | called, it checks     |                       |
|                       | [known]{.c004}. If    |                       |
|                       | the result is already |                       |
|                       | there, it can return  |                       |
|                       | immediately.          |                       |
|                       | Otherwise it has to   |                       |
|                       | compute the new       |                       |
|                       | value, add it to the  |                       |
|                       | dictionary, and       |                       |
|                       | return it.            |                       |
|                       |                       |                       |
|                       | If you run this       |                       |
|                       | version of            |                       |
|                       | [fibonacci]{.c004}    |                       |
|                       | and compare it with   |                       |
|                       | the original, you     |                       |
|                       | will find that it is  |                       |
|                       | much faster.          |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       |  11.7  Global variabl |                       |
|                       | es {#sec136 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default949} |                       |
|                       | []{#hevea_default950} |                       |
|                       |                       |                       |
|                       | In the previous       |                       |
|                       | example,              |                       |
|                       | [known]{.c004} is     |                       |
|                       | created outside the   |                       |
|                       | function, so it       |                       |
|                       | belongs to the        |                       |
|                       | special frame called  |                       |
|                       | `__main__`. Variables |                       |
|                       | in `__main__` are     |                       |
|                       | sometimes called      |                       |
|                       | [global]{.c010}       |                       |
|                       | because they can be   |                       |
|                       | accessed from any     |                       |
|                       | function. Unlike      |                       |
|                       | local variables,      |                       |
|                       | which disappear when  |                       |
|                       | their function ends,  |                       |
|                       | global variables      |                       |
|                       | persist from one      |                       |
|                       | function call to the  |                       |
|                       | next.                 |                       |
|                       | []{#hevea_default951} |                       |
|                       | []{#hevea_default952} |                       |
|                       |                       |                       |
|                       | It is common to use   |                       |
|                       | global variables for  |                       |
|                       | [flags]{.c010}; that  |                       |
|                       | is, boolean variables |                       |
|                       | that indicate         |                       |
|                       | ("flag") whether a    |                       |
|                       | condition is true.    |                       |
|                       | For example, some     |                       |
|                       | programs use a flag   |                       |
|                       | named                 |                       |
|                       | [verbose]{.c004} to   |                       |
|                       | control the level of  |                       |
|                       | detail in the output: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | verbose = True        |                       |
|                       |                       |                       |
|                       | def example1():       |                       |
|                       |     if verbose:       |                       |
|                       |         prin          |                       |
|                       | t('Running example1') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you try to         |                       |
|                       | reassign a global     |                       |
|                       | variable, you might   |                       |
|                       | be surprised. The     |                       |
|                       | following example is  |                       |
|                       | supposed to keep      |                       |
|                       | track of whether the  |                       |
|                       | function has been     |                       |
|                       | called:               |                       |
|                       | []{#hevea_default953} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | been_called = False   |                       |
|                       |                       |                       |
|                       | def example2():       |                       |
|                       |     been_called =     |                       |
|                       |  True         # WRONG |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But if you run it you |                       |
|                       | will see that the     |                       |
|                       | value of              |                       |
|                       | `been_called` doesn't |                       |
|                       | change. The problem   |                       |
|                       | is that               |                       |
|                       | [example2]{.c004}     |                       |
|                       | creates a new local   |                       |
|                       | variable named        |                       |
|                       | `been_called`. The    |                       |
|                       | local variable goes   |                       |
|                       | away when the         |                       |
|                       | function ends, and    |                       |
|                       | has no effect on the  |                       |
|                       | global variable.      |                       |
|                       | []{#hevea_default954} |                       |
|                       | []{#hevea_default955} |                       |
|                       | []{#hevea_default956} |                       |
|                       |                       |                       |
|                       | To reassign a global  |                       |
|                       | variable inside a     |                       |
|                       | function you have to  |                       |
|                       | [declare]{.c010} the  |                       |
|                       | global variable       |                       |
|                       | before you use it:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | been_called = False   |                       |
|                       |                       |                       |
|                       | def example2():       |                       |
|                       |                       |                       |
|                       |   global been_called  |                       |
|                       |                       |                       |
|                       |    been_called = True |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [global           |                       |
|                       | statement]{.c010}     |                       |
|                       | tells the interpreter |                       |
|                       | something like, "In   |                       |
|                       | this function, when I |                       |
|                       | say `been_called`, I  |                       |
|                       | mean the global       |                       |
|                       | variable; don't       |                       |
|                       | create a local one."  |                       |
|                       | []{#hevea_default957} |                       |
|                       | []{#hevea_default958} |                       |
|                       |                       |                       |
|                       | Here's an example     |                       |
|                       | that tries to update  |                       |
|                       | a global variable:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | count = 0             |                       |
|                       |                       |                       |
|                       | def example3():       |                       |
|                       |     count = count     |                       |
|                       |  + 1          # WRONG |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you run it you     |                       |
|                       | get:                  |                       |
|                       | []{#hevea_default959} |                       |
|                       | []{#hevea_default960} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Unbound               |                       |
|                       | LocalError: local var |                       |
|                       | iable 'count' referen |                       |
|                       | ced before assignment |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Python assumes that   |                       |
|                       | [count]{.c004} is     |                       |
|                       | local, and under that |                       |
|                       | assumption you are    |                       |
|                       | reading it before     |                       |
|                       | writing it. The       |                       |
|                       | solution, again, is   |                       |
|                       | to declare            |                       |
|                       | [count]{.c004}        |                       |
|                       | global.               |                       |
|                       | []{#hevea_default961} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def example3():       |                       |
|                       |     global count      |                       |
|                       |     count += 1        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If a global variable  |                       |
|                       | refers to a mutable   |                       |
|                       | value, you can modify |                       |
|                       | the value without     |                       |
|                       | declaring the         |                       |
|                       | variable:             |                       |
|                       | []{#hevea_default962} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | known = {0:0, 1:1}    |                       |
|                       |                       |                       |
|                       | def example4():       |                       |
|                       |     known[2] = 1      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | So you can add,       |                       |
|                       | remove and replace    |                       |
|                       | elements of a global  |                       |
|                       | list or dictionary,   |                       |
|                       | but if you want to    |                       |
|                       | reassign the          |                       |
|                       | variable, you have to |                       |
|                       | declare it:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def example5():       |                       |
|                       |     global known      |                       |
|                       |     known = dict()    |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Global variables can  |                       |
|                       | be useful, but if you |                       |
|                       | have a lot of them,   |                       |
|                       | and you modify them   |                       |
|                       | frequently, they can  |                       |
|                       | make programs hard to |                       |
|                       | debug.                |                       |
|                       |                       |                       |
|                       | ## 11.8  Debuggi      |                       |
|                       | ng {#sec137 .section} |                       |
|                       |                       |                       |
|                       | []{#hevea_default963} |                       |
|                       |                       |                       |
|                       | As you work with      |                       |
|                       | bigger datasets it    |                       |
|                       | can become unwieldy   |                       |
|                       | to debug by printing  |                       |
|                       | and checking the      |                       |
|                       | output by hand. Here  |                       |
|                       | are some suggestions  |                       |
|                       | for debugging large   |                       |
|                       | datasets:             |                       |
|                       |                       |                       |
|                       | [Scale do             |                       |
|                       | wn the input:]{.c010} |                       |
|                       |                       |                       |
|                       | :   If possible,      |                       |
|                       |     reduce the size   |                       |
|                       |     of the dataset.   |                       |
|                       |     For example if    |                       |
|                       |     the program reads |                       |
|                       |     a text file,      |                       |
|                       |     start with just   |                       |
|                       |     the first 10      |                       |
|                       |     lines, or with    |                       |
|                       |     the smallest      |                       |
|                       |     example you can   |                       |
|                       |     find. You can     |                       |
|                       |     either edit the   |                       |
|                       |     files themselves, |                       |
|                       |     or (better)       |                       |
|                       |     modify the        |                       |
|                       |     program so it     |                       |
|                       |     reads only the    |                       |
|                       |     first [n]{.c004}  |                       |
|                       |     lines.            |                       |
|                       |                       |                       |
|                       |     If there is an    |                       |
|                       |     error, you can    |                       |
|                       |     reduce [n]{.c004} |                       |
|                       |     to the smallest   |                       |
|                       |     value that        |                       |
|                       |     manifests the     |                       |
|                       |     error, and then   |                       |
|                       |     increase it       |                       |
|                       |     gradually as you  |                       |
|                       |     find and correct  |                       |
|                       |     errors.           |                       |
|                       |                       |                       |
|                       | [Check summari        |                       |
|                       | es and types:]{.c010} |                       |
|                       |                       |                       |
|                       | :   Instead of        |                       |
|                       |     printing and      |                       |
|                       |     checking the      |                       |
|                       |     entire dataset,   |                       |
|                       |     consider printing |                       |
|                       |     summaries of the  |                       |
|                       |     data: for         |                       |
|                       |     example, the      |                       |
|                       |     number of items   |                       |
|                       |     in a dictionary   |                       |
|                       |     or the total of a |                       |
|                       |     list of numbers.  |                       |
|                       |                       |                       |
|                       |     A common cause of |                       |
|                       |     runtime errors is |                       |
|                       |     a value that is   |                       |
|                       |     not the right     |                       |
|                       |     type. For         |                       |
|                       |     debugging this    |                       |
|                       |     kind of error, it |                       |
|                       |     is often enough   |                       |
|                       |     to print the type |                       |
|                       |     of a value.       |                       |
|                       |                       |                       |
|                       | [Write                |                       |
|                       |  self-checks:]{.c010} |                       |
|                       |                       |                       |
|                       | :   Sometimes you can |                       |
|                       |     write code to     |                       |
|                       |     check for errors  |                       |
|                       |     automatically.    |                       |
|                       |     For example, if   |                       |
|                       |     you are computing |                       |
|                       |     the average of a  |                       |
|                       |     list of numbers,  |                       |
|                       |     you could check   |                       |
|                       |     that the result   |                       |
|                       |     is not greater    |                       |
|                       |     than the largest  |                       |
|                       |     element in the    |                       |
|                       |     list or less than |                       |
|                       |     the smallest.     |                       |
|                       |     This is called a  |                       |
|                       |     "sanity check"    |                       |
|                       |     because it        |                       |
|                       |     detects results   |                       |
|                       |     that are          |                       |
|                       |     "insane".         |                       |
|                       |                       |                       |
|                       | []{#hevea_default964} |                       |
|                       |                       |                       |
|                       | []{#hevea_default965} |                       |
|                       |                       |                       |
|                       |     Another kind of   |                       |
|                       |     check compares    |                       |
|                       |     the results of    |                       |
|                       |     two different     |                       |
|                       |     computations to   |                       |
|                       |     see if they are   |                       |
|                       |     consistent. This  |                       |
|                       |     is called a       |                       |
|                       |     "consistency      |                       |
|                       |     check".           |                       |
|                       |                       |                       |
|                       | [Forma                |                       |
|                       | t the output:]{.c010} |                       |
|                       | :   Formatting        |                       |
|                       |     debugging output  |                       |
|                       |     can make it       |                       |
|                       |     easier to spot an |                       |
|                       |     error. We saw an  |                       |
|                       |     example in        |                       |
|                       |     Sect              |                       |
|                       | ion [6.9](thinkpython |                       |
|                       | 2007.html#factdebug). |                       |
|                       |     Another tool you  |                       |
|                       |     might find useful |                       |
|                       |     is the            |                       |
|                       |     [pprint]{.c004}   |                       |
|                       |     module, which     |                       |
|                       |     provides a        |                       |
|                       |     [pprint]{.c004}   |                       |
|                       |     function that     |                       |
|                       |     displays built-in |                       |
|                       |     types in a more   |                       |
|                       |     human-readable    |                       |
|                       |     format            |                       |
|                       |     ([pprint]{.c004}  |                       |
|                       |     stands for        |                       |
|                       |     "pretty print").  |                       |
|                       |                       |                       |
|                       | []{#hevea_default966} |                       |
|                       |                       |                       |
|                       | []{#hevea_default967} |                       |
|                       |                       |                       |
|                       | []{#hevea_default968} |                       |
|                       |                       |                       |
|                       | Again, time you spend |                       |
|                       | building scaffolding  |                       |
|                       | can reduce the time   |                       |
|                       | you spend debugging.  |                       |
|                       | []{#hevea_default969} |                       |
|                       |                       |                       |
|                       | ## 11.9  Glossa       |                       |
|                       | ry {#sec138 .section} |                       |
|                       |                       |                       |
|                       | [mapping:]{.c010}     |                       |
|                       | :   A relationship in |                       |
|                       |     which each        |                       |
|                       |     element of one    |                       |
|                       |     set corresponds   |                       |
|                       |     to an element of  |                       |
|                       |     another set.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default970} |                       |
|                       |                       |                       |
|                       | [dictionary:]{.c010}  |                       |
|                       | :   A mapping from    |                       |
|                       |     keys to their     |                       |
|                       |     corresponding     |                       |
|                       |     values.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default971} |                       |
|                       |                       |                       |
|                       | [ke                   |                       |
|                       | y-value pair:]{.c010} |                       |
|                       | :   The               |                       |
|                       |     representation of |                       |
|                       |     the mapping from  |                       |
|                       |     a key to a value. |                       |
|                       |                       |                       |
|                       | []{#hevea_default972} |                       |
|                       |                       |                       |
|                       | [item:]{.c010}        |                       |
|                       | :   In a dictionary,  |                       |
|                       |     another name for  |                       |
|                       |     a key-value pair. |                       |
|                       |                       |                       |
|                       | []{#hevea_default973} |                       |
|                       |                       |                       |
|                       | [key:]{.c010}         |                       |
|                       | :   An object that    |                       |
|                       |     appears in a      |                       |
|                       |     dictionary as the |                       |
|                       |     first part of a   |                       |
|                       |     key-value pair.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default974} |                       |
|                       |                       |                       |
|                       | [value:]{.c010}       |                       |
|                       | :   An object that    |                       |
|                       |     appears in a      |                       |
|                       |     dictionary as the |                       |
|                       |     second part of a  |                       |
|                       |     key-value pair.   |                       |
|                       |     This is more      |                       |
|                       |     specific than our |                       |
|                       |     previous use of   |                       |
|                       |     the word "value". |                       |
|                       |                       |                       |
|                       | []{#hevea_default975} |                       |
|                       |                       |                       |
|                       | [im                   |                       |
|                       | plementation:]{.c010} |                       |
|                       | :   A way of          |                       |
|                       |     performing a      |                       |
|                       |     computation.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default976} |                       |
|                       |                       |                       |
|                       | [hashtable:]{.c010}   |                       |
|                       | :   The algorithm     |                       |
|                       |     used to implement |                       |
|                       |     Python            |                       |
|                       |     dictionaries.     |                       |
|                       |                       |                       |
|                       | []{#hevea_default977} |                       |
|                       |                       |                       |
|                       | [h                    |                       |
|                       | ash function:]{.c010} |                       |
|                       | :   A function used   |                       |
|                       |     by a hashtable to |                       |
|                       |     compute the       |                       |
|                       |     location for a    |                       |
|                       |     key.              |                       |
|                       |                       |                       |
|                       | []{#hevea_default978} |                       |
|                       |                       |                       |
|                       | [hashable:]{.c010}    |                       |
|                       | :   A type that has a |                       |
|                       |     hash function.    |                       |
|                       |     Immutable types   |                       |
|                       |     like integers,    |                       |
|                       |     floats and        |                       |
|                       |     strings are       |                       |
|                       |     hashable; mutable |                       |
|                       |     types like lists  |                       |
|                       |     and dictionaries  |                       |
|                       |     are not.          |                       |
|                       |                       |                       |
|                       | []{#hevea_default979} |                       |
|                       |                       |                       |
|                       | [lookup:]{.c010}      |                       |
|                       | :   A dictionary      |                       |
|                       |     operation that    |                       |
|                       |     takes a key and   |                       |
|                       |     finds the         |                       |
|                       |     corresponding     |                       |
|                       |     value.            |                       |
|                       |                       |                       |
|                       | []{#hevea_default980} |                       |
|                       |                       |                       |
|                       | [re                   |                       |
|                       | verse lookup:]{.c010} |                       |
|                       | :   A dictionary      |                       |
|                       |     operation that    |                       |
|                       |     takes a value and |                       |
|                       |     finds one or more |                       |
|                       |     keys that map to  |                       |
|                       |     it.               |                       |
|                       |                       |                       |
|                       | []{#hevea_default981} |                       |
|                       |                       |                       |
|                       | [rai                  |                       |
|                       | se statement:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     (deliberately)    |                       |
|                       |     raises an         |                       |
|                       |     exception.        |                       |
|                       |                       |                       |
|                       | []{#hevea_default982} |                       |
|                       |                       |                       |
|                       | []{#hevea_default983} |                       |
|                       |                       |                       |
|                       | [singleton:]{.c010}   |                       |
|                       | :   A list (or other  |                       |
|                       |     sequence) with a  |                       |
|                       |     single element.   |                       |
|                       |                       |                       |
|                       | []{#hevea_default984} |                       |
|                       |                       |                       |
|                       | [call graph:]{.c010}  |                       |
|                       | :   A diagram that    |                       |
|                       |     shows every frame |                       |
|                       |     created during    |                       |
|                       |     the execution of  |                       |
|                       |     a program, with   |                       |
|                       |     an arrow from     |                       |
|                       |     each caller to    |                       |
|                       |     each callee.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default985} |                       |
|                       |                       |                       |
|                       | []{#hevea_default986} |                       |
|                       |                       |                       |
|                       | [memo:]{.c010}        |                       |
|                       | :   A computed value  |                       |
|                       |     stored to avoid   |                       |
|                       |     unnecessary       |                       |
|                       |     future            |                       |
|                       |     computation.      |                       |
|                       |                       |                       |
|                       | []{#hevea_default987} |                       |
|                       |                       |                       |
|                       | [glo                  |                       |
|                       | bal variable:]{.c010} |                       |
|                       | :   A variable        |                       |
|                       |     defined outside a |                       |
|                       |     function. Global  |                       |
|                       |     variables can be  |                       |
|                       |     accessed from any |                       |
|                       |     function.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default988} |                       |
|                       |                       |                       |
|                       | [glob                 |                       |
|                       | al statement:]{.c010} |                       |
|                       | :   A statement that  |                       |
|                       |     declares a        |                       |
|                       |     variable name     |                       |
|                       |     global.           |                       |
|                       |                       |                       |
|                       | []{#hevea_default989} |                       |
|                       |                       |                       |
|                       | []{#hevea_default990} |                       |
|                       |                       |                       |
|                       | [flag:]{.c010}        |                       |
|                       | :   A boolean         |                       |
|                       |     variable used to  |                       |
|                       |     indicate whether  |                       |
|                       |     a condition is    |                       |
|                       |     true.             |                       |
|                       |                       |                       |
|                       | []{#hevea_default991} |                       |
|                       |                       |                       |
|                       | [declaration:]{.c010} |                       |
|                       | :   A statement like  |                       |
|                       |     [global]{.c004}   |                       |
|                       |     that tells the    |                       |
|                       |     interpreter       |                       |
|                       |     something about a |                       |
|                       |     variable.         |                       |
|                       |                       |                       |
|                       | []{#hevea_default992} |                       |
|                       |                       |                       |
|                       | ## 11.10  Exercis     |                       |
|                       | es {#sec139 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       | []{#wordlist2}        |                       |
|                       | []{#hevea_default993} |                       |
|                       | []{#hevea_default994} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | that reads the words  |                       |
|                       | in [words.txt]{.c004} |                       |
|                       | and stores them as    |                       |
|                       | keys in a dictionary. |                       |
|                       | It doesn't matter     |                       |
|                       | what the values are.  |                       |
|                       | Then you can use the  |                       |
|                       | [in]{.c004} operator  |                       |
|                       | as a fast way to      |                       |
|                       | check whether a       |                       |
|                       | string is in the      |                       |
|                       | dictionary.*          |                       |
|                       |                       |                       |
|                       | *If you did           |                       |
|                       | Exercise              |                       |
|                       |  *[*10*](thinkpython2 |                       |
|                       | 011.html#wordlist1)*, |                       |
|                       | you can compare the   |                       |
|                       | speed of this         |                       |
|                       | implementation with   |                       |
|                       | the list [in]{.c004}  |                       |
|                       | operator and the      |                       |
|                       | bisection search.*    |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#setdefault}       |                       |
|                       |                       |                       |
|                       | *Read the             |                       |
|                       | documentation of the  |                       |
|                       | dictionary method     |                       |
|                       | [setdefault]{.c004}   |                       |
|                       | and use it to write a |                       |
|                       | more concise version  |                       |
|                       | of `invert_dict`.     |                       |
|                       | Solution:*            |                       |
|                       | [[*https://thinkpyth  |                       |
|                       | on.com/code/invert_di |                       |
|                       | ct.py*]{.c004}](https |                       |
|                       | ://thinkpython.com/co |                       |
|                       | de/invert_dict.py)*.* |                       |
|                       | []{#hevea_default995} |                       |
|                       | []{#hevea_default996} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       | *Memoize the          |                       |
|                       | Ackermann function    |                       |
|                       | from                  |                       |
|                       | Exerc                 |                       |
|                       | ise *[*2*](thinkpytho |                       |
|                       | n2007.html#ackermann) |                       |
|                       | *and see if           |                       |
|                       | memoization makes it  |                       |
|                       | possible to evaluate  |                       |
|                       | the function with     |                       |
|                       | bigger arguments.     |                       |
|                       | Hint: no. Solution:*  |                       |
|                       | [[*ht                 |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/ackermann_memo. |                       |
|                       | py*]{.c004}](https:// |                       |
|                       | thinkpython.com/code/ |                       |
|                       | ackermann_memo.py)*.* |                       |
|                       | []{#hevea_default997} |                       |
|                       | []{#hevea_default998} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 4]{.c010}   |                       |
|                       | []{#hevea_default999} |                       |
|                       |                       |                       |
|                       | *If you did           |                       |
|                       | Exercis               |                       |
|                       | e *[*7*](thinkpython2 |                       |
|                       | 011.html#duplicate)*, |                       |
|                       | you already have a    |                       |
|                       | function named        |                       |
|                       | `has_duplicates` that |                       |
|                       | takes a list as a     |                       |
|                       | parameter and returns |                       |
|                       | [True]{.c004} if      |                       |
|                       | there is any object   |                       |
|                       | that appears more     |                       |
|                       | than once in the      |                       |
|                       | list.*                |                       |
|                       |                       |                       |
|                       | *Use a dictionary to  |                       |
|                       | write a faster,       |                       |
|                       | simpler version of    |                       |
|                       | `has_duplicates`.     |                       |
|                       | Solution:*            |                       |
|                       | [[*ht                 |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/has_duplicates. |                       |
|                       | py*]{.c004}](https:// |                       |
|                       | thinkpython.com/code/ |                       |
|                       | has_duplicates.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       | []{#exrotatepairs}    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1000} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1001} |                       |
|                       |                       |                       |
|                       | *Two words are        |                       |
|                       | "rotate pairs" if you |                       |
|                       | can rotate one of     |                       |
|                       | them and get the      |                       |
|                       | other (see            |                       |
|                       | `rotate_word` in      |                       |
|                       | Exercise              |                       |
|                       |  *[*5*](thinkpython20 |                       |
|                       | 09.html#exrotate)*).* |                       |
|                       |                       |                       |
|                       | *Write a program that |                       |
|                       | reads a wordlist and  |                       |
|                       | finds all the rotate  |                       |
|                       | pairs. Solution:*     |                       |
|                       | [                     |                       |
|                       | *[https://thinkpython |                       |
|                       | .com/code/rotate_pair |                       |
|                       | s.py]{.c004}*](https: |                       |
|                       | //thinkpython.com/cod |                       |
|                       | e/rotate_pairs.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 6]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1002} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1003} |                       |
|                       |                       |                       |
|                       | *Here's another       |                       |
|                       | Puzzler from* Car     |                       |
|                       | Talk                  |                       |
|                       | *(*[*[http://www      |                       |
|                       | .cartalk.com/content/ |                       |
|                       | puzzlers]{.c004}*](ht |                       |
|                       | tp://www.cartalk.com/ |                       |
|                       | content/puzzlers)*):* |                       |
|                       |                       |                       |
|                       | > *This was sent in   |                       |
|                       | > by a fellow named   |                       |
|                       | > Dan O'Leary. He     |                       |
|                       | > came upon a common  |                       |
|                       | > one-syllable,       |                       |
|                       | > five-letter word    |                       |
|                       | > recently that has   |                       |
|                       | > the following       |                       |
|                       | > unique property.    |                       |
|                       | > When you remove the |                       |
|                       | > first letter, the   |                       |
|                       | > remaining letters   |                       |
|                       | > form a homophone of |                       |
|                       | > the original word,  |                       |
|                       | > that is a word that |                       |
|                       | > sounds exactly the  |                       |
|                       | > same. Replace the   |                       |
|                       | > first letter, that  |                       |
|                       | > is, put it back and |                       |
|                       | > remove the second   |                       |
|                       | > letter and the      |                       |
|                       | > result is yet       |                       |
|                       | > another homophone   |                       |
|                       | > of the original     |                       |
|                       | > word. And the       |                       |
|                       | > question is, what's |                       |
|                       | > the word?*          |                       |
|                       | >                     |                       |
|                       | > *Now I'm going to   |                       |
|                       | > give you an example |                       |
|                       | > that doesn't work.  |                       |
|                       | > Let's look at the   |                       |
|                       | > five-letter word,   |                       |
|                       | > 'wrack.' W-R-A-C-K, |                       |
|                       | > you know like to    |                       |
|                       | > 'wrack with pain.'  |                       |
|                       | > If I remove the     |                       |
|                       | > first letter, I am  |                       |
|                       | > left with a         |                       |
|                       | > four-letter word,   |                       |
|                       | > 'R-A-C-K.' As in,   |                       |
|                       | > 'Holy cow, did you  |                       |
|                       | > see the rack on     |                       |
|                       | > that buck! It must  |                       |
|                       | > have been a         |                       |
|                       | > nine-pointer!' It's |                       |
|                       | > a perfect           |                       |
|                       | > homophone. If you   |                       |
|                       | > put the 'w' back,   |                       |
|                       | > and remove the 'r,' |                       |
|                       | > instead, you're     |                       |
|                       | > left with the word, |                       |
|                       | > 'wack,' which is a  |                       |
|                       | > real word, it's     |                       |
|                       | > just not a          |                       |
|                       | > homophone of the    |                       |
|                       | > other two words.*   |                       |
|                       | >                     |                       |
|                       | > *But there is,      |                       |
|                       | > however, at least   |                       |
|                       | > one word that Dan   |                       |
|                       | > and we know of,     |                       |
|                       | > which will yield    |                       |
|                       | > two homophones if   |                       |
|                       | > you remove either   |                       |
|                       | > of the first two    |                       |
|                       | > letters to make     |                       |
|                       | > two, new            |                       |
|                       | > four-letter words.  |                       |
|                       | > The question is,    |                       |
|                       | > what's the word?*   |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1004} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1005} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1006} |                       |
|                       |                       |                       |
|                       | *You can use the      |                       |
|                       | dictionary from       |                       |
|                       | Exerci                |                       |
|                       | se *[*1*](#wordlist2) |                       |
|                       | *to check whether a   |                       |
|                       | string is in the word |                       |
|                       | list.*                |                       |
|                       |                       |                       |
|                       | *To check whether two |                       |
|                       | words are homophones, |                       |
|                       | you can use the CMU   |                       |
|                       | Pronouncing           |                       |
|                       | Dictionary. You can   |                       |
|                       | download it from*     |                       |
|                       | [[*http://www.speec   |                       |
|                       | h.cs.cmu.edu/cgi-bin/ |                       |
|                       | cmudict*]{.c004}](htt |                       |
|                       | p://www.speech.cs.cmu |                       |
|                       | .edu/cgi-bin/cmudict) |                       |
|                       | *or from*             |                       |
|                       | [[*https://thinkpy    |                       |
|                       | thon.com/code/c06d*]{ |                       |
|                       | .c004}](https://think |                       |
|                       | python.com/code/c06d) |                       |
|                       | *and you can also     |                       |
|                       | download*             |                       |
|                       | [[*https://thin       |                       |
|                       | kpython.com/code/pron |                       |
|                       | ounce.py*]{.c004}](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/pronounce.py)*, |                       |
|                       | which provides a      |                       |
|                       | function named        |                       |
|                       | `read_dictionary`     |                       |
|                       | that reads the        |                       |
|                       | pronouncing           |                       |
|                       | dictionary and        |                       |
|                       | returns a Python      |                       |
|                       | dictionary that maps  |                       |
|                       | from each word to a   |                       |
|                       | string that describes |                       |
|                       | its primary           |                       |
|                       | pronunciation.*       |                       |
|                       |                       |                       |
|                       | *Write a program that |                       |
|                       | lists all the words   |                       |
|                       | that solve the        |                       |
|                       | Puzzler. Solution:*   |                       |
|                       | [*[https://think      |                       |
|                       | python.com/code/homop |                       |
|                       | hone.py]{.c004}*](htt |                       |
|                       | ps://thinkpython.com/ |                       |
|                       | code/homophone.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2011.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2013.html)
---
generator: hevea 2.32
title: Tuples
---

[![Previous](back.png)](thinkpython2012.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2014.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chapter 12  Tupl    | to support my books,  |
|                       | es {#sec140 .chapter} | you can use the       |
|                       |                       | button below and pay  |
|                       | []{#tuplechap}        | with PayPal. Thank    |
|                       |                       | you!                  |
|                       | This chapter presents |                       |
|                       | one more built-in     |   -----------         |
|                       | type, the tuple, and  | --------------------- |
|                       | then shows how lists, | --------------------- |
|                       | dictionaries, and     | --------------------- |
|                       | tuples work together. | --------------------- |
|                       | I also present a      |   Pay what you want:  |
|                       | useful feature for    |   Small \$1           |
|                       | variable-length       | .00 USD Medium \$5.00 |
|                       | argument lists, the   |  USD Large \$10.00 US |
|                       | gather and scatter    | D X-Large \$20.00 USD |
|                       | operators.            |  XX-Large \$50.00 USD |
|                       |                       |   -----------         |
|                       | One note: there is no | --------------------- |
|                       | consensus on how to   | --------------------- |
|                       | pronounce "tuple".    | --------------------- |
|                       | Some people say       | --------------------- |
|                       | "tuh-ple", which      |                       |
|                       | rhymes with "supple". | ![](                  |
|                       | But in the context of | https://www.paypalobj |
|                       | programming, most     | ects.com/en_US/i/scr/ |
|                       | people say "too-ple", | pixel.gif){border="0" |
|                       | which rhymes with     | width="1" height="1"} |
|                       | "quadruple".          |                       |
|                       |                       | ####                  |
|                       | ## 12.                | Are you using one of  |
|                       | 1  Tuples are immutab | our books in a class? |
|                       | le {#sec141 .section} |                       |
|                       |                       | We\'d like to know    |
|                       | [                     | about it. Please      |
|                       | ]{#hevea_default1007} | consider filling out  |
|                       | [                     | [this short           |
|                       | ]{#hevea_default1008} | survey](http://s      |
|                       | [                     | preadsheets.google.co |
|                       | ]{#hevea_default1009} | m/viewform?formkey=dC |
|                       |                       | 0tNUZkMjBEdXVoRGljNm9 |
|                       | A tuple is a sequence | FRmlTMHc6MA){onclick= |
|                       | of values. The values | "javascript: pageTrac |
|                       | can be any type, and  | ker._trackPageview('/ |
|                       | they are indexed by   | outbound/survey');"}. |
|                       | integers, so in that  |                       |
|                       | respect tuples are a  | \                     |
|                       | lot like lists. The   |                       |
|                       | important difference  | [Think                |
|                       | is that tuples are    | DSP](http             |
|                       | immutable.            | ://www.amazon.com/gp/ |
|                       | [                     | product/1491938455/re |
|                       | ]{#hevea_default1010} | f=as_li_tl?ie=UTF8&ca |
|                       | [                     | mp=1789&creative=9325 |
|                       | ]{#hevea_default1011} | &creativeASIN=1491938 |
|                       |                       | 455&linkCode=as2&tag= |
|                       | Syntactically, a      | greenteapre01-20&link |
|                       | tuple is a            | Id=2JJH4SWCAVVYSQHO){ |
|                       | comma-separated list  | rel="nofollow"}![](ht |
|                       | of values:            | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | ``` verbatim          | nteapre01-20&l=as2&o= |
|                       | >>> t = 'a            | 1&a=1491938455){.c003 |
|                       | ', 'b', 'c', 'd', 'e' | width="1" height="1"  |
|                       | ```                   | border="0"}           |
|                       |                       |                       |
|                       | Although it is not    | [                     |
|                       | necessary, it is      | ![](http://ws-na.amaz |
|                       | common to enclose     | on-adsystem.com/widge |
|                       | tuples in             | ts/q?_encoding=UTF8&A |
|                       | parentheses:          | SIN=1491938455&Format |
|                       | [                     | =_SL160_&ID=AsinImage |
|                       | ]{#hevea_default1012} | &MarketPlace=US&Servi |
|                       |                       | ceVersion=20070822&WS |
|                       | ``` verbatim          | =1&tag=greenteapre01- |
|                       | >>> t = ('a'          | 20){border="0"}](http |
|                       | , 'b', 'c', 'd', 'e') | ://www.amazon.com/gp/ |
|                       | ```                   | product/1491938455/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | To create a tuple     | mp=1789&creative=9325 |
|                       | with a single         | &creativeASIN=1491938 |
|                       | element, you have to  | 455&linkCode=as2&tag= |
|                       | include a final       | greenteapre01-20&link |
|                       | comma:                | Id=CTV7PDT7E5EGGJUM){ |
|                       | [                     | rel="nofollow"}![](ht |
|                       | ]{#hevea_default1013} | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1014} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491938455){.c003 |
|                       | ``` verbatim          | width="1" height="1"  |
|                       | >>> t1 = 'a',         | border="0"}           |
|                       | >>> type(t1)          |                       |
|                       | <class 'tuple'>       | [Think                |
|                       | ```                   | Java](http            |
|                       |                       | ://www.amazon.com/gp/ |
|                       | A value in            | product/1491929561/re |
|                       | parentheses is not a  | f=as_li_tl?ie=UTF8&ca |
|                       | tuple:                | mp=1789&creative=9325 |
|                       |                       | &creativeASIN=1491929 |
|                       | ``` verbatim          | 561&linkCode=as2&tag= |
|                       | >>> t2 = ('a')        | greenteapre01-20&link |
|                       | >>> type(t2)          | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | <class 'str'>         | rel="nofollow"}![](ht |
|                       | ```                   | tp://ir-na.amazon-ads |
|                       |                       | ystem.com/e/ir?t=gree |
|                       | Another way to create | nteapre01-20&l=as2&o= |
|                       | a tuple is the        | 1&a=1491929561){.c003 |
|                       | built-in function     | width="1" height="1"  |
|                       | [tuple]{.c004}. With  | border="0"}           |
|                       | no argument, it       |                       |
|                       | creates an empty      | [                     |
|                       | tuple:                | ![](http://ws-na.amaz |
|                       | [                     | on-adsystem.com/widge |
|                       | ]{#hevea_default1015} | ts/q?_encoding=UTF8&A |
|                       | [                     | SIN=1491929561&Format |
|                       | ]{#hevea_default1016} | =_SL160_&ID=AsinImage |
|                       |                       | &MarketPlace=US&Servi |
|                       | ``` verbatim          | ceVersion=20070822&WS |
|                       | >>> t = tuple()       | =1&tag=greenteapre01- |
|                       | >>> t                 | 20){border="0"}](http |
|                       | ()                    | ://www.amazon.com/gp/ |
|                       | ```                   | product/1491929561/re |
|                       |                       | f=as_li_tl?ie=UTF8&ca |
|                       | If the argument is a  | mp=1789&creative=9325 |
|                       | sequence (string,     | &creativeASIN=1491929 |
|                       | list or tuple), the   | 561&linkCode=as2&tag= |
|                       | result is a tuple     | greenteapre01-20&link |
|                       | with the elements of  | Id=PT77ANWARUNNU3UK){ |
|                       | the sequence:         | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | ``` verbatim          | ystem.com/e/ir?t=gree |
|                       | >>                    | nteapre01-20&l=as2&o= |
|                       | > t = tuple('lupins') | 1&a=1491929561){.c003 |
|                       | >>> t                 | width="1" height="1"  |
|                       | ('l', 'u'             | border="0"}           |
|                       | , 'p', 'i', 'n', 's') |                       |
|                       | ```                   | [Think                |
|                       |                       | Bay                   |
|                       | Because               | es](http://www.amazon |
|                       | [tuple]{.c004} is the | .com/gp/product/14493 |
|                       | name of a built-in    | 70780/ref=as_li_qf_sp |
|                       | function, you should  | _asin_tl?ie=UTF8&camp |
|                       | avoid using it as a   | =1789&creative=9325&c |
|                       | variable name.        | reativeASIN=144937078 |
|                       |                       | 0&linkCode=as2&tag=gr |
|                       | Most list operators   | eenteapre01-20)![](ht |
|                       | also work on tuples.  | tp://ir-na.amazon-ads |
|                       | The bracket operator  | ystem.com/e/ir?t=gree |
|                       | indexes an element:   | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1449370780){.c003 |
|                       | ]{#hevea_default1017} | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1018} |                       |
|                       |                       | [![](http://ws        |
|                       | ``` verbatim          | -na.amazon-adsystem.c |
|                       | >>> t = ('a'          | om/widgets/q?_encodin |
|                       | , 'b', 'c', 'd', 'e') | g=UTF8&ASIN=144937078 |
|                       | >>> t[0]              | 0&Format=_SL160_&ID=A |
|                       | 'a'                   | sinImage&MarketPlace= |
|                       | ```                   | US&ServiceVersion=200 |
|                       |                       | 70822&WS=1&tag=greent |
|                       | And the slice         | eapre01-20){border="0 |
|                       | operator selects a    | "}](http://www.amazon |
|                       | range of elements.    | .com/gp/product/14493 |
|                       | [                     | 70780/ref=as_li_qf_sp |
|                       | ]{#hevea_default1019} | _asin_il?ie=UTF8&camp |
|                       | [                     | =1789&creative=9325&c |
|                       | ]{#hevea_default1020} | reativeASIN=144937078 |
|                       | [                     | 0&linkCode=as2&tag=gr |
|                       | ]{#hevea_default1021} | eenteapre01-20)![](ht |
|                       | [                     | tp://ir-na.amazon-ads |
|                       | ]{#hevea_default1022} | ystem.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1449370780){.c003 |
|                       | >>> t[1:3]            | width="1" height="1"  |
|                       | ('b', 'c')            | border="0"}           |
|                       | ```                   |                       |
|                       |                       | [Think Python         |
|                       | But if you try to     | 2e](http              |
|                       | modify one of the     | ://www.amazon.com/gp/ |
|                       | elements of the       | product/1491939362/re |
|                       | tuple, you get an     | f=as_li_tl?ie=UTF8&ca |
|                       | error:                | mp=1789&creative=9325 |
|                       | [                     | &creativeASIN=1491939 |
|                       | ]{#hevea_default1023} | 362&linkCode=as2&tag= |
|                       | [                     | greenteapre01-20&link |
|                       | ]{#hevea_default1024} | Id=FJKSQ3IHEMY2F2VA){ |
|                       | [                     | rel="nofollow"}![](ht |
|                       | ]{#hevea_default1025} | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1026} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | ``` verbatim          | width="1" height="1"  |
|                       | >>> t[0] = 'A'        | border="0"}           |
|                       | TypeErr               |                       |
|                       | or: object doesn't su | [                     |
|                       | pport item assignment | ![](http://ws-na.amaz |
|                       | ```                   | on-adsystem.com/widge |
|                       |                       | ts/q?_encoding=UTF8&A |
|                       | Because tuples are    | SIN=1491939362&Format |
|                       | immutable, you can't  | =_SL160_&ID=AsinImage |
|                       | modify the elements.  | &MarketPlace=US&Servi |
|                       | But you can replace   | ceVersion=20070822&WS |
|                       | one tuple with        | =1&tag=greenteapre01- |
|                       | another:              | 20){border="0"}](http |
|                       |                       | ://www.amazon.com/gp/ |
|                       | ``` verbatim          | product/1491939362/re |
|                       | >                     | f=as_li_tl?ie=UTF8&ca |
|                       | >> t = ('A',) + t[1:] | mp=1789&creative=9325 |
|                       | >>> t                 | &creativeASIN=1491939 |
|                       | ('A'                  | 362&linkCode=as2&tag= |
|                       | , 'b', 'c', 'd', 'e') | greenteapre01-20&link |
|                       | ```                   | Id=ZZ454DLQ3IXDHNHX){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | This statement makes  | tp://ir-na.amazon-ads |
|                       | a new tuple and then  | ystem.com/e/ir?t=gree |
|                       | makes [t]{.c004}      | nteapre01-20&l=as2&o= |
|                       | refer to it.          | 1&a=1491939362){.c003 |
|                       |                       | width="1" height="1"  |
|                       | The relational        | border="0"}           |
|                       | operators work with   |                       |
|                       | tuples and other      | [Think Stats          |
|                       | sequences; Python     | 2e](http://ww         |
|                       | starts by comparing   | w.amazon.com/gp/produ |
|                       | the first element     | ct/1491907339/ref=as_ |
|                       | from each sequence.   | li_tl?ie=UTF8&camp=17 |
|                       | If they are equal, it | 89&creative=9325&crea |
|                       | goes on to the next   | tiveASIN=1491907339&l |
|                       | elements, and so on,  | inkCode=as2&tag=green |
|                       | until it finds        | teapre01-20&linkId=O7 |
|                       | elements that differ. | WYM6H6YBYUFNWU)![](ht |
|                       | Subsequent elements   | tp://ir-na.amazon-ads |
|                       | are not considered    | ystem.com/e/ir?t=gree |
|                       | (even if they are     | nteapre01-20&l=as2&o= |
|                       | really big).          | 1&a=1491907339){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1027} | border="0"}           |
|                       | [                     |                       |
|                       | ]{#hevea_default1028} | [![](h                |
|                       |                       | ttp://ws-na.amazon-ad |
|                       | ``` verbatim          | system.com/widgets/q? |
|                       | >>>                   | _encoding=UTF8&ASIN=1 |
|                       | (0, 1, 2) < (0, 3, 4) | 491907339&Format=_SL1 |
|                       | True                  | 60_&ID=AsinImage&Mark |
|                       | >>> (0, 1,            | etPlace=US&ServiceVer |
|                       |  2000000) < (0, 3, 4) | sion=20070822&WS=1&ta |
|                       | True                  | g=greenteapre01-20){b |
|                       | ```                   | order="0"}](http://ww |
|                       |                       | w.amazon.com/gp/produ |
|                       | ##                    | ct/1491907339/ref=as_ |
|                       |  12.2  Tuple assignme | li_tl?ie=UTF8&camp=17 |
|                       | nt {#sec142 .section} | 89&creative=9325&crea |
|                       |                       | tiveASIN=1491907339&l |
|                       | []{#tuple.assignment} | inkCode=as2&tag=green |
|                       | [                     | teapre01-20&linkId=JV |
|                       | ]{#hevea_default1029} | SYKQHYSUIEYRHL)![](ht |
|                       | [                     | tp://ir-na.amazon-ads |
|                       | ]{#hevea_default1030} | ystem.com/e/ir?t=gree |
|                       | [                     | nteapre01-20&l=as2&o= |
|                       | ]{#hevea_default1031} | 1&a=1491907339){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1032} | border="0"}           |
|                       |                       |                       |
|                       | It is often useful to | [Think                |
|                       | swap the values of    | Complexity](http      |
|                       | two variables. With   | ://www.amazon.com/gp/ |
|                       | conventional          | product/1449314635/re |
|                       | assignments, you have | f=as_li_tf_tl?ie=UTF8 |
|                       | to use a temporary    | &tag=greenteapre01-20 |
|                       | variable. For         | &linkCode=as2&camp=17 |
|                       | example, to swap      | 89&creative=9325&crea |
|                       | [a]{.c004} and        | tiveASIN=1449314635)! |
|                       | [b]{.c004}:           | [](http://www.assoc-a |
|                       |                       | mazon.com/e/ir?t=gree |
|                       | ``` verbatim          | nteapre01-20&l=as2&o= |
|                       | >>> temp = a          | 1&a=1449314635){.c003 |
|                       | >>> a = b             | width="1" height="1"  |
|                       | >>> b = temp          | border="0"}           |
|                       | ```                   |                       |
|                       |                       | [                     |
|                       | This solution is      | ![](http://ws-na.amaz |
|                       | cumbersome; [tuple    | on-adsystem.com/widge |
|                       | assignment]{.c010} is | ts/q?_encoding=UTF8&A |
|                       | more elegant:         | SIN=1449314635&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | ``` verbatim          | &MarketPlace=US&Servi |
|                       | >>> a, b = b, a       | ceVersion=20070822&WS |
|                       | ```                   | =1&tag=greenteapre01- |
|                       |                       | 20){border="0"}](http |
|                       | The left side is a    | ://www.amazon.com/gp/ |
|                       | tuple of variables;   | product/1449314635/re |
|                       | the right side is a   | f=as_li_tf_il?ie=UTF8 |
|                       | tuple of expressions. | &camp=1789&creative=9 |
|                       | Each value is         | 325&creativeASIN=1449 |
|                       | assigned to its       | 314635&linkCode=as2&t |
|                       | respective variable.  | ag=greenteapre01-20)! |
|                       | All the expressions   | [](http://www.assoc-a |
|                       | on the right side are | mazon.com/e/ir?t=gree |
|                       | evaluated before any  | nteapre01-20&l=as2&o= |
|                       | of the assignments.   | 1&a=1449314635){.c003 |
|                       |                       | width="1" height="1"  |
|                       | The number of         | border="0"}           |
|                       | variables on the left |                       |
|                       | and the number of     |                       |
|                       | values on the right   |                       |
|                       | have to be the same:  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1033} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1034} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> a, b = 1, 2, 3    |                       |
|                       | ValueError: too       |                       |
|                       | many values to unpack |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | More generally, the   |                       |
|                       | right side can be any |                       |
|                       | kind of sequence      |                       |
|                       | (string, list or      |                       |
|                       | tuple). For example,  |                       |
|                       | to split an email     |                       |
|                       | address into a user   |                       |
|                       | name and a domain,    |                       |
|                       | you could write:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1035} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1036} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1037} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> addr              |                       |
|                       |  = 'monty@python.org' |                       |
|                       | >>> uname, dom        |                       |
|                       | ain = addr.split('@') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The return value from |                       |
|                       | [split]{.c004} is a   |                       |
|                       | list with two         |                       |
|                       | elements; the first   |                       |
|                       | element is assigned   |                       |
|                       | to [uname]{.c004},    |                       |
|                       | the second to         |                       |
|                       | [domain]{.c004}.      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> uname             |                       |
|                       | 'monty'               |                       |
|                       | >>> domain            |                       |
|                       | 'python.org'          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ## 12.3               |                       |
|                       | Tuples as return valu |                       |
|                       | es {#sec143 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1038} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1039} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1040} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1041} |                       |
|                       |                       |                       |
|                       | Strictly speaking, a  |                       |
|                       | function can only     |                       |
|                       | return one value, but |                       |
|                       | if the value is a     |                       |
|                       | tuple, the effect is  |                       |
|                       | the same as returning |                       |
|                       | multiple values. For  |                       |
|                       | example, if you want  |                       |
|                       | to divide two         |                       |
|                       | integers and compute  |                       |
|                       | the quotient and      |                       |
|                       | remainder, it is      |                       |
|                       | inefficient to        |                       |
|                       | compute [x//y]{.c004} |                       |
|                       | and then              |                       |
|                       | [x%y]{.c004}. It is   |                       |
|                       | better to compute     |                       |
|                       | them both at the same |                       |
|                       | time.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1042} |                       |
|                       |                       |                       |
|                       | The built-in function |                       |
|                       | [divmod]{.c004} takes |                       |
|                       | two arguments and     |                       |
|                       | returns a tuple of    |                       |
|                       | two values, the       |                       |
|                       | quotient and          |                       |
|                       | remainder. You can    |                       |
|                       | store the result as a |                       |
|                       | tuple:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = divmod(7, 3)  |                       |
|                       | >>> t                 |                       |
|                       | (2, 1)                |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Or use tuple          |                       |
|                       | assignment to store   |                       |
|                       | the elements          |                       |
|                       | separately:           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1043} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1044} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> quo               |                       |
|                       | t, rem = divmod(7, 3) |                       |
|                       | >>> quot              |                       |
|                       | 2                     |                       |
|                       | >>> rem               |                       |
|                       | 1                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here is an example of |                       |
|                       | a function that       |                       |
|                       | returns a tuple:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def min_max(t):       |                       |
|                       |                       |                       |
|                       | return min(t), max(t) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [max]{.c004} and      |                       |
|                       | [min]{.c004} are      |                       |
|                       | built-in functions    |                       |
|                       | that find the largest |                       |
|                       | and smallest elements |                       |
|                       | of a sequence.        |                       |
|                       | `min_max` computes    |                       |
|                       | both and returns a    |                       |
|                       | tuple of two values.  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1045} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1046} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1047} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1048} |                       |
|                       |                       |                       |
|                       | ## 12.4  Variable     |                       |
|                       | -length argument tupl |                       |
|                       | es {#sec144 .section} |                       |
|                       |                       |                       |
|                       | []{#gather}           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1049} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1050} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1051} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1052} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1053} |                       |
|                       |                       |                       |
|                       | Functions can take a  |                       |
|                       | variable number of    |                       |
|                       | arguments. A          |                       |
|                       | parameter name that   |                       |
|                       | begins with           |                       |
|                       | [\*]{.c004}           |                       |
|                       | [gathers]{.c010}      |                       |
|                       | arguments into a      |                       |
|                       | tuple. For example,   |                       |
|                       | [printall]{.c004}     |                       |
|                       | takes any number of   |                       |
|                       | arguments and prints  |                       |
|                       | them:                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def printall(*args):  |                       |
|                       |     print(args)       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The gather parameter  |                       |
|                       | can have any name you |                       |
|                       | like, but             |                       |
|                       | [args]{.c004} is      |                       |
|                       | conventional. Here's  |                       |
|                       | how the function      |                       |
|                       | works:                |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | printall(1, 2.0, '3') |                       |
|                       | (1, 2.0, '3')         |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The complement of     |                       |
|                       | gather is             |                       |
|                       | [scatter]{.c010}. If  |                       |
|                       | you have a sequence   |                       |
|                       | of values and you     |                       |
|                       | want to pass it to a  |                       |
|                       | function as multiple  |                       |
|                       | arguments, you can    |                       |
|                       | use the [\*]{.c004}   |                       |
|                       | operator. For         |                       |
|                       | example,              |                       |
|                       | [divmod]{.c004} takes |                       |
|                       | exactly two           |                       |
|                       | arguments; it doesn't |                       |
|                       | work with a tuple:    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1054} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1055} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1056} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1057} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = (7, 3)        |                       |
|                       | >>> divmod(t)         |                       |
|                       | Typ                   |                       |
|                       | eError: divmod expect |                       |
|                       | ed 2 arguments, got 1 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But if you scatter    |                       |
|                       | the tuple, it works:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> divmod(*t)        |                       |
|                       | (2, 1)                |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Many of the built-in  |                       |
|                       | functions use         |                       |
|                       | variable-length       |                       |
|                       | argument tuples. For  |                       |
|                       | example, [max]{.c004} |                       |
|                       | and [min]{.c004} can  |                       |
|                       | take any number of    |                       |
|                       | arguments:            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1058} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1059} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1060} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1061} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> max(1, 2, 3)      |                       |
|                       | 3                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | But [sum]{.c004} does |                       |
|                       | not.                  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1062} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1063} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> sum(1, 2, 3)      |                       |
|                       | TypeErro              |                       |
|                       | r: sum expected at mo |                       |
|                       | st 2 arguments, got 3 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As an exercise, write |                       |
|                       | a function called     |                       |
|                       | `sum_all` that takes  |                       |
|                       | any number of         |                       |
|                       | arguments and returns |                       |
|                       | their sum.            |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       |  12.5  Lists and tupl |                       |
|                       | es {#sec145 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1064} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1065} |                       |
|                       |                       |                       |
|                       | [zip]{.c004} is a     |                       |
|                       | built-in function     |                       |
|                       | that takes two or     |                       |
|                       | more sequences and    |                       |
|                       | interleaves them. The |                       |
|                       | name of the function  |                       |
|                       | refers to a zipper,   |                       |
|                       | which interleaves two |                       |
|                       | rows of teeth.        |                       |
|                       |                       |                       |
|                       | This example zips a   |                       |
|                       | string and a list:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> s = 'abc'         |                       |
|                       | >>> t = [0, 1, 2]     |                       |
|                       | >>> zip(s, t)         |                       |
|                       | <zip obje             |                       |
|                       | ct at 0x7f7d0a9e7c48> |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result is a [zip  |                       |
|                       | object]{.c010} that   |                       |
|                       | knows how to iterate  |                       |
|                       | through the pairs.    |                       |
|                       | The most common use   |                       |
|                       | of [zip]{.c004} is in |                       |
|                       | a [for]{.c004} loop:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> f                 |                       |
|                       | or pair in zip(s, t): |                       |
|                       | ...     print(pair)   |                       |
|                       | ...                   |                       |
|                       | ('a', 0)              |                       |
|                       | ('b', 1)              |                       |
|                       | ('c', 2)              |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A zip object is a     |                       |
|                       | kind of               |                       |
|                       | [iterator]{.c010},    |                       |
|                       | which is any object   |                       |
|                       | that iterates through |                       |
|                       | a sequence. Iterators |                       |
|                       | are similar to lists  |                       |
|                       | in some ways, but     |                       |
|                       | unlike lists, you     |                       |
|                       | can't use an index to |                       |
|                       | select an element     |                       |
|                       | from an iterator.     |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1066} |                       |
|                       |                       |                       |
|                       | If you want to use    |                       |
|                       | list operators and    |                       |
|                       | methods, you can use  |                       |
|                       | a zip object to make  |                       |
|                       | a list:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> list(zip(s, t))   |                       |
|                       | [('a', 0)             |                       |
|                       | , ('b', 1), ('c', 2)] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result is a list  |                       |
|                       | of tuples; in this    |                       |
|                       | example, each tuple   |                       |
|                       | contains a character  |                       |
|                       | from the string and   |                       |
|                       | the corresponding     |                       |
|                       | element from the      |                       |
|                       | list.                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1067} |                       |
|                       |                       |                       |
|                       | If the sequences are  |                       |
|                       | not the same length,  |                       |
|                       | the result has the    |                       |
|                       | length of the shorter |                       |
|                       | one.                  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> lis               |                       |
|                       | t(zip('Anne', 'Elk')) |                       |
|                       | [('A', 'E'), ('       |                       |
|                       | n', 'l'), ('n', 'k')] |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | You can use tuple     |                       |
|                       | assignment in a       |                       |
|                       | [for]{.c004} loop to  |                       |
|                       | traverse a list of    |                       |
|                       | tuples:               |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1068} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1069} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1070} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | t = [('a', 0)         |                       |
|                       | , ('b', 1), ('c', 2)] |                       |
|                       | for                   |                       |
|                       |  letter, number in t: |                       |
|                       |                       |                       |
|                       | print(number, letter) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Each time through the |                       |
|                       | loop, Python selects  |                       |
|                       | the next tuple in the |                       |
|                       | list and assigns the  |                       |
|                       | elements to           |                       |
|                       | [letter]{.c004} and   |                       |
|                       | [number]{.c004}. The  |                       |
|                       | output of this loop   |                       |
|                       | is:                   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1071} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | 0 a                   |                       |
|                       | 1 b                   |                       |
|                       | 2 c                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you combine        |                       |
|                       | [zip]{.c004},         |                       |
|                       | [for]{.c004} and      |                       |
|                       | tuple assignment, you |                       |
|                       | get a useful idiom    |                       |
|                       | for traversing two    |                       |
|                       | (or more) sequences   |                       |
|                       | at the same time. For |                       |
|                       | example, `has_match`  |                       |
|                       | takes two sequences,  |                       |
|                       | [t1]{.c004} and       |                       |
|                       | [t2]{.c004}, and      |                       |
|                       | returns [True]{.c004} |                       |
|                       | if there is an index  |                       |
|                       | [i]{.c004} such that  |                       |
|                       | [t1\[i\] ==           |                       |
|                       | t2\[i\]]{.c004}:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1072} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef has_match(t1, t2): |                       |
|                       |     for               |                       |
|                       |  x, y in zip(t1, t2): |                       |
|                       |         if x == y:    |                       |
|                       |                       |                       |
|                       |           return True |                       |
|                       |     return False      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you need to        |                       |
|                       | traverse the elements |                       |
|                       | of a sequence and     |                       |
|                       | their indices, you    |                       |
|                       | can use the built-in  |                       |
|                       | function              |                       |
|                       | [enumerate]{.c004}:   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1073} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1074} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1075} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | for index, element    |                       |
|                       |  in enumerate('abc'): |                       |
|                       |                       |                       |
|                       | print(index, element) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result from       |                       |
|                       | [enumerate]{.c004} is |                       |
|                       | an enumerate object,  |                       |
|                       | which iterates a      |                       |
|                       | sequence of pairs;    |                       |
|                       | each pair contains an |                       |
|                       | index (starting from  |                       |
|                       | 0) and an element     |                       |
|                       | from the given        |                       |
|                       | sequence. In this     |                       |
|                       | example, the output   |                       |
|                       | is                    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | 0 a                   |                       |
|                       | 1 b                   |                       |
|                       | 2 c                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Again.                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1076} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1077} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1078} |                       |
|                       |                       |                       |
|                       | ## 12.6               |                       |
|                       | Dictionaries and tupl |                       |
|                       | es {#sec146 .section} |                       |
|                       |                       |                       |
|                       | []{#dictuple}         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1079} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1080} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1081} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1082} |                       |
|                       |                       |                       |
|                       | Dictionaries have a   |                       |
|                       | method called         |                       |
|                       | [items]{.c004} that   |                       |
|                       | returns a sequence of |                       |
|                       | tuples, where each    |                       |
|                       | tuple is a key-value  |                       |
|                       | pair.                 |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> d =               |                       |
|                       | {'a':0, 'b':1, 'c':2} |                       |
|                       | >>> t = d.items()     |                       |
|                       | >>> t                 |                       |
|                       | dict_items([('c', 2), |                       |
|                       |  ('a', 0), ('b', 1)]) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The result is a       |                       |
|                       | `dict_items` object,  |                       |
|                       | which is an iterator  |                       |
|                       | that iterates the     |                       |
|                       | key-value pairs. You  |                       |
|                       | can use it in a       |                       |
|                       | [for]{.c004} loop     |                       |
|                       | like this:            |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1083} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> for key           |                       |
|                       | , value in d.items(): |                       |
|                       | ...                   |                       |
|                       |     print(key, value) |                       |
|                       | ...                   |                       |
|                       | c 2                   |                       |
|                       | a 0                   |                       |
|                       | b 1                   |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | As you should expect  |                       |
|                       | from a dictionary,    |                       |
|                       | the items are in no   |                       |
|                       | particular order.     |                       |
|                       |                       |                       |
|                       | Going in the other    |                       |
|                       | direction, you can    |                       |
|                       | use a list of tuples  |                       |
|                       | to initialize a new   |                       |
|                       | dictionary:           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1084} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [('a', 0)     |                       |
|                       | , ('c', 2), ('b', 1)] |                       |
|                       | >>> d = dict(t)       |                       |
|                       | >>> d                 |                       |
|                       | {'a                   |                       |
|                       | ': 0, 'c': 2, 'b': 1} |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Combining             |                       |
|                       | [dict]{.c004} with    |                       |
|                       | [zip]{.c004} yields a |                       |
|                       | concise way to create |                       |
|                       | a dictionary:         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1085} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> d = dict(         |                       |
|                       | zip('abc', range(3))) |                       |
|                       | >>> d                 |                       |
|                       | {'a                   |                       |
|                       | ': 0, 'c': 2, 'b': 1} |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The dictionary method |                       |
|                       | [update]{.c004} also  |                       |
|                       | takes a list of       |                       |
|                       | tuples and adds them, |                       |
|                       | as key-value pairs,   |                       |
|                       | to an existing        |                       |
|                       | dictionary.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1086} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1087} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1088} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1089} |                       |
|                       |                       |                       |
|                       | It is common to use   |                       |
|                       | tuples as keys in     |                       |
|                       | dictionaries          |                       |
|                       | (primarily because    |                       |
|                       | you can't use lists). |                       |
|                       | For example, a        |                       |
|                       | telephone directory   |                       |
|                       | might map from        |                       |
|                       | last-name, first-name |                       |
|                       | pairs to telephone    |                       |
|                       | numbers. Assuming     |                       |
|                       | that we have defined  |                       |
|                       | [last]{.c004},        |                       |
|                       | [first]{.c004} and    |                       |
|                       | [number]{.c004}, we   |                       |
|                       | could write:          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1090} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1091} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | directory[            |                       |
|                       | last, first] = number |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The expression in     |                       |
|                       | brackets is a tuple.  |                       |
|                       | We could use tuple    |                       |
|                       | assignment to         |                       |
|                       | traverse this         |                       |
|                       | dictionary.           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1092} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | for last              |                       |
|                       | , first in directory: |                       |
|                       |                       |                       |
|                       |  print(first, last, d |                       |
|                       | irectory[last,first]) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This loop traverses   |                       |
|                       | the keys in           |                       |
|                       | [directory]{.c004},   |                       |
|                       | which are tuples. It  |                       |
|                       | assigns the elements  |                       |
|                       | of each tuple to      |                       |
|                       | [last]{.c004} and     |                       |
|                       | [first]{.c004}, then  |                       |
|                       | prints the name and   |                       |
|                       | corresponding         |                       |
|                       | telephone number.     |                       |
|                       |                       |                       |
|                       | There are two ways to |                       |
|                       | represent tuples in a |                       |
|                       | state diagram. The    |                       |
|                       | more detailed version |                       |
|                       | shows the indices and |                       |
|                       | elements just as they |                       |
|                       | appear in a list. For |                       |
|                       | example, the tuple    |                       |
|                       | `('Cleese', 'John')`  |                       |
|                       | would appear as in    |                       |
|                       | Figure                |                       |
|                       |  [12.1](#fig.tuple1). |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1093} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1094} |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2018.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  12.1: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.tuple1}     |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | But in a larger       |                       |
|                       | diagram you might     |                       |
|                       | want to leave out the |                       |
|                       | details. For example, |                       |
|                       | a diagram of the      |                       |
|                       | telephone directory   |                       |
|                       | might appear as in    |                       |
|                       | Figur                 |                       |
|                       | e [12.2](#fig.dict2). |                       |
|                       |                       |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | > ![]                 |                       |
|                       | (thinkpython2019.png) |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > ::: caption         |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | >   Figure            |                       |
|                       |  12.2: State diagram. |                       |
|                       | >   --------          |                       |
|                       | --------------------- |                       |
|                       | > :::                 |                       |
|                       | >                     |                       |
|                       | > []{#fig.dict2}      |                       |
|                       | >                     |                       |
|                       | > ::: center          |                       |
|                       | >                     |                       |
|                       | > ------------------- |                       |
|                       | > :::                 |                       |
|                       |                       |                       |
|                       | Here the tuples are   |                       |
|                       | shown using Python    |                       |
|                       | syntax as a graphical |                       |
|                       | shorthand. The        |                       |
|                       | telephone number in   |                       |
|                       | the diagram is the    |                       |
|                       | complaints line for   |                       |
|                       | the BBC, so please    |                       |
|                       | don't call it.        |                       |
|                       |                       |                       |
|                       | ## 12.7               |                       |
|                       |  Sequences of sequenc |                       |
|                       | es {#sec147 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1095} |                       |
|                       |                       |                       |
|                       | I have focused on     |                       |
|                       | lists of tuples, but  |                       |
|                       | almost all of the     |                       |
|                       | examples in this      |                       |
|                       | chapter also work     |                       |
|                       | with lists of lists,  |                       |
|                       | tuples of tuples, and |                       |
|                       | tuples of lists. To   |                       |
|                       | avoid enumerating the |                       |
|                       | possible              |                       |
|                       | combinations, it is   |                       |
|                       | sometimes easier to   |                       |
|                       | talk about sequences  |                       |
|                       | of sequences.         |                       |
|                       |                       |                       |
|                       | In many contexts, the |                       |
|                       | different kinds of    |                       |
|                       | sequences (strings,   |                       |
|                       | lists and tuples) can |                       |
|                       | be used               |                       |
|                       | interchangeably. So   |                       |
|                       | how should you choose |                       |
|                       | one over the others?  |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1096} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1097} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1098} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1099} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1100} |                       |
|                       |                       |                       |
|                       | To start with the     |                       |
|                       | obvious, strings are  |                       |
|                       | more limited than     |                       |
|                       | other sequences       |                       |
|                       | because the elements  |                       |
|                       | have to be            |                       |
|                       | characters. They are  |                       |
|                       | also immutable. If    |                       |
|                       | you need the ability  |                       |
|                       | to change the         |                       |
|                       | characters in a       |                       |
|                       | string (as opposed to |                       |
|                       | creating a new        |                       |
|                       | string), you might    |                       |
|                       | want to use a list of |                       |
|                       | characters instead.   |                       |
|                       |                       |                       |
|                       | Lists are more common |                       |
|                       | than tuples, mostly   |                       |
|                       | because they are      |                       |
|                       | mutable. But there    |                       |
|                       | are a few cases where |                       |
|                       | you might prefer      |                       |
|                       | tuples:               |                       |
|                       |                       |                       |
|                       | 1.  In some contexts, |                       |
|                       |     like a            |                       |
|                       |     [return]{.c004}   |                       |
|                       |     statement, it is  |                       |
|                       |     syntactically     |                       |
|                       |     simpler to create |                       |
|                       |     a tuple than a    |                       |
|                       |     list.             |                       |
|                       | 2.  If you want to    |                       |
|                       |     use a sequence as |                       |
|                       |     a dictionary key, |                       |
|                       |     you have to use   |                       |
|                       |     an immutable type |                       |
|                       |     like a tuple or   |                       |
|                       |     string.           |                       |
|                       | 3.  If you are        |                       |
|                       |     passing a         |                       |
|                       |     sequence as an    |                       |
|                       |     argument to a     |                       |
|                       |     function, using   |                       |
|                       |     tuples reduces    |                       |
|                       |     the potential for |                       |
|                       |     unexpected        |                       |
|                       |     behavior due to   |                       |
|                       |     aliasing.         |                       |
|                       |                       |                       |
|                       | Because tuples are    |                       |
|                       | immutable, they don't |                       |
|                       | provide methods like  |                       |
|                       | [sort]{.c004} and     |                       |
|                       | [reverse]{.c004},     |                       |
|                       | which modify existing |                       |
|                       | lists. But Python     |                       |
|                       | provides the built-in |                       |
|                       | function              |                       |
|                       | [sorted]{.c004},      |                       |
|                       | which takes any       |                       |
|                       | sequence and returns  |                       |
|                       | a new list with the   |                       |
|                       | same elements in      |                       |
|                       | sorted order, and     |                       |
|                       | [reversed]{.c004},    |                       |
|                       | which takes a         |                       |
|                       | sequence and returns  |                       |
|                       | an iterator that      |                       |
|                       | traverses the list in |                       |
|                       | reverse order.        |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1101} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1102} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1103} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1104} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1105} |                       |
|                       |                       |                       |
|                       | ## 12.8  Debuggi      |                       |
|                       | ng {#sec148 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1106} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1107} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1108} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1109} |                       |
|                       |                       |                       |
|                       | Lists, dictionaries   |                       |
|                       | and tuples are        |                       |
|                       | examples of [data     |                       |
|                       | structures]{.c010};   |                       |
|                       | in this chapter we    |                       |
|                       | are starting to see   |                       |
|                       | compound data         |                       |
|                       | structures, like      |                       |
|                       | lists of tuples, or   |                       |
|                       | dictionaries that     |                       |
|                       | contain tuples as     |                       |
|                       | keys and lists as     |                       |
|                       | values. Compound data |                       |
|                       | structures are        |                       |
|                       | useful, but they are  |                       |
|                       | prone to what I call  |                       |
|                       | [shape                |                       |
|                       | errors]{.c010}; that  |                       |
|                       | is, errors caused     |                       |
|                       | when a data structure |                       |
|                       | has the wrong type,   |                       |
|                       | size, or structure.   |                       |
|                       | For example, if you   |                       |
|                       | are expecting a list  |                       |
|                       | with one integer and  |                       |
|                       | I give you a plain    |                       |
|                       | old integer (not in a |                       |
|                       | list), it won't work. |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1110} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1111} |                       |
|                       |                       |                       |
|                       | To help debug these   |                       |
|                       | kinds of errors, I    |                       |
|                       | have written a module |                       |
|                       | called                |                       |
|                       | [structshape]{.c004}  |                       |
|                       | that provides a       |                       |
|                       | function, also called |                       |
|                       | [structshape]{.c004}, |                       |
|                       | that takes any kind   |                       |
|                       | of data structure as  |                       |
|                       | an argument and       |                       |
|                       | returns a string that |                       |
|                       | summarizes its shape. |                       |
|                       | You can download it   |                       |
|                       | from                  |                       |
|                       | [[https://think       |                       |
|                       | python.com/code/struc |                       |
|                       | tshape.py]{.c004}](ht |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/structshape.py) |                       |
|                       |                       |                       |
|                       | Here's the result for |                       |
|                       | a simple list:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> from structsha    |                       |
|                       | pe import structshape |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> structshape(t)    |                       |
|                       | 'list of 3 int'       |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A fancier program     |                       |
|                       | might write "list of  |                       |
|                       | 3 int*s*", but it was |                       |
|                       | easier not to deal    |                       |
|                       | with plurals. Here's  |                       |
|                       | a list of lists:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t2 =              |                       |
|                       | [[1,2], [3,4], [5,6]] |                       |
|                       | >>> structshape(t2)   |                       |
|                       | 'lis                  |                       |
|                       | t of 3 list of 2 int' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If the elements of    |                       |
|                       | the list are not the  |                       |
|                       | same type,            |                       |
|                       | [structshape]{.c004}  |                       |
|                       | groups them, in       |                       |
|                       | order, by type:       |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>>                   |                       |
|                       | t3 = [1, 2, 3, 4.0, ' |                       |
|                       | 5', '6', [7], [8], 9] |                       |
|                       | >>> structshape(t3)   |                       |
|                       | 'list of              |                       |
|                       | (3 int, float, 2 str, |                       |
|                       |  2 list of int, int)' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here's a list of      |                       |
|                       | tuples:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> s = 'abc'         |                       |
|                       | >>>                   |                       |
|                       |  lt = list(zip(t, s)) |                       |
|                       | >>> structshape(lt)   |                       |
|                       | 'list of 3            |                       |
|                       |  tuple of (int, str)' |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And here's a          |                       |
|                       | dictionary with 3     |                       |
|                       | items that map        |                       |
|                       | integers to strings.  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> d = dict(lt)      |                       |
|                       | >>> structshape(d)    |                       |
|                       | 'dict of 3 int->str'  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | If you are having     |                       |
|                       | trouble keeping track |                       |
|                       | of your data          |                       |
|                       | structures,           |                       |
|                       | [structshape]{.c004}  |                       |
|                       | can help.             |                       |
|                       |                       |                       |
|                       | ## 12.9  Glossa       |                       |
|                       | ry {#sec149 .section} |                       |
|                       |                       |                       |
|                       | [tuple:]{.c010}       |                       |
|                       | :   An immutable      |                       |
|                       |     sequence of       |                       |
|                       |     elements.         |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1112} |                       |
|                       |                       |                       |
|                       | [tupl                 |                       |
|                       | e assignment:]{.c010} |                       |
|                       | :   An assignment     |                       |
|                       |     with a sequence   |                       |
|                       |     on the right side |                       |
|                       |     and a tuple of    |                       |
|                       |     variables on the  |                       |
|                       |     left. The right   |                       |
|                       |     side is evaluated |                       |
|                       |     and then its      |                       |
|                       |     elements are      |                       |
|                       |     assigned to the   |                       |
|                       |     variables on the  |                       |
|                       |     left.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1113} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1114} |                       |
|                       |                       |                       |
|                       | [gather:]{.c010}      |                       |
|                       | :   An operation that |                       |
|                       |     collects multiple |                       |
|                       |     arguments into a  |                       |
|                       |     tuple.            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1115} |                       |
|                       |                       |                       |
|                       | [scatter:]{.c010}     |                       |
|                       | :   An operation that |                       |
|                       |     makes a sequence  |                       |
|                       |     behave like       |                       |
|                       |     multiple          |                       |
|                       |     arguments.        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1116} |                       |
|                       |                       |                       |
|                       | [zip object:]{.c010}  |                       |
|                       | :   The result of     |                       |
|                       |     calling a         |                       |
|                       |     built-in function |                       |
|                       |     [zip]{.c004}; an  |                       |
|                       |     object that       |                       |
|                       |     iterates through  |                       |
|                       |     a sequence of     |                       |
|                       |     tuples.           |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1117} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1118} |                       |
|                       |                       |                       |
|                       | [iterator:]{.c010}    |                       |
|                       | :   An object that    |                       |
|                       |     can iterate       |                       |
|                       |     through a         |                       |
|                       |     sequence, but     |                       |
|                       |     which does not    |                       |
|                       |     provide list      |                       |
|                       |     operators and     |                       |
|                       |     methods.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1119} |                       |
|                       |                       |                       |
|                       | [da                   |                       |
|                       | ta structure:]{.c010} |                       |
|                       | :   A collection of   |                       |
|                       |     related values,   |                       |
|                       |     often organized   |                       |
|                       |     in lists,         |                       |
|                       |     dictionaries,     |                       |
|                       |     tuples, etc.      |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1120} |                       |
|                       |                       |                       |
|                       | [shape error:]{.c010} |                       |
|                       | :   An error caused   |                       |
|                       |     because a value   |                       |
|                       |     has the wrong     |                       |
|                       |     shape; that is,   |                       |
|                       |     the wrong type or |                       |
|                       |     size.             |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1121} |                       |
|                       |                       |                       |
|                       | ## 12.10  Exercis     |                       |
|                       | es {#sec150 .section} |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | called                |                       |
|                       | `most_frequent` that  |                       |
|                       | takes a string and    |                       |
|                       | prints the letters in |                       |
|                       | decreasing order of   |                       |
|                       | frequency. Find text  |                       |
|                       | samples from several  |                       |
|                       | different languages   |                       |
|                       | and see how letter    |                       |
|                       | frequency varies      |                       |
|                       | between languages.    |                       |
|                       | Compare your results  |                       |
|                       | with the tables at*   |                       |
|                       | [[*htt                |                       |
|                       | p://en.wikipedia.org/ |                       |
|                       | wiki/Letter_frequenci |                       |
|                       | es*]{.c004}](http://e |                       |
|                       | n.wikipedia.org/wiki/ |                       |
|                       | Letter_frequencies)*. |                       |
|                       | Solution:*            |                       |
|                       | [[*                   |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/most_frequent |                       |
|                       | .py*]{.c004}](https:/ |                       |
|                       | /thinkpython.com/code |                       |
|                       | /most_frequent.py)*.* |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1122} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1123} |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 2]{.c010}   |                       |
|                       | []{#anagrams}         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1124} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1125} |                       |
|                       |                       |                       |
|                       | *More anagrams!*      |                       |
|                       |                       |                       |
|                       | 1.  *Write a program  |                       |
|                       |     that reads a word |                       |
|                       |     list from a file  |                       |
|                       |     (see              |                       |
|                       |     Section           |                       |
|                       |  *[*9.1*](thinkpython |                       |
|                       | 2010.html#wordlist)*) |                       |
|                       |     and prints all    |                       |
|                       |     the sets of words |                       |
|                       |     that are          |                       |
|                       |     anagrams.*        |                       |
|                       |                       |                       |
|                       |     *Here is an       |                       |
|                       |     example of what   |                       |
|                       |     the output might  |                       |
|                       |     look like:*       |                       |
|                       |                       |                       |
|                       |     ``` verbatim      |                       |
|                       |                       |                       |
|                       |    ['deltas', 'desalt |                       |
|                       | ', 'lasted', 'salted' |                       |
|                       | , 'slated', 'staled'] |                       |
|                       |     ['ret             |                       |
|                       | ainers', 'ternaries'] |                       |
|                       |     ['gener           |                       |
|                       | ating', 'greatening'] |                       |
|                       |     ['resmelts', 's   |                       |
|                       | melters', 'termless'] |                       |
|                       |     ```               |                       |
|                       |                       |                       |
|                       |     *Hint: you might  |                       |
|                       |     want to build a   |                       |
|                       |     dictionary that   |                       |
|                       |     maps from a       |                       |
|                       |     collection of     |                       |
|                       |     letters to a list |                       |
|                       |     of words that can |                       |
|                       |     be spelled with   |                       |
|                       |     those letters.    |                       |
|                       |     The question is,  |                       |
|                       |     how can you       |                       |
|                       |     represent the     |                       |
|                       |     collection of     |                       |
|                       |     letters in a way  |                       |
|                       |     that can be used  |                       |
|                       |     as a key?*        |                       |
|                       |                       |                       |
|                       | 2.  *Modify the       |                       |
|                       |     previous program  |                       |
|                       |     so that it prints |                       |
|                       |     the longest list  |                       |
|                       |     of anagrams       |                       |
|                       |     first, followed   |                       |
|                       |     by the second     |                       |
|                       |     longest, and so   |                       |
|                       |     on.*              |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1126} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1127} |                       |
|                       |                       |                       |
|                       | 3.  *In Scrabble a    |                       |
|                       |     "bingo" is when   |                       |
|                       |     you play all      |                       |
|                       |     seven tiles in    |                       |
|                       |     your rack, along  |                       |
|                       |     with a letter on  |                       |
|                       |     the board, to     |                       |
|                       |     form an           |                       |
|                       |     eight-letter      |                       |
|                       |     word. What        |                       |
|                       |     collection of 8   |                       |
|                       |     letters forms the |                       |
|                       |     most possible     |                       |
|                       |     bingos?*          |                       |
|                       |                       |                       |
|                       |     *Solution:*       |                       |
|                       |     [                 |                       |
|                       | [*https://thinkpython |                       |
|                       | .com/code/anagram_set |                       |
|                       | s.py*]{.c004}](https: |                       |
|                       | //thinkpython.com/cod |                       |
|                       | e/anagram_sets.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 3]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1128} |                       |
|                       |                       |                       |
|                       | *Two words form a     |                       |
|                       | "metathesis pair" if  |                       |
|                       | you can transform one |                       |
|                       | into the other by     |                       |
|                       | swapping two letters; |                       |
|                       | for example,          |                       |
|                       | "converse" and        |                       |
|                       | "conserve". Write a   |                       |
|                       | program that finds    |                       |
|                       | all of the metathesis |                       |
|                       | pairs in the          |                       |
|                       | dictionary. Hint:     |                       |
|                       | don't test all pairs  |                       |
|                       | of words, and don't   |                       |
|                       | test all possible     |                       |
|                       | swaps. Solution:*     |                       |
|                       | [*[https://thinkp     |                       |
|                       | ython.com/code/metath |                       |
|                       | esis.py]{.c004}*](htt |                       |
|                       | ps://thinkpython.com/ |                       |
|                       | code/metathesis.py)*. |                       |
|                       | Credit: This exercise |                       |
|                       | is inspired by an     |                       |
|                       | example at*           |                       |
|                       | [*[http://puzz        |                       |
|                       | lers.org]{.c004}*](ht |                       |
|                       | tp://puzzlers.org)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 4]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1129} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1130} |                       |
|                       |                       |                       |
|                       | *Here's another Car   |                       |
|                       | Talk Puzzler          |                       |
|                       | (*[*[http://www       |                       |
|                       | .cartalk.com/content/ |                       |
|                       | puzzlers]{.c004}*](ht |                       |
|                       | tp://www.cartalk.com/ |                       |
|                       | content/puzzlers)*):* |                       |
|                       |                       |                       |
|                       | > *What is the        |                       |
|                       | > longest English     |                       |
|                       | > word, that remains  |                       |
|                       | > a valid English     |                       |
|                       | > word, as you remove |                       |
|                       | > its letters one at  |                       |
|                       | > a time?*            |                       |
|                       | >                     |                       |
|                       | > *Now, letters can   |                       |
|                       | > be removed from     |                       |
|                       | > either end, or the  |                       |
|                       | > middle, but you     |                       |
|                       | > can't rearrange any |                       |
|                       | > of the letters.     |                       |
|                       | > Every time you drop |                       |
|                       | > a letter, you wind  |                       |
|                       | > up with another     |                       |
|                       | > English word. If    |                       |
|                       | > you do that, you're |                       |
|                       | > eventually going to |                       |
|                       | > wind up with one    |                       |
|                       | > letter and that too |                       |
|                       | > is going to be an   |                       |
|                       | > English word---one  |                       |
|                       | > that's found in the |                       |
|                       | > dictionary. I want  |                       |
|                       | > to know what's the  |                       |
|                       | > longest word and    |                       |
|                       | > how many letters    |                       |
|                       | > does it have?*      |                       |
|                       | >                     |                       |
|                       | > *I'm going to give  |                       |
|                       | > you a little modest |                       |
|                       | > example: Sprite.    |                       |
|                       | > Ok? You start off   |                       |
|                       | > with sprite, you    |                       |
|                       | > take a letter off,  |                       |
|                       | > one from the        |                       |
|                       | > interior of the     |                       |
|                       | > word, take the r    |                       |
|                       | > away, and we're     |                       |
|                       | > left with the word  |                       |
|                       | > spite, then we take |                       |
|                       | > the e off the end,  |                       |
|                       | > we're left with     |                       |
|                       | > spit, we take the s |                       |
|                       | > off, we're left     |                       |
|                       | > with pit, it, and   |                       |
|                       | > I.*                 |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1131} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1132} |                       |
|                       |                       |                       |
|                       | *Write a program to   |                       |
|                       | find all words that   |                       |
|                       | can be reduced in     |                       |
|                       | this way, and then    |                       |
|                       | find the longest      |                       |
|                       | one.*                 |                       |
|                       |                       |                       |
|                       | *This exercise is a   |                       |
|                       | little more           |                       |
|                       | challenging than      |                       |
|                       | most, so here are     |                       |
|                       | some suggestions:*    |                       |
|                       |                       |                       |
|                       | 1.  *You might want   |                       |
|                       |     to write a        |                       |
|                       |     function that     |                       |
|                       |     takes a word and  |                       |
|                       |     computes a list   |                       |
|                       |     of all the words  |                       |
|                       |     that can be       |                       |
|                       |     formed by         |                       |
|                       |     removing one      |                       |
|                       |     letter. These are |                       |
|                       |     the "children" of |                       |
|                       |     the word.*        |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1133} |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1134} |                       |
|                       | 2.  *Recursively, a   |                       |
|                       |     word is reducible |                       |
|                       |     if any of its     |                       |
|                       |     children are      |                       |
|                       |     reducible. As a   |                       |
|                       |     base case, you    |                       |
|                       |     can consider the  |                       |
|                       |     empty string      |                       |
|                       |     reducible.*       |                       |
|                       | 3.  *The wordlist I   |                       |
|                       |     provided,         |                       |
|                       |                       |                       |
|                       |   [words.txt]{.c004}, |                       |
|                       |     doesn't contain   |                       |
|                       |     single letter     |                       |
|                       |     words. So you     |                       |
|                       |     might want to add |                       |
|                       |     "I", "a", and the |                       |
|                       |     empty string.*    |                       |
|                       | 4.  *To improve the   |                       |
|                       |     performance of    |                       |
|                       |     your program, you |                       |
|                       |     might want to     |                       |
|                       |     memoize the words |                       |
|                       |     that are known to |                       |
|                       |     be reducible.*    |                       |
|                       |                       |                       |
|                       | *Solution:*           |                       |
|                       | [*[https://think      |                       |
|                       | python.com/code/reduc |                       |
|                       | ible.py]{.c004}*](htt |                       |
|                       | ps://thinkpython.com/ |                       |
|                       | code/reducible.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | [Buy this book at     |                       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) |                       |
+-----------------------+-----------------------+-----------------------+

------------------------------------------------------------------------

[![Previous](back.png)](thinkpython2012.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2014.html)
---
generator: hevea 2.32
title: "Case study: data structure selection"
---

[![Previous](back.png)](thinkpython2013.html)
[![Up](up.png)](index.html) [![Next](next.png)](thinkpython2015.html)

------------------------------------------------------------------------

+-----------------------+-----------------------+-----------------------+
|                       | [Buy this book at     | #### Contribute       |
|                       | Amazon.com](ht        |                       |
|                       | tp://amzn.to/1VUYQUU) | If you would like to  |
|                       |                       | make a contribution   |
|                       | # Chap                | to support my books,  |
|                       | ter 13  Case study: d | you can use the       |
|                       | ata structure selecti | button below and pay  |
|                       | on {#sec151 .chapter} | with PayPal. Thank    |
|                       |                       | you!                  |
|                       | At this point you     |                       |
|                       | have learned about    |   -----------         |
|                       | Python's core data    | --------------------- |
|                       | structures, and you   | --------------------- |
|                       | have seen some of the | --------------------- |
|                       | algorithms that use   | --------------------- |
|                       | them. If you would    |   Pay what you want:  |
|                       | like to know more     |   Small \$1           |
|                       | about algorithms,     | .00 USD Medium \$5.00 |
|                       | this might be a good  |  USD Large \$10.00 US |
|                       | time to read          | D X-Large \$20.00 USD |
|                       | Cha                   |  XX-Large \$50.00 USD |
|                       | pter [B](thinkpython2 |   -----------         |
|                       | 022.html#algorithms). | --------------------- |
|                       | But you don't have to | --------------------- |
|                       | read it before you go | --------------------- |
|                       | on; you can read it   | --------------------- |
|                       | whenever you are      |                       |
|                       | interested.           | ![](                  |
|                       |                       | https://www.paypalobj |
|                       | This chapter presents | ects.com/en_US/i/scr/ |
|                       | a case study with     | pixel.gif){border="0" |
|                       | exercises that let    | width="1" height="1"} |
|                       | you think about       |                       |
|                       | choosing data         | ####                  |
|                       | structures and        | Are you using one of  |
|                       | practice using them.  | our books in a class? |
|                       |                       |                       |
|                       | ## 13.1               | We\'d like to know    |
|                       | Word frequency analys | about it. Please      |
|                       | is {#sec152 .section} | consider filling out  |
|                       |                       | [this short           |
|                       | []{#analysis}         | survey](http://s      |
|                       |                       | preadsheets.google.co |
|                       | As usual, you should  | m/viewform?formkey=dC |
|                       | at least attempt the  | 0tNUZkMjBEdXVoRGljNm9 |
|                       | exercises before you  | FRmlTMHc6MA){onclick= |
|                       | read my solutions.    | "javascript: pageTrac |
|                       |                       | ker._trackPageview('/ |
|                       | ::: theorem           | outbound/survey');"}. |
|                       | [Exercise 1]{.c010}   |                       |
|                       |                       | \                     |
|                       | *Write a program that |                       |
|                       | reads a file, breaks  | [Think                |
|                       | each line into words, | DSP](http             |
|                       | strips whitespace and | ://www.amazon.com/gp/ |
|                       | punctuation from the  | product/1491938455/re |
|                       | words, and converts   | f=as_li_tl?ie=UTF8&ca |
|                       | them to lowercase.*   | mp=1789&creative=9325 |
|                       | [                     | &creativeASIN=1491938 |
|                       | ]{#hevea_default1135} | 455&linkCode=as2&tag= |
|                       | [                     | greenteapre01-20&link |
|                       | ]{#hevea_default1136} | Id=2JJH4SWCAVVYSQHO){ |
|                       |                       | rel="nofollow"}![](ht |
|                       | *Hint: The            | tp://ir-na.amazon-ads |
|                       | [string]{.c004}       | ystem.com/e/ir?t=gree |
|                       | module provides a     | nteapre01-20&l=as2&o= |
|                       | string named          | 1&a=1491938455){.c003 |
|                       | [whitespace]{.c004},  | width="1" height="1"  |
|                       | which contains space, | border="0"}           |
|                       | tab, newline, etc.,   |                       |
|                       | and                   | [                     |
|                       | [punctuation]{.c004}  | ![](http://ws-na.amaz |
|                       | which contains the    | on-adsystem.com/widge |
|                       | punctuation           | ts/q?_encoding=UTF8&A |
|                       | characters. Let's see | SIN=1491938455&Format |
|                       | if we can make Python | =_SL160_&ID=AsinImage |
|                       | swear:*               | &MarketPlace=US&Servi |
|                       |                       | ceVersion=20070822&WS |
|                       | ``` verbatim          | =1&tag=greenteapre01- |
|                       | >>> import string     | 20){border="0"}](http |
|                       | >                     | ://www.amazon.com/gp/ |
|                       | >> string.punctuation | product/1491938455/re |
|                       | '!"#$%&\'()*+,-       | f=as_li_tl?ie=UTF8&ca |
|                       | ./:;<=>?@[\\]^_`{|}~' | mp=1789&creative=9325 |
|                       | ```                   | &creativeASIN=1491938 |
|                       |                       | 455&linkCode=as2&tag= |
|                       | *Also, you might      | greenteapre01-20&link |
|                       | consider using the    | Id=CTV7PDT7E5EGGJUM){ |
|                       | string methods        | rel="nofollow"}![](ht |
|                       | [strip]{.c004},       | tp://ir-na.amazon-ads |
|                       | [replace]{.c004} and  | ystem.com/e/ir?t=gree |
|                       | [translate]{.c004}.*  | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491938455){.c003 |
|                       | ]{#hevea_default1137} | width="1" height="1"  |
|                       | [                     | border="0"}           |
|                       | ]{#hevea_default1138} |                       |
|                       | [                     | [Think                |
|                       | ]{#hevea_default1139} | Java](http            |
|                       | [                     | ://www.amazon.com/gp/ |
|                       | ]{#hevea_default1140} | product/1491929561/re |
|                       | [                     | f=as_li_tl?ie=UTF8&ca |
|                       | ]{#hevea_default1141} | mp=1789&creative=9325 |
|                       | [                     | &creativeASIN=1491929 |
|                       | ]{#hevea_default1142} | 561&linkCode=as2&tag= |
|                       | :::                   | greenteapre01-20&link |
|                       |                       | Id=ZY6MAYM33ZTNSCNZ){ |
|                       | ::: theorem           | rel="nofollow"}![](ht |
|                       | [Exercise 2]{.c010}   | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1143} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | *Go to Project        | width="1" height="1"  |
|                       | Gutenberg             | border="0"}           |
|                       | (*[[*http://guten     |                       |
|                       | berg.org*]{.c004}](ht | [                     |
|                       | tp://gutenberg.org)*) | ![](http://ws-na.amaz |
|                       | and download your     | on-adsystem.com/widge |
|                       | favorite              | ts/q?_encoding=UTF8&A |
|                       | out-of-copyright book | SIN=1491929561&Format |
|                       | in plain text         | =_SL160_&ID=AsinImage |
|                       | format.*              | &MarketPlace=US&Servi |
|                       | [                     | ceVersion=20070822&WS |
|                       | ]{#hevea_default1144} | =1&tag=greenteapre01- |
|                       | [                     | 20){border="0"}](http |
|                       | ]{#hevea_default1145} | ://www.amazon.com/gp/ |
|                       |                       | product/1491929561/re |
|                       | *Modify your program  | f=as_li_tl?ie=UTF8&ca |
|                       | from the previous     | mp=1789&creative=9325 |
|                       | exercise to read the  | &creativeASIN=1491929 |
|                       | book you downloaded,  | 561&linkCode=as2&tag= |
|                       | skip over the header  | greenteapre01-20&link |
|                       | information at the    | Id=PT77ANWARUNNU3UK){ |
|                       | beginning of the      | rel="nofollow"}![](ht |
|                       | file, and process the | tp://ir-na.amazon-ads |
|                       | rest of the words as  | ystem.com/e/ir?t=gree |
|                       | before.*              | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491929561){.c003 |
|                       | *Then modify the      | width="1" height="1"  |
|                       | program to count the  | border="0"}           |
|                       | total number of words |                       |
|                       | in the book, and the  | [Think                |
|                       | number of times each  | Bay                   |
|                       | word is used.*        | es](http://www.amazon |
|                       | [                     | .com/gp/product/14493 |
|                       | ]{#hevea_default1146} | 70780/ref=as_li_qf_sp |
|                       | [                     | _asin_tl?ie=UTF8&camp |
|                       | ]{#hevea_default1147} | =1789&creative=9325&c |
|                       |                       | reativeASIN=144937078 |
|                       | *Print the number of  | 0&linkCode=as2&tag=gr |
|                       | different words used  | eenteapre01-20)![](ht |
|                       | in the book. Compare  | tp://ir-na.amazon-ads |
|                       | different books by    | ystem.com/e/ir?t=gree |
|                       | different authors,    | nteapre01-20&l=as2&o= |
|                       | written in different  | 1&a=1449370780){.c003 |
|                       | eras. Which author    | width="1" height="1"  |
|                       | uses the most         | border="0"}           |
|                       | extensive             |                       |
|                       | vocabulary?*          | [![](http://ws        |
|                       | :::                   | -na.amazon-adsystem.c |
|                       |                       | om/widgets/q?_encodin |
|                       | ::: theorem           | g=UTF8&ASIN=144937078 |
|                       | [Exercise 3]{.c010}   | 0&Format=_SL160_&ID=A |
|                       |                       | sinImage&MarketPlace= |
|                       | *Modify the program   | US&ServiceVersion=200 |
|                       | from the previous     | 70822&WS=1&tag=greent |
|                       | exercise to print the | eapre01-20){border="0 |
|                       | 20 most frequently    | "}](http://www.amazon |
|                       | used words in the     | .com/gp/product/14493 |
|                       | book.*                | 70780/ref=as_li_qf_sp |
|                       | :::                   | _asin_il?ie=UTF8&camp |
|                       |                       | =1789&creative=9325&c |
|                       | ::: theorem           | reativeASIN=144937078 |
|                       | [Exercise 4]{.c010}   | 0&linkCode=as2&tag=gr |
|                       |                       | eenteapre01-20)![](ht |
|                       | *Modify the previous  | tp://ir-na.amazon-ads |
|                       | program to read a     | ystem.com/e/ir?t=gree |
|                       | word list (see        | nteapre01-20&l=as2&o= |
|                       | Section               | 1&a=1449370780){.c003 |
|                       |  *[*9.1*](thinkpython | width="1" height="1"  |
|                       | 2010.html#wordlist)*) | border="0"}           |
|                       | and then print all    |                       |
|                       | the words in the book | [Think Python         |
|                       | that are not in the   | 2e](http              |
|                       | word list. How many   | ://www.amazon.com/gp/ |
|                       | of them are typos?    | product/1491939362/re |
|                       | How many of them are  | f=as_li_tl?ie=UTF8&ca |
|                       | common words that*    | mp=1789&creative=9325 |
|                       | should *be in the     | &creativeASIN=1491939 |
|                       | word list, and how    | 362&linkCode=as2&tag= |
|                       | many of them are      | greenteapre01-20&link |
|                       | really obscure?*      | Id=FJKSQ3IHEMY2F2VA){ |
|                       | :::                   | rel="nofollow"}![](ht |
|                       |                       | tp://ir-na.amazon-ads |
|                       | ## 13.2  Random numbe | ystem.com/e/ir?t=gree |
|                       | rs {#sec153 .section} | nteapre01-20&l=as2&o= |
|                       |                       | 1&a=1491939362){.c003 |
|                       | [                     | width="1" height="1"  |
|                       | ]{#hevea_default1148} | border="0"}           |
|                       | [                     |                       |
|                       | ]{#hevea_default1149} | [                     |
|                       | [                     | ![](http://ws-na.amaz |
|                       | ]{#hevea_default1150} | on-adsystem.com/widge |
|                       | [                     | ts/q?_encoding=UTF8&A |
|                       | ]{#hevea_default1151} | SIN=1491939362&Format |
|                       |                       | =_SL160_&ID=AsinImage |
|                       | Given the same        | &MarketPlace=US&Servi |
|                       | inputs, most computer | ceVersion=20070822&WS |
|                       | programs generate the | =1&tag=greenteapre01- |
|                       | same outputs every    | 20){border="0"}](http |
|                       | time, so they are     | ://www.amazon.com/gp/ |
|                       | said to be            | product/1491939362/re |
|                       | [d                    | f=as_li_tl?ie=UTF8&ca |
|                       | eterministic]{.c010}. | mp=1789&creative=9325 |
|                       | Determinism is        | &creativeASIN=1491939 |
|                       | usually a good thing, | 362&linkCode=as2&tag= |
|                       | since we expect the   | greenteapre01-20&link |
|                       | same calculation to   | Id=ZZ454DLQ3IXDHNHX){ |
|                       | yield the same        | rel="nofollow"}![](ht |
|                       | result. For some      | tp://ir-na.amazon-ads |
|                       | applications, though, | ystem.com/e/ir?t=gree |
|                       | we want the computer  | nteapre01-20&l=as2&o= |
|                       | to be unpredictable.  | 1&a=1491939362){.c003 |
|                       | Games are an obvious  | width="1" height="1"  |
|                       | example, but there    | border="0"}           |
|                       | are more.             |                       |
|                       |                       | [Think Stats          |
|                       | Making a program      | 2e](http://ww         |
|                       | truly                 | w.amazon.com/gp/produ |
|                       | nondeterministic      | ct/1491907339/ref=as_ |
|                       | turns out to be       | li_tl?ie=UTF8&camp=17 |
|                       | difficult, but there  | 89&creative=9325&crea |
|                       | are ways to make it   | tiveASIN=1491907339&l |
|                       | at least seem         | inkCode=as2&tag=green |
|                       | nondeterministic. One | teapre01-20&linkId=O7 |
|                       | of them is to use     | WYM6H6YBYUFNWU)![](ht |
|                       | algorithms that       | tp://ir-na.amazon-ads |
|                       | generate              | ystem.com/e/ir?t=gree |
|                       | [pseudorandom]{.c010} | nteapre01-20&l=as2&o= |
|                       | numbers. Pseudorandom | 1&a=1491907339){.c003 |
|                       | numbers are not truly | width="1" height="1"  |
|                       | random because they   | border="0"}           |
|                       | are generated by a    |                       |
|                       | deterministic         | [![](h                |
|                       | computation, but just | ttp://ws-na.amazon-ad |
|                       | by looking at the     | system.com/widgets/q? |
|                       | numbers it is all but | _encoding=UTF8&ASIN=1 |
|                       | impossible to         | 491907339&Format=_SL1 |
|                       | distinguish them from | 60_&ID=AsinImage&Mark |
|                       | random.               | etPlace=US&ServiceVer |
|                       | [                     | sion=20070822&WS=1&ta |
|                       | ]{#hevea_default1152} | g=greenteapre01-20){b |
|                       | [                     | order="0"}](http://ww |
|                       | ]{#hevea_default1153} | w.amazon.com/gp/produ |
|                       |                       | ct/1491907339/ref=as_ |
|                       | The [random]{.c004}   | li_tl?ie=UTF8&camp=17 |
|                       | module provides       | 89&creative=9325&crea |
|                       | functions that        | tiveASIN=1491907339&l |
|                       | generate pseudorandom | inkCode=as2&tag=green |
|                       | numbers (which I will | teapre01-20&linkId=JV |
|                       | simply call "random"  | SYKQHYSUIEYRHL)![](ht |
|                       | from here on).        | tp://ir-na.amazon-ads |
|                       | [                     | ystem.com/e/ir?t=gree |
|                       | ]{#hevea_default1154} | nteapre01-20&l=as2&o= |
|                       | [                     | 1&a=1491907339){.c003 |
|                       | ]{#hevea_default1155} | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | The function          |                       |
|                       | [random]{.c004}       | [Think                |
|                       | returns a random      | Complexity](http      |
|                       | float between 0.0 and | ://www.amazon.com/gp/ |
|                       | 1.0 (including 0.0    | product/1449314635/re |
|                       | but not 1.0). Each    | f=as_li_tf_tl?ie=UTF8 |
|                       | time you call         | &tag=greenteapre01-20 |
|                       | [random]{.c004}, you  | &linkCode=as2&camp=17 |
|                       | get the next number   | 89&creative=9325&crea |
|                       | in a long series. To  | tiveASIN=1449314635)! |
|                       | see a sample, run     | [](http://www.assoc-a |
|                       | this loop:            | mazon.com/e/ir?t=gree |
|                       |                       | nteapre01-20&l=as2&o= |
|                       | ``` verbatim          | 1&a=1449314635){.c003 |
|                       | import random         | width="1" height="1"  |
|                       |                       | border="0"}           |
|                       | for i in range(10):   |                       |
|                       |                       | [                     |
|                       |   x = random.random() | ![](http://ws-na.amaz |
|                       |     print(x)          | on-adsystem.com/widge |
|                       | ```                   | ts/q?_encoding=UTF8&A |
|                       |                       | SIN=1449314635&Format |
|                       | The function          | =_SL160_&ID=AsinImage |
|                       | [randint]{.c004}      | &MarketPlace=US&Servi |
|                       | takes parameters      | ceVersion=20070822&WS |
|                       | [low]{.c004} and      | =1&tag=greenteapre01- |
|                       | [high]{.c004} and     | 20){border="0"}](http |
|                       | returns an integer    | ://www.amazon.com/gp/ |
|                       | between [low]{.c004}  | product/1449314635/re |
|                       | and [high]{.c004}     | f=as_li_tf_il?ie=UTF8 |
|                       | (including both).     | &camp=1789&creative=9 |
|                       | [                     | 325&creativeASIN=1449 |
|                       | ]{#hevea_default1156} | 314635&linkCode=as2&t |
|                       | [                     | ag=greenteapre01-20)! |
|                       | ]{#hevea_default1157} | [](http://www.assoc-a |
|                       |                       | mazon.com/e/ir?t=gree |
|                       | ``` verbatim          | nteapre01-20&l=as2&o= |
|                       | >>>                   | 1&a=1449314635){.c003 |
|                       | random.randint(5, 10) | width="1" height="1"  |
|                       | 5                     | border="0"}           |
|                       | >>>                   |                       |
|                       | random.randint(5, 10) |                       |
|                       | 9                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | To choose an element  |                       |
|                       | from a sequence at    |                       |
|                       | random, you can use   |                       |
|                       | [choice]{.c004}:      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1158} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1159} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>> t = [1, 2, 3]     |                       |
|                       | >>> random.choice(t)  |                       |
|                       | 2                     |                       |
|                       | >>> random.choice(t)  |                       |
|                       | 3                     |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The [random]{.c004}   |                       |
|                       | module also provides  |                       |
|                       | functions to generate |                       |
|                       | random values from    |                       |
|                       | continuous            |                       |
|                       | distributions         |                       |
|                       | including Gaussian,   |                       |
|                       | exponential, gamma,   |                       |
|                       | and a few more.       |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 5]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1160} |                       |
|                       |                       |                       |
|                       | *Write a function     |                       |
|                       | named                 |                       |
|                       | `choose_from_hist`    |                       |
|                       | that takes a          |                       |
|                       | histogram as defined  |                       |
|                       | in                    |                       |
|                       | Section               |                       |
|                       |  *[*11.2*](thinkpytho |                       |
|                       | n2012.html#histogram) |                       |
|                       | *and returns a random |                       |
|                       | value from the        |                       |
|                       | histogram, chosen     |                       |
|                       | with probability in   |                       |
|                       | proportion to         |                       |
|                       | frequency. For        |                       |
|                       | example, for this     |                       |
|                       | histogram:*           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | >>                    |                       |
|                       | > t = ['a', 'a', 'b'] |                       |
|                       | >>                    |                       |
|                       | > hist = histogram(t) |                       |
|                       | >>> hist              |                       |
|                       | {'a': 2, 'b': 1}      |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | *your function should |                       |
|                       | return `'a'` with     |                       |
|                       | probability* 2/3 *and |                       |
|                       | `'b'` with            |                       |
|                       | probability* 1/3*.*   |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ## 13.3  Word histogr |                       |
|                       | am {#sec154 .section} |                       |
|                       |                       |                       |
|                       | You should attempt    |                       |
|                       | the previous          |                       |
|                       | exercises before you  |                       |
|                       | go on. You can        |                       |
|                       | download my solution  |                       |
|                       | from                  |                       |
|                       | [[https://thinkpytho  |                       |
|                       | n.com/code/analyze_bo |                       |
|                       | ok1.py]{.c004}](https |                       |
|                       | ://thinkpython.com/co |                       |
|                       | de/analyze_book1.py). |                       |
|                       | You will also need    |                       |
|                       | [[ht                  |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/emma.txt]{.c004 |                       |
|                       | }](https://thinkpytho |                       |
|                       | n.com/code/emma.txt). |                       |
|                       |                       |                       |
|                       | Here is a program     |                       |
|                       | that reads a file and |                       |
|                       | builds a histogram of |                       |
|                       | the words in the      |                       |
|                       | file:                 |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1161} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | import string         |                       |
|                       |                       |                       |
|                       | def pr                |                       |
|                       | ocess_file(filename): |                       |
|                       |     hist = dict()     |                       |
|                       |                       |                       |
|                       |   fp = open(filename) |                       |
|                       |     for line in fp:   |                       |
|                       |         pro           |                       |
|                       | cess_line(line, hist) |                       |
|                       |     return hist       |                       |
|                       |                       |                       |
|                       | def proc              |                       |
|                       | ess_line(line, hist): |                       |
|                       |     line = l          |                       |
|                       | ine.replace('-', ' ') |                       |
|                       |                       |                       |
|                       |     for               |                       |
|                       | word in line.split(): |                       |
|                       |                       |                       |
|                       |       word = word.str |                       |
|                       | ip(string.punctuation |                       |
|                       |  + string.whitespace) |                       |
|                       |                       |                       |
|                       |   word = word.lower() |                       |
|                       |         hist[word] =  |                       |
|                       | hist.get(word, 0) + 1 |                       |
|                       |                       |                       |
|                       | hist = pro            |                       |
|                       | cess_file('emma.txt') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This program reads    |                       |
|                       | [emma.txt]{.c004},    |                       |
|                       | which contains the    |                       |
|                       | text of *Emma* by     |                       |
|                       | Jane Austen.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1162} |                       |
|                       |                       |                       |
|                       | `process_file` loops  |                       |
|                       | through the lines of  |                       |
|                       | the file, passing     |                       |
|                       | them one at a time to |                       |
|                       | `process_line`. The   |                       |
|                       | histogram             |                       |
|                       | [hist]{.c004} is      |                       |
|                       | being used as an      |                       |
|                       | accumulator.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1163} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1164} |                       |
|                       |                       |                       |
|                       | `process_line` uses   |                       |
|                       | the string method     |                       |
|                       | [replace]{.c004} to   |                       |
|                       | replace hyphens with  |                       |
|                       | spaces before using   |                       |
|                       | [split]{.c004} to     |                       |
|                       | break the line into a |                       |
|                       | list of strings. It   |                       |
|                       | traverses the list of |                       |
|                       | words and uses        |                       |
|                       | [strip]{.c004} and    |                       |
|                       | [lower]{.c004} to     |                       |
|                       | remove punctuation    |                       |
|                       | and convert to lower  |                       |
|                       | case. (It is a        |                       |
|                       | shorthand to say that |                       |
|                       | strings are           |                       |
|                       | "converted"; remember |                       |
|                       | that strings are      |                       |
|                       | immutable, so methods |                       |
|                       | like [strip]{.c004}   |                       |
|                       | and [lower]{.c004}    |                       |
|                       | return new strings.)  |                       |
|                       |                       |                       |
|                       | Finally,              |                       |
|                       | `process_line`        |                       |
|                       | updates the histogram |                       |
|                       | by creating a new     |                       |
|                       | item or incrementing  |                       |
|                       | an existing one.      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1165} |                       |
|                       |                       |                       |
|                       | To count the total    |                       |
|                       | number of words in    |                       |
|                       | the file, we can add  |                       |
|                       | up the frequencies in |                       |
|                       | the histogram:        |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef total_words(hist): |                       |
|                       |     retu              |                       |
|                       | rn sum(hist.values()) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The number of         |                       |
|                       | different words is    |                       |
|                       | just the number of    |                       |
|                       | items in the          |                       |
|                       | dictionary:           |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def d                 |                       |
|                       | ifferent_words(hist): |                       |
|                       |     return len(hist)  |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here is some code to  |                       |
|                       | print the results:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | print('T              |                       |
|                       | otal number of words: |                       |
|                       | ', total_words(hist)) |                       |
|                       | print('Number of      |                       |
|                       |  different words:', d |                       |
|                       | ifferent_words(hist)) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | And the results:      |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Total nu              |                       |
|                       | mber of words: 161080 |                       |
|                       | Number of             |                       |
|                       | different words: 7214 |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | ##                    |                       |
|                       | 13.4  Most common wor |                       |
|                       | ds {#sec155 .section} |                       |
|                       |                       |                       |
|                       | To find the most      |                       |
|                       | common words, we can  |                       |
|                       | make a list of        |                       |
|                       | tuples, where each    |                       |
|                       | tuple contains a word |                       |
|                       | and its frequency,    |                       |
|                       | and sort it.          |                       |
|                       |                       |                       |
|                       | The following         |                       |
|                       | function takes a      |                       |
|                       | histogram and returns |                       |
|                       | a list of             |                       |
|                       | word-frequency        |                       |
|                       | tuples:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | d                     |                       |
|                       | ef most_common(hist): |                       |
|                       |     t = []            |                       |
|                       |     for key, v        |                       |
|                       | alue in hist.items(): |                       |
|                       |         t             |                       |
|                       | .append((value, key)) |                       |
|                       |                       |                       |
|                       |                       |                       |
|                       |  t.sort(reverse=True) |                       |
|                       |     return t          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | In each tuple, the    |                       |
|                       | frequency appears     |                       |
|                       | first, so the         |                       |
|                       | resulting list is     |                       |
|                       | sorted by frequency.  |                       |
|                       | Here is a loop that   |                       |
|                       | prints the ten most   |                       |
|                       | common words:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | t = most_common(hist) |                       |
|                       | print('The mos        |                       |
|                       | t common words are:') |                       |
|                       | for                   |                       |
|                       | freq, word in t[:10]: |                       |
|                       |     print(            |                       |
|                       | word, freq, sep='\t') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | I use the keyword     |                       |
|                       | argument [sep]{.c004} |                       |
|                       | to tell               |                       |
|                       | [print]{.c004} to use |                       |
|                       | a tab character as a  |                       |
|                       | "separator", rather   |                       |
|                       | than a space, so the  |                       |
|                       | second column is      |                       |
|                       | lined up. Here are    |                       |
|                       | the results from      |                       |
|                       | *Emma*:               |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | The m                 |                       |
|                       | ost common words are: |                       |
|                       | to      5242          |                       |
|                       | the     5205          |                       |
|                       | and     4897          |                       |
|                       | of      4295          |                       |
|                       | i       3191          |                       |
|                       | a       3130          |                       |
|                       | it      2529          |                       |
|                       | her     2483          |                       |
|                       | was     2400          |                       |
|                       | she     2364          |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | This code can be      |                       |
|                       | simplified using the  |                       |
|                       | [key]{.c004}          |                       |
|                       | parameter of the      |                       |
|                       | [sort]{.c004}         |                       |
|                       | function. If you are  |                       |
|                       | curious, you can read |                       |
|                       | about it at           |                       |
|                       | [[https://wiki        |                       |
|                       | .python.org/moin/HowT |                       |
|                       | o/Sorting]{.c004}](ht |                       |
|                       | tps://wiki.python.org |                       |
|                       | /moin/HowTo/Sorting). |                       |
|                       |                       |                       |
|                       | ## 13                 |                       |
|                       | .5  Optional paramete |                       |
|                       | rs {#sec156 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1166} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1167} |                       |
|                       |                       |                       |
|                       | We have seen built-in |                       |
|                       | functions and methods |                       |
|                       | that take optional    |                       |
|                       | arguments. It is      |                       |
|                       | possible to write     |                       |
|                       | programmer-defined    |                       |
|                       | functions with        |                       |
|                       | optional arguments,   |                       |
|                       | too. For example,     |                       |
|                       | here is a function    |                       |
|                       | that prints the most  |                       |
|                       | common words in a     |                       |
|                       | histogram             |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1168} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1169} |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def print_most_       |                       |
|                       | common(hist, num=10): |                       |
|                       |                       |                       |
|                       | t = most_common(hist) |                       |
|                       |     print('The mos    |                       |
|                       | t common words are:') |                       |
|                       |     for f             |                       |
|                       | req, word in t[:num]: |                       |
|                       |         print(        |                       |
|                       | word, freq, sep='\t') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The first parameter   |                       |
|                       | is required; the      |                       |
|                       | second is optional.   |                       |
|                       | The [default          |                       |
|                       | value]{.c010} of      |                       |
|                       | [num]{.c004} is 10.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1170} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1171} |                       |
|                       |                       |                       |
|                       | If you only provide   |                       |
|                       | one argument:         |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | pr                    |                       |
|                       | int_most_common(hist) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [num]{.c004} gets the |                       |
|                       | default value. If you |                       |
|                       | provide two           |                       |
|                       | arguments:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | print_                |                       |
|                       | most_common(hist, 20) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [num]{.c004} gets the |                       |
|                       | value of the argument |                       |
|                       | instead. In other     |                       |
|                       | words, the optional   |                       |
|                       | argument              |                       |
|                       | [overrides]{.c010}    |                       |
|                       | the default value.    |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1172} |                       |
|                       |                       |                       |
|                       | If a function has     |                       |
|                       | both required and     |                       |
|                       | optional parameters,  |                       |
|                       | all the required      |                       |
|                       | parameters have to    |                       |
|                       | come first, followed  |                       |
|                       | by the optional ones. |                       |
|                       |                       |                       |
|                       | ## 13.6               |                       |
|                       |  Dictionary subtracti |                       |
|                       | on {#sec157 .section} |                       |
|                       |                       |                       |
|                       | []{#dictsub}          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1173} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1174} |                       |
|                       |                       |                       |
|                       | Finding the words     |                       |
|                       | from the book that    |                       |
|                       | are not in the word   |                       |
|                       | list from             |                       |
|                       | [words.txt]{.c004} is |                       |
|                       | a problem you might   |                       |
|                       | recognize as set      |                       |
|                       | subtraction; that is, |                       |
|                       | we want to find all   |                       |
|                       | the words from one    |                       |
|                       | set (the words in the |                       |
|                       | book) that are not in |                       |
|                       | the other (the words  |                       |
|                       | in the list).         |                       |
|                       |                       |                       |
|                       | [subtract]{.c004}     |                       |
|                       | takes dictionaries    |                       |
|                       | [d1]{.c004} and       |                       |
|                       | [d2]{.c004} and       |                       |
|                       | returns a new         |                       |
|                       | dictionary that       |                       |
|                       | contains all the keys |                       |
|                       | from [d1]{.c004} that |                       |
|                       | are not in            |                       |
|                       | [d2]{.c004}. Since we |                       |
|                       | don't really care     |                       |
|                       | about the values, we  |                       |
|                       | set them all to None. |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def subtract(d1, d2): |                       |
|                       |     res = dict()      |                       |
|                       |     for key in d1:    |                       |
|                       |                       |                       |
|                       |     if key not in d2: |                       |
|                       |                       |                       |
|                       |       res[key] = None |                       |
|                       |     return res        |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | To find the words in  |                       |
|                       | the book that are not |                       |
|                       | in                    |                       |
|                       | [words.txt]{.c004},   |                       |
|                       | we can use            |                       |
|                       | `process_file` to     |                       |
|                       | build a histogram for |                       |
|                       | [words.txt]{.c004},   |                       |
|                       | and then subtract:    |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | words = proc          |                       |
|                       | ess_file('words.txt') |                       |
|                       | diff =                |                       |
|                       | subtract(hist, words) |                       |
|                       |                       |                       |
|                       | print("Words i        |                       |
|                       | n the book that aren' |                       |
|                       | t in the word list:") |                       |
|                       | for word in diff:     |                       |
|                       |                       |                       |
|                       |  print(word, end=' ') |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Here are some of the  |                       |
|                       | results from *Emma*:  |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | Words                 |                       |
|                       |  in the book that are |                       |
|                       | n't in the word list: |                       |
|                       | rencontre j           |                       |
|                       | ane's blanche woodhou |                       |
|                       | ses disingenuousness  |                       |
|                       | friend's              |                       |
|                       |  venice apartment ... |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | Some of these words   |                       |
|                       | are names and         |                       |
|                       | possessives. Others,  |                       |
|                       | like "rencontre", are |                       |
|                       | no longer in common   |                       |
|                       | use. But a few are    |                       |
|                       | common words that     |                       |
|                       | should really be in   |                       |
|                       | the list!             |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 6]{.c010}   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1175} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1176} |                       |
|                       |                       |                       |
|                       | *Python provides a    |                       |
|                       | data structure called |                       |
|                       | [set]{.c004} that     |                       |
|                       | provides many common  |                       |
|                       | set operations. You   |                       |
|                       | can read about them   |                       |
|                       | in                    |                       |
|                       | Sect                  |                       |
|                       | ion *[*19.5*](thinkpy |                       |
|                       | thon2020.html#sets)*, |                       |
|                       | or read the           |                       |
|                       | documentation at*     |                       |
|                       | [[*h                  |                       |
|                       | ttp://docs.python.org |                       |
|                       | /3/library/stdtypes.h |                       |
|                       | tml#types-set*]{.c004 |                       |
|                       | }](http://docs.python |                       |
|                       | .org/3/library/stdtyp |                       |
|                       | es.html#types-set)*.* |                       |
|                       |                       |                       |
|                       | *Write a program that |                       |
|                       | uses set subtraction  |                       |
|                       | to find words in the  |                       |
|                       | book that are not in  |                       |
|                       | the word list.        |                       |
|                       | Solution:*            |                       |
|                       | [*[                   |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/analyze_book2 |                       |
|                       | .py]{.c004}*](https:/ |                       |
|                       | /thinkpython.com/code |                       |
|                       | /analyze_book2.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | ## 13.7  Random wor   |                       |
|                       | ds {#sec158 .section} |                       |
|                       |                       |                       |
|                       | []{#randomwords}      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1177} |                       |
|                       |                       |                       |
|                       | To choose a random    |                       |
|                       | word from the         |                       |
|                       | histogram, the        |                       |
|                       | simplest algorithm is |                       |
|                       | to build a list with  |                       |
|                       | multiple copies of    |                       |
|                       | each word, according  |                       |
|                       | to the observed       |                       |
|                       | frequency, and then   |                       |
|                       | choose from the list: |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def random_word(h):   |                       |
|                       |     t = []            |                       |
|                       |     for wor           |                       |
|                       | d, freq in h.items(): |                       |
|                       |         t.            |                       |
|                       | extend([word] * freq) |                       |
|                       |                       |                       |
|                       |     re                |                       |
|                       | turn random.choice(t) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | The expression        |                       |
|                       | [\[word\] \*          |                       |
|                       | freq]{.c004} creates  |                       |
|                       | a list with           |                       |
|                       | [freq]{.c004} copies  |                       |
|                       | of the string         |                       |
|                       | [word]{.c004}. The    |                       |
|                       | [extend]{.c004}       |                       |
|                       | method is similar to  |                       |
|                       | [append]{.c004}       |                       |
|                       | except that the       |                       |
|                       | argument is a         |                       |
|                       | sequence.             |                       |
|                       |                       |                       |
|                       | This algorithm works, |                       |
|                       | but it is not very    |                       |
|                       | efficient; each time  |                       |
|                       | you choose a random   |                       |
|                       | word, it rebuilds the |                       |
|                       | list, which is as big |                       |
|                       | as the original book. |                       |
|                       | An obvious            |                       |
|                       | improvement is to     |                       |
|                       | build the list once   |                       |
|                       | and then make         |                       |
|                       | multiple selections,  |                       |
|                       | but the list is still |                       |
|                       | big.                  |                       |
|                       |                       |                       |
|                       | An alternative is:    |                       |
|                       |                       |                       |
|                       | 1.  Use [keys]{.c004} |                       |
|                       |     to get a list of  |                       |
|                       |     the words in the  |                       |
|                       |     book.             |                       |
|                       | 2.  Build a list that |                       |
|                       |     contains the      |                       |
|                       |     cumulative sum of |                       |
|                       |     the word          |                       |
|                       |     frequencies (see  |                       |
|                       |     Exerc             |                       |
|                       | ise [2](thinkpython20 |                       |
|                       | 11.html#cumulative)). |                       |
|                       |     The last item in  |                       |
|                       |     this list is the  |                       |
|                       |     total number of   |                       |
|                       |     words in the      |                       |
|                       |     book, [n]{.c009}. |                       |
|                       | 3.  Choose a random   |                       |
|                       |     number from 1 to  |                       |
|                       |     [n]{.c009}. Use a |                       |
|                       |     bisection search  |                       |
|                       |     (See              |                       |
|                       |     Exer              |                       |
|                       | cise [10](thinkpython |                       |
|                       | 2011.html#bisection)) |                       |
|                       |     to find the index |                       |
|                       |     where the random  |                       |
|                       |     number would be   |                       |
|                       |     inserted in the   |                       |
|                       |     cumulative sum.   |                       |
|                       | 4.  Use the index to  |                       |
|                       |     find the          |                       |
|                       |     corresponding     |                       |
|                       |     word in the word  |                       |
|                       |     list.             |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 7]{.c010}   |                       |
|                       | []{#randhist}         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1178} |                       |
|                       |                       |                       |
|                       | *Write a program that |                       |
|                       | uses this algorithm   |                       |
|                       | to choose a random    |                       |
|                       | word from the book.   |                       |
|                       | Solution:*            |                       |
|                       | [*[                   |                       |
|                       | https://thinkpython.c |                       |
|                       | om/code/analyze_book3 |                       |
|                       | .py]{.c004}*](https:/ |                       |
|                       | /thinkpython.com/code |                       |
|                       | /analyze_book3.py)*.* |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 13.8  Markov analys |                       |
|                       | is {#sec159 .section} |                       |
|                       |                       |                       |
|                       | []{#markov}           |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1179} |                       |
|                       |                       |                       |
|                       | If you choose words   |                       |
|                       | from the book at      |                       |
|                       | random, you can get a |                       |
|                       | sense of the          |                       |
|                       | vocabulary, but you   |                       |
|                       | probably won't get a  |                       |
|                       | sentence:             |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | this the small regar  |                       |
|                       | d harriet which knigh |                       |
|                       | tley's it most things |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | A series of random    |                       |
|                       | words seldom makes    |                       |
|                       | sense because there   |                       |
|                       | is no relationship    |                       |
|                       | between successive    |                       |
|                       | words. For example,   |                       |
|                       | in a real sentence    |                       |
|                       | you would expect an   |                       |
|                       | article like "the" to |                       |
|                       | be followed by an     |                       |
|                       | adjective or a noun,  |                       |
|                       | and probably not a    |                       |
|                       | verb or adverb.       |                       |
|                       |                       |                       |
|                       | One way to measure    |                       |
|                       | these kinds of        |                       |
|                       | relationships is      |                       |
|                       | Markov analysis,      |                       |
|                       | which characterizes,  |                       |
|                       | for a given sequence  |                       |
|                       | of words, the         |                       |
|                       | probability of the    |                       |
|                       | words that might come |                       |
|                       | next. For example,    |                       |
|                       | the song *Eric, the   |                       |
|                       | Half a Bee* begins:   |                       |
|                       |                       |                       |
|                       | > Half a bee,         |                       |
|                       | > philosophically,\   |                       |
|                       | > Must, ipso facto,   |                       |
|                       | > half not be.\       |                       |
|                       | > But half the bee    |                       |
|                       | > has got to be\      |                       |
|                       | > Vis a vis, its      |                       |
|                       | > entity. D'you see?\ |                       |
|                       | > \                   |                       |
|                       | > But can a bee be    |                       |
|                       | > said to be\         |                       |
|                       | > Or not to be an     |                       |
|                       | > entire bee\         |                       |
|                       | > When half the bee   |                       |
|                       | > is not a bee\       |                       |
|                       | > Due to some ancient |                       |
|                       | > injury?\            |                       |
|                       |                       |                       |
|                       | In this text, the     |                       |
|                       | phrase "half the" is  |                       |
|                       | always followed by    |                       |
|                       | the word "bee", but   |                       |
|                       | the phrase "the bee"  |                       |
|                       | might be followed by  |                       |
|                       | either "has" or "is". |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1180} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1181} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1182} |                       |
|                       |                       |                       |
|                       | The result of Markov  |                       |
|                       | analysis is a mapping |                       |
|                       | from each prefix      |                       |
|                       | (like "half the" and  |                       |
|                       | "the bee") to all     |                       |
|                       | possible suffixes     |                       |
|                       | (like "has" and       |                       |
|                       | "is").                |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1183} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1184} |                       |
|                       |                       |                       |
|                       | Given this mapping,   |                       |
|                       | you can generate a    |                       |
|                       | random text by        |                       |
|                       | starting with any     |                       |
|                       | prefix and choosing   |                       |
|                       | at random from the    |                       |
|                       | possible suffixes.    |                       |
|                       | Next, you can combine |                       |
|                       | the end of the prefix |                       |
|                       | and the new suffix to |                       |
|                       | form the next prefix, |                       |
|                       | and repeat.           |                       |
|                       |                       |                       |
|                       | For example, if you   |                       |
|                       | start with the prefix |                       |
|                       | "Half a", then the    |                       |
|                       | next word has to be   |                       |
|                       | "bee", because the    |                       |
|                       | prefix only appears   |                       |
|                       | once in the text. The |                       |
|                       | next prefix is "a     |                       |
|                       | bee", so the next     |                       |
|                       | suffix might be       |                       |
|                       | "philosophically",    |                       |
|                       | "be" or "due".        |                       |
|                       |                       |                       |
|                       | In this example the   |                       |
|                       | length of the prefix  |                       |
|                       | is always two, but    |                       |
|                       | you can do Markov     |                       |
|                       | analysis with any     |                       |
|                       | prefix length.        |                       |
|                       |                       |                       |
|                       | ::: theorem           |                       |
|                       | [Exercise 8]{.c010}   |                       |
|                       |                       |                       |
|                       | *Markov analysis:*    |                       |
|                       |                       |                       |
|                       | 1.  *Write a program  |                       |
|                       |     to read a text    |                       |
|                       |     from a file and   |                       |
|                       |     perform Markov    |                       |
|                       |     analysis. The     |                       |
|                       |     result should be  |                       |
|                       |     a dictionary that |                       |
|                       |     maps from         |                       |
|                       |     prefixes to a     |                       |
|                       |     collection of     |                       |
|                       |     possible          |                       |
|                       |     suffixes. The     |                       |
|                       |     collection might  |                       |
|                       |     be a list, tuple, |                       |
|                       |     or dictionary; it |                       |
|                       |     is up to you to   |                       |
|                       |     make an           |                       |
|                       |     appropriate       |                       |
|                       |     choice. You can   |                       |
|                       |     test your program |                       |
|                       |     with prefix       |                       |
|                       |     length two, but   |                       |
|                       |     you should write  |                       |
|                       |     the program in a  |                       |
|                       |     way that makes it |                       |
|                       |     easy to try other |                       |
|                       |     lengths.*         |                       |
|                       |                       |                       |
|                       | 2.  *Add a function   |                       |
|                       |     to the previous   |                       |
|                       |     program to        |                       |
|                       |     generate random   |                       |
|                       |     text based on the |                       |
|                       |     Markov analysis.  |                       |
|                       |     Here is an        |                       |
|                       |     example from*     |                       |
|                       |     Emma *with prefix |                       |
|                       |     length 2:*        |                       |
|                       |                       |                       |
|                       |     > *He was very    |                       |
|                       |     > clever, be it   |                       |
|                       |     > sweetness or be |                       |
|                       |     > angry, ashamed  |                       |
|                       |     > or only amused, |                       |
|                       |     > at such a       |                       |
|                       |     > stroke. She had |                       |
|                       |     > never thought   |                       |
|                       |     > of Hannah till  |                       |
|                       |     > you were never  |                       |
|                       |     > meant for me?\" |                       |
|                       |     > \"I cannot make |                       |
|                       |     > speeches,       |                       |
|                       |     > Emma:\" he soon |                       |
|                       |     > cut it all      |                       |
|                       |     > himself.*       |                       |
|                       |                       |                       |
|                       |     *For this         |                       |
|                       |     example, I left   |                       |
|                       |     the punctuation   |                       |
|                       |     attached to the   |                       |
|                       |     words. The result |                       |
|                       |     is almost         |                       |
|                       |     syntactically     |                       |
|                       |     correct, but not  |                       |
|                       |     quite.            |                       |
|                       |     Semantically, it  |                       |
|                       |     almost makes      |                       |
|                       |     sense, but not    |                       |
|                       |     quite.*           |                       |
|                       |                       |                       |
|                       |     *What happens if  |                       |
|                       |     you increase the  |                       |
|                       |     prefix length?    |                       |
|                       |     Does the random   |                       |
|                       |     text make more    |                       |
|                       |     sense?*           |                       |
|                       |                       |                       |
|                       | 3.  *Once your        |                       |
|                       |     program is        |                       |
|                       |     working, you      |                       |
|                       |     might want to try |                       |
|                       |     a mash-up: if you |                       |
|                       |     combine text from |                       |
|                       |     two or more       |                       |
|                       |     books, the random |                       |
|                       |     text you generate |                       |
|                       |     will blend the    |                       |
|                       |     vocabulary and    |                       |
|                       |     phrases from the  |                       |
|                       |     sources in        |                       |
|                       |     interesting       |                       |
|                       |     ways.*            |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1185} |                       |
|                       |                       |                       |
|                       | *Credit: This case    |                       |
|                       | study is based on an  |                       |
|                       | example from          |                       |
|                       | Kernighan and Pike,*  |                       |
|                       | The Practice of       |                       |
|                       | Programming*,         |                       |
|                       | Addison-Wesley,       |                       |
|                       | 1999.*                |                       |
|                       | :::                   |                       |
|                       |                       |                       |
|                       | You should attempt    |                       |
|                       | this exercise before  |                       |
|                       | you go on; then you   |                       |
|                       | can download my       |                       |
|                       | solution from         |                       |
|                       | [[http                |                       |
|                       | s://thinkpython.com/c |                       |
|                       | ode/markov.py]{.c004} |                       |
|                       | ](https://thinkpython |                       |
|                       | .com/code/markov.py). |                       |
|                       | You will also need    |                       |
|                       | [[ht                  |                       |
|                       | tps://thinkpython.com |                       |
|                       | /code/emma.txt]{.c004 |                       |
|                       | }](https://thinkpytho |                       |
|                       | n.com/code/emma.txt). |                       |
|                       |                       |                       |
|                       | #                     |                       |
|                       | # 13.9  Data structur |                       |
|                       | es {#sec160 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1186} |                       |
|                       |                       |                       |
|                       | Using Markov analysis |                       |
|                       | to generate random    |                       |
|                       | text is fun, but      |                       |
|                       | there is also a point |                       |
|                       | to this exercise:     |                       |
|                       | data structure        |                       |
|                       | selection. In your    |                       |
|                       | solution to the       |                       |
|                       | previous exercises,   |                       |
|                       | you had to choose:    |                       |
|                       |                       |                       |
|                       | -   How to represent  |                       |
|                       |     the prefixes.     |                       |
|                       | -   How to represent  |                       |
|                       |     the collection of |                       |
|                       |     possible          |                       |
|                       |     suffixes.         |                       |
|                       | -   How to represent  |                       |
|                       |     the mapping from  |                       |
|                       |     each prefix to    |                       |
|                       |     the collection of |                       |
|                       |     possible          |                       |
|                       |     suffixes.         |                       |
|                       |                       |                       |
|                       | The last one is easy: |                       |
|                       | a dictionary is the   |                       |
|                       | obvious choice for a  |                       |
|                       | mapping from keys to  |                       |
|                       | corresponding values. |                       |
|                       |                       |                       |
|                       | For the prefixes, the |                       |
|                       | most obvious options  |                       |
|                       | are string, list of   |                       |
|                       | strings, or tuple of  |                       |
|                       | strings.              |                       |
|                       |                       |                       |
|                       | For the suffixes, one |                       |
|                       | option is a list;     |                       |
|                       | another is a          |                       |
|                       | histogram             |                       |
|                       | (dictionary).         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1187} |                       |
|                       |                       |                       |
|                       | How should you        |                       |
|                       | choose? The first     |                       |
|                       | step is to think      |                       |
|                       | about the operations  |                       |
|                       | you will need to      |                       |
|                       | implement for each    |                       |
|                       | data structure. For   |                       |
|                       | the prefixes, we need |                       |
|                       | to be able to remove  |                       |
|                       | words from the        |                       |
|                       | beginning and add to  |                       |
|                       | the end. For example, |                       |
|                       | if the current prefix |                       |
|                       | is "Half a", and the  |                       |
|                       | next word is "bee",   |                       |
|                       | you need to be able   |                       |
|                       | to form the next      |                       |
|                       | prefix, "a bee".      |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1188} |                       |
|                       |                       |                       |
|                       | Your first choice     |                       |
|                       | might be a list,      |                       |
|                       | since it is easy to   |                       |
|                       | add and remove        |                       |
|                       | elements, but we also |                       |
|                       | need to be able to    |                       |
|                       | use the prefixes as   |                       |
|                       | keys in a dictionary, |                       |
|                       | so that rules out     |                       |
|                       | lists. With tuples,   |                       |
|                       | you can't append or   |                       |
|                       | remove, but you can   |                       |
|                       | use the addition      |                       |
|                       | operator to form a    |                       |
|                       | new tuple:            |                       |
|                       |                       |                       |
|                       | ``` verbatim          |                       |
|                       | def                   |                       |
|                       |  shift(prefix, word): |                       |
|                       |     return            |                       |
|                       |  prefix[1:] + (word,) |                       |
|                       | ```                   |                       |
|                       |                       |                       |
|                       | [shift]{.c004} takes  |                       |
|                       | a tuple of words,     |                       |
|                       | [prefix]{.c004}, and  |                       |
|                       | a string,             |                       |
|                       | [word]{.c004}, and    |                       |
|                       | forms a new tuple     |                       |
|                       | that has all the      |                       |
|                       | words in              |                       |
|                       | [prefix]{.c004}       |                       |
|                       | except the first, and |                       |
|                       | [word]{.c004} added   |                       |
|                       | to the end.           |                       |
|                       |                       |                       |
|                       | For the collection of |                       |
|                       | suffixes, the         |                       |
|                       | operations we need to |                       |
|                       | perform include       |                       |
|                       | adding a new suffix   |                       |
|                       | (or increasing the    |                       |
|                       | frequency of an       |                       |
|                       | existing one), and    |                       |
|                       | choosing a random     |                       |
|                       | suffix.               |                       |
|                       |                       |                       |
|                       | Adding a new suffix   |                       |
|                       | is equally easy for   |                       |
|                       | the list              |                       |
|                       | implementation or the |                       |
|                       | histogram. Choosing a |                       |
|                       | random element from a |                       |
|                       | list is easy;         |                       |
|                       | choosing from a       |                       |
|                       | histogram is harder   |                       |
|                       | to do efficiently     |                       |
|                       | (see                  |                       |
|                       | Exer                  |                       |
|                       | cise [7](#randhist)). |                       |
|                       |                       |                       |
|                       | So far we have been   |                       |
|                       | talking mostly about  |                       |
|                       | ease of               |                       |
|                       | implementation, but   |                       |
|                       | there are other       |                       |
|                       | factors to consider   |                       |
|                       | in choosing data      |                       |
|                       | structures. One is    |                       |
|                       | run time. Sometimes   |                       |
|                       | there is a            |                       |
|                       | theoretical reason to |                       |
|                       | expect one data       |                       |
|                       | structure to be       |                       |
|                       | faster than other;    |                       |
|                       | for example, I        |                       |
|                       | mentioned that the    |                       |
|                       | [in]{.c004} operator  |                       |
|                       | is faster for         |                       |
|                       | dictionaries than for |                       |
|                       | lists, at least when  |                       |
|                       | the number of         |                       |
|                       | elements is large.    |                       |
|                       |                       |                       |
|                       | But often you don't   |                       |
|                       | know ahead of time    |                       |
|                       | which implementation  |                       |
|                       | will be faster. One   |                       |
|                       | option is to          |                       |
|                       | implement both of     |                       |
|                       | them and see which is |                       |
|                       | better. This approach |                       |
|                       | is called             |                       |
|                       | [                     |                       |
|                       | benchmarking]{.c010}. |                       |
|                       | A practical           |                       |
|                       | alternative is to     |                       |
|                       | choose the data       |                       |
|                       | structure that is     |                       |
|                       | easiest to implement, |                       |
|                       | and then see if it is |                       |
|                       | fast enough for the   |                       |
|                       | intended application. |                       |
|                       | If so, there is no    |                       |
|                       | need to go on. If     |                       |
|                       | not, there are tools, |                       |
|                       | like the              |                       |
|                       | [profile]{.c004}      |                       |
|                       | module, that can      |                       |
|                       | identify the places   |                       |
|                       | in a program that     |                       |
|                       | take the most time.   |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1189} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1190} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1191} |                       |
|                       |                       |                       |
|                       | The other factor to   |                       |
|                       | consider is storage   |                       |
|                       | space. For example,   |                       |
|                       | using a histogram for |                       |
|                       | the collection of     |                       |
|                       | suffixes might take   |                       |
|                       | less space because    |                       |
|                       | you only have to      |                       |
|                       | store each word once, |                       |
|                       | no matter how many    |                       |
|                       | times it appears in   |                       |
|                       | the text. In some     |                       |
|                       | cases, saving space   |                       |
|                       | can also make your    |                       |
|                       | program run faster,   |                       |
|                       | and in the extreme,   |                       |
|                       | your program might    |                       |
|                       | not run at all if you |                       |
|                       | run out of memory.    |                       |
|                       | But for many          |                       |
|                       | applications, space   |                       |
|                       | is a secondary        |                       |
|                       | consideration after   |                       |
|                       | run time.             |                       |
|                       |                       |                       |
|                       | One final thought: in |                       |
|                       | this discussion, I    |                       |
|                       | have implied that we  |                       |
|                       | should use one data   |                       |
|                       | structure for both    |                       |
|                       | analysis and          |                       |
|                       | generation. But since |                       |
|                       | these are separate    |                       |
|                       | phases, it would also |                       |
|                       | be possible to use    |                       |
|                       | one structure for     |                       |
|                       | analysis and then     |                       |
|                       | convert to another    |                       |
|                       | structure for         |                       |
|                       | generation. This      |                       |
|                       | would be a net win if |                       |
|                       | the time saved during |                       |
|                       | generation exceeded   |                       |
|                       | the time spent in     |                       |
|                       | conversion.           |                       |
|                       |                       |                       |
|                       | ## 13.10  Debuggi     |                       |
|                       | ng {#sec161 .section} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1192} |                       |
|                       |                       |                       |
|                       | When you are          |                       |
|                       | debugging a program,  |                       |
|                       | and especially if you |                       |
|                       | are working on a hard |                       |
|                       | bug, there are five   |                       |
|                       | things to try:        |                       |
|                       |                       |                       |
|                       | [Reading:]{.c010}     |                       |
|                       | :   Examine your      |                       |
|                       |     code, read it     |                       |
|                       |     back to yourself, |                       |
|                       |     and check that it |                       |
|                       |     says what you     |                       |
|                       |     meant to say.     |                       |
|                       |                       |                       |
|                       | [Running:]{.c010}     |                       |
|                       | :   Experiment by     |                       |
|                       |     making changes    |                       |
|                       |     and running       |                       |
|                       |     different         |                       |
|                       |     versions. Often   |                       |
|                       |     if you display    |                       |
|                       |     the right thing   |                       |
|                       |     at the right      |                       |
|                       |     place in the      |                       |
|                       |     program, the      |                       |
|                       |     problem becomes   |                       |
|                       |     obvious, but      |                       |
|                       |     sometimes you     |                       |
|                       |     have to build     |                       |
|                       |     scaffolding.      |                       |
|                       |                       |                       |
|                       | [Ruminating:]{.c010}  |                       |
|                       | :   Take some time to |                       |
|                       |     think! What kind  |                       |
|                       |     of error is it:   |                       |
|                       |     syntax, runtime,  |                       |
|                       |     or semantic? What |                       |
|                       |     information can   |                       |
|                       |     you get from the  |                       |
|                       |     error messages,   |                       |
|                       |     or from the       |                       |
|                       |     output of the     |                       |
|                       |     program? What     |                       |
|                       |     kind of error     |                       |
|                       |     could cause the   |                       |
|                       |     problem you're    |                       |
|                       |     seeing? What did  |                       |
|                       |     you change last,  |                       |
|                       |     before the        |                       |
|                       |     problem appeared? |                       |
|                       |                       |                       |
|                       | [R                    |                       |
|                       | ubberducking:]{.c010} |                       |
|                       | :   If you explain    |                       |
|                       |     the problem to    |                       |
|                       |     someone else, you |                       |
|                       |     sometimes find    |                       |
|                       |     the answer before |                       |
|                       |     you finish asking |                       |
|                       |     the question.     |                       |
|                       |     Often you don't   |                       |
|                       |     need the other    |                       |
|                       |     person; you could |                       |
|                       |     just talk to a    |                       |
|                       |     rubber duck. And  |                       |
|                       |     that's the origin |                       |
|                       |     of the well-known |                       |
|                       |     strategy called   |                       |
|                       |     [rubber duck      |                       |
|                       |                       |                       |
|                       |    debugging]{.c010}. |                       |
|                       |     I am not making   |                       |
|                       |     this up; see      |                       |
|                       |     [[https://e       |                       |
|                       | n.wikipedia.org/wiki/ |                       |
|                       | Rubber_duck_debugging |                       |
|                       | ]{.c004}](https://en. |                       |
|                       | wikipedia.org/wiki/Ru |                       |
|                       | bber_duck_debugging). |                       |
|                       |                       |                       |
|                       | [Retreating:]{.c010}  |                       |
|                       | :   At some point,    |                       |
|                       |     the best thing to |                       |
|                       |     do is back off,   |                       |
|                       |     undoing recent    |                       |
|                       |     changes, until    |                       |
|                       |     you get back to a |                       |
|                       |     program that      |                       |
|                       |     works and that    |                       |
|                       |     you understand.   |                       |
|                       |     Then you can      |                       |
|                       |     start rebuilding. |                       |
|                       |                       |                       |
|                       | Beginning programmers |                       |
|                       | sometimes get stuck   |                       |
|                       | on one of these       |                       |
|                       | activities and forget |                       |
|                       | the others. Each      |                       |
|                       | activity comes with   |                       |
|                       | its own failure mode. |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1193} |                       |
|                       |                       |                       |
|                       | For example, reading  |                       |
|                       | your code might help  |                       |
|                       | if the problem is a   |                       |
|                       | typographical error,  |                       |
|                       | but not if the        |                       |
|                       | problem is a          |                       |
|                       | conceptual            |                       |
|                       | misunderstanding. If  |                       |
|                       | you don't understand  |                       |
|                       | what your program     |                       |
|                       | does, you can read it |                       |
|                       | 100 times and never   |                       |
|                       | see the error,        |                       |
|                       | because the error is  |                       |
|                       | in your head.         |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1194} |                       |
|                       |                       |                       |
|                       | Running experiments   |                       |
|                       | can help, especially  |                       |
|                       | if you run small,     |                       |
|                       | simple tests. But if  |                       |
|                       | you run experiments   |                       |
|                       | without thinking or   |                       |
|                       | reading your code,    |                       |
|                       | you might fall into a |                       |
|                       | pattern I call        |                       |
|                       | "random walk          |                       |
|                       | programming", which   |                       |
|                       | is the process of     |                       |
|                       | making random changes |                       |
|                       | until the program     |                       |
|                       | does the right thing. |                       |
|                       | Needless to say,      |                       |
|                       | random walk           |                       |
|                       | programming can take  |                       |
|                       | a long time.          |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1195} |                       |
|                       | [                     |                       |
|                       | ]{#hevea_default1196} |                       |
|                       |                       |                       |
|                       | You have to take time |                       |
|                       | to think. Debugging   |                       |
|                       | is like an            |                       |
|                       | experimental science. |                       |
|                       | You should have at    |                       |
|                       | least one hypothesis  |                       |
|                       | about what the        |                       |
|                       | problem is. If there  |                       |
|                       | are two or more       |                       |
|                       | possibilities, try to |                       |
|                       | think of a test that  |                       |
|                       | would eliminate one   |                       |
|                       | of them.              |                       |
|                       |                       |                       |
|                       | But even the best     |                       |
|                       | debugging techniques  |                       |
|                       | will fail if there    |                       |
|                       | are too many errors,  |                       |
|                       | or if the code you    |                       |
|                       | are trying to fix is  |                       |
|                       | too big and           |                       |
|                       | complicated.          |                       |
|                       | Sometimes the best    |                       |
|                       | option is to retreat, |                       |
|                       | simplifying the       |                       |
|                       | program until you get |                       |
|                       | to something that     |                       |
|                       | works and that you    |                       |
|                       | understand.           |                       |
|                       |                       |                       |
|                       | Beginning programmers |                       |
|                       | are often reluctant   |                       |
|                       | to retreat because    |                       |
|                       | they can't stand to   |                       |
|                       | delete a line of code |                       |
|                       | (even if it's wrong). |                       |
|                       | If it makes you feel  |                       |
|                       | better, copy your     |                       |
|                       | program into another  |                       |
|                       | file before you start |                       |
|                       | stripping it down.    |                       |
|                       | Then you can copy the |                       |
|                       | pieces back one at a  |                       |
|                       | time.                 |                       |
|                       |                       |                       |
|                       | Finding a hard bug    |                       |
|                       | requires reading,     |                       |
|                       | running, ruminating,  |                       |
|                       | and sometimes         |                       |
|                       | retreating. If you    |                       |
|                       | get stuck on one of   |                       |
|                       | these activities, try |                       |
|                       | the others.           |                       |
|                       |                       |                       |
|                       | ## 13.11  Glossa      |                       |
|                       | ry {#sec162 .section} |                       |
|                       |                       |                       |
|                       | [d                    |                       |
|                       | eterministic:]{.c010} |                       |
|                       | :   Pertaining to a   |                       |
|                       |     program that does |                       |
|                       |     the same thing    |                       |
|                       |     each time it      |                       |
|                       |     runs, given the   |                       |
|                       |     same inputs.      |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1197} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | pseudorandom:]{.c010} |                       |
|                       | :   Pertaining to a   |                       |
|                       |     sequence of       |                       |
|                       |     numbers that      |                       |
|                       |     appears to be     |                       |
|                       |     random, but is    |                       |
|                       |     generated by a    |                       |
|                       |     deterministic     |                       |
|                       |     program.          |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1198} |                       |
|                       |                       |                       |
|                       | [d                    |                       |
|                       | efault value:]{.c010} |                       |
|                       | :   The value given   |                       |
|                       |     to an optional    |                       |
|                       |     parameter if no   |                       |
|                       |     argument is       |                       |
|                       |     provided.         |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1199} |                       |
|                       |                       |                       |
|                       | [override:]{.c010}    |                       |
|                       | :   To replace a      |                       |
|                       |     default value     |                       |
|                       |     with an argument. |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1200} |                       |
|                       |                       |                       |
|                       | [                     |                       |
|                       | benchmarking:]{.c010} |                       |
|                       | :   The process of    |                       |
|                       |     choosing between  |                       |
|                       |     data structures   |                       |
|                       |     by implementing   |                       |
|                       |     alternatives and  |                       |
|                       |     testing them on a |                       |
|                       |     sample of the     |                       |
|                       |     possible inputs.  |                       |
|                       |     [                 |                       |
|                       | ]{#hevea_default1201} |                       |
|                       |                       |                       |
|                       | [rubber du            |                       |
|                       | ck debugging:]{.c010} |                       |
|                       | :   Debugging by      |                       |
|                       |     explaining your   |                       |
|                       |     problem to an     |                       |
|                       |     inanimate object  |                       |
|                       |     such as a rubber  |                       |
|                       | 